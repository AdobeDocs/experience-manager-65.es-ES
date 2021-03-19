---
title: Representación de Forms en el cliente
seo-title: Representación de Forms en el cliente
description: Optimice la entrega del contenido PDF y mejore la capacidad del servicio Forms para gestionar la carga de red mediante la capacidad de renderización del lado del cliente de Acrobat o Adobe Reader
seo-description: Optimice la entrega del contenido PDF y mejore la capacidad del servicio Forms para gestionar la carga de red mediante la capacidad de renderización del lado del cliente de Acrobat o Adobe Reader
uuid: 09bcc23d-28b0-473a-87f1-bc17e87620f4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 08d36e9f-cafc-478e-9781-8fc29ac6262e
role: Desarrollador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1731'
ht-degree: 0%

---


# Renderización de Forms en el cliente {#rendering-forms-at-the-client}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

## Renderización de Forms en el cliente {#rendering-forms-at-the-client-inner}

Puede optimizar la entrega de contenido PDF y mejorar la capacidad del servicio Forms para gestionar la carga de red mediante la función de renderización del lado del cliente de Acrobat o Adobe Reader. Este proceso se conoce como procesamiento de un formulario en el cliente. Para procesar un formulario en el cliente, el dispositivo cliente (normalmente un explorador web) debe utilizar Acrobat 7.0 o Adobe Reader 7.0 o posterior.

