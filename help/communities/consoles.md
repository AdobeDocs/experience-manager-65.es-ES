---
title: Consolas de Communities
description: Obtenga información acerca de las consolas de la comunidad de Adobe Experience Manager disponibles en el entorno de creación desde el panel de navegación global.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 36f2e3d2-46c7-48a8-a1e9-213f581bd9f3
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# Consolas de Communities {#communities-consoles}

Las consolas de AEM Communities, disponibles en el entorno de creación desde el panel de navegación global, proporcionan acceso a tareas administrativas como las siguientes:

* [Creación de un sitio de comunidad](sites-console.md)
* Agregando [grupos](groups.md) anidados en el sitio
* Administrando [plantillas de sitio de la comunidad](sites.md)
* Administrando [miembros de la comunidad](members.md)
* [Moderando](moderate-ugc.md) contenido generado por el usuario (UGC)
* Crear [insignias personalizadas](badges.md)
* Configurando el [almacenamiento predeterminado para UGC](srp-config.md)

Cuando el [almacenamiento UGC](working-with-srp.md) está configurado para ser un almacén común compartido por los entornos Author y Publish, la [consola de moderación](moderation.md), disponible en los entornos Author y Publish, funciona en una instancia única de UGC.

En el entorno de creación, después de iniciar sesión con privilegios de administrador, las consolas `Communities` están disponibles en las consolas de herramientas y navegación.

>[!NOTE]
>
>En el entorno de Publish, un [sitio de la comunidad](sites-console.md) muestra un elemento de menú `Administration` cuando el miembro que ha iniciado sesión tiene los privilegios correspondientes.

## Panel de navegación global {#global-navigation-panel}

Seleccione el icono `Adobe Experience Manager` en la esquina superior izquierda para poder abrir el panel de navegación global y acceder a dos iconos:

* [Consola de navegación](#navigation-console)
* [Consola Herramientas](tools.md)

## Consola de navegación {#navigation-console}

Para acceder a las distintas consolas de Communities, en navegación global, seleccione **navigation, Communities**.

![comunidades](assets/communities.png)

* [Sites](sites-console.md)

  Se puede acceder a la consola Sites en el entorno de creación para crear y administrar los sitios de la comunidad y sus [grupos](groups.md).

* [Moderación](moderation.md)

  La consola Moderación se utiliza para la moderación masiva de UGC y en el entorno de creación. Se puede acceder a una consola de moderación en masa similar en el entorno de Publish para los miembros de la comunidad a los que se ha asignado la función de [moderador de la comunidad](users.md#publishenvironmentusersandgroups) en uno o más sitios de la comunidad.

* [Miembros, grupos](members.md)

  Las consolas Miembros y grupos se utilizan para administrar miembros de la comunidad y grupos de miembros que existen en el entorno de Publish desde el entorno de creación.

* [Informes](reports.md)

  En la consola Informes se generan informes sobre asignaciones, vistas de página y contenido publicado (UGC) cuando un sitio de la comunidad tiene [Adobe Analytics habilitado](sites-console.md#analytics). La consola solo está disponible en el entorno de creación.

## Consola Herramientas {#tools-console}

Para tener acceso a [Herramientas de comunidades](tools.md) (anteriormente la consola de administración), desde la navegación global: **[!UICONTROL Herramientas]** > **[!UICONTROL Comunidades]**
