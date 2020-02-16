---
title: Esquema de metadatos de carpeta
description: Obtenga información sobre cómo crear un esquema de metadatos para carpetas de recursos en Recursos AEM
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
uuid: bf8d066c-0f23-4d18-9ce9-860fa505dea2
discoiquuid: 23009e50-a026-4823-8e4c-7a313a11b38c
docset: aem65
translation-type: tm+mt
source-git-commit: 62cc3282f8d8bc77f072de1d027484bd93efa38a

---


# Folder metadata schema {#folder-metadata-schema}

Recursos Adobe Experience Manager (AEM) le permite crear esquemas de metadatos para carpetas de recursos, que definen el diseño y los metadatos que se muestran en las páginas de propiedades de la carpeta.

## Adición de un formulario de esquema de metadatos de carpeta {#add-a-folder-metadata-schema-form}

Utilice el editor de formularios de esquemas de metadatos de carpeta para crear y editar esquemas de metadatos para carpetas.

1. Toque o haga clic en el logotipo de AEM y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > Esquemas **[!UICONTROL de metadatos de carpeta]**.
1. En la página Formularios de esquema de metadatos de la carpeta, toque o haga clic en **[!UICONTROL Crear]**.
1. Especifique un nombre para el formulario y toque o haga clic en **[!UICONTROL Crear]**. El nuevo formulario de esquema aparece en la página Formularios de esquema.

## Edit folder metadata schema forms {#edit-folder-metadata-schema-forms}

Puede editar un formulario de esquema de metadatos recién agregado o existente, que incluye lo siguiente:

* Pestañas
* Elementos de formulario dentro de las fichas.

Puede asignar/configurar estos elementos de formulario a un campo dentro de un nodo de metadatos en el repositorio de CRX. Puede agregar nuevas fichas o elementos de formulario al formulario de esquema de metadatos.

1. En la página Formularios de esquema, seleccione el formulario que ha creado y, a continuación, toque o haga clic en el icono **[!UICONTROL Editar]** de la barra de herramientas.
1. En la página Editor de esquemas de metadatos de la carpeta, toque `+` para agregar una ficha al formulario. Para cambiar el nombre de la ficha, toque o haga clic en el nombre predeterminado y especifique el nuevo nombre en **[!UICONTROL Configuración]**.

   ![custom_tab](assets/custom_tab.png)

   Para agregar más fichas, toque `+`. Toque `X` en una ficha para eliminarla.

1. En la ficha activa, agregue uno o varios componentes de la ficha **[!UICONTROL Generar formulario]** .

   ![adding_components](assets/adding_components.png)

   Si crea varias fichas, toque o haga clic en una ficha concreta para agregar componentes.

1. Para configurar un componente, selecciónelo y modifique sus propiedades en la ficha **[!UICONTROL Configuración]** .

   Si es necesario, elimine un componente de la ficha **[!UICONTROL Configuración]** .

   ![configure_properties](assets/configure_properties.png)

1. Toque o haga clic en **[!UICONTROL Guardar]** en la barra de herramientas para guardar los cambios.

### Componentes para crear formularios {#components-to-build-forms}

La ficha **[!UICONTROL Generar formulario]** muestra los elementos de formulario que se utilizan en el formulario de esquema de metadatos de la carpeta. La ficha **[!UICONTROL Configuración]** muestra los atributos de cada elemento seleccionado en la ficha **[!UICONTROL Generar formulario]** . A continuación se muestra una lista de los elementos de formulario disponibles en la ficha **[!UICONTROL Generar formulario]** :

| Nombre del componente | Descripción |
|---|---|
| [!UICONTROL Sección de encabezado] | Agregue un encabezado de sección para ver una lista de componentes comunes. |
| [!UICONTROL Texto de una sola línea] | Agregue una propiedad de texto de una sola línea. Se almacena como una cadena. |
| [!UICONTROL Texto con varios valores] | Agregue una propiedad de texto con varios valores. Se almacena como una matriz de cadenas. |
| [!UICONTROL Número] | Agregue un componente numérico. |
| [!UICONTROL Fecha] | Agregue un componente de fecha. |
| [!UICONTROL Lista desplegable] | Agregue una lista desplegable. |
| [!UICONTROL Etiquetas estándar] | Añadir una etiqueta. |
| [!UICONTROL Campo oculto] | Agregue un campo oculto. Se envía como parámetro POST cuando se guarda el recurso. |

### Edición de elementos de formulario {#editing-form-items}

Para editar las propiedades de los elementos de formulario, toque o haga clic en el componente y edite todo o un subconjunto de las siguientes propiedades en la ficha **[!UICONTROL Configuración]** .

**[!UICONTROL Etiqueta]** de campo: Nombre de la propiedad de metadatos que se muestra en la página de propiedades de la carpeta.

