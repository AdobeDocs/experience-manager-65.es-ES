---
title: Firma y certificación digitales de documentos
seo-title: Digitally Signing and Certifying Documents
description: Utilice el servicio de firma para agregar y eliminar campos de firma digital a un documento de PDF, recuperar los nombres de campos de firma ubicados en un documento de PDF, modificar campos de firma, firmar digitalmente documentos de PDF, certificar documentos de PDF, validar firmas digitales ubicadas en un documento de PDF, validar todas las firmas digitales ubicadas en un documento de PDF y quitar una firma digital de un campo de firma.
seo-description: Use the Signature service to add and delete digital signature fields to a PDF document, retrieve the names of signature fields located in a PDF document, modify signature fields, digitally sign PDF documents, certify PDF documents, validate digital signatures located in a PDF document, validate all digital signatures located in a PDF document, and remove a digital signature from a signature field.
uuid: 6331de8a-2a9c-45bf-89d2-29f1ad5cc856
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 42de04bf-25e4-4478-a411-38671ed871ae
role: Developer
exl-id: c200f345-40ab-46fd-b6ed-f3af0a23796b
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '17046'
ht-degree: 0%

---

# Firma y certificación digitales de documentos {#digitally-signing-and-certifying-documents}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

**Acerca del servicio de firma**

El servicio Signature permite que su organización proteja la seguridad y la privacidad de los documentos de Adobe PDF que distribuye y recibe. Este servicio utiliza firmas digitales y certificación para garantizar que solo los destinatarios objetivo puedan modificar los documentos. Dado que las características de seguridad se aplican al documento en sí, el documento sigue siendo seguro y controlado durante todo su ciclo de vida. Un documento permanece seguro más allá del cortafuegos, cuando se descarga sin conexión y cuando se envía de nuevo a su organización.

>[!NOTE]
>
>Puede crear un controlador de firma personalizado para el servicio de firma que se invoque cuando se invocan ciertas operaciones, como la firma de un documento de PDF.

**Nombres de campos de firma**

Algunas operaciones del servicio de firma requieren que especifique el nombre del campo de firma en el que se realiza una operación. Por ejemplo, al firmar un documento de PDF, se especifica el nombre del campo de firma que se va a firmar. Supongamos que el nombre completo de un campo de firma es `form1[0].Form1[0].SignatureField1[0]`. Puede especificar `SignatureField1[0]` en lugar de `form1[0].Form1[0].SignatureField1[0]`.

A veces, un conflicto hace que el servicio de firma firme firme (o realice otra operación que requiera el nombre del campo de firma) el campo incorrecto. Este conflicto es el resultado del nombre `SignatureField1[0]` aparece en dos o más lugares del mismo documento de PDF. Por ejemplo, considere un documento de PDF que contenga dos campos de firma llamados `form1[0].Form1[0].SignatureField1[0]` y `form1[0].Form1[0].SubForm1[0].SignatureField1[0]` y especifique `SignatureField1[0]`. En este caso, el servicio de firma firma firma el primer campo de firma que encuentra mientras se iteran todos los campos de firma del documento.

Si hay varios campos de firma ubicados dentro de un documento de PDF, se recomienda especificar los nombres completos de los campos de firma. Es decir, especifique `form1[0].Form1[0].SignatureField1[0]`en lugar de `SignatureField1[0]`.

Puede realizar estas tareas mediante el servicio de firma:

