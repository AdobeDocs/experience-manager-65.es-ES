---
title: API de JavaScript de Client Context
seo-title: API de JavaScript de Client Context
description: La API de Javascript para Client Context
seo-description: La API de Javascript para Client Context
uuid: be58998c-f23e-4768-8394-1f1ad3994c4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: a6e5810b-dac5-4137-93cf-5d8d53cacc49
feature: Context Hub
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3165'
ht-degree: 4%

---


# API de JavaScript de Client Context{#client-context-javascript-api}

## CQ_Analytics.ClientContextMgr {#cq-analytics-clientcontextmgr}

El objeto CQ_Analytics.ClientContextMgr es un singleton que contiene un conjunto de almacenes de sesión autoregistrados y proporciona métodos para registrar, mantener y administrar los almacenes de sesión.

Extiende CQ_Analytics.PersistedSessionStore.

### Métodos {#methods}

#### getRegisteredStore(name) {#getregisteredstore-name}

Devuelve un almacén de sesiones de un nombre especificado. Consulte también [Acceso a un almacén de sesiones](/help/sites-developing/client-context.md#accessing-session-stores).

**Parámetros**

* nombre: Cadena. Nombre del almacén de sesión.

**Devuelve**

Un objeto CQ_Analytics.SessionStore que representa el almacén de sesión del nombre dado. Devuelve `null` cuando no existe ningún almacén del nombre dado.

#### register(sessionstore) {#register-sessionstore}

Registra un almacén de sesiones con Client Context. Activa los eventos storeregister y storeupdate una vez finalizados.

**Parámetros**

* sessionstore: CQ_Analytics.SessionStore. El objeto de almacén de sesión que se va a registrar.

**Devuelve**

No devuelve ningún valor.

## CQ_Analytics.ClientContextUtils {#cq-analytics-clientcontextutils}

Proporciona métodos para escuchar la activación y el registro del almacén de sesiones. Consulte también [Comprobación de que un almacén de sesión está definido e iniciado](/help/sites-developing/client-context.md#checking-that-a-session-store-is-defined-and-initialized).

### Métodos {#methods-1}

#### onStoreInitialized(storeName, callback, delay) {#onstoreinitialized-storename-callback-delay}

Registra una función de llamada de retorno a la que se llama cuando se inicializa un almacén de sesiones. Para las tiendas que se inicializan varias veces, especifique un retraso de llamada de retorno para que la función de llamada de retorno se llame solo una vez:

* Cuando el almacén se inicializa durante el periodo de retraso de una inicialización anterior, la llamada a la función anterior se cancela y se vuelve a llamar a la función para la inicialización actual.
* Si el periodo de retardo transcurre antes de que se produzca una inicialización posterior, la función de llamada de retorno se ejecuta dos veces.

Por ejemplo, un almacén de sesiones se basa en un objeto JSON y se recupera mediante una solicitud JSON. Los siguientes escenarios de inicialización son posibles:

* La solicitud se completa y los datos se recuperan y se cargan en el almacén. En este caso, la inicialización se produce una vez.
* La solicitud falla (tiempo de espera). En este caso, la inicialización no se produce y no hay datos en el almacén.
* El almacén se rellena previamente con valores predeterminados (propiedades init), pero la solicitud falla (tiempo de espera). Solo hay una inicialización con valores predeterminados.
* La tienda está rellenada previamente.

Cuando el retraso se establece en `true` o en un número de milisegundos, el método espera antes de llamar al método de rellamada. Si se activa otro evento de inicialización antes de que se pase el retraso, esperará hasta que se supere el tiempo de retraso sin ningún evento de inicialización. Esto permite esperar a que se active un segundo evento de inicialización y llama a la función de llamada de retorno en el caso más óptimo.

**Parámetros**

* storeName: Cadena. El nombre del almacén de sesiones para agregar el oyente.
* llamada de retorno: Función. La función a la que se llama al inicializar el almacén.
* retraso: Boolean o Number. Tiempo que se tarda en retrasar la llamada a la función de rellamada, en milisegundos. Un valor booleano de `true` utiliza el retardo predeterminado de `200 ms`. Un valor booleano de `false` o un número negativo hacen que no se utilice ningún retraso.

**Devuelve**

No devuelve ningún valor.

#### onStoreRegistered(storeName, callback) {#onstoreregistered-storename-callback}

Registra una función de llamada de retorno a la que se llama cuando se registra un almacén de sesiones. El evento de registro se produce cuando un almacén está registrado en [CQ_Analytics.ClientContextMgr](#cq-analytics-clientcontextmgr).

**Parámetros**

* storeName: Cadena. El nombre del almacén de sesiones para agregar el oyente.
* llamada de retorno: Función. La función a la que se llama al inicializar el almacén.

**Devuelve**

No devuelve ningún valor.

## CQ_Analytics.JSONPStore {#cq-analytics-jsonpstore}

Un almacén de sesiones no persistente que contiene datos JSON. Los datos se recuperan de un servicio JSONP externo. Utilice el método `getInstance` o `getRegisteredInstance` para crear una instancia de esta clase.

Extiende CQ_Analytics.JSONStore.

### Propiedades {#properties}

Consulte CQ_Analytics.JSONStore y CQ_Analytics.SessonStore para ver las propiedades heredadas.

### Métodos {#methods-2}

Consulte también CQ_Analytics.JSONStore y CQ_Analytics.SessionStore para conocer los métodos heredados.

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback}

Crea un objeto CQ_Analytics.JSONPStore.

**Parámetros**

* storeName: Cadena. Nombre que se utilizará como propiedad STORENAME. El valor de la propiedad STOREKEY se establece en storeName con todos los caracteres en mayúsculas. Si no se proporciona storeName, el método devuelve null.
* serviceURL: Cadena. La URL del servicio JSONP
* dynamicData: (Opcional) Objeto. Los datos JSON para anexar a los datos de inicialización del almacén antes de llamar a la función de llamada de retorno.
* deferLoading: (Opcional) Booleano. Un valor de true evita que se llame al servicio JSONP durante la creación del objeto. Un valor false hace que se llame al servicio JSONP.
* loadingCallback: (Opcional) Cadena. Nombre de la función a la que se va a llamar para procesar el objeto JSONP que devuelve el servicio JSONP. La función de llamada de retorno debe definir un solo parámetro que sea un objeto CQ_Analytics.JSONPStore.

**Devuelve**

El nuevo objeto CQ_Analytics.JSONPStore, o nulo si storeName es nulo.

#### getServiceURL() {#getserviceurl}

Recupera la URL del servicio JSONP que este objeto utiliza para recuperar datos JSON.

**Parámetros**

Ninguna.

**Devuelve**

Cadena que representa la dirección URL del servicio o nulo si no se ha configurado ninguna dirección URL del servicio.

#### load(serviceURL, dynamicData, callback) {#load-serviceurl-dynamicdata-callback}

Llama al servicio JSONP. La URL de JSONP es la URL de servicio con el sufijo de un nombre de función de llamada de retorno determinado.

**Parámetros**

* serviceURL: (Opcional) Cadena. El servicio JSONP al que llamar. Un valor de null hace que se utilice la URL de servicio ya configurada. Un valor no nulo establece el servicio JSONP que se utilizará para este objeto. (Consulte setServiceURL.)
* dynamicData: (Opcional) Objeto. Los datos JSON para anexar a los datos de inicialización del almacén antes de llamar a la función de llamada de retorno.
* llamada de retorno: (Opcional) Cadena. Nombre de la función a la que se va a llamar para procesar el objeto JSONP que devuelve el servicio JSONP. La función de llamada de retorno debe definir un solo parámetro que sea un objeto CQ_Analytics.JSONPStore.

**Devuelve**

No devuelve ningún valor.

#### registerNewInstance(storeName, serviceURL, dynamicData, callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback}

Crea un objeto CQ_Analytics.JSONPStore y registra el almacén con Client Context.

**Parámetros**

* storeName: Cadena. Nombre que se utilizará como propiedad STORENAME. El valor de la propiedad STOREKEY se establece en storeName con todos los caracteres en mayúsculas. Si no se proporciona storeName, el método devuelve null.
* serviceURL: (Opcional) Cadena. La URL del servicio JSONP.
* dynamicData: (Opcional) Objeto. Los datos JSON para anexar a los datos de inicialización del almacén antes de llamar a la función de llamada de retorno.
* llamada de retorno: (Opcional) Cadena. Nombre de la función a la que se va a llamar para procesar el objeto JSONP que devuelve el servicio JSONP. La función de llamada de retorno debe definir un solo parámetro que sea un objeto CQ_Analytics.JSONPStore.

**Devuelve**

El objeto CQ_Analytics.JSONPStore registrado.

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl}

Establece la URL del servicio JSONP que se utiliza para recuperar datos JSON.

**Parámetros**

* serviceURL: Cadena. La URL del servicio JSONP que proporciona datos JSON

**Devuelve**

No devuelve ningún valor.

## CQ_Analytics.JSONStore {#cq-analytics-jsonstore}

Un contenedor para un objeto JSON. Cree una instancia de esta clase para crear un almacén de sesiones no persistente que contenga datos JSON:

`myjsonstore = new CQ_Analytics.JSONStore`

Puede definir un conjunto de datos que rellene el almacén tras la inicialización.

Extiende CQ_Analytics.SessionStore.

### Propiedades {#properties-1}

#### STOREKEY {#storekey}

La clave que identifica el almacén. Utilice el método `getInstance` para recuperar este valor.

#### STORENAME {#storename}

Nombre de la tienda. Utilice el método `getInstance` para recuperar este valor.

### Métodos {#methods-3}

Consulte también CQ_Analytics.SessionStore para conocer los métodos heredados.

#### borrar() {#clear}

Quita los datos del almacén de sesión y todas las propiedades de inicialización.

**Parámetros**

Ninguna.

**Devuelve**

No devuelve ningún valor.

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata}

