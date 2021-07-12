---
title: Consolas de comunidades
seo-title: Consolas de comunidades
description: Consolas de comunidad explicadas
seo-description: Consolas de comunidad explicadas
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
source-wordcount: '345'
ht-degree: 2%

---

# Consolas de comunidades {#communities-consoles}

Las consolas de AEM Communities, disponibles en el entorno de creación desde el panel de navegación global, proporcionan acceso a tareas administrativas como:

* [Creación de un sitio de comunidad](sites-console.md)
* Adición de [grupos](groups.md) anidados dentro del sitio
* Administración de [plantillas de sitio de la comunidad](sites.md)
* Administración de [miembros de la comunidad](members.md)
* [](moderate-ugc.md) Moderación del contenido generado por el usuario (UGC)
* Crear [distintivos personalizados](badges.md)
* Configuración del [almacenamiento predeterminado para UGC](srp-config.md)

Cuando [UGC storage](working-with-srp.md) está configurado para ser un almacén común compartido por los entornos de autor y publicación, la [consola de moderación](moderation.md), disponible tanto en los entornos de autor como de publicación, funciona en una instancia solitaria de UGC.

En el entorno de creación, después de iniciar sesión con privilegios de administrador, las consolas `Communities` están disponibles en las consolas de herramientas y navegación.

>[!NOTE]
>
>En el entorno de publicación, un [sitio de la comunidad](sites-console.md) mostrará un elemento de menú `Administration` cuando el miembro que ha iniciado sesión tenga los privilegios adecuados.

## Panel de navegación global {#global-navigation-panel}

Seleccione el icono `Adobe Experience Manager` en la esquina superior izquierda para abrir el panel de navegación global y acceder a dos iconos:

* [Consola de navegación](#navigation-console)
* [Consola Herramientas](tools.md)

## Consola de navegación {#navigation-console}

Para acceder a las distintas consolas de Communities, en la navegación global, seleccione **navigation, Communities**.

![comunidades](assets/communities.png)

* [Sites](sites-console.md)

   Se puede acceder a la consola Sitios desde el entorno de creación con el fin de crear y administrar sitios de la comunidad y sus [grupos](groups.md).

* [Moderación](moderation.md)

   La consola Moderación es para la moderación masiva de UGC y en el entorno de creación. En el entorno de publicación, se puede acceder a una consola de moderación masiva similar a los miembros de la comunidad a los que se haya asignado la función de [moderador de la comunidad](users.md#publishenvironmentusersandgroups) para uno o varios sitios de la comunidad.

* [Miembros, grupos](members.md)

   Las consolas Miembros y Grupos sirven para administrar los miembros de la comunidad y los grupos de miembros que existen en el entorno de publicación desde el entorno de creación.

* [Informes](reports.md)

   La consola Informes es donde se pueden generar informes sobre asignaciones, vistas de página y contenido publicado (UGC) cuando un sitio de la comunidad tiene [Adobe Analytics](sites-console.md#analytics) habilitado. La consola solo está disponible en el entorno de creación.

* [Medios](resources.md)

   La consola Recursos es donde los [administradores de habilitación](enablement.md#communitymanagers) crean, administran y asignan recursos a los miembros de un [sitio de la comunidad de habilitación](overview.md#enablement-community). La consola solo está disponible en el entorno de creación.

## Consola Herramientas {#tools-console}

Para acceder a [Communities Tools](tools.md) (anteriormente, consola de administración) desde la navegación global: **[!UICONTROL Herramientas]** > **[!UICONTROL Comunidades]**
