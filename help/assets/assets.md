---
title: Introducción a  [!DNL Adobe Experience Manager Assets]
description: Cree, administre, procese y distribuya recursos digitales en Experience Manager. Estas guías describen las prácticas recomendadas, las funciones de accesibilidad y cómo utilizar recursos de AEM 6.5.
contentOwner: AG
feature: Asset Management
role: Leader, Architect, User
exl-id: 68239634-a2e8-414e-a866-cd8082641ee8
source-git-commit: fcf7f56fe04cffb077bb40d11429b0c425876489
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 3%

---

# Acerca de [!DNL Adobe Experience Manager Assets] como solución DAM {#administering-assets}

AEM [!DNL Assets] es una herramienta de administración de activos digitales (DAM) que forma parte de [!DNL Experience Manager] y permite a su empresa gestionar y distribuir recursos digitales. Los usuarios de una organización pueden administrar, almacenar y acceder a muchos tipos de recursos digitales, como imágenes, vídeos, documentos, clips de audio, archivos 3D y medios enriquecidos, para usarlos en la web, en la impresión y para la distribución digital.

## ¿Qué es la administración de activos digitales? {#what-is-digital-asset-management}

[!DNL Assets] permite compartir y distribuir en toda la empresa los recursos digitales clave de la organización. CIF Los usuarios de una organización pueden almacenar, administrar y acceder a recursos digitales, como imágenes, gráficos, audio, vídeo y documentos, a través de una interfaz web (o una carpeta de o WebDAV).

[!DNL Assets] capacidad de [!DNL Experience Manager] permite hacer lo siguiente:

* Agregue y comparta imágenes, documentos, archivos de audio y archivos de vídeo en varios formatos de archivo.
* Administre los recursos agrupándolos por etiquetas, lightbox o estrellas (sus favoritos). Agregar anotaciones a recursos.
* Busque recursos buscando nombres de archivo, el texto completo de los documentos y buscando fechas, tipo de documento y etiquetas.
* Añada o edite la información de metadatos de los recursos. Las versiones de los metadatos se realizan automáticamente junto con el recurso correspondiente. Puede importar o exportar metadatos de recursos.
* Realizar funciones de edición de imágenes, como escalar y añadir filtros de imagen. CIF Importe y exporte varios recursos digitales simultáneamente mediante un WebDAV o una carpeta de la.
* Utilice flujos de trabajo y notificaciones para permitir el procesamiento y la descarga conjuntos de cualquier conjunto de recursos y administrar los derechos de acceso a los recursos.

### [!DNL Experience Manager Assets] está integrado con [!DNL Experience Manager Sites] {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] se integra completamente con [!DNL Sites] y funciona perfectamente para todos los casos de uso. Por ejemplo, al crear páginas web, la variable [!DNL Sites] Los creadores pueden encontrar y utilizar los recursos digitales a través del buscador de contenido. La interfaz de usuario de [!DNL Assets] es igual que el de [!DNL Sites]. Consulte un [descripción general de Sites](/help/sites-authoring/page-authoring.md) para obtener información detallada.

La interfaz de usuario básica es la misma que la de [!DNL Sites]. Consulte [Información general de los sitios](/help/sites-authoring/page-authoring.md) para obtener información detallada.

### Administración de activos digitales frente a componente de imagen {#digital-asset-management-versus-image-component}

Al determinar si colocar una imagen en el repositorio de DAM o utilizar un componente de imagen, tenga en cuenta el ciclo vital de la imagen:

* Si la imagen tiene el mismo ciclo de vida que la página, utilice el componente Imagen.
* Si la imagen tiene un ciclo de vida independiente, por ejemplo, si utiliza la imagen dos veces o fuera de WCM, utilice [!DNL Assets].

## ¿Qué son los recursos digitales? {#what-are-digital-assets}

Un recurso es un documento digital, una imagen, un vídeo o audio (o parte del mismo) que puede tener varias representaciones. También puede tener subrecursos, por ejemplo, capas en un archivo Photoshop, diapositivas en un archivo PowerPoint, páginas en un PDF o archivos en un ZIP.

Un recurso es esencialmente un binario más metadatos más representaciones más recursos secundarios. Consulte la [Guía de rendimiento de DAM](/help/sites-deploying/assets-performance-sizing.md) para obtener información detallada.

