---
title: Creación y uso de temáticas
seo-title: Creating and using themes
description: Puede utilizar temas para estilizar y proporcionar una identidad visual a una forma adaptativa o de comunicación interactiva. Puede compartir un tema en cualquier cantidad de formularios adaptables o comunicaciones interactivas.
seo-description: You can use themes to stylize and provide a visual identity to an adaptive form or interactive communication. You can share a theme across any number of adaptive forms or interactive communications.
uuid: 88b6b6fd-181b-48c5-ac15-2b37592bd14b
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop, interactive-communications
content-strategy: max-2018
discoiquuid: 770e9174-b648-462a-abe9-05fefa967d86
docset: aem65
feature: Adaptive Forms
exl-id: 93c360a8-a9d9-4c4b-b7e2-2c44eaf4604c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '6026'
ht-degree: 68%

---

# Creación y uso de temáticas {#creating-and-using-themes}

## Introducción {#introduction}

Puede crear y aplicar temas para diseñar un formulario adaptable o una comunicación interactiva. Una temática contiene detalles de estilo para los componentes y paneles. Los estilos incluyen propiedades como colores de fondo, colores de estado, transparencia, alineación y tamaño. Al aplicar un tema, el estilo especificado se refleja en los componentes correspondientes. Los temas se administran de forma independiente sin hacer referencia a una forma adaptativa o de comunicación interactiva.

Puede hacer lo siguiente:

* Creación de un tema
* Editar y copiar un tema existente
* Descargar y cargar un tema existente en el servidor de AEM Forms
* Administrar dependencias para un tema

## Creación, descarga o carga de una temática {#creating-downloading-or-uploading-a-theme}

Con AEM Forms, puede crear, descargar o cargar temas. Se crea una temática como otros recursos, como formularios, documentos y cartas. El tema se guarda como una entidad independiente, con metapropiedades como los formularios. El hecho de que los temas sean una entidad independiente permite su reutilización en varios formularios adaptables y comunicaciones interactivas. También puede mover un tema a una instancia diferente de AEM Forms y reutilizarlo.

### Creación de una temática {#creating-a-theme}

Siga estos pasos para crear un tema:

1. Haga clic en **Adobe Experience Manager**, luego en **Forms** y, por último, en **Temáticas**.

1. En la página Temáticas, haga clic en **Crear > Temática**. 
Se inicia un asistente para crear una temática.

1. En la pestaña Básico del asistente Crear tema , proporcione **Título** y **Nombre** del tema. Son campos obligatorios.

1. En la pestaña Advanced , se obtienen dos campos:

   * **Ubicación de Clientlib**: Ubicación en el repositorio que almacena las clientlibs para el tema.

   * **Categoría de Clientlib**: Proporciona un campo de texto para introducir el nombre de categoría clientlib para el tema.

1. Haga clic en **Crear** y luego en **Editar** para abrir la temática en el editor de temáticas, o haga clic en **Listo** para volver a la página de temáticas.

### Descargar una temática {#downloading-a-theme}

Puede exportar temas como archivo zip y utilizarlos en otros proyectos o AEM instancias. Para descargar una temática:

1. Haga clic en **Adobe Experience Manager**, luego en **Forms** y, por último, en **Temáticas**.

1. En la página Temáticas, **seleccione** una y haga clic en **Descargar**. Se muestra un cuadro de diálogo con los detalles de la temática.

1. Haga clic en **Descargar**. La temática se descarga como archivo zip.

>[!NOTE]
>
>Si descarga un tema que tiene un formulario adaptable asociado y el formulario adaptable asociado se basa en una plantilla personalizada, también descargue la plantilla personalizada. Al cargar el tema descargado y el formulario adaptable en un servidor de AEM Forms, cargue también la plantilla personalizada relacionada.

### Cargar una temática {#uploading-a-theme}

Puede utilizar las temáticas creadas con ajustes preestablecidos de estilo en su proyecto. Puede importar paquetes de temáticas que otros creen cargándolos en su proyecto.

Para cargar una temática:

1. Haga clic en **Adobe Experience Manager**, luego en **Forms** y, por último, en **Temáticas**.

1. En la página Temáticas, haga clic en **Crear > Cargar archivo**.
1. En la solicitud de carga de archivos, examine y seleccione un paquete de temáticas en el equipo y haga clic en **Cargar**. 
La temática cargada está disponible en la página de temáticas.

## Metadatos de una temática {#metadata-of-a-theme}

Lista de metapropiedades de una temática (que se encuentran en la página de propiedades de una temática).

