---
title: Renderización de Forms con derechos activados
seo-title: Renderización de Forms con derechos activados
description: Utilice el servicio Forms para procesar formularios que tengan derechos de uso aplicados a ellos. Puede procesar formularios habilitados para derechos mediante la API de Java y la API de servicio web.
seo-description: Utilice el servicio Forms para procesar formularios que tengan derechos de uso aplicados a ellos. Puede procesar formularios habilitados para derechos mediante la API de Java y la API de servicio web.
uuid: ce5e4be6-d9b0-4989-a0e1-a8c3b98aed77
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d4c2b2f0-613a-409d-b39b-8e37fdb96eea
role: Desarrollador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 0%

---


# Renderización de Forms con derechos activados {#rendering-rights-enabled-forms}

El servicio Forms puede procesar formularios que tengan derechos de uso aplicados a ellos. Los derechos de uso pertenecen a funciones que están disponibles de forma predeterminada en Acrobat pero no en Adobe Reader, como la capacidad de agregar comentarios a un formulario o de rellenar los campos del formulario y guardar el formulario. Los Forms que tienen derechos de uso aplicados se denominan formularios habilitados para derechos. Un usuario que abre un formulario con derechos activados en Adobe Reader puede realizar operaciones que estén habilitadas para ese formulario.

Para aplicar derechos de uso a un formulario, el servicio de extensiones de Acrobat Reader DC debe formar parte de la instalación de AEM forms. Además, debe tener una credencial válida que le permita aplicar derechos de uso a documentos PDF. Es decir, debe configurar correctamente el servicio de extensiones de Acrobat Reader DC para poder procesar un formulario con derechos activados. (Consulte [Acerca del servicio de extensiones de Acrobat Reader DC](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service)).

>[!NOTE]
>
>Para procesar un formulario que contenga derechos de uso, debe utilizar un archivo XDP como entrada, no como archivo PDF. Si utiliza un archivo PDF como entrada, el formulario se seguirá procesando; sin embargo, no será un formulario con derechos activados.

>[!NOTE]
>
>No se puede rellenar previamente un formulario con datos XML cuando se especifican los siguientes derechos de uso: `enableComments`, `enableCommentsOnline`, `enableEmbeddedFiles` o `enableDigitalSignatures`. (Consulte [Rellenado previo de Forms con diseños de posición variable](/help/forms/developing/prepopulating-forms-flowable-layouts.md)).

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para procesar un formulario con derechos activados, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Establezca las opciones de tiempo de ejecución de los derechos de uso.
1. Representar un formulario con derechos activados.
1. Escriba el formulario con los derechos activados en el explorador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de cliente de Forms**

Para poder realizar mediante programación una operación de API de cliente de servicio de Forms, debe crear un cliente de servicio de Forms.

**Definir opciones de tiempo de ejecución de derechos de uso**

Debe definir opciones de derechos de uso en tiempo de ejecución para procesar un formulario con derechos activados. También debe especificar el alias de la credencial que se utiliza para aplicar derechos de uso a un formulario. Después de especificar el valor de alias, debe especificar cada derecho de uso que se aplicará al formulario.

**Representar un formulario con derechos activados**

Para procesar un formulario con derechos activados, se utiliza la misma lógica de aplicación que para procesar un formulario sin derechos de uso. La única diferencia es que debe asegurarse de que las opciones de tiempo de ejecución de los derechos de uso se incluyen en la lógica de la aplicación.

>[!NOTE]
>
>Al procesar un formulario con derechos activados mediante la API de servicio web de Forms, no se pueden adjuntar archivos al formulario.

**Escribir el flujo de datos del formulario en el explorador web del cliente**

Cuando el servicio Forms procesa un formulario con derechos activados, devuelve un flujo de datos de formulario que debe escribirse en el explorador web del cliente. Una vez escrito en el explorador web del cliente, el formulario es visible para el usuario. Un usuario que vea el formulario con derechos activados en Adobe Reader puede realizar operaciones que estén habilitadas para ese formulario.

**Consulte también**

