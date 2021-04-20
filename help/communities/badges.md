---
title: Consola Distintivos
seo-title: Consola Distintivos
description: La consola Distintivos de comunidades le permite añadir distintivos personalizados que se pueden mostrar para los miembros cuando se ganan (se conceden) o cuando asumen una función específica en la comunidad (se asignan)
seo-description: La consola Distintivos de comunidades le permite añadir distintivos personalizados que se pueden mostrar para los miembros cuando se ganan (se conceden) o cuando asumen una función específica en la comunidad (se asignan)
uuid: 7103b133-ef3f-47d6-a2dc-4e6ff92e8fed
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 135b3077-5343-4888-858d-de5e9b1d4b04
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 4%

---


# Consola Distintivos {#badges-console}

## Acerca de los distintivos {#about-badges}

La consola Distintivos de comunidades permite agregar distintivos personalizados que se pueden mostrar para un miembro cuando se ganan (se conceden) o cuando asumen una función específica en la comunidad (se asignan).

### Visibilidad del distintivo {#badge-visibility}

Actualmente, los distintivos que un miembro de la comunidad gana o es asignado aparecerán junto con su nombre y avatar en las siguientes ubicaciones:

* Perfiles
* [Foros](/help/communities/forum.md)
* [P y R](/help/communities/working-with-qna.md)
* [Paneles](/help/communities/enabling-leaderboard.md)
* [Ideación](/help/communities/ideation-feature.md)

En el entorno de creación, vaya a la consola Distintivos :

* Desde la navegación global: **[!UICONTROL Herramientas]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Distintivos]**

Esta consola muestra los distintivos actualmente disponibles y desde los que se pueden añadir nuevos distintivos.

![badges-homepage](assets/badges-homepage.png)

## Crear distintivo {#create-badge}

Se crea un distintivo cargando una imagen suficientemente pequeña (72 ppp con una altura que oscila entre 26 y 32 píxeles) y proporcionando un nombre. La imagen del distintivo se almacena en el repositorio en `/libs/settings/community/badging/images` y se duplica automáticamente en el entorno de publicación.

Si el entorno de publicación es un conjunto de editores, es necesario configurar la [sincronización de usuarios](/help/communities/sync.md).

![create-badge](assets/create-badge.png)

* **Cargar imagen**

   (*Requerido*) Una imagen de distintivo con un tamaño recomendado de 32 x 32 píxeles a 72 ppp en formato JPEG o PNG.

* **Nombre**

   (*Obligatorio*) El nombre del distintivo. Es el `Display Name` predeterminado, así como el nombre del nodo del repositorio. Si el `Name` no es un nombre de nodo de repositorio válido, se modificará.

* **Nombre para mostrar**

   (*Opcional*) El nombre que se mostrará para el distintivo en la interfaz de usuario. El valor predeterminado es el texto sin modificar introducido para `Name`.

* **Descripción**

   (*Opcional*) Una descripción para el distintivo.

## Información adicional {#additional-information}

Para obtener más información sobre la configuración de las reglas de puntuación y distintivo, consulte [Puntuación y distintivos](/help/communities/implementing-scoring.md).

Para administrar distintivos para miembros, consulte [Consola de miembros](/help/communities/members.md).
