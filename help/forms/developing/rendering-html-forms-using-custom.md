---
title: Procesar formularios HTML mediante archivos CSS personalizados
description: Utilice el servicio Forms para hacer referencia a archivos CSS personalizados y procesar formularios de HTML en respuesta a una solicitud HTTP de un explorador web. Puede procesar un formulario de HTML que utilice un archivo CSS mediante la API de Java y la API de servicio web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 5fa385a7-f030-4c0c-8938-0991d02ef361
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '1682'
ht-degree: 2%

---

# Procesar formularios HTML mediante archivos CSS personalizados {#rendering-html-forms-using-custom-css-files}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

El servicio Forms procesa formularios de HTML en respuesta a una solicitud HTTP de un explorador web. Al procesar un formulario de HTML, el servicio Forms puede hacer referencia a un archivo CSS personalizado. Puede crear un archivo CSS personalizado para satisfacer los requisitos de su empresa y hacer referencia a ese archivo CSS al utilizar el servicio Forms para procesar formularios de HTML.

El servicio Forms analiza de forma silenciosa el archivo CSS personalizado. Es decir, el servicio Forms no informa de los errores que se pueden encontrar si el archivo CSS personalizado no cumple con los estándares CSS. En este caso, el servicio Forms ignora el estilo y continúa con los estilos restantes del archivo CSS.

La siguiente lista especifica los estilos compatibles con un archivo CSS personalizado:

* **Pares de estilo selector de nivel de clase**: Si está presente en un archivo CSS personalizado, se utilizan selectores utilizados en el formulario de HTML como estilos de clase. Se omiten los estilos de clase no utilizados.
* **Pares de estilo selector de nivel de identificador**: Todos los estilos de identificador se utilizan si están en el formulario de HTML.
* **Pares de estilo selector de nivel de elemento**: Todos los estilos de elemento se utilizan si están en el formulario de HTML.
* **Prioridad de estilo**: la prioridad de estilo (como importante) es compatible y se puede utilizar en un archivo CSS personalizado.
* **Tipo de medio**: uno o más pares de estilo selector se pueden ajustar en @media estilo para definir el tipo de medio. El servicio Forms no comprueba si se admite el tipo de medio especificado. El tipo de medios especificado en el archivo CSS personalizado se combina en el formulario de HTML.

Puede recuperar un archivo CSS de ejemplo utilizando la aplicación FormsIVS. Cargue el formulario, selecciónelo en la página Diseño del formulario de prueba y haga clic en Generar CSS. No es necesario configurar el tipo de transformación del HTML antes de hacer clic en el botón. A continuación, seleccione guardar. Puede editar este archivo CSS para satisfacer sus necesidades comerciales.

>[!NOTE]
>
>Antes de procesar un formulario de HTML que utilice un archivo CSS personalizado, es importante que tenga una comprensión sólida del procesamiento de formularios de HTML. (Consulte [Representar Forms como HTML](/help/forms/developing/rendering-forms-html.md).)

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para procesar un formulario de HTML que utilice un archivo CSS, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de Java de Forms.
1. Haga referencia al archivo CSS.
1. Procesar un formulario de HTML.
1. Escriba el flujo de datos del formulario en el explorador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Java de Forms**

Para poder realizar mediante programación una operación admitida por el servicio Forms, debe crear un objeto de cliente de Forms.

**Hacer referencia al archivo CSS**

Para procesar un formulario de HTML que utilice un archivo CSS personalizado, asegúrese de hacer referencia a un archivo CSS existente.

**Procesar un formulario de HTML**

Para procesar un formulario de HTML, especifique un diseño de formulario creado en Designer y guardado como archivo XDP. Seleccione un tipo de transformación de HTML. Por ejemplo, puede especificar el tipo de transformación de HTML que procesa un HTML dinámico para Internet Explorer 5.0 o posterior.

El procesamiento de un formulario de HTML también requiere valores, como los valores de URI necesarios para procesar otros tipos de formulario.

**Escribir el flujo de datos del formulario en el explorador web del cliente**

Cuando el servicio Forms procesa un formulario de HTML, devuelve un flujo de datos de formulario que debe escribir en el explorador web del cliente para que el formulario de HTML sea visible para el usuario.

**Consulte también**

[Procesar un formulario de HTML que utilice un archivo CSS mediante la API de Java](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Procesar formularios PDF interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Procesar formularios como HTML](/help/forms/developing/rendering-forms-html.md)

