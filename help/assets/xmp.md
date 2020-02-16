---
title: Compatibilidad con metadatos XMP en Recursos AEM
description: Obtenga información sobre el estándar de metadatos XMP (Extensible Metadata Platform) utilizado por AEM Assets para la gestión de metadatos. XMP proporciona un formato estándar para la creación, el procesamiento y el intercambio de metadatos para una amplia variedad de aplicaciones.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Metadatos XMP {#xmp-metadata}

XMP (Extensible Metadata Platform) es el estándar de metadatos utilizado por AEM Assets para la gestión de todos los metadatos. XMP proporciona un formato estándar para la creación, el procesamiento y el intercambio de metadatos para una amplia variedad de aplicaciones.

Además de ofrecer codificación de metadatos universales que se puede incrustar en todos los formatos de archivo, XMP proporciona un modelo [de](xmp.md#xmp-core-concepts) contenido enriquecido y es [compatible con Adobe](xmp.md#advantages-of-xmp) y otras empresas, de modo que los usuarios de XMP en combinación con Recursos AEM tienen una plataforma sólida sobre la que construir.

La especificación [](https://www.adobe.com/devnet/xmp.html) XMP está disponible en Adobe.

## ¿Qué es XMP? {#what-is-xmp}

AEM Assets es compatible de forma nativa con XMP, la plataforma de metadatos extensible encabezada por Adobe. XMP es un estándar para procesar y almacenar metadatos estandarizados y propietarios en activos digitales. XMP está diseñado para ser el estándar común que permite que varias aplicaciones funcionen eficazmente con metadatos.

Los profesionales de la producción, por ejemplo, utilizan la compatibilidad integrada con XMP en las aplicaciones de Adobe para pasar información a través de varios formatos de archivo. El repositorio de AEM Assets extrae los metadatos XMP y los utiliza para administrar el ciclo de vida del contenido y ofrece la posibilidad de crear flujos de trabajo de automatización.

XMP estandariza cómo se definen, crean y procesan los metadatos proporcionando un modelo de datos, un modelo de almacenamiento y esquemas. Todos estos conceptos se tratan en esta sección.

Todos los metadatos heredados de EXIF, ID3 o Microsoft Office se traducen automáticamente a XMP, que se pueden ampliar para admitir esquemas de metadatos específicos del cliente, como catálogos de productos.

Los metadatos en XMP constan de un conjunto de propiedades. Estas propiedades siempre están asociadas a una entidad concreta denominada recurso; es decir, las propiedades son &quot;acerca&quot; del recurso. En el caso de XMP, el recurso es siempre el recurso.

### Adobe {#adobe}

Adobe introdujo por primera vez el estándar XMP como parte del producto de software Adobe Acrobat. Desde entonces, el estándar XMP ha sido ampliamente adoptado.

### Ecosistema XMP {#xmp-ecosystem}

XMP define un modelo de [metadatos](https://en.wikipedia.org/wiki/Metadata) que se puede utilizar con cualquier conjunto definido de elementos de metadatos. XMP también define [esquemas](https://en.wikipedia.org/wiki/XML_schema) específicos para propiedades básicas útiles para registrar el historial de un recurso a medida que pasa por varios pasos de procesamiento, desde ser fotografiado, [escaneado](https://en.wikipedia.org/wiki/Image_scanner)o creado como texto, pasando por pasos de edición fotográfica (como [recorte](https://en.wikipedia.org/wiki/Cropping_%28image%29) o ajuste de color), hasta ensamblarse en una imagen final. XMP permite a cada programa o dispositivo de software añadir su propia información a un recurso digital, que se puede retener en el archivo digital final.

XMP se serializa y almacena con mayor frecuencia mediante un subconjunto del [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF), que a su vez se expresa en [XML](https://en.wikipedia.org/wiki/XML).

## Ventajas de XMP {#advantages-of-xmp}

XMP tiene las siguientes ventajas con respecto a otros esquemas y estándares de codificación:

* Los metadatos basados en XMP son muy potentes y detallados.
* XMP permite tener varios valores para una propiedad.
* XMP tiene codificación estandarizada, lo que le permite intercambiar fácilmente metadatos.
* XMP es extensible. Puede agregar información adicional a los recursos.

### Extensible {#extensible}

El estándar XMP está diseñado para ser extensible, lo que le permite agregar tipos personalizados de metadatos a los datos XMP. EXIF, por otro lado, no tiene - tiene una lista fija de propiedades que no puede ampliarse.

>[!NOTE]
>
>XMP generalmente no permite incrustar tipos de datos binarios. Para cargar datos binarios en XMP, por ejemplo, imágenes en miniatura, deben codificarse en un formato compatible con XML, como `Base64`.

## Conceptos principales XMP {#xmp-core-concepts}

Las siguientes secciones describen los conceptos principales de XMP, incluidos espacios de nombres y esquemas, propiedades y valores, y alternativas de idioma.

### Espacios de nombres y esquemas {#namespaces-and-schemata}

Un esquema XMP es un conjunto de nombres de propiedades en un espacio de nombres XML común que incluye el tipo de datos y la información descriptiva. Un esquema XMP se identifica mediante su URI de espacio de nombres XML. El uso de espacios de nombres evita conflictos entre propiedades en distintos esquemas que tienen el mismo nombre pero un significado diferente.

Por ejemplo, la `Creator` propiedad de dos esquemas diseñados de forma independiente puede significar la persona que creó el recurso o bien la aplicación que lo creó (por ejemplo, Adobe Photoshop).

### Propiedades y valores {#properties-and-values}

XMP puede incluir propiedades de uno o varios esquemas.

Por ejemplo, un subconjunto típico utilizado por muchas aplicaciones de Adobe puede incluir lo siguiente:

* Esquema central de Dublín: dc:title, dc:creator, dc:subject, dc:format, dc:rights
* Esquema básico XMP: xmp:CreateDate, xmp:CreatorTool, xmp:ModifyDate, xmp:metadataDate
* Esquema de administración de derechos XMP: xmpRights:WebStatement, xmpRights:Marked
* Esquema de administración de medios XMP: xmpMM:DocumentID

### Alternativas de idioma {#language-alternatives}

XMP le permite agregar una `xml:lang` propiedad a las propiedades de texto para especificar el idioma del texto.
