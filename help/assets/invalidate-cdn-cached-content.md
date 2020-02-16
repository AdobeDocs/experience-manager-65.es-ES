---
title: Invalidación del contenido en caché de CDN
description: La invalidación del contenido en caché de la CDN (Red de entrega de contenido) permite actualizar rápidamente los recursos que los medios dinámicos proporcionan, en lugar de esperar a que caduque la caché.
uuid: 0fd88e31-9745-4c98-a245-9f5d0766cad4
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e6c9b50b-c27c-48bf-b3c0-9994e7bf6d7e
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Invalidación del contenido en caché de CDN {#invalidating-your-cdn-cached-content}

La CDN almacena en caché los recursos de Dynamic Media para una entrega rápida. Sin embargo, cuando realice actualizaciones en un recurso, es posible que desee que esos cambios surtan efecto inmediatamente. La invalidación del contenido en caché de la CDN (Red de entrega de contenido) permite actualizar rápidamente los recursos que los medios dinámicos proporcionan, en lugar de esperar a que caduque la caché.

Consulte también Descripción general [de la caché en Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Para invalidar el contenido en caché de CDN:**

1. Inicie sesión en la cuenta de Dynamic Media Classic (Scene7):

   [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   Adobe proporcionó sus credenciales e inicio de sesión en el momento del aprovisionamiento. Si no dispone de esta información, póngase en contacto con el servicio de asistencia técnica.

1. Haga clic en **[!UICONTROL Ajustes > Ajustes de aplicación > Configuración]** general.
1. En la página Configuración general de la aplicación, en el encabezado del grupo Servidores, busque el cuadro de texto Plantilla **[!UICONTROL de invalidación de]** CDN.

1. Especifique la plantilla que se utiliza para invalidar la caché de CDN (Red de entrega de contenido).

   Por ejemplo, supongamos que introduce una URL de imagen (incluidos los ajustes preestablecidos de imagen o modificadores) que hace referencia a `<ID>`, en lugar de un ID de imagen específico como en el ejemplo siguiente:

   `https://server.com/is/image/Company/<ID>?$product$`

   Si la plantilla solo contiene `<ID>`, Dynamic Media rellena `https://<server>/is/image` donde `<server>` es el nombre del servidor de publicación definido en Configuración general y &lt;ID> es el recurso seleccionado para invalidarse.

1. En la esquina inferior derecha de la página, haga clic en **[!UICONTROL Cerrar]**.
1. En la interfaz de usuario de Dynamic Media Classic (Scene7), seleccione uno o varios recursos y, a continuación, haga clic en **[!UICONTROL Archivo > Invalidar CDN]**. Verá una lista de una o varias direcciones URL generadas a partir de la plantilla que ha creado y los recursos seleccionados. Utiliza la URL del servidor que aparece en &quot;Nombre del servidor publicado&quot; en Configuración general de la aplicación.

   Por ejemplo, con la plantilla de invalidación de CDN definida en el paso anterior, supongamos que ha seleccionado una sola imagen de recurso de imagen con el nombre `Backpack_B`. Al hacer clic en **[!UICONTROL Archivo > Invalidar CDN]** , se genera la siguiente URL en la interfaz de usuario de Invalidación de CDN:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. En el cuadro de lista URL, haga clic en **[!UICONTROL Continuar]** para borrar la caché de cada URL específica. Tenga en cuenta que puede editar una dirección URL o puede agregarla escribiéndola o pegándola en el cuadro de lista de direcciones URL; no es necesario establecer la plantilla de invalidación de CDN de antemano.

   Después de hacer clic en **[!UICONTROL Continuar]**, se muestra un indicador que le proporciona una estimación del tiempo que tardará en borrarse la caché.

   Si seleccionó varios recursos y, a continuación, hizo clic en **[!UICONTROL Archivo > Invalidar CDN]**, se hace referencia a cada recurso en la URL **[!UICONTROL de]** plantilla guardada. Por lo tanto, puede definir una plantilla **[!UICONTROL de invalidación de]** CDN que haga referencia a cada ajuste preestablecido de imagen URL al que se hace referencia en el sitio web (como detalles del producto, resultados de búsqueda, etc.). A continuación, al seleccionar una o varias imágenes para la invalidación desde la caché, las direcciones URL rellenan automáticamente la interfaz.

   >[!NOTE]
   >
   >Al seleccionar recursos y, a continuación, hacer clic en **[!UICONTROL Archivo > Invalidar CDN]**, Dynamic Media utiliza una plantilla de CDN no válida para crear automáticamente direcciones URL que se van a invalidar desde la red de entrega de contenido (CDN). Si no hay nada en el cuadro de texto Plantilla **[!UICONTROL de invalidación de]** CDN, aparecerá una lista de URL en blanco. El almacenamiento en caché en la CDN no está basado en recursos; se basa en URL. Por lo tanto, es necesario conocer las direcciones URL completas que se encuentran en el sitio web. Después de determinar dichas direcciones URL, puede agregarlas al cuadro de texto **[!UICONTROL Invalidar plantilla]** CDN anteriormente en los pasos. A continuación, puede seleccionar esos recursos e invalidar las direcciones URL en un solo paso.
   >
   >Otra opción es agregar direcciones URL completas a la lista **[!UICONTROL Invalidar CDN]** . Si sigue este método, no es necesario seleccionar recursos en Dynamic Media Classic antes de ir a la opción **[!UICONTROL Archivo > Invalidar CDN]** .

