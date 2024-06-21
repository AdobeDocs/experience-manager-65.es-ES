---
title: Conversión entre formatos de archivo y PDF
description: Utilice el servicio Generate PDF para convertir formatos de archivo nativos a PDF. El servicio Generate PDF también convierte PDF a otros formatos de archivo y optimiza el tamaño de los documentos de PDF.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 10535740-e3c2-4347-a88f-86706ad699b4
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,  Document Services
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '7848'
ht-degree: 0%

---

# Conversión entre formatos de archivo y PDF {#converting-between-file-formatsand-pdf}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

**Acerca del servicio Generar PDF**

El servicio Generate PDF convierte los formatos de archivo nativos en PDF. También convierte PDF a otros formatos de archivo y optimiza el tamaño de los documentos PDF.

El servicio Generate PDF utiliza aplicaciones nativas para convertir los siguientes formatos de archivo a PDF. A menos que se indique lo contrario, solo son compatibles las versiones alemana, francesa, inglesa y japonesa de estas aplicaciones. *Solo Windows* indica compatibilidad sólo con Windows Server® 2003 y Windows Server 2008.

* Microsoft Office 2003 y 2007 para convertir DOC, DOCX, RTF, TXT, XLS, XLSX, PPT, PPTX, VSD, MPP, MPPX, XPS y PUB (sólo Windows)

>[!NOTE]
>
>Se requiere Acrobat® 9.2 o posterior para convertir el formato XPS de Microsoft a PDF.

* Autodesk AutoCAD 2005, 2006, 2007, 2008 y 2009 para convertir DWF, DWG y DXW (sólo en inglés)
* Corel WordPerfect 12 y X4 para convertir WPD, QPW, SHW (solo en inglés)
* OpenOffice 2.0, 2.4, 3.0.1 y 3.1 para convertir ODT, ODS, ODP, ODG, ODF, SXW, SXI, SXC, SXD, DOC, DOCX, RTF, TXT, XLS, XLSX, PPT, PPTX, VSD, MPP, MPPX y PUB

>[!NOTE]
>
>El servicio Generar PDF no es compatible con las versiones de 64 bits de OpenOffice.

* Adobe Photoshop® CS2 para convertir el PSD (sólo Windows)

>[!NOTE]
>
>Photoshop CS3 y CS4 no son compatibles porque no son compatibles con Windows Server 2003 o Windows Server 2008.

* Adobe FrameMaker® 7.2 y 8 para convertir FM (sólo Windows)
* PageMaker de Adobe ® 7.0 para convertir PMD, PM6, P65 y PM (sólo Windows)
* Formatos nativos admitidos por aplicaciones de terceros (requiere el desarrollo de archivos de instalación específicos para la aplicación) (solo Windows)

El servicio Generate PDF convierte los siguientes formatos de archivo basados en estándares en PDF.

* Formatos de vídeo: SWF, FLV (sólo Windows)
* Formatos de imagen: JPEG, JPG, JP2, J2Kí, JPC, J2C, GIF, BMP, TIFF, TIF, PNG, JPF
* HTML (Windows, Sun™ Solaris™ y Linux®)

El servicio Generate PDF convierte PDF a los siguientes formatos de archivo (solo Windows):

* PostScript encapsulado (EPS)
* HTML 3.2
* HTML 4.01 con CSS 1.0
* DOC (formato Microsoft Word)
* RTF
* Texto (accesible y sin formato)
* XML
* PDF/A-1a que sólo utiliza el espacio de color DeviceRGB
* PDF/A-1b que utiliza sólo el espacio de color DeviceRGB

El servicio Generate PDF requiere que realice las siguientes tareas administrativas:

* Instalar las aplicaciones nativas necesarias en el equipo que aloja AEM Forms
* Instale Adobe Acrobat Professional o Acrobat Pro Extended 9.2 en el equipo que aloja AEM Forms
* Realizar tareas de instalación posteriores a la instalación

AEM Estas tareas se describen en Instalación e implementación de formularios en forma de mediante JBoss Turnkey.

Puede realizar estas tareas mediante el servicio Generate PDF:

* Convertir de formatos de archivo nativos a PDF.
* Convertir documentos de HTML en documentos de PDF.
* Convierta documentos de PDF en formatos de archivo.

