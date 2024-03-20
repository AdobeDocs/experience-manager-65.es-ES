---
title: Publicación de colecciones en Brand Portal
description: Obtenga información sobre cómo publicar y cancelar la publicación de colecciones en Brand Portal.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
docset: aem65
feature: Brand Portal
role: User
exl-id: 8f426012-d9ec-418e-8ab6-78e4aeff7538
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 30%

---

# Publicación de colecciones en Brand Portal {#publish-collections-to-brand-portal}

Como administrador de recursos de Adobe Experience Manager AEM (), puede publicar colecciones en la instancia de AEM Assets Brand Portal de su organización. Sin embargo, primero debe integrar AEM Assets con Brand Portal. Para obtener más información, consulte [Configurar AEM Assets con Brand Portal](/help/assets/configure-aem-assets-with-brand-portal.md).

Si realiza las modificaciones posteriores a la colección original en AEM Assets, los cambios no se reflejarán en Brand Portal hasta que vuelva a publicar la colección. Esta característica garantiza que los cambios en curso no estén disponibles en Brand Portal. Solo los cambios aprobados publicados por un administrador están disponibles en Brand Portal.

>[!NOTE]
>
>Los fragmentos de contenido no se pueden publicar en Brand Portal. AEM Por lo tanto, si selecciona fragmentos de contenido en Autor de la, **Publicar en Brand Portal** La acción no está disponible.
>
>AEM Si las colecciones que contienen fragmentos de contenido se publican desde el Autor de la publicación a Brand Portal, todo el contenido de la carpeta, excepto los fragmentos de contenido, se replicará en la interfaz de Brand Portal.

## Publicación de una colección en Brand Portal {#publish-a-collection-to-brand-portal}

1. En la interfaz de usuario de AEM Assets, haga clic en el logotipo de AEM.
1. Desde **Navegación** página, vaya a **Recursos > Colecciones**.
1. En la consola Colecciones, seleccione la colección que desea publicar en Brand Portal.

   ![select_collection](assets/select_collection.png)

1. En la barra de herramientas, haga clic en **Publicar en Brand Portal**.
1. En el cuadro de diálogo de confirmación, haga clic en **Publicar**.
1. Cierre el mensaje de confirmación.
1. Inicie sesión en Brand Portal como administrador. La colección publicada está disponible en la consola Colecciones.

   ![colección publicada](assets/published_collection.png)

## Cancelar publicación de colecciones {#unpublish-collections}

Puede cancelar la publicación de colecciones que publique desde AEM Assets en Brand Portal. Después de cancelar la publicación de la colección original, su copia ya no estará disponible para los usuarios de Brand Portal.

1. En la consola Colecciones de la instancia de AEM Assets y seleccione la colección que desea cancelar la publicación.

   ![select_collection-1](assets/select_collection-1.png)

1. En la barra de herramientas, haga clic en el icono **Quitar de Brand Portal** .
1. En el cuadro de diálogo, haga clic en **Cancelar publicación**.
1. Cierre el mensaje de confirmación. La colección se quita de la interfaz de Brand Portal.
