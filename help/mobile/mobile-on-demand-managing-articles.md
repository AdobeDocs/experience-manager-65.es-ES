---
title: Administración de artículos
seo-title: Managing Articles
description: Siga esta página para obtener más información sobre la creación y administración de Artículos.
seo-description: Follow this page to learn about creating and managing Articles.
uuid: 72b86cd7-3016-41b6-a001-9dce4084e9db
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: b46058f9-4691-4fba-a656-0f8507875a79
exl-id: ea6c8aa3-f86e-4878-8550-fe1662f10696
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 1%

---

# Administración de artículos{#managing-articles}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Las acciones de administración de contenido son los componentes básicos que ayudan a crear y administrar artículos dentro de una aplicación. Las siguientes acciones se realizan en artículos dentro de la aplicación.

## Información general sobre artículos {#articles-overview}

Los artículos representan el texto basado en el arte para transmitir información.

>[!NOTE]
>
>Consulte los siguientes recursos en la Ayuda en línea para obtener más información sobre los siguientes temas en las aplicaciones de AEM Mobile:
>
>* [Consideraciones de diseño](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [Administración de artículos](https://helpx.adobe.com/digital-publishing-solution/help/creating-articles.html)
>


## Creación de un artículo {#creating-an-article}

El flujo de trabajo general para crear un artículo es el siguiente:

1. Select **Móvil** del carril lateral.
1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Haga clic en la flecha hacia abajo en la esquina superior derecha de la **Administrar artículos** mosaico.
1. Elija una plantilla de artículo y haga clic en **Siguiente**.
1. Complete cada paso del asistente para seguir creando el nuevo artículo.
1. Cuando esté listo, haga clic en **Crear**.
1. El nuevo artículo aparece en la sección **Administrar artículos** mosaico.

## Importación de un nuevo artículo {#importing-a-new-article}

El contenido existente de Mobile On-Demand se puede descargar (importar) de Mobile On-Demand a AEM. Esto permite la edición y visualización del contenido local.

>[!NOTE]
>
>La importación no incluye imágenes.

Flujo de trabajo para importar un nuevo artículo

1. En Móvil, elija su aplicación móvil bajo demanda en el catálogo.
1. Haga clic en la flecha hacia abajo en la esquina superior derecha de la **Administrar artículos** y seleccione Importar artículos.
1. Haga clic en **Importar artículos** en el cuadro de diálogo y, a continuación, cierre.
1. Los artículos a la carta de Mobile ahora aparecen en la **Administrar artículos** mosaico.

>[!CAUTION]
>
>Primero debe asociar una conexión móvil bajo demanda.

![Chlimage_1-3](assets/chlimage_1-3.gif)

## Edición de un artículo {#editing-an-article}

Utilice el editor integrado AEM arrastrar y soltar para añadir o cambiar un artículo. Se pueden añadir o eliminar componentes como texto e imágenes. Se pueden insertar imágenes de recursos DAM.

>[!CAUTION]
>
>En el editor solo se pueden abrir los artículos creados en AEM.

Flujo de trabajo para editar un artículo:

1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Seleccione un artículo AEM de origen en el **Administrar artículos** mosaico.
1. Haga clic en el artículo resaltado en la vista de lista para abrirlo en el editor de contenido.
1. Utilice el editor de contenido para arrastrar el contenido del artículo (manuscritos, imágenes, texto, etc.).

### Visualización y edición de los metadatos de un artículo {#viewing-and-editing-the-metadata-within-an-article}

El contenido, como artículos, banners, etc., tiene numerosas propiedades, como títulos, descripciones e imágenes. Esta acción se utiliza para ver y modificar estas propiedades. Opcionalmente, estos cambios se pueden cargar en Mobile On-Demand al guardarlos.

Flujo de trabajo general para ver o editar un artículo:

1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Elija un artículo de la lista **Administrar artículos** mosaico.

1. Select **Ver propiedades** de la barra de acciones.
1. Ver todos los metadatos disponibles para ese artículo.
1. Edite los metadatos si lo desea y haga clic en **Guardar** cuando haya terminado.
1. De forma opcional, cargue los cambios inmediatamente en Mobile On-Demand.

## Carga de un artículo {#uploading-an-article}

La acción de carga copia el contenido seleccionado y lo agrega a un proyecto de Mobile On-Demand. El contenido de Mobile On-Demand ya existente se sustituye por la nueva versión.

Flujo de trabajo general para cargar un artículo:

1. De **Móvil**, elija la aplicación móvil bajo demanda en el catálogo.
1. En el **Administrar artículos** , seleccione un artículo para cargarlo en Mobile On-Demand.
1. Agregue más artículos si es necesario desde la vista de lista.
1. Select **Cargar** en la barra de acciones, haga clic en Cargar en el cuadro de diálogo.
1. Los artículos ahora se cargan en Mobile On-Demand.

![Chlimage_1-4](assets/chlimage_1-4.gif)

## Eliminación de un artículo {#deleting-an-article}

Esta operación elimina el contenido seleccionado de Mobile On-Demand y, opcionalmente, de la instancia de AEM local.

Flujo de trabajo general para eliminar un artículo:

1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Seleccione el artículo que desea eliminar en el **Administrar artículos** mosaico.
1. Asegúrese de que está seleccionado en la lista (seleccione otras para eliminarlas según sea necesario).
1. Haga clic en **Eliminar** de la barra de acciones.
1. Compruebe si desea eliminar tanto de AEM como de Mobile On-Demand.
1. Haga clic en **Eliminar**.
1. El artículo se ha eliminado de la lista.

![Chlimage_1-5](assets/chlimage_1-5.gif)

### Pasos siguientes {#the-next-steps}

Una que obtenga información sobre la administración de artículos, consulte

* [Administración de titulares](/help/mobile/mobile-on-demand-managing-banners.md)
* [Administración de colecciones](/help/mobile/mobile-on-demand-managing-collections.md)
* [Carga de recursos compartidos](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicación/cancelación de la publicación del contenido](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Vista previa con comprobación preliminar](/help/mobile/aem-mobile-manage-ondemand-services.md)
