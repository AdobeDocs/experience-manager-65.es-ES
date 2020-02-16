---
title: Incrustación del visor de vídeo o de imagen de Dynamic Media en una página web
description: Obtenga información sobre cómo incrustar vídeos o imágenes de Dynamic Media en una página web
uuid: 6f786521-eb6c-4c80-8c15-9bf97b56818f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4ae76d8a-208f-4099-9f17-a94df424685e
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Incrustación del visor de vídeo o de imagen de Dynamic Media en una página web {#embedding-the-video-or-image-viewer-on-a-web-page}

Utilice la función **[!UICONTROL Código]** incrustado cuando desee reproducir el vídeo o ver un recurso incrustado en una página web. El código incrustado se copia en el portapapeles para pegarlo en las páginas web. No se permite la edición del código en el cuadro de diálogo **[!UICONTROL Código]** incrustado.

Las direcciones URL se incrustan solo si _no está_ usando AEM como WCM. Si está utilizando AEM como WCM, [agregue los recursos directamente en la página.](adding-dynamic-media-assets-to-pages.md)

See [Linking URLs to your Web Application.](linking-urls-to-yourwebapplication.md)

Consulte [Envío de imágenes optimizadas para un sitio interactivo.](responsive-site.md)

>[!NOTE]
>
>El código incrustado no está disponible para copiar hasta que haya publicado el recurso seleccionado. Además, también debe publicar el ajuste preestablecido de visor o el ajuste preestablecido de imagen.
>
>Consulte [Publicación de recursos](publishing-dynamicmedia-assets.md).
>
>See [Publishing Viewer Presets](managing-viewer-presets.md#publishing-viewer-presets).
>
>See [Publishing Image Presets](managing-image-presets.md#publishing-image-presets).

**Incrustación del visor de vídeo o de imagen de Dynamic Media en una página web**

1. Vaya al recurso de imagen o vídeo *publicado* cuyo código incrustado desee copiar.

   Recuerde que el código incrustado solo está disponible para copiar *después* de *publicar* los recursos por primera vez. Además, también se debe publicar el ajuste preestablecido de visor o de imagen.

   Consulte [Publicación de recursos.](publishing-dynamicmedia-assets.md)

   See [Publishing Viewer Presets](managing-viewer-presets.md#publishing-viewer-presets).

   See [Publishing Image Presets](managing-image-presets.md#publishing-image-presets).

1. En el carril izquierdo, seleccione el menú desplegable y toque **[!UICONTROL Visores]**.
1. En el carril izquierdo, toque un nombre de ajuste preestablecido de visor. El ajuste preestablecido de visor se aplica al recurso.
1. Toque **[!UICONTROL Incrustar]**.
1. En el cuadro de diálogo **[!UICONTROL Código]** incrustado, copie todo el código en el portapapeles y, a continuación, toque **[!UICONTROL Cerrar]**.
1. Pegue el código incrustado en las páginas web.

## Uso de HTTP/2 para distribuir los recursos de Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 es el nuevo protocolo web actualizado que mejora la forma en que se comunican los exploradores y los servidores. Proporciona una transferencia de información más rápida y reduce la cantidad de potencia de procesamiento necesaria. La entrega de recursos de Dynamic Media ahora puede realizarse a través de HTTP/2, lo que proporciona mejores tiempos de respuesta y carga.

Consulte Envío de contenido [](http2.md) HTTP2 para obtener información detallada sobre cómo empezar a utilizar HTTP/2 con su cuenta de Dynamic Media.
