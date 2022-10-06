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

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

El servicio AEM Forms procesa PDF forms interactivos en dispositivos cliente, normalmente exploradores web, para recopilar información de los usuarios. Un formulario PDF interactivo se basa en un diseño de formulario que normalmente se guarda como archivo XDP y se crea en Designer. Desde AEM Forms, puede pasar un `com.adobe.idp.Document` objeto que contiene el diseño de formulario al servicio Forms. A continuación, el servicio Forms procesa el diseño de formulario ubicado en la variable `com.adobe.idp.Document` objeto.

Una ventaja de pasar un `com.adobe.idp.Document` El objeto al servicio Forms es que otras operaciones de servicio devuelven un `com.adobe.idp.Document` instancia. Es decir, puede obtener un `com.adobe.idp.Document` de otra operación de servicio y renderícela. Por ejemplo, supongamos que un archivo XDP se almacena en un nodo de Content Services (obsoleto) denominado `/Company Home/Form Designs`, como se muestra en la siguiente ilustración.

Puede recuperar mediante programación Loan.xdp de Content Services (desaprobada) (desaprobada) y pasar el archivo XDP al servicio Forms dentro de un `com.adobe.idp.Document` objeto.

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para pasar un documento obtenido de Content Services (desaprobada) (desaprobada) al servicio de Forms, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree una Forms y un objeto de API de cliente de Document Management.
1. Recupere el diseño de formulario de Content Services (obsoleto).
1. Procese el formulario de PDF interactivo.
1. Realice una acción con la secuencia de datos del formulario.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

**Creación de un objeto de API de cliente de Forms y Document Management**

Antes de realizar una operación de API de servicio de Forms mediante programación, cree un objeto de API de cliente de Forms. Además, como este flujo de trabajo recupera un archivo XDP de Content Services (obsoleto), cree un objeto de API de Document Management.

**Recuperar el diseño de formulario de Content Services (obsoleto)**

Recupere el archivo XDP de Content Services (obsoleto) mediante Java o la API de servicio web. El archivo XDP se devuelve dentro de un `com.adobe.idp.Document` instancia (o una `BLOB` instancia si utiliza servicios web). A continuación, puede pasar la variable `com.adobe.idp.Document` al servicio de Forms.

**Representar un formulario PDF interactivo**

Para procesar un formulario interactivo, pase el `com.adobe.idp.Document` instancia que se devolvió de Content Services (obsoleto) al servicio de Forms.

>[!NOTE]
>
>Puede pasar un `com.adobe.idp.Document` que contiene el diseño de formulario para el servicio de Forms. Dos métodos nuevos denominados `renderPDFForm2` y `renderHTMLForm2` aceptar `com.adobe.idp.Document` objeto que contiene un diseño de formulario.

**Realizar una acción con el flujo de datos del formulario**

Según el tipo de aplicación cliente, puede escribir el formulario en un explorador web cliente o guardarlo como archivo PDF. Una aplicación basada en Web suele escribir el formulario en un explorador Web. Sin embargo, una aplicación de escritorio generalmente guarda el formulario como un archivo PDF.

