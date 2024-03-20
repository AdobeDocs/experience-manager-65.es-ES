---
title: Editor
description: Aprenda a volver al Editor de IU clásico.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: 8540e1f0-22d7-4f48-85d9-7c44eb7185df
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 3%

---


# Editor{#editor}

De forma predeterminada, se ha deshabilitado la capacidad para cambiar a la IU clásica desde el editor.

Para volver a activar la opción **Abrir en IU clásica** en el **Información de página** , siga estos pasos.

1. Con el CRXDE Lite, busque el siguiente nodo:

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   Por ejemplo

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. Cree una superposición con la variable **Nodo de superposición** opción; por ejemplo:

   * **Ruta**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **Ubicación de superposición**: `/apps/`
   * **Hacer coincidir tipos de nodo**: activo (seleccione la casilla de verificación)

1. Agregue la siguiente propiedad de texto de varios valores al nodo superpuesto:

   `sling:hideProperties = ["granite:hidden"]`

1. El **Abrir en IU clásica** está disponible de nuevo en la **Información de página** al editar páginas.

   ![Abrir en la IU clásica opción desde la información de página](assets/syui-03-2019-02-27-15-19-48.png)
