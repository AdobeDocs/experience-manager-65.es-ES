---
title: Diseño interactivo para páginas web
seo-title: Responsive design for web pages
description: Con un diseño interactivo, las mismas páginas se pueden mostrar de forma eficaz en varios dispositivos en varias orientaciones
seo-description: With responsive design, the same pages can be effectively displayed on multiple devices in multiple orientations
uuid: 3d324557-e7ff-4c82-920f-9b5a906925e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 532544b0-1932-419a-b6bd-ecf57a926fef
legacypath: /content/docs/en/aem/6-0/develop/mobile/responsive
exl-id: c705710b-a94a-4f4f-affa-ddd4fc6cb0ec
source-git-commit: e05f6cd7cf17f4420176cf76f28cb469bcee4a0a
workflow-type: tm+mt
source-wordcount: '5336'
ht-degree: 0%

---

# Diseño interactivo para páginas web{#responsive-design-for-web-pages}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren procesamiento del lado del cliente basado en el marco de aplicaciones de una sola página (por ejemplo, _React_). [Más información](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Varios ejemplos se basan en el contenido de muestra de Geometrixx, que ya no se envía con AEM (Adobe Experience Manager), tras ser reemplazado por We.Retail. Consulte el documento [Implementación de referencia de We.Retail](/help/sites-developing/we-retail.md#we-retail-geometrixx) para obtener información sobre cómo descargar e instalar Geometrixx.

Diseñe las páginas web para que se adapten a la ventanilla del cliente en la que se muestran. Con un diseño interactivo, las mismas páginas se pueden mostrar de forma eficaz en varios dispositivos en ambas orientaciones. La siguiente imagen muestra algunas maneras en que una página puede responder a los cambios en el tamaño de la ventanilla móvil:

* Diseño: Utilice diseños de una sola columna para ventanillas más pequeñas y diseños de varias columnas para ventanillas más grandes.
* Tamaño del texto: Utilice un tamaño de texto mayor (cuando corresponda, como encabezados) en ventanillas más grandes.
* Contenido: Incluya solo el contenido más importante cuando se muestre en dispositivos más pequeños.
* Navegación: Se proporcionan herramientas específicas del dispositivo para acceder a otras páginas.
* Imágenes: Proporcionar representaciones de imagen adecuadas para la ventanilla móvil del cliente. según las dimensiones de la ventana.

![Chlimage_1-4](assets/chlimage_1-4a.png)

Desarrolle aplicaciones de Adobe Experience Manager (AEM) que generen páginas de HTML5 que se adapten a múltiples tamaños de ventana y orientaciones. Por ejemplo, los siguientes intervalos de anchura de las ventanillas móviles se corresponden con varios tipos de dispositivos y orientaciones

* Anchura máxima de 480 píxeles (teléfono, vertical)
* Anchura máxima de 767 píxeles (teléfono, horizontal)
* Anchura entre 768 píxeles y 979 píxeles (tableta, vertical)
* Anchura entre 980 píxeles y 1199 píxeles (tableta, horizontal)
* Anchura de 1200 píxeles o buena (escritorio)

Consulte los siguientes temas para obtener información sobre la implementación del comportamiento de diseño interactivo:

* [Consultas de medios](/help/sites-developing/responsive.md#using-media-queries)
* [Cubiertas fluidas](/help/sites-developing/responsive.md#developing-a-fluid-grid)
* [Imágenes adaptables](/help/sites-developing/responsive.md#using-adaptive-images)

A medida que diseña, use **[!UICONTROL Barra de tareas]** para obtener una vista previa de las páginas de distintos tamaños de pantalla.

## Antes de desarrollar {#before-you-develop}

Antes de desarrollar la aplicación de AEM que admite las páginas web, se deben tomar varias decisiones de diseño. Por ejemplo, debe tener la siguiente información:

* Los dispositivos a los que está dirigiendo.
* Los tamaños de las ventanillas de destino.
* Los diseños de página para cada uno de los tamaños de la ventanilla objetivo.

### Estructura de la aplicación {#application-structure}

La estructura de aplicación AEM típica admite todas las implementaciones de diseño adaptables:

* Los componentes de página residen debajo de /apps/*application_name*/componentes
* Las plantillas residen debajo de /apps/*application_name*/templates
* Los diseños se encuentran debajo de /etc/designs

## Uso de consultas de medios {#using-media-queries}

Las consultas de medios permiten el uso selectivo de estilos CSS para el procesamiento de páginas. AEM herramientas y funciones de desarrollo le permiten implementar de forma eficaz y eficiente las consultas de medios en sus aplicaciones.

El grupo W3C proporciona la variable [Consultas multimedia](https://www.w3.org/TR/mediaqueries-3/) recomendación que describe esta función de CSS3 y la sintaxis.

### Creación del archivo CSS {#creating-the-css-file}

En el archivo CSS, defina las consultas de medios en función de las propiedades de los dispositivos a los que esté dirigiendo. La siguiente estrategia de implementación es efectiva para administrar estilos para cada consulta de medios:

* Utilice ClientLibraryFolder para definir el CSS que se ensamblará cuando se represente la página.
* Defina cada consulta de medios y los estilos asociados en archivos CSS independientes. Es útil utilizar nombres de archivo que representen las características del dispositivo de la consulta de medios.
* Defina estilos comunes a todos los dispositivos en un archivo CSS independiente.
* En el archivo css.txt de ClientLibraryFolder, ordene los archivos CSS de la lista como sea necesario en el archivo CSS ensamblado.

La variable `We.Retail` Media sample utiliza esta estrategia para definir estilos en el diseño del sitio. El archivo CSS utilizado por `We.Retail` está en `*/apps/weretail/clientlibs/clientlib-site/less/grid.less`.

La tabla siguiente muestra los archivos de la carpeta secundaria css.

<table>
 <tbody>
  <tr>
   <th>Nombre del archivo</th>
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
   <td>Estilos para todos los medios con una anchura o anchura de 1200 píxeles.</td>
   <td><p>@media (min-width: 1200 px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-980px-1199px.css</td>
   <td>Estilos para medios con una anchura de entre 980 píxeles y 1199 píxeles.</td>
   <td><p>@media (min-width: 980 px) y (ancho máximo: 1199 px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-768px-979px.css</td>
   <td>Estilos para medios con una anchura de entre 768 píxeles y 979 píxeles. </td>
   <td><p>@media (min-width: 768 px) y (ancho máximo: 979 px) {<br /> ...<br /> }</p> </td>
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

El archivo css.txt en la variable `/etc/designs/weretail/clientlibs` carpeta enumera los archivos CSS que incluye la carpeta de biblioteca del cliente. El orden de los archivos implementa la prioridad de estilo. Los estilos son más específicos a medida que disminuye el tamaño del dispositivo.

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

**Sugerencia**: Los nombres de archivo descriptivos permiten identificar fácilmente el tamaño de la ventanilla objetivo.

### Uso de consultas de medios con páginas AEM {#using-media-queries-with-aem-pages}

Incluya la carpeta de la biblioteca del cliente en el script JSP del componente de página. De este modo, se genera el archivo CSS que incluye las consultas de medios y hace referencia al archivo.

```xml
<ui:includeClientLib categories="apps.weretail.all"/>
```

>[!NOTE]
>
>La variable `apps.weretail.all` carpeta de biblioteca de cliente incrusta la biblioteca clientlibs.

El script JSP genera el siguiente código de HTML que hace referencia a las hojas de estilo:

```xml
<link rel="stylesheet" href="/etc/designs/weretail/clientlibs-all.css" type="text/css">
<link href="/etc/designs/weretail.css" rel="stylesheet" type="text/css">
```

## Vista previa para dispositivos específicos {#previewing-for-specific-devices}

Consulte vistas previas de las páginas en diferentes tamaños de ventanilla para poder probar el comportamiento del diseño interactivo. En **[!UICONTROL Vista previa]** modo, **[!UICONTROL Barra de tareas]** incluye un **[!UICONTROL Dispositivos]** menú desplegable que utiliza para seleccionar un dispositivo. Al seleccionar un dispositivo, la página cambia para adaptarse al tamaño de la ventanilla móvil.

![Chlimage_1-5](assets/chlimage_1-5a.png)

Para activar la vista previa del dispositivo en **[!UICONTROL Barra de tareas]**, debe configurar la página y la variable **[!UICONTROL MobileEmulatorProvider]** servicio. Otra configuración de página controla la lista de dispositivos que aparecen en la **[!UICONTROL Dispositivos]** lista.

### Adición de la lista de dispositivos {#adding-the-devices-list}

La variable **[!UICONTROL Dispositivos]** la lista aparece en **[!UICONTROL Barra de tareas]** cuando su página incluye el script JSP que procesa el **[!UICONTROL Dispositivos]** lista. Para agregar la variable **[!UICONTROL Dispositivos]** a **[!UICONTROL Barra de tareas]**, incluya el `/libs/wcm/mobile/components/simulator/simulator.jsp` en el `head` de su página.

Incluya el siguiente código en el JSP que define la variable `head` sección:

`<cq:include script="/libs/wcm/mobile/components/simulator/simulator.jsp"/>`

Para ver un ejemplo, abra el `/apps/weretail/components/page/head.jsp` en CRXDE Lite.

### Registro de componentes de página para simulación {#registering-page-components-for-simulation}

Para permitir que el simulador de dispositivos admita sus páginas, registre los componentes de su página con el servicio de fábrica MobileEmulatorProvider y defina la variable `mobile.resourceTypes` propiedad.

Al trabajar con AEM, existen varios métodos para administrar los ajustes de configuración de dichos servicios; see [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información.

Por ejemplo, para crear un ` [sling:OsgiConfig](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)` en la aplicación:

* Carpeta principal: `/apps/application_name/config`
* Nombre: `com.day.cq.wcm.mobile.core.impl.MobileEmulatorProvider-*alias*`

   El `*alias*` es necesario porque el servicio MobileEmulatorProvider es un servicio de fábrica. Utilice cualquier alias que sea único para esta fábrica.

* jcr:primaryType: `sling:OsgiConfig`

Agregue la siguiente propiedad de nodo:

* Nombre: `mobile.resourceTypes`
* Tipo: `String[]`
* Valor: Las rutas a los componentes de página que representan las páginas web. Por ejemplo, la aplicación geometrixx-media utiliza los siguientes valores:

   ```
   geometrixx-media/components/page
    geometrixx-unlimited/components/pages/page
    geometrixx-unlimited/components/pages/coverpage
    geometrixx-unlimited/components/pages/issue
   ```

### Especificación de los grupos de dispositivos {#specifying-the-device-groups}

Para especificar los grupos de dispositivos que aparecen en la lista Dispositivos, agregue una `cq:deviceGroups` a la `jcr:content` nodo de la página raíz del sitio. El valor de la propiedad es una matriz de rutas a los nodos de grupo de dispositivos.

Los nodos del grupo de dispositivos se encuentran en la variable `/etc/mobile/groups` carpeta.

Por ejemplo, la página raíz del sitio de Geometrixx Medias es `/content/geometrixx-media`. La variable `/content/geometrixx-media/jcr:content` incluye la siguiente propiedad:

* Nombre: `cq:deviceGroups`
* Tipo: `String[]`
* Valor: `/etc/mobile/groups/responsive`

Utilice la consola Herramientas para [crear y editar grupos de dispositivos](/help/sites-developing/groupfilters.md).

>[!NOTE]
>
>Para los grupos de dispositivos que utilice para el diseño interactivo, edite el grupo de dispositivos y, en la ficha General, seleccione Deshabilitar emulador. Esta opción evita que aparezca el carrusel del emulador, lo que no es relevante para el diseño interactivo.

## Uso de imágenes adaptables {#using-adaptive-images}

Puede utilizar consultas de medios para seleccionar un recurso de imagen para mostrar en la página. Sin embargo, todos los recursos que utilizan una consulta de medios para condicionalizar su uso se descargan al cliente. La consulta de medios simplemente determina si se muestra el recurso descargado.

Para recursos de gran tamaño, como imágenes, la descarga de todos los recursos no es un uso eficiente de la canalización de datos del cliente. Para descargar recursos de forma selectiva, utilice JavaScript para iniciar la solicitud de recursos después de que las consultas de medios realicen la selección.

La siguiente estrategia carga un único recurso que se elige mediante consultas de medios:

1. Agregue un elemento DIV para cada versión del recurso. Incluya el URI del recurso como el valor de un valor de atributo. El explorador no interpreta el atributo como un recurso.
1. Agregue una consulta de medios a cada elemento DIV que sea adecuado para el recurso.
1. Cuando se carga el documento o se cambia el tamaño de la ventana, el código JavaScript prueba la consulta de medios de cada elemento DIV.
1. En función de los resultados de las consultas, determine qué recurso incluir.
1. Inserte un elemento HTML en el DOM que haga referencia al recurso.

### Evaluación de consultas de medios mediante JavaScript {#evaluating-media-queries-using-javascript}

Implementación de [Interfaz MediaQueryList](https://drafts.csswg.org/cssom-view/#the-mediaquerylist-interface) que define W3C permite evaluar consultas de medios mediante JavaScript. Puede aplicar lógica a los resultados de la consulta de medios y ejecutar secuencias de comandos que estén dirigidas a la ventana actual:

* Los navegadores que implementan la interfaz MediaQueryList admiten el `window.matchMedia()` función. Esta función prueba las consultas de medios con una cadena determinada. La función devuelve un valor `MediaQueryList` que proporciona acceso a los resultados de la consulta.

* Para los exploradores que no implementan la interfaz, puede utilizar un `matchMedia()` relleno de políticas, como [matchMedia.js](https://github.com/paulirish/matchMedia.js), una biblioteca JavaScript disponible de forma gratuita.

#### Selección de recursos específicos de medios {#selecting-media-specific-resources}

W3C [elemento de imagen](https://html.spec.whatwg.org/multipage/embedded-content.html#the-picture-element) utiliza consultas de medios para determinar el origen que se utilizará para los elementos de imagen. El elemento de imagen utiliza atributos de elemento para asociar consultas de medios con rutas de imágenes.

La disponibilidad gratuita [biblioteca picturefill.js](https://github.com/scottjehl/picturefill) proporciona una funcionalidad similar a la propuesta `picture` y utiliza una estrategia similar. Las llamadas a la biblioteca picturefill.js `window.matchMedia` para evaluar las consultas de medios definidas para un conjunto de `div` elementos. Cada `div` element también especifica un origen de imagen. El origen se utiliza cuando la consulta de medios del `div` elementos devueltos `true`.

La variable `picturefill.js` La biblioteca de requiere un código de HTML similar al del siguiente ejemplo:

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
</div>
```

Cuando se representa la página, picturefull.js inserta un `img` como el último elemento secundario del `<div data-picture>` elemento:

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
    <img src="path to medium image">
</div>
```

En una página AEM, el valor de la variable `data-src` es la ruta a un recurso en el repositorio.

### Implementación de imágenes adaptables en AEM {#implementing-adaptive-images-in-aem}

Para implementar imágenes adaptables en la aplicación de AEM, debe agregar las bibliotecas de JavaScript necesarias e incluir el marcado de HTML requerido en las páginas.

**Bibliotecas**

Obtenga las siguientes bibliotecas JavaScript e inclúyalas en una carpeta de la biblioteca del cliente:

* [matchMedia.js](https://github.com/paulirish/matchMedia.js) (para exploradores que no implementan la interfaz MediaQueryList )
* [picturefill.js](https://github.com/scottjehl/picturefill)
* jquery.js (disponible mediante la variable `/etc/clientlibs/granite/jquery` carpeta de la biblioteca del cliente (categoría = jquery)
* [jquery.debouncedresize.js](https://github.com/louisremi/jquery-smartresize) (un evento jquery que se produce una vez después de cambiar el tamaño de la ventana)

**Sugerencia:** Puede concatenar automáticamente varias carpetas de la biblioteca de cliente mediante [incrustar](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries).

**HTML**

Cree un componente que genere los elementos div necesarios que el código picturefill.js espera. En una página AEM, el valor del atributo data-src es la ruta a un recurso en el repositorio. Por ejemplo, un componente de página puede codificar de forma rígida las consultas de medios y las rutas asociadas para las representaciones de imágenes en DAM. O bien, cree un componente de imagen personalizado que permita a los autores seleccionar representaciones de imagen o especificar opciones de renderización en tiempo de ejecución.

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
>El componente de base de la imagen adaptable implementa imágenes adaptables:
>
>* Carpeta de biblioteca de cliente: `/libs/foundation/components/adaptiveimage/clientlibs`
>* Secuencia de comandos que genera el HTML: `/libs/foundation/components/adaptiveimage/adaptiveimage.jsp`
>
>La sección siguiente proporciona detalles sobre este componente.

### Explicación de la renderización de imágenes en AEM {#understanding-image-rendering-in-aem}

Para personalizar la renderización de imágenes, debe comprender la implementación AEM de renderización de imágenes estáticas predeterminada. AEM proporciona el componente Imagen y un servlet de renderización de imágenes que trabajan juntos para procesar imágenes para una página web. Las siguientes secuencias de eventos se producen cuando el componente Imagen se incluye en el sistema de párrafos de la página:

1. Creación: Los autores editan el componente Imagen para especificar el archivo de imagen que se incluirá en una página HTML. La ruta del archivo se almacena como un valor de propiedad del nodo del componente Imagen.
1. Solicitud de página: El JSP del componente de página genera el código de HTML. El JSP del componente Imagen genera y añade un elemento img a la página.
1. Solicitud de imagen: El explorador web carga la página y solicita la imagen según el atributo src del elemento img.
1. Representación de imágenes: El servlet de renderización de imágenes devuelve la imagen al explorador web.

![Chlimage_1-6](assets/chlimage_1-6a.png)

Por ejemplo, el JSP del componente Imagen genera el siguiente elemento HTML:

`<img title="My Image" alt="My Image" class="cq-dd-image" src="/content/mywebsite/en/_jcr_content/par/image_0.img.jpg/1358372073597.jpg">`

Cuando el explorador carga la página, solicita la imagen utilizando el valor del atributo src como dirección URL. Sling descompone la dirección URL:

* Recurso: `/content/mywebsite/en/_jcr_content/par/image_0`
* Extensión de nombre de archivo: `.jpg`
* Selector: `img`
* Sufijo: `1358372073597.jpg`

La variable `image_0` el nodo tiene un `jcr:resourceType` valor de `foundation/components/image`, que tiene un `sling:resourceSuperType` valor de `foundation/components/parbase`. El componente parbase incluye la secuencia de comandos img.GET.java que coincide con el selector y la extensión de nombre de archivo de la dirección URL de la solicitud. CQ utiliza este script (servlet) para renderizar la imagen.

Para ver el código fuente de la secuencia de comandos, utilice CRXDE Lite para abrir el `/libs/foundation/components/parbase/img.GET.java`
archivo.

## Escalado de imágenes para el tamaño actual de la ventanilla móvil {#scaling-images-for-the-current-viewport-size}

Escale las imágenes durante la ejecución según las características de la ventanilla móvil del cliente para proporcionar imágenes que se ajusten a los principios del diseño interactivo. Utilice el mismo patrón de diseño que la representación de imágenes estáticas, utilizando un servlet y un componente de creación.

El componente debe realizar las siguientes tareas:

* Almacene la ruta y las dimensiones deseadas del recurso de imagen como valores de propiedad.
* Generar `div` elementos que contienen selectores de medios y llamadas de servicio para procesar la imagen.

>[!NOTE]
>
>El cliente web utiliza las bibliotecas JavaScript matchMedia y Picturefill (o bibliotecas similares) para evaluar los selectores de medios.

El servlet que procesa la solicitud de imagen debe realizar las siguientes tareas:

* Recupere la ruta y las dimensiones de la imagen desde las propiedades del componente.
* Escale la imagen según las propiedades y devuelva la imagen.

**Soluciones disponibles**

AEM instala las siguientes implementaciones que puede utilizar o ampliar.

* Componente de base de imagen adaptable que genera consultas de medios y solicitudes HTTP al servlet del componente de imagen adaptable que escala las imágenes.
* El paquete de Geometrixx Commons instala los servlets de muestra de Image Reference Modification Servlet que modifican la resolución de la imagen.

### Explicación del componente de imagen adaptable {#understanding-the-adaptive-image-component}

El componente de imagen adaptable genera llamadas al servlet del componente de imagen adaptable para procesar una imagen cuyo tamaño depende de la pantalla del dispositivo. El componente incluye los siguientes recursos:

* JSP: Agrega elementos div que asocian consultas de medios con llamadas al servlet del componente de imagen adaptable.
* Bibliotecas de cliente: La carpeta clientlibs es un `cq:ClientLibraryFolder` que monta la biblioteca JavaScript matchMedia polyfill y una biblioteca JavaScript Picturefill modificada.
* Cuadro de diálogo Editar: La variable `cq:editConfig` el nodo anula el componente de imagen base de CQ, de modo que el destino de colocación crea un componente de imagen adaptable en lugar de un componente de imagen base.

#### Adición de elementos DIV {#adding-the-div-elements}

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

La variable `path` contiene la ruta del recurso actual (el nodo de componente de imagen adaptable). El código genera una serie de `div` elementos con la siguiente estructura:

`<div data-scr = "*path-to-parent-node*.adaptive-image.adapt.*width*.*quality*.jpg" data-media="*media query*"></div>`

El valor de la variable `data-scr` es una URL que Sling resuelve en el servlet del componente de imagen adaptable que procesa la imagen. El atributo data-media contiene la consulta de medios que se evalúa en relación con las propiedades del cliente.

El siguiente código de HTML es un ejemplo de la variable `div` elementos que genera el JSP:

```xml
<div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.low.jpg'></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.medium.jpg'    data-media="(min-width: 320px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.480.medium.jpg'    data-media="(min-width: 321px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.476.high.jpg'     data-media="(min-width: 481px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.620.high.jpg'     data-media="(min-width: 769px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.full.high.jpg'     data-media="(min-width: 1025px)"></div>
```

#### Cambio de los selectores de tamaño de imagen {#changing-the-image-size-selectors}

Si personaliza el componente de imagen adaptable y cambia los selectores de anchura, también debe configurar el servlet del componente de imagen adaptable para que admita los anchos.

### Explicación del servlet del componente de imagen adaptable {#understanding-the-adaptive-image-component-servlet}

El servlet del componente de imagen adaptable cambia el tamaño de una imagen de JPEG según una anchura especificada y establece la calidad del JPEG.

#### Interfaz del servlet del componente de imagen adaptable {#the-interface-of-the-adaptive-image-component-servlet}

El servlet del componente de imagen adaptable está enlazado al servlet Sling predeterminado y admite las extensiones de archivo .jpg, .jpeg, .gif y .png. El selector de servlet es img.

>[!CAUTION]
>
>Los archivos .gif animados no se admiten en AEM para representaciones adaptables.

Por lo tanto, Sling resuelve las URL de solicitud HTTP del siguiente formato para este servlet:

`*path-to-node*.img.*extension*`

Por ejemplo, Sling reenvía solicitudes HTTP con la dirección URL `http://localhost:4502/content/geometrixx/adaptiveImage.img.jpg` a Servlet de componente de imagen adaptable.

Dos selectores adicionales especifican la anchura de la imagen solicitada y la calidad del JPEG. El siguiente ejemplo solicita una imagen de anchura de 480 píxeles y calidad media:

`http://localhost:4502/content/geometrixx/adaptiveImage.adapt.480.MEDIUM.jpg`

**Propiedades de imagen admitidas**

El servlet acepta un número finito de anchos y cualidades de imagen. Los siguientes anchos son compatibles de forma predeterminada (en píxeles):

* completa
* 320
* 480
* 476
* 620

El valor completo indica que no se ha realizado ninguna escala.

Se admiten los siguientes valores para la calidad del JPEG:

* BAJO
* MEDIO
* ALTO

Los valores numéricos son 0,4, 0,82 y 1,0, respectivamente.

**Cambio de los anchos predeterminados admitidos**

Utilice la consola web ([http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)) o un nodo sling:OsgiConfig para configurar los anchos compatibles del servlet del componente de imagen adaptable de Adobe CQ.

Para obtener información sobre cómo configurar AEM servicios, consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md).

<table>
 <tbody>
  <tr>
   <th> </th>
   <th>Consola web</th>
   <th>sling:OsgiConfig</th>
  </tr>
  <tr>
   <th>Servicio o nombre de nodo</th>
   <td>El nombre de servicio de la ficha Configuración es Servlet de componente de imagen adaptable de Adobe CQ</td>
   <td>com.day.cq.wcm.foundation.impl. AdaptiveImageComponentServlet</td>
  </tr>
  <tr>
   <th>Propiedad</th>
   <td><p>Anchos admitidos</p>
    <ul>
     <li>Para añadir una anchura compatible, haga clic en un botón + e introduzca un número entero positivo.</li>
     <li>Para eliminar una anchura compatible, haga clic en el botón - asociado.</li>
     <li>Para modificar una anchura admitida, edite el valor del campo.</li>
    </ul> </td>
   <td><p>adapt.supported.widths</p>
    <ul>
     <li>La propiedad es un valor de cadena multivalor.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

#### Detalles de implementación {#implementation-details}

La variable `com.day.cq.wcm.foundation.impl.AdaptiveImageComponentServlet` amplía la [AbstractImageServlet](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) Clase . El código fuente AdaptiveImageComponentServlet se encuentra en la variable `/libs/foundation/src/impl/src/com/day/cq/wcm/foundation/impl` carpeta.

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

El servlet utiliza la anotación SCR de propiedad para establecer la calidad y las dimensiones de la imagen admitidas por defecto.

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

La variable `AbstractImageServlet` proporciona la variable `doGet` método que procesa la solicitud HTTP. Este método determina el recurso asociado a la solicitud, recupera las propiedades de los recursos del repositorio y las devuelve en un [ImageContext](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html) objeto.

>[!NOTE]
>
>La variable [com.day.cq.commons.DownloadResource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/DownloadResource.html) proporciona la variable `getFileReference method`, que recupera el valor de la variable `fileReference` propiedad.

La variable `AdaptiveImageComponentServlet` la clase anula la función `createLayer` método. El método obtiene la ruta del recurso de imagen y la anchura de la imagen solicitada desde el `ImageContext` objeto. A continuación, llama a los métodos de la variable `info.geometrixx.commons.impl.AdaptiveImageHelper` que realiza el escalado real de la imagen.

La clase AdaptiveImageComponentServlet también anula el método writeLayer. Este método aplica la calidad de JPEG a la imagen.

### Servlet de modificación de referencia de imagen (Geometrixx común) {#image-reference-modification-servlet-geometrixx-common}

El servlet de modificación de referencia de imagen de ejemplo genera atributos de tamaño para que el elemento img escale una imagen en la página web.

#### Llamada al servlet {#calling-the-servlet}

El servlet está enlazado a `cq:page` y admite la extensión de archivo .jpg . El selector de servlet es `image`. Por lo tanto, Sling resuelve las URL de solicitud HTTP del siguiente formato para este servlet:

`path-to-page-node.image.jpg`

Por ejemplo, Sling reenvía solicitudes HTTP con la dirección URL `http://localhost:4502/content/geometrixx/en.image.jpg` al servlet de modificación de referencia de imagen.

Tres selectores adicionales especifican la anchura, la altura y la calidad de la imagen solicitada (opcionalmente). En el siguiente ejemplo se solicita una imagen de anchura de 770 píxeles, altura de 360 píxeles y calidad media.

`http://localhost:4502/content/geometrixx/en.image.770.360.MEDIUM.jpg`

**Propiedades de imagen admitidas**

El servlet acepta un número finito de dimensiones de imagen y valores de calidad.

Los siguientes valores son compatibles de forma predeterminada (widthxheight):

* 256x192
* 370x150
* 480 x 200
* 127x127
* 770x360
* 620x290
* 480x225
* 320x150
* 375x175
* 303x142
* 1170x400
* 940x340
* 770x300
* 480x190

Se admiten los siguientes valores para la calidad de imagen:

* baja
* mediano
* alto

Al trabajar con AEM, existen varios métodos para administrar los ajustes de configuración de dichos servicios; see [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información.

#### Especificación del recurso de imagen {#specifying-the-image-resource}

La ruta de la imagen, las dimensiones y los valores de calidad deben almacenarse como propiedades de un nodo en el repositorio:

* El nombre del nodo es `image`.
* El nodo principal es el `jcr:content` nodo de a `cq:page` recurso.

* La ruta de la imagen se almacena como el valor de una propiedad denominada `fileReference`.

Al crear una página, utilice **Barra de tareas** para especificar la imagen y agregar la variable `image` a las propiedades de la página:

1. En **Barra de tareas**, haga clic en **Página** y, a continuación, haga clic en **Propiedades de página**.
1. Haga clic en el **Imagen** y especifique la imagen.
1. Haga clic en **Aceptar**.

#### Detalles de implementación {#implementation-details-1}

La clase info.geometrixx.commons.impl.servlets.ImageReferenceModificationServlet amplía la [AbstractImageServlet](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) Clase . Si tiene instalado el paquete cq-geometrixx-commons-pkg, el código fuente ImageReferenceModificationServlet se encuentra en la variable `/apps/geometrixx-commons/src/core/src/main/java/info/geometrixx/commons/impl/servlets` carpeta.

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

El servlet utiliza la anotación SCR de propiedad para establecer la calidad y las dimensiones de la imagen admitidas por defecto.

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

La variable `AbstractImageServlet` proporciona la variable `doGet` método que procesa la solicitud HTTP. Este método determina el recurso asociado a la llamada, recupera las propiedades de los recursos del repositorio y las guarda en un [ImageContext](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html) objeto.

La variable `ImageReferenceModificationServlet` la clase anula la función `createLayer` e implementa la lógica que determina el recurso de imagen que se va a procesar. El método recupera un nodo secundario del nodo de la página `jcr:content` nodo llamado `image`. Un [Imagen](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/foundation/Image.html) el objeto se crea a partir de esta `image` y el `getFileReference` devuelve la ruta al archivo de imagen desde el `fileReference` propiedad del nodo de imagen.

>[!NOTE]
>La variable [com.day.cq.commons.DownloadResource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/DownloadResource.html) proporciona el método getFileReferencemod.

## Desarrollo de una cuadrícula fluida {#developing-a-fluid-grid}

AEM le permite implementar redes fluidas de forma eficiente y eficaz. En esta página se explica cómo integrar la cuadrícula fluida o una implementación de cuadrícula existente (por ejemplo, [Bootstrap](https://github.com/topics/twitter-bootstrap?l=css)) en la aplicación de AEM.

Si no está familiarizado con las cuadrículas de fluidos, consulte la sección [Introducción a las cuadrículas fluidas](/help/sites-developing/responsive.md#developing-a-fluid-grid) en la parte inferior de esta página. Esta introducción proporciona una visión general de las cuadrículas fluidas y una guía para diseñarlas.

### Definición de la cuadrícula mediante un componente Página {#defining-the-grid-using-a-page-component}

Utilice los componentes de página para generar los elementos de HTML que definen los bloques de contenido de la página. ClientLibraryFolder al que hace referencia la página proporciona el CSS que controla el diseño de los bloques de contenido:

* Componente de página: Agrega elementos div que representan filas de bloques de contenido. Los elementos div que representan bloques de contenido incluyen un componente parsys donde los autores añaden contenido.
* Carpeta de biblioteca de cliente: Proporciona el archivo CSS que incluye consultas de medios y estilos para los elementos div.

Por ejemplo, la aplicación geometrixx-media de ejemplo contiene el componente media-home. Este componente de página inserta dos secuencias de comandos, que generan dos `div` elementos de la clase `row-fluid`:

* La primera fila contiene un `div` elemento de clase `span12` (el contenido ocupa 12 columnas). La variable `div` contiene el componente parsys.

* La segunda fila contiene dos `div` elementos, uno de la clase `span8` y el otro de clase `span4`. Cada `div` incluye el componente parsys.

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
>Cuando un componente incluye varios `cq:include` elementos que hacen referencia al componente parsys, cada `path` debe tener un valor diferente.

#### Escalado de la cuadrícula del componente Página {#scaling-the-page-component-grid}

El diseño asociado al componente de página de medios de geometrixx (`/etc/designs/geometrixx-media`) contiene el `clientlibs` ClientLibraryFolder. Esta ClientLibraryFolder define estilos CSS para `row-fluid` clases, `span*` clases y `span*` clases que son hijos de `row-fluid` clases . Las consultas de medios permiten redefinir estilos para diferentes tamaños de ventanilla.

El siguiente ejemplo de CSS es un subconjunto de esos estilos. Este subconjunto se centra en `span12`, `span8`y `span4` clases y consultas de medios para dos tamaños de ventanilla. Observe las siguientes características de la CSS:

* La variable `.span` los estilos definen los anchos de los elementos utilizando números absolutos.
* La variable `.row-fluid .span*` los estilos definen los anchos de elemento como porcentajes del elemento principal. Los porcentajes se calculan a partir de los anchos absolutos.
* Las consultas de medios para ventanillas más grandes asignan anchos absolutos más grandes.

>[!NOTE]
>
>El ejemplo de Geometrixx Medias integra el [Bootstrap](https://getbootstrap.com/2.0.2/) Marco de JavaScript en su implementación de cuadrícula fluida. El marco del Bootstrap proporciona el archivo bootstrap.css.

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

#### Cambio de posición del contenido en la cuadrícula de componentes Página {#repositioning-content-in-the-page-component-grid}

Las páginas de la aplicación de Geometrixx Medias de ejemplo distribuyen filas de bloques de contenido horizontalmente en ventanillas amplias. En ventanillas más pequeñas, los mismos bloques se distribuyen verticalmente. El siguiente ejemplo de CSS muestra los estilos que implementan este comportamiento para el código de HTML que genera el componente de página principal de medios:

* El CSS predeterminado para la página de bienvenida de medios asigna la variable `float:left` estilo para `span*` clases que están dentro `row-fluid` clases .

* Las consultas de medios para ventanillas más pequeñas asignan la variable `float:none` para las mismas clases.

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

#### Modularizar los componentes de la página {#tip-modularize-your-page-components}

Modularizar los componentes para que pueda utilizar el código de forma eficaz. Es probable que el sitio utilice varios tipos diferentes de páginas, como una página de bienvenida, una página de artículos o una página de productos. Cada tipo de página contiene diferentes tipos de contenido y es probable que use diferentes diseños. Sin embargo, cuando ciertos elementos de cada diseño son comunes en varias páginas, puede reutilizar el código que implementa esa parte del diseño.

**Usar superposiciones de componentes de página**

Cree un componente de página principal que proporcione secuencias de comandos para generar las distintas partes de una página, como `head` y `body` secciones y `header`, `content`y `footer` dentro del cuerpo.

Cree otros componentes de página que utilicen el componente de página principal como el `cq:resourceSuperType`. Estos componentes incluyen secuencias de comandos que anulan las secuencias de comandos de la página principal según sea necesario.

Por ejemplo, la aplicación goemetrixx-media incluye el componente de página (el `sling:resourceSuperType` es el componente de página base). Varios componentes secundarios (como artículo, categoría y media-home) utilizan este componente de página como el `sling:resourceSuperType`. Cada componente secundario incluye un archivo content.jsp que anula el archivo content.jsp del componente de página.

**Reutilización de scripts**

Cree varios scripts JSP que generen combinaciones de filas y columnas que son comunes en varios componentes de página. Por ejemplo, la variable `content.jsp` la secuencia de comandos del artículo y los componentes media-home hacen referencia a la variable `8x4col.jsp` secuencia de comandos.

**Organizar estilos CSS según el tamaño de la ventanilla de destino**

Incluya estilos CSS y consultas de medios para diferentes tamaños de ventanilla en archivos independientes. Utilice carpetas de la biblioteca del cliente para concatenarlas.

### Inserción de componentes en la cuadrícula de la página {#inserting-components-into-the-page-grid}

Cuando los componentes generan un solo bloque de contenido, generalmente la cuadrícula que establece el componente de página controla la ubicación del contenido.

Como autor, el bloque de contenido se puede representar en varios tamaños y posiciones relativas. El texto del contenido no debe utilizar direcciones relativas para hacer referencia a otros bloques de contenido.

Si es necesario, el componente debe proporcionar todas las bibliotecas CSS o JavaScript necesarias para el código de HTML que genera. Utilice una carpeta de biblioteca de cliente dentro del componente para que se generen los archivos CSS y JS. Para exponer los archivos, [crear una dependencia o incrustar la biblioteca](/help/sites-developing/clientlibs.md#creating-client-library-folders) en otra carpeta de biblioteca de cliente debajo de la carpeta /etc.

**Subcuadrículas**

Si el componente contiene varios bloques de contenido, añada los bloques de contenido dentro de una fila para establecer una subcuadrícula en la página:

* Utilice los mismos nombres de clase que el componente de página que contiene para poder expresar elementos div como filas y bloques de contenido.
* Para anular el comportamiento que implementa el CSS del diseño de página, utilice un nombre de segunda clase para el elemento div de fila y proporcione el CSS asociado en una carpeta de biblioteca de cliente.

Por ejemplo, la variable `/apps/geometrixx-media/components/2-col-article-summary` genera dos columnas de contenido. El HTML que genera tiene la siguiente estructura:

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

La variable `.row-fluid .span6` selectores de la CSS de la página se aplica al `div` elementos de la misma clase y estructura de este HTML. Sin embargo, el componente también incluye la carpeta de biblioteca cliente /apps/geometrixx-media/components/2-col-article-summary/clientlibs:

* El CSS utiliza las mismas consultas de medios que el componente de página para establecer cambios en el diseño en los mismos anchos de página discretos.
* Los selectores utilizan la variable `multi-col-article-summary` clase de la fila `div` para anular el comportamiento de la página `row-fluid` Clase .

Por ejemplo, los siguientes estilos se incluyen en el `/apps/geometrixx-media/components/2-col-article-summary/clientlibs/css/responsive-480px.css` archivo:

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

## Introducción a las cuadrículas de fluidos {#introduction-to-fluid-grids}

Las cuadrículas fluidas permiten que los diseños de página se adapten a las dimensiones de la ventanilla del cliente. Las cuadrículas constan de columnas lógicas y filas que colocan los bloques de contenido en la página.

* Las columnas determinan las posiciones horizontales y los anchos de los bloques de contenido.
* Las filas determinan las posiciones verticales relativas de los bloques de contenido.

Con la tecnología HTML5, puede implementar la cuadrícula y manipularla para adaptar los diseños de página a diferentes tamaños de ventanilla:

* HTML `div` contienen bloques de contenido que abarcan algunas columnas.
* Uno o más de estos elementos div comprenden una fila cuando comparten un elemento div principal común.

### Uso de anchos discretos {#using-discrete-widths}

Para cada rango de anchuras de las ventanillas móviles objetivo, utilice un ancho de página estático y bloques de contenido de ancho constante. Al cambiar manualmente el tamaño de una ventana del explorador, los cambios en el tamaño del contenido se producen con anchos de ventana discretos (también conocidos como puntos de interrupción). Por lo tanto, los diseños de página se respetan más estrictamente, lo que maximiza la experiencia del usuario.

#### Escalado de la cuadrícula {#scaling-the-grid}

Utilice cuadrículas para escalar bloques de contenido y adaptarse a diferentes tamaños de ventanilla. Los bloques de contenido abarcan un número específico de columnas. A medida que los anchos de columna aumentan o disminuyen para adaptarse a diferentes tamaños de ventanilla, los anchos de los bloques de contenido aumentan o disminuyen en consecuencia. El escalado puede admitir ventanillas grandes y medianas lo suficientemente anchas como para adaptarse a la colocación paralela de bloques de contenido.

![](do-not-localize/chlimage_1-1a.png)

#### Cambio de posición del contenido en la cuadrícula {#repositioning-content-in-the-grid}

El tamaño de los bloques de contenido puede estar limitado por una anchura mínima, por encima de la cual el escalado ya no es efectivo. Para ventanillas más pequeñas, la cuadrícula se puede utilizar para distribuir bloques de contenido verticalmente en lugar de horizontalmente.

![](do-not-localize/chlimage_1-2a.png)

### Diseño de la cuadrícula {#designing-the-grid}

Determine las columnas y filas en las que debe colocar los bloques de contenido en las páginas. Los diseños de página determinan el número de columnas y filas que abarcan la cuadrícula.

**Número de columnas**

Incluya suficientes columnas para colocar horizontalmente los bloques de contenido en todos los diseños, para todos los tamaños de las ventanillas móviles. Utilice más columnas de las que necesita actualmente para poder dar cabida a futuros diseños de página.

**Contenido de fila**

Utilice filas para controlar la posición vertical de los bloques de contenido. Determine los bloques de contenido que comparten la misma fila:

* Los bloques de contenido que se encuentran uno al lado del otro horizontalmente en cualquiera de los diseños están en la misma fila.
* Los bloques de contenido que se encuentran uno junto al otro horizontalmente (ventanillas más anchas) y verticalmente (ventanillas más pequeñas) se encuentran en la misma fila.

### Implementaciones de cuadrícula {#grid-implementations}

Cree clases y estilos CSS para poder controlar el diseño de los bloques de contenido en una página. Los diseños de página a menudo se basan en el tamaño y la posición relativos de los bloques de contenido dentro de la ventanilla. La ventanilla determina el tamaño real de los bloques de contenido. El CSS debe tener en cuenta los tamaños relativo y absoluto. Puede implementar una cuadrícula fluida mediante tres tipos de clases CSS:

* Una clase para un `div` elemento que es un contenedor para todas las filas. Esta clase define la anchura absoluta de la cuadrícula.
* Una clase para `div` elementos que representan una fila. Esta clase controla la posición horizontal o vertical de los bloques de contenido que contiene.
* Clases para `div` elementos que representan bloques de contenido de distintas anchuras. Los anchos se expresan como un porcentaje del elemento principal (la fila).

Los anchos de las ventanillas de destino (y sus consultas de medios asociadas) delimitan los anchos discretos que se utilizan para un diseño de página.

#### Anchura de bloques de contenido {#widths-of-content-blocks}

En general, la variable `width` los estilos de las clases de bloques de contenido se basan en las siguientes características de la página y la cuadrícula:

* El ancho de página absoluto que utiliza para cada tamaño de ventanilla objetivo. Valores conocidos.
* Ancho absoluto de las columnas de la cuadrícula para cada ancho de página. Estos valores se determinan.
* Ancho relativo de cada columna como porcentaje del ancho total de la página. Estos valores se calculan.

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

Utilice el siguiente algoritmo como punto de partida para desarrollar las clases de elementos y los estilos CSS de sus páginas.

1. Defina un nombre de clase para el elemento div que contiene todas las filas, por ejemplo `content.`
1. Defina una clase CSS para elementos div que representen filas, como `row-fluid`.
1. Defina nombres de clase para elementos de bloque de contenido. Se requiere una clase para todas las anchuras posibles, en términos de espacios de columna. Por ejemplo, use el `span3` clase para `div` elementos que abarcan tres columnas, utilice `span4` clases para espacios de cuatro columnas. Defina tantas clases como columnas de la cuadrícula.

1. Para cada tamaño de ventanilla móvil objetivo, agregue la consulta de medios correspondiente al archivo CSS. Agregue los siguientes elementos en cada consulta de medios:

   * Un selector para la variable `content` class, por ejemplo `.content{}`.
   * Selectores para cada clase span, por ejemplo `.span3{ }`.
   * Un selector para la variable `row-fluid` class, por ejemplo `.row-fluid{ }`
   * Selectores para clases span que están dentro de clases de fluidos de fila, por ejemplo `.row-fluid span3 { }`.

1. Agregar estilos de anchura para cada selector:

   1. Establezca la anchura de `content` selectores con el tamaño absoluto de la página, por ejemplo `width:480px`.
   1. Defina la anchura de todos los selectores de fluidos de fila en 100%.
   1. Defina la anchura de todos los selectores de span con la anchura absoluta del bloque de contenido. Una cuadrícula trivial utiliza columnas distribuidas uniformemente de la misma anchura: `(absolute width of page)/(number of columns)`.
   1. Defina la anchura de la variable `.row-fluid .span` selectores como porcentaje de la anchura total. Calcule esta anchura utilizando la variable `(absolute span width)/(absolute page width)*100` fórmula.

#### Colocación de bloques de contenido en filas {#positioning-content-blocks-in-rows}

Utilice el estilo flotante de la variable `.row-fluid` para que pueda controlar si los bloques de contenido de una fila están organizados horizontal o verticalmente.

* La variable `float:left` o `float:right` este estilo produce la distribución horizontal de elementos secundarios (bloques de contenido).

* La variable `float:none` el estilo de crea una distribución vertical de los elementos secundarios.

Añada el estilo al `.row-fluid` dentro de cada consulta de medios. Establezca el valor según el diseño de página que esté utilizando para esa consulta de medios. Por ejemplo, el diagrama siguiente ilustra una fila que distribuye el contenido horizontalmente para ventanillas móviles anchas y verticalmente para ventanillas móviles.

![](do-not-localize/chlimage_1-3a.png)

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

Para el diseño de página de cada tamaño de ventanilla objetivo, determine el número de columnas que ocupa cada bloque de contenido. A continuación, determine qué clase utilizar para los elementos div de esos bloques de contenido.

Cuando haya establecido las clases div, puede implementar la cuadrícula mediante la aplicación AEM.
