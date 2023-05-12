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

[!DNL Adobe Experience Manager Assets] conserva los metadatos de cada recurso. Permite una categorización y organización más sencillas de los recursos, y ayuda a las personas que buscan un recurso específico. Con la capacidad de mantener y administrar metadatos con los recursos, puede organizar y procesar automáticamente los recursos en función de sus metadatos. [!DNL Adobe Experience Manager Assets] permite a los administradores configurar y personalizar la funcionalidad de metadatos para modificar la oferta de Adobe predeterminada.

## Edición del esquema de metadatos {#metadata-schema}

Para obtener más información, consulte [editar formularios de esquema de metadatos](metadata-schemas.md#edit-metadata-schema-forms).

## Registrar un espacio de nombres personalizado en [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

Puede agregar sus propias áreas de nombres dentro de [!DNL Experience Manager]. Igual que hay áreas de nombres predefinidas como `cq`, `jcr`y `sling`, puede tener un espacio de nombres para los metadatos del repositorio y el procesamiento XML.

1. Acceda a la página de administración del tipo de nodo `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Para acceder a la página de administración del área de nombres, haga clic en **[!UICONTROL Espacios de nombres]** en la parte superior de la página.
1. Para agregar un área de nombres, haga clic en **[!UICONTROL Nuevo]** en la parte inferior de la página.
1. Especifique un área de nombres personalizada en la convención de área de nombres XML. Especifique el ID en forma de URI y un prefijo asociado para el ID. Haga clic en **[!UICONTROL Guardar]**.

## Configuración de límites para la actualización de metadatos masivos {#bulk-metadata-update-limit}

Para evitar una situación similar a la de denegación de servicio (DOS), [!DNL Enterprise Manager] limita el número de parámetros admitidos en una solicitud de Sling. Al actualizar los metadatos de muchos recursos de una sola vez, puede que llegue al límite y los metadatos no se actualicen para obtener más recursos. Enterprise Manager genera la siguiente advertencia en los registros:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

Para cambiar el límite, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]** y cambiar el valor de **[!UICONTROL Máximo de parámetros de POST]** en **[!UICONTROL Administración de parámetros de solicitud de Apache Sling]** Configuración de OSGi.

## Perfiles de metadatos {#metadata-profiles}

Un perfil de metadatos permite aplicar metadatos predeterminados a los recursos de una carpeta. Cree un perfil de metadatos y aplíquelo a una carpeta. Cualquier recurso que cargue posteriormente en la carpeta heredará los metadatos predeterminados que haya configurado en el perfil de metadatos.

### Añadir un perfil de metadatos {#adding-a-metadata-profile}

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Perfiles de metadatos]** y haga clic en **[!UICONTROL Crear]**.
1. Introduzca un título para el perfil, por ejemplo `Sample Metadata`y haga clic en **[!UICONTROL Crear]**. La variable [!UICONTROL Editar formulario] para el perfil de metadatos.

   ![Editar un formulario de metadatos](assets/metadata-edit-form.png)

1. Haga clic en un componente y configure sus propiedades en el **[!UICONTROL Configuración]** pestaña . Por ejemplo, haga clic en el botón **[!UICONTROL Descripción]** y editar sus propiedades.

   ![Configuración de un componente en el perfil de metadatos](assets/metadata-profile-component-setting.png)

   Edite las siguientes propiedades para la variable **[!UICONTROL Descripción]** componente:

   * **[!UICONTROL Etiqueta de campo]**: Nombre para mostrar de la propiedad metadata. Solo es para referencia del usuario.

   * **[!UICONTROL Asignar a propiedad]**: El valor de esta propiedad proporciona la ruta o el nombre relativos al nodo de recurso donde se guarda en el repositorio. El valor siempre debe comenzar con `./` porque indica que la ruta está bajo el nodo del recurso.

   ![Asignar a la configuración de propiedad en el perfil de metadatos](assets/metadata-profile-setting-map-property.png)

   El valor que especifique para **[!UICONTROL Asignar a la propiedad]** se almacena como una propiedad en el nodo de metadatos del recurso. Por ejemplo, si especifica `./jcr:content/metadata/dc:desc` como nombre de **[!UICONTROL Asignar a la propiedad]**, [!DNL Assets] almacena el valor `dc:desc` en el nodo de metadatos del recurso. Adobe recomienda asignar solo un campo a una propiedad determinada del esquema de metadatos. De lo contrario, el sistema selecciona el último campo añadido asignado a la propiedad.

   * **[!UICONTROL Valor predeterminado]**: Utilice esta propiedad para añadir un valor predeterminado para el componente de metadatos. Por ejemplo, si especifica &quot;My description&quot;, este valor se asigna a la propiedad `dc:desc` en el nodo de metadatos del recurso.

   ![Establecer una descripción predeterminada en el perfil de metadatos](assets/metadata-profile-setting-default-value.png)

   >[!NOTE]
   >
   >Añadir un valor predeterminado a una nueva propiedad de metadatos (que no existe en `/jcr:content/metadata` (nodo ) no muestra la propiedad ni su valor en el [!UICONTROL Propiedades] de forma predeterminada. Para ver la nueva propiedad en los recursos [!UICONTROL Propiedades] , modifique el formulario de esquema correspondiente.

1. (Opcional) En la **[!UICONTROL Generar formulario]** , agregue más componentes a [!UICONTROL Editar formulario]y configure sus propiedades en la variable **[!UICONTROL Configuración]** pestaña . Las siguientes propiedades están disponibles en el **[!UICONTROL Generar formulario]** pestaña:

| Componente | Propiedades |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL Encabezado de sección] | Etiqueta de campo, <br> Descripción |
| [!UICONTROL Texto de una sola línea] | Etiqueta de campo, <br> Asignar a la propiedad, <br> Valor predeterminado |
| [!UICONTROL Texto con varios valores] | Etiqueta de campo, <br> Asignar a la propiedad, <br> Valor predeterminado |
| [!UICONTROL Número] | Etiqueta de campo, <br> Asignar a la propiedad, <br> Valor predeterminado |
| [!UICONTROL Fecha] | Etiqueta de campo, <br> Asignar a la propiedad, <br> Valor predeterminado |
| [!UICONTROL Etiquetas estándar] | Etiqueta de campo, <br> Asignar a la propiedad, <br> Valor predeterminado, <br> Descripción |

1. Haga clic en **[!UICONTROL Listo]**. El perfil de metadatos se agrega a la lista de perfiles de la variable **[!UICONTROL Perfiles de metadatos]** página.<br>

   ![Perfil de metadatos añadido en la página Perfiles de metadatos](assets/MetadataProfiles-page.png)

### Copiar un perfil de metadatos {#copying-a-metadata-profile}

1. En el **[!UICONTROL Perfiles de metadatos]** seleccione un perfil de metadatos para realizar una copia de él.

   ![Copiar un perfil de metadatos](assets/metadata-profile-edit-copy-option.png)

1. Haga clic en **[!UICONTROL Copiar]** en la barra de herramientas.
1. En el **[!UICONTROL Copiar perfil de metadatos]** , introduzca un título para la nueva copia del perfil de metadatos.
1. Haga clic en **[!UICONTROL Copiar]**. La copia del perfil de metadatos aparece en la lista de perfiles de la página **[!UICONTROL Perfiles de metadatos]**.

   ![Una copia del perfil de metadatos añadido en la página Perfiles de metadatos](assets/copy-metadata-profile.png)

### Eliminación de un perfil de metadatos {#deleting-a-metadata-profile}

1. En el **[!UICONTROL Perfiles de metadatos]** , seleccione un perfil que desee eliminar.

1. Haga clic en **[!UICONTROL Eliminar perfiles de metadatos]** en la barra de herramientas.
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

[!DNL Adobe Experience Manager Assets] permite crear esquemas de metadatos para carpetas de recursos, que definen el diseño y los metadatos que se muestran en las páginas de propiedades de las carpetas.

### Agregar un formulario de esquema de metadatos de carpeta {#add-a-folder-metadata-schema-form}

Utilice el editor Forms de Esquemas de metadatos de carpeta para crear y editar esquemas de metadatos para carpetas.

1. En [!DNL Experience Manager] interfaz, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Esquemas de metadatos de carpeta]**.
1. En el [!UICONTROL Esquema de metadatos de carpeta Forms] página, haga clic en **[!UICONTROL Crear]**.
1. Especifique un nombre para el formulario y haga clic en **[!UICONTROL Crear]**. El nuevo formulario de esquema aparece en la lista [!UICONTROL Esquema Forms] página.

### Editar formularios de esquema de metadatos de carpeta {#edit-folder-metadata-schema-forms}

Puede editar un formulario de esquema de metadatos nuevo o existente, que incluye lo siguiente:

* Pestañas
* Elementos de formulario dentro de las pestañas.

Puede asignar/configurar estos elementos de formulario a un campo dentro de un nodo de metadatos en el repositorio CRX. Puede agregar nuevas fichas o elementos de formulario al formulario de esquema de metadatos.

1. En la página Esquema de Forms, seleccione el formulario que ha creado y, a continuación, seleccione la **[!UICONTROL Editar]** en la barra de herramientas.
1. En la página Editor de esquemas de metadatos de carpeta , haga clic en `+` para agregar una ficha al formulario. Para cambiar el nombre de la pestaña, haga clic en el nombre predeterminado y especifique el nuevo nombre en **[!UICONTROL Configuración]**.

   ![custom_tab](assets/custom_tab.png)

   Para agregar más pestañas, haga clic en `+`. Para eliminar, haga clic en `X` en una pestaña .

1. En la pestaña activa, añada uno o varios componentes de la **[!UICONTROL Generar formulario]** pestaña .

   ![add_components](assets/adding_components.png)

   Si crea varias fichas, haga clic en una ficha concreta para agregar componentes.

1. Para configurar un componente, selecciónelo y modifique sus propiedades en el **[!UICONTROL Configuración]** pestaña .

   Si es necesario, elimine un componente del **[!UICONTROL Configuración]** pestaña .

   ![configure_properties](assets/configure_properties.png)

1. Para guardar los cambios, seleccione **[!UICONTROL Guardar]** en la barra de herramientas.

#### Componentes para crear formularios {#components-to-build-forms}

La variable **[!UICONTROL Generar formulario]** lista los elementos de formulario que se utilizan en el formulario de esquema de metadatos de la carpeta. La variable **[!UICONTROL Configuración]** muestra los atributos de cada elemento que seleccione en la **[!UICONTROL Generar formulario]** pestaña . Esta es una lista de los elementos de formulario disponibles en la **[!UICONTROL Generar formulario]** pestaña:

| Nombre del componente | Descripción |
|---|---|
| [!UICONTROL Encabezado de sección] | Añada un encabezado de sección para ver una lista de componentes comunes. |
| [!UICONTROL Texto de una sola línea] | Agregue una propiedad de texto de una sola línea. Se almacena como una cadena. |
| [!UICONTROL Texto con varios valores] | Agregue una propiedad de texto de varios valores. Se almacena como una matriz de cadenas. |
| [!UICONTROL Número] | Añada un componente numérico. |
| [!UICONTROL Fecha] | Añada un componente de fecha. |
| [!UICONTROL Lista desplegable] | Añada una lista desplegable. |
| [!UICONTROL Etiquetas estándar] | Añadir una etiqueta. |
| [!UICONTROL Campo oculto] | Añada un campo oculto. Se envía como parámetro de POST cuando se guarda el recurso. |

#### Edición de elementos de formulario {#editing-form-items}

Para editar las propiedades de los elementos de formulario, haga clic en el componente y edite todas o un subconjunto de las siguientes propiedades en la **[!UICONTROL Configuración]** pestaña .

**[!UICONTROL Etiqueta de campo]**: Nombre de la propiedad de metadatos que se muestra en la página de propiedades de la carpeta.

**[!UICONTROL Asignar a propiedad]**: Esta propiedad especifica la ruta relativa del nodo de carpeta en el repositorio CRX donde se guarda. Comienza con &quot;**./**&quot;, que indica que la ruta está bajo el nodo de la carpeta.

Los siguientes son los valores válidos para esta propiedad:

* `./jcr:content/metadata/dc:title`: Almacena el valor en el nodo de metadatos de la carpeta como propiedad `dc:title`.

* `./jcr:created`: Muestra la propiedad JCR en el nodo de la carpeta. Si configura estas propiedades en CRXDE, Adobe recomienda marcarlas como Deshabilitar edición, ya que están protegidas. De lo contrario, el error `Asset(s) failed to modify`&#39; se produce cuando se guardan las propiedades del recurso.

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

Si configura un esquema de metadatos para una carpeta, la ruta al formulario de esquema se almacena en la variable `folderMetadataSchema` propiedad del nodo folder en `./jcr:content`.

#### Asignar a un esquema desde la página Esquema de metadatos de carpeta {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. En [!DNL Experience Manager] interfaz, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Esquemas de metadatos de carpeta]**.
1. En la página Forms Esquema de metadatos de carpeta , seleccione el formulario de esquema que desee aplicar a una carpeta.
1. En la barra de herramientas, haga clic en **[!UICONTROL Aplicar a carpetas]**.

1. Seleccione la carpeta en la que desea aplicar el esquema y haga clic en **[!UICONTROL Aplicar]**. Si ya se ha aplicado un esquema de metadatos en la carpeta, un mensaje de advertencia indicará que está a punto de sobrescribir el esquema de metadatos existente. Haga clic en **[!UICONTROL Sobrescribir]**.
1. Abra las propiedades de metadatos de la carpeta a la que aplicó el esquema de metadatos.

   ![folder_properties](assets/folder_properties.png)

   Para ver los campos de metadatos de la carpeta, haga clic en el botón **[!UICONTROL Metadatos de carpeta]** pestaña .

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

#### Asignar un esquema al crear una carpeta {#assign-a-schema-when-creating-a-folder}

Puede asignar un esquema de metadatos de carpeta al crear una carpeta. Si existe al menos un esquema de metadatos de carpeta en el sistema, se muestra una lista adicional en la **[!UICONTROL Crear carpeta]** diálogo. Puede seleccionar el esquema deseado. De forma predeterminada, no hay ningún esquema seleccionado.

1. En el [!DNL Experience Manager Assets] interfaz de usuario, haga clic en **[!UICONTROL Crear]** en la barra de herramientas.
1. Especifique un título y un nombre para la carpeta.
1. En la lista Esquema de metadatos de carpeta , seleccione el esquema deseado. A continuación, haga clic en **[!UICONTROL Crear]**.

   ![select_schema](assets/select_schema.png)

1. Abra las propiedades de metadatos de la carpeta a la que aplicó el esquema de metadatos.
1. Para ver los campos de metadatos de la carpeta, haga clic en el botón **[!UICONTROL Metadatos de carpeta]** pestaña .

### Usar el esquema de metadatos de la carpeta {#use-the-folder-metadata-schema}

Abra las propiedades de una carpeta configurada con un esquema de metadatos de carpeta. A **[!UICONTROL Metadatos de carpeta]** se muestra en la carpeta [!UICONTROL Propiedades] página. Para ver el formulario de esquema de metadatos de la carpeta, seleccione esta pestaña.

Introduzca valores de metadatos en los distintos campos y haga clic en **[!UICONTROL Guardar]** para almacenar los valores. Los valores que especifique se almacenan en el nodo de carpeta del repositorio CRX.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

## Sugerencias y limitaciones {#best-practices-limitations}

* Para importar metadatos en áreas de nombres personalizadas, registre primero las áreas de nombres.
* El Selector de propiedades muestra las propiedades que se utilizan en los editores de esquema y en los formularios de búsqueda. El Selector de propiedades no elige propiedades de metadatos de un recurso.
* Es posible que ya tenga perfiles de metadatos preexistentes desde antes de actualizar a [!DNL Experience Manager] 6.5. Después de la actualización, si aplica dicho perfil en la carpeta [!UICONTROL Propiedades] en [!UICONTROL Perfiles de metadatos] , los campos de formulario de metadatos no se muestran. Sin embargo, si aplica un perfil de metadatos recién creado, los campos del formulario se muestran pero no están disponibles según lo esperado. No se pierde la funcionalidad, pero si desea ver los campos de formulario (no disponibles), edite y guarde los perfiles de metadatos existentes.

>[!MORELIKETHIS]
>
>* [Conceptos y comprensión de metadatos](metadata-concepts.md).
>* [Editar propiedades de metadatos de varias colecciones](manage-collections.md#editing-collection-metadata-in-bulk).
>* [Importación y exportación de metadatos en Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-export.html).
>* [Perfiles para procesar metadatos, imágenes y vídeos](processing-profiles.md).
>* [Prácticas recomendadas para organizar los recursos digitales para utilizar perfiles de procesamiento](/help/assets/organize-assets.md).
>* [XMP reescritura](/help/assets/xmp-writeback.md).

