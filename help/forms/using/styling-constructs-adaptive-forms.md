---
title: Construcciones de estilo para formularios adaptables
seo-title: Construcciones de estilo para formularios adaptables
description: Utilice el marco LESS para personalizar el aspecto de los formularios adaptables.
seo-description: Utilice el marco LESS para personalizar el aspecto de los formularios adaptables.
uuid: d2e45ad9-7322-43ce-a1dd-ad97e2eea742
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: ed50fa70-a8dd-4cc6-82a9-d59de0fa417d
docset: aem65
feature: Formularios adaptables
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2324'
ht-degree: 3%

---


# Construcciones de estilo para formularios adaptables{#styling-constructs-for-adaptive-forms}

## Requisitos previos {#prerequisites}

Conocimiento de CSS y del marco LESS.

## Qué se puede personalizar {#what-can-be-customized}

El artículo enumera las clases css disponibles públicamente de formularios adaptables. Puede aprovechar estas clases para aplicar estilo a varios componentes de un formulario adaptable. El estilo de los componentes de creación, como los cuadros de diálogo y las barras de estado que muestran advertencias, excede el ámbito de este artículo. Utilice estas construcciones de estilo para crear estilos (con CSS o Less) solo cuando no pueda aplicar estilo a los componentes mediante [editor de temas](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html).

## Personalización de estilos en formularios adaptables {#customizing-styles-in-adaptive-forms}

El marco LESS simplifica el caso de uso para personalizar estilos en formularios adaptables. El marco permite definir estilos utilizando un conjunto de variables y funciones (mezclas). El marco LESS ayuda a reducir el tamaño del código agrupado y aumenta su reutilización.

Puede personalizar los estilos de formulario adaptables de las siguientes maneras:

* Cambiar el tema
* Cambiar el estilo del componente

## Cambio del tema {#changing-theme}

Puede cambiar el tema de un formulario adaptable para asegurarse de que su aspecto sea coherente con las páginas web en las que está incrustado el formulario adaptable.

Los cambios en el aspecto general del formulario adaptable que utiliza propiedades CSS suelen formar parte de los cambios de tema. Los principales cambios en la apariencia &quot;adecuada&quot; del formulario adaptable, como los cambios en el diseño y la ubicación de los componentes, no se consideran cambios de tema.

En función del arranque, el siguiente conjunto de propiedades CSS define el tema de una página web:

* Color de fondo
* Borde (tipo, color, grosor)
* Color de fuente
* Espacio
* imagen
* Tamaño de fuente
* LineHeight

Actualmente, las variables LESS se definen solo para estas propiedades de los distintos elementos de una forma adaptativa.

## Cambio del estilo de componente {#changing-component-style}

Puede realizar cambios en el aspecto, el diseño, el posicionamiento y la visibilidad de los elementos. Para realizar esta tarea, cree o actualice los archivos .css personalizados para incluir las construcciones de estilo que se enumeran en este artículo.

Para aplicar un estilo a un formulario adaptable, abra el formulario adaptable en para editarlo, abra las propiedades del contenedor de formularios adaptables y especifique la ruta del archivo CSS personalizado en la pestaña basic . Las construcciones de estilo predeterminadas del formulario adaptable se anulan con las construcciones enumeradas en el archivo .css personalizado.

## Componentes {#components}

Los componentes mencionados en este artículo tienen sus clases CSS predefinidas. Puede editar las variables para modificar los estilos en las clases CSS. Como alternativa, puede reescribir toda la clase. En esta sección se describen las clases dentro de los componentes y los estilos que se pueden modificar mediante variables.

## Estilo de contenedor {#container-styling}

Un contenedor es el componente de nivel superior. Otros paneles y campos se encuentran debajo del componente contenedor.

