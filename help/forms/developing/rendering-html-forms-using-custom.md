---
title: Representación de Forms de HTML mediante archivos CSS personalizados
seo-title: Rendering HTML Forms Using Custom CSS Files
description: Utilice el servicio Forms para hacer referencia a archivos CSS personalizados para procesar formularios HTML en respuesta a una solicitud HTTP de un explorador web. Puede procesar un formulario de HTML que utilice un archivo CSS mediante la API de Java y la API de servicio web.
seo-description: Use the Forms service to refer to custom CSS files to render HTML forms in response to an HTTP request from a web browser. You can render an HTML form that uses a CSS file using the Java API and Web Service API.
uuid: a44e96f1-001d-48a2-8c96-15cb9d0c71b3
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8fe7c072-7df0-44b7-92d0-bf39dc1e688a
role: Developer
exl-id: 5fa385a7-f030-4c0c-8938-0991d02ef361
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1688'
ht-degree: 0%

---

# Representación de Forms de HTML mediante archivos CSS personalizados {#rendering-html-forms-using-custom-css-files}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

El servicio Forms procesa formularios HTML en respuesta a una solicitud HTTP de un explorador web. Al procesar un formulario de HTML, el servicio de Forms puede hacer referencia a un archivo CSS personalizado. Puede crear un archivo CSS personalizado para satisfacer los requisitos empresariales y hacer referencia a ese archivo CSS cuando utilice el servicio Forms para procesar formularios HTML.

El servicio Forms analiza silenciosamente el archivo CSS personalizado. Es decir, el servicio de Forms no informa de errores que se puedan encontrar si el archivo CSS personalizado no cumple con los estándares CSS. En este caso, el servicio de Forms ignora el estilo y continúa con los estilos restantes ubicados en el archivo CSS.

La siguiente lista especifica los estilos compatibles con un archivo CSS personalizado:

* **Pares de estilo selector de nivel de clase**: Si está presente en un archivo CSS personalizado, se utilizan selectores utilizados en el formulario de HTML como estilos de clase. Los estilos de clase no utilizados se ignoran.
* **Pares de estilo selector de nivel de identificador**: Todos los estilos de identificador se utilizan si se utilizan en el formulario de HTML.
* **Pares de estilo selector de nivel de elemento**: Todos los estilos de elemento se utilizan si se utilizan en el formulario de HTML.
* **Prioridad de estilo**: La prioridad de estilo (como importante) es compatible y se puede utilizar en un archivo CSS personalizado.
* **Tipo de medio**: Se pueden ajustar uno o más pares de estilo selector en el estilo @media para definir el tipo de medio. El servicio Forms no comprueba si se admite el tipo de medio especificado. El tipo de medio especificado en el archivo CSS personalizado se combina en el formulario de HTML.

Puede recuperar un archivo CSS de ejemplo utilizando la aplicación FormsIVS. Cargue el formulario, selecciónelo en la página Probar diseño de formulario y haga clic en Generar CSS. No es necesario que configure el tipo de transformación del HTML antes de hacer clic en el botón. A continuación, seleccione Guardar. Puede editar este archivo CSS para satisfacer los requisitos empresariales.

>[!NOTE]
>
>Antes de procesar un formulario de HTML que utilice un archivo CSS personalizado, es importante que tenga una comprensión sólida de la renderización de formularios de HTML. (Consulte [Representación de Forms como HTML](/help/forms/developing/rendering-forms-html.md).)

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para procesar un formulario de HTML que utilice un archivo CSS, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API Java de Forms.
1. Haga referencia al archivo CSS.
1. Representar un formulario de HTML.
1. Escriba el flujo de datos del formulario en el explorador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API Java de Forms**

Para poder realizar mediante programación una operación admitida por el servicio Forms, debe crear un objeto cliente de Forms.

**Hacer referencia al archivo CSS**

Para procesar un formulario de HTML que utilice un archivo CSS personalizado, asegúrese de hacer referencia a un archivo CSS existente.

**Representar un formulario de HTML**

Para procesar un formulario de HTML, debe especificar un diseño de formulario creado en Designer y guardado como archivo XDP. También debe seleccionar un tipo de transformación de HTML. Por ejemplo, puede especificar el tipo de transformación del HTML que representa un HTML dinámico para Internet Explorer 5.0 o posterior.

La renderización de un formulario HTML también requiere valores, como valores de URI necesarios para representar otros tipos de formulario.

**Escribir el flujo de datos del formulario en el explorador web del cliente**

Cuando el servicio Forms procesa un formulario de HTML, devuelve un flujo de datos de formulario que debe escribir en el explorador web del cliente para que el usuario pueda ver el formulario del HTML.

**Consulte también lo siguiente**

[Representar un formulario de HTML que utiliza un archivo CSS mediante la API de Java](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderización de PDF forms interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Representación de Forms como HTML](/help/forms/developing/rendering-forms-html.md)

