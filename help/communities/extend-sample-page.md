---
title: Agregar comentario a una página de muestra
seo-title: Add Comment to Sample Page
description: Agregar comentarios personalizados a una página
seo-description: Add Custom Comments to a page
uuid: ab258960-6de2-4943-80a7-e72904c0fd8e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a5040371-3bc2-43bc-a103-7175c4c6252d
docset: aem65
exl-id: d4295a77-b931-4bc8-b3b4-eec42fdcfc56
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Agregar comentario a una página de muestra  {#add-comment-to-sample-page}

Ahora que los componentes del sistema de comentarios personalizados están en su lugar en el directorio de aplicaciones (/apps), es posible utilizar el componente ampliado. La instancia del sistema de comentarios de un sitio web afectado debe establecer su resourceType como sistema de comentarios personalizado e incluir todas las bibliotecas de cliente necesarias.

## Identificar Clientlibs Necesarios {#identify-required-clientlibs}

Las bibliotecas de cliente necesarias para el estilo y funcionamiento de los Comentarios predeterminados también son necesarias para los Comentarios extendidos.

La variable [Guía de componentes de comunidad](/help/communities/components-guide.md) identifica las bibliotecas de cliente necesarias. Vaya a la Guía del componente y vea el componente Comentarios, por ejemplo:

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

Tenga en cuenta las tres bibliotecas de cliente necesarias para que Comentarios se procese y funcione correctamente. Tendrán que incluirse cuando se haga referencia a los Comentarios ampliados y la variable [biblioteca de cliente de comentarios extendidos](/help/communities/extend-create-components.md#create-a-client-library-folder) ( `apps.custom.comments`).

![comments-component1](assets/comments-component1.png)

### Agregar comentarios personalizados a una página {#add-custom-comments-to-a-page}

Como solo puede haber un sistema de comentarios por página, es más sencillo crear una página de muestra como se describe en la breve [Crear una página de muestra](/help/communities/create-sample-page.md) tutorial.

Una vez creado, introduzca el modo Diseño y ponga a disposición el grupo de componentes Personalizado para permitir que el `Alt Comments` componente que se agregará a la página.

Para que el comentario aparezca y funcione correctamente, las bibliotecas de cliente para Comentarios deben agregarse a la lista clientlibslist de la página (consulte [Clientlibs para componentes de Communities](/help/communities/clientlibs.md)).

#### Comentarios de Clientlibs en la página de muestra {#comments-clientlibs-on-sample-page}

![comments-clientlibs-crxde](assets/comments-clientlibs-crxde.png)

#### Autor: Comentario alternativo en la página de muestra {#author-alt-comment-on-sample-page}

![alt-comment](assets/alt-comment.png)

#### Autor: Nodo de comentarios de página de muestra {#author-sample-page-comments-node}

Puede verificar el resourceType en CRXDE viendo las propiedades del nodo de comentarios de la página de muestra en `/content/sites/sample/en/jcr:content/content/primary/comments`.

![verify-comment-crxde](assets/verify-comment-crxde.png)

#### Publicar página de muestra {#publish-sample-page}

Una vez agregado el componente personalizado a la página, también es necesario (re) [publicar la página](/help/communities/sites-console.md#publishing-the-site).

#### Publicar: Comentario alternativo en la página de muestra {#publish-alt-comment-on-sample-page}

Después de publicar la aplicación personalizada y la página de muestra, es posible introducir un comentario. Cuando haya iniciado sesión, ya sea con un [usuario de demostración](/help/communities/tutorials.md#demo-users) o administrador, es posible publicar un comentario.

Aquí está aaron.mcdonald@mailinator.com publicando un comentario:

![publish-alt-comment](assets/publish-alt-comment.png)

![publish-alt-comment1](assets/publish-alt-comment1.png)

Ahora que parece que el componente extendido funciona correctamente con el aspecto predeterminado, es hora de modificar el aspecto.
