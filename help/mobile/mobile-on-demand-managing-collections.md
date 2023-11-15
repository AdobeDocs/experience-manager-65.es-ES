---
title: Administración de colecciones
description: Las colecciones representan un bloque bien definido lleno de contenido, como artículos o banners, que se adapta al tema de la portada. Siga esta página para obtener más información.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: 0b4aa1a4-449a-4882-8f7c-3ceea6ac7f83
source-git-commit: 69a249e63e2e6b96ba08f9846baa3e91d42b865f
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---

# Administración de colecciones{#managing-collections}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran una representación del lado del cliente basada en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Las acciones de Content Management son los componentes básicos que ayudan a crear y administrar contenido dentro de una aplicación. Las siguientes acciones se realizan en el contenido de la aplicación.

## Resumen de colecciones {#collections-overview}

Las colecciones representan un conjunto bien definido *cubo* se rellena con contenido, como artículos o titulares, que se adapta al tema de la portada.

>[!NOTE]
>
>Consulte los siguientes recursos en la Ayuda en línea para conocer los siguientes temas en las aplicaciones de AEM Mobile:
>
>* [Consideraciones de diseño](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [Administración de colecciones](https://helpx.adobe.com/digital-publishing-solution/help/creating-collections.html)
>

## Creación de una colección {#creating-a-collection}

El flujo de trabajo general para crear una colección es el siguiente:

1. Seleccionar **Móvil** desde la barra lateral.
1. En Mobile, elija su aplicación Mobile On-Demand en el catálogo.
1. Haga clic en la flecha hacia abajo situada en la esquina superior derecha de la **Administrar colecciones** mosaico.
1. Siga cada paso del asistente para seguir creando el nuevo artículo.
1. Cuando esté listo, haga clic en **Crear**.
1. El nuevo artículo aparecerá en la **Administrar colecciones** mosaico.

![chlimage_1-1](assets/chlimage_1-1.gif)

## Importación de una nueva colección {#importing-a-new-collection}

AEM El contenido existente de Mobile On-Demand se puede descargar (importar) de Mobile On-Demand a. Esto permite editar y ver el contenido local.

>[!NOTE]
>
>La importación no incluye imágenes.

Flujo de trabajo para importar una nueva colección

1. En Mobile, seleccione su aplicación Mobile On-Demand en el catálogo.
1. Haga clic en la flecha hacia abajo situada en la esquina superior derecha de la **Administrar colecciones** y seleccione Importar colecciones.
1. Clic **Importar colecciones** en el cuadro de diálogo y, a continuación, Cerrar.
1. Sus colecciones de Mobile On-Demand ahora aparecen en la **Administrar colecciones** mosaico.

>[!CAUTION]
>
>Primero debe asociar una conexión de Mobile On-Demand.

## Edición de una colección {#editing-a-collection}

AEM Utilice el editor integrado de arrastrar y soltar para agregar o cambiar un artículo de la lista de editores de la lista de editores de. Se pueden añadir o eliminar componentes como texto e imágenes. Se pueden insertar imágenes de los recursos DAM.

Flujo de trabajo para editar una colección:

1. En Mobile, elija su aplicación Mobile On-Demand en el catálogo.
1. AEM Seleccione un artículo de origen de la lista de artículos de la lista **Administrar colecciones** mosaico.
1. Haga clic en la colección resaltada de la vista de lista para abrirla en el editor de contenido.
1. Utilice el editor de contenido para arrastrar contenido de la colección (manuscritos, imágenes, texto, etc.).

### Visualización y edición de metadatos dentro de una colección {#viewing-and-editing-the-metadata-within-a-collection}

Las colecciones tienen numerosas propiedades como títulos, descripciones e imágenes. Esta acción se utiliza para ver y modificar dichas propiedades. De forma opcional, estos cambios se pueden cargar en Mobile On-Demand tras guardarlos.

Flujo de trabajo general para ver/editar una colección:

1. En Mobile, elija su aplicación Mobile On-Demand en el catálogo.
1. Elija una colección de la **Administrar colecciones** mosaico.

1. Seleccionar **Propiedades** de la barra de acciones.
1. Vea todos los metadatos disponibles para ese artículo.
1. Si lo desea, edite los metadatos y haga clic en **Guardar** cuando termine.
1. De forma opcional, cargue los cambios inmediatamente en Mobile On-Demand.

## Carga de una colección {#uploading-a-collection}

La acción de carga copia el contenido seleccionado y lo añade a un proyecto de Mobile On-Demand. El contenido existente de Mobile On-Demand se ha sustituido por la nueva versión.

Flujo de trabajo general para cargar una colección:

1. Desde **Móvil**, elija la aplicación Mobile On-Demand en el catálogo.
1. En el **Administrar colecciones** , seleccione un artículo para cargarlo en Mobile On-Demand.
1. Agregue más colecciones si es necesario desde la vista de lista.
1. Seleccionar **Cargar** en la barra de acciones y, a continuación, haga clic en Cargar en el cuadro de diálogo.
1. Las colecciones se han cargado a Mobile On-Demand.

## Eliminación de una colección {#deleting-a-collection}

AEM Esta operación elimina la colección seleccionada de Mobile On-Demand y, opcionalmente, de la instancia de la instancia de la aplicación local de la aplicación de la.

Flujo de trabajo general para eliminar una colección:

1. En Mobile, elija su aplicación Mobile On-Demand en el catálogo.
1. Seleccione el artículo que desea eliminar en la **Administrar colecciones** mosaico.
1. Asegúrese de que esté seleccionado en la lista; seleccione otros para eliminarlos según sea necesario.
1. Clic **Eliminar** de la barra de acciones.
1. AEM Seleccione si desea eliminar de la aplicación de Adobe y de Mobile On-Demand en la lista de dispositivos de la aplicación.
1. Haga clic en **Eliminar**.
1. Su colección se eliminará de la lista.

## Adición de contenido a colecciones {#adding-content-to-collections}

Las colecciones son esencialmente una categoría de contenido relacionado. Recopilan contenido, como artículos y titulares, en paquetes que definen la estructura de navegación de la aplicación. Las colecciones se pueden anidar.

>[!NOTE]
>
>El contenido debe cargarse en Mobile On-Demand para poder añadirse a una colección.

Las colecciones son esencialmente una categoría de contenido relacionado: reúnen contenido como artículos y titulares en paquetes que definen la estructura de navegación de la aplicación. Las colecciones se pueden anidar.

1. En Mobile, elija su aplicación Mobile On-Demand en el catálogo.
1. Seleccione un artículo cargado anteriormente (o titular/colección)
1. Elija Añadir a en la barra de acciones.
1. Seleccione una colección cargada anteriormente en el cuadro de diálogo.
1. Clic **Actualizar** para agregar contenido a la colección.

![chlimage_1-2](assets/chlimage_1-2.gif)

### Pasos siguientes {#the-next-steps}

Una vez que haya aprendido a administrar colecciones, consulte

* [Administración de titulares](/help/mobile/mobile-on-demand-managing-banners.md)
* [Administrar artículos](/help/mobile/mobile-on-demand-managing-articles.md)
* [Carga de recursos compartidos](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicación/cancelación de la publicación del contenido](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Vista previa con comprobación preliminar](/help/mobile/aem-mobile-manage-ondemand-services.md)
