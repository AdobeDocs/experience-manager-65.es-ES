---
title: Desmontaje programático de documentos PDF
seo-title: Programmatically Disassembling PDF Documents
description: Utilice el servicio Assembler para desmontar un único documento de PDF en varios documentos de PDF mediante la API de Java y la API de servicio web.
seo-description: Use the Assembler service to disassemble a single PDF document into multiple PDF documents using the Java API and the Web Service API.
uuid: d71cc044-e948-4b7a-b598-b041723b69e9
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8e38a597-5d22-4d83-95fe-4494fb04e4a3
role: Developer
exl-id: c5e712e0-5c3f-48cd-91cf-fd347222a6b2
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1760'
ht-degree: 1%

---

# Desmontaje programático de documentos PDF {#programmatically-disassembling-pdf-documents}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

Puede desmontar un documento de PDF pasándolo al servicio Assembler. Normalmente, esta tarea resulta útil cuando el documento del PDF se creó originalmente a partir de numerosos documentos individuales, como una colección de declaraciones. En la siguiente ilustración, el DocA se divide en varios documentos resultantes, donde el primer marcador de nivel 1 de una página identifica el inicio de un nuevo documento resultante.

![pd_pd_pdfsfrombookmarks](assets/pd_pd_pdfsfrombookmarks.png)

Para desmontar un documento de PDF, asegúrese de que la variable `PDFsFromBookmarks` está en el documento DDX. El `PDFsFromBookmarks` es un elemento resultante y solo puede ser un elemento secundario del `DDX` Elemento. No tiene un. `result` porque puede dar como resultado la generación de varios documentos.

El `PDFsFromBookmarks` hace que se genere un solo documento para cada marcador de nivel 1 en el documento de origen.

A los efectos de esta discusión, supongamos que se utiliza el siguiente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

