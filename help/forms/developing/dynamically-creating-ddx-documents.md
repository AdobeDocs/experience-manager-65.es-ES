---
title: Creación dinámica de documentos DDX
description: Cree un documento DDX de forma dinámica mediante la API de Java y la API de servicio web. La creación dinámica de un documento DDX permite utilizar valores en el documento DDX que se obtienen durante el tiempo de ejecución.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: b3c19c82-e26f-4dc8-b846-6aec705cee08
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '2153'
ht-degree: 0%

---

# Creación dinámica de documentos DDX {#dynamically-creating-ddx-documents}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

Puede crear dinámicamente un documento DDX que se pueda utilizar para realizar una operación de Assembler. La creación dinámica de un documento DDX permite utilizar valores en el documento DDX que se obtienen durante el tiempo de ejecución. Para crear dinámicamente un documento DDX, utilice clases que pertenezcan al lenguaje de programación que esté utilizando. Por ejemplo, si está desarrollando la aplicación cliente utilizando Java, utilice clases que pertenezcan a `org.w3c.dom.*`paquete. Del mismo modo, si utiliza Microsoft .NET, utilice clases que pertenezcan a la variable `System.Xml` namespace.

Antes de poder pasar el documento DDX al servicio Assembler, convierta el XML de un `org.w3c.dom.Document` instancia a `com.adobe.idp.Document` ejemplo. Si utiliza servicios web, convierta el XML del tipo de datos utilizado para crear el XML (por ejemplo, `XmlDocument`) a un `BLOB` ejemplo.

Para esta discusión, suponga que el siguiente documento DDX se crea dinámicamente.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

Este documento DDX desmonta un documento de PDF. Se recomienda que esté familiarizado con el desmontaje de documentos del PDF.

>[!NOTE]
>
>Para obtener más información sobre el servicio Assembler, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para desmontar un documento de PDF mediante un documento DDX creado dinámicamente, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDF Assembler.
1. Cree el documento DDX.
1. Convierta el documento DDX.
1. Establecer opciones en tiempo de ejecución.
1. Desmontar el documento del PDF.
1. Guarde los documentos del PDF desmontados.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

**Crear un cliente de PDF Assembler**

Para poder realizar mediante programación una operación de Assembler, cree un cliente de servicio Assembler.

**Creación del documento DDX**

Cree un documento DDX utilizando el lenguaje de programación que está utilizando. Para crear un documento DDX que desensambla un documento de PDF, asegúrese de que contiene el `PDFsFromBookmarks` Elemento. Convierta el tipo de datos utilizado para crear el documento DDX en un `com.adobe.idp.Document` instancia de si utiliza la API de Java. Si utiliza servicios web, convierta el tipo de datos a un `BLOB` ejemplo.

**Conversión del documento DDX**

Un documento DDX creado mediante `org.w3c.dom` las clases deben convertirse en un `com.adobe.idp.Document` objeto. Para realizar esta tarea al utilizar la API de Java, utilice las clases de transformación XML de Java. Si utiliza servicios web, convierta el documento DDX en un `BLOB` objeto.

**Hacer referencia a un documento de PDF para desmontar**

Para desmontar un documento de PDF, haga referencia a un fichero de PDF que represente el documento de PDF que se va a desmontar. Cuando se pasa al servicio Assembler, se devuelve un documento de PDF independiente para cada marcador de nivel 1 del documento.

**Establecer opciones en tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlen el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede establecer una opción que indique al servicio Assembler que continúe procesando un trabajo si se produce un error. Para establecer las opciones en tiempo de ejecución, se utiliza un `AssemblerOptionSpec` objeto.

**Desmontar el documento del PDF**

Desmontar el documento del PDF invocando el `invokeDDX` operación. Pase el documento DDX creado dinámicamente. El servicio Assembler devuelve documentos de PDF desensamblados dentro de un objeto de colección.

**Guardar los documentos de PDF desensamblados**

Todos los documentos de PDF desensamblados se devuelven dentro de un objeto de colección. Recorra en iteración el objeto de colección y guarde cada documento de PDF como un archivo de PDF.

**Consulte también**

