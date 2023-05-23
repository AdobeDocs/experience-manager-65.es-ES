---
title: Configuración y administración de la funcionalidad de metadatos.
description: Configuración y administración de [!DNL Experience Manager Assets] funcionalidad relacionada con la adición y administración de metadatos.
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 56c92b7f-e687-4ab5-a376-afa58bdb6ee0
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '2000'
ht-degree: 4%

---

# Configuración y administración de la funcionalidad de metadatos en [!DNL Assets] {#config-metadata}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/metadata-profiles.html?lang=en) |
| AEM 6.5 | Este artículo |

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] mantiene los metadatos de cada recurso. Permite una categorización y organización más sencillas de los recursos y ayuda a las personas que buscan un recurso específico. Con la capacidad de mantener y administrar metadatos con sus recursos, puede organizar y procesar recursos automáticamente en función de sus metadatos. [!DNL Adobe Experience Manager Assets] permite a los administradores configurar y personalizar la funcionalidad de metadatos para modificar la oferta de Adobe predeterminada.

## Editar esquema de metadatos {#metadata-schema}

Para obtener más información, consulte [editar formularios de esquema de metadatos](metadata-schemas.md#edit-metadata-schema-forms).

## Registrar un área de nombres personalizada en [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

Puede agregar sus propias áreas de nombres en [!DNL Experience Manager]. Al igual que hay áreas de nombres predefinidas como `cq`, `jcr`, y `sling`, puede tener un área de nombres para los metadatos del repositorio y el procesamiento XML.

1. Acceso a la página de administración de tipo de nodo `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Para acceder a la página de administración del área de nombres, haga clic en **[!UICONTROL Áreas de nombres]** en la parte superior de la página.
1. Para añadir un área de nombres, haga clic en **[!UICONTROL Nuevo]** en la parte inferior de la página.
1. Especifique un espacio de nombres personalizado en la convención del espacio de nombres XML. Especifique el ID en forma de URI y un prefijo asociado para el ID. Haga clic en **[!UICONTROL Guardar]**.

## Configuración de límites para la actualización masiva de metadatos {#bulk-metadata-update-limit}

Para evitar una situación de denegación de servicio (DOS), [!DNL Enterprise Manager] limita el número de parámetros admitidos en una solicitud de Sling. Al actualizar los metadatos de muchos recursos de una sola vez, es posible que alcance el límite y los metadatos no se actualicen para más recursos. Enterprise Manager genera la siguiente advertencia en los registros:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

Para cambiar el límite, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]** y cambie el valor de **[!UICONTROL Parámetros máximos del POST]** in **[!UICONTROL Administración de parámetros de solicitud de Apache Sling]** Configuración de OSGi.

## Perfiles de metadatos {#metadata-profiles}

Un perfil de metadatos le permite aplicar metadatos predeterminados a los recursos de una carpeta. Cree un perfil de metadatos y aplíquelo a una carpeta. Cualquier recurso que cargue posteriormente en la carpeta hereda los metadatos predeterminados configurados en el perfil de metadatos.

### Añadir un perfil de metadatos {#adding-a-metadata-profile}

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de metadatos]** y haga clic en **[!UICONTROL Crear]**.
1. Introduzca un título para el perfil, por ejemplo `Sample Metadata`y haga clic en **[!UICONTROL Crear]**. El [!UICONTROL Editar formulario] para el perfil de metadatos.

   ![Edición de un formulario de metadatos](assets/metadata-edit-form.png)

1. Haga clic en un componente y configure sus propiedades en la **[!UICONTROL Configuración]** pestaña. Por ejemplo, haga clic en **[!UICONTROL Descripción]** y editar sus propiedades.

   ![Configuración de un componente en el perfil de metadatos](assets/metadata-profile-component-setting.png)

   Edite las siguientes propiedades para **[!UICONTROL Descripción]** componente:

   * **[!UICONTROL Etiqueta de campo]**: nombre para mostrar de la propiedad de metadatos. Solo es para la referencia del usuario.

   * **[!UICONTROL Asignar a la propiedad]**: el valor de esta propiedad proporciona la ruta relativa o el nombre al nodo del recurso donde se guarda en el repositorio. El valor siempre debe comenzar con `./` porque indica que la ruta se encuentra en el nodo del recurso.

   ![Asignar a la configuración de la propiedad en el perfil de metadatos](assets/metadata-profile-setting-map-property.png)

   El valor que especifique para **[!UICONTROL Asignar a la propiedad]** se almacena como una propiedad en el nodo de metadatos del recurso. Por ejemplo, si especifica `./jcr:content/metadata/dc:desc` como el nombre de **[!UICONTROL Asignar a la propiedad]**, [!DNL Assets] almacena el valor `dc:desc` en el nodo de metadatos del recurso. El Adobe recomienda asignar solo un campo a una propiedad determinada en el esquema de metadatos. De lo contrario, el sistema selecciona el último campo añadido asignado a la propiedad.

   * **[!UICONTROL Valor predeterminado]**: utilice esta propiedad para agregar un valor predeterminado para el componente de metadatos. Por ejemplo, si especifica &quot;Mi descripción&quot;, este valor se asigna a la propiedad `dc:desc` en el nodo de metadatos del recurso.

   ![Definir descripción predeterminada en el perfil de metadatos](assets/metadata-profile-setting-default-value.png)

   >[!NOTE]
   >
   >Añadir un valor predeterminado a una nueva propiedad de metadatos (que no existe en `/jcr:content/metadata` ) no muestra la propiedad ni su valor en el [!UICONTROL Propiedades] de forma predeterminada. Para ver la nueva propiedad en los recursos de [!UICONTROL Propiedades] , modifique el formulario de esquema correspondiente.

1. (Opcional) En el **[!UICONTROL Generar formulario]** pestaña, añadir más componentes a [!UICONTROL Editar formulario]y configure sus propiedades en la variable **[!UICONTROL Configuración]** pestaña. Las siguientes propiedades están disponibles en el **[!UICONTROL Generar formulario]** pestaña:

| Componente | Propiedades |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL Encabezado de sección] | Etiqueta de campo, <br> Descripción |
| [!UICONTROL Texto de una sola línea] | Etiqueta de campo, <br> Asignar a la propiedad, <br> Valor predeterminado |
| [!UICONTROL Texto con varios valores] | Etiqueta de campo, <br> Asignar a la propiedad, <br> Valor predeterminado |
| [!UICONTROL Número] | Etiqueta de campo, <br> Asignar a la propiedad, <br> Valor predeterminado |
| [!UICONTROL Fecha] | Etiqueta de campo, <br> Asignar a la propiedad, <br> Valor predeterminado |
| [!UICONTROL Etiquetas estándar] | Etiqueta de campo, <br> Asignar a la propiedad, <br> Valor predeterminado, <br> Descripción |

1. Haga clic en **[!UICONTROL Listo]**. El perfil de metadatos se añade a la lista de perfiles del **[!UICONTROL Perfiles de metadatos]** página.<br>

   ![Perfil de metadatos añadido en la página Perfiles de metadatos](assets/MetadataProfiles-page.png)

### Copiar un perfil de metadatos {#copying-a-metadata-profile}

1. Desde el **[!UICONTROL Perfiles de metadatos]** , seleccione un perfil de metadatos para hacer una copia del mismo.

   ![Copiar un perfil de metadatos](assets/metadata-profile-edit-copy-option.png)

1. Clic **[!UICONTROL Copiar]** en la barra de herramientas.
1. En el **[!UICONTROL Copiar perfil de metadatos]** , introduzca un título para la nueva copia del perfil de metadatos.
1. Clic **[!UICONTROL Copiar]**. La copia del perfil de metadatos aparece en la lista de perfiles de la página **[!UICONTROL Perfiles de metadatos]**.

   ![Se ha agregado una copia del perfil de metadatos en la página Perfiles de metadatos](assets/copy-metadata-profile.png)

### Eliminación de un perfil de metadatos {#deleting-a-metadata-profile}

1. Desde el **[!UICONTROL Perfiles de metadatos]** , seleccione un perfil para eliminar.

1. Clic **[!UICONTROL Eliminar perfiles de metadatos]** en la barra de herramientas.
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

[!DNL Adobe Experience Manager Assets] permite crear esquemas de metadatos para carpetas de recursos, que definen el diseño y los metadatos mostrados en las páginas de propiedades de la carpeta.

### Agregar un formulario de esquema de metadatos de carpeta {#add-a-folder-metadata-schema-form}

Utilice el editor de Forms del Esquema de metadatos de carpeta para crear y editar esquemas de metadatos para carpetas.

1. Entrada [!DNL Experience Manager] interfaz, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadatos de carpeta]**.
1. En el [!UICONTROL Forms de esquema de metadatos de carpeta] página, haga clic en **[!UICONTROL Crear]**.
1. Especifique un nombre para el formulario y haga clic en **[!UICONTROL Crear]**. El nuevo formulario de esquema se enumera en la [!UICONTROL Esquema Forms] página.

### Editar formularios de esquema de metadatos de carpeta {#edit-folder-metadata-schema-forms}

Puede editar un formulario de esquema de metadatos recién agregado o existente, que incluya lo siguiente:

* Pestañas
* Elementos de formulario dentro de pestañas.

Puede asignar o configurar estos elementos de formulario a un campo dentro de un nodo de metadatos en el repositorio CRX. Puede agregar nuevas pestañas o elementos de formulario al formulario de esquema de metadatos.

1. En la página Schema Forms, seleccione el formulario que ha creado y, a continuación, seleccione la opción **[!UICONTROL Editar]** de la barra de herramientas.
1. En la página Editor de esquemas de metadatos de carpeta, haga clic en `+` para agregar una pestaña al formulario. Para cambiar el nombre de la pestaña, haga clic en el nombre predeterminado y especifique el nuevo nombre en **[!UICONTROL Configuración]**.

   ![custom_tab](assets/custom_tab.png)

   Para agregar más pestañas, haga clic en `+`. Para eliminar, haga clic en `X` en una pestaña.

1. En la pestaña activa, añada uno o más componentes del **[!UICONTROL Generar formulario]** pestaña.

   ![adding_components](assets/adding_components.png)

   Si crea varias pestañas, haga clic en una pestaña concreta para añadir componentes.

1. Para configurar un componente, selecciónelo y modifique sus propiedades en la **[!UICONTROL Configuración]** pestaña.

   Si es necesario, elimine un componente del **[!UICONTROL Configuración]** pestaña.

   ![configure_properties](assets/configure_properties.png)

1. Para guardar los cambios, seleccione **[!UICONTROL Guardar]** en la barra de herramientas.

#### Componentes para crear formularios {#components-to-build-forms}

El **[!UICONTROL Generar formulario]** La pestaña enumera los elementos de formulario que utiliza en el formulario de esquema de metadatos de la carpeta. El **[!UICONTROL Configuración]** pestaña muestra los atributos de cada elemento seleccionado en la **[!UICONTROL Generar formulario]** pestaña. Esta es una lista de los elementos de formulario disponibles en la **[!UICONTROL Generar formulario]** pestaña:

| Nombre del componente | Descripción |
|---|---|
| [!UICONTROL Encabezado de sección] | Añada un encabezado de sección para una lista de componentes comunes. |
| [!UICONTROL Texto de una sola línea] | Agregue una propiedad de texto de una sola línea. Se almacena como una cadena. |
| [!UICONTROL Texto con varios valores] | Agregue una propiedad de texto de varios valores. Se almacena como una matriz de cadenas. |
| [!UICONTROL Número] | Añada un componente numérico. |
| [!UICONTROL Fecha] | Añada un componente de fecha. |
| [!UICONTROL Lista desplegable] | Añada una lista desplegable. |
| [!UICONTROL Etiquetas estándar] | Añadir una etiqueta. |
| [!UICONTROL Campo oculto] | Agregue un campo oculto. Se envía como parámetro de POST cuando se guarda el recurso. |

#### Edición de elementos de formulario {#editing-form-items}

Para editar las propiedades de los elementos del formulario, haga clic en el componente y edite todas o un subconjunto de las siguientes propiedades en la **[!UICONTROL Configuración]** pestaña.

**[!UICONTROL Etiqueta de campo]**: Nombre de la propiedad de metadatos que se muestra en la página de propiedades de la carpeta.

**[!UICONTROL Asignar a la propiedad]**: Esta propiedad especifica la ruta relativa del nodo de carpeta en el repositorio CRX donde se guarda. Comienza con &quot;**./**&quot;, que indica que la ruta se encuentra bajo el nodo de la carpeta.

Los siguientes son los valores válidos para esta propiedad:

* `./jcr:content/metadata/dc:title`: Almacena el valor en el nodo de metadatos de la carpeta como propiedad `dc:title`.

* `./jcr:created`: Muestra la propiedad JCR en el nodo de la carpeta. Si configura estas propiedades en CRXDE, Adobe recomienda marcarlas como Deshabilitar edición, ya que están protegidas. De lo contrario, el error &#39; `Asset(s) failed to modify`&#39; se produce al guardar las propiedades del recurso.

Para asegurarse de que el componente se muestra correctamente en el formulario de esquema de metadatos, no incluya un espacio en la ruta de la propiedad.

**[!UICONTROL Ruta de JSON]**: utilícelo para especificar la ruta del archivo JSON donde debe especificar los pares clave-valor para las opciones.

**[!UICONTROL Marcador]**: utilice esta propiedad para especificar el texto de marcador de posición correspondiente a la propiedad de metadatos.

**[!UICONTROL Opciones]**: utilice esta propiedad para especificar opciones en una lista.

**[!UICONTROL Descripción]**: utilice esta propiedad para agregar una descripción breve para el componente de metadatos.

**[!UICONTROL Clase]**: clase de objeto a la que está asociada la propiedad.

### Eliminar formularios de esquema de metadatos de carpeta {#delete-folder-metadata-schema-forms}

Puede eliminar formularios de esquema de metadatos de carpeta desde la página de Forms Esquema de metadatos de carpeta. Para eliminar un formulario, selecciónelo y haga clic en la opción Eliminar de la barra de herramientas.

![delete_form](assets/delete_form.png)

### Asignar un esquema de metadatos de carpeta {#assign-a-folder-metadata-schema}

Puede asignar un esquema de metadatos de carpeta a una carpeta desde la página de Forms Esquema de metadatos de carpeta o al crear una carpeta.

Si configura un esquema de metadatos para una carpeta, la ruta al formulario de esquema se almacena en la variable `folderMetadataSchema` propiedad del nodo de carpeta en `./jcr:content`.

#### Asignar a un esquema desde la página Esquema de metadatos de carpeta {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. Entrada [!DNL Experience Manager] interfaz, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadatos de carpeta]**.
1. En la página Forms del esquema de metadatos de carpeta, seleccione el formulario de esquema que desee aplicar a una carpeta.
1. En la barra de herramientas, haga clic en **[!UICONTROL Aplicar a las carpetas]**.

1. Seleccione la carpeta en la que desea aplicar el esquema y haga clic en **[!UICONTROL Aplicar]**. Si ya se ha aplicado un esquema de metadatos en la carpeta, un mensaje de advertencia le informa de que está a punto de sobrescribir el esquema de metadatos existente. Clic **[!UICONTROL Sobrescribir]**.
1. Abra las propiedades de metadatos de la carpeta a la que aplicó el esquema de metadatos.

   ![folder_properties](assets/folder_properties.png)

   Para ver los campos de metadatos de la carpeta, haga clic en **[!UICONTROL Metadatos de carpeta]** pestaña.

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

#### Asignar un esquema al crear una carpeta {#assign-a-schema-when-creating-a-folder}

Puede asignar un esquema de metadatos de carpeta al crear una carpeta. Si existe al menos un esquema de metadatos de carpeta en el sistema, se muestra una lista adicional en la variable **[!UICONTROL Crear carpeta]** diálogo. Puede seleccionar el esquema deseado. De forma predeterminada, no se selecciona ningún esquema.

1. Desde el [!DNL Experience Manager Assets] interfaz de usuario, haga clic en **[!UICONTROL Crear]** en la barra de herramientas.
1. Especifique un título y un nombre para la carpeta.
1. En la lista Esquema de metadatos de carpeta, seleccione el esquema deseado. A continuación, haga clic en **[!UICONTROL Crear]**.

   ![select_schema](assets/select_schema.png)

1. Abra las propiedades de metadatos de la carpeta a la que aplicó el esquema de metadatos.
1. Para ver los campos de metadatos de la carpeta, haga clic en **[!UICONTROL Metadatos de carpeta]** pestaña.

### Usar el esquema de metadatos de carpeta {#use-the-folder-metadata-schema}

Abra las propiedades de una carpeta configurada con un esquema de metadatos de carpeta. A **[!UICONTROL Metadatos de carpeta]** La pestaña se muestra en la carpeta [!UICONTROL Propiedades] página. Para ver el formulario de esquema de metadatos de la carpeta, seleccione esta pestaña.

Introduzca valores de metadatos en los distintos campos y haga clic en **[!UICONTROL Guardar]** para almacenar los valores. Los valores especificados se almacenan en el nodo de carpeta del repositorio CRX.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

## Sugerencias y limitaciones {#best-practices-limitations}

* Para importar metadatos en áreas de nombres personalizadas, primero registre las áreas de nombres.
* El Selector de propiedades muestra las propiedades que se utilizan en los editores de esquemas y formularios de búsqueda. El Selector de propiedades no elige propiedades de metadatos de un recurso.
* Es posible que tenga perfiles de metadatos preexistentes desde antes de actualizar a [!DNL Experience Manager] 6.5. Después de la actualización, si aplica ese perfil en la carpeta [!UICONTROL Propiedades] in [!UICONTROL Perfiles de metadatos] pestaña, no se muestran los campos del formulario de metadatos. Sin embargo, si aplica un perfil de metadatos recién creado, los campos de formulario se muestran pero no están disponibles según lo esperado. No se pierde la funcionalidad, pero si desea ver los campos de formulario (no disponibles), edite y guarde los perfiles de metadatos existentes.

>[!MORELIKETHIS]
>
>* [Conceptos de metadatos y comprensión](metadata-concepts.md).
>* [Editar propiedades de metadatos de varias colecciones](manage-collections.md#editing-collection-metadata-in-bulk).
>* [Importación y exportación de metadatos en Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-export.html).
>* [Perfiles para procesar metadatos, imágenes y vídeos](processing-profiles.md).
>* [Prácticas recomendadas para organizar los recursos digitales a fin de que utilicen perfiles de procesamiento](/help/assets/organize-assets.md).
>* [XMP respuesta de escritura de la](/help/assets/xmp-writeback.md).

