---
title: Montaje de documentos de PDF cifrados
seo-title: Assembling Encrypted PDF Documents
description: Ensamble documentos de PDF cifrados mediante la API de Java y la API de servicio web.
seo-description: Assemble encrypted PDF documents using the Java API and Web Service API.
uuid: d0948ec9-ab67-4fe4-9062-1c4938460b43
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 6d75c7b1-9c0e-47f3-bdb1-61acf16b97f9
role: Developer
exl-id: 2caaca74-640a-4257-a81b-3e8b295cd182
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1659'
ht-degree: 0%

---

# Montaje de documentos de PDF cifrados {#assembling-encrypted-pdf-documents}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

Puede cifrar un documento PDF con una contraseña utilizando el servicio Assembler. Una vez que un documento de PDF está cifrado con una contraseña, un usuario debe especificar la contraseña para ver el documento de PDF en Adobe Reader o Acrobat. Para codificar un documento PDF con una contraseña, el documento DDX debe contener valores de elementos de cifrado necesarios para cifrar un documento PDF.

A los efectos de esta discusión, supongamos que se utiliza el siguiente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
        <PDF result="EncryptLoan.pdf" encryption="userProtect">
         <PDF source="inDoc" />
     </PDF>
     <PasswordEncryptionProfile name="userProtect" compatibilityLevel="Acrobat7">
         <OpenPassword>AdobeOpen</OpenPassword>
        </PasswordEncryptionProfile>
 </DDX>
```

Dentro de este documento DDX, observe que al atributo de origen se le asigna el valor `inDoc`. En situaciones en las que solo se pasa un documento de PDF de entrada al servicio Assembler y se devuelve un documento de PDF, e invoca la variable `invokeOneDocument` operación, asignar el valor `inDoc` al atributo de origen del PDF. Al invocar la variable `invokeOneDocument` la operación `inDoc` es una clave predefinida que debe especificarse en el documento DDX.

Por el contrario, al pasar dos o más documentos de PDF de entrada al servicio Assembler, puede invocar la variable `invokeDDX` operación. En este caso, asigne el nombre de archivo del documento del PDF de entrada a la variable `source` atributo.

El servicio de cifrado no tiene que formar parte de la instalación de formularios AEM para codificar un documento de PDF con una contraseña. Consulte [Codificación y descifrado de documentos de PDF](/help/forms/developing/encrypting-decrypting-pdf-documents.md).

>[!NOTE]
>
>Para obtener más información sobre el servicio Assembler, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para ensamblar un documento de PDF cifrado, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de ensamblador de PDF.
1. Haga referencia a un documento DDX existente.
1. Haga referencia a un documento PDF no protegido.
1. Establezca las opciones de tiempo de ejecución.
1. Cifrar el documento.
1. Guarde el documento de PDF cifrado.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-Utilities.jar y jbossall-client.jar con archivos JAR específicos del servidor de aplicaciones J2EE en el que AEM Forms está implementado. Para obtener información sobre la ubicación de todos los archivos JAR de AEM Forms, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de ensamblador**

Para poder realizar una operación Assembler mediante programación, debe crear un cliente de servicio Assembler.

**Referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para ensamblar un documento PDF. Por ejemplo, considere el documento DDX que se introdujo en esta sección. Para cifrar un documento PDF, el documento DDX debe contener la variable `PasswordEncryptionProfile` elemento.

**Referencia a un documento PDF no protegido**

Se debe hacer referencia a un documento PDF no protegido y pasarlo al servicio Assembler para cifrarlo. Si hace referencia a un documento de PDF que ya está cifrado, se genera una excepción.

**Establecer opciones de tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlan el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede definir una opción que indique al servicio Assembler que continúe procesando un trabajo si se encuentra un error. Para obtener información sobre las opciones de tiempo de ejecución que puede establecer, consulte la `AssemblerOptionSpec` referencia de clase en [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Codificar el documento**

Después de crear el cliente de servicio Assembler, hacer referencia al documento DDX que contiene información de codificación, hacer referencia a un documento de PDF no protegido y establecer opciones en tiempo de ejecución, puede invocar la función `invokeOneDocument` operación. Como solo se está pasando un documento de PDF de entrada al servicio Assembler (y se devuelve un documento), puede usar la variable `invokeOneDocument` en lugar de `invokeDDX` operación.

**Guardar el documento de PDF cifrado**

Si solo se pasa un documento PDF al servicio Assembler, el servicio Assembler devuelve un documento único en lugar de un objeto de colección. Es decir, al invocar la variable `invokeOneDocument` , se devuelve un solo documento. Dado que el documento DDX al que se hace referencia en esta sección contiene información de codificación, el servicio Assembler devuelve un documento de PDF cifrado con una contraseña.

**Consulte también lo siguiente**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Montaje de un documento de PDF cifrado mediante la API de Java {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-assembler-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente Assembler.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `AssemblerServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un documento DDX existente.

   * Cree un `java.io.FileInputStream` objeto que representa el documento DDX utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo DDX.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Haga referencia a un documento PDF no protegido.

   * Cree un `java.io.FileInputStream` usando su constructor y pasando la ubicación de un documento PDF no protegido.
   * Cree un `com.adobe.idp.Document` y pase el `java.io.FileInputStream` objeto que contiene el documento PDF. Esta `com.adobe.idp.Document` se pasa al `invokeOneDocument` método.

