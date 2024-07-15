---
title: Diseño interactivo para páginas web
description: Con un diseño interactivo, las mismas páginas se pueden mostrar de forma eficaz en varios dispositivos y en varias orientaciones.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
legacypath: /content/docs/en/aem/6-0/develop/mobile/responsive
exl-id: c705710b-a94a-4f4f-affa-ddd4fc6cb0ec
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '5293'
ht-degree: 0%

---

# Diseño interactivo para páginas web{#responsive-design-for-web-pages}

>[!NOTE]
>
>El Adobe SPA recomienda usar el Editor de para proyectos que requieran procesamiento del lado del cliente basado en el marco de trabajo de aplicación de una sola página (como _React_). [Más información](/help/sites-developing/spa-overview.md).
>

>[!NOTE]
>
>Varios ejemplos se basan en el contenido de muestra de Geometrixx AEM, que ya no se envía con (Adobe Experience Manager) y que se ha sustituido por We.Retail. Consulte el documento [Implementación de referencia de We.Retail](/help/sites-developing/we-retail.md#we-retail-geometrixx) para obtener información sobre cómo descargar e instalar Geometrixx.

Diseñar las páginas web para que se adapten a la ventanilla del cliente en la que se muestran. Con un diseño interactivo, las mismas páginas se pueden mostrar de forma eficaz en varios dispositivos en ambas orientaciones. La siguiente imagen muestra algunas formas en que una página puede responder a los cambios en el tamaño de la ventanilla móvil:

* Diseño: utilice diseños de una sola columna para las ventanillas más pequeñas y diseños de varias columnas para las ventanillas más grandes.
* Tamaño de texto: utilice un tamaño de texto más grande (cuando corresponda, como encabezados) en las ventanillas móviles más grandes.
* Contenido: incluya solo el contenido más importante al mostrarlo en dispositivos más pequeños.
* Navegación: se proporcionan herramientas específicas del dispositivo para acceder a otras páginas.
* Imágenes: se muestran las representaciones de imágenes apropiadas para la ventanilla del cliente. según las dimensiones de la ventana.

![chlimage_1-4](assets/chlimage_1-4a.png)

Desarrolle aplicaciones de Adobe Experience Manager AEM () que generen páginas de HTML5 adaptadas a varios tamaños y orientaciones de ventana. Por ejemplo, los siguientes intervalos de anchuras de ventanilla móvil se corresponden con varios tipos de dispositivos y orientaciones

* Anchura máxima de 480 píxeles (teléfono, vertical)
* Anchura máxima de 767 píxeles (teléfono, horizontal)
* Anchura entre 768 píxeles y 979 píxeles (tableta, vertical)
* Anchura entre 980 píxeles y 1199 píxeles (tableta, horizontal)
* Anchura de 1200 píxeles o superior (escritorio)

Consulte los siguientes temas para obtener información sobre la implementación del comportamiento de diseño interactivo:

* [Consultas de medios](/help/sites-developing/responsive.md#using-media-queries)
* [Rejillas fluidas](/help/sites-developing/responsive.md#developing-a-fluid-grid)
* [Imágenes adaptables](/help/sites-developing/responsive.md#using-adaptive-images)

A medida que diseñe, use **[!UICONTROL Sidekick]** para obtener una vista previa de las páginas para diferentes tamaños de pantalla.

## Antes de que desarrolle {#before-you-develop}

AEM Antes de desarrollar la aplicación que admite sus páginas web, se deben tomar varias decisiones de diseño. Por ejemplo, debe tener la siguiente información:

* Los dispositivos a los que está dirigiendo.
* Tamaños de las ventanillas móviles de destino.
* Diseños de página para cada uno de los tamaños de ventanilla móvil de destino.

### Estructura de aplicación {#application-structure}

AEM La estructura típica de la aplicación de la comunidad admite todas las implementaciones de diseño interactivo:

* Los componentes de página residen debajo de /apps/*application_name*/components
* Las plantillas se encuentran debajo de /apps/*nombre_aplicación*/templates
* Los diseños se encuentran debajo de /etc/designs

## Uso de consultas de medios {#using-media-queries}

Las consultas de medios permiten el uso selectivo de estilos CSS para el procesamiento de páginas. AEM Las herramientas y características de desarrollo de la le permiten implementar de forma eficaz y eficiente las consultas de medios en sus aplicaciones.

El grupo W3C proporciona la recomendación [Consultas de medios](https://www.w3.org/TR/mediaqueries-3/) que describe esta característica CSS3 y la sintaxis.

### Creación del archivo CSS {#creating-the-css-file}

En el archivo CSS, defina consultas de medios basadas en las propiedades de los dispositivos a los que está dirigiendo. La siguiente estrategia de implementación es eficaz para administrar estilos para cada consulta de medios:

* Utilice una ClientLibraryFolder para definir el archivo CSS que se ensambla cuando se representa la página.
* Defina cada consulta de medios y los estilos asociados en archivos CSS independientes. Es útil utilizar nombres de archivo que representen las características del dispositivo de la consulta de medios.
* Defina estilos que sean comunes a todos los dispositivos en un archivo CSS independiente.
* En el archivo css.txt de ClientLibraryFolder, ordene los archivos CSS de lista según sea necesario en el archivo CSS ensamblado.

La muestra multimedia `We.Retail` usa esta estrategia para definir estilos en el diseño del sitio. El archivo CSS usado por `We.Retail` se encuentra en `*/apps/weretail/clientlibs/clientlib-site/less/grid.less`.

La siguiente tabla enumera los archivos de la carpeta secundaria css.

<table>
 <tbody>
  <tr>
   <th>Nombre de archivo</th>
   <th>Descripción</th>
   <th>Consulta de medios</th>
  </tr>
  <tr>
   <td>style.css</td>
   <td>Estilos comunes.</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>bootstrap.css</td>
   <td>Estilos comunes, definidos por el Bootstrap de Twitter.</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>responsive-1200px.css</td>
   <td>Estilos para todos los medios que tengan 1200 píxeles de ancho o más.</td>
   <td><p>@media (ancho mínimo: 1200 px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-980px-1199px.css</td>
   <td>Estilos de medios que tienen entre 980 y 1199 píxeles de ancho.</td>
   <td><p>@media (ancho mínimo: 980 px) y (ancho máximo: 1199 px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-768px-979px.css</td>
   <td>Estilos de medios que tienen entre 768 y 979 píxeles de ancho. </td>
   <td><p>@media (ancho mínimo: 768 px) y (ancho máximo: 979 px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-767px-max.css</td>
   <td>Estilos para todos los medios con menos de 768 píxeles de ancho.</td>
   <td><p>@media (ancho máximo: 767 px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-480px.css</td>
   <td>Estilos para todos los medios con menos de 481 píxeles de ancho.</td>
   <td>@media (ancho máximo: 480 px) {<br /> ...<br /> }</td>
  </tr>
 </tbody>
</table>

El archivo css.txt de la carpeta `/etc/designs/weretail/clientlibs` enumera los archivos CSS que incluye la carpeta de biblioteca de cliente. El orden de los archivos implementa la prioridad de estilo. Los estilos son más específicos a medida que disminuye el tamaño del dispositivo.

`#base=css`

```
style.css
 bootstrap.css
```

```
responsive-1200px.css
 responsive-980px-1199px.css
 responsive-768px-979px.css
 responsive-767px-max.css
 responsive-480px.css
```

**Sugerencia**: Los nombres de archivo descriptivos le permiten identificar fácilmente el tamaño de la ventanilla móvil de destino.

### AEM Uso de consultas de medios con páginas de {#using-media-queries-with-aem-pages}

Incluya la carpeta de la biblioteca de cliente en el script JSP del componente de página. Al hacerlo, se ayuda a generar el archivo CSS que incluye las consultas de medios y hace referencia al archivo.

```xml
<ui:includeClientLib categories="apps.weretail.all"/>
```

>[!NOTE]
>
>La carpeta de biblioteca de cliente `apps.weretail.all` incrusta la biblioteca clientlibs.

El script JSP genera el siguiente código de HTML que hace referencia a las hojas de estilo:

```xml
<link rel="stylesheet" href="/etc/designs/weretail/clientlibs-all.css" type="text/css">
<link href="/etc/designs/weretail.css" rel="stylesheet" type="text/css">
```

## Vista previa para dispositivos específicos {#previewing-for-specific-devices}

Vea vistas previas de las páginas en diferentes tamaños de ventanilla móvil para poder probar el comportamiento del diseño interactivo. En el modo **[!UICONTROL Vista previa]**, **[!UICONTROL Sidekick]** incluye un menú desplegable de **[!UICONTROL Dispositivos]** que se usa para seleccionar un dispositivo. Al seleccionar un dispositivo, la página cambia para adaptarse al tamaño de la ventanilla móvil.

![chlimage_1-5](assets/chlimage_1-5a.png)

Para habilitar la vista previa del dispositivo en **[!UICONTROL Sidekick]**, debe configurar la página y el servicio **[!UICONTROL MobileEmulatorProvider]**. Otra configuración de página controla la lista de dispositivos que aparece en la lista **[!UICONTROL Dispositivos]**.

### Agregar la lista de dispositivos {#adding-the-devices-list}

La lista **[!UICONTROL Dispositivos]** aparece en **[!UICONTROL Sidekick]** cuando su página incluye el script JSP que procesa la lista **[!UICONTROL Dispositivos]**. Para agregar la lista **[!UICONTROL Dispositivos]** al **[!UICONTROL Sidekick]**, incluya el script `/libs/wcm/mobile/components/simulator/simulator.jsp` en la sección `head` de su página.

Incluya el siguiente código en el JSP que define la sección `head`:

`<cq:include script="/libs/wcm/mobile/components/simulator/simulator.jsp"/>`

Para ver un ejemplo, abra el archivo `/apps/weretail/components/page/head.jsp` en el CRXDE Lite.

### Registro de componentes de página para simulación {#registering-page-components-for-simulation}

Para habilitar el simulador de dispositivos para que admita las páginas, registre los componentes de página con el servicio de fábrica de MobileEmulatorProvider y defina la propiedad `mobile.resourceTypes`.

AEM Al trabajar con los servicios, existen varios métodos para administrar las opciones de configuración de dichos servicios; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obtener información detallada.

Por ejemplo, para crear un nodo ` [sling:OsgiConfig](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)` en su aplicación:

* Carpeta principal: `/apps/application_name/config`
* Nombre: `com.day.cq.wcm.mobile.core.impl.MobileEmulatorProvider-*alias*`

  El sufijo - `*alias*` es necesario porque el servicio MobileEmulatorProvider es un servicio de fábrica. Utilice cualquier alias que sea único para esta fábrica.

* `jcr:primaryType`: `sling:OsgiConfig`

Agregue la siguiente propiedad de nodo:

* Nombre: `mobile.resourceTypes`
* Tipo: `String[]`
* Valor: Las rutas a los componentes de página que procesan las páginas web. Por ejemplo, la aplicación geometrixx-media utiliza los siguientes valores:

  ```
  geometrixx-media/components/page
   geometrixx-unlimited/components/pages/page
   geometrixx-unlimited/components/pages/coverpage
   geometrixx-unlimited/components/pages/issue
  ```

### Especificar los grupos de dispositivos {#specifying-the-device-groups}

Para especificar los grupos de dispositivos que aparecen en la lista Dispositivos, agregue una propiedad `cq:deviceGroups` al nodo `jcr:content` de la página raíz del sitio. El valor de la propiedad es una matriz de rutas a los nodos del grupo de dispositivos.

Los nodos del grupo de dispositivos se encuentran en la carpeta `/etc/mobile/groups`.

Por ejemplo, la página raíz del sitio de Geometrixx Medias es `/content/geometrixx-media`. El nodo `/content/geometrixx-media/jcr:content` incluye la siguiente propiedad:

* Nombre: `cq:deviceGroups`
* Tipo: `String[]`
* Valor: `/etc/mobile/groups/responsive`

Use la consola Herramientas para [crear y editar grupos de dispositivos](/help/sites-developing/groupfilters.md).

>[!NOTE]
>
>Para los grupos de dispositivos que utiliza para el diseño interactivo, edite el grupo de dispositivos y, en la pestaña General, seleccione Deshabilitar emulador. Esta opción evita que aparezca el carrusel del emulador, lo que no es relevante para el diseño interactivo.
>

## Uso de imágenes adaptables {#using-adaptive-images}

Puede utilizar consultas de medios para seleccionar un recurso de imagen para mostrarlo en la página. Sin embargo, todos los recursos que utilizan una consulta de medios para condicionar su uso se descargan en el cliente. La consulta de medios simplemente determina si se muestra el recurso descargado.

Para recursos de gran tamaño, como imágenes, la descarga de todos los recursos no es un uso eficaz de la canalización de datos del cliente. Para descargar recursos de forma selectiva, utilice JavaScript para iniciar la solicitud de recursos después de que las consultas de medios realicen la selección.

La siguiente estrategia carga un único recurso que se elige mediante consultas de medios:

1. Agregue un elemento DIV para cada versión del recurso. Incluya el URI del recurso como el valor de un valor de atributo. El explorador no interpreta el atributo como un recurso.
1. Agregue una consulta multimedia a cada elemento DIV que sea apropiado para el recurso.
1. Cuando se carga el documento o se cambia el tamaño de la ventana, el código JavaScript prueba la consulta de medios de cada elemento DIV.
1. En función de los resultados de las consultas, determine qué recurso incluir.
1. Inserte un elemento HTML en el DOM que haga referencia al recurso.

### Evaluación de consultas de medios mediante JavaScript {#evaluating-media-queries-using-javascript}

Las implementaciones de la [interfaz MediaQueryList](https://drafts.csswg.org/cssom-view/#the-mediaquerylist-interface) que define el W3C le permiten evaluar consultas de medios mediante JavaScript. Puede aplicar lógica a los resultados de la consulta de medios y ejecutar scripts dirigidos a la ventana actual:

* Los exploradores que implementan la interfaz MediaQueryList admiten la función `window.matchMedia()`. Esta función prueba las consultas de medios con una cadena determinada. La función devuelve un objeto `MediaQueryList` que proporciona acceso a los resultados de la consulta.

* En el caso de los exploradores que no implementan la interfaz, puede usar un relleno de directiva `matchMedia()`, como [matchMedia.js](https://github.com/paulirish/matchMedia.js), una biblioteca de JavaScript disponible libremente.

#### Selección de recursos específicos de medios {#selecting-media-specific-resources}

El [elemento de imagen](https://html.spec.whatwg.org/multipage/embedded-content.html#the-picture-element) del W3C usa consultas de medios para determinar el origen que se va a usar para los elementos de imagen. El elemento de imagen utiliza atributos de elemento para asociar consultas de medios con rutas de imagen.

La biblioteca [picturefill.js](https://github.com/scottjehl/picturefill) disponible de forma gratuita proporciona una funcionalidad similar a la del elemento `picture` propuesto y usa una estrategia similar. La biblioteca picturefill.js llama a `window.matchMedia` para evaluar las consultas de medios definidas para un conjunto de elementos `div`. Cada elemento `div` también especifica un origen de imagen. El origen se usa cuando la consulta multimedia del elemento `div` devuelve `true`.

La biblioteca `picturefill.js` requiere código de HTML similar al siguiente ejemplo:

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
</div>
```

Cuando se representa la página, picturefull.js inserta un elemento `img` como el último elemento secundario del elemento `<div data-picture>`:

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
    <img src="path to medium image">
</div>
```

AEM En una página de, el valor del atributo `data-src` es la ruta a un recurso del repositorio.

### AEM Implementar imágenes adaptables en el {#implementing-adaptive-images-in-aem}

AEM Para implementar imágenes adaptables en la aplicación de, debe agregar las bibliotecas de JavaScript necesarias e incluir el marcado de HTML necesario en las páginas.

**Bibliotecas**

Obtenga las siguientes bibliotecas de JavaScript e inclúyalas en una carpeta de biblioteca de cliente:

* [matchMedia.js](https://github.com/paulirish/matchMedia.js) (para exploradores que no implementan la interfaz MediaQueryList)
* [picturefill.js](https://github.com/scottjehl/picturefill)
* jquery.js (disponible a través de la carpeta de biblioteca de cliente `/etc/clientlibs/granite/jquery` (category = jquery)
* [jquery.debouncedresize.js](https://github.com/louisremi/jquery-smartresize) (un evento jquery que se produce una vez que se cambia el tamaño de la ventana)

**Sugerencia:** Puede concatenar automáticamente varias carpetas de biblioteca de cliente incrustando [3}.](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries)

**HTML**

Cree un componente que genere los elementos div necesarios que espera el código picturefill.js. AEM En una página de, el valor del atributo data-src es la ruta a un recurso del repositorio. Por ejemplo, un componente de página puede codificar de forma rígida las consultas de medios y las rutas asociadas para representaciones de imágenes en DAM. O bien, cree un componente de imagen personalizado que permita a los autores seleccionar representaciones de imágenes o especificar opciones de representación en tiempo de ejecución.

El siguiente HTML de ejemplo selecciona entre dos representaciones DAM de la misma imagen.

```xml
<div data-picture>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png'></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.319.319.png'    data-media="(min-width: 769px)"></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.140.100.png'   data-media="(min-width: 481px)"></div>
</div>
```

>[!NOTE]
>
>El componente de base Imagen adaptable implementa las imágenes adaptables:
>
>* Carpeta de la biblioteca de cliente: `/libs/foundation/components/adaptiveimage/clientlibs`
>* Script que genera el HTML: `/libs/foundation/components/adaptiveimage/adaptiveimage.jsp`
>
>La sección siguiente proporciona detalles sobre este componente.
>

### AEM Explicación de la renderización de imágenes en la {#understanding-image-rendering-in-aem}

AEM Para personalizar la renderización de imágenes, debe comprender la implementación predeterminada de la renderización de imágenes estáticas de la. AEM proporciona el componente Imagen y un servlet de renderización de imágenes que funcionan juntos para procesar imágenes para páginas web. Las siguientes secuencias de eventos se producen cuando el componente Imagen se incluye en el sistema de párrafos de la página:

1. Creación: los autores editan el componente Imagen para especificar el archivo de imagen que desea incluir en una página de HTML. La ruta del archivo se almacena como un valor de propiedad del nodo del componente Imagen.
1. Solicitud de página: el JSP del componente de página genera el código de HTML. El JSP del componente Imagen genera y añade un elemento img a la página.
1. Solicitud de imagen: El explorador web carga la página y solicita la imagen según el atributo src del elemento img.
1. Image rendering: El servlet de renderización de imágenes devuelve la imagen al explorador web.

![chlimage_1-6](assets/chlimage_1-6a.png)

Por ejemplo, el JSP del componente de imagen genera el siguiente elemento HTML:

`<img title="My Image" alt="My Image" class="cq-dd-image" src="/content/mywebsite/en/_jcr_content/par/image_0.img.jpg/1358372073597.jpg">`

Cuando el explorador carga la página, solicita la imagen utilizando el valor del atributo src como dirección URL. Sling descompone la dirección URL:

* Recurso: `/content/mywebsite/en/_jcr_content/par/image_0`
* Extensión de nombre de archivo: `.jpg`
* Selector: `img`
* Sufijo: `1358372073597.jpg`

El nodo `image_0` tiene un valor `jcr:resourceType` de `foundation/components/image`, que tiene un valor `sling:resourceSuperType` de `foundation/components/parbase`. El componente parbase incluye el script img.GET.java que coincide con el selector y la extensión de nombre de archivo de la dirección URL de la solicitud. CQ utiliza este script (servlet) para procesar la imagen.

Para ver el código fuente del script, use el CRXDE Lite para abrir `/libs/foundation/components/parbase/img.GET.java`
archivo.

## Escala de imágenes para el tamaño de la ventanilla actual {#scaling-images-for-the-current-viewport-size}

Escale imágenes en tiempo de ejecución según las características de la ventanilla del cliente para proporcionar imágenes que se ajusten a los principios del diseño interactivo. Utilice el mismo patrón de diseño que el procesamiento de imágenes estáticas, con un servlet y un componente de creación.

El componente debe realizar las siguientes tareas:

* Almacene la ruta y las dimensiones deseadas del recurso de imagen como valores de propiedad.
* Genere `div` elementos que contengan selectores de medios y llamadas de servicio para procesar la imagen.

>[!NOTE]
>
>El cliente web utiliza las bibliotecas JavaScript matchMedia y Picturefill (o bibliotecas similares) para evaluar los selectores de medios.
>

El servlet que procesa la solicitud de imagen debe realizar las siguientes tareas:

* Recupere la ruta y las dimensiones de la imagen desde las propiedades del componente.
* Escale la imagen según las propiedades y devuelva la imagen.

**Soluciones disponibles**

AEM instala las siguientes implementaciones que puede utilizar o ampliar.

* Componente de base de imagen adaptable que genera consultas de medios y solicitudes HTTP al servlet de componente de imagen adaptable que escala las imágenes.
* El paquete de Geometrixx Commons instala los servlets de muestra del servlet de modificación de referencia de imagen que modifican la resolución de la imagen.

### Explicación del componente Imagen adaptable {#understanding-the-adaptive-image-component}

El componente de imagen adaptable genera llamadas al servlet del componente de imagen adaptable para procesar una imagen cuyo tamaño depende de la pantalla del dispositivo. El componente incluye los siguientes recursos:

* JSP: añade elementos div que asocian consultas de medios con llamadas al servlet de componente de imagen adaptable.
* Bibliotecas de cliente: La carpeta clientlibs es un `cq:ClientLibraryFolder` que ensambla la biblioteca de JavaScript matchMedia polyfill y una biblioteca de JavaScript Picturefill modificada.
* Cuadro de diálogo Editar: el nodo `cq:editConfig` anula el componente de imagen de base de CQ para que el destino de colocación cree un componente de imagen adaptable en lugar de un componente de imagen de base.

#### Adición de los elementos DIV {#adding-the-div-elements}

El script adaptive-image.jsp incluye el siguiente código que genera elementos div y consultas de medios:

```
<div data-picture data-alt='<%= alt %>'>
    <div data-src='<%= path + ".img.320.low." + extension + suffix %>'       data-media="(min-width: 1px)"></div>                                        <%-- Small mobile --%>
    <div data-src='<%= path + ".img.320.medium." + extension + suffix %>'    data-media="(min-width: 320px)"></div>  <%-- Portrait mobile --%>
    <div data-src='<%= path + ".img.480.medium." + extension + suffix %>'    data-media="(min-width: 321px)"></div>  <%-- Landscape mobile --%>
    <div data-src='<%= path + ".img.476.high." + extension + suffix %>'      data-media="(min-width: 481px)"></div>   <%-- Portrait iPad --%>
    <div data-src='<%= path + ".img.620.high." + extension + suffix %>'      data-media="(min-width: 769px)"></div>  <%-- Landscape iPad --%>
    <div data-src='<%= path + ".img.full.high." + extension + suffix %>'     data-media="(min-width: 1025px)"></div> <%-- Desktop --%>

    <%-- Fallback content for non-JS browsers. Same img src as the initial, unqualified source element. --%>
    <noscript>
        <img src='<%= path + ".img.320.low." + extension + suffix %>' alt='<%= alt %>'>
    </noscript>
</div>
```

La variable `path` contiene la ruta del recurso actual (el nodo del componente de imagen adaptable). El código genera una serie de `div` elementos con la siguiente estructura:

`<div data-scr = "*path-to-parent-node*.adaptive-image.adapt.*width*.*quality*.jpg" data-media="*media query*"></div>`

El valor del atributo `data-scr` es una URL que Sling resuelve en el servlet del componente de imagen adaptable que procesa la imagen. El atributo data-media contiene la consulta de medios que se evalúa con las propiedades del cliente.

El siguiente código de HTML es un ejemplo de los `div` elementos que genera JSP:

```xml
<div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.low.jpg'></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.medium.jpg'    data-media="(min-width: 320px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.480.medium.jpg'    data-media="(min-width: 321px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.476.high.jpg'     data-media="(min-width: 481px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.620.high.jpg'     data-media="(min-width: 769px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.full.high.jpg'     data-media="(min-width: 1025px)"></div>
```

#### Cambio de los selectores de tamaño de imagen {#changing-the-image-size-selectors}

Si personaliza el componente Imagen adaptable y cambia los selectores de anchura, también debe configurar el servlet del componente de imagen adaptable para que admita las anchuras.

### Explicación del servlet de componente de imagen adaptable {#understanding-the-adaptive-image-component-servlet}

El servlet de componente de imagen adaptable cambia el tamaño de una imagen JPEG según una anchura especificada y establece la calidad JPEG.

#### La interfaz del servlet de componente de imagen adaptable {#the-interface-of-the-adaptive-image-component-servlet}

El servlet de componente de imagen adaptable está enlazado al servlet de Sling predeterminado y admite las extensiones de archivo .jpg, .jpeg, .gif y .png. El selector de servlet es img.

>[!CAUTION]
>
>AEM Los archivos .gif animados no son compatibles con las representaciones adaptables en los archivos de formato .gif de la aplicación.

Por lo tanto, Sling resuelve las URL de solicitud HTTP del siguiente formato en este servlet:

`*path-to-node*.img.*extension*`

Por ejemplo, Sling reenvía solicitudes HTTP con la URL `http://localhost:4502/content/geometrixx/adaptiveImage.img.jpg` al servlet del componente de imagen adaptable.

Dos selectores adicionales especifican la anchura y la calidad JPEG de la imagen solicitada. El siguiente ejemplo solicita una imagen de anchura 480 píxeles y calidad media:

`http://localhost:4502/content/geometrixx/adaptiveImage.adapt.480.MEDIUM.jpg`

**Propiedades de imagen compatibles**

El servlet acepta un número finito de anchuras y calidades de imagen. Las siguientes anchuras son compatibles de forma predeterminada (en píxeles):

* completa
* 320
* 480
* 476
* 620

El valor completo indica que no hay escala.

Se admiten los siguientes valores para una calidad JPEG:

* BAJA
* MEDIANA
* ALTA

Los valores numéricos son 0,4; 0,82 y 1,0, respectivamente.

**Cambiar los anchos admitidos predeterminados**

Utilice la consola web ([http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)) o un nodo sling:OsgiConfig para configurar los anchos admitidos del servlet del componente de imagen adaptable de Adobe CQ.

AEM Para obtener información acerca de cómo configurar servicios de, vea [Configurar OSGi](/help/sites-deploying/configuring-osgi.md).

<table>
 <tbody>
  <tr>
   <th> </th>
   <th>consola web</th>
   <th>sling:OsgiConfig</th>
  </tr>
  <tr>
   <th>Nombre del servicio o nodo</th>
   <td>El nombre de servicio de la pestaña Configuración es Servlet de componente de imagen adaptable de Adobe CQ</td>
   <td>com.day.cq.wcm.foundation.impl. AdaptiveImageComponentServlet</td>
  </tr>
  <tr>
   <th>Propiedad</th>
   <td><p>Anchos admitidos</p>
    <ul>
     <li>Para añadir una anchura admitida, haga clic en un botón + e introduzca un entero positivo.</li>
     <li>Para quitar una anchura admitida, haga clic en el botón - asociado.</li>
     <li>Para modificar una anchura admitida, edite el valor del campo.</li>
    </ul> </td>
   <td><p>adapt.supported.widths</p>
    <ul>
     <li>La propiedad es un valor de tipo String multivalor.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

#### Detalles de implementación {#implementation-details}

La clase `com.day.cq.wcm.foundation.impl.AdaptiveImageComponentServlet` amplía la clase [AbstractImageServlet](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html). El código fuente AdaptiveImageComponentServlet se encuentra en la carpeta `/libs/foundation/src/impl/src/com/day/cq/wcm/foundation/impl`.

La clase utiliza anotaciones Felix SCR para configurar el tipo de recurso y la extensión de archivo con los que está asociado el servlet, así como el nombre del primer selector.

```java
@Component(metatype = true, label = "Adobe CQ Adaptive Image Component Servlet",
        description = "Render adaptive images in a variety of qualities")
@Service
@Properties(value = {
    @Property(name = "sling.servlet.resourceTypes", value = "foundation/components/adaptiveimage", propertyPrivate = true),
    @Property(name = "sling.servlet.selectors", value = "img", propertyPrivate = true),
    @Property(name = "sling.servlet.extensions", value ={
            "jpg",
            "jpeg",
            "png",
            "gif"
    }, propertyPrivate = true)
})
```

El servlet utiliza la anotación SCR de propiedad para establecer la calidad de imagen y las dimensiones admitidas de forma predeterminada.

```java
@Property(value = {
            "320", // iPhone portrait
            "480", // iPhone landscape
            "476", // iPad portrait
            "620" // iPad landscape
    },
            label = "Supported Widths",
            description = "List of widths this component is permitted to generate.")
```

La clase `AbstractImageServlet` proporciona el método `doGet` que procesa la solicitud HTTP. Este método determina el recurso asociado a la solicitud, recupera las propiedades del recurso del repositorio y las devuelve en un objeto [ImageContext](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html).

>[!NOTE]
>
>La clase [com.day.cq.commons.DownloadResource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/DownloadResource.html) proporciona `getFileReference method`, que recupera el valor de la propiedad `fileReference` del recurso.

La clase `AdaptiveImageComponentServlet` invalida el método `createLayer`. El método obtiene la ruta del recurso de imagen y el ancho de imagen solicitado del objeto `ImageContext`. A continuación, llama a los métodos de la clase `info.geometrixx.commons.impl.AdaptiveImageHelper`, que realiza el escalado real de la imagen.

La clase AdaptiveImageComponentServlet también reemplaza el método writeLayer. Este método aplica la calidad JPEG a la imagen.

### Servlet de modificación de referencia de imagen (Geometrixx común) {#image-reference-modification-servlet-geometrixx-common}

El servlet de modificación de referencia de imagen de ejemplo genera atributos de tamaño para que el elemento img escale una imagen en la página web.

#### Llamada al servlet {#calling-the-servlet}

El servlet está enlazado a `cq:page` recursos y admite la extensión de archivo .jpg. El selector de servlet es `image`. Por lo tanto, Sling resuelve las URL de solicitud HTTP del siguiente formato en este servlet:

`path-to-page-node.image.jpg`

Por ejemplo, Sling reenvía solicitudes HTTP con la dirección URL `http://localhost:4502/content/geometrixx/en.image.jpg` al servlet de modificación de referencia de imagen.

Otros tres selectores especifican la anchura, altura y (opcionalmente) calidad de la imagen solicitada. El siguiente ejemplo solicita una imagen de anchura 770 píxeles, altura 360 píxeles y calidad media.

`http://localhost:4502/content/geometrixx/en.image.770.360.MEDIUM.jpg`

**Propiedades de imagen compatibles**

El servlet acepta un número finito de dimensiones de imagen y valores de calidad.

Los siguientes valores son compatibles de forma predeterminada (widthxheight):

* 256 x 192
* 370 x 150
* 480 x 200
* 127 x 127
* 770 x 360
* 620 x 290
* 480 x 225
* 320 x 150
* 375 x 175
* 303x142
* 1170x400
* 940 x 340
* 770 x 300
* 480x190

Se admiten los siguientes valores para la calidad de imagen:

* baja
* mediano
* alto

AEM Al trabajar con los servicios, existen varios métodos para administrar las opciones de configuración de dichos servicios; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obtener información detallada.

#### Especificación del recurso de imagen {#specifying-the-image-resource}

La ruta de la imagen, las dimensiones y los valores de calidad deben almacenarse como propiedades de un nodo en el repositorio:

* El nombre del nodo es `image`.
* El nodo principal es el nodo `jcr:content` de un recurso `cq:page`.

* La ruta de acceso de la imagen se almacena como el valor de una propiedad denominada `fileReference`.

Al crear una página, use **Sidekick** para especificar la imagen y agregar el nodo `image` a las propiedades de la página:

1. En **Sidekick**, haga clic en la ficha **Página** y, a continuación, en **Propiedades de página**.
1. Haga clic en la ficha **Imagen** y especifique la imagen.
1. Haga clic en **OK**.

#### Detalles de implementación {#implementation-details-1}

La clase info.geometrixx.commons.impl.servlets.ImageReferenceModificationServlet amplía la clase [AbstractImageServlet](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html). Si tiene instalado el paquete cq-geometrixx-commons-pkg, el código fuente ImageReferenceModificationServlet se encuentra en la carpeta `/apps/geometrixx-commons/src/core/src/main/java/info/geometrixx/commons/impl/servlets`.

La clase utiliza anotaciones Felix SCR para configurar el tipo de recurso y la extensión de archivo con los que está asociado el servlet, así como el nombre del primer selector.

```java
@Component(metatype = true, label = "Adobe CQ Image Reference Modification Servlet",
        description = "Render the image associated with a page in a variety of dimensions and qualities")
@Service
@Properties(value = {
    @Property(name = "sling.servlet.resourceTypes", value = NameConstants.NT_PAGE, propertyPrivate = true),
    @Property(name = "sling.servlet.selectors", value = "image", propertyPrivate = true),
    @Property(name = "sling.servlet.extensions", value = "jpg", propertyPrivate = true)
})
```

El servlet utiliza la anotación SCR de propiedad para establecer la calidad de imagen y las dimensiones admitidas de forma predeterminada.

```java
@Property(label = "Image Quality",
            description = "Quality must be a double between 0.0 and 1.0", value = "0.82")
@Property(value = {
                "256x192", // Category page article list images
                "370x150", // "Most popular" desktop & iPad & carousel min-width: 1px
                "480x200", // "Most popular" phone
                "127x127", // article summary phone square images
                "770x360", // article summary, desktop
                "620x290", // article summary, tablet
                "480x225", // article summary, phone (landscape)
                "320x150", // article summary, phone (portrait) and fallback
                "375x175", // 2-column article summary, desktop
                "303x142", // 2-column article summary, tablet
                "1170x400", // carousel, full
                "940x340",  // carousel min-width: 980px
                "770x300",  // carousel min-width: 768px
                "480x190"   // carousel min-width: 480px
            },
            label = "Supported Resolutions",
            description = "List of resolutions this component is permitted to generate.")
```

La clase `AbstractImageServlet` proporciona el método `doGet` que procesa la solicitud HTTP. Este método determina el recurso asociado a la llamada, recupera las propiedades del recurso del repositorio y las guarda en un objeto [ImageContext](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html).

La clase `ImageReferenceModificationServlet` reemplaza el método `createLayer` e implementa la lógica que determina el recurso de imagen que se va a procesar. El método recupera un nodo secundario del nodo `jcr:content` de la página denominado `image`. Se crea un objeto [Image](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/foundation/Image.html) a partir de este nodo `image` y el método `getFileReference` devuelve la ruta de acceso al archivo de imagen desde la propiedad `fileReference` del nodo de imagen.

>[!NOTE]
>La clase [com.day.cq.commons.DownloadResource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/DownloadResource.html) proporciona el método getFileReference.
>

## Desarrollo de una cuadrícula fluida {#developing-a-fluid-grid}

AEM le permite implementar de forma eficiente y eficaz las redes fluidas. En esta página se explica cómo puede integrar la cuadrícula de fluidos o una implementación de cuadrícula existente (como [Bootstrap AEM](https://github.com/topics/twitter-bootstrap?l=css)) en la aplicación de la.

Si no está familiarizado con las cuadrículas de fluidos, consulte la sección [Introducción a las cuadrículas de fluidos](/help/sites-developing/responsive.md#developing-a-fluid-grid) en la parte inferior de esta página. Esta introducción proporciona una visión general de las cuadrículas fluidas y una guía para diseñarlas.

### Definición de la cuadrícula mediante un componente Página {#defining-the-grid-using-a-page-component}

Utilice los componentes de página para generar los elementos HTML que definen los bloques de contenido de la página. ClientLibraryFolder, al que hace referencia la página, proporciona el archivo CSS que controla el diseño de los bloques de contenido:

* Componente Página: añade elementos div que representan filas de bloques de contenido. Los elementos div que representan bloques de contenido incluyen un componente parsys en el que los autores agregan contenido.
* Carpeta de la biblioteca de cliente: proporciona el archivo CSS que incluye consultas de medios y estilos para los elementos div.

Por ejemplo, la aplicación Geometrixx-media de ejemplo contiene el componente media-home. Este componente de página inserta dos scripts, que generan dos elementos `div` de la clase `row-fluid`:

* La primera fila contiene un elemento `div` de la clase `span12` (el contenido abarca 12 columnas). El elemento `div` contiene el componente parsys.

* La segunda fila contiene dos elementos `div`, uno de la clase `span8` y el otro de la clase `span4`. Cada elemento `div` incluye el componente parsys.

```xml
<div class="page-content">
    <div class="row-fluid">
        <div class="span12">
            <cq:include path="grid-12-par" resourceType="foundation/components/parsys" />
        </div>
    </div>
    <div class="row-fluid">
        <div class="span8">
            <cq:include path="grid-8-par" resourceType="foundation/components/parsys" />
        </div>
        <div class="span4">
            <cq:include path="grid-4-par" resourceType="foundation/components/parsys" />
        </div>
    </div>
</div>
```

>[!NOTE]
>
>Cuando un componente incluye varios elementos `cq:include` que hacen referencia al componente parsys, cada atributo `path` debe tener un valor diferente.
>

#### Escala de la cuadrícula del componente Página {#scaling-the-page-component-grid}

El diseño asociado con el componente de página geometrixx-media (`/etc/designs/geometrixx-media`) contiene la ClientLibraryFolder `clientlibs`. Esta ClientLibraryFolder define estilos CSS para las clases `row-fluid`, las clases `span*` y las clases `span*` que son secundarias de las clases `row-fluid`. Las consultas de medios permiten redefinir los estilos para diferentes tamaños de ventanilla.

El siguiente ejemplo de CSS es un subconjunto de esos estilos. Este subconjunto se centra en las clases `span12`, `span8` y `span4`, así como en las consultas de medios para dos tamaños de ventanilla móvil. Tenga en cuenta las siguientes características del CSS:

* Los estilos `.span` definen los anchos de los elementos mediante números absolutos.
* Los estilos `.row-fluid .span*` definen las anchuras de los elementos como porcentajes del elemento principal. Los porcentajes se calculan a partir de las anchuras absolutas.
* Las consultas de medios para ventanillas más grandes asignan anchos absolutos mayores.

>[!NOTE]
>
>El ejemplo de Geometrixx Medias integra el módulo de JavaScript [Bootstrap](https://getbootstrap.com/2.0.2/) en su implementación de cuadrícula fluida. El marco de trabajo del Bootstrap proporciona el archivo bootstrap.css.

```xml
/* default styles (no media queries) */
 .span12 { width: 940px }
 .span8 { width: 620px }
 .span4 { width: 300px }
 .row-fluid .span12 { width: 100% }
 .row-fluid .span8 { width: 65.95744680851064% }
 .row-fluid .span4 { width: 31.914893617021278% }

@media (min-width: 768px) and (max-width: 979px) {
 .span12 { width: 724px; }
 .span8 {     width: 476px; }
 .span4 {     width: 228px; }
 .row-fluid .span12 {     width: 100%;}
 .row-fluid .span8 {     width: 65.74585635359117%; }
 .row-fluid .span4 {     width: 31.491712707182323%; }
}

@media (min-width: 1200px) {
 .span12 { width: 1170px }
 .span8 { width: 770px }
 .span4 { width: 370px }
 .row-fluid .span12 { width: 100% }
 .row-fluid .span8 { width: 65.81196581196582% }
 .row-fluid .span4 { width: 31.623931623931625% }
}
```

#### Cambiar la posición del contenido en la cuadrícula de componentes Página {#repositioning-content-in-the-page-component-grid}

Las páginas de la aplicación de Geometrixx Medias de ejemplo distribuyen filas de bloques de contenido horizontalmente en ventanillas amplias. En las ventanillas móviles más pequeñas, los mismos bloques se distribuyen verticalmente. En el siguiente ejemplo de CSS se muestran los estilos que implementan este comportamiento para el código de HTML que genera el componente de la página principal de medios:

* El CSS predeterminado para la página de bienvenida de medios asigna el estilo `float:left` para `span*` clases que se encuentran dentro de `row-fluid` clases.

* Las consultas de medios para ventanillas móviles más pequeñas asignan el estilo `float:none` a las mismas clases.

```xml
/* default styles (no media queries) */
    .row-fluid [class*="span"] {
        width: 100%;
        float: left;
}

@media (max-width: 767px) {
    [class*="span"], .row-fluid [class*="span"] {
        float: none;
        width: 100%;
    }
}
```

#### Modulice los componentes de la página {#tip-modularize-your-page-components}

Modulice los componentes para poder utilizar el código de forma eficiente. Es probable que el sitio utilice varios tipos diferentes de páginas, como una página de bienvenida, una página de artículo o una página de producto. Cada tipo de página contiene diferentes tipos de contenido y es probable que utilice diferentes diseños. Sin embargo, cuando ciertos elementos de cada diseño son comunes en varias páginas, puede reutilizar el código que implementa esa parte del diseño.

**Usar superposiciones de componentes de página**

Cree un componente de página principal que proporcione scripts para generar las distintas partes de una página, como las secciones `head` y `body`, y las secciones `header`, `content` y `footer` dentro del cuerpo.

Cree otros componentes de página que utilicen el componente de página principal como `cq:resourceSuperType`. Estos componentes incluyen scripts que anulan los scripts de la página principal según sea necesario.

Por ejemplo, la aplicación goemetrixx-media incluye el componente de página (el `sling:resourceSuperType` es el componente de página base). Varios componentes secundarios (como artículo, categoría y media-home) utilizan este componente de página como `sling:resourceSuperType`. Cada componente secundario incluye un archivo content.jsp que anula el archivo content.jsp del componente de página.

**Reutilizar scripts**

Cree varios scripts JSP que generen combinaciones de fila y columna comunes para varios componentes de página. Por ejemplo, el script `content.jsp` del artículo y los componentes de inicio de medios hacen referencia al script `8x4col.jsp`.

**Organizar estilos CSS por tamaño de ventanilla de destino**

Incluya estilos CSS y consultas de medios para diferentes tamaños de ventanilla móvil en archivos independientes. Utilice carpetas de la biblioteca del cliente para concatenarlas.

### Insertar componentes en la cuadrícula de la página {#inserting-components-into-the-page-grid}

Cuando los componentes generan un solo bloque de contenido, generalmente la cuadrícula que establece el componente de página controla la ubicación del contenido.

Como autor, el bloque de contenido se puede representar en varios tamaños y posiciones relativas. El texto de contenido no debe utilizar direcciones relativas para hacer referencia a otros bloques de contenido.

Si es necesario, el componente debe proporcionar las bibliotecas CSS o JavaScript necesarias para el código de HTML que genera. Utilice una carpeta de biblioteca de cliente dentro del componente para generar los archivos CSS y JS. Para exponer los archivos, [cree una dependencia o incruste la biblioteca](/help/sites-developing/clientlibs.md#creating-client-library-folders) en otra carpeta de biblioteca de cliente debajo de la carpeta /etc.

**Subcuadrículas**

Si el componente contiene varios bloques de contenido, agregue los bloques de contenido dentro de una fila para establecer una subcuadrícula en la página:

* Utilice los mismos nombres de clase que el componente de página contenedora para poder expresar los elementos div como filas y bloques de contenido.
* Para anular el comportamiento que implementa la CSS del diseño de página, utilice un segundo nombre de clase para el elemento div de fila y proporcione el CSS asociado en una carpeta de biblioteca de cliente.

Por ejemplo, el componente `/apps/geometrixx-media/components/2-col-article-summary` genera dos columnas de contenido. El HTML que genera tiene la siguiente estructura:

```xml
<div class="row-fluid mutli-col-article-summary">
    <div class="span6">
        <article>
            <div class="article-summary-image">...</div>
            <div class="social-header">...</div>
            <div class="article-summary-description">...</div>
            <div class="social">...</div>
        </article>
    </div>
</div>
```

Los selectores `.row-fluid .span6` del CSS de la página se aplican a los elementos `div` de la misma clase y estructura en este HTML. Sin embargo, el componente también incluye la carpeta de biblioteca de cliente /apps/geometrixx-media/components/2-col-article-summary/clientlibs:

* CSS utiliza las mismas consultas de medios que el componente de página para establecer cambios en el diseño con los mismos anchos de página discretos.
* Los selectores utilizan la clase `multi-col-article-summary` del elemento de fila `div` para anular el comportamiento de la clase `row-fluid` de la página.

Por ejemplo, los estilos siguientes se incluyen en el archivo `/apps/geometrixx-media/components/2-col-article-summary/clientlibs/css/responsive-480px.css`:

```xml
@media (max-width: 480px) {
    .mutli-col-article-summary .article-summary-image {
        float: left;
        width: 127px;
    }
    .mutli-col-article-summary .article-summary-description {
        width: auto;
        margin-left: 127px;
    }
    .mutli-col-article-summary .article-summary-description h4 {
        padding-left: 10px;
    }
    .mutli-col-article-summary .article-summary-text {
        margin-left: 127px;
        min-height: 122px;
        top: 0;
    }
}
```

## Introducción a las cuadrículas fluidas {#introduction-to-fluid-grids}

Las cuadrículas fluidas permiten que los diseños de página se adapten a las dimensiones de la ventanilla del cliente. Las cuadrículas constan de columnas lógicas y filas que colocan los bloques de contenido en la página.

* Las columnas determinan las posiciones horizontales y las anchuras de los bloques de contenido.
* Las filas determinan las posiciones verticales relativas de los bloques de contenido.

Con la tecnología de HTML5 puede implementar la cuadrícula y manipularla para adaptar los diseños de página a diferentes tamaños de ventanilla:

* Los elementos del HTML `div` contienen bloques de contenido que abarcan algunas columnas.
* Uno o más de estos elementos div comprenden una fila cuando comparten un elemento div principal común.

### Uso de anchos discretos {#using-discrete-widths}

Para cada rango de anchos de ventanilla móvil objetivo, utilice un ancho de página estático y bloques de contenido de ancho constante. Al cambiar manualmente el tamaño de una ventana del explorador, los cambios en el tamaño del contenido se producen en anchos de ventana discretos (también conocidos como puntos de interrupción). Por lo tanto, los diseños de página se respetan más estrechamente, lo que maximiza la experiencia del usuario.

#### Escala de la cuadrícula {#scaling-the-grid}

Utilice cuadrículas para escalar bloques de contenido y adaptarse a diferentes tamaños de ventanilla. Los bloques de contenido abarcan un número específico de columnas. A medida que los anchos de columna aumentan o disminuyen para adaptarse a diferentes tamaños de ventanilla, los anchos de los bloques de contenido aumentan o disminuyen en consecuencia. La escala puede admitir ventanillas móviles grandes y medianas lo suficientemente anchas como para admitir la colocación simultánea de bloques de contenido.

![Imagen de dos cuadrículas, una de ellas con una escala menor que la otra.](do-not-localize/chlimage_1-1a.png)

#### Reposición de contenido en la cuadrícula {#repositioning-content-in-the-grid}

El tamaño de los bloques de contenido se puede restringir por una anchura mínima, más allá de la cual el escalado ya no es efectivo. Para las ventanillas móviles más pequeñas, la cuadrícula se puede utilizar para distribuir verticalmente bloques de contenido en lugar de horizontalmente.

![Imagen de dos cuadrículas, una de las cuales está colocada de forma más pequeña que la otra.](do-not-localize/chlimage_1-2a.png)

### Diseño de la cuadrícula {#designing-the-grid}

Determine las columnas y filas en las que debe colocar los bloques de contenido de las páginas. Los diseños de página determinan la cantidad de columnas y filas que abarcan la cuadrícula.

**Número de columnas**

Incluya suficientes columnas para colocar horizontalmente los bloques de contenido en todos los diseños, para todos los tamaños de ventanilla. Utilice más columnas de las que se necesitan actualmente para poder acomodar futuros diseños de página.

**Contenido de fila**

Utilice filas para controlar la posición vertical de los bloques de contenido. Determine los bloques de contenido que comparten la misma fila:

* Los bloques de contenido que se encuentran uno junto al otro horizontalmente en cualquiera de los diseños están en la misma fila.
* Los bloques de contenido que se encuentran uno junto al otro horizontalmente (ventanillas más anchas) y verticalmente (ventanillas más pequeñas) están en la misma fila.

### Implementaciones de cuadrícula {#grid-implementations}

Cree clases y estilos CSS para poder controlar el diseño de los bloques de contenido en una página. Los diseños de página suelen basarse en el tamaño y la posición relativos de los bloques de contenido dentro de la ventanilla. La ventanilla determina el tamaño real de los bloques de contenido. El CSS debe tener en cuenta los tamaños relativo y absoluto. Puede implementar una cuadrícula fluida utilizando tres tipos de clases CSS:

* Una clase para un elemento `div` que es un contenedor para todas las filas. Esta clase establece el ancho absoluto de la cuadrícula.
* Una clase para `div` elementos que representan una fila. Esta clase controla la posición horizontal o vertical de los bloques de contenido que contiene.
* Clases para `div` elementos que representan bloques de contenido de diferentes anchos. Las anchuras se expresan como un porcentaje del padre (la fila).

Las anchuras de las ventanillas móviles de destino (y sus consultas de medios asociadas) delimitan los anchos discretos que se utilizan para un diseño de página.

#### Anchuras de los bloques de contenido {#widths-of-content-blocks}

Por lo general, los estilos `width` de las clases de bloques de contenido se basan en las siguientes características de la página y la cuadrícula:

* El ancho de página absoluto que utiliza para cada tamaño de ventanilla de destino. Valores conocidos.
* Ancho absoluto de las columnas de la cuadrícula para cada ancho de página. Usted determina estos valores.
* El ancho relativo de cada columna como porcentaje del ancho total de la página. Usted calcula estos valores.

El CSS incluye una serie de consultas de medios que utilizan la siguiente estructura:

```xml
@media(query_for_targeted_viewport){

  .class_for_container{ width:absolute_page_width }
  .class_for_row { width:100%}

  /* several selectors for content blocks   */
  .class_for_content_block1 { width:absolute_block_width1 }
  .class_for_content_block2 { width:absolute_block_width2 }
  ...

  /* several selectors for content blocks inside rows */
  .class_for_row .class_for_content_block1 { width:relative_block_width1 }
  .class_for_row .class_for_content_block2 { width:relative_block_width2 }
  ...
}
```

Utilice el siguiente algoritmo como punto de partida para desarrollar las clases de elementos y los estilos CSS para sus páginas.

1. Defina un nombre de clase para el elemento div que contiene todas las filas, por ejemplo, `content.`
1. Defina una clase CSS para los elementos div que representan filas, como `row-fluid`.
1. Defina nombres de clase para los elementos de bloque de contenido. Se requiere una clase para todas las anchuras posibles, en términos de intervalos de columnas. Por ejemplo, use la clase `span3` para `div` elementos que abarcan tres columnas, use las clases `span4` para intervalos de cuatro columnas. Defina tantas clases como columnas de la cuadrícula.

1. Para cada tamaño de ventanilla móvil que vaya a segmentar, agregue la consulta de medios correspondiente al archivo CSS. Agregue los siguientes elementos en cada consulta de medios:

   * Un selector para la clase `content`, por ejemplo, `.content{}`.
   * Selectores para cada clase span, por ejemplo, `.span3{ }`.
   * Un selector para la clase `row-fluid`, por ejemplo, `.row-fluid{ }`
   * Selectores para clases span que están dentro de clases row-flow, por ejemplo, `.row-fluid span3 { }`.

1. Agregue estilos de anchura para cada selector:

   1. Establezca la anchura de los selectores `content` en el tamaño absoluto de la página, por ejemplo, `width:480px`.
   1. Establezca la anchura de todos los selectores de fluido de fila en 100%.
   1. Establezca la anchura de todos los selectores de espacio en la anchura absoluta del bloque de contenido. Una cuadrícula trivial utiliza columnas distribuidas uniformemente de la misma anchura: `(absolute width of page)/(number of columns)`.
   1. Establezca la anchura de los selectores `.row-fluid .span` como un porcentaje de la anchura total. Calcule esta anchura utilizando la fórmula `(absolute span width)/(absolute page width)*100`.

#### Colocación de bloques de contenido en filas {#positioning-content-blocks-in-rows}

Utilice el estilo flotante de la clase `.row-fluid` para controlar si los bloques de contenido de una fila se organizan horizontal o verticalmente.

* El estilo `float:left` o `float:right` provoca la distribución horizontal de elementos secundarios (bloques de contenido).

* El estilo `float:none` provoca la distribución vertical de los elementos secundarios.

Agregue el estilo al selector `.row-fluid` dentro de cada consulta multimedia. Establezca el valor según el diseño de página que esté utilizando para esa consulta multimedia. Por ejemplo, el diagrama siguiente ilustra una fila que distribuye el contenido horizontalmente para las ventanillas anchas y verticalmente para las ventanillas estrechas.

![Dos imágenes de bloques de contenido en una fila; la segunda imagen muestra la fila reposicionada.](do-not-localize/chlimage_1-3a.png)

El siguiente CSS podría implementar este comportamiento:

```xml
@media (min-width: 768px) and (max-width: 979px) {
   .row-fluid {
       width:100%;
       float:left
   }
}

@media (max-width:480px){
    .row-fluid {
       width:100%;
       float:none
   }
}
```

#### Asignación de clases a bloques de contenido {#assigning-classes-to-content-blocks}

Para el diseño de página de cada tamaño de ventanilla móvil que vaya a segmentar, determine el número de columnas que abarca cada bloque de contenido. A continuación, determine qué clase utilizar para los elementos div de esos bloques de contenido.

AEM Cuando haya establecido las clases div, puede implementar la cuadrícula mediante la aplicación de la aplicación de la.
