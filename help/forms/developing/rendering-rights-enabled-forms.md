---
title: Procesar formularios con derechos activados
seo-title: Rendering Rights-Enabled Forms
description: Utilice el servicio Forms para procesar formularios a los que se les han aplicado derechos de uso. Puede procesar formularios con derechos activados mediante la API de Java y la API de servicio web.
seo-description: Use the Forms service to render forms that have usage rights applied to them. You can render rights-enabled forms using the Java API and Web Service API.
uuid: ce5e4be6-d9b0-4989-a0e1-a8c3b98aed77
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d4c2b2f0-613a-409d-b39b-8e37fdb96eea
role: Developer
exl-id: 012a3a9f-542c-4ed1-a092-572bfccbdf21
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1463'
ht-degree: 4%

---

# Procesar formularios con derechos activados {#rendering-rights-enabled-forms}

El servicio Forms puede procesar formularios a los que se les han aplicado derechos de uso. Los derechos de uso pertenecen a una funcionalidad que está disponible de forma predeterminada en Acrobat pero no en Adobe Reader, como la capacidad de agregar comentarios a un formulario o rellenar los campos del formulario y guardarlo. Las Forms a las que se les han aplicado derechos de uso se denominan formularios con derechos activados. Un usuario que abre un formulario con derechos activados en Adobe Reader puede realizar las operaciones que están habilitadas para ese formulario.

Para aplicar derechos de uso a un formulario, el servicio de extensiones de Acrobat Reader DC AEM debe formar parte de la instalación de los formularios de. Además, debe tener una credencial válida que le permita aplicar derechos de uso a documentos de PDF. Es decir, debe configurar correctamente el servicio de extensiones de Acrobat Reader DC para poder procesar un formulario con los derechos activados. (Consulte [Acerca del servicio Acrobat Reader DC extensions](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service).)

>[!NOTE]
>
>Para procesar un formulario que contenga derechos de uso, debe utilizar un archivo XDP como entrada, no un archivo de PDF. Si utiliza un archivo de PDF como entrada, el formulario se seguirá representando; sin embargo, no será un formulario con derechos habilitados.

