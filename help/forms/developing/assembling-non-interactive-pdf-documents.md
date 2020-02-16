---
title: Compilación de documentos PDF no interactivos
seo-title: Compilación de documentos PDF no interactivos
description: nulo
seo-description: nulo
uuid: 0c7adeb4-9a3a-4ec5-ba33-c3642928d4ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8a75c201-bd88-4809-be08-69de94656489
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Compilación de documentos PDF no interactivos {#assembling-non-interactive-pdf-documents}

Puede montar un documento PDF no interactivo al utilizar un formulario PDF interactivo como entrada. Es decir, supongamos que tiene un formulario que los usuarios pueden utilizar para introducir datos en sus campos. Puede pasar ese formulario al servicio Ensamblador, lo que resulta en que el servicio Ensamblador devuelva un documento PDF que impide que los usuarios introduzcan datos en sus campos. Este documento es un formulario PDF no interactivo. Por ejemplo, la siguiente ilustración muestra una aplicación hipotecaria que representa un formulario interactivo.

A los efectos de este análisis, supongamos que se utiliza el siguiente documento DDX.

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

En este documento DDX, observe que el atributo de origen está asignado al valor `inDoc`. En situaciones en las que solo se pasa un documento PDF de entrada al servicio Compilador y se devuelve un documento PDF, y se invoca la `invokeOneDocument` operación, asigne el valor `inDoc` al atributo de origen PDF. Al invocar la `invokeOneDocument` operación, el `inDoc` valor es una clave predefinida que debe especificarse en el documento DDX.

Por el contrario, al pasar dos o más documentos PDF de entrada al servicio Ensamblador, puede invocar la `invokeDDX` operación. En este caso, asigne el nombre de archivo del documento PDF de entrada al `source` atributo.

Este documento DDX contiene el `NoXFA` elemento , que indica al servicio Ensamblador que devuelva un documento PDF no interactivo.

El servicio Ensamblador puede montar documentos PDF no interactivos sin que el servicio Output forme parte de la instalación de formularios AEM si el documento PDF de entrada se basa en un formulario de Acrobat o en un formulario XFA estático. Sin embargo, si el documento PDF de entrada es un formulario XFA dinámico, el servicio Output debe formar parte de la instalación de formularios AEM. Si el servicio Output no forma parte de la instalación de formularios AEM cuando se monta un formulario XFA dinámico, se genera una excepción. Consulte [Creación de flujos](/help/forms/developing/creating-document-output-streams.md)de salida de documento.

>[!NOTE]
>
>Antes de leer esta sección, se recomienda familiarizarse con el ensamblado de documentos PDF mediante el servicio Ensamblador. En esta sección no se analizan conceptos como la creación de un objeto de colección que contenga documentos de entrada o el aprendizaje de cómo extraer los resultados del objeto de recopilación devuelto. (Consulte Compilación [programada de documentos](/help/forms/developing/programmatically-assembling-pdf-documents.md)PDF).

>[!NOTE]
>
>Para obtener más información sobre el servicio Compilador, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y Referencia](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Resumen de los pasos {#summary-of-steps}

Para montar un documento PDF no interactivo, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de ensamblador de PDF.
1. Haga referencia a un documento DDX existente.
1. Haga referencia a un documento PDF interactivo.
1. Configure las opciones de tiempo de ejecución.
1. Monte el documento PDF.
1. Guarde el documento PDF no interactivo.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms.

**Crear un cliente de ensamblado**

Antes de realizar una operación de ensamblador mediante programación, debe crear un cliente de servicio de ensamblador.

**Hacer referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para ensamblar un documento PDF. Este documento DDX debe contener el `NoXFA` elemento , que indica al servicio Ensamblador que devuelva un documento PDF no interactivo.

**Hacer referencia a un documento PDF interactivo**

Se debe hacer referencia a un documento PDF interactivo y pasarlo al servicio Ensamblador para recuperar un documento PDF no interactivo.

**Definición de opciones de tiempo de ejecución**

Puede definir opciones en tiempo de ejecución que controlen el comportamiento del servicio de ensamblador mientras realiza un trabajo. Por ejemplo, puede definir una opción que indique al servicio Ensamblador que continúe procesando un trabajo si se produce un error.

**Compilación del documento PDF**

Después de crear el cliente del servicio Ensamblador, hacer referencia al documento DDX, hacer referencia a un documento PDF interactivo y definir las opciones de tiempo de ejecución, puede invocar la `invokeOneDocument` operación. Dado que solo se pasa un documento PDF de entrada al servicio de ensamblador y se devuelve un solo documento, puede utilizar la `invokeOneDocument` operación en lugar de la `invokeDDX` operación.

**Guardar el documento PDF no interactivo**

Si solo se pasa un documento PDF al servicio Ensamblador, el servicio Ensamblador devuelve un único documento en lugar de un objeto de colección. Es decir, al invocar la operación, se devuelve un solo documento `invokeOneDocument` . Dado que el documento DDX al que se hace referencia en esta sección contiene instrucciones para crear un documento PDF no interactivo, el servicio Ensamblador devuelve un documento PDF no interactivo que se puede guardar como archivo PDF.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Compilación de documentos PDF mediante programación](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Compilación de un documento PDF no interactivo mediante la API de Java {#assemble-a-non-interactive-pdf-document-using-the-java-api}

Monte un documento PDF no interactivo mediante la API de servicio de ensamblador (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de ensamblador.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `AssemblerServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un documento DDX existente.

   * Cree un `java.io.FileInputStream` objeto que represente el documento DDX utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo DDX.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Haga referencia a un documento PDF interactivo.

   * Cree un `java.io.FileInputStream` objeto utilizando su constructor y pasando la ubicación de un documento PDF interactivo.
   * Cree un `com.adobe.idp.Document` objeto y pase el `java.io.FileInputStream` objeto que contiene el documento PDF. Este `com.adobe.idp.Document` objeto se pasa al `invokeOneDocument` método .

1. Configure las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` objeto que almacene opciones de tiempo de ejecución mediante su constructor.
   * Configure las opciones de tiempo de ejecución para cumplir los requisitos comerciales invocando un método que pertenece al `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Ensamblador que continúe procesando un trabajo cuando se produzca un error, invoque el `AssemblerOptionSpec` método del `setFailOnError` objeto y pase `false`.

1. Monte el documento PDF.

   Invoque el `AssemblerServiceClient` método del `invokeOneDocument` objeto y pase los valores siguientes:

   * Un `com.adobe.idp.Document` objeto que representa el documento DDX. Asegúrese de que este documento DDX contenga el valor `inDoc` del elemento de origen PDF.
   * Un `com.adobe.idp.Document` objeto que contiene el documento PDF interactivo.
   * Un `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica las opciones en tiempo de ejecución, incluidos el nivel predeterminado de fuente y registro de trabajos.
   El `invokeOneDocument` método devuelve un `com.adobe.idp.Document` objeto que contiene un documento PDF no interactivo.

1. Guarde el documento PDF no interactivo.

   * Cree un `java.io.File` objeto y asegúrese de que la extensión del nombre de archivo sea .pdf.
   * Invocar el `Document` método del `copyToFile` objeto para copiar el contenido del `Document` objeto en el archivo. Asegúrese de utilizar el `Document` objeto que devolvió el `invokeOneDocument` método.

* &quot;Inicio rápido (modo SOAP): Compilación de un documento PDF no interactivo mediante la API de Java&quot;

## Compilación de un documento PDF no interactivo mediante la API de servicio Web {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

Monte un documento PDF no interactivo mediante la API de servicio de ensamblador (servicio Web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de ensamblador.

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
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento DDX y el modo en el que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.

1. Haga referencia a un documento PDF interactivo.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar el documento PDF de entrada. Este `BLOB` objeto se pasa al `invokeOneDocument` como argumento.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF de entrada y el modo en el que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.

1. Configure las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` objeto que almacene opciones de tiempo de ejecución mediante su constructor.
   * Configure las opciones de tiempo de ejecución para cumplir los requisitos comerciales asignando un valor a un miembro de datos que pertenece al `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Ensamblador que continúe procesando un trabajo cuando se produzca un error, asigne `false` al miembro de datos del `AssemblerOptionSpec` objeto `failOnError` .

1. Monte el documento PDF.

   Invoque el `AssemblerServiceClient` método del `invokeOneDocument` objeto y pase los valores siguientes:

   * Un `BLOB` objeto que representa el documento DDX
   * Un `BLOB` objeto que representa el documento PDF interactivo
   * Un `AssemblerOptionSpec` objeto que especifica opciones de tiempo de ejecución
   El `invokeOneDocument` método devuelve un `BLOB` objeto que contiene un documento PDF no interactivo.

1. Guarde el documento PDF no interactivo.

   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF no interactivo y el modo en el que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto devuelto por el `invokeOneDocument` método. Rellene la matriz de bytes obteniendo el valor del `BLOB` campo del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el `System.IO.BinaryWriter` método `Write` del objeto y pasando la matriz de bytes.

* &quot;Inicio rápido (MTOM): Compilación de un documento PDF no interactivo mediante la API de servicio web&quot;.

**Consulte también**

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
