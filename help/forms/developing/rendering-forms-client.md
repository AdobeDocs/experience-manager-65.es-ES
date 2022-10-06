---
title: Representación de Forms en el cliente
seo-title: Rendering Forms at the Client
description: Optimice la entrega del contenido del PDF y mejore la capacidad del servicio de Forms para gestionar la carga de red mediante la capacidad de renderización del lado del cliente de Acrobat o Adobe Reader
seo-description: Optimize the delivery of PDF content and improve the Forms service’s ability to handle network load by using the client-side rendering capability of Acrobat or Adobe Reader
uuid: 09bcc23d-28b0-473a-87f1-bc17e87620f4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 08d36e9f-cafc-478e-9781-8fc29ac6262e
role: Developer
exl-id: e485980d-f200-46b7-9284-c9996003aa47
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 0%

---

# Representación de Forms en el cliente {#rendering-forms-at-the-client}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

## Representación de Forms en el cliente {#rendering-forms-at-the-client-inner}

Puede optimizar la entrega del contenido del PDF y mejorar la capacidad del servicio Forms para gestionar la carga de red mediante la función de renderización del lado del cliente de Acrobat o Adobe Reader. Este proceso se conoce como procesamiento de un formulario en el cliente. Para procesar un formulario en el cliente, el dispositivo cliente (normalmente un explorador web) debe utilizar Acrobat 7.0 o Adobe Reader 7.0 o posterior.

