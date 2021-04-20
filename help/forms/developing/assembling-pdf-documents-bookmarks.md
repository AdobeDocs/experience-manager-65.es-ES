---
title: Montaje de documentos PDF con marcadores
seo-title: Montaje de documentos PDF con marcadores
description: Utilice el servicio Assembler para modificar un documento PDF que contenga marcadores e incluir marcadores mediante la API de Java y la API del servicio Web.
seo-description: Utilice el servicio Assembler para modificar un documento PDF que contenga marcadores e incluir marcadores mediante la API de Java y la API del servicio Web.
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2589'
ht-degree: 0%

---


# Montaje de documentos PDF con marcadores {#assembling-pdf-documents-with-bookmarks}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

Puede ensamblar un documento PDF que contenga marcadores. Por ejemplo, supongamos que tiene un documento PDF que no contiene marcadores y desea modificarlo proporcionando marcadores. Con el servicio Assembler, puede pasarle un documento PDF que no contenga marcadores y recuperar un documento PDF que contenga marcadores.

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

Dentro de este documento DDX, observe que al atributo de origen se le asigna el valor `Loan.pdf`. Este documento DDX especifica que se pasa un solo documento PDF al servicio Assembler. Al ensamblar un documento PDF con marcadores, debe especificar un documento XML de marcador que describa los marcadores en el documento de resultado. Para especificar un documento XML de marcador, asegúrese de que el elemento `Bookmarks` está especificado en el documento DDX.

En este documento DDX de ejemplo, el elemento `Bookmarks` especifica `doc2` como valor. Este valor indica que el mapa de entrada pasado al servicio Assembler contiene una clave denominada `doc2`. El valor de la clave `doc2` es un valor `com.adobe.idp.Document` que representa el documento XML de marcador. (Consulte &quot;Idioma de marcadores&quot; en [Servicio de ensamblador y Referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63)).

En este tema se utiliza el siguiente lenguaje de marcadores XML para ensamblar un documento PDF que contenga marcadores.

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

Dentro de este documento XML de marcador, observe el elemento Acción que define la acción que se realiza cuando un usuario hace clic en el marcador. En el elemento Acción (Action) está el elemento Iniciar que inicia aplicaciones, como NotePad y abre archivos, como archivos PDF. Para abrir un archivo PDF, debe utilizar el elemento Archivo que especifica el archivo que se va a abrir. Por ejemplo, en el archivo XML de marcador especificado en esta sección, el nombre del archivo que se abre es LoanDetails.pdf.

