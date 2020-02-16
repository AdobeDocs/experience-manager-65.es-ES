---
title: Consolas de administración
seo-title: Consolas de administración
description: Obtenga información sobre cómo utilizar las consolas de administración disponibles en AEM.
seo-description: Obtenga información sobre cómo utilizar las consolas de administración disponibles en AEM.
uuid: 82ab5267-2f2a-4772-85d5-678d883a0294
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6dbe82c2-7a25-49ab-a980-3635f0344817
docset: aem65
translation-type: tm+mt
source-git-commit: 954c1d5b06b54d59f523483ce5c1af36c2083a76

---


# Consolas de administración{#admin-consoles}

De forma predeterminada, se ha deshabilitado la capacidad de cambiar a la IU clásica a través de las consolas de administración. Por lo tanto, ya no se muestran los iconos emergentes que se vieron al pasar el ratón sobre determinados iconos de la consola, lo que permite acceder a la IU clásica.

Cada consola que tenga una versión de IU clásica en `/libs/cq/core/content/nav` puede volver a activarse individualmente para que la opción de IU **** clásica aparezca una vez más sobre el icono de la consola cuando se pase el ratón por encima.

En este ejemplo, estamos volviendo a habilitar la IU clásica para la consola Sitios.

1. Con CRXDE Lite, busque el nodo correspondiente a la consola de administración para la que desea volver a habilitar la IU clásica. Se encuentran en:

   `/libs/cq/core/content/nav`

   Por ejemplo

   [ `https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. Seleccione el nodo correspondiente a la consola para la que desea volver a habilitar la IU clásica. Para nuestro ejemplo, reactivaremos la IU clásica para la consola Sitios.

   `/libs/cq/core/content/nav/sites`

1. Crear una superposición con la opción Nodo **de** superposición; por ejemplo:

   * **Ruta**: `/apps/cq/core/content/nav/sites`
   * **Ubicación de la superposición**: `/apps/`
   * **Coincidir tipos** de nodos: activo (seleccione la casilla de verificación)

1. Agregue la siguiente propiedad booleana al nodo superpuesto:

   `enableDesktopOnly = {Boolean}true`

1. La opción de IU **** clásica está disponible de nuevo como opción emergente en la consola de administración.

   ![](assets/syui-01-2019-02-27-15-16-55.png)

Repita estos pasos para cada consola para la que desee volver a habilitar el acceso a la versión de la IU clásica.