---
title: Notas de la versión de [!DNL Adobe Experience Manager Assets] 6.5.
description: Las nuevas capacidades y mejoras de [!DNL Adobe Experience Manager] 6.5 [!DNL Assets].
translation-type: tm+mt
source-git-commit: e95f26cc1a084358b6bcb78605e3acb98f257b66
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 41%

---


# [!DNL Adobe Experience Manager Assets] notas de la versión  {#aem-assets-release-notes}

Estas son las características clave y los aspectos destacados de la [!DNL Adobe Experience Manager] versión 6.5 [!DNL Assets].

## Integración con [!DNL Adobe Creative Cloud] y flujos de trabajo creativos {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager] ofrece varias formas de integración con y permite compartir recursos para usarlos en flujos de trabajo en los que los equipos creativos, de marketing o de negocios colaboran estrechamente.[!DNL Adobe Creative Cloud] [!DNL Experience Manager] 6.5 continúa mejorando la integración y la optimiza para ofrecer más oportunidades y agilizar los métodos existentes.

Continúe leyendo para conocer las capacidades e integraciones específicas de [!DNL Experience Manager] 6.5 que puede aprovechar para admitir mejor los casos de uso de velocidad de contenido.

### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] fortalece la colaboración entre creativos y especialistas en marketing en el proceso de creación de contenido. Los elementos creativos pueden acceder al contenido almacenado en [!DNL Experience Manager Assets] sin dejar las aplicaciones con las que están más familiarizados. Los elementos creativos pueden examinar, buscar, extraer y registrar recursos sin problemas mediante el panel integrado en la aplicación de las aplicaciones [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] y [!DNL Adobe InDesign].

