---
title: Creación de grupos anidados
description: Obtenga información sobre cómo crear grupos anidados para un sitio de comunidades de Adobe Experience Manager.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 55803b7a-9064-4392-9cc2-9f113fa8dc29
source-git-commit: f03d0ab9d0f491441378e16e1590d33651f064b5
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 4%

---

# Creación de grupos anidados{#authoring-nested-groups}

## Creación de grupos en Autor {#creating-groups-on-author}

AEM En la instancia de autor de, en la navegación global:

* Seleccionar **[!UICONTROL Communities]** > **[!UICONTROL Sites]**.
* Seleccionar **[!UICONTROL carpeta de participación]** para abrirlo.
* Seleccione la tarjeta para la **[!UICONTROL Tutorial de introducción]** Sitio en inglés.

   * Seleccione la imagen de la tarjeta.
   * Hacer *no* seleccione un icono.

El resultado es alcanzar el [Consola de grupos](/help/communities/groups.md):

![create-group](assets/create-group.png)

La función de grupos se muestra como una carpeta en la que se crean instancias de grupos. Para abrirla, seleccione la carpeta Groups. El grupo creado en Publicar es visible.

![create-new-group](assets/create-new-group.png)

## Crear grupo de artes principales {#create-main-arts-group}

Este grupo se puede crear porque la estructura del sitio para participar incluye la función de un grupo. La configuración de la función en el `Reference Template` de forma predeterminada, permite seleccionar cualquier plantilla de grupo habilitada. Por lo tanto, la plantilla elegida para este nuevo grupo es `Reference Group`.

Estas consolas son similares a la consola Sitios de Communities.

* Seleccionar **[!UICONTROL Crear grupo]**

* **Plantilla del grupo de la comunidad**:

   * **[!UICONTROL Título del grupo de comunidad]**: artes
   * **[!UICONTROL Descripción del grupo de comunidad]**: un grupo principal para varios grupos artísticos
   * **[!UICONTROL Raíz de grupo de comunidad]**: *dejar como predeterminado*
   * **[!UICONTROL Idiomas de grupo de la comunidad adicionales disponibles]**: utilice el menú desplegable para seleccionar los idiomas de grupo de la comunidad disponibles. El menú muestra todos los idiomas en los que se crea el sitio de la comunidad principal. Los usuarios pueden seleccionar entre estos idiomas para crear grupos en varias configuraciones regionales en este solo paso. El mismo grupo se crea en varios idiomas especificados en la consola Grupos de los sitios de la comunidad correspondientes.
   * **[!UICONTROL Nombre del grupo de comunidad]**: artes
   * **[!UICONTROL Plantilla]**: menú desplegable para seleccionar `Reference Group`
   * Seleccione **[!UICONTROL Siguiente]**

![Grupos de comunidad anidados](assets/parent-to-nestedgroup.png)

Continúe con los otros paneles con esta configuración:

* **[!UICONTROL Design]**

   * Cambie el diseño o permita el diseño predeterminado del sitio principal.
   * Seleccione **[!UICONTROL Siguiente]**.

* **[!UICONTROL Configuración]**

   * **[!UICONTROL Moderación]**

      * Dejar vacío (heredar del sitio principal).

   * **[!UICONTROL Suscripción]**

      * Usar valor predeterminado `Optional Membership.`

      * **[!UICONTROL Miniatura]**
         * `optional.*`

      * **[!UICONTROL Seleccione Siguiente]**.

* Seleccione **[!UICONTROL Crear]**.

### Anidado de grupos dentro del grupo de artes {#nesting-groups-within-arts-group}

El `groups` La carpeta ahora contiene dos grupos (actualice la página).

![Anidado de grupos](assets/create-community-group.png)

#### Publicar grupo  {#publish-group}

Antes de crear grupos anidados en `arts` grupo, pase el ratón sobre `arts` y seleccione el icono publicar para publicarlo.

![publish-site](assets/publish-site.png)

Espere a que se confirme la publicación del grupo.

![publicado en grupo](assets/group-published.png)

El `arts` el grupo también debe contener un `groups` carpeta, pero una que esté vacía y en la que se puedan crear nuevos grupos. Vaya a la carpeta de grupos de artes y cree tres grupos anidados, cada uno con una configuración de pertenencia diferente:

1. **[!UICONTROL Visual]**

   * Título: `Visual Arts`
   * Nombre: `visual`
   * Plantilla: `Reference Group`
   * Suscripción: seleccione `Optional Membership`, un grupo público abierto a todos los miembros.

1. **[!UICONTROL Auditorio]**

   * Título: `Auditory Arts`
   * Nombre: `auditory`
   * Plantilla: `Reference Group`
   * Suscripción: seleccione `Required Membership`, un grupo abierto, disponible para que los miembros se unan.

1. **[!UICONTROL Historia]**

   * Título: `Art History`
   * Nombre: `history`
   * Plantilla: `Reference Group`
   * Suscripción: seleccione `Restricted Membership`, un grupo secreto, visible solo para los miembros invitados. Por ejemplo, invite a [usuario de demostración](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

Actualice la página para poder ver los tres grupos anidados (subcomunidades).

Para desplazarse a los grupos anidados desde la consola Sitios de Communities:

* Seleccione el **[!UICONTROL carpeta de participación]**
* Seleccionar **[!UICONTROL Tarjeta de tutorial de introducción]**
* Seleccione el **[!UICONTROL Grupos]** carpeta
* Seleccionar **[!UICONTROL tarjeta artística]**
* Seleccione el **[!UICONTROL Grupos]** carpeta

![create-new-group2](assets/create-new-group2.png)

## Grupos de publicación {#publishing-groups}

![publish-site](assets/publish-site.png)

Después de publicar el sitio principal de la comunidad:

* Publicar cada grupo individualmente:

   * Esperando confirmación de publicación del grupo.

* Publique el grupo principal antes de publicar cualquier grupo anidado en:

   * Todos los grupos deben publicarse de arriba hacia abajo.

![publicado en grupo](assets/group-published.png)

## Experiencia en publicación {#experience-on-publish}

Es posible experimentar los diferentes grupos cuando se inicia sesión, por ejemplo, con [usuarios de demostración](/help/communities/tutorials.md#demo-users) se usa para:

* Miembro del grupo Arte/Historia: `emily.andrews@mailinator.com/password`
   * El grupo restringido (secreto), artes/historia, es visible:
   * Puede ver grupos opcionales (públicos).
   * Posibilidad de unirse a grupos restringidos (abiertos).

* Administrador del grupo: `aaron.mcdonald@mailinator.com/password`

   * Puede ver grupos opcionales (públicos).
   * Posibilidad de unirse a grupos restringidos (abiertos).
   * No se pueden ver los grupos restringidos (secretos).

Acceso a las comunidades [Consolas de miembros y grupos](/help/communities/members.md) en autor para agregar otros usuarios a varios grupos de miembros que se correspondan con los grupos de la comunidad.
