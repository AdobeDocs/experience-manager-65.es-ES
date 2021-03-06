---
title: Reescritura XMP en representaciones
description: Descubra cómo la función XMP reescritura propaga los cambios de metadatos de un recurso a todas las representaciones del recurso o a algunas de ellas.
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 82148ae5-37e9-4fc5-ada9-db3d91b29c33
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 6%

---

# Reescritura XMP en representaciones {#xmp-writeback-to-renditions}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/xmp-metadata.html?lang=en) |
| AEM 6.5 | Este artículo |
| AEM 6.4 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/xmp-writeback.html?lang=en) |

Esta función de reescritura XMP en [!DNL Adobe Experience Manager Assets] replica los cambios de metadatos en las representaciones del recurso original. Al cambiar los metadatos de un recurso desde Assets o al cargarlo, los cambios se almacenan inicialmente en el nodo de metadatos de la jerarquía de recursos.

La función XMP reescritura permite propagar los cambios de metadatos a todas las representaciones del recurso o a algunas de ellas. La función solo recupera las propiedades de metadatos que utilizan `jcr` namespace, es decir, una propiedad denominada `dc:title` se devuelve, pero una propiedad denominada `mytitle` no.

Considere un escenario en el que modifique la variable [!UICONTROL Título] propiedad del recurso con título `Classic Leather` a `Nylon`.

![metadatos](assets/metadata.png)

En este caso, la variable [!DNL Experience Manager Assets] guarda los cambios en la variable **[!UICONTROL Título]** en la variable `dc:title` para los metadatos de recurso almacenados en la jerarquía de recursos.

![metadata_stored](assets/metadata_stored.png)

Sin embargo, [!DNL Experience Manager Assets] no propaga automáticamente ningún cambio de metadatos en las representaciones de un recurso. Consulte [cómo habilitar XMP escritura](#enable-xmp-writeback).

## Habilitar reescritura XMP {#enable-xmp-writeback}

Para permitir que los cambios en los metadatos se propaguen a las representaciones del recurso al cargarlo, modifique la variable **[!UICONTROL Creador de representaciones de Adobe CQ DAM]** en Configuration Manager.

1. Para abrir Configuration Manager, acceda a `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra el **[!UICONTROL Creador de representaciones de Adobe CQ DAM]** configuración.
1. Seleccione el **[!UICONTROL Propagación de XMP]** y, a continuación, guarde los cambios.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## Activación de la reescritura XMP para representaciones específicas {#enabling-xmp-writeback-for-specific-renditions}

Para permitir que la función XMP de reescritura propague los cambios de metadatos para seleccionar representaciones, especifique estas representaciones en el paso de flujo de trabajo XMP proceso de reescritura de [!UICONTROL Reescritura de metadatos DAM] flujo de trabajo. De forma predeterminada, este paso se configura con la representación original.

Para que la función de escritura XMP propague metadatos a las miniaturas de representación 140.100.png y 319.319.png, realice estos pasos.

1. En la interfaz de Experience Manager, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. En la página Modelos , abra la **[!UICONTROL Reescritura de metadatos DAM]** modelo de flujo de trabajo.
1. En la página de **[!UICONTROL propiedades de escritura de metadatos DAM]**, abra el paso **[!UICONTROL Proceso de escritura XMP]**.
1. En el [!UICONTROL Propiedades de los pasos] , haga clic en el botón **[!UICONTROL Proceso]** pestaña .
1. En el **Argumentos** , agregue `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`y haga clic en **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Guarde los cambios.
1. Para volver a generar las representaciones del TIFF piramidal para [!DNL Dynamic Media] imágenes con los nuevos atributos, añada la variable **[!UICONTROL Recursos de imagen de proceso de Dynamic Media]** paso a [!UICONTROL Reescritura de metadatos DAM] flujo de trabajo.

   Las representaciones PTIFF solo se crean y almacenan localmente en una implementación híbrida de Dynamic Media.

1. Guarde el flujo de trabajo.

Los cambios en los metadatos se propagan a las representaciones de representaciones thumbnail.140.100.png y thumbnail.319.319.png del recurso, y no a las demás.

>[!NOTE]
>
>Para XMP problemas de escritura en Linux de 64 bits, consulte [Cómo habilitar XMP escritura en RedHat Linux de 64 bits](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>Para las plataformas compatibles, consulte [Requisitos previos de reescritura de metadatos de XMP](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## Filtrado XMP metadatos {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] admite el filtrado de listas de permitidos y listas de bloqueados de propiedades/nodos para XMP metadatos que se leen desde binarios de recursos y se almacenan en JCR cuando se introducen recursos.

El filtrado mediante una lista de bloqueados permite importar todas las propiedades de metadatos XMP, excepto las propiedades especificadas para la exclusión. Sin embargo, para tipos de recursos como archivos INDD que tienen grandes cantidades de metadatos XMP (por ejemplo, 1000 nodos con 10 000 propiedades), los nombres de los nodos que se van a filtrar no siempre se conocen de antemano. Si el filtrado mediante una lista de bloqueados permite importar un gran número de recursos con numerosos metadatos de XMP, la variable [!DNL Experience Manager] la implementación puede encontrar problemas de estabilidad, por ejemplo, colas de observación obstruidas.

El filtrado de metadatos de XMP mediante lista de permitidos resuelve este problema ya que permite definir las propiedades de XMP que se van a importar. De este modo, se ignorarán todas las demás propiedades de XMP o desconocidas. Para la compatibilidad con versiones anteriores, puede añadir algunas de estas propiedades al filtro que utiliza una lista de bloqueados .

>[!NOTE]
>
>El filtrado solo funciona para las propiedades derivadas de XMP orígenes en los binarios de recursos. Para las propiedades derivadas de orígenes no XMP, como los formatos EXIF e IPTC, el filtrado no funciona. Por ejemplo, la fecha de creación del recurso se almacena en la propiedad denominada `CreateDate` en el TIFF EXIF. Experience Manager almacena este valor en un campo de metadatos denominado `exif:DateTimeOriginal`. Como el origen no es un origen XMP, el filtrado no funciona en esta propiedad.

1. Para abrir Configuration Manager, acceda a `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra el **[!UICONTROL Adobe CQ DAM XmpFilter]** configuración.
1. Para aplicar el filtrado a través de una lista de permitidos, seleccione **[!UICONTROL Aplicar Lista de permitidos a propiedades XMP]** y especifique las propiedades que desea importar en la variable **[!UICONTROL Nombres XML permitidos para filtrado de XMP]** en la ventana

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. Para filtrar las propiedades de XMP bloqueadas después de aplicar el filtrado a través de la lista de permitidos, especifique las en la **[!UICONTROL Nombres XML bloqueados para XMP filtrado]** en la ventana

   >[!NOTE]
   >
   >La variable **[!UICONTROL Aplicar Lista de bloqueados a propiedades XMP]** está seleccionada de forma predeterminada. En otras palabras, el filtrado mediante una lista de bloqueados está habilitado de forma predeterminada. Para desactivar este filtrado, cancele la selección del **[!UICONTROL Aplicar Lista de bloqueados a propiedades XMP]** .

1. Guarde los cambios.
