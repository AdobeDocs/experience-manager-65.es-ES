---
title: Asignación de derechos de uso
seo-title: Asignación de derechos de uso
description: Utilice la API de cliente Java y la API de servicio web de Acrobat Reader DC Extensions para aplicar y eliminar los derechos de uso de los documentos PDF.
seo-description: Utilice la API de cliente Java y la API de servicio web de Acrobat Reader DC Extensions para aplicar y eliminar los derechos de uso de los documentos PDF.
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3952'
ht-degree: 0%

---


# Asignación de derechos de uso {#assigning-usage-rights}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

## Acerca del servicio de extensiones de Acrobat Reader DC {#about-the-acrobat-reader-dc-extensions-service}

El servicio de extensiones de Acrobat Reader DC permite a su organización compartir fácilmente documentos PDF interactivos mediante la ampliación de la funcionalidad de Adobe Reader. El servicio de extensiones de Acrobat Reader DC es totalmente compatible con cualquier documento PDF, hasta PDF 1.7 incluido. Funciona con Adobe Reader 7.0 y versiones posteriores. El servicio agrega derechos de uso a un documento PDF, activando funciones que normalmente no están disponibles cuando se abre un documento PDF con Adobe Reader. Los usuarios de terceros no necesitan software ni complementos adicionales para trabajar con los documentos habilitados para derechos.

Puede realizar estas tareas mediante el servicio de extensiones de Acrobat Reader DC:

* Aplicar derechos de uso a documentos PDF. Para obtener más información, consulte [Aplicación de derechos de uso a documentos PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).
* Elimine los derechos de uso de los documentos PDF. Para obtener más información, consulte [Eliminación de derechos de uso de documentos PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).
* Recupere detalles de credenciales. Para obtener más información, consulte [Recuperación de información de credenciales](assigning-usage-rights.md#retrieving-credential-information).

>[!NOTE]
>
>Para obtener más información sobre el servicio de extensiones de Acrobat Reader DC, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Aplicación de derechos de uso a documentos PDF {#applying-usage-rights-to-pdf-documents}

Puede aplicar derechos de uso a documentos PDF mediante la API de cliente Java y el servicio web de Acrobat Reader DC Extensions. Los derechos de uso pertenecen a funciones que están disponibles de forma predeterminada en Acrobat pero no en Adobe Reader, como la capacidad de agregar comentarios a un formulario o de rellenar los campos del formulario y guardar el formulario. Los documentos PDF que tienen derechos de uso aplicados se denominan documentos habilitados para derechos. Un usuario que abre un documento con derechos activados en Adobe Reader puede realizar operaciones que estén habilitadas para ese documento específico.

>[!NOTE]
>
>Al aplicar derechos de uso a documentos PDF mediante el método `applyUsageRights`, que forma parte de la API de Java, puede establecer el parámetro `isModeFinal` del objeto `ReaderExtensionsOptionSpec` en `false`. Esto hace que el contador procesado de formularios no se actualice y mejore el rendimiento. Si no le preocupa actualizar el contador procesado de formularios, se recomienda establecer el parámetro `isModeFinal` en `false`.

>[!NOTE]
>
>Para obtener más información sobre el servicio de extensiones de Acrobat Reader DC, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para aplicar derechos de uso a un documento PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto cliente de extensiones de Acrobat Reader DC.
1. Recupere un documento PDF.
1. Especifique los derechos de uso que desea aplicar.
1. Aplique derechos de uso al documento PDF.
1. Guarde el documento PDF con los derechos activados.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un objeto cliente de extensiones de Acrobat Reader DC**

Para realizar una operación de servicio de Acrobat Reader DC Extensions mediante programación, debe crear un objeto cliente de servicio de Acrobat Reader DC Extensions. Si utiliza la API Java de extensiones de Acrobat Reader DC, cree un objeto `ReaderExtensionsServiceClient`. Si utiliza la API de servicio web de extensiones de Acrobat Reader DC, cree un objeto `ReaderExtensionsServiceService`.

**Recuperar un documento PDF**

Debe recuperar un documento PDF para aplicar derechos de uso. Los documentos PDF con derechos activados contienen un diccionario de derechos de uso. Cuando Adobe Reader abre un documento que contiene ese diccionario, habilita los derechos de uso especificados en el diccionario solo para ese documento. Si el documento no contiene un diccionario de derechos de uso, el servicio de extensiones de Acrobat Reader DC crea uno. Si ya contiene un diccionario, el servicio de extensiones de Acrobat Reader DC sobrescribe los derechos de uso existentes con los que especifique. El diccionario especifica qué derechos de uso están habilitados. Cuando un usuario abre el documento en Adobe Reader, solo se permiten los derechos de uso especificados en el diccionario.

**Especificar derechos de uso para aplicar**

Los derechos de uso que puede establecer están determinados por una credencial que compra en Adobe Systems Incorporated. Normalmente, las credenciales proporcionan permiso para establecer un grupo de derechos de uso relacionados, como los que pertenecen a formularios interactivos. Cada credencial proporciona el derecho de crear un determinado número de documentos PDF con derechos activados. Las credenciales de evaluación dan derecho a crear un número ilimitado de borradores de documentos.

>[!NOTE]
>
>Si intenta asignar un derecho de uso no permitido por las credenciales, provocará una excepción.

**Aplicar derechos de uso al documento PDF**

Para aplicar derechos de uso a un documento PDF, se hace referencia al alias de la credencial que se está utilizando para aplicar derechos de uso (normalmente se instala una credencial durante la instalación de AEM Forms). También debe especificar el documento PDF al que se aplican los derechos de uso. Para obtener información sobre la configuración de credenciales, consulte la guía de instalación e implementación para el servidor de aplicaciones.

**Guarde el documento PDF con los derechos activados**

Una vez que el servicio de extensiones de Acrobat Reader DC aplique derechos de uso a un documento PDF, puede guardar el documento PDF con derechos activados como archivo PDF.

**Consulte también**

[Aplicación de derechos de uso mediante la API de Java](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[Aplicar derechos de uso mediante la API de servicio web](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Extensiones de Acrobat Reader DC](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Aplicar derechos de uso mediante la API de Java {#apply-usage-rights-using-the-java-api}

Aplique derechos de uso a un documento PDF utilizando la API de extensiones de Acrobat Reader DC (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-reader-extensions-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto cliente de extensiones de Acrobat Reader DC.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `ReaderExtensionsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Recupere un documento PDF.

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Especifique los derechos de uso que desea aplicar.

   * Cree un objeto `UsageRights` que represente los derechos de uso utilizando su constructor.
   * Para cada derecho de uso que se deba aplicar, invoque un método correspondiente que pertenece al objeto `UsageRights` . Por ejemplo, para añadir el derecho de uso `enableFormFillIn`, invoque el método `UsageRights` del objeto `enableFormFillIn` y pase `true`. (Repita este paso para cada derecho de uso que desee aplicar).

1. Aplique derechos de uso al documento PDF.

   * Cree un objeto `ReaderExtensionsOptionSpec` utilizando su constructor. Este objeto contiene opciones en tiempo de ejecución que requiere el servicio de extensiones de Acrobat Reader DC. Al invocar este constructor, debe especificar los siguientes valores:

      * El objeto `UsageRights` que contiene los derechos de uso que se deben aplicar al documento.
      * Valor de cadena que especifica un mensaje que un usuario ve cuando se abre el documento PDF con derechos activados en Adobe Reader 7.x. Este mensaje no se muestra en Adobe Reader 8.0.
   * Aplique derechos de uso al documento PDF invocando el método `ReaderExtensionsServiceClient` del objeto `applyUsageRights` y pasando los siguientes valores:

      * El objeto `com.adobe.idp.Document` que contiene el documento PDF al que se aplican los derechos de uso.
      * Un valor de cadena que especifica el alias de la credencial que le permite aplicar derechos de uso.
      * Un valor de cadena que especifica el valor de contraseña correspondiente. (Actualmente se ignora este parámetro. Puede pasar `null`.)
   * El objeto `ReaderExtensionsOptionSpec` que contiene opciones en tiempo de ejecución.

   El método `applyUsageRights` devuelve un objeto `com.adobe.idp.Document` que contiene el documento PDF con derechos activados.

1. Guarde el documento PDF con los derechos activados.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea .pdf.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del objeto `com.adobe.idp.Document` en el archivo (asegúrese de utilizar el objeto `com.adobe.idp.Document` que devolvió el método `applyUsageRights`).

**Consulte también**

[Aplicación de derechos de uso a documentos PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Inicio rápido (modo SOAP):Aplicación de derechos de uso mediante la API de Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aplicar derechos de uso mediante la API de servicio web {#apply-usage-rights-using-the-web-service-api}

Aplique derechos de uso a un documento PDF utilizando la API de extensiones de Acrobat Reader DC (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto cliente de extensiones de Acrobat Reader DC.

   * Cree un objeto `ReaderExtensionsServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `ReaderExtensionsServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Asegúrese de especificar `?blob=mtom`.)
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `ReaderExtensionsServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
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
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read`. Pase la matriz de bytes, la posición de inicio y la longitud del flujo para leerlos.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Especifique los derechos de uso que desea aplicar.

   * Cree un objeto `UsageRights` que represente los derechos de uso utilizando su constructor.
   * Para cada derecho de uso que se aplique, asigne el valor `true` al miembro de datos correspondiente que pertenece al objeto `UsageRights`. Por ejemplo, para agregar el derecho de uso `enableFormFillIn`, asigne `true` al miembro de datos `UsageRights` del objeto `enableFormFillIn`. (Repita este paso para cada derecho de uso que desee aplicar).

1. Aplique derechos de uso al documento PDF.

   * Cree un objeto `ReaderExtensionsOptionSpec` utilizando su constructor. Este objeto contiene opciones en tiempo de ejecución que requiere el servicio de extensiones de Acrobat Reader DC.
   * Asigne el objeto `UsageRights` al miembro de datos `ReaderExtensionsOptionSpec` del objeto `usageRights`.
   * Asigne un valor de cadena que especifique el mensaje que verá un usuario cuando se abra el documento PDF con derechos activados en Adobe Reader al miembro de datos `ReaderExtensionsOptionSpec` del objeto `message`.
   * Aplique derechos de uso al documento PDF invocando el método `ReaderExtensionsServiceClient` del objeto `applyUsageRights` y pasando los siguientes valores:

      * El objeto `BLOB` que contiene el documento PDF al que se aplican los derechos de uso.
      * Un valor de cadena que especifica el alias de la credencial que le permite aplicar derechos de uso.
      * Un valor de cadena que especifica el valor de contraseña correspondiente. (Actualmente se ignora este parámetro. Puede pasar `null`.)
   * El objeto `ReaderExtensionsOptionSpec` que contiene opciones en tiempo de ejecución.

   El método `applyUsageRights` devuelve un objeto `BLOB` que contiene el documento PDF con derechos activados.

1. Guarde el documento PDF con los derechos activados.

   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF con derechos activados.
   * Cree una matriz de bytes que almacene el contenido de datos del objeto `BLOB` que el método `applyUsageRights` devolvió. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Aplicación de derechos de uso a documentos PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Eliminación de derechos de uso de documentos PDF {#removing-usage-rights-from-pdf-documents}

Puede quitar derechos de uso de un documento con derechos activados. También es necesario eliminar los derechos de uso de un documento PDF con derechos activados para realizar otras operaciones de AEM Forms en él. Por ejemplo, debe firmar digitalmente (o certificar) un documento PDF antes de establecer los derechos de uso. Por lo tanto, si desea realizar operaciones en un documento con derechos activados, debe eliminar los derechos de uso del documento PDF, realizar las demás operaciones, como la firma digital del documento y, a continuación, volver a aplicar los derechos de uso al documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio de extensiones de Acrobat Reader DC, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para eliminar los derechos de uso de un documento PDF con derechos activados, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto cliente de extensiones de Acrobat Reader DC.
1. Recupere un documento PDF con derechos activados.
1. Elimine los derechos de uso del documento PDF.
1. Guarde el documento PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un objeto cliente de extensiones de Acrobat Reader DC**

Para poder realizar una operación de servicio de extensiones de Acrobat Reader DC mediante programación, debe crear un objeto cliente de servicio de extensiones de Acrobat Reader DC. Si utiliza la API de Java, cree un objeto `ReaderExtensionsServiceClient`. Si utiliza la API de servicio web de extensiones de Acrobat Reader DC, cree un objeto `ReaderExtensionsServiceService`.

**Recuperar un documento PDF con derechos activados**

Recupere un documento PDF con derechos activados para eliminar los derechos de uso.

**Eliminación de los derechos de uso del documento PDF**

Después de recuperar un documento PDF con derechos activados, puede eliminar los derechos de uso. Después de eliminar los derechos de uso, el documento PDF no tendrá ninguna funcionalidad adicional mientras se vea dentro de Adobe Reader.

**Guardar el documento PDF**

Puede guardar el documento PDF que ya no contiene derechos de uso como archivo PDF. Una vez guardado como archivo PDF, el documento PDF se puede ver en Adobe Reader o Acrobat.

**Consulte también**

[Eliminación de los derechos de uso mediante la API de Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Eliminación de los derechos de uso mediante la API de servicio web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Extensiones de Acrobat Reader DC](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[Aplicación de derechos de uso a documentos PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Eliminación de los derechos de uso mediante la API de Java {#remove-usage-rights-using-the-java-api}

Elimine los derechos de uso de un documento PDF con derechos activados mediante la API de extensiones de Acrobat Reader DC (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-reader-extensions-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto cliente de extensiones de Acrobat Reader DC.

   Cree un objeto `ReaderExtensionsServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Recupere un documento PDF.

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF con derechos activados mediante su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Elimine los derechos de uso del documento PDF.

   Elimine los derechos de uso del documento PDF invocando el método `ReaderExtensionsServiceClient` del objeto `removeUsageRights` y pasando el objeto `com.adobe.idp.Document` que contiene el documento PDF con derechos activados. Este método devuelve un objeto `com.adobe.idp.Document` que contiene un documento PDF que no tiene derechos de uso.

1. Aplique derechos de uso al documento PDF.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea .PDF.
   * Invoque el método `Document` del objeto `copyToFile` para copiar el contenido del objeto `Document` en el archivo (asegúrese de utilizar el objeto `Document` que devolvió el método `removeUsageRights`).

**Consulte también**

[Eliminación de derechos de uso de documentos PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Inicio rápido (modo SOAP): Eliminación de derechos de uso de un documento PDF mediante la API de Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminación de los derechos de uso mediante la API de servicio web {#remove-usage-rights-using-the-web-service-api}

Elimine los derechos de uso de un documento PDF con derechos activados mediante la API de extensiones de Acrobat Reader DC (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto cliente de extensiones de Acrobat Reader DC.

   * Cree un objeto `ReaderExtensionsServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `ReaderExtensionsServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Asegúrese de especificar `?blob=mtom`.)
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `ReaderExtensionsServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
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
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición de inicio y la longitud de flujo para leer.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Elimine los derechos de uso del documento PDF.

   Elimine los derechos de uso del documento PDF invocando el método `ReaderExtensionsServiceClient` del objeto `removeUsageRights` y pasando el objeto `BLOB` que contiene el documento PDF con derechos activados. Este método devuelve un objeto `BLOB` que contiene un documento PDF que no tiene derechos de uso.

1. Aplique derechos de uso al documento PDF.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo PDF.
   * Cree una matriz de bytes que almacene el contenido de datos del objeto `BLOB` que el método `removeUsageRights` devolvió. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.

**Consulte también**

[Eliminación de derechos de uso de documentos PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Recuperación de información de credenciales {#retrieving-credential-information}

Puede recuperar información sobre las credenciales que se usaron para aplicar derechos de uso a un documento PDF con derechos activados. Al recuperar información sobre una credencial, puede obtener información como la fecha después de la cual el certificado ya no es válido.

>[!NOTE]
>
>Para obtener más información sobre el servicio de extensiones de Acrobat Reader DC, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-2}

Para recuperar información sobre las credenciales utilizadas para aplicar derechos de uso a un documento PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto cliente de extensiones de Acrobat Reader DC.
1. Recupere un documento PDF con derechos activados.
1. Recupere información sobre las credenciales.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un objeto cliente de extensiones de Acrobat Reader DC**

Para poder realizar una operación de servicio de extensiones de Acrobat Reader DC mediante programación, debe crear un objeto cliente de servicio de extensiones de Acrobat Reader DC. Si utiliza la API de Java, cree un objeto `ReaderExtensionsServiceClient`. Si utiliza la API de servicio web de extensiones de Acrobat Reader DC, cree un objeto `ReaderExtensionsServiceService`.

**Recuperar un documento PDF con derechos activados**

Debe recuperar un documento PDF con derechos activados para recuperar información sobre la credencial. También puede recuperar información sobre una credencial especificando su alias; sin embargo, si desea recuperar información sobre una credencial que se utilizó para aplicar derechos de uso a un documento PDF con derechos activados específicos, debe recuperar el documento.

**Recuperar información sobre la credencial**

Después de recuperar un documento PDF con derechos activados, puede obtener información sobre la credencial que se utilizó para aplicarle derechos de uso. Puede obtener la siguiente información sobre las credenciales:

* Mensaje que se muestra en Adobe Reader cuando se abre el documento PDF con derechos activados.
* La fecha después de la cual la credencial ya no es válida.
* La fecha antes de la cual la credencial no es válida.
* Los derechos de uso establecidos para este documento PDF con derechos activados.
* Número de veces que se ha utilizado la credencial.

**Consulte también**

[Eliminación de los derechos de uso mediante la API de Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Eliminación de los derechos de uso mediante la API de servicio web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Extensiones de Acrobat Reader DC](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Recuperar información de credenciales mediante la API de Java {#retrieve-credential-information-using-the-java-api}

Recupere información de credenciales utilizando la API de extensiones de Acrobat Reader DC (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-reader-extensions-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto cliente de extensiones de Acrobat Reader DC.

   Cree un objeto `ReaderExtensionsServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Recupere un documento PDF.

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF con derechos activados mediante su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF con derechos activados.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Elimine los derechos de uso del documento PDF.

   * Recupere información sobre las credenciales utilizadas para aplicar derechos de uso al documento PDF invocando el método `ReaderExtensionsServiceClient` del objeto `getDocumentUsageRights` y pasando el objeto `com.adobe.idp.Document` que contiene el documento PDF con derechos activados. Este método devuelve un objeto `GetUsageRightsResult` que contiene información de credenciales.
   * Recupere la fecha después de la cual la credencial ya no es válida invocando el método `GetUsageRightsResult` del objeto `getNotAfter`. Este método devuelve un objeto `java.util.Date` que representa la fecha después de la cual la credencial ya no es válida.
   * Recupere el mensaje que se muestra en Adobe Reader cuando se abre el documento PDF con derechos activados invocando el método `GetUsageRightsResult` del objeto `getMessage`. Este método devuelve un valor de cadena que representa el mensaje.

**Consulte también**

[Recuperación de información Credencial](assigning-usage-rights.md#retrieving-credential-information)

[Inicio rápido (modo SOAP): Recuperación de información de credenciales mediante la API de Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar información de credenciales mediante la API de servicio web {#retrieve-credential-information-using-the-web-service-api}

Recupere información de credenciales mediante la API de extensiones de Acrobat Reader DC (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto cliente de extensiones de Acrobat Reader DC.

   * Cree un objeto `ReaderExtensionsServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `ReaderExtensionsServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Asegúrese de especificar `?blob=mtom`.)
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `ReaderExtensionsServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
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
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición de inicio y la longitud de flujo para leer.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Elimine los derechos de uso del documento PDF.

   * Recupere información sobre las credenciales utilizadas para aplicar derechos de uso al documento PDF invocando el método `ReaderExtensionsServiceClient` del objeto `getDocumentUsageRights` y pasando el objeto `com.adobe.idp.Document` que contiene el documento PDF con derechos activados. Este método devuelve un objeto `GetUsageRightsResult` que contiene información de credenciales.
   * Recupere la fecha después de la cual la credencial ya no es válida obteniendo el valor del miembro de datos `GetUsageRightsResult` del objeto `notAfter`. El tipo de datos de este miembro de datos es `System.DateTime`.
   * Recupere el mensaje que se muestra cuando se abre el documento PDF con derechos activados en Adobe Reader obteniendo el valor del miembro de datos `GetUsageRightsResult` del objeto `message`. El tipo de datos de este miembro de datos es una cadena.
   * Recupere el número de veces que se utiliza la credencial obteniendo el valor del miembro de datos `GetUsageRightsResult` del objeto `useCount`. El tipo de datos de este miembro de datos es un número entero.

**Consulte también**

[Recuperación de información Credencial](assigning-usage-rights.md#retrieving-credential-information)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
