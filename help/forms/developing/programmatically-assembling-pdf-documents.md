---
title: Configuración programática de documentos PDF
description: Utilice la API del servicio Assembler para combinar varios documentos de PDF PDF en uno solo mediante la API de Java y la API del servicio web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 7d6fd230-e477-4286-9fb3-18a3474e3e48
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,  Document Services
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '2105'
ht-degree: 0%

---

# Configuración programática de documentos PDF {#programmatically-assembling-pdf-documents}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

Puede utilizar la API del servicio Assembler para combinar varios documentos de PDF en un único documento de PDF. La siguiente ilustración muestra tres documentos de PDF PDF que se combinan en uno solo.

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

Para combinar dos o más documentos de PDF en un único documento de PDF, necesita un documento DDX. Un documento DDX describe el documento de PDF que produce el servicio Assembler. Es decir, el documento DDX indica al servicio Assembler qué acciones debe realizar.

A los efectos de este análisis, supongamos que se utiliza el siguiente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="out.pdf">
         <PDF source="map.pdf" />
         <PDF source="directions.pdf" />
     </PDF>
 </DDX>
```

Este documento DDX combina dos documentos de PDF llamados *map.pdf* y *direction.pdf* en un solo documento de PDF.

>[!NOTE]
>
>Para ver un documento DDX que desmonta un documento de PDF, consulte [Desmontaje programático de documentos de PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents).

>[!NOTE]
>
>Para obtener más información sobre el servicio Assembler, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Consideraciones al invocar el servicio Assembler mediante servicios web {#considerations-when-invoking-assembler-service-using-web-services}

Cuando se agregan encabezados y pies de página durante el ensamblado de documentos grandes, puede encontrarse con un `OutOfMemory` error y los archivos no se ensamblarán. Para reducir las posibilidades de que se produzca este problema, agregue una `DDXProcessorSetting` al documento DDX, como se muestra en el siguiente ejemplo.

`<DDXProcessorSetting name="checkpoint" value="2000" />`

Puede añadir este elemento como elemento secundario del `DDX` o como elemento secundario de un elemento `PDF result` Elemento. El valor predeterminado para esta configuración es 0 (cero), que desactiva el punto de comprobación y el DDX se comporta como si el `DDXProcessorSetting` el elemento no está presente. Si ha encontrado un `OutOfMemory` error, es posible que deba establecer el valor en un entero, normalmente entre 500 y 5000. Un valor de punto de comprobación pequeño provoca puntos de comprobación más frecuentes.

## Resumen de los pasos {#summary-of-steps}

Para combinar un único documento de PDF a partir de varios documentos de PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDF Assembler.
1. Hacer referencia a un documento DDX existente.
1. Documentos de PDF de entrada de referencia.
1. Establecer opciones en tiempo de ejecución.
1. Monte los documentos del PDF de entrada.
1. Extraiga los resultados.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-utilities.jar y jbossall-client.jar con archivos JAR específicos del servidor de aplicaciones J2EE en el que está implementado AEM Forms.

**Crear un cliente de PDF Assembler**

Para poder realizar mediante programación una operación de Assembler, debe crear un cliente Assembler.

**Hacer referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para combinar un documento de PDF. Por ejemplo, considere el documento DDX que se introdujo en esta sección. Este documento DDX indica al servicio Assembler que combine dos documentos de PDF en un único documento de PDF.

**Documentos del PDF de entrada de referencia**

Hacer referencia a los documentos del PDF de entrada que desee pasar al servicio Assembler. Por ejemplo, si desea pasar dos documentos de PDF de entrada denominados Mapa y Direcciones, debe pasar los archivos de PDF correspondientes.

Tanto el archivo map.pdf como el archivo direction.pdf deben colocarse en un objeto de colección. El nombre de la clave debe coincidir con el valor del atributo de origen del PDF en el documento DDX. No importa cuál sea el nombre del archivo PDF si la clave y el atributo de origen del documento DDX coinciden.

>[!NOTE]
>
>Un `AssemblerResult` objeto, que contiene un objeto de colección, se devuelve si invoca el `invokeDDX` operación. Esta operación se utiliza cuando se pasan dos o más documentos del PDF de entrada al servicio Assembler. Sin embargo, si pasa un solo PDF de entrada al servicio Assembler y espera solo un documento de retorno, invoque el `invokeOneDocument` operación. Al invocar esta operación, se devuelve un solo documento. Para obtener información sobre el uso de esta operación, consulte [Agrupar documentos de PDF cifrados](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents).

**Establecer opciones en tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlen el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede establecer una opción que indique al servicio Assembler que continúe procesando un trabajo si se produce un error. Para obtener información acerca de las opciones en tiempo de ejecución que puede establecer, vea la `AssemblerOptionSpec` referencia de clase en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Montar los documentos del PDF de entrada**

Después de crear el cliente de servicio, hacer referencia a un archivo DDX, crear un objeto de colección que almacene documentos del PDF de entrada y establecer opciones en tiempo de ejecución, puede invocar la operación DDX. Al utilizar el documento DDX especificado en esta sección, los archivos map.pdf y direction.pdf se combinan en un documento de PDF.

**Extraer los resultados**

El servicio Assembler devuelve un `java.util.Map` objeto, que se puede obtener del `AssemblerResult` y que contiene los resultados de la operación. El devuelto `java.util.Map` contiene los documentos resultantes y las excepciones.

En la tabla siguiente se resumen algunos de los valores clave y tipos de objeto que se pueden encontrar en los valores devueltos `java.util.Map` objeto.

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

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Desmontaje programático de documentos PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Montar documentos de PDF mediante la API de Java {#assemble-pdf-documents-using-the-java-api}

Montar un documento de PDF mediante la API del servicio Assembler (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de PDF Assembler.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `AssemblerServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Hacer referencia a un documento DDX existente.

   * Crear un `java.io.FileInputStream` que representa el documento DDX utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo DDX.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Documentos de PDF de entrada de referencia.

   * Crear un `java.util.Map` objeto que se utiliza para almacenar documentos del PDF de entrada mediante un `HashMap` constructor.
   * Para cada documento del PDF de entrada, cree un `java.io.FileInputStream` mediante su constructor y pasando la ubicación del documento del PDF de entrada.
   * Para cada documento del PDF de entrada, cree un `com.adobe.idp.Document` y pase el `java.io.FileInputStream` que contiene el documento de PDF.
   * Para cada documento de entrada, agregue una entrada al `java.util.Map` invocando su objeto `put` y pasando los siguientes argumentos:

      * Valor de cadena que representa el nombre de clave. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX.
      * A `com.adobe.idp.Document` objeto (o `java.util.List` que especifica varios documentos) que contiene el documento de PDF de origen.

