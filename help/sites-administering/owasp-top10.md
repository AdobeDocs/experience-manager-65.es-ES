---
title: OWASP Top 10
seo-title: OWASP Top 10
description: Conozca cómo AEM trata los 10 principales riesgos de seguridad OWASP.
seo-description: Learn how AEM deals with the top 10 OWASP security risks.
uuid: a5a7e130-e15b-47ae-ba21-448f9ac76074
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e5323ae8-bc37-4bc6-bca6-9763e18c8e76
exl-id: 8b2a2f1d-8286-4ba5-8fe2-627509c72a45
feature: Security
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# OWASP Top 10{#owasp-top}

El [Open Web Application Security Project](https://www.owasp.org) (OWASP) mantiene una lista de lo que consideran los [Principales 10 Riesgos de Seguridad de Aplicaciones Web](https://www.owasp.org/index.php/OWASP_Top_Ten_Project).

Estos se enumeran a continuación, junto con una explicación de cómo CRX trata con ellos.

## 1. Inyección {#injection}

* SQL: se evita mediante diseño: La configuración predeterminada del repositorio no incluye ni requiere una base de datos tradicional, todos los datos se almacenan en el repositorio de contenido. Todo acceso está limitado a usuarios autenticados y solo se puede realizar a través de la API de JCR. SQL solo se admite para consultas de búsqueda (SELECT). Además, SQL ofrece compatibilidad con enlaces de valores.
* LDAP - La inyección LDAP no es posible, ya que el módulo de autenticación filtra la entrada y realiza la importación del usuario mediante el método bind.
* OS: no se realiza ninguna ejecución de shell desde la aplicación.

## 2. Secuencia de comandos entre sitios (XSS) {#cross-site-scripting-xss}

La práctica general de mitigación es codificar todos los resultados del contenido generado por el usuario utilizando una biblioteca de protección XSS del lado del servidor basada en [OWASP Encoder](https://www.owasp.org/index.php/OWASP_Java_Encoder_Project) y [AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project).

XSS es una prioridad máxima durante las pruebas y el desarrollo, y cualquier problema que se encuentre (normalmente) se resuelve inmediatamente.

## 3. Autenticación rota y administración de sesiones {#broken-authentication-and-session-management}

AEM utiliza técnicas de autenticación sólidas y comprobadas, basadas en [Apache Jackrabbit](https://jackrabbit.apache.org/) y [Apache Sling](https://sling.apache.org/). Las sesiones HTTP/explorador no se utilizan en AEM.

## 4. Referencias de objeto directo no seguras {#insecure-direct-object-references}

Todo acceso a los objetos de datos está mediado por el repositorio y, por lo tanto, restringido por el control de acceso basado en roles.

## 5. Falsificación de solicitudes entre sitios (CSRF) {#cross-site-request-forgery-csrf}

La falsificación de solicitudes entre sitios (CSRF) se mitiga mediante la inyección automática de un token criptográfico en todas las solicitudes de formularios y AJAX y la verificación de este token en el servidor para cada POST.

Además, AEM se envía con un filtro basado en encabezados de referente, que puede configurarse para *solo* permitir solicitudes de POST de hosts específicos (definidos en una lista).

## 6. Configuración incorrecta de la seguridad {#security-misconfiguration}

Es imposible garantizar que todo el software esté siempre configurado correctamente. Sin embargo, nos esforzamos por proporcionar la mayor orientación posible y hacer la configuración lo más sencilla posible. Además, AEM incluye [chequeos de seguridad integrados](/help/sites-administering/operations-dashboard.md) que le ayudan a supervisar la configuración de seguridad de un vistazo.

Revise la [Lista de comprobación de seguridad](/help/sites-administering/security-checklist.md) para obtener más información que le proporcione instrucciones de refuerzo paso a paso.

## 7. Almacenamiento criptográfico inseguro {#insecure-cryptographic-storage}

Las contraseñas se almacenan como hashes criptográficos en el nodo de usuario; de forma predeterminada, estos nodos solo son legibles por el administrador y el propio usuario.

Los datos confidenciales, como las credenciales de terceros, se almacenan en forma cifrada mediante una biblioteca criptográfica certificada FIPS 140-2.

## 8. Error al restringir el acceso a la URL {#failure-to-restrict-url-access}

El repositorio permite establecer [privilegios de granularidad (tal como lo especifica JCR)](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html) para cualquier usuario o grupo determinado en una ruta determinada, a través de entradas de control de acceso. El repositorio aplica las restricciones de acceso.

## 9. Protección insuficiente de la capa de transporte {#insufficient-transport-layer-protection}

Mitigado por la configuración del servidor (por ejemplo, use solo HTTPS).

## 10. Redirecciones y reenvíos no validados {#unvalidated-redirects-and-forwards}

Se ha reducido restringiendo todas las redirecciones a destinos suministrados por el usuario a ubicaciones internas.