[Crear aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Procesar un formulario de HTML que utilice un archivo CSS mediante la API de Java {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

Procesar un formulario de HTML que utilice un archivo CSS personalizado mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clase del proyecto Java.

1. Creación de un objeto de API de Java de Forms

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `FormsServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Hacer referencia al archivo CSS

   * Crear un `HTMLRenderSpec` mediante su constructor.
   * Para procesar el formulario de HTML que utiliza un archivo CSS personalizado, invoque el `HTMLRenderSpec` del objeto `setCustomCSSURI` y pasar un valor de cadena que especifique la ubicación y el nombre del archivo CSS.

1. Procesar un formulario de HTML

   Invoque el `FormsServiceClient` del objeto `(Deprecated) (Deprecated) renderHTMLForm` y pasar los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta de acceso completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valor de enumeración que especifica el tipo de preferencia del HTML. Por ejemplo, para procesar un formulario de HTML compatible con dynamic HTML para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un vacío `com.adobe.idp.Document` objeto.
   * El `HTMLRenderSpec` que almacena las opciones de tiempo de ejecución de HTML.
   * Un valor de cadena que especifica la variable `HTTP_USER_AGENT` valor de encabezado, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` que almacena los valores de URI necesarios para procesar un formulario de HTML.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El `(Deprecated) renderHTMLForm` El método devuelve un valor `FormsResult` que contiene un flujo de datos de formulario que debe escribirse en el explorador web cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Crear un `com.adobe.idp.Document` invocando el objeto de `FormsResult` del objeto `getOutputContent` método.
   * Obtenga el tipo de contenido del `com.adobe.idp.Document` invocando su objeto `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasando el tipo de contenido del `com.adobe.idp.Document` objeto.
   * Crear un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos de formulario en el explorador web del cliente invocando el `javax.servlet.h\ttp.HttpServletResponse` del objeto `getOutputStream` método.
   * Crear un `java.io.InputStream` invocando el objeto de `com.adobe.idp.Document` del objeto `getInputStream` método.
   * Cree una matriz de bytes y rellénela con el flujo de datos de formulario invocando el método `InputStream` del objeto `read` y pasando la matriz de bytes como argumento.
   * Invoque el `javax.servlet.ServletOutputStream` del objeto `write` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes a `write` método.

**Consulte también**

[Procesar formularios HTML mediante archivos CSS personalizados](#rendering-html-forms-using-custom-css-files)

[SOAP Inicio rápido (modo de): Procesamiento de un formulario de HTML que utiliza un archivo CSS mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Procesar un formulario de HTML que utilice un archivo CSS mediante la API de servicio web {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

Procesar un formulario de HTML que utilice un archivo CSS personalizado mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases de proxy Java en la ruta de clase.

1. Creación de un objeto de API de Java de Forms

   Crear un `FormsService` y establezca los valores de autenticación.

1. Hacer referencia al archivo CSS

   * Crear un `HTMLRenderSpec` mediante su constructor.
   * Para procesar el formulario de HTML que utiliza un archivo CSS personalizado, invoque el `HTMLRenderSpec` del objeto `setCustomCSSURI` y pasar un valor de cadena que especifique la ubicación y el nombre del archivo CSS.

1. Procesar un formulario de HTML

   Invoque el `FormsService` del objeto `(Deprecated) renderHTMLForm` y pasar los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta de acceso completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valor de enumeración que especifica el tipo de preferencia del HTML. Por ejemplo, para procesar un formulario de HTML compatible con dynamic HTML para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * A `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar los datos, apruebe `null`. (Consulte [Rellenado previo de Forms con diseños flexibles](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * El `HTMLRenderSpec` que almacena las opciones de tiempo de ejecución de HTML.
   * Un valor de cadena que especifica la variable `HTTP_USER_AGENT` valor de encabezado, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Puede pasar una cadena vacía si no desea establecer este valor.
   * A `URLSpec` que almacena los valores de URI necesarios para procesar un formulario de HTML.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un vacío `com.adobe.idp.services.holders.BLOBHolder` objeto que se rellena con la variable `(Deprecated) renderHTMLForm` método. Este valor de parámetro almacena el formulario procesado.
   * Un vacío `com.adobe.idp.services.holders.BLOBHolder` objeto que se rellena con la variable `(Deprecated) renderHTMLForm` método. Este parámetro almacena los datos XML de salida.
   * Un vacío `javax.xml.rpc.holders.LongHolder` objeto que se rellena con la variable `(Deprecated) renderHTMLForm` método. Este argumento almacena el número de páginas del formulario.
   * Un vacío `javax.xml.rpc.holders.StringHolder` objeto que se rellena con la variable `(Deprecated) renderHTMLForm` método. Este argumento almacena el valor de configuración regional.
   * Un vacío `javax.xml.rpc.holders.StringHolder` objeto que se rellena con la variable `(Deprecated) renderHTMLForm` método. Este argumento almacena el valor de procesamiento del HTML que se utiliza.
   * Un vacío `com.adobe.idp.services.holders.FormsResultHolder` que contendrá los resultados de esta operación.

   El `(Deprecated) renderHTMLForm` rellena el método `com.adobe.idp.services.holders.FormsResultHolder` que se pasa como el último valor de argumento con un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Crear un `FormResult` al obtener el valor de la variable `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value` miembro de datos.
   * Crear un `BLOB` que contiene datos de formulario invocando el `FormsResult` del objeto `getOutputContent` método.
   * Obtenga el tipo de contenido del `BLOB` invocando su objeto `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasando el tipo de contenido del `BLOB` objeto.
   * Crear un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos de formulario en el explorador web del cliente invocando el `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Cree una matriz de bytes y rellénela invocando el método `BLOB` del objeto `getBinaryData` método. Esta tarea asigna el contenido del `FormsResult` a la matriz de bytes.
   * Invoque el `javax.servlet.http.HttpServletResponse` del objeto `write` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes a `write` método.

**Consulte también**

[Procesar formularios HTML mediante archivos CSS personalizados](#rendering-html-forms-using-custom-css-files)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
