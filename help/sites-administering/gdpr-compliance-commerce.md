---
title: 'Comercio AEM: preparación para RGPD'
seo-title: 'Comercio AEM: preparación para RGPD'
description: nulo
seo-description: nulo
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780

---


# Comercio AEM: preparación para RGPD{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>El RGPD se utiliza como ejemplo en las secciones que figuran a continuación, pero los detalles abarcados son aplicables a todas las normas de protección de datos y privacidad; como el RGPD, la CCPA, etc.

El Reglamento general de protección de datos de la Unión Europea sobre derechos de privacidad de datos entrará en vigor en mayo de 2018. Para obtener más información, consulte la página del [RGPD en el Centro](https://www.adobe.com/privacy/general-data-protection-regulation.html)de privacidad de Adobe.

>[!NOTE]
>
>Consulte Preparación para [AEM GDPR](/help/managing/data-protection-and-privacy.md) para obtener más información.

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

En nuestras integraciones de comercio integradas, AEM es la capa de experiencia que consume servicios y envía datos a la plataforma de comercio de clientes que se ejecuta en modo sin cabeza.

Para algunas plataformas comerciales, almacenamos información de perfil ( `/home/users`) y tokens de comercio (para iniciar sesión en la plataforma de comercio) en AEM. Para estos casos de uso, lea [Gestión de solicitudes de RGPD para la plataforma](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)AEM.

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## Gestión de solicitudes GDPR para AEM Commerce {#handling-gdpr-requests-for-aem-commerce}

Para la integración de Salesforce Commerce Cloud, AEM Commerce no almacena ninguna información relevante del RGPD. Debe reenviar la solicitud a [Salesforce Cloud](https://documentation.demandware.com/).

Para las integraciones hybris e IBM WebSphere, hay algunos datos en AEM. Debe utilizar las instrucciones [del RGPD de la plataforma](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) AEM y tener en cuenta estas preguntas:

1. **¿Dónde se almacenan o utilizan los datos?** La información de perfil de usuario en caché, como nombre, identificador de usuario de comercio, token, contraseña, datos de dirección, etc., se muestra desde AEM.
1. **¿Con quién comparto los datos del RGPD cubiertos?** No se almacena ninguna actualización de los datos relevantes del RGPD en AEM Commerce (excepto la información de perfil relevante, como se mencionó anteriormente), sino que se reenvía como proxy a la plataforma de comercio.
1. **¿Cómo eliminar mis datos** de usuario? Elimine el perfil de usuario en AEM e invoque la eliminación del usuario en la plataforma de comercio.

>[!NOTE]
>
>Eche un vistazo a la [wiki](https://wiki.hybris.com/) de híbris o a la documentación [de comercio de la](https://www-01.ibm.com/support/docview.wss?uid=swg27036450) esfera web si es necesario.

