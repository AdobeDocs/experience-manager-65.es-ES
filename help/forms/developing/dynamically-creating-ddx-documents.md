---
title: Creación dinámica de documentos DDX
seo-title: Creación dinámica de documentos DDX
description: nulo
seo-description: nulo
uuid: b73e8069-6c9f-4517-a0ae-f3d503191d2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2ad227de-68a8-446f-8c4f-a33a6f95bec8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Creación dinámica de documentos DDX {#dynamically-creating-ddx-documents}

Puede crear dinámicamente un documento DDX que pueda utilizarse para realizar una operación de ensamblador. La creación dinámica de un documento DDX permite utilizar valores en el documento DDX que se obtienen durante la ejecución. Para crear dinámicamente un documento DDX, utilice clases que pertenezcan al lenguaje de programación que esté utilizando. Por ejemplo, si está desarrollando la aplicación cliente mediante Java, utilice clases que pertenezcan al `org.w3c.dom.*`paquete. Del mismo modo, si utiliza Microsoft .NET, utilice clases que pertenezcan al `System.Xml` espacio de nombres.

Para poder pasar el documento DDX al servicio de ensamblador, convierta el XML de una `org.w3c.dom.Document` instancia a una `com.adobe.idp.Document` instancia. Si utiliza servicios Web, convierta el XML del tipo de datos utilizado para crear el XML (por ejemplo, `XmlDocument`) a una `BLOB` instancia.

Para este análisis, supongamos que se crea dinámicamente el siguiente documento DDX.

```as3
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
>Para obtener más información sobre el servicio Compilador, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y Referencia](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Resumen de los pasos {#summary-of-steps}

Para desmontar un documento PDF mediante un documento DDX creado dinámicamente, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de ensamblador de PDF.
1. Cree el documento DDX.
1. Convierta el documento DDX.
1. Configure las opciones de tiempo de ejecución.
1. Desmontar el documento PDF.
1. Guarde los documentos PDF desmontados.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

**Crear un cliente de ensamblador de PDF**

Antes de realizar una operación de ensamblador mediante programación, cree un cliente de servicio de ensamblador.

**Crear el documento DDX**

Cree un documento DDX utilizando el lenguaje de programación que está utilizando. Para crear un documento DDX que desmonte un documento PDF, asegúrese de que contiene el `PDFsFromBookmarks` elemento . Convierta el tipo de datos utilizado para crear el documento DDX en una `com.adobe.idp.Document` instancia si utiliza la API de Java. Si utiliza servicios Web, convierta el tipo de datos en una `BLOB` instancia.

**Convertir el documento DDX**

Un documento DDX creado mediante `org.w3c.dom` clases debe convertirse en un `com.adobe.idp.Document` objeto. Para realizar esta tarea al utilizar la API de Java, utilice clases de transformación XML de Java. Si utiliza servicios Web, convierta el documento DDX en un `BLOB` objeto.

**Hacer referencia a un documento PDF para desmontarlo**

Para desmontar un documento PDF, haga referencia a un archivo PDF que represente el documento PDF que desea desmontar. Cuando se pasa al servicio Compilador, se devuelve un documento PDF independiente para cada marcador de nivel 1 del documento.

**Definición de opciones de tiempo de ejecución**

Puede definir opciones en tiempo de ejecución que controlen el comportamiento del servicio de ensamblador mientras realiza un trabajo. Por ejemplo, puede definir una opción que indique al servicio Ensamblador que continúe procesando un trabajo si se produce un error. Para definir las opciones de tiempo de ejecución, se utiliza un `AssemblerOptionSpec` objeto.

**Desmontar el documento PDF**

Desmonte el documento PDF invocando la `invokeDDX` operación. Pase el documento DDX que se creó dinámicamente. El servicio Ensamblador devuelve documentos PDF desmontados dentro de un objeto de colección.

**Guardar los documentos PDF desmontados**

Todos los documentos PDF desmontados se devuelven dentro de un objeto de colección. Repita el objeto de colección y guarde cada documento PDF como archivo PDF.

**Consulte también**

[Creación dinámica de un documento DDX mediante la API de Java](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[Creación dinámica de un documento DDX mediante la API de servicio web](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Desensamblar documentos PDF mediante programación](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Creación dinámica de un documento DDX mediante la API de Java {#dynamically-create-a-ddx-document-using-the-java-api}

Crear dinámicamente un documento DDX y desmontar un documento PDF mediante la API de servicio de ensamblador (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de ensamblador de PDF.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `AssemblerServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Cree el documento DDX.

   * Cree un objeto Java `DocumentBuilderFactory` llamando al `DocumentBuilderFactory` método de la `newInstance` clase.
   * Cree un objeto Java `DocumentBuilder` llamando al `DocumentBuilderFactory` método `newDocumentBuilder` del objeto.
   * Llame al `DocumentBuilder` método del `newDocument` objeto para crear una instancia de un `org.w3c.dom.Document` objeto.
   * Cree el elemento raíz del documento DDX invocando el `org.w3c.dom.Document` método `createElement` del objeto. Este método crea un `Element` objeto que representa el elemento raíz. Pase un valor de cadena que represente el nombre del elemento al `createElement` método. Convierta el valor devuelto a `Element`. A continuación, defina un valor para el elemento secundario llamando a su `setAttribute` método. Finalmente, anexe el elemento al elemento de encabezado llamando al método `appendChild` del elemento de encabezado y pase el objeto de elemento secundario como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * Cree el `PDFsFromBookmarks` elemento llamando al `Document` método `createElement` del objeto. Pase un valor de cadena que represente el nombre del elemento al `createElement` método. Convierta el valor devuelto a `Element`. Establezca un valor para el `PDFsFromBookmarks` elemento llamando a su `setAttribute` método. Anexe el `PDFsFromBookmarks` elemento al `DDX` elemento llamando al `appendChild` método del elemento DDX. Pase el objeto `PDFsFromBookmarks` element como un argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * Cree un `PDF` elemento llamando al `Document` método `createElement` del objeto. Pase un valor de cadena que represente el nombre del elemento. Convierta el valor devuelto a `Element`. Establezca un valor para el `PDF` elemento llamando a su `setAttribute` método. Anexe el `PDF` elemento al `PDFsFromBookmarks` elemento llamando al `PDFsFromBookmarks` método `appendChild` del elemento. Pase el objeto `PDF` element como un argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. Convierta el documento DDX.

   * Cree un `javax.xml.transform.Transformer` objeto invocando el `javax.xml.transform.Transformer` método estático `newInstance` del objeto.
   * Cree un `Transformer` objeto invocando el `TransformerFactory` método `newTransformer` del objeto.
   * Cree un `ByteArrayOutputStream` objeto con su constructor.
   * Cree un `javax.xml.transform.dom.DOMSource` objeto con su constructor. Pase el `org.w3c.dom.Document` objeto que representa el documento DDX.
   * Cree un `javax.xml.transform.dom.DOMSource` objeto utilizando su constructor y pasando el `ByteArrayOutputStream` objeto.
   * Rellene el objeto Java `ByteArrayOutputStream` invocando el `javax.xml.transform.Transformer` método `transform` del objeto. Pase los objetos `javax.xml.transform.dom.DOMSource` y los `javax.xml.transform.stream.StreamResult` .
   * Cree una matriz de bytes y asigne el tamaño del `ByteArrayOutputStream` objeto a la matriz de bytes.
   * Rellene la matriz de bytes invocando el `ByteArrayOutputStream` método `toByteArray` del objeto.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando la matriz de bytes.

1. Haga referencia a un documento PDF para desmontarlo.

   * Cree un `java.util.Map` objeto que se utilice para almacenar documentos PDF de entrada mediante un `HashMap` constructor.
   * Cree un `java.io.FileInputStream` objeto utilizando su constructor y pasando la ubicación del documento PDF que desea desmontar.
   * Create a `com.adobe.idp.Document` object. Pase el `java.io.FileInputStream` objeto que contiene el documento PDF para desmontarlo.
   * Agregue una entrada al `java.util.Map` objeto invocando su `put` método y pasando los siguientes argumentos:

      * Un valor de cadena que representa el nombre de la clave. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX. (En el documento DDX creado dinámicamente, el valor es `AssemblerResultPDF.pdf`).
      * Un `com.adobe.idp.Document` objeto que contiene el documento PDF que se va a desmontar.

1. Configure las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` objeto que almacene opciones de tiempo de ejecución mediante su constructor.
   * Configure las opciones de tiempo de ejecución para cumplir los requisitos comerciales invocando un método que pertenece al `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Ensamblador que continúe procesando un trabajo cuando se produzca un error, invoque el `AssemblerOptionSpec` método del `setFailOnError` objeto y pase `false`.

1. Desmontar el documento PDF.

   Invoque el `AssemblerServiceClient` método del `invokeDDX` objeto y pase los valores siguientes:

   * Un `com.adobe.idp.Document` objeto que representa el documento DDX creado dinámicamente
   * Un `java.util.Map` objeto que contiene el documento PDF que se va a desmontar
   * Un `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica las opciones de tiempo de ejecución, incluyendo la fuente predeterminada y el nivel de registro de trabajos
   El `invokeDDX` método devuelve un `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contiene los documentos PDF desensamblados y las excepciones que se hayan producido.

1. Guarde los documentos PDF desmontados.

   Para obtener los documentos PDF desmontados, realice las siguientes acciones:

   * Invocar el `AssemblerResult` método del `getDocuments` objeto. Este método devuelve un `java.util.Map` objeto.
   * Repita el `java.util.Map` objeto hasta que encuentre el `com.adobe.idp.Document` objeto resultante.
   * Invocar el `com.adobe.idp.Document` método del `copyToFile` objeto para extraer el documento PDF.

**Consulte también**

[Inicio rápido (modo SOAP): Creación dinámica de un documento DDX mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Creación dinámica de un documento DDX mediante la API de servicio web {#dynamically-create-a-ddx-document-using-the-web-service-api}

Crear dinámicamente un documento DDX y desmontar un documento PDF mediante la API de servicio de ensamblador (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL al configurar una referencia de servicio: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de ensamblador de PDF.

   * Cree un `AssemblerServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `AssemblerServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio.
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `AssemblerServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Cree el documento DDX.

   * Cree un `System.Xml.XmlElement` objeto con su constructor.
   * Cree el elemento raíz del documento DDX invocando el `XmlElement` método `CreateElement` del objeto. Este método crea un `Element` objeto que representa el elemento raíz. Pase un valor de cadena que represente el nombre del elemento al `CreateElement` método. Establezca un valor para el elemento DDX llamando a su `SetAttribute` método. Finalmente, anexe el elemento al documento DDX llamando al `XmlElement` método del `AppendChild` objeto. Pase el objeto DDX como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * Cree el `PDFsFromBookmarks` elemento del documento DDX llamando al `XmlElement` método `CreateElement` del objeto. Pase un valor de cadena que represente el nombre del elemento al `CreateElement` método. A continuación, establezca un valor para el elemento llamando a su `SetAttribute` método . Anexe el `PDFsFromBookmarks` elemento al elemento raíz llamando al `DDX` método `AppendChild` del elemento. Pase el objeto `PDFsFromBookmarks` element como un argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * Cree el `PDF` elemento del documento DDX llamando al `XmlElement` método `CreateElement` del objeto. Pase un valor de cadena que represente el nombre del elemento al `CreateElement` método. A continuación, defina un valor para el elemento secundario llamando a su `SetAttribute` método. Anexe el `PDF` elemento al `PDFsFromBookmarks` elemento llamando al `PDFsFromBookmarks` método `AppendChild` del elemento. Pase el objeto `PDF` element como un argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. Convierta el documento DDX.

   * Cree un `System.IO.MemoryStream` objeto con su constructor.
   * Rellene el `MemoryStream` objeto con el documento DDX utilizando el `XmlElement` objeto que representa el documento DDX. Invocar el `XmlElement` método del `Save` objeto y pasar el `MemoryStream` objeto.
   * Cree una matriz de bytes y rellénela con datos ubicados en el `MemoryStream` objeto. El siguiente código muestra esta lógica de aplicación:

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * Create a `BLOB` object. Asigne la matriz de bytes al `BLOB` campo del `MTOM` objeto.

1. Haga referencia a un documento PDF para desmontarlo.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar el documento PDF de entrada. Este `BLOB` objeto se pasa al `invokeOneDocument` como argumento.
   * Cree un `System.IO.FileStream` objeto invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` propiedad al contenido de la matriz de bytes.

1. Configure las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` objeto que almacene opciones de tiempo de ejecución mediante su constructor.
   * Configure las opciones de tiempo de ejecución para cumplir los requisitos comerciales asignando un valor a un miembro de datos que pertenece al `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Ensamblador que continúe procesando un trabajo cuando se produzca un error, asigne `false` al miembro de datos del `AssemblerOptionSpec` objeto `failOnError` .

1. Desmontar el documento PDF.

   Invoque el `AssemblerServiceClient` método del `invokeDDX` objeto y pase los valores siguientes:

   * Un `BLOB` objeto que representa el documento DDX creado dinámicamente
   * La `mapItem` matriz que contiene el documento PDF de entrada
   * Un `AssemblerOptionSpec` objeto que especifica opciones de tiempo de ejecución
   El `invokeDDX` método devuelve un `AssemblerResult` objeto que contiene los resultados del trabajo y las excepciones que se hayan producido.

1. Guarde los documentos PDF desmontados.

   Para obtener los documentos PDF recién creados, realice las siguientes acciones:

   * Acceda al `AssemblerResult` campo del `documents` objeto, que es un `Map` objeto que contiene los documentos PDF desensamblados.
   * Repita el `Map` objeto para obtener cada documento resultante. A continuación, convierta los miembros de la matriz `value` a un `BLOB`.
   * Extraiga los datos binarios que representan el documento PDF accediendo a la propiedad del `BLOB` objeto `MTOM` . Esto devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también**

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