Crea un objeto CQ_Analytics.JSONStore con un nombre determinado e inicializado con los datos JSON dados (llama al método initJSON).

**Parámetros**

* storeName: Cadena. Nombre que se utilizará como propiedad STORENAME. El valor de la propiedad STOREKEY se establece en storeName con todos los caracteres en mayúsculas.
* jsonData: Objeto. Un objeto que contiene datos JSON.

**Devuelve**

El objeto CQ_Analytics.JSONStore.

#### getJSON() {#getjson}

Recupera los datos del almacén de sesión en formato JSON.

**Parámetros**

Ninguna.

**Devuelve**

Un objeto que representa los datos almacenados en formato JSON.

#### init() {#init}

Borra el almacén de sesiones y lo inicializa con la propiedad de inicialización. Establece el indicador de inicialización en `true` y, a continuación, activa los eventos `initialize` y `update`.

**Parámetros**

Ninguna.

**Devuelve**

No devuelve datos.

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear}

Crea propiedades de inicialización a partir de los datos en un objeto JSON. Si lo desea, puede quitar todas las propiedades de inicialización existentes.

Los nombres de las propiedades se derivan de la jerarquía de los datos en el objeto JSON. El siguiente código de ejemplo representa un objeto JSON:

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

Para este ejemplo, se crean las siguientes propiedades en el almacén:

