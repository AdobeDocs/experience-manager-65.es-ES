---
title: Trabajar con documentos PDF/A
seo-title: Working with PDF/A Documents
description: Utilice el servicio DocConverter para determinar si un documento de PDF es un documento de PDF PDF/A y convertirlo en documentos de PDF/A.
seo-description: Use the  DocConverter service to determine if a PDF document is a PDF/A document and convert PDF documents to PDF/A documents.
uuid: c258d253-068a-4412-955a-21d8a4792d6f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 1e6cc554-aef1-463c-906b-634b80a27917
role: Developer
exl-id: 966c3554-25df-4467-866e-11c43cc15b58
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2358'
ht-degree: 2%

---

# Trabajar con documentos PDF/A {#working-with-pdf-a-documents}

**Acerca del servicio DocConverter**

El servicio DocConverter puede convertir documentos de PDF en documentos de PDA/A. Puede realizar estas tareas con este servicio:

* Conversión de documentos de PDF en documentos de PDF/A. (Consulte [Conversión de documentos a documentos de PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents).)
* Determine si los documentos del PDF son documentos del PDF/A. (Consulte [Determinación programática de la conformidad de PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

>[!NOTE]
>
>Para obtener más información sobre el servicio DocConverter, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversión de documentos a documentos de PDF/A {#converting-documents-to-pdf-a-documents}

Puede utilizar el servicio DocConverter para convertir un documento de PDF en un documento de PDF/A. Como PDF/A es un formato de archivo para la preservación a largo plazo del contenido del documento, todas las fuentes están incrustadas y el archivo no está comprimido. Como resultado, un documento PDF/A suele ser más grande que un documento PDF estándar. Además, un documento PDF/A no contiene contenido de audio y vídeo. Antes de convertir un documento de PDF en un documento de PDF/A, asegúrese de que el documento de PDF no sea un documento de PDF/A.

La especificación PDF/A-1 consta de dos niveles de conformidad, a saber, A y B. La principal diferencia entre los dos es la compatibilidad con la estructura lógica (accesibilidad), que no es necesaria para el nivel de conformidad B. Independientemente del nivel de conformidad, PDF/A-1 dicta que todas las fuentes estén incrustadas en el documento PDF/A generado. En este momento, solo se admite el PDF/A-1b en la validación (y conversión).

Aunque PDF/A es el estándar para archivar documentos de PDF, no es obligatorio que PDF/A se utilice para archivar si un documento de PDF estándar cumple los requisitos de su empresa. El propósito de la norma PDF/A es crear un archivo PDF destinado a las necesidades de archivo y conservación de documentos a largo plazo.

>[!NOTE]
>
>Para obtener más información sobre el servicio DocConverter, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para convertir un documento de PDF en un documento de PDF/A, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Crear un cliente DocConvert
1. Hacer referencia a un documento de PDF para convertirlo en un documento de PDF/A.
1. Configure la información de seguimiento.
1. Convertir el documento.
1. Guarde el documento PDF/A.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente DocConvert**

Para poder realizar mediante programación una operación DocConverter, debe crear un cliente DocConverter. Si utiliza la API de Java, cree un `DocConverterServiceClient` objeto. Si utiliza la API del servicio web DocConverter, cree un `DocConverterServiceService` objeto.

**Hacer referencia a un documento de PDF para convertirlo en un documento de PDF/A**

Recupere un documento de PDF para convertirlo en un documento de PDF/A. Si intenta convertir un documento de PDF, como un formulario de Acrobat, en un documento de PDF/A, se producirá una excepción.

**Establecer información de seguimiento**

Puede establecer una opción en tiempo de ejecución que determine la cantidad de información que se rastreará durante el proceso de conversión. Es decir, puede establecer nueve niveles diferentes que especifiquen la cantidad de información que el servicio DocConverter rastrea cuando convierte un documento de PDF en un documento de PDF/A.

**Convertir el documento**

Después de crear el cliente de servicio DocConverter, haga referencia al documento de PDF para convertir y establezca la opción de tiempo de ejecución que especifica cuánta información se rastrea, puede convertir el documento de PDF en un documento de PDF/A.

**Guarde el documento PDF/A.**

Puede guardar el documento de PDF/A como un archivo de PDF.

**Consulte también**

[Conversión de documentos en documentos de PDF/A mediante la API de Java](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[Conversión de documentos en documentos de PDF/A mediante la API de servicio web](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Determinación programática de la conformidad de PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### Conversión de documentos en documentos de PDF/A mediante la API de Java {#convert-documents-to-pdf-a-documents-using-the-java-api}

Conversión de un documento de PDF en un documento de PDF/A mediante la API de Java:

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-docconverter-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente DocConvert

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `DocConverterServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Hacer referencia a un documento de PDF para convertirlo en un documento de PDF/A

   * Crear un `java.io.FileInputStream` que representa el documento de PDF que se va a convertir utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo de PDF.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Establecer información de seguimiento

   * Crear un `PDFAConversionOptionSpec` mediante su constructor.
   * Defina el nivel de seguimiento de la información invocando el `PDFAConversionOptionSpec` del objeto `setLogLevel` y pasando un valor de cadena que especifica el nivel de seguimiento. Por ejemplo, pase el valor `FINE`. Para obtener información sobre los distintos valores, consulte la `setLogLevel` método en la [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Convertir el documento

   Convierta el documento de PDF en un documento de PDF/A invocando el `DocConverterServiceClient` del objeto `toPDFA` y pasando los siguientes valores:

   * El `com.adobe.idp.Document` que contiene el documento de PDF que se va a convertir
   * El `PDFAConversionOptionSpec` objeto que especifica información de seguimiento

   El `toPDFA` El método devuelve un valor `PDFAConversionResult` que contiene el documento de PDF/A.

1. Guarde el documento PDF/A.

   * Recupere el documento PDF/A invocando el `PDFAConversionResult` del objeto `getPDFA` método. Este método devuelve un `com.adobe.idp.Document` que representa el documento del PDF/A.
   * Crear un `java.io.File` que representa el archivo PDF/A. Asegúrese de que la extensión del nombre de archivo sea .pdf.
   * Rellene el archivo con datos de PDF/A invocando el `com.adobe.idp.Document` del objeto `copyToFile` y pasando el `java.io.File` objeto.

**Consulte también**

[Trabajar con documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Inicio rápido (modo SOAP): Conversión de un documento a un documento de PDF/A mediante la API de Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de documentos en documentos de PDF/A mediante la API de servicio web {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

Conversión de un documento de PDF en un documento de PDF/A mediante la API de DocConverter (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL de DocConverter.
   * Hacer referencia al ensamblado de cliente de Microsoft .NET.

1. Crear un cliente DocConvert

   * Mediante el ensamblado de cliente de Microsoft .NET, cree un `DocConverterServiceService` invocando su constructor predeterminado.
   * Configure las variables `DocConverterServiceService` del objeto `Credentials` miembro de datos con un `System.Net.NetworkCredential` que especifica el valor de nombre de usuario y contraseña.

1. Hacer referencia a un documento de PDF para convertirlo en un documento de PDF/A

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar el documento de PDF que se convierte en un documento de PDF/A.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación de archivo del documento de PDF y el modo para abrir el archivo en.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` al asignar su `binaryData` con el contenido de la matriz de bytes.

1. Establecer información de seguimiento

   * Crear un `PDFAConversionOptionSpec` mediante su constructor.
   * Establezca el nivel de seguimiento de la información asignando un valor que especifique el nivel de seguimiento a `PDFAConversionOptionSpec` del objeto `logLevel` miembro de datos. Por ejemplo, asigne el valor `FINE` a este miembro de datos.

1. Convertir el documento

   Convierta el documento de PDF en un documento de PDF/A invocando el `DocConverterServiceService` del objeto `toPDFA` y pasando los siguientes valores:

   * El `BLOB` que contiene el documento de PDF que se va a convertir
   * El `PDFAConversionOptionSpec` objeto que especifica información de seguimiento

   El `toPDFA` El método devuelve un valor `PDFAConversionResult` que contiene el documento de PDF/A.

1. Guarde el documento PDF/A.

   * Crear un `BLOB` que almacena el documento de PDF/A al obtener el valor del `PDFAConversionResult` del objeto `PDFADocument` miembro de datos.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto que se devolvió con el objeto `PDFAConversionResult` objeto. Rellene la matriz de bytes obteniendo el valor de `BLOB` del objeto `binaryData` miembro de datos.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación de archivo del documento PDF/A.
   * Crear un `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Trabajar con documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Crear un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Determinación programática de la conformidad de PDF/A {#programmatically-determining-pdf-a-compliancy}

Puede utilizar el servicio DocConverter para determinar si un documento de PDF es compatible con el PDF/A. Para obtener información sobre un documento de PDF PDF/A y cómo convertirlo en un documento de PDF/A, consulte [Conversión de documentos a documentos de PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents).

>[!NOTE]
>
>Para obtener más información sobre el servicio DocConverter, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para determinar la conformidad del PDF/A, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Crear un cliente DocConvert
1. Hacer referencia a un documento de PDF utilizado para determinar la conformidad de PDF/A.
1. Establecer opciones en tiempo de ejecución.
1. Recupere información sobre el documento del PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente DocConvert**

Para poder realizar mediante programación una operación DocConverter, debe crear un cliente DocConverter. Si utiliza la API de Java, cree un `DocConverterServiceClient` objeto. Si utiliza la API del servicio web DocConverter, cree un `DocConverterServiceService` objeto.

**Hacer referencia a un documento de PDF utilizado para determinar la conformidad de PDF/A.**

Se debe hacer referencia a un documento de PDF y pasarlo al servicio DocConverter para determinar si el documento de PDF es compatible con el PDF/A.

**Establecer opciones en tiempo de ejecución**

Puede establecer una opción en tiempo de ejecución que determine la cantidad de información que se rastreará durante el proceso de conversión. Es decir, puede establecer nueve niveles diferentes que especifiquen cuánta información rastrea el servicio DocConverter cuando convierte un documento de PDF en un documento de PDF/A.

**Recuperar información sobre el documento del PDF**

Después de crear el cliente de servicio DocConverter, hacer referencia al documento de PDF y establecer las opciones en tiempo de ejecución, puede determinar si el documento de PDF es un documento compatible con el PDF/A.

**Consulte también**

[Determinar la conformidad del PDF/A mediante la API de Java](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[Determinar la conformidad del PDF/A mediante la API del servicio web](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinar la conformidad del PDF/A mediante la API de Java {#determine-pdf-a-compliancy-using-the-java-api}

Determine la conformidad del PDF/A mediante la API de Java:

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-docconverter-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente DocConvert

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `DocConverterServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Hacer referencia a un documento de PDF utilizado para determinar la conformidad de PDF/A.

   * Crear un `java.io.FileInputStream` que representa el documento de PDF que se va a convertir utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo de PDF.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Establecer opciones en tiempo de ejecución

   * Crear un `PDFAValidationOptionSpec` mediante su constructor.
   * Defina el nivel de conformidad invocando el `PDFAValidationOptionSpec` del objeto `setCompliance` método y paso `PDFAValidationOptionSpec.Compliance.PDFA_1B`.
   * Defina el nivel de seguimiento de la información invocando el `PDFAValidationOptionSpec` del objeto `setLogLevel` y pasando un valor de cadena que especifica el nivel de seguimiento. Por ejemplo, pase el valor `FINE`. Para obtener información sobre los distintos valores, consulte la `setLogLevel` método en la [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Recuperar información sobre el documento del PDF

   Determine la conformidad del PDF/A invocando el `DocConverterServiceClient` del objeto `isPDFA` y pasando los siguientes valores:

   * El `com.adobe.idp.Document` que contiene el documento de PDF.
   * El `PDFAValidationOptionSpec` que especifica las opciones en tiempo de ejecución.

   El `isPDFA` El método devuelve un valor `PDFAValidationResult` que contiene los resultados de esta operación.

**Consulte también**

[Trabajar con documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Inicio rápido (modo SOAP): Determinación de la conformidad del PDF/A mediante la API de Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinar la conformidad del PDF/A mediante la API del servicio web {#determine-pdf-a-compliancy-using-the-web-service-api}

Determine la conformidad del PDF/A mediante la API del servicio web:

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL de DocConverter.
   * Hacer referencia al ensamblado de cliente de Microsoft .NET.

1. Crear un cliente DocConvert

   * Mediante el ensamblado de cliente de Microsoft .NET, cree un `DocConverterServiceService` invocando su constructor predeterminado.
   * Configure las variables `DocConverterServiceService` del objeto `Credentials` miembro de datos con un `System.Net.NetworkCredential` que especifica el valor de nombre de usuario y contraseña.

1. Hacer referencia a un documento de PDF utilizado para determinar la conformidad de PDF/A.

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar el documento de PDF que se convierte en un documento de PDF/A.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación de archivo del documento de PDF y el modo para abrir el archivo en.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` al asignar su `binaryData` con el contenido de la matriz de bytes.

1. Establecer opciones en tiempo de ejecución

   * Crear un `PDFAValidationOptionSpec` mediante su constructor.
   * Defina el nivel de conformidad asignando el `PDFAValidationOptionSpec` del objeto `compliance` miembro de datos con el valor `PDFAConversionOptionSpec_Compliance.PDFA_1B`.
   * Defina el nivel de seguimiento de la información asignando el `PDFAValidationOptionSpec` del objeto `resultLevel` miembro de datos con el valor `PDFAValidationOptionSpec_ResultLevel.DETAILED`.

1. Recuperar información sobre el documento del PDF

   Determine la conformidad del PDF/A invocando el `DocConverterServiceService` del objeto `isPDFA` y pasando los siguientes valores:

   * El `BLOB` que contiene el documento de PDF.
   * El `PDFAValidationOptionSpec` que contiene opciones en tiempo de ejecución.

   El `isPDFA` El método devuelve un valor `PDFAValidationResult` que contiene los resultados de esta operación.

**Consulte también**

[Trabajar con documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Crear un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
