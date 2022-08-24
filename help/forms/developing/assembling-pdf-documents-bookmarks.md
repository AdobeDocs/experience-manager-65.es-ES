---
title: Agrupación de documentos del PDF con marcadores
seo-title: Assembling PDF Documents with Bookmarks
description: Utilice el servicio Assembler para modificar un documento de PDF que contenga marcadores e incluir marcadores mediante la API de Java y la API del servicio Web.
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
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2558'
ht-degree: 0%

---

# Agrupación de documentos del PDF con marcadores {#assembling-pdf-documents-with-bookmarks}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

Puede ensamblar un documento PDF que contenga marcadores. Por ejemplo, supongamos que tiene un documento PDF que no contiene marcadores y que desea modificarlo proporcionando marcadores. Con el servicio Assembler, puede pasarle un documento PDF que no contenga marcadores y recuperar un documento PDF que contenga marcadores.

Los marcadores contienen las siguientes propiedades:

* Título que aparece como texto en la pantalla.
* Acción que especifica lo que sucede cuando un usuario hace clic en el marcador. La acción habitual de un marcador es moverse a otra ubicación del documento actual o abrir otro documento PDF, aunque se pueden especificar otras acciones.

A los efectos de esta discusión, supongamos que se utiliza el siguiente documento DDX.

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

Dentro de este documento DDX, observe que al atributo de origen se le asigna el valor `Loan.pdf`. Este documento DDX especifica que se pasa un solo documento PDF al servicio Assembler. Al ensamblar un documento de PDF con marcadores, debe especificar un documento XML de marcador que describa los marcadores en el documento de resultado. Para especificar un documento XML de marcador, asegúrese de que la variable `Bookmarks` se especifica en el documento DDX.

En este documento DDX de ejemplo, la variable `Bookmarks` element especifica `doc2` como valor. Este valor indica que el mapa de entrada pasado al servicio Assembler contiene una clave denominada `doc2`. El valor de la variable `doc2` la clave es un `com.adobe.idp.Document` que representa el documento XML de marcador. (Consulte &quot;Idioma de los marcadores&quot; en la sección [Servicio de ensamblador y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).)

En este tema se utiliza el siguiente lenguaje de marcadores XML para ensamblar un documento de PDF que contenga marcadores.

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

Dentro de este documento XML de marcador, observe el elemento Acción que define la acción que se realiza cuando un usuario hace clic en el marcador. En el elemento Acción (Action) se encuentra el elemento Iniciar que inicia aplicaciones, como NotePad y abre archivos, como archivos de PDF. Para abrir un archivo PDF, debe utilizar el elemento Archivo que especifica el archivo que se va a abrir. Por ejemplo, en el archivo XML de marcador especificado en esta sección, el nombre del archivo que se abre es LoanDetails.pdf.

