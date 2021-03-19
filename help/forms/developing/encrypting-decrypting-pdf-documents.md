---
title: Codificación y descifrado de documentos PDF
seo-title: Codificación y descifrado de documentos PDF
description: Utilice el servicio de cifrado para cifrar y descifrar documentos. Las tareas del servicio de codificación incluyen la codificación de un documento PDF con contraseña, la codificación de un documento PDF con un certificado, la eliminación del cifrado basado en contraseña de un documento PDF, la eliminación del cifrado basado en certificado de un documento PDF, la desbloqueo del documento PDF para que se puedan realizar otras operaciones del servicio y la determinación del tipo de cifrado de un documento PDF protegido.
seo-description: Utilice el servicio de cifrado para cifrar y descifrar documentos. Las tareas del servicio de codificación incluyen la codificación de un documento PDF con contraseña, la codificación de un documento PDF con un certificado, la eliminación del cifrado basado en contraseña de un documento PDF, la eliminación del cifrado basado en certificado de un documento PDF, la desbloqueo del documento PDF para que se puedan realizar otras operaciones del servicio y la determinación del tipo de cifrado de un documento PDF protegido.
uuid: 4e4e2716-c21f-4bfe-ae7a-7e91442414ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 5e4bda3a-5648-4c0f-b2f8-bdbebb88f537
role: Desarrollador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '8259'
ht-degree: 0%

---


# Codificación y descifrado de documentos PDF {#encrypting-and-decrypting-pdf-documents}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

**Acerca del servicio de cifrado**

El servicio Encryption permite cifrar y descifrar documentos. Cuando se cifra un documento, su contenido se vuelve ilegible. Un usuario autorizado puede descifrar el documento para obtener acceso al contenido. Si un documento PDF está cifrado con una contraseña, el usuario debe especificar la contraseña de apertura antes de que el documento se pueda ver en Adobe Reader o Adobe Acrobat. Del mismo modo, si un documento PDF está cifrado con un certificado, el usuario debe descifrar el documento PDF con la clave pública correspondiente al certificado (clave privada) que se utilizó para codificar el documento PDF.

Puede realizar estas tareas mediante el servicio de cifrado:

* Codificar un documento PDF con una contraseña. (Consulte [Codificación de documentos PDF con una contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)).
* Codificar un documento PDF con un certificado. (Consulte [Codificación de documentos PDF con certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)).
* Elimine el cifrado basado en contraseña de un documento PDF. (Consulte [Eliminación del cifrado de contraseña](encrypting-decrypting-pdf-documents.md#removing-password-encryption)).
* Elimine el cifrado basado en certificados de un documento PDF. (Consulte [Eliminación del cifrado basado en certificados](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption)).
* Desbloquee el documento PDF para que se puedan realizar otras operaciones de servicio. Por ejemplo, después de desbloquear un documento PDF con contraseña cifrada, puede aplicarle una firma digital. (Consulte [Desbloqueo de documentos PDF cifrados](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents)).
* Determine el tipo de cifrado de un documento PDF protegido. (Consulte [Determinación del tipo de codificación](encrypting-decrypting-pdf-documents.md#determining-encryption-type)).

>[!NOTE]
>
>Para obtener más información sobre el servicio de cifrado, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Codificación de documentos PDF con una contraseña {#encrypting-pdf-documents-with-a-password}

Cuando se cifra un documento PDF con contraseña, el usuario debe especificar la contraseña para abrir el documento PDF en Adobe Reader o Acrobat. Además, antes de que se pueda realizar otra operación de AEM Forms, como firmar digitalmente el documento PDF, un documento PDF con contraseña cifrada debe desbloquearse.

>[!NOTE]
>
>Si carga un documento PDF cifrado en el repositorio de AEM Forms, no podrá descifrar el documento PDF ni extraer el contenido XDP. Se recomienda no cifrar un documento antes de cargarlo en el repositorio de AEM Forms. (Consulte [Escritura de recursos](/help/forms/developing/aem-forms-repository.md#writing-resources)).

>[!NOTE]
>
>Para obtener más información sobre el servicio de cifrado, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para codificar un documento PDF con una contraseña, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de cifrado.
1. Obtenga un documento PDF para cifrar.
1. Establezca las opciones de tiempo de ejecución del cifrado.
1. Agregue la contraseña.
1. Guarde el documento PDF cifrado como archivo PDF.

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

**Obtener un documento PDF para codificar**

Debe obtener un documento PDF sin encriptar para codificar el documento con una contraseña. Si intenta proteger un documento PDF que ya está cifrado, provocará una excepción.

**Establecer opciones de tiempo de ejecución de cifrado**

Para codificar un documento PDF con contraseña, debe especificar cuatro valores, incluidos dos valores de contraseña. El primer valor de contraseña se utiliza para codificar el documento PDF y debe especificarse al abrir el documento PDF. El segundo valor de contraseña, denominado el valor de la contraseña maestra, se utiliza para eliminar el cifrado del documento PDF. Los valores de contraseña distinguen entre mayúsculas y minúsculas y estos dos valores de contraseña no pueden ser los mismos.

Debe especificar los recursos del documento PDF que desea codificar. Puede cifrar todo el documento PDF, todo menos los metadatos del documento o solo los archivos adjuntos del documento. Si sólo cifra los archivos adjuntos del documento, se solicita al usuario una contraseña cuando intente acceder a los archivos adjuntos.

Al cifrar un documento PDF, puede especificar los permisos asociados al documento protegido. Si especifica permisos, puede controlar las acciones que puede realizar un usuario que abre un documento PDF con contraseña cifrada. Por ejemplo, para extraer correctamente los datos del formulario, debe definir los siguientes permisos:

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>Los permisos se especifican como valores de enumeración `PasswordEncryptionPermission`.

**Agregar la contraseña**

Después de recuperar un documento PDF no protegido y establecer valores de tiempo de ejecución de cifrado, puede agregar una contraseña al documento PDF.

**Guardar el documento PDF cifrado como un archivo PDF**

Puede guardar el documento PDF cifrado con contraseña como un archivo PDF.

**Consulte también**

[Codificación de un documento PDF mediante la API de Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[Codificación de un documento PDF mediante la API de servicio Web](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Codificación de documentos PDF con certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### Codificar un documento PDF utilizando la API de Java {#encrypt-a-pdf-document-using-the-java-api}

Cifrar un documento PDF con una contraseña utilizando la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-encryption-client.jar, en la ruta de clase de su proyecto Java.

1. Cree una API de cliente de cifrado.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EncryptionServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga un documento PDF para cifrar.

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF que va a codificar utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Establezca las opciones de tiempo de ejecución del cifrado.

   * Cree un objeto `PasswordEncryptionOptionSpec` invocando su constructor.
   * Especifique los recursos del documento PDF que desea cifrar invocando el método `PasswordEncryptionOptionSpec` del objeto `setEncryptOption` y pasando un valor de enumeración `PasswordEncryptionOption` que especifica los recursos del documento que se van a cifrar. Por ejemplo, para cifrar todo el documento PDF, incluidos sus metadatos y sus archivos adjuntos, especifique `PasswordEncryptionOption.ALL`.
   * Cree un objeto `java.util.List` que almacene los permisos de codificación utilizando el constructor `ArrayList`.
   * Especifique un permiso invocando el método `java.util.List` del objeto ‘s `add` y pasando un valor de enumeración que corresponda al permiso que desea establecer. Por ejemplo, para establecer el permiso que permite a un usuario copiar datos ubicados en el documento PDF, especifique `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`. (Repita este paso para cada permiso que desee establecer).
   * Especifique la opción de compatibilidad con Acrobat invocando el método `PasswordEncryptionOptionSpec` del objeto `setCompatability` y pasando un valor de enumeración que especifica el nivel de compatibilidad con Acrobat. Por ejemplo, puede especificar `PasswordEncryptionCompatability.ACRO_7`.
   * Especifique el valor de la contraseña que permite a un usuario abrir el documento PDF cifrado invocando el método `PasswordEncryptionOptionSpec` del objeto `setDocumentOpenPassword` y pasando un valor de cadena que representa la contraseña abierta.
   * Especifique el valor de la contraseña maestra que permite al usuario eliminar el cifrado del documento PDF invocando el método `PasswordEncryptionOptionSpec` del objeto `setPermissionPassword` y pasando un valor de cadena que represente la contraseña maestra.

1. Agregue la contraseña.

   Codifique el documento PDF invocando el método `EncryptionServiceClient` del objeto `encryptPDFUsingPassword` y pasando los siguientes valores:

   * El objeto `com.adobe.idp.Document` que contiene el documento PDF que se va a codificar con la contraseña.
   * El objeto `PasswordEncryptionOptionSpec` que contiene opciones de tiempo de ejecución de cifrado.

   El método `encryptPDFUsingPassword` devuelve un objeto `com.adobe.idp.Document` que contiene un documento PDF con contraseña cifrada.

1. Guarde el documento PDF cifrado como archivo PDF.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea .pdf.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del objeto `com.adobe.idp.Document` en el archivo. Asegúrese de utilizar el objeto `com.adobe.idp.Document` que el método `encryptPDFUsingPassword` devolvió.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Codificación de un documento PDF mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Codificación de un documento PDF mediante la API de servicio Web {#encrypting-a-pdf-document-using-the-web-service-api}

Cifre un documento PDF con una contraseña utilizando la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto de API de cliente de cifrado.

   * Cree un objeto `EncryptionServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `EncryptionServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `EncryptionServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga un documento PDF para cifrar.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar un documento PDF cifrado con una contraseña.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF que desea cifrar y el modo en que desea abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición de inicio y la longitud de flujo para leer.
   * Rellene el objeto `BLOB` asignando el contenido de la matriz de bytes al miembro de datos `MTOM` del objeto `BLOB`.

1. Establezca las opciones de tiempo de ejecución del cifrado.

   * Cree un objeto `PasswordEncryptionOptionSpec` utilizando su constructor.
   * Especifique los recursos del documento PDF que desea codificar asignando un valor de enumeración `PasswordEncryptionOption` al miembro de datos `PasswordEncryptionOptionSpec` del objeto `encryptOption`. Para cifrar todo el PDF, incluidos sus metadatos y sus archivos adjuntos, asigne `PasswordEncryptionOption.ALL` a este miembro de datos.
   * Especifique la opción de compatibilidad con Acrobat asignando un valor de enumeración `PasswordEncryptionCompatability` al miembro de datos `PasswordEncryptionOptionSpec` del objeto `compatability`. Por ejemplo, asigne `PasswordEncryptionCompatability.ACRO_7` a este miembro de datos.
   * Especifique el valor de la contraseña que permite a un usuario abrir el documento PDF cifrado asignando un valor de cadena que represente la contraseña de apertura al miembro de datos `PasswordEncryptionOptionSpec` del objeto `documentOpenPassword`.
   * Especifique el valor de la contraseña que permite al usuario eliminar el cifrado del documento PDF asignando un valor de cadena que representa la contraseña maestra al miembro de datos `PasswordEncryptionOptionSpec` del objeto `permissionPassword`.

1. Agregue la contraseña.

   Codifique el documento PDF invocando el método `EncryptionServiceClient` del objeto `encryptPDFUsingPassword` y pasando los siguientes valores:

   * El objeto `BLOB` que contiene el documento PDF que se va a codificar con la contraseña.
   * El objeto `PasswordEncryptionOptionSpec` que contiene opciones de tiempo de ejecución de cifrado.

   El método `encryptPDFUsingPassword` devuelve un objeto `BLOB` que contiene un documento PDF con contraseña cifrada.

1. Guarde el documento PDF cifrado como archivo PDF.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF protegido.
   * Cree una matriz de bytes que almacene el contenido de datos del objeto `BLOB` que el método `encryptPDFUsingPassword` devolvió. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Codificación de documentos PDF con certificados {#encrypting-pdf-documents-with-certificates}

El cifrado basado en certificados permite cifrar un documento para destinatarios específicos mediante tecnología de clave pública. Se pueden otorgar a varios destinatarios diferentes permisos para el documento. Muchos aspectos del cifrado son posibles gracias a la tecnología de claves públicas. Un algoritmo se utiliza para generar dos números grandes, conocidos como *keys*, que tienen las siguientes propiedades:

* Se utiliza una clave para cifrar un conjunto de datos. Posteriormente, solo se puede utilizar la otra clave para descifrar los datos.
* Es imposible distinguir una clave de la otra.

Una de las claves actúa como clave privada de un usuario. Es importante que solo el usuario tenga acceso a esta clave. La otra clave es la clave pública del usuario, que se puede compartir con otros usuarios.

Un certificado de clave pública contiene la clave pública y la información de identificación del usuario. El formato X.509 se utiliza para almacenar certificados. Los certificados suelen ser emitidos y firmados digitalmente por una autoridad de certificación (CA), que es una entidad reconocida que proporciona una medida de confianza en la validez del certificado. Los certificados tienen una fecha de caducidad tras la cual ya no son válidos. Además, las listas de revocación de certificados (CRL) proporcionan información sobre los certificados revocados antes de su fecha de caducidad. Las listas CRL se publican periódicamente por las autoridades certificadoras. El estado de revocación de un certificado también se puede recuperar mediante el Protocolo de estado de certificado en línea (OCSP) a través de la red.

>[!NOTE]
>
>Si carga un documento PDF cifrado en el repositorio de AEM Forms, no podrá descifrar el documento PDF ni extraer el contenido XDP. Se recomienda no cifrar un documento antes de cargarlo en el repositorio de AEM Forms. (Consulte [Escritura de recursos](/help/forms/developing/aem-forms-repository.md#writing-resources)).

>[!NOTE]
>
>Para poder cifrar un documento PDF con un certificado, debe asegurarse de agregar el certificado a AEM Forms. Se agrega un certificado mediante la consola de administración o mediante programación mediante la API del administrador de confianza. (Consulte [Importación de credenciales mediante la API del administrador de confianza](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)).

>[!NOTE]
>
>Para obtener más información sobre el servicio de cifrado, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para codificar un documento PDF con un certificado, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de cifrado.
1. Obtenga un documento PDF para cifrar.
1. Haga referencia al certificado.
1. Establezca las opciones de tiempo de ejecución del cifrado.
1. Cree un documento PDF con cifrado de certificado.
1. Guarde el documento PDF cifrado como archivo PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

**Creación de un objeto de API de cliente de cifrado**

Para realizar una operación de servicio de cifrado mediante programación, debe crear un cliente de servicio de cifrado. Si utiliza la API del servicio de cifrado de Java, cree un objeto `EncrytionServiceClient`. Si utiliza la API del servicio de cifrado de servicio web, cree un objeto `EncryptionServiceService`.

**Obtener un documento PDF para codificar**

Debe obtener un documento PDF no cifrado para codificarlo. Si intenta proteger un documento PDF que ya está cifrado, se genera una excepción.

**Referencia al certificado**

Para codificar un documento PDF con un certificado, haga referencia a un certificado que se utilice para codificar un documento PDF. El certificado es un archivo .cer, un archivo .crt o un archivo .pem. Se utiliza un archivo PKCS#12 para almacenar claves privadas con los certificados correspondientes.

Al cifrar un documento PDF con un certificado, especifique los permisos asociados al documento protegido. Si especifica permisos, puede controlar las acciones que puede realizar un usuario que abra un documento PDF cifrado con certificado.

**Establecer opciones de tiempo de ejecución de cifrado**

Especifique los recursos del documento PDF que desea codificar. Puede cifrar todo el documento PDF, todo menos los metadatos del documento o solo los archivos adjuntos del documento.

**Creación de un documento PDF cifrado por certificado**

Después de recuperar un documento PDF no protegido, hacer referencia al certificado y establecer las opciones de tiempo de ejecución, puede crear un documento PDF cifrado con certificado. Una vez cifrado el documento PDF, se necesita la clave pública correspondiente para descifrarlo.

**Guardar el documento PDF cifrado como un archivo PDF**

Puede guardar el documento PDF cifrado como un archivo PDF.

**Consulte también**

[Codificación de un documento PDF con un certificado mediante la API de Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[Codificación de un documento PDF con un certificado mediante la API de servicio web](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Codificación de documentos PDF con contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Codificar un documento PDF con un certificado utilizando la API de Java {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

Cifrar un documento PDF con un certificado mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-encryption-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un objeto de API de cliente de cifrado.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EncryptionServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga un documento PDF para cifrar.

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF que va a codificar utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Haga referencia al certificado.

   * Cree un objeto `java.util.List` que almacene información de permisos usando su constructor.
   * Especifique el permiso asociado al documento cifrado invocando el método `java.util.List` del objeto `add` y pasando un valor de enumeración `CertificateEncryptionPermissions` que representa los permisos otorgados al usuario que abre el documento PDF protegido. Por ejemplo, para especificar todos los permisos, pase `CertificateEncryptionPermissions.PKI_ALL_PERM`.
   * Cree un objeto `Recipient` utilizando su constructor.
   * Cree un objeto `java.io.FileInputStream` que represente el certificado que se utiliza para cifrar el documento PDF utilizando su constructor y pasando un valor de cadena que especifique la ubicación del certificado.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream` que representa el certificado.
   * Invoque el método `Recipient` del objeto `setX509Cert` y pase el objeto `com.adobe.idp.Document` que contiene el certificado. (Además, el objeto `Recipient`puede tener un alias de certificado Truststore o una URL LDAP como origen de certificado).
   * Cree un objeto `CertificateEncryptionIdentity` que almacene información de permisos y certificados usando su constructor.
   * Invoque el método `CertificateEncryptionIdentity` del objeto `setPerms` y pase el objeto `java.util.List` que almacena la información de permisos.
   * Invoque el método `CertificateEncryptionIdentity` del objeto `setRecipient` y pase el objeto `Recipient` que almacena la información del certificado.
   * Cree un objeto `java.util.List` que almacene información de certificado usando su constructor.
   * Invoque el método add del objeto `java.util.List` y pase el objeto `CertificateEncryptionIdentity`. (Este objeto `java.util.List` se pasa como parámetro al método `encryptPDFUsingCertificates`).

1. Establezca las opciones de tiempo de ejecución del cifrado.

   * Cree un objeto `CertificateEncryptionOptionSpec` invocando su constructor.
   * Especifique los recursos del documento PDF que desea cifrar invocando el método `CertificateEncryptionOptionSpec` del objeto `setOption` y pasando un valor de enumeración `CertificateEncryptionOption` que especifica los recursos del documento que se van a cifrar. Por ejemplo, para cifrar todo el documento PDF, incluidos sus metadatos y sus archivos adjuntos, especifique `CertificateEncryptionOption.ALL`.
   * Especifique la opción de compatibilidad con Acrobat invocando el método `CertificateEncryptionOptionSpec` del objeto `setCompat` y pasando un valor de enumeración `CertificateEncryptionCompatibility` que especifica el nivel de compatibilidad con Acrobat. Por ejemplo, puede especificar `CertificateEncryptionCompatibility.ACRO_7`.

1. Cree un documento PDF con cifrado de certificado.

   Codifique el documento PDF con un certificado invocando el método `EncryptionServiceClient` del objeto `encryptPDFUsingCertificates` y pasando los siguientes valores:

   * El objeto `com.adobe.idp.Document` que contiene el documento PDF que se va a codificar.
   * El objeto `java.util.List` que almacena información del certificado.
   * El objeto `CertificateEncryptionOptionSpec` que contiene opciones de tiempo de ejecución de cifrado.

   El método `encryptPDFUsingCertificates` devuelve un objeto `com.adobe.idp.Document` que contiene un documento PDF cifrado por certificado.

1. Guarde el documento PDF cifrado como archivo PDF.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del nombre del archivo sea .pdf.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del objeto `com.adobe.idp.Document` en el archivo. Asegúrese de utilizar el objeto `com.adobe.idp.Document` que el método `encryptPDFUsingCertificates` devolvió.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Codificación de un documento PDF con un certificado mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Codificar un documento PDF con un certificado mediante la API de servicio Web {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

Codificar un documento PDF con un certificado mediante la API de codificación (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto de API de cliente de cifrado.

   * Cree un objeto `EncryptionServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `EncryptionServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `EncryptionServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga un documento PDF para cifrar.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar un documento PDF cifrado con un certificado.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF que desea cifrar y el modo en que desea abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición de inicio y la longitud de flujo para leer.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Haga referencia al certificado.

   * Cree un objeto `Recipient` utilizando su constructor. Este objeto almacenará información de certificado.
   * Cree un objeto `BLOB` utilizando su constructor. Este objeto `BLOB` almacenará el certificado que codifica el documento PDF.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del certificado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición de inicio y la longitud de flujo para leer.
   * Rellene el objeto `BLOB` asignando el contenido de la matriz de bytes al miembro de datos `MTOM` del objeto `BLOB`.
   * Asigne el objeto `BLOB` que almacena el certificado al miembro de datos `Recipient` del objeto `x509Cert`.
   * Cree un objeto `CertificateEncryptionIdentity` que almacene información de certificado usando su constructor.
   * Asigne el objeto `Recipient` que almacena el certificado al miembro de datos del destinatario del objeto `CertificateEncryptionIdentity`.
   * Cree una matriz `Object` y asigne el objeto `CertificateEncryptionIdentity` al primer elemento de la matriz `Object`. Esta matriz `Object` se pasa como parámetro al método `encryptPDFUsingCertificates`.

1. Establezca las opciones de tiempo de ejecución del cifrado.

   * Cree un objeto `CertificateEncryptionOptionSpec` utilizando su constructor.
   * Especifique los recursos del documento PDF que desea codificar asignando un valor de enumeración `CertificateEncryptionOption` al miembro de datos `CertificateEncryptionOptionSpec` del objeto `option`. Para cifrar todo el documento PDF, incluidos sus metadatos y sus archivos adjuntos, asigne `CertificateEncryptionOption.ALL` a este miembro de datos.
   * Especifique la opción de compatibilidad con Acrobat asignando un valor de enumeración `CertificateEncryptionCompatibility` al miembro de datos `CertificateEncryptionOptionSpec` del objeto `compat`. Por ejemplo, asigne `CertificateEncryptionCompatibility.ACRO_7` a este miembro de datos.

1. Cree un documento PDF con cifrado de certificado.

   Codifique el documento PDF con un certificado invocando el método `EncryptionServiceService` del objeto `encryptPDFUsingCertificates` y pasando los siguientes valores:

   * El objeto `BLOB` que contiene el documento PDF que se va a codificar.
   * La matriz `Object` que almacena información de certificado.
   * El objeto `CertificateEncryptionOptionSpec` que contiene opciones de tiempo de ejecución de cifrado.

   El método `encryptPDFUsingCertificates` devuelve un objeto `BLOB` que contiene un documento PDF cifrado por certificado.

1. Guarde el documento PDF cifrado como archivo PDF.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF protegido.
   * Cree una matriz de bytes que almacene el contenido de datos del objeto `BLOB` que el método `encryptPDFUsingCertificates` devolvió. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `binaryData`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Eliminación del cifrado basado en certificados {#removing-certificate-based-encryption}

El cifrado basado en certificados se puede eliminar de un documento PDF para que los usuarios puedan abrir el documento PDF en Adobe Reader o Acrobat. Para eliminar el cifrado de un documento PDF cifrado con un certificado, se debe hacer referencia a una clave pública. Una vez eliminado el cifrado de un documento PDF, ya no es seguro.

>[!NOTE]
>
>Para obtener más información sobre el servicio de cifrado, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-2}

Para eliminar el cifrado basado en certificados de un documento PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de cifrado.
1. Obtenga el documento PDF cifrado.
1. Elimine el cifrado.
1. Guarde el documento PDF como archivo PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

**Crear un cliente de servicio de cifrado**

Para realizar una operación de servicio de cifrado mediante programación, debe crear un cliente de servicio de cifrado. Si utiliza la API del servicio de cifrado de Java, cree un objeto `EncrytionServiceClient`. Si utiliza la API del servicio de cifrado de servicio web, cree un objeto `EncryptionServiceService`.

**Obtener el documento PDF cifrado**

Debe obtener un documento PDF cifrado para eliminar el cifrado basado en certificados. Si intenta eliminar el cifrado de un documento PDF que no está cifrado, se genera una excepción. Del mismo modo, si intenta eliminar el cifrado basado en certificados de un documento cifrado con contraseña, se genera una excepción.

**Eliminar cifrado**

Para eliminar el cifrado basado en certificados de un documento PDF cifrado, se requiere un documento PDF cifrado y la clave privada que corresponda a la clave utilizada para codificar el documento PDF. El valor de alias de la clave privada se especifica al quitar el cifrado basado en certificado de un documento PDF cifrado. Para obtener información sobre la clave pública, consulte [Codificación de documentos PDF con certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).

>[!NOTE]
>
>Se almacena una clave privada en el almacén de confianza de AEM Forms. Cuando se coloca un certificado allí, se especifica un valor de alias.

**Guardar el documento PDF**

Una vez eliminado el cifrado basado en certificados de un documento PDF cifrado, puede guardar el documento PDF como archivo PDF. Los usuarios pueden abrir el documento PDF en Adobe Reader o Acrobat.

**Consulte también**

[Eliminación del cifrado basado en certificados mediante la API de Java](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[Eliminación del cifrado basado en certificados mediante la API de servicio web](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Eliminar el cifrado basado en certificados mediante la API de Java {#remove-certificate-based-encryption-using-the-java-api}

Elimine el cifrado basado en certificados de un documento PDF mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-encryption-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente de servicio de cifrado.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EncryptionServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga el documento PDF cifrado.

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF cifrado empleando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF cifrado.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Elimine el cifrado.

   Elimine el cifrado basado en certificados del documento PDF invocando el método `EncryptionServiceClient` del objeto `removePDFCertificateSecurity` y pasando los siguientes valores:

   * El objeto `com.adobe.idp.Document` que contiene el documento PDF cifrado.
   * Un valor de cadena que especifica el nombre de alias de la clave privada que corresponde a la clave utilizada para cifrar el documento PDf.

   El método `removePDFCertificateSecurity` devuelve un objeto `com.adobe.idp.Document` que contiene un documento PDF no protegido.

1. Guarde el documento PDF.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea .pdf.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del objeto `Document` en el archivo. Asegúrese de utilizar el objeto `com.adobe.idp.Document` que el método `removePDFCredentialSecurity` devolvió.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Eliminación del cifrado basado en certificados mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminar el cifrado basado en certificados mediante la API de servicio web {#remove-certificate-based-encryption-using-the-web-service-api}

Elimine el cifrado basado en certificados mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de servicio de cifrado.

   * Cree un objeto `EncryptionServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `EncryptionServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `EncryptionServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
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
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición de inicio y la longitud de flujo para leer.
   * Rellene el objeto `BLOB` asignando el contenido de la matriz de bytes al miembro de datos `MTOM` del objeto `BLOB`.

1. Elimine el cifrado.

   Invoque el método `EncryptionServiceClient` del objeto `removePDFCertificateSecurity` y pase los siguientes valores:

   * El objeto `BLOB` que contiene datos de flujo de archivos que representan un documento PDF cifrado.
   * Un valor de cadena que especifica el nombre de alias de la clave pública que corresponde a la clave privada utilizada para cifrar el documento PDf.

   El método `removePDFCredentialSecurity` devuelve un objeto `BLOB` que contiene un documento PDF no protegido.

1. Guarde el documento PDF.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF no protegido.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` que el método `removePDFPasswordSecurity` devolvió. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Eliminación del cifrado de contraseña {#removing-password-encryption}

El cifrado basado en contraseña se puede eliminar de un documento PDF para que los usuarios puedan abrir el documento PDF en Adobe Reader o Acrobat sin tener que especificar una contraseña. Después de eliminar el cifrado basado en contraseña de un documento PDF, el documento ya no es seguro.

>[!NOTE]
>
>Para obtener más información sobre el servicio de cifrado, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-3}

Para eliminar el cifrado basado en contraseña de un documento PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto
1. Cree un cliente de servicio de cifrado.
1. Obtenga el documento PDF cifrado.
1. Elimine la contraseña.
1. Guarde el documento PDF como archivo PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

**Crear un cliente de servicio de cifrado**

Para realizar una operación de servicio de cifrado mediante programación, debe crear un cliente de servicio de cifrado. Si utiliza la API del servicio de cifrado de Java, cree un objeto `EncrytionServiceClient`. Si utiliza la API del servicio de cifrado de servicio web, cree un objeto `EncryptionServiceService`.

**Obtener el documento PDF cifrado**

Debe obtener un documento PDF cifrado para eliminar el cifrado basado en contraseña. Si intenta eliminar el cifrado de un documento PDF que no está cifrado, se genera una excepción.

**Quitar la contraseña**

Para eliminar el cifrado basado en contraseña de un documento PDF cifrado, se requiere un documento PDF cifrado y un valor de contraseña principal que se utilicen para eliminar el cifrado del documento PDF. La contraseña utilizada para abrir un documento PDF con contraseña cifrada no se puede utilizar para eliminar el cifrado. Se especifica una contraseña maestra cuando el documento PDF está cifrado con una contraseña. (Consulte [Codificación de documentos PDF con una contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)).

**Guardar el documento PDF**

Una vez que el servicio de cifrado elimina el cifrado basado en contraseña de un documento PDF, puede guardar el documento PDF como archivo PDF. Los usuarios pueden abrir el documento PDF en Adobe Reader o Acrobat sin especificar una contraseña.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Codificación de documentos PDF con contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Eliminar el cifrado basado en contraseña mediante la API de Java {#remove-password-based-encryption-using-the-java-api}

Elimine el cifrado basado en contraseña de un documento PDF mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-encryption-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente de servicio de cifrado.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EncryptionServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga el documento PDF cifrado.

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF cifrado empleando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Elimine la contraseña.

   Elimine el cifrado basado en contraseña del documento PDF invocando el método `EncryptionServiceClient` del objeto `removePDFPasswordSecurity` y pasando los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que contiene el documento PDF cifrado.
   * Un valor de cadena que especifica el valor de la contraseña maestra que se utiliza para eliminar el cifrado del documento PDF.

   El método `removePDFPasswordSecurity` devuelve un objeto `com.adobe.idp.Document` que contiene un documento PDF no protegido.

1. Guarde el documento PDF.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del nombre del archivo sea .pdf.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del objeto `Document` en el archivo. Asegúrese de utilizar el objeto `Document` que el método `removePDFPasswordSecurity` devolvió.

**Consulte también**

[Inicio rápido (modo SOAP): Eliminación del cifrado basado en contraseña mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### Eliminar el cifrado basado en contraseña mediante la API de servicio web {#remove-password-based-encryption-using-the-web-service-api}

Elimine el cifrado basado en contraseña mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de servicio de cifrado.

   * Cree un objeto `EncryptionServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `EncryptionServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `EncryptionServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento PDF cifrado.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar un documento PDF cifrado con contraseña.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF cifrado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición de inicio y la longitud de flujo para leer.
   * Rellene el objeto `BLOB` asignando el contenido de la matriz de bytes al miembro de datos `MTOM` del objeto `BLOB`.

1. Elimine la contraseña.

   Invoque el método `EncryptionServiceService` del objeto `removePDFPasswordSecurity` y pase los siguientes valores:

   * El objeto `BLOB` que contiene datos de flujo de archivos que representan un documento PDF cifrado.
   * Un valor de cadena que especifica el valor de contraseña que se utiliza para eliminar el cifrado del documento PDF. Este valor se especifica al codificar el documento PDF con una contraseña.

   El método `removePDFPasswordSecurity` devuelve un objeto `BLOB` que contiene un documento PDF no protegido.

1. Guarde el documento PDF.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF no protegido.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` que el método `removePDFPasswordSecurity` devolvió. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Desbloquear documentos PDF cifrados {#unlocking-encrypted-pdf-documents}

Un documento PDF cifrado con contraseña o con cifrado de certificado debe desbloquearse antes de poder realizar otra operación de AEM Forms en él. Si intenta realizar una operación en un documento PDF cifrado, generará una excepción. Después de desbloquear un documento PDF cifrado, puede realizar una o más operaciones en él. Estas operaciones pueden pertenecer a otros servicios, como el servicio de extensiones de Acrobat Reader DC.

>[!NOTE]
>
>Para obtener más información sobre el servicio de cifrado, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-4}

Para desbloquear un documento PDF cifrado, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de cifrado.
1. Obtenga el documento PDF cifrado.
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

Para realizar una operación de servicio de cifrado mediante programación, debe crear un cliente de servicio de cifrado. Si utiliza la API del servicio de cifrado de Java, cree un objeto `EncrytionServiceClient`. Si utiliza la API del servicio de cifrado de servicio web, cree un objeto `EncryptionServiceService`.

**Obtener el documento PDF cifrado**

Debe obtener un documento PDF cifrado para desbloquearlo. Si intenta desbloquear un documento PDF que no está cifrado, se genera una excepción.

**Desbloquear el documento**

Para desbloquear un documento PDF con contraseña cifrada, se requiere un documento PDF cifrado y un valor de contraseña que se utilicen para abrir un documento PDF con contraseña cifrada. Este valor se especifica al codificar el documento PDF con una contraseña. (Consulte [Codificación de documentos PDF con una contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)).

Para desbloquear un documento PDF con cifrado de certificado, se requiere un documento PDF cifrado y el valor de alias de la clave pública correspondiente a la clave privada que se utilizó para codificar el documento PDF.

**Realizar una operación de AEM Forms**

Una vez desbloqueado un documento PDF cifrado, puede realizar otra operación de servicio, como aplicarle derechos de uso. Esta operación pertenece al servicio Acrobat Reader DC Extensions.

**Consulte también**

[Desbloquear un documento PDF cifrado mediante la API de Java](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[Desbloquear un documento PDF cifrado mediante la API de servicio Web](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Desbloquear un documento PDF cifrado mediante la API de Java {#unlock-an-encrypted-pdf-document-using-the-java-api}

Desbloquee un documento PDF cifrado mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-encryption-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente de servicio de cifrado.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EncryptionServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga el documento PDF cifrado.

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF cifrado empleando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF cifrado.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Desbloquee el documento.

   Desbloquee un documento PDF cifrado invocando el método `EncryptionServiceClient` o `unlockPDFUsingCredential` del objeto `unlockPDFUsingPassword`.

   Para desbloquear un documento PDF cifrado con una contraseña, invoque el método `unlockPDFUsingPassword` y pase los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que contiene el documento PDF cifrado con contraseña.
   * Valor de cadena que especifica el valor de contraseña que se utiliza para abrir un documento PDF con contraseña cifrada. Este valor se especifica al codificar el documento PDF con una contraseña.

   Para desbloquear un documento PDF cifrado con un certificado, invoque el método `unlockPDFUsingCredential` y pase los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que contiene el documento PDF cifrado con certificado.
   * Un valor de cadena que especifica el nombre de alias de la clave pública que corresponde a la clave privada utilizada para cifrar el documento PDF.

   Los métodos `unlockPDFUsingPassword` y `unlockPDFUsingCredential` devuelven un objeto `com.adobe.idp.Document` que se pasa a otro método Java de AEM Forms para realizar una operación.

1. Realice una operación AEM Forms.

   Realice una operación de AEM Forms en el documento PDF desbloqueado para satisfacer los requisitos empresariales. Por ejemplo, suponiendo que desea aplicar derechos de uso a un documento PDF desbloqueado, pase el objeto `com.adobe.idp.Document` que devolvieron los métodos `unlockPDFUsingPassword` o `unlockPDFUsingCredential` al método `ReaderExtensionsServiceClient` del objeto `applyUsageRights`.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Desbloqueo de un documento PDF cifrado mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api)  (modo SOAP)

[Aplicación de derechos de uso a documentos PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Desbloquear un documento PDF cifrado mediante la API de servicio Web {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

Desbloquee un documento PDF cifrado mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de servicio de cifrado.

   * Cree un objeto `EncryptionServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `EncryptionServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `EncryptionServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
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
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición de inicio y la longitud de flujo para leer.
   * Rellene el objeto `BLOB` asignando el contenido de la matriz de bytes al miembro de datos `MTOM` del objeto `BLOB`.

1. Desbloquee el documento.

   Desbloquee un documento PDF cifrado invocando el método `EncryptionServiceClient` o `unlockPDFUsingCredential` del objeto `unlockPDFUsingPassword`.

   Para desbloquear un documento PDF cifrado con una contraseña, invoque el método `unlockPDFUsingPassword` y pase los siguientes valores:

   * Un objeto `BLOB` que contiene el documento PDF cifrado con contraseña.
   * Valor de cadena que especifica el valor de contraseña que se utiliza para abrir un documento PDF con contraseña cifrada. Este valor se especifica al codificar el documento PDF con una contraseña.

   Para desbloquear un documento PDF cifrado con un certificado, invoque el método `unlockPDFUsingCredential` y pase los siguientes valores:

   * Un objeto `BLOB` que contiene el documento PDF cifrado con certificado.
   * Un valor de cadena que especifica el nombre de alias de la clave pública que corresponde a la clave privada utilizada para cifrar el documento PDf.

   Los métodos `unlockPDFUsingPassword` y `unlockPDFUsingCredential` devuelven un objeto `com.adobe.idp.Document` que se pasa a otro método de AEM Forms para realizar una operación.

1. Realice una operación AEM Forms.

   Realice una operación de AEM Forms en el documento PDF desbloqueado para satisfacer los requisitos empresariales. Por ejemplo, suponiendo que desea aplicar derechos de uso al documento PDF desbloqueado, pase el objeto `BLOB` que devolvieron los métodos `unlockPDFUsingPassword` o `unlockPDFUsingCredential` al método `ReaderExtensionsServiceClient` del objeto `applyUsageRights`.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Determinación del tipo de cifrado {#determining-encryption-type}

Puede determinar mediante programación el tipo de cifrado que protege un documento PDF mediante la API del servicio de cifrado de Java o la API del servicio de cifrado de servicio Web. A veces es necesario determinar dinámicamente si un documento PDF está cifrado y, en caso afirmativo, el tipo de codificación. Por ejemplo, puede determinar si un documento PDF está protegido con cifrado basado en contraseña o con una directiva de Rights Management.

Un documento PDF puede estar protegido por los siguientes tipos de codificación:

* Cifrado basado en contraseña
* Cifrado basado en certificados
* Una directiva que crea el servicio de Rights Management
* Otro tipo de cifrado

>[!NOTE]
>
>Para obtener más información sobre el servicio de cifrado, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-5}

Para determinar el tipo de cifrado que protege un documento PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de cifrado.
1. Obtenga el documento PDF cifrado.
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

Para realizar una operación de servicio de cifrado mediante programación, debe crear un cliente de servicio de cifrado. Si utiliza la API del servicio de cifrado de Java, cree un objeto `EncrytionServiceClient`. Si utiliza la API del servicio de cifrado de servicio web, cree un objeto `EncryptionServiceService`.

**Obtener el documento PDF cifrado**

Debe obtener un documento PDF para determinar el tipo de cifrado que lo protege.

**Determinar el tipo de codificación**

Puede determinar el tipo de codificación que protege un documento PDF. Si el documento PDF no está protegido, el servicio Encryption le informa de que el documento PDF no está protegido.

**Consulte también**

[Determinar el tipo de cifrado mediante la API de Java](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[Determinar el tipo de cifrado mediante la API de servicio web](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Protección de documentos con directivas](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### Determine el tipo de cifrado mediante la API de Java {#determine-the-encryption-type-using-the-java-api}

Determine el tipo de cifrado que protege un documento PDF mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-encryption-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente de servicio.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EncryptionServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga el documento PDF cifrado.

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Determine el tipo de cifrado.

   * Determine el tipo de cifrado invocando el método `EncryptionServiceClient` del objeto `getPDFEncryption` y pasando el objeto `com.adobe.idp.Document` que contiene el documento PDF. Este método devuelve un objeto `EncryptionTypeResult`.
   * Invoque el método `EncryptionTypeResult` del objeto `getEncryptionType`. Este método devuelve un valor de enumeración `EncryptionType` que especifica el tipo de cifrado. Por ejemplo, si el documento PDF está protegido con cifrado basado en contraseña, este método devuelve `EncryptionType.PASSWORD`.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Determinación del tipo de cifrado mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinar el tipo de cifrado mediante la API de servicio web {#determine-the-encryption-type-using-the-web-service-api}

Determine el tipo de cifrado que protege un documento PDF mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de servicio.

   * Cree un objeto `EncryptionServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `EncryptionServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `EncryptionServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
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
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición de inicio y la longitud de flujo para leer.
   * Rellene el objeto `BLOB` asignando el contenido de la matriz de bytes al miembro de datos `MTOM` del objeto `BLOB`.

1. Determine el tipo de cifrado.

   * Invoque el método `EncryptionServiceClient` del objeto `getPDFEncryption` y pase el objeto `BLOB` que contiene el documento PDF. Este método devuelve un objeto `EncryptionTypeResult`.
   * Obtenga el valor del método de datos `EncryptionTypeResult` del objeto `encryptionType`. Por ejemplo, si el documento PDF está protegido con cifrado basado en contraseña, el valor de este miembro de datos es `EncryptionType.PASSWORD`.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)