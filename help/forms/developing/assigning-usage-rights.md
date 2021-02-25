---
title: Asignación de derechos de uso
seo-title: Asignación de derechos de uso
description: Utilice la API de Java Client y la API de servicio Web de extensiones de Acrobat Reader DC para aplicar y quitar derechos de uso de documentos PDF.
seo-description: Utilice la API de Java Client y la API de servicio Web de extensiones de Acrobat Reader DC para aplicar y quitar derechos de uso de documentos PDF.
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '3951'
ht-degree: 0%

---


# Asignación de derechos de uso {#assigning-usage-rights}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en el entorno JEE.**

## Acerca del servicio de extensiones de Acrobat Reader DC {#about-the-acrobat-reader-dc-extensions-service}

El servicio de extensiones de Acrobat Reader DC permite a su organización compartir fácilmente documentos PDF interactivos mediante la ampliación de la funcionalidad de Adobe Reader. El servicio de extensiones de Acrobat Reader DC es totalmente compatible con cualquier documento PDF, hasta PDF 1.7 inclusive. Funciona con Adobe Reader 7.0 y posterior. El servicio agrega derechos de uso a un documento PDF, activando funciones que normalmente no están disponibles cuando se abre un documento PDF con Adobe Reader. Los usuarios de terceros no requieren software o complementos adicionales para trabajar con los documentos habilitados para derechos.

Puede realizar estas tareas mediante el servicio de extensiones de Acrobat Reader DC:

