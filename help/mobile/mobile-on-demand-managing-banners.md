---
title: Administración de titulares
seo-title: Managing Banners
description: Los banners representan vínculos promocionales gráficos. Siga esta página para obtener más información.
seo-description: Banners represent typically graphical promotional links. Follow this page to learn more.
uuid: 593fe2ef-84df-42e2-8a03-897fb67a896d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: fb1abaa0-9c02-4f20-aa7c-073def067452
exl-id: c65a24e6-3041-4774-aeed-8e188ea19b78
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 1%

---

# Administración de titulares{#managing-banners}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Las acciones de administración de contenido son los componentes básicos que ayudan a crear y administrar contenido dentro de una aplicación. Las siguientes acciones se realizan en el contenido de la aplicación.

## Información general sobre banners {#banners-overview}

Los banners representan vínculos promocionales gráficos.

>[!NOTE]
>
>Consulte los siguientes recursos en la Ayuda en línea para obtener más información sobre los siguientes temas en las aplicaciones de AEM Mobile:
>
>* [Consideraciones de diseño](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [Creación de titulares](https://helpx.adobe.com/digital-publishing-solution/help/creating-banners.html)
>


## Creación de un banner {#creating-a-banner}

El flujo de trabajo general para crear un artículo es el siguiente:

1. Select **Móvil** del carril lateral.
1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Haga clic en la flecha hacia abajo en la esquina superior derecha de la **Administrar titulares** mosaico.
1. Complete cada paso del asistente para seguir creando el nuevo banner.
1. Cuando esté listo, haga clic en **Crear**.
1. El nuevo banner aparece en la sección **Administrar titulares** mosaico.

![Chlimage_1-6](assets/chlimage_1-6.gif)

## Importación de un nuevo titular {#importing-a-new-banner}

El contenido existente de Mobile On-Demand se puede descargar (importar) de Mobile On-Demand a AEM. Esto permite la edición y visualización del contenido local.

>[!NOTE]
>
>La importación no incluye imágenes.

Flujo de trabajo para importar un nuevo artículo

1. En Móvil, elija su aplicación móvil bajo demanda en el catálogo.
1. Haga clic en la flecha hacia abajo en la esquina superior derecha de la **Administrar titulares** mosaico y seleccione Importar titulares.
1. Haga clic en **Importar titular** en el cuadro de diálogo y, a continuación, cierre.
1. Los artículos a la carta de Mobile ahora aparecen en la **Administrar titulares** mosaico.

>[!CAUTION]
>
>Primero debe asociar una conexión móvil bajo demanda.

## Edición de un titular {#editing-a-banner}

Utilice el editor integrado AEM arrastrar y soltar para añadir o cambiar un artículo. Se pueden añadir o eliminar componentes como texto e imágenes. Se pueden insertar imágenes de recursos DAM.

>[!CAUTION]
>
>En el editor solo se pueden abrir los titulares creados en AEM.

Flujo de trabajo para editar un artículo:

1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Seleccione un banner de origen AEM en el mosaico** Administrar banners**.
1. Haga clic en el banner resaltado de la vista de lista para abrirlo en el editor de contenido.
1. Utilice el editor de contenido para arrastrar el contenido del banner (manuscritos, imágenes, texto, etc.).

### Visualización y edición de los metadatos dentro de un banner {#viewing-and-editing-the-metadata-within-a-banner}

Los titulares tienen numerosas propiedades, como títulos, descripciones e imágenes. Esta acción se utiliza para ver y modificar estas propiedades. Opcionalmente, estos cambios se pueden cargar en Mobile On-Demand al guardarlos.

Flujo de trabajo general para ver o editar un artículo:

1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Elija un banner en la lista **Administrar titulares** mosaico.

1. Select **Propiedades** de la barra de acciones.
1. Ver todos los metadatos disponibles para ese artículo.
1. Edite los metadatos si lo desea y haga clic en **Guardar** cuando haya terminado.
1. De forma opcional, cargue los cambios inmediatamente en Mobile On-Demand.

## Carga de un banner {#uploading-a-banner}

La acción de carga copia el contenido seleccionado y lo agrega a un proyecto de Mobile On-Demand. El contenido de Mobile On-Demand ya existente se sustituye por la nueva versión.

Flujo de trabajo general para cargar un banner:

1. De **Móvil**, elija la aplicación móvil bajo demanda en el catálogo.
1. En el **Administrar titulares** , seleccione un banner para cargarlo en Mobile On-Demand.
1. Agregue más banners si es necesario desde la vista de lista.
1. Select **Cargar** en la barra de acciones, haga clic en Cargar en el cuadro de diálogo.
1. Los banners ahora se cargan en Mobile On-Demand.

![Chlimage_1-7](assets/chlimage_1-7.gif)

## Eliminación de un titular {#deleting-a-banner}

Esta operación elimina el banner seleccionado de Mobile On-Demand y, opcionalmente, de la instancia de AEM local.

Flujo de trabajo general para eliminar un banner:

1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Seleccione el banner que desea eliminar en la **Administrar titulares** mosaico.
1. Asegúrese de que está seleccionado en la lista (seleccione otras para eliminarlas según sea necesario).
1. Haga clic en **Eliminar** de la barra de acciones.
1. Compruebe si desea eliminar tanto de AEM como de Mobile On-Demand.
1. Haga clic en **Eliminar**.
1. El banner ahora se elimina de la lista.

### Pasos siguientes {#the-next-steps}

Una que obtenga información sobre la administración de banners, consulte

* [Administración de artículos](/help/mobile/mobile-on-demand-managing-articles.md)
* [Administración de colecciones](/help/mobile/mobile-on-demand-managing-collections.md)
* [Carga de recursos compartidos](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicación/cancelación de la publicación del contenido](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Vista previa con comprobación preliminar](/help/mobile/aem-mobile-manage-ondemand-services.md)
