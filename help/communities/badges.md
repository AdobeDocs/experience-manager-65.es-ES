---
title: Consola de distintivos
seo-title: Consola de distintivos
description: La consola Distintivos de comunidades permite agregar distintivos personalizados que se pueden mostrar para los miembros cuando se ganan (se otorgan) o cuando asumen una función específica en la comunidad (se asignan)
seo-description: La consola Distintivos de comunidades permite agregar distintivos personalizados que se pueden mostrar para los miembros cuando se ganan (se otorgan) o cuando asumen una función específica en la comunidad (se asignan)
uuid: 7103b133-ef3f-47d6-a2dc-4e6ff92e8fed
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 135b3077-5343-4888-858d-de5e9b1d4b04
docset: aem65
translation-type: tm+mt
source-git-commit: 272eedc1585dbdea315b49d010e4b1d78cedc360

---


# Consola de distintivos {#badges-console}

## Acerca de los distintivos {#about-badges}

La consola Distintivos de comunidades permite agregar distintivos personalizados que se pueden mostrar para un miembro cuando se ganan (se otorgan) o cuando asumen una función específica en la comunidad (se asignan).

### Visibilidad del distintivo {#badge-visibility}

Actualmente, las insignias que un miembro de la comunidad gana o se asigna aparecerán junto con su nombre y avatar en las siguientes ubicaciones:

* Perfiles
* [Foros](/help/communities/forum.md)
* [P y R](/help/communities/working-with-qna.md)
* [Foros](/help/communities/enabling-leaderboard.md)
* [Ideación](/help/communities/ideation-feature.md)

En el entorno de creación, para acceder a la consola Badges

* Desde la navegación global, vaya a Herramientas de control **[UIC > Comunidades > Distintivos]**

Esta consola muestra las insignias disponibles actualmente y desde las cuales se pueden agregar nuevas insignias.

![chlimage_1-123](assets/chlimage_1-123.png)

## Crear distintivo {#create-badge}

Para crear un distintivo, cargue una imagen pequeña adecuada (72 ppp con una altura de entre 26 y 32 píxeles) y proporcione un nombre. La imagen del distintivo se almacena en el repositorio en `/etc/community/badging/images` y se replica automáticamente en el entorno de publicación.

Si el entorno de publicación es un conjunto de editores, es necesario configurar la sincronización [de](/help/communities/sync.md)usuarios.

![chlimage_1-124](assets/chlimage_1-124.png)

* **Cargar imagen**

   (*Requerido*) Imagen de un distintivo con un tamaño recomendado de 32 x 32 píxeles a 72 ppp en formato JPEG o PNG.

* **Nombre**

   (*Requerido*) El nombre del distintivo. Es el nombre predeterminado `Display Name` así como el nombre del nodo del repositorio. Si el nombre `Name` no es un nombre de nodo de repositorio válido, se modificará.

* **Nombre para mostrar**

   (*Opcional*) El nombre que se mostrará para el distintivo en la interfaz de usuario. El valor predeterminado es el texto sin modificar introducido para el `Name`.

* **Descripción**

   (*Opcional*) Descripción del distintivo.

## Información adicional {#additional-information}

Para obtener más información sobre la configuración de las reglas de puntuación y marca, consulte [Puntuación y distintivos](/help/communities/implementing-scoring.md).

Para administrar distintivos para miembros, consulte Consola [](/help/communities/members.md)de miembros.
