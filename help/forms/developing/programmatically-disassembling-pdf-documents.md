---
title: Desensamblar Documentos PDF mediante programación
seo-title: Desensamblar Documentos PDF mediante programación
description: Utilice el servicio Ensamblador para desmontar un solo documento PDF en varios documentos PDF mediante la API de Java y la API de servicio Web.
seo-description: Utilice el servicio Ensamblador para desmontar un solo documento PDF en varios documentos PDF mediante la API de Java y la API de servicio Web.
uuid: d71cc044-e948-4b7a-b598-b041723b69e9
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8e38a597-5d22-4d83-95fe-4494fb04e4a3
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '1788'
ht-degree: 0%

---


# Desmontaje programático de Documentos PDF {#programmatically-disassembling-pdf-documents}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en el entorno JEE.**

Puede desmontar un documento PDF pasándolo al servicio Ensamblador. Normalmente, esta tarea resulta útil cuando el documento PDF se creó originalmente a partir de muchos documentos individuales, como una colección de instrucciones. En la siguiente ilustración, DocA se divide en varios documentos resultantes, donde el primer marcador de nivel 1 de una página identifica el inicio de un nuevo documento resultante.

![pd_pd_pdfsfrombookmarks](assets/pd_pd_pdfsfrombookmarks.png)

Para desmontar un documento PDF, asegúrese de que el elemento `PDFsFromBookmarks` se encuentra en el documento DDX. El elemento `PDFsFromBookmarks` es un elemento resultante y sólo puede ser un elemento secundario del elemento `DDX`. No tiene un atributo `result` porque puede resultar en la generación de varios documentos.

El elemento `PDFsFromBookmarks` hace que se genere un solo documento para cada marcador de nivel 1 en el documento de origen.

A los efectos de este análisis, supongamos que se utiliza el siguiente documento DDX.

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
>Antes de leer esta sección, se recomienda familiarizarse con el ensamblado de documentos PDF mediante el servicio Ensamblador. (Consulte [Compilación programada de Documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)).

>[!NOTE]
>
>Al pasar un solo documento PDF al servicio de Ensamblador y recuperar un solo documento, puede invocar la operación `invokeOneDocument`. Sin embargo, para desmontar un documento PDF, utilice la operación `invokeDDX` porque, aunque se pasa un documento PDF de entrada al servicio Ensamblador, el servicio Ensamblador devuelve un objeto de colección que contiene uno o varios documentos.

>[!NOTE]
>
>Para obtener más información sobre el servicio de ensamblador, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y Referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para desmontar un documento PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de ensamblador de PDF.
1. Haga referencia a un documento DDX existente.
1. Haga referencia a un documento PDF para desmontarlo.
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

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no es JBoss, debe reemplazar adobe-utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms.

**Crear un cliente de ensamblador de PDF**

Antes de realizar una operación de ensamblador mediante programación, debe crear un cliente de servicio de ensamblador.

**Hacer referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para desmontar un documento PDF. Este documento DDX debe contener el elemento `PDFsFromBookmarks`.

**Hacer referencia a un documento PDF para desmontarlo**

Para desmontar un documento PDF, haga referencia a un archivo PDF que represente el documento PDF que desea desmontar. Cuando se pasa al servicio Compilador, se devuelve un documento PDF independiente para cada marcador de nivel 1 del documento.

**Definición de opciones de tiempo de ejecución**

Puede definir opciones en tiempo de ejecución que controlen el comportamiento del servicio de ensamblador mientras realiza un trabajo. Por ejemplo, puede definir una opción que indique al servicio Ensamblador que continúe procesando un trabajo si se produce un error.

**Desmontar el documento PDF**

Después de crear el cliente del servicio Ensamblador, hacer referencia al documento DDX, hacer referencia a un documento PDF para desmontarlo y definir las opciones de tiempo de ejecución, puede desmontar un documento PDF invocando el método `invokeDDX`. Siempre que el documento DDX contenga instrucciones para desmontar el documento PDF, el servicio Ensamblador devuelve documentos PDF desmontados dentro de un objeto de colección.

**Guardar los documentos PDF desmontados**

