---
title: API de JavaScript de ClientContext
seo-title: API de JavaScript de ClientContext
description: La API de Javascript para Client Context
seo-description: La API de Javascript para Client Context
uuid: be58998c-f23e-4768-8394-1f1ad3994c4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: a6e5810b-dac5-4137-93cf-5d8d53cacc49
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '3163'
ht-degree: 4%

---


# API de JavaScript de ClientContext{#client-context-javascript-api}

## CQ_Analytics.ClientContextMgr {#cq-analytics-clientcontextmgr}

El objeto CQ_Analytics.ClientContextMgr es un singleton que contiene un conjunto de almacenes de sesiones autoregistrados y proporciona métodos para registrar, mantener y administrar los almacenes de sesiones.

Extiende CQ_Analytics.PersistedSessionStore.

### Métodos {#methods}

#### getRegisteredStore(nombre) {#getregisteredstore-name}

Devuelve un almacén de sesiones con un nombre especificado. Consulte también [Acceso a un almacén de sesiones](/help/sites-developing/client-context.md#accessing-session-stores).

**Parámetros**

* name: Cadena. Nombre del almacén de sesiones.

**Devuelve**

Un objeto CQ_Analytics.SessionStore que representa el almacén de sesiones del nombre dado. Devuelve `null` cuando no existe ningún almacén del nombre dado.

#### register(sessionstore) {#register-sessionstore}

Registra un almacén de sesiones con ClientContext. Activa los eventos de registro de almacenamiento y actualización de almacenamiento una vez finalizados.

**Parámetros**

* sessionstore: CQ_Analytics.SessionStore. El objeto del almacén de sesiones que se va a registrar.

**Devuelve**

No se devolvió ningún valor.

## CQ_Analytics.ClientContextUtils {#cq-analytics-clientcontextutils}

Proporciona métodos para escuchar la activación y el registro del almacén de sesiones. Consulte también [Comprobación de que un almacén de sesiones está definido e inicializado](/help/sites-developing/client-context.md#checking-that-a-session-store-is-defined-and-initialized).

### Métodos {#methods-1}

#### onStoreInitialized(storeName, callback, delay) {#onstoreinitialized-storename-callback-delay}

Registra una función de llamada de retorno que se llama cuando se inicializa un almacén de sesiones. Para las tiendas inicializadas varias veces, especifique un retraso de llamada de retorno para que la función de llamada de retorno se llame una sola vez:

* Cuando el almacén se inicializa durante el período de retraso de una inicialización anterior, se cancela la llamada a la función anterior y se vuelve a llamar a la función para la inicialización actual.
* Si el período de demora se agota antes de que se produzca una inicialización posterior, la función de llamada de retorno se ejecuta dos veces.

Por ejemplo, un almacén de sesiones se basa en un objeto JSON y se recupera mediante una solicitud JSON. Los siguientes escenarios de inicialización son posibles:

* La solicitud se ha completado, los datos se recuperan y se cargan en el almacén. En este caso, la inicialización se produce una vez.
* La solicitud falla (tiempo de espera). En este caso, la inicialización no se produce y no hay datos en el almacén.
* El almacén se rellena previamente con valores predeterminados (propiedades init), pero la solicitud falla (tiempo de espera). Solo hay una inicialización con valores predeterminados.
* La tienda está prerrellenada.

Cuando el retraso se establece en `true` o en un número de milisegundos, el método espera antes de llamar al método de llamada de retorno. Si se activa otro evento de inicialización antes de que se pase el retraso, esperará hasta que se supere el tiempo de demora sin ningún evento de inicialización. Esto permite esperar a que se active un segundo evento de inicialización y llama a la función de llamada de retorno en el caso más óptimo.

**Parámetros**

* storeName: Cadena. Nombre del almacén de sesiones para agregar el detector.
* llamada de retorno: Función. La función a la que se llama al inicializar el almacén.
* retraso: Boolean o Number. Cantidad de tiempo que se tarda en retrasar la llamada a la función de llamada de retorno, en milisegundos. Un valor booleano `true` utiliza la demora predeterminada de `200 ms`. Un valor booleano de `false` o un número negativo hace que no se utilice ningún retraso.

**Devuelve**

No se devolvió ningún valor.

#### onStoreRegistered(storeName, callback) {#onstoreregistered-storename-callback}

Registra una función de llamada de retorno que se llama cuando se registra un almacén de sesiones. El evento de registro se produce cuando un almacén está registrado en [CQ_Analytics.ClientContextMgr](#cq-analytics-clientcontextmgr).

**Parámetros**

* storeName: Cadena. Nombre del almacén de sesiones para agregar el detector.
* llamada de retorno: Función. La función a la que se llama al inicializar el almacén.

**Devuelve**

No se devolvió ningún valor.

## CQ_Analytics.JSONPStore {#cq-analytics-jsonpstore}

Almacén de sesiones no persistente que contiene datos JSON. Los datos se recuperan de un servicio JSONP externo. Utilice el método `getInstance` o `getRegisteredInstance` para crear una instancia de esta clase.

Extiende CQ_Analytics.JSONStore.

### Propiedades {#properties}

Consulte CQ_Analytics.JSONStore y CQ_Analytics.SessonStore para ver las propiedades heredadas.

### Métodos {#methods-2}

Consulte también CQ_Analytics.JSONStore y CQ_Analytics.SessonStore para conocer los métodos heredados.

#### getInstance(storeName, serviceURL, dynamicData, posterLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback}

Crea un objeto CQ_Analytics.JSONPStore.

**Parámetros**

* storeName: Cadena. Nombre que se va a utilizar como propiedad STORENAME. El valor de la propiedad STOREKEY se establece en storeName con todos los caracteres en mayúsculas. Si no se proporciona storeName, el método devuelve null.
* serviceURL: Cadena. Dirección URL del servicio JSONP
* dynamicData: (Opcional). Datos JSON para anexar a los datos de inicialización del almacén antes de llamar a la función de llamada de retorno.
* deferLoading: (Opcional) Booleano. Un valor true evita que se llame al servicio JSONP al crear objetos. Un valor false hace que se llame al servicio JSONP.
* loadingCallback: (Opcional) Cadena. Nombre de la función que se va a llamar para procesar el objeto JSONP que devuelve el servicio JSONP. La función de llamada de retorno debe definir un solo parámetro que sea un objeto CQ_Analytics.JSONPStore.

**Devuelve**

El nuevo objeto CQ_Analytics.JSONPStore o null si storeName es nulo.

#### getServiceURL() {#getserviceurl}

Recupera la dirección URL del servicio JSONP que utiliza este objeto para recuperar datos JSON.

**Parámetros**

Ninguna.

**Devuelve**

Cadena que representa la dirección URL del servicio o nulo si no se ha configurado ninguna dirección URL del servicio.

#### load(serviceURL, dynamicData, callback) {#load-serviceurl-dynamicdata-callback}

Llama al servicio JSONP. La URL de JSONP es la URL del servicio con el sufijo de un nombre de función de devolución de llamada.

**Parámetros**

* serviceURL: (Opcional) Cadena. El servicio JSONP al que llamar. Un valor nulo hace que se utilice la URL de servicio ya configurada. Un valor que no sea nulo establece el servicio JSONP que se utilizará para este objeto. (Consulte setServiceURL.)
* dynamicData: (Opcional). Datos JSON para anexar a los datos de inicialización del almacén antes de llamar a la función de llamada de retorno.
* llamada de retorno: (Opcional) Cadena. Nombre de la función que se va a llamar para procesar el objeto JSONP que devuelve el servicio JSONP. La función de llamada de retorno debe definir un solo parámetro que sea un objeto CQ_Analytics.JSONPStore.

**Devuelve**

No se devolvió ningún valor.

#### registerNewInstance(storeName, serviceURL, dynamicData, callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback}

Crea un objeto CQ_Analytics.JSONPStore y registra la tienda con Client Context.

**Parámetros**

* storeName: Cadena. Nombre que se va a utilizar como propiedad STORENAME. El valor de la propiedad STOREKEY se establece en storeName con todos los caracteres en mayúsculas. Si no se proporciona storeName, el método devuelve null.
* serviceURL: (Opcional) Cadena. Dirección URL del servicio JSONP.
* dynamicData: (Opcional). Datos JSON para anexar a los datos de inicialización del almacén antes de llamar a la función de llamada de retorno.
* llamada de retorno: (Opcional) Cadena. Nombre de la función que se va a llamar para procesar el objeto JSONP que devuelve el servicio JSONP. La función de llamada de retorno debe definir un solo parámetro que sea un objeto CQ_Analytics.JSONPStore.

**Devuelve**

El objeto CQ_Analytics.JSONPStore registrado.

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl}

Establece la dirección URL del servicio JSONP que se utilizará para recuperar datos JSON.

**Parámetros**

* serviceURL: Cadena. Dirección URL del servicio JSONP que proporciona datos JSON

**Devuelve**

No se devolvió ningún valor.

## CQ_Analytics.JSONStore {#cq-analytics-jsonstore}

Un contenedor para un objeto JSON. Cree una instancia de esta clase para crear un almacén de sesiones no persistente que contenga datos JSON:

`myjsonstore = new CQ_Analytics.JSONStore`

Puede definir un conjunto de datos que rellene el almacén tras la inicialización.

Extiende CQ_Analytics.SessionStore.

### Propiedades {#properties-1}

#### STOREKEY {#storekey}

Clave que identifica la tienda. Utilice el método `getInstance` para recuperar este valor.

#### STORENAME {#storename}

El nombre de la tienda. Utilice el método `getInstance` para recuperar este valor.

### Métodos {#methods-3}

Consulte también CQ_Analytics.SessionStore para ver los métodos heredados.

#### borrar() {#clear}

Elimina los datos del almacén de sesiones y todas las propiedades de inicialización.

**Parámetros**

Ninguna.

**Devuelve**

No se devolvió ningún valor.

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata}

Crea un objeto CQ_Analytics.JSONStore con un nombre determinado e inicializado con los datos JSON dados (llama al método initJSON).

**Parámetros**

* storeName: Cadena. Nombre que se va a utilizar como propiedad STORENAME. El valor de la propiedad STOREKEY se establece en storeName con todos los caracteres en mayúsculas.
* jsonData: Objeto. Objeto que contiene datos JSON.

**Devuelve**

El objeto CQ_Analytics.JSONStore.

#### getJSON() {#getjson}

Recupera los datos del almacén de sesiones en formato JSON.

**Parámetros**

Ninguna.

**Devuelve**

Objeto que representa los datos almacenados en formato JSON.

#### init() {#init}

Borra el almacén de sesiones y lo inicializa con la propiedad de inicialización. Establece el indicador de inicialización en `true` y, a continuación, activa los eventos `initialize` y `update`.

**Parámetros**

Ninguna.

**Devuelve**

No se devolvieron datos.

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear}