**Consulte también lo siguiente**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Pasar documentos al servicio de Forms mediante la API de Java {#pass-documents-to-the-forms-service-using-the-java-api}

Pase un documento obtenido de Content Services (desaprobada) mediante el servicio Forms y la API (desaprobada) de Content Services (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-forms-client.jar y adobe-contentservices-client.jar, en la ruta de clase de su proyecto Java.

1. Creación de un objeto de API de cliente de Forms y Document Management

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión. (Consulte [Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Cree un `FormsServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.
   * Cree un `DocumentManagementServiceClientImpl` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recuperar el diseño de formulario de Content Services (obsoleto)

   Invocar el `DocumentManagementServiceClientImpl` del objeto `retrieveContent` y pase los siguientes valores:

   * Un valor de cadena que especifica el almacén donde se agrega el contenido. El almacén predeterminado es `SpacesStore`. Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la ruta completa del contenido que se va a recuperar (por ejemplo, `/Company Home/Form Designs/Loan.xdp`). Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la versión. Este valor es un parámetro opcional y puede pasar una cadena vacía. En este caso, se recupera la versión más reciente.

   La variable `retrieveContent` el método devuelve un `CRCResult` que contiene el archivo XDP. Obtenga una `com.adobe.idp.Document` invocando la variable `CRCResult` del objeto `getDocument` método.

1. Representar un formulario PDF interactivo

   Invocar el `FormsServiceClient` del objeto `renderPDFForm2` y pase los siguientes valores:

   * A `com.adobe.idp.Document` objeto que contiene el diseño de formulario recuperado de Content Services (obsoleto).
   * A `com.adobe.idp.Document` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un vacío `com.adobe.idp.Document` objeto.
   * A `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución. Este valor es un parámetro opcional y puede especificar `null` si no desea especificar opciones de tiempo de ejecución.
   * A `URLSpec` que contiene valores de URI. Este valor es un parámetro opcional y puede especificar `null`.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este valor es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   La variable `renderPDFForm` el método devuelve un `FormsResult` objeto que contiene un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Realizar una acción con el flujo de datos del formulario

   * Cree un `com.adobe.idp.Document` invocando el objeto `FormsResult` objeto ‘s `getOutputContent` método.
   * Obtenga el tipo de contenido de la variable `com.adobe.idp.Document` invocando su `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasar el tipo de contenido de la variable `com.adobe.idp.Document` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos del formulario en el explorador web del cliente invocando la variable `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Cree un `java.io.InputStream` invocando el objeto `com.adobe.idp.Document` del objeto `getInputStream` método.
   * Cree una matriz de bytes y rellénela con la secuencia de datos del formulario invocando la variable `InputStream` del objeto `read` método. Pase la matriz de bytes como argumento.
   * Invocar el `javax.servlet.ServletOutputStream` del objeto `write` método para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes a la `write` método.

**Consulte también lo siguiente**

[Inicio rápido (modo SOAP): Pasar documentos al servicio de Forms mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Pasar documentos al servicio de Forms mediante la API de servicio web {#pass-documents-to-the-forms-service-using-the-web-service-api}

Pase un documento obtenido de Content Services (desaprobada) mediante el servicio Forms y la API de Content Services (desaprobada) (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Dado que esta aplicación cliente invoca dos servicios de AEM Forms, cree dos referencias de servicio. Utilice la siguiente definición WSDL para la referencia de servicio asociada al servicio Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Utilice la siguiente definición WSDL para la referencia de servicio asociada al servicio de gestión de documentos: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Porque la variable `BLOB` el tipo de datos es común a ambas referencias de servicio; califique completamente la variable `BLOB` tipo de datos al utilizarla. En el inicio rápido correspondiente del servicio web, todas las `BLOB` las instancias están completamente cualificadas.

   >[!NOTE]
   >
   >Reemplazar `localhost`con la dirección IP del servidor que hospeda AEM Forms.

1. Creación de un objeto de API de cliente de Forms y Document Management

   * Cree un `FormsServiceClient` usando su constructor predeterminado.
   * Cree un `FormsServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/FormsService?WSDL`). No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `FormsServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `FormsServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Repita estos pasos para el `DocumentManagementServiceClient`cliente de servicio.

1. Recuperar el diseño de formulario de Content Services (obsoleto)

   Recupere contenido invocando la variable `DocumentManagementServiceClient` del objeto `retrieveContent` y pasando los siguientes valores:

   * Un valor de cadena que especifica el almacén donde se agrega el contenido. El almacén predeterminado es `SpacesStore`. Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la ruta completa del contenido que se va a recuperar (por ejemplo, `/Company Home/Form Designs/Loan.xdp`). Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la versión. Este valor es un parámetro opcional y puede pasar una cadena vacía. En este caso, se recupera la versión más reciente.
   * Un parámetro de salida de cadena que almacena el valor del vínculo de navegación.
   * A `BLOB` parámetro de salida que almacena el contenido. Puede utilizar este parámetro de salida para recuperar el contenido.
   * A `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` parámetro de salida que almacena atributos de contenido.
   * A `CRCResult` parámetro de salida. En lugar de usar este objeto, puede usar la variable `BLOB` parámetro de salida para obtener el contenido.

1. Representar un formulario PDF interactivo

   Invocar el `FormsServiceClient` del objeto `renderPDFForm2` y pase los siguientes valores:

   * A `BLOB` objeto que contiene el diseño de formulario recuperado de Content Services (obsoleto).
   * A `BLOB` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un vacío `BLOB` objeto.
   * A `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución. Este valor es un parámetro opcional y puede especificar `null` si no desea especificar opciones de tiempo de ejecución.
   * A `URLSpec` que contiene valores de URI. Este valor es un parámetro opcional y puede especificar `null`.
   * A `Map` que almacena archivos adjuntos. Este valor es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un parámetro de salida largo que se utiliza para almacenar el recuento de páginas.
   * Un parámetro de salida de cadena que se utiliza para almacenar el valor de configuración regional.
   * A `FormsResult` parámetro de salida que se utiliza para almacenar el formulario de PDF interactivo `.`

   La variable `renderPDFForm2` el método devuelve un `FormsResult` objeto que contiene el formulario de PDF interactivo.

1. Realizar una acción con el flujo de datos del formulario

   * Cree un `BLOB` objeto que contiene datos de formulario obteniendo el valor de la variable `FormsResult` del objeto `outputContent` campo .
   * Cree un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento del PDF interactivo y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto recuperado del `FormsResult` objeto. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` miembro de datos.
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
