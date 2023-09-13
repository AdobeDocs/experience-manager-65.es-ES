---
title: Personalizar páginas mostradas por el controlador de error
description: Adobe Experience Manager incluye un controlador de error estándar para administrar errores HTTP.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: d6745baa-44da-45dd-b5d5-a9b218e7e8cf
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 1%

---

# Personalizar páginas mostradas por el controlador de error{#customizing-pages-shown-by-the-error-handler}

Adobe Experience Manager AEM () viene con un controlador de error estándar para administrar errores HTTP; por ejemplo, mostrando:

![chlimage_1-67](assets/chlimage_1-67a.png)

Existen secuencias de comandos proporcionadas por el sistema (en `/libs/sling/servlet/errorhandler`) para responder a los códigos de error, de forma predeterminada están disponibles las siguientes opciones con una instancia de CQ estándar:

* 403.jsp
* 404.jsp

>[!NOTE]
>
>AEM Se basa en Apache Sling. Como tal, consulte [Control de errores](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html) para obtener información detallada sobre la gestión de errores de Sling.

>[!NOTE]
>
>En una instancia de autor, la variable [Filtro de depuración de CQ WCM](/help/sites-deploying/osgi-configuration-settings.md) está activada de forma predeterminada. Esto siempre resulta en el código de respuesta 200. El controlador de error predeterminado responde escribiendo el seguimiento de pila completo en la respuesta.
>
>En una instancia de publicación, el filtro de depuración de CQ WCM es *siempre* desactivado (incluso si está configurado como activado).

## Personalizar páginas mostradas por el controlador de error {#how-to-customize-pages-shown-by-the-error-handler}

Puede desarrollar sus propias secuencias de comandos para personalizar las páginas que muestra el controlador de errores cuando se produce un error. Las páginas personalizadas se crean en `/apps` y superponer las páginas predeterminadas (que se encuentran en `/libs`).

>[!NOTE]
>
>Consulte [Uso de superposiciones](/help/sites-developing/overlays.md) para obtener más información.

1. En el repositorio, copie los scripts predeterminados:

   * de `/libs/sling/servlet/errorhandler/`
   * hasta `/apps/sling/servlet/errorhandler/`

   Como la ruta de destino no existe de forma predeterminada, debe crearla al hacerlo por primera vez.

1. Vaya a `/apps/sling/servlet/errorhandler` y realice una de las acciones siguientes:

   * edite la secuencia de comandos existente adecuada para poder proporcionar la información necesaria.
   * cree y edite un nuevo script para el código requerido.

1. Guarde los cambios y pruebe.

>[!CAUTION]
>
>Los controladores 404.jsp y 403.jsp se han diseñado para adaptarse a la autenticación CQ5; en particular, para permitir el inicio de sesión en el sistema si se producen estos errores.
>
>Por lo tanto, la sustitución de estos dos controladores debe realizarse con mucho cuidado.

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
>En una instancia de autor, la variable [Filtro de depuración de CQ WCM](/help/sites-deploying/osgi-configuration-settings.md) está activada de forma predeterminada. Esto siempre resulta en el código de respuesta 200. El controlador de error predeterminado responde escribiendo el seguimiento de pila completo en la respuesta.
>
>Para un controlador de error personalizado, se necesitan respuestas con código 500, por lo que la variable [El filtro de depuración de CQ WCM debe estar desactivado](/help/sites-deploying/osgi-configuration-settings.md). Esto garantiza que se devuelva el código de respuesta 500, lo que a su vez déclencheur el controlador de error de Sling correcto.
>
>En una instancia de publicación, el filtro de depuración de CQ WCM es *siempre* desactivado (incluso si está configurado como activado).