Crea propiedades de inicialización a partir de los datos de un objeto JSON. Si lo desea, puede quitar todas las propiedades de inicialización existentes.

Los nombres de las propiedades se derivan de la jerarquía de los datos en el objeto JSON. El siguiente código de ejemplo representa un objeto JSON:

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

En este ejemplo, se crean las siguientes propiedades en la tienda:

```xml
A: "valueA"
B/B1: "valueBB1"
```

**Parámetros**

* jsonData: Un objeto JSON que contiene los datos que se van a almacenar.
* doNotClear: Un valor true preserva las propiedades de inicialización existentes y agrega las derivadas del objeto JSON. Un valor false elimina las propiedades de inicialización existentes antes de agregar las derivadas del objeto JSON.

**Devuelve**

No se devolvió ningún valor.

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata}

Crea un objeto CQ_Analytics.JSONStore con un nombre determinado e inicializado con los datos JSON dados (llama al método initJSON). El nuevo objeto se registra automáticamente con el Administrador de nube de secuencias de clic.

**Parámetros**

* storeName: Cadena. Nombre que se va a utilizar como propiedad STORENAME. El valor de la propiedad STOREKEY se establece en storeName con todos los caracteres en mayúsculas.
* jsonData: Objeto. Objeto que contiene datos JSON.