<table>
 <tbody>
  <tr>
   <td><p><strong>Clase de CSS </strong></p> </td>
   <td><p><code>guideContainerNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Descripción de las variables</strong></p> </td>
   <td><p><strong>Descripción de las variables</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>container-bgColor</code></p> </td>
   <td><p>Color de fondo del contenedor</p> </td>
  </tr>
  <tr>
   <td><p><code>container-padding</code></p> </td>
   <td><p>Relleno para el contenedor</p> </td>
  </tr>
  <tr>
   <td><p><code>container-margin</code></p> </td>
   <td><p>Margen del contenedor</p> </td>
  </tr>
  <tr>
   <td><p><code>container-fontColor</code></p> </td>
   <td><p>Color de fuente del contenedor</p> </td>
  </tr>
 </tbody>
</table>

## Estilo de campo {#field-styling}

Los formularios adaptables incluyen varios tipos de campos. Cada campo tiene un nombre de clase único, que es el nombre del campo. El campo también tiene un nombre de clase común `guideFieldNode`.

Los campos incluyen etiquetas, utilidades, descripción de la ayuda (tanto descripciones largas como cortas) e iconos de ayuda de campos (signo de interrogación).

<table>
 <tbody>
  <tr>
   <td><p><strong>Clase de CSS </strong></p> </td>
   <td><p><code>guideFieldNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>field-padding</code><strong></strong></p> </td>
   <td><p>Relleno para el campo</p> </td>
  </tr>
  <tr>
   <td><p><code>field-error-font-color</code></p> </td>
   <td><p>Color de fuente del mensaje de error del campo</p> </td>
  </tr>
  <tr>
   <td><p><code>field-error-font-size</code></p> </td>
   <td><p>Tamaño de fuente del mensaje de error del campo</p> </td>
  </tr>
 </tbody>
</table>

## Estilo de etiqueta {#label-styling}

El elemento HTML **label** utilizado para el campo incluye las clases **left** o **top** dependiendo de si la etiqueta está en la parte superior o en la izquierda.

<table>
 <tbody>
  <tr>
   <td><p><strong>Clase de CSS </strong></p> </td>
   <td><p><code>guideFieldLabel</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>label-font-color</code></p> </td>
   <td><p>Color de fuente de la etiqueta de campo</p> </td>
  </tr>
  <tr>
   <td><p><code>label-font-size</code></p> </td>
   <td><p>Tamaño de fuente de la etiqueta de campo</p> </td>
  </tr>
  <tr>
   <td><p><code>label-line-height</code></p> </td>
   <td>Propiedad de altura de línea CSS para la etiqueta de campo </td>
  </tr>
  <tr>
   <td><p><code>label-font-weight</code></p> </td>
   <td>Propiedad de ponderación de fuente CSS para la etiqueta de campo </td>
  </tr>
  <tr>
   <td><p><code>label-margin</code></p> </td>
   <td><p>Margen de la etiqueta de campo</p> </td>
  </tr>
 </tbody>
</table>

Las reglas CSS para la etiqueta se aplican utilizando la etiqueta **guideFieldLabel**. Si es autor, anule esta regla para que los cambios personalizados sean visibles.

## Estilo de las utilidades {#widgets-styling}

Según su tipo, las utilidades también incluyen clases. Normalmente, las utilidades incluyen la clase `guideFieldWidget`. Los widgets que se envían con HTML normalmente utilizan la entrada estándar del elemento HTML y seleccionan. El estilo se realiza según corresponda. No se puede aplicar estilo a un widget personalizado cambiando las variables.

