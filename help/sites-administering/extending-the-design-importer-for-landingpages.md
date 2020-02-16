---
title: Ampliación y configuración del Importador de diseños para páginas de aterrizaje
seo-title: Ampliación y configuración del Importador de diseños para páginas de aterrizaje
description: Descubra cómo configurar el Importador de diseños para las páginas de aterrizaje.
seo-description: Descubra cómo configurar el Importador de diseños para las páginas de aterrizaje.
uuid: a2dd0c30-03e4-4e52-ba01-6b0b306c90fc
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e02f5484-fbc2-40dc-8d06-ddb53fd9afc2
docset: aem65
translation-type: tm+mt
source-git-commit: 0a94bf49a7136c5831c42eb274d07517c12014ec

---


# Ampliación y configuración del Importador de diseños para páginas de aterrizaje{#extending-and-configuring-the-design-importer-for-landing-pages}

Esta sección describe cómo configurar y, si se desea, ampliar el importador de diseños para las páginas de aterrizaje. El trabajo con las páginas de aterrizaje después de la importación se trata en las páginas [de aterrizaje.](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)

**Cómo hacer que el importador de diseños extraiga su componente personalizado**

Estos son los pasos lógicos para que el importador de diseños reconozca su componente personalizado

1. Creación de un TagHandler

   * Un controlador de tags en un POJO que gestiona tags HTML de un tipo específico. El tipo de tags HTML que el TagHandler puede gestionar se define mediante la propiedad OSGi “tagpattern.name” de TagHandlerFactory. La propiedad OSGi es un regex que debería coincidir con la tag HTML de entrada que desee gestionar. Todas las tags anidadas se enviarán al controlador de tags para que las gestione. Por ejemplo, si se registra para un div que contiene una etiqueta &lt;p> anidada, la etiqueta &lt;p> también se envía a TagHandler y depende de usted cómo desea cuidarla.
   * La interfaz del controlador de tags es similar a la interfaz del controlador de contenido SAX. Recibe eventos SAX para cada tag HTML. Como autor del controlador de tags, deberá implementar ciertos métodos de ciclo de vida invocados automáticamente por la estructura del importador de diseños.

1. Cree su TagHandlerFactory correspondiente.

   * La fábrica del controlador de tags es un componente OSGi (singleton) responsable de generar instancias de su controlador de tags.
   * su fábrica del controlador de tags debe exponer una propiedad OSGi denominada “tagpattern.name”, cuyo valor se compara con la tag HTML de entrada.
   * Si hay varios controladores de tag que coinciden con la tag HTML de entrada, se elige el que tenga una clasificación superior. The ranking itself is exposed as an OSGi property **service.ranking**.
   * TagHandlerFactory es un componente OSGi. Deberá suministrar todas las referencias al TagHandler mediante esta fábrica.

1. Asegúrese de que TagHandlerFactory tenga una clasificación mejor si desea anular la predeterminada.

