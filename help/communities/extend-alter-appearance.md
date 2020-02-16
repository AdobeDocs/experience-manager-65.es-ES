---
title: Modificar el aspecto (HBS)
seo-title: Modificar el aspecto
description: Modificación de los scripts HBS
seo-description: Modificación de los scripts HBS
uuid: cff24505-dbb3-4312-9b1b-c1693b8d1c98
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e0da09b3-725d-4ed1-9273-2532132f6918
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Modificar el aspecto (HBS){#alter-the-appearance-hbs}

Ahora que los componentes del sistema de comentarios personalizados del directorio de aplicaciones (/apps) están implementados, con un resourceSuperType que hace referencia al sistema de comentarios predeterminado y el modelo/vista personalizado registrado, es posible modificar la implementación.

Para una demostración sencilla, se elimina una característica visual, el avatar que se muestra del usuario que ha iniciado sesión y que publica un comentario.

>[!NOTE]
>
>Para utilizar la extensión, la instancia del sistema de comentarios de un sitio web que se verá afectada (/content) debe establecer resourceType como el sistema de comentarios personalizado.

## Modificación de los scripts de HBS {#modify-the-hbs-scripts}

Uso de [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* open [/apps/custom/components/comments/comment/**comment.hbs **](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * comente la etiqueta que incluye el avatar para un comentario publicado (~ línea 21):

      ```
      <!--
       <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
       -->
      ```

* open [/apps/custom/components/comments/**comments.hbs **](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * comente la etiqueta que incluye el avatar de la siguiente entrada de comentario (~ línea 44):

      ```
      <!--
       <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
       -->
      ```

* seleccione **Guardar todo**

### Replicar aplicación personalizada {#replicate-custom-app}

Una vez modificada la aplicación, es necesario volver a replicar el componente personalizado.

Una manera de hacerlo es

* del menú principal

   * seleccione **Herramientas > Operaciones > Replicación**
   * select `Activate Tree`
   * set `Start Path`: to `/apps/custom`
   * deselect `Only Modified`
   * seleccionar `Activate`botón

### Ver comentario modificado en la página de muestra publicada {#view-modified-comment-on-published-sample-page}

[Continuando con la experiencia](/help/communities/extend-sample-page.md#publish-sample-page) en la instancia de publicación, que aún ha iniciado sesión como el mismo usuario, ahora es posible actualizar la página en el entorno de publicación para ver la modificación y eliminar el avatar:

![chlimage_1-136](assets/chlimage_1-136.png)

### Paquete de extensión de comentarios de muestra {#sample-comment-extension-package}

Se adjunta un paquete de la aplicación de comentarios personalizados creada en este tutorial.

[Obtener archivo](assets/sample-comment-extension-6-1-fp3.zip)
