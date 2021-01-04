---
title: Optimización del rendimiento del servicio Forms
seo-title: Optimización del rendimiento del servicio Forms
description: Configure las opciones de tiempo de ejecución al procesar un formulario y almacene archivos XDP en el repositorio para optimizar el rendimiento del servicio de Forms.
seo-description: Configure las opciones de tiempo de ejecución al procesar un formulario y almacene archivos XDP en el repositorio para optimizar el rendimiento del servicio de Forms.
uuid: 9040c09a-e5d0-432b-b1c5-ad46ab57c4fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f883483-b81e-42c6-a4a1-eb499dd112e7
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 0%

---


# Optimización del rendimiento del servicio de Forms {#optimizing-the-performance-of-theforms-service}

## Optimización del rendimiento del servicio de Forms {#optimizing-the-performance-of-the-forms-service}

Al procesar un formulario, puede definir opciones en tiempo de ejecución que optimizarán el rendimiento del servicio de Forms. Otra tarea que puede realizar para mejorar el rendimiento del servicio Forms es almacenar archivos XDP en el repositorio. Sin embargo, esta sección no describe cómo realizar esta tarea. (Consulte [Invocación de un servicio mediante una biblioteca de cliente Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)).

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para optimizar el rendimiento del servicio Forms al procesar un formulario, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Configure las opciones de rendimiento en tiempo de ejecución.
1. Representar el formulario.
1. Escriba la secuencia de datos del formulario en el navegador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Forms Client**

Para poder realizar mediante programación una operación de API de cliente de servicio de Forms, debe crear un cliente de servicio de Forms. Si utiliza la API de Java, cree un objeto `FormsServiceClient`. Si utiliza la API de servicio Web de Forms, cree un objeto `FormsService`.

**Configurar las opciones de tiempo de ejecución del rendimiento**

Puede definir las siguientes opciones de rendimiento en tiempo de ejecución para mejorar el rendimiento del servicio Forms:

* **Procesamiento de formularios en la caché**: Puede almacenar en caché un formulario procesado como PDF en la caché del servidor. Cada formulario se almacena en la caché una vez que se genera por primera vez. En un procesamiento posterior, si el formulario en caché es más reciente que la marca de tiempo del diseño de formulario, el formulario se recupera de la caché. Al almacenar los formularios en la caché, se mejora el rendimiento del servicio Forms porque no tiene que recuperar el diseño de formulario de un repositorio.
* Las guías de formulario (obsoletas) pueden tardar más en procesarse que otros tipos de transformación. Se recomienda guardar en caché las guías de formulario (obsoletas) para mejorar el rendimiento.
* **Opción** independiente: Si no necesita que el servicio Forms realice cálculos en el servidor, puede establecer la opción Independiente en  `true`, lo que resulta en que los formularios se procesen sin información de estado. La información de estado es necesaria si desea procesar un formulario interactivo para un usuario final que, a continuación, introduce información en el formulario y lo envía de nuevo al servicio de Forms. A continuación, el servicio Forms realiza una operación de cálculo y devuelve el formulario al usuario con los resultados mostrados en el formulario. Si se devuelve un formulario sin información de estado al servicio de Forms, solo estarán disponibles los datos XML y no se realizarán cálculos en el servidor.
* **PDF** linealizado: Un archivo PDF linealizado está organizado para permitir un acceso incremental eficiente en un entorno de red. El archivo PDF es válido en todos los aspectos y es compatible con todos los visores existentes y otras aplicaciones PDF. Es decir, se puede ver un PDF linealizado mientras se está descargando.
* Esta opción no mejora el rendimiento cuando se procesa un formulario PDF en el cliente.
* **GuideRSL, opción**: Habilita la generación de guías de formulario (desaprobada) mediante bibliotecas compartidas en tiempo de ejecución. Esto significa que la primera solicitud descargará un archivo SWF más pequeño, además de bibliotecas compartidas más grandes que se almacenan en la caché del explorador. Para obtener más información, consulte RSL en la documentación de Flex.
* También puede mejorar el rendimiento del servicio de Forms procesando un formulario en el cliente. (Consulte [Representación de Forms en el cliente](/help/forms/developing/rendering-forms-client.md)).

**Representar el formulario**

Para procesar el formulario después de definir las opciones de rendimiento, se utiliza la misma lógica de aplicación que para procesar un formulario sin opciones de rendimiento.

**Escribir el flujo de datos del formulario en el navegador web del cliente**

Una vez que el servicio Forms procesa un formulario, devuelve una secuencia de datos de formulario que debe escribir en el explorador web del cliente. Cuando se escribe en el navegador web del cliente, el formulario es visible para el usuario.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API de servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Representación de PDF forms interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Representación de Forms como HTML](/help/forms/developing/rendering-forms-html.md)

