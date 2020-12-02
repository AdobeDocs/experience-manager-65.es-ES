---
title: Referencia de la API de JavaScript de ContextHub
seo-title: Referencia de la API de JavaScript de ContextHub
description: La API de JavaScript de ContextHub está disponible para las secuencias de comandos cuando se ha agregado el componente ContextHub a la página
seo-description: La API de JavaScript de ContextHub está disponible para las secuencias de comandos cuando se ha agregado el componente ContextHub a la página
uuid: 296d6c8e-517f-4837-9e86-ae571ea8aa17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 90605f41-1861-4891-a7c8-b8b5918cd5c6
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '5029'
ht-degree: 2%

---


# Referencia de la API de JavaScript de ContextHub{#contexthub-javascript-api-reference}

La API de JavaScript de ContextHub está disponible para los scripts cuando el componente [ContextHub se ha agregado a la página](/help/sites-developing/ch-adding.md#adding-contexthub-to-a-page-component).

## Constantes de ContextHub {#contexthub-constants}

Valores constantes que define la API de JavaScript de ContextHub.

### Constantes de evento {#event-constants}

La siguiente tabla lista los eventos de nombres que se producen en las tiendas de ContextHub. Consulte también [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing).

| Constante | Descripción | Value |
|---|---|---|
| ContextHub.Constants.EVENT_NAMESPACE | Área de nombres de evento de ContextHub | ch |
| ContextHub.Constants.EVENT_ALL_STORES_READY | Indica que todos los almacenes requeridos están registrados, inicializados y listos para ser consumidos | all-store-ready |
| ContextHub.Constants.EVENT_STORES_PARTIALLY_READY | Indica que no todos los almacenes se inicializaron dentro de un tiempo de espera determinado | tiendas parcialmente listas |
| ContextHub.Constants.EVENT_STORE_REGISTERED | Se activa cuando se registra una tienda | store-registration |
| ContextHub.Constants.EVENT_STORE_READY | Indica que las tiendas están listas para funcionar. Se activa inmediatamente después del registro, excepto en los almacenes JSONP, donde se activa cuando se recuperan datos). | store-ready |
| ContextHub.Constants.EVENT_STORE_UPDATED | Se activa cuando una tienda actualiza su persistencia | store-update |
| ContextHub.Constants.PERSISTENCE_CONTAINER_NAME | Nombre del contenedor de persistencia | ContextHubPersistence |
| ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY | Almacena el nombre de clave de persistencia específico donde se almacena el resultado JSON sin procesar | /_/raw-response |
| ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY | Almacena una marca de hora específica que indica cuándo se recuperaron los datos JSON | /_/response-time |
| ContextHub.Constants.SERVICE_LAST_URL_KEY | Almacena la dirección URL específica del servicio JSON utilizada durante la última llamada | /_/url |
| ContextHub.Constants.IS_CONTAINER_EXPANDED | Indica si la interfaz de usuario de ContextHub está expandida | /_/expandido por contenedor |

### Constantes de Evento de UI {#ui-event-constants}

La siguiente tabla lista los nombres de los eventos que se producen en la interfaz de usuario de ContextHub.

| **Constante** | **Descripción** | **Value** |
|---|---|---|
| ContextHub.Constants.EVENT_UI_MODE_REGISTERED | Se activa cuando se registra un modo | ui-mode-registration |
| ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED | Se activa cuando un modo no está registrado | ui-mode-unregistration |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED | Se activa cuando se registra un procesador de modo | ui-mode-renderer-registration |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED | Se activa cuando un procesador de modo no está registrado | ui-mode-renderer-unregistration |
| ContextHub.Constants.EVENT_UI_MODE_ADDED | Se activa cuando se agrega un nuevo modo | ui-mode-added |
| ContextHub.Constants.EVENT_UI_MODE_REMOVED | Se activa cuando se elimina un modo | ui-mode-remove |
| ContextHub.Constants.EVENT_UI_MODE_SELECTED | Se activa cuando el usuario selecciona un modo | ui-mode-selected |
| ContextHub.Constants.EVENT_UI_MODULE_REGISTERED | Se activa cuando se registra un nuevo módulo | ui-module-registration |
| ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED | Se activa cuando un módulo no está registrado | ui-module-unregistration |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED | Se activa cuando se registra un procesador de módulos | ui-module-renderer-registration |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED | Se activa cuando un procesador de módulos no está registrado | ui-module-renderer-unregistration |
| ContextHub.Constants.EVENT_UI_MODULE_ADDED | Se activa cuando se agrega un nuevo módulo | ui-module-added |
| ContextHub.Constants.EVENT_UI_MODULE_REMOVED | Se activa cuando se elimina un módulo | ui-module-remove |
| ContextHub.Constants.EVENT_UI_CONTAINER_ADDED | Se activa cuando se agrega el contenedor de IU a la página | ui-contenedor agregado |
| ContextHub.Constants.EVENT_UI_CONTAINER_OPENED | Se activa cuando se abre la interfaz de usuario de ContextHub | abierto de ui-contenedor |
| ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED | Se activa cuando la interfaz de usuario de ContextHub está contraída | ui-contenedor-cerrado |
| ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED | Se activa cuando se modifica una propiedad | ui-property-modified |
| ContextHub.Constants.EVENT_UI_RENDERED | Se activa cada vez que se procesa la interfaz de usuario de ContextHub (por ejemplo, después de un cambio de propiedad) | ui-procesado |
| ContextHub.Constants.EVENT_UI_INITIALIZED | Se activa cuando se inicializa el contenedor de la interfaz de usuario | ui-initialize |
| ContextHub.Constants.ACTIVE_UI_MODE | Indica el modo de IU activo | /_/active-ui-mode |

