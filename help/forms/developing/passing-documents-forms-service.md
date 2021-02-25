---
title: Pasar Documentos a FormsService
seo-title: Pasar Documentos a FormsService
description: 'Pase un objeto com.adobe.idp.Documento que contenga el diseño de formulario al servicio Forms. El servicio Forms procesa el diseño de formulario ubicado en el objeto com.adobe.idp.Documento. '
seo-description: Pase un objeto com.adobe.idp.Documento que contenga el diseño de formulario al servicio Forms. El servicio Forms procesa el diseño de formulario ubicado en el objeto com.adobe.idp.Documento.
uuid: 841e97f3-ebb8-4340-81a9-b6db11f0ec82
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e23de3c3-f8a0-459f-801e-a0942fb1c6aa
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '1714'
ht-degree: 0%

---


# Pasar Documentos al servicio de Forms {#passing-documents-to-the-formsservice}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en el entorno JEE.**

El servicio AEM Forms procesa PDF forms interactivos en los dispositivos cliente, generalmente en los exploradores Web, para recopilar información de los usuarios. Un formulario PDF interactivo se basa en un diseño de formulario que normalmente se guarda como archivo XDP y se crea en Designer. Desde AEM Forms, puede pasar un objeto `com.adobe.idp.Document` que contenga el diseño de formulario al servicio Forms. A continuación, el servicio Forms procesa el diseño de formulario ubicado en el objeto `com.adobe.idp.Document`.

Una ventaja de pasar un objeto `com.adobe.idp.Document` al servicio de Forms es que otras operaciones de servicio devuelven una instancia `com.adobe.idp.Document`. Es decir, puede obtener una instancia `com.adobe.idp.Document` de otra operación de servicio y procesarla. Por ejemplo, supongamos que un archivo XDP se almacena en un nodo de Content Services (desaprobado) denominado `/Company Home/Form Designs`, como se muestra en la siguiente ilustración.

Puede recuperar mediante programación Loan.xdp de Content Services (desaprobado) (desaprobado) y pasar el archivo XDP al servicio de Forms dentro de un objeto `com.adobe.idp.Document`.

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para pasar un documento obtenido de Content Services (desaprobado) al servicio de Forms, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de Forms y una API de cliente de administración de Documento.
1. Recupere el diseño de formulario de Content Services (desaprobado).
1. Representar el formulario PDF interactivo.
1. Realice una acción con el flujo de datos del formulario.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, incluya los archivos proxy.

**Creación de un objeto de API de cliente de administración de Documentos y Forms**

Antes de realizar una operación de API de servicio de Forms mediante programación, cree un objeto de API de cliente de Forms. Además, como este flujo de trabajo recupera un archivo XDP de Content Services (desaprobado), cree un objeto API de administración de Documento.

**Recuperar el diseño de formulario de Content Services (obsoleto)**

Recupere el archivo XDP de Content Services (desaprobado) mediante Java o la API de servicio Web. El archivo XDP se devuelve dentro de una instancia `com.adobe.idp.Document` (o una instancia `BLOB` si utiliza servicios Web). A continuación, puede pasar la instancia `com.adobe.idp.Document` al servicio de Forms.

**Representar un formulario PDF interactivo**

Para procesar un formulario interactivo, pase la instancia `com.adobe.idp.Document` devuelta por Content Services (desaprobada) al servicio de Forms.

>[!NOTE]
>
>Puede pasar un `com.adobe.idp.Document` que contenga el diseño de formulario al servicio de Forms. Dos nuevos métodos llamados `renderPDFForm2` y `renderHTMLForm2` aceptan un objeto `com.adobe.idp.Document` que contiene un diseño de formulario.

**Realizar una acción con el flujo de datos del formulario**

