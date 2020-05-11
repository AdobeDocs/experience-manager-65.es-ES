---
title: Formatos de archivo admitidos para procesamiento en [!DNL Adobe Experience Manager Assets].
description: Formatos de archivo y tipos MIME admitidos [!DNL Assets] and [!DNL Dynamic Media] por y las características admitidas para cada formato.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 138c8d960ad8c1de20212b7aeebbda0a486832ee
workflow-type: tm+mt
source-wordcount: '1779'
ht-degree: 9%

---


# Formatos admitidos en [!DNL Adobe Experience Manager Assets] {#assets-supported-formats}

[!DNL Experience Manager Assets] admite una amplia gama de formatos de archivo y cada funcionalidad admite distintos tipos MIME. Para integrarse [!DNL Assets] con otras soluciones de administración de activos digitales (DAM) compatibles con estándares y software de escritorio, utilice Adobe [!DNL Extensible Metadata Platform] (XMP).

Utilice la leyenda para comprender el nivel de asistencia.

| Nivel de asistencia | Descripción |
| :-----------: | ------------------------------ |
| ✓ | Compatible |
| * | Compatible con funciones de complemento |
| − | No aplicable |

## Formatos de imagen rasterizada admitidos [!DNL Experience Manager] {#supported-raster-image-formats}

Los formatos de imagen rasterizada admitidos en [!DNL Assets] :

| Formato | Almacenamiento | Gestión de metadatos | Extracción de metadatos | Generación de miniaturas | Edición | Reescritura de metadatos | Perspectivas |
| ------------ | :------: | :-----------------: | :-----------------: | :------------------: | :------: | :----------------: | :------: |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| PNM | ✓ | ✓ |  |  |  |  | ✓ |
| PGM | ✓ | ✓ |  |  |  |  | ✓ |
| PBM | ✓ | ✓ |  |  |  |  | ✓ |
| PPM | ✓ | ✓ |  |  |  |  | ✓ |
| PSD* | ✓ | ✓ | ✓ | ✓ |  |  | ✓ |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ |  | ✓ |  |
| PICT |  |  |  |  |  |  | ✓ |
| PSB | ✓ | ✓ | ✓ | ✓ |  |  |  |

† La imagen combinada se extrae del archivo PSD. Se trata de una imagen generada por Adobe Photoshop y incluida en el archivo PSD. Según la configuración, la imagen combinada puede ser o no la imagen real.

Los formatos de imagen rasterizada admitidos en [!DNL Dynamic Media] :

| Formato | Cargar<br> (formato de entrada) | Creación<br> de ajustes preestablecidos<br> de imagen<br> (formato de salida) | Representación dinámica<br> de Previsualización<br> | Entregar<br> representación dinámica<br> | Descargar<br> representación dinámica<br> |
|---|:---:|:---:|:---:|:---:|:---:|
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ |  |  |  |  |
| PSD* | ✓ |  |  |  |  |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ |
| PICT | ✓ |  |  |  |  |

† La imagen combinada se extrae del archivo PSD. Se trata de una imagen generada por Adobe Photoshop y incluida en el archivo PSD. Según la configuración, la imagen combinada puede ser o no la imagen real.

Además de la información anterior, considere lo siguiente:

* La compatibilidad con archivos EPS se aplica solo a imágenes rasterizadas. Por ejemplo, la generación de miniaturas para imágenes vectoriales EPS no es compatible de forma predeterminada. Para agregar compatibilidad, [configure ImageMagick](best-practices-for-imagemagick.md). Para integrar herramientas de terceros para habilitar funciones adicionales, consulte Controlador de medios basado en la línea [de comandos](media-handlers.md#command-line-based-media-handler).

* La reescritura de metadatos funciona para el formato de archivo PSB cuando se agrega al `NComm` controlador.

* Para utilizar [!DNL Dynamic Media] la previsualización y generación de representaciones dinámicas para archivos EPS, consulte los formatos de archivo [Adobe Illustrator (AI), Postscript (EPS) y PDF.](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Para archivos EPS, la reescritura de metadatos se admite en la versión 3.0 o posterior del Convenio de estructura de Documento PostScript (PS-Adobe).

## Formatos de imagen rasterizada no admitidos en Dynamic Media {#unsupported-image-formats-dynamic-media}

La siguiente lista describe los subtipos de formatos de archivo de imagen rasterizada que *no son* compatibles con Dynamic Media.

Consulte también [Detección de formatos de archivo no compatibles para Dynamic Media](https://helpx.adobe.com/experience-manager/kb/detect-unsupported-assets-for-dynamic-media.html).

* Archivos PNG con un tamaño de fragmento IDAT bueno de 100 MB.
* Archivos PSB.
* Los archivos PSD con un espacio de color distinto de CMYK, RGB, escala de grises o mapa de bits no son compatibles. No se admiten los espacios de color DuoTone, Lab e Indexed.
* Archivos PSD con una profundidad buena de 16.
* Archivos TIFF que tienen datos de coma flotante.
* Archivos TIFF que tienen espacio de color Lab.

<!-- Topic commented out for now as of March 31, 2020. The topic may still need adjustment so it can be published live, or it may be moved into a KB article instead. Just waiting on feedback in CQDOC-15657. - Rick
## Unsupported raster image formats in Dynamic Media (#unsupported-image-formats-dynamic-media)

The following table describes the sub-types of raster image formats that are *not* supported in Dynamic Media. The table also describes suggested methods you can use to detect such files.

| Format | What is unsupported? | Suggested detection method |
|---|---|---|
| JPEG  | Files where the initial three bytes is incorrect. | To identify a JPEF file, its initial three bytes must be `ff d8 ff`. If they are anything else, then it is not classified as a JPEG.<br>&bull; There is no software tool that can help with this issue.<br>&bull; A small C++/java program which reads the initial three bytes of a file should be able to detect these types of files.<br>&bull; It may be better to track the source of such files and look at the tool generating the file. |
| PNG |  Files that have an IDAT chunk size greater than 100 MB. | You can detect this issue using [libpng](http://www.libpng.org/pub/png/libpng.html) in C++. |
| PSB |  | Use exiftool if the file type is PSB.<br>Example in an ExifTool log:<br>1. File type: `PSB` |
| PSD | Files with a color space other than CMYK, RGB, Grayscale, or Bitmap are not supported.<br>DuoTone, Lab, and Indexed color spaces are not supported. | Use ExifTool if Color mode is Duotone.<br>Example in an ExifTool log:<br>1. Color mode: `Duotone` |
|  | Files with abrupt endings. | Adobe is unable to detect this condition. Also, such files cannot be opened with Adobe PhotoShop. Adobe suggests you examine the tool that was used to create such a file and troubleshoot at the source. |
|  | Files that have a bit depth greater than 16. | Use ExifTool if the bit depth is greater than 16.<br>Example in an ExifTool log:<br>1. Bit depth: `32` |
|  | File that have Lab color space. | Use exiftool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
| TIFF | Files that have floating point data. That is, a TIFF file with 32-bit depth is not supported. | Use ExifTool if the MIME type is `image/tiff` and the SampleFormat has `Float` in its value. Example in an ExifTool log:<br>1. MIME type: `image/tiff`<br>Sample format: `Float #`<br>2. MIME type: `image/tiff`<br>Sample format: `Float; Float; Float; Float` |
|  | Files that have Lab color space. | Use ExifTool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
-->

## Biblioteca de rasterizadores PDF admitida {#supported-pdf-rasterizer-library}

La biblioteca Rasterizer de Adobe PDF genera previsualizaciones y miniaturas de alta calidad para archivos PDF y de Adobe Illustrator grandes y con gran contenido. Adobe recomienda utilizar la biblioteca Rasterizer de PDF para lo siguiente:

* Archivos AI/PDF con gran cantidad de contenido que requieren muchos recursos para procesarlos.
* Archivos AI/PDF para los que no se generan miniaturas de forma predeterminada.
* Archivos AI con colores Pantone Matching System (PMS).

See [Using PDF Rasterizer](aem-pdf-rasterizer.md).

## Biblioteca de transcodificación de imágenes admitida {#supported-image-transcoding-library}

La biblioteca de transcodificación de imágenes de Adobe es una solución de procesamiento de imágenes que realiza funciones básicas de gestión de imágenes como, por ejemplo, codificación, transcodificación, remuestreo y cambio de tamaño.

La biblioteca de transcodificación de imágenes admite los tipos MIME JPG/JPEG, PNG (8 y 16 bits), GIF, BMP, TIFF/Comprimido (excepto los archivos TIFF de 32 bits y PTIFF), ICO e ICN.

Consulte Biblioteca [de transcodificación de imágenes](imaging-transcoding-library.md).

## RAW de cámara compatible {#supported-camera-raw}

La biblioteca de Adobe Camera Raw permite que Recursos AEM ingrese imágenes sin procesar. See [Camera Raw support](camera-raw.md).

## Formatos de documento de recursos admitidos {#supported-document-formats}

Los formatos de Documento admitidos para las funciones de administración de recursos son los siguientes:

| Formato | Almacenamiento | [Gestión de metadatos](metadata.md) | extracción de texto<br> completo | [Extracción de metadatos](metadata.md) | Generación de miniaturas<br> | [extracción de subbase](managing-linked-subassets.md) | [Reescritura de metadatos](xmp-writeback.md) | [Recursos conectados](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|---|---|---|---|---|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ |  |
| DOC | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| ODT | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| RTF | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| TXT | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| XLS | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| ODS | ✓ | ✓ | ✓ |  |  |  |  |  |
| PPT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| ODP | ✓ | ✓ | ✓ |  |  |  |  |  |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ |  |
| PS | ✓ | ✓ |  |  |  |  |  |  |
| QXP | ✓ | ✓ |  |  |  |  |  |  |
| EPUB | ✓ | ✓ |  | ✓ | ✓ |  |  |  |

## Formatos de documento admitidos en Dynamic Media {#supported-document-formats-dynamic-media}

| Formato | Cargar<br> (formato de entrada) | Creación<br> de ajustes preestablecidos<br> de imagen<br> (formato de salida) | Representación dinámica<br> de Previsualización<br> | Entregar<br> representación dinámica<br> | Descargar<br> representación dinámica<br> |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ |  |  |  |  |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ |  |  |  |  |

Además de la funcionalidad anterior, considere lo siguiente:

* Para utilizar Dynamic Media para generar representaciones dinámicas para archivos PDF, consulte los formatos de archivo [Adobe Illustrator (AI), Postscript (EPS) y PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Para utilizar Dynamic Media para previsualización y generar representaciones dinámicas para archivos AI, consulte los formatos de archivo [Adobe Illustrator (AI), Postscript (EPS) y PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Para utilizar Dynamic Media para generar representaciones dinámicas para archivos INDD, consulte Formato [de archivo](../assets/managing-image-presets.md#indesign-indd-file-format)de InDesign (INDD).

## Formatos multimedia admitidos {#supported-multimedia-formats}

|  | Almacenamiento | Gestión de metadatos | Extracción de metadatos | Generación de miniaturas | Transcodificación FFmpeg |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ |  | − | * |
| MIDI | ✓ | ✓ |  | − | * |
| 3GP | ✓ | ✓ |  | − | * |
| MP3 | ✓ | ✓ | ✓ | − | * |
| MPG | ✓ | ✓ |  | − | * |
| OGA | ✓ | ✓ |  | − | * |
| OGG | ✓ | ✓ |  | − | * |
| RA | ✓ | ✓ |  | − | * |
| WAV | ✓ | ✓ |  | − | * |
| WMA | ✓ | ✓ |  | − | * |
| DVI | ✓ | ✓ |  | * | * |
| FLV | ✓ | ✓ |  | * | * |
| M4V | ✓ | ✓ |  | * | * |
| MPEG | ✓ | ✓ |  | * | * |
| OGV | ✓ | ✓ |  | * | * |
| MOV | ✓ | ✓ |  | * | * |
| WMV | ✓ | ✓ |  | * | * |
| SWF | ✓ | ✓ |  |  |  |

## Formatos de vídeo de entrada admitidos en Dynamic Media para la transcodificación {#supported-input-video-formats-for-dynamic-media-transcoding}

| Extensión de archivo de vídeo | Contenedor | Códecs de vídeo recomendados | Códecs de vídeo no compatibles |
|---|---|---|---|
| MP4 | MPEG-4 | H264/AVC (todos los perfiles) |  |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 y HQ, XDCAM de Sony, DVCAM de Sony, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, animación de Apple |
| FLV, F4V | Adobe Flash | H264/AVC, Flix VP6, H263, Sorenson | SWF (archivos de animación vectorial) |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Microsoft Screen (MSS2), Microsoft Photo Story (WVP2) |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 |  |
| M4V | Apple iTunes | H264/AVC |  |
| AVI | Intercalación A/V | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft Video 1 (MS-CRAM) |
| WebM | WebM | Google VP8 |  |
| OGV, OGG | Ogg | Theora, VP3, Dirac |  |
| MXF | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro |  |
| MTS | AVCHD | H264/AVC |  |
| MKV | Matroska | H264/AVC |  |
| R3D, RM | Vídeo rojo sin formato | MJPEG 2000 |  |
| RAM, RM | RealVideo | No admitido | Real G2 (RV20), Real 8 (RV30), Real 10 (RV40) |
| FLAC | Flac nativo | Códec de audio sin pérdida gratuito |  |
| MJ2 | Motion JPEG 2000 | Códec Motion JPEG 2000 |  |

## Formatos de archivo admitidos {#supported-archive-formats}

Los formatos de archivo admitidos y la aplicabilidad de los flujos de trabajo DAM comunes se tratan en la siguiente tabla.

| Formatos | Almacenamiento | Versiones | Flujo de trabajo | Publicación | Control de acceso | Envío de Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| ZIP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## Otros formatos admitidos {#other-supported-formats}

La aplicabilidad de flujos de trabajo DAM comunes para algunos otros formatos de archivo se describe en la tabla siguiente. La funcionalidad habitual de DAM, como almacenamiento, control de versiones, ACL, flujo de trabajo, publicación y administración de metadatos, excepto Dynamic Media Envío, es compatible con todos los archivos.

| Formatos | Almacenamiento | Versiones | Flujo de trabajo | Publicación | Control de acceso | Envío de Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript (cuando se configura con su propio dominio de envío) |  |  |  |  |  | ✓ |

## Supported MIME types {#supported-mime-types}

De forma predeterminada, AEM detecta el tipo de archivo con la extensión. AEM puede detectarlo a partir del contenido de los archivos. Para este último, seleccione [!UICONTROL Detectar MIME de la opción de contenido] en el servicio [!UICONTROL de tipo de MIME de CQ] Day DAM en la consola web de AEM.

Hay una lista de tipos MIME admitidos disponible en CRXDE Lite en `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`.

| Extensión de archivo | Tipo MIME/tipo de medio de Internet | Valor de jobParam predeterminado | Valor de jobParam permitido |
|---|---|---|---|
| Imagen | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | El jobParam predeterminado se aplica a todos los recursos de tipo MIME de imagen.<ul><li>[knockoutBackgroundOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_knockout_background_options.html)</li><li>manualCropOptions</li><li>[autoColorCropOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_auto_color_crop_options)</li><li>[autoTransparentCropOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_auto_transparent_crop_options)</li><li>[colorManagementOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_color_management_options.html)</li><li>[autoSetCreationOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_auto_set_creation_options.html)</li><li>[emailSetting](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/string_constants/index.html?f=r_email_settings)</li><li>[xmpKeywords](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_xmp_keywords)</li><li>[unsharpMaskOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_unsharp_mask_options.html)</li></ul> |
| 3G2 | video/3gpp2 |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| 3GP | video/3gpp |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_exclude_master_video_from_avs) |
| AAC | audio/x-aac |  |  |
| AFM | application/x-font-type1 |  |  |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_post_script_options.html)</li><li> [illustratorOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_illustrator_options.html)</li></ul> |
| AIFF | audio/x-aiff |  |  |
| AVI | video/x-msvideo |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| BMP | image/bmp |  |  |
| CSS | text/css |  |  |
| DOC | application/msword |  |  |
| EPS | <ul><li>application/postscript</li><li>aplicación/pasos</li><li>application/x-eps</li><li>image/eps</li><li>image/x-eps</li></ul> |  |  |
| F4V | video/x-f4v |  | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash |  |  |
| FLV | video/x-flv |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| FPX | image/vnd.fpx |  |  |
| GIF | image/gif |  |  |
| ICC | application/vnd.iccprofile |  |  |
| ICM | application/vnd.iccprofile |  |  |
| INDD | application/x-indesign |  |  |
| JPEG | image/jpeg |  |  |
| JPG | image/jpeg |  |  |
| M2V | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| M4V | video/x-m4v |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MOV | video/quicktime |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MP3 | audio/mpeg |  |  |
| MP4 | video/mp4 |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MPEG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MPG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MTS | model/vnd.mts |  |  |
| OGV | video/ogg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| OTF | application/x-font-otf |  |  |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdfOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_pdf_options) |
| PFB | application/x-font-type1 |  |  |
| PFM | application/x-font-type1 |  |  |
| PICT | image/x-pict |  |  |
| PNG | image/png |  |  |
| PPT | application/vnd.ms-powerpoint |  |  |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_post_script_options)</li><li>[illustratorOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_illustrator_options)</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_photoshop_options)</li><li>[photoshopLayerOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_photoshop_layer_options.html)</li></ul> |
| RTF | application/rtf |  |  |
| SVG | image/svg+xml |  |  |
| SWF | application/x-shockwave-flash |  |  |
| TAR | application/x-tar |  |  |
| TIF/TIFF | image/tiff |  |  |
| TTC | application/x-font-ttf |  |  |
| TTF | application/x-font-ttf |  |  |
| VOB | vídeo/dvd |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| VTT | text/vtt |  |  |
| WAV | audio/x-wav |  |  |
| WEBM | video/webm |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| WMA | audio/x-ms-wma |  |  |
| WMV | video/x-ms-wmv |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| XLS | application/vnd.ms-excel |  |  |
| ZIP | application/zip |  |  |

>[!MORELIKETHIS]
>
>* [Habilite la compatibilidad](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support)con los parámetros de trabajo de carga de recursos basados en tipos MIME/Scene7.
>* [Configure la compatibilidad](config-dynamic.md)de los parámetros de trabajo de carga según el tipo MIME.

