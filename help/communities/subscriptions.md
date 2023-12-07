---
title: Suscripciones de Communities
description: Los miembros de la comunidad interactúan con otros miembros por correo electrónico
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 338be220-659a-459c-8e90-55e3a11ddeb0
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 1%

---

# Suscripciones de Communities {#communities-subscriptions}

## Información general {#overview}

A partir de comunidades [FP1](deploy-communities.md#latestfeaturepack)Por lo tanto, los miembros de la comunidad pueden interactuar con la comunidad por correo electrónico mediante una función denominada suscripciones.

Las suscripciones son similares a [notificaciones](notifications.md) como miembros pueden suscribirse al seguir artículos de blogs, temas de foros o preguntas de control de calidad.

Lo que distingue las suscripciones de las notificaciones es:

* Los Miembros no podrán suscribirse cuando sigan a otros Miembros.
* La única acción que pueden realizar los miembros es seleccionar `Email Subscriptions` al seguir.
* Cuando se configura la respuesta al correo electrónico, los miembros pueden publicar contenido de manera efectiva simplemente respondiendo al correo electrónico recibido.

### Requisitos  {#requirements}

**Configurar correo electrónico**

El correo electrónico debe configurarse para que las suscripciones funcionen y para que los miembros respondan por correo electrónico.

Para obtener instrucciones sobre la configuración del correo electrónico, consulte [Configurar correo electrónico](email.md).

**Habilitar suscripciones y seguir**

Los componentes deben configurarse para habilitar las suscripciones *y* siguiente. Las funciones que permiten suscripciones son [blog](blog-feature.md), [foro](forum.md) y [QnA](working-with-qna.md).

## Suscripciones de los siguientes {#subscriptions-from-following}

![subscripción-siguiente](assets/subscription-following.png)

El **Seguir** El botón proporciona un medio para seguir las entradas como actividades, suscripciones o notificaciones. Cada vez que **Seguir** botón está seleccionado, es posible activar o desactivar una selección.

Si se selecciona cualquier método de seguimiento, el texto del botón cambia a **Siguientes**. Para su comodidad, es posible seleccionar `Unfollow All` para desactivar todos los métodos.

El **Seguir** El botón incluirá el `Email Subscriptions` opción solo cuando un foro, control de calidad o blog está configurado para habilitar suscripciones por correo electrónico. Este botón aparecerá:

* En la página de características principal del foro, control de calidad o blog habilitados, se enviará un correo electrónico con todas las actividades incluidas en dicha función.

* Para una entrada específica, como un tema de foro, una pregunta de control de calidad o un artículo de blog, se enviará un correo electrónico cuando haya actividad para esa entrada específica.

## Responder por correo electrónico {#reply-by-email}

Cuando el correo electrónico es [configurado para responder por correo electrónico](email.md#configure-polling-importer), el miembro que se haya suscrito recibirá un correo electrónico con el contenido publicado y un enlace al contenido en línea.

Si responde al correo electrónico, el contenido que introduce en la respuesta aparece como contenido en línea.

![email-reply](assets/email-reply.png)

La cantidad de tiempo que tarda una respuesta en publicarse está controlada por el [intervalo de actualización del importador de encuestas](email.md#configure-polling-importer).

![QA](assets/qa.png)
