---
title: Reescritura XMP en representaciones
description: Descubra cómo la función XMP reescritura propaga los cambios de metadatos de un recurso a todas las representaciones del recurso o a algunas de ellas.
contentOwner: AG
role: Profesional empresarial, administrador
feature: Metadatos
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 5%

---


# Reescritura XMP en representaciones {#xmp-writeback-to-renditions}

Esta función XMP reescritura en [!DNL Adobe Experience Manager Assets] duplica los cambios de metadatos en las representaciones del recurso original. Al cambiar los metadatos de un recurso desde Assets o al cargarlo, los cambios se almacenan inicialmente en el nodo de metadatos de la jerarquía de recursos.

La función XMP reescritura permite propagar los cambios de metadatos a todas las representaciones del recurso o a algunas de ellas. La función solo recupera las propiedades de metadatos que utilizan el espacio de nombres `jcr`, es decir, una propiedad denominada `dc:title` se vuelve a escribir, pero no una propiedad denominada `mytitle`.

Considere un escenario en el que modifique la propiedad [!UICONTROL Title] del recurso titulada `Classic Leather` a `Nylon`.

![metadata](assets/metadata.png)

En este caso, [!DNL Experience Manager Assets] guarda los cambios en la propiedad **[!UICONTROL Title]** en el parámetro `dc:title` para los metadatos de recurso almacenados en la jerarquía de recursos.

![metadata_stored](assets/metadata_stored.png)

Sin embargo, [!DNL Experience Manager Assets] no propaga automáticamente ningún cambio en los metadatos de las representaciones de un recurso. Consulte [cómo habilitar XMP reescritura](#enable-xmp-writeback).

## Habilitar XMP escritura {#enable-xmp-writeback}

Para permitir que los cambios en los metadatos se propaguen a las representaciones del recurso al cargarlo, modifique la configuración **[!UICONTROL Adobe CQ DAM Rendition Maker]** en Configuration Manager.

1. Para abrir Configuration Manager, acceda a `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra la configuración **[!UICONTROL Adobe CQ DAM Rendition Maker]**.
1. Seleccione la opción **[!UICONTROL Propagate XMP]** y, a continuación, guarde los cambios.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## Activación de XMP escritura para representaciones específicas {#enabling-xmp-writeback-for-specific-renditions}

Para permitir que la función XMP de escritura propague los cambios de metadatos para seleccionar representaciones, especifique estas representaciones en el paso de flujo de trabajo XMP proceso de escritura del flujo de trabajo [!UICONTROL DAM Metadata WriteBack] . De forma predeterminada, este paso se configura con la representación original.

Para que la función de escritura XMP propague metadatos a las miniaturas de representación 140.100.png y 319.319.png, realice estos pasos.

1. En la interfaz del Experience Manager, vaya a **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. En la página Modelos , abra el modelo de flujo de trabajo **[!UICONTROL reescritura de metadatos DAM]** .
1. En la página de **[!UICONTROL propiedades de escritura de metadatos DAM]**, abra el paso **[!UICONTROL Proceso de escritura XMP]**.
1. En el cuadro de diálogo [!UICONTROL Step Properties], haga clic en la pestaña **[!UICONTROL Process]**.
1. En el cuadro **Argumentos**, añada `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png` y haga clic en **[!UICONTROL Aceptar]**.

   ![step_properties](assets/step_properties.png)

1. Guarde los cambios.
1. Para volver a generar las representaciones TIFF piramidales para imágenes [!DNL Dynamic Media] con los nuevos atributos, agregue el paso **[!UICONTROL Dynamic Media Process Image Assets]** al flujo de trabajo [!UICONTROL escritura de metadatos DAM] .

   Las representaciones PTIFF solo se crean y almacenan localmente en una implementación híbrida de Dynamic Media.

1. Guarde el flujo de trabajo.

Los cambios en los metadatos se propagan a las representaciones de representaciones thumbnail.140.100.png y thumbnail.319.319.png del recurso, y no a las demás.

>[!NOTE]
>
>Para XMP problemas de escritura en Linux de 64 bits, vea [Cómo habilitar XMP escritura en RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html) de 64 bits.
>
>Para las plataformas compatibles, consulte [XMP requisitos previos de reescritura de metadatos](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## Filtrado XMP metadatos {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] admite el filtrado de listas de permitidos y listas de bloqueados de propiedades/nodos para XMP metadatos que se leen desde binarios de recursos y se almacenan en JCR cuando se introducen recursos.

El filtrado mediante una lista de bloqueados permite importar todas las propiedades de metadatos XMP, excepto las propiedades especificadas para la exclusión. Sin embargo, para tipos de recursos como archivos INDD que tienen grandes cantidades de metadatos XMP (por ejemplo, 1000 nodos con 10 000 propiedades), los nombres de los nodos que se van a filtrar no siempre se conocen de antemano. Si el filtrado mediante una lista de bloqueados permite importar un gran número de recursos con varios metadatos de XMP, la implementación [!DNL Experience Manager] puede encontrar problemas de estabilidad, por ejemplo, colas de observación obstruidas.

El filtrado de metadatos de XMP mediante lista de permitidos resuelve este problema ya que permite definir las propiedades de XMP que se van a importar. De este modo, se ignorarán todas las demás propiedades de XMP o desconocidas. Para la compatibilidad con versiones anteriores, puede añadir algunas de estas propiedades al filtro que utiliza una lista de bloqueados .

>[!NOTE]
>
>El filtrado solo funciona para las propiedades derivadas de XMP orígenes en los binarios de recursos. Para las propiedades derivadas de orígenes no XMP, como los formatos EXIF e IPTC, el filtrado no funciona. Por ejemplo, la fecha de creación del recurso se almacena en la propiedad denominada `CreateDate` en el TIFF EXIF. Experience Manager almacena este valor en un campo de metadatos denominado `exif:DateTimeOriginal`. Como el origen no es un origen XMP, el filtrado no funciona en esta propiedad.

1. Para abrir Configuration Manager, acceda a `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra la configuración **[!UICONTROL Adobe CQ DAM XmpFilter]**.
1. Para aplicar el filtrado a través de una lista de permitidos, seleccione **[!UICONTROL Aplicar Lista de permitidos a XMP Propiedades]** y especifique las propiedades que desea importar en el cuadro **[!UICONTROL Nombres XML permitidos para XMP filtrado]**.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. Para filtrar las propiedades de XMP bloqueadas después de aplicar el filtrado mediante lista de permitidos, especifique las que aparecen en el cuadro **[!UICONTROL Nombres XML bloqueados para XMP filtrado]**.

   >[!NOTE]
   >
   >La opción **[!UICONTROL Aplicar Lista de bloqueados a XMP propiedades]** está seleccionada de forma predeterminada. En otras palabras, el filtrado mediante una lista de bloqueados está habilitado de forma predeterminada. Para desactivar este filtrado, cancele la selección de la opción **[!UICONTROL Aplicar Lista de bloqueados a XMP propiedades]**.

1. Guarde los cambios.
