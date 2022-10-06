---
title: Uso de utilidades de PDF
seo-title: Working with PDF Utilities
description: Utilice el servicio Utilidades de PDF para convertir entre los formatos de archivo PDF y XDP, establecer y recuperar propiedades de documento de PDF y manipular metadatos de XMP.
seo-description: Use the PDF Utilities service to convert between PDF and XDP file formats, set and retrieve PDF document properties, and manipulate XMP metadata.
uuid: a2ea2359-c547-4f1b-b6ca-f276f816e36a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d816bf2e-5236-4084-b7c4-c32b72cdff97
role: Developer
exl-id: e4b204ee-7261-42b8-8db8-a92aa9fd0a28
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2579'
ht-degree: 1%

---

# Uso de utilidades de PDF {#working-with-pdf-utilities}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

**Acerca del Servicio de Utilidades del PDF**

El servicio Utilidades de PDF puede convertir entre los formatos de archivo PDF y XDP, establecer y recuperar propiedades de documento de PDF y manipular metadatos de XMP. Por ejemplo, antes de convertir un documento de PDF a otro formato, es útil inspeccionar sus propiedades para determinar qué operación de servicio invocar para la conversión.

Puede realizar estas tareas mediante el servicio PDF Utilities:

* Convierta documentos PDF en documentos XDP.
* Convierta documentos XDP en documentos PDF. (Consulte [Conversión de documentos XDP en documentos de PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents).)
* Recupere las propiedades del documento del PDF. (Consulte [Recuperación de las propiedades del documento PDF](pdf-utilities.md#retrieving-pdf-document-properties).)
* Guarde un documento PDF y optimícelo para una visualización web rápida. (Consulte [Configuración de los modos de guardado de documentos del PDF](pdf-utilities.md#setting-pdf-document-save-modes).)

>[!NOTE]
>
>Para obtener más información sobre el servicio PDF Utilities, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversión de documentos PDF en documentos XDP {#converting-pdf-documents-into-xdp-documents}

Puede utilizar las API de servicio web y Java de PDF Utilities para convertir mediante programación documentos PDF en documentos XDP.

>[!NOTE]
>
>Para obtener más información sobre el servicio PDF Utilities, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para convertir un documento PDF en un documento XDP, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente PDFUtilityService.
1. Invoque el PDF a la operación de conversión XDP.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un cliente PDFUtilityService**

Para poder realizar una operación de PDF Utilidades mediante programación, debe crear un cliente PDFUtilityService. Con la API de Java, esto se consigue creando un `PDFUtilityServiceClient` objeto. Con la API del servicio web, esto se logra mediante el uso de un `PDFUtilityServiceService` objeto.

**Invocar al PDF a la operación de conversión XDP**

Después de crear el cliente de servicio, puede invocar el PDF a la operación de conversión XDP.

**Consulte también lo siguiente**

[Conversión de documentos PDF en documentos XDP mediante la API de Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Conversión de documentos PDF en documentos XDP mediante la API de servicio web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de documentos PDF en documentos XDP mediante la API de Java {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

Convierta documentos PDF en documentos XDP usando la API de PDF Utilities (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-pdfutility-client.jar, en la ruta de clase de su proyecto Java.

1. Creación de un cliente PDFUtilityService

   Cree un `PDFUtilityServiceClient` usando su constructor y pasando un `ServiceClientFactory` objeto que contiene propiedades de conexión.

1. Invocar al PDF a la operación de conversión XDP

   Para realizar la conversión, invoque la función `PDFUtilityServiceClient` del objeto `convertPDFtoXDP` método y pasar un `com.adobe.idp.Document` que representa el archivo PDF. El método devuelve un valor `com.adobe.idp.Document` que representa el archivo XDP recién creado.

**Consulte también lo siguiente**

[Conversión de documentos PDF en documentos XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de documentos PDF en documentos XDP mediante la API de servicio web {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

Convierta documentos PDF en documentos XDP utilizando la API de utilidades de PDF (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el archivo WSDL del servicio de utilidades del PDF.
   * Haga referencia al ensamblado del cliente Microsoft .NET.

1. Creación de un cliente PDFUtilityService

   Cree un `PDFUtilityServiceService` usando el constructor de clase proxy.

1. Invocar al PDF a la operación de conversión XDP

   Invocar el `PDFUtilityServiceService` del objeto `convertPDFtoXDP` método y pasar un `BLOB` que representa el archivo PDF. El método devuelve un valor `BLOB` que representa el archivo XDP recién creado.

**Consulte también lo siguiente**

[Conversión de documentos PDF en documentos XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Conversión de documentos XDP en documentos de PDF {#converting-xdp-documents-into-pdf-documents}

Puede utilizar las API de servicio web y Java de PDF Utilities para convertir mediante programación documentos XDP en documentos PDF.

>[!NOTE]
>
>Para obtener más información sobre el servicio PDF Utilities, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para convertir un documento XDP en un documento PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente PDFUtilityService.
1. Invoque el XDP a la operación de conversión de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un cliente PDFUtilityService**

Para poder realizar una operación de PDF Utilidades mediante programación, debe crear un cliente PDFUtilityService. Con la API de Java, esto se consigue creando un `PDFUtilityServiceClient` objeto. Con la API del servicio web, esto se logra mediante el uso de un `PDFUtilityServiceService` objeto.

**Invocar la operación de conversión de XDP a PDF**

Después de crear el cliente de servicio, puede invocar el XDP a la operación de conversión de PDF.

**Consulte también lo siguiente**

[Conversión de documentos XDP en documentos de PDF mediante la API de Java](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[Conversión de documentos XDP en documentos de PDF mediante la API de servicio web](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de documentos XDP en documentos de PDF mediante la API de Java {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

Convierta documentos XDP en documentos de PDF mediante la API de utilidades de PDF (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-pdfutility-client.jar, en la ruta de clase del proyecto Java.

1. Creación de un cliente PDFUtilityService

   Cree un `PDFUtilityServiceClient` usando su constructor y pasando un `ServiceClientFactory` objeto que contiene propiedades de conexión.

1. Invocar la operación de conversión de XDP a PDF

   Para realizar la conversión, invoque la función `PDFUtilityServiceClient` del objeto `convertXDPtoPDF` método y pasar un `com.adobe.idp.Document` que representa el archivo XDP. El método devuelve un valor `com.adobe.idp.Document` que representa el archivo PDF recién creado.

**Consulte también lo siguiente**

[Conversión de documentos XDP en documentos de PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de documentos XDP en documentos de PDF mediante la API de servicio web {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

Convierta documentos XDP en documentos de PDF mediante la API de utilidades de PDF (API de servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el archivo WSDL del servicio de utilidades del PDF.
   * Haga referencia al ensamblado del cliente Microsoft .NET.

1. Creación de un cliente PDFUtilityService

   Cree un `PDFUtilityServiceService` usando el constructor de clase proxy.

1. Invocar la operación de conversión de XDP a PDF

   Para realizar la conversión, invoque la función `PDFUtilityServiceService` del objeto `convertXDPtoPDF` método y pasar un `BLOB` que representa el archivo XDP. El método devuelve un valor `BLOB` que representa el archivo PDF recién creado.

**Consulte también lo siguiente**

[Conversión de documentos XDP en documentos de PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Recuperación de las propiedades del documento PDF {#retrieving-pdf-document-properties}

Puede utilizar las API de servicios web y Java de utilidades de PDF para recuperar mediante programación las propiedades del documento de PDF, como si el documento es un formulario que se puede rellenar o la versión mínima de Acrobat necesaria para leer el documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio PDF Utilities, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Resumen de los pasos {#summary_of_steps-2}

Para recuperar las propiedades del documento del PDF, realice los pasos siguientes:

1. Incluir archivos de proyecto.
1. Cree un cliente PDFUtilityService.
1. Invoque la operación de recuperación de propiedades.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un cliente PDFUtilityService**

Para poder realizar una operación de PDF Utilidades mediante programación, debe crear un cliente PDFUtilityService. Con la API de Java, esto se consigue creando un `PDFUtilityServiceClient` objeto. Con la API del servicio web, esto se lleva a cabo mediante un `PDFUtilityServiceService` objeto.

**Invocar la operación de recuperación de propiedades**

Después de crear el cliente de servicio, puede invocar la operación de recuperación de propiedades.

**Consulte también lo siguiente**

[Recuperar propiedades de documento del PDF mediante la API de Java](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[Recuperar propiedades de documento del PDF mediante la API de servicio web](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar propiedades de documento del PDF mediante la API de Java {#retrieve-pdf-document-properties-using-the-java-api}

Recupere las propiedades del documento del PDF mediante la API de utilidades del PDF (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-pdfutility-client.jar, en la ruta de clase del proyecto Java.

1. Creación de un cliente PDFUtilityService

   Cree un `PDFUtilityServiceClient` usando su constructor y pasando un `ServiceClientFactory` objeto que contiene propiedades de conexión.

1. Invocar la operación de recuperación de propiedades

   Para realizar la conversión, invoque la función `PDFUtilityServiceClient` del objeto `getPDFProperties` y pase lo siguiente:

   * A `com.adobe.idp.Document` que representa el documento PDF.
   * A `PDFPropertiesOptionSpec` que contiene las propiedades que se van a evaluar.

   El método devuelve un valor `PDFPropertiesResult` que contiene los resultados de la consulta.

**Consulte también lo siguiente**

[Recuperación de las propiedades del documento PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar propiedades de documento del PDF mediante la API de servicio web {#retrieve-pdf-document-properties-using-the-web-service-api}

Recupere las propiedades del documento del PDF mediante la API del servicio web de utilidades del PDF:

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el archivo WSDL del servicio de utilidades del PDF.
   * Haga referencia al ensamblado del cliente Microsoft .NET.

1. Creación de un cliente PDFUtilityService

   Cree un `PDFUtilityServiceService` usando el constructor de clase proxy.

1. Invocar la operación de recuperación de propiedades

   Para realizar la conversión, invoque la función `PDFUtilityServiceService` del objeto `getPDFProperties` y pase lo siguiente:

   * A `BLOB` que representa el documento PDF.
   * A `PDFPropertiesOptionSpec` que contiene las propiedades que se van a evaluar.

   El método devuelve un valor `PDFPropertiesResult` que contiene los resultados de la consulta.

**Consulte también lo siguiente**

[Recuperación de las propiedades del documento PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Configuración de los modos de guardado de documentos del PDF {#setting-pdf-document-save-modes}

Puede utilizar el servicio PDF Utilities Java y las API de servicio web para establecer mediante programación un modo de guardado para un documento PDF. Al utilizar el servicio Utilidades del PDF para establecer un modo de guardado, el servicio Utilidades del PDF solo establece el modo de guardado y no guarda realmente el documento del PDF. El documento del PDF se guarda cuando se pasa a otra operación de servicio. Por ejemplo, puede utilizar el servicio PDF Utilities para establecer un modo de guardado específico y pasarlo al servicio Encryption , donde el documento PDF se guarda y se cifra.

>[!NOTE]
>
>Para obtener más información sobre el servicio PDF Utilities, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-3}

Para definir la opción de guardar para documentos del PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente PDFUtilityService.
1. Establezca el modo de guardado.
1. Invoque la operación de guardado.
1. Pase el documento del PDF a otra operación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un cliente PDFUtilityService**

Para poder realizar una operación de PDF Utilidades mediante programación, debe crear un cliente PDFUtilityService. Con la API de Java, esto se consigue creando un `PDFUtilityServiceClient` objeto. Con la API del servicio web, esto se lleva a cabo mediante un `PDFUtilityServiceService` objeto.

**Definir el modo Guardar**

Puede elegir una de las siguientes opciones de guardado:

* `INCREMENTAL`: Para ahorrar de manera incremental a fin de reducir el tiempo necesario para ahorrar
* `FAST_WEB_VIEW`: guardar para una visualización rápida de la web
* `FULL`: Para guardar con un guardado completo (sin optimizaciones)

**Invocar la operación Guardar estilo**

Después de crear el cliente de servicio, puede invocar la operación de recuperación de propiedades.

**Pasar el documento del PDF a otra operación de AEM Forms**

Una vez que el servicio Utilidades del PDF establece el modo Guardar especificado, pase el documento del PDF a otra operación de AEM Forms. Una vez devuelta la operación, el documento del PDF se guarda en el modo especificado. Por ejemplo, si utiliza el servicio Utilidades del PDF para establecer la variable `FAST_WEB_VIEW` y, a continuación, pase el documento del PDF al `encryptUsingPassword` , el documento PDF devuelto se cifra con una contraseña y se guarda en la `FAST_WEB_VIEW` en el menú contextual.

>[!NOTE]
>
>El inicio rápido asociado a esta sección establece la variable `FAST_WEB_VIEW` y, a continuación, pasa el documento del PDF al `encryptUsingPassword` operación.

**Consulte también lo siguiente**

[Establecer las opciones de guardado del documento del PDF mediante la API de Java](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[Establecer las opciones de guardado del documento del PDF mediante la API de servicio web](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Codificación de documentos del PDF con una contraseña](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Establecer las opciones de guardado del documento del PDF mediante la API de Java {#set-pdf-document-save-options-using-the-java-api}

Establezca las opciones de guardado del documento del PDF mediante la API de utilidades del PDF (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-pdfutility-client.jar, en la ruta de clase del proyecto Java.

1. Creación de un cliente PDFUtilityService

   Cree un `PDFUtilityServiceClient` usando su constructor y pasando un `ServiceClientFactory` objeto que contiene propiedades de conexión.

1. Definir el modo Guardar

   * Cree un `PDFUtilitySaveMode` usando su constructor.
   * Configure el modo de guardado invocando la variable `PDFUtilitySaveMode` del objeto `setSaveStyle` y pasando un valor de cadena que especifica el modo de guardado. Por ejemplo, para guardar y ver rápidamente la web, pase `FAST_WEB_VIEW`.

1. Invocar la operación Guardar estilo

   Invocar el `PDFUtilityServiceClient` del objeto `setSaveMode` y pase los siguientes valores:

   * A `com.adobe.idp.Document` que representa el documento PDF.
   * A `PDFUtilitySaveMode` objeto que contiene el estilo de guardado que se va a utilizar.
   * Un valor booleano que se utiliza para determinar si se va a anular la configuración anterior.

   El método devuelve un valor `com.adobe.idp.Document` objeto formateado con el estilo de guardado especificado.

1. Pasar el documento del PDF a otra operación de AEM Forms

   * Pase el `com.adobe.idp.Document` a otra operación de AEM Forms.

**Consulte también lo siguiente**

[Configuración de los modos de guardado de documentos del PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Establecer las opciones de guardado del documento del PDF mediante la API de servicio web {#set-pdf-document-save-options-using-the-web-service-api}

Establezca las opciones de guardado del documento del PDF mediante el AP (servicio Web) de Utilidades del PDF:

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el archivo WSDL del servicio de utilidades del PDF.
   * Haga referencia al ensamblado del cliente Microsoft .NET.

1. Creación de un cliente PDFUtilityService

   Cree un `PDFUtilityServiceService` usando el constructor de clase proxy.

1. Definir el modo Guardar

   * Cree un `PDFUtilitySaveMode` usando su constructor.
   * Configure el modo de guardado asignando un valor de cadena a la variable `PDFUtilitySaveMode` del objeto `saveStyle` método que especifica el modo de guardado. Por ejemplo, para guardar y ver rápidamente la web, especifique `FAST_WEB_VIEW`.

1. Invocar la operación Guardar estilo

   Invocar el `PDFUtilityServiceService` del objeto `setSaveMode` y pase los siguientes valores:

   * A `BLOB` que representa el documento PDF.
   * A `PDFUtilitySaveMode` objeto que contiene el estilo de guardado que se va a utilizar.
   * Un valor booleano que se utiliza para determinar si se va a anular la configuración anterior.

   El método devuelve un valor `BLOB` objeto formateado con el estilo de guardado especificado. A continuación, puede guardar ese objeto como un documento PDF.

1. Pasar el documento del PDF a otra operación de Forms

   * Pase el `BLOB` a otra operación de AEM Forms.

**Consulte también lo siguiente**

[Configuración de los modos de guardado de documentos del PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Sanitización de documentos PDF {#sanitizing-pdf-documents}

Puede utilizar las API de Java de utilidades de PDF para convertir mediante programación documentos PDF en documentos XDP.

>[!NOTE]
>
>Para obtener más información sobre el servicio PDF Utilities, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-4}

Para sanear el documento del PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente PDFUtilityService.
1. Invoque la operación de saneamiento.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Para crear una aplicación cliente utilizando Java, incluya los archivos JAR necesarios.

**Creación de un cliente PDFUtilityService**

Antes de realizar una operación de sanización mediante programación, debe crear un cliente PDFUtilityService. Con la API de Java, esto se consigue creando un `PDFUtilityServiceClient` objeto.

**Invocar al PDF a la operación de conversión XDP**

Después de crear el cliente de servicio, puede invocar la operación de sanización.

**Consulte también lo siguiente**

[Conversión de documentos PDF en documentos XDP mediante la API de Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Conversión de documentos PDF en documentos XDP mediante la API de servicio web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Sanear documentos del PDF mediante la API de Java {#sanitize-pdf-documents-using-the-java-api}

Sanice los documentos utilizando la API de PDF Utilities (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-pdfutility-client.jar, en la ruta de clase del proyecto Java.

1. Creación de un cliente PDFUtilityService

   Cree un `PDFUtilityServiceClient` usando su constructor y pasando un `ServiceClientFactory` objeto que contiene propiedades de conexión.

1. Invocar al PDF a la operación de conversión XDP

   Para realizar la conversión, invoque la función `PDFUtilityServiceClient` del objeto `convertPDFtoXDP` método y pasar un `com.adobe.idp.Document` que representa el archivo PDF. El método devuelve un valor `com.adobe.idp.Document` que representa el archivo XDP recién creado.

**Consulte también lo siguiente**

[Sanitización de documentos PDF](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
