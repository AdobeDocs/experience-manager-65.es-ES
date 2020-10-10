---
title: Notas de la versión de [!DNL Adobe Experience Manager Assets] 6.5.
description: The new capabilities and enhancements to [!DNL Adobe Experience Manager] 6.5 [!DNL Assets].
translation-type: tm+mt
source-git-commit: 2cccbdea594bb9ba61e8c0f7884b724aab10b5da
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 41%

---


# [!DNL Adobe Experience Manager Assets] notas de la versión {#aem-assets-release-notes}

Here are the key features and highlights of the [!DNL Adobe Experience Manager] 6.5 [!DNL Assets] release.

## Integration with [!DNL Adobe Creative Cloud] and creative workflows {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager] ofrece varias formas de integración con y permite compartir recursos para usarlos en flujos de trabajo en los que los equipos creativos, de marketing o de negocios colaboran estrechamente.[!DNL Adobe Creative Cloud] [!DNL Experience Manager] 6.5 continúa mejorando la integración y la optimiza para ofrecer más oportunidades y agilizar los métodos existentes.

Read on to know the specific capabilities and integrations of [!DNL Experience Manager] 6.5 that you can leverage to best support your content velocity use cases.

### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] fortalece la colaboración entre creativos y especialistas en marketing en el proceso de creación de contenido. Creatives can access content stored in [!DNL Experience Manager Assets], without leaving the apps that they are most familiar with. Creatives can seamlessly browse, search, check out, and check in assets using the in-app panel in [!DNL Adobe Photoshop], [!DNL Adobe Illustrator], and [!DNL Adobe InDesign] apps.

