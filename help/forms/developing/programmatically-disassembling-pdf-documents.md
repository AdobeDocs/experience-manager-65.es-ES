---
title: Desmontaje programático de documentos PDF
seo-title: Programmatically Disassembling PDF Documents
description: Utilice el servicio Assembler para desmontar un solo documento de PDF en varios documentos de PDF mediante la API de Java y la API del servicio Web.
seo-description: Use the Assembler service to disassemble a single PDF document into multiple PDF documents using the Java API and the Web Service API.
uuid: d71cc044-e948-4b7a-b598-b041723b69e9
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8e38a597-5d22-4d83-95fe-4494fb04e4a3
role: Developer
exl-id: c5e712e0-5c3f-48cd-91cf-fd347222a6b2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1761'
ht-degree: 0%

---

# Desmontaje programático de documentos PDF {#programmatically-disassembling-pdf-documents}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

Puede desmontar un documento PDF pasándolo al servicio Assembler. Normalmente, esta tarea resulta útil cuando el documento del PDF se creó originalmente a partir de muchos documentos individuales, como una colección de instrucciones. En la siguiente ilustración, el DocA se divide en varios documentos resultantes, donde el primer marcador de nivel 1 de una página identifica el inicio de un nuevo documento resultante.

![pd_pd_pdfsfrombookmarks](assets/pd_pd_pdfsfrombookmarks.png)

Para desmontar un documento de PDF, asegúrese de que la variable `PDFsFromBookmarks` se encuentra en el documento DDX. La variable `PDFsFromBookmarks` es un elemento resultante y solo puede ser un elemento secundario del `DDX` elemento. No tiene un `result` porque puede generar varios documentos.

