---
title: Comercio AEM - Preparación para el RGPD
seo-title: AEM Commerce - GDPR Readiness
description: "Comercio AEM - Preparación para el RGPD"
seo-description: null
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
source-git-commit: 71842228dd3cb1ce3b79728912e8333d25fccefc
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---

# Comercio AEM - Preparación para el RGPD{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>El RGPD se utiliza como ejemplo en las secciones siguientes, pero los detalles cubiertos son aplicables a todas las normas de protección de datos y privacidad; como el RGPD y la CCPA.

El Reglamento general de protección de datos de la Unión Europea sobre derechos de privacidad de datos entrará en vigor en mayo de 2018. Consulte la [Página del RGPD en el Centro de privacidad de Adobe](https://business.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Consulte [Preparación AEM RGPD](/help/managing/data-protection-and-privacy.md) para obtener más información.

![screen_shot_2018-03-22at11606](assets/screen_shot_2018-03-22at111606.jpg)

Con las integraciones de comercio integradas de Adobe, AEM es la capa de experiencia, que consume servicios y envía datos de vuelta a la plataforma de comercio de clientes que se ejecuta en modo remoto.

En algunas plataformas comerciales, Adobe almacena información de perfil ( `/home/users`) y tokens de comercio (para iniciar sesión en la plataforma de comercio) en AEM. Para estos casos de uso, lea [Gestión de solicitudes de RGPD para la plataforma AEM](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![screen_shot_2018-03-22at11621](assets/screen_shot_2018-03-22at111621.jpg)

## Gestión de solicitudes de RGPD para AEM comercio {#handling-gdpr-requests-for-aem-commerce}

Para la integración del Commerce Cloud de Salesforce, AEM Commerce no almacena ninguna información relevante del RGPD. Reenviar la solicitud al [Salesforce Cloud](https://documentation.b2c.commercecloud.salesforce.com/DOC1/index.jsp).

Para las integraciones de hybris y HCL WebSphere® Commerce, hay algunos datos en AEM. Utilice la variable [Instrucciones del RGPD de AEM Platform](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) y considere estas preguntas:

1. **¿Dónde se almacenan o utilizan mis datos?** La información de perfil de usuario en caché, como el nombre, el identificador de usuario de comercio, el token, la contraseña y los datos de dirección, tal como se muestra en AEM.
1. **¿Con quién comparto los datos del RGPD cubiertos?** Cualquier actualización de los datos relevantes del RGPD en AEM Comercio no se almacena (excepto la información de perfil relevante, como se mencionó anteriormente) sino que se reenvía como proxy a la plataforma de comercio.
1. **Eliminar mis datos de usuario**? Elimine el perfil de usuario en AEM e invoque la eliminación del usuario en la plataforma de comercio.

>[!NOTE]
>
>Eche un vistazo a la [wiki hibris](https://wiki.hybris.com/) o [Documentación de HCL WebSphere® Commerce](https://help.hcltechsw.com/commerce/index.html), si es necesario.
