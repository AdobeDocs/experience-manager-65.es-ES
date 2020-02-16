---
title: Determinación de si los documentos son compatibles con PDF/A
seo-title: Determinación de si los documentos son compatibles con PDF/A
description: nulo
seo-description: nulo
uuid: 4e9d8c8f-2153-411b-9c4b-2d14b3c8f4bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c429d6e1-7847-43c8-bf75-cb0078dbb9d5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Determinación de si los documentos son compatibles con PDF/A {#determining-whether-documents-are-pdf-a-compliant}

Puede determinar si un documento PDF es compatible con PDF/A mediante el servicio Ensamblador. Un documento PDF/A existe como formato de archivo para la conservación a largo plazo del contenido del documento. Las fuentes se incrustan en el documento y el archivo se descomprime. Como resultado, un documento PDF/A suele ser más grande que un documento PDF estándar. Además, un documento PDF/A no contiene contenido de audio y vídeo.

La especificación PDF/A-1 consta de dos niveles de conformidad, a saber, A y B. La principal diferencia entre los dos niveles es la compatibilidad con la estructura lógica (accesibilidad), que no es necesaria para el nivel de conformidad B. Independientemente del nivel de conformidad, PDF/A-1 dicta que todas las fuentes están incrustadas en el documento PDF/A generado. En este momento, solo se admite PDF/A-1b en la validación (y conversión).

A los efectos de este análisis, supongamos que se utiliza el siguiente documento DDX.

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

En este documento DDX, el `DocumentInformation` elemento indica al servicio Ensamblador que devuelva información sobre el documento PDF de entrada. Dentro del `DocumentInformation` elemento, el `PDFAValidation` elemento ordena al servicio Ensamblador que indique si el documento PDF de entrada es compatible con PDF/A.

El servicio Ensamblador devuelve información que especifica si el documento PDF de entrada es compatible con PDF/A en un documento XML que contiene un `PDFAConformance` elemento. Si el documento PDF de entrada es compatible con PDF/A, el valor del `PDFAConformance` atributo `isCompliant` del elemento es `true`. Si el documento PDF no es compatible con PDF/A, el valor del `PDFAConformance` atributo `isCompliant` del elemento es `false`.

>[!NOTE]
>
>Dado que el documento DDX especificado en esta sección contiene un `DocumentInformation` elemento, el servicio Ensamblador devuelve datos XML en lugar de un documento PDF. Es decir, el servicio Ensamblador no monta ni desmonta un documento PDF; devuelve información sobre el documento PDF de entrada dentro de un documento XML.

>[!NOTE]
>
>Para obtener más información sobre el servicio Compilador, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y Referencia](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Resumen de los pasos {#summary-of-steps}

Para determinar si un documento PDF es compatible con PDF/A, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de ensamblador de PDF.
1. Haga referencia a un documento DDX existente.
1. Haga referencia a un documento PDF utilizado para determinar la compatibilidad con PDF/A.
1. Configure las opciones de tiempo de ejecución.
1. Recupere información sobre el documento PDF.
1. Guarde el documento XML devuelto.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms. Para obtener información sobre la ubicación de todos los archivos JAR de AEM Forms, consulte [Inclusión de archivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)de biblioteca Java de AEM Forms.

**Crear un cliente de ensamblador de PDF**

Antes de realizar una operación de ensamblador mediante programación, debe crear un cliente de servicio de ensamblador.

**Hacer referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para realizar una operación de servicio de ensamblador. Para determinar si un documento PDF de entrada es compatible con PDF/A, asegúrese de que el documento DDX contiene el `PDFAValidation` elemento dentro de un `DocumentInformation` elemento. El `PDFAValidation` elemento ordena al servicio Ensamblador que devuelva un documento XML que especifica si el documento PDF de entrada es compatible con PDF/A.

**Hacer referencia a un documento PDF utilizado para determinar la conformidad con PDF/A**

Se debe hacer referencia a un documento PDF y pasarlo al servicio Ensamblador para determinar si el documento PDF es compatible con PDF/A.

**Definición de opciones de tiempo de ejecución**

Puede definir opciones en tiempo de ejecución que controlen el comportamiento del servicio de ensamblador mientras realiza un trabajo. Por ejemplo, puede definir una opción que indique al servicio Ensamblador que continúe procesando un trabajo si se produce un error. Para obtener información sobre las opciones de tiempo de ejecución que puede definir, consulte la referencia de la `AssemblerOptionSpec` clase en Referencia [de API de formularios](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM.

**Recuperar información sobre el documento PDF**

Después de crear el cliente del servicio Ensamblador, hacer referencia al documento DDX, hacer referencia a un documento PDF interactivo y definir las opciones de tiempo de ejecución, puede invocar la `invokeDDX` operación. Dado que el documento DDX contiene el `DocumentInformation` elemento, el servicio Ensamblador devuelve datos XML en lugar de un documento PDF.

**Guardar el documento XML devuelto**

El documento XML que devuelve el servicio Ensamblador especifica si el documento PDF de entrada es compatible con PDF/A. Por ejemplo, si el documento PDF de entrada no es compatible con PDF/A, el servicio Ensamblador devuelve un documento XML que contiene el siguiente elemento:

```as3
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

Guarde el documento XML como archivo XML para que pueda abrir el archivo y ver los resultados.

**Consulte también**

[Determinar si un documento es compatible con PDF/A mediante la API de Java](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[Determinar si un documento es compatible con PDF/A mediante la API de servicio Web](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Compilación de documentos PDF mediante programación](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Determinar si un documento es compatible con PDF/A mediante la API de Java {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

Determine si un documento PDF es compatible con PDF/A mediante la API de servicio de ensamblador (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de ensamblador de PDF.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `AssemblerServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un documento DDX existente.

   * Cree un `java.io.FileInputStream` objeto que represente el documento DDX utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo DDX. Para determinar si el documento PDF es compatible con PDF/A, asegúrese de que el documento DDX contiene el `PDFAValidation` elemento contenido en un `DocumentInformation` elemento.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Haga referencia a un documento PDF utilizado para determinar la compatibilidad con PDF/A.

   * Cree un `java.io.FileInputStream` objeto utilizando su constructor y pasando la ubicación de un documento PDF que se utiliza para determinar la compatibilidad con PDF/A.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto que contiene el documento PDF.
   * Cree un `java.util.Map` objeto que se utilice para almacenar el documento PDF de entrada mediante un `HashMap` constructor.
   * Agregue una entrada al `java.util.Map` objeto invocando su `put` método y pasando los siguientes argumentos:

      * Un valor de cadena que representa el nombre de la clave. Este valor debe coincidir con el valor del elemento de origen especificado en el documento DDX. Por ejemplo, el valor del elemento de origen ubicado en el documento DDX que se introduce en esta sección es Loan.pdf.
      * Un `com.adobe.idp.Document` objeto que contiene el documento PDF de entrada.

1. Configure las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` objeto que almacene opciones de tiempo de ejecución mediante su constructor.
   * Configure las opciones de tiempo de ejecución para cumplir los requisitos comerciales invocando un método que pertenece al `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Ensamblador que continúe procesando un trabajo cuando se produzca un error, invoque el `AssemblerOptionSpec` método del `setFailOnError` objeto y pase `false`.

1. Recupere información sobre el documento PDF.

   Invoque el `AssemblerServiceClient` método del `invokeDDX` objeto y pase los siguientes valores obligatorios:

   * Un `com.adobe.idp.Document` objeto que representa el documento DDX que se va a utilizar
   * Un `java.util.Map` objeto que contiene el archivo PDF de entrada que se utiliza para determinar la compatibilidad con PDF/A
   * Un `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica las opciones de tiempo de ejecución
   El `invokeDDX` método devuelve un `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contiene datos XML que especifica si el documento PDF de entrada es compatible con PDF/A.

1. Guarde el documento XML devuelto.

   Para obtener datos XML que especifican si el documento PDF de entrada es un documento PDF/A, realice las siguientes acciones:

   * Invocar el `AssemblerResult` método del `getDocuments` objeto. Esto devuelve un `java.util.Map` objeto.
   * Repita el `java.util.Map` objeto hasta que encuentre el `com.adobe.idp.Document` objeto resultante.
   * Invocar el `com.adobe.idp.Document` método del `copyToFile` objeto para extraer el documento XML. Asegúrese de guardar los datos XML como un archivo XML.

**Consulte también**

[Inicio rápido (modo SOAP): Determinación de si un documento es compatible con PDF/A mediante la API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) de Java (modo SOAP)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Determinar si un documento es compatible con PDF/A mediante la API de servicio Web {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

Determine si un documento PDF es compatible con PDF/A mediante la API de servicio de ensamblador (servicio Web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de ensamblador de PDF.

   * Cree un `AssemblerServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `AssemblerServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `AssemblerServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un documento DDX existente.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar el documento DDX.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento DDX y el modo en el que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.

1. Haga referencia a un documento PDF utilizado para determinar la compatibilidad con PDF/A.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar el documento PDF de entrada.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` propiedad con el contenido de la matriz de bytes.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Este objeto de colección se utiliza para almacenar el documento PDF.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType_Item` object.
   * Asigne un valor de cadena que represente el nombre clave al `MyMapOf_xsd_string_To_xsd_anyType_Item` campo del `key` objeto. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX.
   * Asigne el `BLOB` objeto que almacena el documento PDF al `MyMapOf_xsd_string_To_xsd_anyType_Item` campo del `value` objeto.
   * Agregue el `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto al `MyMapOf_xsd_string_To_xsd_anyType` objeto. Invocar el `MyMapOf_xsd_string_To_xsd_anyType` método del `Add` objeto y pasar el `MyMapOf_xsd_string_To_xsd_anyType` objeto.

1. Configure las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` objeto que almacene opciones de tiempo de ejecución mediante su constructor.
   * Configure las opciones de tiempo de ejecución para cumplir los requisitos comerciales asignando un valor a un miembro de datos que pertenece al `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Ensamblador que continúe procesando un trabajo cuando se produzca un error, asigne `false` al miembro de datos del `AssemblerOptionSpec` objeto `failOnError` .

1. Recupere información sobre el documento PDF.

   Invoque el `AssemblerServiceService` método del `invoke` objeto y pase los valores siguientes:

   * Un `BLOB` objeto que representa el documento DDX.
   * El `MyMapOf_xsd_string_To_xsd_anyType` objeto que contiene el documento PDF de entrada. Sus claves deben coincidir con los nombres de los archivos de origen PDF y sus valores deben ser el `BLOB` objeto que corresponde al archivo PDF de entrada.
   * Un `AssemblerOptionSpec` objeto que especifica opciones de tiempo de ejecución.
   El `invoke` método devuelve un `AssemblerResult` objeto que contiene datos XML que especifica si el documento PDF de entrada es un documento PDF/A.

1. Guarde el documento XML devuelto.

   Para obtener datos XML que especifican si el documento PDF de entrada es un documento PDF/A, realice las siguientes acciones:

   * Acceda al `AssemblerResult` campo del `documents` objeto, que es un `Map` objeto que contiene los datos XML que especifica si el documento PDF de entrada es un documento PDF/A.
   * Repita el `Map` objeto para obtener cada documento resultante. A continuación, convierta el valor del miembro de la matriz en un `BLOB`.
   * Extraiga los datos binarios que representan los datos XML accediendo al campo de su `BLOB` objeto `MTOM` . Este campo almacena una matriz de bytes a los que puede escribir como archivo XML.

**Consulte también**

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
