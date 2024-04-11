---
title: AEM Comercio de - Preparación para el RGPD
description: AEM Conozca los procedimientos para gestionar las solicitudes de RGPD en Commerce y cómo utilizarlas.
contentOwner: carlino
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
solution: Experience Manager, Experience Manager Sites
feature: Compliance
role: Admin, Architect, Developer, Leader, User, Data Architect, Data Engineer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# AEM Comercio de - Preparación para el RGPD{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>El RGPD se utiliza como ejemplo en las secciones siguientes, pero los detalles cubiertos son aplicables a todas las regulaciones de protección de datos y privacidad; como el RGPD y la CCPA.

El Reglamento General de Protección de Datos de la Unión Europea sobre los derechos de privacidad de datos entra en vigor en mayo de 2018. Consulte la [Página de RGPD en el Centro de privacidad de Adobe](https://business.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Consulte [AEM Preparación para el RGPD de](/help/managing/data-protection-and-privacy.md) para obtener más información.

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

Con las integraciones de Commerce AEM listas para usar de Adobe, se utiliza el nivel de experiencia, que consume servicios y devuelve datos a la plataforma de comercio del cliente que se ejecuta en un modo sin encabezado.

En algunas plataformas de comercio, Adobe almacena información de perfil ( `/home/users`AEM ) y tokens de comercio (para iniciar sesión en la plataforma de comercio) en la versión de. Para estos casos de uso, lea [AEM Gestión de solicitudes de RGPD para la plataforma de](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## AEM Gestión de solicitudes de RGPD para el uso de Commerce en la {#handling-gdpr-requests-for-aem-commerce}

Para la integración de Commerce Cloud AEM de Salesforce, Commerce no almacena ninguna información relevante para el RGPD. Reenviar la solicitud a [Salesforce Cloud](https://documentation.b2c.commercecloud.salesforce.com/DOC1/index.jsp).

Para las integraciones de Commerce AEM de hybris y HCL WebSphere®, hay algunos datos en el archivo de datos en el sitio de trabajo de la interfaz de usuario de la plataforma de datos de. Utilice el [AEM Instrucciones de RGPD de plataforma de](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) y considere estas preguntas:

1. **¿Dónde se almacenan o utilizan mis datos?** AEM Información de perfil de usuario en caché, como nombre, identificador de usuario de comercio, token, contraseña y datos de dirección, como se muestra a partir de la vista de datos de la página de inicio de sesión de.
1. **¿Con quién comparto los datos del RGPD cubiertos?** AEM Cualquier actualización de los datos relevantes del RGPD en Commerce no se almacena (excepto la información de perfil relevante, como se ha mencionado anteriormente), sino que se procesa como proxy de vuelta a la plataforma de comercio.
1. **Eliminar mis datos de usuario**? AEM Elimine el perfil de usuario en e invoque la eliminación de usuario en la plataforma de comercio.

>[!NOTE]
>
>Eche un vistazo a la [wiki de hybris](https://wiki.hybris.com/) o el [Documentación de HCL WebSphere® Commerce](https://help.hcltechsw.com/commerce/index.html), si es necesario.