<table>
 <tbody>
  <tr>
   <td><p><strong>Clase de CSS </strong></p> </td>
   <td><p><code>guideFieldWidget</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables <code></code></strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-bg-color</code></p> </td>
   <td>Color de fondo de las utilidades (no funciona para la casilla de verificación y el botón de radio)</td>
  </tr>
  <tr>
   <td><p><code>widgets-border-color</code></p> </td>
   <td><p>Color de borde para las utilidades</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-thickness</code></p> </td>
   <td><p>Tamaño de borde de las utilidades</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-radius</code></p> </td>
   <td><p>Radio del borde de las utilidades</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-type</code></p> </td>
   <td><p>Tipo de borde de las utilidades</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-border-focus-type</code></p> </td>
   <td><p>Tipo de enfoque de los bordes de los widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border</code></p> </td>
   <td><p>Estilo de borde consolidado de las utilidades</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-color</code></p> </td>
   <td><p>Color del texto dentro del widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-size</code></p> </td>
   <td><p>Tamaño del texto dentro del widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-line-height</code></p> </td>
   <td>Propiedad CSS lineheight para el widget </td>
  </tr>
  <tr>
   <td><p><code>widgets-padding</code></p> </td>
   <td><p>Propiedad de relleno CSS para el widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-focus-border-color</code></p> </td>
   <td><p>Color de borde cuando el widget está enfocado</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-mandatory-border-color</code></p> </td>
   <td><p>Color de borde del widget para los campos obligatorios</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-mandatory-bg-color</code></p> </td>
   <td><p>Color de fondo del widget para los campos obligatorios</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-bg-color</code></p> </td>
   <td><p>Color de fondo del widget cuando el campo está desactivado</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-font-color</code></p> </td>
   <td><p>Color de fuente del widget cuando el campo está desactivado</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-border-color</code></p> </td>
   <td><p>Color de borde del widget cuando el campo está desactivado</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-height</code></p> </td>
   <td>Altura del widget (no funciona para la casilla de verificación y el botón de radio)</td>
  </tr>
  <tr>
   <td><p><code>checkbutton-height</code></p> </td>
   <td><p>Altura de la casilla de verificación y el botón de radio.</p> </td>
  </tr>
  <tr>
   <td><p><code>listboxwidget-height</code></p> </td>
   <td><p>Altura máxima de un menú desplegable de selección múltiple</p> </td>
  </tr>
 </tbody>
</table>

### Limitaciones en el estilo del widget {#limitations-in-widget-styling}

El estilo de los campos centrados, obligatorios y desactivados está restringido mediante variables. Sin embargo, puede cambiarlo anulando los estilos. La restricción mediante variables se proporciona principalmente para mantener bajo control el número de variables. La restricción se puede relajar si el aspecto de un campo cambia drásticamente porque está en cualquiera de los estados mencionados anteriormente.

## Descripción de la ayuda {#help-description}

Un autor puede especificar el contenido de la Ayuda en los campos mediante los componentes de descripción corta y larga . Ambos componentes tienen una clase común `.guideHelpDescription` y otra clase `.long`/ `.short`, según el tipo de descripción. El contenido de la Ayuda se adjunta en un elemento de párrafo para anular el estilo de la descripción. La descripción de la Ayuda (tanto larga como corta) se modifica mediante variables que comienzan por widgetshelp, como se indica en la siguiente tabla:

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-bg-color</code></p> </td>
   <td><p>Color de fondo de la ayuda larga de los widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-color</code></p> </td>
   <td><p>Color de borde de la ayuda larga de los widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-indicator-color</code></p> </td>
   <td><p>Color del borde del indicador izquierdo de la ayuda larga de los widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-bg-color</code></p> </td>
   <td><p>Color de fondo de la ayuda breve de las utilidades</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-color</code></p> </td>
   <td><p>Color de fuente de la ayuda breve de las utilidades</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-bg-color</code></p> </td>
   <td><p>Color de fondo de la ayuda de información breve del objeto de las utilidades</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-color</code></p> </td>
   <td><p>Color de fuente de la información de objeto corta de los widgets Ayuda</p> </td>
  </tr>
 </tbody>
</table>

## Términos y condiciones {#terms-and-conditions}

La utilidad Términos y condiciones (TnC `` ``) permite especificar términos y condiciones. Puede personalizar la utilidad mediante las variables que se describen en la tabla siguiente.

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><code>tnc-unvisited</code></td>
   <td>Color de fuente del vínculo tnc no visitado.</td>
  </tr>
  <tr>
   <td><code>tnc-visited</code></td>
   <td>Color de fuente del vínculo tnc visitado.</td>
  </tr>
 </tbody>