* Agregue y elimine campos de firma digital a un documento de PDF. (Consulte [Adición de campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields).)
* Recupere los nombres de los campos de firma ubicados en un documento de PDF. (Consulte [Recuperación de nombres de campos de firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names).)
* Modificar campos de firma. (Consulte [Modificación de campos de firma](digitally-signing-certifying-documents.md#modifying-signature-fields).)
* Firme digitalmente documentos PDF. (Consulte [Firma digital de documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)
* Certificar documentos del PDF. (Consulte [Certificación de documentos del PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents).)
* Valide las firmas digitales ubicadas en un documento de PDF. (Consulte [Verificación de firmas digitales](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* Valide todas las firmas digitales ubicadas en un documento de PDF. (Consulte [Verificación de varias firmas digitales](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* Eliminar una firma digital de un campo de firma. (Consulte [Eliminación de firmas digitales](digitally-signing-certifying-documents.md#removing-digital-signatures).)

>[!NOTE]
>
>Para obtener más información sobre el servicio Signature, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)...

## Adición de campos de firma {#adding-signature-fields}

Las firmas digitales aparecen en los campos de firma, que son campos de formulario que contienen una representación gráfica de la firma. Los campos de firma pueden ser visibles o invisibles. Los firmantes pueden utilizar un campo de firma preexistente o se puede agregar un campo de firma mediante programación. En cualquier caso, el campo de firma debe existir antes de que se pueda firmar un documento de PDF.

Puede añadir mediante programación un campo de firma utilizando la API de Java del servicio de firma o la API del servicio web de firma. Puede agregar más de un campo de firma a un documento de PDF; sin embargo, cada nombre de campo de firma debe ser único.

>[!NOTE]
>
>Algunos tipos de documento PDF no permiten agregar un campo de firma mediante programación. Para obtener más información sobre el servicio Signature y la adición de campos de firma, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para agregar un campo de firma a un documento de PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de firma.
1. Obtenga un documento PDF al que se agrega un campo de firma.
1. Agregue un campo de firma.
1. Guarde el documento de PDF como archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

**Crear un cliente de firma**

Para poder realizar una operación de servicio de firma mediante programación, debe crear un cliente de servicio de firma.

**Obtener un documento del PDF al que se agrega un campo de firma**

Debe obtener un documento de PDF al que se agregue un campo de firma.

**Añadir un campo de firma**

Para agregar correctamente un campo de firma a un documento de PDF, se especifican valores de coordenadas que identifican la ubicación del campo de firma. (Si agrega un campo de firma invisible, estos valores no son obligatorios). Además, puede especificar qué campos del documento del PDF están bloqueados después de aplicar una firma al campo de firma.

**Guarde el documento del PDF como archivo del PDF**

Una vez que el servicio de firma agrega un campo de firma al documento del PDF, puede guardar el documento como archivo del PDF para que los usuarios puedan abrirlo en Acrobat o Adobe Reader.

**Consulte también lo siguiente**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Firma digital de documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Adición de campos de firma mediante la API de Java {#add-signature-fields-using-the-java-api}

Agregue un campo de firma utilizando la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-signatures-client.jar, en la ruta de clase de su proyecto Java.

1. Crear un cliente de firma

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `SignatureServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtener un documento del PDF al que se agrega un campo de firma

   * Cree un `java.io.FileInputStream` objeto que representa el documento PDF al que se agrega un campo de firma empleando su constructor y pasando un valor de cadena que especifica la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Añadir un campo de firma

   * Cree un `PositionRectangle` objeto que especifica la ubicación del campo de firma utilizando su constructor. Dentro del constructor, especifique valores de coordenadas.
   * Si lo desea, cree un `FieldMDPOptions` objeto que especifica los campos que están bloqueados cuando se aplica una firma digital al campo de firma.
   * Agregue un campo de firma a un documento de PDF invocando la variable `SignatureServiceClient` del objeto `addSignatureField` y pasando los siguientes valores:

      * A `com.adobe.idp`. `Document` objeto que representa el documento del PDF al que se agrega un campo de firma.
      * Un valor de cadena que especifica el nombre del campo de firma.
      * A `java.lang.Integer` que representa el número de página al que se agrega un campo de firma.
      * A `PositionRectangle` objeto que especifica la ubicación del campo de firma.
      * A `FieldMDPOptions` objeto que especifica los campos del documento del PDF que se bloquean después de aplicar una firma digital al campo de firma. Este valor del parámetro es opcional y puede pasar `null`.
   * A `PDFSeedValueOptions` objeto que especifica varios valores de tiempo de ejecución. Este valor del parámetro es opcional y puede pasar `null`.

      La variable `addSignatureField` el método devuelve un `com.adobe.idp`. `Document` objeto que representa un documento de PDF que contiene un campo de firma.
   >[!NOTE]
   >
   >Puede invocar la variable `SignatureServiceClient` del objeto `addInvisibleSignatureField` para añadir un campo de firma invisible.

1. Guarde el documento del PDF como archivo del PDF

   * Cree un `java.io.File` y asegúrese de que la extensión de archivo es .pdf.
   * Invocar el `com.adobe.idp`. `Document` del objeto `copyToFile` para copiar el contenido del `Document` al archivo. Asegúrese de usar la variable `com.adobe.idp`. `Document` objeto devuelto por el `addSignatureField` método.

**Consulte también lo siguiente**

[Inicio rápido de la API del servicio de firma](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### Adición de campos de firma mediante la API de servicio web {#add-signature-fields-using-the-web-service-api}

Para añadir un campo de firma mediante la API de firma (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Crear un cliente de firma

   * Cree un `SignatureServiceClient` usando su constructor predeterminado.
   * Cree un `SignatureServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `SignatureServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtener un documento del PDF al que se agrega un campo de firma

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar el documento del PDF que contendrá un campo de firma.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Añadir un campo de firma

   Agregue un campo de firma al documento del PDF invocando la variable `SignatureServiceClient` del objeto `addSignatureField` y pasando los siguientes valores:

   * A `BLOB` objeto que representa el documento del PDF al que se agrega un campo de firma.
   * Valor de cadena que especifica el nombre del campo de firma.
   * Un valor entero que representa el número de página al que se agrega un campo de firma.
   * A `PositionRect` objeto que especifica la ubicación del campo de firma.
   * A `FieldMDPOptions` objeto que especifica los campos del documento del PDF que se bloquean después de aplicar una firma digital al campo de firma. Este valor del parámetro es opcional y puede pasar `null`.
   * A `PDFSeedValueOptions` objeto que especifica varios valores de tiempo de ejecución. Este valor del parámetro es opcional y puede pasar `null`.

   La variable `addSignatureField` el método devuelve un `BLOB` objeto que representa un documento de PDF que contiene un campo de firma.

1. Guarde el documento del PDF como archivo del PDF

   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF que contendrá el campo de firma y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto devuelto por el `addSignatureField` método. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `binaryData` miembro de datos.
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Recuperación de nombres de campos de firma {#retrieving-signature-field-names}

Puede recuperar los nombres de todos los campos de firma que se encuentran en un documento de PDF que desee firmar o certificar. Si no está seguro de los nombres de los campos de firma que se encuentran en un documento de PDF o desea verificarlos, puede recuperarlos mediante programación. El servicio de firma devuelve el nombre completo del campo de firma, como `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

>[!NOTE]
>
>Para obtener más información sobre el servicio Signature, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Resumen de los pasos {#summary_of_steps-1}

Para recuperar los nombres de los campos de firma, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de firma.
1. Obtenga el documento del PDF que contiene campos de firma.
1. Recupere los nombres de los campos de firma.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de firma**

Para poder realizar una operación de servicio de firma mediante programación, debe crear un cliente de servicio de firma.

**Obtener el documento del PDF que contiene campos de firma**

Recupere un documento de PDF que contenga campos de firma.

**Recuperar los nombres de los campos de firma**

Puede recuperar los nombres de los campos de firma después de recuperar un documento de PDF que contenga uno o más campos de firma.

**Consulte también lo siguiente**

[Recuperar nombres de campos de firma mediante la API de Java](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[Recuperar el campo de firma mediante la API de servicio web](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adición de campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields)

### Recuperar nombres de campos de firma mediante la API de Java {#retrieve-signature-field-names-using-the-java-api}

Recupere los nombres de los campos de firma utilizando la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-signatures-client.jar, en la ruta de clase de su proyecto Java.

1. Crear un cliente de firma

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `SignatureServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtener el documento del PDF que contiene campos de firma

   * Cree un `java.io.FileInputStream` objeto que representa el documento de PDF que contiene campos de firma utilizando su constructor y pasando un valor de cadena que especifica la ubicación del documento de PDF.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Recuperar los nombres de los campos de firma

   * Recupere los nombres de los campos de firma invocando la variable `SignatureServiceClient` del objeto `getSignatureFieldList` y pasando el `com.adobe.idp.Document` objeto que contiene el documento del PDF que contiene campos de firma. Este método devuelve un `java.util.List` objeto, en el que cada elemento contiene un `PDFSignatureField` objeto. Con este objeto, puede obtener información adicional sobre un campo de firma, como si está visible.
   * Iterar a través de la variable `java.util.List` para determinar si hay nombres de campo de firma. Para cada campo de firma del documento del PDF, puede obtener una `PDFSignatureField` objeto. Para obtener el nombre del campo de firma, invoque la variable `PDFSignatureField` del objeto `getName` método. Este método devuelve un valor de cadena que especifica el nombre del campo de firma.

**Consulte también lo siguiente**

[Recuperación de nombres de campos de firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Inicio rápido (modo SOAP): Recuperación de nombres de campos de firma mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar el campo de firma mediante la API de servicio web {#retrieve-signature-field-using-the-web-service-api}

Recupere los nombres de los campos de firma mediante la API de firma (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Crear un cliente de firma

   * Cree un `SignatureServiceClient` usando su constructor predeterminado.
   * Cree un `SignatureServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `SignatureServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtener el documento del PDF que contiene campos de firma

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar el documento del PDF que contiene campos de firma.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` campo el contenido de la matriz de bytes.

1. Recuperar los nombres de los campos de firma

   * Recupere los nombres de los campos de firma invocando `SignatureServiceClient` del objeto `getSignatureFieldList` y pasando el `BLOB` objeto que contiene el documento del PDF que contiene campos de firma. Este método devuelve un `MyArrayOfPDFSignatureField` objeto de colección donde cada elemento contiene un `PDFSignatureField` objeto.
   * Iterar a través de la variable `MyArrayOfPDFSignatureField` para determinar si hay nombres de campo de firma. Para cada campo de firma del documento del PDF, puede obtener una `PDFSignatureField` objeto. Para obtener el nombre del campo de firma, invoque la variable `PDFSignatureField` del objeto `getName` método. Este método devuelve un valor de cadena que especifica el nombre del campo de firma.

**Consulte también lo siguiente**

[Recuperación de nombres de campos de firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modificación de campos de firma {#modifying-signature-fields}

Puede modificar los campos de firma que se encuentran en un documento de PDF mediante la API de Java y la API de servicio web. La modificación de un campo de firma implica la manipulación de sus valores de diccionario de bloqueo de campo de firma o valores de diccionario de valores semilla.

A *diccionario de bloqueo de campo* especifica una lista de campos que están bloqueados cuando se firma el campo de firma. Un campo bloqueado impide que los usuarios realicen cambios en el campo. A *diccionario de valores semilla* contiene información de restricción que se utiliza en el momento en que se aplica la firma. Por ejemplo, puede cambiar los permisos que controlan las acciones que se pueden producir sin invalidar una firma.

Si modifica un campo de firma existente, puede realizar cambios en el documento del PDF para reflejar los cambios en los requisitos comerciales. Por ejemplo, un nuevo requisito comercial puede requerir el bloqueo de todos los campos de documento después de firmar el documento.

En esta sección se explica cómo modificar un campo de firma mediante la modificación de los valores del diccionario de bloqueo de campos y del diccionario de valores semilla. Los cambios realizados en el diccionario de bloqueo de campos de firma hacen que todos los campos del documento del PDF se bloqueen cuando se firma un campo de firma. Los cambios realizados en el diccionario de valores sembrados prohíben tipos específicos de cambios en el documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio de firma y la modificación de los campos de firma, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-2}

Para modificar los campos de firma ubicados en un documento de PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de firma.
1. Obtenga el documento del PDF que contiene el campo de firma que desea modificar.
1. Establezca los valores del diccionario.
1. Modifique el campo de firma.
1. Guarde el documento de PDF como archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de LiveCycle](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de firma**

Para poder realizar una operación de servicio de firma mediante programación, debe crear un cliente de servicio de firma.

**Obtener el documento del PDF que contiene el campo de firma que se va a modificar**

Recupere un documento de PDF que contenga el campo de firma que desea modificar.

**Definir valores de diccionario**

Para modificar un campo de firma, asigne valores a su diccionario de bloqueo de campo o diccionario de valores semilla. La especificación de los valores del diccionario de bloqueo de campos de firma implica la especificación de los campos de documento de PDF que están bloqueados cuando se firma el campo de firma. (Esta sección explica cómo bloquear todos los campos).

Se pueden configurar los siguientes valores de diccionario de valores semilla:

* **Comprobación de revisión**: Especifica si la comprobación de revocación se realiza cuando se aplica una firma al campo de firma.
* **Opciones de certificado**: Asigna valores al diccionario de valores sembrados de certificados. Antes de especificar las opciones de certificado, se recomienda que se familiarice con un diccionario de valores sembrados de certificado. (Consulte [Referencia del PDF](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **Opciones de resumen**: Asigna los algoritmos de compendio que se utilizan para la firma. Los valores válidos son SHA1, SHA256, SHA384, SHA512 y RIPEMD160.
* **Filtro**: Especifica el filtro que se utiliza con el campo de firma. Por ejemplo, puede utilizar el filtro Adobe.PPKLite . (Consulte [Referencia del PDF](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **Opciones de marca**: Especifica los valores de marca asociados a este campo de firma. Un valor de 1 significa que un firmante debe utilizar solamente los valores especificados para la entrada. Un valor de 0 significa que se permiten otros valores. Estas son las posiciones de Bit:

   * **1 (Filtro):** El controlador de firma que se utilizará para firmar el campo de firma
   * **2 (Subfiltro):** Matriz de nombres que indican codificaciones aceptables para utilizar al firmar
   * **3 V)**: El número mínimo de versión requerido del controlador de firma que se utilizará para firmar el campo de firma
   * **4 (Motivos):** Matriz de cadenas que especifican posibles motivos para firmar un documento
   * **5 (PDFLegalWarnings):** Conjunto de cadenas que especifica posibles autenticaciones legales

* **Afirmaciones legales**: Cuando un documento está certificado, se analiza automáticamente para detectar tipos específicos de contenido que puedan hacer que el contenido visible de un documento sea ambiguo o engañoso. Por ejemplo, una anotación puede ocultar texto importante para comprender lo que se está certificando. El proceso de digitalización genera advertencias que indican la presencia de este tipo de contenido. También proporciona una explicación adicional del contenido que puede haber generado advertencias.
* **Permisos**: Especifica los permisos que se pueden utilizar en un documento de PDF sin invalidar la firma.
* **Razones**: Especifica los motivos por los que se debe firmar este documento.
* **Marca de tiempo**: Especifica las opciones de marca de hora. Por ejemplo, puede establecer la dirección URL del servidor de marca de tiempo utilizado.
* **Versión**: Especifica el número de versión mínimo del controlador de firma que se utilizará para firmar el campo de firma.

**Modificación del campo de firma**

Después de crear un cliente de servicios de firma, recuperar el documento del PDF que contiene el campo de firma que se va a modificar y establecer los valores del diccionario, puede solicitar al servicio de firma que modifique el campo de firma. A continuación, el servicio de firma devuelve un documento de PDF que contiene el campo de firma modificado. El documento del PDF original no se ve afectado.

**Guarde el documento del PDF como archivo del PDF**

Guarde el documento PDF que contiene el campo de firma modificado como archivo PDF para que los usuarios puedan abrirlo en Acrobat o Adobe Reader.

**Consulte también lo siguiente**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de firma](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[Firma digital de documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Modificación de campos de firma mediante la API de Java {#modify-signature-fields-using-the-java-api}

Modifique un campo de firma utilizando la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-signatures-client.jar, en la ruta de clase de su proyecto Java.

1. Crear un cliente de firma

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `SignatureServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtener el documento del PDF que contiene el campo de firma que se va a modificar

   * Cree un `java.io.FileInputStream` objeto que representa el documento del PDF que contiene el campo de firma que se va a modificar utilizando su constructor y pasando un valor de cadena que especifica la ubicación del documento del PDF.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Definir valores de diccionario

   * Cree un `PDFSignatureFieldProperties` usando su constructor. A `PDFSignatureFieldProperties` el objeto almacena información de diccionario de bloqueo de campos de firma y de diccionario de valores semilla.
   * Cree un `PDFSeedValueOptionSpec` usando su constructor. Este objeto permite establecer valores de diccionario de valores semilla.
   * No permitir cambios en el documento del PDF invocando la variable `PDFSeedValueOptionSpec` del objeto `setMdpValue` y pasando el `MDPPermissions.NoChanges` valor de enumeración.
   * Cree un `FieldMDPOptionSpec` usando su constructor. Este objeto permite establecer los valores del diccionario de bloqueo de campos de firma.
   * Bloqueo de todos los campos del documento del PDF invocando la variable `FieldMDPOptionSpec` del objeto `setMdpValue` y pasando el `FieldMDPAction.ALL` valor de enumeración.
   * Establezca la información del diccionario de valores semilla invocando la variable `PDFSignatureFieldProperties` del objeto `setSeedValue` y pasando el `PDFSeedValueOptionSpec` objeto.
   * Establezca la información del diccionario de bloqueo del campo de firma invocando la variable `PDFSignatureFieldProperties`del objeto `setFieldMDP` y pasando el `FieldMDPOptionSpec` objeto.

   >[!NOTE]
   >
   >Para ver todos los valores del diccionario de valores sembrados que puede establecer, consulte la `PDFSeedValueOptionSpec` referencia de clase. (Consulte [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

1. Modificación del campo de firma

   Modifique el campo de firma invocando la variable `SignatureServiceClient` del objeto `modifySignatureField` y pasando los siguientes valores:

   * La variable `com.adobe.idp.Document` objeto que almacena el documento del PDF que contiene el campo de firma que se va a modificar
   * Un valor de cadena que especifica el nombre del campo de firma
   * La variable `PDFSignatureFieldProperties` objeto que almacena información del diccionario de bloqueo de campos de firma y del diccionario de valores semilla

   La variable `modifySignatureField` el método devuelve un `com.adobe.idp.Document` objeto que almacena un documento de PDF que contiene el campo de firma modificado.

1. Guarde el documento del PDF como archivo del PDF

   * Cree un `java.io.File` y asegúrese de que la extensión del nombre de archivo es .pdf.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `com.adobe.idp.Document` al archivo. Asegúrese de usar la variable `com.adobe.idp.Document` que la variable `modifySignatureField` método devuelto.

### Modificación de campos de firma mediante la API de servicio web {#modify-signature-fields-using-the-web-service-api}

Modifique un campo de firma utilizando la API de firma (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Crear un cliente de firma

   * Cree un `SignatureServiceClient` usando su constructor predeterminado.
   * Cree un `SignatureServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `SignatureServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtener el documento del PDF que contiene el campo de firma que se va a modificar

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar el documento del PDF que contiene el campo de firma que se va a modificar.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` propiedad del contenido de la matriz de bytes.

1. Definir valores de diccionario

   * Cree un `PDFSignatureFieldProperties` usando su constructor. Este objeto almacena el diccionario de bloqueo de campos de firma y la información del diccionario de valores semilla.
   * Cree un `PDFSeedValueOptionSpec` usando su constructor. Este objeto permite establecer valores de diccionario de valores semilla.
   * No permitir cambios en el documento del PDF asignando la variable `MDPPermissions.NoChanges` valor de enumeración a la variable `PDFSeedValueOptionSpec` del objeto `mdpValue` miembro de datos.
   * Cree un `FieldMDPOptionSpec` usando su constructor. Este objeto permite establecer los valores del diccionario de bloqueo de campos de firma.
   * Bloquee todos los campos del documento del PDF asignando la variable `FieldMDPAction.ALL` valor de enumeración a la variable `FieldMDPOptionSpec` del objeto `mdpValue` miembro de datos.
   * Configure la información del diccionario del valor de inicialización asignando la variable `PDFSeedValueOptionSpec` al `PDFSignatureFieldProperties` del objeto `seedValue` miembro de datos.
   * Configure la información del diccionario de bloqueo del campo de firma asignando la variable `FieldMDPOptionSpec` al `PDFSignatureFieldProperties` del objeto `fieldMDP` miembro de datos.

   >[!NOTE]
   >
   >Para ver todos los valores del diccionario de valores sembrados que puede establecer, consulte la `PDFSeedValueOptionSpec` referencia de clase. (Consulte [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)).

1. Modificación del campo de firma

   Modifique el campo de firma invocando la variable `SignatureServiceClient` del objeto `modifySignatureField` y pasando los siguientes valores:

   * La variable `BLOB` objeto que almacena el documento del PDF que contiene el campo de firma que se va a modificar
   * Un valor de cadena que especifica el nombre del campo de firma
   * La variable `PDFSignatureFieldProperties` objeto que almacena información del diccionario de bloqueo de campos de firma y del diccionario de valores semilla

   La variable `modifySignatureField` el método devuelve un `BLOB` objeto que almacena un documento de PDF que contiene el campo de firma modificado.

1. Guarde el documento del PDF como archivo del PDF

   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF que contendrá el campo de firma y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` que la variable `addSignatureField` devuelve. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` miembro de datos.
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Firma digital de documentos PDF {#digitally-signing-pdf-documents}

Las firmas digitales se pueden aplicar a documentos PDF para proporcionar un nivel de seguridad. Las firmas digitales, como las firmas manuscritas, proporcionan un medio para que los firmantes se identifiquen y hagan declaraciones sobre un documento. La tecnología utilizada para firmar documentos digitalmente ayuda a garantizar que tanto el firmante como los destinatarios tengan una idea clara de lo que se firmó y estén seguros de que el documento no se alteró desde que se firmó.

Los documentos PDF se firman mediante tecnología de clave pública. Un firmante tiene dos claves: una clave pública y una clave privada. La clave privada se almacena en las credenciales de un usuario que deben estar disponibles en el momento de la firma. La clave pública se almacena en el certificado del usuario que debe estar disponible para que los destinatarios validen la firma. La información sobre los certificados revocados se encuentra en las listas de revocación de certificados (CRL) y en las respuestas del Protocolo de estado de certificado en línea (OCSP) distribuidas por las autoridades de certificación (CA). La hora de la firma se puede obtener de una fuente de confianza conocida como Autoridad de marca de tiempo.

>[!NOTE]
>
>Para poder firmar digitalmente un documento de PDF, debe asegurarse de agregar el certificado a AEM Forms. Se agrega un certificado mediante la consola de administración o mediante programación mediante la API del administrador de confianza. (Consulte [Importación de credenciales mediante la API del administrador de confianza](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

Puede firmar digitalmente mediante programación documentos PDF. Al firmar digitalmente un documento de PDF, debe hacer referencia a una credencial de seguridad que exista en AEM Forms. La credencial es la clave privada que se utiliza para la firma.

El servicio Signature realiza los siguientes pasos cuando se firma un documento de PDF:

1. El servicio de firma recupera las credenciales del Truststore pasando el alias especificado en la solicitud.
1. Truststore busca las credenciales especificadas.
1. La credencial se devuelve al servicio de firma y se utiliza para firmar el documento. Las credenciales también se almacenan en caché con el alias para solicitudes futuras.

Para obtener información sobre la administración de las credenciales de seguridad, consulte la *Instalación e implementación de AEM Forms* para su servidor de aplicaciones.

>[!NOTE]
>
>Existen diferencias entre la firma y la certificación de documentos. (Consulte [Certificación de documentos del PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents).)

>[!NOTE]
>
>No todos los documentos del PDF admiten la firma. Para obtener más información sobre el servicio Signature y la firma digital de documentos, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>El servicio Signature no admite archivos XDP con datos de PDF incrustados como entrada para una operación, como la certificación de un documento. Esta acción hace que el servicio de firma inicie una `PDFOperationException`. Para resolver este problema, convierta el archivo XDP a un archivo PDF mediante el servicio PDF Utilidades y, a continuación, pase el archivo PDF convertido a una operación del servicio de firma. (Consulte [Uso de utilidades de PDF](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities).)

**Credencial nShield HSM del cifrado**

Cuando se utiliza una credencial nCipher nShield HSM para firmar o certificar un documento PDF, no se puede utilizar la nueva credencial hasta que se reinicie el servidor de aplicaciones J2EE en el que se implementa AEM Forms. Sin embargo, puede establecer un valor de configuración, lo que da como resultado que la operación de firma o certificación funcione sin reiniciar el servidor de aplicaciones J2EE.

Puede añadir el siguiente valor de configuración en el archivo cknfastrc, que se encuentra en /opt/nfast/cknfastrc (o c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Después de agregar este valor de configuración al archivo cknfastrc, la nueva credencial se puede usar sin reiniciar el servidor de aplicaciones J2EE.

**La firma no es de confianza**

Al certificar y firmar el mismo documento de PDF, si la firma de certificación no es de confianza, aparece un triángulo amarillo contra la primera firma al abrir el documento de PDF en Acrobat o Adobe Reader. La firma certificadora debe ser de confianza para evitar esta situación.

**Firma de documentos que son formularios basados en XFA**

Si intenta firmar un formulario basado en XFA mediante la API de servicio de firma, es posible que falten los datos en la variable `View` `Signed` `Version` ubicado en Acrobat. Por ejemplo, considere el siguiente flujo de trabajo:

* Con un archivo XDP creado con Designer, se combina un diseño de formulario que contiene un campo de firma y datos XML que contienen datos de formulario. El servicio Forms se utiliza para generar un documento de PDF interactivo.
* Firma el documento del PDF mediante la API del servicio de firma.

### Resumen de los pasos {#summary_of_steps-3}

Para firmar digitalmente un documento de PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de firma.
1. Obtenga el documento del PDF para firmar.
1. Firme el documento del PDF.
1. Guarde el documento de PDF firmado como archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

**Crear un cliente de firmas**

Para poder realizar una operación de servicio de firma mediante programación, debe crear un cliente de servicio de firma.

**Obtener el documento del PDF para firmar**

Para firmar un documento de PDF, debe obtener un documento de PDF que contenga un campo de firma. Si un documento PDF no contiene un campo de firma, no se puede firmar. Se puede agregar un campo de firma mediante Designer o mediante programación.

**Firmar el documento del PDF**

Al firmar un documento de PDF, puede establecer las opciones en tiempo de ejecución que utiliza el servicio de firma. Puede establecer las siguientes opciones:

* Opciones de aspecto
* Comprobación de revocación
* Valores de marca de hora

Las opciones de aspecto se configuran mediante una `PDFSignatureAppearanceOptionSpec` objeto. Por ejemplo, puede mostrar la fecha dentro de una firma invocando la variable `PDFSignatureAppearanceOptionSpec` del objeto `setShowDate` método y paso `true`.

También puede especificar si desea realizar o no una comprobación de revocación que determine si se ha revocado el certificado utilizado para firmar digitalmente un documento PDF. Para realizar la comprobación de revocación, puede especificar uno de los siguientes valores:

* **NoCheck**: No realice la comprobación de revocación.
* **BestEffort**: Intente comprobar siempre la revocación de todos los certificados de la cadena. Si se produce algún problema en la comprobación, se supone que la revocación es válida. Si se produce algún error, supongamos que el certificado no se revoca.
* **CheckIfAvailable:** Compruebe la revocación de todos los certificados de la cadena si la información de revocación está disponible. Si se produce algún problema al comprobar, se supone que la revocación no es válida. Si se produce algún error, supongamos que el certificado se revoca y no es válido. (Este es el valor predeterminado.)
* **AlwaysCheck**: Compruebe la revocación de todos los certificados de la cadena. Si la información de revocación no está presente en ningún certificado, se supone que la revocación no es válida.

Para realizar la comprobación de revocación en un certificado, puede especificar una URL para un servidor de lista de revocación de certificados (CRL) utilizando un `CRLOptionSpec` objeto. Sin embargo, si desea comprobar la revocación y no especifica una URL a un servidor CRL, el servicio de firma obtiene la URL del certificado.

En lugar de utilizar un servidor CRL, puede utilizar un servidor de protocolo de estado de certificado en línea (OCSP) al realizar la comprobación de revocación. Normalmente, cuando se utiliza un servidor OCSP en lugar de un servidor CRL, la comprobación de revocación se realiza más rápido. (Consulte &quot;Protocolo de estado de certificado en línea&quot; en [https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560).)

Puede establecer el orden del servidor CRL y OCSP que utiliza el servicio de firmas mediante Aplicaciones y Servicios de Adobe. Por ejemplo, si el servidor OCSP se configura primero en Aplicaciones y Servicios de Adobe, se comprueba el servidor OCSP, seguido del servidor CRL. (Consulte &quot;Administración de certificados y credenciales mediante el almacén de confianza&quot; en la Ayuda de AAC).

Si especifica que no se debe realizar la comprobación de revocación, el servicio de firma no comprobará si se ha revocado el certificado utilizado para firmar o certificar un documento. Es decir, se ignora la información del servidor CRL y OCSP.

>[!NOTE]
>
>Aunque en el certificado se puede especificar una CRL o un servidor OCSP, puede anular la URL especificada en el certificado mediante una `CRLOptionSpec` y `OCSPOptionSpec` objeto. Por ejemplo, para anular el servidor CRL, puede invocar la variable `CRLOptionSpec` del objeto `setLocalURI` método.

La marca de hora se refiere al proceso de seguimiento del momento en que se modificó un documento firmado o certificado. Una vez firmado un documento, no se debe modificar, ni siquiera por el propietario del documento. La marca de hora ayuda a hacer cumplir la validez de un documento firmado o certificado. Puede establecer las opciones de marca de hora mediante un `TSPOptionSpec` objeto. Por ejemplo, puede especificar la URL de un servidor de proveedor de marca de hora (TSP).

>[!NOTE]
>
>En el recorrido de Java y el servicio web por las secciones y los inicios rápidos correspondientes, se utiliza la comprobación de revocación. Dado que no se especifica ninguna CRL ni información del servidor OCSP, la información del servidor se obtiene del certificado utilizado para firmar digitalmente el documento de PDF.

Para firmar correctamente un documento de PDF, puede especificar el nombre completo del campo de firma que contendrá la firma digital, como `form1[0].#subform[1].SignatureField3[3]`. Al utilizar un campo de formulario XFA, también se puede utilizar el nombre parcial del campo de firma: `SignatureField3[3]`.

También debe hacer referencia a una credencial de seguridad para firmar digitalmente un documento de PDF. Para hacer referencia a una credencial de seguridad, debe especificar un alias. El alias es una referencia a una credencial real que puede estar en un archivo PKCS#12 (con extensión .pfx) o en un módulo de seguridad de hardware (HSM). Para obtener información sobre las credenciales de seguridad, consulte la *Instalación e implementación de AEM Forms* para su servidor de aplicaciones.

**Guardar el documento del PDF firmado**

Una vez que el servicio de firma firma firma digitalmente el documento de PDF, puede guardarlo como archivo de PDF para que los usuarios puedan abrirlo en Acrobat o Adobe Reader.

**Consulte también lo siguiente**

[Firmar digitalmente documentos PDF mediante la API de Java](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[Firma digital de documentos de PDF mediante la API de servicio web](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adición de campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields)

[Recuperación de nombres de campos de firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### Firmar digitalmente documentos PDF mediante la API de Java {#digitally-sign-pdf-documents-using-the-java-api}

Firme digitalmente un documento de PDF mediante la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-signatures-client.jar, en la ruta de clase de su proyecto Java.

1. Crear un cliente de firmas

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `SignatureServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtener el documento del PDF para firmar

   * Cree un `java.io.FileInputStream` objeto que representa el documento PDF que se va a firmar digitalmente usando su constructor y pasando un valor de cadena que especifica la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Firmar el documento del PDF

   Firme el documento del PDF invocando la variable `SignatureServiceClient` del objeto `sign` y pasando los siguientes valores:

   * A `com.adobe.idp.Document` que representa el documento PDF que se va a firmar.
   * Valor de cadena que representa el nombre del campo de firma que contendrá la firma digital.
   * A `Credential` objeto que representa la credencial que se utiliza para firmar digitalmente el documento del PDF. Cree un `Credential` invocando el objeto `Credential` estático del objeto `getInstance` y pasando un valor de cadena que especifica el valor de alias que corresponde a la credencial de seguridad.
   * A `HashAlgorithm` objeto que especifica un miembro de datos estático que representa el algoritmo hash que se va a usar para resumir el documento del PDF. Por ejemplo, puede especificar `HashAlgorithm.SHA1` para usar el algoritmo SHA1.
   * Un valor de cadena que representa el motivo por el que el documento del PDF se firmó digitalmente.
   * Valor de cadena que representa la información de contacto del firmante.
   * A `PDFSignatureAppearanceOptions` que controla el aspecto de la firma digital. Por ejemplo, puede utilizar este objeto para agregar un logotipo personalizado a una firma digital.
   * A `java.lang.Boolean` objeto que especifica si se realizará la comprobación de revocación en el certificado del firmante.
   * Un `OCSPOptionSpec` objeto que almacena preferencias para la compatibilidad con el Protocolo de estado de certificado en línea (OCSP). Si no se realiza la comprobación de revocación, no se usa este parámetro y puede especificar `null`.
   * A `CRLPreferences` objeto que almacena las preferencias de lista de revocación de certificados (CRL). Si no se realiza la comprobación de revocación, no se usa este parámetro y puede especificar `null`.
   * A `TSPPreferences` objeto que almacena las preferencias de compatibilidad con el proveedor de marcas de hora (TSP). Este parámetro es opcional y puede ser `null`. Para obtener más información, consulte [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   La variable `sign` el método devuelve un `com.adobe.idp.Document` que representa el documento PDF firmado.

1. Guardar el documento del PDF firmado

   * Cree un `java.io.File` y asegúrese de que la extensión de archivo es .pdf.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` método y pase `java.io.File`para copiar el contenido del `Document` al archivo. Asegúrese de usar la variable `com.adobe.idp.Document` objeto devuelto por el `sign` método.

**Consulte también lo siguiente**

[Firma digital de documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Inicio rápido (modo SOAP): Firma digital de un documento de PDF mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Firma digital de documentos de PDF mediante la API de servicio web {#digitally-signing-pdf-documents-using-the-web-service-api}

Para firmar digitalmente un documento de PDF mediante la API de firma (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Crear un cliente de firmas

   * Cree un `SignatureServiceClient` usando su constructor predeterminado.
   * Cree un `SignatureServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `SignatureServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtener el documento del PDF para firmar

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar un documento de PDF firmado.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF que se va a firmar y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` propiedad del contenido de la matriz de bytes.

1. Firmar el documento del PDF

   Firme el documento del PDF invocando la variable `SignatureServiceClient` del objeto `sign` y pasando los siguientes valores:

   * A `BLOB` que representa el documento PDF que se va a firmar.
   * Valor de cadena que representa el nombre del campo de firma que contendrá la firma digital.
   * A `Credential` objeto que representa la credencial que se utiliza para firmar digitalmente el documento del PDF. Cree un `Credential` utilizando su constructor y especifique el alias asignando un valor al `Credential` del objeto `alias` propiedad.
   * A `HashAlgorithm` objeto que especifica un miembro de datos estático que representa el algoritmo hash que se va a usar para resumir el documento del PDF. Por ejemplo, puede especificar `HashAlgorithm.SHA1` para usar el algoritmo SHA1.
   * Un valor booleano que especifica si se utiliza el algoritmo hash.
   * Un valor de cadena que representa el motivo por el que el documento del PDF se firmó digitalmente.
   * Valor de cadena que representa la ubicación del firmante.
   * Valor de cadena que representa la información de contacto del firmante.
   * A `PDFSignatureAppearanceOptions` que controla el aspecto de la firma digital. Por ejemplo, puede utilizar este objeto para agregar un logotipo personalizado a una firma digital.
   * A `System.Boolean` objeto que especifica si se realizará la comprobación de revocación en el certificado del firmante. Si esta comprobación de revocación se realiza, se incrusta en la firma. El valor predeterminado es `false`.
   * Un `OCSPOptionSpec` objeto que almacena preferencias para la compatibilidad con el Protocolo de estado de certificado en línea (OCSP). Si no se realiza la comprobación de revocación, no se usa este parámetro y puede especificar `null`. Para obtener información sobre este objeto, consulte [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `CRLPreferences` objeto que almacena las preferencias de lista de revocación de certificados (CRL). Si no se realiza la comprobación de revocación, no se usa este parámetro y puede especificar `null`.
   * A `TSPPreferences` objeto que almacena las preferencias de compatibilidad con el proveedor de marcas de hora (TSP). Este parámetro es opcional y puede ser `null`.

   La variable `sign` el método devuelve un `BLOB` que representa el documento PDF firmado.

1. Guardar el documento del PDF firmado

   * Cree un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento del PDF firmado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto devuelto por el `sign` método. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` miembro de datos.
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Firma digital de documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Firma digital de Forms interactivo {#digitally-signing-interactive-forms}

Puede firmar un formulario interactivo que crea el servicio de Forms. Por ejemplo, considere el siguiente flujo de trabajo:

* Se combina un formulario de PDF basado en XFA creado mediante Designer y datos de formulario ubicados en un documento XML utilizando el servicio Forms. El servidor de Forms procesa un formulario interactivo.
* El formulario interactivo se firma mediante la API del servicio de firma.

El resultado es un formulario de PDF interactivo con firma digital. Al firmar un formulario de PDF basado en un formulario XFA, asegúrese de guardar el archivo de PDF como un formulario de PDF estático de Adobe. Si intenta firmar un formulario de PDF guardado como formulario de PDF dinámico de Adobe, se producirá una excepción. Como está firmando el formulario que devuelve el servicio Forms, asegúrese de que el formulario contenga un campo de firma.

>[!NOTE]
>
>Para poder firmar digitalmente un formulario interactivo, debe asegurarse de agregar el certificado a AEM Forms. Se agrega un certificado mediante la consola de administración o mediante programación mediante la API del administrador de confianza. (Consulte [Importación de credenciales mediante la API del administrador de confianza](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

Al utilizar la API de servicio de Forms, establezca la variable `GenerateServerAppearance` opción de tiempo de ejecución a `true`. Esta opción en tiempo de ejecución garantiza que el aspecto del formulario generado en el servidor sea válido cuando se abra en Acrobat o Adobe Reader. Se recomienda definir esta opción en tiempo de ejecución al generar un formulario interactivo para firmar con la API de Forms.

>[!NOTE]
>
>Antes de leer Digitally Signing Interactive Forms, se recomienda que esté familiarizado con la firma de documentos PDF. (Consulte [Firma digital de documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

### Resumen de los pasos {#summary_of_steps-4}

Para firmar digitalmente un formulario interactivo que devuelve el servicio de Forms, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de Forms y firmas.
1. Obtenga el formulario interactivo mediante el servicio de Forms.
1. Firme el formulario interactivo.
1. Guarde el documento de PDF firmado como archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de Forms y firmas**

Dado que este flujo de trabajo invoca Forms y los servicios de firma, cree un cliente de servicio de Forms y un cliente de servicio de firma.

**Obtener el formulario interactivo mediante el servicio Forms**

Puede utilizar el servicio de Forms para obtener el formulario de PDF interactivo que desea firmar. Desde AEM Forms, puede pasar un `com.adobe.idp.Document` al servicio de Forms que contiene el formulario que se va a procesar. El nombre de este método es `renderPDFForm2`. Este método devuelve un `com.adobe.idp.Document` objeto que contiene el formulario que se va a firmar. Puede pasar esto `com.adobe.idp.Document` al servicio de firma.

Del mismo modo, si utiliza servicios web, puede pasar la variable `BLOB` instancia que el servicio Forms devuelve al servicio Signature.

>[!NOTE]
>
>El inicio rápido asociado con la sección Forms interactivo de firma digital invoca la variable `renderPDFForm2` método.

**Firmar el formulario interactivo**

Al firmar un documento de PDF, puede establecer las opciones de tiempo de ejecución que utiliza el servicio Signature. Puede establecer las siguientes opciones:

* Opciones de aspecto
* Comprobación de revocación
* Valores de marca de hora

Las opciones de aspecto se configuran mediante una `PDFSignatureAppearanceOptionSpec` objeto. Por ejemplo, puede mostrar la fecha dentro de una firma invocando la variable `PDFSignatureAppearanceOptionSpec` del objeto `setShowDate` método y paso `true`.

**Guardar el documento del PDF firmado**

Una vez que el servicio de firma firme digitalmente el documento del PDF, puede guardarlo como archivo del PDF. El archivo PDF se puede abrir en Acrobat o Adobe Reader.

**Consulte también lo siguiente**

[Firmar digitalmente un formulario interactivo mediante la API de Java](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[Firmar digitalmente un formulario interactivo mediante la API de servicio web](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Firma digital de documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Renderización de PDF forms interactivos](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### Firmar digitalmente un formulario interactivo mediante la API de Java {#digitally-sign-an-interactive-form-using-the-java-api}

Firme digitalmente un formulario interactivo utilizando Forms y la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-signatures-client.jar y adobe-forms-client.jar, en la ruta de clase de su proyecto Java.

1. Crear un cliente de Forms y firmas

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `SignatureServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.
   * Cree un `FormsServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtener el formulario interactivo mediante el servicio Forms

   * Cree un `java.io.FileInputStream` objeto que representa el documento de PDF que se va a pasar al servicio de Forms mediante su constructor. Pase un valor de cadena que especifique la ubicación del documento del PDF.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.
   * Cree un `java.io.FileInputStream` objeto que representa el documento XML que contiene los datos de formulario que se van a pasar al servicio Forms utilizando su constructor. Pase un valor de cadena que especifique la ubicación del archivo XML.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.
   * Cree un `PDFFormRenderSpec` objeto que se utiliza para definir las opciones de tiempo de ejecución. Invocar el `PDFFormRenderSpec` del objeto `setGenerateServerAppearance` método y pase `true`.
   * Invocar el `FormsServiceClient` del objeto `renderPDFForm2` y pase los siguientes valores:

      * A `com.adobe.idp.Document` objeto que contiene el formulario de PDF que se va a procesar.
      * A `com.adobe.idp.Document` objeto que contiene datos para combinar con el formulario.
      * A `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución.
      * A `URLSpec` que contiene valores de URI necesarios para el servicio Forms. Puede especificar `null` para este valor de parámetro.
      * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

      La variable `renderPDFForm2` el método devuelve un `FormsResult` objeto que contiene una secuencia de datos de formulario

   * Recupere el formulario del PDF invocando la variable `FormsResult` del objeto `getOutputContent` método. Este método devuelve un `com.adobe.idp.Document` objeto que representa el formulario interactivo.


1. Firmar el formulario interactivo

   Firme el documento del PDF invocando la variable `SignatureServiceClient` del objeto `sign` y pasando los siguientes valores:

   * A `com.adobe.idp.Document` que representa el documento PDF que se va a firmar. Asegúrese de que este objeto sea el `com.adobe.idp.Document` objeto obtenido del servicio Forms.
   * Valor de cadena que representa el nombre del campo de firma que se firma.
   * A `Credential` objeto que representa la credencial que se utiliza para firmar digitalmente el documento del PDF. Cree un `Credential` invocando el objeto `Credential` estático del objeto `getInstance` método. Pase un valor de cadena que especifique el valor de alias que corresponde a la credencial de seguridad.
   * A `HashAlgorithm` objeto que especifica un miembro de datos estático que representa el algoritmo hash que se va a usar para resumir el documento del PDF. Por ejemplo, puede especificar `HashAlgorithm.SHA1` para usar el algoritmo SHA1.
   * Un valor de cadena que representa el motivo por el que el documento del PDF se firmó digitalmente.
   * Valor de cadena que representa la información de contacto del firmante.
   * A `PDFSignatureAppearanceOptions` que controla el aspecto de la firma digital. Por ejemplo, puede utilizar este objeto para agregar un logotipo personalizado a una firma digital.
   * A `java.lang.Boolean` objeto que especifica si se realizará la comprobación de revocación en el certificado del firmante.
   * Un `OCSPPreferences` objeto que almacena preferencias para la compatibilidad con el Protocolo de estado de certificado en línea (OCSP). Si no se realiza la comprobación de revocación, no se usa este parámetro y puede especificar `null`.
   * A `CRLPreferences` objeto que almacena las preferencias de lista de revocación de certificados (CRL). Si no se realiza la comprobación de revocación, no se usa este parámetro y puede especificar `null`.
   * A `TSPPreferences` objeto que almacena las preferencias de compatibilidad con el proveedor de marcas de hora (TSP). Este parámetro es opcional y puede ser `null`.

   La variable `sign` el método devuelve un `com.adobe.idp.Document` que representa el documento PDF firmado.

1. Guardar el documento del PDF firmado

   * Cree un `java.io.File` y asegúrese de que la extensión de nombre de archivo es .pdf.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` método y pase `java.io.File`para copiar el contenido del `Document` al archivo. Asegúrese de usar la variable `com.adobe.idp.Document` que la variable `sign` método devuelto.

**Consulte también lo siguiente**

[Firma digital de Forms interactivo](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Inicio rápido (modo SOAP): Firma digital de un documento de PDF mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Firmar digitalmente un formulario interactivo mediante la API de servicio web {#digitally-sign-an-interactive-form-using-the-web-service-api}

Firme digitalmente un formulario interactivo utilizando la API de Forms y Firma (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Dado que esta aplicación cliente invoca dos servicios de AEM Forms, cree dos referencias de servicio. Utilice la siguiente definición WSDL para la referencia de servicio asociada al servicio de firma: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   Utilice la siguiente definición WSDL para la referencia de servicio asociada al servicio Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Porque la variable `BLOB` el tipo de datos es común a ambas referencias de servicio; califique completamente la variable `BLOB` tipo de datos al utilizarla. En el inicio rápido correspondiente del servicio web, todas las `BLOB` las instancias están completamente cualificadas.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Crear un cliente de Forms y firmas

   * Cree un `SignatureServiceClient` usando su constructor predeterminado.
   * Cree un `SignatureServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `SignatureServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Repita estos pasos para el cliente de servicio de Forms.

1. Obtener el formulario interactivo mediante el servicio Forms

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar un documento de PDF firmado.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF que se va a firmar y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` propiedad del contenido de la matriz de bytes.
   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar datos de formulario.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo XML que contiene los datos del formulario y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` propiedad del contenido de la matriz de bytes.
   * Cree un `PDFFormRenderSpec` objeto que se utiliza para definir las opciones de tiempo de ejecución. Asignar el valor `true` a `PDFFormRenderSpec` del objeto `generateServerAppearance` campo .
   * Invocar el `FormsServiceClient` del objeto `renderPDFForm2` y pase los siguientes valores:

      * A `BLOB` objeto que contiene el formulario de PDF que se va a procesar.
      * A `BLOB` objeto que contiene datos para combinar con el formulario.
      * A `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución.
      * A `URLSpec` que contiene valores de URI necesarios para el servicio Forms. Puede especificar `null` para este valor de parámetro.
      * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
      * Parámetro de salida largo utilizado para almacenar el número de páginas en el formulario.
      * Un parámetro de salida de cadena que se utiliza para el valor de configuración regional.
      * A `FormResult` que es un parámetro de salida que se utiliza para almacenar el formulario interactivo.
   * Recupere el formulario del PDF invocando la variable `FormsResult` del objeto `outputContent` campo . Este campo almacena un `BLOB` objeto que representa el formulario interactivo.


1. Firmar el formulario interactivo

   Firme el documento del PDF invocando la variable `SignatureServiceClient` del objeto `sign` y pasando los siguientes valores:

   * A `BLOB` que representa el documento PDF que se va a firmar. Utilice la variable `BLOB` instancia devuelta por el servicio de Forms.
   * Valor de cadena que representa el nombre del campo de firma que se firma.
   * A `Credential` objeto que representa la credencial que se utiliza para firmar digitalmente el documento del PDF. Cree un `Credential` utilizando su constructor y especifique el alias asignando un valor al `Credential` del objeto `alias` propiedad.
   * A `HashAlgorithm` objeto que especifica un miembro de datos estático que representa el algoritmo hash que se va a usar para resumir el documento del PDF. Por ejemplo, puede especificar `HashAlgorithm.SHA1` para usar el algoritmo SHA1.
   * Un valor booleano que especifica si se utiliza el algoritmo hash.
   * Un valor de cadena que representa el motivo por el que el documento del PDF se firmó digitalmente.
   * Valor de cadena que representa la ubicación del firmante.
   * Valor de cadena que representa la información de contacto del firmante.
   * A `PDFSignatureAppearanceOptions` que controla el aspecto de la firma digital. Por ejemplo, puede utilizar este objeto para agregar un logotipo personalizado a una firma digital.
   * A `System.Boolean` objeto que especifica si se realizará la comprobación de revocación en el certificado del firmante. Si esta comprobación de revocación se realiza, se incrusta en la firma. El valor predeterminado es `false`.
   * Un `OCSPPreferences` objeto que almacena preferencias para la compatibilidad con el Protocolo de estado de certificado en línea (OCSP). Si no se realiza la comprobación de revocación, no se usa este parámetro y puede especificar `null`. Para obtener información sobre este objeto, consulte [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `CRLPreferences` objeto que almacena las preferencias de lista de revocación de certificados (CRL). Si no se realiza la comprobación de revocación, no se usa este parámetro y puede especificar `null`.
   * A `TSPPreferences` objeto que almacena las preferencias de compatibilidad con el proveedor de marcas de hora (TSP). Este parámetro es opcional y puede ser `null`.

   La variable `sign` el método devuelve un `BLOB` que representa el documento PDF firmado.

1. Guardar el documento del PDF firmado

   * Cree un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento del PDF firmado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto devuelto por el `sign` método. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` miembro de datos.
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Firma digital de Forms interactivo](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Certificación de documentos del PDF {#certifying-pdf-documents}

Puede proteger un documento PDF certificándolo con un tipo concreto de firma denominada firma certificada. Una firma certificada se distingue de una firma digital de las siguientes maneras:

* Debe ser la primera firma aplicada al documento PDF; es decir, en el momento en que se aplica la firma certificada, cualquier otro campo de firma del documento debe estar sin firmar. Sólo se permite una firma certificada en un documento de PDF. Si desea firmar y certificar un documento de PDF, debe certificarlo antes de firmarlo. Después de certificar un documento de PDF, puede firmar digitalmente campos de firma adicionales.
* El autor o el creador del documento pueden especificar que el documento se puede modificar de determinadas formas sin invalidar la firma certificada. Por ejemplo, el documento puede permitir rellenar formularios o hacer comentarios. Si el autor especifica que no se permite una modificación determinada, Acrobat impide que los usuarios modifiquen el documento de esa manera. Si se realizan dichas modificaciones, como por ejemplo utilizando otra aplicación, la firma certificada no es válida y Acrobat emite una advertencia cuando un usuario abre el documento. (Con las firmas no certificadas, no se evitan las modificaciones y las operaciones de edición normales no invalidan la firma original).
* En el momento de la firma, el documento se analiza para detectar tipos específicos de contenido que puedan hacer que el contenido de un documento sea ambiguo o engañoso. Por ejemplo, una anotación podría oscurecer algún texto de una página que sea importante para comprender qué se está certificando. Se puede proporcionar una explicación (autenticación legal) sobre dicho contenido.

Puede certificar mediante programación documentos de PDF mediante la API de Java del servicio de firmas o la API del servicio web de firmas. Al certificar un documento de PDF, debe hacer referencia a una credencial de seguridad que existe en el servicio Credencial. Para obtener información sobre las credenciales de seguridad, consulte la *Instalación e implementación de AEM Forms* para su servidor de aplicaciones.

>[!NOTE]
>
>Al certificar y firmar el mismo documento de PDF, si la firma del certificado no es de confianza, aparece un triángulo amarillo junto a la primera firma de signo al abrir el documento de PDF en Acrobat o Adobe Reader. Debe confiarse en la firma certificadora para evitar esta situación.

>[!NOTE]
>
>Cuando se utiliza una credencial nCipher nShield HSM para firmar o certificar un documento PDF, no se puede utilizar la nueva credencial hasta que se reinicie el servidor de aplicaciones J2EE en el que se implementa AEM Forms. Sin embargo, puede establecer un valor de configuración, lo que da como resultado que la operación de firma o certificación funcione sin reiniciar el servidor de aplicaciones J2EE.

Puede añadir el siguiente valor de configuración en el archivo cknfastrc, que se encuentra en /opt/nfast/cknfastrc (o c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Después de agregar este valor de configuración al archivo cknfastrc, la nueva credencial se puede usar sin reiniciar el servidor de aplicaciones J2EE.

>[!NOTE]
>
>Para obtener más información sobre el servicio Signature y la certificación de un documento, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-5}

Para certificar un documento de PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de firma.
1. Obtenga el documento del PDF para certificarlo.
1. Certifique el documento del PDF.
1. Guarde el documento de PDF certificado como archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de firma**

Para poder realizar una operación de firma mediante programación, debe crear un cliente de firma.

**Obtener el documento del PDF para certificar**

Para certificar un documento de PDF, debe obtener un documento de PDF que contenga un campo de firma. Si un documento PDF no contiene un campo de firma, no se puede certificar. Se puede agregar un campo de firma mediante Designer o mediante programación. Para obtener información sobre cómo agregar un campo de firma mediante programación, consulte [Adición de campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields).

**Certificar el documento del PDF**

Para certificar correctamente un documento de PDF, se requieren los siguientes valores de entrada que utiliza el servicio Signature para certificar un documento de PDF:

* **documento del PDF**: Documento de PDF que contiene un campo de firma, que es un campo de formulario que contiene una representación gráfica de la firma certificada. Un documento PDF debe contener un campo de firma para poder certificarlo. Se puede agregar un campo de firma mediante Designer o mediante programación. (Consulte [Adición de campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields).)
* **Nombre del campo de firma**: El nombre completo del campo de firma certificado. El siguiente valor es un ejemplo: `form1[0].#subform[1].SignatureField3[3]`. Al utilizar un campo de formulario XFA, también se puede utilizar el nombre parcial del campo de firma: `SignatureField3[3]`. Si se pasa un valor nulo para el nombre del campo, se crea y certifica dinámicamente un campo de firma invisible.
* **Credenciales de seguridad**: Credencial que se utiliza para certificar el documento del PDF. Esta credencial de seguridad contiene una contraseña y un alias, que deben coincidir con un alias que aparezca en la credencial que se encuentra dentro del servicio Credential. El alias es una referencia a una credencial real que puede estar en un archivo PKCS#12 (con extensión .pfx) o en un módulo de seguridad de hardware (HSM).
* **Algoritmo de hash**: Algoritmo hash que se debe usar para resumir el documento del PDF.
* **Motivo de la firma**: Valor que se muestra en Acrobat o Adobe Reader para que otros usuarios sepan el motivo por el que el documento del PDF se certificó.
* **Ubicación del firmante**: La ubicación del firmante especificada por la credencial.
* **Información de contacto**: Información de contacto, como la dirección y el número de teléfono del firmante.
* **Información de permisos**: Permisos que controlan las acciones que un usuario final puede realizar en un documento sin que la firma certificada no sea válida. Por ejemplo, puede establecer el permiso para que cualquier cambio en el documento del PDF haga que la firma certificada no sea válida.
* **Explicación legal**: Cuando un documento está certificado, se analiza automáticamente para detectar tipos específicos de contenido que podrían hacer que el contenido de un documento sea ambiguo o engañoso. Por ejemplo, una anotación podría oscurecer algún texto de una página que sea importante para comprender qué se está certificando. El proceso de digitalización genera advertencias sobre estos tipos de contenido. Este valor proporciona una explicación adicional del contenido que puede haber generado advertencias.
* **Opciones de aspecto**: Opciones que controlan el aspecto de la firma certificada. Por ejemplo, la firma certificada puede mostrar información de fecha.
* **Comprobación de revocación**: Este valor especifica si la comprobación de revocación se realiza para el certificado del firmante. La configuración predeterminada de `false` significa que la comprobación de revocación no se ha realizado.
* **Configuración de OCSP**: Configuración de la compatibilidad con el Protocolo de estado de certificado en línea (OCSP), que proporciona información sobre el estado de las credenciales que se usan para certificar el documento del PDF. Por ejemplo, puede especificar la dirección URL del servidor que proporciona información sobre las credenciales que utiliza para iniciar sesión en el documento del PDF.
* **Configuración de CRL**: Configuración de las preferencias de la lista de revocación de certificados (CRL) si se ha realizado la comprobación de revocación. Por ejemplo, puede especificar que siempre verifique si se revocó una credencial.
* **Marca de tiempo**: Configuración que define la información de marca de hora que se aplica a la firma certificada. Una marca de hora indica que se establecieron datos específicos antes de un tiempo determinado. Este conocimiento ayuda a construir una relación de confianza entre el firmante y el verificador.

**Guarde el documento de PDF certificado como archivo de PDF**

Una vez que el servicio de firma certifica el documento de PDF, puede guardarlo como archivo de PDF para que los usuarios puedan abrirlo en Acrobat o Adobe Reader.

**Consulte también lo siguiente**

[Certificar documentos del PDF mediante la API de Java](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[Certificar documentos del PDF mediante la API de servicio web](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adición de campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields)

### Certificar documentos del PDF mediante la API de Java {#certify-pdf-documents-using-the-java-api}

Certificar un documento de PDF mediante la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-signatures-client.jar, en la ruta de clase de su proyecto Java.

1. Crear un cliente de firma

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `SignatureServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtener el documento del PDF para certificar

   * Cree un `java.io.FileInputStream` objeto que representa el documento de PDF que se va a certificar utilizando su constructor y pasando un valor de cadena que especifica la ubicación del documento de PDF.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Certificar el documento del PDF

   Certifique el documento del PDF invocando la variable `SignatureServiceClient` del objeto `certify` y pasando los siguientes valores:

   * La variable `com.adobe.idp.Document` que representa el documento del PDF que se va a certificar.
   * Un valor de cadena que representa el nombre del campo de firma que contendrá la firma.
   * A `Credential` que representa la credencial que se utiliza para certificar el documento del PDF. Cree un `Credential` invocando el objeto `Credential` estático del objeto `getInstance` y pasando un valor de cadena que especifica el valor de alias que corresponde a la credencial de seguridad.
   * A `HashAlgorithm` objeto que especifica un miembro de datos estático que representa el algoritmo hash utilizado para resumir el documento del PDF. Por ejemplo, puede especificar `HashAlgorithm.SHA1` para usar el algoritmo SHA1.
   * Un valor de cadena que representa el motivo por el que el documento de PDF está certificado.
   * Valor de cadena que representa la información de contacto del firmante.
   * A `MDPPermissions` objeto que especifica las acciones que se pueden realizar en el documento del PDF que invalida la firma.
   * A `PDFSignatureAppearanceOptions` que controla el aspecto de la firma certificada. Si lo desea, modifique el aspecto de la firma invocando un método como `setShowDate`.
   * Valor de cadena que proporciona una explicación de las acciones que invalidan la firma.
   * A `java.lang.Boolean` objeto que especifica si se realizará la comprobación de revocación en el certificado del firmante. Si esta comprobación de revocación se realiza, se incrusta en la firma. El valor predeterminado es `false`.
   * A `java.lang.Boolean` objeto que especifica si el campo de firma que se va a certificar está bloqueado. Si el campo está bloqueado, el campo de firma está marcado como de solo lectura, sus propiedades no se pueden modificar y nadie que no tenga los permisos necesarios no puede borrarlo. El valor predeterminado es `false`.
   * Un `OCSPPreferences` objeto que almacena preferencias para la compatibilidad con el Protocolo de estado de certificado en línea (OCSP). Si no se realiza la comprobación de revocación, no se usa este parámetro y puede especificar `null`. Para obtener información sobre este objeto, consulte [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `CRLPreferences` objeto que almacena las preferencias de lista de revocación de certificados (CRL). Si no se realiza la comprobación de revocación, no se usa este parámetro y puede especificar `null`.
   * A `TSPPreferences` objeto que almacena las preferencias de compatibilidad con el proveedor de marcas de hora (TSP). Por ejemplo, después de crear un `TSPPreferences` , puede establecer la dirección URL del servidor TSP invocando la variable `TSPPreferences` del objeto `setTspServerURL` método. Este parámetro es opcional y puede ser `null`. Para obtener más información, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

   La variable `certify` el método devuelve un `com.adobe.idp.Document` objeto que representa el documento de PDF certificado.

1. Guarde el documento de PDF certificado como archivo de PDF

   * Cree un `java.io.File` y asegúrese de que la extensión de archivo es .pdf.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `com.adobe.idp.Document` al archivo.

**Consulte también lo siguiente**

[Certificación de documentos del PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Inicio rápido (modo SOAP): Certificación de un documento de PDF mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Certificar documentos del PDF mediante la API de servicio web {#certify-pdf-documents-using-the-web-service-api}

Certifique un documento del PDF mediante la API de firma (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Crear un cliente de firma

   * Cree un `SignatureServiceClient` usando su constructor predeterminado.
   * Cree un `SignatureServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `SignatureServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtener el documento del PDF para certificar

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar un documento de PDF certificado.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF que se va a certificar y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` miembro de datos el contenido de la matriz de bytes.

1. Certificar el documento del PDF

   Certifique el documento del PDF invocando la variable `SignatureServiceClient` del objeto `certify` y pasando los siguientes valores:

   * La variable `BLOB` que representa el documento del PDF que se va a certificar.
   * Un valor de cadena que representa el nombre del campo de firma que contendrá la firma.
   * A `Credential` que representa la credencial que se utiliza para certificar el documento del PDF. Cree un `Credential` utilizando su constructor y especifique el alias asignando un valor al `Credential` del objeto `alias` propiedad.
   * A `HashAlgorithm` objeto que especifica un miembro de datos estático que representa el algoritmo hash utilizado para resumir el documento del PDF. Por ejemplo, puede especificar `HashAlgorithm.SHA1` para usar el algoritmo SHA1.
   * Un valor booleano que especifica si se utiliza el algoritmo hash.
   * Un valor de cadena que representa el motivo por el que el documento de PDF está certificado.
   * Valor de cadena que representa la ubicación del firmante.
   * Valor de cadena que representa la información de contacto del firmante.
   * Un `MDPPermissions` miembro de datos estáticos del objeto que especifica las acciones que se pueden realizar en el documento del PDF que invalidan la firma.
   * Un valor booleano que especifica si se utiliza la variable `MDPPermissions` objeto que se pasó como el valor del parámetro anterior.
   * Un valor de cadena que explica qué acciones invalidan la firma.
   * A `PDFSignatureAppearanceOptions` que controla el aspecto de la firma certificada. Cree un `PDFSignatureAppearanceOptions` usando su constructor. Puede modificar el aspecto de la firma estableciendo uno de sus miembros de datos.
   * A `System.Boolean` objeto que especifica si se realizará la comprobación de revocación en el certificado del firmante. Si esta comprobación de revocación se realiza, se incrusta en la firma. El valor predeterminado es `false`.
   * A `System.Boolean` objeto que especifica si el campo de firma que se va a certificar está bloqueado. Si el campo está bloqueado, el campo de firma está marcado como de solo lectura, sus propiedades no se pueden modificar y nadie que no tenga los permisos necesarios no puede borrarlo. El valor predeterminado es `false`.
   * A `System.Boolean` objeto que especifica si el campo de firma está bloqueado. Es decir, si pasa `true` al parámetro anterior y, a continuación, pase `true` a este parámetro.
   * Un `OCSPPreferences` objeto que almacena preferencias para la compatibilidad con el Protocolo de estado de certificado en línea (OCSP), que proporciona información sobre el estado de la credencial que se utiliza para certificar el documento de PDF. Si no se realiza la comprobación de revocación, no se usa este parámetro y puede especificar `null`.
   * A `CRLPreferences` objeto que almacena las preferencias de lista de revocación de certificados (CRL). Si no se realiza la comprobación de revocación, no se usa este parámetro y puede especificar `null`.
   * A `TSPPreferences` objeto que almacena las preferencias de compatibilidad con el proveedor de marcas de hora (TSP). Por ejemplo, después de crear un `TSPPreferences` , puede establecer la dirección URL del TSP estableciendo la variable `TSPPreferences` del objeto `tspServerURL` miembro de datos. Este parámetro es opcional y puede ser `null`.

   La variable `certify` el método devuelve un `BLOB` objeto que representa el documento de PDF certificado.

1. Guarde el documento de PDF certificado como archivo de PDF

   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF que contendrá el documento PDF certificado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto devuelto por el `certify` método. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `binaryData` miembro de datos.
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Certificación de documentos del PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verificación de firmas digitales {#verifying-digital-signatures}

Las firmas digitales se pueden comprobar para garantizar que no se haya modificado un documento PDF firmado y que la firma digital sea válida. Al verificar una firma digital, puede comprobar el estado de la firma y las propiedades de la firma, como la identidad del firmante. Antes de confiar en una firma digital, se recomienda verificarla. Al verificar una firma digital, haga referencia a un documento de PDF que contenga una firma digital.

Supongamos que se desconoce la identidad del firmante. Cuando abre el documento del PDF en Acrobat, un mensaje de advertencia indica que la identidad del firmante es desconocida, como se muestra en la siguiente ilustración.

![vd_vd_verifysig](assets/vd_vd_verifysig.png)

Del mismo modo, al verificar mediante programación una firma digital, puede determinar el estado de la identidad del firmante. Por ejemplo, si verifica la firma digital en el documento mostrado en la ilustración anterior, el resultado sería que la identidad del firmante es desconocida.

>[!NOTE]
>
>Para obtener más información sobre el servicio Signature y la verificación de firmas digitales, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-6}

Para verificar una firma digital, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de firma.
1. Obtenga el documento del PDF que contiene la firma que desea verificar.
1. Establezca las opciones de tiempo de ejecución de PKI.
1. Compruebe la firma digital.
1. Determine el estado de la firma.
1. Determine la identidad del firmante.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de firma**

Antes de realizar una operación de servicio de firma mediante programación, cree un cliente de servicio de firma.

**Obtener el documento del PDF que contiene la firma para comprobar**

Para comprobar una firma utilizada para firmar o certificar digitalmente un documento PDF, obtenga un documento PDF que contenga una firma.

**Configurar las opciones de tiempo de ejecución de PKI**

Establezca estas opciones en tiempo de ejecución de PKI que utiliza el servicio de firmas al verificar firmas en un documento de PDF:

* Hora de la verificación
* Comprobación de revocación
* Valores de marca de hora

Como parte de la configuración de estas opciones, puede especificar el tiempo de verificación. Por ejemplo, puede seleccionar la hora actual (la hora en el equipo del validador), que indica que se debe utilizar la hora actual. Para obtener información sobre los distintos valores de tiempo, consulte la `VerificationTime` valor de enumeración en [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

También puede especificar si desea realizar la comprobación de revocación como parte del proceso de verificación. Por ejemplo, puede realizar una comprobación de revocación para determinar si el certificado está revocado. Para obtener información sobre las opciones de comprobación de revocación, consulte la `RevocationCheckStyle` valor de enumeración en [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Para realizar la comprobación de revocación en un certificado, especifique una URL para un servidor de lista de revocación de certificados (CRL) utilizando un `CRLOptionSpec` objeto. Sin embargo, si no especifica una URL para el servidor CRL, el servicio de firma obtiene la URL del certificado.

En lugar de utilizar un servidor CRL, puede utilizar un servidor de protocolo de estado de certificado en línea (OCSP) al realizar la comprobación de revocación. Normalmente, cuando se utiliza un servidor OCSP en lugar de un servidor CRL, la comprobación de revocación se realiza más rápido. (Consulte [Protocolo de estado de certificado en línea](https://tools.ietf.org/html/rfc2560).)

Puede establecer el orden del servidor CRL y OCSP que utiliza el servicio de firmas mediante el uso de Aplicaciones y Servicios de Adobe. Por ejemplo, si el servidor OCSP se configura primero en Aplicaciones y Servicios de Adobe, se comprueba el servidor OCSP, seguido del servidor CRL.

Si no realiza la comprobación de revocación, el servicio de firma no comprueba si el certificado está revocado. Es decir, se ignora la información del servidor CRL y OCSP.

>[!NOTE]
>
>Puede anular la dirección URL especificada en el certificado utilizando una `CRLOptionSpec` y `OCSPOptionSpec` objeto. Por ejemplo, para anular el servidor CRL, puede invocar la variable `CRLOptionSpec` del objeto `setLocalURI` método.

La marca de hora es el proceso de seguimiento del momento en que se modificó un documento firmado o certificado. Después de firmar un documento, nadie puede modificarlo. La marca de hora ayuda a hacer cumplir la validez de un documento firmado o certificado. Puede establecer las opciones de marca de hora mediante un `TSPOptionSpec` objeto. Por ejemplo, puede especificar la URL de un servidor de proveedor de marca de hora (TSP).

>[!NOTE]
>
>En los inicios rápidos del servicio web y Java, el tiempo de verificación se establece en `VerificationTime.CURRENT_TIME` y la comprobación de revocación está configurada en `RevocationCheckStyle.BestEffort`. Dado que no se especifica ninguna CRL ni información del servidor OCSP, la información del servidor se obtiene del certificado.

**Verificar la firma digital**

Para verificar correctamente una firma, especifique el nombre completo del campo de firma que contiene la firma, como `form1[0].#subform[1].SignatureField3[3]`. Al utilizar un campo de formulario XFA, también puede utilizar el nombre parcial del campo de firma : `SignatureField3`.

De forma predeterminada, el servicio de firma limita la cantidad de tiempo que se puede firmar un documento después del tiempo de validación a 65 minutos. Si un usuario intenta verificar una firma en el momento actual y la hora de firma es posterior a la hora actual y está dentro de los 65 minutos, el servicio de firma no crea un error de verificación.

>[!NOTE]
>
>Para ver otros valores que necesita para verificar una firma, consulte [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Determinar el estado de la firma**

Como parte de la verificación de una firma digital, puede comprobar el estado de la firma.

**Determinar la identidad del firmante**

Puede determinar la identidad del firmante, que puede ser uno de los siguientes valores:

* **Unknown**: Este firmante es desconocido porque no se puede realizar la verificación del firmante.
* **De confianza**: Este firmante es de confianza.
* **No confiable**: Este firmante no es de confianza.

**Consulte también lo siguiente**

[Verificación de firmas digitales mediante la API de Java](#verify-digital-signatures-using-the-java-api)

[Verificación de firmas digitales mediante la API de servicio web](#verify-digital-signatures-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificación de firmas digitales mediante la API de Java {#verify-digital-signatures-using-the-java-api}

Compruebe una firma digital utilizando la API del servicio de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-signatures-client.jar, en la ruta de clase de su proyecto Java.

1. Crear un cliente de firma

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `SignatureServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtener el documento del PDF que contiene la firma para comprobar

   * Cree un `java.io.FileInputStream` objeto que representa el documento de PDF que contiene la firma que se va a comprobar utilizando su constructor. Pase un valor de cadena que especifique la ubicación del documento del PDF.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Configurar las opciones de tiempo de ejecución de PKI

   * Cree un `PKIOptions` usando su constructor.
   * Establezca el tiempo de verificación invocando la variable `PKIOptions` del objeto `setVerificationTime` método y pasar una `VerificationTime` valor de enumeración que especifica el tiempo de verificación.
   * Establezca la opción de comprobación de revocación invocando `PKIOptions` del objeto `setRevocationCheckStyle` método y pasar una `RevocationCheckStyle` valor de enumeración que especifica si se realizará la comprobación de revocación.

1. Verificar la firma digital

   Compruebe la firma invocando la variable `SignatureServiceClient` del objeto `verify2` y pasando los siguientes valores:

   * A `com.adobe.idp.Document` objeto que contiene un documento PDF certificado o firmado digitalmente.
   * Valor de cadena que representa el nombre del campo de firma que contiene la firma que se va a verificar.
   * A `PKIOptions` que contiene opciones de tiempo de ejecución PKI.
   * A `VerifySPIOptions` instancia que contiene información de SPI. Puede especificar `null` para este parámetro.

   La variable `verify2` el método devuelve un `PDFSignatureVerificationInfo` objeto que contiene información que se puede utilizar para verificar la firma digital.

1. Determinar el estado de la firma

   * Determine el estado de la firma invocando la variable `PDFSignatureVerificationInfo` del objeto `getStatus` método. Este método devuelve un `SignatureStatus` objeto que especifica el estado de firma. Por ejemplo, si no se modifica un documento de PDF firmado, este método devuelve `SignatureStatus.DocumentSigNoChanges`.

1. Determinar la identidad del firmante

   * Determine la identidad del firmante invocando la variable `PDFSignatureVerificationInfo` del objeto `getSigner` método. Este método devuelve un `IdentityInformation` objeto.
   * Invocar el `IdentityInformation` del objeto `getStatus` para determinar la identidad del firmante. Este método devuelve un `IdentityStatus` valor de enumeración que especifica la identidad. Por ejemplo, si el firmante es de confianza, este método devuelve `IdentityStatus.TRUSTED`.

**Consulte también lo siguiente**

[Verificación de firmas digitales](#verify-digital-signatures-using-the-java-api)

[Inicio rápido (modo SOAP): Verificación de una firma digital mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificación de firmas digitales mediante la API de servicio web {#verify-digital-signatures-using-the-web-service-api}

Compruebe una firma digital utilizando la API del servicio de firma (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Crear un cliente de firma

   * Cree un `SignatureServiceClient` usando su constructor predeterminado.
   * Cree un `SignatureServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `SignatureServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtener el documento del PDF que contiene la firma para comprobar

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar un documento de PDF que contiene una firma digital o certificada que se debe verificar.
   * Cree un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento del PDF firmado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` método. Pase la matriz de bytes, la posición de inicio y la longitud del flujo para leerlos.
   * Rellene el `BLOB` asignando su `MTOM` propiedad del contenido de la matriz de bytes.

1. Configurar las opciones de tiempo de ejecución de PKI

   * Cree un `PKIOptions` usando su constructor.
   * Configure la hora de verificación asignando la variable `PKIOptions` del objeto `verificationTime` miembro de datos a `VerificationTime` valor de enumeración que especifica el tiempo de verificación.
   * Establezca la opción de comprobación de revocación asignando la variable `PKIOptions` del objeto `revocationCheckStyle` miembro de datos a `RevocationCheckStyle` valor de enumeración que especifica si se realizará la comprobación de revocación.

1. Verificar la firma digital

   Compruebe la firma invocando la variable `SignatureServiceClient` del objeto `verify2` y pasando los siguientes valores:

   * La variable `BLOB` objeto que contiene un documento PDF certificado o firmado digitalmente.
   * Valor de cadena que representa el nombre del campo de firma que contiene la firma que se va a verificar.
   * A `PKIOptions` que contiene opciones de tiempo de ejecución PKI.
   * A `VerifySPIOptions` instancia que contiene información de SPI. Puede especificar `null` para este parámetro.

   La variable `verify2` el método devuelve un `PDFSignatureVerificationInfo` objeto que contiene información que se puede utilizar para verificar la firma digital.

1. Determinar el estado de la firma

   Determine el estado de la firma obteniendo el valor de la variable `PDFSignatureVerificationInfo` del objeto `status` miembro de datos. Este miembro de datos almacena un `SignatureStatus` objeto que especifica el estado de la firma. Por ejemplo, si se modifica un documento de PDF firmado, la variable `status` el miembro de datos almacena el valor `SignatureStatus.DocumentSigNoChanges`.

1. Determinar la identidad del firmante

   * Determine la identidad del firmante recuperando el valor de la variable `PDFSignatureVerificationInfo` del objeto `signer` miembro de datos. Este miembro devuelve un `IdentityInformation` objeto.
   * Recupere el `IdentityInformation` del objeto `status` miembro de datos para determinar la identidad del firmante. Este miembro de datos devuelve un `IdentityStatus` valor de enumeración que especifica la identidad. Por ejemplo, si el firmante es de confianza, este miembro devuelve `IdentityStatus.TRUSTED`.

**Consulte también lo siguiente**

[Verificación de firmas digitales](#verify-digital-signatures-using-the-java-api)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verificación de varias firmas digitales {#verifying-multiple-digital-signatures}

AEM Forms proporciona los medios para verificar todas las firmas digitales que se encuentran en un documento de PDF. Supongamos que un documento de PDF contiene varias firmas digitales como resultado de un proceso empresarial que requiere firmas de varios firmantes. Por ejemplo, considere una transacción financiera que requiera la firma de un agente de préstamos y de un administrador. Puede utilizar la API de Java o la API de servicio web del servicio de firma para comprobar todas las firmas del documento del PDF. Al comprobar varias firmas digitales, puede comprobar el estado y las propiedades de cada firma. Antes de confiar en una firma digital, se recomienda verificarla. Se recomienda que esté familiarizado con la verificación de una sola firma digital.

>[!NOTE]
>
>Para obtener más información sobre el servicio Signature y la verificación de firmas digitales, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-7}

Para verificar varias firmas digitales, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de firma.
1. Obtenga el documento del PDF que contiene las firmas que desea verificar.
1. Establezca las opciones de tiempo de ejecución de PKI.
1. Recupere todas las firmas digitales.
1. Iterar a través de todas las firmas.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de firma**

Antes de realizar una operación de servicio de firma mediante programación, cree un cliente de servicio de firma.

**Obtenga el documento del PDF que contiene las firmas que desea verificar**

Para comprobar una firma utilizada para firmar o certificar digitalmente un documento PDF, obtenga un documento PDF que contenga una firma.

**Establecer opciones de tiempo de ejecución de PKI**

Establezca estas opciones en tiempo de ejecución de PKI que utiliza el servicio de firmas al verificar todas las firmas en un documento de PDF:

* Hora de la verificación
* Comprobación de revocación
* Valores de marca de hora

Como parte de la configuración de estas opciones, puede especificar el tiempo de verificación. Por ejemplo, puede seleccionar la hora actual (la hora en el equipo del validador), que indica que se debe utilizar la hora actual. Para obtener información sobre los distintos valores de tiempo, consulte la `VerificationTime` valor de enumeración en [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

También puede especificar si desea realizar la comprobación de revocación como parte del proceso de verificación. Por ejemplo, puede realizar una comprobación de revocación para determinar si el certificado está revocado. Para obtener información sobre las opciones de comprobación de revocación, consulte la `RevocationCheckStyle` valor de enumeración en [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Para realizar la comprobación de revocación en un certificado, especifique una URL para un servidor de lista de revocación de certificados (CRL) utilizando un `CRLOptionSpec` objeto. Sin embargo, si no especifica una URL a un servidor CRL, el servicio de firmas obtiene la URL del certificado.

En lugar de utilizar un servidor CRL, puede utilizar un servidor de protocolo de estado de certificado en línea (OCSP) al realizar la comprobación de revocación. Normalmente, cuando se utiliza un servidor OCSP en lugar de un servidor CRL, la comprobación de revocación se realiza más rápido. (Consulte [Protocolo de estado de certificado en línea](https://tools.ietf.org/html/rfc2560).)

Puede establecer el orden del servidor CRL y OCSP que utiliza el servicio de firmas mediante el uso de Aplicaciones y Servicios de Adobe. Por ejemplo, si el servidor OCSP se configura primero en Aplicaciones y Servicios de Adobe, el servidor OCSP se marca, seguido del servidor CRL.

Si no realiza la comprobación de revocación, el servicio de firma no comprueba si el certificado está revocado. Es decir, se ignora la información del servidor CRL y OCSP.

>[!NOTE]
>
>Puede anular la dirección URL especificada en el certificado utilizando una `CRLOptionSpec` y `OCSPOptionSpec` objeto. Por ejemplo, para anular el servidor CRL, puede invocar la variable `CRLOptionSpec` del objeto `setLocalURI` método.

La marca de hora es el proceso de seguimiento del momento en que se modificó un documento firmado o certificado. Después de firmar un documento, nadie puede modificarlo. La marca de hora ayuda a hacer cumplir la validez de un documento firmado o certificado. Puede establecer las opciones de marca de hora utilizando un `TSPOptionSpec` objeto. Por ejemplo, puede especificar la URL de un servidor de proveedor de marca de hora (TSP).

>[!NOTE]
>
>En los inicios rápidos del servicio web y Java, el tiempo de verificación se establece en `VerificationTime.CURRENT_TIME` y la comprobación de revocación está configurada en `RevocationCheckStyle.BestEffort`. Dado que no se especifica ninguna CRL ni información del servidor OCSP, la información del servidor se obtiene del certificado.

**Recuperar todas las firmas digitales**

Para comprobar todas las firmas digitales ubicadas en un documento de PDF, recupere las firmas digitales del documento de PDF. Todas las firmas se devuelven en una lista. Como parte de la verificación de una firma digital, compruebe el estado de la firma.

>[!NOTE]
>
>A diferencia de cuando se verifica una sola firma digital, cuando se verifican varias firmas, no es necesario especificar el nombre del campo de firma.

**Iterar a través de todas las firmas**

Iterar a través de cada firma. Es decir, para cada firma, verifique la firma digital y compruebe la identidad del firmante y el estado de cada firma. (Consulte [Verificación de firmas digitales](#verify-digital-signatures-using-the-java-api).)

>[!NOTE]
>
>No es necesario iterar todas las firmas si el requisito es todo el documento.

**Consulte también lo siguiente**

[Verificar varias firmas digitales mediante la API de Java](#verify-digital-signatures-using-the-java-api)

[Verificación de varias firmas digitales mediante la API de servicio web](#verify-digital-signatures-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificar varias firmas digitales mediante la API de Java {#verify-multiple-digital-signatures-using-the-java-api}

Compruebe varias firmas digitales mediante la API del servicio de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-signatures-client.jar, en la ruta de clase de su proyecto Java.

1. Crear un cliente de firma

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `SignatureServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtenga el documento del PDF que contiene las firmas que desea verificar

   * Cree un `java.io.FileInputStream` objeto que representa el documento de PDF que contiene varias firmas digitales que se deben comprobar mediante su constructor. Pase un valor de cadena que especifique la ubicación del documento del PDF.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Establecer opciones de tiempo de ejecución de PKI

   * Cree un `PKIOptions` usando su constructor.
   * Establezca el tiempo de verificación invocando la variable `PKIOptions` del objeto `setVerificationTime` método y pasar una `VerificationTime` valor de enumeración que especifica el tiempo de verificación.
   * Establezca la opción de comprobación de revocación invocando `PKIOptions` del objeto `setRevocationCheckStyle` método y pasar una `RevocationCheckStyle` valor de enumeración que especifica si se realizará la comprobación de revocación.

1. Recuperar todas las firmas digitales

   Invocar el `SignatureServiceClient` del objeto `verifyPDFDocument` y pase los siguientes valores:

   * A `com.adobe.idp.Document` objeto que contiene un documento de PDF que contiene varias firmas digitales.
   * A `PKIOptions` que contiene opciones de tiempo de ejecución PKI.
   * A `VerifySPIOptions` instancia que contiene información de SPI. Puede especificar `null` para este parámetro.

   La variable `verifyPDFDocument` el método devuelve un `PDFDocumentVerificationInfo` objeto que contiene información sobre todas las firmas digitales ubicadas en el documento del PDF.

1. Iterar a través de todas las firmas

   * Interrumpa todas las firmas invocando la variable `PDFDocumentVerificationInfo` del objeto `getVerificationInfos` método. Este método devuelve un `java.util.List` objeto donde cada elemento es un `PDFSignatureVerificationInfo` objeto. Utilice un `java.util.Iterator` para iterar en la lista de firmas.
   * Al usar la variable `PDFSignatureVerificationInfo` , puede realizar tareas como determinar el estado de la firma invocando la variable `PDFSignatureVerificationInfo` del objeto `getStatus` método. Este método devuelve un `SignatureStatus` cuyo miembro de datos estáticos le informa sobre el estado de la firma. Por ejemplo, si la firma es desconocida, este método devuelve `SignatureStatus.DocumentSignatureUnknown`.

**Consulte también lo siguiente**

[Verificación de varias firmas digitales](#verifying-multiple-digital-signatures)

[Inicio rápido (modo SOAP): Verificación de varias firmas digitales mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Verificación de firmas digitales](#verify-digital-signatures-using-the-java-api)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificación de varias firmas digitales mediante la API de servicio web {#verifying-multiple-digital-signatures-using-the-web-service-api}

Compruebe varias firmas digitales mediante la API del servicio de firma (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Crear un cliente de firma

   * Cree un `SignatureServiceClient` usando su constructor predeterminado.
   * Cree un `SignatureServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `SignatureServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento del PDF que contiene las firmas que desea verificar

   * Cree un `BLOB` usando su constructor. La variable `BLOB` almacena un documento de PDF que contiene varias firmas digitales que comprobar.
   * Cree un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento del PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` método. Pase la matriz de bytes, la posición de inicio y la longitud del flujo para leerlos.
   * Rellene el `BLOB` asignando su `MTOM` propiedad del contenido de la matriz de bytes.

1. Establecer opciones de tiempo de ejecución de PKI

   * Cree un `PKIOptions` usando su constructor.
   * Configure la hora de verificación asignando la variable `PKIOptions` del objeto `verificationTime` miembro de datos a `VerificationTime` valor de enumeración que especifica el tiempo de verificación.
   * Establezca la opción de comprobación de revocación asignando la variable `PKIOptions` del objeto `revocationCheckStyle` miembro de datos a `RevocationCheckStyle` valor de enumeración que especifica si se realizará la comprobación de revocación.

1. Recuperar todas las firmas digitales

   Invocar el `SignatureServiceClient` del objeto `verifyPDFDocument` y pase los siguientes valores:

   * A `BLOB` objeto que contiene un documento de PDF que contiene varias firmas digitales.
   * A `PKIOptions` que contiene opciones de tiempo de ejecución PKI.
   * A `VerifySPIOptions` instancia que contiene información de SPI. Puede especificar null para este parámetro.

   La variable `verifyPDFDocument` el método devuelve un `PDFDocumentVerificationInfo` objeto que contiene información sobre todas las firmas digitales ubicadas en el documento del PDF.

1. Iterar a través de todas las firmas

   * Iterar a través de todas las firmas obteniendo el `PDFDocumentVerificationInfo` del objeto `verificationInfos` miembro de datos. Este miembro de datos devuelve un `Object` matriz donde cada elemento es un `PDFSignatureVerificationInfo` objeto.
   * Al usar la variable `PDFSignatureVerificationInfo` , puede realizar tareas como determinar el estado de la firma obteniendo la variable `PDFSignatureVerificationInfo` del objeto `status` miembro de datos. Este miembro de datos devuelve un `SignatureStatus` cuyo miembro de datos estáticos le informa sobre el estado de la firma. Por ejemplo, si la firma es desconocida, este método devuelve `SignatureStatus.DocumentSignatureUnknown`.

**Consulte también lo siguiente**

[Verificación de varias firmas digitales](#verifying-multiple-digital-signatures)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Eliminación de firmas digitales {#removing-digital-signatures}

Las firmas digitales deben eliminarse de un campo de firma para poder aplicar una firma digital más reciente. No se puede sobrescribir una firma digital. Si intenta aplicar una firma digital a un campo de firma que contenga una firma, se producirá una excepción.

>[!NOTE]
>
>Para obtener más información sobre el servicio Signature, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-8}

Para quitar una firma digital de un campo de firma, realice las tareas siguientes:

1. Incluir archivos de proyecto.
1. Cree un cliente de firma.
1. Obtenga el documento del PDF que contiene una firma que se va a quitar.
1. Elimine la firma digital del campo de firma.
1. Guarde el documento de PDF como archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de firma**

Para poder realizar una operación de servicio de firma mediante programación, debe crear un cliente de servicio de firma.

**Obtener el documento del PDF que contiene una firma para quitar**

Para quitar una firma de un documento de PDF, debe obtener un documento de PDF que contenga una firma.

**Eliminación de la firma digital del campo de firma**

Para quitar correctamente una firma digital de un documento de PDF, debe especificar el nombre del campo de firma que contiene la firma digital. Además, debe tener permiso para eliminar la firma digital; de lo contrario, se produce una excepción.

**Guarde el documento del PDF como archivo del PDF**

Una vez que el servicio de firma elimina una firma digital de un campo de firma, puede guardar el documento PDF como archivo PDF para que los usuarios puedan abrirlo en Acrobat o Adobe Reader.

**Consulte también lo siguiente**

[Eliminación de firmas digitales mediante la API de Java](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[Eliminación de firmas digitales mediante la API de servicio web](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adición de campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields)

### Eliminación de firmas digitales mediante la API de Java {#remove-digital-signatures-using-the-java-api}

Elimine una firma digital utilizando la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-signatures-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente de firma.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `SignatureServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Obtener el documento del PDF que contiene una firma para quitar

   * Cree un `java.io.FileInputStream` objeto que representa el documento de PDF que contiene la firma que se va a quitar mediante su constructor y pasando un valor de cadena que especifica la ubicación del documento de PDF.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Eliminación de la firma digital del campo de firma

   Eliminar una firma digital de un campo de firma invocando la variable `SignatureServiceClient` del objeto `clearSignatureField` y pasando los siguientes valores:

   * A `com.adobe.idp.Document` que representa el documento del PDF que contiene la firma que se va a quitar.
   * Un valor de cadena que especifica el nombre del campo de firma que contiene la firma digital.

   La variable `clearSignatureField` el método devuelve un `com.adobe.idp.Document` objeto que representa el documento PDF del que se ha eliminado la firma digital.

1. Guarde el documento del PDF como archivo del PDF

   * Cree un `java.io.File` y asegúrese de que la extensión de archivo es .pdf.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` método. Pase el `java.io.File` para copiar el contenido del `com.adobe.idp.Document` al archivo. Asegúrese de usar la variable `Document` objeto devuelto por el `clearSignatureField` método.

**Consulte también lo siguiente**

[Eliminación de firmas digitales](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Inicio rápido (modo SOAP): Eliminación de una firma digital mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminación de firmas digitales mediante la API de servicio web {#remove-digital-signatures-using-the-web-service-api}

Elimine una firma digital mediante la API de firma (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Crear un cliente de firma

   * Cree un `SignatureServiceClient` usando su constructor predeterminado.
   * Cree un `SignatureServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `SignatureServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtener el documento del PDF que contiene una firma para quitar

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar un documento de PDF que contiene una firma digital que se va a quitar.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF firmado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` método. Pase la matriz de bytes, la posición de inicio y la longitud del flujo para leerlos.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Eliminación de la firma digital del campo de firma

   Elimine la firma digital invocando la variable `SignatureServiceClient` del objeto `clearSignatureField` y pasando los siguientes valores:

   * A `BLOB` objeto que contiene el documento de PDF firmado.
   * Valor de cadena que representa el nombre del campo de firma que contiene la firma digital que se va a quitar.

   La variable `clearSignatureField` el método devuelve un `BLOB` objeto que representa el documento PDF del que se ha eliminado la firma digital.

1. Guarde el documento del PDF como archivo del PDF

   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF que contiene un campo de firma vacío y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto devuelto por el `sign` método. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` miembro de datos.
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en el archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Eliminación de firmas digitales](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
