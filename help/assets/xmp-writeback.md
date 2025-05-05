---
title: XMP respuesta de escritura a las representaciones de
description: XMP Descubra cómo la función de reescritura de la propaga los cambios de metadatos de un recurso a todas las representaciones del recurso o a algunas específicas.
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 82148ae5-37e9-4fc5-ada9-db3d91b29c33
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 6%

---

# XMP respuesta de escritura a las representaciones de {#xmp-writeback-to-renditions}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/xmp-metadata.html?lang=es) |
| AEM 6.5 | Este artículo |

XMP Esta característica de reescritura de la [!DNL Adobe Experience Manager Assets] replica los cambios de metadatos en las representaciones del recurso original. Al cambiar los metadatos de un recurso desde Assets o al cargar el recurso, los cambios se almacenan inicialmente en el nodo de metadatos de la jerarquía de recursos.

XMP La función de reescritura de datos le permite propagar los cambios de metadatos a todas las representaciones del recurso o a algunas específicas. La característica sólo devuelve las propiedades de metadatos que utilizan áreas de nombres registradas, es decir, se devuelve una propiedad denominada `dc:title` pero no una propiedad denominada `mytitle`.

Imagine un escenario en el que modifica la propiedad [!UICONTROL Title] del recurso con título `Classic Leather` a `Nylon`.

![metadatos](assets/metadata.png)

En este caso, [!DNL Experience Manager Assets] guarda los cambios realizados en la propiedad **[!UICONTROL Title]** en el parámetro `dc:title` para los metadatos de recursos almacenados en la jerarquía de recursos.

![metadata_stored](assets/metadata_stored.png)

Sin embargo, [!DNL Experience Manager Assets] no propaga automáticamente ningún cambio de metadatos a las representaciones de un recurso. XMP Consulte [cómo habilitar la reescritura de la escritura en el código de la cuenta de usuario](#enable-xmp-writeback).

## XMP Habilitar reescritura de la {#enable-xmp-writeback}

Para permitir que los cambios de metadatos se propaguen a las representaciones del recurso al cargarlo, modifique la configuración de **[!UICONTROL Adobe CQ DAM Rendition Maker]** en Configuration Manager.

1. Para abrir el Administrador de configuración, acceda a `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra la configuración de **[!UICONTROL Adobe CQ DAM Rendition Maker]**.
1. XMP Seleccione la opción **[!UICONTROL Propagación de los cambios]** y, a continuación, guarde los cambios.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## XMP Activación de la reescritura de datos para representaciones específicas {#enabling-xmp-writeback-for-specific-renditions}

XMP XMP Para permitir que la característica de escritura en tiempo real de la función de escritura en tiempo real propague los cambios de metadatos a las representaciones seleccionadas, especifique estas representaciones en el paso de flujo de trabajo Proceso de escritura en tiempo real de [!UICONTROL DAM Metadata WriteBack] del flujo de trabajo. De forma predeterminada, este paso se configura con la representación original.

XMP Siga estos pasos para que la función de reescritura de la representación propague metadatos a las miniaturas de representación 140.100.png y 319.319.png.

1. En la interfaz del Experience Manager, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. En la página Modelos, abra el modelo de flujo de trabajo **[!UICONTROL DAM Metadata Writeback]**.
1. En la página de **[!UICONTROL propiedades de escritura de metadatos DAM]**, abra el paso **[!UICONTROL Proceso de escritura XMP]**.
1. En el cuadro de diálogo [!UICONTROL Propiedades del paso], haga clic en la ficha **[!UICONTROL Proceso]**.
1. En el cuadro **Argumentos**, agregue `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png` y haga clic en **[!UICONTROL Aceptar]**.

   ![step_properties](assets/step_properties.png)

1. Guarde los cambios.
1. Para volver a generar las representaciones de TIFF piramidales de [!DNL Dynamic Media] imágenes con los nuevos atributos, agregue el paso **[!UICONTROL Dynamic Media Process Image Assets]** al flujo de trabajo [!UICONTROL DAM Metadata Writeback].

   Las representaciones PTIFF solo se crean y almacenan localmente en una implementación híbrida de Dynamic Media.

1. Guarde el flujo de trabajo.

Los cambios de metadatos se propagan a las representaciones representaciones thumbnail.140.100.png y thumbnail.319.319.png del recurso, y no a las demás.

>[!NOTE]
>
>XMP XMP Para obtener información sobre problemas de reescritura en Linux de 64 bits, consulte [Cómo habilitar la reescritura en redHat Linux de 64 bits](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html) con el procedimiento de reescritura en redHat .
>
>XMP Para las plataformas admitidas, consulte [Requisitos previos para la reescritura de metadatos de la colección de ](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## XMP Filtrado de metadatos de {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] admite el filtrado de propiedades/nodos de lista de bloqueados y lista de permitidos XMP para los metadatos de los recursos que se leen desde los archivos binarios de recursos y se almacenan en JCR cuando se incorporan los recursos.

El filtrado mediante una lista de bloqueados XMP permite importar todas las propiedades de metadatos de la, excepto las propiedades especificadas para la exclusión. XMP Sin embargo, para los tipos de recursos como archivos INDD que tienen grandes cantidades de metadatos de recursos (por ejemplo, 1000 nodos con 10 000 propiedades), los nombres de los nodos que se van a filtrar no siempre se conocen de antemano. Si el filtrado mediante una lista de bloqueados XMP permite importar un gran número de recursos con numerosos metadatos de la, la implementación de [!DNL Experience Manager] puede encontrar problemas de estabilidad, por ejemplo, colas de observación obstruidas.

XMP El filtrado de metadatos de la a través de la lista de permitidos XMP resuelve este problema ya que permite definir las propiedades que se van a importar. XMP De este modo, se ignoran todas las demás propiedades de la o desconocidas. Para la compatibilidad con versiones anteriores, puede agregar algunas de estas propiedades al filtro que utiliza una lista de bloqueados.

>[!NOTE]
>
>XMP El filtrado solo funciona para las propiedades derivadas de fuentes de recursos en archivos binarios de recursos. XMP Para las propiedades derivadas de fuentes no-, como los formatos EXIF e IPTC, el filtrado no funciona. Por ejemplo, la fecha de creación del recurso se almacena en la propiedad denominada `CreateDate` del TIFF EXIF. El Experience Manager almacena este valor en un campo de metadatos denominado `exif:DateTimeOriginal`. XMP Como el origen no es un origen de datos de tipo de datos, el filtrado no funciona con esta propiedad.

1. Para abrir el Administrador de configuración, acceda a `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra la configuración de **[!UICONTROL Adobe CQ DAM XmpFilter]**.
1. Para aplicar el filtrado a través de una lista de permitidos, seleccione **[!UICONTROL Aplicar Lista de permitidos XMP XMP a propiedades de la]** y especifique las propiedades que se importarán en el cuadro **[!UICONTROL Nombres XML permitidos para el filtrado]**.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. XMP Para filtrar las propiedades bloqueadas después de aplicar el filtrado mediante la lista de permitidos XMP, especifique las del cuadro **[!UICONTROL Nombres XML bloqueados para el filtrado de la]**.

   >[!NOTE]
   >
   >La opción **[!UICONTROL Aplicar Lista de bloqueados XMP a las propiedades de la]** está seleccionada de forma predeterminada. En otras palabras, el filtrado con una lista de bloqueados está habilitado de forma predeterminada. Para deshabilitar este tipo de filtrado, cancele la selección de la opción **[!UICONTROL Aplicar Lista de bloqueados XMP a las propiedades de la]**.

1. Guarde los cambios.
