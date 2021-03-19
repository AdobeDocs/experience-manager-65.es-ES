---
title: Conversión de PDF a archivos Postscript e Image
seo-title: Conversión de PDF a archivos Postscript e Image
description: Utilice el servicio Convertir PDF para convertir documentos PDF a PostScript y a varios formatos de imagen (JPEG, JPEG 2000, PNG y TIFF) mediante la API de Java y la API de servicio Web.
seo-description: Utilice el servicio Convertir PDF para convertir documentos PDF a PostScript y a varios formatos de imagen (JPEG, JPEG 2000, PNG y TIFF) mediante la API de Java y la API de servicio Web.
uuid: 07da0391-7180-4197-aaa6-ae753d753b84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f8707752-2c83-461a-b83d-708754b0f3f6
role: Desarrollador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2847'
ht-degree: 0%

---


# Conversión de PDF a archivos de imagen y Postscript {#converting-pdf-to-postscript-andimage-files}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

**Acerca del servicio Convertir PDF**

El servicio Convertir PDF convierte los documentos PDF a PostScript y a varios formatos de imagen (JPEG, JPEG 2000, PNG y TIFF). La conversión de un documento PDF a PostScript es útil para la impresión desatendida basada en servidor en cualquier impresora PostScript. La conversión de un documento PDF en un archivo TIFF de varias páginas es práctica cuando se archivan documentos en sistemas de administración de contenido que no admiten documentos PDF.

Puede realizar estas tareas mediante el servicio Convertir PDF:

* Convertir documentos PDF a PostScript.
* Convierta documentos PDF a formatos de imagen.

