---
title: Administración de colecciones
seo-title: Administración de colecciones
description: Las colecciones representan un bloque bien definido con contenido como artículos o pancartas que se ajustan al tema de la portada. Siga esta página para obtener más información.
seo-description: Las colecciones representan un bloque bien definido con contenido como artículos o pancartas que se ajustan al tema de la portada. Siga esta página para obtener más información.
uuid: 1d2e9769-d2cc-4d43-a428-e962a51eb5d0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: 64c6d198-983f-4a52-9c83-560206363868
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Administración de colecciones{#managing-collections}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Las acciones de Administración de contenido son los componentes básicos que ayudan a crear y administrar contenido dentro de una aplicación. Las siguientes acciones se realizan en el contenido de la aplicación.

## Información general de colecciones {#collections-overview}

Las colecciones representan un *bloque* bien definido con contenido como artículos o pancartas que se ajustan al tema de la portada.

>[!NOTE]
>
>Consulte los siguientes recursos en la Ayuda en línea para conocer los siguientes temas en las aplicaciones de AEM Mobile:
>
>* [Consideraciones de diseño](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
   >
   >
* [Administración de colecciones](https://helpx.adobe.com/digital-publishing-solution/help/creating-collections.html)
>



## Creación de una colección {#creating-a-collection}

El flujo de trabajo general para crear una colección es el siguiente:

1. Seleccione **Móvil** en el carril lateral.
1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Haga clic en la flecha hacia abajo en la esquina superior derecha del mosaico **Administrar colecciones** .
1. Siga todos los pasos del asistente para seguir creando el nuevo artículo.
1. Cuando esté listo, haga clic en **Crear**.
1. El nuevo artículo aparece en el mosaico **Administrar colecciones** .

![chlimage_1-1](assets/chlimage_1-1.gif)

## Importación de una nueva colección {#importing-a-new-collection}

El contenido de Mobile On-Demand existente se puede descargar (importar) de Mobile On-Demand a AEM. Esto permite la edición y visualización de contenido local.

>[!NOTE]
>
>La importación no incluye imágenes.

Flujo de trabajo para importar una nueva colección

1. En Mobile, seleccione su aplicación móvil bajo demanda en el catálogo.
1. Haga clic en la flecha hacia abajo en la esquina superior derecha del mosaico **Administrar colecciones** y seleccione Importar colecciones.
1. Haga clic en **Importar colecciones** en el cuadro de diálogo y, a continuación, en Cerrar.
1. Las colecciones bajo demanda de Mobile aparecen ahora en el mosaico **Administrar colecciones** .

>[!CAUTION]
>
>Primero debe asociar una conexión móvil bajo demanda.

## Edición de una colección {#editing-a-collection}

Utilice el editor de arrastrar y soltar integrado de AEM para añadir o cambiar un artículo. Se pueden añadir o eliminar componentes como texto e imágenes. Se pueden insertar imágenes de Recursos DAM.

Flujo de trabajo para editar una colección:

1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Seleccione un artículo de origen de AEM en el mosaico **Administrar colecciones** .
1. Haga clic en la colección resaltada en la vista de lista para abrirla en el editor de contenido.
1. Utilice el editor de contenido para arrastrar el contenido de la colección (manuscritos, imágenes, texto, etc.).

### Visualización y edición de metadatos en una colección {#viewing-and-editing-the-metadata-within-a-collection}

Las colecciones tienen numerosas propiedades, como títulos, descripciones e imágenes. Esta acción se utiliza para ver y modificar dichas propiedades. Opcionalmente, estos cambios se pueden cargar a Mobile On-Demand al guardarlos.

Flujo de trabajo general para ver/editar una colección:

1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Elija una colección en el mosaico **Administrar colecciones** .

1. Seleccione **Propiedades** en la barra de acciones.
1. Ver todos los metadatos disponibles para ese artículo.
1. Edite los metadatos si lo desea y haga clic en **Guardar** cuando termine.
1. De forma opcional, cargue los cambios inmediatamente en Mobile On-Demand.

## Carga de una colección {#uploading-a-collection}

La acción de carga copia el contenido seleccionado y lo agrega a un proyecto de Mobile On-Demand. El contenido ya existente de Mobile On-Demand se sustituye por la nueva versión.

Flujo de trabajo general para cargar una colección:

1. En **Mobile**, elija la aplicación móvil bajo demanda en el catálogo.
1. En el mosaico **Administrar colecciones** , seleccione un artículo para cargarlo en Mobile On-Demand.
1. Agregue más colecciones si es necesario desde la vista de lista.
1. Seleccione **Cargar** en la barra de acciones y, a continuación, haga clic en Cargar en el cuadro de diálogo.
1. Las colecciones se cargan ahora en Mobile On-Demand.

## Eliminación de una colección {#deleting-a-collection}

Esta operación elimina la colección seleccionada de Mobile On-Demand y, opcionalmente, de la instancia local de AEM.

Flujo de trabajo general para eliminar una colección:

1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Seleccione el artículo que desea eliminar en el mosaico **Administrar colecciones** .
1. Asegúrese de que esté seleccionado en la lista (seleccione otros para eliminar según sea necesario).
1. Click **Delete** from the action bar.
1. Compruebe si desea eliminar de AEM y Mobile On-Demand.
1. Haga clic en **Eliminar**.
1. La colección se ha eliminado de la lista.

## Adición de contenido a colecciones {#adding-content-to-collections}

Las colecciones son esencialmente una categoría de contenido relacionado.  Recopilan contenido como artículos y pancartas en paquetes que definen la estructura de navegación de la aplicación. Las colecciones se pueden anidar.

>[!NOTE]
>
>El contenido debe cargarse en Mobile On-Demand para poder agregarlo a una colección.

Las colecciones son esencialmente una categoría de contenido relacionado: Recopilan contenido como artículos y pancartas en paquetes que definen la estructura de navegación de la aplicación. Las colecciones se pueden anidar.

1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Seleccione un artículo cargado anteriormente (o pancarta/colección)
1. Elija Agregar a en la barra de acciones.
1. Seleccione una colección cargada anteriormente en el cuadro de diálogo.
1. Haga clic en **Actualizar** para añadir contenido a la colección.

![chlimage_1-2](assets/chlimage_1-2.gif)

### Pasos siguientes {#the-next-steps}

Una que aprenda a administrar colecciones, consulte

* [Administración de pancartas](/help/mobile/mobile-on-demand-managing-banners.md)
* [Administración de artículos](/help/mobile/mobile-on-demand-managing-articles.md)
* [Carga de recursos compartidos](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicación/Cancelación de la publicación del contenido](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Vista previa con verificación previa](/help/mobile/aem-mobile-manage-ondemand-services.md)
