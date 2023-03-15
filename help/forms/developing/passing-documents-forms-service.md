---
title: Pasar documentos a FormsService
seo-title: Passing Documents to the FormsService
description: Pase un objeto com.adobe.idp.Document que contenga el diseño de formulario al servicio Forms. El servicio Forms procesa el diseño de formulario ubicado en el objeto com.adobe.idp.Document.
seo-description: Pass a com.adobe.idp.Document object that contains the form design to the Forms service. The Forms service renders the form design located in the com.adobe.idp.Document object.
uuid: 841e97f3-ebb8-4340-81a9-b6db11f0ec82
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e23de3c3-f8a0-459f-801e-a0942fb1c6aa
role: Developer
exl-id: 29c7ebda-407a-464b-a9db-054163f5b737
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1684'
ht-degree: 0%

---

# Pasar documentos al servicio de Forms {#passing-documents-to-the-formsservice}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

El servicio AEM Forms procesa PDF forms interactivos en dispositivos cliente, normalmente exploradores web, para recopilar información de los usuarios. Un formulario PDF interactivo se basa en un diseño de formulario que normalmente se guarda como archivo XDP y se crea en Designer. A partir de AEM Forms, puede pasar un `com.adobe.idp.Document` que contiene el diseño de formulario al servicio Forms. A continuación, el servicio Forms procesa el diseño de formulario ubicado en la variable `com.adobe.idp.Document` objeto.

Una ventaja de pasar un `com.adobe.idp.Document` objeto del servicio de Forms es que otras operaciones del servicio devuelven un `com.adobe.idp.Document` ejemplo. Es decir, puede obtener una `com.adobe.idp.Document` instancia de otra operación de servicio y procesarla. Por ejemplo, supongamos que un archivo XDP se almacena en un nodo de Content Services (obsoleto) denominado `/Company Home/Form Designs`, como se muestra en la siguiente ilustración.

Puede recuperar mediante programación Loan.xdp de Content Services (obsoleto) (obsoleto) y pasar el archivo XDP al servicio de Forms dentro de un `com.adobe.idp.Document` objeto.

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para pasar un documento obtenido de Content Services (obsoleto) (obsoleto) al servicio Forms, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms y de Administración de documentos.
1. Recupere el diseño de formulario de Content Services (obsoleto).
1. Procese el formulario interactivo del PDF.
1. Realice una acción con el flujo de datos del formulario.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

**Crear un objeto de API de cliente de Forms y Administración de documentos**

Para poder realizar mediante programación una operación de API de servicio de Forms, cree un objeto de API de cliente de Forms. Además, como este flujo de trabajo recupera un archivo XDP de los servicios de contenido (obsoleto), cree un objeto de API de administración de documentos.

**Recuperar el diseño de formulario de Content Services (obsoleto)**

Recupere el archivo XDP de los servicios de contenido (obsoleto) mediante Java o la API de servicio web. El archivo XDP se devuelve en un `com.adobe.idp.Document` instancia de (o un `BLOB` si utiliza servicios web). A continuación, puede pasar el `com.adobe.idp.Document` al servicio Forms.

**Procesar un formulario interactivo de PDF**

Para procesar un formulario interactivo, pase el `com.adobe.idp.Document` instancia devuelta por Content Services (obsoleta) al servicio Forms.

>[!NOTE]
>
>Puede pasar un `com.adobe.idp.Document` que contiene el diseño de formulario al servicio Forms. Dos nuevos métodos llamados `renderPDFForm2` y `renderHTMLForm2` aceptar un `com.adobe.idp.Document` que contiene un diseño de formulario.

**Realizar una acción con el flujo de datos del formulario**

