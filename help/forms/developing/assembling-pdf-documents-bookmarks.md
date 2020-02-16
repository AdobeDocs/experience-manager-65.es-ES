---
title: Compilación de documentos PDF con marcadores
seo-title: Compilación de documentos PDF con marcadores
description: nulo
seo-description: nulo
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Compilación de documentos PDF con marcadores {#assembling-pdf-documents-with-bookmarks}

Puede montar un documento PDF que contenga marcadores. Por ejemplo, supongamos que tiene un documento PDF que no contiene marcadores y que desea modificarlo proporcionando marcadores. Con el servicio Ensamblador, puede pasarle un documento PDF que no contenga marcadores y recuperar un documento PDF que contenga marcadores.

Los marcadores contienen las siguientes propiedades:

* Título que aparece como texto en la pantalla.
* Acción que especifica lo que sucede cuando un usuario hace clic en el marcador. La acción habitual de un marcador es moverse a otra ubicación del documento actual o abrir otro documento PDF, aunque se pueden especificar otras acciones.

A los efectos de este análisis, supongamos que se utiliza el siguiente documento DDX.

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
       <PDF result="FinalDoc.pdf">
          <PDF source="Loan.pdf">
             <Bookmarks source="doc2" />
          </PDF>
       </PDF>
 </DDX>
```

En este documento DDX, observe que el atributo de origen está asignado al valor `Loan.pdf`. Este documento DDX especifica que se pasa un solo documento PDF al servicio Ensamblador. Al montar un documento PDF con marcadores, debe especificar un documento XML de marcadores que describa los marcadores en el documento de resultados. Para especificar un documento XML de marcador, asegúrese de que el `Bookmarks` elemento está especificado en el documento DDX.

En este documento DDX de ejemplo, el `Bookmarks` elemento especifica `doc2` como valor. Este valor indica que el mapa de entrada pasado al servicio de ensamblador contiene una clave denominada `doc2`. El valor de la `doc2` clave es un `com.adobe.idp.Document` valor que representa el documento XML de marcador. (Consulte &quot;Lenguaje de marcadores&quot; en el servicio [Ensamblador y la referencia](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX).

En este tema se utiliza el siguiente lenguaje de marcadores XML para crear un documento PDF que contenga marcadores.

```as3
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

Dentro de este documento XML de marcador, observe el elemento Acción que define la acción que se realiza cuando un usuario hace clic en el marcador. En el elemento Acción está el elemento Iniciar que inicia aplicaciones, como NotePad y abre archivos, como archivos PDF. Para abrir un archivo PDF, debe utilizar el elemento Archivo que especifica el archivo que se va a abrir. Por ejemplo, en el archivo XML de marcador especificado en esta sección, el nombre del archivo que se abre es LoanDetails.pdf.

>[!NOTE]
>
>Para obtener más información sobre las acciones admitidas, consulte &quot; `Action` element&quot; (elemento) en el servicio [Ensamblador y en la referencia](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

Dado el documento DDX especificado en esta sección y el archivo XML de marcador como entrada, el servicio Ensamblador ensambla un documento PDF que contiene los siguientes marcadores.

![aw_aw_bmark](assets/aw_aw_bmark.png)

Cuando un usuario hace clic en el marcador *Abrir los detalles* del préstamo, se abre LoanDetails.pdf. Del mismo modo, cuando el usuario hace clic en el marcador *Iniciar NotePad* , se inicia NotePad.

>[!NOTE]
>
>Antes de leer esta sección, se recomienda familiarizarse con el ensamblado de documentos PDF mediante el servicio Ensamblador. En esta sección no se analizan conceptos como la creación de un objeto de colección que contenga documentos de entrada o el aprendizaje de cómo extraer los resultados del objeto de recopilación devuelto. (Consulte Compilación [programática de documentos]PDF (/help/forms/develop/programmaticamente-assembling-pdf-documents-programáticamente-ensamblar-pdf-documentos-programáticamente.md#programmatical-ensamblar-pdf-documentos).)

>[!NOTE]
>
>Para obtener más información sobre el servicio Compilador, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y Referencia](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Resumen de los pasos {#summary-of-steps}

Para montar un documento PDF que contenga marcadores, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de ensamblador de PDF.
1. Haga referencia a un documento DDX existente.
1. Haga referencia a un documento PDF al que se han agregado marcadores.
1. Haga referencia al documento XML de marcador.
1. Agregue el documento PDF y el documento XML de marcador a una colección Map.
1. Configure las opciones de tiempo de ejecución.
1. Monte el documento PDF.
1. Guarde el documento PDF que contiene marcadores.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms. Para obtener información sobre la ubicación de todos los archivos JAR de AEM Forms, consulte [Inclusión de archivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)de biblioteca Java de AEM Forms.

**Crear un cliente de ensamblador de PDF**

Antes de realizar una operación de ensamblador mediante programación, debe crear un cliente de servicio de ensamblador.

**Hacer referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para ensamblar un documento PDF. Este documento DDX debe contener el `Bookmarks` elemento , que indica al servicio Ensamblador que cree un PDF que contenga marcadores. (Consulte el documento DDX que se muestra anteriormente en esta sección para ver un ejemplo).

**Hacer referencia a un documento PDF al que se han agregado marcadores**

Haga referencia a un documento PDF al que se han agregado marcadores. No importa si el documento PDF al que se hace referencia ya contiene marcadores. Si el `Bookmarks` elemento es un elemento secundario del elemento de origen PDF, los marcadores reemplazarán a los que ya existen en el origen PDF. Sin embargo, si desea conservar los marcadores existentes, asegúrese de que `Bookmarks` sea un elemento del mismo nivel que el elemento de origen del PDF. Por ejemplo, consideremos el siguiente ejemplo:

```as3
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**Hacer referencia al documento XML de marcador**

Para compilar un PDF que contenga nuevos marcadores, debe hacer referencia a un documento XML de marcador. El documento XML de marcador se pasa al servicio Ensamblador dentro del objeto de colección Map. (Consulte el documento XML de marcador que se muestra anteriormente en esta sección para ver un ejemplo).

>[!NOTE]
>
>Consulte &quot;Lenguaje de marcadores&quot; en el servicio [Ensamblador y la referencia](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

**Agregar el documento PDF y el documento XML de marcador a una colección Map**

Debe agregar el documento PDF al que se han agregado marcadores y el documento XML de marcadores a la colección Map. Por lo tanto, el objeto de colección Map contiene dos elementos: un documento PDF y el documento XML con marcador.

**Definición de opciones de tiempo de ejecución**

Puede definir opciones en tiempo de ejecución que controlen el comportamiento del servicio de ensamblador mientras realiza un trabajo. Por ejemplo, puede definir una opción que indique al servicio Ensamblador que continúe procesando un trabajo si se produce un error. Para obtener información sobre las opciones de tiempo de ejecución que puede definir, consulte la referencia de la `AssemblerOptionSpec` clase en Referencia [de API de formularios](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM.

**Compilación del documento PDF**

Para montar un documento PDF que contenga nuevos marcadores, utilice la operación del servicio Ensamblador `invokeDDX` . El motivo por el que debe utilizar la operación en lugar de otras operaciones de servicio de Ensamblador, como `invokeDDX` `invokeOneDocument` es porque el servicio Ensamblador requiere un documento XML de marcador que se pasa dentro del objeto de colección Map. Este objeto es un parámetro de la `invokeDDX` operación.

**Guardar el documento PDF que contiene marcadores**

Debe extraer los resultados del objeto de mapa devuelto y guardar el documento PDF correspondiente. (Consulte &quot;Extraer los resultados&quot; en [Compilación programada de documentos](/help/forms/developing/programmatically-assembling-pdf-documents.md)PDF).

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Compilación de documentos PDF mediante programación](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Compilación de documentos PDF con marcadores mediante la API de Java {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Monte un documento PDF con marcadores mediante la API de servicio de ensamblador (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de ensamblador de PDF.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión. (Consulte [Configuración de propiedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexión).
   * Cree un `AssemblerServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un documento DDX existente.

   * Cree un `java.io.FileInputStream` objeto que represente el documento DDX utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo DDX.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Haga referencia a un documento PDF al que se han agregado marcadores.

   * Cree un `java.io.FileInputStream` objeto utilizando su constructor y pasando la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` objeto con su constructor y pase el `java.io.FileInputStream` objeto que contiene el documento PDF.

1. Haga referencia al documento XML de marcador.

   * Cree un `java.io.FileInputStream` objeto utilizando su constructor y pasando la ubicación del archivo XML que representa el documento XML de marcador.
   * Cree un `com.adobe.idp.Document` objeto y pase el `java.io.FileInputStream` objeto que contiene el documento PDF.

1. Agregue el documento PDF y el documento XML de marcador a una colección Map.

   * Cree un `java.util.Map` objeto que se utilice para almacenar el documento PDF de entrada y el documento XML de marcador.
   * Agregue el documento PDF de entrada invocando el `java.util.Map` método `put` del objeto y pasando los siguientes argumentos:

      * Un valor de cadena que representa el nombre de la clave. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX.
      * Un `com.adobe.idp.Document` objeto que contiene el documento PDF de entrada.
   * Agregue el documento XML de marcador invocando el `java.util.Map` método del `put` objeto y pasando los siguientes argumentos:

      * Un valor de cadena que representa el nombre de la clave. Este valor debe coincidir con el valor del elemento de origen Marcadores especificado en el documento DDX.
      * Un `com.adobe.idp.Document` objeto que contiene el documento XML de marcador.


1. Configure las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` objeto que almacene opciones de tiempo de ejecución mediante su constructor.
   * Configure las opciones de tiempo de ejecución para cumplir los requisitos comerciales invocando un método que pertenece al `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Ensamblador que continúe procesando un trabajo cuando se produzca un error, invoque el `AssemblerOptionSpec` método del `setFailOnError` objeto y pase `false`.

1. Monte el documento PDF.

   Invoque el `AssemblerServiceClient` método del `invokeDDX` objeto y pase los siguientes valores obligatorios:

   * Un `com.adobe.idp.Document` objeto que representa el documento DDX que se va a utilizar
   * Un `java.util.Map` objeto que contiene tanto el documento PDF de entrada como el documento XML de marcador.
   * Un `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica las opciones en tiempo de ejecución, incluidos el nivel predeterminado de fuente y registro de trabajos
   El `invokeDDX` método devuelve un `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contiene los resultados del trabajo y las excepciones que se hayan producido.

1. Guarde el documento PDF que contiene marcadores.

   Para obtener el documento PDF recién creado, realice las siguientes acciones:

   * Invocar el `AssemblerResult` método del `getDocuments` objeto. Esto devuelve un `java.util.Map` objeto.
   * Repita el `java.util.Map` objeto hasta que encuentre el `com.adobe.idp.Document` objeto resultante. (Puede utilizar el elemento de resultado PDF especificado en el documento DDX para obtener el documento).
   * Invocar el `com.adobe.idp.Document` método del `copyToFile` objeto para extraer el documento PDF.

**Consulte también**

[Inicio rápido (modo SOAP): Compilación de documentos PDF con marcadores mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Compilación de documentos PDF con marcadores mediante la API de servicio Web {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

Monte un documento PDF con marcadores mediante la API de servicio de ensamblador (servicio Web):

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
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.

1. Haga referencia a un documento PDF al que se han agregado marcadores.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar el PDF de entrada.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.

1. Haga referencia al documento XML de marcador.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar el documento XML con marcador.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.

1. Agregue el documento PDF y el documento XML de marcador a una colección Map.

   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Este objeto de colección se utiliza para almacenar los documentos PDF de entrada y el documento XML de marcador.
   * Para cada documento PDF de entrada y el documento XML de marcador, cree un `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Asigne un valor de cadena que represente el nombre clave al `MyMapOf_xsd_string_To_xsd_anyType_Item` campo del `key` objeto. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX.
   * Asigne el `BLOB` objeto que almacena el documento PDF al `MyMapOf_xsd_string_To_xsd_anyType_Item` campo del `value` objeto.
   * Agregue el `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto al `MyMapOf_xsd_string_To_xsd_anyType` objeto. Invoque el `MyMapOf_xsd_string_To_xsd_anyType` método del `Add` objeto y pase el `MyMapOf_xsd_string_To_xsd_anyType` objeto. (Realice esta tarea para cada documento PDF de entrada y el documento XML de marcador).

1. Configure las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` objeto que almacene opciones de tiempo de ejecución mediante su constructor.
   * Configure las opciones de tiempo de ejecución para cumplir los requisitos comerciales asignando un valor a un miembro de datos que pertenece al `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Ensamblador que continúe procesando un trabajo cuando se produzca un error, asigne `false` al miembro de datos del `AssemblerOptionSpec` objeto `failOnError` .

1. Monte el documento PDF.

   Invoque el `AssemblerServiceClient` método del `invokeDDX` objeto y pase los valores siguientes:

   * Un `BLOB` objeto que representa el documento DDX
   * La `MyMapOf_xsd_string_To_xsd_anyType` matriz que contiene los documentos de entrada
   * Un `AssemblerOptionSpec` objeto que especifica opciones de tiempo de ejecución
   El `invokeDDX` método devuelve un `AssemblerResult` objeto que contiene los resultados del trabajo y las excepciones que puedan haberse producido.

1. Guarde el documento PDF que contiene marcadores.

   Para obtener el documento PDF recién creado, realice las siguientes acciones:

   * Acceda al `AssemblerResult` campo del `documents` objeto, que es un `Map` objeto que contiene los documentos PDF resultantes.
   * Repita el `Map` objeto hasta que encuentre la clave que coincida con el nombre del documento resultante. A continuación, convierta los elementos del miembro `value` de la matriz en un `BLOB`.
   * Extraiga los datos binarios que representan el documento PDF accediendo al campo del `BLOB` objeto `MTOM` . Esto devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también**

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
