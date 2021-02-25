---
title: Trabajar con credenciales
seo-title: Trabajar con credenciales
description: Importar credenciales a AEM Forms mediante la API de administrador de confianza y la API de Java. Además, aprenda a eliminar credenciales mediante la API del administrador de confianza y la API de Java.
seo-description: Importar credenciales a AEM Forms mediante la API de administrador de confianza y la API de Java. Además, aprenda a eliminar credenciales mediante la API del administrador de confianza y la API de Java.
uuid: b794428f-49bf-4a91-bc5f-d855881f4f38
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: bc06d9bd-af6c-47b1-b46f-aab990ef5816
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 0%

---


# Trabajar con credenciales {#working-with-credentials}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en el entorno JEE.**

**Acerca del servicio de credenciales**

Las credenciales contienen la información de clave privada necesaria para firmar o identificar documentos. Un certificado es información de clave pública que se configura para la confianza. AEM Forms utiliza certificados y credenciales para varios fines:

* Las extensiones de Acrobat Reader DC utilizan una credencial para habilitar los derechos de uso de Adobe Reader en documentos PDF. (Consulte [Aplicación de derechos de uso a Documentos PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)).
* El servicio Signature accede a los certificados y las credenciales mientras realiza operaciones como la firma digital de documentos PDF. (Consulte [Firma digital de Documentos PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)).

Puede interactuar mediante programación con el servicio de credenciales mediante la API de Java del Administrador de confianza. Puede realizar las siguientes tareas:

* [Importación de credenciales mediante la API del Administrador de confianza](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [Eliminación de credenciales mediante la API del Administrador de confianza](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>También puede importar y eliminar certificados mediante la consola de administración. (Consulte [ayuda de administración.](https://www.adobe.com/go/learn_aemforms_admin_63))

## Importación de credenciales mediante la API del Administrador de confianza {#importing-credentials-by-using-the-trust-manager-api}

Puede importar mediante programación una credencial a AEM Forms mediante la API del administrador de confianza. Por ejemplo, puede importar las credenciales utilizadas para firmar un documento PDF. (Consulte [Firma digital de Documentos PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)).

Al importar una credencial, se especifica un alias para la credencial. El alias se utiliza para realizar una operación de Forms que requiere una credencial. Una vez importadas, las credenciales se pueden ver en la consola de administración, como se muestra en la siguiente ilustración. Observe que el alias de la credencial es *Secure*.

![ww_ww_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>No puede importar una credencial en AEM Forms mediante servicios Web.

### Resumen de los pasos {#summary-of-steps}

Para importar una credencial a AEM Forms, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de credenciales.
1. Haga referencia a las credenciales.
1. Realice la operación de importación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de servicio de credenciales**

Antes de poder importar mediante programación una credencial en AEM Forms, cree un cliente de servicio de credenciales. Para obtener más información, consulte [Configuración de propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Hacer referencia a las credenciales**

Haga referencia a una credencial que desee importar en AEM Forms. El inicio rápido asociado con esta sección hace referencia a un archivo P12 ubicado en el sistema de archivos.

**Realizar la operación de importación**

Después de hacer referencia a las credenciales, importe las credenciales en AEM Forms. Si la credencial no se importa correctamente, se genera una excepción. Al importar una credencial, se especifica un alias para la credencial.

**Consulte también**

[Importar credenciales mediante la API de Java](credentials.md#import-credentials-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API del servicio de credenciales](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[Eliminación de credenciales mediante la API del Administrador de confianza](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### Importar credenciales mediante la API de Java {#import-credentials-using-the-java-api}

Importe una credencial en AEM Forms mediante la API del Administrador de confianza (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-trust-store.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente de servicio de credenciales

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `CredentialServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Hacer referencia a las credenciales

   * Cree un objeto `java.io.FileInputStream` utilizando su constructor. Pase un valor de cadena que especifique la ubicación de la credencial.
   * Cree un objeto `com.adobe.idp.Document` que almacene las credenciales mediante el constructor `com.adobe.idp.Document`. Pase el objeto `java.io.FileInputStream` que contiene la credencial al constructor.

1. Realizar la operación de importación

   * Cree una matriz de cadenas que contenga un elemento. Asigne el valor `truststore.usage.type.sign` al elemento.
   * Invoque el método `CredentialServiceClient` del objeto `importCredential` y pase los siguientes valores:

      * Un valor de cadena que especifica el valor de alias de la credencial.
      * La instancia `com.adobe.idp.Document` que almacena las credenciales.
      * Un valor de cadena que especifica la contraseña asociada a la credencial.
      * Matriz de cadenas que contiene el valor de uso. Por ejemplo, puede especificar este valor `truststore.usage.type.sign`. Para importar una credencial de extensión de Reader, especifique `truststore.usage.type.lcre`.

**Consulte también**

[Importación de credenciales mediante la API del Administrador de confianza](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[Inicio rápido (modo SOAP): Importación de credenciales mediante la API de Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Eliminación de credenciales mediante la API del Administrador de confianza {#deleting-credentials-by-using-the-trust-manager-api}

Puede eliminar mediante programación una credencial mediante la API del Administrador de confianza. Al eliminar una credencial, se especifica un alias que corresponde a la credencial. Una vez eliminadas, las credenciales no se pueden utilizar para realizar una operación.

>[!NOTE]
>
>No puede eliminar una credencial en AEM Forms mediante servicios Web.

### Resumen de los pasos {#summary_of_steps-1}

Para eliminar una credencial, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de credenciales.
1. Realice la operación de eliminación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de servicio de credenciales**

Antes de poder eliminar mediante programación una credencial, cree un cliente del servicio de integración de datos. Al crear un cliente de servicio, se define la configuración de conexión necesaria para invocar un servicio. Para obtener más información, consulte [Configuración de propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Realizar la operación de eliminación**

Para eliminar una credencial, especifique el alias que corresponde a la credencial. Si especifica un alias que no existe, se genera una excepción.

**Consulte también**

[Importar credenciales mediante la API de Java](credentials.md#import-credentials-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Importar credenciales mediante la API de Java](credentials.md#import-credentials-using-the-java-api)

### Eliminación de credenciales mediante la API de Java {#deleting-credentials-using-the-java-api}

Elimine una credencial de AEM Forms mediante la API del Administrador de confianza (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-trust-store.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente de servicio de credenciales

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `CredentialServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Realizar la operación de eliminación

   Invoque el método `CredentialServiceClient` del objeto `deleteCredential` y pase un valor de cadena que especifique el valor de alias.

**Consulte también**

[Eliminación de credenciales mediante la API del Administrador de confianza](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[Inicio rápido (modo SOAP): Eliminación de credenciales mediante la API de Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
