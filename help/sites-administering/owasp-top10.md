---
title: 10 primeros OWASP
seo-title: 10 primeros OWASP
description: Descubra cómo AEM se ocupa de los 10 principales riesgos de seguridad OWASP.
seo-description: Descubra cómo AEM se ocupa de los 10 principales riesgos de seguridad OWASP.
uuid: a5a7e130-e15b-47ae-ba21-448f9ac76074
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e5323ae8-bc37-4bc6-bca6-9763e18c8e76
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 10 primeros OWASP{#owasp-top}

El [Open Web Application Security Project](https://www.owasp.org) (OWASP) mantiene una lista de los 10 [principales riesgos](https://www.owasp.org/index.php/OWASP_Top_Ten_Project)de seguridad de aplicaciones Web.

A continuación se detallan estos temas, junto con una explicación de cómo CRX los trata.

## 1. Inyección {#injection}

* SQL: se evitó mediante diseño: La configuración predeterminada del repositorio no incluye ni requiere una base de datos tradicional; todos los datos se almacenan en el repositorio de contenido. Todo acceso está limitado a usuarios autenticados y solo se puede realizar a través de la API de JCR. SQL sólo se admite para consultas de búsqueda (SELECT). Además, SQL ofrece compatibilidad con enlace de valores.
* LDAP: la inyección de LDAP no es posible, ya que el módulo de autenticación filtra la entrada y realiza la importación del usuario mediante el método bind.
* SO: no se ejecuta shell desde la aplicación.

## 2. Secuencia de comandos entre sitios (XSS) {#cross-site-scripting-xss}

La práctica general de mitigación es codificar toda la salida del contenido generado por el usuario mediante una biblioteca de protección XSS del lado del servidor basada en [OWASP Encoder](https://www.owasp.org/index.php/OWASP_Java_Encoder_Project) y [AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project).

XSS es una prioridad principal durante las pruebas y el desarrollo, y cualquier problema que se encuentre se resuelve (normalmente) inmediatamente.

## 3. Autenticación y administración de sesiones dañadas {#broken-authentication-and-session-management}

AEM utiliza técnicas de autenticación sólidas y probadas, basadas en [Apache Jackrabbit](https://jackrabbit.apache.org/) y [Apache Sling](https://sling.apache.org/). Las sesiones HTTP/explorador no se utilizan en AEM.

## 4. Referencias de objeto directo inseguras {#insecure-direct-object-references}

Todo acceso a los objetos de datos está mediado por el repositorio y, por lo tanto, restringido por el control de acceso basado en roles.

## 5. Falsificación de solicitudes entre sitios (CSRF) {#cross-site-request-forgery-csrf}

La falsificación de solicitudes entre sitios (CSRF) se mitiga mediante la inyección automática de un token criptográfico en todos los formularios y solicitudes AJAX y la verificación de este token en el servidor para cada POST.

Además, AEM se incluye con un filtro basado en el encabezado del referente, que se puede configurar para permitir únicamente solicitudes POST de hosts incluidos específicamente en la lista blanca.

## 6. Error de configuración de seguridad {#security-misconfiguration}

Es imposible garantizar que todo el software esté siempre correctamente configurado. Sin embargo, nos esforzamos por brindar la mayor orientación posible y hacer la configuración lo más simple posible. Además, AEM incluye comprobaciones de estado de seguridad [integradas](/help/sites-administering/operations-dashboard.md) que le ayudan a supervisar la configuración de seguridad de un vistazo.

Revise la lista [de comprobación de](/help/sites-administering/security-checklist.md) seguridad para obtener más información que le proporcione instrucciones de refuerzo paso a paso.

## 7. Almacenamiento criptográfico no seguro {#insecure-cryptographic-storage}

Las contraseñas se almacenan como hashes criptográficos en el nodo de usuario; de forma predeterminada, el administrador y el propio usuario solo pueden leer estos nodos.

Los datos confidenciales, como las credenciales de terceros, se almacenan en forma cifrada mediante una biblioteca criptográfica certificada FIPS 140-2.

## 8. Error al restringir el acceso a URL {#failure-to-restrict-url-access}

El repositorio permite la configuración de privilegios [finamente arraigados (según lo especificado por JCR)](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html) para cualquier usuario o grupo determinado en cualquier ruta, a través de entradas de control de acceso. El repositorio aplica las restricciones de acceso.

## 9. Protección insuficiente de la capa de transporte {#insufficient-transport-layer-protection}

Mitigado por la configuración del servidor (p. ej., utilice sólo HTTPS).

## 10. Redirecciones y reenvíos no validados {#unvalidated-redirects-and-forwards}

Se ha reducido restringiendo todas las redirecciones a destinos suministrados por el usuario a ubicaciones internas.

