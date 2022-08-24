---
title: Conversión de PDF a archivos Postscript e Image
seo-title: Converting PDF to Postscript andImage Files
description: Utilice el servicio Convertir PDF para convertir documentos de PDF a PostScript y a varios formatos de imagen (JPEG, JPEG 2000, PNG y TIFF) mediante la API de Java y la API de servicio web.
seo-description: Use the Convert PDF service to convert PDF documents to PostScript and to a number of image formats (JPEG, JPEG 2000, PNG, and TIFF) using the Java API and Web Service API.
uuid: 07da0391-7180-4197-aaa6-ae753d753b84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f8707752-2c83-461a-b83d-708754b0f3f6
role: Developer
exl-id: 31730c24-46c3-4111-9391-ccd4342740e9
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2809'
ht-degree: 0%

---

# Conversión de PDF a archivos de imagen y Postscript {#converting-pdf-to-postscript-andimage-files}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

**Acerca del servicio Convertir PDF**

El servicio Convertir PDF convierte los documentos de PDF a PostScript y a varios formatos de imagen (JPEG, JPEG 2000, PNG y TIFF). La conversión de un documento PDF a PostScript es útil para la impresión desatendida basada en servidor en cualquier impresora PostScript. La conversión de un documento de PDF en un archivo de TIFF de varias páginas es práctica cuando se archivan documentos en sistemas de administración de contenido que no admiten documentos de PDF.

Puede realizar estas tareas mediante el servicio Convertir PDF:

* Convertir documentos PDF a PostScript.
* Convierta documentos PDF a formatos de imagen.

