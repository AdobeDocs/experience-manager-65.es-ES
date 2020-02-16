---
title: Validación de documentos DDX
seo-title: Validación de documentos DDX
description: nulo
seo-description: nulo
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Validación de documentos DDX {#validating-ddx-documents}

Puede validar mediante programación un documento DDX que utilice el servicio Ensamblador. Es decir, con la API de servicio de ensamblador, puede determinar si un documento DDX es válido o no. Por ejemplo, si ha actualizado desde una versión anterior de AEM Forms y desea asegurarse de que el documento DDX es válido, puede validarlo con la API de servicio de ensamblador.

>[!NOTE]
>
>Para obtener más información sobre el servicio Compilador, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y Referencia](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Resumen de los pasos {#summary-of-steps}

Para validar un documento DDX, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de ensamblador.
1. Haga referencia a un documento DDX existente.
1. Configure las opciones de tiempo de ejecución para validar el documento DDX.
1. Realice la validación.
1. Guarde los resultados de validación en un archivo de registro.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms.

**Crear un cliente de ensamblador de PDF**

Antes de realizar una operación de ensamblador mediante programación, debe crear un cliente de servicio de ensamblador.

**Hacer referencia a un documento DDX existente**

Para validar un documento DDX, debe hacer referencia a un documento DDX existente.

**Configure las opciones de tiempo de ejecución para validar el documento DDX**

Al validar un documento DDX, debe definir opciones específicas de tiempo de ejecución que indiquen al servicio Ensamblador que valide el documento DDX en lugar de ejecutarlo. Además, puede aumentar la cantidad de información que el servicio del ensamblador escribe en el archivo de registro.

**Realizar la validación**

Después de crear el cliente del servicio Ensamblador, hacer referencia al documento DDX y definir las opciones de tiempo de ejecución, puede invocar la `invokeDDX` operación para validar el documento DDX. Al validar el documento DDX, puede pasar `null` como parámetro de mapa (este parámetro generalmente almacena documentos PDF que el ensamblador necesita para realizar las operaciones especificadas en el documento DDX).

Si la validación falla, se genera una excepción y el archivo de registro contiene detalles que explican por qué el documento DDX no es válido se puede obtener de la `OperationException` instancia. Una vez pasado el análisis XML básico y la comprobación de esquema, se realiza la validación con respecto a la especificación DDX. Todos los errores que se encuentran en el documento DDX se especifican en el registro.

**Guardar los resultados de validación en un archivo de registro**

El servicio Ensamblador devuelve los resultados de validación que puede escribir en un archivo de registro XML. La cantidad de detalles que el servicio del ensamblador escribe en el archivo de registro depende de la opción de tiempo de ejecución que configure.

**Consulte también**

[Validación de un documento DDX mediante la API de Java](#validate-a-ddx-document-using-the-java-api)

[Validación de un documento DDX mediante la API de servicio Web](#validate-a-ddx-document-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Compilación de documentos PDF mediante programación](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Validación de un documento DDX mediante la API de Java {#validate-a-ddx-document-using-the-java-api}

Valide un documento DDX mediante la API de servicio de ensamblador (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de ensamblador de PDF.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `AssemblerServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un documento DDX existente.

   * Cree un `java.io.FileInputStream` objeto que represente el documento DDX utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo DDX.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Configure las opciones de tiempo de ejecución para validar el documento DDX.

   * Cree un `AssemblerOptionSpec` objeto que almacene opciones de tiempo de ejecución mediante su constructor.
   * Establezca la opción de tiempo de ejecución que indica al servicio Ensamblador que valide el documento DDX invocando el método setValidateOnly del `AssemblerOptionSpec` objeto y pasando `true`.
   * Configure la cantidad de información que el servicio Ensamblador escribe en el archivo de registro invocando el `AssemblerOptionSpec` método del `getLogLevel` objeto y pasando un valor de cadena que cumpla con sus requisitos. Al validar un documento DDX, desea que se escriba más información en el archivo de registro que le ayudará en el proceso de validación. Como resultado, puede pasar el valor `FINE` o `FINER`.

1. Realice la validación.

   Invoque el `AssemblerServiceClient` método del `invokeDDX` objeto y pase los valores siguientes:

   * Un `com.adobe.idp.Document` objeto que representa el documento DDX.
   * El valor `null` del objeto java.io.Map que generalmente almacena documentos PDF.
   * Un `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica las opciones de tiempo de ejecución.
   El `invokeDDX` método devuelve un `AssemblerResult` objeto que contiene información que especifica si el documento DDX es válido.

1. Guarde los resultados de validación en un archivo de registro.

   * Cree un `java.io.File` objeto y asegúrese de que la extensión del nombre de archivo sea .xml.
   * Invocar el `AssemblerResult` método del `getJobLog` objeto. Este método devuelve una `com.adobe.idp.Document` instancia que contiene información de validación.
   * Invocar el `com.adobe.idp.Document` método del `copyToFile` objeto para copiar el contenido del `com.adobe.idp.Document` objeto en el archivo.
   >[!NOTE]
   >
   >Si el documento DDX no es válido, se `OperationException` genera un error. En la sentencia catch, puede invocar el `OperationException` método del `getJobLog` objeto.

**Consulte también**

[Validación de documentos DDX](#validating-ddx-documents)

[Inicio rápido (modo SOAP): Validación de documentos DDX mediante la API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) de Java (modo SOAP)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Validación de un documento DDX mediante la API de servicio Web {#validate-a-ddx-document-using-the-web-service-api}

Valide un documento DDX mediante la API de servicio de ensamblador (servicio Web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar localhost con la dirección IP del servidor de formularios.

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
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento DDX y el modo en el que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` propiedad con el contenido de la matriz de bytes.

1. Configure las opciones de tiempo de ejecución para validar el documento DDX.

   * Cree un `AssemblerOptionSpec` objeto que almacene opciones de tiempo de ejecución mediante su constructor.
   * Defina la opción de tiempo de ejecución que indica al servicio Ensamblador que valide el documento DDX asignando el valor true al miembro de `AssemblerOptionSpec` datos del `validateOnly` objeto.
   * Configure la cantidad de información que el servicio Ensamblador escribe en el archivo de registro asignando un valor de cadena al miembro de `AssemblerOptionSpec` datos del `logLevel` objeto. al validar un documento DDX, desea que se escriba más información en el archivo de registro que le ayudará en el proceso de validación. Como resultado, puede especificar el valor `FINE` o `FINER`. Para obtener información sobre las opciones de tiempo de ejecución que puede definir, consulte la referencia de la `AssemblerOptionSpec` clase en Referencia [de API de formularios](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM.

1. Realice la validación.

   Invoque el `AssemblerServiceClient` método del `invokeDDX` objeto y pase los valores siguientes:

   * Un `BLOB` objeto que representa el documento DDX.
   * Valor `null` del `Map` objeto que normalmente almacena documentos PDF.
   * Un `AssemblerOptionSpec` objeto que especifica opciones de tiempo de ejecución.
   El `invokeDDX` método devuelve un `AssemblerResult` objeto que contiene información que especifica si el documento DDX es válido.

1. Guarde los resultados de validación en un archivo de registro.

   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo de registro y el modo en el que se abre el archivo. Asegúrese de que la extensión del nombre de archivo sea .xml.
   * Cree un `BLOB` objeto que almacene información de registro obteniendo el valor del miembro de datos del `AssemblerResult` objeto `jobLog` .
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto. Rellene la matriz de bytes obteniendo el valor del `BLOB` campo del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el `System.IO.BinaryWriter` método `Write` del objeto y pasando la matriz de bytes.
   >[!NOTE]
   >
   >Si el documento DDX no es válido, se `OperationException` genera un error. Dentro de la sentencia catch, puede obtener el valor del `OperationException` miembro del `jobLog` objeto.

**Consulte también**

[Validación de documentos DDX](#validating-ddx-documents)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
