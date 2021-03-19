---
title: Referencia de la API de JavaScript de ContextHub
seo-title: Referencia de la API de JavaScript de ContextHub
description: La API de JavaScript de ContextHub está disponible para los scripts cuando el componente ContextHub se ha agregado a la página
seo-description: La API de JavaScript de ContextHub está disponible para los scripts cuando el componente ContextHub se ha agregado a la página
uuid: 296d6c8e-517f-4837-9e86-ae571ea8aa17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 90605f41-1861-4891-a7c8-b8b5918cd5c6
feature: Context Hub
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '5031'
ht-degree: 3%

---


# Referencia de la API de JavaScript de ContextHub{#contexthub-javascript-api-reference}

La API de JavaScript de ContextHub está disponible para los scripts cuando el componente [ContextHub se ha agregado a la página](/help/sites-developing/ch-adding.md#adding-contexthub-to-a-page-component).

## Constantes de ContextHub {#contexthub-constants}

Valores constantes que define la API de JavaScript de ContextHub.

### Constantes de eventos {#event-constants}

En la tabla siguiente se enumeran los eventos de nombre que se producen en las tiendas de ContextHub. Consulte también [ContextHub.Utils.Event](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing).

| Constante | Descripción | Value |
|---|---|---|
| ContextHub.Constants.EVENT_NAMESPACE | Área de nombres de eventos de ContextHub | ch |
| ContextHub.Constants.EVENT_ALL_STORES_READY | Indica que todas las tiendas requeridas están registradas, inicializadas y listas para ser consumidas | all-store-ready |
| ContextHub.Constants.EVENT_STORES_PARTIALLY_READY | Indica que no todas las tiendas se inicializaron dentro de un tiempo de espera determinado | store-part-ready |
| ContextHub.Constants.EVENT_STORE_REGISTERED | Se activa cuando se registra una tienda | registrado en el almacén |
| ContextHub.Constants.EVENT_STORE_READY | Indica que las tiendas están listas para funcionar. Se activa inmediatamente después del registro, excepto en los almacenes JSONP, donde se activa cuando se recuperan datos). | listo para almacenar |
| ContextHub.Constants.EVENT_STORE_UPDATED | Se activa cuando una tienda actualiza su persistencia | store-update |
| ContextHub.Constants.PERSISTENCE_CONTAINER_NAME | Nombre del contenedor de persistencia | Persistencia de ContextHub |
| ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY | Almacena el nombre de clave de persistencia específico donde se almacena el resultado JSON sin procesar | /_/raw-response |
| ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY | Almacena una marca de hora específica que indica cuándo se recuperaron los datos JSON | /_/response-time |
| ContextHub.Constants.SERVICE_LAST_URL_KEY | Almacena la url específica del servicio JSON utilizado durante la última llamada | /_/url |
| ContextHub.Constants.IS_CONTAINER_EXPANDED | Indica si la interfaz de usuario de ContextHub está expandida | /_/container-expand |

### Constantes de eventos de interfaz de usuario {#ui-event-constants}

En la tabla siguiente se enumeran los nombres de los eventos que se producen en la interfaz de usuario de ContextHub.

| **Constante** | **Descripción** | **Value** |
|---|---|---|
| ContextHub.Constants.EVENT_UI_MODE_REGISTERED | Se activa cuando se registra un modo | ui-mode registrado |
| ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED | Se activa cuando un modo no está registrado | ui-mode-unregister |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED | Se activa cuando se registra un renderizador de modo | ui-mode-renderer-register |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED | Se activa cuando un renderizador de modo no está registrado | ui-mode-renderer-unregister |
| ContextHub.Constants.EVENT_UI_MODE_ADDED | Se activa cuando se agrega un nuevo modo | ui-mode-added |
| ContextHub.Constants.EVENT_UI_MODE_REMOVED | Se activa cuando se elimina un modo | ui-mode-remove |
| ContextHub.Constants.EVENT_UI_MODE_SELECTED | Se activa cuando el usuario selecciona un modo | ui-mode-selected |
| ContextHub.Constants.EVENT_UI_MODULE_REGISTERED | Se activa cuando se registra un nuevo módulo | ui-module-register |
| ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED | Se activa cuando un módulo no está registrado | ui-module-unregister |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED | Se activa cuando se registra un renderizador de módulo | ui-module-renderer-register |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED | Se activa cuando un renderizador de módulo no está registrado | ui-module-renderer-unregister |
| ContextHub.Constants.EVENT_UI_MODULE_ADDED | Se activa cuando se agrega un nuevo módulo | ui-module-added |
| ContextHub.Constants.EVENT_UI_MODULE_REMOVED | Se activa cuando se elimina un módulo | ui-module-remove |
| ContextHub.Constants.EVENT_UI_CONTAINER_ADDED | Se activa cuando el contenedor de interfaz de usuario se agrega a la página | ui-container-added |
| ContextHub.Constants.EVENT_UI_CONTAINER_OPENED | Se activa cuando se abre la interfaz de usuario de ContextHub | ui-container abierto |
| ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED | Se activa cuando la interfaz de usuario de ContextHub está contraída | ui-container-closed |
| ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED | Se activa cuando se modifica una propiedad | ui-property-modified |
| ContextHub.Constants.EVENT_UI_RENDERED | Se activa cada vez que se procesa la interfaz de usuario de ContextHub (por ejemplo, después de un cambio de propiedad) | ui-renderizado |
| ContextHub.Constants.EVENT_UI_INITIALIZED | Se activa cuando el contenedor de IU se inicializa | ui-inicializado |
| ContextHub.Constants.ACTIVE_UI_MODE | Indica el modo de IU activo | /_/active-ui-mode |