[Crear dinámicamente un documento DDX mediante la API de Java](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[Crear dinámicamente un documento DDX mediante la API de servicio web](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Desmontaje programático de documentos PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Crear dinámicamente un documento DDX mediante la API de Java {#dynamically-create-a-ddx-document-using-the-java-api}

Cree de forma dinámica un documento DDX y desmonte un documento de PDF mediante la API del servicio Assembler (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de PDF Assembler.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `AssemblerServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Cree el documento DDX.

   * Crear un Java `DocumentBuilderFactory` llamando a la función `DocumentBuilderFactory` class&#39; `newInstance` método.
   * Crear un Java `DocumentBuilder` llamando a la función `DocumentBuilderFactory` del objeto `newDocumentBuilder` método.
   * Llame a `DocumentBuilder` del objeto `newDocument` método para crear una instancia de `org.w3c.dom.Document` objeto.
   * Cree el elemento raíz del documento DDX invocando el `org.w3c.dom.Document` del objeto `createElement` método. Este método crea un `Element` que representa el elemento raíz. Pase un valor de cadena que represente el nombre del elemento a `createElement` método. Convierta el valor devuelto en `Element`. A continuación, establezca un valor para el elemento secundario llamando a su `setAttribute` método. Finalmente, anexe el elemento al elemento header llamando al método `appendChild` y pase el objeto de elemento secundario como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:
     ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * Cree el `PDFsFromBookmarks` llamando a la variable `Document` del objeto `createElement` método. Pase un valor de cadena que represente el nombre del elemento a `createElement` método. Convierta el valor devuelto en `Element`. Establezca un valor para `PDFsFromBookmarks` llamando a su elemento `setAttribute` método. Adjuntar el `PDFsFromBookmarks` al elemento `DDX` llamando al elemento DDX de `appendChild` método. Pase el `PDFsFromBookmarks` objeto element como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

     ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * Crear un `PDF` llamando a la variable `Document` del objeto `createElement` método. Pase un valor de cadena que represente el nombre del elemento. Convierta el valor devuelto en `Element`. Establezca un valor para `PDF` llamando a su elemento `setAttribute` método. Adjuntar el `PDF` al elemento `PDFsFromBookmarks` llamando a la variable `PDFsFromBookmarks` del elemento `appendChild` método. Pase el `PDF` objeto element como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

     ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. Convierta el documento DDX.

   * Crear un `javax.xml.transform.Transformer` invocando el objeto de `javax.xml.transform.Transformer` objeto estático `newInstance` método.
   * Crear un `Transformer` invocando el objeto de `TransformerFactory` del objeto `newTransformer` método.
   * Crear un `ByteArrayOutputStream` mediante su constructor.
   * Crear un `javax.xml.transform.dom.DOMSource` mediante su constructor. Pase el `org.w3c.dom.Document` que representa el documento DDX.
   * Crear un `javax.xml.transform.dom.DOMSource` usando su constructor y pasando el objeto `ByteArrayOutputStream` objeto.
   * Rellenar el Java `ByteArrayOutputStream` invocando el objeto de `javax.xml.transform.Transformer` del objeto `transform` método. Pase el `javax.xml.transform.dom.DOMSource` y el `javax.xml.transform.stream.StreamResult` objetos.
   * Cree una matriz de bytes y asigne el tamaño del `ByteArrayOutputStream` a la matriz de bytes.
   * Rellene la matriz de bytes invocando `ByteArrayOutputStream` del objeto `toByteArray` método.
   * Crear un `com.adobe.idp.Document` mediante su constructor y pasando la matriz de bytes.

1. Hacer referencia a un documento de PDF para desmontar.

   * Crear un `java.util.Map` objeto que se utiliza para almacenar documentos del PDF de entrada mediante un `HashMap` constructor.
   * Crear un `java.io.FileInputStream` utilizando su constructor y pasando la ubicación del documento de PDF que se va a desmontar.
   * Crear un `com.adobe.idp.Document` objeto. Pase el `java.io.FileInputStream` que contiene el documento de PDF que se va a desmontar.
   * Añada una entrada a `java.util.Map` invocando su objeto `put` y pasando los siguientes argumentos:

      * Valor de cadena que representa el nombre de clave. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX. (En el documento DDX creado dinámicamente, el valor es `AssemblerResultPDF.pdf`.)
      * A `com.adobe.idp.Document` que contiene el documento de PDF que se va a desmontar.

1. Establecer opciones en tiempo de ejecución.

   * Crear un `AssemblerOptionSpec` que almacena las opciones en tiempo de ejecución mediante su constructor.
   * Establezca opciones en tiempo de ejecución para satisfacer sus necesidades empresariales invocando un método que pertenezca a `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, invoque el `AssemblerOptionSpec` del objeto `setFailOnError` método y pase `false`.

1. Desmontar el documento del PDF.

   Invoque el `AssemblerServiceClient` del objeto `invokeDDX` y pasar los siguientes valores:

   * A `com.adobe.idp.Document` que representa el documento DDX creado dinámicamente
   * A `java.util.Map` que contiene el documento de PDF que se va a desmontar
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones en tiempo de ejecución, incluida la fuente predeterminada y el nivel de registro de trabajo

   El `invokeDDX` El método devuelve un valor `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene los documentos de PDF desensamblados y las excepciones que se han producido.

1. Guarde los documentos del PDF desmontados.

   Para obtener los documentos de PDF desmontados, realice las siguientes acciones:

   * Invoque el `AssemblerResult` del objeto `getDocuments` método. Este método devuelve un `java.util.Map` objeto.
   * Itere a través de `java.util.Map` hasta que encuentre el resultado `com.adobe.idp.Document` objeto.
   * Invoque el `com.adobe.idp.Document` del objeto `copyToFile` para extraer el documento del PDF.

**Consulte también**

[SOAP Inicio rápido (modo de): Creación dinámica de un documento DDX mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Crear dinámicamente un documento DDX mediante la API de servicio web {#dynamically-create-a-ddx-document-using-the-web-service-api}

Cree de forma dinámica un documento DDX y desmonte un documento de PDF mediante la API del servicio Assembler (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL al configurar una referencia de servicio: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de PDF Assembler.

   * Crear un `AssemblerServiceClient` mediante su constructor predeterminado.
   * Crear un `AssemblerServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio.
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `AssemblerServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Cree el documento DDX.

   * Crear un `System.Xml.XmlElement` mediante su constructor.
   * Cree el elemento raíz del documento DDX invocando el `XmlElement` del objeto `CreateElement` método. Este método crea un `Element` que representa el elemento raíz. Pase un valor de cadena que represente el nombre del elemento a `CreateElement` método. Establezca un valor para el elemento DDX llamando a su `SetAttribute` método. Finalmente, anexe el elemento al documento DDX llamando a la función `XmlElement` del objeto `AppendChild` método. Pase el objeto DDX como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

     ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * Cree el documento DDX de `PDFsFromBookmarks` llamando a la variable `XmlElement` del objeto `CreateElement` método. Pase un valor de cadena que represente el nombre del elemento a `CreateElement` método. A continuación, establezca un valor para el elemento llamando a su `SetAttribute` método. Adjuntar el `PDFsFromBookmarks` al elemento raíz llamando a la variable `DDX` del elemento `AppendChild` método. Pase el `PDFsFromBookmarks` objeto element como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

     ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * Cree el documento DDX de `PDF` llamando a la variable `XmlElement` del objeto `CreateElement` método. Pase un valor de cadena que represente el nombre del elemento a `CreateElement` método. A continuación, establezca un valor para el elemento secundario llamando a su `SetAttribute` método. Adjuntar el `PDF` al elemento `PDFsFromBookmarks` llamando a la variable `PDFsFromBookmarks` del elemento `AppendChild` método. Pase el `PDF` objeto element como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

     ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. Convierta el documento DDX.

   * Crear un `System.IO.MemoryStream` mediante su constructor.
   * Rellene el `MemoryStream` con el documento DDX utilizando el objeto `XmlElement` que representa el documento DDX. Invoque el `XmlElement` del objeto `Save` y pase el `MemoryStream` objeto.
   * Cree una matriz de bytes y rellénela con datos en `MemoryStream` objeto. El siguiente código muestra esta lógica de aplicación:

     ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * Crear un `BLOB` objeto. Asigne la matriz de bytes al `BLOB` del objeto `MTOM` field.

1. Hacer referencia a un documento de PDF para desmontar.

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar el documento del PDF de entrada. Esta `BLOB` El objeto se pasa a `invokeOneDocument` como argumento.
   * Crear un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento del PDF de entrada y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` al asignar su `MTOM` propiedad el contenido de la matriz de bytes.

1. Establecer opciones en tiempo de ejecución.

   * Crear un `AssemblerOptionSpec` que almacena las opciones en tiempo de ejecución mediante su constructor.
   * Establezca las opciones en tiempo de ejecución para satisfacer sus necesidades empresariales asignando un valor a un miembro de datos que pertenezca a `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne a `false` a la `AssemblerOptionSpec` del objeto `failOnError` miembro de datos.

1. Desmontar el documento del PDF.

   Invoque el `AssemblerServiceClient` del objeto `invokeDDX` y pasar los siguientes valores:

   * A `BLOB` que representa el documento DDX creado dinámicamente
   * El `mapItem` matriz que contiene el documento del PDF de entrada
   * Un `AssemblerOptionSpec` objeto que especifica opciones en tiempo de ejecución

   El `invokeDDX` El método devuelve un `AssemblerResult` que contiene los resultados del trabajo y las excepciones que se han producido.

1. Guarde los documentos del PDF desmontados.

   Para obtener los documentos del PDF recién creados, realice las siguientes acciones:

   * Acceda a la `AssemblerResult` del objeto `documents` , que es un `Map` que contiene los documentos de PDF desensamblados.
   * Itere a través de `Map` para obtener cada documento resultante. A continuación, convierta el de ese miembro de la matriz `value` a un `BLOB`.
   * Extraiga los datos binarios que representan el documento PDF accediendo a su `BLOB` del objeto `MTOM` propiedad. Devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
