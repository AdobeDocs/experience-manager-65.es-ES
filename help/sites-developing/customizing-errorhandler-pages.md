---
title: Personalización de páginas mostradas por el controlador de errores
seo-title: Personalización de páginas mostradas por el controlador de errores
description: AEM viene con un controlador de error estándar para el manejo de errores HTTP
seo-description: AEM viene con un controlador de error estándar para el manejo de errores HTTP
uuid: aaf940fd-e428-4c7c-af7f-88b1d02c17c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 63c94c82-ed96-4d10-b645-227fa3c09f4b
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---


# Personalización de páginas mostradas por el controlador de errores{#customizing-pages-shown-by-the-error-handler}

AEM viene con un controlador de error estándar para controlar los errores HTTP; por ejemplo, mostrando:

![chlimage_1-67](assets/chlimage_1-67a.png)

Existen secuencias de comandos proporcionadas por el sistema (en `/libs/sling/servlet/errorhandler`) para responder a códigos de error; de forma predeterminada, las siguientes están disponibles con una instancia de CQ estándar:

* 403.jsp
* 404.jsp

>[!NOTE]
>
>AEM se basa en Apache Sling, por lo tanto consulte [https://sling.apache.org/site/errorhandling.html](https://sling.apache.org/site/errorhandling.html) para obtener información detallada sobre la gestión de errores de Sling.

>[!NOTE]
>
>En una instancia de autor, [el filtro de depuración de CQ WCM](/help/sites-deploying/osgi-configuration-settings.md) está habilitado de forma predeterminada. Esto siempre resulta en el código de respuesta 200. El controlador de error predeterminado responde escribiendo el seguimiento de pila completo en la respuesta.
>
>En una instancia de publicación, el filtro de depuración de CQ WCM está *siempre* deshabilitado (aunque esté configurado como habilitado).

## Cómo personalizar páginas mostradas por el controlador de errores {#how-to-customize-pages-shown-by-the-error-handler}

Puede desarrollar sus propias secuencias de comandos para personalizar las páginas que muestra el controlador de errores cuando se encuentra un error. Las páginas personalizadas se crearán en `/apps` y superpondrán las páginas predeterminadas (que se encuentran en `/libs`).

>[!NOTE]
>
>Consulte [Uso de Overlays](/help/sites-developing/overlays.md) para obtener más detalles.

1. En el repositorio, copie las secuencias de comandos predeterminadas:

   * de `/libs/sling/servlet/errorhandler/`
   * hasta `/apps/sling/servlet/errorhandler/`

   Como la ruta de destino no existe de forma predeterminada, deberá crearla al hacerlo por primera vez.

1. Ir a `/apps/sling/servlet/errorhandler`. Aquí puede:

   * edite la secuencia de comandos existente adecuada para proporcionar la información requerida.
   * cree y edite una nueva secuencia de comandos para el código requerido.

1. Guarde los cambios y pruebe.

>[!CAUTION]
>
>Los controladores 404.jsp y 403.jsp se han diseñado específicamente para adaptarse a la autenticación CQ5; en particular, permitir el inicio de sesión del sistema en caso de estos errores.
>
>Por lo tanto, la sustitución de estos dos controladores debe realizarse con bueno cuidado.

### Personalización de la respuesta a los errores HTTP 500 {#customizing-the-response-to-http-errors}

Los errores HTTP 500 son causados por excepciones del lado del servidor.

* **[500 ](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**
Error interno del servidorEl servidor encontró una condición inesperada que impedía que cumpliera la solicitud.

Cuando el procesamiento de la solicitud resulta en una excepción, el marco de Apache Sling (en el que AEM está integrado):

* registra la excepción
* devuelve:

   * el código de respuesta HTTP 500
   * seguimiento de pila de excepciones

   en el cuerpo de la respuesta.

Al [personalizar las páginas que muestra el controlador de errores](#how-to-customize-pages-shown-by-the-error-handler) se puede crear una secuencia de comandos `500.jsp`. Sin embargo, sólo se utiliza si `HttpServletResponse.sendError(500)` se ejecuta explícitamente; es decir, desde un captador de excepciones.

De lo contrario, el código de respuesta se establece en 500, pero la secuencia de comandos `500.jsp` no se ejecuta.

Para gestionar errores 500, el nombre de archivo de la secuencia de comandos del controlador de errores debe ser el mismo que la clase de excepción (o superclase). Para gestionar todas estas excepciones, puede crear una secuencia de comandos `/apps/sling/servlet/errorhandler/Throwable.js`p o `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!CAUTION]
>
>En una instancia de autor, [el filtro de depuración de CQ WCM](/help/sites-deploying/osgi-configuration-settings.md) está habilitado de forma predeterminada. Esto siempre resulta en el código de respuesta 200. El controlador de error predeterminado responde escribiendo el seguimiento de pila completo en la respuesta.
>
>Para un controlador de errores personalizado, se necesitan respuestas con código 500, por lo que el [filtro de depuración de CQ WCM debe deshabilitarse](/help/sites-deploying/osgi-configuration-settings.md). Esto garantiza que se devuelve el código de respuesta 500, que a su vez activa el controlador de error Sling correcto.
>
>En una instancia de publicación, el filtro de depuración de CQ WCM está *siempre* deshabilitado (aunque esté configurado como habilitado).

