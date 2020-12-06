---
title: Conceptos de metadatos
description: Obtenga información sobre la necesidad y los tipos de metadatos que facilitan la categorización y organización de los recursos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: adeb20c1e7222e7c5702061cba73350002f5154c
workflow-type: tm+mt
source-wordcount: '2731'
ht-degree: 6%

---


# Comprender los conceptos de metadatos {#why-we-need-metadata}

Metadatos significa datos sobre los datos. A este respecto, los datos hacen referencia a su recurso digital, por ejemplo una imagen. Los metadatos son fundamentales para una administración eficaz de los recursos.

Los metadatos son la recopilación de todos los datos disponibles para un recurso, pero no necesariamente están contenidos en esa imagen. Algunos ejemplos de metadatos son:

* Nombre del recurso.
* Hora y fecha de la última modificación.
* Tamaño del recurso tal como se almacenó en el repositorio.
* Nombre de la carpeta en la que está contenido.
* Recursos relacionados o etiquetas aplicadas.

Lo anterior son las propiedades básicas de metadatos que [!DNL Experience Manager] puede administrar para los recursos, lo que permite a los usuarios ver todos los recursos. Por ejemplo, ordenar los recursos por fecha de la última modificación resulta útil cuando se intenta descubrir los recursos agregados recientemente.

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

## Estándares de codificación {#encoding-standards}

Existen varias formas de incrustar metadatos en los archivos. Se admite una selección de estándares de codificación:

