---
title: Trabajar con credenciales
seo-title: Working with Credentials
description: Importe credenciales en AEM Forms mediante la API de Trust Manager y la API de Java. Además, aprenda a eliminar credenciales mediante la API de Trust Manager y la API de Java.
seo-description: Import credentials into AEM Forms using the Trust Manager API and Java API. In addition, learn how to delete credentials using the Trust Manager API and Java API.
uuid: b794428f-49bf-4a91-bc5f-d855881f4f38
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: bc06d9bd-af6c-47b1-b46f-aab990ef5816
role: Developer
exl-id: 1101c85a-6a90-471d-a7be-8d25765e84bf
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 1%

---

# Trabajar con credenciales {#working-with-credentials}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

**Acerca del servicio de credenciales**

Una credencial contiene la información de clave privada necesaria para firmar o identificar documentos. Un certificado es información de clave pública que se configura para la confianza. AEM Forms utiliza certificados y credenciales para varios fines:

* Las extensiones de Acrobat Reader DC utilizan una credencial para habilitar los derechos de uso de Adobe Reader en documentos de PDF. (Consulte [Aplicar derechos de uso a documentos de PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).)
* El servicio Signature accede a los certificados y las credenciales mientras realiza operaciones como firmar digitalmente documentos de PDF. (Consulte [Firma digital de documentos de PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

Puede interactuar mediante programación con el servicio de credenciales mediante la API de Java de Administrador de confianza. Puede realizar las siguientes tareas:

* [Importación de credenciales mediante la API de Trust Manager](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [Eliminación de credenciales mediante la API de Administrador de confianza](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>También puede importar y eliminar certificados mediante la consola de administración. (Consulte [ayuda de administración.](https://www.adobe.com/go/learn_aemforms_admin_63_es))

## Importación de credenciales mediante la API de Trust Manager {#importing-credentials-by-using-the-trust-manager-api}

Puede importar mediante programación una credencial en AEM Forms mediante la API de Administrador de confianza. Por ejemplo, puede importar una credencial utilizada para firmar un documento de PDF. (Consulte [Firma digital de documentos de PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)).

Al importar una credencial, se especifica un alias para la credencial. El alias se utiliza para realizar una operación de Forms que requiere credenciales. Una vez importadas, las credenciales se pueden ver en la consola de administración, como se muestra en la siguiente ilustración. Observe que el alias de la credencial es *Secure*.

![ww_ww_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>No puede importar una credencial en AEM Forms mediante servicios web.

### Resumen de los pasos {#summary-of-steps}

Para importar una credencial en AEM Forms, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de credenciales.
1. Haga referencia a la credencial.
1. Realice la operación de importación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben añadirse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de servicio de credenciales**

Para poder importar mediante programación una credencial en AEM Forms, cree un cliente de servicio de credenciales. Para obtener más información, consulte [Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Hacer referencia a la credencial**

Haga referencia a una credencial que desee importar en AEM Forms. El inicio rápido asociado a esta sección hace referencia a un archivo P12 en el sistema de archivos.

**Realice la operación de importación**

Después de hacer referencia a la credencial, impórtela a AEM Forms. Si la credencial no se importa correctamente, se produce una excepción. Al importar una credencial, se especifica un alias para la credencial.

**Consulte también**

[Importar credenciales mediante la API de Java](credentials.md#import-credentials-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de API de servicio de credenciales](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[Eliminación de credenciales mediante la API de Administrador de confianza](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### Importar credenciales mediante la API de Java {#import-credentials-using-the-java-api}

Importe una credencial en AEM Forms mediante la API de Trust Manager (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-truststore-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente de servicio de credenciales

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `CredentialServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Hacer referencia a la credencial

   * Crear un `java.io.FileInputStream` mediante su constructor. Pase un valor de cadena que especifique la ubicación de la credencial.
   * Crear un `com.adobe.idp.Document` que almacena la credencial utilizando el objeto `com.adobe.idp.Document` constructor. Pase el `java.io.FileInputStream` que contiene la credencial al constructor.

1. Realice la operación de importación

   * Cree una matriz de cadenas que contenga un elemento. Asignar el valor `truststore.usage.type.sign` al elemento.
   * Invoque el `CredentialServiceClient` del objeto `importCredential` y pasar los siguientes valores:

      * Valor de cadena que especifica el valor de alias de la credencial.
      * El `com.adobe.idp.Document` instancia que almacena las credenciales.
      * Valor de cadena que especifica la contraseña asociada a la credencial.
      * Matriz de cadenas que contiene el valor de uso. Por ejemplo, puede especificar este valor `truststore.usage.type.sign`. Para importar una credencial de extensión de Reader, especifique `truststore.usage.type.lcre`.

**Consulte también**

[Importación de credenciales mediante la API de Trust Manager](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[Inicio rápido (modo SOAP): Importación de credenciales mediante la API de Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Eliminación de credenciales mediante la API de Administrador de confianza {#deleting-credentials-by-using-the-trust-manager-api}

Puede eliminar una credencial mediante programación utilizando la API de Administrador de confianza. Al eliminar una credencial, debe especificar un alias que corresponda a la credencial. Una vez eliminada, no se puede utilizar una credencial para realizar una operación.

>[!NOTE]
>
>No puede eliminar una credencial en AEM Forms mediante servicios web.

### Resumen de los pasos {#summary_of_steps-1}

Para eliminar una credencial, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de credenciales.
1. Realice la operación de eliminación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Los siguientes archivos JAR deben añadirse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de servicio de credenciales**

Para poder eliminar una credencial mediante programación, cree un cliente del servicio de integración de datos. Al crear un cliente de servicios, define la configuración de conexión necesaria para invocar un servicio. Para obtener más información, consulte [Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Realice la operación de eliminación**

Para eliminar una credencial, especifique el alias que corresponda a la credencial. Si especifica un alias que no existe, se produce una excepción.

**Consulte también**

[Importar credenciales mediante la API de Java](credentials.md#import-credentials-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Importar credenciales mediante la API de Java](credentials.md#import-credentials-using-the-java-api)

### Eliminación de credenciales mediante la API de Java {#deleting-credentials-using-the-java-api}

Eliminar una credencial de AEM Forms mediante la API de Administrador de confianza (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-truststore-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente de servicio de credenciales

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `CredentialServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Realice la operación de eliminación

   Invoque el `CredentialServiceClient` del objeto `deleteCredential` y pasan un valor de cadena que especifica el valor del alias.

**Consulte también**

[Eliminación de credenciales mediante la API de Administrador de confianza](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[Inicio rápido (modo SOAP): Eliminación de credenciales mediante la API de Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
