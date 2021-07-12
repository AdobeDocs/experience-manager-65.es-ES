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
role: Admin
exl-id: cadb62c9-210d-4204-8abc-d0cf70960392
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 1%

---

# Notificaciones de comunidades {#communities-notifications}

## Información general {#overview}

AEM Communities proporciona una sección de notificaciones que muestra eventos de interés para el miembro de la comunidad que ha iniciado sesión.

Las notificaciones son similares a las [actividades](/help/communities/essentials-activities.md) y [suscripciones](/help/communities/subscriptions.md) que pueden resultar de:

* El miembro que publica el contenido.
* El miembro que decide seguir a otro miembro.
* El miembro que elige seguir temas específicos, artículos y otros subprocesos de contenido.
* El etiquetado de miembros (@mention) es otro miembro de la comunidad de un usuario que genera contenido.

Lo que distingue las notificaciones de actividades y suscripciones es:

* Un vínculo a la sección de notificaciones siempre está presente en el encabezado de un sitio de la comunidad:

   * Las actividades requieren que la [función del flujo de actividad](/help/communities/functions.md#activity-stream-function) se incluya en la estructura del sitio de la comunidad.
   * Las suscripciones requieren [configuración de correo electrónico](/help/communities/email.md).

* La implementación de las notificaciones se realiza a través de canales ampliables y conectables:

   * Las actividades solo están disponibles en la web.
   * Las suscripciones solo están disponibles mediante correo electrónico.

A partir de Communities [FP1](/help/communities/deploy-communities.md#latestfeaturepack), los canales de notificación disponibles son:

* El canal web, al que se accede mediante el enlace `Notifications`.
* El canal de correo electrónico, disponible cuando el correo electrónico está configurado correctamente.

Los canales futuros son móviles y de escritorio.

### Requisitos {#requirements}

**Configurar correo electrónico**

El correo electrónico debe configurarse para que el canal de correo electrónico de las notificaciones funcione.

Para obtener instrucciones sobre la configuración del correo electrónico, consulte [Configuración del correo electrónico](/help/communities/analytics.md).

**Habilitar seguir**

Los componentes deben configurarse para habilitar lo siguiente. Las funciones que permiten lo siguiente son [blog](/help/communities/blog-feature.md), [foro](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendario](/help/communities/calendar.md), [biblioteca de archivos](/help/communities/file-library.md) y [comentarios](/help/communities/comments.md).

**Nota**:

* Los componentes utilizados dentro de las [plantillas de sitio](/help/communities/sites.md) de la comunidad y [plantillas de grupo](/help/communities/tools-groups.md) pueden estar configurados para seguir.

* Los perfiles de miembro ya están configurados para permitir que otros miembros puedan seguir.

## Notificaciones de lo siguiente {#notifications-from-following}

![notificaciones](assets/notifications.png)

El botón **[!UICONTROL Follow]** proporciona un medio para seguir entradas como actividades, suscripciones y/o notificaciones. Cada vez que se selecciona el botón **[!UICONTROL Follow]**, es posible activar o desactivar una selección. La selección `Email Subscriptions` solo está presente cuando está configurada.

Si se selecciona algún método de seguimiento, el texto del botón cambia a **[!UICONTROL Siguiendo]**. Para su comodidad, es posible seleccionar `Unfollow All` para desactivar todos los métodos.

Aparecerá el botón **[!UICONTROL Follow]**:

* Al ver el perfil de otro miembro.
* En una página de características principales, como foros, QnA y blogs:

   * Sigue toda la actividad de esa función general.

* Para una entrada específica, como un tema de foro, una pregunta de control de calidad o un artículo de blog:

   * Sigue toda la actividad de esa entrada específica.

## Administración de la configuración de notificaciones {#managing-notification-settings}

Al seleccionar el vínculo Configuración de notificación de la página Notificaciones , es posible que cada miembro administre cómo se reciben las notificaciones.

El canal web siempre está habilitado.

![notifications14](assets/notifications1.png)

El canal de correo electrónico, que se basa en una [configuración adecuada del correo electrónico](/help/communities/email.md), proporciona la misma configuración que para el canal web.

El canal de correo electrónico está desactivado de forma predeterminada.

![notifications2](assets/notifications2.png)

Un miembro puede activarlo, pero aun así depende del correo electrónico que se esté configurando.

![notifications3](assets/notifications3.png)

## Visualización de notificaciones  {#viewing-notifications}

### Notificaciones web {#web-notifications}

Un [asistente creado en el sitio de la comunidad](/help/communities/sites-console.md) ahora incluye un vínculo a la función `Notifications` en la barra de encabezado del sitio que se encuentra encima del banner. A diferencia de los mensajes, las notificaciones se crean para cada sitio de la comunidad, mientras que los mensajes deben habilitarse durante el proceso de creación del sitio.

Al visitar el sitio publicado, seleccionar el enlace `Notifications` mostrará todas las notificaciones del miembro.

![notifications4](assets/notifications4.png)

### Notificaciones por correo electrónico {#email-notifications}

Cuando el canal de correo electrónico está habilitado, el miembro recibe un correo electrónico que contiene un vínculo al contenido de la web.

![notifications5](assets/notifications5.png)

## Personalización de las notificaciones por correo electrónico {#customize-email-notifications}

Las organizaciones pueden personalizar las notificaciones por correo electrónico [superponiendo](/help/communities/client-customize.md#overlays) las plantillas en **/libs/settings/community/templates/email/html**.

Por ejemplo, para modificar las notificaciones de los correos electrónicos de menciones (para un componente de comunidades), agregue una condición **if** para el verbo **mention** en las plantillas de los componentes para los que ha habilitado la compatibilidad con **@mentions**.

Para modificar la plantilla de notificaciones de correo electrónico para @mention en comentarios de blog, coloque la plantilla predeterminada en: **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```
