---
title: Trabajar con utilidades PDF
description: Utilice el servicio Utilidades de PDF para realizar conversiones entre los formatos de archivo PDF y XDP, definir y recuperar propiedades de documento de PDF XMP y manipular metadatos de la.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: e4b204ee-7261-42b8-8db8-a92aa9fd0a28
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2549'
ht-degree: 1%

---

# Trabajar con utilidades PDF {#working-with-pdf-utilities}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

**Acerca del servicio Utilidades del PDF**

El servicio Utilidades de PDF puede realizar conversiones entre los formatos de archivo PDF y XDP, establecer y recuperar propiedades de documento de PDF XMP y manipular metadatos de. Por ejemplo, antes de convertir un documento de PDF a otro formato, es útil inspeccionar sus propiedades para determinar qué operación de servicio invocar para la conversión.

Puede realizar estas tareas mediante el servicio Utilidades de PDF:

* Convertir documentos de PDF en documentos XDP.
* Convierta documentos XDP en documentos de PDF. (Consulte [Convertir documentos XDP en documentos de PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents).)
* Recupere las propiedades del documento del PDF. (Consulte [Recuperando propiedades de documento de PDF](pdf-utilities.md#retrieving-pdf-document-properties).)
* Guarde un documento de PDF y optimícelo para una visualización web rápida. (Consulte [Estableciendo modos de guardado de documentos de PDF](pdf-utilities.md#setting-pdf-document-save-modes).)

>[!NOTE]
>
>Para obtener más información sobre el servicio Utilidades de PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Convertir documentos de PDF en documentos XDP {#converting-pdf-documents-into-xdp-documents}

Puede utilizar las API de Java y de servicios web de Utilidades de PDF para convertir mediante programación documentos de PDF en documentos XDP.

>[!NOTE]
>
>Para obtener más información sobre el servicio Utilidades de PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para convertir un documento de PDF en un documento XDP, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDFUtilityService.
1. Invoque la operación de conversión del PDF a XDP.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente de PDFUtilityService**

Para poder realizar mediante programación una operación de Utilidades de PDF, debe crear un cliente PDFUtilityService. Con la API de Java, esto se logra creando un `PDFUtilityServiceClient` objeto. Con la API del servicio web, esto se logra mediante una `PDFUtilityServiceService` objeto.

**Invocar la operación de conversión del PDF a XDP**

Después de crear el cliente de servicio, puede invocar la operación de conversión del PDF a XDP.

**Consulte también**

[Convertir documentos de PDF en documentos XDP mediante la API de Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Conversión de documentos de PDF en documentos XDP mediante la API de servicio web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir documentos de PDF en documentos XDP mediante la API de Java {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

Convierta documentos de PDF en documentos XDP mediante la API de utilidades de PDF (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-pdfutility-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente de PDFUtilityService

   Crear un `PDFUtilityServiceClient` mediante su constructor y pasando un objeto `ServiceClientFactory` que contiene las propiedades de conexión.

1. Invocar la operación de conversión del PDF a XDP

   Para realizar la conversión, invoque el `PDFUtilityServiceClient` del objeto `convertPDFtoXDP` método y pasar un `com.adobe.idp.Document` que representa el archivo del PDF. El método devuelve un valor `com.adobe.idp.Document` que representa el archivo XDP recién creado.

**Consulte también**

[Convertir documentos de PDF en documentos XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de documentos de PDF en documentos XDP mediante la API de servicio web {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

Convierta documentos de PDF en documentos XDP mediante la API de Utilidades de PDF (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el archivo WSDL del servicio Utilidades de PDF.
   * Hacer referencia al ensamblado de cliente de Microsoft .NET.

1. Crear un cliente de PDFUtilityService

   Crear un `PDFUtilityServiceService` mediante el constructor de la clase de proxy.

1. Invocar la operación de conversión del PDF a XDP

   Invoque el `PDFUtilityServiceService` del objeto `convertPDFtoXDP` método y pasar un `BLOB` que representa el archivo del PDF. El método devuelve un valor `BLOB` que representa el archivo XDP recién creado.

**Consulte también**

[Convertir documentos de PDF en documentos XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Crear un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Convertir documentos XDP en documentos de PDF {#converting-xdp-documents-into-pdf-documents}

Puede utilizar las API de Java y de servicios web de Utilidades de PDF para convertir mediante programación documentos XDP en documentos de PDF.

>[!NOTE]
>
>Para obtener más información sobre el servicio Utilidades de PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para convertir un documento XDP en un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDFUtilityService.
1. Invoque el XDP para la operación de conversión del PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente de PDFUtilityService**

Para poder realizar mediante programación una operación de Utilidades de PDF, debe crear un cliente PDFUtilityService. Con la API de Java, esto se logra creando un `PDFUtilityServiceClient` objeto. Con la API del servicio web, esto se logra mediante una `PDFUtilityServiceService` objeto.

**Invoque el XDP para la operación de conversión del PDF**

Después de crear el cliente de servicios, puede invocar el XDP para la operación de conversión del PDF.

**Consulte también**

[Conversión de documentos XDP en documentos de PDF mediante la API de Java](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[Conversión de documentos XDP en documentos de PDF mediante la API de servicio web](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de documentos XDP en documentos de PDF mediante la API de Java {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

Convierta documentos XDP en documentos de PDF mediante la API de utilidades de PDF (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-pdfutility-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente de PDFUtilityService

   Crear un `PDFUtilityServiceClient` mediante su constructor y pasando un objeto `ServiceClientFactory` que contiene las propiedades de conexión.

1. Invoque el XDP para la operación de conversión del PDF

   Para realizar la conversión, invoque el `PDFUtilityServiceClient` del objeto `convertXDPtoPDF` método y pasar un `com.adobe.idp.Document` que representa el archivo XDP. El método devuelve un valor `com.adobe.idp.Document` que representa el archivo de PDF recién creado.

**Consulte también**

[Convertir documentos XDP en documentos de PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de documentos XDP en documentos de PDF mediante la API de servicio web {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

Convierta documentos XDP en documentos de PDF mediante la API de utilidades de PDF (API de servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el archivo WSDL del servicio Utilidades de PDF.
   * Hacer referencia al ensamblado de cliente de Microsoft .NET.

1. Crear un cliente de PDFUtilityService

   Crear un `PDFUtilityServiceService` mediante el constructor de la clase de proxy.

1. Invoque el XDP para la operación de conversión del PDF

   Para realizar la conversión, invoque el `PDFUtilityServiceService` del objeto `convertXDPtoPDF` método y pasar un `BLOB` que representa el archivo XDP. El método devuelve un valor `BLOB` que representa el archivo de PDF recién creado.

**Consulte también**

[Convertir documentos XDP en documentos de PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Crear un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Recuperando propiedades de documento de PDF {#retrieving-pdf-document-properties}

Puede utilizar las API de Java y del servicio web de Utilidades de PDF para recuperar mediante programación las propiedades de los documentos de PDF, como si el documento es un formulario rellenable o la versión mínima de Acrobat necesaria para leer el documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio Utilidades de PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Resumen de los pasos {#summary_of_steps-2}

Para recuperar las propiedades del documento del PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDFUtilityService.
1. Invoque la operación de recuperación de propiedades.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente de PDFUtilityService**

Para poder realizar mediante programación una operación de Utilidades de PDF, debe crear un cliente PDFUtilityService. Con la API de Java, esto se logra creando un `PDFUtilityServiceClient` objeto. Con la API del servicio web, esto se logra mediante una `PDFUtilityServiceService` objeto.

**Invocar la operación de recuperación de propiedades**

Después de crear el cliente de servicios, puede invocar la operación de recuperación de propiedades.

**Consulte también**

[Recuperación de propiedades de documentos del PDF mediante la API de Java](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[Recuperar propiedades de documento de PDF mediante la API de servicio web](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperación de propiedades de documentos del PDF mediante la API de Java {#retrieve-pdf-document-properties-using-the-java-api}

Recupere las propiedades del documento del PDF mediante la API de Utilidades del PDF (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-pdfutility-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente de PDFUtilityService

   Crear un `PDFUtilityServiceClient` mediante su constructor y pasando un objeto `ServiceClientFactory` que contiene las propiedades de conexión.

1. Invocar la operación de recuperación de propiedades

   Para realizar la conversión, invoque el `PDFUtilityServiceClient` del objeto `getPDFProperties` y pase lo siguiente:

   * A `com.adobe.idp.Document` que representa el documento del PDF.
   * A `PDFPropertiesOptionSpec` que contiene las propiedades que se van a evaluar.

   El método devuelve un valor `PDFPropertiesResult` que contiene los resultados de la consulta.

**Consulte también**

[Recuperando propiedades de documento de PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar propiedades de documento de PDF mediante la API de servicio web {#retrieve-pdf-document-properties-using-the-web-service-api}

Recupere las propiedades del documento del PDF mediante la API del servicio web Utilidades del PDF:

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el archivo WSDL del servicio Utilidades de PDF.
   * Hacer referencia al ensamblado de cliente de Microsoft .NET.

1. Crear un cliente de PDFUtilityService

   Crear un `PDFUtilityServiceService` mediante el constructor de la clase de proxy.

1. Invocar la operación de recuperación de propiedades

   Para realizar la conversión, invoque el `PDFUtilityServiceService` del objeto `getPDFProperties` y pase lo siguiente:

   * A `BLOB` que representa el documento del PDF.
   * A `PDFPropertiesOptionSpec` que contiene las propiedades que se van a evaluar.

   El método devuelve un valor `PDFPropertiesResult` que contiene los resultados de la consulta.

**Consulte también**

[Recuperando propiedades de documento de PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Crear un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Estableciendo modos de guardado de documentos de PDF {#setting-pdf-document-save-modes}

Puede utilizar la Java del servicio Utilidades de PDF y las API del servicio web para establecer mediante programación un modo de guardado para un documento de PDF. Cuando se utiliza el servicio Utilidades del PDF para establecer un modo de guardado, el servicio Utilidades del PDF sólo establece el modo de guardado y no guarda realmente el documento del PDF. El documento del PDF se guarda cuando se pasa a otra operación de servicio. Por ejemplo, puede utilizar el servicio Utilidades de PDF para establecer un modo de guardado específico y pasarlo al servicio Cifrado, donde el documento de PDF se guarda y se cifra.

>[!NOTE]
>
>Para obtener más información sobre el servicio Utilidades de PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-3}

Para definir la opción de guardado para documentos de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDFUtilityService.
1. Configure el modo de guardado.
1. Invoque la operación de guardado.
1. Pase el documento del PDF a otra operación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente de PDFUtilityService**

Para poder realizar mediante programación una operación de Utilidades de PDF, debe crear un cliente PDFUtilityService. Con la API de Java, esto se logra creando un `PDFUtilityServiceClient` objeto. Con la API del servicio web, esto se logra mediante una `PDFUtilityServiceService` objeto.

**Configuración del modo Guardar**

Puede elegir una de las siguientes opciones de guardado:

* `INCREMENTAL`: Para guardar de forma incremental para reducir el tiempo necesario para guardar
* `FAST_WEB_VIEW`: guarde para visualizar la web rápidamente
* `FULL`: Para guardar mediante un guardado completo (sin optimizaciones)

**Invocar la operación de guardar estilo**

Después de crear el cliente de servicios, puede invocar la operación de recuperación de propiedades.

**Pase el documento del PDF a otra operación de AEM Forms**

Una vez que el servicio Utilidades del PDF haya establecido el modo Guardar especificado, pase el documento del PDF a otra operación de AEM Forms. Una vez devuelta la operación, el documento del PDF se guarda en el modo especificado. Por ejemplo, si utiliza el servicio Utilidades del PDF para configurar la variable `FAST_WEB_VIEW` y, a continuación, pase el documento del PDF al `encryptUsingPassword` operación, el documento de PDF devuelto se cifra con una contraseña y se guarda en `FAST_WEB_VIEW` modo.

>[!NOTE]
>
>El Inicio rápido asociado a esta sección establece lo siguiente `FAST_WEB_VIEW` y, a continuación, pasa el documento del PDF al `encryptUsingPassword` operación.

**Consulte también**

[Definir opciones de guardado de documentos de PDF mediante la API de Java](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[Definir opciones de guardado de documentos de PDF mediante la API de servicio web](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Cifrar documentos de PDF con una contraseña](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Definir opciones de guardado de documentos de PDF mediante la API de Java {#set-pdf-document-save-options-using-the-java-api}

Defina las opciones de guardado de documentos de PDF mediante la API de Utilidades de PDF (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-pdfutility-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente de PDFUtilityService

   Crear un `PDFUtilityServiceClient` mediante su constructor y pasando un objeto `ServiceClientFactory` que contiene las propiedades de conexión.

1. Configuración del modo Guardar

   * Crear un `PDFUtilitySaveMode` mediante su constructor.
   * Configure el modo de guardado invocando el `PDFUtilitySaveMode` del objeto `setSaveStyle` y pasando un valor de cadena que especifica el modo de guardado. Por ejemplo, para guardar para ver rápidamente en la web, pase `FAST_WEB_VIEW`.

1. Invocar la operación de guardar estilo

   Invoque el `PDFUtilityServiceClient` del objeto `setSaveMode` y pasar los siguientes valores:

   * A `com.adobe.idp.Document` que representa el documento del PDF.
   * A `PDFUtilitySaveMode` que contiene el estilo de guardado que se va a utilizar.
   * Valor booleano que se utiliza para determinar si se debe anular la configuración anterior.

   El método devuelve un valor `com.adobe.idp.Document` objeto formateado con el estilo de guardado especificado.

1. Pase el documento del PDF a otra operación de AEM Forms

   * Pase el devuelto `com.adobe.idp.Document` objeto a otra operación de AEM Forms.

**Consulte también**

[Estableciendo modos de guardado de documentos de PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Definir opciones de guardado de documentos de PDF mediante la API de servicio web {#set-pdf-document-save-options-using-the-web-service-api}

Defina las opciones de guardado de documentos del PDF mediante la API de Utilidades del PDF (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el archivo WSDL del servicio Utilidades de PDF.
   * Hacer referencia al ensamblado de cliente de Microsoft .NET.

1. Crear un cliente de PDFUtilityService

   Crear un `PDFUtilityServiceService` mediante el constructor de la clase de proxy.

1. Configuración del modo Guardar

   * Crear un `PDFUtilitySaveMode` mediante su constructor.
   * Configure el modo de guardado asignando un valor de cadena a la variable `PDFUtilitySaveMode` del objeto `saveStyle` que especifica el modo de guardado. Por ejemplo, para guardar para visualizar rápidamente en la web, especifique `FAST_WEB_VIEW`.

1. Invocar la operación de guardar estilo

   Invoque el `PDFUtilityServiceService` del objeto `setSaveMode` y pasar los siguientes valores:

   * A `BLOB` que representa el documento del PDF.
   * A `PDFUtilitySaveMode` que contiene el estilo de guardado que se va a utilizar.
   * Valor booleano que se utiliza para determinar si se debe anular la configuración anterior.

   El método devuelve un valor `BLOB` objeto formateado con el estilo de guardado especificado. A continuación, puede guardar ese objeto como un documento de PDF.

1. Pase el documento del PDF a otra operación de Forms

   * Pase el devuelto `BLOB` objeto a otra operación de AEM Forms.

**Consulte también**

[Estableciendo modos de guardado de documentos de PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Crear un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Desinfectar documentos de PDF {#sanitizing-pdf-documents}

Puede utilizar las API de Java de Utilidades de PDF para convertir mediante programación documentos de PDF en documentos XDP.

>[!NOTE]
>
>Para obtener más información sobre el servicio Utilidades de PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-4}

Para sanear el documento del PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDFUtilityService.
1. Invoque la operación de desinfección.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Para crear una aplicación cliente con Java, incluya los archivos JAR necesarios.

**Crear un cliente de PDFUtilityService**

Para poder realizar mediante programación una operación de saneamiento, debe crear un cliente PDFUtilityService. Con la API de Java, esto se logra creando un `PDFUtilityServiceClient` objeto.

**Invocar la operación de conversión del PDF a XDP**

Después de crear el cliente de servicios, puede invocar la operación de saneamiento.

**Consulte también**

[Convertir documentos de PDF en documentos XDP mediante la API de Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Conversión de documentos de PDF en documentos XDP mediante la API de servicio web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Limpieza de documentos del PDF mediante la API de Java {#sanitize-pdf-documents-using-the-java-api}

Limpieza de documentos mediante la API de Utilidades del PDF (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-pdfutility-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente de PDFUtilityService

   Crear un `PDFUtilityServiceClient` mediante su constructor y pasando un objeto `ServiceClientFactory` que contiene las propiedades de conexión.

1. Invocar la operación de conversión del PDF a XDP

   Para realizar la conversión, invoque el `PDFUtilityServiceClient` del objeto `convertPDFtoXDP` método y pasar un `com.adobe.idp.Document` que representa el archivo del PDF. El método devuelve un valor `com.adobe.idp.Document` que representa el archivo XDP recién creado.

**Consulte también**

[Sanear documentos del PDF](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