Los cambios en un formulario resultantes de la ejecución de secuencias de comandos en el servidor no se reflejan en un formulario procesado en el cliente a menos que el subformulario raíz contenga la variable `restoreState` atributo que está establecido en `auto`. Para obtener más información sobre este atributo, consulte [Diseñador de Forms.](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para procesar un formulario en el cliente, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Establezca las opciones de tiempo de ejecución de procesamiento del cliente.
1. Representar un formulario en el cliente.
1. Escriba el formulario en el explorador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de cliente de Forms**

Para poder realizar mediante programación una operación de API de cliente de servicio de Forms, debe crear un cliente de servicio de Forms. Si utiliza la API de Java, cree un `FormsServiceClient` objeto. Si utiliza la API del servicio web de Forms, cree un `FormsService` objeto.

**Establecer las opciones de ejecución de procesamiento del cliente**

Debe definir la opción tiempo de ejecución de procesamiento del cliente para procesar un formulario en el cliente configurando la variable `RenderAtClient` opción de tiempo de ejecución a `true`. Esto hace que el formulario se envíe al dispositivo cliente en el que se procese. If `RenderAtClient` es `auto` (el valor predeterminado), el diseño de formulario determina si el formulario se procesa en el cliente. El diseño de formulario debe ser un diseño de formulario con una presentación flexible.

Una opción opcional de tiempo de ejecución que puede establecer es la `SeedPDF` . La variable `SeedPDF` combina el contenedor de PDF (documento de PDF semilla) con el diseño de formulario y los datos XML. Tanto el diseño de formulario como los datos XML se envían a Acrobat o Adobe Reader, donde se procesa el formulario. La variable `SeedPDF` se puede utilizar cuando el equipo cliente no tiene fuentes que se utilicen en el formulario, como cuando un usuario final no tiene licencia para utilizar una fuente para la que el propietario del formulario tenga licencia.

Puede utilizar Designer para crear un archivo de PDF dinámico simple y utilizarlo como archivo de PDF semilla. Se requieren los siguientes pasos para realizar esta tarea:

1. Determine si debe incrustar las fuentes dentro del archivo del PDF semilla. El archivo del PDF semilla deberá contener las fuentes adicionales requeridas por el formulario que se está procesando. Al incrustar fuentes en el archivo del PDF semilla, asegúrese de no infringir ningún acuerdo de licencia de fuentes. En Designer, puede determinar si las fuentes se pueden incrustar legalmente. Al guardar, si hay fuentes que no se pueden incrustar en el formulario, Designer muestra un mensaje con las fuentes que no se pueden incrustar. Este mensaje no se muestra en Designer en documentos PDF estáticos.
1. Si está creando el archivo de PDF semilla en Designer, se recomienda que, como mínimo, agregue un campo de texto que contenga un mensaje. El mensaje debe dirigirse a los usuarios de versiones anteriores de Adobe Reader indicando que necesitan Acrobat 7.0 o posterior, o Adobe Reader 7.0 o posterior para ver el documento.
1. Guarde el archivo del PDF semilla como un archivo del PDF dinámico con la extensión de nombre de archivo del PDF.

>[!NOTE]
>
>No es necesario definir la opción de tiempo de ejecución del PDF semilla para procesar un formulario en el cliente. Si no especifica un PDF semilla, el servicio Forms crea un shell pdf que no contendrá objetos COS pero contendrá un envoltorio de PDF con el contenido XDP real incrustado dentro. Los pasos de esta sección no establecen la opción de tiempo de ejecución del PDF semilla. Para obtener información sobre los objetos COS, consulte la guía de referencia de Adobe PDF.

**Representar un formulario en el cliente**

Para procesar un formulario en el cliente, debe asegurarse de que las opciones de tiempo de ejecución de representación del cliente se incluyen en la lógica de la aplicación para procesar un formulario.

**Escribir el flujo de datos del formulario en el explorador web del cliente**

El servicio Forms crea un flujo de datos de formulario que debe escribir en el explorador web del cliente. Cuando se escribe en el explorador web del cliente, el formulario lo representa Acrobat 7.0 o Adobe Reader 7.0 o posterior y es visible para el usuario.

**Consulte también lo siguiente**

[Representar un formulario en el cliente mediante la API de Java](#render-a-form-at-the-client-using-the-java-api)

[Representar un formulario en el cliente mediante la API de servicio web](#render-a-form-at-the-client-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Pasar documentos al servicio de Forms](/help/forms/developing/passing-documents-forms-service.md)

[Creación de aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Representar un formulario en el cliente mediante la API de Java {#render-a-form-at-the-client-using-the-java-api}

Representar un formulario en el cliente mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-forms-client.jar, en la ruta de clase de su proyecto Java.

1. Creación de un objeto de API de cliente de Forms

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `FormsServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Establecer las opciones de ejecución de procesamiento del cliente

   * Cree un `PDFFormRenderSpec` usando su constructor.
   * Configure las variables `RenderAtClient` opción en tiempo de ejecución invocando la variable `PDFFormRenderSpec` del objeto `setRenderAtClient` método y pasar el valor de enumeración `RenderAtClient.Yes`.

1. Representar un formulario en el cliente

   Invocar el `FormsServiceClient` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de AEM Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un vacío `com.adobe.idp.Document` objeto.
   * A `PDFFormRenderSpec` que almacena las opciones en tiempo de ejecución necesarias para procesar un formulario en el cliente.
   * A `URLSpec` objeto que contiene valores de URI necesarios para el servicio Forms para procesar un formulario.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   La variable `renderPDFForm` el método devuelve un `FormsResult` objeto que contiene un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un `com.adobe.idp.Document` invocando el objeto `FormsResult` objeto ‘s `getOutputContent` método.
   * Obtenga el tipo de contenido de la variable `com.adobe.idp.Document` invocando su `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasar el tipo de contenido de la variable `com.adobe.idp.Document` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos del formulario en el explorador web del cliente invocando la variable `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Cree un `java.io.InputStream` invocando el objeto `com.adobe.idp.Document` del objeto `getInputStream` método.
   * Cree una matriz de bytes y rellénela con la secuencia de datos del formulario invocando la variable `InputStream` del objeto `read` y pasando la matriz de bytes como argumento.
   * Invocar el `javax.servlet.ServletOutputStream` del objeto `write` método para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes a la `write` método.

**Consulte también lo siguiente**

[Inicio rápido (modo SOAP): Representación de un formulario en el cliente mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Representar un formulario en el cliente mediante la API de servicio web {#render-a-form-at-the-client-using-the-web-service-api}

Representar un formulario en el cliente mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases proxy de Java en la ruta de clase.

1. Creación de un objeto de API de cliente de Forms

   Cree un `FormsService` y establezca los valores de autenticación.

1. Establecer las opciones de ejecución de procesamiento del cliente

   * Cree un `PDFFormRenderSpec` usando su constructor.
   * Configure las variables `RenderAtClient` opción en tiempo de ejecución invocando la variable `PDFFormRenderSpec` del objeto `setRenderAtClient` método y pasar el valor de cadena `RenderAtClient.Yes`.

1. Representar un formulario en el cliente

   Invocar el `FormsService` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`. (Consulte [Rellenado previo de Forms con diseños flexibles](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * A `PDFFormRenderSpec` que almacena las opciones en tiempo de ejecución necesarias para procesar un formulario en el cliente.
   * A `URLSpec` que contiene valores de URI necesarios para el servicio Forms.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un vacío `com.adobe.idp.services.holders.BLOBHolder` objeto que rellena el método . Este parámetro se utiliza para almacenar el formulario de PDF procesado.
   * Un vacío `javax.xml.rpc.holders.LongHolder` objeto que rellena el método . (Este argumento almacenará el número de páginas del formulario).
   * Un vacío `javax.xml.rpc.holders.StringHolder` objeto que rellena el método . (Este argumento almacenará el valor de configuración regional).
   * Un vacío `com.adobe.idp.services.holders.FormsResultHolder` que contendrá los resultados de esta operación.

   La variable `renderPDFForm` rellena el `com.adobe.idp.services.holders.FormsResultHolder` objeto que se pasa como el último valor de argumento con un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un `FormResult` obteniendo el valor de `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value` miembro de datos.
   * Cree un `BLOB` objeto que contiene datos de formulario invocando la variable `FormsResult` del objeto `getOutputContent` método.
   * Obtenga el tipo de contenido de la variable `BLOB` invocando su `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasar el tipo de contenido de la variable `BLOB` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos del formulario en el explorador web del cliente invocando la variable `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Cree una matriz de bytes y rellénela invocando la variable `BLOB` del objeto `getBinaryData` método. Esta tarea asigna el contenido de la variable `FormsResult` a la matriz de bytes.
   * Invocar el `javax.servlet.http.HttpServletResponse` del objeto `write` método para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes a la `write` método.

**Consulte también lo siguiente**

[Representación de Forms en el cliente](#rendering-forms-at-the-client)

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
