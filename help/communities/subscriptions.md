---
title: Suscripciones de Communities
seo-title: Suscripciones de Communities
description: Los miembros de la comunidad interactúan con otros miembros a través del correo electrónico
seo-description: Los miembros de la comunidad interactúan con otros miembros a través del correo electrónico
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
role: Admin
exl-id: 338be220-659a-459c-8e90-55e3a11ddeb0
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 2%

---

# Suscripciones de Communities {#communities-subscriptions}

## Información general {#overview}

A partir de Communities [FP1](deploy-communities.md#latestfeaturepack), los miembros de la comunidad pueden interactuar con ella por correo electrónico con una función denominada como suscripciones.

Las suscripciones son similares a las [notificaciones](notifications.md) ya que los miembros pueden suscribirse a través de artículos de blog, temas de foro o preguntas de control de calidad.

Lo que distingue las suscripciones de las notificaciones es:

* Los Miembros no podrán suscribirse cuando sigan a otros miembros.
* La única acción que deben realizar los miembros es seleccionar `Email Subscriptions` cuando siga.
* Cuando se configura la respuesta por correo electrónico, los miembros pueden publicar contenido simplemente respondiendo al correo electrónico recibido.

### Requisitos {#requirements}

**Configurar correo electrónico**

El correo electrónico debe configurarse para que las suscripciones funcionen y para que los miembros respondan por correo electrónico.

Para obtener instrucciones sobre la configuración del correo electrónico, consulte [Configuración del correo electrónico](email.md).

**Habilitar suscripciones y seguir**

Los componentes deben configurarse para habilitar las suscripciones *y* siguientes. Las funciones que permiten suscripciones son [blog](blog-feature.md), [foro](forum.md) y [QnA](working-with-qna.md).

## Suscripciones de lo siguiente {#subscriptions-from-following}

![suscripción siguiente](assets/subscription-following.png)

El botón **Follow** proporciona un medio para seguir entradas como actividades, suscripciones y/o notificaciones. Cada vez que se selecciona el botón **Follow**, es posible activar o desactivar una selección.

Si se selecciona algún método de seguimiento, el texto del botón cambia a **Siguiendo**. Para su comodidad, es posible seleccionar `Unfollow All` para desactivar todos los métodos.

El botón **Follow** incluirá la opción `Email Subscriptions` solo cuando se haya configurado un foro, control de calidad o blog para habilitar las suscripciones por correo electrónico. Aparecerá este botón:

* En la página de características principal del foro habilitado, QnA o blog Enviará un correo electrónico para toda la actividad que se encuentre bajo esa función.

* Para una entrada específica, como un tema del foro, una pregunta de control de calidad o un artículo del blog Enviará un correo electrónico cuando haya actividad para esa entrada específica.

## Responder por correo electrónico {#reply-by-email}

Cuando el correo electrónico está [configurado para responder por correo electrónico](email.md#configure-polling-importer), el miembro que se suscribió recibe un correo electrónico con el contenido publicado y un vínculo al contenido en línea.

Si responden al correo electrónico, el contenido que introduzcan en la respuesta aparecerá como contenido en línea.

![email-reply](assets/email-reply.png)

La cantidad de tiempo que se tarda en publicar una respuesta está controlada por el [intervalo de actualización del importador de encuestas](email.md#configure-polling-importer).

![QA](assets/qa.png)