</table>

## Botón {#button}

Los botones también son widgets. Sin embargo, su estilo es ligeramente diferente del de los widgets. En los formularios adaptables, cualquiera de las siguientes opciones constituye un botón:

* input[type = text]
* botón
* elemento con clase .button

Código HTML para el botón :

`<button type="button" >`

`<span class="iconButtonicon"></`

`span>`

`<span class="iconButtonlabel"></`

`span>`

`</button>`

<table>
 <tbody>
  <tr>
   <td><p><strong>Clase de CSS</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>iconButton-icon</code></p> </td>
   <td><p>Proporciona iconos para el botón</p> </td>
  </tr>
  <tr>
   <td><p><code>iconButton-label</code></p> </td>
   <td><p>Etiqueta/rótulo del botón Estilos</p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables <code></code></strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-size</code></p> </td>
   <td><p>Tamaño del borde de los botones</p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-type</code></p> </td>
   <td><p>Tipo de borde</p> </td>
  </tr>
  <tr>
   <td><p><code>button-padding</code></p> </td>
   <td><p>Propiedad de relleno CSS para el botón</p> </td>
  </tr>
  <tr>
   <td><p><code>button-font-size</code></p> </td>
   <td><p>Tamaño de fuente del botón</p> </td>
  </tr>
  <tr>
   <td><p><code>button-background-color</code></p> </td>
   <td><p>Color de fondo del botón</p> </td>
  </tr>
  <tr>
   <td><p><code>button-font-color</code></p> </td>
   <td><p>Color de fuente del botón</p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-color</code></p> </td>
   <td><p>Color del borde del botón</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-padding</code></p> </td>
   <td><p>Relleno para botones grandes (botones con clase .buttonlarge)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-font-size</code></p> </td>
   <td><p>Tamaño de fuente para botones grandes</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-padding</code></p> </td>
   <td><p>Relleno para los botones pequeños (botones con clase .buttonsmall)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-font-size</code></p> </td>
   <td><p>Tamaño de fuente para botones pequeños</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-background-color</code></p> </td>
   <td><p>Color de fondo para botones informativos (botones con clase .buttoninformative)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-font-color</code></p> </td>
   <td><p>Color de fuente para botones informativos</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-border-color</code></p> </td>
   <td><p>Color del borde de los botones informativos</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-background-color</code></p> </td>
   <td><p>Color de fondo para botones con estilo de advertencia (botones con clase .buttonwarning)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-font-color</code></p> </td>
   <td><p>Color de fuente para botones con estilo de advertencia</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-border-color</code></p> </td>
   <td><p>Color del borde de los botones con estilo de advertencia</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-background-color</code></p> </td>
   <td><p>Color de fondo para botones de alerta (botones con clase .buttonalert)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-font-color</code></p> </td>
   <td><p>Color de fuente para botones de alerta</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-border-color</code></p> </td>
   <td><p>Color de borde para botones de alerta</p> </td>
  </tr>
 </tbody>
</table>

## Signo de interrogación {#question-mark}

Para las utilidades, se muestra un signo de interrogación cuando un autor añade una descripción larga al contenido de la Ayuda. Se utiliza el icono predeterminado proporcionado en bootstrap. Para utilizar un icono personalizado, puede personalizar los iconos de arranque.

<table>
 <tbody>
  <tr>
   <td><p><strong>Clase de CSS </strong></p> </td>
   <td><p><code>guideHelpQuestionMark</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>questionmark-font-color</code></p> </td>
   <td><p>Color del icono</p> </td>
  </tr>
  <tr>
   <td><p><code>questionmark-hover-font-color</code></p> </td>
   <td><p>Color del icono cuando se pasa el ratón sobre él</p> </td>
  </tr>
 </tbody>
</table>

## Tabla {#table}

