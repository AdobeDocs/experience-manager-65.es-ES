---
title: Creación de grupos anidados
description: Obtenga información sobre cómo crear grupos anidados para un sitio de comunidades de Adobe Experience Manager.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 55803b7a-9064-4392-9cc2-9f113fa8dc29
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 1%

---

# Creación de grupos anidados{#authoring-nested-groups}

## Creación de grupos en Autor {#creating-groups-on-author}

AEM En la instancia de autor de, en la navegación global:

* Seleccione **[!UICONTROL Comunidades]** > **[!UICONTROL Sitios]**.
* Seleccione **[!UICONTROL activar carpeta]** para abrirla.
* Seleccione la tarjeta del sitio en inglés **[!UICONTROL Tutorial de introducción]**.

   * Seleccione la imagen de la tarjeta.
   * *no* selecciona un icono.

El resultado es llegar a la [consola de grupos](/help/communities/groups.md):

![crear-grupo](assets/create-group.png)

La función de grupos se muestra como una carpeta en la que se crean instancias de grupos. Para abrirla, seleccione la carpeta Groups. El grupo creado en Publish es visible.

![crear-nuevo-grupo](assets/create-new-group.png)

## Crear grupo de artes principales {#create-main-arts-group}

Este grupo se puede crear porque la estructura del sitio para participar incluye la función de un grupo. La configuración de la función en `Reference Template` del sitio toma como valor predeterminado permitir la selección de cualquier plantilla de grupo habilitada. Por lo tanto, la plantilla elegida para este nuevo grupo es `Reference Group`.

Estas consolas son similares a la consola Sitios de Communities.

* Seleccionar **[!UICONTROL Crear grupo]**

* **Plantilla de grupo de comunidad**:

   * **[!UICONTROL Título del grupo de la comunidad]**: artes
   * **[!UICONTROL Descripción del grupo de la comunidad]**: un grupo principal para varios grupos de artes
   * **[!UICONTROL Raíz de grupo de comunidad]**: *dejar como predeterminado*
   * **[!UICONTROL Idiomas de grupo de comunidad adicionales disponibles]**: use el menú desplegable para seleccionar los idiomas de grupo de comunidad disponibles. El menú muestra todos los idiomas en los que se crea el sitio de la comunidad principal. Los usuarios pueden seleccionar entre estos idiomas para crear grupos en varias configuraciones regionales en este solo paso. El mismo grupo se crea en varios idiomas especificados en la consola Grupos de los sitios de la comunidad correspondientes.
   * **[!UICONTROL Nombre de grupo de comunidad]**: arts
   * **[!UICONTROL Plantilla]**: lista desplegable para seleccionar `Reference Group`
   * Seleccionar **[!UICONTROL Siguiente]**

![Grupos de la comunidad anidados](assets/parent-to-nestedgroup.png)

Continúe con los otros paneles con esta configuración:

* **[!UICONTROL Design]**

   * Cambie el diseño o permita el diseño predeterminado del sitio principal.
   * Seleccione **[!UICONTROL Siguiente]**.

* **[!UICONTROL Configuración]**

   * **[!UICONTROL Moderación]**

      * Dejar vacío (heredar del sitio principal).

   * **[!UICONTROL Pertenencia]**

      * Usar predeterminado `Optional Membership.`

      * **[!UICONTROL Miniatura]**
         * `optional.*`

      * **[!UICONTROL Seleccionar Siguiente]**.

* Seleccione **[!UICONTROL Crear]**.

### Anidado de grupos dentro del grupo de artes {#nesting-groups-within-arts-group}

La carpeta `groups` ahora contiene dos grupos (actualice la página).

![Anidando los grupos](assets/create-community-group.png)

#### Grupo de Publish {#publish-group}

Antes de crear grupos anidados en el grupo `arts`, pase el ratón sobre la tarjeta `arts` y seleccione el icono Publicar para publicarlo.

![sitio de publicación](assets/publish-site.png)

Espere a que se confirme la publicación del grupo.

![publicado en grupo](assets/group-published.png)

El grupo `arts` también debe contener una carpeta `groups`, pero debe contener una carpeta vacía en la que se puedan crear nuevos grupos. Vaya a la carpeta de grupos de artes y cree tres grupos anidados, cada uno con una configuración de pertenencia diferente:

1. **[!UICONTROL Visual]**

   * Título: `Visual Arts`
   * Nombre: `visual`
   * Plantilla: `Reference Group`
   * Pertenencia: seleccione `Optional Membership`, un grupo público, abierto a todos los miembros.

1. **[!UICONTROL Auditorio]**

   * Título: `Auditory Arts`
   * Nombre: `auditory`
   * Plantilla: `Reference Group`
   * Pertenencia: seleccione `Required Membership`, un grupo abierto, disponible para que los miembros se unan.

1. **[!UICONTROL Historial]**

   * Título: `Art History`
   * Nombre: `history`
   * Plantilla: `Reference Group`
   * Pertenencia: seleccione `Restricted Membership`, un grupo secreto, visible solo para los miembros invitados. Por ejemplo, invite a [usuario de demostración](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

Actualice la página para poder ver los tres grupos anidados (subcomunidades).

Para desplazarse a los grupos anidados desde la consola Sitios de Communities:

* Seleccione la **[!UICONTROL carpeta de participación]**
* Seleccione **[!UICONTROL Tarjeta de tutorial de introducción]**
* Seleccione la carpeta **[!UICONTROL Grupos]**
* Seleccionar **[!UICONTROL tarjeta de arte]**
* Seleccione la carpeta **[!UICONTROL Grupos]**

![create-new-group2](assets/create-new-group2.png)

## Grupos de publicación {#publishing-groups}

![sitio de publicación](assets/publish-site.png)

Después de publicar el sitio principal de la comunidad:

* Publish cada grupo individualmente:

   * Esperando confirmación de publicación del grupo.

* Publish el grupo principal antes de publicar cualquier grupo anidado en:

   * Todos los grupos deben publicarse de arriba hacia abajo.

![publicado en grupo](assets/group-published.png)

## Experiencia en Publish {#experience-on-publish}

Es posible experimentar los diferentes grupos al iniciar sesión, por ejemplo, con los [usuarios de demostración](/help/communities/tutorials.md#demo-users) utilizados para:

* Miembro del grupo Arte/Historia: `emily.andrews@mailinator.com/password`
   * El grupo restringido (secreto), artes/historia, es visible:
   * Puede ver grupos opcionales (públicos).
   * Posibilidad de unirse a grupos restringidos (abiertos).

* Administrador del grupo: `aaron.mcdonald@mailinator.com/password`

   * Puede ver grupos opcionales (públicos).
   * Posibilidad de unirse a grupos restringidos (abiertos).
   * No se pueden ver los grupos restringidos (secretos).

Acceda a las consolas de comunidades [Miembros y grupos](/help/communities/members.md) en Autor para agregar otros usuarios a varios grupos de miembros que se correspondan con los grupos de la comunidad.
