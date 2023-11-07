---
title: Procesar formularios en el cliente
seo-title: Rendering Forms at the Client
description: Optimizar la entrega de contenido de PDF y mejorar la capacidad del servicio Forms para gestionar la carga de red mediante la capacidad de procesamiento del lado del cliente de Acrobat o Adobe Reader
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
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1694'
ht-degree: 2%

---

# Procesar formularios en el cliente {#rendering-forms-at-the-client}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

## Procesar formularios en el cliente {#rendering-forms-at-the-client-inner}

Puede optimizar la entrega de contenido de PDF y mejorar la capacidad del servicio Forms para gestionar la carga de red mediante la capacidad de procesamiento del lado del cliente de Acrobat o Adobe Reader. Este proceso se conoce como procesar un formulario en el cliente. Para procesar un formulario en el cliente, el dispositivo cliente (normalmente un explorador web) debe utilizar Acrobat 7.0 o Adobe Reader 7.0 o posterior.

Los cambios realizados en un formulario como resultado de la ejecución de scripts del lado del servidor no se reflejan en un formulario que se procese en el cliente a menos que el subformulario raíz contenga el `restoreState` atributo que se establece en `auto`. Para obtener más información sobre este atributo, consulte [Forms Designer.](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para procesar un formulario en el cliente, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Establecer las opciones de tiempo de ejecución de procesamiento de cliente.
1. Procesar un formulario en el cliente.
1. Escriba el formulario en el explorador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API de cliente de Forms**

Para poder realizar mediante programación una operación de API de cliente de servicio de Forms, debe crear un cliente de servicio de Forms. Si utiliza la API de Java, cree un `FormsServiceClient` objeto. Si utiliza la API del servicio web de Forms, cree un `FormsService` objeto.

**Establecer opciones de tiempo de ejecución de procesamiento de cliente**

Establezca la opción de tiempo de ejecución de representación de cliente para procesar un formulario en el cliente estableciendo la variable `RenderAtClient` opción de tiempo de ejecución para `true`. Esto hace que el formulario se envíe al dispositivo cliente donde se representa. If `RenderAtClient` es `auto` (el valor predeterminado), el diseño de formulario determina si el formulario se procesa en el cliente. El diseño de formulario debe ser un diseño de formulario con un diseño fluido.

Una opción de tiempo de ejecución opcional que puede establecer es la `SeedPDF` opción. El `SeedPDF` combina el contenedor de PDF (documento de PDF semilla) con el diseño de formulario y los datos XML. Tanto el diseño de formulario como los datos XML se envían a Acrobat o Adobe Reader, donde se procesa el formulario. El `SeedPDF` se puede utilizar cuando el equipo cliente no tiene fuentes que se utilicen en el formulario, como cuando un usuario final no tiene licencia para utilizar una fuente para la que el propietario del formulario tiene licencia.

Puede utilizar Designer para crear un archivo PDF dinámico simple para utilizarlo como archivo PDF semilla. Se requieren los siguientes pasos para realizar esta tarea:

1. Determine si necesita incrustar alguna fuente dentro del archivo del PDF semilla. El archivo del PDF semilla debe contener las fuentes adicionales que requiere el formulario que se está procesando. Al incrustar fuentes en el archivo del PDF semilla, asegúrese de que no infringe ningún acuerdo de licencia de fuentes. En Designer, puede determinar si puede incrustar fuentes legalmente. Al guardar, si hay fuentes que no se pueden incrustar en el formulario, Designer muestra un mensaje con las fuentes que no se pueden incrustar. Este mensaje no se muestra en Designer para documentos de PDF estáticos.
1. Si está creando el archivo del PDF semilla en Designer, se recomienda que, como mínimo, añada un campo de texto que contenga un mensaje. El mensaje debe dirigirse a los usuarios de versiones anteriores de Adobe Reader para informarles de que necesitan Acrobat 7.0 o posterior, o Adobe Reader 7.0 o posterior, para ver el documento.
1. Guarde el archivo del PDF semilla como un archivo de PDF dinámico con la extensión de nombre de archivo del PDF.

>[!NOTE]
>
>No es necesario definir la opción del PDF semilla en tiempo de ejecución para procesar un formulario en el cliente. Si no especifica un PDF semilla, el servicio Forms crea un PDF de shell que no contendrá objetos COS, pero sí un envoltorio de PDF con el contenido XDP real incrustado en él. Los pasos de esta sección no establecen la opción del PDF semilla en tiempo de ejecución. Para obtener información sobre los objetos COS, consulte la Guía de referencia de Adobe PDF.

**Procesar un formulario en el cliente**

Para procesar un formulario en el cliente, debe asegurarse de que las opciones de tiempo de ejecución de procesamiento del cliente estén incluidas en la lógica de la aplicación para procesar un formulario.

**Escribir el flujo de datos del formulario en el explorador web del cliente**

El servicio Forms crea un flujo de datos de formulario que debe escribir en el explorador web del cliente. Cuando se escribe en el explorador web del cliente, el formulario se procesa mediante Acrobat 7.0 o Adobe Reader 7.0 o posterior y es visible para el usuario.

**Consulte también**

[Procesar un formulario en el cliente mediante la API de Java](#render-a-form-at-the-client-using-the-java-api)

[Procesar un formulario en el cliente mediante la API de servicio web](#render-a-form-at-the-client-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Pasar documentos al servicio de Forms](/help/forms/developing/passing-documents-forms-service.md)

[Crear aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Procesar un formulario en el cliente mediante la API de Java {#render-a-form-at-the-client-using-the-java-api}

Procesar un formulario en el cliente mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clase del proyecto Java.

1. Crear un objeto de API de cliente de Forms

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `FormsServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Establecer opciones de tiempo de ejecución de procesamiento de cliente

   * Crear un `PDFFormRenderSpec` mediante su constructor.
   * Configure las variables `RenderAtClient` en tiempo de ejecución invocando la opción `PDFFormRenderSpec` del objeto `setRenderAtClient` y pasando el valor de enumeración `RenderAtClient.Yes`.

1. Procesar un formulario en el cliente

   Invoque el `FormsServiceClient` del objeto `renderPDFForm` y pasar los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de AEM Forms, asegúrese de especificar la ruta de acceso completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un vacío `com.adobe.idp.Document` objeto.
   * A `PDFFormRenderSpec` que almacena las opciones en tiempo de ejecución necesarias para procesar un formulario en el cliente.
   * A `URLSpec` que contiene valores de URI requeridos por el servicio Forms para procesar un formulario.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El `renderPDFForm` El método devuelve un valor `FormsResult` que contiene un flujo de datos de formulario que debe escribirse en el explorador web cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Crear un `com.adobe.idp.Document` invocando el objeto de `FormsResult` objeto ‘s `getOutputContent` método.
   * Obtenga el tipo de contenido del `com.adobe.idp.Document` invocando su objeto `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasando el tipo de contenido del `com.adobe.idp.Document` objeto.
   * Crear un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos de formulario en el explorador web del cliente invocando el `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Crear un `java.io.InputStream` invocando el objeto de `com.adobe.idp.Document` del objeto `getInputStream` método.
   * Cree una matriz de bytes y rellénela con el flujo de datos de formulario invocando el método `InputStream` del objeto `read` y pasando la matriz de bytes como argumento.
   * Invoque el `javax.servlet.ServletOutputStream` del objeto `write` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes a `write` método.

**Consulte también**

[Inicio rápido (modo SOAP): Procesamiento de un formulario en el cliente mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Procesar un formulario en el cliente mediante la API de servicio web {#render-a-form-at-the-client-using-the-web-service-api}

Procesar un formulario en el cliente mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases de proxy Java en la ruta de clase.

1. Crear un objeto de API de cliente de Forms

   Crear un `FormsService` y establezca los valores de autenticación.

1. Establecer opciones de tiempo de ejecución de procesamiento de cliente

   * Crear un `PDFFormRenderSpec` mediante su constructor.
   * Configure las variables `RenderAtClient` en tiempo de ejecución invocando la opción `PDFFormRenderSpec` del objeto `setRenderAtClient` método y pasar el valor de cadena `RenderAtClient.Yes`.

1. Procesar un formulario en el cliente

   Invoque el `FormsService` del objeto `renderPDFForm` y pasar los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta de acceso completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar los datos, apruebe `null`. (Consulte [Rellenado previo de Forms con diseños flexibles](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * A `PDFFormRenderSpec` que almacena las opciones en tiempo de ejecución necesarias para procesar un formulario en el cliente.
   * A `URLSpec` que contiene valores de URI requeridos por el servicio de Forms.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un vacío `com.adobe.idp.services.holders.BLOBHolder` objeto que rellena el método. Este parámetro se utiliza para almacenar el formulario de PDF procesado.
   * Un vacío `javax.xml.rpc.holders.LongHolder` objeto que rellena el método. (Este argumento almacenará el número de páginas en el formulario).
   * Un vacío `javax.xml.rpc.holders.StringHolder` objeto que rellena el método. (Este argumento almacenará el valor de configuración regional).
   * Un vacío `com.adobe.idp.services.holders.FormsResultHolder` que contendrá los resultados de esta operación.

   El `renderPDFForm` rellena el método `com.adobe.idp.services.holders.FormsResultHolder` que se pasa como el último valor de argumento con un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Crear un `FormResult` al obtener el valor de la variable `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value` miembro de datos.
   * Crear un `BLOB` que contiene datos de formulario invocando el `FormsResult` del objeto `getOutputContent` método.
   * Obtenga el tipo de contenido del `BLOB` invocando su objeto `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasando el tipo de contenido del `BLOB` objeto.
   * Crear un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos de formulario en el explorador web del cliente invocando el `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Cree una matriz de bytes y rellénela invocando el método `BLOB` del objeto `getBinaryData` método. Esta tarea asigna el contenido del `FormsResult` a la matriz de bytes.
   * Invoque el `javax.servlet.http.HttpServletResponse` del objeto `write` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes a `write` método.

**Consulte también**

[Procesar formularios en el cliente](#rendering-forms-at-the-client)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
