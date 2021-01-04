---
title: Creación dinámica de Documentos DDX
seo-title: Creación dinámica de Documentos DDX
description: Cree un documento DDX dinámicamente mediante la API de Java y la API de servicio Web. La creación dinámica de un documento DDX le permite utilizar valores en el documento DDX que se obtienen durante la ejecución.
seo-description: Cree un documento DDX dinámicamente mediante la API de Java y la API de servicio Web. La creación dinámica de un documento DDX le permite utilizar valores en el documento DDX que se obtienen durante la ejecución.
uuid: b73e8069-6c9f-4517-a0ae-f3d503191d2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2ad227de-68a8-446f-8c4f-a33a6f95bec8
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '2185'
ht-degree: 0%

---


# Creación dinámica de Documentos DDX {#dynamically-creating-ddx-documents}

Puede crear dinámicamente un documento DDX que pueda utilizarse para realizar una operación de ensamblador. La creación dinámica de un documento DDX le permite utilizar valores en el documento DDX que se obtienen durante la ejecución. Para crear dinámicamente un documento DDX, utilice clases que pertenezcan al lenguaje de programación que esté utilizando. Por ejemplo, si está desarrollando la aplicación cliente mediante Java, utilice clases que pertenezcan al paquete `org.w3c.dom.*`. Del mismo modo, si utiliza Microsoft .NET, utilice clases que pertenezcan a la Área de nombres `System.Xml`.

Antes de pasar el documento DDX al servicio de ensamblador, convierta el XML de una instancia `org.w3c.dom.Document` a una instancia `com.adobe.idp.Document`. Si utiliza servicios Web, convierta el XML del tipo de datos utilizado para crear el XML (por ejemplo, `XmlDocument`) a una instancia `BLOB`.

Para este análisis, supongamos que se crea dinámicamente el siguiente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

Este documento DDX desmonta un documento PDF. Se recomienda familiarizarse con el desmontaje de documentos PDF.

>[!NOTE]
>
>Para obtener más información sobre el servicio de ensamblador, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y Referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para desmontar un documento PDF mediante un documento DDX creado dinámicamente, lleve a cabo las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de ensamblador de PDF.
1. Cree el documento DDX.
1. Convierta el documento DDX.
1. Configure las opciones de tiempo de ejecución.
1. Desmonte el documento PDF.
1. Guarde los documentos PDF desmontados.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requerido si AEM Forms se implementa en JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss)

**Crear un cliente de ensamblador de PDF**

Antes de realizar una operación de ensamblador mediante programación, cree un cliente de servicio de ensamblador.

**Creación del documento DDX**

Cree un documento DDX utilizando el lenguaje de programación que está utilizando. Para crear un documento DDX que desmonte un documento PDF, asegúrese de que contiene el elemento `PDFsFromBookmarks`. Convierta el tipo de datos utilizado para crear el documento DDX en una instancia `com.adobe.idp.Document` si utiliza la API de Java. Si utiliza servicios Web, convierta el tipo de datos en una instancia `BLOB`.

**Convertir el documento DDX**

Un documento DDX que se crea mediante clases `org.w3c.dom` debe convertirse en un objeto `com.adobe.idp.Document`. Para realizar esta tarea al utilizar la API de Java, utilice clases de transformación XML de Java. Si utiliza servicios Web, convierta el documento DDX en un objeto `BLOB`.

**Hacer referencia a un documento PDF para desmontarlo**

Para desmontar un documento PDF, haga referencia a un archivo PDF que represente el documento PDF que desea desmontar. Cuando se pasa al servicio Compilador, se devuelve un documento PDF independiente para cada marcador de nivel 1 del documento.

**Definición de opciones de tiempo de ejecución**

Puede definir opciones en tiempo de ejecución que controlen el comportamiento del servicio de ensamblador mientras realiza un trabajo. Por ejemplo, puede definir una opción que indique al servicio Ensamblador que continúe procesando un trabajo si se produce un error. Para establecer las opciones de tiempo de ejecución, se utiliza un objeto `AssemblerOptionSpec`.

**Desmontar el documento PDF**

Para desmontar el documento PDF, invoque la operación `invokeDDX`. Transfiera el documento DDX que se creó dinámicamente. El servicio Ensamblador devuelve documentos PDF desmontados dentro de un objeto de colección.

**Guardar los documentos PDF desmontados**

Todos los documentos PDF desmontados se devuelven dentro de un objeto de colección. Repita el objeto de colección y guarde cada documento PDF como archivo PDF.

**Consulte también**

