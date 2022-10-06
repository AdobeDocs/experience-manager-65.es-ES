---
title: Publicación de recursos de Dynamic Media
description: Cómo publicar recursos de Dynamic Media
uuid: b1bee905-86cf-4284-8d4e-067e11557899
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 99d7025f-d022-4213-83c0-815a4712c573
role: User, Admin
exl-id: 750627fc-2a29-43ff-867e-55cb2e371043
feature: Publishing
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 4%

---

# Publicación de recursos de Dynamic Media {#publishing-dynamic-media-assets}

Para publicar los recursos de Dynamic Media, seleccione los que ya ha cargado y pulse **[!UICONTROL Publicación]** o **[!UICONTROL Publicación rápida]**. Una vez publicados los recursos de Dynamic Media, quedan disponibles para su inclusión en una página web mediante una URL o incrustando el código en la página.

También puede publicar recursos instantáneamente que cargue, sin intervención del usuario. Consulte [Configuración de Dynamic Media: modo Scene7](config-dms7.md).
O bien, puede publicar selectivamente recursos en Dynamic Media o Adobe Experience Manager, mutuamente excluyentes entre sí, utilizando **[!UICONTROL Publicación selectiva]** en el nivel de carpeta. Consulte [Trabajar con publicación selectiva en Dynamic Media](/help/assets/selective-publishing.md).

En el **[!UICONTROL Vista de tarjeta]**, aparece un pequeño icono de globo terráqueo directamente debajo del nombre de un recurso y a la izquierda de la fecha y la hora para indicar que se ha publicado. En la **[!UICONTROL vista de lista]**, una columna **[!UICONTROL Publicada]** indica qué recursos se publican o cuáles no.

>[!NOTE]
>
>Si ya se ha publicado un recurso, utilice Experience Manager para moverlo a otra carpeta y vuelva a publicar desde su nueva ubicación. La ubicación del recurso publicado originalmente aún está disponible, junto con el recurso recién republicado. Sin embargo, el recurso publicado original se &quot;pierde&quot; para el Experience Manager y no se puede cancelar su publicación. Por lo tanto, se recomienda cancelar la publicación de los recursos primero antes de moverlos a una carpeta diferente.

Si tiene intención de publicar recursos de vídeo inmediatamente después de codificarlos, asegúrese de que la codificación esté completa. Mientras se codifican los vídeos, el sistema le permite saber que hay un flujo de trabajo de procesamiento de vídeo en curso. Cuando haya terminado la codificación de vídeo, puede obtener una vista previa de las representaciones de vídeo. En este punto, es seguro que publique los vídeos sin incurrir en errores de publicación.

Consulte también [Vincular URL a la aplicación web](linking-urls-to-yourwebapplication.md).

Consulte también [Incrustar el visualizador de imágenes o vídeo de Dynamic Media en una página web](embed-code.md)

>[!NOTE]
>
>* Los recursos deben publicarse para poder utilizar la dirección URL. Si los recursos no se publican, copiar y pegar la URL en un explorador web no funciona.
>* Los ajustes preestablecidos de imagen y los ajustes preestablecidos de visualizador deben activarse y publicarse para que se puedan publicar en directo.
>


Para obtener información detallada sobre la publicación de un conjunto o un recurso, consulte [Publicar recursos](manage-assets.md).

## Entrega HTTP/2 de recursos de Dynamic Media {#http-delivery-of-dynamic-media-assets}

Ahora, el Experience Manager admite la entrega de todo el contenido de Dynamic Media (imágenes y vídeo) a través de HTTP/2. Es decir, una URL publicada o un código incrustado para la imagen o el vídeo están disponibles para integrarse con cualquier aplicación que acepte un recurso alojado. Ese recurso publicado se entrega mediante el protocolo HTTP/2. Este método de envío mejora la forma en que se comunican los exploradores y los servidores, lo que permite mejorar los tiempos de respuesta y carga de todos los recursos de Dynamic Media.

Para obtener más información, consulte [Entrega HTTP/2 de contenido preguntas más frecuentes](/help/sites-administering/scene7-http2faq.md).
