---
title: Invalidación de la caché de CDN mediante Dynamic Media
description: La invalidación del contenido en caché de CDN (Red de Envío de contenido) permite actualizar rápidamente los recursos que se entregan mediante Dynamic Media, en lugar de esperar a que caduque la caché.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
translation-type: tm+mt
source-git-commit: 9e67e252348f471c052f6c3e88aea61d7a309241
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 4%

---


# Invalidación de la caché de CDN mediante Dynamic Media {#invalidating-cdn-cache-for-dm-assets}

Los recursos de Dynamic Media se almacenan en caché en la red de Envío de contenido (CDN) para un envío rápido a sus clientes. Sin embargo, cuando actualice estos recursos, es posible que desee que los cambios surtan efecto inmediatamente en el sitio web. La depuración o invalidación de la caché de CDN permite actualizar rápidamente los recursos que se envían mediante Dynamic Media. En lugar de esperar a que la caché caduque con un valor TTL (tiempo de vida) (el valor predeterminado es 10 horas), puede enviar una solicitud desde Dynamic Media para que la caché caduque inmediatamente.

>[!IMPORTANT]
>
>Estos pasos solo se aplican al modo Dynamic Media - Scene7 en AEM 6.5, Service Pack 6 o posterior. <!-- If you are using Dynamic Media in AEM 6.5, Service Pack 5 or earlier [use the steps found here](/help/assets/invalidate-cdn-cache-dm-classic.md). -->

Consulte también Descripción general [del almacenamiento en caché en Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Para invalidar el contenido en caché de CDN de los recursos de Dynamic Media:**

1. En AEM 6.5.6 o posterior, toque **[!UICONTROL Herramientas > Recursos > Invalidación de CDN.]**

   ![Función de validación de CDN](/help/assets/assets-dm/cdn-invalidation-path.png)

1. En la página Invalidación de CDN, configure las opciones que desee:

   | Opción | Descripción |
   | --- | --- |
   | **[!UICONTROL Anular los ajustes preestablecidos de imagen asociados a activos en la CDN]** | Al marcar esta opción, puede seleccionar uno o varios recursos de Dynamic Media (independientemente del tipo MIME) y los ajustes preestablecidos de imagen asociados para la invalidación de caché.<br>Aunque puede seleccionar una o varias carpetas que contengan recursos, Adobe no recomienda este método. En su lugar, debe seleccionar archivos de recursos individuales.<br>Continúe con el paso siguiente. |
   | **[!UICONTROL Invalidación basada en plantilla]** | Al seleccionar esta opción, puede seleccionar los recursos de Dynamic Media y la plantilla de invalidación que ha creado anteriormente. Utilice esta opción con |
   | **[!UICONTROL Añadir recursos]** | Blah |
   | **[!UICONTROL Añadir URL]** | Agregue manualmente rutas de URL completas a los recursos de Dynamic Media cuya caché desee invalidar. |

1. 
1. Puntee **[!UICONTROL Siguiente.]**
1. 
