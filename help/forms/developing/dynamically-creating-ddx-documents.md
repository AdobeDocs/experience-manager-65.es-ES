---
title: Creación dinámica de documentos DDX
seo-title: Dynamically Creating DDX Documents
description: Cree un documento DDX de forma dinámica mediante la API de Java y la API de servicio web. La creación dinámica de un documento DDX permite utilizar valores en el documento DDX obtenidos durante la ejecución.
seo-description: Create a DDX document dynamically using the Java API and Web Service API. Dynamically creating a DDX document enables you to use values in the DDX document that are obtained during run-time.
uuid: b73e8069-6c9f-4517-a0ae-f3d503191d2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2ad227de-68a8-446f-8c4f-a33a6f95bec8
role: Developer
exl-id: b3c19c82-e26f-4dc8-b846-6aec705cee08
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2163'
ht-degree: 0%

---

# Creación dinámica de documentos DDX {#dynamically-creating-ddx-documents}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

Puede crear dinámicamente un documento DDX que pueda utilizarse para realizar una operación Assembler. La creación dinámica de un documento DDX permite utilizar valores en el documento DDX obtenidos durante la ejecución. Para crear dinámicamente un documento DDX, utilice clases que pertenezcan al lenguaje de programación que esté utilizando. Por ejemplo, si está desarrollando la aplicación cliente mediante Java, utilice clases que pertenezcan al grupo `org.w3c.dom.*`paquete. Del mismo modo, si utiliza Microsoft .NET, utilice clases que pertenezcan a la variable `System.Xml` espacio de nombres.

Para poder pasar el documento DDX al servicio Assembler, convierta el XML desde un `org.w3c.dom.Document` instancia a un `com.adobe.idp.Document` instancia. Si utiliza servicios web, convierta el XML del tipo de datos utilizado para crear el XML (por ejemplo, `XmlDocument`) a `BLOB` instancia.

Para esta discusión, supongamos que el siguiente documento DDX se crea de forma dinámica.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

Este documento DDX desmonta un documento PDF. Se recomienda que esté familiarizado con el desmontaje de documentos PDF.

>[!NOTE]
>
>Para obtener más información sobre el servicio Assembler, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para desmontar un documento PDF utilizando un documento DDX creado dinámicamente, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de ensamblador de PDF.
1. Cree el documento DDX.
1. Convierta el documento DDX.
1. Establezca las opciones de tiempo de ejecución.
1. Desmonte el documento del PDF.
1. Guarde los documentos de PDF desmontados.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

**Creación de un cliente de ensamblador de PDF**

Antes de realizar una operación Assembler mediante programación, cree un cliente de servicio Assembler.

**Crear el documento DDX**

Cree un documento DDX utilizando el lenguaje de programación que está utilizando. Para crear un documento DDX que desmonte un documento PDF, asegúrese de que contiene el `PDFsFromBookmarks` elemento. Convertir el tipo de datos utilizado para crear el documento DDX a un `com.adobe.idp.Document` instancia si utiliza la API de Java. Si utiliza servicios web, convierta el tipo de datos en un `BLOB` instancia.

**Convertir el documento DDX**

Un documento DDX que se crea mediante el uso de `org.w3c.dom` las clases deben convertirse en `com.adobe.idp.Document` objeto. Para realizar esta tarea al utilizar la API de Java, utilice clases de transformación XML de Java. Si utiliza servicios web, convierta el documento DDX a un `BLOB` objeto.

**Haga referencia a un documento del PDF para desmontarlo**

Para desmontar un documento de PDF, haga referencia a un archivo de PDF que representa el documento de PDF que se va a desmontar. Cuando se pasa al servicio Assembler, se devuelve un documento PDF independiente para cada marcador de nivel 1 del documento.

**Establecer opciones de tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlan el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede definir una opción que indique al servicio Assembler que continúe procesando un trabajo si se encuentra un error. Para configurar las opciones de tiempo de ejecución, utilice un `AssemblerOptionSpec` objeto.

**Desmontar el documento del PDF**

Desmonte el documento del PDF invocando el `invokeDDX` operación. Pase el documento DDX que se creó dinámicamente. El servicio Assembler devuelve documentos PDF desmontados dentro de un objeto de colección.

**Guarde los documentos del PDF desmontados**

Todos los documentos PDF desmontados se devuelven dentro de un objeto de colección. Itere a través del objeto de colección y guarde cada documento de PDF como archivo de PDF.

**Consulte también lo siguiente**