```xml
A: "valueA"
B/B1: "valueBB1"
```

**Parámetros**

* jsonData: Un objeto JSON que contiene los datos que se van a almacenar.
* doNotClear: El valor true conserva las propiedades de inicialización existentes y agrega las derivadas del objeto JSON. El valor false elimina las propiedades de inicialización existentes antes de añadir las derivadas del objeto JSON.

**Devuelve**

No devuelve ningún valor.

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata}

Crea un objeto CQ_Analytics.JSONStore con un nombre determinado e inicializado con los datos JSON dados (llama al método initJSON). El nuevo objeto se registra automáticamente en el Administrador de nube de flujo de navegación.

**Parámetros**

* storeName: Cadena. Nombre que se utilizará como propiedad STORENAME. El valor de la propiedad STOREKEY se establece en storeName con todos los caracteres en mayúsculas.
* jsonData: Objeto. Un objeto que contiene datos JSON.

**Devuelve**

El objeto CQ_Analytics.JSONStore.

## CQ_Analytics.Observable {#cq-analytics-observable}

Activa eventos y permite que otros objetos escuchen estos eventos y reaccionen. Las clases que amplían esta clase pueden activar eventos que provocan que se llame a los oyentes.

### Métodos {#methods-4}

#### addListener(event, fct, scope) {#addlistener-event-fct-scope}