La variable `PDFsFromBookmarks` hace que se genere un solo documento para cada marcador de nivel 1 en el documento de origen.

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
>Antes de leer esta sección, se recomienda que esté familiarizado con el ensamblaje de documentos PDF mediante el servicio Assembler. (Consulte [Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Al pasar un solo documento de PDF al servicio Assembler y recuperar un solo documento, puede invocar la función `invokeOneDocument` operación. Sin embargo, para desmontar un documento de PDF, utilice el `invokeDDX` porque, aunque se pasa un documento de PDF de entrada al servicio Assembler, el servicio Assembler devuelve un objeto de colección que contiene uno o más documentos.

>[!NOTE]
>
>Para obtener más información sobre el servicio Assembler, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para desmontar un documento de PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de ensamblador de PDF.
1. Haga referencia a un documento DDX existente.
1. Haga referencia a un documento del PDF para desmontarlo.
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

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar adobe-Utilities.jar y jbossall-client.jar con archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms.

**Creación de un cliente de ensamblador de PDF**

Para poder realizar una operación Assembler mediante programación, debe crear un cliente de servicio Assembler.

**Referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para desmontar un documento PDF. Este documento DDX debe contener la variable `PDFsFromBookmarks` elemento.

**Haga referencia a un documento del PDF para desmontarlo**

Para desmontar un documento de PDF, haga referencia a un archivo de PDF que representa el documento de PDF que se va a desmontar. Cuando se pasa al servicio Assembler, se devuelve un documento PDF independiente para cada marcador de nivel 1 del documento.

**Establecer opciones de tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlan el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede definir una opción que indique al servicio Assembler que continúe procesando un trabajo si se encuentra un error.

**Desmontar el documento del PDF**

Después de crear el cliente de servicio Assembler, hacer referencia al documento DDX, hacer referencia a un documento de PDF para desmontarlo y establecer las opciones de tiempo de ejecución, puede desensamblar un documento de PDF invocando el `invokeDDX` método. Siempre que el documento DDX contenga instrucciones para desmontar el documento PDF, el servicio Assembler devuelve documentos PDF desmontados dentro de un objeto de colección.

**Guarde los documentos del PDF desmontados**

Todos los documentos PDF desmontados se devuelven dentro de un objeto de colección. Itere a través del objeto de colección y guarde cada documento de PDF como archivo de PDF.

**Consulte también lo siguiente**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Desmontaje de un documento de PDF mediante la API de Java {#disassemble-a-pdf-document-using-the-java-api}

Desmonte un documento de PDF utilizando la API de servicio del ensamblador (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-assembler-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente de ensamblador de PDF.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `AssemblerServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un documento DDX existente.

   * Cree un `java.io.FileInputStream` objeto que representa el documento DDX utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo DDX.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Haga referencia a un documento del PDF para desmontarlo.

   * Cree un `java.util.Map` objeto que se utiliza para almacenar documentos del PDF de entrada mediante un `HashMap` constructor.
   * Cree un `java.io.FileInputStream` utilizando su constructor y pasando la ubicación del documento PDF para desmontarlo.
   * Cree un `com.adobe.idp.Document` y pase el `java.io.FileInputStream` objeto que contiene el documento PDF que se va a desmontar.
   * Agregue una entrada al `java.util.Map` invocando su `put` y pasando los siguientes argumentos:

      * Un valor de cadena que representa el nombre de la clave. Este valor debe coincidir con el valor del elemento de origen del PDF especificado en el documento DDX.
      * A `com.adobe.idp.Document` objeto que contiene el documento PDF que se va a desmontar.

1. Establezca las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` que almacena opciones en tiempo de ejecución mediante su constructor.
   * Configure las opciones en tiempo de ejecución para satisfacer los requisitos empresariales invocando un método que pertenece al `AssemblerOptionSpec` objeto. Por ejemplo, para solicitar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, invoque la función `AssemblerOptionSpec` del objeto `setFailOnError` método y pase `false`.

1. Desmonte el documento del PDF.

   Invocar el `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores obligatorios:

   * A `com.adobe.idp.Document` objeto que representa el documento DDX que se va a utilizar
   * A `java.util.Map` objeto que contiene el documento del PDF que se va a desmontar
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica las opciones de tiempo de ejecución, incluyendo la fuente predeterminada y el nivel de registro de trabajo

   La variable `invokeDDX` el método devuelve un `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene los documentos de PDF desmontados y cualquier excepción que se haya producido.

1. Guarde los documentos de PDF desmontados.

   Para obtener los documentos de PDF desmontados, realice las siguientes acciones:

   * Invocar el `AssemblerResult` del objeto `getDocuments` método. Esto devuelve un `java.util.Map` objeto.
   * Iterar a través de la variable `java.util.Map` hasta que encuentre el resultado `com.adobe.idp.Document` objeto.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` método para extraer el documento PDF.

**Consulte también lo siguiente**

[Desmontaje programático de documentos PDF](#programmatically-disassembling-pdf-documents)

[Inicio rápido (modo SOAP): Desmontaje de un documento de PDF mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Desmontaje de un documento de PDF mediante la API de servicio web {#disassemble-a-pdf-document-using-the-web-service-api}

Desmonte un documento del PDF utilizando la API del servicio Assembler (servicio Web):

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

1. Haga referencia a un documento DDX existente.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar el documento DDX.
   * Cree un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento DDX y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Haga referencia a un documento del PDF para desmontarlo.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar el documento del PDF de entrada. Esta `BLOB` se pasa al `invokeOneDocument` como argumento.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento del PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` campo el contenido de la matriz de bytes.
   * Cree un `MyMapOf_xsd_string_To_xsd_anyType` objeto. Este objeto de colección se utiliza para almacenar el PDF que se va a desmontar.
   * Cree un `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Asigne un valor de cadena que represente el nombre de clave a la variable `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key` campo . Este valor debe coincidir con el valor del elemento de origen del PDF especificado en el documento DDX.
   * Asigne la variable `BLOB` objeto que almacena el documento del PDF en el `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value` campo .
   * Agregue la variable `MyMapOf_xsd_string_To_xsd_anyType_Item` al `MyMapOf_xsd_string_To_xsd_anyType` objeto. Invocar el `MyMapOf_xsd_string_To_xsd_anyType` object’ `Add` y pase el `MyMapOf_xsd_string_To_xsd_anyType` objeto.

1. Establezca las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` que almacena opciones en tiempo de ejecución mediante su constructor.
   * Configure las opciones en tiempo de ejecución para satisfacer los requisitos empresariales asignando un valor a un miembro de datos que pertenezca al grupo `AssemblerOptionSpec` objeto. Por ejemplo, para solicitar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne `false` a `AssemblerOptionSpec` del objeto `failOnError` campo .

1. Desmonte el documento del PDF.

   Invocar el `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores:

   * A `BLOB` objeto que representa el documento DDX que desmonta el documento PDF
   * La variable `MyMapOf_xsd_string_To_xsd_anyType` objeto que contiene el documento del PDF que se va a desmontar
   * Un `AssemblerOptionSpec` objeto que especifica opciones en tiempo de ejecución

   La variable `invokeDDX` devuelve un valor `AssemblerResult` objeto que contiene los resultados del trabajo y cualquier excepción que se haya producido.

1. Guarde los documentos de PDF desmontados.

   Para obtener los documentos de PDF recién creados, realice las siguientes acciones:

   * Acceda a la `AssemblerResult` del objeto `documents` , que es un `Map` que contiene los documentos de PDF desmontados.
   * Iterar a través de la variable `Map` para obtener cada documento resultante. A continuación, cree el `value` a `BLOB`.
   * Extraiga los datos binarios que representan el documento del PDF accediendo a su `BLOB` del objeto `MTOM` propiedad. Esto devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también lo siguiente**

[Desmontaje programático de documentos PDF](#programmatically-disassembling-pdf-documents)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
