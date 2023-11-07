---
title: Convertir archivos PDF a Postscript andImage
description: Utilice el servicio ConvertPDF para convertir documentos de PDF a PostScript y a varios formatos de imagen (JPEG, JPEG 2000, PNG y TIFF) mediante la API de Java y la API de servicio web.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 31730c24-46c3-4111-9391-ccd4342740e9
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2801'
ht-degree: 2%

---

# Conversión del PDF a archivos Postscript y de imagen {#converting-pdf-to-postscript-andimage-files}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

**Acerca del servicio Convertir PDF**

El servicio ConvertPDF convierte los documentos de PDF a PostScript y a varios formatos de imagen (JPEG, JPEG 2000, PNG y TIFF). Convertir un documento PDF a PostScript es útil para la impresión desatendida basada en servidor en cualquier impresora PostScript. Convertir un documento PDF en un archivo TIFF de varias páginas es práctico cuando se archivan documentos en sistemas de administración de contenido que no admiten documentos PDF.

Puede realizar estas tareas mediante el servicio Convert PDF:

* Convertir documentos PDF a PostScript.
* Convierta documentos de PDF a formatos de imagen.

>[!NOTE]
>
>Para obtener más información sobre el servicio ConvertPDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Convertir documentos de PDF a PostScript {#converting-pdf-documents-to-postscript}

En este tema se describe cómo se puede utilizar la API del servicio ConvertPDF (Java y servicio Web) para convertir mediante programación documentos de PDF en archivos PostScript. El documento de PDF convertido en un archivo PostScript debe ser un documento de PDF no interactivo. Es decir, si intenta convertir un documento PDF interactivo en un archivo PostScript, se genera una excepción.

>[!NOTE]
>
>Para obtener más información sobre el servicio ConvertPDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para convertir un documento de PDF en un archivo PostScript, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio del PDF Convert.
1. Hacer referencia al documento de PDF para convertirlo en un archivo PostScript.
1. Establecer las opciones de tiempo de ejecución de conversión.
1. Convierta el documento de PDF en un archivo PostScript.
1. Guarde el archivo PostScript.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un cliente PDF de conversión**

Para poder realizar mediante programación una operación de servicio ConvertPDF, debe crear un cliente de servicio ConvertPDF. Si utiliza la API de Java, cree un `ConvertPdfServiceClient` objeto. Si utiliza la API del servicio web, cree un `ConvertPDFServiceService` objeto.

Esta sección utiliza la funcionalidad de servicio web que se introduce en AEM Forms. Para acceder a la nueva funcionalidad, debe construir el objeto proxy utilizando `lc_version` atributo. (Consulte &quot;Acceso a la nueva funcionalidad mediante servicios web&quot; en [Invocar AEM Forms mediante servicios web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

**Hacer referencia al documento de PDF para convertirlo en un archivo PostScript**

Haga referencia al documento de PDF que desee convertir en un archivo PostScript. Como se ha indicado anteriormente en este tema, el documento de PDF debe ser un documento de PDF no interactivo. Si intenta convertir un documento PDF interactivo en un archivo PostScript, se producirá una excepción.

**Establecer opciones de tiempo de ejecución de conversión**

Al convertir un documento de PDF en un archivo PostScript, puede definir opciones en tiempo de ejecución que especifiquen el tipo PostScript que se crea. Por ejemplo, puede definir un archivo PostScript de nivel 3.

Normalmente, el archivo PostScript generado reflejará el tamaño del documento del PDF de entrada. Si selecciona la opción `ShrinkToFit` opción (que reduce la salida del archivo PostScript para que se ajuste a la página), no verá una diferencia entre el documento del PDF de entrada y el archivo PostScript generado. El `ShrinkToFit` se aplica únicamente si se selecciona imprimir en un tamaño de página menor que el documento del PDF de entrada. Para seleccionar un tamaño de página menor, defina la variable `PageSize` opción. Además, se recomienda configurar la variable `RotateAndCenter` opción para `true` para obtener la salida PostScript correcta.

Del mismo modo, si selecciona la `ExpandToFit` (que expande la salida del archivo PostScript para ajustarse a la página), sólo tendrá efecto si selecciona imprimir en un tamaño de página mayor que el documento del PDF de entrada. Para seleccionar un tamaño de página mayor, defina la variable `PageSize` opción. Además, se recomienda configurar la variable `RotateAndCenter` opción para `true` para obtener la salida PostScript correcta.

>[!NOTE]
>
>Para obtener información acerca de los valores en tiempo de ejecución que puede establecer, vea la `ToPSOptionsSpec` referencia de clase en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Conversión del documento de PDF en un archivo PostScript**

Después de crear el cliente de servicios y establecer las opciones en tiempo de ejecución, puede invocar la operación de conversión PostScript. Esta operación necesitará información sobre el documento que se va a convertir, incluido el nivel PostScript preferido para el documento de destino.

**Guarde el archivo PostScript**

Después de convertir el documento de PDF a PostScript, puede guardar la salida como un archivo PostScript.

**Consulte también**

[Conversión de un documento de PDF en PS mediante la API de Java](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[Conversión de un documento de PDF en PS mediante la API de servicio web](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API de ConvertPDF Service](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Conversión de un documento de PDF en PS mediante la API de Java {#convert-a-pdf-document-to-ps-using-the-java-api}

Conversión de un documento de PDF a PostScript mediante la API del servicio ConvertPDF (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-convertpdf-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente PDF de conversión.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `ConvertPdfServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Hacer referencia al documento de PDF para convertirlo en un archivo PostScript.

   * Crear un `java.io.FileInputStream` mediante su constructor y pase un valor de cadena que especifique la ubicación del documento de PDF que se va a convertir.
   * Crear un `com.adobe.idp.Document` que almacena el documento de PDF utilizando el objeto `com.adobe.idp.Document` constructor. Pase el `java.io.FileInputStream` que contiene el documento de PDF.

1. Establecer las opciones de tiempo de ejecución de conversión.

   * Crear un `ToPSOptionsSpec` invocando su constructor.
   * Establezca las opciones en tiempo de ejecución invocando un método apropiado que pertenezca a la variable `ToPSOptionsSpec` objeto. Por ejemplo, para definir el nivel de PostScript que se crea, invoque el `ToPSOptionsSpec` del objeto `setPsLevel` método y pase un `PSLevel` valor de enumeración que especifica el nivel PostScript. Para obtener información acerca de todos los valores en tiempo de ejecución que puede establecer, vea la `ToPSOptionsSpec` referencia de clase en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Convierta el documento de PDF en un archivo PostScript.

   Invoque el `ConvertPdfServiceClient`del objeto `toPS2` y pasar los siguientes valores:

   * A `com.adobe.idp.Document` que representa el documento de PDF que se va a convertir en un archivo PostScript.
   * A `ToPSOptionsSpec` que especifica las opciones de tiempo de ejecución de PostScript.

   El `toPS2` El método devuelve un valor `Document` que contiene el nuevo documento PostScript.

1. Guarde el archivo PostScript.

   * Crear un `java.io.File` y asegúrese de que la extensión del nombre de archivo es .ps.
   * Invoque el `Document` del objeto `copyToFile` para copiar el contenido del `Document` al archivo (asegúrese de utilizar la variable `Document` objeto que ha devuelto el `toPS2` método).

**Consulte también**

[Resumen de los pasos](converting-pdf-postscript-image-files.md#summary-of-steps)

[Inicio rápido (modo SOAP): Conversión de un documento de PDF a PostScript mediante la API de Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de un documento de PDF en PS mediante la API de servicio web {#convert-a-pdf-document-to-ps-using-the-web-service-api}

Conversión de un documento de PDF a PostScript mediante la API del servicio ConvertPDF (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente PDF de conversión.

   * Crear un `ConvertPdfServiceClient` mediante su constructor predeterminado.
   * Crear un `ConvertPdfServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) No es necesario que utilice el `lc_version` atributo. Sin embargo, especifique `?blob=mtom`.
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `ConvertPdfServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Hacer referencia al documento de PDF para convertirlo en un archivo PostScript.

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar un documento de PDF que se convierte en un archivo PostScript.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento de PDF que se va a convertir y el modo en que se va a abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de secuencia para que se lean.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.

1. Establecer las opciones de tiempo de ejecución de conversión.

   * Crear un `ToPSOptionsSpec` invocando su constructor.
   * Establezca las opciones en tiempo de ejecución asignando un valor a `ToPSOptionsSpec` miembro de datos del objeto. Por ejemplo, para definir el nivel de PostScript que se crea, asigne un `PSLevel` valor de enumeración para `ToPSOptionsSpec` del objeto `psLevel` miembro de datos.

1. Convierta el documento de PDF en un archivo PostScript.

   Invoque el `GeneratePDFServiceService` del objeto `toPS2` y pasar los siguientes valores:

   * A `BLOB` que representa el documento de PDF para convertirlo en un archivo PostScript
   * A `ToPSOptionsSpec` objeto que especifica opciones en tiempo de ejecución

   Una vez completada la conversión, extraiga los datos binarios que representan el documento PostScript accediendo a su `BLOB` del objeto `MTOM` propiedad. Devuelve una matriz de bytes que se puede escribir en un archivo PostScript.

1. Guarde el archivo PostScript.

   * Crear un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo PS.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto que ha devuelto el `encryptPDFUsingPassword` método. Rellene la matriz de bytes obteniendo el valor de `BLOB` del objeto `MTOM` field.
   * Crear un `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en el archivo PostScript invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](converting-pdf-postscript-image-files.md#summary-of-steps)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Conversión de documentos de PDF a formatos de imagen {#converting-pdf-documents-to-image-formats}

Puede utilizar el servicio PDF de conversión para convertir mediante programación documentos de PDF a formatos de imagen, que incluyen JPEG, JPEG 2000, TIFF y PNG. Al convertir un documento de PDF en un archivo de imagen, puede utilizar el documento de PDF como archivo de imagen. Por ejemplo, puede colocar la imagen en un sistema de administración de contenido empresarial para su almacenamiento.

Al convertir un documento de PDF en una imagen, el servicio ConvertPDF crea una imagen independiente para cada página del documento. Es decir, si el documento tiene 20 páginas, el servicio ConvertPDF crea 20 archivos de imagen. Al convertir un documento de PDF a un formato de imagen, puede crear imágenes individuales para cada página dentro del documento de PDF o un solo archivo de imagen para todo el documento de PDF.

>[!NOTE]
>
>Para obtener más información sobre el servicio ConvertPDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para convertir un documento de PDF en cualquiera de los tipos compatibles, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio del PDF Convert.
1. Recupere el documento del PDF que desea convertir.
1. Establecer opciones en tiempo de ejecución.
1. Convierta el PDF en una imagen.
1. Recupere los archivos de imagen de una colección.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un cliente PDF de conversión**

Para poder realizar mediante programación una operación de servicio ConvertPDF, debe crear un cliente de servicio ConvertPDF. Si utiliza la API de Java, cree un `ConvertPdfServiceClient` objeto. Si utiliza la API del servicio web, cree un `ConvertPDFServiceService` objeto.

**Recuperar el documento del PDF para convertirlo**

Recupere el documento del PDF para convertirlo en una imagen. No se puede convertir un documento interactivo de PDF en una imagen. Si intenta hacerlo, se produce una excepción. Para convertir un documento de PDF interactivo en un archivo de imagen, debe acoplar el documento de PDF antes de convertirlo. (Consulte [Acoplar documentos de PDF](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents).)

**Establecer opciones en tiempo de ejecución**

Establezca opciones en tiempo de ejecución como el formato de imagen y los valores de resolución. Para obtener información sobre los valores en tiempo de ejecución, vea la `ToImageOptionsSpec` referencia de clase en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Conversión del PDF en imagen**

Después de crear el cliente de servicios y establecer las opciones en tiempo de ejecución, puede convertir el documento de PDF en una imagen. Se devuelve un objeto de colección que contiene las imágenes.

**Recuperar los archivos de imagen de una colección**

Puede recuperar archivos de imagen de un objeto de colección devuelto por el servicio Convert PDF. Cada elemento de la colección es un `com.adobe.idp.Document` instancia de (o un `BLOB` ejemplo, si utiliza servicios web) que puede guardar como archivo de imagen, como un archivo de JPG.

El formato del archivo de imagen depende de la variable `ImageConvertFormat` en tiempo de ejecución. Es decir, si establece la variable `ImageConvertFormat` opción de tiempo de ejecución para `ImageConvertFormat.JPEG`, puede guardar archivos de imagen como archivos de JPG.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API de ConvertPDF Service](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Conversión de un documento de PDF en archivos de imagen mediante la API de Java {#convert-a-pdf-document-to-image-files-using-the-java-api}

Conversión de un documento de PDF a un formato de imagen mediante la API del servicio ConvertPDF (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-convertpdf-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente PDF de conversión.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `ConvertPdfServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Recupere el documento del PDF que desea convertir.

   * Crear un `java.io.FileInputStream` que representa el documento de PDF que se va a convertir utilizando su constructor y pasando un valor de cadena que especifica la ubicación del documento de PDF.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Establecer opciones en tiempo de ejecución.

   * Crear un `ToImageOptionsSpec` mediante su constructor.
   * Invoque los métodos que pertenezcan a este objeto según sea necesario. Por ejemplo, establezca el tipo de imagen invocando el método `setImageConvertFormat` método y pasar un `ImageConvertFormat` valor de enumeración que especifica el tipo de formato.

   >[!NOTE]
   >
   >Configuración de la `ImageConvertFormat` el valor de enumeración es obligatorio.

1. Convierta el PDF en una imagen.

   Invoque el `ConvertPdfServiceClient` del objeto `toImage2` y pasar los siguientes valores:

   * A `com.adobe.idp.Document` que representa el archivo PDF que se va a convertir.
   * A `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` que contiene las distintas preferencias sobre el formato de imagen de destino.

   El `toImage2` El método devuelve un valor `java.util.List` que contiene imágenes. Cada elemento de la colección es un `com.adobe.idp.Document` ejemplo.

1. Recupere los archivos de imagen de una colección.

   Itere a través de `java.util.List` para determinar si las imágenes están presentes. Cada elemento es un `com.adobe.idp.Document` ejemplo. Guarde la imagen invocando el `com.adobe.idp.Document` del objeto `copyToFile` método y pasar un `java.io.File` objeto.

**Consulte también**

[Inicio rápido (modo SOAP): Conversión de un documento de PDF a archivos de JPEG mediante la API de Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### Conversión de un documento de PDF en archivos de imagen mediante la API de servicio web {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

Conversión de un documento de PDF a un formato de imagen mediante la API del servicio ConvertPDF (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente PDF de conversión.

   * Crear un `ConvertPdfServiceClient` mediante su constructor predeterminado.
   * Crear un `ConvertPdfServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) No es necesario que utilice el `lc_version` atributo. Sin embargo, especifique `?blob=mtom`.
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `ConvertPdfServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere el documento del PDF que desea convertir.

   * Crear un `BLOB` mediante su constructor. Esta `BLOB` se utiliza para almacenar el formulario de PDF.
   * Crear un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que especifique la ubicación del formulario de PDF y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Determinar el tamaño de la matriz de bytes obteniendo `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` método. Pase a leer la matriz de bytes, la posición inicial y la longitud de la secuencia.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.

1. Establecer opciones en tiempo de ejecución.

   * Crear un `ToImageOptionsSpec` mediante su constructor.
   * Invoque los métodos que pertenezcan a este objeto según sea necesario. Por ejemplo, establezca el tipo de imagen invocando el método `setImageConvertFormat` método y pasar un `ImageConvertFormat` valor de enumeración que especifica el tipo de formato.

   >[!NOTE]
   >
   >Configuración de la `ImageConvertFormat` el valor de enumeración es obligatorio.

1. Convierta el PDF en una imagen.

   Invoque el `ConvertPDFServiceService` del objeto `toImage2` y pasar los siguientes valores:

   * A `BLOB` objeto que representa el archivo que se va a convertir
   * A `ToImageOptionsSpec` que contiene las distintas preferencias sobre el formato de imagen de destino

   El `toImage2` El método devuelve un valor `MyArrayOfBLOB` que contiene los archivos de imagen recién creados.

1. Recupere los archivos de imagen de una colección.

   * Determine el número de elementos en la `MyArrayOfBLOB` al obtener el valor de su `Count` field. Cada elemento es un `BLOB` que contiene la imagen.
   * Itere a través de `MyArrayOfBLOB` y guarde cada archivo de imagen.

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
