---
title: Componentes de comunidades de superposición
seo-title: Overlay communities components
description: Componentes de comunidades de superposición
seo-description: Overlay communities components
uuid: 872f7006-959a-49d2-b025-3a5abb7c6dca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 502c0916-6c54-440c-be8c-eae56001fa26
docset: aem65
exl-id: 18376805-c2ed-439a-abc7-e9657afe8baf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# Componentes de comunidades de superposición {#overlay-communities-components}

La intención de [superposición](/help/communities/client-customize.md#overlays) un componente predeterminado es modificar el aspecto o el comportamiento de un componente globalmente, para todas las referencias relativas al componente. Depende de la naturaleza de sling para resolver la carpeta /apps antes de buscar en la carpeta /libs. Por lo tanto, la ruta al componente es idéntica a la ruta al componente predeterminado, excepto que está en la carpeta /apps y no en la carpeta /libs.

## Ejemplo {#example}

**Componente de comentarios de superposición**

Supongamos que desea modificar la función de comentarios para que coincida con el diseño del sitio web, cambiando el encabezado de los comentarios para que ya no muestre el avatar de ningún comentario. Las soluciones para ocultar el avatar utilizan CSS o, como se describe aquí, superponen header.jsp en la carpeta de aplicaciones para que el HTML que contiene el avatar no se envíe nunca al cliente.

Para superponer comentarios, deberá:

1. [Página Comentarios](/help/communities/overlay-create-comments-page.md)
1. [Crear nodos](/help/communities/overlay-create-nodes.md)
1. [Modificar el aspecto](/help/communities/overlay-alter-appearance.md)

**Correos electrónicos de notificaciones de superposición**

Supongamos que desea personalizar el mensaje de las notificaciones por correo electrónico, puede hacerlo mediante [superposición](/help/communities/client-customize.md#overlays) las plantillas en **/libs/settings/community/templates/email/html**.

Por ejemplo, para modificar las menciones, envíe notificaciones por correo electrónico (para un componente de comunidades específicas donde se crea ugc) y añada una **if** condición para verbo **mención** en las plantillas de los componentes para los que ha habilitado el **@mentions** asistencia técnica.

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

Para modificar la plantilla de notificaciones de correo electrónico para @mention en comentarios de blog, coloque la plantilla predeterminada en: `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