**Devuelve**

El objeto CQ_Analytics.JSONStore.

## CQ_Analytics.Observable {#cq-analytics-observable}

Dispara eventos y permite que otros objetos escuchen estos eventos y reaccionen. Las clases que amplían esta clase pueden activar eventos que provocan que se llame a los oyentes.

### Métodos {#methods-4}

#### addListener(evento, fct, scope) {#addlistener-event-fct-scope}

Registra un detector de un evento. Consulte también [Creación de un detector para reaccionar ante una actualización del almacén de sesiones](/help/sites-developing/client-context.md#creating-a-listener-to-react-to-a-session-store-update).

**Parámetros**

* evento: Cadena. El nombre del evento que escuchar.
* fct: Función. Función a la que se llama cuando se produce el evento.
* ámbito: (Opcional). Ámbito en el que se ejecuta la función de controlador. El contexto &quot;this&quot; de la función de controlador.

**Devuelve**

No se devolvió ningún valor.

#### removeListener(evento, fct) {#removelistener-event-fct}

Quita el controlador de evento dado para un evento.

**Parámetros**

* evento: Cadena. El nombre del evento.
* fct: Función. El controlador de evento.

**Devuelve**

No se devolvió ningún valor.

## CQ_Analytics.PersistedJSONPStore {#cq-analyics-persistedjsonpstore}

Contenedor persistente de un objeto JSON recuperado de un servicio JSONP remoto.

Extiende CQ_Analytics.PersistedJSONStore.

### Métodos {#methods-5}

Consulte también CQ_Analytics.PersistedJSONStore para conocer los métodos heredados.

#### getInstance(storeName, serviceURL, dynamicData, posterLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback-1}

Crea un objeto CQ_Analytics.PersistedJSONPStore.

**Parámetros**

* storeName: Cadena. Nombre que se va a utilizar como propiedad STORENAME. El valor de la propiedad STOREKEY se establece en storeName con todos los caracteres en mayúsculas. Si no se proporciona storeName, el método devuelve null.
* serviceURL: Cadena. Dirección URL del servicio JSONP
* dynamicData: (Opcional). Datos JSON para anexar a los datos de inicialización del almacén antes de llamar a la función de llamada de retorno.
* deferLoading: (Opcional) Booleano. Un valor true evita que se llame al servicio JSONP al crear objetos. Un valor false hace que se llame al servicio JSONP.
* loadingCallback: (Opcional) Cadena. Nombre de la función que se va a llamar para procesar el objeto JSONP que devuelve el servicio JSONP. La función de llamada de retorno debe definir un solo parámetro que sea un objeto CQ_Analytics.JSONPStore.

**Devuelve**

El nuevo objeto CQ_Analytics.PersistedJSONPStore o nulo si storeName es nulo.

#### getServiceURL() {#getserviceurl-1}

Recupera la dirección URL del servicio JSONP que utiliza este objeto para recuperar datos JSON.

**Parámetros**

Ninguna.

**Devuelve**

Cadena que representa la dirección URL del servicio o nulo si no se ha configurado ninguna dirección URL del servicio.

#### load(serviceURL, dynamicData, callback) {#load-serviceurl-dynamicdata-callback-1}

Llama al servicio JSONP. La URL de JSONP es la URL del servicio con el sufijo de un nombre de función de devolución de llamada.

**Parámetros**

* serviceURL: (Opcional) Cadena. El servicio JSONP al que llamar. Un valor nulo hace que se utilice la dirección URL de servicio ya configurada. Un valor que no sea nulo establece el servicio JSONP que se utilizará para este objeto. (Consulte setServiceURL.)
* dynamicData: (Opcional). Datos JSON para anexar a los datos de inicialización del almacén antes de llamar a la función de llamada de retorno.
* llamada de retorno: (Opcional) Cadena. Nombre de la función que se va a llamar para procesar el objeto JSONP que devuelve el servicio JSONP. La función de llamada de retorno debe definir un solo parámetro que sea un objeto CQ_Analytics.JSONPStore.

**Devuelve**

No se devolvió ningún valor.

#### registerNewInstance(storeName, serviceURL, dynamicData, callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback-1}

Crea un objeto CQ_Analytics.PersistedJSONPStore y registra la tienda con Client Context.

**Parámetros**

* storeName: Cadena. Nombre que se va a utilizar como propiedad STORENAME. El valor de la propiedad STOREKEY se establece en storeName con todos los caracteres en mayúsculas. Si no se proporciona storeName, el método devuelve null.
* serviceURL: (Opcional) Cadena. Dirección URL del servicio JSONP.
* dynamicData: (Opcional). Datos JSON para anexar a los datos de inicialización del almacén antes de llamar a la función de llamada de retorno.
* llamada de retorno: (Opcional) Cadena. Nombre de la función que se va a llamar para procesar el objeto JSONP que devuelve el servicio JSONP. La función de llamada de retorno debe definir un solo parámetro que sea un objeto CQ_Analytics.JSONPStore.

**Devuelve**

El objeto CQ_Analytics.PersistedJSONPStore registrado.

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl-1}

