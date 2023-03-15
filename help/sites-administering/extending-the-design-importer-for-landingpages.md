---
title: Ampliación y configuración del importador de diseños para páginas de destino
seo-title: Extending and Configuring the Design Importer for Landing Pages
description: Obtenga información sobre cómo configurar el Importador de diseños para páginas de aterrizaje.
seo-description: Learn how to configure the Design Importer for landing pages.
uuid: a2dd0c30-03e4-4e52-ba01-6b0b306c90fc
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e02f5484-fbc2-40dc-8d06-ddb53fd9afc2
docset: aem65
exl-id: 1b8c6075-13c6-4277-b726-8dea7991efec
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '3503'
ht-degree: 62%

---

# Ampliación y configuración del importador de diseños para páginas de destino{#extending-and-configuring-the-design-importer-for-landing-pages}

Esta sección describe cómo configurar y, si se desea, ampliar el importador de diseños para las páginas de aterrizaje. El trabajo con las páginas de aterrizaje después de la importación se trata en [Páginas de aterrizaje.](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)

**Cómo hacer que el importador de diseños extraiga su componente personalizado**

Estos son los pasos lógicos para que el importador de diseños reconozca su componente personalizado

1. Crear un TagHandler

   * Un controlador de tags en un POJO que gestiona tags HTML de un tipo específico. El &quot;tipo&quot; de HTML que TagHandler puede gestionar se define mediante la propiedad OSGi de TagHandlerFactory &quot;tagpattern.name&quot;. La propiedad OSGi es un regex que debería coincidir con la tag HTML de entrada que desee gestionar. Todas las tags anidadas se enviarán al controlador de tags para que las gestione. Por ejemplo, si se registra en un div que contiene un anidado &lt;p> , la etiqueta &lt;p> La etiqueta de también se lanzaría a su TagHandler y depende de usted cómo desee encargarse de ella.
   * La interfaz del controlador de tags es similar a la interfaz del controlador de contenido SAX. Recibe eventos SAX para cada tag HTML. Como autor del controlador de tags, deberá implementar ciertos métodos de ciclo de vida invocados automáticamente por la estructura del importador de diseños.

1. Cree su TagHandlerFactory correspondiente.

   * La fábrica del controlador de tags es un componente OSGi (singleton) responsable de generar instancias de su controlador de tags.
   * el generador del controlador de etiquetas debe exponer una propiedad OSGi llamada &quot;tagpattern.name&quot; cuyo valor coincida con la etiqueta html de entrada.
   * Si hay varios controladores de tag que coinciden con la tag HTML de entrada, se elige el que tenga una clasificación superior. La propia clasificación se expone como una propiedad OSGi **service.ranking**.
   * TagHandlerFactory es un componente OSGi. Deberá suministrar todas las referencias al TagHandler mediante esta fábrica.

1. Asegúrese de que TagHandlerFactory tenga una mejor clasificación si desea anular el valor predeterminado.

