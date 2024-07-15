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

Las notificaciones son similares a [actividades](/help/communities/essentials-activities.md) y [suscripciones](/help/communities/subscriptions.md), ya que pueden ser el resultado de:

* El miembro que publica contenido.
* El miembro que elige seguir a otro miembro.
* El miembro que elige seguir temas específicos, artículos y otros hilos de contenido.
* Etiquetado de miembros (@mention): otro miembro de la comunidad en un contenido generado por el usuario.

Lo que distingue las notificaciones de las actividades y las suscripciones es:

* Un vínculo a la sección de notificaciones siempre está presente en el encabezado de un sitio de la comunidad:

   * Las actividades requieren que [la función de flujo de actividad](/help/communities/functions.md#activity-stream-function) se incluya en la estructura del sitio de la comunidad.
   * Las suscripciones requieren [la configuración del correo electrónico](/help/communities/email.md).

* La implementación de las notificaciones se realiza a través de canales escalables y conectables:

   * Las actividades solo están disponibles en la web.
   * Las suscripciones solo están disponibles por correo electrónico.

A partir de las comunidades [FP1](/help/communities/deploy-communities.md#latestfeaturepack), los canales de notificación disponibles son:

* Canal web, al que se accede mediante el vínculo `Notifications`.
* El canal de correo electrónico, disponible cuando el correo electrónico está configurado correctamente.

Los canales futuros son móviles y de escritorio.

### Requisitos  {#requirements}

**Configurar correo electrónico**

El correo electrónico debe configurarse para que el canal de correo electrónico funcione para las notificaciones.

Para obtener instrucciones sobre cómo configurar el correo electrónico, consulte [Configuración del correo electrónico](/help/communities/analytics.md).

**Activar Seguir**

Los componentes deben configurarse para habilitar lo siguiente. Las características que permiten el seguimiento son [blog](/help/communities/blog-feature.md), [foro](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendario](/help/communities/calendar.md), [biblioteca de archivos](/help/communities/file-library.md) y [comentarios](/help/communities/comments.md).

**Nota**:

* Es posible que los componentes utilizados en la comunidad [plantillas de sitio](/help/communities/sites.md) y [plantillas de grupo](/help/communities/tools-groups.md) ya estén configurados para seguir.

* Los perfiles de miembro ya están configurados para permitir que los sigan otros miembros.

## Notificaciones de lo siguiente {#notifications-from-following}

![notificaciones](assets/notifications.png)

El botón **[!UICONTROL Seguir]** proporciona un medio para seguir las entradas como actividades, suscripciones o notificaciones. Cada vez que se selecciona el botón **[!UICONTROL Seguir]**, es posible activar o desactivar una selección. La selección `Email Subscriptions` solo está presente cuando se configura.

Si se selecciona cualquier método de seguimiento, el texto del botón cambia a **[!UICONTROL Siguiendo]**. Para su comodidad, es posible seleccionar `Unfollow All` para desactivar todos los métodos.

Aparecerá el botón **[!UICONTROL Seguir]**:

* Al ver el perfil de otro miembro.
* En una página de funciones principal, como foros, control de calidad y blogs:

   * Sigue toda la actividad de para esa función general.

* Para una entrada específica, como un tema de foro, una pregunta de control de calidad o un artículo de blog:

   * Sigue todas las actividades de esa entrada específica.

## Administración de configuración de notificación {#managing-notification-settings}

Al seleccionar el vínculo Configuración de notificación en la página Notificaciones, es posible que cada miembro administre cómo se reciben las notificaciones.

El canal Web siempre está habilitado.

![notifications14](assets/notifications1.png)

El canal de correo electrónico, que depende de la [configuración correcta del correo electrónico](/help/communities/email.md), proporciona la misma configuración que para el canal web.

El canal de correo electrónico está desactivado de forma predeterminada.

![notificaciones2](assets/notifications2.png)

Puede ser activado por un miembro, pero aún depende de que se configure el correo electrónico.

![notificaciones3](assets/notifications3.png)

## Visualización de notificaciones  {#viewing-notifications}

### Notificaciones web {#web-notifications}

Un [sitio de la comunidad creado por el asistente](/help/communities/sites-console.md) ahora incluye un vínculo a la característica `Notifications` en la barra de encabezado del sitio sobre el titular. A diferencia de los mensajes, las notificaciones se crean para cada sitio de la comunidad, mientras que los mensajes deben habilitarse durante el proceso de creación del sitio.

Al visitar el sitio publicado, al seleccionar el vínculo `Notifications` se mostrarán todas las notificaciones del miembro.

![notificaciones4](assets/notifications4.png)

### Notificaciones por correo electrónico {#email-notifications}

Cuando el canal de correo electrónico está habilitado, el miembro recibe un correo electrónico que contiene un vínculo al contenido de la web.

![notificaciones5](assets/notifications5.png)

## Personalizar notificaciones por correo electrónico {#customize-email-notifications}

Las organizaciones pueden personalizar las notificaciones por correo electrónico [superponiendo](/help/communities/client-customize.md#overlays) las plantillas en **/libs/settings/community/templates/email/html**.

Por ejemplo, para modificar las notificaciones de correos electrónicos de menciones (para un componente de comunidades), agregue una condición **if** para el verbo **mención** en las plantillas de los componentes para los que habilitó la compatibilidad con **@mentions**.

Para modificar la plantilla de notificaciones de correo electrónico para @mention en los comentarios del blog, coloque la plantilla predeterminada en: **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```