>[!NOTE]
>
>Para obtener más información sobre las acciones admitidas, consulte &quot; `Action` &quot;&quot; en el [Servicio de ensamblador y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

Dado el documento DDX especificado en esta sección y el archivo XML de marcador como entrada, el servicio Assembler monta un documento PDF que contiene los siguientes marcadores.

![aw_aw_bmark](assets/aw_aw_bmark.png)

Cuando un usuario hace clic en la variable *Abrir los detalles del préstamo* marcador, se abre LoanDetails.pdf. Del mismo modo, cuando el usuario hace clic en la variable *Iniciar NotaPad* marcador, NotePad se ha iniciado.

>[!NOTE]
>
>Antes de leer esta sección, se recomienda que esté familiarizado con el ensamblaje de documentos PDF mediante el servicio Assembler. En esta sección no se tratan conceptos como la creación de un objeto de colección que contenga documentos de entrada o el aprendizaje de cómo extraer los resultados del objeto de colección devuelto. (Consulte [Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents).)

>[!NOTE]
>
>Para obtener más información sobre el servicio Assembler, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para ensamblar un documento de PDF que contenga marcadores, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de ensamblador de PDF.
1. Haga referencia a un documento DDX existente.
1. Haga referencia a un documento de PDF al que se agregarán marcadores.
1. Haga referencia al documento XML del marcador.
1. Agregue el documento del PDF y el documento XML del marcador a una colección Map.
1. Establezca las opciones de tiempo de ejecución.
1. Ensamble el documento del PDF.
1. Guarde el documento del PDF que contiene marcadores.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-Utilities.jar y jbossall-client.jar con archivos JAR específicos del servidor de aplicaciones J2EE en el que AEM Forms está implementado. Para obtener información sobre la ubicación de todos los archivos JAR de AEM Forms, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creación de un cliente de ensamblador de PDF**

Para poder realizar una operación Assembler mediante programación, debe crear un cliente de servicio Assembler.

**Referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para ensamblar un documento PDF. Este documento DDX debe contener la variable `Bookmarks` elemento, que indica al servicio Assembler que ensamble un PDF que contenga marcadores. (Consulte el documento DDX mostrado anteriormente en esta sección para ver un ejemplo).

**Hacer referencia a un documento del PDF al que se agregan marcadores**

Haga referencia a un documento de PDF al que se agregarán marcadores. No importa si el documento del PDF al que se hace referencia ya contiene marcadores. Si la variable `Bookmarks` es un elemento secundario del elemento de origen del PDF y, a continuación, los marcadores reemplazarán a los que ya existen en el origen del PDF. Sin embargo, si desea conservar los marcadores existentes, asegúrese de que `Bookmarks` es un elemento del mismo nivel del elemento de origen del PDF. Por ejemplo, veamos el siguiente ejemplo:

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**Referencia al documento XML de marcador**

Para ensamblar un PDF que contenga marcadores nuevos, debe hacer referencia a un documento XML de marcadores. El documento XML de marcador se pasa al servicio Assembler dentro del objeto de colección Map. (Consulte el documento XML de marcadores que se muestra anteriormente en esta sección para ver un ejemplo).

>[!NOTE]
>
>Consulte &quot;Idioma de los marcadores&quot; en la sección [Servicio de ensamblador y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

**Agregue el documento del PDF y el documento XML del marcador a una colección de mapas**

Debe agregar el documento del PDF al que se agregan marcadores y el documento XML del marcador a la colección Map . Por lo tanto, el objeto de colección Map contiene dos elementos: un documento de PDF y el documento XML de marcador.

**Establecer opciones de tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlan el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede definir una opción que indique al servicio Assembler que continúe procesando un trabajo si se encuentra un error. Para obtener información sobre las opciones de tiempo de ejecución que puede establecer, consulte la `AssemblerOptionSpec` referencia de clase en [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Montaje del documento del PDF**

Para ensamblar un documento de PDF que contenga marcadores nuevos, utilice el `invokeDDX` operación. El motivo por el que debe usar la variable `invokeDDX` operación a diferencia de otras operaciones de servicio del ensamblador como `invokeOneDocument` se debe a que el servicio Assembler requiere un documento XML de marcador que se pasa dentro del objeto de colección Map. Este objeto es un parámetro de la variable `invokeDDX` operación.

**Guarde el documento del PDF que contiene marcadores**

Debe extraer los resultados del objeto de asignación devuelto y guardar el documento de PDF correspondiente. (Consulte &quot;Extraer los resultados&quot; en [Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

**Consulte también lo siguiente**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Montaje de documentos del PDF con marcadores mediante la API de Java {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Ensamble un documento de PDF con marcadores mediante la API del servicio Assembler (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-assembler-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente de ensamblador de PDF.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión. (Consulte [Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Cree un `AssemblerServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un documento DDX existente.

   * Cree un `java.io.FileInputStream` objeto que representa el documento DDX utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo DDX.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Haga referencia a un documento de PDF al que se agregarán marcadores.

   * Cree un `java.io.FileInputStream` usando su constructor y pasando la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto que contiene el documento PDF.

1. Haga referencia al documento XML del marcador.

   * Cree un `java.io.FileInputStream` utilizando su constructor y pasando la ubicación del archivo XML que representa el documento XML de marcador.
   * Cree un `com.adobe.idp.Document` y pase el `java.io.FileInputStream` objeto que contiene el documento PDF.

1. Agregue el documento del PDF y el documento XML del marcador a una colección Map.

   * Cree un `java.util.Map` objeto que se utiliza para almacenar el documento del PDF de entrada y el documento XML del marcador.
   * Agregue el documento del PDF de entrada invocando la variable `java.util.Map` del objeto `put` y pasando los siguientes argumentos:

      * Un valor de cadena que representa el nombre de la clave. Este valor debe coincidir con el valor del elemento de origen del PDF especificado en el documento DDX.
      * A `com.adobe.idp.Document` objeto que contiene el documento del PDF de entrada.
   * Agregue el documento XML de marcador invocando la variable `java.util.Map` del objeto `put` y pasando los siguientes argumentos:

      * Un valor de cadena que representa el nombre de la clave. Este valor debe coincidir con el valor del elemento de origen Bookmarks especificado en el documento DDX.
      * A `com.adobe.idp.Document` objeto que contiene el documento XML de marcador.


1. Establezca las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` que almacena opciones en tiempo de ejecución mediante su constructor.
   * Configure las opciones en tiempo de ejecución para satisfacer los requisitos empresariales invocando un método que pertenece al `AssemblerOptionSpec` objeto. Por ejemplo, para solicitar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, invoque la función `AssemblerOptionSpec` del objeto `setFailOnError` método y pase `false`.

1. Ensamble el documento del PDF.

   Invocar el `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores obligatorios:

   * A `com.adobe.idp.Document` objeto que representa el documento DDX que se va a utilizar
   * A `java.util.Map` objeto que contiene el documento del PDF de entrada y el documento XML del marcador.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica las opciones de tiempo de ejecución, incluido el nivel predeterminado de fuente y registro de trabajo

   La variable `invokeDDX` el método devuelve un `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene los resultados del trabajo y cualquier excepción que se haya producido.

1. Guarde el documento del PDF que contiene marcadores.

   Para obtener el documento de PDF recién creado, realice las siguientes acciones:

   * Invocar el `AssemblerResult` del objeto `getDocuments` método. Esto devuelve un `java.util.Map` objeto.
   * Iterar a través de la variable `java.util.Map` hasta que encuentre el resultado `com.adobe.idp.Document` objeto. (Puede utilizar el elemento de resultado del PDF especificado en el documento DDX para obtener el documento).
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` método para extraer el documento PDF.

**Consulte también lo siguiente**

[Inicio rápido (modo SOAP): Agrupación de documentos del PDF con marcadores mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Montaje de documentos del PDF con marcadores mediante la API de servicio web {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

Ensamble un documento de PDF con marcadores mediante la API del servicio Assembler (servicio web):

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

1. Haga referencia a un documento de PDF al que se agregarán marcadores.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar el PDF de entrada.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento del PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Haga referencia al documento XML del marcador.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar el documento XML del marcador.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento del PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Agregue el documento del PDF y el documento XML del marcador a una colección Map.

   * Cree un `MyMapOf_xsd_string_To_xsd_anyType` objeto. Este objeto de colección se utiliza para almacenar los documentos del PDF de entrada y el documento XML del marcador.
   * Para cada documento del PDF de entrada y el documento XML del marcador , cree un `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Asigne un valor de cadena que represente el nombre de clave a la variable `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key` campo . Este valor debe coincidir con el valor del elemento de origen del PDF especificado en el documento DDX.
   * Asigne la variable `BLOB` objeto que almacena el documento del PDF en el `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value` campo .
   * Agregue la variable `MyMapOf_xsd_string_To_xsd_anyType_Item` al `MyMapOf_xsd_string_To_xsd_anyType` objeto. Invocar el `MyMapOf_xsd_string_To_xsd_anyType` del objeto `Add` y pase el `MyMapOf_xsd_string_To_xsd_anyType` objeto. (Realice esta tarea para cada documento del PDF de entrada y el documento XML del marcador).

1. Establezca las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` que almacena opciones en tiempo de ejecución mediante su constructor.
   * Configure las opciones en tiempo de ejecución para satisfacer los requisitos empresariales asignando un valor a un miembro de datos que pertenezca al grupo `AssemblerOptionSpec` objeto. Por ejemplo, para solicitar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne `false` a `AssemblerOptionSpec` del objeto `failOnError` miembro de datos.

1. Ensamble el documento del PDF.

   Invocar el `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores:

   * A `BLOB` objeto que representa el documento DDX
   * La variable `MyMapOf_xsd_string_To_xsd_anyType` matriz que contiene los documentos de entrada
   * Un `AssemblerOptionSpec` objeto que especifica opciones en tiempo de ejecución

   La variable `invokeDDX` devuelve un valor `AssemblerResult` objeto que contiene los resultados del trabajo y cualquier excepción que pueda haberse producido.

1. Guarde el documento del PDF que contiene marcadores.

   Para obtener el documento de PDF recién creado, realice las siguientes acciones:

   * Acceda a la `AssemblerResult` del objeto `documents` , que es un `Map` que contiene los documentos del PDF de resultados.
   * Iterar a través de la variable `Map` hasta que encuentre la clave que coincida con el nombre del documento resultante. A continuación, cree el `value` a `BLOB`.
   * Extraiga los datos binarios que representan el documento del PDF accediendo a su `BLOB` del objeto `MTOM` campo . Esto devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también lo siguiente**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
