---
title: Formularios habilitados para derechos de representación
seo-title: Formularios habilitados para derechos de representación
description: nulo
seo-description: nulo
uuid: ce5e4be6-d9b0-4989-a0e1-a8c3b98aed77
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d4c2b2f0-613a-409d-b39b-8e37fdb96eea
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Formularios habilitados para derechos de representación {#rendering-rights-enabled-forms}

El servicio Forms puede procesar formularios que tengan derechos de uso aplicados. Los derechos de uso se refieren a funciones que están disponibles de forma predeterminada en Acrobat pero no en Adobe Reader, como la capacidad de agregar comentarios a un formulario o de rellenar los campos del formulario y guardarlo. Los formularios que tienen derechos de uso aplicados se denominan formularios habilitados para derechos. Un usuario que abre un formulario con derechos activados en Adobe Reader puede realizar operaciones que estén activadas para ese formulario.

Para aplicar derechos de uso a un formulario, el servicio de extensiones de Acrobat Reader DC debe formar parte de la instalación de formularios AEM. Además, debe tener una credencial válida que le permita aplicar derechos de uso a documentos PDF. Es decir, debe configurar correctamente el servicio de extensiones de Acrobat Reader DC para poder procesar un formulario con derechos activados. (Consulte [Acerca del servicio](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service)de extensiones de Acrobat Reader DC).

>[!NOTE]
>
>Para procesar un formulario que contenga derechos de uso, debe utilizar un archivo XDP como entrada, no un archivo PDF. Si se utiliza un archivo PDF como entrada, el formulario se seguirá procesando; sin embargo, no será un formulario con derechos activados.

>[!NOTE]
>
>No se puede rellenar previamente un formulario con datos XML cuando se especifican los siguientes derechos de uso: `enableComments`, `enableCommentsOnline`, `enableEmbeddedFiles`o `enableDigitalSignatures`. (Consulte [Rellenado previo de formularios con diseños](/help/forms/developing/prepopulating-forms-flowable-layouts.md)de posición variable).

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para procesar un formulario con derechos activados, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de Forms Client.
1. Configure las opciones de tiempo de ejecución de los derechos de uso.
1. Representar un formulario con derechos activados.
1. Escriba el formulario con derechos activados en el navegador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Forms Client**

Para poder realizar mediante programación una operación de API de cliente de servicio de Forms, debe crear un cliente de servicio de Forms.

**Definición de opciones de tiempo de ejecución de derechos de uso**

Debe definir las opciones de tiempo de ejecución de los derechos de uso para procesar un formulario con derechos activados. También debe especificar el alias de la credencial que se utiliza para aplicar derechos de uso a un formulario. Después de especificar el valor de alias, debe especificar cada derecho de uso que se aplicará al formulario.

**Representar un formulario con derechos activados**

Para procesar un formulario con derechos activados, se utiliza la misma lógica de aplicación que para procesar un formulario sin derechos de uso. La única diferencia es que debe asegurarse de que las opciones de tiempo de ejecución de los derechos de uso se incluyen en la lógica de la aplicación.

>[!NOTE]
>
>Cuando se procesa un formulario con derechos activados mediante la API de servicio web de Forms, no se pueden adjuntar archivos al formulario.

**Escribir el flujo de datos del formulario en el navegador web del cliente**

Cuando el servicio Forms procesa un formulario con derechos activados, devuelve una secuencia de datos de formulario que debe escribir en el explorador web del cliente. Una vez escrito en el navegador web del cliente, el formulario es visible para el usuario. Un usuario que visualiza el formulario con derechos activados en Adobe Reader puede realizar operaciones que estén activadas para ese formulario.

**Consulte también**

[Representar formularios habilitados para derechos mediante la API de Java](#render-rights-enabled-forms-using-the-java-api)

[Representar formularios habilitados para derechos mediante la API de servicio web](#render-rights-enabled-forms-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de formularios](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Representación de formularios PDF interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Creación de aplicaciones Web que procesan formularios](/help/forms/developing/creating-web-applications-renders-forms.md)

### Representar formularios habilitados para derechos mediante la API de Java {#render-rights-enabled-forms-using-the-java-api}

Representar un formulario con derechos activados mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clases del proyecto Java.

1. Creación de un objeto de API de Forms Client

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `FormsServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Definición de opciones de tiempo de ejecución de derechos de uso

   * Cree un `ReaderExtensionSpec` objeto con su constructor.
   * Especifique el alias de la credencial invocando el `ReaderExtensionSpec` método del `setReCredentialAlias` objeto y especifique un valor de cadena que represente el valor del alias.
   * Establezca cada derecho de uso invocando el método correspondiente que pertenece al `ReaderExtensionSpec` objeto. Sin embargo, solo puede establecer un derecho de uso si la credencial a la que hace referencia le permite hacerlo. Es decir, no puede establecer un derecho de uso si la credencial no le permite establecerlo. Por ejemplo. para definir el derecho de uso que permite al usuario rellenar campos de formulario y guardar el formulario, invoque el `ReaderExtensionSpec` método del `setReFillIn` objeto y pase `true`.
   >[!NOTE]
   >
   >No es necesario invocar el `ReaderExtensionSpec` método `setReCredentialPassword` del objeto. El servicio Forms no utiliza este método.

1. Representar un formulario con derechos activados

   Invoque el `FormsServiceClient` método del `renderPDFFormWithUsageRights` objeto y pase los valores siguientes:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un `com.adobe.idp.Document` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un `com.adobe.idp.Document` objeto vacío.
   * Un `PDFFormRenderSpec` objeto que almacena opciones de tiempo de ejecución.
   * Un `ReaderExtensionSpec` objeto que almacena opciones de tiempo de ejecución de derechos de uso.
   * Un `URLSpec` objeto que contiene valores de URI necesarios para el servicio Forms.
   El `renderPDFFormWithUsageRights` método devuelve un `FormsResult` objeto que contiene una secuencia de datos de formulario que se debe escribir en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un `com.adobe.idp.Document` objeto invocando el `FormsResult` método ‘s `getOutputContent` .
   * Obtenga el tipo de contenido del `com.adobe.idp.Document` objeto invocando su `getContentType` método.
   * Defina el tipo de contenido del `javax.servlet.http.HttpServletResponse` objeto invocando su `setContentType` método y pasando el tipo de contenido del `com.adobe.idp.Document` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el `javax.servlet.http.HttpServletResponse` método `getOutputStream` del objeto.
   * Cree un `java.io.InputStream` objeto invocando el `com.adobe.idp.Document` método `getInputStream` del objeto.
   * Cree una matriz de bytes para rellenarla con la secuencia de datos del formulario invocando el `InputStream` método `read` del objeto y pasando la matriz de bytes como argumento.
   * Invoque el `javax.servlet.ServletOutputStream` método del `write` objeto para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al `write` método .

**Consulte también**

[Inicio rápido (modo SOAP): Representación de un formulario con derechos activados mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Representar formularios habilitados para derechos mediante la API de servicio web {#render-rights-enabled-forms-using-the-web-service-api}

Representar un formulario con derechos activados mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases proxy de Java que consuman el WSDL del servicio Forms.
   * Incluya las clases proxy de Java en la ruta de clases.

1. Creación de un objeto de API de Forms Client

   Cree un `FormsService` objeto y defina los valores de autenticación.

1. Definición de opciones de tiempo de ejecución de derechos de uso

   * Cree un `ReaderExtensionSpec` objeto con su constructor.
   * Especifique el alias de la credencial invocando el `ReaderExtensionSpec` método del `setReCredentialAlias` objeto y especifique un valor de cadena que represente el valor del alias.
   * Establezca cada derecho de uso invocando el método correspondiente que pertenece al `ReaderExtensionSpec` objeto. Sin embargo, solo puede establecer un derecho de uso si la credencial a la que hace referencia le permite hacerlo. Es decir, no puede establecer un derecho de uso si la credencial no le permite establecerlo. Para definir el derecho de uso que permite al usuario rellenar los campos del formulario y guardarlo, invoque el `ReaderExtensionSpec` método `setReFillIn` del objeto y pase `true`.

1. Representar un formulario con derechos activados

   Invoque el `FormsService` método del `renderPDFFormWithUsageRights` objeto y pase los valores siguientes:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un `BLOB` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos con el formulario, debe pasar un `BLOB` objeto basado en un origen de datos XML vacío. No se puede pasar un `BLOB` objeto que sea nulo; de lo contrario, se genera una excepción.
   * Un `PDFFormRenderSpec` objeto que almacena opciones de tiempo de ejecución.
   * Un `ReaderExtensionSpec` objeto que almacena opciones de tiempo de ejecución de derechos de uso.
   * Un `URLSpec` objeto que contiene valores de URI necesarios para el servicio Forms.
   El `renderPDFFormWithUsageRights` método devuelve un `FormsResult` objeto que contiene una secuencia de datos de formulario que se debe escribir en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un `BLOB` objeto que contenga datos de formulario invocando el `FormsResult` método `getOutputContent` del objeto.
   * Obtenga el tipo de contenido del `BLOB` objeto invocando su `getContentType` método.
   * Defina el tipo de contenido del `javax.servlet.http.HttpServletResponse` objeto invocando su `setContentType` método y pasando el tipo de contenido del `BLOB` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el `javax.servlet.http.HttpServletResponse` método `getOutputStream` del objeto.
   * Cree una matriz de bytes y rellénela invocando el `BLOB` método `getBinaryData` del objeto. Esta tarea asigna el contenido del `FormsResult` objeto a la matriz de bytes.
   * Invoque el `javax.servlet.http.HttpServletResponse` método del `write` objeto para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al `write` método .

**Consulte también**

[Formularios habilitados para derechos de representación](#rendering-rights-enabled-forms)

[Invocación de formularios AEM con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
