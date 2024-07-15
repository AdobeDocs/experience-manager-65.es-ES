---
title: Consola Insignias
description: La consola Distintivos de comunidades le permite añadir insignias personalizadas que se pueden mostrar para los miembros cuando ganan (reciben premios) o cuando asumen un rol específico en la comunidad (asignan)
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 50ed9ec4-ff04-4f9d-aefb-0837542a9455
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 4%

---

# Consola Insignias {#badges-console}

## Acerca de los distintivos {#about-badges}

La consola Distintivos de comunidades le permite añadir insignias personalizadas que se pueden mostrar para un miembro cuando se ganan (se otorgan) o cuando asumen un rol específico en la comunidad (se asignan).

### Visibilidad de distintivo {#badge-visibility}

Actualmente, las insignias que gana un miembro de la comunidad, o que se le asigna, aparecen junto con su nombre y avatar en las siguientes ubicaciones:

* Perfiles
* [Foros](/help/communities/forum.md)
* [P y R](/help/communities/working-with-qna.md)
* [Tablas de clasificación](/help/communities/enabling-leaderboard.md)
* [Ideación](/help/communities/ideation-feature.md)

En el entorno de creación, vaya a la consola Insignias:

* Desde la navegación global: **[!UICONTROL Herramientas]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Insignias]**

Esta consola muestra los distintivos disponibles actualmente y desde los cuales se pueden agregar nuevos distintivos.

![badges-homepage](assets/badges-homepage.png)

## Crear distintivo {#create-badge}

Un distintivo se crea cargando una imagen convenientemente pequeña (72 ppp con una altura que varía entre 26 y 32 píxeles) y proporcionando un nombre. La imagen del distintivo se almacena en el repositorio en `/libs/settings/community/badging/images` y se replica automáticamente en el entorno de publicación.

Si el entorno de publicación es una granja de editores, es necesario configurar la [sincronización de usuarios](/help/communities/sync.md).

![crear distintivo](assets/create-badge.png)

* **Cargar imagen**

  (*Obligatorio*) Una imagen de distintivo con un tamaño recomendado de 32 x 32 píxeles a 72 ppp en formato JPEG o PNG.

* **Nombre**

  (*Requerido*) El nombre del distintivo. Es el valor predeterminado `Display Name` y el nombre del nodo del repositorio. Si `Name` no es un nombre de nodo de repositorio válido, se modifica.

* **Nombre para mostrar**

  (*Opcional*) El nombre que se mostrará para el distintivo en la interfaz de usuario. El valor predeterminado es el texto sin modificar especificado para `Name`.

* **Descripción**

  (*Opcional*) Una descripción del distintivo.

## Información adicional {#additional-information}

Para obtener más información sobre la configuración de reglas de puntuación e insignias, consulte [Puntuación e insignias](/help/communities/implementing-scoring.md).

Para administrar distintivos para miembros, consulte [Consola de miembros](/help/communities/members.md).
