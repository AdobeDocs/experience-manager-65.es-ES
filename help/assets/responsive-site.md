---
title: Envío de imágenes optimizadas para un sitio interactivo
description: Cómo utilizar la función de código interactivo para distribuir imágenes optimizadas
uuid: 7c6baef5-7513-4644-94ed-2383e8724c17
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 5edcc765-c374-4368-a0d9-e02a713a24f2
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 12%

---


# Distribución de imágenes adaptables para un sitio interactivo {#delivering-optimized-images-for-a-responsive-site}

Utilice la función de código adaptable cuando desee compartir el código para la prestación de servicios interactivos con el desarrollador web. Copie el código interactivo (**[!UICONTROL RESS]**) en el portapapeles para poder compartirlo con el programador web.

Esta función tiene sentido si el sitio web está en un WCM de terceros. Sin embargo, si el sitio web está en AEM, un servidor de imágenes externo procesa la imagen y la suministra a la página web.

Consulte también [Incrustación del visor de vídeos en una página Web.](embed-code.md)

Consulte también [Vinculación de direcciones URL a la Aplicación web.](linking-urls-to-yourwebapplication.md)

**Para distribuir imágenes optimizadas para un sitio** interactivo:

1. Vaya a la imagen para la que desee proporcionar código interactivo y, en el menú desplegable, toque **[!UICONTROL Representaciones]**.

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. Seleccione un ajuste preestablecido de imagen interactivo. Aparecerán los botones **[!UICONTROL URL]** y **[!UICONTROL RESS]**.

   ![chlimage_1-409](assets/chlimage_1-208.png)

   >[!NOTE]
   >
   >El recurso seleccionado *y* el ajuste preestablecido de imagen o visualizador seleccionado deben publicarse para que los botones **[!UICONTROL URL]** o **[!UICONTROL RESS]** estén disponibles.
   >
   >Dynamic Media - El modo híbrido requiere que publique los ajustes preestablecidos de imagen; Dynamic Media: el modo Scene7 publica automáticamente ajustes preestablecidos de imagen.

1. Toque **[!UICONTROL RESS]**.

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. En el cuadro de diálogo **[!UICONTROL Incrustar imagen adaptable]**, seleccione y copie el texto del código interactivo y péguelo en el sitio Web para acceder al recurso interactivo.
1. Edite los puntos de interrupción predeterminados en el código incrustado para que coincidan con los del sitio web interactivo directamente en el código. Además, pruebe las distintas resoluciones de imagen que se proporcionan en diferentes puntos de interrupción de página.

## Uso de HTTP/2 para el envío de los recursos de Dynamic Media {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2 es el nuevo protocolo web actualizado que mejora la forma en que se comunican los exploradores y los servidores. Proporciona una transferencia de información más rápida y reduce la cantidad de potencia de procesamiento necesaria. El envío de recursos de Dynamic Media se admite mediante HTTP/2, que proporciona mejores tiempos de respuesta y carga.

Consulte [Envío HTTP2 de contenido](http2.md) para obtener información detallada sobre cómo empezar a utilizar HTTP/2 con su cuenta de Dynamic Media.