[!DNL Adobe Asset Link] forma parte de la oferta de [Creative Cloud para empresas](https://www.adobe.com/creativecloud/business/enterprise.html) . For more information about it, including necessary configuration of your [!DNL Experience Manager] deployment, see [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html).

![Buscar recursos en Adobe Photoshop](assets/asset_search_photoshop.png)

### [!DNL Adobe Stock] integración {#stock}

Your organization can use its [!DNL Adobe Stock] enterprise plan within [!DNL Experience Manager Assets] to ensure that licensed assets are broadly available for your creative and marketing projects. You can quickly find, preview, and license [!DNL Adobe Stock] assets that are saved in Experience Manager, using the powerful DAM capabilities of [!DNL Experience Manager].

[!DNL Adobe Stock]El servicio proporciona a diseñadores y empresas acceso a millones de fotos, vectores, ilustraciones, vídeos, plantillas y recursos 3D de alta calidad, verificados y libres de derechos de autor para todos sus proyectos creativos.

For more info, see [Use Adobe Stock assets in Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md).

![Previsualización de imágenes y licencias de Adobe Stock desde Experience Manager Assets](assets/stock_image_preview_license_options.png)

*Figura: Previsualización[!DNL Adobe Stock]imagen y licencia desde dentro[!DNL Experience Manager Assets].*

![Buscar y filtrar las imágenes de Adobe Stock con licencia en Experience Manager](assets/aem-search-filters2.jpg)

*Figura: Busque y filtre las[!DNL Adobe Stock]imágenes con licencia en[!DNL Experience Manager].*

### Dynamic references in [!DNL Adobe InDesign] {#dynamic-references-in-indesign}

[!DNL Experience Manager Assets] se utilizan en [!DNL Adobe InDesign] archivos dinámicos. Las referencias se actualizan automáticamente si los recursos a los que se hace referencia se mueven en el repositorio. Para obtener más información, consulte [cómo administrar recursos](/help/assets/managing-linked-subassets.md)compuestos.

## Capacidades de Brand Portal {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] le ayuda a adquirir, controlar y distribuir de forma eficaz y segura los recursos aprobados a agencias o proveedores externos y a usuarios de negocios internos en todos los dispositivos. Asimismo, le permite mejorar la eficiencia del uso compartido de recursos, acelera el tiempo de comercialización de esos recursos y elimina el riesgo de uso indebido y los accesos no autorizados.

Para obtener más información, consulte [Novedades de Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/using/whats-new.html).

## Recursos conectados {#connectedassets}

En las grandes empresas se puede distribuir la infraestructura necesaria para crear sitios web. A veces, las capacidades de creación de sitios web y los recursos digitales necesarios residen en distintos silos.

[!DNL Experience Manager Sites] ofrece capacidades de crear páginas web y es el sistema de gestión de recursos digitales (DAM) que proporciona los recursos necesarios para los sitios web.[!DNL Experience Manager Assets] [!DNL Experience Manager] ahora admite el caso de uso anterior mediante la integración [!DNL Sites] y [!DNL Assets]. Consulte [cómo configurar y utilizar la función](/help/assets/use-assets-across-connected-assets-instances.md)Recursos conectados.

![Arrastre un recurso desde una [!DNL Experience Manager] implementación en una [!DNL Sites] página de una implementación diferente [!DNL Experience Manager]](assets/connected-assets-drag-and-drop-only.gif)

*Figura: Arrastre un recurso desde una[!DNL Experience Manager]implementación en una[!DNL Sites]página en otra[!DNL Experience Manager]implementación.*

## Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] proporciona envío y creación de medios enriquecidos mejorados [!DNL Experience Manager Assets] para impulsar experiencias de vanguardia que son envolventes y personalizadas. Al cargar un único recurso maestro de alta calidad y utilizar nuestros visores y procesamiento avanzados en la nube, puede distribuir cualquier combinación de representaciones sobre la marcha para respaldar la estrategia de medios de su organización.

For more details on new [!DNL Dynamic Media] features see [Dynamic Media Release Notes](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/release-notes/s7rn2017.html).

### 360 video support {#video-support}

Manage your 360-video files directly in [!DNL Experience Manager] using the cutting edge viewers to deliver VR-experiences to desktops, mobile and VR-headsets. Para obtener más información, consulte [Uso de vídeos 360](/help/assets/360-video.md).

### Custom video thumbnails {#custom-video-thumbnails}

Ahora puede personalizar las miniaturas de sus recursos de vídeo utilizando fotogramas del propio vídeo u otro contenido almacenado en DAM. Para obtener instrucciones adicionales, consulte [Acerca de las miniaturas de vídeo](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

### Mejoras de accesibilidad {#accessibility-enhancements}

[!DNL Dynamic Media] los visores ahora admiten funciones de accesibilidad mejoradas como compatibilidad con Aria, lectores de pantalla y texto alternativo. Para obtener información adicional, consulte [Notas de versión de los visores de Dynamic Media](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/home.html).

## Mejora de la opción de búsqueda {#experience-enhancement-for-searching}

[!DNL Experience Manager] A partir de la versión 6.5, los especialistas en mercadotecnia pueden descubrir los recursos deseados con mayor rapidez desde la página de resultados de búsqueda. Las facetas de búsqueda se actualizan con el número de recursos incluso antes de aplicar el filtro de búsqueda. Ver la cantidad esperada con el filtro ayuda a los usuarios a navegar a través de los resultados de búsqueda de forma eficaz. Para obtener más información, consulte [Buscar recursos en Experience Manager](../assets/search-assets.md).

![Ver el número de recursos sin filtrar los resultados de búsqueda en las facetas de búsqueda](/help/assets/assets/asset_search_results_in_facets_filters.png)

*Figura: Ver el número de recursos sin filtrar los resultados de búsqueda en facetas de búsqueda.*

## Mejora de la capacidad de uso {#usability-enhancement}

Ahora puede seleccionar todos los recursos cargados dentro de una carpeta o desde un resultado de búsqueda con una sola acción. Esto le permite administrar varios recursos rápidamente. The check box selects all the assets that fits the scenario, say a search result and not just the assets that are visible in the [!DNL Experience Manager] interface.

![Utilice la opción Seleccionar todo para seleccionar todos los recursos cargados con un solo clic.](assets/select-all-in-aem-assets.gif)

*Figura: Utilice la opción Seleccionar todo para seleccionar todos los recursos cargados con un solo clic.*

## Mejoras en los metadatos {#metadata-enhancements}

[!DNL Assets] le permite crear esquemas de metadatos para carpetas de recursos, que definen el diseño y los metadatos mostrados en las páginas de propiedades de las carpetas. Ahora puede asignar un esquema de metadatos de carpeta a una carpeta existente o al crear una carpeta nueva. Para obtener más información, consulte [Esquema de metadatos de carpeta](/help/assets/metadata-config.md#folder-metadata-schema).

Al especificar los metadatos en cascada, las opciones se pueden cargar desde un archivo JSON en tiempo de ejecución, en lugar de escribir manualmente en el formulario. For more information, see [cascading metadata](/help/assets/metadata-schemas.md#cascading-metadata).

## Mejoras en los informes {#reporting-enhancements}

Los fragmentos de contenido y los recursos compartidos de vínculos se incluyen ahora en el informe descargado. Para obtener más información, consulte los [informes de recursos](/help/assets/asset-reports.md).