[Creación de aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Representar un formulario de HTML que utiliza un archivo CSS mediante la API de Java {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

Representar un formulario de HTML que utilice un archivo CSS personalizado mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-forms-client.jar, en la ruta de clase de su proyecto Java.

1. Creación de un objeto de API Java de Forms

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `FormsServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Hacer referencia al archivo CSS

   * Cree un `HTMLRenderSpec` usando su constructor.
   * Para procesar el formulario del HTML que utiliza un archivo CSS personalizado, invoque la función `HTMLRenderSpec` del objeto `setCustomCSSURI` y pase un valor de cadena que especifique la ubicación y el nombre del archivo CSS.

1. Representar un formulario de HTML

   Invocar el `FormsServiceClient` del objeto `(Deprecated) (Deprecated) renderHTMLForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valor enum que especifica el tipo de preferencia de HTML. Por ejemplo, para procesar un formulario de HTML compatible con dynamic HTML para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un vacío `com.adobe.idp.Document` objeto.
   * La variable `HTMLRenderSpec` que almacena las opciones de tiempo de ejecución del HTML.
   * Un valor de cadena que especifica la variable `HTTP_USER_AGENT` valor de encabezado, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` objeto que almacena valores de URI necesarios para procesar un formulario de HTML.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   La variable `(Deprecated) renderHTMLForm` el método devuelve un `FormsResult` objeto que contiene un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un `com.adobe.idp.Document` invocando el objeto `FormsResult` objeto ‘s `getOutputContent` método.
   * Obtenga el tipo de contenido de la variable `com.adobe.idp.Document` invocando su `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasar el tipo de contenido de la variable `com.adobe.idp.Document` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos del formulario en el explorador web del cliente invocando la variable `javax.servlet.h\ttp.HttpServletResponse` del objeto `getOutputStream` método.
   * Cree un `java.io.InputStream` invocando el objeto `com.adobe.idp.Document` del objeto `getInputStream` método.
   * Cree una matriz de bytes y rellénela con la secuencia de datos del formulario invocando la variable `InputStream` del objeto `read` y pasando la matriz de bytes como argumento.
   * Invocar el `javax.servlet.ServletOutputStream` del objeto `write` método para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes a la `write` método.

**Consulte también lo siguiente**

[Representación de Forms de HTML mediante archivos CSS personalizados](#rendering-html-forms-using-custom-css-files)

[Inicio rápido (modo SOAP): Representación de un formulario de HTML que utiliza un archivo CSS mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Representar un formulario de HTML que utiliza un archivo CSS mediante la API de servicio web {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

Representar un formulario de HTML que utiliza un archivo CSS personalizado mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases proxy de Java en la ruta de clase.

1. Creación de un objeto de API Java de Forms

   Cree un `FormsService` y establezca los valores de autenticación.

1. Hacer referencia al archivo CSS

   * Cree un `HTMLRenderSpec` usando su constructor.
   * Para procesar el formulario del HTML que utiliza un archivo CSS personalizado, invoque la función `HTMLRenderSpec` del objeto `setCustomCSSURI` y pase un valor de cadena que especifique la ubicación y el nombre del archivo CSS.

1. Representar un formulario de HTML

   Invocar el `FormsService` del objeto `(Deprecated) renderHTMLForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valor enum que especifica el tipo de preferencia de HTML. Por ejemplo, para procesar un formulario de HTML compatible con dynamic HTML para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * A `BLOB` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`. (Consulte [Rellenado previo de Forms con diseños flexibles](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * La variable `HTMLRenderSpec` que almacena las opciones de tiempo de ejecución del HTML.
   * Un valor de cadena que especifica la variable `HTTP_USER_AGENT` valor de encabezado, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Puede pasar una cadena vacía si no desea establecer este valor.
   * A `URLSpec` objeto que almacena valores de URI necesarios para procesar un formulario de HTML.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un vacío `com.adobe.idp.services.holders.BLOBHolder` objeto que rellena el `(Deprecated) renderHTMLForm` método. Este valor de parámetro almacena el formulario procesado.
   * Un vacío `com.adobe.idp.services.holders.BLOBHolder` objeto que rellena el `(Deprecated) renderHTMLForm` método. Este parámetro almacena los datos XML de salida.
   * Un vacío `javax.xml.rpc.holders.LongHolder` objeto que rellena el `(Deprecated) renderHTMLForm` método. Este argumento almacena el número de páginas del formulario.
   * Un vacío `javax.xml.rpc.holders.StringHolder` objeto que rellena el `(Deprecated) renderHTMLForm` método. Este argumento almacena el valor de configuración regional.
   * Un vacío `javax.xml.rpc.holders.StringHolder` objeto que rellena el `(Deprecated) renderHTMLForm` método. Este argumento almacena el valor de renderización del HTML que se utiliza.
   * Un vacío `com.adobe.idp.services.holders.FormsResultHolder` que contendrá los resultados de esta operación.

   La variable `(Deprecated) renderHTMLForm` rellena el `com.adobe.idp.services.holders.FormsResultHolder` objeto que se pasa como el último valor de argumento con un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un `FormResult` obteniendo el valor de `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value` miembro de datos.
   * Cree un `BLOB` objeto que contiene datos de formulario invocando la variable `FormsResult` del objeto `getOutputContent` método.
   * Obtenga el tipo de contenido de la variable `BLOB` invocando su `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasar el tipo de contenido de la variable `BLOB` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos del formulario en el explorador web del cliente invocando la variable `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Cree una matriz de bytes y rellénela invocando la variable `BLOB` del objeto `getBinaryData` método. Esta tarea asigna el contenido de la variable `FormsResult` a la matriz de bytes.
   * Invocar el `javax.servlet.http.HttpServletResponse` del objeto `write` método para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes a la `write` método.

**Consulte también lo siguiente**

[Representación de Forms de HTML mediante archivos CSS personalizados](#rendering-html-forms-using-custom-css-files)

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
