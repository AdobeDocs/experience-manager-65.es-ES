---
title: Compilación de documentos PDF mediante programación
seo-title: Compilación de documentos PDF mediante programación
description: nulo
seo-description: nulo
uuid: aa3f8f39-1fbc-48d0-82ff-6caaadf125fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ebe8136b-2a79-4035-b9d5-aa70a5bbd4af
translation-type: tm+mt
source-git-commit: 868936e0fd20d3867e31f0351d7b388149472fd2

---


# Compilación de documentos PDF mediante programación {#programmatically-assembling-pdf-documents}

Puede utilizar la API de servicio de ensamblador para reunir varios documentos PDF en un único documento PDF. La siguiente ilustración muestra tres documentos PDF que se están combinando en un solo documento PDF.

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

Para montar dos o más documentos PDF en un solo documento PDF, necesita un documento DDX. Un documento DDX describe el documento PDF que produce el servicio Ensamblador. Es decir, el documento DDX indica al servicio Ensamblador qué acciones realizar.

A los efectos de este análisis, supongamos que se utiliza el siguiente documento DDX.

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="out.pdf">
         <PDF source="map.pdf" />
         <PDF source="directions.pdf" />
     </PDF>
 </DDX>
```

Este documento DDX combina dos documentos PDF denominados *map.pdf* y *direcciones.pdf* en un solo documento PDF.

>[!NOTE]
>
>Para ver un documento DDX que desmonta un documento PDF, consulte Desmontaje [programático de documentos](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)PDF.

>[!NOTE]
>
>Para obtener más información sobre el servicio Compilador, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y Referencia](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Consideraciones al invocar el servicio de ensamblador mediante servicios Web {#considerations-when-invoking-assembler-service-using-web-services}

Al agregar encabezados y pies de página durante el ensamblaje de documentos de gran tamaño, es posible que se produzca un `OutOfMemory` error y que los archivos no se ensamblen. Para reducir la posibilidad de que se produzca este problema, agregue un `DDXProcessorSetting` elemento al documento DDX, como se muestra en el siguiente ejemplo.

`<DDXProcessorSetting name="checkpoint" value="2000" />`

Puede agregar este elemento como un elemento secundario del `DDX` elemento o como un elemento secundario de un `PDF result` elemento. El valor predeterminado para este ajuste es 0 (cero), que desactiva la señalización de verificación y el DDX se comporta como si el `DDXProcessorSetting` elemento no estuviera presente. Si ha encontrado un `OutOfMemory` error, es posible que tenga que establecer el valor en un entero, normalmente entre 500 y 5000. Un valor pequeño de punto de comprobación resulta en una comprobación más frecuente.

## Resumen de los pasos {#summary-of-steps}

Para montar un solo documento PDF a partir de varios documentos PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de ensamblador de PDF.
1. Haga referencia a un documento DDX existente.
1. Consulte documentos PDF de entrada.
1. Configure las opciones de tiempo de ejecución.
1. Monte los documentos PDF de entrada.
1. Extraiga los resultados.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms.

**Crear un cliente de ensamblador de PDF**

Para poder realizar una operación de ensamblador mediante programación, debe crear un cliente de ensamblador.

**Hacer referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para ensamblar un documento PDF. Por ejemplo, considere el documento DDX que se introdujo en esta sección. Este documento DDX indica al servicio de ensamblador que combine dos documentos PDF en un único documento PDF.

**Documentos PDF de entrada de referencia**

Haga referencia a los documentos PDF de entrada que desea pasar al servicio de ensamblador. Por ejemplo, si desea pasar dos documentos PDF de entrada denominados Mapa y direcciones, debe pasar los archivos PDF correspondientes.

Tanto el archivo map.pdf como el archivo direccionamiento.pdf deben colocarse en un objeto de recopilación. El nombre de la clave debe coincidir con el valor del atributo de origen PDF en el documento DDX. No importa cuál sea el nombre del archivo PDF si coinciden la clave y el atributo de origen del documento DDX.

>[!NOTE]
>
>Se devuelve un `AssemblerResult` objeto, que contiene un objeto de colección, si se invoca la `invokeDDX` operación. Esta operación se utiliza cuando se pasan dos o más documentos PDF de entrada al servicio Ensamblador. Sin embargo, si solo pasa un archivo PDF de entrada al servicio Ensamblador y espera un solo documento de devolución, invoque la `invokeOneDocument` operación. Al invocar esta operación, se devuelve un solo documento. Para obtener información sobre el uso de esta operación, consulte [Compilación de documentos](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents)PDF cifrados.

**Definición de opciones de tiempo de ejecución**

Puede definir opciones en tiempo de ejecución que controlen el comportamiento del servicio de ensamblador mientras realiza un trabajo. Por ejemplo, puede definir una opción que indique al servicio Ensamblador que continúe procesando un trabajo si se produce un error. Para obtener información sobre las opciones de tiempo de ejecución que puede definir, consulte la referencia de la `AssemblerOptionSpec` clase en Referencia [de API de formularios](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM.

**Compilación de documentos PDF de entrada**

Después de crear el cliente de servicio, hacer referencia a un archivo DDX, crear un objeto de colección que almacene los documentos PDF de entrada y definir las opciones de tiempo de ejecución, puede invocar la operación DDX. Al utilizar el documento DDX especificado en esta sección, los archivos map.pdf y direction.pdf se combinan en un documento PDF.

**Extraer los resultados**

El servicio Ensamblador devuelve un `java.util.Map` objeto, que se puede obtener del `AssemblerResult` objeto y que contiene los resultados de la operación. El `java.util.Map` objeto devuelto contiene los documentos resultantes y cualquier excepción.

En la tabla siguiente se resumen algunos de los valores clave y tipos de objetos que se pueden situar en el `java.util.Map` objeto devuelto.

<table>
 <thead>
  <tr>
   <th><p>Valor clave</p></th>
   <th><p>Tipo de objeto</p></th>
   <th><p>Descripción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>com.adobe.idp.Document</code></p></td>
   <td><p>Contiene los documentos resultantes especificados en un elemento resultante DDX</p></td>
  </tr>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>Exception</code></p></td>
   <td><p>Contiene cualquier excepción para el documento</p></td>
  </tr>
  <tr>
   <td><p><code>OutputMapConstants.LOG_NAME</code></p></td>
   <td><p><code>com.adobe.idp.Documen</code></p></td>
   <td><p>Contiene el registro de trabajos</p></td>
  </tr>
 </tbody>
</table>

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Desensamblar documentos PDF mediante programación](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Compilación de documentos PDF mediante la API de Java {#assemble-pdf-documents-using-the-java-api}

Compilación de un documento PDF mediante la API de servicio de ensamblador (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de ensamblador de PDF.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `AssemblerServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un documento DDX existente.

   * Cree un `java.io.FileInputStream` objeto que represente el documento DDX utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo DDX.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Consulte documentos PDF de entrada.

   * Cree un `java.util.Map` objeto que se utilice para almacenar documentos PDF de entrada mediante un `HashMap` constructor.
   * Para cada documento PDF de entrada, cree un `java.io.FileInputStream` objeto utilizando su constructor y pasando la ubicación del documento PDF de entrada.
   * Para cada documento PDF de entrada, cree un `com.adobe.idp.Document` objeto y pase el `java.io.FileInputStream` objeto que contiene el documento PDF.
   * Para cada documento de entrada, agregue una entrada al `java.util.Map` objeto invocando su `put` método y pasando los siguientes argumentos:

      * Un valor de cadena que representa el nombre de la clave. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX.
      * Un `com.adobe.idp.Document` objeto (o `java.util.List` objeto que especifica varios documentos) que contiene el documento PDF de origen.

