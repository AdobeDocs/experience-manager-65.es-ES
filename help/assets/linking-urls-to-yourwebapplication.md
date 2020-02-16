---
title: Vinculación de URL en la aplicación web
description: Cómo vincular direcciones URL a la aplicación web en medios dinámicos
uuid: cf599e66-b1f9-40c0-b572-cea19f2e6793
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: d12e6ea3-aaf4-4672-9679-3c16c76d7d5b
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Vinculación de URL en la aplicación web {#linking-urls-to-your-web-application}

Los sitios web y las aplicaciones acceden a los servicios de Dynamic Media mediante llamadas mediante URL. Después de publicar un recurso, Dynamic Media activa una cadena URL que hace referencia al recurso. Puede pegar estas direcciones URL en un navegador web para realizar pruebas.

Solo puede vincular a direcciones URL si *no está* utilizando AEM como WCM. La vinculación frente a la incrustación se utiliza cuando se desea distribuir un reproductor de vídeo como ventana emergente o modal. Si está utilizando AEM como WCM, [agregue los recursos directamente en la página.](adding-dynamic-media-assets-to-pages.md)

Para colocar estas cadenas URL en las páginas web y las aplicaciones, cópielas desde Dynamic Media.

>[!NOTE]
>
>Las cadenas URL solo están disponibles para las representaciones dinámicas de recursos. Actualmente no están disponibles para recursos estáticos que residen en DAM y no en el servidor de medios dinámicos. El botón URL no aparece en las representaciones estáticas.

Consulte también [Incrustación del visor de imágenes o vídeos en una página web.](embed-code.md)

See also [Linking YouTube URLs to your Web Application.](video.md)

Consulte también [Envío de imágenes optimizadas para un sitio interactivo.](responsive-site.md)

See also [Uploading Assets.](managing-assets-touch-ui.md#uploading-assets)

## Obtención de una URL para un recurso {#obtaining-a-url-for-an-asset}

Puede obtener una cadena URL generada por un ajuste preestablecido de imagen o de visor. Después de copiar la URL, ésta se coloca en el portapapeles para que pueda pegarla según sea necesario en las páginas del sitio Web o la aplicación.

>[!NOTE]
>
>La URL no está disponible para copiarse hasta que haya publicado el recurso seleccionado. Además, también debe publicar el ajuste preestablecido de visor o el ajuste preestablecido de imagen.
>
>Consulte [Publicación de recursos](publishing-dynamicmedia-assets.md).
>
>See [Publishing Viewer Presets](managing-viewer-presets.md#publishing-viewer-presets).
>
>See [Publishing Image Presets](managing-image-presets.md#publishing-image-presets).

Existen varias formas de obtener una cadena URL. Sin embargo, los pasos a continuación muestran un solo método que puede utilizar.

**Para obtener una URL para un recurso**

1. Vaya al recurso *publicado* cuya URL de ajuste preestablecido de imagen o URL de ajuste preestablecido de visor desee copiar y toque el recurso para abrirlo.

   Recuerde que las direcciones URL solo están disponibles para copiarse *después* de *publicar* los recursos por primera vez. Además, también se debe publicar el ajuste preestablecido de visor o de imagen.

   Consulte [Publicación de recursos.](publishing-dynamicmedia-assets.md)

   See [Publishing Viewer Presets](managing-viewer-presets.md#publishing-viewer-presets).

   See [Publishing Image Presets](managing-image-presets.md#publishing-image-presets).

1. En función del recurso seleccionado, realice una de las siguientes acciones:

   * Si ha seleccionado una imagen, en el menú desplegable, toque **[!UICONTROL Representaciones]**.

      Bajo el encabezado **[!UICONTROL Dinámico]** , toque un nombre de ajuste preestablecido para ver su representación en el marco derecho. Es posible que tenga que desplazarse por la lista Representaciones para ver el encabezado Dinámico.

      En la parte inferior del carril izquierdo, toque **[!UICONTROL URL]**.

      ![chlimage_1-270](assets/chlimage_1-270.png)

   * Si ha seleccionado un conjunto de giros, un conjunto de imágenes, un conjunto de carrusel o un vídeo en el menú desplegable, toque **[!UICONTROL Visores]**.

      En el carril izquierdo, toque un nombre de ajuste preestablecido de visor. Se abre una vista previa del conjunto o vídeo en una página independiente.

      En el carril izquierdo, en la parte inferior, toque **[!UICONTROL URL]**.

      ![chlimage_1-271](assets/chlimage_1-271.png)

1. Seleccione y copie el texto en el navegador web para obtener una vista previa del recurso o agregarlo a la página de contenido web.

   Para salir de la ventana URL, toque la **[!UICONTROL X]** o **[!UICONTROL Cerrar]**.

## Obtención de una URL para un recurso estático {#obtaining-a-url-for-a-static-asset}

Dynamic Media admite la entrega de recursos estáticos, que son recursos adicionales que van más allá de las imágenes y el vídeo. Los formatos de recursos estáticos admitidos para la entrega son los siguientes:

* GIF animado
* Archivos de audio
* CSS
* JavaScript (cuando su empresa está configurada con su propio dominio)
* PDF
* SVG
* XML
* ZIP

**Para obtener una URL para un recurso estático**

1. Vaya al *recurso estático publicado cuya URL desea copiar y toque el recurso para abrirlo.

   Recuerde que las direcciones URL solo están disponibles para copiarse *después* de *publicar* el recurso estático por primera vez.

   Consulte [Publicación de recursos.](publishing-dynamicmedia-assets.md)

1. Utilice cualquiera de los siguientes métodos para obtener la URL del recurso estático publicado:

   * `The URL of the published static is the following:`

      * `https://*<server_name>*/is/content/*<company_name>*/*<static_asset_filename>*.*<extension>*`

         Por ejemplo, `https://aem.com/is/content/adobe/image.gif`.
   * haga clic en **[!UICONTROL Recurso > Representaciones]** dinámicas, toque una representación dinámica del recurso estático y copie la URL.

      Cambie la URL copiada para usarla `is/content` en la ruta en lugar de `is/image/`.


## Obtención de una URL de vídeo para una representación de vídeo publicada {#obtaining-a-video-url-for-a-published-video-rendition}

1. En AEM, vaya a **[!UICONTROL Herramientas > Implementación > Nube > Servicios]** de nube.
1. En la página Servicios **[!UICONTROL de]** nube, desplácese hacia abajo hasta el encabezado de Servicios **[!UICONTROL de]** Dynamic Media Cloud y, a continuación, toque **[!UICONTROL Mostrar configuraciones]**.
1. En Configuraciones **** disponibles, toque el nombre de la configuración que desee.

1. En la página Configuración **[!UICONTROL de]** Dynamic Media Cloud, en Dirección URL **[!UICONTROL del servicio]** de vídeo, copie toda la ruta URL. Necesitará la ruta de URL copiada más adelante en los pasos.

   Por ejemplo, la ruta de URL puede aparecer de forma similar a la siguiente:

   `https://s7athens.macromedia.com:9090/DMGateway/`

   (La ruta de acceso de arriba es sólo para fines ilustrativos; no es la ruta real que copia).

1. En ID **** de registro, copie el nombre del cliente que se encuentra en la última parte del ID.

   Por ejemplo, si el ID de registro fuera `87654321|MyCompany`, el nombre del cliente sería `MyCompany`.

1. Cerca de la esquina superior izquierda de la página, toque **[!UICONTROL Cloud Services**, toque el logotipo de Experience Manager y vaya a **[!UICONTROL General > CRXDE Lite]**.
1. Copie toda la ruta de representación de vídeo desde el JCR (repositorio de contenido de Java).

   Por ejemplo, la ruta de representación del vídeo puede tener un aspecto similar al siguiente:

   `/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112f/avs/Momentum_1080-0x720-2600k.mp4`

   (La ruta de acceso de arriba es sólo para fines ilustrativos; no es la ruta real que copia).

1. Organice la información copiada en el orden siguiente para formar una ruta de URL completa:

   `<Video_Service_URL>/public/<Customer_name_from_Registration_ID>/<Video_rendition_path>`

   Por ejemplo, si se utilizan las rutas de ejemplo y el nombre del cliente de ejemplo desde los pasos anteriores, la ruta completa aparece de la siguiente manera:

   `https://s7athens.macromedia.com:9090/DMGateway/public/MyCompany/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112ff/avs/Momentum_1080-0x720-2600k.mp4`

   Esta es la URL completa del vídeo para una representación de vídeo publicada.

## Obtención de una URL de vídeo para flujo continuo adaptable (HLS) {#obtaining-a-video-url-for-adaptive-streaming-hls}

1. En AEM, vaya a **[!UICONTROL Herramientas > Implementación > Nube > Servicios]** de nube.
1. En la página Servicios **[!UICONTROL de]** nube, desplácese hacia abajo hasta el encabezado de Servicios **[!UICONTROL de]** Dynamic Media Cloud y, a continuación, toque **[!UICONTROL Mostrar configuraciones]**.
1. En Configuraciones **** disponibles, toque el nombre de la configuración que desee.
1. En la página Configuración **[!UICONTROL de los servicios de]** Dynamic Media Cloud, haga lo siguiente:

   * En Dirección URL **[!UICONTROL del servicio]** de vídeo, copie la ruta de URL completa. Necesitará la ruta de URL copiada más adelante en estos pasos. Por ejemplo, la ruta de URL puede aparecer de forma similar a la siguiente:
   `https://gateway-na.assetsadobe.com/DMGateway/`

   (La ruta de acceso de arriba es sólo para fines ilustrativos; no es la ruta real que copia).

   * En ID **** de registro, copie el nombre del cliente que se encuentra en la última parte del ID. Necesitará el nombre de cliente copiado más adelante en estos pasos.

      Por ejemplo, si el ID de registro fuera `87654321|demoCo`, el nombre de cliente que copia será `demoCo`.


1. En función del protocolo de entrega de vídeo que utilice, copie el selector de protocolo correspondiente. Necesitará el selector de protocolo copiado más adelante en estos pasos.

   | Protocolo de envío de vídeo que utiliza | Selector de protocolo para usar |
   |---|---|
   | HTTP <br> Si utiliza HTTP (entrega de vídeo no segura), asegúrese de cambiar https a http en el valor de URL del servicio de vídeo que ha copiado anteriormente. | `public/` |
   | HTTPS | `public-ssl/` |

1. Copie la ruta completa del recurso de vídeo en AEM, tal como lo ha procesado Dynamic Media. Necesitará esta ruta de recursos de vídeo copiada más adelante en estos pasos.

   Por ejemplo:

   `/content/dam/marketing/MyVideo.mp4`

1. Combine todos los fragmentos copiados anteriormente para crear una cadena en el siguiente orden:

   &lt; `video service URL`>&lt; `protocol selector`>&lt; `customer name`>&lt; `video asset path`>

   Por ejemplo, si se utiliza la información copiada de los ejemplos de estos pasos, la cadena aparecerá de la siguiente manera:

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4`

1. Complete la dirección URL anexando `.m3u8` al final de la cadena. Por ejemplo, anexando `.m3u8` a la cadena del paso anterior, la ruta completa de la dirección URL aparecerá de la siguiente manera:

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4.m3u8`

## Uso de HTTP/2 para distribuir los recursos de Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 es el nuevo protocolo web actualizado que mejora la forma en que se comunican los exploradores y los servidores. Proporciona una transferencia de información más rápida y reduce la cantidad de potencia de procesamiento necesaria. La entrega de recursos de Dynamic Media ahora puede realizarse a través de HTTP/2, lo que proporciona mejores tiempos de respuesta y carga.

Consulte Envío de contenido [](http2.md) HTTP2 para obtener información detallada sobre cómo empezar a utilizar HTTP/2 con su cuenta de Dynamic Media.
