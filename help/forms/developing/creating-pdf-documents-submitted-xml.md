---
title: Creación de documentos PDF con datos XML enviados
seo-title: Creación de documentos PDF con datos XML enviados
description: nulo
seo-description: nulo
uuid: 2676c614-8988-451b-ac7c-bd07731a3f5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 62490230-a24e-419d-95bb-c0bb04a03f96
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Creación de documentos PDF con datos XML enviados {#creating-pdf-documents-with-submittedxml-data}

## Creación de documentos PDF con datos XML enviados {#creating-pdf-documents-with-submitted-xml-data}

Las aplicaciones basadas en la Web que permiten a los usuarios rellenar formularios interactivos requieren que los datos se envíen de nuevo al servidor. Con el servicio Forms, puede recuperar los datos del formulario que el usuario ha introducido en un formulario interactivo. A continuación, puede pasar los datos del formulario a otra operación de servicio de AEM Forms y crear un documento PDF con los datos.

>[!NOTE]
>
>Antes de leer este contenido, se recomienda tener una sólida comprensión del manejo de los formularios enviados. Los conceptos como la relación entre un diseño de formulario y los datos XML enviados se tratan en Gestión de formularios enviados.

Considere el siguiente flujo de trabajo que incluye tres servicios de AEM Forms:

* Un usuario envía datos XML al servicio Forms desde una aplicación basada en web.
* El servicio Forms se utiliza para procesar el formulario enviado y extraer los campos del formulario. Se pueden procesar los datos del formulario. Por ejemplo, los datos se pueden enviar a una base de datos empresarial.
* Los datos del formulario se envían al servicio Output para crear un documento PDF no interactivo.
* El documento PDF no interactivo se almacena en Content Services (desaprobado).

El diagrama siguiente proporciona una representación visual de este flujo de trabajo.

![cd_cd_finsrv_Architecture_xml_pdf1](assets/cd_cd_finsrv_architecture_xml_pdf1.png)

Una vez que el usuario envía el formulario desde el navegador web del cliente, el documento PDF no interactivo se almacena en Content Services (desaprobado). La siguiente ilustración muestra un documento PDF almacenado en Content Services (desaprobado).

![cd_cd_cs_gui](assets/cd_cd_cs_gui.png)

### Resumen de los pasos {#summary-of-steps}

Para crear un documento PDF no interactivo con datos XML enviados y almacenarlo en el documento PDF en Content Services (desaprobado), realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Crear objetos de Forms, Output y Document Management.
1. Recuperar datos de formulario mediante el servicio Forms.
1. Cree un documento PDF no interactivo mediante el servicio Output.
1. Almacene el formulario PDF en Content Services (desaprobado) mediante el servicio de administración de documentos.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de objetos de Forms, Output y Document Management**

Antes de realizar una operación de API de servicio de Forms mediante programación, cree un objeto de API de cliente de Forms. Del mismo modo, como este flujo de trabajo invoca los servicios Output y Document Management, cree tanto un objeto API de Output Client como un objeto API de Document Management Client.

**Recuperar datos de formulario mediante el servicio Forms**

Recuperar datos de formulario enviados al servicio Forms. Puede procesar los datos enviados para satisfacer los requisitos comerciales. Por ejemplo, puede almacenar datos de formulario en una base de datos empresarial. Sin embargo, para crear un documento PDF no interactivo, los datos del formulario se pasan al servicio Output.

**Cree un documento PDF no interactivo mediante el servicio Output.**

Utilice el servicio Output para crear un documento PDF no interactivo basado en un diseño de formulario y en datos de formulario XML. En el flujo de trabajo, los datos del formulario se recuperan del servicio Forms.

**Almacenar el formulario PDF en Content Services (desaprobado) mediante el servicio de administración de documentos**

Utilice la API de servicio de Document Management para almacenar un documento PDF en Content Services (desaprobado).

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de formularios](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### Creación de un documento PDF con datos XML enviados mediante la API de Java {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}

Cree un documento PDF con datos XML enviados mediante la API de Forms, Output y Document Management (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, adobe-output-client.jar y adobe-contentservices-client.jar en la ruta de clases del proyecto Java.

1. Creación de objetos de Forms, Output y Document Management

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `FormsServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.
   * Cree un `OutputClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.
   * Cree un `DocumentManagementServiceClientImpl` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recuperar datos de formulario mediante el servicio Forms

   * Invoque el `FormsServiceClient` método del `processFormSubmission` objeto y pase los valores siguientes:

      * El `com.adobe.idp.Document` objeto que contiene los datos del formulario.
      * Un valor de cadena que especifica variables de entorno, incluidos todos los encabezados HTTP relevantes. Especifique el tipo de contenido que se va a gestionar especificando uno o varios valores para la variable de `CONTENT_TYPE` entorno. Por ejemplo, para gestionar datos XML, especifique el siguiente valor de cadena para este parámetro: `CONTENT_TYPE=text/xml`.
      * Un valor de cadena que especifica el valor del `HTTP_USER_AGENT` encabezado, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Un `RenderOptionsSpec` objeto que almacena opciones de tiempo de ejecución.
      El `processFormSubmission` método devuelve un `FormsResult` objeto que contiene los resultados del envío del formulario.

   * Determine si el servicio Forms ha terminado de procesar los datos del formulario invocando el `FormsResult` método del `getAction` objeto. Si este método devuelve el valor `0`, los datos están listos para ser procesados.
   * Recuperar datos de formulario creando un `com.adobe.idp.Document` objeto invocando el `FormsResult` método `getOutputContent` del objeto. (Este objeto contiene datos de formulario que se pueden enviar al servicio Output).
   * Cree un `java.io.InputStream` objeto invocando el `java.io.DataInputStream` constructor y pasando el `com.adobe.idp.Document` objeto.
   * Cree un `org.w3c.dom.DocumentBuilderFactory` objeto llamando al `org.w3c.dom.DocumentBuilderFactory` método `newInstance` del objeto estático.
   * Cree un `org.w3c.dom.DocumentBuilder` objeto invocando el `org.w3c.dom.DocumentBuilderFactory` método `newDocumentBuilder` del objeto.
   * Cree un `org.w3c.dom.Document` objeto invocando el `org.w3c.dom.DocumentBuilder` método `parse` del objeto y pasando el `java.io.InputStream` objeto.
   * Recupere el valor de cada nodo dentro del documento XML. Una forma de realizar esta tarea es crear un método personalizado que acepte dos parámetros: el `org.w3c.dom.Document` objeto y el nombre del nodo cuyo valor desea recuperar. Este método devuelve un valor de cadena que representa el valor del nodo. En el ejemplo de código que sigue a este proceso, se llama a este método personalizado `getNodeText`. Se muestra el cuerpo de este método.


1. Cree un documento PDF no interactivo mediante el servicio Output.

   Cree un documento PDF invocando el `OutputClient` método `generatePDFOutput` del objeto y pasando los siguientes valores:

   * Un valor `TransformationFormat` enum. Para generar un documento PDF, especifique `TransformationFormat.PDF`.
   * Un valor de cadena que especifica el nombre del diseño de formulario. Asegúrese de que el diseño de formulario es compatible con los datos de formulario recuperados del servicio Forms.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentra el diseño de formulario.
   * Un `PDFOutputOptionsSpec` objeto que contiene opciones de tiempo de ejecución de PDF.
   * Un `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * El `com.adobe.idp.Document` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario. Asegúrese de que el `FormsResult` método del `getOutputContent` objeto devuelve este objeto.
   * El `generatePDFOutput` método devuelve un `OutputResult` objeto que contiene los resultados de la operación.
   * Recupere el documento PDF no interactivo invocando el `OutputResult` método `getGeneratedDoc` del objeto. Este método devuelve una `com.adobe.idp.Document` instancia que representa el documento PDF no interactivo.

1. Almacenar el formulario PDF en Content Services (desaprobado) mediante el servicio de administración de documentos

   Agregue el contenido invocando el `DocumentManagementServiceClientImpl` método del `storeContent` objeto y pasando los siguientes valores:

   * Un valor de cadena que especifica el almacén donde se agrega el contenido. La tienda predeterminada es `SpacesStore`. Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la ruta completa del espacio donde se agrega el contenido (por ejemplo, `/Company Home/Test Directory`). Este valor es un parámetro obligatorio.
   * El nombre del nodo que representa el nuevo contenido (por ejemplo, `MortgageForm.pdf`). Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica el tipo de nodo. Para agregar contenido nuevo, como un archivo PDF, especifique `{https://www.alfresco.org/model/content/1.0}content`. Este valor es un parámetro obligatorio.
   * Un `com.adobe.idp.Document` objeto que representa el contenido. Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica el valor de codificación (por ejemplo, `UTF-8`). Este valor es un parámetro obligatorio.
   * Un valor `UpdateVersionType` de enumeración que especifica cómo gestionar la información de la versión (por ejemplo, `UpdateVersionType.INCREMENT_MAJOR_VERSION` para incrementar la versión del contenido). ) Este valor es un parámetro obligatorio.
   * Una `java.util.List` instancia que especifica aspectos relacionados con el contenido. Este valor es un parámetro opcional y se puede especificar `null`.
   * Un `java.util.Map` objeto que almacena atributos de contenido.
   El `storeContent` método devuelve un `CRCResult` objeto que describe el contenido. Con un `CRCResult` objeto, puede, por ejemplo, obtener el valor de identificador único del contenido. Para realizar esta tarea, invoque el `CRCResult` método `getNodeUuid` del objeto.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
