---
title: Trabajar con formularios con códigos de barras
seo-title: Working with barcoded forms
description: Descodificar datos de un formulario de PDF o una imagen que contenga un código de barras mediante la API de Java y la API de servicio web.
seo-description: Decode data from a PDF form or an image that contains a barcode using the Java API and Web Service API.
uuid: e56c3c94-384d-401f-b418-dd34cdc57eda
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: eb28ac30-265c-4611-8247-1f4bc826f254
role: Developer
exl-id: dd32808e-b773-48a2-90e1-7a277d349493
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '1920'
ht-degree: 0%

---

# Trabajar con formularios con códigos de barras {#working-with-barcoded-forms}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

## Acerca del servicio de formularios con códigos de barras {#about-the-barcoded-forms-service}

El servicio de formularios con códigos de barras automatiza la captura de datos de los formularios de cumplimentación e impresión e integra la información capturada en los sistemas informáticos principales de una organización.

Con el servicio de formularios con códigos de barras, puede agregar códigos de barras unidimensionales y bidimensionales a los PDF forms interactivos. A continuación, puede publicar los formularios con códigos de barras en un sitio web o distribuirlos por correo electrónico o CD. Cuando un usuario rellena un formulario con códigos de barras con Adobe Reader, Acrobat Professional o Acrobat Standard, el código de barras se actualiza automáticamente para codificar los datos del formulario proporcionados por el usuario. El usuario puede enviar el formulario electrónicamente o imprimirlo en papel y enviarlo por correo, fax o mano. Posteriormente, puede extraer los datos suministrados por el usuario como parte de un flujo de trabajo automatizado, y enrutar los datos entre procesos de aprobación y sistemas empresariales.

Para obtener más información sobre el servicio de formularios con códigos de barras, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Descodificación de datos de formulario con códigos de barras {#decoding-barcoded-form-data}

Puede utilizar la API del servicio de formularios con códigos de barras para descodificar datos de un formulario de PDF o de una imagen que contenga un código de barras. Descodificar datos de formulario significa extraer datos que se encuentran en el código de barras. Para poder descodificar los datos de un formulario (o imagen) de PDF, un usuario debe rellenar el formulario con datos.

>[!NOTE]
>
>Para obtener más información sobre el servicio de formularios con códigos de barras, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para descodificar datos de un formulario de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API formsClient con códigos de barras.
1. Obtenga un formulario de PDF que contenga datos con códigos de barras.
1. Descodificar los datos del formulario de PDF.
1. Convertir los datos en una fuente de datos XML.
1. Procese los datos descodificados.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben añadirse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)
* xercesImpl.jar (ubicado en &lt;install directory=&quot;&quot;>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\third-party)