[Representar formularios habilitados para derechos mediante la API de Java](#render-rights-enabled-forms-using-the-java-api)

[Representar formularios habilitados para derechos mediante la API de servicio web](#render-rights-enabled-forms-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderización de PDF forms interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Creación de aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Representar formularios habilitados para derechos mediante la API de Java {#render-rights-enabled-forms-using-the-java-api}

Representar un formulario habilitado para derechos mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-forms-client.jar, en la ruta de clase de su proyecto Java.

1. Creación de un objeto de API de cliente de Forms

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `FormsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Definir opciones de tiempo de ejecución de derechos de uso

   * Cree un objeto `ReaderExtensionSpec` utilizando su constructor.
   * Especifique el alias de la credencial invocando el método `ReaderExtensionSpec` del objeto `setReCredentialAlias` y especifique un valor de cadena que represente el valor del alias.
   * Establezca cada derecho de uso invocando el método correspondiente que pertenece al objeto `ReaderExtensionSpec` . Sin embargo, solo puede establecer un derecho de uso si las credenciales a las que hace referencia le permiten hacerlo. Es decir, no puede establecer un derecho de uso si las credenciales no permiten establecerlo. Por ejemplo. para definir el derecho de uso que permite al usuario rellenar los campos del formulario y guardar el formulario, invoque el método `ReaderExtensionSpec` del objeto `setReFillIn` y pase `true`.

   >[!NOTE]
   >
   >No es necesario invocar el método `ReaderExtensionSpec` del objeto `setReCredentialPassword`. El servicio Forms no utiliza este método.

1. Representar un formulario con derechos activados

   Invoque el método `FormsServiceClient` del objeto `renderPDFFormWithUsageRights` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un objeto `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un objeto `com.adobe.idp.Document` vacío.
   * Un objeto `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución.
   * Un objeto `ReaderExtensionSpec` que almacena opciones en tiempo de ejecución de derechos de uso.
   * Un objeto `URLSpec` que contiene valores de URI necesarios para el servicio Forms.

   El método `renderPDFFormWithUsageRights` devuelve un objeto `FormsResult` que contiene un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un objeto `com.adobe.idp.Document` invocando el método `FormsResult` del objeto ‘s `getOutputContent`.
   * Obtenga el tipo de contenido del objeto `com.adobe.idp.Document` invocando su método `getContentType`.
   * Establezca el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `com.adobe.idp.Document`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se utilice para escribir el flujo de datos del formulario en el explorador web del cliente invocando el método `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream`.
   * Cree un objeto `java.io.InputStream` invocando el método `com.adobe.idp.Document` del objeto `getInputStream`.
   * Cree una matriz de bytes rellénela con la secuencia de datos del formulario invocando el método `InputStream` del objeto `read` y pasando la matriz de bytes como argumento.
   * Invoque el método `javax.servlet.ServletOutputStream` del objeto `write` para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Inicio rápido (modo SOAP): Representación de un formulario con derechos activados mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Representar formularios habilitados para derechos mediante la API de servicio web {#render-rights-enabled-forms-using-the-web-service-api}

Representar un formulario con derechos activados mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases proxy de Java en la ruta de clase.

1. Creación de un objeto de API de cliente de Forms

   Cree un objeto `FormsService` y establezca valores de autenticación.

1. Definir opciones de tiempo de ejecución de derechos de uso

   * Cree un objeto `ReaderExtensionSpec` utilizando su constructor.
   * Especifique el alias de la credencial invocando el método `ReaderExtensionSpec` del objeto `setReCredentialAlias` y especifique un valor de cadena que represente el valor del alias.
   * Establezca cada derecho de uso invocando el método correspondiente que pertenece al objeto `ReaderExtensionSpec` . Sin embargo, solo puede establecer un derecho de uso si las credenciales a las que hace referencia le permiten hacerlo. Es decir, no puede establecer un derecho de uso si las credenciales no permiten establecerlo. Para definir el derecho de uso que permite al usuario rellenar los campos del formulario y guardar el formulario, invoque el método `ReaderExtensionSpec` del objeto `setReFillIn` y pase `true`.

1. Representar un formulario con derechos activados

   Invoque el método `FormsService` del objeto `renderPDFFormWithUsageRights` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un objeto `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar datos con el formulario, debe pasar un objeto `BLOB` basado en un origen de datos XML vacío. No se puede pasar un objeto `BLOB` que sea nulo; de lo contrario, se genera una excepción.
   * Un objeto `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución.
   * Un objeto `ReaderExtensionSpec` que almacena opciones en tiempo de ejecución de derechos de uso.
   * Un objeto `URLSpec` que contiene valores de URI necesarios para el servicio Forms.

   El método `renderPDFFormWithUsageRights` devuelve un objeto `FormsResult` que contiene un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un objeto `BLOB` que contenga datos de formulario invocando el método `FormsResult` del objeto `getOutputContent`.
   * Obtenga el tipo de contenido del objeto `BLOB` invocando su método `getContentType`.
   * Establezca el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `BLOB`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se utilice para escribir el flujo de datos del formulario en el explorador web del cliente invocando el método `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream`.
   * Cree una matriz de bytes y rellénela invocando el método `BLOB` del objeto `getBinaryData`. Esta tarea asigna el contenido del objeto `FormsResult` a la matriz de bytes.
   * Invoque el método `javax.servlet.http.HttpServletResponse` del objeto `write` para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Renderización de Forms con derechos activados](#rendering-rights-enabled-forms)

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