1. Configure las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` objeto que almacene opciones de tiempo de ejecución mediante su constructor.
   * Configure las opciones de tiempo de ejecución para cumplir los requisitos comerciales invocando un método que pertenece al `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Ensamblador que continúe procesando un trabajo cuando se produzca un error, invoque el `AssemblerOptionSpec` método del `setFailOnError` objeto y pase `false`.

1. Monte los documentos PDF de entrada.

   Invoque el `AssemblerServiceClient` método del `invokeDDX` objeto y pase los siguientes valores obligatorios:

   * Un `com.adobe.idp.Document` objeto que representa el documento DDX que se va a utilizar
   * Un `java.util.Map` objeto que contiene los archivos PDF de entrada que se van a montar
   * Un `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica las opciones en tiempo de ejecución, incluidos el nivel predeterminado de fuente y registro de trabajos
   El `invokeDDX` método devuelve un `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contiene los resultados del trabajo y las excepciones que se hayan producido.

1. Extraiga los resultados.

   Para obtener el documento PDF recién creado, realice las siguientes acciones:

   * Invocar el `AssemblerResult` método del `getDocuments` objeto. Esto devuelve un `java.util.Map` objeto.
   * Repita el `java.util.Map` objeto hasta que encuentre el `com.adobe.idp.Document` objeto resultante. (Puede utilizar el elemento de resultado PDF especificado en el documento DDX para obtener el documento).
   * Invocar el `com.adobe.idp.Document` método del `copyToFile` objeto para extraer el documento PDF.
   >[!NOTE]
   >
   >Si `LOG_LEVEL` se configuró para generar un registro, puede extraer el registro utilizando el `AssemblerResult` método `getJobLog` del objeto.

