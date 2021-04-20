---
title: Determinación de si los documentos cumplen los requisitos de PDF/A
seo-title: Determinación de si los documentos cumplen los requisitos de PDF/A
description: Utilice el servicio Assembler para determinar si un documento PDF es compatible con PDF/A mediante la API de Java y la API del servicio Web.
seo-description: Utilice el servicio Assembler para determinar si un documento PDF es compatible con PDF/A mediante la API de Java y la API del servicio Web.
uuid: 4e9d8c8f-2153-411b-9c4b-2d14b3c8f4bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c429d6e1-7847-43c8-bf75-cb0078dbb9d5
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2110'
ht-degree: 0%

---


# Determinación de si los documentos cumplen con PDF/A {#determining-whether-documents-are-pdf-a-compliant}

Puede determinar si un documento PDF es compatible con PDF/A mediante el servicio Assembler. Un documento PDF/A existe como formato de archivo destinado a la conservación a largo plazo del contenido del documento. Las fuentes están incrustadas en el documento y el archivo no está comprimido. Como resultado, un documento PDF/A suele ser más grande que un documento PDF estándar. Además, un documento PDF/A no contiene contenido de audio y vídeo.

La especificación PDF/A-1 consta de dos niveles de conformidad, a saber, A y B. La diferencia principal entre los dos niveles es la compatibilidad con la estructura lógica (accesibilidad), que no es necesaria para el nivel de conformidad B. Independientemente del nivel de conformidad, PDF/A-1 dicta que todas las fuentes están incrustadas en el documento PDF/A generado. En este momento, solo se admite PDF/A-1b en la validación (y conversión).

A los efectos de esta discusión, supongamos que se utiliza el siguiente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

Dentro de este documento DDX, el elemento `DocumentInformation` ordena al servicio Assembler que devuelva información sobre el documento PDF de entrada. Dentro del elemento `DocumentInformation` , el elemento `PDFAValidation` ordena al servicio Assembler que indique si el documento PDF de entrada es compatible con PDF/A.

El servicio Assembler devuelve información que especifica si el documento PDF de entrada es compatible con PDF/A dentro de un documento XML que contiene un elemento `PDFAConformance`. Si el documento PDF de entrada es compatible con PDF/A, el valor del atributo `PDFAConformance` del elemento `isCompliant` es `true`. Si el documento PDF no es compatible con PDF/A, el valor del atributo `PDFAConformance` del elemento `isCompliant` es `false`.

>[!NOTE]
>
>Dado que el documento DDX especificado en esta sección contiene un elemento `DocumentInformation`, el servicio Assembler devuelve datos XML en lugar de un documento PDF. Es decir, el servicio Assembler no monta ni desmonta un documento PDF; devuelve información sobre el documento PDF de entrada dentro de un documento XML.

>[!NOTE]
>
>Para obtener más información sobre el servicio Assembler, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para determinar si un documento PDF es compatible con PDF/A, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente del ensamblador PDF.
1. Haga referencia a un documento DDX existente.
1. Haga referencia a un documento PDF utilizado para determinar la conformidad con PDF/A.
1. Establezca las opciones de tiempo de ejecución.
1. Recupere información sobre el documento PDF.
1. Guarde el documento XML devuelto.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-Utilities.jar y jbossall-client.jar con archivos JAR específicos del servidor de aplicaciones J2EE en el que AEM Forms está implementado. Para obtener información sobre la ubicación de todos los archivos JAR de AEM Forms, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de ensamblador PDF**

Para poder realizar una operación Assembler mediante programación, debe crear un cliente de servicio Assembler.

**Referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para realizar una operación de servicio Assembler. Para determinar si un documento PDF de entrada es compatible con PDF/A, asegúrese de que el documento DDX contenga el elemento `PDFAValidation` dentro de un elemento `DocumentInformation`. El elemento `PDFAValidation` ordena al servicio Assembler que devuelva un documento XML que especifique si el documento PDF de entrada es compatible con PDF/A.

**Hacer referencia a un documento PDF utilizado para determinar la conformidad con PDF/A**

Se debe hacer referencia a un documento PDF y pasarlo al servicio Assembler para determinar si el documento PDF es compatible con PDF/A.

**Establecer opciones de tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlan el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede definir una opción que indique al servicio Assembler que continúe procesando un trabajo si se encuentra un error. Para obtener información sobre las opciones de tiempo de ejecución que puede establecer, consulte la referencia de clase `AssemblerOptionSpec` en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Recuperar información sobre el documento PDF**

Después de crear el cliente de servicio Assembler, hacer referencia al documento DDX, hacer referencia a un documento PDF interactivo y establecer las opciones de tiempo de ejecución, puede invocar la operación `invokeDDX`. Dado que el documento DDX contiene el elemento `DocumentInformation`, el servicio Assembler devuelve datos XML en lugar de un documento PDF.

**Guardar el documento XML devuelto**

El documento XML que devuelve el servicio Assembler especifica si el documento PDF de entrada es compatible con PDF/A. Por ejemplo, si el documento PDF de entrada no es compatible con PDF/A, el servicio Assembler devuelve un documento XML que contiene el siguiente elemento:

```xml
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

Guarde el documento XML como archivo XML para que pueda abrir el archivo y ver los resultados.

**Consulte también**

[Determinar si un documento es compatible con PDF/A mediante la API de Java](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[Determinar si un documento es compatible con PDF/A mediante la API de servicio web](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montaje programático de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Determinar si un documento es compatible con PDF/A mediante la API de Java {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

Determine si un documento PDF es compatible con PDF/A utilizando la API del servicio Assembler (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-assembler-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente del ensamblador PDF.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `AssemblerServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Haga referencia a un documento DDX existente.

   * Cree un objeto `java.io.FileInputStream` que represente el documento DDX utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo DDX. Para determinar si el documento PDF es compatible con PDF/A, asegúrese de que el documento DDX contenga el elemento `PDFAValidation` que se encuentra dentro de un elemento `DocumentInformation`.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Haga referencia a un documento PDF utilizado para determinar la conformidad con PDF/A.

   * Cree un objeto `java.io.FileInputStream` utilizando su constructor y pasando la ubicación de un documento PDF que se utiliza para determinar la conformidad con PDF/A.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream` que contiene el documento PDF.
   * Cree un objeto `java.util.Map` que se utilice para almacenar el documento PDF de entrada utilizando un constructor `HashMap`.
   * Agregue una entrada al objeto `java.util.Map` invocando su método `put` y pasando los siguientes argumentos:

      * Un valor de cadena que representa el nombre de la clave. Este valor debe coincidir con el valor del elemento de origen especificado en el documento DDX. Por ejemplo, el valor del elemento de origen ubicado en el documento DDX que se introduce en esta sección es Loan.pdf.
      * Un objeto `com.adobe.idp.Document` que contiene el documento PDF de entrada.

1. Establezca las opciones de tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución empleando su constructor.
   * Defina las opciones en tiempo de ejecución para satisfacer los requisitos empresariales invocando un método que pertenece al objeto `AssemblerOptionSpec` . Por ejemplo, para solicitar al servicio Assembler que continúe procesando un trabajo cuando se produce un error, invoque el método `AssemblerOptionSpec` del objeto `setFailOnError` y pase `false`.

1. Recupere información sobre el documento PDF.

   Invoque el método `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores obligatorios:

   * Un objeto `com.adobe.idp.Document` que representa el documento DDX que se va a utilizar
   * Un objeto `java.util.Map` que contiene el archivo PDF de entrada que se utiliza para determinar la conformidad con PDF/A
   * Un objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones en tiempo de ejecución

   El método `invokeDDX` devuelve un objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene datos XML que especifican si el documento PDF de entrada es compatible con PDF/A.

1. Guarde el documento XML devuelto.

   Para obtener datos XML que especifiquen si el documento PDF de entrada es un documento PDF/A, realice las siguientes acciones:

   * Invoque el método `AssemblerResult` del objeto `getDocuments`. Esto devuelve un objeto `java.util.Map`.
   * Repita el objeto `java.util.Map` hasta que encuentre el objeto `com.adobe.idp.Document` resultante.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para extraer el documento XML. Asegúrese de guardar los datos XML como un archivo XML.

**Consulte también**

[Inicio rápido (modo SOAP): Determinación de si un documento es compatible con PDF/A mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api)  (modo SOAP)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Determinar si un documento es compatible con PDF/A utilizando la API de servicio web {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

Determine si un documento PDF es compatible con PDF/A utilizando la API del servicio Assembler (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente del ensamblador PDF.

   * Cree un objeto `AssemblerServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `AssemblerServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `AssemblerServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un documento DDX existente.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el documento DDX.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento DDX y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición de inicio y la longitud de flujo para leer.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Haga referencia a un documento PDF utilizado para determinar la conformidad con PDF/A.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el documento PDF de entrada.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición de inicio y la longitud de flujo para leer.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.
   * Cree un objeto `MyMapOf_xsd_string_To_xsd_anyType`. Este objeto de colección se utiliza para almacenar el documento PDF.
   * Cree un objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Asigne un valor de cadena que represente el nombre clave al campo `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key`. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX.
   * Asigne el objeto `BLOB` que almacena el documento PDF al campo `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value`.
   * Agregue el objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` al objeto `MyMapOf_xsd_string_To_xsd_anyType`. Invoque el método `MyMapOf_xsd_string_To_xsd_anyType` object&#39; `Add` y pase el objeto `MyMapOf_xsd_string_To_xsd_anyType`.

1. Establezca las opciones de tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución empleando su constructor.
   * Defina las opciones en tiempo de ejecución para satisfacer los requisitos empresariales asignando un valor a un miembro de datos que pertenece al objeto `AssemblerOptionSpec`. Por ejemplo, para solicitar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne `false` al miembro de datos `AssemblerOptionSpec` del objeto `failOnError`.

1. Recupere información sobre el documento PDF.

   Invoque el método `AssemblerServiceService` del objeto `invoke` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento DDX.
   * El objeto `MyMapOf_xsd_string_To_xsd_anyType` que contiene el documento PDF de entrada. Sus claves deben coincidir con los nombres de los archivos de origen PDF y sus valores deben ser el objeto `BLOB` que corresponda al archivo PDF de entrada.
   * Un objeto `AssemblerOptionSpec` que especifica opciones en tiempo de ejecución.

   El método `invoke` devuelve un objeto `AssemblerResult` que contiene datos XML que especifican si el documento PDF de entrada es un documento PDF/A.

1. Guarde el documento XML devuelto.

   Para obtener datos XML que especifiquen si el documento PDF de entrada es un documento PDF/A, realice las siguientes acciones:

   * Acceda al campo `AssemblerResult` del objeto `documents`, que es un objeto `Map` que contiene los datos XML que especifican si el documento PDF de entrada es un documento PDF/A.
   * Repita el objeto `Map` para obtener cada documento resultante. A continuación, convierta el valor de ese miembro de la matriz en `BLOB`.
   * Extraiga los datos binarios que representan los datos XML accediendo al campo `BLOB` del objeto `MTOM`. Este campo almacena una matriz de bytes a los que puede escribir como archivo XML.

**Consulte también**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
