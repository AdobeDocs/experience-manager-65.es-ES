---
title: Administración de pancartas
seo-title: Administración de pancartas
description: Las pancartas representan vínculos promocionales gráficos. Siga esta página para obtener más información.
seo-description: Las pancartas representan vínculos promocionales gráficos. Siga esta página para obtener más información.
uuid: 593fe2ef-84df-42e2-8a03-897fb67a896d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: fb1abaa0-9c02-4f20-aa7c-073def067452
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Administración de pancartas{#managing-banners}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Las acciones de Administración de contenido son los componentes básicos que ayudan a crear y administrar contenido dentro de una aplicación. Las siguientes acciones se realizan en el contenido de la aplicación.

## Información general de pancartas {#banners-overview}

Las pancartas representan vínculos promocionales gráficos.

>[!NOTE]
>
>Consulte los siguientes recursos en la Ayuda en línea para conocer los siguientes temas en las aplicaciones de AEM Mobile:
>
>* [Consideraciones de diseño](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
   >
   >
* [Creación de pancartas](https://helpx.adobe.com/digital-publishing-solution/help/creating-banners.html)
>



## Creación de una pancarta {#creating-a-banner}

El flujo de trabajo general para crear un artículo es el siguiente:

1. Seleccione **Móvil** en el carril lateral.
1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Haga clic en la flecha hacia abajo en la esquina superior derecha del mosaico **Administrar pancartas** .
1. Siga todos los pasos del asistente para seguir creando la nueva pancarta.
1. Cuando esté listo, haga clic en **Crear**.
1. La nueva pancarta aparece en el mosaico **Administrar pancartas** .

![climage_1-6](assets/chlimage_1-6.gif)

## Importación de letreros nuevos {#importing-a-new-banner}

El contenido de Mobile On-Demand existente se puede descargar (importar) de Mobile On-Demand a AEM. Esto permite la edición y visualización de contenido local.

>[!NOTE]
>
>La importación no incluye imágenes.

Flujo de trabajo para importar un nuevo artículo

1. En Mobile, seleccione su aplicación móvil bajo demanda en el catálogo.
1. Haga clic en la flecha hacia abajo en la esquina superior derecha del mosaico **Administrar pancartas** y seleccione Importar pancartas.
1. Haga clic en **Importar pancarta** en el cuadro de diálogo y, a continuación, en Cerrar.
1. Los artículos a petición de Mobile aparecen ahora en el mosaico **Administrar pancartas** .

>[!CAUTION]
>
>Primero debe asociar una conexión móvil bajo demanda.

## Edición de letreros {#editing-a-banner}

Utilice el editor de arrastrar y soltar integrado de AEM para añadir o cambiar un artículo. Se pueden añadir o eliminar componentes como texto e imágenes. Se pueden insertar imágenes de Recursos DAM.

>[!CAUTION]
>
>En el editor solo se pueden abrir las pancartas creadas en AEM.

Flujo de trabajo para editar un artículo:

1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Seleccione un letrero de origen AEM en el mosaico** Administrar pancartas**.
1. Haga clic en el letrero resaltado en la vista de lista para abrirlo en el editor de contenido.
1. Utilice el editor de contenido para arrastrar el contenido de la pancarta (manuscritos, imágenes, texto, etc.).

### Visualización y edición de metadatos en un letrero {#viewing-and-editing-the-metadata-within-a-banner}

Los letreros tienen numerosas propiedades, como títulos, descripciones e imágenes. Esta acción se utiliza para ver y modificar dichas propiedades. Opcionalmente, estos cambios se pueden cargar a Mobile On-Demand al guardarlos.

Flujo de trabajo general para ver/editar un artículo:

1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Elija una pancarta en el mosaico **Administrar pancartas** .

1. Seleccione **Propiedades** en la barra de acciones.
1. Ver todos los metadatos disponibles para ese artículo.
1. Edite los metadatos si lo desea y haga clic en **Guardar** cuando termine.
1. De forma opcional, cargue los cambios inmediatamente en Mobile On-Demand.

## Carga de letreros {#uploading-a-banner}

La acción de carga copia el contenido seleccionado y lo agrega a un proyecto de Mobile On-Demand. El contenido ya existente de Mobile On-Demand se sustituye por la nueva versión.

Flujo de trabajo general para cargar una pancarta:

1. En **Mobile**, elija la aplicación móvil bajo demanda en el catálogo.
1. En el mosaico **Administrar pancartas** , seleccione un letrero para cargar en Mobile On-Demand.
1. Agregue más pancartas si es necesario desde la vista de lista.
1. Seleccione **Cargar** en la barra de acciones y, a continuación, haga clic en Cargar en el cuadro de diálogo.
1. Los letreros ahora se cargan en Mobile On-Demand.

![climage_1-7](assets/chlimage_1-7.gif)

## Eliminación de un letrero {#deleting-a-banner}

Esta operación elimina la pancarta seleccionada de Mobile On-Demand y, opcionalmente, de la instancia local de AEM.

Flujo de trabajo general para eliminar una pancarta:

1. En Mobile, elija la aplicación móvil bajo demanda en el catálogo.
1. Seleccione la pancarta que desea eliminar en el mosaico **Administrar pancartas** .
1. Asegúrese de que esté seleccionado en la lista (seleccione otros para eliminar según sea necesario).
1. Click **Delete** from the action bar.
1. Compruebe si desea eliminar de AEM y Mobile On-Demand.
1. Haga clic en **Eliminar**.
1. La pancarta se ha eliminado de la lista.

### Pasos siguientes {#the-next-steps}

Una vez que aprenda a administrar letreros, consulte

* [Administración de artículos](/help/mobile/mobile-on-demand-managing-articles.md)
* [Administración de colecciones](/help/mobile/mobile-on-demand-managing-collections.md)
* [Carga de recursos compartidos](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicación/Cancelación de la publicación del contenido](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Vista previa con verificación previa](/help/mobile/aem-mobile-manage-ondemand-services.md)
