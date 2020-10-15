---
title: Administre los metadatos de sus recursos digitales en [!DNL Adobe Experience Manager].
description: Obtenga información sobre los tipos de metadatos y [!DNL Adobe Experience Manager Assets] helps manage metadata for assets to allow easier categorization and organization of assets. [!DNL Experience Manager] cómo pueden organizarse y procesarse automáticamente los recursos en función de sus metadatos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b14b377e52ab10c41355f069d97508b588d82216
workflow-type: tm+mt
source-wordcount: '2423'
ht-degree: 11%

---


# Gestión de metadatos de los recursos digitales {#managing-metadata-for-digital-assets}

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] guarda los metadatos de cada recurso. Permite una clasificación y organización más sencillas de los recursos y ayuda a las personas que buscan un recurso específico. Con la capacidad de extraer metadatos de los archivos cargados en [!DNL Experience Manager Assets], la administración de metadatos se integra con el flujo de trabajo creativo. Con la capacidad de mantener y administrar metadatos con sus recursos, puede organizar y procesar automáticamente recursos en función de sus metadatos.

## Metadatos y su origen {#how-to-edit-or-add-metadata}

Los metadatos son información adicional sobre el recurso que se puede buscar. Se agrega a los recursos y [!DNL Experience Manager] se procesa al cargarlos. Puede editar los metadatos existentes y agregar nuevas propiedades de metadatos a los campos existentes. Las organizaciones necesitan vocabularios de metadatos fiables y controlados. Por lo tanto, [!DNL Experience Manager Assets] no permite la adición a petición de nuevas propiedades de metadatos. Solo los administradores y desarrolladores pueden agregar nuevas propiedades o campos que contengan metadatos. Los usuarios pueden rellenar los campos existentes con metadatos.

Se pueden utilizar los siguientes métodos para agregar metadatos a recursos digitales:

