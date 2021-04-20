---
title: Validación de documentos DDX
seo-title: Validación de documentos DDX
description: Valide un documento DDX mediante programación utilizando la API de Java y la API de servicio web.
seo-description: Valide un documento DDX mediante programación utilizando la API de Java y la API de servicio web.
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 0%

---


# Validación de documentos DDX {#validating-ddx-documents}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

Puede validar mediante programación un documento DDX que utilice el servicio Assembler. Es decir, con la API de servicio de Assembler, puede determinar si un documento DDX es válido o no. Por ejemplo, si ha actualizado desde una versión anterior de AEM Forms y desea asegurarse de que el documento DDX sea válido, puede validarlo mediante la API de servicio de Assembler.

>[!NOTE]
>
>Para obtener más información sobre el servicio Assembler, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para validar un documento DDX, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente Assembler.
1. Haga referencia a un documento DDX existente.
1. Defina las opciones en tiempo de ejecución para validar el documento DDX.
1. Realice la validación.
1. Guarde los resultados de validación en un archivo de registro.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-Utilities.jar y jbossall-client.jar con archivos JAR específicos del servidor de aplicaciones J2EE en el que AEM Forms está implementado.

**Crear un cliente de ensamblador PDF**

Para poder realizar una operación Assembler mediante programación, debe crear un cliente de servicio Assembler.

**Referencia a un documento DDX existente**

Para validar un documento DDX, debe hacer referencia a un documento DDX existente.

**Establecer opciones de tiempo de ejecución para validar el documento DDX**

Al validar un documento DDX, debe establecer opciones específicas de tiempo de ejecución que indiquen al servicio Assembler que valide el documento DDX en lugar de ejecutarlo. Además, puede aumentar la cantidad de información que el servicio Assembler escribe en el archivo de registro.

**Realizar la validación**

Después de crear el cliente de servicio Assembler, hacer referencia al documento DDX y establecer las opciones de tiempo de ejecución, puede invocar la operación `invokeDDX` para validar el documento DDX. Al validar el documento DDX, puede pasar `null` como parámetro de asignación (este parámetro generalmente almacena documentos PDF que requiere el ensamblador para realizar las operaciones especificadas en el documento DDX).

Si la validación falla, se genera una excepción y el archivo de registro contiene detalles que explican por qué el documento DDX no es válido y se puede obtener desde la instancia `OperationException`. Una vez pasado el análisis XML básico y la comprobación de esquemas, se realiza la validación con la especificación DDX. Todos los errores que se encuentran en el documento DDX se especifican en el registro.

**Guardar los resultados de validación en un archivo de registro**

El servicio Assembler devuelve los resultados de validación que puede escribir en un archivo de registro XML. La cantidad de detalle que el servicio Assembler escribe en el archivo de registro depende de la opción de tiempo de ejecución que haya establecido.

**Consulte también**

[Validación de un documento DDX mediante la API de Java](#validate-a-ddx-document-using-the-java-api)

[Validación de un documento DDX mediante la API de servicio web](#validate-a-ddx-document-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montaje programático de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Validar un documento DDX utilizando la API de Java {#validate-a-ddx-document-using-the-java-api}

Valide un documento DDX utilizando la API del servicio Assembler (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-assembler-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente del ensamblador PDF.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `AssemblerServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Haga referencia a un documento DDX existente.

   * Cree un objeto `java.io.FileInputStream` que represente el documento DDX utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo DDX.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Defina las opciones en tiempo de ejecución para validar el documento DDX.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución empleando su constructor.
   * Establezca la opción en tiempo de ejecución que indica al servicio Assembler que valide el documento DDX invocando el método setValidateOnly del objeto `AssemblerOptionSpec` y pasando `true`.
   * Establezca la cantidad de información que el servicio Assembler escribe en el archivo de registro invocando el método `AssemblerOptionSpec` del objeto `getLogLevel` y pasando un valor de cadena que cumpla con sus necesidades. Al validar un documento DDX, desea que se escriba más información en el archivo de registro que ayudará en el proceso de validación. Como resultado, puede pasar el valor `FINE` o `FINER`.

1. Realice la validación.

   Invoque el método `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que representa el documento DDX.
   * El valor `null` del objeto java.io.Map que generalmente almacena documentos PDF.
   * Un objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones en tiempo de ejecución.

   El método `invokeDDX` devuelve un objeto `AssemblerResult` que contiene información que especifica si el documento DDX es válido.

1. Guarde los resultados de validación en un archivo de registro.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del nombre de archivo sea .xml.
   * Invoque el método `AssemblerResult` del objeto `getJobLog`. Este método devuelve una instancia `com.adobe.idp.Document` que contiene información de validación.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del objeto `com.adobe.idp.Document` en el archivo.

   >[!NOTE]
   >
   >Si el documento DDX no es válido, se genera un `OperationException`. Dentro de la sentencia catch, puede invocar el método `OperationException` del objeto `getJobLog` .

**Consulte también**

[Validación de documentos DDX](#validating-ddx-documents)

[Inicio rápido (modo SOAP): Validación de documentos DDX mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api)  (modo SOAP)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Validar un documento DDX utilizando la API de servicio web {#validate-a-ddx-document-using-the-web-service-api}

Valide un documento DDX utilizando la API del servicio Assembler (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace localhost por la dirección IP del servidor de formularios.

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
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Defina las opciones en tiempo de ejecución para validar el documento DDX.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución empleando su constructor.
   * Establezca la opción en tiempo de ejecución que indica al servicio Assembler que valide el documento DDX asignando el valor true al miembro de datos `AssemblerOptionSpec` del objeto `validateOnly`.
   * Establezca la cantidad de información que el servicio Assembler escribe en el archivo de registro asignando un valor de cadena al miembro de datos `AssemblerOptionSpec` del objeto `logLevel`. método Al validar un documento DDX, desea que se escriba más información en el archivo de registro que ayudará en el proceso de validación. Como resultado, puede especificar el valor `FINE` o `FINER`. Para obtener información sobre las opciones de tiempo de ejecución que puede establecer, consulte la referencia de clase `AssemblerOptionSpec` en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Realice la validación.

   Invoque el método `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento DDX.
   * El valor `null` del objeto `Map` que generalmente almacena documentos PDF.
   * Un objeto `AssemblerOptionSpec` que especifica opciones en tiempo de ejecución.

   El método `invokeDDX` devuelve un objeto `AssemblerResult` que contiene información que especifica si el documento DDX es válido.

1. Guarde los resultados de validación en un archivo de registro.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo de registro y el modo en que se abre el archivo. Asegúrese de que la extensión del nombre de archivo es .xml.
   * Cree un objeto `BLOB` que almacene información de registro obteniendo el valor del miembro de datos `AssemblerResult` del objeto `jobLog`.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB`. Rellene la matriz de bytes obteniendo el valor del campo `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

   >[!NOTE]
   >
   >Si el documento DDX no es válido, se genera un `OperationException`. Dentro de la sentencia catch, puede obtener el valor del miembro `OperationException` del objeto `jobLog`.

**Consulte también**

[Validación de documentos DDX](#validating-ddx-documents)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
