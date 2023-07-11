---
title: Principales 10 de OWASP
description: AEM Conozca cómo lidia la con los diez riesgos de seguridad principales de OWASP.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 8b2a2f1d-8286-4ba5-8fe2-627509c72a45
feature: Security
source-git-commit: 1ef5593495b4bf22d2635492a360168bccc1725d
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# Principales 10 de OWASP{#owasp-top}

El [Abrir proyecto de seguridad de aplicación web](https://owasp.org/) (OWASP) mantiene una lista de lo que consideran el [Diez riesgos principales de seguridad de aplicaciones web](https://owasp.org/www-project-top-ten/).

A continuación se enumeran, junto con una explicación de cómo CRX los trata.

## 1. Inyección {#injection}

* SQL: evitado por diseño: la configuración predeterminada del repositorio no incluye ni requiere una base de datos tradicional, todos los datos se almacenan en el repositorio de contenido. Todo el acceso está limitado a usuarios autenticados y solo se puede realizar a través de la API de JCR. SQL solo se admite para consultas de búsqueda (SELECT). Además, SQL ofrece compatibilidad con enlaces de valores.
* LDAP: no es posible la inyección de LDAP, ya que el módulo de autenticación filtra la entrada y realiza la importación del usuario mediante el método bind.
* SO: no se realiza ninguna ejecución de shell desde la aplicación.

## 2. Scripts entre sitios (XSS) {#cross-site-scripting-xss}

La práctica general de mitigación es codificar todos los resultados del contenido generado por el usuario mediante una biblioteca de protección XSS del lado del servidor basada en [Codificador OWASP](https://owasp.org/www-project-java-encoder/) y [AntiSamy](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project).

XSS es una prioridad principal durante las pruebas y el desarrollo, y los problemas encontrados se resuelven (normalmente) inmediatamente.

## 3. Autenticación rota y administración de sesión {#broken-authentication-and-session-management}

AEM utiliza técnicas de autenticación sólidas y comprobadas, basadas en [Apache Jackrabbit](https://jackrabbit.apache.org/jcr/index.html) y [Apache Sling](https://sling.apache.org/). AEM Las sesiones de explorador/HTTP no se utilizan en las sesiones de.

## 4. Referencias de objeto directo no seguras {#insecure-direct-object-references}

Todo acceso a los objetos de datos está mediado por el repositorio y, por lo tanto, restringido por el control de acceso basado en roles.

## 5. Falsificación de solicitudes entre sitios (CSRF) {#cross-site-request-forgery-csrf}

AJAX La falsificación de solicitudes entre sitios (CSRF) se mitiga mediante la inyección automática de un token criptográfico en todas las solicitudes de formularios y y la verificación de este token en el servidor para cada POST.

AEM Además, se envía con un filtro basado en el encabezado de referente, que se puede configurar para que utilice *solamente* permitir solicitudes de POST de hosts específicos (definidos en una lista).

## 6. Configuración incorrecta de seguridad {#security-misconfiguration}

Es imposible garantizar que todo el software esté siempre correctamente configurado. Sin embargo, Adobe se esfuerza por proporcionar la mayor orientación posible y hacer que la configuración sea lo más sencilla posible. AEM Además, se envía a los buques con [Comprobaciones de estado de seguridad integradas](/help/sites-administering/operations-dashboard.md) que le ayudarán a supervisar la configuración de seguridad de un vistazo.

Revise la [Lista de comprobación de seguridad](/help/sites-administering/security-checklist.md) para obtener más información, que le proporciona instrucciones de protección paso a paso.

## 7. Almacenamiento criptográfico no seguro {#insecure-cryptographic-storage}

Las contraseñas se almacenan como hashes criptográficos en el nodo del usuario. De forma predeterminada, estos nodos solo los pueden leer el administrador y el propio usuario.

Los datos confidenciales, como las credenciales de terceros, se almacenan en forma cifrada mediante una biblioteca criptográfica certificada FIPS 140-2.

## 8. Error al restringir el acceso a la URL {#failure-to-restrict-url-access}

El repositorio permite la configuración de [privilegios muy específicos (según lo especificado por JCR)](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html) para un usuario o grupo determinado en cualquier ruta determinada, mediante entradas de control de acceso. El repositorio aplica las restricciones de acceso.

## 9. Protección insuficiente de la capa de transporte {#insufficient-transport-layer-protection}

Mitigado por la configuración del servidor (por ejemplo, utilice solo HTTPS).

## 10. Redirecciones y reenvíos sin validar {#unvalidated-redirects-and-forwards}

Se ha mitigado restringiendo todas las redirecciones a destinos proporcionados por el usuario a ubicaciones internas.