* Para empezar, las aplicaciones nativas que crean recursos le agregan algunos metadatos. Por ejemplo, [Acrobat agrega algunos metadatos](https://helpx.adobe.com/acrobat/using/pdf-properties-metadata.html) a los archivos PDF o una cámara agrega algunos metadatos básicos a las fotografías. Al generar recursos, puede agregar los metadatos en las propias aplicaciones nativas. Por ejemplo, puede [agregar metadatos IPTC en Adobe Lightroom](https://helpx.adobe.com/lightroom-classic/help/metadata-basics-actions.html).

* Antes de cargar un recurso en [!DNL Experience Manager], puede editar y modificar los metadatos con la aplicación nativa utilizada para crear un recurso o con otra aplicación de edición de metadatos. Al cargar un recurso en el Experience Manager, se procesan los metadatos. Por ejemplo, consulte cómo [trabajar con metadatos en [!DNL Adobe Bridge]](https://helpx.adobe.com/bridge/user-guide.html/bridge/using/metadata-adobe-bridge.ug.html) y ver el panel [de etiquetas para [!DNL Bridge CC]](https://exchange.adobe.com/creativecloud.details.20009.aem-tags-panel-for-bridge-cc.html) en [!DNL Adobe Exchange].

* En [!DNL Experience Manager Assets], puede agregar o editar manualmente los metadatos de los recursos en la página [!UICONTROL Propiedades] .

* Puede aprovechar la funcionalidad [de perfiles](/help/assets/metadata-config.md#metadata-profiles) de metadatos de [!DNL Experience Manager Assets] para agregar metadatos automáticamente cuando los recursos se carguen en DAM.

## Añadir o editar metadatos en [!DNL Experience Manager Assets] {#add-edit-metadata}

Para editar los metadatos de un recurso en la interfaz de [!DNL Assets] usuario, siga estos pasos:

1. Realice una de las acciones siguientes:

   * En la [!DNL Assets] interfaz, seleccione el recurso y haga clic en Propiedades **[!UICONTROL de la]** Vista en la barra de herramientas.
   * En la miniatura del recurso, seleccione la acción rápida Propiedades de la **[!UICONTROL Vista]** .
   * En la página de recursos, haga clic en el icono **[!UICONTROL de información Propiedades]** de ![Vista de](assets/do-not-localize/info-circle-icon.png) recursos de la barra de herramientas.

   La página de recursos muestra todos los metadatos del recurso. Los metadatos se extraen cuando se carga el recurso (se ingesta) en [!DNL Experience Manager].

   ![Seleccionar propiedades de un recurso para vista de sus metadatos](assets/asset-metadata.png)

   *Figura: Edite o agregue metadatos en la página [!UICONTROL Propiedades] del recurso.*

1. Make edits to the metadata under the various tabs, as required, and when completed, click **[!UICONTROL Save]** from the toolbar to save your changes. Click **[!UICONTROL Close]** to return to the [!DNL Assets] web interface.

   >[!NOTE]
   >
   >Si un campo de texto está vacío, no hay ningún conjunto de metadatos existente. Puede introducir un valor en el campo y guardarlo para agregar esa propiedad de metadatos.

Cualquier cambio en los metadatos de un recurso se vuelve a escribir en el binario original como parte de sus datos XMP. El flujo de trabajo de escritura de metadatos agrega los metadatos al binario original. Los cambios realizados en las propiedades existentes (como `dc:title`) se sobrescriben y las propiedades nuevas (incluidas las propiedades personalizadas como `cq:tags`) se agregan con el esquema.

Se admite y activa la XMP de la escritura en pantalla para las plataformas y los formatos de archivo descritos en los requisitos [técnicos.](/help/sites-deploying/technical-requirements.md)

## Editar propiedades de metadatos de varios recursos {#editing-metadata-properties-of-multiple-assets}

[!DNL Adobe Enterprise Manager Assets] le permite editar los metadatos de varios recursos de forma simultánea para poder propagar rápidamente cambios comunes de metadatos a los recursos de forma masiva. También puede editar los metadatos de varias colecciones de forma masiva. Utilice la página de propiedades para realizar cambios en los metadatos de varios recursos o colecciones:

* Cambiar las propiedades de metadatos a un valor común
* Añadir o modificar etiquetas

Para personalizar la página de propiedades de metadatos, incluida la adición, modificación y eliminación de propiedades de metadatos, utilice el editor de [esquema](metadata-config.md#folder-metadata-schema).

>[!NOTE]
>
>Los métodos de edición masiva funcionan para los recursos disponibles en una carpeta o una colección. En el caso de los recursos disponibles en varias carpetas o que cumplen un criterio común, es posible actualizar [masivamente los metadatos después de realizar la búsqueda](search-assets.md#metadataupdates).

1. En la interfaz de usuario, navegue hasta la ubicación de los recursos que desee editar. [!DNL Assets]
1. Seleccione los recursos para los que desea editar propiedades comunes.
1. En la barra de herramientas, haga clic en **[!UICONTROL Propiedades]** para abrir la página de propiedades de los recursos seleccionados.

   >[!NOTE]
   >
   >Cuando se seleccionan varios recursos, se selecciona el formulario principal común más bajo para los recursos. En otras palabras, la página de propiedades solo muestra los campos de metadatos comunes en las páginas de propiedades de todos los recursos individuales.

1. Modifique las propiedades de metadatos de los recursos seleccionados en las distintas fichas.
1. Para vista del editor de metadatos de un recurso específico, anule la selección de los recursos restantes de la lista. Los campos del editor de metadatos se rellenan con los metadatos del recurso concreto.

   >[!NOTE]
   >
   >* En la página de propiedades, puede quitar recursos de la lista de recursos anulándolos. La lista de recursos tiene todos los recursos seleccionados de forma predeterminada. Los metadatos de los recursos que se eliminan de la lista no se actualizan.
   >* En la parte superior de la lista de recursos, active la casilla de verificación situada junto a **[!UICONTROL Título]** para alternar entre seleccionar los recursos y borrar la lista.


1. Para seleccionar otro esquema de metadatos para los recursos, haga clic en **[!UICONTROL Configuración]** en la barra de herramientas y seleccione el esquema que desee.
1. Guarde los cambios.
1. Para anexar los nuevos metadatos con los metadatos existentes en los campos que contienen varios valores, seleccione el **[!UICONTROL modo Anexar]**. Si no selecciona esta opción, los metadatos nuevos sustituirán a los metadatos existentes en los campos. Haga clic en **[!UICONTROL Enviar]**.

   >[!CAUTION]
   >
   >En el caso de los campos de un solo valor, los nuevos metadatos no se anexan al valor existente en el campo aunque seleccione el modo **[!UICONTROL Anexar]**.

## Importación de metadatos {#import-metadata}

[!DNL Assets] permite importar metadatos de recursos de forma masiva mediante un archivo CSV. Puede realizar actualizaciones masivas para los recursos cargados recientemente o los recursos existentes mediante la importación de un archivo CSV. También puede ingerir metadatos de recursos de forma masiva desde sistemas de terceros en formato CSV.

La importación de metadatos es asincrónica y no impide el rendimiento del sistema. La actualización simultánea de los metadatos de varios recursos puede requerir muchos recursos debido a XMP actividad de reescritura si se marca el indicador de flujo de trabajo. Planifique una importación de este tipo durante el uso del servidor liso para que el rendimiento de otros usuarios no se vea afectado.

>[!NOTE]
>
>Para importar metadatos en Áreas de nombres personalizadas, primero registre las Áreas de nombres.

1. Vaya a la interfaz de usuario y haga clic en [!DNL Assets] Crear **** en la barra de herramientas.
1. En el menú, seleccione **[!UICONTROL Metadatos]**.
1. In the **[!UICONTROL Metadata Import]** page, click **[!UICONTROL Select File]**. Seleccione el archivo CSV con los metadatos.
1. Especifique los siguientes parámetros. Consulte un archivo CSV de muestra en [metadata-import-sample-file.csv](assets/metadata-import-sample-file.csv).

   | Parámetros de importación de metadatos | Descripción |
   |:---|:---|
   | [!UICONTROL Tamaño del lote] | Número de recursos de un lote para el que se van a importar metadatos. El valor predeterminado es 50. El valor máximo es 100. |
   | [!UICONTROL Separador de campos] | El valor predeterminado es `,` (coma). Puede especificar cualquier otro carácter. |
   | [!UICONTROL Delimitador de varios valores] | Separador para valores de metadatos. El valor predeterminado es `|`. |
   | [!UICONTROL Lanzar flujos de trabajo] | False de forma predeterminada. Cuando se establece en `true` y la configuración predeterminada del iniciador está en vigor para el flujo de trabajo WriteBack [!UICONTROL de metadatos] DAM (que escribe metadatos en los datos de XMP binarios). Al habilitar los flujos de trabajo de inicio se ralentiza el sistema. |
   | [!UICONTROL Nombre de columna de ruta de activos] | Define el nombre de la columna para el archivo CSV con recursos. |

1. Click **[!UICONTROL Import]** from the toolbar. Una vez importados los metadatos, se muestra una notificación en la bandeja de entrada [!UICONTROL Notificación] .

1. Para verificar la importación correcta, vaya a la página [!UICONTROL Propiedades] de un recurso y compruebe los valores de los campos.

Para agregar la fecha y la marca de hora al importar metadatos, utilice `YYYY-MM-DDThh:mm:ss.fff-00:00` el formato de fecha y hora. La fecha y la hora se separan por `T`, `hh` es hora en formato de 24 horas, `fff` es nanosegundos y `-00:00` es desplazamiento de zona horaria. Por ejemplo, `2020-03-26T11:26:00.000-07:00` es 26 de marzo de 2020 a las 11:26:00.000 AM hora PST.

>[!CAUTION]
>
>Si el formato de fecha no coincide `YYYY-MM-DDThh:mm:ss.fff-00:00`, no se establecen los valores de fecha. Los formatos de fecha del archivo CSV de metadatos exportado tienen el formato `YYYY-MM-DDThh:mm:ss-00:00`. Si desea importarla, conviértala al formato aceptable agregando el valor de nanosegundos indicado por `fff`.

## Export metadata {#export-metadata}

Puede exportar metadatos de varios recursos en formato CSV. Los metadatos se exportan asincrónicamente y no afectan al rendimiento del sistema. Para exportar metadatos, [!DNL Experience Manager] recorre las propiedades del nodo de recursos `jcr:content/metadata` y sus nodos secundarios y exporta las propiedades de metadatos en un archivo CSV.

Algunos casos de uso para exportar metadatos de forma masiva son:

* Importe los metadatos en un sistema de terceros al migrar recursos.
* Comparta metadatos de recursos con un equipo de proyecto más amplio.
* Probar o auditar los metadatos para comprobar la conformidad.
* Externalice los metadatos para localizarlos por separado.

1. Seleccione la carpeta de recursos que contiene los recursos para los que desea exportar metadatos. En la barra de herramientas, seleccione **[!UICONTROL Exportar metadatos]**.

1. En el cuadro de diálogo Exportar  metadatos, especifique un nombre para el archivo CSV. Para exportar metadatos de recursos en subcarpetas, seleccione **[!UICONTROL Incluir recursos en subcarpetas]**.

   ![Interfaz y opciones para exportar metadatos de todos los recursos de una](assets/export_metadata_page.png "carpetaInterfaz y opciones para exportar metadatos de todos los recursos de una carpeta")

1. Seleccione las opciones que desee. Proporcione un nombre de archivo y, si es necesario, una fecha.

1. En el campo **[!UICONTROL Propiedades que exportar]** , especifique si desea exportar todas las propiedades o determinadas. Si selecciona Propiedades selectivas para exportar, agregue las propiedades que desee.

1. En la barra de herramientas, haga clic en **[!UICONTROL Exportar]**. Un mensaje confirma que se exportan los metadatos. Cierre el mensaje.

1. Abra la notificación de la bandeja de entrada para el trabajo de exportación. Seleccione el trabajo y haga clic en **[!UICONTROL Abrir]** en la barra de herramientas. To download the CSV file with the metadata, click **[!UICONTROL CSV Download]** from the toolbar. Haga clic en **[!UICONTROL Cerrar]**.

   ![Cuadro de diálogo para descargar el archivo CSV que contiene metadatos exportados de forma masiva](assets/csv_download.png)

   *Figura: Cuadro de diálogo para descargar el archivo CSV que contiene metadatos exportados de forma masiva.*

## Editar metadatos de colecciones {#collections-metadata}

Para obtener más información, consulte [vista y edición de metadatos](/help/assets/managing-collections-touch-ui.md#view-edit-collection-metadata) de la colección y [edición masiva](/help/assets/managing-collections-touch-ui.md#editing-collection-metadata-in-bulk)de metadatos de varias colecciones.

## Aplicación de un perfil de metadatos a las carpetas {#applying-a-metadata-profile-to-folders}

<!-- TBD: Review this overview.
-->

Al asignar un perfil de metadatos a una carpeta, las subcarpetas heredan automáticamente el perfil de la carpeta principal. Esto significa que solo puede asignar un perfil de metadatos a una carpeta. Como tal, considere cuidadosamente la estructura de carpetas en la que carga, almacena, utiliza y archiva los recursos.

Si ha asignado un perfil de metadatos diferente a una carpeta, el nuevo perfil anula el perfil anterior. Los recursos de carpeta existentes anteriormente permanecen sin cambios. El nuevo perfil se aplica a los recursos que se agregan a la carpeta más adelante.

Las carpetas que tienen asignado un perfil se indican en la interfaz de usuario por el nombre del perfil que aparece en el nombre de la tarjeta.

![La vista de tarjetas muestra el perfil de metadatos aplicado a una carpeta](assets/metadata-profile-card-view-display.png)

Puede aplicar perfiles de metadatos a carpetas específicas o globalmente a todos los recursos.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de metadatos existente que haya cambiado posteriormente. Consulte el artículo [Reprocesamiento de recursos en una carpeta después de editar su perfil de procesamiento](processing-profiles.md#reprocessing-assets).

Puede aplicar un perfil de metadatos a una carpeta desde el menú **[!UICONTROL Herramientas]** o si está en la carpeta, desde **[!UICONTROL Propiedades]**. En esta sección se describe cómo aplicar perfiles de metadatos a las carpetas de ambos modos.

Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de vídeo existente que haya cambiado posteriormente. Consulte el artículo [Reprocesamiento de recursos en una carpeta después de editar su perfil de procesamiento](processing-profiles.md#reprocessing-assets).

### Aplicación de perfiles de metadatos a las carpetas desde la interfaz de usuario de [!UICONTROL Perfiles] {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

Siga los pasos para aplicar el perfil de metadatos:

1. Click the [!DNL Experience Manager] logo and navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Profiles]**.
1. Seleccione el perfil de metadatos que desea aplicar a una o varias carpetas.
1. Click **[!UICONTROL Apply Metadata Profile to Folder(s)]** and select the folder or multiple folders you want use to receive the newly uploaded assets and click **[!UICONTROL Done]**. Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

### Aplicación de perfiles de metadatos a las carpetas de [!UICONTROL Propiedades] {#applying-metadata-profiles-to-folders-from-properties}

1. En el carril izquierdo, haga clic en **[!UICONTROL Recursos]** y, a continuación, navegue a la carpeta a la que desee aplicar un perfil de metadatos.
1. En la carpeta, haga clic en la marca de verificación para seleccionarla y, a continuación, haga clic en **[!UICONTROL Propiedades]**.

1. Select the **[!UICONTROL Metadata Profiles]** tab and select the profile from the popup menu and click **[!UICONTROL Save]**.

Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

<!-- TBD: Commenting as the topic in metadata-config.md is incomplete.

### Apply metadata profile globally {#metadata-profile-global}

For details, see [configuration to apply metadata profile globally](/help/assets/metadata-config.md#apply-a-metadata-profile-globally). -->

### Eliminación de un perfil de metadatos de las carpetas {#removing-a-metadata-profile-from-folders}

Al eliminar un perfil de metadatos de una carpeta, las subcarpetas heredan automáticamente la eliminación del perfil de la carpeta principal. Sin embargo, cualquier procesamiento de archivos que se haya producido dentro de las carpetas permanece intacto.

Puede quitar un perfil de metadatos de una carpeta desde el menú **[!UICONTROL Herramientas]** o desde **[!UICONTROL Propiedades]** desde dentro de la carpeta.

#### Quitar perfiles de metadatos de las carpetas mediante la interfaz de usuario de Perfiles {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Click the [!DNL Experience Manager] logo and navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Profiles]**.
1. Seleccione el perfil de metadatos que desea eliminar de una carpeta o de varias carpetas.
1. Click **[!UICONTROL Remove Metadata Profile from Folder(s)]** and select the folder or multiple folders you want use to remove a profile from and click **[!UICONTROL Done]**.

   Puede confirmar que el perfil de metadatos ya no se aplica a una carpeta porque el nombre ya no aparece debajo del nombre.

#### Quitar perfiles de metadatos de las carpetas mediante Propiedades {#removing-metadata-profiles-from-folders-via-properties}

1. Haga clic en el [!DNL Experience Manager] logotipo, desplácese por **[!UICONTROL Recursos]** y, a continuación, por la carpeta desde la que desea eliminar un perfil de metadatos.
1. En la carpeta, haga clic en la marca de verificación para seleccionarla y, a continuación, haga clic en **[!UICONTROL Propiedades]**.
1. Seleccione la pestaña **[!UICONTROL Perfiles de metadatos]**, seleccione **[!UICONTROL Ninguno]** en el menú desplegable y haga clic en **[!UICONTROL Guardar]**. Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

## Sugerencias y limitaciones {#best-practices-limitations}

* Las actualizaciones de metadatos mediante la interfaz de usuario cambian las propiedades de metadatos de la `dc` Área de nombres. Cualquier actualización realizada mediante la API HTTP cambia las propiedades de metadatos de la `jcr` Área de nombres. Consulte [cómo actualizar metadatos mediante la API](/help/assets/mac-api-assets.md#update-asset-metadata)HTTP.

* El archivo CSV para importar metadatos de recursos tiene un formato muy específico. Para ahorrar esfuerzo y tiempo y evitar errores no deseados, puede crear el CSV en inicio con el formato de un archivo CSV exportado.

* Al importar metadatos con un archivo CSV, se requiere el formato de fecha `YYYY-MM-DDThh:mm:ss.fff-00:00`. Si se utiliza cualquier otro formato, no se configuran los valores de fecha. Los formatos de fecha del archivo CSV de metadatos exportado tienen el formato `YYYY-MM-DDThh:mm:ss-00:00`. Si desea importarla, conviértala al formato aceptable agregando el valor de nanosegundos indicado por `fff`.

>[!MORELIKETHIS]
>
>* [Conceptos y comprensión](metadata-concepts.md)de metadatos.
>* [Editar propiedades de metadatos de varias colecciones](managing-collections-touch-ui.md#editing-collection-metadata-in-bulk)
>* [Importación y exportación de metadatos en recursos de Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html)


<!-- TBD: Try filling the available information in these topics to the extent possible. As and when complete, publish the sections live.

## Where to find metadata of an asset or folder {#find-metadata}

What all methods to access asset Properties. More Details option in column view. Select asset and click Properties. Keyboard shortcut `p`. What else?

## Understand metadata handling in Experience Manager {#metadata-possibilities-with-aem}

Describe the journey of an assets' metadata. What all happens to metadata when an asset is added to Experience Manager.

## Add metadata to your digital assets {#add-metadata}

* To begin with, assets come with some metadata. The applications that create digital assets add some metadata to the assets created. Before uploading an asset to Experience Manager, you can edit and modify metadata using either the native application used to create an asset or using some other metadata editing application. When you upload an asset to Experience Manager, the metadata is processed.

* Link to PS, ID, AI, PDF, etc. metadata-related help articles.

* Link to XMP writeback.

* Manually add (or edit) metadata in AEM in Properties page.

* Metadata profiles

* Any workflows related to metadata?

* Advanced topic: Add, edit, modify, process and writeback metadata of subassets.

## Metadata of assets, folders, and collections {#metadata-of-assets-folders-collections}

Similarities and differences between metadata of asset and folder. 

Link to metadata handling of collections.

## Modify metadata of an asset, folder, or collection {#modify-metadata}

* While creating assets: Native application.

* Before ingesting assets: Metadata editors

* After ingesting assets: Properties of an asset, folder, collection, etc.

* Any supported programmatic method to bulk edit metadata directly in JCR?

## Modify metadata in bulk {#modify-metadata-in-bulk}

[!DNL Adobe Enterprise Manager Assets] lets you edit the metadata of multiple assets simultaneously so you can quickly propagate common metadata changes to assets in bulk. You can also edit the metadata for multiple collections in bulk.

Use the properties page to perform metadata changes on multiple assets or collections:

* Change metadata properties to a common value

* Add or modify tags

To customize the metadata properties page, including adding, modifying, deleting metadata properties, use the schema editor.

>[!NOTE]
>
>The bulk editing methods work for assets available in a folder or a collection. For the assets that are available across folders or match a common criteria, it is possible to [bulk update the metadata after searching](search-assets.md#metadataupdates).

1. In the [!DNL Assets] user interface, navigate to the location of the assets you want to edit.
1. Select the assets for which you want to edit common properties.
1. From the toolbar, click **[!UICONTROL Properties]** to open the properties page for the selected assets.

   >[!NOTE]
   >
   >When you select multiple assets, the lowest common parent form is selected for the assets. In other words, the properties page only displays metadata fields that are common across the properties pages of all the individual assets.

1. Modify the metadata properties for selected assets under the various tabs.
1. To view the metadata editor for a specific asset, deselect the remaining assets in the list. The metadata editor fields are populated with the metadata for the particular asset.

   >[!NOTE]
   >
   >* In the Properties page, you can remove assets from the asset list by deselecting them. The asset list has all the assets selected by default. The metadata for assets that you remove from the list is not updated.
   >
   >* At the top of assets list, select the check box near **[!UICONTROL Title]** to toggle between selecting the assets and clearing the list.

1. To select a different metadata schema for the assets, click **[!UICONTROL Settings]** from the toolbar, and select the desired schema.
1. Save the changes.
1. To append the new metadata with the existing metadata in fields that contain multiple values, select **[!UICONTROL Append mode]**. If you do not select this option, the new metadata replaces the existing metadata in the fields. click **[!UICONTROL Submit]**.

   >[!CAUTION]
   >
   >For single-value fields, the new metadata is not appended to the existing value in the field even if you select **[!UICONTROL Append mode]**.

-->
