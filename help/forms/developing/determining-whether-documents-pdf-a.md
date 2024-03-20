---
title: Determinar si los documentos cumplen los criterios de PDF/A
description: Utilice el servicio Assembler para determinar si un documento de PDF es compatible con el PDF/A mediante la API de Java y la API de servicio web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 096fd2ac-616f-484a-b093-9d98b2f87093
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2065'
ht-degree: 2%

---

# Determinar si los documentos cumplen los criterios de PDF/A {#determining-whether-documents-are-pdf-a-compliant}

Puede determinar si un documento de PDF es compatible con el PDF/A mediante el servicio Assembler. Existe un documento PDF/A como formato de archivo diseñado para la preservación a largo plazo del contenido del documento. Las fuentes están incrustadas en el documento y el archivo no está comprimido. Como resultado, un documento PDF/A suele ser más grande que un documento PDF estándar. Además, un documento PDF/A no contiene contenido de audio y vídeo.

La especificación PDF/A-1 consta de dos niveles de conformidad, a saber, A y B. La principal diferencia entre los dos niveles es la compatibilidad con la estructura lógica (accesibilidad), que no es necesaria para el nivel de conformidad B. Independientemente del nivel de conformidad, PDF/A-1 dicta que todas las fuentes estén incrustadas en el documento PDF/A generado. En este momento, solo se admite el PDF/A-1b en la validación (y conversión).

A los efectos de este análisis, supongamos que se utiliza el siguiente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

Dentro de este documento DDX, la variable `DocumentInformation` indica al servicio Assembler que devuelva información sobre el documento del PDF de entrada. Dentro de `DocumentInformation` , el `PDFAValidation` indica al servicio Assembler que indique si el documento del PDF de entrada es compatible con el PDF/A.

El servicio Assembler devuelve información que especifica si el documento del PDF de entrada es compatible con el PDF/A de un documento XML que contiene un `PDFAConformance` Elemento. Si el documento del PDF de entrada es compatible con el PDF/A, el valor del `PDFAConformance` del elemento `isCompliant` el atributo es `true`. Si el documento del PDF no es compatible con el PDF/A, el valor del `PDFAConformance` del elemento `isCompliant` el atributo es `false`.

>[!NOTE]
>
>Dado que el documento DDX especificado en esta sección contiene un `DocumentInformation` , el servicio Assembler devuelve datos XML en lugar de un documento de PDF. Es decir, el servicio Assembler no monta ni desmonta un documento de PDF; devuelve información sobre el documento de PDF de entrada dentro de un documento XML.

