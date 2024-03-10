---
title: XMP respuesta de escritura a las representaciones de
description: XMP Descubra cómo la función de reescritura de la propaga los cambios de metadatos de un recurso a todas las representaciones del recurso o a algunas específicas.
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 82148ae5-37e9-4fc5-ada9-db3d91b29c33
hide: true
source-git-commit: f349c8fd9c370ba589d217cd3b1d0521ae5c5597
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 6%

---

# XMP respuesta de escritura a las representaciones de {#xmp-writeback-to-renditions}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/xmp-metadata.html?lang=en) |
| AEM 6.5 | Este artículo |

XMP Esta función de reescritura de la en [!DNL Adobe Experience Manager Assets] replica los cambios de metadatos en las representaciones del recurso original. Al cambiar los metadatos de un recurso desde Recursos o al cargar el recurso, los cambios se almacenan inicialmente en el nodo de metadatos de la jerarquía de recursos.

XMP La función de reescritura de datos le permite propagar los cambios de metadatos a todas las representaciones del recurso o a algunas específicas. La función escribe únicamente las propiedades de metadatos que utilizan áreas de nombres registradas, es decir, una propiedad denominada `dc:title` se vuelve a escribir, pero una propiedad denominada `mytitle` no es.

Imagine un escenario en el que modifique la variable [!UICONTROL Título] propiedad del recurso con título `Classic Leather` hasta `Nylon`.

![metadatos](assets/metadata.png)

En este caso, la variable [!DNL Experience Manager Assets] guarda los cambios en el **[!UICONTROL Título]** propiedad en el `dc:title` para los metadatos de recurso almacenados en la jerarquía de recursos.

![metadata_stored](assets/metadata_stored.png)

Sin embargo, [!DNL Experience Manager Assets] no propaga automáticamente ningún cambio de metadatos a las representaciones de un recurso. Consulte [XMP cómo habilitar la reescritura de la](#enable-xmp-writeback).

## XMP Habilitar reescritura de la {#enable-xmp-writeback}

Para permitir que los cambios en los metadatos se propaguen a las representaciones del recurso al cargarlo, modifique la **[!UICONTROL Adobe CQ DAM Rendition Maker]** en el Administrador de configuración.

1. Para abrir el Administrador de configuración, acceda a `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra el **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuración.
1. Seleccione el **[!UICONTROL XMP Propagación de la]** y, a continuación, guarde los cambios.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## XMP Activación de la reescritura de datos para representaciones específicas {#enabling-xmp-writeback-for-specific-renditions}

XMP XMP Para permitir que la función de escritura en tiempo de ejecución de la propague los cambios de metadatos a ciertas representaciones, especifique estas representaciones en el paso de flujo de trabajo Proceso de escritura en tiempo de ejecución de la de [!UICONTROL Reescritura de metadatos DAM] flujo de trabajo. De forma predeterminada, este paso se configura con la representación original.

XMP Siga estos pasos para que la función de reescritura de la representación propague metadatos a las miniaturas de representación 140.100.png y 319.319.png.

1. En la interfaz de Experience Manager, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. En la página Modelos, abra el **[!UICONTROL Reescritura de metadatos DAM]** modelo de flujo de trabajo.
1. En la página de **[!UICONTROL propiedades de escritura de metadatos DAM]**, abra el paso **[!UICONTROL Proceso de escritura XMP]**.
1. En el [!UICONTROL Propiedades del paso] , haga clic en el **[!UICONTROL Proceso]** pestaña.
1. En el **Argumentos** cuadro, agregar `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`y haga clic en **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Guarde los cambios.
1. Para regenerar las representaciones de TIFF piramidal de [!DNL Dynamic Media] imágenes con los nuevos atributos, añada la variable **[!UICONTROL Recursos de imagen de proceso Dynamic Media]** paso a la [!UICONTROL Reescritura de metadatos DAM] flujo de trabajo.

   Las representaciones PTIFF solo se crean y almacenan localmente en una implementación híbrida de Dynamic Media.

1. Guarde el flujo de trabajo.

Los cambios de metadatos se propagan a las representaciones representaciones thumbnail.140.100.png y thumbnail.319.319.png del recurso, y no a las demás.

>[!NOTE]
>
>XMP Para ver los problemas de reescritura de la documentación en Linux de 64 bits, consulte [XMP Cómo habilitar la reescritura de datos en RedHat Linux de 64 bits](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>Para ver las plataformas compatibles, consulte [XMP Requisitos previos para la reescritura de metadatos](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## XMP Filtrado de metadatos de {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] admite el filtrado por lista de bloqueados y por lista de permitidos XMP de propiedades/nodos para metadatos de que se leen desde archivos binarios de recursos y se almacenan en JCR cuando se incorporan recursos.

El filtrado mediante una lista de bloqueados XMP permite importar todas las propiedades de metadatos de la, excepto las propiedades especificadas para la exclusión. XMP Sin embargo, para los tipos de recursos como archivos INDD que tienen grandes cantidades de metadatos de recursos (por ejemplo, 1000 nodos con 10 000 propiedades), los nombres de los nodos que se van a filtrar no siempre se conocen de antemano. Si el filtrado con una lista de bloqueados XMP permite importar un gran número de recursos con numerosos metadatos de la, la variable [!DNL Experience Manager] la implementación puede encontrar problemas de estabilidad, por ejemplo, colas de observación obstruidas.

XMP El filtrado de metadatos de la a través de la lista de permitidos XMP resuelve este problema ya que permite definir las propiedades que se van a importar. XMP De este modo, se ignoran todas las demás propiedades de la o desconocidas. Para la compatibilidad con versiones anteriores, puede agregar algunas de estas propiedades al filtro que utiliza una lista de bloqueados.

>[!NOTE]
>
>XMP El filtrado solo funciona para las propiedades derivadas de fuentes de recursos en archivos binarios de recursos. XMP Para las propiedades derivadas de fuentes no-, como los formatos EXIF e IPTC, el filtrado no funciona. Por ejemplo, la fecha de creación del recurso se almacena en la propiedad denominada `CreateDate` en el TIFF EXIF. El Experience Manager almacena este valor en un campo de metadatos denominado `exif:DateTimeOriginal`. XMP Como el origen no es un origen de datos de tipo de datos, el filtrado no funciona con esta propiedad.

1. Para abrir el Administrador de configuración, acceda a `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra el **[!UICONTROL XmpFilter DAM de Adobe CQ]** configuración.
1. Para aplicar el filtrado mediante una lista de permitidos, seleccione **[!UICONTROL Aplicar Lista de permitidos XMP a propiedades de la]** y especifique las propiedades que se importarán en la variable **[!UICONTROL XMP Nombres XML permitidos para el filtrado de la]** cuadro.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. XMP Para filtrar las propiedades bloqueadas después de aplicar el filtrado mediante lista de permitidos, especifíquelas en la **[!UICONTROL XMP Nombres XML bloqueados para el filtrado de la]** cuadro.

   >[!NOTE]
   >
   >El **[!UICONTROL Aplicar Lista de bloqueados XMP a propiedades de la]** está seleccionada de forma predeterminada. En otras palabras, el filtrado con una lista de bloqueados está habilitado de forma predeterminada. Para desactivar este filtrado, cancele la selección del **[!UICONTROL Aplicar Lista de bloqueados XMP a propiedades de la]** opción.

1. Guarde los cambios.
