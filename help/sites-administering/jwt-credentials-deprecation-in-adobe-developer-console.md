---
title: Credenciales JWT de Adobe Developer Console en desuso
description: Obtenga información sobre el impacto de las credenciales de JWT en desuso en Adobe Developer Console en AEM.
source-git-commit: 72974d27fecbd9c242f66e203b02463c22b93108
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 80%

---


# Credenciales JWT de Adobe Developer Console en desuso {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
> AEM as a Cloud service debe hacer referencia a [este artículo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html) para obtener más información.

Los clientes de Adobe utilizan [Adobe Developer Console](https://developer.adobe.com/console) para generar credenciales que permitan el acceso a varias API. Los clientes seleccionan entre varios tipos de credenciales, que van de servidor a servidor OAuth a aplicaciones de una sola página. Uno de estos tipos de credenciales, las credenciales de cuenta de servicio (JWT), han quedado obsoletas y pasan a ser las credenciales de servidor a servidor de OAuth. Las credenciales de nueva cuenta de servicio (JWT) no se pueden crear el 1 de mayo de 2024 o después, y las credenciales de JWT existentes no funcionarán el 1 de enero de 2025 o después. Puede [obtener más información sobre el desuso](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

AEM Este artículo proporciona contexto adicional acerca de cómo los clientes de la versión 6.5 de deben gestionar el periodo de desuso.

Lo más importante en este momento es que las características de la aplicación aún no son compatibles con las nuevas credenciales de servidor a servidor OAuth. AEM La compatibilidad llegará pronto: a mediados de abril de 2024, mediante un paquete de compatibilidad especial para instalar para 6.5, si ejecuta el último Service Pack 20 o inferior (el Service Pack 21 y superior lo incluirá automáticamente). Es posible que haya recibido un correo electrónico con instrucciones para migrar sus credenciales de JWT, pero asegúrese de que puede y debe aplazar la migración de credenciales hasta que AEM admita el nuevo tipo de credencial de servidor OAuth.

En las secciones siguientes se enumeran los escenarios en los que los clientes deben reemplazar (o en algunos casos no) sus credenciales de cuenta de servicio (JWT) por credenciales de servidor a servidor OAuth, una vez que los clientes las admitan a mediados de abril. [Averigüe cómo](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) reemplazar las credenciales en el futuro.

## Integración de AEM con otras soluciones de Adobe {#integrating-aem-with-other-adobe-solutions}

**Acción**: espere para migrar hasta después de mediados de abril de 2024, cuando AEM lo admita.

**AEM Versiones relevantes de la**: Adobe Managed Services (Service Pack 20 y posteriores).


Los clientes de AEM utilizan la interfaz de usuario de Autor de AEM para configurar integraciones con todas las demás soluciones de Adobe. Por ejemplo, Adobe Target, Adobe Analytics, Adobe Launch, AFCS y muchos más.

![Integración de AEM con otras soluciones](/help/sites-administering/assets/jwt-deprecation.png)

A modo de ejemplo, estas son [las instrucciones](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=es) para configurar la integración con Adobe Target. La clave API en la sección [Finalización de la configuración de IMS en AEM](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=es#completing-the-ims-configuration-in-aem) debe migrarse al tipo de credencial de servidor a servidor OAuth, cuando AEM admita estas credenciales a mediados de abril. Estas instrucciones se actualizarán y revisarán a mediados de abril para ayudarle a aplicar las nuevas credenciales de servidor a servidor OAuth.

## API de Cloud Manager {#cloud-manager-apis}

**Acción**: espere para migrar hasta después de mediados de abril de 2024, cuando AEM lo admita.

**AEM Versiones relevantes de la**: Adobe Managed Services (Service Pack 20 y posteriores).

Los clientes crean proyectos de Adobe Developer Console para que puedan invocar las [API de Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). Las credenciales del proyecto de Adobe Developer deben migrarse al tipo de credencial de servidor a servidor OAuth, una vez que AEM y Cloud Manager las admita.