>[!NOTE]
>
>Para obtener más información sobre el servicio Assembler, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para determinar si un documento de PDF es compatible con el PDF/A, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDF Assembler.
1. Hacer referencia a un documento DDX existente.
1. Hacer referencia a un documento de PDF utilizado para determinar la conformidad de PDF/A.
1. Establecer opciones en tiempo de ejecución.
1. Recupere información sobre el documento del PDF.
1. Guarde el documento XML devuelto.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-utilities.jar y jbossall-client.jar con archivos JAR específicos del servidor de aplicaciones J2EE en el que AEM Forms está implementado. Para obtener información sobre la ubicación de todos los archivos JAR de AEM Forms, consulte [Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de PDF Assembler**

Para poder realizar mediante programación una operación de Assembler, debe crear un cliente de servicio Assembler.

**Hacer referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para realizar una operación del servicio Assembler. Para determinar si un documento del PDF de entrada es compatible con el PDF/A, asegúrese de que el documento DDX contenga el `PDFAValidation` dentro de un `DocumentInformation` Elemento. El `PDFAValidation` indica al servicio Assembler que devuelva un documento XML que especifica si el documento del PDF de entrada es compatible con el PDF/A.

**Hacer referencia a un documento de PDF utilizado para determinar la conformidad de PDF/A.**

Se debe hacer referencia a un documento de PDF y pasarlo al servicio Assembler para determinar si el documento de PDF es compatible con el PDF/A.

**Establecer opciones en tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlen el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede establecer una opción que indique al servicio Assembler que continúe procesando un trabajo si se produce un error. Para obtener información acerca de las opciones en tiempo de ejecución que puede establecer, vea la `AssemblerOptionSpec` referencia de clase en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Recuperar información sobre el documento del PDF**

Después de crear el cliente de servicio Assembler, hacer referencia al documento DDX, hacer referencia a un documento interactivo de PDF y establecer las opciones en tiempo de ejecución, puede invocar el `invokeDDX` operación. Dado que el documento DDX contiene el `DocumentInformation` , el servicio Assembler devuelve datos XML en lugar de un documento de PDF.

**Guardar el documento XML devuelto**

El documento XML que devuelve el servicio Assembler especifica si el documento del PDF de entrada es compatible con el PDF/A. Por ejemplo, si el documento del PDF de entrada no es compatible con el PDF/A, el servicio Assembler devuelve un documento XML que contiene el siguiente elemento:

```xml
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

Guarde el documento XML como archivo XML para poder abrir el archivo y ver los resultados.

**Consulte también**

[Determine si un documento es compatible con el PDF/A mediante la API de Java](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[Determine si un documento es compatible con el PDF/A mediante la API de servicio web](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Determine si un documento es compatible con el PDF/A mediante la API de Java {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

Determine si un documento de PDF es compatible con el PDF/A mediante la API del servicio del ensamblador (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de PDF Assembler.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `AssemblerServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Hacer referencia a un documento DDX existente.

   * Crear un `java.io.FileInputStream` que representa el documento DDX utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo DDX. Para determinar si el documento de PDF es compatible con el PDF/A, asegúrese de que el documento DDX contenga el `PDFAValidation` que está contenido dentro de un `DocumentInformation` Elemento.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Hacer referencia a un documento de PDF utilizado para determinar la conformidad de PDF/A.

   * Crear un `java.io.FileInputStream` mediante su constructor y pasando la ubicación de un documento de PDF que se utiliza para determinar el cumplimiento de PDF/A.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` que contiene el documento de PDF.
   * Crear un `java.util.Map` objeto que se utiliza para almacenar el documento del PDF de entrada mediante un `HashMap` constructor.
   * Añada una entrada a `java.util.Map` invocando su objeto `put` y pasando los siguientes argumentos:

      * Valor de cadena que representa el nombre de clave. Este valor debe coincidir con el valor del elemento de origen especificado en el documento DDX. Por ejemplo, el valor del elemento de origen en el documento DDX que se introduce en esta sección es Loan.pdf.
      * A `com.adobe.idp.Document` que contiene el documento del PDF de entrada.

1. Establecer opciones en tiempo de ejecución.

   * Crear un `AssemblerOptionSpec` que almacena las opciones en tiempo de ejecución mediante su constructor.
   * Establezca opciones en tiempo de ejecución para satisfacer sus necesidades empresariales invocando un método que pertenezca a `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, invoque el `AssemblerOptionSpec` del objeto `setFailOnError` método y pase `false`.

1. Recupere información sobre el documento del PDF.

   Invoque el `AssemblerServiceClient` del objeto `invokeDDX` y pasar los siguientes valores obligatorios:

   * A `com.adobe.idp.Document` que representa el documento DDX a utilizar
   * A `java.util.Map` que contiene el archivo del PDF de entrada que se utiliza para determinar la conformidad del PDF/A
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones en tiempo de ejecución

   El `invokeDDX` El método devuelve un valor `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene datos XML que especifica si el documento del PDF de entrada es compatible con el PDF/A.

1. Guarde el documento XML devuelto.

   Para obtener datos XML que especifiquen si el documento del PDF de entrada es un documento del PDF/A, realice las siguientes acciones:

   * Invoque el `AssemblerResult` del objeto `getDocuments` método. Esto devuelve un `java.util.Map` objeto.
   * Itere a través de `java.util.Map` hasta que encuentre el resultado `com.adobe.idp.Document` objeto.
   * Invoque el `com.adobe.idp.Document` del objeto `copyToFile` para extraer el documento XML. Asegúrese de guardar los datos XML como un archivo XML.

**Consulte también**

[Inicio rápido (modo SOAP): Determinación de si un documento es compatible con el PDF/A mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) (modo SOAP)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Determine si un documento es compatible con el PDF/A mediante la API de servicio web {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

Determine si un documento de PDF es compatible con el PDF/A mediante la API del servicio Assembler (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de PDF Assembler.

   * Crear un `AssemblerServiceClient` mediante su constructor predeterminado.
   * Crear un `AssemblerServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `AssemblerServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Hacer referencia a un documento DDX existente.

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar el documento DDX.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación de archivo del documento DDX y el modo para abrir el archivo en.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.

1. Hacer referencia a un documento de PDF utilizado para determinar la conformidad de PDF/A.

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar el documento del PDF de entrada.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento del PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.
   * Crear un `MyMapOf_xsd_string_To_xsd_anyType` objeto. Este objeto de colección se utiliza para almacenar el documento de PDF.
   * Crear un `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Asigne un valor de cadena que represente el nombre de clave al `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key` field. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX.
   * Asigne el `BLOB` que almacena el documento del PDF en `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value` field.
   * Añada el `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto a `MyMapOf_xsd_string_To_xsd_anyType` objeto. Invoque el `MyMapOf_xsd_string_To_xsd_anyType` object&#39; `Add` y pase el `MyMapOf_xsd_string_To_xsd_anyType` objeto.

1. Establecer opciones en tiempo de ejecución.

   * Crear un `AssemblerOptionSpec` que almacena las opciones en tiempo de ejecución mediante su constructor.
   * Establezca las opciones en tiempo de ejecución para satisfacer sus necesidades empresariales asignando un valor a un miembro de datos que pertenezca a `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne a `false` a la `AssemblerOptionSpec` del objeto `failOnError` miembro de datos.

1. Recupere información sobre el documento del PDF.

   Invoque el `AssemblerServiceService` del objeto `invoke` y pasar los siguientes valores:

   * A `BLOB` que representa el documento DDX.
   * El `MyMapOf_xsd_string_To_xsd_anyType` que contiene el documento del PDF de entrada. Sus claves deben coincidir con los nombres de los archivos de origen del PDF y sus valores deben ser `BLOB` que corresponde al archivo del PDF de entrada.
   * Un `AssemblerOptionSpec` que especifica las opciones en tiempo de ejecución.

   El `invoke` El método devuelve un `AssemblerResult` que contiene datos XML que especifican si el documento del PDF de entrada es un documento del PDF/A.

1. Guarde el documento XML devuelto.

   Para obtener datos XML que especifiquen si el documento del PDF de entrada es un documento del PDF/A, realice las siguientes acciones:

   * Acceda a la `AssemblerResult` del objeto `documents` , que es un `Map` que contiene los datos XML que especifican si el documento del PDF de entrada es un documento del PDF/A.
   * Itere a través de `Map` para obtener cada documento resultante. A continuación, convierta el valor de ese miembro de la matriz en un `BLOB`.
   * Extraiga los datos binarios que representan los datos XML accediendo a su `BLOB` del objeto `MTOM` field. Este campo almacena una matriz de bytes en la que puede escribir como archivo XML.

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
