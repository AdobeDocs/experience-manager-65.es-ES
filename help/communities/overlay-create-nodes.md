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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 8%

---


# Crear nodos {#create-nodes}

Superponga el sistema de comentarios con una versión personalizada copiando el número mínimo de archivos necesarios de `/libs` a `/apps` y modificándolos en `/apps`.

>[!CAUTION]
>
>El contenido de la carpeta /libs nunca se edita porque cualquier reinstalación o actualización puede eliminar o reemplazar la carpeta /libs mientras el contenido de la carpeta /apps no se modifica.

El uso de [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) en una instancia de autor comienza por crear una ruta en la carpeta /apps que es idéntica a la ruta de acceso a los componentes superpuestos en la carpeta /libs.

La ruta que se está duplicando es:

* `/libs/social/commons/components/hbs/comments/comment`

Algunos nodos de la ruta son carpetas y otros componentes.

1. Vaya a [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. Crear `/apps/social` (si aún no existe)
   * Seleccionar nodo `/apps`
   * **[!UICONTROL Crear > Carpeta...]**
      * Introduzca el nombre: `social`
1. Seleccionar nodo `social`
   * **[!UICONTROL Crear]** >  **[!UICONTROL Carpeta...]**
      * Introduzca el nombre: `commons`
1. Seleccionar nodo `commons`
   * **[!UICONTROL Crear > Carpeta...]**
      * Introduzca el nombre: `components`
1. Seleccionar nodo `components`
   * **[!UICONTROL Crear > Carpeta..]**.
      * Introduzca el nombre: `hbs`
1. Seleccionar nodo `hbs`
   * **[!UICONTROL Crear]**  >  **[!UICONTROL Crear componente...]**
      * Escriba la etiqueta: `comments`
      * Escriba el título: `Comments`
      * Escriba la descripción: `List of comments without showing avatars`
      * Super Type: `social/commons/components/comments`
      * Especifique el grupo: `Communities`
      * Haga clic **[!UICONTROL Siguiente]** hasta **[!UICONTROL Aceptar]**
1. Seleccionar nodo `comments`

   * **[!UICONTROL Crear]**  >  **[!UICONTROL Crear componente...]**

      * Escriba la etiqueta: `comment`
      * Escriba el título: `Comment`
      * Escriba la descripción: `A comment instance without avatars`
      * Super Tipo: `social/commons/components/comments/comment`
      * Especifique el grupo: `.hidden`
      * Haga clic **[!UICONTROL Siguiente]** hasta **[!UICONTROL Aceptar]**
   * Seleccione **[!UICONTROL Guardar todo]**
1. Eliminar el valor predeterminado `comments.jsp`
   * Seleccionar nodo `/apps/social/commons/components/hbs/comments/comments.jsp`
   * Seleccione **[!UICONTROL Eliminar]**
1. Eliminar el comentario predeterminado.jsp
   * select node `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * Seleccione **[!UICONTROL Eliminar]**
   * Seleccione **[!UICONTROL Guardar todo]**

>[!NOTE]
>
>Para preservar la cadena de herencia, la `Super Type` (propiedad `sling:resourceSuperType`) de los componentes de superposición se establece en el mismo valor que la `Super Type` de los componentes que se superponen, en este caso:
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`


La propia `Type`(propiedad `sling:resourceType`) de la superposición debe ser una autorreferencia relativa para que el contenido no encontrado en /apps se busque en /libs.
* Nombre: `sling:resourceType`
* Tipo: `String`
* Value: `social/commons/components/hbs/comments`

1. Seleccione el `[+] Add` verde
   * Nombre: `sling:resourceType`
   * Tipo: `String`
   * Valor: `social/commons/components/hbs/comments/comment`
1. Seleccione el `[+] Add` verde
   * Seleccione **[!UICONTROL Guardar todo]**

![create-nodes](assets/create-nodes.png)

