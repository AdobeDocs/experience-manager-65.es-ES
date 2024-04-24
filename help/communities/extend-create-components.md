---
title: Creación de componentes
description: Obtenga información sobre cómo ampliar componentes mediante el sistema de comentarios, que está compuesto por los componentes Comentarios y Comentarios.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 2e02db9f-294d-4d4a-92da-3ab1d38416ab
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 0%

---

# Creación de componentes  {#create-the-components}

El ejemplo de ampliación de componentes utiliza el sistema de comentarios, que está compuesto por dos componentes.

* Comentarios: el sistema de comentarios envolvente que es el componente colocado en una página.
* Comentario: componente que captura una instancia de un comentario publicado.

Ambos componentes deben ponerse en marcha, especialmente si se personaliza la apariencia de un comentario publicado.

>[!NOTE]
>
>Solo se permite un sistema de comentarios por página de sitio.
>
>Muchas funciones de Communities ya incluyen un sistema de comentarios cuyo resourceType se puede modificar para hacer referencia al sistema de comentarios ampliado.

## Creación del componente Comentarios {#create-the-comments-component}

Estas instrucciones especifican una **Grupo** valor distinto de `.hidden` por lo tanto, el componente puede estar disponible desde el explorador de componentes (barra de tareas).

La eliminación del archivo JSP creado automáticamente se debe a que se utiliza el archivo HBS predeterminado en su lugar.

1. Navegar a **CRXDE|Lite** ([http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp))

1. Cree una ubicación para las aplicaciones personalizadas:

   * Seleccione el `/apps` nodo

      * **Crear carpeta** nombrado **[!UICONTROL personalizado]**

   * Seleccione el `/apps/custom` nodo

      * **Crear carpeta** nombrado **[!UICONTROL componentes]**

1. Seleccione el `/apps/custom/components` nodo

   * **[!UICONTROL Crear > Componente...]**

      * **Etiqueta**: *comentarios*
      * **Título**: *Comentarios Alt*
      * **Descripción**: *Estilo de comentarios alternativos*
      * **Super Type**: *social/commons/components/hbs/comments*
      * **Grupo**: *Personalizado*

   * Seleccionar **[!UICONTROL Siguiente]**
   * Seleccionar **[!UICONTROL Siguiente]**
   * Seleccionar **[!UICONTROL Siguiente]**
   * Seleccionar **[!UICONTROL OK]**

1. Expanda el nodo que ha creado: `/apps/custom/components/comments`
1. Seleccionar **[!UICONTROL Guardar todo]**
1. Clic con el botón derecho `comments.jsp`
1. Seleccionar **[!UICONTROL Eliminar]**
1. Seleccionar **[!UICONTROL Guardar todo]**

![create-component](assets/create-component.png)

### Creación del componente Comentario secundario {#create-the-child-comment-component}

Estas direcciones se establecen **Grupo** hasta `.hidden` ya que solo el componente principal debe incluirse en una página.

La eliminación del archivo JSP creado automáticamente se debe a que se utiliza el archivo HBS predeterminado en su lugar.

1. Vaya a `/apps/custom/components/comments` nodo
1. Haga clic con el botón derecho en el nodo

   * Seleccionar **[!UICONTROL Crear]** > **[!UICONTROL Componente...]**

      * **Etiqueta**: *comentario*
      * **Título**: *Alt comentario*
      * **Descripción**: *Estilo de comentario alternativo*
      * **Super Type**: *social/commons/components/hbs/comments/comment*
      * **Grupo**: `*.hidden*`

   * Seleccionar **[!UICONTROL Siguiente]**
   * Seleccionar **[!UICONTROL Siguiente]**
   * Seleccionar **[!UICONTROL Siguiente]**
   * Seleccionar **[!UICONTROL OK]**

1. Expanda el nodo que ha creado: `/apps/custom/components/comments/comment`
1. Seleccionar **[!UICONTROL Guardar todo]**
1. Clic con el botón derecho `comment.jsp`
1. Seleccionar **[!UICONTROL Eliminar]**
1. Seleccionar **[!UICONTROL Guardar todo]**