Puede cambiar el tema de color para el encabezado y las filas de trabajo de una tabla mediante las siguientes variables.

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>table-header-bg-color</code></p> </td>
   <td><p>Color de fondo para la fila de encabezado. El valor predeterminado es <code>#333</code>.<br /> </p> </td>
  </tr>
  <tr>
   <td><p><code>table-odd-row-bg-color</code></p> </td>
   <td><p>Color de fondo para la fila de trabajo impar. El valor predeterminado es <code>rgb(255, 255, 255)</code>.</p> </td>
  </tr>
  <tr>
   <td><p><code>table-even-row-bg-color</code></p> </td>
   <td><p>Color de fondo para la fila de trabajo par. El valor predeterminado es <code>#eee</code>.</p> </td>
  </tr>
 </tbody>
</table>

## Archivo adjunto {#file-attachment}

El widget Archivo adjunto de los formularios adaptables permite cargar archivos. También puede personalizar la utilidad mediante las variables .

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemPadding</code></p> </td>
   <td><p>Relleno para los archivos mostrados en el widget</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemBackground</code></p> </td>
   <td><p>Color de fondo para el elemento de archivo</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemBorderColor</code></p> </td>
   <td><p>Color de borde para el borde superior</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemColor</code></p> </td>
   <td><p>Color de fuente para el elemento de archivo</p> </td>
  </tr>
  <tr>
   <td><p><code>filePreviewIconColor</code></p> </td>
   <td><p>Color del icono Vista previa (icono de Bootstrap) del widget</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemCommentHeight</code></p> </td>
   <td><p>Altura del comentario para el elemento de archivo</p> </td>
  </tr>
 </tbody>
</table>

## Estilos del navegador {#navigator-styles}

Existen cuatro tipos de pestañas del navegador. Estas incluyen pestañas a la izquierda, arriba, en el asistente y acordeón. Cada navegador tiene una clase diferente.

<table>
 <tbody>
  <tr>
   <td><p><strong>Navegador</strong></p> </td>
   <td><p><strong>Clase de CSS</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>Accordion</code></p> </td>
   <td><p>.acordion-navigators</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the left</code></p> </td>
   <td><p>.tab-navigators-vertical</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the top</code></p> </td>
   <td><p>.tab-navigators</p> </td>
  </tr>
  <tr>
   <td><p><code>Wizard</code></p> </td>
   <td><p>.wizard-navigators</p> </td>
  </tr>
 </tbody>
</table>

El siguiente es el código HTML para el elemento del navegador de pestañas (similar a las pestañas de arranque):

`<li>`

`<a>tab title</a>`

`</li>`

`Accordion navigator is an exception, it has following barebone`

`structure:`

`<div class="accordion.navigators">`

`<div>`

`<div class = "guideHeader">`

`<a>`

`<span class = "guideSummary" ></code>`

`........................... repeatable buttons, if the repeatable configuration is set ................................`

`<div class = "repeatableButtons">`

`<button name="Add" class="Add"/>`

`<button name="Remove" class="Remove"/>`

`</div>`

`</a>`

`</div>`

`................................ panel content ..................................`

`</div>`

`</div>`

Puede cambiar el estilo del navegador mediante reglas CSS que seleccionen los elementos con selectores **descenant**. Por ejemplo, para añadir un estilo de decoración de texto a la etiqueta de anclaje:

Navegador de pestañas en la parte superior:

`.tab-navigators`

`li a {`

`text-decoration:`

`underline;`

`}`

`Tab navigator on left:`

`.tab-navigators-vertical`

`li a {`

`text-decoration:`

`underline;`

`}`

`Accordion navigator:`

`.accordion-navigators .guideHeader a .guideSummary {`

`text-decoration:`

`underline;`

`}`

`Wizard navigator:`

`.wizard-navigators`

`li a {`

`text-decoration:`

`underline;`

`}`

Además, hay clases para aplicar estilo a los navegadores de pestañas (tanto izquierda como superior) en función de si tienen anidados/secundarios/subnavegadores.

