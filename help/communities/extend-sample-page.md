---
title: Añadir comentario a página de muestra
seo-title: Añadir comentario a página de muestra
description: Añadir comentarios personalizados a una página
seo-description: Añadir comentarios personalizados a una página
uuid: ab258960-6de2-4943-80a7-e72904c0fd8e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a5040371-3bc2-43bc-a103-7175c4c6252d
docset: aem65
translation-type: tm+mt
source-git-commit: 230c700d87d82d248b7d0bbc45c69c5c2b0e3ff8
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# Añadir comentario en página de muestra {#add-comment-to-sample-page}

Ahora que los componentes del sistema de comentarios personalizados están en su lugar en el directorio de la aplicación (/apps), es posible utilizar el componente extendido. La instancia del sistema de comentarios de un sitio web que se verá afectado debe establecer resourceType como el sistema de comentarios personalizado e incluir todas las bibliotecas de cliente necesarias.

## Identifique los clientes {#identify-required-clientlibs} requeridos

Las bibliotecas de cliente necesarias para el estilo y funcionamiento de los comentarios predeterminados también son necesarias para los comentarios extendidos.

La [Guía de componentes de comunidad](/help/communities/components-guide.md) identifica las bibliotecas de cliente requeridas. Vaya a la Guía del componente y vista del componente Comentarios, por ejemplo:

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

Tenga en cuenta las tres bibliotecas de cliente necesarias para que Comentarios se procese y funcione correctamente. Será necesario incluirlos donde se haga referencia a los Comentarios extendidos y la biblioteca de cliente [Comentarios extendidos&#39;](/help/communities/extend-create-components.md#create-a-client-library-folder) ( `apps.custom.comments`).

![chlimage_1-47](assets/chlimage_1-47.png)

### Añadir comentarios personalizados a una página {#add-custom-comments-to-a-page}

Como sólo puede haber un sistema de comentarios por página, es más sencillo crear una página de muestra como se describe en el breve tutorial [Crear una página de muestra](/help/communities/create-sample-page.md).

Una vez creado, ingrese al modo Diseño y ponga a disposición el grupo de componentes Personalizado para permitir que el componente `Alt Comments` se agregue a la página.

Para que el comentario aparezca y funcione correctamente, las bibliotecas de cliente para Comentarios deben agregarse a la lista clientlibsde la página (consulte [Clientlibs para componentes de comunidades](/help/communities/clientlibs.md)).

#### Comentarios de Clientlibs en la página de muestra {#comments-clientlibs-on-sample-page}

![chlimage_1-48](assets/chlimage_1-48.png)

#### Autor: Comentario alternativo en la página de muestra {#author-alt-comment-on-sample-page}

![chlimage_1-49](assets/chlimage_1-49.png)

#### Autor: Nodo de comentarios de página de muestra {#author-sample-page-comments-node}

Puede comprobar resourceType en CRXDE viendo las propiedades del nodo de comentarios de la página de muestra en `/content/sites/sample/en/jcr:content/content/primary/comments`.

![chlimage_1-50](assets/chlimage_1-50.png)

#### Publicar página de muestra {#publish-sample-page}

Una vez agregado el componente personalizado a la página, también es necesario (re) [publicar la página](/help/communities/sites-console.md#publishing-the-site).

#### Publicar: Comentario alternativo en la página de muestra {#publish-alt-comment-on-sample-page}

Después de publicar la aplicación personalizada y la página de muestra, es posible introducir un comentario. Cuando se inicia sesión, ya sea con un [usuario de demostración](/help/communities/tutorials.md#demo-users) o administrador, es posible publicar un comentario.

Aquí está aaron.mcdonald@mailinator.com un comentario:

![chlimage_1-51](assets/chlimage_1-51.png)

![chlimage_1-52](assets/chlimage_1-52.png)

Ahora que parece que el componente extendido funciona correctamente con la apariencia predeterminada, es hora de modificar la apariencia.