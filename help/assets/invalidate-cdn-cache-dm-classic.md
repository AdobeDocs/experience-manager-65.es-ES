---
title: Invalidación de la caché de CDN mediante Dynamic Media Classic
description: La invalidación del contenido en caché de CDN (Red de Envío de contenido) permite actualizar rápidamente los recursos que ofrece Dynamic Media Classic, en lugar de esperar a que caduque la caché.
uuid: 0fd88e31-9745-4c98-a245-9f5d0766cad4
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e6c9b50b-c27c-48bf-b3c0-9994e7bf6d7e
translation-type: tm+mt
source-git-commit: 10dae6e9f49e93d2f4923cee754c1d23d9d4b25e
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 24%

---


# Invalidación de la caché de CDN mediante Dynamic Media Classic {#invalidating-your-cdn-cached-content}

La CDN almacena en caché los recursos de Dynamic Media para un envío rápido. Sin embargo, cuando realice actualizaciones en un recurso, es posible que desee que esos cambios surtan efecto inmediatamente. La invalidación del contenido en caché de CDN (Red de Envío de contenido) permite actualizar rápidamente los recursos que se entregan mediante Dynamic Media, en lugar de esperar a que caduque la caché.

>[!IMPORTANT]
>
>Los pasos siguientes solo se aplican a Dynamic Media en AEM 6.5, Service Pack 5 (AEM 6.5.5) o versiones anteriores.<br>Si utiliza Dynamic Media en AEM 6.5, Service Pack 6 (AEM 6.5.6) o posterior, siga los pasos que se encuentran en  [Invalidación de la caché de CDN mediante Dynamic Media.](/help/assets/invalidate-cdn-cache-dynamic-media.md)

Consulte también [Descripción general de caché en Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Para invalidar la caché de CDN mediante Dynamic Media Classic:**

1. Realice una de las acciones siguientes:

   * En el navegador web, inicie sesión en su cuenta de Dynamic Media Classic:

      [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

      Adobe proporcionó las credenciales y el inicio de sesión en el momento del aprovisionamiento. Si no dispone de esta información, póngase en contacto con el servicio de asistencia técnica.

   * Abra la aplicación de Dynamic Media Classic e inicie sesión en su cuenta.

1. Cerca de la esquina superior derecha de la página, toque **[!UICONTROL Ajustes > Ajustes de aplicación > Configuración general.]**
1. En la página Configuración general de la aplicación, bajo el encabezado del grupo Servidores, busque el cuadro de texto **[!UICONTROL Plantilla de invalidación de CDN]**.

1. Especifique la plantilla que se utiliza para invalidar la caché de CDN (red de Envío de contenido).

   Por ejemplo, supongamos que introduce una URL de imagen (incluidos los ajustes preestablecidos de imagen o modificadores) que hace referencia a `<ID>`, en lugar de un ID de imagen específico como en el ejemplo siguiente:

   `https://server.com/is/image/Company/<ID>?$product$`

   Si la plantilla solo contiene `<ID>`, Dynamic Media rellena `https://<server>/is/image` donde `<server>` es el nombre del servidor de publicación definido en Configuración general y &lt;ID> es el recurso seleccionado para invalidarse.

1. En la esquina inferior derecha de la página, haga clic en **[!UICONTROL Cerrar.]**
1. En la interfaz de usuario de Dynamic Media Classic, seleccione uno o varios recursos y haga clic en **[!UICONTROL Archivo > Invalidar CDN.]** Verá una lista de una o varias direcciones URL generadas a partir de la plantilla creada y de los recursos seleccionados. Utiliza la URL del servidor que aparece en &quot;Nombre del servidor publicado&quot; en Configuración general de la aplicación.

   Por ejemplo, con la plantilla de invalidación de CDN definida en el paso anterior, supongamos que ha seleccionado una sola imagen de recurso de imagen con el nombre `Backpack_B`. Al hacer clic en **[!UICONTROL Archivo > Invalidar CDN]**, se genera la siguiente URL en la interfaz de usuario de Invalidación de CDN:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. En el cuadro lista de URL, haga clic en **[!UICONTROL Continuar]** para borrar la caché de cada dirección URL específica. Tenga en cuenta que puede editar una dirección URL o puede agregarla escribiéndola o pegándola en el cuadro de lista URL; no es necesario establecer la plantilla de invalidación de CDN de antemano.

   Después de hacer clic en **[!UICONTROL Continuar]**, se muestra un indicador que le proporciona una estimación del tiempo que tardará en borrarse la caché.

   Si seleccionó varios recursos y, a continuación, hizo clic en **[!UICONTROL Archivo > Invalidar CDN]**, se hace referencia a cada recurso en la **[!UICONTROL URL de plantilla guardada.]** Por lo tanto, puede definir una **[!UICONTROL plantilla de invalidación de CDN]** que haga referencia a cada ajuste preestablecido de imagen URL al que se hace referencia en el sitio web (como detalles del producto, resultados de búsqueda, etc.). A continuación, al seleccionar una o varias imágenes para la invalidación desde la caché, las direcciones URL rellenan automáticamente la interfaz.

   >[!NOTE]
   >
   >Al seleccionar recursos y, a continuación, hacer clic en **[!UICONTROL Archivo > Invalidar CDN]**, Dynamic Media utiliza una plantilla de CDN no válida para crear automáticamente direcciones URL que se van a invalidar desde la red de entrega de contenido (CDN). Si no hay nada en el cuadro de texto **[!UICONTROL Plantilla de invalidación de CDN]**, aparecerá una lista de URL en blanco. El almacenamiento en caché en la CDN no está basado en recursos; se basa en la URL. Por lo tanto, es necesario conocer las direcciones URL completas que se encuentran en el sitio web. Después de establecer dichas direcciones URL, puede agregarlas al cuadro de texto **[!UICONTROL Invalidar plantilla CDN]** en los pasos anteriores. A continuación, puede seleccionar esos recursos e invalidar las direcciones URL en un solo paso.
   >
   >Otra opción es agregar direcciones URL completas a la lista **[!UICONTROL Invalidar CDN]**. Si sigue este método, no es necesario seleccionar recursos en Dynamic Media Classic antes de ir a la opción **[!UICONTROL Archivo > Invalidar CDN]**.