<table>
 <tbody>
  <tr>
   <td><p><strong>Clase de CSS</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>nested_true</code></p> </td>
   <td><p>Navegadores de pestañas (izquierda y arriba) que tienen anidados/secundarios/subnavegadores</p> </td>
  </tr>
  <tr>
   <td><p><code>nested_false</code></p> </td>
   <td><p>Navegadores de pestañas (izquierda y superior) que no tienen anidados/secundarios/subnavegadores</p> </td>
  </tr>
 </tbody>
</table>

La clase guidenavIcon proporciona un icono predeterminado para los navegadores de pestañas (izquierda y superior) y los navegadores del asistente.

<table>
 <tbody>
  <tr>
   <td><p><strong>Clase de CSS </strong></p> </td>
   <td><p><code>guideNavIcon</code></p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Puede cambiar el icono de un navegador concreto proporcionando una clase CSS en el panel de creación, como por ejemplo &lt;CLASS_NAME>. Agregue un **&lt;CLASS_NAME>_nav** para el icono del navegador.

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>Navegadores de pestañas</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>navigator-bg-color</code></p> </td>
   <td><p>Color de fondo para todo el navegador de pestañas</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bg-color</code></p> </td>
   <td><p>Color de fondo de la ficha</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-color</code></p> </td>
   <td><p>Color de fuente de la ficha</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-hover-bg-color</code></p> </td>
   <td><p>Color de fondo de la ficha al pasar el ratón por encima</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-hover-font-color</code></p> </td>
   <td><p>Color de fuente para la ficha al pasar el ratón por encima</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-active-bg-color</code></p> </td>
   <td><p>Color de fondo cuando el panel está enfocado (activo)</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-active-font-color</code></p> </td>
   <td><p>Color de fuente cuando el panel está enfocado</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-bg-color</code></p> </td>
   <td><p>Color de fondo cuando la expresión de finalización del panel devuelve verdadero</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-font-color</code></p> </td>
   <td><p>Color de fuente cuando la expresión de finalización del panel devuelve verdadero</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-bg-color</code></p> </td>
   <td>Color de fondo cuando el panel ha estado enfocado una vez, pero la expresión de finalización devuelve el valor false </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-font-color</code></p> </td>
   <td>Color de fuente cuando el panel ha estado seleccionado una vez, pero la expresión de finalización devuelve el valor false </td>
  </tr>
  <tr>
   <td><p><code>tabs-border-color</code></p> </td>
   <td><p>Color de borde de la pestaña</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-size</code></p> </td>
   <td><p>Tamaño de fuente de la ficha</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-padding</code></p> </td>
   <td><p>Relleno para la pestaña</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-margin</code></p> </td>
   <td><p>Margen para la pestaña</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-vertical-margin</code></p> </td>
   <td><p>Margen de las pestañas verticales</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-border-thickness</code></p> </td>
   <td><p>Tamaño del borde de las pestañas</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-min-height</code></p> </td>
   <td><p>Altura mínima de las pestañas</p> </td>
  </tr>
  <tr>
   <td><p><code>heirarichal-indent</code></p> </td>
   <td><p>Sangría para las pestañas anidadas</p> </td>
  </tr>
  <tr>
   <td><p><strong>Navegadores de asistente</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-navigator-bg-color</code></p> </td>
   <td>Color de fondo para todo el navegador del asistente</td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-bg-color</code></p> </td>
   <td><p>Color de fondo del asistente</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-color</code></p> </td>
   <td><p>Color de fuente para el asistente</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-active-bg-color</code></p> </td>
   <td><p>Color de fondo cuando el panel está enfocado (activo)</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-active-font-color</code></p> </td>
   <td><p>Color de fuente cuando el panel está enfocado (centrado)</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-bg-color</code></p> </td>
   <td><p>Color de fondo cuando la expresión de finalización del panel devuelve verdadero</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-font-color</code></p> </td>
   <td><p>Color de fuente cuando la expresión de finalización del panel devuelve verdadero</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-bg-color</code></p> </td>
   <td>Color de fondo cuando el panel ha estado enfocado una vez, pero la expresión de finalización devuelve el valor false</td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-font-color</code></p> </td>
   <td><p>Color de fuente cuando el panel se ha centrado una vez, pero la expresión de finalización devuelve false</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-color</code></p> </td>
   <td><p>Color del asistente</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-size</code></p> </td>
   <td><p>Tamaño de fuente del asistente</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-padding</code></p> </td>
   <td><p>Relleno para el asistente</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-thickness</code></p> </td>
   <td><p>Tamaño del borde del asistente</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-nav-bullet-border</code></p> </td>
   <td><p>Color del borde de la viñeta del navegador del asistente (prefiriendo el rótulo/etiqueta)</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-bg-color</code></p> </td>
   <td><p>Color de fondo de la barra de progreso del navegador del asistente</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-color</code></p> </td>
   <td><p>Color de relleno para la barra de progreso</p> </td>
  </tr>
  <tr>
   <td><p><strong>Navegadores de acordeón</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>accordion-tabs-padding</code></p> </td>
   <td><p>Relleno para acordeón</p> </td>
  </tr>
 </tbody>
