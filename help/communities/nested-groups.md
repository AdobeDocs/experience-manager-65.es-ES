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
source-git-commit: 5d196d1f6d5f94f2d3ef0d4461cfe38562f8ba8c
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 5%

---


# Creación de grupos anidados{#authoring-nested-groups}

## Creación de grupos en el autor {#creating-groups-on-author}

En la instancia de AEM Author, desde la navegación global:

* Seleccione **[!UICONTROL Comunidades]** > **[!UICONTROL Sitios]**.
* Seleccione **[!UICONTROL carpeta de participación]** para abrirla.
* Seleccione la tarjeta para el **[!UICONTROL Tutorial de introducción]** sitio en inglés.

   * Seleccione la imagen de la tarjeta.
   * *no* seleccione un icono.

El resultado es llegar a la [consola de grupos](/help/communities/groups.md):

![create-group](assets/create-group.png)

La función de grupos se mostrará como una carpeta en la que se crearán las instancias de grupos. Seleccione la carpeta Grupos para abrirla. El grupo creado al publicar está visible.

![create-new-group](assets/create-new-group.png)

## Crear grupo de artes principales {#create-main-arts-group}

Este grupo se puede crear porque la estructura del sitio para la participación incluye una función de grupo. La configuración de la función en el `Reference Template` del sitio permite de forma predeterminada la selección de cualquier plantilla de grupo habilitada. Por lo tanto, la plantilla elegida para este nuevo grupo es `Reference Group`.

Estas consolas son similares a la consola Sitios de comunidades.

* Seleccione **[!UICONTROL Crear grupo]**.

* **Plantilla del grupo de la comunidad**:

   * **[!UICONTROL Título]** del grupo de la comunidad: Artes.
   * **[!UICONTROL Descripción]** del grupo de la comunidad: Un grupo de padres para varios grupos de artes.
   * **[!UICONTROL Raíz]** del grupo de la comunidad:  *dejar como predeterminado*.
   * **[!UICONTROL Idioma(s)]** adicional(s) disponible(s) del grupo de la comunidad: utilice el menú desplegable para seleccionar los idiomas de grupo de comunidad disponibles. El menú muestra todos los idiomas en los que se crea el sitio de comunidad principal. Los usuarios pueden seleccionar entre estos idiomas para crear grupos en varias configuraciones regionales en este solo paso. El mismo grupo se crea en varios idiomas especificados en la consola Grupos de los respectivos sitios de la comunidad.
   * **[!UICONTROL Nombre]** del grupo de la comunidad: Artículos 10
   * **[!UICONTROL Plantilla]**: desplegable para seleccionar  `Reference Group.`
   * Seleccione **[!UICONTROL Siguiente]**.

![Grupos de comunidades anidadas](assets/parent-to-nestedgroup.png)

Continúe por los demás paneles con esta configuración:

* **[!UICONTROL Diseño]**

   * Cambie el diseño o permita el diseño predeterminado del sitio principal.
   * Seleccione **[!UICONTROL Siguiente]**.

* **[!UICONTROL Configuración]**

   * **[!UICONTROL Moderación]**

      * Deje vacío (herede del sitio principal).
   * **[!UICONTROL Suscripción]**

      * Usar `Optional Membership.` predeterminado

      * **[!UICONTROL Miniatura]**
         * `optional.*`
      * **[!UICONTROL Seleccione Siguiente]**.



* Seleccione **[!UICONTROL Crear]**.

### Anidado de grupos dentro del grupo de artes {#nesting-groups-within-arts-group}

La carpeta `groups` ahora contiene dos grupos (actualizar la página).

![Anidación de grupos](assets/create-community-group.png)

#### Publicar grupo {#publish-group}

Antes de crear grupos anidados dentro del grupo `arts`, pase el ratón por encima de la tarjeta `arts` y seleccione el icono de publicación para publicarla.

![publish-site](assets/publish-site.png)

Espere a que se confirme que se publicó el grupo.

![grupo publicado](assets/group-published.png)

El grupo `arts` también debe contener una carpeta `groups`, pero una carpeta vacía y en la que se pueden crear nuevos grupos. Vaya a la carpeta del grupo de artes y cree 3 grupos anidados, cada uno con una configuración de pertenencia diferente:

1. **[!UICONTROL Visual]**

   * Título: `Visual Arts`
   * Nombre: `visual`
   * Plantilla: `Reference Group`
   * Membresía: seleccione `Optional Membership`, un grupo público, abierto a todos los miembros.

1. **[!UICONTROL Auditorio]**

   * Título: `Auditory Arts`
   * Nombre: `auditory`
   * Plantilla: `Reference Group`
   * Membresía: seleccione `Required Membership`, un grupo abierto, disponible para que los miembros se unan.

1. **[!UICONTROL Historia]**

   * Título: `Art History`
   * Nombre: `history`
   * Plantilla: `Reference Group`
   * Membresía: seleccione `Restricted Membership`, un grupo secreto, visible sólo para los miembros invitados. Como ejemplo, invite a [usuario de demostración](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

Actualice la página para ver los tres grupos anidados (subcomunidades).

Para desplazarse a los grupos anidados desde la consola Sitios de comunidades:

* Seleccione **[!UICONTROL carpeta de participación]**
* Seleccione **[!UICONTROL Tutorial de introducción]**
* Seleccionar carpeta **[!UICONTROL Grupos]**
* Seleccionar **[!UICONTROL tarjeta de artes]**
* Seleccionar carpeta **[!UICONTROL Grupos]**

![create-new-group2](assets/create-new-group2.png)

## Grupos de publicaciones {#publishing-groups}

![publish-site](assets/publish-site.png)

Después de publicar el sitio principal de la comunidad:

* Publicar cada grupo individualmente:

   * Esperando confirmación de que se publicó el grupo.

* Publicar grupo principal antes de publicar cualquier grupo anidado en:

   * Todos los grupos deben publicarse de manera vertical.

![grupo publicado](assets/group-published.png)

## Experiencia en publicación {#experience-on-publish}

Es posible experimentar los diferentes grupos al iniciar sesión, por ejemplo con los [usuarios de demostración](/help/communities/tutorials.md#demo-users) utilizados para:

* Miembro del grupo Arte/Historia: emily.andrews@mailinator.com/password
   * El grupo restringido (secreto), arte/historia, es visible:
   * Puede ver grupos opcionales (públicos).
   * Puede unirse a grupos restringidos (abiertos).

* Administrador de grupos: aaron.mcdonald@mailinator.com/password

   * Puede ver grupos opcionales (públicos).
   * Puede unirse a grupos restringidos (abiertos).
   * No se pueden ver los grupos restringidos (secretos).

Acceda a las consolas Comunidades [Miembros y Grupos](/help/communities/members.md) del autor para agregar otros usuarios a varios grupos de miembros que se correspondan con los grupos de la comunidad.