Si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBOSS, deberá reemplazar adobe-utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que está implementado AEM Forms. Para obtener información sobre la ubicación de todos los archivos JAR de AEM Forms, consulte [Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un objeto de API de cliente de formularios con códigos de barras**

Para poder realizar mediante programación una operación de servicio de Forms con códigos de barras, debe crear un cliente de servicio de Forms con códigos de barras. Si utiliza la API de Java, cree un `BarcodedFormsServiceClient` objeto. Si utiliza la API del servicio web de formularios con códigos de barras, cree un `BarcodedFormsServiceService` objeto.

**Obtenga un formulario de PDF que contenga datos con códigos de barras**

Debe obtener un formulario de PDF que contenga un código de barras que se haya rellenado con datos de usuario.

**Descodificar los datos del formulario de PDF**

Después de obtener un formulario (o una imagen) de PDF que contiene un código de barras, puede descodificar los datos. El servicio de Forms con códigos de barras es compatible con los siguientes tipos de códigos de barras:

* Códigos de barras PDF 417.
* Códigos de barras de matriz de datos.
* Códigos de barras QR.
* Códigos de barras de Codabar.
* Código 128 códigos de barras.
* Código 39 códigos de barras.
* Códigos de barras EAN-13.
* Códigos de barras EAN-8.

La entrada de conjunto de caracteres como hexadecimal en la API de descodificación implica que el contenido del código de barras se codifica como una cadena hexadecimal. Por ejemplo, si se especifica UTF-8 como codificación de caracteres en el formulario y se especifica Hex en la operación de descodificación, el contenido del código de barras se codifica como una cadena Hex en el elemento &lt; `xb:content`> en la salida descodificada. Puede convertir este valor hexadecimal para obtener el contenido original creando lógica de aplicación en la aplicación cliente.

**Convertir los datos en una fuente de datos XML**

Después de descodificar los datos del formulario, puede convertirlos en datos XDP o XFDF. Por ejemplo, supongamos que desea importar los datos en otro formulario. Para importar los datos en un formulario XFA, debe convertirlos en datos XDP. Para obtener más información, consulte [Importación de datos de formulario](/help/forms/developing/importing-exporting-data.md#importing-form-data).

**Procesamiento de los datos descodificados**

Puede procesar los datos convertidos para satisfacer sus necesidades comerciales. Por ejemplo, después de descodificar y convertir los datos, puede guardarlos en un archivo, almacenarlos en una base de datos empresarial, rellenar otro formulario, etc. En esta sección se explica cómo guardar los datos convertidos como un archivo XML.

>[!NOTE]
>
>El servicio de Forms con códigos de barras no puede descodificar los datos de códigos de barras cuando los parámetros delimitador de línea y delimitador de campo tienen el mismo valor

**Consulte también**

[Descodificar datos de formulario con códigos de barras mediante la API de Java](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[Descodificar datos de formulario con códigos de barras mediante la API de servicio web](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Descodificar datos de formulario con códigos de barras mediante la API de Java {#decode-barcoded-form-data-using-the-java-api}

Descodificar datos de formulario mediante la API de formularios con códigos de barras (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente en la ruta de clase del proyecto Java.

1. Crear un objeto de API de cliente de formularios con códigos de barras

   Crear un `BarcodedFormsServiceClient` mediante su constructor y pasando un objeto `ServiceClientFactory` que contiene las propiedades de conexión.

1. Obtenga un formulario de PDF que contenga datos con códigos de barras

   * Crear un `java.io.FileInputStream` que representa el formulario de PDF que contiene datos con códigos de barras utilizando su constructor y pasando un valor de cadena que especifica la ubicación del documento de PDF.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Descodificar los datos del formulario de PDF

   Descodificar los datos del formulario invocando el `BarcodedFormsServiceClient` del objeto `decode` y pasando los siguientes valores:

   * El `com.adobe.idp.Document` que contiene el formulario de PDF.
   * A `java.lang.Boolean` que especifica si se debe descodificar un código de barras PDF 417.
   * A `java.lang.Boolean` que especifica si se debe descodificar un código de barras de matriz de datos.
   * A `java.lang.Boolean` que especifica si se descodifica un código de barras de código QR.
   * A `java.lang.Boolean` que especifica si se descodifica un código de barras de codabar.
   * A `java.lang.Boolean` que especifica si se debe descodificar un código de barras 128.
   * A `java.lang.Boolean` que especifica si se debe descodificar un código de barras 39.
   * A `java.lang.Boolean` que especifica si se debe descodificar un código de barras EAN-13.
   * A `java.lang.Boolean` que especifica si se debe descodificar un código de barras EAN-8.
   * A `com.adobe.livecycle.barcodedforms.CharSet` valor de enumeración que especifica el valor de codificación del conjunto de caracteres utilizado en el código de barras.

   El `decode` El método devuelve un `org.w3c.dom.Document` que contiene datos de formulario descodificados.

1. Convertir los datos en una fuente de datos XML

   Convertir los datos descodificados en datos XDP o XFDF invocando el `BarcodedFormsServiceClient` del objeto `extractToXML` y pasando los siguientes valores:

   * El `org.w3c.dom.Document` que contiene datos descodificados (asegúrese de utilizar la variable `decode` valor devuelto del método).
   * A `com.adobe.livecycle.barcodedforms.Delimiter` valor de enumeración que especifica el delimitador de línea. Se recomienda especificar lo siguiente `Delimiter.Carriage_Return`.
   * A `com.adobe.livecycle.barcodedforms.Delimiter` valor de enumeración que especifica el delimitador de campo. Por ejemplo, especifique `Delimiter.Tab`.
   * A `com.adobe.livecycle.barcodedforms.XMLFormat` valor de enumeración que especifica si se convierten los datos de código de barras en datos XML XDP o XFDF. Por ejemplo, especifique `XMLFormat.XDP` para convertir los datos en datos XDP.

   >[!NOTE]
   >
   >No especifique los mismos valores para los parámetros de delimitador de línea y delimitador de campo.

   El `extractToXML` El método devuelve un valor `java.util.List` objeto donde cada elemento es un `org.w3c.dom.Document` objeto. Hay un elemento independiente para cada código de barras ubicado en el formulario. Es decir, si hay cuatro códigos de barras en el formulario, entonces hay cuatro elementos en el devuelto `java.util.List` objeto.

1. Procesamiento de los datos descodificados

   * Itere a través de `java.util.List` objeto para obtener cada `org.w3c.dom.Document` que se encuentra en la lista.
   * Para cada elemento de la lista, convierta el `org.w3c.dom.Document` objeto a `com.adobe.idp.Document` objeto. (La lógica de la aplicación que convierte un `org.w3c.dom.Document` objeto en un `com.adobe.idp.Document` se muestra en los datos del formulario con códigos de barras de Descodificación (con el ejemplo de la API de Java).
   * Guarde los datos XML como un archivo XML invocando el `com.adobe.idp.Document` del objeto `copyToFile`y pasando un objeto File que representa el archivo XML.

**Consulte también**

[Inicio rápido (modo SOAP): Descodificación de datos de formulario con códigos de barras mediante la API de Java](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Descodificar datos de formulario con códigos de barras mediante la API de servicio web {#decode-barcoded-form-data-using-the-web-service-api}

Descodificar datos de formulario mediante la API de formularios con códigos de barras (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL del servicio de formularios con códigos de barras. Para obtener más información, consulte [Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).
   * Hacer referencia al ensamblado de cliente de Microsoft .NET. Para obtener más información, vea &quot;Hacer referencia al ensamblado de cliente .NET&quot; en [Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).

1. Crear un objeto de API de cliente de formularios con códigos de barras

   Mediante el ensamblado de cliente de Microsoft .NET que consume el WSDL del servicio de formularios con códigos de barras, cree un `BarcodedFormsServiceService` invocando su constructor predeterminado.

1. Obtenga un formulario de PDF que contenga datos con códigos de barras

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar un documento de PDF que contiene un código de barras.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento de PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` al asignar su `binaryData` con el contenido de la matriz de bytes.

1. Descodificar los datos del formulario de PDF

   Descodificar los datos del formulario invocando el `BarcodedFormsServiceService` del objeto `decode` y pasando los siguientes valores:

   * El `BLOB` que contiene el formulario de PDF.
   * A `Boolean` que especifica si se debe descodificar un código de barras PDF 417.
   * A `Boolean` que especifica si se debe descodificar un código de barras de matriz de datos.
   * A `Boolean` que especifica si se descodifica un código de barras de código QR.
   * A `Boolean` que especifica si se descodifica un código de barras de codabar.
   * A `Boolean` que especifica si se debe descodificar un código de barras 128.
   * A `Bolean` que especifica si se debe descodificar un código de barras 39.
   * A `Boolean` que especifica si se debe descodificar un código de barras EAN-13.
   * A `Boolean` que especifica si se debe descodificar un código de barras EAN-8.
   * A `CharSet` valor de enumeración que especifica el valor de codificación del conjunto de caracteres utilizado en el código de barras.

   El `decode` devuelve un valor de cadena que contiene datos de formulario descodificados.

1. Convertir los datos en una fuente de datos XML

   Convertir los datos descodificados en datos XDP o XFDF invocando el `BarcodedFormsServiceService` del objeto `extractToXML` y pasando los siguientes valores:

   * Un valor de cadena que contiene datos descodificados (asegúrese de utilizar la variable `decode` valor devuelto del método).
   * A `Delimiter` valor de enumeración que especifica el delimitador de línea. Se recomienda especificar lo siguiente `Delimiter.Carriage_Return`.
   * A `Delimiter` valor de enumeración que especifica el delimitador de campo. Por ejemplo, especifique `Delimiter.Tab`.
   * A `XMLFormat` valor de enumeración que especifica si se convierten los datos de código de barras en datos XML XDP o XFDF. Por ejemplo, especifique `XMLFormat.XDP` para convertir los datos en datos XDP.

   >[!NOTE]
   >
   >No especifique los mismos valores para los parámetros de delimitador de línea y delimitador de campo.

   El `extractToXML` El método devuelve un `Object` matriz donde cada elemento es un `BLOB` ejemplo. Hay un elemento independiente para cada código de barras ubicado en el formulario. Es decir, si hay cuatro códigos de barras en el formulario, entonces hay cuatro elementos en el devuelto `Object` matriz.

1. Procesamiento de los datos descodificados

   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación de archivo del documento de PDF protegido.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto que ha devuelto el `encryptPDFUsingPassword` método. Rellene la matriz de bytes obteniendo el valor de `BLOB` del objeto `binaryData` miembro de datos.
   * Crear un `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
