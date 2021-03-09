---
title: Reescritura XMP en representaciones
description: Descubra cómo la función de reescritura XMP propaga los cambios de metadatos de un recurso a todas las representaciones del recurso o a algunas de ellas.
contentOwner: AG
translation-type: tm+mt
source-git-commit: cf86d0c38e326766b35318e78a94a3f32e166e01
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 5%

---


# Reescritura XMP en representaciones {#xmp-writeback-to-renditions}

La función de reescritura XMP de [!DNL Adobe Experience Manager Assets] duplica los cambios en los metadatos de los recursos en las representaciones del recurso. Cuando cambia los metadatos de un recurso desde [!DNL Experience Manager Assets] o mientras carga el recurso, los cambios se almacenan inicialmente dentro del nodo del recurso en CRXDe. La función de reescritura XMP propaga los cambios de metadatos en todas las representaciones del recurso o en determinadas representaciones.

Considere un escenario en el que modifique la propiedad [!UICONTROL Title] del recurso titulada `Classic Leather` a `Nylon`.

![metadata](assets/metadata.png)

En este caso, [!DNL Experience Manager Assets] guarda los cambios en la propiedad **[!UICONTROL Title]** en el parámetro `dc:title` para los metadatos de recurso almacenados en la jerarquía de recursos.

![metadata_stored](assets/metadata_stored.png)

Sin embargo, [!DNL Experience Manager Assets] no propaga automáticamente ningún cambio en los metadatos de las representaciones de un recurso.

La función de reescritura XMP permite propagar los cambios de metadatos a todas las representaciones del recurso o a algunas de ellas. Sin embargo, los cambios no se almacenan en el nodo de metadatos de la jerarquía de recursos. En su lugar, esta función incrusta los cambios en los archivos binarios de las representaciones.

## Habilitación del reescritura XMP {#enabling-xmp-writeback}

Para permitir que los cambios en los metadatos se propaguen a las representaciones del recurso al cargarlo, modifique la configuración **[!UICONTROL Adobe CQ DAM Rendition Maker]** en Configuration Manager.

1. Para abrir Configuration Manager, acceda a `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra la configuración **[!UICONTROL Adobe CQ DAM Rendition Maker]**.
1. Seleccione la opción **[!UICONTROL Propagate XMP]** y, a continuación, guarde los cambios.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## Habilitación de la reescritura XMP para representaciones específicas {#enabling-xmp-writeback-for-specific-renditions}

Para que la función de escritura XMP propague los cambios de metadatos para seleccionar representaciones, especifique estas representaciones en el paso de flujo de trabajo del proceso de escritura XMP del flujo de trabajo [!UICONTROL DAM Metadata WriteBack] . De forma predeterminada, este paso se configura con la representación original.

Para que la función de escritura XMP propague metadatos a las miniaturas de representación 140.100.png y 319.319.png, realice estos pasos.

1. En la interfaz de Experience Manager, vaya a **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. En la página Modelos , abra el modelo de flujo de trabajo **[!UICONTROL reescritura de metadatos DAM]** .
1. En la página de **[!UICONTROL propiedades de escritura de metadatos DAM]**, abra el paso **[!UICONTROL Proceso de escritura XMP]**.
1. En el cuadro de diálogo [!UICONTROL Step Properties], haga clic en la pestaña **[!UICONTROL Process]**.
1. En el cuadro **Argumentos**, añada `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png` y haga clic en **Aceptar**.

   ![step_properties](assets/step_properties.png)

1. Guarde los cambios.
1. Para volver a generar las representaciones TIFF piramidales para imágenes [!DNL Dynamic Media] con los nuevos atributos, agregue el paso **[!UICONTROL Recursos de imagen de proceso de Dynamic Media]** al flujo de trabajo [!UICONTROL Reescritura de metadatos DAM] .

   Las representaciones PTIFF solo se crean y almacenan localmente en una implementación híbrida de Dynamic Media.

1. Guarde el flujo de trabajo.

Los cambios en los metadatos se propagan a las representaciones de representaciones thumbnail.140.100.png y thumbnail.319.319.png del recurso, y no a las demás.

>[!NOTE]
>
>Para problemas de escritura XMP en Linux de 64 bits, consulte [Cómo habilitar la reescritura XMP en RedHat Linux de 64 bits](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>Para las plataformas compatibles, consulte [Requisitos previos de reescritura de metadatos XMP](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## Filtrado de metadatos XMP {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] admite el filtrado de listas bloqueadas y listas permitidas de propiedades/nodos para metadatos XMP que se leen desde binarios de recursos y se almacenan en JCR cuando se incorporan recursos.

El filtrado mediante una lista bloqueada permite importar todas las propiedades de metadatos XMP, excepto las propiedades especificadas para la exclusión. Sin embargo, para tipos de recursos como archivos INDD que tienen grandes cantidades de metadatos XMP (por ejemplo, 1000 nodos con 10 000 propiedades), los nombres de los nodos que se van a filtrar no siempre se conocen de antemano. Si el filtrado mediante una lista bloqueada permite importar un gran número de activos con numerosos metadatos XMP, la implementación [!DNL Experience Manager] puede encontrar problemas de estabilidad, por ejemplo colas de observación obstruidas.

El filtrado de metadatos XMP a través de la lista de permitidos resuelve este problema permitiendo definir las propiedades XMP que se van a importar. De este modo, se ignorarán todas las demás propiedades XMP o desconocidas. Para la compatibilidad con versiones anteriores, puede agregar algunas de estas propiedades al filtro que utiliza una lista bloqueada.

>[!NOTE]
>
>El filtrado solo funciona para las propiedades derivadas de orígenes XMP en los binarios de recursos. Para las propiedades derivadas de orígenes no XMP, como los formatos EXIF e IPTC, el filtrado no funciona. Por ejemplo, la fecha de creación del recurso se almacena en la propiedad denominada `CreateDate` en el TIFF EXIF. Experience Manager almacena este valor en un campo de metadatos denominado `exif:DateTimeOriginal`. Como el origen es un origen que no es XMP, el filtrado no funciona en esta propiedad.

1. Para abrir Configuration Manager, acceda a `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra la configuración **[!UICONTROL Adobe CQ DAM XmpFilter]**.
1. Para aplicar el filtrado a través de una lista permitida, seleccione **[!UICONTROL Aplicar lista de permitidos a las propiedades XMP]** y especifique las propiedades que desea importar en el cuadro **[!UICONTROL Nombres XML permitidos para el filtrado XMP]**.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. Para filtrar las propiedades XMP bloqueadas después de aplicar el filtrado a través de la lista permitida, especifique las que aparecen en el cuadro **[!UICONTROL Nombres XML bloqueados para el filtrado XMP]**.

   >[!NOTE]
   >
   >La opción **[!UICONTROL Aplicar lista de bloqueados a propiedades XMP]** está seleccionada de forma predeterminada. En otras palabras, el filtrado mediante una lista bloqueada está habilitado de forma predeterminada. Para desactivar este filtrado, cancele la selección de la opción **[!UICONTROL Apply Blocklist to XMP Properties]**.

1. Guarde los cambios.
