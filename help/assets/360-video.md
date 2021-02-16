---
title: Vídeo 360/VR
description: Aprenda a trabajar con los vídeos 360 y Realidad virtual (VR) en Dynamic Media.
uuid: c21bf2c0-7acc-401f-857e-0186de86e7a1
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: aac3c850-ae84-4bff-80de-d370e150f675
docset: aem65
translation-type: tm+mt
source-git-commit: 0d5ee29141c897284f3f298d921f4f8528216f8f
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 0%

---


# Video 360/VR {#vr-video}

Los vídeos de 360 grados graban una vista en todas las direcciones al mismo tiempo. Se graban con una cámara omnidireccional o con una colección de cámaras. Durante la reproducción en una pantalla plana, el usuario controla el ángulo de visualización; la reproducción en dispositivos móviles suele aprovechar los controles giroscópicos integrados.

Dynamic Media: el modo Scene7 incluye compatibilidad nativa con el envío de 360 recursos de vídeo. De forma predeterminada, no es necesaria ninguna configuración adicional para la visualización o reproducción. El vídeo 360 se distribuye con extensiones de vídeo estándar como .mp4, .mkv y .mov. El códec más común es H.264.

En esta sección se describe cómo trabajar con el visor de vídeo de 360/VR para procesar vídeos equirectangulares para una experiencia de visualización envolvente de una sala, propiedad, ubicación, paisaje, procedimiento médico, etc.

Actualmente no se admite el audio espacial; si el audio se mezcla en estéreo, el equilibrio (L/R) no cambia a medida que el cliente cambia el ángulo de visualización de la cámara.

Consulte también [Administración de ajustes preestablecidos de visor](/help/assets/managing-viewer-presets.md).

## 360 Video en acción {#video-in-action}

