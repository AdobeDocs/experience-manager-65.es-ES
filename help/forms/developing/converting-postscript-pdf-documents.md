---
title: Conversión de Postscript a Documentos PDF
seo-title: Conversión de Postscript a Documentos PDF
description: Utilice el servicio Distiller para convertir archivos PostScript®, Encapsulated PostScript (EPS) y PRN en archivos PDF compactos, fiables y más seguros a través de una red. El servicio Distiller convierte grandes volúmenes de documentos impresos en documentos electrónicos, como facturas y estados de cuenta mediante la API de Java y la API de servicio Web.
seo-description: Utilice el servicio Distiller para convertir archivos PostScript®, Encapsulated PostScript (EPS) y PRN en archivos PDF compactos, fiables y más seguros a través de una red. El servicio Distiller convierte grandes volúmenes de documentos impresos en documentos electrónicos, como facturas y estados de cuenta mediante la API de Java y la API de servicio Web.
uuid: 2143f406-1fdd-4551-a738-1a8388f8d478
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 06ad343a-f74d-41f5-b3c8-b85bb723ceeb
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 0%

---


# Conversión de Postscript a Documentos PDF {#converting-postscript-to-pdf-documents}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en el entorno JEE.**

## Acerca del servicio de Distiller {#about-the-distiller-service}

El servicio Distiller® convierte archivos PostScript®, Encapsulated PostScript (EPS) y PRN en archivos PDF compactos, fiables y más seguros a través de una red. El servicio Distiller se utiliza con frecuencia para convertir grandes volúmenes de documentos impresos en documentos electrónicos, como facturas y estados de cuentas. La conversión de documentos a PDF también permite a las empresas enviar a sus clientes una versión en papel y una versión electrónica de un documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio Distiller, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversión de PostScript a documentos PDF {#converting-postscript-to-pdf-documents-inner}

En este tema se describe cómo puede utilizar la API de servicio de Distiller (Java y servicio web) para convertir en forma programada archivos PostScript (PS), PostScript encapsulado (EPS) y PRN en documentos PDF.

>[!NOTE]
>
>Para obtener más información sobre el servicio Distiller, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para convertir archivos PostScript a documentos PDF, debe instalarse una de las siguientes opciones en el servidor que aloja AEM Forms: Paquete redistribuible de Acrobat 9 o Microsoft Visual C++ 2005.

### Resumen de los pasos {#summary-of-steps}

Para convertir cualquiera de los tipos admitidos en un documento PDF, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de Distiller.
1. Recupere el archivo que desea convertir.
1. Invoque la operación de creación de PDF.
1. Guarde el documento PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Crear un cliente de servicio de Distiller**

Antes de realizar una operación de servicio de Distiller mediante programación, debe crear un cliente de servicio de Distiller. Si utiliza la API de Java, cree un objeto `DistillerServiceClient`. Si utiliza la API de servicio Web, cree un objeto `DistillerServiceService`.

**Recuperar el archivo para convertir**

Debe recuperar el archivo que desea convertir. Por ejemplo, para convertir un archivo PS a un documento PDF, debe recuperar el archivo PS.

**Invocar la operación de creación de PDF**

Después de crear el cliente de servicio, puede invocar la operación de creación de PDF. Esta operación necesitará información sobre el documento que se va a convertir, incluida la ruta al documento de destinatario.

**Guardar el documento PDF**

Puede guardar el documento PDF como un archivo PDF.

**Consulte también**

[Convertir un archivo PostScript a PDF mediante la API de Java](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[Conversión de un archivo PostScript a PDF mediante la API de servicio Web](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de API de servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Convertir un archivo PostScript a PDF mediante la API de Java {#convert-a-postscript-file-to-pdf-using-the-java-api}

Convertir un archivo PostScript a documento PDF mediante la API de servicio de Distiller (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-distiller-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de servicio de Distiller.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `DistillerServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Recupere el archivo que desea convertir.

   * Cree un objeto `java.io.FileInputStream` que represente el archivo que se va a convertir utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Invoque la operación de creación de PDF.

   Invoque el método `DistillerServiceClient` del objeto `createPDF` y pase los siguientes valores:

   * El objeto `com.adobe.idp.Document` que representa el archivo PS, EPS o PRN que se va a convertir
   * Un objeto `java.lang.String` que contiene el nombre del archivo que se va a convertir
   * Un objeto `java.lang.String` que contiene el nombre de la configuración de Adobe PDF que se va a utilizar
   * Un objeto `java.lang.String` que contiene el nombre de la configuración de seguridad que se va a utilizar
   * Un objeto `com.adobe.idp.Document` opcional que contiene la configuración que se aplicará al generar el documento PDF
   * Un objeto `com.adobe.idp.Document` opcional que contiene información de metadatos que se aplicará al documento PDF

   El método `createPDF` devuelve un objeto `CreatePDFResult` que contiene el nuevo documento PDF y un archivo de registro que se puede generar. El archivo de registro generalmente contiene mensajes de error o de advertencia generados por la solicitud de conversión.

1. Guarde el documento PDF.

   Para obtener el documento PDF recién creado, realice las siguientes acciones:

   * Invocar el método `CreatePDFResult` del objeto `getCreatedDocument`. Esto devuelve un objeto `com.adobe.idp.Document`.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para extraer el documento PDF.

   Del mismo modo, para obtener el documento de registro, realice las siguientes acciones.

   * Invocar el método `CreatePDFResult` del objeto `getLogDocument`. Esto devuelve un objeto `com.adobe.idp.Document`.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para extraer el documento de registro.


**Consulte también**

[Resumen de los pasos](converting-postscript-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Conversión de un archivo PostScript a un documento PDF mediante la API de Java](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de un archivo PostScript a PDF mediante la API de servicio Web {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

Convertir un archivo PostScript a documento PDF mediante la API de servicio de Distiller (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de servicio de Distiller.

   * Cree un objeto `DistillerServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `DistillerServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/DistillerService?blob=mtom`). No es necesario usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para utilizar MTOM.
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `DistillerServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `DistillerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DistillerServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere el archivo que desea convertir.

   * Cree un objeto `BLOB` utilizando su constructor. Este objeto `BLOB` se utiliza para almacenar el archivo y convertirlo en un documento PDF.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo y el modo en el que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Invoque la operación de creación de PDF.

   Invoque el método `DistillerServiceService` del objeto `CreatePDF2` y pase los siguientes valores obligatorios:

   * El objeto `BLOB` que representa el archivo PS que se va a convertir
   * Una cadena que contiene el nombre de ruta del archivo que se va a convertir
   * Un objeto de cadena que contiene la configuración de Adobe PDF que se va a utilizar (por ejemplo, `Standard`)
   * Un objeto de cadena que contiene la configuración de seguridad que se va a utilizar (por ejemplo, `No Securit`y)
   * Un objeto `BLOB` opcional que contiene la configuración que se aplicará al generar el documento PDF
   * Un objeto `BLOB` opcional que contiene información de metadatos que se aplicará al documento PDF
   * Parámetro de salida `BLOB` utilizado para almacenar el documento PDF
   * Parámetro de salida `BLOB` utilizado para almacenar el registro

1. Guarde el documento PDF.

   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF firmado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` devuelto por el método `CreatePDF2` (el parámetro de salida). Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
