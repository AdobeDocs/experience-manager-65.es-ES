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
translation-type: tm+mt
source-git-commit: 5a76200a573d95026e2347d2049a089d975b5619
workflow-type: tm+mt
source-wordcount: '2322'
ht-degree: 3%

---


# Construcciones de estilo para formularios adaptables{#styling-constructs-for-adaptive-forms}

## Requisitos previos {#prerequisites}

Conocimiento de CSS y del marco LESS.

## Qué se puede personalizar {#what-can-be-customized}

El artículo lista clases css de formularios adaptables disponibles al público. Puede aprovechar estas clases para aplicar estilo a varios componentes de un formulario adaptable. El estilo de los componentes de creación, como cuadros de diálogo y barras de estado que muestran advertencias, está fuera del alcance de este artículo. Utilice estas construcciones de estilo para crear estilos (con CSS o Menos) solo cuando no pueda aplicar estilo a los componentes con [editor de temas](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html).

## Personalización de estilos en formularios adaptables {#customizing-styles-in-adaptive-forms}

El marco LESS simplifica el caso de uso para personalizar estilos en formularios adaptables. El marco permite definir estilos mediante un conjunto de variables y funciones (mezclas). El marco LESS ayuda a reducir el tamaño del código incorporado y aumenta su reutilización.

Puede personalizar los estilos de formulario adaptables de las siguientes formas:

* Cambiar el tema
* Cambiar el estilo del componente

## Cambio del tema {#changing-theme}

Puede cambiar el tema de un formulario adaptable para garantizar que su aspecto sea coherente con las páginas web en las que está incrustado el formulario adaptable.

Los cambios en el aspecto general del formulario adaptable que utiliza propiedades CSS suelen formar parte de los cambios del tema. Los cambios más importantes en el aspecto y funcionamiento del formulario adaptable, como los cambios en la presentación y la colocación de los componentes, no se consideran cambios de tema.

En función del bootstrap, el siguiente conjunto de propiedades CSS define el tema de una página web:

* Color de fondo
* Borde (tipo, color, grosor)
* Color de fuente
* Espacio
* imagen
* Tamaño de fuente
* LineHeight

Actualmente, las variables LESS se definen solo para estas propiedades de los distintos elementos de un formulario adaptable.

## Cambio del estilo de componente {#changing-component-style}

Puede realizar cambios en el aspecto, el diseño, la posición y la visibilidad de los elementos. Para lograr esta tarea, cree o actualice los archivos .css personalizados para incluir las construcciones de estilo enumeradas en este artículo.

Para aplicar un estilo a un formulario adaptable, abra el formulario adaptable en para editarlo y abra las propiedades del contenedor de formularios adaptables, especifique la ruta de acceso del archivo CSS personalizado en la ficha básica. Las construcciones de estilo predeterminadas del formulario adaptable y sustituidas por las construcciones enumeradas en el archivo .css personalizado.

## Componentes {#components}

Los componentes analizados en este artículo tienen sus clases CSS predefinidas. Puede editar las variables para modificar los estilos en las clases CSS. Como alternativa, puede volver a escribir toda la clase. En esta sección se describen las clases de los componentes y los estilos que se pueden modificar mediante variables.

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

Los campos incluyen etiquetas, utilidades, descripción de la ayuda (descripción larga y breve) e iconos de ayuda de campo (signo de interrogación).

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

El elemento HTML **label** utilizado para el campo incluye las clases **left** o **top** según si la etiqueta está en la parte superior o en la izquierda.

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
   <td>Propiedad de peso de fuente CSS para la etiqueta de campo </td>
  </tr>
  <tr>
   <td><p><code>label-margin</code></p> </td>
   <td><p>Margen de la etiqueta de campo</p> </td>
  </tr>
 </tbody>
</table>

Las reglas CSS de la etiqueta se aplican mediante la etiqueta **guideFieldLabel**. Si es un autor, sobrescriba esta regla para que los cambios personalizados sean visibles.

## Estilo de utilidades {#widgets-styling}

