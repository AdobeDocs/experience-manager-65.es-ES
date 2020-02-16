---
title: Administración de artículos
seo-title: Administración de artículos
description: Siga esta página para conocer la creación y administración de artículos.
seo-description: Siga esta página para conocer la creación y administración de artículos.
uuid: 72b86cd7-3016-41b6-a001-9dce4084e9db
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: b46058f9-4691-4fba-a656-0f8507875a79
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Administración de artículos{#managing-articles}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Las acciones de Administración de contenido son los componentes básicos que ayudan a crear y administrar artículos dentro de una aplicación. Las siguientes acciones se realizan en artículos dentro de la aplicación.

## Información general de artículos {#articles-overview}

Los artículos representan el texto basado en el arte para transmitir información.

>[!NOTE]
>
>Consulte los siguientes recursos en la Ayuda en línea para conocer los siguientes temas en las aplicaciones de AEM Mobile:
>
>* [Consideraciones de diseño](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
   >
   >
* [Administración de artículos](https://helpx.adobe.com/digital-publishing-solution/help/creating-articles.html)
>



## Creación de un artículo {#creating-an-article}

El flujo de trabajo general para crear un artículo es el siguiente:

1. Seleccione **Móvil** en el carril lateral.
1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Haga clic en la flecha hacia abajo en la esquina superior derecha del mosaico **Administrar artículos** .
1. Elija una plantilla de artículo y haga clic en **Siguiente**.
1. Siga todos los pasos del asistente para seguir creando el nuevo artículo.
1. Cuando esté listo, haga clic en **Crear**.
1. El nuevo artículo aparece en el mosaico **Administrar artículos** .

## Importación de un nuevo artículo {#importing-a-new-article}

El contenido de Mobile On-Demand existente se puede descargar (importar) de Mobile On-Demand a AEM. Esto permite la edición y visualización de contenido local.

>[!NOTE]
>
>La importación no incluye imágenes.

Flujo de trabajo para importar un nuevo artículo

1. En Mobile, seleccione su aplicación móvil bajo demanda en el catálogo.
1. Haga clic en la flecha hacia abajo en la esquina superior derecha del mosaico **Administrar artículos** y seleccione Importar artículos.
1. Haga clic en **Importar artículos** en el cuadro de diálogo y, a continuación, en Cerrar.
1. Los artículos a petición de Mobile aparecen ahora en el mosaico **Administrar artículos** .

>[!CAUTION]
>
>Primero debe asociar una conexión móvil bajo demanda.

![climage_1-3](assets/chlimage_1-3.gif)

## Edición de un artículo {#editing-an-article}

Utilice el editor de arrastrar y soltar integrado de AEM para añadir o cambiar un artículo. Se pueden añadir o eliminar componentes como texto e imágenes. Se pueden insertar imágenes de Recursos DAM.

>[!CAUTION]
>
>Solo los artículos creados en AEM se pueden abrir en el editor.

Flujo de trabajo para editar un artículo:

1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Seleccione un artículo de origen AEM en el mosaico **Administrar artículos** .
1. Haga clic en el artículo resaltado en la vista de lista para abrirlo en el editor de contenido.
1. Utilice el editor de contenido para arrastrar el contenido del artículo (manuscritos, imágenes, texto, etc.).

### Visualización y edición de metadatos en un artículo {#viewing-and-editing-the-metadata-within-an-article}

Contenido como artículos, pancartas, etc. tiene numerosas propiedades, como títulos, descripciones e imágenes. Esta acción se utiliza para ver y modificar dichas propiedades. Opcionalmente, estos cambios se pueden cargar a Mobile On-Demand al guardarlos.

Flujo de trabajo general para ver/editar un artículo:

1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Elija un artículo en el mosaico **Administrar artículos** .

1. Seleccione **Ver propiedades** en la barra de acciones.
1. Ver todos los metadatos disponibles para ese artículo.
1. Edite los metadatos si lo desea y haga clic en **Guardar** cuando termine.
1. De forma opcional, cargue los cambios inmediatamente en Mobile On-Demand.

## Carga de un artículo {#uploading-an-article}

La acción de carga copia el contenido seleccionado y lo agrega a un proyecto de Mobile On-Demand. El contenido ya existente de Mobile On-Demand se sustituye por la nueva versión.

Flujo de trabajo general para cargar un artículo:

1. En **Mobile**, elija la aplicación móvil bajo demanda en el catálogo.
1. En el mosaico **Administrar artículos** , seleccione un artículo para cargarlo en Mobile On-Demand.
1. Agregue más artículos si es necesario desde la vista de lista.
1. Seleccione **Cargar** en la barra de acciones y, a continuación, haga clic en Cargar en el cuadro de diálogo.
1. Los artículos ahora se cargan en Mobile On-Demand.

![climage_1-4](assets/chlimage_1-4.gif)

## Eliminación de un artículo {#deleting-an-article}

Esta operación elimina el contenido seleccionado de Mobile On-Demand y, opcionalmente, de la instancia local de AEM.

Flujo de trabajo general para eliminar un artículo:

1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Seleccione el artículo que desea eliminar en el mosaico **Administrar artículos** .
1. Asegúrese de que esté seleccionado en la lista (seleccione otros para eliminar según sea necesario).
1. Click **Delete** from the action bar.
1. Compruebe si desea eliminar de AEM y Mobile On-Demand.
1. Haga clic en **Eliminar**.
1. El artículo se ha eliminado de la lista.

![climage_1-5](assets/chlimage_1-5.gif)

### Pasos siguientes {#the-next-steps}

Una que aprenda a administrar artículos, consulte

* [Administración de pancartas](/help/mobile/mobile-on-demand-managing-banners.md)
* [Administración de colecciones](/help/mobile/mobile-on-demand-managing-collections.md)
* [Carga de recursos compartidos](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicación/Cancelación de la publicación del contenido](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Vista previa con verificación previa](/help/mobile/aem-mobile-manage-ondemand-services.md)