1. Establezca las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` que almacena opciones en tiempo de ejecución mediante su constructor.
   * Configure las opciones en tiempo de ejecución para satisfacer los requisitos empresariales invocando un método que pertenece al `AssemblerOptionSpec` objeto. Por ejemplo, para solicitar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, invoque la función `AssemblerOptionSpec` del objeto `setFailOnError` método y pase `false`.

1. Cifrar el documento.

   Invocar el `AssemblerServiceClient` del objeto `invokeOneDocument` y pase los siguientes valores:

   * A `com.adobe.idp.Document` que representa el documento DDX. Asegúrese de que este documento DDX contenga el valor `inDoc` para el elemento de origen del PDF.
   * A `com.adobe.idp.Document` objeto que contiene el documento PDF no protegido.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica las opciones en tiempo de ejecución, incluidos el nivel predeterminado de fuente y registro de trabajos.

   La variable `invokeOneDocument` el método devuelve un `com.adobe.idp.Document` objeto que contiene un documento de PDF cifrado con contraseña.

1. Guarde el documento de PDF cifrado.

   * Cree un `java.io.File` y asegúrese de que la extensión del nombre de archivo es .pdf.
   * Invocar el `Document` del objeto `copyToFile` para copiar el contenido del `Document` al archivo. Asegúrese de usar la variable `Document` que la variable `invokeOneDocument` método devuelto.

**Consulte también lo siguiente**

[Inicio rápido (modo SOAP): Montaje de un documento PDF cifrado mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## Montaje de un documento de PDF cifrado mediante la API de servicio web {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL al configurar una referencia de servicio: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente Assembler.

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

1. Haga referencia a un documento PDF no protegido.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar el documento del PDF de entrada. Esta `BLOB` se pasa al `invokeOneDocument` como argumento.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento del PDF de entrada y el modo en el que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Establezca las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` que almacena opciones en tiempo de ejecución mediante su constructor.
   * Configure las opciones en tiempo de ejecución para satisfacer los requisitos empresariales asignando un valor a un miembro de datos que pertenezca al grupo `AssemblerOptionSpec` objeto. Por ejemplo, para solicitar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne `false` a `AssemblerOptionSpec` del objeto `failOnError` miembro de datos.

1. Cifrar el documento.

   Invocar el `AssemblerServiceClient` del objeto `invokeOneDocument` y pase los siguientes valores:

   * A `BLOB` objeto que representa el documento DDX
   * A `BLOB` objeto que representa el documento PDF no protegido
   * Un `AssemblerOptionSpec` objeto que especifica opciones en tiempo de ejecución

   La variable `invokeOneDocument` el método devuelve un `BLOB` objeto que contiene un documento de PDF cifrado.

1. Guarde el documento de PDF cifrado.

   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento del PDF cifrado y el modo en el que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` que la variable `invokeOneDocument` método devuelto. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` miembro de datos.
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
