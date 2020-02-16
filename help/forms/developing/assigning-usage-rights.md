---
title: Asignación de derechos de uso
seo-title: Asignación de derechos de uso
description: nulo
seo-description: nulo
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# Asignación de derechos de uso {#assigning-usage-rights}

## Acerca del servicio de extensiones de Acrobat Reader DC {#about-the-acrobat-reader-dc-extensions-service}

El servicio de extensiones de Acrobat Reader DC permite a su organización compartir fácilmente documentos PDF interactivos mediante la ampliación de la funcionalidad de Adobe Reader. El servicio de extensiones de Acrobat Reader DC es totalmente compatible con cualquier documento PDF, hasta PDF 1.7 inclusive. Funciona con Adobe Reader 7.0 y posterior. El servicio agrega derechos de uso a un documento PDF, activando funciones que normalmente no están disponibles cuando se abre un documento PDF con Adobe Reader. Los usuarios de terceros no requieren software o complementos adicionales para trabajar con los documentos habilitados para derechos.

Puede realizar estas tareas mediante el servicio de extensiones de Acrobat Reader DC:

* Aplicar derechos de uso a documentos PDF. Para obtener más información, consulte [Aplicación de derechos de uso a documentos](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)PDF.
* Elimine los derechos de uso de los documentos PDF. Para obtener más información, consulte [Eliminación de derechos de uso de documentos](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)PDF.
* Recuperar detalles de credenciales. Para obtener más información, consulte [Recuperación de información](assigning-usage-rights.md#retrieving-credential-information)de credenciales.

>[!NOTE]
>
>Para obtener más información sobre el servicio de extensiones de Acrobat Reader DC, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Aplicación de derechos de uso a documentos PDF {#applying-usage-rights-to-pdf-documents}

Puede aplicar derechos de uso a documentos PDF mediante las extensiones de Acrobat Reader DC API de Java Client y el servicio Web. Los derechos de uso se refieren a funciones que están disponibles de forma predeterminada en Acrobat pero no en Adobe Reader, como la capacidad de agregar comentarios a un formulario o de rellenar los campos del formulario y guardarlo. Los documentos PDF que tienen derechos de uso aplicados se denominan documentos habilitados para derechos. Un usuario que abre un documento con derechos activados en Adobe Reader puede realizar operaciones que estén activadas para ese documento específico.

>[!NOTE]
>
>Al aplicar derechos de uso a documentos PDF mediante el `applyUsageRights` método, que forma parte de la API de Java, puede establecer el `isModeFinal` parámetro del `ReaderExtensionsOptionSpec` objeto en `false`. Esto hace que el contador procesado de formularios no se actualice y mejore el rendimiento. Si no le preocupa actualizar el contador procesado de formularios, se recomienda establecer el `isModeFinal` parámetro en `false`.

>[!NOTE]
>
>Para obtener más información sobre el servicio de extensiones de Acrobat Reader DC, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

**Creación de un objeto de cliente para extensiones de Acrobat Reader DC**

Para realizar mediante programación una operación de servicio de extensiones de Acrobat Reader DC, debe crear un objeto cliente de servicio de extensiones de Acrobat Reader DC. Si utiliza la API de Java de extensiones de Acrobat Reader DC, cree un `ReaderExtensionsServiceClient` objeto. Si utiliza la API de servicio web de extensiones de Acrobat Reader DC, cree un `ReaderExtensionsServiceService` objeto.

**Recuperar un documento PDF**

Debe recuperar un documento PDF para aplicar derechos de uso. Los documentos PDF con derechos activados contienen un diccionario de derechos de uso. Cuando Adobe Reader abre un documento que contiene dicho diccionario, solo activa los derechos de uso especificados en el diccionario para ese documento. Si el documento no contiene un diccionario de derechos de uso, el servicio de extensiones de Acrobat Reader DC crea uno. Si ya contiene un diccionario, el servicio de extensiones de Acrobat Reader DC sobrescribe los derechos de uso existentes con los que especifique. El diccionario especifica los derechos de uso activados. Cuando un usuario abre el documento en Adobe Reader, solo se permiten los derechos de uso especificados en el diccionario.

**Especifique los derechos de uso que aplicar**

Los derechos de uso que puede establecer están determinados por una credencial que adquiere de Adobe Systems Incorporated. Normalmente, las credenciales proporcionan permiso para establecer un grupo de derechos de uso relacionados, como los relativos a los formularios interactivos. Cada credencial proporciona el derecho de crear un determinado número de documentos PDF con derechos activados. Las credenciales de evaluación dan derecho a crear un número ilimitado de borradores de documentos.

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

[Inicio rápido de la API del servicio de extensiones de Acrobat Reader DC](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Aplicar derechos de uso mediante la API de Java {#apply-usage-rights-using-the-java-api}

Aplique derechos de uso a un documento PDF mediante la API de extensiones de Acrobat Reader DC (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-reader-Extensions-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto de cliente de extensiones de Acrobat Reader DC.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `ReaderExtensionsServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recupere un documento PDF.

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Especifique los derechos de uso que desea aplicar.

   * Cree un `UsageRights` objeto que represente derechos de uso mediante su constructor.
   * Para cada derecho de uso que se va a aplicar, invoque un método correspondiente que pertenece al `UsageRights` objeto. Por ejemplo, para agregar la `enableFormFillIn` propiedad de uso, invoque el `UsageRights` método `enableFormFillIn` del objeto y pase `true`. (Repita este paso para cada derecho de uso que desee aplicar).

1. Aplique derechos de uso al documento PDF.

   * Cree un `ReaderExtensionsOptionSpec` objeto con su constructor. Este objeto contiene opciones de tiempo de ejecución que requiere el servicio de extensiones de Acrobat Reader DC. Al invocar este constructor, debe especificar los siguientes valores:

      * El `UsageRights` objeto que contiene los derechos de uso que se aplicarán al documento.
      * Un valor de cadena que especifica un mensaje que un usuario ve cuando se abre el documento PDF con derechos activados en Adobe Reader 7.x. Este mensaje no se muestra en Adobe Reader 8.0.
   * Aplique derechos de uso al documento PDF invocando el `ReaderExtensionsServiceClient` método del `applyUsageRights` objeto y pasando los siguientes valores:

      * El `com.adobe.idp.Document` objeto que contiene el documento PDF al que se aplican derechos de uso.
      * Un valor de cadena que especifica el alias de la credencial que le permite aplicar derechos de uso.
      * Un valor de cadena que especifica el valor de contraseña correspondiente. (Actualmente, se ignora este parámetro. Puedes pasar `null`).
   * El `ReaderExtensionsOptionSpec` objeto que contiene opciones de tiempo de ejecución.
   El `applyUsageRights` método devuelve un `com.adobe.idp.Document` objeto que contiene el documento PDF con derechos activados.

1. Guarde el documento PDF con derechos activados.

   * Cree un `java.io.File` objeto y asegúrese de que la extensión del archivo sea .pdf.
   * Invoque el `com.adobe.idp.Document` método del `copyToFile` objeto para copiar el contenido del `com.adobe.idp.Document` objeto en el archivo (asegúrese de utilizar el `com.adobe.idp.Document` objeto devuelto por el `applyUsageRights` método).

**Consulte también**

[Aplicación de derechos de uso a documentos PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Inicio rápido (modo SOAP):Aplicación de derechos de uso mediante la API de Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aplicar derechos de uso mediante la API de servicio Web {#apply-usage-rights-using-the-web-service-api}

Aplique derechos de uso a un documento PDF mediante la API de extensiones de Acrobat Reader DC (servicio Web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto de cliente de extensiones de Acrobat Reader DC.

   * Cree un `ReaderExtensionsServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `ReaderExtensionsServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Asegúrese de especificar `?blob=mtom`).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `ReaderExtensionsServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere un documento PDF.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar un documento PDF al que se aplican derechos de uso.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el `BLOB` objeto asignando su `MTOM` propiedad con el contenido de la matriz de bytes.

1. Especifique los derechos de uso que desea aplicar.

   * Cree un `UsageRights` objeto que represente derechos de uso mediante su constructor.
   * Para cada derecho de uso que aplicar, asigne el valor `true` al miembro de datos correspondiente que pertenece al `UsageRights` objeto. Por ejemplo, para agregar el derecho de `enableFormFillIn` uso, asigne `true` al miembro de datos del `UsageRights` objeto `enableFormFillIn` . (Repita este paso para cada derecho de uso que desee aplicar).

1. Aplique derechos de uso al documento PDF.

   * Cree un `ReaderExtensionsOptionSpec` objeto con su constructor. Este objeto contiene opciones de tiempo de ejecución que requiere el servicio de extensiones de Acrobat Reader DC.
   * Asigne el `UsageRights` objeto al miembro de `ReaderExtensionsOptionSpec` datos `usageRights` del objeto.
   * Asigne un valor de cadena que especifique el mensaje que verá un usuario cuando se abra el documento PDF con derechos activados en Adobe Reader al miembro de `ReaderExtensionsOptionSpec` datos del `message` objeto.
   * Aplique derechos de uso al documento PDF invocando el `ReaderExtensionsServiceClient` método del `applyUsageRights` objeto y pasando los siguientes valores:

      * El `BLOB` objeto que contiene el documento PDF al que se aplican derechos de uso.
      * Un valor de cadena que especifica el alias de la credencial que le permite aplicar derechos de uso.
      * Un valor de cadena que especifica el valor de contraseña correspondiente. (Actualmente, se ignora este parámetro. Puedes pasar `null`).
   * El `ReaderExtensionsOptionSpec` objeto que contiene opciones de tiempo de ejecución.
   El `applyUsageRights` método devuelve un `BLOB` objeto que contiene el documento PDF con derechos activados.

1. Guarde el documento PDF con derechos activados.

   * Cree un `System.IO.FileStream` objeto invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF con derechos activados.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto devuelto por el `applyUsageRights` método. Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el `System.IO.BinaryWriter` método `Write` del objeto y pasando la matriz de bytes.

**Consulte también**

[Aplicación de derechos de uso a documentos PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Eliminación de derechos de uso de documentos PDF {#removing-usage-rights-from-pdf-documents}

Puede quitar derechos de uso de un documento con derechos activados. También es necesario quitar derechos de uso de un documento PDF con derechos activados para realizar otras operaciones de AEM Forms en él. Por ejemplo, debe firmar digitalmente (o certificar) un documento PDF antes de definir los derechos de uso. Por lo tanto, si desea realizar operaciones en un documento con derechos activados, debe quitar derechos de uso del documento PDF, realizar las demás operaciones, como firmar digitalmente el documento y volver a aplicar derechos de uso al documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio de extensiones de Acrobat Reader DC, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para quitar derechos de uso de un documento PDF con derechos activados, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de cliente de extensiones de Acrobat Reader DC.
1. Recupere un documento PDF con derechos activados.
1. Elimine los derechos de uso del documento PDF.
1. Guarde el documento PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de cliente para extensiones de Acrobat Reader DC**

Para poder realizar mediante programación una operación de servicio de extensiones de Acrobat Reader DC, debe crear un objeto cliente de servicio de extensiones de Acrobat Reader DC. Si utiliza la API de Java, cree un `ReaderExtensionsServiceClient` objeto. Si utiliza la API de servicio web de extensiones de Acrobat Reader DC, cree un `ReaderExtensionsServiceService` objeto.

**Recuperar un documento PDF con derechos activados**

Recupere un documento PDF con derechos activados para eliminar los derechos de uso.

**Quitar derechos de uso del documento PDF**

Después de recuperar un documento PDF con derechos activados, puede eliminar los derechos de uso. Después de eliminar los derechos de uso, el documento PDF no tendrá ninguna funcionalidad adicional mientras se visualiza en Adobe Reader.

**Guardar el documento PDF**

Puede guardar el documento PDF que ya no contenga derechos de uso como archivo PDF. Una vez guardado como archivo PDF, el documento PDF se puede ver en Adobe Reader o Acrobat.

**Consulte también**

[Eliminar los derechos de uso mediante la API de Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Eliminar derechos de uso mediante la API de servicio Web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de extensiones de Acrobat Reader DC](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[Aplicación de derechos de uso a documentos PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Eliminar los derechos de uso mediante la API de Java {#remove-usage-rights-using-the-java-api}

Elimine los derechos de uso de un documento PDF con derechos activados mediante la API de extensiones de Acrobat Reader DC (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-reader-Extensions-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto de cliente de extensiones de Acrobat Reader DC.

   Cree un `ReaderExtensionsServiceClient` objeto utilizando su constructor y pasando un `ServiceClientFactory` objeto que contenga propiedades de conexión.

1. Recupere un documento PDF.

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF con derechos activados mediante su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Elimine los derechos de uso del documento PDF.

   Elimine los derechos de uso del documento PDF invocando el `ReaderExtensionsServiceClient` método `removeUsageRights` del objeto y pasando el `com.adobe.idp.Document` objeto que contiene el documento PDF con derechos activados. Este método devuelve un `com.adobe.idp.Document` objeto que contiene un documento PDF que no tiene derechos de uso.

1. Aplique derechos de uso al documento PDF.

   * Cree un `java.io.File` objeto y asegúrese de que la extensión del archivo sea .PDF.
   * Invoque el `Document` método del `copyToFile` objeto para copiar el contenido del `Document` objeto en el archivo (asegúrese de utilizar el `Document` objeto devuelto por el `removeUsageRights` método).

**Consulte también**

[Eliminación de derechos de uso de documentos PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Inicio rápido (modo SOAP): Eliminación de derechos de uso de un documento PDF mediante la API de Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminar derechos de uso mediante la API de servicio Web {#remove-usage-rights-using-the-web-service-api}

Elimine los derechos de uso de un documento PDF con derechos activados mediante la API de extensiones de Acrobat Reader DC (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto de cliente de extensiones de Acrobat Reader DC.

   * Cree un `ReaderExtensionsServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `ReaderExtensionsServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Asegúrese de especificar `?blob=mtom`).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `ReaderExtensionsServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere un documento PDF.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar el documento PDF con derechos activados del que se eliminan los derechos de uso.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` propiedad con el contenido de la matriz de bytes.

1. Elimine los derechos de uso del documento PDF.

   Elimine los derechos de uso del documento PDF invocando el `ReaderExtensionsServiceClient` método `removeUsageRights` del objeto y pasando el `BLOB` objeto que contiene el documento PDF con derechos activados. Este método devuelve un `BLOB` objeto que contiene un documento PDF que no tiene derechos de uso.

1. Aplique derechos de uso al documento PDF.

   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo PDF.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto devuelto por el `removeUsageRights` método. Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.

**Consulte también**

[Eliminación de derechos de uso de documentos PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Recuperación de información de credenciales {#retrieving-credential-information}

Puede recuperar información sobre las credenciales utilizadas para aplicar derechos de uso a un documento PDF con derechos activados. Al recuperar información sobre una credencial, puede obtener información como la fecha después de la cual el certificado ya no es válido.

>[!NOTE]
>
>Para obtener más información sobre el servicio de extensiones de Acrobat Reader DC, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-2}

Para recuperar información sobre las credenciales utilizadas para aplicar derechos de uso a un documento PDF, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de cliente de extensiones de Acrobat Reader DC.
1. Recupere un documento PDF con derechos activados.
1. Recupere información sobre las credenciales.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de cliente para extensiones de Acrobat Reader DC**

Para poder realizar mediante programación una operación de servicio de extensiones de Acrobat Reader DC, debe crear un objeto cliente de servicio de extensiones de Acrobat Reader DC. Si utiliza la API de Java, cree un `ReaderExtensionsServiceClient` objeto. Si utiliza la API de servicio web de extensiones de Acrobat Reader DC, cree un `ReaderExtensionsServiceService` objeto.

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

[Inicio rápido de la API del servicio de extensiones de Acrobat Reader DC](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Recuperar información de credenciales mediante la API de Java {#retrieve-credential-information-using-the-java-api}

Recupere información de credenciales mediante la API de extensiones de Acrobat Reader DC (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-reader-Extensions-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto de cliente de extensiones de Acrobat Reader DC.

   Cree un `ReaderExtensionsServiceClient` objeto utilizando su constructor y pasando un `ServiceClientFactory` objeto que contenga propiedades de conexión.

1. Recupere un documento PDF.

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF con derechos activados mediante su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF con derechos activados.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Elimine los derechos de uso del documento PDF.

   * Recupere información sobre las credenciales utilizadas para aplicar derechos de uso al documento PDF invocando el `ReaderExtensionsServiceClient` método del `getDocumentUsageRights` objeto y pasando el `com.adobe.idp.Document` objeto que contiene el documento PDF con derechos activados. Este método devuelve un `GetUsageRightsResult` objeto que contiene información de credenciales.
   * Recupere la fecha después de la cual la credencial ya no es válida invocando el `GetUsageRightsResult` método `getNotAfter` del objeto. Este método devuelve un `java.util.Date` objeto que representa la fecha después de la cual la credencial ya no es válida.
   * Recupere el mensaje que se muestra en Adobe Reader cuando se abre el documento PDF con derechos activados invocando el `GetUsageRightsResult` método del `getMessage` objeto. Este método devuelve un valor de cadena que representa el mensaje.

**Consulte también**

[Recuperación de información de credenciales](assigning-usage-rights.md#retrieving-credential-information)

[Inicio rápido (modo SOAP): Recuperación de información de credenciales mediante la API de Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar información de credenciales mediante la API de servicio web {#retrieve-credential-information-using-the-web-service-api}

Recupere información de credenciales mediante la API de extensiones de Acrobat Reader DC (servicio Web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto de cliente de extensiones de Acrobat Reader DC.

   * Cree un `ReaderExtensionsServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `ReaderExtensionsServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Asegúrese de especificar `?blob=mtom`).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `ReaderExtensionsServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere un documento PDF.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar un documento PDF con derechos activados.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF con derechos activados y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` propiedad con el contenido de la matriz de bytes.

1. Elimine los derechos de uso del documento PDF.

   * Recupere información sobre las credenciales utilizadas para aplicar derechos de uso al documento PDF invocando el `ReaderExtensionsServiceClient` método del `getDocumentUsageRights` objeto y pasando el `com.adobe.idp.Document` objeto que contiene el documento PDF con derechos activados. Este método devuelve un `GetUsageRightsResult` objeto que contiene información de credenciales.
   * Recupere la fecha después de la cual la credencial ya no es válida obteniendo el valor del miembro de `GetUsageRightsResult` datos del `notAfter` objeto. El tipo de datos de este miembro de datos es `System.DateTime`.
   * Recupere el mensaje que se muestra cuando se abre el documento PDF con derechos activados en Adobe Reader obteniendo el valor del miembro de `GetUsageRightsResult` datos del `message` objeto. El tipo de datos de este miembro de datos es una cadena.
   * Recupere el número de veces que se utiliza la credencial obteniendo el valor del miembro de `GetUsageRightsResult` datos del `useCount` objeto. El tipo de datos de este miembro de datos es un entero.

**Consulte también**

[Recuperación de información de credenciales](assigning-usage-rights.md#retrieving-credential-information)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
