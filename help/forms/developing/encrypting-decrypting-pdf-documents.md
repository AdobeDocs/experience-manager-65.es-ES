---
title: Codificar y descifrar documentos PDF
seo-title: Encrypting and Decrypting PDF Documents
description: Utilice el servicio Encryption para cifrar y descifrar documentos. Las tareas del servicio Encryption incluyen cifrar un documento de PDF con una contraseña, cifrar un documento de PDF con un certificado, quitar el cifrado basado en contraseña de un documento de PDF, quitar el cifrado basado en certificado de un documento de PDF, desbloquear el documento de PDF para que se puedan realizar otras operaciones de servicio y determinar el tipo de cifrado de un documento de PDF protegido.
seo-description: Use the Encryption service to encrypt and decrypt documents. The Encryption service tasks include encrypting a PDF document with a password, encrypting a PDF document with a certificate, removing password-based encryption from a PDF document, removing certificate-based encryption from a PDF document, unlocking the PDF document so that other service operations can be performed, and determining the encryption type of a secured PDF document.
uuid: 4e4e2716-c21f-4bfe-ae7a-7e91442414ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 5e4bda3a-5648-4c0f-b2f8-bdbebb88f537
role: Developer
exl-id: d3cbca7f-9277-4d61-b198-abf4bb008f15
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '8187'
ht-degree: 2%

---

# Codificar y descifrar documentos PDF {#encrypting-and-decrypting-pdf-documents}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

**Acerca del servicio Encryption**

El servicio Encryption permite cifrar y descifrar documentos. Cuando se cifra un documento, su contenido se vuelve ilegible. Un usuario autorizado puede descifrar el documento para obtener acceso al contenido. Si un documento de PDF está cifrado con una contraseña, el usuario debe especificar la contraseña de apertura para poder ver el documento en Adobe Reader o Adobe Acrobat. Del mismo modo, si un documento de PDF está cifrado con un certificado, el usuario debe descifrar el documento de PDF con la clave pública que corresponde al certificado (clave privada) que se utilizó para cifrar el documento de PDF.

Puede realizar estas tareas mediante el servicio Encryption:

* Cifrar un documento de PDF con una contraseña. (Consulte [Cifrar documentos de PDF con una contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)
* Cifrar un documento de PDF con un certificado. (Consulte [Cifrar documentos de PDF con certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).)
* Quitar el cifrado basado en contraseña de un documento de PDF. (Consulte [Quitar el cifrado de contraseña](encrypting-decrypting-pdf-documents.md#removing-password-encryption).)
* Quitar el cifrado basado en certificados de un documento de PDF. (Consulte [Quitar el cifrado basado en certificados](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption).)
* Desbloquee el documento del PDF para que se puedan realizar otras operaciones de servicio. Por ejemplo, después de desbloquear un documento PDF cifrado con contraseña, puede aplicarle una firma digital. (Consulte [Desbloquear documentos cifrados de PDF](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents).)
* Determine el tipo de cifrado de un documento de PDF protegido. (Consulte [Determinar el tipo de cifrado](encrypting-decrypting-pdf-documents.md#determining-encryption-type).)

>[!NOTE]
>
>Para obtener más información sobre el servicio Encryption, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Cifrar documentos de PDF con una contraseña {#encrypting-pdf-documents-with-a-password}

Cuando se cifra un documento PDF con una contraseña, cualquier usuario deberá especificar la contraseña para abrir el documento PDF en Adobe Reader o Acrobat. Además, antes de que se pueda realizar otra operación de AEM Forms, como firmar digitalmente el documento de PDF, se debe desbloquear un documento de PDF cifrado con contraseña.

>[!NOTE]
>
>Si carga un documento de PDF cifrado en el repositorio de AEM Forms, no podrá descifrar el documento de PDF ni extraer el contenido XDP. Se recomienda no cifrar un documento antes de cargarlo en el repositorio de AEM Forms. (Consulte [Recursos de escritura](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Para obtener más información sobre el servicio Encryption, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para cifrar un documento de PDF con una contraseña, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de cifrado.
1. Obtenga un documento de PDF para cifrar.
1. Establecer opciones de cifrado en tiempo de ejecución.
1. Añada la contraseña.
1. Guarde el documento de PDF cifrado como un archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

**Crear un objeto de API de cliente de cifrado**

Para realizar mediante programación una operación de servicio Encryption, debe crear un cliente de servicio Encryption.

**Obtener un documento de PDF para cifrar**

Debe obtener un documento de PDF sin cifrar para cifrar el documento con una contraseña. Si intenta proteger un documento de PDF que ya está cifrado, se producirá una excepción.

**Establecer opciones de cifrado en tiempo de ejecución**

Para cifrar un documento de PDF con una contraseña, debe especificar cuatro valores, incluidos dos valores de contraseña. El primer valor de contraseña se utiliza para cifrar el documento de PDF y debe especificarse al abrir el documento de PDF. El segundo valor de contraseña, denominado valor de contraseña maestra, se utiliza para quitar el cifrado del documento de PDF. Los valores de contraseña distinguen entre mayúsculas y minúsculas y estos dos valores de contraseña no pueden ser iguales.

Debe especificar los recursos de documentos de PDF que desea cifrar. Puede cifrar todo el documento de PDF, todo excepto los metadatos del documento o solo los archivos adjuntos del documento. Si cifra únicamente los datos adjuntos del documento, se pedirá al usuario una contraseña cuando intente obtener acceso a los datos adjuntos del archivo.

Al cifrar un documento de PDF, puede especificar los permisos asociados al documento protegido. Al especificar permisos, puede controlar las acciones que puede realizar un usuario que abre un documento de PDF cifrado con contraseña. Por ejemplo, para extraer correctamente datos de formulario, debe definir los siguientes permisos:

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>Los permisos se especifican como `PasswordEncryptionPermission` valores de enumeración.

**Añadir la contraseña**

Después de recuperar un documento de PDF no protegido y establecer los valores de cifrado en tiempo de ejecución, puede agregar una contraseña al documento de PDF.

**Guarde el documento de PDF cifrado como un archivo de PDF**

Puede guardar el documento de PDF cifrado con contraseña como un archivo de PDF.

**Consulte también**

[Cifrado de un documento de PDF mediante la API de Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[Cifrado de un documento de PDF mediante la API de servicio web](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de API de servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Cifrar documentos de PDF con certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### Cifrado de un documento de PDF mediante la API de Java {#encrypt-a-pdf-document-using-the-java-api}

Cifrar un documento de PDF con una contraseña mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-encryption-client.jar, en la ruta de clase del proyecto Java.

1. Crear una API de cliente de cifrado.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `EncryptionServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Obtenga un documento de PDF para cifrar.

   * Crear un `java.io.FileInputStream` que representa el documento de PDF que se va a cifrar utilizando su constructor y pasando un valor de cadena que especifica la ubicación del documento de PDF.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Establecer opciones de cifrado en tiempo de ejecución.

   * Crear un `PasswordEncryptionOptionSpec` invocando su constructor.
   * Especifique los recursos de documento de PDF que se van a cifrar invocando el `PasswordEncryptionOptionSpec` del objeto `setEncryptOption` método y pasar un `PasswordEncryptionOption` valor de enumeración que especifica los recursos de documento que se van a cifrar. Por ejemplo, para cifrar todo el documento de PDF, incluidos sus metadatos y sus archivos adjuntos, especifique `PasswordEncryptionOption.ALL`.
   * Crear un `java.util.List` que almacena los permisos de cifrado mediante el objeto `ArrayList` constructor.
   * Especifique un permiso invocando el `java.util.List` objeto ‘s `add` y pasando un valor de enumeración que corresponde al permiso que desea establecer. Por ejemplo, para establecer el permiso que permite a un usuario copiar los datos ubicados en el documento del PDF, especifique `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`. (Repita este paso para cada permiso que desee establecer).
   * Especifique la opción de compatibilidad de Acrobat invocando la variable `PasswordEncryptionOptionSpec` del objeto `setCompatability` y pasando un valor de enumeración que especifica el nivel de compatibilidad de Acrobat. Por ejemplo, puede especificar `PasswordEncryptionCompatability.ACRO_7`.
   * Especifique el valor de contraseña que permite a un usuario abrir el documento de PDF cifrado invocando el `PasswordEncryptionOptionSpec` del objeto `setDocumentOpenPassword` y pasando un valor de cadena que representa la contraseña de apertura.
   * Especifique el valor de la contraseña maestra que permite al usuario quitar el cifrado del documento del PDF invocando el `PasswordEncryptionOptionSpec` del objeto `setPermissionPassword` y pasando un valor de cadena que representa la contraseña maestra.

1. Añada la contraseña.

   Cifre el documento del PDF invocando el `EncryptionServiceClient` del objeto `encryptPDFUsingPassword` y pasando los siguientes valores:

   * El `com.adobe.idp.Document` que contiene el documento de PDF que se va a cifrar con la contraseña.
   * El `PasswordEncryptionOptionSpec` que contiene opciones de cifrado en tiempo de ejecución.

   El `encryptPDFUsingPassword` El método devuelve un valor `com.adobe.idp.Document` que contiene un documento de PDF cifrado con contraseña.

1. Guarde el documento de PDF cifrado como un archivo de PDF.

   * Crear un `java.io.File` y asegúrese de que la extensión del archivo es .pdf.
   * Invoque el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `com.adobe.idp.Document` al archivo. Asegúrese de utilizar el `com.adobe.idp.Document` objeto que ha devuelto el `encryptPDFUsingPassword` método.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): cifrado de un documento de PDF mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Cifrado de un documento de PDF mediante la API de servicio web {#encrypting-a-pdf-document-using-the-web-service-api}

Cifrar un documento de PDF con una contraseña mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto de API de cliente de cifrado.

   * Crear un `EncryptionServiceClient` mediante su constructor predeterminado.
   * Crear un `EncryptionServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `EncryptionServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga un documento de PDF para cifrar.

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar un documento de PDF cifrado con una contraseña.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento de PDF que se va a cifrar y el modo en que se va a abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` asignando el contenido de la matriz de bytes al objeto `BLOB` del objeto `MTOM` miembro de datos.

1. Establecer opciones de cifrado en tiempo de ejecución.

   * Crear un `PasswordEncryptionOptionSpec` mediante su constructor.
   * Especifique los recursos de documento de PDF que se van a cifrar asignando un `PasswordEncryptionOption` valor de enumeración para `PasswordEncryptionOptionSpec` del objeto `encryptOption` miembro de datos. Para cifrar todo el PDF, incluidos sus metadatos y archivos adjuntos, asigne a `PasswordEncryptionOption.ALL` a este miembro de datos.
   * Especifique la opción de compatibilidad de Acrobat asignando un `PasswordEncryptionCompatability` valor de enumeración para `PasswordEncryptionOptionSpec` del objeto `compatability` miembro de datos. Por ejemplo, asigne a `PasswordEncryptionCompatability.ACRO_7` a este miembro de datos.
   * Especifique el valor de contraseña que permite a un usuario abrir el documento de PDF cifrado asignando un valor de cadena que representa la contraseña de apertura a `PasswordEncryptionOptionSpec` del objeto `documentOpenPassword` miembro de datos.
   * Especifique el valor de contraseña que permite al usuario quitar el cifrado del documento del PDF asignando un valor de cadena que represente la contraseña maestra al `PasswordEncryptionOptionSpec` del objeto `permissionPassword` miembro de datos.

1. Añada la contraseña.

   Cifre el documento del PDF invocando el `EncryptionServiceClient` del objeto `encryptPDFUsingPassword` y pasando los siguientes valores:

   * El `BLOB` que contiene el documento de PDF que se va a cifrar con la contraseña.
   * El `PasswordEncryptionOptionSpec` que contiene opciones de cifrado en tiempo de ejecución.

   El `encryptPDFUsingPassword` El método devuelve un valor `BLOB` que contiene un documento de PDF cifrado con contraseña.

1. Guarde el documento de PDF cifrado como un archivo de PDF.

   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación de archivo del documento de PDF protegido.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto que ha devuelto el `encryptPDFUsingPassword` método. Rellene la matriz de bytes obteniendo el valor de `BLOB` del objeto `MTOM` miembro de datos.
   * Crear un `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Cifrar documentos de PDF con certificados {#encrypting-pdf-documents-with-certificates}

El cifrado basado en certificados permite cifrar un documento para destinatarios específicos mediante tecnología de clave pública. Se pueden otorgar permisos a varios destinatarios diferentes para el documento. Muchos aspectos del cifrado son posibles gracias a la tecnología de claves públicas. Se utiliza un algoritmo para generar dos números grandes, conocidos como *teclas*, que tienen las siguientes propiedades:

* Se utiliza una clave para cifrar un conjunto de datos. Posteriormente, solo se puede utilizar la otra clave para descifrar los datos.
* Es imposible distinguir una clave de la otra.

Una de las claves actúa como clave privada de un usuario. Es importante que solo el usuario tenga acceso a esta clave. La otra clave es la clave pública del usuario, que se puede compartir con otros.

Un certificado de clave pública contiene la clave pública y la información de identificación del usuario. Se utiliza el formato X.509 para almacenar certificados. Los certificados los suele emitir y firmar digitalmente una autoridad de certificación (CA), que es una entidad reconocida que proporciona confianza en la validez del certificado. Los certificados tienen una fecha de caducidad tras la cual ya no son válidos. Además, las listas de revocación de certificados (CRL) proporcionan información sobre los certificados revocados antes de su fecha de caducidad. Las listas CRL las publican periódicamente las autoridades certificadoras. El estado de revocación de un certificado también se puede recuperar mediante el Protocolo de estado de certificado en línea (OCSP) a través de la red.

>[!NOTE]
>
>Si carga un documento de PDF cifrado en el repositorio de AEM Forms, no podrá descifrar el documento de PDF ni extraer el contenido XDP. Se recomienda no cifrar un documento antes de cargarlo en el repositorio de AEM Forms. (Consulte [Recursos de escritura](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Para poder cifrar un documento de PDF con un certificado, debe asegurarse de agregar el certificado a AEM Forms. Se agrega un certificado mediante la consola de administración o mediante programación mediante la API de Administrador de confianza. (Consulte [Importación de credenciales mediante la API de Trust Manager](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

>[!NOTE]
>
>Para obtener más información sobre el servicio Encryption, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para cifrar un documento de PDF con un certificado, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de cifrado.
1. Obtenga un documento de PDF para cifrar.
1. Haga referencia al certificado.
1. Establecer opciones de cifrado en tiempo de ejecución.
1. Cree un documento de PDF cifrado mediante certificado.
1. Guarde el documento de PDF cifrado como un archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

**Crear un objeto de API de cliente de cifrado**

Para realizar mediante programación una operación de servicio Encryption, debe crear un cliente de servicio Encryption. Si utiliza la API del servicio de cifrado de Java, cree un `EncrytionServiceClient` objeto. Si utiliza la API del servicio de cifrado del servicio web, cree un `EncryptionServiceService` objeto.

**Obtener un documento de PDF para cifrar**

Debe obtener un documento de PDF sin cifrar para cifrarlo. Si intenta proteger un documento de PDF que ya está cifrado, se generará una excepción.

**Hacer referencia al certificado**

Para cifrar un documento de PDF con un certificado, haga referencia a un certificado que se utiliza para cifrar un documento de PDF. El certificado es un archivo .cer, .crt o .pem. Se utiliza un archivo PKCS#12 para almacenar claves privadas con los certificados correspondientes.

Al cifrar un documento de PDF con un certificado, especifique los permisos asociados al documento protegido. Al especificar permisos, puede controlar las acciones que puede realizar un usuario que abre un documento de PDF cifrado mediante certificado.

**Establecer opciones de cifrado en tiempo de ejecución**

Especifique los recursos del documento de PDF que desea cifrar. Puede cifrar todo el documento de PDF, todo excepto los metadatos del documento o solo los archivos adjuntos del documento.

**Crear un documento de PDF cifrado mediante certificado**

Después de recuperar un documento de PDF no protegido, hacer referencia al certificado y establecer las opciones en tiempo de ejecución, puede crear un documento de PDF cifrado mediante certificado. Una vez cifrado el documento del PDF, se necesita la clave pública correspondiente para descifrarlo.

**Guarde el documento de PDF cifrado como un archivo de PDF**

Puede guardar el documento de PDF cifrado como un archivo de PDF.

**Consulte también**

[Cifrar un documento de PDF con un certificado mediante la API de Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[Cifrar un documento de PDF con un certificado mediante la API de servicio web](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de API de servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Cifrar documentos de PDF con una contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Cifrar un documento de PDF con un certificado mediante la API de Java {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

Cifrar un documento de PDF con un certificado mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-encryption-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto de API de cliente de cifrado.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `EncryptionServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Obtenga un documento de PDF para cifrar.

   * Crear un `java.io.FileInputStream` que representa el documento de PDF que se va a cifrar utilizando su constructor y pasando un valor de cadena que especifica la ubicación del documento de PDF.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Haga referencia al certificado.

   * Crear un `java.util.List` que almacena información de permisos utilizando su constructor.
   * Especifique el permiso asociado con el documento cifrado invocando el `java.util.List` del objeto `add` método y pasar un `CertificateEncryptionPermissions` valor de enumeración que representa los permisos concedidos al usuario que abre el documento de PDF protegido. Por ejemplo, para especificar todos los permisos, apruebe `CertificateEncryptionPermissions.PKI_ALL_PERM`.
   * Crear un `Recipient` mediante su constructor.
   * Crear un `java.io.FileInputStream` que representa el certificado que se utiliza para cifrar el documento del PDF utilizando su constructor y pasando un valor de cadena que especifica la ubicación del certificado.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` que representa el certificado.
   * Invoque el `Recipient` del objeto `setX509Cert` y pase el `com.adobe.idp.Document` que contiene el certificado. (Además, la variable `Recipient`El objeto puede tener un alias de certificado de Truststore o una URL LDAP como origen de certificado.)
   * Crear un `CertificateEncryptionIdentity` que almacena información de permisos y certificados utilizando su constructor.
   * Invoque el `CertificateEncryptionIdentity` del objeto `setPerms` y pase el `java.util.List` que almacena información de permisos.
   * Invoque el `CertificateEncryptionIdentity` del objeto `setRecipient` y pase el `Recipient` objeto que almacena información de certificado.
   * Crear un `java.util.List` que almacena información de certificados utilizando su constructor.
   * Invoque el `java.util.List` método add del objeto y pase el `CertificateEncryptionIdentity` objeto. (Esta `java.util.List` El objeto de se pasa como parámetro a `encryptPDFUsingCertificates` método.)

1. Establecer opciones de cifrado en tiempo de ejecución.

   * Crear un `CertificateEncryptionOptionSpec` invocando su constructor.
   * Especifique los recursos de documento de PDF que se van a cifrar invocando el `CertificateEncryptionOptionSpec` del objeto `setOption` método y pasar un `CertificateEncryptionOption` valor de enumeración que especifica los recursos de documento que se van a cifrar. Por ejemplo, para cifrar todo el documento de PDF, incluidos sus metadatos y sus archivos adjuntos, especifique `CertificateEncryptionOption.ALL`.
   * Especifique la opción de compatibilidad de Acrobat invocando la variable `CertificateEncryptionOptionSpec` del objeto `setCompat` método y pasar un `CertificateEncryptionCompatibility` valor de enumeración que especifica el nivel de compatibilidad de Acrobat. Por ejemplo, puede especificar `CertificateEncryptionCompatibility.ACRO_7`.

1. Cree un documento de PDF cifrado mediante certificado.

   Cifre el documento del PDF con un certificado invocando el `EncryptionServiceClient` del objeto `encryptPDFUsingCertificates` y pasando los siguientes valores:

   * El `com.adobe.idp.Document` que contiene el documento de PDF que se va a cifrar.
   * El `java.util.List` objeto que almacena información de certificado.
   * El `CertificateEncryptionOptionSpec` que contiene opciones de cifrado en tiempo de ejecución.

   El `encryptPDFUsingCertificates` El método devuelve un valor `com.adobe.idp.Document` que contiene un documento de PDF cifrado mediante certificado.

1. Guarde el documento de PDF cifrado como un archivo de PDF.

   * Crear un `java.io.File` y asegúrese de que la extensión del nombre de archivo es .pdf.
   * Invoque el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `com.adobe.idp.Document` al archivo. Asegúrese de utilizar el `com.adobe.idp.Document` objeto que ha devuelto el `encryptPDFUsingCertificates` método.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): cifrado de un documento de PDF con un certificado mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Cifrar un documento de PDF con un certificado mediante la API de servicio web {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

Cifrar un documento de PDF con un certificado mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto de API de cliente de cifrado.

   * Crear un `EncryptionServiceClient` mediante su constructor predeterminado.
   * Crear un `EncryptionServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `EncryptionServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga un documento de PDF para cifrar.

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar un documento de PDF cifrado con un certificado.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento de PDF que se va a cifrar y el modo en que se va a abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.

1. Haga referencia al certificado.

   * Crear un `Recipient` mediante su constructor. Este objeto almacenará información de certificado.
   * Crear un `BLOB` mediante su constructor. Esta `BLOB` almacenará el certificado que cifra el documento del PDF.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del certificado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` asignando el contenido de la matriz de bytes al objeto `BLOB` del objeto `MTOM` miembro de datos.
   * Asigne el `BLOB` que almacena el certificado en el `Recipient` del objeto `x509Cert` miembro de datos.
   * Crear un `CertificateEncryptionIdentity` que almacena información de certificados utilizando su constructor.
   * Asigne el `Recipient` que almacena el certificado en el `CertificateEncryptionIdentity`miembro de datos de destinatario del objeto.
   * Crear un `Object` y asigne la variable `CertificateEncryptionIdentity` al primer elemento del objeto `Object` matriz. Esta `Object` La matriz se pasa como parámetro a `encryptPDFUsingCertificates` método.

1. Establecer opciones de cifrado en tiempo de ejecución.

   * Crear un `CertificateEncryptionOptionSpec` mediante su constructor.
   * Especifique los recursos de documento de PDF que se van a cifrar asignando un `CertificateEncryptionOption` valor de enumeración para `CertificateEncryptionOptionSpec` del objeto `option` miembro de datos. Para cifrar todo el documento del PDF, incluidos sus metadatos y sus archivos adjuntos, asigne a `CertificateEncryptionOption.ALL` a este miembro de datos.
   * Especifique la opción de compatibilidad de Acrobat asignando un `CertificateEncryptionCompatibility` valor de enumeración para `CertificateEncryptionOptionSpec` del objeto `compat` miembro de datos. Por ejemplo, asigne a `CertificateEncryptionCompatibility.ACRO_7` a este miembro de datos.

1. Cree un documento de PDF cifrado mediante certificado.

   Cifre el documento del PDF con un certificado invocando el `EncryptionServiceService` del objeto `encryptPDFUsingCertificates` y pasando los siguientes valores:

   * El `BLOB` que contiene el documento de PDF que se va a cifrar.
   * El `Object` matriz que almacena información de certificados.
   * El `CertificateEncryptionOptionSpec` que contiene opciones de cifrado en tiempo de ejecución.

   El `encryptPDFUsingCertificates` El método devuelve un valor `BLOB` que contiene un documento de PDF cifrado mediante certificado.

1. Guarde el documento de PDF cifrado como un archivo de PDF.

   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación de archivo del documento de PDF protegido.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto que ha devuelto el `encryptPDFUsingCertificates` método. Rellene la matriz de bytes obteniendo el valor de `BLOB` del objeto `binaryData` miembro de datos.
   * Crear un `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Quitar el cifrado basado en certificados {#removing-certificate-based-encryption}

El cifrado basado en certificados se puede quitar de un documento de PDF para que los usuarios puedan abrir el documento de PDF en Adobe Reader o Acrobat. Para quitar el cifrado de un documento de PDF cifrado con un certificado, se debe hacer referencia a una clave pública. Una vez eliminado el cifrado de un documento de PDF, ya no es seguro.

>[!NOTE]
>
>Para obtener más información sobre el servicio Encryption, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-2}

Para quitar el cifrado basado en certificados de un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de cifrado.
1. Obtenga el documento cifrado del PDF.
1. Elimine el cifrado.
1. Guarde el documento de PDF como un archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

**Crear un cliente de servicio de cifrado**

Para realizar mediante programación una operación de servicio Encryption, debe crear un cliente de servicio Encryption. Si utiliza la API del servicio de cifrado de Java, cree un `EncrytionServiceClient` objeto. Si utiliza la API del servicio de cifrado del servicio web, cree un `EncryptionServiceService` objeto.

**Obtener el documento de PDF cifrado**

Debe obtener un documento de PDF cifrado para quitar el cifrado basado en certificados. Si intenta quitar el cifrado de un documento de PDF que no está cifrado, se generará una excepción. Del mismo modo, si intenta quitar el cifrado basado en certificados de un documento cifrado con contraseña, se generará una excepción.

**Quitar cifrado**

Para quitar el cifrado basado en certificados de un documento de PDF cifrado, necesita un documento de PDF cifrado y la clave privada que corresponde a la clave utilizada para cifrar el documento de PDF. El valor de alias de la clave privada se especifica al quitar el cifrado basado en certificados de un documento PDF cifrado. Para obtener información sobre la clave pública, consulte [Cifrar documentos de PDF con certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).

>[!NOTE]
>
>Una clave privada se almacena en el Almacén de confianza de AEM Forms. Cuando se coloca un certificado, se especifica un valor de alias.

**Guardar el documento del PDF**

Una vez quitado el cifrado basado en certificados de un documento de PDF cifrado, puede guardar el documento de PDF como un archivo de PDF. Los usuarios pueden abrir el documento del PDF en Adobe Reader o Acrobat.

**Consulte también**

[Quite el cifrado basado en certificados mediante la API de Java](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[Quitar el cifrado basado en certificados mediante la API de servicio web](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de API de servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Quite el cifrado basado en certificados mediante la API de Java {#remove-certificate-based-encryption-using-the-java-api}

Quite el cifrado basado en certificados de un documento de PDF mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-encryption-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de servicio de cifrado.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `EncryptionServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Obtenga el documento cifrado del PDF.

   * Crear un `java.io.FileInputStream` que representa el documento PDF cifrado utilizando su constructor y pasando un valor de cadena que especifica la ubicación del documento PDF cifrado.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Elimine el cifrado.

   Quite el cifrado basado en certificados del documento de PDF invocando el `EncryptionServiceClient` del objeto `removePDFCertificateSecurity` y pasando los siguientes valores:

   * El `com.adobe.idp.Document` que contiene el documento de PDF cifrado.
   * Valor de cadena que especifica el nombre de alias de la clave privada que corresponde a la clave utilizada para cifrar el documento PDFf.

   El `removePDFCertificateSecurity` El método devuelve un valor `com.adobe.idp.Document` que contiene un documento de PDF no protegido.

1. Guarde el documento del PDF.

   * Crear un `java.io.File` y asegúrese de que la extensión del archivo es .pdf.
   * Invoque el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `Document` al archivo. Asegúrese de utilizar el `com.adobe.idp.Document` objeto que ha devuelto el `removePDFCredentialSecurity` método.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Quitar el cifrado basado en certificados mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Quitar el cifrado basado en certificados mediante la API de servicio web {#remove-certificate-based-encryption-using-the-web-service-api}

Quite el cifrado basado en certificados mediante la API Encryption (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de servicio de cifrado.

   * Crear un `EncryptionServiceClient` mediante su constructor predeterminado.
   * Crear un `EncryptionServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `EncryptionServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento cifrado del PDF.

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar el documento de PDF cifrado.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF cifrado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` asignando el contenido de la matriz de bytes al objeto `BLOB` del objeto `MTOM` miembro de datos.

1. Elimine el cifrado.

   Invoque el `EncryptionServiceClient` del objeto `removePDFCertificateSecurity` y pasar los siguientes valores:

   * El `BLOB` que contiene datos de secuencia de archivos que representan un documento de PDF cifrado.
   * Valor de cadena que especifica el nombre de alias de la clave pública correspondiente a la clave privada utilizada para cifrar el documento PDFf.

   El `removePDFCredentialSecurity` El método devuelve un valor `BLOB` que contiene un documento de PDF no protegido.

1. Guarde el documento del PDF.

   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación de archivo del documento de PDF no protegido.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto que ha devuelto el `removePDFPasswordSecurity` método. Rellene la matriz de bytes obteniendo el valor de `BLOB` del objeto `MTOM` miembro de datos.
   * Crear un `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Quitar el cifrado de contraseña {#removing-password-encryption}

El cifrado basado en contraseña se puede quitar de un documento de PDF para que los usuarios puedan abrir el documento de PDF en Adobe Reader o Acrobat sin tener que especificar una contraseña. Una vez eliminado el cifrado basado en contraseña de un documento de PDF, el documento deja de ser seguro.

>[!NOTE]
>
>Para obtener más información sobre el servicio Encryption, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-3}

Para quitar el cifrado basado en contraseña de un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto
1. Cree un cliente de servicio de cifrado.
1. Obtenga el documento cifrado del PDF.
1. Elimine la contraseña.
1. Guarde el documento de PDF como un archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

**Crear un cliente de servicio de cifrado**

Para realizar mediante programación una operación de servicio Encryption, debe crear un cliente de servicio Encryption. Si utiliza la API del servicio de cifrado de Java, cree un `EncrytionServiceClient` objeto. Si utiliza la API del servicio de cifrado del servicio web, cree un `EncryptionServiceService` objeto.

**Obtener el documento de PDF cifrado**

Debe obtener un documento de PDF cifrado para quitar el cifrado basado en contraseña. Si intenta quitar el cifrado de un documento de PDF que no está cifrado, se generará una excepción.

**Eliminar la contraseña**

Para quitar el cifrado basado en contraseña de un documento de PDF cifrado, necesita un documento de PDF cifrado y un valor de contraseña maestra que se utilice para quitar el cifrado del documento de PDF. La contraseña utilizada para abrir un documento de PDF cifrado con contraseña no se puede utilizar para quitar el cifrado. Se especifica una contraseña maestra cuando el documento del PDF se cifra con una contraseña. (Consulte [Cifrar documentos de PDF con una contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

**Guardar el documento del PDF**

Una vez que el servicio Encryption quita el cifrado basado en contraseña de un documento de PDF, puede guardar el documento de PDF como un archivo de PDF. Los usuarios pueden abrir el documento del PDF en Adobe Reader o Acrobat sin especificar una contraseña.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de API de servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Cifrar documentos de PDF con una contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Eliminación del cifrado basado en contraseña mediante la API de Java {#remove-password-based-encryption-using-the-java-api}

Elimine el cifrado basado en contraseña de un documento de PDF mediante la API Encryption (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-encryption-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de servicio de cifrado.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `EncryptionServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Obtenga el documento cifrado del PDF.

   * Crear un `java.io.FileInputStream` que representa el documento PDF cifrado utilizando su constructor y pasando un valor de cadena que especifica la ubicación del documento PDF.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Elimine la contraseña.

   Quite el cifrado basado en contraseña del documento de PDF invocando el `EncryptionServiceClient` del objeto `removePDFPasswordSecurity` y pasando los siguientes valores:

   * A `com.adobe.idp.Document` que contiene el documento de PDF cifrado.
   * Valor de cadena que especifica el valor de la contraseña maestra que se utiliza para quitar el cifrado del documento de PDF.

   El `removePDFPasswordSecurity` El método devuelve un valor `com.adobe.idp.Document` que contiene un documento de PDF no protegido.

1. Guarde el documento del PDF.

   * Crear un `java.io.File` y asegúrese de que la extensión del nombre de archivo es .pdf.
   * Invoque el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `Document` al archivo. Asegúrese de utilizar el `Document` objeto que ha devuelto el `removePDFPasswordSecurity` método.

**Consulte también**

[Inicio rápido (modo SOAP): Eliminación del cifrado basado en contraseña mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### Quitar el cifrado basado en contraseña mediante la API de servicio web {#remove-password-based-encryption-using-the-web-service-api}

Quite el cifrado basado en contraseña utilizando la API Encryption (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de servicio de cifrado.

   * Crear un `EncryptionServiceClient` mediante su constructor predeterminado.
   * Crear un `EncryptionServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `EncryptionServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento cifrado del PDF.

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar un documento de PDF cifrado con contraseña.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF cifrado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` asignando el contenido de la matriz de bytes al objeto `BLOB` del objeto `MTOM` miembro de datos.

1. Elimine la contraseña.

   Invoque el `EncryptionServiceService` del objeto `removePDFPasswordSecurity` y pasar los siguientes valores:

   * El `BLOB` que contiene datos de secuencia de archivos que representan un documento de PDF cifrado.
   * Valor de cadena que especifica el valor de contraseña que se utiliza para quitar el cifrado del documento de PDF. Este valor se especifica al cifrar el documento del PDF con una contraseña.

   El `removePDFPasswordSecurity` El método devuelve un valor `BLOB` que contiene un documento de PDF no protegido.

1. Guarde el documento del PDF.

   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación de archivo del documento de PDF no protegido.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto que ha devuelto el `removePDFPasswordSecurity` método. Rellene la matriz de bytes obteniendo el valor de `BLOB` del objeto `MTOM` miembro de datos.
   * Crear un `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Desbloquear documentos cifrados de PDF {#unlocking-encrypted-pdf-documents}

Un documento de PDF cifrado con contraseña o cifrado con certificado debe estar desbloqueado para que se pueda realizar otra operación de AEM Forms en él. Si intenta realizar una operación en un documento de PDF cifrado, generará una excepción. Después de desbloquear un documento de PDF cifrado, puede realizar una o varias operaciones en él. Estas operaciones pueden pertenecer a otros servicios, como Acrobat Reader DC extensions Service.

>[!NOTE]
>
>Para obtener más información sobre el servicio Encryption, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-4}

Para desbloquear un documento de PDF cifrado, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de cifrado.
1. Obtenga el documento cifrado del PDF.
1. Desbloquee el documento.
1. Realice una operación de AEM Forms.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

**Crear un cliente de servicio de cifrado**

Para realizar mediante programación una operación de servicio Encryption, debe crear un cliente de servicio Encryption. Si utiliza la API del servicio de cifrado de Java, cree un `EncrytionServiceClient` objeto. Si utiliza la API del servicio de cifrado del servicio web, cree un `EncryptionServiceService` objeto.

**Obtener el documento de PDF cifrado**

Debe obtener un documento de PDF cifrado para desbloquearlo. Si intenta desbloquear un documento PDF que no está cifrado, se generará una excepción.

**Desbloquear el documento**

Para desbloquear un documento de PDF cifrado con contraseña, necesita un documento de PDF cifrado y un valor de contraseña que se utilice para abrir un documento de PDF cifrado con contraseña. Este valor se especifica al cifrar el documento del PDF con una contraseña. (Consulte [Cifrar documentos de PDF con una contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

Para desbloquear un documento de PDF cifrado mediante certificado, se necesita un documento de PDF cifrado y el valor de alias de la clave pública que corresponde a la clave privada que se utilizó para cifrar el documento de PDF.

**Realizar una operación de AEM Forms**

Una vez desbloqueado un documento de PDF cifrado, puede realizar otra operación de servicio en él, como aplicarle derechos de uso. Esta operación pertenece al servicio Acrobat Reader DC Extensions.

**Consulte también**

[Desbloquear un documento de PDF cifrado mediante la API de Java](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[Desbloquear un documento de PDF cifrado mediante la API de servicio web](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de API de servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Desbloquear un documento de PDF cifrado mediante la API de Java {#unlock-an-encrypted-pdf-document-using-the-java-api}

Desbloquee un documento de PDF cifrado mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-encryption-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de servicio de cifrado.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `EncryptionServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Obtenga el documento cifrado del PDF.

   * Crear un `java.io.FileInputStream` que representa el documento PDF cifrado utilizando su constructor y pasando un valor de cadena que especifica la ubicación del documento PDF cifrado.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Desbloquee el documento.

   Desbloquee un documento de PDF cifrado invocando el `EncryptionServiceClient` del objeto `unlockPDFUsingPassword` o `unlockPDFUsingCredential` método.

   Para desbloquear un documento de PDF cifrado con una contraseña, invoque el `unlockPDFUsingPassword` y pasar los siguientes valores:

   * A `com.adobe.idp.Document` que contiene el documento de PDF cifrado con contraseña.
   * Valor de cadena que especifica el valor de contraseña que se utiliza para abrir un documento de PDF cifrado con contraseña. Este valor se especifica al cifrar el documento del PDF con una contraseña.

   Para desbloquear un documento de PDF cifrado con un certificado, invoque el `unlockPDFUsingCredential` y pasar los siguientes valores:

   * A `com.adobe.idp.Document` que contiene el documento de PDF cifrado mediante certificado.
   * Valor de cadena que especifica el nombre de alias de la clave pública correspondiente a la clave privada utilizada para cifrar el documento de PDF.

   El `unlockPDFUsingPassword` y `unlockPDFUsingCredential` ambos métodos devuelven un `com.adobe.idp.Document` objeto que se pasa a otro método Java de AEM Forms para realizar una operación.

1. Realice una operación de AEM Forms.

   Realice una operación AEM Forms en el documento de PDF desbloqueado para satisfacer sus necesidades empresariales. Por ejemplo, suponiendo que desea aplicar derechos de uso a un documento de PDF desbloqueado, pase el `com.adobe.idp.Document` objeto devuelto por el método `unlockPDFUsingPassword` o `unlockPDFUsingCredential` métodos para la `ReaderExtensionsServiceClient` del objeto `applyUsageRights` método.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Desbloquear un documento de PDF cifrado mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) (modo SOAP)

[Aplicar derechos de uso a documentos de PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Desbloquear un documento de PDF cifrado mediante la API de servicio web {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

Desbloquee un documento de PDF cifrado mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de servicio de cifrado.

   * Crear un `EncryptionServiceClient` mediante su constructor predeterminado.
   * Crear un `EncryptionServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `EncryptionServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga un documento de PDF cifrado.

   * Crear un `BLOB` mediante su constructor.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF cifrado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` asignando el contenido de la matriz de bytes al objeto `BLOB` del objeto `MTOM` miembro de datos.

1. Desbloquee el documento.

   Desbloquee un documento de PDF cifrado invocando el `EncryptionServiceClient` del objeto `unlockPDFUsingPassword` o `unlockPDFUsingCredential` método.

   Para desbloquear un documento de PDF cifrado con una contraseña, invoque el `unlockPDFUsingPassword` y pasar los siguientes valores:

   * A `BLOB` que contiene el documento de PDF cifrado con contraseña.
   * Valor de cadena que especifica el valor de contraseña que se utiliza para abrir un documento de PDF cifrado con contraseña. Este valor se especifica al cifrar el documento del PDF con una contraseña.

   Para desbloquear un documento de PDF cifrado con un certificado, invoque el `unlockPDFUsingCredential` y pasar los siguientes valores:

   * A `BLOB` que contiene el documento de PDF cifrado mediante certificado.
   * Valor de cadena que especifica el nombre de alias de la clave pública correspondiente a la clave privada utilizada para cifrar el documento PDFf.

   El `unlockPDFUsingPassword` y `unlockPDFUsingCredential` ambos métodos devuelven un `com.adobe.idp.Document` objeto que se pasa a otro método AEM Forms para realizar una operación.

1. Realice una operación de AEM Forms.

   Realice una operación AEM Forms en el documento de PDF desbloqueado para satisfacer sus necesidades empresariales. Por ejemplo, suponiendo que desea aplicar derechos de uso al documento de PDF desbloqueado, pase el `BLOB` objeto devuelto por el método `unlockPDFUsingPassword` o `unlockPDFUsingCredential` métodos para la `ReaderExtensionsServiceClient` del objeto `applyUsageRights` método.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Determinar el tipo de cifrado {#determining-encryption-type}

Puede determinar mediante programación el tipo de cifrado que protege un documento de PDF mediante la API del servicio de cifrado de Java o la API del servicio de cifrado del servicio web. A veces es necesario determinar dinámicamente si un documento de PDF está cifrado y, si es así, el tipo de cifrado. Por ejemplo, puede determinar si un documento de PDF está protegido mediante cifrado basado en contraseña o una directiva de Rights Management.

Un documento de PDF puede protegerse con los siguientes tipos de cifrado:

* Cifrado basado en contraseña
* Cifrado basado en certificados
* Una directiva creada por el servicio Rights Management
* Otro tipo de cifrado

>[!NOTE]
>
>Para obtener más información sobre el servicio Encryption, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-5}

Para determinar el tipo de cifrado que protege un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de cifrado.
1. Obtenga el documento cifrado del PDF.
1. Determine el tipo de cifrado.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

**Creación de un cliente de servicios**

Para realizar mediante programación una operación de servicio Encryption, debe crear un cliente de servicio Encryption. Si utiliza la API del servicio de cifrado de Java, cree un `EncrytionServiceClient` objeto. Si utiliza la API del servicio de cifrado del servicio web, cree un `EncryptionServiceService` objeto.

**Obtener el documento de PDF cifrado**

Debe obtener un documento de PDF para determinar el tipo de cifrado que lo protege.

**Determinar el tipo de cifrado**

Puede determinar el tipo de cifrado que protege un documento de PDF. Si el documento del PDF no está protegido, el servicio Encryption le informa de que el documento del PDF no está protegido.

**Consulte también**

[Determine el tipo de cifrado mediante la API de Java](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[Determinar el tipo de cifrado mediante la API de servicio web](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de API de servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Proteger documentos mediante directivas](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### Determine el tipo de cifrado mediante la API de Java {#determine-the-encryption-type-using-the-java-api}

Determine el tipo de cifrado que protege un documento del PDF mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-encryption-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de servicios.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `EncryptionServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Obtenga el documento cifrado del PDF.

   * Crear un `java.io.FileInputStream` que representa el documento de PDF utilizando su constructor y pasando un valor de cadena que especifica la ubicación del documento de PDF.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Determine el tipo de cifrado.

   * Determine el tipo de cifrado invocando el `EncryptionServiceClient` del objeto `getPDFEncryption` y pasando el `com.adobe.idp.Document` que contiene el documento de PDF. Este método devuelve un `EncryptionTypeResult` objeto.
   * Invoque el `EncryptionTypeResult` del objeto `getEncryptionType` método. Este método devuelve un `EncryptionType` valor de enumeración que especifica el tipo de cifrado. Por ejemplo, si el documento de PDF está protegido con cifrado basado en contraseña, este método devuelve `EncryptionType.PASSWORD`.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Determinación del tipo de cifrado mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinar el tipo de cifrado mediante la API de servicio web {#determine-the-encryption-type-using-the-web-service-api}

Determine el tipo de cifrado que protege un documento del PDF mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de servicios.

   * Crear un `EncryptionServiceClient` mediante su constructor predeterminado.
   * Crear un `EncryptionServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `EncryptionServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento cifrado del PDF.

   * Crear un `BLOB` mediante su constructor.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF cifrado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` asignando el contenido de la matriz de bytes al objeto `BLOB` del objeto `MTOM` miembro de datos.

1. Determine el tipo de cifrado.

   * Invoque el `EncryptionServiceClient` del objeto `getPDFEncryption` y pase el `BLOB` que contiene el documento de PDF. Este método devuelve un `EncryptionTypeResult` objeto.
   * Obtener el valor de `EncryptionTypeResult` del objeto `encryptionType` método de datos. Por ejemplo, si el documento de PDF está protegido con cifrado basado en contraseña, el valor de este miembro de datos es `EncryptionType.PASSWORD`.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