Según el tipo de aplicación cliente, puede escribir el formulario en un explorador web de cliente o guardarlo como archivo de PDF. Una aplicación basada en web suele escribir el formulario en el explorador web. Sin embargo, una aplicación de escritorio suele guardar el formulario como un archivo de PDF.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Pasar documentos al servicio de Forms mediante la API de Java {#pass-documents-to-the-forms-service-using-the-java-api}

Pase un documento obtenido de Content Services (obsoleto) mediante el servicio Forms y la API de Content Services (obsoleto) (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar y adobe-contentservices-client.jar, en la ruta de clase del proyecto Java.

1. Crear un objeto de API de cliente de Forms y Administración de documentos

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión. (Consulte [Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Crear un `FormsServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.
   * Crear un `DocumentManagementServiceClientImpl` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Recuperar el diseño de formulario de Content Services (obsoleto)

   Invoque el `DocumentManagementServiceClientImpl` del objeto `retrieveContent` y pasar los siguientes valores:

   * Un valor de cadena que especifica el almacén donde se agrega el contenido. El almacén predeterminado es `SpacesStore`. Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la ruta completa del contenido que se va a recuperar (por ejemplo, `/Company Home/Form Designs/Loan.xdp`). Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la versión. Este valor es un parámetro opcional y puede pasar una cadena vacía. En este caso, se recupera la versión más reciente.

   El `retrieveContent` El método devuelve un valor `CRCResult` que contiene el archivo XDP. Obtenga una `com.adobe.idp.Document` invocando el método `CRCResult` del objeto `getDocument` método.

1. Procesar un formulario interactivo de PDF

   Invoque el `FormsServiceClient` del objeto `renderPDFForm2` y pasar los siguientes valores:

   * A `com.adobe.idp.Document` que contiene el diseño de formulario recuperado de Content Services (obsoleto).
   * A `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un vacío `com.adobe.idp.Document` objeto.
   * A `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución. Este valor es un parámetro opcional y puede especificar `null` si no desea especificar opciones en tiempo de ejecución.
   * A `URLSpec` que contiene valores de URI. Este valor es un parámetro opcional y puede especificar `null`.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este valor es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El `renderPDFForm` El método devuelve un valor `FormsResult` que contiene un flujo de datos de formulario que debe escribirse en el explorador web cliente.

1. Realizar una acción con el flujo de datos del formulario

   * Crear un `com.adobe.idp.Document` invocando el objeto de `FormsResult` objeto ‘s `getOutputContent` método.
   * Obtenga el tipo de contenido del `com.adobe.idp.Document` invocando su objeto `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasando el tipo de contenido del `com.adobe.idp.Document` objeto.
   * Crear un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos de formulario en el explorador web del cliente invocando el `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Crear un `java.io.InputStream` invocando el objeto de `com.adobe.idp.Document` del objeto `getInputStream` método.
   * Cree una matriz de bytes y rellénela con el flujo de datos de formulario invocando el método `InputStream` del objeto `read` método. Pase la matriz de bytes como argumento.
   * Invoque el `javax.servlet.ServletOutputStream` del objeto `write` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes a `write` método.

**Consulte también**

[Inicio rápido (modo SOAP): Pasar documentos al servicio de Forms mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Pase documentos al servicio de Forms mediante la API de servicio web {#pass-documents-to-the-forms-service-using-the-web-service-api}

Pase un documento obtenido de Content Services (obsoleto) mediante el servicio Forms y la API de Content Services (obsoleto) (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Dado que esta aplicación cliente invoca dos servicios de AEM Forms, cree dos referencias de servicio. Utilice la siguiente definición de WSDL para la referencia de servicio asociada al servicio de Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Utilice la siguiente definición de WSDL para la referencia de servicio asociada al servicio de administración de documentos: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Debido a que el `BLOB` El tipo de datos es común a ambas referencias de servicio. Califique completamente el `BLOB` tipo de datos al utilizarlo. En el inicio rápido del servicio web correspondiente, todas las etiquetas `BLOB` Las instancias de están totalmente cualificadas.

   >[!NOTE]
   >
   >Reemplazar `localhost`con la dirección IP del servidor que aloja AEM Forms.

1. Crear un objeto de API de cliente de Forms y Administración de documentos

   * Crear un `FormsServiceClient` mediante su constructor predeterminado.
   * Crear un `FormsServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/FormsService?WSDL`). No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `FormsServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `FormsServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Repita estos pasos para el `DocumentManagementServiceClient`cliente de servicio.

1. Recuperar el diseño de formulario de Content Services (obsoleto)

   Recupere contenido invocando el `DocumentManagementServiceClient` del objeto `retrieveContent` y pasando los siguientes valores:

   * Un valor de cadena que especifica el almacén donde se agrega el contenido. El almacén predeterminado es `SpacesStore`. Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la ruta completa del contenido que se va a recuperar (por ejemplo, `/Company Home/Form Designs/Loan.xdp`). Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la versión. Este valor es un parámetro opcional y puede pasar una cadena vacía. En este caso, se recupera la versión más reciente.
   * Un parámetro de salida de cadena que almacena el valor del vínculo de exploración.
   * A `BLOB` parámetro de salida que almacena el contenido. Puede utilizar este parámetro de salida para recuperar el contenido.
   * A `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` parámetro de salida que almacena atributos de contenido.
   * A `CRCResult` parámetro de salida. En lugar de utilizar este objeto, puede utilizar la variable `BLOB` parámetro de salida para obtener el contenido.

1. Procesar un formulario interactivo de PDF

   Invoque el `FormsServiceClient` del objeto `renderPDFForm2` y pasar los siguientes valores:

   * A `BLOB` que contiene el diseño de formulario recuperado de Content Services (obsoleto).
   * A `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un vacío `BLOB` objeto.
   * A `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución. Este valor es un parámetro opcional y puede especificar `null` si no desea especificar opciones en tiempo de ejecución.
   * A `URLSpec` que contiene valores de URI. Este valor es un parámetro opcional y puede especificar `null`.
   * A `Map` que almacena archivos adjuntos. Este valor es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un parámetro de salida largo que se utiliza para almacenar el recuento de páginas.
   * Un parámetro de salida de cadena que se utiliza para almacenar el valor de configuración regional.
   * A `FormsResult` parámetro de salida que se utiliza para almacenar el formulario del PDF interactivo `.`

   El `renderPDFForm2` El método devuelve un valor `FormsResult` que contiene el formulario PDF interactivo.

1. Realizar una acción con el flujo de datos del formulario

   * Crear un `BLOB` que contiene datos de formulario al obtener el valor del objeto `FormsResult` del objeto `outputContent` field.
   * Crear un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento interactivo del PDF y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto recuperado del `FormsResult` objeto. Rellene la matriz de bytes obteniendo el valor de `BLOB` del objeto `MTOM` miembro de datos.
   * Crear un `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
