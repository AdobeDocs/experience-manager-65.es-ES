---
title: Representación de HTML en Forms mediante archivos CSS personalizados
seo-title: Representación de HTML en Forms mediante archivos CSS personalizados
description: Utilice el servicio Forms para hacer referencia a archivos CSS personalizados para procesar formularios HTML en respuesta a una solicitud HTTP de un explorador Web. Puede procesar un formulario HTML que utilice un archivo CSS mediante la API de Java y la API de servicio Web.
seo-description: Utilice el servicio Forms para hacer referencia a archivos CSS personalizados para procesar formularios HTML en respuesta a una solicitud HTTP de un explorador Web. Puede procesar un formulario HTML que utilice un archivo CSS mediante la API de Java y la API de servicio Web.
uuid: a44e96f1-001d-48a2-8c96-15cb9d0c71b3
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8fe7c072-7df0-44b7-92d0-bf39dc1e688a
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1724'
ht-degree: 0%

---


# Representación de HTML Forms mediante archivos CSS personalizados {#rendering-html-forms-using-custom-css-files}

El servicio Forms procesa formularios HTML en respuesta a una solicitud HTTP procedente de un navegador web. Al procesar un formulario HTML, el servicio de Forms puede hacer referencia a un archivo CSS personalizado. Puede crear un archivo CSS personalizado para cumplir los requisitos comerciales y hacer referencia a ese archivo CSS cuando utilice el servicio Forms para procesar formularios HTML.

El servicio Forms analiza en silencio el archivo CSS personalizado. Es decir, el servicio de Forms no informa de los errores que puedan producirse si el archivo CSS personalizado no cumple con los estándares CSS. En este caso, el servicio Forms ignora el estilo y continúa con el resto de estilos que se encuentran en el archivo CSS.

La siguiente lista especifica los estilos que se admiten en un archivo CSS personalizado:

* **Pares** de estilo selector de nivel de clase: Si está presente en un archivo CSS personalizado, se utilizan selectores utilizados en el formulario HTML como estilos de clase. Se omiten los estilos de clase no utilizados.
* **Par** de estilo selector de nivel de identificador: Todos los estilos de identificador se utilizan si se utilizan en el formulario HTML.
* **Par** de estilo selector de nivel de elemento: Todos los estilos de elemento se utilizan si se utilizan en el formulario HTML.
* **Prioridad** de estilo: Se admite la prioridad de estilo (como importante) y se puede utilizar en un archivo CSS personalizado.
* **Tipo** de medio: Se pueden ajustar uno o varios pares de estilo selector en el estilo @media para definir el tipo de papel. El servicio Forms no comprueba si se admite el tipo de medio especificado. El tipo de medio especificado en el archivo CSS personalizado se combina en el formulario HTML.

Puede recuperar un archivo CSS de ejemplo mediante la aplicación FormsIVS. Cargue el formulario, selecciónelo en la página Probar diseño de formulario y haga clic en Generar CSS. No es necesario definir el tipo de transformación HTML antes de hacer clic en el botón. A continuación, seleccione Guardar. Puede editar este archivo CSS para satisfacer los requisitos comerciales.

>[!NOTE]
>
>Antes de procesar un formulario HTML que utilice un archivo CSS personalizado, es importante que tenga una sólida comprensión del procesamiento de formularios HTML. (Consulte [Representación de Forms como HTML](/help/forms/developing/rendering-forms-html.md)).

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para procesar un formulario HTML que utilice un archivo CSS, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API Java de Forms.
1. Haga referencia al archivo CSS.
1. Representar un formulario HTML.
1. Escriba la secuencia de datos del formulario en el navegador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Forms Java**

Para poder realizar mediante programación una operación admitida por el servicio Forms, debe crear un objeto de cliente de Forms.

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

[Inicios rápidos de la API de servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Representación de PDF forms interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Representación de Forms como HTML](/help/forms/developing/rendering-forms-html.md)

