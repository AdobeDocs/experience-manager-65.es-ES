---
title: Formatos de archivo compatibles y tipos MIME
description: Formatos de archivo y tipos MIME admitidos por [!DNL Assets] y [!DNL Dynamic Media] y las funciones compatibles con cada formato.
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: Asset Management,Renditions
exl-id: a4bcf67b-54f4-4681-9e42-fd4753acde1a
hide: true
source-git-commit: c1878d6aadba9c795168459dbd5f09abfe0fc327
workflow-type: tm+mt
source-wordcount: '1751'
ht-degree: 10%

---

# Formatos admitidos en [!DNL Adobe Experience Manager Assets] {#assets-supported-formats}

[!DNL Experience Manager Assets] admite una amplia gama de formatos de archivo y cada funcionalidad tiene compatibilidad variada con distintos tipos de MIME. Para integrar [!DNL Assets] con otras soluciones de administración de activos digitales (DAM) compatibles con los estándares y software de escritorio, utilice el [!DNL Extensible Metadata Platform] XMP.

Utilice la leyenda para comprender el nivel de compatibilidad.

| Nivel de soporte | Descripción |
| :-----------: | ------------------------------ |
| ✓ | Compatibilidad |
| &#42; | Compatible con funciones de complemento |
| − | No aplicable |

## Formatos de imagen de trama compatibles con [!DNL Experience Manager] {#supported-raster-image-formats}

Los formatos de imagen de trama admitidos en [!DNL Assets] son:

| Formato | Almacenamiento | Gestión de metadatos | Extracción de metadatos | Generación de miniaturas | Edición | Reescritura de metadatos | Perspectivas |
| ------------ | :------: | :-----------------: | :-----------------: | :------------------: | :------: | :----------------: | :------: |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| PNM | ✓ | ✓ | − | − | − | − | ✓ |
| PGM | ✓ | ✓ | − | − | − | − | ✓ |
| PBM | ✓ | ✓ | − | − | − | − | ✓ |
| PPM | ✓ | ✓ | − | − | − | − | ✓ |
| PSD ‡ | ✓ | ✓ | ✓ | ✓ | − | − | ✓ |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | − | ✓ | − |
| PICT | − | − | − | − | − | − | ✓ |
| PSB | ✓ | ✓ | ✓ | ✓ | − | − | − |

✓ La imagen combinada se extrae del archivo PSD. Es una imagen que genera Adobe Photoshop y que se incluye en el archivo PSD. Dependiendo de la configuración, la imagen combinada puede ser o no la imagen real.

Además de la información anterior, considere lo siguiente:

* La compatibilidad con archivos EPS se aplica solo a imágenes de trama. Por ejemplo, la generación de miniaturas para imágenes vectoriales de EPS no es compatible de forma predeterminada. Para agregar compatibilidad, [configurar ImageMagick](best-practices-for-imagemagick.md). Para integrar herramientas de terceros para habilitar funciones adicionales, consulte [Controlador de medios basado en líneas de comandos](media-handlers.md#command-line-based-media-handler).

* La reescritura de metadatos funciona para el formato de archivo PSB cuando se agrega al `NComm` controlador.

* Para los archivos EPS, la reescritura de metadatos es compatible con la versión 3.0 o posterior del Convenio de estructura de documentos de PostScript (PS-Adobe).

## Formatos 3D compatibles {#support-3d-formats}

Se admite la siguiente lista de formatos 3D.

Consulte también [Uso de recursos 3D en Dynamic Media.](/help/assets/assets-3d.md)

| Formato | Almacenamiento | Versiones | Flujo de trabajo | Publicación | Control de acceso | Vista previa de miniatura | Vista previa 3D | Entrega de Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ |  | ✓ | ✓ | − | − |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ |  | ✓ | − | ✓ | − |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | − | − | ✓ |

## Biblioteca Rasterizadora de PDF admitida {#supported-pdf-rasterizer-library}

La biblioteca Rasterizer de Adobe PDF genera miniaturas y previsualizaciones de alta calidad para vídeos de gran tamaño y con gran contenido [!DNL Adobe Illustrator] y archivos PDF. Adobe recomienda utilizar la biblioteca PDF Rasterizer para lo siguiente:

* Archivos AI/PDF con gran cantidad de contenido que requieren muchos recursos para su procesamiento.
* Archivos AI/PDF para los que no se generan miniaturas de forma predeterminada.
* Archivos AI con colores del sistema de coincidencia de Pantone (PMS).

Consulte [Uso del rasterizador del PDF](aem-pdf-rasterizer.md).

## Biblioteca de transcodificación de imágenes admitida {#supported-image-transcoding-library}

La biblioteca de transcodificación de imágenes de Adobe es una solución de procesamiento de imágenes que realiza funciones básicas de gestión de imágenes, como codificación, transcodificación, remuestreo y cambio de tamaño.

La biblioteca de transcodificación de imágenes admite los tipos MIME JPG/JPEG, PNG (8 y 16 bits), GIF, BMP, TIFF/comprimido (excepto los archivos TIFF de 32 bits y los archivos PTIFF), ICO e ICN.

Consulte [Biblioteca de transcodificación de imágenes](imaging-transcoding-library.md).

## Admitido Camera Raw {#supported-camera-raw}

La variable [!DNL Adobe Camera Raw] biblioteca habilita [!DNL Assets] para ingerir imágenes sin procesar. Consulte [compatibilidad Camera Raw](camera-raw.md).

## Admitido [!DNL Assets] formatos de documento {#supported-document-formats}

Los formatos de documento admitidos para las funciones de administración de recursos son los siguientes:

| Formato | Almacenamiento | [Gestión de metadatos](metadata.md) | Texto completo<br> extracción | [Extracción de metadatos](metadata.md) | Miniatura<br> generación | [Extracción de subconjunto](managing-linked-subassets.md) | [Reescritura de metadatos](xmp-writeback.md) | [Recursos conectados](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|---|---|---|---|---|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ | − |
| DOC | ✓ | ✓ | ✓ | ✓ | − | − | − | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | − | − | − | ✓ |
| ODT | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| RTF | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| TXT | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| XLS | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | − | − | − | ✓ |
| ODS | ✓ | ✓ | ✓ | − | − | − | − | − |
| PPT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| ODP | ✓ | ✓ | ✓ | − | − | − | − | − |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ | − |
| PS | ✓ | ✓ | − | − | − | − | − | − |
| QXP | ✓ | ✓ | − | − | − | − | − | − |
| ePub | ✓ | ✓ | − | ✓ | ✓ | − | − | − |

## Formatos multimedia compatibles {#supported-multimedia-formats}

|  | Almacenamiento | Gestión de metadatos | Extracción de metadatos | Generación de miniaturas | Transcodificación FFmpeg |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ | − | − | &#42; |
| MIDI | ✓ | ✓ | − | − | &#42; |
| 3GP | ✓ | ✓ | − | − | &#42; |
| MP3 | ✓ | ✓ | ✓ | − | &#42; |
| MPG | ✓ | ✓ | − | − | &#42; |
| OGA | ✓ | ✓ | − | − | &#42; |
| OGG | ✓ | ✓ | − | − | &#42; |
| RA | ✓ | ✓ | − | − | &#42; |
| WAV | ✓ | ✓ | − | − | &#42; |
| WMA | ✓ | ✓ | − | − | &#42; |
| DVI | ✓ | ✓ | − | &#42; | &#42; |
| FLV | ✓ | ✓ | − | &#42; | &#42; |
| M4V | ✓ | ✓ | − | &#42; | &#42; |
| MPEG | ✓ | ✓ | − | &#42; | &#42; |
| OGV | ✓ | ✓ | − | &#42; | &#42; |
| MOV | ✓ | ✓ | − | &#42; | &#42; |
| WMV | ✓ | ✓ | − | &#42; | &#42; |
| SWF | ✓ | ✓ | − | − | − |

## Formatos de archivo compatibles {#supported-archive-formats}

Los formatos de archivo compatibles y la aplicabilidad de los flujos de trabajo DAM comunes se tratan en la siguiente tabla.

| Formatos | Almacenamiento | Versiones | Flujo de trabajo | Publicación | Control de acceso | Entrega en Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| ZIP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## Otros formatos admitidos {#other-supported-formats}

A continuación se describe la aplicabilidad de las funcionalidades habituales de DAM para algunos formatos de archivo específicos.

| Formatos | Almacenamiento | Versiones | Flujo de trabajo | Publicación | Control de acceso | Entrega en Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript (cuando se configura con su propio dominio de envío) | − | − | − | − | − | ✓ |

>[!NOTE]
>
>Cargar y distribuir archivos JavaScript puede o no ser seguro. Si es necesario, puede utilizar superposiciones para evitar que los usuarios carguen archivos JS.

## Tipos MIME admitidos {#supported-mime-types}

De forma predeterminada, [!DNL Experience Manager] detecta el tipo de archivo con la extensión de archivo . [!DNL Experience Manager] puede detectarlo a partir del contenido de los archivos. Para este último, seleccione [!UICONTROL Detectar MIME del contenido] en [!UICONTROL Servicio Day CQ DAM Mime Type] en el [!DNL Experience Manager] Consola web.

Una lista de tipos MIME admitidos está disponible en CRXDE Lite en `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`.

| Extensión de archivo | Tipo MIME/ Tipo de medio de Internet | Valor predeterminado de jobParam | Valor de jobParam permitido |
|---|---|---|---|
| Imagen | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | El jobParam predeterminado se aplica a todos los recursos de tipo MIME de imagen.<ul><li>[knockoutBackgroundOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-knockout-background-options.html)</li><li>[manualCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-manual-crop-options.html)</li><li>[autoColorCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-color-crop-options.html)</li><li>[autoTransparentCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-transparent-crop-options.html)</li><li>[colorManagementOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-color-management-options.html)</li><li>[autoSetCreationOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-set-creation-options.html)</li><li>[emailSetting](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/sting-constants/r-email-settings.html)</li><li>[xmpKeywords](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-xmp-keywords.html)</li><li>[unSharpMaskOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-unsharp-mask-options.html)</li></ul> |
| 3G2 | video/3gpp2 |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| 3GP | video/3gpp |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| AAC | audio/x-aac |  |  |
| AFM | application/x-font-type1 |  |  |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li> [illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html)</li></ul> |
| AIFF | audio/x-aiff |  |  |
| AVI | video/x-msvideo |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| BMP | image/bmp |  |  |
| CSS | text/css |  |  |
| DOC | application/msword |  |  |
| EPS | <ul><li>application/postscript</li><li>aplicación/eps</li><li>application/x-eps</li><li>image/eps</li><li>image/x-eps</li></ul> |  |  |
| F4V | video/x-f4v |  | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash |  |  |
| FLV | video/x-flv |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| FPX | image/vnd.fpx |  |  |
| GIF | image/gif |  |  |
| ICC | application/vnd.iccprofile |  |  |
| ICM | application/vnd.iccprofile |  |  |
| INDD | application/x-indesign |  |  |
| JPEG | image/jpeg |  |  |
| JPG | image/jpeg |  |  |
| M2V | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| M4V | video/x-m4v |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MOV | video/quicktime |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MP3 | audio/mpeg |  |  |
| MP4 | video/mp4 |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPEG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MTS | model/vnd.mts |  |  |
| OGV | video/ogg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| OTF | application/x-font-otf |  |  |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdfOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-pdf-options.html) |
| PFB | application/x-font-type1 |  |  |
| PFM | application/x-font-type1 |  |  |
| PICT | image/x-pict |  |  |
| PNG | image/png |  |  |
| PPT | application/vnd.ms-powerpoint |  |  |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li>[illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html)</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-options.html)</li><li>[photoshopLayerOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-layer-options.html)</li></ul> |
| RTF | application/rtf |  |  |
| SVG | image/svg+xml |  |  |
| SWF | application/x-shockwave-flash |  |  |
| TAR | application/x-tar |  |  |
| TIF / TIFF | image/tiff |  |  |
| TTC | application/x-font-ttf |  |  |
| TTF | application/x-font-ttf |  |  |
| VOB | video/dvd |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| VTT | text/vtt |  |  |
| WAV | audio/x-wav |  |  |
| WEBM | video/webm |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| WMA | audio/x-ms-wma |  |  |
| WMV | video/x-ms-wmv |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| XLS | application/vnd.ms-excel |  |  |
| ZIP | application/zip |  |  |

