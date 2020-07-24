---
title: Modificar el aspecto
seo-title: Modificar el aspecto
description: Modificación de la secuencia de comandos
seo-description: Modificación de la secuencia de comandos
uuid: 30555b9f-da29-4115-9ed5-25f80a247bd6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: c9d31ed8-c105-453b-bd3c-4660dfd81272
docset: aem65
translation-type: tm+mt
source-git-commit: 4e823136604d291c5b867634268f67e003185a15
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Modificar el aspecto {#alter-the-appearance}

## Modificación de la secuencia de comandos {#modify-the-script}

La secuencia de comandos comment.hbs es responsable de crear el HTML general para cada comentario.

Para no mostrar el avatar al lado de cada comentario publicado:

1. Copiar `comment.hbs`de `libs`a `apps`

   1. Seleccione `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. Seleccionar **copia**
   1. Seleccione `/apps/social/commons/components/hbs/comments/comment`
   1. Seleccionar **pegar**

1. Abrir las superposiciones `comment.hbs`

   * Doble-clic en el nodo `comment.hbs` en `/apps/social/commons/components/hbs/comments/comment folder`

1. Busque las líneas siguientes y elimínelas o coméntelas:

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

Elimine las líneas o rodeándolas con `<!--` y `-->` comentándolas. Además, los caracteres &#39;xxx&#39; se están agregando como un indicador visual de dónde se habría encontrado el avatar.

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### Replicar la superposición {#replicate-the-overlay}

Inserte el componente de comentarios superpuestos en la instancia de publicación mediante la herramienta de replicación.

>[!NOTE]
>
>Una forma más sólida de replicación sería crear un paquete en el Administrador de paquetes y [activarlo](/help/sites-administering/package-manager.md#replicating-packages) . Se puede exportar y archivar un paquete.


En la navegación global, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Implementación]** > **[!UICONTROL Replicación]** y haga clic en **[!UICONTROL Activar árbol]**.

Para la Ruta de Inicio, introduzca `/apps/social/commons` y seleccione **[!UICONTROL Activar]**.

![verify-content-template](assets/verify-content-template.png)

### Resultados de Vista {#view-results}

Si inicia sesión en la instancia de publicación como administrador, por ejemplo: https://localhost:4503/crx/de como administrador/administrador, puede comprobar que los componentes superpuestos están allí.

Si cierra la sesión y vuelve a iniciarla `aaron.mcdonald@mailinator.com/password` y actualiza la página, observará que el comentario publicado ya no se muestra con un avatar, sino que se muestra un sencillo &#39;xxx&#39;.

![create-template-component](assets/create-template-component.png)

