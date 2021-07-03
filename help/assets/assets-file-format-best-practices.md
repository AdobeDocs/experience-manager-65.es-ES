---
title: Prácticas recomendadas para procesar los formatos de archivo admitidos
description: Prácticas recomendadas para procesar los distintos tipos de archivos admitidos con [!DNL Experience Manager Assets].
contentOwner: AG
role: Admin
feature: Administración de recursos,Herramientas para desarrolladores
exl-id: da080f12-4cf7-4c26-901b-cd40d9c00bcb
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Prácticas recomendadas del formato de los archivos de recursos {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] admite muchas bibliotecas de formato de archivos propietarias y de terceros para satisfacer los diversos requisitos de compatibilidad de archivos de los usuarios. Las bibliotecas de Adobe admitidas son [!DNL Adobe Camera Raw], Gibson, Adobe PDF Rasterizer y [!DNL Adobe InDesign Server]. Además, [!DNL Experience Manager Assets] admite bibliotecas de terceros, incluidas [!DNL ImageMagick], [!DNL TwelveMonkeys], etc.

Para ver los formatos de archivo compatibles, consulte [Formatos compatibles con Assets](/help/assets/assets-formats.md).

>[!TIP]
>
>Si utiliza [!DNL Experience Manager] en Adobe Managed Services (AMS), póngase en contacto con el Servicio de atención al cliente de Adobe si tiene previsto procesar muchos archivos PSD o PSB de gran tamaño. Trabaje con el representante del Servicio de atención al cliente de Adobe para implementar estas prácticas recomendadas para su implementación de AMS y elegir las mejores herramientas y modelos posibles para los formatos propietarios de Adobe. [!DNL Experience Manager] es posible que no procese archivos PSB de alta resolución que superen los 30000 x 23000 píxeles.

## [!DNL Adobe Camera Raw] biblioteca {#adobe-camera-raw-library}

Para obtener un rendimiento óptimo, Adobe recomienda utilizar la biblioteca [!DNL Adobe Camera Raw] para archivos RAW y DNG.

[!DNL Adobe Camera Raw] la biblioteca de admite el perfil de color CMYK como entrada. Sin embargo, genera la salida en espacio de color RGB y sólo admite la salida en formato JPEG. No conserva el espacio de color del archivo de origen (por ejemplo, CMYK) en las miniaturas.

Para obtener más información, consulte [Soporte Camera Raw](/help/assets/camera-raw.md).

## Biblioteca Adobe PDF Rasterizer {#adobe-pdf-rasterizer-library}

Para obtener mejores resultados, Adobe recomienda utilizar la biblioteca Adobe PDF Rasterizer para los siguientes archivos:

* Archivos PDF pesados y con gran contenido
* Los archivos AI con miniaturas no se generan de forma predeterminada
* Para archivos AI con colores SPOT (PMS)

Las miniaturas y vistas previas generadas con el rasterizador de PDF son de mejor calidad en comparación con los resultados de raster predeterminados. La biblioteca Adobe PDF Rasterizer no admite ninguna conversión de espacio de color. Independientemente del espacio de color del archivo PDF de origen, Adobe PDF Rasterizer genera solo salida RGB.

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobe recomienda utilizar [!DNL Adobe InDesign Server] para extraer [!DNL Adobe InDesign] representaciones específicas, como IDML y HTML. Para obtener más información, consulte [Adición de recursos de Experience Manager como referencias en Adobe InDesign](/help/assets/managing-linked-subassets.md#refai).

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media] genera y ofrece múltiples variaciones de contenido enriquecido en tiempo real a través de su red global, escalable y optimizada para el rendimiento. Proporciona experiencias de visualización interactivas y optimiza el proceso de administración de campañas digitales. Para obtener más información sobre cómo habilitar [!DNL Dynamic Media], consulte [Configuración de Dynamic Media](/help/assets/config-dynamic.md).

Actualmente, [!DNL Dynamic Media] puede admitir vídeos de hasta 15 GB de contenido por archivo.

## Biblioteca ImageMagick {#imagemagick-library}

Adobe recomienda utilizar la biblioteca ImageMagick en los siguientes escenarios:

* Para generar representaciones en miniatura de archivos EPS.
* Para conservar la información del perfil de la imagen.
* Para preservar la transparencia.
* Para procesar archivos PSD y PSB.

Para saber cómo configurar la biblioteca [!DNL ImageMagick] en [!DNL Experience Manager], consulte [Uso de ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick). Para obtener un uso óptimo, consulte [Prácticas recomendadas para configurar ImageMagick](/help/assets/best-practices-for-imagemagick.md).

## Biblioteca de transcodificación de imágenes {#image-transcoding-library}

La biblioteca de transcodificación de imágenes de Adobe es una solución de procesamiento de imágenes que realiza funciones básicas de gestión de imágenes, como codificación, transcodificación, remuestreo, cambio de tamaño, etc.

La biblioteca de transcodificación de imágenes admite los siguientes tipos de MIME:

* JPG/JPEG
* PNG (8 bits y 16 bits)
* GIF
* BMP
* TIFF/TIFF comprimido (excepto Tiffs de 32 bits y PTiffs).
* ICO
* ICN

Para obtener más información, consulte [Biblioteca de transcodificación de imágenes](/help/assets/imaging-transcoding-library.md).
