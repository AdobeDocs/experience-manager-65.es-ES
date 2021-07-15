---
title: Vídeo 360/VR
description: Aprenda a trabajar con 360 y vídeo de realidad virtual (VR) en Dynamic Media.
uuid: c21bf2c0-7acc-401f-857e-0186de86e7a1
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: aac3c850-ae84-4bff-80de-d370e150f675
docset: aem65
feature: Vídeo de RV 360
role: User, Admin
exl-id: 0c2077a7-bd16-484b-980f-4d4a1a681491
source-git-commit: 471f9e99078a1e0af60024d439afd42ae77cba8c
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 0%

---

# Vídeo 360/VR {#vr-video}

Los vídeos de 360 grados graban una vista en todas las direcciones al mismo tiempo. Se graban con una cámara omnidireccional o con una colección de cámaras. Durante la reproducción en una pantalla plana, el usuario controla el ángulo de visualización; los reproductores en dispositivos móviles suelen utilizar sus controles giroscópicos integrados.

Dynamic Media: el modo Scene7 incluye compatibilidad nativa con la entrega de 360 recursos de vídeo. De forma predeterminada, no es necesaria ninguna configuración adicional para la visualización o reproducción. El vídeo 360 se entrega con extensiones de vídeo estándar como .mp4, .mkv y .mov. El códec más común es H.264.

En esta sección se describe cómo trabajar con el visualizador de vídeo 360/VR para procesar un vídeo equirectangular que ofrezca una experiencia de visualización inmersiva de una habitación, propiedad, ubicación, paisaje, procedimiento médico, etc.

Actualmente no se admite audio espacial; si el audio se mezcla en estéreo, el balance (L/R) no cambia a medida que el cliente cambia el ángulo de visualización de la cámara.

Consulte también [Administración de ajustes preestablecidos de visualizador](/help/assets/managing-viewer-presets.md).

## 360 Vídeo en acción {#video-in-action}

