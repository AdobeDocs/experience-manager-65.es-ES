---
title: Superponer componentes de Communities
description: Obtenga información sobre la superposición de un componente predeterminado para poder modificar el aspecto o el comportamiento de un componente globalmente, para todas las referencias relativas al componente.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 18376805-c2ed-439a-abc7-e9657afe8baf
solution: Experience Manager
feature: Communities
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%
---
# Superponer componentes de Communities {#overlay-communities-components}

La intención de [superponer](/help/communities/client-customize.md#overlays) un componente predeterminado es modificar el aspecto o el comportamiento de un componente globalmente, para todas las referencias relativas al componente. Se basa en la naturaleza de sling para resolver en la carpeta /apps antes de buscar en la carpeta /libs. Por lo tanto, la ruta al componente es idéntica a la ruta al componente predeterminado, excepto que se encuentra en la carpeta /apps y no en la carpeta /libs.

## Ejemplo {#example}

**Componente de comentarios de superposición**

Supongamos que desea modificar la función de comentarios para que coincida con el diseño del sitio web, cambiando el encabezado del comentario para que ya no muestre el avatar de ningún comentario. Las soluciones para ocultar el avatar utilizan CSS o, como se describe aquí, superponen header.jsp en la carpeta de aplicaciones para que el HTML que contiene el avatar nunca se envíe al cliente.

Para superponer comentarios, debe:

1. [Página Crear Comentarios](/help/communities/overlay-create-comments-page.md)
1. [Crear nodos](/help/communities/overlay-create-nodes.md)
1. [Modificar el aspecto](/help/communities/overlay-alter-appearance.md)

**Correos electrónicos de notificaciones de superposición**

Supongamos que desea personalizar el mensaje de las notificaciones por correo electrónico, para ello, [superponga](/help/communities/client-customize.md#overlays) las plantillas en `/libs/settings/community/templates/email/html`.

Por ejemplo, supongamos que desea editar las notificaciones de las menciones por correo electrónico (para un componente específico de Communities en el que se crea UGC). En estos casos, agregue una condición **if** para el verbo **mención** en las plantillas de los componentes para los que habilitó la compatibilidad con **@mentions**.

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

Para modificar la plantilla de notificaciones de correo electrónico para @mention en comentarios de blog, coloque la plantilla predeterminada en: `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
