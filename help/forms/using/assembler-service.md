---
title: Uso del servicio de ensamblador
seo-title: Uso del servicio de ensamblador
description: El servicio Ensamblador le permite combinar, reorganizar y aumentar documentos PDF y XDP y obtener información sobre documentos PDF.
seo-description: El servicio Ensamblador le permite combinar, reorganizar y aumentar documentos PDF y XDP y obtener información sobre documentos PDF.
uuid: 1efce50b-2d98-408e-aa43-ac4999de41a8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 6a99042f-79c7-494b-bca0-73f2b5725b58
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c
workflow-type: tm+mt
source-wordcount: '2143'
ht-degree: 0%

---


# Uso del servicio de ensamblador{#using-assembler-service}

El servicio Ensamblador le permite combinar, reorganizar y aumentar documentos PDF y XDP y obtener información sobre documentos PDF. Cada trabajo enviado al servicio de ensamblador incluye un documento XML de descripción de Documento (DDX), documentos de origen y recursos externos (cadenas y gráficos). Para obtener más información sobre el servicio de ensamblador, consulte [Visión general del servicio de ensamblador](../../forms/using/overview-aem-document-services.md#p-assembler-service-p).

Puede utilizar el servicio de ensamblaje para las siguientes operaciones:

## Compilación de documentos PDF {#assemble-pdf-documents}

Puede utilizar el servicio Compilador para montar dos o más documentos PDF en un solo documento PDF o Portfolio PDF. También puede aplicar funciones al documento PDF que ayuden a la navegación o mejoren la seguridad. A continuación se indican algunas de las formas de montar documentos PDF:

### Compilación de un documento PDF simple {#assemble-a-simple-pdf-document}

La siguiente ilustración muestra tres documentos de origen que se están combinando en un solo documento resultante.

![Compilación de un documento PDF sencillo desde varios documentos PDF](assets/as_document_assembly.png)

Compilación de un documento PDF sencillo desde varios documentos PDF

El siguiente ejemplo es un documento DDX sencillo que se utiliza para montar el documento. Especifica los nombres de los documentos de origen utilizados para producir el documento resultante, así como el nombre del documento resultante:

```xml
<PDF result="Doc4">
<PDF source="Doc1"/>
<PDF source="Doc2"/>
<PDF source="Doc3"/>
</PDF>
```

El ensamblado de documento produce un documento resultante que contiene el siguiente contenido y\
características:

* Todo o parte de cada documento de origen
* Todos o parte de los marcadores de cada documento de origen, normalizados para el documento resultante ensamblado
* Otras características adoptadas a partir del documento base (Doc1), incluidos metadatos, etiquetas de página y tamaño de página
* De forma opcional, el documento resultante incluye una tabla de contenido creada a partir de los marcadores en los documentos de origen

### Crear un Portfolio PDF {#create-a-pdf-portfolio}

El servicio Ensamblador puede crear Portfolio PDF que contengan una colección de documentos y una interfaz de usuario independiente. La interfaz se denomina Diseño del Portfolio PDF o navegador del Portfolio PDF (navegador). Los Portfolio PDF amplían la capacidad de los paquetes PDF agregando un navegador, carpetas y páginas de bienvenida. La interfaz puede mejorar la experiencia del usuario aprovechando la cadena de texto localizada, los esquemas de color personalizados y los recursos gráficos. El Portfolio PDF también puede incluir carpetas para organizar los archivos del portafolio.

Cuando el servicio Ensamblador interpreta el siguiente documento DDX, ensambla un Portfolio PDF que incluye un navegador Portfolio PDF y un paquete de dos archivos. El servicio obtiene el navegador de la ubicación especificada por el origen myNavigator. Cambia la combinación de colores predeterminada del navegador a la combinación de colores rosaScheme.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="Untitled 1">
<Portfolio>
<Navigator source="myNavigator"/>
<ColorScheme scheme="pinkScheme"/>
</Portfolio>
<PackageFiles>
<PDF source="sourcePDF1"/>
<PDF source="sourcePDF2"/>
</PackageFiles>
</PDF>
</DDX>
```

### Compilación de documentos cifrados {#assemble-encrypted-documents}

Al montar un documento, también puede codificar el documento PDF con una contraseña. Después de cifrar un documento PDF con una contraseña, el usuario debe especificar la contraseña para la vista del documento PDF en Adobe Reader o Acrobat. Para cifrar un documento PDF con una contraseña, el documento DDX debe contener valores de elementos de codificación que sean necesarios para cifrar un documento PDF.

El servicio de cifrado no tiene que formar parte de la instalación de LiveCycle para cifrar un documento PDF con una contraseña.

Si uno o varios de los documentos de entrada están cifrados, proporcione una contraseña para abrir el documento como parte del DDX.

### Compilación de documentos mediante numeración Bates {#assemble-documents-using-bates-numbering}

Al compilar un documento, puede utilizar la numeración Bates para aplicar un identificador de página único a cada página. Al utilizar la numeración Bates, a cada página del documento (o conjunto de documentos) se le asigna un número que identifica de forma exclusiva la página. Por ejemplo, los documentos de fabricación que contienen información sobre listas de materiales y están asociados con la producción de un conjunto pueden contener un identificador. Un número Bates contiene un valor numérico incrementado secuencialmente y un prefijo y sufijo opcionales. El prefijo + valor numérico + sufijo se denomina patrón bates.

La siguiente ilustración muestra un documento PDF que contiene un identificador único ubicado en el encabezado del documento.

![Un documento PDF que contiene un identificador único ubicado en el encabezado del documento](do-not-localize/as_batesnumber.png)

Un documento PDF que contiene un identificador único ubicado en el encabezado del documento

### Acoplar y montar documentos {#flatten-and-assemble-documents}

Puede utilizar el servicio Ensamblador para transformar un documento PDF interactivo (por ejemplo, un formulario) en un documento PDF no interactivo. Un documento PDF interactivo permite a los usuarios introducir o modificar datos ubicados en los campos del documento PDF. El proceso de transformación de un documento PDF interactivo en un documento PDF no interactivo se denomina acoplamiento. Cuando se acopla un documento PDF, los campos del formulario conservan su aspecto gráfico, pero ya no son interactivos. Un motivo para acoplar un documento PDF es asegurarse de que no se puedan modificar los datos. Además, las secuencias de comandos asociadas a los campos ya no funcionan.

Cuando se crea un documento PDF que se ensambla a partir de documentos PDF interactivos, el servicio Ensamblador acopla dichos formularios antes de ensamblarlos en el documento resultante.

>[!NOTE]
>
>El servicio Ensamblador utiliza el servicio Output para acoplar formularios XFA dinámicos. Si el servicio Ensamblador procesa un DDX que lo requiere para acoplar un formulario dinámico XFA y el servicio Output no está disponible, se genera una excepción. El servicio Ensamblador puede acoplar un formulario Acrobat o un formulario XFA estático sin utilizar el servicio Output.

## Compilación de documentos XDP {#assemble-xdp-documents}

Puede utilizar el servicio Ensamblador para montar varios documentos XDP en un solo documento XDP o en un documento PDF. Para los archivos XDP de origen que incluyen puntos de inserción, puede especificar los fragmentos que desea insertar.

Estas son algunas de las formas en que puede montar documentos XDP:

### Monte un documento XDP simple {#assemble-a-simple-xdp-document}

La siguiente ilustración muestra tres documentos XDP de origen que se están ensamblando en un solo documento XDP resultante. El documento XDP resultante contiene los tres documentos XDP de origen, incluidos los datos asociados. El documento resultante obtiene atributos básicos del documento base, que es el primer documento XDP de origen.

![Compilación de un documento XDP simple a partir de varios documentos XDP](assets/as_assembler_xdpassembly.png)

Compilación de un documento XDP simple a partir de varios documentos XDP

Este es un documento DDX que produce el resultado ilustrado anteriormente.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="MyXDPResult">
<XDP source="sourceXDP1"/>
<XDP source="sourceXDP2"/>
<XDP source="sourceXDP3"/>
</XDP>
</DDX>
```

### Resolviendo referencias durante el ensamblado {#resolving-references-during-assembly}

Normalmente, los documentos XDP pueden contener imágenes a las que se hace referencia mediante referencias absolutas o relativas. El servicio de ensamblador, de forma predeterminada, conserva las referencias a las imágenes en el documento XDP resultante.

Puede especificar el modo en que el servicio Ensamblador gestiona las imágenes a las que se hace referencia en los documentos XDP de origen mediante referencias absolutas o relativas en los archivos XDP al ensamblar. Puede elegir que todas las imágenes estén incrustadas en el resultado para que no contenga referencias relativas o absolutas. Esto se define estableciendo el valor de la etiqueta resolveAssets, que puede tomar cualquiera de las siguientes opciones. De forma predeterminada, no se resuelve ninguna referencia en el documento de resultados.

<table>
 <tbody> 
  <tr> 
   <th>Value</th> 
   <th>Descripción</th> 
  </tr> 
  <tr> 
   <td>ninguno</td> 
   <td>No resuelve ninguna referencia.</td> 
  </tr> 
  <tr> 
   <td>all</td> 
   <td>Incrusta todas las imágenes a las que se hace referencia en el documento XDP de origen.</td> 
  </tr> 
  <tr> 
   <td>relativo</td> 
   <td>Incrusta todas las imágenes a las que se hace referencia mediante referencias relativas en el documento XDP<br /> de origen.</td> 
  </tr> 
  <tr> 
   <td>absoluto</td> 
   <td>Incrusta todas las imágenes a las que se hace referencia mediante referencias absolutas en el documento XDP<br /> de origen.</td> 
  </tr> 
 </tbody> 
</table>

Puede especificar el valor del atributo resolveAssets en la etiqueta de origen XDP o en la etiqueta de resultado XDP principal. Si el atributo se especifica en la etiqueta de resultado XDP, todos los elementos de origen XDP que sean secundarios de un resultado XDP lo heredarán. Sin embargo, si se especifica explícitamente el atributo de un elemento de origen, se anula la configuración del elemento de resultado solo para ese documento de origen.

#### Resolver todas las referencias de origen en un documento XDP {#resolve-all-source-references-in-an-xdp-document}

Para resolver todas las referencias en los documentos XDP de origen, especifique el atributo resolveAssets para el\
documento resultante para todos, como en el ejemplo siguiente:

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="all">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
<XDP source="input3.xdp" />
</XDP>
</DDX
```

También puede especificar el atributo de todos los documentos XDP de origen de forma independiente para obtener el mismo\
resultado.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp">
<XDP source="input1.xdp" resolveAssets="all"/>
<XDP source="input2.xdp" resolveAssets="all"/>
<XDP source="input3.xdp" resolveAssets="all"/>
</XDP>
</DDX>
```

#### Resolver referencias de origen seleccionadas en un documento XDP {#resolve-selected-source-references-in-an-xdp-document}

Puede especificar de forma selectiva las referencias de origen que desea resolver especificando el atributo resolveAssets para ellas. Los atributos de los documentos de origen individuales anulan la configuración del documento XDP resultante. En este ejemplo, los fragmentos incluidos también se resuelven.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="all">
<XDP source="input1.xdp" >
<XDPContent source="fragment.xdp" insertionPoint="MyInsertionPoint"
fragment="myFragment"/>
</XDP>
<XDP source="input2.xdp" />
</XDP>
</DDX>
```

#### Resuelva selectivamente referencias absolutas o relativas {#selectively-resolve-absolute-or-relative-references}

Puede resolver de forma selectiva referencias absolutas o relativas en todos o algunos de los documentos de origen, como se muestra en el ejemplo siguiente:

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="absolute">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
</XDP>
</DDX
```

### Inserte dinámicamente fragmentos de formulario en un formulario XFA {#dynamically-insert-form-fragments-into-an-xfa-form}

Puede utilizar el servicio Ensamblador para crear un formulario XFA creado a partir de otro formulario XFA en el que se insertan fragmentos. Con esta función, puede utilizar fragmentos para crear varios formularios.

La compatibilidad con la inserción dinámica de fragmentos de formulario admite el control de un solo origen. Se mantiene una única fuente de componentes de uso común. Por ejemplo, puede crear un fragmento para la pancarta de compañía. Si la pancarta cambia, solo tiene que modificar el fragmento. Los demás formularios que incluyen el fragmento no cambian.

Los diseñadores de formularios utilizan LiveCycle Designer para crear fragmentos de formulario. Estos fragmentos son subformularios con un nombre exclusivo dentro de un formulario XFA. Los diseñadores de formularios también utilizan Designer para crear formularios XFA con nombres únicos. Usted (el programador) escribe documentos DDX que especifican cómo se insertan los fragmentos en el formulario XFA.

La siguiente ilustración muestra dos formularios XML (plantillas XFA). El formulario de la izquierda contiene un punto de inserción denominado myInsertionPoint. El formulario de la derecha contiene un fragmento denominado myFragment.

![Inserción de fragmentos de formulario en un formulario XFA](assets/as_assembler_fragment_assy_assembled.png)

Inserción de fragmentos de formulario en un formulario XFA

Cuando el servicio Ensamblador interpreta el siguiente documento DDX, crea un formulario XML que contiene otro formulario XML. El subformulario myFragment del documento myFragmentSource se inserta en myInsertionPoint en el documento myFormSource.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="myFormResult">
<XDP source="myFormSource">
<XDPContent fragment="myFragment" insertionPoint="myInsertionPoint"
source="myFragmentSource"/>
</XDP>
</XDP>
</DDX
```

### Empaquetar un documento XDP como PDF {#package-an-xdp-document-as-pdf}

Puede utilizar el servicio Ensamblador para empaquetar un documento XDP como un documento PDF, como se muestra en este documento DDX.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="Untitled 1" encryption="passEncProfile1">
<XDP>
<XDP source="sourceXDP3"/>
<XDP source="sourceXDP4"/>
</XDP>
</PDF>
</DDX>
```

## Desmontar documentos PDF {#disassemble-pdf-documents}

Puede utilizar el servicio Ensamblador para desmontar un documento PDF. El servicio puede extraer páginas del documento de origen o dividir un documento de origen según los marcadores. Normalmente, esta tarea resulta útil si el documento PDF se creó originalmente a partir de muchos documentos individuales, como una colección de instrucciones.

### Extraer páginas de un documento de origen {#extract-pages-from-a-source-document}

En la siguiente ilustración, las páginas 1 a 3 se extraen del documento de origen y se colocan en un nuevo documento resultante.

![Extracción de páginas específicas de un documento de origen](assets/as_intro_page_extraction.png)

Extracción de páginas específicas de un documento de origen

El siguiente ejemplo es un documento DDX utilizado para desmontar el documento.

```xml
<PDF result="Doc4">
<PDF source="Doc2" pages="1-3"/>
</PDF>
```

### Dividir un documento de origen en función de los marcadores {#divide-a-source-document-based-on-bookmarks}

En la siguiente ilustración, DocA se divide en varios documentos resultantes. El primer marcador de nivel 1 de una página identifica el inicio de un nuevo documento resultante.

![División de un documento de origen basado en marcadores en varios documentos](assets/as_intro_pdfsfrombookmarks.png)

División de un documento de origen basado en marcadores en varios documentos

El siguiente ejemplo es un documento DDX que utiliza marcadores para desmontar un documento de origen.

```xml
<PDFsFromBookmarks prefix="A">
<PDF source="DocA"/>
</PDFsFromBookmarks>
```

## Determinar si los documentos son compatibles con PDF/A {#determine-whether-documents-are-pdf-a-compliant}

Puede utilizar el servicio Compilador para determinar si un documento PDF es compatible con PDF/A. PDF/A es un formato de archivo diseñado para la conservación a largo plazo del contenido del documento. Las fuentes se incrustan en el documento y el archivo se descomprime. Como resultado, un documento PDF/A suele ser mayor que un documento PDF estándar. Además, un documento PDF/A no contiene contenido de audio y vídeo.

## Obtener información sobre un documento PDF {#obtain-information-about-a-pdf-document}

Puede utilizar el servicio Compilador para obtener la siguiente información sobre un documento PDF:

* Información de texto.

   * Palabras en cada página del documento
   * Posición de cada palabra en cada página del documento
   * Sentencias en cada párrafo de cada página del documento

* Marcadores, incluidos el número de página, el título, el destino y la apariencia. Puede exportar esto\
   datos de un documento PDF e impórtelos en un documento PDF.

* Archivos adjuntos, incluida la información del archivo. Para los datos adjuntos de nivel de página, también incluye la variable\
   ubicación de la anotación de archivo adjunto. Puede exportar estos datos desde un documento PDF y\
   impórtela en un documento PDF.

* Empaquetar archivos, incluida la información de archivo, las carpetas, el paquete, el esquema y los datos de campo. Puede exportar estos datos desde un documento PDF e importarlos en un documento PDF.

## Validar documentos DDX {#validate-ddx-documents}

Puede utilizar el servicio Ensamblador para determinar si un documento DDX es válido. Por ejemplo, si ha actualizado desde una versión de LiveCycle anterior, la validación garantiza que el documento DDX sea válido.

## Llamar a otros servicios {#call-other-services}

Puede utilizar documentos DDX que hagan que el servicio Ensamblador llame a los siguientes servicios de ciclo LiveC. El servicio del ensamblador puede llamar únicamente a los servicios instalados con LiveCycle.

**Servicio** Extensiones de Reader: Permite a los usuarios de Adobe Reader firmar digitalmente el documento PDF resultante.

**Servicio** Forms: Combina un archivo XDP y un archivo de datos XML para crear un documento PDF que contenga el formulario interactivo rellenado.

**Servicio** de salida: Convierte un formulario XML dinámico en un documento PDF que contiene un formulario no interactivo (acopla el formulario). El servicio Ensamblador acopla formularios XML estáticos y formularios Acrobat sin llamar al servicio Output.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="outDoc">
<PDF source="doc1"/>
<PDF source="doc2"/>
<ReaderRights
credentialAlias="LCESCred"
digitalSignatures="true"/>
</PDF>
</DDX>
```

El uso de DDX y el servicio de ensamblador para llamar a otros servicios de ciclo LiveC puede simplificar el diagrama de proceso. Puede incluso reducir el esfuerzo que gasta en personalizar sus flujos de trabajo. (Consulte también
