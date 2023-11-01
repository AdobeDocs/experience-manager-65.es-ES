---
title: Publicación de recursos de Dynamic Media
description: Obtenga información sobre cómo publicar recursos de Dynamic Media, como vídeos e imágenes, incluido el envío HTTP/2 de dichos recursos.
uuid: b1bee905-86cf-4284-8d4e-067e11557899
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 99d7025f-d022-4213-83c0-815a4712c573
role: User, Admin
exl-id: 750627fc-2a29-43ff-867e-55cb2e371043
feature: Publishing
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 4%

---

# Publicación de recursos de Dynamic Media {#publishing-dynamic-media-assets}

Para publicar los recursos de Dynamic Media, seleccione los que ya ha cargado y pulse **[!UICONTROL Publish]** o **[!UICONTROL Publicación rápida]**. Una vez publicados los recursos de Dynamic Media, estarán disponibles para su inclusión en una página web mediante una URL o incrustando el código en la página web.

También puede publicar al instante los recursos que carga, sin ninguna intervención del usuario. Consulte [Configuración de Dynamic Media: modo Scene7](config-dms7.md).
O bien, puede publicar recursos de forma selectiva en Dynamic Media o Adobe Experience Manager, mutuamente excluyentes, mediante **[!UICONTROL Publicación selectiva]** en el nivel de carpeta. Consulte [Trabajo con Publicación selectiva en Dynamic Media](/help/assets/selective-publishing.md).

En el **[!UICONTROL Vista de tarjeta]**, aparece un pequeño icono de globo terráqueo directamente debajo del nombre de un recurso y a la izquierda de la fecha y la hora para indicar que se ha publicado. En la **[!UICONTROL vista de lista]**, una columna **[!UICONTROL Publicada]** indica qué recursos se publican o cuáles no.

>[!NOTE]
>
>Si un recurso ya se ha publicado, utilice el Experience Manager para mover el recurso a otra carpeta y vuelva a publicar desde su nueva ubicación. La ubicación del recurso publicado original aún está disponible junto con el recurso recién republicado. Sin embargo, el recurso publicado original se &quot;pierde&quot; para el Experience Manager y no se puede cancelar su publicación. Por lo tanto, como práctica recomendada, cancele la publicación de los recursos primero antes de moverlos a una carpeta diferente.

Si tiene intención de publicar recursos de vídeo inmediatamente después de codificarlos, asegúrese de que la codificación está completada. Mientras se codifican los vídeos, el sistema le permite saber que hay un flujo de trabajo de procesamiento de vídeo en curso. Cuando se haya completado la codificación de vídeo, puede obtener una vista previa de las representaciones de vídeo. En ese punto, es seguro para usted publicar los vídeos sin incurrir en ningún error de publicación.

Consulte también [Vinculación de URL en la aplicación web](linking-urls-to-yourwebapplication.md).

Consulte también [Incrustar el visualizador de imágenes o vídeos de Dynamic Media en una página web](embed-code.md)

>[!NOTE]
>
>* Los recursos deben publicarse para utilizar la dirección URL. Si los recursos no se publican, no funcionará copiar y pegar la dirección URL en un explorador web.
>* Los ajustes preestablecidos de imagen y de visualizador se deben activar y publicar para la entrega en directo.
>

Para obtener información detallada sobre cómo publicar un conjunto o un recurso, consulte [Publicar recursos](manage-assets.md).

## Envío HTTP/2 de recursos de Dynamic Media {#http-delivery-of-dynamic-media-assets}

Experience Manager ahora admite la entrega de todo el contenido de Dynamic Media (imágenes y vídeo) a través de HTTP/2. Es decir, hay disponible una URL publicada o código incrustado para la imagen o el vídeo que se va a integrar con cualquier aplicación que acepte un recurso alojado. Ese recurso publicado se entrega mediante el protocolo HTTP/2. Este método de entrega mejora la forma en que los navegadores y servidores se comunican, lo que permite una mejor respuesta y tiempos de carga de todos los recursos de Dynamic Media.

Para obtener más información, consulte [Entrega HTTP/2 de contenido: preguntas más frecuentes](/help/sites-administering/scene7-http2faq.md).
