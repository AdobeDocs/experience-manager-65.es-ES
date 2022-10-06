---
title: Asignación de derechos de uso
seo-title: Assigning Usage Rights
description: Utilice la API de cliente Java y la API de servicio web de Acrobat Reader DC Extensions para aplicar y eliminar los derechos de uso de los documentos del PDF.
seo-description: Use the Acrobat Reader DC extensions Java Client API and Web Service API to apply and remove usage rights from PDF documents.
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
role: Developer
exl-id: 6af148eb-427a-4b54-9c5f-8750736882d8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3926'
ht-degree: 0%

---

# Asignación de derechos de uso {#assigning-usage-rights}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

## Acerca del servicio de extensiones de Acrobat Reader DC {#about-the-acrobat-reader-dc-extensions-service}

El servicio de extensiones de Acrobat Reader DC permite a su organización compartir fácilmente documentos de PDF interactivos mediante la ampliación de la funcionalidad de Adobe Reader. El servicio de extensiones de Acrobat Reader DC es totalmente compatible con cualquier documento de PDF, hasta el PDF 1.7 incluido. Funciona con Adobe Reader 7.0 y versiones posteriores. El servicio agrega derechos de uso a un documento de PDF, activando funciones que normalmente no están disponibles cuando se abre un documento de PDF con Adobe Reader. Los usuarios de terceros no necesitan software ni complementos adicionales para trabajar con los documentos habilitados para derechos.

Puede realizar estas tareas mediante el servicio de extensiones de Acrobat Reader DC:

* Aplique derechos de uso a documentos de PDF. Para obtener más información, consulte [Aplicación de derechos de uso a documentos de PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).
* Elimine los derechos de uso de los documentos del PDF. Para obtener más información, consulte [Eliminación de derechos de uso de documentos de PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).
* Recupere detalles de credenciales. Para obtener más información, consulte [Recuperación de información Credencial](assigning-usage-rights.md#retrieving-credential-information).

>[!NOTE]
>
>Para obtener más información sobre el servicio de extensiones de Acrobat Reader DC, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Aplicación de derechos de uso a documentos de PDF {#applying-usage-rights-to-pdf-documents}

Puede aplicar derechos de uso a documentos de PDF mediante la API de cliente Java y el servicio web de Acrobat Reader DC Extensions. Los derechos de uso pertenecen a funciones que están disponibles de forma predeterminada en Acrobat pero no en Adobe Reader, como la capacidad de agregar comentarios a un formulario o de rellenar los campos del formulario y guardar el formulario. Los documentos del PDF que tienen derechos de uso aplicados se denominan documentos habilitados para derechos. Un usuario que abre un documento con derechos activados en Adobe Reader puede realizar operaciones que estén habilitadas para ese documento específico.

>[!NOTE]
>
>Al aplicar derechos de uso a documentos del PDF mediante la variable `applyUsageRights` , que forma parte de la API de Java, puede establecer la variable `isModeFinal` del parámetro `ReaderExtensionsOptionSpec` objeto a `false`. Esto hace que el contador procesado de formularios no se actualice y mejore el rendimiento. Si no le preocupa actualizar el contador procesado de formularios, se recomienda configurar la variable `isModeFinal` parámetro a `false`.

>[!NOTE]
>
>Para obtener más información sobre el servicio de extensiones de Acrobat Reader DC, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para aplicar derechos de uso a un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto cliente de extensiones de Acrobat Reader DC.
1. Recupere un documento de PDF.
1. Especifique los derechos de uso que desea aplicar.
1. Aplique derechos de uso al documento del PDF.
1. Guarde el documento de PDF habilitado para derechos.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un objeto cliente de extensiones de Acrobat Reader DC**

Para realizar una operación de servicio de Acrobat Reader DC Extensions mediante programación, debe crear un objeto cliente de servicio de Acrobat Reader DC Extensions. Si utiliza la API de Java de las extensiones de Acrobat Reader DC, cree un `ReaderExtensionsServiceClient` objeto. Si utiliza la API del servicio web de extensiones de Acrobat Reader DC, cree un `ReaderExtensionsServiceService` objeto.

**Recuperar un documento PDF**

Debe recuperar un documento de PDF para aplicar derechos de uso. Los documentos de PDF habilitados para derechos contienen un diccionario de derechos de uso. Cuando Adobe Reader abre un documento que contiene ese diccionario, habilita los derechos de uso especificados en el diccionario solo para ese documento. Si el documento no contiene un diccionario de derechos de uso, el servicio de extensiones de Acrobat Reader DC crea uno. Si ya contiene un diccionario, el servicio de extensiones de Acrobat Reader DC sobrescribe los derechos de uso existentes con los que especifique. El diccionario especifica qué derechos de uso están habilitados. Cuando un usuario abre el documento en Adobe Reader, solo se permiten los derechos de uso especificados en el diccionario.

**Especificar derechos de uso para aplicar**

Los derechos de uso que puede establecer están determinados por una credencial que compra en Adobe Systems Incorporated. Normalmente, las credenciales proporcionan permiso para establecer un grupo de derechos de uso relacionados, como los que pertenecen a formularios interactivos. Cada credencial proporciona el derecho de crear un determinado número de documentos PDF habilitados para derechos. Las credenciales de evaluación dan derecho a crear un número ilimitado de borradores de documentos.

>[!NOTE]
>
>Si intenta asignar un derecho de uso no permitido por las credenciales, provocará una excepción.

**Aplicar derechos de uso al documento del PDF**

Para aplicar derechos de uso a un documento de PDF, se hace referencia al alias de la credencial que se utiliza para aplicar derechos de uso (normalmente se instala una credencial durante la instalación de AEM Forms). También debe especificar el documento de PDF al que se aplican los derechos de uso. Para obtener información sobre la configuración de credenciales, consulte la guía de instalación e implementación para el servidor de aplicaciones.

**Guarde el documento de PDF con derechos activados**

Una vez que el servicio de extensiones de Acrobat Reader DC aplique derechos de uso a un documento de PDF, puede guardar el documento de PDF habilitado para derechos como un archivo de PDF.

**Consulte también lo siguiente**

[Aplicación de derechos de uso mediante la API de Java](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[Aplicar derechos de uso mediante la API de servicio web](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Extensiones de Acrobat Reader DC](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Aplicación de derechos de uso mediante la API de Java {#apply-usage-rights-using-the-java-api}

Aplique derechos de uso a un documento de PDF utilizando la API de extensiones de Acrobat Reader DC (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-reader-extensions-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto cliente de extensiones de Acrobat Reader DC.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `ReaderExtensionsServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recupere un documento de PDF.

   * Cree un `java.io.FileInputStream` objeto que representa el documento PDF utilizando su constructor y pasando un valor de cadena que especifica la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Especifique los derechos de uso que desea aplicar.

   * Cree un `UsageRights` objeto que representa derechos de uso mediante su constructor.
   * Para cada derecho de uso que se deba aplicar, invoque un método correspondiente que pertenece a la variable `UsageRights` objeto. Por ejemplo, para agregar la variable `enableFormFillIn` derecho de uso, invocar el `UsageRights` del objeto `enableFormFillIn` método y pase `true`. (Repita este paso para cada derecho de uso que desee aplicar).

1. Aplique derechos de uso al documento del PDF.

   * Cree un `ReaderExtensionsOptionSpec` usando su constructor. Este objeto contiene opciones en tiempo de ejecución que requiere el servicio de extensiones de Acrobat Reader DC. Al invocar este constructor, debe especificar los siguientes valores:

      * La variable `UsageRights` objeto que contiene los derechos de uso que se aplicarán al documento.
      * Valor de cadena que especifica un mensaje que un usuario ve cuando se abre el documento PDF con derechos activados en Adobe Reader 7.x. Este mensaje no se muestra en Adobe Reader 8.0.
   * Aplique derechos de uso al documento del PDF invocando la variable `ReaderExtensionsServiceClient` del objeto `applyUsageRights` y pasando los siguientes valores:

      * La variable `com.adobe.idp.Document` objeto que contiene el documento del PDF al que se aplican los derechos de uso.
      * Un valor de cadena que especifica el alias de la credencial que le permite aplicar derechos de uso.
      * Un valor de cadena que especifica el valor de contraseña correspondiente. (Actualmente se ignora este parámetro. Puede pasar `null`.)
   * La variable `ReaderExtensionsOptionSpec` que contiene opciones de tiempo de ejecución.

   La variable `applyUsageRights` el método devuelve un `com.adobe.idp.Document` objeto que contiene el documento PDF con derechos activados.

1. Guarde el documento de PDF habilitado para derechos.

   * Cree un `java.io.File` y asegúrese de que la extensión de archivo es .pdf.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `com.adobe.idp.Document` al archivo (asegúrese de usar la variable `com.adobe.idp.Document` objeto devuelto por el `applyUsageRights` método).

**Consulte también lo siguiente**

[Aplicación de derechos de uso a documentos de PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Inicio rápido (modo SOAP):Aplicación de derechos de uso mediante la API de Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aplicar derechos de uso mediante la API de servicio web {#apply-usage-rights-using-the-web-service-api}

Aplique derechos de uso a un documento de PDF mediante la API de extensiones de Acrobat Reader DC (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto cliente de extensiones de Acrobat Reader DC.

   * Cree un `ReaderExtensionsServiceClient` usando su constructor predeterminado.
   * Cree un `ReaderExtensionsServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Asegúrese de especificar `?blob=mtom`.)
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `ReaderExtensionsServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere un documento de PDF.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar un documento de PDF al que se aplican derechos de uso.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` método. Pase la matriz de bytes, la posición de inicio y la longitud del flujo para leerlos.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Especifique los derechos de uso que desea aplicar.

   * Cree un `UsageRights` objeto que representa derechos de uso mediante su constructor.
   * Para cada derecho de uso a aplicar, asigne el valor `true` al miembro de datos correspondiente que pertenece al grupo `UsageRights` objeto. Por ejemplo, para agregar la variable `enableFormFillIn` derecho de uso, asignar `true` a `UsageRights` del objeto `enableFormFillIn` miembro de datos. (Repita este paso para cada derecho de uso que desee aplicar).

1. Aplique derechos de uso al documento del PDF.

   * Cree un `ReaderExtensionsOptionSpec` usando su constructor. Este objeto contiene opciones en tiempo de ejecución que requiere el servicio de extensiones de Acrobat Reader DC.
   * Asigne la variable `UsageRights` al `ReaderExtensionsOptionSpec` del objeto `usageRights` miembro de datos.
   * Asigne un valor de cadena que especifique el mensaje que ve un usuario cuando se abre en Adobe Reader el documento PDF con derechos activados al `ReaderExtensionsOptionSpec` del objeto `message` miembro de datos.
   * Aplique derechos de uso al documento del PDF invocando la variable `ReaderExtensionsServiceClient` del objeto `applyUsageRights` y pasando los siguientes valores:

      * La variable `BLOB` objeto que contiene el documento del PDF al que se aplican los derechos de uso.
      * Un valor de cadena que especifica el alias de la credencial que le permite aplicar derechos de uso.
      * Un valor de cadena que especifica el valor de contraseña correspondiente. (Actualmente se ignora este parámetro. Puede pasar `null`.)
   * La variable `ReaderExtensionsOptionSpec` que contiene opciones de tiempo de ejecución.

   La variable `applyUsageRights` el método devuelve un `BLOB` objeto que contiene el documento PDF con derechos activados.

1. Guarde el documento de PDF habilitado para derechos.

   * Cree un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento de PDF con derechos activados.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto devuelto por el `applyUsageRights` método. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` miembro de datos.
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Aplicación de derechos de uso a documentos de PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Eliminación de derechos de uso de documentos de PDF {#removing-usage-rights-from-pdf-documents}

Puede quitar derechos de uso de un documento con derechos activados. También es necesario eliminar los derechos de uso de un documento PDF habilitado para derechos para realizar otras operaciones de AEM Forms en él. Por ejemplo, debe firmar digitalmente (o certificar) un documento PDF antes de establecer los derechos de uso. Por lo tanto, si desea realizar operaciones en un documento con derechos activados, debe eliminar los derechos de uso del documento PDF, realizar las demás operaciones, como firmar digitalmente el documento y, a continuación, volver a aplicar los derechos de uso al documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio de extensiones de Acrobat Reader DC, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para eliminar los derechos de uso de un documento de PDF habilitado para derechos, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto cliente de extensiones de Acrobat Reader DC.
1. Recupere un documento PDF con derechos activados.
1. Elimine los derechos de uso del documento del PDF.
1. Guarde el documento del PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un objeto cliente de extensiones de Acrobat Reader DC**

Para poder realizar una operación de servicio de extensiones de Acrobat Reader DC mediante programación, debe crear un objeto cliente de servicio de extensiones de Acrobat Reader DC. Si utiliza la API de Java, cree un `ReaderExtensionsServiceClient` objeto. Si utiliza la API del servicio web de extensiones de Acrobat Reader DC, cree un `ReaderExtensionsServiceService` objeto.

**Recuperar un documento de PDF con derechos activados**

Recupere un documento de PDF habilitado para derechos para eliminar los derechos de uso.

**Eliminación de los derechos de uso del documento del PDF**

Después de recuperar un documento de PDF habilitado para derechos, puede eliminar los derechos de uso. Después de eliminar los derechos de uso, el documento PDF no tendrá ninguna funcionalidad adicional mientras se vea dentro de Adobe Reader.

**Guardar el documento del PDF**

Puede guardar el documento del PDF que ya no contiene derechos de uso como archivo del PDF. Una vez guardado como archivo de PDF, el documento de PDF se puede ver en Adobe Reader o Acrobat.

**Consulte también lo siguiente**

[Eliminación de los derechos de uso mediante la API de Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Eliminación de los derechos de uso mediante la API de servicio web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Extensiones de Acrobat Reader DC](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[Aplicación de derechos de uso a documentos de PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Eliminación de los derechos de uso mediante la API de Java {#remove-usage-rights-using-the-java-api}

Elimine los derechos de uso de un documento de PDF habilitado para derechos mediante la API de extensiones de Acrobat Reader DC (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-reader-extensions-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto cliente de extensiones de Acrobat Reader DC.

   Cree un `ReaderExtensionsServiceClient` usando su constructor y pasando un `ServiceClientFactory` objeto que contiene propiedades de conexión.

1. Recupere un documento de PDF.

   * Cree un `java.io.FileInputStream` que representan el documento PDF habilitado para derechos mediante el uso de su constructor y pasando un valor de cadena que especifica la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Elimine los derechos de uso del documento del PDF.

   Elimine los derechos de uso del documento del PDF invocando la variable `ReaderExtensionsServiceClient` del objeto `removeUsageRights` y pasando el `com.adobe.idp.Document` objeto que contiene el documento PDF con derechos activados. Este método devuelve un `com.adobe.idp.Document` objeto que contiene un documento de PDF que no tiene derechos de uso.

1. Aplique derechos de uso al documento del PDF.

   * Cree un `java.io.File` y asegúrese de que la extensión de archivo es .PDF.
   * Invocar el `Document` del objeto `copyToFile` para copiar el contenido del `Document` al archivo (asegúrese de usar la variable `Document` objeto devuelto por el `removeUsageRights` método).

**Consulte también lo siguiente**

[Eliminación de derechos de uso de documentos de PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Inicio rápido (modo SOAP): Eliminación de derechos de uso de un documento de PDF mediante la API de Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminación de los derechos de uso mediante la API de servicio web {#remove-usage-rights-using-the-web-service-api}

Elimine los derechos de uso de un documento PDF habilitado para derechos mediante la API de extensiones de Acrobat Reader DC (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto cliente de extensiones de Acrobat Reader DC.

   * Cree un `ReaderExtensionsServiceClient` usando su constructor predeterminado.
   * Cree un `ReaderExtensionsServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Asegúrese de especificar `?blob=mtom`.)
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `ReaderExtensionsServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere un documento de PDF.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar el documento PDF con derechos activados del que se eliminan los derechos de uso.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Elimine los derechos de uso del documento del PDF.

   Elimine los derechos de uso del documento del PDF invocando la variable `ReaderExtensionsServiceClient` del objeto `removeUsageRights` y pasando el `BLOB` objeto que contiene el documento PDF con derechos activados. Este método devuelve un `BLOB` objeto que contiene un documento de PDF que no tiene derechos de uso.

1. Aplique derechos de uso al documento del PDF.

   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo PDF.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto devuelto por el `removeUsageRights` método. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` miembro de datos.
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.

**Consulte también lo siguiente**

[Eliminación de derechos de uso de documentos de PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Recuperación de información Credencial {#retrieving-credential-information}

Puede recuperar información sobre las credenciales que se usaron para aplicar derechos de uso a un documento PDF con derechos activados. Al recuperar información sobre una credencial, puede obtener información como la fecha después de la cual el certificado ya no es válido.

>[!NOTE]
>
>Para obtener más información sobre el servicio de extensiones de Acrobat Reader DC, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-2}

Para recuperar información sobre las credenciales utilizadas para aplicar derechos de uso a un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto cliente de extensiones de Acrobat Reader DC.
1. Recupere un documento PDF con derechos activados.
1. Recupere información sobre las credenciales.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un objeto cliente de extensiones de Acrobat Reader DC**

Para poder realizar una operación de servicio de extensiones de Acrobat Reader DC mediante programación, debe crear un objeto cliente de servicio de extensiones de Acrobat Reader DC. Si utiliza la API de Java, cree un `ReaderExtensionsServiceClient` objeto. Si utiliza la API del servicio web de extensiones de Acrobat Reader DC, cree un `ReaderExtensionsServiceService` objeto.

**Recuperar un documento de PDF con derechos activados**

Debe recuperar un documento PDF con derechos activados para recuperar información sobre las credenciales. También puede recuperar información sobre una credencial especificando su alias; sin embargo, si desea recuperar información sobre una credencial que se utilizó para aplicar derechos de uso a un documento PDF específico con derechos activados, debe recuperar el documento.

**Recuperar información sobre la credencial**

Después de recuperar un documento de PDF habilitado para derechos, puede obtener información sobre las credenciales que se usaron para aplicarle derechos de uso. Puede obtener la siguiente información sobre las credenciales:

* Mensaje que se muestra en Adobe Reader cuando se abre el documento PDF con derechos activados.
* La fecha después de la cual la credencial ya no es válida.
* La fecha antes de la cual la credencial no es válida.
* Los derechos de uso establecidos para este documento de PDF con derechos activados.
* Número de veces que se ha utilizado la credencial.

**Consulte también lo siguiente**

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

   Cree un `ReaderExtensionsServiceClient` usando su constructor y pasando un `ServiceClientFactory` objeto que contiene propiedades de conexión.

1. Recupere un documento de PDF.

   * Cree un `java.io.FileInputStream` que representan el documento PDF habilitado para derechos mediante el uso de su constructor y pasando un valor de cadena que especifica la ubicación del documento PDF habilitado para derechos.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Elimine los derechos de uso del documento del PDF.

   * Recupere información sobre las credenciales utilizadas para aplicar derechos de uso al documento del PDF invocando la variable `ReaderExtensionsServiceClient` del objeto `getDocumentUsageRights` y pasando el `com.adobe.idp.Document` objeto que contiene el documento PDF con derechos activados. Este método devuelve un `GetUsageRightsResult` objeto que contiene información de credenciales.
   * Recupere la fecha después de la cual la credencial ya no es válida invocando la variable `GetUsageRightsResult` del objeto `getNotAfter` método. Este método devuelve un `java.util.Date` que representa la fecha después de la cual la credencial ya no es válida.
   * Recupere el mensaje que se muestra en Adobe Reader cuando se abre el documento del PDF con derechos activados invocando el `GetUsageRightsResult` del objeto `getMessage` método. Este método devuelve un valor de cadena que representa el mensaje.

**Consulte también lo siguiente**

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
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto cliente de extensiones de Acrobat Reader DC.

   * Cree un `ReaderExtensionsServiceClient` usando su constructor predeterminado.
   * Cree un `ReaderExtensionsServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Asegúrese de especificar `?blob=mtom`.)
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `ReaderExtensionsServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere un documento de PDF.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar un documento PDF con derechos activados.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF con derechos activados y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Elimine los derechos de uso del documento del PDF.

   * Recupere información sobre las credenciales utilizadas para aplicar derechos de uso al documento del PDF invocando la variable `ReaderExtensionsServiceClient` del objeto `getDocumentUsageRights` y pasando el `com.adobe.idp.Document` objeto que contiene el documento PDF con derechos activados. Este método devuelve un `GetUsageRightsResult` objeto que contiene información de credenciales.
   * Recupere la fecha después de la cual la credencial ya no es válida obteniendo el valor de la variable `GetUsageRightsResult` del objeto `notAfter` miembro de datos. El tipo de datos de este miembro de datos es `System.DateTime`.
   * Recupere el mensaje que se muestra cuando se abre el documento del PDF con derechos activados en Adobe Reader obteniendo el valor de `GetUsageRightsResult` del objeto `message` miembro de datos. El tipo de datos de este miembro de datos es una cadena.
   * Recupere el número de veces que se utiliza la credencial obteniendo el valor de la variable `GetUsageRightsResult` del objeto `useCount` miembro de datos. El tipo de datos de este miembro de datos es un número entero.

**Consulte también lo siguiente**

[Recuperación de información Credencial](assigning-usage-rights.md#retrieving-credential-information)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