[Creación dinámica de un documento DDX mediante la API de Java](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[Creación dinámica de un documento DDX mediante la API de servicio web](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Desensamblar Documentos PDF mediante programación](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Crear dinámicamente un documento DDX con la API de Java {#dynamically-create-a-ddx-document-using-the-java-api}

Cree dinámicamente un documento DDX y desensamble un documento PDF mediante la API de servicio de ensamblador (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de ensamblador de PDF.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `AssemblerServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Cree el documento DDX.

   * Cree un objeto Java `DocumentBuilderFactory` llamando al método `DocumentBuilderFactory` class’ `newInstance`.
   * Cree un objeto Java `DocumentBuilder` llamando al método `DocumentBuilderFactory` del objeto `newDocumentBuilder`.
   * Llame al método `DocumentBuilder` del objeto `newDocument` para crear una instancia de un objeto `org.w3c.dom.Document`.
   * Cree el elemento raíz del documento DDX invocando el método `org.w3c.dom.Document` del objeto `createElement`. Este método crea un objeto `Element` que representa el elemento raíz. Pase un valor de cadena que represente el nombre del elemento al método `createElement`. Convierta el valor devuelto a `Element`. A continuación, establezca un valor para el elemento secundario llamando a su método `setAttribute`. Finalmente, anexe el elemento al elemento de encabezado llamando al método `appendChild` del elemento de encabezado y pase el objeto de elemento secundario como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * Cree el elemento `PDFsFromBookmarks` llamando al método `Document` del objeto `createElement`. Pase un valor de cadena que represente el nombre del elemento al método `createElement`. Convierta el valor devuelto a `Element`. Establezca un valor para el elemento `PDFsFromBookmarks` llamando a su método `setAttribute`. Anexe el elemento `PDFsFromBookmarks` al elemento `DDX` llamando al método `appendChild` del elemento DDX. Pase el objeto de elemento `PDFsFromBookmarks` como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * Cree un elemento `PDF` llamando al método `Document` del objeto `createElement`. Pase un valor de cadena que represente el nombre del elemento. Convierta el valor devuelto a `Element`. Establezca un valor para el elemento `PDF` llamando a su método `setAttribute`. Anexe el elemento `PDF` al elemento `PDFsFromBookmarks` llamando al método `PDFsFromBookmarks` del elemento `appendChild`. Pase el objeto de elemento `PDF` como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. Convierta el documento DDX.

   * Cree un objeto `javax.xml.transform.Transformer` invocando el método estático `javax.xml.transform.Transformer` del objeto `newInstance`.
   * Cree un objeto `Transformer` invocando el método `TransformerFactory` del objeto `newTransformer`.
   * Cree un objeto `ByteArrayOutputStream` utilizando su constructor.
   * Cree un objeto `javax.xml.transform.dom.DOMSource` utilizando su constructor. Pase el objeto `org.w3c.dom.Document` que representa el documento DDX.
   * Cree un objeto `javax.xml.transform.dom.DOMSource` utilizando su constructor y pasando el objeto `ByteArrayOutputStream`.
   * Rellene el objeto Java `ByteArrayOutputStream` invocando el método `javax.xml.transform.Transformer` del objeto `transform`. Pase los objetos `javax.xml.transform.dom.DOMSource` y `javax.xml.transform.stream.StreamResult`.
   * Cree una matriz de bytes y asigne el tamaño del objeto `ByteArrayOutputStream` a la matriz de bytes.
   * Rellene la matriz de bytes invocando el método `ByteArrayOutputStream` del objeto `toByteArray`.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando la matriz de bytes.

1. Haga referencia a un documento PDF para desmontarlo.

   * Cree un objeto `java.util.Map` que se utilice para almacenar documentos PDF de entrada mediante un constructor `HashMap`.
   * Cree un objeto `java.io.FileInputStream` utilizando su constructor y pasando la ubicación del documento PDF para desmontarlo.
   * Cree un objeto `com.adobe.idp.Document`. Pase el objeto `java.io.FileInputStream` que contiene el documento PDF para desmontarlo.
   * Añada una entrada al objeto `java.util.Map` invocando su método `put` y pasando los siguientes argumentos:

      * Un valor de cadena que representa el nombre de la clave. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX. (En el documento DDX que se crea dinámicamente, el valor es `AssemblerResultPDF.pdf`).
      * Objeto `com.adobe.idp.Document` que contiene el documento PDF que se va a desmontar.

1. Configure las opciones de tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene las opciones de tiempo de ejecución mediante su constructor.
   * Configure las opciones de tiempo de ejecución para satisfacer los requisitos comerciales invocando un método que pertenece al objeto `AssemblerOptionSpec`. Por ejemplo, para indicar al servicio Ensamblador que continúe procesando un trabajo cuando se produzca un error, invoque el método `AssemblerOptionSpec` del objeto `setFailOnError` y pase `false`.

1. Desmonte el documento PDF.

   Invoque el método `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que representa el documento DDX creado dinámicamente
   * Un objeto `java.util.Map` que contiene el documento PDF que se va a desmontar
   * Un objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones de tiempo de ejecución, incluyendo la fuente predeterminada y el nivel de registro de trabajo

   El método `invokeDDX` devuelve un objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene los documentos PDF desmontados y las excepciones que se hayan producido.

1. Guarde los documentos PDF desmontados.

   Para obtener los documentos PDF desmontados, realice las siguientes acciones:

   * Invocar el método `AssemblerResult` del objeto `getDocuments`. Este método devuelve un objeto `java.util.Map`.
   * Repita el objeto `java.util.Map` hasta que encuentre el objeto `com.adobe.idp.Document` resultante.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para extraer el documento PDF.

**Consulte también**

[Inicio rápido (modo SOAP): Creación dinámica de un documento DDX mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Crear dinámicamente un documento DDX mediante la API de servicio Web {#dynamically-create-a-ddx-document-using-the-web-service-api}

Cree dinámicamente un documento DDX y desmonte un documento PDF mediante la API de servicio de ensamblador (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL al configurar una referencia de servicio: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de ensamblador de PDF.

   * Cree un objeto `AssemblerServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `AssemblerServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). No es necesario usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio.
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `AssemblerServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Cree el documento DDX.

   * Cree un objeto `System.Xml.XmlElement` utilizando su constructor.
   * Cree el elemento raíz del documento DDX invocando el método `XmlElement` del objeto `CreateElement`. Este método crea un objeto `Element` que representa el elemento raíz. Pase un valor de cadena que represente el nombre del elemento al método `CreateElement`. Establezca un valor para el elemento DDX llamando a su método `SetAttribute`. Finalmente, anexe el elemento al documento DDX llamando al método `XmlElement` del objeto `AppendChild`. Pase el objeto DDX como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * Cree el elemento `PDFsFromBookmarks` del documento DDX llamando al método `XmlElement` del objeto `CreateElement`. Pase un valor de cadena que represente el nombre del elemento al método `CreateElement`. A continuación, establezca un valor para el elemento llamando a su método `SetAttribute`. Anexe el elemento `PDFsFromBookmarks` al elemento raíz llamando al método `DDX` del elemento `AppendChild`. Pase el objeto de elemento `PDFsFromBookmarks` como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * Cree el elemento `PDF` del documento DDX llamando al método `XmlElement` del objeto `CreateElement`. Pase un valor de cadena que represente el nombre del elemento al método `CreateElement`. A continuación, establezca un valor para el elemento secundario llamando a su método `SetAttribute`. Anexe el elemento `PDF` al elemento `PDFsFromBookmarks` llamando al método `PDFsFromBookmarks` del elemento `AppendChild`. Pase el objeto de elemento `PDF` como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. Convierta el documento DDX.

   * Cree un objeto `System.IO.MemoryStream` utilizando su constructor.
   * Rellene el objeto `MemoryStream` con el documento DDX utilizando el objeto `XmlElement` que representa el documento DDX. Invoque el método `XmlElement` del objeto `Save` y pase el objeto `MemoryStream`.
   * Cree una matriz de bytes y rellénela con datos ubicados en el objeto `MemoryStream`. El siguiente código muestra esta lógica de aplicación:

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * Cree un objeto `BLOB`. Asigne la matriz de bytes al campo `BLOB` del objeto `MTOM`.

1. Haga referencia a un documento PDF para desmontarlo.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el documento PDF de entrada. Este objeto `BLOB` se pasa a `invokeOneDocument` como argumento.
   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` el contenido de la matriz de bytes.

1. Configure las opciones de tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene las opciones de tiempo de ejecución mediante su constructor.
   * Configure las opciones de tiempo de ejecución para satisfacer los requisitos comerciales asignando un valor a un miembro de datos que pertenece al objeto `AssemblerOptionSpec`. Por ejemplo, para indicar al servicio Ensamblador que continúe procesando un trabajo cuando se produzca un error, asigne `false` al miembro de datos `AssemblerOptionSpec` del objeto `failOnError`.

1. Desmonte el documento PDF.

   Invoque el método `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento DDX creado dinámicamente
   * La matriz `mapItem` que contiene el documento PDF de entrada
   * Un objeto `AssemblerOptionSpec` que especifica opciones de tiempo de ejecución

   El método `invokeDDX` devuelve un objeto `AssemblerResult` que contiene los resultados del trabajo y las excepciones que se hayan producido.

1. Guarde los documentos PDF desmontados.

   Para obtener los documentos PDF recién creados, realice las siguientes acciones:

   * Acceda al campo `AssemblerResult` del objeto `documents`, que es un objeto `Map` que contiene los documentos PDF desmontados.
   * Repita el objeto `Map` para obtener cada documento resultante. A continuación, convierta el `value` miembro del arreglo de discos en un `BLOB`.
   * Extraiga los datos binarios que representan el documento PDF accediendo a la propiedad `BLOB` del objeto `MTOM`. Esto devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
