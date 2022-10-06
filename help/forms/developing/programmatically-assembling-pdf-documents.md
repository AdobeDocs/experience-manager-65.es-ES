---
title: Configuración programática de documentos PDF
seo-title: Programmatically Assembling PDF Documents
description: Utilice la API del servicio Assembler para ensamblar varios documentos de PDF en un único documento de PDF mediante la API de Java y la API del servicio Web.
seo-description: Use the Assembler service API to assemble multiple PDF documents into a single PDF document using the Java API and the Web Service API.
uuid: aa3f8f39-1fbc-48d0-82ff-6caaadf125fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ebe8136b-2a79-4035-b9d5-aa70a5bbd4af
role: Developer
exl-id: 7d6fd230-e477-4286-9fb3-18a3474e3e48
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2124'
ht-degree: 0%

---

# Configuración programática de documentos PDF {#programmatically-assembling-pdf-documents}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

Puede utilizar la API del servicio Assembler para ensamblar varios documentos de PDF en un único documento de PDF. La siguiente ilustración muestra tres documentos PDF que se están combinando en un solo documento PDF.

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

Para ensamblar dos o más documentos PDF en un único documento PDF, se necesita un documento DDX. Un documento DDX describe el documento PDF que produce el servicio Assembler. Es decir, el documento DDX indica al servicio Assembler qué acciones realizar.

A los efectos de esta discusión, supongamos que se utiliza el siguiente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="out.pdf">
         <PDF source="map.pdf" />
         <PDF source="directions.pdf" />
     </PDF>
 </DDX>
