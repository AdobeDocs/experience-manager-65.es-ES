---
title: Conversión de archivos PDF a archivos Postscript e Image
seo-title: Conversión de archivos PDF a archivos Postscript e Image
description: nulo
seo-description: nulo
uuid: 07da0391-7180-4197-aaa6-ae753d753b84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f8707752-2c83-461a-b83d-708754b0f3f6
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# Conversión de archivos PDF a archivos de imagen y postscript {#converting-pdf-to-postscript-andimage-files}

**Acerca del servicio Convertir PDF**

El servicio Convertir PDF convierte documentos PDF a PostScript y a varios formatos de imagen (JPEG, JPEG 2000, PNG y TIFF). Convertir un documento PDF a PostScript es útil para la impresión desatendida basada en servidor en cualquier impresora PostScript. Convertir un documento PDF en un archivo TIFF de varias páginas resulta práctico al archivar documentos en sistemas de administración de contenido que no admiten documentos PDF.

Puede realizar estas tareas mediante el servicio Convertir PDF:

* Convertir documentos PDF a PostScript.
* Convertir documentos PDF a formatos de imagen.

   ***Nota **: Para obtener más información sobre el servicio Convertir PDF, consulte Referencia de[servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).*

## Conversión de documentos PDF a PostScript {#converting-pdf-documents-to-postscript}

En este tema se describe cómo puede utilizar la API de conversión de servicio PDF (Java y servicio Web) para convertir documentos PDF en archivos PostScript mediante programación. El documento PDF que se convierte en un archivo PostScript debe ser un documento PDF no interactivo. Es decir, si intenta convertir un documento PDF interactivo en un archivo PostScript, se genera una excepción.

>[!NOTE]
>
> Para obtener más información sobre el servicio Convertir PDF, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para convertir un documento PDF en un archivo PostScript, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio Convertir PDF.
1. Haga referencia al documento PDF para convertirlo en un archivo PostScript.
1. Configure las opciones de tiempo de ejecución de conversión.
1. Convierta el documento PDF en un archivo PostScript.
1. Guarde el archivo PostScript.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Crear un cliente Convertir PDF**

Para poder realizar mediante programación una operación de servicio Convertir PDF, debe crear un cliente de servicio Convertir PDF. Si utiliza la API de Java, cree un `ConvertPdfServiceClient` objeto. Si utiliza la API de servicio Web, cree un `ConvertPDFServiceService` objeto.

En esta sección se utiliza la funcionalidad de servicio web que se introduce en AEM Forms. Para acceder a la nueva funcionalidad, debe construir el objeto proxy utilizando el `lc_version` atributo . (Consulte &quot;Acceso a nuevas funciones mediante servicios web&quot; en [Invocación de formularios AEM mediante servicios](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)web).

**Hacer referencia al documento PDF para convertirlo en un archivo PostScript**

Haga referencia al documento PDF que desea convertir en un archivo PostScript. Como se indicó anteriormente en este tema, el documento PDF debe ser un documento PDF no interactivo. Si intenta convertir un documento PDF interactivo en un archivo PostScript, se genera una excepción.

**Establecer las opciones de tiempo de ejecución de conversión**

Al convertir un documento PDF a un archivo PostScript, puede definir opciones en tiempo de ejecución que especifican el tipo de PostScript que se crea. Por ejemplo, puede definir un archivo PostScript de nivel 3.

Normalmente, el archivo PostScript generado reflejará el tamaño del documento PDF de entrada. Si selecciona la `ShrinkToFit` opción (que reduce la salida del archivo PostScript para que se ajuste a la página), no verá ninguna diferencia entre el documento PDF de entrada y el archivo PostScript generado. La `ShrinkToFit` opción solo se aplica si selecciona imprimir en un tamaño de página menor que el del documento PDF de entrada. Para seleccionar un tamaño de página más pequeño, defina la `PageSize` opción. Además, se recomienda configurar la `RotateAndCenter` opción para `true` obtener la salida PostScript correcta.

