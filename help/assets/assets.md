---
title: Acerca de Recursos AEM
description: Descubra qué es la administración de recursos digitales, sus casos de uso y la oferta de recursos AEM de Adobe
contentOwner: AG
translation-type: tm+mt
source-git-commit: 01475dc8cf4f1e4cb0575c60523c27105ebd1150

---


# Administración de recursos {#administering-assets}

Assets es una herramienta de gestión de recursos digitales (DAM) totalmente integrada con la plataforma AEM y que permite a su empresa compartir y distribuir recursos digitales. Los usuarios de una organización pueden administrar y almacenar imágenes, vídeos, documentos, clips de audio o medios enriquecidos tales como archivos Flash, así como acceder a ellos, a fin de utilizarlos en Internet, para imprimirlos o para distribuirlos de forma digital.

## What is Digital Asset Management? {#what-is-digital-asset-management}

Assets proporciona un método de uso compartido y distribución en toda la empresa de los activos digitales clave de una organización. Los usuarios de una organización pueden almacenar, administrar y acceder a recursos digitales como imágenes, gráficos, audio, vídeo y documentos a través de una interfaz web (o una carpeta CIFS o WebDAV).

AEM Assets, bien integrado en AEM, le permite hacer lo siguiente:

* Añadir y compartir imágenes, documentos, audio y vídeo en diversos formatos de archivo.
* Administre los recursos agrupándolos por etiquetas, Lightbox o estrellas (sus favoritos). Añadir anotaciones a los recursos.
* Buscar recursos por nombres de archivo, texto completo de documentos, fechas, tipo de documento y etiquetas.
* Añadir o editar información de metadatos para los activos. Automáticamente, se genera una versión de los metadatos junto con el activo correspondiente. Los metadatos de activos se pueden importar o exportar.
* Realizar funciones de edición de imágenes, como escalar y añadir filtros de imagen. Importar y exportar varios activos digitales de forma simultánea mediante una carpeta WebDAV o CIFS.
* Usar los flujos de trabajo y las notificaciones para permitir el procesamiento y la descarga de forma conjunta de cualquier grupo de activos y administrar los derechos de acceso a los activos.

### AEM Assets está completamente integrado en CQ WCM {#aem-assets-fully-integrated-in-cq-wcm}

AEM Assets está totalmente integrado con CQ WCM y la funcionalidad está disponible mediante el icono DAM:

![screen_shot_2012-04-17at15946pm](assets/screen_shot_2012-04-17at15946pm.png) ![screen_shot_2012-04-17at20100pm](assets/screen_shot_2012-04-17at20100pm.png)

A continuación, se puede acceder a los recursos administrados en CQ DAM mediante el buscador de contenido de WCM:

![screen_shot_2012-04-17at20214pm](assets/screen_shot_2012-04-17at20214pm.png)

>[!NOTE]
>
>La administración básica de la interfaz gráfica de usuario es la misma que el resto de WCM; consulte [Visión General de la Consola](/help/sites-authoring/page-authoring.md) GUI para obtener más detalles.

### Administración de activos digitales frente a componente de imagen {#digital-asset-management-versus-image-component}

Al determinar si se debe colocar una imagen en Recursos AEM o utilizar el componente de imagen AEM, tenga en cuenta el ciclo vital de la imagen:

* Si la imagen tiene el mismo ciclo de vida que la página, utilice el componente de imagen.
* Si la imagen tiene un ciclo de vida independiente, por ejemplo, si utiliza la imagen dos veces o fuera de WCM, emplee AEM Assets.

## What are digital assets? {#what-are-digital-assets}

Un recurso es un documento digital, una imagen, un vídeo o audio (o parte del mismo) que puede tener varias representaciones y subrecursos (por ejemplo, capas en un archivo de Photoshop, diapositivas en un archivo de PowerPoint, páginas en un PDF o archivos en un ZIP).

Un activo es, en esencia, un binario más metadatos, representaciones y subactivos. Consulte la [Guía de rendimiento de DAM](/help/sites-deploying/assets-performance-sizing.md) para obtener información detallada.

>[!CAUTION]
>
>La carga y/o edición de un gran volumen de recursos (especialmente imágenes) puede afectar al rendimiento de la instancia de CQ.

### AEM Assets terminology {#aem-assets-terminology}

Cuando se trabaja con activos digitales en AEM, debe conocer los siguientes términos:

* **Colección** Colección de recursos, ya sea en función de la ubicación física (carpeta), las propiedades comunes (carpeta de búsqueda guardada) o la selección de usuarios (carpetas de caja de luz).

* **Los recursos de metadatos** tienen metadatos; por ejemplo, autor, fecha de caducidad, Información de DRM (Digital Rights Management), etc. Los metadatos están sujetos a control de acceso. AEM Assets admite los siguientes esquemas comunes de metadatos predefinidos:

   * Dublin Core: incluye autor, descripción, fecha, asunto, etc.
   * IPTC: incluye evento, modelo, ubicación, etc.
   * WCM: incluyendo propiedades de página, Tiempo [!UICONTROL de activación] y Tiempo de [!UICONTROL desactivación, etc].

* **Los recursos de etiquetado** se pueden etiquetar y clasificar. Consulte Utilización de etiquetas y Administración de etiquetas.

* **Representaciones** Una representación es la representación binaria de un recurso. Los recursos siempre tienen una representación principal, que es la del archivo cargado. Pueden tener una multitud de representaciones adicionales que se crean, por ejemplo, por medio de flujos de trabajo personalizados o al cargar un recurso. Las representaciones pueden tener tamaños y resoluciones distintas, y tener agregadas marcas de agua o cualquier otra característica modificada.

* **Versiones** Al generar una versión se crea una instantánea de los recursos digitales en un momento específico. Los activos se pueden restaurar a versiones anteriores. See [versioning in AEM Assets](managing-assets-touch-ui.md#asset-versioning).

* **Los subrecursos** son recursos que componen un recurso, por ejemplo, capas en un archivo de Adobe Photoshop o páginas en un archivo PDF. En AEM Assets, puede administrar los subactivos igual que los activos.

### How to work with assets {#how-to-work-with-assets}

Las acciones se realizan sobre activos o colecciones. Sirven para crear o modificar activos, colecciones y representaciones. Muchas de las acciones básicas que realiza en los recursos (cargar, eliminar, actualizar y guardar subrecursos) activan flujos de trabajo preconfigurados. Estos se activan automáticamente en AEM Assets y se describen en detalle en los controladores de medios de AEM Assets.

Las tareas que puede realizar con estos flujos de trabajo preconfigurados:

* Guardar el activo en el repositorio o eliminarlo de él.
* Extraer y guardar los metadatos del activo; cada elemento de metadatos se guarda como XMP.
* Generar representaciones y miniaturas del activo, incluido el cambio de tamaño y el recorte automáticos cuando sea necesario.
* Transcodificar el activo en caso necesario. Por ejemplo, los vídeos para uso en móviles e Internet se transcodifican con 24 fotogramas por segundo y se descargan con 30 fotogramas por segundo. El audio para uso en móviles e Internet se transcodifica con 128 kbp y se descarga con 192 kbp.

Los flujos de trabajo también se pueden aplicar manualmente. Consulte en [Controladores de medios de AEM Assets](/help/assets/media-handlers.md) la lista de flujos de trabajo predeterminados.

## AEM Assets and AEM MediaLibrary {#cq-dam-vs-cq-medialibrary}

Consulte Recursos [AEM y AEM MediaLibrary](/help/assets/medialibrary.md) para obtener información sobre las diferencias.
