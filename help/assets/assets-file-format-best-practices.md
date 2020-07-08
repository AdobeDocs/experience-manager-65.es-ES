---
title: Prácticas recomendadas para procesar los distintos formatos de archivo admitidos mediante [!DNL Adobe Experience Manager Assets].
description: Prácticas recomendadas para procesar los distintos tipos de archivos admitidos mediante [!DNL Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 678e91699523c22a7048bd7b344fa539b849ae8b
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---


# Assets file format best practices {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] admite muchas bibliotecas de formato de archivos de propiedad y de terceros para satisfacer los diversos requisitos de compatibilidad de archivos de los usuarios. Las bibliotecas de Adobe admitidas incluyen, [!DNL Adobe Camera Raw], Gibson, Adobe PDF Rasterizer y [!DNL Adobe InDesign Server]. Además, [!DNL Experience Manager Assets] admite bibliotecas de terceros, incluidas [!DNL ImageMagick], [!DNL TwelveMonkeys]etc.

For the supported file formats, see [Assets supported formats](/help/assets/assets-formats.md).

>[!TIP]
>
>Si utiliza [!DNL Experience Manager] Adobes Managed Services (AMS), póngase en contacto con el Servicio de atención al cliente de Adobe si tiene previsto procesar muchos archivos PSD o PSB de gran tamaño. Póngase en contacto con el representante del Servicio de atención al cliente de Adobe para implementar estas optimizaciones para la implementación de AMS y para elegir las mejores herramientas y modelos posibles para los formatos propietarios de Adobe. [!DNL Experience Manager] es posible que no procese archivos PSB de alta resolución que superen los 30000 x 23000 píxeles.

## [!DNL Adobe Camera Raw] biblioteca {#adobe-camera-raw-library}

Para un rendimiento óptimo, Adobe recomienda utilizar [!DNL Adobe Camera Raw] la biblioteca para archivos RAW y DNG.

[!DNL Adobe Camera Raw] la biblioteca admite el perfil de color CMYK como entrada. Sin embargo, genera la salida en espacio de color RGB y admite la salida en formato JPEG solamente. No conserva el espacio de color del archivo de origen (por ejemplo, CMYK) en las miniaturas.

Para obtener más información, consulte Compatibilidad con [Camera Raw](/help/assets/camera-raw.md).

## Biblioteca de Adobe PDF Rasterizer {#adobe-pdf-rasterizer-library}

Para obtener los mejores resultados, Adobe recomienda utilizar la biblioteca Rasterizer de Adobe PDF para los siguientes archivos:

* Archivos PDF pesados y con gran contenido
* Archivos AI con miniaturas no generados de forma predeterminada
* Para archivos AI con colores SPOT (PMS)

Las miniaturas y previsualizaciones que se generan con el rasterizador de PDF son de mejor calidad en comparación con la salida de rasterizado lista para usar. La biblioteca Rasterizer de Adobe PDF no admite conversión de espacio de color. Independientemente del espacio de color del archivo PDF de origen, Adobe PDF Rasterizer solo genera salida RGB.

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobe recomienda usar [!DNL Adobe InDesign Server] para extraer representaciones [!DNL Adobe InDesign]específicas, como IDML y HTML. Para obtener más información, consulte [Añadir recursos de Experience Manager como referencias en Adobe InDesign](/help/assets/managing-linked-subassets.md#refai).

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media] genera y ofrece múltiples variaciones de contenido enriquecido en tiempo real a través de su red global, escalable y optimizada para el rendimiento. Ofrece experiencias de visualización interactivas y optimiza el proceso de gestión de la campaña digital. Para obtener más información sobre cómo habilitar [!DNL Dynamic Media], consulte [Configuración de Dynamic Media](/help/assets/config-dynamic.md).

Actualmente, [!DNL Dynamic Media] puede admitir vídeos de hasta 15 GB de contenido por archivo.

## Biblioteca ImageMagick {#imagemagick-library}

Adobe recomienda utilizar la biblioteca ImageMagick en los siguientes casos:

* Para generar representaciones en miniatura para archivos EPS.
* Para conservar la información del perfil de la imagen.
* Para preservar la transparencia.
* Para procesar archivos PSD y PSB.

Para saber cómo configurar la [!DNL ImageMagick] biblioteca en [!DNL Experience Manager], consulte [Uso de ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick). Para obtener un uso óptimo, consulte [Prácticas recomendadas para configurar ImageMagick](/help/assets/best-practices-for-imagemagick.md).

## Biblioteca de transcodificación de imágenes {#image-transcoding-library}

La biblioteca de transcodificación de imágenes de Adobe es una solución de procesamiento de imágenes que realiza funciones básicas de gestión de imágenes, como codificación, transcodificación, remuestreo, cambio de tamaño, etc.

La biblioteca de transcodificación de imágenes admite los siguientes tipos MIME:

* JPG/JPEG
* PNG (8 y 16 bits)
* GIF
* BMP
* TIFF/TIFF comprimido (excepto Tiffs de 32 bits y PTiffs).
* ICO
* ICN

Para obtener más información, consulte Biblioteca [de transcodificación de imágenes](/help/assets/imaging-transcoding-library.md).
