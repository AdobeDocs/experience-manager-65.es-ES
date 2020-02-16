---
title: Optimización del rendimiento del servicio Forms
seo-title: Optimización del rendimiento del servicio Forms
description: nulo
seo-description: nulo
uuid: 9040c09a-e5d0-432b-b1c5-ad46ab57c4fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f883483-b81e-42c6-a4a1-eb499dd112e7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Optimización del rendimiento del servicio Forms {#optimizing-the-performance-of-theforms-service}

## Optimización del rendimiento del servicio Forms {#optimizing-the-performance-of-the-forms-service}

Al procesar un formulario, puede definir opciones en tiempo de ejecución que optimizarán el rendimiento del servicio Forms. Otra tarea que puede realizar para mejorar el rendimiento del servicio Forms es almacenar archivos XDP en el repositorio. Sin embargo, esta sección no describe cómo realizar esta tarea. (Consulte [Invocación de un servicio mediante una biblioteca](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)de cliente Java).

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para optimizar el rendimiento del servicio Forms al procesar un formulario, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de Forms Client.
1. Configure las opciones de rendimiento en tiempo de ejecución.
1. Representar el formulario.
1. Escriba la secuencia de datos del formulario en el navegador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Forms Client**

Para poder realizar mediante programación una operación de API de cliente de servicio de Forms, debe crear un cliente de servicio de Forms. Si utiliza la API de Java, cree un `FormsServiceClient` objeto. Si utiliza la API de servicio web de Forms, cree un `FormsService` objeto.

**Establecer las opciones de tiempo de ejecución del rendimiento**

Puede definir las siguientes opciones de rendimiento en tiempo de ejecución para mejorar el rendimiento del servicio Forms:

* **Procesamiento de formularios en la caché**: Puede almacenar en caché un formulario procesado como PDF en la caché del servidor. Cada formulario se almacena en la caché una vez que se genera por primera vez. En un procesamiento posterior, si el formulario en caché es más reciente que la marca de tiempo del diseño de formulario, el formulario se recupera de la caché. Al almacenar en caché los formularios, se mejora el rendimiento del servicio Forms porque no tiene que recuperar el diseño de formulario de un repositorio.
* Las guías de formulario (obsoletas) pueden tardar más en procesarse que otros tipos de transformación. Se recomienda guardar en caché las guías de formulario (obsoletas) para mejorar el rendimiento.
* **Opción** independiente: Si no necesita que el servicio Forms realice cálculos en el servidor, puede establecer la opción Independiente en `true`, lo que resulta en que los formularios se procesen sin información de estado. La información de estado es necesaria si desea procesar un formulario interactivo para un usuario final que, a continuación, introduce información en el formulario y lo devuelve al servicio Forms. A continuación, el servicio Forms realiza una operación de cálculo y devuelve el formulario al usuario con los resultados mostrados en el formulario. Si se devuelve un formulario sin información de estado al servicio Forms, solo estarán disponibles los datos XML y no se realizarán cálculos en el servidor.
* **PDF** linealizado: Un archivo PDF linealizado está organizado para permitir un acceso incremental eficiente en un entorno de red. El archivo PDF es válido en todos los aspectos y es compatible con todos los visores existentes y otras aplicaciones PDF. Es decir, se puede ver un PDF linealizado mientras se está descargando.
* Esta opción no mejora el rendimiento cuando se procesa un formulario PDF en el cliente.
* **GuideRSL, opción**: Habilita la generación de guías de formulario (desaprobada) mediante bibliotecas compartidas en tiempo de ejecución. Esto significa que la primera solicitud descargará un archivo SWF más pequeño, además de bibliotecas compartidas más grandes que se almacenan en la caché del explorador. Para obtener más información, consulte RSL en la documentación de Flex.
* También puede mejorar el rendimiento del servicio Forms procesando un formulario en el cliente. (Consulte [Representación de formularios en el cliente](/help/forms/developing/rendering-forms-client.md)).

**Representar el formulario**

Para procesar el formulario después de definir las opciones de rendimiento, se utiliza la misma lógica de aplicación que para procesar un formulario sin opciones de rendimiento.

**Escribir el flujo de datos del formulario en el navegador web del cliente**

Una vez que el servicio Forms procesa un formulario, devuelve una secuencia de datos de formulario que debe escribir en el explorador web del cliente. Cuando se escribe en el navegador web del cliente, el formulario es visible para el usuario.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de formularios](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Representación de formularios PDF interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Representación de formularios como HTML](/help/forms/developing/rendering-forms-html.md)

[Creación de aplicaciones Web que procesan formularios](/help/forms/developing/creating-web-applications-renders-forms.md)

### Optimizar el rendimiento mediante la API de Java {#optimize-the-performance-using-the-java-api}

