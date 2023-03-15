---
title: Consola Insignias
seo-title: Badges Console
description: La consola Distintivos de comunidades le permite añadir insignias personalizadas que se pueden mostrar para los miembros cuando ganan (reciben premios) o cuando asumen un rol específico en la comunidad (asignan)
seo-description: The Communities Badges console lets you add custom badges that can be displayed for members when earned (awarded) or when they take on a specific role in the community (assigned)
uuid: 7103b133-ef3f-47d6-a2dc-4e6ff92e8fed
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 135b3077-5343-4888-858d-de5e9b1d4b04
docset: aem65
role: Admin
exl-id: 50ed9ec4-ff04-4f9d-aefb-0837542a9455
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 4%

---

# Consola Insignias {#badges-console}

## Acerca de los distintivos {#about-badges}

La consola Distintivos de comunidades permite agregar insignias personalizadas que se pueden mostrar para un miembro cuando se ganan (se otorgan) o cuando asumen un rol específico en la comunidad (se asignan).

### Visibilidad de distintivo {#badge-visibility}

Actualmente, las insignias que gana un miembro de la comunidad o que se le asigna aparecen junto con su nombre y avatar en las siguientes ubicaciones:

* Perfiles
* [Foros](/help/communities/forum.md)
* [P y R](/help/communities/working-with-qna.md)
* [Tablas de clasificación](/help/communities/enabling-leaderboard.md)
* [Ideación](/help/communities/ideation-feature.md)

En el entorno de creación, vaya a la consola Insignias:

* Desde la navegación global: **[!UICONTROL Herramientas]** > **[!UICONTROL Communities]** > **[!UICONTROL Insignias]**

Esta consola muestra los distintivos disponibles actualmente y desde los cuales se pueden agregar nuevos distintivos.

![badges-homepage](assets/badges-homepage.png)

## Crear distintivo {#create-badge}

Para crear un distintivo, cargue una imagen muy pequeña (72 ppp con una altura de entre 26 y 32 píxeles) y proporcione un nombre. La imagen del distintivo se almacena en el repositorio en `/libs/settings/community/badging/images` y se duplican automáticamente en el entorno de publicación.

Si el entorno de publicación es una granja de editores, es necesario configurar [sincronización de usuarios](/help/communities/sync.md).

![create-badge](assets/create-badge.png)

* **Cargar imagen**

   (*Requerido*) Imagen de distintivo con un tamaño recomendado de 32 x 32 píxeles a 72 ppp en formato JPEG o PNG.

* **Nombre**

   (*Requerido*) El nombre del distintivo. Es la opción predeterminada `Display Name` así como el nombre del nodo del repositorio. Si la variable `Name` no es un nombre de nodo de repositorio válido, se modificará.

* **Nombre para mostrar**

   (*Opcional*) Nombre que se mostrará para el distintivo en la interfaz de usuario. El valor por defecto es el texto sin modificar introducido para `Name`.

* **Descripción**

   (*Opcional*) Una descripción del distintivo.

## Información adicional {#additional-information}

Para obtener más información sobre la configuración de reglas de puntuación e insignias, consulte [Puntuación y distintivos](/help/communities/implementing-scoring.md).

Para administrar insignias para miembros, consulte [Consola Miembros](/help/communities/members.md).
