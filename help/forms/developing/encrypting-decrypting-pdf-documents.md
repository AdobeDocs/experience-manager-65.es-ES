---
title: Cifrar y descifrar Documentos PDF
seo-title: Cifrar y descifrar Documentos PDF
description: Utilice el servicio Cifrado para cifrar y descifrar documentos. Las tareas del servicio de cifrado incluyen cifrar un documento PDF con una contraseña, cifrar un documento PDF con un certificado, quitar la codificación basada en contraseña de un documento PDF, quitar la codificación basada en certificados de un documento PDF, desbloquear el documento PDF para que se puedan realizar otras operaciones de servicio y determinar el tipo de codificación de un documento PDF seguro.
seo-description: Utilice el servicio Cifrado para cifrar y descifrar documentos. Las tareas del servicio de cifrado incluyen cifrar un documento PDF con una contraseña, cifrar un documento PDF con un certificado, quitar la codificación basada en contraseña de un documento PDF, quitar la codificación basada en certificados de un documento PDF, desbloquear el documento PDF para que se puedan realizar otras operaciones de servicio y determinar el tipo de codificación de un documento PDF seguro.
uuid: 4e4e2716-c21f-4bfe-ae7a-7e91442414ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 5e4bda3a-5648-4c0f-b2f8-bdbebb88f537
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '8258'
ht-degree: 0%

---


# Cifrar y descifrar Documentos PDF {#encrypting-and-decrypting-pdf-documents}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en el entorno JEE.**

**Acerca del servicio de cifrado**

El servicio Cifrado le permite cifrar y descifrar documentos. Cuando se cifra un documento, su contenido se vuelve ilegible. Un usuario autorizado puede descifrar el documento para obtener acceso al contenido. Si un documento PDF está cifrado con una contraseña, el usuario debe especificar la contraseña abierta para que el documento se pueda ver en Adobe Reader o Adobe Acrobat. Del mismo modo, si un documento PDF está cifrado con un certificado, el usuario debe descifrar el documento PDF con la clave pública correspondiente al certificado (clave privada) que se utilizó para cifrar el documento PDF.

Puede realizar estas tareas mediante el servicio Cifrado:

* Cifre un documento PDF con una contraseña. (Consulte [Cifrar Documentos PDF con una contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)).
* Cifrar un documento PDF con un certificado. (Consulte [Codificación de Documentos PDF con certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)).
* Elimine la codificación basada en contraseña de un documento PDF. (Consulte [Eliminación del cifrado de contraseña](encrypting-decrypting-pdf-documents.md#removing-password-encryption).)
* Elimine la codificación basada en certificados de un documento PDF. (Consulte [Eliminación del cifrado basado en certificados](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption).)
* Desbloquee el documento PDF para que se puedan realizar otras operaciones de servicio. Por ejemplo, después de desbloquear un documento PDF con contraseña cifrada, puede aplicarle una firma digital. (Consulte [Desbloqueo de Documentos PDF cifrados](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents)).
* Determine el tipo de codificación de un documento PDF seguro. (Consulte [Determinación del tipo de cifrado](encrypting-decrypting-pdf-documents.md#determining-encryption-type)).

>[!NOTE]
>
>Para obtener más información sobre el servicio de cifrado, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Cifrar Documentos PDF con una contraseña {#encrypting-pdf-documents-with-a-password}

Al cifrar un documento PDF con una contraseña, el usuario debe especificar la contraseña para abrir el documento PDF en Adobe Reader o Acrobat. Además, antes de que otra operación de AEM Forms, como la firma digital del documento PDF, se pueda realizar en el documento, se debe desbloquear un documento PDF con contraseña cifrada.

>[!NOTE]
>
>Si carga un documento PDF cifrado en el repositorio de AEM Forms, no podrá descifrar el documento PDF ni extraer el contenido XDP. Se recomienda no cifrar un documento antes de cargarlo en el repositorio de AEM Forms. (Consulte [Escritura de recursos](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Para obtener más información sobre el servicio de cifrado, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para cifrar un documento PDF con una contraseña, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de cifrado.
1. Obtenga un documento PDF para cifrar.
1. Configure las opciones de tiempo de ejecución de cifrado.
1. Añada la contraseña.
1. Guarde el documento PDF codificado como archivo PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (requerido si AEM Forms se implementa en JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss)

**Creación de un objeto de API de cliente de codificación**

Para realizar una operación de servicio de cifrado mediante programación, debe crear un cliente de servicio de cifrado.

**Obtener un documento PDF para cifrar**

Debe obtener un documento PDF sin cifrar para cifrar el documento con una contraseña. Si intenta proteger un documento PDF que ya está cifrado, puede provocar una excepción.

**Configurar opciones de tiempo de ejecución de cifrado**

Para cifrar un documento PDF con una contraseña, debe especificar cuatro valores, incluidos dos valores de contraseña. El primer valor de contraseña se utiliza para cifrar el documento PDF y debe especificarse al abrir el documento PDF. El segundo valor de contraseña, denominado valor de contraseña maestro, se utiliza para eliminar la codificación del documento PDF. Los valores de contraseña distinguen entre mayúsculas y minúsculas y estos dos valores de contraseña no pueden ser los mismos.

Debe especificar los recursos de documento PDF que desea cifrar. Puede cifrar todo el documento PDF, todo excepto los metadatos del documento o solo los datos adjuntos del documento. Si sólo cifra los datos adjuntos del documento, se solicita al usuario una contraseña cuando intente acceder a los datos adjuntos del archivo.

Al cifrar un documento PDF, puede especificar los permisos asociados al documento seguro. Al especificar permisos, puede controlar las acciones que un usuario que abre un documento PDF con contraseña cifrada puede realizar. Por ejemplo, para extraer correctamente los datos del formulario, debe establecer los siguientes permisos:

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>Los permisos se especifican como valores de lista desglosada `PasswordEncryptionPermission`.

**Añadir la contraseña**

Después de recuperar un documento PDF no seguro y establecer valores de tiempo de ejecución de codificación, puede agregar una contraseña al documento PDF.

**Guardar el documento PDF codificado como archivo PDF**

Puede guardar el documento PDF con contraseña cifrada como archivo PDF.

**Consulte también**

[Cifrar un documento PDF mediante la API de Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[Cifrado de un documento PDF mediante la API de servicio Web](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Codificación de Documentos PDF con certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### Cifrar un documento PDF mediante la API de Java {#encrypt-a-pdf-document-using-the-java-api}

Cifrar un documento PDF con una contraseña mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-encoding-client.jar, en la ruta de clases del proyecto Java.

1. Crear una API de cliente de cifrado.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EncryptionServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga un documento PDF para cifrar.

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF que se va a cifrar utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Configure las opciones de tiempo de ejecución de cifrado.

   * Cree un objeto `PasswordEncryptionOptionSpec` invocando su constructor.
   * Especifique los recursos de documento PDF que desea cifrar invocando el método `PasswordEncryptionOptionSpec` del objeto `setEncryptOption` y pasando un valor de lista desglosada `PasswordEncryptionOption` que especifica los recursos de documento que desea cifrar. Por ejemplo, para cifrar todo el documento PDF, incluidos sus metadatos y sus archivos adjuntos, especifique `PasswordEncryptionOption.ALL`.
   * Cree un objeto `java.util.List` que almacene los permisos de codificación mediante el constructor `ArrayList`.
   * Especifique un permiso invocando el método `java.util.List` del objeto ‘s `add` y pasando un valor de lista desglosada que corresponda al permiso que desea establecer. Por ejemplo, para establecer el permiso que permite a un usuario copiar datos ubicados en el documento PDF, especifique `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`. (Repita este paso para cada permiso que desee establecer).
   * Especifique la opción de compatibilidad con Acrobat invocando el método `PasswordEncryptionOptionSpec` del objeto `setCompatability` y pasando un valor de lista desglosada que especifica el nivel de compatibilidad con Acrobat. Por ejemplo, puede especificar `PasswordEncryptionCompatability.ACRO_7`.
   * Especifique el valor de contraseña que permite al usuario abrir el documento PDF cifrado invocando el método `PasswordEncryptionOptionSpec` del objeto `setDocumentOpenPassword` y pasando un valor de cadena que representa la contraseña abierta.
   * Especifique el valor de la contraseña maestra que permite al usuario eliminar el cifrado del documento PDF invocando el método `PasswordEncryptionOptionSpec` del objeto `setPermissionPassword` y pasando un valor de cadena que representa la contraseña maestra.

1. Añada la contraseña.

   Cifre el documento PDF invocando el método `EncryptionServiceClient` del objeto `encryptPDFUsingPassword` y pasando los siguientes valores:

   * El objeto `com.adobe.idp.Document` que contiene el documento PDF que se va a cifrar con la contraseña.
   * El objeto `PasswordEncryptionOptionSpec` que contiene opciones de tiempo de ejecución de cifrado.

   El método `encryptPDFUsingPassword` devuelve un objeto `com.adobe.idp.Document` que contiene un documento PDF con contraseña cifrada.

1. Guarde el documento PDF codificado como archivo PDF.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea .pdf.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del objeto `com.adobe.idp.Document` en el archivo. Asegúrese de utilizar el objeto `com.adobe.idp.Document` devuelto por el método `encryptPDFUsingPassword`.

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
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto de API de cliente de cifrado.

   * Cree un objeto `EncryptionServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `EncryptionServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`). No es necesario usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `EncryptionServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga un documento PDF para cifrar.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar un documento PDF cifrado con una contraseña.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF que se va a cifrar y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando el contenido de la matriz de bytes al miembro de datos `BLOB` del objeto `MTOM`.

1. Configure las opciones de tiempo de ejecución de cifrado.

   * Cree un objeto `PasswordEncryptionOptionSpec` utilizando su constructor.
   * Especifique los recursos de documento PDF que desea cifrar asignando un valor de lista desglosada `PasswordEncryptionOption` al miembro de datos `PasswordEncryptionOptionSpec` del objeto `encryptOption`. Para cifrar todo el PDF, incluidos sus metadatos y sus archivos adjuntos, asigne `PasswordEncryptionOption.ALL` a este miembro de datos.
   * Especifique la opción de compatibilidad con Acrobat asignando un valor de lista desglosada `PasswordEncryptionCompatability` al miembro de datos `PasswordEncryptionOptionSpec` del objeto `compatability`. Por ejemplo, asigne `PasswordEncryptionCompatability.ACRO_7` a este miembro de datos.
   * Especifique el valor de contraseña que permite al usuario abrir el documento PDF cifrado asignando un valor de cadena que representa la contraseña abierta al miembro de datos `PasswordEncryptionOptionSpec` del objeto `documentOpenPassword`.
   * Especifique el valor de la contraseña que permite al usuario eliminar el cifrado del documento PDF asignando un valor de cadena que representa la contraseña maestra al miembro de datos `PasswordEncryptionOptionSpec` del objeto `permissionPassword`.

1. Añada la contraseña.

   Cifre el documento PDF invocando el método `EncryptionServiceClient` del objeto `encryptPDFUsingPassword` y pasando los siguientes valores:

   * El objeto `BLOB` que contiene el documento PDF que se va a cifrar con la contraseña.
   * El objeto `PasswordEncryptionOptionSpec` que contiene opciones de tiempo de ejecución de cifrado.

   El método `encryptPDFUsingPassword` devuelve un objeto `BLOB` que contiene un documento PDF con contraseña cifrada.

1. Guarde el documento PDF codificado como archivo PDF.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF protegido.
   * Cree una matriz de bytes que almacene el contenido de datos del objeto `BLOB` devuelto por el método `encryptPDFUsingPassword`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Codificación de Documentos PDF con certificados {#encrypting-pdf-documents-with-certificates}

El cifrado basado en certificados permite cifrar un documento para destinatarios específicos mediante tecnología de clave pública. Se pueden otorgar diferentes permisos a varios destinatarios para el documento. Muchos aspectos de la encriptación son posibles gracias a la tecnología de claves públicas. Se utiliza un algoritmo para generar dos números grandes, conocidos como *claves*, que tienen las siguientes propiedades:

* Se utiliza una clave para cifrar un conjunto de datos. Posteriormente, sólo se puede utilizar la otra clave para descifrar los datos.
* Es imposible distinguir una clave de la otra.

Una de las claves actúa como clave privada del usuario. Es importante que solo el usuario tenga acceso a esta clave. La otra clave es la clave pública del usuario, que se puede compartir con otros usuarios.

Un certificado de clave pública contiene la clave pública y la información de identificación del usuario. El formato X.509 se utiliza para almacenar certificados. Los certificados suelen ser emitidos y firmados digitalmente por una autoridad de certificación (CA), que es una entidad reconocida que proporciona una medida de confianza en la validez del certificado. Los certificados tienen una fecha de caducidad, tras la cual ya no son válidos. Además, las listas de revocación de certificados (CRL) proporcionan información sobre los certificados revocados antes de su fecha de caducidad. Las listas CRL son publicadas periódicamente por las autoridades de certificación. El estado de revocación de un certificado también se puede recuperar mediante el protocolo de estado de certificado en línea (OCSP) a través de la red.

>[!NOTE]
>
>Si carga un documento PDF cifrado en el repositorio de AEM Forms, no podrá descifrar el documento PDF ni extraer el contenido XDP. Se recomienda no cifrar un documento antes de cargarlo en el repositorio de AEM Forms. (Consulte [Escritura de recursos](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Para poder cifrar un documento PDF con un certificado, debe asegurarse de agregar el certificado a AEM Forms. Se agrega un certificado mediante la consola de administración o mediante programación mediante la API del administrador de confianza. (Consulte [Importación de credenciales mediante la API del administrador de confianza](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)).

>[!NOTE]
>
>Para obtener más información sobre el servicio de cifrado, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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
* adobe-encryption-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss Application Server)

**Creación de un objeto de API de cliente de codificación**

Para realizar una operación de servicio de cifrado mediante programación, debe crear un cliente de servicio de cifrado. Si utiliza la API de servicio de cifrado Java, cree un objeto `EncrytionServiceClient`. Si está utilizando la API de servicio de cifrado de servicio Web, cree un objeto `EncryptionServiceService`.

**Obtener un documento PDF para cifrar**

Debe obtener un documento PDF no cifrado para cifrar. Si intenta proteger un documento PDF que ya está cifrado, se genera una excepción.

**Hacer referencia al certificado**

Para cifrar un documento PDF con un certificado, haga referencia a un certificado que se utilice para cifrar un documento PDF. El certificado es un archivo .cer, un archivo .crt o un archivo .pem. Se utiliza un archivo PKCS#12 para almacenar claves privadas con los certificados correspondientes.

Al cifrar un documento PDF con un certificado, especifique los permisos asociados al documento seguro. Si especifica permisos, puede controlar las acciones que puede realizar un usuario que abre un documento PDF con cifrado de certificado.

**Configurar opciones de tiempo de ejecución de cifrado**

Especifique los recursos de documento PDF que desea cifrar. Puede cifrar todo el documento PDF, todo excepto los metadatos del documento o solo los archivos adjuntos del documento.

**Creación de un documento PDF con cifrado de certificado**

Después de recuperar un documento PDF no seguro, hacer referencia al certificado y definir las opciones en tiempo de ejecución, puede crear un documento PDF con cifrado de certificado. Una vez cifrado el documento PDF, necesita la clave pública correspondiente para descifrarlo.

**Guardar el documento PDF codificado como archivo PDF**

Puede guardar el documento PDF codificado como archivo PDF.

**Consulte también**

[Cifrar un documento PDF con un certificado mediante la API de Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[Cifrar un documento PDF con un certificado mediante la API de servicio Web](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Cifrado de Documentos PDF con contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Cifrar un documento PDF con un certificado mediante la API de Java {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

Cifrar un documento PDF con un certificado mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-encoding-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto de API de cliente de cifrado.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EncryptionServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga un documento PDF para cifrar.

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF que se va a cifrar utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Haga referencia al certificado.

   * Cree un objeto `java.util.List` que almacene información de permisos mediante su constructor.
   * Especifique el permiso asociado con el documento cifrado invocando el método `java.util.List` del objeto `add` y pasando un valor de lista desglosada `CertificateEncryptionPermissions` que represente los permisos concedidos al usuario que abre el documento PDF protegido. Por ejemplo, para especificar todos los permisos, pase `CertificateEncryptionPermissions.PKI_ALL_PERM`.
   * Cree un objeto `Recipient` utilizando su constructor.
   * Cree un objeto `java.io.FileInputStream` que represente el certificado que se utiliza para cifrar el documento PDF utilizando su constructor y pasando un valor de cadena que especifique la ubicación del certificado.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream` que representa el certificado.
   * Invoque el método `Recipient` del objeto `setX509Cert` y pase el objeto `com.adobe.idp.Document` que contiene el certificado. (Además, el objeto `Recipient`puede tener un alias de certificado Truststore o una URL LDAP como origen de certificado).
   * Cree un objeto `CertificateEncryptionIdentity` que almacene información de permisos y certificados mediante su constructor.
   * Invoque el método `CertificateEncryptionIdentity` del objeto `setPerms` y pase el objeto `java.util.List` que almacena información de permisos.
   * Invoque el método `CertificateEncryptionIdentity` del objeto `setRecipient` y pase el objeto `Recipient` que almacena información del certificado.
   * Cree un objeto `java.util.List` que almacene información de certificado mediante su constructor.
   * Invoque el método add del objeto `java.util.List` y pase el objeto `CertificateEncryptionIdentity`. (Este objeto `java.util.List` se pasa como parámetro al método `encryptPDFUsingCertificates`).

1. Configure las opciones de tiempo de ejecución de cifrado.

   * Cree un objeto `CertificateEncryptionOptionSpec` invocando su constructor.
   * Especifique los recursos de documento PDF que desea cifrar invocando el método `CertificateEncryptionOptionSpec` del objeto `setOption` y pasando un valor de lista desglosada `CertificateEncryptionOption` que especifica los recursos de documento que desea cifrar. Por ejemplo, para cifrar todo el documento PDF, incluidos sus metadatos y sus archivos adjuntos, especifique `CertificateEncryptionOption.ALL`.
   * Especifique la opción de compatibilidad con Acrobat invocando el método `CertificateEncryptionOptionSpec` del objeto `setCompat` y pasando un valor de lista desglosada `CertificateEncryptionCompatibility` que especifica el nivel de compatibilidad con Acrobat. Por ejemplo, puede especificar `CertificateEncryptionCompatibility.ACRO_7`.

1. Cree un documento PDF con cifrado de certificado.

   Cifre el documento PDF con un certificado invocando el método `EncryptionServiceClient` del objeto `encryptPDFUsingCertificates` y pasando los siguientes valores:

   * El objeto `com.adobe.idp.Document` que contiene el documento PDF que se va a cifrar.
   * El objeto `java.util.List` que almacena la información del certificado.
   * El objeto `CertificateEncryptionOptionSpec` que contiene opciones de tiempo de ejecución de cifrado.

   El método `encryptPDFUsingCertificates` devuelve un objeto `com.adobe.idp.Document` que contiene un documento PDF con cifrado de certificado.

1. Guarde el documento PDF codificado como archivo PDF.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del nombre de archivo sea .pdf.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del objeto `com.adobe.idp.Document` en el archivo. Asegúrese de utilizar el objeto `com.adobe.idp.Document` devuelto por el método `encryptPDFUsingCertificates`.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Codificación de un documento PDF con un certificado mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Cifrar un documento PDF con un certificado mediante la API de servicio Web {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

Cifre un documento PDF con un certificado mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto de API de cliente de cifrado.

   * Cree un objeto `EncryptionServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `EncryptionServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`). No es necesario usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `EncryptionServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga un documento PDF para cifrar.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar un documento PDF cifrado con un certificado.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF que se va a cifrar y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Haga referencia al certificado.

   * Cree un objeto `Recipient` utilizando su constructor. Este objeto almacenará información de certificado.
   * Cree un objeto `BLOB` utilizando su constructor. Este objeto `BLOB` almacenará el certificado que codifica el documento PDF.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del certificado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando el contenido de la matriz de bytes al miembro de datos `BLOB` del objeto `MTOM`.
   * Asigne el objeto `BLOB` que almacena el certificado al miembro de datos `Recipient` del objeto `x509Cert`.
   * Cree un objeto `CertificateEncryptionIdentity` que almacene información de certificado mediante su constructor.
   * Asigne el objeto `Recipient` que almacena el certificado al miembro de datos de destinatario del objeto `CertificateEncryptionIdentity`.
   * Cree una matriz `Object` y asigne el objeto `CertificateEncryptionIdentity` al primer elemento de la matriz `Object`. Esta matriz `Object` se pasa como parámetro al método `encryptPDFUsingCertificates`.

1. Configure las opciones de tiempo de ejecución de cifrado.

   * Cree un objeto `CertificateEncryptionOptionSpec` utilizando su constructor.
   * Especifique los recursos de documento PDF que desea cifrar asignando un valor de lista desglosada `CertificateEncryptionOption` al miembro de datos `CertificateEncryptionOptionSpec` del objeto `option`. Para cifrar todo el documento PDF, incluidos sus metadatos y sus archivos adjuntos, asigne `CertificateEncryptionOption.ALL` a este miembro de datos.
   * Especifique la opción de compatibilidad con Acrobat asignando un valor de lista desglosada `CertificateEncryptionCompatibility` al miembro de datos `CertificateEncryptionOptionSpec` del objeto `compat`. Por ejemplo, asigne `CertificateEncryptionCompatibility.ACRO_7` a este miembro de datos.

1. Cree un documento PDF con cifrado de certificado.

   Cifre el documento PDF con un certificado invocando el método `EncryptionServiceService` del objeto `encryptPDFUsingCertificates` y pasando los siguientes valores:

   * El objeto `BLOB` que contiene el documento PDF que se va a cifrar.
   * Matriz `Object` que almacena información de certificado.
   * El objeto `CertificateEncryptionOptionSpec` que contiene opciones de tiempo de ejecución de cifrado.

   El método `encryptPDFUsingCertificates` devuelve un objeto `BLOB` que contiene un documento PDF con cifrado de certificado.

1. Guarde el documento PDF codificado como archivo PDF.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF protegido.
   * Cree una matriz de bytes que almacene el contenido de datos del objeto `BLOB` devuelto por el método `encryptPDFUsingCertificates`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `binaryData`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Eliminando Cifrado Basado en Certificado {#removing-certificate-based-encryption}

La codificación basada en certificados se puede eliminar de un documento PDF para que los usuarios puedan abrir el documento PDF en Adobe Reader o Acrobat. Para eliminar la codificación de un documento PDF cifrado con un certificado, se debe hacer referencia a una clave pública. Después de eliminar la codificación de un documento PDF, ya no es segura.

>[!NOTE]
>
>Para obtener más información sobre el servicio de cifrado, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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
* adobe-encryption-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss Application Server)

**Crear un cliente de servicio de cifrado**

Para realizar una operación de servicio de cifrado mediante programación, debe crear un cliente de servicio de cifrado. Si utiliza la API de servicio de cifrado Java, cree un objeto `EncrytionServiceClient`. Si está utilizando la API de servicio de cifrado de servicio Web, cree un objeto `EncryptionServiceService`.

**Obtener el documento PDF cifrado**

Debe obtener un documento PDF cifrado para eliminar el cifrado basado en certificados. Si intenta eliminar la codificación de un documento PDF que no está cifrado, se genera una excepción. Del mismo modo, si intenta eliminar el cifrado basado en certificados de un documento cifrado con contraseña, se genera una excepción.

**Eliminar cifrado**

Para eliminar el cifrado basado en certificados de un documento PDF cifrado, se requiere un documento PDF cifrado y la clave privada que corresponda a la clave utilizada para cifrar el documento PDF. El valor de alias de la clave privada se especifica al eliminar la codificación basada en certificados de un documento PDF cifrado. Para obtener información sobre la clave pública, consulte [Cifrar Documentos PDF con certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).

>[!NOTE]
>
>Una clave privada se almacena en AEM Forms Trust Store. Cuando se coloca un certificado allí, se especifica un valor de alias.

**Guardar el documento PDF**

Una vez que el cifrado basado en certificados se haya eliminado de un documento PDF cifrado, puede guardar el documento PDF como archivo PDF. Los usuarios pueden abrir el documento PDF en Adobe Reader o Acrobat.

**Consulte también**

[Eliminar el cifrado basado en certificados mediante la API de Java](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[Eliminar el cifrado basado en certificados mediante la API de servicio Web](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Eliminar el cifrado basado en certificados mediante la API de Java {#remove-certificate-based-encryption-using-the-java-api}

Elimine el cifrado basado en certificados de un documento PDF mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-encoding-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de servicio de cifrado.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EncryptionServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga el documento PDF cifrado.

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF cifrado mediante su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF cifrado.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Eliminar cifrado.

   Elimine el cifrado basado en certificados del documento PDF invocando el método `EncryptionServiceClient` del objeto `removePDFCertificateSecurity` y pasando los valores siguientes:

   * El objeto `com.adobe.idp.Document` que contiene el documento PDF cifrado.
   * Un valor de cadena que especifica el nombre de alias de la clave privada que corresponde a la clave utilizada para cifrar el documento PDf.

   El método `removePDFCertificateSecurity` devuelve un objeto `com.adobe.idp.Document` que contiene un documento PDF no seguro.

1. Guarde el documento PDF.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea .pdf.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del objeto `Document` en el archivo. Asegúrese de utilizar el objeto `com.adobe.idp.Document` devuelto por el método `removePDFCredentialSecurity`.

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
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de servicio de cifrado.

   * Cree un objeto `EncryptionServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `EncryptionServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`). No es necesario usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `EncryptionServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento PDF cifrado.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el documento PDF cifrado.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF cifrado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando el contenido de la matriz de bytes al miembro de datos `BLOB` del objeto `MTOM`.

1. Eliminar cifrado.

   Invoque el método `EncryptionServiceClient` del objeto `removePDFCertificateSecurity` y pase los siguientes valores:

   * El objeto `BLOB` que contiene datos de flujo de archivos que representan un documento PDF cifrado.
   * Un valor de cadena que especifica el nombre de alias de la clave pública que corresponde a la clave privada utilizada para cifrar el documento PDf.

   El método `removePDFCredentialSecurity` devuelve un objeto `BLOB` que contiene un documento PDF no seguro.

1. Guarde el documento PDF.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF no seguro.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` devuelto por el método `removePDFPasswordSecurity`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Eliminando cifrado de contraseña {#removing-password-encryption}

La codificación basada en contraseña se puede eliminar de un documento PDF para que los usuarios puedan abrir el documento PDF en Adobe Reader o Acrobat sin tener que especificar una contraseña. Una vez que se elimina la codificación basada en contraseña de un documento PDF, el documento ya no es seguro.

>[!NOTE]
>
>Para obtener más información sobre el servicio de cifrado, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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
* adobe-encryption-client.jar
* adobe-utilities.jar (requerido si AEM Forms se implementa en JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss)

**Crear un cliente de servicio de cifrado**

Para realizar una operación de servicio de cifrado mediante programación, debe crear un cliente de servicio de cifrado. Si utiliza la API de servicio de cifrado Java, cree un objeto `EncrytionServiceClient`. Si está utilizando la API de servicio de cifrado de servicio Web, cree un objeto `EncryptionServiceService`.

**Obtener el documento PDF cifrado**

Debe obtener un documento PDF cifrado para eliminar la codificación basada en contraseña. Si intenta eliminar la codificación de un documento PDF que no está cifrado, se genera una excepción.

**Quitar la contraseña**

Para eliminar la codificación basada en contraseña de un documento PDF cifrado, se necesita un documento PDF cifrado y un valor de contraseña maestro que se utilicen para eliminar la codificación del documento PDF. La contraseña que se utiliza para abrir un documento PDF con contraseña cifrada no se puede utilizar para eliminar la codificación. Se especifica una contraseña maestra cuando el documento PDF se cifra con una contraseña. (Consulte [Cifrar Documentos PDF con una contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)).

**Guardar el documento PDF**

Después de que el servicio de cifrado elimine la codificación basada en contraseña de un documento PDF, puede guardar el documento PDF como archivo PDF. Los usuarios pueden abrir el documento PDF en Adobe Reader o Acrobat sin especificar una contraseña.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Cifrado de Documentos PDF con contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Eliminar el cifrado basado en contraseña mediante la API de Java {#remove-password-based-encryption-using-the-java-api}

Elimine la codificación basada en contraseña de un documento PDF mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-encoding-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de servicio de cifrado.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EncryptionServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga el documento PDF cifrado.

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF cifrado mediante su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Quite la contraseña.

   Elimine el cifrado basado en contraseña del documento PDF invocando el método `EncryptionServiceClient` del objeto `removePDFPasswordSecurity` y pasando los valores siguientes:

   * Un objeto `com.adobe.idp.Document` que contiene el documento PDF cifrado.
   * Un valor de cadena que especifica el valor de contraseña principal que se utiliza para eliminar la codificación del documento PDF.

   El método `removePDFPasswordSecurity` devuelve un objeto `com.adobe.idp.Document` que contiene un documento PDF no seguro.

1. Guarde el documento PDF.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del nombre de archivo sea .pdf.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del objeto `Document` en el archivo. Asegúrese de utilizar el objeto `Document` devuelto por el método `removePDFPasswordSecurity`.

**Consulte también**

[Inicio rápido (modo SOAP): Eliminación del cifrado basado en contraseña mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### Eliminar el cifrado basado en contraseña mediante la API de servicio Web {#remove-password-based-encryption-using-the-web-service-api}

Elimine el cifrado basado en contraseña mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de servicio de cifrado.

   * Cree un objeto `EncryptionServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `EncryptionServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`). No es necesario usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `EncryptionServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento PDF cifrado.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar un documento PDF con contraseña cifrada.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF cifrado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando el contenido de la matriz de bytes al miembro de datos `BLOB` del objeto `MTOM`.

1. Quite la contraseña.

   Invoque el método `EncryptionServiceService` del objeto `removePDFPasswordSecurity` y pase los siguientes valores:

   * El objeto `BLOB` que contiene datos de flujo de archivos que representan un documento PDF cifrado.
   * Un valor de cadena que especifica el valor de contraseña que se utiliza para eliminar la codificación del documento PDF. Este valor se especifica al cifrar el documento PDF con una contraseña.

   El método `removePDFPasswordSecurity` devuelve un objeto `BLOB` que contiene un documento PDF no seguro.

1. Guarde el documento PDF.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF no seguro.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` devuelto por el método `removePDFPasswordSecurity`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Desbloqueo de Documentos PDF cifrados {#unlocking-encrypted-pdf-documents}

Un documento PDF con cifrado de contraseña o certificado debe desbloquearse antes de que se pueda realizar otra operación de AEM Forms. Si intenta realizar una operación en un documento PDF cifrado, generará una excepción. Después de desbloquear un documento PDF cifrado, puede realizar una o varias operaciones en él. Estas operaciones pueden pertenecer a otros servicios, como el servicio de extensiones de Acrobat Reader DC.

>[!NOTE]
>
>Para obtener más información sobre el servicio de cifrado, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-4}

Para desbloquear un documento PDF cifrado, realice los siguientes pasos:

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
* adobe-encryption-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss Application Server)

**Crear un cliente de servicio de cifrado**

Para realizar una operación de servicio de cifrado mediante programación, debe crear un cliente de servicio de cifrado. Si utiliza la API de servicio de cifrado Java, cree un objeto `EncrytionServiceClient`. Si está utilizando la API de servicio de cifrado de servicio Web, cree un objeto `EncryptionServiceService`.

**Obtener el documento PDF cifrado**

Debe obtener un documento PDF cifrado para desbloquearlo. Si intenta desbloquear un documento PDF que no está cifrado, se genera una excepción.

**Desbloquear el documento**

Para desbloquear un documento PDF con contraseña cifrada, necesita un documento PDF cifrado y un valor de contraseña que se utilicen para abrir un documento PDF con contraseña cifrada. Este valor se especifica al cifrar el documento PDF con una contraseña. (Consulte [Cifrar Documentos PDF con una contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)).

Para desbloquear un documento PDF con cifrado de certificado, necesita un documento PDF cifrado y el valor de alias de la clave pública correspondiente a la clave privada que se utilizó para cifrar el documento PDF.

**Realizar una operación de AEM Forms**

Después de desbloquear un documento PDF cifrado, puede realizar otra operación de servicio en él, como aplicarle derechos de uso. Esta operación pertenece al servicio Extensiones de Acrobat Reader DC.

**Consulte también**

[Desbloquear un documento PDF cifrado mediante la API de Java](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[Desbloquear un documento PDF cifrado mediante la API de servicio web](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Desbloquear un documento PDF cifrado mediante la API de Java {#unlock-an-encrypted-pdf-document-using-the-java-api}

Desbloquear un documento PDF cifrado mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-encoding-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de servicio de cifrado.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EncryptionServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga el documento PDF cifrado.

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF cifrado mediante su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF cifrado.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Desbloquee el documento.

   Desbloquee un documento PDF cifrado invocando el método `EncryptionServiceClient` o `unlockPDFUsingCredential` del objeto `unlockPDFUsingPassword`.

   Para desbloquear un documento PDF codificado con una contraseña, invoque el método `unlockPDFUsingPassword` y pase los valores siguientes:

   * Un objeto `com.adobe.idp.Document` que contiene el documento PDF con contraseña cifrada.
   * Un valor de cadena que especifica el valor de contraseña que se utiliza para abrir un documento PDF con contraseña cifrada. Este valor se especifica al cifrar el documento PDF con una contraseña.

   Para desbloquear un documento PDF cifrado con un certificado, invoque el método `unlockPDFUsingCredential` y pase los valores siguientes:

   * Un objeto `com.adobe.idp.Document` que contiene el documento PDF con cifrado de certificado.
   * Un valor de cadena que especifica el nombre de alias de la clave pública que corresponde a la clave privada utilizada para cifrar el documento PDF.

   Los métodos `unlockPDFUsingPassword` y `unlockPDFUsingCredential` devuelven un objeto `com.adobe.idp.Document` que pasa a otro método Java de AEM Forms para realizar una operación.

1. Realice una operación de AEM Forms.

   Realice una operación de AEM Forms en el documento PDF desbloqueado para cumplir los requisitos comerciales. Por ejemplo, suponiendo que desea aplicar derechos de uso a un documento PDF desbloqueado, pase el objeto `com.adobe.idp.Document` devuelto por los métodos `unlockPDFUsingPassword` o `unlockPDFUsingCredential` al método `ReaderExtensionsServiceClient` del objeto `applyUsageRights`.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Desbloqueo de un documento PDF cifrado mediante la API](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api)  de Java (modo SOAP)

[Aplicación de derechos de uso a Documentos PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Desbloquear un documento PDF cifrado mediante la API de servicio Web {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

Desbloquear un documento PDF cifrado mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de servicio de cifrado.

   * Cree un objeto `EncryptionServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `EncryptionServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`). No es necesario usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `EncryptionServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga un documento PDF cifrado.

   * Cree un objeto `BLOB` utilizando su constructor.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF cifrado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando el contenido de la matriz de bytes al miembro de datos `BLOB` del objeto `MTOM`.

1. Desbloquee el documento.

   Desbloquee un documento PDF cifrado invocando el método `EncryptionServiceClient` o `unlockPDFUsingCredential` del objeto `unlockPDFUsingPassword`.

   Para desbloquear un documento PDF codificado con una contraseña, invoque el método `unlockPDFUsingPassword` y pase los valores siguientes:

   * Un objeto `BLOB` que contiene el documento PDF con contraseña cifrada.
   * Un valor de cadena que especifica el valor de contraseña que se utiliza para abrir un documento PDF con contraseña cifrada. Este valor se especifica al cifrar el documento PDF con una contraseña.

   Para desbloquear un documento PDF cifrado con un certificado, invoque el método `unlockPDFUsingCredential` y pase los valores siguientes:

   * Un objeto `BLOB` que contiene el documento PDF con cifrado de certificado.
   * Un valor de cadena que especifica el nombre de alias de la clave pública que corresponde a la clave privada utilizada para cifrar el documento PDf.

   Los métodos `unlockPDFUsingPassword` y `unlockPDFUsingCredential` devuelven un objeto `com.adobe.idp.Document` que pasa a otro método de AEM Forms para realizar una operación.

1. Realice una operación de AEM Forms.

   Realice una operación de AEM Forms en el documento PDF desbloqueado para cumplir los requisitos comerciales. Por ejemplo, suponiendo que desea aplicar derechos de uso al documento PDF desbloqueado, pase el objeto `BLOB` devuelto por los métodos `unlockPDFUsingPassword` o `unlockPDFUsingCredential` al método `ReaderExtensionsServiceClient` del objeto `applyUsageRights`.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Determinación del tipo de cifrado {#determining-encryption-type}

Puede determinar mediante programación el tipo de codificación que protege un documento PDF mediante la API de servicio de cifrado de Java o la API de servicio de cifrado de servicio Web. A veces es necesario determinar dinámicamente si un documento PDF está cifrado y, en caso afirmativo, el tipo de codificación. Por ejemplo, puede determinar si un documento PDF está protegido con codificación basada en contraseña o con una política de Rights Management.

Un documento PDF puede protegerse mediante los siguientes tipos de codificación:

* Cifrado basado en contraseña
* Cifrado basado en certificados
* Directiva creada por el servicio Rights Management
* Otro tipo de cifrado

>[!NOTE]
>
>Para obtener más información sobre el servicio de cifrado, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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
* adobe-encryption-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss Application Server)

**Crear un cliente de servicio**

Para realizar una operación de servicio de cifrado mediante programación, debe crear un cliente de servicio de cifrado. Si utiliza la API de servicio de cifrado Java, cree un objeto `EncrytionServiceClient`. Si está utilizando la API de servicio de cifrado de servicio Web, cree un objeto `EncryptionServiceService`.

**Obtener el documento PDF cifrado**

Debe obtener un documento PDF para determinar el tipo de codificación que la protege.

**Determinar el tipo de codificación**

Puede determinar el tipo de codificación que protege un documento PDF. Si el documento PDF no está protegido, el servicio Cifrado le informa de que el documento PDF no está seguro.

**Consulte también**

[Determinar el tipo de codificación mediante la API de Java](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[Determinar el tipo de codificación mediante la API de servicio Web](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Protección de Documentos con políticas](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### Determinar el tipo de codificación mediante la API de Java {#determine-the-encryption-type-using-the-java-api}

Determine el tipo de codificación que protege un documento PDF mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-encoding-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de servicio.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EncryptionServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga el documento PDF cifrado.

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Determine el tipo de codificación.

   * Determine el tipo de codificación invocando el método `EncryptionServiceClient` del objeto `getPDFEncryption` y pasando el objeto `com.adobe.idp.Document` que contiene el documento PDF. Este método devuelve un objeto `EncryptionTypeResult`.
   * Invocar el método `EncryptionTypeResult` del objeto `getEncryptionType`. Este método devuelve un valor de enumeración `EncryptionType` que especifica el tipo de codificación. Por ejemplo, si el documento PDF está protegido con cifrado basado en contraseña, este método devuelve `EncryptionType.PASSWORD`.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Determinación del tipo de codificación mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinar el tipo de cifrado mediante la API de servicio Web {#determine-the-encryption-type-using-the-web-service-api}

Determine el tipo de codificación que protege un documento PDF mediante la API de cifrado (servicio Web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de servicio.

   * Cree un objeto `EncryptionServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `EncryptionServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`). No es necesario usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `EncryptionServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento PDF cifrado.

   * Cree un objeto `BLOB` utilizando su constructor.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF cifrado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando el contenido de la matriz de bytes al miembro de datos `BLOB` del objeto `MTOM`.

1. Determine el tipo de codificación.

   * Invoque el método `EncryptionServiceClient` del objeto `getPDFEncryption` y pase el objeto `BLOB` que contiene el documento PDF. Este método devuelve un objeto `EncryptionTypeResult`.
   * Obtenga el valor del método de datos `EncryptionTypeResult` del objeto `encryptionType`. Por ejemplo, si el documento PDF está protegido con cifrado basado en contraseña, el valor de este miembro de datos es `EncryptionType.PASSWORD`.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)