>[!CAUTION]
>
>El Importador de diseños que se usa para importar páginas de aterrizaje [está en desuso en AEM 6.5](/help/release-notes/deprecated-removed-features.md#deprecated-features).

## Preparar el HTML para su importación {#preparing-the-html-for-import}

Después de crear una página de importador, puede importar la página de aterrizaje HTML completa. Para importar su página de aterrizaje HTML, primero debe comprimir su contenido en un paquete de diseño. El paquete de diseño contiene la página de aterrizaje HTML y los recursos a los que hace referencia (imágenes, css, iconos, scripts, etc.).

La hoja de trucos siguiente le muestra cómo preparar el HTML para la importación:

Hoja de consejos de la página de aterrizaje

[Obtener archivo](assets/cheatsheet.zip)

### Diseño y requisitos del archivo comprimido {#zip-file-layout-and-requirements}

>[!NOTE]
>
>Los archivos comprimidos solo pueden contener una parte de una página o una página HTML.

A continuación se muestra un ejemplo de diseño de archivo comprimido:

* /index.html -> archivo HTML de la página de aterrizaje
* /css -> para agregar a la clientlib CSS
* /img -> todas las imágenes y recursos
* /js -> para agregar a la clientlib JS

El diseño se basa en el diseño de las recomendaciones HTML5 Boilerplate. Obtenga más información en [https://html5boilerplate.com/](https://html5boilerplate.com/)

>[!NOTE]
>
>At a minimum, the design package **must** contain an **index.html** file at the root level. In case the landing page to be imported has a mobile version as well, then the zip must contain a **mobile.index.html** along with **index.html** at the root level.

### Preparación del HTML de la página de aterrizaje {#preparing-the-landing-page-html}

Para poder importar el HTML, debe añadir un div lienzo al HTML de la página de aterrizaje.

The canvas div is an html **div** with `id="cqcanvas"` that must be inserted within the HTML `<body>` tag and must wrap the content intended for conversion.

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

En la sección siguiente se describe cómo editar su archivo HTML para poder convertir ciertas partes de sus páginas de aterrizaje en diferentes componentes de AEM editables. Los componentes se describen en detalle en los componentes [de las páginas de](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)aterrizaje.

>[!NOTE]
>
>El código HTML que se utiliza para convertir partes de la página de aterrizaje en componentes de AEM tiene una forma larga y una declaración abreviada de tag. Ambas se describen para cada componente.

### Restricciones {#limitations}

Antes de importar, tenga en cuenta las restricciones siguientes:

### Los atributos como class o id aplicados a No se conserva la etiqueta &amp;lt;body> {#any-attribute-like-class-or-id-applied-on-the-amp-lt-body-tag-is-not-preserved}

If any attribute like id or class is applied on the body tag for example `<body id="container">` then it is not preserved after the import. So the design being imported should not have any dependencies on the attributes applied on the `<body>` tag.

### Arrastre y colocación del archivo comprimido {#drag-and-drop-zip}

La carga de archivos comprimidos de arrastrar y soltar no es compatible con Internet Explorer y Firefox versión 3.6 y anteriores. Para cargar un diseño con estos navegadores, haga clic en la zona en la que desea soltar los archivos para abrir un cuadro de diálogo de carga de archivos y cargar el diseño.

Los navegadores que admiten &quot;arrastrar y soltar&quot; del zip de diseño son Chrome, Safari5.x, Firefox 4 y versiones posteriores.

### No se admite Modernizr {#modernizr-is-not-supported}

`Modernizr.js` es una herramienta basada en javascript que detecta capacidades nativas de los navegadores y determina si son o no adecuadas para elementos HTML5. Los diseños que utilizan Modernizr para mejorar la compatibilidad con versiones anteriores de diferentes navegadores pueden causar problemas de importación en la solución de página de aterrizaje. No se admiten los scripts de `Modernizr.js` con el importador de diseños.

### No se conservan las propiedades de página cuando se importa un paquete de diseño {#page-properties-are-not-preserved-at-the-time-of-importing-design-package}

Todas las propiedades de página (e.g. dominio personalizado, aplicación de HTTPS, etc.) definidas antes de importar el paquete de diseño para una página que utilice la plantilla de página de aterrizaje en blanco se perderán tras la importación del diseño. Por lo tanto, se recomienda definir las propiedades de página tras importar el paquete de diseño.

### Se asume el código HTML solamente {#html-only-markup-assumed}

Tras la importación, el marcado se corrige por motivos de seguridad y para evitar la importación y publicación del marcado que no sea válido. Debido a ello, el marcado que sea solo HTML y cualquier otra forma de elemento, como el SVG incorporado o los componentes web se eliminarán.

### Texto {#text}

Código HTML para insertar un componente de texto (`foundation/components/text`) en el HTML dentro del paquete de diseño:

```xml
<div data-cq-component="text"> <p>This is some editable text</p> </div>
```

Si se incluye el código anterior en el HTML, ocurrirá lo siguiente:

* Creates an editable AEM text component ( `sling:resourceType=foundation/components/text`) in the landing page created after importing the design package.
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

HTML markup to insert a title component ( `wcm/landingpage/components/title`) in the HTML within design package:

```xml
<div data-cq-component="title"> <h1>This is some editable title text</h1> </div>
```

Si se incluye el código anterior en el HTML, ocurrirá lo siguiente:

* Creates an editable AEM title component ( `sling:resourceType=wcm/landingpage/components/title`) in the landing page created after importing the design package.
* La propiedad`jcr:title`   del componente de título creado se configurará en el texto dentro de la tag de encabezado encerrada en el div.
* La propiedad `type` se configurará en la tag de encabezado, en este caso `h1`.

El componente de título admite 7 tipos `h1, h2, h3, h4, h5, h6` y `default`.

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

* Creates an editable AEM image component ( `sling:resourceType=foundation/components/image`) in the landing page created after importing the design package.
* La propiedad `fileReference` del componente de imagen creado se configurará en la ruta en la que se importará la imagen especificada en el atributo src.
* Sets the `alt` property to the value of alt attribute in the img tag.
* Sets the `title` property to the value of title attribute in the img tag.
* Sets the `width` property to the value of width attribute in the img tag.
* Sets the `height` property to the value of height attribute in the img tag.

**Declaración abreviada de tag de componente:**

```xml
<img data-cq-component="image" src="test.png" alt="Image component shorthand"/>
```

#### No se admite img src de URL absoluta dentro del div del componente imagen {#absolute-url-img-src-not-supported-within-image-component-div}

If an `<img>` tag with an absolute url src is attempted for component conversion, an appropriate **UnsupportedTagContentException** is raised. Por ejemplo, no se admite lo siguiente:

`<div data-cq-component="image">`

`<img src="https://cdn.printfriendly.com/pf-button.gif" alt="Print Friendly and PDF"/>`

`</div>`

Aparte de esto, se admiten las imágenes de URL absoluta para las tags img que no formen parte del div componente de imagen.

### Componentes de llamada a acción {#call-to-action-components}

Puede marcar parte de la página de aterrizaje para importarla como un &quot;componente de llamada a acción editable&quot;; estos componentes de llamada a acción importados se pueden editar después de importar la página de aterrizaje. AEM incluye los componentes de llamada a acción siguientes:

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

Tag HTML para incluir un componente de vínculo gráfico en el archivo comprimido importado. Aquí href se asignará a la dirección URL de destino, img src será la imagen de procesamiento, &quot;title&quot; se tomará como texto al pasar el ratón, etc.

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
>To create a clickthroughgraphical link, you need to wrap an anchor tag and the image tag inside a div with `data-cq-component="clickthroughgraphicallink"` attribute.
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
>con un `css .hasbackground { background-image: pathtoimage }`


### Formulario de posibles clientes {#lead-form}

Los formularios de posibles clientes se utilizan para recopilar información de perfil de un visitante o posible cliente. Dicha información puede guardarse y utilizarse posteriormente para realizar campañas de marketing eficaces basadas en la información. Esta información suele incluir título, nombre, correo electrónico, fecha de nacimiento, dirección, intereses, etc. Forma parte del grupo &quot;Llamada a acción: formulario de posibles clientes&quot;.

**Funciones admitidas**

* Campos de posibles clientes predefinidos: nombre, apellidos, dirección, dob, sexo, acerca de, userId, emailId, botón de envío están disponibles en la barra de tareas. Tan solo tiene que arrastrar y soltar el componente deseado en el formulario de posibles clientes.
* Con estos componentes, se puede diseñar un formulario de posibles clientes independiente; estos campos corresponden con los campos del formulario de posibles clientes. En las aplicaciones independientes o de archivos comprimidos importados, el usuario puede añadir campos suplementarios mediante los campos de Llamada a acción: formulario de posibles clientes o cq:form, darles un nombre y diseñarlos como prefiera.
* Asigne campos de formulario de posibles clientes utilizando nombres predefinidos específicos del formulario de posibles clientes de llamada a acción, por ejemplo: firstName para el nombre en el formulario de posibles clientes, etc.
* Los campos que no se asignen a un formulario de posibles clientes se asignarán a componentes de cq:form: texto, botón de opción, casilla de verificación, menú desplegable, oculto, contraseña.
* El usuario puede especificar el título mediante la tag “label” y escoger el estilo con el atributo de estilo “class” (solo disponible para los componentes de Llamada a acción: formulario de posibles clientes).
* La página de agradecimiento y la lista de suscripciones se pueden proporcionar como parámetros ocultos del formulario (presentes en index.htm) o se pueden agregar o editar desde la barra de edición de &quot;Inicio del formulario de posibles clientes&quot;

   &lt;input type=&quot;hidden&quot; name=&quot;redirectUrl&quot; value=&quot;/content/we-retail/es/user/register/thank_you&quot;/>

   &lt;input type=&quot;hidden&quot; name=&quot;groupName&quot; value=&quot;leadForm&quot;/>

* Las restricciones como - requeridas pueden proporcionarse desde la configuración de edición de cada componente.

Tag HTML para incluir un componente de vínculo gráfico en el archivo comprimido importado. Aquí &quot;firstName&quot; se asigna a firstName del formulario de posibles clientes, etc., excepto para las casillas de verificación: estas dos casillas de verificación se asignan al componente desplegable cq:form.

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
* Superposición de la plantilla de página del importador.

### Configuración de las propiedades de página extrayendo los metadatos definidos en el HTML importado {#setting-page-properties-by-extracting-metadata-defined-in-imported-html}

El importador de diseños debe extraer y conservar los metadatos siguientes declarados en el encabezado del HTML importado como propiedad &quot;jcr:description&quot;:

* &lt;meta name=&quot;description&quot; content=&quot;&quot;>

El importador de diseños debe extraer y conservar el atributo Lang establecido en la etiqueta HTML como propiedad &quot;jcr:language&quot;

* &lt;html lang=&quot;en&quot;>

### Especificación de la codificación del juego de caracteres en HTML {#specifying-the-charset-encoding-in-the-html}

El importador de diseños lee la codificación especificada en el HTML importado. La codificación puede especificarse como se indica:

`<meta charset="UTF-8">`

*O*

`<meta http-equiv="content-type" content="text/html;charset=utf-8">`

Si no se especifica ninguna codificación en el HTML importado, la codificación predeterminada del importador de diseños es UTF-8.

### Superposición de la plantilla {#overlaying-template}

La plantilla Página de aterrizaje en blanco se puede superponer creando una nueva en: `/apps/<appName>/designimporter/templates/<templateName>`

Los pasos para crear una nueva plantilla en AEM se explican [aquí](/help/sites-developing/templates.md).

### Referencia a un componente desde la página de aterrizaje {#referring-a-component-from-landing-page}

Supongamos que tiene un componente al que desea hacer referencia en el HTML mediante un atributo data-cq-component de forma que el importador de diseños procese un componente &quot;incluir en este lugar&quot;. e.g., you want to reference the table component ( `resourceType = /libs/foundation/components/table`). Se debe añadir lo siguiente al HTML:

`<div data-cq-component="/libs/foundation/components/table">foundation table</div>`

La ruta en data-cq-component debería ser el resourceType del componente.

### Recomendaciones {#best-practices}

No se recomienda utilizar selectores de CSS similares a los siguientes con elementos marcados para la conversión de componentes durante la importación.

| E > F | un elemento secundario F de un elemento E | [Combinador secundario](https://www.w3.org/TR/css3-selectors/#child-combinators) |
|---|---|---|
| E &amp;gt; F | un elemento F precedido inmediatamente por un elemento E | [Combinador adyacente del mismo nivel](https://www.w3.org/TR/css3-selectors/#adjacent-sibling-combinators) |
| E ~ F | un elemento F precedido por un elemento E | [Combinador de elementos del mismo nivel general](https://www.w3.org/TR/css3-selectors/#general-sibling-combinators) |
| E:root | un elemento E, raíz del documento | [Pseudoclases estructurales](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-child(n) | un elemento E, el elemento secundario n del primario | [Pseudoclases estructurales](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-child(n) | un elemento E, el elemento secundario n del primario, contando a partir del último | [Pseudoclases estructurales](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-of-type(n) | un elemento E, el elemento similar n de este tipo | [Pseudoclases estructurales](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-of-type(n) | un elemento E, el elemento similar n de su tipo, contando a partir del último | [Pseudoclases estructurales](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |

Esto se debe a que después de la importación se agregan elementos HTML adicionales como la etiqueta &lt;div> al HTML generado.

* No se recomiendan los scripts que dependen de una estructura similar a la siguiente para elementos marcados para su conversión en componentes de AEM.
* No se recomienda el uso de estilos en las etiquetas de marcado para la conversión de componentes como &lt;div data-cq-component=&quot;&amp;ast;&quot;>.
* El formato de diseño debería seguir las recomendaciones de HTML5 Boilerplate. Lea más sobre: [https://html5boilerplate.com/](https://html5boilerplate.com/).

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
   <td>El Generador de páginas de aterrizaje puede configurarse para gestionar archivos HTML que coincidan con una expresión regular, tal como se define en el patrón de archivos.</td>
  </tr>
  <tr>
   <td>Generador de páginas de aterrizaje móviles</td>
   <td>Patrón de archivos</td>
   <td>El Generador de páginas de aterrizaje puede configurarse para gestionar archivos HTML que coincidan con una expresión regular, tal como se define en el patrón de archivos.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Grupos de dispositivos</td>
   <td>Lista de grupos de dispositivos que se admiten.</td>
  </tr>
  <tr>
   <td>Preprocesador de entradas de páginas de aterrizaje</td>
   <td>Patrón de búsqueda </td>
   <td>Patrón que se buscará en el contenido de entradas del archivo. Esta expresión regular coincide con el contenido de entrada línea por línea. Una vez coincidido, el texto coincidente se sustituye por el patrón de reemplazo especificado.<br /> <br /> Consulte la nota siguiente sobre las restricciones actuales del preprocesador de entradas de páginas de aterrizaje.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Patrón de sustitución</td>
   <td>Patrón que sustituye las coincidencias encontradas. Puede utilizar referencias de grupo regex como $1, $2. Además, este patrón admite palabras clave como {designPath} que se resuelven con el valor real durante la importación.</td>
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
>Y necesitas reemplazar >`CQ_DESIGN_PATH` con `VIPURL` el patrón de búsqueda, el patrón de búsqueda debería tener este aspecto:
`/\* *VIPURL *\*/ *(['"])`

## Solución de problemas {#troubleshooting}

Al importar el paquete de diseño, pueden producirse varios errores, que se describen en esta sección.

### Inicialización de la barra de tareas con los componentes relevantes de la página de aterrizaje {#initialization-of-sidekick-with-landing-page-relevant-components}

Si el paquete de diseño contiene un código de componente parsys, tras la importación, la barra de tareas comienza a mostrar los componentes relevantes de la página de aterrizaje. Puede arrastrar y soltar nuevos componentes en el componente parsys de su página de aterrizaje. También puede ir al modo de diseño y añadir nuevos componentes a la barra de tareas.

### Se muestran mensajes de error durante la importación {#error-messages-displayed-during-import}

En caso de que se produzcan errores (por ejemplo, el paquete importado no es un archivo comprimido válido), la importación del diseño no importará el paquete y mostrará un mensaje de error en la parte superior de la página, encima del cuadro de arrastrar y soltar. A continuación se muestran ejemplos de errores. Tras corregir el error, puede volver a importar el archivo comprimido actualizado en la misma página de aterrizaje en blanco. Distintos casos en los que se producen errores:

* El paquete de diseño importado no es un archivo comprimido válido.
* El paquete de diseño importado no contiene un index.html en el nivel superior.

### Advertencias que se muestran tras la importación {#warnings-displayed-after-import}

En caso de que aparezca alguna advertencia (p. ej., HTML hace referencia a imágenes que no existen dentro del paquete), el importador de diseños importará el zip pero, al mismo tiempo, mostrará una lista de problemas/advertencias en el panel de resultados. Al hacer clic en el vínculo de problemas, se mostrará una lista de advertencias que señalarán cualquier problema dentro del paquete de diseño. Los siguientes son casos en los que el importador de diseños captura y muestra advertencias:

* HTML hace referencia a imágenes que no existen dentro del paquete.
* HTML hace referencia a secuencias de comandos que no existen en el paquete.
* HTML hace referencia a estilos que no existen dentro del paquete.

### Where are the files of the ZIP file being stored in AEM? {#where-are-the-files-of-the-zip-file-being-stored-in-aem}

Tras importar la página de aterrizaje, los archivos (imágenes, css, js, etc.) dentro del paquete de diseño se almacenan en la siguiente ubicación de AEM:

`/etc/designs/default/canvas/content/campaigns/<name of brand>/<name of campaign>/<name of landing page>`

Suppose the landing page is created under the campaign We.Retail and the name of the landing page is **myBlankLandingPage** then the location were Zip files are stored is as follows:

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

with a CSS applied on the class `box` as follows:

```xml
.box

{ width: 450px; padding:10px; border: 1px #C5DBE7 solid; margin: 0px auto 0 auto; background-image:url(assets/box.gif); background-repeat:repeat-x,y; font-family:Verdana, Arial, Helvetica, sans-serif; font-size:12px; color:#6D6D6D; }
```

Then `box img` is used in the design importer, the resulting landing page appears not have preserved the formatting. Para solucionarlo, tenga en cuenta que AEM añade etiquetas div en el CSS y vuelva a escribir el código como corresponda. De lo contrario, ciertas reglas de CSS no serán válidas.

```xml
.box img

{ float:right; margin: 0 0 5px 5px; border: 1px #343434 solid; }
```

>[!NOTE]
Also, designers should be aware that only code inside the **id=cqcanvas** tag is recognized by the importer, otherwise design is not preserved.

