---
title: Validar documentos DDX
description: Valide un documento DDX mediante programación utilizando la API de Java y la API de servicio web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 1f5a2cf3-ef6b-45b4-8fa8-b300e492fee1
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1507'
ht-degree: 2%

---

# Validar documentos DDX {#validating-ddx-documents}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

Puede validar mediante programación un documento DDX que utilice el servicio Assembler. Es decir, mediante la API del servicio Assembler, puede determinar si un documento DDX es válido o no. Por ejemplo, si ha actualizado desde una versión anterior de AEM Forms y desea asegurarse de que el documento DDX sea válido, puede validarlo mediante la API del servicio Assembler.

>[!NOTE]
>
>Para obtener más información sobre el servicio Assembler, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para validar un documento DDX, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de Assembler.
1. Hacer referencia a un documento DDX existente.
1. Establezca las opciones en tiempo de ejecución para validar el documento DDX.
1. Realice la validación.
1. Guarde los resultados de validación en un archivo de registro.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-utilities.jar y jbossall-client.jar con archivos JAR específicos del servidor de aplicaciones J2EE en el que AEM Forms está implementado.

**Crear un cliente de PDF Assembler**

Para poder realizar mediante programación una operación de Assembler, debe crear un cliente de servicio Assembler.

**Hacer referencia a un documento DDX existente**

Para validar un documento DDX, debe hacer referencia a un documento DDX existente.

**Establecer opciones en tiempo de ejecución para validar el documento DDX**

Al validar un documento DDX, debe establecer opciones específicas en tiempo de ejecución que indiquen al servicio Assembler que valide el documento DDX en lugar de ejecutarlo. Además, puede aumentar la cantidad de información que el servicio Assembler escribe en el archivo de registro.

**Realice la validación**

Después de crear el cliente de servicio Assembler, hacer referencia al documento DDX y establecer las opciones en tiempo de ejecución, puede invocar el `invokeDDX` para validar el documento DDX. Al validar el documento DDX, puede pasar `null` como parámetro de asignación (este parámetro generalmente almacena los documentos de PDF que el ensamblador necesita para realizar las operaciones especificadas en el documento DDX).

Si la validación falla, se inicia una excepción y el archivo de registro contiene detalles que explican por qué el documento DDX no es válido y se pueden obtener de `OperationException` ejemplo. Una vez pasado el análisis XML básico y la comprobación de esquema, se realiza la validación con respecto a la especificación DDX. Todos los errores que se encuentran en el documento DDX se especifican en el registro.

**Guardar los resultados de validación en un archivo de registro**

El servicio Assembler devuelve los resultados de validación que se pueden escribir en un archivo de registro XML. La cantidad de detalles que el servicio Assembler escribe en el archivo de registro depende de la opción de tiempo de ejecución que se establezca.

**Consulte también**

[Validar un documento DDX mediante la API de Java](#validate-a-ddx-document-using-the-java-api)

[Validar un documento DDX mediante la API de servicio web](#validate-a-ddx-document-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Validar un documento DDX mediante la API de Java {#validate-a-ddx-document-using-the-java-api}

Valide un documento DDX mediante la API del servicio Assembler (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de PDF Assembler.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `AssemblerServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Hacer referencia a un documento DDX existente.

   * Crear un `java.io.FileInputStream` que representa el documento DDX utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo DDX.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Establezca las opciones en tiempo de ejecución para validar el documento DDX.

   * Crear un `AssemblerOptionSpec` que almacena las opciones en tiempo de ejecución mediante su constructor.
   * Establezca la opción en tiempo de ejecución que indica al servicio Assembler que valide el documento DDX invocando el `AssemblerOptionSpec` método setValidateOnly del objeto y pasar `true`.
   * Establezca la cantidad de información que el servicio Assembler escribe en el archivo de registro invocando el método `AssemblerOptionSpec` del objeto `getLogLevel` y pasar un valor de cadena cumple con sus requisitos. Al validar un documento DDX, desea escribir más información en el archivo de registro que ayude en el proceso de validación. Como resultado, puede pasar el valor `FINE` o `FINER`.

1. Realice la validación.

   Invoque el `AssemblerServiceClient` del objeto `invokeDDX` y pasar los siguientes valores:

   * A `com.adobe.idp.Document` que representa el documento DDX.
   * El valor `null` para el objeto java.io.Map que generalmente almacena documentos de PDF.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones en tiempo de ejecución.

   El `invokeDDX` El método devuelve un `AssemblerResult` que contiene información que especifica si el documento DDX es válido.

1. Guarde los resultados de validación en un archivo de registro.

   * Crear un `java.io.File` y asegúrese de que la extensión del nombre de archivo es .xml.
   * Invoque el `AssemblerResult` del objeto `getJobLog` método. Este método devuelve un `com.adobe.idp.Document` que contiene información de validación.
   * Invoque el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `com.adobe.idp.Document` al archivo.

   >[!NOTE]
   >
   >Si el documento DDX no es válido, un `OperationException` se ha lanzado. Dentro de la instrucción catch, puede invocar el método `OperationException` del objeto `getJobLog` método.

**Consulte también**

[Validar documentos DDX](#validating-ddx-documents)

[Inicio rápido (modo SOAP): Validación de documentos DDX mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) (modo SOAP)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Validar un documento DDX mediante la API de servicio web {#validate-a-ddx-document-using-the-web-service-api}

Valide un documento DDX mediante la API del servicio Assembler (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace localhost por la dirección IP del servidor de Forms.

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
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación de archivo del documento DDX y el modo para abrir el archivo en.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.

1. Establezca las opciones en tiempo de ejecución para validar el documento DDX.

   * Crear un `AssemblerOptionSpec` que almacena las opciones en tiempo de ejecución mediante su constructor.
   * Establezca la opción en tiempo de ejecución que indica al servicio Assembler que valide el documento DDX asignando el valor true a `AssemblerOptionSpec` del objeto `validateOnly` miembro de datos.
   * Establezca la cantidad de información que el servicio Assembler escribe en el archivo de registro asignando un valor de cadena al `AssemblerOptionSpec` del objeto `logLevel` miembro de datos. método Al validar un documento DDX, desea obtener más información escrita en el archivo de registro que le ayudará en el proceso de validación. Como resultado, puede especificar el valor `FINE` o `FINER`. Para obtener información acerca de las opciones en tiempo de ejecución que puede establecer, vea la `AssemblerOptionSpec` referencia de clase en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Realice la validación.

   Invoque el `AssemblerServiceClient` del objeto `invokeDDX` y pasar los siguientes valores:

   * A `BLOB` que representa el documento DDX.
   * El valor `null` para el `Map` que generalmente almacena documentos de PDF.
   * Un `AssemblerOptionSpec` que especifica las opciones en tiempo de ejecución.

   El `invokeDDX` El método devuelve un `AssemblerResult` que contiene información que especifica si el documento DDX es válido.

1. Guarde los resultados de validación en un archivo de registro.

   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo de registro y el modo para abrir el archivo en. Asegúrese de que la extensión del nombre de archivo sea .xml.
   * Crear un `BLOB` que almacena información de registro obteniendo el valor del objeto `AssemblerResult` del objeto `jobLog` miembro de datos.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto. Rellene la matriz de bytes obteniendo el valor de `BLOB` del objeto `MTOM` field.
   * Crear un `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

   >[!NOTE]
   >
   >Si el documento DDX no es válido, un `OperationException` se ha lanzado. Dentro de la instrucción catch, puede obtener el valor de `OperationException` del objeto `jobLog` miembro.

**Consulte también**

[Validar documentos DDX](#validating-ddx-documents)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
