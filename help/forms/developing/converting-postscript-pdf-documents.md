---
title: Conversión de Postscript a documentos de PDF
seo-title: Converting Postscript to PDF Documents
description: Utilice el servicio Distiller para convertir archivos de PostScript®, PostScript encapsulado (EPS) y PRN a archivos de PDF compactos, fiables y más seguros a través de una red. El servicio Distiller convierte grandes volúmenes de documentos impresos en documentos electrónicos, como facturas y estados de cuentas utilizando la API de Java y la API de Web Service.
seo-description: Use the Distiller service to convert PostScript®, Encapsulated PostScript (EPS), and PRN files to compact, reliable, and more secure PDF files over a network. The Distiller service converts large volumes of print documents to electronic documents, such as invoices and statements using the Java API and Web Service API.
uuid: 2143f406-1fdd-4551-a738-1a8388f8d478
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 06ad343a-f74d-41f5-b3c8-b85bb723ceeb
role: Developer
exl-id: 744df8b2-0c61-410f-89e9-20b8adddbf45
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1325'
ht-degree: 0%

---

# Conversión de Postscript a documentos de PDF {#converting-postscript-to-pdf-documents}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

## Acerca del servicio Distiller {#about-the-distiller-service}

El servicio Distiller® convierte archivos de PostScript®, PostScript encapsulado (EPS) y PRN en archivos PDF compactos, confiables y más seguros a través de una red. El servicio Distiller se utiliza con frecuencia para convertir grandes volúmenes de documentos impresos en documentos electrónicos, como facturas y estados de cuentas. La conversión de documentos a PDF también permite a las empresas enviar a sus clientes una versión en papel y una versión electrónica de un documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio Distiller, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversión de PostScript en documentos de PDF {#converting-postscript-to-pdf-documents-inner}

En este tema se describe cómo puede utilizar la API de servicio de Distiller (Java y servicio web) para convertir mediante programación archivos PostScript (PS), PostScript encapsulado (EPS) y PRN a documentos de PDF.

>[!NOTE]
>
>Para obtener más información sobre el servicio Distiller, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para convertir archivos PostScript en documentos de PDF, se debe instalar una de las siguientes opciones en el servidor que aloje AEM Forms: Paquete redistribuible de Acrobat 9 o Microsoft Visual C++ 2005.

### Resumen de los pasos {#summary-of-steps}

Para convertir cualquiera de los tipos admitidos en un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de Distiller.
1. Recupere el archivo que desea convertir.
1. Invoque la operación de creación del PDF.
1. Guarde el documento del PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un cliente de servicio de Distiller**

Para poder realizar una operación de servicio de Distiller mediante programación, debe crear un cliente de servicio de Distiller. Si utiliza la API de Java, cree un `DistillerServiceClient` objeto. Si utiliza la API de servicio web, cree un `DistillerServiceService` objeto.

**Recupere el archivo que desea convertir**

Debe recuperar el archivo que desea convertir. Por ejemplo, para convertir un archivo PS en un documento PDF, debe recuperar el archivo PS.

**Invocar la operación de creación del PDF**

Después de crear el cliente de servicio, puede invocar la operación de creación del PDF. Esta operación necesitará información sobre el documento que se va a convertir, incluida la ruta al documento de destino.

**Guardar el documento del PDF**

Puede guardar el documento del PDF como un archivo del PDF.

**Consulte también lo siguiente**

[Convertir un archivo PostScript a PDF mediante la API de Java](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[Conversión de un archivo PostScript a PDF mediante la API de servicio web](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Convertir un archivo PostScript a PDF mediante la API de Java {#convert-a-postscript-file-to-pdf-using-the-java-api}

Convierta un archivo PostScript a un documento de PDF mediante la API de servicio de Distiller (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-distiller-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente de servicio de Distiller.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `DistillerServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recupere el archivo que desea convertir.

   * Cree un `java.io.FileInputStream` objeto que representa el archivo que se va a convertir utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Invoque la operación de creación del PDF.

   Invocar el `DistillerServiceClient` del objeto `createPDF` y pase los siguientes valores:

   * La variable `com.adobe.idp.Document` objeto que representa el archivo PS, EPS o PRN que se va a convertir
   * A `java.lang.String` objeto que contiene el nombre del archivo que se va a convertir
   * A `java.lang.String` objeto que contiene el nombre de la configuración de Adobe PDF que se va a utilizar
   * A `java.lang.String` objeto que contiene el nombre de la configuración de seguridad que se va a utilizar
   * Un `com.adobe.idp.Document` objeto que contiene la configuración que se aplicará al generar el documento PDF
   * Un `com.adobe.idp.Document` objeto que contiene información de metadatos que se aplicará al documento del PDF

   La variable `createPDF` el método devuelve un `CreatePDFResult` que contiene el nuevo documento de PDF y un archivo de registro que se pueden generar. El archivo de registro suele contener mensajes de error o de advertencia generados por la solicitud de conversión.

1. Guarde el documento del PDF.

   Para obtener el documento de PDF recién creado, realice las siguientes acciones:

   * Invocar el `CreatePDFResult` del objeto `getCreatedDocument` método. Esto devuelve un `com.adobe.idp.Document` objeto.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` método para extraer el documento PDF.

   Del mismo modo, para obtener el documento de registro, realice las siguientes acciones.

   * Invocar el `CreatePDFResult` del objeto `getLogDocument` método. Esto devuelve un `com.adobe.idp.Document` objeto.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` método para extraer el documento de registro.


**Consulte también lo siguiente**

[Resumen de los pasos](converting-postscript-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Conversión de un archivo PostScript en un documento PDF mediante la API de Java](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de un archivo PostScript a PDF mediante la API de servicio web {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

Convierta un archivo PostScript a un documento de PDF mediante la API de servicio de Distiller (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de servicio de Distiller.

   * Cree un `DistillerServiceClient` usando su constructor predeterminado.
   * Cree un `DistillerServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/DistillerService?blob=mtom`.) No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para usar MTOM.
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `DistillerServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `DistillerServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `DistillerServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere el archivo que desea convertir.

   * Cree un `BLOB` usando su constructor. Esta `BLOB` se utiliza para almacenar el archivo y convertirlo en un documento PDF.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo y el modo en el que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Invoque la operación de creación del PDF.

   Invocar el `DistillerServiceService` del objeto `CreatePDF2` y pase los siguientes valores obligatorios:

   * La variable `BLOB` objeto que representa el archivo PS a convertir
   * Una cadena que contiene el nombre de ruta del archivo que se va a convertir
   * Un objeto de cadena que contiene la configuración de Adobe PDF que se va a utilizar (por ejemplo, `Standard`)
   * Un objeto de cadena que contiene la configuración de seguridad que se va a utilizar (por ejemplo, `No Securit`y)
   * Un `BLOB` objeto que contiene la configuración que se aplicará al generar el documento PDF
   * Un `BLOB` objeto que contiene información de metadatos que se aplicará al documento del PDF
   * A `BLOB` parámetro de salida utilizado para almacenar el documento del PDF
   * A `BLOB` parámetro de salida utilizado para almacenar el registro

1. Guarde el documento del PDF.

   * Cree un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento del PDF firmado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto devuelto por el `CreatePDF2` (el parámetro de salida). Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` miembro de datos.
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Resumen de los pasos](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
