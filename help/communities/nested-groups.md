---
title: Creación de grupos anidados
seo-title: Authoring Nested Groups
description: Crear grupos anidados
seo-description: Create nested groups
uuid: b377dc1b-bbb6-41c9-b0fc-8281e1410685
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 752235d2-21ac-46d2-82ed-5fec09c645e9
docset: aem65
exl-id: 55803b7a-9064-4392-9cc2-9f113fa8dc29
source-git-commit: 1074843a0105df39382b64defe66fc262986b9c9
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 5%

---

# Creación de grupos anidados{#authoring-nested-groups}

## Creación de grupos en el autor {#creating-groups-on-author}

En la instancia de AEM Author, desde la navegación global:

* Select **[!UICONTROL Comunidades]** > **[!UICONTROL Sitios]**.
* Select **[!UICONTROL carpeta de participación]** para abrirlo.
* Seleccione la tarjeta para el **[!UICONTROL Tutorial de introducción]** Sitio en inglés.

   * Seleccione la imagen de la tarjeta.
   * Do *not* seleccione un icono.

El resultado es alcanzar la variable [Consola Grupos](/help/communities/groups.md):

![create-group](assets/create-group.png)

La función de grupos se muestra como una carpeta en la que se crean instancias de grupos. Seleccione la carpeta Grupos para abrirla. El grupo creado al publicar está visible.

![create-new-group](assets/create-new-group.png)

## Crear grupo de artes principales {#create-main-arts-group}

Este grupo se puede crear porque la estructura del sitio para la participación incluye una función de grupo. La configuración de la función en el `Reference Template` de forma predeterminada, permite seleccionar cualquier plantilla de grupo habilitada. Por lo tanto, la plantilla elegida para este nuevo grupo es la `Reference Group`.

Estas consolas son similares a la consola Sitios de Communities .

* Select **[!UICONTROL Crear grupo]**

* **Plantilla del grupo de la comunidad**:

   * **[!UICONTROL Título de grupo de la comunidad]**: Artes
   * **[!UICONTROL Descripción del grupo de la comunidad]**: Un grupo principal para varios grupos artísticos
   * **[!UICONTROL Raíz del grupo de la comunidad]**: *dejar como predeterminado*
   * **[!UICONTROL Idiomas de grupo de la comunidad disponibles adicionales]**: utilice el menú desplegable para seleccionar los idiomas de grupo de comunidad disponibles. El menú muestra todos los idiomas en los que se crea el sitio de la comunidad principal. Los usuarios pueden seleccionar entre estos idiomas para crear grupos en varias configuraciones regionales en este solo paso. El mismo grupo se crea en varios idiomas especificados en la consola Grupos de los respectivos sitios de la comunidad.
   * **[!UICONTROL Nombre del grupo de la comunidad]**: arts
   * **[!UICONTROL Plantilla]**: lista desplegable para seleccionar `Reference Group`
   * Seleccione **[!UICONTROL Siguiente]**

![Grupos de comunidades anidadas](assets/parent-to-nestedgroup.png)

Continúe por los demás paneles con esta configuración:

* **[!UICONTROL Design]**

   * Cambie el diseño o permita el diseño predeterminado del sitio principal.
   * Seleccione **[!UICONTROL Siguiente]**.

* **[!UICONTROL Configuración]**

   * **[!UICONTROL Moderación]**

      * Deje vacío (heredar del sitio principal).
   * **[!UICONTROL Suscripción]**

      * Utilizar predeterminado `Optional Membership.`

      * **[!UICONTROL Miniatura]**
         * `optional.*`
      * **[!UICONTROL Seleccione Siguiente]**.



* Seleccione **[!UICONTROL Crear]**.

### Grupos de anidación dentro del Grupo de Artes {#nesting-groups-within-arts-group}

La variable `groups` La carpeta ahora contiene dos grupos (actualice la página).

![Anidado de grupos](assets/create-community-group.png)

#### Publicar grupo  {#publish-group}

Antes de crear grupos anidados dentro de la variable `arts` , pase el ratón sobre el `arts` y seleccione el icono de publicación para publicarlo.

![publish-site](assets/publish-site.png)

Espere a que se confirme que se publicó el grupo.

![publicado en grupo](assets/group-published.png)

La variable `arts` El grupo también debe contener `groups` , pero una que esté vacía y en la que se puedan crear nuevos grupos. Vaya a la carpeta de grupos de artes y cree 3 grupos anidados, cada uno con una configuración de pertenencia diferente:

1. **[!UICONTROL Visual]**

   * Título: `Visual Arts`
   * Nombre: `visual`
   * Plantilla: `Reference Group`
   * Membresía: select `Optional Membership`, un grupo público, abierto a todos los miembros.

1. **[!UICONTROL Auditorio]**

   * Título: `Auditory Arts`
   * Nombre: `auditory`
   * Plantilla: `Reference Group`
   * Membresía: select `Required Membership`, un grupo abierto, disponible para que los miembros se unan.

1. **[!UICONTROL Historia]**

   * Título: `Art History`
   * Nombre: `history`
   * Plantilla: `Reference Group`
   * Membresía: select `Restricted Membership`, un grupo secreto, visible únicamente para los miembros invitados. A modo de ejemplo, invite [usuario de demostración](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

Actualice la página para ver los tres grupos anidados (subcomunidades).

Para desplazarse a los grupos anidados desde la consola Sitios de Communities:

* Select **[!UICONTROL carpeta de participación]**
* Select **[!UICONTROL Tarjeta de tutorial de introducción]**
* Select **[!UICONTROL Grupos]** carpeta
* Select **[!UICONTROL tarjeta de arte]**
* Select **[!UICONTROL Grupos]** carpeta

![create-new-group2](assets/create-new-group2.png)

## Grupos de publicaciones {#publishing-groups}

![publish-site](assets/publish-site.png)

Después de publicar el sitio de la comunidad principal:

* Publicar cada grupo individualmente:

   * Esperando confirmación de que el grupo fue publicado.

* Publicar grupo principal antes de publicar cualquier grupo anidado en:

   * Todos los grupos deben publicarse de forma descendente.

![publicado en grupo](assets/group-published.png)

## Experiencia en la publicación {#experience-on-publish}

Es posible experimentar los diferentes grupos cuando se inicia sesión, por ejemplo, con la variable [usuarios de demostración](/help/communities/tutorials.md#demo-users) utilizado para:

* Miembro del grupo Arte/Historia: emily.andrews@mailinator.com/password
   * El grupo restringido (secreto), arte/historia, es visible:
   * Se pueden ver grupos opcionales (públicos).
   * Pueden unirse a grupos restringidos (abiertos).

* Administrador de grupos: aaron.mcdonald@mailinator.com/password

   * Se pueden ver grupos opcionales (públicos).
   * Pueden unirse a grupos restringidos (abiertos).
   * No se pueden ver grupos restringidos (secretos).

Acceso a las comunidades [Consolas Miembros y Grupos](/help/communities/members.md) un autor para agregar otros usuarios a varios grupos de miembros que se correspondan con los grupos de la comunidad.