Registra un oyente para un evento. Consulte también [Creación de un oyente para reaccionar ante una actualización de almacén de sesiones](/help/sites-developing/client-context.md#creating-a-listener-to-react-to-a-session-store-update).

**Parámetros**

* evento: Cadena. Nombre del evento que se va a escuchar.
* fct: Función. Función a la que se llama cuando se produce el evento.
* ámbito: (Opcional) Objeto. El ámbito en el que se ejecutará la función de controlador. El contexto &quot;this&quot; de la función del controlador.

**Devuelve**

No devuelve ningún valor.

#### removeListener(event, fct) {#removelistener-event-fct}

Quita el controlador de eventos dado para un evento.

**Parámetros**

* evento: Cadena. Nombre del evento.
* fct: Función. El controlador de eventos.

**Devuelve**

No devuelve ningún valor.

## CQ_Analytics.PersistedJSONPStore {#cq-analyics-persistedjsonpstore}

Contenedor persistente de un objeto JSON recuperado de un servicio JSONP remoto.

Extiende CQ_Analytics.PersistedJSONStore.

### Métodos {#methods-5}

Consulte también CQ_Analytics.PersistedJSONStore para conocer los métodos heredados.

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback-1}

Crea un objeto CQ_Analytics.PersistedJSONPStore.

**Parámetros**

* storeName: Cadena. Nombre que se utilizará como propiedad STORENAME. El valor de la propiedad STOREKEY se establece en storeName con todos los caracteres en mayúsculas. Si no se proporciona storeName, el método devuelve null.
* serviceURL: Cadena. La URL del servicio JSONP
* dynamicData: (Opcional) Objeto. Los datos JSON para anexar a los datos de inicialización del almacén antes de llamar a la función de llamada de retorno.
* deferLoading: (Opcional) Booleano. Un valor de true evita que se llame al servicio JSONP durante la creación del objeto. Un valor false hace que se llame al servicio JSONP.
* loadingCallback: (Opcional) Cadena. Nombre de la función a la que se va a llamar para procesar el objeto JSONP que devuelve el servicio JSONP. La función de llamada de retorno debe definir un solo parámetro que sea un objeto CQ_Analytics.JSONPStore.

**Devuelve**

El nuevo objeto CQ_Analytics.PersistedJSONPStore o nulo si storeName es nulo.

#### getServiceURL() {#getserviceurl-1}

Recupera la URL del servicio JSONP que este objeto utiliza para recuperar datos JSON.

**Parámetros**

Ninguna.

**Devuelve**

Cadena que representa la dirección URL del servicio o nulo si no se ha configurado ninguna dirección URL del servicio.

#### load(serviceURL, dynamicData, callback) {#load-serviceurl-dynamicdata-callback-1}

Llama al servicio JSONP. La URL de JSONP es la URL de servicio con el sufijo de un nombre de función de llamada de retorno determinado.

**Parámetros**

* serviceURL: (Opcional) Cadena. El servicio JSONP al que llamar. Un valor de null hace que se utilice la URL de servicio ya configurada. Un valor no nulo establece el servicio JSONP que se utilizará para este objeto. (Consulte setServiceURL.)
* dynamicData: (Opcional) Objeto. Los datos JSON para anexar a los datos de inicialización del almacén antes de llamar a la función de llamada de retorno.
* llamada de retorno: (Opcional) Cadena. Nombre de la función a la que se va a llamar para procesar el objeto JSONP que devuelve el servicio JSONP. La función de llamada de retorno debe definir un solo parámetro que sea un objeto CQ_Analytics.JSONPStore.

