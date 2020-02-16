---
title: Desensamblar documentos PDF mediante programación
seo-title: Desensamblar documentos PDF mediante programación
description: nulo
seo-description: nulo
uuid: d71cc044-e948-4b7a-b598-b041723b69e9
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8e38a597-5d22-4d83-95fe-4494fb04e4a3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Desensamblar documentos PDF mediante programación {#programmatically-disassembling-pdf-documents}

Puede desmontar un documento PDF pasando el documento al servicio Ensamblador. Normalmente, esta tarea resulta útil cuando el documento PDF se creó originalmente a partir de muchos documentos individuales, como una colección de instrucciones. En la siguiente ilustración, DocA se divide en varios documentos resultantes, donde el primer marcador de nivel 1 de una página identifica el inicio de un nuevo documento resultante.

![pd_pd_pdfsfrombookmarks](assets/pd_pd_pdfsfrombookmarks.png)

Para desmontar un documento PDF, asegúrese de que el `PDFsFromBookmarks` elemento se encuentra en el documento DDX. El `PDFsFromBookmarks` elemento es un elemento resultante y solo puede ser un elemento secundario del `DDX` elemento. No tiene un `result` atributo porque puede dar como resultado la generación de varios documentos.

El `PDFsFromBookmarks` elemento hace que se genere un solo documento para cada marcador de nivel 1 del documento de origen.

A los efectos de este análisis, supongamos que se utiliza el siguiente documento DDX.

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

>[!NOTE]
>
>Antes de leer esta sección, se recomienda familiarizarse con el ensamblado de documentos PDF mediante el servicio Ensamblador. (Consulte Compilación [programada de documentos](/help/forms/developing/programmatically-assembling-pdf-documents.md)PDF).

>[!NOTE]
>
>Al pasar un solo documento PDF al servicio de Ensamblador y recuperar un solo documento, puede invocar la `invokeOneDocument` operación. Sin embargo, para desmontar un documento PDF, utilice la `invokeDDX` operación porque, aunque se pasa un documento PDF de entrada al servicio Ensamblador, el servicio Ensamblador devuelve un objeto de colección que contiene uno o varios documentos.

>[!NOTE]
>
>Para obtener más información sobre el servicio Compilador, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y Referencia](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Resumen de los pasos {#summary-of-steps}

Para desmontar un documento PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de ensamblador de PDF.
1. Haga referencia a un documento DDX existente.
1. Haga referencia a un documento PDF para desmontarlo.
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

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no es JBoss, debe reemplazar adobe-utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms.

**Crear un cliente de ensamblador de PDF**

Antes de realizar una operación de ensamblador mediante programación, debe crear un cliente de servicio de ensamblador.

**Hacer referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para desmontar un documento PDF. Este documento DDX debe contener el `PDFsFromBookmarks` elemento .

**Hacer referencia a un documento PDF para desmontarlo**

Para desmontar un documento PDF, haga referencia a un archivo PDF que represente el documento PDF que desea desmontar. Cuando se pasa al servicio Compilador, se devuelve un documento PDF independiente para cada marcador de nivel 1 del documento.

**Definición de opciones de tiempo de ejecución**

Puede definir opciones en tiempo de ejecución que controlen el comportamiento del servicio de ensamblador mientras realiza un trabajo. Por ejemplo, puede definir una opción que indique al servicio Ensamblador que continúe procesando un trabajo si se produce un error.

**Desmontar el documento PDF**

Después de crear el cliente del servicio Ensamblador, hacer referencia al documento DDX, hacer referencia a un documento PDF para desmontarlo y definir las opciones en tiempo de ejecución, puede desmontar un documento PDF invocando el `invokeDDX` método . Siempre que el documento DDX contenga instrucciones para desmontar el documento PDF, el servicio Ensamblador devuelve documentos PDF desmontados dentro de un objeto de colección.

**Guardar los documentos PDF desmontados**

Todos los documentos PDF desmontados se devuelven dentro de un objeto de colección. Repita el objeto de colección y guarde cada documento PDF como archivo PDF.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Compilación de documentos PDF mediante programación](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Desmontaje de un documento PDF mediante la API de Java {#disassemble-a-pdf-document-using-the-java-api}

Desmontar un documento PDF mediante la API de servicio de ensamblador (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de ensamblador de PDF.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `AssemblerServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un documento DDX existente.

   * Cree un `java.io.FileInputStream` objeto que represente el documento DDX utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo DDX.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Haga referencia a un documento PDF para desmontarlo.

   * Cree un `java.util.Map` objeto que se utilice para almacenar documentos PDF de entrada mediante un `HashMap` constructor.
   * Cree un `java.io.FileInputStream` objeto utilizando su constructor y pasando la ubicación del documento PDF que desea desmontar.
   * Cree un `com.adobe.idp.Document` objeto y pase el `java.io.FileInputStream` objeto que contiene el documento PDF para desmontarlo.
   * Agregue una entrada al `java.util.Map` objeto invocando su `put` método y pasando los siguientes argumentos:

      * Un valor de cadena que representa el nombre de la clave. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX.
      * Un `com.adobe.idp.Document` objeto que contiene el documento PDF que se va a desmontar.

1. Configure las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` objeto que almacene opciones de tiempo de ejecución mediante su constructor.
   * Configure las opciones de tiempo de ejecución para cumplir los requisitos comerciales invocando un método que pertenece al `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Ensamblador que continúe procesando un trabajo cuando se produzca un error, invoque el `AssemblerOptionSpec` método del `setFailOnError` objeto y pase `false`.

1. Desmontar el documento PDF.

   Invoque el `AssemblerServiceClient` método del `invokeDDX` objeto y pase los siguientes valores obligatorios:

   * Un `com.adobe.idp.Document` objeto que representa el documento DDX que se va a utilizar
   * Un `java.util.Map` objeto que contiene el documento PDF que se va a desmontar
   * Un `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica las opciones de tiempo de ejecución, incluyendo la fuente predeterminada y el nivel de registro de trabajos
   El `invokeDDX` método devuelve un `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contiene los documentos PDF desensamblados y las excepciones que se hayan producido.

1. Guarde los documentos PDF desmontados.

   Para obtener los documentos PDF desmontados, realice las siguientes acciones:

   * Invocar el `AssemblerResult` método del `getDocuments` objeto. Esto devuelve un `java.util.Map` objeto.
   * Repita el `java.util.Map` objeto hasta que encuentre el `com.adobe.idp.Document` objeto resultante.
   * Invocar el `com.adobe.idp.Document` método del `copyToFile` objeto para extraer el documento PDF.

**Consulte también**

[Desensamblar documentos PDF mediante programación](#programmatically-disassembling-pdf-documents)

[Inicio rápido (modo SOAP): Desmontaje de un documento PDF mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Desmontaje de un documento PDF mediante la API de servicio Web {#disassemble-a-pdf-document-using-the-web-service-api}

Desmontar un documento PDF mediante la API de servicio de ensamblador (servicio Web):

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

1. Haga referencia a un documento DDX existente.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar el documento DDX.
   * Cree un `System.IO.FileStream` objeto invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento DDX y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` propiedad con el contenido de la matriz de bytes.

1. Haga referencia a un documento PDF para desmontarlo.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar el documento PDF de entrada. Este `BLOB` objeto se pasa al `invokeOneDocument` como argumento.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo al contenido de la matriz de bytes.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Este objeto de colección se utiliza para almacenar el PDF que se va a desmontar.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType_Item` object.
   * Asigne un valor de cadena que represente el nombre clave al `MyMapOf_xsd_string_To_xsd_anyType_Item` campo del `key` objeto. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX.
   * Asigne el `BLOB` objeto que almacena el documento PDF al `MyMapOf_xsd_string_To_xsd_anyType_Item` campo del `value` objeto.
   * Agregue el `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto al `MyMapOf_xsd_string_To_xsd_anyType` objeto. Invocar el `MyMapOf_xsd_string_To_xsd_anyType` método del `Add` objeto y pasar el `MyMapOf_xsd_string_To_xsd_anyType` objeto.

1. Configure las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` objeto que almacene opciones de tiempo de ejecución mediante su constructor.
   * Configure las opciones de tiempo de ejecución para cumplir los requisitos comerciales asignando un valor a un miembro de datos que pertenece al `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Ensamblador que continúe procesando un trabajo cuando se produzca un error, asigne `false` al `AssemblerOptionSpec` campo del `failOnError` objeto.

1. Desmontar el documento PDF.

   Invoque el `AssemblerServiceClient` método del `invokeDDX` objeto y pase los valores siguientes:

   * Un `BLOB` objeto que representa el documento DDX que desmonta el documento PDF
   * El `MyMapOf_xsd_string_To_xsd_anyType` objeto que contiene el documento PDF que se va a desmontar
   * Un `AssemblerOptionSpec` objeto que especifica opciones de tiempo de ejecución
   El `invokeDDX` método devuelve un `AssemblerResult` objeto que contiene los resultados del trabajo y las excepciones que se hayan producido.

1. Guarde los documentos PDF desmontados.

   Para obtener los documentos PDF recién creados, realice las siguientes acciones:

   * Acceda al `AssemblerResult` campo del `documents` objeto, que es un `Map` objeto que contiene los documentos PDF desensamblados.
   * Repita el `Map` objeto para obtener cada documento resultante. A continuación, convierta los miembros de la matriz `value` a un `BLOB`.
   * Extraiga los datos binarios que representan el documento PDF accediendo a la propiedad del `BLOB` objeto `MTOM` . Esto devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también**

[Desensamblar documentos PDF mediante programación](#programmatically-disassembling-pdf-documents)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
