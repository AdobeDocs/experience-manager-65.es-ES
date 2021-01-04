---
title: Firma digital y certificación de Documentos
seo-title: Firma digital y certificación de Documentos
description: Utilice el servicio Signature para agregar y eliminar campos de firma digital a un documento PDF, recuperar los nombres de los campos de firma ubicados en un documento PDF, modificar los campos de firma, firmar digitalmente documentos PDF, certificar documentos PDF, validar firmas digitales ubicadas en un documento PDF, validar todas las firmas digitales ubicadas en un documento PDF y quitar una firma digital de un campo de firma.
seo-description: Utilice el servicio Signature para agregar y eliminar campos de firma digital a un documento PDF, recuperar los nombres de los campos de firma ubicados en un documento PDF, modificar los campos de firma, firmar digitalmente documentos PDF, certificar documentos PDF, validar firmas digitales ubicadas en un documento PDF, validar todas las firmas digitales ubicadas en un documento PDF y quitar una firma digital de un campo de firma.
uuid: 6331de8a-2a9c-45bf-89d2-29f1ad5cc856
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 42de04bf-25e4-4478-a411-38671ed871ae
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '17099'
ht-degree: 0%

---


# Firma digital y certificación de Documentos {#digitally-signing-and-certifying-documents}

**Acerca del servicio de firma**

El servicio Signature permite a su organización proteger la seguridad y la privacidad de los documentos de Adobe PDF que distribuye y recibe. Este servicio utiliza las firmas digitales y la certificación para garantizar que solo los destinatarios deseados pueden alterar los documentos. Como las características de seguridad se aplican al documento mismo, el documento permanece seguro y controlado durante todo su ciclo de vida. Un documento permanece seguro más allá del servidor de seguridad, cuando se descarga sin conexión y cuando se envía de nuevo a la organización.

>[!NOTE]
>
>Puede crear un controlador de firma personalizado para el servicio Signature que se invoca cuando se invocan determinadas operaciones, como la firma de un documento PDF.

**Nombres de campos de firma**

Algunas operaciones del servicio de firma requieren que especifique el nombre del campo de firma en el que se realiza una operación. Por ejemplo, al firmar un documento PDF, se especifica el nombre del campo de firma que se va a firmar. Supongamos que el nombre completo de un campo de firma es `form1[0].Form1[0].SignatureField1[0]`. Puede especificar `SignatureField1[0]` en lugar de `form1[0].Form1[0].SignatureField1[0]`.

A veces, un conflicto hace que el servicio Signature firme firme (o realice otra operación que requiera el nombre del campo de firma) el campo incorrecto. Este conflicto es el resultado de que el nombre `SignatureField1[0]` aparece en dos o más lugares del mismo documento PDF. Por ejemplo, considere un documento PDF que contenga dos campos de firma denominados `form1[0].Form1[0].SignatureField1[0]` y `form1[0].Form1[0].SubForm1[0].SignatureField1[0]` y especifique `SignatureField1[0]`. En este caso, el servicio de firma firma firma firma el primer campo de firma que encuentra mientras se iteran todos los campos de firma del documento.

Si hay varios campos de firma dentro de un documento PDF, se recomienda especificar los nombres completos de los campos de firma. Es decir, especifique `form1[0].Form1[0].SignatureField1[0]`en lugar de `SignatureField1[0]`.

Puede realizar estas tareas mediante el servicio Signature:

* Añada y elimine los campos de firma digital en un documento PDF. (Consulte [Añadir campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields)).
* Recupere los nombres de los campos de firma ubicados en un documento PDF. (Consulte [Recuperación de nombres de campos de firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names).)
* Modifique los campos de firma. (Consulte [Modificación de campos de firma](digitally-signing-certifying-documents.md#modifying-signature-fields).)
* Firmar digitalmente documentos PDF. (Consulte [Firma digital de Documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)).
* Certificar documentos PDF. (Consulte [Certificación de Documentos PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)).
* Valide las firmas digitales ubicadas en un documento PDF. (Consulte [Verificación de firmas digitales](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* Valide todas las firmas digitales ubicadas en un documento PDF. (Consulte [Verificación de varias firmas digitales](digitally-signing-certifying-documents.md#verifying-digital-signatures)).
* Quitar una firma digital de un campo de firma. (Consulte [Eliminación de firmas digitales](digitally-signing-certifying-documents.md#removing-digital-signatures).)

>[!NOTE]
>
>Para obtener más información sobre el servicio Signature, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Añadir campos de firma {#adding-signature-fields}

Las firmas digitales aparecen en los campos de firma, que son campos de formulario que contienen una representación gráfica de la firma. Los campos de firma pueden ser visibles o invisibles. Los firmantes pueden utilizar un campo de firma preexistente o se puede agregar un campo de firma mediante programación. En cualquier caso, el campo de firma debe existir para poder firmar un documento PDF.

Puede agregar un campo de firma mediante programación mediante la API de Java del servicio de firma o la API del servicio web de firma. Puede agregar más de un campo de firma a un documento PDF; sin embargo, cada nombre de campo de firma debe ser único.

>[!NOTE]
>
>Algunos tipos de documentos PDF no permiten agregar un campo de firma mediante programación. Para obtener más información sobre el servicio de firmas y la adición de campos de firma, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para agregar un campo de firma a un documento PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de firma.
1. Obtenga un documento PDF al que se agrega un campo de firma.
1. Añada un campo de firma.
1. Guarde el documento PDF como archivo PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (requerido si AEM Forms se implementa en JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss)

**Crear un cliente de firma**

Para poder realizar una operación de servicio de firma mediante programación, debe crear un cliente de servicio de firma.

**Obtener un documento PDF al que se ha agregado un campo de firma**

Debe obtener un documento PDF al que se agregue un campo de firma.

**Añadir un campo de firma**

Para agregar correctamente un campo de firma a un documento PDF, especifique los valores de las coordenadas que identifican la ubicación del campo de firma. (Si agrega un campo de firma invisible, estos valores no son obligatorios). Además, puede especificar qué campos del documento PDF se bloquean después de aplicar una firma al campo de firma.

**Guardar el documento PDF como archivo PDF**

Una vez que el servicio Signature haya agregado un campo de firma al documento PDF, puede guardar el documento como archivo PDF para que los usuarios puedan abrirlo en Acrobat o Adobe Reader.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Firma digital de Documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Añadir campos de firma mediante la API de Java {#add-signature-fields-using-the-java-api}

Añada un campo de firma mediante la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente de firma

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `SignatureServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtener un documento PDF al que se ha agregado un campo de firma

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF al que se agrega un campo de firma utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Añadir un campo de firma

   * Cree un objeto `PositionRectangle` que especifique la ubicación del campo de firma mediante su constructor. En el constructor, especifique los valores de las coordenadas.
   * Si lo desea, cree un objeto `FieldMDPOptions` que especifique los campos que se bloquean cuando se aplica una firma digital al campo de firma.
   * Añada un campo de firma en un documento PDF invocando el método `SignatureServiceClient` del objeto `addSignatureField` y pasando los valores siguientes:

      * A `com.adobe.idp`. `Document` objeto que representa el documento PDF al que se agrega un campo de firma.
      * Un valor de cadena que especifica el nombre del campo de firma.
      * Un valor `java.lang.Integer` que representa el número de página al que se agrega un campo de firma.
      * Un objeto `PositionRectangle` que especifica la ubicación del campo de firma.
      * Un objeto `FieldMDPOptions` que especifica los campos del documento PDF que se bloquean después de aplicar una firma digital al campo de firma. Este valor de parámetro es opcional y puede pasar `null`.
   * Un objeto `PDFSeedValueOptions` que especifica varios valores de tiempo de ejecución. Este valor de parámetro es opcional y puede pasar `null`.

      El método `addSignatureField` devuelve un `com.adobe.idp`. `Document` objeto que representa un documento PDF que contiene un campo de firma.
   >[!NOTE]
   >
   >Puede invocar el método `SignatureServiceClient` del objeto `addInvisibleSignatureField` para agregar un campo de firma invisible.

1. Guardar el documento PDF como archivo PDF

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea .pdf.
   * Invoque el `com.adobe.idp`. `Document` el  `copyToFile` método del objeto para copiar el contenido del  `Document` objeto en el archivo. Asegúrese de utilizar el `com.adobe.idp`. `Document` objeto devuelto por el  `addSignatureField` método.

**Consulte también**

[Inicios rápidos de la API de servicio de firma](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### Añadir campos de firma mediante la API de servicio Web {#add-signature-fields-using-the-web-service-api}

Para agregar un campo de firma mediante la API de firma (servicio Web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Crear un cliente de firma

   * Cree un objeto `SignatureServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `SignatureServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `SignatureServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtener un documento PDF al que se ha agregado un campo de firma

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el documento PDF que contendrá un campo de firma.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Añadir un campo de firma

   Añada un campo de firma en el documento PDF invocando el método `SignatureServiceClient` del objeto `addSignatureField` y pasando los valores siguientes:

   * Un objeto `BLOB` que representa el documento PDF al que se agrega un campo de firma.
   * Un valor de cadena que especifica el nombre del campo de firma.
   * Un valor entero que representa el número de página al que se agrega un campo de firma.
   * Un objeto `PositionRect` que especifica la ubicación del campo de firma.
   * Un objeto `FieldMDPOptions` que especifica los campos del documento PDF que se bloquean después de aplicar una firma digital al campo de firma. Este valor de parámetro es opcional y puede pasar `null`.
   * Un objeto `PDFSeedValueOptions` que especifica varios valores de tiempo de ejecución. Este valor de parámetro es opcional y puede pasar `null`.

   El método `addSignatureField` devuelve un objeto `BLOB` que representa un documento PDF que contiene un campo de firma.

1. Guardar el documento PDF como archivo PDF

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF que contendrá el campo de firma y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` devuelto por el método `addSignatureField`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `binaryData`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Recuperación de nombres de campos de firma {#retrieving-signature-field-names}

Puede recuperar los nombres de todos los campos de firma ubicados en un documento PDF que desee firmar o certificar. Si no está seguro de los nombres de los campos de firma que se encuentran en un documento PDF o desea comprobar los nombres, puede recuperarlos mediante programación. El servicio Signature devuelve el nombre completo del campo de firma, como `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

>[!NOTE]
>
>Para obtener más información sobre el servicio Signature, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Resumen de los pasos {#summary_of_steps-1}

Para recuperar los nombres de los campos de firma, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de firma.
1. Obtenga el documento PDF que contiene campos de firma.
1. Recupere los nombres de los campos de firma.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (requerido si AEM Forms se implementa en JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de firma**

Para poder realizar una operación de servicio de firma mediante programación, debe crear un cliente de servicio de firma.

**Obtener el documento PDF que contiene campos de firma**

Recupere un documento PDF que contenga campos de firma.

**Recuperar nombres de campo de firma**

Puede recuperar los nombres de los campos de firma después de recuperar un documento PDF que contenga uno o varios campos de firma.

**Consulte también**

[Recuperar nombres de campo de firma mediante la API de Java](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[Recuperar campo de firma mediante la API de servicio Web](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Añadir campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields)

### Recuperar nombres de campo de firma mediante la API de Java {#retrieve-signature-field-names-using-the-java-api}

Recuperar nombres de campo de firma mediante la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente de firma

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `SignatureServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtener el documento PDF que contiene campos de firma

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF que contiene campos de firma utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Recuperar nombres de campo de firma

   * Recupere los nombres de los campos de firma invocando el método `SignatureServiceClient` del objeto `getSignatureFieldList` y pasando el objeto `com.adobe.idp.Document` que contiene el documento PDF que contiene los campos de firma. Este método devuelve un objeto `java.util.List`, en el que cada elemento contiene un objeto `PDFSignatureField`. Con este objeto, puede obtener información adicional sobre un campo de firma, como si está visible.
   * Repita el objeto `java.util.List` para determinar si hay nombres de campo de firma. Para cada campo de firma del documento PDF, puede obtener un objeto `PDFSignatureField` independiente. Para obtener el nombre del campo de firma, invoque el método `PDFSignatureField` del objeto `getName`. Este método devuelve un valor de cadena que especifica el nombre del campo de firma.

**Consulte también**

[Recuperación de nombres de campos de firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Inicio rápido (modo SOAP): Recuperación de nombres de campo de firma mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar el campo de firma mediante la API de servicio Web {#retrieve-signature-field-using-the-web-service-api}

Recuperar nombres de campo de firma mediante la API de firma (servicio Web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Crear un cliente de firma

   * Cree un objeto `SignatureServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `SignatureServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `SignatureServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtener el documento PDF que contiene campos de firma

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el documento PDF que contiene campos de firma.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` el contenido de la matriz de bytes.

1. Recuperar nombres de campo de firma

   * Recupere los nombres de los campos de firma invocando el método `SignatureServiceClient` del objeto `getSignatureFieldList` y pasando el objeto `BLOB` que contiene el documento PDF que contiene los campos de firma. Este método devuelve un objeto de colección `MyArrayOfPDFSignatureField` donde cada elemento contiene un objeto `PDFSignatureField`.
   * Repita el objeto `MyArrayOfPDFSignatureField` para determinar si hay nombres de campo de firma. Para cada campo de firma del documento PDF, puede obtener un objeto `PDFSignatureField`. Para obtener el nombre del campo de firma, invoque el método `PDFSignatureField` del objeto `getName`. Este método devuelve un valor de cadena que especifica el nombre del campo de firma.

**Consulte también**

[Recuperación de nombres de campos de firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modificación de campos de firma {#modifying-signature-fields}

Puede modificar los campos de firma que se encuentran en un documento PDF mediante la API de Java y la API de servicio Web. La modificación de un campo de firma implica la manipulación de los valores del diccionario de bloqueo de campos de firma o de los valores del diccionario de valores de raíz.

Un *diccionario de bloqueo de campo* especifica una lista de campos que se bloquean cuando se firma el campo de firma. Un campo bloqueado impide que los usuarios realicen cambios en el campo. Un *diccionario de valores de raíz* contiene información de restricción que se utiliza en el momento en que se aplica la firma. Por ejemplo, puede cambiar los permisos que controlan las acciones que pueden producirse sin invalidar una firma.

Al modificar un campo de firma existente, puede realizar cambios en el documento PDF para reflejar los cambios en los requisitos comerciales. Por ejemplo, un nuevo requisito comercial puede requerir bloquear todos los campos de documento después de firmar el documento.

En esta sección se explica cómo modificar un campo de firma modificando los valores del diccionario de bloqueo de campos y del diccionario de valores de inicialización. Los cambios realizados en el diccionario de bloqueo de campos de firma hacen que todos los campos del documento PDF se bloqueen cuando se firma un campo de firma. Los cambios realizados en el diccionario de valores de inicialización prohíben tipos específicos de cambios en el documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio de firmas y la modificación de los campos de firma, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-2}

Para modificar los campos de firma ubicados en un documento PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de firma.
1. Obtenga el documento PDF que contiene el campo de firma que desea modificar.
1. Defina los valores del diccionario.
1. Modifique el campo de firma.
1. Guarde el documento PDF como archivo PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (requerido si AEM Forms se implementa en JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de LiveCycle](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de firma**

Para poder realizar una operación de servicio de firma mediante programación, debe crear un cliente de servicio de firma.

**Obtenga el documento PDF que contiene el campo de firma para modificar**

Recupere un documento PDF que contenga el campo de firma que desea modificar.

**Definir valores de diccionario**

Para modificar un campo de firma, asigne valores a su diccionario de bloqueo de campo o diccionario de valores de raíz. Especificar los valores del diccionario de bloqueo de campos de firma implica especificar los campos de documento PDF que se bloquean cuando se firma el campo de firma. (En esta sección se explica cómo bloquear todos los campos).

Se pueden definir los siguientes valores del diccionario de valores de inicialización:

* **Comprobación** de revisión: Especifica si se realiza la comprobación de revocación cuando se aplica una firma al campo de firma.
* **Opciones** de certificado: Asigna valores al diccionario de valores de raíz del certificado. Antes de especificar las opciones de certificado, se recomienda familiarizarse con un diccionario de valores de raíz de certificado. (Consulte [Referencia de PDF](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)).
* **Opciones** de resumen: Asigna algoritmos de compendio que se utilizan para firmar. Los valores válidos son SHA1, SHA256, SHA384, SHA512 y RIPEMD160.
* **Filtro**: Especifica el filtro que se utiliza con el campo de firma. Por ejemplo, puede utilizar el filtro Adobe.PPKLite. (Consulte [Referencia de PDF](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)).
* **Opciones** de indicador: Especifica los valores del indicador asociados a este campo de firma. Un valor de 1 significa que un firmante debe utilizar solo los valores especificados para la entrada. Un valor de 0 significa que se permiten otros valores. Estas son las posiciones de Bit:

   * **1(Filtro):** El controlador de firma que se utilizará para firmar el campo de firma
   * **2 (SubFilter):** Matriz de nombres que indican codificaciones aceptables para usar al firmar
   * **3 V)**: El número mínimo de versión requerido del controlador de firma que se va a utilizar para firmar el campo de firma
   * **4 (Razones):** matriz de cadenas que especifican posibles motivos para firmar un documento
   * **5 (PDFLegalWarnings):** una matriz de cadenas que especifican posibles autenticaciones legales

* **Afirmaciones** legales: Cuando un documento está certificado, se escanea automáticamente para buscar tipos específicos de contenido que puedan hacer que el contenido visible de un documento sea ambiguo o engañoso. Por ejemplo, una anotación puede oscurecer el texto que es importante para comprender lo que se está certificando. El proceso de análisis genera advertencias que indican la presencia de este tipo de contenido. También proporciona una explicación adicional del contenido que puede haber generado advertencias.
* **Permisos**: Especifica los permisos que se pueden usar en un documento PDF sin invalidar la firma.
* **Razones**: Especifica los motivos por los que se debe firmar este documento.
* **Marca** de hora: Especifica las opciones de marca de hora. Por ejemplo, puede establecer la dirección URL del servidor de marca de hora que se utiliza.
* **Versión**: Especifica el número de versión mínimo del controlador de firma que se va a utilizar para firmar el campo de firma.

**Modificación del campo de firma**

Después de crear un cliente de servicio de firma, recuperar el documento PDF que contiene el campo de firma para modificarlo y establecer los valores del diccionario, puede indicar al servicio de firma que modifique el campo de firma. A continuación, el servicio Signature devuelve un documento PDF que contiene el campo de firma modificado. El documento PDF original no se ve afectado.

**Guardar el documento PDF como archivo PDF**

Guarde el documento PDF que contiene el campo de firma modificado como archivo PDF para que los usuarios puedan abrirlo en Acrobat o Adobe Reader.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API de servicio de firma](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[Firma digital de Documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Modificación de campos de firma mediante la API de Java {#modify-signature-fields-using-the-java-api}

Modifique un campo de firma mediante la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente de firma

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `SignatureServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga el documento PDF que contiene el campo de firma para modificar

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF que contiene el campo de firma que se va a modificar mediante su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Definir valores de diccionario

   * Cree un objeto `PDFSignatureFieldProperties` utilizando su constructor. Un objeto `PDFSignatureFieldProperties` almacena información del diccionario de bloqueo de campos de firma y del diccionario de valores de raíz.
   * Cree un objeto `PDFSeedValueOptionSpec` utilizando su constructor. Este objeto permite definir valores de diccionario de valores de inicialización.
   * No permitir cambios en el documento PDF invocando el método `PDFSeedValueOptionSpec` del objeto `setMdpValue` y pasando el valor de lista desglosada `MDPPermissions.NoChanges`.
   * Cree un objeto `FieldMDPOptionSpec` utilizando su constructor. Este objeto permite definir valores del diccionario de bloqueo de campos de firma.
   * Bloquear todos los campos del documento PDF invocando el método `FieldMDPOptionSpec` del objeto `setMdpValue` y pasando el valor de lista desglosada `FieldMDPAction.ALL`.
   * Configure la información del diccionario de valores de raíz invocando el método `PDFSignatureFieldProperties` del objeto `setSeedValue` y pasando el objeto `PDFSeedValueOptionSpec`.
   * Para establecer la información del diccionario de bloqueo de campos de firma, invoque el método `PDFSignatureFieldProperties``setFieldMDP` del objeto y pase el objeto `FieldMDPOptionSpec`.

   >[!NOTE]
   >
   >Para ver todos los valores del diccionario de valores de raíz que puede establecer, consulte la referencia de clase `PDFSeedValueOptionSpec`. (Consulte [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)).

1. Modificación del campo de firma

   Modifique el campo de firma invocando el método `SignatureServiceClient` del objeto `modifySignatureField` y pasando los siguientes valores:

   * El objeto `com.adobe.idp.Document` que almacena el documento PDF que contiene el campo de firma que se va a modificar
   * Un valor de cadena que especifica el nombre del campo de firma
   * El objeto `PDFSignatureFieldProperties` que almacena información del diccionario de bloqueo de campos de firma y del diccionario de valores de raíz

   El método `modifySignatureField` devuelve un objeto `com.adobe.idp.Document` que almacena un documento PDF que contiene el campo de firma modificado.

1. Guardar el documento PDF como archivo PDF

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del nombre de archivo sea .pdf.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del objeto `com.adobe.idp.Document` en el archivo. Asegúrese de utilizar el objeto `com.adobe.idp.Document` que devolvió el método `modifySignatureField`.

### Modificación de campos de firma mediante la API de servicio Web {#modify-signature-fields-using-the-web-service-api}

Modifique un campo de firma mediante la API de firma (servicio Web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Crear un cliente de firma

   * Cree un objeto `SignatureServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `SignatureServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `SignatureServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento PDF que contiene el campo de firma para modificar

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el documento PDF que contiene el campo de firma que se va a modificar.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` el contenido de la matriz de bytes.

1. Definir valores de diccionario

   * Cree un objeto `PDFSignatureFieldProperties` utilizando su constructor. Este objeto almacena información del diccionario de bloqueo de campos de firma y del diccionario de valores de raíz.
   * Cree un objeto `PDFSeedValueOptionSpec` utilizando su constructor. Este objeto permite definir valores de diccionario de valores de inicialización.
   * No permitir cambios en el documento PDF asignando el valor de lista desglosada `MDPPermissions.NoChanges` al miembro de datos `PDFSeedValueOptionSpec` del objeto `mdpValue`.
   * Cree un objeto `FieldMDPOptionSpec` utilizando su constructor. Este objeto permite definir valores del diccionario de bloqueo de campos de firma.
   * Bloquear todos los campos del documento PDF asignando el valor de lista desglosada `FieldMDPAction.ALL` al miembro de datos `FieldMDPOptionSpec` del objeto `mdpValue`.
   * Configure la información del diccionario de valores de raíz asignando el objeto `PDFSeedValueOptionSpec` al miembro de datos `PDFSignatureFieldProperties` del objeto `seedValue`.
   * Para definir la información del diccionario de bloqueo de campos de firma, asigne el objeto `FieldMDPOptionSpec` al miembro de datos `PDFSignatureFieldProperties` del objeto `fieldMDP`.

   >[!NOTE]
   >
   >Para ver todos los valores del diccionario de valores de raíz que puede establecer, consulte la referencia de clase `PDFSeedValueOptionSpec`. (Consulte [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)).

1. Modificación del campo de firma

   Modifique el campo de firma invocando el método `SignatureServiceClient` del objeto `modifySignatureField` y pasando los siguientes valores:

   * El objeto `BLOB` que almacena el documento PDF que contiene el campo de firma que se va a modificar
   * Un valor de cadena que especifica el nombre del campo de firma
   * El objeto `PDFSignatureFieldProperties` que almacena información del diccionario de bloqueo de campos de firma y del diccionario de valores de raíz

   El método `modifySignatureField` devuelve un objeto `BLOB` que almacena un documento PDF que contiene el campo de firma modificado.

1. Guardar el documento PDF como archivo PDF

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF que contendrá el campo de firma y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` que devuelve el método `addSignatureField`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Firma digital de Documentos PDF {#digitally-signing-pdf-documents}

Las firmas digitales se pueden aplicar a documentos PDF para proporcionar un nivel de seguridad. Las firmas digitales, como las manuscritas, proporcionan un medio para que los firmantes se identifiquen y hagan declaraciones sobre un documento. La tecnología utilizada para firmar digitalmente documentos ayuda a garantizar que tanto el firmante como los destinatarios tengan una idea clara de lo que se firmó y tengan la certeza de que el documento no se alteró desde que se firmó.

Los documentos PDF se firman mediante tecnología de clave pública. Un firmante tiene dos claves: una clave pública y una clave privada. La clave privada se almacena en las credenciales de un usuario que deben estar disponibles en el momento de la firma. La clave pública se almacena en el certificado del usuario que debe estar disponible para que los destinatarios puedan validar la firma. La información sobre los certificados revocados se encuentra en las respuestas de listas de revocación de certificados (CRL) y del protocolo de estado de certificados en línea (OCSP) distribuidas por las entidades emisoras de certificados (CA). La hora de firma se puede obtener de un origen de confianza conocido como Autoridad de marca de hora.

>[!NOTE]
>
>Para poder firmar digitalmente un documento PDF, debe asegurarse de agregar el certificado a AEM Forms. Se agrega un certificado mediante la consola de administración o mediante programación mediante la API del administrador de confianza. (Consulte [Importación de credenciales mediante la API del administrador de confianza](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)).

Puede firmar digitalmente documentos PDF mediante programación. Al firmar digitalmente un documento PDF, debe hacer referencia a una credencial de seguridad que exista en AEM Forms. La credencial es la clave privada que se utiliza para firmar.

El servicio Signature realiza los siguientes pasos cuando se firma un documento PDF:

1. El servicio Signature recupera las credenciales del Truststore pasando el alias especificado en la solicitud.
1. Truststore busca la credencial especificada.
1. La credencial se devuelve al servicio Signature y se utiliza para firmar el documento. Las credenciales también se almacenan en la caché con el alias para solicitudes futuras.

Para obtener información sobre la administración de credenciales de seguridad, consulte la guía *Instalación e implementación de AEM Forms* para su servidor de aplicaciones.

>[!NOTE]
>
>Existen diferencias entre los documentos de firma y de certificación. (Consulte [Certificación de Documentos PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)).

>[!NOTE]
>
>No todos los documentos PDF admiten la firma. Para obtener más información sobre el servicio Signature y los documentos de firma digital, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>El servicio Signature no admite archivos XDP con datos PDF incrustados como entrada para una operación, como la certificación de un documento. Esta acción hace que el servicio Signature emita un `PDFOperationException`. Para resolver este problema, convierta el archivo XDP a un archivo PDF mediante el servicio Utilidades de PDF y, a continuación, pase el archivo PDF convertido a una operación de servicio de firma. (Consulte [Uso de utilidades de PDF](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities)).

**Credencial nShield HSM de cifrado**

Cuando se utiliza una credencial nShield HSM de Cipher para firmar o certificar un documento PDF, no se puede utilizar la nueva credencial hasta que se reinicie el servidor de aplicaciones J2EE en el que se implementa AEM Forms. Sin embargo, puede establecer un valor de configuración, lo que resulta en que la operación de firma o certificación funcione sin reiniciar el servidor de aplicaciones J2EE.

Puede agregar el siguiente valor de configuración en el archivo cknfastrc, que se encuentra en /opt/nfast/cknfastrc (o c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Después de agregar este valor de configuración al archivo cknfastrc, la nueva credencial se puede utilizar sin reiniciar el servidor de aplicaciones J2EE.

**La firma no es de confianza**

Al certificar y firmar el mismo documento PDF, si la firma certificadora no es de confianza, aparece un triángulo amarillo contra la primera firma al abrir el documento PDF en Acrobat o Adobe Reader. La firma certificadora debe ser de confianza para evitar esta situación.

**Documentos de firma que son formularios basados en XFA**

Si intenta firmar un formulario basado en XFA mediante la API de servicio de firma, es posible que falten los datos en el `View` `Signed` `Version` ubicado en Acrobat. Por ejemplo, considere el siguiente flujo de trabajo:

* Mediante un archivo XDP creado con Designer, se combina un diseño de formulario que contiene un campo de firma y datos XML que contienen datos de formulario. Utilice el servicio Forms para generar un documento PDF interactivo.
* Puede firmar el documento PDF con la API de servicio de firma.

### Resumen de los pasos {#summary_of_steps-3}

Para firmar digitalmente un documento PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de firma.
1. Obtenga el documento PDF para firmar.
1. Firme el documento PDF.
1. Guarde el documento PDF firmado como archivo PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (requerido si AEM Forms se implementa en JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss)

**Crear un cliente de firmas**

Para poder realizar una operación de servicio de firma mediante programación, debe crear un cliente de servicio de firma.

**Obtener el documento PDF para firmar**

Para firmar un documento PDF, debe obtener un documento PDF que contenga un campo de firma. Si un documento PDF no contiene un campo de firma, no se puede firmar. Se puede agregar un campo de firma mediante Designer o mediante programación.

**Firmar el documento PDF**

Al firmar un documento PDF, puede definir las opciones en tiempo de ejecución que utiliza el servicio Signature. Puede definir las siguientes opciones:

* Opciones de aspecto
* Comprobación de revocación
* Valores de marca de hora

Las opciones de apariencia se definen mediante un objeto `PDFSignatureAppearanceOptionSpec`. Por ejemplo, puede mostrar la fecha dentro de una firma invocando el método `PDFSignatureAppearanceOptionSpec` del objeto `setShowDate` y pasando `true`.

También puede especificar si desea o no realizar una comprobación de revocación que determine si se ha revocado el certificado que se utiliza para firmar digitalmente un documento PDF. Para realizar la comprobación de revocación, puede especificar uno de los siguientes valores:

* **NoCheck**: No realice la comprobación de revocación.
* **BestEffort**: Intente siempre comprobar la revocación de todos los certificados de la cadena. Si se produce algún problema al comprobar, se supone que la revocación es válida. Si se produce algún error, supongamos que el certificado no se revoca.
* **CheckIfAvailable:** Compruebe la revocación de todos los certificados de la cadena si hay información de revocación disponible. Si se produce algún problema al comprobar, se supone que la revocación no es válida. Si se produce algún error, supongamos que el certificado se ha revocado y no es válido. (Este es el valor predeterminado).
* **AlwaysCheck**: Compruebe la revocación de todos los certificados de la cadena. Si la información de revocación no está presente en ningún certificado, se supone que la revocación no es válida.

Para realizar la comprobación de revocación en un certificado, puede especificar una URL para un servidor de lista de revocación de certificados (CRL) mediante un objeto `CRLOptionSpec`. Sin embargo, si desea realizar una comprobación de revocación y no especifica una URL a un servidor CRL, el servicio Signature obtiene la URL del certificado.

En lugar de utilizar un servidor CRL, puede utilizar un servidor de protocolo de estado de certificado en línea (OCSP) al realizar la comprobación de revocación. Normalmente, cuando se utiliza un servidor OCSP en lugar de un servidor CRL, la comprobación de revocación se realiza más rápido. (Consulte &quot;Protocolo de estado de certificado en línea&quot; en [https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560)).

Puede establecer el orden de los servidores CRL y OCSP que utiliza el servicio de firmas mediante Aplicaciones y Servicios de Adobe. Por ejemplo, si el servidor OCSP se configura primero en Aplicaciones y servicios de Adobe, se selecciona el servidor OCSP, seguido del servidor CRL. (Consulte &quot;Administración de certificados y credenciales mediante el almacén de confianza&quot; en la Ayuda de AAC).

Si especifica que no se debe realizar la comprobación de revocación, el servicio Signature no comprueba si se ha revocado el certificado utilizado para firmar o certificar un documento. Es decir, se ignora la información del servidor CRL y OCSP.

>[!NOTE]
>
>Aunque se puede especificar una CRL o un servidor OCSP en el certificado, puede anular la dirección URL especificada en el certificado mediante un objeto `CRLOptionSpec` y un objeto `OCSPOptionSpec`. Por ejemplo, para anular el servidor CRL, puede invocar el método `CRLOptionSpec` del objeto `setLocalURI`.

La marca de hora se refiere al proceso de seguimiento de la hora en que se modificó un documento firmado o certificado. Una vez que se firma un documento, éste no debe ser modificado, ni siquiera por el propietario del documento. La marca de hora ayuda a garantizar la validez de un documento firmado o certificado. Puede definir las opciones de marca de hora mediante un objeto `TSPOptionSpec`. Por ejemplo, puede especificar la dirección URL de un servidor de proveedor de marca de hora (TSP).

>[!NOTE]
>
>En las secciones de Java y servicio Web y en los inicios rápidos correspondientes, se utiliza la verificación de revocación. Dado que no se especifica ninguna CRL ni información de servidor OCSP, la información de servidor se obtiene del certificado utilizado para firmar digitalmente el documento PDF.

Para firmar correctamente un documento PDF, puede especificar el nombre completo del campo de firma que contendrá la firma digital, como `form1[0].#subform[1].SignatureField3[3]`. Al utilizar un campo de formulario XFA, también se puede utilizar el nombre parcial del campo de firma: `SignatureField3[3]`.

También debe hacer referencia a una credencial de seguridad para firmar digitalmente un documento PDF. Para hacer referencia a una credencial de seguridad, debe especificar un alias. El alias es una referencia a una credencial real que puede estar en un archivo PKCS#12 (con la extensión .pfx) o en un módulo de seguridad de hardware (HSM). Para obtener información sobre las credenciales de seguridad, consulte la guía *Instalación e implementación de AEM Forms* para su servidor de aplicaciones.

**Guardar el documento PDF firmado**

Una vez que el servicio Signature firme digitalmente el documento PDF, puede guardarlo como archivo PDF para que los usuarios puedan abrirlo en Acrobat o Adobe Reader.

**Consulte también**

[Firmar digitalmente documentos PDF mediante la API de Java](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[Firma digital de documentos PDF mediante la API de servicio web](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Añadir campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields)

[Recuperación de nombres de campos de firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### Firmar digitalmente documentos PDF mediante la API de Java {#digitally-sign-pdf-documents-using-the-java-api}

Firmar digitalmente un documento PDF mediante la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente de firmas

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `SignatureServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtener el documento PDF para firmar

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF para firmar digitalmente utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Firmar el documento PDF

   Firme el documento PDF invocando el método `SignatureServiceClient` del objeto `sign` y pasando los valores siguientes:

   * Un objeto `com.adobe.idp.Document` que representa el documento PDF que se va a firmar.
   * Un valor de cadena que representa el nombre del campo de firma que contendrá la firma digital.
   * Un objeto `Credential` que representa las credenciales utilizadas para firmar digitalmente el documento PDF. Cree un objeto `Credential` invocando el método estático `Credential` del objeto `getInstance` y pasando un valor de cadena que especifica el valor de alias que corresponde a la credencial de seguridad.
   * Un objeto `HashAlgorithm` que especifica un miembro de datos estático que representa el algoritmo hash que se va a utilizar para compender el documento PDF. Por ejemplo, puede especificar `HashAlgorithm.SHA1` para utilizar el algoritmo SHA1.
   * Un valor de cadena que representa el motivo por el que el documento PDF se firmó digitalmente.
   * Un valor de cadena que representa la información de contacto del firmante.
   * Objeto `PDFSignatureAppearanceOptions` que controla el aspecto de la firma digital. Por ejemplo, puede utilizar este objeto para agregar un logotipo personalizado a una firma digital.
   * Un objeto `java.lang.Boolean` que especifica si se debe realizar una comprobación de revocación en el certificado del firmante.
   * Un objeto `OCSPOptionSpec` que almacena las preferencias para la compatibilidad con el protocolo de estado de certificado en línea (OCSP). Si no se realiza la comprobación de revocación, este parámetro no se utiliza y puede especificar `null`.
   * Objeto `CRLPreferences` que almacena las preferencias de lista de revocación de certificados (CRL). Si no se realiza la comprobación de revocación, este parámetro no se utiliza y puede especificar `null`.
   * Objeto `TSPPreferences` que almacena las preferencias para la compatibilidad con el proveedor de marca de hora (TSP). Este parámetro es opcional y puede ser `null`. Para obtener más información, consulte [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   El método `sign` devuelve un objeto `com.adobe.idp.Document` que representa el documento PDF firmado.

1. Guardar el documento PDF firmado

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea .pdf.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` y pase `java.io.File`para copiar el contenido del objeto `Document` en el archivo. Asegúrese de utilizar el objeto `com.adobe.idp.Document` devuelto por el método `sign`.

**Consulte también**

[Firma digital de Documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Inicio rápido (modo SOAP): Firma digital de un documento PDF mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Firma digital de documentos PDF mediante la API de servicio Web {#digitally-signing-pdf-documents-using-the-web-service-api}

Para firmar digitalmente un documento PDF mediante la API de firma (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Crear un cliente de firmas

   * Cree un objeto `SignatureServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `SignatureServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `SignatureServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtener el documento PDF para firmar

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar un documento PDF firmado.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF que se va a firmar y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` el contenido de la matriz de bytes.

1. Firmar el documento PDF

   Firme el documento PDF invocando el método `SignatureServiceClient` del objeto `sign` y pasando los valores siguientes:

   * Un objeto `BLOB` que representa el documento PDF que se va a firmar.
   * Un valor de cadena que representa el nombre del campo de firma que contendrá la firma digital.
   * Un objeto `Credential` que representa las credenciales utilizadas para firmar digitalmente el documento PDF. Cree un objeto `Credential` utilizando su constructor y especifique el alias asignando un valor a la propiedad `Credential` del objeto `alias`.
   * Un objeto `HashAlgorithm` que especifica un miembro de datos estático que representa el algoritmo hash que se va a utilizar para compender el documento PDF. Por ejemplo, puede especificar `HashAlgorithm.SHA1` para utilizar el algoritmo SHA1.
   * Un valor booleano que especifica si se utiliza el algoritmo hash.
   * Un valor de cadena que representa el motivo por el que el documento PDF se firmó digitalmente.
   * Un valor de cadena que representa la ubicación del firmante.
   * Un valor de cadena que representa la información de contacto del firmante.
   * Objeto `PDFSignatureAppearanceOptions` que controla el aspecto de la firma digital. Por ejemplo, puede utilizar este objeto para agregar un logotipo personalizado a una firma digital.
   * Un objeto `System.Boolean` que especifica si se debe realizar una comprobación de revocación en el certificado del firmante. Si esta comprobación de revocación se realiza, se incrusta en la firma. El valor predeterminado es `false`.
   * Un objeto `OCSPOptionSpec` que almacena las preferencias para la compatibilidad con el protocolo de estado de certificado en línea (OCSP). Si no se realiza la comprobación de revocación, este parámetro no se utiliza y puede especificar `null`. Para obtener información sobre este objeto, consulte [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Objeto `CRLPreferences` que almacena las preferencias de lista de revocación de certificados (CRL). Si no se realiza la comprobación de revocación, este parámetro no se utiliza y puede especificar `null`.
   * Objeto `TSPPreferences` que almacena las preferencias para la compatibilidad con el proveedor de marca de hora (TSP). Este parámetro es opcional y puede ser `null`.

   El método `sign` devuelve un objeto `BLOB` que representa el documento PDF firmado.

1. Guardar el documento PDF firmado

   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF firmado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` devuelto por el método `sign`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Firma digital de Documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Firma digital de Forms interactivo {#digitally-signing-interactive-forms}

Puede firmar un formulario interactivo que cree el servicio de Forms. Por ejemplo, considere el siguiente flujo de trabajo:

* Se combina un formulario PDF basado en XFA creado mediante Designer y datos de formulario ubicados en un documento XML mediante el servicio Forms. El servidor de Forms procesa un formulario interactivo.
* El formulario interactivo se firma con la API de servicio de firma.

El resultado es un formulario PDF interactivo con firma digital. Al firmar un formulario PDF basado en un formulario XFA, asegúrese de guardar el archivo PDF como un formulario PDF estático de Adobe. Si intenta firmar un formulario PDF guardado como formulario PDF dinámico de Adobe, se producirá una excepción. Como está firmando el formulario que se devuelve desde el servicio de Forms, asegúrese de que el formulario contiene un campo de firma.

>[!NOTE]
>
>Para poder firmar digitalmente un formulario interactivo, debe asegurarse de agregar el certificado a AEM Forms. Se agrega un certificado mediante la consola de administración o mediante programación mediante la API del administrador de confianza. (Consulte [Importación de credenciales mediante la API del administrador de confianza](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)).

Al utilizar la API de servicio de Forms, establezca la opción `GenerateServerAppearance` tiempo de ejecución en `true`. Esta opción de tiempo de ejecución garantiza que el aspecto del formulario generado en el servidor siga siendo válido cuando se abre en Acrobat o Adobe Reader. Se recomienda definir esta opción en tiempo de ejecución al generar un formulario interactivo para firmar mediante la API de Forms.

>[!NOTE]
>
>Antes de leer Forms interactivo con firma digital, se recomienda que esté familiarizado con la firma de documentos PDF. (Consulte [Firma digital de Documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)).

### Resumen de los pasos {#summary_of_steps-4}

Para firmar digitalmente un formulario interactivo que devuelve el servicio Forms, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de Forms y firmas.
1. Obtenga el formulario interactivo mediante el servicio Forms.
1. Firme el formulario interactivo.
1. Guarde el documento PDF firmado como archivo PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar (requerido si AEM Forms se implementa en JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de Forms y firmas**

Dado que este flujo de trabajo invoca los servicios Forms y Signature, cree un cliente de servicio Forms y un cliente de servicio Signature.

**Obtenga el formulario interactivo mediante el servicio Forms**

Puede utilizar el servicio Forms para obtener el formulario PDF interactivo que desea firmar. A partir de AEM Forms, puede pasar un objeto `com.adobe.idp.Document` al servicio de Forms que contenga el formulario que se va a procesar. El nombre de este método es `renderPDFForm2`. Este método devuelve un objeto `com.adobe.idp.Document` que contiene el formulario que se va a firmar. Puede pasar esta instancia `com.adobe.idp.Document` al servicio Signature.

Del mismo modo, si utiliza servicios Web, puede pasar la instancia `BLOB` que el servicio de Forms devuelve al servicio Signature.

>[!NOTE]
>
>El inicio rápido asociado con la sección Forms interactivo de firma digital invoca el método `renderPDFForm2`.

**Firmar el formulario interactivo**

Al firmar un documento PDF, puede definir las opciones de tiempo de ejecución que utiliza el servicio Signature. Puede definir las siguientes opciones:

* Opciones de aspecto
* Comprobación de revocación
* Valores de marca de hora

Las opciones de apariencia se definen mediante un objeto `PDFSignatureAppearanceOptionSpec`. Por ejemplo, puede mostrar la fecha dentro de una firma invocando el método `PDFSignatureAppearanceOptionSpec` del objeto `setShowDate` y pasando `true`.

**Guardar el documento PDF firmado**

Una vez que el servicio Signature firme digitalmente el documento PDF, puede guardarlo como archivo PDF. El archivo PDF se puede abrir en Acrobat o Adobe Reader.

**Consulte también**

[Firma digital de un formulario interactivo mediante la API de Java](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[Firma digital de un formulario interactivo mediante la API de servicio web](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Firma digital de Documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Representación de PDF forms interactivos](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### Firmar digitalmente un formulario interactivo con la API de Java {#digitally-sign-an-interactive-form-using-the-java-api}

Firmar digitalmente un formulario interactivo mediante la Forms y la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar y adobe-forms-client.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente de Forms y firmas

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `SignatureServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.
   * Cree un objeto `FormsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga el formulario interactivo mediante el servicio Forms

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF que se pasará al servicio Forms mediante su constructor. Pase un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.
   * Cree un objeto `java.io.FileInputStream` que represente el documento XML que contiene los datos de formulario que se pasarán al servicio Forms mediante su constructor. Pase un valor de cadena que especifique la ubicación del archivo XML.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.
   * Cree un objeto `PDFFormRenderSpec` que se utilice para definir las opciones de tiempo de ejecución. Invoque el método `PDFFormRenderSpec` del objeto `setGenerateServerAppearance` y pase `true`.
   * Invoque el método `FormsServiceClient` del objeto `renderPDFForm2` y pase los siguientes valores:

      * Objeto `com.adobe.idp.Document` que contiene el formulario PDF que se va a procesar.
      * Un objeto `com.adobe.idp.Document` que contiene datos para combinar con el formulario.
      * Un objeto `PDFFormRenderSpec` que almacena opciones de tiempo de ejecución.
      * Un objeto `URLSpec` que contiene valores de URI necesarios para el servicio de Forms. Puede especificar `null` para este valor de parámetro.
      * Objeto `java.util.HashMap` que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

      El método `renderPDFForm2` devuelve un objeto `FormsResult` que contiene una secuencia de datos de formulario

   * Recupere el formulario PDF invocando el método `FormsResult` del objeto `getOutputContent`. Este método devuelve un objeto `com.adobe.idp.Document` que representa el formulario interactivo.


1. Firmar el formulario interactivo

   Firme el documento PDF invocando el método `SignatureServiceClient` del objeto `sign` y pasando los valores siguientes:

   * Un objeto `com.adobe.idp.Document` que representa el documento PDF que se va a firmar. Asegúrese de que este objeto sea el objeto `com.adobe.idp.Document` obtenido del servicio de Forms.
   * Un valor de cadena que representa el nombre del campo de firma que se firma.
   * Un objeto `Credential` que representa las credenciales utilizadas para firmar digitalmente el documento PDF. Cree un objeto `Credential` invocando el método estático `Credential` del objeto `getInstance`. Pase un valor de cadena que especifique el valor de alias que corresponde a la credencial de seguridad.
   * Un objeto `HashAlgorithm` que especifica un miembro de datos estático que representa el algoritmo hash que se va a utilizar para compender el documento PDF. Por ejemplo, puede especificar `HashAlgorithm.SHA1` para utilizar el algoritmo SHA1.
   * Un valor de cadena que representa el motivo por el que el documento PDF se firmó digitalmente.
   * Un valor de cadena que representa la información de contacto del firmante.
   * Objeto `PDFSignatureAppearanceOptions` que controla el aspecto de la firma digital. Por ejemplo, puede utilizar este objeto para agregar un logotipo personalizado a una firma digital.
   * Un objeto `java.lang.Boolean` que especifica si se debe realizar una comprobación de revocación en el certificado del firmante.
   * Un objeto `OCSPPreferences` que almacena las preferencias para la compatibilidad con el protocolo de estado de certificado en línea (OCSP). Si no se realiza la comprobación de revocación, este parámetro no se utiliza y puede especificar `null`.
   * Objeto `CRLPreferences` que almacena las preferencias de lista de revocación de certificados (CRL). Si no se realiza la comprobación de revocación, este parámetro no se utiliza y puede especificar `null`.
   * Objeto `TSPPreferences` que almacena las preferencias para la compatibilidad con el proveedor de marca de hora (TSP). Este parámetro es opcional y puede ser `null`.

   El método `sign` devuelve un objeto `com.adobe.idp.Document` que representa el documento PDF firmado.

1. Guardar el documento PDF firmado

   * Cree un objeto `java.io.File` y asegúrese de que la extensión de nombre de archivo sea .pdf.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` y pase `java.io.File`para copiar el contenido del objeto `Document` en el archivo. Asegúrese de utilizar el objeto `com.adobe.idp.Document` que devolvió el método `sign`.

**Consulte también**

[Firma digital de Forms interactivo](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Inicio rápido (modo SOAP): Firma digital de un documento PDF mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Firmar digitalmente un formulario interactivo mediante la API de servicio Web {#digitally-sign-an-interactive-form-using-the-web-service-api}

Firmar digitalmente un formulario interactivo mediante la Forms y la API de firma (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Dado que esta aplicación cliente invoca dos servicios de AEM Forms, cree dos referencias de servicio. Utilice la siguiente definición WSDL para la referencia de servicio asociada con el servicio Signature: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   Utilice la siguiente definición WSDL para la referencia de servicio asociada al servicio Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Debido a que el tipo de datos `BLOB` es común a ambas referencias de servicio, califique completamente el tipo de datos `BLOB` al utilizarlo. En el inicio rápido correspondiente del servicio Web, todas las instancias `BLOB` están completamente calificadas.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Crear un cliente de Forms y firmas

   * Cree un objeto `SignatureServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `SignatureServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `SignatureServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Repita estos pasos para el cliente del servicio Forms.

1. Obtenga el formulario interactivo mediante el servicio Forms

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar un documento PDF firmado.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF que se va a firmar y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` el contenido de la matriz de bytes.
   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar datos de formulario.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo XML que contiene los datos del formulario y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` el contenido de la matriz de bytes.
   * Cree un objeto `PDFFormRenderSpec` que se utilice para definir las opciones de tiempo de ejecución. Asigne el valor `true` al campo `PDFFormRenderSpec` del objeto `generateServerAppearance`.
   * Invoque el método `FormsServiceClient` del objeto `renderPDFForm2` y pase los siguientes valores:

      * Objeto `BLOB` que contiene el formulario PDF que se va a procesar.
      * Un objeto `BLOB` que contiene datos para combinar con el formulario.
      * Un objeto `PDFFormRenderSpec` que almacena opciones de tiempo de ejecución.
      * Un objeto `URLSpec` que contiene valores de URI necesarios para el servicio de Forms. Puede especificar `null` para este valor de parámetro.
      * Objeto `java.util.HashMap` que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
      * Parámetro de salida largo utilizado para almacenar el número de páginas del formulario.
      * Parámetro de salida de cadena que se utiliza para el valor de configuración regional.
      * Un valor `FormResult` que es un parámetro de salida que se utiliza para almacenar el formulario interactivo.
   * Recupere el formulario PDF invocando el campo `FormsResult` del objeto `outputContent`. Este campo almacena un objeto `BLOB` que representa el formulario interactivo.


1. Firmar el formulario interactivo

   Firme el documento PDF invocando el método `SignatureServiceClient` del objeto `sign` y pasando los valores siguientes:

   * Un objeto `BLOB` que representa el documento PDF que se va a firmar. Utilice la instancia `BLOB` devuelta por el servicio de Forms.
   * Un valor de cadena que representa el nombre del campo de firma que se firma.
   * Un objeto `Credential` que representa las credenciales utilizadas para firmar digitalmente el documento PDF. Cree un objeto `Credential` utilizando su constructor y especifique el alias asignando un valor a la propiedad `Credential` del objeto `alias`.
   * Un objeto `HashAlgorithm` que especifica un miembro de datos estático que representa el algoritmo hash que se va a utilizar para compender el documento PDF. Por ejemplo, puede especificar `HashAlgorithm.SHA1` para utilizar el algoritmo SHA1.
   * Un valor booleano que especifica si se utiliza el algoritmo hash.
   * Un valor de cadena que representa el motivo por el que el documento PDF se firmó digitalmente.
   * Un valor de cadena que representa la ubicación del firmante.
   * Un valor de cadena que representa la información de contacto del firmante.
   * Objeto `PDFSignatureAppearanceOptions` que controla el aspecto de la firma digital. Por ejemplo, puede utilizar este objeto para agregar un logotipo personalizado a una firma digital.
   * Un objeto `System.Boolean` que especifica si se debe realizar una comprobación de revocación en el certificado del firmante. Si esta comprobación de revocación se realiza, se incrusta en la firma. El valor predeterminado es `false`.
   * Un objeto `OCSPPreferences` que almacena las preferencias para la compatibilidad con el protocolo de estado de certificado en línea (OCSP). Si no se realiza la comprobación de revocación, este parámetro no se utiliza y puede especificar `null`. Para obtener información sobre este objeto, consulte [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Objeto `CRLPreferences` que almacena las preferencias de lista de revocación de certificados (CRL). Si no se realiza la comprobación de revocación, este parámetro no se utiliza y puede especificar `null`.
   * Objeto `TSPPreferences` que almacena las preferencias para la compatibilidad con el proveedor de marca de hora (TSP). Este parámetro es opcional y puede ser `null`.

   El método `sign` devuelve un objeto `BLOB` que representa el documento PDF firmado.

1. Guardar el documento PDF firmado

   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF firmado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` devuelto por el método `sign`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Firma digital de Forms interactivo](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Certificación de Documentos PDF {#certifying-pdf-documents}

Puede asegurar un documento PDF certificándolo con un tipo particular de firma denominada firma certificada. Una firma certificada se distingue de una firma digital de las siguientes formas:

* Debe ser la primera firma aplicada al documento PDF; es decir, en el momento de aplicar la firma certificada, cualquier otro campo de firma del documento debe ser unsigned. Solo se permite una firma certificada en un documento PDF. Si desea firmar y certificar un documento PDF, debe certificarlo antes de firmarlo. Después de certificar un documento PDF, puede firmar digitalmente campos de firma adicionales.
* El autor o creador del documento puede especificar que el documento se puede modificar de determinadas formas sin invalidar la firma certificada. Por ejemplo, el documento puede permitir rellenar formularios o comentarios. Si el autor especifica que no se permite una modificación determinada, Acrobat impide que los usuarios modifiquen el documento de esa manera. Si se realizan dichas modificaciones, como por ejemplo utilizando otra aplicación, la firma certificada no es válida y Acrobat emite una advertencia cuando un usuario abre el documento. (Con las firmas no certificadas, no se evitan las modificaciones y las operaciones de edición normales no invalidan la firma original).
* En el momento de la firma, el documento se analiza para detectar tipos específicos de contenido que podrían hacer que el contenido de un documento sea ambiguo o engañoso. Por ejemplo, una anotación podría oscurecer algún texto de una página que sea importante para comprender lo que se está certificando. Se puede proporcionar una explicación (autenticación legal) sobre dicho contenido.

Puede certificar documentos PDF mediante programación mediante la API de Java del servicio de firmas o la API del servicio web de firmas. Al certificar un documento PDF, debe hacer referencia a una credencial de seguridad que exista en el servicio de credenciales. Para obtener información sobre las credenciales de seguridad, consulte la guía *Instalación e implementación de AEM Forms* para su servidor de aplicaciones.

>[!NOTE]
>
>Al certificar y firmar el mismo documento PDF, si la firma del certificado no es de confianza, aparece un triángulo amarillo junto a la primera firma de firma cuando se abre el documento PDF en Acrobat o Adobe Reader. Debe confiarse en la firma certificadora para evitar esta situación.

>[!NOTE]
>
>Cuando se utiliza una credencial nShield HSM de Cipher para firmar o certificar un documento PDF, no se puede utilizar la nueva credencial hasta que se reinicie el servidor de aplicaciones J2EE en el que se implementa AEM Forms. Sin embargo, puede establecer un valor de configuración, lo que resulta en que la operación de firma o certificación funcione sin reiniciar el servidor de aplicaciones J2EE.

Puede agregar el siguiente valor de configuración en el archivo cknfastrc, que se encuentra en /opt/nfast/cknfastrc (o c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Después de agregar este valor de configuración al archivo cknfastrc, la nueva credencial se puede utilizar sin reiniciar el servidor de aplicaciones J2EE.

>[!NOTE]
>
>Para obtener más información sobre el servicio Signature y la certificación de un documento, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-5}

Para certificar un documento PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de firma.
1. Obtenga el documento PDF para certificar.
1. Certifique el documento PDF.
1. Guarde el documento PDF certificado como archivo PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (requerido si AEM Forms se implementa en JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de firma**

Para poder realizar una operación de firma mediante programación, debe crear un cliente de firma.

**Obtener el documento PDF para certificar**

Para certificar un documento PDF, debe obtener un documento PDF que contenga un campo de firma. Si un documento PDF no contiene un campo de firma, no se puede certificar. Se puede agregar un campo de firma mediante Designer o mediante programación. Para obtener información sobre cómo agregar un campo de firma mediante programación, consulte [Añadir campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields).

**Certificar el documento PDF**

Para certificar correctamente un documento PDF, necesita los siguientes valores de entrada que utiliza el servicio Signature para certificar un documento PDF:

* **DOCUMENTO** PDF: Un documento PDF que contiene un campo de firma, que es un campo de formulario que contiene una representación gráfica de la firma certificada. Un documento PDF debe contener un campo de firma para poder certificarlo. Se puede agregar un campo de firma mediante Designer o mediante programación. (Consulte [Añadir campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields)).
* **Nombre** del campo de firma: Nombre completo del campo de firma que está certificado. El siguiente valor es un ejemplo: `form1[0].#subform[1].SignatureField3[3]`. Al utilizar un campo de formulario XFA, también se puede utilizar el nombre parcial del campo de firma: `SignatureField3[3]`. Si se pasa un valor nulo para el nombre del campo, se crea y certifica dinámicamente un campo de firma invisible.
* **Credenciales** de seguridad: Una credencial que se utiliza para certificar el documento PDF. Esta credencial de seguridad contiene una contraseña y un alias, que deben coincidir con un alias que aparece en la credencial que se encuentra dentro del servicio de credenciales. El alias es una referencia a una credencial real que puede estar en un archivo PKCS#12 (con la extensión .pfx) o en un módulo de seguridad de hardware (HSM).
* **Algoritmo** hash: Algoritmo hash que se usará para resumir el documento PDF.
* **Motivo de la firma**: Un valor que se muestra en Acrobat o Adobe Reader para que otros usuarios sepan el motivo por el que se certificó el documento PDF.
* **Ubicación del firmante**: Ubicación del firmante especificada por la credencial.
* **Información** de contacto: Información de contacto, como la dirección y el número de teléfono, del firmante.
* **Información** de permisos: Permisos que controlan las acciones que un usuario final puede realizar en un documento sin que la firma certificada no sea válida. Por ejemplo, puede establecer el permiso para que cualquier cambio en el documento PDF haga que la firma certificada no sea válida.
* **Explicación** legal: Cuando se certifica un documento, se escanea automáticamente en busca de tipos específicos de contenido que puedan hacer que el contenido de un documento sea ambiguo o engañoso. Por ejemplo, una anotación podría oscurecer algún texto de una página que sea importante para comprender lo que se está certificando. El proceso de análisis genera advertencias sobre estos tipos de contenido. Este valor proporciona una explicación adicional del contenido que puede haber generado advertencias.
* **Opciones** de aspecto: Opciones que controlan el aspecto de la firma certificada. Por ejemplo, la firma certificada puede mostrar información de fecha.
* **Comprobación** de revocación: Este valor especifica si la comprobación de revocación se realiza para el certificado del firmante. La configuración predeterminada de `false` significa que no se ha realizado la comprobación de revocación.
* **Configuración** de OCSP: Configuración de la compatibilidad con el protocolo de estado de certificado en línea (OCSP), que proporciona información sobre el estado de las credenciales que se utilizan para certificar el documento PDF. Por ejemplo, puede especificar la dirección URL del servidor que proporciona información sobre las credenciales que utiliza para iniciar sesión en el documento PDF.
* **Configuración** de CRL: Configuración de las preferencias de lista de revocación de certificados (CRL) si se ha realizado la comprobación de revocación. Por ejemplo, puede especificar que siempre se compruebe si se revocó una credencial.
* **Marca de hora**: Configuración que define la información de marca de hora que se aplica a la firma certificada. Una marca de hora indica que se establecieron datos específicos antes de un determinado momento. Este conocimiento ayuda a construir una relación de confianza entre el firmante y el verificador.

**Guardar el documento PDF certificado como archivo PDF**

Una vez que el servicio Signature certifique el documento PDF, puede guardarlo como archivo PDF para que los usuarios puedan abrirlo en Acrobat o Adobe Reader.

**Consulte también**

[Certificar documentos PDF mediante la API de Java](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[Certificar documentos PDF mediante la API de servicio web](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Añadir campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields)

### Certificar documentos PDF mediante la API de Java {#certify-pdf-documents-using-the-java-api}

Certifique un documento PDF mediante la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente de firma

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `SignatureServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtener el documento PDF para certificar

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF que se va a certificar mediante su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Certificar el documento PDF

   Certifique el documento PDF invocando el método `SignatureServiceClient` del objeto `certify` y pasando los siguientes valores:

   * El objeto `com.adobe.idp.Document` que representa el documento PDF que se va a certificar.
   * Un valor de cadena que representa el nombre del campo de firma que contendrá la firma.
   * Un objeto `Credential` que representa la credencial que se utiliza para certificar el documento PDF. Cree un objeto `Credential` invocando el método estático `Credential` del objeto `getInstance` y pasando un valor de cadena que especifica el valor de alias que corresponde a la credencial de seguridad.
   * Un objeto `HashAlgorithm` que especifica un miembro de datos estático que representa el algoritmo hash utilizado para resumir el documento PDF. Por ejemplo, puede especificar `HashAlgorithm.SHA1` para utilizar el algoritmo SHA1.
   * Un valor de cadena que representa el motivo por el que se certificó el documento PDF.
   * Un valor de cadena que representa la información de contacto del firmante.
   * Un objeto `MDPPermissions` que especifica acciones que se pueden realizar en el documento PDF que invalida la firma.
   * Objeto `PDFSignatureAppearanceOptions` que controla el aspecto de la firma certificada. Si lo desea, modifique el aspecto de la firma invocando un método como `setShowDate`.
   * Un valor de cadena que proporciona una explicación de las acciones que invalidan la firma.
   * Un objeto `java.lang.Boolean` que especifica si se debe realizar una comprobación de revocación en el certificado del firmante. Si esta comprobación de revocación se realiza, se incrusta en la firma. El valor predeterminado es `false`.
   * Un objeto `java.lang.Boolean` que especifica si el campo de firma que se está certificando está bloqueado. Si el campo está bloqueado, el campo de firma se marca como de solo lectura, sus propiedades no se pueden modificar y nadie que no tenga los permisos necesarios no puede borrarlo. El valor predeterminado es `false`.
   * Un objeto `OCSPPreferences` que almacena las preferencias para la compatibilidad con el protocolo de estado de certificado en línea (OCSP). Si no se realiza la comprobación de revocación, este parámetro no se utiliza y puede especificar `null`. Para obtener información sobre este objeto, consulte [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Objeto `CRLPreferences` que almacena las preferencias de lista de revocación de certificados (CRL). Si no se realiza la comprobación de revocación, este parámetro no se utiliza y puede especificar `null`.
   * Objeto `TSPPreferences` que almacena las preferencias para la compatibilidad con el proveedor de marca de hora (TSP). Por ejemplo, después de crear un objeto `TSPPreferences`, puede establecer la dirección URL del servidor TSP invocando el método `TSPPreferences` del objeto `setTspServerURL`. Este parámetro es opcional y puede ser `null`. Para obtener más información, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

   El método `certify` devuelve un objeto `com.adobe.idp.Document` que representa el documento PDF certificado.

1. Guardar el documento PDF certificado como archivo PDF

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea .pdf.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del objeto `com.adobe.idp.Document` en el archivo.

**Consulte también**

[Certificación de Documentos PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Inicio rápido (modo SOAP): Certificación de un documento PDF mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Certificar documentos PDF mediante la API de servicio Web {#certify-pdf-documents-using-the-web-service-api}

Certifique un documento PDF mediante la API de firma (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Crear un cliente de firma

   * Cree un objeto `SignatureServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `SignatureServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `SignatureServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtener el documento PDF para certificar

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar un documento PDF certificado.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF que se va a certificar y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando a su miembro de datos `MTOM` el contenido de la matriz de bytes.

1. Certificar el documento PDF

   Certifique el documento PDF invocando el método `SignatureServiceClient` del objeto `certify` y pasando los siguientes valores:

   * El objeto `BLOB` que representa el documento PDF que se va a certificar.
   * Un valor de cadena que representa el nombre del campo de firma que contendrá la firma.
   * Un objeto `Credential` que representa la credencial que se utiliza para certificar el documento PDF. Cree un objeto `Credential` utilizando su constructor y especifique el alias asignando un valor a la propiedad `Credential` del objeto `alias`.
   * Un objeto `HashAlgorithm` que especifica un miembro de datos estático que representa el algoritmo hash utilizado para resumir el documento PDF. Por ejemplo, puede especificar `HashAlgorithm.SHA1` para utilizar el algoritmo SHA1.
   * Un valor booleano que especifica si se utiliza el algoritmo hash.
   * Un valor de cadena que representa el motivo por el que se certificó el documento PDF.
   * Un valor de cadena que representa la ubicación del firmante.
   * Un valor de cadena que representa la información de contacto del firmante.
   * Un miembro de datos estático del objeto `MDPPermissions` que especifica las acciones que se pueden realizar en el documento PDF que invalidan la firma.
   * Un valor booleano que especifica si se utiliza el objeto `MDPPermissions` que se pasó como el valor del parámetro anterior.
   * Un valor de cadena que explica qué acciones invalidan la firma.
   * Objeto `PDFSignatureAppearanceOptions` que controla el aspecto de la firma certificada. Cree un objeto `PDFSignatureAppearanceOptions` utilizando su constructor. Puede modificar el aspecto de la firma estableciendo uno de sus miembros de datos.
   * Un objeto `System.Boolean` que especifica si se debe realizar una comprobación de revocación en el certificado del firmante. Si esta comprobación de revocación se realiza, se incrusta en la firma. El valor predeterminado es `false`.
   * Un objeto `System.Boolean` que especifica si el campo de firma que se está certificando está bloqueado. Si el campo está bloqueado, el campo de firma se marca como de solo lectura, sus propiedades no se pueden modificar y nadie que no tenga los permisos necesarios no puede borrarlo. El valor predeterminado es `false`.
   * Un objeto `System.Boolean` que especifica si el campo de firma está bloqueado. Es decir, si pasa `true` al parámetro anterior, pase `true` a este parámetro.
   * Un objeto `OCSPPreferences` que almacena las preferencias para la compatibilidad con el protocolo de estado de certificado en línea (OCSP), que proporciona información sobre el estado de la credencial que se utiliza para certificar el documento PDF. Si no se realiza la comprobación de revocación, este parámetro no se utiliza y puede especificar `null`.
   * Objeto `CRLPreferences` que almacena las preferencias de lista de revocación de certificados (CRL). Si no se realiza la comprobación de revocación, este parámetro no se utiliza y puede especificar `null`.
   * Objeto `TSPPreferences` que almacena las preferencias para la compatibilidad con el proveedor de marca de hora (TSP). Por ejemplo, después de crear un objeto `TSPPreferences`, puede establecer la dirección URL del TSP estableciendo el miembro de datos `TSPPreferences` del objeto `tspServerURL`. Este parámetro es opcional y puede ser `null`.

   El método `certify` devuelve un objeto `BLOB` que representa el documento PDF certificado.

1. Guardar el documento PDF certificado como archivo PDF

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF que contendrá el documento PDF certificado y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` devuelto por el método `certify`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `binaryData`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Certificación de Documentos PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verificación de firmas digitales {#verifying-digital-signatures}

Las firmas digitales se pueden comprobar para garantizar que no se haya modificado un documento PDF firmado y que la firma digital sea válida. Al verificar una firma digital, puede comprobar el estado de la firma y las propiedades de la firma, como la identidad del firmante. Antes de confiar en una firma digital, se recomienda verificarla. Al verificar una firma digital, haga referencia a un documento PDF que contenga una firma digital.

Supongamos que se desconoce la identidad del firmante. Al abrir el documento PDF en Acrobat, aparece un mensaje de advertencia que indica que la identidad del firmante es desconocida, como se muestra en la siguiente ilustración.

![vd_vd_verifysig](assets/vd_vd_verifysig.png)

Del mismo modo, cuando se verifica mediante programación una firma digital, se puede determinar el estado de la identidad del firmante. Por ejemplo, si comprueba la firma digital en el documento mostrado en la ilustración anterior, el resultado sería que se desconoce la identidad del firmante.

>[!NOTE]
>
>Para obtener más información sobre el servicio Signature y la verificación de firmas digitales, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-6}

Para comprobar una firma digital, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de firma.
1. Obtenga el documento PDF que contiene la firma para comprobarlo.
1. Configure las opciones de tiempo de ejecución de PKI.
1. Compruebe la firma digital.
1. Determine el estado de la firma.
1. Determinar la identidad del firmante.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, incluya los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (requerido si AEM Forms se implementa en JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de firma**

Antes de realizar una operación de servicio de firma mediante programación, cree un cliente de servicio de firma.

**Obtenga el documento PDF que contiene la firma para verificar**

Para comprobar una firma utilizada para firmar digitalmente o certificar un documento PDF, obtenga un documento PDF que contenga una firma.

**Definición de las opciones de tiempo de ejecución de PKI**

Defina estas opciones de tiempo de ejecución PKI que utiliza el servicio Signature al comprobar firmas en un documento PDF:

* Hora de verificación
* Comprobación de revocación
* Valores de marca de hora

Como parte de la configuración de estas opciones, puede especificar el tiempo de verificación. Por ejemplo, puede seleccionar la hora actual (la hora en el equipo del validador), que indica el uso de la hora actual. Para obtener información sobre los diferentes valores de tiempo, consulte el valor de lista desglosada `VerificationTime` en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

También puede especificar si desea realizar la comprobación de revocación como parte del proceso de verificación. Por ejemplo, puede realizar una comprobación de revocación para determinar si el certificado está revocado. Para obtener información sobre las opciones de comprobación de revocación, consulte el valor de lista desglosada `RevocationCheckStyle` en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Para realizar la comprobación de revocación en un certificado, especifique una URL para un servidor de lista de revocación de certificados (CRL) mediante un objeto `CRLOptionSpec`. Sin embargo, si no especifica una URL para el servidor CRL, el servicio Signature obtendrá la URL del certificado.

En lugar de utilizar un servidor CRL, puede utilizar un servidor de protocolo de estado de certificado en línea (OCSP) al realizar la comprobación de revocación. Normalmente, cuando se utiliza un servidor OCSP en lugar de un servidor CRL, la comprobación de revocación se realiza más rápido. (Consulte [Protocolo de estado de certificado en línea](https://tools.ietf.org/html/rfc2560).)

Puede establecer el orden de los servidores CRL y OCSP que utiliza el servicio Signature mediante el uso de aplicaciones y servicios de Adobe. Por ejemplo, si el servidor OCSP se configura primero en Aplicaciones y servicios de Adobe, se selecciona el servidor OCSP, seguido del servidor CRL.

Si no realiza la comprobación de revocación, el servicio Signature no comprueba si el certificado está revocado. Es decir, se ignora la información del servidor CRL y OCSP.

>[!NOTE]
>
>Puede anular la dirección URL especificada en el certificado mediante un objeto `CRLOptionSpec` y un objeto `OCSPOptionSpec`. Por ejemplo, para anular el servidor CRL, puede invocar el método `CRLOptionSpec` del objeto `setLocalURI`.

La marca de hora es el proceso de seguimiento de la hora en que se modificó un documento firmado o certificado. Después de firmar un documento, nadie puede modificarlo. La marca de hora ayuda a garantizar la validez de un documento firmado o certificado. Puede definir las opciones de marca de hora mediante un objeto `TSPOptionSpec`. Por ejemplo, puede especificar la dirección URL de un servidor de proveedor de marca de hora (TSP).

>[!NOTE]
>
>En los inicios rápidos de Java y servicio Web, el tiempo de verificación se establece en `VerificationTime.CURRENT_TIME` y la comprobación de revocación en `RevocationCheckStyle.BestEffort`. Dado que no se especifica ninguna CRL ni información de servidor OCSP, la información de servidor se obtiene del certificado.

**Verificar la firma digital**

Para verificar correctamente una firma, especifique el nombre completo del campo de firma que contiene la firma, como `form1[0].#subform[1].SignatureField3[3]`. Al utilizar un campo de formulario XFA, también puede utilizar el nombre parcial del campo de firma: `SignatureField3`.

De forma predeterminada, el servicio Signature limita la cantidad de tiempo que se puede firmar un documento después del tiempo de validación a 65 minutos. Si un usuario intenta comprobar una firma en este momento y la hora de firma es posterior a la hora actual y está a 65 minutos, el servicio Signature no crea un error de verificación.

>[!NOTE]
>
>Para conocer otros valores que se requieren al verificar una firma, consulte [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Determinar el estado de la firma**

Como parte de la verificación de una firma digital, puede comprobar el estado de la firma.

**Determinar la identidad del firmante**

Puede determinar la identidad del firmante, que puede ser uno de los siguientes valores:

* **Desconocido**: Este firmante es desconocido porque no se puede realizar la verificación del firmante.
* **De confianza**: Este firmante es de confianza.
* **No es de confianza**: Este firmante no es de confianza.

**Consulte también**

[Verificación de firmas digitales mediante la API de Java](#verify-digital-signatures-using-the-java-api)

[Verificar firmas digitales mediante la API de servicio web](#verify-digital-signatures-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificar firmas digitales mediante la API de Java {#verify-digital-signatures-using-the-java-api}

Verifique una firma digital mediante la API de servicio de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente de firma

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `SignatureServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga el documento PDF que contiene la firma para verificar

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF que contiene la firma que se va a comprobar utilizando su constructor. Pase un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Definición de las opciones de tiempo de ejecución de PKI

   * Cree un objeto `PKIOptions` utilizando su constructor.
   * Establezca el tiempo de verificación invocando el método `PKIOptions` del objeto `setVerificationTime` y pasando un valor de lista desglosada `VerificationTime` que especifica el tiempo de verificación.
   * Configure la opción de comprobación de revocación invocando el método `PKIOptions` del objeto `setRevocationCheckStyle` y pasando un valor de lista desglosada `RevocationCheckStyle` que especifica si se debe realizar la comprobación de revocación.

1. Verificar la firma digital

   Compruebe la firma invocando el método `SignatureServiceClient` del objeto `verify2` y pasando los siguientes valores:

   * Objeto `com.adobe.idp.Document` que contiene un documento PDF con firma digital o certificado.
   * Un valor de cadena que representa el nombre del campo de firma que contiene la firma que se va a comprobar.
   * Un objeto `PKIOptions` que contiene opciones de tiempo de ejecución PKI.
   * Instancia `VerifySPIOptions` que contiene información de SPI. Puede especificar `null` para este parámetro.

   El método `verify2` devuelve un objeto `PDFSignatureVerificationInfo` que contiene información que puede utilizarse para verificar la firma digital.

1. Determinar el estado de la firma

   * Determine el estado de la firma invocando el método `PDFSignatureVerificationInfo` del objeto `getStatus`. Este método devuelve un objeto `SignatureStatus` que especifica el estado de la firma. Por ejemplo, si no se modifica un documento PDF firmado, este método devuelve `SignatureStatus.DocumentSigNoChanges`.

1. Determinar la identidad del firmante

   * Determine la identidad del firmante invocando el método `PDFSignatureVerificationInfo` del objeto `getSigner`. Este método devuelve un objeto `IdentityInformation`.
   * Invoque el método `IdentityInformation` del objeto `getStatus` para determinar la identidad del firmante. Este método devuelve un valor de lista desglosada `IdentityStatus` que especifica la identidad. Por ejemplo, si el firmante es de confianza, este método devuelve `IdentityStatus.TRUSTED`.

**Consulte también**

[Verificación de firmas digitales](#verify-digital-signatures-using-the-java-api)

[Inicio rápido (modo SOAP): Verificación de una firma digital mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificar firmas digitales mediante la API de servicio Web {#verify-digital-signatures-using-the-web-service-api}

Verifique una firma digital mediante la API de servicio de firma (servicio Web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Crear un cliente de firma

   * Cree un objeto `SignatureServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `SignatureServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `SignatureServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento PDF que contiene la firma para verificar

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar un documento PDF que contiene una firma digital o certificada para verificarla.
   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF firmado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read`. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` el contenido de la matriz de bytes.

1. Definición de las opciones de tiempo de ejecución de PKI

   * Cree un objeto `PKIOptions` utilizando su constructor.
   * Establezca el tiempo de verificación asignando al miembro de datos `PKIOptions` del objeto `verificationTime` un valor de lista desglosada `VerificationTime` que especifique el tiempo de verificación.
   * Establezca la opción de comprobación de revocación asignando el miembro de datos `PKIOptions` del objeto `revocationCheckStyle` un valor de lista desglosada `RevocationCheckStyle` que especifique si desea realizar la comprobación de revocación.

1. Verificar la firma digital

   Compruebe la firma invocando el método `SignatureServiceClient` del objeto `verify2` y pasando los siguientes valores:

   * El objeto `BLOB` que contiene un documento PDF con firma digital o certificado.
   * Un valor de cadena que representa el nombre del campo de firma que contiene la firma que se va a comprobar.
   * Un objeto `PKIOptions` que contiene opciones de tiempo de ejecución PKI.
   * Instancia `VerifySPIOptions` que contiene información de SPI. Puede especificar `null` para este parámetro.

   El método `verify2` devuelve un objeto `PDFSignatureVerificationInfo` que contiene información que puede utilizarse para verificar la firma digital.

1. Determinar el estado de la firma

   Determine el estado de la firma obteniendo el valor del miembro de datos `PDFSignatureVerificationInfo` del objeto `status`. Este miembro de datos almacena un objeto `SignatureStatus` que especifica el estado de la firma. Por ejemplo, si se modifica un documento PDF firmado, el miembro de datos `status` almacena el valor `SignatureStatus.DocumentSigNoChanges`.

1. Determinar la identidad del firmante

   * Determine la identidad del firmante recuperando el valor del miembro de datos `PDFSignatureVerificationInfo` del objeto `signer`. Este miembro devuelve un objeto `IdentityInformation`.
   * Recupere el miembro de datos `IdentityInformation` del objeto `status` para determinar la identidad del firmante. Este miembro de datos devuelve un valor de lista desglosada `IdentityStatus` que especifica la identidad. Por ejemplo, si el firmante es de confianza, este miembro devuelve `IdentityStatus.TRUSTED`.

**Consulte también**

[Verificación de firmas digitales](#verify-digital-signatures-using-the-java-api)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verificación de varias firmas digitales {#verifying-multiple-digital-signatures}

AEM Forms proporciona los medios para comprobar todas las firmas digitales que se encuentran en un documento PDF. Supongamos que un documento PDF contiene varias firmas digitales como resultado de un proceso empresarial que requiere firmas de varios firmantes. Por ejemplo, considere una transacción financiera que requiere la firma de un responsable de préstamos y de un administrador. Puede utilizar la API de Java del servicio de firmas o la API del servicio web para comprobar todas las firmas del documento PDF. Al verificar varias firmas digitales, puede comprobar el estado y las propiedades de cada firma. Antes de confiar en una firma digital, se recomienda verificarla. Se recomienda que esté familiarizado con la verificación de una sola firma digital.

>[!NOTE]
>
>Para obtener más información sobre el servicio Signature y la verificación de firmas digitales, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-7}

Para verificar varias firmas digitales, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de firma.
1. Obtenga el documento PDF que contiene las firmas que se van a comprobar.
1. Configure las opciones de tiempo de ejecución de PKI.
1. Recupere todas las firmas digitales.
1. Repetir a través de todas las firmas.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, incluya los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (requerido si AEM Forms se implementa en JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de firma**

Antes de realizar una operación de servicio de firma mediante programación, cree un cliente de servicio de firma.

**Obtenga el documento PDF que contiene las firmas para verificar**

Para comprobar una firma utilizada para firmar digitalmente o certificar un documento PDF, obtenga un documento PDF que contenga una firma.

**Definición de las opciones de tiempo de ejecución de PKI**

Defina estas opciones de tiempo de ejecución PKI que utiliza el servicio Signature al comprobar todas las firmas de un documento PDF:

* Hora de verificación
* Comprobación de revocación
* Valores de marca de hora

Como parte de la configuración de estas opciones, puede especificar el tiempo de verificación. Por ejemplo, puede seleccionar la hora actual (la hora en el equipo del validador), que indica el uso de la hora actual. Para obtener información sobre los diferentes valores de tiempo, consulte el valor de lista desglosada `VerificationTime` en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

También puede especificar si desea realizar la comprobación de revocación como parte del proceso de verificación. Por ejemplo, puede realizar una comprobación de revocación para determinar si el certificado está revocado. Para obtener información sobre las opciones de comprobación de revocación, consulte el valor de lista desglosada `RevocationCheckStyle` en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Para realizar la comprobación de revocación en un certificado, especifique una URL para un servidor de lista de revocación de certificados (CRL) mediante un objeto `CRLOptionSpec`. Sin embargo, si no especifica una URL para un servidor CRL, el servicio Signature obtendrá la URL del certificado.

En lugar de utilizar un servidor CRL, puede utilizar un servidor de protocolo de estado de certificado en línea (OCSP) al realizar la comprobación de revocación. Normalmente, cuando se utiliza un servidor OCSP en lugar de un servidor CRL, la comprobación de revocación se realiza más rápido. (Consulte [Protocolo de estado de certificado en línea](https://tools.ietf.org/html/rfc2560).)

Puede establecer el orden de los servidores CRL y OCSP que utiliza el servicio Signature mediante el uso de aplicaciones y servicios de Adobe. Por ejemplo, si el servidor OCSP se establece primero en Aplicaciones y servicios de Adobe, se comprueba el servidor OCSP, seguido del servidor CRL.

Si no realiza la comprobación de revocación, el servicio Signature no comprueba si el certificado está revocado. Es decir, se ignora la información del servidor CRL y OCSP.

>[!NOTE]
>
>Puede anular la dirección URL especificada en el certificado mediante un objeto `CRLOptionSpec` y un objeto `OCSPOptionSpec`. Por ejemplo, para anular el servidor CRL, puede invocar el método `CRLOptionSpec` del objeto `setLocalURI`.

La marca de hora es el proceso de seguimiento de la hora en que se modificó un documento firmado o certificado. Después de firmar un documento, nadie puede modificarlo. La marca de hora ayuda a garantizar la validez de un documento firmado o certificado. Puede definir las opciones de marca de hora mediante un objeto `TSPOptionSpec`. Por ejemplo, puede especificar la dirección URL de un servidor de proveedor de marca de hora (TSP).

>[!NOTE]
>
>En los inicios rápidos de Java y servicio Web, el tiempo de verificación se establece en `VerificationTime.CURRENT_TIME` y la comprobación de revocación en `RevocationCheckStyle.BestEffort`. Dado que no se especifica ninguna CRL ni información de servidor OCSP, la información de servidor se obtiene del certificado.

**Recuperar todas las firmas digitales**

Para comprobar todas las firmas digitales ubicadas en un documento PDF, recupere las firmas digitales del documento PDF. Todas las firmas se devuelven en una lista. Como parte de la verificación de una firma digital, compruebe el estado de la firma.

>[!NOTE]
>
>A diferencia de lo que sucede cuando se comprueba una sola firma digital, cuando se verifican varias firmas, no es necesario especificar el nombre del campo de firma.

**Repetir mediante todas las firmas**

Repita cada firma. Es decir, para cada firma, verifique la firma digital y la identidad del firmante y el estado de cada firma. (Consulte [Verificación de firmas digitales](#verify-digital-signatures-using-the-java-api).)

>[!NOTE]
>
>No es necesario repetir todas las firmas si el requisito es el documento completo.

**Consulte también**

[Verificación de varias firmas digitales mediante la API de Java](#verify-digital-signatures-using-the-java-api)

[Verificación de varias firmas digitales mediante la API de servicio web](#verify-digital-signatures-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificar varias firmas digitales mediante la API de Java {#verify-multiple-digital-signatures-using-the-java-api}

Compruebe varias firmas digitales mediante la API de servicio de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente de firma

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `SignatureServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga el documento PDF que contiene las firmas para verificar

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF que contiene varias firmas digitales para comprobarlo mediante su constructor. Pase un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Definición de las opciones de tiempo de ejecución de PKI

   * Cree un objeto `PKIOptions` utilizando su constructor.
   * Establezca el tiempo de verificación invocando el método `PKIOptions` del objeto `setVerificationTime` y pasando un valor de lista desglosada `VerificationTime` que especifica el tiempo de verificación.
   * Configure la opción de comprobación de revocación invocando el método `PKIOptions` del objeto `setRevocationCheckStyle` y pasando un valor de lista desglosada `RevocationCheckStyle` que especifica si se debe realizar la comprobación de revocación.

1. Recuperar todas las firmas digitales

   Invoque el método `SignatureServiceClient` del objeto `verifyPDFDocument` y pase los siguientes valores:

   * Objeto `com.adobe.idp.Document` que contiene un documento PDF que contiene varias firmas digitales.
   * Un objeto `PKIOptions` que contiene opciones de tiempo de ejecución PKI.
   * Instancia `VerifySPIOptions` que contiene información de SPI. Puede especificar `null` para este parámetro.

   El método `verifyPDFDocument` devuelve un objeto `PDFDocumentVerificationInfo` que contiene información sobre todas las firmas digitales ubicadas en el documento PDF.

1. Repetir mediante todas las firmas

   * Repita todas las firmas invocando el método `PDFDocumentVerificationInfo` del objeto `getVerificationInfos`. Este método devuelve un objeto `java.util.List` donde cada elemento es un objeto `PDFSignatureVerificationInfo`. Utilice un objeto `java.util.Iterator` para iterar a través de la lista de firmas.
   * Con el objeto `PDFSignatureVerificationInfo`, puede realizar tareas como determinar el estado de la firma invocando el método `PDFSignatureVerificationInfo` del objeto `getStatus`. Este método devuelve un objeto `SignatureStatus` cuyo miembro de datos estáticos le informa sobre el estado de la firma. Por ejemplo, si la firma es desconocida, este método devuelve `SignatureStatus.DocumentSignatureUnknown`.

**Consulte también**

[Verificación de varias firmas digitales](#verifying-multiple-digital-signatures)

[Inicio rápido (modo SOAP): Verificación de varias firmas digitales mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Verificación de firmas digitales](#verify-digital-signatures-using-the-java-api)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificación de varias firmas digitales mediante la API de servicio Web {#verifying-multiple-digital-signatures-using-the-web-service-api}

Compruebe varias firmas digitales mediante la API de servicio de firma (servicio Web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Crear un cliente de firma

   * Cree un objeto `SignatureServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `SignatureServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `SignatureServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento PDF que contiene las firmas para verificar

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` almacena un documento PDF que contiene varias firmas digitales para verificar.
   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read`. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` el contenido de la matriz de bytes.

1. Definición de las opciones de tiempo de ejecución de PKI

   * Cree un objeto `PKIOptions` utilizando su constructor.
   * Establezca el tiempo de verificación asignando al miembro de datos `PKIOptions` del objeto `verificationTime` un valor de lista desglosada `VerificationTime` que especifique el tiempo de verificación.
   * Establezca la opción de comprobación de revocación asignando al miembro de datos `PKIOptions` del objeto `revocationCheckStyle` un valor de lista desglosada `RevocationCheckStyle` que especifique si desea realizar la comprobación de revocación.

1. Recuperar todas las firmas digitales

   Invoque el método `SignatureServiceClient` del objeto `verifyPDFDocument` y pase los siguientes valores:

   * Objeto `BLOB` que contiene un documento PDF que contiene varias firmas digitales.
   * Un objeto `PKIOptions` que contiene opciones de tiempo de ejecución PKI.
   * Instancia `VerifySPIOptions` que contiene información de SPI. Puede especificar null para este parámetro.

   El método `verifyPDFDocument` devuelve un objeto `PDFDocumentVerificationInfo` que contiene información sobre todas las firmas digitales ubicadas en el documento PDF.

1. Repetir mediante todas las firmas

   * Repita todas las firmas obteniendo el miembro de datos `PDFDocumentVerificationInfo` del objeto `verificationInfos`. Este miembro de datos devuelve una matriz `Object` donde cada elemento es un objeto `PDFSignatureVerificationInfo`.
   * Con el objeto `PDFSignatureVerificationInfo`, puede realizar tareas como determinar el estado de la firma obteniendo el miembro de datos `PDFSignatureVerificationInfo` del objeto `status`. Este miembro de datos devuelve un objeto `SignatureStatus` cuyo miembro de datos estáticos le informa sobre el estado de la firma. Por ejemplo, si la firma es desconocida, este método devuelve `SignatureStatus.DocumentSignatureUnknown`.

**Consulte también**

[Verificación de varias firmas digitales](#verifying-multiple-digital-signatures)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Eliminando firmas digitales {#removing-digital-signatures}

Las firmas digitales deben eliminarse de un campo de firma para poder aplicar una firma digital más reciente. No se puede sobrescribir una firma digital. Si intenta aplicar una firma digital a un campo de firma que contiene una firma, se producirá una excepción.

>[!NOTE]
>
>Para obtener más información sobre el servicio Signature, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-8}

Para quitar una firma digital de un campo de firma, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de firma.
1. Obtenga el documento PDF que contiene una firma para eliminar.
1. Elimine la firma digital del campo de firma.
1. Guarde el documento PDF como archivo PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (requerido si AEM Forms se implementa en JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de firma**

Para poder realizar una operación de servicio de firma mediante programación, debe crear un cliente de servicio de firma.

**Obtener el documento PDF que contiene una firma para eliminar**

Para quitar una firma de un documento PDF, debe obtener un documento PDF que contenga una firma.

**Quitar la firma digital del campo de firma**

Para eliminar correctamente una firma digital de un documento PDF, debe especificar el nombre del campo de firma que contiene la firma digital. Además, debe tener permiso para eliminar la firma digital; de lo contrario, se produce una excepción.

**Guardar el documento PDF como archivo PDF**

Una vez que el servicio Signature haya eliminado una firma digital de un campo de firma, puede guardar el documento PDF como archivo PDF para que los usuarios puedan abrirlo en Acrobat o Adobe Reader.

**Consulte también**

[Eliminación de firmas digitales mediante la API de Java](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[Eliminación de firmas digitales mediante la API de servicio web](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Añadir campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields)

### Eliminar firmas digitales mediante la API de Java {#remove-digital-signatures-using-the-java-api}

Elimine una firma digital mediante la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de firma.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `SignatureServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtener el documento PDF que contiene una firma para eliminar

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF que contiene la firma que se va a quitar mediante su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Quitar la firma digital del campo de firma

   Elimine una firma digital de un campo de firma invocando el método `SignatureServiceClient` del objeto `clearSignatureField` y pasando los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que representa el documento PDF que contiene la firma que se va a quitar.
   * Un valor de cadena que especifica el nombre del campo de firma que contiene la firma digital.

   El método `clearSignatureField` devuelve un objeto `com.adobe.idp.Document` que representa el documento PDF del que se eliminó la firma digital.

1. Guardar el documento PDF como archivo PDF

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea .pdf.
   * Invocar el método `com.adobe.idp.Document` del objeto `copyToFile`. Pase el objeto `java.io.File` para copiar el contenido del objeto `com.adobe.idp.Document` en el archivo. Asegúrese de utilizar el objeto `Document` devuelto por el método `clearSignatureField`.

**Consulte también**

[Eliminación de firmas digitales](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Inicio rápido (modo SOAP): Eliminación de una firma digital mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminar firmas digitales mediante la API de servicio Web {#remove-digital-signatures-using-the-web-service-api}

Elimine una firma digital mediante la API de firma (servicio Web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Crear un cliente de firma

   * Cree un objeto `SignatureServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `SignatureServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `SignatureServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtener el documento PDF que contiene una firma para eliminar

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar un documento PDF que contiene una firma digital que se va a quitar.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF firmado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read`. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Quitar la firma digital del campo de firma

   Elimine la firma digital invocando el método `SignatureServiceClient` del objeto `clearSignatureField` y pasando los siguientes valores:

   * Un objeto `BLOB` que contiene el documento PDF firmado.
   * Un valor de cadena que representa el nombre del campo de firma que contiene la firma digital que se va a quitar.

   El método `clearSignatureField` devuelve un objeto `BLOB` que representa el documento PDF del que se eliminó la firma digital.

1. Guardar el documento PDF como archivo PDF

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF que contiene un campo de firma vacío y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` devuelto por el método `sign`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en el archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Eliminación de firmas digitales](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