>[!NOTE]
>
>Antes de leer esta sección, se recomienda que esté familiarizado con el ensamblado de documentos de PDF mediante el servicio Assembler. (Consulte [Agrupar documentos de PDF mediante programación](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Al pasar un solo documento de PDF al servicio Assembler y recuperar un solo documento, puede invocar el `invokeOneDocument` operación. Sin embargo, para desmontar un documento de PDF, utilice el `invokeDDX` porque aunque se pasa un documento de PDF de entrada al servicio Assembler, el servicio Assembler devuelve un objeto de colección que contiene uno o varios documentos.

>[!NOTE]
>
>Para obtener más información sobre el servicio Assembler, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para desmontar un documento de PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDF Assembler.
1. Hacer referencia a un documento DDX existente.
1. Hacer referencia a un documento de PDF para desmontar.
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

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar adobe-utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que AEM Forms está implementado.

**Crear un cliente de PDF Assembler**

Para poder realizar mediante programación una operación de Assembler, debe crear un cliente de servicio Assembler.

**Hacer referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para desmontar un documento PDF. Este documento DDX debe contener la variable `PDFsFromBookmarks` Elemento.

**Hacer referencia a un documento de PDF para desmontar**

Para desmontar un documento de PDF, haga referencia a un fichero de PDF que represente el documento de PDF que se va a desmontar. Cuando se pasa al servicio Assembler, se devuelve un documento de PDF independiente para cada marcador de nivel 1 del documento.

**Establecer opciones en tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlen el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede establecer una opción que indique al servicio Assembler que continúe procesando un trabajo si se produce un error.

**Desmontar el documento del PDF**

Después de crear el cliente de servicio Assembler, hacer referencia al documento DDX, hacer referencia a un documento de PDF para desmontar y establecer las opciones en tiempo de ejecución, puede desmontar un documento de PDF invocando el método `invokeDDX` método. Siempre que el documento DDX contenga instrucciones para desmontar el documento del PDF, el servicio Assembler devolverá documentos del PDF desensamblados dentro de un objeto de colección.

**Guardar los documentos de PDF desensamblados**

Todos los documentos de PDF desensamblados se devuelven dentro de un objeto de colección. Recorra en iteración el objeto de colección y guarde cada documento de PDF como un archivo de PDF.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Desmontar un documento de PDF mediante la API de Java {#disassemble-a-pdf-document-using-the-java-api}

Desmontar un documento de PDF mediante la API del servicio del ensamblador (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de PDF Assembler.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `AssemblerServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Hacer referencia a un documento DDX existente.

   * Crear un `java.io.FileInputStream` que representa el documento DDX utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo DDX.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Hacer referencia a un documento de PDF para desmontar.

   * Crear un `java.util.Map` objeto que se utiliza para almacenar documentos del PDF de entrada mediante un `HashMap` constructor.
   * Crear un `java.io.FileInputStream` utilizando su constructor y pasando la ubicación del documento de PDF que se va a desmontar.
   * Crear un `com.adobe.idp.Document` y pase el `java.io.FileInputStream` que contiene el documento de PDF que se va a desmontar.
   * Añada una entrada a `java.util.Map` invocando su objeto `put` y pasando los siguientes argumentos:

      * Valor de cadena que representa el nombre de clave. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX.
      * A `com.adobe.idp.Document` que contiene el documento de PDF que se va a desmontar.

1. Establecer opciones en tiempo de ejecución.

   * Crear un `AssemblerOptionSpec` que almacena las opciones en tiempo de ejecución mediante su constructor.
   * Establezca opciones en tiempo de ejecución para satisfacer sus necesidades empresariales invocando un método que pertenezca a `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, invoque el `AssemblerOptionSpec` del objeto `setFailOnError` método y pase `false`.

1. Desmontar el documento del PDF.

   Invoque el `AssemblerServiceClient` del objeto `invokeDDX` y pasar los siguientes valores obligatorios:

   * A `com.adobe.idp.Document` que representa el documento DDX a utilizar
   * A `java.util.Map` que contiene el documento de PDF que se va a desmontar
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones en tiempo de ejecución, incluida la fuente predeterminada y el nivel de registro de trabajo

   El `invokeDDX` El método devuelve un valor `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene los documentos de PDF desensamblados y las excepciones que se han producido.

1. Guarde los documentos del PDF desmontados.

   Para obtener los documentos de PDF desmontados, realice las siguientes acciones:

   * Invoque el `AssemblerResult` del objeto `getDocuments` método. Esto devuelve un `java.util.Map` objeto.
   * Itere a través de `java.util.Map` hasta que encuentre el resultado `com.adobe.idp.Document` objeto.
   * Invoque el `com.adobe.idp.Document` del objeto `copyToFile` para extraer el documento del PDF.

**Consulte también**

[Desmontaje programático de documentos PDF](#programmatically-disassembling-pdf-documents)

[Inicio rápido (modo SOAP): Desmontaje de un documento de PDF mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Desagrupar de un documento PDF mediante la API de servicio web {#disassemble-a-pdf-document-using-the-web-service-api}

Desmontar un documento de PDF mediante la API del servicio Assembler (servicio web):

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

1. Hacer referencia a un documento DDX existente.

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar el documento DDX.
   * Crear un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación de archivo del documento DDX y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.

1. Hacer referencia a un documento de PDF para desmontar.

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar el documento del PDF de entrada. Esta `BLOB` El objeto se pasa a `invokeOneDocument` como argumento.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento del PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` al asignar su `MTOM` el contenido de la matriz de bytes.
   * Crear un `MyMapOf_xsd_string_To_xsd_anyType` objeto. Este objeto de colección se utiliza para almacenar el PDF que se va a desmontar.
   * Crear un `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Asigne un valor de cadena que represente el nombre de clave al `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key` field. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX.
   * Asigne el `BLOB` que almacena el documento del PDF en `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value` field.
   * Añada el `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto a `MyMapOf_xsd_string_To_xsd_anyType` objeto. Invoque el `MyMapOf_xsd_string_To_xsd_anyType` object&#39; `Add` y pase el `MyMapOf_xsd_string_To_xsd_anyType` objeto.

1. Establecer opciones en tiempo de ejecución.

   * Crear un `AssemblerOptionSpec` que almacena las opciones en tiempo de ejecución mediante su constructor.
   * Establezca las opciones en tiempo de ejecución para satisfacer sus necesidades empresariales asignando un valor a un miembro de datos que pertenezca a `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne a `false` a la `AssemblerOptionSpec` del objeto `failOnError` field.

1. Desmontar el documento del PDF.

   Invoque el `AssemblerServiceClient` del objeto `invokeDDX` y pasar los siguientes valores:

   * A `BLOB` que representa el documento DDX que desmonta el documento de PDF
   * El `MyMapOf_xsd_string_To_xsd_anyType` que contiene el documento de PDF que se va a desmontar
   * Un `AssemblerOptionSpec` objeto que especifica opciones en tiempo de ejecución

   El `invokeDDX` El método devuelve un `AssemblerResult` que contiene los resultados del trabajo y las excepciones que se han producido.

1. Guarde los documentos del PDF desmontados.

   Para obtener los documentos del PDF recién creados, realice las siguientes acciones:

   * Acceda a la `AssemblerResult` del objeto `documents` , que es un `Map` que contiene los documentos de PDF desensamblados.
   * Itere a través de `Map` para obtener cada documento resultante. A continuación, convierta el de ese miembro de la matriz `value` a un `BLOB`.
   * Extraiga los datos binarios que representan el documento PDF accediendo a su `BLOB` del objeto `MTOM` propiedad. Devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también**

[Desmontaje programático de documentos PDF](#programmatically-disassembling-pdf-documents)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