```

Este documento DDX combina dos documentos PDF llamados *map.pdf* y *addresses.pdf* en un documento de PDF único.

>[!NOTE]
>
>Para ver un documento DDX que desmonta un documento PDF, consulte [Desmontaje programático de documentos PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents).

>[!NOTE]
>
>Para obtener más información sobre el servicio Assembler, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Consideraciones al invocar el servicio Assembler mediante servicios web {#considerations-when-invoking-assembler-service-using-web-services}

Al agregar encabezados y pies de página durante el ensamblaje de documentos grandes, puede encontrar una `OutOfMemory` y los archivos no se ensamblarán. Para reducir las posibilidades de que se produzca este problema, agregue una `DDXProcessorSetting` del documento DDX, como se muestra en el siguiente ejemplo.

`<DDXProcessorSetting name="checkpoint" value="2000" />`

Puede añadir este elemento como un elemento secundario del `DDX` o como elemento secundario de un `PDF result` elemento. El valor predeterminado de esta configuración es 0 (cero), que desactiva la señalización y el DDX se comporta como si el valor `DDXProcessorSetting` no está presente. Si ha encontrado un `OutOfMemory` error, es posible que tenga que establecer el valor en un entero, normalmente entre 500 y 5000. Un valor pequeño de punto de comprobación resulta en comprobaciones más frecuentes.

## Resumen de los pasos {#summary-of-steps}

Para ensamblar un solo documento de PDF a partir de varios documentos de PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de ensamblador de PDF.
1. Haga referencia a un documento DDX existente.
1. Documentos de PDF de entrada de referencia.
1. Establezca las opciones de tiempo de ejecución.
1. Ensamble los documentos del PDF de entrada.
1. Extraiga los resultados.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-Utilities.jar y jbossall-client.jar con archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms.

**Creación de un cliente de ensamblador de PDF**

Para poder realizar una operación Assembler mediante programación, debe crear un cliente Assembler.

**Referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para ensamblar un documento PDF. Por ejemplo, considere el documento DDX que se introdujo en esta sección. Este documento DDX ordena al servicio Assembler que combine dos documentos PDF en un único documento PDF.

**Documentos de PDF de entrada de referencia**

Haga referencia a los documentos del PDF de entrada que desee pasar al servicio Assembler. Por ejemplo, si desea pasar dos documentos de PDF de entrada llamados Mapa y direcciones, debe pasar los archivos de PDF correspondientes.

Tanto el archivo map.pdf como el archivo addresses.pdf deben colocarse en un objeto de colección. El nombre de la clave debe coincidir con el valor del atributo de origen del PDF en el documento DDX. No importa cuál sea el nombre del archivo PDF si coinciden la clave y el atributo de origen del documento DDX.

>[!NOTE]
>
>Un `AssemblerResult` , que contiene un objeto de colección, se devuelve si invoca el objeto `invokeDDX` operación. Esta operación se utiliza cuando se pasan dos o más documentos de PDF de entrada al servicio Assembler. Sin embargo, si pasa un solo PDF de entrada al servicio Assembler y espera un solo documento devuelto, invoque la variable `invokeOneDocument` operación. Al invocar esta operación, se devuelve un solo documento. Para obtener información sobre el uso de esta operación, consulte [Montaje de documentos de PDF cifrados](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents).

**Establecer opciones de tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlan el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede definir una opción que indique al servicio Assembler que continúe procesando un trabajo si se encuentra un error. Para obtener información sobre las opciones de tiempo de ejecución que puede establecer, consulte la `AssemblerOptionSpec` referencia de clase en [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Montaje de los documentos del PDF de entrada**

Después de crear el cliente de servicio, hacer referencia a un archivo DDX, crear un objeto de colección que almacene documentos de PDF de entrada y establecer opciones de tiempo de ejecución, puede invocar la operación DDX. Cuando se utiliza el documento DDX especificado en esta sección, los archivos map.pdf y address.pdf se combinan en un documento PDF.

**Extraer los resultados**

El servicio Assembler devuelve un valor `java.util.Map` que se puede obtener de la variable `AssemblerResult` y que contiene resultados de operación. El `java.util.Map` contiene los documentos resultantes y cualquier excepción.

En la tabla siguiente se resumen algunos de los valores clave y tipos de objeto que se pueden encontrar en la `java.util.Map` objeto.

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

**Consulte también lo siguiente**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Desmontaje programático de documentos PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Montaje de documentos del PDF mediante la API de Java {#assemble-pdf-documents-using-the-java-api}

Ensamble un documento de PDF mediante la API del servicio Assembler (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-assembler-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente de ensamblador de PDF.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `AssemblerServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un documento DDX existente.

   * Cree un `java.io.FileInputStream` objeto que representa el documento DDX utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo DDX.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Documentos de PDF de entrada de referencia.

   * Cree un `java.util.Map` objeto que se utiliza para almacenar documentos del PDF de entrada mediante un `HashMap` constructor.
   * Para cada documento del PDF de entrada, cree un `java.io.FileInputStream` usando su constructor y pasando la ubicación del documento del PDF de entrada.
   * Para cada documento del PDF de entrada, cree un `com.adobe.idp.Document` y pase el `java.io.FileInputStream` objeto que contiene el documento PDF.
   * Para cada documento de entrada, agregue una entrada al `java.util.Map` invocando su `put` y pasando los siguientes argumentos:

      * Un valor de cadena que representa el nombre de la clave. Este valor debe coincidir con el valor del elemento de origen del PDF especificado en el documento DDX.
      * A `com.adobe.idp.Document` objeto (o `java.util.List` objeto que especifica varios documentos) que contiene el documento del PDF de origen.

1. Establezca las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` que almacena opciones en tiempo de ejecución mediante su constructor.
   * Configure las opciones en tiempo de ejecución para satisfacer los requisitos empresariales invocando un método que pertenece al `AssemblerOptionSpec` objeto. Por ejemplo, para solicitar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, invoque la función `AssemblerOptionSpec` del objeto `setFailOnError` método y pase `false`.

1. Ensamble los documentos del PDF de entrada.

   Invocar el `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores obligatorios:

   * A `com.adobe.idp.Document` objeto que representa el documento DDX que se va a utilizar
   * A `java.util.Map` objeto que contiene los archivos de PDF de entrada que se van a ensamblar
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica las opciones de tiempo de ejecución, incluido el nivel predeterminado de fuente y registro de trabajo

   La variable `invokeDDX` el método devuelve un `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene los resultados del trabajo y cualquier excepción que se haya producido.

1. Extraiga los resultados.

   Para obtener el documento de PDF recién creado, realice las siguientes acciones:

   * Invocar el `AssemblerResult` del objeto `getDocuments` método. Esto devuelve un `java.util.Map` objeto.
   * Iterar a través de la variable `java.util.Map` hasta que encuentre el resultado `com.adobe.idp.Document` objeto. (Puede utilizar el elemento de resultado del PDF especificado en el documento DDX para obtener el documento).
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` método para extraer el documento PDF.

   >[!NOTE]
   >
   >If `LOG_LEVEL` se configuró para producir un registro, puede extraer el registro utilizando la variable `AssemblerResult` del objeto `getJobLog` método.