Los cambios en un formulario resultantes de la ejecución de secuencias de comandos en el servidor no se reflejan en un formulario procesado en el cliente a menos que el subformulario raíz contenga el atributo `restoreState` definido como `auto`. Para obtener más información sobre este atributo, consulte [Forms Designer.](https://www.adobe.com/go/learn_aemforms_designer_63)

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

Para poder realizar mediante programación una operación de API de cliente de servicio de Forms, debe crear un cliente de servicio de Forms. Si utiliza la API de Java, cree un objeto `FormsServiceClient`. Si utiliza la API de servicio web de Forms, cree un objeto `FormsService`.

**Establecer las opciones de ejecución de procesamiento del cliente**

Debe definir la opción tiempo de ejecución de procesamiento del cliente para procesar un formulario en el cliente estableciendo la opción `RenderAtClient` tiempo de ejecución en `true`. Esto hace que el formulario se envíe al dispositivo cliente en el que se procese. Si `RenderAtClient` es `auto` (el valor predeterminado), el diseño de formulario determina si el formulario se procesa en el cliente. El diseño de formulario debe ser un diseño de formulario con una presentación flexible.

Una opción opcional de tiempo de ejecución que puede establecer es la opción `SeedPDF`. La opción `SeedPDF` combina el contenedor de PDF (documento PDF semilla) con el diseño de formulario y los datos XML. Tanto el diseño de formulario como los datos XML se envían a Acrobat o Adobe Reader, donde se procesa el formulario. La opción `SeedPDF` se puede utilizar cuando el equipo cliente no tiene fuentes que se utilicen en el formulario, como cuando un usuario final no tiene licencia para utilizar una fuente que el propietario del formulario tenga licencia para utilizar.

Puede utilizar Designer para crear un archivo PDF dinámico simple y utilizarlo como archivo PDF semilla. Se requieren los siguientes pasos para realizar esta tarea:

1. Determine si necesita incrustar alguna fuente dentro del archivo PDF raíz. El archivo PDF semilla deberá contener las fuentes adicionales requeridas por el formulario que se está procesando. Al incrustar fuentes en el archivo PDF semilla, asegúrese de que no infringe ningún acuerdo de licencia de fuentes. En Designer, puede determinar si las fuentes se pueden incrustar legalmente. Al guardar, si hay fuentes que no se pueden incrustar en el formulario, Designer muestra un mensaje con las fuentes que no se pueden incrustar. Este mensaje no se muestra en Designer para documentos PDF estáticos.
1. Si está creando el archivo PDF semilla en Designer, se recomienda que, como mínimo, agregue un campo de texto que contenga un mensaje. El mensaje debe dirigirse a los usuarios de versiones anteriores de Adobe Reader indicando que necesitan Acrobat 7.0 o posterior, o Adobe Reader 7.0 o posterior para ver el documento.
1. Guarde el archivo PDF raíz como archivo PDF dinámico con la extensión de nombre de archivo PDF.

>[!NOTE]
>
>No es necesario definir la opción de ejecución del PDF semilla para procesar un formulario en el cliente. Si no especifica un PDF semilla, el servicio de Forms crea un PDF raíz que no contendrá objetos COS pero contendrá un envoltorio PDF con el contenido XDP real incrustado dentro. Los pasos de esta sección no establecen la opción de tiempo de ejecución del PDF semilla. Para obtener información sobre los objetos COS, consulte la guía de referencia de Adobe PDF.

**Representar un formulario en el cliente**

Para procesar un formulario en el cliente, debe asegurarse de que las opciones de tiempo de ejecución de representación del cliente se incluyen en la lógica de la aplicación para procesar un formulario.

**Escribir el flujo de datos del formulario en el explorador web del cliente**

El servicio Forms crea un flujo de datos de formulario que debe escribir en el explorador web del cliente. Cuando se escribe en el explorador web del cliente, el formulario lo representa Acrobat 7.0 o Adobe Reader 7.0 o posterior y es visible para el usuario.

**Consulte también**

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

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `FormsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Establecer las opciones de ejecución de procesamiento del cliente

   * Cree un objeto `PDFFormRenderSpec` utilizando su constructor.
   * Establezca la opción `RenderAtClient` tiempo de ejecución invocando el método `PDFFormRenderSpec` del objeto `setRenderAtClient` y pasando el valor de enumeración `RenderAtClient.Yes`.

1. Representar un formulario en el cliente

   Invoque el método `FormsServiceClient` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de AEM Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un objeto `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un objeto `com.adobe.idp.Document` vacío.
   * Un objeto `PDFFormRenderSpec` que almacena las opciones en tiempo de ejecución necesarias para procesar un formulario en el cliente.
   * Un objeto `URLSpec` que contiene valores de URI necesarios para el servicio Forms para procesar un formulario.
   * Un objeto `java.util.HashMap` que almacena archivos adjuntos. Se trata de un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El método `renderPDFForm` devuelve un objeto `FormsResult` que contiene un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un objeto `com.adobe.idp.Document` invocando el método `FormsResult` del objeto ‘s `getOutputContent`.
   * Obtenga el tipo de contenido del objeto `com.adobe.idp.Document` invocando su método `getContentType`.
   * Establezca el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `com.adobe.idp.Document`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se utilice para escribir el flujo de datos del formulario en el explorador web del cliente invocando el método `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream`.
   * Cree un objeto `java.io.InputStream` invocando el método `com.adobe.idp.Document` del objeto `getInputStream`.
   * Cree una matriz de bytes y rellénela con la secuencia de datos del formulario invocando el método `InputStream` del objeto `read` y pasando la matriz de bytes como argumento.
   * Invoque el método `javax.servlet.ServletOutputStream` del objeto `write` para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Inicio rápido (modo SOAP): Representación de un formulario en el cliente mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Representar un formulario en el cliente mediante la API de servicio web {#render-a-form-at-the-client-using-the-web-service-api}

Representar un formulario en el cliente mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases proxy de Java en la ruta de clase.

1. Creación de un objeto de API de cliente de Forms

   Cree un objeto `FormsService` y establezca valores de autenticación.

1. Establecer las opciones de ejecución de procesamiento del cliente

   * Cree un objeto `PDFFormRenderSpec` utilizando su constructor.
   * Establezca la opción `RenderAtClient` tiempo de ejecución invocando el método `PDFFormRenderSpec` del objeto `setRenderAtClient` y pasando el valor de cadena `RenderAtClient.Yes`.

1. Representar un formulario en el cliente

   Invoque el método `FormsService` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un objeto `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`. (Consulte [Rellenado previo de Forms con diseños de posición variable](/help/forms/developing/prepopulating-forms-flowable-layouts.md)).
   * Un objeto `PDFFormRenderSpec` que almacena las opciones en tiempo de ejecución necesarias para procesar un formulario en el cliente.
   * Un objeto `URLSpec` que contiene valores de URI necesarios para el servicio Forms.
   * Un objeto `java.util.HashMap` que almacena archivos adjuntos. Se trata de un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un objeto `com.adobe.idp.services.holders.BLOBHolder` vacío que se rellena con el método . Este parámetro se utiliza para almacenar el formulario PDF procesado.
   * Un objeto `javax.xml.rpc.holders.LongHolder` vacío que se rellena con el método . (Este argumento almacenará el número de páginas del formulario).
   * Un objeto `javax.xml.rpc.holders.StringHolder` vacío que se rellena con el método . (Este argumento almacenará el valor de configuración regional).
   * Un objeto `com.adobe.idp.services.holders.FormsResultHolder` vacío que contendrá los resultados de esta operación.

   El método `renderPDFForm` rellena el objeto `com.adobe.idp.services.holders.FormsResultHolder` que se pasa como el último valor de argumento con un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un objeto `FormResult` obteniendo el valor del miembro de datos `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value`.
   * Cree un objeto `BLOB` que contenga datos de formulario invocando el método `FormsResult` del objeto `getOutputContent`.
   * Obtenga el tipo de contenido del objeto `BLOB` invocando su método `getContentType`.
   * Establezca el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `BLOB`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se utilice para escribir el flujo de datos del formulario en el explorador web del cliente invocando el método `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream`.
   * Cree una matriz de bytes y rellénela invocando el método `BLOB` del objeto `getBinaryData`. Esta tarea asigna el contenido del objeto `FormsResult` a la matriz de bytes.
   * Invoque el método `javax.servlet.http.HttpServletResponse` del objeto `write` para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Representación de Forms en el cliente](#rendering-forms-at-the-client)

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