[Creación de Aplicaciones web que procesan Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Representar un formulario HTML que utiliza un archivo CSS mediante la API de Java {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

Representar un formulario HTML que utiliza un archivo CSS personalizado mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clases del proyecto Java.

1. Creación de un objeto de API de Forms Java

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `FormsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Hacer referencia al archivo CSS

   * Cree un objeto `HTMLRenderSpec` utilizando su constructor.
   * Para procesar el formulario HTML que utiliza un archivo CSS personalizado, invoque el método `HTMLRenderSpec` del objeto `setCustomCSSURI` y pase un valor de cadena que especifique la ubicación y el nombre del archivo CSS.

1. Representar un formulario HTML

   Invoque el método `FormsServiceClient` del objeto `(Deprecated) (Deprecated) renderHTMLForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un valor de enumeración `TransformTo` que especifica el tipo de preferencia HTML. Por ejemplo, para procesar un formulario HTML compatible con HTML dinámico para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * Un objeto `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un objeto vacío `com.adobe.idp.Document`.
   * El objeto `HTMLRenderSpec` que almacena las opciones de tiempo de ejecución HTML.
   * Un valor de cadena que especifica el valor del encabezado `HTTP_USER_AGENT`, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Un objeto `URLSpec` que almacena valores URI necesarios para procesar un formulario HTML.
   * Objeto `java.util.HashMap` que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El método `(Deprecated) renderHTMLForm` devuelve un objeto `FormsResult` que contiene una secuencia de datos de formulario que debe escribirse en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un objeto `com.adobe.idp.Document` invocando el método `FormsResult` del objeto ‘s `getOutputContent`.
   * Obtenga el tipo de contenido del objeto `com.adobe.idp.Document` invocando su método `getContentType`.
   * Configure el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `com.adobe.idp.Document`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el método `javax.servlet.h\ttp.HttpServletResponse` del objeto `getOutputStream`.
   * Cree un objeto `java.io.InputStream` invocando el método `com.adobe.idp.Document` del objeto `getInputStream`.
   * Cree una matriz de bytes y rellénela con la secuencia de datos del formulario invocando el método `InputStream` del objeto `read` y pasando la matriz de bytes como argumento.
   * Invoque el método `javax.servlet.ServletOutputStream` del objeto `write` para enviar la secuencia de datos del formulario al explorador Web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Representación de HTML en Forms mediante archivos CSS personalizados](#rendering-html-forms-using-custom-css-files)

[Inicio rápido (modo SOAP): Representación de un formulario HTML que utiliza un archivo CSS mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Representar un formulario HTML que utiliza un archivo CSS mediante la API de servicio Web {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

Representar un formulario HTML que utiliza un archivo CSS personalizado mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases proxy de Java que consuman el WSDL del servicio de Forms.
   * Incluya las clases proxy de Java en la ruta de clases.

1. Creación de un objeto de API de Forms Java

   Cree un objeto `FormsService` y defina los valores de autenticación.

1. Hacer referencia al archivo CSS

   * Cree un objeto `HTMLRenderSpec` utilizando su constructor.
   * Para procesar el formulario HTML que utiliza un archivo CSS personalizado, invoque el método `HTMLRenderSpec` del objeto `setCustomCSSURI` y pase un valor de cadena que especifique la ubicación y el nombre del archivo CSS.

1. Representar un formulario HTML

   Invoque el método `FormsService` del objeto `(Deprecated) renderHTMLForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un valor de enumeración `TransformTo` que especifica el tipo de preferencia HTML. Por ejemplo, para procesar un formulario HTML compatible con HTML dinámico para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * Un objeto `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`. (Consulte [Rellenado previo de Forms con diseños de posición variable](/help/forms/developing/prepopulating-forms-flowable-layouts.md)).
   * El objeto `HTMLRenderSpec` que almacena las opciones de tiempo de ejecución HTML.
   * Un valor de cadena que especifica el valor del encabezado `HTTP_USER_AGENT`, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Puede pasar una cadena vacía si no desea establecer este valor.
   * Un objeto `URLSpec` que almacena valores URI necesarios para procesar un formulario HTML.
   * Objeto `java.util.HashMap` que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un objeto vacío `com.adobe.idp.services.holders.BLOBHolder` que se rellena con el método `(Deprecated) renderHTMLForm`. Este valor de parámetro almacena el formulario procesado.
   * Un objeto vacío `com.adobe.idp.services.holders.BLOBHolder` que se rellena con el método `(Deprecated) renderHTMLForm`. Este parámetro almacena los datos XML de salida.
   * Un objeto vacío `javax.xml.rpc.holders.LongHolder` que se rellena con el método `(Deprecated) renderHTMLForm`. Este argumento almacena el número de páginas del formulario.
   * Un objeto vacío `javax.xml.rpc.holders.StringHolder` que se rellena con el método `(Deprecated) renderHTMLForm`. Este argumento almacena el valor de configuración regional.
   * Un objeto vacío `javax.xml.rpc.holders.StringHolder` que se rellena con el método `(Deprecated) renderHTMLForm`. Este argumento almacena el valor de representación HTML que se utiliza.
   * Un objeto vacío `com.adobe.idp.services.holders.FormsResultHolder` que contendrá los resultados de esta operación.

   El método `(Deprecated) renderHTMLForm` rellena el objeto `com.adobe.idp.services.holders.FormsResultHolder` que se pasa como el último valor de argumento con una secuencia de datos de formulario que debe escribirse en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un objeto `FormResult` obteniendo el valor del miembro de datos `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value`.
   * Cree un objeto `BLOB` que contenga datos de formulario invocando el método `FormsResult` del objeto `getOutputContent`.
   * Obtenga el tipo de contenido del objeto `BLOB` invocando su método `getContentType`.
   * Configure el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `BLOB`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el método `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream`.
   * Cree una matriz de bytes y rellénela invocando el método `BLOB` del objeto `getBinaryData`. Esta tarea asigna el contenido del objeto `FormsResult` a la matriz de bytes.
   * Invoque el método `javax.servlet.http.HttpServletResponse` del objeto `write` para enviar la secuencia de datos del formulario al explorador Web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Representación de HTML en Forms mediante archivos CSS personalizados](#rendering-html-forms-using-custom-css-files)

[Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
