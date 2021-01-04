---
title: Compilación de Documentos PDF no interactivos
seo-title: Compilación de Documentos PDF no interactivos
description: Utilice un formulario PDF no interactivo como entrada para montar un documento PDF no interactivo mediante la API de Java y la API de servicio Web.
seo-description: Utilice un formulario PDF no interactivo como entrada para montar un documento PDF no interactivo mediante la API de Java y la API de servicio Web.
uuid: 0c7adeb4-9a3a-4ec5-ba33-c3642928d4ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8a75c201-bd88-4809-be08-69de94656489
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1800'
ht-degree: 0%

---


# Compilación de Documentos PDF no interactivos {#assembling-non-interactive-pdf-documents}

Puede montar un documento PDF no interactivo al utilizar un formulario PDF interactivo como entrada. Es decir, supongamos que tiene un formulario que los usuarios pueden utilizar para introducir datos en sus campos. Puede pasar ese formulario al servicio Ensamblador, lo que resulta en que el servicio Ensamblador devuelva un documento PDF que impide que los usuarios introduzcan datos en sus campos. Este documento es un formulario PDF no interactivo. Por ejemplo, la siguiente ilustración muestra una aplicación hipotecaria que representa un formulario interactivo.

A los efectos de este análisis, supongamos que se utiliza el siguiente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

Dentro de este documento DDX, observe que al atributo de origen se le asigna el valor `inDoc`. En situaciones en las que solo se pasa un documento PDF de entrada al servicio Ensamblador y se devuelve un documento PDF y se invoca la operación `invokeOneDocument`, asigne el valor `inDoc` al atributo de origen PDF. Al invocar la operación `invokeOneDocument`, el valor `inDoc` es una clave predefinida que debe especificarse en el documento DDX.

Por el contrario, al pasar dos o más documentos PDF de entrada al servicio Ensamblador, puede invocar la operación `invokeDDX`. En este caso, asigne el nombre de archivo del documento PDF de entrada al atributo `source`.

Este documento DDX contiene el elemento `NoXFA`, que indica al servicio Ensamblador que devuelva un documento PDF no interactivo.

El servicio Ensamblador puede montar documentos PDF no interactivos sin que el servicio Output forme parte de la instalación de formularios AEM si el documento PDF de entrada se basa en un formulario Acrobat o en un formulario XFA estático. Sin embargo, si el documento PDF de entrada es un formulario XFA dinámico, el servicio Output debe formar parte de la instalación de AEM formularios. Si el servicio Output no forma parte de la instalación de formularios AEM cuando se monta un formulario XFA dinámico, se genera una excepción. Consulte [Creación de flujos de salida de Documento](/help/forms/developing/creating-document-output-streams.md).

>[!NOTE]
>
>Antes de leer esta sección, se recomienda familiarizarse con el ensamblado de documentos PDF mediante el servicio Ensamblador. En esta sección no se analizan los conceptos, como la creación de un objeto de colección que contiene documentos de entrada o el aprendizaje de cómo extraer los resultados del objeto de colección devuelto. (Consulte [Compilación programada de Documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)).

