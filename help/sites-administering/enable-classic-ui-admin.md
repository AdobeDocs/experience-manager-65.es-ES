---
title: Admin Console
description: Aprenda a utilizar los Admin Console disponibles en Adobe Experience Manager.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: d4de517e-50bc-4ca5-89b1-295d259fd5bb
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---


# Admin Console{#admin-consoles}

De forma predeterminada, la capacidad de cambiar a la IU clásica mediante Admin Consoles está desactivada. Por lo tanto, ya no se muestran los iconos emergentes que se veían al pasar el ratón por encima de ciertos iconos de la consola, lo que permitía el acceso a la IU clásica.

Todas las consolas que tienen una versión de IU clásica en `/libs/cq/core/content/nav` se puede volver a habilitar individualmente para que el **IU clásica** Una vez más, la opción aparece sobre el icono de la consola cuando se pasa el ratón por encima.

En este ejemplo, vuelve a habilitar la IU clásica para la consola Sitios.

1. Con CRXDE Lite, busque el nodo correspondiente al Admin Console para el que desea volver a habilitar la IU clásica. Se encuentran en:

   `/libs/cq/core/content/nav`

   Por ejemplo

   [`https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. Seleccione el nodo correspondiente a la consola para la que desea volver a habilitar la IU clásica. Para este ejemplo, está volviendo a habilitar la IU clásica para la consola Sitios.

   `/libs/cq/core/content/nav/sites`

1. Cree una superposición con la variable **Nodo de superposición** opción; por ejemplo:

   * **Ruta**: `/apps/cq/core/content/nav/sites`
   * **Ubicación de superposición**: `/apps/`
   * **Hacer coincidir tipos de nodo**: activo (seleccione la casilla de verificación)

1. Agregue la siguiente propiedad booleana al nodo superpuesto:

   `enableDesktopOnly = {Boolean}true`

1. El **IU clásica** está disponible de nuevo como una opción emergente en el Admin Console.

   ![opción emergente de IU clásica](assets/syui-01-2019-02-27-15-16-55.png)

Repita estos pasos para cada consola para la que desee volver a habilitar el acceso a la versión de la IU clásica.
