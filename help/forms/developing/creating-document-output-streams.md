---
title: Creación de flujos de salida de documento
seo-title: Creating Document Output Streams
description: Utilice el servicio Output para convertir documentos como formatos de PDF (incluidos documentos de PDF/A), PostScript, Printer Control Language (PCL) y Zebra - ZPL, Intertypes - IPL, Datamax - DPL y TecToshiba - TPCL.
seo-description: Use the Output service to convert documents as PDF (including PDF/A documents), PostScript, Printer Control Language (PCL), and Zebra - ZPL, Intermec - IPL, Datamax - DPL, and TecToshiba - TPCL label formats.
uuid: 80c28efa-35ce-4073-9ca6-2d93bcd67fdd
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: de527d50-991b-4ca3-a8ac-44d5cab988e9
role: Developer
exl-id: a521bfac-f417-4002-9c5c-8d7794d3eec7
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '19016'
ht-degree: 1%

---

# Creación de flujos de salida de documento  {#creating-document-output-streams}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

**Acerca del servicio de salida**

El servicio Output permite generar documentos como PDF (incluidos documentos de PDF/A), PostScript, Printer Control Language (PCL) y los siguientes formatos de etiqueta:

* Zebra - ZPL
* Interė - IPL
* Datamax - DPL
* TecToshiba - TPCL

Con el servicio Output, puede combinar los datos de formulario XML con un diseño de formulario y enviar el documento a una impresora o archivo de red.

Existen dos formas de pasar un diseño de formulario (un archivo XDP) al servicio Output. Puede pasar un `com.adobe.idp.Document` instancia que contiene un diseño de formulario para el servicio Output . O puede pasar un valor de URI que especifique la ubicación del diseño de formulario. Ambas maneras se discuten en *Programación con formularios AEM*.

>[!NOTE]
>
>El servicio Output no admite documentos de Acrobat PDF que contengan secuencias de comandos específicas de objetos de aplicación. No se procesan los documentos del PDF de formularios que contienen secuencias de comandos específicas de objetos de aplicación.

Las siguientes secciones muestran cómo pasar un diseño de formulario al servicio Output utilizando un valor URI:

* [Creación de documentos de PDF](creating-document-output-streams.md#creating-pdf-documents)
* [Creación de documentos de PDF/A](creating-document-output-streams.md#creating-pdf-a-documents)

Las secciones siguientes muestran cómo pasar un diseño de formulario dentro de un `com.adobe.idp.Document` instancia:

* [Pasar documentos ubicados en Content Services (obsoleto) al servicio de salida](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [Creación de documentos del PDF mediante fragmentos](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

Una consideración a la hora de decidir qué técnica utilizar es si obtiene el diseño de formulario de otro servicio de AEM Forms y, a continuación, páselo dentro de un `com.adobe.idp.Document` instancia. Ambas *Pasar documentos al servicio de salida* y *Creación de documentos del PDF mediante fragmentos* las secciones muestran cómo obtener un diseño de formulario de otro servicio de AEM Forms. La primera sección recupera el diseño de formulario de Content Services (obsoleto). La segunda sección recupera el diseño de formulario del servicio Assembler.

Si obtiene el diseño de formulario de una ubicación fija, como el sistema de archivos, puede utilizar cualquiera de estas técnicas. Es decir, puede especificar el valor de URI en un archivo XDP o utilizar un `com.adobe.idp.Document` instancia.

Para pasar un valor de URI que especifique la ubicación del diseño de formulario al crear un documento PDF, utilice la variable `generatePDFOutput` método. Del mismo modo, para pasar un `com.adobe.idp.Document` al servicio Output al crear un documento de PDF, utilice el `generatePDFOutput2` método.

Al enviar un flujo de salida a una impresora de red, también puede utilizar cualquiera de estas técnicas. Para enviar un flujo de salida a una impresora pasando un `com.adobe.idp.Document` instancia que contiene un diseño de formulario, utilice la variable `sendToPrinter2`método. Para enviar un flujo de salida a una impresora pasando un valor de URI, utilice la variable `sendToPrinter`método. La variable *Envío de emisiones de impresión a impresoras* utiliza el `sendToPrinter` método.

Puede realizar estas tareas utilizando el servicio Output :

* [Creación de documentos de PDF](creating-document-output-streams.md#creating-pdf-documents)
* [Creación de documentos de PDF/A](creating-document-output-streams.md#creating-pdf-a-documents)
* [Pasar documentos ubicados en Content Services (obsoleto) al servicio de salida](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [Creación de documentos del PDF mediante fragmentos](creating-document-output-streams.md#creating-pdf-documents-using-fragments)
* [Imprimir en archivos](creating-document-output-streams.md#printing-to-files)
* [Envío de emisiones de impresión a impresoras](creating-document-output-streams.md#sending-print-streams-to-printers)
* [Creación de varios archivos de salida](creating-document-output-streams.md#creating-multiple-output-files)
* [Creación de reglas de búsqueda](creating-document-output-streams.md#creating-search-rules)
* [Acoplamiento de documentos del PDF](creating-document-output-streams.md#flattening-pdf-documents)

>[!NOTE]
>
>Para obtener más información sobre el servicio Output , consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Creación de documentos de PDF {#creating-pdf-documents}

Puede utilizar el servicio Output para crear un documento de PDF basado en un diseño de formulario y en los datos de formulario XML proporcionados. El documento PDF creado por el servicio Output no es un documento PDF interactivo; un usuario no puede introducir ni modificar datos de formulario.

Si desea crear un documento de PDF pensado para el almacenamiento a largo plazo, se recomienda crear un documento de PDF/A. (Consulte [Creación de documentos de PDF/A](creating-document-output-streams.md#creating-pdf-a-documents).)

Para crear un formulario de PDF interactivo que permita a un usuario introducir datos, utilice el servicio Forms. (Consulte [Renderización de PDF forms interactivos](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms).)

>[!NOTE]
>
>Para obtener más información sobre el servicio Output , consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para crear un documento de PDF, realice los pasos siguientes:

1. Incluir archivos de proyecto.
1. Cree un objeto Cliente de salida.
1. Haga referencia a un origen de datos XML.
1. Establezca las opciones de tiempo de ejecución del PDF.
1. Establezca las opciones de procesamiento en tiempo de ejecución.
1. Genere un documento de PDF.
1. Recupere los resultados de la operación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, deberá reemplazar los archivos adobe-Utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms.

**Creación de un objeto de cliente de salida**

Para poder realizar una operación de servicio de salida mediante programación, debe crear un objeto cliente de servicio de salida. Si utiliza la API de Java, cree un `OutputClient` objeto. Si utiliza la API del servicio web de salida, cree un `OutputServiceService` objeto.

**Referencia a un origen de datos XML**

Para combinar datos con el diseño de formulario, debe hacer referencia a un origen de datos XML que contenga datos. Debe existir un elemento XML para cada campo de formulario que desee rellenar con datos. El nombre del elemento XML debe coincidir con el nombre del campo. Se ignora un elemento XML si no se corresponde con un campo de formulario o si el nombre del elemento XML no coincide con el nombre del campo. No es necesario coincidir con el orden en que se muestran los elementos XML si se especifican todos los elementos XML.

Consulte el siguiente ejemplo de formulario de solicitud de préstamo.

![cp_cp_loanformdata](assets/cp_cp_loanformdata.png)

Para combinar datos en este diseño de formulario, debe crear un origen de datos XML que corresponda al formulario. El siguiente XML representa un origen de datos XML XDP que corresponde al formulario de aplicación hipotecaria de ejemplo.

```xml
 <?xml version="1.0" encoding="UTF-8" ?>
 - <xfa:datasets xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
 - <xfa:data>
 - <data>
     - <Layer>
         <closeDate>1/26/2007</closeDate>
         <lastName>Johnson</lastName>
         <firstName>Jerry</firstName>
         <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
         <city>New York</city>
         <zipCode>00501</zipCode>
         <state>NY</state>
         <dateBirth>26/08/1973</dateBirth>
         <middleInitials>D</middleInitials>
         <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
         <phoneNumber>5555550000</phoneNumber>
     </Layer>
     - <Mortgage>
         <mortgageAmount>295000.00</mortgageAmount>
         <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
         <purchasePrice>300000</purchasePrice>
         <downPayment>5000</downPayment>
         <term>25</term>
         <interestRate>5.00</interestRate>
     </Mortgage>
 </data>
 </xfa:data>
 </xfa:datasets>
```

**Establecer opciones de tiempo de ejecución del PDF**

Establezca la opción URI de archivo al crear un documento de PDF. Esta opción especifica el nombre y la ubicación del archivo de PDF que genera el servicio Output.

>[!NOTE]
>
>En lugar de establecer la opción de tiempo de ejecución del URI de archivo, puede recuperar mediante programación el documento del PDF del tipo de datos complejo que devuelve el servicio Output. Sin embargo, al establecer la opción de tiempo de ejecución del URI de archivo, no es necesario crear una lógica de aplicación que recupere mediante programación el documento del PDF.

**Establecer las opciones de procesamiento en tiempo de ejecución**

Al crear un documento PDF, se pueden definir opciones de renderización en tiempo de ejecución. Aunque estas opciones no son necesarias (a diferencia de las opciones de tiempo de ejecución del PDF que son necesarias), puede realizar tareas como mejorar el rendimiento del servicio Output . Por ejemplo, puede almacenar en caché el diseño de formulario que utiliza el servicio Output para mejorar su rendimiento.

Si utiliza un formulario Acrobat etiquetado como entrada, no puede utilizar el Java del servicio de salida o la API del servicio web para desactivar la configuración etiquetada. Si intenta establecer esta opción mediante programación en `false`, el documento de PDF de resultados aún está etiquetado.

>[!NOTE]
>
>Si no especifica opciones de tiempo de ejecución de procesamiento, se utilizan los valores predeterminados. Para obtener información sobre las opciones de procesamiento en tiempo de ejecución, consulte la `RenderOptionsSpec` referencia de clase. (Consulte [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)).

**Generar un documento de PDF**

Después de hacer referencia a un origen de datos XML válido que contiene datos de formulario y de definir las opciones en tiempo de ejecución, puede invocar el servicio Output , que genera un documento PDF.

Al generar un documento de PDF, se especifican los valores de URI necesarios para que el servicio Output cree un documento de PDF. Un diseño de formulario se puede almacenar en ubicaciones como el sistema de archivos del servidor o como parte de una aplicación de AEM Forms. Se puede hacer referencia a un diseño de formulario (u otros recursos, como un archivo de imagen) que existe como parte de una aplicación de Forms mediante el valor URI raíz del contenido `repository:///`. Por ejemplo, considere el siguiente diseño de formulario denominado *Loan.xdp* ubicada dentro de una aplicación de Forms llamada *Aplicaciones/FormsApplication*:

![cp_cp_formrepository](assets/cp_cp_formrepository.png)

Para acceder al archivo Loan.xdp que se muestra en la ilustración anterior, especifique `repository:///Applications/FormsApplication/1.0/FormsFolder/` como el tercer parámetro que se pasa a la variable `OutputClient` del objeto `generatePDFOutput` método. Especifique el nombre del formulario (*Loan.xdp*) como el segundo parámetro pasado al `OutputClient` del objeto `generatePDFOutput` método.

Si el archivo XDP contiene imágenes (u otros recursos como fragmentos), coloque los recursos en la misma carpeta de aplicación que el archivo XDP. AEM Forms utiliza el URI raíz del contenido como ruta base para resolver referencias a imágenes. Por ejemplo, si el archivo Loan.xdp contiene una imagen, asegúrese de colocar la imagen en `Applications/FormsApplication/1.0/FormsFolder/`.

>[!NOTE]
>
>Puede hacer referencia a un URI de aplicación de Forms al invocar la variable `OutputClient` del objeto `generatePDFOutput` o `generatePrintedOutput` métodos.

>[!NOTE]
>
>Para ver un inicio rápido completo que crea un documento de PDF haciendo referencia a un XDP ubicado en una aplicación de Forms, consulte [Inicio rápido (modo EJB): Creación de un documento de PDF basado en un archivo XDP de aplicación mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api).

**Recuperar los resultados de la operación**

Una vez que el servicio Output realiza una operación, devuelve varios elementos de datos, como datos XML de estado, que especifican si la operación se realizó correctamente.

**Consulte también lo siguiente**

[Creación de un documento de PDF mediante la API de Java](creating-document-output-streams.md#create-a-pdf-document-using-the-java-api)

[Creación de un documento de PDF mediante la API de servicio web](creating-document-output-streams.md#create-a-pdf-document-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Creación de un documento de PDF mediante la API de Java {#create-a-pdf-document-using-the-java-api}

Cree un documento de PDF utilizando la API de salida (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-output-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un objeto Cliente de salida.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `OutputClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un origen de datos XML.

   * Cree un `java.io.FileInputStream` objeto que representa el origen de datos XML que se utiliza para rellenar el documento PDF utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo XML.
   * Cree un `com.adobe.idp.Document` usando su constructor. Pase el `java.io.FileInputStream` objeto.

1. Establezca las opciones de tiempo de ejecución del PDF.

   * Cree un `PDFOutputOptionsSpec` usando su constructor.
   * Establezca la opción URI de archivo invocando la variable `PDFOutputOptionsSpec` del objeto `setFileURI` método. Pase un valor de cadena que especifique la ubicación del archivo de PDF que genera el servicio Output. La opción URI de archivo es relativa al servidor de aplicaciones J2EE que aloja AEM Forms, no al equipo cliente.

1. Establezca las opciones de procesamiento en tiempo de ejecución.

   * Cree un `RenderOptionsSpec` usando su constructor.
   * Almacene en caché el diseño de formulario para mejorar el rendimiento del servicio Output invocando el `RenderOptionsSpec` del objeto `setCacheEnabled` y pasar `true`.

   >[!NOTE]
   >
   >No se puede establecer la versión del documento del PDF utilizando la variable `RenderOptionsSpec` del objeto `setPdfVersion` método si el documento de entrada es un formulario de Acrobat (un formulario creado en Acrobat) o un documento XFA que está firmado o certificado. El documento del PDF de salida conserva la versión original del PDF. Del mismo modo, no puede establecer la opción Adobe PDF etiquetada invocando la variable `RenderOptionsSpec` del objeto `setTaggedPDF` método si el documento de entrada es un formulario de Acrobat o un documento XFA firmado o certificado.

   >[!NOTE]
   >
   >No se puede establecer la opción de PDF linealizado utilizando la variable `RenderOptionsSpec` del objeto `setLinearizedPDF` método si el documento del PDF de entrada está certificado o firmado digitalmente. (Consulte [Firma digital de documentos PDF ](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. Genere un documento de PDF.

   Cree un documento de PDF invocando la variable `OutputClient` del objeto `generatePDFOutput` y pasando los siguientes valores:

   * A `TransformationFormat` valor de enumeración. Para generar un documento de PDF, especifique `TransformationFormat.PDF`.
   * Un valor de cadena que especifica el nombre del diseño de formulario.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentra el diseño de formulario.
   * A `PDFOutputOptionsSpec` que contiene opciones de tiempo de ejecución del PDF.
   * A `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * La variable `com.adobe.idp.Document` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario.

   La variable `generatePDFOutput` devuelve un valor `OutputResult` que contiene los resultados de la operación.

   >[!NOTE]
   >
   >Al generar un documento de PDF invocando la variable `generatePDFOutput` Tenga en cuenta que no puede combinar datos con un formulario de PDF XFA que esté firmado o certificado. (Consulte [Firma y certificación digitales de documentos ](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >La variable `OutputResult` del objeto `getRecordLevelMetaDataList` devuelve el método `null`*.*

   >[!NOTE]
   >
   >También puede crear un documento de PDF invocando la variable `OutputClient` del objeto `generatePDFOutput2` método. (Consulte [Pasar documentos ubicados en Content Services (obsoleto) al servicio de salida ](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*.)*

1. Recupere los resultados de la operación.

   * Recuperar un `com.adobe.idp.Document` objeto que representa el estado del `generatePDFOutput` mediante la invocación de la función `OutputResult` del objeto `getStatusDoc` método. Este método devuelve datos XML de estado que especifican si la operación se realizó correctamente.
   * Cree un `java.io.File` que contiene los resultados de la operación. Asegúrese de que la extensión del nombre de archivo es .xml.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `com.adobe.idp.Document` al archivo (asegúrese de usar la variable `com.adobe.idp.Document` objeto devuelto por el `getStatusDoc` método).

   Aunque el servicio Output escribe el documento del PDF en la ubicación especificada por el argumento que se pasa al `PDFOutputOptionsSpec` del objeto `setFileURI` , puede recuperar mediante programación el documento PDF/A invocando el método `OutputResult` del objeto `getGeneratedDoc` método.

**Consulte también lo siguiente**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Inicio rápido (modo EJB): Creación de un documento de PDF mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[Inicio rápido (modo SOAP): Creación de un documento de PDF mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creación de un documento de PDF mediante la API de servicio web {#create-a-pdf-document-using-the-web-service-api}

Cree un documento de PDF mediante la API de salida (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto Cliente de salida.

   * Cree un `OutputServiceClient` usando su constructor predeterminado.
   * Cree un `OutputServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para usar MTOM.
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `OutputServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un origen de datos XML.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar datos XML que se combinarán con el documento del PDF.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo XML que contiene los datos del formulario.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Establecer opciones de tiempo de ejecución del PDF

   * Cree un `PDFOutputOptionsSpec` usando su constructor.
   * Establezca la opción URI de archivo asignando un valor de cadena que especifique la ubicación del archivo de PDF que genera el servicio de salida al `PDFOutputOptionsSpec` del objeto `fileURI` miembro de datos. La opción URI de archivo es relativa al servidor de aplicaciones J2EE que aloja AEM Forms, no al equipo cliente.

1. Establezca las opciones de procesamiento en tiempo de ejecución.

   * Cree un `RenderOptionsSpec` usando su constructor.
   * Almacene en caché el diseño de formulario para mejorar el rendimiento del servicio Output asignando el valor `true` a `RenderOptionsSpec` del objeto `cacheEnabled` miembro de datos.

   >[!NOTE]
   >
   >No se puede establecer la versión del documento del PDF utilizando la variable `RenderOptionsSpec` del objeto `setPdfVersion` método si el documento de entrada es un formulario de Acrobat (un formulario creado en Acrobat) o un documento XFA que está firmado o certificado. El documento del PDF de salida conserva la versión original del PDF. Del mismo modo, no puede establecer la opción Adobe PDF etiquetada invocando la variable `RenderOptionsSpec` del objeto `setTaggedPDF`* método si el documento de entrada es un formulario de Acrobat o un documento XFA firmado o certificado.*

   >[!NOTE]
   >
   >No se puede establecer la opción de PDF linealizado utilizando la variable `RenderOptionsSpec` del objeto `linearizedPDF` miembro si el documento del PDF de entrada está certificado o firmado digitalmente. (Consulte [Firma digital de documentos PDF ](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. Genere un documento de PDF.

   Cree un documento de PDF invocando la variable `OutputServiceService` del objeto `generatePDFOutput`y pasando los siguientes valores:

   * A `TransformationFormat` valor de enumeración. Para generar un documento de PDF, especifique `TransformationFormat.PDF`.
   * Un valor de cadena que especifica el nombre del diseño de formulario.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentra el diseño de formulario.
   * A `PDFOutputOptionsSpec` que contiene opciones de tiempo de ejecución del PDF.
   * A `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * La variable `BLOB` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario.
   * A `BLOB` objeto que rellena el `generatePDFOutput` método. La variable `generatePDFOutput` rellena este objeto con metadatos generados que describen el documento. (Este valor de parámetro solo es necesario para la invocación de servicio web).
   * A `BLOB` objeto que rellena el `generatePDFOutput` método. La variable `generatePDFOutput` rellena este objeto con datos de resultado. (Este valor de parámetro solo es necesario para la invocación de servicio web).
   * Un `OutputResult` que contiene los resultados de la operación. (Este valor de parámetro solo es necesario para la invocación de servicio web).

   >[!NOTE]
   >
   >Al generar un documento de PDF invocando la variable `generatePDFOutput` Tenga en cuenta que no puede combinar datos con un formulario de PDF XFA que esté firmado o certificado. (Consulte [Firma y certificación digitales de documentos ](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >También puede crear un documento de PDF invocando la variable `OutputClient` del objeto `generatePDFOutput2` método. (Consulte [Pasar documentos ubicados en Content Services (obsoleto) al servicio de salida ](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*.)*

1. Recupere los resultados de la operación.

   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa una ubicación de archivo XML que contiene datos de resultados. Asegúrese de que la extensión del nombre de archivo es .xml.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto que el `OutputServiceService` del objeto `generatePDFOutput` (el octavo parámetro). Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` `field`.
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en el archivo XML invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

   Consulte también

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

   >[!NOTE]
   >
   >La variable `OutputServiceService` del objeto `generateOutput` está en desuso.

## Creación de documentos de PDF/A {#creating-pdf-a-documents}

Puede utilizar el servicio Output para crear un documento PDF/A. Como PDF/A es un formato de archivo para la preservación a largo plazo del contenido del documento, todas las fuentes están incrustadas y el archivo no está comprimido. Como resultado, un documento PDF/A suele ser más grande que un documento PDF estándar. Además, un documento PDF/A no contiene contenido de audio y vídeo. Al igual que otras tareas del servicio de salida, se proporciona un diseño de formulario y datos para combinar con un diseño de formulario para crear un documento PDF/A.

La especificación del PDF/A-1 consta de dos niveles de conformidad, a saber, a y b. La principal diferencia entre ambos es la compatibilidad con la estructura lógica (accesibilidad), que no es necesaria para el nivel de conformidad b. Independientemente del nivel de conformidad, PDF/A-1 dicta que todas las fuentes están incrustadas en el documento PDF/A generado.

Aunque el PDF/A es el estándar para archivar documentos de PDF, no es obligatorio que el PDF/A se utilice para archivar si un documento de PDF estándar satisface las necesidades de su empresa. El propósito de la norma de PDF/A es crear un archivo de PDF que pueda almacenarse durante un largo período de tiempo, así como cumplir los requisitos de conservación de documentos. Por ejemplo, una URL no se puede incrustar en un PDF/A porque con el tiempo la URL puede no ser válida.

Su organización debe evaluar sus propias necesidades, el tiempo durante el cual desea mantener el documento, las consideraciones sobre el tamaño del archivo y determinar su propia estrategia de archiving. Puede determinar mediante programación si un documento de PDF es compatible con PDF/A mediante el servicio DocConverter. (Consulte [Determinación programática del cumplimiento de PDF/A](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

Un documento PDF/A debe utilizar la fuente especificada en el diseño de formulario y no se pueden sustituir las fuentes. Como resultado, si una fuente ubicada dentro de un documento de PDF no está disponible en el sistema operativo del host (OS), se produce una excepción.

Cuando se abre un documento PDF/A en Acrobat, se muestra un mensaje que confirma que el documento es un documento PDF/A, como se muestra en la siguiente ilustración.

![cp_cp_pdfamessage](assets/cp_cp_pdfamessage.png)

>[!NOTE]
>
>El sitio web de AIIM tiene una sección de preguntas frecuentes sobre PDF/A a la que puede acceder desde [https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml](https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml).

>[!NOTE]
>
>Para obtener más información sobre el servicio Output , consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_65).

### Resumen de los pasos {#summary_of_steps-1}

Para crear un documento PDF/A, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto Cliente de salida.
1. Haga referencia a un origen de datos XML.
1. Establezca las opciones de PDF/A en tiempo de ejecución.
1. Establezca las opciones de procesamiento en tiempo de ejecución.
1. Genere un documento PDF/A.
1. Recupere los resultados de la operación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación personalizada mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, deberá reemplazar los archivos adobe-Utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms.

**Creación de un objeto de cliente de salida**

Para poder realizar una operación de servicio de salida mediante programación, debe crear un objeto cliente de servicio de salida. Si utiliza la API de Java, cree un `OutputClient` objeto. Si utiliza la API del servicio web de salida, cree un `OutputServiceService` objeto.

**Referencia a un origen de datos XML**

Para combinar datos con el diseño de formulario, debe hacer referencia a un origen de datos XML que contenga datos. Debe existir un elemento XML para cada campo de formulario que desee rellenar con datos. El nombre del elemento XML debe coincidir con el nombre del campo. Se ignora un elemento XML si no se corresponde con un campo de formulario o si el nombre del elemento XML no coincide con el nombre del campo. No es necesario coincidir con el orden en que se muestran los elementos XML si se especifican todos los elementos XML.

**Establecer opciones de tiempo de ejecución del PDF/A**

Puede establecer la opción URI de archivo al crear un documento PDF/A. El URI es relativo al servidor de aplicaciones J2EE que aloja AEM Forms. Es decir, si establece C:\Adobe, el archivo se escribe en la carpeta del servidor, no en el equipo cliente. El URI especifica el nombre y la ubicación del archivo PDF/A que genera el servicio Output.

**Establecer las opciones de procesamiento en tiempo de ejecución**

Puede definir opciones de procesamiento en tiempo de ejecución al crear documentos de PDF/A. Dos opciones relacionadas con el PDF/A que puede establecer son la `PDFAConformance` y `PDFARevisionNumber` valores. La variable `PDFAConformance` se refiere a la forma en que un documento PDF se adhiere a los requisitos que especifican cómo se conservan los documentos electrónicos a largo plazo. Los valores válidos para esta opción son `A` y `B`. Para obtener información sobre la conformidad con los niveles a y b, consulte la especificación ISO PDF/A-1 con título *ISO 19005-1 Gestión de documentos*.

La variable `PDFARevisionNumber` hace referencia al número de revisión de un documento PDF/A. Para obtener información sobre el número de revisión de un documento PDF/A, consulte la especificación ISO PDF/A-1 con título *ISO 19005-1 Gestión de documentos*.

>[!NOTE]
>
>No puede establecer la opción Adobe PDF etiquetado en `false` al crear un documento PDF/A 1A. PDF/A 1A siempre será un documento PDF etiquetado. Además, no puede establecer la opción Adobe PDF etiquetado en `true` al crear un documento PDF/A 1B. PDF/A 1B siempre será un documento PDF sin etiquetar.

**Generación de un documento PDF/A**

Después de hacer referencia a un origen de datos XML válido que contiene datos de formulario y de definir las opciones en tiempo de ejecución, puede invocar el servicio Output, lo que hace que genere un documento PDF/A.

**Recuperar los resultados de la operación**

Una vez que el servicio Output realiza una operación, devuelve varios elementos de datos, como datos XML, que especifican si la operación se realizó correctamente.

**Consulte también lo siguiente**

[Creación de un documento de PDF/A mediante la API de Java](creating-document-output-streams.md#create-a-pdf-a-document-using-the-java-api)

[Creación de un documento de PDF/A mediante la API de servicio web](creating-document-output-streams.md#create-a-pdf-a-document-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Creación de un documento de PDF/A mediante la API de Java {#create-a-pdf-a-document-using-the-java-api}

Cree un documento PDF/A utilizando la API de salida (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-output-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un objeto Cliente de salida.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `OutputClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un origen de datos XML.

   * Cree un `java.io.FileInputStream` objeto que representa el origen de datos XML que se utiliza para rellenar el documento PDF/A utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo XML.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Establezca las opciones de PDF/A en tiempo de ejecución.

   * Cree un `PDFOutputOptionsSpec` usando su constructor.
   * Establezca la opción URI de archivo invocando la variable `PDFOutputOptionsSpec` del objeto `setFileURI` método. Pase un valor de cadena que especifique la ubicación del archivo de PDF que genera el servicio Output. La opción URI de archivo es relativa al servidor de aplicaciones J2EE que aloja AEM Forms, no al equipo cliente.

1. Establezca las opciones de procesamiento en tiempo de ejecución.

   * Cree un `RenderOptionsSpec` usando su constructor.
   * Configure las variables `PDFAConformance` invocando la variable `RenderOptionsSpec` del objeto `setPDFAConformance` método y pasar una `PDFAConformance` valor de enumeración que especifica el nivel de conformidad. Por ejemplo, para especificar el nivel de conformidad A, pase `PDFAConformance.A`.
   * Configure las variables `PDFARevisionNumber` invocando la variable `RenderOptionsSpec` del objeto `setPDFARevisionNumber` método y paso `PDFARevisionNumber.Revision_1`.

   >[!NOTE]
   >
   >La versión de PDF de un documento de PDF/A es 1.4 independientemente del valor que especifique para la variable `RenderOptionsSpec` del objeto `setPdfVersion`*método.*

1. Genere un documento PDF/A.

   Cree un documento de PDF/A invocando la variable `OutputClient` del objeto `generatePDFOutput` y pasando los siguientes valores:

   * A `TransformationFormat` valor de enumeración. Para generar un documento de PDF/A, especifique `TransformationFormat.PDFA`.
   * Un valor de cadena que especifica el nombre del diseño de formulario.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentra el diseño de formulario.
   * A `PDFOutputOptionsSpec` que contiene opciones de tiempo de ejecución del PDF.
   * A `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * La variable `com.adobe.idp.Document` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario.

   La variable `generatePDFOutput` devuelve un valor `OutputResult` que contiene los resultados de la operación.

   >[!NOTE]
   >
   >La variable `OutputResult` del objeto `getRecordLevelMetaDataList` devuelve el método `null`.

   >[!NOTE]
   >
   >También puede crear un documento /A de PDF invocando la variable `OutputClient` del objeto `generatePDFOutput`2. (Consulte [Pasar documentos ubicados en Content Services (obsoleto) al servicio de salida](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service).)

1. Recupere los resultados de la operación.

   * Cree un `com.adobe.idp.Document` objeto que representa el estado del `generatePDFOutput` invocando el método `OutputResult` del objeto `getStatusDoc` método.
   * Cree un `java.io.File` que contendrá los resultados de la operación. Asegúrese de que la extensión del nombre de archivo es .xml.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `com.adobe.idp.Document` al archivo (asegúrese de usar la variable `com.adobe.idp.Document` objeto devuelto por el `getStatusDoc` método).

   >[!NOTE]
   >
   >Aunque el servicio Output escribe el documento PDF/A en la ubicación especificada por el argumento que se pasa al `PDFOutputOptionsSpec` del objeto `setFileURI` , puede recuperar mediante programación el documento PDF/A invocando el método `OutputResult` del objeto `getGeneratedDoc` método.

**Consulte también lo siguiente**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Inicio rápido (modo SOAP): Creación de un documento de PDF/A mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### Creación de un documento de PDF/A mediante la API de servicio web {#create-a-pdf-a-document-using-the-web-service-api}

Cree un documento PDF/A utilizando la API de salida (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto Cliente de salida.

   * Cree un `OutputServiceClient` usando su constructor predeterminado.
   * Cree un `OutputServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para usar MTOM.
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `OutputServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un origen de datos XML.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar datos que se combinarán con el documento PDF/A.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF que se va a cifrar y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Establezca las opciones de PDF/A en tiempo de ejecución.

   * Cree un `PDFOutputOptionsSpec` usando su constructor.
   * Establezca la opción URI de archivo asignando un valor de cadena que especifique la ubicación del archivo de PDF que genera el servicio de salida al `PDFOutputOptionsSpec` del objeto `fileURI` miembro de datos. La opción URI de archivo es relativa al servidor de aplicaciones J2EE que aloja AEM Forms, no al equipo cliente

1. Establezca las opciones de procesamiento en tiempo de ejecución.

   * Cree un `RenderOptionsSpec` usando su constructor.
   * Configure las variables `PDFAConformance` asignando un `PDFAConformance` valor de enumeración de `RenderOptionsSpec` del objeto `PDFAConformance` miembro de datos. Por ejemplo, para especificar el nivel de conformidad A, asigne `PDFAConformance.A` a este miembro de datos.
   * Configure las variables `PDFARevisionNumber` asignando un `PDFARevisionNumber` valor de enumeración de `RenderOptionsSpec` del objeto `PDFARevisionNumber` miembro de datos. Asignar `PDFARevisionNumber.Revision_1` a este miembro de datos.

   >[!NOTE]
   >
   >La versión PDF de un documento PDF/A es 1.4 independientemente del valor que especifique.

1. Genere un documento PDF/A.

   Cree un documento de PDF invocando la variable `OutputServiceService` del objeto `generatePDFOutput`y pasando los siguientes valores:

   * Un valor de enumeración TransformationFormat. Para generar un documento de PDF, especifique `TransformationFormat.PDFA`.
   * Un valor de cadena que especifica el nombre del diseño de formulario.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentra el diseño de formulario.
   * A `PDFOutputOptionsSpec` que contiene opciones de tiempo de ejecución del PDF.
   * A `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * La variable `BLOB` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario.
   * A `BLOB` objeto que rellena el `generatePDFOutput` método. La variable `generatePDFOutput` rellena este objeto con metadatos generados que describen el documento. (Este valor de parámetro solo es necesario para invocar un servicio web).
   * A `BLOB` objeto que rellena el `generatePDFOutput` método. La variable `generatePDFOutput` rellena este objeto con datos de resultado. (Este valor de parámetro solo es necesario para invocar un servicio web).
   * Un `OutputResult` que contiene los resultados de la operación. (Este valor de parámetro solo es necesario para invocar un servicio web).

   >[!NOTE]
   >
   >También puede crear un documento /A de PDF invocando la variable `OutputClient` del objeto `generatePDFOutput`2. (Consulte [Pasar documentos ubicados en Content Services (obsoleto) al servicio de salida](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service).)

1. Recupere los resultados de la operación.

   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa una ubicación de archivo XML que contiene datos de resultados. Asegúrese de que la extensión del nombre de archivo es .xml.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto que el `OutputServiceService` del objeto `generatePDFOutput` (el octavo parámetro). Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` campo .
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en el archivo XML invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Pasar documentos ubicados en Content Services (obsoleto) al servicio de salida {#passing-documents-located-in-content-services-deprecated-to-the-output-service}

El servicio Output procesa un formulario de PDF no interactivo basado en un diseño de formulario que normalmente se guarda como archivo XDP y se crea en Designer. Puede pasar un `com.adobe.idp.Document` objeto que contiene el diseño de formulario en el servicio Output. A continuación, el servicio Output procesa el diseño de formulario ubicado en la variable `com.adobe.idp.Document` objeto.

Una ventaja de pasar un `com.adobe.idp.Document` al servicio de salida es que otras operaciones de servicio de AEM Forms devuelven un `com.adobe.idp.Document` instancia. Es decir, puede obtener un `com.adobe.idp.Document` de otra operación de servicio y renderícela. Por ejemplo, supongamos que un archivo XDP se almacena en un nodo de Content Services (obsoleto) denominado `/Company Home/Form Designs`, como se muestra en la siguiente ilustración.

Puede recuperar mediante programación Loan.xdp de Content Services (obsoleto) y pasar el archivo XDP al servicio Output dentro de un `com.adobe.idp.Document` objeto.

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-2}

Para pasar un documento obtenido de Content Services (desaprobada) al servicio Output , realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto Output y un objeto Document Management Client API.
1. Recupere el diseño de formulario de Content Services (obsoleto).
1. Procese el formulario de PDF no interactivo.
1. Realice una acción con el flujo de datos.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

**Creación de una salida y un objeto de API de cliente de Document Management**

Para poder realizar mediante programación una operación de API de servicio de salida, cree un objeto de API de cliente de salida. Además, como este flujo de trabajo recupera un archivo XDP de Content Services (obsoleto), cree un objeto de API de Document Management.

**Recuperar el diseño de formulario de Content Services (obsoleto)**

Recupere el archivo XDP de Content Services (obsoleto) mediante Java o la API de servicio web. El archivo XDP se devuelve dentro de un `com.adobe.idp.Document` instancia (o una `BLOB` instancia si utiliza servicios web). A continuación, puede pasar la variable `com.adobe.idp.Document` al servicio Output.

**Representar el formulario de PDF no interactivo**

Para procesar un formulario no interactivo, pase el `com.adobe.idp.Document` instancia que se devolvió de Content Services (desaprobada) al servicio de salida.

>[!NOTE]
>
>Dos métodos nuevos denominados `generatePDFOutput2`y g `eneratePrintedOutput2`aceptar `com.adobe.idp.Document` objeto que contiene un diseño de formulario. También puede pasar un `com.adobe.idp.Document`que contiene el diseño de formulario al servicio Output al enviar una secuencia de impresión a una impresora de red.

**Realizar una acción con el flujo de datos del formulario**

Puede guardar el formulario no interactivo como un archivo PDF. El formulario se puede ver en Adobe Reader o Acrobat.

**Consulte también lo siguiente**

[Pasar documentos al servicio de salida mediante la API de Java](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-java-api)

[Pasar documentos al servicio de salida mediante la API de servicio web](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[Creación de documentos del PDF mediante fragmentos](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

### Pasar documentos al servicio de salida mediante la API de Java {#pass-documents-to-the-output-service-using-the-java-api}

Pase un documento recuperado de Content Services (desaprobada) mediante el servicio de salida y la API de Content Services (desaprobada) (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-output-client.jar y adobe-contentservices-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un objeto Output y un objeto Document Management Client API.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión. (Consulte [Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Cree un `OutputClient` usando su constructor y pasando el `ServiceClientFactory` objeto.
   * Cree un `DocumentManagementServiceClientImpl` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recupere el diseño de formulario de Content Services (obsoleto).

   Invocar el `DocumentManagementServiceClientImpl` del objeto `retrieveContent` y pase los siguientes valores:

   * Un valor de cadena que especifica el almacén donde se agrega el contenido. El almacén predeterminado es `SpacesStore`. Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la ruta completa del contenido que se va a recuperar (por ejemplo, `/Company Home/Form Designs/Loan.xdp`). Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la versión. Este valor es un parámetro opcional y puede pasar una cadena vacía. En este caso, se recupera la versión más reciente.

   La variable `retrieveContent` el método devuelve un `CRCResult` que contiene el archivo XDP. Recuperar un `com.adobe.idp.Document` invocando la variable `CRCResult` del objeto `getDocument` método.

1. Procese el formulario de PDF no interactivo.

   Invocar el `OutputClient` del objeto `generatePDFOutput2` y pase los siguientes valores:

   * A `TransformationFormat` valor de enumeración. Para generar un documento de PDF, especifique `TransformationFormat.PDF`.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentran los recursos adicionales, como imágenes.
   * A `com.adobe.idp.Document` objeto que representa el diseño de formulario (utilice la instancia devuelta por la variable `CRCResult` del objeto `getDocument` método).
   * A `PDFOutputOptionsSpec` que contiene opciones de tiempo de ejecución del PDF.
   * A `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * La variable `com.adobe.idp.Document` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario.

   La variable `generatePDFOutput2` devuelve un valor `OutputResult` que contiene los resultados de la operación.

1. Realice una acción con la secuencia de datos del formulario.

   * Recuperar un `com.adobe.idp.Document` objeto que representa el formulario no interactivo invocando la variable `OutputResult` del objeto `getGeneratedDoc` método.
   * Cree un `java.io.File` que contiene los resultados de la operación. Asegúrese de que la extensión del nombre de archivo es .pdf.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `com.adobe.idp.Document` al archivo (asegúrese de usar la variable `com.adobe.idp.Document` objeto devuelto por el `getGeneratedDoc` método).

**Consulte también lo siguiente**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Inicio rápido (modo EJB): Pasar documentos al servicio de salida mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[Inicio rápido (modo SOAP): Pasar documentos al servicio de salida mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Pasar documentos al servicio de salida mediante la API de servicio web {#pass-documents-to-the-output-service-using-the-web-service-api}

Pase un documento recuperado de Content Services (desaprobada) mediante el servicio de salida y la API de Content Services (desaprobada) (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Dado que esta aplicación cliente invoca dos servicios de AEM Forms, cree dos referencias de servicio. Utilice la siguiente definición WSDL para la referencia de servicio asociada al servicio Output : `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   Utilice la siguiente definición WSDL para la referencia de servicio asociada al servicio de gestión de documentos: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Porque la variable `BLOB` el tipo de datos es común a ambas referencias de servicio; califique completamente la variable `BLOB` tipo de datos al utilizarla. En el inicio rápido correspondiente del servicio web, todas las `BLOB` las instancias están completamente cualificadas.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto Output y un objeto Document Management Client API.

   * Cree un `OutputServiceClient` usando su constructor predeterminado.
   * Cree un `OutputServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de Forms (por ejemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`). No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `OutputServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Repita estos pasos para el `DocumentManagementServiceClient`cliente de servicio.

1. Recupere el diseño de formulario de Content Services (obsoleto).

   Recupere contenido invocando la variable `DocumentManagementServiceClient` del objeto `retrieveContent` y pasando los siguientes valores:

   * Un valor de cadena que especifica el almacén donde se agrega el contenido. El almacén predeterminado es `SpacesStore`. Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la ruta completa del contenido que se va a recuperar (por ejemplo, `/Company Home/Form Designs/Loan.xdp`). Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la versión. Este valor es un parámetro opcional y puede pasar una cadena vacía. En este caso, se recupera la versión más reciente.
   * Un parámetro de salida de cadena que almacena el valor del vínculo de navegación.
   * A `BLOB` parámetro de salida que almacena el contenido. Puede utilizar este parámetro de salida para recuperar el contenido.
   * A `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` parámetro de salida que almacena atributos de contenido.
   * A `CRCResult` parámetro de salida. En lugar de usar este objeto, puede usar la variable `BLOB` parámetro de salida para recuperar el contenido.

1. Procese el formulario de PDF no interactivo.

   Invocar el `OutputServiceClient` del objeto `generatePDFOutput2` y pase los siguientes valores:

   * A `TransformationFormat` valor de enumeración. Para generar un documento de PDF, especifique `TransformationFormat.PDF`.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentran los recursos adicionales, como imágenes.
   * A `BLOB` objeto que representa el diseño de formulario (utilice el `BLOB` instancia devuelta por Content Services (desaprobada).
   * A `PDFOutputOptionsSpec` que contiene opciones de tiempo de ejecución del PDF.
   * A `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * La variable `BLOB` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario.
   * Una salida `BLOB` objeto que rellena el `generatePDFOutput2` método. La variable `generatePDFOutput2` rellena este objeto con metadatos generados que describen el documento. (Este valor de parámetro solo es necesario para la invocación de servicio web).
   * Una salida `OutputResult` que contiene los resultados de la operación. (Este valor de parámetro solo es necesario para la invocación de servicio web).

   La variable `generatePDFOutput2` el método devuelve un `BLOB` objeto que contiene el formulario de PDF no interactivo.

1. Realice una acción con la secuencia de datos del formulario.

   * Cree un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento del PDF interactivo y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto recuperado del `generatePDFOutput2` método. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` miembro de datos.
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Pasar documentos ubicados en el Repositorio al Servicio de Salida {#passing-documents-located-in-the-repository-to-the-output-service}

El servicio Output procesa un formulario de PDF no interactivo basado en un diseño de formulario que normalmente se guarda como archivo XDP y se crea en Designer. Puede pasar un `com.adobe.idp.Document` objeto que contiene el diseño de formulario en el servicio Output. A continuación, el servicio Output procesa el diseño de formulario ubicado en la variable `com.adobe.idp.Document` objeto.

Una ventaja de pasar un `com.adobe.idp.Document` al servicio de salida es que otras operaciones de servicio de AEM Forms devuelven un `com.adobe.idp.Document` instancia. Es decir, puede obtener un `com.adobe.idp.Document` de otra operación de servicio y renderícela. Por ejemplo, suponga que un archivo XDP se almacena en el repositorio de AEM Forms, como se muestra en la siguiente ilustración.

![pd_pd_formrepository](assets/pd_pd_formrepository.png)

La variable *FormsFolder* es una ubicación definida por el usuario en el repositorio de AEM Forms (esta ubicación es un ejemplo y no existe de forma predeterminada). En este ejemplo, un diseño de formulario llamado Loan.xdp se encuentra en esta carpeta. Además del diseño de formulario, en esta ubicación se pueden almacenar otros materiales de formulario, como imágenes. La ruta a un recurso ubicado en el repositorio de AEM Forms es:

`Applications/Application-name/Application-version/Folder.../Filename`

Puede recuperar mediante programación Loan.xdp del repositorio de AEM Forms y pasarlo al servicio Output dentro de un `com.adobe.idp.Document` objeto.

Puede crear un PDF basado en un archivo XDP ubicado en el repositorio de una de las dos maneras siguientes. Puede pasar la ubicación XDP por referencia o puede recuperar el XDP del repositorio mediante programación y pasarlo al servicio Output dentro de un archivo XDP.

[Inicio rápido (modo EJB): Creación de un documento de PDF basado en un archivo XDP de aplicación mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api) (muestra cómo pasar la ubicación del archivo XDP por referencia).

[Inicio rápido (modo EJB): Pasar un documento ubicado en el repositorio de AEM Forms al servicio de salida mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) (muestra cómo recuperar mediante programación el archivo XDP del repositorio de AEM Forms y pasarlo al servicio Output dentro de un `com.adobe.idp.Document` ). (Esta sección describe cómo realizar esta tarea)

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-3}

Para pasar un documento obtenido del repositorio de AEM Forms al servicio Output , realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto Output y un objeto Document Management Client API.
1. Recupere el diseño de formulario del repositorio de AEM Forms.
1. Procese el formulario de PDF no interactivo.
1. Realice una acción con el flujo de datos.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

**Creación de una salida y un objeto de API de cliente de Document Management**

Para poder realizar mediante programación una operación de API de servicio de salida, cree un objeto de API de cliente de salida. Además, como este flujo de trabajo recupera un archivo XDP de Content Services (obsoleto), cree un objeto de API de Document Management.

**Recupere el diseño de formulario del repositorio de AEM Forms**

Recupere el archivo XDP del repositorio de AEM Forms utilizando la API del repositorio. (Consulte [Leer recursos](/help/forms/developing/aem-forms-repository.md#reading-resources).)

El archivo XDP se devuelve dentro de un `com.adobe.idp.Document` instancia (o una `BLOB` instancia si utiliza servicios web). A continuación, puede pasar la variable `com.adobe.idp.Document` del servicio Output.

**Representar el formulario de PDF no interactivo**

Para procesar un formulario no interactivo, pase el `com.adobe.idp.Document` instancia que se devolvió mediante la API del repositorio de AEM Forms.

>[!NOTE]
>
>Dos métodos nuevos denominados `generatePDFOutput2`y `generatePrintedOutput2`aceptar `com.adobe.idp.Document`objeto que contiene un diseño de formulario. También puede pasar un `com.adobe.idp.Document` que contiene el diseño de formulario al servicio Output al enviar una secuencia de impresión a una impresora de red.

**Realizar una acción con el flujo de datos del formulario**

Puede guardar el formulario no interactivo como un archivo PDF. El formulario se puede ver en Adobe Reader o Acrobat.

**Consulte también lo siguiente**

[Pasar documentos ubicados en el repositorio al servicio de salida mediante la API de Java](creating-document-output-streams.md#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

ResourceRepositoryClient

### Pasar documentos ubicados en el repositorio al servicio de salida mediante la API de Java {#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api}

Pase un documento recuperado del repositorio utilizando el servicio de salida y la API del repositorio (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-output-client.jar y adobe-repository-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un objeto Output y un objeto Document Management Client API.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión. (Consulte [Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Cree un `OutputClient` usando su constructor y pasando el `ServiceClientFactory` objeto.
   * Cree un `DocumentManagementServiceClientImpl` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recupere el diseño de formulario del repositorio de AEM Forms.

   Invocar el `ResourceRepositoryClient` del objeto `readResourceContent` y pase un valor de cadena que especifique la ubicación de URI al archivo XDP. Por ejemplo, `/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`. Este valor es obligatorio. Este método devuelve un `com.adobe.idp.Document` que representa el archivo XDP.

1. Procese el formulario de PDF no interactivo.

   Invocar el `OutputClient` del objeto `generatePDFOutput2` y pase los siguientes valores:

   * A `TransformationFormat` valor de enumeración. Para generar un documento de PDF, especifique `TransformationFormat.PDF`.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentran los recursos adicionales, como imágenes. Por ejemplo, `repository:///Applications/FormsApplication/1.0/FormsFolder/`.
   * A `com.adobe.idp.Document` objeto que representa el diseño de formulario (utilice la instancia devuelta por la variable `ResourceRepositoryClient` del objeto `readResourceContent` método).
   * A `PDFOutputOptionsSpec` que contiene opciones de tiempo de ejecución del PDF.
   * A `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * La variable `com.adobe.idp.Document` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario.

   La variable `generatePDFOutput2` devuelve un valor `OutputResult` que contiene los resultados de la operación.

1. Realice una acción con la secuencia de datos del formulario.

   * Recuperar un `com.adobe.idp.Document` objeto que representa el formulario no interactivo invocando la variable `OutputResult` del objeto `getGeneratedDoc` método.
   * Cree un `java.io.File` que contiene los resultados de la operación. Asegúrese de que la extensión del nombre de archivo es .pdf.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `com.adobe.idp.Document` al archivo (asegúrese de usar la variable `com.adobe.idp.Document` objeto devuelto por el `getGeneratedDoc` método).

**Consulte también lo siguiente**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Inicio rápido (modo EJB): Pasar un documento ubicado en el repositorio de AEM Forms al servicio de salida mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Creación de documentos del PDF mediante fragmentos {#creating-pdf-documents-using-fragments}

Puede utilizar los servicios Output y Assembler para crear un flujo de salida, como un documento PDF, basado en fragmentos. El servicio Assembler monta un documento XDP basado en fragmentos ubicados en varios archivos XDP. El documento XDP montado se pasa al servicio Output, que crea un documento PDF. Aunque este flujo de trabajo muestra un documento PDF que se está generando, el servicio Output puede generar otros tipos de salida, como ZPL, para este flujo de trabajo. Un documento PDF se utiliza únicamente para fines de discusión.

La siguiente ilustración muestra este flujo de trabajo.

![cp_cp_outputensambllefragments](assets/cp_cp_outputassemblefragments.png)

Antes de leer *Creación de documentos del PDF mediante fragmentos*, se recomienda familiarizarse con el uso del servicio Assembler para ensamblar varios documentos XDP. (Consulte [Agrupación de varios fragmentos XDP](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments).)

>[!NOTE]
>
>También puede pasar un diseño de formulario montado por el servicio Assembler al servicio Forms en lugar del servicio Output . La diferencia principal entre el servicio Output y el servicio Forms es que el servicio Forms genera documentos de PDF interactivos y el servicio Output produce documentos de PDF no interactivos. Además, el servicio Forms no puede generar flujos de salida basados en impresoras como ZPL.

>[!NOTE]
>
>Para obtener más información sobre el servicio Output , consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-4}

Para crear un documento PDF basado en fragmentos, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto cliente de salida y ensamblador.
1. Utilice el servicio Assembler para generar el diseño de formulario.
1. Utilice el servicio Output para generar el documento de PDF.
1. Guarde el documento de PDF como archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un objeto cliente de salida y ensamblador**

Para poder realizar mediante programación una operación de API de servicio de salida, cree un objeto de API de cliente de salida. Además, como este flujo de trabajo invoca el servicio Assembler para crear el diseño de formulario, cree un objeto de API de cliente Assembler.

**Utilice el servicio Assembler para generar el diseño de formulario**

Utilice el servicio Assembler para generar el diseño de formulario mediante fragmentos. El servicio Assembler devuelve un valor `com.adobe.idp.Document` instancia que contiene el diseño de formulario.

**Utilice el servicio Output para generar el documento del PDF**

Puede utilizar el servicio Output para generar un documento de PDF utilizando el diseño de formulario creado por el servicio Assembler. Pase el `com.adobe.idp.Document` instancia que el servicio Assembler devolvió al servicio Output.

**Guarde el documento del PDF como archivo del PDF**

Una vez que el servicio Output haya creado un documento de PDF, puede guardarlo como archivo de PDF.

**Consulte también lo siguiente**

[Creación de un documento de PDF basado en fragmentos mediante la API de Java](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-java-api)

[Creación de un documento de PDF basado en fragmentos mediante la API de servicio web](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[Agrupación de varios fragmentos XDP](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)

[Creación de documentos de PDF](creating-document-output-streams.md#creating-pdf-documents)

### Creación de un documento de PDF basado en fragmentos mediante la API de Java {#create-a-pdf-document-based-on-fragments-using-the-java-api}

Cree un documento de PDF basado en fragmentos utilizando la API de servicio de salida y la API de servicio de ensamblador (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-output-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un objeto cliente de salida y ensamblador.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `OutputClient` usando su constructor y pasando el `ServiceClientFactory` objeto.
   * Cree un `AssemblerServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Utilice el servicio Assembler para generar el diseño de formulario.

   Invocar el `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores obligatorios:

   * A `com.adobe.idp.Document` que representa el documento DDX que se va a utilizar.
   * A `java.util.Map` objeto que contiene los archivos XDP de entrada.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica las opciones en tiempo de ejecución, incluyendo la fuente predeterminada y el nivel de registro de trabajo.

   La variable `invokeDDX` el método devuelve un `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene el documento XDP montado. Para recuperar el documento XDP montado, realice las siguientes acciones:

   * Invocar el `AssemblerResult` del objeto `getDocuments` método. Este método devuelve un `java.util.Map` objeto.
   * Iterar a través de la variable `java.util.Map` hasta que encuentre el resultado `com.adobe.idp.Document` objeto.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` método para extraer el documento XDP ensamblado.


1. Utilice el servicio Output para generar el documento de PDF.

   Invocar el `OutputClient` del objeto `generatePDFOutput2` y pase los siguientes valores:

   * A `TransformationFormat` valor de enumeración. Para generar un documento de PDF, especifique `TransformationFormat.PDF`
   * Un valor de cadena que especifica la raíz del contenido donde se encuentran los recursos adicionales, como imágenes.
   * A `com.adobe.idp.Document` objeto que representa el diseño de formulario (utilice la instancia devuelta por el servicio Assembler)
   * A `PDFOutputOptionsSpec` objeto que contiene opciones de tiempo de ejecución del PDF
   * A `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución
   * La variable `com.adobe.idp.Document` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario

   La variable `generatePDFOutput2` devuelve un valor `OutputResult` objeto que contiene los resultados de la operación

1. Guarde el documento de PDF como archivo de PDF.

   * Recuperar un `com.adobe.idp.Document` objeto que representa el documento del PDF invocando la variable `OutputResult` del objeto `getGeneratedDoc` método.
   * Cree un `java.io.File` que contiene los resultados de la operación. Asegúrese de que la extensión del nombre del archivo sea .pdf.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `com.adobe.idp.Document` al archivo. (Asegúrese de usar la variable `com.adobe.idp.Document` que la variable `getGeneratedDoc` método devuelto).

**Consulte también lo siguiente**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Inicio rápido (modo EJB): Creación de un documento de PDF basado en fragmentos mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[Inicio rápido (modo SOAP): Creación de un documento de PDF basado en fragmentos mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### Creación de un documento de PDF basado en fragmentos mediante la API de servicio web {#create-a-pdf-document-based-on-fragments-using-the-web-service-api}

Cree un documento de PDF basado en fragmentos utilizando la API del servicio de salida y la API del servicio de ensamblador (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Utilice la siguiente definición WSDL para la referencia de servicio asociada al servicio Output :

   ```java
    http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1.
   ```

   Utilice la siguiente definición WSDL para la referencia de servicio asociada al servicio Assembler:

   ```java
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   Porque la variable `BLOB` el tipo de datos es común a ambas referencias de servicio; califique completamente la variable `BLOB` tipo de datos al utilizarla. En el inicio rápido correspondiente del servicio web, todas las `BLOB` las instancias están completamente cualificadas.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto cliente de salida y ensamblador.

   * Cree un `OutputServiceClient` usando su constructor predeterminado.
   * Cree un `OutputServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para usar MTOM.
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `OutputServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al `OutputServiceClient.ClientCredentials.UserName.UserName`campo .
      * Asigne el valor de contraseña correspondiente a la variable `OutputServiceClient.ClientCredentials.UserName.Password`campo .
      * Asignar el valor constante `HttpClientCredentialType.Basic` a `BasicHttpBindingSecurity.Transport.ClientCredentialType`campo .
   * Asigne la variable `BasicHttpSecurityMode.TransportCredentialOnly` valor constante de la variable `BasicHttpBindingSecurity.Security.Mode`campo .

   >[!NOTE]
   >
   >Repita estos pasos para el `AssemblerServiceClient`objeto.

1. Utilice el servicio Assembler para generar el diseño de formulario.

   Invocar el `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores:

   * A `BLOB` objeto que representa el documento DDX
   * La variable `MyMapOf_xsd_string_To_xsd_anyType` objeto que contiene los archivos necesarios
   * Un `AssemblerOptionSpec` objeto que especifica opciones en tiempo de ejecución

   La variable `invokeDDX` devuelve un valor `AssemblerResult` que contiene los resultados del trabajo y cualquier excepción que se haya producido. Para obtener el documento XDP recién creado, realice las siguientes acciones:

   * Acceda a la `AssemblerResult` del objeto `documents` , que es un `Map` que contiene los documentos de PDF resultantes.
   * Iterar a través de la variable `Map` para recuperar el diseño de formulario ensamblado. Realizar el almacenamiento en la memoria del miembro de la matriz `value` a `BLOB`. Pasa esto `BLOB` al servicio Output.


1. Utilice el servicio Output para generar el documento de PDF.

   Invocar el `OutputServiceClient` del objeto `generatePDFOutput2` y pase los siguientes valores:

   * A `TransformationFormat` valor de enumeración. Para generar un documento de PDF, especifique `TransformationFormat.PDF`.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentran los recursos adicionales, como imágenes.
   * A `BLOB` objeto que representa el diseño de formulario (utilice el `BLOB` instancia devuelta por el servicio Assembler).
   * A `PDFOutputOptionsSpec` que contiene opciones de tiempo de ejecución del PDF.
   * A `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * La variable `BLOB` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario.
   * Una salida `BLOB` que la variable `generatePDFOutput2` rellena el método. La variable `generatePDFOutput2` rellena este objeto con metadatos generados que describen el documento. (Este valor de parámetro solo es necesario para la invocación de servicio web).
   * Una salida `OutputResult` que contiene los resultados de la operación. (Este valor de parámetro solo es necesario para la invocación de servicio web).

   La variable `generatePDFOutput2` el método devuelve un `BLOB` objeto que contiene el formulario de PDF no interactivo.

1. Guarde el documento de PDF como archivo de PDF.

   * Cree un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento del PDF interactivo y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto recuperado del `generatePDFOutput2` método. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` miembro de datos.
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Imprimir en archivos {#printing-to-files}

Puede utilizar el servicio Output para imprimir flujos como PostScript, Printer Control Language (PCL) o los siguientes formatos de etiqueta en un archivo:

* Zebra - ZPL
* Interė - IPL
* Datamax - DPL
* TecToshiba - TPCL

Con el servicio Output se pueden combinar los datos XML con un diseño de formulario y se puede imprimir el formulario en un archivo. La siguiente ilustración muestra el servicio Output creando archivos láser y de etiqueta.

>[!NOTE]
>
>Para obtener información sobre cómo enviar emisiones de impresión a impresoras, consulte [Envío de emisiones de impresión a impresoras](creating-document-output-streams.md#sending-print-streams-to-printers).

>[!NOTE]
>
>Para obtener más información sobre el servicio Output , consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-5}

Para imprimir en un archivo, realice los pasos siguientes:

1. Incluir archivos de proyecto.
1. Cree un objeto Cliente de salida.
1. Haga referencia a un origen de datos XML.
1. Defina las opciones de tiempo de ejecución de impresión necesarias para imprimir en un archivo.
1. Imprima el flujo de impresión en un archivo.
1. Recupere los resultados de la operación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, deberá reemplazar los archivos adobe-Utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms. (Consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).)

**Creación de un objeto de cliente de salida**

Para poder realizar una operación de servicio de salida mediante programación, debe crear un objeto cliente de servicio de salida. Si utiliza la API de Java, cree un `OutputClient` objeto. Si utiliza la API del servicio web de salida, cree un `OutputServiceService` objeto.

**Referencia a un origen de datos XML**

Para imprimir un documento que contenga datos, debe hacer referencia a un origen de datos XML que contenga elementos XML para cada campo de formulario que desee rellenar con datos. El nombre del elemento XML debe coincidir con el nombre del campo. Se ignora un elemento XML si no se corresponde con un campo de formulario o si el nombre del elemento XML no coincide con el nombre del campo. No es necesario coincidir con el orden en que se muestran los elementos XML si se especifican todos los elementos XML.

**Establecer las opciones de tiempo de ejecución de impresión necesarias para imprimir en un archivo**

Para imprimir en un archivo, debe definir la opción de tiempo de ejecución del URI de archivo especificando la ubicación y el nombre del archivo al que se imprime el servicio Output. Por ejemplo, para indicar al servicio Output que imprima un archivo PostScript denominado *MortgageForm.ps* para C:\Adobe, especifique C:\Adobe\MortgageForm.ps.

>[!NOTE]
>
>Existen opciones opcionales en tiempo de ejecución que puede definir. Para obtener información sobre todas las opciones que puede establecer, consulte la `PrintedOutputOptionsSpec` referencia de clase en [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Imprimir el flujo de impresión en un archivo**

Después de hacer referencia a un origen de datos XML válido que contiene datos de formulario y de definir las opciones de impresión en tiempo de ejecución, puede invocar el servicio Output , que hace que imprima un archivo.

**Recuperar los resultados de la operación**

Una vez que el servicio Output realiza una operación, devuelve varios elementos de datos, como datos XML, que especifican si la operación se realizó correctamente.

**Consulte también lo siguiente**

[Imprimir en archivos mediante la API de Java](creating-document-output-streams.md#print-to-files-using-the-java-api)

[Imprimir en archivos mediante la API de servicio web](creating-document-output-streams.md#print-to-files-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Imprimir en archivos mediante la API de Java {#print-to-files-using-the-java-api}

Imprimir en un archivo mediante la API de salida (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-output-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un objeto Cliente de salida.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `OutputClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un origen de datos XML.

   * Cree un `java.io.FileInputStream` objeto que representa el origen de datos XML que se utiliza para rellenar el documento utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo XML.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Defina las opciones de tiempo de ejecución de impresión necesarias para imprimir en un archivo.

   * Cree un `PrintedOutputOptionsSpec` usando su constructor.
   * Especifique el archivo invocando el objeto PrintedOutputOptionsSpec `setFileURI` y pasando un valor de cadena que representa el nombre y la ubicación del archivo. Por ejemplo, si desea que el servicio Output imprima en un archivo PostScript denominado MortgageForm.ps ubicado en C:\Adobe, especifique C:\\Adobe\MortgageForm.ps.
   * Especifique el número de copias que desea imprimir invocando la variable `PrintedOutputOptionsSpec` del objeto `setCopies` y pasando un valor entero que representa el número de copias.

1. Imprima el flujo de impresión en un archivo.

   Imprimir en un archivo invocando la variable `OutputClient` del objeto `generatePrintedOutput` y pasando los siguientes valores:

   * A `PrintFormat` valor de enumeración que especifica el formato de flujo de impresión que se va a crear. Por ejemplo, para crear un flujo de impresión PostScript, pase `PrintFormat.PostScript`.
   * Un valor de cadena que especifica el nombre del diseño de formulario.
   * Un valor de cadena que especifica la ubicación de archivos colaterales relacionados, como archivos de imagen.
   * Un valor de cadena que especifica la ubicación del archivo XDC que se va a utilizar (puede pasar `null` si especificó el archivo XDC que se va a usar usando la variable `PrintedOutputOptionsSpec` ).
   * La variable `PrintedOutputOptionsSpec` que contiene las opciones de tiempo de ejecución necesarias para imprimir en un archivo.
   * La variable `com.adobe.idp.Document` objeto que contiene el origen de datos XML que contiene los datos del formulario.

   La variable `generatePrintedOutput` devuelve un valor `OutputResult` que contiene los resultados de la operación.

   >[!NOTE]
   >
   >La variable `OutputResult` del objeto `getRecordLevelMetaDataList` devuelve el método `null`.

1. Recupere los resultados de la operación.

   * Cree un `com.adobe.idp.Document` objeto que representa el estado del `generatePrintedOutput` invocando el método `OutputResult` del objeto `getStatusDoc` (el método `OutputResult` el objeto fue devuelto por el `generatePrintedOutput` método).
   * Cree un `java.io.File` que contendrá los resultados de la operación. Asegúrese de que la extensión de archivo es XML.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `com.adobe.idp.Document` al archivo (asegúrese de usar la variable `com.adobe.idp.Document` objeto devuelto por el `getStatusDoc` método).

**Consulte también lo siguiente**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Inicio rápido (modo SOAP): Impresión en un archivo mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### Imprimir en archivos mediante la API de servicio web {#print-to-files-using-the-web-service-api}

Imprimir en un archivo mediante la API de salida (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto Cliente de salida.

   * Cree un `OutputServiceClient` usando su constructor predeterminado.
   * Cree un `OutputServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para usar MTOM.
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `OutputServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un origen de datos XML.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar datos de formulario.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que especifica la ubicación del archivo XML que contiene datos de formulario.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `binaryData` con el contenido de la matriz de bytes.

1. Defina las opciones de tiempo de ejecución de impresión necesarias para imprimir en un archivo.

   * Cree un `PrintedOutputOptionsSpec` usando su constructor.
   * Especifique el archivo asignando un valor de cadena que represente la ubicación y el nombre del archivo a la variable `PrintedOutputOptionsSpec` del objeto `fileURI` miembro de datos. Por ejemplo, si desea que el servicio Output imprima en un archivo PostScript denominado *MortgageForm.ps* ubicado en C:\Adobe, especifique C:\\Adobe\MortgageForm.ps.
   * Especifique el número de copias que desea imprimir asignando un valor entero que represente el número de copias al `PrintedOutputOptionsSpec` del objeto `copies` miembros de datos.

1. Imprima el flujo de impresión en un archivo.

   Imprimir en un archivo invocando la variable `OutputServiceService` del objeto `generatePrintedOutput` y pasando los siguientes valores:

   * A `PrintFormat` valor de enumeración que especifica el formato de flujo de impresión que se va a crear. Por ejemplo, para crear un flujo de impresión PostScript, pase `PrintFormat.PostScript`.
   * Un valor de cadena que especifica el nombre del diseño de formulario.
   * Un valor de cadena que especifica la ubicación de archivos colaterales relacionados, como archivos de imagen.
   * Un valor de cadena que especifica la ubicación del archivo XDC que se va a utilizar (puede pasar `null` si especificó el archivo XDC que se va a usar usando la variable `PrintedOutputOptionsSpec` ).
   * La variable `PrintedOutputOptionsSpec` que contiene las opciones de tiempo de ejecución de impresión necesarias para imprimir en un archivo.
   * La variable `BLOB` objeto que contiene el origen de datos XML que contiene los datos del formulario.
   * A `BLOB` objeto que rellena el `generatePDFOutput` método. La variable `generatePDFOutput` rellena este objeto con metadatos generados que describen el documento. (Este valor de parámetro solo es necesario para invocar un servicio web).
   * A `BLOB` objeto que rellena el `generatePDFOutput` método. La variable `generatePDFOutput` rellena este objeto con datos de resultado. (Este valor de parámetro solo es necesario para invocar un servicio web).
   * Un `OutputResult` que contiene los resultados de la operación. (Este valor de parámetro solo es necesario para invocar un servicio web).

1. Recupere los resultados de la operación.

   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa una ubicación de archivo XML que contiene datos de resultados. Asegúrese de que la extensión de archivo es XML.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto que el `OutputServiceService` del objeto `generatePDFOutput` (el octavo parámetro). Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` miembro de datos.
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en el archivo XML invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Envío de emisiones de impresión a impresoras {#sending-print-streams-to-printers}

Puede utilizar el servicio Output para enviar flujos de impresión como PostScript, Printer Control Language (PCL) o los siguientes formatos de etiqueta a impresoras de red:

* Zebra - ZPL
* Interė - IPL
* Datamax - DPL
* TecToshiba - TPCL

Con el servicio Output se pueden combinar los datos XML con un diseño de formulario y obtener el formulario como una secuencia de impresión. Por ejemplo, puede crear un flujo de impresión PostScript y enviarlo a una impresora de red. La siguiente ilustración muestra el servicio de salida que envía transmisiones de impresión a impresoras de red.

>[!NOTE]
>
>Para demostrar cómo enviar un flujo de impresión a una impresora de red, esta sección envía un flujo de impresión PostScript a una impresora de red mediante el protocolo de impresora SharedPrinter.

>[!NOTE]
>
>Para obtener más información sobre el servicio Output , consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-6}

Para enviar un flujo de impresión a una impresora de red, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto Cliente de salida.
1. Haga referencia a un origen de datos XML.
1. Establecer opciones de tiempo de ejecución de impresión
1. Recupere un documento para imprimir.
1. Envíe el documento a una impresora de red.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, deberá reemplazar los archivos adobe-Utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms.

**Creación de un objeto de cliente de salida**

Antes de realizar una operación de servicio de salida mediante programación, cree un objeto cliente de servicio de salida. Si utiliza la API de Java, cree un `OutputClient` objeto. Si utiliza la API del servicio web de salida, cree un `OutputServiceClient` objeto.

**Referencia a un origen de datos XML**

Para imprimir un documento que contenga datos, debe hacer referencia a un origen de datos XML que contenga elementos XML para cada campo de formulario que desee rellenar con datos. El nombre del elemento XML debe coincidir con el nombre del campo. Se ignora un elemento XML si no se corresponde con un campo de formulario o si el nombre del elemento XML no coincide con el nombre del campo. No es necesario coincidir con el orden en que se muestran los elementos XML si se especifican todos los elementos XML.

**Establecer opciones de tiempo de ejecución de impresión**

Puede establecer las opciones en tiempo de ejecución al enviar un flujo de impresión a una impresora, incluidas las siguientes opciones:

* **Copias**: Especifica el número de copias que se enviarán a la impresora. El valor predeterminado es 1.
* **Grapado**: Se establece una opción XCI cuando se utiliza una grapadora. Esta opción se puede especificar en el modelo de configuración mediante el elemento básico y se utiliza únicamente para impresoras PS y PCL.
* **OutputJog**: Se establece una opción XCI cuando las páginas de salida se deben bloquear (desplazar físicamente en la bandeja de salida). Esta opción es solo para impresoras PS y PCL.
* **OutputBin**: Valor XCI que se utiliza para permitir que el controlador de impresión seleccione el grupo de salida adecuado.

>[!NOTE]
>
>Para obtener información sobre todas las opciones de tiempo de ejecución que puede establecer, consulte la `PrintedOutputOptionsSpec` referencia de clase.

**Recuperar un documento para imprimir**

Recupere un flujo de impresión para enviarlo a una impresora. Por ejemplo, puede recuperar un archivo PostScript y enviarlo a una impresora.

Puede elegir enviar un archivo PDF si la impresora admite PDF. Sin embargo, un problema con el envío de un documento de PDF a una impresora es que cada fabricante de la impresora tiene una implementación diferente del intérprete de PDF. Es decir, algunos fabricantes de impresoras utilizan la interpretación Adobe PDF, pero depende de la impresora. Otras impresoras tienen su propio intérprete PDF. Como resultado, los resultados de impresión pueden variar.

Otra limitación del envío de un documento de PDF a una impresora es que solo imprime; no puede acceder a la selección a doble cara, a la selección de la bandeja de papel ni al grapado, excepto a través de la configuración de la impresora.

Para recuperar un documento para imprimir, utilice la variable `generatePrintedOutput` método. La tabla siguiente especifica los tipos de contenido que se establecen para un flujo de impresión determinado al usar la variable `generatePrintedOutput` método.

<table>
 <thead>
  <tr>
   <th><p>Formato de impresión </p></th>
   <th><p>Descripción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>DPL </p></td>
   <td><p>Crea un dpl203.xdc de salida xdc predeterminado o personalizado.</p></td>
  </tr>
  <tr>
   <td><p>DPL 300 ppp </p></td>
   <td><p>Crea un flujo de salida DPL 300 DPI.</p></td>
  </tr>
  <tr>
   <td><p>DPL 406 ppp </p></td>
   <td><p>Crea un flujo de salida DPL 400 DPI.</p></td>
  </tr>
  <tr>
   <td><p>DPL 600 ppp </p></td>
   <td><p>Crea un flujo de salida DPL 600 DPI.</p></td>
  </tr>
  <tr>
   <td><p>GenericColorPCL </p></td>
   <td><p>Crea un flujo de salida PCL de color genérico (5c).</p></td>
  </tr>
  <tr>
   <td><p>GenericPSLevel3 </p></td>
   <td><p>Crea un flujo de salida genérico PostScript de nivel 3.</p></td>
  </tr>
  <tr>
   <td><p>IPL </p></td>
   <td><p>Crea un flujo de salida de IPL personalizado.</p></td>
  </tr>
  <tr>
   <td><p>IPL 300 ppp </p></td>
   <td><p>Crea un flujo de salida IPL 300 DPI.</p></td>
  </tr>
  <tr>
   <td><p>IPL 400 ppp </p></td>
   <td><p>Crea un flujo de salida IPL 400 DPI.</p></td>
  </tr>
  <tr>
   <td><p>PCL </p></td>
   <td><p>Crea un flujo de salida genérico monocromo PCL (5e).</p></td>
  </tr>
  <tr>
   <td><p>PostScript </p></td>
   <td><p>Crea un flujo de salida genérico PostScript de nivel 2.</p></td>
  </tr>
  <tr>
   <td><p>TPCL </p></td>
   <td><p>Crea un flujo de salida TPCL personalizado.</p></td>
  </tr>
  <tr>
   <td><p>TPCL 305 ppp </p></td>
   <td><p>Crea un flujo de salida TPCL 305 DPI.</p></td>
  </tr>
  <tr>
   <td><p>TPCL 600 ppp </p></td>
   <td><p>Crea un flujo de salida TPCL 600 DPI.</p></td>
  </tr>
  <tr>
   <td><p>ZPL </p></td>
   <td><p>Crea un flujo de salida ZPL 203 DPI.</p></td>
  </tr>
  <tr>
   <td><p>ZPL 300 ppp </p></td>
   <td><p>Crea un flujo de salida ZPL 300 DPI.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>También puede enviar un flujo de impresión a una impresora utilizando la variable `generatePrintedOutput2` método. Sin embargo, los inicios rápidos asociados con la sección Envío de flujos de impresión a impresoras utilizan la variable `generatePrintedOutput` método.

**Enviar el flujo de impresión a una impresora de red**

Después de recuperar un documento para imprimir, puede invocar el servicio Output , que hace que envíe un flujo de impresión a una impresora de red. Para que el servicio Output localice correctamente la impresora, debe especificar tanto el servidor de impresión como el nombre de la impresora. Además, también debe especificar el protocolo de impresión.

>[!NOTE]
>
>Si PDFG está instalado en el servidor de formularios y el servidor se ejecuta en Windows Server 2008, no puede utilizar la propiedad SharedPrinter. En este caso, utilice un protocolo de impresora diferente.

>[!NOTE]
>
>Si utiliza una impresora de red y el mecanismo de acceso es SharedPrinter, debe especificar la ruta de red completa de la impresora.Envíe un flujo de impresión a una impresora de red mediante la API de Java

Envíe un flujo de impresión a una impresora de red mediante la API de salida (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-output-client.jar, en la ruta de clase de su proyecto Java.

1. Creación de un objeto de cliente de salida

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `OutputClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Referencia a un origen de datos XML

   * Cree un `java.io.FileInputStream` objeto que representa el origen de datos XML que se utiliza para rellenar el documento utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo XML.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Establecer opciones de tiempo de ejecución de impresión

   Cree un `PrintedOutputOptionsSpec` que representa las opciones de impresión en tiempo de ejecución. Por ejemplo, puede especificar el número de copias que desea imprimir invocando la variable `PrintedOutputOptionsSpec` del objeto `setCopies` método.

   >[!NOTE]
   >
   >No se puede establecer el valor de paginación utilizando la variable `PrintedOutputOptionsSpec` del objeto `setPagination` método si está generando un flujo de impresión ZPL. Tampoco puede establecer las siguientes opciones para un flujo de impresión ZPL: OutputJog, PageOffset y Staple. La variable `setPagination` El método no es válido para la generación de PostScript. Solo es válido para la generación de PCL.

1. Recuperar un documento para imprimir

   * Recupere un documento para imprimir invocando el `OutputClient` del objeto `generatePrintedOutput` y pasando los siguientes valores:

      * A `PrintFormat` valor de enumeración que especifica el flujo de impresión. Por ejemplo, para crear un flujo de impresión PostScript, pase `PrintFormat.PostScript`.
      * Un valor de cadena que especifica el nombre del diseño de formulario.
      * Un valor de cadena que especifica la ubicación de archivos colaterales relacionados, como archivos de imagen.
      * Un valor de cadena que especifica la ubicación del archivo XDC que se va a utilizar.
      * La variable `PrintedOutputOptionsSpec` que contiene las opciones en tiempo de ejecución necesarias para imprimir en un archivo.
      * La variable `com.adobe.idp.Document` objeto que representa el origen de datos XML que contiene los datos de formulario que se van a combinar con el diseño de formulario.

      Este método devuelve un `OutputResult` que contiene los resultados de la operación.

   * Cree un `com.adobe.idp.Document` para enviar a la impresora invocando el objeto `OutputResult` objeto ‘s `getGeneratedDoc` método. Este método devuelve un `com.adobe.idp.Document` objeto.


1. Enviar el flujo de impresión a una impresora de red

   Envíe el flujo de impresión a una impresora de red invocando el `OutputClient` del objeto `sendToPrinter` y pasando los siguientes valores:

   * A `com.adobe.idp.Document` que representa el flujo de impresión que se va a enviar a la impresora.
   * A `PrinterProtocol` valor de enumeración que especifica el protocolo de impresora que se va a utilizar. Por ejemplo, para especificar el protocolo SharedPrinter, pase `PrinterProtocol.SharedPrinter`.
   * Valor de cadena que especifica el nombre del servidor de impresión. Por ejemplo, suponiendo que el nombre del servidor de impresión sea PrintServer1, pase `\\\PrintSever1`.
   * Un valor de cadena que especifica el nombre de la impresora. Por ejemplo, suponiendo que el nombre de la impresora sea Impresora1, pase `\\\PrintSever1\Printer1`.

   >[!NOTE]
   >
   >La variable `sendToPrinter` se ha añadido al método de API de AEM Forms en la versión 8.2.1.

### Envío de un flujo de impresión a una impresora mediante la API de servicio web {#send-a-print-stream-to-a-printer-using-the-web-service-api}

Envíe un flujo de impresión a una impresora de red mediante la API de salida (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto Cliente de salida.

   * Cree un `OutputServiceClient` usando su constructor predeterminado.
   * Cree un `OutputServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para usar MTOM.
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `OutputServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un origen de datos XML.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar datos de formulario.
   * Cree un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que especifique la ubicación del archivo XML que contiene los datos del formulario.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Determine la longitud de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Establezca las opciones de impresión en tiempo de ejecución.

   Cree un `PrintedOutputOptionsSpec` usando su constructor. Por ejemplo, puede especificar el número de copias que desea imprimir asignando un valor entero que represente el número de copias al `PrintedOutputOptionsSpec` del objeto `copies` miembro de datos.

   >[!NOTE]
   >
   >No se puede establecer el valor de paginación utilizando la variable `PrintedOutputOptionsSpec` del objeto `pagination` miembro de datos si está generando un flujo de impresión ZPL. Tampoco puede establecer las siguientes opciones para un flujo de impresión ZPL: OutputJog, PageOffset y Staple. La variable `pagination` El miembro de datos no es válido para la generación de PostScript. Solo es válido para la generación de PCL.

1. Recupere un documento para imprimir.

   * Recupere un documento para imprimir invocando el `OutputServiceService` del objeto `generatePrintedOutput` y pasando los siguientes valores:

      * A `PrintFormat` valor de enumeración que especifica el flujo de impresión. Por ejemplo, para crear un flujo de impresión PostScript, pase `PrintFormat.PostScript`.
      * Un valor de cadena que especifica el nombre del diseño de formulario.
      * Un valor de cadena que especifica la ubicación de archivos colaterales relacionados, como archivos de imagen.
      * Un valor de cadena que especifica la ubicación del archivo XDC que se va a utilizar.
      * La variable `PrintedOutputOptionsSpec` objeto que contiene opciones de tiempo de ejecución de impresión que se utilizan al enviar un flujo de impresión a una impresora de red.
      * La variable `BLOB` objeto que contiene el origen de datos XML que contiene los datos del formulario.
      * A `BLOB` objeto que rellena el `generatePrintedOutput` método. La variable `generatePrintedOutput` rellena este objeto con metadatos generados que describen el documento. (Este valor de parámetro solo es necesario para invocar un servicio web).
      * A `BLOB` objeto que rellena el `generatePrintedOutput` método. La variable `generatePrintedOutput` rellena este objeto con datos de resultado. (Este valor de parámetro solo es necesario para invocar un servicio web).
      * Un `OutputResult` que contiene los resultados de la operación. (Este valor de parámetro solo es necesario para invocar un servicio web).
   * Cree un `BLOB` para enviar a la impresora obteniendo el valor de `OutputResult` objeto ‘s `generatedDoc` método. Este método devuelve un `BLOB` objeto que contiene datos de PostScript devueltos por la variable `generatePrintedOutput` método.


1. Envíe el flujo de impresión a una impresora de red.

   Envíe el flujo de impresión a una impresora de red invocando el `OutputClient` del objeto `sendToPrinter` y pasando los siguientes valores:

   * A `BLOB` que representa el flujo de impresión que se va a enviar a la impresora.
   * A `PrinterProtocol` valor de enumeración que especifica el protocolo de impresora que se va a utilizar. Por ejemplo, para especificar el protocolo SharedPrinter, pase `PrinterProtocol.SharedPrinter`.
   * A `bool` que especifica si se va a usar el valor del parámetro anterior. Transmitir el valor `true`. (Este valor de parámetro solo es necesario para invocar un servicio web).
   * Valor de cadena que especifica el nombre del servidor de impresión. Por ejemplo, suponiendo que el nombre del servidor de impresión sea PrintServer1, pase `\\\PrintSever1`.
   * Un valor de cadena que especifica el nombre de la impresora. Por ejemplo, suponiendo que el nombre de la impresora sea Impresora1, pase `\\\PrintSever1\Printer1`.

   >[!NOTE]
   >
   >La variable `sendToPrinter` se ha añadido al método de API de AEM Forms en la versión 8.2.1.

## Creación de varios archivos de salida {#creating-multiple-output-files}

El servicio Output puede crear documentos independientes para cada registro dentro de un origen de datos XML o un solo archivo que contenga todos los registros (esta funcionalidad es la predeterminada). Por ejemplo, supongamos que diez registros se encuentran en un origen de datos XML y se indica al servicio Output que cree documentos de PDF independientes (u otros tipos de salida) para cada registro mediante la API del servicio de salida. Como resultado, el servicio Output genera diez documentos PDF. (En lugar de crear documentos, puede enviar varios flujos de impresión a una impresora).

La siguiente ilustración también muestra el servicio Output procesando un archivo de datos XML que contiene varios registros. Sin embargo, supongamos que ordena al servicio Output que cree un único documento de PDF que contenga todos los registros de datos. En esta situación, el servicio Output genera un documento que contiene todos los registros.

La siguiente ilustración muestra el servicio Output procesando un archivo de datos XML que contiene varios registros. Supongamos que ordena al servicio Output que cree un documento de PDF independiente para cada registro de datos. En este caso, el servicio Output genera un documento de PDF independiente para cada registro de datos.

![cm_outputbatchmany](assets/cm_outputbatchmany.png)

Los siguientes datos XML muestran un ejemplo de un archivo de datos que contiene tres registros de datos.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <batch>
 <LoanRecord>
     <mortgageAmount>500000</mortgageAmount>
     <lastName>Blue</lastName>
     <firstName>Tony</firstName>
     <SSN>555666777</SSN>
     <PositionTitle>Product Manager</PositionTitle>
     <Address>555 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>TBlue@NoMailServer.com</Email>
     <PhoneNum>555-7418</PhoneNum>
     <FaxNum>555-9981</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 <LoanRecord>
     <mortgageAmount>300000</mortgageAmount>
     <lastName>White</lastName>
     <firstName>Sam</firstName>
     <SSN>555666222</SSN>
     <PositionTitle>Program Manager</PositionTitle>
     <Address>557 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>SWhite@NoMailServer.com</Email>
     <PhoneNum>555-7445</PhoneNum>
     <FaxNum>555-9986</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 <LoanRecord>
     <mortgageAmount>700000</mortgageAmount>
     <lastName>Green</lastName>
     <firstName>Steve</firstName>
     <SSN>55566688</SSN>
     <PositionTitle>Project Manager</PositionTitle>
     <Address>445 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>SGreeb@NoMailServer.com</Email>
     <PhoneNum>555-2211</PhoneNum>
     <FaxNum>555-2221</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 </batch>
```

Observe que el elemento XML que inicia y finaliza cada registro de datos es `LoanRecord`. La lógica de aplicación que genera varios archivos hace referencia a este elemento XML.

>[!NOTE]
>
>Para obtener más información sobre el servicio Output , consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-7}

Para crear varios archivos de PDF basados en un origen de datos XML, siga estos pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto Cliente de salida.
1. Haga referencia a un origen de datos XML.
1. Establezca las opciones de tiempo de ejecución del PDF.
1. Establezca las opciones de procesamiento en tiempo de ejecución.
1. Genere varios archivos de PDF.
1. Recupere los resultados de la operación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, deberá reemplazar los archivos adobe-Utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms.

**Creación de un objeto de cliente de salida**

Para poder realizar una operación de servicio de salida mediante programación, debe crear un objeto cliente de servicio de salida. Si utiliza la API de Java, cree un `OutputClient` objeto. Si utiliza la API del servicio web de salida, cree un `OutputServiceService` objeto.

**Referencia a un origen de datos XML**

Haga referencia a un origen de datos XML que contiene varios registros. Se debe utilizar un elemento XML para separar los registros de datos. Por ejemplo, en el origen de datos XML de ejemplo que se muestra anteriormente en esta sección, el elemento XML que separa los registros de datos tiene un nombre `LoanRecord`.

Debe existir un elemento XML para cada campo de formulario que desee rellenar con datos. El nombre del elemento XML debe coincidir con el nombre del campo. Se ignora un elemento XML si no se corresponde con un campo de formulario o si el nombre del elemento XML no coincide con el nombre del campo. No es necesario coincidir con el orden en que se muestran los elementos XML si se especifican todos los elementos XML.

**Establecer opciones de tiempo de ejecución del PDF**

Debe establecer las siguientes opciones de tiempo de ejecución para que el servicio Output cree correctamente varios archivos basados en un origen de datos XML:

* **Muchos archivos**: Especifica si el servicio Output crea un solo documento o varios documentos. Puede especificar true o false. Para crear un documento independiente para cada registro de datos en el origen de datos XML, especifique true.
* **URI de archivo**: Especifica la ubicación de los archivos que genera el servicio Output. Por ejemplo, suponga que especifica C:\\Adobe\forms\Loan.pdf. En esta situación, el servicio Output crea un archivo llamado Loan.pdf y coloca el archivo en el directorio C:\\Adobe\forms folder. Cuando hay varios archivos, los nombres de los archivos son Loan0001.pdf, Loan0002.pdf, Loan0003.pdf y así sucesivamente. Si especifica una ubicación de archivo, los archivos se colocan en el servidor, no en el equipo cliente.
* **Nombre de registro**: Especifica el nombre del elemento XML en el origen de datos que separa los registros de datos. Por ejemplo, en el origen de datos XML de ejemplo que se muestra anteriormente en esta sección, el elemento XML que separa los registros de datos se llama `LoanRecord`. (En lugar de establecer la opción Nombre de registro en tiempo de ejecución, puede establecer el Nivel de registro asignándole un valor numérico que indique el nivel de elemento que contiene los registros de datos. Sin embargo, solo puede establecer el Nombre de registro o el Nivel de registro. No se pueden establecer ambos valores).

**Establecer las opciones de procesamiento en tiempo de ejecución**

Puede definir opciones de procesamiento en tiempo de ejecución al crear varios archivos. Aunque estas opciones no son necesarias (a diferencia de las opciones de tiempo de ejecución de salida, que son necesarias), puede realizar tareas como mejorar el rendimiento del servicio Output . Por ejemplo, puede almacenar en caché el diseño de formulario que utiliza el servicio Output para mejorar el rendimiento.

Cuando el servicio Output procesa los registros por lotes, lee los datos que contienen varios registros de forma incremental. Es decir, el servicio Output lee los datos en la memoria y los libera a medida que se procesa el lote de registros. El servicio Output carga los datos de forma incremental cuando se establece una de las dos opciones de tiempo de ejecución. Si establece la opción Nombre de registro en tiempo de ejecución, el servicio Salida lee los datos de forma incremental. Del mismo modo, si establece la opción de tiempo de ejecución Nivel de registro en 2 o bueno, el servicio Salida lee los datos de forma incremental.

Puede controlar si el servicio Output realiza una carga incremental utilizando la variable `PDFOutputOptionsSpec` o `PrintedOutputOptionSpec` del objeto `setLazyLoading` método. Puede pasar el valor `false` a este método que desactiva la carga incremental.

**Generar varios archivos de PDF**

Después de hacer referencia a un origen de datos XML válido que contiene varios registros de datos y establecer opciones de tiempo de ejecución, puede invocar el servicio Output , que hace que genere varios archivos. Cuando se generan varios registros, la variable `OutputResult` del objeto `getGeneratedDoc` devuelve el método `null`.

**Recuperar los resultados de la operación**

Una vez que el servicio Output realiza una operación, devuelve datos XML que especifican si la operación se ha realizado correctamente. El servicio Output devuelve el siguiente XML. En esta situación, el servicio Output generó 42 documentos.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <printResult>
 <status>0</status>
 <requestId>4ad85f9e2</requestId>
 <context/>
 <messages>
 <message>Printed all 42 records successfully.</message>
 </messages>
 <printSpec>
 <input>
 <validated>true</validated>
 <dataFile recordIdField="" recordLevel="0" recordName="LoanRecord"/>
 <sniffRules lookAhead="300"/>
 <formDesign>Loan.xdp</formDesign>
 <contentRoot>C:\Adobe</contentRoot>
 <metadata-spec record="false"/>
 </input>
 <output>
 <format>PDF</format>
 <fileURI>C:\Adobe\forms\Loan.pdf</fileURI>
 <optionString>cacheenabled=true&padebug=false&linearpdf=false&pdfarevisionnumber=1&pdfaconformance=A&taggedpdf=false&TransactionTimeOut=180</optionString>
 <waitForResponse>true</waitForResponse>
 <outputStream>multiple</outputStream>
 </output>
 </printSpec>
 </printResult>
```

**Consulte también lo siguiente**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Creación de varios archivos de PDF mediante la API de Java {#create-multiple-pdf-files-using-the-java-api}

Cree varios archivos de PDF utilizando la API de salida (Java):

1. Incluir archivos de proyecto&quot;

   Incluya archivos JAR del cliente, como adobe-output-client.jar, en la ruta de clase de su proyecto Java. .

1. Creación de un objeto de cliente de salida

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `OutputClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Referencia a un origen de datos XML

   * Cree un `java.io.FileInputStream` objeto que representa el origen de datos XML que contiene varios registros utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo XML.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Establecer opciones de tiempo de ejecución del PDF

   * Cree un `PDFOutputOptionsSpec` usando su constructor.
   * Configure la opción Muchos archivos invocando la variable `PDFOutputOptionsSpec` del objeto `setGenerateManyFiles` método. Por ejemplo, pase el valor `true` para indicar al servicio Output que cree un archivo PDF independiente para cada registro del origen de datos XML. (Si pasa `false`, el servicio Output genera un solo documento de PDF que contiene todos los registros).
   * Establezca la opción URI de archivo invocando la variable `PDFOutputOptionsSpec` del objeto `setFileUri` y pasando un valor de cadena que especifica la ubicación de los archivos que genera el servicio Output. La opción URI de archivo es relativa al servidor de aplicaciones J2EE que aloja AEM Forms, no al equipo cliente.
   * Establezca la opción Nombre de registro invocando la variable `OutputOptionsSpec` del objeto `setRecordName` y pasando un valor de cadena que especifica el nombre del elemento XML en el origen de datos que separa los registros de datos. (Por ejemplo, considere el origen de datos XML que se ha mostrado anteriormente en esta sección. El nombre del elemento XML que separa los registros de datos es LoanRecord).

1. Establecer las opciones de procesamiento en tiempo de ejecución

   * Cree un `RenderOptionsSpec` usando su constructor.
   * Almacene en caché el diseño de formulario para mejorar el rendimiento del servicio Output invocando el `RenderOptionsSpec` del objeto `setCacheEnabled` y pasar una `Boolean` valor de `true`.

1. Generar varios archivos de PDF

   Genere varios archivos de PDF invocando la variable `OutputClient` del objeto `generatePDFOutput` y pasando los siguientes valores:

   * A `TransformationFormat` valor de enumeración. Para generar un documento de PDF, especifique `TransformationFormat.PDF`.
   * Un valor de cadena que especifica el nombre del diseño de formulario.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentra el diseño de formulario.
   * A `PDFOutputOptionsSpec` que contiene opciones de tiempo de ejecución del PDF.
   * A `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * La variable `com.adobe.idp.Document` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario.

   La variable `generatePDFOutput` devuelve un valor `OutputResult` que contiene los resultados de la operación.

1. Recuperar los resultados de la operación

   * Cree un `java.io.File` que representa un archivo XML que contendrá los resultados de la `generatePDFOutput` método. Asegúrese de que la extensión del nombre de archivo es .xml.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `com.adobe.idp.Document` al archivo (asegúrese de usar la variable `com.adobe.idp.Document` objeto devuelto por el `applyUsageRights` método).

**Consulte también lo siguiente**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Inicio rápido (modo EJB): Creación de varios archivos de PDF mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creación de varios archivos de PDF mediante la API de servicio web {#create-multiple-pdf-files-using-the-web-service-api}

Cree varios archivos de PDF mediante la API de salida (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto Cliente de salida.

   * Cree un `OutputServiceClient` usando su constructor predeterminado.
   * Cree un `OutputServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para usar MTOM.
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `OutputServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un origen de datos XML.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar datos de formulario que contienen varios registros.
   * Cree un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo XML que contiene varios registros.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Establezca las opciones de tiempo de ejecución del PDF.

   * Cree un `PDFOutputOptionsSpec` usando su constructor.
   * Defina la opción Muchos archivos asignando un valor booleano a la variable `OutputOptionsSpec` del objeto `generateManyFiles` miembro de datos. Por ejemplo, asigne el valor `true` a este miembro de datos para solicitar al servicio Output que cree un archivo PDF independiente para cada registro del origen de datos XML. (Si asigna `false` a este miembro de datos, el servicio Output genera un solo PDF que contiene todos los registros).
   * Establezca la opción de URI de archivo asignando un valor de cadena que especifique la ubicación de los archivos que genera el servicio Output al `OutputOptionsSpec` del objeto `fileURI` miembro de datos. La opción URI de archivo es relativa al servidor de aplicaciones J2EE que aloja AEM Forms, no al equipo cliente.
   * Establezca la opción de nombre de registro asignando un valor de cadena que especifica el nombre del elemento XML en el origen de datos que separa los registros de datos del `OutputOptionsSpec` del objeto `recordName` miembro de datos.
   * Establezca la opción copias asignando un valor entero que especifica el número de copias que el servicio Output genera al `OutputOptionsSpec` del objeto `copies` miembro de datos.

1. Establezca las opciones de procesamiento en tiempo de ejecución.

   * Cree un `RenderOptionsSpec` usando su constructor.
   * Almacene en caché el diseño de formulario para mejorar el rendimiento del servicio Output asignando el valor `true` a `RenderOptionsSpec` del objeto `cacheEnabled` miembro de datos.

1. Genere varios archivos de PDF.

   Cree varios archivos de PDF invocando la variable `OutputServiceService` del objeto `generatePDFOutput`y pasando los siguientes valores:

   * Un valor de enumeración TransformationFormat. Para generar un documento de PDF, especifique `TransformationFormat.PDF`.
   * Un valor de cadena que especifica el nombre del diseño de formulario.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentra el diseño de formulario.
   * A `PDFOutputOptionsSpec` que contiene opciones de tiempo de ejecución del PDF.
   * A `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * La variable `BLOB` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario.
   * A `BLOB` objeto que rellena el `generatePDFOutput` método. La variable `generatePDFOutput` rellena este objeto con metadatos generados que describen el documento.
   * A `BLOB` objeto que rellena el `generatePDFOutput` método. La variable `generatePDFOutput` rellena este objeto con datos de resultado.
   * Un `OutputResult` que contiene los resultados de la operación.

1. Recuperar los resultados de la operación

   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa una ubicación de archivo XML que contiene datos de resultados. Asegúrese de que la extensión del nombre de archivo es .xml.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto que el `OutputServiceService` del objeto `generatePDFOutput` (el octavo parámetro). Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `binaryData` miembro de datos.
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en el archivo XML invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Creación de reglas de búsqueda {#creating-search-rules}

Puede crear reglas de búsqueda que resulten en que el servicio Output examine los datos de entrada y utilice diferentes diseños de formulario basados en el contenido de datos para generar resultados. Por ejemplo, si el texto *hipoteca* se encuentra dentro de los datos de entrada, el servicio Output puede utilizar un diseño de formulario denominado Mortgage.xdp. Del mismo modo, si el texto *automobile* se encuentra en los datos de entrada, el servicio Output puede utilizar un diseño de formulario guardado como AutomobileLoan.xdp. Aunque el servicio Output puede generar diferentes tipos de salida, esta sección supone que el servicio Output genera un archivo PDF. En el diagrama siguiente se muestra el servicio Output que genera un archivo PDF procesando un archivo de datos XML y utilizando uno de los muchos diseños de formulario.

Además, el servicio Output puede generar paquetes de documentos, en los que se proporcionan varios registros en el conjunto de datos y cada registro coincide con un diseño de formulario, y un solo documento se genera a partir de varios diseños de formulario.

![cs_outputbatchmanyformdesigns2](assets/cs_outputbatchmanyformdesigns2.png)

>[!NOTE]
>
>Para obtener más información sobre el servicio Output , consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-8}

Para indicar al servicio Output que utilice reglas de búsqueda mientras genera un documento, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto Cliente de salida.
1. Haga referencia a un origen de datos XML.
1. Defina las reglas de búsqueda.
1. Establezca las opciones de tiempo de ejecución del PDF.
1. Establezca las opciones de procesamiento en tiempo de ejecución.
1. Genere un documento de PDF.
1. Recupere los resultados de la operación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, deberá reemplazar adobe-Utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms.

**Creación de un objeto de cliente de salida**

Para poder realizar una operación de servicio de salida mediante programación, debe crear un objeto cliente de servicio de salida.

**Referencia a un origen de datos XML**

Debe existir un elemento XML para cada campo de formulario que desee rellenar con datos. El nombre del elemento XML debe coincidir con el nombre del campo. Se ignora un elemento XML si no se corresponde con un campo de formulario o si el nombre del elemento XML no coincide con el nombre del campo. No es necesario coincidir con el orden en que se muestran los elementos XML, siempre y cuando se especifiquen todos los elementos XML.

**Definir reglas de búsqueda**

Para definir las reglas de búsqueda, debe definir uno o varios patrones de texto que los servicios de salida buscan en los datos de entrada. Para cada patrón de texto que defina, debe especificar el diseño de formulario correspondiente que se utilizará si se encuentra el patrón de texto. Si se encuentra un patrón de texto, el servicio Output utiliza el diseño de formulario correspondiente para generar el resultado. Un ejemplo de patrón de texto es *hipoteca*.

>[!NOTE]
>
>Si no se encuentran los patrones de texto, se utiliza el formulario predeterminado. Asegúrese de que todos los diseños de formulario que utilice se encuentran en la raíz del contenido.

**Establecer opciones de tiempo de ejecución del PDF**

Defina las siguientes opciones de tiempo de ejecución del PDF para que el servicio Output cree correctamente un documento de PDF basado en varios diseños de formulario:

* **URI de archivo**: Especifica el nombre y la ubicación del archivo de PDF que genera el servicio Output.
* **Reglas**: Especifica las reglas que ha definido.
* **LookAHead**: Especifica el número de bytes que se utilizarán desde el principio del archivo de datos de entrada para analizar los patrones de texto definidos. El valor predeterminado es 500 bytes.

**Establecer las opciones de procesamiento en tiempo de ejecución**

Puede definir opciones de procesamiento en tiempo de ejecución al crear archivos PDF. Aunque estas opciones no son necesarias (a diferencia de las opciones de tiempo de ejecución del PDF), puede realizar tareas como mejorar el rendimiento del servicio Output . Por ejemplo, puede almacenar en caché el diseño de formulario que utiliza el servicio Output para mejorar el rendimiento.

**Generar un documento de PDF**

Después de hacer referencia a un origen de datos XML válido y establecer las opciones de tiempo de ejecución, puede invocar el servicio Output, lo que hace que genere un documento PDF. Si el servicio Output localiza un patrón de texto especificado en los datos de entrada, utilizará el diseño de formulario correspondiente. Si no se utiliza un patrón de texto, el servicio Output utilizará el diseño de formulario predeterminado.

**Recuperar los resultados de la operación**

Una vez que el servicio Output realiza una operación, devuelve datos XML que especifican si la operación se ha realizado correctamente.

**Consulte también lo siguiente**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Creación de reglas de búsqueda mediante la API de Java {#create-search-rules-using-the-java-api}

Cree reglas de búsqueda usando la API de salida (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-output-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un objeto Cliente de salida.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `OutputClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un origen de datos XML.

   * Cree un `java.io.FileInputStream` objeto que representa el origen de datos XML que se utiliza para rellenar el documento PDF utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo XML.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Defina las reglas de búsqueda.

   * Cree un `Rule` usando su constructor.
   * Defina un patrón de texto invocando la variable `Rule` del objeto `setPattern` y pasando un valor de cadena que especifica un patrón de texto.
   * Defina el diseño de formulario correspondiente invocando la variable `Rule` del objeto `setForm` método . Pase un valor de cadena que especifique el nombre del diseño de formulario.

   >[!NOTE]
   >
   >Para cada patrón de texto que desee definir, repita los tres subpasos anteriores.

   * Cree un `java.util.List` usando un `java.util.ArrayList` constructor.
   * Para cada `Rule` objeto que ha creado, invocar el `java.util.List` del objeto `add` y pase el `Rule` objeto.


1. Establezca las opciones de tiempo de ejecución del PDF.

   * Cree un `PDFOutputOptionsSpec` usando su constructor.
   * Especifique el nombre y la ubicación del archivo de PDF que genera el servicio de salida invocando la variable `PDFOutputOptionsSpec` del objeto `setFileURI` método. Pase un valor de cadena que especifique la ubicación del archivo PDF. La opción URI de archivo es relativa al servidor de aplicaciones J2EE que aloja AEM Forms, no al equipo cliente.
   * Establezca las reglas que definió invocando la variable `PDFOutputOptionsSpec` del objeto `setRules` método. Pase el `java.util.List` objeto que contiene la variable `Rule` objetos.
   * Establezca el número de bytes que se analizarán para buscar los patrones de texto definidos invocando la variable `PDFOutputOptionsSpec` del objeto `setLookAhead` método. Pase un valor entero que represente los números de bytes.

1. Establezca las opciones de procesamiento en tiempo de ejecución.

   * Cree un `RenderOptionsSpec` usando su constructor.
   * Almacene en caché el diseño de formulario para mejorar el rendimiento del servicio Output invocando la variable `RenderOptionsSpec` del objeto `setCacheEnabled` y pasar `true`.

1. Genere un documento de PDF.

   Genere un documento de PDF basado en varios diseños de formulario invocando la variable `OutputClient` del objeto `generatePDFOutput` y pasando los siguientes valores:

   * A `TransformationFormat` valor de enumeración. Para generar un documento de PDF, especifique `TransformationFormat.PDF`.
   * Un valor de cadena que especifica el nombre del diseño de formulario predeterminado. Es decir, el diseño de formulario que se utiliza si no se encuentra un patrón de texto.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentran los diseños de formulario.
   * A `PDFOutputOptionsSpec` que contiene opciones de tiempo de ejecución del PDF.
   * A `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * La variable `com.adobe.idp.Document` objeto que contiene los datos de formulario que el servicio Output busca para los patrones de texto definidos.

   La variable `generatePDFOutput` devuelve un valor `OutputResult` que contiene los resultados de la operación.

1. Recupere los resultados de la operación.

   * Cree un `com.adobe.idp.Document` objeto que representa el estado del `generatePDFOutput` invocando el método `OutputResult` del objeto `getStatusDoc` método.
   * Cree un `java.io.File` que contendrá los resultados de la operación. Asegúrese de que la extensión de archivo es .xml.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `com.adobe.idp.Document` al archivo (asegúrese de usar la variable `com.adobe.idp.Document` objeto devuelto por el `getStatusDoc` método).

**Consulte también lo siguiente**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Inicio rápido (modo EJB): Creación de reglas de búsqueda mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[Inicio rápido (modo SOAP): Creación de reglas de búsqueda mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creación de reglas de búsqueda mediante la API de servicio web {#create-search-rules-using-the-web-service-api}

Cree reglas de búsqueda mediante la API de salida (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto Cliente de salida.

   * Cree un `OutputServiceClient` usando su constructor predeterminado.
   * Cree un `OutputServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para usar MTOM.
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `OutputServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un origen de datos XML.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar datos que se combinarán con el documento del PDF.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF que se va a cifrar y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Defina las reglas de búsqueda.

   * Cree un `Rule` usando su constructor.
   * Definir un patrón de texto asignando un valor de cadena que especifica un patrón de texto a la variable `Rule` del objeto `pattern` miembro de datos.
   * Defina el diseño de formulario correspondiente asignando un valor de cadena que especifique el diseño de formulario al `Rule` del objeto `form` miembro de datos.

   >[!NOTE]
   >
   >Para cada patrón de texto que desee definir, repita los tres subpasos anteriores.

   * Cree un `MyArrayOf_xsd_anyType` que almacena las reglas.
   * Asigne cada `Rule` a un elemento de la variable `MyArrayOf_xsd_anyType` matriz. Invocar el `MyArrayOf_xsd_anyType` del objeto `Add` método para cada `Rule` objeto.


1. Establecer opciones de tiempo de ejecución del PDF

   * Cree un `PDFOutputOptionsSpec` usando su constructor.
   * Establezca la opción de URI de archivo asignando un valor de cadena que especifica la ubicación del archivo PDF que genera el servicio Output al `PDFOutputOptionsSpec` del objeto `fileURI` miembro de datos. La opción URI de archivo es relativa al servidor de aplicaciones J2EE que aloja AEM Forms, no al equipo cliente.
   * Establezca la opción copias asignando un valor entero que especifica el número de copias que el servicio Output genera al `PDFOutputOptionsSpec` del objeto `copies` miembro de datos.
   * Defina las reglas que definió asignando la variable `MyArrayOf_xsd_anyType` objeto que almacena las reglas en el `PDFOutputOptionsSpec` del objeto `rules` miembro de datos.
   * Establezca el número de bytes que se analizarán para buscar los patrones de texto definidos asignando un valor entero que represente los números de bytes que se analizarán en la variable `PDFOutputOptionsSpec` del objeto `lookAhead` método de datos.

1. Establecer las opciones de procesamiento en tiempo de ejecución

   * Cree un `RenderOptionsSpec` usando su constructor.
   * Almacene en caché el diseño de formulario para mejorar el rendimiento del servicio Output asignando el valor `true` a `RenderOptionsSpec` del objeto `cacheEnabled` miembro de datos.

   >[!NOTE]
   >
   >No se puede establecer la versión del documento del PDF utilizando la variable `RenderOptionsSpec` del objeto `pdfVersion` miembro si el documento de entrada es un formulario de Acrobat. El documento del PDF de salida conserva la versión del PDF del formulario de Acrobat. Del mismo modo, no se puede establecer la opción de PDF etiquetado utilizando la variable `RenderOptionsSpec` del objeto `taggedPDF` método si el documento de entrada es un formulario de Acrobat.

   >[!NOTE]
   >
   >No se puede establecer la opción de PDF linealizado utilizando la variable `RenderOptionsSpec` del objeto `linearizedPDF` miembro si el documento del PDF de entrada está certificado o firmado digitalmente. Para obtener más información, consulte [Firma digital de documentos PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).

1. Generar un documento de PDF

   Cree un documento de PDF invocando la variable `OutputServiceService` del objeto `generatePDFOutput`y pasando los siguientes valores:

   * A `TransformationFormat` valor de enumeración. Para generar un documento de PDF, especifique `TransformationFormat.PDF`.
   * Un valor de cadena que especifica el nombre del diseño de formulario.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentra el diseño de formulario.
   * A `PDFOutputOptionsSpec` que contiene opciones de tiempo de ejecución del PDF.
   * A `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * La variable `BLOB` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario.
   * A `BLOB` objeto que rellena el `generatePDFOutput` método. La variable `generatePDFOutput` rellena este objeto con metadatos generados que describen el documento. (Este valor de parámetro solo es necesario para la invocación de servicio web).
   * A `BLOB` objeto que rellena el `generatePDFOutput` método. La variable `generatePDFOutput` rellena este objeto con datos de resultado. (Este valor de parámetro solo es necesario para la invocación de servicio web).
   * Un `OutputResult` que contiene los resultados de la operación. (Este valor de parámetro solo es necesario para la invocación de servicio web).

   >[!NOTE]
   >
   >Al generar un documento de PDF invocando la variable `generatePDFOutput` Tenga en cuenta que no puede combinar datos con un formulario de PDF XFA que esté firmado, certificado o contenga derechos de uso. Para obtener información sobre los derechos de uso, consulte [Aplicación de derechos de uso a documentos de PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).

1. Recuperar los resultados de la operación

   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa una ubicación de archivo XML que contiene datos de resultados. Asegúrese de que la extensión de archivo es XML.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto que el `OutputServiceService` del objeto `generatePDFOutput` (el octavo parámetro). Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` miembro de datos.
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en el archivo XML invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Acoplamiento de documentos del PDF {#flattening-pdf-documents}

Puede utilizar el servicio Output para transformar un documento de PDF interactivo en un PDF no interactivo. Un documento PDF interactivo permite a los usuarios introducir o modificar datos que se encuentran en los campos del documento PDF. El proceso de transformar un documento de PDF interactivo en un documento de PDF no interactivo se llama *aplanar*. Cuando se aplana un documento PDF, un usuario no puede modificar los datos de los campos del documento. Una razón para acoplar un documento PDF es garantizar que no se puedan modificar los datos.

Puede acoplar los siguientes tipos de documentos PDF:

* Documentos de PDF XFA interactivos
* Acrobat Forms

El intento de acoplar un PDF que es un documento PDF no interactivo provoca una excepción.

>[!NOTE]
>
>Para obtener más información sobre el servicio Output , consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-9}

Para acoplar un documento de PDF interactivo a un documento de PDF no interactivo, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto Cliente de salida.
1. Recupere un documento de PDF interactivo.
1. Transforme el documento del PDF.
1. Guarde el documento de PDF no interactivo como archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, deberá reemplazar los archivos adobe-Utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms. Para obtener información sobre la ubicación de todos los archivos JAR de AEM Forms, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creación de un objeto de cliente de salida**

Para poder realizar una operación de servicio de salida mediante programación, debe crear un objeto cliente de servicio de salida. Si utiliza la API de Java, cree un `OutputClient` objeto. Si utiliza la API del servicio web de salida, cree un `OutputServiceService` objeto.

**Recuperar un documento PDF interactivo**

Recupere un documento de PDF interactivo que desee transformar en un documento de PDF no interactivo. Si se intenta transformar un documento PDF no interactivo, se producirá una excepción.

**Transformar el documento del PDF**

Después de recuperar un documento de PDF interactivo, puede transformarlo en un documento de PDF no interactivo. El servicio Output devuelve un documento PDF no interactivo.

**Guarde el documento de PDF no interactivo como archivo de PDF**

Puede guardar el documento de PDF no interactivo como un archivo de PDF.

**Consulte también lo siguiente**

[Acoplar un documento de PDF mediante la API de Java](creating-document-output-streams.md#flatten-a-pdf-document-using-the-java-api)

[Acoplar un documento de PDF mediante la API de servicio web](creating-document-output-streams.md#flatten-a-pdf-document-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Acoplar un documento de PDF mediante la API de Java {#flatten-a-pdf-document-using-the-java-api}

Acople un documento de PDF interactivo a un documento de PDF no interactivo mediante la API de salida (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-output-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un objeto Cliente de salida.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `OutputClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recupere un documento de PDF interactivo.

   * Cree un `java.io.FileInputStream` objeto que representa el documento de PDF interactivo que se va a transformar utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo de PDF interactivo.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Transforme el documento del PDF.

   Transforme el documento del PDF interactivo a un documento del PDF no interactivo invocando la variable `OutputServiceService` del objeto `transformPDF` y pasando los siguientes valores:

   * La variable `com.adobe.idp.Document` objeto que contiene el documento PDF interactivo.
   * A `TransformationFormat` valor de enumeración. Para generar un documento de PDF no interactivo, especifique `TransformationFormat.PDF`.
   * A `PDFARevisionNumber` valor de enumeración que especifica el número de revisión. Dado que este parámetro está diseñado para un documento PDF/A, puede especificar `null`.
   * Un valor de cadena que representa el número de enmienda y el año, separados por dos puntos. Dado que este parámetro está diseñado para un documento PDF/A, puede especificar `null`.
   * A `PDFAConformance` valor de enumeración que representa el nivel de conformidad PDF/A. Dado que este parámetro está diseñado para un documento PDF/A, puede especificar `null`.

   La variable `transformPDF` el método devuelve un `com.adobe.idp.Document` objeto que contiene un documento de PDF no interactivo.

1. Guarde el documento de PDF no interactivo como archivo de PDF.

   * Cree un `java.io.File` y asegúrese de que la extensión del nombre de archivo es .pdf.
   * Invocar el `Document` del objeto `copyToFile` para copiar el contenido del `Document` al archivo (asegúrese de usar la variable `Document` objeto devuelto por el `transformPDF` método).

**Consulte también lo siguiente**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Inicio rápido (modo EJB): Transformación de un documento de PDF mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[Inicio rápido (modo SOAP): Transformación de un documento de PDF mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Acoplar un documento de PDF mediante la API de servicio web {#flatten-a-pdf-document-using-the-web-service-api}

Acople un documento de PDF interactivo a un documento de PDF no interactivo mediante la API de salida (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto Cliente de salida.

   * Cree un `OutputServiceClient` usando su constructor predeterminado.
   * Cree un `OutputServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para usar MTOM.
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `OutputServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere un documento de PDF interactivo.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar el documento del PDF interactivo.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF interactivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Transforme el documento del PDF.

   Transforme el documento del PDF interactivo a un documento del PDF no interactivo invocando la variable `OutputClient` del objeto `transformPDF` y pasando los siguientes valores:

   * A `BLOB` objeto que contiene el documento PDF interactivo.
   * A `TransformationFormat` valor de enumeración. Para generar un documento de PDF no interactivo, especifique `TransformationFormat.PDF`.
   * A `PDFARevisionNumber` valor de enumeración que especifica el número de revisión.
   * Un valor booleano que especifica si la variable `PDFARevisionNumber` se utiliza el valor enum . Dado que este parámetro está diseñado para un documento PDF/A, puede especificar `false`.
   * Un valor de cadena que representa el número de enmienda y el año, separados por dos puntos. Dado que este parámetro está diseñado para un documento PDF/A, puede especificar `null`.
   * A `PDFAConformance` valor de enumeración que representa el nivel de conformidad PDF/A.
   * Valor booleano que especifica si la variable `PDFAConformance` se utiliza el valor enum . Dado que este parámetro está diseñado para un documento PDF/A, puede especificar `false`.

   La variable `transformPDF` el método devuelve un `BLOB` objeto que contiene un documento de PDF no interactivo.

1. Guarde el documento de PDF no interactivo como archivo de PDF.

   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF no interactivo.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto devuelto por el `transformPDF` método. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` miembro de datos.
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