**Devuelve**

No devuelve ningún valor.

#### registerNewInstance(storeName, serviceURL, dynamicData, callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback-1}

Crea un objeto CQ_Analytics.PersistedJSONPStore y registra el almacén con Client Context.

**Parámetros**

* storeName: Cadena. Nombre que se utilizará como propiedad STORENAME. El valor de la propiedad STOREKEY se establece en storeName con todos los caracteres en mayúsculas. Si no se proporciona storeName, el método devuelve null.
* serviceURL: (Opcional) Cadena. La URL del servicio JSONP.
* dynamicData: (Opcional) Objeto. Los datos JSON para anexar a los datos de inicialización del almacén antes de llamar a la función de llamada de retorno.
* llamada de retorno: (Opcional) Cadena. Nombre de la función a la que se va a llamar para procesar el objeto JSONP que devuelve el servicio JSONP. La función de llamada de retorno debe definir un solo parámetro que sea un objeto CQ_Analytics.JSONPStore.

**Devuelve**

El objeto CQ_Analytics.PersistedJSONPStore registrado.

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl-1}

Establece la URL del servicio JSONP que se utiliza para recuperar datos JSON.

**Parámetros**

* serviceURL: Cadena. La URL del servicio JSONP que proporciona datos JSON

**Devuelve**

No devuelve ningún valor.

## CQ_Analytics.PersistedJSONStore {#cq-analytics-persistedjsonstore}

Contenedor persistente de un objeto JSON.

Amplía `CQ_Analytics.PersistedSessionStore`.

### Propiedades {#properties-2}

#### STOREKEY {#storekey-1}

La clave que identifica el almacén. Utilice el método `getInstance` para recuperar este valor.

#### STORENAME {#storename-1}

Nombre de la tienda. Utilice el método `getInstance` para recuperar este valor.

### Métodos {#methods-6}

Consulte también CQ_Analytics.PersistedSessionStore para conocer los métodos heredados.

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata-1}

Crea un objeto CQ_Analytics.PersistedJSONStore con un nombre determinado e inicializado con los datos JSON dados (llama al método initJSON ).

**Parámetros**

* storeName: Cadena. Nombre que se utilizará como propiedad STORENAME. El valor de la propiedad STOREKEY se establece en storeName con todos los caracteres en mayúsculas.
* jsonData: Objeto. Un objeto que contiene datos JSON.

**Devuelve**

El objeto CQ_Analytics.PersistedJSONStore .

#### getJSON() {#getjson-1}

Recupera los datos del almacén de sesión en formato JSON.

**Parámetros**

Ninguna.

**Devuelve**

Un objeto que representa los datos almacenados en formato JSON.

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear-1}

Crea propiedades de inicialización a partir de los datos en un objeto JSON. Si lo desea, puede quitar todas las propiedades de inicialización existentes.

Los nombres de las propiedades se derivan de la jerarquía de los datos en el objeto JSON. El siguiente código de ejemplo representa un objeto JSON:

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

Para este ejemplo, se crean las siguientes propiedades en el almacén:

```xml
A: "valueA"
B/B1: "valueBB1"
```

**Parámetros**

* jsonData: Un objeto JSON que contiene los datos que se van a almacenar.
* doNotClear: El valor true conserva las propiedades de inicialización existentes y agrega las derivadas del objeto JSON. El valor false elimina las propiedades de inicialización existentes antes de añadir las derivadas del objeto JSON.

**Devuelve**

No devuelve ningún valor.

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata-1}

Crea un objeto CQ_Analytics.PersistedJSONStore con un nombre determinado e inicializado con los datos JSON dados (llama al método initJSON ). El nuevo objeto se registra automáticamente con Client Context Manager.

**Parámetros**

* storeName: Cadena. Nombre que se utilizará como propiedad STORENAME. El valor de la propiedad STOREKEY se establece en storeName con todos los caracteres en mayúsculas.
* jsonData: Objeto. Un objeto que contiene datos JSON.

