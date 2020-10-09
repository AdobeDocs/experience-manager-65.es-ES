---
title: Administre los metadatos de sus recursos digitales en [!DNL Adobe Experience Manager].
description: Obtenga información sobre los tipos de metadatos y [!DNL Adobe Experience Manager Assets] helps manage metadata for assets to allow easier categorization and organization of assets. [!DNL Experience Manager] cómo pueden organizarse y procesarse automáticamente los recursos en función de sus metadatos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 117208c634613559bb13556e12f094add70006e2
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 0%

---


# Gestión de metadatos de los recursos digitales {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] guarda los metadatos de cada recurso. Permite una clasificación y organización más sencillas de los recursos y ayuda a las personas que buscan un recurso específico. Con la capacidad de extraer metadatos de los archivos cargados en [!DNL Experience Manager Assets], la administración de metadatos se integra con el flujo de trabajo creativo. Con la capacidad de mantener y administrar metadatos con sus recursos, puede organizar y procesar automáticamente recursos en función de sus metadatos.

* [Metadatos XMP](xmp.md).
* [Cómo editar o agregar metadatos](meta-edit.md).
* [Referencia](meta-ref.md)de esquemas de metadatos.

<!--  TBD: Complete this section. Take help from Metadata IRD for DDAM. Also, look at metadata features in Forrester analysis.

## Understand metadata handling in Experience Manager {#metadata-possibilities-with-aem}

Describe the journey of an assets' metadata. What all happens to metadata when an asset is added to Experience Manager.

## Add metadata to your digital assets {#add-metadata}

Typically, the applications that create digital assets add some metadata to the assets created. Before uploading an asset to Experience Manager, you can edit and modify metadata using either the native application used to create an asset or using some metadata editors. When you upload an asset to Experience Manager, the metadata is processed.

## Metadata of assets, folders, and collections {#metadata-of-assets-folders-collections}

## Modify metadata of an asset, folder, or collection {#modify-metadata}

## Modify metadata in bulk {#modify-metadata-in-bulk}

[!DNL Adobe Enterprise Manager Assets] lets you edit the metadata of multiple assets simultaneously so you can quickly propagate common metadata changes to assets in bulk. You can also edit the metadata for multiple collections in bulk.

Use the properties page to perform metadata changes on multiple assets or collections:

* Change metadata properties to a common value
* Add or modify tags

To customize the metadata properties page, including adding, modifying, deleting metadata properties, use the schema editor.