## Dynamic Media: formatos de vídeo de entrada compatibles para la transcodificación {#supported-input-video-formats-for-dynamic-media-transcoding}

| Extensión de archivo de vídeo | Contenedor | Códecs de vídeo recomendados | Códecs de vídeo no compatibles |
|---|---|---|---|
| AVI | Intercalación A/V | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft® Video 1 (MS-CRAM) |
| FLV, F4V | Flash de Adobe | H264/AVC, Flix VP6, H263, Sorenson | SWF (archivos de animación vectoriales) |
| M4V | Apple iTunes | H264/AVC | − |
| MKV | Matroska | H264/AVC | − |
| MOV, QT | QuickTime de Apple | H264/AVC, Apple ProRes422 &amp; HQ, XDCAM de Sony, DVCAM de Sony, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermedio, animación de Apple |
| MP4 | MPEG-4 | H264/AVC (todos los perfiles) | − |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 | − |
| MXF ‡ | MXF | XDCAM de Sony, MPEG-2, MPEG-4, DVCP de Panasonic | − |
| OGV, OGG | Ogg | Theora, VP3, Dirac | − |
| WebM | WebM | Google VP8 | − |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Pantalla Microsoft® (MSS2), Microsoft® Photo Story (WVP2) |

✓ Este formato de vídeo aún no es compatible para su uso con vídeos interactivos en Dynamic Media o con anotaciones en Experience Manager Assets.

