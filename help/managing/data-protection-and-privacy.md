---
title: 'Protección de datos y normativas de privacidad de datos: Preparación de Adobe Experience Manager'
seo-title: Normas de preparación para la protección de datos y privacidad de datos de Adobe Experience Manager; como el RGPD, la CCPA, etc.
description: 'Obtenga información sobre la compatibilidad de Adobe Experience Manager con las distintas normativas de protección de datos y privacidad de datos; incluido el Reglamento General de Protección de Datos de la UE (RGPD), la Ley de Protección de los Consumidores de California y la forma de cumplirlo al implementar un nuevo proyecto de AEM. '
seo-description: 'Obtenga información sobre la compatibilidad de Adobe Experience Manager con las distintas normativas de protección de datos y privacidad de datos; incluido el Reglamento General de Protección de Datos de la UE (RGPD), la Ley de Protección de los Consumidores de California y la forma de cumplirlo al implementar un nuevo proyecto de AEM. '
uuid: 9b0b8101-929c-4232-8c6e-1f9b8b2e0aa2
contentOwner: aheimoz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: grdp
discoiquuid: 0bcd7ac4-3071-466d-bd11-701f35ccf5bd
docset: aem65
translation-type: tm+mt
source-git-commit: 9b16c8ae2ee28c60f35f9e0f990d79173463c33b

---


# Preparación de Adobe Experience Manager para la protección de datos y normativas de privacidad de datos {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>El contenido de este documento no constituye asesoramiento jurídico y no se pretende sustituir al asesoramiento jurídico.
>
>Consulte con el departamento legal de su empresa para obtener asesoramiento acerca de las normas de protección de datos y privacidad de datos.