>[!NOTE]
>
>The bulk editing methods work for assets available in a folder or a collection. For the assets that are available across folders or match a common criteria, it is possible to [bulk update the metadata after searching](search-assets.md#metadataupdates).

1. In the [!DNL Assets] user interface, navigate to the location of the assets you want to edit.
1. Select the assets for which you want to edit common properties.
1. From the toolbar, click **[!UICONTROL Properties]** to open the properties page for the selected assets.

   >[!NOTE]
   >
   >When you select multiple assets, the lowest common parent form is selected for the assets. In other words, the properties page only displays metadata fields that are common across the properties pages of all the individual assets.

1. Modify the metadata properties for selected assets under the various tabs.
1. To view the metadata editor for a specific asset, deselect the remaining assets in the list. The metadata editor fields are populated with the metadata for the particular asset.

   >[!NOTE]
   >
   >* In the properties page, you can remove assets from the asset list by deselecting them. The asset list has all the assets selected by default. The metadata for assets that you remove from the list is not updated.
   >* At the top of assets list, select the check box near **[!UICONTROL Title]** to toggle between selecting the assets and clearing the list.

1. To select a different metadata schema for the assets, click **[!UICONTROL Settings]** from the toolbar, and select the desired schema.
1. Save the changes.
1. To append the new metadata with the existing metadata in fields that contain multiple values, select **[!UICONTROL Append mode]**. If you do not select this option, the new metadata replaces the existing metadata in the fields. click **[!UICONTROL Submit]**.

   >[!CAUTION]
   >
   >For single-value fields, the new metadata is not appended to the existing value in the field even if you select **[!UICONTROL Append mode]**.

## Configure limit for bulk metadata update {#limit-bulk-metadata-updates}

To prevent DOS like situation, Enterprise Manager limits the number of parameters supported in a Sling request. When updating metadata of many assets in one go, you may reach the limit and the metadata does not get updated for more assets. Enterprise Manager generates the following warning in the logs:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

To change the limit, access **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** and change the value of **[!UICONTROL Maximum POST Parameters]** in **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi configuration.

-->

## Por qué necesitamos metadatos {#why-we-need-metadata}

Metadatos significa datos sobre los datos. A este respecto, los datos hacen referencia a su recurso digital, por ejemplo una imagen. Los metadatos son fundamentales para una administración eficaz de los recursos.

Los metadatos son la recopilación de todos los datos disponibles para un recurso, pero no necesariamente están contenidos en esa imagen. Algunos ejemplos de metadatos son:

* Nombre del recurso.
* Hora y fecha de la última modificación.
* Tamaño del recurso tal como se almacenó en el repositorio.
* Nombre de la carpeta en la que está contenido.
* Recursos relacionados o etiquetas aplicadas.

Lo anterior son las propiedades básicas de metadatos que [!DNL Experience Manager] pueden administrarse para los recursos, lo que permite a los usuarios ver todos los recursos. Por ejemplo, ordenar los recursos por fecha de la última modificación resulta útil cuando se intenta descubrir los recursos agregados recientemente.

Puede agregar más datos de alto nivel a recursos digitales, por ejemplo:

* Tipo de recurso (¿es una imagen, un vídeo, un clip de audio o un documento?).
* Propietario del recurso.
* Título del recurso.
* Descripción del recurso.
* Etiquetas asignadas a un recurso.

Más metadatos le ayudan a categorizar los recursos y resulta útil a medida que crece la cantidad de información digital. Es posible administrar unos cientos de archivos basándose únicamente en los nombres de archivo. Sin embargo, este enfoque no es escalable. Se queda corto cuando aumenta el número de personas involucradas y el número de activos gestionados.

Con la adición de metadatos, el valor de un recurso digital aumenta, ya que el recurso se convierte en

* Más accesible: los sistemas y usuarios pueden encontrarlo fácilmente.
* Más fácil de administrar: puede encontrar recursos con el mismo conjunto de propiedades más fácilmente y aplicarles cambios.
* Completado: el recurso ofrece más información y contexto con más metadatos.

Por estas razones, [!DNL Assets] le proporciona los medios adecuados para crear, administrar e intercambiar metadatos para sus recursos digitales.

## Tipos de metadatos {#types-of-metadata}

Los dos tipos básicos de metadatos son los metadatos técnicos y los descriptivos.

Los metadatos técnicos son útiles para las aplicaciones de software que se ocupan de activos digitales y no deben mantenerse manualmente. [!DNL Experience Manager Assets] y otro software determina automáticamente los metadatos técnicos y los metadatos pueden cambiar cuando se modifica el recurso. Los metadatos técnicos disponibles de un recurso dependen en gran medida del tipo de archivo del recurso. Algunos ejemplos de metadatos técnicos son:

* Tamaño de un archivo.
* Dimension (altura y anchura) de una imagen.
* Velocidad de bits de un archivo de audio o vídeo.
* Resolución (nivel de detalle) de una imagen.

Los metadatos descriptivos son metadatos relacionados con el dominio de la aplicación, por ejemplo, el negocio del que proviene un recurso. Los metadatos descriptivos no se pueden determinar automáticamente. Se crea de forma manual o semiautomática. Por ejemplo, una cámara con GPS puede rastrear automáticamente la latitud y la longitud y añadir la etiqueta geográfica de la imagen.

El costo de crear manualmente información descriptiva de metadatos es alto. Por lo tanto, se establecen normas para facilitar el intercambio de metadatos entre sistemas y organizaciones de software. [!DNL Experience Manager Assets] admite todas las normas pertinentes para la gestión de metadatos.

## Normas de codificación {#encoding-standards}

Existen varias formas de incrustar metadatos en los archivos. Se admite una selección de estándares de codificación:

* XMP: utilizado por [!DNL Assets] para almacenar los metadatos extraídos en el repositorio.
* ID3: para archivos de audio y vídeo.
* Exif: para archivos de imagen.
* Otro/Heredado: desde [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel], etc.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP) es un estándar abierto que se utiliza [!DNL Experience Manager Assets] para toda la administración de metadatos. El estándar oferta la codificación de metadatos universales que puede incrustarse en todos los formatos de archivo. Adobe y otras compañías admiten XMP estándar ya que proporciona un modelo de contenido enriquecido. Los usuarios de XMP estándar y de [!DNL Experience Manager Assets] tienen una poderosa plataforma sobre la que construir. For more information, see [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

Los datos almacenados en estas etiquetas ID3 se muestran cuando se reproduce un archivo de audio digital en el equipo o en un reproductor portátil MP3.

Las etiquetas ID3 están diseñadas para el formato de archivo MP3. Información adicional sobre los formatos:

* Las etiquetas ID3 funcionan en archivos MP3 y mp3PRO.
* WAV no tiene etiquetas.
* WMA tiene etiquetas de propiedad que no permiten la implementación de código abierto.
* Ogg Vorbis utiliza Comentarios Xiph incrustados en el contenedor Ogg.
* AAC utiliza un formato de etiquetado propio.

### Exif {#exif}

El formato de archivo de imagen intercambiable (Exif) es el formato de metadatos más utilizado en la fotografía digital. Proporciona una forma de incrustar un vocabulario fijo de propiedades de metadatos en muchos formatos de archivo, como JPEG, TIFF, RIFF y WAV. Exif almacena los metadatos como pares de un nombre de metadatos y un valor de metadatos. Estos pares de metadatos nombre-valor-valor también se denominan etiquetas, por lo que no deben confundirse con el etiquetado de [!DNL Experience Manager]. Las cámaras digitales modernas crean metadatos Exif y el software de gráficos moderno lo admite. El formato Exif es el denominador común más bajo para la administración de metadatos, especialmente para imágenes.

Una limitación importante de Exif es que algunos formatos de archivo de imagen populares como BMP, GIF o PNG no lo admiten.

Los campos de metadatos definidos por Exif suelen ser de naturaleza técnica y tienen un uso limitado para la administración descriptiva de metadatos. Por este motivo, [!DNL Experience Manager Assets] oferta la asignación de propiedades Exif en esquemas [de metadatos](metadata-schemas.md) comunes y en [XMP](xmp-writeback.md).

### Otros metadatos {#other-metadata}

Otros metadatos que se pueden incrustar desde archivos son [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel], etc.

## Esquemas de metadatos {#metadata-schemata}

Los esquemas de metadatos son conjuntos predefinidos de definiciones de propiedades de metadatos que se pueden utilizar en varias aplicaciones. Las propiedades siempre están asociadas a un recurso, lo que significa que las propiedades están &quot;cerca&quot; del recurso.

También puede diseñar sus propios esquemas de metadatos si no existe ninguno que satisfaga sus necesidades. No duplicado la información existente. Dentro de una organización, la separación de esquemas facilita el uso compartido de metadatos. [!DNL Experience Manager] proporciona una lista predeterminada de los esquemas de metadatos más populares. La lista le ayuda a poner en marcha la estrategia de metadatos y a elegir rápidamente las propiedades de metadatos que necesita.

A continuación se enumeran los esquemas de metadatos admitidos.

### Metadatos estándar {#standard-metadata}

* DC - [!DNL Dublin Core] es un conjunto de metadatos importante y ampliamente utilizado.
* DICOM - Imágenes digitales y comunicaciones en medicina.
* `Iptc4xmpCore` y `iptc4xmpExt` - International Press Communications Standard contiene muchos metadatos específicos de cada asunto.
* RDF - Marco de descripción de recursos - para metadatos web semánticos genéricos.
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ` - Entradas de trabajo básicas.

### Metadatos específicos de la aplicación {#application-specific-metadata}

Los metadatos específicos de la aplicación incluyen metadatos técnicos y descriptivos. Si utiliza estos metadatos, es posible que otras aplicaciones no puedan utilizarlos. Por ejemplo, es posible que una aplicación de procesamiento de imágenes diferente no pueda acceder a [!DNL Adobe Photoshop] los metadatos. Puede crear un paso de flujo de trabajo que cambie una propiedad específica de la aplicación a una propiedad estándar.

* ACDSee: metadatos administrados por el [!DNL ACDSee] programa. Consulte [www.acdsee.com/](https://www.acdsee.com/).
* Álbum - [!DNL Adobe Photoshop Album].
* CQ - Utilizado por [!DNL Experience Manager Assets].
* DAM - Utilizado por [!DNL Experience Manager Assets].
* DEX - [Optima SC Description explorer](http://www.optimasc.com/products/dex/index.html) es una colección de herramientas para la administración de metadatos y archivos para sistemas operativos Windows.
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhoto y MP - Microsoft Photo.
* PDF y PDF/X.
* Photoshop y psAux - [!DNL Adobe Photoshop].

### Metadatos de Digital Rights Management {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights].
* PLUS - Sistema [universal de licencias de](https://www.useplus.com)imágenes.
* PRISM: requisitos de [publicación para metadatos](https://www.idealliance.org/prism-metadata)estándar del sector.
* PRL - lenguaje de derechos PRISM.
* PUR - Derechos de uso de PRISM.
* `xmpPlus` - Integración de PLUS con XMP.

### Metadatos específicos de la fotografía {#photography-specific-metadata}

* Exif - Información técnica de la cámara, incluyendo la posición GPS.
* CRS - [!DNL Camera Raw] esquema.
* `iptc4xmpCore` y `iptc4xmpExt`.
* TIFF: metadatos de imagen (no solo para imágenes TIFF).

### Metadatos específicos de impresión {#print-specific-metadata}

* PDF y PDF/X: Adobe PDF y aplicaciones de terceros.
* PRISM: requisitos de [publicación para metadatos](https://www.idealliance.org/prism-metadata/)estándar del sector.
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG` - XMP metadatos para texto paginado.

### Metadatos específicos de multimedia {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM` - Administración de medios.

## Flujos de trabajo impulsados por metadatos {#metadata-driven-workflows}

La creación de flujos de trabajo basados en metadatos le ayuda a automatizar algunos procesos, lo que mejora la eficacia. En un flujo de trabajo basado en metadatos, el sistema de administración de flujo de trabajo lee el flujo de trabajo y, como resultado, realiza alguna acción predefinida. Por ejemplo, algunas de las formas en que puede utilizar flujos de trabajo basados en metadatos:

* El flujo de trabajo puede comprobar si una imagen tiene un título o no. Si no lo hace, el sistema notifica que se debe agregar un título.
* El flujo de trabajo puede comprobar si un aviso de copyright de un recurso permite la distribución o no. Por lo tanto, el sistema envía el recurso a un servidor o al otro.
* Un flujo de trabajo puede buscar recursos sin metadatos predefinidos y obligatorios ni recursos con metadatos *no válidos* .

>[!MORELIKETHIS]
>
>* [Editar propiedades de metadatos de varias colecciones](managing-collections-touch-ui.md#editing-collection-metadata-in-bulk)
>* [Metadatos XMP](xmp.md).
>* [Cómo editar o agregar metadatos](meta-edit.md).
>* [Referencia](meta-ref.md)de esquemas de metadatos.