Según el tipo, las utilidades también incluyen clases. Normalmente, los widgets incluyen la clase `guideFieldWidget`. Los widgets que se envían con HTML normalmente utilizan la entrada y selección de elementos HTML estándar. El estilo se realiza en consecuencia. No se puede aplicar estilo a una utilidad personalizada cambiando las variables.

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
   <td>Color de fondo para los widgets (no funciona para la casilla de verificación y el botón de radio)</td>
  </tr>
  <tr>
   <td><p><code>widgets-border-color</code></p> </td>
   <td><p>Color del borde de los widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-thickness</code></p> </td>
   <td><p>Tamaño del borde de los widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-radius</code></p> </td>
   <td><p>Radio del borde de los widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-type</code></p> </td>
   <td><p>Tipo de borde de los widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-border-focus-type</code></p> </td>
   <td><p>Tipo de enfoque para bordes de widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border</code></p> </td>
   <td><p>Estilo de borde consolidado de widgets</p> </td>
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
   <td>Propiedad de lineheight CSS para la utilidad </td>
  </tr>
  <tr>
   <td><p><code>widgets-padding</code></p> </td>
   <td><p>Propiedad de relleno CSS para la utilidad</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-focus-border-color</code></p> </td>
   <td><p>Color del borde cuando el widget está en foco</p> </td>
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
   <td>Altura del widget (no funciona con la casilla de verificación y el botón de radio)</td>
  </tr>
  <tr>
   <td><p><code>checkbutton-height</code></p> </td>
   <td><p>Altura de la casilla de verificación y del botón de radio.</p> </td>
  </tr>
  <tr>
   <td><p><code>listboxwidget-height</code></p> </td>
   <td><p>Altura máxima de un menú desplegable de selección múltiple</p> </td>
  </tr>
 </tbody>
</table>

### Limitaciones en el estilo de utilidades {#limitations-in-widget-styling}

El estilo de los campos seleccionados, obligatorios y desactivados se restringe mediante variables. Sin embargo, puede cambiarlo anulando los estilos. La restricción mediante variables se proporciona principalmente para mantener el número de variables bajo control. La restricción se puede relajar si el aspecto de un campo cambia drásticamente porque está en cualquiera de los estados mencionados anteriormente.

## Descripción de la ayuda {#help-description}

Un autor puede especificar el contenido de la Ayuda en los campos mediante los componentes de descripción breve y larga. Ambos componentes tienen una clase común `.guideHelpDescription` y otra clase `.long`/ `.short`, según el tipo de descripción. El contenido de la Ayuda se incluye en un elemento de párrafo para anular el estilo de la descripción. La descripción de la Ayuda (larga y corta) se modifica mediante variables que empiezan por widgetshelp, como se indica en la siguiente tabla:

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
   <td><p>Color del borde de la ayuda larga de los widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-indicator-color</code></p> </td>
   <td><p>Color del borde del indicador izquierdo de la Ayuda larga de los widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-bg-color</code></p> </td>
   <td><p>Color de fondo de la breve ayuda de los widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-color</code></p> </td>
   <td><p>Color de fuente de la breve ayuda de los widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-bg-color</code></p> </td>
   <td><p>Color de fondo de la ayuda de información de objeto breve de los widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-color</code></p> </td>
   <td><p>Color de fuente de la ayuda de información de objeto corta de los widgets</p> </td>
  </tr>
 </tbody>
</table>

## Términos y condiciones {#terms-and-conditions}

La utilidad Términos y condiciones (TnC `` ``) permite especificar términos y condiciones. Puede personalizar la utilidad con las variables descritas en la tabla siguiente.

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

Los botones también son widgets. Sin embargo, su estilo es ligeramente distinto al de los widgets. En los formularios adaptables, cualquiera de los siguientes elementos constituye un botón:

* input[type = text]
* botón
* elemento con clase .button

Código HTML para el botón:

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
   <td><p>Relleno para botones pequeños (botones con clase .buttonsmall)</p> </td>
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
   <td><p>Color del borde para botones informativos</p> </td>
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
   <td><p>Color de borde para botones con estilo de advertencia</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-background-color</code></p> </td>
   <td><p>Color de fondo para los botones de alerta (botones con clase .buttonalert)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-font-color</code></p> </td>
   <td><p>Color de fuente para botones de alerta</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-border-color</code></p> </td>
   <td><p>Color del borde para los botones de alerta</p> </td>
  </tr>
 </tbody>
</table>

## Signo de interrogación {#question-mark}

Para las utilidades, se muestra un questionMark cuando un autor agrega una descripción larga en el contenido de la Ayuda. Se utiliza el icono predeterminado que se proporciona en bootstrap. Para utilizar un icono personalizado, puede personalizar los iconos de arranque.

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

Puede cambiar el tema de color de las filas de encabezado y de trabajo en una tabla mediante las siguientes variables.

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
   <td><p>Color de fondo de la fila de trabajo impar. El valor predeterminado es <code>rgb(255, 255, 255)</code>.</p> </td>
  </tr>
  <tr>
   <td><p><code>table-even-row-bg-color</code></p> </td>
   <td><p>Color de fondo para la fila de trabajo par. El valor predeterminado es <code>#eee</code>.</p> </td>
  </tr>
 </tbody>