Establece la dirección URL del servicio JSONP que se utilizará para recuperar datos JSON.

**Parámetros**

* serviceURL: Cadena. Dirección URL del servicio JSONP que proporciona datos JSON

**Devuelve**

No se devolvió ningún valor.

## CQ_Analytics.PersistedJSONStore {#cq-analytics-persistedjsonstore}

Contenedor persistente de un objeto JSON.

Extiende `CQ_Analytics.PersistedSessionStore`.

### Propiedades {#properties-2}

#### STOREKEY {#storekey-1}

Clave que identifica la tienda. Utilice el método `getInstance` para recuperar este valor.

#### STORENAME {#storename-1}

El nombre de la tienda. Utilice el método `getInstance` para recuperar este valor.

### Métodos {#methods-6}

Consulte también CQ_Analytics.PersistedSessionStore para ver los métodos heredados.

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata-1}

Crea un objeto CQ_Analytics.PersistedJSONStore con un nombre determinado e inicializado con los datos JSON dados (llama al método initJSON).

**Parámetros**

* storeName: Cadena. Nombre que se va a utilizar como propiedad STORENAME. El valor de la propiedad STOREKEY se establece en storeName con todos los caracteres en mayúsculas.
* jsonData: Objeto. Objeto que contiene datos JSON.

