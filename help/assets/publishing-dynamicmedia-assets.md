---
title: Publicación de Dynamic Media Assets
description: Cómo publicar recursos de medios dinámicos
uuid: b1bee905-86cf-4284-8d4e-067e11557899
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 99d7025f-d022-4213-83c0-815a4712c573
translation-type: tm+mt
source-git-commit: e916f70549197ac9f95443e972401a78735b0560
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 3%

---


# Publishing Dynamic Media Assets {#publishing-dynamic-media-assets}

Para publicar los recursos de Dynamic Media, seleccione los recursos que ya haya cargado y toque **[!UICONTROL Publicar]** o **[!UICONTROL Publicación rápida.]** Una vez publicados los recursos de Dynamic Media, estarán disponibles para incluirlos en una página web mediante una URL o incrustando el código en la página.

También puede publicar instantáneamente recursos que cargue, sin intervención del usuario. Consulte [Configuración de Dynamic Media: modo](config-dms7.md)Scene7.

En la Vista **[!UICONTROL de]** tarjeta, aparece un pequeño icono de globo terráqueo directamente debajo del nombre de un recurso y a la izquierda de la fecha y hora para indicar que se ha publicado. En la **[!UICONTROL vista de lista]**, una columna **[!UICONTROL Publicada]** indica qué recursos se publican o cuáles no.

>[!NOTE]
>
>Si ya se ha publicado un recurso, utilice AEM para moverlo a otra carpeta y volver a publicarlo desde su nueva ubicación, la ubicación original del recurso publicado seguirá estando disponible, junto con el recurso recién republicado. Sin embargo, el recurso publicado original se &quot;pierde&quot; en AEM y no se puede cancelar la publicación. Por lo tanto, se recomienda cancelar la publicación de los recursos antes de moverlos a una carpeta diferente.

Si tiene intención de publicar recursos de vídeo inmediatamente después de codificarlos, asegúrese de que la codificación está completa. Cuando se siguen codificando los vídeos, el sistema le permite saber que hay un flujo de trabajo de procesamiento de vídeo en curso. Cuando haya terminado la codificación de vídeo, debería poder realizar la previsualización de las representaciones de vídeo. En ese momento, puede publicar los vídeos sin incurrir en errores de publicación.

See also [Linking URLs to your Web Application](linking-urls-to-yourwebapplication.md).

See also [Embedding the Dynamic Media Video or Image viewer on a web page](embed-code.md)

>[!NOTE]
>
>* Los recursos deben publicarse para poder utilizar la dirección URL. Si no se publican los recursos, no funcionará copiar y pegar la URL en un explorador web.
>* Los ajustes preestablecidos de imagen y los ajustes preestablecidos de visor deben activarse y publicarse para el envío en directo.

>



Para obtener información detallada sobre la publicación de un conjunto o recurso, consulte [Publicación de recursos.](managing-assets-touch-ui.md)

## envío HTTP/2 de los recursos de Dynamic Media {#http-delivery-of-dynamic-media-assets}

AEM ahora admite el envío de todo el contenido de Dynamic Media (imágenes y vídeo) a través de HTTP/2. Es decir, una URL publicada o código incrustado para la imagen o el vídeo está disponible para integrarse con cualquier aplicación que acepte un recurso alojado. Ese recurso publicado se entrega a través del protocolo HTTP/2. Este método de envío mejora la forma en que se comunican los exploradores y los servidores, lo que permite una mejor respuesta y tiempos de carga de todos los recursos de Dynamic Media.

Consulte el envío [HTTP/2 del contenido de las preguntas](/help/sites-administering/scene7-http2faq.md) más frecuentes para obtener más información.
