---
title: Editor
seo-title: Editor
description: Obtenga información sobre cómo volver al Editor de IU clásica.
seo-description: Obtenga información sobre cómo volver al Editor de IU clásica.
uuid: ca8b07e7-014f-428e-82bd-87f3aae12f6e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 54903f3a-1e7e-4083-a2c9-b2ea4555d7fc
docset: aem65
translation-type: tm+mt
source-git-commit: 954c1d5b06b54d59f523483ce5c1af36c2083a76

---


# Editor{#editor}

De forma predeterminada, la capacidad de cambiar a la IU clásica desde el editor está deshabilitada.

Para volver a habilitar la opción **Abrir en la IU** clásica en el menú Información **de** página, siga estos pasos.

1. Con CRXDE Lite, busque el nodo siguiente:

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   Por ejemplo

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. Crear una superposición con la opción Nodo **de** superposición; por ejemplo:

   * **Ruta**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **Ubicación de la superposición**: `/apps/`
   * **Coincidir tipos** de nodos: activo (seleccione la casilla de verificación)

1. Agregue la siguiente propiedad de texto de varios valores al nodo superpuesto:

   `sling:hideProperties = ["granite:hidden"]`

1. La opción **Abrir en la IU** clásica vuelve a estar disponible en el menú Información **de** página al editar páginas.

   ![](assets/syui-03-2019-02-27-15-19-48.png)