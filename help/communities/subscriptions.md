---
title: Suscripciones de comunidades
seo-title: Suscripciones de comunidades
description: Los miembros de la comunidad interactúan con otros miembros a través del correo electrónico
seo-description: Los miembros de la comunidad interactúan con otros miembros a través del correo electrónico
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
translation-type: tm+mt
source-git-commit: 2fcd87cd1def7fc265ba40c83b50db86618f3b70
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---


# Suscripciones de comunidades {#communities-subscriptions}

## Información general {#overview}

Desde Communities [FP1](deploy-communities.md#latestfeaturepack), los miembros de la comunidad pueden interactuar con la comunidad a través del correo electrónico mediante una función denominada suscripciones.

Las suscripciones son similares a [notificaciones](notifications.md) ya que los miembros pueden suscribirse cuando siguen artículos de blog, temas de foro o preguntas de control de calidad.

Lo que distingue las suscripciones de las notificaciones es:

* Los miembros no podrán suscribirse cuando sigan a otros miembros.
* La única acción que deben realizar los miembros es seleccionar `Email Subscriptions` cuando se realice lo siguiente.
* Cuando se configura la respuesta por correo electrónico, los miembros pueden publicar contenido simplemente respondiendo al correo electrónico recibido.

### Requisitos {#requirements}

**Configurar correo electrónico**

El correo electrónico debe configurarse para que las suscripciones funcionen y para que los miembros respondan por correo electrónico.

Para obtener instrucciones sobre cómo configurar el correo electrónico, consulte [Configuración del correo electrónico](email.md).

**Habilitar Suscripciones y seguir**

Los componentes deben configurarse para habilitar las suscripciones *y* siguientes. Las funciones que permiten suscripciones son [blog](blog-feature.md), [foro](forum.md) y [QnA](working-with-qna.md).

## Suscripciones de la siguiente {#subscriptions-from-following}

![suscripción-siguiente](assets/subscription-following.png)

El botón **Seguir** proporciona un medio para seguir las entradas como actividades, suscripciones y/o notificaciones. Cada vez que se selecciona el botón **Seguir**, es posible activar o desactivar una selección.

Si se selecciona cualquier método de seguimiento, el texto del botón cambia a **Siguiente**. Para mayor comodidad, es posible seleccionar `Unfollow All` para desactivar todos los métodos.

El botón **Seguir** incluirá la opción `Email Subscriptions` sólo cuando se configure un foro, QnA o blog para habilitar suscripciones de correo electrónico. Aparecerá este botón:

* En la página de características principal del foro habilitado, QnA o blog Enviará un mensaje de correo electrónico para todas las actividades de esa función.

* Para una entrada específica, como un tema del foro, una pregunta de QnA o un artículo del blog Enviará un correo electrónico cuando haya actividad para esa entrada específica.

## Responder por correo electrónico {#reply-by-email}

Cuando el correo electrónico se [configura para responder por correo electrónico](email.md#configure-polling-importer), el miembro que se suscribió recibirá un correo electrónico con el contenido publicado y un vínculo al contenido en línea.

Si responden al correo electrónico, el contenido que introduzcan en la respuesta aparecerá como contenido en línea.

![email-response](assets/email-reply.png)

La cantidad de tiempo que tarda en anunciarse una respuesta está controlada por el intervalo de actualización del [importador de encuestas](email.md#configure-polling-importer).

![QA](assets/qa.png)

