---
title: Agrupar documentos PDF con marcadores
seo-title: Assembling PDF Documents with Bookmarks
description: Utilice el servicio Assembler para modificar un documento de PDF que no contenga marcadores para incluir marcadores mediante la API de Java y la API de servicio Web.
seo-description: Use the Assembler service to modify a PDF document that does contain bookmarks to include bookmarks using the Java API and the Web Service API.
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
role: Developer
exl-id: 2b938410-f51b-420b-b5d4-2ed13ec29c5a
source-git-commit: 10227bcfcfd5a9b0f126fee74dce6ec7842f5e95
workflow-type: tm+mt
source-wordcount: '2558'
ht-degree: 0%

---

# Agrupar documentos PDF con marcadores {#assembling-pdf-documents-with-bookmarks}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

Puede combinar un documento de PDF que contenga marcadores. Por ejemplo, supongamos que tiene un documento de PDF que no contiene marcadores y desea modificarlo proporcionando marcadores. Con el servicio Assembler, puede pasarle un documento de PDF que no contenga marcadores y recuperar un documento de PDF que contenga marcadores.

Los marcadores contienen las siguientes propiedades:

* Título que aparece como texto en la pantalla.
* Una acción que especifica lo que sucede cuando un usuario hace clic en el marcador. La acción típica de un marcador es moverse a otra ubicación en el documento actual o abrir otro documento de PDF, aunque se pueden especificar otras acciones.

A los efectos de este análisis, supongamos que se utiliza el siguiente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
       <PDF result="FinalDoc.pdf">
          <PDF source="Loan.pdf">
             <Bookmarks source="doc2" />
          </PDF>
       </PDF>
 </DDX>
```

Dentro de este documento DDX, observe que el atributo de origen tiene asignado el valor `Loan.pdf`. Este documento DDX especifica que se pasa un solo documento de PDF al servicio Assembler. Al combinar un documento de PDF con marcadores, debe especificar un documento XML de marcador que describa los marcadores en el documento de resultados. Para especificar un documento XML de marcador, asegúrese de que la variable `Bookmarks` se especifica en el documento DDX.

En este documento DDX de ejemplo, la variable `Bookmarks` element especifica `doc2` como el valor. Este valor indica que el mapa de entrada pasado al servicio Assembler contiene una clave denominada `doc2`. El valor del `doc2` la clave es un `com.adobe.idp.Document` que representa el documento XML de marcador. (Consulte &quot;Idioma de los marcadores&quot; en la [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).)

En este tema se utiliza el siguiente lenguaje de marcadores XML para combinar un documento de PDF que contenga marcadores.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <Bookmarks xmlns="https://ns.adobe.com/pdf/bookmarks" version="1.0">
       <Bookmark>
          <Action>
             <Launch NewWindow="true">
                <File Name="C:\Adobe\LoanDetails.pdf" />
             </Launch>
          </Action>
         <Title>Open the Loan document</Title>
       </Bookmark>
 <Bookmark>
          <Action>
             <Launch>
                <Win Name="C:\WINDOWS\notepad.exe" />
             </Launch>
          </Action>
     <Title>Launch NotePad</Title>
       </Bookmark>
 </Bookmarks>
```

Dentro de este documento XML de marcador, observe el elemento Action que define la acción que se realiza cuando un usuario hace clic en el marcador. Debajo del elemento Action está el elemento Launch que inicia aplicaciones, como NotePad y abre archivos, como archivos de PDF. Para abrir un archivo de PDF, debe utilizar el elemento File que especifica el archivo que se va a abrir. Por ejemplo, en el archivo XML de marcador especificado en esta sección, el nombre del archivo que se abre es LoanDetails.pdf.

