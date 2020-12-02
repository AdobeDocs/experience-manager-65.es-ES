---
title: Contexto de cliente en detalle
seo-title: Contexto de cliente en detalle
description: ClientContext representa una colección de datos de usuario que se ensambla dinámicamente
seo-description: ClientContext representa una colección de datos de usuario que se ensambla dinámicamente
uuid: 95b08fbd-4f50-44a1-80fb-46335fe04a40
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: c881ad66-bcc3-4f99-b77f-0944c23e2d29
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '3023'
ht-degree: 0%

---


# Contexto de cliente en detalle{#client-context-in-detail}

>[!NOTE]
>
>Context del cliente ha sido reemplazado por ContextHub. Consulte la [documentación relacionada](/help/sites-developing/contexthub.md) para obtener más información.

ClientContext representa una colección de datos de usuario que se ensambla dinámicamente. Puede utilizar los datos para determinar el contenido que se mostrará en una página web en una situación determinada (segmentación de contenido). Los datos también están disponibles para el análisis de sitios web y para cualquier JavaScript de la página.

ClientContext consiste principalmente en los siguientes aspectos:

* El almacén de sesiones, que contiene los datos del usuario.
* La interfaz de usuario que muestra los datos del usuario y proporciona herramientas para simular la experiencia del usuario.
* Una [API de javascript](/help/sites-developing/ccjsapi.md) para interactuar con almacenes de sesiones.

Para crear un almacén de sesiones independiente y agregarlo a ClientContext, o crear un almacén de sesiones vinculado a un componente de Context Store. AEM instala varios componentes de Context Store que puede utilizar de inmediato. Puede utilizar estos componentes como base para sus componentes.

Para obtener información sobre cómo abrir Client Context, configurar la información que muestra y simular la experiencia del usuario, consulte [Client Context](/help/sites-administering/client-context.md).

## Almacenes de sesiones {#session-stores}

Client Context incluye varios almacenes de sesiones que contienen datos de usuario. Los datos del almacén provienen de las siguientes fuentes:

