---
title: Seguridad
description: La seguridad de la aplicación se inicia durante la fase de desarrollo
exl-id: c4f7f45f-224b-4fc3-b4b0-f5b21b8a466f
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Seguridad{#security}

La seguridad de la aplicación se inicia durante la fase de desarrollo. El Adobe recomienda aplicar las siguientes prácticas recomendadas de seguridad.

## Usar sesión de solicitud {#use-request-session}

Siguiendo el principio de menor privilegio, Adobe recomienda que cada acceso al repositorio se realice mediante la sesión enlazada a la solicitud del usuario y el control de acceso adecuado.

## Protect con scripts en sitios múltiples (XSS) {#protect-against-cross-site-scripting-xss}

El proceso de ejecución de scripts en sitios múltiples (XSS) permite a los atacantes insertar código en páginas web que han visto otros usuarios. Los usuarios web malintencionados pueden aprovechar esta vulnerabilidad de seguridad para evitar los controles de acceso.

AEM Se aplica el principio de filtrado de todo el contenido proporcionado por el usuario en la salida. La prevención de XSS tiene la máxima prioridad tanto durante el desarrollo como durante las pruebas.

AEM El mecanismo de protección XSS proporcionado por el usuario se basa en la variable [Biblioteca Java™ AntiSamy](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project) proporcionado por [OWASP (El proyecto Open Web Application Security)](https://owasp.org/). La configuración predeterminada de AntiSamy se encuentra en

`/libs/cq/xssprotection/config.xml`

Es importante que adapte esta configuración a sus propias necesidades de seguridad superponiendo el archivo de configuración. El funcionario [Documentación de AntiSamy](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project) proporciona toda la información necesaria para implementar los requisitos de seguridad.

>[!NOTE]
>
>El Adobe recomienda que siempre acceda a la API de protección XSS utilizando [AEM XSSAPI proporcionado por el usuario de](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/xss/XSSAPI.html).

Además, un cortafuegos de aplicaciones web, como [mod_security para Apache](https://www.modsecurity.org), puede proporcionar un control central y fiable sobre la seguridad del entorno de implementación y proteger contra ataques de scripts entre sitios que no se habían detectado anteriormente.

## Acceso a la información del Cloud Service {#access-to-cloud-service-information}

>[!NOTE]
>
>Las ACL de la información del Cloud Service y la configuración de OSGi necesaria para proteger su instancia están automatizadas como parte de [Modo Producción lista](/help/sites-administering/production-ready.md). Aunque esto significa que no necesita cambiar la configuración manualmente, se recomienda revisarla antes de activarla con la implementación.

Cuando usted [AEM integración de la instancia de con Adobe Experience Cloud](/help/sites-administering/marketing-cloud.md), se utiliza [Configuraciones del Cloud Service](/help/sites-developing/extending-cloud-config.md). La información sobre estas configuraciones, junto con las estadísticas recopiladas, se almacenan en el repositorio. El Adobe recomienda que, si utiliza esta funcionalidad, revise si la seguridad predeterminada de esta información coincide con sus necesidades.

El módulo webservicesupport escribe estadísticas e información de configuración en:

`/etc/cloudservices`

Con los permisos predeterminados:

* Entorno de creación: `read` para `contributors`

* Entorno de publicación: `read` para `everyone`

## Protect contra ataques de falsificación de solicitud en sitios múltiples {#protect-against-cross-site-request-forgery-attacks}

AEM Para obtener más información sobre los mecanismos de seguridad que emplea el para mitigar los ataques de CSRF, consulte la [Filtro de referente de Sling](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) de la lista de comprobación de seguridad y la [Documentación del marco de protección CSRF](/help/sites-developing/csrf-protection.md).
