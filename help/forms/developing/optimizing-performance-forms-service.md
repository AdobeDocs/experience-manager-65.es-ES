---
title: Optimización del rendimiento del servicio Forms
seo-title: Optimizing the Performance of theForms Service
description: Configure las opciones en tiempo de ejecución al procesar un formulario y almacenar archivos XDP en el repositorio para optimizar el rendimiento del servicio Forms.
seo-description: Set run-time options when rendering a form and store XDP files in the repository to optimize the performance of the Forms service.
uuid: 9040c09a-e5d0-432b-b1c5-ad46ab57c4fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f883483-b81e-42c6-a4a1-eb499dd112e7
role: Developer
exl-id: 5a746c6c-bf6e-4b25-ba7c-a35edb1f55f3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1431'
ht-degree: 0%

---

# Optimización del rendimiento del servicio Forms {#optimizing-the-performance-of-theforms-service}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

## Optimización del rendimiento del servicio Forms {#optimizing-the-performance-of-the-forms-service}

Al procesar un formulario, puede definir opciones en tiempo de ejecución que optimicen el rendimiento del servicio Forms. Otra tarea que puede realizar para mejorar el rendimiento del servicio Forms es almacenar archivos XDP en el repositorio. Sin embargo, esta sección no describe cómo realizar esta tarea. (Consulte [Invocación de un servicio mediante una biblioteca de cliente Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library).)

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para optimizar el rendimiento del servicio Forms mientras se procesa un formulario, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Establezca las opciones de rendimiento en tiempo de ejecución.
1. Procese el formulario.
1. Escriba el flujo de datos del formulario en el explorador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de cliente de Forms**

Para poder realizar mediante programación una operación de API de cliente de servicio de Forms, debe crear un cliente de servicio de Forms. Si utiliza la API de Java, cree un `FormsServiceClient` objeto. Si utiliza la API del servicio web de Forms, cree un `FormsService` objeto.

**Establecer opciones de tiempo de ejecución del rendimiento**

Puede configurar las siguientes opciones de rendimiento en tiempo de ejecución para mejorar el rendimiento del servicio Forms:

* **Procesamiento de formularios en la caché**: Se puede almacenar en caché un formulario procesado como PDF en la caché del servidor. Cada formulario se almacena en caché una vez que se genera por primera vez. En un procesamiento posterior, si el formulario almacenado en caché es más reciente que la marca de tiempo del diseño de formulario, el formulario se recupera de la caché. Al almacenar en caché los formularios, se mejora el rendimiento del servicio Forms porque no tiene que recuperar el diseño de formulario de un repositorio.
* Las guías del formulario (obsoletas) pueden tardar más en procesarse que otros tipos de transformación. Se recomienda almacenar en caché las guías del formulario (obsoleto) para mejorar el rendimiento.
* **Opción independiente**: Si no necesita que el servicio Forms realice cálculos en el servidor, puede establecer la opción Independiente en `true`, lo que hace que los formularios se procesen sin información de estado. La información de estado es necesaria si desea procesar un formulario interactivo para un usuario final que, a continuación, introduzca información en el formulario y lo envíe de nuevo al servicio de Forms. A continuación, el servicio Forms realiza una operación de cálculo y vuelve a procesar el formulario para el usuario con los resultados mostrados en el formulario. Si se devuelve un formulario sin información de estado al servicio Forms, solo están disponibles los datos XML y no se realizan cálculos en el servidor.
* **PDF lineal**: Se organiza un archivo PDF lineal para permitir un acceso incremental eficiente en un entorno de red. El archivo de PDF es PDF válido en todos los aspectos y es compatible con todos los visores existentes y otras aplicaciones de PDF. Es decir, se puede ver un PDF linealizado mientras se sigue descargando.
* Esta opción no mejora el rendimiento cuando se procesa un formulario de PDF en el cliente.
* **Opción GuideRSL**: Habilita la generación de guías de formulario (obsoleto) mediante bibliotecas compartidas en tiempo de ejecución. Esto significa que la primera solicitud descargará un archivo SWF más pequeño, además de bibliotecas compartidas más grandes que se almacenan en la caché del explorador. Para obtener más información, consulte RSL en la documentación de Flex.
* También puede mejorar el rendimiento del servicio Forms procesando un formulario en el cliente. (Consulte [Representación de Forms en el cliente](/help/forms/developing/rendering-forms-client.md).)

**Procesamiento del formulario**

Para procesar el formulario después de definir las opciones de rendimiento, se utiliza la misma lógica de aplicación que para procesar un formulario sin opciones de rendimiento.

**Escribir el flujo de datos del formulario en el explorador web del cliente**