[Creación dinámica de un documento DDX mediante la API de Java](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[Creación dinámica de un documento DDX mediante la API de servicio web](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Desmontaje programático de documentos PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Creación dinámica de un documento DDX mediante la API de Java {#dynamically-create-a-ddx-document-using-the-java-api}

Cree dinámicamente un documento DDX y desmonte un documento PDF utilizando la API de servicio del ensamblador (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-assembler-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente de ensamblador de PDF.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `AssemblerServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Cree el documento DDX.

   * Creación de un Java `DocumentBuilderFactory` llamando al `DocumentBuilderFactory` class&quot; `newInstance` método.
   * Creación de un Java `DocumentBuilder` llamando al `DocumentBuilderFactory` del objeto `newDocumentBuilder` método.
   * Llame a la función `DocumentBuilder` del objeto `newDocument` para crear una instancia de `org.w3c.dom.Document` objeto.
   * Cree el elemento raíz del documento DDX invocando la variable `org.w3c.dom.Document` del objeto `createElement` método. Este método crea un `Element` objeto que representa el elemento raíz. Pase un valor de cadena que represente el nombre del elemento a la variable `createElement` método. Conversión del valor devuelto a `Element`. A continuación, establezca un valor para el elemento secundario llamando a su `setAttribute` método. Finalmente, anexe el elemento al elemento del encabezado llamando al elemento del encabezado `appendChild` y pase el objeto de elemento secundario como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * Cree la variable `PDFsFromBookmarks` llamando al `Document` del objeto `createElement` método. Pase un valor de cadena que represente el nombre del elemento a la variable `createElement` método. Conversión del valor devuelto a `Element`. Establezca un valor para la variable `PDFsFromBookmarks` llamando a su `setAttribute` método. Anexe la variable `PDFsFromBookmarks` al `DDX` llamando al elemento DDX de `appendChild` método. Pase el `PDFsFromBookmarks` objeto element como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * Cree un `PDF` llamando al `Document` del objeto `createElement` método. Pase un valor de cadena que represente el nombre del elemento. Conversión del valor devuelto a `Element`. Establezca un valor para la variable `PDF` llamando a su `setAttribute` método. Anexe la variable `PDF` al `PDFsFromBookmarks` llamando al `PDFsFromBookmarks` del elemento `appendChild` método. Pase el `PDF` objeto element como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. Convierta el documento DDX.

   * Cree un `javax.xml.transform.Transformer` invocando el objeto `javax.xml.transform.Transformer` estático del objeto `newInstance` método.
   * Cree un `Transformer` invocando el objeto `TransformerFactory` del objeto `newTransformer` método.
   * Cree un `ByteArrayOutputStream` usando su constructor.
   * Cree un `javax.xml.transform.dom.DOMSource` usando su constructor. Pase el `org.w3c.dom.Document` que representa el documento DDX.
   * Cree un `javax.xml.transform.dom.DOMSource` usando su constructor y pasando el `ByteArrayOutputStream` objeto.
   * Rellenar el Java `ByteArrayOutputStream` invocando el objeto `javax.xml.transform.Transformer` del objeto `transform` método. Pase el `javax.xml.transform.dom.DOMSource` y `javax.xml.transform.stream.StreamResult` objetos.
   * Cree una matriz de bytes y asigne el tamaño de la variable `ByteArrayOutputStream` a la matriz de bytes.
   * Rellene la matriz de bytes invocando la variable `ByteArrayOutputStream` del objeto `toByteArray` método.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando la matriz de bytes.

1. Haga referencia a un documento del PDF para desmontarlo.

   * Cree un `java.util.Map` objeto que se utiliza para almacenar documentos del PDF de entrada mediante un `HashMap` constructor.
   * Cree un `java.io.FileInputStream` utilizando su constructor y pasando la ubicación del documento PDF para desmontarlo.
   * Cree un `com.adobe.idp.Document` objeto. Pase el `java.io.FileInputStream` objeto que contiene el documento PDF que se va a desmontar.
   * Agregue una entrada al `java.util.Map` invocando su `put` y pasando los siguientes argumentos:

      * Un valor de cadena que representa el nombre de la clave. Este valor debe coincidir con el valor del elemento de origen del PDF especificado en el documento DDX. (En el documento DDX que se crea dinámicamente, el valor es `AssemblerResultPDF.pdf`.)
      * A `com.adobe.idp.Document` objeto que contiene el documento PDF que se va a desmontar.

1. Establezca las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` que almacena opciones en tiempo de ejecución mediante su constructor.
   * Configure las opciones en tiempo de ejecución para satisfacer los requisitos empresariales invocando un método que pertenece al `AssemblerOptionSpec` objeto. Por ejemplo, para solicitar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, invoque la función `AssemblerOptionSpec` del objeto `setFailOnError` método y pase `false`.

1. Desmonte el documento del PDF.

   Invocar el `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores:

   * A `com.adobe.idp.Document` objeto que representa el documento DDX creado dinámicamente
   * A `java.util.Map` objeto que contiene el documento del PDF que se va a desmontar
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica las opciones de tiempo de ejecución, incluyendo la fuente predeterminada y el nivel de registro de trabajo

   La variable `invokeDDX` el método devuelve un `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene los documentos de PDF desmontados y cualquier excepción que se haya producido.

1. Guarde los documentos de PDF desmontados.

   Para obtener los documentos de PDF desmontados, realice las siguientes acciones:

   * Invocar el `AssemblerResult` del objeto `getDocuments` método. Este método devuelve un `java.util.Map` objeto.
   * Iterar a través de la variable `java.util.Map` hasta que encuentre el resultado `com.adobe.idp.Document` objeto.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` método para extraer el documento PDF.

**Consulte también lo siguiente**

[Inicio rápido (modo SOAP): Creación dinámica de un documento DDX mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Creación dinámica de un documento DDX mediante la API de servicio web {#dynamically-create-a-ddx-document-using-the-web-service-api}

Cree dinámicamente un documento DDX y desmonte un documento PDF utilizando la API de servicio del ensamblador (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL al configurar una referencia de servicio: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de ensamblador de PDF.

   * Cree un `AssemblerServiceClient` usando su constructor predeterminado.
   * Cree un `AssemblerServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio.
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `AssemblerServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Cree el documento DDX.

   * Cree un `System.Xml.XmlElement` usando su constructor.
   * Cree el elemento raíz del documento DDX invocando la variable `XmlElement` del objeto `CreateElement` método. Este método crea un `Element` objeto que representa el elemento raíz. Pase un valor de cadena que represente el nombre del elemento a la variable `CreateElement` método. Establezca un valor para el elemento DDX llamando a su `SetAttribute` método. Finalmente, anexe el elemento al documento DDX llamando a la variable `XmlElement` del objeto `AppendChild` método. Pase el objeto DDX como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * Creación del documento DDX `PDFsFromBookmarks` llamando al `XmlElement` del objeto `CreateElement` método. Pase un valor de cadena que represente el nombre del elemento a la variable `CreateElement` método. A continuación, establezca un valor para el elemento llamando a su `SetAttribute` método. Anexe la variable `PDFsFromBookmarks` al elemento raíz llamando a la función `DDX` del elemento `AppendChild` método. Pase el `PDFsFromBookmarks` objeto element como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * Creación del documento DDX `PDF` llamando al `XmlElement` del objeto `CreateElement` método. Pase un valor de cadena que represente el nombre del elemento a la variable `CreateElement` método. A continuación, establezca un valor para el elemento secundario llamando a su `SetAttribute` método. Anexe la variable `PDF` al `PDFsFromBookmarks` llamando al `PDFsFromBookmarks` del elemento `AppendChild` método. Pase el `PDF` objeto element como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. Convierta el documento DDX.

   * Cree un `System.IO.MemoryStream` usando su constructor.
   * Rellene el `MemoryStream` con el documento DDX utilizando la variable `XmlElement` que representa el documento DDX. Invocar el `XmlElement` del objeto `Save` y pase el `MemoryStream` objeto.
   * Cree una matriz de bytes y rellénela con datos ubicados en la variable `MemoryStream` objeto. El siguiente código muestra esta lógica de aplicación:

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * Cree un `BLOB` objeto. Asigne la matriz de bytes a la variable `BLOB` del objeto `MTOM` campo .

1. Haga referencia a un documento del PDF para desmontarlo.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar el documento del PDF de entrada. Esta `BLOB` se pasa al `invokeOneDocument` como argumento.
   * Cree un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento del PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` propiedad del contenido de la matriz de bytes.

1. Establezca las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` que almacena opciones en tiempo de ejecución mediante su constructor.
   * Configure las opciones en tiempo de ejecución para satisfacer los requisitos empresariales asignando un valor a un miembro de datos que pertenezca al grupo `AssemblerOptionSpec` objeto. Por ejemplo, para solicitar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne `false` a `AssemblerOptionSpec` del objeto `failOnError` miembro de datos.

1. Desmonte el documento del PDF.

   Invocar el `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores:

   * A `BLOB` objeto que representa el documento DDX creado dinámicamente
   * La variable `mapItem` matriz que contiene el documento del PDF de entrada
   * Un `AssemblerOptionSpec` objeto que especifica opciones en tiempo de ejecución

   La variable `invokeDDX` devuelve un valor `AssemblerResult` que contiene los resultados del trabajo y cualquier excepción que se haya producido.

1. Guarde los documentos de PDF desmontados.

   Para obtener los documentos de PDF recién creados, realice las siguientes acciones:

   * Acceda a la `AssemblerResult` del objeto `documents` , que es un `Map` que contiene los documentos de PDF desmontados.
   * Iterar a través de la variable `Map` para obtener cada documento resultante. A continuación, cree el `value` a `BLOB`.
   * Extraiga los datos binarios que representan el documento del PDF accediendo a su `BLOB` del objeto `MTOM` propiedad. Esto devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también lo siguiente**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
