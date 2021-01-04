---
title: Uso de formularios con código de barras
seo-title: Uso de formularios con código de barras
description: Descodificar datos de un formulario PDF o una imagen que contenga un código de barras mediante la API de Java y la API de servicio Web.
seo-description: Descodificar datos de un formulario PDF o una imagen que contenga un código de barras mediante la API de Java y la API de servicio Web.
uuid: e56c3c94-384d-401f-b418-dd34cdc57eda
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: eb28ac30-265c-4611-8247-1f4bc826f254
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1931'
ht-degree: 0%

---


# Uso de formularios con códigos de barras {#working-with-barcoded-forms}

## Acerca del servicio de formularios con códigos de barras {#about-the-barcoded-forms-service}

El servicio de formularios con códigos de barras automatiza la captura de datos de formularios de relleno e impresión e integra la información capturada en los sistemas informáticos principales de una organización.

Con el servicio de formularios con códigos de barras, puede agregar códigos de barras unidimensionales y bidimensionales a PDF forms interactivos. A continuación, puede publicar los formularios con códigos de barras en un sitio web o distribuirlos por correo electrónico o CD. Cuando un usuario rellena un formulario con códigos de barras mediante Adobe Reader, Acrobat Professional o Acrobat Standard, el código de barras se actualiza automáticamente para codificar los datos del formulario proporcionados por el usuario. El usuario puede enviar el formulario electrónicamente o imprimirlo en papel y enviarlo por correo electrónico, fax o mano. Posteriormente, puede extraer los datos suministrados por el usuario como parte de un flujo de trabajo automatizado, lo que permite el enrutamiento de los datos entre los procesos de aprobación y los sistemas empresariales.

Para obtener más información sobre el servicio de formularios con códigos de barras, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Descodificación de datos de formulario codificados con barras {#decoding-barcoded-form-data}

Puede utilizar la API de servicio de formularios con códigos de barras para descodificar datos de un formulario PDF o una imagen que contenga un código de barras. Descodificar datos de formulario significa extraer datos que se encuentran en el código de barras. Para que los datos se puedan descodificar desde un formulario PDF (o imagen), el usuario debe rellenar el formulario con datos.

>[!NOTE]
>
>Para obtener más información sobre el servicio de formularios con códigos de barras, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para descodificar datos de un formulario PDF, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API formClient con códigos de barras.
1. Obtenga un formulario PDF que contenga datos codificados por barras.
1. Descodificar los datos del formulario PDF.
1. Convierta los datos a un origen de datos XML.
1. Procese los datos descodificados.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)
* xercesImpl.jar (ubicado en &lt;directorio de instalación>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty)

Si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no es JBOSS, deberá reemplazar adobe-utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms. Para obtener información sobre la ubicación de todos los archivos JAR de AEM Forms, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creación de un objeto API de cliente de formularios con código de barras**

Para poder realizar mediante programación una operación de servicio de formularios con códigos de barras, debe crear un cliente de servicio de Forms con códigos de barras. Si utiliza la API de Java, cree un objeto `BarcodedFormsServiceClient`. Si utiliza la API de servicio Web de formularios con códigos de barras, cree un objeto `BarcodedFormsServiceService`.

**Obtener un formulario PDF que contiene datos codificados con barras**

Debe obtener un formulario PDF que contenga un código de barras que se haya rellenado con datos de usuario.

**Descodificar los datos del formulario PDF**

Después de obtener un formulario PDF (o una imagen) que contenga un código de barras, puede descodificar los datos. El servicio Forms con códigos de barras admite los siguientes tipos de códigos de barras:

* Códigos de barras PDF417.
* Códigos de barras de la matriz de datos.
* Códigos de barras QR.
* Códigos de barras de Codabar.
* Códigos de barras Código 128.
* Códigos de barras Código 39.
* Códigos de barras EAN-13.
* Códigos de barras EAN-8.

La entrada de conjuntos de caracteres como hexadecimal en la API de descodificación implica que el contenido del código de barras se codifica como una cadena hexadecimal. Por ejemplo, si se especifica UTF-8 como codificación de caracteres en el formulario y se especifica Hex en la operación de descodificación, el contenido del código de barras se codifica como una cadena Hex en el elemento &lt; `xb:content`> del resultado descodificado. Puede convertir este valor hexadecimal para obtener el contenido original creando la lógica de la aplicación en la aplicación cliente.

