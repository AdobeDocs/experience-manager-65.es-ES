---
title: Comercio AEM - Preparación para el RGPD
seo-title: Comercio AEM - Preparación para el RGPD
description: '"Comercio AEM - Preparación para el RGPD"'
seo-description: nulo
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# AEM Commerce - Preparación para el RGPD{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>El RGPD se utiliza como ejemplo en las secciones siguientes, pero los detalles cubiertos son aplicables a todas las normas de protección de datos y privacidad; como el RGPD, la CCPA, etc.

El Reglamento general de protección de datos de la Unión Europea sobre derechos de privacidad de datos entrará en vigor en mayo de 2018. Para obtener más información, consulte la página [RGPD en el Centro de privacidad de Adobe](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Consulte [AEM Preparación para el RGPD](/help/managing/data-protection-and-privacy.md) para obtener más información.

![screen_shot_2018-03-22at11606](assets/screen_shot_2018-03-22at111606.jpg)

En nuestras integraciones de Commerce integradas, AEM es la capa de experiencia, que consume servicios y envía datos de vuelta a la plataforma de comercio de clientes que se ejecuta en modo remoto.

En algunas plataformas de comercio, almacenamos información de perfil ( `/home/users`) y tokens de comercio (para iniciar sesión en la plataforma de comercio) en AEM. Para estos casos de uso, lea [Gestión de solicitudes de RGPD para la Plataforma AEM](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![screen_shot_2018-03-22at11621](assets/screen_shot_2018-03-22at111621.jpg)

## Gestión de solicitudes de RGPD para AEM comercio {#handling-gdpr-requests-for-aem-commerce}

Para la integración del Commerce Cloud de Salesforce, AEM Commerce no almacena ninguna información relevante del RGPD. Debe reenviar la solicitud a [Salesforce Cloud](https://documentation.demandware.com/).

Para las integraciones de hybris e IBM WebSphere, hay algunos datos en AEM. Debe utilizar las [AEM instrucciones del RGPD de la plataforma](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) y tener en cuenta estas preguntas:

1. **¿Dónde se almacenan o utilizan mis datos?** La información de perfil de usuario en caché, como nombre, identificador de usuario de comercio, token, contraseña, datos de dirección, etc., se muestra desde AEM.
1. **¿Con quién comparto los datos del RGPD cubiertos?** Cualquier actualización de los datos relevantes del RGPD en AEM comercio no se almacena (excepto la información de perfil relevante, como se mencionó anteriormente) sino que se reenvía como proxy a la plataforma de comercio.
1. **¿Cómo puedo eliminar mis datos** de usuario? Elimine el perfil de usuario en AEM e invoque la eliminación del usuario en la plataforma de comercio.

>[!NOTE]
>
>Consulte la [wiki de hybris](https://wiki.hybris.com/) o la [documentación de Websphere Commerce](https://www-01.ibm.com/support/docview.wss?uid=swg27036450) si es necesario.

