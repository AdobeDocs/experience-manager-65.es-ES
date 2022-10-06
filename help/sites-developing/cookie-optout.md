---
title: Configuración del uso de cookies
seo-title: Configuring Cookie Usage
description: AEM proporciona un servicio que le permite configurar y controlar cómo se utilizan las cookies con las páginas web
seo-description: AEM provides a service that enables you to configure and control how cookies are used with your web pages
uuid: 10d95176-0a56-41f1-9d36-01dbdac757d4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 5773ec1a-f15b-462d-8f9f-54ee1d7ead44
exl-id: 42e8d804-6b6a-432e-a651-940b9f45db4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 5%

---

# Configuración del uso de cookies{#configuring-cookie-usage}

AEM proporciona un servicio que le permite configurar y controlar cómo se utilizan las cookies con las páginas web:

* Un servicio configurable del lado del servidor mantiene una lista de cookies que se pueden utilizar.
* Una API de javascript permite que su código javascript compruebe que se puede utilizar una cookie.

Utilice esta función para asegurarse de que las páginas cumplen con el consentimiento de los usuarios con respecto al uso de cookies.

## Configuración de las cookies permitidas {#configuring-allowed-cookies}

Configure el servicio de exclusión de Adobe Granite para especificar cómo se utilizan las cookies en las páginas web. En la tabla siguiente se describen las propiedades que se pueden configurar.

Para configurar el servicio, puede utilizar la variable [Consola web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) o [añadir una configuración OSGi al repositorio](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository). En la tabla siguiente se describen las propiedades que necesita para cualquiera de los métodos. Para una configuración OSGi, el PID de servicio es `com.adobe.granite.optout`.

| Nombre de propiedad (consola web) | Nombre de propiedad OSGi | Descripción |
|---|---|---|
| Cookies de exclusión | optout.cookies | Nombres de cookies que indican, cuando están presentes en el dispositivo del usuario, que el usuario no ha aceptado utilizar cookies. |
| Encabezados HTTP de exclusión | optout.headers | Nombres de encabezados HTTP que indican, cuando están presentes, que el usuario no ha aceptado utilizar cookies. |
| Cookies de la lista blanca | optout.whitelist.cookies | Una lista de cookies que son esenciales para el funcionamiento del sitio web y pueden utilizarse sin el consentimiento del usuario. |

## Validación del uso de cookies {#validating-cookie-usage}

Utilice javascript del lado del cliente para llamar al servicio de exclusión de Adobe Granite y comprobar que puede utilizar una cookie. Utilice el objeto javascript Granite.OptOutUtil para realizar cualquiera de las siguientes tareas:

* Obtenga una lista de nombres de cookies que indique que el usuario no da su consentimiento para usar cookies con fines de seguimiento.
* Obtenga una lista de cookies que se pueden utilizar.
* Determine si el explorador web contiene una cookie que indica que el usuario no da su consentimiento para el uso de cookies para el seguimiento.
* Determine si se puede usar una cookie específica.

El granito.utils [carpeta de biblioteca cliente](/help/sites-developing/clientlibs.md#referencing-client-side-libraries) proporciona el objeto Granite.OptOutUtil . Agregue el siguiente código al JSP del encabezado de la página para incluir un vínculo a la biblioteca javascript:

`<ui:includeClientLib categories="granite.utils" />`

Por ejemplo, la siguiente función de javascript determina si se permite utilizar la cookie COOKIE_NAME antes de escribirla:

```
function writeCookie(value){
   if (!Granite.OptOutUtil.maySetCookie("COOKIE_NAME"))
      return;
   if (value) {
      value = encodeURIComponent(value);
      document.cookie = "COOKIE_NAME=" + value;
   }
}
```

## El objeto JavaScript Granite.OptOutUtil {#the-granite-optoututil-javascript-object}

Granite.OptOutUtil le permite determinar si se permite el uso de cookies.

### getCookieNames(), función {#getcookienames-function}

Devuelve los nombres de las cookies que, cuando están presentes, indican que el usuario no ha dado su consentimiento para el uso de cookies.

**Parámetros**

Ninguno.

**Devuelve**

Matriz de nombres de cookies.

#### función getWhitelistCookieNames() {#getwhitelistcookienames-function}

Devuelve los nombres de las cookies que se pueden usar independientemente del consentimiento del usuario.

**Parámetros**

Ninguno.

**Devuelve**

Matriz de nombres de cookies.

#### isOptedOut(), función {#isoptedout-function}

Determina si el explorador del usuario contiene cookies que indican que no se ha dado el consentimiento para usar cookies.

**Parámetros**

Ninguno.

**Devuelve**

Un valor booleano de `true` si se encuentra una cookie que indica que no hay consentimiento, y un valor de `false` si ninguna cookie indica no consentimiento.

### función maySetCookie(cookieName) {#maysetcookie-cookiename-function}

Determina si se puede usar una cookie específica en el explorador del usuario. Esta función equivale a usar la variable `isOptedOut` junto con la determinación de si la cookie dada está incluida en la lista de que `getWhitelistCookieNames` devuelve.

**Parámetros**

* cookieName: Cadena. Nombre de la cookie.

**Devuelve**

Un valor booleano de `true` if `cookieName` puede utilizarse, o bien un valor de `false` if `cookieName` no se puede usar.