>[!NOTE]
>
>No se puede rellenar previamente un formulario con datos XML cuando se especifican los siguientes derechos de uso: `enableComments`, `enableCommentsOnline`, `enableEmbeddedFiles`, o `enableDigitalSignatures`. (Consulte [Rellenado previo de Forms con diseños flexibles](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para procesar un formulario con derechos activados, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Establecer opciones de tiempo de ejecución de derechos de uso.
1. Procesar un formulario con los derechos activados.
1. Escriba el formulario con los derechos activados en el explorador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API de cliente de Forms**

Para poder realizar mediante programación una operación de API de cliente de servicio de Forms, debe crear un cliente de servicio de Forms.

**Establecer opciones de tiempo de ejecución de derechos de uso**

Debe establecer opciones de tiempo de ejecución de derechos de uso para procesar un formulario con derechos habilitados. También debe especificar el alias de la credencial que se utiliza para aplicar derechos de uso a un formulario. Después de especificar el valor del alias, debe especificar cada derecho de uso que se aplicará al formulario.

**Procesar un formulario con derechos activados**

Para procesar un formulario con derechos activados, se utiliza la misma lógica de aplicación que para procesar un formulario sin derechos de uso. La única diferencia es que debe asegurarse de que las opciones de derechos de uso en tiempo de ejecución estén incluidas en la lógica de la aplicación.

>[!NOTE]
>
>Al procesar un formulario con derechos activados mediante la API del servicio web de Forms, no se pueden adjuntar archivos al formulario.

**Escribir el flujo de datos del formulario en el explorador web del cliente**

Cuando el servicio Forms procesa un formulario con derechos habilitados, devuelve un flujo de datos de formulario que debe escribir en el explorador web del cliente. Una vez escrito en el explorador web del cliente, el formulario es visible para el usuario. Un usuario que visualiza el formulario con derechos activados en Adobe Reader puede realizar las operaciones que están habilitadas para ese formulario.

**Consulte también**

[Procesar formularios con derechos activados mediante la API de Java](#render-rights-enabled-forms-using-the-java-api)

[Procesar formularios con derechos activados mediante la API de servicio web](#render-rights-enabled-forms-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Procesar formularios PDF interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Crear aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Procesar formularios con derechos activados mediante la API de Java {#render-rights-enabled-forms-using-the-java-api}

Procesar un formulario con derechos activados mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clase del proyecto Java.

1. Crear un objeto de API de cliente de Forms

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `FormsServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Establecer opciones de tiempo de ejecución de derechos de uso

   * Crear un `ReaderExtensionSpec` mediante su constructor.
   * Especifique el alias de la credencial invocando el `ReaderExtensionSpec` del objeto `setReCredentialAlias` y especifique un valor de cadena que represente el valor del alias.
   * Establezca cada derecho de uso invocando el método correspondiente que pertenece a `ReaderExtensionSpec` objeto. Sin embargo, solo puede establecer un derecho de uso si la credencial a la que hace referencia le permite hacerlo. Es decir, no puede establecer un derecho de uso si la credencial no le permite establecerlo. Por ejemplo. para establecer el derecho de uso que permite a un usuario rellenar los campos del formulario y guardarlo, invoque el `ReaderExtensionSpec` del objeto `setReFillIn` método y pase `true`.

   >[!NOTE]
   >
   >No es necesario invocar el `ReaderExtensionSpec` del objeto `setReCredentialPassword` método. El servicio Forms no utiliza este método.

1. Procesar un formulario con derechos activados

   Invoque el `FormsServiceClient` del objeto `renderPDFFormWithUsageRights` y pasar los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta de acceso completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un vacío `com.adobe.idp.Document` objeto.
   * A `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución.
   * A `ReaderExtensionSpec` que almacena las opciones de tiempo de ejecución de los derechos de uso.
   * A `URLSpec` que contiene valores de URI requeridos por el servicio de Forms.

   El `renderPDFFormWithUsageRights` El método devuelve un valor `FormsResult` que contiene un flujo de datos de formulario que debe escribirse en el explorador web cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Crear un `com.adobe.idp.Document` invocando el objeto de `FormsResult` objeto ‘s `getOutputContent` método.
   * Obtenga el tipo de contenido del `com.adobe.idp.Document` invocando su objeto `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasando el tipo de contenido del `com.adobe.idp.Document` objeto.
   * Crear un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos de formulario en el explorador web del cliente invocando el `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Crear un `java.io.InputStream` invocando el objeto de `com.adobe.idp.Document` del objeto `getInputStream` método.
   * Cree una matriz de bytes y rellénela con el flujo de datos de formulario invocando el método `InputStream` del objeto `read` y pasando la matriz de bytes como argumento.
   * Invoque el `javax.servlet.ServletOutputStream` del objeto `write` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes a `write` método.

**Consulte también**

[Inicio rápido (modo SOAP): Procesamiento de un formulario con derechos activados mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Procesar formularios con derechos activados mediante la API de servicio web {#render-rights-enabled-forms-using-the-web-service-api}

Procesar un formulario con derechos activados mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases de proxy Java en la ruta de clase.

1. Crear un objeto de API de cliente de Forms

   Crear un `FormsService` y establezca los valores de autenticación.

1. Establecer opciones de tiempo de ejecución de derechos de uso

   * Crear un `ReaderExtensionSpec` mediante su constructor.
   * Especifique el alias de la credencial invocando el `ReaderExtensionSpec` del objeto `setReCredentialAlias` y especifique un valor de cadena que represente el valor del alias.
   * Establezca cada derecho de uso invocando el método correspondiente que pertenece a `ReaderExtensionSpec` objeto. Sin embargo, solo puede establecer un derecho de uso si la credencial a la que hace referencia le permite hacerlo. Es decir, no puede establecer un derecho de uso si la credencial no le permite establecerlo. Para establecer el derecho de uso que permite a un usuario rellenar los campos del formulario y guardarlo, invoque el `ReaderExtensionSpec` del objeto `setReFillIn` método y pase `true`.

1. Procesar un formulario con derechos activados

   Invoque el `FormsService` del objeto `renderPDFFormWithUsageRights` y pasar los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta de acceso completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar datos con el formulario, debe pasar un `BLOB` que se basa en una fuente de datos XML vacía. No puede pasar un `BLOB` objeto que es nulo; de lo contrario, se produce una excepción.
   * A `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución.
   * A `ReaderExtensionSpec` que almacena las opciones de tiempo de ejecución de los derechos de uso.
   * A `URLSpec` que contiene valores de URI requeridos por el servicio de Forms.

   El `renderPDFFormWithUsageRights` El método devuelve un valor `FormsResult` que contiene un flujo de datos de formulario que debe escribirse en el explorador web cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Crear un `BLOB` que contiene datos de formulario invocando el `FormsResult` del objeto `getOutputContent` método.
   * Obtenga el tipo de contenido del `BLOB` invocando su objeto `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasando el tipo de contenido del `BLOB` objeto.
   * Crear un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos de formulario en el explorador web del cliente invocando el `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Cree una matriz de bytes y rellénela invocando el método `BLOB` del objeto `getBinaryData` método. Esta tarea asigna el contenido del `FormsResult` a la matriz de bytes.
   * Invoque el `javax.servlet.http.HttpServletResponse` del objeto `write` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes a `write` método.

**Consulte también**

[Procesar formularios con derechos activados](#rendering-rights-enabled-forms)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
