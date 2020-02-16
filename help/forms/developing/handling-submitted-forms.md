---
title: Gestión de formularios enviados
seo-title: Gestión de formularios enviados
description: nulo
seo-description: nulo
uuid: 673b28f1-f023-4da8-a6a0-c5ff921c5f5d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3d838027-6bde-4a71-a428-4d5102f7d799
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Gestión de formularios enviados {#handling-submitted-forms}

Las aplicaciones basadas en la Web que permiten al usuario rellenar formularios interactivos requieren que los datos se envíen de nuevo al servidor. Con el servicio Forms, puede recuperar los datos introducidos por el usuario en un formulario interactivo. Después de recuperar los datos, puede procesarlos para cumplir con los requisitos comerciales. Por ejemplo, puede almacenar los datos en una base de datos, enviarlos a otra aplicación, enviarlos a otro servicio, combinar los datos en un diseño de formulario, mostrar los datos en un explorador Web, etc.

Los datos de formulario se envían al servicio Forms como datos XML o PDF, que es una opción establecida en Designer. Un formulario que se envía como XML permite extraer valores de datos de campo individuales. Es decir, puede extraer el valor de cada campo de formulario que el usuario haya introducido en el formulario. Un formulario que se envía como datos PDF es datos binarios, no datos XML. Puede guardar el formulario como archivo PDF o enviarlo a otro servicio. Si desea extraer datos de un formulario enviado como XML y, a continuación, utilizar los datos del formulario para crear un documento PDF, invoque otra operación de AEM Forms. (Consulte [Creación de documentos PDF con datos](/help/forms/developing/creating-pdf-documents-submitted-xml.md)XML enviados)

El diagrama siguiente muestra los datos que se envían a un servlet Java denominado `HandleData` desde un formulario interactivo que se muestra en un explorador Web.

![hs_hs_handlesubmit](assets/hs_hs_handlesubmit.png)

En la tabla siguiente se explican los pasos del diagrama.

<table>
 <thead>
  <tr>
   <th><p>Etapa</p></th>
   <th><p>Descripción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Un usuario rellena un formulario interactivo y hace clic en el botón Enviar del formulario.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Los datos se envían al servlet de Java <code>HandleData</code> como datos XML.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>El servlet <code>HandleData</code> Java contiene lógica de aplicación para recuperar los datos.</p></td>
  </tr>
 </tbody>
</table>

## Gestión de datos XML enviados {#handling-submitted-xml-data}

Cuando los datos del formulario se envían como XML, se pueden recuperar datos XML que representen los datos enviados. Todos los campos de formulario aparecen como nodos en un esquema XML. Los valores de nodo corresponden a los valores que el usuario ha rellenado. Considere un formulario de préstamo donde cada campo del formulario aparece como un nodo dentro de los datos XML. El valor de cada nodo corresponde al valor que rellena el usuario. Supongamos que un usuario rellena el formulario de préstamo con los datos que se muestran en el siguiente formulario.

![hs_hs_loanformdata](assets/hs_hs_loanformdata.png)

En la siguiente ilustración se muestran los datos XML correspondientes que se recuperan mediante la API del cliente del servicio Forms.

![hs_hs_loandata](assets/hs_hs_loandata.png)

Los campos del formulario de préstamo. Estos valores se pueden recuperar mediante clases XML de Java.

>[!NOTE]
>
>El diseño de formulario debe configurarse correctamente en Designer para que los datos se envíen como datos XML. Para configurar correctamente el diseño de formulario para enviar datos XML, asegúrese de que el botón Enviar que se encuentra en el diseño de formulario está configurado para enviar datos XML. Para obtener más información sobre la configuración del botón Enviar para enviar datos XML, consulte Diseñador de [AEM Forms](https://www.adobe.com/go/learn_aemforms_designer_63).

## Gestión de datos de PDF enviados {#handling-submitted-pdf-data}

Considere una aplicación web que invoque el servicio Forms. Una vez que el servicio Forms procesa un formulario PDF interactivo en un navegador web cliente, el usuario lo rellena y lo devuelve como datos PDF. Cuando el servicio Forms recibe los datos PDF, puede enviarlos a otro servicio o guardarlos como un archivo PDF. El diagrama siguiente muestra el flujo lógico de la aplicación.

![hs_hs_savingforms](assets/hs_hs_savingforms.png)

En la tabla siguiente se describen los pasos de este diagrama.

<table>
 <thead>
  <tr>
   <th><p>Etapa</p></th>
   <th><p>Descripción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Una página web contiene un vínculo que accede a un servlet Java que invoca el servicio Forms.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>El servicio Forms procesa un formulario PDF interactivo en el navegador web del cliente.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>El usuario rellena un formulario interactivo y hace clic en un botón de envío. El formulario se devuelve al servicio Forms como datos PDF. Esta opción se establece en Designer.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>El servicio Forms guarda los datos PDF como un archivo PDF. </p></td>
  </tr>
 </tbody>
</table>

## Gestión de datos UTF-16 de la URL enviada {#handling-submitted-url-utf-16-data}

Si los datos del formulario se envían como datos UTF-16 de URL, el equipo cliente necesita Adobe Reader o Acrobat 8.1 o posterior. Además, si el diseño de formulario contiene un botón de envío con datos codificados con URL (HTTP Post) y la opción de codificación de datos es UTF-16, el diseño de formulario debe modificarse en un editor de texto como el Bloc de notas. Puede definir la opción de codificación en `UTF-16LE` o `UTF-16BE` para el botón de envío. Designer no proporciona esta funcionalidad.

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para gestionar los formularios enviados, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de Forms Client.
1. Recuperar datos de formulario.
1. Determine si el envío del formulario contiene archivos adjuntos.
1. Procese los datos enviados.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Forms Client**

Para poder realizar mediante programación una operación de API de cliente de servicio de Forms, debe crear un cliente de servicio de Forms. Si utiliza la API de Java, cree un `FormsServiceClient` objeto. Si utiliza la API de servicio web de Forms, cree un `FormsService` objeto.

**Recuperar datos de formulario**

Para recuperar los datos de formulario enviados, se invoca el `FormsServiceClient` método `processFormSubmission` del objeto. Al invocar este método, debe especificar el tipo de contenido del formulario enviado. Cuando los datos se envían desde un navegador web de cliente al servicio Forms, se pueden enviar como datos XML o PDF. Para recuperar los datos introducidos en los campos de formulario, estos se pueden enviar como datos XML.

También puede recuperar campos de formulario de un formulario enviado como datos PDF estableciendo las siguientes opciones en tiempo de ejecución:

* Pase el siguiente valor al `processFormSubmission` método como parámetro de tipo de contenido: `CONTENT_TYPE=application/pdf`.
* Definir el `RenderOptionsSpec` valor del `PDFToXDP` objeto en `true`
* Definir el `RenderOptionsSpec` valor del `ExportDataFormat` objeto en `XMLData`

Especifique el tipo de contenido del formulario enviado cuando invoque el `processFormSubmission` método. La siguiente lista especifica los valores de tipo de contenido aplicables:

* **text/xml**: Representa el tipo de contenido que se utiliza cuando un formulario PDF envía datos de formulario como XML.
* **application/x-www-form-urlencoded**: Representa el tipo de contenido que se utiliza cuando un formulario HTML envía datos como XML.
* **application/pdf**: Representa el tipo de contenido que se utiliza cuando un formulario PDF envía datos como PDF.

>[!NOTE]
>
>Observará que hay tres inicios rápidos correspondientes asociados a la sección Gestión de formularios enviados. La administración de formularios PDF enviados como PDF mediante el inicio rápido de la API de Java muestra cómo tratar los datos de PDF enviados. El tipo de contenido especificado en este inicio rápido es `application/pdf`. La administración de formularios PDF enviados como XML mediante el inicio rápido de la API de Java muestra cómo tratar los datos XML enviados desde un formulario PDF. El tipo de contenido especificado en este inicio rápido es `text/xml`. Del mismo modo, la administración de formularios HTML enviados como XML mediante el inicio rápido de la API de Java muestra cómo tratar los datos XML enviados desde un formulario HTML. El tipo de contenido especificado en este inicio rápido es application/x-www-form-urlencoded.

Los datos de formulario que se publicaron en el servicio Forms se recuperan y determinan su estado de procesamiento. Es decir, cuando los datos se envían al servicio Forms, no significa necesariamente que el servicio Forms haya terminado de procesar los datos y que los datos estén listos para procesarse. Por ejemplo, los datos se pueden enviar al servicio Forms para que se pueda realizar un cálculo. Cuando se completa el cálculo, el formulario se devuelve al usuario con los resultados de cálculo mostrados. Antes de procesar los datos enviados, se recomienda determinar si el servicio Forms ha terminado de procesar los datos.

El servicio Forms devuelve los siguientes valores para indicar si ha terminado de procesar los datos:

* **** 0 (Enviar): Los datos enviados están listos para ser procesados.
* **** 1 (Calcular): El servicio Forms realizó una operación de cálculo en los datos y los resultados se deben devolver al usuario.
* **** 2 (Validar): El servicio Forms validó los datos del formulario y los resultados se deben devolver al usuario.
* **** 3 (Siguiente): La página actual ha cambiado con resultados que deben escribirse en la aplicación cliente.
* **4 (Anterior**): La página actual ha cambiado con resultados que deben escribirse en la aplicación cliente.

>[!NOTE]
>
>Los cálculos y las validaciones se deben devolver al usuario. (Consulte [Cálculo de datos]de formulario(/help/forms/develop/procesando-formularios-procesando-formularios calculando-formulario-datos-calculando-formulario-calculando-datos-formulario.md#calculando-formulario-datos)*.)*

**Determinar si el envío del formulario contiene archivos adjuntos**

Los formularios enviados al servicio Forms pueden contener archivos adjuntos. Por ejemplo, con el panel de datos adjuntos integrado de Acrobat, un usuario puede seleccionar archivos adjuntos para enviarlos junto con el formulario. Asimismo, un usuario también puede seleccionar archivos adjuntos mediante una barra de herramientas HTML que se procesa con un archivo HTML.

Después de determinar si un formulario contiene archivos adjuntos, puede procesar los datos. Por ejemplo, puede guardar el archivo adjunto en el sistema de archivos local.

>[!NOTE]
>
>El formulario debe enviarse como datos PDF para recuperar archivos adjuntos. Si el formulario se envía como datos XML, no se envían los archivos adjuntos.

**Procesar los datos enviados**

Según el tipo de contenido de los datos enviados, puede extraer valores de campo de formulario individuales de los datos XML enviados o guardar los datos PDF enviados como archivo PDF (o enviarlos a otro servicio). Para extraer campos de formulario individuales, convierta los datos XML enviados a un origen de datos XML y, a continuación, recupere los valores del origen de datos XML mediante `org.w3c.dom` clases.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de formularios](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Pasar documentos al servicio Forms](/help/forms/developing/passing-documents-forms-service.md)

[Creación de aplicaciones Web que procesan formularios](/help/forms/developing/creating-web-applications-renders-forms.md)

## Administrar formularios enviados mediante la API de Java {#handle-submitted-forms-using-the-java-api}

Gestionar un formulario enviado mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clases del proyecto Java.

1. Creación de un objeto de API de Forms Client

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `FormsServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recuperar datos de formulario

   * Para recuperar datos de formulario publicados en un servlet de Java, cree un `com.adobe.idp.Document` objeto utilizando su constructor e invocando el `javax.servlet.http.HttpServletResponse` método del `getInputStream` objeto desde el constructor.
   * Cree un `RenderOptionsSpec` objeto con su constructor. Establezca el valor de configuración regional invocando el `RenderOptionsSpec` método `setLocale` del objeto y pasando un valor de cadena que especifica el valor de configuración regional.
   >[!NOTE]
   >
   >Puede indicar al servicio Forms que cree datos XDP o XML a partir del contenido PDF enviado invocando el `RenderOptionsSpec` método del `setPDF2XDP` objeto y pasando `true` y también llamando `setXMLData` y pasando `true`. A continuación, puede invocar el `FormsResult` método del `getOutputXML` objeto para recuperar los datos XML que corresponden a los datos XDP/XML. (El `FormsResult` objeto lo devuelve el `processFormSubmission` método, que se explica en el siguiente subpaso).

   * Invoque el `FormsServiceClient` método del `processFormSubmission` objeto y pase los valores siguientes:

      * El `com.adobe.idp.Document` objeto que contiene los datos del formulario.
      * Un valor de cadena que especifica variables de entorno, incluyendo todos los encabezados HTTP relevantes. Especifique el tipo de contenido que se va a gestionar. Para gestionar datos XML, especifique el siguiente valor de cadena para este parámetro: `CONTENT_TYPE=text/xml`. Para gestionar datos PDF, especifique el siguiente valor de cadena para este parámetro: `CONTENT_TYPE=application/pdf`.
      * Un valor de cadena que especifica el valor del `HTTP_USER_AGENT` encabezado, por ejemplo, . `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Este valor de parámetro es opcional.
      * Un `RenderOptionsSpec` objeto que almacena opciones de tiempo de ejecución.
      El `processFormSubmission` método devuelve un `FormsResult` objeto que contiene los resultados del envío del formulario.

   * Determine si el servicio Forms ha terminado de procesar los datos del formulario invocando el `FormsResult` método del `getAction` objeto. Si este método devuelve el valor `0`, los datos están listos para ser procesados.



1. Determinar si el envío del formulario contiene archivos adjuntos

   * Invocar el `FormsResult` método del `getAttachments` objeto. Este método devuelve un `java.util.List` objeto que contiene archivos enviados con el formulario.
   * Repita el `java.util.List` objeto para determinar si hay archivos adjuntos. Si hay archivos adjuntos, cada elemento es una `com.adobe.idp.Document` instancia. Puede guardar los archivos adjuntos invocando el `com.adobe.idp.Document` método del `copyToFile` objeto y pasando un `java.io.File` objeto.
   >[!NOTE]
   >
   >Este paso solo es aplicable si el formulario se envía como PDF.

1. Procesar los datos enviados

   * Si el tipo de contenido de datos es `application/vnd.adobe.xdp+xml` o `text/xml`, cree una lógica de aplicación para recuperar valores de datos XML.

      * Cree un `com.adobe.idp.Document` objeto invocando el `FormsResult` método `getOutputContent` del objeto.
      * Cree un `java.io.InputStream` objeto invocando el `java.io.DataInputStream` constructor y pasando el `com.adobe.idp.Document` objeto.
      * Cree un `org.w3c.dom.DocumentBuilderFactory` objeto llamando al `org.w3c.dom.DocumentBuilderFactory` método `newInstance` del objeto estático.
      * Cree un `org.w3c.dom.DocumentBuilder` objeto invocando el `org.w3c.dom.DocumentBuilderFactory` método `newDocumentBuilder` del objeto.
      * Cree un `org.w3c.dom.Document` objeto invocando el `org.w3c.dom.DocumentBuilder` método `parse` del objeto y pasando el `java.io.InputStream` objeto.
      * Recupere el valor de cada nodo dentro del documento XML. Una forma de realizar esta tarea es crear un método personalizado que acepte dos parámetros: el `org.w3c.dom.Document` objeto y el nombre del nodo cuyo valor desea recuperar. Este método devuelve un valor de cadena que representa el valor del nodo. En el ejemplo de código que sigue a este proceso, se llama a este método personalizado `getNodeText`. Se muestra el cuerpo de este método.
   * Si el tipo de contenido de datos es `application/pdf`, cree una lógica de aplicación para guardar los datos PDF enviados como un archivo PDF.

      * Cree un `com.adobe.idp.Document` objeto invocando el `FormsResult` método `getOutputContent` del objeto.
      * Cree un `java.io.File` objeto mediante su constructor público. Asegúrese de especificar PDF como extensión de nombre de archivo.
      * Rellene el archivo PDF invocando el `com.adobe.idp.Document` método del `copyToFile` objeto y pasando el `java.io.File` objeto.


**Consulte también**

[Inicio rápido (modo SOAP): Gestión de formularios PDF enviados como XML mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[Inicio rápido (modo SOAP): Gestión de formularios HTML enviados como XML mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[Inicio rápido (modo SOAP): Gestión de formularios PDF enviados como PDF mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Gestión de datos de PDF enviados mediante la API de servicio web {#handle-submitted-pdf-data-using-the-web-service-api}

Gestionar un formulario enviado mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases proxy de Java que consuman el WSDL del servicio Forms.
   * Incluya las clases proxy de Java en la ruta de clases.

1. Creación de un objeto de API de Forms Client

   Cree un `FormsService` objeto y defina los valores de autenticación.

1. Recuperar datos de formulario

   * Para recuperar datos de formulario publicados en un servlet Java, cree un `BLOB` objeto con su constructor.
   * Cree un `java.io.InputStream` objeto invocando el `javax.servlet.http.HttpServletResponse` método `getInputStream` del objeto.
   * Cree un `java.io.ByteArrayOutputStream` objeto utilizando su constructor y pasando la longitud del `java.io.InputStream` objeto.
   * Copie el contenido del `java.io.InputStream` objeto en el `java.io.ByteArrayOutputStream` objeto.
   * Cree una matriz de bytes invocando el `java.io.ByteArrayOutputStream` método `toByteArray` del objeto.
   * Rellene el `BLOB` objeto invocando su `setBinaryData` método y pasando la matriz de bytes como argumento.
   * Cree un `RenderOptionsSpec` objeto con su constructor. Establezca el valor de configuración regional invocando el `RenderOptionsSpec` método `setLocale` del objeto y pasando un valor de cadena que especifica el valor de configuración regional.
   * Invoque el `FormsService` método del `processFormSubmission` objeto y pase los valores siguientes:

      * El `BLOB` objeto que contiene los datos del formulario.
      * Un valor de cadena que especifica variables de entorno, incluyendo todos los encabezados HTTP relevantes. Especifique el tipo de contenido que se va a gestionar. Para gestionar datos XML, especifique el siguiente valor de cadena para este parámetro: `CONTENT_TYPE=text/xml`. Para gestionar datos PDF, especifique el siguiente valor de cadena para este parámetro: `CONTENT_TYPE=application/pdf`.
      * Un valor de cadena que especifica el valor del `HTTP_USER_AGENT` encabezado; por ejemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Un `RenderOptionsSpec` objeto que almacena opciones de tiempo de ejecución.
      * Objeto vacío `BLOBHolder` que se rellena con el método .
      * Objeto vacío `javax.xml.rpc.holders.StringHolder` que se rellena con el método .
      * Objeto vacío `BLOBHolder` que se rellena con el método .
      * Objeto vacío `BLOBHolder` que se rellena con el método .
      * Objeto vacío `javax.xml.rpc.holders.ShortHolder` que se rellena con el método .
      * Objeto vacío `MyArrayOf_xsd_anyTypeHolder` que se rellena con el método . Este parámetro se utiliza para almacenar archivos adjuntos enviados junto con el formulario.
      * Objeto vacío `FormsResultHolder` que se rellena con el método con el formulario que se envía.
      El `processFormSubmission` método rellena el `FormsResultHolder` parámetro con los resultados del envío del formulario.

   * Determine si el servicio Forms ha terminado de procesar los datos del formulario invocando el `FormsResult` método del `getAction` objeto. Si este método devuelve el valor `0`, los datos del formulario están listos para procesarse. Puede obtener un `FormsResult` objeto obteniendo el valor del miembro de datos del `FormsResultHolder` objeto `value` .


1. Determinar si el envío del formulario contiene archivos adjuntos

   Obtenga el valor del miembro de `MyArrayOf_xsd_anyTypeHolder` datos del `value` objeto (el `MyArrayOf_xsd_anyTypeHolder` objeto se pasó al `processFormSubmission` método). Este miembro de datos devuelve una matriz de `Objects`. Cada elemento de la `Object` matriz es un elemento `Object`que corresponde a los archivos enviados junto con el formulario. Puede obtener cada elemento dentro de la matriz y convertirlo en un `BLOB` objeto.

1. Procesar los datos enviados

   * Si el tipo de contenido de datos es `application/vnd.adobe.xdp+xml` o `text/xml`, cree una lógica de aplicación para recuperar valores de datos XML.

      * Cree un `BLOB` objeto invocando el `FormsResult` método `getOutputContent` del objeto.
      * Cree una matriz de bytes invocando el `BLOB` método `getBinaryData` del objeto.
      * Cree un `java.io.InputStream` objeto invocando el `java.io.ByteArrayInputStream` constructor y pasando la matriz de bytes.
      * Cree un `org.w3c.dom.DocumentBuilderFactory` objeto llamando al `org.w3c.dom.DocumentBuilderFactory` método `newInstance` del objeto estático.
      * Cree un `org.w3c.dom.DocumentBuilder` objeto invocando el `org.w3c.dom.DocumentBuilderFactory` método `newDocumentBuilder` del objeto.
      * Cree un `org.w3c.dom.Document` objeto invocando el `org.w3c.dom.DocumentBuilder` método `parse` del objeto y pasando el `java.io.InputStream` objeto.
      * Recupere el valor de cada nodo dentro del documento XML. Una forma de realizar esta tarea es crear un método personalizado que acepte dos parámetros: el `org.w3c.dom.Document` objeto y el nombre del nodo cuyo valor desea recuperar. Este método devuelve un valor de cadena que representa el valor del nodo. En el ejemplo de código que sigue a este proceso, se llama a este método personalizado `getNodeText`. Se muestra el cuerpo de este método.
   * Si el tipo de contenido de datos es `application/pdf`, cree una lógica de aplicación para guardar los datos PDF enviados como un archivo PDF.

      * Cree un `BLOB` objeto invocando el `FormsResult` método `getOutputContent` del objeto.
      * Cree una matriz de bytes invocando el `BLOB` método `getBinaryData` del objeto.
      * Cree un `java.io.File` objeto mediante su constructor público. Asegúrese de especificar PDF como extensión de nombre de archivo.
      * Cree un `java.io.FileOutputStream` objeto utilizando su constructor y pasando el `java.io.File` objeto.
      * Rellene el archivo PDF invocando el `java.io.FileOutputStream` método del `write` objeto y pasando la matriz de bytes.


**Consulte también**

[Invocación de formularios AEM con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)