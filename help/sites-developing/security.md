---
title: Seguridad
seo-title: Seguridad
description: Inicios de seguridad de las aplicaciones durante la fase de desarrollo
seo-description: Inicios de seguridad de las aplicaciones durante la fase de desarrollo
uuid: efd5f3bc-da07-4fc8-a6ce-f1e6f5084c9e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: d2267663-6c1d-413c-9862-e82e21ae6906
translation-type: tm+mt
source-git-commit: ea4de28525ec4c2094e84d98aad6a518b03f011e
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---


# Seguridad{#security}

Inicios de seguridad de la aplicación durante la fase de desarrollo. Adobe recomienda aplicar las siguientes optimizaciones de seguridad.

## Usar sesión de solicitud {#use-request-session}

Siguiendo el principio de los menos privilegios, Adobe recomienda que cada acceso al repositorio se realice utilizando la sesión enlazada a la solicitud del usuario y el control de acceso adecuado.

## Protect contra scripts entre sitios (XSS) {#protect-against-cross-site-scripting-xss}

La secuencia de comandos entre sitios (XSS) permite a los atacantes insertar código en páginas web vistas por otros usuarios. Esta vulnerabilidad de seguridad puede ser aprovechada por usuarios web malintencionados para evitar controles de acceso.

AEM aplica el principio de filtrar todo el contenido proporcionado por el usuario durante la salida. La prevención de XSS recibe la máxima prioridad durante el desarrollo y las pruebas.

El mecanismo de protección XSS proporcionado por AEM se basa en la [biblioteca Java AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) proporcionada por [OWASP (proyecto de seguridad de Aplicación web abierta)](https://www.owasp.org/). La configuración predeterminada de AntiSamy se encuentra en

`/libs/cq/xssprotection/config.xml`

Es importante adaptar esta configuración a sus propias necesidades de seguridad mediante la superposición del archivo de configuración. La [documentación oficial de AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) le proporcionará toda la información que necesita para implementar sus requerimientos de seguridad.

>[!NOTE]
>
>Le recomendamos encarecidamente que siempre acceda a la API de protección XSS mediante el uso de [XSSAPI proporcionado por AEM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html).

Además, un firewall de aplicaciones web, como [mod_security para Apache](https://www.modsecurity.org), puede proporcionar un control central y confiable sobre la seguridad del entorno de implementación y protegerse contra ataques de scripts entre sitios no detectados anteriormente.

## Acceso a la información del Cloud Service {#access-to-cloud-service-information}

>[!NOTE]
>
>Las ACL para la información del Cloud Service, así como la configuración de OSGi necesaria para proteger su instancia, se automatizan como parte del [modo listo para la producción](/help/sites-administering/production-ready.md). Aunque esto significa que no necesita realizar los cambios de configuración manualmente, se recomienda revisarlos antes de empezar a implementar la implementación.

Cuando [integra la instancia de AEM con Adobe Marketing Cloud](/help/sites-administering/marketing-cloud.md), utiliza [configuraciones de Cloud Service](/help/sites-developing/extending-cloud-config.md). La información sobre estas configuraciones, junto con las estadísticas recopiladas, se almacenan en el repositorio. Recomendamos que, si utiliza esta funcionalidad, revise si la seguridad predeterminada de esta información coincide con sus necesidades.

El módulo webservicesupport escribe estadísticas e información de configuración en:

`/etc/cloudservices`

Con los permisos predeterminados:

* Entorno del autor: `read` para `contributors`

* Entorno de publicación: `read` para `everyone`

## Protect contra ataques de falsificación de solicitudes entre sitios {#protect-against-cross-site-request-forgery-attacks}

Para obtener más información sobre los mecanismos de seguridad AEM emplea para mitigar los ataques de CSRF, consulte la sección [Filtro de Remitente del reenvío Sling](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) de la lista de comprobación de seguridad y la [documentación del marco de protección de CSRF](/help/sites-developing/csrf-protection.md).