**[!UICONTROL Asignar a propiedad]**: Esta propiedad especifica la ruta relativa del nodo de la carpeta en el repositorio de CRX donde se guarda. Comienza con &quot;**./**&quot;, que indica que la ruta está debajo del nodo de la carpeta.

Los siguientes son los valores válidos para esta propiedad:

* `./jcr:content/metadata/dc:title`:: Almacena el valor en el nodo de metadatos de la carpeta como propiedad `dc:title`.

* `./jcr:created`:: Muestra la propiedad JCR en el nodo de la carpeta. Si configura estas propiedades en CRXDE, Adobe recomienda marcarlas como Deshabilitar edición, ya que están protegidas. De lo contrario, el error &#39; `Asset(s) failed to modify`&#39; se produce al guardar las propiedades del recurso.

Para asegurarse de que el componente se muestra correctamente en el formulario de esquema de metadatos, no incluya ningún espacio en la ruta de la propiedad.

**[!UICONTROL Ruta]** JSON: Utilícelo para especificar la ruta del archivo JSON en la que se especifican pares de clave-valor para las opciones.

**[!UICONTROL Marcador de posición]**: Utilice esta propiedad para especificar el texto del marcador de posición correspondiente a la propiedad metadata.

**[!UICONTROL Opciones]**: Utilice esta propiedad para especificar opciones en una lista.

**[!UICONTROL Descripción]**: Utilice esta propiedad para agregar una breve descripción para el componente de metadatos.

**[!UICONTROL Clase]**: Clase de objeto con la que está asociada la propiedad.

## Delete folder metadata schema forms {#delete-folder-metadata-schema-forms}

Puede eliminar formularios de esquema de metadatos de carpeta desde la página Formularios de esquema de metadatos de carpeta. Para eliminar un formulario, selecciónelo y toque o haga clic en el icono Eliminar de la barra de herramientas.

![delete_form](assets/delete_form.png)

## Asignación de un esquema de metadatos de carpeta {#assign-a-folder-metadata-schema}

Puede asignar un esquema de metadatos de carpeta a una carpeta desde la página Formularios de esquema de metadatos de carpeta o al crear una carpeta.

Si configura un esquema de metadatos para una carpeta, la ruta al formulario de esquema se almacena en la propiedad del nodo de carpeta en la `folderMetadataSchema` .*/jcr:content*.

### Asignar a un esquema desde la página Esquema de metadatos de la carpeta {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. Toque o haga clic en el logotipo de AEM y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]**> Esquemas **[!UICONTROL de metadatos de carpeta]**.
1. En la página Formularios de esquema de metadatos de carpeta, seleccione el formulario de esquema que desee aplicar a una carpeta.
1. En la barra de herramientas, toque o haga clic en **[!UICONTROL Aplicar a carpetas]**.

1. Seleccione la carpeta en la que desea aplicar el esquema y toque o haga clic en **[!UICONTROL Aplicar]**. Si ya se ha aplicado un esquema de metadatos en la carpeta, un mensaje de advertencia indicará que está a punto de sobrescribir el esquema de metadatos existente. Toque o haga clic en **[!UICONTROL Sobrescribir]**.
1. Abra las propiedades de metadatos de la carpeta a la que ha aplicado el esquema de metadatos.

   ![folder_properties](assets/folder_properties.png)

   Para ver los campos de metadatos de la carpeta, toque o haga clic en la ficha Metadatos **[!UICONTROL de la]** carpeta.

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

### Asignar un esquema al crear una carpeta {#assign-a-schema-when-creating-a-folder}

Puede asignar un esquema de metadatos de carpeta al crear una carpeta. Si existe al menos un esquema de metadatos de carpeta en el sistema, se muestra una lista adicional en el cuadro de diálogo **[!UICONTROL Crear carpeta]** . Puede seleccionar el esquema deseado. De forma predeterminada, no hay ningún esquema seleccionado.

1. En la interfaz de usuario de Recursos AEM, toque o haga clic en **[!UICONTROL Crear]** desde la barra de herramientas.
1. Especifique un título y un nombre para la carpeta.
1. En la lista Esquema de metadatos de carpeta, seleccione el esquema deseado. Then, tap/click **[!UICONTROL Create]**.

   ![select_schema](assets/select_schema.png)

1. Abra las propiedades de metadatos de la carpeta a la que ha aplicado el esquema de metadatos.
1. Para ver los campos de metadatos de la carpeta, toque o haga clic en la ficha Metadatos **[!UICONTROL de la]** carpeta.

## Uso del esquema de metadatos de la carpeta {#use-the-folder-metadata-schema}

Abra las propiedades de una carpeta configurada con un esquema de metadatos de carpeta. Se muestra una ficha Metadatos **[!UICONTROL de]** carpeta en la página de propiedades de la carpeta. Para ver el formulario de esquema de metadatos de la carpeta, seleccione esta ficha.

Introduzca valores de metadatos en los distintos campos y toque o haga clic en **[!UICONTROL Guardar]** para almacenar los valores. Los valores que especifique se almacenan en el nodo de la carpeta en el repositorio de CRX.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

