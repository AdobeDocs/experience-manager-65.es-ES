---
title: Uso de credenciales
seo-title: Working with Credentials
description: Importe credenciales en AEM Forms mediante la API de administrador de confianza y la API de Java. Además, aprenda a eliminar credenciales mediante la API de administrador de confianza y la API de Java.
seo-description: Import credentials into AEM Forms using the Trust Manager API and Java API. In addition, learn how to delete credentials using the Trust Manager API and Java API.
uuid: b794428f-49bf-4a91-bc5f-d855881f4f38
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: bc06d9bd-af6c-47b1-b46f-aab990ef5816
role: Developer
exl-id: 1101c85a-6a90-471d-a7be-8d25765e84bf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 0%

---

# Uso de credenciales {#working-with-credentials}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

**Acerca del servicio Credencial**

Las credenciales contienen la información de clave privada necesaria para firmar o identificar documentos. Un certificado es información de clave pública que se configura para la confianza. AEM Forms utiliza certificados y credenciales para varios fines:

* Las extensiones de Acrobat Reader DC utilizan una credencial para habilitar los derechos de uso de Adobe Reader en documentos de PDF. (Consulte [Aplicación de derechos de uso a documentos de PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).)
* El servicio de firma accede a certificados y credenciales mientras realiza operaciones como la firma digital de documentos de PDF. (Consulte [Firma digital de documentos PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

Puede interactuar mediante programación con el servicio Credential mediante la API Java de Trust Manager. Puede realizar las siguientes tareas:

* [Importación de credenciales mediante la API del administrador de confianza](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [Eliminación de credenciales mediante la API del administrador de confianza](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>También puede importar y eliminar certificados mediante la consola de administración. (Consulte [ayuda de administración.](https://www.adobe.com/go/learn_aemforms_admin_63))

## Importación de credenciales mediante la API del administrador de confianza {#importing-credentials-by-using-the-trust-manager-api}

Puede importar mediante programación una credencial a AEM Forms mediante la API del administrador de confianza. Por ejemplo, se puede importar una credencial utilizada para firmar un documento de PDF. (Consulte [Firma digital de documentos PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)).

Al importar una credencial, se especifica un alias para la credencial. El alias se utiliza para realizar una operación de Forms que requiere credenciales. Una vez importadas, las credenciales se pueden ver en la consola de administración, como se muestra en la siguiente ilustración. Observe que el alias de la credencial es *Secure*.

![ww_ww_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>No puede importar credenciales en AEM Forms mediante servicios web.

### Resumen de los pasos {#summary-of-steps}

Para importar una credencial en AEM Forms, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de credenciales.
1. Haga referencia a las credenciales.
1. Realice la operación de importación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de servicio de credenciales**

Antes de poder importar mediante programación una credencial en AEM Forms, cree un cliente de servicio de credenciales. Para obtener más información, consulte [Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Hacer referencia a la credencial**

Haga referencia a una credencial que desee importar en AEM Forms. El inicio rápido asociado con esta sección hace referencia a un archivo P12 ubicado en el sistema de archivos.

**Realizar la operación de importación**

Después de hacer referencia a las credenciales, importe las credenciales en AEM Forms. Si la credencial no se importa correctamente, se genera una excepción. Al importar una credencial, se especifica un alias para la credencial.

**Consulte también lo siguiente**

[Importar credenciales mediante la API de Java](credentials.md#import-credentials-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de credenciales](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[Eliminación de credenciales mediante la API del administrador de confianza](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### Importar credenciales mediante la API de Java {#import-credentials-using-the-java-api}

Importe una credencial en AEM Forms mediante la API del administrador de confianza (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-truststore-client.jar, en la ruta de clase de su proyecto Java.

1. Crear un cliente de servicio de credenciales

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `CredentialServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Hacer referencia a la credencial

   * Cree un `java.io.FileInputStream` usando su constructor. Pase un valor de cadena que especifique la ubicación de la credencial.
   * Cree un `com.adobe.idp.Document` objeto que almacena la credencial utilizando la variable `com.adobe.idp.Document` constructor. Pase el `java.io.FileInputStream` objeto que contiene la credencial al constructor.

1. Realizar la operación de importación

   * Cree una matriz de cadenas que contenga un elemento. Asignar el valor `truststore.usage.type.sign` al elemento .
   * Invocar el `CredentialServiceClient` del objeto `importCredential` y pase los siguientes valores:

      * Un valor de cadena que especifica el valor de alias de la credencial.
      * La variable `com.adobe.idp.Document` instancia que almacena las credenciales.
      * Un valor de cadena que especifica la contraseña asociada a la credencial.
      * La matriz de cadenas que contiene el valor de uso. Por ejemplo, puede especificar este valor `truststore.usage.type.sign`. Para importar una credencial de extensión de Reader, especifique `truststore.usage.type.lcre`.

**Consulte también lo siguiente**

[Importación de credenciales mediante la API del administrador de confianza](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[Inicio rápido (modo SOAP): Importación de credenciales mediante la API de Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Eliminación de credenciales mediante la API del administrador de confianza {#deleting-credentials-by-using-the-trust-manager-api}

Puede eliminar una credencial mediante programación mediante la API del administrador de confianza. Al eliminar una credencial, se especifica un alias que corresponde a la credencial. Una vez eliminada, no se puede utilizar una credencial para realizar una operación.

>[!NOTE]
>
>No puede eliminar una credencial en AEM Forms mediante servicios web.

### Resumen de los pasos {#summary_of_steps-1}

Para eliminar una credencial, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de credenciales.
1. Realice la operación de eliminación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de servicio de credenciales**

Antes de poder eliminar mediante programación una credencial, cree un cliente de servicio de integración de datos. Al crear un cliente de servicio, define la configuración de conexión necesaria para invocar un servicio. Para obtener más información, consulte [Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Realizar la operación de eliminación**

Para eliminar una credencial, especifique el alias que corresponda a la credencial. Si especifica un alias que no existe, se genera una excepción.

**Consulte también lo siguiente**

[Importar credenciales mediante la API de Java](credentials.md#import-credentials-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Importar credenciales mediante la API de Java](credentials.md#import-credentials-using-the-java-api)

### Eliminación de credenciales mediante la API de Java {#deleting-credentials-using-the-java-api}

Elimine una credencial de AEM Forms mediante la API del administrador de confianza (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-truststore-client.jar, en la ruta de clase de su proyecto Java.

1. Crear un cliente de servicio de credenciales

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `CredentialServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Realizar la operación de eliminación

   Invocar el `CredentialServiceClient` del objeto `deleteCredential` y pasa un valor de cadena que especifica el valor de alias.

**Consulte también lo siguiente**

[Eliminación de credenciales mediante la API del administrador de confianza](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[Inicio rápido (modo SOAP): Eliminación de credenciales mediante la API de Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
