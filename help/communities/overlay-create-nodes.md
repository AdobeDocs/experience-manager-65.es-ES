---
title: Crear nodos
description: Aprenda a superponer el sistema de comentarios con una versión personalizada copiando el número mínimo de archivos necesarios de /libs y editándolos en /apps.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3d72cbdf-5eb4-477d-aa61-035a846f7dcb
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# Crear nodos {#create-nodes}

Superponga el sistema de comentarios con una versión personalizada copiando el número mínimo de archivos necesarios de `/libs` en `/apps` y modificándolos en `/apps`.

>[!CAUTION]
>
>El contenido de la carpeta /libs nunca se edita porque cualquier reinstalación o actualización puede eliminar o reemplazar la carpeta /libs mientras el contenido de la carpeta /apps no se modifica.

Para empezar, use [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) en una instancia de autor y cree una ruta en la carpeta /apps que sea idéntica a la ruta de los componentes superpuestos en la carpeta /libs.

La ruta que se está duplicando es:

* `/libs/social/commons/components/hbs/comments/comment`

Algunos nodos de la ruta son carpetas y otros son componentes.

1. Vaya a [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. Crear `/apps/social` (si aún no existe)
   * Seleccionar nodo `/apps`
   * **[!UICONTROL Crear > Carpeta]**
      * Escriba el nombre: `social`
1. Seleccionar nodo `social`
   * **[!UICONTROL Crear]** > **[!UICONTROL Carpeta]**
      * Escriba el nombre: `commons`
1. Seleccionar nodo `commons`
   * **[!UICONTROL Crear > Carpeta]**
      * Escriba el nombre: `components`
1. Seleccionar nodo `components`
   * **[!UICONTROL Crear > Carpeta]**.
      * Escriba el nombre: `hbs`
1. Seleccionar nodo `hbs`
   * **[!UICONTROL Crear]** > **[!UICONTROL Crear componente]**
      * Especifique la etiqueta: `comments`
      * Escriba el título: `Comments`
      * Escriba la descripción: `List of comments without showing avatars`
      * Supertipo: `social/commons/components/comments`
      * Introducir grupo: `Communities`
      * Haga clic en **[!UICONTROL Siguiente]** hasta **[!UICONTROL Aceptar]**
1. Seleccionar nodo `comments`

   * **[!UICONTROL Crear]** > **[!UICONTROL Crear componente]**

      * Especifique la etiqueta: `comment`
      * Escriba el título: `Comment`
      * Escriba la descripción: `A comment instance without avatars`
      * Supertipo: `social/commons/components/comments/comment`
      * Introducir grupo: `.hidden`
      * Haga clic en **[!UICONTROL Siguiente]** hasta **[!UICONTROL Aceptar]**
   * Seleccionar **[!UICONTROL Guardar todo]**
1. Eliminar el valor predeterminado `comments.jsp`
   * Seleccionar nodo `/apps/social/commons/components/hbs/comments/comments.jsp`
   * Seleccionar **[!UICONTROL Eliminar]**
1. Elimine el archivo comment.jsp predeterminado
   * seleccionar nodo `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * Seleccionar **[!UICONTROL Eliminar]**
   * Seleccionar **[!UICONTROL Guardar todo]**

>[!NOTE]
>
>Para conservar la cadena de herencia, el `Super Type` (propiedad `sling:resourceSuperType`) de los componentes de superposición se establecen con el mismo valor que el `Super Type` de los componentes que se superponen, en este caso:
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`

El propio `Type` (propiedad `sling:resourceType`) de la superposición debe ser una referencia automática relativa para que cualquier contenido que no se encuentre en /apps se busque en /libs.
* Nombre: `sling:resourceType`
* Tipo: `String`
* Valor: `social/commons/components/hbs/comments`

1. Seleccionar el `[+] Add` verde
   * Nombre: `sling:resourceType`
   * Tipo: `String`
   * Valor: `social/commons/components/hbs/comments/comment`
1. Seleccionar el `[+] Add` verde
   * Seleccionar **[!UICONTROL Guardar todo]**

![create-nodes](assets/create-nodes.png)