## Referencia de la API de JavaScript de ContextHub {#contexthub-javascript-api-reference-2}

El objeto ContextHub proporciona acceso a todas las tiendas.

### Funciones (ContextHub) {#functions-contexthub}

#### getAllStores() {#getallstores}

Devuelve todos los almacenes registrados de ContextHub.

Esta función no tiene parámetros.

**Devuelve**

Un objeto que contiene todos los almacenes de ContextHub. Cada almacén es un objeto que utiliza el mismo nombre que el almacén.

**Ejemplo**

El ejemplo siguiente recupera todas las tiendas y, a continuación, recupera el almacén de geolocalización:

```
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(name) {#getstore-name}

Recupera un almacén como objeto de Javascript.

**Parámetros**

* **name:** El nombre con el que se registró la tienda.

**Devuelve**

Un objeto que representa el almacén.

**Ejemplo**

El ejemplo siguiente recupera el almacén de geolocalización:

```
var geoloc = ContextHub.getStore("geolocation");
```

## ContextHub.SegmentEngine.Segment {#contexthub-segmentengine-segment}

Representa un segmento de ContextHub. Utilice ContextHub.SegmentEngine.SegmentManager para obtener segmentos.

### Funciones (ContextHub.ContextEngine.Segment) {#functions-contexthub-contextengine-segment}

#### getName() {#getname}

Devuelve el nombre del segmento como un valor de tipo String.

#### getPath() {#getpath}

Devuelve la ruta de acceso del repositorio de la definición del segmento como un valor de tipo String.

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

Proporciona acceso a los segmentos de ContextHub.

### Funciones (ContextHub.SegmentEngine.SegmentManager) {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

Devuelve los segmentos resueltos en el contexto actual. Esta función no tiene parámetros.

**Devuelve**

Matriz de objetos ContextHub.SegmentEngine.Segment .

## ContextHub.Store.Core {#contexthub-store-core}

La clase base de los almacenes de ContextHub.

### Propiedades (ContextHub.Store.Core) {#properties-contexthub-store-core}

#### evento {#eventing}

Un objeto [ContextHub.Utils.Event](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing). Utilice este objeto para funciones de enlace para almacenar eventos. Para obtener información sobre el valor predeterminado y la inicialización, consulte [init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config).

#### name {#name}

Nombre de la tienda.

#### persistencia {#persistence}

Un objeto ContextHub.Utils.Persistence. Para obtener información sobre el valor predeterminado y la inicialización, consulte `[init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config).`

### Funciones (ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems(tree, options) {#addallitems-tree-options}

Combina un objeto de datos o una matriz con los datos del almacén. Cada par clave/valor del objeto o matriz se agrega al almacén (a través de la función `setItem` ):

* **Objeto:** Las claves son los nombres de propiedad.
* **Matriz:** Las claves son los índices de matriz.

Tenga en cuenta que los valores pueden ser objetos.

**Parámetros**

* **árbol:**  (objeto o matriz) Los datos que se van a añadir al almacén.
* **opciones:**  (Objeto) un objeto opcional de opciones que se pasa a la función setItem. Para obtener más información, consulte el parámetro `options` de [setItem(key,value,options)](/help/sites-developing/contexthub-api.md#setitem-key-value-options).

**Devuelve**

Un valor `boolean`:

* El valor `true` indica que se ha almacenado el objeto de datos.
* Un valor de `false` indica que el almacén de datos no ha cambiado.

#### addReference(key, anotherKey) {#addreference-key-anotherkey}

Crea una referencia de una clave a otra. Una clave no se puede hacer referencia a sí misma.

**Parámetros**

* **clave:** La clave a la que se hace referencia  `anotherKey`.

* **anotherkey:** Clave a la que se hace referencia en  `key`.

**Devuelve**

Un valor `boolean`:

* Un valor de `true` indica que se agregó la referencia.
* Un valor de `false` indica que no se agregó ninguna referencia.

#### notifyReadiness() {#announcereadiness}

Déclencheur el evento `ready` para este almacén. Esta función no tiene parámetros y no devuelve ningún valor.

#### clean() {#clean}

Quita todos los datos del almacén. La función no tiene parámetros ni valor devuelto.

#### getItem(key) {#getitem-key}

Devuelve el valor asociado a una clave.

**Parámetros**

* **clave:**  (cadena) la clave para la que se devolverá el valor.

**Devuelve**

Objeto que representa el valor de la clave.

#### getKeys(includeInternals) {#getkeys-includeinternals}

Recupera las claves del almacén. Opcionalmente, puede recuperar las claves que utiliza internamente el marco de ContextHub.

**Parámetros**

* **includeInternals:** un valor de  `true` incluye claves utilizadas internamente en los resultados. Estas teclas comienzan con el carácter de subrayado (&quot;_&quot;). El valor predeterminado es `false`.

**Devuelve**

Matriz de nombres de claves ( `string` valores).

#### getReferences() {#getreferences}

Recupera las referencias del almacén.

**Devuelve**

Matriz que utiliza claves de referencia como índices para las claves a las que se hace referencia:

* Las claves de referencia se corresponden con el parámetro `key` de la función `addReference`.

* Las claves a las que se hace referencia se corresponden con el parámetro `anotherKey` de la función `addReference`.

#### getTree(includeInternals) {#gettree-includeinternals}

Recupera el árbol de datos del almacén. Opcionalmente, puede incluir los pares de clave/valor que utiliza internamente el marco de ContextHub.

**Parámetros**

* `includeInternals:` Un valor de  `true` incluye pares de clave/valor utilizados internamente en los resultados. Las claves de estos datos comienzan con el carácter de subrayado (&quot;_&quot;). El valor predeterminado es `false`.

**Devuelve**

Un objeto que representa el árbol de datos. Las claves son los nombres de propiedad del objeto.

#### init(name, config) {#init-name-config}

Inicializa la tienda.

* Establece los datos almacenados en un objeto vacío.
* Establece las referencias de almacenamiento en un objeto vacío.
* eventChannel son datos:*name*, donde *name* es el nombre del almacén.

* storeDataKey es /store/*name*, donde *name* es el nombre del almacén.

**Parámetros**

* **nombre:** el nombre del almacén.
* **Configuración:** Un objeto que contiene propiedades de configuración:

   * eventDeferring: El valor predeterminado es 32.
   * evento: El objeto [ContextHub.Utils.Event](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) para este almacén. El valor predeterminado es el objeto ContextHub.eventing que utiliza.
   * persistencia: El objeto ContextHub.Utils.Persistence de este almacén. El valor predeterminado es el objeto ContextHub.persistence .

#### isEventPaused() {#iseventingpaused}

Determina si el evento está en pausa para esta tienda.

**Devuelve**

Un valor booleano:

* `true`: El evento se pone en pausa para que no se activen eventos para esta tienda.
* `false`: Los eventos no se pausan para que se activen eventos para esta tienda.

#### pauseEvent() {#pauseeventing}

Pone en pausa el evento de la tienda para que no se active ningún evento. Esta función no requiere parámetros y no devuelve ningún valor.

#### removeItem(key, options) {#removeitem-key-options}

Quita un par clave/valor de la tienda.

Cuando se elimina una clave, la función déclencheur el evento `data` . Los datos del evento incluyen el nombre del almacén, el nombre de la clave que se eliminó, el valor que se eliminó, el nuevo valor para la clave (nulo) y el tipo de acción &quot;remove&quot; (eliminar).

Opcionalmente, puede evitar que se active el evento `data`.

**Parámetros**

* **clave:**  (cadena) nombre de la clave que se va a quitar.
* **opciones:**  (Objeto) Un objeto de opciones. Las siguientes propiedades de objeto son válidas:

   * silencioso: Un valor de `true` impide que se active el evento `data`. El valor predeterminado es `false`.

**Devuelve**

Un valor `boolean`:

* Un valor de `true` indica que se ha eliminado el par clave/valor.
* Un valor de `false` indica que el almacén de datos no ha cambiado porque la clave no se ha encontrado en el almacén.

#### removeReference(key) {#removereference-key}

Quita una referencia de la tienda.

**Parámetros**

* **clave:** La referencia clave que se va a eliminar. Este parámetro corresponde al parámetro `key` de la función `addReference`.

**Devuelve**

Un valor `boolean`:

* Un valor de `true` indica que se ha eliminado la referencia.
* Un valor de `false` indica que la clave no era válida y que el almacén no ha cambiado.

#### reset(keepRemainingData) {#reset-keepremainingdata}

Restaura los valores iniciales de los datos persistentes del almacén. De forma opcional, puede eliminar todos los demás datos del almacén. El evento está en pausa para esta tienda mientras se restablece la tienda. Esta función no devuelve ningún valor.

Los valores iniciales se proporcionan en la propiedad initialValues del objeto config que se utiliza para crear una instancia del objeto store .

**Parámetros**

* **keepRemainingData:**  (booleano) Un valor de true hace que se mantengan los datos no iniciales. Un valor false hace que se eliminen todos los datos excepto los valores iniciales.

Restaura los valores iniciales de los datos persistentes del almacén. De forma opcional, puede eliminar todos los demás datos del almacén. El evento está en pausa para esta tienda mientras se restablece la tienda. Esta función no devuelve ningún valor.

Los valores iniciales se proporcionan en la propiedad initialValues del objeto config que se utiliza para crear una instancia del objeto store .

**Parámetros**

* keepRemainingData: (Booleano) Un valor de true hace que se mantengan los datos no iniciales. Un valor false hace que se eliminen todos los datos excepto los valores iniciales.

#### resolveReference(key, retry) {#resolvereference-key-retry}

Recupera una clave a la que se hace referencia. De forma opcional, puede especificar el número de iteraciones que se utilizarán para resolver la mejor coincidencia.

**Parámetros**

* **clave:**  (cadena) la clave para la que se resuelve la referencia. Este parámetro `key` corresponde al parámetro `key` de la función `addReference`.

* **reintento:**  (número) número de iteraciones que se van a utilizar.

**Devuelve**

Un valor `string` que representa la clave a la que se hace referencia. Si no se resuelve ninguna referencia, se devuelve el valor del parámetro `key`.

#### resumeEvent() {#resumeeventing}

Reanuda el evento de este almacén para que se activen los eventos. Esta función no define parámetros ni devuelve ningún valor.

#### setItem(clave, valor, opciones) {#setitem-key-value-options}

Agrega un par clave/valor a la tienda.

Déclencheur el evento `data` solo si el valor de la clave es diferente del valor que está almacenado para la clave. Si lo desea, puede evitar que se active el evento `data`.

Los datos de evento incluyen el nombre del almacén, la clave, el valor anterior, el nuevo valor y el tipo de acción `set`.

**Parámetros**

* **clave:**  (cadena) nombre de la clave.
* **opciones:**  (Objeto) Un objeto de opciones. Las siguientes propiedades de objeto son válidas:

   * silencioso: Un valor de `true` impide que se active el evento `data`. El valor predeterminado es `false`.

* **valor:**  (Objeto) El valor que se va a asociar a la clave.

**Devuelve**

Un valor `boolean`:

* El valor `true` indica que se ha almacenado el objeto de datos.
* Un valor de `false` indica que el almacén de datos no ha cambiado.

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

Un almacén que contiene datos JSON. Los datos se recuperan de un servicio JSONP externo o, opcionalmente, de un servicio que devuelve datos JSON. Especifique los detalles del servicio mediante la función [ `init`](/help/sites-developing/contexthub-api.md#init-name-config) al crear una instancia de esta clase.

El almacén utiliza la persistencia en memoria (variable JavaScript). Los datos del almacén solo están disponibles durante toda la página.

ContextHub.Store.JSONPStore amplía [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) y hereda las funciones de esa clase.

### Funciones (ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig, override) {#configureservice-serviceconfig-override}

Configura los detalles para conectarse al servicio JSONP que utiliza este objeto. Puede actualizar o reemplazar la configuración existente. La función no devuelve ningún valor.

**Parámetros**

* **serviceConfig:** objeto que contiene las siguientes propiedades:

   * host: (Cadena) El nombre del servidor o la dirección IP.
   * jsonp: (Booleano) Un valor de true indica que el servicio es un servicio JSONP, false en caso contrario. Cuando es true, la llamada de retorno {Callback: &quot;ContextHub.Callback.*El objeto Object.name*} se agrega al objeto service.params.
   * parámetros: (Objeto) Los parámetros de URL representados como propiedades de objeto. Los nombres de parámetro son nombres de propiedad y los valores de parámetro son valores de propiedad.
   * ruta: (Cadena) La ruta al servicio.
   * puerto: (Número) El número de puerto del servicio.
   * seguro: (Cadena o Booleano) Determina el protocolo que se utiliza para la URL del servicio:

      * auto: //
      * true: https://
      * false: https://

* **override:**  (booleano). Un valor de `true` hace que la configuración de servicio existente se sustituya por las propiedades de `serviceConfig`. Un valor de `false` hace que las propiedades de configuración de servicio existentes se fusionen con las propiedades de `serviceConfig`.

#### getRawResponse() {#getrawresponse}

Devuelve la respuesta sin procesar que se almacena en caché desde la última llamada al servicio JSONP. La función no requiere parámetros.

**Devuelve**

Un objeto que representa la respuesta sin procesar.

#### getServiceDetails() {#getservicedetails}

Recupera el objeto de servicio para este objeto ContextHub.Store.JSONPStore. El objeto service contiene toda la información necesaria para crear la URL del servicio.

**Devuelve**

Un objeto con las siguientes propiedades:

* **host:**  (cadena) El nombre del servidor o la dirección IP.
* **jsonp:**  (booleano) un valor de true indica que el servicio es un servicio JSONP, false en caso contrario. Cuando es true, la llamada de retorno {Callback: &quot;ContextHub.Callback.*El objeto Object.name*} se agrega al objeto service.params.

* **parámetros:**  (objeto) parámetros de URL representados como propiedades de objeto. Los nombres de parámetro son nombres de propiedad y los valores de parámetro son valores de propiedad.
* **ruta:**  (cadena) La ruta al servicio.
* **puerto:**  (número) número de puerto del servicio.
* **secure:**  (cadena o booleano) determina el protocolo que se utilizará para la URL del servicio:

   * auto: //
   * true: https://
   * false: https://

#### getServiceURL(resolve) {#getserviceurl-resolve}

Recupera la URL del servicio JSONP.

**Parámetros**

* **resolver:**  (booleano) determina si se incluyen parámetros resueltos en la dirección URL. Un valor de `true` resuelve los parámetros y `false` no.

**Devuelve**

Un valor `string` que representa la dirección URL del servicio.

#### init(name, config) {#init-name-config-1}

inicia el objeto ContextHub.Store.JSONPStore.

**Parámetros**

* **name:**  (cadena) nombre del almacén.
* **config:**  (Objeto) Un objeto que contiene la propiedad service. El objeto JSONPStore utiliza las propiedades del objeto `service` para construir la URL del servicio JSONP:

   * eventDeferring: 32.
   * evento: El objeto ContextHub.Utils.Event de esta tienda. El valor predeterminado es el objeto `ContextHub.eventing`.
   * persistencia: El objeto ContextHub.Utils.Persistence de este almacén. De forma predeterminada, se utiliza la persistencia de la memoria (objeto Javascript).
   * servicio: (Objeto)

      * host: (Cadena) El nombre del servidor o la dirección IP.
      * jsonp: (Booleano) Un valor de true indica que el servicio es un servicio JSONP, false en caso contrario. Cuando es verdadero, el objeto `{callback: "ContextHub.Callbacks.*Object.name*}`se agrega a `service.params`.
      * parámetros: (Objeto) Los parámetros de URL representados como propiedades de objeto. Los nombres y valores de parámetro son los nombres y valores de las propiedades de objeto, respectivamente.
      * ruta: (Cadena) La ruta al servicio.
      * puerto: (Número) El número de puerto del servicio.
      * seguro: (Cadena o Booleano) Determina el protocolo que se utiliza para la URL del servicio:

         * auto: //
         * true: https://
         * false: https://
      * tiempo de espera: (Número) La cantidad de tiempo de espera para que el servicio JSONP responda antes de finalizar el tiempo de espera, en milisegundos.
      * ttl: Cantidad mínima de tiempo en milisegundos que transcurre entre llamadas al servicio JSONP. (Consulte la función [queryService](/help/sites-developing/contexthub-api.md#queryservice-reload) ).


#### queryService(reload) {#queryservice-reload}

Consulta el servicio JSONP remoto y almacena en caché la respuesta. Si la cantidad de tiempo desde la llamada anterior a esta función es menor que el valor de `config.service.ttl`, no se llama al servicio y no se cambia la respuesta en caché. Opcionalmente, puede forzar la llamada al servicio. La propiedad `config.service.ttl`se establece al llamar a la función [init](/help/sites-developing/contexthub-api.md#init-name-config) para inicializar el almacén.

Déclencheur el evento ready cuando la consulta termina. Si no se establece la URL del servicio JSONP, la función no hace nada.

**Parámetros**

* **recarga:**  (booleano) Un valor de true elimina la respuesta en caché y fuerza la llamada al servicio JSONP.

#### reset {#reset}

Restaura los valores iniciales de los datos persistentes del almacén y, a continuación, llama al servicio JSONP. De forma opcional, puede eliminar todos los demás datos del almacén. El evento se pone en pausa para este almacén mientras se restablecen los valores iniciales. Esta función no devuelve ningún valor.

Los valores iniciales se proporcionan en la propiedad initialValues del objeto config que se utiliza para crear una instancia del objeto store .

**Parámetros**

* **keepRemainingData:**  (booleano) Un valor de true hace que se mantengan los datos no iniciales. Un valor false hace que se eliminen todos los datos excepto los valores iniciales.

#### resolveParameter(f) {#resolveparameter-f}

Resuelve el parámetro dado.

## ContextHub.Store.PersistedJSONPStore {#contexthub-store-persistedjsonpstore}

ContextHub.Store.PersistedJSONPStore extiende [ContextHub.Store.JSONPStore](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore) para que herede todas las funciones de esa clase. Sin embargo, los datos recuperados del servicio JSONP se mantienen según la configuración de la persistencia de ContextHub. (Consulte [Modos de persistencia](/help/sites-developing/ch-adding.md#persistence-modes)).

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

ContextHub.Store.PersistedStore amplía [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) de modo que hereda todas las funciones de esa clase. Los datos de este almacén se mantienen según la configuración de la persistencia de ContextHub.

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

ContextHub.Store.SessionStore amplía [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) de modo que hereda todas las funciones de esa clase. Los datos de este almacén se mantienen utilizando la persistencia en memoria (objeto Javascript).

## ContextHub.UI {#contexthub-ui}

Gestiona los módulos de IU y los procesadores de módulos de IU.

### Funciones (ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType, renderer, dontRender) {#registerrenderer-moduletype-renderer-dontrender}

Registra un procesador de módulos de IU con ContextHub. Una vez registrado el renderizador, se puede utilizar para [crear módulos de IU](ch-configuring.md#adding-a-ui-module). Utilice esta función cuando [extienda ContextHub.UI.BaseModuleRenderer](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types) para crear un procesador de módulos de interfaz de usuario personalizado.

**Parámetros**

* **moduleType:**  (String) identificador del procesador del módulo de la interfaz de usuario. Si un renderizador ya está registrado con el valor especificado, el renderizador existente no está registrado antes de que se registre este renderizador.
* **renderizador:**  (cadena) nombre de la clase que procesa el módulo de IU.
* **dontRender:**  (booleano) se configura como  `true` para evitar que la interfaz de usuario de ContextHub se represente después de registrar el renderizador. El valor predeterminado es `false`.

**Ejemplo**

En el siguiente ejemplo se registra un renderizador como tipo de módulo contexthub.browserinfo .

```
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

Una clase de utilidad para interactuar con cookies.

### Funciones (ContextHub.Utils.Cookie) {#functions-contexthub-utils-cookie}

#### exists(key) {#exists-key}

Determina si existe una cookie.

**Parámetros**

* **clave:** una  `String` que contiene la clave de la cookie para la que está probando.

**Devuelve**

Un valor `boolean` de true indica que la cookie existe.

**Ejemplo**

```
if (ContextHub.Utils.Cookie.exists("name")) {
   // conditionally-executed code
}
```

#### getAllItems(filter) {#getallitems-filter}

Devuelve todas las cookies que tienen claves que coinciden con un filtro.

**Parámetros**

* (Opcional) **filtro:** Criterios para las claves de cookie coincidentes. Para devolver todas las cookies, no especifique ningún valor. Se admiten los siguientes tipos:

   * Cadena: La cadena se compara con la clave de cookie.
   * Matriz: Cada elemento de la matriz es un filtro.
   * Un objeto RegExp: La función de prueba del objeto se utiliza para hacer coincidir las claves de las cookies.
   * Una función: Una función que prueba una clave de cookie para una coincidencia. La función debe tomar la clave de cookie como parámetro y devolver true si la prueba confirma una coincidencia.

**Devuelve**

Un objeto de cookies. Las propiedades de objeto son claves de cookie y los valores clave son valores de cookie.

**Ejemplo**

```
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

Devuelve un valor de cookie.

**Parámetros**

* **clave:** La clave de la cookie para la que desea el valor.

**Devuelve**

El valor de la cookie o `null` si no se encontró ninguna cookie para la clave.

**Ejemplo**

```
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter) {#getkeys-filter}

Devuelve una matriz de las claves de las cookies existentes que coinciden con un filtro.

**Parámetros**

* **filtro:** criterios para coincidencia de claves de cookies. Se admiten los siguientes tipos:

   * Cadena: La cadena se compara con la clave de cookie.
   * Matriz: Cada elemento de la matriz es un filtro.
   * Un objeto RegExp: La función de prueba del objeto se utiliza para hacer coincidir las claves de las cookies.
   * Una función: Una función que prueba una clave de cookie para una coincidencia. La función debe tomar la clave de cookie como parámetro y devolver `true` si la prueba confirma una coincidencia.

**Devuelve**

Matriz de cadenas en la que cada cadena es la clave de una cookie que coincide con el filtro.

**Ejemplo**

```
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key, options) {#removeitem-key-options-1}

Quita una cookie. Para eliminar la cookie, el valor se establece en una cadena vacía y la fecha de caducidad se establece en el día anterior a la fecha actual.

**Parámetros**

* **clave:** un  `String` valor que representa la clave de la cookie que se va a eliminar.

* **opciones:** un objeto que contiene valores de propiedad para configurar los atributos de cookie. Consulte la función ` [setItem](/help/sites-developing/contexthub-api.md#setitem-key-value-options)` para obtener más información. La propiedad `expires` no tiene ningún efecto.

**Devuelve**

Esta función no devuelve un valor.

**Ejemplo**

```
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(clave, valor, opciones) {#setitem-key-value-options-1}

Crea una cookie de la clave y valor dados y la agrega al documento actual. De forma opcional, puede especificar opciones para configurar los atributos de la cookie.

**Parámetros**

* **clave:** una cadena que contiene la clave de la cookie.
* **value:** una cadena que contiene el valor de la cookie.
* **opciones:**  (opcional) un objeto que contiene cualquiera de las siguientes propiedades que configuran los atributos de cookie:

   * caduca: Un valor `date` o `number` que especifica cuándo caduca la cookie. Un valor de fecha especifica la hora absoluta de caducidad. Un número (en días) establece la hora de caducidad en la hora actual más el número. El valor predeterminado es `undefined`.
   * seguro: Un valor `boolean` que especifica el atributo `Secure` de la cookie. El valor predeterminado es `false`.
   * ruta: Un valor `String` que se utilizará como atributo `Path` de la cookie. El valor predeterminado es `undefined`.

**Devuelve**

La cookie con el valor establecido.

**Ejemplo**

```
ContextHub.Utils.Cookie.setItem("name", "mycookie", {
    expires: 3,
    domain: 'localhost',
    path: '/some/directory',
    secure: true
});
```

#### vanish(filter, options) {#vanish-filter-options}

Elimina todas las cookies que coinciden con un filtro determinado. Las cookies se comparan con usando la función getKeys y se eliminan con la función removeItem .

**Parámetros**

* **filter:** El  `filter` argumento que se utiliza en la llamada a la  `[getKeys](/help/sites-developing/contexthub-api.md#getkeys-filter)` función.

* **options:** El  `options` argumento que se utilizará en la llamada a la  `[removeItem](/help/sites-developing/contexthub-api.md#removeitem-key-options)` función.

**Devuelve**

Esta función no devuelve un valor.

## ContextHub.Utils.Event {#contexthub-utils-eventing}

Permite enlazar y desenlazar funciones a eventos de almacenamiento de ContextHub. Acceda a los objetos ContextHub.Utils.Event de un almacén con la propiedad [eventing](/help/sites-developing/contexthub-api.md#eventing) del almacén.

### Funciones (ContextHub.Utils.Eventing) {#functions-contexthub-utils-eventing}

#### off(name, selector) {#off-name-selector}

Desvincula una función de un evento.

**Parámetros**

* **name:** El  [nombre del ](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) evento para el que va a desenlazar la función.

* **selector:** Selector que identifica el enlace. (Consulte el parámetro `selector` para las funciones [on](/help/sites-developing/contexthub-api.md#on-name-handler-selector-triggerforpastevents) y [once](/help/sites-developing/contexthub-api.md#once-name-handler-selector-triggerforpastevents)).

**Devuelve**

Esta función no devuelve ningún valor.

#### on(name, handler, selector, triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

Enlaza una función a un evento. Se llama a la función cada vez que se produce el evento. Opcionalmente, se puede llamar a la función para eventos que se hayan producido en el pasado antes de establecer el enlace.

**Parámetros**

* **name:**  (String)  [nombre del evento ](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) al que está enlazando la función.

* **controlador:**  (función) la función que se va a enlazar al evento.
* **selector:**  (Cadena) Identificador único del enlace. Necesita el selector para identificar el enlace si desea utilizar la función `off` para quitar el enlace.

* **triggerForPastEvents:**  (booleano) Indica si el controlador debe ejecutarse para eventos que se hayan producido en el pasado. Un valor de `true` llama al controlador para eventos anteriores. Un valor de `false` llama al controlador para eventos futuros. El valor predeterminado es `true`.

**Devuelve**

Cuando el argumento `triggerForPastEvents` es `true`, esta función devuelve un valor `boolean` que indica si el evento se produjo en el pasado:

* `true`: El evento se produjo en el pasado y se llamará al controlador.
* `false`: El evento no ha ocurrido en el pasado.

Si `triggerForPastEvents` es `false`, esta función no devuelve ningún valor.

**Ejemplo**

En el siguiente ejemplo se vincula una función al evento de datos del almacén de geolocalización. La función rellena un elemento en la página con el valor del elemento de datos de latitud del almacén.

```
<div class="location">
    <p>latitude: <span id="lat"></span></p>
</div>

<script>
    var geostore = ContextHub.getStore("geolocation");
    geostore.eventing.on(ContextHub.Constants.EVENT_DATA_UPDATE,getlat,"getlat");

    function getlat(){
       latitude = geostore.getItem("latitude");
       $("#lat").html(latitude);
    }
</script>
```

#### once(nombre, controlador, selector, triggerForPastEvents) {#once-name-handler-selector-triggerforpastevents}

Enlaza una función a un evento. La función se llama una sola vez, para la primera aparición del evento. Opcionalmente, se puede llamar a la función para el evento que se ha producido en el pasado, antes de que se establezca el enlace.

**Parámetros**

* **name:**  (String)  [nombre del evento ](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) al que está enlazando la función.

* **controlador:**  (función) la función que se va a enlazar al evento.
* **selector:**  (Cadena) Identificador único del enlace. Necesita el selector para identificar el enlace si desea utilizar la función `off` para quitar el enlace.

* **triggerForPastEvents:**  (booleano) Indica si el controlador debe ejecutarse para eventos que se hayan producido en el pasado. Un valor de `true` llama al controlador para eventos anteriores. Un valor de `false` llama al controlador para eventos futuros. El valor predeterminado es `true`.

**Devuelve**

Cuando el argumento `triggerForPastEvents` es `true`, esta función devuelve un valor `boolean` que indica si el evento se produjo en el pasado:

* `true`: El evento se produjo en el pasado y se llamará al controlador.
* `false`: El evento no ha ocurrido en el pasado.

Si `triggerForPastEvents` es `false`, esta función no devuelve ningún valor.

## ContextHub.Utils.herencia {#contexthub-utils-inheritance}

Clase de utilidad que permite a un objeto heredar las propiedades y los métodos de otro objeto.

### Funciones (ContextHub.Utils.herencia) {#functions-contexthub-utils-inheritance}

#### herit(child, parent) {#inherit-child-parent}

Hace que un objeto herede las propiedades y los métodos de otro objeto.

**Parámetros**

* **secundario:**  (objeto) el objeto que hereda.
* **parent:**  (Object) objeto que define las propiedades y los métodos heredados.

## ContextHub.Utils.JSON {#contexthub-utils-json}

Proporciona funciones para serializar objetos en formato JSON y deserializar cadenas JSON en objetos.

### Funciones (ContextHub.Utils.JSON) {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

Analiza un valor de cadena como JSON y lo convierte en un objeto de javascript.

**Parámetros**

* **datos:** un valor de cadena en formato JSON.

**Devuelve**

Un objeto Javascript.

**Ejemplo**

El código `ContextHub.Utils.JSON.parse("{'city':'Basel','country':'Switzerland','population':'173330'}");` devuelve el siguiente objeto:

```
Object {
   city: "Basel",
   country: "Switzerland",
   population: 173330
}
```

#### stringify(data) {#stringify-data}

Serializa los valores y objetos de JavaScript en valores de cadena de formato JSON.

**Parámetros**

* **data:** El valor u objeto que se va a serializar. Esta función admite valores booleanos, de matriz, de número, de cadena y de fecha.

**Devuelve**

El valor de cadena serializada. Cuando `data` es un valor R `egExp`, esta función devuelve un objeto vacío. Cuando `data` es una función, devuelve `undefined`.

**Ejemplo**

El siguiente código devuelve `"{'city':'Basel','country':'Switzerland','population':'173330'}":`

```
ContextHub.Utils.JSON.stringify({
   city: "Basel",
   country: "Switzerland",
   population: 173330
});
```

## ContextHub.Utils.JSON.tree {#contexthub-utils-json-tree}

Esta clase facilita la manipulación de objetos de datos que se van a almacenar o que se recuperan de los almacenes de ContextHub.

### Funciones (ContextHub.Utils.JSON.tree) {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

Crea una copia de un objeto de datos y le añade el árbol de datos de un segundo objeto. La función devuelve la copia y no modifica ninguno de los objetos originales. Cuando los árboles de datos de los dos objetos contienen claves idénticas, el valor del segundo objeto sobrescribe el valor del primer objeto.

**Parámetros**

* **árbol:** el objeto que se copia.
* **SecondTree:** el objeto que se combina con la copia del  `tree` objeto.

**Devuelve**

Objeto que contiene los datos combinados.

#### cleanup() {#cleanup}

Crea una copia de un objeto, busca y elimina elementos en el árbol de datos que no contienen valores, valores nulos o valores indefinidos, y devuelve la copia.

**Parámetros**

* **árbol:** El objeto que se va a limpiar.

**Devuelve**

Una copia del árbol que se limpia.

#### getItem() {#getitem}

Recupera el valor de un objeto para una clave.

**Parámetros**

* **árbol:** El objeto de datos.
* **clave:** La clave del valor que desea recuperar.

**Devuelve**

El valor que corresponde a la clave. Cuando la clave tiene claves secundarias, esta función devuelve un objeto complejo. Cuando el tipo del valor de la clave es `undefined`, se devuelve `null`.

**Ejemplo**

Tenga en cuenta el siguiente objeto de JavaScript:

```
myObject {
  user: {
    location: {
      city: "Basel",
        details: {
          population: 173330,
          elevation: 260
        }
      }
    }
  }
```

El siguiente código de ejemplo devuelve el valor `260`:

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user/location/details/elevation");
```

El siguiente código de ejemplo recupera el valor de una clave que tiene claves secundarias:

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user");
```

La función devuelve el siguiente objeto:

```
Object {
  location: {
    city: "Basel",
    details: {
      population: 173330,
      elevation: 260
    }
  }
}
```

#### getKeys() {#getkeys}

Recupera todas las claves del árbol de datos de un objeto. De forma opcional, solo puede recuperar las claves de los elementos secundarios de una clave específica. También puede especificar un orden de las claves recuperadas.

**Parámetros**

* **árbol:** El objeto desde el que se recuperan las claves del árbol de datos.
* **principal:**  (opcional) la clave de un elemento del árbol de datos para el que desea recuperar las claves de los elementos secundarios.
* **order:**  (opcional) una función que determina el orden de las claves devueltas. (Consulte [Array.prototype.sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) en Mozilla Developer Network).

**Devuelve**

Matriz de claves.

**Ejemplo**

Consideremos el siguiente objeto:

```
myObject {
  location: {
    weather: {
      temperature: "28C",
      humidity: "77%",
      precipitation: "10%",
      wind: "8km/h"
    },
    city: "Basel",
    country: "Switzerland",
    longitude: 7.5925727,
    latitude: 47.557421
  }
}
```

El script `ContextHub.Utils.JSON.tree.getKeys(myObject);` devuelve la siguiente matriz:

```
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

Crea una copia de un objeto determinado, quita la rama especificada del árbol de datos y devuelve la copia modificada.

**Parámetros**

* árbol: Un objeto de datos.
* clave: La clave que se va a quitar.

**Devuelve**

Una copia del objeto de datos original con la clave eliminada.

**Ejemplo**

Consideremos el siguiente objeto:

```
myObject {
  one: {
    foo: "bar",
    two: {
      three: {
        four: {
          five: 5,
          six: 6
        }
      }
    }
  }
}
```

La siguiente secuencia de comandos de ejemplo elimina la rama /one/two/tres/cuatro del árbol de datos:

```
myObject = ContextHub.Utils.JSON.tree.removeItem(myObject, "/one/two/three/four");
```

La función devuelve el siguiente objeto:

```
myObject {
  one: {
    foo: "bar"
  }
}
```

#### sanitizeKey(key) {#sanitizekey-key}

Anida los valores de cadena para que se puedan utilizar como claves. Para sanear una cadena, esta función realiza las siguientes acciones:

* Reduce varias barras diagonales consecutivas a una sola barra diagonal.
* Elimina los espacios en blanco del principio y del final de la cadena.
* Divide el resultado en una matriz de cadenas que están delimitadas por barras diagonales.

Utilice la matriz resultante para crear una clave utilizable.  **Parámetros**

* **clave:** El  `string` que se va a sanear.

**Devuelve**

Matriz de valores `string` donde cada cadena es la parte del `key` que se marcó con barras oblicuas. representa la clave saneada. Si la matriz saneada tiene una longitud de cero, esta función devuelve `null`.

**Ejemplo**

El siguiente código depura una cadena para producir la matriz `["this", "is", "a", "path"]` y luego genera la clave `"/this/is/a/path"` de la matriz:

```
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(tree, key, value) {#setitem-tree-key-value}

Agrega un par clave/valor al árbol de datos de una copia de un objeto. Para obtener información sobre los árboles de datos, consulte [Persistence](/help/sites-developing/contexthub.md#persistence).

**Parámetros**

* árbol: Un objeto de datos.
* clave: La clave que se va a asociar al valor que está agregando. La clave es la ruta al elemento del árbol de datos. Esta función llama a `ContextHub.Utils.JSON.tree.sanitize` para sanear la clave antes de agregarla.
* valor: El valor que se va a añadir al árbol de datos.

**Devuelve**

Una copia del objeto `tree` que incluye el par `key`/ `value`.

**Ejemplo**

Tenga en cuenta el siguiente código JavaScript:

```
var myObject = {
     user: {
        location: {
           city: "Basel"
           }
        }
     };

var myKey = "/user/location/details";

var myValue = {
      population: 173330,
      elevation: 260
     };

myObject = ContextHub.Utils.JSON.tree.setItem(myObject, myKey, myValue);
```

El objeto myObject tiene el siguiente valor:

## ContextHub.Utils.storeCandidate {#contexthub-utils-storecandidates}

Permite registrar a los candidatos a la tienda y obtener los candidatos registrados a la tienda.

### Funciones (ContextHub.Utils.storeCandidates) {#functions-contexthub-utils-storecandidates}

#### getRegisteredCandidates(storeType) {#getregisteredcandidates-storetype}

Devuelve los tipos de tienda registrados como candidatos de tienda. Recupere los candicados registrados de un tipo de almacén específico o de todos los tipos de almacén.

**Parámetros**

* **storeType:**  (String) nombre del tipo de almacén. Consulte el parámetro `storeType` de la función [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates).

**Devuelve**

Un objeto de tipos de almacén. Las propiedades de objeto son los nombres de tipo de almacén y los valores de propiedad son una matriz de candidatos de almacén registrados.

#### getStoreFromCandidates(storeType) {#getstorefromcandidates-storetype}

Devuelve un tipo de tienda de los candidatos registrados. Si se registra más de un tipo de almacén del mismo nombre, la función devuelve el tipo de almacén con la prioridad más alta.

**Parámetros**

* storeType: (Cadena) El nombre del candidato de la tienda. Consulte el parámetro `storeType` de la función [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies).

**Devuelve**

Un objeto que representa el candidato de almacén registrado. Si el tipo de almacén solicitado no está registrado, se genera un error.

#### getSupportedStoreTypes() {#getsupportedstoretypes}

Devuelve los nombres de los tipos de tienda que están registrados como candidatos de tienda. Esta función no requiere parámetros.

**Devuelve**

Matriz de valores de cadena, donde cada cadena es el tipo de tienda con el que se registró un candidato a tienda. Consulte el parámetro `storeType` de la función [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates).

#### registerStoreCandidate(store, storeType, priority, apply) {#registerstorecandidate-store-storetype-priority-applies}

Registra un objeto store como candidato de tienda con un nombre y una prioridad.

La prioridad es un número que indica la importancia de las tiendas con el mismo nombre. Cuando se registra un candidato de tienda con el mismo nombre que un candidato de tienda ya registrado, se utiliza el candidato con mayor prioridad. Al registrar un candidato de tienda, el almacén solo se registra si la prioridad es mayor que los candidatos registrados de tienda con el mismo nombre.

**Parámetros**

* **store:**  (Objeto) El objeto store que se va a registrar como candidato a almacén.
* **storeType:**  (String) nombre del candidato de tienda. Este valor es necesario al crear una instancia del candidato de la tienda.
* **prioridad:**  (número) la prioridad del candidato a almacén.
* **aplica:**  (función) la función que se invoca y que evalúa la aplicabilidad del almacén en el entorno actual. La función debe devolver `true` si el almacén es aplicable y `false` en caso contrario. El valor predeterminado es una función que devuelve true: `function() {return true;}`

**Ejemplo**

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```

