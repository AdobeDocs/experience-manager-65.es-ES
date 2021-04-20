---
title: Uso de utilidades de PDF
seo-title: Uso de utilidades de PDF
description: Utilice el servicio Utilidades de PDF para convertir entre los formatos de archivo PDF y XDP, establecer y recuperar propiedades de documento PDF y manipular metadatos de XMP.
seo-description: Utilice el servicio Utilidades de PDF para convertir entre los formatos de archivo PDF y XDP, establecer y recuperar propiedades de documento PDF y manipular metadatos de XMP.
uuid: a2ea2359-c547-4f1b-b6ca-f276f816e36a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d816bf2e-5236-4084-b7c4-c32b72cdff97
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2607'
ht-degree: 1%

---


# Uso de utilidades de PDF {#working-with-pdf-utilities}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

**Acerca del servicio de utilidades de PDF**

El servicio Utilidades de PDF puede convertir entre los formatos de archivo PDF y XDP, establecer y recuperar propiedades de documento PDF y manipular metadatos de XMP. Por ejemplo, antes de convertir un documento PDF a otro formato, es útil inspeccionar sus propiedades para determinar qué operación de servicio invocar para la conversión.

Puede realizar estas tareas mediante el servicio Utilidades de PDF:

* Convierta documentos PDF en documentos XDP.
* Convierta documentos XDP en documentos PDF. (Consulte [Conversión de documentos XDP en documentos PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)).
* Recupere las propiedades del documento PDF. (Consulte [Recuperación de las propiedades del documento PDF](pdf-utilities.md#retrieving-pdf-document-properties)).
* Guarde un documento PDF y optimícelo para una visualización web rápida. (Consulte [Configuración de los modos de guardado de documentos PDF](pdf-utilities.md#setting-pdf-document-save-modes)).

>[!NOTE]
>
>Para obtener más información sobre el servicio de utilidades de PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversión de documentos PDF en documentos XDP {#converting-pdf-documents-into-xdp-documents}

Puede utilizar las API de servicio web y Java de utilidades de PDF para convertir mediante programación documentos PDF en documentos XDP.

>[!NOTE]
>
>Para obtener más información sobre el servicio de utilidades de PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para convertir un documento PDF en un documento XDP, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente PDFUtilityService.
1. Invoque la operación de conversión de PDF a XDP.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un cliente PDFUtilityService**

Antes de poder realizar mediante programación una operación de Utilidades PDF, debe crear un cliente PDFUtilityService. Con la API de Java, esto se consigue creando un objeto `PDFUtilityServiceClient`. Con la API de servicio web, esto se logra mediante el uso de un objeto `PDFUtilityServiceService`.

**Invocar la operación de conversión PDF a XDP**

Después de crear el cliente de servicio, puede invocar la operación de conversión PDF a XDP.

**Consulte también**

[Convertir documentos PDF en documentos XDP mediante la API de Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Convertir documentos PDF en documentos XDP mediante la API de servicio Web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de documentos PDF en documentos XDP mediante la API de Java {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

Convierta documentos PDF en documentos XDP utilizando la API de utilidades de PDF (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-pdfutility-client.jar, en la ruta de clase de su proyecto Java.

1. Creación de un cliente PDFUtilityService

   Cree un objeto `PDFUtilityServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Invocar la operación de conversión PDF a XDP

   Para realizar la conversión, invoque el método `PDFUtilityServiceClient` del objeto `convertPDFtoXDP` y pase un objeto `com.adobe.idp.Document` que represente el archivo PDF. El método devuelve un objeto `com.adobe.idp.Document` que representa el archivo XDP recién creado.

**Consulte también**

[Conversión de documentos PDF en documentos XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de documentos PDF en documentos XDP mediante la API de servicio Web {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

Convierta documentos PDF en documentos XDP utilizando la API de utilidades de PDF (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el archivo WSDL del servicio de utilidades de PDF.
   * Haga referencia al ensamblado cliente de Microsoft .NET.

1. Creación de un cliente PDFUtilityService

   Cree un objeto `PDFUtilityServiceService` utilizando su constructor de clase proxy.

1. Invocar la operación de conversión PDF a XDP

   Invoque el método `PDFUtilityServiceService` del objeto `convertPDFtoXDP` y pase un objeto `BLOB` que represente el archivo PDF. El método devuelve un objeto `BLOB` que representa el archivo XDP recién creado.

**Consulte también**

[Conversión de documentos PDF en documentos XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Conversión de documentos XDP en documentos PDF {#converting-xdp-documents-into-pdf-documents}

Puede utilizar las API de servicio web y Java de utilidades de PDF para convertir mediante programación documentos XDP en documentos PDF.

>[!NOTE]
>
>Para obtener más información sobre el servicio de utilidades de PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para convertir un documento XDP en un documento PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente PDFUtilityService.
1. Invoque la operación de conversión de XDP a PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un cliente PDFUtilityService**

Antes de poder realizar mediante programación una operación de Utilidades PDF, debe crear un cliente PDFUtilityService. Con la API de Java, esto se consigue creando un objeto `PDFUtilityServiceClient`. Con la API de servicio web, esto se logra mediante el uso de un objeto `PDFUtilityServiceService`.

**Invocar la operación de conversión de XDP a PDF**

Después de crear el cliente de servicio, puede invocar la operación de conversión de XDP a PDF.

**Consulte también**

[Conversión de documentos XDP en documentos PDF mediante la API de Java](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[Conversión de documentos XDP en documentos PDF mediante la API de servicio web](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de documentos XDP en documentos PDF mediante la API de Java {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

Convierta documentos XDP en documentos PDF utilizando la API de utilidades de PDF (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-pdfutility-client.jar, en la ruta de clase del proyecto Java.

1. Creación de un cliente PDFUtilityService

   Cree un objeto `PDFUtilityServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Invocar la operación de conversión de XDP a PDF

   Para realizar la conversión, invoque el método `PDFUtilityServiceClient` del objeto `convertXDPtoPDF` y pase un objeto `com.adobe.idp.Document` que represente el archivo XDP. El método devuelve un objeto `com.adobe.idp.Document` que representa el archivo PDF recién creado.

**Consulte también**

[Conversión de documentos XDP en documentos PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de documentos XDP en documentos PDF mediante la API de servicio Web {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

Convierta documentos XDP en documentos PDF utilizando la API de utilidades de PDF (API de servicio Web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el archivo WSDL del servicio de utilidades de PDF.
   * Haga referencia al ensamblado cliente de Microsoft .NET.

1. Creación de un cliente PDFUtilityService

   Cree un objeto `PDFUtilityServiceService` utilizando su constructor de clase proxy.

1. Invocar la operación de conversión de XDP a PDF

   Para realizar la conversión, invoque el método `PDFUtilityServiceService` del objeto `convertXDPtoPDF` y pase un objeto `BLOB` que represente el archivo XDP. El método devuelve un objeto `BLOB` que representa el archivo PDF recién creado.

**Consulte también**

[Conversión de documentos XDP en documentos PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Recuperación de las propiedades del documento PDF {#retrieving-pdf-document-properties}

Puede utilizar las API de servicio web y Java de utilidades de PDF para recuperar mediante programación las propiedades de documento PDF, como si el documento es un formulario rellenable o la versión mínima de Acrobat necesaria para leer el documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio de utilidades de PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Resumen de los pasos {#summary_of_steps-2}

Para recuperar las propiedades del documento PDF, realice los pasos siguientes:

1. Incluir archivos de proyecto.
1. Cree un cliente PDFUtilityService.
1. Invoque la operación de recuperación de propiedades.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un cliente PDFUtilityService**

Antes de poder realizar mediante programación una operación de Utilidades PDF, debe crear un cliente PDFUtilityService. Con la API de Java, esto se consigue creando un objeto `PDFUtilityServiceClient`. Con la API de servicio web, esto se logra mediante un objeto `PDFUtilityServiceService`.

**Invocar la operación de recuperación de propiedades**

Después de crear el cliente de servicio, puede invocar la operación de recuperación de propiedades.

**Consulte también**

[Recuperar propiedades de documento PDF mediante la API de Java](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[Recuperar propiedades de documento PDF mediante la API de servicio Web](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar propiedades de documento PDF mediante la API de Java {#retrieve-pdf-document-properties-using-the-java-api}

Recupere las propiedades del documento PDF utilizando la API de utilidades de PDF (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-pdfutility-client.jar, en la ruta de clase del proyecto Java.

1. Creación de un cliente PDFUtilityService

   Cree un objeto `PDFUtilityServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Invocar la operación de recuperación de propiedades

   Para realizar la conversión, invoque el método `PDFUtilityServiceClient` del objeto `getPDFProperties` y pase lo siguiente:

   * Un objeto `com.adobe.idp.Document` que representa el documento PDF.
   * Un objeto `PDFPropertiesOptionSpec` que contiene las propiedades que se van a evaluar.

   El método devuelve un objeto `PDFPropertiesResult` que contiene los resultados de la consulta.

**Consulte también**

[Recuperación de las propiedades del documento PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recupere las propiedades del documento PDF utilizando la API de servicio Web {#retrieve-pdf-document-properties-using-the-web-service-api}

Recupere las propiedades del documento PDF utilizando la API del servicio web de utilidades PDF:

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el archivo WSDL del servicio de utilidades de PDF.
   * Haga referencia al ensamblado cliente de Microsoft .NET.

1. Creación de un cliente PDFUtilityService

   Cree un objeto `PDFUtilityServiceService` utilizando su constructor de clase proxy.

1. Invocar la operación de recuperación de propiedades

   Para realizar la conversión, invoque el método `PDFUtilityServiceService` del objeto `getPDFProperties` y pase lo siguiente:

   * Un objeto `BLOB` que representa el documento PDF.
   * Un objeto `PDFPropertiesOptionSpec` que contiene las propiedades que se van a evaluar.

   El método devuelve un objeto `PDFPropertiesResult` que contiene los resultados de la consulta.

**Consulte también**

[Recuperación de las propiedades del documento PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Configuración de los modos de guardado de documentos PDF {#setting-pdf-document-save-modes}

Puede utilizar el servicio de utilidades de PDF Java y las API de servicio web para establecer mediante programación un modo de guardado para un documento PDF. Al utilizar el servicio Utilidades de PDF para establecer un modo de guardado, el servicio Utilidades de PDF solo establece el modo de guardado y no guarda realmente el documento PDF. El documento PDF se guarda cuando se pasa a otra operación de servicio. Por ejemplo, puede utilizar el servicio de utilidades de PDF para establecer un modo de guardado específico y pasarlo al servicio de codificación, donde el documento PDF se guarda y se cifra.

>[!NOTE]
>
>Para obtener más información sobre el servicio de utilidades de PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-3}

Para definir la opción de guardado para documentos PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente PDFUtilityService.
1. Establezca el modo de guardado.
1. Invoque la operación de guardado.
1. Pase el documento PDF a otra operación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un cliente PDFUtilityService**

Antes de poder realizar mediante programación una operación de Utilidades PDF, debe crear un cliente PDFUtilityService. Con la API de Java, esto se consigue creando un objeto `PDFUtilityServiceClient`. Con la API de servicio web, esto se logra mediante un objeto `PDFUtilityServiceService`.

**Definir el modo Guardar**

Puede elegir una de las siguientes opciones de guardado:

* `INCREMENTAL`: Para ahorrar de manera incremental a fin de reducir el tiempo necesario para ahorrar
* `FAST_WEB_VIEW`: guardar para una visualización rápida de la web
* `FULL`: Para guardar con un guardado completo (sin optimizaciones)

**Invocar la operación Guardar estilo**

Después de crear el cliente de servicio, puede invocar la operación de recuperación de propiedades.

**Pasar el documento PDF a otra operación de AEM Forms**

Una vez que el servicio Utilidades de PDF haya configurado el modo Guardar especificado, pase el documento PDF a otra operación de AEM Forms. Una vez devuelto desde esa operación, el documento PDF se guarda en el modo especificado. Por ejemplo, si utiliza el servicio Utilidades de PDF para establecer el modo `FAST_WEB_VIEW` y después pasar el documento PDF a la operación `encryptUsingPassword` del servicio de cifrado, el documento PDF devuelto se cifrará con una contraseña y se guardará en el modo `FAST_WEB_VIEW`.

>[!NOTE]
>
>El Inicio rápido asociado con esta sección establece el modo `FAST_WEB_VIEW` y luego pasa el documento PDF a la operación `encryptUsingPassword` del servicio de cifrado.

**Consulte también**

[Definir las opciones de guardado de documentos PDF mediante la API de Java](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[Definir las opciones de guardado de documentos PDF mediante la API de servicio Web](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Codificación de documentos PDF con contraseña](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Configure las opciones de guardado de documentos PDF utilizando la API de Java {#set-pdf-document-save-options-using-the-java-api}

Establezca las opciones de guardado del documento PDF utilizando la API de utilidades de PDF (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-pdfutility-client.jar, en la ruta de clase del proyecto Java.

1. Creación de un cliente PDFUtilityService

   Cree un objeto `PDFUtilityServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Definir el modo Guardar

   * Cree un objeto `PDFUtilitySaveMode` utilizando su constructor.
   * Establezca el modo de guardado invocando el método `PDFUtilitySaveMode` del objeto `setSaveStyle` y pasando un valor de cadena que especifica el modo de guardado. Por ejemplo, para guardar y ver rápidamente la web, pase `FAST_WEB_VIEW`.

1. Invocar la operación Guardar estilo

   Invoque el método `PDFUtilityServiceClient` del objeto `setSaveMode` y pase los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que representa el documento PDF.
   * Un objeto `PDFUtilitySaveMode` que contiene el estilo de guardado que se va a utilizar.
   * Un valor booleano que se utiliza para determinar si se va a anular la configuración anterior.

   El método devuelve un objeto `com.adobe.idp.Document` formateado con el estilo de guardado especificado.

1. Pasar el documento PDF a otra operación de AEM Forms

   * Pase el objeto `com.adobe.idp.Document` devuelto a otra operación de AEM Forms.

**Consulte también**

[Configuración de los modos de guardado de documentos PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Establecer las opciones de guardado de documentos PDF utilizando la API de servicio Web {#set-pdf-document-save-options-using-the-web-service-api}

Defina las opciones de guardado del documento PDF utilizando el API de utilidades de PDF (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el archivo WSDL del servicio de utilidades de PDF.
   * Haga referencia al ensamblado cliente de Microsoft .NET.

1. Creación de un cliente PDFUtilityService

   Cree un objeto `PDFUtilityServiceService` utilizando su constructor de clase proxy.

1. Definir el modo Guardar

   * Cree un objeto `PDFUtilitySaveMode` utilizando su constructor.
   * Establezca el modo de guardado asignando un valor de cadena al método `PDFUtilitySaveMode` del objeto `saveStyle` que especifica el modo de guardado. Por ejemplo, para guardar para una visualización web rápida, especifique `FAST_WEB_VIEW`.

1. Invocar la operación Guardar estilo

   Invoque el método `PDFUtilityServiceService` del objeto `setSaveMode` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento PDF.
   * Un objeto `PDFUtilitySaveMode` que contiene el estilo de guardado que se va a utilizar.
   * Un valor booleano que se utiliza para determinar si se va a anular la configuración anterior.

   El método devuelve un objeto `BLOB` formateado con el estilo de guardado especificado. A continuación, puede guardar ese objeto como un documento PDF.

1. Pasar el documento PDF a otra operación de Forms

   * Pase el objeto `BLOB` devuelto a otra operación de AEM Forms.

**Consulte también**

[Configuración de los modos de guardado de documentos PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Sanitización de documentos PDF {#sanitizing-pdf-documents}

Puede utilizar las API de Java de utilidades de PDF para convertir documentos PDF en documentos XDP mediante programación.

>[!NOTE]
>
>Para obtener más información sobre el servicio de utilidades de PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-4}

Para sanear un documento PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente PDFUtilityService.
1. Invoque la operación de saneamiento.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Para crear una aplicación cliente utilizando Java, incluya los archivos JAR necesarios.

**Creación de un cliente PDFUtilityService**

Antes de realizar una operación de sanización mediante programación, debe crear un cliente PDFUtilityService. Con la API de Java, esto se consigue creando un objeto `PDFUtilityServiceClient`.

**Invocar la operación de conversión PDF a XDP**

Después de crear el cliente de servicio, puede invocar la operación de sanización.

**Consulte también**

[Convertir documentos PDF en documentos XDP mediante la API de Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Convertir documentos PDF en documentos XDP mediante la API de servicio Web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Sanear documentos PDF usando la API de Java {#sanitize-pdf-documents-using-the-java-api}

Sanice los documentos utilizando la API de utilidades de PDF (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-pdfutility-client.jar, en la ruta de clase del proyecto Java.

1. Creación de un cliente PDFUtilityService

   Cree un objeto `PDFUtilityServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Invocar la operación de conversión PDF a XDP

   Para realizar la conversión, invoque el método `PDFUtilityServiceClient` del objeto `convertPDFtoXDP` y pase un objeto `com.adobe.idp.Document` que represente el archivo PDF. El método devuelve un objeto `com.adobe.idp.Document` que representa el archivo XDP recién creado.

**Consulte también**

[Sanitización de documentos PDF](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
