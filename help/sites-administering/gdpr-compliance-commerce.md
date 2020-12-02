---
title: Comercio AEM - Preparación para RGPD
seo-title: Comercio AEM - Preparación para RGPD
description: nulo
seo-description: nulo
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---


# Comercio AEM - Preparación para RGPD{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>El RGPD se utiliza como ejemplo en las secciones que figuran a continuación, pero los detalles abarcados son aplicables a todas las normas de protección de datos y privacidad; como el RGPD, la CCPA, etc.

El Reglamento general de protección de datos de la Unión Europea sobre derechos de privacidad de datos entrará en vigor en mayo de 2018. Para obtener más información, consulte la página [RGPD en el Centro de privacidad de Adobe](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Consulte [Preparación para el RGPD AEM](/help/managing/data-protection-and-privacy.md) para obtener más información.

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

En nuestras integraciones de comercio integradas, AEM es la capa de experiencia, que consume servicios y envía datos a la plataforma de comercio de clientes que se ejecuta en modo sin cabeza.

Para algunas plataformas comerciales, almacenamos información de perfil ( `/home/users`) y tokens de comercio (para iniciar sesión en la plataforma comercial) en AEM. Para estos casos de uso, lea [Gestión de las solicitudes del RGPD para la Plataforma de AEM](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## Gestión de solicitudes de RGPD para AEM comercio {#handling-gdpr-requests-for-aem-commerce}

Para la integración de Commerce Cloud de Salesforce, AEM Commerce no almacena ninguna información relevante del RGPD. Debe reenviar la solicitud a [Salesforce Cloud](https://documentation.demandware.com/).

Para las integraciones de hybris e IBM WebSphere, hay algunos datos en AEM. Debe utilizar las [instrucciones de RGPD de la Plataforma de AEM](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) y tener en cuenta estas preguntas:

1. **¿Dónde se almacenan o utilizan los datos?** La información de perfil del usuario en caché, como nombre, identificador de usuario de comercio, token, contraseña, datos de dirección, etc., se muestra desde AEM.
1. **¿Con quién comparto los datos del RGPD cubiertos?** No se almacena ninguna actualización de los datos pertinentes del RGPD en AEM comercio (excepto la información pertinente sobre perfiles, como se ha mencionado anteriormente), sino que se redirige a la plataforma comercial.
1. **¿Cómo eliminar mis datos** de usuario? Elimine el perfil del usuario en AEM e invoque la eliminación del usuario en la plataforma comercial.

>[!NOTE]
>
>Consulte la [wiki de híbris](https://wiki.hybris.com/) o la [documentación de comercio de la esfera web](https://www-01.ibm.com/support/docview.wss?uid=swg27036450) si es necesario.