>[!NOTE]
>
>Para obtener más información sobre el servicio de ensamblador, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y Referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

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
* adobe-utilities.jar (requerido si AEM Forms se implementa en JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms.

**Crear un cliente de ensamblado**

Antes de realizar una operación de ensamblador mediante programación, debe crear un cliente de servicio de ensamblador.

**Hacer referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para montar un documento PDF. Este documento DDX debe contener el elemento `NoXFA`, que indica al servicio Ensamblador que devuelva un documento PDF no interactivo.

**Referencia a un documento PDF interactivo**

Se debe hacer referencia a un documento PDF interactivo y pasarlo al servicio Ensamblador para recuperar un documento PDF no interactivo.

**Definición de opciones de tiempo de ejecución**

Puede definir opciones en tiempo de ejecución que controlen el comportamiento del servicio de ensamblador mientras realiza un trabajo. Por ejemplo, puede definir una opción que indique al servicio Ensamblador que continúe procesando un trabajo si se produce un error.

**Compilación del documento PDF**

Después de crear el cliente del servicio Ensamblador, hacer referencia al documento DDX, hacer referencia a un documento PDF interactivo y definir las opciones de tiempo de ejecución, puede invocar la operación `invokeOneDocument`. Dado que solo se pasa un documento PDF de entrada al servicio Ensamblador y se devuelve un solo documento, puede utilizar la operación `invokeOneDocument` en lugar de la operación `invokeDDX`.

**Guardar el documento PDF no interactivo**

Si solo se pasa un documento PDF al servicio Ensamblador, el servicio Ensamblador devuelve un solo documento en lugar de un objeto de colección. Es decir, al invocar la operación `invokeOneDocument`, se devuelve un solo documento. Dado que el documento DDX al que se hace referencia en esta sección contiene instrucciones para crear un documento PDF no interactivo, el servicio Ensamblador devuelve un documento PDF no interactivo que se puede guardar como archivo PDF.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Compilación programada de Documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Compilación de un documento PDF no interactivo mediante la API de Java {#assemble-a-non-interactive-pdf-document-using-the-java-api}

Monte un documento PDF no interactivo mediante la API de servicio de ensamblador (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de ensamblador.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `AssemblerServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Haga referencia a un documento DDX existente.

   * Cree un objeto `java.io.FileInputStream` que represente el documento DDX utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo DDX.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Haga referencia a un documento PDF interactivo.

   * Cree un objeto `java.io.FileInputStream` utilizando su constructor y pasando la ubicación de un documento PDF interactivo.
   * Cree un objeto `com.adobe.idp.Document` y pase el objeto `java.io.FileInputStream` que contiene el documento PDF. Este objeto `com.adobe.idp.Document` se pasa al método `invokeOneDocument`.

1. Configure las opciones de tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene las opciones de tiempo de ejecución mediante su constructor.
   * Configure las opciones de tiempo de ejecución para satisfacer los requisitos comerciales invocando un método que pertenece al objeto `AssemblerOptionSpec`. Por ejemplo, para indicar al servicio Ensamblador que continúe procesando un trabajo cuando se produzca un error, invoque el método `AssemblerOptionSpec` del objeto `setFailOnError` y pase `false`.

1. Monte el documento PDF.

   Invoque el método `AssemblerServiceClient` del objeto `invokeOneDocument` y pase los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que representa el documento DDX. Asegúrese de que este documento DDX contenga el valor `inDoc` para el elemento de origen PDF.
   * Un objeto `com.adobe.idp.Document` que contiene el documento PDF interactivo.
   * Un objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones en tiempo de ejecución, incluido el nivel predeterminado de fuente y registro de trabajos.

   El método `invokeOneDocument` devuelve un objeto `com.adobe.idp.Document` que contiene un documento PDF no interactivo.

1. Guarde el documento PDF no interactivo.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del nombre de archivo sea .pdf.
   * Invoque el método `Document` del objeto `copyToFile` para copiar el contenido del objeto `Document` en el archivo. Asegúrese de utilizar el objeto `Document` que devolvió el método `invokeOneDocument`.

* &quot;Inicio rápido (modo SOAP): Compilación de un documento PDF no interactivo mediante la API de Java&quot;

## Compilación de un documento PDF no interactivo mediante la API de servicio Web {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

Monte un documento PDF no interactivo mediante la API de servicio de ensamblador (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de ensamblador.

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
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento DDX y el modo en el que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read`. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Haga referencia a un documento PDF interactivo.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el documento PDF de entrada. Este objeto `BLOB` se pasa a `invokeOneDocument` como argumento.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF de entrada y el modo en el que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read`. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Configure las opciones de tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene las opciones de tiempo de ejecución mediante su constructor.
   * Configure las opciones de tiempo de ejecución para satisfacer los requisitos comerciales asignando un valor a un miembro de datos que pertenece al objeto `AssemblerOptionSpec`. Por ejemplo, para indicar al servicio Ensamblador que continúe procesando un trabajo cuando se produzca un error, asigne `false` al miembro de datos `AssemblerOptionSpec` del objeto `failOnError`.

1. Monte el documento PDF.

   Invoque el método `AssemblerServiceClient` del objeto `invokeOneDocument` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento DDX
   * Un objeto `BLOB` que representa el documento PDF interactivo
   * Un objeto `AssemblerOptionSpec` que especifica opciones de tiempo de ejecución

   El método `invokeOneDocument` devuelve un objeto `BLOB` que contiene un documento PDF no interactivo.

1. Guarde el documento PDF no interactivo.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF no interactivo y el modo en el que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` que el método `invokeOneDocument` devolvió. Rellene la matriz de bytes obteniendo el valor del campo `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

* &quot;Inicio rápido (MTOM): Compilación de un documento PDF no interactivo mediante la API de servicio web&quot;.

**Consulte también**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
