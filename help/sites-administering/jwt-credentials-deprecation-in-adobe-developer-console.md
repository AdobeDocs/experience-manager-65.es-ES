---
title: Credenciales JWT de Adobe Developer Console en desuso
description: Obtenga información sobre el impacto de las credenciales de JWT en desuso en Adobe Developer Console en AEM.
exl-id: f19a92de-ba6a-4f6d-9e12-60ad1bad2e74
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: bb4367fa9916a8bafa6255562b2454ddae143351
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 73%

---

# Credenciales JWT de Adobe Developer Console en desuso {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
> AEM as a Cloud service debe hacer referencia a [este artículo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html) para obtener más información.

Los clientes de Adobe utilizan [Adobe Developer Console](https://developer.adobe.com/console) para generar credenciales que permitan el acceso a varias API. Los clientes seleccionan entre varios tipos de credenciales, que van de servidor a servidor OAuth a aplicaciones de una sola página. Uno de estos tipos de credenciales, las credenciales de cuenta de servicio (JWT), han quedado obsoletas y pasan a ser las credenciales de servidor a servidor de OAuth. Las credenciales de la nueva cuenta de servicio (JWT) no se pueden crear el 3 de junio de 2024 o después, y las credenciales de JWT existentes no funcionarán el 27 de enero de 2025 o después. Puede [obtener más información sobre el desuso](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

Este artículo proporciona contexto adicional sobre cómo los clientes de Adobe Experience Manager AEM () 6.5 deben gestionar el periodo de desuso.

AEM AEM La principal desventaja es que ahora admite las nuevas credenciales de servidor a servidor de OAuth para las credenciales de servidor a servidor de OAuth (OAuth Server-to-Server) que ahora son compatibles con las nuevas credenciales de los servidores de OAuth para la administración de la. Es posible que haya recibido un correo electrónico con instrucciones para migrar sus credenciales de JWT. Esta migración ya se puede realizar.

En las secciones siguientes se enumeran los escenarios en los que los clientes deben (o en algunos casos, no) reemplazar sus credenciales de cuenta de servicio (JWT) por credenciales de servidor a servidor de OAuth, ahora que AEM los admite. [Lea cómo](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) migrar las credenciales.

## Integración de AEM con otras soluciones de Adobe {#integrating-aem-with-other-adobe-solutions}

**Acción**: migre la configuración ahora que AEM admite las credenciales de OAuth.

**AEM Versiones relevantes de la**: Adobe Managed Services (Service Pack 21 y posterior).

AEM AEM Los clientes de utilizan la configuración de para configurar integraciones con todas las demás soluciones de Adobe de. Por ejemplo, Adobe Target y Adobe Analytics, entre otras.

![Integración de AEM con otras soluciones](/help/sites-administering/assets/jwt-deprecation.png)

Consulte [AEM Configuración de integraciones de IMS para la](/help/sites-administering/setting-up-ims-integrations-for-aem.md) para obtener más información sobre cómo:

* crear configuraciones con credenciales de OAuth.
* Migrar las configuraciones creadas con credenciales de JWT para utilizar las credenciales de OAuth.

## Las API de Cloud Manager {#cloud-manager-apis}

**Acción**: confirme cuándo se puede realizar la migración de JWT a las credenciales de OAuth.

**AEM Versiones relevantes de la**: Adobe Managed Services (Service Pack 21 y posterior).

Los clientes crean proyectos de Adobe Developer Console para que puedan invocar las [API de Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). Las credenciales del proyecto de Adobe Developer deben migrarse al tipo de credencial de servidor a servidor de OAuth, antes de que las credenciales de JWT caduquen en enero de 2025.
