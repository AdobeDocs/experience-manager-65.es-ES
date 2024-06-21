---
title: Convertir documentos Postscript a PDF
description: Utilice el servicio Distiller para convertir archivos PostScript®, PostScript encapsulado (EPS) y PRN en archivos de PDF compactos, fiables y más seguros a través de una red. El servicio Distiller convierte grandes volúmenes de documentos impresos en documentos electrónicos, como facturas e instrucciones, mediante la API de Java y la API de servicio web.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 744df8b2-0c61-410f-89e9-20b8adddbf45
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 2%

---

# Convertir documentos Postscript a PDF {#converting-postscript-to-pdf-documents}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

## Acerca del servicio Distiller {#about-the-distiller-service}

El servicio Distiller® convierte los archivos PostScript®, PostScript encapsulado (EPS) y PRN en archivos de PDF compactos, fiables y más seguros a través de una red. El servicio Distiller se utiliza con frecuencia para convertir grandes volúmenes de documentos impresos en documentos electrónicos, como facturas e instrucciones. La conversión de documentos a PDF también permite a las empresas enviar a sus clientes una versión en papel y otra electrónica de un documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio Distiller, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversión de documentos PostScript a PDF {#converting-postscript-to-pdf-documents-inner}

En este tema se describe cómo puede utilizar la API del servicio Distiller (Java y servicio web) para convertir mediante programación archivos PostScript (PS), PostScript encapsulado (EPS) y PRN en documentos de PDF.

>[!NOTE]
>
>Para obtener más información sobre el servicio Distiller, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para convertir archivos PostScript en documentos de PDF, es necesario instalar uno de los siguientes en el servidor que aloja AEM Forms: Acrobat 9 o paquete redistribuible de Microsoft Visual C++ 2005.

### Resumen de los pasos {#summary-of-steps}

Para convertir cualquiera de los tipos admitidos en un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de Distiller.
1. Recupere el archivo que desea convertir.
1. Invoque la operación de creación del PDF.
1. Guarde el documento del PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente de servicio de Distiller**

Para poder realizar mediante programación una operación de servicio de Distiller, debe crear un cliente de servicio de Distiller. Si utiliza la API de Java, cree un `DistillerServiceClient` objeto. Si utiliza la API del servicio web, cree un `DistillerServiceService` objeto.

**Recupere el archivo que desea convertir**

Recupere el archivo que desea convertir. Por ejemplo, para convertir un archivo PS en un documento de PDF, debe recuperar el archivo PS.

**Invocar la operación de creación del PDF**

Después de crear el cliente de servicios, puede invocar la operación de creación del PDF. Esta operación necesita información sobre el documento que se va a convertir, incluida la ruta al documento de destino.

**Guardar el documento del PDF**

Puede guardar el documento de PDF como un archivo de PDF.

**Consulte también**

[Conversión de un archivo PostScript a PDF mediante la API de Java](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[Conversión de un archivo PostScript a PDF mediante la API de servicio web](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de API del servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Conversión de un archivo PostScript a PDF mediante la API de Java {#convert-a-postscript-file-to-pdf-using-the-java-api}

Conversión de un archivo PostScript en un documento de PDF mediante la API de servicio de Distiller (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-distiller-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de servicio de Distiller.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `DistillerServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Recupere el archivo que desea convertir.

   * Crear un `java.io.FileInputStream` que representa el archivo que se va a convertir utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Invoque la operación de creación del PDF.

   Invoque el `DistillerServiceClient` del objeto `createPDF` y pasar los siguientes valores:

   * El `com.adobe.idp.Document` que representa el archivo PS, EPS o PRN que se va a convertir
   * A `java.lang.String` que contiene el nombre del archivo que se va a convertir
   * A `java.lang.String` que contiene el nombre de la configuración de Adobe PDF que se va a utilizar
   * A `java.lang.String` objeto que contiene el nombre de la configuración de seguridad que se va a utilizar
   * Un opcional `com.adobe.idp.Document` objeto que contiene la configuración que se aplicará durante la generación del documento de PDF
   * Un opcional `com.adobe.idp.Document` que contiene información de metadatos que se aplicará al documento del PDF

   El `createPDF` El método devuelve un valor `CreatePDFResult` que contiene el nuevo documento de PDF y un archivo de registro que se puede generar. El archivo de registro suele contener mensajes de error o advertencia generados por la solicitud de conversión.

1. Guarde el documento del PDF.

   Para obtener el documento de PDF recién creado, realice las siguientes acciones:

   * Invoque el `CreatePDFResult` del objeto `getCreatedDocument` método. Esto devuelve un `com.adobe.idp.Document` objeto.
   * Invoque el `com.adobe.idp.Document` del objeto `copyToFile` para extraer el documento del PDF.

   Del mismo modo, para obtener el documento de registro, realice las siguientes acciones.

   * Invoque el `CreatePDFResult` del objeto `getLogDocument` método. Esto devuelve un `com.adobe.idp.Document` objeto.
   * Invoque el `com.adobe.idp.Document` del objeto `copyToFile` para extraer el documento de registro.

**Consulte también**

[Resumen de los pasos](converting-postscript-pdf-documents.md#summary-of-steps)

[SOAP Inicio rápido (modo de): Conversión de un archivo PostScript a un documento de PDF mediante la API de Java](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de un archivo PostScript a PDF mediante la API de servicio web {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

Conversión de un archivo PostScript en un documento de PDF mediante la API de servicio Distiller (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de servicio de Distiller.

   * Crear un `DistillerServiceClient` mediante su constructor predeterminado.
   * Crear un `DistillerServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/DistillerService?blob=mtom`.) No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para utilizar MTOM.
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `DistillerServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `DistillerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DistillerServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere el archivo que desea convertir.

   * Crear un `BLOB` mediante su constructor. Esta `BLOB` se utiliza para almacenar el archivo que se va a convertir en un documento de PDF.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo y el modo para abrir el archivo en.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.

1. Invoque la operación de creación del PDF.

   Invoque el `DistillerServiceService` del objeto `CreatePDF2` y pasar los siguientes valores obligatorios:

   * El `BLOB` que representa el archivo PS que se va a convertir
   * Cadena que contiene el nombre de ruta del archivo que se va a convertir
   * Objeto de cadena que contiene la configuración de Adobe PDF que se va a utilizar (por ejemplo, `Standard`)
   * Objeto de cadena que contiene la configuración de seguridad que se va a utilizar (por ejemplo, `No Securit`y)
   * Un opcional `BLOB` objeto que contiene la configuración que se aplicará durante la generación del documento de PDF
   * Un opcional `BLOB` que contiene información de metadatos que se aplicará al documento del PDF
   * A `BLOB` parámetro de salida utilizado para almacenar el documento de PDF
   * A `BLOB` parámetro de salida utilizado para almacenar el registro

1. Guarde el documento del PDF.

   * Crear un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento de PDF firmado y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto que ha devuelto el `CreatePDF2` (el parámetro de salida). Rellene la matriz de bytes obteniendo el valor de `BLOB` del objeto `MTOM` miembro de datos.
   * Crear un `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
