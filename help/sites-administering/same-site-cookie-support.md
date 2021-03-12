---
title: Compatibilidad con cookies del mismo sitio para AEM 6.5
description: Compatibilidad con cookies del mismo sitio para AEM 6.5
topic-tags: security
translation-type: tm+mt
source-git-commit: ac2f3d69fd20d7779120a194c698d6f0dd6e6a84
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---


# Compatibilidad con cookies del mismo sitio para AEM 6.5 {#same-site-cookie-support-for-aem-65}

Desde la versión 80, Chrome y posterior Safari, introdujeron un nuevo modelo para la seguridad de las cookies. Este modo está diseñado para introducir controles de seguridad en torno a la disponibilidad de cookies en sitios de terceros, a través de una configuración denominada `SameSite`. Para obtener información más detallada, consulte este [artículo](https://web.dev/samesite-cookies-explained/).

El valor predeterminado de esta configuración (`SameSite=Lax`) puede causar que la autenticación entre instancias o servicios de AEM no funcione. Esto se debe a que es posible que los dominios o las estructuras URL de estos servicios no entren dentro de las restricciones de esta directiva de cookies.

Para evitarlo, debe establecer el atributo de cookie SameSite en `None` para el token de inicio de sesión.

Para ello, siga los siguientes pasos:

1. Vaya a la consola web en `http://serveraddress:serverport/system/console/configMgr`
1. Busque y haga clic en **Adobe Granite Token Authentication Handler**
1. Establezca el atributo **SameSite para la cookie de token de inicio de sesión** en `None`, como se muestra en la imagen siguiente
   ![samesite](assets/samesite1.png)
1. Haga clic en Guardar
1. Una vez que esta configuración se actualice y los usuarios cierren la sesión y vuelvan a iniciarla, las cookies `login-token` tendrán el atributo `None` establecido y se incluirán en las solicitudes entre sitios.
