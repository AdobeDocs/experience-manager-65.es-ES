---
title: 'Reglamentos de protección de datos y privacidad de datos: preparación para Adobe Experience Manager'
seo-title: Adobe Experience Manager Readiness for Data Protection and Data Privacy Regulations; such as GDPR, CCPA, etc
description: Obtenga información sobre la compatibilidad de Adobe Experience Manager con las distintas normas de protección de datos y privacidad de datos; incluido el Reglamento general de protección de datos (RGPD) de la UE, la Ley de Privacidad del Consumidor de California y cómo cumplir al implementar un nuevo proyecto AEM.
seo-description: Learn about Adobe Experience Manager support for the various Data Protection and Data Privacy Regulations; including the EU General Data Protection Regulation (GDPR), the California Consumer Privacy Act and how to comply when implementing a new AEM project.
uuid: 9b0b8101-929c-4232-8c6e-1f9b8b2e0aa2
contentOwner: aheimoz
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
discoiquuid: 0bcd7ac4-3071-466d-bd11-701f35ccf5bd
docset: aem65
exl-id: 46c1ca14-78f6-4b33-9fdf-1b90a9875f66
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 58%

---

# Preparación de Adobe Experience Manager para la protección de datos y las normas de privacidad de datos {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>El contenido de este documento no constituye asesoramiento jurídico y no está pensado para sustituirlo.
>
>Consulte con el departamento legal de su empresa para obtener asesoramiento sobre los reglamentos de protección de datos y privacidad de datos.