Según el tipo de aplicación cliente, puede escribir el formulario en un navegador web cliente o guardarlo como archivo PDF. Una aplicación basada en Web suele escribir el formulario en un explorador Web. Sin embargo, una aplicación de escritorio generalmente guarda el formulario como archivo PDF.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API de servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Pasar documentos al servicio de Forms mediante la API de Java {#pass-documents-to-the-forms-service-using-the-java-api}

Transmitir un documento obtenido de Content Services (desaprobado) mediante la API (Java) del servicio y los servicios de contenido de Forms (desaprobada):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar y adobe-contentservices-client.jar, en la ruta de clases del proyecto Java.

1. Creación de un objeto de API de cliente de administración de Documentos y Forms

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión. (Consulte [Configuración de propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Cree un objeto `FormsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.
   * Cree un objeto `DocumentManagementServiceClientImpl` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Recuperar el diseño de formulario de Content Services (obsoleto)

   Invoque el método `DocumentManagementServiceClientImpl` del objeto `retrieveContent` y pase los siguientes valores:

   * Un valor de cadena que especifica el almacén donde se agrega el contenido. El almacén predeterminado es `SpacesStore`. Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la ruta completa del contenido que se va a recuperar (por ejemplo, `/Company Home/Form Designs/Loan.xdp`). Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la versión. Este valor es un parámetro opcional y puede pasar una cadena vacía. En este caso, se recupera la versión más reciente.

   El método `retrieveContent` devuelve un objeto `CRCResult` que contiene el archivo XDP. Obtenga una instancia `com.adobe.idp.Document` invocando el método `CRCResult` del objeto `getDocument`.

1. Representar un formulario PDF interactivo

   Invoque el método `FormsServiceClient` del objeto `renderPDFForm2` y pase los siguientes valores:

   * Objeto `com.adobe.idp.Document` que contiene el diseño de formulario recuperado de Content Services (desaprobado).
   * Un objeto `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un objeto vacío `com.adobe.idp.Document`.
   * Un objeto `PDFFormRenderSpec` que almacena opciones de tiempo de ejecución. Este valor es un parámetro opcional y puede especificar `null` si no desea especificar opciones de tiempo de ejecución.
   * Un objeto `URLSpec` que contiene valores de URI. Este valor es un parámetro opcional y puede especificar `null`.
   * Objeto `java.util.HashMap` que almacena archivos adjuntos. Este valor es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El método `renderPDFForm` devuelve un objeto `FormsResult` que contiene una secuencia de datos de formulario que debe escribirse en el explorador Web del cliente.

1. Realizar una acción con el flujo de datos del formulario

   * Cree un objeto `com.adobe.idp.Document` invocando el método `FormsResult` del objeto ‘s `getOutputContent`.
   * Obtenga el tipo de contenido del objeto `com.adobe.idp.Document` invocando su método `getContentType`.
   * Configure el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `com.adobe.idp.Document`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el método `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream`.
   * Cree un objeto `java.io.InputStream` invocando el método `com.adobe.idp.Document` del objeto `getInputStream`.
   * Cree una matriz de bytes y rellénela con la secuencia de datos del formulario invocando el método `InputStream` del objeto `read`. Pase la matriz de bytes como un argumento.
   * Invoque el método `javax.servlet.ServletOutputStream` del objeto `write` para enviar la secuencia de datos del formulario al explorador Web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Inicio rápido (modo SOAP): Pasar documentos al servicio Forms mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Transmitir documentos al servicio Forms mediante la API de servicio Web {#pass-documents-to-the-forms-service-using-the-web-service-api}

Transmitir un documento obtenido de Content Services (desaprobado) mediante la API (servicio web) de Forms Service and Content Services (desaprobada):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Dado que esta aplicación cliente invoca dos servicios de AEM Forms, cree dos referencias de servicio. Utilice la siguiente definición WSDL para la referencia de servicio asociada al servicio Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Utilice la siguiente definición WSDL para la referencia de servicio asociada al servicio de gestión de Documentos: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Debido a que el tipo de datos `BLOB` es común a ambas referencias de servicio, califique completamente el tipo de datos `BLOB` al utilizarlo. En el inicio rápido correspondiente del servicio Web, todas las instancias `BLOB` están completamente calificadas.

   >[!NOTE]
   >
   >Reemplace `localhost`con la dirección IP del servidor que aloja AEM Forms.

1. Creación de un objeto de API de cliente de administración de Documentos y Forms

   * Cree un objeto `FormsServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `FormsServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/FormsService?WSDL`). No es necesario usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `FormsServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `FormsServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Repita estos pasos para el cliente de servicio `DocumentManagementServiceClient`.

1. Recuperar el diseño de formulario de Content Services (obsoleto)

   Recupere contenido invocando el método `DocumentManagementServiceClient` del objeto `retrieveContent` y pasando los siguientes valores:

   * Un valor de cadena que especifica el almacén donde se agrega el contenido. El almacén predeterminado es `SpacesStore`. Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la ruta completa del contenido que se va a recuperar (por ejemplo, `/Company Home/Form Designs/Loan.xdp`). Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la versión. Este valor es un parámetro opcional y puede pasar una cadena vacía. En este caso, se recupera la versión más reciente.
   * Parámetro de salida de cadena que almacena el valor del vínculo de exploración.
   * Parámetro de salida `BLOB` que almacena el contenido. Puede utilizar este parámetro de salida para recuperar el contenido.
   * Parámetro de salida `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` que almacena atributos de contenido.
   * Un parámetro de salida `CRCResult`. En lugar de utilizar este objeto, puede utilizar el parámetro de salida `BLOB` para obtener el contenido.

1. Representar un formulario PDF interactivo

   Invoque el método `FormsServiceClient` del objeto `renderPDFForm2` y pase los siguientes valores:

   * Objeto `BLOB` que contiene el diseño de formulario recuperado de Content Services (desaprobado).
   * Un objeto `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un objeto vacío `BLOB`.
   * Un objeto `PDFFormRenderSpec` que almacena opciones de tiempo de ejecución. Este valor es un parámetro opcional y puede especificar `null` si no desea especificar opciones de tiempo de ejecución.
   * Un objeto `URLSpec` que contiene valores de URI. Este valor es un parámetro opcional y puede especificar `null`.
   * Objeto `Map` que almacena archivos adjuntos. Este valor es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Parámetro de salida largo que se utiliza para almacenar el recuento de páginas.
   * Parámetro de salida de cadena que se utiliza para almacenar el valor de configuración regional.
   * Parámetro de salida `FormsResult` que se utiliza para almacenar el formulario PDF interactivo `.`

   El método `renderPDFForm2` devuelve un objeto `FormsResult` que contiene el formulario PDF interactivo.

1. Realizar una acción con el flujo de datos del formulario

   * Cree un objeto `BLOB` que contenga datos de formulario obteniendo el valor del campo `FormsResult` del objeto `outputContent`.
   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF interactivo y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` recuperado del objeto `FormsResult`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
