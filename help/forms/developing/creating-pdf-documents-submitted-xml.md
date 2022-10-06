---
title: Creación de documentos de PDF con datos XML enviados
seo-title: Creating PDF Documents with SubmittedXML Data
description: Utilice el servicio Forms para recuperar los datos de formulario que el usuario ha introducido en un formulario interactivo. Pase los datos del formulario a otra operación de servicio de AEM Forms y cree un documento de PDF con los datos.
seo-description: Use the Forms service to retrieve the form data that the user entered into an interactive form. Pass the form data to another AEM Forms service operation and create a PDF document using the data.
uuid: 2676c614-8988-451b-ac7c-bd07731a3f5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 62490230-a24e-419d-95bb-c0bb04a03f96
role: Developer
exl-id: d9d5b94a-9d10-4d90-9e10-5142f30ba4a3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1320'
ht-degree: 0%

---

# Creación de documentos de PDF con datos XML enviados {#creating-pdf-documents-with-submittedxml-data}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

## Creación de documentos de PDF con datos XML enviados {#creating-pdf-documents-with-submitted-xml-data}

Las aplicaciones basadas en la Web que permiten a los usuarios rellenar formularios interactivos requieren que los datos se envíen de nuevo al servidor. Con el servicio Forms, puede recuperar los datos de formulario que el usuario introdujo en un formulario interactivo. A continuación, puede pasar los datos del formulario a otra operación de servicio de AEM Forms y crear un documento de PDF con los datos.

>[!NOTE]
>
>Antes de leer este contenido, se recomienda tener una comprensión sólida de la gestión de los formularios enviados. Los conceptos como la relación entre un diseño de formulario y los datos XML enviados se tratan en Gestión de Forms enviados.

Considere el siguiente flujo de trabajo que incluye tres servicios de AEM Forms:

* Un usuario envía datos XML al servicio Forms desde una aplicación basada en Web.
* El servicio Forms se utiliza para procesar los campos de formulario enviado y de formulario extraído. Se pueden procesar los datos del formulario. Por ejemplo, los datos se pueden enviar a una base de datos empresarial.
* Los datos del formulario se envían al servicio Output para crear un documento de PDF no interactivo.
* El documento de PDF no interactivo se almacena en Content Services (obsoleto).

El diagrama siguiente proporciona una representación visual de este flujo de trabajo.

![cd_cd_finsrv_Architecture_xml_pdf1](assets/cd_cd_finsrv_architecture_xml_pdf1.png)

Una vez que el usuario envía el formulario desde el explorador web del cliente, el documento de PDF no interactivo se almacena en Content Services (obsoleto). La siguiente ilustración muestra un documento de PDF almacenado en Content Services (obsoleto).

![cd_cd_cs_gui](assets/cd_cd_cs_gui.png)

### Resumen de los pasos {#summary-of-steps}

Para crear un documento de PDF no interactivo con datos XML enviados y almacenarlos en el documento de PDF en Content Services (obsoleto), realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Crear objetos Forms, Output y Document Management.
1. Recupere los datos del formulario mediante el servicio Forms.
1. Cree un documento de PDF no interactivo mediante el servicio Output .
1. Almacene el formulario de PDF en Content Services (obsoleto) mediante el servicio de Gestión de documentos.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear objetos de Forms, Output y Document Management**

Antes de realizar una operación de API de servicio de Forms mediante programación, cree un objeto de API de cliente de Forms. Del mismo modo, como este flujo de trabajo invoca los servicios de Output y Document Management, cree un objeto de API de cliente de salida y un objeto de API de cliente de Document Management.

**Recuperación de datos de formulario mediante el servicio Forms**

Recupere los datos de formulario enviados al servicio Forms. Puede procesar los datos enviados para satisfacer los requisitos empresariales. Por ejemplo, puede almacenar datos de formulario en una base de datos de empresa. Sin embargo, para crear un documento de PDF no interactivo, los datos del formulario se pasan al servicio Output .

**Cree un documento de PDF no interactivo mediante el servicio Output .**

Utilice el servicio Output para crear un documento PDF no interactivo basado en un diseño de formulario y en datos de formulario XML. En el flujo de trabajo, los datos del formulario se recuperan del servicio Forms.

**Almacene el formulario de PDF en Content Services (obsoleto) mediante el servicio de gestión de documentos**

Utilice la API de servicio de gestión de documentos para almacenar un documento de PDF en Content Services (obsoleto).

**Consulte también lo siguiente**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### Creación de un documento de PDF con datos XML enviados mediante la API de Java {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}

