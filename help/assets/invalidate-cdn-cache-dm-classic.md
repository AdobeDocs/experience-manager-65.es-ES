---
title: Invalidación de la caché de la red de distribución de contenido mediante Dynamic Media Classic
description: La invalidación del contenido en caché de la red de distribución de contenido (CDN) le permite actualizar rápidamente los recursos que entrega Dynamic Media Classic, en lugar de esperar a que caduque la caché.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: CDN Cache,Dynamic Media Classic
role: User, Admin
exl-id: 7020343a-b556-4091-9717-93fcc55e623b
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 13%

---

# Invalidación de la caché de la red de distribución de contenido mediante Dynamic Media Classic {#invalidating-your-cdn-cached-content}

La CDN (red de distribución de contenido) almacena en caché los recursos de Dynamic Media para agilizar la entrega. Sin embargo, cuando realiza actualizaciones en un recurso, desea que los cambios surtan efecto inmediatamente. La invalidación del contenido en caché de la CDN le permite actualizar rápidamente los recursos que entrega Dynamic Media, en lugar de esperar a que la caché caduque.

>[!NOTE]
>
>Esta función requiere que utilice la CDN predeterminada que está integrada en Adobe Experience Manager Dynamic Media. Esta función no admite ninguna otra CDN personalizada.

>[!IMPORTANT]
>
>Los siguientes pasos se aplican únicamente a Dynamic Media en Adobe Experience Manager 6.5, Service Pack 5 (Experience Manager 6.5.5) o versiones anteriores.<br>Si utiliza Dynamic Media en Experience Manager 6.5, Service Pack 6 (Experience Manager 6.5.6) o posterior, siga los pasos que se encuentran en [Invalidación de la caché de CDN mediante Dynamic Media](/help/assets/invalidate-cdn-cache-dynamic-media.md).

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**Para invalidar la caché de la CDN mediante Dynamic Media Classic:**

1. Abra el [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html#system-requirements-dmc-app), luego inicie sesión en su cuenta.

   Las credenciales y el inicio de sesión se proporcionaron mediante el Adobe en el momento de la provisión. Si no dispone de esta información, póngase en contacto con el Servicio de atención al cliente de Adobe.

1. Cerca de la esquina superior derecha de la página, vaya a **[!UICONTROL Configurar]** > **[!UICONTROL Ajustes de aplicación]** > **[!UICONTROL Configuración general]**.
1. En la página Configuración general de la aplicación, en el encabezado del grupo Servidores, busque la variable **[!UICONTROL Plantilla de invalidación de CDN]** cuadro de texto.

1. Especifique la plantilla que se utiliza para invalidar la caché de la CDN (red de distribución de contenido).

   Por ejemplo, supongamos que introduce una URL de imagen (incluidos los ajustes preestablecidos o modificadores de imagen) que haga referencia a `<ID>`, en lugar de un ID de imagen específico, como en el siguiente ejemplo:

   `https://server.com/is/image/Company/<ID>?$product$`

   Si la plantilla solo contiene `<ID>`y luego Dynamic Media rellena `https://<server>/is/image` donde `<server>` es el nombre del servidor de publicación definido en Configuración general y &lt;id> son los recursos seleccionados para invalidar.

1. En la esquina inferior derecha de la página, seleccione **[!UICONTROL Cerrar]**.
1. En la interfaz de usuario de Dynamic Media Classic, seleccione uno o varios recursos y vaya a **[!UICONTROL Archivo]** > **[!UICONTROL Invalidar CDN]**. Verá una lista de una o más direcciones URL generadas a partir de la plantilla que creó y los recursos seleccionados. Utiliza la URL del servidor que aparece en &quot;Nombre de servidor publicado&quot; en la Configuración general de la aplicación.

   Por ejemplo, con la plantilla de invalidación de CDN establecida en el paso anterior, suponga que ha seleccionado una sola imagen de recurso de imagen denominada `Backpack_B`. Cuando vaya a **[!UICONTROL Archivo]** > **[!UICONTROL Invalidar CDN]**, genera la siguiente URL generada en la interfaz de usuario de invalidación de CDN:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. En el cuadro de lista Dirección URL, seleccione **[!UICONTROL Continuar]** para borrar la caché de cada URL específica. Puede editar una dirección URL o puede agregarla escribiéndola o pegándola en el cuadro de lista URL; no necesita establecer previamente una plantilla de invalidación de CDN.

   Después de seleccionar **[!UICONTROL Continuar]**, se muestra un indicador que proporciona una estimación de cuánto tiempo tardará en borrar la caché.

   Si seleccionó varios recursos y, a continuación, fue a **[!UICONTROL Archivo]** > **[!UICONTROL Invalidar CDN]**, se hace referencia a cada recurso en la lista guardada **[!UICONTROL URL de plantilla]**. Por lo tanto, puede definir un **[!UICONTROL Plantilla de invalidación de CDN]** hacer referencia a cada ajuste preestablecido de imagen URL al que se hace referencia en el sitio web (como detalles del producto y resultados de búsqueda). A continuación, al seleccionar una o varias imágenes para la invalidación desde la caché, las direcciones URL rellenan automáticamente la interfaz.

   >[!NOTE]
   >
   >Al seleccionar recursos y, a continuación, ir a **[!UICONTROL Archivo]** > **[!UICONTROL Invalidar CDN]**, Dynamic Media utiliza una plantilla de CDN no válida para crear automáticamente direcciones URL que se van a invalidar desde la red de distribución de contenido (CDN). Si no hay nada en el cuadro de texto **[!UICONTROL Plantilla de invalidación de CDN]**, aparecerá una lista de URL en blanco. El almacenamiento en caché en la CDN no está basado en recursos; se basa en la URL. Por lo tanto, es necesario conocer las direcciones URL completas que se encuentran en el sitio web. Después de establecer dichas direcciones URL, puede agregarlas al cuadro de texto **[!UICONTROL Invalidar plantilla CDN]** en los pasos anteriores. A continuación, puede seleccionar esos recursos e invalidar las direcciones URL en un solo paso.
   >
   >Otra opción es añadir direcciones URL completas a **[!UICONTROL Invalidar CDN]** lista. Si sigue este método, no es necesario seleccionar los recursos en Dynamic Media Classic antes de ir a **[!UICONTROL Archivo > Invalidar CDN]** opción.
