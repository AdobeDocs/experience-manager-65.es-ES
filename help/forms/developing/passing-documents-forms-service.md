---
title: Pasar documentos a FormsService
seo-title: Pasar documentos a FormsService
description: nulo
seo-description: nulo
uuid: 841e97f3-ebb8-4340-81a9-b6db11f0ec82
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e23de3c3-f8a0-459f-801e-a0942fb1c6aa
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Pasar documentos al servicio Forms {#passing-documents-to-the-formsservice}

El servicio AEM Forms procesa formularios PDF interactivos en dispositivos cliente, normalmente exploradores Web, para recopilar información de los usuarios. Un formulario PDF interactivo se basa en un diseño de formulario que normalmente se guarda como archivo XDP y se crea en Designer. Desde AEM Forms, puede pasar un `com.adobe.idp.Document` objeto que contenga el diseño de formulario al servicio Forms. A continuación, el servicio Forms procesa el diseño de formulario ubicado en el `com.adobe.idp.Document` objeto.

Una ventaja de pasar un `com.adobe.idp.Document` objeto al servicio Forms es que otras operaciones de servicio devuelven una `com.adobe.idp.Document` instancia. Es decir, puede obtener una `com.adobe.idp.Document` instancia de otra operación de servicio y procesarla. Por ejemplo, supongamos que un archivo XDP se almacena en un nodo de Content Services (desaprobado) denominado `/Company Home/Form Designs`, como se muestra en la siguiente ilustración.

Puede recuperar mediante programación Loan.xdp de Content Services (desaprobado) (desaprobado) y pasar el archivo XDP al servicio Forms dentro de un `com.adobe.idp.Document` objeto.

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para pasar un documento obtenido de Content Services (desaprobado) al servicio Forms, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de Forms y Document Management Client.
1. Recupere el diseño de formulario de Content Services (desaprobado).
1. Representar el formulario PDF interactivo.
1. Realice una acción con el flujo de datos del formulario.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, incluya los archivos proxy.

**Creación de un objeto de API de Forms y Document Management Client**

Antes de realizar una operación de API de servicio de Forms mediante programación, cree un objeto de API de cliente de Forms. Además, como este flujo de trabajo recupera un archivo XDP de Content Services (desaprobado), cree un objeto de API de Document Management.

**Recuperar el diseño de formulario de Content Services (obsoleto)**

Recupere el archivo XDP de Content Services (desaprobado) mediante Java o la API de servicio Web. El archivo XDP se devuelve dentro de una `com.adobe.idp.Document` instancia (o una `BLOB` instancia si utiliza servicios Web). A continuación, puede pasar la `com.adobe.idp.Document` instancia al servicio Forms.

**Representar un formulario PDF interactivo**

Para procesar un formulario interactivo, pase la `com.adobe.idp.Document` instancia devuelta por Content Services (desaprobada) al servicio Forms.

>[!NOTE]
>
>Puede pasar un `com.adobe.idp.Document` formulario que contenga el diseño de formulario al servicio Forms. Dos nuevos métodos con nombre `renderPDFForm2` y `renderHTMLForm2` aceptar un `com.adobe.idp.Document` objeto que contiene un diseño de formulario.

**Realizar una acción con el flujo de datos del formulario**

Según el tipo de aplicación cliente, puede escribir el formulario en un navegador web cliente o guardarlo como archivo PDF. Una aplicación basada en Web suele escribir el formulario en un explorador Web. Sin embargo, una aplicación de escritorio generalmente guarda el formulario como archivo PDF.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de formularios](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Transmisión de documentos al servicio de formularios mediante la API de Java {#pass-documents-to-the-forms-service-using-the-java-api}

Transmitir un documento obtenido de Content Services (desaprobado) mediante el servicio de formularios y la API de Content Services (desaprobada) (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar y adobe-contentservices-client.jar, en la ruta de clases del proyecto Java.

1. Creación de un objeto de API de Forms y Document Management Client

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión. (Consulte [Configuración de propiedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexión).
   * Cree un `FormsServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.
   * Cree un `DocumentManagementServiceClientImpl` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recuperar el diseño de formulario de Content Services (obsoleto)

   Invoque el `DocumentManagementServiceClientImpl` método del `retrieveContent` objeto y pase los valores siguientes:

   * Un valor de cadena que especifica el almacén donde se agrega el contenido. La tienda predeterminada es `SpacesStore`. Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la ruta completa del contenido que se va a recuperar (por ejemplo, `/Company Home/Form Designs/Loan.xdp`). Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la versión. Este valor es un parámetro opcional y puede pasar una cadena vacía. En este caso, se recupera la versión más reciente.
   El `retrieveContent` método devuelve un `CRCResult` objeto que contiene el archivo XDP. Obtenga una `com.adobe.idp.Document` instancia invocando el `CRCResult` método `getDocument` del objeto.

1. Representar un formulario PDF interactivo

   Invoque el `FormsServiceClient` método del `renderPDFForm2` objeto y pase los valores siguientes:

   * Un `com.adobe.idp.Document` objeto que contiene el diseño de formulario recuperado de Content Services (desaprobado).
   * Un `com.adobe.idp.Document` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un `com.adobe.idp.Document` objeto vacío.
   * Un `PDFFormRenderSpec` objeto que almacena opciones de tiempo de ejecución. Este valor es un parámetro opcional y puede especificar `null` si no desea especificar opciones de tiempo de ejecución.
   * Un `URLSpec` objeto que contiene valores de URI. Este valor es un parámetro opcional y se puede especificar `null`.
   * Un `java.util.HashMap` objeto que almacena archivos adjuntos. Este valor es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   El `renderPDFForm` método devuelve un `FormsResult` objeto que contiene una secuencia de datos de formulario que se debe escribir en el explorador Web del cliente.

1. Realizar una acción con el flujo de datos del formulario

   * Cree un `com.adobe.idp.Document` objeto invocando el `FormsResult` método ‘s `getOutputContent` .
   * Obtenga el tipo de contenido del `com.adobe.idp.Document` objeto invocando su `getContentType` método.
   * Defina el tipo de contenido del `javax.servlet.http.HttpServletResponse` objeto invocando su `setContentType` método y pasando el tipo de contenido del `com.adobe.idp.Document` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el `javax.servlet.http.HttpServletResponse` método `getOutputStream` del objeto.
   * Cree un `java.io.InputStream` objeto invocando el `com.adobe.idp.Document` método `getInputStream` del objeto.
   * Cree una matriz de bytes y rellénela con la secuencia de datos del formulario invocando el `InputStream` método del `read` objeto. Pase la matriz de bytes como un argumento.
   * Invoque el `javax.servlet.ServletOutputStream` método del `write` objeto para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al `write` método .

**Consulte también**

[Inicio rápido (modo SOAP): Paso de documentos al servicio de formularios mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Transmisión de documentos al servicio de formularios mediante la API de servicio Web {#pass-documents-to-the-forms-service-using-the-web-service-api}

Transmitir un documento obtenido de Content Services (desaprobado) mediante el servicio de formularios y la API de Content Services (desaprobada) (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Dado que esta aplicación cliente invoca dos servicios de AEM Forms, cree dos referencias de servicio. Utilice la siguiente definición WSDL para la referencia de servicio asociada al servicio Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Utilice la siguiente definición WSDL para la referencia de servicio asociada al servicio de Document Management: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Debido a que el tipo de datos es común a ambas referencias de servicio, califique completamente el tipo de datos `BLOB` `BLOB` cuando lo utilice. En el inicio rápido correspondiente del servicio Web, todas `BLOB` las instancias están completamente cualificadas.

   >[!NOTE]
   >
   >Reemplazar `localhost`por la dirección IP del servidor que aloja AEM Forms.

1. Creación de un objeto de API de Forms y Document Management Client

   * Cree un `FormsServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `FormsServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/FormsService?WSDL`). No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `FormsServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `FormsServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.
   >[!NOTE]
   >
   >Repita estos pasos para el cliente `DocumentManagementServiceClient`de servicio.

1. Recuperar el diseño de formulario de Content Services (obsoleto)

   Recupere contenido invocando el `DocumentManagementServiceClient` método `retrieveContent` del objeto y pasando los siguientes valores:

   * Un valor de cadena que especifica el almacén donde se agrega el contenido. La tienda predeterminada es `SpacesStore`. Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la ruta completa del contenido que se va a recuperar (por ejemplo, `/Company Home/Form Designs/Loan.xdp`). Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la versión. Este valor es un parámetro opcional y puede pasar una cadena vacía. En este caso, se recupera la versión más reciente.
   * Parámetro de salida de cadena que almacena el valor del vínculo de exploración.
   * Parámetro `BLOB` de salida que almacena el contenido. Puede utilizar este parámetro de salida para recuperar el contenido.
   * Parámetro `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` de salida que almacena atributos de contenido.
   * Parámetro `CRCResult` de salida. En lugar de utilizar este objeto, puede utilizar el parámetro `BLOB` output para obtener el contenido.

1. Representar un formulario PDF interactivo

   Invoque el `FormsServiceClient` método del `renderPDFForm2` objeto y pase los valores siguientes:

   * Un `BLOB` objeto que contiene el diseño de formulario recuperado de Content Services (desaprobado).
   * Un `BLOB` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un `BLOB` objeto vacío.
   * Un `PDFFormRenderSpec` objeto que almacena opciones de tiempo de ejecución. Este valor es un parámetro opcional y puede especificar `null` si no desea especificar opciones de tiempo de ejecución.
   * Un `URLSpec` objeto que contiene valores de URI. Este valor es un parámetro opcional y se puede especificar `null`.
   * Un `Map` objeto que almacena archivos adjuntos. Este valor es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Parámetro de salida largo que se utiliza para almacenar el recuento de páginas.
   * Parámetro de salida de cadena que se utiliza para almacenar el valor de configuración regional.
   * Parámetro `FormsResult` de salida que se utiliza para almacenar el formulario PDF interactivo `.`
   El `renderPDFForm2` método devuelve un `FormsResult` objeto que contiene el formulario PDF interactivo.

1. Realizar una acción con el flujo de datos del formulario

   * Cree un `BLOB` objeto que contenga datos de formulario obteniendo el valor del `FormsResult` campo del `outputContent` objeto.
   * Cree un `System.IO.FileStream` objeto invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF interactivo y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto recuperado del `FormsResult` objeto. Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el `System.IO.BinaryWriter` método `Write` del objeto y pasando la matriz de bytes.

**Consulte también**

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