**Consulte también**

[Inicio rápido (modo SOAP): Compilación de un documento PDF mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Compilación de documentos PDF mediante la API de servicio Web {#assemble-pdf-documents-using-the-web-service-api}

Compilación de documentos PDF mediante la API de servicio de ensamblador (servicio Web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento DDX y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` propiedad con el contenido de la matriz de bytes.

1. Consulte documentos PDF de entrada.

   * Para cada documento PDF de entrada, cree un `BLOB` objeto utilizando su constructor. El `BLOB` objeto se utiliza para almacenar el documento PDF de entrada.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Este objeto de colección se utiliza para almacenar documentos PDF de entrada.
   * Para cada documento PDF de entrada, cree un `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto. Por ejemplo, si se utilizan dos documentos PDF de entrada, cree dos `MyMapOf_xsd_string_To_xsd_anyType_Item` objetos.
   * Asigne un valor de cadena que represente el nombre clave al `MyMapOf_xsd_string_To_xsd_anyType_Item` campo del `key` objeto. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX. (Realice esta tarea para cada documento PDF de entrada).
   * Asigne el `BLOB` objeto que almacena el documento PDF al `MyMapOf_xsd_string_To_xsd_anyType_Item` campo del `value` objeto. (Realice esta tarea para cada documento PDF de entrada).
   * Agregue el `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto al `MyMapOf_xsd_string_To_xsd_anyType` objeto. Invoque el `MyMapOf_xsd_string_To_xsd_anyType` método del `Add` objeto y pase el `MyMapOf_xsd_string_To_xsd_anyType` objeto. (Realice esta tarea para cada documento PDF de entrada).

1. Configure las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` objeto que almacene opciones de tiempo de ejecución mediante su constructor.
   * Configure las opciones de tiempo de ejecución para cumplir los requisitos comerciales asignando un valor a un miembro de datos que pertenece al `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Ensamblador que continúe procesando un trabajo cuando se produzca un error, asigne `false` al miembro de datos del `AssemblerOptionSpec` objeto `failOnError` .

1. Monte los documentos PDF de entrada.

   Invoque el `AssemblerServiceClient` método del `invoke` objeto y pase los valores siguientes:

   * Un `BLOB` objeto que representa el documento DDX.
   * La `mapItem` matriz que contiene los documentos PDF de entrada. Sus claves deben coincidir con los nombres de los archivos de origen PDF y sus valores deben ser los `BLOB` objetos que correspondan a dichos archivos.
   * Un `AssemblerOptionSpec` objeto que especifica opciones de tiempo de ejecución.
   El `invoke` método devuelve un `AssemblerResult` objeto que contiene los resultados del trabajo y las excepciones que puedan haberse producido.

1. Extraiga los resultados.

   Para obtener el documento PDF recién creado, realice las siguientes acciones:

   * Acceda al `AssemblerResult` campo del `documents` objeto, que es un `Map` objeto que contiene los documentos PDF resultantes.
   * Repita el `Map` objeto hasta que encuentre la clave que coincida con el nombre del documento resultante. A continuación, convierta los elementos del miembro `value` de la matriz en un `BLOB`.
   * Extraiga los datos binarios que representan el documento PDF accediendo a la propiedad del `BLOB` objeto `MTOM` . Esto devuelve una matriz de bytes que puede escribir en un archivo PDF.
   >[!NOTE]
   >
   >Si `LOG_LEVEL` se configuró para generar un registro, puede extraer el registro obteniendo el valor del miembro de datos del `AssemblerResult` objeto `jobLog` .

**Consulte también**

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