1. Establecer opciones en tiempo de ejecución.

   * Crear un `AssemblerOptionSpec` que almacena las opciones en tiempo de ejecución mediante su constructor.
   * Establezca opciones en tiempo de ejecución para satisfacer sus necesidades empresariales invocando un método que pertenezca a `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, invoque el `AssemblerOptionSpec` del objeto `setFailOnError` método y pase `false`.

1. Monte los documentos del PDF de entrada.

   Invoque el `AssemblerServiceClient` del objeto `invokeDDX` y pasar los siguientes valores obligatorios:

   * A `com.adobe.idp.Document` que representa el documento DDX que se va a utilizar
   * A `java.util.Map` que contiene los archivos de PDF de entrada que se van a ensamblar
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones en tiempo de ejecución, incluida la fuente predeterminada y el nivel de registro de trabajo

   El `invokeDDX` El método devuelve un valor `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene los resultados del trabajo y las excepciones que se han producido.

1. Extraiga los resultados.

   Para obtener el documento de PDF recién creado, realice las siguientes acciones:

   * Invoque el `AssemblerResult` del objeto `getDocuments` método. Esto devuelve un `java.util.Map` objeto.
   * Itere a través de `java.util.Map` hasta que encuentre el resultado `com.adobe.idp.Document` objeto. (Puede utilizar el elemento de resultado PDF especificado en el documento DDX para obtener el documento).
   * Invoque el `com.adobe.idp.Document` del objeto `copyToFile` para extraer el documento del PDF.

   >[!NOTE]
   >
   >If `LOG_LEVEL` se ha configurado para producir un registro, puede extraerlo utilizando el `AssemblerResult` del objeto `getJobLog` método.

