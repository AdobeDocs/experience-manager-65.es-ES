---
title: Conversión de Postscript a documentos PDF
seo-title: Conversión de Postscript a documentos PDF
description: nulo
seo-description: nulo
uuid: 2143f406-1fdd-4551-a738-1a8388f8d478
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 06ad343a-f74d-41f5-b3c8-b85bb723ceeb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Conversión de Postscript a documentos PDF {#converting-postscript-to-pdf-documents}

## Acerca del servicio Distiller {#about-the-distiller-service}

El servicio Distiller® convierte archivos PostScript®, Encapsulated PostScript (EPS) y PRN en archivos PDF compactos, fiables y más seguros a través de una red. El servicio Distiller se utiliza con frecuencia para convertir grandes volúmenes de documentos impresos en documentos electrónicos, como facturas y estados de cuentas. La conversión de documentos a PDF también permite a las empresas enviar a sus clientes una versión en papel y una versión electrónica de un documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio Distiller, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversión de PostScript a documentos PDF {#converting-postscript-to-pdf-documents-inner}

En este tema se describe cómo puede utilizar la API de servicio de Distiller (Java y servicio web) para convertir en forma programada archivos PostScript (PS), PostScript encapsulado (EPS) y PRN en documentos PDF.

>[!NOTE]
>
>Para obtener más información sobre el servicio Distiller, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para convertir archivos PostScript en documentos PDF, debe instalarse una de las siguientes opciones en el servidor que aloja AEM Forms: Paquete redistribuible de Acrobat 9 o Microsoft Visual C++ 2005.

### Resumen de los pasos {#summary-of-steps}

Para convertir cualquiera de los tipos admitidos en un documento PDF, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de Distiller.
1. Recupere el archivo que desea convertir.
1. Invoque la operación de creación de PDF.
1. Guarde el documento PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Crear un cliente de servicio Distiller**

Para poder realizar una operación de servicio de Distiller mediante programación, debe crear un cliente de servicio de Distiller. Si utiliza la API de Java, cree un `DistillerServiceClient` objeto. Si utiliza la API de servicio Web, cree un `DistillerServiceService` objeto.

**Recuperar el archivo para convertir**

Debe recuperar el archivo que desea convertir. Por ejemplo, para convertir un archivo PS a un documento PDF, debe recuperar el archivo PS.

**Invocar la operación de creación de PDF**

Después de crear el cliente de servicio, puede invocar la operación de creación de PDF. Esta operación necesitará información sobre el documento que se va a convertir, incluida la ruta al documento de destino.

**Guardar el documento PDF**

Puede guardar el documento PDF como archivo PDF.

**Consulte también**

[Convertir un archivo PostScript a PDF mediante la API de Java](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[Conversión de un archivo PostScript a PDF mediante la API de servicio Web](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de API de servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Convertir un archivo PostScript a PDF mediante la API de Java {#convert-a-postscript-file-to-pdf-using-the-java-api}

Conversión de un archivo PostScript a un documento PDF mediante la API de Distiller Service (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-distiller-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de servicio de Distiller.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `DistillerServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recupere el archivo que desea convertir.

   * Cree un `java.io.FileInputStream` objeto que represente el archivo que se va a convertir utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Invoque la operación de creación de PDF.

   Invoque el `DistillerServiceClient` método del `createPDF` objeto y pase los valores siguientes:

   * El `com.adobe.idp.Document` objeto que representa el archivo PS, EPS o PRN que se va a convertir
   * Un `java.lang.String` objeto que contiene el nombre del archivo que se va a convertir
   * Un `java.lang.String` objeto que contiene el nombre de la configuración de Adobe PDF que se va a utilizar
   * Un `java.lang.String` objeto que contiene el nombre de la configuración de seguridad que se va a utilizar
   * Un `com.adobe.idp.Document` objeto opcional que contiene la configuración que se va a aplicar al generar el documento PDF
   * Objeto opcional `com.adobe.idp.Document` que contiene información de metadatos que se aplicará al documento PDF
   El `createPDF` método devuelve un `CreatePDFResult` objeto que contiene el nuevo documento PDF y un archivo de registro que se puede generar. El archivo de registro generalmente contiene mensajes de error o de advertencia generados por la solicitud de conversión.

1. Guarde el documento PDF.

   Para obtener el documento PDF recién creado, realice las siguientes acciones:

   * Invocar el `CreatePDFResult` método del `getCreatedDocument` objeto. Esto devuelve un `com.adobe.idp.Document` objeto.
   * Invocar el `com.adobe.idp.Document` método del `copyToFile` objeto para extraer el documento PDF.
   Del mismo modo, para obtener el documento de registro, realice las siguientes acciones.

   * Invocar el `CreatePDFResult` método del `getLogDocument` objeto. Esto devuelve un `com.adobe.idp.Document` objeto.
   * Invocar el `com.adobe.idp.Document` método del `copyToFile` objeto para extraer el documento de registro.


**Consulte también**

[Resumen de los pasos](converting-postscript-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Conversión de un archivo PostScript a un documento PDF mediante la API de Java](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de un archivo PostScript a PDF mediante la API de servicio Web {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

Convertir un archivo PostScript a un documento PDF mediante la API de servicio de Distiller (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de servicio de Distiller.

   * Cree un `DistillerServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `DistillerServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/DistillerService?blob=mtom`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para usar MTOM.
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `DistillerServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `DistillerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DistillerServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere el archivo que desea convertir.

   * Cree un `BLOB` objeto con su constructor. Este `BLOB` objeto se utiliza para almacenar el archivo que se va a convertir en un documento PDF.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo y el modo en el que desea abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` propiedad con el contenido de la matriz de bytes.

1. Invoque la operación de creación de PDF.

   Invoque el `DistillerServiceService` método del `CreatePDF2` objeto y pase los siguientes valores obligatorios:

   * El `BLOB` objeto que representa el archivo PS que se va a convertir
   * Una cadena que contiene el nombre de ruta del archivo que se va a convertir
   * Objeto de cadena que contiene la configuración de Adobe PDF que se va a utilizar (por ejemplo, `Standard`)
   * Objeto de cadena que contiene la configuración de seguridad que se va a utilizar (por ejemplo, `No Securit`y)
   * Un `BLOB` objeto opcional que contiene la configuración que se va a aplicar al generar el documento PDF
   * Objeto opcional `BLOB` que contiene información de metadatos que se aplicará al documento PDF
   * Parámetro `BLOB` de salida utilizado para almacenar el documento PDF
   * Parámetro `BLOB` de salida utilizado para almacenar el registro

1. Guarde el documento PDF.

   * Cree un `System.IO.FileStream` objeto invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF firmado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto devuelto por el `CreatePDF2` método (el parámetro de salida). Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el `System.IO.BinaryWriter` método `Write` del objeto y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