>[!NOTE]
>
>Para obtener más información acerca de la respuesta de Adobe a los problemas de privacidad y lo que esto supone para usted como cliente de Adobe, consulte el [Centro de privacidad de Adobe](https://www.adobe.com/es/privacy.html).

Adobe proporciona documentación y procedimientos (con API cuando están disponibles), para que el administrador de privacidad del cliente o el administrador de AEM gestione las solicitudes de protección de datos y privacidad de datos y ayude a nuestros clientes a cumplir con estas regulaciones. Los procedimientos documentados permitirán a los clientes ejecutar las solicitudes reglamentarias manualmente o llamando a las API, si están disponibles, desde un portal o servicio externo.

>[!CAUTION]
>
>Los detalles documentados aquí están restringidos a Adobe Experience Manager.
>
>Los datos de otro servicio bajo demanda de Adobe, junto con cualquier solicitud de privacidad relacionada, requerirán que se realicen acciones en ese servicio.
>
>Para obtener más información, consulte el [Centro de privacidad de Adobe](https://www.adobe.com/privacy.html).

## Introducción {#introduction}

Las instancias de Adobe Experience Manager, y las aplicaciones que se ejecutan en ellas, son propiedad de nuestros clientes y son operadas por ellos.

Como consecuencia, las regulaciones de protección de datos, como el RGPD, la CCPA y otras, son en gran medida responsabilidad de los clientes.

Como introducción muy breve, las regulaciones para la privacidad y protección de datos incluyen nuevas reglas a las que deben seguir las funciones de:

* Entidades comerciales (CCPA) y/o controladores de datos (RGPD)

* Proveedores de servicios (CCPA) o procesadores de datos (RGPD)

Las principales disposiciones de esos reglamentos son las siguientes:

1. Definición ampliada de datos personales para incluir todos los ID únicos; como en datos directa e indirectamente identificables.

2. Fortalecimiento de los requisitos de consentimiento.

3. Mayor enfoque a los derechos de eliminación (eliminación de datos).

4. Exclusión de la venta de datos.

Para Adobe Experience Manager:

* Las instancias, y las aplicaciones que se ejecutan en ellas, son propiedad del cliente y las gestiona.

   * Esto significa que el cliente gestiona las funciones regulatorias, incluidas las entidades del negocio y el proveedor de servicios, el controlador de datos y el procesador de datos, entre otras.

   * Adobe Experience Platform Privacy Service no formará parte del flujo de trabajo para AEM, como se ilustra en el diagrama siguiente.

* AEM incluye documentación y procedimientos para el administrador de privacidad del cliente o el administrador de AEM para ejecutar las solicitudes de regulación de privacidad; manualmente o a través de API, cuando esté disponible.

* No se ha agregado ningún servicio ni interfaz de usuario nuevos.

   * En su lugar, los procedimientos y las API están documentados para su uso por las IU o portales de los clientes que administran solicitudes de regulación de la privacidad.

* AEM no incluirá ninguna herramienta predeterminada para admitir el flujo de trabajo de solicitudes de privacidad.

   * Adobe proporcionará documentación y procedimientos para el administrador de privacidad o AEM del cliente, lo que les permitirá ejecutar manualmente las solicitudes relacionadas con las normas de privacidad.

Adobe proporciona procedimientos para gestionar solicitudes de privacidad relacionadas con acceso, eliminación y exclusión para Adobe Experience Manager. En algunos casos, hay API disponibles a las que se puede llamar desde un portal o scripts desarrollados por el cliente para ayudar con la automatización.

El diagrama siguiente ilustra el aspecto que podría tener un flujo de trabajo de solicitud de privacidad (ilustrado con Adobe Experience Manager 6.5):

![Protección de datos y privacidad](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager y preparación regulatoria {#aem-and-regulatory-readiness}

Consulte las secciones siguientes para obtener documentación reglamentaria sobre las áreas de producto de AEM.

## AEM Foundation {#aem-foundation}

Consulte [Gestión de solicitudes de privacidad y protección de datos para la base de AEM](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

## AEM de la recopilación de estadísticas de uso agregadas {#aem-opting-into-aggregate-usage-statistics-collection}

Consulte [Recopilación de estadísticas de uso agregadas](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

## AEM Sites {#aem-sites}

Consulte [AEM Sites: Protección de datos y preparación para la privacidad.](/help/sites-administering/gdpr-compliance-sites.md)

## AEM Commerce {#aem-commerce}

Consulte [AEM Commerce: Protección de datos y preparación para la privacidad](/help/sites-administering/gdpr-compliance-commerce.md).

## AEM Mobile {#aem-mobile}

Consulte [AEM Mobile: Protección de datos y preparación para la privacidad](/help/mobile/aem-mobile-gdpr-compliance.md).

## Integración AEM con Adobe Target y Adobe Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Estas integraciones de Adobe Experience Manager se basan en servicios preparados para la protección de datos y la privacidad (por ejemplo, RGPD o CCPA). No se almacenan datos personales de Adobe Target o Adobe Analytics en AEM en relación con las integraciones.
Para obtener más información, consulte:

* [Adobe Target: Información general de privacidad](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Flujo de trabajo de privacidad de datos de Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)

## AEM Communities {#aem-communities}

AEM Communities otorga a los interesados el derecho a su portabilidad de datos, el derecho de acceso y el derecho a ser olvidados mediante [API integradas](/help/communities/user-ugc-management-service.md). Estas API permiten la eliminación masiva y la exportación masiva de contenido generado por el usuario, y desactivan las cuentas de usuario identificadas mediante sus ID autorizables. Sin embargo, es posible eliminar permanentemente la cuenta de usuario eliminando el nodo de usuario en el CRXDE Lite, lo que responde a la necesidad de una exclusión sencilla del sistema.

Además, AEM Communities ofrece privacidad por diseño gracias a su consola de moderación masiva, que permite a los miembros privilegiados encontrar y eliminar las contribuciones y los detalles de los usuarios. La consola de administración de miembros permite limitar hasta el punto de prohibir un colaborador. Además, autoriza a los interesados a eliminar las contribuciones que hayan escrito.

## AEM Forms {#aem-forms}

AEM Forms incluye componentes y flujos de trabajo que capturan, procesan y almacenan datos para organizar procesos empresariales y transacciones digitales completas. Los distintos componentes utilizan diferentes almacenes de datos y permiten la integración con almacenes de datos personalizados. En la siguiente documentación se explican los procedimientos y las directrices para acceder y gestionar los datos de usuario con el fin de admitir los flujos de trabajo de protección de datos y privacidad (por ejemplo, RGPD o CCPA) de un componente.

* [Forms Portal](/help/forms/using/forms-portal-handling-user-data.md)
* [Administración de correspondencia](/help/forms/using/correspondence-management-handling-user-data.md)
* [Integración con Adobe Sign](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [Flujos de trabajo centrados en Forms en OSGi](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Flujos de trabajo de Forms JEE](/help/forms/using/forms-workflow-jee-handling-user-data.md) (solo AEM Forms JEE)
* [Seguridad de los documentos](/help/forms/using/document-security-handling-user-data.md) (solo AEM Forms JEE)
* [Administración de usuarios](/help/forms/using/user-management-handling-user-data.md) (solo AEM Forms JEE)
