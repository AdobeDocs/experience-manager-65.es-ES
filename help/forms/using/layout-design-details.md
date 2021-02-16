---
title: Diseño de maquetación
seo-title: Diseño de maquetación
description: Los detalles del diseño de maquetación explican cómo se pueden crear maquetaciones para utilizarlas en las cartas o en las comunicaciones interactivas.
seo-description: Los detalles del diseño de maquetación explican cómo se pueden crear maquetaciones para utilizarlas en las cartas o en las comunicaciones interactivas.
uuid: 469a8a71-88f7-4102-bb02-38ed05390f6c
content-type: reference
topic-tags: correspondence-management, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 683809ac-089b-49bf-a72c-67d32439081f
docset: aem65
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '2190'
ht-degree: 0%

---


# Diseño de diseño{#layout-design}

Las plantillas de formulario XFA o XDP son las plantillas para:

* [Cartas](/help/forms/using/create-letter.md)
* [Imprimir ](/help/forms/using/web-channel-print-channel.md#printchannel) canal de comunicaciones  [interactivas](/help/forms/using/interactive-communications-overview.md)

* Fragmentos de diseños

Un XDP está diseñado en Adobe Forms Designer. Este artículo proporciona detalles sobre cómo diseñar los XDP para crear correspondencias/comunicaciones interactivas eficaces, como dónde utilizar campos de formulario o áreas de destinatario y cuándo utilizar fragmentos de diseño.

## Creación de un diseño para letras o para el canal de impresión de Interactive Communications {#creating-a-layout-for-letters-or-for-interactive-communications-print-channel}

Un diseño define el diseño gráfico de un canal de letras e impresiones de una comunicación interactiva. La presentación puede contener campos de formulario típicos como &quot;Dirección&quot; y &quot;Número de referencia&quot;. También contiene subformularios vacíos que denotan áreas de destinatario. Cree la presentación en el diseñador de formularios y, una vez completada, el Especialista en aplicaciones la carga en AEM servidor. Desde allí, puede seleccionar el diseño al crear una plantilla de correspondencia o un canal de impresión de una comunicación interactiva.

![Designer: crear un diseño](assets/claimsubrogationlayout.png)

Siga estos pasos para crear diseños para letras/canal de impresión de Interactive Communications:

1. Analizar el diseño y determinar el contenido que se repite en todas las páginas; generalmente el encabezado y pie de página encajan en esta categoría. Este contenido se coloca en las páginas de formato del diseño. El contenido restante va a las páginas de trabajo del diseño. En una chaqueta de política, el logotipo y la dirección de compañía se pueden agregar al encabezado y al pie de página de la página de formato. Por ejemplo, la Notificación de cancelación utiliza la misma presentación.
1. Al diseñar páginas de trabajo, divida el contenido de la página en secciones. Cada sección está diseñada como un subformulario incrustado en la propia presentación o como una presentación de fragmento. Si la sección contiene una tabla, modele la sección como un fragmento de diseño.
1. Un diseño se puede diseñar de la siguiente manera:

   1. Convierta cada sección en un subformulario independiente que contenga todos los elementos de la sección.
   1. Hacer que cada subformulario de sección sea secundario del mismo subformulario principal. La presentación del subformulario principal está definida en posición variable para permitir que las secciones cambien a continuación en caso de que se combinen datos de gran tamaño en secciones anteriores.
   1. La residencia principal de la sección también se puede reutilizar en otros diseños. Crearla como un diseño de fragmento.
   1. Sección Los detalles de interés adicionales contienen sólo dos elementos colocados uno debajo de otro, pueden contener datos grandes y están diseñados como de posición variable.
   1. Otras secciones contienen elementos en posiciones específicas, por lo que están diseñadas como maquetaciones colocadas.
   1. Si la sección contiene elementos en posiciones específicas, divida una sección en subformularios y estos elementos contienen grandes cantidades de datos. A continuación, organice los subformularios para lograr el comportamiento deseado.
   1. En la sección de residencia principal, agregue un área de destinatario de marcador de posición. Este marcador de posición está enlazado a la residencia principal de fragmento en el momento del diseño de la carta/comunicación interactiva.
   1. Cargue el diseño (y el fragmento, si lo hay, que utiliza el diseño) en el servidor de AEM Forms.

### Usar subformulario en una plantilla XDP {#usesubformxdp}

Una vez analizada la presentación necesaria para crear la comunicación interactiva, puede crear subformularios en la plantilla XDP con Forms Designer. Los componentes de subformulario en blanco que se utilizan en la plantilla XDP dan como resultado la visualización de áreas de destinatario en el canal Imprimir de la Comunicación interactiva.

>[!NOTE]
>
>Añada contenido en el canal de impresión de la comunicación interactiva en lugar de agregar contenido al componente de subformulario en la plantilla XDP. Añada contenido en las áreas de destinatario del canal de impresión mediante [fragmentos de documento, gráficos, imágenes](create-interactive-communication.md#step2) y fragmentos de diseño.

Siga estos pasos para utilizar subformulario en una plantilla XDP:

1. Abra Forms Designer, seleccione **Archivo** > **Nuevo** > **Usar un formulario en blanco**, toque **Siguiente** y, a continuación, toque **Finalizar** para abrir el formulario para la creación de plantillas.

   Asegúrese de que las opciones **Biblioteca de objetos** y **Objeto** están seleccionadas en el menú **Ventana**.

1. Arrastre y suelte el componente **Subformulario** desde la **Biblioteca de objetos** al formulario.

   ![Diseñador de componentes](assets/subform_component_designer_new.png)

1. Seleccione el subformulario para mostrar las opciones del subformulario en la ventana **Objeto** del panel derecho.
1. Seleccione la ficha **Subformulario** y seleccione **De posición variable** en la lista desplegable **Contenido**. Arrastre el extremo izquierdo del subformulario para ajustar la longitud.

   ![Subformulario de posición variable](assets/object_subform_flowed_new.png)

1. En la ficha **Enlace**:

   1. Especifique un nombre para el subformulario en el campo **Nombre**.
   1. Seleccione **Ningún enlace de datos** en la lista desplegable **Enlace de datos**.

1. Del mismo modo, seleccione el subformulario raíz en el panel izquierdo.

   ![Subformulario raíz](assets/root_subform_designer_new.png)

1. Seleccione la ficha **Subformulario** y seleccione **De posición variable** en la lista desplegable **Contenido**. En la ficha **Enlaces**:

   1. Especifique un nombre para el subformulario en el campo **Nombre**.
   1. Seleccione **Ningún enlace de datos** en la lista desplegable **Enlace de datos**.

   Repita los pasos del 2 al 5 para agregar más subformularios a la plantilla XDP. Añada [texto, fragmentos de documento, imágenes y gráficos](create-interactive-communication.md#step2) en las áreas de destinatario solo mientras crea la Comunicación interactiva.

1. Seleccione **Archivo** > **Guardar como** para guardar el archivo en el sistema de archivos local:

   1. Vaya a la ubicación para guardar el archivo y especifique un nombre para la plantilla XDP.
   1. Seleccione **.xdp** en la lista desplegable **Guardar como tipo**.

   1. Toque **Guardar**.

### Usar el componente Campo de imagen en una plantilla XDP {#use-image-field-component-in-an-xdp-template}

Utilice el componente Campo de imagen o Subformulario en la plantilla XDP y agregue una imagen durante la creación de la comunicación interactiva.

>[!NOTE]
>
>Añada la imagen en el canal de impresión de la comunicación interactiva en lugar de agregar la imagen al campo de imagen o al componente Subformulario en la plantilla XDP. Para obtener más información, consulte [Añadir contenido a la comunicación interactiva](../../forms/using/create-interactive-communication.md#step2).

Siga estos pasos para utilizar el componente Campo de imagen en una plantilla XDP:

1. Arrastre y suelte el componente **Campo de imagen** desde la **Biblioteca de objetos** al formulario.
1. Seleccione el subformulario para mostrar las opciones del subformulario en la ventana **Objeto** del panel derecho.
1. En la ficha **Enlace**:

   1. Especifique un nombre para el campo de imagen en el campo **Nombre**.
   1. Seleccione **Ningún enlace de datos** en la lista desplegable **Enlace de datos**.

### Crear una plantilla XDP para fragmentos de diseño {#xdplayoutfragments}

Utilice el componente Tabla de Forms Designer para crear fragmentos de diseño y, a continuación, utilizarlos para crear tablas mientras crea el canal Imprimir de Comunicación interactiva. El uso de fragmentos de diseño para crear tablas garantiza que el contenido de la tabla conserva la estructura cuando el canal web se genera automáticamente mediante el canal de impresión.

>[!NOTE]
>
>Introduzca texto en las celdas de la tabla o [cree un enlace con los objetos del modelo de datos de formulario](create-interactive-communication.md#step2) solo durante la creación de la comunicación interactiva.

Siga estos pasos para utilizar el componente Tabla en la plantilla XDP con Forms Designer:

1. Arrastre y suelte el componente **Tabla** desde la **Biblioteca de objetos** al formulario.
1. En el cuadro de diálogo **Insertar tabla**:

   1. Especifique el número de filas y columnas de la tabla.
   1. Seleccione la casilla **Incluir fila de encabezado en tabla** para incluir una fila para el encabezado de tabla.
   1. Toque **Aceptar**.

1. Toque **+** en el panel izquierdo junto al nombre de la tabla, haga clic con el botón derecho en los nombres de celda incluidos en el encabezado y otras filas y seleccione **Cambiar el nombre del objeto** para cambiar el nombre de las celdas de la tabla.
1. Haga clic en los campos de texto del encabezado de tabla en la **Vista de diseño** y cámbieles el nombre.
1. Arrastre y suelte el componente **Campo de texto** de la **Biblioteca de objetos** a cada celda de tabla de la **Vista de diseño**. Siga este paso para poder enlazar celdas de tabla con los objetos del modelo de datos de formulario durante la creación de la comunicación interactiva.

   ![Campos de texto en una tabla](assets/text_fields_table_new.png)

1. Seleccione el nombre de la fila en el panel izquierdo y seleccione **Objeto** > **Enlace** > **Repetir fila para cada elemento de datos**. Realice este paso para asegurarse de que si se crea un enlace entre las celdas de tabla de esta fila con objetos del modelo de datos de formulario de tipo colección, la fila de tabla se repite automáticamente para cada elemento de datos disponible en la base de datos.

   Introduzca texto en las celdas de la tabla o [cree un enlace con los objetos del modelo de datos de formulario](create-interactive-communication.md#step2) solo durante la creación de la comunicación interactiva.

1. Seleccione **Archivo** > **Guardar como** para guardar el archivo en el sistema de archivos local:

   1. Vaya a la ubicación para guardar el archivo y especifique el nombre de la plantilla XDP.
   1. Seleccione **.xdp** en la lista desplegable **Guardar como tipo**.

   1. Toque **Guardar**.

### Cargar plantilla XDP en el servidor de AEM Forms {#uploadxdptemplate}

Una vez creada una plantilla XDP con Forms Designer, debe cargarla en el servidor de AEM Forms para que la plantilla esté disponible para su uso durante la creación de la comunicación interactiva.

1. Seleccione **Forms** > **Forms &amp; Documentos**.
1. Toque **Crear** > **Carga de archivo**.
1. Vaya a la ubicación de la plantilla XDP en el sistema de archivos local y toque **Abrir** para importar la plantilla XDP al servidor de AEM Forms.

## Uso de esquema {#using-schema}

Puede utilizar un esquema en un fragmento de diseño o diseño, pero no es obligatorio. Si utiliza un esquema, asegúrese de lo siguiente:

1. El diseño y todos los diseños de fragmento utilizados en una carta/Comunicación interactiva utilizan el mismo esquema que la letra/Comunicación interactiva.
1. Todos los campos necesarios para rellenarse con datos están enlazados al esquema.

## Creación de campos relacionados {#creating-relatable-fields}

De forma predeterminada, todos los campos se consideran relacionados con otros orígenes de datos. Si el diseño contiene campos que no están relacionados con un origen de datos, asigne al campo un sufijo &quot;_int&quot; (interno); por ejemplo, pageCount_int.

Un campo relativo debe:

* ser un XFA &lt;field> o &lt;exclGroup>
* tener una referencia de enlace XFA
* si se trata de un &lt;exclGroup>, debe tener al menos un campo de botón de radio secundario; de lo contrario, no se puede determinar su tipo de valor

Un campo relativo debe:

* tener un nombre

Un campo relativo no debe:

* Incluir un sufijo &quot;_int&quot; en su nombre
* tienen el enlace establecido como &quot;ninguno&quot;
* ser un elemento secundario de un elemento &lt;exclGroup>

Siempre que un campo relativo cumpla los criterios descritos anteriormente, puede estar en cualquier ubicación y en cualquier profundidad de anidación del diseño. Puede utilizar campos relacionados dentro de las páginas de formato.

Los campos son más flexibles en su configuración de presentación que los subformularios de área de destinatario; sin embargo, están ligadas a un solo tipo de valor. Puede hacer que un campo sea grande o establecer su anchura y altura fijas, etc. El resultado de la regla o módulo resuelto se inserta en el campo.

## Decidir cuándo utilizar subformularios y campos de texto {#deciding-when-to-use-subforms-and-text-nbsp-fields}

Utilice un subformulario si desea capturar contenido de varios módulos en una presentación vertical de arriba hacia abajo (varios párrafos o imágenes). La presentación debe tener en cuenta el hecho de que el subformulario crece en altura para adaptarse a su contenido. Si no puede estar seguro de que la longitud del contenido asociado al subformulario o destinatario nunca exceda el espacio reservado para el subformulario en la presentación, cree el subformulario como secundario en un contenedor de subformulario de posición variable. Este proceso garantiza que los objetos de presentación situados debajo del subformulario fluyan hacia abajo a medida que crece el subformulario.

Utilice un campo si desea capturar datos de módulos o datos de elementos de diccionario de datos en el esquema de la maquetación (porque los campos están enlazados a datos) o para mostrar contenido de módulos en una página de formato. Recuerde que el contenido de una página de formato no puede fluir con el contenido de la página de trabajo, por lo que debe asegurarse de que el campo de imagen se utiliza como logotipo de encabezado. Esta tabla proporciona más criterios para decidir cuándo utilizar un subformulario o un campo en una presentación.

<table>
 <tbody>
  <tr>
   <td><p><strong>Usar un subformulario cuando</strong></p> </td>
   <td><p><strong>Usar un campo de texto cuando</strong></p> </td>
  </tr>
  <tr>
   <td><p>Contiene una combinación de elementos, como Apellidos y Nombre</p> </td>
   <td><p>Contiene un solo elemento, como un número de directiva.</p> </td>
  </tr>
  <tr>
   <td><p>Incluye varios párrafos</p> </td>
   <td><p>El texto está ajustado y justificado</p> </td>
  </tr>
  <tr>
   <td><p>Los grupos de datos repetitivos, opcionales y condicionales están enlazados a subformularios para reducir el riesgo de errores de diseño que podrían producirse si se utilizan secuencias de comandos para obtener los mismos resultados</p> </td>
   <td><p>Los elementos como el logotipo y la dirección de su organización aparecen en todas las páginas de una carta o comunicación interactiva. En este caso, cree campos de formulario para esos elementos y colóquelos en la página de formato. Si establece el enlace de campo en "Sin enlace de datos", los campos no aparecerán como campos relacionados en el Editor de cartas/comunicaciones interactivas. Si desea relacionar algún tipo de contenido con estos campos, deben tener enlace.</p> <p>Si la dirección de compañía contiene más de una línea de datos, utilice el campo de texto con la opción "Permitir líneas múltiples" para representar la dirección en la presentación.</p> <p>Si el tipo de datos de un campo de texto se define como texto sin formato, se utiliza la versión de texto sin formato de la salida del módulo en lugar de la versión de texto enriquecido (se descarta todo el formato). Para conservar el formato, defina el tipo de datos del campo de texto en texto enriquecido.</p> </td>
  </tr>
  <tr>
   <td><p>El texto tiene posición variable</p> </td>
   <td><p>Los campos de texto y los campos de imagen se utilizan en las páginas de formato. Las páginas de formato no pueden utilizar subformularios como áreas de destinatario.</p> </td>
  </tr>
  <tr>
   <td><p>Los objetos se agrupan y organizan sin enlazar el subformulario a un elemento de datos</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Hay un campo de texto dentro del subformulario. El subformulario puede crecer y no sobrescribir otros objetos debajo de él en la presentación.</p> </td>
   <td><p>Es necesario acceder fácilmente a sus datos en el proceso de publicación.</p> </td>
  </tr>
 </tbody>
</table>

## Configuración de elementos repetitivos {#setting-up-repetitive-elements}

Cuando elementos como el logotipo y la dirección de su organización aparezcan en todas las páginas de una carta o comunicación interactiva, cree campos de formulario para esos elementos y colóquelos en la página de formato. Utilice el enlace Nombre (Nombre del campo) para estos campos.

## Especifique el formato de procesamiento del servidor {#specify-the-server-nbsp-render-format}

Utilice el formato de procesamiento del servidor de la presentación en Formulario XML dinámico; de lo contrario, las letras o comunicaciones interactivas basadas en este diseño no se pueden procesar correctamente. De forma predeterminada, el formato de procesamiento del servidor en Forms Designer se establece en Formulario XML dinámico. Para asegurarse de que está utilizando el formato correcto:

* En Designer, haga clic en **Archivo** > **Propiedades del formulario** > **Predeterminados** y asegúrese de que la configuración de Procesamiento/Formato de PDF está establecida en Formulario XML dinámico.

