---
title: Optimizar el rendimiento del servicio de Forms
description: Establezca opciones en tiempo de ejecución al procesar un formulario y almacenar archivos XDP en el repositorio para optimizar el rendimiento del servicio de Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 5a746c6c-bf6e-4b25-ba7c-a35edb1f55f3
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 1%

---

# Optimización del rendimiento del servicio de Forms {#optimizing-the-performance-of-theforms-service}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

## Optimización del rendimiento del servicio de Forms {#optimizing-the-performance-of-the-forms-service}

Al procesar un formulario, puede establecer opciones en tiempo de ejecución que optimicen el rendimiento del servicio de Forms. Otra tarea que puede realizar para mejorar el rendimiento del servicio Forms es almacenar los archivos XDP en el repositorio. Sin embargo, esta sección no describe cómo realizar esta tarea. (Consulte [Invocar un servicio mediante una biblioteca de cliente Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library).)

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para optimizar el rendimiento del servicio Forms al procesar un formulario, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Establecer opciones de rendimiento en tiempo de ejecución.
1. Procese el formulario.
1. Escriba el flujo de datos del formulario en el explorador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API de cliente de Forms**

Para poder realizar mediante programación una operación de API de cliente de servicio de Forms, debe crear un cliente de servicio de Forms. Si utiliza la API de Java, cree un `FormsServiceClient` objeto. Si utiliza la API del servicio web de Forms, cree un `FormsService` objeto.

**Establecer opciones de rendimiento en tiempo de ejecución**

Puede establecer las siguientes opciones de tiempo de ejecución de rendimiento para mejorar el rendimiento del servicio de Forms:

* **Almacenamiento en caché de formularios**: puede almacenar en caché un formulario que se represente como PDF en la caché del servidor. Cada formulario se almacena en caché después de generarse por primera vez. En un procesamiento posterior, si el formulario en caché es más reciente que la marca de tiempo del diseño de formulario, el formulario se recuperará de la caché. Al almacenar en caché los formularios, se mejora el rendimiento del servicio de Forms porque no tiene que recuperar el diseño de formulario de un repositorio.
* Las guías del formulario (obsoletas) pueden tardar más en procesarse que otros tipos de transformación. Se recomienda almacenar en caché las guías del formulario (obsoletas) para mejorar el rendimiento.
* **Opción independiente**: Si no requiere que el servicio Forms realice cálculos en el lado del servidor, puede establecer la opción Independiente en `true`, lo que hace que los formularios se procesen sin información de estado. La información de estado es necesaria si desea procesar un formulario interactivo para un usuario final que luego introduzca información en el formulario y lo envíe de nuevo al servicio de Forms. A continuación, el servicio Forms realiza una operación de cálculo y devuelve el formulario al usuario con los resultados mostrados en el formulario. Si se devuelve un formulario sin información de estado al servicio Forms, solo estarán disponibles los datos XML y no se realizarán cálculos en el servidor.
* **PDF linealizado**: un archivo PDF linealizado está organizado para permitir un acceso incremental eficiente en un entorno de red. El archivo de PDF es un PDF válido en todos los aspectos y es compatible con todos los visores existentes y otras aplicaciones de PDF. Es decir, se puede ver un PDF linealizado mientras se sigue descargando.
* Esta opción no mejora el rendimiento cuando se procesa un formulario de PDF en el cliente.
* **Opción GuideRSL**: permite la generación de la Guía de formularios (obsoleta) mediante bibliotecas compartidas en tiempo de ejecución. Esto significa que la primera solicitud descargará un archivo de SWF más pequeño, además de bibliotecas compartidas más grandes almacenadas en la caché del explorador. Para obtener más información, consulte RSL en la documentación de Flex.
* También puede mejorar el rendimiento del servicio Forms al procesar un formulario en el cliente. (Consulte [Procesar Forms en el cliente](/help/forms/developing/rendering-forms-client.md).)

**Procesar el formulario**

Para procesar el formulario después de establecer las opciones de rendimiento, utilice la misma lógica de aplicación que para procesar un formulario sin opciones de rendimiento.

**Escribir el flujo de datos del formulario en el explorador web del cliente**

Una vez que el servicio Forms procesa un formulario, devuelve un flujo de datos de formulario que debe escribir en el explorador web del cliente. Cuando se escribe en el explorador web del cliente, el formulario es visible para el usuario.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Procesar formularios PDF interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Procesar formularios como HTML](/help/forms/developing/rendering-forms-html.md)

