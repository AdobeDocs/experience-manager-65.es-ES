---
title: Configuración y administración de la funcionalidad de metadatos.
description: Configuración y administración [!DNL Experience Manager Assets] de la funcionalidad relacionada con la administración y adición de metadatos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b14b377e52ab10c41355f069d97508b588d82216
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 6%

---


# Configuración y administración de la funcionalidad de metadatos en [!DNL Assets] {#config-metadata}

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] guarda los metadatos de cada recurso. Permite una clasificación y organización más sencillas de los recursos y ayuda a las personas que buscan un recurso específico. Con la capacidad de mantener y administrar metadatos con sus recursos, puede organizar y procesar automáticamente recursos en función de sus metadatos. [!DNL Adobe Experience Manager Assets] permite a los administradores configurar y personalizar la funcionalidad de metadatos para modificar la oferta de Adobe predeterminada.

## Editar esquema de metadatos {#metadata-schema}

Para obtener más información, consulte [Edición de formularios](metadata-schemas.md#edit-metadata-schema-forms)de esquema de metadatos.

## Registrar una Área de nombres personalizada en [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

Puede agregar sus propias Áreas de nombres dentro de [!DNL Experience Manager]. Al igual que hay Áreas de nombres predefinidas como `cq`, `jcr`, y `sling`, puede tener una Área de nombres para los metadatos del repositorio y el procesamiento de XML.

1. Acceda a la página de administración del tipo de nodo `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Para acceder a la página Administración de Áreas de nombres, haga clic en **[!UICONTROL Áreas de nombres]** en la parte superior de la página.
1. Para agregar una Área de nombres, haga clic en **[!UICONTROL Nuevo]** en la parte inferior de la página.
1. Especifique una Área de nombres personalizada en la convención de Área de nombres XML. Especifique el ID en forma de URI y un prefijo asociado para el ID. Haga clic en **[!UICONTROL Guardar]**.

## Configurar límites para la actualización masiva de metadatos {#bulk-metadata-update-limit}

Para evitar una situación similar a la de denegación de servicio (DOS), [!DNL Enterprise Manager] limita el número de parámetros admitidos en una solicitud de Sling. Al actualizar los metadatos de muchos recursos de una sola vez, es posible que se alcance el límite y que los metadatos no se actualicen para más recursos. Enterprise Manager genera la siguiente advertencia en los registros:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

To change the limit, access **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** and change the value of **[!UICONTROL Maximum POST Parameters]** in **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi configuration.

## Perfiles de metadatos {#metadata-profiles}

Un perfil de metadatos permite aplicar metadatos predeterminados a los recursos de una carpeta. Cree un perfil de metadatos y aplíquelo a una carpeta. Cualquier recurso que cargue posteriormente en la carpeta heredará los metadatos predeterminados configurados en el perfil de metadatos.

### Añadir un perfil de metadatos {#adding-a-metadata-profile}

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > Perfiles **** de metadatos y haga clic en **[!UICONTROL Crear]**.
1. Escriba un título para el perfil, por ejemplo `Sample Metadata`y haga clic en **[!UICONTROL Crear]**. Se muestra el perfil [!UICONTROL Editar formulario] para los metadatos.

   ![Editar un formulario de metadatos](assets/metadata-edit-form.png)

1. Haga clic en un componente y configure sus propiedades en la ficha **[!UICONTROL Configuración]** . Por ejemplo, haga clic en el componente **[!UICONTROL Descripción]** y edite sus propiedades.

   ![Configuración de un componente en el perfil de metadatos](assets/metadata-profile-component-setting.png)

   Edite las siguientes propiedades para el componente **[!UICONTROL Descripción]** :

   * **[!UICONTROL Etiqueta]** de campo: Nombre para mostrar de la propiedad metadata. Solo sirve para la referencia del usuario.

   * **[!UICONTROL Asignar a propiedad]**: El valor de esta propiedad proporciona la ruta o el nombre relativos al nodo de recurso donde se guarda en el repositorio. El valor siempre debe tener inicios `./` porque indica que la ruta está debajo del nodo del recurso.

   ![Asignar a la configuración de propiedad en el perfil de metadatos](assets/metadata-profile-setting-map-property.png)

   The value you specify for **[!UICONTROL Map to property]** is stored as a property under the asset&#39;s metadata node. Por ejemplo, si especifica `./jcr:content/metadata/dc:desc` como nombre de **[!UICONTROL Asignar a propiedad]**, [!DNL Assets] almacena el valor `dc:desc` en el nodo de metadatos del recurso.

   * **[!UICONTROL Valor]** predeterminado: Utilice esta propiedad para agregar un valor predeterminado para el componente de metadatos. Por ejemplo, si especifica &quot;Mi descripción&quot;, este valor se asigna a la propiedad `dc:desc` en el nodo de metadatos del recurso.

   ![Definir la descripción predeterminada en el perfil de metadatos](assets/metadata-profile-setting-default-value.png)

   >[!NOTE]
   >
   >Añadiendo un valor predeterminado en una nueva propiedad de metadatos (que no existe ya en la . `/jcr:content/metadata` ) no muestra la propiedad y su valor en la página Propiedades del recurso de forma predeterminada. Para vista de la nueva propiedad en la página [!UICONTROL Propiedades] de los recursos, modifique el formulario de esquema correspondiente.

1. (Opcional) Agregue más componentes a Editar formulario desde la pestaña **[!UICONTROL Generar formulario]** y configure sus propiedades en la pestaña **[!UICONTROL Configuración]**. Las siguientes propiedades están disponibles en la pestaña **[!UICONTROL Generar formulario]**:

| Componente | Propiedades |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL Sección de encabezado] | Etiqueta de campo, <br> descripción |
| [!UICONTROL Texto de una sola línea] | Etiqueta de campo, <br> Asignar a propiedad, <br> Valor predeterminado |
| [!UICONTROL Texto con varios valores] | Etiqueta de campo, <br> Asignar a propiedad, <br> Valor predeterminado |
| [!UICONTROL Número] | Etiqueta de campo, <br> Asignar a propiedad, <br> Valor predeterminado |
| [!UICONTROL Fecha] | Etiqueta de campo, <br> Asignar a propiedad, <br> Valor predeterminado |
| [!UICONTROL Etiquetas estándar] | Etiqueta de campo, <br> Asignar a propiedad, <br> Valor predeterminado, <br> Descripción |

1. Haga clic en **[!UICONTROL Finalizado]**. El Perfil Metadatos se agrega a la lista de perfiles en la página Perfiles **[!UICONTROL de]** metadatos.<br>

   ![Perfil de metadatos agregado en la página Perfiles de metadatos](assets/MetadataProfiles-page.png)

### Copiar un perfil de metadatos {#copying-a-metadata-profile}

1. En la página Perfiles **[!UICONTROL de]** metadatos, seleccione un perfil de metadatos para realizar una copia del mismo.

   ![Copiar un perfil de metadatos](assets/metadata-profile-edit-copy-option.png)

1. Click **[!UICONTROL Copy]** from the toolbar.
1. En el cuadro de diálogo **[!UICONTROL Copiar Perfil]** de metadatos, introduzca un título para la nueva copia del Perfil de metadatos.
1. Haga clic en **[!UICONTROL Copiar]**. La copia del perfil de metadatos aparece en la lista de perfiles de la página **[!UICONTROL Perfiles de metadatos]**.

   ![Se agregó una copia del perfil de metadatos en la página Perfiles de metadatos](assets/copy-metadata-profile.png)

### Eliminar un perfil de metadatos {#deleting-a-metadata-profile}

1. En la página Perfiles **[!UICONTROL de]** metadatos, seleccione un perfil para eliminarlo.

1. Haga clic en **[!UICONTROL Eliminar Perfiles]** de metadatos en la barra de herramientas.
1. En el cuadro de diálogo, haga clic en **[!UICONTROL Eliminar]** para confirmar la operación de eliminación. El perfil de metadatos se elimina de la lista.

<!-- TBD: Revisit to find out the correct config. and update these steps. When fixed, also o
These steps have been carried forward from old AEM versions. See https://helpx.adobe.com/experience-manager/6-2/assets/using/metadata-profiles.html#ApplyingaMetadataProfiletoFolders

### Configuration to apply a metadata profile globally {#apply-a-metadata-profile-globally}

In addition to applying a profile to a folder, you can also apply one globally so that any content uploaded into [!DNL Experience Manager] assets in any folder has the selected profile applied.

You can reprocess assets in a folder that already has an existing metadata profile that you later changed. See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets).

To apply a metadata profile globally, follow these steps:

* Navigate to `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` and apply the appropriate profile and click **[!UICONTROL Save]**.

  ![Apply metadata profile to a folder globally](assets/metadata-profile-folder-setting.png)

* In CRXDE Lite, navigate to the following node: `/content/dam/jcr:content`. Add the property `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>` and click **[!UICONTROL Save All]**.

  ![See applied metadata profile to a folder in the JCR in CRXDE](assets/metadata-profile-folder-setting2.png)
-->

## Esquema de metadatos de una carpeta {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets] le permite crear esquemas de metadatos para carpetas de recursos, que definen el diseño y los metadatos mostrados en las páginas de propiedades de las carpetas.

### Añadir un formulario de esquema de metadatos de carpeta {#add-a-folder-metadata-schema-form}

Utilice el editor de Forms de Esquema de metadatos de carpeta para crear y editar esquemas de metadatos para las carpetas.

1. En [!DNL Experience Manager] la interfaz, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > Esquemas **[!UICONTROL de metadatos de]** carpeta.
1. En la página [!UICONTROL Esquema de metadatos de carpeta de Forms] , haga clic en **[!UICONTROL Crear]**.
1. Specify a name for the form, and click **[!UICONTROL Create]**. El nuevo formulario de esquema aparece en la página de Forms [!UICONTROL de] Esquema.

### Edit folder metadata schema forms {#edit-folder-metadata-schema-forms}

Puede editar un formulario de esquema de metadatos recién agregado o existente, que incluye lo siguiente:

* Pestañas
* Elementos de formulario dentro de las fichas.

Puede asignar/configurar estos elementos de formulario a un campo dentro de un nodo de metadatos en el repositorio de CRX. Puede agregar nuevas fichas o elementos de formulario al formulario de esquema de metadatos.

1. En la página Esquema Forms, seleccione el formulario que ha creado y, a continuación, seleccione la opción **[!UICONTROL Editar]** en la barra de herramientas.
1. En la página Editor de Esquemas de metadatos de carpeta, haga clic en `+` para agregar una ficha al formulario. Para cambiar el nombre de la ficha, haga clic en el nombre predeterminado y especifique el nuevo nombre en **[!UICONTROL Configuración]**.

   ![custom_tab](assets/custom_tab.png)

   Para agregar más fichas, haga clic en `+`. Haga clic `X` en una ficha para eliminarla.

1. En la ficha activa, agregue uno o varios componentes de la ficha **[!UICONTROL Generar formulario]** .

   ![adding_components](assets/adding_components.png)

   Si crea varias fichas, haga clic en una ficha concreta para agregar componentes.

1. Para configurar un componente, selecciónelo y modifique sus propiedades en la ficha **[!UICONTROL Configuración]** .

   Si es necesario, elimine un componente de la ficha **[!UICONTROL Configuración]** .

   ![configure_properties](assets/configure_properties.png)

1. Haga clic en **[!UICONTROL Guardar]** en la barra de herramientas para guardar los cambios.

#### Componentes para crear formularios {#components-to-build-forms}

La ficha **[!UICONTROL Generar formulario]** lista los elementos de formulario que se utilizan en el formulario de esquema de metadatos de la carpeta. La ficha **[!UICONTROL Configuración]** muestra los atributos de cada elemento seleccionado en la ficha **[!UICONTROL Generar formulario]** . Esta es una lista de los elementos de formulario disponibles en la ficha **[!UICONTROL Generar formulario]** :

| Nombre del componente | Descripción |
|---|---|
| [!UICONTROL Sección de encabezado] | Añada un encabezado de sección para una lista de componentes comunes. |
| [!UICONTROL Texto de una sola línea] | Añada una propiedad de texto de una sola línea. Se almacena como una cadena. |
| [!UICONTROL Texto con varios valores] | Añada una propiedad de texto con varios valores. Se almacena como una matriz de cadenas. |
| [!UICONTROL Número] | Añada un componente numérico. |
| [!UICONTROL Fecha] | Añada un componente de fecha. |
| [!UICONTROL Lista desplegable] | Añada una lista desplegable. |
| [!UICONTROL Etiquetas estándar] | Añadir una etiqueta. |
| [!UICONTROL Campo oculto] | Añada un campo oculto. Se envía como parámetro de POST cuando se guarda el recurso. |

#### Edición de elementos de formulario {#editing-form-items}

Para editar las propiedades de los elementos de formulario, haga clic en el componente y edite todas o un subconjunto de las siguientes propiedades en la ficha **[!UICONTROL Configuración]** .

**[!UICONTROL Etiqueta]** de campo: Nombre de la propiedad de metadatos que se muestra en la página de propiedades de la carpeta.

**[!UICONTROL Asignar a propiedad]**: Esta propiedad especifica la ruta relativa del nodo de la carpeta en el repositorio de CRX donde se guarda. Inicio con &quot;**./**&quot;, que indica que la ruta está debajo del nodo de la carpeta.

Los siguientes son los valores válidos para esta propiedad:

* `./jcr:content/metadata/dc:title`:: Almacena el valor en el nodo de metadatos de la carpeta como propiedad `dc:title`.

* `./jcr:created`:: Muestra la propiedad JCR en el nodo de la carpeta. Si configura estas propiedades en CRXDE, Adobe recomienda marcarlas como Deshabilitar edición, ya que están protegidas. De lo contrario, el error &#39; `Asset(s) failed to modify`&#39; se produce al guardar las propiedades del recurso.

Para asegurarse de que el componente se muestra correctamente en el formulario de esquema de metadatos, no incluya ningún espacio en la ruta de la propiedad.

**[!UICONTROL Ruta]** JSON: Utilícelo para especificar la ruta del archivo JSON en la que se especifican pares de clave-valor para las opciones.

**[!UICONTROL Marcador de posición]**: Utilice esta propiedad para especificar el texto del marcador de posición correspondiente a la propiedad metadata.

**[!UICONTROL Opciones]**: Utilice esta propiedad para especificar opciones en una lista.

**[!UICONTROL Descripción]**: Utilice esta propiedad para agregar una breve descripción para el componente de metadatos.

**[!UICONTROL Clase]**: Clase de objeto con la que está asociada la propiedad.

### Delete folder metadata schema forms {#delete-folder-metadata-schema-forms}

Puede eliminar los formularios de esquema de metadatos de la carpeta desde la página de Forms Esquema de metadatos de la carpeta. Para eliminar un formulario, selecciónelo y haga clic en la opción Eliminar de la barra de herramientas.

![delete_form](assets/delete_form.png)

### Asignación de un esquema de metadatos de carpeta {#assign-a-folder-metadata-schema}

Puede asignar un esquema de metadatos de carpeta a una carpeta desde la página de Forms Esquema de metadatos de carpeta o al crear una carpeta.

Si se configura un esquema de metadatos para una carpeta, la ruta al formulario de esquema se almacena en la propiedad del nodo de la carpeta en `folderMetadataSchema` `./jcr:content`.

#### Asignar a un esquema desde la página Esquema de metadatos de la carpeta {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. En [!DNL Experience Manager] la interfaz, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > Esquemas **[!UICONTROL de metadatos de]** carpeta.
1. En la página Forms Esquema de metadatos de carpeta, seleccione el formulario de esquema que desea aplicar a una carpeta.
1. En la barra de herramientas, haga clic en **[!UICONTROL Aplicar a carpetas]**.

1. Seleccione la carpeta en la que desea aplicar el esquema y, a continuación, haga clic en **[!UICONTROL Aplicar]**. Si ya se ha aplicado un esquema de metadatos a la carpeta, aparecerá un mensaje de advertencia para informarle de que va a sobrescribir el esquema de metadatos existente. Haga clic en **[!UICONTROL Sobrescribir]**.
1. Abra las propiedades de metadatos de la carpeta a la que ha aplicado el esquema de metadatos.

   ![folder_properties](assets/folder_properties.png)

   To view the folder metadata fields, click the **[!UICONTROL Folder Metadata]** tab.

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

#### Asignar un esquema al crear una carpeta {#assign-a-schema-when-creating-a-folder}

Puede asignar un esquema de metadatos de carpeta al crear una carpeta. Si existe al menos un esquema de metadatos de carpeta en el sistema, se muestra una lista adicional en el cuadro de diálogo **[!UICONTROL Crear carpeta]** . Puede seleccionar el esquema que desee. De forma predeterminada, no hay ningún esquema seleccionado.

1. En la interfaz de usuario, haga clic en [!DNL Experience Manager Assets] Crear **** desde la barra de herramientas.
1. Especifique un título y un nombre para la carpeta.
1. En la lista Esquema de metadatos de carpeta, seleccione el esquema que desee. A continuación, haga clic en **[!UICONTROL Crear]**.

   ![select_esquema](assets/select_schema.png)

1. Abra las propiedades de metadatos de la carpeta a la que ha aplicado el esquema de metadatos.
1. To view the folder metadata fields, click the **[!UICONTROL Folder Metadata]** tab.

### Uso del esquema de metadatos de la carpeta {#use-the-folder-metadata-schema}

Abra las propiedades de una carpeta configurada con un esquema de metadatos de carpeta. A **[!UICONTROL Folder Metadata]** tab is displayed in the folder [!UICONTROL Properties] page. Para ver el formulario de esquema de metadatos de la carpeta, seleccione esta pestaña.

Introduzca valores de metadatos en los distintos campos y haga clic en **[!UICONTROL Guardar]** para almacenar los valores. Los valores que especifique se almacenan en el nodo de la carpeta en el repositorio de CRX.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

## Sugerencias y limitaciones {#best-practices-limitations}

* Para importar metadatos en Áreas de nombres personalizadas, primero registre las Áreas de nombres.
* El selector de propiedades muestra las propiedades que se utilizan en los editores de esquema y en los formularios de búsqueda. El selector de propiedades no elige propiedades de metadatos de un recurso.
* Es posible que haya perfiles de metadatos preexistentes desde entonces antes de actualizar a [!DNL Experience Manager] 6.5. Después de la actualización, si aplica este perfil en [!UICONTROL Propiedades] de carpeta en la ficha Perfiles  de metadatos, no se muestran los campos del formulario de metadatos. Sin embargo, si aplica un perfil de metadatos recién creado, los campos del formulario se muestran pero no están disponibles según lo esperado. No se pierde la funcionalidad pero si desea ver los campos del formulario (no disponibles), edite y guarde los perfiles de metadatos existentes.

>[!MORELIKETHIS]
>
>* [Conceptos y comprensión](metadata-concepts.md)de metadatos.
>* [Edite las propiedades de metadatos de varias colecciones](managing-collections-touch-ui.md#editing-collection-metadata-in-bulk).
>* [Importación y exportación de metadatos en Recursos](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html)Experience Manager.
>* [Perfiles para procesar metadatos, imágenes y vídeos](processing-profiles.md).
>* [Prácticas recomendadas para organizar los recursos digitales con el fin de utilizar perfiles](/help/assets/organize-assets.md)de procesamiento.
>* [XMP reescritura](/help/assets/xmp-writeback.md).