* El navegador web del cliente.
* El servidor (consulte [Almacenamiento JSONP](/help/sites-administering/client-context.md#main-pars-variable-8) para almacenar información de orígenes de terceros)

Client Context framework proporciona una [API de javascript](/help/sites-developing/ccjsapi.md) que puede utilizar para interactuar con almacenes de sesiones a fin de leer y escribir datos de usuarios, y escuchar y reaccionar ante eventos de almacenamiento. También puede crear almacenes de sesiones para los datos de usuario que utilice para la segmentación de contenido u otros fines.

Los datos del almacén de sesiones permanecen en el cliente. Client Context no devuelve datos al servidor. Para enviar datos al servidor, utilice un formulario o desarrolle JavaScript personalizado.

Cada almacén de sesiones es una colección de pares propiedad-valor. El almacén de sesiones representa una colección de datos (de cualquier tipo), cuyo significado conceptual puede ser decidido por el diseñador y/o el desarrollador. El siguiente ejemplo de código javascript define un objeto que representa los datos de perfil que puede contener el almacén de sesiones:

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

Un almacén de sesiones puede persistir en todas las sesiones del explorador o solo puede durar en la sesión del explorador en la que se ha creado.

>[!NOTE]
>
>La persistencia de la tienda utiliza almacenamientos del explorador o cookies (la cookie `SessionPersistence`). El almacenamiento del explorador es más común.
>
>Cuando se cierra y vuelve a abrir el explorador, se puede cargar un almacén de sesiones con los valores de un almacén persistente. A continuación, es necesario borrar la caché del explorador para eliminar los valores antiguos.

### Componentes del almacén de contexto {#context-store-components}

Un componente de almacén de contexto es un componente de CQ que se puede agregar a ClientContext. Normalmente, los componentes del almacén de contexto muestran datos de un almacén de sesiones con el que están asociados. Sin embargo, la información que muestran los componentes del almacén de contexto no se limita a los datos del almacén de sesiones.

Los componentes del almacén de contexto pueden incluir los siguientes elementos:

* Secuencias de comandos JSP que definen el aspecto en Client Context.
* Propiedades para mostrar el componente en la barra de tareas.
* Editar cuadros de diálogo para configurar instancias de componentes.
* Javascript que inicializa el almacén de sesiones.

Para obtener una descripción de los componentes del almacén de contexto instalados que puede agregar al almacén de contexto, consulte [Componentes de contexto de cliente disponibles](/help/sites-administering/client-context.md#available-client-context-components).

>[!NOTE]
>
>Los datos de página ya no están en el contexto del cliente como componente predeterminado. Si es necesario, puede agregar esto editando el contexto de cliente, agregando el componente **Propiedades genéricas de la tienda** y luego configurándolo para definir el **almacén** como `pagedata`.

### Envío de contenido objetivo {#targeted-content-delivery}

La información de perfil también se utiliza para entregar [contenido de destino](/help/sites-authoring/content-targeting-touch.md).

![clientcontext_](assets/clientcontext_targetedcontentdelivery.png) ![targetedcontentdelivery clientcontext_targetedcontentdelivery detalle](assets/clientcontext_targetedcontentdeliverydetail.png)

## Añadir ClientContext A Una Página {#adding-client-context-to-a-page}

Incluya el componente ClientContext en la sección body de las páginas web para habilitar ClientContext. La ruta del nodo del componente ClientContext es `/libs/cq/personalization/components/clientcontext`. Para incluir el componente, agregue el siguiente código al archivo JSP del componente de página, ubicado justo debajo del elemento `body` de la página:

```java
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

El componente clientcontext hace que la página cargue las bibliotecas de cliente que implementan ClientContext.

* La API de JavaScript de Client Context.
* Entorno de ClientContext que admite almacenes de sesiones, administración de eventos, etc.
* Segmentos definidos.
* Secuencias de comandos init.js que se generan para cada componente del almacén de contexto que se ha agregado a Client Context.
* (Solo para la instancia de autor) La interfaz de usuario del contexto de cliente.

La interfaz de usuario de ClientContext solo está disponible en la instancia de creación.

## Extensión del contexto de cliente {#extending-client-context}

Para ampliar ClientContext, cree un almacén de sesiones y, opcionalmente, muestre los datos del almacén:

* Cree un almacén de sesiones para los datos de usuario que necesita para la segmentación de contenido y el análisis de Web.
* Cree un componente de almacén de contexto para permitir a los administradores configurar el almacén de sesiones asociado y mostrar los datos de almacenamiento en ClientContext para realizar pruebas.

>[!NOTE]
>
>Si tiene (o crea) un servicio `JSONP` que puede proporcionar los datos, simplemente puede utilizar el componente del almacén de contexto `JSONP` y asignarlo al servicio JSONP. Esto administrará el almacén de sesiones.

### Creación de un almacén de sesiones {#creating-a-session-store}

Cree un almacén de sesiones para los datos que necesita agregar y recuperar desde ClientContext. Generalmente, se utiliza el procedimiento siguiente para crear un almacén de sesiones:

1. Cree una carpeta de biblioteca de cliente que tenga un valor de propiedad `categories` de `personalization.stores.kernel`. ClientContext carga automáticamente las bibliotecas de cliente de esta categoría.

1. Configure la carpeta de la biblioteca del cliente para que tenga una dependencia en la carpeta de la biblioteca del cliente `personalization.core.kernel`. La biblioteca de cliente `personalization.core.kernel` proporciona la API de JavaScript de Client Context.

1. Añada el javascript que crea e inicializa el almacén de sesiones.

Si se incluye javascript en la biblioteca de cliente personalization.store.kernel, se crea la tienda cuando se carga el marco de trabajo de ClientContext.

>[!NOTE]
>
>Si va a crear un almacén de sesiones como parte de un componente de almacén de contexto, puede colocar el javascript en el archivo init.js.jsp del componente. En este caso, el almacén de sesiones solo se crea si el componente se agrega a ClientContext.

#### Tipos de almacenes de sesiones {#types-of-session-stores}

Los almacenes de sesiones se crean y están disponibles durante una sesión del explorador o se conservan en el almacenamiento del explorador o en las cookies. La API de JavaScript de ClientContext define varias clases que representan ambos tipos de almacenes de datos:

* ` [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore)`:: Estos objetos solo residen en el DOM de la página. Los datos se crean y se conservan durante la duración de la página.
* ` [CQ_Analytics.PerstistedSessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedsessionstore)`:: Estos objetos residen en el DOM de la página y se conservan en el almacenamiento del explorador o en las cookies. Los datos están disponibles en todas las páginas y en todas las sesiones de usuario.

La API también proporciona extensiones de estas clases especializadas para almacenar datos JSON o JSONP:

* Objetos de solo sesión: [CQ_Analytics.JSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-jsonstore) y [CQ_Analytics.JSONPStore](/help/sites-developing/ccjsapi.md#cq-analytics-jsonpstore).

* Objetos persistentes: [CQ_Analytics.PersistedJSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedjsonstore) y [CQ_Analytics.PersistedJSONPStore](/help/sites-developing/ccjsapi.md#cq-analyics-persistedjsonpstore).

#### Creación del objeto Almacén de sesiones {#creating-the-session-store-object}

El javascript de la carpeta de la biblioteca del cliente crea e inicializa el almacén de sesiones. A continuación, el almacén de sesiones debe registrarse mediante el Administrador de almacenamiento de contexto. En el ejemplo siguiente se crea y registra un objeto [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore).

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

Cree un componente de almacén de contexto para procesar los datos del almacén de sesiones en ClientContext. Una vez creado, puede arrastrar el componente de almacén de contexto a ClientContext para procesar los datos de un almacén de sesiones. Los componentes del almacén de contexto constan de los siguientes elementos:

* Secuencia de comandos JSP para procesar los datos.
* Cuadro de diálogo de edición.
* Un script JSP para inicializar el almacén de sesiones.
* (Opcional) Una carpeta de biblioteca de cliente que crea el almacén de sesiones. No es necesario incluir la carpeta de la biblioteca del cliente si el componente utiliza un almacén de sesiones existente.

#### Ampliación de los componentes proporcionados del almacén de contexto {#extending-the-provided-context-store-components}

AEM proporciona los componentes de almacén de contexto de genericstore y genericstoreproperties que puede ampliar. La estructura de los datos del almacén determina el componente que se extiende:

* Par propiedad-valor: Extienda el componente `GenericStoreProperties`. Este componente procesa automáticamente los almacenes de pares propiedad-valor. Se suministran varios puntos de interacción:

   * `prolog.jsp` y  `epilog.jsp`: interacción de componentes que le permite agregar lógica del lado del servidor antes o después del procesamiento de componentes.

* Datos complejos: Extienda el componente `GenericStore`. El almacén de sesiones necesitará entonces un método de &quot;procesador&quot; al que se llamará cada vez que se deba procesar el componente. Se llama a la función de procesador con dos parámetros:

   * `@param {String} store`
El almacén que se va a procesar

   * `@param {String} divId`
Id. del div en el que se debe representar el almacén.

>[!NOTE]
>
>Todos los componentes de ClientContext son extensiones de los componentes Generic Store o Generic Store Properties. Hay varios ejemplos instalados en la carpeta `/libs/cq/personalization/components/contextstores`.

#### Configuración del aspecto en la barra de tareas {#configuring-the-appearance-in-sidekick}

Al editar ClientContext, los componentes del almacén de contexto aparecen en la barra de tareas. Al igual que con todos los componentes, las propiedades `componentGroup` y `jcr:title` del componente de contexto de cliente determinan el grupo y el nombre del componente.

Todos los componentes que tienen un valor de propiedad `componentGroup` de `Client Context` aparecen en la barra de tareas de forma predeterminada. Si utiliza un valor diferente para la propiedad `componentGroup`, debe agregar manualmente el componente a la barra de tareas mediante el modo Diseño.

#### Instancias de componentes del almacén de contexto {#context-store-component-instances}

Al agregar un componente de almacén de contexto a Client Context, se crea un nodo que representa la instancia de componente debajo de `/etc/clientcontext/default/content/jcr:content/stores`. Este nodo contiene los valores de propiedad que se configuran mediante el cuadro de diálogo de edición del componente.

Cuando se inicializa ClientContext, estos nodos se procesan.

#### Inicialización del almacén de sesiones asociado {#initializing-the-associated-session-store}

Añada un archivo init.js.jsp a su componente para generar código javascript que inicialice el almacén de sesiones que utiliza el componente del almacén de contexto. Por ejemplo, utilice la secuencia de comandos de inicialización para recuperar las propiedades de configuración del componente y usarlas para rellenar el almacén de sesiones.

El javascript que se genera se agrega a la página cuando Client Context se inicializa al cargarse la página en las instancias de autor y publicación. Este JSP se ejecuta antes de que se cargue y procese la instancia del componente del almacén de contexto.

El código debe establecer el tipo MIME del archivo en `text/javascript` o no se ejecuta.

>[!CAUTION]
>
>La secuencia de comandos init.js.jsp se ejecuta en la instancia de creación y publicación, pero solo si el componente del almacén de contexto se agrega a ClientContext.

El siguiente procedimiento crea el archivo de secuencias de comandos init.js.jsp y agrega el código que establece el tipo de MIME correcto. El código que realiza la inicialización de la tienda sería el siguiente.

1. Haga clic con el botón secundario en el nodo del componente del almacén de contexto y, a continuación, haga clic en Crear > Crear archivo.
1. En el campo Nombre, escriba `init.js.jsp` y haga clic en Aceptar.
1. En la parte superior de la página, agregue el siguiente código y haga clic en Guardar todo.

   ```java
   <%@page contentType="text/javascript" %>
   ```

### Representación de datos del almacén de sesiones para componentes genericstoreproperties {#rendering-session-store-data-for-genericstoreproperties-components}

Muestre los datos del almacén de sesiones en ClientContext con un formato coherente.

#### Visualización de datos de propiedad {#displaying-property-data}

La biblioteca de etiquetas de personalización proporciona la etiqueta `personalization:storePropertyTag` que muestra el valor de una propiedad de un almacén de sesiones. Para utilizar la etiqueta, incluya la siguiente línea de código en el archivo JSP:

```xml
<%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
```

La etiqueta tiene el siguiente formato:

```xml
<personalization:storePropertyTag propertyName="property_name" store="session_store_name"/>
```

El atributo `propertyName` es el nombre de la propiedad store que se va a mostrar. El atributo `store` es el nombre del almacén registrado. La etiqueta de ejemplo siguiente muestra el valor de la propiedad `authorizableId` del almacén `profile`:

```xml
<personalization:storePropertyTag propertyName="authorizableId" store="profile"/>
```

#### Estructura HTML {#html-structure}

La carpeta de la biblioteca del cliente personalization.ui (/etc/clientlibs/foundation/personalization/ui/temáticas/default) proporciona los estilos CSS que ClientContext utiliza para dar formato al código HTML. El siguiente código ilustra la estructura sugerida para mostrar los datos del almacén:

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

El componente `/libs/cq/personalization/components/contextstores/profiledata` del almacén de contexto utiliza esta estructura para mostrar datos del almacén de sesiones de perfil. La clase `cq-cc-thumbnail` coloca la imagen en miniatura. Las clases `cq-cc-store-property-level*x*` dan formato a los datos alfanuméricos:

* level0, level1 y level2 se distribuyen verticalmente y utilizan una fuente blanca.
* level3, y cualquier nivel adicional, se distribuyen horizontalmente y utilizan una fuente blanca con un fondo más oscuro.

![climage_1-4](assets/chlimage_1-4.png)

### Representación de datos del almacén de sesiones para componentes del almacén de datos genéricos {#rendering-session-store-data-for-genericstore-components}

Para procesar los datos del almacén mediante un componente de almacén genérico, debe:

* Añada la etiqueta personalization:storeRendererTag al script JSP del componente para identificar el nombre del almacén de sesiones.
* Implemente un método de procesamiento en la clase de almacén de sesiones.

#### Identificación del almacén de sesiones de genericstore {#identifying-the-genericstore-session-store}

La biblioteca de etiquetas de personalización proporciona la etiqueta `personalization:storePropertyTag` que muestra el valor de una propiedad de un almacén de sesiones. Para utilizar la etiqueta, incluya la siguiente línea de código en el archivo JSP:

```xml
<%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
```

La etiqueta tiene el siguiente formato:

```java
<personalization:storeRendererTag store="store_name"/>
```

#### Implementación del método de procesamiento del almacén de sesiones {#implementing-the-session-store-renderer-method}

El almacén de sesiones necesitará entonces un método de &quot;procesador&quot; al que se llamará cada vez que se deba procesar el componente. Se llama a la función de procesador con dos parámetros:

* @param {String} tienda
El almacén que se va a procesar
* @param {String} divId
Id. del div en el que se debe representar el almacén.

## Interactuar con almacenes de sesiones {#interacting-with-session-stores}

Utilice javascript para interactuar con los almacenes de sesiones.

### Acceso a los almacenes de sesiones {#accessing-session-stores}

Obtenga un objeto de almacén de sesiones para leer o escribir datos en el almacén. [CQ_Analytics.](/help/sites-developing/ccjsapi.md#cq-analytics-clientcontextmgr) ClientContextMgrproporciona acceso a las tiendas en función del nombre de la tienda. Una vez obtenidos, utilice los métodos de [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) o [CQ_Analytics.PersistedSessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedsessionstore) para interactuar con los datos del almacén.

El ejemplo siguiente obtiene el almacén `profile` y, a continuación, recupera la propiedad `formattedName` del almacén.

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

### Creación de un detector para reaccionar ante una actualización del almacén de sesiones {#creating-a-listener-to-react-to-a-session-store-update}

La sesión almacena eventos de activación, de modo que es posible agregar oyentes y activar eventos en función de estos eventos.

Los almacenes de sesiones se crean según el patrón `Observable`. Se extienden [ `CQ_Analytics.Observable`](/help/sites-developing/ccjsapi.md#cq-analytics-observable) que proporciona el método ` [addListener](/help/sites-developing/ccjsapi.md#addlistener-event-fct-scope)`.

En el ejemplo siguiente se agrega un detector al evento `update` del almacén de sesiones `profile`.

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

### Comprobando que un almacén de sesiones está definido e inicializado {#checking-that-a-session-store-is-defined-and-initialized}

Los almacenes de sesiones no estarán disponibles hasta que se carguen e inicialicen con datos. Los siguientes factores pueden afectar a la temporización de la disponibilidad del almacén de sesiones:

* Carga de página
* Carga de JavaScript
* Tiempo de ejecución de JavaScript
* Tiempos de respuesta para solicitudes XHR
* Cambios dinámicos en el almacén de sesiones

Utilice los métodos [CQ_Analytics.ClientContextUtils](/help/sites-developing/ccjsapi.md#cq-analytics-clientcontextutils) del objeto [onStoreRegistered](/help/sites-developing/ccjsapi.md#onstoreregistered-storename-callback) y [onStoreInitialized](/help/sites-developing/ccjsapi.md#onstoreinitialized-storename-callback-delay) para acceder a los almacenes de sesiones solo cuando estén disponibles. Estos métodos le permiten registrar oyentes de evento que reaccionan a los eventos de registro e inicialización de la sesión.

>[!CAUTION]
>
>Si dependes de otra tienda, debes atender el caso de cuando la tienda nunca se registre.

El ejemplo siguiente utiliza el evento `onStoreRegistered` del almacén de sesiones `profile`. Cuando se registra el almacén, se agrega un detector al evento `update` del almacén de sesiones. Cuando se actualiza la tienda, el contenido del elemento `<div class="welcome">` de la página se actualiza con el nombre del almacén `profile`.

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

Para evitar que una propiedad de `PersistedSessionStore` permanezca (es decir, excluirla de la cookie `sessionpersistence`), agregue la propiedad a la lista de propiedad no persistente del almacén de sesiones persistente.

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

La página actual debe tener una página móvil correspondiente; esto se determina solamente si la página tiene un LiveCopy configurado con una configuración de implementación móvil ( `rolloutconfig.path.toLowerCase` contiene `mobile`).

#### Configuración {#configuration}

Al cambiar de la página de escritorio a su equivalente móvil:

* Se carga el DOM de la página móvil.
* El `div` principal (requerido) que contiene el contenido, se extrae e e inserta en la página de escritorio actual.

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

## Ejemplo: Creación de un componente personalizado del almacén de contexto {#example-creating-a-custom-context-store-component}

En este ejemplo, se crea un componente de almacén de contexto que recupera datos de un servicio externo y lo almacena en el almacén de sesiones:

* Extiende el componente genericstoreproperties.
* Inicializa una tienda con un objeto CQ_Analytics.JSONPStore javascript.
* Llama a un servicio JSONP para recuperar datos y agregarlos a la tienda.
* Procesa los datos en ClientContext.

### Añadir el componente geográfico {#add-the-geoloc-component}

Cree una aplicación de CQ y agregue el componente de geolocalización.

1. Abra el CRXDE Lite en el navegador web ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Haga clic con el botón secundario en la carpeta `/apps` y haga clic en Crear > Crear carpeta. Especifique un nombre para `myapp` y haga clic en Aceptar.
1. Del mismo modo, debajo de `myapp`, cree una carpeta con el nombre `contextstores`. &quot;
1. Haga clic con el botón secundario en la carpeta `/apps/myapp/contextstores` y haga clic en Crear > Crear componente. Especifique los siguientes valores de propiedad y haga clic en Siguiente:

   * Etiqueta: geoloc
   * Título: Almacén de ubicaciones
   * Super Tipo: cq/personalization/components/contextstore/genericstoreproperties
   * Grupo: ClientContext

1. En el cuadro de diálogo Crear componente, haga clic en Siguiente en cada página hasta que se active el botón Aceptar y, a continuación, haga clic en Aceptar.
1. Haga clic en Guardar todo.

### Crear el cuadro de diálogo Editar geográfico {#create-the-geoloc-edit-dialog}

El componente del almacén de contexto requiere un cuadro de diálogo de edición. El cuadro de diálogo de edición de geolocalización contendrá un mensaje estático que indica que no hay propiedades que configurar.

1. Haga clic con el botón derecho en el nodo `/libs/cq/personalization/components/contextstores/genericstoreproperties/dialog` y haga clic en Copiar.
1. Haga clic con el botón secundario en el nodo `/apps/myapp/contextstores/geoloc` y haga clic en Pegar.
1. Elimine todos los nodos secundarios situados debajo del nodo /apps/myapp/contextstore/geoloc/dialog/items/items/tab1/items:

   * store
   * propiedades
   * thumbnail

1. Haga clic con el botón secundario en el nodo `/apps/myapp/contextstores/geoloc/dialog/items/items/tab1/items` y haga clic en Crear > Crear nodo. Especifique los siguientes valores de propiedad y haga clic en Aceptar:

   * Nombre: static
   * Tipo: cq:Widget

1. Añada las siguientes propiedades en el nodo:

   | Nombre | Tipo | Value |
   |---|---|---|
   | cls | Cadena | x-form-field-set-description |
   | text | Cadena | El componente de geolocalización no requiere configuración. |
   | xtype | Cadena | static |

1. Haga clic en Guardar todo.

   ![climage_1-5](assets/chlimage_1-5.png)

### Crear la secuencia de comandos de inicialización {#create-the-initialization-script}

Añada un archivo init.js.jsp al componente geolocalizado y úselo para crear el almacén de sesiones, recuperar los datos de ubicación y agregarlo a la tienda.

El archivo init.js.jsp se ejecuta cuando la página carga Client Context. En este momento, la API de javascript de ClientContext está cargada y disponible para su script.

1. Haga clic con el botón derecho en el nodo /apps/myapp/contextstore/geoloc y, a continuación, haga clic en Crear > Crear archivo. Especifique un nombre para init.js.jsp y haga clic en Aceptar.
1. Añada el siguiente código a la parte superior de la página y haga clic en Guardar todo.

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

### Representar los datos geolocalizados del almacén de sesiones {#render-the-geoloc-session-store-data}

Añada el código en el archivo JSP del componente geolocalizado para procesar los datos del almacén en Client Context.

![climage_1-6](assets/chlimage_1-6.png)

1. En CRXDE Lite, abra el archivo `/apps/myapp/contextstores/geoloc/geoloc.jsp`.
1. Añada el siguiente código HTML debajo del código auxiliar:

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

### Añadir el componente a ClientContext {#add-the-component-to-client-context}

Añada el componente Almacén de ubicaciones a ClientContext para que se inicialice al cargarse la página.

1. Abra la página de inicio Geometrixx Outdoors en la instancia de creación ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html)).
1. Haga clic en Ctrl-Alt-c (ventanas) o control-opción-c (Mac) para abrir Client Context.
1. Haga clic en el icono Editar en la parte superior de Client Context para abrir ClientContext Designer.

   ![](do-not-localize/chlimage_1.png)

1. Arrastre el componente Almacén de ubicaciones a ClientContext.

### Consulte la información de ubicación en el contexto de cliente {#see-the-location-information-in-client-context}

Abra la página de inicio Geometrixx Outdoors en modo de edición y, a continuación, abra Client Context para ver los datos del componente Almacén de ubicaciones.

1. Abra la página en inglés del sitio de Geometrixx Outdoors. ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html))
1. Para abrir Client Context, pulse Ctrl-Alt-c (windows) o control-opción-c (Mac).

## Creación de un contexto de cliente personalizado {#creating-a-customized-client-context}

Para crear un segundo contexto de cliente, debe realizar el duplicado de la rama:

`/etc/clientcontext/default`

* La subcarpeta:
   `/content`
contendrá el contenido del contexto de cliente personalizado.

* La carpeta:
   `/contextstores`
permite definir diferentes configuraciones para los almacenes de contexto.

Para utilizar el contexto de cliente personalizado, edite la propiedad
`path`
en el estilo de diseño del componente de contexto de cliente, tal como se incluye en la plantilla de página. Por ejemplo, como ubicación estándar de:
`/libs/cq/personalization/components/clientcontext/design_dialog/items/path`