[Crear aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Optimizar el rendimiento mediante la API de Java {#optimize-the-performance-using-the-java-api}

Procese un formulario con un rendimiento optimizado mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clase del proyecto Java.

1. Crear un objeto de API de cliente de Forms

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `FormsServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Establecer opciones de rendimiento en tiempo de ejecución

   * Crear un `PDFFormRenderSpec` mediante su constructor.
   * Establezca la opción de caché del formulario invocando la variable `PDFFormRenderSpec` del objeto `setCacheEnabled` método y paso `true`.
   * Establezca la opción linearizada invocando el `PDFFormRenderSpec` del objeto `setLinearizedPDF` método y paso `true.`

1. Procesar el formulario

   Invoque el `FormsServiceClient` del objeto `renderPDFForm` y pasar los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo.
   * A `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un vacío `com.adobe.idp.Document` objeto.
   * A `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución para mejorar el rendimiento.
   * A `URLSpec` que contiene valores de URI requeridos por el servicio de Forms.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El `renderPDFForm` El método devuelve un valor `FormsResult` que contiene un flujo de datos de formulario que debe escribirse en el explorador web cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Crear un `javax.servlet.ServletOutputStream` objeto utilizado para enviar un flujo de datos de formulario al explorador web del cliente.
   * Crear un `com.adobe.idp.Document` invocando el objeto de `FormsResult` objeto ‘s `getOutputContent` método.
   * Crear un `java.io.InputStream` invocando el objeto de `com.adobe.idp.Document` del objeto `getInputStream` método.
   * Cree una matriz de bytes y rellénela con el flujo de datos de formulario invocando el método `InputStream` del objeto `read`y pasando la matriz de bytes como argumento.
   * Invoque el `javax.servlet.ServletOutputStream` del objeto `write` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes a `write` método.

**Consulte también**

[Inicio rápido (modo SOAP): Optimización del rendimiento mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Optimizar el rendimiento mediante la API de servicio web {#optimize-the-performance-using-the-web-service-api}

Procese un formulario con un rendimiento optimizado mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases de proxy Java en la ruta de clase.

1. Crear un objeto de API de cliente de Forms

   Crear un `FormsService` y establezca los valores de autenticación.

1. Establecer opciones de rendimiento en tiempo de ejecución

   * Crear un `PDFFormRenderSpec` mediante su constructor.
   * Establezca la opción de caché del formulario invocando la variable `PDFFormRenderSpec` del objeto `setCacheEnabled` y pasando true.
   * Establezca la opción independiente invocando la variable `PDFFormRenderSpec` del objeto `setStandAlone` y pasando true.
   * Establezca la opción linearizada invocando el `PDFFormRenderSpec` del objeto `setLinearizedPDF` y pasando true.

1. Procesar el formulario

   Invoque el `FormsService` del objeto `renderPDFForm` y pasar los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo.
   * A `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar los datos, apruebe `null`.
   * A `PDFFormRenderSpecc` que almacena opciones en tiempo de ejecución.
   * A `URLSpec` que contiene valores de URI requeridos por el servicio de Forms.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un vacío `com.adobe.idp.services.holders.BLOBHolder` objeto que rellena el método. Se utiliza para almacenar el formulario de PDF procesado.
   * Un vacío `javax.xml.rpc.holders.LongHolder` objeto que rellena el método. (Este argumento almacenará el número de páginas en el formulario).
   * Un vacío `javax.xml.rpc.holders.StringHolder` objeto que rellena el método. (Este argumento almacenará el valor de configuración regional).
   * Un vacío `com.adobe.idp.services.holders.FormsResultHolder` que contendrá los resultados de esta operación.

   El `renderPDFForm` rellena el método `com.adobe.idp.services.holders.FormsResultHolder` que se pasa como el último valor de argumento con un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Crear un `FormResult` al obtener el valor de la variable `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value` miembro de datos.
   * Crear un `javax.servlet.ServletOutputStream` objeto utilizado para enviar un flujo de datos de formulario al explorador web del cliente.
   * Crear un `BLOB` que contiene datos de formulario invocando el `FormsResult` del objeto `getOutputContent` método.
   * Cree una matriz de bytes y rellénela invocando el método `BLOB` del objeto `getBinaryData` método. Esta tarea asigna el contenido del `FormsResult` a la matriz de bytes.
   * Invoque el `javax.servlet.http.HttpServletResponse` del objeto `write` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes a `write` método.

**Consulte también**

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