>[!NOTE]
>
>Para obtener más información sobre el servicio Generate PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Convertir documentos de Word en documentos de PDF {#converting-word-documents-to-pdf-documents}

En esta sección se describe cómo puede utilizar la API Generate PDF para convertir mediante programación un documento de Microsoft Word en un documento de PDF.

>[!NOTE]
>
>Para obtener más información sobre formatos de archivo adicionales, consulte [Añadir compatibilidad con formatos de archivo nativos adicionales](converting-file-formats-pdf.md#adding-support-for-additional-native-file-formats).

>[!NOTE]
>
>Para obtener más información sobre el servicio Generate PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para convertir un documento de Microsoft Word en un documento de PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente Generate PDF.
1. Recupere el archivo para convertirlo en un documento de PDF.
1. Convierta el archivo en un documento de PDF.
1. Recupere los resultados.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un cliente de Generador de PDF**

Para poder realizar mediante programación una operación Generate PDF, cree un cliente de servicio Generate PDF. Si utiliza la API de Java, cree un `GeneratePdfServiceClient` objeto. Si utiliza la API del servicio web, cree un `GeneratePDFServiceService` objeto.

**Recupere el archivo para convertirlo en un documento de PDF**

Recupere el documento de Microsoft Word para convertirlo en un documento de PDF.

**Conversión del archivo en un documento de PDF**

Después de crear el cliente del servicio Generate PDF, puede invocar el `createPDF2` método. Este método necesita información sobre el documento que se va a convertir, incluida la extensión de archivo.

**Recuperación de los resultados**

Una vez convertido el archivo en un documento de PDF, puede recuperar los resultados. Por ejemplo, después de convertir un archivo de Word en un documento de PDF, puede recuperar y guardar el documento de PDF.

**Consulte también**

[Conversión de documentos de Word en documentos de PDF mediante la API de Java](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-java-api)

[Conversión de documentos de Word en documentos de PDF mediante la API de servicio web](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API de generación de servicio de PDF](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Conversión de documentos de Word en documentos de PDF mediante la API de Java {#convert-word-documents-to-pdf-documents-using-the-java-api}

Convierta un documento de Microsoft Word en un documento de PDF mediante la API Generate PDF (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-generatepdf-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente Generate PDF.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `GeneratePdfServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Recupere el archivo para convertirlo en un documento de PDF.

   * Crear un `java.io.FileInputStream` que representa el archivo de Word que se va a convertir mediante su constructor. Pase un valor de cadena que especifique la ubicación del archivo.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Convierta el archivo en un documento de PDF.

   Convierta el archivo en un documento de PDF invocando el `GeneratePdfServiceClient` del objeto `createPDF2` y pasando los siguientes valores:

   * A `com.adobe.idp.Document` que representa el archivo que se va a convertir.
   * A `java.lang.String` que contiene la extensión de archivo.
   * A `java.lang.String` que contiene la configuración de tipo de archivo que se utilizará en la conversión. La configuración de tipo de archivo proporciona opciones de conversión para diferentes tipos de archivo, como .doc o .xls.
   * A `java.lang.String` que contiene el nombre de la configuración de PDF que se va a utilizar. Por ejemplo, puede especificar `Standard`.
   * A `java.lang.String` que contiene el nombre de la configuración de seguridad que se va a utilizar.
   * Un opcional `com.adobe.idp.Document` que contiene la configuración que se aplicará durante la generación del documento de PDF.
   * Un opcional `com.adobe.idp.Document` que contiene información de metadatos que se aplicará al documento del PDF.

   El `createPDF2` El método devuelve un valor `CreatePDFResult` que contiene el nuevo documento de PDF y una información de registro. El archivo de registro suele contener mensajes de error o advertencia generados por la solicitud de conversión.

1. Recupere los resultados.

   Para obtener el documento de PDF, realice las siguientes acciones:

   * Invoque el `CreatePDFResult` del objeto `getCreatedDocument` método, que devuelve un valor `com.adobe.idp.Document` objeto.
   * Invoque el `com.adobe.idp.Document` del objeto `copyToFile` para extraer el documento de PDF del objeto creado en el paso anterior.

   Si ha utilizado la variable `createPDF2` para obtener el documento de registro (no aplicable a las conversiones de HTML), realice las siguientes acciones:

   * Invoque el `CreatePDFResult` del objeto `getLogDocument` método. Esto devuelve un `com.adobe.idp.Document` objeto.
   * Invoque el `com.adobe.idp.Document` del objeto `copyToFile` para extraer el documento de registro.

**Consulte también**

[Resumen de los pasos](converting-file-formats-pdf.md#summary-of-steps)

[SOAP Inicio rápido (modo de): Conversión de un documento de Microsoft Word en un documento de PDF mediante la API de Java](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de documentos de Word en documentos de PDF mediante la API de servicio web {#convert-word-documents-to-pdf-documents-using-the-web-service-api}

Conversión de un documento de Microsoft Word en un documento de PDF mediante la API Generate PDF (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente Generate PDF.

   * Crear un `GeneratePDFServiceClient` mediante su constructor predeterminado.
   * Crear un `GeneratePDFServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.) No es necesario que utilice el `lc_version` atributo. Sin embargo, especifique `?blob=mtom`.
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `GeneratePDFServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere el archivo para convertirlo en un documento de PDF.

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar el archivo que desea convertir en un documento de PDF.
   * Crear un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo que se va a convertir y el modo en que se va a abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` asignando a su `MTOM` propiedad el contenido de la matriz de bytes.

1. Convierta el archivo en un documento de PDF.

   Convierta el archivo en un documento de PDF invocando el `GeneratePDFServiceService` del objeto `CreatePDF2` y pasando los siguientes valores:

   * A `BLOB` que representa el archivo que se va a convertir.
   * Cadena que contiene la extensión del archivo.
   * A `java.lang.String` que contiene la configuración de tipo de archivo que se utilizará en la conversión. La configuración de tipo de archivo proporciona opciones de conversión para diferentes tipos de archivo, como .doc o .xls.
   * Objeto de cadena que contiene la configuración del PDF que se va a utilizar. Puede especificar `Standard`.
   * Objeto de cadena que contiene la configuración de seguridad que se va a utilizar. Puede especificar `No Security`.
   * Un opcional `BLOB` que contiene la configuración que se aplicará durante la generación del documento de PDF.
   * Un opcional `BLOB` que contiene información de metadatos que se aplicará al documento del PDF.
   * Un parámetro de salida de tipo `BLOB` que se rellena con la variable `CreatePDF2` método. El `CreatePDF2` rellena este objeto con el documento convertido. (Este valor de parámetro solo es necesario para la invocación del servicio web).
   * Un parámetro de salida de tipo `BLOB` que se rellena con la variable `CreatePDF2` método. El `CreatePDF2` Este método rellena este objeto con el documento de registro. (Este valor de parámetro solo es necesario para la invocación del servicio web).

1. Recupere los resultados.

   * Recupere el documento de PDF convertido asignando el `BLOB` del objeto `MTOM` a una matriz de bytes. La matriz de bytes representa el documento de PDF convertido. Asegúrese de utilizar el `BLOB` objeto que se utiliza como parámetro de salida para `createPDF2` método.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación de archivo del documento de PDF convertido.
   * Crear un `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](converting-file-formats-pdf.md#summary-of-steps)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Conversión de Documentos de HTML en Documentos de PDF {#converting-html-documents-to-pdf-documents}

En esta sección se describe cómo puede utilizar la API Generate PDF para convertir mediante programación documentos de HTML en documentos de PDF.

>[!NOTE]
>
>Para obtener más información sobre el servicio Generate PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para convertir un documento de HTML en un documento de PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente Generate PDF.
1. Recupere el contenido del HTML para convertirlo en un documento del PDF.
1. Convierta el contenido del HTML en un documento del PDF.
1. Recupere los resultados.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un cliente de Generador de PDF**

Para poder realizar mediante programación una operación Generate PDF, debe crear un cliente de servicio Generate PDF. Si utiliza la API de Java, cree un `GeneratePdfServiceClient` objeto. Si utiliza la API del servicio web, cree un `GeneratePDFServiceService`.

**Recuperar el contenido del HTML para convertirlo en un documento del PDF**

Haga referencia al contenido del HTML que desee convertir en un documento del PDF. Puede hacer referencia a contenido de HTML, como un archivo de HTML o a contenido de HTML al que se puede acceder mediante una dirección URL.

**Conversión del contenido del HTML en un documento del PDF**

Después de crear el cliente de servicios, puede invocar la operación de creación de PDF adecuada. Esta operación necesita información sobre el documento que se va a convertir, incluida la ruta al documento de destino.

**Recuperación de los resultados**

Una vez convertido el contenido del HTML en un documento del PDF, puede recuperar los resultados y guardar el documento del PDF.

**Consulte también**

[Conversión del contenido del HTML en un documento del PDF mediante la API de Java](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-java-api)

[Conversión del contenido de un HTML en un documento de un PDF mediante la API de servicio web](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API de generación de servicio de PDF](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Conversión del contenido del HTML en un documento del PDF mediante la API de Java {#convert-html-content-to-a-pdf-document-using-the-java-api}

Conversión de un documento de HTML en un documento de PDF mediante la API de generación de PDF (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-generatepdf-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente Generate PDF.

   Crear un `GeneratePdfServiceClient` mediante su constructor y pasando un objeto `ServiceClientFactory` que contiene las propiedades de conexión.

1. Recupere el contenido del HTML para convertirlo en un documento del PDF.

   Recupere contenido de HTML creando una variable de cadena y asignando una dirección URL que apunte al contenido de HTML.

1. Convierta el contenido del HTML en un documento del PDF.

   Invoque el `GeneratePdfServiceClient` del objeto `htmlToPDF2` y pasar los siguientes valores:

   * A `java.lang.String` que contiene la dirección URL del archivo de HTML que se va a convertir.
   * A `java.lang.String` que contiene la configuración de tipo de archivo que se utilizará en la conversión. La configuración de tipo de archivo puede incluir niveles de araña.
   * A `java.lang.String` que contiene el nombre de la configuración de seguridad que se va a utilizar.
   * Un opcional `com.adobe.idp.Document` que contiene la configuración que se aplicará durante la generación del documento de PDF. Si no se proporciona esta información, la configuración se elige automáticamente en función de los tres parámetros anteriores.
   * Un opcional `com.adobe.idp.Document` que contiene información de metadatos que se aplicará al documento del PDF.

1. Recupere los resultados.

   El `htmlToPDF2` El método devuelve un `HtmlToPdfResult` que contiene el nuevo documento de PDF que se ha generado. Para obtener el documento de PDF recién creado, realice las siguientes acciones:

   * Invoque el `HtmlToPdfResult` del objeto `getCreatedDocument` método. Esto devuelve un `com.adobe.idp.Document` objeto.
   * Invoque el `com.adobe.idp.Document` del objeto `copyToFile` para extraer el documento de PDF del objeto creado en el paso anterior.

**Consulte también**

[Conversión de Documentos de HTML en Documentos de PDF](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[SOAP Inicio rápido (modo de): Conversión del contenido del HTML a un documento del PDF mediante la API de Java](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[SOAP Inicio rápido (modo de): Conversión del contenido del HTML a un documento del PDF mediante la API de Java](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión del contenido de un HTML en un documento de un PDF mediante la API de servicio web {#convert-html-content-to-a-pdf-document-using-the-web-service-api}

Conversión del contenido de un HTML en un documento de un PDF mediante la API de generación de PDF (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente Generate PDF.

   * Crear un `GeneratePDFServiceClient` mediante su constructor predeterminado.
   * Crear un `GeneratePDFServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.) No es necesario que utilice el `lc_version` atributo. Sin embargo, especifique `?blob=mtom`.
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `GeneratePDFServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere el contenido del HTML para convertirlo en un documento del PDF.

   Recupere contenido de HTML creando una variable de cadena y asignando una dirección URL que apunte al contenido de HTML.

1. Convierta el contenido del HTML en un documento del PDF.

   Convierta el contenido del HTML en un documento del PDF invocando el `GeneratePDFServiceService` del objeto `HtmlToPDF2` y pasar los siguientes valores:

   * Cadena que contiene el contenido del HTML que se va a convertir.
   * A `java.lang.String` que contiene la configuración de tipo de archivo que se utilizará en la conversión.
   * Objeto de cadena que contiene la configuración de seguridad que se va a utilizar.
   * Un opcional `BLOB` que contiene la configuración que se aplicará durante la generación del documento de PDF.
   * Un opcional `BLOB` que contiene información de metadatos que se aplicará al documento del PDF.
   * Un parámetro de salida de tipo `BLOB` que se rellena con la variable `CreatePDF2` método. El `CreatePDF2` rellena este objeto con el documento convertido. (Este valor de parámetro solo es necesario para la invocación del servicio web).

1. Recupere los resultados.

   * Recupere el documento de PDF convertido asignando el `BLOB` del objeto `MTOM` a una matriz de bytes. La matriz de bytes representa el documento de PDF convertido. Asegúrese de utilizar el `BLOB` objeto que se utiliza como parámetro de salida para `HtmlToPDF2` método.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación de archivo del documento de PDF convertido.
   * Crear un `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Conversión de Documentos de HTML en Documentos de PDF](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Conversión de documentos de PDF a formatos que no sean imágenes {#converting-pdf-documents-to-non-image-formats}

En esta sección se describe cómo puede utilizar la API Generate PDF Java y la API de servicio web para convertir mediante programación un documento de PDF en un archivo RTF, que es un ejemplo de formato que no es de imagen. Otros formatos que no son de imagen son HTML, texto, DOC y EPS. Al convertir un documento de PDF a RTF, asegúrese de que el documento de PDF no contenga elementos de formulario, como un botón de envío. Los elementos de formulario no se convierten.

>[!NOTE]
>
>Para obtener más información sobre el servicio Generate PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-2}

Para convertir un documento de PDF en cualquiera de los tipos compatibles, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente Generate PDF.
1. Recupere el documento del PDF que desea convertir.
1. Convierta el documento del PDF.
1. Guarde el archivo convertido.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un cliente de Generador de PDF**

Para poder realizar mediante programación una operación Generate PDF, debe crear un cliente de servicio Generate PDF. Si utiliza la API de Java, cree un `GeneratePdfServiceClient` objeto. Si utiliza la API del servicio web, cree un `GeneratePDFServiceService` objeto.

**Recuperar el documento del PDF para convertirlo**

Recupere el documento del PDF para convertirlo a un formato que no sea de imagen.

**Conversión del documento del PDF**

Después de crear el cliente de servicios, puede invocar la operación de exportación del PDF. Esta operación necesita información sobre el documento que se va a convertir, incluida la ruta al documento de destino.

**Guardar el archivo convertido**

Guarde el archivo convertido. Por ejemplo, si convierte un documento de PDF en un archivo RTF, guarde el documento convertido en un archivo RTF.

**Consulte también**

[Conversión de un documento de PDF en un archivo RTF mediante la API de Java](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-java-api)

[Conversión de un documento de PDF en un archivo RTF mediante la API de servicio web](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API de generación de servicio de PDF](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Conversión de un documento de PDF en un archivo RTF mediante la API de Java {#convert-a-pdf-document-to-a-rtf-file-using-the-java-api}

Conversión de un documento de PDF en un archivo RTF mediante la API Generate PDF (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-generatepdf-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente Generate PDF.

   Crear un `GeneratePdfServiceClient` mediante su constructor y pasando un objeto `ServiceClientFactory` que contiene las propiedades de conexión.

1. Recupere el documento del PDF que desea convertir.

   * Crear un `java.io.FileInputStream` que representa el documento de PDF que se va a convertir mediante su constructor. Pase un valor de cadena que especifique la ubicación del documento del PDF.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Convierta el documento del PDF.

   Invoque el `GeneratePdfServiceClient` del objeto `exportPDF2` y pasar los siguientes valores:

   * A `com.adobe.idp.Document` que representa el archivo PDF que se va a convertir.
   * A `java.lang.String` que contiene el nombre del archivo que se va a convertir.
   * A `java.lang.String` que contiene el nombre de la configuración de Adobe PDF.
   * A `ConvertPDFFormatType` que especifica el tipo de archivo de destino para la conversión.
   * Un opcional `com.adobe.idp.Document` que contiene la configuración que se aplicará durante la generación del documento de PDF.

   El `exportPDF2` El método devuelve un `ExportPDFResult` que contiene el archivo convertido.

1. Convierta el documento del PDF.

   Para obtener el archivo recién creado, realice las siguientes acciones:

   * Invoque el `ExportPDFResult` del objeto `getConvertedDocument` método. Esto devuelve un `com.adobe.idp.Document` objeto.
   * Invoque el `com.adobe.idp.Document` del objeto `copyToFile` para extraer el nuevo documento.

**Consulte también**

[Resumen de los pasos](converting-file-formats-pdf.md#summary-of-steps)

[SOAP Inicio rápido (modo de): Conversión del contenido del HTML a un documento del PDF mediante la API de Java](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de un documento de PDF en un archivo RTF mediante la API de servicio web {#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api}

Conversión de un documento de PDF en un archivo RTF mediante la API Generate PDF (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente Generar PDF.

   * Crear un `GeneratePDFServiceClient` mediante su constructor predeterminado.
   * Crear un `GeneratePDFServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.) No es necesario que utilice el `lc_version` atributo. Sin embargo, especifique `?blob=mtom`.
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `GeneratePDFServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere el documento del PDF que desea convertir.

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar un documento de PDF convertido.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento de PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` asignando a su `MTOM` propiedad el contenido de la matriz de bytes.

1. Convierta el documento del PDF.

   Invoque el `GeneratePDFServiceServiceWse` del objeto `ExportPDF2` y pasar los siguientes valores:

   * A `BLOB` que representa el archivo PDF que se va a convertir.
   * Cadena que contiene el nombre de ruta del archivo que se va a convertir.
   * A `java.lang.String` que especifica la ubicación del archivo.
   * Un objeto de cadena que especifica el tipo de archivo de destino para la conversión. Especificar `RTF`.
   * Un opcional `BLOB` que contiene la configuración que se aplicará durante la generación del documento de PDF.
   * Un parámetro de salida de tipo `BLOB` que se rellena con la variable `ExportPDF2` método. El `ExportPDF2` rellena este objeto con el documento convertido. (Este valor de parámetro solo es necesario para la invocación del servicio web).

1. Guarde el archivo convertido.

   * Recupere el documento RTF convertido asignando el `BLOB` del objeto `MTOM` a una matriz de bytes. La matriz de bytes representa el documento RTF convertido. Asegúrese de utilizar el `BLOB` objeto que se utiliza como parámetro de salida para `ExportPDF2` método.
   * Crear un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo RTF.
   * Crear un `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo RTF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](converting-file-formats-pdf.md#summary-of-steps)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Añadir compatibilidad con formatos de archivo nativos adicionales {#adding-support-for-additional-native-file-formats}

Esta sección explica cómo agregar compatibilidad con formatos de archivo nativos adicionales. Proporciona una descripción general de las interacciones entre el servicio Generate PDF y las aplicaciones nativas que este servicio utiliza para convertir formatos de archivo nativos en PDF.

Esta sección también explica lo siguiente:

* Cómo modificar la respuesta que el servicio Generate PDF proporciona a las aplicaciones nativas que este producto ya utiliza para convertir formatos de archivo nativos en PDF
* Las interacciones entre el servicio Generate PDF, el componente Application Monitor (AppMon) del servicio Generate PDF y las aplicaciones nativas, como Microsoft Word
* Las funciones que desempeñan las gramáticas XML en esas interacciones

### Interacciones de componentes {#component-interactions}

El servicio Generate PDF convierte los formatos de archivo nativos invocando la aplicación asociada al formato de archivo e interactuando con la aplicación para imprimir el documento mediante la impresora predeterminada. La impresora predeterminada debe estar configurada como impresora de Adobe PDF.

Esta ilustración muestra los componentes y controladores implicados en la compatibilidad con aplicaciones nativas. También menciona las gramáticas XML que influyen en las interacciones.

Interacciones de componentes para la conversión de archivos nativos

Este documento utiliza el término *aplicación nativa* para indicar la aplicación utilizada para producir un formato de archivo nativo, como Microsoft Word.

*AppMon* es un componente de empresa que interactúa con una aplicación nativa del mismo modo que lo haría un usuario a través de los cuadros de diálogo que presenta esa aplicación. Las gramáticas XML utilizadas por AppMon para indicar a una aplicación, como Microsoft Word, que abra e imprima un archivo implican estas tareas secuenciales:

1. Abra el archivo seleccionando Archivo > Abrir
1. Comprobar que aparece el cuadro de diálogo Abrir; si no es así, controlar el error
1. Proporcione el nombre del archivo en el campo Nombre de archivo y haga clic en el botón Abrir
1. Comprobar que el archivo se abre realmente
1. Abrir el cuadro de diálogo Imprimir seleccionando Archivo > Imprimir
1. Comprobación de que aparece el cuadro de diálogo Imprimir

AppMon utiliza API estándar de Win32 para interactuar con aplicaciones de terceros y transferir eventos de interfaz de usuario, como pulsaciones de teclas y clics de mouse (ratón), lo que resulta útil para controlar estas aplicaciones y producir archivos PDF a partir de ellas.

Debido a una limitación con estas API de Win32, AppMon no puede distribuir estos eventos de interfaz de usuario a algunos tipos específicos de ventanas, como barras de menú flotantes (que se encuentran en algunas aplicaciones como TextPad) y cierto tipo de cuadros de diálogo cuyo contenido no se puede recuperar mediante las API de Win32.

Es fácil identificar visualmente una barra de menús flotante; sin embargo, es posible que no sea posible identificar los tipos especiales de diálogos solo mediante la inspección visual. Necesitaría una aplicación de terceros como Microsoft Spy++ (parte del entorno de desarrollo de Microsoft Visual C++) o su WinID equivalente (que se puede descargar gratuitamente desde [https://www.dennisbabkin.com/php/download.php?what=WinID](https://www.dennisbabkin.com/php/download.php?what=WinID)) para examinar un cuadro de diálogo y determinar si AppMon podría interactuar con él mediante las API estándar de Win32.

Si WinID puede extraer el contenido del cuadro de diálogo, como el texto, las ventanas secundarias, el ID de clase de ventana, etc., AppMon también podrá hacer lo mismo.

En esta tabla se muestra el tipo de información utilizada para imprimir formatos de archivo nativos.

<table>
 <thead>
  <tr>
   <th><p>Tipo de información</p></th>
   <th><p>Descripción</p></th>
   <th><p>Modificar/crear entradas relacionadas con archivos nativos </p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Configuración administrativa </p></td>
   <td><p>Incluye la configuración del PDF, la configuración de seguridad y la configuración del tipo de archivo. </p><p>La configuración de tipo de archivo asocia las extensiones de nombre de archivo con las aplicaciones nativas correspondientes. La configuración de tipo de archivo también especifica la configuración de la aplicación nativa utilizada para imprimir archivos nativos. </p></td>
   <td><p>Para cambiar la configuración de una aplicación nativa ya admitida, el administrador del sistema establece la Configuración de tipo de archivo en la consola de administración. </p><p>Para añadir compatibilidad con un nuevo formato de archivo nativo, debe editar manualmente el archivo. (Consulte <a href="converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format">Agregar o modificar la compatibilidad con un formato de archivo nativo</a>.) </p></td>
  </tr>
  <tr>
   <td><p>Script </p></td>
   <td><p>Especifica las interacciones entre el servicio Generate PDF y una aplicación nativa. Estas interacciones normalmente dirigen la aplicación para imprimir un archivo al controlador de Adobe PDF. </p><p>La secuencia de comandos contiene instrucciones que dirigen la aplicación nativa para abrir cuadros de diálogo específicos y que proporcionan respuestas específicas a los campos y botones de esos cuadros de diálogo. </p></td>
   <td><p>El servicio Generate PDF incluye archivos de script para todas las aplicaciones nativas admitidas. Puede modificar estos archivos mediante una aplicación de edición XML.</p><p>Para agregar compatibilidad con una nueva aplicación nativa, debe crear un archivo de script. (Consulte <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">Crear o modificar un archivo XML de diálogo adicional para una aplicación nativa</a>.) </p></td>
  </tr>
  <tr>
   <td><p>Instrucciones genéricas del cuadro de diálogo </p></td>
   <td><p>Especifica cómo responder a los cuadros de diálogo comunes a varias aplicaciones. Estos cuadros de diálogo los generan los sistemas operativos, las aplicaciones de ayuda (como PDFMaker) y los controladores. </p><p>El archivo que contiene esta información es appmon.global.en_US.xml.</p></td>
   <td><p>No modifique este archivo. </p></td>
  </tr>
  <tr>
   <td><p>Instrucciones del cuadro de diálogo específico de la aplicación</p></td>
   <td><p>Especifica cómo responder a los cuadros de diálogo específicos de la aplicación. </p><p>El archivo que contiene esta información es appmon.<i>`[appname]`</i>.dialog.<i>"[locale]"</i>.xml (por ejemplo, appmon.word.en_US.xml).</p></td>
   <td><p>No modifique este archivo. </p><p>Para agregar instrucciones de cuadro de diálogo para una nueva aplicación nativa, consulte <a href="converting-file-formats-pdf.md#creating_or_modifying_an_additional_dialog_xml_file_for_a_native_application">Crear o modificar un archivo XML de diálogo adicional para una aplicación nativa</a>.</p></td>
  </tr>
  <tr>
   <td><p>Instrucciones adicionales del cuadro de diálogo específico de la aplicación </p></td>
   <td><p>Especifica las invalidaciones y adiciones a las instrucciones del cuadro de diálogo específico de la aplicación. La sección presenta un ejemplo de dicha información. </p><p>El archivo que contiene esta información es appmon.<i>`[appname]`</i>.adición.<i>"[locale]"</i>.xml. Un ejemplo es appmon.add.en_US.xml.</p></td>
   <td><p>Los archivos de este tipo se pueden crear y modificar mediante una aplicación de edición XML. (Consulte <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">Crear o modificar un archivo XML de diálogo adicional para una aplicación nativa</a>.) </p><p><strong>Importante</strong>: cree instrucciones adicionales de cuadro de diálogo específicas para cada aplicación nativa que admitirá el servidor. </p></td>
  </tr>
 </tbody>
</table>

### Acerca de los archivos XML de script y diálogo {#about-the-script-and-dialog-xml-files}

Los archivos XML de secuencia de comandos dirigen el servicio Generate PDF para que navegue por los cuadros de diálogo de la aplicación del mismo modo que lo haría un usuario por los cuadros de diálogo de la aplicación. Los archivos XML de secuencia de comandos también dirigen el servicio Generate PDF para que responda a los cuadros de diálogo mediante acciones como presionar botones, seleccionar o anular la selección de casillas de verificación o seleccionar elementos de menú.

Por el contrario, los archivos XML de diálogo sólo responden a cuadros de diálogo con los mismos tipos de acciones utilizadas en los archivos XML de secuencias de comandos.

#### Terminología del cuadro de diálogo y del elemento de ventana {#dialog-box-and-window-element-terminology}

En esta sección y en la siguiente se utiliza una terminología diferente para los cuadros de diálogo y los componentes que contienen, según la perspectiva que se describa. Los componentes de cuadro de diálogo son elementos como botones, campos y cuadros combinados.

Cuando esta sección y la siguiente describen los cuadros de diálogo y sus componentes desde la perspectiva de un usuario, términos como *cuadro de diálogo*, *botón*, *campo*, y *cuadro combinado* se utilizan.

Cuando esta sección y la siguiente describen los cuadros de diálogo y sus componentes desde la perspectiva de su representación interna, el término *elemento window* se utiliza. La representación interna de los elementos de ventana es una jerarquía, donde cada instancia del elemento de ventana se identifica con etiquetas. La instancia del elemento window también describe sus características físicas y su comportamiento.

Desde la perspectiva de un usuario, los cuadros de diálogo y sus componentes muestran comportamientos diferentes, donde algunos elementos del cuadro de diálogo se ocultan hasta que se activan. Desde la perspectiva de la representación interna, no existe tal cuestión de comportamiento. Por ejemplo, la representación interna de un cuadro de diálogo tiene un aspecto similar al de los componentes que contiene, con la excepción de que los componentes están anidados en el cuadro de diálogo.

En esta sección se describen los elementos XML que proporcionan instrucciones a AppMon. Estos elementos tienen nombres como `dialog` y el elemento `window` Elemento. Este documento utiliza una fuente monoespaciada para distinguir los elementos XML. El `dialog` identifica un cuadro de diálogo que un archivo de secuencia de comandos XML puede hacer que se muestre, ya sea intencionada o involuntariamente. El `window` identifica un elemento de ventana (cuadro de diálogo o los componentes de un cuadro de diálogo).

#### Jerarquía {#hierarchy}

Este diagrama muestra la jerarquía del script y el XML de diálogo. Un archivo XML de secuencia de comandos se ajusta al esquema script.xsd, que incluye (en el sentido XML) el esquema window.xsd. Del mismo modo, un archivo XML de diálogo se ajusta al esquema dialog.xsd, que también incluye el esquema window.xsd.

![as_as_xml_hierarchy](assets/as_as_xml_hierarchy.png)

Jerarquía de script y XML de diálogo

#### Archivos XML de script {#script-xml-files}

A *archivo XML de script* especifica una serie de pasos que indican a la aplicación nativa que se desplace hasta determinados elementos de la ventana y que, a continuación, proporcionen respuestas a dichos elementos. La mayoría de las respuestas son texto o pulsaciones de teclas que corresponden a la entrada que un usuario proporcionaría a un campo, cuadro combinado o botón del cuadro de diálogo correspondiente.

La intención de la compatibilidad del servicio Generate PDF con los archivos XML de script es dirigir una aplicación nativa para imprimir un archivo nativo. Sin embargo, los archivos XML de secuencias de comandos se pueden utilizar para realizar cualquier tarea que pueda realizar un usuario al interactuar con los cuadros de diálogo de la aplicación nativa.

Los pasos de un archivo XML de script se ejecutan en orden, sin ninguna oportunidad de bifurcación. La única prueba condicional admitida es el tiempo de espera/reintento, que hace que una secuencia de comandos se termine si un paso no se completa correctamente en un período de tiempo específico y después de un número específico de reintentos.

Además de los pasos que son secuenciales, las instrucciones dentro de un paso también se ejecutan en orden. Asegúrese de que los pasos e instrucciones reflejen el orden en que un usuario realizaría esos mismos pasos.

Cada paso de un archivo XML de secuencia de comandos identifica el elemento window que se espera que aparezca si las instrucciones del paso se realizan correctamente. Si aparece un cuadro de diálogo inesperado al ejecutar un paso de script, el servicio Generate PDF busca los archivos XML de diálogo como se describe en la siguiente sección.

#### Archivos XML de diálogo {#dialog-xml-files}

La ejecución de aplicaciones nativas muestra diferentes cuadros de diálogo, que aparecen independientemente de si las aplicaciones nativas están en modo visible o invisible. Los cuadros de diálogo pueden ser generados por el sistema operativo o por la propia aplicación. Cuando las aplicaciones nativas se ejecutan bajo el control del servicio Generate PDF, los cuadros de diálogo system y native application se muestran en una ventana invisible.

A *archivo XML de diálogo* especifica cómo responde el servicio Generate PDF a los cuadros de diálogo del sistema o de la aplicación nativa. Los archivos XML de diálogo permiten que el servicio Generate PDF responda a los cuadros de diálogo no solicitados de forma que facilite el proceso de .

Cuando el sistema o la aplicación nativa muestra un cuadro de diálogo que no está controlado por el archivo XML de secuencia de comandos que se está ejecutando, el servicio Generate PDF busca los archivos XML de diálogo en este orden y se detiene cuando encuentra una coincidencia:

* ¡Applón!`[appname]`.additional.`[locale]`.xml
* ¡Applón!`[appname]`.`[locale]`.xml (No modifique este archivo).
* appmon.global.`[locale]`.xml (No modifique este archivo).

Si el servicio Generar PDF encuentra una coincidencia para el cuadro de diálogo, lo descarta enviándole la pulsación de tecla u otra acción especificada para el cuadro de diálogo. Si las instrucciones del cuadro de diálogo especifican un mensaje de anulación, el servicio Generate PDF finaliza el trabajo que se está ejecutando y genera un mensaje de error. Este mensaje de anulación se especificaría en la variable `abortMessage` en la gramática XML del script.

Si el servicio Generar PDF encuentra un cuadro de diálogo que no se describe en ninguno de los archivos enumerados anteriormente, el servicio Generar PDF incorpora el título del cuadro de diálogo en la entrada del archivo de registro. El trabajo que se está ejecutando finaliza el tiempo de espera. A continuación, puede utilizar la información del archivo de registro para crear nuevas instrucciones en el archivo XML de diálogo adicional para la aplicación nativa.

### Agregar o modificar la compatibilidad con un formato de archivo nativo {#adding-or-modifying-support-for-a-native-file-format}

En esta sección se describen las tareas que debe realizar para admitir otros formatos de archivo nativos o para modificar la compatibilidad con un formato de archivo nativo ya admitido.

Antes de agregar o modificar la compatibilidad, debe completar las tareas siguientes.

#### Selección de una herramienta para identificar los elementos de la ventana {#choosing-a-tool-for-identifying-window-elements}

Los archivos XML de diálogo y script requieren que identifique el elemento window (cuadro de diálogo, campo u otro componente de diálogo) al que responde el elemento dialog o script. Por ejemplo, después de que un script invoque un menú para una aplicación nativa, el script debe identificar el elemento window de ese menú al que se deben aplicar las pulsaciones de teclas o una acción.

Puede identificar fácilmente un cuadro de diálogo por el título que muestra en su barra de título. Sin embargo, debe utilizar una herramienta como Microsoft Spy++ para identificar los elementos de ventana de nivel inferior. Los elementos de ventana de nivel inferior se pueden identificar mediante una variedad de atributos, que no son obvios. Además, cada aplicación nativa puede identificar su elemento de ventana de forma diferente. Como resultado, hay varias formas de identificar un elemento window. Este es el orden sugerido para considerar la identificación de elementos de ventana:

1. Pie de ilustración si es único
1. ID de control, que puede ser único o no para un cuadro de diálogo determinado
1. Nombre de clase, que puede ser único o no

Cualquiera de estos tres atributos, o una combinación de ellos, puede utilizarse para identificar una ventana.

Si los atributos no identifican un pie de ilustración, puede identificar un elemento de ventana mediante su índice con respecto a su elemento principal. Un *índice* especifica la posición del elemento window en relación con los elementos window del mismo nivel. Con frecuencia, los índices son la única manera de identificar los cuadros combinados.

Tenga en cuenta los siguientes problemas:

* Microsoft Spy++ muestra los subtítulos utilizando un signo &amp; para identificar la tecla de acceso directo del subtítulo. Por ejemplo, Spy++ muestra el título de un cuadro de diálogo Imprimir como `Pri&nt`, que indica que la tecla de acceso directo es *n*. Los títulos de los títulos de los archivos XML de script y diálogo deben omitir el símbolo et.
* Algunos subtítulos incluyen saltos de línea. el servicio Generar PDF no puede identificar saltos de línea. Si un pie de ilustración incluye un salto de línea, incluya suficiente para diferenciarlo de los demás elementos de menú y, a continuación, utilice expresiones regulares para el fragmento omitido. Un ejemplo es ( `^Long caption title$`). (Consulte [Uso de expresiones regulares en atributos de rótulo](converting-file-formats-pdf.md#using-regular-expressions-in-caption-attributes).)
* Utilice entidades de caracteres (también denominadas secuencias de escape) para caracteres XML reservados. Por ejemplo, use `&` para el símbolo et, `<` y `>` para símbolos menor que y mayor que, `&apos;` para apóstrofos, y `&quot;` para las comillas.

Si planea trabajar en archivos XML de cuadros de diálogo o secuencias de comandos, debe instalar la aplicación Microsoft Spy++.

#### Desempaquetado de los archivos de diálogo y script {#unpackaging-the-dialog-and-script-files}

Los archivos de cuadro de diálogo y de script residen en el archivo appmondata.jar. Antes de poder modificar cualquiera de estos archivos o agregar nuevos archivos de script o de diálogo, debe desempaquetar este archivo JAR. Por ejemplo, supongamos que desea añadir compatibilidad con la aplicación EditPlus. Puede crear dos archivos XML, llamados appmon.editplus.script.en_US.xml y appmon.editplus.script.additplus.en_US.xml. Estos scripts XML deben agregarse al archivo adobe-appmondata.jar en dos ubicaciones, como se especifica a continuación:

* adobe-livecycle-native-jboss-x86_win32.ear > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar\com\adobe\appmon. El archivo adobe-livecycle-native-jboss-x86_win32.ear se encuentra en la carpeta de exportación en `[AEM forms install directory]\configurationManager`. (si AEM Forms está implementado en otro servidor de aplicaciones J2EE, sustituya el archivo adobe-livecycle-native-jboss-x86_win32.ear por el archivo EAR que corresponda a su servidor de aplicaciones J2EE).
* adobe-generatepdf-dsc.jar > adobe-appmondata.jar\com\adobe\appmon (el archivo adobe-appmondata.jar se encuentra dentro del archivo adobe-generatepdf-dsc.jar). El archivo adobe-generatepdf-dsc.jar se encuentra en `[AEM forms install directory]\deploy` carpeta.

Después de agregar estos archivos XML al archivo adobe-appmondata.jar, debe volver a implementar el componente GeneratePDF. Para agregar archivos XML de cuadros de diálogo y secuencias de comandos al archivo adobe-appmondata.jar, realice estas tareas:

1. Con una herramienta como WinZip o WinRAR, abra el archivo adobe-livecycle-native-jboss-x86_win32.earfile > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar > adobe-appmondata.jar.
1. Agregue los archivos XML de cuadro de diálogo y secuencia de comandos al archivo appmondata.jar o modifique los archivos XML existentes en este archivo. (Consulte [Crear o modificar un archivo XML de secuencia de comandos para una aplicación nativa](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)y [Crear o modificar un archivo XML de diálogo adicional para una aplicación nativa](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application).)
1. Con una herramienta como WinZip o WinRAR, abra adobe-generatepdf-dsc.jar > adobe-appmondata.jar.
1. Agregue los archivos XML de cuadro de diálogo y secuencia de comandos al archivo appmondata.jar o modifique los archivos XML existentes en este archivo. (Consulte [Crear o modificar un archivo XML de secuencia de comandos para una aplicación nativa](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)y [Crear o modificar un archivo XML de diálogo adicional para una aplicación nativa](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application).) Después de agregar los archivos XML al archivo adobe-appmondata.jar, coloque el nuevo archivo adobe-appmondata.jar en el archivo adobe-generatepdf-dsc.jar.
1. Si ha agregado compatibilidad con un formato de archivo nativo adicional, cree una variable de entorno del sistema que proporcione la ruta de la aplicación (Consulte [Creación de una variable de entorno para localizar la aplicación nativa](converting-file-formats-pdf.md#creating-an-environment-variable-to-locate-the-native-application).)

**Para volver a implementar el componente GeneratePDF**

1. Inicie sesión en Workbench.
1. Seleccionar **Ventana** > **Mostrar vistas** > **Componentes**. Esta acción añade la vista Componentes a Workbench.
1. Haga clic con el botón derecho en el componente GeneratePDF y seleccione **Detener componente**.
1. Cuando el componente se haya detenido, haga clic con el botón derecho y seleccione Desinstalar componente para eliminarlo.
1. Haga clic con el botón derecho en **Componentes** y seleccione **Instalar componente**.
1. Busque y seleccione el archivo adobe-generatepdf-dsc.jar modificado y, a continuación, haga clic en Abrir. Observe que aparece un cuadrado rojo junto al componente GeneratePDF.
1. Expanda el componente GeneratePDF, seleccione Descriptores de servicio, haga clic con el botón derecho en GeneratePDFService y seleccione Activar servicio.
1. En el cuadro de diálogo de configuración que aparece, introduzca los valores de configuración aplicables. Si deja estos valores en blanco, se utilizan los valores de configuración predeterminados.
1. Haga clic con el botón derecho en GeneratePDF y seleccione Start Component.
1. Expanda Servicios activos. Si se está ejecutando, aparecerá una flecha verde junto al nombre del servicio. De lo contrario, el servicio está en estado detenido.
1. Si el servicio está en estado detenido, haga clic con el botón derecho en el nombre del servicio y seleccione Iniciar servicio.

### Crear o modificar un archivo XML de secuencia de comandos para una aplicación nativa {#creating-or-modifying-a-script-xml-file-for-a-native-application}

Si desea dirigir los archivos a una nueva aplicación nativa, debe crear un archivo XML de secuencia de comandos para esa aplicación. Si desea modificar la forma en que el servicio Generate PDF interactúa con una aplicación nativa ya admitida, deberá modificar el script de dicha aplicación.

La secuencia de comandos contiene instrucciones que permiten navegar por los elementos window de la aplicación nativa y proporcionar respuestas específicas a dichos elementos. El archivo que contiene esta información es `appmon.`[appname]&quot; `.script.`[locale]`.xml`. Un ejemplo es appmon.notepad.script.en_US.xml.

#### Identificación de los pasos que debe ejecutar el script {#identifying-steps-the-script-must-execute}

Con la aplicación nativa, determine los elementos de ventana que debe desplazarse y cada respuesta que debe realizar para imprimir el documento. Fíjese en los cuadros de diálogo que resultan de cualquier respuesta. Los pasos son similares a estos pasos:

1. Seleccione Archivo > Abrir.
1. Especifique la ruta y haga clic en Abrir.
1. Seleccione Archivo > Imprimir en la barra de menús.
1. Especifique las propiedades necesarias para la impresora.
1. Seleccione Imprimir y espere a que aparezca el cuadro de diálogo Guardar como. El cuadro de diálogo Guardar como es necesario para que el servicio Generate PDF especifique el destino del archivo de PDF.

#### Identificación de los cuadros de diálogo especificados en los atributos de rótulo {#identifying-the-dialogs-specified-in-caption-attributes}

Utilice Microsoft Spy++ para obtener las identidades de las propiedades de los elementos de ventana en la aplicación nativa. Debe tener estas identidades para escribir scripts.

#### Uso de expresiones regulares en atributos de rótulo {#using-regular-expressions-in-caption-attributes}

Puede utilizar expresiones regulares en las especificaciones de los subtítulos. El servicio Generar PDF utiliza el `java.util.regex.Matcher` para admitir expresiones regulares. Esa utilidad admite las expresiones regulares descritas en `java.util.regex.Pattern`.

**Expresión regular que acomoda el nombre de archivo anexado al Bloc de notas en el titular del Bloc de notas**

```xml
 <!-- The regular expression ".*Notepad" means any number of non-terminating characters followed by Notepad. -->
 <step>
     <expectedWindow>
         <window caption=".*Notepad"/>
     </expectedWindow>
 </step>
```

**Expresión regular que diferencia Imprimir de Configuración de impresión**

```xml
 <!-- This regular expression differentiates the Print dialog box from the Print Setup dialog box. The "^" specifies the beginning of the line, and the "$" specifies the end of the line. -->
 <windowList>
     <window controlID="0x01" caption="^Print$" action="press"/>
 </windowList>
```

#### Ordenación de los elementos window y windowList {#ordering-the-window-and-windowlist-elements}

Pedido `window` y `windowList` como se indica a continuación:

* Cuando hay varios `window` Los elementos de aparecen como elementos secundarios en una `windowList` o `dialog` elemento, ordene esos `window` elementos en orden descendente, con las longitudes del `caption` nombres que indiquen la posición en el orden.
* Cuando hay varios `windowList` elementos aparecen en una `window` elemento, ordene esos `windowList` elementos en orden descendente, con las longitudes del `caption` atributos del primero `indexes/`que indica la posición en el orden.

**Ordenación de elementos de ventana en un fichero de diálogo**

```xml
 <!-- The caption attribute in the following window element is 40 characters long. It is the longest caption in this example, so its parent window element appears before the others. -->
 <window caption="Unexpected Failure in DebugActiveProcess">
     <…>
 </window>

 <!-- Caption length is 33 characters. -->
 <window caption="Adobe Acrobat - License Agreement">
     <…>
 </window>

 <!-- Caption length is 33 characters. -->
 <window caption="Microsoft Visual.*Runtime Library">
     <…>
 </window>

 <!-- The caption attribute in the following window element is 28 characters long. It is the shortest caption in this example, so its parent window element appears after the others. -->
 <window caption="Adobe Acrobat - Registration">
     <…>
 </window>
```

**Ordenación de elementos window dentro de un elemento windowList**

```xml
 <!-- The caption attribute in the following indexes element is 56 characters long. It is the longest caption in this example, so its parent window element appears before the others. -->
 <windowList>
     <window caption="Can&apos;t exit design mode because.* cannot be created"/>
     <window className="Button" caption="OK" action="press"/>
 </windowList>
 <windowList>
     <window caption="Do you want to continue loading the project?"/>
     <window className="Button" caption="No" action="press"/>
 </windowList>
 <windowList>
     <window caption="The macros in this project are disabled"/>
     <window className="Button" caption="OK" action="press"/>
 </windowList>
```

### Crear o modificar un archivo XML de diálogo adicional para una aplicación nativa {#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application}

Si crea una secuencia de comandos para una aplicación nativa que no era compatible anteriormente, también debe crear un archivo XML de diálogo adicional para esa aplicación. Cada aplicación nativa que utiliza AppMon debe tener solo un archivo XML de diálogo adicional. El archivo XML de diálogo adicional es necesario aunque no se esperen cuadros de diálogo no solicitados. El cuadro de diálogo adicional debe tener al menos uno `window` elemento, aunque sea `window` es simplemente un marcador de posición.

>[!NOTE]
>
>En este contexto, el término adicional significa el contenido de la `appmon.[applicationname].addition.[locale].xml` archivo. Este archivo especifica las anulaciones y adiciones al archivo XML de diálogo.

También puede modificar el archivo XML de diálogo adicional para una aplicación nativa con estos fines:

* Para anular el archivo XML de cuadro de diálogo de una aplicación con una respuesta diferente
* Para agregar una respuesta a un cuadro de diálogo que no está incluido en el archivo XML de diálogo de esa aplicación

El nombre de archivo que identifica un archivo dialogXML adicional es `appmon.[appname].addition.[locale].xml`. Un ejemplo es appmon.excel.add.en_US.xml.

El nombre del fichero XML de diálogo adicional debe utilizar el formato `appmon.[applicationname].addition.[locale].xml`, donde *applicationName* debe coincidir exactamente con el nombre de aplicación utilizado en el archivo de configuración XML y en la secuencia de comandos.

>[!NOTE]
>
>Ninguna de las aplicaciones genéricas especificadas en el archivo de configuración native2pdfconfig.xml tiene un archivo XML de diálogo principal. La sección [Agregar o modificar la compatibilidad con un formato de archivo nativo](converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format) describe dichas especificaciones.

Pedido `windowList` elementos que aparecen como elementos secundarios en una `window` Elemento. (Consulte [Ordenación de los elementos window y windowList](converting-file-formats-pdf.md#ordering-the-window-and-windowlist-elements).)

### Modificación del archivo XML de diálogo general {#modifying-the-general-dialog-xml-file}

Puede modificar el archivo XML de diálogo general para responder a cuadros de diálogo generados por el sistema o para responder a cuadros de diálogo comunes a varias aplicaciones.

#### Agregar una entrada de tipo de archivo en el archivo de configuración XML {#adding-a-filetype-entry-in-the-xml-configuration-file}

En este procedimiento se explica cómo actualizar el archivo de configuración del servicio Generate PDF para asociar tipos de archivo con aplicaciones nativas. Para actualizar este archivo de configuración, debe utilizar la consola de administración para exportar los datos de configuración a un archivo. El nombre de archivo predeterminado para los datos de configuración es native2pdfconfig.xml.

**Actualizar el archivo de configuración del servicio Generar PDF**

1. Seleccionar **Inicio** > **Servicios** > **Generador de Adobe PDF** > **Archivos de configuración**, y luego seleccione **Configuración de exportación**.
1. Modifique la `filetype-settings` en el archivo native2pdfconfig.xml, según sea necesario.
1. Seleccionar **Inicio** > **Servicios** > **Generador de Adobe PDF** >**Archivos de configuración**, y luego seleccione **Importar configuración**. Los datos de configuración se importan en el servicio Generate PDF y reemplazan la configuración anterior.

>[!NOTE]
>
>El nombre de la aplicación se especifica como el valor del `GenericApp` del elemento `name` atributo. Este valor debe coincidir exactamente con el nombre correspondiente especificado en el script que desarrolle para esa aplicación. Del mismo modo, la variable `GenericApp` del elemento `displayName` debe coincidir exactamente con el atributo del script correspondiente `expectedWindow` pie de ilustración de ventana. Esta equivalencia se evalúa después de resolver cualquier expresión regular que aparezca en el `displayName` o `caption` atributos.

En este ejemplo, los datos de configuración predeterminados suministrados con el servicio Generate PDF se modificaron para especificar que se debe utilizar Notepad (no Microsoft Word) para procesar archivos con la extensión de nombre de archivo .txt. Antes de esta modificación, se especificó Microsoft Word como la aplicación nativa que debe procesar dichos archivos.

**Modificaciones para dirigir archivos de texto al Bloc de notas (native2pdfconfig.xml)**

```xml
 <filetype-settings>

 <!-- Some native app file types were omitted for brevity. -->
 <!-- The following GenericApp element specifies Notepad as the native application that should be used to process files that have a txt file name extension. -->
             <GenericApp
                 extensions="txt"
                 name="Notepad" displayName=".*Notepad"/>
             <GenericApp
                 extensions="wpd"
                 name="WordPerfect" displayName="Corel WordPerfect"/>
             <GenericApp extensions="pmd,pm6,p65,pm"
                 name="PageMaker" displayName="Adobe PageMaker"/>
             <GenericApp extensions="fm"
                 name="FrameMaker" displayName="Adobe FrameMaker"/>
             <GenericApp extensions="psd"
                 name="Photoshop" displayName="Adobe Photoshop"/>
         </settings>
     </filetype-settings>
```

#### Creación de una variable de entorno para localizar la aplicación nativa {#creating-an-environment-variable-to-locate-the-native-application}

Cree una variable de entorno que especifique la ubicación del ejecutable de la aplicación nativa. La variable debe utilizar el formato `[applicationname]_PATH`, donde *applicationName* debe coincidir exactamente con el nombre de aplicación utilizado en el archivo de configuración XML y en la secuencia de comandos, y donde la ruta de acceso contiene la ruta de acceso al ejecutable entre comillas dobles. Un ejemplo de esta variable de entorno es `Photoshop_PATH`.

Después de crear la nueva variable de entorno, debe reiniciar el servidor en el que se implementa el servicio Generate PDF.

>[!NOTE]
>
> Se recomienda utilizar el comando &quot;Ctrl + C&quot; para reiniciar el servidor SDK. AEM AEM El reinicio del servidor del SDK de la mediante métodos alternativos, como detener los procesos de Java, puede generar incoherencias en el entorno de desarrollo de la.

**Crear una variable del sistema en el entorno de Windows XP**

1. Seleccionar **Panel de control de Campaign > Sistema**.
1. En el cuadro de diálogo Propiedades del sistema, haga clic en **Avanzadas** y luego haga clic en **Variables de entorno**.
1. En Variables del sistema, en el cuadro de diálogo Variables de entorno, haga clic en **Nuevo**.
1. En el cuadro de diálogo Nueva variable del sistema, en la variable **Nombre de variable** , escriba un nombre que utilice el formato `[applicationname]_PATH`.
1. En el **Valor variable** , escriba la ruta de acceso completa y el nombre del archivo ejecutable de la aplicación y, a continuación, haga clic en **OK**. Por ejemplo, escriba: `c:\windows\Notepad.exe`
1. En el cuadro de diálogo Variables de entorno, haga clic en **OK**.

**Crear una variable del sistema desde la línea de comandos**

1. En una ventana de línea de comandos, escriba la definición de la variable con este formato:

   ```shell
            [applicationname]_PATH=[Full path name]
   ```

   Por ejemplo, escriba: `NotePad_PATH=C:\WINDOWS\NOTEPAD.EXE`

1. Inicie un nuevo símbolo del sistema para que la variable del sistema surta efecto.

#### Archivos XML {#xml-files}

AEM Forms incluye archivos XML de ejemplo que hacen que el servicio Generate PDF utilice Notepad para procesar cualquier archivo con la extensión de nombre de archivo .txt. Este código se incluye en esta sección. Además, debe realizar las demás modificaciones que se describen en esta sección.

#### Archivo XML de diálogo adicional {#additional-dialog-xml-file}

Este ejemplo contiene los cuadros de diálogo adicionales para la aplicación Bloc de notas. Estos cuadros de diálogo se pueden añadir a los especificados por el servicio Generate PDF.

**Cuadros de diálogo del Bloc de notas(appmon.notepad.add.en_US.xml)**

```xml
 <dialogs app="Notepad" locale="en_US" version="7.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="dialogs.xsd">
     <window caption="Caption Title">
         <windowList>
             <window className="Button" caption="OK" action="press"/>
         </windowList>
     </window>
 </dialogs>
```

#### Archivo XML de script {#script-xml-file}

En este ejemplo se especifica cómo debe interactuar el servicio Generate PDF con el Bloc de notas para imprimir archivos mediante la impresora Adobe PDF.

**Archivo XML de script de Bloc de notas (appmon.notepad.script.en_US.xml)**

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<!--
*
* ADOBE CONFIDENTIAL
* ___________________
* Copyright 2004 - 2005 Adobe Systems Incorporated
* All Rights Reserved.
*
* NOTICE:  All information contained herein is, and remains
* the property of Adobe Systems Incorporated and its suppliers,
* if any.  The intellectual and technical concepts contained
* herein are proprietary to Adobe Systems Incorporated and its
* suppliers and may be covered by U.S. and Foreign Patents,
* patents in process, and are protected by trade secret or copyright law.
* Dissemination of this information or reproduction of this material
* is strictly forbidden unless prior written permission is obtained
* from Adobe Systems Incorporated.
*-->

<!-- This file automates printing of text files via notepad to Adobe PDF printer. To see the complete hierarchy Adobe recommends using the Microsoft Spy++ which details the properties of windows necessary to write scripts. In this sample there are total of eight steps-->

<application name="Notepad" version="9.0" locale="en_US" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="scripts.xsd">

    <!-- In this step we wait for the application window to appear -->
    <step>
        <expectedWindow>
            <window caption=".*Notepad"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the application window and send File->Open menu bar, menu item commands and the expectation is the windows Open dialog-->
    <step>
        <acquiredWindow>
            <window caption=".*Notepad">
                <virtualInput>
                    <menuBar>
                        <selection>
                            <name>File</name>
                        </selection>
                        <selection>
                            <name>Open...</name>
                        </selection>
                    </menuBar>
                </virtualInput>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Open"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the Open window and then select the 'Edit' widget and input the source path followed by clicking on the 'Open' button . The expectation of this 'action' is that the Open dialog will disappear -->
    <step>
        <acquiredWindow>
            <window caption="Open">
                <windowList>
                    <window className="ComboBoxEx32">
                        <windowList>
                            <window className="ComboBox">
                                <windowList>
                                <window className="Edit" action="inputSourcePath"/>
                                </windowList>
                            </window>
                        </windowList>
                    </window>
                </windowList>
                <windowList>
                    <window className="Button" caption="Open" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Open" action="disappear"/>
        </expectedWindow>
        <pause value="30"/>
    </step>

    <!-- In this step, we acquire the application window and send File->Print menu bar, menu item commands and the expectation is the windows Print dialog-->
    <step>
        <acquiredWindow>
            <window caption=".*Notepad">
                <virtualInput>
                    <menuBar>
                        <selection>
                            <name>File</name>
                        </selection>
                        <selection>
                            <name>Print...</name>
                        </selection>
                    </menuBar>
                </virtualInput>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Print">
        </window>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the Print dialog and click the 'Preferences' button and the expected window in this case is the dialog with the caption '"Printing Preferences' -->
    <step>
        <acquiredWindow>
            <window caption="Print">
                <windowList>
                    <window caption="General">
                        <windowList>
                            <window className="Button" caption="Preferences" action="press"/>
                        </windowList>
                    </window>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Printing Preferences"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the dialog "Printing Preferences' and select the combo box which is the 10th child of window with caption '"Adobe PDF Settings' and select the first index. (Note: All indeces start with 0.) Besides this we uncheck the box which has the caption '"View Adobe PDF results' and we click the button OK. The expectation is that 'Printing Preferences' dialog disappears. -->
    <step>
        <acquiredWindow>
            <window caption="Printing Preferences">
                <windowList>
                    <window caption="Adobe PDF Settings">
                        <windowList>
                            <window className="Button" caption="View Adobe PDF results" action="uncheck"/>
                        </windowList>
                        <windowList>
                            <window className="Button" caption="Ask to Replace existing PDF file" action="uncheck"/>
                        </windowList>
                    </window>
                </windowList>
                <windowList>
                    <window className="Button" caption="OK" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Printing Preferences" action="disappear"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the 'Print' dialog and click the Print button. The expectation is that the dialog with caption 'Print' disappears. In this case we use the regular expression '^Print$' for specifying the caption given there could be multiple dialogs with caption that includes the word Print. -->
    <step>
        <acquiredWindow>
            <window caption="Print">
                <windowList>
                    <window caption="General"/>
                    <window className="Button" caption="^Print$" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Print" action="disappear"/>
        </expectedWindow>
    </step>
    <step>
        <expectedWindow>
            <window caption="Save PDF File As"/>
        </expectedWindow>
    </step>
    <!-- Finally in this step, we acquire the dialog with caption "Save PDF File As" and in the Edit widget type the destination path for the output PDF file and click the Save button. The expectation is that the dialog disappears-->
    <step>
        <acquiredWindow>
            <window caption="Save PDF File As">
                <windowList>
                    <window className="Edit" action="inputDestinationPath"/>
                </windowList>
                <windowList>
                    <window className="Button" caption="Save" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Save PDF File As" action="disappear"/>
        </expectedWindow>
    </step>

    <!-- We can always set a retry count or a maximum time for a step. In case we surpass these limitations, PDF Generator generates this abort message and terminates processing. -->
    <abortMessage msg="15078"/>
</application>
```