Todos los documentos PDF desmontados se devuelven dentro de un objeto de colección. Repita el objeto de colección y guarde cada documento PDF como archivo PDF.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Compilación programada de Documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Desmontar un documento PDF mediante la API de Java {#disassemble-a-pdf-document-using-the-java-api}

Desmontar un documento PDF mediante la API de servicio de ensamblador (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de ensamblador de PDF.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `AssemblerServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Haga referencia a un documento DDX existente.

   * Cree un objeto `java.io.FileInputStream` que represente el documento DDX utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo DDX.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Haga referencia a un documento PDF para desmontarlo.

   * Cree un objeto `java.util.Map` que se utilice para almacenar documentos PDF de entrada mediante un constructor `HashMap`.
   * Cree un objeto `java.io.FileInputStream` utilizando su constructor y pasando la ubicación del documento PDF para desmontarlo.
   * Cree un objeto `com.adobe.idp.Document` y pase el objeto `java.io.FileInputStream` que contiene el documento PDF para desmontarlo.
   * Añada una entrada al objeto `java.util.Map` invocando su método `put` y pasando los siguientes argumentos:

      * Un valor de cadena que representa el nombre de la clave. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX.
      * Objeto `com.adobe.idp.Document` que contiene el documento PDF que se va a desmontar.

1. Configure las opciones de tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene las opciones de tiempo de ejecución mediante su constructor.
   * Configure las opciones de tiempo de ejecución para satisfacer los requisitos comerciales invocando un método que pertenece al objeto `AssemblerOptionSpec`. Por ejemplo, para indicar al servicio Ensamblador que continúe procesando un trabajo cuando se produzca un error, invoque el método `AssemblerOptionSpec` del objeto `setFailOnError` y pase `false`.

1. Desmonte el documento PDF.

   Invoque el método `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores obligatorios:

   * Un objeto `com.adobe.idp.Document` que representa el documento DDX que se va a utilizar
   * Un objeto `java.util.Map` que contiene el documento PDF que se va a desmontar
   * Un objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones de tiempo de ejecución, incluyendo la fuente predeterminada y el nivel de registro de trabajo

   El método `invokeDDX` devuelve un objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene los documentos PDF desmontados y las excepciones que se hayan producido.

1. Guarde los documentos PDF desmontados.

   Para obtener los documentos PDF desmontados, realice las siguientes acciones:

   * Invocar el método `AssemblerResult` del objeto `getDocuments`. Esto devuelve un objeto `java.util.Map`.
   * Repita el objeto `java.util.Map` hasta que encuentre el objeto `com.adobe.idp.Document` resultante.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para extraer el documento PDF.

**Consulte también**

[Desensamblar Documentos PDF mediante programación](#programmatically-disassembling-pdf-documents)

[Inicio rápido (modo SOAP): Desmontaje de un documento PDF mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Desmontar un documento PDF mediante la API de servicio Web {#disassemble-a-pdf-document-using-the-web-service-api}

Desmontar un documento PDF mediante la API de servicio de ensamblador (servicio Web):

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

1. Haga referencia a un documento DDX existente.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el documento DDX.
   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento DDX y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Haga referencia a un documento PDF para desmontarlo.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el documento PDF de entrada. Este objeto `BLOB` se pasa a `invokeOneDocument` como argumento.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` el contenido de la matriz de bytes.
   * Cree un objeto `MyMapOf_xsd_string_To_xsd_anyType`. Este objeto de colección se utiliza para almacenar el PDF que se va a desmontar.
   * Cree un objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Asigne un valor de cadena que represente el nombre clave al campo `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key`. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX.
   * Asigne el objeto `BLOB` que almacena el documento PDF al campo `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value`.
   * Añada el objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` al objeto `MyMapOf_xsd_string_To_xsd_anyType`. Invoque el método `MyMapOf_xsd_string_To_xsd_anyType` object’ `Add` y pase el objeto `MyMapOf_xsd_string_To_xsd_anyType`.

1. Configure las opciones de tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene las opciones de tiempo de ejecución mediante su constructor.
   * Configure las opciones de tiempo de ejecución para satisfacer los requisitos comerciales asignando un valor a un miembro de datos que pertenece al objeto `AssemblerOptionSpec`. Por ejemplo, para indicar al servicio Ensamblador que continúe procesando un trabajo cuando se produzca un error, asigne `false` al campo `AssemblerOptionSpec` del objeto `failOnError`.

1. Desmonte el documento PDF.

   Invoque el método `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento DDX que desmonta el documento PDF
   * El objeto `MyMapOf_xsd_string_To_xsd_anyType` que contiene el documento PDF que se va a desmontar
   * Un objeto `AssemblerOptionSpec` que especifica opciones de tiempo de ejecución

   El método `invokeDDX` devuelve un objeto `AssemblerResult` que contiene los resultados del trabajo y las excepciones que se han producido.

1. Guarde los documentos PDF desmontados.

   Para obtener los documentos PDF recién creados, realice las siguientes acciones:

   * Acceda al campo `AssemblerResult` del objeto `documents`, que es un objeto `Map` que contiene los documentos PDF desmontados.
   * Repita el objeto `Map` para obtener cada documento resultante. A continuación, convierta el `value` miembro del arreglo de discos en un `BLOB`.
   * Extraiga los datos binarios que representan el documento PDF accediendo a la propiedad `BLOB` del objeto `MTOM`. Esto devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también**

[Desensamblar Documentos PDF mediante programación](#programmatically-disassembling-pdf-documents)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