</table>

## Estilo de panel {#panel-styling}

Un panel incluye una barra de herramientas opcional y su contenido.

<table>
 <tbody>
  <tr>
   <td><p><strong>Clase de CSS </strong></p> </td>
   <td><p><code>guidePanelNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>panel-background-color</code></p> </td>
   <td><p>Color de fondo del panel</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-font-size</code></p> </td>
   <td><p>Tamaño de fuente del texto del panel</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-font-color</code></p> </td>
   <td><p>Color de fuente para el texto del panel<br /> </p> </td>
  </tr>
  <tr>
   <td><p><code>panel-padding</code></p> </td>
   <td><p>Relleno dentro del panel</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-font-size</code></p> </td>
   <td><p>Tamaño de fuente de la descripción del panel</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-padding</code></p> </td>
   <td><p>Relleno de la descripción del panel</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-help-bg-color</code></p> </td>
   <td><p>Color de fondo para la ayuda del panel</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-help-border-indicator-color</code></p> </td>
   <td><p>Color del borde indicador para la ayuda del panel</p> </td>
  </tr>
 </tbody>
</table>

El nodo del panel se divide en navegadores y contenido. No existe `` `` un componente de estilo independiente para el contenido. Las variables descritas se aplican tanto en el navegador como en el contenido.

El panel superior (RootPanel) no tiene esta clase.

## Estilo móvil {#mobile-styling}

## Barra de encabezado {#header-bar}

Estas variables influyen en la barra de encabezado que es visible en un dispositivo móvil o en dispositivos de pantalla pequeña que contienen título de panel y navegadores siguientes y posteriores.

<table>
 <tbody>
  <tr>
   <td><p><strong>Clase de CSS </strong></p> </td>
   <td><p><code>guide-header-bar</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-background-color</code></p> </td>
   <td><p>Color de fondo de la barra de encabezado</p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-font-color</code></p> </td>
   <td><p>Color de fuente para el texto dentro de la barra de encabezado</p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-padding</code></p> </td>
   <td><p>Relleno para barra de encabezado</p> </td>
  </tr>
 </tbody>
</table>

## Indicador de desplazamiento {#scroll-indicator}

Estas variables influyen en el indicador de desplazamiento, que es una flecha naranja que aparece en un dispositivo móvil o en dispositivos de pantalla pequeña. Un indicador de desplazamiento indica que hay contenido más allá de la parte visible de la pantalla. Puede desplazarse hacia abajo para verlo. Cuando llega al final del contenido, la flecha desaparece.

<table>
 <tbody>
  <tr>
   <td><p><strong>Clase de CSS </strong></p> </td>
   <td><p><code>mobileScrollIndicator</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorBottom</code></p> </td>
   <td><p>Posición fija del indicador de desplazamiento desde la parte inferior</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorRight</code></p> </td>
   <td><p>Posición fija del indicador de desplazamiento desde la derecha</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorWidth</code></p> </td>
   <td><p>Anchura del indicador de desplazamiento</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorHeight</code></p> </td>
   <td><p>Altura del indicador de desplazamiento</p> </td>
  </tr>
 </tbody>
