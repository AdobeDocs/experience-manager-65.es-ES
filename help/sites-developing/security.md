---
title: Seguridad
seo-title: Seguridad
description: La seguridad de la aplicación se inicia durante la fase de desarrollo
seo-description: La seguridad de la aplicación se inicia durante la fase de desarrollo
uuid: efd5f3bc-da07-4fc8-a6ce-f1e6f5084c9e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: d2267663-6c1d-413c-9862-e82e21ae6906
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Seguridad{#security}

La seguridad de la aplicación se inicia durante la fase de desarrollo. Adobe recomienda aplicar las siguientes optimizaciones de seguridad.

## Usar sesión de solicitud {#use-request-session}

Siguiendo el principio de privilegios de cliente, Adobe recomienda que cada acceso al repositorio se realice utilizando la sesión vinculada a la solicitud del usuario y el control de acceso adecuado.

## Proteger contra secuencias de comandos entre sitios (XSS) {#protect-against-cross-site-scripting-xss}

La secuencia de comandos entre sitios (XSS) permite a los atacantes insertar código en páginas web vistas por otros usuarios. Esta vulnerabilidad de seguridad puede ser aprovechada por usuarios web malintencionados para evitar los controles de acceso.

AEM aplica el principio de filtrar todo el contenido proporcionado por el usuario durante la salida. La prevención de XSS recibe la máxima prioridad durante el desarrollo y las pruebas.

El mecanismo de protección XSS proporcionado por AEM se basa en la biblioteca [Java](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) AntiSamy proporcionada por [OWASP (proyecto de seguridad de la aplicación web abierta)](https://www.owasp.org/). La configuración predeterminada de AntiSamy se encuentra en

`/libs/cq/xssprotection/config.xml`

Es importante adaptar esta configuración a sus propias necesidades de seguridad mediante la superposición del archivo de configuración. La documentación [oficial de](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) AntiSamy le proporcionará toda la información necesaria para implementar sus requisitos de seguridad.

>[!NOTE]
>
>Le recomendamos encarecidamente que siempre acceda a la API de protección XSS mediante el uso de [XSSAPI proporcionado por AEM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html).

Además, un servidor de seguridad de aplicaciones web, como [mod_security para Apache](https://www.modsecurity.org), puede proporcionar un control centralizado y fiable sobre la seguridad del entorno de implementación y proteger contra ataques de scripts entre sitios no detectados anteriormente.

## Acceso a la información del servicio de nube {#access-to-cloud-service-information}

>[!NOTE]
>
>Las ACL para la información del servicio en la nube, así como la configuración de OSGi necesaria para proteger su instancia, se automatizan como parte del modo [](/help/sites-administering/production-ready.md)de producción lista. Aunque esto significa que no necesita realizar los cambios de configuración manualmente, se recomienda revisarlos antes de empezar a implementar la implementación.

Al [integrar la instancia de AEM con Adobe Marketing Cloud](/help/sites-administering/marketing-cloud.md) , se utilizan las configuraciones [del servicio de](/help/sites-developing/extending-cloud-config.md)nube. La información sobre estas configuraciones, junto con las estadísticas recopiladas, se almacenan en el repositorio. Recomendamos que, si utiliza esta funcionalidad, revise si la seguridad predeterminada de esta información coincide con sus necesidades.

El módulo webservicesupport escribe estadísticas e información de configuración en:

`/etc/cloudservices`

Con los permisos predeterminados:

* Entorno de creación: `read` para `contributors`

* Entorno de publicación: `read` para `everyone`

## Proteger contra ataques de falsificación de solicitudes entre sitios {#protect-against-cross-site-request-forgery-attacks}

Para obtener más información sobre los mecanismos de seguridad que AEM emplea para mitigar los ataques de CSRF, consulte la sección Filtro [de referente de](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) Sling de la lista de comprobación de seguridad y la documentación [del marco de protección de](/help/sites-developing/csrf-protection.md)CSRF.