**Consulte también**

[SOAP Inicio rápido (modo de): Agrupar un documento de PDF mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Montar documentos de PDF mediante la API de servicio web {#assemble-pdf-documents-using-the-web-service-api}

Ensamble documentos de PDF mediante la API del servicio Assembler (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación de archivo del documento DDX y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.

1. Documentos de PDF de entrada de referencia.

   * Para cada documento del PDF de entrada, cree un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar el documento del PDF de entrada.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento del PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` método. Pase a leer la matriz de bytes, la posición inicial y la longitud de la secuencia.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.
   * Crear un `MyMapOf_xsd_string_To_xsd_anyType` objeto. Este objeto de colección se utiliza para almacenar documentos del PDF de entrada.
   * Para cada documento del PDF de entrada, cree un `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto. Por ejemplo, si se utilizan dos documentos de PDF de entrada, cree dos `MyMapOf_xsd_string_To_xsd_anyType_Item` objetos.
   * Asigne un valor de cadena que represente el nombre de clave al `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key` field. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX. (Realice esta tarea para cada documento de PDF de entrada).
   * Asigne el `BLOB` que almacena el documento del PDF en `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value` field. (Realice esta tarea para cada documento de PDF de entrada).
   * Añada el `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto a `MyMapOf_xsd_string_To_xsd_anyType` objeto. Invoque el `MyMapOf_xsd_string_To_xsd_anyType` del objeto `Add` y pase el `MyMapOf_xsd_string_To_xsd_anyType` objeto. (Realice esta tarea para cada documento de PDF de entrada).

1. Establecer opciones en tiempo de ejecución.

   * Crear un `AssemblerOptionSpec` que almacena las opciones en tiempo de ejecución mediante su constructor.
   * Establezca las opciones en tiempo de ejecución para satisfacer sus necesidades empresariales asignando un valor a un miembro de datos que pertenezca a `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne a `false` a la `AssemblerOptionSpec` del objeto `failOnError` miembro de datos.

1. Monte los documentos del PDF de entrada.

   Invoque el `AssemblerServiceClient` del objeto `invoke` y pasar los siguientes valores:

   * A `BLOB` que representa el documento DDX.
   * El `mapItem` matriz que contiene los documentos del PDF de entrada. Sus claves deben coincidir con los nombres de los archivos de origen del PDF y sus valores deben ser `BLOB` objetos que corresponden a esos archivos.
   * Un `AssemblerOptionSpec` que especifica las opciones en tiempo de ejecución.

   El `invoke` El método devuelve un `AssemblerResult` que contiene los resultados del trabajo y cualquier excepción que se haya producido.

1. Extraiga los resultados.

   Para obtener el documento de PDF recién creado, realice las siguientes acciones:

   * Acceda a la `AssemblerResult` del objeto `documents` , que es un `Map` que contiene los documentos del PDF de resultados.
   * Itere a través de `Map` hasta que encuentre la clave que coincida con el nombre del documento resultante. A continuación, convierta el de ese miembro de la matriz `value` a un `BLOB`.
   * Extraiga los datos binarios que representan el documento PDF accediendo a su `BLOB` del objeto `MTOM` propiedad. Devuelve una matriz de bytes que puede escribir en un archivo PDF.

   >[!NOTE]
   >
   >If `LOG_LEVEL` se ha configurado para producir un registro, puede extraerlo obteniendo el valor del `AssemblerResult` del objeto `jobLog` miembro de datos.

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