Representar un formulario con rendimiento optimizado mediante la API de formularios (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clases del proyecto Java.

1. Creación de un objeto de API de Forms Client

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `FormsServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Establecer las opciones de tiempo de ejecución del rendimiento

   * Cree un `PDFFormRenderSpec` objeto con su constructor.
   * Defina la opción de la caché de formularios invocando el `PDFFormRenderSpec` método `setCacheEnabled` del objeto y pasando `true`.
   * Establezca la opción linealizada invocando el `PDFFormRenderSpec` método del `setLinearizedPDF` objeto y pasando `true.`

1. Representar el formulario

   Invoque el `FormsServiceClient` método del `renderPDFForm` objeto y pase los valores siguientes:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo.
   * Un `com.adobe.idp.Document` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un `com.adobe.idp.Document` objeto vacío.
   * Un `PDFFormRenderSpec` objeto que almacena opciones de tiempo de ejecución para mejorar el rendimiento.
   * Un `URLSpec` objeto que contiene valores de URI necesarios para el servicio Forms.
   * Un `java.util.HashMap` objeto que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   El `renderPDFForm` método devuelve un `FormsResult` objeto que contiene una secuencia de datos de formulario que se debe escribir en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un `javax.servlet.ServletOutputStream` objeto que se utilice para enviar una secuencia de datos de formulario al navegador web del cliente.
   * Cree un `com.adobe.idp.Document` objeto invocando el `FormsResult` método ‘s `getOutputContent` .
   * Cree un `java.io.InputStream` objeto invocando el `com.adobe.idp.Document` método `getInputStream` del objeto.
   * Cree una matriz de bytes y rellénela con la secuencia de datos del formulario invocando el `InputStream` método del `read`objeto y pasando la matriz de bytes como argumento.
   * Invoque el `javax.servlet.ServletOutputStream` método del `write` objeto para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al `write` método .

**Consulte también**

[Inicio rápido (modo SOAP): Optimización del rendimiento mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Optimizar el rendimiento mediante la API de servicio Web {#optimize-the-performance-using-the-web-service-api}

Representar un formulario con rendimiento optimizado mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases proxy de Java que consuman el WSDL del servicio Forms.
   * Incluya las clases proxy de Java en la ruta de clases.

1. Creación de un objeto de API de Forms Client

   Cree un `FormsService` objeto y defina los valores de autenticación.

1. Establecer las opciones de tiempo de ejecución del rendimiento

   * Cree un `PDFFormRenderSpec` objeto con su constructor.
   * Defina la opción de la caché de formularios invocando el `PDFFormRenderSpec` método del `setCacheEnabled` objeto y pasando true.
   * Establezca la opción independiente invocando el `PDFFormRenderSpec` método del `setStandAlone` objeto y pasando true.
   * Establezca la opción linealizada invocando el `PDFFormRenderSpec` método del `setLinearizedPDF` objeto y pasando true.

1. Representar el formulario

   Invoque el `FormsService` método del `renderPDFForm` objeto y pase los valores siguientes:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo.
   * Un `BLOB` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`.
   * Un `PDFFormRenderSpecc` objeto que almacena opciones de tiempo de ejecución.
   * Un `URLSpec` objeto que contiene valores de URI necesarios para el servicio Forms.
   * Un `java.util.HashMap` objeto que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Objeto vacío `com.adobe.idp.services.holders.BLOBHolder` que se rellena con el método . Se utiliza para almacenar el formulario PDF procesado.
   * Objeto vacío `javax.xml.rpc.holders.LongHolder` que se rellena con el método . (Este argumento almacenará el número de páginas del formulario).
   * Objeto vacío `javax.xml.rpc.holders.StringHolder` que se rellena con el método . (Este argumento almacenará el valor de configuración regional).
   * Un `com.adobe.idp.services.holders.FormsResultHolder` objeto vacío que contendrá los resultados de esta operación.
   El `renderPDFForm` método rellena el `com.adobe.idp.services.holders.FormsResultHolder` objeto que se pasa como el último valor de argumento con una secuencia de datos de formulario que se debe escribir en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un `FormResult` objeto obteniendo el valor del `com.adobe.idp.services.holders.FormsResultHolder` miembro de `value` datos del objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto que se utilice para enviar una secuencia de datos de formulario al navegador web del cliente.
   * Cree un `BLOB` objeto que contenga datos de formulario invocando el `FormsResult` método `getOutputContent` del objeto.
   * Cree una matriz de bytes y rellénela invocando el `BLOB` método `getBinaryData` del objeto. Esta tarea asigna el contenido del `FormsResult` objeto a la matriz de bytes.
   * Invoque el `javax.servlet.http.HttpServletResponse` método del `write` objeto para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al `write` método .

**Consulte también**

[Invocación de formularios AEM con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