</table>

## Archivo adjunto {#file-attachment}

El widget de archivos adjuntos de formularios adaptables permite cargar archivos. También puede personalizar la utilidad con las variables.

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemPadding</code></p> </td>
   <td><p>Relleno para los archivos que se muestran en la utilidad</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemBackground</code></p> </td>
   <td><p>Color de fondo del elemento de archivo</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemBorderColor</code></p> </td>
   <td><p>Color del borde superior</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemColor</code></p> </td>
   <td><p>Color de fuente del elemento de archivo</p> </td>
  </tr>
  <tr>
   <td><p><code>filePreviewIconColor</code></p> </td>
   <td><p>Color del icono de Previsualización (icono de Bootstrap) del widget</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemCommentHeight</code></p> </td>
   <td><p>Altura del comentario del elemento de archivo</p> </td>
  </tr>
 </tbody>
</table>

## Estilos del navegador {#navigator-styles}

Existen cuatro tipos de fichas del navegador. Estas incluyen fichas a la izquierda, arriba, en el asistente y acordeón. Cada navegador tiene una clase diferente.

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
   <td><p>.Wizard-navigators</p> </td>
  </tr>
 </tbody>
</table>

El siguiente es el código HTML del elemento de navegador de fichas (similar a las fichas de arranque):

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

Puede cambiar el estilo del navegador mediante reglas CSS que seleccionan los elementos mediante selectores **descendant**. Por ejemplo, para agregar un estilo de decoración de texto a la etiqueta de anclaje:

Navegador de fichas en la parte superior:

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

Además, hay clases para aplicar estilo a los navegadores de fichas (tanto a la izquierda como a la parte superior) en función de si tienen navegadores anidados/secundarios/secundarios.

<table>
 <tbody>
  <tr>
   <td><p><strong>Clase de CSS</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>nested_true</code></p> </td>
   <td><p>Navegadores de fichas (izquierda y arriba) que tienen navegadores anidados/secundarios/secundarios</p> </td>
  </tr>
  <tr>
   <td><p><code>nested_false</code></p> </td>
   <td><p>Navegadores de fichas (izquierda y arriba) que no tienen navegadores anidados/secundarios/secundarios</p> </td>
  </tr>
 </tbody>
</table>

La clase guideNavIcon proporciona un icono predeterminado para los navegadores de tabuladores (tanto izquierdos como superiores) y los navegadores de asistente.

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
   <td><p><strong>Navegadores de fichas</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>navigator-bg-color</code></p> </td>
   <td><p>Color de fondo para todo el navegador de fichas</p> </td>
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
   <td><p>Color de fondo de la ficha al pasar el ratón</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-hover-font-color</code></p> </td>
   <td><p>Color de fuente de la ficha al pasar el ratón</p> </td>
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
   <td>Color de fondo cuando el panel ha estado seleccionado una vez pero la expresión de finalización devuelve false </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-font-color</code></p> </td>
   <td>Color de fuente cuando el panel ha estado seleccionado una vez pero la expresión de finalización devuelve false </td>
  </tr>
  <tr>
   <td><p><code>tabs-border-color</code></p> </td>
   <td><p>Color del borde de la ficha</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-size</code></p> </td>
   <td><p>Tamaño de fuente de la ficha</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-padding</code></p> </td>
   <td><p>Relleno para la ficha</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-margin</code></p> </td>
   <td><p>Margen de la ficha</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-vertical-margin</code></p> </td>
   <td><p>Margen de las fichas verticales</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-border-thickness</code></p> </td>
   <td><p>Tamaño del borde de las fichas</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-min-height</code></p> </td>
   <td><p>Altura mínima de las fichas</p> </td>
  </tr>
  <tr>
   <td><p><code>heirarichal-indent</code></p> </td>
   <td><p>Sangría para las fichas anidadas</p> </td>
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
   <td>Color de fondo cuando el panel ha estado seleccionado una vez pero la expresión de finalización devuelve false</td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-font-color</code></p> </td>
   <td><p>Color de fuente cuando el panel se ha seleccionado una vez pero la expresión de finalización devuelve false</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-color</code></p> </td>
   <td><p>Color del asistente</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-size</code></p> </td>
   <td><p>Tamaño de fuente para el asistente</p> </td>
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
   <td><p>Color del borde de la viñeta del navegador del asistente (anteponer el rótulo o la etiqueta)</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-bg-color</code></p> </td>
   <td><p>Color de fondo de la barra de progreso del navegador del asistente</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-color</code></p> </td>
   <td><p>Color de relleno de la barra de progreso</p> </td>
  </tr>
  <tr>
   <td><p><strong>Exploradores de acordeón</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>accordion-tabs-padding</code></p> </td>
   <td><p>Relleno para acordeón</p> </td>
  </tr>
 </tbody>