>[!CAUTION]
>
>La carga o edición de un gran volumen de recursos (especialmente imágenes) puede afectar al rendimiento de su [!DNL Experience Manager] implementación.

### [!DNL Experience Manager Assets] terminología {#aem-assets-terminology}

Cuando se trabaja con recursos digitales en [!DNL Experience Manager], le resultará útil si comprende la siguiente terminología:

* **Colección**: una colección de recursos, ya sea en función de la ubicación física (carpeta), las propiedades comunes (carpeta de búsqueda guardada) o la selección del usuario (carpetas Lightbox).

* **Metadatos** [!DNL Assets] tienen metadatos; por ejemplo, autor, fecha de caducidad e información de DRM (Digital Rights Management). Los metadatos están bajo control de acceso. [!DNL Assets] admite los siguientes esquemas de metadatos comunes predeterminados:

   * Núcleo de Dublín: incluye autor, descripción, fecha, asunto, etc.
   * IPTC: incluye evento, modelo, ubicación, etc.
   * WCM: incluidas las propiedades de página, [!UICONTROL Tiempo de activación] y [!UICONTROL Tiempo de inactividad], etc.

* **Etiquetado**: [!DNL Assets] pueden etiquetarse y clasificarse. Consulte [organización de recursos](/help/assets/organize-assets.md).

* **Representaciones**: una representación es la representación binaria de un recurso. [!DNL Assets] siempre tienen una representación principal: la del archivo cargado. Pueden tener cualquier número de representaciones adicionales que se crean, por ejemplo, mediante pasos de flujo de trabajo personalizados o cuando se carga un recurso. Las representaciones pueden tener un tamaño diferente, con una resolución diferente, con una marca de agua agregada o cualquier otra característica modificada.

* **Versiones**: el control de versiones crea una instantánea de los recursos digitales en un momento específico. Puede restaurar los recursos a versiones anteriores. Consulte [versiones en [!DNL Assets]](manage-assets.md#asset-versioning).

* **Subrecursos**: los subrecursos son recursos que conforman un recurso, por ejemplo, capas de un [!DNL Adobe Photoshop] archivo o páginas en un archivo de PDF. Entrada [!DNL Assets], puede administrar subrecursos del mismo modo que lo haría con los recursos.

### Cómo trabajar con recursos digitales {#how-to-work-with-assets}

Realiza una acción en un recurso o una colección. Las acciones pueden crear o modificar recursos, colecciones y representaciones. Muchas de las acciones básicas que realiza en los recursos (cargar, eliminar, actualizar, guardar subrecursos) almacenan en déclencheur los flujos de trabajo preconfigurados. Se activan automáticamente en [!DNL Assets] y se describen detalladamente en [!DNL Assets] controladores de medios.

Las tareas que puede realizar con estos flujos de trabajo preconfigurados:

* Guarde el recurso en el repositorio o elimínelo de él.
* XMP Extraiga y guarde metadatos para el recurso; los elementos de metadatos individuales se guardan como elementos de metadatos de archivo
* Generar representaciones y miniaturas del recurso, incluido el cambio de tamaño y el recorte automáticos cuando sea necesario.
* Transcodifique el recurso donde sea necesario. Por ejemplo, el vídeo para uso móvil y web se transcodifica con 24 fotogramas por segundo y el vídeo de descarga con 30 fotogramas por segundo. El audio para uso móvil y web se transcodifica con 128 Kbps, el audio para descarga con 192 Kbps.

También puede aplicar flujos de trabajo manualmente. Consulte [Controladores de medios de recursos](media-handlers.md)para obtener una lista de flujos de trabajo predeterminados.

## [!DNL Experience Manager Assets] y [!DNL Media Library] {#cq-dam-vs-cq-medialibrary}

Consulte [Assets y Media Library](medialibrary.md) para obtener información sobre las diferencias.

>[!MORELIKETHIS]
>
>* [Introducción en vídeo: Experience Manager Assets as a modern DAM](https://www.youtube.com/watch?v=PBwQqZgC-yo)
>* [Comprender los conceptos de metadatos](/help/assets/metadata-concepts.md)
