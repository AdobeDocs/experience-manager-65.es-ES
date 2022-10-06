---
title: Admin Console
seo-title: Admin Consoles
description: Aprenda a utilizar los Admin Console disponibles en AEM.
seo-description: Lear how to use the Admin Consoles available in AEM.
uuid: 82ab5267-2f2a-4772-85d5-678d883a0294
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6dbe82c2-7a25-49ab-a980-3635f0344817
docset: aem65
exl-id: d4de517e-50bc-4ca5-89b1-295d259fd5bb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 2%

---

# Admin Console{#admin-consoles}

De forma predeterminada, se ha deshabilitado la capacidad de cambiar a la IU clásica a través de las consolas de administración. Por lo tanto, ya no se muestran los iconos emergentes que se veían al pasar el ratón por encima de determinados iconos de la consola, lo que permite acceder a la IU clásica.

Todas las consolas que tengan una versión de IU clásica en `/libs/cq/core/content/nav` se puede volver a habilitar de forma individual para que la variable **IU clásica** una vez más aparece sobre el icono de la consola cuando se pasa el ratón por encima.

En este ejemplo, se vuelve a habilitar la IU clásica para la consola Sitios .

1. Con CRXDE Lite, busque el nodo correspondiente a la consola de administración para la que desea volver a habilitar la IU clásica. Se encuentran en:

   `/libs/cq/core/content/nav`

   Por ejemplo

   [ `https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. Seleccione el nodo correspondiente a la consola para la que desea volver a habilitar la IU clásica. Para nuestro ejemplo, volveremos a habilitar la IU clásica para la consola Sitios .

   `/libs/cq/core/content/nav/sites`

1. Creación de una superposición con la variable **Nodo de superposición** , por ejemplo:

   * **Ruta**: `/apps/cq/core/content/nav/sites`
   * **Ubicación de la superposición**: `/apps/`
   * **Coincidir tipos de nodo**: activo (seleccione la casilla de verificación)

1. Agregue la siguiente propiedad booleana al nodo superpuesto:

   `enableDesktopOnly = {Boolean}true`

1. La variable **IU clásica** está disponible de nuevo como opción de ampliación en admin console.

   ![](assets/syui-01-2019-02-27-15-16-55.png)

Repita estos pasos para cada consola para la que desee volver a habilitar el acceso a la versión de la IU clásica.
