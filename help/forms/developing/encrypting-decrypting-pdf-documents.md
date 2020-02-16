---
title: Cifrar y descifrar documentos PDF
seo-title: Cifrar y descifrar documentos PDF
description: nulo
seo-description: nulo
uuid: 4e4e2716-c21f-4bfe-ae7a-7e91442414ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 5e4bda3a-5648-4c0f-b2f8-bdbebb88f537
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# Cifrar y descifrar documentos PDF {#encrypting-and-decrypting-pdf-documents}

**Acerca del servicio de cifrado**

El servicio Cifrado le permite cifrar y descifrar documentos. Cuando se cifra un documento, su contenido se vuelve ilegible. Un usuario autorizado puede descifrar el documento para obtener acceso al contenido. Si un documento PDF está codificado con una contraseña, el usuario debe especificar la contraseña abierta antes de poder ver el documento en Adobe Reader o Adobe Acrobat. Del mismo modo, si un documento PDF está cifrado con un certificado, el usuario debe descifrar el documento PDF con la clave pública correspondiente al certificado (clave privada) que se utilizó para cifrar el documento PDF.

Puede realizar estas tareas mediante el servicio Cifrado:

* Cifre un documento PDF con una contraseña. (Consulte [Codificación de documentos PDF con una contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)).
* Cifrar un documento PDF con un certificado. (Consulte [Codificación de documentos PDF con certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)).
* Elimine la codificación basada en contraseña de un documento PDF. (Consulte [Eliminación del cifrado](encrypting-decrypting-pdf-documents.md#removing-password-encryption)de contraseña).
* Elimine la codificación basada en certificados de un documento PDF. (Consulte [Eliminación del cifrado](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption)basado en certificados).
* Desbloquee el documento PDF para que se puedan realizar otras operaciones de servicio. Por ejemplo, después de desbloquear un documento PDF con contraseña cifrada, puede aplicarle una firma digital. (Consulte [Desbloqueo de documentos](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents)PDF cifrados).
* Determinar el tipo de codificación de un documento PDF protegido. (Consulte [Determinación del tipo](encrypting-decrypting-pdf-documents.md#determining-encryption-type)de codificación.)

   ***Nota **:Para obtener más información sobre el servicio de cifrado, consulte Referencia de[servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).*

## Cifrado de documentos PDF con contraseña {#encrypting-pdf-documents-with-a-password}

Al cifrar un documento PDF con una contraseña, el usuario debe especificar la contraseña para abrir el documento PDF en Adobe Reader o Acrobat. Además, antes de que se pueda realizar otra operación de AEM Forms, como firmar digitalmente el documento PDF, se debe desbloquear un documento PDF con contraseña cifrada.

>[!NOTE]
>
>Si carga un documento PDF cifrado en el repositorio de AEM Forms, no podrá descifrar el documento PDF ni extraer el contenido XDP. Se recomienda no cifrar un documento antes de cargarlo en el repositorio de AEM Forms. (Consulte [Escritura de recursos](/help/forms/developing/aem-forms-repository.md#writing-resources)).

>[!NOTE]
>
>Para obtener más información sobre el servicio de cifrado, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para cifrar un documento PDF con una contraseña, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de cifrado.
1. Obtenga un documento PDF para cifrar.
1. Configure las opciones de tiempo de ejecución de cifrado.
1. Agregue la contraseña.
1. Guarde el documento PDF codificado como archivo PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encoding-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

**Creación de un objeto de API de cliente de codificación**

Para realizar una operación de servicio de cifrado mediante programación, debe crear un cliente de servicio de cifrado.

**Obtener un documento PDF para cifrar**

Debe obtener un documento PDF sin cifrar para cifrar el documento con una contraseña. Si intenta proteger un documento PDF que ya está codificado, puede provocar una excepción.

**Configurar opciones de tiempo de ejecución de cifrado**

Para cifrar un documento PDF con una contraseña, debe especificar cuatro valores, incluidos dos valores de contraseña. El primer valor de contraseña se utiliza para cifrar el documento PDF y debe especificarse al abrir el documento PDF. El segundo valor de contraseña, denominado valor de contraseña maestro, se utiliza para eliminar la codificación del documento PDF. Los valores de contraseña distinguen entre mayúsculas y minúsculas y estos dos valores de contraseña no pueden ser los mismos.

Debe especificar los recursos del documento PDF que desea codificar. Puede codificar todo el documento PDF, todo excepto los metadatos del documento o sólo los archivos adjuntos del documento. Si sólo cifra los datos adjuntos del documento, se solicita al usuario una contraseña cuando intente acceder a los datos adjuntos del archivo.

Al cifrar un documento PDF, puede especificar los permisos asociados al documento protegido. Al especificar permisos, puede controlar las acciones que un usuario que abre un documento PDF con contraseña cifrada puede realizar. Por ejemplo, para extraer correctamente los datos del formulario, debe establecer los siguientes permisos:

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>Los permisos se especifican como valores `PasswordEncryptionPermission` de enumeración.

**Agregar la contraseña**

Después de recuperar un documento PDF no seguro y establecer valores de tiempo de ejecución de codificación, puede agregar una contraseña al documento PDF.

**Guardar el documento PDF codificado como archivo PDF**

Puede guardar el documento PDF con contraseña cifrada como archivo PDF.

**Consulte también**

[Codificación de un documento PDF mediante la API de Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[Cifrado de un documento PDF mediante la API de servicio Web](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Codificación de documentos PDF con certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### Codificación de un documento PDF mediante la API de Java {#encrypt-a-pdf-document-using-the-java-api}

Cifrar un documento PDF con una contraseña mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-encoding-client.jar, en la ruta de clases del proyecto Java.

1. Crear una API de cliente de cifrado.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `EncryptionServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtenga un documento PDF para cifrar.

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF que se va a codificar utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Configure las opciones de tiempo de ejecución de cifrado.

   * Cree un `PasswordEncryptionOptionSpec` objeto invocando su constructor.
   * Especifique los recursos del documento PDF que desea codificar invocando el `PasswordEncryptionOptionSpec` método `setEncryptOption` del objeto y pasando un valor de `PasswordEncryptionOption` enumeración que especifica los recursos del documento que desea cifrar. Por ejemplo, para cifrar todo el documento PDF, incluidos sus metadatos y sus archivos adjuntos, especifique `PasswordEncryptionOption.ALL`.
   * Cree un `java.util.List` objeto que almacene los permisos de codificación mediante el `ArrayList` constructor.
   * Especifique un permiso invocando el `java.util.List` método &#39;s `add` del objeto y pasando un valor de enumeración que corresponda al permiso que desea establecer. Por ejemplo, para establecer el permiso que permite al usuario copiar datos ubicados en el documento PDF, especifique `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`. (Repita este paso para cada permiso que desee establecer).
   * Especifique la opción de compatibilidad de Acrobat invocando el `PasswordEncryptionOptionSpec` método `setCompatability` del objeto y pasando un valor de enumeración que especifica el nivel de compatibilidad de Acrobat. Por ejemplo, puede especificar `PasswordEncryptionCompatability.ACRO_7`.
   * Especifique el valor de contraseña que permite al usuario abrir el documento PDF codificado invocando el `PasswordEncryptionOptionSpec` método del `setDocumentOpenPassword` objeto y pasando un valor de cadena que representa la contraseña abierta.
   * Especifique el valor de la contraseña maestra que permite al usuario eliminar el cifrado del documento PDF invocando el `PasswordEncryptionOptionSpec` método `setPermissionPassword` del objeto y pasando un valor de cadena que representa la contraseña maestra.

1. Agregue la contraseña.

   Cifre el documento PDF invocando el `EncryptionServiceClient` método `encryptPDFUsingPassword` del objeto y pasando los siguientes valores:

   * El `com.adobe.idp.Document` objeto que contiene el documento PDF que se va a codificar con la contraseña.
   * El `PasswordEncryptionOptionSpec` objeto que contiene opciones de tiempo de ejecución de codificación.
   El `encryptPDFUsingPassword` método devuelve un `com.adobe.idp.Document` objeto que contiene un documento PDF con contraseña cifrada.

1. Guarde el documento PDF codificado como archivo PDF.

   * Cree un `java.io.File` objeto y asegúrese de que la extensión del archivo sea .pdf.
   * Invocar el `com.adobe.idp.Document` método del `copyToFile` objeto para copiar el contenido del `com.adobe.idp.Document` objeto en el archivo. Asegúrese de utilizar el `com.adobe.idp.Document` objeto devuelto por el `encryptPDFUsingPassword` método .

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Cifrado de un documento PDF mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Cifrado de un documento PDF mediante la API de servicio Web {#encrypting-a-pdf-document-using-the-web-service-api}

Cifre un documento PDF con una contraseña mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto de API de cliente de cifrado.

   * Cree un `EncryptionServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `EncryptionServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `EncryptionServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga un documento PDF para cifrar.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar un documento PDF codificado con una contraseña.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF que desea codificar y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando el contenido de la matriz de bytes al miembro de `BLOB` datos del `MTOM` objeto.

1. Configure las opciones de tiempo de ejecución de cifrado.

   * Cree un `PasswordEncryptionOptionSpec` objeto con su constructor.
   * Especifique los recursos del documento PDF que desea cifrar asignando un valor de `PasswordEncryptionOption` enumeración al miembro de `PasswordEncryptionOptionSpec` datos del `encryptOption` objeto. Para cifrar todo el PDF, incluidos sus metadatos y sus archivos adjuntos, asigne `PasswordEncryptionOption.ALL` a este miembro de datos.
   * Especifique la opción de compatibilidad de Acrobat asignando un valor de `PasswordEncryptionCompatability` enumeración al miembro de `PasswordEncryptionOptionSpec` datos del `compatability` objeto. Por ejemplo, asigne `PasswordEncryptionCompatability.ACRO_7` a este miembro de datos.
   * Especifique el valor de contraseña que permite al usuario abrir el documento PDF codificado asignando un valor de cadena que representa la contraseña abierta al miembro de `PasswordEncryptionOptionSpec` datos del `documentOpenPassword` objeto.
   * Especifique el valor de la contraseña que permite al usuario eliminar el cifrado del documento PDF asignando un valor de cadena que representa la contraseña maestra al miembro de `PasswordEncryptionOptionSpec` datos del `permissionPassword` objeto.

1. Agregue la contraseña.

   Cifre el documento PDF invocando el `EncryptionServiceClient` método `encryptPDFUsingPassword` del objeto y pasando los siguientes valores:

   * El `BLOB` objeto que contiene el documento PDF que se va a codificar con la contraseña.
   * El `PasswordEncryptionOptionSpec` objeto que contiene opciones de tiempo de ejecución de codificación.
   El `encryptPDFUsingPassword` método devuelve un `BLOB` objeto que contiene un documento PDF con contraseña cifrada.

1. Guarde el documento PDF codificado como archivo PDF.

   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF protegido.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto devuelto por el `encryptPDFUsingPassword` método. Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el `System.IO.BinaryWriter` método `Write` del objeto y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Codificación de documentos PDF con certificados {#encrypting-pdf-documents-with-certificates}

El cifrado basado en certificados permite cifrar un documento para destinatarios específicos mediante tecnología de clave pública. Se pueden otorgar a varios destinatarios permisos diferentes para el documento. Muchos aspectos de la encriptación son posibles gracias a la tecnología de claves públicas. Un algoritmo se utiliza para generar dos números grandes, conocidos como *claves*, que tienen las siguientes propiedades:

* Se utiliza una clave para cifrar un conjunto de datos. Posteriormente, sólo se puede utilizar la otra clave para descifrar los datos.
* Es imposible distinguir una clave de la otra.

Una de las claves actúa como clave privada del usuario. Es importante que solo el usuario tenga acceso a esta clave. La otra clave es la clave pública del usuario, que se puede compartir con otros usuarios.

Un certificado de clave pública contiene la clave pública y la información de identificación del usuario. El formato X.509 se utiliza para almacenar certificados. Los certificados suelen ser emitidos y firmados digitalmente por una autoridad de certificación (CA), que es una entidad reconocida que proporciona una medida de confianza en la validez del certificado. Los certificados tienen una fecha de caducidad, tras la cual ya no son válidos. Además, las listas de revocación de certificados (CRL) proporcionan información sobre los certificados revocados antes de su fecha de caducidad. Las listas CRL son publicadas periódicamente por las autoridades de certificación. El estado de revocación de un certificado también se puede recuperar mediante el protocolo de estado de certificado en línea (OCSP) a través de la red.

>[!NOTE]
>
>Si carga un documento PDF cifrado en el repositorio de AEM Forms, no podrá descifrar el documento PDF ni extraer el contenido XDP. Se recomienda no cifrar un documento antes de cargarlo en el repositorio de AEM Forms. (Consulte [Escritura de recursos](/help/forms/developing/aem-forms-repository.md#writing-resources)).

>[!NOTE]
>
>Para poder cifrar un documento PDF con un certificado, debe asegurarse de agregar el certificado a AEM Forms. Se agrega un certificado mediante la consola de administración o mediante programación mediante la API del administrador de confianza. (Consulte [Importación de credenciales mediante la API](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)del administrador de confianza).

>[!NOTE]
>
>Para obtener más información sobre el servicio de cifrado, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para cifrar un documento PDF con un certificado, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de cifrado.
1. Obtenga un documento PDF para cifrar.
1. Haga referencia al certificado.
1. Configure las opciones de tiempo de ejecución de cifrado.
1. Cree un documento PDF con cifrado de certificado.
1. Guarde el documento PDF codificado como archivo PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encoding-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en el servidor de aplicaciones JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en el servidor de aplicaciones JBoss)

**Creación de un objeto de API de cliente de codificación**

Para realizar una operación de servicio de cifrado mediante programación, debe crear un cliente de servicio de cifrado. Si utiliza la API de servicio de cifrado Java, cree un `EncrytionServiceClient` objeto. Si está utilizando la API de servicio de cifrado de servicio Web, cree un `EncryptionServiceService` objeto.

**Obtener un documento PDF para cifrar**

Debe obtener un documento PDF sin cifrar para cifrar. Si intenta proteger un documento PDF que ya está cifrado, se genera una excepción.

**Hacer referencia al certificado**

Para cifrar un documento PDF con un certificado, haga referencia a un certificado que se utilice para codificar un documento PDF. El certificado es un archivo .cer, un archivo .crt o un archivo .pem. Se utiliza un archivo PKCS#12 para almacenar claves privadas con los certificados correspondientes.

Al cifrar un documento PDF con un certificado, especifique los permisos asociados al documento protegido. Al especificar permisos, puede controlar las acciones que puede realizar un usuario que abre un documento PDF con cifrado de certificado.

**Configurar opciones de tiempo de ejecución de cifrado**

Especifique los recursos del documento PDF que desea codificar. Puede cifrar todo el documento PDF, excepto los metadatos del documento, o solo los archivos adjuntos del documento.

**Creación de un documento PDF con cifrado de certificado**

Después de recuperar un documento PDF no seguro, hacer referencia al certificado y definir las opciones en tiempo de ejecución, puede crear un documento PDF con cifrado de certificado. Después de codificar el documento PDF, necesita la clave pública correspondiente para descifrarlo.

**Guardar el documento PDF codificado como archivo PDF**

Puede guardar el documento PDF codificado como archivo PDF.

**Consulte también**

[Codificación de un documento PDF con un certificado mediante la API de Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[Codificación de un documento PDF con un certificado mediante la API de servicio Web](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Cifrado de documentos PDF con contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Codificación de un documento PDF con un certificado mediante la API de Java {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

Cifrar un documento PDF con un certificado mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-encoding-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto de API de cliente de cifrado.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `EncryptionServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtenga un documento PDF para cifrar.

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF que se va a codificar utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Haga referencia al certificado.

   * Cree un `java.util.List` objeto que almacene información de permisos mediante su constructor.
   * Especifique el permiso asociado al documento codificado invocando el `java.util.List` método `add` del objeto y pasando un valor de `CertificateEncryptionPermissions` enumeración que represente los permisos concedidos al usuario que abre el documento PDF protegido. Por ejemplo, para especificar todos los permisos, pase `CertificateEncryptionPermissions.PKI_ALL_PERM`.
   * Cree un `Recipient` objeto con su constructor.
   * Cree un `java.io.FileInputStream` objeto que represente el certificado que se utiliza para cifrar el documento PDF utilizando su constructor y pasando un valor de cadena que especifique la ubicación del certificado.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto que representa el certificado.
   * Invoque el `Recipient` método del `setX509Cert` objeto y pase el `com.adobe.idp.Document` objeto que contiene el certificado. (Además, el `Recipient`objeto puede tener un alias de certificado Truststore o una URL LDAP como origen de certificado).
   * Cree un `CertificateEncryptionIdentity` objeto que almacene información de permisos y certificados mediante su constructor.
   * Invoque el `CertificateEncryptionIdentity` método del `setPerms` objeto y pase el `java.util.List` objeto que almacena información de permisos.
   * Invoque el `CertificateEncryptionIdentity` método del `setRecipient` objeto y pase el `Recipient` objeto que almacena la información del certificado.
   * Cree un `java.util.List` objeto que almacene información de certificado mediante su constructor.
   * Invoque el método add del `java.util.List` objeto y pase el `CertificateEncryptionIdentity` objeto. (Este `java.util.List` objeto se pasa como parámetro al `encryptPDFUsingCertificates` método).

1. Configure las opciones de tiempo de ejecución de cifrado.

   * Cree un `CertificateEncryptionOptionSpec` objeto invocando su constructor.
   * Especifique los recursos del documento PDF que desea codificar invocando el `CertificateEncryptionOptionSpec` método `setOption` del objeto y pasando un valor de `CertificateEncryptionOption` enumeración que especifica los recursos del documento que desea cifrar. Por ejemplo, para cifrar todo el documento PDF, incluidos sus metadatos y sus archivos adjuntos, especifique `CertificateEncryptionOption.ALL`.
   * Especifique la opción de compatibilidad de Acrobat invocando el `CertificateEncryptionOptionSpec` método `setCompat` del objeto y pasando un valor de `CertificateEncryptionCompatibility` enumeración que especifica el nivel de compatibilidad de Acrobat. Por ejemplo, puede especificar `CertificateEncryptionCompatibility.ACRO_7`.

1. Cree un documento PDF con cifrado de certificado.

   Cifre el documento PDF con un certificado invocando el `EncryptionServiceClient` método `encryptPDFUsingCertificates` del objeto y pasando los valores siguientes:

   * El `com.adobe.idp.Document` objeto que contiene el documento PDF que se va a codificar.
   * El `java.util.List` objeto que almacena la información del certificado.
   * El `CertificateEncryptionOptionSpec` objeto que contiene opciones de tiempo de ejecución de codificación.
   El `encryptPDFUsingCertificates` método devuelve un `com.adobe.idp.Document` objeto que contiene un documento PDF con cifrado de certificado.

1. Guarde el documento PDF codificado como archivo PDF.

   * Cree un `java.io.File` objeto y asegúrese de que la extensión del nombre de archivo sea .pdf.
   * Invocar el `com.adobe.idp.Document` método del `copyToFile` objeto para copiar el contenido del `com.adobe.idp.Document` objeto en el archivo. Asegúrese de utilizar el `com.adobe.idp.Document` objeto devuelto por el `encryptPDFUsingCertificates` método .

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Codificación de un documento PDF con un certificado mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Codificación de un documento PDF con un certificado mediante la API de servicio Web {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

Cifrar un documento PDF con un certificado mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto de API de cliente de cifrado.

   * Cree un `EncryptionServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `EncryptionServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `EncryptionServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga un documento PDF para cifrar.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar un documento PDF codificado con un certificado.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF que desea codificar y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` propiedad con el contenido de la matriz de bytes.

1. Haga referencia al certificado.

   * Cree un `Recipient` objeto con su constructor. Este objeto almacenará información de certificado.
   * Cree un `BLOB` objeto con su constructor. Este `BLOB` objeto almacenará el certificado que codifica el documento PDF.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del certificado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando el contenido de la matriz de bytes al miembro de `BLOB` datos del `MTOM` objeto.
   * Asigne el `BLOB` objeto que almacena el certificado al miembro de datos del `Recipient` objeto `x509Cert` .
   * Cree un `CertificateEncryptionIdentity` objeto que almacene información de certificado mediante su constructor.
   * Asigne el `Recipient` objeto que almacena el certificado al miembro de datos del destinatario del `CertificateEncryptionIdentity`objeto.
   * Cree una `Object` matriz y asigne el `CertificateEncryptionIdentity` objeto al primer elemento de la `Object` matriz. Esta `Object` matriz se pasa como parámetro al `encryptPDFUsingCertificates` método.

1. Configure las opciones de tiempo de ejecución de cifrado.

   * Cree un `CertificateEncryptionOptionSpec` objeto con su constructor.
   * Especifique los recursos del documento PDF que desea cifrar asignando un valor de `CertificateEncryptionOption` enumeración al miembro de `CertificateEncryptionOptionSpec` datos del `option` objeto. Para cifrar todo el documento PDF, incluidos sus metadatos y sus archivos adjuntos, asígnele `CertificateEncryptionOption.ALL` a este miembro de datos.
   * Especifique la opción de compatibilidad de Acrobat asignando un valor de `CertificateEncryptionCompatibility` enumeración al miembro de `CertificateEncryptionOptionSpec` datos del `compat` objeto. Por ejemplo, asigne `CertificateEncryptionCompatibility.ACRO_7` a este miembro de datos.

1. Cree un documento PDF con cifrado de certificado.

   Cifre el documento PDF con un certificado invocando el `EncryptionServiceService` método `encryptPDFUsingCertificates` del objeto y pasando los valores siguientes:

   * El `BLOB` objeto que contiene el documento PDF que se va a codificar.
   * Matriz `Object` que almacena información de certificado.
   * El `CertificateEncryptionOptionSpec` objeto que contiene opciones de tiempo de ejecución de codificación.
   El `encryptPDFUsingCertificates` método devuelve un `BLOB` objeto que contiene un documento PDF con cifrado de certificado.

1. Guarde el documento PDF codificado como archivo PDF.

   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF protegido.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto devuelto por el `encryptPDFUsingCertificates` método. Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `binaryData` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el `System.IO.BinaryWriter` método `Write` del objeto y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Eliminación de la codificación basada en certificados {#removing-certificate-based-encryption}

La codificación basada en certificados se puede eliminar de un documento PDF para que los usuarios puedan abrir el documento PDF en Adobe Reader o Acrobat. Para eliminar la codificación de un documento PDF codificado con un certificado, se debe hacer referencia a una clave pública. Después de eliminar la codificación de un documento PDF, ya no es segura.

>[!NOTE]
>
>Para obtener más información sobre el servicio de cifrado, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-2}

Para eliminar la codificación basada en certificados de un documento PDF, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de cifrado.
1. Obtenga el documento PDF cifrado.
1. Eliminar cifrado.
1. Guarde el documento PDF como archivo PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encoding-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en el servidor de aplicaciones JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en el servidor de aplicaciones JBoss)

**Crear un cliente de servicio de cifrado**

Para realizar una operación de servicio de cifrado mediante programación, debe crear un cliente de servicio de cifrado. Si utiliza la API de servicio de cifrado Java, cree un `EncrytionServiceClient` objeto. Si está utilizando la API de servicio de cifrado de servicio Web, cree un `EncryptionServiceService` objeto.

**Obtener el documento PDF codificado**

Debe obtener un documento PDF cifrado para eliminar el cifrado basado en certificados. Si intenta eliminar la codificación de un documento PDF que no está cifrado, se genera una excepción. Del mismo modo, si intenta eliminar el cifrado basado en certificados de un documento con contraseña cifrada, se genera una excepción.

**Eliminar cifrado**

Para eliminar la codificación basada en certificados de un documento PDF codificado, se requiere tanto un documento PDF codificado como la clave privada correspondiente a la clave utilizada para cifrar el documento PDF. El valor de alias de la clave privada se especifica al eliminar la codificación basada en certificados de un documento PDF cifrado. Para obtener información sobre la clave pública, consulte [Codificación de documentos PDF con certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).

>[!NOTE]
>
>Una clave privada se almacena en el almacén de confianza de AEM Forms. Cuando se coloca un certificado allí, se especifica un valor de alias.

**Guardar el documento PDF**

Una vez que el cifrado basado en certificados se haya eliminado de un documento PDF codificado, puede guardar el documento PDF como archivo PDF. Los usuarios pueden abrir el documento PDF en Adobe Reader o Acrobat.

**Consulte también**

[Eliminar el cifrado basado en certificados mediante la API de Java](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[Eliminar el cifrado basado en certificados mediante la API de servicio Web](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Eliminar el cifrado basado en certificados mediante la API de Java {#remove-certificate-based-encryption-using-the-java-api}

Elimine el cifrado basado en certificados de un documento PDF mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-encoding-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de servicio de cifrado.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `EncryptionServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtenga el documento PDF cifrado.

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF codificado utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF codificado.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Eliminar cifrado.

   Elimine la codificación basada en certificados del documento PDF invocando el `EncryptionServiceClient` método `removePDFCertificateSecurity` del objeto y pasando los valores siguientes:

   * El `com.adobe.idp.Document` objeto que contiene el documento PDF codificado.
   * Un valor de cadena que especifica el nombre de alias de la clave privada que corresponde a la clave utilizada para cifrar el documento PDf.
   El `removePDFCertificateSecurity` método devuelve un `com.adobe.idp.Document` objeto que contiene un documento PDF no seguro.

1. Guarde el documento PDF.

   * Cree un `java.io.File` objeto y asegúrese de que la extensión del archivo sea .pdf.
   * Invocar el `com.adobe.idp.Document` método del `copyToFile` objeto para copiar el contenido del `Document` objeto en el archivo. Asegúrese de utilizar el `com.adobe.idp.Document` objeto devuelto por el `removePDFCredentialSecurity` método .

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Eliminación del cifrado basado en certificados mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminar el cifrado basado en certificados mediante la API de servicio Web {#remove-certificate-based-encryption-using-the-web-service-api}

Elimine el cifrado basado en certificados mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de servicio de cifrado.

   * Cree un `EncryptionServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `EncryptionServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `EncryptionServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento PDF cifrado.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar el documento PDF codificado.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF codificado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando el contenido de la matriz de bytes al miembro de `BLOB` datos del `MTOM` objeto.

1. Eliminar cifrado.

   Invoque el `EncryptionServiceClient` método del `removePDFCertificateSecurity` objeto y pase los valores siguientes:

   * El `BLOB` objeto que contiene datos de flujo de archivos que representa un documento PDF codificado.
   * Un valor de cadena que especifica el nombre de alias de la clave pública que corresponde a la clave privada utilizada para cifrar el documento PDf.
   El `removePDFCredentialSecurity` método devuelve un `BLOB` objeto que contiene un documento PDF no seguro.

1. Guarde el documento PDF.

   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF no protegido.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto devuelto por el `removePDFPasswordSecurity` método. Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el `System.IO.BinaryWriter` método `Write` del objeto y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Eliminación del cifrado de contraseña {#removing-password-encryption}

La codificación basada en contraseña se puede eliminar de un documento PDF para que los usuarios puedan abrir el documento PDF en Adobe Reader o Acrobat sin tener que especificar una contraseña. Una vez que se elimina la codificación basada en contraseña de un documento PDF, el documento ya no es seguro.

>[!NOTE]
>
>Para obtener más información sobre el servicio de cifrado, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-3}

Para eliminar la codificación basada en contraseña de un documento PDF, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto
1. Cree un cliente de servicio de cifrado.
1. Obtenga el documento PDF cifrado.
1. Quite la contraseña.
1. Guarde el documento PDF como archivo PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encoding-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

**Crear un cliente de servicio de cifrado**

Para realizar una operación de servicio de cifrado mediante programación, debe crear un cliente de servicio de cifrado. Si utiliza la API de servicio de cifrado Java, cree un `EncrytionServiceClient` objeto. Si está utilizando la API de servicio de cifrado de servicio Web, cree un `EncryptionServiceService` objeto.

**Obtener el documento PDF codificado**

Debe obtener un documento PDF cifrado para eliminar el cifrado basado en contraseña. Si intenta eliminar la codificación de un documento PDF que no está cifrado, se genera una excepción.

**Quitar la contraseña**

Para eliminar la codificación basada en contraseña de un documento PDF codificado, se necesita un documento PDF cifrado y un valor de contraseña maestro que se utilicen para eliminar la codificación del documento PDF. La contraseña que se utiliza para abrir un documento PDF con contraseña cifrada no se puede utilizar para eliminar la codificación. Se especifica una contraseña maestra cuando el documento PDF se cifra con una contraseña. (Consulte [Codificación de documentos PDF con una contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)).

**Guardar el documento PDF**

Después de que el servicio de cifrado elimine la codificación basada en contraseña de un documento PDF, puede guardar el documento PDF como archivo PDF. Los usuarios pueden abrir el documento PDF en Adobe Reader o Acrobat sin especificar una contraseña.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Cifrado de documentos PDF con contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Eliminar el cifrado basado en contraseña mediante la API de Java {#remove-password-based-encryption-using-the-java-api}

Elimine la codificación basada en contraseña de un documento PDF mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-encoding-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de servicio de cifrado.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `EncryptionServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtenga el documento PDF cifrado.

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF codificado utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Quite la contraseña.

   Elimine la codificación basada en contraseña del documento PDF invocando el `EncryptionServiceClient` método `removePDFPasswordSecurity` del objeto y pasando los valores siguientes:

   * Un `com.adobe.idp.Document` objeto que contiene el documento PDF codificado.
   * Un valor de cadena que especifica el valor de contraseña principal que se utiliza para eliminar la codificación del documento PDF.
   El `removePDFPasswordSecurity` método devuelve un `com.adobe.idp.Document` objeto que contiene un documento PDF no seguro.

1. Guarde el documento PDF.

   * Cree un `java.io.File` objeto y asegúrese de que la extensión del nombre de archivo sea .pdf.
   * Invocar el `com.adobe.idp.Document` método del `copyToFile` objeto para copiar el contenido del `Document` objeto en el archivo. Asegúrese de utilizar el `Document` objeto devuelto por el `removePDFPasswordSecurity` método .

**Consulte también**

[Inicio rápido (modo SOAP): Eliminación del cifrado basado en contraseña mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### Eliminar el cifrado basado en contraseña mediante la API de servicio Web {#remove-password-based-encryption-using-the-web-service-api}

Elimine el cifrado basado en contraseña mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de servicio de cifrado.

   * Cree un `EncryptionServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `EncryptionServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `EncryptionServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento PDF cifrado.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar un documento PDF con contraseña cifrada.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF codificado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando el contenido de la matriz de bytes al miembro de `BLOB` datos del `MTOM` objeto.

1. Quite la contraseña.

   Invoque el `EncryptionServiceService` método del `removePDFPasswordSecurity` objeto y pase los valores siguientes:

   * El `BLOB` objeto que contiene datos de flujo de archivos que representa un documento PDF codificado.
   * Un valor de cadena que especifica el valor de contraseña que se utiliza para eliminar la codificación del documento PDF. Este valor se especifica al cifrar el documento PDF con una contraseña.
   El `removePDFPasswordSecurity` método devuelve un `BLOB` objeto que contiene un documento PDF no seguro.

1. Guarde el documento PDF.

   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF no protegido.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto devuelto por el `removePDFPasswordSecurity` método. Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el `System.IO.BinaryWriter` método `Write` del objeto y pasando la matriz de bytes.

**Consulte también**

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Desbloqueo de documentos PDF cifrados {#unlocking-encrypted-pdf-documents}

Un documento PDF con cifrado de contraseña o certificado debe desbloquearse antes de poder realizar otra operación de AEM Forms en él. Si intenta realizar una operación en un documento PDF cifrado, generará una excepción. Después de desbloquear un documento PDF codificado, puede realizar una o varias operaciones en él. Estas operaciones pueden pertenecer a otros servicios, como el servicio de extensiones de Acrobat Reader DC.

>[!NOTE]
>
>Para obtener más información sobre el servicio de cifrado, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-4}

Para desbloquear un documento PDF codificado, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de cifrado.
1. Obtenga el documento PDF cifrado.
1. Desbloquee el documento.
1. Realice una operación de AEM Forms.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encoding-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en el servidor de aplicaciones JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en el servidor de aplicaciones JBoss)

**Crear un cliente de servicio de cifrado**

Para realizar una operación de servicio de cifrado mediante programación, debe crear un cliente de servicio de cifrado. Si utiliza la API de servicio de cifrado Java, cree un `EncrytionServiceClient` objeto. Si está utilizando la API de servicio de cifrado de servicio Web, cree un `EncryptionServiceService` objeto.

**Obtener el documento PDF codificado**

Debe obtener un documento PDF cifrado para desbloquearlo. Si intenta desbloquear un documento PDF que no está cifrado, se genera una excepción.

**Desbloquear el documento**

Para desbloquear un documento PDF con contraseña cifrada, se necesita un documento PDF codificado y un valor de contraseña que se utilicen para abrir un documento PDF con contraseña cifrada. Este valor se especifica al cifrar el documento PDF con una contraseña. (Consulte [Codificación de documentos PDF con una contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)).

Para desbloquear un documento PDF con cifrado de certificado, se requiere un documento PDF codificado y el valor de alias de la clave pública correspondiente a la clave privada que se utilizó para cifrar el documento PDF.

**Realizar una operación de AEM Forms**

Después de desbloquear un documento PDF cifrado, puede realizar otra operación de servicio en él, como aplicarle derechos de uso. Esta operación pertenece al servicio Extensiones de Acrobat Reader DC.

**Consulte también**

[Desbloquear un documento PDF codificado mediante la API de Java](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[Desbloquear un documento PDF codificado mediante la API de servicio Web](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Desbloquear un documento PDF codificado mediante la API de Java {#unlock-an-encrypted-pdf-document-using-the-java-api}

Desbloquear un documento PDF cifrado mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-encoding-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de servicio de cifrado.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `EncryptionServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtenga el documento PDF cifrado.

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF codificado utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF codificado.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Desbloquee el documento.

   Desbloquee un documento PDF codificado invocando el `EncryptionServiceClient` método o `unlockPDFUsingPassword` el `unlockPDFUsingCredential` objeto.

   Para desbloquear un documento PDF codificado con una contraseña, invoque el `unlockPDFUsingPassword` método y pase los valores siguientes:

   * Un `com.adobe.idp.Document` objeto que contiene el documento PDF con contraseña cifrada.
   * Un valor de cadena que especifica el valor de contraseña que se utiliza para abrir un documento PDF con contraseña cifrada. Este valor se especifica al cifrar el documento PDF con una contraseña.
   Para desbloquear un documento PDF codificado con un certificado, invoque el `unlockPDFUsingCredential` método y pase los valores siguientes:

   * Un `com.adobe.idp.Document` objeto que contiene el documento PDF con cifrado de certificado.
   * Un valor de cadena que especifica el nombre de alias de la clave pública que corresponde a la clave privada utilizada para cifrar el documento PDF.
   Los métodos `unlockPDFUsingPassword` y `unlockPDFUsingCredential` devuelven un `com.adobe.idp.Document` objeto que se pasa a otro método Java de AEM Forms para realizar una operación.

1. Realice una operación de AEM Forms.

   Realice una operación de AEM Forms en el documento PDF desbloqueado para cumplir los requisitos comerciales. Por ejemplo, suponiendo que desea aplicar derechos de uso a un documento PDF desbloqueado, pase el `com.adobe.idp.Document` objeto devuelto por los métodos `unlockPDFUsingPassword` o `unlockPDFUsingCredential` al método del `ReaderExtensionsServiceClient` objeto `applyUsageRights` .

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Desbloqueo de un documento PDF codificado mediante la API](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) de Java (modo SOAP)

[Aplicación de derechos de uso a documentos PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Desbloquear un documento PDF codificado mediante la API de servicio Web {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

Desbloquear un documento PDF cifrado mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de servicio de cifrado.

   * Cree un `EncryptionServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `EncryptionServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `EncryptionServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga un documento PDF cifrado.

   * Cree un `BLOB` objeto con su constructor.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF codificado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando el contenido de la matriz de bytes al miembro de `BLOB` datos del `MTOM` objeto.

1. Desbloquee el documento.

   Desbloquee un documento PDF codificado invocando el `EncryptionServiceClient` método o `unlockPDFUsingPassword` el `unlockPDFUsingCredential` objeto.

   Para desbloquear un documento PDF codificado con una contraseña, invoque el `unlockPDFUsingPassword` método y pase los valores siguientes:

   * Un `BLOB` objeto que contiene el documento PDF con contraseña cifrada.
   * Un valor de cadena que especifica el valor de contraseña que se utiliza para abrir un documento PDF con contraseña cifrada. Este valor se especifica al cifrar el documento PDF con una contraseña.
   Para desbloquear un documento PDF codificado con un certificado, invoque el `unlockPDFUsingCredential` método y pase los valores siguientes:

   * Un `BLOB` objeto que contiene el documento PDF con cifrado de certificado.
   * Un valor de cadena que especifica el nombre de alias de la clave pública que corresponde a la clave privada utilizada para cifrar el documento PDf.
   Los métodos `unlockPDFUsingPassword` y `unlockPDFUsingCredential` devuelven un `com.adobe.idp.Document` objeto que se pasa a otro método de AEM Forms para realizar una operación.

1. Realice una operación de AEM Forms.

   Realice una operación de AEM Forms en el documento PDF desbloqueado para cumplir los requisitos comerciales. Por ejemplo, suponiendo que desea aplicar derechos de uso al documento PDF desbloqueado, pase el `BLOB` objeto devuelto por los métodos `unlockPDFUsingPassword` o `unlockPDFUsingCredential` al método del `ReaderExtensionsServiceClient` objeto `applyUsageRights` .

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Determinación del tipo de cifrado {#determining-encryption-type}

Puede determinar mediante programación el tipo de codificación que protege un documento PDF mediante la API de servicio de cifrado de Java o la API de servicio de cifrado de servicio Web. A veces es necesario determinar dinámicamente si un documento PDF está cifrado y, en caso afirmativo, el tipo de codificación. Por ejemplo, puede determinar si un documento PDF está protegido con codificación basada en contraseña o con una política de Rights Management.

Un documento PDF puede protegerse mediante los siguientes tipos de codificación:

* Cifrado basado en contraseña
* Cifrado basado en certificados
* Directiva creada por el servicio Rights Management
* Otro tipo de cifrado

>[!NOTE]
>
>Para obtener más información sobre el servicio de cifrado, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-5}

Para determinar el tipo de codificación que protege un documento PDF, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de cifrado.
1. Obtenga el documento PDF cifrado.
1. Determine el tipo de codificación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encoding-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en el servidor de aplicaciones JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en el servidor de aplicaciones JBoss)

**Crear un cliente de servicio**

Para realizar una operación de servicio de cifrado mediante programación, debe crear un cliente de servicio de cifrado. Si utiliza la API de servicio de cifrado Java, cree un `EncrytionServiceClient` objeto. Si está utilizando la API de servicio de cifrado de servicio Web, cree un `EncryptionServiceService` objeto.

**Obtener el documento PDF codificado**

Debe obtener un documento PDF para determinar el tipo de codificación que lo protege.

**Determinar el tipo de codificación**

Puede determinar el tipo de codificación que protege un documento PDF. Si el documento PDF no está protegido, el servicio Cifrado le informa de que el documento PDF no está protegido.

**Consulte también**

[Determinar el tipo de codificación mediante la API de Java](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[Determinar el tipo de codificación mediante la API de servicio Web](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Protección de documentos con políticas](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### Determinar el tipo de codificación mediante la API de Java {#determine-the-encryption-type-using-the-java-api}

Determine el tipo de codificación que protege un documento PDF mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-encoding-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de servicio.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `EncryptionServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtenga el documento PDF cifrado.

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Determine el tipo de codificación.

   * Determine el tipo de codificación invocando el `EncryptionServiceClient` método `getPDFEncryption` del objeto y pasando el `com.adobe.idp.Document` objeto que contiene el documento PDF. Este método devuelve un `EncryptionTypeResult` objeto.
   * Invocar el `EncryptionTypeResult` método del `getEncryptionType` objeto. Este método devuelve un valor `EncryptionType` enum que especifica el tipo de codificación. Por ejemplo, si el documento PDF está protegido con codificación basada en contraseña, este método devuelve `EncryptionType.PASSWORD`.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Determinación del tipo de codificación mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinar el tipo de codificación mediante la API de servicio Web {#determine-the-encryption-type-using-the-web-service-api}

Determine el tipo de codificación que protege un documento PDF mediante la API de cifrado (servicio Web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de servicio.

   * Cree un `EncryptionServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `EncryptionServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `EncryptionServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento PDF cifrado.

   * Cree un `BLOB` objeto con su constructor.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF codificado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando el contenido de la matriz de bytes al miembro de `BLOB` datos del `MTOM` objeto.

1. Determine el tipo de codificación.

   * Invoque el `EncryptionServiceClient` método del `getPDFEncryption` objeto y pase el `BLOB` objeto que contiene el documento PDF. Este método devuelve un `EncryptionTypeResult` objeto.
   * Obtenga el valor del método de datos del `EncryptionTypeResult` objeto `encryptionType` . Por ejemplo, si el documento PDF está protegido con codificación basada en contraseña, el valor de este miembro de datos es `EncryptionType.PASSWORD`.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)