---
title: Consolas de Communities
seo-title: Communities Consoles
description: Consolas de la comunidad explicadas
seo-description: Community Consoles explained
uuid: 1c5b2600-9059-4b44-9741-f1b627423d3c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 5fa9ee8b-5893-4ae9-a986-bfdbb00f355f
role: Admin
exl-id: 36f2e3d2-46c7-48a8-a1e9-213f581bd9f3
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 2%

---

# Consolas de Communities {#communities-consoles}

Las consolas de AEM Communities, disponibles en el entorno de creación desde el panel de navegación global, proporcionan acceso a tareas administrativas como las siguientes:

* [Creación de un sitio de comunidad](sites-console.md)
* Agregando [grupos](groups.md) anidados dentro del sitio
* Administración [plantillas de sitio de comunidad](sites.md)
* Administración [miembros de la comunidad](members.md)
* [Moderando](moderate-ugc.md) contenido generado por el usuario (UGC)
* Crear [insignias personalizadas](badges.md)
* Configuración de la [almacenamiento predeterminado para UGC](srp-config.md)

Cuándo [Almacenamiento UGC](working-with-srp.md) está configurado para ser un almacén común compartido por los entornos de autor y publicación, el [consola de moderación](moderation.md), disponible tanto en entornos de creación como de publicación, funciona en una instancia única de UGC.

En el entorno de creación, después de iniciar sesión con privilegios de administrador, la variable `Communities` Las consolas están disponibles en las consolas de navegación y herramientas.

>[!NOTE]
>
>En el entorno de publicación, una [sitio comunitario](sites-console.md) mostrará un `Administration` elemento de menú cuando el miembro que ha iniciado sesión tiene los privilegios adecuados.

## Panel de navegación global {#global-navigation-panel}

Seleccione el `Adobe Experience Manager` en la esquina superior izquierda para abrir el panel de navegación global y acceder a dos iconos:

* [Consola de navegación](#navigation-console)
* [Consola Herramientas](tools.md)

## Consola de navegación {#navigation-console}

Para acceder a las distintas consolas de Communities, en navegación global, seleccione **navegación, Communities**.

![comunidades](assets/communities.png)

* [Sites](sites-console.md)

   La consola Sitios es accesible en el entorno de creación con el fin de crear y administrar los sitios de la comunidad y sus [grupos](groups.md).

* [Moderación](moderation.md)

   La consola Moderación se utiliza para la moderación masiva de UGC y en el entorno de creación. En el entorno de publicación hay disponible una consola de moderación masiva similar a la que pueden acceder los miembros de la comunidad a los que se les ha asignado la función [moderador de la comunidad](users.md#publishenvironmentusersandgroups) para uno o más sitios de la comunidad.

* [Miembros, grupos](members.md)

   Las consolas Miembros y grupos se utilizan para administrar miembros de la comunidad y grupos de miembros que existen en el entorno de publicación desde el entorno de creación.

* [Informes](reports.md)

   En la consola Informes es donde se pueden generar informes sobre asignaciones, vistas de página y contenido publicado (UGC) cuando un sitio de la comunidad tiene [Adobe Analytics habilitado](sites-console.md#analytics). La consola solo está disponible en el entorno de creación.

* [Recursos](resources.md)

   La consola Recursos es donde [administradores de habilitación](enablement.md#communitymanagers) crear, administrar y asignar recursos a los miembros de un [sitio de la comunidad de habilitación](overview.md#enablement-community). La consola solo está disponible en el entorno de creación.

## Consola Herramientas {#tools-console}

Para acceder a [Herramientas de Communities](tools.md) (anteriormente consola de administración), desde navegación global: **[!UICONTROL Herramientas]** > **[!UICONTROL Communities]**