* Aplicar derechos de uso a documentos PDF. Para obtener más información, consulte [Aplicación de derechos de uso a Documentos PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).
* Elimine los derechos de uso de los documentos PDF. Para obtener más información, consulte [Eliminación de derechos de uso de Documentos PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).
* Recuperar detalles de credenciales. Para obtener más información, consulte [Recuperación de información de credenciales](assigning-usage-rights.md#retrieving-credential-information).

>[!NOTE]
>
>Para obtener más información sobre el servicio de extensiones de Acrobat Reader DC, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Aplicación de derechos de uso a Documentos PDF {#applying-usage-rights-to-pdf-documents}

Puede aplicar derechos de uso a documentos PDF mediante las extensiones de Acrobat Reader DC, la API de Java Client y el servicio Web. Los derechos de uso se refieren a la funcionalidad que está disponible de forma predeterminada en Acrobat pero no en Adobe Reader, como la capacidad de agregar comentarios a un formulario o de rellenar los campos del formulario y guardar el formulario. Los documentos PDF que tienen derechos de uso aplicados se denominan documentos habilitados para derechos. Un usuario que abre un documento con derechos activados en Adobe Reader puede realizar operaciones habilitadas para ese documento específico.

>[!NOTE]
>
>Al aplicar derechos de uso a documentos PDF mediante el método `applyUsageRights`, que forma parte de la API de Java, puede establecer el parámetro `isModeFinal` del objeto `ReaderExtensionsOptionSpec` en `false`. Esto hace que el contador procesado de formularios no se actualice y mejore el rendimiento. Si no le preocupa actualizar el contador procesado de formularios, se recomienda establecer el parámetro `isModeFinal` en `false`.

>[!NOTE]
>
>Para obtener más información sobre el servicio de extensiones de Acrobat Reader DC, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para aplicar derechos de uso a un documento PDF, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de cliente de extensiones de Acrobat Reader DC.
1. Recupere un documento PDF.
1. Especifique los derechos de uso que desea aplicar.
1. Aplique derechos de uso al documento PDF.
1. Guarde el documento PDF con derechos activados.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de cliente de extensiones de Acrobat Reader DC**

Para realizar mediante programación una operación de servicio Extensiones de Acrobat Reader DC, debe crear un objeto cliente de servicio de extensiones de Acrobat Reader DC. Si utiliza la API de Java de extensiones de Acrobat Reader DC, cree un objeto `ReaderExtensionsServiceClient`. Si utiliza la API de servicio Web de extensiones de Acrobat Reader DC, cree un objeto `ReaderExtensionsServiceService`.

**Recuperar un documento PDF**

Debe recuperar un documento PDF para poder aplicar derechos de uso. Los documentos PDF con derechos activados contienen un diccionario de derechos de uso. Cuando Adobe Reader abre un documento que contiene dicho diccionario, solo activa los derechos de uso especificados en el diccionario para ese documento. Si el documento no contiene un diccionario de derechos de uso, el servicio de extensiones de Acrobat Reader DC crea uno. Si ya contiene un diccionario, el servicio de extensiones de Acrobat Reader DC sobrescribe los derechos de uso existentes con los que especifique. El diccionario especifica los derechos de uso activados. Cuando un usuario abre el documento en Adobe Reader, solo se permiten los derechos de uso especificados en el diccionario.

**Especificar derechos de uso para aplicar**

Los derechos de uso que puede establecer están determinados por una credencial que adquiere de Adobe Systems Incorporated. Normalmente, las credenciales proporcionan permiso para establecer un grupo de derechos de uso relacionados, como los relativos a los formularios interactivos. Cada credencial proporciona el derecho de crear un determinado número de documentos PDF con derechos activados. Las credenciales de evaluación dan derecho a crear un número ilimitado de documentos de borrador.

>[!NOTE]
>
>Si intenta asignar un derecho de uso no permitido por las credenciales, provocará una excepción.

**Aplicar derechos de uso al documento PDF**

Para aplicar derechos de uso a un documento PDF, debe hacer referencia al alias de las credenciales que utiliza para aplicar derechos de uso (una credencial suele instalarse durante la instalación de AEM Forms). También debe especificar el documento PDF al que se aplican los derechos de uso. Para obtener más información sobre la configuración de credenciales, consulte la guía de instalación e implementación del servidor de aplicaciones.

**Guardar el documento PDF con derechos activados**

Después de que el servicio de extensiones de Acrobat Reader DC aplique derechos de uso a un documento PDF, puede guardar el documento PDF con derechos activados como archivo PDF.

**Consulte también**

[Aplicar derechos de uso mediante la API de Java](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[Aplicar derechos de uso mediante la API de servicio Web](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[inicios rápidos de la API del servicio Extensiones de Acrobat Reader DC](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Aplicar derechos de uso mediante la API de Java {#apply-usage-rights-using-the-java-api}

Aplique derechos de uso a un documento PDF mediante la API de extensiones de Acrobat Reader DC (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-reader-Extensions-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto de cliente de extensiones de Acrobat Reader DC.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `ReaderExtensionsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Recupere un documento PDF.

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Especifique los derechos de uso que desea aplicar.

   * Cree un objeto `UsageRights` que represente los derechos de uso mediante su constructor.
   * Para cada derecho de uso que se va a aplicar, invoque un método correspondiente que pertenece al objeto `UsageRights`. Por ejemplo, para agregar el derecho de uso `enableFormFillIn`, invoque el método `UsageRights` del objeto `enableFormFillIn` y pase `true`. (Repita este paso para cada derecho de uso que desee aplicar).

1. Aplique derechos de uso al documento PDF.

   * Cree un objeto `ReaderExtensionsOptionSpec` utilizando su constructor. Este objeto contiene opciones de tiempo de ejecución que requiere el servicio de extensiones de Acrobat Reader DC. Al invocar este constructor, debe especificar los siguientes valores:

      * El objeto `UsageRights` que contiene los derechos de uso que se aplicarán al documento.
      * Un valor de cadena que especifica un mensaje que un usuario ve cuando se abre el documento PDF con derechos activados en Adobe Reader 7.x. Este mensaje no se muestra en Adobe Reader 8.0.
   * Aplique derechos de uso al documento PDF invocando el método `ReaderExtensionsServiceClient` del objeto `applyUsageRights` y pasando los siguientes valores:

      * El objeto `com.adobe.idp.Document` que contiene el documento PDF al que se aplican derechos de uso.
      * Un valor de cadena que especifica el alias de la credencial que le permite aplicar derechos de uso.
      * Un valor de cadena que especifica el valor de contraseña correspondiente. (Actualmente, se ignora este parámetro. Puede pasar `null`.)
   * El objeto `ReaderExtensionsOptionSpec` que contiene opciones de tiempo de ejecución.

   El método `applyUsageRights` devuelve un objeto `com.adobe.idp.Document` que contiene el documento PDF con derechos activados.

1. Guarde el documento PDF con derechos activados.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea .pdf.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del objeto `com.adobe.idp.Document` en el archivo (asegúrese de utilizar el objeto `com.adobe.idp.Document` devuelto por el método `applyUsageRights`).

**Consulte también**

[Aplicación de derechos de uso a Documentos PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Inicio rápido (modo SOAP):Aplicación de derechos de uso mediante la API de Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aplicar derechos de uso mediante la API de servicio Web {#apply-usage-rights-using-the-web-service-api}

Aplique derechos de uso a un documento PDF mediante la API de extensiones de Acrobat Reader DC (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto de cliente de extensiones de Acrobat Reader DC.

   * Cree un objeto `ReaderExtensionsServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `ReaderExtensionsServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Asegúrese de especificar `?blob=mtom`.)
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `ReaderExtensionsServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere un documento PDF.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar un documento PDF al que se aplican derechos de uso.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read`. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Especifique los derechos de uso que desea aplicar.

   * Cree un objeto `UsageRights` que represente los derechos de uso mediante su constructor.
   * Para cada derecho de uso que aplicar, asigne el valor `true` al miembro de datos correspondiente que pertenece al objeto `UsageRights`. Por ejemplo, para agregar el derecho de uso `enableFormFillIn`, asigne `true` al miembro de datos `UsageRights` del objeto `enableFormFillIn`. (Repita este paso para cada derecho de uso que desee aplicar).

1. Aplique derechos de uso al documento PDF.

   * Cree un objeto `ReaderExtensionsOptionSpec` utilizando su constructor. Este objeto contiene opciones de tiempo de ejecución que requiere el servicio de extensiones de Acrobat Reader DC.
   * Asigne el objeto `UsageRights` al miembro de datos `ReaderExtensionsOptionSpec` del objeto `usageRights`.
   * Asigne un valor de cadena que especifique el mensaje que un usuario ve cuando se abre el documento PDF con derechos activados en Adobe Reader al miembro de datos `ReaderExtensionsOptionSpec` del objeto `message`.
   * Aplique derechos de uso al documento PDF invocando el método `ReaderExtensionsServiceClient` del objeto `applyUsageRights` y pasando los siguientes valores:

      * El objeto `BLOB` que contiene el documento PDF al que se aplican derechos de uso.
      * Un valor de cadena que especifica el alias de la credencial que le permite aplicar derechos de uso.
      * Un valor de cadena que especifica el valor de contraseña correspondiente. (Actualmente, se ignora este parámetro. Puede pasar `null`.)
   * El objeto `ReaderExtensionsOptionSpec` que contiene opciones de tiempo de ejecución.

   El método `applyUsageRights` devuelve un objeto `BLOB` que contiene el documento PDF con derechos activados.

1. Guarde el documento PDF con derechos activados.

   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF con derechos activados.
   * Cree una matriz de bytes que almacene el contenido de datos del objeto `BLOB` devuelto por el método `applyUsageRights`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Aplicación de derechos de uso a Documentos PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Quitando derechos de uso de Documentos PDF {#removing-usage-rights-from-pdf-documents}

Puede eliminar los derechos de uso de un documento con derechos activados. También es necesario quitar derechos de uso de un documento PDF con derechos activados para realizar otras operaciones de AEM Forms en él. Por ejemplo, debe firmar digitalmente (o certificar) un documento PDF antes de definir los derechos de uso. Por lo tanto, si desea realizar operaciones en un documento con derechos activados, debe quitar los derechos de uso del documento PDF, realizar las demás operaciones, como firmar digitalmente el documento y volver a aplicar los derechos de uso al documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio de extensiones de Acrobat Reader DC, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para quitar derechos de uso de un documento PDF con derechos activados, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de cliente de extensiones de Acrobat Reader DC.
1. Recupere un documento PDF con derechos activados.
1. Elimine los derechos de uso del documento PDF.
1. Guarde el documento PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de cliente de extensiones de Acrobat Reader DC**

Para poder realizar mediante programación una operación de servicio de extensiones de Acrobat Reader DC, debe crear un objeto cliente de servicio de extensiones de Acrobat Reader DC. Si utiliza la API de Java, cree un objeto `ReaderExtensionsServiceClient`. Si utiliza la API de servicio Web de extensiones de Acrobat Reader DC, cree un objeto `ReaderExtensionsServiceService`.

**Recuperar un documento PDF con derechos activados**

Recupere un documento PDF con derechos activados para eliminar los derechos de uso.

**Quitar derechos de uso del documento PDF**

Después de recuperar un documento PDF con derechos activados, puede eliminar los derechos de uso. Después de eliminar los derechos de uso, el documento PDF no tendrá ninguna funcionalidad adicional mientras se visualiza en Adobe Reader.

**Guardar el documento PDF**

Puede guardar el documento PDF que ya no contiene derechos de uso como archivo PDF. Una vez guardado como archivo PDF, el documento PDF se puede ver en Adobe Reader o Acrobat.

**Consulte también**

[Eliminar los derechos de uso mediante la API de Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Eliminar derechos de uso mediante la API de servicio Web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[inicios rápidos de la API del servicio Extensiones de Acrobat Reader DC](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[Aplicación de derechos de uso a Documentos PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Eliminar los derechos de uso mediante la API de Java {#remove-usage-rights-using-the-java-api}

Elimine los derechos de uso de un documento PDF con derechos activados mediante la API de extensiones de Acrobat Reader DC (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-reader-Extensions-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto de cliente de extensiones de Acrobat Reader DC.

   Cree un objeto `ReaderExtensionsServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Recupere un documento PDF.

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF con derechos activados mediante su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Elimine los derechos de uso del documento PDF.

   Elimine los derechos de uso del documento PDF invocando el método `ReaderExtensionsServiceClient` del objeto `removeUsageRights` y pasando el objeto `com.adobe.idp.Document` que contiene el documento PDF con derechos activados. Este método devuelve un objeto `com.adobe.idp.Document` que contiene un documento PDF que no tiene derechos de uso.

1. Aplique derechos de uso al documento PDF.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea .PDF.
   * Invoque el método `Document` del objeto `copyToFile` para copiar el contenido del objeto `Document` en el archivo (asegúrese de utilizar el objeto `Document` devuelto por el método `removeUsageRights`).

**Consulte también**

[Eliminación de derechos de uso de Documentos PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Inicio rápido (modo SOAP): Eliminación de derechos de uso de un documento PDF mediante la API de Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminar los derechos de uso mediante la API de servicio Web {#remove-usage-rights-using-the-web-service-api}

Elimine los derechos de uso de un documento PDF con derechos activados mediante la API de extensiones de Acrobat Reader DC (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto de cliente de extensiones de Acrobat Reader DC.

   * Cree un objeto `ReaderExtensionsServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `ReaderExtensionsServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Asegúrese de especificar `?blob=mtom`.)
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `ReaderExtensionsServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere un documento PDF.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el documento PDF con derechos activados del que se eliminan los derechos de uso.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Elimine los derechos de uso del documento PDF.

   Elimine los derechos de uso del documento PDF invocando el método `ReaderExtensionsServiceClient` del objeto `removeUsageRights` y pasando el objeto `BLOB` que contiene el documento PDF con derechos activados. Este método devuelve un objeto `BLOB` que contiene un documento PDF que no tiene derechos de uso.

1. Aplique derechos de uso al documento PDF.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo PDF.
   * Cree una matriz de bytes que almacene el contenido de datos del objeto `BLOB` devuelto por el método `removeUsageRights`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.

**Consulte también**

[Eliminación de derechos de uso de Documentos PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Recuperación de información de credenciales {#retrieving-credential-information}

Puede recuperar información sobre las credenciales que se utilizaron para aplicar derechos de uso a un documento PDF con derechos activados. Al recuperar información sobre una credencial, puede obtener información como la fecha después de la cual el certificado ya no es válido.

>[!NOTE]
>
>Para obtener más información sobre el servicio de extensiones de Acrobat Reader DC, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-2}

Para recuperar información sobre las credenciales utilizadas para aplicar derechos de uso a un documento PDF, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de cliente de extensiones de Acrobat Reader DC.
1. Recupere un documento PDF con derechos activados.
1. Recupere información sobre las credenciales.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de cliente de extensiones de Acrobat Reader DC**

Para poder realizar mediante programación una operación de servicio de extensiones de Acrobat Reader DC, debe crear un objeto cliente de servicio de extensiones de Acrobat Reader DC. Si utiliza la API de Java, cree un objeto `ReaderExtensionsServiceClient`. Si utiliza la API de servicio Web de extensiones de Acrobat Reader DC, cree un objeto `ReaderExtensionsServiceService`.

**Recuperar un documento PDF con derechos activados**

Debe recuperar un documento PDF con derechos activados para recuperar información sobre las credenciales. También puede recuperar información sobre una credencial especificando su alias; sin embargo, si desea recuperar información sobre una credencial que se utilizó para aplicar derechos de uso a un documento PDF con derechos específicos activados, debe recuperar el documento.

**Recuperar información sobre la credencial**

Después de recuperar un documento PDF con derechos activados, puede obtener información sobre las credenciales que se utilizaron para aplicarle derechos de uso. Puede obtener la siguiente información sobre las credenciales:

* Mensaje que se muestra en Adobe Reader cuando se abre el documento PDF con derechos activados.
* La fecha después de la cual la credencial ya no es válida.
* La fecha antes de la cual la credencial no es válida.
* Derechos de uso establecidos para este documento PDF con derechos activados.
* El número de veces que se ha utilizado la credencial.

**Consulte también**

[Eliminar los derechos de uso mediante la API de Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Eliminar derechos de uso mediante la API de servicio Web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[inicios rápidos de la API del servicio Extensiones de Acrobat Reader DC](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Recuperar información de credenciales mediante la API de Java {#retrieve-credential-information-using-the-java-api}

Recupere información de credenciales mediante la API de extensiones de Acrobat Reader DC (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-reader-Extensions-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto de cliente de extensiones de Acrobat Reader DC.

   Cree un objeto `ReaderExtensionsServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Recupere un documento PDF.

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF con derechos activados mediante su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF con derechos activados.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Elimine los derechos de uso del documento PDF.

   * Recupere información sobre las credenciales utilizadas para aplicar derechos de uso al documento PDF invocando el método `ReaderExtensionsServiceClient` del objeto `getDocumentUsageRights` y pasando el objeto `com.adobe.idp.Document` que contiene el documento PDF con derechos activados. Este método devuelve un objeto `GetUsageRightsResult` que contiene información de credenciales.
   * Recupere la fecha después de la cual la credencial ya no es válida invocando el método `GetUsageRightsResult` del objeto `getNotAfter`. Este método devuelve un objeto `java.util.Date` que representa la fecha después de la cual la credencial ya no es válida.
   * Recupere el mensaje que se muestra en Adobe Reader cuando se abre el documento PDF con derechos activados invocando el método `GetUsageRightsResult` del objeto `getMessage`. Este método devuelve un valor de cadena que representa el mensaje.

**Consulte también**

[Recuperación de información de credenciales](assigning-usage-rights.md#retrieving-credential-information)

[Inicio rápido (modo SOAP): Recuperación de información de credenciales mediante la API de Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar información de credenciales mediante la API de servicio Web {#retrieve-credential-information-using-the-web-service-api}

Recuperar información de credenciales mediante la API de extensiones de Acrobat Reader DC (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto de cliente de extensiones de Acrobat Reader DC.

   * Cree un objeto `ReaderExtensionsServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `ReaderExtensionsServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Asegúrese de especificar `?blob=mtom`.)
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `ReaderExtensionsServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere un documento PDF.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar un documento PDF con derechos activados.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF con derechos activados y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Elimine los derechos de uso del documento PDF.

   * Recupere información sobre las credenciales utilizadas para aplicar derechos de uso al documento PDF invocando el método `ReaderExtensionsServiceClient` del objeto `getDocumentUsageRights` y pasando el objeto `com.adobe.idp.Document` que contiene el documento PDF con derechos activados. Este método devuelve un objeto `GetUsageRightsResult` que contiene información de credenciales.
   * Recupere la fecha después de la cual la credencial ya no es válida obteniendo el valor del miembro de datos `GetUsageRightsResult` del objeto `notAfter`. El tipo de datos de este miembro de datos es `System.DateTime`.
   * Recupere el mensaje que se muestra cuando se abre el documento PDF con derechos activados en Adobe Reader obteniendo el valor del miembro de datos `GetUsageRightsResult` del objeto `message`. El tipo de datos de este miembro de datos es una cadena.
   * Recupere el número de veces que se utiliza la credencial obteniendo el valor del miembro de datos `GetUsageRightsResult` del objeto `useCount`. El tipo de datos de este miembro de datos es un entero.

**Consulte también**

[Recuperación de información de credenciales](assigning-usage-rights.md#retrieving-credential-information)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
