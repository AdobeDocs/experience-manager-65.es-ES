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
source-wordcount: '400'
ht-degree: 0%
---
# Agregar comentario a página de muestra  {#add-comment-to-sample-page}

Ahora que los componentes del sistema de comentarios personalizado están en el directorio de la aplicación (/apps), es posible utilizar el componente ampliado. La instancia del sistema de comentarios de un sitio web que se va a ver afectado debe establecer su resourceType para que sea el sistema de comentarios personalizado e incluir todas las bibliotecas de cliente necesarias.

## Identificar Clientlibs Requeridos {#identify-required-clientlibs}

Las bibliotecas de cliente necesarias para el estilo y el funcionamiento de los comentarios predeterminados también son necesarias para los comentarios ampliados.

La [Guía de componentes de la comunidad](/help/communities/components-guide.md) identifica las bibliotecas de cliente necesarias. Vaya a la Guía de componentes y vea el componente Comentarios, por ejemplo:

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

Tenga en cuenta las tres bibliotecas de cliente necesarias para que los comentarios se representen y funcionen correctamente. Se deben incluir donde se hace referencia a los Comentarios extendidos y a la biblioteca de cliente de [Comentarios extendidos](/help/communities/extend-create-components.md#create-a-client-library-folder) ( `apps.custom.comments`).

![comentarios-componente1](assets/comments-component1.png)

### Agregar comentarios personalizados a una página {#add-custom-comments-to-a-page}

Como solo puede haber un sistema de comentarios por página, es más sencillo crear una página de muestra como se describe en el tutorial breve [crear una página de muestra](/help/communities/create-sample-page.md).

Una vez creado, introduzca el modo de diseño y active el grupo de componentes personalizados para permitir que se agregue el componente `Alt Comments` a la página.

Para que Comment aparezca y funcione correctamente, las bibliotecas de cliente para Comments deben agregarse a la lista clientlibs de la página (consulte [Clientlibs para componentes de Communities](/help/communities/clientlibs.md)).

#### Comentarios de Clientlibs en la página de muestra {#comments-clientlibs-on-sample-page}

![comments-clientlibs-crxde](assets/comments-clientlibs-crxde.png)

#### Autor: comentar de forma alternativa en la página de muestra {#author-alt-comment-on-sample-page}

![alt-comment](assets/alt-comment.png)

#### Autor: Nodo de comentarios de página de muestra {#author-sample-page-comments-node}

Puede comprobar el resourceType en CRXDE si ve las propiedades del nodo de comentarios de la página de muestra en `/content/sites/sample/en/jcr:content/content/primary/comments`.

![verify-comment-crxde](assets/verify-comment-crxde.png)

#### Publicar página de muestra {#publish-sample-page}

Una vez agregado el componente personalizado a la página, también es necesario [volver a publicar la página](/help/communities/sites-console.md#publishing-the-site).

#### Publicar: comentar de forma alternativa en la página de muestra {#publish-alt-comment-on-sample-page}

Después de publicar la aplicación personalizada y la página de muestra, es posible introducir un comentario. Cuando se inicia sesión, ya sea con un [usuario de demostración](/help/communities/tutorials.md#demo-users) o administrador, es posible publicar un comentario.

Aquí está aaron.mcdonald@mailinator.com publicando un comentario:

![publish-alt-comment](assets/publish-alt-comment.png)

![publish-alt-comment1](assets/publish-alt-comment1.png)

Ahora que parece que el componente ampliado funciona correctamente con la apariencia predeterminada, es hora de modificar la apariencia.
