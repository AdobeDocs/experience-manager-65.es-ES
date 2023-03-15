---
title: Elementos básicos del editor de texto enriquecido
seo-title: Rich Text Editor Essentials
description: Resumen de las funciones del Editor de texto enriquecido
seo-description: Rich text Editor feature overview
uuid: f96015cc-114b-431a-a5ba-dc195c2a0b83
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0225a543-0fad-488b-8b0b-8b3512d44fbe
exl-id: 821e32f4-da8d-4bbb-936a-0844b8a24cdd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 3%

---

# Elementos básicos del editor de texto enriquecido {#rich-text-editor-essentials}

## Información general {#overview}

Un editor de texto enriquecido (RTE) permite introducir texto con marcado.

Para los componentes de Communities, aunque es similar a la [editor de texto enriquecido en el entorno de creación](../../help/sites-authoring/rich-text-editor.md), afecta al texto introducido en el entorno de publicación.

![editor de texto enriquecido](assets/rich-text-editor.png)

## Habilitar el editor de texto enriquecido {#enabling-rich-text-editor}

Los componentes de las comunidades que permiten contenido generado por el usuario (UGC) se pueden habilitar para permitir RTE. En función de si el componente se añadió a una página o se incluyó en una [función](functions.md), RTE puede estar o no habilitado de forma predeterminada.

Si no está activada, simplemente introduzca [modo de edición de autor](sites-console.md#authoring-site-content), seleccione el componente para editarlo y seleccione el `Rich Text Editor` casilla de verificación

RTE está disponible para los siguientes componentes de Communities:

* [Blog](blog-feature.md)
* [Calendario](calendar.md)
* [Comentarios](comments.md)
* [Filelibrary](file-library.md)
* [Foro](forum.md)
* [Mensajes](configure-messaging.md)
* [P y R](working-with-qna.md)
* [Críticas](reviews.md)

## Personalización {#customization}

La personalización del editor de texto enriquecido es posible porque la implementación se basa en lo siguiente [CKEditor](https://www.ckeditor.com/).

La configuración actual de los componentes de Communities se encuentra en `cq.social.  scf   clientlib`, ubicado en el repositorio en

`/libs/clientlibs/social/commons/scf/ckrte.js`

No se recomienda modificar cq.social.scf clientlib, ya que las futuras actualizaciones pueden anular las ediciones.

### Personalización de ejemplo: Vínculos en línea {#example-customization-inline-links}

Por motivos de seguridad, las opciones de hipervínculos no se incluyen en el conjunto de iconos de texto enriquecido que se presentan a los miembros de forma predeterminada. La capacidad para la travesura es extensa cuando se permiten hrefs en UGC.

Para agregar las opciones de hipervínculo a la barra de herramientas:

* Añada una barra de herramientas denominada &quot; `links`&quot;
   * `{ name: 'links', items: [ 'Link','Unlink','Anchor' ] }`
* Seleccionar **[!UICONTROL Guardar todo]**

#### /libs/clientlibs/social/commons/scf/ckrte.js {#libs-clientlibs-social-commons-scf-ckrte-js}

```
CKRte.prototype.config = {
    toolbar: [
        { name: "basicstyles",
           items: ["Bold", "Italic", "Underline", "NumberedList", "BulletedList", "Outdent", "Indent", "JustifyLeft", "JustifyCenter", "JustifyRight", "JustifyBlock", "TextColor"]
        },
        { name: 'links',
           items: [ 'Link','Unlink','Anchor' ]
        }
    ],
    autoParagraph: false,
    autoUpdateElement: false,
    removePlugins: "elementspath",
    resize_enabled: false
};
```
