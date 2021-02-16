---
title: Uso de Documentos PDF/A
seo-title: Uso de Documentos PDF/A
description: Utilice el servicio DocConverter para determinar si un documento PDF es un documento PDF/A y convertir documentos PDF en documentos PDF/A.
seo-description: Utilice el servicio DocConverter para determinar si un documento PDF es un documento PDF/A y convertir documentos PDF en documentos PDF/A.
uuid: c258d253-068a-4412-955a-21d8a4792d6f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 1e6cc554-aef1-463c-906b-634b80a27917
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '2386'
ht-degree: 0%

---


# Trabajar con Documentos PDF/A {#working-with-pdf-a-documents}

**Acerca del servicio DocConverter**

El servicio DocConverter puede convertir documentos PDF a documentos PDA/A. Puede realizar estas tareas mediante este servicio:

* Convertir documentos PDF a documentos PDF/A. (Consulte [Conversión de Documentos a Documentos PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents)).
* Determine si los documentos PDF son documentos PDF/A. (Consulte [Determinación mediante programación de la conformidad con PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)).

>[!NOTE]
>
>Para obtener más información sobre el servicio DocConverter, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversión de Documentos a Documentos PDF/A {#converting-documents-to-pdf-a-documents}

Puede utilizar el servicio DocConverter para convertir un documento PDF en un documento PDF/A. Dado que PDF/A es un formato de archivo para la conservación a largo plazo del contenido del documento, todas las fuentes se incrustan y el archivo se descomprime. Como resultado, un documento PDF/A suele ser mayor que un documento PDF estándar. Además, un documento PDF/A no contiene contenido de audio y vídeo. Antes de convertir un documento PDF a un documento PDF/A, asegúrese de que el documento PDF no es un documento PDF/A.

La especificación PDF/A-1 consta de dos niveles de conformidad, a saber, A y B. La principal diferencia entre ambas es la compatibilidad con la estructura lógica (accesibilidad), que no es necesaria para el nivel de conformidad B. Independientemente del nivel de conformidad, PDF/A-1 dicta que todas las fuentes están incrustadas en el documento PDF/A generado. En este momento, solo se admite PDF/A-1b en la validación (y conversión).

Aunque PDF/A es el estándar para archivar documentos PDF, no es obligatorio que se utilice PDF/A para archivar si un documento PDF estándar cumple los requisitos de la compañía. El propósito de la norma PDF/A es crear un archivo PDF para necesidades de archivo y conservación de documentos a largo plazo.

>[!NOTE]
>
>Para obtener más información sobre el servicio DocConverter, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para convertir un documento PDF en un documento PDF/A, lleve a cabo los siguientes pasos:

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
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss Application Server)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente DocConvert**

Para poder realizar una operación de DocConverter mediante programación, debe crear un cliente DocConverter. Si utiliza la API de Java, cree un objeto `DocConverterServiceClient`. Si utiliza la API de servicio Web DocConverter, cree un objeto `DocConverterServiceService`.

**Hacer referencia a un documento PDF para convertirlo en un documento PDF/A**

Recupere un documento PDF para convertirlo en un documento PDF/A. Si intenta convertir un documento PDF, como un formulario Acrobat, en un documento PDF/A, provocará una excepción.

**Configurar información de seguimiento**

Puede definir una opción en tiempo de ejecución que determine la cantidad de información que se rastreará durante el proceso de conversión. Es decir, puede establecer nueve niveles diferentes que especifican cuánta información rastrea el servicio DocConverter cuando convierte un documento PDF en un documento PDF/A.

**Convertir el documento**

Después de crear el cliente del servicio DocConverter, haga referencia al documento PDF para convertir y defina la opción en tiempo de ejecución que especifica la cantidad de información que se rastreará, puede convertir el documento PDF en un documento PDF/A.

**Guardar el documento PDF/A**

Puede guardar el documento PDF/A como archivo PDF.

**Consulte también**