**Devuelve**

El objeto CQ_Analytics.PersistedJSONStore.

#### getJSON() {#getjson-1}

Recupera los datos del almacén de sesiones en formato JSON.

**Parámetros**

Ninguna.

**Devuelve**

Objeto que representa los datos almacenados en formato JSON.

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear-1}

Crea propiedades de inicialización a partir de los datos de un objeto JSON. Si lo desea, puede quitar todas las propiedades de inicialización existentes.

Los nombres de las propiedades se derivan de la jerarquía de los datos en el objeto JSON. El siguiente código de ejemplo representa un objeto JSON:

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

En este ejemplo, se crean las siguientes propiedades en la tienda:

```xml
A: "valueA"
B/B1: "valueBB1"
```

**Parámetros**

* jsonData: Un objeto JSON que contiene los datos que se van a almacenar.
* doNotClear: Un valor true preserva las propiedades de inicialización existentes y agrega las derivadas del objeto JSON. Un valor false elimina las propiedades de inicialización existentes antes de agregar las derivadas del objeto JSON.

**Devuelve**

No se devolvió ningún valor.

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata-1}

Crea un objeto CQ_Analytics.PersistedJSONStore con un nombre determinado e inicializado con los datos JSON dados (llama al método initJSON). El nuevo objeto se registra automáticamente con Client Context Manager.

**Parámetros**

* storeName: Cadena. Nombre que se va a utilizar como propiedad STORENAME. El valor de la propiedad STOREKEY se establece en storeName con todos los caracteres en mayúsculas.
* jsonData: Objeto. Objeto que contiene datos JSON.

