---
title: Crear nodos
seo-title: Crear nodos
description: Superponer el sistema de comentarios
seo-description: Superponer el sistema de comentarios
uuid: 802ae28b-9989-4c2c-b466-ab76a724efd3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cd4f53ee-537b-4f10-a64f-474ba2c44576
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Crear nodos {#create-nodes}

Superponga el sistema de comentarios con una versión personalizada copiando el número mínimo de archivos necesarios de /libs en /apps y modificándolos en /apps.

>[!CAUTION]
>
>El contenido de la carpeta /libs nunca se edita porque cualquier reinstalación o actualización puede eliminar o reemplazar la carpeta /libs mientras el contenido de la carpeta /apps no se modifica.

Con [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) en una instancia de autor, comience por crear una ruta en la carpeta /apps que sea idéntica a la ruta a los componentes superpuestos en la carpeta /libs.

La ruta que se está duplicando es

* `/libs/social/commons/components/hbs/comments/comment`

Algunos nodos de la ruta son carpetas y otros componentes.

1. Vaya a [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. Crear `/apps/social` (si no existe)
   * Seleccionar `/apps` nodo
   * **[!UICONTROL Crear > Carpeta...]**
      * Introduzca el nombre: `social`
1. Seleccionar `social` nodo
   * **[!UICONTROL Crear > Carpeta...]**
      * Introduzca el nombre: `commons`
1. Seleccionar `commons` nodo
   * **[!UICONTROL Crear > Carpeta...]**
      * Introduzca el nombre: `components`
1. Seleccionar `components` nodo
   * **[!UICONTROL Crear > Carpeta..]**.
      * Introduzca el nombre: `hbs`
1. Seleccionar `hbs` nodo
   * **[!UICONTROL Crear > Crear componente...]**
      * Escriba la etiqueta: `comments`
      * Enter Title: `Comments`
      * Enter Description: `List of comments without showing avatars`
      * Super Type: `social/commons/components/comments`
      * Especifique el grupo: `Communities`
      * Haga clic en **[!UICONTROL Siguiente]** hasta **[!UICONTROL Aceptar]**
1. Seleccionar `comments` nodo

   * **[!UICONTROL Crear > Crear componente...]**

      * Escriba la etiqueta: `comment`
      * Enter Title: `Comment`
      * Enter Description: `A comment instance without avatars`
      * Super Type: `social/commons/components/comments/comment`
      * Especifique el grupo: `.hidden`
      * Haga clic en **[!UICONTROL Siguiente]** hasta **[!UICONTROL Aceptar]**
   * Seleccione **[!UICONTROL Guardar todo]**
1. Eliminar el valor predeterminado `comments.jsp`
   * Seleccionar nodo `/apps/social/commons/components/hbs/comments/comments.jsp`
   * Seleccionar **[!UICONTROL eliminación]**
1. Eliminar el comentario predeterminado.jsp
   * seleccionar nodo `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * Seleccionar **[!UICONTROL eliminación]**
   * Seleccione **[!UICONTROL Guardar todo]**

>[!NOTE]
>
>Para preservar la cadena de herencia, la `Super Type` (propiedad `sling:resourceSuperType`) de los componentes de superposición se establece en el mismo valor que el `Super Type` de los componentes que se superponen, en este caso
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`
>



La propia superposición `Type`(propiedad `sling:resourceType`) debe ser una autorreferencia relativa para que cualquier contenido no encontrado en /apps se busque en /libs.
* Nombre: `sling:resourceType`
* Tipo: `String`
* Value: `social/commons/components/hbs/comments`

1. Seleccione el verde `[+] Add`
   * Nombre: `sling:resourceType`
   * Tipo: `String`
   * Value: `social/commons/components/hbs/comments/comment`
1. Seleccione el verde `[+] Add`
   * Seleccione **[!UICONTROL Guardar todo]**

![climage_1-4](assets/chlimage_1-4.png)