<table>
 <tbody>
  <tr>
   <th><p><strong>ID</strong></p> <p> </p> </th>
   <th><strong>Nombre</strong></th>
   <th><strong>Se puede editar</strong></th>
   <th><strong>Descripción de la propiedad</strong></th>
  </tr>
  <tr>
   <td>1.</td>
   <td>Título</td>
   <td>Sí</td>
   <td>Nombre para mostrar de la temática.</td>
  </tr>
  <tr>
   <td>2.</td>
   <td>Descripción</td>
   <td>Sí</td>
   <td>Descripción de la temática.</td>
  </tr>
  <tr>
   <td>3.</td>
   <td>Tipo</td>
   <td>No</td>
   <td>
    <ul>
     <li>Tipo de recurso.</li>
     <li>El valor siempre es Temática.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>4.</td>
   <td>Creado</td>
   <td>No</td>
   <td>Fecha de creación de la temática</td>
  </tr>
  <tr>
   <td>5.</td>
   <td>Nombre de autor</td>
   <td>Sí</td>
   <td>Autor de la temática. Se calcula en el momento de la creación de la temática.</td>
  </tr>
  <tr>
   <td>6.</td>
   <td>Fecha de última modificación</td>
   <td>No</td>
   <td>Fecha en la que se modificó la temática por última vez.</td>
  </tr>
  <tr>
   <td>7.</td>
   <td>Estado</td>
   <td>No</td>
   <td>Estado de la temática (modificada/publicada).</td>
  </tr>
  <tr>
   <td>8.</td>
   <td>Hora de publicación activada</td>
   <td>Sí</td>
   <td>Hora a la que publicar automáticamente la temática.</td>
  </tr>
  <tr>
   <td>9.</td>
   <td>Hora de publicación desactivada</td>
   <td>Sí</td>
   <td>Hora a la que cancelar automáticamente la publicación de la temática.</td>
  </tr>
  <tr>
   <td>10.</td>
   <td>Etiquetas</td>
   <td>Sí</td>
   <td>Etiqueta de identificación adjunta a la temática que se utiliza para mejorar la búsqueda.</td>
  </tr>
  <tr>
   <td>11.</td>
   <td>Referencias</td>
   <td>Vínculos</td>
   <td>
    <ul>
     <li>Contiene la sección "Remitido por". Enumera los formularios que utilizan el tema.</li>
     <li>Dado que el tema no hace referencia a ningún otro recurso, no hay sección "Referencias".</li>
    </ul> </td>
  </tr>
  <tr>
   <td>12.</td>
   <td>Ubicación de biblioteca de cliente</td>
   <td>Sí</td>
   <td>
    <ul>
     <li>Ruta del repositorio definida por el usuario dentro de '/etc' donde se almacenan los clientlibs correspondientes a este tema.</li>
     <li>Valor predeterminado: '/etc/clientlibs/fd/themes' + ruta relativa del recurso del tema.</li>
     <li>Si la ubicación no existe, la jerarquía de carpetas se genera automáticamente.</li>
     <li>Cuando se cambia este valor, la estructura del nodo clientlib se mueve a la nueva ubicación introducida.<br /> <em><strong>Nota:</strong> Si cambia la ubicación clientlib predeterminada, en el repositorio CRXDE asigne <code>crx:replicate, rep:write, rep:glob:*, rep:itemNames:: js.txt, jcr:read </code>a <code>forms-users</code> y <code>crx:replicate</code>, <code>jcr:read </code>a <code>fd-service</code> en la nueva ubicación. Adjunte también otra ACL añadiendo <code>deny jcr:addChildNodes</code> para <code>forms-user</code></em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>13.</td>
   <td>Nombre de categoría de biblioteca de cliente</td>
   <td>Sí</td>
   <td>
    <ul>
     <li>El nombre de categoría clientlib definido por el usuario para este tema.</li>
     <li>Se muestra un error si el nombre ya está siendo utilizado por otro tema existente.</li>
     <li>Valor predeterminado: se calcula mediante la ubicación del tema.</li>
     <li>Cuando se cambia este valor, el nombre de la categoría se actualiza en el nodo clientlib correspondiente. No es necesario actualizar el nombre de categoría de Clientlib en los archivos jsp porque el nombre de categoría clientlib se utiliza como referencia.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Acerca del editor de temáticas {#about-the-theme-editor}

AEM Forms se envía con el Editor de temas. Es una interfaz fácil de usar para el usuario empresarial y el diseñador web/desarrollador que proporciona las funcionalidades necesarias para especificar fácilmente el estilo de varios elementos de comunicación interactivos y formularios adaptables. Cuando se crea un tema, se almacena como una entidad independiente, como formularios, comunicaciones interactivas, cartas, fragmentos de documento y diccionarios de datos.

El editor de temáticas permite personalizar estilos de los componentes diseñados en una temática. Puede personalizar el aspecto de un formulario o una comunicación interactiva en un dispositivo.

El editor de temáticas se divide en dos paneles:

* **Lienzo** - Aparece en el lado derecho. Muestra una forma adaptativa o comunicación interactiva de ejemplo en la que todos los cambios de estilo se reflejan instantáneamente. También puede seleccionar objetos directamente del lienzo para buscar los estilos asociados a ellos y editarlos. Una regla de resolución de dispositivo en la parte superior gobierna el lienzo. Al seleccionar un punto de interrupción de resolución en la regla, se muestra la vista previa del formulario de ejemplo o la comunicación interactiva para la resolución correspondiente. El lienzo se analiza en detalle [a continuación](../../forms/using/themes.md#using-canvas).

* **Barra lateral**- Aparece en el lado izquierdo. Tiene los siguientes elementos:

   * **Selector:** muestra el componente seleccionado para el estilo y sus propiedades que puede aplicar. El selector representa todos los componentes de un tipo. Si selecciona un componente de cuadro de texto en un tema para el estilo, todos los cuadros de texto del formulario o la comunicación interactiva heredarán el estilo. Los selectores permiten seleccionar un componente genérico o un componente específico para el estilo. Por ejemplo, un componente de campo es un componente genérico y un cuadro de texto es un componente específico.

      **Estilo del componente genérico:**
un campo puede ser un campo de cuadro numérico, como la edad, o un campo de cuadro de texto, como la dirección. 
Al aplicar estilo a un campo, se aplica a todos los campos, como edad, nombre y dirección.

      **Estilo de un componente específico**: un componente específico afecta a los objetos de la categoría específica. Cuando aplique estilo al componente de cuadro numérico en la temática, solo el objeto de cuadro numérico heredará el estilo.

      Por ejemplo, un campo de cuadro de texto como la dirección tiene una longitud mayor y un campo de cuadro numérico como la edad tiene una longitud menor. Puede seleccionar un campo de cuadro numérico, reducir su longitud y aplicarlo al formulario. La anchura de todos los campos numéricos de cuadro se reduce en el formulario.

      Al personalizar todos los componentes de campo con un color de fondo específico, todos los campos, como edad, nombre y dirección, heredan el color de fondo. Al seleccionar un cuadro numérico, como la edad, y reducir su anchura, se reduce la anchura de todos los cuadros numéricos, como la edad o el número de personas de una familia. La anchura de los cuadros de texto no cambia.

   * **Estado:** permite personalizar estilos de un objeto en un estado específico. Por ejemplo, puede especificar el aspecto que tendrá un objeto cuando esté en estado predeterminado, de enfoque, desactivado, de desplazamiento o de error.
   * **Categorías de las propiedades:** las propiedades de estilo se dividen en varias categorías. Por ejemplo, Dimensión y posición, Texto, Fondo, Borde y Efectos. En cada categoría, se proporciona información sobre el estilo. Por ejemplo, en Fondo, puede proporcionar Color de fondo e Imagen y degradado.

   * **Avanzado:** permite agregar CSS personalizado a un objeto, que anula las propiedades que los controles visuales definen si hay una superposición.

   * **Ver CSS**: permite ver el CSS del componente seleccionado
   Además, en la barra lateral, en la parte inferior hay una flecha. Al hacer clic en la flecha, aparecen dos opciones más: **Simular éxito** y **Simular error.** Estas opciones, junto con las opciones descritas anteriormente, se examinan en detalle [a continuación](../../forms/using/themes.md#using-rail).

[ ![Editor de temas con carril y lienzo resaltados.](assets/themes.png)](assets/themes-1.png) **A.** Barra lateral **B.** Lienzo

### Estilo de componentes {#styling-components}

Puede utilizar un tema en varios formularios adaptables y comunicaciones interactivas, lo que importa el formato de componente que haya especificado en el tema. Puede aplicar estilo a varios componentes, como títulos, descripciones, paneles, campos, iconos y cuadros de texto. Use widgets para configurar propiedades de componentes en una temática. Los conocimientos previos de CSS o LESS no son necesarios, pero se recomienda; aunque la sección Anulaciones de CSS le permite escribir código CSS o proporcionar selectores personalizados. La sección Anulaciones de CSS aparece cuando selecciona un componente en la barra lateral.

![Componentes a los que se puede dar estilo en la barra lateral](assets/stylable-components.png)

Opciones en la barra lateral que permiten seleccionar y aplicar estilo a distintos componentes.

Al hacer clic en el botón Editar de un componente en la barra lateral, se selecciona el componente en Lienzo y se le permite aplicar estilo al componente mediante las opciones de la barra lateral.

Algunos componentes, como el cuadro de texto, el cuadro numérico, el botón de opción y la casilla de verificación, se clasifican en componentes genéricos como Campo. Por ejemplo, desea personalizar el estilo de los botones de opción. Para seleccionar botones de opción para el estilo, seleccione **Campo > Widget > Botón de opción**.

Haga clic en **EXPANDIR TODO** en la barra lateral para ver, seleccione y aplique estilo a los componentes categorizados que no estén visibles al principio.

### Estilo de diseños de panel {#styling-panel-layouts-br}

Los temas de AEM Forms admiten el estilo de elementos en la presentación de paneles en los formularios y las comunicaciones interactivas. Se admite el estilo de elementos en diseños predeterminados y diseños personalizados.

Los paneles integrados incluyen:

* Pestañas izquierda
* Pestañas arriba
* Acordeón
* Interactiva
* Asistente
* Diseño móvil

   * Títulos del panel en el encabezado
   * Sin títulos del panel en el encabezado

Los selectores varían para cada diseño. 
Dar estilo a los diseños personalizados desde el editor de temáticas implica:

* Definición de los componentes para un diseño al que se pueda dar estilo y selectores CSS para identificar estos componentes de forma exclusiva
* Definición de las propiedades CSS que se pueden aplicar a estos componentes
* Definición del estilo de estos componentes de forma interactiva desde la interfaz de usuario

### Distintos estilos para diferentes tamaños de pantalla {#different-styles-for-different-screen-sizes-br}

Los diseños de escritorio y móviles pueden tener estilos ligera o totalmente diferentes. Los dispositivos móviles, tabletas y teléfonos comparten diseños similares, excepto para tamaños de componente.

Utilice los puntos de interrupción del editor de temáticas para definir un estilo alternativo para diferentes tamaños de pantalla. Puede seleccionar un dispositivo base o una resolución en la que comience a crear la temática, tras lo que las variaciones de estilo para otras resoluciones se generan automáticamente. Puede modificar explícitamente el estilo para todas las resoluciones.

>[!NOTE]
>
>El tema primero se crea mediante un formulario o comunicación interactiva y, a continuación, se aplica en diferentes formularios o comunicaciones interactivas. Los puntos de interrupción utilizados en la creación del tema pueden ser diferentes del formulario o de la comunicación interactiva en la que se aplica el tema. Las consultas de medios CSS se basan en el formulario o la comunicación interactiva utilizados en la creación del tema, y no en el formulario o la comunicación interactiva en la que se aplica el tema.

### El contexto de las propiedades de estilo cambia en la barra lateral al seleccionar objetos {#styling-properties-context-changes-in-sidebar-on-selecting-objects}

Al seleccionar un componente en el Lienzo, sus propiedades de estilo se muestran en la barra lateral. Seleccione el tipo de objeto y su estado y, a continuación, proporcione su estilo.

### Estilos utilizados recientemente en el Editor de temas {#recently-used-styles-in-theme-editor}

El editor de temas almacena en caché hasta 10 estilos aplicados a un componente. Puede utilizar los estilos en caché con otros componentes de una temática. Los estilos utilizados recientemente están disponibles justo debajo del componente seleccionado en la barra lateral como un cuadro de lista. Inicialmente, la lista de estilos utilizados recientemente está vacía.

![biblioteca de recursos](assets/asset-library.png)

Al aplicar estilo a un componente, los estilos se almacenan en caché y se enumeran en el cuadro de lista. En este ejemplo, la etiqueta del cuadro de texto incluye un estilo para cambiar el tamaño y el color de la fuente. Puede seguir pasos similares para elegir una imagen o cambiar los colores para aplicar estilo a un componente. Observe cómo el estilo se almacena en caché y se enumera en el cuadro de lista cuando se cambia de la etiqueta de campo.

![Estilo de fuente almacenado en caché para un componente disponible para otro](assets/font-style-cached.png)

En este ejemplo, se cambia el estilo de la etiqueta de campo y, cuando se selecciona Descripción del panel interactivo para el estilo, se añade una entrada de lista en la biblioteca de recursos. La entrada de la biblioteca de recursos se puede utilizar para cambiar el estilo de Descripción del panel interactivo.

Cuando se añade un estilo en la biblioteca de recursos, está disponible para otros temas y para el [modo de estilo](../../forms/using/inline-style-adaptive-forms.md) del editor de formularios o la interfaz de usuario del editor de comunicaciones interactivo. Del mismo modo, cuando se utiliza el modo de estilo del editor de formularios o la IU del editor de comunicaciones interactivo para aplicar estilo a un componente, el estilo se almacena en caché y está disponible en los temas.

El botón “+” de la biblioteca de recursos permite guardar de forma permanente el estilo con el nombre que proporcione. El botón “+” guarda el estilo aunque no haga clic en el botón Guardar de la barra lateral para aplicarlo a un componente. El botón “+” para guardar un estilo para usarlo más tarde no está disponible en el modo de estilo.

![Proporcionar un nombre de estilo personalizado para la biblioteca de recursos](assets/custom-style-name.png)

Cuando se proporciona un nombre personalizado para un estilo, este se asocia a una temática y ya no está disponible para otras. Para eliminar un estilo guardado:

1. En la barra de herramientas LIENZO, haga clic en **Opciones de temática** ![theme-options](assets/theme-options.png) > **Administrar estilos**.
1. En el cuadro de diálogo Administrar estilos, seleccione un estilo guardado y haga clic en **Eliminar**.

   ![Eliminar el estilo guardado](assets/manage-styles.png)

### Vista previa activa, guardar y descartar cambios {#live-preview-save-and-discard-changes}

Las modificaciones realizadas en el estilo se reflejan instantáneamente en el formulario o en la comunicación interactiva cargada en el lienzo. La vista previa en directo permite definir y ver de forma interactiva el impacto del estilo. Al cambiar el estilo de un componente, el botón **Listo** aparece habilitado en la barra lateral. Para conservar los cambios, haga clic en el botón **Listo**.

>[!NOTE]
>
>Cuando se introduce un carácter no válido en un campo, el color del límite del campo cambia a rojo y se muestra un mensaje de error en la esquina superior izquierda de la pantalla. Por ejemplo, si se introducen caracteres alfabéticos en un cuadro de texto que acepta caracteres numéricos como entrada, el color de los límites del cuadro de entrada cambia a rojo. No puede guardar un tema de este tipo sin resolver el error mostrado en la parte superior.

### Tema con otra forma adaptable o comunicación interactiva {#theme-with-another-adaptive-form-or-interactive-communication}

Cuando se crea una temática, se crea con un formulario que se envía con el editor de temáticas. Se proporciona estilo para los componentes de este formulario. En lugar del formulario enviado con el Editor de temas, puede seleccionar un formulario o comunicación interactiva de su elección para proporcionar estilo y previsualizar sus resultados.

Para reemplazar el formulario actual o la comunicación interactiva en el Lienzo del Editor de temas:

1. En el panel EDITOR DE TEMÁTICAS, haga clic en **Opciones de temática** ![theme-options](assets/theme-options.png) > **Configurar**.

1. En la ficha General , busque y seleccione un formulario o una comunicación interactiva para la **Formulario/documento adaptable** campo .

### Rehacer/deshacer {#redo-undo}

Puede deshacer o rehacer los cambios no deseados que se producen accidentalmente. Utilice los botones Rehacer y Deshacer del lienzo.

![Rehacer y deshacer acciones](assets/redo_undo_new.png)

Botones Deshacer/Rehacer en Lienzo

Los botones Rehacer y Deshacer aparecen al aplicar estilo a un componente en el editor de temáticas.

## Uso del editor de temáticas {#using-the-theme-editor}

El editor de temáticas permite editar una temática que haya creado o cargado. Vaya a **Formularios y documentos > Temáticas**; luego, seleccione una y ábrala. La temática se abre en el editor de temáticas.

Como se ha indicado anteriormente, el editor de temáticas tiene dos paneles: Barra lateral y Lienzo. 
![editor de temas](assets/theme-editor.png)

Personalización del estilo del estado de éxito del componente Widget de cuadro de texto en el editor de temáticas. El componente está seleccionado en Lienzo y su estado está seleccionado en la barra lateral. Las opciones de estilo disponibles en la barra lateral se utilizan para personalizar el aspecto de un componente.

### Uso del lienzo {#using-canvas}

El tema se crea mediante el formulario predeterminado o utilizando un formulario o una comunicación interactiva de su elección. El lienzo muestra la vista previa del formulario o la comunicación interactiva utilizada para crear el tema con las personalizaciones especificadas en el tema. La regla situada encima del formulario se utiliza para determinar la presentación en función del tamaño de visualización del dispositivo.

En la barra de herramientas Lienzo, verá:

* **Alternar panel lateral** ![toggle-side-panel](assets/toggle-side-panel.png): permite mostrar u ocultar la barra lateral.
* **Opciones de la temática** ![theme-options](assets/theme-options.png): proporciona tres opciones

   * Configurar: Proporciona opciones para seleccionar el formulario de vista previa o la comunicación interactiva, la clientlib base y la configuración de Adobe Fonts.
   * Ver temática CSS: genera CSS para la temática seleccionada.
   * Administrar estilos: proporciona opciones para administrar estilos de texto e imagen
   * Ayuda: ejecuta una repaso guiado con imágenes sobre el editor de temáticas.

* **Emulador** ![ruler](assets/ruler.png): emula el aspecto de la temática para diferentes tamaños de visualización. Un tamaño de visualización se trata como un punto de interrupción en el emulador. Puede seleccionar un punto de interrupción y especificar un estilo para él. Por ejemplo, Escritorio y Tablet son dos puntos de interrupción. Puede especificar distintos estilos para cada punto de interrupción.

Cuando seleccione un componente en el lienzo, verá la barra de herramientas de componentes encima. La barra de herramientas de componentes permite seleccionar componentes o cambiar a componentes genéricos. Por ejemplo, se selecciona un cuadro de texto numérico en un panel. Verá las siguientes opciones en la barra de herramientas de componentes:

* **Widget de cuadro numérico**: permite seleccionar el componente para personalizar su aspecto en la barra lateral.
* **Widget de campos**: permite seleccionar el componente genérico para el estilo. En este ejemplo, todos los componentes de entrada de texto (cuadro de texto/cuadro numérico/paso numérico/entrada de fecha) están seleccionados para el estilo.

* ![nivel de campo](assets/field-level.png): Permite cambiar al componente genérico para el estilo. Si selecciona un cuadro numérico y pulsa este icono, el componente de campo estará seleccionado. Si selecciona el componente de campo y pulsa este icono, el panel estará seleccionado. Si sigue pulsando este icono para seleccionarlo, acaba seleccionando el diseño para el estilo.

>[!NOTE]
>
>Las opciones disponibles en la barra de herramientas de componentes varían en función del componente que seleccione.

![Barra de herramientas de los componentes](assets/overlay.png)

Barra de herramientas de componentes del cuadro numérico del lienzo

### Uso de la barra lateral {#using-rail}

La barra lateral del editor de temáticas ofrece opciones para personalizar estilos para los componentes de una temática y utilizar selectores. Los selectores permiten seleccionar un grupo de componentes o componentes individuales, así como buscar selectores en la barra lateral. Puede escribir selectores para los componentes personalizados.

Cuando se selecciona un componente del lienzo o los selectores en la barra lateral, la barra lateral muestra todas las opciones que le permiten personalizar los estilos para él. 
A continuación se muestran las opciones que ve en la barra lateral al seleccionar un componente:

* Estado
* Hoja de propiedades
* Simular error/éxito

#### Estado {#state}

Un estado es un indicador de la interacción del usuario con un componente. Por ejemplo, cuando un usuario introduce datos erróneos en un cuadro de texto, el estado del cuadro de texto cambia a un estado de error. El editor de temáticas permite especificar el estilo de un estado en particular.

Las opciones para personalizar los estilos de estado varían para los distintos componentes.

#### Hoja de propiedades {#property-sheet}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Uso de</strong></td>
  </tr>
  <tr>
   <td><p>Dimensiones y posición</p> </td>
   <td><p>Permite aplicar estilo a la alineación, el tamaño, el posicionamiento y la colocación de los componentes en la temática. </p> <p>Las opciones son configuración de visualización, relleno, margen, anchura, altura e índice Z.</p> <p>También puede utilizar el modo Diseño para definir la anchura de los componentes con una interfaz sencilla de arrastrar y soltar. Para obtener más información, consulte <a href="../../forms/using/resize-using-layout-mode.md">Uso del modo Diseño para cambiar el tamaño de los componentes</a>.</p> </td>
  </tr>
  <tr>
   <td><p>Texto</p> </td>
   <td><p>Permite personalizar los estilos de texto en el componente de la temática.</p> <p>Por ejemplo, desea cambiar el aspecto del texto introducido en el cuadro de texto.</p> <p>Las opciones son familia de fuentes, grosor, color, tamaño, altura de línea, alineación del texto, espaciado entre letras, sangría del texto, subrayado, cursiva, transformación del texto, alineación vertical, línea de base y dirección. </p> </td>
  </tr>
  <tr>
   <td><p>Fondo </p> </td>
   <td><p>Permite rellenar el fondo del componente con una imagen o un color. </p> </td>
  </tr>
  <tr>
   <td><p>Borde</p> </td>
   <td><p>Permite elegir el aspecto del borde del componente. Por ejemplo, desea que el cuadro de texto tenga un borde grueso y rojo profundo con una línea de puntos. </p> <p>Las opciones son anchura, estilo, radio y color del borde.</p> </td>
  </tr>
  <tr>
   <td><p>Efectos</p> </td>
   <td><p>Permite agregar efectos especiales a los componentes, como opacidad, modo de fusión y sombras. </p> </td>
  </tr>
  <tr>
   <td><p>Avanzado </p> </td>
   <td><p>Permite agregar:</p>
    <ul>
     <li>Propiedades para los pseudoelementos <code>::before</code> y <code>::after</code> para agregar contenido después o antes del contenido predeterminado en el selector y aplicarle así estilo.<br /> Consulte <a href="https://www.w3schools.com/css/css_pseudo_elements.asp" target="_blank">Pseudoelementos CSS</a>.</li>
     <li>Código CSS personalizado en línea a un componente y escribir selectores personalizados. </li>
    </ul> <p>Cuando agrega un código CSS personalizado, anula la personalización que ha agregado con las opciones de la barra lateral. </p> </td>
  </tr>
 </tbody>
</table>

#### Simular error/éxito {#simulate-error-success}

Las opciones de simular error y éxito están disponibles en la parte inferior de la barra lateral. Se pueden ver mediante una flecha de mostrar u ocultar visible en la parte inferior de la barra lateral. Con el editor de temáticas, puede aplicar estilo a varios estados de un componente.

Por ejemplo, se agrega un campo numérico al formulario y se especifica su estilo en el editor de temáticas. Cuando un usuario escribe un valor alfanumérico en el campo, desea que cambie el color de fondo del cuadro de texto. Se selecciona el campo numérico en la temática y se utiliza la opción de estado en la barra lateral. Seleccione el estado Error en la barra lateral y cambie el color de fondo a rojo. Para obtener una vista previa del comportamiento, puede utilizar la opción Simular error disponible en la barra lateral. Las opciones de simular error y éxito se describen en detalle a continuación:

* **Simular éxito**:
le permite ver el aspecto de un componente si especifica su estilo para el estado de éxito. Por ejemplo, en un formulario, los clientes establecen la contraseña. Los usuarios pueden configurar la contraseña según las directrices que proporcione. Cuando un usuario escribe una contraseña siguiendo todas las directrices proporcionadas, el cuadro de texto se vuelve verde. Cuando el cuadro de texto se vuelve verde, está en estado de éxito. Puede especificar el estilo de un componente en estado de éxito y simular su aspecto utilizando la opción Simular éxito.

* **Simular error**:
le permite ver el aspecto de un componente si especifica su estilo para el estado de error. Por ejemplo, en un formulario, los clientes establecen la contraseña. Los usuarios pueden configurar la contraseña según las directrices que proporcione. Cuando un usuario escribe una contraseña que no sigue todas las directrices proporcionadas, el cuadro de texto se vuelve rojo. Cuando el cuadro de texto se vuelve rojo, está en estado de error. Puede especificar el estilo de un componente en estado de error y simular su aspecto utilizando la opción Simular error.

### Estilo de un componente {#styling-a-component}

Por ejemplo, en el formulario, tiene dos tipos de cuadros de texto: uno que solo acepta valores numéricos y otro que acepta valores alfanuméricos. Puede personalizar el estilo del cuadro de texto que solo acepta valores numéricos (un cuadro numérico).

Siga estos pasos para personalizar el estilo de un componente en particular (un cuadro numérico en este ejemplo):

1. En el editor de temáticas, seleccione el cuadro numérico en el lienzo.
1. Al seleccionar el cuadro numérico, puede ver la barra de herramientas de componentes con tres opciones:

   * **Widget del cuadro numérico**
   * **Widget del campo** ![nivel de campo](assets/field-level.png)

1. Seleccione **Widget del cuadro numérico**.
1. El título de la barra lateral cambia a Widget del cuadro numérico y muestra las opciones para personalizar su aspecto. 
Use **Dimensión y posición** en la barra lateral para personalizar el tamaño del componente. Compruebe que el estado es **Predeterminado**.

En lugar de seleccionar **Widget del cuadro numérico**, seleccione **Widget del campo** en la barra de herramientas de componentes y realice los pasos anteriores. Al seleccionar dimensiones para **Widget del campo**, todos los cuadros de texto excepto el cuadro numérico tienen el mismo tamaño.

### Estilo de campos para un estado determinado {#styling-fields-given-state}

Con la barra de herramientas de componentes, también puede especificar el estilo de los componentes para sus distintos estados. Por ejemplo, si un componente está deshabilitado, entonces está en estado deshabilitado. Los estados más utilizados de un componente al que se puede aplicar estilo en el editor de temáticas son: Predeterminado, Enfoque, Deshabilitado, Error, Éxito y Desplazamiento. Puede seleccionar un componente en el lienzo y utilizar la opción Estado en la barra lateral para personalizar su aspecto.

Siga estos pasos para personalizar el estilo de un componente en un estado específico:

1. Seleccione un componente en el lienzo y seleccione la opción adecuada en la barra de herramientas de componentes. 
La barra lateral muestra las opciones para personalizar el estilo del componente.
1. Seleccione un estado en la barra lateral. Por ejemplo, Estado de error.
1. Utilice opciones como **Borde o Fondo** en la barra lateral para personalizar el aspecto del componente.
1. Utilice la opción **Simular error** en la parte inferior de la barra lateral para ver el aspecto del estilo en la edición.

Al personalizar el estilo de un componente después de especificar su estado, la personalización solo aparece para el componente en el estado especificado. Por ejemplo, si personaliza el estilo del componente cuando está seleccionado el estado de desplazamiento. La personalización aparece para el componente cuando mueve el puntero sobre el componente en el formulario procesado o comunicación interactiva al que aplica el tema.

Para simular el comportamiento de estados que no sean errores y de éxito, utilice el modo de vista previa. Para utilizar el modo de vista previa, haga clic en **Vista previa** en la barra de herramientas de la página.

### Estilo de diseños para pantallas más pequeñas {#styling-layouts-for-smaller-displays}

Utilice la regla del lienzo para seleccionar puntos de interrupción para dispositivos con pantallas más pequeñas. Haga clic en emulador ![ruler](assets/ruler.png) en Lienzo para ver la regla y los puntos de interrupción. Los puntos de interrupción permiten previsualizar un formulario o una comunicación interactiva para tamaños de visualización pertenecientes a distintos dispositivos, como teléfonos y tabletas. El editor de temáticas admite varios tamaños de visualización.

Para aplicar estilo a los componentes de distintos puntos de interrupción:

1. En el lienzo, seleccione un punto de interrupción encima de la regla. 
Un punto de interrupción representa un dispositivo móvil y su tamaño de visualización.
1. Utilice la barra lateral para personalizar el estilo de los componentes de formulario o de comunicación interactiva en el tema para el tamaño de visualización seleccionado.
1. Asegúrese de que la personalización esté guardada.

Puede aplicar estilo a los componentes de formulario o comunicación interactiva para varios dispositivos. Los componentes de formulario y comunicación interactiva para equipos de escritorio y dispositivos móviles pueden tener estilos totalmente diferentes.

### Uso de fuentes web en un tema {#using-web-fonts-in-a-theme}

Ahora puede utilizar fuentes disponibles en un servicio web en un formulario adaptable o una comunicación interactiva. De forma predeterminada, [Adobe Fonts](https://fonts.adobe.com/), el servicio de fuentes web de Adobe, está disponible. Para usar Adobe Fonts, cree un kit, añada fuentes y obtenga el ID del kit de [Adobe Fonts](https://fonts.adobe.com/).

Siga estos pasos para configurar Adobe Fonts en AEM:

1. En la instancia de autor, haga clic en ![adobeexperiencemanager](assets/adobeexperiencemanager.png)Adobe Experience Manager > Herramientas ![martillo](assets/hammer.png) > Implementación > Cloud Services.
1. En la página **Cloud Service**, vaya y abra la opción **Adobe Fonts**. Abra la carpeta de configuración y haga clic en **Crear**.
1. En el **Crear configuración** , especifique un título para la configuración y haga clic en **Crear**.

   Se le redirigirá a la página de configuración.

1. En el cuadro de diálogo Editar componente que aparece, proporcione el ID del kit y haga clic en **Aceptar**.

Siga estos pasos para configurar un tema para utilizar la configuración de Adobe Fonts:

1. En la instancia de autor, abra una temática en el editor de temáticas.
1. En el editor de temáticas, vaya a **Opciones de temática** ![theme-options](assets/theme-options.png) > **Configurar**.
1. En **Configuración de Adobe Fonts**, seleccione un kit y haga clic en **Guardar**.

   Ahora, puede ver que las fuentes se añaden en la propiedad font-family del tema.

### Listado y selección de fuentes en el editor de temas {#listing-and-selecting-fonts-in-theme-editor}

Puede utilizar el servicio de configuración de temas para agregar más fuentes al editor de temas. Siga estos pasos para añadir fuentes:

1. Inicie sesión en AEM consola web con privilegios administrativos. La dirección URL de la consola web AEM es `https://'[server]:[port]'/system/console/configMgr`.
1. Apertura **Servicio de configuración de tema del formulario adaptable**.

   ![theme-config](assets/theme-config.png)

1. Haga clic en +, especifique el nombre de la fuente y haga clic en **Guardar**. La fuente se añade y está disponible en el editor de temas.

#### Selección de fuentes en el editor de temáticas {#selecting-fonts-in-theme-editor}

Puede utilizar el botón “+” para agregar una fuente. Cuando se añade una fuente, esta aparece en la barra lateral.

![Nueva fuente enumerada en el editor de temáticas](assets/theme-font.png)

Además de la opción de configuración de la temática, también puede agregar la fuente desde el editor de temáticas en sí. Escriba la fuente que desee utilizar en el campo de la familia de fuentes en la barra lateral y pulse la tecla “retorno” (return) del teclado.

![Escritura y selección de fuentes en el editor de temáticas](assets/font-selection.png)

Cuando selecciona una fuente, esta se añade en la lista de la familia de fuentes. Puede utilizar la opción Máscara en el editor de temáticas para deshabilitar o habilitar las fuentes de la lista.

![fuentes múltiples](assets/multi-fonts.jpg)

Puede ver el cambio de fuente del componente.

El campo Familia de fuentes admite varias fuentes. Al escribir una fuente, el navegador la busca y la aplica al componente seleccionado. Si el navegador no encuentra una fuente, busca una que esté junto a ella en la familia. Puede empezar escribiendo la fuente específica que está buscando. Si no encuentra la fuente que desea utilizar, puede escribir una fuente genérica en la familia y utilizarla.

#### Estilos de máscara aplicados en el editor de temáticas {#mask-styles-applied-in-theme-editor}

Puede enmascarar estilos aplicados en una temática. En la barra lateral del editor de temáticas, puede usar el icono ![toggle_eye](assets/toggle_eye.png) para desactivar un estilo aplicado. Por ejemplo, si cambia las dimensiones de un componente en un formulario o una comunicación interactiva, puede utilizar el botón de máscara de la izquierda de una propiedad para desactivarlo. Al guardar una temática, se conservan las opciones de máscara seleccionadas.

![Opción Máscara disponible en la barra lateral del editor de temáticas](assets/mask-styles.png)

El ejemplo siguiente muestra estilos enmascarados y sin enmascarar en una temática.

![Estilos enmascarados y sin enmascarar](assets/mask2.png)

## Aplicación de una temática a un formulario o comunicación interactiva {#applying-a-theme-to-a-form-or-interactive-communication-br}

Para aplicar un tema a un formulario adaptable:

1. Abra el formulario en modo de edición. Para abrir un formulario en modo de edición, seleccione un formulario y haga clic en **Abrir**.
1. En el modo de edición, seleccione un componente y, a continuación, pulse ![field-level](assets/field-level.png) > **Contenedor de formulario adaptable** y haga clic en ![cmppr](assets/cmppr.png).

   Puede editar las propiedades del formulario en la barra lateral.

1. En la barra lateral, haga clic en **Estilo**.
1. Seleccione la temática en el menú desplegable **Temática del formulario adaptable** y haga clic en **Listo** ![check-button](assets/check-button.png).

Para aplicar un tema a una comunicación interactiva:

1. Abra la comunicación interactiva en modo de edición. Para abrir una comunicación interactiva en modo de edición, seleccione un formulario y haga clic en **Apertura**.
1. En el modo de edición, seleccione un componente y haga clic en ![nivel de campo](assets/field-level.png) >**Contenedor de documento** y, a continuación, haga clic en ![cmppr](assets/cmppr.png).

   Puede editar las propiedades del formulario en la barra lateral.

1. En la barra lateral, debajo de **Básico**, seleccione el tema en la **Tema** y haga clic en **Listo** ![botón de verificación](assets/check-button.png)

### Cambiar la temática de un formulario durante la ejecución {#change-theme-of-a-form-at-runtime}

Una temática presenta distintos componentes de un formulario. Puede usar la propiedad `themeOverride` para cambiar dinámicamente la temática de un formulario. Una URL típica de un formulario es:

`https://<server>:<port>/content/forms/af/test.html`

Puede utilizar el parámetro themeOverride para aplicar una temática durante la ejecución.

`https://<server>:<port>/content/forms/af/test.html?themeOverride=/content/dam/formsanddocuments-themes/simpleEnrollmentTheme`

La opción `themeOverride` permite proporcionar una ruta a una temática. Cambia la temática del formulario y lo actualiza con estilos mejorados.

## Obtención de un aspecto específico mediante Temáticas {#specific-af-appearance}

Con AEM Forms, junto con el tema de lienzo predeterminado, hay muchos otros temas. Si desea diseñar el formulario o la comunicación interactiva utilizando otros temas, junto con cambios adicionales, copie el tema de la carpeta Biblioteca de temas. Pegue las temáticas copiadas fuera de la carpeta Biblioteca de temáticas y edite la temática copiada según los cambios que desee.

Para copiar una temática, realice los siguientes pasos:

1. En la instancia de creación, vaya a **Adobe Experience Manager > Forms > Temáticas**.
1. Abra la carpeta Biblioteca de temáticas.
1. En la carpeta Biblioteca de temáticas, pase el puntero sobre la temática correspondiente y pulse **Copiar**.
1. Pegue la temática copiada fuera de la carpeta Biblioteca de temáticas.
1. Personalice la temática copiada.

Después de personalizar el tema, aplique este al formulario o a la comunicación interactiva.

>[!NOTE]
>
>No modifique las temáticas disponibles en la carpeta Biblioteca de temáticas. Esta carpeta contiene temáticas del sistema. Cualquier cambio que haya realizado en estos temas se sobrescribirá al instalar una versión más reciente o una corrección de AEM Forms.

## Impacto en otros casos de uso de formularios adaptables {#impact-on-other-adaptive-form-use-cases}

* **Publicar/cancelar la publicación de un formulario:** al publicar un formulario, la temática aplicada también se publica (si aún no se ha publicado).
* **Importar/exportar un formulario:** al importar o exportar un formulario, su temática asociada también se importa o exporta automáticamente.
* **Referencias de un formulario:** la sección Referencias de las referencias de formulario contiene una entrada adicional para la temática.
* **Hora de la última modificación de un formulario:** se actualiza cuando se cambia la temática asociada.
* **Prueba A/B:** Puede aplicar un tema diferente a dos versiones del formulario en las pruebas A/B. La información de los dos temas se almacena individualmente en los dos contenedores de guías.

## Secuencia de generación de CSS {#css-generation-sequence}

Cuando selecciona Ver CSS, el Editor de temáticas recopila toda la información de estilo y crea un archivo CSS. Recopila información en el siguiente orden:

1. Estilo definido en la biblioteca de cliente base del tema.
1. Estilo definido por el usuario, especificado con las propiedades de la barra lateral.
1. Estilo CSS proporcionado mediante la opción Sustitución de CSS.

Por ejemplo, el color de fondo de un cuadro de texto es azul en la biblioteca de cliente base. Puede cambiarlo a rosa con las propiedades de la barra lateral. Cuando genere un archivo CSS, verá el color de fondo del cuadro de texto como rosa. Después de cambiar el color de fondo mediante las propiedades, otro autor utiliza la opción de anulación de CSS para cambiar el cuadro de texto de color de fondo como blanco. Cuando genere un archivo CSS, verá el color de fondo como blanco en el CSS generado.

## Depuración de estilos {#debugging-styles}

Cuando se especifican estilos para los componentes en el Editor de temáticas, se genera un archivo CSS. Al aplicar estilo a un componente genérico, también se diseñan varios componentes incluidos en él. Por ejemplo, al aplicar estilo a un campo, también se le aplica estilo al cuadro de texto y a la etiqueta. Cuando aplica estilo al cuadro de texto dentro del campo, obtiene su propio archivo CSS. Si desea depurar el archivo CSS generado para el campo y el componente, el Editor de temáticas proporciona opciones que le permiten ver el CSS.

Puede ver el CSS generado mediante las siguientes opciones:

* Opción **Ver CSS** en la barra lateral: al seleccionar un componente en la temática, puede ver la opción VER CSS en la barra lateral. Muestra el CSS generado, incluido el CSS para los pseudoelementos `::before` y `::after`.
* Opción **Ver temática CSS** en la barra de herramientas del lienzo: en la barra de herramientas del lienzo, haga clic en ![theme-options](assets/theme-options.png) > **Ver temática CSS**. Puede ver la temática completa en CSS generada a partir de las propiedades definidas en el Editor de temáticas.

## Solución de problemas, recomendaciones y prácticas recomendadas {#troubleshooting-recommendations-and-best-practices}

* **Evitar recursos de otra temática**

   Al editar una temática, puede examinar y agregar recursos (como imágenes) de otras temáticas. Por ejemplo, quiere editar el fondo de una página. Al seleccionar **Página** ![edit-button](assets/edit-button.png) > **Fondo** > **Agregar** > **Imagen**, verá un cuadro de diálogo que le permite examinar y agregar imágenes en otras temáticas.

* Puede tener problemas con la temática actual si se agrega un recurso desde otra y esta se mueve o se elimina. Se recomienda evitar explorar y agregar recursos de otras temáticas.
* **Uso de clientlib base, editor de temas y estilo en línea**

   * **Base clientlib**:

      La biblioteca de cliente base contiene información de estilo. Para utilizar información de estilo en bibliotecas de cliente en temas.

      1. Vaya a **Experience Manager > Forms > Temas**.
      1. En la página Temas , seleccione un tema y haga clic en **Ver propiedades**.
      1. En la página Propiedades que se abre, haga clic en **Avanzadas**.
      1. En la ficha Avanzado , en el campo Ubicación de Clientlib , busque y seleccione la biblioteca de cliente que desee utilizar.
      1. Haga clic en **Guardar**.

      El estilo que especifique en la biblioteca de cliente se importa en el tema que lo utiliza. Por ejemplo, puede especificar estilo para el cuadro de texto, el cuadro numérico y el conmutador en la biblioteca de cliente. Cuando se importa la biblioteca de cliente en el tema, se importa el estilo del cuadro de texto, el cuadro numérico y el conmutador. A continuación, puede aplicar estilo a otros componentes mediante el editor de temas.
También puede crear una temática, crear copias de la misma y, a continuación, modificar el estilo proporcionado en las temáticas copiadas para casos de uso similares.
Consulte [Obtención de un aspecto específico mediante Temas](#specific-af-appearance)

   * **Editor de temas:**

      El editor de temas permite crear temas para aplicar estilo al formulario o a la comunicación interactiva. Puede especificar el estilo de los componentes de un tema, que permiten la coherencia en el aspecto de los distintos formularios o comunicaciones interactivas que desarrolle. Se recomienda especificar información de estilo en una temática y, a continuación, aplicarla a un formulario.

   * **Estilo en línea:**

      Los componentes de estilo se pueden aplicar con el modo Estilo del editor multicanal de comunicación interactiva o de formulario cuando se trabaja con un formulario. Si se utiliza el modo de estilo para cambiar el estilo de los componentes del formulario, se anula el estilo especificado en la temática. Si desea cambiar el estilo de ciertos componentes de un formulario concreto, consulte [Estilo en línea de los componentes](../../forms/using/inline-style-adaptive-forms.md).


* **Uso de bibliotecas del lado del cliente**

   Si desea crear bibliotecas de cliente para importar información de estilo, consulte [Uso de bibliotecas del cliente](/help/sites-developing/clientlibs.md). Después de crear una biblioteca de cliente, puede importarla en su tema siguiendo los pasos mencionados anteriormente.

* **Cambio de la anchura de diseño del panel contenedor**

   No se recomienda cambiar la anchura del diseño del panel contenedor. Cuando se especifica la anchura de un panel contenedor, este se vuelve estático y no se adapta a distintas pantallas.

* **Utilización del editor de formularios o del editor de temáticas para trabajar con encabezado y pie de página**

   Utilice el editor de temáticas si desea aplicar estilo al encabezado y al pie de página mediante opciones de estilo como estilo de fuente, fondo y transparencia. 
Si desea proporcionar información como un logotipo, el nombre de la empresa en el encabezado e información de copyright en el pie de página, utilice las opciones del editor de formularios.
