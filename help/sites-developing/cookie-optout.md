---
title: Configuración del uso de cookies
seo-title: Configuración del uso de cookies
description: AEM proporciona un servicio que le permite configurar y controlar cómo se utilizan las cookies con las páginas Web
seo-description: AEM proporciona un servicio que le permite configurar y controlar cómo se utilizan las cookies con las páginas Web
uuid: 10d95176-0a56-41f1-9d36-01dbdac757d4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 5773ec1a-f15b-462d-8f9f-54ee1d7ead44
translation-type: tm+mt
source-git-commit: f64eb57a69f2124523bd6eaed3e2f58a54c1ea8e
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 3%

---


# Configuración del uso de cookies{#configuring-cookie-usage}

AEM proporciona un servicio que le permite configurar y controlar cómo se utilizan las cookies con las páginas web:

* Un servicio configurable del lado del servidor mantiene una lista de cookies que se pueden utilizar.
* Una API de javascript permite que el código de javascript compruebe que se puede utilizar una cookie.

Utilice esta función para asegurarse de que las páginas cumplen con el consentimiento de los usuarios en cuanto al uso de cookies.

## Configuración de cookies permitidas {#configuring-allowed-cookies}

Configure el servicio de exclusión de Adobe Granite para especificar cómo se utilizan las cookies en las páginas web. En la tabla siguiente se describen las propiedades que se pueden configurar.

Para configurar el servicio, puede utilizar la [Consola Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) o [agregar una configuración OSGi al repositorio](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository). En la tabla siguiente se describen las propiedades necesarias para cada método. Para una configuración OSGi, el PID de servicio es `com.adobe.granite.optout`.

| Nombre de propiedad (consola web) | Nombre de propiedad OSGi | Descripción |
|---|---|---|
| Cookies de exclusión | optout.cookies | Los nombres de las cookies que indican, cuando están presentes en el dispositivo del usuario, que el usuario no ha consentido en utilizar cookies. |
| Encabezados HTTP de exclusión | optout.headers | Nombres de encabezados HTTP que indican, cuando están presentes, que el usuario no ha consentido en utilizar cookies. |
| Cookies de Lista blanca | optout.whitelist.cookies | Una lista de cookies que son esenciales para el funcionamiento del sitio Web y pueden utilizarse sin el consentimiento del usuario. |

## Validación del uso de cookies {#validating-cookie-usage}

Utilice javascript del lado del cliente para llamar al servicio de exclusión de Adobe Granite para verificar que puede utilizar una cookie. Utilice el objeto javascript Granite.OptOutUtil para realizar cualquiera de las siguientes tareas:

* Obtenga una lista de nombres de cookies que indique que el usuario no acepta usar cookies para fines de seguimiento.
* Obtenga una lista de cookies que se puedan utilizar.
* Determine si el explorador Web contiene una cookie que indica que el usuario no acepta el uso de cookies para el seguimiento.
* Determine si se puede utilizar una cookie específica.

La carpeta de biblioteca de cliente granite.utils [](/help/sites-developing/clientlibs.md#referencing-client-side-libraries) proporciona el objeto Granite.OptOutUtil. Añada el siguiente código en el JSP del encabezado de página para incluir un vínculo a la biblioteca de javascript:

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

## El objeto Granite.OptOutUtil de JavaScript {#the-granite-optoututil-javascript-object}

Granite.OptOutUtil le permite determinar si se permite el uso de cookies.

### función getCookieNames() {#getcookienames-function}

Devuelve los nombres de las cookies que, cuando están presentes, indican que el usuario no ha dado su consentimiento para el uso de cookies.

**Parámetros**

Ninguna.

**Devuelve**

Matriz de nombres de cookies.

#### función getWhitelistCookieNames() {#getwhitelistcookienames-function}

Devuelve los nombres de las cookies que se pueden utilizar independientemente del consentimiento del usuario.

**Parámetros**

Ninguna.

**Devuelve**

Matriz de nombres de cookies.

#### Función isOptedOut() {#isoptedout-function}

Determina si el explorador del usuario contiene cookies que indican que no se ha dado el consentimiento para usar cookies.

**Parámetros**

Ninguna.

**Devuelve**

Un valor booleano de `true` si se encuentra una cookie que indica no consentimiento, y un valor de `false` si ninguna cookie indica no consentimiento.

### función maySetCookie(cookieName) {#maysetcookie-cookiename-function}

Determina si se puede utilizar una cookie específica en el explorador del usuario. Esta función equivale a utilizar la función `isOptedOut` junto con determinar si la cookie dada se incluye en la lista que devuelve la función `getWhitelistCookieNames`.

**Parámetros**

* cookieName: Cadena. El nombre de la cookie.

**Devuelve**

Un valor booleano de `true` si se puede utilizar `cookieName` o un valor de `false` si no se puede utilizar `cookieName`.