Del mismo modo, si selecciona la `ExpandToFit` opción (que expande la salida del archivo PostScript para que se ajuste a la página), solo surtirá efecto si selecciona imprimir en un tamaño de página mayor que el documento PDF de entrada. Para seleccionar un tamaño de página mayor, defina la `PageSize` opción. Además, se recomienda configurar la `RotateAndCenter` opción para `true` obtener la salida PostScript correcta.

>[!NOTE]
>
>Para obtener información sobre los valores en tiempo de ejecución que puede definir, consulte la referencia de la `ToPSOptionsSpec` clase en Referencia [de API de formularios](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM.

**Convertir el documento PDF en un archivo PostScript**

Después de crear el cliente de servicio y establecer las opciones de tiempo de ejecución, puede invocar la operación de conversión PostScript. Esta operación necesitará información sobre el documento que se va a convertir, incluido el nivel PostScript preferido para el documento de destino.

**Guardar el archivo PostScript**

Después de convertir el documento PDF a PostScript, puede guardar la salida como un archivo PostScript.

**Consulte también**

[Conversión de un documento PDF a PS mediante la API de Java](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[Convertir un documento PDF a PS mediante la API de servicio web](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Convertir inicios rápidos de API de servicio PDF](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Conversión de un documento PDF a PS mediante la API de Java {#convert-a-pdf-document-to-ps-using-the-java-api}

Conversión de un documento PDF a PostScript mediante la conversión de la API de servicio PDF (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-convertpdf-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente Convertir PDF.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `ConvertPdfServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia al documento PDF para convertirlo en un archivo PostScript.

   * Cree un `java.io.FileInputStream` objeto con su constructor y pase un valor de cadena que especifique la ubicación del documento PDF que se va a convertir.
   * Cree un `com.adobe.idp.Document` objeto que almacene el documento PDF mediante el `com.adobe.idp.Document` constructor. Pase el `java.io.FileInputStream` objeto que contiene el documento PDF.

1. Configure las opciones de tiempo de ejecución de conversión.

   * Cree un `ToPSOptionsSpec` objeto invocando su constructor.
   * Configure las opciones de tiempo de ejecución invocando un método adecuado que pertenece al `ToPSOptionsSpec` objeto. Por ejemplo, para definir el nivel PostScript que se crea, invoque el `ToPSOptionsSpec` método del `setPsLevel` objeto y pase un valor de `PSLevel` enumeración que especifique el nivel PostScript. Para obtener información sobre todos los valores en tiempo de ejecución que puede establecer, consulte la referencia de la `ToPSOptionsSpec` clase en Referencia [de API de formularios](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM.

1. Convierta el documento PDF en un archivo PostScript.

   Invoque el método del `ConvertPdfServiceClient`objeto y pase los `toPS2` valores siguientes:

   * Un `com.adobe.idp.Document` objeto que representa el documento PDF que se va a convertir en un archivo PostScript.
   * Un `ToPSOptionsSpec` objeto que especifica las opciones de tiempo de ejecución de PostScript.
   El `toPS2` método devuelve un `Document` objeto que contiene el nuevo documento PostScript.

1. Guarde el archivo PostScript.

   * Cree un `java.io.File` objeto y asegúrese de que la extensión del nombre de archivo sea .ps.
   * Invoque el `Document` método del `copyToFile` objeto para copiar el contenido del `Document` objeto en el archivo (asegúrese de utilizar el `Document` objeto devuelto por el `toPS2` método).

**Consulte también**

[Resumen de los pasos](converting-pdf-postscript-image-files.md#summary-of-steps)

[Inicio rápido (modo SOAP): Conversión de un documento PDF a PostScript mediante la API de Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir un documento PDF a PS mediante la API de servicio web {#convert-a-pdf-document-to-ps-using-the-web-service-api}

Conversión de un documento PDF a PostScript mediante la función Convertir API de servicio PDF (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente Convertir PDF.

   * Cree un `ConvertPdfServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `ConvertPdfServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) No es necesario usar el `lc_version` atributo. Sin embargo, especifique `?blob=mtom`.
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `ConvertPdfServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia al documento PDF para convertirlo en un archivo PostScript.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar un documento PDF que se convierte en un archivo PostScript.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF que se va a convertir y el modo en el que se va a abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.

1. Configure las opciones de tiempo de ejecución de conversión.

   * Cree un `ToPSOptionsSpec` objeto invocando su constructor.
   * Defina las opciones de tiempo de ejecución asignando un valor al miembro de datos del `ToPSOptionsSpec` objeto. Por ejemplo, para definir el nivel PostScript que se crea, asigne un valor de `PSLevel` enumeración al miembro de datos del `ToPSOptionsSpec` objeto `psLevel` .

1. Convierta el documento PDF en un archivo PostScript.

   Invoque el `GeneratePDFServiceService` método del `toPS2` objeto y pase los valores siguientes:

   * Un `BLOB` objeto que representa el documento PDF que se va a convertir en un archivo PostScript
   * Un `ToPSOptionsSpec` objeto que especifica opciones de tiempo de ejecución
   Una vez finalizada la conversión, extraiga los datos binarios que representan el documento PostScript accediendo a la `BLOB` propiedad del `MTOM` objeto. Esto devuelve una matriz de bytes que puede escribir en un archivo PostScript.

1. Guarde el archivo PostScript.

   * Cree un `System.IO.FileStream` objeto invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo PS.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto devuelto por el `encryptPDFUsingPassword` método. Rellene la matriz de bytes obteniendo el valor del `BLOB` campo del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en el archivo PostScript invocando el `System.IO.BinaryWriter` método del `Write` objeto y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](converting-pdf-postscript-image-files.md#summary-of-steps)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Conversión de documentos PDF a formatos de imagen {#converting-pdf-documents-to-image-formats}

Puede utilizar el servicio Convertir PDF para convertir documentos PDF en formatos de imagen mediante programación, como JPEG, JPEG 2000, TIFF y PNG. Al convertir un documento PDF en un archivo de imagen, puede utilizarlo como archivo de imagen. Por ejemplo, puede colocar la imagen en un sistema de administración de contenido empresarial para almacenamiento.

Al convertir un documento PDF en una imagen, el servicio Convertir PDF crea una imagen independiente para cada página del documento. Es decir, si el documento tiene 20 páginas, el servicio Convertir PDF crea 20 archivos de imagen. Al convertir un documento PDF a un formato de imagen, puede crear imágenes individuales para cada página del documento PDF o un solo archivo de imagen para todo el documento PDF.

>[!NOTE]
>
> Para obtener más información sobre el servicio Convertir PDF, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para convertir un documento PDF a cualquiera de los tipos admitidos, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio Convertir PDF.
1. Recupere el documento PDF que desea convertir.
1. Configure las opciones de tiempo de ejecución.
1. Convierta el PDF en una imagen.
1. Recupere los archivos de imagen de una colección.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Crear un cliente Convertir PDF**

Para poder realizar mediante programación una operación de servicio Convertir PDF, debe crear un cliente de servicio Convertir PDF. Si utiliza la API de Java, cree un `ConvertPdfServiceClient` objeto. Si utiliza la API de servicio Web, cree un `ConvertPDFServiceService` objeto.

**Recuperar el documento PDF para convertir**

Debe recuperar el documento PDF para convertir en una imagen. No se puede convertir un documento PDF interactivo en una imagen. Si intenta hacerlo, se genera una excepción. Para convertir un documento PDF interactivo a un archivo de imagen, debe acoplar el documento PDF antes de convertirlo. (Consulte [Acoplamiento de documentos](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents)PDF).

**Definición de opciones de tiempo de ejecución**

Debe definir opciones de tiempo de ejecución como el formato de imagen y los valores de resolución. Para obtener información sobre los valores en tiempo de ejecución, consulte la referencia de la `ToImageOptionsSpec` clase en Referencia [de API de formularios](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM.

**Convertir el PDF en una imagen**

Después de crear el cliente de servicio y definir las opciones de tiempo de ejecución, puede convertir el documento PDF en una imagen. Se devuelve un objeto de colección que contiene las imágenes.

**Recuperar los archivos de imagen de una colección**

Puede recuperar archivos de imagen de un objeto de colección que devuelve el servicio Convertir PDF. Cada elemento de la colección es una `com.adobe.idp.Document` instancia (o una `BLOB` instancia si utiliza servicios Web) que puede guardar como archivo de imagen, como un archivo JPG.

El formato del archivo de imagen depende de la opción de tiempo de `ImageConvertFormat` ejecución. Es decir, si establece la opción de tiempo de `ImageConvertFormat` ejecución en `ImageConvertFormat.JPEG`, puede guardar archivos de imagen como archivos JPG.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Convertir inicios rápidos de API de servicio PDF](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Convertir un documento PDF en archivos de imagen mediante la API de Java {#convert-a-pdf-document-to-image-files-using-the-java-api}

Convertir un documento PDF a un formato de imagen mediante la API de servicio Convertir PDF (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-convertpdf-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente Convertir PDF.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `ConvertPdfServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recupere el documento PDF que desea convertir.

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF que se va a convertir utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Configure las opciones de tiempo de ejecución.

   * Cree un `ToImageOptionsSpec` objeto con su constructor.
   * Invocar los métodos que pertenecen a este objeto según sea necesario. Por ejemplo, para establecer el tipo de imagen, invoque el `setImageConvertFormat` método y pase un valor `ImageConvertFormat` enum que especifique el tipo de formato.
   >[!NOTE]
   >
   >La configuración del valor de `ImageConvertFormat` enumeración es obligatoria.

1. Convierta el PDF en una imagen.

   Invoque el `ConvertPdfServiceClient` método del `toImage2` objeto y pase los valores siguientes:

   * Un `com.adobe.idp.Document` objeto que representa el archivo PDF que se va a convertir.
   * Un `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` objeto que contiene las distintas preferencias sobre el formato de imagen de destino.
   El `toImage2` método devuelve un `java.util.List` objeto que contiene imágenes. Cada elemento de la colección es una `com.adobe.idp.Document` instancia.

1. Recupere los archivos de imagen de una colección.

   Repita el `java.util.List` objeto para determinar si hay imágenes presentes. Cada elemento es una `com.adobe.idp.Document` instancia. Guarde la imagen invocando el `com.adobe.idp.Document` método del `copyToFile` objeto y pasando un `java.io.File` objeto.

**Consulte también**

[Inicio rápido (modo SOAP): Conversión de un documento PDF a archivos JPEG mediante la API de Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### Convertir un documento PDF en archivos de imagen mediante la API de servicio Web {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

Conversión de un documento PDF a un formato de imagen mediante la función Convertir API de servicio PDF (servicio Web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente PDF de conversión.

   * Cree un `ConvertPdfServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `ConvertPdfServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) No es necesario usar el `lc_version` atributo. Sin embargo, especifique `?blob=mtom`.
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `ConvertPdfServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere el documento PDF que desea convertir.

   * Cree un `BLOB` objeto con su constructor. Este `BLOB` objeto se utiliza para almacenar el formulario PDF.
   * Cree un `System.IO.FileStream` objeto invocando su constructor. Pase un valor de cadena que especifique la ubicación del formulario PDF y el modo en el que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.

1. Configure las opciones de tiempo de ejecución.

   * Cree un `ToImageOptionsSpec` objeto con su constructor.
   * Invocar los métodos que pertenecen a este objeto según sea necesario. Por ejemplo, para establecer el tipo de imagen, invoque el `setImageConvertFormat` método y pase un valor de enumeración `ImageConvertFormat` que especifique el tipo de formato.
   >[!NOTE]
   >
   >La configuración del valor de `ImageConvertFormat` enumeración es obligatoria.

1. Convierta el PDF en una imagen.

   Invoque el `ConvertPDFServiceService` método del `toImage2` objeto y pase los valores siguientes:

   * Un `BLOB` objeto que representa el archivo que se va a convertir
   * Un `ToImageOptionsSpec` objeto que contiene las distintas preferencias sobre el formato de imagen de destino
   El `toImage2` método devuelve un `MyArrayOfBLOB` objeto que contiene los archivos de imagen recién creados.

1. Recupere los archivos de imagen de una colección.

   * Determinar el número de elementos del `MyArrayOfBLOB` objeto obteniendo el valor de su `Count` campo. Cada elemento es un `BLOB` objeto que contiene la imagen.
   * Repita el `MyArrayOfBLOB` objeto y guarde cada archivo de imagen.

**Consulte también**

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
