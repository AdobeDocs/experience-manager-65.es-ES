---
title: Validación de documentos DDX
seo-title: Validating DDX Documents
description: Valide un documento DDX mediante programación utilizando la API de Java y la API de servicio web.
seo-description: Validate a DDX document programmatically using the Java API and the Web Service API.
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
role: Developer
exl-id: 1f5a2cf3-ef6b-45b4-8fa8-b300e492fee1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1526'
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

**Creación de un cliente de ensamblador de PDF**

Para poder realizar una operación Assembler mediante programación, debe crear un cliente de servicio Assembler.

**Referencia a un documento DDX existente**

Para validar un documento DDX, debe hacer referencia a un documento DDX existente.

**Establecer opciones de tiempo de ejecución para validar el documento DDX**

Al validar un documento DDX, debe establecer opciones específicas de tiempo de ejecución que indiquen al servicio Assembler que valide el documento DDX en lugar de ejecutarlo. Además, puede aumentar la cantidad de información que el servicio Assembler escribe en el archivo de registro.

**Realizar la validación**

Después de crear el cliente de servicio Assembler, hacer referencia al documento DDX y establecer las opciones de tiempo de ejecución, puede invocar la función `invokeDDX` para validar el documento DDX. Al validar el documento DDX, puede pasar `null` como parámetro de mapa (este parámetro generalmente almacena documentos PDF que requiere el ensamblador para realizar las operaciones especificadas en el documento DDX).

Si la validación falla, se genera una excepción y el archivo de registro contiene detalles que explican por qué el documento DDX no es válido y se puede obtener de la variable `OperationException` instancia. Una vez pasado el análisis XML básico y la comprobación de esquemas, se realiza la validación con la especificación DDX. Todos los errores que se encuentran en el documento DDX se especifican en el registro.

**Guardar los resultados de validación en un archivo de registro**

El servicio Assembler devuelve los resultados de validación que puede escribir en un archivo de registro XML. La cantidad de detalle que el servicio Assembler escribe en el archivo de registro depende de la opción de tiempo de ejecución que haya establecido.

**Consulte también lo siguiente**

[Validación de un documento DDX mediante la API de Java](#validate-a-ddx-document-using-the-java-api)

[Validación de un documento DDX mediante la API de servicio web](#validate-a-ddx-document-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Validación de un documento DDX mediante la API de Java {#validate-a-ddx-document-using-the-java-api}

Valide un documento DDX utilizando la API del servicio Assembler (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-assembler-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente de ensamblador de PDF.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `AssemblerServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un documento DDX existente.

   * Cree un `java.io.FileInputStream` objeto que representa el documento DDX utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo DDX.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Defina las opciones en tiempo de ejecución para validar el documento DDX.

   * Cree un `AssemblerOptionSpec` que almacena opciones en tiempo de ejecución mediante su constructor.
   * Establezca la opción en tiempo de ejecución que indica al servicio Assembler que valide el documento DDX invocando el `AssemblerOptionSpec` método setValidateOnly del objeto y pasar `true`.
   * Establezca la cantidad de información que el servicio Assembler escribe en el archivo de registro invocando la variable `AssemblerOptionSpec` del objeto `getLogLevel` y pasar un valor de cadena cumple con sus requisitos. Al validar un documento DDX, desea que se escriba más información en el archivo de registro que ayudará en el proceso de validación. Como resultado, puede pasar el valor `FINE` o `FINER`.

1. Realice la validación.

   Invocar el `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores:

   * A `com.adobe.idp.Document` que representa el documento DDX.
   * El valor `null` para el objeto java.io.Map que generalmente almacena documentos de PDF.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica las opciones de tiempo de ejecución.

   La variable `invokeDDX` devuelve un valor `AssemblerResult` objeto que contiene información que especifica si el documento DDX es válido.

1. Guarde los resultados de validación en un archivo de registro.

   * Cree un `java.io.File` y asegúrese de que la extensión de nombre de archivo es .xml.
   * Invocar el `AssemblerResult` del objeto `getJobLog` método. Este método devuelve un `com.adobe.idp.Document` que contiene información de validación.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `com.adobe.idp.Document` al archivo.

   >[!NOTE]
   >
   >Si el documento DDX no es válido, `OperationException` se lanza. Dentro de la sentencia catch, puede invocar la variable `OperationException` del objeto `getJobLog` método.

**Consulte también lo siguiente**

[Validación de documentos DDX](#validating-ddx-documents)

[Inicio rápido (modo SOAP): Validación de documentos DDX mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) (modo SOAP)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Validación de un documento DDX mediante la API de servicio web {#validate-a-ddx-document-using-the-web-service-api}

Valide un documento DDX utilizando la API del servicio Assembler (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace localhost por la dirección IP del servidor de formularios.

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
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento DDX y el modo en el que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Defina las opciones en tiempo de ejecución para validar el documento DDX.

   * Cree un `AssemblerOptionSpec` que almacena opciones en tiempo de ejecución mediante su constructor.
   * Establezca la opción en tiempo de ejecución que indica al servicio Assembler que valide el documento DDX asignando el valor true al `AssemblerOptionSpec` del objeto `validateOnly` miembro de datos.
   * Establezca la cantidad de información que el servicio Assembler escribe en el archivo de registro asignando un valor de cadena al `AssemblerOptionSpec` del objeto `logLevel` miembro de datos. método Al validar un documento DDX, desea que se escriba más información en el archivo de registro que ayudará en el proceso de validación. Como resultado, puede especificar el valor `FINE` o `FINER`. Para obtener información sobre las opciones de tiempo de ejecución que puede establecer, consulte la `AssemblerOptionSpec` referencia de clase en [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Realice la validación.

   Invocar el `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores:

   * A `BLOB` que representa el documento DDX.
   * El valor `null` para el `Map` que generalmente almacena documentos PDF.
   * Un `AssemblerOptionSpec` objeto que especifica opciones en tiempo de ejecución.

   La variable `invokeDDX` devuelve un valor `AssemblerResult` objeto que contiene información que especifica si el documento DDX es válido.

1. Guarde los resultados de validación en un archivo de registro.

   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo de registro y el modo en el que se abre el archivo. Asegúrese de que la extensión del nombre de archivo es .xml.
   * Cree un `BLOB` objeto que almacena información de registro obteniendo el valor de la variable `AssemblerResult` del objeto `jobLog` miembro de datos.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` campo .
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

   >[!NOTE]
   >
   >Si el documento DDX no es válido, `OperationException` se lanza. Dentro de la sentencia catch, puede obtener el valor de la variable `OperationException` del objeto `jobLog` miembro.

**Consulte también lo siguiente**

[Validación de documentos DDX](#validating-ddx-documents)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
