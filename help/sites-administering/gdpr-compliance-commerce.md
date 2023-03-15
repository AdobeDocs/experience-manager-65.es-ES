---
title: AEM Comercio de - Preparación para el RGPD
seo-title: AEM Commerce - GDPR Readiness
description: AEM "Comercio de - Preparación para el RGPD"
seo-description: null
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# AEM Comercio de - Preparación para el RGPD{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>El RGPD se utiliza como ejemplo en las secciones siguientes, pero los detalles cubiertos son aplicables a todas las regulaciones de protección de datos y privacidad; como el RGPD, la CCPA, etc.

El Reglamento General de Protección de Datos de la Unión Europea sobre los derechos de privacidad de datos entra en vigor en mayo de 2018. Para obtener más información, consulte la [Página de RGPD en el Centro de privacidad de Adobe](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Consulte [AEM Preparación para el RGPD de](/help/managing/data-protection-and-privacy.md) para obtener más información.

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

AEM En nuestras integraciones de Commerce listas para usar, se utiliza la capa de experiencia, que consume servicios y devuelve datos a la plataforma de comercio del cliente que se ejecuta en un modo sin encabezado.

Para algunas plataformas de comercio, almacenamos información de perfil ( `/home/users`AEM ) y tokens de comercio (para iniciar sesión en la plataforma de comercio) en la plataforma de. Para estos casos de uso, lea [AEM Gestión de solicitudes de RGPD para la plataforma de](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## AEM Gestión de solicitudes de RGPD para el comercio de {#handling-gdpr-requests-for-aem-commerce}

Para la integración de Commerce Cloud AEM de Salesforce, Comercio de la no almacena ninguna información relevante del RGPD. Debe reenviar la solicitud a [Salesforce Cloud](https://documentation.demandware.com/).

Para las integraciones de hybris y IBM AEM WebSphere, hay algunos datos en la interfaz de usuario de la interfaz de usuario de. Debe usar el [AEM Instrucciones de RGPD de plataforma de](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) y considere estas preguntas:

1. **¿Dónde se almacenan o utilizan mis datos?** AEM La información de perfil de usuario en caché, como nombre, identificador de usuario de comercio, token, contraseña, datos de dirección, etc., se muestra a partir de la vista de página de inicio de sesión de la página de usuario de.
1. **¿Con quién comparto los datos del RGPD cubiertos?** AEM Cualquier actualización de los datos relevantes del RGPD en Comercio de datos no se almacena (excepto la información de perfil relevante, como se ha mencionado anteriormente), sino que se procesa como proxy de vuelta a la plataforma de comercio.
1. **Eliminar mis datos de usuario**? AEM Elimine el perfil de usuario en e invoque la eliminación de usuario en la plataforma de comercio.

>[!NOTE]
>
>Eche un vistazo a la [wiki de hybris](https://wiki.hybris.com/) o el [Documentación de Websphere Commerce](https://www-01.ibm.com/support/docview.wss?uid=swg27036450) si es necesario.
