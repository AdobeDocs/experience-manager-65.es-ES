---
title: Modificar el aspecto visual (HBS)
description: Aprenda a cambiar la apariencia (HBS) editando los scripts de HBS.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 27e1bff3-385e-4ced-87af-54044b7e8812
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Modificar el aspecto visual (HBS) {#alter-the-appearance-hbs}

Ahora que los componentes del sistema de comentarios personalizado del directorio de aplicaciones (/apps) están instalados, con un resourceSuperType que hace referencia al sistema de comentarios predeterminado y el modelo/vista personalizado registrado, puede editar la implementación.

Para una demostración sencilla, se elimina una característica visual, el avatar que se muestra del usuario que ha iniciado sesión y que publica un comentario.

>[!NOTE]
>
>Para utilizar la extensión, la instancia del sistema de comentarios de un sitio web afectado (/content) debe establecer su resourceType para que sea el sistema de comentarios personalizado.

## Modificación de los scripts HBS {#modify-the-hbs-scripts}

Uso de [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Abrir [/apps/custom/components/comments/comment/**comment.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * Comente la etiqueta que incluye el avatar para una publicación de comentario (~ línea 21):

     ```
       <!--
        <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
        -->
     ```

* Abrir [/apps/custom/components/comments/**comments.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * Convierta en comentario la etiqueta que incluye el avatar para la siguiente entrada de comentario (~ línea 44):

     ```
       <!--
        <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
        -->
     ```

* Seleccionar **Guardar todo**

### Replicar aplicación personalizada {#replicate-custom-app}

Una vez modificada la aplicación, es necesario volver a replicar el componente personalizado.

Una forma de hacerlo es:

* Desde el menú principal

   * Seleccionar **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Replicación]**.
   * Seleccionar **[!UICONTROL Activar árbol]**.
   * Establecer `Start Path` hasta `/apps/custom`.
   * Anular selección **[!UICONTROL Solo modificadas]**.
   * Seleccionar **[!UICONTROL Activar]** botón.

### Ver comentario modificado en la página de muestra publicada {#view-modified-comment-on-published-sample-page}

[Continuación de la experiencia](/help/communities/extend-sample-page.md#publish-sample-page) en la instancia de publicación, que aún tiene la sesión iniciada por el mismo usuario, ahora es posible actualizar la página en el entorno de publicación para ver la modificación y eliminar el avatar:

![view-modified-content](assets/view-modified-content.png)

### Paquete de extensiones de comentarios de muestra {#sample-comment-extension-package}

Se adjunta un paquete de la aplicación de comentarios personalizados creada en este tutorial.

[Obtener archivo](assets/sample-comment-extension-6-1-fp3.zip)
