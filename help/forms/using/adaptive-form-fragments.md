---
title: Fragmentos de formulario adaptables
seo-title: Fragmentos de formulario adaptables
description: Los formularios adaptables proporcionan un mecanismo para crear un segmento de formulario, como un panel o un grupo de campos, tal como se utiliza en cualquier formulario adaptable. También puede guardar un panel existente como fragmento.
seo-description: Los formularios adaptables proporcionan un mecanismo para crear un segmento de formulario, como un panel o un grupo de campos, tal como se utiliza en cualquier formulario adaptable. También puede guardar un panel existente como fragmento.
uuid: bb4830b5-82a0-4026-9dae-542daed10e6f
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 1a32eb24-db3b-4fad-b1c7-6326b5af4e5e
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Adaptive form fragments{#adaptive-form-fragments}

Aunque cada formulario está diseñado para un propósito específico, hay algunos segmentos comunes en la mayoría de las formas, como proporcionar detalles personales como nombre y dirección, detalles de familia, detalles de ingresos, etc. Los desarrolladores de formularios deben crear estos segmentos comunes cada vez que se cree un nuevo formulario.

Los formularios adaptables proporcionan un mecanismo cómodo para crear segmentos de formulario como un panel o un grupo de campos una sola vez y reutilizarlos en formularios adaptables. Estos segmentos reutilizables y independientes se denominan fragmentos de formulario adaptables.

## Creación de un fragmento {#create-a-fragment}

Puede crear un fragmento de formulario adaptable desde cero o guardar un panel en un formulario adaptable existente como fragmento.

### Crear fragmento desde cero {#create-fragment-from-scratch}

1. Inicie sesión en la instancia de creación de AEM Forms en https://[*hostname*]:[*port*]/aem/forms.html.
1. Click **Create > Adaptive Form Fragment**.
1. Especifique el título, el nombre, la descripción y las etiquetas del fragmento.

   >[!NOTE]
   >
   >Asegúrese de especificar un nombre único para el fragmento. Si ya existe otro fragmento con el mismo nombre, no se puede crear el fragmento.

1. Haga clic para abrir la ficha Modelo **de** formulario y, en el menú desplegable **Seleccionar desde** , seleccione uno de los siguientes modelos para el fragmento:

   * **Ninguno**: Especifica que se cree el fragmento desde cero sin utilizar ningún modelo de formulario.
   * **Plantilla** de formulario: Especifica la creación del fragmento mediante una plantilla XDP cargada en AEM Forms. Seleccione la plantilla XDP adecuada como modelo de formulario para el fragmento.
   ![Creación de un formulario adaptable mediante una plantilla de formulario como modelo](assets/form-template-model.png)

   También se muestran los subformularios marcados como fragmentos en la plantilla de formulario seleccionada. Puede seleccionar un subformulario para el fragmento de formulario adaptable desde la lista desplegable.

   ![Seleccionar subformularios de la plantilla de formulario especificada](assets/fragment-subform.png)

   Además, puede crear un fragmento de formulario adaptable utilizando subformularios que no estén marcados como fragmentos en la plantilla de formulario especificando la expresión SOM para el subformulario en el cuadro desplegable.

   * **Esquema** XML: Especifica que se crea el fragmento con un esquema XML cargado en AEM Forms. Puede cargar o seleccionar los esquemas XML disponibles como modelo de formulario para el fragmento.
   ![Creación de un fragmento de formulario adaptable basado en un esquema XML como modelo](assets/xml-schema-model.png)

   También puede crear un fragmento de formulario adaptable seleccionando un valor de complejoType presente en el esquema seleccionado en el cuadro desplegable.

   ![Seleccione un tipo complejo del modelo de esquema XML especificado](assets/complex-type.png)

1. Haga clic en **Crear** y, a continuación, en **Abrir** para abrir el fragmento, con una plantilla predeterminada, en modo de edición.

En el modo de edición, puede arrastrar y soltar cualquier componente de formulario adaptable de la barra de tareas de AEM en el fragmento. Para obtener información sobre los componentes de formularios adaptables, consulte [Introducción a la creación de formularios](../../forms/using/introduction-forms-authoring.md)adaptables.

Además, si ha seleccionado un esquema XML o una plantilla de formulario XDP como modelo de formulario para el fragmento, aparecerá una nueva ficha con la jerarquía de modelo de formulario en el buscador de contenido. Permite arrastrar y soltar elementos del modelo de formulario en el fragmento. Los elementos de modelo de formulario añadidos se convierten en componentes de formulario y se mantienen las propiedades originales del XDP o XSD asociados.

### Guardar el panel como un fragmento {#save-panel-as-a-fragment}

1. Abra un formulario adaptable que contenga el panel que desee guardar como fragmento de formulario adaptable.
1. En la barra de herramientas del panel, haga clic en **[!UICONTROL Guardar como fragmento]**. Se abre el cuadro de diálogo Guardar como fragmento.

   >[!NOTE]
   >
   >Si el panel que está guardando como fragmento contiene un panel secundario, el fragmento resultante lo incluirá.

1. En el cuadro de diálogo Creación de fragmentos, especifique la siguiente información:

   * **Nombre**: Nombre del fragmento. El valor predeterminado es el nombre del elemento del panel. Es un campo obligatorio.
      ***Nota **: Asegúrese de especificar un nombre único para el fragmento. Si ya existe otro fragmento con el mismo nombre, no se puede crear el fragmento.*

   * **Título**: Título del fragmento. El valor predeterminado es el título del panel.

   * **Descripción**: Descripción del fragmento.

   * **Etiquetas**: Etiqueta metadatos para el fragmento.

   * **Ruta** de Destinatario: Ruta del repositorio donde se guardará el fragmento. Si no especifica una ruta, se crea un nodo con el mismo nombre que el del fragmento junto al nodo que contiene el formulario adaptable. El fragmento se guarda en este nodo.

   * **Modelo** de formulario: Según el modelo de formulario para el formulario adaptable, este campo muestra el Esquema **** XML, la plantilla **de** formulario o **Ninguno**. Es un campo no editable.

   * **Raíz** del modelo de fragmento: Solo aparece en formularios adaptables basados en XSD. Especifica la raíz del modelo de fragmento. Puede elegir **/** o el tipo de complejo XSD en la lista desplegable. Tenga en cuenta que sólo puede reutilizar el fragmento en otro formulario adaptable si selecciona el tipo complejo como raíz del modelo de fragmento.
Si elige **/** como raíz del modelo de fragmento, el árbol XSD completo de la raíz estará visible en la ficha del modelo de datos de formulario adaptable. Para una raíz de modelo de fragmento de tipo complejo, solo los descendientes del tipo complejo seleccionado están visibles en la ficha del modelo de datos de formulario adaptable.

   * **Ref** XSD: Solo aparece en formularios adaptables basados en XSD. Muestra la ubicación del esquema XML.

   * **Ref** XDP: Solo aparece en formularios adaptables basados en XDP. Muestra la ubicación de la plantilla de formulario XDP.
   ![save-fragment](assets/save-fragment.png)

   Cuadro de diálogo Guardar como fragmento

1. Haga clic en **Aceptar**.

   El panel se guarda en la ubicación especificada o predeterminada del repositorio. En el formulario adaptable, el panel se sustituye por una instantánea del fragmento. Como se muestra a continuación, el panel Información general y sus paneles secundarios, Información personal y Dirección, se guardan como un fragmento.

   Para editar el fragmento, haga clic en **[!UICONTROL Editar recurso]** en la barra de herramientas del panel. El fragmento se abre en una nueva ficha o ventana en modo de edición.

   ![Edición de fragmento](assets/edit-fragment.png)

## Uso de fragmentos {#working-with-fragments}

### Configuración del aspecto del fragmento {#configure-fragment-appearance}

Cualquier fragmento que inserte en formularios adaptables aparecerá como una imagen de marcador de posición. El marcador de posición muestra títulos de hasta un máximo de diez paneles secundarios en el fragmento. Puede configurar AEM Forms para que muestre el fragmento completo en lugar de la imagen del marcador de posición.

Realice los siguientes pasos para mostrar fragmentos completos en los formularios:

1. Vaya a la página de configuración de la consola web de AEM en https:[*host*]:[*port*]/system/console/configMgr.

1. Busque y haga clic en Servicio **** de configuración de formulario adaptable para abrirlo en modo de edición.
1. Desactive la **[!UICONTROL casilla de verificación Habilitar marcador de posición en lugar de Fragmento]** para mostrar fragmentos completos en lugar de la imagen de marcador de posición.

### Inserción de un fragmento en un formulario adaptable {#insert-a-fragment-in-an-adaptive-form}

Los fragmentos de formulario adaptables que cree aparecerán en la ficha Fragmentos de formulario adaptables del buscador de contenido de AEM. Inserción de un fragmento de formulario adaptable en un formulario adaptable:

1. Abra el formulario adaptable, en modo de edición, en el que desea insertar un fragmento de formulario adaptable.
1. Haga clic en **Recursos** navegador ![de](assets/assets-browser.png) recursos en la barra lateral. En el navegador de recursos, seleccione Fragmentos **de formulario** adaptables en la lista desplegable.

   También puede elegir mostrar todos los fragmentos de formulario adaptables o filtrar según su modelo de formulario: Plantilla de formulario, Esquema XML o Básico.

1. Arrastre y suelte un fragmento de formulario adaptable en el formulario adaptable.

   >[!NOTE]
   >
   >El fragmento de formulario adaptable no está habilitado para la creación desde el formulario adaptable. Además, no se puede utilizar un fragmento basado en XSD en un formulario adaptable basado en JSON y de la forma opuesta.

El fragmento de formulario adaptable se inserta por referencia en el formulario adaptable y se sincroniza con el fragmento de formulario adaptable independiente. Significa que, al actualizar el fragmento de formulario adaptable, los cambios se reflejan en todos los formularios adaptables en los que se utiliza el fragmento.

### Incrustar un fragmento en un formulario adaptable {#embed-a-fragment-in-adaptive-form}

Puede incrustar un fragmento de formulario adaptable en un formulario adaptable haciendo clic en **Incrustar recurso: Botón &lt;*fragmentName*>** en la barra de herramientas del panel del fragmento agregado, como se muestra en la siguiente imagen de ejemplo.

![Incrustar un fragmento de formulario en un formulario adaptable](assets/embed-fragment.png)

>[!NOTE]
>
>El fragmento incrustado ya no está vinculado al fragmento independiente. Puede editar los componentes del fragmento incrustado desde el formulario adaptable.

### Uso de fragmentos dentro de fragmentos {#using-fragments-within-fragments}

Puede crear fragmentos de formulario adaptables anidados, lo que significa que puede arrastrar y soltar un fragmento en otro fragmento y puede tener una estructura de fragmento anidada.

### Cambio de fragmentos {#change-fragments}

Puede reemplazar o cambiar un fragmento de formulario adaptable por otro fragmento mediante la propiedad **Seleccionar fragmento de recurso** en el cuadro de diálogo Editar componente para un panel de fragmento de formulario adaptable.

## Asignación automática de fragmentos para el enlace de datos {#auto-mapping-of-fragments-for-data-binding}

Cuando se crea un fragmento de formulario adaptable mediante una plantilla de formulario XFA o un tipo complejo XSD y se arrastra y se suelta el fragmento en un formulario adaptable, el fragmento XFA o el tipo complejo XSD se reemplazan automáticamente por el fragmento de formulario adaptable correspondiente cuya raíz del modelo de fragmento se asigna al fragmento XFA o al tipo complejo XSD.

Puede cambiar el recurso de fragmento y sus enlaces desde el cuadro de diálogo Editar componente.

>[!NOTE]
>
>También puede arrastrar y soltar un fragmento de formulario adaptable enlazado desde la biblioteca de fragmentos de formulario adaptable en AEM Content Finder y proporcionar la referencia de enlace correcta desde el cuadro de diálogo Editar componente del panel de fragmentos de formulario adaptable.

## Administrar fragmentos {#manage-fragments}

Puede realizar varias operaciones en fragmentos de formulario adaptables mediante la interfaz de usuario de AEM Forms.

1. Ir a `https://[hostname]:'port'/aem/forms.html`.

1. Haga clic en **Seleccionar** en la barra de herramientas de la interfaz de usuario de AEM Forms y seleccione un fragmento de formulario adaptable. La barra de herramientas muestra las siguientes operaciones que puede realizar en el fragmento de formulario adaptable seleccionado.

<table>
 <tbody>
  <tr>
   <td><p><strong>Operación</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p>Abra</p> </td>
   <td><p>Abre el fragmento de formulario adaptable seleccionado en modo de edición.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Ver propiedades</p> </td>
   <td><p>Abre el panel Propiedades. Desde el panel Propiedades, puede realizar vistas y editar propiedades, generar una previsualización y cargar una imagen en miniatura para el fragmento seleccionado. For more information, see <a href="../../forms/using/manage-form-metadata.md" target="_blank">Managing metadata</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Copiar</p> </td>
   <td><p>Copia el fragmento seleccionado. El botón Pegar aparece en la barra de herramientas.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Descargar</p> </td>
   <td><p>Descarga el fragmento seleccionado.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Vista previa</p> </td>
   <td><p>Proporciona opciones para la previsualización del fragmento como HTML o una previsualización personalizada mediante la combinación de datos de un archivo XML con el fragmento. Para obtener más información, consulte <a href="/help/forms/using/previewing-forms.md" target="_blank">Vista previa de un formulario</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Revisión/Administrar revisión de Inicio</p> </td>
   <td><p>Permite iniciar y administrar una revisión del fragmento seleccionado. Para obtener más información, consulte <a href="../../forms/using/create-reviews-forms.md" target="_blank">Creación y administración de revisiones</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Crear diccionario</p> </td>
   <td><p>Genera un diccionario para localizar el fragmento seleccionado. Para obtener más información, consulte <a href="/help/forms/using/lazy-loading-adaptive-forms.md" target="_blank">Localización de formularios</a>adaptables.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Publicar o cancelar la publicación</p> </td>
   <td><p>Publica o anula la publicación del fragmento seleccionado.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Eliminar</p> </td>
   <td><p>Elimina el fragmento seleccionado.<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## Localización de formularios adaptables que contienen fragmentos {#localizing-adaptive-form-containing-fragments}

Para localizar un formulario adaptable que contenga fragmentos de formulario adaptables, debe localizar el fragmento y el formulario por separado. La idea es localizar un fragmento una vez y reutilizarlo en varios formularios adaptables.

>[!NOTE]
>
>Las claves de localización del fragmento no aparecerán en el archivo XLIFF para un formulario adaptable.

## Puntos clave que recordar al trabajar con fragmentos {#key-points-to-remember-when-working-with-fragments}

* Asegúrese de que el nombre del fragmento sea único. El fragmento no se puede crear si hay un fragmento existente con el mismo nombre.
* En un formulario adaptable basado en XDP, si guarda un panel como fragmento que incluye otro fragmento XDP, el fragmento resultante se enlazará automáticamente al fragmento XDP secundario. En el caso de un formulario adaptable basado en XSD, el fragmento resultante se enlazará a la raíz del esquema.
* Cuando se crea un fragmento de formulario adaptable, se crea un nodo de fragmento, similar al nodo guideContainer de un formulario adaptable, en CRXDe Lite.
* No se admite un fragmento en un formulario adaptable que utilice un modelo de datos de formulario diferente. Por ejemplo, un fragmento basado en XDP no se admite en un formulario adaptable basado en XSD y viceversa.
* Los fragmentos de formulario adaptables están disponibles para su uso a través de la ficha Fragmentos de formulario adaptables de AEM Content Finder.
* Cualquier expresión, secuencia de comandos o estilo de un fragmento de formulario adaptable independiente se conserva cuando se inserta por referencia o se incrusta en un formulario adaptable.
* No se puede editar un fragmento de formulario adaptable, que se inserta por referencia, desde un formulario adaptable. Para editar, edite el fragmento de formulario adaptable independiente o incruste el fragmento en el formulario adaptable.
* Cuando publica un formulario adaptable, debe publicar los fragmentos de formulario adaptable independientes insertados por referencia en el formulario adaptable.
* Al volver a publicar un fragmento de formulario adaptable actualizado, los cambios se reflejan en las instancias publicadas del formulario adaptable en el que se utiliza el fragmento.
* El formulario adaptable que contiene el componente Verificar no admite usuarios anónimos. Además, no se recomienda utilizar el componente Verificar en un fragmento de formulario adaptable.
* (Solo **Mac**) Para asegurarse de que la funcionalidad de los fragmentos de formulario funciona perfectamente en todos los escenarios, agregue la siguiente entrada al archivo /private/etc/hosts:
   `127.0.0.1 <Host machine>` Equipo **host**: El ordenador Apple Mac en el que se implementa AEM Forms.

## Fragmentos de referencia {#reference-fragments}

Hay disponibles fragmentos de formulario adaptables de referencia que se pueden utilizar para crear el formulario. For more information, see [Reference Fragments](../../forms/using/reference-adaptive-form-fragments.md).
