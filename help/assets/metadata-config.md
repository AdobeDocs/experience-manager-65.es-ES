---
title: Configuración y administración de la funcionalidad de metadatos.
description: Configuración y administración de la funcionalidad [!DNL Experience Manager Assets] relacionada con la adición y administración de metadatos.
contentOwner: AG
role: Profesional empresarial, administrador
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '1954'
ht-degree: 6%

---


# Configuración y administración de la funcionalidad de metadatos en [!DNL Assets] {#config-metadata}

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] conserva los metadatos de cada recurso. Permite una categorización y organización más sencillas de los recursos, y ayuda a las personas que buscan un recurso específico. Con la capacidad de mantener y administrar metadatos con los recursos, puede organizar y procesar automáticamente los recursos en función de sus metadatos. [!DNL Adobe Experience Manager Assets] permite a los administradores configurar y personalizar la funcionalidad de metadatos para modificar la oferta de Adobe predeterminada.

## Editar esquema de metadatos {#metadata-schema}

Para obtener más información, consulte [edición de formularios de esquema de metadatos](metadata-schemas.md#edit-metadata-schema-forms).

## Registrar un espacio de nombres personalizado en [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

Puede agregar sus propios espacios de nombres dentro de [!DNL Experience Manager]. Del mismo modo que hay áreas de nombres predefinidas como `cq`, `jcr` y `sling`, puede tener un área de nombres para los metadatos del repositorio y el procesamiento XML.

1. Acceda a la página de administración del tipo de nodo `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Para acceder a la página de administración del área de nombres, haga clic en **[!UICONTROL Espacios de nombres]** en la parte superior de la página.
1. Para agregar un área de nombres, haga clic en **[!UICONTROL New]** en la parte inferior de la página.
1. Especifique un área de nombres personalizada en la convención de área de nombres XML. Especifique el ID en forma de URI y un prefijo asociado para el ID. Haga clic en **[!UICONTROL Guardar]**.

## Configurar límites para la actualización de metadatos masivos {#bulk-metadata-update-limit}

Para evitar una situación similar a la de denegación de servicio (DOS), [!DNL Enterprise Manager] limita el número de parámetros admitidos en una solicitud de Sling. Al actualizar los metadatos de muchos recursos de una sola vez, puede que llegue al límite y los metadatos no se actualicen para obtener más recursos. Enterprise Manager genera la siguiente advertencia en los registros:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

Para cambiar el límite, acceda a **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** y cambie el valor de **[!UICONTROL Maximum POST Parameters]** en la configuración OSGi de **[!UICONTROL Apache Sling Request Parameter Handling]**.

## Perfiles de metadatos {#metadata-profiles}

Un perfil de metadatos permite aplicar metadatos predeterminados a los recursos de una carpeta. Cree un perfil de metadatos y aplíquelo a una carpeta. Cualquier recurso que suba a la carpeta hereda los metadatos predeterminados que haya configurado en el perfil de metadatos.

### Añadir un perfil de metadatos {#adding-a-metadata-profile}

1. Vaya a **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Profiles]** y haga clic en **[!UICONTROL Create]**.
1. Introduzca un título para el perfil, por ejemplo `Sample Metadata`, y haga clic en **[!UICONTROL Crear]**. Se muestra el [!UICONTROL Editar formulario] para el perfil de metadatos.

   ![Editar un formulario de metadatos](assets/metadata-edit-form.png)

1. Haga clic en un componente y configure sus propiedades en la pestaña **[!UICONTROL Settings]**. Por ejemplo, haga clic en el componente **[!UICONTROL Description]** y edite sus propiedades.

   ![Configuración de un componente en el perfil de metadatos](assets/metadata-profile-component-setting.png)

   Edite las siguientes propiedades para el componente **[!UICONTROL Description]**:

   * **[!UICONTROL Etiqueta]** de campo: Nombre para mostrar de la propiedad metadata. Solo es para referencia del usuario.

   * **[!UICONTROL Asignar a propiedad]**: El valor de esta propiedad proporciona la ruta o el nombre relativos al nodo de recurso donde se guarda en el repositorio. El valor siempre debe comenzar por `./` porque indica que la ruta está bajo el nodo del recurso.

   ![Asignar a la configuración de propiedad en el perfil de metadatos](assets/metadata-profile-setting-map-property.png)

   El valor que especifique para **[!UICONTROL Asignar a la propiedad]** se almacena como una propiedad en el nodo de metadatos del recurso. Por ejemplo, si especifica `./jcr:content/metadata/dc:desc` como nombre de **[!UICONTROL Asignar a la propiedad]**, [!DNL Assets] almacena el valor `dc:desc` en el nodo de metadatos del recurso.

   * **[!UICONTROL Valor]** predeterminado: Utilice esta propiedad para añadir un valor predeterminado para el componente de metadatos. Por ejemplo, si especifica &quot;Mi descripción&quot;, este valor se asigna a la propiedad `dc:desc` en el nodo de metadatos del recurso.

   ![Establecer una descripción predeterminada en el perfil de metadatos](assets/metadata-profile-setting-default-value.png)

   >[!NOTE]
   >
   >Añadir un valor predeterminado a una nueva propiedad de metadatos (que no existe ya en . `/jcr:content/metadata` ) no muestra la propiedad y su valor en la página Propiedades del recurso de forma predeterminada. Para ver la nueva propiedad en la página [!UICONTROL Properties] de los recursos, modifique el formulario de esquema correspondiente.

1. (Opcional) Agregue más componentes a Editar formulario desde la pestaña **[!UICONTROL Generar formulario]** y configure sus propiedades en la pestaña **[!UICONTROL Configuración]**. Las siguientes propiedades están disponibles en la pestaña **[!UICONTROL Generar formulario]**:

| Componente | Propiedades |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL Sección de encabezado] | Etiqueta de campo, <br> Descripción |
| [!UICONTROL Texto de una sola línea] | Etiqueta de campo, <br> Asignar a propiedad, <br> Valor predeterminado |
| [!UICONTROL Texto con varios valores] | Etiqueta de campo, <br> Asignar a propiedad, <br> Valor predeterminado |
| [!UICONTROL Número] | Etiqueta de campo, <br> Asignar a propiedad, <br> Valor predeterminado |
| [!UICONTROL Fecha] | Etiqueta de campo, <br> Asignar a propiedad, <br> Valor predeterminado |
| [!UICONTROL Etiquetas estándar] | Etiqueta de campo, <br> Asignar a propiedad, <br> Valor predeterminado, <br> Descripción |

1. Haga clic en **[!UICONTROL Listo]**. El perfil de metadatos se agrega a la lista de perfiles de la página **[!UICONTROL Perfiles de metadatos]**.<br>

   ![Perfil de metadatos añadido en la página Perfiles de metadatos](assets/MetadataProfiles-page.png)

### Copiar un perfil de metadatos {#copying-a-metadata-profile}

1. En la página **[!UICONTROL Perfiles de metadatos]**, seleccione un perfil de metadatos para realizar una copia de él.

   ![Copiar un perfil de metadatos](assets/metadata-profile-edit-copy-option.png)

1. Haga clic en **[!UICONTROL Copiar]** en la barra de herramientas.
1. En el cuadro de diálogo **[!UICONTROL Copiar perfil de metadatos]**, introduzca un título para la nueva copia del perfil de metadatos.
1. Haga clic en **[!UICONTROL Copiar]**. La copia del perfil de metadatos aparece en la lista de perfiles de la página **[!UICONTROL Perfiles de metadatos]**.

   ![Una copia del perfil de metadatos añadido en la página Perfiles de metadatos](assets/copy-metadata-profile.png)

### Eliminar un perfil de metadatos {#deleting-a-metadata-profile}

1. En la página **[!UICONTROL Perfiles de metadatos]**, seleccione un perfil que desee eliminar.

1. Haga clic en **[!UICONTROL Eliminar perfiles de metadatos]** en la barra de herramientas.
1. En el cuadro de diálogo, haga clic en **[!UICONTROL Delete]** para confirmar la operación de eliminación. El perfil de metadatos se elimina de la lista.

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

## Esquema de metadatos para una carpeta {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets] le permite crear esquemas de metadatos para carpetas de recursos, que definen el diseño y los metadatos mostrados en las páginas de propiedades de las carpetas.

### Agregar un formulario de esquema de metadatos de carpeta {#add-a-folder-metadata-schema-form}

Utilice el editor Forms de Esquemas de metadatos de carpeta para crear y editar esquemas de metadatos para carpetas.

1. En la interfaz [!DNL Experience Manager], vaya a **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Folder Metadata schemas]**.
1. En la página [!UICONTROL Folder Metadata Schema Forms], haga clic en **[!UICONTROL Create]**.
1. Especifique un nombre para el formulario y haga clic en **[!UICONTROL Crear]**. El nuevo formulario de esquema aparece en la página [!UICONTROL Schema Forms].

### Editar formularios de esquema de metadatos de carpeta {#edit-folder-metadata-schema-forms}

Puede editar un formulario de esquema de metadatos nuevo o existente, que incluye lo siguiente:

* Pestañas
* Elementos de formulario dentro de las pestañas.

Puede asignar/configurar estos elementos de formulario a un campo dentro de un nodo de metadatos en el repositorio CRX. Puede agregar nuevas fichas o elementos de formulario al formulario de esquema de metadatos.

1. En la página Esquema de Forms, seleccione el formulario que ha creado y, a continuación, seleccione la opción **[!UICONTROL Editar]** en la barra de herramientas.
1. En la página Editor de esquemas de metadatos de carpeta , haga clic en `+` para agregar una pestaña al formulario. Para cambiar el nombre de la ficha, haga clic en el nombre predeterminado y especifique el nuevo nombre en **[!UICONTROL Configuración]**.

   ![custom_tab](assets/custom_tab.png)

   Para agregar más pestañas, haga clic en `+`. Haga clic `X` en una pestaña para eliminarla.

1. En la ficha activa, agregue uno o más componentes de la pestaña **[!UICONTROL Generar formulario]**.

   ![add_components](assets/adding_components.png)

   Si crea varias fichas, haga clic en una ficha concreta para agregar componentes.

1. Para configurar un componente, selecciónelo y modifique sus propiedades en la pestaña **[!UICONTROL Settings]**.

   Si es necesario, elimine un componente de la ficha **[!UICONTROL Configuración]**.

   ![configure_properties](assets/configure_properties.png)

1. Haga clic en **[!UICONTROL Guardar]** en la barra de herramientas para guardar los cambios.

#### Componentes para crear formularios {#components-to-build-forms}

La ficha **[!UICONTROL Generar formulario]** enumera los elementos de formulario que utiliza en el formulario de esquema de metadatos de la carpeta. La ficha **[!UICONTROL Configuración]** muestra los atributos de cada elemento que seleccione en la ficha **[!UICONTROL Generar formulario]**. A continuación se muestra una lista de los elementos de formulario disponibles en la pestaña **[!UICONTROL Generar formulario]**:

| Nombre del componente | Descripción |
|---|---|
| [!UICONTROL Sección de encabezado] | Añada un encabezado de sección para ver una lista de componentes comunes. |
| [!UICONTROL Texto de una sola línea] | Agregue una propiedad de texto de una sola línea. Se almacena como una cadena. |
| [!UICONTROL Texto con varios valores] | Agregue una propiedad de texto de varios valores. Se almacena como una matriz de cadenas. |
| [!UICONTROL Número] | Añada un componente numérico. |
| [!UICONTROL Fecha] | Añada un componente de fecha. |
| [!UICONTROL Lista desplegable] | Añada una lista desplegable. |
| [!UICONTROL Etiquetas estándar] | Añadir una etiqueta. |
| [!UICONTROL Campo oculto] | Añada un campo oculto. Se envía como parámetro de POST cuando se guarda el recurso. |

#### Edición de elementos de formulario {#editing-form-items}

Para editar las propiedades de los elementos de formulario, haga clic en el componente y edite todas o un subconjunto de las siguientes propiedades en la pestaña **[!UICONTROL Settings]**.

**[!UICONTROL Etiqueta]** de campo: Nombre de la propiedad de metadatos que se muestra en la página de propiedades de la carpeta.

**[!UICONTROL Asignar a propiedad]**: Esta propiedad especifica la ruta relativa del nodo de carpeta en el repositorio CRX donde se guarda. Comienza con &quot;**./**&quot;, que indica que la ruta está bajo el nodo de la carpeta.

Los siguientes son los valores válidos para esta propiedad:

* `./jcr:content/metadata/dc:title`: Almacena el valor en el nodo de metadatos de la carpeta como propiedad  `dc:title`.

* `./jcr:created`: Muestra la propiedad JCR en el nodo de la carpeta. Si configura estas propiedades en CRXDE, Adobe recomienda marcarlas como Deshabilitar edición, ya que están protegidas. De lo contrario, el error &quot;`Asset(s) failed to modify`&quot; se produce cuando se guardan las propiedades del recurso.

Para asegurarse de que el componente se muestra correctamente en el formulario de esquema de metadatos, no incluya un espacio en la ruta de la propiedad.

**[!UICONTROL Ruta de JSON]**: Utilícelo para especificar la ruta del archivo JSON donde especifique pares clave-valor para las opciones.

**[!UICONTROL Marcador de posición]**: Utilice esta propiedad para especificar el texto del marcador de posición correspondiente a la propiedad metadata.

**[!UICONTROL Opciones]**: Utilice esta propiedad para especificar opciones en una lista.

**[!UICONTROL Descripción]**: Utilice esta propiedad para añadir una breve descripción para el componente de metadatos.

**[!UICONTROL Clase]**: Clase de objeto a la que está asociada la propiedad.

### Eliminación de formularios de esquema de metadatos de carpeta {#delete-folder-metadata-schema-forms}

Puede eliminar formularios de esquema de metadatos de carpeta desde la página Forms Esquema de metadatos de carpeta . Para eliminar un formulario, seleccione el formulario y haga clic en la opción eliminar de la barra de herramientas.

![delete_form](assets/delete_form.png)

### Asignar un esquema de metadatos de carpeta {#assign-a-folder-metadata-schema}

Puede asignar un esquema de metadatos de carpeta a una carpeta desde la página Forms del esquema de metadatos de la carpeta o al crear una carpeta.

Si configura un esquema de metadatos para una carpeta, la ruta al formulario de esquema se almacena en la propiedad `folderMetadataSchema` del nodo de carpeta en `./jcr:content`.

#### Asignar a un esquema desde la página Esquema de metadatos de carpeta {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. En la interfaz [!DNL Experience Manager], vaya a **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Folder Metadata schemas]**.
1. En la página Forms Esquema de metadatos de carpeta , seleccione el formulario de esquema que desee aplicar a una carpeta.
1. En la barra de herramientas, haga clic en **[!UICONTROL Aplicar a las carpetas]**.

1. Seleccione la carpeta en la que desea aplicar el esquema y haga clic en **[!UICONTROL Apply]**. Si ya se ha aplicado un esquema de metadatos en la carpeta, un mensaje de advertencia indicará que está a punto de sobrescribir el esquema de metadatos existente. Haga clic en **[!UICONTROL Sobrescribir]**.
1. Abra las propiedades de metadatos de la carpeta a la que aplicó el esquema de metadatos.

   ![folder_properties](assets/folder_properties.png)

   Para ver los campos de metadatos de la carpeta, haga clic en la pestaña **[!UICONTROL Metadatos de carpeta]**.

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

#### Asignar un esquema al crear una carpeta {#assign-a-schema-when-creating-a-folder}

Puede asignar un esquema de metadatos de carpeta al crear una carpeta. Si existe al menos un esquema de metadatos de carpeta en el sistema, se muestra una lista adicional en el cuadro de diálogo **[!UICONTROL Crear carpeta]**. Puede seleccionar el esquema deseado. De forma predeterminada, no hay ningún esquema seleccionado.

1. En la interfaz de usuario [!DNL Experience Manager Assets], haga clic en **[!UICONTROL Crear]** en la barra de herramientas.
1. Especifique un título y un nombre para la carpeta.
1. En la lista Esquema de metadatos de carpeta , seleccione el esquema deseado. A continuación, haga clic en **[!UICONTROL Crear]**.

   ![select_schema](assets/select_schema.png)

1. Abra las propiedades de metadatos de la carpeta a la que aplicó el esquema de metadatos.
1. Para ver los campos de metadatos de la carpeta, haga clic en la pestaña **[!UICONTROL Metadatos de carpeta]**.

### Usar el esquema de metadatos de la carpeta {#use-the-folder-metadata-schema}

Abra las propiedades de una carpeta configurada con un esquema de metadatos de carpeta. Se muestra la pestaña **[!UICONTROL Metadatos de carpeta]** en la página [!UICONTROL Propiedades] de la carpeta. Para ver el formulario de esquema de metadatos de la carpeta, seleccione esta pestaña.

Introduzca valores de metadatos en los distintos campos y haga clic en **[!UICONTROL Save]** para almacenar los valores. Los valores que especifique se almacenan en el nodo de carpeta del repositorio CRX.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

## Sugerencias y limitaciones {#best-practices-limitations}

* Para importar metadatos en áreas de nombres personalizadas, registre primero las áreas de nombres.
* El Selector de propiedades muestra las propiedades que se utilizan en los editores de esquema y en los formularios de búsqueda. El Selector de propiedades no elige propiedades de metadatos de un recurso.
* Es posible que haya perfiles de metadatos preexistentes desde antes de actualizar a [!DNL Experience Manager] 6.5. Después de la actualización, si aplica dicho perfil en la carpeta [!UICONTROL Properties] de la pestaña [!UICONTROL Metadata Profiles], no se muestran los campos del formulario de metadatos. Sin embargo, si aplica un perfil de metadatos recién creado, los campos del formulario se muestran pero no están disponibles según lo esperado. No se pierde la funcionalidad, pero si desea ver los campos de formulario (no disponibles), edite y guarde los perfiles de metadatos existentes.

>[!MORELIKETHIS]
>
>* [Conceptos y comprensión de metadatos](metadata-concepts.md).
>* [Editar propiedades de metadatos de varias colecciones](manage-collections.md#editing-collection-metadata-in-bulk).
>* [Importación y exportación de metadatos en Recursos de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html).
>* [Perfiles para procesar metadatos, imágenes y vídeos](processing-profiles.md).
>* [Prácticas recomendadas para organizar los recursos digitales para utilizar perfiles](/help/assets/organize-assets.md) de procesamiento.
>* [XMP reescritura](/help/assets/xmp-writeback.md).

