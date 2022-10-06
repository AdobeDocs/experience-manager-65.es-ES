---
title: Uso del servicio Assembler
seo-title: Using Assembler Service
description: El servicio Assembler permite combinar, reorganizar y aumentar documentos PDF y XDP, así como obtener información sobre documentos PDF.
seo-description: The Assembler service lets you combine, rearrange, and augment PDF and XDP documents and obtain information about PDF documents.
uuid: 1efce50b-2d98-408e-aa43-ac4999de41a8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 6a99042f-79c7-494b-bca0-73f2b5725b58
docset: aem65
exl-id: 2acd6b19-0fe8-4994-b0f4-c9d5b9f3fdf1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2121'
ht-degree: 6%

---

# Uso del servicio Assembler{#using-assembler-service}

El servicio Assembler permite combinar, reorganizar y aumentar documentos PDF y XDP, así como obtener información sobre documentos PDF. Cada trabajo enviado al servicio Assembler incluye un documento XML de descripción de documento (DDX), documentos de origen y recursos externos (cadenas y gráficos). Para obtener más información sobre el servicio de ensamblador, consulte [Descripción general del servicio Assembler](../../forms/using/overview-aem-document-services.md#p-assembler-service-p).

Puede utilizar el servicio de ensamblados para las siguientes operaciones:

## Montar los documentos PDF {#assemble-pdf-documents}

Puede utilizar el servicio Assembler para ensamblar dos o más documentos PDF en un único documento PDF o Portfolio PDF. También puede aplicar funciones al documento del PDF que ayuden a la navegación o mejoren la seguridad. A continuación se indican algunas formas de montar documentos PDF:

### Montar un documento PDF sencillo {#assemble-a-simple-pdf-document}

La siguiente ilustración muestra tres documentos de origen que se están combinando en un solo documento resultante.

![Montaje de un documento PDF simple desde varios documentos PDF](assets/as_document_assembly.png)

Montaje de un documento PDF simple desde varios documentos PDF

El siguiente ejemplo es un documento DDX sencillo que se utiliza para ensamblar el documento. Especifica los nombres de los documentos de origen utilizados para producir el documento resultante, así como el nombre del documento resultante:

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
* Opcionalmente, el documento resultante incluye una tabla de contenido creada a partir de los marcadores en los documentos de origen

### Crear un Portfolio PDF {#create-a-pdf-portfolio}

El servicio Assembler puede crear Portfolio PDF que contengan una colección de documentos y una interfaz de usuario independiente. La interfaz se denomina Diseño del Portfolio del PDF o Navegador del Portfolio del PDF (navegador). Los Portfolio del PDF amplían la capacidad de los paquetes del PDF añadiendo un navegador, carpetas y páginas de bienvenida. La interfaz puede mejorar la experiencia del usuario aprovechando la cadena de texto localizada, los esquemas de color personalizados y los recursos gráficos. El Portfolio del PDF también puede incluir carpetas para organizar los archivos del portafolio.

Cuando el servicio Assembler interpreta el siguiente documento DDX, monta un Portfolio PDF que incluye un navegador Portfolio PDF y un paquete de dos archivos. El servicio obtiene el navegador de la ubicación especificada por el origen myNavigator. Cambia el esquema de colores predeterminado del navegador al esquema de colores pinkScheme.

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

### Montar documentos cifrados {#assemble-encrypted-documents}

Al ensamblar un documento, también puede codificar el documento PDF con una contraseña. Una vez que un documento de PDF está cifrado con una contraseña, un usuario debe especificar la contraseña para ver el documento de PDF en Adobe Reader o Acrobat. Para codificar un documento PDF con una contraseña, el documento DDX debe contener valores de elementos de cifrado necesarios para cifrar un documento PDF.

El servicio de cifrado no tiene que formar parte de la instalación del LiveCycle para cifrar un documento PDF con una contraseña.

Si uno o más de los documentos de entrada están cifrados, proporcione una contraseña para abrir el documento como parte del DDX.

### Montar documentos utilizando la numeración Bates {#assemble-documents-using-bates-numbering}

Al ensamblar un documento, puede utilizar la numeración Bates para aplicar un identificador de página único a cada página. Al utilizar la numeración Bates, a cada página del documento (o conjunto de documentos) se le asigna un número que identifica de forma exclusiva la página. Por ejemplo, los documentos de fabricación que contienen información de lista de materiales y están asociados con la producción de un conjunto pueden contener un identificador. Un número Bates contiene un valor numérico incrementado secuencialmente y un prefijo y sufijo opcionales. El prefijo + valor numérico + sufijo se denomina patrón de fechas.

La siguiente ilustración muestra un documento PDF que contiene un identificador único ubicado en el encabezado del documento.

![Documento PDF que contiene un identificador único ubicado en el encabezado del documento](do-not-localize/as_batesnumber.png)

Documento PDF que contiene un identificador único ubicado en el encabezado del documento

### Acoplar y montar documentos {#flatten-and-assemble-documents}

Puede utilizar el servicio Assembler para transformar un documento de PDF interactivo (por ejemplo, un formulario) en un documento de PDF no interactivo. Un documento PDF interactivo permite a los usuarios introducir o modificar datos ubicados en los campos del documento PDF. El proceso de transformar un documento de PDF interactivo en un documento de PDF no interactivo se denomina aplanamiento. Cuando se aplana un documento PDF, los campos de formulario conservan su aspecto gráfico, pero ya no son interactivos. Una razón para acoplar un documento PDF es garantizar que no se puedan modificar los datos. Además, las secuencias de comandos asociadas a los campos ya no funcionan.

Cuando se crea un documento de PDF que se monta a partir de documentos de PDF interactivos, el servicio Assembler aplana dichos formularios antes de ensamblarlos en el documento resultante.

>[!NOTE]
>
>El servicio Assembler utiliza el servicio Output para acoplar formularios XFA dinámicos. Si el servicio Assembler procesa un DDX que lo requiere para acoplar un formulario dinámico XFA y el servicio Output no está disponible, se genera una excepción. El servicio Assembler puede acoplar un formulario Acrobat o un formulario XFA estático sin utilizar el servicio Output .

## Agrupar documentos XDP {#assemble-xdp-documents}

Puede utilizar el servicio Assembler para ensamblar varios documentos XDP en un único documento XDP o en un documento PDF. Para los archivos XDP de origen que incluyen puntos de inserción, puede especificar los fragmentos que desea insertar.

Estas son algunas de las formas de ensamblar documentos XDP:

### Montaje de un documento XDP simple {#assemble-a-simple-xdp-document}

La siguiente ilustración muestra tres documentos XDP de origen que se están ensamblando en un único documento XDP resultante. El documento XDP resultante contiene los tres documentos XDP de origen, incluidos sus datos asociados. El documento resultante obtiene atributos básicos del documento base, que es el primer documento XDP de origen.

![Montaje de un simple documento XDP a partir de varios documentos XDP](assets/as_assembler_xdpassembly.png)

Montaje de un simple documento XDP a partir de varios documentos XDP

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

### Resolución de referencias durante el ensamblado {#resolving-references-during-assembly}

Normalmente, los documentos XDP pueden contener imágenes a las que se hace referencia mediante referencias absolutas o relativas. El servicio Assembler, de forma predeterminada, conserva las referencias a las imágenes en el documento XDP resultante.

Puede especificar cómo el servicio Assembler gestiona las imágenes a las que se hace referencia en los documentos XDP de origen mediante referencias absolutas o relativas en los archivos XDP al ensamblar. Puede elegir que todas las imágenes estén incrustadas en el resultado, de modo que no contenga referencias relativas o absolutas. Puede definirlo estableciendo el valor de la etiqueta resolveAssets , que puede utilizar cualquiera de las siguientes opciones. De forma predeterminada, no se resuelve ninguna referencia en el documento de resultados.

<table>
 <tbody> 
  <tr> 
   <th>Valor</th> 
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
   <td>Incrusta todas las imágenes a las que se hace referencia mediante referencias relativas en el XDP de origen<br /> documento.</td> 
  </tr> 
  <tr> 
   <td>absoluto</td> 
   <td>Incrusta todas las imágenes a las que se hace referencia mediante referencias absolutas en el XDP de origen<br /> documento.</td> 
  </tr> 
 </tbody> 
</table>

Puede especificar el valor del atributo resolveAssets en la etiqueta de origen XDP o en la etiqueta de resultado XDP principal. Si el atributo se especifica en la etiqueta de resultado XDP, todos los elementos de origen XDP que sean secundarios del resultado XDP lo heredarán. Sin embargo, si se especifica explícitamente el atributo para un elemento de origen, solo se anula la configuración del elemento de resultado para ese documento de origen.

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

También puede especificar el atributo para todos los documentos XDP de origen de forma independiente para obtener el mismo\
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

Puede especificar selectivamente las referencias de origen que desea resolver especificando el atributo resolveAssets para ellas. Los atributos de los documentos de origen individuales anulan la configuración del documento XDP resultante. En este ejemplo, los fragmentos incluidos también se resuelven.

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

#### Resolución selectiva de referencias absolutas o relativas {#selectively-resolve-absolute-or-relative-references}

Puede resolver selectivamente referencias absolutas o relativas en todos o algunos de los documentos de origen, como se muestra en el ejemplo siguiente:

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="absolute">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
</XDP>
</DDX
```

### Insertar dinámicamente fragmentos de formulario en un formulario XFA {#dynamically-insert-form-fragments-into-an-xfa-form}

Puede utilizar el servicio Assembler para crear un formulario XFA creado a partir de otro formulario XFA en el que se insertan fragmentos. Con esta función, puede utilizar fragmentos para crear varios formularios.

La compatibilidad con la inserción dinámica de fragmentos de formulario admite el control de un solo origen. Se mantiene una única fuente de componentes utilizados con frecuencia. Por ejemplo, puede crear un fragmento para el banner de la empresa. Si el banner cambia, solo tiene que modificar el fragmento. Los demás formularios que incluyen el fragmento no cambian.

Los diseñadores de formularios utilizan LiveCycle Designer para crear fragmentos de formulario. Estos fragmentos son subformularios con un nombre único dentro de un formulario XFA. Los diseñadores de formularios también utilizan Designer para crear formularios XFA con nombres únicos. Usted (el programador) escribe documentos DDX que especifican cómo se insertan los fragmentos en el formulario XFA.

La siguiente ilustración muestra dos formularios XML (plantillas XFA). El formulario de la izquierda contiene un punto de inserción denominado myInsertionPoint. El formulario de la derecha contiene un fragmento llamado myFragment.

![Inserción de fragmentos de formulario en un formulario XFA](assets/as_assembler_fragment_assy_assembled.png)

Inserción de fragmentos de formulario en un formulario XFA

Cuando el servicio Assembler interpreta el siguiente documento DDX, crea un formulario XML que contiene otro formulario XML. El subformulario myFragment del documento myFragmentSource se inserta en myInsertionPoint en el documento myFormSource.

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

Puede utilizar el servicio Assembler para empaquetar un documento XDP como documento PDF, como se muestra en este documento DDX.

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

## Desmontar los documentos PDF {#disassemble-pdf-documents}

Puede utilizar el servicio Assembler para desmontar un documento PDF. El servicio puede extraer páginas del documento de origen o dividir un documento de origen basado en marcadores. Normalmente, esta tarea resulta útil si el documento del PDF se creó originalmente a partir de numerosos documentos individuales, como una colección de declaraciones.

### Extraer páginas de un documento fuente {#extract-pages-from-a-source-document}

En la siguiente ilustración, las páginas 1 a 3 se extraen del documento de origen y se colocan en un nuevo documento resultante.

![Extracción de páginas específicas de un documento de origen](assets/as_intro_page_extraction.png)

Extracción de páginas específicas de un documento de origen

El siguiente ejemplo es un documento DDX utilizado para desmontar el documento.

```xml
<PDF result="Doc4">
<PDF source="Doc2" pages="1-3"/>
</PDF>
```

### Dividir un documento fuente basado en marcadores {#divide-a-source-document-based-on-bookmarks}

En la siguiente ilustración, el DocA se divide en varios documentos resultantes. El primer marcador de nivel 1 de una página identifica el inicio de un nuevo documento resultante.

![Dividir un documento de origen basado en marcadores en varios documentos](assets/as_intro_pdfsfrombookmarks.png)

Dividir un documento de origen basado en marcadores en varios documentos

El siguiente ejemplo es un documento DDX que utiliza marcadores para desmontar un documento de origen.

```xml
<PDFsFromBookmarks prefix="A">
<PDF source="DocA"/>
</PDFsFromBookmarks>
```

## Determinar si los documentos son compatibles con el PDF/A {#determine-whether-documents-are-pdf-a-compliant}

Puede utilizar el servicio Assembler para determinar si un documento PDF es compatible con el PDF/A. PDF/A es un formato de archivo diseñado para la conservación a largo plazo del contenido del documento. Las fuentes están incrustadas en el documento y el archivo no está comprimido. Como resultado, un documento PDF/A suele ser más grande que un documento PDF estándar. Además, un documento PDF/A no contiene contenido de audio y vídeo.

## Obtener información sobre un documento de PDF {#obtain-information-about-a-pdf-document}

Puede utilizar el servicio Assembler para obtener la siguiente información sobre un documento de PDF:

* Información de texto.

   * Palabras en cada página del documento
   * Posición de cada palabra en cada página del documento
   * Frases en cada párrafo de cada página del documento

* Marcadores, incluido el número de página, el título, el destino y la apariencia. Puede exportar esto\
   datos de un documento de PDF e importarlos en un documento de PDF.

* Archivos adjuntos, incluida la información del archivo. Para los archivos adjuntos de nivel de página, también incluye el\
   ubicación de la anotación de archivo adjunto. Puede exportar estos datos desde un documento de PDF y\
   impórtelos en un documento de PDF.

* Archivos de paquete, incluida la información de archivo, las carpetas, el paquete, el esquema y los datos de campo. Puede exportar estos datos desde un documento de PDF e importarlos en un documento de PDF.

## Validación de documentos DDX {#validate-ddx-documents}

Puede utilizar el servicio Assembler para determinar si un documento DDX es válido. Por ejemplo, si ha actualizado desde una versión de LiveCycle anterior, la validación garantiza que el documento DDX sea válido.

## Llamar a otros servicios {#call-other-services}

Puede utilizar documentos DDX que hagan que el servicio Assembler llame a los siguientes servicios de ciclo LiveC. El servicio Assembler solo puede llamar a los servicios instalados con LiveCycle.

**Servicio de extensiones de Reader**: Permite a los usuarios de Adobe Reader firmar digitalmente el documento PDF resultante.

**Servicio de Forms**: Combina un archivo XDP y un archivo de datos XML para producir un documento PDF que contenga el formulario interactivo rellenado.

**Servicio de salida**: Convierte un formulario XML dinámico en un documento PDF que contiene un formulario no interactivo (aplana el formulario). El servicio Assembler aplana los formularios XML estáticos y los formularios Acrobat sin llamar al servicio Output .

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

El uso de DDX y el servicio Assembler para llamar a otros servicios de ciclo LiveC puede simplificar el diagrama de proceso. Incluso puede reducir el esfuerzo que invierte en personalizar los flujos de trabajo. (Consulte también lo siguiente
