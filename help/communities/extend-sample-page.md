---
title: Agregar comentario a página de muestra
description: Descubra cómo una instancia del sistema de comentarios de un sitio web debe establecer su resourceType para que sea el sistema de comentarios personalizado e incluir todas las bibliotecas de cliente necesarias.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: d4295a77-b931-4bc8-b3b4-eec42fdcfc56
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# Agregar comentario a página de muestra  {#add-comment-to-sample-page}

Ahora que los componentes del sistema de comentarios personalizado están en el directorio de la aplicación (/apps), es posible utilizar el componente ampliado. La instancia del sistema de comentarios de un sitio web que se va a ver afectado debe establecer su resourceType para que sea el sistema de comentarios personalizado e incluir todas las bibliotecas de cliente necesarias.

## Identificar Clientlibs Requeridos {#identify-required-clientlibs}

Las bibliotecas de cliente necesarias para el estilo y el funcionamiento de los comentarios predeterminados también son necesarias para los comentarios ampliados.

El [Guía de componentes de la comunidad](/help/communities/components-guide.md) identifica las bibliotecas de cliente necesarias. Vaya a la Guía de componentes y vea el componente Comentarios, por ejemplo:

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

Tenga en cuenta las tres bibliotecas de cliente necesarias para que los comentarios se representen y funcionen correctamente. Se deben incluir cuando se haga referencia a los comentarios ampliados y la variable [biblioteca de cliente de comentarios extendidos](/help/communities/extend-create-components.md#create-a-client-library-folder) ( `apps.custom.comments`).

![comments-component1](assets/comments-component1.png)

### Agregar comentarios personalizados a una página {#add-custom-comments-to-a-page}

Como solo puede haber un sistema de comentarios por página, es más sencillo crear una página de muestra como se describe en la información [crear una página de muestra](/help/communities/create-sample-page.md) tutorial.

Una vez creado, introduzca el modo de diseño y active el grupo de componentes personalizados para permitir el `Alt Comments` componente que se añadirá a la página.

Para que Comment aparezca y funcione correctamente, las bibliotecas de cliente para Comments deben agregarse a la lista clientlibs de la página (consulte [Componentes de Clientlibs para Communities](/help/communities/clientlibs.md)).

#### Comentarios de Clientlibs en la página de muestra {#comments-clientlibs-on-sample-page}

![comments-clientlibs-crxde](assets/comments-clientlibs-crxde.png)

#### Autor: comentar de forma alternativa en la página de muestra {#author-alt-comment-on-sample-page}

![alt-comment](assets/alt-comment.png)

#### Autor: Nodo de comentarios de página de muestra {#author-sample-page-comments-node}

Puede comprobar el resourceType en CRXDE si ve las propiedades del nodo de comentarios de la página de ejemplo en `/content/sites/sample/en/jcr:content/content/primary/comments`.

![verify-comment-crxde](assets/verify-comment-crxde.png)

#### Publicar página de muestra {#publish-sample-page}

Una vez agregado el componente personalizado a la página, también es necesario (re) [publicar la página](/help/communities/sites-console.md#publishing-the-site).

#### Publicar: comentar de forma alternativa en la página de muestra {#publish-alt-comment-on-sample-page}

Después de publicar la aplicación personalizada y la página de muestra, es posible introducir un comentario. Cuando se inicia sesión, ya sea con una [usuario de demostración](/help/communities/tutorials.md#demo-users) Para el administrador, es posible publicar un comentario.

Aquí está aaron.mcdonald@mailinator.com publicando un comentario:

![publish-alt-comment](assets/publish-alt-comment.png)

![publish-alt-comment1](assets/publish-alt-comment1.png)

Ahora que parece que el componente ampliado funciona correctamente con la apariencia predeterminada, es hora de modificar la apariencia.