>[!NOTE]
>
>Para obtener más información sobre el servicio Convertir PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversión de documentos PDF a PostScript {#converting-pdf-documents-to-postscript}

En este tema se describe cómo utilizar la API Convertir servicio de PDF (Java y servicio web) para convertir mediante programación documentos de PDF en archivos PostScript. El documento PDF que se convierte en un archivo PostScript debe ser un documento PDF no interactivo. Es decir, si intenta convertir un documento PDF interactivo en un archivo PostScript, se genera una excepción.

>[!NOTE]
>
>Para obtener más información sobre el servicio Convertir PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para convertir un documento de PDF en un archivo PostScript, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio Convertir PDF.
1. Haga referencia al documento del PDF para convertirlo en un archivo PostScript.
1. Establezca las opciones de tiempo de ejecución de la conversión.
1. Convierta el documento PDF en un archivo PostScript.
1. Guarde el archivo PostScript.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente de PDF de conversión**

Para poder realizar mediante programación una operación de servicio Convertir PDF, debe crear un cliente de servicio Convertir PDF. Si utiliza la API de Java, cree un `ConvertPdfServiceClient` objeto. Si utiliza la API de servicio web, cree un `ConvertPDFServiceService` objeto.

Esta sección utiliza la funcionalidad de servicio web que se introduce en AEM Forms. Para acceder a la nueva funcionalidad, debe construir el objeto proxy utilizando la variable `lc_version` atributo. (Consulte &quot;Acceso a la nueva funcionalidad mediante servicios web&quot; en [Invocación de AEM Forms mediante servicios web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

**Haga referencia al documento del PDF para convertirlo en un archivo PostScript**

Haga referencia al documento PDF que desea convertir en un archivo PostScript. Como se ha indicado anteriormente en este tema, el documento de PDF debe ser un documento de PDF no interactivo. Si intenta convertir un documento PDF interactivo en un archivo PostScript, se genera una excepción.

**Definir opciones de tiempo de ejecución de conversión**

Al convertir un documento PDF en un archivo PostScript, puede definir opciones en tiempo de ejecución que especifiquen el tipo de PostScript que se crea. Por ejemplo, puede definir un archivo PostScript de nivel 3.

Normalmente, el archivo PostScript generado reflejará el tamaño del documento del PDF de entrada. Si selecciona la opción `ShrinkToFit` (que reduce la salida del archivo PostScript para que se ajuste a la página), no verá ninguna diferencia entre el documento del PDF de entrada y el archivo PostScript generado. La variable `ShrinkToFit` sólo surte efecto si selecciona imprimir en un tamaño de página menor que el documento del PDF de entrada. Para seleccionar un tamaño de página más pequeño, defina la variable `PageSize` . Además, se recomienda configurar la variable `RotateAndCenter` a `true` para obtener la salida PostScript correcta.

Del mismo modo, si selecciona la variable `ExpandToFit` (que expande la salida del archivo PostScript para que se ajuste a la página), solo surte efecto si selecciona imprimir en un tamaño de página mayor que el documento del PDF de entrada. Para seleccionar un tamaño de página mayor, defina la variable `PageSize` . Además, se recomienda configurar la variable `RotateAndCenter` a `true` para obtener la salida PostScript correcta.

>[!NOTE]
>
>Para obtener información sobre los valores de tiempo de ejecución que puede establecer, consulte la `ToPSOptionsSpec` referencia de clase en [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Convertir el documento PDF en un archivo PostScript**

Después de crear el cliente de servicio y establecer las opciones de tiempo de ejecución, puede invocar la operación de conversión PostScript. Esta operación necesitará información sobre el documento a convertir, incluido el nivel de PostScript preferido para el documento de destino.

**Guarde el archivo PostScript**

Después de convertir el documento de PDF a PostScript, puede guardar la salida como un archivo PostScript.

**Consulte también lo siguiente**

[Convertir un documento PDF a PS mediante la API de Java](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[Convertir un documento PDF a PS mediante la API de servicio web](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Convertir inicio rápido de la API del servicio de PDF](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Convertir un documento PDF a PS mediante la API de Java {#convert-a-pdf-document-to-ps-using-the-java-api}

Convertir un documento de PDF a PostScript mediante la Convertir API de servicio de PDF (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-convertpdf-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente Convertir PDF.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `ConvertPdfServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia al documento del PDF para convertirlo en un archivo PostScript.

   * Cree un `java.io.FileInputStream` mediante su constructor y pase un valor de cadena que especifica la ubicación del documento PDF que se va a convertir.
   * Cree un `com.adobe.idp.Document` objeto que almacena el documento del PDF utilizando la variable `com.adobe.idp.Document` constructor. Pase el `java.io.FileInputStream` objeto que contiene el documento PDF.

1. Establezca las opciones de tiempo de ejecución de la conversión.

   * Cree un `ToPSOptionsSpec` invocando su constructor.
   * Configure las opciones en tiempo de ejecución invocando un método apropiado que pertenece al `ToPSOptionsSpec` objeto. Por ejemplo, para definir el nivel PostScript que se crea, invoque la variable `ToPSOptionsSpec` del objeto `setPsLevel` método y pasar una `PSLevel` valor de enumeración que especifica el nivel PostScript. Para obtener información sobre todos los valores de tiempo de ejecución que puede establecer, consulte la `ToPSOptionsSpec` referencia de clase en [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Convierta el documento PDF en un archivo PostScript.

   Invocar el `ConvertPdfServiceClient`del objeto `toPS2` y pase los siguientes valores:

   * A `com.adobe.idp.Document` que representa el documento PDF que se va a convertir en un archivo PostScript.
   * A `ToPSOptionsSpec` objeto que especifica las opciones de tiempo de ejecución de PostScript.

   La variable `toPS2` el método devuelve un `Document` que contiene el nuevo documento PostScript.

1. Guarde el archivo PostScript.

   * Cree un `java.io.File` y asegúrese de que la extensión de nombre de archivo es .ps.
   * Invocar el `Document` del objeto `copyToFile` para copiar el contenido del `Document` al archivo (asegúrese de usar la variable `Document` objeto devuelto por el `toPS2` método).

**Consulte también lo siguiente**

[Resumen de los pasos](converting-pdf-postscript-image-files.md#summary-of-steps)

[Inicio rápido (modo SOAP): Conversión de un documento de PDF a PostScript mediante la API de Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir un documento PDF a PS mediante la API de servicio web {#convert-a-pdf-document-to-ps-using-the-web-service-api}

Convertir un documento de PDF a PostScript mediante la API Convertir servicio de PDF (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente Convertir PDF.

   * Cree un `ConvertPdfServiceClient` usando su constructor predeterminado.
   * Cree un `ConvertPdfServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) No es necesario que use la variable `lc_version` atributo. Sin embargo, especifique `?blob=mtom`.
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `ConvertPdfServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia al documento del PDF para convertirlo en un archivo PostScript.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar un documento PDF que se convierte en un archivo PostScript.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF a convertir y el modo en el que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Establezca las opciones de tiempo de ejecución de la conversión.

   * Cree un `ToPSOptionsSpec` invocando su constructor.
   * Configure las opciones en tiempo de ejecución asignando un valor a la variable `ToPSOptionsSpec` miembro de datos del objeto. Por ejemplo, para definir el nivel PostScript que se crea, asigne un `PSLevel` valor de enumeración a la variable `ToPSOptionsSpec` del objeto `psLevel` miembro de datos.

1. Convierta el documento PDF en un archivo PostScript.

   Invocar el `GeneratePDFServiceService` del objeto `toPS2` y pase los siguientes valores:

   * A `BLOB` objeto que representa el documento PDF que se va a convertir en un archivo PostScript
   * A `ToPSOptionsSpec` objeto que especifica opciones en tiempo de ejecución

   Una vez finalizada la conversión, extraiga los datos binarios que representan el documento PostScript accediendo a su `BLOB` del objeto `MTOM` propiedad. Esto devuelve una matriz de bytes que puede escribir en un archivo PostScript.

1. Guarde el archivo PostScript.

   * Cree un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo PS.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto devuelto por el `encryptPDFUsingPassword` método. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` campo .
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en el archivo PostScript invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Resumen de los pasos](converting-pdf-postscript-image-files.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Conversión de documentos del PDF a formatos de imagen {#converting-pdf-documents-to-image-formats}

Puede utilizar el servicio Convertir PDF para convertir mediante programación documentos PDF a formatos de imagen, que incluyen JPEG, JPEG 2000, TIFF y PNG. Al convertir un documento PDF en un archivo de imagen, puede utilizar el documento PDF como archivo de imagen. Por ejemplo, puede colocar la imagen en un sistema de administración de contenido empresarial para su almacenamiento.

Al convertir un documento PDF en una imagen, el servicio Convertir PDF crea una imagen independiente para cada página del documento. Es decir, si el documento tiene 20 páginas, el servicio Convertir PDF crea 20 archivos de imagen. Al convertir un documento PDF a un formato de imagen, puede crear imágenes individuales para cada página dentro del documento PDF o un archivo de imagen único para todo el documento PDF.

>[!NOTE]
>
>Para obtener más información sobre el servicio Convertir PDF, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para convertir un documento de PDF en cualquiera de los tipos admitidos, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio Convertir PDF.
1. Recupere el documento del PDF que desea convertir.
1. Establezca las opciones de tiempo de ejecución.
1. Convierta el PDF en una imagen.
1. Recupere los archivos de imagen de una colección.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente de PDF de conversión**

Para poder realizar mediante programación una operación de servicio Convertir PDF, debe crear un cliente de servicio Convertir PDF. Si utiliza la API de Java, cree un `ConvertPdfServiceClient` objeto. Si utiliza la API de servicio web, cree un `ConvertPDFServiceService` objeto.

**Recupere el documento del PDF para convertir**

Debe recuperar el documento PDF para convertir en una imagen. No se puede convertir un documento PDF interactivo en una imagen. Si intenta hacerlo, se genera una excepción. Para convertir un documento PDF interactivo en un archivo de imagen, debe acoplar el documento PDF antes de convertirlo. (Consulte [Acoplamiento de documentos del PDF](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents).)

**Establecer opciones de tiempo de ejecución**

Debe establecer opciones en tiempo de ejecución como el formato de imagen y los valores de resolución. Para obtener información sobre los valores de tiempo de ejecución, consulte la `ToImageOptionsSpec` referencia de clase en [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Convertir el PDF en una imagen**

Después de crear el cliente de servicio y establecer las opciones de tiempo de ejecución, puede convertir el documento del PDF en una imagen. Se devuelve un objeto de colección que contiene las imágenes.

**Recuperar los archivos de imagen de una colección**

Puede recuperar archivos de imagen de un objeto de colección que devuelva el servicio Convertir PDF. Cada elemento de la colección es un `com.adobe.idp.Document` instancia (o una `BLOB` instancia si utiliza servicios web) que puede guardar como archivo de imagen, como un archivo de JPG.

El formato del archivo de imagen depende del `ImageConvertFormat` durante la ejecución. Es decir, si configura la variable `ImageConvertFormat` opción de tiempo de ejecución a `ImageConvertFormat.JPEG`, puede guardar archivos de imagen como archivos JPG.

**Consulte también lo siguiente**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Convertir inicio rápido de la API del servicio de PDF](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Conversión de un documento PDF en archivos de imagen mediante la API de Java {#convert-a-pdf-document-to-image-files-using-the-java-api}

Convertir un documento PDF a un formato de imagen mediante la Convertir API de servicio PDF (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-convertpdf-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente Convertir PDF.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `ConvertPdfServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recupere el documento del PDF que desea convertir.

   * Cree un `java.io.FileInputStream` objeto que representa el documento PDF que se va a convertir utilizando su constructor y pasando un valor de cadena que especifica la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Establezca las opciones de tiempo de ejecución.

   * Cree un `ToImageOptionsSpec` usando su constructor.
   * Invoque los métodos que pertenezcan a este objeto según sea necesario. Por ejemplo, para configurar el tipo de imagen, invoque la variable `setImageConvertFormat` método y pasar un `ImageConvertFormat` valor enum que especifica el tipo de formato.

   >[!NOTE]
   >
   >Configuración de la variable `ImageConvertFormat` el valor de enumeración es obligatorio.

1. Convierta el PDF en una imagen.

   Invocar el `ConvertPdfServiceClient` del objeto `toImage2` y pase los siguientes valores:

   * A `com.adobe.idp.Document` que representa el archivo PDF que se va a convertir.
   * A `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` objeto que contiene las distintas preferencias sobre el formato de imagen de destino.

   La variable `toImage2` el método devuelve un `java.util.List` objeto que contiene imágenes. Cada elemento de la colección es un `com.adobe.idp.Document` instancia.

1. Recupere los archivos de imagen de una colección.

   Iterar a través de la variable `java.util.List` para determinar si las imágenes están presentes. Cada elemento es un `com.adobe.idp.Document` instancia. Guarde la imagen invocando `com.adobe.idp.Document` del objeto `copyToFile` método y pasar una `java.io.File` objeto.

**Consulte también lo siguiente**

[Inicio rápido (modo SOAP): Conversión de un documento de PDF en archivos de JPEG mediante la API de Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### Conversión de un documento PDF en archivos de imagen mediante la API de servicio web {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

Convertir un documento PDF a un formato de imagen mediante la Convertir API de servicio PDF (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de PDF de conversión.

   * Cree un `ConvertPdfServiceClient` usando su constructor predeterminado.
   * Cree un `ConvertPdfServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) No es necesario que use la variable `lc_version` atributo. Sin embargo, especifique `?blob=mtom`.
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `ConvertPdfServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere el documento del PDF que desea convertir.

   * Cree un `BLOB` usando su constructor. Esta `BLOB` se utiliza para almacenar el formulario de PDF.
   * Cree un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que especifique la ubicación del formulario del PDF y el modo en el que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Determine el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` método. Pase la matriz de bytes, la posición de inicio y la longitud del flujo para leerlos.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Establezca las opciones de tiempo de ejecución.

   * Cree un `ToImageOptionsSpec` usando su constructor.
   * Invoque los métodos que pertenezcan a este objeto según sea necesario. Por ejemplo, para configurar el tipo de imagen, invoque la variable `setImageConvertFormat` método y pasar un `ImageConvertFormat` valor de enumeración que especifica el tipo de formato.

   >[!NOTE]
   >
   >Configuración de la variable `ImageConvertFormat` el valor de enumeración es obligatorio.

1. Convierta el PDF en una imagen.

   Invocar el `ConvertPDFServiceService` del objeto `toImage2` y pase los siguientes valores:

   * A `BLOB` objeto que representa el archivo que se va a convertir
   * A `ToImageOptionsSpec` objeto que contiene las distintas preferencias sobre el formato de imagen de destino

   La variable `toImage2` el método devuelve un `MyArrayOfBLOB` que contiene los archivos de imagen recién creados.

1. Recupere los archivos de imagen de una colección.

   * Determine el número de elementos de la variable `MyArrayOfBLOB` obteniendo el valor de su `Count` campo . Cada elemento es un `BLOB` objeto que contiene la imagen.
   * Iterar a través de la variable `MyArrayOfBLOB` y guarde cada archivo de imagen.

**Consulte también lo siguiente**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
