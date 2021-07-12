---
title: Publicar colecciones en Brand Portal
seo-title: Publicar colecciones en Brand Portal
description: Obtenga información sobre cómo publicar y cancelar la publicación de colecciones en Brand Portal.
seo-description: Obtenga información sobre cómo publicar y cancelar la publicación de colecciones en Brand Portal.
uuid: 7de58548-4cfa-4a94-bac7-9e914dee9042
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 90e3fd0e-9bc3-4aff-8c7b-7408f5b940e8
docset: aem65
feature: Brand Portal
role: User
exl-id: 8f426012-d9ec-418e-8ab6-78e4aeff7538
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 37%

---

# Publicar colecciones en Brand Portal {#publish-collections-to-brand-portal}

Como administrador de recursos de Adobe Experience Manager (AEM), puede publicar colecciones en la instancia de AEM Assets Brand Portal para su organización. Sin embargo, primero debe integrar AEM Assets con Brand Portal. Para obtener más información, consulte [Configurar AEM Assets con Brand Portal](/help/assets/configure-aem-assets-with-brand-portal.md).

Si realiza las modificaciones posteriores a la colección original en AEM Assets, los cambios no se reflejarán en Brand Portal hasta que vuelva a publicar la colección. Esta característica garantiza que los cambios en curso no estén disponibles en Brand Portal. Solo los cambios aprobados publicados por un administrador están disponibles en Brand Portal.

>[!NOTE]
>
>Los fragmentos de contenido no se pueden publicar en Brand Portal. Por lo tanto, si selecciona fragmentos de contenido en AEM Author, la acción **Publicar en Brand Portal** no estará disponible.
>
>Si las colecciones que contienen fragmentos de contenido se publican de AEM Author a Brand Portal, todo el contenido de la carpeta, excepto los fragmentos de contenido, se replican en la interfaz de Brand Portal.

## Publicación de una colección en Brand Portal {#publish-a-collection-to-brand-portal}

1. En la interfaz de usuario de AEM Assets, haga clic en el logotipo de AEM.
1. En la página **Navegación**, vaya a **Recursos > Colecciones**.
1. En la consola Colecciones , seleccione la colección que desee publicar en Brand Portal.

   ![select_collection](assets/select_collection.png)

1. En la barra de herramientas, haga clic en **Publicar en Brand Portal**.
1. En el cuadro de diálogo de confirmación, haga clic en **Publicar**.
1. Cierre el mensaje de confirmación.
1. Inicie sesión en Brand Portal como administrador. La colección publicada está disponible en la consola Colecciones.

   ![colección publicada](assets/published_collection.png)

## Cancelar la publicación de colecciones {#unpublish-collections}

Puede cancelar la publicación de colecciones que publique desde AEM Assets en Brand Portal. Después de cancelar la publicación de la colección original, la copia ya no estará disponible para los usuarios de Brand Portal.

1. En la consola Colecciones de la instancia de AEM Assets y seleccione la colección que desea cancelar la publicación.

   ![select_collection-1](assets/select_collection-1.png)

1. En la barra de herramientas, haga clic en el icono **Quitar de Brand Portal** .
1. En el cuadro de diálogo, haga clic en **Cancelar publicación**.
1. Cierre el mensaje de confirmación. La colección se quita de la interfaz de Brand Portal.
