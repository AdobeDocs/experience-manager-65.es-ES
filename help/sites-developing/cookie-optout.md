---
title: Configurar el uso de cookies
description: AEM proporciona un servicio que le permite configurar y controlar cómo se utilizan las cookies con sus páginas web.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 42e8d804-6b6a-432e-a651-940b9f45db4e
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 2%

---

# Configurar el uso de cookies{#configuring-cookie-usage}

AEM proporciona un servicio que le permite configurar y controlar cómo se utilizan las cookies con sus páginas web:

* Un servicio configurable del lado del servidor mantiene una lista de cookies que se pueden utilizar.
* La API de JavaScript permite al código JavaScript verificar que se pueda usar una cookie.

Utilice esta función para asegurarse de que las páginas cumplen con el consentimiento de los usuarios con respecto al uso de cookies.

## Configuración de cookies permitidas {#configuring-allowed-cookies}

Configure el Servicio de exclusión de Granite de Adobe para especificar cómo se utilizan las cookies en sus páginas web. En la tabla siguiente se describen las propiedades que se pueden configurar.

Para configurar el servicio, puede utilizar el [Consola web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) o [añadir una configuración OSGi al repositorio](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository). En la tabla siguiente se describen las propiedades que necesita para cualquiera de los métodos. Para una configuración OSGi, el PID de servicio es `com.adobe.granite.optout`.

| Nombre de propiedad (consola web) | Nombre de propiedad OSGi | Descripción |
|---|---|---|
| Cookies de exclusión | optout.cookies | Los nombres de las cookies que indican, cuando están presentes en el dispositivo del usuario, que el usuario no ha aceptado utilizar cookies. |
| Encabezados HTTP de exclusión | optout.headers | Nombres de encabezados HTTP que indican, cuando están presentes, que el usuario no ha aceptado utilizar cookies. |
| Cookies de lista blanca | optout.whitelist.cookies | Una lista de cookies que son esenciales para el funcionamiento del sitio web, y pueden ser utilizadas sin el consentimiento del usuario. |

## Validación del uso de cookies {#validating-cookie-usage}

Utilice JavaScript del lado del cliente para llamar al servicio de exclusión de Adobe Granite y comprobar que puede utilizar una cookie. Utilice el objeto JavaScript Granite.OptOutUtil para realizar cualquiera de las siguientes tareas:

* Obtenga una lista de nombres de cookies que indique que ese usuario no consiente el uso de cookies con fines de seguimiento.
* Obtenga una lista de las cookies que se pueden utilizar.
* Determine si el explorador web contiene una cookie que indique que el usuario no consiente el uso de cookies para el seguimiento.
* Determine si se puede utilizar una cookie específica.

El granite.utils [carpeta de biblioteca de cliente](/help/sites-developing/clientlibs.md#referencing-client-side-libraries) proporciona el objeto Granite.OptOutUtil. Agregue el siguiente código al JSP del encabezado de la página para incluir un vínculo a la biblioteca JavaScript:

`<ui:includeClientLib categories="granite.utils" />`

Por ejemplo, la siguiente función de JavaScript determina si se permite el uso de la cookie COOKIE_NAME antes de escribir en ella:

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

Los nombres de las cookies que, en su caso, indican que el usuario no ha dado su consentimiento para el uso de cookies.

**Parámetros**

Ninguna.

**Devuelve**

Una matriz de nombres de cookies.

#### getWhitelistCookieNames(), función {#getwhitelistcookienames-function}

Nombres de las cookies que se pueden utilizar independientemente del consentimiento del usuario.

**Parámetros**

Ninguna.

**Devuelve**

Una matriz de nombres de cookies.

#### Función isOptedOut() {#isoptedout-function}

Determina si el explorador del usuario contiene cookies que indiquen que no se ha dado el consentimiento para utilizar cookies.

**Parámetros**

Ninguna.

**Devuelve**

Un valor booleano de `true` si se encuentra una cookie que indique que no hay consentimiento y un valor de `false` si no hay cookies, indica no consentimiento.

### función maySetCookie(cookieName) {#maysetcookie-cookiename-function}

Determina si se puede utilizar una cookie específica en el explorador del usuario. Esta función equivale a utilizar el `isOptedOut` función para determinar si la cookie dada se incluye en la lista de que el `getWhitelistCookieNames` función devuelve.

**Parámetros**

* cookieName: String. Nombre de la cookie.

**Devuelve**

Un valor booleano de `true` if `cookieName` se puede utilizar o un valor de `false` if `cookieName` no se puede usar.