Una vez que el servicio Forms procesa un formulario, devuelve un flujo de datos de formulario que debe escribir en el explorador web del cliente. Cuando se escribe en el explorador web del cliente, el formulario es visible para el usuario.

**Consulte también lo siguiente**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderización de PDF forms interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Representación de Forms como HTML](/help/forms/developing/rendering-forms-html.md)

[Creación de aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Optimizar el rendimiento mediante la API de Java {#optimize-the-performance-using-the-java-api}

Representar un formulario con rendimiento optimizado mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-forms-client.jar, en la ruta de clase de su proyecto Java.

1. Creación de un objeto de API de cliente de Forms

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `FormsServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Establecer opciones de tiempo de ejecución del rendimiento

   * Cree un `PDFFormRenderSpec` usando su constructor.
   * Establezca la opción de caché de formulario invocando la variable `PDFFormRenderSpec` del objeto `setCacheEnabled` método y paso `true`.
   * Establezca la opción linealizada invocando la variable `PDFFormRenderSpec` del objeto `setLinearizedPDF` método y paso `true.`

1. Procesamiento del formulario

   Invocar el `FormsServiceClient` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo.
   * A `com.adobe.idp.Document` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un vacío `com.adobe.idp.Document` objeto.
   * A `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución para mejorar el rendimiento.
   * A `URLSpec` que contiene valores de URI necesarios para el servicio Forms.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   La variable `renderPDFForm` el método devuelve un `FormsResult` objeto que contiene un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un `javax.servlet.ServletOutputStream` objeto utilizado para enviar una secuencia de datos de formulario al explorador web del cliente.
   * Cree un `com.adobe.idp.Document` invocando el objeto `FormsResult` objeto ‘s `getOutputContent` método.
   * Cree un `java.io.InputStream` invocando el objeto `com.adobe.idp.Document` del objeto `getInputStream` método.
   * Cree una matriz de bytes y rellénela con la secuencia de datos del formulario invocando la variable `InputStream` del objeto `read`y pasando la matriz de bytes como argumento.
   * Invocar el `javax.servlet.ServletOutputStream` del objeto `write` método para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes a la `write` método.

**Consulte también lo siguiente**

[Inicio rápido (modo SOAP): Optimización del rendimiento mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Optimizar el rendimiento mediante la API de servicio web {#optimize-the-performance-using-the-web-service-api}

Representar un formulario con un rendimiento optimizado mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases proxy de Java en la ruta de clase.

1. Creación de un objeto de API de cliente de Forms

   Cree un `FormsService` y establezca los valores de autenticación.

1. Establecer opciones de tiempo de ejecución del rendimiento

   * Cree un `PDFFormRenderSpec` usando su constructor.
   * Establezca la opción de caché de formulario invocando la variable `PDFFormRenderSpec` del objeto `setCacheEnabled` y pasar a verdadero.
   * Configure la opción independiente invocando la variable `PDFFormRenderSpec` del objeto `setStandAlone` y pasar a verdadero.
   * Establezca la opción linealizada invocando la variable `PDFFormRenderSpec` del objeto `setLinearizedPDF` y pasar a verdadero.

1. Procesamiento del formulario

   Invocar el `FormsService` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo.
   * A `BLOB` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`.
   * A `PDFFormRenderSpecc` que almacena opciones en tiempo de ejecución.
   * A `URLSpec` que contiene valores de URI necesarios para el servicio Forms.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un vacío `com.adobe.idp.services.holders.BLOBHolder` objeto que rellena el método . Se utiliza para almacenar el formulario de PDF procesado.
   * Un vacío `javax.xml.rpc.holders.LongHolder` objeto que rellena el método . (Este argumento almacenará el número de páginas del formulario).
   * Un vacío `javax.xml.rpc.holders.StringHolder` objeto que rellena el método . (Este argumento almacenará el valor de configuración regional).
   * Un vacío `com.adobe.idp.services.holders.FormsResultHolder` que contendrá los resultados de esta operación.

   La variable `renderPDFForm` rellena el `com.adobe.idp.services.holders.FormsResultHolder` objeto que se pasa como el último valor de argumento con un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un `FormResult` obteniendo el valor de `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value` miembro de datos.
   * Cree un `javax.servlet.ServletOutputStream` objeto utilizado para enviar una secuencia de datos de formulario al explorador web del cliente.
   * Cree un `BLOB` objeto que contiene datos de formulario invocando la variable `FormsResult` del objeto `getOutputContent` método.
   * Cree una matriz de bytes y rellénela invocando la variable `BLOB` del objeto `getBinaryData` método. Esta tarea asigna el contenido de la variable `FormsResult` a la matriz de bytes.
   * Invocar el `javax.servlet.http.HttpServletResponse` del objeto `write` método para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes a la `write` método.

**Consulte también lo siguiente**

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