>[!NOTE]
>
>Para obtener más información sobre las acciones admitidas, consulte &quot; `Action` elemento&quot; en [Servicio de ensamblador y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

Dado el documento DDX especificado en esta sección y el archivo XML de marcador como entrada, el servicio Assembler monta un documento PDF que contiene los siguientes marcadores.

![aw_aw_bmark](assets/aw_aw_bmark.png)

Cuando un usuario hace clic en el marcador *Open the Loan Details*, se abre LoanDetails.pdf. Del mismo modo, cuando el usuario hace clic en el marcador *Iniciar NotePad*, se inicia NotePad.

>[!NOTE]
>
>Antes de leer esta sección, se recomienda que esté familiarizado con el ensamblaje de documentos PDF mediante el servicio Assembler. En esta sección no se tratan conceptos como la creación de un objeto de colección que contenga documentos de entrada o el aprendizaje de cómo extraer los resultados del objeto de colección devuelto. (Consulte [Agrupación programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)).

>[!NOTE]
>
>Para obtener más información sobre el servicio Assembler, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para ensamblar un documento PDF que contenga marcadores, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente del ensamblador PDF.
1. Haga referencia a un documento DDX existente.
1. Haga referencia a un documento PDF al que se agregarán marcadores.
1. Haga referencia al documento XML del marcador.
1. Agregue el documento PDF y el documento XML de marcador a una colección Map.
1. Establezca las opciones de tiempo de ejecución.
1. Ensamble el documento PDF.
1. Guarde el documento PDF que contiene marcadores.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-Utilities.jar y jbossall-client.jar con archivos JAR específicos del servidor de aplicaciones J2EE en el que AEM Forms está implementado. Para obtener información sobre la ubicación de todos los archivos JAR de AEM Forms, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de ensamblador PDF**

Para poder realizar una operación Assembler mediante programación, debe crear un cliente de servicio Assembler.

**Referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para ensamblar un documento PDF. Este documento DDX debe contener el elemento `Bookmarks`, que ordena al servicio Assembler que ensamble un PDF que contenga marcadores. (Consulte el documento DDX mostrado anteriormente en esta sección para ver un ejemplo).

**Hacer referencia a un documento PDF al que se agregan marcadores**

Haga referencia a un documento PDF al que se agregarán marcadores. No importa si el documento PDF al que se hace referencia ya contenga marcadores. Si el elemento `Bookmarks` es un elemento secundario del elemento de origen PDF, los marcadores reemplazarán a los que ya existen en el origen PDF. Sin embargo, si desea conservar los marcadores existentes, asegúrese de que `Bookmarks` sea un elemento del mismo nivel del elemento de origen del PDF. Por ejemplo, veamos el siguiente ejemplo:

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
>Consulte &quot;Idioma de los marcadores&quot; en la [Referencia de Assembler Service y DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

**Agregue el documento PDF y el documento XML de marcador a una colección de mapas**

Debe agregar el documento PDF al que se agregan marcadores y el documento XML de marcadores a la colección Map. Por lo tanto, el objeto de colección Map contiene dos elementos: un documento PDF y el documento XML de marcador.

**Establecer opciones de tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlan el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede definir una opción que indique al servicio Assembler que continúe procesando un trabajo si se encuentra un error. Para obtener información sobre las opciones de tiempo de ejecución que puede establecer, consulte la referencia de clase `AssemblerOptionSpec` en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Montaje del documento PDF**

Para ensamblar un documento PDF que contenga marcadores nuevos, utilice la operación `invokeDDX` del servicio Assembler. El motivo por el que debe utilizar la operación `invokeDDX` en lugar de otras operaciones de servicio del ensamblador como `invokeOneDocument` es porque el servicio Assembler requiere un documento XML de marcador que se pasa dentro del objeto de colección Map. Este objeto es un parámetro de la operación `invokeDDX`.

**Guarde el documento PDF que contiene marcadores**

Debe extraer los resultados del objeto de asignación devuelto y guardar el documento PDF correspondiente. (Consulte &quot;Extraer los resultados&quot; en [Agrupación programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)).

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montaje programático de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Ensamble documentos PDF con marcadores usando la API de Java {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Ensamble un documento PDF con marcadores utilizando la API del servicio Assembler (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-assembler-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente del ensamblador PDF.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión. (Consulte [Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).
   * Cree un objeto `AssemblerServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Haga referencia a un documento DDX existente.

   * Cree un objeto `java.io.FileInputStream` que represente el documento DDX utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo DDX.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Haga referencia a un documento PDF al que se agregarán marcadores.

   * Cree un objeto `java.io.FileInputStream` utilizando su constructor y pasando la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pase el objeto `java.io.FileInputStream` que contiene el documento PDF.

1. Haga referencia al documento XML del marcador.

   * Cree un objeto `java.io.FileInputStream` utilizando su constructor y pasando la ubicación del archivo XML que representa el documento XML de marcador.
   * Cree un objeto `com.adobe.idp.Document` y pase el objeto `java.io.FileInputStream` que contiene el documento PDF.

1. Agregue el documento PDF y el documento XML de marcador a una colección Map.

   * Cree un objeto `java.util.Map` que se utilice para almacenar el documento PDF de entrada y el documento XML de marcador.
   * Agregue el documento PDF de entrada invocando el método `java.util.Map` del objeto `put` y pasando los siguientes argumentos:

      * Un valor de cadena que representa el nombre de la clave. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX.
      * Un objeto `com.adobe.idp.Document` que contiene el documento PDF de entrada.
   * Agregue el documento XML de marcador invocando el método `java.util.Map` del objeto `put` y pasando los siguientes argumentos:

      * Un valor de cadena que representa el nombre de la clave. Este valor debe coincidir con el valor del elemento de origen Bookmarks especificado en el documento DDX.
      * Un objeto `com.adobe.idp.Document` que contiene el documento XML de marcador.


1. Establezca las opciones de tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución empleando su constructor.
   * Defina las opciones en tiempo de ejecución para satisfacer los requisitos empresariales invocando un método que pertenece al objeto `AssemblerOptionSpec` . Por ejemplo, para solicitar al servicio Assembler que continúe procesando un trabajo cuando se produce un error, invoque el método `AssemblerOptionSpec` del objeto `setFailOnError` y pase `false`.

1. Ensamble el documento PDF.

   Invoque el método `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores obligatorios:

   * Un objeto `com.adobe.idp.Document` que representa el documento DDX que se va a utilizar
   * Un objeto `java.util.Map` que contiene el documento PDF de entrada y el documento XML de marcador.
   * Un objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones de tiempo de ejecución, incluidos el nivel predeterminado de fuente y registro de trabajo

   El método `invokeDDX` devuelve un objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene los resultados del trabajo y cualquier excepción que se haya producido.

1. Guarde el documento PDF que contiene marcadores.

   Para obtener el documento PDF recién creado, realice las siguientes acciones:

   * Invoque el método `AssemblerResult` del objeto `getDocuments`. Esto devuelve un objeto `java.util.Map`.
   * Repita el objeto `java.util.Map` hasta que encuentre el objeto `com.adobe.idp.Document` resultante. (Puede utilizar el elemento de resultado PDF especificado en el documento DDX para obtener el documento).
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para extraer el documento PDF.

**Consulte también**

[Inicio rápido (modo SOAP): Agrupación de documentos PDF con marcadores mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Ensamble documentos PDF con marcadores usando la API de servicio Web {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

Ensamble un documento PDF con marcadores utilizando la API del servicio Assembler (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente del ensamblador PDF.

   * Cree un objeto `AssemblerServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `AssemblerServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio.
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `AssemblerServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un documento DDX existente.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el documento DDX.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento DDX y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición de inicio y la longitud de flujo para leer.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Haga referencia a un documento PDF al que se agregarán marcadores.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el PDF de entrada.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición de inicio y la longitud de flujo para leer.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Haga referencia al documento XML del marcador.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el documento XML de marcador.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición de inicio y la longitud de flujo para leer.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Agregue el documento PDF y el documento XML de marcador a una colección Map.

   * Cree un objeto `MyMapOf_xsd_string_To_xsd_anyType`. Este objeto de colección se utiliza para almacenar los documentos PDF de entrada y el documento XML de marcador.
   * Para cada documento PDF de entrada y el documento XML de marcador , cree un objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` .
   * Asigne un valor de cadena que represente el nombre clave al campo `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key`. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX.
   * Asigne el objeto `BLOB` que almacena el documento PDF al campo `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value`.
   * Agregue el objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` al objeto `MyMapOf_xsd_string_To_xsd_anyType`. Invoque el método `MyMapOf_xsd_string_To_xsd_anyType` del objeto `Add` y pase el objeto `MyMapOf_xsd_string_To_xsd_anyType`. (Realice esta tarea para cada documento PDF de entrada y el documento XML de marcador).

1. Establezca las opciones de tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución empleando su constructor.
   * Defina las opciones en tiempo de ejecución para satisfacer los requisitos empresariales asignando un valor a un miembro de datos que pertenece al objeto `AssemblerOptionSpec`. Por ejemplo, para solicitar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne `false` al miembro de datos `AssemblerOptionSpec` del objeto `failOnError`.

1. Ensamble el documento PDF.

   Invoque el método `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento DDX
   * La matriz `MyMapOf_xsd_string_To_xsd_anyType` que contiene los documentos de entrada
   * Un objeto `AssemblerOptionSpec` que especifica opciones en tiempo de ejecución

   El método `invokeDDX` devuelve un objeto `AssemblerResult` que contiene los resultados del trabajo y cualquier excepción que pueda haberse producido.

1. Guarde el documento PDF que contiene marcadores.

   Para obtener el documento PDF recién creado, realice las siguientes acciones:

   * Acceda al campo `AssemblerResult` del objeto `documents`, que es un objeto `Map` que contiene los documentos PDF resultantes.
   * Repita el objeto `Map` hasta que encuentre la clave que coincida con el nombre del documento resultante. A continuación, convierta el `value` del miembro de la matriz en un `BLOB`.
   * Extraiga los datos binarios que representan el documento PDF accediendo al campo `BLOB` del objeto `MTOM`. Esto devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
