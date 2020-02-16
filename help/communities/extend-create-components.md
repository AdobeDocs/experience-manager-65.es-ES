---
title: Crear los componentes
seo-title: Crear los componentes
description: Creación del componente Comentarios
seo-description: Creación del componente Comentarios
uuid: ea6e00d4-1db7-40ef-ae49-9ec55df58adf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 83c4f18a-d7d6-4090-88c7-41a9075153b5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Crear los componentes {#create-the-components}

El ejemplo de ampliación de componentes utiliza el sistema de comentarios, que en realidad está compuesto por dos componentes

* Comentarios: el sistema de comentarios que incluye el componente colocado en una página
* Comentario: componente que captura una instancia de un comentario publicado

Ambos componentes deben implementarse, especialmente si se personaliza el aspecto de un comentario publicado.

>[!NOTE]
>
>Solo se permite un sistema de comentarios por página del sitio.
>
>Muchas funciones de Comunidades ya incluyen un sistema de comentarios cuyo resourceType puede modificarse para hacer referencia al sistema de comentarios ampliado.

## Creación del componente Comentarios {#create-the-comments-component}

Estas direcciones especifican un valor de **grupo** distinto de `.hidden` modo que el componente puede estar disponible desde el navegador de componentes (barra de tareas).

La eliminación del archivo JSP creado automáticamente se debe a que se utilizará el archivo HBS predeterminado.

1. Vaya a **CRXDE|Lite** ([http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp))

1. Cree una ubicación para las aplicaciones personalizadas:

   * Seleccione el `/apps` nodo

      * **Crear carpeta** con el nombre **[!UICONTROL personalizado]**
   * Seleccione el `/apps/custom` nodo

      * **Crear carpeta** con **[!UICONTROL componentes con nombre]**


1. Seleccione el `/apps/custom/components` nodo

   * **[!UICONTROL Crear > Componente...]**

      * **Etiqueta**: *comentarios*
      * **Título**: Comentarios *alternativos*
      * **Descripción**: Estilo de comentarios *alternativos*
      * **Super Tipo**: *social/commons/components/hbs/comments*
      * **Grupo**: *Personalizado*
   * Seleccione **[!UICONTROL Siguiente]**
   * Seleccione **[!UICONTROL Siguiente]**
   * Seleccione **[!UICONTROL Siguiente]**
   * Seleccione **[!UICONTROL Aceptar]**


1. Expanda el nodo recién creado: `/apps/custom/components/comments`
1. Seleccione **[!UICONTROL Guardar todo]**
1. Clic con el botón derecho `comments.jsp`
1. Seleccionar **[!UICONTROL eliminación]**
1. Seleccione **[!UICONTROL Guardar todo]**

![chlimage_1-70](assets/chlimage_1-70.png)

### Crear el componente de comentario secundario {#create-the-child-comment-component}

Estas instrucciones establecen **Agrupar** en `.hidden` como si solo se incluyera el componente principal en una página.

La eliminación del archivo JSP creado automáticamente se debe a que se utilizará el archivo HBS predeterminado.

1. Navegar al `/apps/custom/components/comments` nodo
1. Haga clic con el botón secundario en el nodo

   * Seleccione **[!UICONTROL Crear > Componente...]**

      * **Etiqueta**: *comentario*
      * **Título**: Comentario *alternativo*
      * **Descripción**: Estilo de comentario *alternativo*
      * **Super Tipo**: *social/commons/components/hbs/comments/comment*
      * **Agrupar**: `*.hidden*`
   * Seleccione **[!UICONTROL Siguiente]**
   * Seleccione **[!UICONTROL Siguiente]**
   * Seleccione **[!UICONTROL Siguiente]**
   * Seleccione **[!UICONTROL Aceptar]**


1. Expanda el nodo recién creado: `/apps/custom/components/comments/comment`
1. Seleccione **[!UICONTROL Guardar todo]**
1. Clic con el botón derecho `comment.jsp`
1. Seleccionar **[!UICONTROL eliminación]**
1. Seleccione **[!UICONTROL Guardar todo]**

![chlimage_1-71](assets/chlimage_1-71.png) ![chlimage_1-72](assets/chlimage_1-72.png)

### Copiar y modificar los scripts HBS predeterminados {#copy-and-modify-the-default-hbs-scripts}

Uso de [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Copiar `comments.hbs`

   * De [/libs/social/commons/components/hbs/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * Para [/aplicaciones/custom/components/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* Editar `comments.hbs` a:

   * Cambie el valor del `data-scf-component` atributo (~línea 20):

      * De `social/commons/components/hbs/comments`
      * A `/apps/custom/components/comments`
   * Modifique para incluir el componente de comentario personalizado (~línea 75):

      * Reemplazar `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * Mediante una de las opciones siguientes `{{include this resourceType='/apps/custom/components/comments/comment'}}`


* Copiar `comment.hbs`

   * De [/libs/social/commons/components/hbs/comments/comment](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * Para [/aplicaciones/custom/components/comments/comment](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* Editar `comment.hbs` a:

   * Cambiar el valor del atributo data-scf-component (~ línea 19)

      * De `social/commons/components/hbs/comments/comment`
      * A `/apps/custom/components/comments/comment`

* Seleccionar `/apps/custom` nodo
* Seleccione **[!UICONTROL Guardar todo]**

## Crear una carpeta de biblioteca de clientes {#create-a-client-library-folder}

Para evitar tener que incluir explícitamente esta biblioteca de cliente, se podría usar el valor de categorías para la clientlib del sistema de comentarios predeterminado ( `cq.social.author.hbs.comments`), pero entonces esta clientlib también se incluiría para todas las instancias del componente predeterminado.

Uso de [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Seleccionar `/apps/custom/components/comments` nodo
* Seleccione **[!UICONTROL Crear nodo]**

   * **Nombre**: `clientlibs`
   * **Tipo**: `cq:ClientLibraryFolder`
   * Agregar a la ficha **[!UICONTROL Propiedades]** :

      * **Nombre** `categories` Tipo **** Valor `String` **** `cq.social.author.hbs.comments``Multi`
      * **Nombre** `dependencies` Tipo **** Valor `String` **** `cq.social.scf``Multi`

* Seleccione **[!UICONTROL Guardar todo]**
* Con `/apps/custom/components/comments/clientlib`el nodo s seleccionado, cree 3 archivos:

   * **Nombre**: `css.txt`
   * **Nombre**: `js.txt`
   * **Nombre**: custom comentsystem.js

* Especifique &#39;customcomentsystem.js&#39; como contenido de `js.txt`
* Seleccione **[!UICONTROL Guardar todo]**

![chlimage_1-73](assets/chlimage_1-73.png)

## Registrar el modelo y la vista de SCF {#register-the-scf-model-view}

Al ampliar (anular) un componente SCF, resourceType es diferente (al superponer se utiliza el mecanismo de búsqueda relativo que busca `/apps` antes `/libs` para que resourceType siga siendo el mismo). Por este motivo, es necesario escribir JavaScript (en la biblioteca del cliente) para registrar el modelo JS SCF y ver el resourceType personalizado.

Escriba el siguiente texto como contenido de `customcommentsystem.js`:

### custom comentsystem.js {#customcommentsystem-js}

```xml
(function($CQ, _, Backbone, SCF) {
    "use strict";

    var CustomComment = SCF.Components["social/commons/components/hbs/comments/comment"].Model;
    var CustomCommentView = SCF.Components["social/commons/components/hbs/comments/comment"].View;

    var CustomCommentSystem = SCF.Components["social/commons/components/hbs/comments"].Model;
    var CustomCommentSystemView = SCF.Components["social/commons/components/hbs/comments"].View;

    SCF.registerComponent('/apps/custom/components/comments/comment', CustomComment, CustomCommentView);
    SCF.registerComponent('/apps/custom/components/comments', CustomCommentSystem, CustomCommentSystemView);

})($CQ, _, Backbone, SCF);
```

* Seleccione **[!UICONTROL Guardar todo]**

## Publicar la aplicación {#publish-the-app}

Para poder experimentar el componente extendido en el entorno de publicación, es necesario replicar el componente personalizado.

Una manera de hacerlo es

* Desde la navegación global

   * Seleccione **[!UICONTROL Herramientas > Implementación > Replicación]**
   * Seleccione `Activate Tree`
   * Definir `Start Path`: to `/apps/custom`
   * Desmarcar `Only Modified`
   * Seleccionar `Activate`botón