**Devuelve**

El objeto CQ_Analytics.PersistedJSONStore.

## CQ_Analytics.PersistedSessionStore {#cq-analytics-persistedsessionstore}

Un contenedor de propiedades y valores. Los datos se conservan con CQ_Analytics.SessionPersistence. Cree una instancia de esta clase para crear un almacén de sesiones persistente:

`mypersistedstore = new CQ_Analytics.PersistedSessionStore`

Extiende CQ_Analytics.SessionStore.

### Propiedades {#properties-3}

#### STOREKEY {#storekey-2}

El valor predeterminado es `key`.

### Métodos {#methods-7}

Consulte CQ_Analytics.SessionStore para conocer los métodos heredados.

Cuando se utilizan los métodos heredados `clear`, `setProperty`, `setProperties`, `removeProperty` para cambiar los datos del almacén, los cambios se mantienen automáticamente, a menos que las propiedades cambiadas se marquen como noPersisted.

#### getStoreKey() {#getstorekey}

Recupera la propiedad `STOREKEY`.

**Parámetros**

Ninguna

**Devuelve**

El valor de la propiedad `STOREKEY`.

#### isPersisted(name) {#ispersisted-name}

Determina si se mantiene una propiedad de datos.

**Parámetros**

* name: Cadena. Nombre de la propiedad.

**Devuelve**

Un valor booleano de `true` si la propiedad se mantiene y un valor de `false` si el valor no es una propiedad persistente.

#### persist() {#persist}

Persiste el almacén de sesiones. El modo de persistencia predeterminado utiliza el explorador `localStorage` usando `ClientSidePersistence` como nombre ( `window.localStorage.set("ClientSidePersistance", store);`)

Si localStorage no está disponible o no se puede escribir en él, el almacén se mantiene como propiedad de la ventana.

Activa el evento `persist` una vez finalizado.

**Parámetros**

Ninguna

**Devuelve**

No se devolvió ningún valor.

#### reset(deferEvent) {#reset-deferevent}

Quita todas las propiedades de datos del almacén y lo mantiene. Opcionalmente, no activa el evento `udpate` una vez finalizado.

**Parámetros**

* deferEvent: Un valor true evita que se active el evento `update`. Un valor de `false` hace que el evento de actualización se active.

**Devuelve**

No se devolvió ningún valor.

#### setNonPersisted(name) {#setnonpersisted-name}

Marca una propiedad de datos como no persistente.

**Parámetros**

* name: Cadena. Nombre de la propiedad que no se va a mantener.

**Devuelve**

No hay ningún valor devuelto.

## CQ_Analytics.SessionStore {#cq-analytics-sessionstore}

CQ_Analytics.SessionStore representa un almacén de sesiones. Cree una instancia de esta clase para crear un almacén de sesiones:

`mystore = new CQ_Analytics.SessionStore`

Extiende CQ_Analytics.Observable.

### Propiedades {#properties-4}

#### STORENAME {#storename-2}

Nombre del almacén de sesiones. Utilice getName para recuperar el valor de esta propiedad.

### Métodos {#methods-8}

#### addInitProperty(nombre, valor) {#addinitproperty-name-value}

Añade una propiedad y un valor a los datos de inicialización del almacén de sesiones.

Utilice loadInitProperties para rellenar los datos del almacén de sesión con los valores de inicialización.

**Parámetros**

* name: Cadena. Nombre de la propiedad que se va a agregar.
* value: Cadena. Valor de la propiedad que se va a agregar.

**Devuelve**

No se devolvió ningún valor.

#### borrar() {#clear-1}

Quita todas las propiedades de datos del almacén.

**Parámetros**

Ninguna.

**Devuelve**

No hay ningún valor devuelto.

#### getData(excluido) {#getdata-excluded}

Devuelve los datos del almacén. Opcionalmente, excluye las propiedades de nombre de los datos. Llama al método `init` si la propiedad data del almacén no existe.

**Parámetros**

excluido: (Opcional) Una matriz de nombres de propiedades para excluir de los datos devueltos.

**Devuelve**

Objeto de propiedades y sus valores.

