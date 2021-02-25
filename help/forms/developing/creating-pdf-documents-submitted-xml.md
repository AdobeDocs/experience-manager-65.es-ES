---
title: Creación de Documentos PDF con datos XML enviados
seo-title: Creación de Documentos PDF con datos XML enviados
description: Utilice el servicio Forms para recuperar los datos del formulario que el usuario ha introducido en un formulario interactivo. Transfiera los datos del formulario a otra operación de servicio de AEM Forms y cree un documento PDF con los datos.
seo-description: Utilice el servicio Forms para recuperar los datos del formulario que el usuario ha introducido en un formulario interactivo. Transfiera los datos del formulario a otra operación de servicio de AEM Forms y cree un documento PDF con los datos.
uuid: 2676c614-8988-451b-ac7c-bd07731a3f5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 62490230-a24e-419d-95bb-c0bb04a03f96
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '1361'
ht-degree: 0%

---


# Creación de Documentos PDF con datos XML enviados {#creating-pdf-documents-with-submittedxml-data}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en el entorno JEE.**

## Creación de Documentos PDF con datos XML enviados {#creating-pdf-documents-with-submitted-xml-data}

Las aplicaciones basadas en la Web que permiten a los usuarios rellenar formularios interactivos requieren que los datos se envíen de nuevo al servidor. Con el servicio Forms, puede recuperar los datos del formulario que el usuario ha introducido en un formulario interactivo. A continuación, puede pasar los datos del formulario a otra operación de servicio de AEM Forms y crear un documento PDF con los datos.

>[!NOTE]
>
>Antes de leer este contenido, se recomienda tener una sólida comprensión del manejo de los formularios enviados. Conceptos como la relación entre un diseño de formulario y los datos XML enviados se tratan en Gestión de envío de Forms.

Considere el siguiente flujo de trabajo que incluye tres servicios de AEM Forms:

* Un usuario envía datos XML al servicio de Forms desde una aplicación basada en Web.
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
1. Cree objetos de Forms, Output y Documento Management.
1. Recupere los datos del formulario mediante el servicio Forms.
1. Cree un documento PDF no interactivo mediante el servicio Output.
1. Almacene el formulario PDF en Content Services (desaprobado) mediante el servicio de administración de Documentos.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de objetos de Forms, Output y Documento Management**

Antes de realizar una operación de API de servicio de Forms mediante programación, cree un objeto de API de cliente de Forms. Del mismo modo, como este flujo de trabajo invoca los servicios de Output y Documento Management, cree tanto un objeto de API de Output Client como un objeto de API de cliente de administración de Documento.

**Recuperar datos de formulario mediante el servicio Forms**

Recuperar datos de formulario enviados al servicio de Forms. Puede procesar los datos enviados para satisfacer los requisitos comerciales. Por ejemplo, puede almacenar datos de formulario en una base de datos empresarial. Sin embargo, para crear un documento PDF no interactivo, los datos del formulario se pasan al servicio Output.

**Cree un documento PDF no interactivo mediante el servicio Output.**

Utilice el servicio Output para crear un documento PDF no interactivo basado en un diseño de formulario y datos de formulario XML. En el flujo de trabajo, los datos del formulario se recuperan del servicio Forms.

**Almacenar el formulario PDF en Content Services (desaprobado) mediante el servicio de administración de Documentos**

Utilice la API de servicio de administración de Documentos para almacenar un documento PDF en Content Services (obsoleto).

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API de servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### Crear un Documento PDF con datos XML enviados mediante la API de Java {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}

