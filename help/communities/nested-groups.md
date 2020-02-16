---
title: Creación de grupos anidados
seo-title: Creación de grupos anidados
description: Crear grupos anidados
seo-description: Crear grupos anidados
uuid: b377dc1b-bbb6-41c9-b0fc-8281e1410685
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 752235d2-21ac-46d2-82ed-5fec09c645e9
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Creación de grupos anidados{#authoring-nested-groups}

## Creación de grupos en el autor {#creating-groups-on-author}

En la instancia de AEM Author, desde la navegación global:

* Seleccione** Comunidades, Sitios.**
* Seleccione **la carpeta** de participación para abrirla.
* Seleccione la tarjeta para el sitio **Tutorial** de introducción en inglés.

   * Seleccione la imagen de la tarjeta.
   * No *seleccione* ningún icono.

El resultado es llegar a la consola [](/help/communities/groups.md)Grupos:

![chlimage_1-91](assets/chlimage_1-91.png)

La función de grupos se mostrará como una carpeta en la que se crearán las instancias de grupos. Seleccione la carpeta Grupos para abrirla. El grupo creado al publicar está visible.

![chlimage_1-92](assets/chlimage_1-92.png)

## Crear grupo de artes principales {#create-main-arts-group}

Este grupo se puede crear porque la estructura del sitio para la participación incluye una función de grupo. La configuración de la función en el sitio `Reference Template` de forma predeterminada permite la selección de cualquier plantilla de grupo habilitada. Por lo tanto, la plantilla elegida para este nuevo grupo es la `Reference Group`.

Estas consolas son similares a la consola Sitios de comunidades.

* Seleccione **Crear grupo.**
* **Plantilla del grupo de la comunidad**:

   * Título del grupo de la comunidad: Artes.
   * Descripción del grupo de la comunidad: Un grupo de padres para varios grupos de artes.
   * Raíz del grupo de la comunidad: *dejar como predeterminado.*
   * Idioma(s) adicional(s) disponible(s) del grupo de la comunidad: utilice el menú desplegable para seleccionar los idiomas de grupo de comunidad disponibles. El menú muestra todos los idiomas en los que se crea el sitio de comunidad principal. Los usuarios pueden seleccionar entre estos idiomas para crear grupos en varias configuraciones regionales en este solo paso. El mismo grupo se crea en varios idiomas especificados en la consola Grupos de los respectivos sitios de la comunidad.
   * Nombre del grupo de la comunidad: Artículos 10
   * Plantilla: desplegable para seleccionar `Reference Group.`
   * `Select Next.`

![Grupos de comunidades anidadas](assets/parent-to-nestedgroup.png)

Continúe por los demás paneles con esta configuración:

* **Diseño**

   * Cambie el diseño o permita el diseño predeterminado del sitio principal.
   * Seleccione **Siguiente.**

* **Configuración**

   * **Moderación**

      * dejar vacío (heredar del sitio principal).
   * **Suscripción**

      * use default `Optional Membership.`
   * **Miniatura**

      * `*optional.*`
   * `Select Next.`




* Seleccione **Crear.**

### Grupos de anidación dentro del grupo de artes {#nesting-groups-within-arts-group}

La `groups` carpeta ahora contiene dos grupos (actualice la página).

![Anidación de grupos](assets/create-community-group.png)

#### Publicar grupo {#publish-group}

Antes de crear grupos anidados dentro del `arts``arts` grupo, coloque el puntero sobre la tarjeta y seleccione el icono de publicación para publicarla.

![chlimage_1-93](assets/chlimage_1-93.png)

Espere a que se confirme que se publicó el grupo.

![chlimage_1-94](assets/chlimage_1-94.png)

El `arts` grupo también debe contener una `groups` carpeta, pero una que esté vacía y en la que se puedan crear nuevos grupos. Vaya a la carpeta del grupo de artes y cree 3 grupos anidados, cada uno con una configuración de pertenencia diferente:

1. Visual

   * Título: `Visual Arts`
   * Nombre: `visual`
   * Plantilla: `Reference Group`
   * Membresía: seleccionar `Optional Membership`un grupo público, abierto a todos los miembros

1. Auditorio

   * Título: `Auditory Arts`
   * Nombre: `auditory`
   * Plantilla: `Reference Group`
   * Membresía: seleccionar `Required Membership`un grupo abierto, disponible para que los miembros se unan

1. Historia

   * Título: `Art History`
   * Nombre: `history`
   * Plantilla: `Reference Group`
   * Membresía: seleccione `Restricted Membership`un grupo secreto, visible sólo para los miembros invitados como ejemplo, invite a un usuario [de](/help/communities/tutorials.md#demo-users) demostración `emily.andrews@mailinator.com`

Actualice la página para ver los tres grupos anidados (subcomunidades).

Para desplazarse a los grupos anidados desde la consola Sitios de comunidades:

* seleccionar carpeta de participación
* seleccionar la tarjeta de tutoriales de introducción
* seleccionar la carpeta Grupos
* seleccionar tarjeta de artes
* seleccionar la carpeta Grupos

![chlimage_1-95](assets/chlimage_1-95.png)

## Grupos de publicaciones {#publishing-groups}

![chlimage_1-96](assets/chlimage_1-96.png)

Después de publicar el sitio principal de la comunidad:

* publicar cada grupo individualmente

   * esperando confirmación de que se publicó el grupo

* publicar grupo principal antes de publicar cualquier grupo anidado en

   * todos los grupos deben publicarse de manera descendente.

![chlimage_1-97](assets/chlimage_1-97.png)

## Experiencia en la publicación {#experience-on-publish}

Es posible experimentar los diferentes grupos al iniciar sesión, por ejemplo con los usuarios [de](/help/communities/tutorials.md#demo-users) demostración utilizados para

* Miembro del grupo Arte/Historia: emily.andrews@mailinator.com/password

   * el grupo restringido (secreto), arte/historia, es visible
   * puede ver grupos opcionales (públicos)
   * puede unirse a grupos restringidos (abiertos)

* Administrador de grupos: aaron.mcdonald@mailinator.com/password

   * puede ver grupos opcionales (públicos)
   * puede unirse a grupos restringidos (abiertos)
   * no se pueden ver los grupos restringidos (secretos)

Acceda a las consolas [Miembros y Grupos de comunidades](/help/communities/members.md) del autor para agregar otros usuarios a varios grupos de miembros que se correspondan con los grupos de la comunidad.