**Convertir los datos en un origen de datos XML**

Después de decodificar los datos del formulario, puede convertirlos en datos XDP o XFDF. Por ejemplo, supongamos que desea importar los datos en otro formulario. Para importar los datos en un formulario XFA, debe convertir los datos en datos XDP. Para obtener más información, consulte [Importación de datos de formulario](/help/forms/developing/importing-exporting-data.md#importing-form-data).

**Procesar los datos descodificados**

Puede procesar los datos convertidos para satisfacer los requisitos comerciales. Por ejemplo, después de descodificar y convertir los datos, puede guardarlos en un archivo, almacenarlos en una base de datos empresarial, rellenar otro formulario, etc. En esta sección se explica cómo guardar los datos convertidos como un archivo XML.

>[!NOTE]
>
>El servicio de formularios con códigos de barras no puede descodificar los datos del código de barras cuando los parámetros delimitador de línea y delimitador de campo tienen el mismo valor

**Consulte también**

[Descodificar datos de formulario con código de barras mediante la API de Java](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[Descodificar datos de formulario con código de barras mediante la API de servicio Web](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Descodificar datos de formulario con códigos de barras mediante la API de Java {#decode-barcoded-form-data-using-the-java-api}

Descodificar datos de formulario mediante la API de formularios codificados (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente en la ruta de clases del proyecto Java.

1. Creación de un objeto API de cliente de formularios con código de barras

   Cree un objeto `BarcodedFormsServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Obtener un formulario PDF que contiene datos codificados con barras

   * Cree un objeto `java.io.FileInputStream` que represente el formulario PDF que contiene datos codificados con barras mediante su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Descodificar los datos del formulario PDF

   Para descodificar los datos del formulario, invoque el método `BarcodedFormsServiceClient` del objeto `decode` y pase los valores siguientes:

   * El objeto `com.adobe.idp.Document` que contiene el formulario PDF.
   * Un objeto `java.lang.Boolean` que especifica si se descodifica un código de barras PDF417.
   * Un objeto `java.lang.Boolean` que especifica si se descodifica un código de barras de matriz de datos.
   * Un objeto `java.lang.Boolean` que especifica si se descodifica un código de barras de código QR.
   * Un objeto `java.lang.Boolean` que especifica si se descodifica un código de barras de códigos.
   * Un objeto `java.lang.Boolean` que especifica si se descodifica un código de barras 128.
   * Un objeto `java.lang.Boolean` que especifica si se descodifica un código de barras de código 39.
   * Un objeto `java.lang.Boolean` que especifica si se descodifica un código de barras EAN-13.
   * Un objeto `java.lang.Boolean` que especifica si se descodifica un código de barras EAN-8.
   * Un valor de lista desglosada `com.adobe.livecycle.barcodedforms.CharSet` que especifica el valor de codificación del conjunto de caracteres utilizado en el código de barras.

   El método `decode` devuelve un objeto `org.w3c.dom.Document` que contiene datos de formulario descodificados.

1. Convertir los datos en un origen de datos XML

   Convierta los datos descodificados en datos XDP o XFDF invocando el método `BarcodedFormsServiceClient` del objeto `extractToXML` y pasando los siguientes valores:

   * El objeto `org.w3c.dom.Document` que contiene datos descodificados (asegúrese de utilizar el valor devuelto del método `decode`).
   * Un valor de lista desglosada `com.adobe.livecycle.barcodedforms.Delimiter` que especifica el delimitador de línea. Se recomienda especificar `Delimiter.Carriage_Return`.
   * Un valor de lista desglosada `com.adobe.livecycle.barcodedforms.Delimiter` que especifica el delimitador de campo. Por ejemplo, especifique `Delimiter.Tab`.
   * Un valor de lista desglosada `com.adobe.livecycle.barcodedforms.XMLFormat` que especifica si se deben convertir los datos del código de barras en datos XDP o XFDF XML. Por ejemplo, especifique `XMLFormat.XDP` para convertir los datos en datos XDP.

   >[!NOTE]
   >
   >No especifique los mismos valores para los parámetros delimitador de línea y delimitador de campo.

   El método `extractToXML` devuelve un objeto `java.util.List` donde cada elemento es un objeto `org.w3c.dom.Document`. Hay un elemento independiente para cada código de barras ubicado en el formulario. Es decir, si hay cuatro códigos de barras en el formulario, entonces hay cuatro elementos en el objeto `java.util.List` devuelto.

1. Procesar los datos descodificados

   * Repita el objeto `java.util.List` para obtener cada objeto `org.w3c.dom.Document` ubicado en la lista.
   * Para cada elemento de la lista, convierta el objeto `org.w3c.dom.Document` en un objeto `com.adobe.idp.Document`. (La lógica de la aplicación que convierte un objeto `org.w3c.dom.Document` en un objeto `com.adobe.idp.Document` se muestra en los datos de formulario codificados con barras de descodificación mediante el ejemplo de la API de Java).
   * Guarde los datos XML como archivo XML invocando el `com.adobe.idp.Document` objeto `copyToFile` y pasando un objeto File que representa el archivo XML.

**Consulte también**

[Inicio rápido (modo SOAP): Descodificación de datos de formulario con código de barras mediante la API de Java](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Descodificar datos de formulario codificados con barras mediante la API de servicio Web {#decode-barcoded-form-data-using-the-web-service-api}

Descodificar datos de formulario mediante la API de formularios codificados (servicio Web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que utilice el WSDL del servicio de formularios con códigos de barras. Para obtener más información, consulte [Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).
   * Haga referencia al ensamblado de cliente de Microsoft .NET. Para obtener más información, consulte &quot;Referencia al ensamblado de cliente .NET&quot; en [Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).

1. Creación de un objeto API de cliente de formularios con código de barras

   Mediante el ensamblado de cliente de Microsoft .NET que utiliza el WSDL del servicio de formularios con códigos de barras, cree un objeto `BarcodedFormsServiceService` invocando su constructor predeterminado.

1. Obtener un formulario PDF que contiene datos codificados con barras

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar un documento PDF que contiene un código de barras.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando su propiedad `binaryData` con el contenido de la matriz de bytes.

1. Descodificar los datos del formulario PDF

   Para descodificar los datos del formulario, invoque el método `BarcodedFormsServiceService` del objeto `decode` y pase los valores siguientes:

   * El objeto `BLOB` que contiene el formulario PDF.
   * Un objeto `Boolean` que especifica si se descodifica un código de barras PDF417.
   * Un objeto `Boolean` que especifica si se descodifica un código de barras de matriz de datos.
   * Un objeto `Boolean` que especifica si se descodifica un código de barras de código QR.
   * Un objeto `Boolean` que especifica si se descodifica un código de barras de códigos.
   * Un objeto `Boolean` que especifica si se descodifica un código de barras 128.
   * Un objeto `Bolean` que especifica si se descodifica un código de barras de código 39.
   * Un objeto `Boolean` que especifica si se descodifica un código de barras EAN-13.
   * Un objeto `Boolean` que especifica si se descodifica un código de barras EAN-8.
   * Un valor de lista desglosada `CharSet` que especifica el valor de codificación del conjunto de caracteres utilizado en el código de barras.

   El método `decode` devuelve un valor de cadena que contiene datos de formulario descodificados.

1. Convertir los datos en un origen de datos XML

   Convierta los datos descodificados en datos XDP o XFDF invocando el método `BarcodedFormsServiceService` del objeto `extractToXML` y pasando los siguientes valores:

   * Un valor de cadena que contiene datos descodificados (asegúrese de utilizar el valor devuelto por el método `decode`).
   * Un valor de lista desglosada `Delimiter` que especifica el delimitador de línea. Se recomienda especificar `Delimiter.Carriage_Return`.
   * Un valor de lista desglosada `Delimiter` que especifica el delimitador de campo. Por ejemplo, especifique `Delimiter.Tab`.
   * Un valor de lista desglosada `XMLFormat` que especifica si se deben convertir los datos del código de barras en datos XDP o XFDF XML. Por ejemplo, especifique `XMLFormat.XDP` para convertir los datos en datos XDP.

   >[!NOTE]
   >
   >No especifique los mismos valores para los parámetros delimitador de línea y delimitador de campo.

   El método `extractToXML` devuelve una matriz `Object` donde cada elemento es una instancia `BLOB`. Hay un elemento independiente para cada código de barras ubicado en el formulario. Es decir, si hay cuatro códigos de barras en el formulario, entonces hay cuatro elementos en la matriz `Object` devuelta.

1. Procesar los datos descodificados

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF protegido.
   * Cree una matriz de bytes que almacene el contenido de datos del objeto `BLOB` devuelto por el método `encryptPDFUsingPassword`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `binaryData`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