![create-child-component](assets/create-child-component.png)

![create-component-crxde](assets/create-component-crxde.png)

### Copiar y modificar scripts HBS predeterminados {#copy-and-modify-the-default-hbs-scripts}

Uso de [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Copie `comments.hbs`

   * Desde [/libs/social/commons/components/hbs/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * Hasta [/apps/custom/components/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* Editar `comments.hbs` hasta:

   * Cambie el valor del `data-scf-component` atributo (~línea 20):

      * Desde `social/commons/components/hbs/comments`
      * Hasta `/apps/custom/components/comments`

   * Modifique para incluir el componente de comentario personalizado (línea 75):

      * Reemplazar `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * Con `{{include this resourceType='/apps/custom/components/comments/comment'}}`

* Copie `comment.hbs`

   * Desde [/libs/social/commons/components/hbs/comments/comment](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * Hasta [/apps/custom/components/comments/comment](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* Editar `comment.hbs` hasta:

   * Cambie el valor del atributo data-scf-component (~ línea 19)

      * Desde `social/commons/components/hbs/comments/comment`
      * Hasta `/apps/custom/components/comments/comment`

* Seleccionar `/apps/custom` nodo
* Seleccionar **[!UICONTROL Guardar todo]**

## Crear una carpeta de biblioteca de cliente {#create-a-client-library-folder}

Para evitar tener que incluir esta biblioteca de cliente, se puede utilizar el valor categories para la clientlib del sistema de comentarios predeterminado ( `cq.social.author.hbs.comments`). Sin embargo, esta clientlib también tendría que incluirse para todas las instancias del componente predeterminado.

Uso de [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Seleccionar `/apps/custom/components/comments` nodo
* Seleccionar **[!UICONTROL Crear nodo]**

   * **Nombre**: `clientlibs`
   * **Tipo**: `cq:ClientLibraryFolder`
   * Añadir a **[!UICONTROL Propiedades]** pestaña:

      * **Nombre** `categories` **Tipo** `String` **Valor** `cq.social.author.hbs.comments` `Multi`
      * **Nombre** `dependencies` **Tipo** `String` **Valor** `cq.social.scf` `Multi`

* Seleccionar **[!UICONTROL Guardar todo]**
* Con `/apps/custom/components/comments/clientlib`Como nodo seleccionado, cree tres archivos:

   * **Nombre**: `css.txt`
   * **Nombre**: `js.txt`
   * **Nombre**: customcomentsystem.js

* Escriba &quot;customcomment.js&quot; como contenido de `js.txt`
* Seleccionar **[!UICONTROL Guardar todo]**

![comments-clientlibs](assets/comments-clientlibs.png)

## Registrar el modelo y vista de SCF {#register-the-scf-model-view}

Al ampliar (anular) un componente SCF, el resourceType es diferente (la superposición utiliza el mecanismo de búsqueda relativa que busca a través de `/apps` antes `/libs` para que resourceType siga siendo el mismo). Por este motivo, es necesario escribir JavaScript (en la biblioteca de cliente) para registrar el modelo JS de SCF y la vista para el resourceType personalizado.

Escriba el siguiente texto como contenido de `customcommentsystem.js`:

### customcommentsystem.js {#customcommentsystem-js}

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

* Seleccionar **[!UICONTROL Guardar todo]**

## Publicar la aplicación {#publish-the-app}

Para experimentar el componente ampliado en el entorno de publicación, es necesario replicar el componente personalizado.

Una forma de hacerlo es:

* Desde la navegación global,

   * Seleccionar **[!UICONTROL Herramientas]** > **[!UICONTROL Implementación]** > **[!UICONTROL Replicación]**
   * Seleccionar **[!UICONTROL Activar árbol]**
   * Establecer `Start Path` hasta `/apps/custom`
   * Desmarcar **[!UICONTROL Solo modificadas]**
   * Seleccionar **[!UICONTROL Activar]** botón
