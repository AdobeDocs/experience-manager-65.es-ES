---
title: Agregar comentario a la página de muestra
seo-title: Agregar comentario a la página de muestra
description: Agregar comentarios personalizados a una página
seo-description: Agregar comentarios personalizados a una página
uuid: ab258960-6de2-4943-80a7-e72904c0fd8e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a5040371-3bc2-43bc-a103-7175c4c6252d
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Agregar comentario a la página de muestra {#add-comment-to-sample-page}

Ahora que los componentes del sistema de comentarios personalizados están en su lugar en el directorio de la aplicación (/apps), es posible utilizar el componente extendido. La instancia del sistema de comentarios de un sitio web que se verá afectado debe establecer resourceType como el sistema de comentarios personalizado e incluir todas las bibliotecas de cliente necesarias.

## Identifique los clientes requeridos {#identify-required-clientlibs}

Las bibliotecas de cliente necesarias para el estilo y funcionamiento de los comentarios predeterminados también son necesarias para los comentarios extendidos.

La Guía [de componentes de comunidad](/help/communities/components-guide.md) identifica las bibliotecas de cliente necesarias. Vaya a la Guía del componente y vea el componente Comentarios, por ejemplo:

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

Tenga en cuenta las tres bibliotecas de cliente necesarias para que Comentarios se procese y funcione correctamente. Será necesario incluirlos donde se haga referencia a los comentarios extendidos y en la biblioteca [cliente de Comentarios](/help/communities/extend-create-components.md#create-a-client-library-folder) extendidos ( `apps.custom.comments`).

![chlimage_1-79](assets/chlimage_1-79.png)

### Agregar comentarios personalizados a una página {#add-custom-comments-to-a-page}

Como sólo puede haber un sistema de comentarios por página, es más sencillo crear una página de muestra como se describe en el breve tutorial [Crear una página](/help/communities/create-sample-page.md) de muestra.

Una vez creado, introduzca el modo Diseño y ponga a disposición el grupo de componentes Personalizado para permitir que el `Alt Comments` componente se añada a la página.

Para que el comentario aparezca y funcione correctamente, las bibliotecas de cliente para Comentarios deben agregarse a la lista de clientes de la página (consulte Componentes [de](/help/communities/clientlibs.md)clientes para comunidades).

#### Comentarios de clientes en la página de muestra {#comments-clientlibs-on-sample-page}

![Comentarios de clientes en la página de muestra](assets/chlimage_1-80.png)

#### Autor: Comentario alternativo en la página de muestra {#author-alt-comment-on-sample-page}

![Comentario alternativo en la página de muestra](assets/chlimage_1-81.png)

#### Autor: Nodo de comentarios de página de muestra {#author-sample-page-comments-node}

Puede comprobar resourceType en CRXDE consultando las propiedades del nodo de comentarios de la página de muestra en `/content/sites/sample/en/jcr:content/content/primary/comments`.

![chlimage_1-82](assets/chlimage_1-82.png)

#### Publicar página de muestra {#publish-sample-page}

Una vez agregado el componente personalizado a la página, también es necesario (volver a) [publicar la página](/help/communities/sites-console.md#publishing-the-site).

#### Publicar: Comentario alternativo en la página de muestra {#publish-alt-comment-on-sample-page}

Después de publicar la aplicación personalizada y la página de muestra, es posible introducir un comentario. Cuando se inicia sesión, ya sea con un usuario [de](/help/communities/tutorials.md#demo-users) demostración o con un administrador, es posible publicar un comentario.

Aquí está aaron.mcdonald@mailinator.com un comentario:

![chlimage_1-83](assets/chlimage_1-83.png) ![chlimage_1-84](assets/chlimage_1-84.png)

Ahora que parece que el componente extendido funciona correctamente con la apariencia predeterminada, es hora de modificar la apariencia.