[Creación de Aplicaciones web que procesan Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Optimizar el rendimiento mediante la API de Java {#optimize-the-performance-using-the-java-api}

Representar un formulario con rendimiento optimizado mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clases del proyecto Java.

1. Creación de un objeto de API de Forms Client

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `FormsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Configurar las opciones de tiempo de ejecución del rendimiento

   * Cree un objeto `PDFFormRenderSpec` utilizando su constructor.
   * Configure la opción de caché de formularios invocando el método `PDFFormRenderSpec` del objeto `setCacheEnabled` y pasando `true`.
   * Configure la opción linealizada invocando el método `PDFFormRenderSpec` del objeto `setLinearizedPDF` y pasando `true.`

1. Representar el formulario

   Invoque el método `FormsServiceClient` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo.
   * Un objeto `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un objeto vacío `com.adobe.idp.Document`.
   * Un objeto `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución para mejorar el rendimiento.
   * Un objeto `URLSpec` que contiene valores de URI necesarios para el servicio de Forms.
   * Objeto `java.util.HashMap` que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El método `renderPDFForm` devuelve un objeto `FormsResult` que contiene una secuencia de datos de formulario que debe escribirse en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un objeto `javax.servlet.ServletOutputStream` que se utilice para enviar una secuencia de datos de formulario al explorador Web del cliente.
   * Cree un objeto `com.adobe.idp.Document` invocando el método `FormsResult` del objeto ‘s `getOutputContent`.
   * Cree un objeto `java.io.InputStream` invocando el método `com.adobe.idp.Document` del objeto `getInputStream`.
   * Cree una matriz de bytes y rellénela con la secuencia de datos del formulario invocando el método `InputStream` del objeto `read`y pasando la matriz de bytes como argumento.
   * Invoque el método `javax.servlet.ServletOutputStream` del objeto `write` para enviar la secuencia de datos del formulario al explorador Web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Inicio rápido (modo SOAP): Optimización del rendimiento mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Optimizar el rendimiento mediante la API de servicio Web {#optimize-the-performance-using-the-web-service-api}

Representar un formulario con rendimiento optimizado mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases proxy de Java que consuman el WSDL del servicio de Forms.
   * Incluya las clases proxy de Java en la ruta de clases.

1. Creación de un objeto de API de Forms Client

   Cree un objeto `FormsService` y defina los valores de autenticación.

1. Configurar las opciones de tiempo de ejecución del rendimiento

   * Cree un objeto `PDFFormRenderSpec` utilizando su constructor.
   * Configure la opción de caché de formularios invocando el método `PDFFormRenderSpec` del objeto `setCacheEnabled` y pasando true.
   * Establezca la opción independiente invocando el método `PDFFormRenderSpec` del objeto `setStandAlone` y pasando true.
   * Configure la opción linealizada invocando el método `PDFFormRenderSpec` del objeto `setLinearizedPDF` y pasando true.

1. Representar el formulario

   Invoque el método `FormsService` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo.
   * Un objeto `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`.
   * Un objeto `PDFFormRenderSpecc` que almacena opciones de tiempo de ejecución.
   * Un objeto `URLSpec` que contiene valores de URI necesarios para el servicio de Forms.
   * Objeto `java.util.HashMap` que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un objeto vacío `com.adobe.idp.services.holders.BLOBHolder` que se rellena con el método. Se utiliza para almacenar el formulario PDF procesado.
   * Un objeto vacío `javax.xml.rpc.holders.LongHolder` que se rellena con el método. (Este argumento almacenará el número de páginas del formulario).
   * Un objeto vacío `javax.xml.rpc.holders.StringHolder` que se rellena con el método. (Este argumento almacenará el valor de configuración regional).
   * Un objeto vacío `com.adobe.idp.services.holders.FormsResultHolder` que contendrá los resultados de esta operación.

   El método `renderPDFForm` rellena el objeto `com.adobe.idp.services.holders.FormsResultHolder` que se pasa como el último valor de argumento con una secuencia de datos de formulario que debe escribirse en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un objeto `FormResult` obteniendo el valor del miembro de datos `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se utilice para enviar una secuencia de datos de formulario al explorador Web del cliente.
   * Cree un objeto `BLOB` que contenga datos de formulario invocando el método `FormsResult` del objeto `getOutputContent`.
   * Cree una matriz de bytes y rellénela invocando el método `BLOB` del objeto `getBinaryData`. Esta tarea asigna el contenido del objeto `FormsResult` a la matriz de bytes.
   * Invoque el método `javax.servlet.http.HttpServletResponse` del objeto `write` para enviar la secuencia de datos del formulario al explorador Web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