#### getInitProperty(name) {#getinitproperty-name}

Recupera el valor de una propiedad de datos.

**Parámetros**

* name: Cadena. Nombre de la propiedad de datos que se va a recuperar.

**Devuelve**

El valor de la propiedad data. Devuelve `null` si el almacén de sesiones no contiene ninguna propiedad del nombre dado.

#### getName() {#getname}

Devuelve el nombre del almacén de sesiones.

**Parámetros**

Ninguna.

**Devuelve**

Un valor de cadena que representa el nombre del almacén.

#### getProperty(name, raw) {#getproperty-name-raw}

Devuelve el valor de una propiedad. El valor se devuelve como la propiedad raw o el valor filtrado por XSS. Llama al método `init` si la propiedad data del almacén no existe.

**Parámetros**

* name: Cadena. Nombre de la propiedad de datos que se va a recuperar.
* raw: Booleano. Un valor de true hace que se devuelva el valor de propiedad sin procesar. Un valor false hace que el valor devuelto se filtre con XSS.

**Devuelve**

El valor de la propiedad data.

#### getPropertyNames(excluded) {#getpropertynames-excluded}

Devuelve los nombres de las propiedades que contiene el almacén de sesiones. Llama al método `init` si la propiedad data del almacén no existe.

**Parámetros**

excluido: (Opcional) Una matriz de nombres de propiedades para omitir los resultados.

**Devuelve**

Matriz de valores de tipo String que representan los nombres de propiedad session.

#### getSessionStore() {#getsessionstore}

Devuelve el almacén de sesiones adjunto al objeto actual.

**Parámetros**

Ninguna.

**Devuelve**

this

#### init() {#init-1}

Marca el almacén como inicializado y activa el evento `initialize`.

**Parámetros**

Ninguna.

**Devuelve**

No se devolvió ningún valor.

#### isInitialized() {#isinitialized}

Indica si se ha inicializado el almacén de sesiones.

**Parámetros**

Ninguna.

**Devuelve**

Un valor de `true` si se inicializa el almacén y un valor de `false` si no se inicializa el almacén.

#### loadInitProperties(obj, setValues) {#loadinitproperties-obj-setvalues}

Añade las propiedades de un objeto determinado en los datos de inicialización del almacén de sesiones. Opcionalmente, los datos de objeto también se agregan a los datos del almacén.

**Parámetros**

* obj: Objeto que contiene propiedades enumerables.
* setValues: Cuando es true, las propiedades obj se agregan a los datos del almacén de sesión si los datos del almacén no incluyen ya una propiedad del mismo nombre. Si es false, no se agregan datos a los datos del almacén de sesiones.

**Devuelve**

No se devolvió ningún valor.

#### removeProperty(name) {#removeproperty-name}

Quita una propiedad del almacén de sesiones. Activa el evento `update` una vez finalizado. Llama al método `init` si la propiedad data del almacén no existe.

**Parámetros**

* name: Cadena. Nombre de la propiedad que se va a quitar.

**Devuelve**

No se devolvió ningún valor.

#### reset() {#reset}

Restaura los valores iniciales del almacén de datos. La implementación predeterminada simplemente elimina todos los datos. Activa el evento `update` una vez finalizado.

**Parámetros**

Ninguna.

**Devuelve**

No se devolvió ningún valor.

#### setProperties(properties) {#setproperties-properties}

Establece los valores de varias propiedades. Activa el evento `update` una vez finalizado. Llama al método `init` si la propiedad data del almacén no existe.

**Parámetros**

* Propiedades: Objeto. Objeto que contiene propiedades enumerables. Cada nombre y valor de propiedad se agrega al almacén.

**Devuelve**

No se devolvió ningún valor.

#### setProperty(name, value) {#setproperty-name-value}

Define el valor de una propiedad. Activa el evento `update` una vez finalizado. Llama al método `init` si la propiedad data del almacén no existe.

**Parámetros**

* name: Cadena. Nombre de la propiedad.
* value: Cadena. Valor de propiedad.

**Devuelve**

No se devolvió ningún valor.