Toque [Space Station 360](http://mobiletest.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS) para abrir una ventana del explorador y ver un vídeo de 360 grados. Durante la reproducción de vídeo, arrastre el puntero del ratón a una nueva ubicación para cambiar el ángulo de visualización.

![360 Video ](assets/6_5_360videoiss_simplified.png)
*sampleFotograma de vídeo de Space Station 360*

## Video 360/VR y Adobe Premiere Pro {#vr-video-and-adobe-premiere-pro}

Puede utilizar Adobe Premier Pro para la vista y edición de material de archivo 360/VR. Por ejemplo, puede colocar logotipos y texto correctamente en una escena y aplicar efectos y transiciones diseñados específicamente para medios equirectangulares.

Consulte [Editar video 360/VR](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html).

## Carga de recursos para su uso con el visor de vídeo 360 {#uploading-assets-for-use-with-the-video-viewer}

Los 360 recursos de vídeo que se cargan en AEM se etiquetan como **Multimedia** en una página de recursos, de forma similar al recurso de vídeo normal.

![6_5_360video-](assets/6_5_360video-selecttopreview.png)
*selecttopreviewRecurso de vídeo cargado 360 visto en la vista de tarjetas. El recurso está etiquetado como Multimedia.*

**Para cargar recursos para utilizarlos con el visor de vídeo de 360°:**

1. Se ha creado una carpeta dedicada al recurso de vídeo de 360°.
1. [Aplique un perfil de vídeo adaptable a la carpeta.](/help/assets/video-profiles.md#applying-a-video-profile-to-folders)

   La representación de contenido de vídeo de 360 impone requisitos más altos para la resolución de vídeo de origen y para la resolución de representaciones codificadas que el contenido de vídeo estándar que no es de 360.

   Puede utilizar el Perfil de vídeo adaptable incorporado que ya viene con Dynamic Media. Sin embargo, tenga en cuenta que el resultado será una calidad de vídeo 360 perceptiblemente inferior a la que obtendría para los vídeos no 360 codificados con la misma configuración representada con un visor de vídeo no 360. Por lo tanto, si se requiere vídeo 360 de alta calidad, haga lo siguiente:

   * Idealmente, el contenido de vídeo original de 360 debería tener una de las siguientes resoluciones:

      * 1080p - 1920 x 1080, conocida como resolución Full HD o FHD o,
      * 2160p - 3840 x 2160, conocida como resolución de 4 K, UHD o HD Ultra. Esta resolución de pantalla muy grande se encuentra con frecuencia en los televisores de alta calidad y en los monitores de ordenador. La resolución de 2160p se denomina a menudo &quot;4K&quot; porque la anchura es cercana a los 4000 píxeles. En otras palabras, oferta cuatro veces los píxeles de 1080p.
   * [Cree un ](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) perfil de vídeo adaptable personalizado con representaciones de mayor calidad. Por ejemplo, es posible que desee crear un Perfil de vídeo adaptable que contenga los tres ajustes siguientes:

      * width=auto; height=720; velocidad de bits=2500 kbps
      * width=auto; height=1080; velocidad de bits=5000 kbps
      * width=auto; height=1440; velocidad de bits=6600 kbps
   * Procese contenido de vídeo 360 en una carpeta dedicada exclusivamente a 360 recursos de vídeo.

   Tenga en cuenta que este enfoque también colocará buenas exigencias en la red y la CPU del usuario final.

1. [Cargue el vídeo en la carpeta](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).

## Anulación de la proporción de aspecto predeterminada de 360 vídeos {#overriding-the-default-aspect-ratio-of-videos}

Para que un recurso cargado se considere un vídeo de 360° que se va a utilizar con el visor de vídeo de 360°, el recurso debe tener una proporción de aspecto de 2°.

De forma predeterminada, AEM detecta el vídeo como &quot;360&quot; si su proporción de aspecto (anchura/altura) es 2,0. Si es un administrador, puede anular la configuración de proporción de aspecto predeterminada de 2 estableciendo la propiedad opcional `s7video360AR` en CRXDE Lite de la siguiente manera:

* `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

   * **Tipo** de propiedad: Doble
   * **Valor**: proporción de aspecto de coma flotante, valor predeterminado 2,0.

Después de establecer esta propiedad, esta se aplicará inmediatamente tanto a los vídeos existentes como a los vídeos recién cargados.

La proporción de aspecto se aplica a 360 recursos de vídeo para la página de detalles de recursos y el [componente WCM de medios de vídeo 360](/help/assets/adding-dynamic-media-assets-to-pages.md#dynamic-media-components).

Inicio mediante la carga de 360 vídeos.

## Vista previa de vídeo de 360 {#previewing-video}

Puede utilizar la Previsualización para ver el aspecto que tendrá el vídeo 360 para los clientes y asegurarse de que se comporta de la forma esperada.

Consulte también [Edición de ajustes preestablecidos de visor](/help/assets/managing-viewer-presets.md#editing-viewer-presets).

Cuando esté satisfecho con el vídeo de 360, puede publicarlo.

Consulte [Incrustación del visor de imágenes o vídeos en una página Web.](https://helpx.adobe.com/experience-manager/6-5/help/assets/embed-code.html)
Consulte  [Vinculación de direcciones URL a la aplicación](https://helpx.adobe.com/experience-manager/6-5/help/assets/linking-urls-to-yourwebapplication.html) web. Tenga en cuenta que el método de vinculación basado en URL no es posible si el contenido interactivo tiene vínculos con direcciones URL relativas, especialmente vínculos a páginas de AEM Sites.
Consulte [Añadir Dynamic Media Assets a páginas.](https://helpx.adobe.com/experience-manager/6-5/help/assets/adding-dynamic-media-assets-to-pages.html)

**Para previsualización De Videos 360**

1. En **[!UICONTROL Recursos]**, navegue a un vídeo existente de 360 que haya creado. Toque el recurso de vídeo 360 para abrirlo en modo de previsualización.

   ![6_5_360video-selecttopreview-1](assets/6_5_360video-selecttopreview-1.png)

   Toque el recurso de vídeo 360 para previsualización del vídeo.

1. En la página previsualización, cerca de la esquina superior izquierda de la página, toque la lista desplegable y, a continuación, seleccione **[!UICONTROL Visores.]**

   ![6_5_360visores de previsualización de vídeo](assets/6_5_360video-preview-viewers.png)

   En la lista Visores, toque **[!UICONTROL Video360_social]** y, a continuación, realice una de las siguientes acciones:

   * Arrastre el puntero del ratón sobre el vídeo para modificar el ángulo de visualización de la escena estática.
   * Toque el botón **[!UICONTROL Reproducir]** del vídeo para iniciar la reproducción; a medida que se reproduce el vídeo, arrastre el puntero del ratón sobre el vídeo para modificar el ángulo de visualización.

   ![6_5_360video-previsualización-video360-](assets/6_5_360video-preview-video360-social.png)*socialCaptura de pantalla de vídeo de 360°.*

   * En la lista Visores, toque **[!UICONTROL Video360VR.]**

      El vídeo de Realidad virtual (VR) es un contenido de vídeo envolvente al que se accede mediante auriculares de realidad virtual. Al igual que con los vídeos normales, puede crear vídeos VR al principio cuando se graba o captura un vídeo con cámaras de vídeo de 360 grados.
   ![6_5_360video-previsualización-video360vr](assets/6_5_360video-preview-video360vr.png)
   *Captura de pantalla de vídeo de 360 VR.*

1. Cerca de la parte superior derecha de la página de previsualización, toque **[!UICONTROL Cerrar.]**

## Publicación de vídeo 360 {#publishing-video}

Debe publicar el vídeo 360 para utilizarlo. La publicación de un vídeo de 360 activa la URL y el código incrustado. También publica el vídeo 360 en la nube de Dynamic Media, que está integrado con una CDN para un envío escalable y de rendimiento.

Consulte [Publicación de Dynamic Media Assets](/help/assets/publishing-dynamicmedia-assets.md) para obtener más información sobre cómo publicar Video 360.
Consulte también [Incrustación del visor de imágenes o vídeos en una página Web](https://helpx.adobe.com/experience-manager/6-5/help/assets/embed-code.html).
Consulte también [Vinculación de direcciones URL a la aplicación Web](https://helpx.adobe.com/experience-manager/6-5/help/assets/linking-urls-to-yourwebapplication.html). Tenga en cuenta que el método de vinculación basado en URL no es posible si el contenido interactivo tiene vínculos con direcciones URL relativas, especialmente vínculos a páginas de AEM Sites.
Consulte también [Añadir Dynamic Media Assets a páginas.](https://helpx.adobe.com/experience-manager/6-5/help/assets/adding-dynamic-media-assets-to-pages.html)
