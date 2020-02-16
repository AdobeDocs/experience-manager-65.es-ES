---
title: Uso de documentos PDF/A
seo-title: Uso de documentos PDF/A
description: nulo
seo-description: nulo
uuid: c258d253-068a-4412-955a-21d8a4792d6f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 1e6cc554-aef1-463c-906b-634b80a27917
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Uso de documentos PDF/A {#working-with-pdf-a-documents}

**Acerca del servicio DocConverter**

El servicio DocConverter puede convertir documentos PDF a documentos PDA/A. Puede realizar estas tareas mediante este servicio:

* Convertir documentos PDF a documentos PDF/A. (Consulte [Conversión de documentos a documentos](pdf-a-documents.md#converting-documents-to-pdf-a-documents)PDF/A).
* Determine si los documentos PDF son documentos PDF/A. (Consulte Determinación [mediante programación de la conformidad con PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)).

>[!NOTE]
>
>Para obtener más información sobre el servicio DocConverter, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversión de documentos a documentos PDF/A {#converting-documents-to-pdf-a-documents}

Puede utilizar el servicio DocConverter para convertir un documento PDF en un documento PDF/A. Dado que PDF/A es un formato de archivo para la conservación a largo plazo del contenido del documento, todas las fuentes se incrustan y el archivo se descomprime. Como resultado, un documento PDF/A suele ser más grande que un documento PDF estándar. Además, un documento PDF/A no contiene contenido de audio y vídeo. Antes de convertir un documento PDF a un documento PDF/A, asegúrese de que el documento PDF no es un documento PDF/A.

La especificación PDF/A-1 consta de dos niveles de conformidad, a saber, A y B. La principal diferencia entre ambas es la compatibilidad con la estructura lógica (accesibilidad), que no es necesaria para el nivel de conformidad B. Independientemente del nivel de conformidad, PDF/A-1 dicta que todas las fuentes están incrustadas en el documento PDF/A generado. En este momento, solo se admite PDF/A-1b en la validación (y conversión).

Aunque PDF/A es el estándar para archivar documentos PDF, no es obligatorio que se utilice PDF/A para archivar si un documento PDF estándar cumple los requisitos de su empresa. El propósito de la norma PDF/A es establecer un archivo PDF para necesidades de archivo y conservación de documentos a largo plazo.

>[!NOTE]
>
>Para obtener más información sobre el servicio DocConverter, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para convertir un documento PDF en un documento PDF/A, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Crear un cliente DocConvert
1. Haga referencia a un documento PDF para convertirlo en un documento PDF/A.
1. Configure la información de seguimiento.
1. Convierta el documento.
1. Guarde el documento PDF/A.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en el servidor de aplicaciones JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en el servidor de aplicaciones JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)de biblioteca Java de AEM Forms.

**Crear un cliente DocConvert**

Para poder realizar una operación de DocConverter mediante programación, debe crear un cliente DocConverter. Si utiliza la API de Java, cree un `DocConverterServiceClient` objeto. Si utiliza la API de servicio Web DocConverter, cree un `DocConverterServiceService` objeto.

**Hacer referencia a un documento PDF para convertirlo a un documento PDF/A**

Recupere un documento PDF para convertirlo en un documento PDF/A. Si intenta convertir un documento PDF, como un formulario de Acrobat, en un documento PDF/A, provocará una excepción.

**Configurar información de seguimiento**

Puede definir una opción en tiempo de ejecución que determine la cantidad de información que se rastreará durante el proceso de conversión. Es decir, puede establecer nueve niveles diferentes que especifican la cantidad de información que el servicio DocConverter rastrea cuando convierte un documento PDF en un documento PDF/A.

**Convertir el documento**

Después de crear el cliente del servicio DocConverter, haga referencia al documento PDF para convertir y defina la opción en tiempo de ejecución que especifica la cantidad de información que se rastreará, puede convertir el documento PDF en un documento PDF/A.

**Guardar el documento PDF/A**

Puede guardar el documento PDF/A como archivo PDF.

**Consulte también**

[Conversión de documentos a documentos PDF/A mediante la API de Java](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[Conversión de documentos a documentos PDF/A mediante la API de servicio Web](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Determinación programática de la compatibilidad con PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### Conversión de documentos a documentos PDF/A mediante la API de Java {#convert-documents-to-pdf-a-documents-using-the-java-api}

Convertir un documento PDF en un documento PDF/A mediante la API de Java:

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-docconverter-client.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente DocConvert

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `DocConverterServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Hacer referencia a un documento PDF para convertirlo a un documento PDF/A

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF que se va a convertir utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo PDF.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Configurar información de seguimiento

   * Cree un `PDFAConversionOptionSpec` objeto con su constructor.
   * Establezca el nivel de seguimiento de la información invocando el `PDFAConversionOptionSpec` método `setLogLevel` del objeto y pasando un valor de cadena que especifica el nivel de seguimiento. For example, pass the value `FINE`. Para obtener información sobre los distintos valores, consulte el `setLogLevel` método en la Referencia [de API de formularios](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM.

1. Convertir el documento

   Convierta el documento PDF a un documento PDF/A invocando el `DocConverterServiceClient` método del `toPDFA` objeto y pasando los valores siguientes:

   * El `com.adobe.idp.Document` objeto que contiene el documento PDF que se va a convertir
   * El `PDFAConversionOptionSpec` objeto que especifica la información de seguimiento
   El `toPDFA` método devuelve un `PDFAConversionResult` objeto que contiene el documento PDF/A.

1. Guardar el documento PDF/A

   * Recupere el documento PDF/A invocando el `PDFAConversionResult` método `getPDFA` del objeto. Este método devuelve un `com.adobe.idp.Document` objeto que representa el documento PDF/A.
   * Cree un `java.io.File` objeto que represente el archivo PDF/A. Asegúrese de que la extensión del nombre de archivo sea .pdf.
   * Rellene el archivo con datos PDF/A invocando el `com.adobe.idp.Document` método del `copyToFile` objeto y pasando el `java.io.File` objeto.

**Consulte también**

[Uso de documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Inicio rápido (modo SOAP): Conversión de un documento a un documento PDF/A mediante la API de Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de documentos a documentos PDF/A mediante la API de servicio Web {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

Convertir un documento PDF en un documento PDF/A mediante la API de DocConverter (servicio Web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que utilice el WSDL DocConverter.
   * Haga referencia al ensamblado de cliente de Microsoft .NET.

1. Crear un cliente DocConvert

   * Mediante el ensamblado de cliente de Microsoft .NET, cree un `DocConverterServiceService` objeto invocando su constructor predeterminado.
   * Establezca el miembro de datos del `DocConverterServiceService` objeto con `Credentials` un `System.Net.NetworkCredential` valor que especifique el nombre de usuario y el valor de la contraseña.

1. Hacer referencia a un documento PDF para convertirlo a un documento PDF/A

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar el documento PDF que se convierte en un documento PDF/A.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF y el modo en el que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `binaryData` propiedad con el contenido de la matriz de bytes.

1. Configurar información de seguimiento

   * Cree un `PDFAConversionOptionSpec` objeto con su constructor.
   * Establezca el nivel de seguimiento de la información asignando un valor que especifique el nivel de seguimiento al miembro de `PDFAConversionOptionSpec` datos del `logLevel` objeto. Por ejemplo, asigne el valor `FINE` a este miembro de datos.

1. Convertir el documento

   Convierta el documento PDF a un documento PDF/A invocando el `DocConverterServiceService` método del `toPDFA` objeto y pasando los valores siguientes:

   * El `BLOB` objeto que contiene el documento PDF que se va a convertir
   * El `PDFAConversionOptionSpec` objeto que especifica la información de seguimiento
   El `toPDFA` método devuelve un `PDFAConversionResult` objeto que contiene el documento PDF/A.

1. Guardar el documento PDF/A

   * Cree un `BLOB` objeto que almacene el documento PDF/A obteniendo el valor del miembro de `PDFAConversionResult` datos del `PDFADocument` objeto.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto devuelto mediante el `PDFAConversionResult` objeto. Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `binaryData` objeto.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF/A.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el `System.IO.BinaryWriter` método `Write` del objeto y pasando la matriz de bytes.

**Consulte también**

[Uso de documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Invocación de formularios AEM con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Determinación programática de la compatibilidad con PDF/A {#programmatically-determining-pdf-a-compliancy}

Puede utilizar el servicio DocConverter para determinar si un documento PDF es compatible con PDF/A. Para obtener información sobre un documento PDF/A y cómo convertir un documento PDF a un documento PDF/A, consulte [Conversión de documentos a documentos](pdf-a-documents.md#converting-documents-to-pdf-a-documents)PDF/A.

>[!NOTE]
>
>Para obtener más información sobre el servicio DocConverter, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para determinar la compatibilidad con PDF/A, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Crear un cliente DocConvert
1. Haga referencia a un documento PDF utilizado para determinar la compatibilidad con PDF/A.
1. Configure las opciones de tiempo de ejecución.
1. Recupere información sobre el documento PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en el servidor de aplicaciones JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en el servidor de aplicaciones JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)de biblioteca Java de AEM Forms.

**Crear un cliente DocConvert**

Para poder realizar una operación de DocConverter mediante programación, debe crear un cliente DocConverter. Si utiliza la API de Java, cree un `DocConverterServiceClient` objeto. Si utiliza la API de servicio Web DocConverter, cree un `DocConverterServiceService` objeto.

**Hacer referencia a un documento PDF utilizado para determinar la conformidad con PDF/A**

Se debe hacer referencia a un documento PDF y pasarlo al servicio DocConverter para determinar si el documento PDF es compatible con PDF/A.

**Definición de opciones de tiempo de ejecución**

Puede definir una opción en tiempo de ejecución que determine la cantidad de información que se rastreará durante el proceso de conversión. Es decir, puede establecer nueve niveles diferentes que especifican la cantidad de información que el servicio DocConverter rastrea cuando convierte un documento PDF en un documento PDF/A.

**Recuperar información sobre el documento PDF**

Después de crear el cliente del servicio DocConverter, hacer referencia al documento PDF y establecer las opciones de tiempo de ejecución, puede determinar si el documento PDF es compatible con PDF/A.

**Consulte también**

[Determinar la compatibilidad con PDF/A mediante la API de Java](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[Determinar la compatibilidad con PDF/A mediante la API de servicio Web](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinar la compatibilidad con PDF/A mediante la API de Java {#determine-pdf-a-compliancy-using-the-java-api}

Determinar la compatibilidad con PDF/A mediante la API de Java:

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-docconverter-client.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente DocConvert

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `DocConverterServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Hacer referencia a un documento PDF utilizado para determinar la conformidad con PDF/A

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF que se va a convertir utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo PDF.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Definición de opciones de tiempo de ejecución

   * Cree un `PDFAValidationOptionSpec` objeto con su constructor.
   * Establezca el nivel de cumplimiento invocando el `PDFAValidationOptionSpec` método `setCompliance` del objeto y pasando `PDFAValidationOptionSpec.Compliance.PDFA_1B`.
   * Establezca el nivel de seguimiento de la información invocando el `PDFAValidationOptionSpec` método `setLogLevel` del objeto y pasando un valor de cadena que especifica el nivel de seguimiento. For example, pass the value `FINE`. Para obtener información sobre los distintos valores, consulte el `setLogLevel` método en la Referencia [de API de formularios](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM.

1. Recuperar información sobre el documento PDF

   Determine la compatibilidad con PDF/A invocando el `DocConverterServiceClient` método del `isPDFA` objeto y pasando los siguientes valores:

   * El `com.adobe.idp.Document` objeto que contiene el documento PDF.
   * El `PDFAValidationOptionSpec` objeto que especifica las opciones de tiempo de ejecución.
   El `isPDFA` método devuelve un `PDFAValidationResult` objeto que contiene los resultados de esta operación.

**Consulte también**

[Uso de documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Inicio rápido (modo SOAP): Determinación de la compatibilidad con PDF/A mediante la API de Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinar la compatibilidad con PDF/A mediante la API de servicio Web {#determine-pdf-a-compliancy-using-the-web-service-api}

Determinar la compatibilidad con PDF/A mediante la API de servicio Web:

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que utilice el WSDL DocConverter.
   * Haga referencia al ensamblado de cliente de Microsoft .NET.

1. Crear un cliente DocConvert

   * Mediante el ensamblado de cliente de Microsoft .NET, cree un `DocConverterServiceService` objeto invocando su constructor predeterminado.
   * Establezca el miembro de datos del `DocConverterServiceService` objeto con `Credentials` un `System.Net.NetworkCredential` valor que especifique el nombre de usuario y el valor de la contraseña.

1. Hacer referencia a un documento PDF utilizado para determinar la conformidad con PDF/A

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar el documento PDF que se convierte en un documento PDF/A.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF y el modo en el que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `binaryData` propiedad con el contenido de la matriz de bytes.

1. Definición de opciones de tiempo de ejecución

   * Cree un `PDFAValidationOptionSpec` objeto con su constructor.
   * Establezca el nivel de cumplimiento asignando el valor al miembro de `PDFAValidationOptionSpec` datos del `compliance` objeto `PDFAConversionOptionSpec_Compliance.PDFA_1B`.
   * Establezca el nivel de seguimiento de la información asignando el `PDFAValidationOptionSpec` miembro de datos del `resultLevel` objeto con el valor `PDFAValidationOptionSpec_ResultLevel.DETAILED`.

1. Recuperar información sobre el documento PDF

   Determine la compatibilidad con PDF/A invocando el `DocConverterServiceService` método del `isPDFA` objeto y pasando los siguientes valores:

   * El `BLOB` objeto que contiene el documento PDF.
   * El `PDFAValidationOptionSpec` objeto que contiene opciones de tiempo de ejecución.
   El `isPDFA` método devuelve un `PDFAValidationResult` objeto que contiene los resultados de esta operación.

**Consulte también**

[Uso de documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Invocación de formularios AEM con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
