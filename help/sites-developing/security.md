---
title: Seguridad
seo-title: Security
description: La seguridad de la aplicación se inicia durante la fase de desarrollo
seo-description: Application Security starts during the development phase
exl-id: c4f7f45f-224b-4fc3-b4b0-f5b21b8a466f
source-git-commit: c55b70ec11842d3f7d82adbf552b2624c1dcc599
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Seguridad{#security}

La seguridad de la aplicación se inicia durante la fase de desarrollo. Adobe recomienda aplicar las siguientes prácticas recomendadas de seguridad.

## Usar sesión de solicitud {#use-request-session}

Siguiendo el principio de menor privilegio, Adobe recomienda que cada acceso al repositorio se realice utilizando la sesión enlazada a la solicitud del usuario y el control de acceso adecuado.

## Protect contra scripts en sitios múltiples (XSS) {#protect-against-cross-site-scripting-xss}

La ejecución de scripts en sitios múltiples (XSS) permite a los atacantes insertar código en páginas web vistas por otros usuarios. Esta vulnerabilidad de seguridad puede ser explotada por usuarios web malintencionados para evitar los controles de acceso.

AEM aplica el principio de filtrado de todo el contenido proporcionado por el usuario en la salida. La prevención de XSS tiene la prioridad más alta durante el desarrollo y las pruebas.

El mecanismo de protección XSS proporcionado por AEM se basa en la variable [Biblioteca Java AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) proporcionado por [OWASP (El proyecto de seguridad de la aplicación web abierta)](https://www.owasp.org/). La configuración predeterminada de AntiSamy se encuentra en

`/libs/cq/xssprotection/config.xml`

Es importante que adapte esta configuración a sus propias necesidades de seguridad superponiendo el archivo de configuración. El oficial [Documentación AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) le proporcionará toda la información que necesite para implementar sus requisitos de seguridad.

>[!NOTE]
>
>Le recomendamos encarecidamente que siempre acceda a la API de protección XSS utilizando la variable [XSSAPI proporcionado por AEM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html).

Además, un cortafuegos de la aplicación web, como [mod_security para Apache](https://www.modsecurity.org), puede proporcionar un control central fiable sobre la seguridad del entorno de implementación y protegerse contra ataques de scripts entre sitios no detectados anteriormente.

## Acceso a la información del Cloud Service {#access-to-cloud-service-information}

>[!NOTE]
>
>Las ACL para la información del Cloud Service, así como la configuración OSGi necesaria para proteger su instancia, están automatizadas como parte del [Modo listo para la producción](/help/sites-administering/production-ready.md). Aunque esto significa que no necesita realizar los cambios de configuración manualmente, se recomienda revisarlos antes de publicarlos con la implementación.

Cuando [integrar la instancia de AEM con Adobe Marketing Cloud](/help/sites-administering/marketing-cloud.md) utilice [configuraciones del Cloud Service](/help/sites-developing/extending-cloud-config.md). La información sobre estas configuraciones, junto con las estadísticas recopiladas, se almacenan en el repositorio. Le recomendamos que, si utiliza esta funcionalidad, revise si la seguridad predeterminada de esta información coincide con sus necesidades.

El módulo webservicesupport escribe estadísticas e información de configuración en:

`/etc/cloudservices`

Con los permisos predeterminados:

* Entorno de creación: `read` para `contributors`

* Entorno de publicación: `read` para `everyone`

## Protect contra ataques de falsificación de solicitudes entre sitios {#protect-against-cross-site-request-forgery-attacks}

Para obtener más información sobre los mecanismos de seguridad que AEM emplea para mitigar los ataques de CSRF, consulte la [Filtro de referente de Sling](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) de la lista de comprobación de seguridad y la sección [Documentación del marco de protección CSRF](/help/sites-developing/csrf-protection.md).