* XMP: utilizado por [!DNL Assets] para almacenar los metadatos extraídos en el repositorio.
* ID3: para archivos de audio y vídeo.
* Exif: para archivos de imagen.
* Otro/Heredado: desde [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel], etc.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP) es un estándar abierto que se utiliza  [!DNL Experience Manager Assets] para toda la administración de metadatos. El estándar oferta la codificación de metadatos universales que puede incrustarse en todos los formatos de archivo. Adobe y otras compañías admiten XMP estándar ya que proporciona un modelo de contenido enriquecido. Los usuarios de XMP estándar y de [!DNL Experience Manager Assets] tienen una poderosa plataforma sobre la que construir. Para obtener más información, consulte [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

Los datos almacenados en estas etiquetas ID3 se muestran cuando se reproduce un archivo de audio digital en el equipo o en un reproductor portátil MP3.

Las etiquetas ID3 están diseñadas para el formato de archivo MP3. Información adicional sobre los formatos:

* Las etiquetas ID3 funcionan en archivos MP3 y mp3PRO.
* WAV no tiene etiquetas.
* WMA tiene etiquetas de propiedad que no permiten la implementación de código abierto.
* Ogg Vorbis utiliza Comentarios Xiph incrustados en el contenedor Ogg.
* AAC utiliza un formato de etiquetado propio.

### Exif {#exif}

El formato de archivo de imagen intercambiable (Exif) es el formato de metadatos más utilizado en la fotografía digital. Proporciona una forma de incrustar un vocabulario fijo de propiedades de metadatos en muchos formatos de archivo, como JPEG, TIFF, RIFF y WAV. Exif almacena los metadatos como pares de un nombre de metadatos y un valor de metadatos. Estos pares de metadatos nombre-valor-valor también se denominan etiquetas, no se deben confundir con el etiquetado de [!DNL Experience Manager]. Las cámaras digitales modernas crean metadatos Exif y el software de gráficos moderno lo admite. El formato Exif es el denominador común más bajo para la administración de metadatos, especialmente para imágenes.

Una limitación importante de Exif es que algunos formatos de archivo de imagen populares como BMP, GIF o PNG no lo admiten.

Los campos de metadatos definidos por Exif suelen ser de naturaleza técnica y tienen un uso limitado para la administración descriptiva de metadatos. Por este motivo, [!DNL Experience Manager Assets] oferta la asignación de propiedades Exif en [esquemas de metadatos comunes](metadata-schemas.md) y en [XMP](xmp-writeback.md).

### Otros metadatos {#other-metadata}

Otros metadatos que se pueden incrustar desde archivos son [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel], etc.

## Comprender los esquemas de metadatos {#metadata-schemata}

Los esquemas de metadatos son conjuntos predefinidos de definiciones de propiedades de metadatos que se pueden utilizar en varias aplicaciones. Las propiedades siempre están asociadas a un recurso, lo que significa que las propiedades están &quot;cerca&quot; del recurso.

También puede diseñar sus propios esquemas de metadatos si no existe ninguno que satisfaga sus necesidades. No duplicado la información existente. Dentro de una organización, la separación de esquemas facilita el uso compartido de metadatos. [!DNL Experience Manager] proporciona una lista predeterminada de los esquemas de metadatos más populares. La lista le ayuda a poner en marcha la estrategia de metadatos y a elegir rápidamente las propiedades de metadatos que necesita.

A continuación se enumeran los esquemas de metadatos admitidos.

### Metadatos estándar {#standard-metadata}

* DC: [!DNL Dublin Core] es un conjunto de metadatos importante y ampliamente utilizado.
* DICOM - Imágenes digitales y comunicaciones en medicina.
* `Iptc4xmpCore` y  `iptc4xmpExt` - International Press Communications Standard contiene muchos metadatos específicos del tema.
* RDF - Marco de descripción de recursos - para metadatos web semánticos genéricos.
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ` - Entradas de trabajo básicas.

### Metadatos específicos de la aplicación {#application-specific-metadata}

Los metadatos específicos de la aplicación incluyen metadatos técnicos y descriptivos. Si utiliza estos metadatos, es posible que otras aplicaciones no puedan utilizarlos. Por ejemplo, es posible que una aplicación de procesamiento de imágenes diferente no pueda acceder a los metadatos [!DNL Adobe Photoshop]. Puede crear un paso de flujo de trabajo que cambie una propiedad específica de la aplicación a una propiedad estándar.

* ACDSee: metadatos administrados por el programa [!DNL ACDSee]. Consulte [www.acdsee.com/](https://www.acdsee.com/).
* Álbum: [!DNL Adobe Photoshop Album].
* CQ - Utilizado por [!DNL Experience Manager Assets].
* DAM - Utilizado por [!DNL Experience Manager Assets].
* DEX - [Optima SC Description explorer](http://www.optimasc.com/products/dex/index.html) es una colección de herramientas para la administración de archivos y metadatos para sistemas operativos Windows.
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhoto y MP - Microsoft Photo.
* PDF y PDF/X.
* Photoshop y psAux: [!DNL Adobe Photoshop].

### Metadatos de Digital Rights Management (DRM) {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights].
* PLUS: [Sistema universal de licencias de imágenes](https://www.useplus.com).
* PRISM - [Requisitos de publicación para metadatos estándar del sector](https://www.idealliance.org/prism-metadata).
* PRL - lenguaje de derechos PRISM.
* PUR - Derechos de uso de PRISM.
* `xmpPlus` - Integración de PLUS con XMP.

### Metadatos específicos de la fotografía {#photography-specific-metadata}

* Exif - Información técnica de la cámara, incluyendo la posición GPS.
* CRS: esquema [!DNL Camera Raw].
* `iptc4xmpCore` y `iptc4xmpExt`.
* TIFF: metadatos de imagen (no solo para imágenes TIFF).

### Metadatos específicos de impresión {#print-specific-metadata}

* PDF y PDF/X: Adobe PDF y aplicaciones de terceros.
* PRISM - [Requisitos de publicación para metadatos estándar del sector](https://www.idealliance.org/prism-metadata).
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG` - XMP metadatos para texto paginado.

### Metadatos específicos de multimedia {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM` - Administración de medios.

## Referencia de esquemas de metadatos {#metadata-schemata-reference}

La siguiente referencia incluye información sobre un esquema de metadatos concreto (en orden alfabético), así como una lista de las propiedades y sus definiciones.

### Dublin Core {#dublin-core}

Los metadatos de Dublin Core proporcionan un conjunto estandarizado de convenciones para describir los recursos y facilitar su búsqueda. En [!DNL Assets], Dublin Core describe los recursos digitales, incluidos vídeo, sonido, imágenes y documentos.

El conjunto de elementos de metadatos básico de Dublín (DCMES) simple contiene 15 elementos de metadatos como se muestra en la tabla siguiente. Cada elemento Dublin Core es opcional y se puede repetir. Puede agregar o eliminar información de metadatos de Dublin Core como lo haría con metadatos específicos de tipo de medios.

Además del DCMES, hay otros elementos de metadatos creados por la Iniciativa Dublin Core. Consulte la [iniciativa Dublin Core](https://dublincore.org/) para obtener más información.

| Propiedad | Descripción |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| colaborador | Persona o compañía responsable de contribuir al contenido. |
| cobertura | Ubicación geográfica o período de tiempo que cubre el activo. |
| creador | Persona o compañía responsable de la creación del contenido. |
| date | Fecha o período de tiempo asociados al activo. |
| Descripción | Más información sobre el recurso. |
| format | Formato de archivo, medio físico o dimensiones del recurso. [!DNL Experience Manager] se utiliza  `dc:format` para denotar el tipo MIME del recurso. |
| identifier | Una referencia única al recurso. |
| language | El idioma del recurso (por ejemplo, `en` para inglés). |
| publisher | Persona o compañía responsable de la disponibilidad del recurso. |
| relation | Un recurso relacionado. |
| derechos | Información sobre quién tiene los derechos de este recurso. |
| source | Recurso relacionado del que se deriva el activo. |
| subject | Tema del recurso. |
| el título | Un nombre para el recurso. |
| tipo | La naturaleza o el género del recurso. |

### IPTC {#iptc}

El Consejo Internacional de Telecomunicaciones de Prensa (IPTC) es un consorcio de agencias de noticias de todo el mundo - uno de sus objetivos es desarrollar y mantener estándares técnicos. El IPTC definió un conjunto de estándares de metadatos de fotos para imágenes que son casi universalmente aceptados por los fotógrafos. Estas normas de metadatos formaban parte de la norma más amplia conocida como el Modelo de Intercambio de Información IPTC (IIM) creado en los años noventa.

Aunque la información del encabezado IPTC ha sido reemplazada mayormente por XMP, un esquema central IPTC y un esquema de extensión están disponibles para XMP. En los programas de imagen, las propiedades XMP e IPTC están sincronizadas.

## Flujos de trabajo basados en metadatos {#metadata-driven-workflows}

La creación de flujos de trabajo basados en metadatos le ayuda a automatizar algunos procesos, lo que mejora la eficacia. En un flujo de trabajo basado en metadatos, el sistema de administración de flujo de trabajo lee el flujo de trabajo y, como resultado, realiza alguna acción predefinida. Por ejemplo, algunas de las formas en que puede utilizar flujos de trabajo basados en metadatos:

* El flujo de trabajo puede comprobar si una imagen tiene un título o no. Si no lo hace, el sistema notifica que se debe agregar un título.
* El flujo de trabajo puede comprobar si un aviso de copyright de un recurso permite la distribución o no. Por lo tanto, el sistema envía el recurso a un servidor o al otro.
* Un flujo de trabajo puede buscar recursos sin metadatos predefinidos y obligatorios ni recursos con metadatos *no válidos*.

## Metadatos XMP {#xmp-metadata}

XMP (Extensible Metadata Platform) es el estándar de metadatos utilizado por [!DNL Adobe Experience Manager Assets] para toda la administración de metadatos. XMP proporciona un formato estándar para la creación, el procesamiento y el intercambio de metadatos para una amplia variedad de aplicaciones.

Además de ofrecer codificación de metadatos universales que se puede incrustar en todos los formatos de archivo, XMP ofrece un [modelo de contenido enriquecido](#xmp-core-concepts) y [es compatible con Adobe](#advantages-of-xmp) y otras compañías, de modo que los usuarios de XMP en combinación con [!DNL Assets] tienen una poderosa plataforma sobre la que construir.

La [especificación de XMP](https://www.adobe.com/devnet/xmp.html) está disponible en Adobe.

### ¿Qué es XMP? {#what-is-xmp}

Adobe introdujo por primera vez el estándar XMP como parte del producto de software Adobe Acrobat. Desde entonces, la norma XMP ha sido ampliamente adoptada. [!DNL Assets] nativamente admite el XMP: la plataforma de metadatos extensible encabezada por el Adobe. XMP es un estándar para procesar y almacenar metadatos estandarizados y propietarios en activos digitales. XMP está diseñado para ser el estándar común que permite que varias aplicaciones funcionen eficazmente con metadatos.

Los profesionales de la producción, por ejemplo, utilizan la compatibilidad de XMP integrada en las aplicaciones de Adobe para pasar información a través de varios formatos de archivo. [!DNL Assets] extrae los metadatos XMP y los utiliza para administrar el ciclo de vida del contenido y oferta la capacidad de crear flujos de trabajo de automatización.

XMP estandariza la forma en que se definen, crean y procesan los metadatos proporcionando un modelo de datos, un modelo de almacenamiento y esquemas. Todos estos conceptos se tratan en esta sección.

Todos los metadatos heredados de EXIF, ID3 o Microsoft Office se traducen automáticamente a XMP, lo que se puede ampliar para admitir el esquema de metadatos específico del cliente, como catálogos de productos.

Los metadatos de XMP constan de un conjunto de propiedades. Estas propiedades siempre están asociadas con un
entidad concreta denominada recurso; es decir, las propiedades son &quot;acerca&quot; del recurso. En el caso de XMP, el recurso es siempre el recurso.

### ecosistema XMP {#xmp-ecosystem}

XMP define un modelo de [metadatos](https://es.wikipedia.org/wiki/Metadatos) que se puede utilizar con cualquier conjunto definido de elementos de metadatos. XMP también define [esquemas](https://en.wikipedia.org/wiki/XML_schema) específicos para propiedades básicas útiles para registrar el historial de un recurso a medida que pasa por varios pasos de procesamiento, desde ser fotografiado, [escaneado](https://es.wikipedia.org/wiki/Esc%C3%A1ner_inform%C3%A1tico) o creado como texto, pasando por etapas de edición fotográfica (como [recorte](https://en.wikipedia.org/wiki/Cropping_%28image%29) o ajuste de color), hasta ensamblarse en una imagen final. XMP permite a cada programa o dispositivo de software añadir su propia información a un recurso digital, que se puede retener en el archivo digital final.

XMP se serializa y almacena con mayor frecuencia mediante un subconjunto del [W3C](https://es.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF), que a su vez se expresa en [XML](https://en.wikipedia.org/wiki/XML).

### Ventajas de XMP {#advantages-of-xmp}

XMP tiene las siguientes ventajas con respecto a otros esquemas y estándares de codificación:

* Los metadatos basados en XMP son muy potentes y detallados.
* XMP permite tener varios valores para una propiedad.
* XMP cuenta con codificación estandarizada, lo que le permite intercambiar fácilmente metadatos.
* XMP es extensible. Puede agregar información adicional a los recursos.

El XMP estándar está diseñado para ser extensible, lo que le permite agregar tipos personalizados de metadatos a los datos XMP. EXIF, por otro lado, no - tiene una lista fija de propiedades que no puede ampliarse.

>[!NOTE]
>
>XMP generalmente no permite incrustar tipos de datos binarios. Para cargar datos binarios en XMP, por ejemplo, imágenes en miniatura, deben codificarse en un formato compatible con XML como `Base64`.

### Conceptos de XMP {#xmp-core-concepts}

En las secciones siguientes se describen los conceptos básicos de XMP, incluidas Áreas de nombres y esquemas, propiedades y valores, y alternativas de idioma.

#### Áreas de nombres y esquemas {#namespaces-and-schemata}

Un esquema XMP es un conjunto de nombres de propiedades en una Área de nombres XML común que incluye
el tipo de datos y la información descriptiva. Un esquema de XMP se identifica mediante su URI de Área de nombres XML. El uso de Áreas de nombres evita conflictos entre propiedades en diferentes esquemas que tienen el mismo nombre pero un significado diferente.

Por ejemplo, la propiedad `Creator` de dos esquemas de diseño independiente puede significar la persona que creó el recurso o bien la aplicación que lo creó (por ejemplo, Adobe Photoshop).

#### Propiedades y valores {#properties-and-values}

XMP pueden incluir propiedades de uno o varios de los esquemas. Por ejemplo, un subconjunto típico utilizado por muchas aplicaciones Adobe puede incluir lo siguiente:

* Esquema central de Dublín: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`.
* XMP esquema básico: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`.
* esquema de gestión de derechos de XMP: `xmpRights:WebStatement`, `xmpRights:Marked`.
* esquema de administración de medios XMP: `xmpMM:DocumentID`.

#### Alternativas de idioma {#language-alternatives}

XMP permite agregar una propiedad `xml:lang` a las propiedades de texto para especificar el idioma del texto.

## Trabajar con metadatos IPTC {#support-for-iptc-metadata}

Descubra cómo [!DNL Adobe Experience Manager Assets] admite los metadatos IPTC, las clasificaciones creativas y las palabras clave agregadas a los recursos a través de [!DNL Adobe Bridge] y otras aplicaciones [!DNL Adobe Creative Cloud].

[!DNL Adobe Experience Manager Assets] admite el estándar de metadatos IPTC que se utiliza ampliamente para describir recursos. De esta manera, [!DNL Assets] mejora la aceptación de sus imágenes entre diversas partes, incluyendo fotógrafos, agencias creativas, bibliotecas, museos, etc.

El esquema de metadatos predeterminado para los recursos ahora incorpora los esquemas de metadatos IPTC Core y IPTC Extension para definir propiedades de metadatos completas que permiten a los usuarios agregar datos precisos y fiables sobre las personas, ubicaciones y productos que se muestran en una imagen. También admite fechas, nombres e identificadores relacionados con la creación de la imagen, y una forma flexible de expresar información sobre derechos.

La página Propiedades de los recursos ahora incluye fichas independientes para mostrar los metadatos IPTC Core y Extensión IPTC en campos editables.

1. En la interfaz de usuario [!DNL Assets], seleccione una imagen.
1. Haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas.
1. Haga clic en la ficha **[!UICONTROL IPTC]** para vista de los metadatos IPTC del recurso.
1. Edite las propiedades de metadatos IPTC, según sea necesario.

   ![iptc_tab](assets/keywords-in-iptc-tab.png)

1. Haga clic en la ficha **[!UICONTROL Extensión IPTC]** para vista de metadatos de extensión IPTC para el recurso.
1. Edite las propiedades de metadatos de IPTC Extension, según sea necesario.
1. Haga clic en **[!UICONTROL Guardar y cerrar]** para guardar los cambios.

### Compatibilidad con la clasificación creativa {#creative-rating-support}

Además de mostrar clasificaciones de usuarios individuales y clasificaciones acumuladas, la página Propiedades ahora muestra las clasificaciones asignadas a los recursos a través de Adobe Bridge y otras aplicaciones creativas

Estas clasificaciones están disponibles en la sección **[!UICONTROL Clasificación creativa]** de la pestaña **[!UICONTROL Avanzado]**.

Esta clasificación es una propiedad de sólo lectura e incluye entre 1 y 5. Puede buscar recursos en función de su clasificación creativa en el panel de búsqueda.

Sin embargo, esta propiedad no está indizada actualmente para evitar conflictos con los cambios personalizados realizados por los usuarios.

### Compatibilidad con palabras clave {#keyword-support}

La ficha **[!UICONTROL IPTC]** de la página [!UICONTROL Propiedades] también muestra las palabras clave agregadas a los recursos a través de Adobe Bridge y otras aplicaciones de Adobe Creative Cloud. También puede editar estas palabras clave y agregar más palabras clave desde la ficha **[!UICONTROL IPTC]**.

![keywords](assets/keywords-in-iptc-tab.png)
