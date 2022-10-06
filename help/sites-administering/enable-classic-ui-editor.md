---
title: Editor
seo-title: Editor
description: Obtenga información sobre cómo volver al Editor de IU clásica.
seo-description: Learn how to switch back to the Classic UI Editor.
uuid: ca8b07e7-014f-428e-82bd-87f3aae12f6e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 54903f3a-1e7e-4083-a2c9-b2ea4555d7fc
docset: aem65
exl-id: 8540e1f0-22d7-4f48-85d9-7c44eb7185df
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 7%

---

# Editor{#editor}

De forma predeterminada, se ha desactivado la posibilidad de cambiar a la IU clásica desde el editor.

Para volver a activar la opción **Abrir en la IU clásica** en el **Información de la página** , siga estos pasos.

1. Con CRXDE Lite, busque el nodo siguiente:

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   Por ejemplo

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. Creación de una superposición con la variable **Nodo de superposición** , por ejemplo:

   * **Ruta**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **Ubicación de la superposición**: `/apps/`
   * **Coincidir tipos de nodo**: activo (seleccione la casilla de verificación)

1. Agregue la siguiente propiedad de texto de varios valores al nodo superpuesto:

   `sling:hideProperties = ["granite:hidden"]`

1. La variable **Abrir en la IU clásica** vuelve a estar disponible en la **Información de la página** al editar páginas.

   ![](assets/syui-03-2019-02-27-15-19-48.png)