</table>

## Estilo del panel {#panel-styling}

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
   <td><p>Color de fuente del texto del panel<br /> </p> </td>
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
   <td><p>Color del borde del indicador para la ayuda del panel</p> </td>
  </tr>
 </tbody>
</table>

El nodo del panel se divide en navegadores y contenido. No existe `` `` un componente de estilo independiente para el contenido. Las variables descritas se aplican tanto al navegador como al contenido.

El panel superior (RootPanel) no tiene esta clase.

## Estilo móvil {#mobile-styling}

## Barra de encabezado {#header-bar}

Estas variables influyen en la barra de encabezado que está visible en un dispositivo móvil o en dispositivos de pantalla pequeña que contienen el título del panel y los navegadores siguiente y posterior.

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
   <td><p>Color de fuente del texto dentro de la barra de encabezado</p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-padding</code></p> </td>
   <td><p>Relleno para barra de encabezado</p> </td>
  </tr>
 </tbody>
</table>

## Indicador de desplazamiento {#scroll-indicator}

Estas variables influyen en el indicador de desplazamiento, que es una flecha naranja que aparece en un dispositivo móvil o en dispositivos de pantalla pequeños. Un indicador de desplazamiento indica que hay contenido más allá de la parte visible de la pantalla. Puede desplazarse hacia abajo para verlo. Cuando se llega al final del contenido, la flecha desaparece.

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
   <td><p>Ancho del indicador de desplazamiento</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorHeight</code></p> </td>
   <td><p>Altura del indicador de desplazamiento</p> </td>
  </tr>
 </tbody>
</table>

## Variables específicas del diseño de la barra de herramientas fijas móviles {#mobile-fixed-toolbar-layout-specific-variables}

Estas variables de la tabla siguiente influyen en el diseño de la barra de herramientas fija móvil.

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
   <td><p>Posición fija de la barra de herramientas, en dispositivos móviles, desde la parte inferior</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarTop</code></p> </td>
   <td><p>Posición fija de la barra de herramientas, en dispositivos móviles, desde la parte superior</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarLeft</code></p> </td>
   <td><p>Posición fija de la barra de herramientas, en el dispositivo móvil, desde la izquierda</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarRight</code></p> </td>
   <td><p>Posición fija de la barra de herramientas, en dispositivos móviles, desde la derecha</p> </td>
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

El tema de **inscripción simple** en /etc/clientlibs/fd/af/guide/simpleEnregistration y la categoría `guide.theme.simpleEnrollment` también presentan algunas variables. Si desea crear un tema que mejore la inscripción simple, puede utilizar las siguientes &quot;variables adicionales&quot;:

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>button-focus-bg-color</code></p> </td>
   <td><p>Color de fondo del botón al foco</p> </td>
  </tr>
  <tr>
   <td><p><code>button-hover-bg-color</code></p> </td>
   <td><p>Color de fondo del botón al pasar el ratón</p> </td>
  </tr>
  <tr>
   <td><p><code>button-radius</code></p> </td>
   <td><p>Radio del botón</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-color</code></p> </td>
   <td><p>Color de fondo para los botones de navegación (atrás/siguiente)</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-hover-color</code></p> </td>
   <td><p>Color de fondo para los botones de navegación (atrás/siguiente) al pasar el ratón</p> </td>
  </tr>
  <tr>
   <td><p><code>initial-nav-color</code></p> </td>
   <td><p>Color de fondo para los navegadores del asistente y la barra de progreso correspondiente, cuando se procesa por primera vez.</p> </td>
  </tr>
  <tr>
   <td><p><code>active-nav-color</code></p> </td>
   <td>Color de fondo para el navegador del asistente actual o activo y la correspondiente barra de progreso </td>
  </tr>
  <tr>
   <td><p><code>visited-nav-color</code></p> </td>
   <td><p>Color de fondo para los navegadores del asistente y la barra de progreso correspondiente, que se han visitado.</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bifercating-border-color</code></p> </td>
   <td><p>Contenedor de bifurcación de color de borde en navegadores y panel</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-navigator-separator-color</code></p> </td>
   <td><p>Color del borde inferior que separa las fichas de la izquierda (navegadores de fichas).</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-child-nav-bg-color</code></p> </td>
   <td><p>Color de fondo para los navegadores anidados/secundarios/secundarios del navegador</p> </td>
  </tr>
 </tbody>
</table>

