---
title: Administrar artículos
description: Siga esta página para obtener más información sobre la creación y administración de artículos.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: ea6c8aa3-f86e-4878-8550-fe1662f10696
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 1%

---

# Administrar artículos{#managing-articles}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran una representación del lado del cliente basada en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Las acciones de Content Management son los componentes básicos que ayudan a crear y administrar artículos dentro de una aplicación. Las siguientes acciones se realizan en artículos dentro de la aplicación.

## Resumen de artículos {#articles-overview}

Los artículos representan el texto basado junto con el arte para transmitir información.

>[!NOTE]
>
>Consulte los siguientes recursos en la Ayuda en línea para conocer los siguientes temas en las aplicaciones de AEM Mobile:
>
>* [Consideraciones de diseño](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [Administrar artículos](https://helpx.adobe.com/digital-publishing-solution/help/creating-articles.html)
>

## Creación de un artículo {#creating-an-article}

El flujo de trabajo general para crear un artículo es el siguiente:

1. Seleccionar **Móvil** desde la barra lateral.
1. En Mobile, elija su aplicación Mobile On-Demand en el catálogo.
1. Haga clic en la flecha hacia abajo situada en la esquina superior derecha de la **Administrar artículos** mosaico.
1. Elija una plantilla de artículo y haga clic en **Siguiente**.
1. Siga cada paso del asistente para seguir creando el nuevo artículo.
1. Cuando esté listo, haga clic en **Crear**.
1. El nuevo artículo aparecerá en la **Administrar artículos** mosaico.

## Importación de un nuevo artículo {#importing-a-new-article}

AEM El contenido existente de Mobile On-Demand se puede descargar (importar) de Mobile On-Demand a. Esto permite editar y ver el contenido local.

>[!NOTE]
>
>La importación no incluye imágenes.

Flujo de trabajo para importar un nuevo artículo

1. En Mobile, seleccione su aplicación Mobile On-Demand en el catálogo.
1. Haga clic en la flecha hacia abajo situada en la esquina superior derecha de la **Administrar artículos** y seleccione Importar artículos.
1. Clic **Importar artículos** en el cuadro de diálogo y, a continuación, Cerrar.
1. Sus artículos de Mobile On-Demand ahora aparecen en la **Administrar artículos** mosaico.

>[!CAUTION]
>
>Primero debe asociar una conexión de Mobile On-Demand.

![chlimage_1-3](assets/chlimage_1-3.gif)

## Edición de un artículo {#editing-an-article}

AEM Utilice el editor integrado de arrastrar y soltar para agregar o cambiar un artículo de la lista de editores de la lista de editores de. Se pueden añadir o eliminar componentes como texto e imágenes. Se pueden insertar imágenes de los recursos DAM.

>[!CAUTION]
>
>AEM En el editor solo se pueden abrir los artículos creados en la.

Flujo de trabajo para editar un artículo:

1. En Mobile, elija su aplicación Mobile On-Demand en el catálogo.
1. AEM Seleccione un artículo de origen de la lista de artículos de la lista **Administrar artículos** mosaico.
1. Haga clic en el artículo resaltado de la vista de lista para abrirlo en el editor de contenido.
1. Utilice el editor de contenido para arrastrar contenido de artículo (manuscritos, imágenes, texto, etc.).

### Visualización y edición de los metadatos de un artículo {#viewing-and-editing-the-metadata-within-an-article}

Contenido como artículos, banners, etc. tiene numerosas propiedades como títulos, descripciones e imágenes. Esta acción se utiliza para ver y modificar dichas propiedades. De forma opcional, estos cambios se pueden cargar en Mobile On-Demand tras guardarlos.

Flujo de trabajo general para ver o editar un artículo:

1. En Mobile, elija su aplicación Mobile On-Demand en el catálogo.
1. Elija un artículo de la **Administrar artículos** mosaico.

1. Seleccionar **Ver propiedades** de la barra de acciones.
1. Vea todos los metadatos disponibles para ese artículo.
1. Si lo desea, edite los metadatos y haga clic en **Guardar** cuando termine.
1. De forma opcional, cargue los cambios inmediatamente en Mobile On-Demand.

## Cargar un artículo {#uploading-an-article}

La acción de carga copia el contenido seleccionado y lo añade a un proyecto de Mobile On-Demand. El contenido existente de Mobile On-Demand se ha sustituido por la nueva versión.

Flujo de trabajo general para cargar un artículo:

1. Desde **Móvil**, elija la aplicación Mobile On-Demand en el catálogo.
1. En el **Administrar artículos** , seleccione un artículo para cargarlo en Mobile On-Demand.
1. Agregue más artículos si es necesario desde la vista de lista.
1. Seleccionar **Cargar** en la barra de acciones y, a continuación, haga clic en Cargar en el cuadro de diálogo.
1. Sus artículos se han cargado a Mobile On-Demand.

![chlimage_1-4](assets/chlimage_1-4.gif)

## Eliminación de un artículo {#deleting-an-article}

AEM Esta operación elimina el contenido seleccionado de Mobile On-Demand y, opcionalmente, de la instancia local de la instancia de la.

Flujo de trabajo general para eliminar un artículo:

1. En Mobile, elija su aplicación Mobile On-Demand en el catálogo.
1. Seleccione el artículo que desea eliminar en la **Administrar artículos** mosaico.
1. Asegúrese de que esté seleccionado en la lista (seleccione otros para eliminarlos según sea necesario).
1. Clic **Eliminar** de la barra de acciones.
1. AEM Seleccione si desea eliminar de la aplicación de Adobe y de Mobile On-Demand en la lista de dispositivos de la aplicación.
1. Haga clic en **Eliminar**.
1. El artículo se eliminará de la lista.

![chlimage_1-5](assets/chlimage_1-5.gif)

### Pasos siguientes {#the-next-steps}

Una vez que aprenda a administrar artículos, consulte

* [Administración de titulares](/help/mobile/mobile-on-demand-managing-banners.md)
* [Administración de colecciones](/help/mobile/mobile-on-demand-managing-collections.md)
* [Carga de recursos compartidos](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicación/cancelación de la publicación del contenido](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Vista previa con comprobación preliminar](/help/mobile/aem-mobile-manage-ondemand-services.md)
