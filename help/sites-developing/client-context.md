---
title: Client Context en detalle
seo-title: Client Context en detalle
description: Client Context representa una colección de datos de usuario formada dinámicamente
seo-description: Client Context representa una colección de datos de usuario formada dinámicamente
uuid: 95b08fbd-4f50-44a1-80fb-46335fe04a40
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: c881ad66-bcc3-4f99-b77f-0944c23e2d29
docset: aem65
feature: Context Hub
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3025'
ht-degree: 0%

---


# Contexto de cliente en detalle{#client-context-in-detail}

>[!NOTE]
>
>Context del cliente ha sido reemplazado por ContextHub. Consulte la [documentación relacionada](/help/sites-developing/contexthub.md) para obtener más información.

Client Context representa una colección de datos de usuario ensamblada dinámicamente. Puede utilizar los datos para determinar el contenido que se mostrará en una página web en una situación determinada (segmentación de contenido). Los datos también están disponibles para el análisis de sitios web y para cualquier javascript de la página.

Client Context consta principalmente de los siguientes aspectos:

* El almacén de sesiones, que contiene los datos del usuario.
* La IU que muestra los datos del usuario y proporciona herramientas para simular su experiencia.
* Una [API de javascript](/help/sites-developing/ccjsapi.md) para interactuar con almacenes de sesiones.

Para crear un almacén de sesiones independiente y agregarlo a Client Context, o crear un almacén de sesiones vinculado a un componente de Context Store. AEM instala varios componentes de Context Store que puede utilizar de inmediato. Puede utilizar estos componentes como base para sus componentes.

Para obtener información sobre cómo abrir Client Context, configurar la información que se muestra y simular la experiencia del usuario, consulte [Client Context](/help/sites-administering/client-context.md).

## Almacenamiento de sesión {#session-stores}

Client Context incluye varios almacenes de sesión que contienen datos de usuario. Los datos del almacén proceden de las siguientes fuentes:

* El explorador web del cliente.
* El servidor (consulte [JSONP Store](/help/sites-administering/client-context.md#main-pars-variable-8) para almacenar información de fuentes de terceros)

El marco de trabajo de Client Context proporciona una [API de javascript](/help/sites-developing/ccjsapi.md) que puede utilizar para interactuar con almacenes de sesiones a fin de leer y escribir datos de usuarios, y escuchar y reaccionar ante eventos de almacenamiento. También puede crear almacenes de sesión para datos de usuario que utilice con fines de segmentación de contenido u otros fines.

Los datos del almacén de sesiones permanecen en el cliente. Client Context no vuelve a escribir datos en el servidor. Para enviar datos al servidor, utilice un formulario o desarrolle javascript personalizado.

Cada almacén de sesión es una colección de pares de propiedad-valor. El almacén de sesiones representa una colección de datos (de cualquier tipo), cuyo significado conceptual puede ser decidido por el diseñador y/o desarrollador. El siguiente ejemplo de código javascript define un objeto que representa los datos de perfil que podría contener el almacén de sesiones:

```
{
  age: 20,
  authorizableId: "aparker@geometrixx.info",
  birthday: "27 Feb 1992",
  email: "aparker@geometrixx.info",
  formattedName: "Alison Parker",
  gender: "female",
  path: "/home/users/geometrixx/aparker@geometrixx.info/profile"
}
```

Un almacén de sesiones se puede mantener en todas las sesiones del explorador o solo puede durar durante la sesión del explorador en la que se crea.

>[!NOTE]
>
>La persistencia del almacén utiliza el almacenamiento del explorador o las cookies (la cookie `SessionPersistence` ). El almacenamiento del explorador es más común.
>
>Cuando se cierra y vuelve a abrir el explorador, se puede cargar un almacén de sesión con los valores de un almacén persistente. A continuación, es necesario borrar la caché del explorador para eliminar los valores antiguos.

### Componentes de almacenamiento de contexto {#context-store-components}

Un componente de almacén de contexto es un componente de CQ que se puede añadir a Client Context. Normalmente, los componentes del almacén de contexto muestran datos de un almacén de sesión con el que están asociados. Sin embargo, la información que muestran los componentes del almacén de contexto no se limita a los datos del almacén de sesiones.

Los componentes del almacén de contexto pueden incluir los siguientes elementos:

* Secuencias de comandos JSP que definen el aspecto en Client Context.
* Propiedades para mostrar el componente en la barra de tareas.
* Edite los cuadros de diálogo para configurar instancias de componentes.
* Javascript que inicializa el almacén de sesiones.

Para obtener una descripción de los componentes de almacén de contexto instalados que puede agregar al almacén de contexto, consulte [Componentes de contexto de cliente disponibles](/help/sites-administering/client-context.md#available-client-context-components).

>[!NOTE]
>
>Los datos de página ya no están en ClientContext como componente predeterminado. Si es necesario, puede agregarlo editando el contexto del cliente, agregando el componente **Propiedades de almacén genéricas** y, a continuación, configurándolo para definir el **Almacenamiento** como `pagedata`.

### Entrega de contenido dirigido {#targeted-content-delivery}

La información de perfil también se utiliza para enviar [contenido de destino](/help/sites-authoring/content-targeting-touch.md).

![clientcontext_](assets/clientcontext_targetedcontentdelivery.png) ![targetedcontentdeliveryclientcontext_targetedcontentdeliverydetail](assets/clientcontext_targetedcontentdeliverydetail.png)

## Adición De Contexto De Cliente A Una Página {#adding-client-context-to-a-page}

Incluya el componente Client Context en la sección del cuerpo de las páginas web para habilitar Client Context. La ruta del nodo del componente Client Context es `/libs/cq/personalization/components/clientcontext`. Para incluir el componente, añada el siguiente código al archivo JSP del componente de página, situado justo debajo del elemento `body` de la página:

```java
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

El componente clientcontext hace que la página cargue las bibliotecas de cliente que implementan Client Context.

* La API de JavaScript de Client Context.
* El marco de Client Context que admite almacenes de sesiones, administración de eventos, etc.
* Segmentos definidos.
* Secuencias de comandos init.js que se generan para cada componente de almacén de contexto que se ha agregado a Client Context.
* (Solo instancia de autor) La interfaz de usuario de Client Context.

La interfaz de usuario de Client Context solo está disponible en la instancia de autor.

## Extensión de Client Context {#extending-client-context}

Para ampliar Client Context, cree un almacén de sesiones y, opcionalmente, muestre los datos del almacén:

* Cree un almacén de sesiones para los datos de usuario necesarios para la segmentación de contenido y el análisis web.
* Cree un componente de almacén de contexto para permitir a los administradores configurar el almacén de sesiones asociado y mostrar los datos de almacenamiento en Client Context para realizar pruebas.

>[!NOTE]
>
>Si tiene (o crea) un servicio `JSONP` que puede proporcionar los datos, simplemente puede utilizar el componente de almacén de contexto `JSONP` y asignarlo al servicio JSONP. Esto administrará el almacén de sesiones.

### Creación de un almacén de sesiones {#creating-a-session-store}

Cree un almacén de sesiones para los datos que debe añadir y recuperar de Client Context. Por lo general, se utiliza el siguiente procedimiento para crear un almacén de sesiones:

1. Cree una carpeta de biblioteca de cliente que tenga un valor de propiedad `categories` de `personalization.stores.kernel`. Client Context carga automáticamente las bibliotecas de cliente de esta categoría.

1. Configure la carpeta de la biblioteca del cliente para que tenga una dependencia de la carpeta de la biblioteca del cliente `personalization.core.kernel`. La biblioteca de cliente `personalization.core.kernel` proporciona la API de JavaScript de Client Context.

1. Agregue el javascript que crea e inicializa el almacén de sesiones.

Al incluir el javascript en la biblioteca de cliente personalization.store.kernel , el almacén se crea cuando se carga el marco de cliente.

>[!NOTE]
>
>Si está creando un almacén de sesiones como parte de un componente de almacén de contexto, puede colocar el javascript en el archivo init.js.jsp del componente. En este caso, el almacén de sesiones solo se crea si el componente se agrega a Client Context.

#### Tipos de almacenes de sesión {#types-of-session-stores}

Los almacenes de sesión se crean y están disponibles durante una sesión del explorador o se mantienen en el almacenamiento del explorador o en las cookies. La API de JavaScript de Client Context define varias clases que representan ambos tipos de almacenes de datos:

* ` [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore)`: Estos objetos residen únicamente en el DOM de la página. Los datos se crean y mantienen durante toda la página.
* ` [CQ_Analytics.PerstistedSessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedsessionstore)`: Estos objetos residen en el DOM de página y se conservan en el almacenamiento del explorador o en las cookies. Los datos están disponibles en todas las páginas y en todas las sesiones de usuario.

La API también proporciona extensiones de estas clases que están especializadas para almacenar datos JSON o datos JSONP:

* Objetos de solo sesión: [CQ_Analytics.JSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-jsonstore) y [CQ_Analytics.JSONPStore](/help/sites-developing/ccjsapi.md#cq-analytics-jsonpstore).

* Objetos persistentes: [CQ_Analytics.PersistedJSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedjsonstore) y [CQ_Analytics.PersistedJSONPStore](/help/sites-developing/ccjsapi.md#cq-analyics-persistedjsonpstore).

#### Creación del objeto Almacén de sesión {#creating-the-session-store-object}

El javascript de la carpeta de biblioteca del cliente crea e inicializa el almacén de sesiones. El almacén de sesiones debe registrarse mediante el Administrador del almacén de contexto. En el siguiente ejemplo se crea y registra un objeto [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore).

```
//Create the session store
if (!CQ_Analytics.MyStore) {
    CQ_Analytics.MyStore = new CQ_Analytics.SessionStore();
    CQ_Analytics.MyStore.STOREKEY = "MYSTORE";
    CQ_Analytics.MyStore.STORENAME = "mystore";
    CQ_Analytics.MyStore.data={};
}
//register the session store
if (CQ_Analytics.ClientContextMgr){
    CQ_Analytics.ClientContextMgr.register(CQ_Analytics.MyStore)
}
```

Para almacenar datos JSON, en el siguiente ejemplo se crea y registra un objeto [CQ_Analytics.JSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore).

```
if (!CQ_Analytics.myJSONStore) {
    CQ_Analytics.myJSONStore = CQ_Analytics.JSONStore.registerNewInstance("myjsonstore",{});
}
```

### Creación de un componente de almacén de contexto {#creating-a-context-store-component}

Cree un componente de almacén de contexto para procesar los datos del almacén de sesiones en Client Context. Una vez creado, puede arrastrar el componente de almacén de contexto a Client Context para procesar los datos de un almacén de sesiones. Los componentes del almacén de contexto constan de los siguientes elementos:

* Secuencia de comandos JSP para procesar los datos.
* Un cuadro de diálogo de edición.
* Un script JSP para inicializar el almacén de sesiones.
* (Opcional) Una carpeta de biblioteca de cliente que crea el almacén de sesiones. No es necesario incluir la carpeta de la biblioteca del cliente si el componente utiliza un almacén de sesión existente.

#### Ampliación de los componentes proporcionados del almacén de contexto {#extending-the-provided-context-store-components}

AEM proporciona los componentes del almacén de contexto de genericstore y genericstoreproperties que puede ampliar. La estructura de los datos de almacenamiento determina el componente que se amplía:

* Pares de propiedad-valor: Amplíe el componente `GenericStoreProperties`. Este componente procesa automáticamente las tiendas de pares de propiedad-valor. Se proporcionan varios puntos de interacción:

   * `prolog.jsp` y  `epilog.jsp`: interacción de componentes que le permite añadir lógica del lado del servidor antes o después del procesamiento de componentes.

* Datos complejos: Amplíe el componente `GenericStore`. El almacén de sesiones necesitará un método de &quot;renderizador&quot; al que se llamará cada vez que se necesite procesar el componente. Se llama a la función de renderizador con dos parámetros:

   * `@param {String} store`
El almacén que se va a procesar

   * `@param {String} divId`
Id del div en el que se debe representar el almacén.

>[!NOTE]
>
>Todos los componentes de Client Context son extensiones de los componentes Generic Store o Generic Store Properties . Hay varios ejemplos instalados en la carpeta `/libs/cq/personalization/components/contextstores`.

#### Configuración del aspecto en la barra de tareas {#configuring-the-appearance-in-sidekick}

Al editar Client Context, los componentes del almacén de contexto aparecen en la barra de tareas. Al igual que con todos los componentes, las propiedades `componentGroup` y `jcr:title` del componente ClientContext determinan el grupo y el nombre del componente.

Todos los componentes que tienen un valor de propiedad `componentGroup` de `Client Context` aparecen en la barra de tareas de forma predeterminada. Si utiliza un valor diferente para la propiedad `componentGroup`, debe agregar manualmente el componente a la barra de tareas mediante el modo Diseño.

#### Instancias de componentes del almacén de contexto {#context-store-component-instances}

Cuando se agrega un componente de almacén de contexto a Client Context, un nodo que representa la instancia del componente se crea debajo de `/etc/clientcontext/default/content/jcr:content/stores`. Este nodo contiene los valores de propiedad que se configuran mediante el cuadro de diálogo de edición del componente.

Cuando Client Context se inicializa, estos nodos se procesan.

#### Inicialización del almacén de sesiones asociado {#initializing-the-associated-session-store}

Añada un archivo init.js.jsp a su componente para generar código javascript que inicialice el almacén de sesiones que utiliza el componente de almacén de contexto. Por ejemplo, utilice la secuencia de comandos de inicialización para recuperar las propiedades de configuración del componente y utilícelas para rellenar el almacén de sesiones.

El javascript que se genera se agrega a la página cuando Client Context se inicializa en la carga de la página, tanto en la instancia de autor como en la de publicación. Este JSP se ejecuta antes de que la instancia de componente del almacén de contexto se cargue y procese.

El código debe establecer el tipo mime del archivo en `text/javascript` o no se ejecuta.

>[!CAUTION]
>
>La secuencia de comandos init.js.jsp se ejecuta en la instancia de autor y publicación, pero solo si el componente de almacén de contexto se agrega a Client Context.

El siguiente procedimiento crea el archivo de script init.js.jsp y agrega el código que establece el tipo de mime correcto. El código que realiza la inicialización del almacén sería el siguiente.

1. Haga clic con el botón derecho en el nodo de componente del almacén de contexto y haga clic en Crear > Crear archivo.
1. En el campo Nombre, escriba `init.js.jsp` y haga clic en Aceptar.
1. En la parte superior de la página, añada el siguiente código y luego haga clic en Guardar todo.

   ```java
   <%@page contentType="text/javascript" %>
   ```

### Procesamiento de datos del almacén de sesión para componentes de genericstoreproperties {#rendering-session-store-data-for-genericstoreproperties-components}

Muestre los datos del almacén de sesiones en Client Context con un formato coherente.

#### Visualización de datos de propiedad {#displaying-property-data}

La biblioteca de etiquetas de personalización proporciona la etiqueta `personalization:storePropertyTag` que muestra el valor de una propiedad de un almacén de sesiones. Para utilizar la etiqueta , incluya la siguiente línea de código en su archivo JSP:

```xml
<%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
```

La etiqueta tiene el siguiente formato:

```xml
<personalization:storePropertyTag propertyName="property_name" store="session_store_name"/>
```

El atributo `propertyName` es el nombre de la propiedad store que se va a mostrar. El atributo `store` es el nombre del almacén registrado. La siguiente etiqueta de ejemplo muestra el valor de la propiedad `authorizableId` del almacén `profile`:

```xml
<personalization:storePropertyTag propertyName="authorizableId" store="profile"/>
```

#### Estructura HTML {#html-structure}

La carpeta de biblioteca de cliente de personalization.ui (/etc/clientlibs/foundation/personalization/ui/themes/default) proporciona los estilos CSS que utiliza Client Context para dar formato al código HTML. El siguiente código ilustra la estructura sugerida para usarla para mostrar los datos del almacén:

```xml
<div class="cq-cc-store">
   <div class="cq-cc-thumbnail">
      <div class="cq-cc-store-property">
           <!-- personalization:storePropertyTag for the store thumbnail image goes here -->
      </div>
   </div>
   <div class="cq-cc-content">
       <div class="cq-cc-store-property cq-cc-store-property-level0">
           <!-- personalization:storePropertyTag for a store property goes here -->
       </div>
       <div class="cq-cc-store-property cq-cc-store-property-level1">
           <!-- personalization:storePropertyTag for a store property goes here -->
       </div>
       <div class="cq-cc-store-property cq-cc-store-property-level2">
           <!-- personalization:storePropertyTag for a store property goes here -->
       </div>
       <div class="cq-cc-store-property cq-cc-store-property-level3">
           <!-- personalization:storePropertyTag for a store property goes here -->
       </div>
   </div>
   <div class="cq-cc-clear"></div>
</div>
```

El componente de almacén de contexto `/libs/cq/personalization/components/contextstores/profiledata` utiliza esta estructura para mostrar los datos del almacén de sesiones de perfil. La clase `cq-cc-thumbnail` coloca la imagen en miniatura. Las clases `cq-cc-store-property-level*x*` dan formato a los datos alfanuméricos:

* level0, level1 y level2 se distribuyen verticalmente y utilizan una fuente blanca.
* nivel 3, y cualquier nivel adicional, se distribuyen horizontalmente y utilizan una fuente blanca con un fondo más oscuro.

![Chlimage_1-4](assets/chlimage_1-4.png)

### Procesamiento de datos del almacén de sesión para componentes de almacén de genéricos {#rendering-session-store-data-for-genericstore-components}

Para procesar los datos del almacén mediante un componente de almacén de datos genéricos, debe:

* Agregue la etiqueta personalization:storeRendererTag al script JSP del componente para identificar el nombre del almacén de sesiones.
* Implemente un método de renderización en la clase de almacén de sesiones.

#### Identificación del almacén de sesión de genericstore {#identifying-the-genericstore-session-store}

La biblioteca de etiquetas de personalización proporciona la etiqueta `personalization:storePropertyTag` que muestra el valor de una propiedad de un almacén de sesiones. Para utilizar la etiqueta , incluya la siguiente línea de código en su archivo JSP:

```xml
<%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
```

La etiqueta tiene el siguiente formato:

```java
<personalization:storeRendererTag store="store_name"/>
```

#### Implementación del método de renderizador del almacén de sesiones {#implementing-the-session-store-renderer-method}

El almacén de sesiones necesitará un método de &quot;renderizador&quot; al que se llamará cada vez que se necesite procesar el componente. Se llama a la función de renderizador con dos parámetros:

* @param {String} tienda
El almacén que se va a procesar
* @param {String} divId
Id del div en el que se debe representar el almacén.

## Interactuar con almacenes de sesión {#interacting-with-session-stores}

Utilice javascript para interactuar con almacenes de sesiones.

### Acceso a los almacenes de sesión {#accessing-session-stores}

Obtenga un objeto de almacén de sesión para leer o escribir datos en el almacén. [CQ_Analytics.](/help/sites-developing/ccjsapi.md#cq-analytics-clientcontextmgr) ClientContextMgrproporciona acceso a las tiendas en función del nombre de la tienda. Una vez obtenidos, utilice los métodos de [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) o [CQ_Analytics.PersistedSessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedsessionstore) para interactuar con los datos del almacén.

El siguiente ejemplo obtiene el almacén `profile` y, a continuación, recupera la propiedad `formattedName` del almacén.

```
function getName(){
   var profilestore = CQ_Analytics.ClientContextMgr.getRegisteredStore("profile");
   if(profilestore){
      return profilestore.getProperty("formattedName", false);
   } else {
      return null;
   }
}
```

### Creación de un oyente para reaccionar a una actualización del almacén de sesiones {#creating-a-listener-to-react-to-a-session-store-update}

La sesión almacena eventos de activación, por lo que es posible añadir oyentes y eventos de déclencheur basados en estos eventos.

Los almacenes de sesión se crean siguiendo el patrón `Observable` . Amplían [ `CQ_Analytics.Observable`](/help/sites-developing/ccjsapi.md#cq-analytics-observable) que proporciona el método ` [addListener](/help/sites-developing/ccjsapi.md#addlistener-event-fct-scope)`.

En el siguiente ejemplo se agrega un oyente al evento `update` del almacén de sesiones `profile`.

```
var profileStore = ClientContextMgr.getRegisteredStore("profile");
if( profileStore ) {
  //callback execution context
  var executionContext = this;

  //add "update" event listener to store
  profileStore.addListener("update",function(store, property) {
    //do something on store update

  },executionContext);
}
```

### Comprobación de que un almacén de sesión está definido e inicializado {#checking-that-a-session-store-is-defined-and-initialized}

Los almacenes de sesión no están disponibles hasta que se cargan e inicializan con datos. Los siguientes factores pueden afectar al momento de disponibilidad del almacén de sesiones:

* Carga de página
* Carga de JavaScript
* Tiempo de ejecución de JavaScript
* Tiempos de respuesta para solicitudes XHR
* Cambios dinámicos en el almacén de sesiones

Utilice los métodos [CQ_Analytics.ClientContextUtils](/help/sites-developing/ccjsapi.md#cq-analytics-clientcontextutils) del objeto [onStoreRegistered](/help/sites-developing/ccjsapi.md#onstoreregistered-storename-callback) y [onStoreInitialized](/help/sites-developing/ccjsapi.md#onstoreinitialized-storename-callback-delay) para acceder a los almacenes de sesiones solo cuando estén disponibles. Estos métodos permiten registrar los oyentes de eventos que reaccionan a los eventos de registro e inicialización de la sesión.

>[!CAUTION]
>
>Si usted depende de otra tienda, usted necesita atender el caso de que la tienda nunca esté registrada.

El siguiente ejemplo utiliza el evento `onStoreRegistered` del almacén de sesiones `profile`. Cuando se registra el almacén, se agrega un oyente al evento `update` del almacén de sesiones. Cuando se actualiza el almacén, el contenido del elemento `<div class="welcome">` de la página se actualiza con el nombre del almacén `profile`.

```
//listen for the store registration
CQ_Analytics.ClientContextUtils.onStoreRegistered("profile", listen);

//listen for the store's update event
function listen(){
 var profilestore = CQ_Analytics.ClientContextMgr.getRegisteredStore("profile");
    profilestore.addListener("update",insertName);
}

//insert the welcome message
function insertName(){
 $("div.welcome").text("Welcome "+getName());
}

//obtain the name from the profile store
function getName(){
 var profilestore = CQ_Analytics.ClientContextMgr.getRegisteredStore("profile");
 if(profilestore){
  return profilestore.getProperty("formattedName", false);
    } else {
        return null;
    }
}
```

### Exclusión de una propiedad de la cookie de persistencia de sesión {#excluding-a-property-from-the-sessionpersistence-cookie}

Para evitar que una propiedad de `PersistedSessionStore` persista (es decir, excluirla de la cookie `sessionpersistence`), agregue la propiedad a la lista de propiedades no persistentes del almacén de sesión persistente.

Consulte ` [CQ_Analytics.PersistedSessionStore.setNonPersisted(propertyName)](/help/sites-developing/ccjsapi.md#setnonpersisted-name)`

```
CQ_Analytics.ClientContextUtils.onStoreRegistered("surferinfo", function(store) {
  //this will exclude the browser, OS and resolution properties of the surferinfo session store from the
  store.setNonPersisted("browser");
  store.setNonPersisted("OS");
  store.setNonPersisted("resolution");
});
```

## Configuración del deslizador del dispositivo {#configuring-the-device-slider}

### Condiciones {#conditions}

La página actual debe tener una página móvil correspondiente; esto solo se determina si la página tiene una LiveCopy configurada con una configuración de lanzamiento móvil ( `rolloutconfig.path.toLowerCase` contiene `mobile`).

#### Configuración {#configuration}

Al cambiar de la página de escritorio a su equivalente móvil:

* Se carga el DOM de la página móvil.
* El `div` principal (obligatorio) que contiene el contenido, se extrae e e inserta en la página de escritorio actual.

* Las clases CSS y body que deben cargarse deben configurarse manualmente.

Por ejemplo:

```
window.CQMobileSlider["geometrixx-outdoors"] = {
  //CSS used by desktop that need to be removed when mobile
  DESKTOP_CSS: [
    "/etc/designs/${app}/clientlibs_desktop_v1.css"
  ],

  //CSS used by mobile that need to be removed when desktop
  MOBILE_CSS: [
    "/etc/designs/${app}/clientlibs_mobile_v1.css"
  ],

  //id of the content that needs to be removed when mobile
  DESKTOP_MAIN_ID: "main",

  //id of the content that needs to be removed when desktop
  MOBILE_MAIN_ID: "main",

  //body classes used by desktop that need to be removed when mobile
  DESKTOP_BODY_CLASS: [
    "page"
  ],

  //body classes used by mobile that need to be removed when desktop
  MOBILE_BODY_CLASS: [
    "page-mobile"
  ]
};
```

## Ejemplo: Creación de un componente de almacén de contexto personalizado {#example-creating-a-custom-context-store-component}

En este ejemplo, se crea un componente de almacén de contexto que recupera datos de un servicio externo y lo almacena en el almacén de sesiones:

* Amplía el componente genericstoreproperties .
* Inicializa una tienda utilizando un objeto javascript CQ_Analytics.JSONPStore .
* Llama a un servicio JSONP para recuperar datos y agregarlos a la tienda.
* Procesa los datos en Client Context.

### Añadir el componente geográfico {#add-the-geoloc-component}

Cree una aplicación CQ y añada el componente geolocalizado.

1. Abra el CRXDE Lite en su explorador web ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Haga clic con el botón derecho en la carpeta `/apps` y haga clic en Crear > Crear carpeta. Especifique un nombre de `myapp` y haga clic en Aceptar.
1. Del mismo modo, debajo de `myapp`, cree una carpeta con el nombre `contextstores`. &quot;
1. Haga clic con el botón derecho en la carpeta `/apps/myapp/contextstores` y haga clic en Crear > Crear componente. Especifique los siguientes valores de propiedad y haga clic en Siguiente:

   * Etiqueta: geoloc
   * Título: Tienda de ubicación
   * Super Tipo: cq/personalization/components/contextstores/genericstoreproperties
   * Grupo: ClientContext

1. En el cuadro de diálogo Crear componente, haga clic en Siguiente en cada página hasta que se active el botón Aceptar y, a continuación, haga clic en Aceptar.
1. Haga clic en Guardar todo.

### Crear el cuadro de diálogo Editar geográfico {#create-the-geoloc-edit-dialog}

El componente de almacén de contexto requiere un cuadro de diálogo de edición. El cuadro de diálogo de edición de geolocalización contendrá un mensaje estático que indica que no hay propiedades para configurar.

1. Haga clic con el botón derecho en el nodo `/libs/cq/personalization/components/contextstores/genericstoreproperties/dialog` y haga clic en Copiar.
1. Haga clic con el botón derecho en el nodo `/apps/myapp/contextstores/geoloc` y haga clic en pegar.
1. Elimine todos los nodos secundarios debajo del nodo /apps/myapp/contextstore/geoloc/dialog/items/items/tab1/items :

   * almacenar
   * propiedades
   * miniatura

1. Haga clic con el botón derecho en el nodo `/apps/myapp/contextstores/geoloc/dialog/items/items/tab1/items` y haga clic en Crear > Crear nodo. Especifique los siguientes valores de propiedad y haga clic en Aceptar:

   * Nombre: static
   * Tipo: cq:Widget

1. Agregue las siguientes propiedades al nodo :

   | Nombre | Tipo | Value |
   |---|---|---|
   | cls | Cadena | x-form-field-set-description |
   | text | Cadena | El componente geográfico no requiere configuración. |
   | xtype | Cadena | static |

1. Haga clic en Guardar todo.

   ![Chlimage_1-5](assets/chlimage_1-5.png)

### Creación del script de inicialización {#create-the-initialization-script}

Agregue un archivo init.js.jsp al componente geográfico y utilícelo para crear el almacén de sesiones, recuperar los datos de ubicación y añadirlos a la tienda.

El archivo init.js.jsp se ejecuta cuando la página carga Client Context. Para este momento, la API de javascript de Client Context se carga y está disponible para el script.

1. Haga clic con el botón derecho en el nodo /apps/myapp/contextstore/geoloc y haga clic en Crear > Crear archivo. Especifique un Nombre de init.js.jsp y haga clic en Aceptar.
1. Agregue el siguiente código a la parte superior de la página y haga clic en Guardar todo.

   ```java
   <%@page contentType="text/javascript;charset=utf-8" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   log.info("***** initializing geolocstore ****");
   String store = "locstore";
   String jsonpurl = "https://api.wipmania.com/jsonp?callback=${callback}";
   
   %>
   var locstore = CQ_Analytics.StoreRegistry.getStore("<%= store %>");
   if(!locstore){
    locstore = CQ_Analytics.JSONPStore.registerNewInstance("<%= store %>", "<%= jsonpurl %>",{});
   }
   <% log.info(" ***** done initializing geoloc ************"); %>
   ```

### Procesar los datos geolocalizados del almacén de sesiones {#render-the-geoloc-session-store-data}

Agregue el código al archivo JSP del componente geográfico para procesar los datos de almacenamiento en Client Context.

![Chlimage_1-6](assets/chlimage_1-6.png)

1. En el CRXDE Lite, abra el archivo `/apps/myapp/contextstores/geoloc/geoloc.jsp` .
1. Agregue el siguiente código HTML debajo del código auxiliar:

   ```xml
   <%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
   <div class="cq-cc-store">
      <div class="cq-cc-content">
          <div class="cq-cc-store-property cq-cc-store-property-level0">
              Continent: <personalization:storePropertyTag propertyName="address/continent" store="locstore"/>
          </div>
          <div class="cq-cc-store-property cq-cc-store-property-level1">
              Country: <personalization:storePropertyTag propertyName="address/country" store="locstore"/>
          </div>
          <div class="cq-cc-store-property cq-cc-store-property-level2">
              City: <personalization:storePropertyTag propertyName="address/city" store="locstore"/>
          </div>
          <div class="cq-cc-store-property cq-cc-store-property-level3">
              Latitude: <personalization:storePropertyTag propertyName="latitude" store="locstore"/>
          </div>
          <div class="cq-cc-store-property cq-cc-store-property-level4">
              Longitude: <personalization:storePropertyTag propertyName="longitude" store="locstore"/>
          </div>
      </div>
       <div class="cq-cc-clear"></div>
   </div>
   ```

1. Haga clic en Guardar todo.

### Añadir el componente a Client Context {#add-the-component-to-client-context}

Agregue el componente Almacén de ubicación a Client Context para que se inicialice cuando se cargue la página.

1. Abra la página de inicio de Geometrixx Outdoors en la instancia de autor ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html)).
1. Haga clic en Ctrl-Alt-c (ventanas) o control-opción-c (Mac) para abrir Client Context.
1. Haga clic en el icono de edición en la parte superior de Client Context para abrir Client Context Designer.

   ![](do-not-localize/chlimage_1.png)

1. Arrastre el componente Almacén de ubicación a Client Context.

### Consulte la información de ubicación en Client Context {#see-the-location-information-in-client-context}

Abra la página de inicio de Geometrixx Outdoors en modo de edición y, a continuación, abra Client Context para ver los datos del componente Almacén de ubicación.

1. Abra la página en inglés del sitio de Geometrixx Outdoors. ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html))
1. Para abrir Client Context, pulse Ctrl-Alt-c (windows) o control-opción-c (Mac).

## Creación de un contexto de cliente personalizado {#creating-a-customized-client-context}

Para crear un segundo contexto de cliente, debe duplicar la rama:

`/etc/clientcontext/default`

* La subcarpeta:
   `/content`
contiene el contenido del contexto de cliente personalizado.

* La carpeta :
   `/contextstores`
permite definir diferentes configuraciones para las tiendas de contexto.

Para utilizar el contexto de cliente personalizado, edite la propiedad
`path`
en el estilo de diseño del componente ClientContext, tal como se incluye en la plantilla de página. Por ejemplo, como la ubicación estándar de:
`/libs/cq/personalization/components/clientcontext/design_dialog/items/path`
