---
title: Representación de formularios en el cliente
seo-title: Representación de formularios en el cliente
description: nulo
seo-description: nulo
uuid: 09bcc23d-28b0-473a-87f1-bc17e87620f4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 08d36e9f-cafc-478e-9781-8fc29ac6262e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Representación de formularios en el cliente {#rendering-forms-at-the-client}

## Representación de formularios en el cliente {#rendering-forms-at-the-client-inner}

Puede optimizar la entrega de contenido PDF y mejorar la capacidad del servicio Forms para gestionar la carga de red mediante la función de representación del lado del cliente de Acrobat o Adobe Reader. Este proceso se denomina procesamiento de un formulario en el cliente. Para procesar un formulario en el cliente, el dispositivo cliente (normalmente un navegador web) debe utilizar Acrobat 7.0 o Adobe Reader 7.0 o posterior.

Los cambios en un formulario resultantes de la ejecución de una secuencia de comandos en el lado del servidor no se reflejan en un formulario que se procesa en el cliente a menos que el subformulario raíz contenga el `restoreState` atributo definido en `auto`. Para obtener más información sobre este atributo, consulte Diseñador de [formularios.](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para procesar un formulario en el cliente, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de Forms Client.
1. Configure las opciones de tiempo de ejecución de procesamiento del cliente.
1. Representar un formulario en el cliente.
1. Escriba el formulario en el navegador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Forms Client**

Para poder realizar mediante programación una operación de API de cliente de servicio de Forms, debe crear un cliente de servicio de Forms. Si utiliza la API de Java, cree un `FormsServiceClient` objeto. Si utiliza la API de servicio web de Forms, cree un `FormsService` objeto.

**Definir las opciones de tiempo de ejecución de procesamiento del cliente**

Debe definir la opción de tiempo de ejecución de representación del cliente para procesar un formulario en el cliente estableciendo la opción de tiempo de ejecución en `RenderAtClient``true`. De este modo, el formulario se envía al dispositivo cliente en el que se procesa. Si `RenderAtClient` es `auto` (el valor predeterminado), el diseño de formulario determina si el formulario se procesa en el cliente. El diseño de formulario debe ser un diseño de formulario con una presentación flexible.

Una opción opcional de tiempo de ejecución que puede establecer es la `SeedPDF` opción. La `SeedPDF` opción combina el contenedor PDF (documento PDF raíz) con el diseño de formulario y los datos XML. Tanto el diseño de formulario como los datos XML se envían a Acrobat o Adobe Reader, donde se procesa el formulario. La `SeedPDF` opción se puede utilizar cuando el equipo cliente no tiene fuentes que se utilicen en el formulario, como cuando un usuario final no tiene licencia para utilizar una fuente que el propietario del formulario tenga licencia para utilizar.

Puede utilizar Designer para crear un archivo PDF dinámico sencillo y utilizarlo como archivo PDF raíz. Se requieren los siguientes pasos para realizar esta tarea:

1. Determine si necesita incrustar alguna fuente dentro del archivo PDF raíz. El archivo PDF raíz deberá contener fuentes adicionales requeridas por el formulario que se está procesando. Al incrustar fuentes en el archivo PDF raíz, asegúrese de que no infringe ningún acuerdo de licencia de fuentes. En Designer, puede determinar si las fuentes se pueden incrustar legalmente. Al guardar, si hay fuentes que no se pueden incrustar en el formulario, Designer muestra un mensaje con las fuentes que no se pueden incrustar. Este mensaje no se muestra en Designer para documentos PDF estáticos.
1. Si va a crear el archivo PDF raíz en Designer, se recomienda que, como mínimo, agregue un campo de texto que contenga un mensaje. El mensaje debe dirigirse a los usuarios de versiones anteriores de Adobe Reader indicando que necesitan Acrobat 7.0 o posterior o Adobe Reader 7.0 o posterior para ver el documento.
1. Guarde el archivo PDF raíz como un archivo PDF dinámico con la extensión de nombre de archivo PDF.

>[!NOTE]
>
>No es necesario definir la opción de tiempo de ejecución del PDF de raíz para procesar un formulario en el cliente. Si no especifica un PDF raíz, el servicio Forms crea un PDF raíz que no contendrá objetos COS, pero contendrá un contenedor PDF con el contenido XDP real incrustado dentro. Los pasos de esta sección no definen la opción de tiempo de ejecución del PDF raíz. Para obtener más información sobre los objetos COS, consulte la Guía de referencia de Adobe PDF.

**Representar un formulario en el cliente**

Para procesar un formulario en el cliente, debe asegurarse de que las opciones de procesamiento en tiempo de ejecución del cliente se incluyen en la lógica de la aplicación para procesar un formulario.

**Escribir el flujo de datos del formulario en el navegador web del cliente**

El servicio Forms crea una secuencia de datos de formulario que se debe escribir en el navegador web del cliente. Cuando se escribe en el navegador web del cliente, el formulario se procesa con Acrobat 7.0 o Adobe Reader 7.0 o posterior y es visible para el usuario.

**Consulte también**

[Representar un formulario en el cliente mediante la API de Java](#render-a-form-at-the-client-using-the-java-api)

[Representar un formulario en el cliente mediante la API de servicio Web](#render-a-form-at-the-client-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de formularios](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Pasar documentos al servicio Forms](/help/forms/developing/passing-documents-forms-service.md)

[Creación de aplicaciones Web que procesan formularios](/help/forms/developing/creating-web-applications-renders-forms.md)

### Representar un formulario en el cliente mediante la API de Java {#render-a-form-at-the-client-using-the-java-api}

Representar un formulario en el cliente mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clases del proyecto Java.

1. Creación de un objeto de API de Forms Client

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `FormsServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Definir las opciones de tiempo de ejecución de procesamiento del cliente

   * Cree un `PDFFormRenderSpec` objeto con su constructor.
   * Establezca la opción de tiempo de ejecución `RenderAtClient` invocando el `PDFFormRenderSpec` método `setRenderAtClient` del objeto y pasando el valor enum `RenderAtClient.Yes`.

1. Representar un formulario en el cliente

   Invoque el `FormsServiceClient` método del `renderPDFForm` objeto y pase los valores siguientes:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de AEM Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un `com.adobe.idp.Document` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un `com.adobe.idp.Document` objeto vacío.
   * Un `PDFFormRenderSpec` objeto que almacena las opciones en tiempo de ejecución necesarias para procesar un formulario en el cliente.
   * Un `URLSpec` objeto que contiene valores de URI que el servicio Forms requiere para procesar un formulario.
   * Un `java.util.HashMap` objeto que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   El `renderPDFForm` método devuelve un `FormsResult` objeto que contiene una secuencia de datos de formulario que se debe escribir en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un `com.adobe.idp.Document` objeto invocando el `FormsResult` método ‘s `getOutputContent` .
   * Obtenga el tipo de contenido del `com.adobe.idp.Document` objeto invocando su `getContentType` método.
   * Defina el tipo de contenido del `javax.servlet.http.HttpServletResponse` objeto invocando su `setContentType` método y pasando el tipo de contenido del `com.adobe.idp.Document` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el `javax.servlet.http.HttpServletResponse` método `getOutputStream` del objeto.
   * Cree un `java.io.InputStream` objeto invocando el `com.adobe.idp.Document` método `getInputStream` del objeto.
   * Cree una matriz de bytes y rellénela con la secuencia de datos del formulario invocando el `InputStream` método del `read` objeto y pasando la matriz de bytes como argumento.
   * Invoque el `javax.servlet.ServletOutputStream` método del `write` objeto para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al `write` método .

**Consulte también**

[Inicio rápido (modo SOAP): Representación de un formulario en el cliente mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Representar un formulario en el cliente mediante la API de servicio Web {#render-a-form-at-the-client-using-the-web-service-api}

Representar un formulario en el cliente mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases proxy de Java que consuman el WSDL del servicio Forms.
   * Incluya las clases proxy de Java en la ruta de clases.

1. Creación de un objeto de API de Forms Client

   Cree un `FormsService` objeto y defina los valores de autenticación.

1. Definir las opciones de tiempo de ejecución de procesamiento del cliente

   * Cree un `PDFFormRenderSpec` objeto con su constructor.
   * Establezca la opción de tiempo de ejecución `RenderAtClient` invocando el `PDFFormRenderSpec` método `setRenderAtClient` del objeto y pasando el valor de cadena `RenderAtClient.Yes`.

1. Representar un formulario en el cliente

   Invoque el `FormsService` método del `renderPDFForm` objeto y pase los valores siguientes:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un `BLOB` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`. (Consulte [Rellenado previo de formularios con diseños]de posición variable (/help/forms/develop/renderizado-formularios cumplimentación previa de formularios-presentación-presentación-presentación-formularios-rellenado previo.md#prerellating-forms-with-flowable-layouts).
   * Un `PDFFormRenderSpec` objeto que almacena las opciones en tiempo de ejecución necesarias para procesar un formulario en el cliente.
   * Un `URLSpec` objeto que contiene valores de URI necesarios para el servicio Forms.
   * Un `java.util.HashMap` objeto que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Objeto vacío `com.adobe.idp.services.holders.BLOBHolder` que se rellena con el método . Este parámetro se utiliza para almacenar el formulario PDF procesado.
   * Objeto vacío `javax.xml.rpc.holders.LongHolder` que se rellena con el método . (Este argumento almacenará el número de páginas del formulario).
   * Objeto vacío `javax.xml.rpc.holders.StringHolder` que se rellena con el método . (Este argumento almacenará el valor de configuración regional).
   * Un `com.adobe.idp.services.holders.FormsResultHolder` objeto vacío que contendrá los resultados de esta operación.
   El `renderPDFForm` método rellena el `com.adobe.idp.services.holders.FormsResultHolder` objeto que se pasa como el último valor de argumento con una secuencia de datos de formulario que se debe escribir en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un `FormResult` objeto obteniendo el valor del `com.adobe.idp.services.holders.FormsResultHolder` miembro de `value` datos del objeto.
   * Cree un `BLOB` objeto que contenga datos de formulario invocando el `FormsResult` método `getOutputContent` del objeto.
   * Obtenga el tipo de contenido del `BLOB` objeto invocando su `getContentType` método.
   * Defina el tipo de contenido del `javax.servlet.http.HttpServletResponse` objeto invocando su `setContentType` método y pasando el tipo de contenido del `BLOB` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el `javax.servlet.http.HttpServletResponse` método `getOutputStream` del objeto.
   * Cree una matriz de bytes y rellénela invocando el `BLOB` método `getBinaryData` del objeto. Esta tarea asigna el contenido del `FormsResult` objeto a la matriz de bytes.
   * Invoque el `javax.servlet.http.HttpServletResponse` método del `write` objeto para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al `write` método .

**Consulte también**

[Representación de formularios en el cliente](#rendering-forms-at-the-client)

[Invocación de formularios AEM con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