**Devuelve**

El objeto CQ_Analytics.PersistedJSONStore .

## CQ_Analytics.PersistedSessionStore {#cq-analytics-persistedsessionstore}

Un contenedor de propiedades y valores. Los datos se mantienen utilizando CQ_Analytics.SessionPersistence. Cree una instancia de esta clase para crear un almacén de sesiones persistente:

`mypersistedstore = new CQ_Analytics.PersistedSessionStore`

Extiende CQ_Analytics.SessionStore.

### Propiedades {#properties-3}

#### STOREKEY {#storekey-2}

El valor predeterminado es `key`.

### Métodos {#methods-7}

Consulte CQ_Analytics.SessionStore para conocer los métodos heredados.

Cuando se utilizan los métodos heredados `clear`, `setProperty`, `setProperties`, `removeProperty` para cambiar los datos del almacén, los cambios se mantienen automáticamente, a menos que las propiedades cambiadas se marquen como no persistentes.

#### getStoreKey() {#getstorekey}

Recupera la propiedad `STOREKEY`.

**Parámetros**

Ninguna

**Devuelve**

El valor de la propiedad `STOREKEY`.

#### isPersisted(name) {#ispersisted-name}

Determina si se mantiene una propiedad de datos.

**Parámetros**

* nombre: Cadena. Nombre de la propiedad.

**Devuelve**

Un valor booleano de `true` si la propiedad se mantiene y un valor de `false` si el valor no es una propiedad persistente.

#### persist() {#persist}

Mantiene el almacén de sesiones. El modo de persistencia predeterminado usa el explorador `localStorage` usando `ClientSidePersistence` como nombre ( `window.localStorage.set("ClientSidePersistance", store);`)

Si localStorage no está disponible o no se puede escribir, el almacén se mantiene como una propiedad de la ventana.

Activa el evento `persist` al completarse.

**Parámetros**

Ninguna

**Devuelve**

No devuelve ningún valor.

#### reset(deferEvent) {#reset-deferevent}

Quita todas las propiedades de datos del almacén y lo conserva. Opcionalmente, no activa el evento `udpate` al completarse.

**Parámetros**

* deferEvent: El valor true evita que se active el evento `update`. Un valor de `false` hace que el evento de actualización se active.

**Devuelve**

No devuelve ningún valor.

#### setNonPersisted(name) {#setnonpersisted-name}

Marca una propiedad de datos como no persistente.

**Parámetros**

* nombre: Cadena. Nombre de la propiedad que no se va a mantener.

**Devuelve**

Sin valor devuelto.

## CQ_Analytics.SessionStore {#cq-analytics-sessionstore}

CQ_Analytics.SessionStore representa un almacén de sesiones. Cree una instancia de esta clase para crear un almacén de sesiones:

`mystore = new CQ_Analytics.SessionStore`

Amplía CQ_Analytics.Observable.

### Propiedades {#properties-4}

#### STORENAME {#storename-2}

Nombre del almacén de sesión. Utilice getName para recuperar el valor de esta propiedad.

### Métodos {#methods-8}

#### addInitProperty(name, value) {#addinitproperty-name-value}

Agrega una propiedad y un valor a los datos de inicialización del almacén de sesión.

Utilice loadInitProperties para rellenar los datos del almacén de sesión con los valores de inicialización.

**Parámetros**

* nombre: Cadena. Nombre de la propiedad que se va a añadir.
* valor: Cadena. El valor de la propiedad que se va a añadir.

**Devuelve**

No devuelve ningún valor.

#### borrar() {#clear-1}

Quita todas las propiedades de datos del almacén.

**Parámetros**

Ninguna.

**Devuelve**

Sin valor devuelto.

#### getData(excluded) {#getdata-excluded}

Devuelve los datos del almacén. Opcionalmente, excluye las propiedades de nombre de los datos. Llama al método `init` si la propiedad data del almacén no existe.

**Parámetros**

excluido: (Opcional) Una matriz de nombres de propiedades para excluir de los datos devueltos.

**Devuelve**

Un objeto de propiedades y sus valores.