Cree un documento PDF con los datos XML enviados mediante la API de Forms, Output y administración de Documentos (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, adobe-output-client.jar y adobe-contentservices-client.jar en la ruta de clases del proyecto Java.

1. Creación de objetos de Forms, Output y Documento Management

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `FormsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.
   * Cree un objeto `OutputClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.
   * Cree un objeto `DocumentManagementServiceClientImpl` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Recuperar datos de formulario mediante el servicio Forms

   * Invoque el método `FormsServiceClient` del objeto `processFormSubmission` y pase los siguientes valores:

      * El objeto `com.adobe.idp.Document` que contiene los datos del formulario.
      * Un valor de cadena que especifica variables de entorno, incluidos todos los encabezados HTTP relevantes. Especifique el tipo de contenido que se va a gestionar especificando uno o varios valores para la variable de entorno `CONTENT_TYPE`. Por ejemplo, para gestionar datos XML, especifique el siguiente valor de cadena para este parámetro: `CONTENT_TYPE=text/xml`.
      * Un valor de cadena que especifica el valor del encabezado `HTTP_USER_AGENT`, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Un objeto `RenderOptionsSpec` que almacena opciones de tiempo de ejecución.

      El método `processFormSubmission` devuelve un objeto `FormsResult` que contiene los resultados del envío del formulario.

   * Determine si el servicio de Forms ha terminado de procesar los datos del formulario invocando el método `FormsResult` del objeto `getAction`. Si este método devuelve el valor `0`, los datos están listos para ser procesados.
   * Recupere los datos del formulario creando un objeto `com.adobe.idp.Document` invocando el método `FormsResult` del objeto `getOutputContent`. (Este objeto contiene datos de formulario que se pueden enviar al servicio Output).
   * Cree un objeto `java.io.InputStream` invocando el constructor `java.io.DataInputStream` y pasando el objeto `com.adobe.idp.Document`.
   * Cree un objeto `org.w3c.dom.DocumentBuilderFactory` llamando al método `org.w3c.dom.DocumentBuilderFactory` del objeto estático `newInstance`.
   * Cree un objeto `org.w3c.dom.DocumentBuilder` invocando el método `org.w3c.dom.DocumentBuilderFactory` del objeto `newDocumentBuilder`.
   * Cree un objeto `org.w3c.dom.Document` invocando el método `org.w3c.dom.DocumentBuilder` del objeto `parse` y pasando el objeto `java.io.InputStream`.
   * Recupere el valor de cada nodo dentro del documento XML. Una forma de lograr esta tarea es crear un método personalizado que acepte dos parámetros: el objeto `org.w3c.dom.Document` y el nombre del nodo cuyo valor desea recuperar. Este método devuelve un valor de cadena que representa el valor del nodo. En el ejemplo de código que sigue a este proceso, este método personalizado se denomina `getNodeText`. Se muestra el cuerpo de este método.


1. Cree un documento PDF no interactivo mediante el servicio Output.

   Cree un documento PDF invocando el método `OutputClient` del objeto `generatePDFOutput` y pasando los valores siguientes:

   * Un valor de enumeración `TransformationFormat`. Para generar un documento PDF, especifique `TransformationFormat.PDF`.
   * Un valor de cadena que especifica el nombre del diseño de formulario. Asegúrese de que el diseño de formulario es compatible con los datos de formulario recuperados del servicio Forms.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentra el diseño de formulario.
   * Un objeto `PDFOutputOptionsSpec` que contiene opciones de tiempo de ejecución de PDF.
   * Un objeto `RenderOptionsSpec` que contiene opciones de procesamiento en tiempo de ejecución.
   * El objeto `com.adobe.idp.Document` que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario. Asegúrese de que el método `FormsResult` del objeto `getOutputContent` devuelve este objeto.
   * El método `generatePDFOutput` devuelve un objeto `OutputResult` que contiene los resultados de la operación.
   * Recupere el documento PDF no interactivo invocando el método `OutputResult` del objeto `getGeneratedDoc`. Este método devuelve una instancia `com.adobe.idp.Document` que representa el documento PDF no interactivo.

1. Almacenar el formulario PDF en Content Services (desaprobado) mediante el servicio de administración de Documentos

   Añada el contenido invocando el método `DocumentManagementServiceClientImpl` del objeto `storeContent` y pasando los valores siguientes:

   * Un valor de cadena que especifica el almacén donde se agrega el contenido. El almacén predeterminado es `SpacesStore`. Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la ruta completa del espacio donde se agrega el contenido (por ejemplo, `/Company Home/Test Directory`). Este valor es un parámetro obligatorio.
   * El nombre del nodo que representa el nuevo contenido (por ejemplo, `MortgageForm.pdf`). Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica el tipo de nodo. Para agregar contenido nuevo, como un archivo PDF, especifique `{https://www.alfresco.org/model/content/1.0}content`. Este valor es un parámetro obligatorio.
   * Un objeto `com.adobe.idp.Document` que representa el contenido. Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica el valor de codificación (por ejemplo, `UTF-8`). Este valor es un parámetro obligatorio.
   * Un valor de lista desglosada `UpdateVersionType` que especifica cómo administrar la información de la versión (por ejemplo, `UpdateVersionType.INCREMENT_MAJOR_VERSION` para incrementar la versión del contenido. ) Este valor es un parámetro obligatorio.
   * Instancia `java.util.List` que especifica aspectos relacionados con el contenido. Este valor es un parámetro opcional y puede especificar `null`.
   * Un objeto `java.util.Map` que almacena atributos de contenido.

   El método `storeContent` devuelve un objeto `CRCResult` que describe el contenido. Mediante el uso de un objeto `CRCResult`, puede, por ejemplo, obtener el valor de identificador único del contenido. Para realizar esta tarea, invoque el método `CRCResult` del objeto `getNodeUuid`.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
