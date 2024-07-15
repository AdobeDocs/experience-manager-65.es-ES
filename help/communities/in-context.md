---
title: Moderación en contexto
description: Descubra cómo los administradores y los miembros de confianza de la comunidad pueden realizar acciones de moderador en las comunidades de Adobe Experience Manager.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 47b3c19c-5228-4b72-b78c-7ed71b308921
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# Moderación en contexto {#in-context-moderation}

Para AEM Communities, la moderación pueden realizarla administradores y miembros de la comunidad de confianza directamente en la página publicada en la que se publicó el contenido de la comunidad.

Al usar [consola de moderación](moderation.md), la información mostrada para el contenido incluye un vínculo a la página publicada para permitir el acceso a acciones de moderación adicionales disponibles al moderar en contexto.

## Acciones de moderación {#moderation-actions}

Visite el resumen de moderación para obtener una descripción de [acciones de moderación](moderate-ugc.md#moderation-actions).

## IU de moderación {#moderation-ui}

La interfaz de usuario presentada al moderador en la instancia de publicación se encuentra en el cuadro de diálogo para publicar y administrar contenido generado por el usuario (UGC). Los elementos de la interfaz de usuario están determinados por el estado del visitante del sitio, ya sean...

1. El miembro que publicó el contenido.
1. Un moderador miembro de confianza.
1. Un administrador.
1. Ha iniciado sesión, pero no es administrador, moderador ni autor del contenido.
1. No se ha iniciado sesión.

## Ejemplos {#example}

Con el sitio [Geometrixx Engage](http://localhost:4503/content/sites/engage/en.html) creado al [Comenzar con AEM Communities](getting-started.md), es posible configurar un hilo en un foro en el que experimentar diversas actividades de moderación en el entorno de Publish. Consulte a continuación.

Aaron McDonald (`aaron.mcdonald@mailinator.com`) se identificó como un miembro de confianza de la comunidad agregándolo al grupo de moderadores de participación de la comunidad al crear el sitio.

Rebekah Larsen (`rebekah.larsen@trashymail.com`) se puede agregar como miembro del grupo de miembros de la comunidad mediante la [consola Miembros](members.md).

Para obtener más información sobre los grupos de usuarios de la comunidad, visite [Administración de usuarios y grupos de usuarios](users.md).

### Creación de entradas de foro {#create-the-forum-posts}

* Iniciar sesión como Rebekah Larsen (rebekah.larsen@trashymail.com)

   * Seleccionar foro
   * Seleccione Nuevo Post
   * Introduzca el asunto

     Cuándo cambiar el néctar en Humming Bird Feeder

   * Escriba el texto del cuerpo

     No he tenido mucho éxito cuando cuelgo un alimentador de colibrí cada año. Parece que vienen un día o dos, entonces eso es todo. Lo cambio una vez a la semana, ¿es demasiado largo? ¿Debo cambiarlo antes?

   * Seleccionar Post
   * Seleccione Cerrar sesión

* Iniciar sesión como Aaron McDonald (aaron.mcdonald@mailinator.com)

   * Seleccionar foro
   * Para el tema de Hummingbird, seleccione Leer más
   * Escriba el comentario para la respuesta de Post

     Me cambio la mía una vez a la semana y las recibo de mayo a octubre.

   * Seleccionar respuesta
   * Seleccione Cerrar sesión

* Inicie sesión como Andrew Schaeffer (andrew.schaeffer@trashymail.com)

   * Seleccionar foro
   * Para el tema de Hummingbird, seleccione Leer más
   * Escriba el comentario para la respuesta de Post

     Vendo néctar y alimentadores - visita https://my.viral.url/

   * Seleccionar respuesta
   * Seleccione Cerrar sesión

### Visitante anónimo del sitio (#5) {#anonymous-site-visitor}

A continuación se muestra una vista del foro vista por un visitante del sitio que no ha iniciado sesión (5).

Un visitante anónimo del sitio solo puede ver el foro, pero no puede publicar ningún contenido ni realizar ninguna acción de moderación.

![visitante-foro-comunidad](assets/community-forum-visitor.png)

### Nuevo miembro (#4) {#new-member}

En el autor, inicie sesión como administrador y agregue Boyd Larsen (boyd.larsen@dodgit.com) como nuevo miembro del grupo de miembros de la comunidad mediante la [consola de miembros](members.md). A continuación, cierre la sesión.

En la publicación, inicie sesión como Boyd Larsen y acceda al subproceso seleccionando `Forum` y, a continuación, `Read more` para la publicación de colibrí.

Aviso:

* Boyd no ha participado en el foro.
* Boyd no puede eliminar nada.
* El cuerpo ha iniciado sesión y puede responder o marcar contenido.

Haga que Boyd seleccione Marcar para marcar el contenido publicado por Andrew.

Cerrar sesión

![miembro-foro-comunidad](assets/community-forum-member.png)

### Administrador (#3) {#administrator}

Inicie sesión como administrador (administrador) y acceda al hilo seleccionando Foro y, a continuación, Más información para una publicación.

Aviso:

* El administrador puede marcar, eliminar, editar, denegar, cortar, cerrar, anclar y utilizar funciones.
* El administrador puede seleccionar Administración para acceder a la consola de moderación.

![community-admin-forum](assets/community-admin-forum.png)

Seleccione el elemento de menú Administración para poder acceder a la [consola de moderación](moderation.md) desde el entorno de Publish.

Tenga en cuenta que, para un administrador, todo el contenido moderable es visible, no solo el contenido del sitio de la comunidad de Geometrixx Engage.

El filtro de búsqueda es un panel lateral que alterna entre abierto y cerrado.

Cerrar sesión.

![moderation-console-publish](assets/moderation-console-publish.png)

### Moderador de la comunidad (#2) {#community-moderator}

Inicie sesión como Aaron McDonald (`aaron.mcdonal@mailinator.com`), un moderador de la comunidad, y acceda al hilo seleccionando Foro y, a continuación, Leer más para la publicación de colibrí.

Aviso:

* Aaron puede responder, eliminar, editar o denegar su propia publicación.
* Aaron también puede Marcar/Permitir, Responder, Eliminar, Editar, Denegar otro contenido.
* Aaron puede Cortar el tema del foro para moverlo a otro foro para el que modera.
* Aaron puede seleccionar Administración para acceder a la consola de moderación.

![moderador-foro-comunidad](assets/community-forum-moderator.png)

Seleccione el elemento de menú Administración para poder acceder a la [consola de moderación](moderation.md) desde el entorno de Publish.

Tenga en cuenta que, para un moderador de la comunidad, solo está visible el contenido moderable del sitio de la comunidad de Geometrixx Engage.

AEM Observe que el moderador de la comunidad tiene las mismas opciones que el administrador (la imagen tiene la barra lateral de búsqueda activada o cerrada), pero no tiene acceso a otras consolas de la.

Cerrar sesión.

![acceso de moderador](assets/moderator-access.png)

### Autor de contenido (#1) {#content-author}

Inicie sesión como Rebekah Larsen (`rebekah.larsen@mailinator.com`), un miembro de la comunidad que inició el hilo, y acceda al hilo seleccionando Foro y, a continuación, Más información para la publicación de colibrí.

Aviso:

* Rebekah puede eliminar o editar su propia publicación.
* Rebekah también puede responder o marcar otro contenido.
* Rebeca no puede acceder a la consola de moderación.

![community-forum-author](assets/community-forum-author.png)
