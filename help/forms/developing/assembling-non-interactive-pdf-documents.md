---
title: Agrupar documentos PDF no interactivos
seo-title: Assembling Non-Interactive PDF Documents
description: Utilice un formulario de PDF no interactivo como entrada para combinar un documento de PDF no interactivo mediante la API de Java y la API de servicio web.
seo-description: Use a non-interactive PDF form as input to assemble a non-interactive PDF document using the Java API and Web Service API.
uuid: 0c7adeb4-9a3a-4ec5-ba33-c3642928d4ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8a75c201-bd88-4809-be08-69de94656489
role: Developer
exl-id: 4677b9e5-3811-4de3-b4f4-9574b5898486
source-git-commit: 10227bcfcfd5a9b0f126fee74dce6ec7842f5e95
workflow-type: tm+mt
source-wordcount: '1775'
ht-degree: 0%

---

# Agrupar documentos PDF no interactivos {#assembling-non-interactive-pdf-documents}

Puede combinar un documento de PDF no interactivo al utilizar un formulario de PDF interactivo como entrada. Es decir, supongamos que tiene un formulario que los usuarios pueden utilizar para introducir datos en sus campos. Puede pasar ese formulario al servicio Assembler, lo que hace que el servicio Assembler devuelva un documento de PDF que impide que los usuarios introduzcan datos en sus campos. Este documento es un formulario de PDF no interactivo. Por ejemplo, la siguiente ilustración muestra una solicitud hipotecaria que representa un formulario interactivo.

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

Dentro de este documento DDX, observe que el atributo de origen tiene asignado el valor `inDoc`. En situaciones en las que solo se pasa un documento de PDF de entrada al servicio Assembler y se devuelve un documento de PDF, se invoca el `invokeOneDocument` operación, asignar el valor `inDoc` al atributo de origen del PDF. Al invocar el `invokeOneDocument` operación, el `inDoc` value es una clave predefinida que debe especificarse en el documento DDX.

Por el contrario, al pasar dos o más documentos del PDF de entrada al servicio Assembler, puede invocar el método `invokeDDX` operación. En este caso, asigne el nombre de archivo del documento del PDF de entrada al `source` atributo.

Este documento DDX contiene el `NoXFA` , que indica al servicio Assembler que devuelva un documento de PDF no interactivo.

El servicio Assembler puede ensamblar documentos de PDF AEM no interactivos sin que el servicio Output forme parte de la instalación de formularios de entrada si el documento de PDF de entrada se basa en un formulario de Acrobat o en un formulario XFA estático. Sin embargo, si el documento del PDF AEM de entrada es un formulario XFA dinámico, el servicio Output debe formar parte de la instalación de los formularios de. AEM Si el servicio Output no forma parte de la instalación de los formularios de cuando se monta un formulario XFA dinámico, se genera una excepción. Consulte [Crear flujos de salida de documento](/help/forms/developing/creating-document-output-streams.md).