</table>

## Variables específicas del diseño de la barra de herramientas fija y móvil {#mobile-fixed-toolbar-layout-specific-variables}

Estas variables de la siguiente tabla influyen en el diseño de la barra de herramientas fija móvil.

<table>
 <tbody>
  <tr>
   <td><p><strong>Clase de CSS </strong></p> </td>
   <td><p><code>mobileToolbar</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarBottom</code></p> </td>
   <td><p>Posición fija de la barra de herramientas, en el dispositivo móvil, desde la parte inferior</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarTop</code></p> </td>
   <td><p>Posición fija de la barra de herramientas, en el dispositivo móvil, desde la parte superior</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarLeft</code></p> </td>
   <td><p>Posición fija de la barra de herramientas, en el dispositivo móvil, desde la izquierda</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarRight</code></p> </td>
   <td><p>Posición fija de la barra de herramientas, en el dispositivo móvil, desde la derecha</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconTopMargin</code></p> </td>
   <td><p>Posición fija del icono de botones de la barra de herramientas, desde la parte superior</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconWidth</code></p> </td>
   <td><p>Anchura del icono de botones de la barra de herramientas en el dispositivo móvil</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconHeight</code></p> </td>
   <td><p>Altura del icono de botones de la barra de herramientas en el dispositivo móvil</p> </td>
  </tr>
  <tr>
   <td><p><code>mobilefixedtoolbarbgcolor</code></p> </td>
   <td><p>Color de fondo de la barra de herramientas en dispositivos móviles</p> </td>
  </tr>
 </tbody>
</table>

## Variable específica del tema {#theme-specific-variable}

El tema **Simple ensubscription** en /etc/clientlibs/fd/af/guidetheme/simpleEnscriptions y la categoría `guide.theme.simpleEnrollment` también presentan algunas variables. Si desea crear un tema para mejorar la inscripción simple, puede utilizar las siguientes &quot;variables adicionales&quot;:

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>button-focus-bg-color</code></p> </td>
   <td><p>Color de fondo para el foco del botón</p> </td>
  </tr>
  <tr>
   <td><p><code>button-hover-bg-color</code></p> </td>
   <td><p>Color de fondo para el botón al pasar el ratón por encima</p> </td>
  </tr>
  <tr>
   <td><p><code>button-radius</code></p> </td>
   <td><p>Radio del botón</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-color</code></p> </td>
   <td><p>Color de fondo de los botones de navegación (atrás/siguiente)</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-hover-color</code></p> </td>
   <td><p>Color de fondo de los botones de navegación (atrás/siguiente) al pasar el ratón por encima</p> </td>
  </tr>
  <tr>
   <td><p><code>initial-nav-color</code></p> </td>
   <td><p>Color de fondo para los navegadores del asistente y la barra de progreso correspondiente, al procesarse por primera vez.</p> </td>
  </tr>
  <tr>
   <td><p><code>active-nav-color</code></p> </td>
   <td>Color de fondo para el navegador de asistente actual/activo y la barra de progreso correspondiente </td>
  </tr>
  <tr>
   <td><p><code>visited-nav-color</code></p> </td>
   <td><p>Color de fondo para los navegadores del asistente y la barra de progreso correspondiente, que se han visitado.</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bifercating-border-color</code></p> </td>
   <td><p>Color de borde bifurcar contenedor en navegadores y panel</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-navigator-separator-color</code></p> </td>
   <td><p>Color del borde inferior que separa las pestañas de la izquierda (navegadores de pestañas).</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-child-nav-bg-color</code></p> </td>
   <td><p>Color de fondo para los navegadores anidados/secundarios/secundarios anidados del navegador</p> </td>
  </tr>
 </tbody>
</table>

