---
title: Elementos esenciales del editor de texto enriquecido
seo-title: Elementos esenciales del editor de texto enriquecido
description: Descripción general de la función Editor de texto enriquecido
seo-description: Descripción general de la función Editor de texto enriquecido
uuid: f96015cc-114b-431a-a5ba-dc195c2a0b83
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0225a543-0fad-488b-8b0b-8b3512d44fbe
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Rich Text Editor Essentials {#rich-text-editor-essentials}

## Información general {#overview}

Un editor de texto enriquecido (RTE) permite introducir texto con marcado.

En el caso de los componentes Communities, aunque es similar al editor de texto [enriquecido del entorno](../../help/sites-authoring/rich-text-editor.md)de creación, afecta al texto introducido en el entorno de publicación.

![chlimage_1-410](assets/chlimage_1-410.png)

## Enabling Rich Text Editor {#enabling-rich-text-editor}

Los componentes de comunidades que permiten contenido generado por el usuario (UGC) pueden habilitarse para permitir RTE. Dependiendo de si el componente se agregó a una página o se incluyó en una [función](functions.md), RTE puede habilitarse o no de forma predeterminada.

Si no está activado, simplemente ingrese al modo [de edición del](sites-console.md#authoring-site-content)autor, seleccione el componente para editar y seleccione la `Rich Text Editor` casilla de verificación.

RTE está disponible para los siguientes componentes de Comunidades:

* [Blog](blog-feature.md)
* [Calendario](calendar.md)
* [Comentarios](comments.md)
* [Filelibrary](file-library.md)
* [Foro](forum.md)
* [Mensajes](configure-messaging.md)
* [P y R](working-with-qna.md)
* [Críticas](reviews.md)

## Personalización {#customization}

La personalización del editor de texto enriquecido es posible, ya que la implementación se basa en [CKEditor](https://www.ckeditor.com/).

La configuración actual de los componentes de Communities está en la `cq.social.  scf   clientlib`, ubicada en el repositorio en

`/libs/clientlibs/social/commons/scf/ckrte.js`

No se recomienda modificar la clientlib cq.social.scf, ya que las futuras actualizaciones pueden anular cualquier edición.

### Ejemplo de personalización: Vínculos en línea {#example-customization-inline-links}

Debido a problemas de seguridad, las opciones de hipervínculo no se incluyen en el conjunto de iconos de texto enriquecido que se presentan a los miembros de forma predeterminada. La capacidad para causar daños es amplia cuando se permiten hrefs en UGC.

Para agregar las opciones de hipervínculo a la barra de herramientas:

* Agregar una barra de herramientas con el nombre &quot; `links`&quot;
   * `{ name: 'links', items: [ 'Link','Unlink','Anchor' ] }`
* Seleccione **[!UICONTROL Guardar todo]**

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