>[!NOTE]
>
>Para obtener más información sobre la respuesta de Adobe a los problemas de privacidad y lo que esto significa para usted como cliente de Adobe, consulte el Centro [de privacidad de](https://www.adobe.com/privacy.html)Adobe.

Adobe proporciona documentación y procedimientos (con API cuando están disponibles), para que el administrador de privacidad del cliente o el administrador de AEM puedan gestionar las solicitudes de protección de datos y privacidad de datos y ayudar a nuestros clientes a cumplir con estas normativas. Los procedimientos documentados permitirán a los clientes ejecutar las solicitudes reglamentarias manualmente o llamando a las API, cuando estén disponibles, desde un portal o servicio externo.

>[!CAUTION]
>
>Los detalles documentados aquí están restringidos a Adobe Experience Manager.
>
>Los datos de otro servicio a petición de Adobe, junto con las solicitudes de privacidad relacionadas, requerirán que se realicen acciones en ese servicio.
>
>Para obtener más información, consulte el Centro [de privacidad de](https://www.adobe.com/privacy.html)Adobe.

## Introducción {#introduction}

Las instancias de Adobe Experience Manager y las aplicaciones que se ejecutan en ellas son propiedad de nuestros clientes y son gestionadas por ellos.

En consecuencia, las regulaciones de protección de datos, como el RGPD, la CCPA y otras, son en gran medida responsabilidad de los clientes.

Como breve introducción, las regulaciones para la protección y la privacidad de los datos incluyen nuevas normas que deben ir seguidas de las funciones de:

* Entidades comerciales (CCPA) y/o controladores de datos (RGPD)

* Proveedores de servicios (CCPA) y/o procesadores de datos (RGPD)

Las principales disposiciones de esos reglamentos son las siguientes:

1. Definición ampliada de datos personales para incluir todos los ID únicos; como en datos identificables directa e indirectamente.

2. Reforzar los requisitos de consentimiento.

3. Se ha aumentado el enfoque en los derechos de eliminación (Eliminación de datos).

4. Exclusión de la venta de datos.

Para Adobe Experience Manager:

* Las instancias, y las aplicaciones que se ejecutan en ellas, son propiedad del cliente y son operadas por él.

   * Esto significa efectivamente que el cliente administra las funciones reglamentarias, incluidas las entidades comerciales y el proveedor de servicios, el controlador de datos y el procesador de datos, entre otras.

   * Adobe Experience Platform Privacy Service no formará parte del flujo de trabajo para AEM, como se ilustra en el diagrama siguiente.

* AEM incluye documentación y procedimientos para que el administrador de privacidad del cliente y/o el administrador de AEM ejecuten las solicitudes de regulación de privacidad; manualmente o a través de API, cuando esté disponible.

* No se ha agregado ningún servicio ni interfaz de usuario nuevos.

   * En su lugar, los procedimientos y las API están documentados para su uso por las UI/portales del cliente que gestionan solicitudes de regulación de privacidad.

* AEM no incluirá ninguna herramienta lista para usar para admitir el flujo de trabajo de las solicitudes de privacidad.

   * Adobe proporcionará documentación y procedimientos para el administrador de privacidad del cliente y/o el administrador de AEM, permitiéndoles ejecutar manualmente las solicitudes relacionadas con las normativas de privacidad.

Adobe proporciona procedimientos para gestionar solicitudes de privacidad relacionadas con Access, Delete y Opt-Out para Adobe Experience Manager. En algunos casos, hay API disponibles que se pueden llamar desde un portal desarrollado por el cliente o desde scripts para ayudar con la automatización.

El diagrama siguiente ilustra el aspecto que podría tener un flujo de trabajo de solicitud de privacidad (ilustrado con Adobe Experience Manager 6.5):

![Protección de datos y privacidad](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager y preparación normativa {#aem-and-regulatory-readiness}

Consulte las secciones siguientes para obtener documentación normativa sobre las áreas de producto de AEM.

## AEM Foundation {#aem-foundation}

Consulte [Gestión de solicitudes de privacidad y protección de datos para AEM Foundation](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

## Recopilación de estadísticas de uso agregadas de AEM {#aem-opting-into-aggregate-usage-statistics-collection}

Consulte Recopilación [de estadísticas de uso agregadas](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

## AEM Sites {#aem-sites}

Consulte Sitios [AEM: Protección de datos y preparación para la privacidad.](/help/sites-administering/gdpr-compliance-sites.md)

## AEM Commerce {#aem-commerce}

Consulte [AEM Commerce - Protección de datos y preparación para la privacidad](/help/sites-administering/gdpr-compliance-commerce.md).

## AEM Mobile {#aem-mobile}

Consulte [AEM Mobile - Protección de datos y preparación para la privacidad](/help/mobile/aem-mobile-gdpr-compliance.md).

## Integración de AEM con Adobe Target y Adobe Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Estas integraciones de Adobe Experience Manager se realizan con servicios preparados para la protección de datos y la privacidad (por ejemplo, GDPR o CCPA). No se almacenan datos personales de Adobe Target o Adobe Analytics en AEM en relación con las integraciones.
Para obtener más información, consulte:

* [Adobe Target: Información general de privacidad](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Flujo de trabajo de privacidad de datos de Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)

## AEM Communities {#aem-communities}

AEM Communities concede a los interesados el derecho a su portabilidad de datos, el derecho de acceso y el derecho a ser olvidados por medio de API [](/help/communities/user-ugc-management-service.md)integradas. Estas API permiten la eliminación masiva y la exportación masiva de contenido generado por el usuario, así como la desactivación de cuentas de usuario identificadas mediante sus ID autorizados. Sin embargo, la eliminación permanente de la cuenta de usuario es realizable mediante la eliminación del nodo de usuario en CRXDE Lite, que responde a la necesidad de una fácil exclusión del sistema.

Además, AEM Communities ofrece privacidad por diseño gracias a su consola de Moderación masiva, que permite a los miembros privilegiados buscar y eliminar las contribuciones y los detalles de los usuarios. La consola de administración Miembros permite limitar hasta el punto de prohibir un colaborador. Además, autoriza a los interesados a suprimir las contribuciones que hayan aportado.

## Formularios AEM {#aem-forms}

AEM Forms incluye componentes y flujos de trabajo que capturan, procesan y almacenan datos para orquestar procesos empresariales y completar transacciones digitales. Los diferentes componentes utilizan diferentes almacenes de datos y permiten la integración con los almacenes de datos personalizados. En la siguiente documentación se explican los procedimientos y las directrices para acceder a los datos de usuario y gestionarlos a fin de admitir los flujos de trabajo de protección de datos y privacidad (por ejemplo, RGPD o CCPA) de un componente.

* [Forms Portal](/help/forms/using/forms-portal-handling-user-data.md)
* [Administración de correspondencia](/help/forms/using/correspondence-management-handling-user-data.md)
* [Integración con Adobe Sign](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [Flujos de trabajo centrados en formularios en OSGi](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Flujos de trabajo](/help/forms/using/forms-workflow-jee-handling-user-data.md) de Forms JEE (solo AEM Forms JEE)
* [Document Security](/help/forms/using/document-security-handling-user-data.md) (solo JEE de AEM Forms)
* [Administración](/help/forms/using/user-management-handling-user-data.md) de usuarios (solo JEE de AEM Forms)
