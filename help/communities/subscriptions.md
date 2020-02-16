---
title: Suscripciones a comunidades
seo-title: Suscripciones a comunidades
description: Los miembros de la comunidad interactúan con otros miembros a través del correo electrónico
seo-description: Los miembros de la comunidad interactúan con otros miembros a través del correo electrónico
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Suscripciones a comunidades {#communities-subscriptions}

## Información general {#overview}

A partir de Communities [FP1](deploy-communities.md#latestfeaturepack), los miembros de la comunidad pueden interactuar con la comunidad a través del correo electrónico mediante una función denominada suscripciones.

Las suscripciones son similares a [las notificaciones](notifications.md) , ya que los miembros pueden suscribirse a continuación de artículos de blog, temas de foro o preguntas de control de calidad.

Lo que distingue las suscripciones de las notificaciones es:

* Los Miembros no podrán suscribirse cuando sigan a otros miembros
* La única acción que deben realizar los miembros es seleccionar `Email Subscriptions` al
* Cuando se configura la respuesta por correo electrónico, los miembros pueden publicar contenido de forma eficaz simplemente respondiendo al correo electrónico recibido

### Requisitos {#requirements}

**Configurar correo electrónico**

El correo electrónico debe configurarse para que las suscripciones funcionen y para que los miembros respondan por correo electrónico.

Para obtener instrucciones sobre cómo configurar el correo electrónico, consulte [Configuración del correo electrónico](email.md).

**Habilitar suscripciones y seguir**

Los componentes deben configurarse para habilitar las suscripciones *y las* siguientes. Las funciones que permiten suscripciones son [blog](blog-feature.md), [foro](forum.md) y [QnA](working-with-qna.md).

## Suscripciones desde: {#subscriptions-from-following}

![climage_1-5](assets/chlimage_1-5.png)

El botón **Seguir** proporciona un medio para seguir las entradas como actividades, suscripciones y/o notificaciones. Cada vez que se selecciona el botón **Seguir** , es posible activar o desactivar una selección.

Si se selecciona cualquier método de seguimiento, el texto del botón cambia a **Siguiente**. Para mayor comodidad, es posible seleccionar `Unfollow All` desactivar todos los métodos.

El botón **Seguir** incluirá la `Email Subscriptions` opción solo cuando se configure un foro, un control de calidad o un blog para habilitar las suscripciones por correo electrónico. Aparecerá este botón

* En la página de características principal del foro, control de calidad o blog habilitado

   * Enviará un mensaje de correo electrónico para todas las actividades de esa función

* Para una entrada específica, como un tema del foro, una pregunta de preguntas y respuestas o un artículo del blog

   * Enviará un correo electrónico cuando haya actividad para esa entrada específica

## Responder por correo electrónico {#reply-by-email}

Cuando se [configura el correo electrónico para responder por correo electrónico](email.md#configure-polling-importer), el miembro que se suscribió recibirá un correo electrónico con el contenido publicado y un vínculo al contenido en línea.

Si responden al correo electrónico, el contenido que introduzcan en la respuesta aparecerá como contenido en línea.

![climage_1-6](assets/chlimage_1-6.png)

El intervalo [de actualización del importador de](email.md#configure-polling-importer)encuestas controla la cantidad de tiempo que tarda una respuesta en anunciarse.

![climage_1-7](assets/chlimage_1-7.png)