**Consulte también lo siguiente**

[Inicio rápido (modo SOAP): Montaje de un documento de PDF mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Montaje de documentos del PDF mediante la API de servicio web {#assemble-pdf-documents-using-the-web-service-api}

Ensamble los documentos del PDF mediante la API del servicio Assembler (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento DDX y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Documentos de PDF de entrada de referencia.

   * Para cada documento del PDF de entrada, cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar el documento del PDF de entrada.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento del PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` método. Pase la matriz de bytes, la posición de inicio y la longitud del flujo para leerlos.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.
   * Cree un `MyMapOf_xsd_string_To_xsd_anyType` objeto. Este objeto de colección se utiliza para almacenar documentos de PDF de entrada.
   * Para cada documento del PDF de entrada, cree un `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto. Por ejemplo, si se utilizan dos documentos de PDF de entrada, cree dos `MyMapOf_xsd_string_To_xsd_anyType_Item` objetos.
   * Asigne un valor de cadena que represente el nombre de clave a la variable `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key` campo . Este valor debe coincidir con el valor del elemento de origen del PDF especificado en el documento DDX. (Realice esta tarea para cada documento del PDF de entrada).
   * Asigne la variable `BLOB` objeto que almacena el documento del PDF en el `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value` campo . (Realice esta tarea para cada documento del PDF de entrada).
   * Agregue la variable `MyMapOf_xsd_string_To_xsd_anyType_Item` al `MyMapOf_xsd_string_To_xsd_anyType` objeto. Invocar el `MyMapOf_xsd_string_To_xsd_anyType` del objeto `Add` y pase el `MyMapOf_xsd_string_To_xsd_anyType` objeto. (Realice esta tarea para cada documento del PDF de entrada).

1. Establezca las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` que almacena opciones en tiempo de ejecución mediante su constructor.
   * Configure las opciones en tiempo de ejecución para satisfacer los requisitos empresariales asignando un valor a un miembro de datos que pertenezca al grupo `AssemblerOptionSpec` objeto. Por ejemplo, para solicitar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne `false` a `AssemblerOptionSpec` del objeto `failOnError` miembro de datos.

1. Ensamble los documentos del PDF de entrada.

   Invocar el `AssemblerServiceClient` del objeto `invoke` y pase los siguientes valores:

   * A `BLOB` que representa el documento DDX.
   * La variable `mapItem` matriz que contiene los documentos del PDF de entrada. Sus claves deben coincidir con los nombres de los archivos de origen del PDF, y sus valores deben ser `BLOB` objetos que corresponden a esos archivos.
   * Un `AssemblerOptionSpec` objeto que especifica opciones en tiempo de ejecución.

   La variable `invoke` devuelve un valor `AssemblerResult` objeto que contiene los resultados del trabajo y cualquier excepción que pueda haberse producido.

1. Extraiga los resultados.

   Para obtener el documento de PDF recién creado, realice las siguientes acciones:

   * Acceda a la `AssemblerResult` del objeto `documents` , que es un `Map` que contiene los documentos del PDF de resultados.
   * Iterar a través de la variable `Map` hasta que encuentre la clave que coincida con el nombre del documento resultante. A continuación, cree el `value` a `BLOB`.
   * Extraiga los datos binarios que representan el documento del PDF accediendo a su `BLOB` del objeto `MTOM` propiedad. Esto devuelve una matriz de bytes que puede escribir en un archivo PDF.

   >[!NOTE]
   >
   >If `LOG_LEVEL` se ha configurado para producir un registro, puede extraer el registro obteniendo el valor de la variable `AssemblerResult` del objeto `jobLog` miembro de datos.

**Consulte también lo siguiente**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
