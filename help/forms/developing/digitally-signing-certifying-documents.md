---
title: Firma digital y certificación de documentos
seo-title: Firma digital y certificación de documentos
description: nulo
seo-description: nulo
uuid: 6331de8a-2a9c-45bf-89d2-29f1ad5cc856
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 42de04bf-25e4-4478-a411-38671ed871ae
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Firma digital y certificación de documentos {#digitally-signing-and-certifying-documents}

**Acerca del servicio de firma**

El servicio Signature permite a su organización proteger la seguridad y la privacidad de los documentos Adobe PDF que distribuye y recibe. Este servicio utiliza firmas digitales y certificación para garantizar que solo los destinatarios previstos puedan modificar documentos. Dado que las funciones de seguridad se aplican al documento mismo, éste permanece seguro y controlado durante todo su ciclo de vida. Un documento permanece seguro más allá del servidor de seguridad, cuando se descarga sin conexión y cuando se envía de nuevo a la organización.

>[!NOTE]
>
>Puede crear un controlador de firma personalizado para el servicio Signature que se invoca cuando se invocan determinadas operaciones, como la firma de un documento PDF.

**Nombres de campos de firma**

Algunas operaciones del servicio de firma requieren que especifique el nombre del campo de firma en el que se realiza una operación. Por ejemplo, al firmar un documento PDF, se especifica el nombre del campo de firma que se va a firmar. Supongamos que el nombre completo de un campo de firma es `form1[0].Form1[0].SignatureField1[0]`. Puede especificar `SignatureField1[0]` en lugar de `form1[0].Form1[0].SignatureField1[0]`.

A veces, un conflicto hace que el servicio Signature firme firme (o realice otra operación que requiera el nombre del campo de firma) el campo incorrecto. Este conflicto es el resultado de que el nombre `SignatureField1[0]` aparezca en dos o más lugares del mismo documento PDF. Por ejemplo, considere un documento PDF que contenga dos campos de firma con el nombre `form1[0].Form1[0].SignatureField1[0]` y `form1[0].Form1[0].SubForm1[0].SignatureField1[0]` y especifique `SignatureField1[0]`. En este caso, el servicio Signature firma el primer campo de firma que encuentra mientras se iteran todos los campos de firma del documento.

Si hay varios campos de firma dentro de un documento PDF, se recomienda especificar los nombres completos de los campos de firma. Es decir, especifique `form1[0].Form1[0].SignatureField1[0]`en lugar de `SignatureField1[0]`.

Puede realizar estas tareas mediante el servicio Signature:

* Agregue y elimine campos de firma digital a un documento PDF. (Consulte [Adición de campos](digitally-signing-certifying-documents.md#adding-signature-fields)de firma).
* Recupere los nombres de los campos de firma ubicados en un documento PDF. (Consulte [Recuperación de nombres](digitally-signing-certifying-documents.md#retrieving-signature-field-names)de campos de firma).
* Modifique los campos de firma. (Consulte [Modificación de campos](digitally-signing-certifying-documents.md#modifying-signature-fields)de firma).
* Firmar digitalmente documentos PDF. (Consulte Firma [digital de documentos](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)PDF).
* Certificar documentos PDF. (Consulte [Certificación de documentos](digitally-signing-certifying-documents.md#certifying-pdf-documents)PDF).
* Valide las firmas digitales ubicadas en un documento PDF. (Consulte [Verificación de firmas](digitally-signing-certifying-documents.md#verifying-digital-signatures)digitales).
* Valide todas las firmas digitales ubicadas en un documento PDF. (Consulte [Verificación de varias firmas](digitally-signing-certifying-documents.md#verifying-digital-signatures)digitales).
* Quitar una firma digital de un campo de firma. (Consulte [Eliminación de firmas](digitally-signing-certifying-documents.md#removing-digital-signatures)digitales.)

   ***Nota **: Para obtener más información sobre el servicio Signature, consulte Referencia de[servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).*

## Adición de campos de firma {#adding-signature-fields}

Las firmas digitales aparecen en los campos de firma, que son campos de formulario que contienen una representación gráfica de la firma. Los campos de firma pueden ser visibles o invisibles. Los firmantes pueden utilizar un campo de firma preexistente o se puede agregar un campo de firma mediante programación. En cualquier caso, el campo de firma debe existir para poder firmar un documento PDF.

Puede agregar un campo de firma mediante programación mediante la API de Java del servicio de firma o la API del servicio web de firma. Puede agregar más de un campo de firma a un documento PDF; sin embargo, cada nombre de campo de firma debe ser único.

>[!NOTE]
>
>Algunos tipos de documento PDF no permiten agregar un campo de firma mediante programación. Para obtener más información sobre el servicio de firma y la adición de campos de firma, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para agregar un campo de firma a un documento PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de firma.
1. Obtenga un documento PDF al que se ha agregado un campo de firma.
1. Agregue un campo de firma.
1. Guarde el documento PDF como archivo PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

**Crear un cliente de firma**

Para poder realizar una operación de servicio de firma mediante programación, debe crear un cliente de servicio de firma.

**Obtener un documento PDF al que se ha agregado un campo de firma**

Debe obtener un documento PDF al que se agregue un campo de firma.

**Agregar un campo de firma**

Para agregar correctamente un campo de firma a un documento PDF, especifique valores de coordenadas que identifiquen la ubicación del campo de firma. (Si agrega un campo de firma invisible, estos valores no son obligatorios). Además, puede especificar qué campos del documento PDF se bloquean después de aplicar una firma al campo de firma.

**Guardar el documento PDF como archivo PDF**

Una vez que el servicio de firma agrega un campo de firma al documento PDF, puede guardar el documento como archivo PDF para que los usuarios puedan abrirlo en Acrobat o Adobe Reader.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Firma digital de documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Adición de campos de firma mediante la API de Java {#add-signature-fields-using-the-java-api}

Agregue un campo de firma mediante la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente de firma

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `SignatureServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtener un documento PDF al que se ha agregado un campo de firma

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF al que se agrega un campo de firma utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Agregar un campo de firma

   * Cree un `PositionRectangle` objeto que especifique la ubicación del campo de firma utilizando su constructor. En el constructor, especifique los valores de las coordenadas.
   * Si lo desea, cree un `FieldMDPOptions` objeto que especifique los campos bloqueados cuando se aplique una firma digital al campo de firma.
   * Agregue un campo de firma a un documento PDF invocando el `SignatureServiceClient` método `addSignatureField` del objeto y pasando los valores siguientes:

      * A `com.adobe.idp`. `Document` objeto que representa el documento PDF al que se agrega un campo de firma.
      * Un valor de cadena que especifica el nombre del campo de firma.
      * Un `java.lang.Integer` valor que representa el número de página al que se agrega un campo de firma.
      * Un `PositionRectangle` objeto que especifica la ubicación del campo de firma.
      * Objeto `FieldMDPOptions` que especifica los campos del documento PDF que se bloquean después de aplicar una firma digital al campo de firma. Este valor de parámetro es opcional y se puede pasar `null`.
   * Un `PDFSeedValueOptions` objeto que especifica varios valores de tiempo de ejecución. Este valor de parámetro es opcional y se puede pasar `null`.

      El `addSignatureField` método devuelve un `com.adobe.idp`. `Document` objeto que representa un documento PDF que contiene un campo de firma.
   >[!NOTE]
   >
   >Puede invocar el `SignatureServiceClient` método del `addInvisibleSignatureField` objeto para agregar un campo de firma invisible.

1. Guardar el documento PDF como archivo PDF

   * Cree un `java.io.File` objeto y asegúrese de que la extensión del archivo sea .pdf.
   * Invoque el `com.adobe.idp`. `Document` método `copyToFile` del objeto para copiar el contenido del `Document` objeto en el archivo. Asegúrese de utilizar el `com.adobe.idp`. `Document` objeto devuelto por el `addSignatureField` método.

**Consulte también**

[Inicio rápido de la API de servicio de firma](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### Adición de campos de firma mediante la API de servicio Web {#add-signature-fields-using-the-web-service-api}

Para agregar un campo de firma mediante la API de firma (servicio Web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Crear un cliente de firma

   * Cree un `SignatureServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `SignatureServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `SignatureServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtener un documento PDF al que se ha agregado un campo de firma

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar el documento PDF que contendrá un campo de firma.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` propiedad con el contenido de la matriz de bytes.

1. Agregar un campo de firma

   Agregue un campo de firma al documento PDF invocando el `SignatureServiceClient` método del `addSignatureField` objeto y pasando los valores siguientes:

   * Un `BLOB` objeto que representa el documento PDF al que se agrega un campo de firma.
   * Un valor de cadena que especifica el nombre del campo de firma.
   * Un valor entero que representa el número de página al que se agrega un campo de firma.
   * Un `PositionRect` objeto que especifica la ubicación del campo de firma.
   * Objeto `FieldMDPOptions` que especifica los campos del documento PDF que se bloquean después de aplicar una firma digital al campo de firma. Este valor de parámetro es opcional y se puede pasar `null`.
   * Un `PDFSeedValueOptions` objeto que especifica varios valores de tiempo de ejecución. Este valor de parámetro es opcional y se puede pasar `null`.
   El `addSignatureField` método devuelve un `BLOB` objeto que representa un documento PDF que contiene un campo de firma.

1. Guardar el documento PDF como archivo PDF

   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF que contendrá el campo de firma y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto devuelto por el `addSignatureField` método. Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `binaryData` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el `System.IO.BinaryWriter` método `Write` del objeto y pasando la matriz de bytes.

**Consulte también**

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Recuperación de nombres de campos de firma {#retrieving-signature-field-names}

Puede recuperar los nombres de todos los campos de firma que se encuentran en un documento PDF que desee firmar o certificar. Si no está seguro de los nombres de los campos de firma que se encuentran en un documento PDF o desea comprobar los nombres, puede recuperarlos mediante programación. El servicio Signature devuelve el nombre completo del campo de firma, como `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

>[!NOTE]
>
>Para obtener más información sobre el servicio Signature, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

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
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)de biblioteca Java de AEM Forms.

**Crear un cliente de firma**

Para poder realizar una operación de servicio de firma mediante programación, debe crear un cliente de servicio de firma.

**Obtener el documento PDF que contiene campos de firma**

Recupere un documento PDF que contenga campos de firma.

**Recuperar nombres de campo de firma**

Puede recuperar nombres de campo de firma después de recuperar un documento PDF que contenga uno o varios campos de firma.

**Consulte también**

[Recuperar nombres de campo de firma mediante la API de Java](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[Recuperar campo de firma mediante la API de servicio Web](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adición de campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields)

### Recuperar nombres de campo de firma mediante la API de Java {#retrieve-signature-field-names-using-the-java-api}

Recuperar nombres de campo de firma mediante la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente de firma

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `SignatureServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtener el documento PDF que contiene campos de firma

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF que contiene campos de firma utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Recuperar nombres de campo de firma

   * Recupere los nombres de los campos de firma invocando el `SignatureServiceClient` método `getSignatureFieldList` del objeto y pasando el `com.adobe.idp.Document` objeto que contiene el documento PDF que contiene los campos de firma. Este método devuelve un `java.util.List` objeto, en el que cada elemento contiene un `PDFSignatureField` objeto. Con este objeto, puede obtener información adicional sobre un campo de firma, como si está visible.
   * Repita el `java.util.List` objeto para determinar si hay nombres de campo de firma. Para cada campo de firma del documento PDF, puede obtener un `PDFSignatureField` objeto independiente. Para obtener el nombre del campo de firma, invoque el `PDFSignatureField` método del `getName` objeto. Este método devuelve un valor de cadena que especifica el nombre del campo de firma.

**Consulte también**

[Recuperación de nombres de campos de firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Inicio rápido (modo SOAP): Recuperación de nombres de campo de firma mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar campo de firma mediante la API de servicio Web {#retrieve-signature-field-using-the-web-service-api}

Recuperar nombres de campo de firma mediante la API de firma (servicio Web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Crear un cliente de firma

   * Cree un `SignatureServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `SignatureServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `SignatureServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtener el documento PDF que contiene campos de firma

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar el documento PDF que contiene campos de firma.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo al contenido de la matriz de bytes.

1. Recuperar nombres de campo de firma

   * Recupere los nombres de los campos de firma invocando el `SignatureServiceClient` método del `getSignatureFieldList` objeto y pasando el `BLOB` objeto que contiene el documento PDF que contiene los campos de firma. Este método devuelve un objeto de `MyArrayOfPDFSignatureField` colección donde cada elemento contiene un `PDFSignatureField` objeto.
   * Repita el `MyArrayOfPDFSignatureField` objeto para determinar si hay nombres de campo de firma. Para cada campo de firma del documento PDF, puede obtener un `PDFSignatureField` objeto. Para obtener el nombre del campo de firma, invoque el `PDFSignatureField` método del `getName` objeto. Este método devuelve un valor de cadena que especifica el nombre del campo de firma.

**Consulte también**

[Recuperación de nombres de campos de firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modificación de los campos de firma {#modifying-signature-fields}

Puede modificar los campos de firma que se encuentran en un documento PDF mediante la API de Java y la API de servicio Web. La modificación de un campo de firma implica la manipulación de los valores del diccionario de bloqueo de campos de firma o de los valores del diccionario de valores de raíz.

Un diccionario *de bloqueo de* campos especifica una lista de campos que se bloquean cuando se firma el campo de firma. Un campo bloqueado impide que los usuarios realicen cambios en el campo. Un diccionario *de valores* raíz contiene información de restricción que se utiliza en el momento en que se aplica la firma. Por ejemplo, puede cambiar los permisos que controlan las acciones que pueden producirse sin invalidar una firma.

Al modificar un campo de firma existente, puede realizar cambios en el documento PDF para reflejar los cambios en los requisitos comerciales. Por ejemplo, un nuevo requisito comercial puede requerir el bloqueo de todos los campos del documento una vez firmado el documento.

En esta sección se explica cómo modificar un campo de firma modificando los valores del diccionario de bloqueo de campos y del diccionario de valores de inicialización. Los cambios realizados en el diccionario de bloqueo del campo de firma tienen como resultado que todos los campos del documento PDF se bloqueen cuando se firma un campo de firma. Los cambios realizados en el diccionario de valores de inicialización prohíben tipos específicos de cambios en el documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio de firma y la modificación de los campos de firma, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)de biblioteca Java de LiveCycle.

**Crear un cliente de firma**

Para poder realizar una operación de servicio de firma mediante programación, debe crear un cliente de servicio de firma.

**Obtener el documento PDF que contiene el campo de firma para modificar**

Recupere un documento PDF que contenga el campo de firma que desea modificar.

**Definir valores de diccionario**

Para modificar un campo de firma, asigne valores a su diccionario de bloqueo de campo o diccionario de valores de raíz. Especificar los valores del diccionario de bloqueo de campos de firma implica especificar los campos del documento PDF que se bloquean cuando se firma el campo de firma. (En esta sección se explica cómo bloquear todos los campos).

Se pueden definir los siguientes valores del diccionario de valores de inicialización:

* **Comprobación** de revisión: Especifica si se realiza la comprobación de revocación cuando se aplica una firma al campo de firma.
* **Opciones** de certificado: Asigna valores al diccionario de valores de raíz del certificado. Antes de especificar las opciones de certificado, se recomienda familiarizarse con un diccionario de valores de raíz de certificado. (Consulte Referencia [](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)PDF).
* **Opciones** de resumen: Asigna algoritmos de compendio que se utilizan para firmar. Los valores válidos son SHA1, SHA256, SHA384, SHA512 y RIPEMD160.
* **Filtro**: Especifica el filtro que se utiliza con el campo de firma. Por ejemplo, puede utilizar el filtro Adobe.PPKLite. (Consulte Referencia [](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)PDF).
* **Opciones** de indicador: Especifica los valores del indicador asociados a este campo de firma. Un valor de 1 significa que un firmante debe utilizar solo los valores especificados para la entrada. Un valor de 0 significa que se permiten otros valores. Estas son las posiciones de Bit:

   * **** 1(Filtro): Controlador de firma que se va a utilizar para firmar el campo de firma
   * **** 2 (Subfiltro): Matriz de nombres que indica codificaciones aceptables para usar al firmar
   * **3 V)**: El número mínimo de versión requerido del controlador de firma que se va a utilizar para firmar el campo de firma
   * **** 4 (Motivos): Matriz de cadenas que especifica los posibles motivos para firmar un documento
   * **** 5 (PDFLegalWarnings): Una matriz de cadenas que especifican posibles autenticaciones legales

* **Afirmaciones** legales: Cuando un documento está certificado, se escanea automáticamente en busca de tipos específicos de contenido que puedan hacer que el contenido visible de un documento sea ambiguo o engañoso. Por ejemplo, una anotación puede oscurecer el texto que es importante para comprender lo que se está certificando. El proceso de análisis genera advertencias que indican la presencia de este tipo de contenido. También proporciona una explicación adicional del contenido que puede haber generado advertencias.
* **Permisos**: Especifica los permisos que se pueden utilizar en un documento PDF sin invalidar la firma.
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

[Inicio rápido de la API de servicio de firma](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[Firma digital de documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Modificación de campos de firma mediante la API de Java {#modify-signature-fields-using-the-java-api}

Modifique un campo de firma mediante la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente de firma

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `SignatureServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtener el documento PDF que contiene el campo de firma para modificar

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF que contiene el campo de firma que se va a modificar con su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Definir valores de diccionario

   * Cree un `PDFSignatureFieldProperties` objeto con su constructor. Un `PDFSignatureFieldProperties` objeto almacena información del diccionario de bloqueo de campos de firma y del diccionario de valores de raíz.
   * Cree un `PDFSeedValueOptionSpec` objeto con su constructor. Este objeto permite definir valores de diccionario de valores de inicialización.
   * No permitir cambios en el documento PDF invocando el `PDFSeedValueOptionSpec` método del `setMdpValue` objeto y pasando el valor de la `MDPPermissions.NoChanges` enumeración.
   * Cree un `FieldMDPOptionSpec` objeto con su constructor. Este objeto permite definir valores del diccionario de bloqueo de campos de firma.
   * Bloquear todos los campos del documento PDF invocando el `FieldMDPOptionSpec` método del `setMdpValue` objeto y pasando el valor de la `FieldMDPAction.ALL` enumeración.
   * Configure la información del diccionario de valores de inicialización invocando el `PDFSignatureFieldProperties` método `setSeedValue` del objeto y pasando el `PDFSeedValueOptionSpec` objeto.
   * Para definir la información del diccionario de bloqueo de campos de firma, invoque el método del `PDFSignatureFieldProperties`objeto y pase el `setFieldMDP` objeto `FieldMDPOptionSpec` .
   >[!NOTE]
   >
   >Para ver todos los valores del diccionario de valores de raíz que puede establecer, consulte la referencia de la `PDFSeedValueOptionSpec` clase. (Consulte Referencia [de la API de](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms).

1. Modificación del campo de firma

   Modifique el campo de firma invocando el `SignatureServiceClient` método `modifySignatureField` del objeto y pasando los siguientes valores:

   * El `com.adobe.idp.Document` objeto que almacena el documento PDF que contiene el campo de firma que se va a modificar
   * Un valor de cadena que especifica el nombre del campo de firma
   * El `PDFSignatureFieldProperties` objeto que almacena la información del diccionario de bloqueo de campos de firma y del diccionario de valores de raíz
   El `modifySignatureField` método devuelve un `com.adobe.idp.Document` objeto que almacena un documento PDF que contiene el campo de firma modificado.

1. Guardar el documento PDF como archivo PDF

   * Cree un `java.io.File` objeto y asegúrese de que la extensión del nombre de archivo sea .pdf.
   * Invocar el `com.adobe.idp.Document` método del `copyToFile` objeto para copiar el contenido del `com.adobe.idp.Document` objeto en el archivo. Asegúrese de utilizar el `com.adobe.idp.Document` objeto que devolvió el `modifySignatureField` método.

### Modificación de campos de firma mediante la API de servicio Web {#modify-signature-fields-using-the-web-service-api}

Modifique un campo de firma mediante la API de firma (servicio Web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Crear un cliente de firma

   * Cree un `SignatureServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `SignatureServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `SignatureServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtener el documento PDF que contiene el campo de firma para modificar

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar el documento PDF que contiene el campo de firma que se va a modificar.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` propiedad al contenido de la matriz de bytes.

1. Definir valores de diccionario

   * Cree un `PDFSignatureFieldProperties` objeto con su constructor. Este objeto almacena información del diccionario de bloqueo de campos de firma y del diccionario de valores de raíz.
   * Cree un `PDFSeedValueOptionSpec` objeto con su constructor. Este objeto permite definir valores de diccionario de valores de inicialización.
   * No permitir cambios en el documento PDF asignando el valor de `MDPPermissions.NoChanges` enumeración al miembro de `PDFSeedValueOptionSpec` datos del `mdpValue` objeto.
   * Cree un `FieldMDPOptionSpec` objeto con su constructor. Este objeto permite definir valores del diccionario de bloqueo de campos de firma.
   * Bloquear todos los campos del documento PDF asignando el valor de `FieldMDPAction.ALL` enumeración al miembro de `FieldMDPOptionSpec` datos del `mdpValue` objeto.
   * Defina la información del diccionario de valores de inicialización asignando el `PDFSeedValueOptionSpec` objeto al miembro de datos del `PDFSignatureFieldProperties` objeto `seedValue` .
   * Para definir la información del diccionario de bloqueo de campos de firma, asigne el `FieldMDPOptionSpec` objeto al miembro de datos del `PDFSignatureFieldProperties` objeto `fieldMDP` .
   >[!NOTE]
   >
   >Para ver todos los valores del diccionario de valores de raíz que puede establecer, consulte la referencia de la `PDFSeedValueOptionSpec` clase. (Consulte Referencia [de la API de](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms).

1. Modificación del campo de firma

   Modifique el campo de firma invocando el `SignatureServiceClient` método `modifySignatureField` del objeto y pasando los siguientes valores:

   * El `BLOB` objeto que almacena el documento PDF que contiene el campo de firma que se va a modificar
   * Un valor de cadena que especifica el nombre del campo de firma
   * El `PDFSignatureFieldProperties` objeto que almacena la información del diccionario de bloqueo de campos de firma y del diccionario de valores de raíz
   El `modifySignatureField` método devuelve un `BLOB` objeto que almacena un documento PDF que contiene el campo de firma modificado.

1. Guardar el documento PDF como archivo PDF

   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF que contendrá el campo de firma y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto que devuelve el `addSignatureField` método. Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el `System.IO.BinaryWriter` método `Write` del objeto y pasando la matriz de bytes.

**Consulte también**

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Firma digital de documentos PDF {#digitally-signing-pdf-documents}

Las firmas digitales se pueden aplicar a documentos PDF para proporcionar un nivel de seguridad. Las firmas digitales, como las firmas manuscritas, proporcionan un medio para que los firmantes se identifiquen y hagan declaraciones sobre un documento. La tecnología utilizada para firmar documentos digitalmente ayuda a garantizar que tanto el firmante como los destinatarios tengan una idea clara de lo que se firmó y estén seguros de que el documento no se ha modificado desde que se firmó.

Los documentos PDF se firman mediante tecnología de clave pública. Un firmante tiene dos claves: una clave pública y una clave privada. La clave privada se almacena en las credenciales de un usuario que deben estar disponibles en el momento de la firma. La clave pública se almacena en el certificado del usuario que debe estar disponible para que los destinatarios puedan validar la firma. La información sobre los certificados revocados se encuentra en las listas de revocación de certificados (CRL) y en las respuestas de protocolo de estado de certificado en línea (OCSP) distribuidas por las autoridades certificadas (CA). La hora de firma se puede obtener de un origen de confianza conocido como Autoridad de marca de hora.

>[!NOTE]
>
>Para poder firmar digitalmente un documento PDF, debe asegurarse de agregar el certificado a AEM Forms. Se agrega un certificado mediante la consola de administración o mediante programación mediante la API del administrador de confianza. (Consulte [Importación de credenciales mediante la API](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)del administrador de confianza).

Puede firmar documentos PDF digitalmente mediante programación. Al firmar digitalmente un documento PDF, debe hacer referencia a una credencial de seguridad que existe en AEM Forms. La credencial es la clave privada que se utiliza para firmar.

El servicio Signature realiza los siguientes pasos cuando se firma un documento PDF:

1. El servicio Signature recupera las credenciales del Truststore pasando el alias especificado en la solicitud.
1. Truststore busca la credencial especificada.
1. La credencial se devuelve al servicio Signature y se utiliza para firmar el documento. Las credenciales también se almacenan en la caché con el alias para solicitudes futuras.

Para obtener información sobre la gestión de credenciales de seguridad, consulte la guía *Instalación e implementación de AEM Forms* para su servidor de aplicaciones.

>[!NOTE]
>
>Existen diferencias entre la firma y la certificación de documentos. (Consulte [Certificación de documentos](digitally-signing-certifying-documents.md#certifying-pdf-documents)PDF).

>[!NOTE]
>
>No todos los documentos PDF admiten la firma. Para obtener más información sobre el servicio Signature y la firma digital de documentos, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>El servicio Signature no admite archivos XDP con datos PDF incrustados como entrada para una operación, como la certificación de un documento. Esta acción provoca que el servicio de firmas emita un `PDFOperationException`. Para resolver este problema, convierta el archivo XDP a un archivo PDF mediante el servicio Utilidades de PDF y, a continuación, pase el archivo PDF convertido a una operación de servicio de firma. (Consulte [Uso de las utilidades](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities)PDF).

**Credencial nShield HSM de cifrado**

Cuando se utiliza una credencial Cipher nShield HSM para firmar o certificar un documento PDF, no se puede utilizar la nueva credencial hasta que se reinicie el servidor de aplicaciones J2EE en el que se implementa AEM Forms. Sin embargo, puede establecer un valor de configuración, lo que resulta en que la operación de firma o certificación funcione sin reiniciar el servidor de aplicaciones J2EE.

Puede agregar el siguiente valor de configuración en el archivo cknfastrc, que se encuentra en /opt/nfast/cknfastrc (o c:\nfast\cknfastrc):

```as3
 CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Después de agregar este valor de configuración al archivo cknfastrc, la nueva credencial se puede utilizar sin reiniciar el servidor de aplicaciones J2EE.

**La firma no es de confianza**

Al certificar y firmar el mismo documento PDF, si la firma certificadora no es de confianza, aparece un triángulo amarillo contra la primera firma al abrir el documento PDF en Acrobat o Adobe Reader. La firma certificadora debe ser de confianza para evitar esta situación.

**Firma de documentos que son formularios basados en XFA**

Si intenta firmar un formulario basado en XFA con la API de servicio de firma, es posible que falten datos del `View` sitio `Signed` `Version` de Acrobat. Por ejemplo, considere el siguiente flujo de trabajo:

* Mediante un archivo XDP creado con Designer, se combina un diseño de formulario que contiene un campo de firma y datos XML que contienen datos de formulario. El servicio Forms se utiliza para generar un documento PDF interactivo.
* El documento PDF se firma con la API de servicio de firma.

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
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

**Crear un cliente de firmas**

Para poder realizar una operación de servicio de firma mediante programación, debe crear un cliente de servicio de firma.

**Obtener el documento PDF que firmar**

Para firmar un documento PDF, debe obtener un documento PDF que contenga un campo de firma. Si un documento PDF no contiene un campo de firma, no se puede firmar. Se puede agregar un campo de firma mediante Designer o mediante programación.

**Firmar el documento PDF**

Al firmar un documento PDF, puede definir las opciones en tiempo de ejecución que utiliza el servicio Signature. Puede definir las siguientes opciones:

* Opciones de aspecto
* Comprobación de revocación
* Valores de marca de hora

Las opciones de apariencia se definen mediante un `PDFSignatureAppearanceOptionSpec` objeto. Por ejemplo, puede mostrar la fecha dentro de una firma invocando el `PDFSignatureAppearanceOptionSpec` método `setShowDate` del objeto y pasando `true`.

También puede especificar si desea o no realizar una comprobación de revocación que determine si el certificado que se utiliza para firmar digitalmente un documento PDF se ha revocado. Para realizar la comprobación de revocación, puede especificar uno de los siguientes valores:

* **NoCheck**: No realice la comprobación de revocación.
* **BestEffort**: Intente siempre comprobar la revocación de todos los certificados de la cadena. Si se produce algún problema al comprobar, se supone que la revocación es válida. Si se produce algún error, supongamos que el certificado no se revoca.
* **** CheckIfAvailable: Compruebe la revocación de todos los certificados de la cadena si hay información de revocación disponible. Si se produce algún problema al comprobar, se supone que la revocación no es válida. Si se produce algún error, supongamos que el certificado se ha revocado y no es válido. (Este es el valor predeterminado).
* **AlwaysCheck**: Compruebe la revocación de todos los certificados de la cadena. Si la información de revocación no está presente en ningún certificado, se supone que la revocación no es válida.

Para realizar la comprobación de revocación en un certificado, puede especificar una URL para un servidor de lista de revocación de certificados (CRL) mediante un `CRLOptionSpec` objeto. Sin embargo, si desea realizar una comprobación de revocación y no especifica una URL a un servidor CRL, el servicio Signature obtiene la URL del certificado.

En lugar de utilizar un servidor CRL, puede utilizar un servidor de protocolo de estado de certificado en línea (OCSP) al realizar la comprobación de revocación. Normalmente, cuando se utiliza un servidor OCSP en lugar de un servidor CRL, la comprobación de revocación se realiza más rápido. (Consulte &quot;Protocolo de estado de certificado en línea&quot; en [https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560)).

Puede establecer el orden de los servidores CRL y OCSP que utiliza el servicio de firmas mediante las aplicaciones y los servicios de Adobe. Por ejemplo, si el servidor OCSP se establece primero en Aplicaciones y servicios de Adobe, se comprueba el servidor OCSP, seguido del servidor CRL. (Consulte &quot;Administración de certificados y credenciales mediante el almacén de confianza&quot; en la Ayuda de AAC).

Si especifica que no se debe realizar la comprobación de revocación, el servicio Signature no comprueba si se ha revocado el certificado utilizado para firmar o certificar un documento. Es decir, se ignora la información del servidor CRL y OCSP.

>[!NOTE]
>
>Aunque se puede especificar una CRL o un servidor OCSP en el certificado, puede anular la URL especificada en el certificado mediante un `CRLOptionSpec` objeto y un `OCSPOptionSpec` objeto. Por ejemplo, para anular el servidor CRL, puede invocar el `CRLOptionSpec` método `setLocalURI` del objeto.

La marca de hora se refiere al proceso de seguimiento de la hora en que se modificó un documento firmado o certificado. Una vez que se firma un documento, éste no debe modificarse, ni siquiera por parte del propietario del documento. La marca de hora ayuda a reforzar la validez de un documento firmado o certificado. Puede definir las opciones de marca de hora mediante un `TSPOptionSpec` objeto. Por ejemplo, puede especificar la dirección URL de un servidor de proveedor de marca de hora (TSP).

>[!NOTE]
>
>En las secciones de Java y servicio Web y los inicios rápidos correspondientes, se utiliza la verificación de revocación. Dado que no se especifica ninguna CRL ni información de servidor OCSP, la información de servidor se obtiene del certificado utilizado para firmar digitalmente el documento PDF.

Para firmar correctamente un documento PDF, puede especificar el nombre completo del campo de firma que contendrá la firma digital, como `form1[0].#subform[1].SignatureField3[3]`. Al utilizar un campo de formulario XFA, también se puede utilizar el nombre parcial del campo de firma: `SignatureField3[3]`.

También debe hacer referencia a una credencial de seguridad para firmar digitalmente un documento PDF. Para hacer referencia a una credencial de seguridad, debe especificar un alias. El alias es una referencia a una credencial real que puede estar en un archivo PKCS#12 (con la extensión .pfx) o en un módulo de seguridad de hardware (HSM). Para obtener información sobre las credenciales de seguridad, consulte la guía *Instalación e implementación de AEM Forms* para el servidor de aplicaciones.

**Guardar el documento PDF firmado**

Una vez que el servicio de firma firme digitalmente el documento PDF, puede guardarlo como archivo PDF para que los usuarios puedan abrirlo en Acrobat o Adobe Reader.

**Consulte también**

[Firmar digitalmente documentos PDF mediante la API de Java](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[Firma digital de documentos PDF mediante la API de servicio web](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adición de campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields)

[Recuperación de nombres de campos de firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### Firmar digitalmente documentos PDF mediante la API de Java {#digitally-sign-pdf-documents-using-the-java-api}

Firmar digitalmente un documento PDF mediante la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente de firmas

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `SignatureServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtener el documento PDF que firmar

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF para firmar digitalmente utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Firmar el documento PDF

   Firme el documento PDF invocando el `SignatureServiceClient` método `sign` del objeto y pasando los siguientes valores:

   * Un `com.adobe.idp.Document` objeto que representa el documento PDF que se va a firmar.
   * Un valor de cadena que representa el nombre del campo de firma que contendrá la firma digital.
   * Un `Credential` objeto que representa las credenciales utilizadas para firmar digitalmente el documento PDF. Cree un `Credential` objeto invocando el método estático del `Credential` objeto y pasando un `getInstance` valor de cadena que especifica el valor de alias que corresponde a la credencial de seguridad.
   * Un `HashAlgorithm` objeto que especifica un miembro de datos estático que representa el algoritmo hash que se va a utilizar para compender el documento PDF. Por ejemplo, puede especificar `HashAlgorithm.SHA1` el uso del algoritmo SHA1.
   * Un valor de cadena que representa el motivo por el que el documento PDF se firmó digitalmente.
   * Un valor de cadena que representa la información de contacto del firmante.
   * Un `PDFSignatureAppearanceOptions` objeto que controla el aspecto de la firma digital. Por ejemplo, puede utilizar este objeto para agregar un logotipo personalizado a una firma digital.
   * Un `java.lang.Boolean` objeto que especifica si se va a realizar la comprobación de revocación en el certificado del firmante.
   * Un `OCSPOptionSpec` objeto que almacena las preferencias para la compatibilidad con el protocolo de estado de certificado en línea (OCSP). Si no se realiza la comprobación de revocación, este parámetro no se utiliza y puede especificar `null`.
   * Un `CRLPreferences` objeto que almacena las preferencias de la lista de revocación de certificados (CRL). Si no se realiza la comprobación de revocación, este parámetro no se utiliza y puede especificar `null`.
   * Objeto `TSPPreferences` que almacena las preferencias de compatibilidad con el proveedor de marca de hora (TSP). Este parámetro es opcional y puede ser `null`. Para obtener más información, consulte [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   El `sign` método devuelve un `com.adobe.idp.Document` objeto que representa el documento PDF firmado.

1. Guardar el documento PDF firmado

   * Cree un `java.io.File` objeto y asegúrese de que la extensión del archivo sea .pdf.
   * Invoque el `com.adobe.idp.Document` método del `copyToFile` objeto y pase `java.io.File`para copiar el contenido del `Document` objeto en el archivo. Asegúrese de utilizar el `com.adobe.idp.Document` objeto devuelto por el `sign` método .

**Consulte también**

[Firma digital de documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Inicio rápido (modo SOAP): Firma digital de un documento PDF mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Firma digital de documentos PDF mediante la API de servicio web {#digitally-signing-pdf-documents-using-the-web-service-api}

Para firmar digitalmente un documento PDF mediante la API de firma (servicio Web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Crear un cliente de firmas

   * Cree un `SignatureServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `SignatureServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `SignatureServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtener el documento PDF que firmar

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar un documento PDF firmado.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF que se va a firmar, así como el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` propiedad al contenido de la matriz de bytes.

1. Firmar el documento PDF

   Firme el documento PDF invocando el `SignatureServiceClient` método `sign` del objeto y pasando los siguientes valores:

   * Un `BLOB` objeto que representa el documento PDF que se va a firmar.
   * Un valor de cadena que representa el nombre del campo de firma que contendrá la firma digital.
   * Un `Credential` objeto que representa las credenciales utilizadas para firmar digitalmente el documento PDF. Cree un `Credential` objeto con su constructor y especifique el alias asignando un valor a la `Credential` propiedad `alias` del objeto.
   * Un `HashAlgorithm` objeto que especifica un miembro de datos estático que representa el algoritmo hash que se va a utilizar para compender el documento PDF. Por ejemplo, puede especificar `HashAlgorithm.SHA1` el uso del algoritmo SHA1.
   * Un valor booleano que especifica si se utiliza el algoritmo hash.
   * Un valor de cadena que representa el motivo por el que el documento PDF se firmó digitalmente.
   * Un valor de cadena que representa la ubicación del firmante.
   * Un valor de cadena que representa la información de contacto del firmante.
   * Un `PDFSignatureAppearanceOptions` objeto que controla el aspecto de la firma digital. Por ejemplo, puede utilizar este objeto para agregar un logotipo personalizado a una firma digital.
   * Un `System.Boolean` objeto que especifica si se va a realizar la comprobación de revocación en el certificado del firmante. Si esta comprobación de revocación se realiza, se incrusta en la firma. El valor predeterminado es `false`.
   * Un `OCSPOptionSpec` objeto que almacena las preferencias para la compatibilidad con el protocolo de estado de certificado en línea (OCSP). Si no se realiza la comprobación de revocación, este parámetro no se utiliza y puede especificar `null`. Para obtener más información sobre este objeto, consulte [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Un `CRLPreferences` objeto que almacena las preferencias de la lista de revocación de certificados (CRL). Si no se realiza la comprobación de revocación, este parámetro no se utiliza y puede especificar `null`.
   * Objeto `TSPPreferences` que almacena las preferencias de compatibilidad con el proveedor de marca de hora (TSP). Este parámetro es opcional y puede ser `null`.
   El `sign` método devuelve un `BLOB` objeto que representa el documento PDF firmado.

1. Guardar el documento PDF firmado

   * Cree un `System.IO.FileStream` objeto invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF firmado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto devuelto por el `sign` método. Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el `System.IO.BinaryWriter` método `Write` del objeto y pasando la matriz de bytes.

**Consulte también**

[Firma digital de documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Firma digital de formularios interactivos {#digitally-signing-interactive-forms}

Puede firmar un formulario interactivo que cree el servicio Forms. Por ejemplo, considere el siguiente flujo de trabajo:

* Se combina un formulario PDF basado en XFA creado mediante Designer y datos de formulario ubicados en un documento XML mediante el servicio Forms. El servidor de Forms procesa un formulario interactivo.
* Puede firmar el formulario interactivo mediante la API de servicio de firma.

El resultado es un formulario PDF interactivo con firma digital. Al firmar un formulario PDF basado en un formulario XFA, asegúrese de guardar el archivo PDF como un formulario PDF estático de Adobe. Si intenta firmar un formulario PDF guardado como un formulario PDF dinámico de Adobe, se producirá una excepción. Dado que va a firmar el formulario que se devuelve desde el servicio Forms, asegúrese de que el formulario contiene un campo de firma.

>[!NOTE]
>
>Para poder firmar digitalmente un formulario interactivo, debe asegurarse de agregar el certificado a AEM Forms. Se agrega un certificado mediante la consola de administración o mediante programación mediante la API del administrador de confianza. (Consulte [Importación de credenciales mediante la API](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)del administrador de confianza).

Al utilizar la API de Forms Service, establezca la opción de tiempo de `GenerateServerAppearance` ejecución en `true`. Esta opción en tiempo de ejecución garantiza que el aspecto del formulario generado en el servidor siga siendo válido cuando se abre en Acrobat o Adobe Reader. Se recomienda definir esta opción en tiempo de ejecución al generar un formulario interactivo para firmar mediante la API de Forms.

>[!NOTE]
>
>Antes de leer Formularios interactivos de firma digital, se recomienda que esté familiarizado con la firma de documentos PDF. (Consulte Firma [digital de documentos](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)PDF).

### Resumen de los pasos {#summary_of_steps-4}

Para firmar digitalmente un formulario interactivo que devuelve el servicio Forms, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Crear un cliente de Forms y Signatures.
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
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)de biblioteca Java de AEM Forms.

**Creación de un cliente de formularios y firmas**

Dado que este flujo de trabajo invoca los servicios Forms y Signature, cree un cliente de servicio Forms y un cliente de servicio Signature.

**Obtener el formulario interactivo mediante el servicio Forms**

Puede utilizar el servicio Forms para obtener el formulario PDF interactivo que desea firmar. Desde AEM Forms, puede pasar un `com.adobe.idp.Document` objeto al servicio Forms que contenga el formulario que se va a procesar. El nombre de este método es `renderPDFForm2`. Este método devuelve un `com.adobe.idp.Document` objeto que contiene el formulario que se va a firmar. Puede pasar esta `com.adobe.idp.Document` instancia al servicio Signature.

Del mismo modo, si utiliza servicios Web, puede pasar la `BLOB` instancia que el servicio Forms devuelve al servicio Signature.

>[!NOTE]
>
>El inicio rápido asociado con la sección Formularios interactivos de firma digital invoca el `renderPDFForm2` método .

**Firmar el formulario interactivo**

Al firmar un documento PDF, puede definir las opciones en tiempo de ejecución que utiliza el servicio Signature. Puede definir las siguientes opciones:

* Opciones de aspecto
* Comprobación de revocación
* Valores de marca de hora

Las opciones de apariencia se definen mediante un `PDFSignatureAppearanceOptionSpec` objeto. Por ejemplo, puede mostrar la fecha dentro de una firma invocando el `PDFSignatureAppearanceOptionSpec` método `setShowDate` del objeto y pasando `true`.

**Guardar el documento PDF firmado**

Una vez que el servicio de firma firme digitalmente el documento PDF, puede guardarlo como archivo PDF. El archivo PDF se puede abrir en Acrobat o Adobe Reader.

**Consulte también**

[Firma digital de un formulario interactivo mediante la API de Java](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[Firma digital de un formulario interactivo mediante la API de servicio web](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Firma digital de documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Representación de formularios PDF interactivos](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### Firma digital de un formulario interactivo mediante la API de Java {#digitally-sign-an-interactive-form-using-the-java-api}

Firmar digitalmente un formulario interactivo mediante la API de formularios y firmas (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar y adobe-forms-client.jar, en la ruta de clases del proyecto Java.

1. Creación de un cliente de formularios y firmas

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `SignatureServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.
   * Cree un `FormsServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtener el formulario interactivo mediante el servicio Forms

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF para pasarlo al servicio Forms mediante su constructor. Pase un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.
   * Cree un `java.io.FileInputStream` objeto que represente el documento XML que contiene datos de formulario para pasarlos al servicio Forms mediante su constructor. Pase un valor de cadena que especifique la ubicación del archivo XML.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.
   * Cree un `PDFFormRenderSpec` objeto que se utilice para definir las opciones de tiempo de ejecución. Invocar el `PDFFormRenderSpec` método del `setGenerateServerAppearance` objeto y pasarlo `true`.
   * Invoque el `FormsServiceClient` método del `renderPDFForm2` objeto y pase los valores siguientes:

      * Un `com.adobe.idp.Document` objeto que contiene el formulario PDF que se va a procesar.
      * Un `com.adobe.idp.Document` objeto que contiene datos para combinar con el formulario.
      * Un `PDFFormRenderSpec` objeto que almacena opciones de tiempo de ejecución.
      * Un `URLSpec` objeto que contiene valores de URI necesarios para el servicio Forms. Puede especificar `null` para este valor de parámetro.
      * Un `java.util.HashMap` objeto que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
      El `renderPDFForm2` método devuelve un `FormsResult` objeto que contiene una secuencia de datos de formulario

   * Recupere el formulario PDF invocando el `FormsResult` método `getOutputContent` del objeto. Este método devuelve un `com.adobe.idp.Document` objeto que representa el formulario interactivo.


1. Firmar el formulario interactivo

   Firme el documento PDF invocando el `SignatureServiceClient` método `sign` del objeto y pasando los siguientes valores:

   * Un `com.adobe.idp.Document` objeto que representa el documento PDF que se va a firmar. Asegúrese de que este objeto es el `com.adobe.idp.Document` objeto obtenido del servicio Forms.
   * Un valor de cadena que representa el nombre del campo de firma que se firma.
   * Un `Credential` objeto que representa las credenciales utilizadas para firmar digitalmente el documento PDF. Cree un `Credential` objeto invocando el `Credential` método estático `getInstance` del objeto. Pase un valor de cadena que especifique el valor de alias que corresponde a la credencial de seguridad.
   * Un `HashAlgorithm` objeto que especifica un miembro de datos estático que representa el algoritmo hash que se va a utilizar para compender el documento PDF. Por ejemplo, puede especificar `HashAlgorithm.SHA1` el uso del algoritmo SHA1.
   * Un valor de cadena que representa el motivo por el que el documento PDF se firmó digitalmente.
   * Un valor de cadena que representa la información de contacto del firmante.
   * Un `PDFSignatureAppearanceOptions` objeto que controla el aspecto de la firma digital. Por ejemplo, puede utilizar este objeto para agregar un logotipo personalizado a una firma digital.
   * Un `java.lang.Boolean` objeto que especifica si se va a realizar la comprobación de revocación en el certificado del firmante.
   * Un `OCSPPreferences` objeto que almacena las preferencias para la compatibilidad con el protocolo de estado de certificado en línea (OCSP). Si no se realiza la comprobación de revocación, este parámetro no se utiliza y puede especificar `null`.
   * Un `CRLPreferences` objeto que almacena las preferencias de la lista de revocación de certificados (CRL). Si no se realiza la comprobación de revocación, este parámetro no se utiliza y puede especificar `null`.
   * Objeto `TSPPreferences` que almacena las preferencias de compatibilidad con el proveedor de marca de hora (TSP). Este parámetro es opcional y puede ser `null`.
   El `sign` método devuelve un `com.adobe.idp.Document` objeto que representa el documento PDF firmado.

1. Guardar el documento PDF firmado

   * Cree un `java.io.File` objeto y asegúrese de que la extensión de nombre de archivo sea .pdf.
   * Invoque el `com.adobe.idp.Document` método del `copyToFile` objeto y pase `java.io.File`para copiar el contenido del `Document` objeto en el archivo. Asegúrese de utilizar el `com.adobe.idp.Document` objeto que devolvió el `sign` método.

**Consulte también**

[Firma digital de formularios interactivos](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Inicio rápido (modo SOAP): Firma digital de un documento PDF mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Firma digital de un formulario interactivo mediante la API de servicio web {#digitally-sign-an-interactive-form-using-the-web-service-api}

Firmar digitalmente un formulario interactivo mediante la API de Forms y Signature (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Dado que esta aplicación cliente invoca dos servicios de AEM Forms, cree dos referencias de servicio. Utilice la siguiente definición WSDL para la referencia de servicio asociada con el servicio Signature: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   Utilice la siguiente definición WSDL para la referencia de servicio asociada al servicio Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Debido a que el tipo de datos es común a ambas referencias de servicio, califique completamente el tipo de datos `BLOB` `BLOB` cuando lo utilice. En el inicio rápido correspondiente del servicio Web, todas `BLOB` las instancias están completamente cualificadas.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Creación de un cliente de formularios y firmas

   * Cree un `SignatureServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `SignatureServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `SignatureServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.
   >[!NOTE]
   >
   >Repita estos pasos para el cliente del servicio Forms.

1. Obtener el formulario interactivo mediante el servicio Forms

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar un documento PDF firmado.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF que se va a firmar, así como el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` propiedad al contenido de la matriz de bytes.
   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar datos de formulario.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo XML que contiene los datos del formulario y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` propiedad al contenido de la matriz de bytes.
   * Cree un `PDFFormRenderSpec` objeto que se utilice para definir las opciones de tiempo de ejecución. Asigne el valor `true` al `PDFFormRenderSpec` campo del `generateServerAppearance` objeto.
   * Invoque el `FormsServiceClient` método del `renderPDFForm2` objeto y pase los valores siguientes:

      * Un `BLOB` objeto que contiene el formulario PDF que se va a procesar.
      * Un `BLOB` objeto que contiene datos para combinar con el formulario.
      * Un `PDFFormRenderSpec` objeto que almacena opciones de tiempo de ejecución.
      * Un `URLSpec` objeto que contiene valores de URI necesarios para el servicio Forms. Puede especificar `null` para este valor de parámetro.
      * Un `java.util.HashMap` objeto que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
      * Parámetro de salida largo utilizado para almacenar el número de páginas del formulario.
      * Parámetro de salida de cadena que se utiliza para el valor de configuración regional.
      * Un `FormResult` valor que es un parámetro de salida que se utiliza para almacenar el formulario interactivo.
   * Recupere el formulario PDF invocando el `FormsResult` campo del `outputContent` objeto. Este campo almacena un `BLOB` objeto que representa el formulario interactivo.


1. Firmar el formulario interactivo

   Firme el documento PDF invocando el `SignatureServiceClient` método `sign` del objeto y pasando los siguientes valores:

   * Un `BLOB` objeto que representa el documento PDF que se va a firmar. Utilice la `BLOB` instancia devuelta por el servicio Forms.
   * Un valor de cadena que representa el nombre del campo de firma que se firma.
   * Un `Credential` objeto que representa las credenciales utilizadas para firmar digitalmente el documento PDF. Cree un `Credential` objeto con su constructor y especifique el alias asignando un valor a la `Credential` propiedad `alias` del objeto.
   * Un `HashAlgorithm` objeto que especifica un miembro de datos estático que representa el algoritmo hash que se va a utilizar para compender el documento PDF. Por ejemplo, puede especificar `HashAlgorithm.SHA1` el uso del algoritmo SHA1.
   * Un valor booleano que especifica si se utiliza el algoritmo hash.
   * Un valor de cadena que representa el motivo por el que el documento PDF se firmó digitalmente.
   * Un valor de cadena que representa la ubicación del firmante.
   * Un valor de cadena que representa la información de contacto del firmante.
   * Un `PDFSignatureAppearanceOptions` objeto que controla el aspecto de la firma digital. Por ejemplo, puede utilizar este objeto para agregar un logotipo personalizado a una firma digital.
   * Un `System.Boolean` objeto que especifica si se va a realizar la comprobación de revocación en el certificado del firmante. Si esta comprobación de revocación se realiza, se incrusta en la firma. El valor predeterminado es `false`.
   * Un `OCSPPreferences` objeto que almacena las preferencias para la compatibilidad con el protocolo de estado de certificado en línea (OCSP). Si no se realiza la comprobación de revocación, este parámetro no se utiliza y puede especificar `null`. Para obtener más información sobre este objeto, consulte [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Un `CRLPreferences` objeto que almacena las preferencias de la lista de revocación de certificados (CRL). Si no se realiza la comprobación de revocación, este parámetro no se utiliza y puede especificar `null`.
   * Objeto `TSPPreferences` que almacena las preferencias de compatibilidad con el proveedor de marca de hora (TSP). Este parámetro es opcional y puede ser `null`.
   El `sign` método devuelve un `BLOB` objeto que representa el documento PDF firmado.

1. Guardar el documento PDF firmado

   * Cree un `System.IO.FileStream` objeto invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF firmado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto devuelto por el `sign` método. Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el `System.IO.BinaryWriter` método `Write` del objeto y pasando la matriz de bytes.

**Consulte también**

[Firma digital de formularios interactivos](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Certificación de documentos PDF {#certifying-pdf-documents}

Puede asegurar un documento PDF certificándolo con un tipo particular de firma denominada firma certificada. Una firma certificada se distingue de una firma digital de las siguientes formas:

* Debe ser la primera firma aplicada al documento PDF; es decir, en el momento en que se aplica la firma certificada, cualquier otro campo de firma del documento debe estar sin firmar. Solo se permite una firma certificada en un documento PDF. Si desea firmar y certificar un documento PDF, debe certificarlo antes de firmarlo. Después de certificar un documento PDF, puede firmar digitalmente campos de firma adicionales.
* El autor o creador del documento puede especificar que el documento se puede modificar de determinadas formas sin invalidar la firma certificada. Por ejemplo, el documento puede permitir rellenar formularios o comentarios. Si el autor especifica que no se permite una modificación determinada, Acrobat impide que los usuarios modifiquen el documento de esa manera. Si se realizan dichas modificaciones, como por ejemplo utilizando otra aplicación, la firma certificada no es válida y Acrobat emite una advertencia cuando un usuario abre el documento. (Con las firmas no certificadas, no se evitan las modificaciones y las operaciones de edición normales no invalidan la firma original).
* En el momento de la firma, el documento se analiza para detectar tipos específicos de contenido que podrían hacer que el contenido de un documento fuera ambiguo o engañoso. Por ejemplo, una anotación podría oscurecer algún texto de una página que sea importante para comprender lo que se está certificando. Se puede proporcionar una explicación (autenticación legal) sobre dicho contenido.

Puede certificar documentos PDF mediante programación mediante la API de Java del servicio de firmas o la API del servicio web de firmas. Al certificar un documento PDF, debe hacer referencia a una credencial de seguridad que exista en el servicio de credenciales. Para obtener información sobre las credenciales de seguridad, consulte la guía *Instalación e implementación de AEM Forms* para el servidor de aplicaciones.

>[!NOTE]
>
>Al certificar y firmar el mismo documento PDF, si la firma del certificado no es de confianza, aparece un triángulo amarillo junto a la primera firma de firma al abrir el documento PDF en Acrobat o Adobe Reader. Debe confiarse en la firma certificadora para evitar esta situación.

>[!NOTE]
>
>Cuando se utiliza una credencial Cipher nShield HSM para firmar o certificar un documento PDF, no se puede utilizar la nueva credencial hasta que se reinicie el servidor de aplicaciones J2EE en el que se implementa AEM Forms. Sin embargo, puede establecer un valor de configuración, lo que resulta en que la operación de firma o certificación funcione sin reiniciar el servidor de aplicaciones J2EE.

Puede agregar el siguiente valor de configuración en el archivo cknfastrc, que se encuentra en /opt/nfast/cknfastrc (o c:\nfast\cknfastrc):

```as3
             CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Después de agregar este valor de configuración al archivo cknfastrc, la nueva credencial se puede utilizar sin reiniciar el servidor de aplicaciones J2EE.

>[!NOTE]
>
>Para obtener más información sobre el servicio Signature y la certificación de un documento, consulte [Servicios de referencia para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-5}

Para certificar un documento PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de firma.
1. Obtenga el documento PDF que certificar.
1. Certifique el documento PDF.
1. Guarde el documento PDF certificado como archivo PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)de biblioteca Java de AEM Forms.

**Crear un cliente de firma**

Para poder realizar una operación de firma mediante programación, debe crear un cliente de firma.

**Obtener el documento PDF para certificar**

Para certificar un documento PDF, debe obtener un documento PDF que contenga un campo de firma. Si un documento PDF no contiene un campo de firma, no se puede certificar. Se puede agregar un campo de firma mediante Designer o mediante programación. Para obtener información sobre cómo agregar un campo de firma mediante programación, consulte [Adición de campos](digitally-signing-certifying-documents.md#adding-signature-fields)de firma.

**Certificar el documento PDF**

Para certificar correctamente un documento PDF, necesita los siguientes valores de entrada que utiliza el servicio Signature para certificar un documento PDF:

* **Documento** PDF: Documento PDF que contiene un campo de firma, que es un campo de formulario que contiene una representación gráfica de la firma certificada. Un documento PDF debe contener un campo de firma para poder certificarlo. Se puede agregar un campo de firma mediante Designer o mediante programación. (Consulte [Adición de campos](digitally-signing-certifying-documents.md#adding-signature-fields)de firma).
* **Nombre** del campo de firma: Nombre completo del campo de firma que está certificado. El siguiente valor es un ejemplo: `form1[0].#subform[1].SignatureField3[3]`. Al utilizar un campo de formulario XFA, también se puede utilizar el nombre parcial del campo de firma: `SignatureField3[3]`. Si se pasa un valor nulo para el nombre del campo, se crea y certifica dinámicamente un campo de firma invisible.
* **Credenciales** de seguridad: Una credencial que se utiliza para certificar el documento PDF. Esta credencial de seguridad contiene una contraseña y un alias, que deben coincidir con un alias que aparece en la credencial que se encuentra dentro del servicio de credenciales. El alias es una referencia a una credencial real que puede estar en un archivo PKCS#12 (con la extensión .pfx) o en un módulo de seguridad de hardware (HSM).
* **Algoritmo** hash: Algoritmo hash que se usará para compender el documento PDF.
* **Motivo de la firma**: Valor que se muestra en Acrobat o Adobe Reader para que otros usuarios sepan el motivo por el que se certificó el documento PDF.
* **Ubicación del firmante**: Ubicación del firmante especificada por la credencial.
* **Información** de contacto: Información de contacto, como la dirección y el número de teléfono, del firmante.
* **Información** de permisos: Permisos que controlan las acciones que un usuario final puede realizar en un documento sin que la firma certificada no sea válida. Por ejemplo, puede establecer el permiso para que cualquier cambio en el documento PDF haga que la firma certificada no sea válida.
* **Explicación** legal: Cuando se certifica un documento, éste se analiza automáticamente en busca de tipos específicos de contenido que puedan hacer que el contenido de un documento sea ambiguo o engañoso. Por ejemplo, una anotación podría oscurecer algún texto de una página que sea importante para comprender lo que se está certificando. El proceso de análisis genera advertencias sobre estos tipos de contenido. Este valor proporciona una explicación adicional del contenido que puede haber generado advertencias.
* **Opciones** de aspecto: Opciones que controlan el aspecto de la firma certificada. Por ejemplo, la firma certificada puede mostrar información de fecha.
* **Comprobación** de revocación: Este valor especifica si la comprobación de revocación se realiza para el certificado del firmante. La configuración predeterminada de `false` significa que no se ha realizado la comprobación de revocación.
* **Configuración** de OCSP: Configuración de la compatibilidad con el protocolo de estado de certificado en línea (OCSP), que proporciona información sobre el estado de la credencial que se utiliza para certificar el documento PDF. Por ejemplo, puede especificar la dirección URL del servidor que proporciona información sobre las credenciales que utiliza para iniciar sesión en el documento PDF.
* **Configuración** de CRL: Configuración de las preferencias de la lista de revocación de certificados (CRL) si se ha realizado la comprobación de revocación. Por ejemplo, puede especificar que siempre se compruebe si se revocó una credencial.
* **Marca de hora**: Configuración que define la información de marca de hora que se aplica a la firma certificada. Una marca de hora indica que se establecieron datos específicos antes de un determinado momento. Este conocimiento ayuda a construir una relación de confianza entre el firmante y el verificador.

**Guardar el documento PDF certificado como archivo PDF**

Una vez que el servicio de firma certifique el documento PDF, puede guardarlo como archivo PDF para que los usuarios puedan abrirlo en Acrobat o Adobe Reader.

**Consulte también**

[Certificar documentos PDF mediante la API de Java](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[Certificar documentos PDF mediante la API de servicio web](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adición de campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields)

### Certificar documentos PDF mediante la API de Java {#certify-pdf-documents-using-the-java-api}

Certifique un documento PDF mediante la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente de firma

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `SignatureServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtener el documento PDF para certificar

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF que se va a certificar mediante su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Certificar el documento PDF

   Certifique el documento PDF invocando el `SignatureServiceClient` método del `certify` objeto y pasando los siguientes valores:

   * El `com.adobe.idp.Document` objeto que representa el documento PDF que se va a certificar.
   * Un valor de cadena que representa el nombre del campo de firma que contendrá la firma.
   * Un `Credential` objeto que representa la credencial que se utiliza para certificar el documento PDF. Cree un `Credential` objeto invocando el método estático del `Credential` objeto y pasando un `getInstance` valor de cadena que especifica el valor de alias que corresponde a la credencial de seguridad.
   * Un `HashAlgorithm` objeto que especifica un miembro de datos estático que representa el algoritmo hash utilizado para compender el documento PDF. Por ejemplo, puede especificar `HashAlgorithm.SHA1` el uso del algoritmo SHA1.
   * Un valor de cadena que representa el motivo por el que se certificó el documento PDF.
   * Un valor de cadena que representa la información de contacto del firmante.
   * Un `MDPPermissions` objeto que especifica las acciones que se pueden realizar en el documento PDF que invalidan la firma.
   * Un `PDFSignatureAppearanceOptions` objeto que controla el aspecto de la firma certificada. Si lo desea, modifique el aspecto de la firma invocando un método como, por ejemplo, `setShowDate`.
   * Un valor de cadena que proporciona una explicación de las acciones que invalidan la firma.
   * Un `java.lang.Boolean` objeto que especifica si se va a realizar la comprobación de revocación en el certificado del firmante. Si esta comprobación de revocación se realiza, se incrusta en la firma. El valor predeterminado es `false`.
   * Un `java.lang.Boolean` objeto que especifica si el campo de firma que se está certificando está bloqueado. Si el campo está bloqueado, el campo de firma se marca como de solo lectura, sus propiedades no se pueden modificar y nadie que no tenga los permisos necesarios no puede borrarlo. El valor predeterminado es `false`.
   * Un `OCSPPreferences` objeto que almacena las preferencias para la compatibilidad con el protocolo de estado de certificado en línea (OCSP). Si no se realiza la comprobación de revocación, este parámetro no se utiliza y puede especificar `null`. Para obtener más información sobre este objeto, consulte [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Un `CRLPreferences` objeto que almacena las preferencias de la lista de revocación de certificados (CRL). Si no se realiza la comprobación de revocación, este parámetro no se utiliza y puede especificar `null`.
   * Objeto `TSPPreferences` que almacena las preferencias de compatibilidad con el proveedor de marca de hora (TSP). Por ejemplo, después de crear un `TSPPreferences` objeto, puede establecer la dirección URL del servidor TSP invocando el `TSPPreferences` método del `setTspServerURL` objeto. Este parámetro es opcional y puede ser `null`. Para obtener más información, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).
   El `certify` método devuelve un `com.adobe.idp.Document` objeto que representa el documento PDF certificado.

1. Guardar el documento PDF certificado como archivo PDF

   * Cree un `java.io.File` objeto y asegúrese de que la extensión del archivo sea .pdf.
   * Invocar el `com.adobe.idp.Document` método del `copyToFile` objeto para copiar el contenido del `com.adobe.idp.Document` objeto en el archivo.

**Consulte también**

[Certificación de documentos PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Inicio rápido (modo SOAP): Certificación de un documento PDF mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Certificar documentos PDF mediante la API de servicio web {#certify-pdf-documents-using-the-web-service-api}

Certifique un documento PDF mediante la API de firma (servicio Web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Crear un cliente de firma

   * Cree un `SignatureServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `SignatureServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `SignatureServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtener el documento PDF para certificar

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar un documento PDF certificado.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF que se va a certificar y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando a su miembro `MTOM` de datos el contenido de la matriz de bytes.

1. Certificar el documento PDF

   Certifique el documento PDF invocando el `SignatureServiceClient` método del `certify` objeto y pasando los siguientes valores:

   * El `BLOB` objeto que representa el documento PDF que se va a certificar.
   * Un valor de cadena que representa el nombre del campo de firma que contendrá la firma.
   * Un `Credential` objeto que representa la credencial que se utiliza para certificar el documento PDF. Cree un `Credential` objeto con su constructor y especifique el alias asignando un valor a la `Credential` propiedad del `alias` objeto.
   * Un `HashAlgorithm` objeto que especifica un miembro de datos estático que representa el algoritmo hash utilizado para compender el documento PDF. Por ejemplo, puede especificar `HashAlgorithm.SHA1` el uso del algoritmo SHA1.
   * Un valor booleano que especifica si se utiliza el algoritmo hash.
   * Un valor de cadena que representa el motivo por el que se certificó el documento PDF.
   * Un valor de cadena que representa la ubicación del firmante.
   * Un valor de cadena que representa la información de contacto del firmante.
   * Miembro de datos estático de un `MDPPermissions` objeto que especifica las acciones que se pueden realizar en el documento PDF que invalidan la firma.
   * Un valor booleano que especifica si se debe utilizar el `MDPPermissions` objeto que se pasó como el valor del parámetro anterior.
   * Un valor de cadena que explica qué acciones invalidan la firma.
   * Un `PDFSignatureAppearanceOptions` objeto que controla el aspecto de la firma certificada. Cree un `PDFSignatureAppearanceOptions` objeto con su constructor. Puede modificar el aspecto de la firma estableciendo uno de sus miembros de datos.
   * Un `System.Boolean` objeto que especifica si se va a realizar la comprobación de revocación en el certificado del firmante. Si esta comprobación de revocación se realiza, se incrusta en la firma. El valor predeterminado es `false`.
   * Un `System.Boolean` objeto que especifica si el campo de firma que se está certificando está bloqueado. Si el campo está bloqueado, el campo de firma se marca como de solo lectura, sus propiedades no se pueden modificar y nadie que no tenga los permisos necesarios no puede borrarlo. El valor predeterminado es `false`.
   * Un `System.Boolean` objeto que especifica si el campo de firma está bloqueado. Es decir, si pasa `true` al parámetro anterior, pase `true` a este parámetro.
   * Un `OCSPPreferences` objeto que almacena las preferencias para la compatibilidad con el protocolo de estado de certificado en línea (OCSP), que proporciona información sobre el estado de la credencial que se utiliza para certificar el documento PDF. Si no se realiza la comprobación de revocación, este parámetro no se utiliza y puede especificar `null`.
   * Un `CRLPreferences` objeto que almacena las preferencias de la lista de revocación de certificados (CRL). Si no se realiza la comprobación de revocación, este parámetro no se utiliza y puede especificar `null`.
   * Objeto `TSPPreferences` que almacena las preferencias de compatibilidad con el proveedor de marca de hora (TSP). Por ejemplo, después de crear un `TSPPreferences` objeto, puede establecer la dirección URL del TSP estableciendo el miembro de datos del `TSPPreferences` objeto `tspServerURL` . Este parámetro es opcional y puede ser `null`.
   El `certify` método devuelve un `BLOB` objeto que representa el documento PDF certificado.

1. Guardar el documento PDF certificado como archivo PDF

   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF que contendrá el documento PDF certificado y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto devuelto por el `certify` método. Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `binaryData` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el `System.IO.BinaryWriter` método `Write` del objeto y pasando la matriz de bytes.

**Consulte también**

[Certificación de documentos PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verificación de firmas digitales {#verifying-digital-signatures}

Las firmas digitales se pueden comprobar para garantizar que un documento PDF firmado no se haya modificado y que la firma digital sea válida. Al verificar una firma digital, puede comprobar el estado de la firma y las propiedades de la firma, como la identidad del firmante. Antes de confiar en una firma digital, se recomienda verificarla. Al verificar una firma digital, haga referencia a un documento PDF que contenga una firma digital.

Supongamos que se desconoce la identidad del firmante. Al abrir el documento PDF en Acrobat, aparece un mensaje de advertencia que indica que la identidad del firmante es desconocida, como se muestra en la siguiente ilustración.

![vd_vd_verifysig](assets/vd_vd_verifysig.png)

Del mismo modo, cuando se verifica mediante programación una firma digital, se puede determinar el estado de la identidad del firmante. Por ejemplo, si comprueba la firma digital en el documento mostrado en la ilustración anterior, el resultado sería que la identidad del firmante es desconocida.

>[!NOTE]
>
>Para obtener más información sobre el servicio Signature y la verificación de firmas digitales, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-6}

Para verificar una firma digital, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de firma.
1. Obtenga el documento PDF que contiene la firma para verificarlo.
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
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)de biblioteca Java de AEM Forms.

**Crear un cliente de firma**

Antes de realizar una operación de servicio de firma mediante programación, cree un cliente de servicio de firma.

**Obtener el documento PDF que contiene la firma para verificar**

Para verificar una firma utilizada para firmar digitalmente o certificar un documento PDF, obtenga un documento PDF que contenga una firma.

**Definición de las opciones de tiempo de ejecución de PKI**

Defina estas opciones de tiempo de ejecución PKI que utiliza el servicio Signature al comprobar firmas en un documento PDF:

* Hora de verificación
* Comprobación de revocación
* Valores de marca de hora

Como parte de la configuración de estas opciones, puede especificar el tiempo de verificación. Por ejemplo, puede seleccionar la hora actual (la hora en el equipo del validador), que indica el uso de la hora actual. Para obtener información sobre los diferentes valores de tiempo, consulte el valor de `VerificationTime` enumeración en Referencia [de API de formularios](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM.

También puede especificar si desea realizar la comprobación de revocación como parte del proceso de verificación. Por ejemplo, puede realizar una comprobación de revocación para determinar si el certificado está revocado. Para obtener información sobre las opciones de comprobación de revocación, consulte el valor de la `RevocationCheckStyle` enumeración en Referencia [de API de formularios](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM.

Para realizar la comprobación de revocación en un certificado, especifique una URL para un servidor de lista de revocación de certificados (CRL) mediante un `CRLOptionSpec` objeto. Sin embargo, si no especifica una URL para el servidor CRL, el servicio Signature obtendrá la URL del certificado.

En lugar de utilizar un servidor CRL, puede utilizar un servidor de protocolo de estado de certificado en línea (OCSP) al realizar la comprobación de revocación. Normalmente, cuando se utiliza un servidor OCSP en lugar de un servidor CRL, la comprobación de revocación se realiza más rápido. (Consulte Protocolo [de estado de certificado](https://tools.ietf.org/html/rfc2560)en línea).

Puede establecer el orden de los servidores CRL y OCSP que utiliza el servicio de firmas mediante las aplicaciones y los servicios de Adobe. Por ejemplo, si el servidor OCSP se establece primero en Aplicaciones y servicios de Adobe, se comprueba el servidor OCSP, seguido del servidor CRL.

Si no realiza la comprobación de revocación, el servicio Signature no comprueba si el certificado está revocado. Es decir, se ignora la información del servidor CRL y OCSP.

>[!NOTE]
>
>Puede anular la dirección URL especificada en el certificado mediante un objeto `CRLOptionSpec` y `OCSPOptionSpec` . Por ejemplo, para anular el servidor CRL, puede invocar el `CRLOptionSpec` método `setLocalURI` del objeto.

La marca de hora es el proceso de seguimiento de la hora en que se modificó un documento firmado o certificado. Después de firmar un documento, nadie puede modificarlo. La marca de hora ayuda a reforzar la validez de un documento firmado o certificado. Puede definir las opciones de marca de hora mediante un `TSPOptionSpec` objeto. Por ejemplo, puede especificar la dirección URL de un servidor de proveedor de marca de hora (TSP).

>[!NOTE]
>
>En el inicio rápido de Java y servicio Web, el tiempo de verificación se establece en `VerificationTime.CURRENT_TIME` y la comprobación de revocación se establece en `RevocationCheckStyle.BestEffort`. Dado que no se especifica ninguna CRL ni información de servidor OCSP, la información de servidor se obtiene del certificado.

**Verificar la firma digital**

Para verificar correctamente una firma, especifique el nombre completo del campo de firma que contiene la firma, como `form1[0].#subform[1].SignatureField3[3]`. Al utilizar un campo de formulario XFA, también puede utilizar el nombre parcial del campo de firma: `SignatureField3`.

De forma predeterminada, el servicio Signature limita la cantidad de tiempo que se puede firmar un documento después del tiempo de validación a 65 minutos. Si un usuario intenta comprobar una firma en este momento y la hora de firma es posterior a la hora actual y está a 65 minutos, el servicio Signature no crea un error de verificación.

>[!NOTE]
>
>Para conocer otros valores que se requieren al comprobar una firma, consulte Referencia [de API de](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

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

### Verificación de firmas digitales mediante la API de Java {#verify-digital-signatures-using-the-java-api}

Verifique una firma digital mediante la API de servicio de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente de firma

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `SignatureServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtener el documento PDF que contiene la firma para verificar

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF que contiene la firma que se va a comprobar con su constructor. Pase un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Definición de las opciones de tiempo de ejecución de PKI

   * Cree un `PKIOptions` objeto con su constructor.
   * Establezca el tiempo de verificación invocando el `PKIOptions` método `setVerificationTime` del objeto y pasando un valor de `VerificationTime` enumeración que especifica el tiempo de verificación.
   * Establezca la opción de comprobación de revocación invocando el `PKIOptions` método del `setRevocationCheckStyle` objeto y pasando un valor de `RevocationCheckStyle` enumeración que especifique si se va a realizar la comprobación de revocación.

1. Verificar la firma digital

   Compruebe la firma invocando el `SignatureServiceClient` método `verify2` del objeto y pasando los siguientes valores:

   * Un `com.adobe.idp.Document` objeto que contiene un documento PDF con firma digital o certificado.
   * Un valor de cadena que representa el nombre del campo de firma que contiene la firma que se va a comprobar.
   * Un `PKIOptions` objeto que contiene opciones de tiempo de ejecución PKI.
   * Una `VerifySPIOptions` instancia que contiene información de SPI. Puede especificar `null` para este parámetro.
   El `verify2` método devuelve un `PDFSignatureVerificationInfo` objeto que contiene información que se puede utilizar para verificar la firma digital.

1. Determinar el estado de la firma

   * Determine el estado de la firma invocando el `PDFSignatureVerificationInfo` método del `getStatus` objeto. Este método devuelve un `SignatureStatus` objeto que especifica el estado de la firma. Por ejemplo, si no se modifica un documento PDF firmado, este método devuelve `SignatureStatus.DocumentSigNoChanges`.

1. Determinar la identidad del firmante

   * Determine la identidad del firmante invocando el `PDFSignatureVerificationInfo` método del `getSigner` objeto. Este método devuelve un `IdentityInformation` objeto.
   * Invocar el `IdentityInformation` método del `getStatus` objeto para determinar la identidad del firmante. Este método devuelve un valor de `IdentityStatus` enumeración que especifica la identidad. Por ejemplo, si el firmante es de confianza, este método devuelve `IdentityStatus.TRUSTED`.

**Consulte también**

[Verificación de firmas digitales](#verify-digital-signatures-using-the-java-api)

[Inicio rápido (modo SOAP): Verificación de una firma digital mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificar firmas digitales mediante la API de servicio web {#verify-digital-signatures-using-the-web-service-api}

Verifique una firma digital mediante la API de servicio de firma (servicio Web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Crear un cliente de firma

   * Cree un `SignatureServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `SignatureServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `SignatureServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtener el documento PDF que contiene la firma para verificar

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar un documento PDF que contiene una firma digital o certificada que se va a comprobar.
   * Cree un `System.IO.FileStream` objeto invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF firmado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el `BLOB` objeto asignando su `MTOM` propiedad al contenido de la matriz de bytes.

1. Definición de las opciones de tiempo de ejecución de PKI

   * Cree un `PKIOptions` objeto con su constructor.
   * Establezca el tiempo de verificación asignando al miembro de datos del `PKIOptions` objeto un valor de `verificationTime` `VerificationTime` enumeración que especifique el tiempo de verificación.
   * Establezca la opción de comprobación de revocación asignando al miembro de datos del `PKIOptions` objeto un valor de `revocationCheckStyle` `RevocationCheckStyle` enumeración que especifique si desea realizar la comprobación de revocación.

1. Verificar la firma digital

   Compruebe la firma invocando el `SignatureServiceClient` método `verify2` del objeto y pasando los siguientes valores:

   * El `BLOB` objeto que contiene un documento PDF con firma digital o certificado.
   * Un valor de cadena que representa el nombre del campo de firma que contiene la firma que se va a comprobar.
   * Un `PKIOptions` objeto que contiene opciones de tiempo de ejecución PKI.
   * Una `VerifySPIOptions` instancia que contiene información de SPI. Puede especificar `null` para este parámetro.
   El `verify2` método devuelve un `PDFSignatureVerificationInfo` objeto que contiene información que se puede utilizar para verificar la firma digital.

1. Determinar el estado de la firma

   Para determinar el estado de la firma, obtenga el valor del miembro de `PDFSignatureVerificationInfo` datos del `status` objeto. Este miembro de datos almacena un `SignatureStatus` objeto que especifica el estado de la firma. Por ejemplo, si se modifica un documento PDF firmado, el miembro de `status` datos almacena el valor `SignatureStatus.DocumentSigNoChanges`.

1. Determinar la identidad del firmante

   * Determine la identidad del firmante recuperando el valor del miembro de datos del `PDFSignatureVerificationInfo` objeto `signer` . Este miembro devuelve un `IdentityInformation` objeto.
   * Recupere el miembro de datos del `IdentityInformation` `status` objeto para determinar la identidad del firmante. Este miembro de datos devuelve un valor de `IdentityStatus` enumeración que especifica la identidad. Por ejemplo, si el firmante es de confianza, este miembro devuelve `IdentityStatus.TRUSTED`.

**Consulte también**

[Verificación de firmas digitales](#verify-digital-signatures-using-the-java-api)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verificación de varias firmas digitales {#verifying-multiple-digital-signatures}

AEM Forms proporciona los medios para comprobar todas las firmas digitales que se encuentran en un documento PDF. Supongamos que un documento PDF contiene varias firmas digitales como resultado de un proceso empresarial que requiere firmas de varios firmantes. Por ejemplo, considere una transacción financiera que requiere la firma de un responsable de préstamos y de un administrador. Puede utilizar la API de Java del servicio de firmas o la API del servicio web para comprobar todas las firmas del documento PDF. Al verificar varias firmas digitales, puede comprobar el estado y las propiedades de cada firma. Antes de confiar en una firma digital, se recomienda verificarla. Se recomienda que esté familiarizado con la verificación de una sola firma digital.

>[!NOTE]
>
>Para obtener más información sobre el servicio Signature y la verificación de firmas digitales, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)de biblioteca Java de AEM Forms.

**Crear un cliente de firma**

Antes de realizar una operación de servicio de firma mediante programación, cree un cliente de servicio de firma.

**Obtenga el documento PDF que contiene las firmas para verificar**

Para verificar una firma utilizada para firmar digitalmente o certificar un documento PDF, obtenga un documento PDF que contenga una firma.

**Definición de las opciones de tiempo de ejecución de PKI**

Defina estas opciones de tiempo de ejecución PKI que utiliza el servicio Signature al comprobar todas las firmas de un documento PDF:

* Hora de verificación
* Comprobación de revocación
* Valores de marca de hora

Como parte de la configuración de estas opciones, puede especificar el tiempo de verificación. Por ejemplo, puede seleccionar la hora actual (la hora en el equipo del validador), que indica el uso de la hora actual. Para obtener información sobre los diferentes valores de tiempo, consulte el valor de `VerificationTime` enumeración en Referencia [de API de formularios](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM.

También puede especificar si desea realizar la comprobación de revocación como parte del proceso de verificación. Por ejemplo, puede realizar una comprobación de revocación para determinar si el certificado está revocado. Para obtener información sobre las opciones de comprobación de revocación, consulte el valor de la `RevocationCheckStyle` enumeración en Referencia [de API de formularios](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM.

Para realizar la comprobación de revocación en un certificado, especifique una URL para un servidor de lista de revocación de certificados (CRL) mediante un `CRLOptionSpec` objeto. Sin embargo, si no especifica una URL para un servidor CRL, el servicio Signature obtendrá la URL del certificado.

En lugar de utilizar un servidor CRL, puede utilizar un servidor de protocolo de estado de certificado en línea (OCSP) al realizar la comprobación de revocación. Normalmente, cuando se utiliza un servidor OCSP en lugar de un servidor CRL, la comprobación de revocación se realiza más rápido. (Consulte Protocolo [de estado de certificado](https://tools.ietf.org/html/rfc2560)en línea).

Puede establecer el orden de los servidores CRL y OCSP que utiliza el servicio de firmas mediante las aplicaciones y los servicios de Adobe. Por ejemplo, si el servidor OCSP se establece primero en Aplicaciones y servicios de Adobe, se comprueba el servidor OCSP, seguido del servidor CRL.

Si no realiza la comprobación de revocación, el servicio Signature no comprueba si el certificado está revocado. Es decir, se ignora la información del servidor CRL y OCSP.

>[!NOTE]
>
>Puede anular la dirección URL especificada en el certificado mediante un objeto `CRLOptionSpec` y `OCSPOptionSpec` . Por ejemplo, para anular el servidor CRL, puede invocar el `CRLOptionSpec` método `setLocalURI` del objeto.

La marca de hora es el proceso de seguimiento de la hora en que se modificó un documento firmado o certificado. Después de firmar un documento, nadie puede modificarlo. La marca de hora ayuda a reforzar la validez de un documento firmado o certificado. Puede definir las opciones de marca de hora mediante un `TSPOptionSpec` objeto. Por ejemplo, puede especificar la dirección URL de un servidor de proveedor de marca de hora (TSP).

>[!NOTE]
>
>En el inicio rápido de Java y servicio Web, el tiempo de verificación se establece en `VerificationTime.CURRENT_TIME` y la comprobación de revocación se establece en `RevocationCheckStyle.BestEffort`. Dado que no se especifica ninguna CRL ni información de servidor OCSP, la información de servidor se obtiene del certificado.

**Recuperar todas las firmas digitales**

Para comprobar todas las firmas digitales que se encuentran en un documento PDF, recupere las firmas digitales del documento PDF. Todas las firmas se devuelven en una lista. Como parte de la verificación de una firma digital, compruebe el estado de la firma.

>[!NOTE]
>
>A diferencia de lo que sucede cuando se comprueba una sola firma digital, cuando se verifican varias firmas, no es necesario especificar el nombre del campo de firma.

**Repetir mediante todas las firmas**

Repita cada firma. Es decir, para cada firma, verifique la firma digital y la identidad del firmante y el estado de cada firma. (Consulte [Verificación de firmas](#verify-digital-signatures-using-the-java-api)digitales).

>[!NOTE]
>
>No es necesario repetir todas las firmas si el requisito es todo el documento.

**Consulte también**

[Verificación de varias firmas digitales mediante la API de Java](#verify-digital-signatures-using-the-java-api)

[Verificación de varias firmas digitales mediante la API de servicio web](#verify-digital-signatures-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificación de varias firmas digitales mediante la API de Java {#verify-multiple-digital-signatures-using-the-java-api}

Compruebe varias firmas digitales mediante la API de servicio de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar, en la ruta de clases del proyecto Java.

1. Crear un cliente de firma

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `SignatureServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtenga el documento PDF que contiene las firmas para verificar

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF que contiene varias firmas digitales para verificarlo con su constructor. Pase un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Definición de las opciones de tiempo de ejecución de PKI

   * Cree un `PKIOptions` objeto con su constructor.
   * Establezca el tiempo de verificación invocando el `PKIOptions` método `setVerificationTime` del objeto y pasando un valor de `VerificationTime` enumeración que especifica el tiempo de verificación.
   * Establezca la opción de comprobación de revocación invocando el método del `PKIOptions` objeto y pasando un valor de `setRevocationCheckStyle` `RevocationCheckStyle` enumeración que especifique si se va a realizar la comprobación de revocación.

1. Recuperar todas las firmas digitales

   Invoque el `SignatureServiceClient` método del `verifyPDFDocument` objeto y pase los valores siguientes:

   * Un `com.adobe.idp.Document` objeto que contiene un documento PDF que contiene varias firmas digitales.
   * Un `PKIOptions` objeto que contiene opciones de tiempo de ejecución PKI.
   * Una `VerifySPIOptions` instancia que contiene información de SPI. Puede especificar `null` para este parámetro.
   El `verifyPDFDocument` método devuelve un `PDFDocumentVerificationInfo` objeto que contiene información sobre todas las firmas digitales del documento PDF.

1. Repetir mediante todas las firmas

   * Repita todas las firmas invocando el `PDFDocumentVerificationInfo` método `getVerificationInfos` del objeto. Este método devuelve un `java.util.List` objeto en el que cada elemento es un `PDFSignatureVerificationInfo` objeto. Utilice un `java.util.Iterator` objeto para iterar por la lista de firmas.
   * Con el `PDFSignatureVerificationInfo` objeto, puede realizar tareas como determinar el estado de la firma invocando el `PDFSignatureVerificationInfo` método del `getStatus` objeto. Este método devuelve un `SignatureStatus` objeto cuyo miembro de datos estáticos le informa sobre el estado de la firma. Por ejemplo, si la firma es desconocida, este método devuelve `SignatureStatus.DocumentSignatureUnknown`.

**Consulte también**

[Verificación de varias firmas digitales](#verifying-multiple-digital-signatures)

[Inicio rápido (modo SOAP): Verificación de varias firmas digitales mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Verificación de firmas digitales](#verify-digital-signatures-using-the-java-api)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificación de varias firmas digitales mediante la API de servicio web {#verifying-multiple-digital-signatures-using-the-web-service-api}

Compruebe varias firmas digitales mediante la API de servicio de firma (servicio Web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Crear un cliente de firma

   * Cree un `SignatureServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `SignatureServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `SignatureServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento PDF que contiene las firmas para verificar

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto almacena un documento PDF que contiene varias firmas digitales para verificar.
   * Cree un `System.IO.FileStream` objeto invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el `BLOB` objeto asignando su `MTOM` propiedad al contenido de la matriz de bytes.

1. Definición de las opciones de tiempo de ejecución de PKI

   * Cree un `PKIOptions` objeto con su constructor.
   * Establezca el tiempo de verificación asignando al miembro de datos del `PKIOptions` objeto un valor de `verificationTime` `VerificationTime` enumeración que especifique el tiempo de verificación.
   * Defina la opción de comprobación de revocación asignando al miembro de datos del `PKIOptions` objeto un valor de `revocationCheckStyle` `RevocationCheckStyle` enumeración que especifique si desea realizar la comprobación de revocación.

1. Recuperar todas las firmas digitales

   Invoque el `SignatureServiceClient` método del `verifyPDFDocument` objeto y pase los valores siguientes:

   * Un `BLOB` objeto que contiene un documento PDF que contiene varias firmas digitales.
   * Un `PKIOptions` objeto que contiene opciones de tiempo de ejecución PKI.
   * Una `VerifySPIOptions` instancia que contiene información de SPI. Puede especificar null para este parámetro.
   El `verifyPDFDocument` método devuelve un `PDFDocumentVerificationInfo` objeto que contiene información sobre todas las firmas digitales del documento PDF.

1. Repetir mediante todas las firmas

   * Repita todas las firmas obteniendo el miembro de datos del `PDFDocumentVerificationInfo` objeto `verificationInfos` . Este miembro de datos devuelve una `Object` matriz donde cada elemento es un `PDFSignatureVerificationInfo` objeto.
   * Con el `PDFSignatureVerificationInfo` objeto, puede realizar tareas como determinar el estado de la firma obteniendo el miembro de `PDFSignatureVerificationInfo` datos del `status` objeto. Este miembro de datos devuelve un `SignatureStatus` objeto cuyo miembro de datos estáticos le informa sobre el estado de la firma. Por ejemplo, si la firma es desconocida, este método devuelve `SignatureStatus.DocumentSignatureUnknown`.

**Consulte también**

[Verificación de varias firmas digitales](#verifying-multiple-digital-signatures)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Eliminación de firmas digitales {#removing-digital-signatures}

Las firmas digitales deben eliminarse de un campo de firma para poder aplicar una firma digital más reciente. No se puede sobrescribir una firma digital. Si intenta aplicar una firma digital a un campo de firma que contiene una firma, se producirá una excepción.

>[!NOTE]
>
> Para obtener más información sobre el servicio Signature, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)de biblioteca Java de AEM Forms.

**Crear un cliente de firma**

Para poder realizar una operación de servicio de firma mediante programación, debe crear un cliente de servicio de firma.

**Obtener el documento PDF que contiene una firma para eliminar**

Para quitar una firma de un documento PDF, debe obtener un documento PDF que contenga una firma.

**Quitar la firma digital del campo de firma**

Para eliminar correctamente una firma digital de un documento PDF, debe especificar el nombre del campo de firma que contiene la firma digital. Además, debe tener permiso para eliminar la firma digital; de lo contrario, se produce una excepción.

**Guardar el documento PDF como archivo PDF**

Una vez que el servicio de firma elimina una firma digital de un campo de firma, puede guardar el documento PDF como archivo PDF para que los usuarios puedan abrirlo en Acrobat o Adobe Reader.

**Consulte también**

[Eliminación de firmas digitales mediante la API de Java](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[Eliminación de firmas digitales mediante la API de servicio web](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adición de campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields)

### Eliminación de firmas digitales mediante la API de Java {#remove-digital-signatures-using-the-java-api}

Elimine una firma digital mediante la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de firma.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `SignatureServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtener el documento PDF que contiene una firma para eliminar

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF que contiene la firma que se va a quitar mediante su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Quitar la firma digital del campo de firma

   Elimine una firma digital de un campo de firma invocando el `SignatureServiceClient` método `clearSignatureField` del objeto y pasando los siguientes valores:

   * Un `com.adobe.idp.Document` objeto que representa el documento PDF que contiene la firma que se va a quitar.
   * Un valor de cadena que especifica el nombre del campo de firma que contiene la firma digital.
   El `clearSignatureField` método devuelve un `com.adobe.idp.Document` objeto que representa el documento PDF del que se ha eliminado la firma digital.

1. Guardar el documento PDF como archivo PDF

   * Cree un `java.io.File` objeto y asegúrese de que la extensión del archivo sea .pdf.
   * Invocar el `com.adobe.idp.Document` método del `copyToFile` objeto. Pase el `java.io.File` objeto para copiar el contenido del `com.adobe.idp.Document` objeto en el archivo. Asegúrese de utilizar el `Document` objeto devuelto por el `clearSignatureField` método .

**Consulte también**

[Eliminación de firmas digitales](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Inicio rápido (modo SOAP): Eliminación de una firma digital mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminación de firmas digitales mediante la API de servicio web {#remove-digital-signatures-using-the-web-service-api}

Elimine una firma digital mediante la API de firma (servicio Web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Crear un cliente de firma

   * Cree un `SignatureServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `SignatureServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `SignatureServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtener el documento PDF que contiene una firma para eliminar

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar un documento PDF que contiene una firma digital que se va a quitar.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF firmado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el `BLOB` objeto asignando su `MTOM` propiedad con el contenido de la matriz de bytes.

1. Quitar la firma digital del campo de firma

   Elimine la firma digital invocando el `SignatureServiceClient` método `clearSignatureField` del objeto y pasando los siguientes valores:

   * Un `BLOB` objeto que contiene el documento PDF firmado.
   * Un valor de cadena que representa el nombre del campo de firma que contiene la firma digital que se va a quitar.
   El `clearSignatureField` método devuelve un `BLOB` objeto que representa el documento PDF del que se ha eliminado la firma digital.

1. Guardar el documento PDF como archivo PDF

   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF que contiene un campo de firma vacío y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto devuelto por el `sign` método. Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en el archivo PDF invocando el `System.IO.BinaryWriter` método del `Write` objeto y pasando la matriz de bytes.

**Consulte también**

[Eliminación de firmas digitales](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
