---
title: Moderación en contexto
seo-title: Moderación en contexto
description: Cómo realizar acciones de moderador
seo-description: Cómo realizar acciones de moderador
uuid: 282a8bea-2822-4e5c-b9f4-4d9a5380d895
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ee104f6f-123b-4a6e-9031-849fc1318cc5
translation-type: tm+mt
source-git-commit: 917fceffb58883df83e96f60da4769046a18f3c0
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 1%

---


# Moderación en contexto {#in-context-moderation}

Para AEM Communities, la moderación puede ser realizada por administradores y miembros de la comunidad de confianza directamente en la página publicada donde se publicó el contenido de la comunidad.

Al utilizar una [consola de moderación](moderation.md), la información mostrada para el contenido incluye un vínculo a la página publicada para permitir el acceso a acciones de moderación adicionales disponibles al moderar en contexto.

## Acciones de moderación {#moderation-actions}

Visite la información general de moderación para obtener una descripción de [acciones de moderación](moderate-ugc.md#moderation-actions).

## Interfaz de usuario de moderación {#moderation-ui}

La interfaz de usuario presentada al moderador en la instancia de publicación está incluida en el cuadro de diálogo para publicar y administrar el contenido generado por el usuario (UGC). Los elementos de la interfaz de usuario están determinados por el estado del visitante del sitio, independientemente de si lo están...

1. El miembro que publicó el contenido.
1. Un moderador de miembros de confianza.
1. Un administrador.
1. Ha iniciado sesión, pero no es administrador, moderador ni autor del contenido.
1. No ha iniciado sesión.

## Ejemplo {#example}

Mediante el uso del [sitio de participación de Geometrixx](http://localhost:4503/content/sites/engage/en.html) creado al [Introducción a AEM Communities](getting-started.md), es posible configurar rápidamente un subproceso en un foro en el que experimentar varias actividades de moderación en el entorno de publicación, como se muestra a continuación.

Aaron McDonald (aaron.mcdonald@mailinator.com) fue identificado como un miembro de la comunidad de confianza al agregarlo al grupo de moderadores de participación de la comunidad al crear el sitio.

Rebekah Larsen (rebekah.larsen@trashymail.com) se puede agregar como miembro del grupo community-engagement-members mediante la [consola de miembros](members.md).

Para obtener más información sobre los grupos de usuarios de la comunidad, visite [Administración de usuarios y grupos de usuarios](users.md).

### Crear publicaciones de foro {#create-the-forum-posts}

* Inicie sesión como Rebekah Larsen (rebekah.larsen@trashymail.com)

   * Seleccionar foro
   * Seleccionar nuevo anuncio
   * Introduzca el asunto

      Cuándo cambiar el néctar en el alimentador de aves que rebota

   * Introduzca el texto principal

      No he tenido mucho éxito cuando cuelgo un alimentador de colibríes cada año. Parece que vienen uno o dos días y eso es todo. ¿Lo cambio una vez a la semana es demasiado largo? ¿Necesito cambiarlo antes?

   * Seleccionar anuncio
   * Seleccionar Cerrar sesión

* Inicie sesión como Aaron McDonald (aaron.mcdonald@mailinator.com)

   * Seleccionar foro
   * Para el tema Hummingbird, selecciona Leer más
   * Escriba el comentario para la respuesta de anuncio

      Cambio el mío una vez a la semana y los obtengo de mayo a octubre.

   * Seleccionar respuesta
   * Seleccionar Cerrar sesión

* Inicie sesión como Andrew Schaeffer (andrew.schaeffer@trashymail.com)

   * Seleccionar foro
   * Para el tema Hummingbird, selecciona Leer más
   * Escriba el comentario para la respuesta de anuncio

      Vendo néctar y alimentadores: visite https://my.viral.url/

   * Seleccionar respuesta
   * Seleccionar Cerrar sesión

### Visitante del sitio anónimo (#5) {#anonymous-site-visitor}

A continuación se muestra una vista del foro vista por un visitante del sitio que no ha iniciado sesión (5).

Un visitante anónimo del sitio solo puede realizar vistas en el foro, pero no puede publicar contenido ni realizar acciones de moderación.

![community-forum-visitante](assets/community-forum-visitor.png)

### Nuevo miembro (#4) {#new-member}

En el momento de la creación, inicie sesión como administrador y agregue Boyd Larsen (boyd.larsen@dodgit.com) como nuevo miembro del grupo de miembros de la comunidad que participan mediante la [consola de miembros](members.md) y, a continuación, cierre la sesión.

Al publicar, inicie sesión como Boyd Larsen y acceda al subproceso seleccionando `Forum` y luego `Read more` para el anuncio de colibrí.

Aviso:

* Boyd no ha participado en el foro.
* Boyd no puede eliminar nada.
* Boyd ha iniciado sesión y puede responder o marcar el contenido.

Haga que Boyd seleccione Marcar para marcar el contenido publicado por Andrew.

Cerrar sesión

![community-forum-miembro](assets/community-forum-member.png)

### Administrador (#3) {#administrator}

Inicie sesión como administrador (administrador) y acceda al subproceso seleccionando Foro y, a continuación, Leer más para un anuncio.

Aviso:

* El administrador puede marcar, eliminar, editar, denegar, cortar, cerrar, fijar, función.
* El administrador puede seleccionar Administración para acceder a la consola de moderación.

![community-admin-forum](assets/community-admin-forum.png)

Seleccione el elemento de menú Administración para acceder a la [consola de moderación](moderation.md) desde el entorno de publicación.

Observe que, para un administrador, todo el contenido moderable es visible, no solo el contenido del sitio de la comunidad de Geometrixx Engage.

El filtro de búsqueda es un panel lateral que activa o cierra.

Cerrar sesión.

![moderation-console-publish](assets/moderation-console-publish.png)

### Moderador de la comunidad (#2) {#community-moderator}

Inicie sesión como Aaron McDonald (aaron.mcdonal@mailinator.com), un moderador de la comunidad, y acceda al hilo seleccionando Foro y, a continuación, lea más para la publicación de comingbird.

Aviso:

* Aaron puede responder, eliminar, editar o denegar su propia publicación.
* Aaron también puede marcar/permitir, responder, eliminar, editar y denegar otro contenido.
* Aaron puede cortar el tema del foro para trasladarlo a otro foro del que él modera.
* Aaron puede seleccionar Administración para acceder a la consola de moderación.

![community-forum-moderator](assets/community-forum-moderator.png)

Seleccione el elemento de menú Administración para acceder a la [consola de moderación](moderation.md) desde el entorno de publicación.

Tenga en cuenta que, para un moderador de la comunidad, solo está visible el contenido moderable del sitio de la comunidad de Geometrixx Engage.

Observe que el moderador de la comunidad tiene las mismas opciones que el administrador (la imagen está con la barra lateral de búsqueda activada y cerrada), pero no tiene acceso a otras consolas de AEM.

Cerrar sesión.

![acceso de moderador](assets/moderator-access.png)

### Autor de contenido (#1) {#content-author}

Inicie sesión como Rebekah Larsen (rebekah.larsen@mailinator.com), un miembro de la comunidad que inició el subproceso, y acceda al subproceso seleccionando Foro y, a continuación, lea más para el anuncio de comingbird.

Aviso:

* Rebekah puede eliminar o editar su propio post.
* Rebekah también puede responder o marcar otro contenido.
* Rebekah no puede acceder a la consola de moderación.

![community-forum-author](assets/community-forum-author.png)

