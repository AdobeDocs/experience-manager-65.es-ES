---
title: Codificación y descifrado de documentos de PDF
seo-title: Encrypting and Decrypting PDF Documents
description: Utilice el servicio de cifrado para cifrar y descifrar documentos. Las tareas del servicio de cifrado incluyen la codificación de un documento de PDF con contraseña, la codificación de un documento de PDF con un certificado, la eliminación del cifrado basado en contraseña de un documento de PDF, la eliminación del cifrado basado en certificado de un documento de PDF, el desbloqueo del documento de PDF para que se puedan realizar otras operaciones del servicio y la determinación del tipo de cifrado de un documento de PDF protegido.
seo-description: Use the Encryption service to encrypt and decrypt documents. The Encryption service tasks include encrypting a PDF document with a password, encrypting a PDF document with a certificate, removing password-based encryption from a PDF document, removing certificate-based encryption from a PDF document, unlocking the PDF document so that other service operations can be performed, and determining the encryption type of a secured PDF document.
uuid: 4e4e2716-c21f-4bfe-ae7a-7e91442414ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 5e4bda3a-5648-4c0f-b2f8-bdbebb88f537
role: Developer
exl-id: d3cbca7f-9277-4d61-b198-abf4bb008f15
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '8189'
ht-degree: 0%

---

# Codificación y descifrado de documentos de PDF {#encrypting-and-decrypting-pdf-documents}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

**Acerca del servicio de cifrado**

El servicio Encryption permite cifrar y descifrar documentos. Cuando se cifra un documento, su contenido se vuelve ilegible. Un usuario autorizado puede descifrar el documento para obtener acceso al contenido. Si un documento PDF está cifrado con una contraseña, el usuario debe especificar la contraseña de apertura antes de que el documento se pueda ver en Adobe Reader o Adobe Acrobat. Del mismo modo, si un documento de PDF está cifrado con un certificado, el usuario debe descifrar el documento de PDF con la clave pública correspondiente al certificado (clave privada) que se utilizó para cifrar el documento de PDF.

Puede realizar estas tareas mediante el servicio de cifrado:

* Codifique un documento PDF con una contraseña. (Consulte [Codificación de documentos del PDF con una contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)
* Codificar un documento PDF con un certificado. (Consulte [Codificación de documentos del PDF con certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).)
* Elimine el cifrado basado en contraseña de un documento de PDF. (Consulte [Eliminación de la codificación de contraseña](encrypting-decrypting-pdf-documents.md#removing-password-encryption).)
* Elimine el cifrado basado en certificados de un documento de PDF. (Consulte [Eliminación de la codificación basada en certificados](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption).)
* Desbloquee el documento del PDF para que se puedan realizar otras operaciones de servicio. Por ejemplo, una vez desbloqueado un documento PDF cifrado con contraseña, puede aplicarle una firma digital. (Consulte [Desbloquear documentos PDF cifrados](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents).)
* Determine el tipo de cifrado de un documento de PDF protegido. (Consulte [Determinación del tipo de codificación](encrypting-decrypting-pdf-documents.md#determining-encryption-type).)

>[!NOTE]
>
>Para obtener más información sobre el servicio Cifrado, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Codificación de documentos del PDF con una contraseña {#encrypting-pdf-documents-with-a-password}

Cuando se cifra un documento PDF con una contraseña, un usuario debe especificar la contraseña para abrir el documento PDF en Adobe Reader o Acrobat. Además, antes de que se pueda realizar otra operación de AEM Forms, como firmar digitalmente el documento del PDF, un documento del PDF cifrado con contraseña debe desbloquearse.

>[!NOTE]
>
>Si se carga un documento de PDF cifrado en el repositorio de AEM Forms, no se puede descifrar el documento de PDF ni extraer el contenido XDP. Se recomienda no cifrar un documento antes de cargarlo en el repositorio de AEM Forms. (Consulte [Escribir recursos](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Para obtener más información sobre el servicio Cifrado, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para cifrar un documento PDF con una contraseña, realice los pasos siguientes:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de cifrado.
1. Obtenga un documento PDF para cifrar.
1. Establezca las opciones de tiempo de ejecución del cifrado.
1. Agregue la contraseña.
1. Guarde el documento de PDF cifrado como archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

**Creación de un objeto de API de cliente de cifrado**

Para realizar una operación de servicio de cifrado mediante programación, debe crear un cliente de servicio de cifrado.

**Obtener un documento PDF para cifrar**

Debe obtener un documento PDF sin encriptar para cifrar el documento con una contraseña. Si intenta proteger un documento de PDF que ya está cifrado, debe hacer una excepción.

**Establecer opciones de tiempo de ejecución de cifrado**

Para cifrar un documento PDF con una contraseña, debe especificar cuatro valores, incluidos dos valores de contraseña. El primer valor de contraseña se utiliza para cifrar el documento del PDF y debe especificarse al abrir el documento del PDF. El segundo valor de contraseña, denominado valor de contraseña maestro, se utiliza para eliminar el cifrado del documento de PDF. Los valores de contraseña distinguen entre mayúsculas y minúsculas y estos dos valores de contraseña no pueden ser los mismos.

Debe especificar los recursos del documento del PDF que desea codificar. Puede cifrar todo el documento del PDF, todo menos los metadatos del documento o solo los archivos adjuntos del documento. Si sólo cifra los archivos adjuntos del documento, se solicita al usuario una contraseña cuando intente acceder a los archivos adjuntos.

Al cifrar un documento de PDF, puede especificar los permisos asociados al documento protegido. Si especifica permisos, puede controlar las acciones que puede realizar un usuario que abre un documento PDF cifrado con contraseña. Por ejemplo, para extraer correctamente los datos del formulario, debe definir los siguientes permisos:

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>Los permisos se especifican como `PasswordEncryptionPermission` valores de enumeración.

**Agregar la contraseña**

Después de recuperar un documento de PDF no protegido y establecer valores de tiempo de ejecución de cifrado, puede agregar una contraseña al documento de PDF.

**Guarde el documento de PDF cifrado como archivo de PDF**

Puede guardar el documento de PDF cifrado con contraseña como archivo de PDF.

**Consulte también lo siguiente**

[Codificación de un documento de PDF mediante la API de Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[Codificación de un documento de PDF mediante la API de servicio web](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Codificación de documentos del PDF con certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### Codificación de un documento de PDF mediante la API de Java {#encrypt-a-pdf-document-using-the-java-api}

Codificar un documento PDF con una contraseña mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-encryption-client.jar, en la ruta de clase de su proyecto Java.

1. Cree una API de cliente de cifrado.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `EncryptionServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtenga un documento PDF para cifrar.

   * Cree un `java.io.FileInputStream` objeto que representa el documento del PDF que se va a cifrar usando su constructor y pasando un valor de cadena que especifica la ubicación del documento del PDF.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Establezca las opciones de tiempo de ejecución del cifrado.

   * Cree un `PasswordEncryptionOptionSpec` invocando su constructor.
   * Especifique los recursos del documento del PDF que desea cifrar invocando la variable `PasswordEncryptionOptionSpec` del objeto `setEncryptOption` método y pasar una `PasswordEncryptionOption` valor de enumeración que especifica los recursos de documento que se van a cifrar. Por ejemplo, para cifrar todo el documento del PDF, incluidos sus metadatos y sus archivos adjuntos, especifique `PasswordEncryptionOption.ALL`.
   * Cree un `java.util.List` objeto que almacena los permisos de codificación utilizando la variable `ArrayList` constructor.
   * Especifique un permiso invocando la variable `java.util.List` objeto ‘s `add` y pasando un valor de enumeración que corresponda al permiso que desea establecer. Por ejemplo, para establecer el permiso que permite a un usuario copiar datos ubicados en el documento del PDF, especifique `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`. (Repita este paso para cada permiso que desee establecer).
   * Especifique la opción de compatibilidad con Acrobat invocando la variable `PasswordEncryptionOptionSpec` del objeto `setCompatability` y pasando un valor de enumeración que especifica el nivel de compatibilidad de Acrobat. Por ejemplo, puede especificar `PasswordEncryptionCompatability.ACRO_7`.
   * Especifique el valor de la contraseña que permite a un usuario abrir el documento del PDF cifrado invocando la variable `PasswordEncryptionOptionSpec` del objeto `setDocumentOpenPassword` y pasando un valor de cadena que representa la contraseña abierta.
   * Especifique el valor de la contraseña maestra que permite al usuario eliminar el cifrado del documento del PDF invocando la variable `PasswordEncryptionOptionSpec` del objeto `setPermissionPassword` y pasando un valor de cadena que representa la contraseña maestra.

1. Agregue la contraseña.

   Codificar el documento del PDF invocando la variable `EncryptionServiceClient` del objeto `encryptPDFUsingPassword` y pasando los siguientes valores:

   * La variable `com.adobe.idp.Document` objeto que contiene el documento del PDF que se va a cifrar con la contraseña.
   * La variable `PasswordEncryptionOptionSpec` objeto que contiene opciones de tiempo de ejecución de cifrado.

   La variable `encryptPDFUsingPassword` el método devuelve un `com.adobe.idp.Document` objeto que contiene un documento de PDF cifrado con contraseña.

1. Guarde el documento de PDF cifrado como archivo de PDF.

   * Cree un `java.io.File` y asegúrese de que la extensión de archivo es .pdf.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `com.adobe.idp.Document` al archivo. Asegúrese de usar la variable `com.adobe.idp.Document` objeto devuelto por el `encryptPDFUsingPassword` método.

**Consulte también lo siguiente**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Codificación de un documento de PDF mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Codificación de un documento de PDF mediante la API de servicio web {#encrypting-a-pdf-document-using-the-web-service-api}

Cifre un documento PDF con una contraseña utilizando la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto de API de cliente de cifrado.

   * Cree un `EncryptionServiceClient` usando su constructor predeterminado.
   * Cree un `EncryptionServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `EncryptionServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga un documento PDF para cifrar.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar un documento de PDF cifrado con una contraseña.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF que se va a cifrar y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando el contenido de la matriz de bytes a la variable `BLOB` del objeto `MTOM` miembro de datos.

1. Establezca las opciones de tiempo de ejecución del cifrado.

   * Cree un `PasswordEncryptionOptionSpec` usando su constructor.
   * Especifique los recursos del documento del PDF que desea cifrar asignando una `PasswordEncryptionOption` valor de enumeración a la variable `PasswordEncryptionOptionSpec` del objeto `encryptOption` miembro de datos. Para cifrar todo el PDF, incluidos sus metadatos y sus archivos adjuntos, asigne `PasswordEncryptionOption.ALL` a este miembro de datos.
   * Especifique la opción de compatibilidad con Acrobat asignando una `PasswordEncryptionCompatability` valor de enumeración a la variable `PasswordEncryptionOptionSpec` del objeto `compatability` miembro de datos. Por ejemplo, asigne `PasswordEncryptionCompatability.ACRO_7` a este miembro de datos.
   * Especifique el valor de la contraseña que permite a un usuario abrir el documento del PDF cifrado asignando un valor de cadena que represente la contraseña de apertura al `PasswordEncryptionOptionSpec` del objeto `documentOpenPassword` miembro de datos.
   * Especifique el valor de la contraseña que permite al usuario eliminar el cifrado del documento del PDF asignando un valor de cadena que represente la contraseña maestra al `PasswordEncryptionOptionSpec` del objeto `permissionPassword` miembro de datos.

1. Agregue la contraseña.

   Codificar el documento del PDF invocando la variable `EncryptionServiceClient` del objeto `encryptPDFUsingPassword` y pasando los siguientes valores:

   * La variable `BLOB` objeto que contiene el documento del PDF que se va a cifrar con la contraseña.
   * La variable `PasswordEncryptionOptionSpec` objeto que contiene opciones de tiempo de ejecución de cifrado.

   La variable `encryptPDFUsingPassword` el método devuelve un `BLOB` objeto que contiene un documento de PDF cifrado con contraseña.

1. Guarde el documento de PDF cifrado como archivo de PDF.

   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento de PDF protegido.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto devuelto por el `encryptPDFUsingPassword` método. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` miembro de datos.
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Codificación de documentos del PDF con certificados {#encrypting-pdf-documents-with-certificates}

El cifrado basado en certificados permite cifrar un documento para destinatarios específicos mediante tecnología de clave pública. Se pueden otorgar a varios destinatarios diferentes permisos para el documento. Muchos aspectos del cifrado son posibles gracias a la tecnología de claves públicas. Se utiliza un algoritmo para generar dos números grandes, conocidos como *keys*, que tienen las siguientes propiedades:

* Se utiliza una clave para cifrar un conjunto de datos. Posteriormente, solo se puede utilizar la otra clave para descifrar los datos.
* Es imposible distinguir una clave de la otra.

Una de las claves actúa como clave privada de un usuario. Es importante que solo el usuario tenga acceso a esta clave. La otra clave es la clave pública del usuario, que se puede compartir con otros usuarios.

Un certificado de clave pública contiene la clave pública y la información de identificación del usuario. El formato X.509 se utiliza para almacenar certificados. Los certificados suelen ser emitidos y firmados digitalmente por una autoridad de certificación (CA), que es una entidad reconocida que proporciona una medida de confianza en la validez del certificado. Los certificados tienen una fecha de caducidad tras la cual ya no son válidos. Además, las listas de revocación de certificados (CRL) proporcionan información sobre los certificados revocados antes de su fecha de caducidad. Las listas CRL se publican periódicamente por las autoridades certificadoras. El estado de revocación de un certificado también se puede recuperar mediante el Protocolo de estado de certificado en línea (OCSP) a través de la red.

>[!NOTE]
>
>Si se carga un documento de PDF cifrado en el repositorio de AEM Forms, no se puede descifrar el documento de PDF ni extraer el contenido XDP. Se recomienda no cifrar un documento antes de cargarlo en el repositorio de AEM Forms. (Consulte [Escribir recursos](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Para poder cifrar un documento de PDF con un certificado, debe asegurarse de agregar el certificado a AEM Forms. Se agrega un certificado mediante la consola de administración o mediante programación mediante la API del administrador de confianza. (Consulte [Importación de credenciales mediante la API del administrador de confianza](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

>[!NOTE]
>
>Para obtener más información sobre el servicio Cifrado, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para cifrar un documento PDF con un certificado, realice los pasos siguientes:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de cifrado.
1. Obtenga un documento PDF para cifrar.
1. Haga referencia al certificado.
1. Establezca las opciones de tiempo de ejecución del cifrado.
1. Cree un documento de PDF cifrado por certificado.
1. Guarde el documento de PDF cifrado como archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

**Creación de un objeto de API de cliente de cifrado**

Para realizar una operación de servicio de cifrado mediante programación, debe crear un cliente de servicio de cifrado. Si utiliza la API del servicio de cifrado de Java, cree un `EncrytionServiceClient` objeto. Si está utilizando la API del servicio de cifrado del servicio web, cree un `EncryptionServiceService` objeto.

**Obtener un documento PDF para cifrar**

Debe obtener un documento PDF sin cifrar para cifrar. Si intenta proteger un documento PDF que ya está cifrado, se genera una excepción.

**Referencia al certificado**

Para codificar un documento PDF con un certificado, haga referencia a un certificado que se utilice para codificar un documento PDF. El certificado es un archivo .cer, un archivo .crt o un archivo .pem. Se utiliza un archivo PKCS#12 para almacenar claves privadas con los certificados correspondientes.

Al cifrar un documento PDF con un certificado, especifique los permisos asociados al documento protegido. Si especifica permisos, puede controlar las acciones que puede realizar un usuario que abra un documento de PDF cifrado por certificado.

**Establecer opciones de tiempo de ejecución de cifrado**

Especifique los recursos del documento del PDF que desea codificar. Puede cifrar todo el documento del PDF, todo lo que no sean los metadatos del documento o solo los archivos adjuntos del documento.

**Creación de un documento de PDF cifrado por certificado**

Después de recuperar un documento de PDF no protegido, hacer referencia al certificado y establecer las opciones de tiempo de ejecución, puede crear un documento de PDF cifrado por certificado. Una vez cifrado el documento del PDF, se necesita la clave pública correspondiente para descifrarlo.

**Guarde el documento de PDF cifrado como archivo de PDF**

Puede guardar el documento de PDF cifrado como un archivo de PDF.

**Consulte también lo siguiente**

[Codificar un documento de PDF con un certificado mediante la API de Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[Codificar un documento de PDF con un certificado mediante la API de servicio web](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Codificación de documentos del PDF con una contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Codificar un documento de PDF con un certificado mediante la API de Java {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

Codificar un documento de PDF con un certificado mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-encryption-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un objeto de API de cliente de cifrado.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `EncryptionServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtenga un documento PDF para cifrar.

   * Cree un `java.io.FileInputStream` objeto que representa el documento del PDF que se va a cifrar usando su constructor y pasando un valor de cadena que especifica la ubicación del documento del PDF.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Haga referencia al certificado.

   * Cree un `java.util.List` objeto que almacena información de permisos utilizando su constructor.
   * Especifique el permiso asociado al documento cifrado invocando la variable `java.util.List` del objeto `add` método y pasar una `CertificateEncryptionPermissions` valor de enumeración que representa los permisos otorgados al usuario que abre el documento de PDF protegido. Por ejemplo, para especificar todos los permisos, pase `CertificateEncryptionPermissions.PKI_ALL_PERM`.
   * Cree un `Recipient` usando su constructor.
   * Cree un `java.io.FileInputStream` objeto que representa el certificado que se utiliza para cifrar el documento del PDF utilizando su constructor y pasando un valor de cadena que especifica la ubicación del certificado.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` que representa el certificado.
   * Invocar el `Recipient` del objeto `setX509Cert` y pase el `com.adobe.idp.Document` que contiene el certificado. (Además, la variable `Recipient`puede tener un alias de certificado Truststore o una URL LDAP como origen de certificado).
   * Cree un `CertificateEncryptionIdentity` objeto que almacena información de permisos y certificados usando su constructor.
   * Invocar el `CertificateEncryptionIdentity` del objeto `setPerms` y pase el `java.util.List` objeto que almacena información de permisos.
   * Invocar el `CertificateEncryptionIdentity` del objeto `setRecipient` y pase el `Recipient` objeto que almacena información de certificado.
   * Cree un `java.util.List` objeto que almacena información de certificado usando su constructor.
   * Invocar el `java.util.List` método add del objeto y pase el `CertificateEncryptionIdentity` objeto. (Esta `java.util.List` se pasa como parámetro a la variable `encryptPDFUsingCertificates` método).

1. Establezca las opciones de tiempo de ejecución del cifrado.

   * Cree un `CertificateEncryptionOptionSpec` invocando su constructor.
   * Especifique los recursos del documento del PDF que desea cifrar invocando la variable `CertificateEncryptionOptionSpec` del objeto `setOption` método y pasar una `CertificateEncryptionOption` valor de enumeración que especifica los recursos de documento que se van a cifrar. Por ejemplo, para cifrar todo el documento del PDF, incluidos sus metadatos y sus archivos adjuntos, especifique `CertificateEncryptionOption.ALL`.
   * Especifique la opción de compatibilidad con Acrobat invocando la variable `CertificateEncryptionOptionSpec` del objeto `setCompat` método y pasar una `CertificateEncryptionCompatibility` valor de enumeración que especifica el nivel de compatibilidad de Acrobat. Por ejemplo, puede especificar `CertificateEncryptionCompatibility.ACRO_7`.

1. Cree un documento de PDF cifrado por certificado.

   Codificar el documento del PDF con un certificado invocando la variable `EncryptionServiceClient` del objeto `encryptPDFUsingCertificates` y pasando los siguientes valores:

   * La variable `com.adobe.idp.Document` objeto que contiene el documento PDF que se va a codificar.
   * La variable `java.util.List` objeto que almacena información de certificado.
   * La variable `CertificateEncryptionOptionSpec` objeto que contiene opciones de tiempo de ejecución de cifrado.

   La variable `encryptPDFUsingCertificates` el método devuelve un `com.adobe.idp.Document` objeto que contiene un documento de PDF cifrado con certificado.

1. Guarde el documento de PDF cifrado como archivo de PDF.

   * Cree un `java.io.File` y asegúrese de que la extensión del nombre de archivo es .pdf.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `com.adobe.idp.Document` al archivo. Asegúrese de usar la variable `com.adobe.idp.Document` objeto devuelto por el `encryptPDFUsingCertificates` método.

**Consulte también lo siguiente**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Codificación de un documento PDF con un certificado mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Codificar un documento de PDF con un certificado mediante la API de servicio web {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

Cifre un documento de PDF con un certificado mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto de API de cliente de cifrado.

   * Cree un `EncryptionServiceClient` usando su constructor predeterminado.
   * Cree un `EncryptionServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `EncryptionServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga un documento PDF para cifrar.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar un documento de PDF cifrado con un certificado.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF que se va a cifrar y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Haga referencia al certificado.

   * Cree un `Recipient` usando su constructor. Este objeto almacenará información de certificado.
   * Cree un `BLOB` usando su constructor. Esta `BLOB` almacenará el certificado que codifica el documento PDF.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del certificado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando el contenido de la matriz de bytes a la variable `BLOB` del objeto `MTOM` miembro de datos.
   * Asigne la variable `BLOB` objeto que almacena el certificado en el `Recipient` del objeto `x509Cert` miembro de datos.
   * Cree un `CertificateEncryptionIdentity` objeto que almacena información de certificado usando su constructor.
   * Asigne la variable `Recipient` objeto que almacena el certificado en el `CertificateEncryptionIdentity`miembro de datos del destinatario del objeto.
   * Cree un `Object` y asigne la `CertificateEncryptionIdentity` al primer elemento del `Object` matriz. Esta `Object` se pasa como parámetro a la matriz `encryptPDFUsingCertificates` método.

1. Establezca las opciones de tiempo de ejecución del cifrado.

   * Cree un `CertificateEncryptionOptionSpec` usando su constructor.
   * Especifique los recursos del documento del PDF que desea cifrar asignando una `CertificateEncryptionOption` valor de enumeración a la variable `CertificateEncryptionOptionSpec` del objeto `option` miembro de datos. Para cifrar todo el documento del PDF, incluidos sus metadatos y sus archivos adjuntos, asigne `CertificateEncryptionOption.ALL` a este miembro de datos.
   * Especifique la opción de compatibilidad con Acrobat asignando una `CertificateEncryptionCompatibility` valor de enumeración a la variable `CertificateEncryptionOptionSpec` del objeto `compat` miembro de datos. Por ejemplo, asigne `CertificateEncryptionCompatibility.ACRO_7` a este miembro de datos.

1. Cree un documento de PDF cifrado por certificado.

   Codificar el documento del PDF con un certificado invocando la variable `EncryptionServiceService` del objeto `encryptPDFUsingCertificates` y pasando los siguientes valores:

   * La variable `BLOB` objeto que contiene el documento PDF que se va a codificar.
   * La variable `Object` matriz que almacena información de certificado.
   * La variable `CertificateEncryptionOptionSpec` objeto que contiene opciones de tiempo de ejecución de cifrado.

   La variable `encryptPDFUsingCertificates` el método devuelve un `BLOB` objeto que contiene un documento de PDF cifrado con certificado.

1. Guarde el documento de PDF cifrado como archivo de PDF.

   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento de PDF protegido.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto devuelto por el `encryptPDFUsingCertificates` método. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `binaryData` miembro de datos.
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Eliminación de la codificación basada en certificados {#removing-certificate-based-encryption}

El cifrado basado en certificados se puede eliminar de un documento de PDF para que los usuarios puedan abrir el documento de PDF en Adobe Reader o Acrobat. Para eliminar el cifrado de un documento de PDF cifrado con un certificado, se debe hacer referencia a una clave pública. Una vez eliminado el cifrado de un documento de PDF, ya no es seguro.

>[!NOTE]
>
>Para obtener más información sobre el servicio Cifrado, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-2}

Para eliminar el cifrado basado en certificados de un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de cifrado.
1. Obtenga el documento de PDF cifrado.
1. Elimine el cifrado.
1. Guarde el documento de PDF como archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

**Crear un cliente de servicio de cifrado**

Para realizar una operación de servicio de cifrado mediante programación, debe crear un cliente de servicio de cifrado. Si utiliza la API del servicio de cifrado de Java, cree un `EncrytionServiceClient` objeto. Si está utilizando la API del servicio de cifrado del servicio web, cree un `EncryptionServiceService` objeto.

**Obtener el documento de PDF cifrado**

Debe obtener un documento de PDF cifrado para eliminar el cifrado basado en certificados. Si intenta eliminar el cifrado de un documento PDF que no está cifrado, se genera una excepción. Del mismo modo, si intenta eliminar el cifrado basado en certificados de un documento cifrado con contraseña, se genera una excepción.

**Eliminar cifrado**

Para eliminar el cifrado basado en certificados de un documento de PDF cifrado, se requiere un documento de PDF cifrado y la clave privada que corresponda a la clave utilizada para cifrar el documento de PDF. El valor de alias de la clave privada se especifica al quitar el cifrado basado en certificado de un documento de PDF cifrado. Para obtener información sobre la clave pública, consulte [Codificación de documentos del PDF con certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).

>[!NOTE]
>
>Se almacena una clave privada en el almacén de confianza de AEM Forms. Cuando se coloca un certificado allí, se especifica un valor de alias.

**Guardar el documento del PDF**

Una vez eliminado el cifrado basado en certificados de un documento de PDF cifrado, puede guardar el documento de PDF como archivo de PDF. Los usuarios pueden abrir el documento del PDF en Adobe Reader o Acrobat.

**Consulte también lo siguiente**

[Eliminación del cifrado basado en certificados mediante la API de Java](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[Eliminación del cifrado basado en certificados mediante la API de servicio web](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Eliminación del cifrado basado en certificados mediante la API de Java {#remove-certificate-based-encryption-using-the-java-api}

Elimine el cifrado basado en certificados de un documento de PDF mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-encryption-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente de servicio de cifrado.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `EncryptionServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtenga el documento de PDF cifrado.

   * Cree un `java.io.FileInputStream` objeto que representa el documento de PDF cifrado utilizando su constructor y pasando un valor de cadena que especifica la ubicación del documento de PDF cifrado.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Elimine el cifrado.

   Elimine el cifrado basado en certificados del documento de PDF invocando la variable `EncryptionServiceClient` del objeto `removePDFCertificateSecurity` y pasando los siguientes valores:

   * La variable `com.adobe.idp.Document` objeto que contiene el documento de PDF cifrado.
   * Un valor de cadena que especifica el nombre de alias de la clave privada que corresponde a la clave utilizada para cifrar el documento PDf.

   La variable `removePDFCertificateSecurity` el método devuelve un `com.adobe.idp.Document` objeto que contiene un documento PDF no protegido.

1. Guarde el documento del PDF.

   * Cree un `java.io.File` y asegúrese de que la extensión de archivo es .pdf.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `Document` al archivo. Asegúrese de usar la variable `com.adobe.idp.Document` objeto devuelto por el `removePDFCredentialSecurity` método.

**Consulte también lo siguiente**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Eliminación del cifrado basado en certificados mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminación del cifrado basado en certificados mediante la API de servicio web {#remove-certificate-based-encryption-using-the-web-service-api}

Elimine el cifrado basado en certificados mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de servicio de cifrado.

   * Cree un `EncryptionServiceClient` usando su constructor predeterminado.
   * Cree un `EncryptionServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `EncryptionServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento de PDF cifrado.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar el documento de PDF cifrado.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento del PDF cifrado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando el contenido de la matriz de bytes a la variable `BLOB` del objeto `MTOM` miembro de datos.

1. Elimine el cifrado.

   Invocar el `EncryptionServiceClient` del objeto `removePDFCertificateSecurity` y pase los siguientes valores:

   * La variable `BLOB` objeto que contiene datos de flujo de archivos que representan un documento PDF cifrado.
   * Un valor de cadena que especifica el nombre de alias de la clave pública que corresponde a la clave privada utilizada para cifrar el documento PDf.

   La variable `removePDFCredentialSecurity` el método devuelve un `BLOB` objeto que contiene un documento PDF no protegido.

1. Guarde el documento del PDF.

   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF no protegido.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto devuelto por el `removePDFPasswordSecurity` método. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` miembro de datos.
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Eliminación de la codificación de contraseña {#removing-password-encryption}

El cifrado basado en contraseña se puede eliminar de un documento de PDF para que los usuarios puedan abrir el documento de PDF en Adobe Reader o Acrobat sin tener que especificar una contraseña. Después de eliminar el cifrado basado en contraseña de un documento de PDF, el documento ya no es seguro.

>[!NOTE]
>
>Para obtener más información sobre el servicio Cifrado, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-3}

Para eliminar el cifrado basado en contraseña de un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto
1. Cree un cliente de servicio de cifrado.
1. Obtenga el documento de PDF cifrado.
1. Elimine la contraseña.
1. Guarde el documento de PDF como archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

**Crear un cliente de servicio de cifrado**

Para realizar una operación de servicio de cifrado mediante programación, debe crear un cliente de servicio de cifrado. Si utiliza la API del servicio de cifrado de Java, cree un `EncrytionServiceClient` objeto. Si está utilizando la API del servicio de cifrado del servicio web, cree un `EncryptionServiceService` objeto.

**Obtener el documento de PDF cifrado**

Debe obtener un documento de PDF cifrado para eliminar el cifrado basado en contraseña. Si intenta eliminar el cifrado de un documento PDF que no está cifrado, se genera una excepción.

**Quitar la contraseña**

Para eliminar el cifrado basado en contraseña de un documento de PDF cifrado, se requiere un documento de PDF cifrado y un valor de contraseña maestro que se utilicen para eliminar el cifrado del documento de PDF. La contraseña utilizada para abrir un documento PDF cifrado con contraseña no se puede usar para eliminar el cifrado. Se especifica una contraseña maestra cuando el documento PDF está cifrado con una contraseña. (Consulte [Codificación de documentos del PDF con una contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

**Guardar el documento del PDF**

Una vez que el servicio de cifrado elimina el cifrado basado en contraseña de un documento de PDF, puede guardar el documento de PDF como archivo de PDF. Los usuarios pueden abrir el documento del PDF en Adobe Reader o Acrobat sin especificar una contraseña.

**Consulte también lo siguiente**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Codificación de documentos del PDF con una contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Eliminación del cifrado basado en contraseña mediante la API de Java {#remove-password-based-encryption-using-the-java-api}

Elimine el cifrado basado en contraseña de un documento de PDF mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-encryption-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente de servicio de cifrado.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `EncryptionServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtenga el documento de PDF cifrado.

   * Cree un `java.io.FileInputStream` objeto que representa el documento de PDF cifrado utilizando su constructor y pasando un valor de cadena que especifica la ubicación del documento de PDF.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Elimine la contraseña.

   Elimine el cifrado basado en contraseña del documento de PDF invocando la variable `EncryptionServiceClient` del objeto `removePDFPasswordSecurity` y pasando los siguientes valores:

   * A `com.adobe.idp.Document` objeto que contiene el documento de PDF cifrado.
   * Un valor de cadena que especifica el valor de la contraseña maestra que se utiliza para eliminar el cifrado del documento del PDF.

   La variable `removePDFPasswordSecurity` el método devuelve un `com.adobe.idp.Document` objeto que contiene un documento PDF no protegido.

1. Guarde el documento del PDF.

   * Cree un `java.io.File` y asegúrese de que la extensión del nombre de archivo es .pdf.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `Document` al archivo. Asegúrese de usar la variable `Document` objeto devuelto por el `removePDFPasswordSecurity` método.

**Consulte también lo siguiente**

[Inicio rápido (modo SOAP): Eliminación del cifrado basado en contraseña mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### Eliminación del cifrado basado en contraseña mediante la API de servicio web {#remove-password-based-encryption-using-the-web-service-api}

Elimine el cifrado basado en contraseña mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de servicio de cifrado.

   * Cree un `EncryptionServiceClient` usando su constructor predeterminado.
   * Cree un `EncryptionServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `EncryptionServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento de PDF cifrado.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar un documento PDF cifrado con contraseña.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento del PDF cifrado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando el contenido de la matriz de bytes a la variable `BLOB` del objeto `MTOM` miembro de datos.

1. Elimine la contraseña.

   Invocar el `EncryptionServiceService` del objeto `removePDFPasswordSecurity` y pase los siguientes valores:

   * La variable `BLOB` objeto que contiene datos de flujo de archivos que representan un documento PDF cifrado.
   * Un valor de cadena que especifica el valor de contraseña que se utiliza para eliminar el cifrado del documento del PDF. Este valor se especifica al cifrar el documento PDF con una contraseña.

   La variable `removePDFPasswordSecurity` el método devuelve un `BLOB` objeto que contiene un documento PDF no protegido.

1. Guarde el documento del PDF.

   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF no protegido.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto devuelto por el `removePDFPasswordSecurity` método. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` miembro de datos.
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Desbloquear documentos PDF cifrados {#unlocking-encrypted-pdf-documents}

Un documento PDF cifrado con contraseña o certificado debe desbloquearse antes de poder realizar otra operación de AEM Forms en él. Si intenta realizar una operación en un documento PDF cifrado, generará una excepción. Después de desbloquear un documento de PDF cifrado, puede realizar una o más operaciones en él. Estas operaciones pueden pertenecer a otros servicios, como el servicio de extensiones de Acrobat Reader DC.

>[!NOTE]
>
>Para obtener más información sobre el servicio Cifrado, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-4}

Para desbloquear un documento de PDF cifrado, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de cifrado.
1. Obtenga el documento de PDF cifrado.
1. Desbloquee el documento.
1. Realice una operación AEM Forms.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

**Crear un cliente de servicio de cifrado**

Para realizar una operación de servicio de cifrado mediante programación, debe crear un cliente de servicio de cifrado. Si utiliza la API del servicio de cifrado de Java, cree un `EncrytionServiceClient` objeto. Si está utilizando la API del servicio de cifrado del servicio web, cree un `EncryptionServiceService` objeto.

**Obtener el documento de PDF cifrado**

Debe obtener un documento PDF cifrado para desbloquearlo. Si intenta desbloquear un documento de PDF que no está cifrado, se genera una excepción.

**Desbloquear el documento**

Para desbloquear un documento de PDF cifrado con contraseña, se requiere un documento de PDF cifrado y un valor de contraseña que se utilicen para abrir un documento de PDF cifrado con contraseña. Este valor se especifica al cifrar el documento PDF con una contraseña. (Consulte [Codificación de documentos del PDF con una contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

Para desbloquear un documento de PDF cifrado por certificado, se requiere un documento de PDF cifrado y el valor de alias de la clave pública correspondiente a la clave privada que se utilizó para codificar el documento de PDF.

**Realizar una operación de AEM Forms**

Una vez desbloqueado un documento de PDF cifrado, puede realizar otra operación de servicio, como aplicarle derechos de uso. Esta operación pertenece al servicio Acrobat Reader DC Extensions.

**Consulte también lo siguiente**

[Desbloquear un documento PDF cifrado mediante la API de Java](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[Desbloquear un documento PDF cifrado mediante la API de servicio web](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Desbloquear un documento PDF cifrado mediante la API de Java {#unlock-an-encrypted-pdf-document-using-the-java-api}

Desbloquee un documento de PDF cifrado mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-encryption-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente de servicio de cifrado.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `EncryptionServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtenga el documento de PDF cifrado.

   * Cree un `java.io.FileInputStream` objeto que representa el documento de PDF cifrado utilizando su constructor y pasando un valor de cadena que especifica la ubicación del documento de PDF cifrado.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Desbloquee el documento.

   Desbloquee un documento de PDF cifrado invocando la variable `EncryptionServiceClient` del objeto `unlockPDFUsingPassword` o `unlockPDFUsingCredential` método.

   Para desbloquear un documento de PDF cifrado con una contraseña, invoque la función `unlockPDFUsingPassword` y pase los siguientes valores:

   * A `com.adobe.idp.Document` objeto que contiene el documento PDF cifrado con contraseña.
   * Valor de cadena que especifica el valor de contraseña que se utiliza para abrir un documento PDF cifrado con contraseña. Este valor se especifica al cifrar el documento PDF con una contraseña.

   Para desbloquear un documento de PDF cifrado con un certificado, invoque la función `unlockPDFUsingCredential` y pase los siguientes valores:

   * A `com.adobe.idp.Document` objeto que contiene el documento de PDF cifrado con certificado.
   * Un valor de cadena que especifica el nombre de alias de la clave pública que corresponde a la clave privada utilizada para cifrar el documento del PDF.

   La variable `unlockPDFUsingPassword` y `unlockPDFUsingCredential` los dos métodos devuelven un `com.adobe.idp.Document` objeto que pasa a otro método Java de AEM Forms para realizar una operación.

1. Realice una operación AEM Forms.

   Realice una operación de AEM Forms en el documento PDF desbloqueado para satisfacer los requisitos empresariales. Por ejemplo, suponiendo que desea aplicar derechos de uso a un documento de PDF desbloqueado, pase el `com.adobe.idp.Document` objeto devuelto por cualquiera de los `unlockPDFUsingPassword` o `unlockPDFUsingCredential` métodos de `ReaderExtensionsServiceClient` del objeto `applyUsageRights` método.

**Consulte también lo siguiente**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Desbloqueo de un documento PDF cifrado mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) (modo SOAP)

[Aplicación de derechos de uso a documentos de PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Desbloquear un documento PDF cifrado mediante la API de servicio web {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

Desbloquee un documento de PDF cifrado mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de servicio de cifrado.

   * Cree un `EncryptionServiceClient` usando su constructor predeterminado.
   * Cree un `EncryptionServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `EncryptionServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga un documento PDF cifrado.

   * Cree un `BLOB` usando su constructor.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento del PDF cifrado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando el contenido de la matriz de bytes a la variable `BLOB` del objeto `MTOM` miembro de datos.

1. Desbloquee el documento.

   Desbloquee un documento de PDF cifrado invocando la variable `EncryptionServiceClient` del objeto `unlockPDFUsingPassword` o `unlockPDFUsingCredential` método.

   Para desbloquear un documento de PDF cifrado con una contraseña, invoque la función `unlockPDFUsingPassword` y pase los siguientes valores:

   * A `BLOB` objeto que contiene el documento PDF cifrado con contraseña.
   * Valor de cadena que especifica el valor de contraseña que se utiliza para abrir un documento PDF cifrado con contraseña. Este valor se especifica al cifrar el documento PDF con una contraseña.

   Para desbloquear un documento de PDF cifrado con un certificado, invoque la función `unlockPDFUsingCredential` y pase los siguientes valores:

   * A `BLOB` objeto que contiene el documento de PDF cifrado con certificado.
   * Un valor de cadena que especifica el nombre de alias de la clave pública que corresponde a la clave privada utilizada para cifrar el documento PDf.

   La variable `unlockPDFUsingPassword` y `unlockPDFUsingCredential` los dos métodos devuelven un `com.adobe.idp.Document` objeto que se pasa a otro método de AEM Forms para realizar una operación.

1. Realice una operación AEM Forms.

   Realice una operación de AEM Forms en el documento PDF desbloqueado para satisfacer los requisitos empresariales. Por ejemplo, suponiendo que desea aplicar derechos de uso al documento del PDF desbloqueado, pase el `BLOB` objeto devuelto por cualquiera de los `unlockPDFUsingPassword` o `unlockPDFUsingCredential` métodos de `ReaderExtensionsServiceClient` del objeto `applyUsageRights` método.

**Consulte también lo siguiente**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Determinación del tipo de codificación {#determining-encryption-type}

Puede determinar mediante programación el tipo de cifrado que protege un documento de PDF mediante la API de servicio de cifrado de Java o la API de servicio de cifrado de servicio web. A veces es necesario determinar dinámicamente si un documento PDF está cifrado y, en caso afirmativo, el tipo de cifrado. Por ejemplo, puede determinar si un documento de PDF está protegido con cifrado basado en contraseña o con una directiva de Rights Management.

Un documento PDF puede estar protegido por los siguientes tipos de codificación:

* Cifrado basado en contraseña
* Cifrado basado en certificados
* Una directiva que crea el servicio de Rights Management
* Otro tipo de cifrado

>[!NOTE]
>
>Para obtener más información sobre el servicio Cifrado, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-5}

Para determinar el tipo de cifrado que protege un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de cifrado.
1. Obtenga el documento de PDF cifrado.
1. Determine el tipo de cifrado.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

**Crear un cliente de servicio**

Para realizar una operación de servicio de cifrado mediante programación, debe crear un cliente de servicio de cifrado. Si utiliza la API del servicio de cifrado de Java, cree un `EncrytionServiceClient` objeto. Si está utilizando la API del servicio de cifrado del servicio web, cree un `EncryptionServiceService` objeto.

**Obtener el documento de PDF cifrado**

Debe obtener un documento de PDF para determinar el tipo de cifrado que la protege.

**Determinar el tipo de codificación**

Puede determinar el tipo de cifrado que protege un documento PDF. Si el documento del PDF no está protegido, el servicio Encryption le informa de que el documento del PDF no está protegido.

**Consulte también lo siguiente**

[Determinar el tipo de cifrado mediante la API de Java](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[Determinar el tipo de cifrado mediante la API de servicio web](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Protección de documentos con directivas](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### Determinar el tipo de cifrado mediante la API de Java {#determine-the-encryption-type-using-the-java-api}

Determine el tipo de cifrado que protege un documento de PDF mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-encryption-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente de servicio.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `EncryptionServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtenga el documento de PDF cifrado.

   * Cree un `java.io.FileInputStream` objeto que representa el documento PDF utilizando su constructor y pasando un valor de cadena que especifica la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Determine el tipo de cifrado.

   * Determine el tipo de cifrado invocando la variable `EncryptionServiceClient` del objeto `getPDFEncryption` y pasando el `com.adobe.idp.Document` objeto que contiene el documento PDF. Este método devuelve un `EncryptionTypeResult` objeto.
   * Invocar el `EncryptionTypeResult` del objeto `getEncryptionType` método. Este método devuelve un `EncryptionType` valor de enumeración que especifica el tipo de codificación. Por ejemplo, si el documento del PDF está protegido con cifrado basado en contraseña, este método devuelve `EncryptionType.PASSWORD`.

**Consulte también lo siguiente**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Determinación del tipo de cifrado mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinar el tipo de cifrado mediante la API de servicio web {#determine-the-encryption-type-using-the-web-service-api}

Determine el tipo de cifrado que protege un documento de PDF mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de servicio.

   * Cree un `EncryptionServiceClient` usando su constructor predeterminado.
   * Cree un `EncryptionServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `EncryptionServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento de PDF cifrado.

   * Cree un `BLOB` usando su constructor.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento del PDF cifrado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando el contenido de la matriz de bytes a la variable `BLOB` del objeto `MTOM` miembro de datos.

1. Determine el tipo de cifrado.

   * Invocar el `EncryptionServiceClient` del objeto `getPDFEncryption` y pase el `BLOB` objeto que contiene el documento PDF. Este método devuelve un `EncryptionTypeResult` objeto.
   * Obtener el valor de la variable `EncryptionTypeResult` del objeto `encryptionType` método de datos. Por ejemplo, si el documento del PDF está protegido con cifrado basado en contraseña, el valor de este miembro de datos es `EncryptionType.PASSWORD`.

**Consulte también lo siguiente**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