>[!CAUTION]
>
>El Importador de diseños que se usa para importar páginas de aterrizaje [está en desuso en AEM 6.5](/help/release-notes/deprecated-removed-features.md#deprecated-features).

## Preparar el HTML para su importación {#preparing-the-html-for-import}

Después de crear una página de importador, puede importar la página de aterrizaje completa del HTML. Para importar su página de aterrizaje HTML, primero debe comprimir su contenido en un paquete de diseño. El paquete de diseño contiene la página de aterrizaje HTML y los recursos a los que hace referencia (imágenes, css, iconos, scripts, etc.).

La hoja de trucos siguiente le muestra cómo preparar el HTML para la importación:

Hoja de características clave de página de aterrizaje

[Obtener archivo](assets/cheatsheet.zip)

### Diseño y requisitos del archivo comprimido {#zip-file-layout-and-requirements}

>[!NOTE]
>
>Los archivos comprimidos solo pueden contener una parte de una página o una página HTML.

A continuación se muestra un ejemplo de diseño de archivo comprimido:

* /index.html -> archivo HTML de página de aterrizaje
* /css -> para agregar a la clientlib de CSS
* /img -> todas las imágenes y recursos
* /js -> para agregarlo a la clientlib de JS

El diseño se basa en el diseño de las recomendaciones HTML5 Boilerplate. Más información en [https://html5boilerplate.com/](https://html5boilerplate.com/)

>[!NOTE]
>
>Como mínimo, el paquete de diseño **debe** contener un **index.html** en el nivel raíz. En caso de que la página de aterrizaje que se va a importar también tenga una versión móvil, el zip debe contener un **mobile.index.html** junto con **index.html** en el nivel raíz.

### Preparación del HTML de la página de aterrizaje {#preparing-the-landing-page-html}

Para poder importar el HTML, debe añadir un div lienzo al HTML de la página de aterrizaje.

El div lienzo es un html **div** con `id="cqcanvas"` que debe insertarse dentro del HTML `<body>` y deben envolver el contenido que se va a convertir.

A continuación se muestra un ejemplo de fragmento de HTML de página de lanzamiento tras añadir el div lienzo:

```xml
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title></title>
  <meta name="description" content="">
</head>
<body>
 <div id="cqcanvas">
  <!-- HTML content intended for conversion -->
 </div>
</body>
</html>
```

### Preparación del HTML para incluir componentes de AEM editables {#preparing-the-html-to-include-editable-aem-components}

Al importar una página de aterrizaje, puede elegir importarla tal cual, lo que significa que, tras importarla, no podrá modificar ninguno de los elementos importados en AEM (pero podrá añadir componentes de AEM adicionales a la página).

Es posible que, antes de importar la página de aterrizaje, desee convertir ciertas partes de la página de aterrizaje en componentes de AEM editables. Esto le permite editar con rapidez partes de la página de aterrizaje incluso tras importar el diseño de dicha página.

Para ello, añada el `data-cq-component` al componente apropiado del archivo HTML que desee importar.

En la sección siguiente se describe cómo editar su archivo HTML para poder convertir ciertas partes de sus páginas de aterrizaje en diferentes componentes de AEM editables. Los componentes se describen en detalle en [Componentes de páginas de aterrizaje](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md).

>[!NOTE]
>
>El código HTML que se utiliza para convertir partes de la página de aterrizaje en componentes de AEM tiene una forma larga y una declaración abreviada de tag. Ambas se describen para cada componente.

### Restricciones {#limitations}

Antes de importar, tenga en cuenta las restricciones siguientes:

### Los atributos como class o id aplicados a &amp;lt;body> etiqueta no se conserva {#any-attribute-like-class-or-id-applied-on-the-amp-lt-body-tag-is-not-preserved}

Si se aplica algún atributo como id o class en la etiqueta body, por ejemplo `<body id="container">` a continuación, no se conserva después de la importación. Por lo tanto, el diseño que se esté importando no debería depender de los atributos aplicados en la `<body>` etiqueta.

### Arrastre y colocación del archivo comprimido {#drag-and-drop-zip}

La carga ZIP de arrastrar y soltar no es compatible con Internet Explorer y Firefox versiones 3.6 y anteriores. Para cargar un diseño con estos navegadores, haga clic en la zona en la que desea soltar los archivos para abrir un cuadro de diálogo de carga de archivos y cargar el diseño.

Los navegadores que admiten el &quot;arrastre y suelte&quot; del zip de diseño son Chrome, Safari5.x, Firefox 4 y posteriores.

### No se admite Modernizr {#modernizr-is-not-supported}

`Modernizr.js` es una herramienta basada en javascript que detecta capacidades nativas de los navegadores y determina si son o no adecuadas para elementos HTML5. Los diseños que utilizan Modernizr para mejorar la compatibilidad con versiones anteriores de diferentes navegadores pueden causar problemas de importación en la solución de página de aterrizaje. No se admiten los scripts de `Modernizr.js` con el importador de diseños.

### No se conservan las propiedades de página cuando se importa un paquete de diseño {#page-properties-are-not-preserved-at-the-time-of-importing-design-package}

Todas las propiedades de página (e.g. dominio personalizado, aplicación de HTTPS, etc.) definidas antes de importar el paquete de diseño para una página que utilice la plantilla de página de aterrizaje en blanco se perderán tras la importación del diseño. Por lo tanto, se recomienda definir las propiedades de página tras importar el paquete de diseño.

### Se supone un marcado solo de HTML {#html-only-markup-assumed}

Tras la importación, el marcado se corrige por motivos de seguridad y para evitar la importación y publicación del marcado que no sea válido. Debido a ello, el marcado que sea solo HTML y cualquier otra forma de elemento, como el SVG incorporado o los componentes web se eliminarán.

### Texto {#text}

Código HTML para insertar un componente de texto (`foundation/components/text`) en el HTML dentro del paquete de diseño:

```xml
<div data-cq-component="text"> <p>This is some editable text</p> </div>
```

Si se incluye el código anterior en el HTML, ocurrirá lo siguiente:

* AEM Crea un componente de texto editable de la ( `sling:resourceType=foundation/components/text`) en la página de aterrizaje creada después de importar el paquete de diseño.
* Se define la propiedad `text` del componente de texto creado en el HTML delimitado por el `div`.

**Declaración abreviada de tag de componente**:

```xml
<p data-cq-component="text">Text component shorthand</p>
```

**Texto con una lista**

Para añadir texto con una lista:

* 1º
* 2º

que puede editarse en el editor RTE:

```xml
<div data-cq-component="text"><p>This is text with a list:</p><ul><li>1st</li><li>2nd</li></ul><p>It can be edited with the RTE editor</p></div>
```

**Texto con color**

Para añadir texto con color (rosa) que puede editarse en el editor RTE:

```xml
<div class="pink" data-cq-component="text"><p>This is pink text.</p><p>It can be edited with the RTE editor</p></div>
```

### Título {#title}

Marcado del HTML para insertar un componente de título ( `wcm/landingpage/components/title`) en el HTML dentro del paquete de diseño:

```xml
<div data-cq-component="title"> <h1>This is some editable title text</h1> </div>
```

Si se incluye el código anterior en el HTML, ocurrirá lo siguiente:

* AEM Crea un componente de título editable de la ( `sling:resourceType=wcm/landingpage/components/title`) en la página de aterrizaje creada después de importar el paquete de diseño.
* La propiedad`jcr:title`   del componente de título creado se configurará en el texto dentro de la tag de encabezado encerrada en el div.
* La propiedad `type` se configurará en la tag de encabezado, en este caso `h1`.

El componente de título admite 7 tipos: `h1, h2, h3, h4, h5, h6` y `default`.

**Declaración abreviada de tag de componente**:

```xml
<h1 data-cq-component="title">Title component shorthand</h1>
```

### Imagen {#image}

Código HTML para insertar un componente de imagen (foundation/components/image) en el HTML dentro del paquete de diseño:

```xml
<div data-cq-component="image">
<img src="img/video1.png" alt="Video about Polar Brake Goggles in action" title="Polar Brake Goggles" width="300" height="200" />
</div>
```

Si se incluye el código anterior en el HTML, ocurrirá lo siguiente:

* AEM Crea un componente de imagen editable de la ( `sling:resourceType=foundation/components/image`) en la página de aterrizaje creada después de importar el paquete de diseño.
* La propiedad `fileReference` del componente de imagen creado se configurará en la ruta en la que se importará la imagen especificada en el atributo src.
* Establece el `alt` propiedad al valor del atributo alt en la etiqueta img.
* Establece el `title` propiedad al valor del atributo title en la etiqueta img.
* Establece el `width` propiedad al valor del atributo width en la etiqueta img.
* Establece el `height` propiedad al valor del atributo height en la etiqueta img.

**Declaración abreviada de tag de componente:**

```xml
<img data-cq-component="image" src="test.png" alt="Image component shorthand"/>
```

#### No se admite img src de URL absoluta dentro del div del componente imagen {#absolute-url-img-src-not-supported-within-image-component-div}

Si un `<img>` se intenta la conversión de componentes con una src de url absoluta, una opción apropiada **UnsupportedTagContentException** se ha elevado. Por ejemplo, no se admite lo siguiente:

`<div data-cq-component="image">`

`<img src="https://cdn.printfriendly.com/pf-button.gif" alt="Print Friendly and PDF"/>`

`</div>`

Aparte de esto, se admiten las imágenes de URL absoluta para las tags img que no formen parte del div componente de imagen.

### Componentes de llamada a acción {#call-to-action-components}

Puede marcar parte de la página de aterrizaje para importarla como un &quot;componente editable de llamada a la acción&quot;; estos componentes importados se pueden editar después de importar la página de aterrizaje. AEM incluye los componentes de llamada a acción siguientes:

* Vínculo de pulsaciones: le permite añadir un vínculo de texto que dirigirá al visitante a la URL de destino cuando haga clic en él.
* Vínculo gráfico: le permite añadir una imagen que dirigirá al visitante a una URL de destino cuando haga clic en ella.

#### Vínculo de pulsaciones {#click-through-link}

Este componente de llamada a acción puede utliizarse para añadir un vínculo de texto en la página de aterrizaje.

Propiedades admitidas

* Etiqueta, con opciones en negrita, cursiva y subrayada
* URL de destino, admite URL de AEM y de terceros
* Opciones de procesamiento de página (misma ventana, nueva ventana, etc.)

La tag HTML debe incluir el componente de pulsaciones en el archivo comprimido importado. Aquí href se asigna a la dirección URL de destino, &quot;Ver detalles del producto&quot; se asigna a la etiqueta, etc.

```xml
<div id="cqcanvas">
.
.
                <div data-cq-component="clickThroughLink">
        <a href="/content/we-retail/us/en/products/equipment/snow-sports/flying-snowboard.html">View Product Details  ></a>
  </div>
.
.
</div>
```

Este componente puede utilizarse en cualquier aplicación independiente o importarse de un archivo comprimido.

**Declaración abreviada de tag de componente**:

```xml
<a href="/somelink.html" data-cq-component="clickThroughLink">Click Through Link shorthand</a>
```

#### Vínculo gráfico {#graphical-link}

Este componente de llamada a acción puede utilizarse para añadir imágenes gráficas con un vínculo en la página de aterrizaje. La imagen puede ser un botón simple o cualquier imagen gráfica como fondo. Cuando se hace clic en la imagen, se llevará al usuario a una URL de destino especificada en las propiedades de componente. Forma parte del grupo &quot;Llamada a acción&quot;.

Propiedades admitidas

* Rotación, recorte de imágenes
* Texto por pase, descripción tamaño en píxeles
* URL de destino, admite URL de AEM y de terceros
* Opciones de procesamiento de página (misma ventana, nueva ventana, etc.)

Tag HTML para incluir un componente de vínculo gráfico en el archivo comprimido importado. Aquí href se asignará a la dirección URL de destino, img src será la imagen de renderización, &quot;título&quot; se tomará como texto de desplazamiento, etc.

```xml
<div id="cqcanvas">
  <div data-cq-component="clickThroughGraphicalLink"><a href="https://www.adobe.com/go/wem"><img src="img/call-to-action-button.png" title="Click Here to Learn More" /></a></div>
</div>
```

**Declaración abreviada de tag de componente**:

```xml
<a href="/somelink.html" data-cq-component="clickThroughGraphicalLink"><img src="linkimage.png" alt="Click Through Graphical Link shorthand"/></a>
```

>[!NOTE]
>
>Para crear un vínculo gráfico de pulsaciones, debe envolver una etiqueta de anclaje y la etiqueta de imagen dentro de un div con `data-cq-component="clickthroughgraphicallink"` atributo.
>
>p. ej.`<div data-cq-component="clickthroughlink"> <a href="https://myURLhere/"><img src="image source here"></a> </div>`
>
>No se admiten otros métodos para asociar una imagen con una tag de anclaje mediante CSS; por ejemplo, el código siguiente no funcionará:
>
>`<div data-cq-component="clickthroughgraphicallink">`
>
>`<a class="hasBackground" href="https://myURLhere/"></a>`
>
>`</div>`
>
>con un asociado `css .hasbackground { background-image: pathtoimage }`

### Formulario de posibles clientes {#lead-form}

Los formularios de posibles clientes se utilizan para recopilar información de perfil de un visitante o posible cliente. Dicha información puede guardarse y utilizarse posteriormente para realizar campañas de marketing eficaces basadas en la información. Esta información suele incluir título, nombre, correo electrónico, fecha de nacimiento, dirección, intereses, etc. Forma parte del grupo &quot;Formulario de posible cliente de CTA&quot;.

**Funciones admitidas**

* Campos de posibles clientes predefinidos: nombre, apellido, dirección, dob, sexo, acerca de, userId, emailId, botón de envío están disponibles en la barra de tareas. Tan solo tiene que arrastrar y soltar el componente deseado en el formulario de posibles clientes.
* Con estos componentes, se puede diseñar un formulario de posibles clientes independiente; estos campos corresponden con los campos del formulario de posibles clientes. En las aplicaciones independientes o de archivos comprimidos importados, el usuario puede añadir campos suplementarios mediante los campos de Llamada a acción: formulario de posibles clientes o cq:form, darles un nombre y diseñarlos como prefiera.
* Asigne campos de formulario de posibles clientes con nombres predefinidos específicos de formularios de posibles clientes de CTA, por ejemplo: firstName para el nombre en el formulario de posibles clientes, etc.
* Los campos que no se asignen a un formulario de posibles clientes se asignarán a componentes de cq:form: texto, botón de opción, casilla de verificación, menú desplegable, oculto, contraseña.
* El usuario puede proporcionar el título con la etiqueta &quot;label&quot; y puede proporcionar estilo utilizando el atributo de estilo &quot;class&quot; (solo disponible para componentes de formulario de posibles clientes de CTA).
* La página de agradecimiento y la lista de suscripción se pueden proporcionar como un parámetro oculto del formulario (presente en el index.htm) o se pueden agregar o editar desde la barra de edición de Inicio del formulario de posibles clientes

   &lt;input type=&quot;hidden&quot; name=&quot;redirectUrl&quot; value=&quot;/content/we-retail/en/user/register/thank_you&quot;/>

   &lt;input type=&quot;hidden&quot; name=&quot;groupName&quot; value=&quot;leadForm&quot;/>

* Las restricciones como - obligatorio se pueden proporcionar desde la configuración de edición de cada uno de los componentes.

Tag HTML para incluir un componente de vínculo gráfico en el archivo comprimido importado. Aquí, &quot;firstName&quot; se asigna al nombre del formulario principal y así sucesivamente, excepto para las casillas de verificación: estas dos casillas de verificación se asignan al componente desplegable cq:form.

```xml
<div id="cqcanvas">
   <div id="form_wrapper">
    <h2>NEWSLETTER SIGN UP</h2>
       <div data-cq-component="leadFormGeneration">
       <form method="post" action="#" onsubmit="return popupBox()">
       <label for="firstName" class="checkText">
        FIRST NAME
       </label><br />
       <input name="firstName" class="text pink" type="text" /><br />
       <label for="lastName" class="checkText">
        LAST NAME
       </label><br />
       <input name="lastName" class="text pink" type="text" /><br />
       <label for="emailId" class="checkText">
        EMAIL ADDRESS
       </label><br />
       <input name="emailId" class="text pink" type="text" /><br />

       <div class="checkboxes">
       <input type="checkbox" class="check" name="send_news" /> <label for="send_news" class="checkText">Send me the latest We.Retail news and announcements.</label><br />
       <input type="checkbox" class="check" name="send_offers" /> <label for="send_offers" class="checkText">Send me We.Retail deals and special offers.</label><br />
       </div>
       <input type="submit" name="submit" class="submit pink" value="Sign Up >" />
       </form>
     </div>
   </div>
```

### Parsys {#parsys}

El componente parsys de AEM es un componente contenedor que puede contener otros componentes de AEM. Es posible añadir un componente parsys al HTML importado, lo que permite al usuario añadir y eliminar componentes de AEM editables en la página de aterrizaje tras haberla importado.

El sistema de párrafos permite a los usuarios añadir componentes mediante la barra de tareas.

Código HTML para insertar un componente parsys (`foundation/components/parsys`) en el HTML del paquete de diseño:

```xml
<div data-cq-component="parsys">
   <div data-cq-component="title"><h2>ULTIMATE PROTECTION</h2></div>
        <div data-cq-component="title"><h3>ON SALE</h3></div>
</div>
```

Si se incluye el código anterior, pasará lo siguiente:

* Se insertará un componente parsys de AEM (foundation/components/parsys) en la página de aterrizaje creada tras importar el paquete de diseño.
* Se inicializará la barra de tareas con los componentes predeterminados. Se pueden arrastrar componentes nuevos de la barra de tareas al componente parsys para añadirlos a la página de aterrizaje.
* En parsys también hay dos componentes de título.

### Destino {#target}

El componente de destino muestra el contenido de una experiencia en la página. Puede haber muchas experiencias creadas en una campaña y el componente de destino mostrará de forma dinámica el contenido de experiencias distintas a diferentes usuarios que visiten la página.

El código HTML para insertar un componente de destino y crear también experiencias distintas en una campaña:

```xml
<div data-cq-component="target">
 <section data-cq-component="experience" data-cq-experience="default">
  <p data-cq-component="text">Default content. Select this campaign in client context to view other experiences</p>
 </section>

 <section data-cq-component="experience" data-cq-segment="over-30">
  <p data-cq-component="text">Content for Over 30</p>
 </section>

 <section data-cq-component="experience" data-cq-segment="under-30">
  <p data-cq-component="text">Content for Under 30</p>
 </section>
</div>
```

## Opciones de importación adicionales {#additional-importing-options}

Además de especificar si los componentes que se importarán serán componentes de AEM editables, también puede configurar las opciones siguientes antes de importar el paquete de diseño:

* Configurar las propiedades de página extrayendo los metadatos definidos en el HTML importado.
* Especificar la codificación del juego de caracteres en HTML.
* Superponiendo la plantilla de página del importador.

### Configuración de las propiedades de página extrayendo los metadatos definidos en el HTML importado {#setting-page-properties-by-extracting-metadata-defined-in-imported-html}

El importador de diseños extraerá y conservará como propiedad &quot;jcr:description&quot; los metadatos siguientes declarados en el encabezado del HTML importado:

* &lt;meta name=&quot;description&quot; content=&quot;&quot;>

El importador de diseños extraerá y conservará el atributo de idioma establecido en la etiqueta de HTML como la propiedad &quot;jcr:language&quot;

* &lt;html lang=&quot;en&quot;>

### Especificación de la codificación del juego de caracteres en HTML {#specifying-the-charset-encoding-in-the-html}

El importador de diseños lee la codificación especificada en el HTML importado. La codificación puede especificarse como se indica:

`<meta charset="UTF-8">`

*O*

`<meta http-equiv="content-type" content="text/html;charset=utf-8">`

Si no se especifica ninguna codificación en el HTML importado, la codificación predeterminada del importador de diseños es UTF-8.

### Superposición de la plantilla {#overlaying-template}

La plantilla Página de aterrizaje en blanco se puede superponer creando una nueva en: `/apps/<appName>/designimporter/templates/<templateName>`

AEM Se explican los pasos para crear una nueva plantilla en la creación de plantillas de formulario [aquí](/help/sites-developing/templates.md).

### Referencia a un componente desde la página de aterrizaje {#referring-a-component-from-landing-page}

Supongamos que tiene un componente al que desea hacer referencia en el HTML mediante un atributo data-cq-component de forma que el importador de diseños procese un componente &quot;incluir en este lugar&quot;. por ejemplo, desea hacer referencia al componente de tabla ( `resourceType = /libs/foundation/components/table`). Se debe añadir lo siguiente al HTML:

`<div data-cq-component="/libs/foundation/components/table">foundation table</div>`

La ruta en data-cq-component debería ser el resourceType del componente.

### Prácticas recomendadas {#best-practices}

No se recomienda utilizar selectores de CSS similares a los siguientes con elementos marcados para la conversión de componentes durante la importación.

| E > F | un elemento secundario F de un elemento E | [Combinador secundario](https://www.w3.org/TR/css3-selectors/#child-combinators) |
|---|---|---|
| E &amp;gt; F | un elemento F precedido inmediatamente por un elemento E | [Combinador del mismo nivel adyacente](https://www.w3.org/TR/css3-selectors/#adjacent-sibling-combinators) |
| E ~ F | un elemento F precedido por un elemento E | [Combinador general del mismo nivel](https://www.w3.org/TR/css3-selectors/#general-sibling-combinators) |
| E:root | un elemento E, raíz del documento | [Pseudoclases estructurales](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-child(n) | un elemento E, el elemento secundario n del primario | [Pseudoclases estructurales](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-child(n) | un elemento E, el elemento secundario n del primario, contando a partir del último | [Pseudoclases estructurales](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-of-type(n) | un elemento E, el elemento similar n de este tipo | [Pseudoclases estructurales](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-of-type(n) | un elemento E, el elemento similar n de su tipo, contando a partir del último | [Pseudoclases estructurales](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |

Esto se debe al hecho de que los elementos HTML adicionales como &lt;div> se añaden al HTML generado después de la importación.

* No se recomiendan los scripts que dependen de una estructura similar a la siguiente para elementos marcados para su conversión en componentes de AEM.
* Uso de estilos en las etiquetas de marcado para la conversión de componentes como &lt;div data-cq-component=&quot;&amp;ast;&quot;> no se recomienda.
* El formato de diseño debería seguir las recomendaciones de HTML5 Boilerplate. Más información sobre: [https://html5boilerplate.com/](https://html5boilerplate.com/).

## Configuración de módulos OSGI {#configuring-osgi-modules}

Los componentes que exponen propiedades configurables mediante la consola OSGI son los siguientes:

* Importador de diseños de páginas de aterrizaje
* Generador de páginas de aterrizaje
* Generador de páginas de aterrizaje móviles
* Preprocesador de entradas de páginas de aterrizaje

La tabla que aparece a continuación describe brevemente las propiedades:

<table>
 <tbody>
  <tr>
   <td><strong>Componente</strong></td>
   <td><strong>Nombre de propiedad</strong></td>
   <td><strong>Descripción de la propiedad </strong></td>
  </tr>
  <tr>
   <td>Importador de diseños de páginas de aterrizaje</td>
   <td>Filtro de extracción</td>
   <td>Lista de expresiones regulares que se utilizará para filtrar archivos de la extracción. <br /> Las entradas de archivos comprimidos que coincidan con los patrones especificados se excluirán de la extracción</td>
  </tr>
  <tr>
   <td>Generador de páginas de aterrizaje</td>
   <td>Patrón de archivos</td>
   <td>El Generador de páginas de aterrizaje se puede configurar para que gestione los archivos de HTML que coinciden con una expresión regular según se define en el patrón de archivo.</td>
  </tr>
  <tr>
   <td>Generador de páginas de aterrizaje móviles</td>
   <td>Patrón de archivos</td>
   <td>El Generador de páginas de aterrizaje se puede configurar para que gestione los archivos de HTML que coinciden con una expresión regular según se define en el patrón de archivo.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Grupos de dispositivos</td>
   <td>Lista de grupos de dispositivos que se admiten.</td>
  </tr>
  <tr>
   <td>Preprocesador de entradas de páginas de aterrizaje</td>
   <td>Patrón de búsqueda </td>
   <td>Patrón que se buscará en el contenido de entradas del archivo. Esta expresión regular coincide con la entrada de contenido línea a línea. Tras la coincidencia, el texto coincidente se reemplaza con el patrón de reemplazo especificado.<br /> <br /> Consulte la nota siguiente sobre las restricciones actuales del preprocesador de entradas de páginas de aterrizaje.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Patrón de sustitución</td>
   <td>Patrón que sustituye las coincidencias encontradas. Puede usar referencias de grupo regex como $1 o $2. Además, este patrón admite palabras clave como {designPath} que se resuelven con el valor real durante la importación.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>**Restricciones actuales del preprocesador de entradas de páginas de aterrizaje:**
>Si necesita realizar cambios en el patrón de búsqueda, al abrir el editor de propiedades felix deberá añadir caracteres de barra invertida de forma manual para evitar los metacaracteres regex. Si no añade dichos caracteres de forma manual, regex se considerará no válido y no sustituirá el anterior.
>
>Por ejemplo, si la configuración predeterminada es
>`/\* *CQ_DESIGN_PATH *\*/ *(['"])`
>
>Y usted necesita reemplazar >`CQ_DESIGN_PATH` con `VIPURL` en el patrón de búsqueda, el patrón de búsqueda debería tener este aspecto:
`/\* *VIPURL *\*/ *(['"])`

## Solución de problemas {#troubleshooting}

Al importar el paquete de diseño, pueden producirse varios errores, que se describen en esta sección.

### Inicialización de la barra de tareas con los componentes relevantes de la página de aterrizaje {#initialization-of-sidekick-with-landing-page-relevant-components}

Si el paquete de diseño contiene un código de componente parsys, tras la importación, la barra de tareas comienza a mostrar los componentes relevantes de la página de aterrizaje. Puede arrastrar y soltar nuevos componentes en el componente parsys de su página de aterrizaje. También puede ir al modo de diseño y añadir nuevos componentes a la barra de tareas.

### Se muestran mensajes de error durante la importación {#error-messages-displayed-during-import}

En caso de errores (por ejemplo, el paquete importado no es un zip válido), la importación de diseño no importará el paquete y, en su lugar, mostrará un mensaje de error en la parte superior de la página justo encima del cuadro de arrastre y suelte. A continuación se muestran ejemplos de errores. Tras corregir el error, puede volver a importar el archivo comprimido actualizado en la misma página de aterrizaje en blanco. Distintos casos en los que se producen errores:

* El paquete de diseño importado no es un archivo comprimido válido.
* El paquete de diseño importado no contiene un index.html en el nivel superior.

### Advertencias que se muestran tras la importación {#warnings-displayed-after-import}

En caso de advertencias (por ejemplo, HTML se refiere a imágenes que no existen dentro del paquete), el importador de diseños importará el zip, pero al mismo tiempo mostrará una lista de problemas/advertencias en el panel de resultados. Al hacer clic en el vínculo de problemas, se mostrará una lista de advertencias que señalan cualquier problema dentro del paquete de diseño. Los siguientes son casos en los que el importador de diseños captura y muestra advertencias:

* El HTML hace referencia a imágenes que no existen dentro del paquete.
* El HTML hace referencia a scripts que no existen dentro del paquete.
* HTML hace referencia a estilos que no existen dentro del paquete.

### ¿Dónde se guardan los archivos del archivo comprimido en AEM? {#where-are-the-files-of-the-zip-file-being-stored-in-aem}

Tras importar la página de aterrizaje, los archivos (imágenes, css, js, etc.) AEM dentro del paquete de diseño se almacenan en la siguiente ubicación en la siguiente ubicación de la:

`/etc/designs/default/canvas/content/campaigns/<name of brand>/<name of campaign>/<name of landing page>`

Supongamos que la página de aterrizaje se crea en la campaña We.Retail y que el nombre de la página de aterrizaje es **myBlankLandingPage** a continuación, la ubicación donde se almacenan los archivos Zip es la siguiente:

`/etc/designs/default/canvas/content/campaigns/geometrixx/myBlankLandingPage`

### No se conserva el formato {#formatting-not-preserved}

Al crear un CSS, tenga en cuenta las restricciones siguientes:

Si un texto y una imagen (editable) son como los siguientes:

```xml
<div class="box">
<p><div data-cq-component="image"><img src="assets/image.jpg" width="115"
height="116" /></div>Some Text </p>
</div>
```

con un CSS aplicado a la clase `box` como sigue:

```xml
.box

{ width: 450px; padding:10px; border: 1px #C5DBE7 solid; margin: 0px auto 0 auto; background-image:url(assets/box.gif); background-repeat:repeat-x,y; font-family:Verdana, Arial, Helvetica, sans-serif; font-size:12px; color:#6D6D6D; }
```

Entonces `box img` se utiliza en el importador de diseños, la página de aterrizaje resultante parece no haber conservado el formato. Para solucionarlo, tenga en cuenta que AEM añade etiquetas div en el CSS y vuelva a escribir el código como corresponda. De lo contrario, ciertas reglas de CSS no serán válidas.

```xml
.box img

{ float:right; margin: 0 0 5px 5px; border: 1px #343434 solid; }
```

>[!NOTE]
Además, los diseñadores deben tener en cuenta que solo el código dentro de **id=cqcanvas** el importador reconoce la etiqueta; de lo contrario, el diseño no se conserva.
