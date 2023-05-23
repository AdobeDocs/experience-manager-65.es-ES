---
title: Aplicación de ajustes preestablecidos de imagen de Dynamic Media
description: Aprenda a aplicar ajustes preestablecidos de imagen en Dynamic Media
uuid: 8bafcbd0-6df0-4d5b-b2f7-116ddb4ec060
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 5c1f60ac-3741-4002-9c5d-c128f118342b
feature: Image Presets
role: User,Admin
exl-id: 98d88b59-eb8f-42db-abb8-04506a5b8c30
source-git-commit: 4b8369de9e6a10b73115d53358ce98729d92ed44
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 3%

---

# Aplicar ajustes preestablecidos de imagen de Dynamic Media {#applying-image-presets}

Los ajustes preestablecidos de imagen permiten que los recursos entreguen imágenes de forma dinámica en diferentes tamaños, en diferentes formatos o con otras propiedades de imagen que se generan dinámicamente. Puede elegir un ajuste preestablecido al exportar imágenes. El ajuste preestablecido redistribuye las imágenes según las especificaciones especificadas por el administrador.

Además, puede elegir un ajuste preestablecido de imagen que sea interactivo (designado por el **[!UICONTROL RESS]** después de seleccionarlo).

En esta sección se describe cómo utilizar los ajustes preestablecidos de imagen. [Los administradores pueden crear y configurar ajustes preestablecidos de imagen](managing-image-presets.md).

>[!NOTE]
>
>Las imágenes inteligentes funcionan con los ajustes preestablecidos de imagen existentes y utilizan inteligencia en el último milisegundo de entrega para reducir aún más el tamaño del archivo de imagen en función de la velocidad de conexión del explorador o de la red. Consulte [Imágenes inteligentes](imaging-faq.md) para obtener más información.

Puede aplicar un ajuste preestablecido de imagen a una imagen cada vez que la previsualice.

>[!NOTE]
>
>En el modo Dynamic Media - Scene7, los ajustes preestablecidos de imagen solo son compatibles con los recursos de imagen.

**Para aplicar ajustes preestablecidos de imagen de Dynamic Media:**

1. Abra el recurso y, en el carril izquierdo, seleccione el menú desplegable y, a continuación, seleccione **[!UICONTROL Representaciones]**.

   >[!NOTE]
   >
   >* Las representaciones estáticas aparecen en la mitad superior del panel. Las representaciones dinámicas aparecen en la mitad inferior. Solo con las representaciones dinámicas, puede utilizar la dirección URL para mostrar la imagen. El **[!UICONTROL URL]** El botón sólo aparece si selecciona una representación dinámica. El **[!UICONTROL RESS]** El botón solo aparece si selecciona un ajuste preestablecido de imagen interactivo.
   >
   >* El sistema muestra numerosas representaciones al seleccionar **[!UICONTROL Representaciones]** en la Vista de detalles de un recurso. Puede aumentar el número de ajustes preestablecidos vistos. Consulte [Aumente el número de ajustes preestablecidos de imagen que se muestran](managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display).


   ![chlimage_1-208](assets/chlimage_1-208.png)

1. Realice una de las siguientes acciones:

   * Seleccione una representación dinámica para poder previsualizar el ajuste preestablecido de imagen.
   * Para mostrar la ventana emergente, seleccione **[!UICONTROL URL]**, **[!UICONTROL Incrustar]**, o **[!UICONTROL RESS]**.

   >[!NOTE]
   >
   >Si el recurso *y* Si los ajustes preestablecidos de imagen aún no se han publicado, la variable **[!UICONTROL URL]** botón (o **[!UICONTROL URL]** y **[!UICONTROL RESS]** botones, si corresponde) no está disponible.
   >
   >Tenga en cuenta también que los ajustes preestablecidos de imagen se publican automáticamente en un servidor de Dynamic Media.