Cree un documento PDF con los datos XML enviados mediante la API de Forms, salida y gestión de documentos (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-forms-client.jar, adobe-output-client.jar y adobe-contentservices-client.jar en la ruta de clase de su proyecto Java.

1. Crear objetos de Forms, Output y Document Management

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `FormsServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.
   * Cree un `OutputClient` usando su constructor y pasando el `ServiceClientFactory` objeto.
   * Cree un `DocumentManagementServiceClientImpl` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recuperación de datos de formulario mediante el servicio Forms

   * Invocar el `FormsServiceClient` del objeto `processFormSubmission` y pase los siguientes valores:

      * La variable `com.adobe.idp.Document` objeto que contiene los datos del formulario.
      * Un valor de cadena que especifica variables de entorno, incluidos todos los encabezados HTTP relevantes. Especifique el tipo de contenido que se va a gestionar especificando uno o más valores para la variable `CONTENT_TYPE` variable de entorno. Por ejemplo, para gestionar datos XML, especifique el siguiente valor de cadena para este parámetro: `CONTENT_TYPE=text/xml`.
      * Un valor de cadena que especifica la variable `HTTP_USER_AGENT` valor de encabezado, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` que almacena opciones en tiempo de ejecución.

      La variable `processFormSubmission` el método devuelve un `FormsResult` que contiene los resultados del envío del formulario.

   * Determine si el servicio Forms ha terminado de procesar los datos del formulario invocando la variable `FormsResult` del objeto `getAction` método. Si este método devuelve el valor `0`, los datos están listos para procesarse.
   * Recupere los datos del formulario creando un `com.adobe.idp.Document` invocando el objeto `FormsResult` del objeto `getOutputContent` método. (Este objeto contiene datos de formulario que se pueden enviar al servicio Output ).
   * Cree un `java.io.InputStream` invocando el objeto `java.io.DataInputStream` constructor y pasar el `com.adobe.idp.Document` objeto.
   * Cree un `org.w3c.dom.DocumentBuilderFactory` llamando al objeto estático `org.w3c.dom.DocumentBuilderFactory` del objeto `newInstance` método.
   * Cree un `org.w3c.dom.DocumentBuilder` invocando el objeto `org.w3c.dom.DocumentBuilderFactory` del objeto `newDocumentBuilder` método.
   * Cree un `org.w3c.dom.Document` invocando el objeto `org.w3c.dom.DocumentBuilder` del objeto `parse` y pasando el `java.io.InputStream` objeto.
   * Recupere el valor de cada nodo dentro del documento XML. Una forma de realizar esta tarea es crear un método personalizado que acepte dos parámetros: el `org.w3c.dom.Document` y el nombre del nodo cuyo valor desea recuperar. Este método devuelve un valor de cadena que representa el valor del nodo . En el ejemplo de código que sigue este proceso, se llama a este método personalizado `getNodeText`. Se muestra el cuerpo de este método.


1. Cree un documento de PDF no interactivo mediante el servicio Output .

   Cree un documento de PDF invocando la variable `OutputClient` del objeto `generatePDFOutput` y pasando los siguientes valores:

   * A `TransformationFormat` valor de enumeración. Para generar un documento de PDF, especifique `TransformationFormat.PDF`.
   * Un valor de cadena que especifica el nombre del diseño de formulario. Asegúrese de que el diseño de formulario sea compatible con los datos de formulario recuperados del servicio Forms.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentra el diseño de formulario.
   * A `PDFOutputOptionsSpec` que contiene opciones de tiempo de ejecución del PDF.
   * A `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * La variable `com.adobe.idp.Document` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario. Asegúrese de que el `FormsResult` del objeto `getOutputContent` método.
   * La variable `generatePDFOutput` devuelve un valor `OutputResult` que contiene los resultados de la operación.
   * Recupere el documento de PDF no interactivo invocando la variable `OutputResult` del objeto `getGeneratedDoc` método. Este método devuelve un `com.adobe.idp.Document` que representa el documento de PDF no interactivo.

1. Almacene el formulario de PDF en Content Services (obsoleto) mediante el servicio de gestión de documentos

   Añada el contenido invocando la variable `DocumentManagementServiceClientImpl` del objeto `storeContent` y pasando los siguientes valores:

   * Un valor de cadena que especifica el almacén donde se agrega el contenido. El almacén predeterminado es `SpacesStore`. Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la ruta completa del espacio donde se agrega el contenido (por ejemplo, `/Company Home/Test Directory`). Este valor es un parámetro obligatorio.
   * El nombre del nodo que representa el nuevo contenido (por ejemplo, `MortgageForm.pdf`). Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica el tipo de nodo. Para añadir contenido nuevo, como un archivo de PDF, especifique `{https://www.alfresco.org/model/content/1.0}content`. Este valor es un parámetro obligatorio.
   * A `com.adobe.idp.Document` que representa el contenido. Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica el valor de codificación (por ejemplo, `UTF-8`). Este valor es un parámetro obligatorio.
   * Un `UpdateVersionType` valor de enumeración que especifica cómo gestionar la información de versión (por ejemplo, `UpdateVersionType.INCREMENT_MAJOR_VERSION` para aumentar la versión del contenido. ) Este valor es un parámetro obligatorio.
   * A `java.util.List` instancia que especifica aspectos relacionados con el contenido. Este valor es un parámetro opcional y puede especificar `null`.
   * A `java.util.Map` objeto que almacena atributos de contenido.

   La variable `storeContent` el método devuelve un `CRCResult` objeto que describe el contenido. Uso de un `CRCResult` , puede, por ejemplo, obtener el valor de identificador único del contenido. Para realizar esta tarea, invoque la función `CRCResult` del objeto `getNodeUuid` método.

**Consulte también lo siguiente**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