#### getInitProperty(name) {#getinitproperty-name}

Recupera el valor de una propiedad data.

**Parámetros**

* nombre: Cadena. Nombre de la propiedad de datos que se va a recuperar.

**Devuelve**

El valor de la propiedad data. Devuelve `null` si el almacén de sesiones no contiene ninguna propiedad del nombre dado.

#### getName() {#getname}

Devuelve el nombre del almacén de sesiones.

**Parámetros**

Ninguna.

**Devuelve**

Valor de cadena que representa el nombre del almacén.

#### getProperty(name, raw) {#getproperty-name-raw}

Devuelve el valor de una propiedad. El valor se devuelve como la propiedad raw o el valor filtrado por XSS. Llama al método `init` si la propiedad data del almacén no existe.

**Parámetros**

* nombre: Cadena. Nombre de la propiedad de datos que se va a recuperar.
* sin procesar: Booleano. Un valor de true hace que se devuelva el valor de propiedad sin procesar. El valor false hace que el valor devuelto se filtre con XSS.

**Devuelve**

El valor de la propiedad data.

#### getPropertyNames(excluded) {#getpropertynames-excluded}

Devuelve los nombres de las propiedades que contiene el almacén de sesiones. Llama al método `init` si la propiedad data del almacén no existe.

**Parámetros**

excluido: (Opcional) Matriz de nombres de propiedad para omitir de los resultados.

**Devuelve**

Matriz de valores de cadena que representan los nombres de propiedades de sesión.

#### getSessionStore() {#getsessionstore}

Devuelve el almacén de sesión adjunto al objeto actual.

**Parámetros**

Ninguna.

**Devuelve**

this

#### init() {#init-1}

Marca el almacén como inicializado y activa el evento `initialize`.

**Parámetros**

Ninguna.

**Devuelve**

No devuelve ningún valor.

#### isInitialized() {#isinitialized}

Indica si el almacén de sesiones está inicializado.

**Parámetros**

Ninguna.

**Devuelve**

Un valor de `true` si el almacén se inicializa y un valor de `false` si el almacén no se inicializa.

#### loadInitProperties(obj, setValues) {#loadinitproperties-obj-setvalues}

Agrega las propiedades de un objeto determinado a los datos de inicialización del almacén de sesiones. Opcionalmente, los datos del objeto también se agregan a los datos de almacenamiento.

**Parámetros**

* obj: Un objeto que contiene propiedades enumerables.
* setValues: Cuando se establece en true, las propiedades obj se añaden a los datos del almacén de sesión si los datos del almacén no incluyen ya una propiedad del mismo nombre. Cuando es false, no se agregan datos a los datos del almacén de sesión.

**Devuelve**

No devuelve ningún valor.

#### removeProperty(name) {#removeproperty-name}

Quita una propiedad del almacén de sesiones. Activa el evento `update` al completarse. Llama al método `init` si la propiedad data del almacén no existe.

**Parámetros**

* nombre: Cadena. Nombre de la propiedad que se va a quitar.

**Devuelve**

No devuelve ningún valor.

#### reset() {#reset}

Restaura los valores iniciales del almacén de datos. La implementación predeterminada simplemente elimina todos los datos. Activa el evento `update` al completarse.

**Parámetros**

Ninguna.

**Devuelve**

No devuelve ningún valor.

#### setProperties(properties) {#setproperties-properties}

Define los valores de varias propiedades. Activa el evento `update` al completarse. Llama al método `init` si la propiedad data del almacén no existe.

**Parámetros**

* Propiedades: Objeto. Un objeto que contiene propiedades enumerables. Cada nombre y valor de propiedad se agrega al almacén.

**Devuelve**

No devuelve ningún valor.

#### setProperty(name, value) {#setproperty-name-value}

Define el valor de una propiedad. Activa el evento `update` al completarse. Llama al método `init` si la propiedad data del almacén no existe.

**Parámetros**

* nombre: Cadena. Nombre de la propiedad.
* valor: Cadena. Valor de propiedad.

**Devuelve**

No devuelve ningún valor.
