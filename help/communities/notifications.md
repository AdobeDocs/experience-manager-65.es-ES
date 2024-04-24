---
title: Notificaciones de Communities
description: AEM Communities tiene notificaciones que muestran eventos de interés para el miembro de la comunidad que ha iniciado sesión
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: cadb62c9-210d-4204-8abc-d0cf70960392
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 1%

---

# Notificaciones de Communities {#communities-notifications}

## Información general {#overview}

AEM Communities proporciona una sección de notificaciones que muestra eventos de interés para el miembro de la comunidad que ha iniciado sesión.

Las notificaciones son similares a [actividades](/help/communities/essentials-activities.md) y [suscripciones](/help/communities/subscriptions.md) ya que pueden resultar de:

* El miembro que publica contenido.
* El miembro que elige seguir a otro miembro.
* El miembro que elige seguir temas específicos, artículos y otros hilos de contenido.
* Etiquetado de miembros (@mention): otro miembro de la comunidad en un contenido generado por el usuario.

Lo que distingue las notificaciones de las actividades y las suscripciones es:

* Un vínculo a la sección de notificaciones siempre está presente en el encabezado de un sitio de la comunidad:

   * Las actividades requieren la [función de flujo de actividad](/help/communities/functions.md#activity-stream-function) para que se incluya en la estructura del sitio de la comunidad.
   * Las suscripciones requieren [configuración del correo electrónico](/help/communities/email.md).

* La implementación de las notificaciones se realiza a través de canales escalables y conectables:

   * Las actividades solo están disponibles en la web.
   * Las suscripciones solo están disponibles por correo electrónico.

A partir de comunidades [FP1](/help/communities/deploy-communities.md#latestfeaturepack), los canales de notificación disponibles son:

* El canal Web, al que se accede mediante la variable `Notifications` vínculo.
* El canal de correo electrónico, disponible cuando el correo electrónico está configurado correctamente.

Los canales futuros son móviles y de escritorio.

### Requisitos  {#requirements}

**Configurar correo electrónico**

El correo electrónico debe configurarse para que el canal de correo electrónico funcione para las notificaciones.

Para obtener instrucciones sobre la configuración del correo electrónico, consulte [Configurar correo electrónico](/help/communities/analytics.md).

**Activar Seguir**

Los componentes deben configurarse para habilitar lo siguiente. Las funciones que permiten lo siguiente son [blog](/help/communities/blog-feature.md), [foro](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendario](/help/communities/calendar.md), [filelibrary](/help/communities/file-library.md), y [comentarios](/help/communities/comments.md).

**Nota**:

* Componentes utilizados en la comunidad [plantillas del sitio](/help/communities/sites.md) y [plantillas de grupo](/help/communities/tools-groups.md) puede que ya esté configurado para seguir.

* Los perfiles de miembro ya están configurados para permitir que los sigan otros miembros.

## Notificaciones de lo siguiente {#notifications-from-following}

![notificaciones](assets/notifications.png)

El **[!UICONTROL Seguir]** El botón proporciona un medio para seguir las entradas como actividades, suscripciones o notificaciones. Cada vez que **[!UICONTROL Seguir]** botón está seleccionado, es posible activar o desactivar una selección. El `Email Subscriptions` la selección solo está presente cuando está configurada.

Si se selecciona cualquier método de seguimiento, el texto del botón cambia a **[!UICONTROL Siguientes]**. Para su comodidad, es posible seleccionar `Unfollow All` para desactivar todos los métodos.

El **[!UICONTROL Seguir]** aparecerá el botón:

* Al ver el perfil de otro miembro.
* En una página de funciones principal, como foros, control de calidad y blogs:

   * Sigue toda la actividad de para esa función general.

* Para una entrada específica, como un tema de foro, una pregunta de control de calidad o un artículo de blog:

   * Sigue todas las actividades de esa entrada específica.

## Administración de configuración de notificación {#managing-notification-settings}

Al seleccionar el vínculo Configuración de notificación en la página Notificaciones, es posible que cada miembro administre cómo se reciben las notificaciones.

El canal Web siempre está habilitado.

![notifications14](assets/notifications1.png)

El canal de correo electrónico, que depende de la correcta [configuración del correo electrónico](/help/communities/email.md), proporciona la misma configuración que para el canal Web.

El canal de correo electrónico está desactivado de forma predeterminada.

![notifications2](assets/notifications2.png)

Puede ser activado por un miembro, pero aún depende de que se configure el correo electrónico.

![notifications3](assets/notifications3.png)

## Visualización de notificaciones  {#viewing-notifications}

### Notificaciones web {#web-notifications}

A [sitio de comunidad creado por el asistente](/help/communities/sites-console.md) ahora incluye un vínculo al `Notifications` en la barra de encabezado del sitio, encima del titular. A diferencia de los mensajes, las notificaciones se crean para cada sitio de la comunidad, mientras que los mensajes deben habilitarse durante el proceso de creación del sitio.

Al visitar el sitio publicado, seleccionar la variable `Notifications` El vínculo mostrará todas las notificaciones del miembro.

![notifications4](assets/notifications4.png)

### Notificaciones por correo electrónico {#email-notifications}

Cuando el canal de correo electrónico está habilitado, el miembro recibe un correo electrónico que contiene un vínculo al contenido de la web.

![notificaciones5](assets/notifications5.png)

## Personalizar notificaciones por correo electrónico {#customize-email-notifications}

Las organizaciones pueden personalizar las notificaciones por correo electrónico mediante [superposición](/help/communities/client-customize.md#overlays) las plantillas en **/libs/settings/community/templates/email/html**.

Por ejemplo, para modificar las notificaciones de las menciones de los correos electrónicos (para un componente de comunidades), añada un **if** condición para verbo **mencionar** en las plantillas de los componentes para los que habilitó la variable **@mentions** soporte.

Para modificar la plantilla de notificaciones de correo electrónico para @mention en los comentarios del blog, coloque la plantilla predeterminada en: **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```
