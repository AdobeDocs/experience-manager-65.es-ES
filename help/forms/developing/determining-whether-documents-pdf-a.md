---
title: Determinación de si los documentos cumplen los criterios de PDF/A
seo-title: Determining Whether Documents Are PDF/A-Compliant
description: Utilice el servicio Assembler para determinar si un documento de PDF es compatible con el PDF/A mediante la API de Java y la API del servicio web.
seo-description: Use the Assembler service to determine if a PDF document is PDF/A-compliant using the Java API and Web Service API.
uuid: 4e9d8c8f-2153-411b-9c4b-2d14b3c8f4bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c429d6e1-7847-43c8-bf75-cb0078dbb9d5
role: Developer
exl-id: 096fd2ac-616f-484a-b093-9d98b2f87093
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2082'
ht-degree: 2%

---

# Determinación de si los documentos cumplen los criterios de PDF/A {#determining-whether-documents-are-pdf-a-compliant}

Puede determinar si un documento de PDF es compatible con el PDF/A mediante el servicio Assembler. Un documento PDF/A existe como formato de archivo destinado a la conservación a largo plazo del contenido del documento. Las fuentes están incrustadas en el documento y el archivo no está comprimido. Como resultado, un documento PDF/A suele ser más grande que un documento PDF estándar. Además, un documento PDF/A no contiene contenido de audio y vídeo.

La especificación del PDF/A-1 consta de dos niveles de conformidad, a saber, A y B. La principal diferencia entre los dos niveles es la compatibilidad con la estructura lógica (accesibilidad), que no es necesaria para el nivel de conformidad B. Independientemente del nivel de conformidad, el PDF/A-1 dicta que todas las fuentes están incrustadas en el documento PDF/A generado. En este momento, solo se admite el PDF/A-1b en la validación (y conversión).

A los efectos de esta discusión, supongamos que se utiliza el siguiente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

Dentro de este documento DDX, la variable `DocumentInformation` indica al servicio Assembler que devuelva información sobre el documento del PDF de entrada. Dentro de `DocumentInformation` elemento, la variable `PDFAValidation` indica al servicio Assembler que indique si el documento del PDF de entrada es compatible con el PDF/A.

El servicio Assembler devuelve información que especifica si el documento del PDF de entrada es compatible con el PDF/A en un documento XML que contiene un `PDFAConformance` elemento. Si el documento del PDF de entrada es compatible con el PDF/A, el valor de la variable `PDFAConformance` del elemento `isCompliant` el atributo es `true`. Si el documento del PDF no es compatible con el PDF/A, el valor de la variable `PDFAConformance` del elemento `isCompliant` el atributo es `false`.

>[!NOTE]
>
>Porque el documento DDX especificado en esta sección contiene un `DocumentInformation` , el servicio Assembler devuelve datos XML en lugar de un documento PDF. Es decir, el servicio del ensamblador no monta ni desmonta un documento del PDF; devuelve información sobre el documento del PDF de entrada dentro de un documento XML.

>[!NOTE]
>
>Para obtener más información sobre el servicio Assembler, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para determinar si un documento de PDF es compatible con el PDF/A, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de ensamblador de PDF.
1. Haga referencia a un documento DDX existente.
1. Haga referencia a un documento de PDF utilizado para determinar la conformidad del PDF/A.
1. Establezca las opciones de tiempo de ejecución.
1. Recupere información sobre el documento del PDF.
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

**Creación de un cliente de ensamblador de PDF**

Para poder realizar una operación Assembler mediante programación, debe crear un cliente de servicio Assembler.

**Referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para realizar una operación de servicio Assembler. Para determinar si un documento de PDF de entrada es compatible con el PDF/A, asegúrese de que el documento DDX contenga la variable `PDFAValidation` dentro de un `DocumentInformation` elemento. La variable `PDFAValidation` indica al servicio Assembler que devuelva un documento XML que especifica si el documento del PDF de entrada es compatible con el PDF/A.

