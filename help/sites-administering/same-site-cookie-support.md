---
title: AEM Compatibilidad con cookies de SameSite para la versión 6.5 de
description: AEM Compatibilidad con cookies de SameSite para la versión 6.5 de
topic-tags: security
exl-id: e1616385-0855-4f70-b787-b01701929bbc
source-git-commit: f7a4907ca6ce8ecaff9ef1fdf99ec0951ff497e0
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 74%

---

# AEM Compatibilidad con cookies de SameSite para la versión 6.5 de {#same-site-cookie-support-for-aem-65}

Desde la versión 80, Chrome y posterior Safari, introdujeron un nuevo modelo para la seguridad de las cookies. Este modo está diseñado para introducir controles de seguridad en torno a la disponibilidad de cookies en sitios de terceros, a través de una configuración denominada `SameSite`. Para obtener información más detallada, consulte este [artículo](https://web.dev/samesite-cookies-explained/).

El valor predeterminado de esta configuración (`SameSite=Lax`) puede causar que la autenticación entre instancias o servicios de AEM no funcione. Esto se debe a que es posible que los dominios o las estructuras URL de estos servicios no entren dentro de las restricciones de esta directiva de cookies.

Para evitar esto, debe configurar la variable `SameSite` atributo de cookie a `None` para el token de inicio de sesión.

>[!CAUTION]
>
>La configuración `SameSite=None` solo se aplica si el protocolo es seguro (HTTPS).
>
>Si el protocolo no es seguro (HTTP), la configuración se ignora y el servidor muestra este mensaje ADVERTENCIA:
>
>`WARN com.day.crx.security.token.TokenCookie Skip 'SameSite=None'`

Puede agregar la configuración siguiendo los pasos siguientes:

1. Vaya a la consola web en `http://serveraddress:serverport/system/console/configMgr`
1. Busque y haga clic en el **controlador de autenticación de token de Granite de Adobe**
1. Configure el **atributo SameSite para la cookie de token de inicio de sesión** a `None`, como se muestra en la imagen siguiente
   ![samesite](assets/samesite1.png)
1. Haga clic en Guardar
1. Una vez que se actualiza esta configuración y se cierra la sesión de los usuarios y se inicia sesión de nuevo, las cookies `login-token` tendrán el conjunto de atributos `None` y se incluirán en solicitudes entre sitios.
