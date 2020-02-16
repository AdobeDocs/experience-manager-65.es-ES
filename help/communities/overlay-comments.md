---
title: Componentes de comunidades de superposición
seo-title: Componentes de comunidades de superposición
description: Componentes de comunidades de superposición
seo-description: Componentes de comunidades de superposición
uuid: 872f7006-959a-49d2-b025-3a5abb7c6dca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 502c0916-6c54-440c-be8c-eae56001fa26
docset: aem65
translation-type: tm+mt
source-git-commit: 70e6f2d8366456e5091b7b775dc40914948921ab

---


# Componentes de comunidades de superposición {#overlay-communities-components}

La intención de [superponer](/help/communities/client-customize.md#overlays) un componente predeterminado es alterar el aspecto o el comportamiento de un componente globalmente, para todas las referencias relativas al componente. Depende de la naturaleza de sling para resolver en la carpeta /apps antes de buscar en la carpeta /libs. Por lo tanto, la ruta del componente es idéntica a la ruta del componente predeterminado, excepto que se encuentra en la carpeta /apps y no en la carpeta /libs.

## Ejemplo {#example}

**Componente de comentarios de superposición**

Supongamos que desea modificar la función de comentarios para que coincida con el diseño de su sitio web, cambiando el encabezado de comentario para que ya no muestre el avatar de ningún comentario. Las soluciones para ocultar el avatar utilizan CSS o, como se describe aquí, superponen header.jsp en la carpeta de aplicaciones para que el HTML que contiene el avatar nunca se envíe al cliente.

Para superponer comentarios, deberá:

1. [Página de comentarios](/help/communities/overlay-create-comments-page.md)
1. [Crear nodos](/help/communities/overlay-create-nodes.md)
1. [Modificar el aspecto](/help/communities/overlay-alter-appearance.md)

**Correos electrónicos de notificaciones de superposición**

Supongamos que desea personalizar el mensaje de las notificaciones por correo electrónico, puede [superponer](/help/communities/client-customize.md#overlays) las plantillas en **/libs/settings/community/templates/email/html**.

Por ejemplo, para modificar las notificaciones de correo electrónico de menciones (para un componente de comunidades específicas en el que se crea ugc), agregue una** si **condición para la **mención verbo** en las plantillas de los componentes para los que habilitó la compatibilidad con **@mentions** .

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

Para modificar la plantilla de notificaciones de correo electrónico para @uncia en los comentarios del blog, coloque la plantilla predeterminada en: **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/es**