>[!NOTE]
>
>Para obtener más información sobre el servicio Convertir PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversión de documentos PDF a PostScript {#converting-pdf-documents-to-postscript}

En este tema se describe cómo utilizar la API Convertir servicio PDF (Java y servicio Web) para convertir documentos PDF en archivos PostScript mediante programación. El documento PDF que se convierte en un archivo PostScript debe ser un documento PDF no interactivo. Es decir, si intenta convertir un documento PDF interactivo en un archivo PostScript, se produce una excepción.

>[!NOTE]
>
>Para obtener más información sobre el servicio Convertir PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para convertir un documento PDF en un archivo PostScript, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio Convert PDF.
1. Haga referencia al documento PDF para convertirlo en un archivo PostScript.
1. Establezca las opciones de tiempo de ejecución de la conversión.
1. Convierta el documento PDF en un archivo PostScript.
1. Guarde el archivo PostScript.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente Convertir PDF**

Para poder realizar mediante programación una operación del servicio Convertir PDF, debe crear un cliente de servicio Convertir PDF. Si utiliza la API de Java, cree un objeto `ConvertPdfServiceClient`. Si utiliza la API de servicio web, cree un objeto `ConvertPDFServiceService`.

Esta sección utiliza la funcionalidad de servicio web que se introduce en AEM Forms. Para acceder a la nueva funcionalidad, debe construir el objeto proxy utilizando el atributo `lc_version` . (Consulte &quot;Acceso a la nueva funcionalidad mediante servicios web&quot; en [Invocación de AEM Forms mediante servicios web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)).

**Hacer referencia al documento PDF para convertirlo en un archivo PostScript**

Haga referencia al documento PDF que desea convertir en un archivo PostScript. Como se ha indicado anteriormente en este tema, el documento PDF debe ser un documento PDF no interactivo. Si intenta convertir un documento PDF interactivo en un archivo PostScript, se produce una excepción.

**Definir opciones de tiempo de ejecución de conversión**

Al convertir un documento PDF en un archivo PostScript, puede definir opciones en tiempo de ejecución que especifiquen el tipo de PostScript que se crea. Por ejemplo, puede definir un archivo PostScript de nivel 3.

Normalmente, el archivo PostScript generado reflejará el tamaño del documento PDF de entrada. Si selecciona la opción `ShrinkToFit` (que reduce la salida del archivo PostScript para que se ajuste a la página), no verá ninguna diferencia entre el documento PDF de entrada y el archivo PostScript generado. La opción `ShrinkToFit` sólo surte efecto si selecciona imprimir en un tamaño de página menor que el documento PDF de entrada. Para seleccionar un tamaño de página más pequeño, defina la opción `PageSize`. Además, se recomienda establecer la opción `RotateAndCenter` en `true` para obtener la salida correcta de PostScript.

Del mismo modo, si selecciona la opción `ExpandToFit` (que amplía la salida del archivo PostScript para que se ajuste a la página), tendrá efecto únicamente si selecciona imprimir en un tamaño de página mayor que el documento PDF de entrada. Para seleccionar un tamaño de página mayor, defina la opción `PageSize`. Además, se recomienda establecer la opción `RotateAndCenter` en `true` para obtener la salida correcta de PostScript.

>[!NOTE]
>
>Para obtener información sobre los valores en tiempo de ejecución que puede establecer, consulte la referencia de clase `ToPSOptionsSpec` en [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Convertir el documento PDF en un archivo PostScript**

Después de crear el cliente de servicio y establecer las opciones de tiempo de ejecución, puede invocar la operación de conversión PostScript. Esta operación necesitará información sobre el documento a convertir, incluido el nivel de PostScript preferido para el documento de destino.

**Guarde el archivo PostScript**

Después de convertir el documento PDF a PostScript, puede guardar la salida como un archivo PostScript.

**Consulte también**

[Convertir un documento PDF a PS mediante la API de Java](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[Convertir un documento PDF a PS mediante la API de servicio web](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Convertir inicio rápido de la API del servicio PDF](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Convertir un documento PDF a PS mediante la API de Java {#convert-a-pdf-document-to-ps-using-the-java-api}

Convertir un documento PDF a PostScript mediante la Convertir API de servicio PDF (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-convertpdf-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente Convertir PDF.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `ConvertPdfServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Haga referencia al documento PDF para convertirlo en un archivo PostScript.

   * Cree un objeto `java.io.FileInputStream` utilizando su constructor y pase un valor de cadena que especifique la ubicación del documento PDF que desea convertir.
   * Cree un objeto `com.adobe.idp.Document` que almacene el documento PDF utilizando el constructor `com.adobe.idp.Document`. Pase el objeto `java.io.FileInputStream` que contiene el documento PDF.

1. Establezca las opciones de tiempo de ejecución de la conversión.

   * Cree un objeto `ToPSOptionsSpec` invocando su constructor.
   * Defina las opciones en tiempo de ejecución invocando un método apropiado que pertenece al objeto `ToPSOptionsSpec`. Por ejemplo, para definir el nivel PostScript que se crea, invoque el método `ToPSOptionsSpec` del objeto `setPsLevel` y pase un valor de enumeración `PSLevel` que especifique el nivel PostScript. Para obtener información sobre todos los valores en tiempo de ejecución que puede establecer, consulte la referencia de clase `ToPSOptionsSpec` en [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Convierta el documento PDF en un archivo PostScript.

   Invoque el método `ConvertPdfServiceClient`object `toPS2` y pase los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que representa el documento PDF que se va a convertir en un archivo PostScript.
   * Un objeto `ToPSOptionsSpec` que especifica las opciones de tiempo de ejecución de PostScript.

   El método `toPS2` devuelve un objeto `Document` que contiene el nuevo documento PostScript.

1. Guarde el archivo PostScript.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del nombre de archivo sea .ps.
   * Invoque el método `Document` del objeto `copyToFile` para copiar el contenido del objeto `Document` en el archivo (asegúrese de utilizar el objeto `Document` que devolvió el método `toPS2`).

**Consulte también**

[Resumen de los pasos](converting-pdf-postscript-image-files.md#summary-of-steps)

[Inicio rápido (modo SOAP): Conversión de un documento PDF a PostScript mediante la API de Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir un documento PDF a PS mediante la API de servicio web {#convert-a-pdf-document-to-ps-using-the-web-service-api}

Convertir un documento PDF a PostScript mediante la Convertir API de servicio PDF (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente Convertir PDF.

   * Cree un objeto `ConvertPdfServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `ConvertPdfServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`). No es necesario utilizar el atributo `lc_version`. Sin embargo, especifique `?blob=mtom`.
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `ConvertPdfServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia al documento PDF para convertirlo en un archivo PostScript.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar un documento PDF que se convierte en un archivo PostScript.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF que desea convertir y el modo en el que desea abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición de inicio y la longitud de flujo para leerlos.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Establezca las opciones de tiempo de ejecución de la conversión.

   * Cree un objeto `ToPSOptionsSpec` invocando su constructor.
   * Defina las opciones en tiempo de ejecución asignando un valor al miembro de datos del objeto `ToPSOptionsSpec`. Por ejemplo, para definir el nivel PostScript que se crea, asigne un valor de enumeración `PSLevel` al miembro de datos `ToPSOptionsSpec` del objeto `psLevel`.

1. Convierta el documento PDF en un archivo PostScript.

   Invoque el método `GeneratePDFServiceService` del objeto `toPS2` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento PDF que se va a convertir en un archivo PostScript
   * Un objeto `ToPSOptionsSpec` que especifica opciones en tiempo de ejecución

   Una vez finalizada la conversión, extraiga los datos binarios que representan el documento PostScript accediendo a la propiedad `BLOB` del objeto `MTOM`. Esto devuelve una matriz de bytes que puede escribir en un archivo PostScript.

1. Guarde el archivo PostScript.

   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo PS.
   * Cree una matriz de bytes que almacene el contenido de datos del objeto `BLOB` que el método `encryptPDFUsingPassword` devolvió. Rellene la matriz de bytes obteniendo el valor del campo `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en el archivo PostScript invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](converting-pdf-postscript-image-files.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Conversión de documentos PDF a formatos de imagen {#converting-pdf-documents-to-image-formats}

Puede utilizar el servicio Convertir PDF para convertir documentos PDF mediante programación a formatos de imagen, que incluyen JPEG, JPEG 2000, TIFF y PNG. Al convertir un documento PDF en un archivo de imagen, puede utilizar el documento PDF como archivo de imagen. Por ejemplo, puede colocar la imagen en un sistema de administración de contenido empresarial para su almacenamiento.

Al convertir un documento PDF en una imagen, el servicio Convertir PDF crea una imagen independiente para cada página del documento. Es decir, si el documento tiene 20 páginas, el servicio Convertir PDF crea 20 archivos de imagen. Al convertir un documento PDF en un formato de imagen, se pueden crear imágenes individuales para cada página del documento PDF o un solo archivo de imagen para todo el documento PDF.

>[!NOTE]
>
>Para obtener más información sobre el servicio Convertir PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para convertir un documento PDF en cualquiera de los tipos admitidos, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio Convert PDF.
1. Recupere el documento PDF que desea convertir.
1. Establezca las opciones de tiempo de ejecución.
1. Convierta el PDF en una imagen.
1. Recupere los archivos de imagen de una colección.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente Convertir PDF**

Para poder realizar mediante programación una operación del servicio Convertir PDF, debe crear un cliente de servicio Convertir PDF. Si utiliza la API de Java, cree un objeto `ConvertPdfServiceClient`. Si utiliza la API de servicio web, cree un objeto `ConvertPDFServiceService`.

**Recupere el documento PDF que desea convertir**

Debe recuperar el documento PDF para convertir en una imagen. No se puede convertir un documento PDF interactivo en una imagen. Si intenta hacerlo, se genera una excepción. Para convertir un documento PDF interactivo en un archivo de imagen, debe acoplar el documento PDF antes de convertirlo. (Consulte [Acoplamiento de documentos PDF](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents)).

**Establecer opciones de tiempo de ejecución**

Debe establecer opciones en tiempo de ejecución como el formato de imagen y los valores de resolución. Para obtener información sobre los valores en tiempo de ejecución, consulte la referencia de clase `ToImageOptionsSpec` en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Convertir el PDF en una imagen**

Después de crear el cliente de servicio y establecer las opciones de tiempo de ejecución, puede convertir el documento PDF en una imagen. Se devuelve un objeto de colección que contiene las imágenes.

**Recuperar los archivos de imagen de una colección**

Puede recuperar archivos de imagen de un objeto de colección que devuelva el servicio Convertir PDF. Cada elemento de la colección es una instancia `com.adobe.idp.Document` (o una instancia `BLOB` si utiliza servicios web) que puede guardar como un archivo de imagen, como un archivo JPG.

El formato del archivo de imagen depende de la opción `ImageConvertFormat` durante la ejecución. Es decir, si establece la opción `ImageConvertFormat` tiempo de ejecución en `ImageConvertFormat.JPEG`, puede guardar archivos de imagen como archivos JPG.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Convertir inicio rápido de la API del servicio PDF](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Conversión de un documento PDF en archivos de imagen mediante la API de Java {#convert-a-pdf-document-to-image-files-using-the-java-api}

Convertir un documento PDF en un formato de imagen mediante la Convertir API de servicio PDF (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-convertpdf-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente Convertir PDF.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `ConvertPdfServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Recupere el documento PDF que desea convertir.

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF que desea convertir empleando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Establezca las opciones de tiempo de ejecución.

   * Cree un objeto `ToImageOptionsSpec` utilizando su constructor.
   * Invoque los métodos que pertenezcan a este objeto según sea necesario. Por ejemplo, para configurar el tipo de imagen, invoque el método `setImageConvertFormat` y pase un valor de enumeración `ImageConvertFormat` que especifique el tipo de formato.

   >[!NOTE]
   >
   >La configuración del valor de la enumeración `ImageConvertFormat` es obligatoria.

1. Convierta el PDF en una imagen.

   Invoque el método `ConvertPdfServiceClient` del objeto `toImage2` y pase los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que representa el archivo PDF que se va a convertir.
   * Un objeto `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` que contiene las distintas preferencias sobre el formato de imagen de destino.

   El método `toImage2` devuelve un objeto `java.util.List` que contiene imágenes. Cada elemento de la colección es una instancia `com.adobe.idp.Document`.

1. Recupere los archivos de imagen de una colección.

   Itere a través del objeto `java.util.List` para determinar si las imágenes están presentes. Cada elemento es una instancia `com.adobe.idp.Document`. Guarde la imagen invocando el método `com.adobe.idp.Document` del objeto `copyToFile` y pasando un objeto `java.io.File`.

**Consulte también**

[Inicio rápido (modo SOAP): Conversión de un documento PDF en archivos JPEG mediante la API de Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### Conversión de un documento PDF en archivos de imagen mediante la API de servicio Web {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

Convertir un documento PDF en un formato de imagen mediante la Convertir API de servicio PDF (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente PDF de conversión.

   * Cree un objeto `ConvertPdfServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `ConvertPdfServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`). No es necesario utilizar el atributo `lc_version`. Sin embargo, especifique `?blob=mtom`.
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `ConvertPdfServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere el documento PDF que desea convertir.

   * Cree un objeto `BLOB` utilizando su constructor. Este objeto `BLOB` se utiliza para almacenar el formulario PDF.
   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que especifique la ubicación del formulario PDF y el modo en el que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Determine el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read`. Pase la matriz de bytes, la posición de inicio y la longitud del flujo para leerlos.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Establezca las opciones de tiempo de ejecución.

   * Cree un objeto `ToImageOptionsSpec` utilizando su constructor.
   * Invoque los métodos que pertenezcan a este objeto según sea necesario. Por ejemplo, para configurar el tipo de imagen, invoque el método `setImageConvertFormat` y pase un valor de enumeración `ImageConvertFormat` que especifique el tipo de formato.

   >[!NOTE]
   >
   >La configuración del valor de la enumeración `ImageConvertFormat` es obligatoria.

1. Convierta el PDF en una imagen.

   Invoque el método `ConvertPDFServiceService` del objeto `toImage2` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el archivo que se va a convertir
   * Un objeto `ToImageOptionsSpec` que contiene las distintas preferencias sobre el formato de imagen de destino

   El método `toImage2` devuelve un objeto `MyArrayOfBLOB` que contiene los archivos de imagen recién creados.

1. Recupere los archivos de imagen de una colección.

   * Determine el número de elementos del objeto `MyArrayOfBLOB` obteniendo el valor de su campo `Count`. Cada elemento es un objeto `BLOB` que contiene la imagen.
   * Itere a través del objeto `MyArrayOfBLOB` y guarde cada archivo de imagen.

**Consulte también**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