## Referencia de la API de JavaScript de ContextHub {#contexthub-javascript-api-reference-2}

El objeto ContextHub proporciona acceso a todas las tiendas.

### Funciones (ContextHub) {#functions-contexthub}

#### getAllStores() {#getallstores}

Devuelve todos los almacenes de ContextHub registrados.

Esta función no tiene parámetros.

**Devuelve**

Objeto que contiene todos los almacenes de ContextHub. Cada tienda es un objeto que utiliza el mismo nombre que la tienda.

**Ejemplo**

El ejemplo siguiente recupera todas las tiendas y, a continuación, recupera el almacén de geolocalización:

```
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(name) {#getstore-name}

Recupera una tienda como un objeto Javascript.

**Parámetros**

* **name:** El nombre con el que se registró la tienda.

**Devuelve**

Objeto que representa la tienda.

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

Devuelve la ruta del repositorio de la definición del segmento como un valor de tipo String.

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

Proporciona acceso a los segmentos de ContextHub.

### Funciones (ContextHub.SegmentEngine.SegmentManager) {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

Devuelve los segmentos resueltos en el contexto actual. Esta función no tiene parámetros.

**Devuelve**

Matriz de objetos ContextHub.SegmentEngine.Segment.

## ContextHub.Store.Core {#contexthub-store-core}

La clase base de las tiendas de ContextHub.

### Propiedades (ContextHub.Store.Core) {#properties-contexthub-store-core}

#### evento {#eventing}

Un objeto [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing). Utilice este objeto para funciones de enlace para almacenar eventos. Para obtener información sobre el valor predeterminado y la inicialización, consulte [init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config).

#### name {#name}

El nombre de la tienda.

#### persistencia {#persistence}

Un objeto ContextHub.Utils.Persistence. Para obtener información sobre el valor predeterminado y la inicialización, consulte `[init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config).`

### Funciones (ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems(tree, options) {#addallitems-tree-options}

Combina un objeto de datos o una matriz con los datos del almacén. Cada par clave/valor del objeto o matriz se agrega al almacén (mediante la función `setItem`):

* **Objeto:** Las claves son los nombres de las propiedades.
* **Matriz:** las claves son los índices de matriz.

Tenga en cuenta que los valores pueden ser objetos.

**Parámetros**

* **tree:** (Objeto o matriz) Los datos que se van a agregar al almacén.
* **opciones:** (Objeto) Objeto opcional de opciones que se pasa a la función setItem. Para obtener más información, consulte el parámetro `options` de [setItem(key,value,options)](/help/sites-developing/contexthub-api.md#setitem-key-value-options).

**Devuelve**

Un valor `boolean`:

* Un valor de `true` indica que se almacenó el objeto de datos.
* Un valor de `false` indica que el almacén de datos no ha cambiado.

#### addReference(key, anotherKey) {#addreference-key-anotherkey}

Crea una referencia de una clave a otra. Una clave no se puede hacer referencia a sí misma.

**Parámetros**

* **key:** la clave a la que hace referencia  `anotherKey`.

* **anotherkey:** Clave a la que hace referencia  `key`.

**Devuelve**

Un valor `boolean`:

* Un valor de `true` indica que se agregó la referencia.
* Un valor de `false` indica que no se agregó ninguna referencia.

#### publishReadiness() {#announcereadiness}

Activa el evento `ready` para esta tienda. Esta función no tiene parámetros y no devuelve ningún valor.

#### clean() {#clean}

Quita todos los datos del almacén. La función no tiene parámetros ni valor devuelto.

#### getItem(key) {#getitem-key}

Devuelve el valor asociado a una clave.

**Parámetros**

* **key:** (String) La clave para la que se devuelve el valor.

**Devuelve**

Objeto que representa el valor de la clave.

#### getKeys(includeInternals) {#getkeys-includeinternals}

Recupera las claves de la tienda. Opcionalmente, puede recuperar las claves que utiliza internamente el marco de ContextHub.

**Parámetros**

* **includeInternals:** un valor de  `true` incluye claves utilizadas internamente en los resultados. Estas teclas comienzan con el carácter de subrayado (&quot;_&quot;). El valor predeterminado es `false`.

**Devuelve**

Matriz de nombres de clave ( `string` valores).

#### getReferences() {#getreferences}

Recupera las referencias de la tienda.

**Devuelve**

Matriz que utiliza claves de referencia como índices para las claves a las que se hace referencia:

* Las claves de referencia se corresponden con el parámetro `key` de la función `addReference`.

* Las claves a las que se hace referencia corresponden con el parámetro `anotherKey` de la función `addReference`.

#### getTree(includeInternals) {#gettree-includeinternals}

Recupera el árbol de datos del almacén. Opcionalmente, puede incluir los pares clave/valor que utiliza internamente el marco de trabajo de ContextHub.

**Parámetros**

* `includeInternals:` Un valor de  `true` incluye pares de clave/valor utilizados internamente en los resultados. Las claves de estos datos comienzan con el carácter de subrayado (&quot;_&quot;). El valor predeterminado es `false`.

**Devuelve**

Objeto que representa el árbol de datos. Las claves son los nombres de propiedad del objeto.

#### init(name, config) {#init-name-config}

Inicializa la tienda.

* Establece los datos de almacenamiento en un objeto vacío.
* Establece las referencias de almacenamiento en un objeto vacío.
* eventChannel son datos:*nombre*, donde *nombre* es el nombre del almacén.

* storeDataKey es /store/*nombre*, donde *nombre* es el nombre del almacén.

**Parámetros**

* **nombre:** el nombre de la tienda.
* **config:** Objeto que contiene propiedades de configuración:

   * eventDeferring: El valor predeterminado es 32.
   * evento: El objeto [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) para esta tienda. El valor predeterminado es el objeto ContextHub.eventing que utiliza.
   * persistencia: El objeto ContextHub.Utils.Persistence de esta tienda. El valor predeterminado es el objeto ContextHub.persistence.

#### isEventingPaused() {#iseventingpaused}

Determina si el evento está en pausa para esta tienda.

**Devuelve**

Un valor booleano:

* `true`:: El evento se pone en pausa para que no se activen eventos para esta tienda.
* `false`:: La acción de evasión no se pone en pausa para que se activen eventos para esta tienda.

#### pauseEventing() {#pauseeventing}

Pone en pausa los eventos de la tienda para que no se active ningún evento. Esta función no requiere parámetros y no devuelve ningún valor.

#### removeItem(key, options) {#removeitem-key-options}

Quita un par clave/valor de la tienda.

Cuando se elimina una clave, la función activa el evento `data`. Los datos de evento incluyen el nombre del almacén, el nombre de la clave que se eliminó, el valor que se eliminó, el nuevo valor de la clave (nulo) y el tipo de acción &quot;remove&quot;.

Opcionalmente, puede evitar la activación del evento `data`.

**Parámetros**

* **key:** (String) El nombre de la clave que se va a quitar.
* **opciones:** (Objeto) Objeto de opciones. Las siguientes propiedades de objeto son válidas:

   * silencioso: Un valor de `true` evita la activación del evento `data`. El valor predeterminado es `false`.

**Devuelve**

Un valor `boolean`:

* Un valor de `true` indica que se ha quitado el par clave/valor.
* Un valor de `false` indica que el almacén de datos no ha cambiado porque la clave no se encontró en el almacén.

#### removeReference(key) {#removereference-key}

Elimina una referencia de la tienda.

**Parámetros**

* **key:** la referencia clave que se va a quitar. Este parámetro corresponde al parámetro `key` de la función `addReference`.

**Devuelve**

Un valor `boolean`:

* Un valor de `true` indica que se ha quitado la referencia.
* Un valor de `false` indica que la clave no es válida y que el almacén no ha cambiado.

#### reset(keepReminningData) {#reset-keepremainingdata}

Restablece los valores iniciales de los datos persistentes del almacén. Opcionalmente, puede eliminar todos los demás datos de la tienda. El evento se pone en pausa para esta tienda mientras se restablece la tienda. Esta función no devuelve ningún valor.

Los valores iniciales se proporcionan en la propiedad initialValues del objeto config que se utiliza para crear una instancia del objeto store.

**Parámetros**

* **keepReminningData:** (Boolean) Un valor true hace que se mantengan los datos no iniciales. Un valor false hace que se eliminen todos los datos excepto los valores iniciales.

Restablece los valores iniciales de los datos persistentes del almacén. Opcionalmente, puede eliminar todos los demás datos de la tienda. El evento se pone en pausa para esta tienda mientras se restablece la tienda. Esta función no devuelve ningún valor.

Los valores iniciales se proporcionan en la propiedad initialValues del objeto config que se utiliza para crear una instancia del objeto store.

**Parámetros**

* keepReminningData: (Boolean) Un valor true hace que los datos no iniciales se mantengan. Un valor false hace que se eliminen todos los datos excepto los valores iniciales.

#### resolveReference(key, reintentar) {#resolvereference-key-retry}

Recupera una clave a la que se hace referencia. Opcionalmente, puede especificar el número de iteraciones que se utilizarán para resolver la mejor coincidencia.

**Parámetros**

* **key:** (String) La clave para la que se resuelve la referencia. Este parámetro `key` se corresponde con el parámetro `key` de la función `addReference`.

* **reintentar:** (número) El número de iteraciones que se van a utilizar.

**Devuelve**

Un valor `string` que representa la clave a la que se hace referencia. Si no se resuelve ninguna referencia, se devuelve el valor del parámetro `key`.

#### resumeEventing() {#resumeeventing}

Reanuda el evento de esta tienda para que se activen eventos. Esta función no define parámetros y no devuelve ningún valor.

#### setItem(key, value, options) {#setitem-key-value-options}

Añade un par clave/valor en la tienda.

Activa el evento `data` sólo si el valor de la clave es diferente al valor que está almacenado actualmente para la clave. Opcionalmente, puede evitar la activación del evento `data`.

Los datos de evento incluyen el nombre del almacén, la clave, el valor anterior, el nuevo valor y el tipo de acción `set`.

**Parámetros**

* **key:** (String) El nombre de la clave.
* **opciones:** (Objeto) Objeto de opciones. Las siguientes propiedades de objeto son válidas:

   * silencioso: Un valor de `true` evita la activación del evento `data`. El valor predeterminado es `false`.

* **value:** (Object) El valor que se va a asociar a la clave.

**Devuelve**

Un valor `boolean`:

* Un valor de `true` indica que se almacenó el objeto de datos.
* Un valor de `false` indica que el almacén de datos no ha cambiado.

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

Almacén que contiene datos JSON. Los datos se recuperan de un servicio JSONP externo o, opcionalmente, de un servicio que devuelve datos JSON. Especifique los detalles del servicio mediante la función [ `init`](/help/sites-developing/contexthub-api.md#init-name-config) al crear una instancia de esta clase.

La tienda utiliza la resistencia en memoria (variable Javascript). Los datos de almacenamiento solo están disponibles durante la duración de la página.

ContextHub.Store.JSONPStore amplía [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) y hereda las funciones de esa clase.

### Funciones (ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig, override) {#configureservice-serviceconfig-override}

Configura los detalles para la conexión al servicio JSONP que utiliza este objeto. Puede actualizar o reemplazar la configuración existente. La función no devuelve ningún valor.

**Parámetros**

* **serviceConfig:** objeto que contiene las siguientes propiedades:

   * host: (Cadena) El nombre del servidor o la dirección IP.
   * jsonp: (Boolean) Un valor true indica que el servicio es un servicio JSONP; en caso contrario, false. Cuando es true, la llamada de retorno {callback: &quot;ContextHub.Callback.*El objeto Object.name*} se agrega al objeto service.params.
   * parámetros: (Objeto) Parámetros URL representados como propiedades de objeto. Los nombres de parámetro son nombres de propiedad y los valores de parámetro son valores de propiedad.
   * path: (Cadena) La ruta al servicio.
   * puerto: (Número) El número de puerto del servicio.
   * secure: (Cadena o Booleano) Determina el protocolo que se usará para la dirección URL del servicio:

      * auto: //
      * true: https://
      * false: https://

* **override:** (Boolean). Un valor de `true` hace que la configuración de servicio existente se reemplace por las propiedades de `serviceConfig`. Un valor de `false` hace que las propiedades de configuración de servicio existentes se combinen con las propiedades de `serviceConfig`.

#### getRawResponse() {#getrawresponse}

Devuelve la respuesta sin procesar almacenada en caché desde la última llamada al servicio JSONP. La función no requiere parámetros.

**Devuelve**

Objeto que representa la respuesta sin procesar.

#### getServiceDetails() {#getservicedetails}

Recupera el objeto de servicio para este objeto ContextHub.Store.JSONPStore. El objeto service contiene toda la información necesaria para crear la dirección URL del servicio.

**Devuelve**

Un objeto con las siguientes propiedades:

* **host:** (String) El nombre del servidor o la dirección IP.
* **jsonp:** (Boolean) Un valor true indica que el servicio es un servicio JSONP; en caso contrario, false. Cuando es true, la llamada de retorno {callback: &quot;ContextHub.Callback.*El objeto Object.name*} se agrega al objeto service.params.

* **parámetros:**  parámetros de URL (objeto) representados como propiedades de objeto. Los nombres de parámetro son nombres de propiedad y los valores de parámetro son valores de propiedad.
* **path:** (String) La ruta al servicio.
* **puerto:** (número) El número de puerto del servicio.
* **secure:** (String o Boolean) Determina el protocolo que se utilizará para la dirección URL del servicio:

   * auto: //
   * true: https://
   * false: https://

#### getServiceURL(resolve) {#getserviceurl-resolve}

Recupera la dirección URL del servicio JSONP.

**Parámetros**

* **resolve:** (Boolean) Determina si se incluyen parámetros resueltos en la dirección URL. Un valor de `true` resuelve los parámetros y `false` no.

**Devuelve**

Un valor `string` que representa la dirección URL del servicio.

#### init(name, config) {#init-name-config-1}

inicializa el objeto ContextHub.Store.JSONPStore.

**Parámetros**

* **name:** (String) El nombre de la tienda.
* **config:** (Object) Objeto que contiene la propiedad service. El objeto JSONPStore utiliza las propiedades del objeto `service` para construir la dirección URL del servicio JSONP:

   * eventDeferring: 32.
   * evento: El objeto ContextHub.Utils.Eventing para esta tienda. El valor predeterminado es el objeto `ContextHub.eventing`.
   * persistencia: El objeto ContextHub.Utils.Persistence de esta tienda. De forma predeterminada, se utiliza la persistencia de memoria (objeto Javascript).
   * servicio: (Objeto)

      * host: (Cadena) El nombre del servidor o la dirección IP.
      * jsonp: (Boolean) Un valor true indica que el servicio es un servicio JSONP; en caso contrario, false. Cuando es true, el objeto `{callback: "ContextHub.Callbacks.*Object.name*}`se agrega a `service.params`.
      * parámetros: (Objeto) Parámetros URL representados como propiedades de objeto. Los nombres y valores de los parámetros son los nombres y valores de las propiedades de los objetos, respectivamente.
      * path: (Cadena) La ruta al servicio.
      * puerto: (Número) El número de puerto del servicio.
      * secure: (Cadena o Booleano) Determina el protocolo que se usará para la dirección URL del servicio:

         * auto: //
         * true: https://
         * false: https://
      * timeout: (Número) La cantidad de tiempo que se debe esperar para que el servicio JSONP responda antes de que se agote el tiempo de espera, en milisegundos.
      * ttl: Cantidad mínima de tiempo en milisegundos que transcurre entre llamadas al servicio JSONP. (Consulte la función [queryService](/help/sites-developing/contexthub-api.md#queryservice-reload)).


#### queryService(reload) {#queryservice-reload}

Consulta el servicio JSONP remoto y almacena en caché la respuesta. Si la cantidad de tiempo desde la llamada anterior a esta función es menor que el valor de `config.service.ttl`, no se llama al servicio y no se cambia la respuesta en caché. Opcionalmente, puede forzar la llamada del servicio. La propiedad `config.service.ttl`se establece al llamar a la función [init](/help/sites-developing/contexthub-api.md#init-name-config) para inicializar el almacén.

Activa el evento listo cuando la consulta ha finalizado. Si la URL del servicio JSONP no está configurada, la función no hace nada.

**Parámetros**

* **recarga:** (Boolean) Un valor true elimina la respuesta en caché y fuerza la llamada al servicio JSONP.

#### reset {#reset}

Restaura los valores iniciales de los datos persistentes del almacén y, a continuación, llama al servicio JSONP. Opcionalmente, puede eliminar todos los demás datos de la tienda. El evento se pone en pausa para este almacén mientras se restablecen los valores iniciales. Esta función no devuelve ningún valor.

Los valores iniciales se proporcionan en la propiedad initialValues del objeto config que se utiliza para crear una instancia del objeto store.

**Parámetros**

* **keepReminningData:** (Boolean) Un valor true hace que se mantengan los datos no iniciales. Un valor false hace que se eliminen todos los datos excepto los valores iniciales.

#### resolveParameter(f) {#resolveparameter-f}

Resuelve el parámetro dado.

## ContextHub.Store.PersistedJSONPStore {#contexthub-store-persistedjsonpstore}

ContextHub.Store.PersistedJSONPStore amplía [ContextHub.Store.JSONPStore](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore) para que hereda todas las funciones de esa clase. Sin embargo, los datos recuperados del servicio JSONP se mantienen según la configuración de la persistencia de ContextHub. (Consulte [Modos de persistencia](/help/sites-developing/ch-adding.md#persistence-modes).)

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

ContextHub.Store.PersistedStore amplía [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) para que hereda todas las funciones de esa clase. Los datos de este almacén se conservan según la configuración de la persistencia de ContextHub.

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

ContextHub.Store.SessionStore amplía [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) para que hereda todas las funciones de esa clase. Los datos de este almacén se conservan mediante la resistencia en memoria (objeto Javascript).

## ContextHub.UI {#contexthub-ui}

Gestiona los módulos de interfaz de usuario y los procesadores de módulos de interfaz de usuario.

### Funciones (ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType, renderer, dontRender) {#registerrenderer-moduletype-renderer-dontrender}

Registra un procesador de módulos de interfaz de usuario con ContextHub. Una vez registrado el procesador, se puede utilizar para [crear módulos de interfaz de usuario](ch-configuring.md#adding-a-ui-module). Utilice esta función cuando [extienda ContextHub.UI.BaseModuleRenderer](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types) para crear un procesador de módulos de interfaz de usuario personalizado.

**Parámetros**

* **moduleType:** (String) El identificador del procesador de módulos de interfaz de usuario. Si un procesador ya está registrado con el valor especificado, el procesador existente no estará registrado antes de que se registre este procesador.
* **procesador:** (Cadena) nombre de la clase que procesa el módulo de interfaz de usuario.
* **dontRender:** (Booleano) Se establece en  `true` para evitar que la interfaz de usuario de ContextHub se procese después de registrar el procesador. El valor predeterminado es `false`.

**Ejemplo**

En el siguiente ejemplo se registra un procesador como tipo de módulo contexthub.browserinfo.

```
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

Clase de utilidad para interactuar con cookies.

### Funciones (ContextHub.Utils.Cookie) {#functions-contexthub-utils-cookie}

#### exists(key) {#exists-key}

Determina si existe una cookie.

**Parámetros**

* **key:** Un  `String` que contiene la clave de la cookie para la que está realizando la prueba.

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

* (Opcional) **filter:** Criterios para coincidencia de claves de cookie. Para devolver todas las cookies, especifique ningún valor. Se admiten los siguientes tipos:

   * Cadena: La cadena se compara con la clave de cookie.
   * Matriz: Cada elemento de la matriz es un filtro.
   * Un objeto RegExp: La función de prueba del objeto se utiliza para hacer coincidir las claves de cookie.
   * Una función: Función que prueba una clave de cookie para una coincidencia. La función debe tomar la clave de cookie como parámetro y devolver true si la prueba confirma una coincidencia.

**Devuelve**

Objeto de cookies. Las propiedades de objeto son claves de cookie y los valores clave son valores de cookie.

**Ejemplo**

```
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

Devuelve un valor de cookie.

**Parámetros**

* **clave:** la clave de la cookie para la que desea el valor.

**Devuelve**

El valor de la cookie o `null` si no se encontró ninguna cookie para la clave.

**Ejemplo**

```
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter) {#getkeys-filter}

Devuelve una matriz de las claves de las cookies existentes que coinciden con un filtro.

**Parámetros**

* **filter:** Criterios para coincidencia de claves de cookie. Se admiten los siguientes tipos:

   * Cadena: La cadena se compara con la clave de cookie.
   * Matriz: Cada elemento de la matriz es un filtro.
   * Un objeto RegExp: La función de prueba del objeto se utiliza para hacer coincidir las claves de cookie.
   * Una función: Función que prueba una clave de cookie para una coincidencia. La función debe tomar la clave de cookie como parámetro y devolver `true` si la prueba confirma una coincidencia.

**Devuelve**

Matriz de cadenas donde cada cadena es la clave de una cookie que coincide con el filtro.

**Ejemplo**

```
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key, options) {#removeitem-key-options-1}

Elimina una cookie. Para eliminar la cookie, el valor se establece en una cadena vacía y la fecha de caducidad se establece en el día anterior a la fecha actual.

**Parámetros**

* **key:** un  `String` valor que representa la clave de la cookie que se va a eliminar.

* **opciones:** Objeto que contiene valores de propiedad para configurar los atributos de cookie. Consulte la función ` [setItem](/help/sites-developing/contexthub-api.md#setitem-key-value-options)` para obtener más información. La propiedad `expires` no tiene ningún efecto.

**Devuelve**

Esta función no devuelve un valor.

**Ejemplo**

```
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(key, value, options) {#setitem-key-value-options-1}

Crea una cookie de la clave y el valor dados y la agrega al documento actual. De forma opcional, puede especificar opciones para configurar los atributos de la cookie.

**Parámetros**

* **key:** Cadena que contiene la clave de la cookie.
* **value:** Una cadena que contiene el valor de la cookie.
* **opciones:**  (Opcional) Objeto que contiene cualquiera de las siguientes propiedades que configuran los atributos de cookie:

   * caduca: Un valor `date` o `number` que especifica cuándo caduca la cookie. Un valor de fecha especifica la hora absoluta de caducidad. Un número (en días) establece la hora de caducidad en la hora actual más el número. El valor predeterminado es `undefined`.
   * secure: Un valor `boolean` que especifica el atributo `Secure` de la cookie. El valor predeterminado es `false`.
   * path: Un valor `String` que se usará como el atributo `Path` de la cookie. El valor predeterminado es `undefined`.

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

Elimina todas las cookies que coinciden con un filtro determinado. Las cookies se comparan mediante la función getKeys y se eliminan mediante la función removeItem.

**Parámetros**

* **filter:** El  `filter` argumento que se va a utilizar en la llamada a la  `[getKeys](/help/sites-developing/contexthub-api.md#getkeys-filter)` función.

* **opciones:** el  `options` argumento que se va a utilizar en la llamada a la  `[removeItem](/help/sites-developing/contexthub-api.md#removeitem-key-options)` función.

**Devuelve**

Esta función no devuelve un valor.

## ContextHub.Utils.Eventing {#contexthub-utils-eventing}

Permite enlazar y desenlazar funciones a eventos de la tienda de ContextHub. Acceda a los objetos ContextHub.Utils.Eventing de una tienda mediante la propiedad [eventing](/help/sites-developing/contexthub-api.md#eventing) de la tienda.

### Funciones (ContextHub.Utils.Eventing) {#functions-contexthub-utils-eventing}

#### off(name, selector) {#off-name-selector}

Desenlaza una función de un evento.

**Parámetros**

* **name:** El  [nombre del ](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) evento para el que se está desvinculando la función.

* **selector:** Selector que identifica el enlace. (Consulte el parámetro `selector` para las funciones [on](/help/sites-developing/contexthub-api.md#on-name-handler-selector-triggerforpastevents) y [once](/help/sites-developing/contexthub-api.md#once-name-handler-selector-triggerforpastevents)).

**Devuelve**

Esta función no devuelve ningún valor.

#### on(nombre, controlador, selector, desencadenadorForPastEvents) {#on-name-handler-selector-triggerforpastevents}

Enlaza una función a un evento. Se llama a la función cada vez que se produce el evento. Opcionalmente, la función se puede llamar para eventos que hayan ocurrido en el pasado, antes de que se establezca el enlace.

**Parámetros**

* **name:** (String) El  [nombre del ](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) evento al que está enlazando la función.

* **handler:** (Function) La función que se va a enlazar al evento.
* **selector:** (String) Un identificador único para el enlace. Necesita el selector para identificar el enlace si desea utilizar la función `off` para quitar el enlace.

* **activateForPastEvents:** (Boolean) Indica si el controlador debe ejecutarse para eventos que se hayan producido en el pasado. Un valor de `true` llama al controlador para eventos anteriores. Un valor de `false` llama al controlador para futuros eventos. El valor predeterminado es `true`.

**Devuelve**

Cuando el argumento `triggerForPastEvents` es `true`, esta función devuelve un valor `boolean` que indica si el evento se produjo en el pasado:

* `true`:: El evento se produjo en el pasado y se llamará al controlador.
* `false`:: El evento no ha ocurrido en el pasado.

Si `triggerForPastEvents` es `false`, esta función no devuelve ningún valor.

**Ejemplo**

El ejemplo siguiente enlaza una función al evento de datos del almacén de geolocalización. La función rellena un elemento de la página con el valor del elemento de datos de latitud del almacén.

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

#### once(nombre, controlador, selector, desencadenadorForPastEvents) {#once-name-handler-selector-triggerforpastevents}

Enlaza una función a un evento. La función se llama una sola vez, para la primera incidencia del evento. Opcionalmente, la función se puede llamar para el evento que se ha producido en el pasado, antes de que se establezca el enlace.

**Parámetros**

* **name:** (String) El  [nombre del ](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) evento al que está enlazando la función.

* **handler:** (Function) La función que se va a enlazar al evento.
* **selector:** (String) Un identificador único para el enlace. Necesita el selector para identificar el enlace si desea utilizar la función `off` para quitar el enlace.

* **activateForPastEvents:** (Boolean) Indica si el controlador debe ejecutarse para eventos que se hayan producido en el pasado. Un valor de `true` llama al controlador para eventos anteriores. Un valor de `false` llama al controlador para futuros eventos. El valor predeterminado es `true`.

**Devuelve**

Cuando el argumento `triggerForPastEvents` es `true`, esta función devuelve un valor `boolean` que indica si el evento se produjo en el pasado:

* `true`:: El evento se produjo en el pasado y se llamará al controlador.
* `false`:: El evento no ha ocurrido en el pasado.

Si `triggerForPastEvents` es `false`, esta función no devuelve ningún valor.

## ContextHub.Utils.herencia {#contexthub-utils-inheritance}

Clase de utilidad que permite a un objeto heredar las propiedades y los métodos de otro objeto.

### Funciones (ContextHub.Utils.herencia) {#functions-contexthub-utils-inheritance}

#### inherit(child, parent) {#inherit-child-parent}

Hace que un objeto herede las propiedades y los métodos de otro objeto.

**Parámetros**

* **child:** (Object) El objeto que hereda.
* **parent:** (Object) el objeto que define las propiedades y los métodos heredados.

## ContextHub.Utils.JSON {#contexthub-utils-json}

Proporciona funciones para serializar objetos en formato JSON y deserializar cadenas JSON en objetos.

### Funciones (ContextHub.Utils.JSON) {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

Analiza un valor de cadena como JSON y lo convierte en un objeto javascript.

**Parámetros**

* **data:** Un valor de cadena en formato JSON.

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

* **data:** el valor o el objeto que se va a serializar. Esta función admite valores booleanos, de matriz, de número, de cadena y de fecha.

**Devuelve**

El valor de la cadena serializada. Cuando `data` es un valor R `egExp`, esta función devuelve un objeto vacío. Cuando `data` es una función, devuelve `undefined`.

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

Esta clase facilita la manipulación de objetos de datos que se van a almacenar o recuperar de los almacenes de ContextHub.

### Funciones (ContextHub.Utils.JSON.tree) {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

Crea una copia de un objeto de datos y le agrega el árbol de datos desde un segundo objeto. La función devuelve la copia y no modifica ninguno de los objetos originales. Cuando los árboles de datos de los dos objetos contienen claves idénticas, el valor del segundo objeto sobrescribe el valor del primer objeto.

**Parámetros**

* **tree:** El objeto que se copia.
* **secondTree:** El objeto que se combina con la copia del  `tree` objeto.

**Devuelve**

Objeto que contiene los datos combinados.

#### clean() {#cleanup}

Crea una copia de un objeto, busca y elimina los elementos del árbol de datos que no contienen valores, valores nulos o valores no definidos, y devuelve la copia.

**Parámetros**

* **tree:** El objeto que se va a limpiar.

**Devuelve**

Una copia del árbol que se limpia.

#### getItem() {#getitem}

Recupera el valor de un objeto para una clave.

**Parámetros**

* **tree:** El objeto de datos.
* **key:** la clave del valor que desea recuperar.

**Devuelve**

Valor que corresponde a la clave. Cuando la clave tiene claves secundarias, esta función devuelve un objeto complejo. Cuando el tipo de valor de la clave es `undefined`, se devuelve `null`.

**Ejemplo**

Considere el siguiente objeto Javascript:

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

Recupera todas las claves del árbol de datos de un objeto. De forma opcional, solo puede recuperar las claves de los elementos secundarios de una clave específica. También puede especificar de forma opcional un orden de las claves recuperadas.

**Parámetros**

* **tree:** El objeto desde el que se recuperan las claves del árbol de datos.
* **parent:**  (opcional) la clave de un elemento en el árbol de datos para el que desea recuperar las claves de los elementos secundarios.
* **order:** (Opcional) Una función que determina el orden de clasificación de las claves devueltas. (Consulte [Array.prototype.sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) en Mozilla Developer Network.)

**Devuelve**

Matriz de claves.

**Ejemplo**

Considere el siguiente objeto:

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

La secuencia de comandos `ContextHub.Utils.JSON.tree.getKeys(myObject);` devuelve la siguiente matriz:

```
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

Crea una copia de un objeto determinado, quita la rama especificada del árbol de datos y devuelve la copia modificada.

**Parámetros**

* tree: Un objeto de datos.
* key: Clave que se va a quitar.

**Devuelve**

Una copia del objeto de datos original con la clave eliminada.

**Ejemplo**

Considere el siguiente objeto:

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

Sanitiza los valores de cadena para que se puedan utilizar como claves. Para sanear una cadena, esta función realiza las siguientes acciones:

* Reduce varias barras diagonales consecutivas a una sola barra diagonal.
* Elimina los espacios en blanco del principio y del final de la cadena.
* Divide el resultado en una matriz de cadenas que están delimitadas por barras diagonales.

Utilice la matriz resultante para crear una clave utilizable.  **Parámetros**

* **key:** El  `string` que sanear.

**Devuelve**

Matriz de valores `string` donde cada cadena es la porción del `key` que se delimitó mediante barras diagonales. representa la clave saneada. Si la matriz saneada tiene una longitud de cero, esta función devuelve `null`.

**Ejemplo**

El siguiente código elimina una cadena para producir la matriz `["this", "is", "a", "path"]` y, a continuación, genera la clave `"/this/is/a/path"` de la matriz:

```
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(tree, key, value) {#setitem-tree-key-value}

Añade un par clave/valor en el árbol de datos de una copia de un objeto. Para obtener información sobre los árboles de datos, consulte [Persistencia](/help/sites-developing/contexthub.md#persistence).

**Parámetros**

* tree: Un objeto de datos.
* key: La clave que se asociará al valor que se está agregando. La clave es la ruta del elemento en el árbol de datos. Esta función llama a `ContextHub.Utils.JSON.tree.sanitize` para sanear la clave antes de agregarla.
* value: Valor que se va a agregar al árbol de datos.

**Devuelve**

Una copia del objeto `tree` que incluye el par `key`/ `value`.

**Ejemplo**

Considere el siguiente código Javascript:

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

Le permite registrar candidatos para tiendas y obtener candidatos para tiendas registradas.

### Funciones (ContextHub.Utils.storeCandidate) {#functions-contexthub-utils-storecandidates}

#### getRegisteredCandidate(storeType) {#getregisteredcandidates-storetype}

Devuelve los tipos de tienda registrados como candidatos de tienda. Recupere los candicados registrados de un tipo de almacén específico o de todos los tipos de tienda.

**Parámetros**

* **storeType:** (String) El nombre del tipo de almacén. Consulte el parámetro `storeType` de la función [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates).

**Devuelve**

Objeto de tipos de almacén. Las propiedades de objeto son los nombres de tipo de almacén y los valores de propiedad son una matriz de candidatos de almacén registrados.

#### getStoreFromCandidate(storeType) {#getstorefromcandidates-storetype}

Devuelve un tipo de tienda de los candidatos registrados. Si se registra más de un tipo de almacén con el mismo nombre, la función devuelve el tipo de almacén con la prioridad más alta.

**Parámetros**

* storeType: (Cadena) El nombre del candidato de la tienda. Consulte el parámetro `storeType` de la función [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies).

**Devuelve**

Objeto que representa el candidato de almacén registrado. Si el tipo de almacén solicitado no está registrado, se genera un error.

#### getSupportedStoreTypes() {#getsupportedstoretypes}

Devuelve los nombres de los tipos de tienda registrados como candidatos de tienda. Esta función no requiere parámetros.

**Devuelve**

Matriz de valores de cadena, donde cada cadena es el tipo de tienda con el que se registró un candidato a la tienda. Consulte el parámetro `storeType` de la función [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates).

#### registerStoreCandidate(store, storeType, priority, apply) {#registerstorecandidate-store-storetype-priority-applies}

Registra un objeto de almacén como candidato de almacén con un nombre y una prioridad.

La prioridad es un número que indica la importancia de las tiendas con el mismo nombre. Cuando un candidato a tienda se registra con el mismo nombre que un candidato a tienda ya registrado, se utiliza el candidato con mayor prioridad. Cuando se registra un candidato a tienda, la tienda se registra solo si la prioridad es mayor que la de los candidatos a tiendas registradas con el mismo nombre.

**Parámetros**

* **store:** (Object) El objeto store que se va a registrar como candidato de almacén.
* **storeType:** (String) El nombre del candidato de la tienda. Este valor es necesario cuando se crea una instancia del candidato de la tienda.
* **prioridad:** (número) La prioridad del candidato de la tienda.
* **aplica:** (Función) la función que se va a invocar que evalúa la aplicabilidad del almacén en el entorno actual. La función debe devolver `true` si el almacén es aplicable y `false` en caso contrario. El valor predeterminado es una función que devuelve true: `function() {return true;}`

**Ejemplo**

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```

