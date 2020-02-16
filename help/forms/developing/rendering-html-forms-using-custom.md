---
title: Representación de formularios HTML mediante archivos CSS personalizados
seo-title: Representación de formularios HTML mediante archivos CSS personalizados
description: nulo
seo-description: nulo
uuid: a44e96f1-001d-48a2-8c96-15cb9d0c71b3
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8fe7c072-7df0-44b7-92d0-bf39dc1e688a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Representación de formularios HTML mediante archivos CSS personalizados {#rendering-html-forms-using-custom-css-files}

El servicio Forms procesa formularios HTML en respuesta a una solicitud HTTP de un explorador web. Al procesar un formulario HTML, el servicio Forms puede hacer referencia a un archivo CSS personalizado. Puede crear un archivo CSS personalizado para cumplir los requisitos comerciales y hacer referencia a dicho archivo CSS cuando utilice el servicio Forms para procesar formularios HTML.

El servicio Forms analiza en silencio el archivo CSS personalizado. Es decir, el servicio Forms no informa de los errores que se pueden encontrar si el archivo CSS personalizado no cumple con los estándares CSS. En este caso, el servicio Forms ignora el estilo y continúa con los estilos restantes que se encuentran en el archivo CSS.

La siguiente lista especifica los estilos que se admiten en un archivo CSS personalizado:

* **Pares** de estilo selector de nivel de clase: Si está presente en un archivo CSS personalizado, se utilizan selectores utilizados en el formulario HTML como estilos de clase. Se omiten los estilos de clase no utilizados.
* **Par** de estilo selector de nivel de identificador: Todos los estilos de identificador se utilizan si se utilizan en el formulario HTML.
* **Par** de estilo selector de nivel de elemento: Todos los estilos de elemento se utilizan si se utilizan en el formulario HTML.
* **Prioridad** de estilo: Se admite la prioridad de estilo (como importante) y se puede utilizar en un archivo CSS personalizado.
* **Tipo** de medio: Se pueden ajustar uno o varios pares de estilo selector en el estilo @media para definir el tipo de papel. El servicio Forms no comprueba si se admite el tipo de medio especificado. El tipo de medio especificado en el archivo CSS personalizado se combina en el formulario HTML.

Puede recuperar un archivo CSS de ejemplo mediante la aplicación FormsIVS. Cargue el formulario, selecciónelo en la página Probar diseño de formulario y haga clic en Generar CSS. No es necesario definir el tipo de transformación HTML antes de hacer clic en el botón. A continuación, seleccione Guardar. Puede editar este archivo CSS para satisfacer los requisitos comerciales.

>[!NOTE]
>
>Antes de procesar un formulario HTML que utilice un archivo CSS personalizado, es importante que tenga una sólida comprensión del procesamiento de formularios HTML. (Consulte [Representación de formularios como HTML](/help/forms/developing/rendering-forms-html.md)).

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para procesar un formulario HTML que utilice un archivo CSS, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de Java de Forms.
1. Haga referencia al archivo CSS.
1. Representar un formulario HTML.
1. Escriba la secuencia de datos del formulario en el navegador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Java de Forms**

Para poder realizar mediante programación una operación admitida por el servicio Forms, debe crear un objeto de cliente Forms.

**Hacer referencia al archivo CSS**

Para procesar un formulario HTML que utilice un archivo CSS personalizado, asegúrese de que hace referencia a un archivo CSS existente.

**Representar un formulario HTML**

Para procesar un formulario HTML, debe especificar un diseño de formulario creado en Designer y guardado como archivo XDP. También debe seleccionar un tipo de transformación HTML. Por ejemplo, puede especificar el tipo de transformación HTML que procesa un HTML dinámico para Internet Explorer 5.0 o posterior.

La representación de un formulario HTML también requiere valores, como valores URI necesarios para representar otros tipos de formulario.

**Escribir el flujo de datos del formulario en el navegador web del cliente**

Cuando el servicio Forms procesa un formulario HTML, devuelve una secuencia de datos de formulario que debe escribir en el navegador web del cliente para que el usuario pueda ver el formulario HTML.

**Consulte también**

[Representar un formulario HTML que utiliza un archivo CSS mediante la API de Java](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de formularios](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Representación de formularios PDF interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Representación de formularios como HTML](/help/forms/developing/rendering-forms-html.md)

[Creación de aplicaciones Web que procesan formularios](/help/forms/developing/creating-web-applications-renders-forms.md)

## Representar un formulario HTML que utiliza un archivo CSS mediante la API de Java {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

Representar un formulario HTML que utiliza un archivo CSS personalizado mediante la API de formularios (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clases del proyecto Java.

1. Creación de un objeto de API de Java de Forms

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `FormsServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Hacer referencia al archivo CSS

   * Cree un `HTMLRenderSpec` objeto con su constructor.
   * Para procesar el formulario HTML que utiliza un archivo CSS personalizado, invoque el `HTMLRenderSpec` método del `setCustomCSSURI` objeto y pase un valor de cadena que especifique la ubicación y el nombre del archivo CSS.

1. Representar un formulario HTML

   Invoque el `FormsServiceClient` método del `(Deprecated) (Deprecated) renderHTMLForm` objeto y pase los valores siguientes:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un valor `TransformTo` enum que especifica el tipo de preferencia HTML. Por ejemplo, para procesar un formulario HTML compatible con HTML dinámico para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * Un `com.adobe.idp.Document` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un `com.adobe.idp.Document` objeto vacío.
   * El `HTMLRenderSpec` objeto que almacena las opciones de tiempo de ejecución HTML.
   * Un valor de cadena que especifica el valor del `HTTP_USER_AGENT` encabezado, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Un `URLSpec` objeto que almacena valores URI necesarios para procesar un formulario HTML.
   * Un `java.util.HashMap` objeto que almacena archivos adjuntos. Se trata de un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   El `(Deprecated) renderHTMLForm` método devuelve un `FormsResult` objeto que contiene una secuencia de datos de formulario que se debe escribir en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un `com.adobe.idp.Document` objeto invocando el `FormsResult` método ‘s `getOutputContent` .
   * Obtenga el tipo de contenido del `com.adobe.idp.Document` objeto invocando su `getContentType` método.
   * Defina el tipo de contenido del `javax.servlet.http.HttpServletResponse` objeto invocando su `setContentType` método y pasando el tipo de contenido del `com.adobe.idp.Document` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el `javax.servlet.h\ttp.HttpServletResponse` método `getOutputStream` del objeto.
   * Cree un `java.io.InputStream` objeto invocando el `com.adobe.idp.Document` método `getInputStream` del objeto.
   * Cree una matriz de bytes y rellénela con la secuencia de datos del formulario invocando el `InputStream` método del `read` objeto y pasando la matriz de bytes como argumento.
   * Invoque el `javax.servlet.ServletOutputStream` método del `write` objeto para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al `write` método .

**Consulte también**

[Representación de formularios HTML mediante archivos CSS personalizados](#rendering-html-forms-using-custom-css-files)

[Inicio rápido (modo SOAP): Representación de un formulario HTML que utiliza un archivo CSS mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Representar un formulario HTML que utiliza un archivo CSS mediante la API de servicio web {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

Representar un formulario HTML que utiliza un archivo CSS personalizado mediante la API de formularios (servicio web):

1. Incluir archivos de proyecto

   * Cree clases proxy de Java que consuman el WSDL del servicio Forms.
   * Incluya las clases proxy de Java en la ruta de clases.

1. Creación de un objeto de API de Java de Forms

   Cree un `FormsService` objeto y defina los valores de autenticación.

1. Hacer referencia al archivo CSS

   * Cree un `HTMLRenderSpec` objeto con su constructor.
   * Para procesar el formulario HTML que utiliza un archivo CSS personalizado, invoque el `HTMLRenderSpec` método del `setCustomCSSURI` objeto y pase un valor de cadena que especifique la ubicación y el nombre del archivo CSS.

1. Representar un formulario HTML

   Invoque el `FormsService` método del `(Deprecated) renderHTMLForm` objeto y pase los valores siguientes:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un valor `TransformTo` enum que especifica el tipo de preferencia HTML. Por ejemplo, para procesar un formulario HTML compatible con HTML dinámico para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * Un `BLOB` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`. (Consulte [Rellenado previo de formularios con diseños]de posición variable (/help/forms/develop/renderizado-formularios cumplimentación previa de formularios-presentación-presentación-presentación-formularios-rellenado previo.md#prerellating-forms-with-flowable-layouts).
   * El `HTMLRenderSpec` objeto que almacena las opciones de tiempo de ejecución HTML.
   * Un valor de cadena que especifica el valor del `HTTP_USER_AGENT` encabezado, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Puede pasar una cadena vacía si no desea establecer este valor.
   * Un `URLSpec` objeto que almacena valores URI necesarios para procesar un formulario HTML.
   * Un `java.util.HashMap` objeto que almacena archivos adjuntos. Se trata de un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Objeto vacío `com.adobe.idp.services.holders.BLOBHolder` que se rellena con el `(Deprecated) renderHTMLForm` método . Este valor de parámetro almacena el formulario procesado.
   * Objeto vacío `com.adobe.idp.services.holders.BLOBHolder` que se rellena con el `(Deprecated) renderHTMLForm` método . Este parámetro almacena los datos XML de salida.
   * Objeto vacío `javax.xml.rpc.holders.LongHolder` que se rellena con el `(Deprecated) renderHTMLForm` método . Este argumento almacena el número de páginas del formulario.
   * Objeto vacío `javax.xml.rpc.holders.StringHolder` que se rellena con el `(Deprecated) renderHTMLForm` método . Este argumento almacena el valor de configuración regional.
   * Objeto vacío `javax.xml.rpc.holders.StringHolder` que se rellena con el `(Deprecated) renderHTMLForm` método . Este argumento almacena el valor de representación HTML que se utiliza.
   * Un `com.adobe.idp.services.holders.FormsResultHolder` objeto vacío que contendrá los resultados de esta operación.
   El `(Deprecated) renderHTMLForm` método rellena el `com.adobe.idp.services.holders.FormsResultHolder` objeto que se pasa como el último valor de argumento con una secuencia de datos de formulario que se debe escribir en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un `FormResult` objeto obteniendo el valor del `com.adobe.idp.services.holders.FormsResultHolder` miembro de `value` datos del objeto.
   * Cree un `BLOB` objeto que contenga datos de formulario invocando el `FormsResult` método `getOutputContent` del objeto.
   * Obtenga el tipo de contenido del `BLOB` objeto invocando su `getContentType` método.
   * Defina el tipo de contenido del `javax.servlet.http.HttpServletResponse` objeto invocando su `setContentType` método y pasando el tipo de contenido del `BLOB` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el `javax.servlet.http.HttpServletResponse` método `getOutputStream` del objeto.
   * Cree una matriz de bytes y rellénela invocando el `BLOB` método `getBinaryData` del objeto. Esta tarea asigna el contenido del `FormsResult` objeto a la matriz de bytes.
   * Invoque el `javax.servlet.http.HttpServletResponse` método del `write` objeto para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al `write` método .

**Consulte también**

[Representación de formularios HTML mediante archivos CSS personalizados](#rendering-html-forms-using-custom-css-files)

[Invocación de formularios AEM con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