**Referencia a un documento de PDF utilizado para determinar la conformidad del PDF/A**

Se debe hacer referencia a un documento PDF y pasarlo al servicio Assembler para determinar si el documento PDF es compatible con el PDF/A.

**Establecer opciones de tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlan el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede definir una opción que indique al servicio Assembler que continúe procesando un trabajo si se encuentra un error. Para obtener información sobre las opciones de tiempo de ejecución que puede establecer, consulte la `AssemblerOptionSpec` referencia de clase en [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Recuperar información sobre el documento del PDF**

Después de crear el cliente de servicio Assembler, hacer referencia al documento DDX, hacer referencia a un documento de PDF interactivo y establecer las opciones de tiempo de ejecución, puede invocar la variable `invokeDDX` operación. Dado que el documento DDX contiene la variable `DocumentInformation` , el servicio Assembler devuelve datos XML en lugar de un documento PDF.

**Guardar el documento XML devuelto**

El documento XML que devuelve el servicio Assembler especifica si el documento del PDF de entrada es compatible con el PDF/A. Por ejemplo, si el documento del PDF de entrada no es compatible con PDF/A, el servicio Assembler devuelve un documento XML que contiene el siguiente elemento:

```xml
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

Guarde el documento XML como archivo XML para que pueda abrir el archivo y ver los resultados.

**Consulte también lo siguiente**

[Determinar si un documento es compatible con el PDF/A mediante la API de Java](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[Determinar si un documento es compatible con el PDF/A mediante la API de servicio web](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Determinar si un documento es compatible con el PDF/A mediante la API de Java {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

Determine si un documento de PDF es compatible con el PDF/A mediante la API de servicio del ensamblador (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-assembler-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente de ensamblador de PDF.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `AssemblerServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un documento DDX existente.

   * Cree un `java.io.FileInputStream` objeto que representa el documento DDX utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo DDX. Para determinar si el documento del PDF es compatible con el PDF/A, asegúrese de que el documento DDX contenga la variable `PDFAValidation` elemento que se encuentra dentro de un `DocumentInformation` elemento.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Haga referencia a un documento de PDF utilizado para determinar la conformidad del PDF/A.

   * Cree un `java.io.FileInputStream` mediante el uso de su constructor y pasando la ubicación de un documento PDF que se utiliza para determinar la conformidad PDF/A.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto que contiene el documento PDF.
   * Cree un `java.util.Map` objeto que se utiliza para almacenar el documento del PDF de entrada utilizando un `HashMap` constructor.
   * Agregue una entrada al `java.util.Map` invocando su `put` y pasando los siguientes argumentos:

      * Un valor de cadena que representa el nombre de la clave. Este valor debe coincidir con el valor del elemento de origen especificado en el documento DDX. Por ejemplo, el valor del elemento de origen ubicado en el documento DDX que se introduce en esta sección es Loan.pdf.
      * A `com.adobe.idp.Document` objeto que contiene el documento del PDF de entrada.

1. Establezca las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` que almacena opciones en tiempo de ejecución mediante su constructor.
   * Configure las opciones en tiempo de ejecución para satisfacer los requisitos empresariales invocando un método que pertenece al `AssemblerOptionSpec` objeto. Por ejemplo, para solicitar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, invoque la función `AssemblerOptionSpec` del objeto `setFailOnError` método y pase `false`.

1. Recupere información sobre el documento del PDF.

   Invocar el `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores obligatorios:

   * A `com.adobe.idp.Document` objeto que representa el documento DDX que se va a utilizar
   * A `java.util.Map` objeto que contiene el archivo de PDF de entrada que se utiliza para determinar la conformidad PDF/A
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica las opciones de tiempo de ejecución

   La variable `invokeDDX` el método devuelve un `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contiene datos XML que especifican si el documento del PDF de entrada es compatible con el PDF/A.

1. Guarde el documento XML devuelto.

   Para obtener datos XML que especifiquen si el documento del PDF de entrada es un documento PDF/A, realice las siguientes acciones:

   * Invocar el `AssemblerResult` del objeto `getDocuments` método. Esto devuelve un `java.util.Map` objeto.
   * Iterar a través de la variable `java.util.Map` hasta que encuentre el resultado `com.adobe.idp.Document` objeto.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` para extraer el documento XML. Asegúrese de guardar los datos XML como un archivo XML.

**Consulte también lo siguiente**

[Inicio rápido (modo SOAP): Determinación de si un documento es compatible con el PDF/A mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) (modo SOAP)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Determinar si un documento es compatible con el PDF/A mediante la API de servicio web {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

Determine si un documento de PDF es compatible con el PDF/A mediante el uso de la API de servicio del ensamblador (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de ensamblador de PDF.

   * Cree un `AssemblerServiceClient` usando su constructor predeterminado.
   * Cree un `AssemblerServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `AssemblerServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un documento DDX existente.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar el documento DDX.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento DDX y el modo en el que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Haga referencia a un documento de PDF utilizado para determinar la conformidad del PDF/A.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar el documento del PDF de entrada.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento del PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.
   * Cree un `MyMapOf_xsd_string_To_xsd_anyType` objeto. Este objeto de colección se utiliza para almacenar el documento del PDF.
   * Cree un `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Asigne un valor de cadena que represente el nombre de clave a la variable `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key` campo . Este valor debe coincidir con el valor del elemento de origen del PDF especificado en el documento DDX.
   * Asigne la variable `BLOB` objeto que almacena el documento del PDF en el `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value` campo .
   * Agregue la variable `MyMapOf_xsd_string_To_xsd_anyType_Item` al `MyMapOf_xsd_string_To_xsd_anyType` objeto. Invocar el `MyMapOf_xsd_string_To_xsd_anyType` objeto&#39; `Add` y pase el `MyMapOf_xsd_string_To_xsd_anyType` objeto.

1. Establezca las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` que almacena opciones en tiempo de ejecución mediante su constructor.
   * Configure las opciones en tiempo de ejecución para satisfacer los requisitos empresariales asignando un valor a un miembro de datos que pertenezca al grupo `AssemblerOptionSpec` objeto. Por ejemplo, para solicitar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne `false` a `AssemblerOptionSpec` del objeto `failOnError` miembro de datos.

1. Recupere información sobre el documento del PDF.

   Invocar el `AssemblerServiceService` del objeto `invoke` y pase los siguientes valores:

   * A `BLOB` que representa el documento DDX.
   * La variable `MyMapOf_xsd_string_To_xsd_anyType` objeto que contiene el documento del PDF de entrada. Sus claves deben coincidir con los nombres de los archivos de origen del PDF, y sus valores deben ser `BLOB` que corresponde al archivo de PDF de entrada.
   * Un `AssemblerOptionSpec` objeto que especifica opciones en tiempo de ejecución.

   La variable `invoke` devuelve un valor `AssemblerResult` objeto que contiene datos XML que especifican si el documento del PDF de entrada es un documento PDF/A.

1. Guarde el documento XML devuelto.

   Para obtener datos XML que especifiquen si el documento del PDF de entrada es un documento PDF/A, realice las siguientes acciones:

   * Acceda a la `AssemblerResult` del objeto `documents` , que es un `Map` objeto que contiene los datos XML que especifican si el documento del PDF de entrada es un documento PDF/A.
   * Iterar a través de la variable `Map` para obtener cada documento resultante. A continuación, convierta el valor de ese miembro de la matriz en un `BLOB`.
   * Extraiga los datos binarios que representan los datos XML accediendo a su `BLOB` del objeto `MTOM` campo . Este campo almacena una matriz de bytes a los que puede escribir como archivo XML.

**Consulte también lo siguiente**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