[Convertir documentos a documentos PDF/A mediante la API de Java](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[Convertir documentos a documentos PDF/A mediante la API de servicio web](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Determinación programática de la compatibilidad con PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### Convertir documentos a documentos PDF/A mediante la API de Java {#convert-documents-to-pdf-a-documents-using-the-java-api}

Convertir un documento PDF en un documento PDF/A mediante la API de Java:

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-docconverter-client.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente DocConvert

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `DocConverterServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Hacer referencia a un documento PDF para convertirlo en un documento PDF/A

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF que se va a convertir utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Configurar información de seguimiento

   * Cree un objeto `PDFAConversionOptionSpec` utilizando su constructor.
   * Establezca el nivel de seguimiento de la información invocando el método `PDFAConversionOptionSpec` del objeto `setLogLevel` y pasando un valor de cadena que especifica el nivel de seguimiento. Por ejemplo, pase el valor `FINE`. Para obtener información sobre los diferentes valores, consulte el método `setLogLevel` en la [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Convertir el documento

   Convierta el documento PDF en un documento PDF/A invocando el método `DocConverterServiceClient` del objeto `toPDFA` y pasando los siguientes valores:

   * El objeto `com.adobe.idp.Document` que contiene el documento PDF que se va a convertir
   * El objeto `PDFAConversionOptionSpec` que especifica la información de seguimiento

   El método `toPDFA` devuelve un objeto `PDFAConversionResult` que contiene el documento PDF/A.

1. Guardar el documento PDF/A

   * Recupere el documento PDF/A invocando el método `PDFAConversionResult` del objeto `getPDFA`. Este método devuelve un objeto `com.adobe.idp.Document` que representa el documento PDF/A.
   * Cree un objeto `java.io.File` que represente el archivo PDF/A. Asegúrese de que la extensión del nombre de archivo sea .pdf.
   * Rellene el archivo con datos PDF/A invocando el método `com.adobe.idp.Document` del objeto `copyToFile` y pasando el objeto `java.io.File`.

**Consulte también**

[Uso de Documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Inicio rápido (modo SOAP): Conversión de un documento a un documento PDF/A mediante la API de Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir documentos a documentos PDF/A mediante la API de servicio Web {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

Convertir un documento PDF en un documento PDF/A mediante la API de DocConverter (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que utilice el WSDL DocConverter.
   * Haga referencia al ensamblado de cliente de Microsoft .NET.

1. Crear un cliente DocConvert

   * Mediante el ensamblado de cliente de Microsoft .NET, cree un objeto `DocConverterServiceService` invocando su constructor predeterminado.
   * Establezca el miembro de datos `DocConverterServiceService` del objeto `Credentials` con un valor `System.Net.NetworkCredential` que especifique el nombre de usuario y el valor de la contraseña.

1. Hacer referencia a un documento PDF para convertirlo en un documento PDF/A

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el documento PDF que se convierte en un documento PDF/A.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF y el modo en el que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando su propiedad `binaryData` con el contenido de la matriz de bytes.

1. Configurar información de seguimiento

   * Cree un objeto `PDFAConversionOptionSpec` utilizando su constructor.
   * Establezca el nivel de seguimiento de la información asignando un valor que especifique el nivel de seguimiento al miembro de datos `PDFAConversionOptionSpec` del objeto `logLevel`. Por ejemplo, asigne el valor `FINE` a este miembro de datos.

1. Convertir el documento

   Convierta el documento PDF en un documento PDF/A invocando el método `DocConverterServiceService` del objeto `toPDFA` y pasando los siguientes valores:

   * El objeto `BLOB` que contiene el documento PDF que se va a convertir
   * El objeto `PDFAConversionOptionSpec` que especifica la información de seguimiento

   El método `toPDFA` devuelve un objeto `PDFAConversionResult` que contiene el documento PDF/A.

1. Guardar el documento PDF/A

   * Cree un objeto `BLOB` que almacene el documento PDF/A obteniendo el valor del miembro de datos `PDFAConversionResult` del objeto `PDFADocument`.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` que se devolvió mediante el objeto `PDFAConversionResult`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `binaryData`.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF/A.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Uso de Documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Determinación programática de la conformidad con PDF/A {#programmatically-determining-pdf-a-compliancy}

Puede utilizar el servicio DocConverter para determinar si un documento PDF es compatible con PDF/A. Para obtener información sobre un documento PDF/A y cómo convertir un documento PDF en un documento PDF/A, consulte [Conversión de Documentos en Documentos PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents).

>[!NOTE]
>
>Para obtener más información sobre el servicio DocConverter, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss Application Server)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente DocConvert**

Para poder realizar una operación de DocConverter mediante programación, debe crear un cliente DocConverter. Si utiliza la API de Java, cree un objeto `DocConverterServiceClient`. Si utiliza la API de servicio Web DocConverter, cree un objeto `DocConverterServiceService`.

**Referencia a un documento PDF utilizado para determinar la conformidad con PDF/A**

Se debe hacer referencia a un documento PDF y pasarlo al servicio DocConverter para determinar si el documento PDF es compatible con PDF/A.

**Definición de opciones de tiempo de ejecución**

Puede definir una opción en tiempo de ejecución que determine la cantidad de información que se rastreará durante el proceso de conversión. Es decir, puede establecer nueve niveles diferentes que especifican la cantidad de información que el servicio DocConverter rastrea cuando convierte un documento PDF en un documento PDF/A.

**Recuperar información sobre el documento PDF**

Después de crear el cliente del servicio DocConverter, hacer referencia al documento PDF y establecer las opciones de tiempo de ejecución, puede determinar si el documento PDF es un documento compatible con PDF/A.

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

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `DocConverterServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Referencia a un documento PDF utilizado para determinar la conformidad con PDF/A

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF que se va a convertir utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Definición de opciones de tiempo de ejecución

   * Cree un objeto `PDFAValidationOptionSpec` utilizando su constructor.
   * Establezca el nivel de cumplimiento invocando el método `PDFAValidationOptionSpec` del objeto `setCompliance` y pasando `PDFAValidationOptionSpec.Compliance.PDFA_1B`.
   * Establezca el nivel de seguimiento de la información invocando el método `PDFAValidationOptionSpec` del objeto `setLogLevel` y pasando un valor de cadena que especifica el nivel de seguimiento. Por ejemplo, pase el valor `FINE`. Para obtener información sobre los diferentes valores, consulte el método `setLogLevel` en la [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Recuperar información sobre el documento PDF

   Determine la compatibilidad con PDF/A invocando el método `DocConverterServiceClient` del objeto `isPDFA` y pasando los valores siguientes:

   * El objeto `com.adobe.idp.Document` que contiene el documento PDF.
   * El objeto `PDFAValidationOptionSpec` que especifica las opciones de tiempo de ejecución.

   El método `isPDFA` devuelve un objeto `PDFAValidationResult` que contiene los resultados de esta operación.

**Consulte también**

[Uso de Documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Inicio rápido (modo SOAP): Determinación de la compatibilidad con PDF/A mediante la API de Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinar la compatibilidad con PDF/A mediante la API de servicio Web {#determine-pdf-a-compliancy-using-the-web-service-api}

Determinar la compatibilidad con PDF/A mediante la API de servicio Web:

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que utilice el WSDL DocConverter.
   * Haga referencia al ensamblado de cliente de Microsoft .NET.

1. Crear un cliente DocConvert

   * Mediante el ensamblado de cliente de Microsoft .NET, cree un objeto `DocConverterServiceService` invocando su constructor predeterminado.
   * Establezca el miembro de datos `DocConverterServiceService` del objeto `Credentials` con un valor `System.Net.NetworkCredential` que especifique el nombre de usuario y el valor de la contraseña.

1. Referencia a un documento PDF utilizado para determinar la conformidad con PDF/A

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el documento PDF que se convierte en un documento PDF/A.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF y el modo en el que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando su propiedad `binaryData` con el contenido de la matriz de bytes.

1. Definición de opciones de tiempo de ejecución

   * Cree un objeto `PDFAValidationOptionSpec` utilizando su constructor.
   * Establezca el nivel de cumplimiento asignando el miembro de datos `PDFAValidationOptionSpec` del objeto `compliance` con el valor `PDFAConversionOptionSpec_Compliance.PDFA_1B`.
   * Establezca el nivel de seguimiento de la información asignando el miembro de datos `PDFAValidationOptionSpec` del objeto `resultLevel` con el valor `PDFAValidationOptionSpec_ResultLevel.DETAILED`.

1. Recuperar información sobre el documento PDF

   Determine la compatibilidad con PDF/A invocando el método `DocConverterServiceService` del objeto `isPDFA` y pasando los valores siguientes:

   * El objeto `BLOB` que contiene el documento PDF.
   * El objeto `PDFAValidationOptionSpec` que contiene opciones de tiempo de ejecución.

   El método `isPDFA` devuelve un objeto `PDFAValidationResult` que contiene los resultados de esta operación.

**Consulte también**

[Uso de Documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
