---
title: Administración de colecciones
seo-title: Managing Collections
description: Las colecciones representan un grupo bien definido y lleno de contenido como artículos o banners que se ajustan al tema de la portada. Siga esta página para obtener más información.
seo-description: Collections represent a well defined bucket filled with content such as articles or banners that suits the cover's theme. Follow this page to learn more.
uuid: 1d2e9769-d2cc-4d43-a428-e962a51eb5d0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: 64c6d198-983f-4a52-9c83-560206363868
exl-id: 0b4aa1a4-449a-4882-8f7c-3ceea6ac7f83
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 1%

---

# Administración de colecciones{#managing-collections}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Las acciones de administración de contenido son los componentes básicos que ayudan a crear y administrar contenido dentro de una aplicación. Las siguientes acciones se realizan en el contenido de la aplicación.

## Información general de colecciones {#collections-overview}

Las colecciones representan una *depósito* relleno de contenido como artículos o banners que se adapten al tema de la portada.

>[!NOTE]
>
>Consulte los siguientes recursos en la Ayuda en línea para obtener más información sobre los siguientes temas en las aplicaciones de AEM Mobile:
>
>* [Consideraciones de diseño](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [Administración de colecciones](https://helpx.adobe.com/digital-publishing-solution/help/creating-collections.html)
>


## Creación de una colección {#creating-a-collection}

El flujo de trabajo general para crear una colección es el siguiente:

1. Select **Móvil** del carril lateral.
1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Haga clic en la flecha hacia abajo en la esquina superior derecha de la **Administrar colecciones** mosaico.
1. Complete cada paso del asistente para seguir creando el nuevo artículo.
1. Cuando esté listo, haga clic en **Crear**.
1. El nuevo artículo aparece en la sección **Administrar colecciones** mosaico.

![Chlimage_1-1](assets/chlimage_1-1.gif)

## Importación de una nueva colección {#importing-a-new-collection}

El contenido existente de Mobile On-Demand se puede descargar (importar) de Mobile On-Demand a AEM. Esto permite la edición y visualización del contenido local.

>[!NOTE]
>
>La importación no incluye imágenes.

Flujo de trabajo para importar una nueva colección

1. En Móvil, elija su aplicación móvil bajo demanda en el catálogo.
1. Haga clic en la flecha hacia abajo en la esquina superior derecha de la **Administrar colecciones** y seleccione Importar colecciones.
1. Haga clic en **Importar colecciones** en el cuadro de diálogo y, a continuación, cierre.
1. Las colecciones móviles bajo demanda ahora aparecen en la sección **Administrar colecciones** mosaico.

>[!CAUTION]
>
>Primero debe asociar una conexión móvil bajo demanda.

## Edición de una colección {#editing-a-collection}

Utilice el editor integrado AEM arrastrar y soltar para añadir o cambiar un artículo. Se pueden añadir o eliminar componentes como texto e imágenes. Se pueden insertar imágenes de recursos DAM.

Flujo de trabajo para editar una colección:

1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Seleccione un artículo AEM de origen en el **Administrar colecciones** mosaico.
1. Haga clic en la colección resaltada en la vista de lista para abrirla en el editor de contenido.
1. Utilice el editor de contenido para arrastrar contenido de recopilación (manuscritos, imágenes, texto, etc.).

### Visualización y edición de los metadatos de una colección {#viewing-and-editing-the-metadata-within-a-collection}

Las colecciones tienen numerosas propiedades, como títulos, descripciones e imágenes. Esta acción se utiliza para ver y modificar estas propiedades. Opcionalmente, estos cambios se pueden cargar en Mobile On-Demand al guardarlos.

Flujo de trabajo general para ver o editar una colección:

1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Elija una colección de **Administrar colecciones** mosaico.

1. Select **Propiedades** de la barra de acciones.
1. Ver todos los metadatos disponibles para ese artículo.
1. Edite los metadatos si lo desea y haga clic en **Guardar** cuando haya terminado.
1. De forma opcional, cargue los cambios inmediatamente en Mobile On-Demand.

## Carga de una colección {#uploading-a-collection}

La acción de carga copia el contenido seleccionado y lo agrega a un proyecto de Mobile On-Demand. El contenido de Mobile On-Demand ya existente se sustituye por la nueva versión.

Flujo de trabajo general para cargar una colección:

1. De **Móvil**, elija la aplicación móvil bajo demanda en el catálogo.
1. En el **Administrar colecciones** , seleccione un artículo para cargarlo en Mobile On-Demand.
1. Agregue más colecciones si es necesario desde la vista de lista.
1. Select **Cargar** en la barra de acciones, haga clic en Cargar en el cuadro de diálogo.
1. Sus colecciones ahora se cargan en Mobile On-Demand.

## Eliminación de una colección {#deleting-a-collection}

Esta operación elimina la colección seleccionada de Mobile On-Demand y, opcionalmente, de la instancia de AEM local.

Flujo de trabajo general para eliminar una colección:

1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Seleccione el artículo que desea eliminar en el **Administrar colecciones** mosaico.
1. Asegúrese de que está seleccionado en la lista (seleccione otras para eliminarlas según sea necesario).
1. Haga clic en **Eliminar** de la barra de acciones.
1. Compruebe si desea eliminar tanto de AEM como de Mobile On-Demand.
1. Haga clic en **Eliminar**.
1. La colección se ha eliminado de la lista.

## Adición de contenido a colecciones {#adding-content-to-collections}

Las colecciones son esencialmente una categoría de contenido relacionado. Recopilan contenido, como artículos o banners, en paquetes que definen la estructura de navegación de la aplicación. Las colecciones se pueden anidar.

>[!NOTE]
>
>El contenido debe cargarse en Mobile On-Demand para poder agregarlo a una colección.

Las colecciones son esencialmente una categoría de contenido relacionado: Recopilan contenido, como artículos o banners, en paquetes que definen la estructura de navegación de la aplicación. Las colecciones se pueden anidar.

1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Seleccionar un artículo cargado previamente (o titular/colección)
1. Elija Agregar a en la barra de acciones.
1. Seleccione una colección cargada previamente del cuadro de diálogo.
1. Haga clic en **Actualizar** para añadir contenido a la colección.

![Chlimage_1-2](assets/chlimage_1-2.gif)

### Pasos siguientes {#the-next-steps}

Una que obtenga información sobre la administración de colecciones, consulte

* [Administración de titulares](/help/mobile/mobile-on-demand-managing-banners.md)
* [Administración de artículos](/help/mobile/mobile-on-demand-managing-articles.md)
* [Carga de recursos compartidos](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicación/cancelación de la publicación del contenido](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Vista previa con comprobación preliminar](/help/mobile/aem-mobile-manage-ondemand-services.md)