Seleccione [Space Station 360](https://mobiletest.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS) para abrir una ventana del navegador y ver un vídeo de 360 grados. Durante la reproducción de vídeo, arrastre el puntero del ratón a una nueva ubicación para cambiar el ángulo de visualización.

![360 ](assets/6_5_360videoiss_simplified.png)
*Ejemplo de vídeoFotograma de vídeo de la estación espacial 360*

## Vídeo y Adobe Premiere Pro 360/VR {#vr-video-and-adobe-premiere-pro}

Puede utilizar Adobe Premier Pro para ver y editar material de archivo 360/VR. Por ejemplo, puede colocar logotipos y texto correctamente en una escena y aplicar efectos y transiciones diseñados específicamente para medios equirectangulares.

Consulte [Editar vídeo 360/VR](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html).

## Cargar recursos para usarlos con el visor de vídeos 360 {#uploading-assets-for-use-with-the-video-viewer}

Los 360 recursos de vídeo que se cargan en Adobe Experience Manager están etiquetados como **Multimedia** en una página de Asset, de forma similar al recurso de vídeo normal.

![6_5_360video-](assets/6_5_360video-selecttopreview.png)
*selecttopreviewRecurso de vídeo cargado 360 que se ve en la vista de tarjeta. El recurso está etiquetado como multimedia.*

**Cargue recursos para utilizarlos con el visor de vídeos 360:**

1. Se ha creado una carpeta dedicada al recurso de vídeo 360.
1. [Aplicar un perfil de vídeo adaptable a la carpeta](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).

   El procesamiento de contenido de vídeo 360 supone un requisito mayor para la resolución de vídeo de origen y para la resolución de representaciones codificadas que el contenido de vídeo estándar no 360.

   Puede utilizar el perfil de vídeo adaptable incorporado que ya viene con Dynamic Media. Sin embargo, tiene como resultado una calidad de vídeo 360 perceptiblemente inferior a la que obtendría para el vídeo no 360 codificado con la misma configuración representada con un visor de vídeo no 360. Por lo tanto, si se requiere vídeo 360 de alta calidad, haga lo siguiente:

   * Lo ideal es que su contenido original de vídeo 360 tenga una de las siguientes resoluciones:

      * 1080p - 1920 x 1080, conocida como resolución Full HD o FHD,
      * 2160p - 3840 x 2160, conocida como resolución de alta definición de 4 k, UHD o Ultra. Esta gran resolución de pantalla suele encontrarse en los televisores de gama alta y en los monitores de ordenador. La resolución 2160p a menudo se denomina &quot;4k&quot; porque la anchura es cercana a los 4000 píxeles. En otras palabras, ofrece cuatro veces los píxeles de 1080p.
   * [Cree un ](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) perfil de vídeo adaptable personalizado con representaciones de mayor calidad. Por ejemplo, cree un perfil de vídeo adaptable que contenga las tres configuraciones siguientes:

      * width=auto; height=720; velocidad de bits=2500 kbps
      * width=auto; height=1080; velocidad de bits=5000 kbps
      * width=auto; height=1440; velocidad de bits=6600 kbps
   * Procese contenido de vídeo 360 en una carpeta dedicada exclusivamente a 360 recursos de vídeo.

   Este enfoque impone buenas exigencias a la red y a la CPU del usuario final.

1. [Cargue el vídeo en la carpeta](/help/assets/managing-video-assets.md#upload-and-preview-video-assets) .

## Anular la proporción de aspecto predeterminada de 360 vídeos  {#overriding-the-default-aspect-ratio-of-videos}

Para que un recurso cargado se clasifique como vídeo de 360 que pretenda usar con el visor de vídeo de 360, el recurso debe tener una proporción de aspecto de 2.

De forma predeterminada, el Experience Manager detecta el vídeo como &quot;360&quot; si su relación de aspecto (anchura/altura) es 2.0. Si es un administrador, puede anular el valor predeterminado de relación de aspecto de 2 estableciendo la propiedad opcional `s7video360AR` en el CRXDE Lite de la siguiente manera:

* `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

   * **Tipo de propiedad** : doble
   * **Valor** : relación de aspecto de coma flotante, predeterminada 2,0.

Después de establecer esta propiedad, esta entra en vigor inmediatamente en los vídeos existentes y en los nuevos cargados.

La proporción de aspecto se aplica a 360 recursos de vídeo para la página de detalles del recurso y el [componente Media WCM de vídeo 360](/help/assets/adding-dynamic-media-assets-to-pages.md#dynamic-media-components).

Comience por cargar 360 vídeos.

## Vista previa del vídeo 360 {#previewing-video}

Puede usar Vista previa para ver el aspecto que tendrá el vídeo 360 para los clientes y asegurarse de que se comporta según lo esperado.

Consulte también [Editar ajustes preestablecidos de visualizador](/help/assets/managing-viewer-presets.md#editing-viewer-presets).

Cuando esté satisfecho con el vídeo 360, puede publicarlo.

Consulte [Incrustar el visualizador de imágenes o vídeos en una página web](/help/assets/embed-code.md).
Consulte [Vincular URL a su aplicación web](/help/assets/linking-urls-to-yourwebapplication.md). El método de vinculación basado en URL no es posible si el contenido interactivo tiene vínculos con direcciones URL relativas, especialmente vínculos a páginas de sitios Experience Manager.
Consulte [Agregar recursos de Dynamic Media a las páginas](/help/assets/adding-dynamic-media-assets-to-pages.md).

**Para previsualizar el vídeo 360:**

1. En **[!UICONTROL Assets]**, vaya a un vídeo 360 existente que haya creado. Seleccione el recurso de vídeo 360 para poder abrirlo en el modo de vista previa.

   ![6_5_360video-selecttopreview-1](assets/6_5_360video-selecttopreview-1.png)

   Seleccione el recurso de vídeo 360 para poder previsualizar el vídeo.

1. En la página de vista previa, cerca de la esquina superior izquierda de la página, seleccione la lista desplegable y luego seleccione **[!UICONTROL Visualizadores]**.

   ![6_5_360visores de vista previa de vídeo](assets/6_5_360video-preview-viewers.png)

   En la lista Visualizadores, seleccione **[!UICONTROL Video360_social]** y, a continuación, realice una de las siguientes acciones:

   * Arrastre el puntero del ratón por el vídeo si desea modificar el ángulo de visualización de la escena estática.
   * Seleccione el botón **[!UICONTROL Play]** del vídeo si desea comenzar la reproducción. A medida que se reproduce el vídeo, arrastre el puntero del ratón sobre el vídeo para modificar su ángulo de visualización.

   ![Captura de pantalla de vídeo de 6_5_360video-preview-video360-](assets/6_5_360video-preview-video360-social.png)*socialA 360.*

   * En la lista Visualizadores, seleccione **[!UICONTROL Video360VR]**.

      El vídeo de Realidad virtual (VR) es contenido de vídeo inmersivo al que se accede mediante auriculares de realidad virtual. Al igual que con los vídeos normales, se crean vídeos VR al principio cuando se graba o captura un vídeo con cámaras de vídeo de 360 grados.
   ![6_5_360video-preview-video360vr](assets/6_5_360video-preview-video360vr.png)
   *Captura de pantalla de un video de 360 VR.*

1. Cerca de la parte superior derecha de la página de vista previa, seleccione **[!UICONTROL Cerrar]**.

## Publicar vídeo 360 {#publishing-video}

Publique el vídeo 360 para que pueda utilizarlo. Al publicar un vídeo de 360 se activa la dirección URL y el código incrustado. También publica el vídeo 360 en la nube de Dynamic Media, que está integrado con una CDN para una entrega escalable y con rendimiento.

Consulte [Publicar recursos de Dynamic Media](/help/assets/publishing-dynamicmedia-assets.md) para obtener más información sobre cómo publicar vídeos 360.
Consulte también [Incrustar el visualizador de imágenes o vídeos en una página web](/help/assets/embed-code.md).
Consulte también [Vincular URL a su aplicación web](/help/assets/linking-urls-to-yourwebapplication.md). El método de vinculación basado en URL no es posible si el contenido interactivo tiene vínculos con direcciones URL relativas, especialmente vínculos a páginas de sitios Experience Manager.
Consulte también [Agregar recursos de Dynamic Media a páginas](/help/assets/adding-dynamic-media-assets-to-pages.md).
