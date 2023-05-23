---
title: Personalizar páginas mostradas por el controlador de error
seo-title: Customizing Pages shown by the Error Handler
description: AEM viene con un controlador de error estándar para administrar errores HTTP
seo-description: AEM comes with a standard error handler for handling HTTP errors
uuid: aaf940fd-e428-4c7c-af7f-88b1d02c17c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 63c94c82-ed96-4d10-b645-227fa3c09f4b
exl-id: d6745baa-44da-45dd-b5d5-a9b218e7e8cf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 2%

---

# Personalizar páginas mostradas por el controlador de error{#customizing-pages-shown-by-the-error-handler}

AEM viene con un controlador de error estándar para la administración de errores HTTP; por ejemplo, mostrando:

![chlimage_1-67](assets/chlimage_1-67a.png)

Existen secuencias de comandos proporcionadas por el sistema (en `/libs/sling/servlet/errorhandler`) para responder a los códigos de error, de forma predeterminada están disponibles las siguientes opciones con una instancia de CQ estándar:

* 403.jsp
* 404.jsp

>[!NOTE]
>
>AEM Se basa en Apache Sling, por lo que consulte [https://sling.apache.org/site/errorhandling.html](https://sling.apache.org/site/errorhandling.html) para obtener información detallada sobre Sling Error Handling.

>[!NOTE]
>
>En una instancia de autor, [Filtro de depuración de CQ WCM](/help/sites-deploying/osgi-configuration-settings.md) está activada de forma predeterminada. Esto siempre resulta en el código de respuesta 200. El controlador de error predeterminado responde escribiendo el seguimiento de pila completo en la respuesta.
>
>En una instancia de publicación, el filtro de depuración de CQ WCM es *siempre* desactivado (incluso si está configurado como activado).

## Personalizar páginas mostradas por el controlador de error {#how-to-customize-pages-shown-by-the-error-handler}

Puede desarrollar sus propias secuencias de comandos para personalizar las páginas que muestra el controlador de errores cuando se produce un error. Sus páginas personalizadas se crearán en `/apps` y superponer las páginas predeterminadas (que se encuentran en `/libs`).

>[!NOTE]
>
>Consulte [Uso de superposiciones](/help/sites-developing/overlays.md) para obtener más información.

1. En el repositorio, copie los scripts predeterminados:

   * de `/libs/sling/servlet/errorhandler/`
   * hasta `/apps/sling/servlet/errorhandler/`

   Como la ruta de destino no existe de forma predeterminada, deberá crearla al hacerlo por primera vez.

1. Navegue hasta `/apps/sling/servlet/errorhandler`. Aquí puede hacer lo siguiente:

   * edite la secuencia de comandos existente adecuada para proporcionar la información necesaria.
   * cree y edite un nuevo script para el código requerido.

1. Guarde los cambios y pruebe.

>[!CAUTION]
>
>Los controladores 404.jsp y 403.jsp se han diseñado específicamente para adaptarse a la autenticación CQ5; en particular, para permitir el inicio de sesión en el sistema en caso de estos errores.
>
>Por lo tanto, la sustitución de estos dos controladores debe realizarse con bueno cuidado.

### Personalización de la Respuesta a Errores HTTP 500 {#customizing-the-response-to-http-errors}

Los errores de HTTP 500 se deben a excepciones del lado del servidor.

* **[500 Error interno del servidor](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**
El servidor encontró una condición inesperada que le impedía cumplir la solicitud.

AEM Cuando el procesamiento de solicitudes resulta en una excepción, el marco de trabajo de Apache Sling (en el que se basa ese):

* registra la excepción
* devuelve:

   * el código de respuesta HTTP 500
   * el seguimiento de pila de excepciones

   en el cuerpo de la respuesta.

Por [personalización de las páginas mostradas por el controlador de error](#how-to-customize-pages-shown-by-the-error-handler) a `500.jsp` se puede crear el script. Sin embargo, solo se utiliza si `HttpServletResponse.sendError(500)` se ejecuta explícitamente; es decir, desde un receptor de excepciones.

De lo contrario, el código de respuesta se establece en 500, pero la variable `500.jsp` no se ejecuta el script.

Para controlar 500 errores, el nombre de archivo de la secuencia de comandos del controlador de errores debe ser el mismo que la clase de excepción (o superclase). Para gestionar todas estas excepciones, puede crear un script `/apps/sling/servlet/errorhandler/Throwable.js`p o `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!CAUTION]
>
>En una instancia de autor, [Filtro de depuración de CQ WCM](/help/sites-deploying/osgi-configuration-settings.md) está activada de forma predeterminada. Esto siempre resulta en el código de respuesta 200. El controlador de error predeterminado responde escribiendo el seguimiento de pila completo en la respuesta.
>
>Para un controlador de error personalizado, se necesitan respuestas con código 500, por lo que la variable [El filtro de depuración de CQ WCM debe deshabilitarse](/help/sites-deploying/osgi-configuration-settings.md). Esto garantiza que se devuelva el código de respuesta 500, lo que a su vez déclencheur el controlador de error de Sling correcto.
>
>En una instancia de publicación, el filtro de depuración de CQ WCM es *siempre* desactivado (incluso si está configurado como activado).