## Dynamic Media: formatos de documento compatibles {#supported-document-formats-dynamic-media}

| Formato | Cargar<br> (Formato de entrada) | Crear<br> image<br> ajuste preestablecido<br> (Formato de salida) | Vista previa<br> dinámico<br> representación | Entrega<br> dinámico<br> representación | Descargar<br> dinámico<br> representación |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | − | − | − | − |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | − | − | − | − |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) (Consulte la nota siguiente) | ✓ | ✓ | ✓ | ✓ | ✓ |

>[!NOTE]
>
>Para PDF seguros, solo se admite Cargar .

Además de la funcionalidad anterior, considere lo siguiente:

* Para utilizar Dynamic Media para generar representaciones dinámicas para archivos PDF, consulte [Formatos de archivo Adobe Illustrator (AI), Postscript (EPS) y PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Para utilizar Dynamic Media para obtener una vista previa y generar representaciones dinámicas para archivos AI, consulte [Formatos de archivo Adobe Illustrator (AI), Postscript (EPS) y PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Para utilizar Dynamic Media para generar representaciones dinámicas para archivos INDD, consulte [Formato del archivo InDesign (INDD)](../assets/managing-image-presets.md#indesign-indd-file-format).

## Dynamic Media: formatos de imagen de trama compatibles {#supported-raster-image-formats-dynamic-media}

| Formato | Cargar<br> (Formato de entrada) | Crear<br> image<br> ajuste preestablecido<br> (Formato de salida) | Vista previa<br> dinámico<br> representación | Entrega<br> dinámico<br> representación | Descargar<br> dinámico<br> representación | Establecer tipos compatibles con este formato |
|---|:---:|:---:|:---:|:---:|:---:| --- |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | [Imagen](/help/assets/image-sets.md), [Medios mixtos](/help/assets/mixed-media-sets.md)y [Giro](/help/assets/spin-sets.md) |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | [Imagen](/help/assets/image-sets.md), [Medios mixtos](/help/assets/mixed-media-sets.md)y [Giro](/help/assets/spin-sets.md) |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | [Imagen](/help/assets/image-sets.md), [Medios mixtos](/help/assets/mixed-media-sets.md)y [Giro](/help/assets/spin-sets.md) |
| BMP | ✓ | − | − | − | − | [Imagen](/help/assets/image-sets.md), [Medios mixtos](/help/assets/mixed-media-sets.md)y [Giro](/help/assets/spin-sets.md) |
| PSD ‡ | ✓ | − | − | − | − | − |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| PICT | ✓ | − | − | − | − | − |

✓ La imagen combinada se extrae del archivo PSD. Es una imagen que genera Adobe Photoshop y que se incluye en el archivo PSD. Dependiendo de la configuración, la imagen combinada puede ser o no la imagen real.

* La compatibilidad con archivos EPS se aplica solo a imágenes de trama. Por ejemplo, la generación de miniaturas para imágenes vectoriales de EPS no es compatible de forma predeterminada. Para agregar compatibilidad, [configurar ImageMagick](best-practices-for-imagemagick.md). Para integrar herramientas de terceros para habilitar funciones adicionales, consulte [Controlador de medios basado en líneas de comandos](media-handlers.md#command-line-based-media-handler).

* Para usar [!DNL Dynamic Media] para obtener una vista previa y generar representaciones dinámicas para archivos EPS, consulte [Formatos de archivo Adobe Illustrator (AI), Postscript (EPS) y PDF.](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Para los archivos EPS, la reescritura de metadatos es compatible con la versión 3.0 o posterior del Convenio de estructura de documentos de PostScript (PS-Adobe).

## Dynamic Media: formatos de imagen de trama no compatibles {#unsupported-image-formats-dynamic-media}

La siguiente lista describe los subtipos de formatos de archivo de imagen de trama que se *not* compatible con Dynamic Media.

Consulte también [Detectar formatos de archivo no compatibles para Dynamic Media](https://helpx.adobe.com/experience-manager/kb/detect-unsupported-assets-for-dynamic-media.html) Artículo de la Base de conocimiento.

* Los archivos PNG que tienen un tamaño de fragmento IDAT tienen un tamaño bueno de más de 100 MB.
* Archivos PSB.
* Los archivos PSD con un espacio de color distinto de CMYK, RGB, escala de grises o mapa de bits no son compatibles. Los espacios de color DuoTone, Lab e Indexed no son compatibles.
* archivos PSD con una profundidad buena superior a 16.
* archivos TIFF que tienen datos de coma flotante.
* Archivos TIFF que tienen espacio de color Lab.

<!-- Topic commented out for now as of March 31, 2020. The topic may still need adjustment so it can be published live, or it may be moved into a KB article instead. Just waiting on feedback in CQDOC-15657. - Rick
## Unsupported raster image formats in Dynamic Media (#unsupported-image-formats-dynamic-media)

The following table describes the sub-types of raster image formats that are *not* supported in Dynamic Media. The table also describes suggested methods you can use to detect such files.

| Format | What is unsupported? | Suggested detection method |
|---|---|---|
| JPEG  | Files where the initial three bytes is incorrect. | To identify a JPEG file, its initial three bytes must be `ff d8 ff`. If they are anything else, then it is not classified as a JPEG.<br>&bull; There is no software tool that can help with this issue.<br>&bull; A small C++/java program which reads the initial three bytes of a file should be able to detect these types of files.<br>&bull; It may be better to track the source of such files and look at the tool generating the file. |
| PNG |  Files that have an IDAT chunk size greater than 100 MB. | You can detect this issue using [libpng](https://www.libpng.org/pub/png/libpng.html) in C++. |
| PSB |  | Use exiftool if the file type is PSB.<br>Example in an ExifTool log:<br>1. File type: `PSB` |
| PSD | Files with a color space other than CMYK, RGB, Grayscale, or Bitmap are not supported.<br>DuoTone, Lab, and Indexed color spaces are not supported. | Use ExifTool if Color mode is Duotone.<br>Example in an ExifTool log:<br>1. Color mode: `Duotone` |
|  | Files with abrupt endings. | Adobe is unable to detect this condition. Also, such files cannot be opened with Adobe PhotoShop. Adobe suggests you examine the tool that was used to create such a file and troubleshoot at the source. |
|  | Files that have a bit depth greater than 16. | Use ExifTool if the bit depth is greater than 16.<br>Example in an ExifTool log:<br>1. Bit depth: `32` |
|  | File that have Lab color space. | Use exiftool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
| TIFF | Files that have floating point data. That is, a TIFF file with 32-bit depth is not supported. | Use ExifTool if the MIME type is `image/tiff` and the SampleFormat has `Float` in its value. Example in an ExifTool log:<br>1. MIME type: `image/tiff`<br>Sample format: `Float #`<br>2. MIME type: `image/tiff`<br>Sample format: `Float; Float; Float; Float` |
|  | Files that have Lab color space. | Use ExifTool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
-->

## Dynamic Media: formatos 3D compatibles {#supported-three-d-file-formats-in-dm}

Dynamic Media admite los siguientes formatos 3D.

Consulte también [Uso de recursos 3D en Dynamic Media](/help/assets/assets-3d.md).

| Extensión de archivo 3D | Formato del archivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmisión binaria de GL | model/gltf-binary | Incluye los materiales y texturas como un único recurso. |
| OBJ | Archivo de objeto 3D WaveFront | application/x-tgif |  |
| STL | Esteroolitografía | application/vnd.ms-pki.stl |  |
| USDZ | Archivo zip de descripción de escena universal | model/vnd.usdz+zip | *Compatibilidad únicamente con la ingesta; no hay visualización ni interacción disponibles.* USDZ es un formato 3D propietario que los dispositivos Safari y iOS pueden visualizar de forma nativa. |

>[!MORELIKETHIS]
>
>* [Habilite la compatibilidad con los parámetros de trabajo de carga de recursos basados en tipos MIME y Dynamic Media Classic](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).
>* [Configuración de la compatibilidad con los parámetros de trabajo de carga basada en tipos MIME](config-dynamic.md).

