---
title: Uso de documentos de PDF/A
seo-title: Working with PDF/A Documents
description: Utilice el servicio DocConverter para determinar si un documento de PDF es un documento de PDF/A y convertir los documentos de PDF en documentos de PDF/A.
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
ht-degree: 1%

---

# Uso de documentos de PDF/A {#working-with-pdf-a-documents}

**Acerca del servicio DocConverter**

El servicio DocConverter puede convertir documentos PDF a documentos PDA/A. Puede realizar estas tareas mediante este servicio:

* Convierta documentos PDF en documentos PDF/A. (Consulte [Conversión de documentos a documentos de PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents).)
* Determine si los documentos del PDF son documentos del PDF/A. (Consulte [Determinación programática del cumplimiento de PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

>[!NOTE]
>
>Para obtener más información sobre el servicio DocConverter, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversión de documentos a documentos de PDF/A {#converting-documents-to-pdf-a-documents}

Puede utilizar el servicio DocConverter para convertir un documento PDF en un documento PDF/A. Como PDF/A es un formato de archivo para la preservación a largo plazo del contenido del documento, todas las fuentes están incrustadas y el archivo no está comprimido. Como resultado, un documento PDF/A suele ser más grande que un documento PDF estándar. Además, un documento PDF/A no contiene contenido de audio y vídeo. Antes de convertir un documento de PDF en un documento de PDF/A, asegúrese de que el documento de PDF no sea un documento de PDF/A.

La especificación del PDF/A-1 consta de dos niveles de conformidad, a saber, A y B. La principal diferencia entre ambos es la compatibilidad con la estructura lógica (accesibilidad), que no es necesaria para el nivel de conformidad B. Independientemente del nivel de conformidad, el PDF/A-1 dicta que todas las fuentes están incrustadas en el documento PDF/A generado. En este momento, solo se admite el PDF/A-1b en la validación (y conversión).

Aunque el PDF/A es el estándar para archivar documentos de PDF, no es obligatorio que el PDF/A se utilice para archivar si un documento de PDF estándar cumple los requisitos de la empresa. El propósito de la norma PDF/A es crear un archivo PDF destinado a las necesidades de archivo y conservación de documentos a largo plazo.

>[!NOTE]
>
>Para obtener más información sobre el servicio DocConverter, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para convertir un documento PDF en un documento PDF/A, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Crear un cliente DocConvert
1. Haga referencia a un documento de PDF para convertirlo en un documento de PDF/A.
1. Configure la información de seguimiento.
1. Convierta el documento.
1. Guarde el documento PDF/A.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente DocConvert**

Para poder realizar una operación de DocConverter mediante programación, debe crear un cliente de DocConverter. Si utiliza la API de Java, cree un `DocConverterServiceClient` objeto. Si utiliza la API del servicio web DocConverter, cree un `DocConverterServiceService` objeto.

**Hacer referencia a un documento de PDF para convertirlo en un documento de PDF/A**

Recupere un documento PDF para convertirlo en un documento PDF/A. Si intenta convertir un documento de PDF, como un formulario de Acrobat, en un documento de PDF/A, provocará una excepción.

**Configuración de la información de seguimiento**

Puede establecer una opción en tiempo de ejecución que determine la cantidad de información que se rastreará durante el proceso de conversión. Es decir, puede establecer nueve niveles diferentes que especifiquen cuánta información rastrea el servicio DocConverter cuando convierte un documento PDF en un documento PDF/A.

**Convertir el documento**

Después de crear el cliente de servicio DocConverter, haga referencia al documento PDF para convertir y establezca la opción en tiempo de ejecución que especifica cuánta información se rastrea, puede convertir el documento PDF a un documento PDF/A.

**Guarde el documento PDF/A**

Puede guardar el documento PDF/A como archivo PDF.

**Consulte también lo siguiente**

[Convertir documentos a documentos de PDF/A mediante la API de Java](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[Convertir documentos en documentos de PDF/A mediante la API de servicio web](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Determinación programática del cumplimiento de PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### Convertir documentos a documentos de PDF/A mediante la API de Java {#convert-documents-to-pdf-a-documents-using-the-java-api}

Convierta un documento de PDF en un documento de PDF/A mediante la API de Java:

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-docConverter-client.jar, en la ruta de clase de su proyecto Java.

1. Crear un cliente DocConvert

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `DocConverterServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Hacer referencia a un documento de PDF para convertirlo en un documento de PDF/A

   * Cree un `java.io.FileInputStream` objeto que representa el documento PDF que se va a convertir utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo PDF.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Configuración de la información de seguimiento

   * Cree un `PDFAConversionOptionSpec` usando su constructor.
   * Establezca el nivel de seguimiento de la información invocando la variable `PDFAConversionOptionSpec` del objeto `setLogLevel` y pasando un valor de cadena que especifica el nivel de seguimiento. Por ejemplo, pase el valor `FINE`. Para obtener información sobre los distintos valores, consulte la `setLogLevel` en el [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Convertir el documento

   Convierta el documento del PDF en un documento de PDF/A invocando la variable `DocConverterServiceClient` del objeto `toPDFA` y pasando los siguientes valores:

   * La variable `com.adobe.idp.Document` objeto que contiene el documento PDF que se va a convertir
   * La variable `PDFAConversionOptionSpec` objeto que especifica información de seguimiento

   La variable `toPDFA` el método devuelve un `PDFAConversionResult` objeto que contiene el documento PDF/A.

1. Guarde el documento PDF/A

   * Recupere el documento del PDF/A invocando la variable `PDFAConversionResult` del objeto `getPDFA` método. Este método devuelve un `com.adobe.idp.Document` objeto que representa el documento PDF/A.
   * Cree un `java.io.File` que representa el archivo PDF/A. Asegúrese de que la extensión del nombre de archivo es .pdf.
   * Rellene el archivo con datos de PDF/A invocando la variable `com.adobe.idp.Document` del objeto `copyToFile` y pasando el `java.io.File` objeto.

**Consulte también lo siguiente**

[Uso de documentos de PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Inicio rápido (modo SOAP): Conversión de un documento en un documento de PDF/A mediante la API de Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir documentos en documentos de PDF/A mediante la API de servicio web {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

Convierta un documento PDF en un documento PDF/A mediante la API DocConverter (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente Microsoft .NET que consuma el WSDL DocConverter.
   * Haga referencia al ensamblado del cliente Microsoft .NET.

1. Crear un cliente DocConvert

   * Con el ensamblado del cliente Microsoft .NET, cree un `DocConverterServiceService` invocando su constructor predeterminado.
   * Configure las variables `DocConverterServiceService` del objeto `Credentials` miembro de datos con un `System.Net.NetworkCredential` que especifica el nombre de usuario y el valor de contraseña.

1. Hacer referencia a un documento de PDF para convertirlo en un documento de PDF/A

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar el documento PDF que se convierte en un documento PDF/A.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF y el modo en el que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `binaryData` con el contenido de la matriz de bytes.

1. Configuración de la información de seguimiento

   * Cree un `PDFAConversionOptionSpec` usando su constructor.
   * Establezca el nivel de seguimiento de la información asignando un valor que especifique el nivel de seguimiento a la variable `PDFAConversionOptionSpec` del objeto `logLevel` miembro de datos. Por ejemplo, asigne el valor `FINE` a este miembro de datos.

1. Convertir el documento

   Convierta el documento del PDF en un documento de PDF/A invocando la variable `DocConverterServiceService` del objeto `toPDFA` y pasando los siguientes valores:

   * La variable `BLOB` objeto que contiene el documento PDF que se va a convertir
   * La variable `PDFAConversionOptionSpec` objeto que especifica información de seguimiento

   La variable `toPDFA` el método devuelve un `PDFAConversionResult` objeto que contiene el documento PDF/A.

1. Guarde el documento PDF/A

   * Cree un `BLOB` objeto que almacena el documento PDF/A obteniendo el valor de la variable `PDFAConversionResult` del objeto `PDFADocument` miembro de datos.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto que se devolvió utilizando la variable `PDFAConversionResult` objeto. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `binaryData` miembro de datos.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF/A.
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Uso de documentos de PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Determinación programática del cumplimiento de PDF/A {#programmatically-determining-pdf-a-compliancy}

Puede utilizar el servicio DocConverter para determinar si un documento de PDF es compatible con PDF/A. Para obtener información sobre un documento de PDF/A y cómo convertir un documento de PDF en un documento de PDF/A, consulte [Conversión de documentos a documentos de PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents).

>[!NOTE]
>
>Para obtener más información sobre el servicio DocConverter, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para determinar la conformidad PDF/A, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Crear un cliente DocConvert
1. Haga referencia a un documento de PDF utilizado para determinar la conformidad del PDF/A.
1. Establezca las opciones de tiempo de ejecución.
1. Recupere información sobre el documento del PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente DocConvert**

Para poder realizar una operación de DocConverter mediante programación, debe crear un cliente de DocConverter. Si utiliza la API de Java, cree un `DocConverterServiceClient` objeto. Si utiliza la API del servicio web DocConverter, cree un `DocConverterServiceService` objeto.

**Referencia a un documento de PDF utilizado para determinar la conformidad del PDF/A**

Se debe hacer referencia a un documento PDF y pasarlo al servicio DocConverter para determinar si el documento PDF es compatible con el PDF/A.

**Establecer opciones de tiempo de ejecución**

Puede establecer una opción en tiempo de ejecución que determine la cantidad de información que se rastreará durante el proceso de conversión. Es decir, puede establecer nueve niveles diferentes que especifiquen cuánta información rastrea el servicio DocConverter cuando convierte un documento PDF en un documento PDF/A.

**Recuperar información sobre el documento del PDF**

Después de crear el cliente de servicio DocConverter, hacer referencia al documento del PDF y establecer las opciones de tiempo de ejecución, puede determinar si el documento del PDF es un documento compatible con el PDF/A.

**Consulte también lo siguiente**

[Determinar la conformidad del PDF/A mediante la API de Java](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[Determinar la conformidad del PDF/A mediante la API de servicio web](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinar la conformidad del PDF/A mediante la API de Java {#determine-pdf-a-compliancy-using-the-java-api}

Determinar la conformidad del PDF/A mediante la API de Java:

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-docConverter-client.jar, en la ruta de clase de su proyecto Java.

1. Crear un cliente DocConvert

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `DocConverterServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Referencia a un documento de PDF utilizado para determinar la conformidad del PDF/A

   * Cree un `java.io.FileInputStream` objeto que representa el documento PDF que se va a convertir utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo PDF.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Establecer opciones de tiempo de ejecución

   * Cree un `PDFAValidationOptionSpec` usando su constructor.
   * Establezca el nivel de conformidad invocando la variable `PDFAValidationOptionSpec` del objeto `setCompliance` método y paso `PDFAValidationOptionSpec.Compliance.PDFA_1B`.
   * Establezca el nivel de seguimiento de la información invocando la variable `PDFAValidationOptionSpec` del objeto `setLogLevel` y pasando un valor de cadena que especifica el nivel de seguimiento. Por ejemplo, pase el valor `FINE`. Para obtener información sobre los distintos valores, consulte la `setLogLevel` en el [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Recuperar información sobre el documento del PDF

   Determine la conformidad del PDF/A invocando la variable `DocConverterServiceClient` del objeto `isPDFA` y pasando los siguientes valores:

   * La variable `com.adobe.idp.Document` objeto que contiene el documento PDF.
   * La variable `PDFAValidationOptionSpec` objeto que especifica opciones en tiempo de ejecución.

   La variable `isPDFA` el método devuelve un `PDFAValidationResult` que contiene los resultados de esta operación.

**Consulte también lo siguiente**

[Uso de documentos de PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Inicio rápido (modo SOAP): Determinación de la conformidad PDF/A mediante la API de Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinar la conformidad del PDF/A mediante la API de servicio web {#determine-pdf-a-compliancy-using-the-web-service-api}

Determine la conformidad de PDF/A mediante la API de servicio web:

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente Microsoft .NET que consuma el WSDL DocConverter.
   * Haga referencia al ensamblado del cliente Microsoft .NET.

1. Crear un cliente DocConvert

   * Con el ensamblado del cliente Microsoft .NET, cree un `DocConverterServiceService` invocando su constructor predeterminado.
   * Configure las variables `DocConverterServiceService` del objeto `Credentials` miembro de datos con un `System.Net.NetworkCredential` que especifica el nombre de usuario y el valor de contraseña.

1. Referencia a un documento de PDF utilizado para determinar la conformidad del PDF/A

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar el documento PDF que se convierte en un documento PDF/A.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF y el modo en el que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `binaryData` con el contenido de la matriz de bytes.

1. Establecer opciones de tiempo de ejecución

   * Cree un `PDFAValidationOptionSpec` usando su constructor.
   * Establezca el nivel de cumplimiento asignando la variable `PDFAValidationOptionSpec` del objeto `compliance` miembro de datos con el valor `PDFAConversionOptionSpec_Compliance.PDFA_1B`.
   * Establezca el nivel de seguimiento de la información asignando la variable `PDFAValidationOptionSpec` del objeto `resultLevel` miembro de datos con el valor `PDFAValidationOptionSpec_ResultLevel.DETAILED`.

1. Recuperar información sobre el documento del PDF

   Determine la conformidad del PDF/A invocando la variable `DocConverterServiceService` del objeto `isPDFA` y pasando los siguientes valores:

   * La variable `BLOB` objeto que contiene el documento PDF.
   * La variable `PDFAValidationOptionSpec` que contiene opciones de tiempo de ejecución.

   La variable `isPDFA` el método devuelve un `PDFAValidationResult` que contiene los resultados de esta operación.

**Consulte también lo siguiente**

[Uso de documentos de PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
