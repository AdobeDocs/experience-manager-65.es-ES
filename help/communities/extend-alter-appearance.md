---
title: Modificar el aspecto (HBS)
seo-title: Alter the Appearance
description: Modificación de los scripts HBS
seo-description: Modify the HBS scripts
uuid: cff24505-dbb3-4312-9b1b-c1693b8d1c98
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e0da09b3-725d-4ed1-9273-2532132f6918
docset: aem65
exl-id: 27e1bff3-385e-4ced-87af-54044b7e8812
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Modificar el aspecto (HBS) {#alter-the-appearance-hbs}

Ahora que los componentes del sistema de comentarios personalizados del directorio de aplicaciones (/apps) están implementados, con un resourceSuperType que hace referencia al sistema de comentarios predeterminado y el Model/View personalizado registrado, es posible modificar la implementación.

Para una demostración sencilla, se elimina una característica visual, el avatar mostrado por el usuario que ha iniciado sesión y que publica un comentario.

>[!NOTE]
>
>Para utilizar la extensión, la instancia del sistema de comentarios de un sitio web que se verá afectada (/content) debe establecer su resourceType en el sistema de comentarios personalizado.

## Modificación de los scripts HBS {#modify-the-hbs-scripts}

Uso [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Apertura [/apps/custom/components/comments/comment/**comment.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * Comente la etiqueta que incluye el avatar para una publicación de comentario (~ línea 21):

      ```
        <!--
         <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
         -->
      ```

* Apertura [/apps/custom/components/comments/**comments.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * Comente la etiqueta que incluye el avatar para la siguiente entrada de comentario (~ línea 44):

      ```
        <!--
         <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
         -->
      ```

* Select **Guardar todo**

### Replicar aplicación personalizada {#replicate-custom-app}

Una vez modificada la aplicación, es necesario volver a replicar el componente personalizado.

Una forma de hacerlo es:

* Desde el menú principal

   * Select **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Replicación]**.
   * Select **[!UICONTROL Activar árbol]**.
   * Establezca `Start Path` a `/apps/custom`.
   * Anular selección **[!UICONTROL Solo modificado]**.
   * Select **[!UICONTROL Activar]** botón.

### Ver comentario modificado en la página de muestra publicada {#view-modified-comment-on-published-sample-page}

[Continuación de la experiencia](/help/communities/extend-sample-page.md#publish-sample-page) en la instancia de publicación, que aún ha iniciado sesión como el mismo usuario, ahora es posible actualizar la página en el entorno de publicación para ver la modificación para eliminar el avatar:

![ver-modificado-content](assets/view-modified-content.png)

### Paquete de extensión de comentario de ejemplo {#sample-comment-extension-package}

Se adjunta un paquete de la aplicación de comentarios personalizados creada en este tutorial.

[Obtener archivo](assets/sample-comment-extension-6-1-fp3.zip)
