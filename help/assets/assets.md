---
title: Introducción a [!DNL Adobe Experience Manager Assets]
description: Descubra qué es la administración de recursos digitales, sus casos de uso y la oferta  [!DNL Adobe Experience Manager Asset] .
contentOwner: AG
feature: Asset Management
role: Leader, Architect, Business Practitioner
translation-type: tm+mt
source-git-commit: ebe7042b931869c3b4b7204e3ce7afa52d56f0ef
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Acerca de [!DNL Adobe Experience Manager Assets] como solución DAM {#administering-assets}

[!DNL Assets] es una herramienta de administración de recursos digitales (DAM) que forma parte integral de la  [!DNL Experience Manager] plataforma y permite a su empresa administrar y distribuir recursos digitales. Los usuarios de una organización pueden administrar, almacenar y acceder a muchos tipos de recursos digitales, como imágenes, vídeos, documentos, clips de audio, archivos 3D y medios enriquecidos, para utilizarlos en la web, en la impresión y para la distribución digital.

## ¿Qué es la administración de activos digitales? {#what-is-digital-asset-management}

[!DNL Assets] proporciona un método de uso compartido y distribución en toda la empresa de los activos digitales clave de una organización. Los usuarios de una organización pueden almacenar, administrar y acceder a recursos digitales, como imágenes, gráficos, audio, vídeo y documentos, a través de una interfaz web (o una carpeta CIFS o WebDAV).

[!DNL Assets] permite  [!DNL Experience Manager] hacer lo siguiente:

* Añadir y compartir imágenes, documentos, audio y vídeo en diversos formatos de archivo.
* Administre los recursos agrupándolos por etiquetas, lightbox o estrellas (sus favoritos). Añadir anotaciones a los recursos.
* Buscar recursos por nombres de archivo, texto completo de documentos, fechas, tipo de documento y etiquetas.
* Añadir o editar información de metadatos para los activos. Automáticamente, se genera una versión de los metadatos junto con el activo correspondiente. Los metadatos de activos se pueden importar o exportar.
* Realizar funciones de edición de imágenes, como escalar y añadir filtros de imagen. Importar y exportar varios activos digitales de forma simultánea mediante una carpeta WebDAV o CIFS.
* Usar los flujos de trabajo y las notificaciones para permitir el procesamiento y la descarga de forma conjunta de cualquier grupo de activos y administrar los derechos de acceso a los activos.

### [!DNL Experience Manager Assets] está integrado con  [!DNL Experience Manager Sites] {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] se integra completamente con  [!DNL Sites] y funciona perfectamente para todos los casos de uso. Por ejemplo, al crear páginas web, los autores de [!DNL Sites] pueden encontrar y utilizar los recursos digitales mediante el Buscador de contenido. La interfaz de usuario de [!DNL Assets] es la misma que la de [!DNL Sites]. Consulte [descripción general de Sitios](/help/sites-authoring/page-authoring.md) para obtener más información.

La interfaz de usuario básica es la misma que la de [!DNL Sites]. Consulte [Información general de los sitios](/help/sites-authoring/page-authoring.md) para obtener más información.

### Administración de activos digitales frente a componente de imagen {#digital-asset-management-versus-image-component}

Cuando determine si desea colocar una imagen en un repositorio DAM o utilizar un componente de imagen, tenga en cuenta el ciclo de vida de la imagen:

* Si la imagen tiene el mismo ciclo de vida que la página, utilice el componente Imagen .
* Si la imagen tiene un ciclo de vida independiente, por ejemplo, si utiliza la imagen dos veces o fuera de WCM, emplee [!DNL Assets].

## ¿Qué son los recursos digitales? {#what-are-digital-assets}

Un recurso es un documento digital, una imagen, un vídeo o audio (o parte del mismo) que puede tener varias representaciones y subrecursos (por ejemplo, capas en un archivo de Photoshop, diapositivas en un archivo de PowerPoint, páginas en un pdf o archivos en un ZIP).

Un activo es, en esencia, un binario más metadatos, representaciones y subactivos. Consulte la [Guía de rendimiento de DAM](/help/sites-deploying/assets-performance-sizing.md) para obtener información detallada.

>[!CAUTION]
>
>Cargar o editar un gran volumen de recursos (especialmente imágenes) puede afectar al rendimiento de su implementación [!DNL Experience Manager].

### [!DNL Experience Manager Assets] terminología  {#aem-assets-terminology}

Al trabajar con recursos digitales en [!DNL Experience Manager], debe comprender la siguiente terminología:

* **Colección**: Una colección de recursos, ya sea en función de la ubicación física (carpeta), las propiedades comunes (carpeta de búsqueda guardada) o la selección de usuarios (carpetas Lightbox).

* **** [!DNL Assets] Los metadatos tienen metadatos; por ejemplo, autor, fecha de caducidad, información de DRM (Digital Rights Management), etc. Los metadatos están sujetos a control de acceso. [!DNL Assets] admite los siguientes esquemas comunes de metadatos predefinidos:

   * Dublin Core: incluye autor, descripción, fecha, asunto, etc.
   * IPTC: incluye evento, modelo, ubicación, etc.
   * WCM: incluidas las propiedades de página, [!UICONTROL Tiempo de activación] y [!UICONTROL Tiempo de inactividad], entre otros.

* **Etiquetado**:  [!DNL Assets] se pueden etiquetar y clasificar. Consulte [organización de recursos](/help/assets/organize-assets.md).

* **Representaciones**: Una representación es la representación binaria de un recurso. [!DNL Assets] siempre tienen una representación principal: la del archivo cargado. Pueden tener una multitud de representaciones adicionales que se crean, por ejemplo, por medio de flujos de trabajo personalizados o al cargar un recurso. Las representaciones pueden tener tamaños y resoluciones distintas, y tener agregadas marcas de agua o cualquier otra característica modificada.

* **Versiones**: Al generar versiones, se crea una instantánea de los recursos digitales en un momento específico. Los activos se pueden restaurar a versiones anteriores. Consulte [versioning in [!DNL Assets]](manage-assets.md#asset-versioning).

* **Subactivos**: Los subrecursos son recursos que constituyen un recurso; por ejemplo, capas de un  [!DNL Adobe Photoshop] archivo o páginas de un archivo PDF. En [!DNL Assets], puede administrar los subrecursos del mismo modo que lo haría con los recursos.

### Cómo trabajar con recursos digitales {#how-to-work-with-assets}

Las acciones se realizan sobre activos o colecciones. Sirven para crear o modificar activos, colecciones y representaciones. Muchas de las acciones básicas que realiza en los recursos (cargar, eliminar, actualizar y guardar subrecursos) realizan déclencheur en flujos de trabajo preconfigurados. Estos se activan automáticamente en [!DNL Assets] y se describen detalladamente en [!DNL Assets] controladores de medios.

Las tareas que puede realizar con estos flujos de trabajo preconfigurados:

* Guarde el recurso en el repositorio o elimínelo de él.
* Extraer y guardar metadatos del recurso; los elementos de metadatos individuales se guardan como XMP.
* Generar representaciones y miniaturas del recurso; incluido el cambio de tamaño y el recorte automáticos cuando sea necesario.
* Transcodificar el recurso donde sea necesario. Por ejemplo, los vídeos para uso en móviles e Internet se transcodifican con 24 fotogramas por segundo y se descargan con 30 fotogramas por segundo. El audio para uso móvil y web se transcodifica con 128 Kbps, y el audio se descarga con 192 Kbps.

Los flujos de trabajo también se pueden aplicar manualmente. Consulte en [Controladores de medios de Assets](media-handlers.md) la lista de flujos de trabajo predeterminados.

## [!DNL Experience Manager Assets] y  [!DNL Media Library] {#cq-dam-vs-cq-medialibrary}

Consulte [Recursos y Biblioteca de medios](medialibrary.md) para obtener información sobre las diferencias.

>[!MORELIKETHIS]
>
>* [Introducción al vídeo: Recursos de Experience Manager como DAM moderno](https://www.youtube.com/watch?v=PBwQqZgC-yo)
>* [Explicación de los conceptos de metadatos](/help/assets/metadata-concepts.md)

