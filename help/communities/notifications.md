---
title: Notificaciones de comunidades
seo-title: Notificaciones de comunidades
description: AEM Communities tiene notificaciones que muestran eventos de interés para el miembro de la comunidad que ha iniciado sesión
seo-description: AEM Communities tiene notificaciones que muestran eventos de interés para el miembro de la comunidad que ha iniciado sesión
uuid: 2f5ea4b5-7308-414e-a3f8-2e8aa76b1ef4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ab9088b7-a691-4153-ac82-1e8c0a19ed5d
docset: aem65
translation-type: tm+mt
source-git-commit: 22e853ecaf2696c7329a81bb9d375b1dbc74452c

---


# Notificaciones de comunidades {#communities-notifications}

## Información general {#overview}

Comunidades de AEM proporciona una sección de notificaciones que muestra eventos de interés para el miembro de la comunidad que ha firmado.

Las notificaciones son similares a [actividades](/help/communities/essentials-activities.md) y [suscripciones](/help/communities/subscriptions.md) que pueden derivarse de:

* El miembro que publica contenido.
* El miembro que decide seguir a otro miembro.
* El miembro que elige seguir temas específicos, artículos y otros hilos de contenido.
* El miembro que etiqueta (@uncia) otro miembro de la comunidad en un contenido generado por el usuario.

Lo que distingue las notificaciones de actividades y suscripciones es:

* Siempre hay un vínculo a la sección de notificaciones en el encabezado de un sitio de comunidad:

   * Las Actividades requieren que la función [de flujo de](/help/communities/functions.md#activity-stream-function) actividad se incluya en la estructura del sitio de la comunidad.
   * Las Suscripciones requieren [la configuración del correo electrónico](/help/communities/email.md).

* La implementación de las notificaciones se realiza mediante canales escalables y conectables:

   * Las Actividades solo están disponibles en la web.
   * Las Suscripciones solo están disponibles mediante correo electrónico.

A partir del [PM1](/help/communities/deploy-communities.md#latestfeaturepack)de las Comunidades, los canales de notificación disponibles son:

* El canal web, al que se accede mediante el `Notifications` vínculo.
* El canal de correo electrónico, disponible cuando el correo electrónico está configurado correctamente.

Los canales futuros son móviles y de escritorio.

### Requisitos {#requirements}

**Configurar correo electrónico**

El correo electrónico debe configurarse para que el canal de correo electrónico de las notificaciones funcione.

Para obtener instrucciones sobre cómo configurar el correo electrónico, consulte [Configuración del correo electrónico](/help/communities/analytics.md).

**Habilitar Seguir**

Los componentes deben configurarse para habilitar lo siguiente. Las funciones que permiten lo siguiente son [blog](/help/communities/blog-feature.md), [foro](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendario](/help/communities/calendar.md), [biblioteca](/help/communities/file-library.md)[](/help/communities/comments.md)de archivos y comentarios.

**Nota**:

* Es posible que los componentes utilizados dentro de las plantillas [de](/help/communities/sites.md) sitio de la comunidad y las plantillas [de](/help/communities/tools-groups.md) grupo ya estén configurados para seguir.

* Los perfiles de miembros ya están configurados para permitir que otros miembros los sigan.

## Notificaciones de lo siguiente {#notifications-from-following}

![chlimage_1-243](assets/chlimage_1-243.png)

El botón **[!UICONTROL Seguir]** proporciona un medio para seguir las entradas como actividades, suscripciones y/o notificaciones. Cada vez que se selecciona el botón **[!UICONTROL Seguir]** , es posible activar o desactivar una selección. La `Email Subscriptions` selección solo está presente cuando está configurada.

Si se selecciona cualquier método de seguimiento, el texto del botón cambia a **[!UICONTROL Siguiente]**. Para mayor comodidad, es posible seleccionar `Unfollow All` desactivar todos los métodos.

Aparecerá el botón **[!UICONTROL Seguir]** :

* Al ver el perfil de otro miembro.
* En una página de características principal, como foros, QnA y blogs:

   * Sigue toda la actividad de esa función general.

* Para una entrada específica, como un tema del foro, una pregunta de QnA o un artículo del blog:

   * Sigue toda la actividad de esa entrada específica.

## Administración de la configuración de notificaciones {#managing-notification-settings}

Al seleccionar el vínculo Configuración de notificación en la página Notificaciones, cada miembro puede administrar cómo se reciben las notificaciones.

El canal web siempre está habilitado.

![chlimage_1-244](assets/chlimage_1-244.png)

El canal de correo electrónico, que depende de la [configuración correcta del correo electrónico](/help/communities/email.md), proporciona la misma configuración que para el canal web.

El canal de correo electrónico está desactivado de forma predeterminada.

![chlimage_1-245](assets/chlimage_1-245.png)

Un miembro puede activarlo, pero aún depende de la configuración del correo electrónico.

![chlimage_1-246](assets/chlimage_1-246.png)

## Visualización de notificaciones{#viewing-notifications} 

### Notificaciones Web {#web-notifications}

Un [asistente creado en un sitio](/help/communities/sites-console.md) de comunidad ahora incluye un vínculo a la `Notifications` función en la barra de encabezado del sitio que hay encima del letrero. A diferencia de los mensajes, las notificaciones se crean para cada sitio de la comunidad, mientras que los mensajes se deben habilitar durante el proceso de creación del sitio.

Al visitar el sitio publicado, al seleccionar el `Notifications` vínculo se mostrarán todas las notificaciones del miembro.

![chlimage_1-247](assets/chlimage_1-247.png)

### Notificaciones de correo electrónico {#email-notifications}

Cuando el canal de correo electrónico está activado, el miembro recibe un correo electrónico que contiene un vínculo al contenido de la web.

![chlimage_1-248](assets/chlimage_1-248.png)

## Personalizar notificaciones por correo electrónico {#customize-email-notifications}

Las organizaciones pueden personalizar las notificaciones por correo electrónico [superponiendo](/help/communities/client-customize.md#overlays) las plantillas en **/libs/settings/community/templates/email/html**.

Por ejemplo, para modificar las notificaciones de correo electrónico de menciones (para un componente de comunidad), agregue una condición **if** para la **mención** verbo en las plantillas de los componentes para los que habilitó la compatibilidad con **@mentions** .

Para modificar la plantilla de notificaciones de correo electrónico para @uncia en los comentarios del blog, coloque la plantilla predeterminada en: **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/es**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

