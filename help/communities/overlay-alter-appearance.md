---
title: Modificar el aspecto
seo-title: Alter the Appearance
description: Modificación del script
seo-description: Modify the script
uuid: 30555b9f-da29-4115-9ed5-25f80a247bd6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: c9d31ed8-c105-453b-bd3c-4660dfd81272
docset: aem65
exl-id: cb8f6967-216c-46d3-a7ba-068b0f5e3b94
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---

# Modificar el aspecto {#alter-the-appearance}

## Modificación del script {#modify-the-script}

El script comment.hbs es responsable de crear el HTML general para cada comentario.

Para no mostrar el avatar junto a cada comentario publicado:

1. Copiar `comment.hbs`de `libs`hasta `apps`

   1. Seleccione `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. Seleccionar **[!UICONTROL Copiar]**
   1. Seleccione `/apps/social/commons/components/hbs/comments/comment`
   1. Seleccionar **[!UICONTROL Pegar]**

1. Abrir la superposición `comment.hbs`

   * Doble clic en el nodo `comment.hbs` in `/apps/social/commons/components/hbs/comments/comment folder`

1. Busque las siguientes líneas y elimínelas o coméntelas:

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

Elimine las líneas o rodee con `<!--` y `-->` para comentarlos. Además, los caracteres &quot;xxx&quot; se agregan como indicador visual de dónde habría estado el avatar.

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

Si cierra la sesión y vuelve a iniciarla como `aaron.mcdonald@mailinator.com/password` y actualice la página, observará que el comentario publicado ya no se muestra con un avatar, sino que se muestra un simple &quot;xxx&quot;.

![create-template-component](assets/create-template-component.png)