>[!NOTE]
>
>Para obtener más información sobre las acciones compatibles, consulte `Action` element&quot; en [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

Dado el documento DDX especificado en esta sección y el archivo XML de marcador como entrada, el servicio Assembler monta un documento de PDF que contiene los siguientes marcadores.

![aw_aw_bmark](assets/aw_aw_bmark.png)

Cuando un usuario hace clic en *Abrir los detalles del préstamo* , se abre LoanDetails.pdf. Del mismo modo, cuando el usuario hace clic en la variable *Iniciar NotePad* marcador, NotePad se inicia.

>[!NOTE]
>
>Antes de leer esta sección, se recomienda que esté familiarizado con el ensamblado de documentos de PDF mediante el servicio Assembler. En esta sección no se tratan conceptos como, por ejemplo, la creación de un objeto de colección que contenga documentos de entrada o el aprendizaje de cómo extraer los resultados del objeto de colección devuelto. (Consulte [Agrupar documentos de PDF mediante programación](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents).)

>[!NOTE]
>
>Para obtener más información sobre el servicio Assembler, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para combinar un documento de PDF que contenga marcadores, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDF Assembler.
1. Hacer referencia a un documento DDX existente.
1. Hacer referencia a un documento de PDF al que se agregan marcadores.
1. Haga referencia al documento XML de marcador.
1. Agregue el documento PDF y el documento XML de marcador a una colección Map.
1. Establecer opciones en tiempo de ejecución.
1. Montar el documento del PDF.
1. Guarde el documento de PDF que contiene marcadores.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-utilities.jar y jbossall-client.jar con archivos JAR específicos del servidor de aplicaciones J2EE en el que AEM Forms está implementado. Para obtener información sobre la ubicación de todos los archivos JAR de AEM Forms, consulte [Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de PDF Assembler**

Para poder realizar mediante programación una operación de Assembler, debe crear un cliente de servicio Assembler.

**Hacer referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para combinar un documento de PDF. Este documento DDX debe contener la variable `Bookmarks` , que indica al servicio Assembler que combine un PDF que contiene marcadores. (Consulte el documento DDX mostrado anteriormente en esta sección para ver un ejemplo).

**Hacer referencia a un documento de PDF al que se agregan marcadores**

Hacer referencia a un documento de PDF al que se agregan marcadores. No importa si el documento de PDF al que se hace referencia ya contiene marcadores. Si la variable `Bookmarks` es un elemento secundario del elemento de origen PDF, luego los marcadores reemplazarán a los que ya existen en el origen PDF. Sin embargo, si desea conservar los marcadores existentes, asegúrese de que `Bookmarks` es un elemento del mismo nivel del elemento de origen PDF. Veamos el siguiente ejemplo:

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**Hacer referencia al documento XML de marcador**

Para combinar un PDF que contenga marcadores nuevos, debe hacer referencia a un documento XML de marcador. El documento XML de marcador se pasa al servicio Assembler dentro del objeto de la colección Map. (Consulte el documento XML de marcadores que se muestra anteriormente en esta sección para ver un ejemplo).

>[!NOTE]
>
>Consulte &quot;Idioma de los marcadores&quot; en la [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

**Agregue el documento PDF y el documento XML de marcador a una colección Map**

Debe agregar el documento PDF al que se agregan los marcadores y el documento XML de marcador a la colección Map. Por lo tanto, el objeto de la colección Map contiene dos elementos: un documento de PDF y el documento XML de marcador.

**Establecer opciones en tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlen el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede establecer una opción que indique al servicio Assembler que continúe procesando un trabajo si se produce un error. Para obtener información acerca de las opciones en tiempo de ejecución que puede establecer, vea la `AssemblerOptionSpec` referencia de clase en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Montar el documento de PDF**

Para combinar un documento de PDF que contenga nuevos marcadores, utilice el `invokeDDX` operación. El motivo por el que debe utilizar la variable `invokeDDX` a diferencia de otras operaciones del servicio Assembler como `invokeOneDocument` Esto se debe a que el servicio Assembler requiere un documento XML de marcador que se pasa dentro del objeto de colección Map. Este objeto es un parámetro del `invokeDDX` operación.

**Guarde el documento de PDF que contiene marcadores**

Debe extraer los resultados del objeto de asignación devuelto y guardar el documento de PDF correspondiente. (Consulte &quot;Extraer los resultados&quot; en [Agrupar documentos de PDF mediante programación](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Ensamble documentos de PDF con marcadores mediante la API de Java {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Ensamble un documento de PDF con marcadores mediante la API del servicio Assembler (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de PDF Assembler.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión. (Consulte [Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Crear un `AssemblerServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Hacer referencia a un documento DDX existente.

   * Crear un `java.io.FileInputStream` que representa el documento DDX utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo DDX.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Hacer referencia a un documento de PDF al que se agregan marcadores.

   * Crear un `java.io.FileInputStream` mediante su constructor y pasando la ubicación del documento de PDF.
   * Crear un `com.adobe.idp.Document` mediante su constructor y pase el objeto `java.io.FileInputStream` que contiene el documento de PDF.

1. Haga referencia al documento XML de marcador.

   * Crear un `java.io.FileInputStream` utilizando su constructor y pasando la ubicación del archivo XML que representa el documento XML de marcador.
   * Crear un `com.adobe.idp.Document` y pase el `java.io.FileInputStream` que contiene el documento de PDF.

1. Agregue el documento PDF y el documento XML de marcador a una colección Map.

   * Crear un `java.util.Map` que se utiliza para almacenar el documento del PDF de entrada y el documento XML de marcador.
   * Agregue el documento del PDF de entrada invocando el `java.util.Map` del objeto `put` y pasando los siguientes argumentos:

      * Valor de cadena que representa el nombre de clave. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX.
      * A `com.adobe.idp.Document` que contiene el documento del PDF de entrada.

   * Agregue el documento XML de marcador invocando el `java.util.Map` del objeto `put` y pasando los siguientes argumentos:

      * Valor de cadena que representa el nombre de clave. Este valor debe coincidir con el valor del elemento de origen Bookmarks especificado en el documento DDX.
      * A `com.adobe.idp.Document` que contiene el documento XML de marcador.

1. Establecer opciones en tiempo de ejecución.

   * Crear un `AssemblerOptionSpec` que almacena las opciones en tiempo de ejecución mediante su constructor.
   * Establezca opciones en tiempo de ejecución para satisfacer sus necesidades empresariales invocando un método que pertenezca a `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, invoque el `AssemblerOptionSpec` del objeto `setFailOnError` método y pase `false`.

1. Montar el documento del PDF.

   Invoque el `AssemblerServiceClient` del objeto `invokeDDX` y pasar los siguientes valores obligatorios:

   * A `com.adobe.idp.Document` que representa el documento DDX que se va a utilizar
   * A `java.util.Map` que contiene el documento del PDF de entrada y el documento XML de marcador.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones en tiempo de ejecución, incluida la fuente predeterminada y el nivel de registro de trabajo

   El `invokeDDX` El método devuelve un valor `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene los resultados del trabajo y las excepciones que se han producido.

1. Guarde el documento de PDF que contiene marcadores.

   Para obtener el documento de PDF recién creado, realice las siguientes acciones:

   * Invoque el `AssemblerResult` del objeto `getDocuments` método. Esto devuelve un `java.util.Map` objeto.
   * Itere a través de `java.util.Map` hasta que encuentre el resultado `com.adobe.idp.Document` objeto. (Puede utilizar el elemento de resultado PDF especificado en el documento DDX para obtener el documento).
   * Invoque el `com.adobe.idp.Document` del objeto `copyToFile` para extraer el documento del PDF.

**Consulte también**

[Inicio rápido (modo SOAP): Agrupar documentos de PDF con marcadores mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Ensamble documentos de PDF con marcadores mediante la API de servicio web {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

Ensamble un documento de PDF con marcadores mediante la API del servicio Assembler (servicio web):

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

1. Hacer referencia a un documento de PDF al que se agregan marcadores.

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar el PDF de entrada.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento del PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.

1. Haga referencia al documento XML de marcador.

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar el documento XML de marcador.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento del PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.

1. Agregue el documento PDF y el documento XML de marcador a una colección Map.

   * Crear un `MyMapOf_xsd_string_To_xsd_anyType` objeto. Este objeto de colección se utiliza para almacenar los documentos del PDF de entrada y el documento XML de marcador.
   * Para cada documento del PDF de entrada y el documento XML de marcador , cree un `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Asigne un valor de cadena que represente el nombre de clave al `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key` field. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX.
   * Asigne el `BLOB` que almacena el documento del PDF en `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value` field.
   * Añada el `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto a `MyMapOf_xsd_string_To_xsd_anyType` objeto. Invoque el `MyMapOf_xsd_string_To_xsd_anyType` del objeto `Add` y pase el `MyMapOf_xsd_string_To_xsd_anyType` objeto. (Realice esta tarea para cada documento del PDF de entrada y el documento XML de marcador).

1. Establecer opciones en tiempo de ejecución.

   * Crear un `AssemblerOptionSpec` que almacena las opciones en tiempo de ejecución mediante su constructor.
   * Establezca las opciones en tiempo de ejecución para satisfacer sus necesidades empresariales asignando un valor a un miembro de datos que pertenezca a `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne a `false` a la `AssemblerOptionSpec` del objeto `failOnError` miembro de datos.

1. Montar el documento del PDF.

   Invoque el `AssemblerServiceClient` del objeto `invokeDDX` y pasar los siguientes valores:

   * A `BLOB` que representa el documento DDX
   * El `MyMapOf_xsd_string_To_xsd_anyType` matriz que contiene los documentos de entrada
   * Un `AssemblerOptionSpec` objeto que especifica opciones en tiempo de ejecución

   El `invokeDDX` El método devuelve un `AssemblerResult` que contiene los resultados del trabajo y cualquier excepción que se haya producido.

1. Guarde el documento de PDF que contiene marcadores.

   Para obtener el documento de PDF recién creado, realice las siguientes acciones:

   * Acceda a la `AssemblerResult` del objeto `documents` , que es un `Map` que contiene los documentos del PDF de resultados.
   * Itere a través de `Map` hasta que encuentre la clave que coincida con el nombre del documento resultante. A continuación, convierta el de ese miembro de la matriz `value` a un `BLOB`.
   * Extraiga los datos binarios que representan el documento PDF accediendo a su `BLOB` del objeto `MTOM` field. Devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
