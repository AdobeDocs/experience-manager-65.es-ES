---
title: Prácticas recomendadas para procesar los formatos de archivo admitidos
description: Prácticas recomendadas para procesar los distintos tipos de archivos admitidos con [!DNL Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---


# Prácticas recomendadas sobre el formato de archivo de recursos {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] admite muchas bibliotecas de formato de archivos de propiedad y de terceros para satisfacer los diversos requisitos de compatibilidad de archivos de los usuarios. Las bibliotecas de Adobe admitidas son [!DNL Adobe Camera Raw], Gibson, Adobe PDF Rasterizer y [!DNL Adobe InDesign Server]. Además, [!DNL Experience Manager Assets] admite bibliotecas de terceros, incluidas [!DNL ImageMagick], [!DNL TwelveMonkeys], etc.

Para ver los formatos de archivo admitidos, consulte [Formatos admitidos por los recursos](/help/assets/assets-formats.md).

>[!TIP]
>
>Si utiliza [!DNL Experience Manager] en los servicios gestionados de Adobe (AMS), póngase en contacto con el servicio de atención al cliente de Adobe si tiene previsto procesar muchos archivos PSD o PSB de gran tamaño. Trabaje con el representante del Servicio de atención al cliente de Adobe para implementar estas optimizaciones para la implementación de AMS y para elegir las mejores herramientas y modelos posibles para los formatos propios de Adobe. [!DNL Experience Manager] es posible que no procese archivos PSB de alta resolución que superen los 30000 x 23000 píxeles.

## [!DNL Adobe Camera Raw] biblioteca  {#adobe-camera-raw-library}

Para un rendimiento óptimo, Adobe recomienda utilizar la biblioteca [!DNL Adobe Camera Raw] para archivos RAW y DNG.

[!DNL Adobe Camera Raw] la biblioteca admite el perfil de color CMYK como entrada. Sin embargo, genera la salida en espacio de color RGB y admite la salida en formato JPEG solamente. No conserva el espacio de color del archivo de origen (por ejemplo, CMYK) en las miniaturas.

Para obtener más información, consulte [Soporte Camera Raw](/help/assets/camera-raw.md).

## Biblioteca Adobe PDF Rasterizer {#adobe-pdf-rasterizer-library}

Para obtener los mejores resultados, Adobe recomienda utilizar la biblioteca Adobe PDF Rasterizer para los siguientes archivos:

* Archivos PDF pesados y con gran contenido
* Archivos AI con miniaturas no generados de forma predeterminada
* Para archivos AI con colores SPOT (PMS)

Las miniaturas y previsualizaciones que se generan con el rasterizador de PDF son de mejor calidad en comparación con la salida de rasterizado lista para usar. La biblioteca Rasterizer de Adobe PDF no admite ninguna conversión de espacio de color. Independientemente del espacio de color del archivo PDF de origen, Adobe PDF Rasterizer sólo genera salida RGB.

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobe recomienda utilizar [!DNL Adobe InDesign Server] para extraer representaciones específicas de [!DNL Adobe InDesign], como IDML y HTML. Para obtener más información, consulte [Añadir recursos de Experience Manager como referencias en Adobe InDesign](/help/assets/managing-linked-subassets.md#refai).

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media] genera y ofrece múltiples variaciones de contenido enriquecido en tiempo real a través de su red global, escalable y optimizada para el rendimiento. Ofrece experiencias de visualización interactivas y optimiza el proceso de gestión de la campaña digital. Para obtener más información sobre cómo habilitar [!DNL Dynamic Media], consulte [Configuración de Dynamic Media](/help/assets/config-dynamic.md).

Actualmente, [!DNL Dynamic Media] admite vídeos de hasta 15 GB de contenido por archivo.

## Biblioteca ImageMagick {#imagemagick-library}

Adobe recomienda utilizar la biblioteca ImageMagick en los siguientes casos:

* Para generar representaciones en miniatura para archivos EPS.
* Para conservar la información del perfil de la imagen.
* Para preservar la transparencia.
* Para procesar archivos PSD y PSB.

Para saber cómo configurar la biblioteca [!DNL ImageMagick] en [!DNL Experience Manager], consulte [Uso de ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick). Para obtener un uso óptimo, consulte [Prácticas recomendadas para configurar ImageMagick](/help/assets/best-practices-for-imagemagick.md).

## Biblioteca de transcodificación de imágenes {#image-transcoding-library}

La biblioteca de transcodificación de imágenes de Adobe es una solución de procesamiento de imágenes que realiza funciones básicas de gestión de imágenes, como codificación de imágenes, transcodificación, remuestreo, cambio de tamaño, etc.

La biblioteca de transcodificación de imágenes admite los siguientes tipos MIME:

* JPG/JPEG
* PNG (8 y 16 bits)
* GIF
* BMP
* TIFF/TIFF comprimido (excepto Tiffs de 32 bits y PTiffs).
* ICO
* ICN

Para obtener más información, consulte [Biblioteca de transcodificación de imágenes](/help/assets/imaging-transcoding-library.md).
