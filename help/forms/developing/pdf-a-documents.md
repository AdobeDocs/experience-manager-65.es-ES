---
title: Uso de documentos PDF/A
seo-title: Uso de documentos PDF/A
description: Utilice el servicio DocConverter para determinar si un documento PDF es un documento PDF/A y convertir documentos PDF a documentos PDF/A.
seo-description: Utilice el servicio DocConverter para determinar si un documento PDF es un documento PDF/A y convertir documentos PDF a documentos PDF/A.
uuid: c258d253-068a-4412-955a-21d8a4792d6f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 1e6cc554-aef1-463c-906b-634b80a27917
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2387'
ht-degree: 0%

---


# Uso de documentos PDF/A {#working-with-pdf-a-documents}

**Acerca del servicio DocConverter**

El servicio DocConverter puede convertir documentos PDF a documentos PDA/A. Puede realizar estas tareas mediante este servicio:

* Convierta documentos PDF en documentos PDF/A. (Consulte [Conversión de documentos a documentos PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents)).
* Determine si los documentos PDF son documentos PDF/A. (Consulte [Determinación mediante programación del cumplimiento de PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)).

>[!NOTE]
>
>Para obtener más información sobre el servicio DocConverter, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversión de documentos a documentos PDF/A {#converting-documents-to-pdf-a-documents}

Puede utilizar el servicio DocConverter para convertir un documento PDF en un documento PDF/A. Dado que PDF/A es un formato de archivo para la preservación a largo plazo del contenido del documento, todas las fuentes están incrustadas y el archivo no está comprimido. Como resultado, un documento PDF/A suele ser más grande que un documento PDF estándar. Además, un documento PDF/A no contiene contenido de audio y vídeo. Antes de convertir un documento PDF en un documento PDF/A, asegúrese de que el documento PDF no sea un documento PDF/A.

La especificación PDF/A-1 consta de dos niveles de conformidad, a saber, A y B. La diferencia principal entre ambos es la compatibilidad con la estructura lógica (accesibilidad), que no es necesaria para el nivel de conformidad B. Independientemente del nivel de conformidad, PDF/A-1 dicta que todas las fuentes están incrustadas dentro del documento PDF/A generado. En este momento, solo se admite PDF/A-1b en la validación (y conversión).

Aunque PDF/A es el estándar para archivar documentos PDF, no es obligatorio que PDF/A se utilice para archivar si un documento PDF estándar cumple los requisitos de la empresa. El propósito del estándar PDF/A es establecer un archivo PDF destinado a necesidades de archivo y preservación de documentos a largo plazo.

>[!NOTE]
>
>Para obtener más información sobre el servicio DocConverter, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para convertir un documento PDF en un documento PDF/A, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Crear un cliente DocConvert
1. Haga referencia a un documento PDF para convertirlo en un documento PDF/A.
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

Para poder realizar una operación de DocConverter mediante programación, debe crear un cliente de DocConverter. Si utiliza la API de Java, cree un objeto `DocConverterServiceClient`. Si utiliza la API de servicio web de DocConverter, cree un objeto `DocConverterServiceService`.

**Hacer referencia a un documento PDF para convertirlo en un documento PDF/A**

Recupere un documento PDF para convertirlo en un documento PDF/A. Si intenta convertir un documento PDF, como un formulario Acrobat, en un documento PDF/A, provocará una excepción.

**Configuración de la información de seguimiento**

Puede establecer una opción en tiempo de ejecución que determine la cantidad de información que se rastreará durante el proceso de conversión. Es decir, puede establecer nueve niveles diferentes que especifiquen cuánta información rastrea el servicio DocConverter cuando convierte un documento PDF en un documento PDF/A.

**Convertir el documento**

Después de crear el cliente de servicio DocConverter, haga referencia al documento PDF para convertir y establezca la opción en tiempo de ejecución que especifica cuánta información se rastrea, puede convertir el documento PDF a un documento PDF/A.

**Guardar el documento PDF/A**

Puede guardar el documento PDF/A como un archivo PDF.

**Consulte también**

[Convertir documentos a documentos PDF/A mediante la API de Java](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[Convertir documentos a documentos PDF/A mediante la API de servicio Web](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Determinación programática del cumplimiento de PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### Convertir documentos a documentos PDF/A mediante la API de Java {#convert-documents-to-pdf-a-documents-using-the-java-api}

Convertir un documento PDF en un documento PDF/A mediante la API de Java:

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-docConverter-client.jar, en la ruta de clase de su proyecto Java.

1. Crear un cliente DocConvert

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `DocConverterServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Hacer referencia a un documento PDF para convertirlo en un documento PDF/A

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF que desea convertir empleando su constructor y pasando un valor de cadena que especifique la ubicación del archivo PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Configuración de la información de seguimiento

   * Cree un objeto `PDFAConversionOptionSpec` utilizando su constructor.
   * Establezca el nivel de seguimiento de la información invocando el método `PDFAConversionOptionSpec` del objeto `setLogLevel` y pasando un valor de cadena que especifica el nivel de seguimiento. Por ejemplo, pase el valor `FINE`. Para obtener información sobre los distintos valores, consulte el método `setLogLevel` en la [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Convertir el documento

   Convierta el documento PDF en un documento PDF/A invocando el método `DocConverterServiceClient` del objeto `toPDFA` y pasando los siguientes valores:

   * El objeto `com.adobe.idp.Document` que contiene el documento PDF que se va a convertir
   * El objeto `PDFAConversionOptionSpec` que especifica la información de seguimiento

   El método `toPDFA` devuelve un objeto `PDFAConversionResult` que contiene el documento PDF/A.

1. Guardar el documento PDF/A

   * Recupere el documento PDF/A invocando el método `PDFAConversionResult` del objeto `getPDFA`. Este método devuelve un objeto `com.adobe.idp.Document` que representa el documento PDF/A.
   * Cree un objeto `java.io.File` que represente el archivo PDF/A. Asegúrese de que la extensión del nombre de archivo es .pdf.
   * Rellene el archivo con datos PDF/A invocando el método `com.adobe.idp.Document` del objeto `copyToFile` y pasando el objeto `java.io.File`.

**Consulte también**

[Uso de documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Inicio rápido (modo SOAP): Conversión de un documento en un documento PDF/A mediante la API de Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir documentos a documentos PDF/A mediante la API de servicio Web {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

Convertir un documento PDF en un documento PDF/A mediante la API DocConverter (servicio Web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL DocConverter.
   * Haga referencia al ensamblado cliente de Microsoft .NET.

1. Crear un cliente DocConvert

   * Mediante el ensamblado de cliente de Microsoft .NET, cree un objeto `DocConverterServiceService` invocando su constructor predeterminado.
   * Establezca el miembro de datos `DocConverterServiceService` del objeto `Credentials` con un valor `System.Net.NetworkCredential` que especifica el nombre de usuario y el valor de la contraseña.

1. Hacer referencia a un documento PDF para convertirlo en un documento PDF/A

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el documento PDF que se convierte en un documento PDF/A.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición de inicio y la longitud de flujo para leer.
   * Rellene el objeto `BLOB` asignando su propiedad `binaryData` con el contenido de la matriz de bytes.

1. Configuración de la información de seguimiento

   * Cree un objeto `PDFAConversionOptionSpec` utilizando su constructor.
   * Establezca el nivel de seguimiento de la información asignando un valor que especifica el nivel de seguimiento al miembro de datos `PDFAConversionOptionSpec` del objeto `logLevel`. Por ejemplo, asigne el valor `FINE` a este miembro de datos.

1. Convertir el documento

   Convierta el documento PDF en un documento PDF/A invocando el método `DocConverterServiceService` del objeto `toPDFA` y pasando los siguientes valores:

   * El objeto `BLOB` que contiene el documento PDF que se va a convertir
   * El objeto `PDFAConversionOptionSpec` que especifica la información de seguimiento

   El método `toPDFA` devuelve un objeto `PDFAConversionResult` que contiene el documento PDF/A.

1. Guardar el documento PDF/A

   * Cree un objeto `BLOB` que almacene el documento PDF/A obteniendo el valor del miembro de datos `PDFAConversionResult` del objeto `PDFADocument`.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` que se devolvió utilizando el objeto `PDFAConversionResult`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `binaryData`.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF/A.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Uso de documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Determinación mediante programación del cumplimiento de PDF/A {#programmatically-determining-pdf-a-compliancy}

Puede utilizar el servicio DocConverter para determinar si un documento PDF es compatible con PDF/A. Para obtener información sobre un documento PDF/A y cómo convertir un documento PDF a un documento PDF/A, consulte [Conversión de documentos a documentos PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents).

>[!NOTE]
>
>Para obtener más información sobre el servicio DocConverter, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para determinar la conformidad con PDF/A, realice los pasos siguientes:

1. Incluir archivos de proyecto.
1. Crear un cliente DocConvert
1. Haga referencia a un documento PDF utilizado para determinar la conformidad con PDF/A.
1. Establezca las opciones de tiempo de ejecución.
1. Recupere información sobre el documento PDF.

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

Para poder realizar una operación de DocConverter mediante programación, debe crear un cliente de DocConverter. Si utiliza la API de Java, cree un objeto `DocConverterServiceClient`. Si utiliza la API de servicio web de DocConverter, cree un objeto `DocConverterServiceService`.

**Hacer referencia a un documento PDF utilizado para determinar la conformidad con PDF/A**

Se debe hacer referencia a un documento PDF y pasarlo al servicio DocConverter para determinar si el documento PDF es compatible con PDF/A.

**Establecer opciones de tiempo de ejecución**

Puede establecer una opción en tiempo de ejecución que determine la cantidad de información que se rastreará durante el proceso de conversión. Es decir, puede establecer nueve niveles diferentes que especifiquen cuánta información rastrea el servicio DocConverter cuando convierte un documento PDF en un documento PDF/A.

**Recuperar información sobre el documento PDF**

Después de crear el cliente de servicio DocConverter, hacer referencia al documento PDF y establecer las opciones de tiempo de ejecución, puede determinar si el documento PDF es compatible con PDF/A.

**Consulte también**

[Determinar la conformidad con PDF/A mediante la API de Java](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[Determinar la conformidad con PDF/A mediante la API de servicio web](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinar la conformidad con PDF/A mediante la API de Java {#determine-pdf-a-compliancy-using-the-java-api}

Determine la conformidad con PDF/A mediante la API de Java:

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-docConverter-client.jar, en la ruta de clase de su proyecto Java.

1. Crear un cliente DocConvert

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `DocConverterServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Hacer referencia a un documento PDF utilizado para determinar la conformidad con PDF/A

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF que desea convertir empleando su constructor y pasando un valor de cadena que especifique la ubicación del archivo PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Establecer opciones de tiempo de ejecución

   * Cree un objeto `PDFAValidationOptionSpec` utilizando su constructor.
   * Establezca el nivel de conformidad invocando el método `PDFAValidationOptionSpec` del objeto `setCompliance` y pasando `PDFAValidationOptionSpec.Compliance.PDFA_1B`.
   * Establezca el nivel de seguimiento de la información invocando el método `PDFAValidationOptionSpec` del objeto `setLogLevel` y pasando un valor de cadena que especifica el nivel de seguimiento. Por ejemplo, pase el valor `FINE`. Para obtener información sobre los distintos valores, consulte el método `setLogLevel` en la [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Recuperar información sobre el documento PDF

   Determine la conformidad con PDF/A invocando el método `DocConverterServiceClient` del objeto `isPDFA` y pasando los siguientes valores:

   * El objeto `com.adobe.idp.Document` que contiene el documento PDF.
   * El objeto `PDFAValidationOptionSpec` que especifica opciones en tiempo de ejecución.

   El método `isPDFA` devuelve un objeto `PDFAValidationResult` que contiene los resultados de esta operación.

**Consulte también**

[Uso de documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Inicio rápido (modo SOAP): Determinación de la conformidad con PDF/A mediante la API de Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinar la conformidad con PDF/A mediante la API de servicio web {#determine-pdf-a-compliancy-using-the-web-service-api}

Determine la conformidad con PDF/A mediante la API de servicio web:

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL DocConverter.
   * Haga referencia al ensamblado cliente de Microsoft .NET.

1. Crear un cliente DocConvert

   * Mediante el ensamblado de cliente de Microsoft .NET, cree un objeto `DocConverterServiceService` invocando su constructor predeterminado.
   * Establezca el miembro de datos `DocConverterServiceService` del objeto `Credentials` con un valor `System.Net.NetworkCredential` que especifica el nombre de usuario y el valor de la contraseña.

1. Hacer referencia a un documento PDF utilizado para determinar la conformidad con PDF/A

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el documento PDF que se convierte en un documento PDF/A.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición de inicio y la longitud de flujo para leer.
   * Rellene el objeto `BLOB` asignando su propiedad `binaryData` con el contenido de la matriz de bytes.

1. Establecer opciones de tiempo de ejecución

   * Cree un objeto `PDFAValidationOptionSpec` utilizando su constructor.
   * Establezca el nivel de cumplimiento asignando el miembro de datos `PDFAValidationOptionSpec` del objeto `compliance` con el valor `PDFAConversionOptionSpec_Compliance.PDFA_1B`.
   * Establezca el nivel de seguimiento de la información asignando el miembro de datos `PDFAValidationOptionSpec` del objeto `resultLevel` con el valor `PDFAValidationOptionSpec_ResultLevel.DETAILED`.

1. Recuperar información sobre el documento PDF

   Determine la conformidad con PDF/A invocando el método `DocConverterServiceService` del objeto `isPDFA` y pasando los siguientes valores:

   * El objeto `BLOB` que contiene el documento PDF.
   * El objeto `PDFAValidationOptionSpec` que contiene opciones en tiempo de ejecución.

   El método `isPDFA` devuelve un objeto `PDFAValidationResult` que contiene los resultados de esta operación.

**Consulte también**

[Uso de documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