[!DNL Adobe Asset Link] es parte de un  [Creative Cloud de ](https://www.adobe.com/creativecloud/business/enterprise.html) oferta empresarial. Para obtener más información al respecto, incluida la configuración necesaria de la implementación [!DNL Experience Manager], consulte [Vínculo de recursos de Adobe](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html).

![Buscar recursos en Adobe Photoshop](assets/asset_search_photoshop.png)

### [!DNL Adobe Stock] integración  {#stock}

Su organización puede utilizar su [!DNL Adobe Stock] plan empresarial dentro de [!DNL Experience Manager Assets] para garantizar que los activos con licencia estén disponibles en general para sus proyectos creativos y de mercadotecnia. Puede encontrar, previsualización y obtener licencias [!DNL Adobe Stock] rápidamente de los recursos que se guardan en Experience Manager, mediante las potentes capacidades de DAM de [!DNL Experience Manager].

[!DNL Adobe Stock]El servicio proporciona a diseñadores y empresas acceso a millones de fotos, vectores, ilustraciones, vídeos, plantillas y recursos 3D de alta calidad, verificados y libres de derechos de autor para todos sus proyectos creativos.

Para obtener más información, consulte [Uso de recursos de Adobe Stock en Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md).

![Previsualización de imágenes y licencias de Adobe Stock desde Experience Manager Assets](assets/stock_image_preview_license_options.png)

*Figura: Previsualización de  [!DNL Adobe Stock] imagen y licencia desde dentro  [!DNL Experience Manager Assets].*

![Buscar y filtrar las imágenes de Adobe Stock con licencia en Experience Manager](assets/aem-search-filters2.jpg)

*Figura: Busque y filtre las  [!DNL Adobe Stock] imágenes con licencia en  [!DNL Experience Manager].*

### Referencias dinámicas en [!DNL Adobe InDesign] {#dynamic-references-in-indesign}

[!DNL Experience Manager Assets] se utilizan en  [!DNL Adobe InDesign] archivos dinámicos. Las referencias se actualizan automáticamente si los recursos a los que se hace referencia se mueven en el repositorio. Para obtener más información, consulte [cómo administrar recursos compuestos](/help/assets/managing-linked-subassets.md).

## Capacidades de Brand Portal {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] le ayuda a adquirir, controlar y distribuir de forma eficaz y segura los recursos aprobados a agencias o proveedores externos y a usuarios de negocios internos en todos los dispositivos. Asimismo, le permite mejorar la eficiencia del uso compartido de recursos, acelera el tiempo de comercialización de esos recursos y elimina el riesgo de uso indebido y los accesos no autorizados.

Para obtener más información, consulte [Novedades de Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/using/whats-new.html).

## Recursos conectados {#connectedassets}

En las grandes empresas se puede distribuir la infraestructura necesaria para crear sitios web. A veces, las capacidades de creación de sitios web y los recursos digitales necesarios residen en distintos silos.

[!DNL Experience Manager Sites] ofrece capacidades de crear páginas web y es el sistema de gestión de recursos digitales (DAM) que proporciona los recursos necesarios para los sitios web.[!DNL Experience Manager Assets] [!DNL Experience Manager] ahora admite el caso de uso anterior mediante la integración  [!DNL Sites] y  [!DNL Assets]. Consulte [cómo configurar y utilizar la función Recursos conectados](/help/assets/use-assets-across-connected-assets-instances.md).

![Arrastre un recurso desde una  [!DNL Experience Manager] implementación en una  [!DNL Sites] página de otra  [!DNL Experience Manager] implementación](assets/connected-assets-drag-and-drop-only.gif)

*Figura: Arrastre un recurso desde una  [!DNL Experience Manager] implementación en una  [!DNL Sites] página en una  [!DNL Experience Manager] implementación diferente.*

## Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] proporciona envío y creación de medios enriquecidos mejorados  [!DNL Experience Manager Assets] para impulsar experiencias de vanguardia que son envolventes y personalizadas. Al cargar un único recurso maestro de alta calidad y utilizar nuestros visores y procesamiento avanzados en la nube, puede distribuir cualquier combinación de representaciones sobre la marcha para respaldar la estrategia de medios de su organización.

Para obtener más información sobre las nuevas [!DNL Dynamic Media] funciones, consulte [Notas de la versión de Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html).

### Compatibilidad con video de 360 {#video-support}

Administre sus archivos de 360 vídeos directamente en [!DNL Experience Manager] mediante los visores más avanzados para ofrecer experiencias de VR a equipos de escritorio, dispositivos móviles y auriculares VR. Para obtener más información, consulte [Uso de vídeos 360](/help/assets/360-video.md).

### Miniaturas de vídeo personalizadas {#custom-video-thumbnails}

Ahora puede personalizar las miniaturas de sus recursos de vídeo utilizando fotogramas del propio vídeo u otro contenido almacenado en DAM. Para obtener instrucciones adicionales, consulte [Acerca de las miniaturas de vídeo](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

### Mejoras de accesibilidad {#accessibility-enhancements}

[!DNL Dynamic Media] los visores ahora admiten funciones de accesibilidad mejoradas como compatibilidad con Aria, lectores de pantalla y texto alternativo. Para obtener información adicional, consulte [Notas de versión de los visores de Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/home.html).

## Mejora de la opción de búsqueda {#experience-enhancement-for-searching}

[!DNL Experience Manager] A partir de la versión 6.5, los especialistas en mercadotecnia pueden descubrir los recursos deseados con mayor rapidez desde la página de resultados de búsqueda. Las facetas de búsqueda se actualizan con el número de recursos incluso antes de aplicar el filtro de búsqueda. Ver la cantidad esperada con el filtro ayuda a los usuarios a navegar a través de los resultados de búsqueda de forma eficaz. Para obtener más información, consulte [Buscar recursos en Experience Manager](../assets/search-assets.md).

![Ver el número de recursos sin filtrar los resultados de búsqueda en las facetas de búsqueda](/help/assets/assets/asset_search_results_in_facets_filters.png)

*Figura: Ver el número de recursos sin filtrar los resultados de búsqueda en facetas de búsqueda.*

## Mejora de la capacidad de uso {#usability-enhancement}

Ahora puede seleccionar todos los recursos cargados dentro de una carpeta o desde un resultado de búsqueda con una sola acción. Esto le permite administrar varios recursos rápidamente. La casilla de verificación selecciona todos los recursos que se ajustan al escenario, como un resultado de búsqueda y no sólo los recursos que están visibles en la interfaz [!DNL Experience Manager].

![Utilice la opción Seleccionar todo para seleccionar todos los recursos cargados con un solo clic.](assets/select-all-in-aem-assets.gif)

*Figura: Utilice la opción Seleccionar todo para seleccionar todos los recursos cargados con un solo clic.*

## Mejoras en los metadatos {#metadata-enhancements}

[!DNL Assets] le permite crear esquemas de metadatos para carpetas de recursos, que definen el diseño y los metadatos mostrados en las páginas de propiedades de las carpetas. Ahora puede asignar un esquema de metadatos de carpeta a una carpeta existente o al crear una carpeta nueva. Para obtener más información, consulte [Esquema de metadatos de carpeta](/help/assets/metadata-config.md#folder-metadata-schema).

Al especificar los metadatos en cascada, las opciones se pueden cargar desde un archivo JSON en tiempo de ejecución, en lugar de escribir manualmente en el formulario. Para obtener más información, consulte [metadatos en cascada](/help/assets/metadata-schemas.md#cascading-metadata).

## Mejoras en los informes {#reporting-enhancements}

Los fragmentos de contenido y los recursos compartidos de vínculos se incluyen ahora en el informe descargado. Para obtener más información, consulte los [informes de recursos](/help/assets/asset-reports.md).
