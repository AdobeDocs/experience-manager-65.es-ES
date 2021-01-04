---
title: Uso de las utilidades de PDF
seo-title: Uso de las utilidades de PDF
description: Utilice el servicio de utilidades de PDF para convertir entre formatos de archivo PDF y XDP, establecer y recuperar propiedades de documento de PDF y manipular metadatos de XMP.
seo-description: Utilice el servicio de utilidades de PDF para convertir entre formatos de archivo PDF y XDP, establecer y recuperar propiedades de documento de PDF y manipular metadatos de XMP.
uuid: a2ea2359-c547-4f1b-b6ca-f276f816e36a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d816bf2e-5236-4084-b7c4-c32b72cdff97
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '2592'
ht-degree: 1%

---


# Uso de las utilidades de PDF {#working-with-pdf-utilities}

**Acerca del servicio de utilidades de PDF**

El servicio Utilidades de PDF puede convertir entre formatos de archivo PDF y XDP, establecer y recuperar propiedades de documento PDF y manipular metadatos de XMP. Por ejemplo, antes de convertir un documento PDF a otro formato, resulta útil inspeccionar sus propiedades para determinar qué operación de servicio se va a invocar para la conversión.

Puede realizar estas tareas mediante el servicio Utilidades de PDF:

* Convertir documentos PDF en documentos XDP.
* Convertir documentos XDP en documentos PDF. (Consulte [Conversión de Documentos XDP en Documentos PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)).
* Recupere las propiedades del documento PDF. (Consulte [Recuperación de propiedades de Documento PDF](pdf-utilities.md#retrieving-pdf-document-properties).)
* Guarde un documento PDF y optimícelo para una visualización rápida de la Web. (Consulte [Configuración de los modos de guardado de Documento PDF](pdf-utilities.md#setting-pdf-document-save-modes)).

>[!NOTE]
>
>Para obtener más información sobre el servicio de utilidades de PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversión de Documentos PDF en Documentos XDP {#converting-pdf-documents-into-xdp-documents}

Puede utilizar las API de servicio web y Java de Utilidades de PDF para convertir documentos PDF en documentos XDP mediante programación.

>[!NOTE]
>
>Para obtener más información sobre el servicio de utilidades de PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para convertir un documento PDF en un documento XDP, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente PDFUtilityService.
1. Invoque la operación de conversión de PDF a XDP.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Crear un cliente PDFUtilityService**

Para poder realizar mediante programación una operación de Utilidades PDF, debe crear un cliente PDFUtilityService. Con la API de Java, esto se logra creando un objeto `PDFUtilityServiceClient`. Con la API de servicio Web, esto se logra mediante el uso de un objeto `PDFUtilityServiceService`.

**Invocar la operación de conversión de PDF a XDP**

Después de crear el cliente de servicio, puede invocar la operación de conversión PDF a XDP.

**Consulte también**

[Convertir documentos PDF en documentos XDP mediante la API de Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Convertir documentos PDF en documentos XDP mediante la API de servicio web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir documentos PDF en documentos XDP mediante la API de Java {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

Convertir documentos PDF en documentos XDP mediante la API de utilidades de PDF (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-pdfutility-client.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente PDFUtilityService

   Cree un objeto `PDFUtilityServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Invocar la operación de conversión de PDF a XDP

   Para realizar la conversión, invoque el método `PDFUtilityServiceClient` del objeto `convertPDFtoXDP` y pase un objeto `com.adobe.idp.Document` que represente el archivo PDF. El método devuelve un objeto `com.adobe.idp.Document` que representa el archivo XDP recién creado.

**Consulte también**

[Conversión de Documentos PDF en Documentos XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir documentos PDF en documentos XDP mediante la API de servicio Web {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

Convertir documentos PDF en documentos XDP mediante la API de utilidades de PDF (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que utilice el archivo WSDL del servicio de utilidades de PDF.
   * Haga referencia al ensamblado de cliente de Microsoft .NET.

1. Crear un cliente PDFUtilityService

   Cree un objeto `PDFUtilityServiceService` mediante el constructor de la clase proxy.

1. Invocar la operación de conversión de PDF a XDP

   Invoque el método `PDFUtilityServiceService` del objeto `convertPDFtoXDP` y pase un objeto `BLOB` que represente el archivo PDF. El método devuelve un objeto `BLOB` que representa el archivo XDP recién creado.

**Consulte también**

[Conversión de Documentos PDF en Documentos XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Conversión de Documentos XDP en Documentos PDF {#converting-xdp-documents-into-pdf-documents}

Puede utilizar las API de servicio Web y Java de Utilidades PDF para convertir documentos XDP en documentos PDF mediante programación.

>[!NOTE]
>
>Para obtener más información sobre el servicio de utilidades de PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para convertir un documento XDP en un documento PDF, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente PDFUtilityService.
1. Invoque la operación de conversión de XDP a PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Crear un cliente PDFUtilityService**

Para poder realizar mediante programación una operación de Utilidades PDF, debe crear un cliente PDFUtilityService. Con la API de Java, esto se logra creando un objeto `PDFUtilityServiceClient`. Con la API de servicio Web, esto se logra mediante el uso de un objeto `PDFUtilityServiceService`.

**Invocar la operación de conversión XDP a PDF**

Después de crear el cliente de servicio, puede invocar la operación de conversión XDP a PDF.

**Consulte también**

[Convertir documentos XDP en documentos PDF mediante la API de Java](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[Conversión de documentos XDP en documentos PDF mediante la API de servicio web](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir documentos XDP en documentos PDF mediante la API de Java {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

Convertir documentos XDP en documentos PDF mediante la API de utilidades de PDF (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-pdfutility-client.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente PDFUtilityService

   Cree un objeto `PDFUtilityServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Invocar la operación de conversión XDP a PDF

   Para realizar la conversión, invoque el método `PDFUtilityServiceClient` del objeto `convertXDPtoPDF` y pase un objeto `com.adobe.idp.Document` que represente el archivo XDP. El método devuelve un objeto `com.adobe.idp.Document` que representa el archivo PDF recién creado.

**Consulte también**

[Conversión de Documentos XDP en Documentos PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de documentos XDP en documentos PDF mediante la API de servicio Web {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

Convertir documentos XDP en documentos PDF mediante la API de utilidades de PDF (servicio Web API):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que utilice el archivo WSDL del servicio de utilidades de PDF.
   * Haga referencia al ensamblado de cliente de Microsoft .NET.

1. Crear un cliente PDFUtilityService

   Cree un objeto `PDFUtilityServiceService` mediante el constructor de la clase proxy.

1. Invocar la operación de conversión XDP a PDF

   Para realizar la conversión, invoque el método `PDFUtilityServiceService` del objeto `convertXDPtoPDF` y pase un objeto `BLOB` que represente el archivo XDP. El método devuelve un objeto `BLOB` que representa el archivo PDF recién creado.

**Consulte también**

[Conversión de Documentos XDP en Documentos PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Recuperando propiedades de Documento PDF {#retrieving-pdf-document-properties}

Puede utilizar las API de servicio Web y Java de Utilidades PDF para recuperar mediante programación las propiedades de documento PDF, como si el documento es un formulario rellenable o la versión mínima de Acrobat necesaria para leer el documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio de utilidades de PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Resumen de los pasos {#summary_of_steps-2}

Para recuperar las propiedades del documento PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente PDFUtilityService.
1. Invocar la operación de recuperación de propiedades.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Crear un cliente PDFUtilityService**

Para poder realizar mediante programación una operación de Utilidades PDF, debe crear un cliente PDFUtilityService. Con la API de Java, esto se logra creando un objeto `PDFUtilityServiceClient`. Con la API de servicio Web, esto se logra mediante un objeto `PDFUtilityServiceService`.

**Invocar la operación de recuperación de propiedades**

Después de crear el cliente de servicio, puede invocar la operación de recuperación de propiedades.

**Consulte también**

[Recuperar propiedades de documento PDF mediante la API de Java](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[Recuperar propiedades de documento PDF mediante la API de servicio Web](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar propiedades de documento PDF mediante la API de Java {#retrieve-pdf-document-properties-using-the-java-api}

Recupere las propiedades del documento PDF mediante la API de utilidades de PDF (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-pdfutility-client.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente PDFUtilityService

   Cree un objeto `PDFUtilityServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Invocar la operación de recuperación de propiedades

   Para realizar la conversión, invoque el método `PDFUtilityServiceClient` del objeto `getPDFProperties` y pase lo siguiente:

   * Un objeto `com.adobe.idp.Document` que representa el documento PDF.
   * Un objeto `PDFPropertiesOptionSpec` que contiene las propiedades que se van a evaluar.

   El método devuelve un objeto `PDFPropertiesResult` que contiene los resultados de la consulta.

**Consulte también**

[Recuperación de propiedades de Documento PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar propiedades de documento PDF mediante la API de servicio Web {#retrieve-pdf-document-properties-using-the-web-service-api}

Recupere las propiedades del documento PDF mediante la API del servicio web de Utilidades PDF:

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que utilice el archivo WSDL del servicio de utilidades de PDF.
   * Haga referencia al ensamblado de cliente de Microsoft .NET.

1. Crear un cliente PDFUtilityService

   Cree un objeto `PDFUtilityServiceService` mediante el constructor de la clase proxy.

1. Invocar la operación de recuperación de propiedades

   Para realizar la conversión, invoque el método `PDFUtilityServiceService` del objeto `getPDFProperties` y pase lo siguiente:

   * Un objeto `BLOB` que representa el documento PDF.
   * Un objeto `PDFPropertiesOptionSpec` que contiene las propiedades que se van a evaluar.

   El método devuelve un objeto `PDFPropertiesResult` que contiene los resultados de la consulta.

**Consulte también**

[Recuperación de propiedades de Documento PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Configuración de los modos de guardado de Documento PDF {#setting-pdf-document-save-modes}

Puede utilizar el servicio de utilidades de PDF Java y las API de servicio Web para establecer mediante programación un modo de guardado para un documento PDF. Al utilizar el servicio Utilidades PDF para establecer un modo de guardado, el servicio Utilidades PDF solo establece el modo de guardado y no guarda el documento PDF. El documento PDF se guarda cuando se pasa a otra operación de servicio. Por ejemplo, puede utilizar el servicio Utilidades PDF para establecer un modo de guardado específico y pasarlo al servicio Cifrado, donde el documento PDF se guarda y se cifra.

>[!NOTE]
>
>Para obtener más información sobre el servicio de utilidades de PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-3}

Para definir la opción de guardar para documentos PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente PDFUtilityService.
1. Establezca el modo de guardado.
1. Invocar la operación de guardado.
1. Pase el documento PDF a otra operación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Crear un cliente PDFUtilityService**

Para poder realizar mediante programación una operación de Utilidades PDF, debe crear un cliente PDFUtilityService. Con la API de Java, esto se logra creando un objeto `PDFUtilityServiceClient`. Con la API de servicio Web, esto se logra mediante un objeto `PDFUtilityServiceService`.

**Definir el modo Guardar**

Puede elegir una de las siguientes opciones de guardado:

* `INCREMENTAL`:: Para ahorrar de forma incremental a fin de reducir el tiempo necesario para ahorrar
* `FAST_WEB_VIEW`:: guardar para una visualización rápida de Web
* `FULL`:: Para guardar con un almacenamiento completo (sin optimizaciones)

**Invocar la operación de guardar estilo**

Después de crear el cliente de servicio, puede invocar la operación de recuperación de propiedades.

**Pasar el documento PDF a otra operación de AEM Forms**

Una vez que el servicio Utilidades PDF establece el modo Guardar especificado, pase el documento PDF a otra operación de AEM Forms. Una vez devuelta la operación, el documento PDF se guarda en el modo especificado. Por ejemplo, si utiliza el servicio Utilidades de PDF para establecer el modo `FAST_WEB_VIEW` y luego pasar el documento PDF a la operación `encryptUsingPassword` del servicio de cifrado, el documento de PDF devuelto se cifrará con una contraseña y se guardará en el modo `FAST_WEB_VIEW`.

>[!NOTE]
>
>El Inicio rápido asociado con esta sección establece el modo `FAST_WEB_VIEW` y, a continuación, pasa el documento PDF a la operación `encryptUsingPassword` del servicio de cifrado.

**Consulte también**

[Definir las opciones de guardado del documento PDF mediante la API de Java](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[Establecer las opciones de guardado de documento PDF mediante la API de servicio Web](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Cifrado de Documentos PDF con contraseña](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Configure las opciones de guardado del documento PDF mediante la API de Java {#set-pdf-document-save-options-using-the-java-api}

Configure las opciones de guardado del documento PDF mediante la API de utilidades de PDF (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-pdfutility-client.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente PDFUtilityService

   Cree un objeto `PDFUtilityServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Definir el modo Guardar

   * Cree un objeto `PDFUtilitySaveMode` utilizando su constructor.
   * Establezca el modo de guardado invocando el método `PDFUtilitySaveMode` del objeto `setSaveStyle` y pasando un valor de cadena que especifica el modo de guardado. Por ejemplo, para guardar y ver rápidamente la Web, pase `FAST_WEB_VIEW`.

1. Invocar la operación de guardar estilo

   Invoque el método `PDFUtilityServiceClient` del objeto `setSaveMode` y pase los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que representa el documento PDF.
   * Un objeto `PDFUtilitySaveMode` que contiene el estilo de guardado que se va a utilizar.
   * Un valor booleano que se utiliza para determinar si se debe anular cualquier configuración anterior.

   El método devuelve un objeto `com.adobe.idp.Document` con formato mediante el estilo de guardado especificado.

1. Pasar el documento PDF a otra operación de AEM Forms

   * Pase el objeto `com.adobe.idp.Document` devuelto a otra operación de AEM Forms.

**Consulte también**

[Configuración de los modos de guardado de Documento PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Configure las opciones de guardado del documento PDF mediante la API de servicio Web {#set-pdf-document-save-options-using-the-web-service-api}

Defina las opciones de guardado del documento PDF mediante el AP de Utilidades PDF (servicio Web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que utilice el archivo WSDL del servicio de utilidades de PDF.
   * Haga referencia al ensamblado de cliente de Microsoft .NET.

1. Crear un cliente PDFUtilityService

   Cree un objeto `PDFUtilityServiceService` mediante el constructor de la clase proxy.

1. Definir el modo Guardar

   * Cree un objeto `PDFUtilitySaveMode` utilizando su constructor.
   * Establezca el modo de guardado asignando un valor de cadena al método `PDFUtilitySaveMode` del objeto `saveStyle` que especifica el modo de guardado. Por ejemplo, para guardar para una visualización rápida de Web, especifique `FAST_WEB_VIEW`.

1. Invocar la operación de guardar estilo

   Invoque el método `PDFUtilityServiceService` del objeto `setSaveMode` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento PDF.
   * Un objeto `PDFUtilitySaveMode` que contiene el estilo de guardado que se va a utilizar.
   * Un valor booleano que se utiliza para determinar si se debe anular cualquier configuración anterior.

   El método devuelve un objeto `BLOB` con formato mediante el estilo de guardado especificado. A continuación, puede guardar ese objeto como un documento PDF.

1. Pasar el documento PDF a otra operación de Forms

   * Pase el objeto `BLOB` devuelto a otra operación de AEM Forms.

**Consulte también**

[Configuración de los modos de guardado de Documento PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Sanitización de Documentos PDF {#sanitizing-pdf-documents}

Puede utilizar las API de Java de Utilidades de PDF para convertir documentos PDF en documentos XDP mediante programación.

>[!NOTE]
>
>Para obtener más información sobre el servicio de utilidades de PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-4}

Para sanear el documento PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente PDFUtilityService.
1. Invoque la operación de limpieza.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Para crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios.

**Crear un cliente PDFUtilityService**

Antes de realizar una operación de saneamiento mediante programación, debe crear un cliente PDFUtilityService. Con la API de Java, esto se logra creando un objeto `PDFUtilityServiceClient`.

**Invocar la operación de conversión de PDF a XDP**

Después de crear el cliente de servicio, puede invocar la operación de saneamiento.

**Consulte también**

[Convertir documentos PDF en documentos XDP mediante la API de Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Convertir documentos PDF en documentos XDP mediante la API de servicio web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Optimizar documentos PDF mediante la API de Java {#sanitize-pdf-documents-using-the-java-api}

Sanear documentos mediante la API de utilidades de PDF (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-pdfutility-client.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente PDFUtilityService

   Cree un objeto `PDFUtilityServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Invocar la operación de conversión de PDF a XDP

   Para realizar la conversión, invoque el método `PDFUtilityServiceClient` del objeto `convertPDFtoXDP` y pase un objeto `com.adobe.idp.Document` que represente el archivo PDF. El método devuelve un objeto `com.adobe.idp.Document` que representa el archivo XDP recién creado.

**Consulte también**

[Anidación de documentos PDF](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
