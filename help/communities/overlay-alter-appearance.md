---
title: Modificar el aspecto
description: Aprenda a editar el script comment.hbs responsable de crear el HTML general para cada comentario en las comunidades de Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: cb8f6967-216c-46d3-a7ba-068b0f5e3b94
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# Modificar el aspecto {#alter-the-appearance}

## Modificación del script {#modify-the-script}

El `comment.hbs` El script es responsable de crear el HTML general para cada comentario.

Para no mostrar el avatar junto a cada comentario publicado:

1. Copiar `comment.hbs`de `libs`hasta `apps`

   1. Seleccione lo siguiente `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. Seleccionar **[!UICONTROL Copiar]**
   1. Seleccione lo siguiente `/apps/social/commons/components/hbs/comments/comment`
   1. Seleccionar **[!UICONTROL Pegar]**

1. Abrir la superposición `comment.hbs`

   * Haga doble clic en el nodo `comment.hbs` in `/apps/social/commons/components/hbs/comments/comment folder`

1. Busque las siguientes líneas y elimínelas o coméntelas:

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

Elimine las líneas o rodee con `<!--` y `-->` así que los comentas. Además, los caracteres &quot;xxx&quot; se agregan como indicador visual de dónde habría estado el avatar.

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### Duplicación de la superposición {#replicate-the-overlay}

Inserte el componente de comentarios superpuestos en la instancia de publicación mediante la herramienta de replicación.

>[!NOTE]
>
>Una forma más sólida de replicación sería crear un paquete en el Administrador de paquetes y [activar](/help/sites-administering/package-manager.md#replicating-packages) it. Se puede exportar y archivar un paquete.

En la navegación global, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Implementación]** > **[!UICONTROL Replicación]** y haga clic en **[!UICONTROL Activar árbol]**.

En Ruta de inicio, escriba `/apps/social/commons` y seleccione **[!UICONTROL Activar]**.

![verify-content-template](assets/verify-content-template.png)

### Ver resultados {#view-results}

Si inicia sesión en la instancia de publicación como administrador, por ejemplo, https://localhost:4503/crx/de como administrador/administrador, puede verificar que los componentes superpuestos estén presentes.

Si cierra la sesión y luego la inicia como `aaron.mcdonald@mailinator.com/password` y actualiza la página, observa que no se muestra un avatar con el comentario publicado. En su lugar, se muestra un &quot;xxx&quot; simple.

![create-template-component](assets/create-template-component.png)