>[!NOTE]
>
>Antes de leer esta sección, se recomienda que esté familiarizado con el ensamblado de documentos de PDF mediante el servicio Assembler. En esta sección no se tratan conceptos como, por ejemplo, la creación de un objeto de colección que contenga documentos de entrada o el aprendizaje de cómo extraer los resultados del objeto de colección devuelto. (Consulte [Agrupar documentos de PDF mediante programación](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Para obtener más información sobre el servicio Assembler, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para combinar un documento de PDF no interactivo, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDF Assembler.
1. Hacer referencia a un documento DDX existente.
1. Hacer referencia a un documento interactivo de PDF.
1. Establecer opciones en tiempo de ejecución.
1. Montar el documento del PDF.
1. Guarde el documento no interactivo del PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-utilities.jar y jbossall-client.jar con archivos JAR específicos del servidor de aplicaciones J2EE en el que AEM Forms está implementado.

**Crear un cliente de Assembler**

Para poder realizar mediante programación una operación de Assembler, debe crear un cliente de servicio Assembler.

**Hacer referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para combinar un documento de PDF. Este documento DDX debe contener la variable `NoXFA` , que indica al servicio Assembler que devuelva un documento de PDF no interactivo.

**Hacer referencia a un documento interactivo de PDF**

Se debe hacer referencia a un documento de PDF interactivo y pasarlo al servicio Assembler para recuperar un documento de PDF no interactivo.

**Establecer opciones en tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlen el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede establecer una opción que indique al servicio Assembler que continúe procesando un trabajo si se produce un error.

**Montar el documento de PDF**

Después de crear el cliente de servicio Assembler, hacer referencia al documento DDX, hacer referencia a un documento interactivo de PDF y establecer las opciones en tiempo de ejecución, puede invocar el `invokeOneDocument` operación. Dado que sólo se pasa un documento de PDF de entrada al servicio Assembler y se devuelve un único documento, puede utilizar el `invokeOneDocument` operación en lugar de la `invokeDDX` operación.

**Guarde el documento no interactivo del PDF**

Si se pasa un solo documento de PDF al servicio Assembler, el servicio Assembler devuelve un solo documento en lugar de un objeto de colección. Es decir, al invocar el `invokeOneDocument` operación, se devuelve un solo documento. Dado que el documento DDX al que se hace referencia en esta sección contiene instrucciones para crear un documento de PDF no interactivo, el servicio Assembler devuelve un documento de PDF no interactivo que se puede guardar como archivo de PDF.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Montar un documento de PDF no interactivo con la API de Java {#assemble-a-non-interactive-pdf-document-using-the-java-api}

Ensamble un documento de PDF no interactivo mediante la API del servicio del ensamblador (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de Assembler.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `AssemblerServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Hacer referencia a un documento DDX existente.

   * Crear un `java.io.FileInputStream` que representa el documento DDX utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo DDX.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Hacer referencia a un documento interactivo de PDF.

   * Crear un `java.io.FileInputStream` mediante su constructor y pasando la ubicación de un documento de PDF interactivo.
   * Crear un `com.adobe.idp.Document` y pase el `java.io.FileInputStream` que contiene el documento de PDF. Esta `com.adobe.idp.Document` El objeto se pasa a `invokeOneDocument` método.

1. Establecer opciones en tiempo de ejecución.

   * Crear un `AssemblerOptionSpec` que almacena las opciones en tiempo de ejecución mediante su constructor.
   * Establezca opciones en tiempo de ejecución para satisfacer sus necesidades empresariales invocando un método que pertenezca a `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, invoque el `AssemblerOptionSpec` del objeto `setFailOnError` método y pase `false`.

1. Montar el documento del PDF.

   Invoque el `AssemblerServiceClient` del objeto `invokeOneDocument` y pasar los siguientes valores:

   * A `com.adobe.idp.Document` que representa el documento DDX. Asegúrese de que este documento DDX contenga el valor `inDoc` para el elemento de origen PDF.
   * A `com.adobe.idp.Document` que contiene el documento interactivo del PDF.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones en tiempo de ejecución, incluida la fuente predeterminada y el nivel de registro de trabajo.

   El `invokeOneDocument` El método devuelve un valor `com.adobe.idp.Document` que contiene un documento de PDF no interactivo.

1. Guarde el documento no interactivo del PDF.

   * Crear un `java.io.File` y asegúrese de que la extensión del nombre de archivo es .pdf.
   * Invoque el `Document` del objeto `copyToFile` para copiar el contenido del `Document` al archivo. Asegúrese de utilizar el `Document` objetar que la `invokeOneDocument` método devuelto.

* &quot;Inicio rápido (modo SOAP): Combinar un documento de PDF no interactivo con la API de Java&quot;

## Montar un documento de PDF no interactivo mediante la API de servicio web {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

Ensamble un documento de PDF no interactivo mediante la API del servicio Assembler (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de Assembler.

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
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación de archivo del documento DDX y el modo para abrir el archivo en.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` método. Pase a leer la matriz de bytes, la posición inicial y la longitud de la secuencia.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.

1. Hacer referencia a un documento interactivo de PDF.

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar el documento del PDF de entrada. Esta `BLOB` El objeto se pasa a `invokeOneDocument` como argumento.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento del PDF de entrada y el modo para abrir el archivo en.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` método. Pase a leer la matriz de bytes, la posición inicial y la longitud de la secuencia.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.

1. Establecer opciones en tiempo de ejecución.

   * Crear un `AssemblerOptionSpec` que almacena las opciones en tiempo de ejecución mediante su constructor.
   * Establezca las opciones en tiempo de ejecución para satisfacer sus necesidades empresariales asignando un valor a un miembro de datos que pertenezca a `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne a `false` a la `AssemblerOptionSpec` del objeto `failOnError` miembro de datos.

1. Montar el documento del PDF.

   Invoque el `AssemblerServiceClient` del objeto `invokeOneDocument` y pasar los siguientes valores:

   * A `BLOB` que representa el documento DDX
   * A `BLOB` objeto que representa el documento interactivo del PDF
   * Un `AssemblerOptionSpec` objeto que especifica opciones en tiempo de ejecución

   El `invokeOneDocument` El método devuelve un valor `BLOB` que contiene un documento de PDF no interactivo.

1. Guarde el documento no interactivo del PDF.

   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento de PDF no interactivo y el modo para abrir el archivo en.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objetar que la `invokeOneDocument` método devuelto. Rellene la matriz de bytes obteniendo el valor de `BLOB` del objeto `MTOM` field.
   * Crear un `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

* &quot;Inicio rápido (MTOM): Combinar un documento de PDF no interactivo mediante la API de servicio web&quot;.

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
