---
title: Creación de flujos de salida de documento
seo-title: Creación de flujos de salida de documento
description: nulo
seo-description: nulo
uuid: 80c28efa-35ce-4073-9ca6-2d93bcd67fdd
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: de527d50-991b-4ca3-a8ac-44d5cab988e9
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Creación de flujos de salida de documento {#creating-document-output-streams}

**Acerca del servicio de salida**

El servicio Output permite generar documentos como PDF (incluidos documentos PDF/A), PostScript, Printer Control Language (PCL) y los siguientes formatos de etiqueta:

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Con el servicio Output, puede combinar datos de formulario XML con un diseño de formulario y generar el documento en una impresora o archivo de red.

Existen dos formas de pasar un diseño de formulario (un archivo XDP) al servicio Output. Puede pasar una `com.adobe.idp.Document` instancia que contenga un diseño de formulario al servicio Output. O bien, puede pasar un valor URI que especifique la ubicación del diseño de formulario. Ambas formas se describen en *Programación con formularios* AEM.

>[!NOTE]
>
>El servicio Output no admite documentos PDF de Acrobat que contengan secuencias de comandos específicas de objetos de aplicación. Los documentos PDF de Acrobat que contienen secuencias de comandos específicas de objetos de aplicación no se procesan.

Las siguientes secciones muestran cómo pasar un diseño de formulario al servicio Output mediante un valor URI:

* [Creación de documentos PDF](creating-document-output-streams.md#creating-pdf-documents)
* [Creación de documentos PDF/A](creating-document-output-streams.md#creating-pdf-a-documents)

Las siguientes secciones muestran cómo pasar un diseño de formulario dentro de una `com.adobe.idp.Document` instancia:

* [Pasar documentos ubicados en Content Services (desaprobado) al servicio de salida](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [Creación de documentos PDF mediante fragmentos](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

Una consideración a la hora de decidir qué técnica utilizar es si está obteniendo el diseño de formulario de otro servicio de AEM Forms y, a continuación, pasarlo dentro de una `com.adobe.idp.Document` instancia. Las secciones *Pasar documentos al servicio* de salida y *Crear documentos PDF mediante fragmentos* muestran cómo obtener un diseño de formulario de otro servicio de AEM Forms. La primera sección recupera el diseño de formulario de Content Services (desaprobado). La segunda sección recupera el diseño de formulario del servicio Ensamblador.

Si está obteniendo el diseño de formulario desde una ubicación fija, como el sistema de archivos, puede utilizar cualquiera de estas técnicas. Es decir, puede especificar el valor URI en un archivo XDP o utilizar una `com.adobe.idp.Document` instancia.

Para pasar un valor URI que especifique la ubicación del diseño de formulario al crear un documento PDF, utilice el `generatePDFOutput` método . Del mismo modo, para pasar una `com.adobe.idp.Document` instancia al servicio Output al crear un documento PDF, utilice el `generatePDFOutput2` método .

Al enviar un flujo de salida a una impresora de red, también puede utilizar cualquiera de estas técnicas. Para enviar una secuencia de salida a una impresora pasando una `com.adobe.idp.Document` instancia que contenga un diseño de formulario, utilice el `sendToPrinter2`método . Para enviar un flujo de salida a una impresora pasando un valor URI, utilice el `sendToPrinter`método . La sección *Envío de flujos de impresión a impresoras* utiliza el `sendToPrinter` método .

Puede realizar estas tareas mediante el servicio Output:

* [Creación de documentos PDF](creating-document-output-streams.md#creating-pdf-documents)
* [Creación de documentos PDF/A](creating-document-output-streams.md#creating-pdf-a-documents)
* [Pasar documentos ubicados en Content Services (desaprobado) al servicio de salida](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [Creación de documentos PDF mediante fragmentos](creating-document-output-streams.md#creating-pdf-documents-using-fragments)
* [Impresión en archivos](creating-document-output-streams.md#printing-to-files)
* [Envío de flujos de impresión a impresoras](creating-document-output-streams.md#sending-print-streams-to-printers)
* [Creación de varios archivos de salida](creating-document-output-streams.md#creating-multiple-output-files)
* [Creación de reglas de búsqueda](creating-document-output-streams.md#creating-search-rules)
* [Acoplamiento de documentos PDF](creating-document-output-streams.md#flattening-pdf-documents)

   ***Nota **:Para obtener más información sobre el servicio Output, consulte Referencia de[servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).*

## Creación de documentos PDF {#creating-pdf-documents}

Puede utilizar el servicio Output para crear un documento PDF basado en un diseño de formulario y en datos de formulario XML proporcionados. El documento PDF creado por el servicio Output no es un documento PDF interactivo; un usuario no puede introducir ni modificar datos de formulario.

Si desea crear un documento PDF para almacenamiento a largo plazo, se recomienda crear un documento PDF/A. (Consulte [Creación de documentos](creating-document-output-streams.md#creating-pdf-a-documents)PDF/A).

Para crear un formulario PDF interactivo que permita a un usuario introducir datos, utilice el servicio Forms. (Consulte [Representación de formularios](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)PDF interactivos).

>[!NOTE]
>
>Para obtener más información sobre el servicio Output, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para crear un documento PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto Output Client.
1. Haga referencia a un origen de datos XML.
1. Configure las opciones de tiempo de ejecución de PDF.
1. Configure las opciones de procesamiento en tiempo de ejecución.
1. Genere un documento PDF.
1. Recupere los resultados de la operación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no es JBoss, deberá reemplazar los archivos adobe-utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms.

**Creación de un objeto Output Client**

Antes de realizar una operación de servicio Output mediante programación, debe crear un objeto cliente de servicio Output. Si utiliza la API de Java, cree un `OutputClient` objeto. Si está utilizando la API de servicio Web Output, cree un `OutputServiceService` objeto.

**Referencia a un origen de datos XML**

Para combinar datos con el diseño de formulario, debe hacer referencia a un origen de datos XML que contenga datos. Debe existir un elemento XML para cada campo de formulario que se va a rellenar con datos. El nombre del elemento XML debe coincidir con el nombre del campo. Un elemento XML se omite si no se corresponde con un campo de formulario o si el nombre del elemento XML no coincide con el nombre del campo. No es necesario coincidir con el orden en que se muestran los elementos XML si se especifican todos los elementos XML.

Considere el siguiente ejemplo de formulario de solicitud de préstamo.

![cp_cp_loanformdata](assets/cp_cp_loanformdata.png)

Para combinar datos en este diseño de formulario, debe crear un origen de datos XML que corresponda al formulario. El siguiente XML representa un origen de datos XML XDP que corresponde al formulario de solicitud de hipoteca de ejemplo.

```as3
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

**Definir opciones de tiempo de ejecución de PDF**

Configure la opción URI de archivo al crear un documento PDF. Esta opción especifica el nombre y la ubicación del archivo PDF que genera el servicio Output.

>[!NOTE]
>
>En lugar de definir la opción de tiempo de ejecución de URI de archivo, puede recuperar mediante programación el documento PDF del tipo de datos complejo que devuelve el servicio Output. Sin embargo, al establecer la opción de tiempo de ejecución de URI de archivo, no es necesario crear una lógica de aplicación que recupere mediante programación el documento PDF.

**Definición de opciones de tiempo de ejecución de procesamiento**

Puede definir las opciones de procesamiento en tiempo de ejecución al crear un documento PDF. Aunque estas opciones no son necesarias (a diferencia de las opciones en tiempo de ejecución de PDF que son necesarias), puede realizar tareas como mejorar el rendimiento del servicio Output. Por ejemplo, puede almacenar en caché el diseño de formulario que utiliza el servicio Output para mejorar su rendimiento.

Si utiliza un formulario Acrobat etiquetado como entrada, no puede utilizar el Java del servicio de salida ni la API del servicio Web para desactivar la configuración etiquetada. Si intenta establecer esta opción mediante programación en, `false`el documento PDF resultante seguirá estando etiquetado.

>[!NOTE]
>
>Si no especifica opciones de tiempo de ejecución de procesamiento, se utilizan los valores predeterminados. Para obtener información sobre las opciones de procesamiento en tiempo de ejecución, consulte la referencia de la `RenderOptionsSpec` clase. (Consulte Referencia [de la API de](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms).

**Generar un documento PDF**

Después de hacer referencia a un origen de datos XML válido que contiene datos de formulario y de definir las opciones en tiempo de ejecución, puede invocar el servicio Output, que resulta en la generación de un documento PDF.

Al generar un documento PDF, se especifican los valores de URI que necesita el servicio Output para crear un documento PDF. Un diseño de formulario se puede almacenar en ubicaciones como el sistema de archivos del servidor o como parte de una aplicación de AEM Forms. Se puede hacer referencia a un diseño de formulario (u otros recursos como un archivo de imagen) que existe como parte de una aplicación Forms mediante el valor URI raíz del contenido `repository:///`. Por ejemplo, piense en el siguiente diseño de formulario llamado *Loan.xdp* ubicado en una aplicación Forms denominada *Aplicaciones/FormsApplication*:

![cp_cp_formrepositorio](assets/cp_cp_formrepository.png)

Para acceder al archivo Loan.xdp que se muestra en la ilustración anterior, especifique `repository:///Applications/FormsApplication/1.0/FormsFolder/` como tercer parámetro pasado al `OutputClient` método `generatePDFOutput` del objeto. Especifique el nombre del formulario (*Loan.xdp*) como el segundo parámetro que se pasa al `OutputClient` método `generatePDFOutput` del objeto.

Si el archivo XDP contiene imágenes (u otros recursos como fragmentos), coloque los recursos en la misma carpeta de la aplicación que el archivo XDP. AEM Forms utiliza el URI raíz de contenido como ruta de acceso base para resolver referencias a imágenes. Por ejemplo, si el archivo Loan.xdp contiene una imagen, asegúrese de colocar la imagen en `Applications/FormsApplication/1.0/FormsFolder/`.

>[!NOTE]
>
>Puede hacer referencia a un URI de aplicación de Forms al invocar los `OutputClient` métodos `generatePDFOutput` o `generatePrintedOutput` del objeto.

>[!NOTE]
>
>Para ver un inicio rápido completo que crea un documento PDF haciendo referencia a un XDP ubicado en una aplicación Forms, consulte Inicio [rápido (modo EJB): Creación de un documento PDF basado en un archivo XDP de aplicación mediante la API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api)de Java.

**Recuperar los resultados de la operación**

Una vez que el servicio Output realiza una operación, devuelve varios elementos de datos, como datos XML de estado, que especifican si la operación se realizó correctamente.

**Consulte también**

[Creación de un documento PDF mediante la API de Java](creating-document-output-streams.md#create-a-pdf-document-using-the-java-api)

[Creación de un documento PDF mediante la API de servicio Web](creating-document-output-streams.md#create-a-pdf-document-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de API de servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Creación de un documento PDF mediante la API de Java {#create-a-pdf-document-using-the-java-api}

Cree un documento PDF mediante la API de salida (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-output-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto Output Client.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `OutputClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un origen de datos XML.

   * Cree un `java.io.FileInputStream` objeto que represente el origen de datos XML que se utiliza para rellenar el documento PDF utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo XML.
   * Cree un `com.adobe.idp.Document` objeto con su constructor. Pase el `java.io.FileInputStream` objeto.

1. Configure las opciones de tiempo de ejecución de PDF.

   * Cree un `PDFOutputOptionsSpec` objeto con su constructor.
   * Establezca la opción URI de archivo invocando el `PDFOutputOptionsSpec` método `setFileURI` del objeto. Pase un valor de cadena que especifique la ubicación del archivo PDF que genera el servicio Output. La opción URI de archivo es relativa al servidor de aplicaciones J2EE que aloja AEM Forms, no al equipo cliente.

1. Configure las opciones de procesamiento en tiempo de ejecución.

   * Cree un `RenderOptionsSpec` objeto con su constructor.
   * Almacene en caché el diseño de formulario para mejorar el rendimiento del servicio Output invocando el `RenderOptionsSpec` objeto `setCacheEnabled` y pasando `true`.
   >[!NOTE]
   >
   >No se puede establecer la versión del documento PDF utilizando el `RenderOptionsSpec` método del `setPdfVersion` objeto si el documento de entrada es un formulario de Acrobat (un formulario creado en Acrobat) o un documento XFA firmado o certificado. El documento PDF de salida conserva la versión original del PDF. Del mismo modo, no puede establecer la opción PDF de Adobe con etiquetas invocando el `RenderOptionsSpec` método del `setTaggedPDF` objeto si el documento de entrada es un formulario de Acrobat o un documento XFA firmado o certificado.

   >[!NOTE]
   >
   >No se puede establecer la opción de PDF linealizado mediante el `RenderOptionsSpec` método del `setLinearizedPDF` objeto si el documento PDF de entrada está certificado o firmado digitalmente. (Consulte Firma [digital de documentos](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*PDF).*

1. Genere un documento PDF.

   Cree un documento PDF invocando el `OutputClient` método `generatePDFOutput` del objeto y pasando los siguientes valores:

   * Un valor `TransformationFormat` de enumeración. Para generar un documento PDF, especifique `TransformationFormat.PDF`.
   * Un valor de cadena que especifica el nombre del diseño de formulario.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentra el diseño de formulario.
   * Un `PDFOutputOptionsSpec` objeto que contiene opciones de tiempo de ejecución de PDF.
   * Un `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * El `com.adobe.idp.Document` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario.
   El `generatePDFOutput` método devuelve un `OutputResult` objeto que contiene los resultados de la operación.

   >[!NOTE]
   >
   >Al generar un documento PDF invocando el `generatePDFOutput` método, tenga en cuenta que no se pueden combinar datos con un formulario PDF XFA firmado o certificado. (Consulte Firma [digital y certificación de documentos](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*).*

   >[!NOTE]
   >
   >El `OutputResult` método `getRecordLevelMetaDataList` del objeto devuelve `null`*.*

   >[!NOTE]
   >
   >También puede crear un documento PDF invocando el `OutputClient` método del `generatePDFOutput2` objeto. (Consulte [Pasar documentos ubicados en Content Services (desaprobado) al servicio](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*de salida).*

1. Recupere los resultados de la operación.

   * Recupere un `com.adobe.idp.Document` objeto que represente el estado de la `generatePDFOutput` operación invocando el `OutputResult` método `getStatusDoc` del objeto. Este método devuelve datos XML de estado que especifican si la operación se realizó correctamente.
   * Cree un `java.io.File` objeto que contenga los resultados de la operación. Asegúrese de que la extensión del nombre de archivo sea .xml.
   * Invoque el `com.adobe.idp.Document` método del `copyToFile` objeto para copiar el contenido del `com.adobe.idp.Document` objeto en el archivo (asegúrese de utilizar el `com.adobe.idp.Document` objeto devuelto por el `getStatusDoc` método).
   Aunque el servicio Output escribe el documento PDF en la ubicación especificada por el argumento que se pasa al `PDFOutputOptionsSpec` método del `setFileURI` objeto, puede recuperar mediante programación el documento PDF/A invocando el `OutputResult` método `getGeneratedDoc` del objeto.

**Consulte también**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Inicio rápido (modo EJB): Creación de un documento PDF mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[Inicio rápido (modo SOAP): Creación de un documento PDF mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creación de un documento PDF mediante la API de servicio Web {#create-a-pdf-document-using-the-web-service-api}

Cree un documento PDF mediante la API de salida (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto Output Client.

   * Cree un `OutputServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `OutputServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para usar MTOM.
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `OutputServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un origen de datos XML.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar datos XML que se combinarán con el documento PDF.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo XML que contiene los datos del formulario.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.

1. Definir opciones de tiempo de ejecución de PDF

   * Cree un `PDFOutputOptionsSpec` objeto con su constructor.
   * Defina la opción URI de archivo asignando un valor de cadena que especifique la ubicación del archivo PDF que el servicio Output genera para el miembro de `PDFOutputOptionsSpec` datos del `fileURI` objeto. La opción URI de archivo es relativa al servidor de aplicaciones J2EE que aloja AEM Forms, no al equipo cliente.

1. Configure las opciones de procesamiento en tiempo de ejecución.

   * Cree un `RenderOptionsSpec` objeto con su constructor.
   * Almacene en caché el diseño de formulario para mejorar el rendimiento del servicio Output asignando el valor `true` al miembro de datos del `RenderOptionsSpec` objeto `cacheEnabled` .
   >[!NOTE]
   >
   >No se puede establecer la versión del documento PDF utilizando el `RenderOptionsSpec` método del `setPdfVersion` objeto si el documento de entrada es un formulario de Acrobat (un formulario creado en Acrobat) o un documento XFA firmado o certificado. El documento PDF de salida conserva la versión original del PDF. Del mismo modo, no puede establecer la opción PDF de Adobe con etiquetas invocando el método `RenderOptionsSpec` * del `setTaggedPDF`objeto si el documento de entrada es un formulario de Acrobat o un documento XFA firmado o certificado.*

   >[!NOTE]
   >
   >No se puede establecer la opción de PDF linealizado mediante el uso del `RenderOptionsSpec` miembro del `linearizedPDF` objeto si el documento PDF de entrada está certificado o firmado digitalmente. (Consulte Firma [digital de documentos](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*PDF).*

1. Genere un documento PDF.

   Cree un documento PDF invocando el `OutputServiceService` método del `generatePDFOutput`objeto y pasando los siguientes valores:

   * Un valor `TransformationFormat` de enumeración. Para generar un documento PDF, especifique `TransformationFormat.PDF`.
   * Un valor de cadena que especifica el nombre del diseño de formulario.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentra el diseño de formulario.
   * Un `PDFOutputOptionsSpec` objeto que contiene opciones de tiempo de ejecución de PDF.
   * Un `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * El `BLOB` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario.
   * Un `BLOB` objeto que se rellena con el `generatePDFOutput` método . El `generatePDFOutput` método rellena este objeto con metadatos generados que describen el documento. (Este valor de parámetro solo es necesario para la invocación de servicio Web).
   * Un `BLOB` objeto que se rellena con el `generatePDFOutput` método . El `generatePDFOutput` método rellena este objeto con datos de resultados. (Este valor de parámetro solo es necesario para la invocación de servicio Web).
   * Un `OutputResult` objeto que contiene los resultados de la operación. (Este valor de parámetro solo es necesario para la invocación de servicio Web).
   >[!NOTE]
   >
   >Al generar un documento PDF invocando el `generatePDFOutput` método, tenga en cuenta que no se pueden combinar datos con un formulario PDF XFA firmado o certificado. (Consulte Firma [digital y certificación de documentos](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*).*

   >[!NOTE]
   >
   >También puede crear un documento PDF invocando el `OutputClient` método del `generatePDFOutput2` objeto. (Consulte [Pasar documentos ubicados en Content Services (desaprobado) al servicio](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*de salida).*

1. Recupere los resultados de la operación.

   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa una ubicación de archivo XML que contiene datos de resultados. Asegúrese de que la extensión del nombre de archivo sea .xml.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto que se rellenó con los datos de resultado mediante el `OutputServiceService` método `generatePDFOutput` del objeto (el octavo parámetro). Rellene la matriz de bytes obteniendo el valor del `BLOB` objeto `MTOM``field`.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en el archivo XML invocando el `System.IO.BinaryWriter` método del `Write` objeto y pasando la matriz de bytes.
   Consulte también

   [Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

   [Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

   [Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

   >[!NOTE]
   >
   >El `OutputServiceService` método del `generateOutput` objeto está en desuso.

## Creación de documentos PDF/A {#creating-pdf-a-documents}

Puede utilizar el servicio Output para crear un documento PDF/A. Dado que PDF/A es un formato de archivo para la conservación a largo plazo del contenido del documento, todas las fuentes se incrustan y el archivo se descomprime. Como resultado, un documento PDF/A suele ser más grande que un documento PDF estándar. Además, un documento PDF/A no contiene contenido de audio y vídeo. Al igual que otras tareas del servicio Output, se proporciona un diseño de formulario y datos para combinar con un diseño de formulario para crear un documento PDF/A.

La especificación PDF/A-1 consta de dos niveles de conformidad, a saber, a y b. La principal diferencia entre ambas es la compatibilidad con la estructura lógica (accesibilidad), que no es necesaria para el nivel de conformidad b. Independientemente del nivel de conformidad, PDF/A-1 dicta que todas las fuentes están incrustadas en el documento PDF/A generado.

Aunque PDF/A es el estándar para archivar documentos PDF, no es obligatorio que se utilice PDF/A para archivar si un documento PDF estándar satisface las necesidades de su empresa. El propósito del estándar PDF/A es establecer un archivo PDF que se pueda almacenar durante un largo período de tiempo y cumplir con los requisitos de conservación de documentos. Por ejemplo, una dirección URL no se puede incrustar en un PDF/A porque con el tiempo la dirección URL podría no ser válida.

Su organización debe evaluar sus propias necesidades, el período de tiempo que tiene intención de mantener el documento, las consideraciones sobre el tamaño del archivo y determinar su propia estrategia de archiving. Puede determinar mediante programación si un documento PDF es compatible con PDF/A mediante el servicio DocConverter. (Consulte Determinación [mediante programación de la conformidad con PDF/A](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)).

Un documento PDF/A debe utilizar la fuente especificada en el diseño de formulario y no se pueden sustituir las fuentes. Como resultado, si una fuente ubicada en un documento PDF no está disponible en el sistema operativo (SO) del host, se producirá una excepción.

Cuando se abre un documento PDF/A en Acrobat, se muestra un mensaje que confirma que el documento es un documento PDF/A, como se muestra en la siguiente ilustración.

![cp_cp_pdfamessage](assets/cp_cp_pdfamessage.png)

>[!NOTE]
>
>El sitio web de AIIM tiene una sección de preguntas frecuentes en PDF/A a la que puede acceder desde [https://www.aiim.org/documents/standards/19005-1_FAQ.pdf](https://www.aiim.org/documents/standards/19005-1_FAQ.pdf).

>[!NOTE]
>
>Para obtener más información sobre el servicio Output, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para crear un documento PDF/A, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto Output Client.
1. Haga referencia a un origen de datos XML.
1. Configure las opciones de tiempo de ejecución de PDF/A.
1. Configure las opciones de procesamiento en tiempo de ejecución.
1. Genere un documento PDF/A.
1. Recupere los resultados de la operación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación personalizada mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no es JBoss, deberá reemplazar los archivos adobe-utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms.

**Creación de un objeto Output Client**

Antes de realizar una operación de servicio Output mediante programación, debe crear un objeto cliente de servicio Output. Si utiliza la API de Java, cree un `OutputClient` objeto. Si está utilizando la API de servicio Web Output, cree un `OutputServiceService` objeto.

**Referencia a un origen de datos XML**

Para combinar datos con el diseño de formulario, debe hacer referencia a un origen de datos XML que contenga datos. Debe existir un elemento XML para cada campo de formulario que desee rellenar con datos. El nombre del elemento XML debe coincidir con el nombre del campo. Un elemento XML se omite si no se corresponde con un campo de formulario o si el nombre del elemento XML no coincide con el nombre del campo. No es necesario coincidir con el orden en que se muestran los elementos XML si se especifican todos los elementos XML.

**Definición de las opciones de tiempo de ejecución de PDF/A**

Puede definir la opción URI de archivo al crear un documento PDF/A. El URI es relativo al servidor de aplicaciones J2EE que aloja AEM Forms. Es decir, si establece C:\Adobe, el archivo se escribe en la carpeta del servidor, no en el equipo cliente. El URI especifica el nombre y la ubicación del archivo PDF/A que genera el servicio Output.

**Definición de opciones de tiempo de ejecución de procesamiento**

Puede definir las opciones de procesamiento en tiempo de ejecución al crear documentos PDF/A. Dos opciones relacionadas con PDF/A que puede establecer son los `PDFAConformance` valores y `PDFARevisionNumber` . El `PDFAConformance` valor hace referencia a la forma en que un documento PDF cumple los requisitos que especifican cómo se conservan los documentos electrónicos a largo plazo. Los valores válidos para esta opción son `A` y `B`. Para obtener información sobre la conformidad con los niveles a y b, consulte la especificación ISO PDF/A-1, titulada *ISO 19005-1 Document management*.

El `PDFARevisionNumber` valor hace referencia al número de revisión de un documento PDF/A. Para obtener información sobre el número de revisión de un documento PDF/A, consulte la especificación PDF/A-1 ISO, titulada *ISO 19005-1 Document management*.

>[!NOTE]
>
>No se puede establecer la opción PDF de Adobe con etiquetas en `false` al crear un documento PDF/A 1A. PDF/A 1A siempre será un documento PDF con etiquetas. Además, no puede establecer la opción PDF de Adobe con etiquetas en `true` al crear un documento PDF/A 1B. PDF/A 1B siempre será un documento PDF sin etiquetas.

**Generar un documento PDF/A**

Después de hacer referencia a un origen de datos XML válido que contiene datos de formulario y definir las opciones en tiempo de ejecución, puede invocar el servicio Output, lo que provoca que genere un documento PDF/A.

**Recuperar los resultados de la operación**

Una vez que el servicio Output realiza una operación, devuelve varios elementos de datos, como datos XML, que especifican si la operación se realizó correctamente.

**Consulte también**

[Creación de un documento PDF/A mediante la API de Java](creating-document-output-streams.md#create-a-pdf-a-document-using-the-java-api)

[Creación de un documento PDF/A mediante la API de servicio Web](creating-document-output-streams.md#create-a-pdf-a-document-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de API de servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Creación de un documento PDF/A mediante la API de Java {#create-a-pdf-a-document-using-the-java-api}

Cree un documento PDF/A mediante la API de salida (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-output-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto Output Client.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `OutputClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un origen de datos XML.

   * Cree un `java.io.FileInputStream` objeto que represente el origen de datos XML que se utiliza para rellenar el documento PDF/A utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo XML.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Configure las opciones de tiempo de ejecución de PDF/A.

   * Cree un `PDFOutputOptionsSpec` objeto con su constructor.
   * Establezca la opción URI de archivo invocando el `PDFOutputOptionsSpec` método `setFileURI` del objeto. Pase un valor de cadena que especifique la ubicación del archivo PDF que genera el servicio Output. La opción URI de archivo es relativa al servidor de aplicaciones J2EE que aloja AEM Forms, no al equipo cliente.

1. Configure las opciones de procesamiento en tiempo de ejecución.

   * Cree un `RenderOptionsSpec` objeto con su constructor.
   * Establezca el `PDFAConformance` valor invocando el `RenderOptionsSpec` método `setPDFAConformance` del objeto y pasando un valor de enumeración `PDFAConformance` que especifique el nivel de conformidad. Por ejemplo, para especificar el nivel de conformidad A, pase `PDFAConformance.A`.
   * Establezca el `PDFARevisionNumber` valor invocando el `RenderOptionsSpec` método `setPDFARevisionNumber` del objeto y pasando `PDFARevisionNumber.Revision_1`.
   >[!NOTE]
   >
   >La versión PDF de un documento PDF/A es 1.4 independientemente del valor que especifique para el `RenderOptionsSpec``setPdfVersion`*método del objeto.*

1. Genere un documento PDF/A.

   Cree un documento PDF/A invocando el `OutputClient` método del `generatePDFOutput` objeto y pasando los valores siguientes:

   * Un valor `TransformationFormat` de enumeración. Para generar un documento PDF/A, especifique `TransformationFormat.PDFA`.
   * Un valor de cadena que especifica el nombre del diseño de formulario.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentra el diseño de formulario.
   * Un `PDFOutputOptionsSpec` objeto que contiene opciones de tiempo de ejecución de PDF.
   * Un `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * El `com.adobe.idp.Document` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario.
   El `generatePDFOutput` método devuelve un `OutputResult` objeto que contiene los resultados de la operación.

   >[!NOTE]
   >
   >El `OutputResult` método `getRecordLevelMetaDataList` del objeto devuelve `null`.

   >[!NOTE]
   >
   >También puede crear un documento PDF/A invocando el método `OutputClient` 2 del `generatePDFOutput`objeto. (Consulte [Pasar documentos ubicados en Content Services (desaprobado) al servicio](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)de salida).

1. Recupere los resultados de la operación.

   * Cree un `com.adobe.idp.Document` objeto que represente el estado del `generatePDFOutput` método invocando el `OutputResult` método `getStatusDoc` del objeto.
   * Cree un `java.io.File` objeto que contenga los resultados de la operación. Asegúrese de que la extensión del nombre de archivo sea .xml.
   * Invoque el `com.adobe.idp.Document` método del `copyToFile` objeto para copiar el contenido del `com.adobe.idp.Document` objeto en el archivo (asegúrese de utilizar el `com.adobe.idp.Document` objeto devuelto por el `getStatusDoc` método).
   >[!NOTE]
   >
   >Aunque el servicio Output escribe el documento PDF/A en la ubicación especificada por el argumento que se pasa al `PDFOutputOptionsSpec` método del `setFileURI` objeto, puede recuperar mediante programación el documento PDF/A invocando el `OutputResult` método `getGeneratedDoc` del objeto.

**Consulte también**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Inicio rápido (modo SOAP): Creación de un documento PDF/A mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexión.

### Creación de un documento PDF/A mediante la API de servicio Web {#create-a-pdf-a-document-using-the-web-service-api}

Cree un documento PDF/A mediante la API de salida (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto Output Client.

   * Cree un `OutputServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `OutputServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para usar MTOM.
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `OutputServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un origen de datos XML.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar datos que se combinarán con el documento PDF/A.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF que desea codificar y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.

1. Configure las opciones de tiempo de ejecución de PDF/A.

   * Cree un `PDFOutputOptionsSpec` objeto con su constructor.
   * Defina la opción URI de archivo asignando un valor de cadena que especifique la ubicación del archivo PDF que el servicio Output genera para el miembro de `PDFOutputOptionsSpec` datos del `fileURI` objeto. La opción URI de archivo es relativa al servidor de aplicaciones J2EE que aloja AEM Forms, no al equipo cliente

1. Configure las opciones de procesamiento en tiempo de ejecución.

   * Cree un `RenderOptionsSpec` objeto con su constructor.
   * Establezca el `PDFAConformance` valor asignando un valor `PDFAConformance` enum al miembro de datos del `RenderOptionsSpec` objeto `PDFAConformance` . Por ejemplo, para especificar el nivel de conformidad A, asigne `PDFAConformance.A` a este miembro de datos.
   * Establezca el `PDFARevisionNumber` valor asignando un valor `PDFARevisionNumber` enum al miembro de datos del `RenderOptionsSpec` objeto `PDFARevisionNumber` . Asignar `PDFARevisionNumber.Revision_1` a este miembro de datos.
   >[!NOTE]
   >
   >La versión PDF de un documento PDF/A es 1.4 independientemente del valor que especifique.

1. Genere un documento PDF/A.

   Cree un documento PDF invocando el `OutputServiceService` método del `generatePDFOutput`objeto y pasando los siguientes valores:

   * Un valor de enumeración TransformationFormat. Para generar un documento PDF, especifique `TransformationFormat.PDFA`.
   * Un valor de cadena que especifica el nombre del diseño de formulario.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentra el diseño de formulario.
   * Un `PDFOutputOptionsSpec` objeto que contiene opciones de tiempo de ejecución de PDF.
   * Un `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * El `BLOB` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario.
   * Un `BLOB` objeto que se rellena con el `generatePDFOutput` método . El `generatePDFOutput` método rellena este objeto con metadatos generados que describen el documento. (Este valor de parámetro solo es necesario para la invocación de servicio Web).
   * Un `BLOB` objeto que se rellena con el `generatePDFOutput` método . El `generatePDFOutput` método rellena este objeto con datos de resultados. (Este valor de parámetro solo es necesario para la invocación de servicio Web).
   * Un `OutputResult` objeto que contiene los resultados de la operación. (Este valor de parámetro solo es necesario para la invocación de servicio Web).
   >[!NOTE]
   >
   >También puede crear un documento PDF/A invocando el método `OutputClient` 2 del `generatePDFOutput`objeto. (Consulte [Pasar documentos ubicados en Content Services (desaprobado) al servicio](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)de salida).

1. Recupere los resultados de la operación.

   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa una ubicación de archivo XML que contiene datos de resultados. Asegúrese de que la extensión del nombre de archivo sea .xml.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto que se rellenó con los datos de resultado mediante el `OutputServiceService` método `generatePDFOutput` del objeto (el octavo parámetro). Rellene la matriz de bytes obteniendo el valor del `BLOB` campo del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en el archivo XML invocando el `System.IO.BinaryWriter` método del `Write` objeto y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Pasar documentos ubicados en Content Services (desaprobado) al servicio de salida {#passing-documents-located-in-content-services-deprecated-to-the-output-service}

El servicio Output procesa un formulario PDF no interactivo basado en un diseño de formulario que se guarda normalmente como archivo XDP y se crea en Designer. Puede pasar un `com.adobe.idp.Document` objeto que contenga el diseño de formulario al servicio Output. A continuación, el servicio Output procesa el diseño de formulario ubicado en el `com.adobe.idp.Document` objeto.

Una ventaja de pasar un `com.adobe.idp.Document` objeto al servicio Output es que otras operaciones de servicio de AEM Forms devuelven una `com.adobe.idp.Document` instancia. Es decir, puede obtener una `com.adobe.idp.Document` instancia de otra operación de servicio y procesarla. Por ejemplo, supongamos que un archivo XDP se almacena en un nodo de Content Services (desaprobado) denominado `/Company Home/Form Designs`, como se muestra en la siguiente ilustración.

Puede recuperar mediante programación Loan.xdp de Content Services (desaprobado) y pasar el archivo XDP al servicio Output dentro de un `com.adobe.idp.Document` objeto.

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-2}

Para pasar un documento obtenido de Content Services (desaprobado) al servicio Output, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto Output y una API de cliente de Document Management.
1. Recupere el diseño de formulario de Content Services (desaprobado).
1. Procese el formulario PDF no interactivo.
1. Realice una acción con el flujo de datos.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, incluya los archivos proxy.

**Creación de un objeto Output y de una API de cliente de Document Management**

Antes de realizar una operación de API de servicio de salida mediante programación, cree un objeto de API de cliente de salida. Además, como este flujo de trabajo recupera un archivo XDP de Content Services (desaprobado), cree un objeto de API de Document Management.

**Recuperar el diseño de formulario de Content Services (obsoleto)**

Recupere el archivo XDP de Content Services (desaprobado) mediante Java o la API de servicio Web. El archivo XDP se devuelve dentro de una `com.adobe.idp.Document` instancia (o una `BLOB` instancia si utiliza servicios Web). A continuación, puede pasar la `com.adobe.idp.Document` instancia al servicio Output.

**Representar el formulario PDF no interactivo**

Para procesar un formulario no interactivo, pase la `com.adobe.idp.Document` instancia devuelta por Content Services (desaprobada) al servicio Output.

>[!NOTE]
>
>Dos nuevos métodos denominados `generatePDFOutput2`y g `eneratePrintedOutput2`aceptan un `com.adobe.idp.Document` objeto que contiene un diseño de formulario. También puede pasar un formulario `com.adobe.idp.Document`que contenga el diseño de formulario al servicio Output al enviar un flujo de impresión a una impresora de red.

**Realizar una acción con el flujo de datos del formulario**

Puede guardar el formulario no interactivo como archivo PDF. El formulario se puede ver en Adobe Reader o Acrobat.

**Consulte también**

[Pasar documentos al servicio de salida mediante la API de Java](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-java-api)

[Transmitir documentos al servicio de salida mediante la API de servicio Web](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de API de servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[Creación de documentos PDF mediante fragmentos](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

### Pasar documentos al servicio de salida mediante la API de Java {#pass-documents-to-the-output-service-using-the-java-api}

Transmitir un documento recuperado de Content Services (desaprobado) mediante el servicio de salida y la API de Content Services (desaprobada) (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-output-client.jar y adobe-contentservices-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto Output y una API de cliente de Document Management.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión. (Consulte [Configuración de propiedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexión).
   * Cree un `OutputClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.
   * Cree un `DocumentManagementServiceClientImpl` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recupere el diseño de formulario de Content Services (desaprobado).

   Invoque el `DocumentManagementServiceClientImpl` método del `retrieveContent` objeto y pase los valores siguientes:

   * Un valor de cadena que especifica el almacén donde se agrega el contenido. La tienda predeterminada es `SpacesStore`. Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la ruta completa del contenido que se va a recuperar (por ejemplo, `/Company Home/Form Designs/Loan.xdp`). Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la versión. Este valor es un parámetro opcional y puede pasar una cadena vacía. En este caso, se recupera la versión más reciente.
   El `retrieveContent` método devuelve un `CRCResult` objeto que contiene el archivo XDP. Recuperar una `com.adobe.idp.Document` instancia invocando el `CRCResult` método `getDocument` del objeto.

1. Procese el formulario PDF no interactivo.

   Invoque el `OutputClient` método del `generatePDFOutput2` objeto y pase los valores siguientes:

   * Un valor `TransformationFormat` de enumeración. Para generar un documento PDF, especifique `TransformationFormat.PDF`.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentran los recursos adicionales, como las imágenes.
   * Objeto `com.adobe.idp.Document` que representa el diseño de formulario (utilice la instancia devuelta por el `CRCResult` método `getDocument` del objeto).
   * Un `PDFOutputOptionsSpec` objeto que contiene opciones de tiempo de ejecución de PDF.
   * Un `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * El `com.adobe.idp.Document` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario.
   El `generatePDFOutput2` método devuelve un `OutputResult` objeto que contiene los resultados de la operación.

1. Realice una acción con el flujo de datos del formulario.

   * Recupere un `com.adobe.idp.Document` objeto que represente el formulario no interactivo invocando el `OutputResult` método `getGeneratedDoc` del objeto.
   * Cree un `java.io.File` objeto que contenga los resultados de la operación. Asegúrese de que la extensión del nombre de archivo sea .pdf.
   * Invoque el `com.adobe.idp.Document` método del `copyToFile` objeto para copiar el contenido del `com.adobe.idp.Document` objeto en el archivo (asegúrese de utilizar el `com.adobe.idp.Document` objeto devuelto por el `getGeneratedDoc` método).

**Consulte también**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Inicio rápido (modo EJB): Paso de documentos al servicio de salida mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[Inicio rápido (modo SOAP): Paso de documentos al servicio de salida mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Transmitir documentos al servicio de salida mediante la API de servicio Web {#pass-documents-to-the-output-service-using-the-web-service-api}

Transmitir un documento recuperado de Content Services (desaprobado) mediante el servicio Output y la API de Content Services (desaprobada) (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Dado que esta aplicación cliente invoca dos servicios de AEM Forms, cree dos referencias de servicio. Utilice la siguiente definición WSDL para la referencia de servicio asociada al servicio Output: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   Utilice la siguiente definición WSDL para la referencia de servicio asociada al servicio de Document Management: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Debido a que el tipo de datos es común a ambas referencias de servicio, califique completamente el tipo de datos `BLOB` `BLOB` cuando lo utilice. En el inicio rápido correspondiente del servicio Web, todas `BLOB` las instancias están completamente cualificadas.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto Output y una API de cliente de Document Management.

   * Cree un `OutputServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `OutputServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio Forms (por ejemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`). No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `OutputServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.
   >[!NOTE]
   >
   >Repita estos pasos para el cliente `DocumentManagementServiceClient`de servicio.

1. Recupere el diseño de formulario de Content Services (desaprobado).

   Recupere contenido invocando el `DocumentManagementServiceClient` método `retrieveContent` del objeto y pasando los siguientes valores:

   * Un valor de cadena que especifica el almacén donde se agrega el contenido. La tienda predeterminada es `SpacesStore`. Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la ruta completa del contenido que se va a recuperar (por ejemplo, `/Company Home/Form Designs/Loan.xdp`). Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la versión. Este valor es un parámetro opcional y puede pasar una cadena vacía. En este caso, se recupera la versión más reciente.
   * Parámetro de salida de cadena que almacena el valor del vínculo de exploración.
   * Parámetro `BLOB` de salida que almacena el contenido. Puede utilizar este parámetro de salida para recuperar el contenido.
   * Parámetro `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` de salida que almacena atributos de contenido.
   * Parámetro `CRCResult` de salida. En lugar de utilizar este objeto, puede utilizar el parámetro `BLOB` output para recuperar el contenido.

1. Procese el formulario PDF no interactivo.

   Invoque el `OutputServiceClient` método del `generatePDFOutput2` objeto y pase los valores siguientes:

   * Un valor `TransformationFormat` de enumeración. Para generar un documento PDF, especifique `TransformationFormat.PDF`.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentran los recursos adicionales, como las imágenes.
   * Un `BLOB` objeto que representa el diseño de formulario (utilice la `BLOB` instancia devuelta por Content Services (desaprobada)).
   * Un `PDFOutputOptionsSpec` objeto que contiene opciones de tiempo de ejecución de PDF.
   * Un `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * El `BLOB` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario.
   * Objeto de salida `BLOB` que se rellena con el `generatePDFOutput2` método . El `generatePDFOutput2` método rellena este objeto con metadatos generados que describen el documento. (Este valor de parámetro solo es necesario para la invocación de servicio Web).
   * Un `OutputResult` objeto de salida que contiene los resultados de la operación. (Este valor de parámetro solo es necesario para la invocación de servicio Web).
   El `generatePDFOutput2` método devuelve un `BLOB` objeto que contiene el formulario PDF no interactivo.

1. Realice una acción con el flujo de datos del formulario.

   * Cree un `System.IO.FileStream` objeto invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF interactivo y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto recuperado del `generatePDFOutput2` método. Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el `System.IO.BinaryWriter` método `Write` del objeto y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Pasar documentos ubicados en el repositorio al servicio de salida {#passing-documents-located-in-the-repository-to-the-output-service}

El servicio Output procesa un formulario PDF no interactivo basado en un diseño de formulario que se guarda normalmente como archivo XDP y se crea en Designer. Puede pasar un `com.adobe.idp.Document` objeto que contenga el diseño de formulario al servicio Output. A continuación, el servicio Output procesa el diseño de formulario ubicado en el `com.adobe.idp.Document` objeto.

Una ventaja de pasar un `com.adobe.idp.Document` objeto al servicio Output es que otras operaciones de servicio de AEM Forms devuelven una `com.adobe.idp.Document` instancia. Es decir, puede obtener una `com.adobe.idp.Document` instancia de otra operación de servicio y procesarla. Por ejemplo, supongamos que un archivo XDP se almacena en el repositorio de AEM Forms, como se muestra en la siguiente ilustración.

![pd_pd_formrepositorio](assets/pd_pd_formrepository.png)

La carpeta *FormsFolder* es una ubicación definida por el usuario en el repositorio de AEM Forms (esta ubicación es un ejemplo y no existe de forma predeterminada). En este ejemplo, se encuentra en esta carpeta un diseño de formulario denominado Loan.xdp. Además del diseño de formulario, en esta ubicación se pueden almacenar otros materiales de formulario, como imágenes. La ruta a un recurso ubicado en el repositorio de AEM Forms es:

`Applications/Application-name/Application-version/Folder.../Filename`

Puede recuperar mediante programación Loan.xdp del repositorio de AEM Forms y pasarlo al servicio Output dentro de un `com.adobe.idp.Document` objeto.

Puede crear un archivo PDF basado en un archivo XDP ubicado en el repositorio de dos maneras. Puede pasar la ubicación XDP por referencia o puede recuperar el XDP del repositorio mediante programación y pasarlo al servicio Output dentro de un archivo XDP.

[Inicio rápido (modo EJB): Creación de un documento PDF basado en un archivo XDP de aplicación mediante la API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api) de Java (muestra cómo pasar la ubicación del archivo XDP por referencia).

[Inicio rápido (modo EJB): Pasar un documento ubicado en el repositorio de AEM Forms al servicio Output mediante la API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) de Java (muestra cómo recuperar mediante programación el archivo XDP del repositorio de AEM Forms y pasarlo al servicio Output en una `com.adobe.idp.Document` instancia). (Esta sección explica cómo realizar esta tarea)

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-3}

Para pasar un documento obtenido del repositorio de AEM Forms al servicio Output, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto Output y una API de cliente de Document Management.
1. Recupere el diseño de formulario del repositorio de AEM Forms.
1. Procese el formulario PDF no interactivo.
1. Realice una acción con el flujo de datos.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, incluya los archivos proxy.

**Creación de un objeto Output y de una API de cliente de Document Management**

Antes de realizar una operación de API de servicio de salida mediante programación, cree un objeto de API de cliente de salida. Además, como este flujo de trabajo recupera un archivo XDP de Content Services (desaprobado), cree un objeto de API de Document Management.

**Recuperar el diseño de formulario del repositorio de AEM Forms**

Recupere el archivo XDP del repositorio de AEM Forms mediante la API de repositorio. (Consulte [Lectura de recursos](/help/forms/developing/aem-forms-repository.md#reading-resources)).

El archivo XDP se devuelve dentro de una `com.adobe.idp.Document` instancia (o una `BLOB` instancia si utiliza servicios Web). A continuación, puede pasar la `com.adobe.idp.Document` instancia al servicio Output.

**Representar el formulario PDF no interactivo**

Para procesar un formulario no interactivo, pase la `com.adobe.idp.Document` instancia que se devolvió mediante la API de repositorio de AEM Forms.

>[!NOTE]
>
>Dos nuevos métodos con nombre `generatePDFOutput2`y `generatePrintedOutput2`aceptar un `com.adobe.idp.Document`objeto que contiene un diseño de formulario. También puede pasar un `com.adobe.idp.Document` formulario que contenga el diseño de formulario al servicio Output al enviar un flujo de impresión a una impresora de red.

**Realizar una acción con el flujo de datos del formulario**

Puede guardar el formulario no interactivo como archivo PDF. El formulario se puede ver en Adobe Reader o Acrobat.

**Consulte también**

[Pasar documentos ubicados en el repositorio al servicio de salida mediante la API de Java](creating-document-output-streams.md#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de API de servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

ResourceRepositoryClient

### Pasar documentos ubicados en el repositorio al servicio de salida mediante la API de Java {#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api}

Transmitir un documento recuperado del repositorio mediante el servicio Output y la API de repositorio (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-output-client.jar y adobe-repository-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto Output y una API de cliente de Document Management.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión. (Consulte [Configuración de propiedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexión).
   * Cree un `OutputClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.
   * Cree un `DocumentManagementServiceClientImpl` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recupere el diseño de formulario del repositorio de AEM Forms.

   Invoque el `ResourceRepositoryClient` método del `readResourceContent` objeto y pase un valor de cadena que especifique la ubicación URI al archivo XDP. Por ejemplo, `/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`. Este valor es obligatorio. Este método devuelve una `com.adobe.idp.Document` instancia que representa el archivo XDP.

1. Procese el formulario PDF no interactivo.

   Invoque el `OutputClient` método del `generatePDFOutput2` objeto y pase los valores siguientes:

   * Un valor `TransformationFormat` de enumeración. Para generar un documento PDF, especifique `TransformationFormat.PDF`.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentran los recursos adicionales, como las imágenes. Por ejemplo, `repository:///Applications/FormsApplication/1.0/FormsFolder/`.
   * Objeto `com.adobe.idp.Document` que representa el diseño de formulario (utilice la instancia devuelta por el `ResourceRepositoryClient` método `readResourceContent` del objeto).
   * Un `PDFOutputOptionsSpec` objeto que contiene opciones de tiempo de ejecución de PDF.
   * Un `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * El `com.adobe.idp.Document` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario.
   El `generatePDFOutput2` método devuelve un `OutputResult` objeto que contiene los resultados de la operación.

1. Realice una acción con el flujo de datos del formulario.

   * Recupere un `com.adobe.idp.Document` objeto que represente el formulario no interactivo invocando el `OutputResult` método `getGeneratedDoc` del objeto.
   * Cree un `java.io.File` objeto que contenga los resultados de la operación. Asegúrese de que la extensión del nombre de archivo sea .pdf.
   * Invoque el `com.adobe.idp.Document` método del `copyToFile` objeto para copiar el contenido del `com.adobe.idp.Document` objeto en el archivo (asegúrese de utilizar el `com.adobe.idp.Document` objeto devuelto por el `getGeneratedDoc` método).

**Consulte también**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Inicio rápido (modo EJB): Paso de un documento ubicado en el repositorio de AEM Forms al servicio Output mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Creación de documentos PDF mediante fragmentos {#creating-pdf-documents-using-fragments}

Puede utilizar los servicios Salida y Ensamblador para crear un flujo de salida, como un documento PDF, basado en fragmentos. El servicio Ensamblador ensambla un documento XDP basado en fragmentos ubicados en varios archivos XDP. El documento XDP ensamblado se pasa al servicio Output, que crea un documento PDF. Aunque este flujo de trabajo muestra un documento PDF que se está generando, el servicio Output puede generar otros tipos de salida, como ZPL, para este flujo de trabajo. Un documento PDF se utiliza únicamente para fines de discusión.

La siguiente ilustración muestra este flujo de trabajo.

![cp_cp_outputassemfragments](assets/cp_cp_outputassemblefragments.png)

Antes de leer *Creación de documentos PDF mediante fragmentos*, se recomienda familiarizarse con el uso del servicio Ensamblador para ensamblar varios documentos XDP. (Consulte [Compilación de varios fragmentos](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)XDP).

>[!NOTE]
>
>También puede pasar un diseño de formulario ensamblado por el servicio Ensamblador al servicio Forms en lugar del servicio Output. La diferencia principal entre el servicio Output y el servicio Forms es que el servicio Forms genera documentos PDF interactivos y el servicio Output produce documentos PDF no interactivos. Además, el servicio Forms no puede generar flujos de salida basados en impresoras como ZPL.

>[!NOTE]
>
>Para obtener más información sobre el servicio Output, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-4}

Para crear un documento PDF basado en fragmentos, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto Cliente de salida y ensamblado.
1. Utilice el servicio Ensamblador para generar el diseño de formulario.
1. Utilice el servicio Output para generar el documento PDF.
1. Guarde el documento PDF como archivo PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto cliente de salida y ensamblado**

Antes de realizar mediante programación una operación de API de servicio de salida, cree un objeto de API de cliente de salida. Además, como este flujo de trabajo invoca el servicio Ensamblador para crear el diseño de formulario, cree un objeto de API de cliente de ensamblador.

**Utilice el servicio Ensamblador para generar el diseño de formulario**

Utilice el servicio Compilador para generar el diseño de formulario con fragmentos. El servicio Ensamblador devuelve una `com.adobe.idp.Document` instancia que contiene el diseño de formulario.

**Utilice el servicio Output para generar el documento PDF**

Puede utilizar el servicio Output para generar un documento PDF utilizando el diseño de formulario que creó el servicio Ensamblador. Pase la `com.adobe.idp.Document` instancia que el servicio Ensamblador devolvió al servicio Output.

**Guardar el documento PDF como archivo PDF**

Una vez que el servicio Output haya generado un documento PDF, puede guardarlo como archivo PDF.

**Consulte también**

[Creación de un documento PDF basado en fragmentos mediante la API de Java](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-java-api)

[Creación de un documento PDF basado en fragmentos mediante la API de servicio Web](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de API de servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[Compilación de varios fragmentos XDP](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)

[Creación de documentos PDF](creating-document-output-streams.md#creating-pdf-documents)

### Creación de un documento PDF basado en fragmentos mediante la API de Java {#create-a-pdf-document-based-on-fragments-using-the-java-api}

Cree un documento PDF basado en fragmentos mediante la API de servicio de salida y la API de servicio de ensamblador (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-output-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto Cliente de salida y ensamblado.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `OutputClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.
   * Cree un `AssemblerServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Utilice el servicio Ensamblador para generar el diseño de formulario.

   Invoque el `AssemblerServiceClient` método del `invokeDDX` objeto y pase los siguientes valores obligatorios:

   * Un `com.adobe.idp.Document` objeto que representa el documento DDX que se va a utilizar.
   * Un `java.util.Map` objeto que contiene los archivos XDP de entrada.
   * Un `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica las opciones de tiempo de ejecución, incluyendo la fuente predeterminada y el nivel de registro de trabajos.
   El `invokeDDX` método devuelve un `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contiene el documento XDP ensamblado. Para recuperar el documento XDP ensamblado, realice las siguientes acciones:

   * Invocar el `AssemblerResult` método del `getDocuments` objeto. Este método devuelve un `java.util.Map` objeto.
   * Repita el `java.util.Map` objeto hasta que encuentre el `com.adobe.idp.Document` objeto resultante.
   * Invocar el `com.adobe.idp.Document` método del `copyToFile` objeto para extraer el documento XDP ensamblado.


1. Utilice el servicio Output para generar el documento PDF.

   Invoque el `OutputClient` método del `generatePDFOutput2` objeto y pase los valores siguientes:

   * Un valor `TransformationFormat` de enumeración. Para generar un documento PDF, especifique `TransformationFormat.PDF`
   * Un valor de cadena que especifica la raíz del contenido donde se ubican los recursos adicionales, como las imágenes.
   * Un `com.adobe.idp.Document` objeto que representa el diseño de formulario (utilice la instancia devuelta por el servicio Ensamblador)
   * Un `PDFOutputOptionsSpec` objeto que contiene opciones de tiempo de ejecución de PDF
   * Un `RenderOptionsSpec` objeto que contiene opciones de tiempo de ejecución de procesamiento
   * El `com.adobe.idp.Document` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario
   El `generatePDFOutput2` método devuelve un `OutputResult` objeto que contiene los resultados de la operación

1. Guarde el documento PDF como archivo PDF.

   * Recupere un `com.adobe.idp.Document` objeto que represente el documento PDF invocando el `OutputResult` método `getGeneratedDoc` del objeto.
   * Cree un `java.io.File` objeto que contenga los resultados de la operación. Asegúrese de que la extensión de nombre de archivo sea .pdf.
   * Invocar el `com.adobe.idp.Document` método del `copyToFile` objeto para copiar el contenido del `com.adobe.idp.Document` objeto en el archivo. (Asegúrese de utilizar el `com.adobe.idp.Document` objeto que devolvió el `getGeneratedDoc` método).

**Consulte también**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Inicio rápido (modo EJB): Creación de un documento PDF basado en fragmentos mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[Inicio rápido (modo SOAP): Creación de un documento PDF basado en fragmentos mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexión.

### Creación de un documento PDF basado en fragmentos mediante la API de servicio Web {#create-a-pdf-document-based-on-fragments-using-the-web-service-api}

Cree un documento PDF basado en fragmentos mediante la API de servicio de salida y la API de servicio de ensamblador (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Utilice la siguiente definición WSDL para la referencia de servicio asociada al servicio Output:

   ```as3
    http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1.
   ```

   Utilice la siguiente definición WSDL para la referencia de servicio asociada al servicio de ensamblador:

   ```as3
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   Debido a que el tipo de datos es común a ambas referencias de servicio, califique completamente el tipo de datos `BLOB` `BLOB` cuando lo utilice. En el inicio rápido correspondiente del servicio Web, todas `BLOB` las instancias están completamente cualificadas.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto Cliente de salida y ensamblado.

   * Cree un `OutputServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `OutputServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para usar MTOM.
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `OutputServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al `OutputServiceClient.ClientCredentials.UserName.UserName`campo.
      * Asigne el valor de contraseña correspondiente al `OutputServiceClient.ClientCredentials.UserName.Password`campo.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al `BasicHttpBindingSecurity.Transport.ClientCredentialType`campo.
   * Asigne el valor `BasicHttpSecurityMode.TransportCredentialOnly` constante al `BasicHttpBindingSecurity.Security.Mode`campo.
   >[!NOTE]
   >
   >Repita estos pasos para el `AssemblerServiceClient`objeto.

1. Utilice el servicio Ensamblador para generar el diseño de formulario.

   Invoque el `AssemblerServiceClient` método del `invokeDDX` objeto y pase los valores siguientes:

   * Un `BLOB` objeto que representa el documento DDX
   * El `MyMapOf_xsd_string_To_xsd_anyType` objeto que contiene los archivos necesarios
   * Un `AssemblerOptionSpec` objeto que especifica opciones de tiempo de ejecución
   El `invokeDDX` método devuelve un `AssemblerResult` objeto que contiene los resultados del trabajo y las excepciones que se hayan producido. Para obtener el documento XDP recién creado, realice las siguientes acciones:

   * Acceda al `AssemblerResult` campo del `documents` objeto, que es un `Map` objeto que contiene los documentos PDF resultantes.
   * Repita el `Map` objeto para recuperar el diseño de formulario ensamblado. Difundir el elemento `value` de la matriz a un `BLOB`. Transfiera esta `BLOB` instancia al servicio Output.


1. Utilice el servicio Output para generar el documento PDF.

   Invoque el `OutputServiceClient` método del `generatePDFOutput2` objeto y pase los valores siguientes:

   * Un valor `TransformationFormat` de enumeración. Para generar un documento PDF, especifique `TransformationFormat.PDF`.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentran los recursos adicionales, como las imágenes.
   * Un `BLOB` objeto que representa el diseño de formulario (utilice la `BLOB` instancia devuelta por el servicio Ensamblador).
   * Un `PDFOutputOptionsSpec` objeto que contiene opciones de tiempo de ejecución de PDF.
   * Un `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * El `BLOB` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario.
   * Objeto de salida `BLOB` que rellena el `generatePDFOutput2` método. El `generatePDFOutput2` método rellena este objeto con metadatos generados que describen el documento. (Este valor de parámetro solo es necesario para la invocación de servicio Web).
   * Un `OutputResult` objeto de salida que contiene los resultados de la operación. (Este valor de parámetro solo es necesario para la invocación de servicio Web).
   El `generatePDFOutput2` método devuelve un `BLOB` objeto que contiene el formulario PDF no interactivo.

1. Guarde el documento PDF como archivo PDF.

   * Cree un `System.IO.FileStream` objeto invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF interactivo y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto recuperado del `generatePDFOutput2` método. Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el `System.IO.BinaryWriter` método `Write` del objeto y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Impresión en archivos {#printing-to-files}

Puede utilizar el servicio Output para imprimir flujos como PostScript, Printer Control Language (PCL) o los siguientes formatos de etiqueta en un archivo:

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Con el servicio Output, puede combinar datos XML con un diseño de formulario e imprimir el formulario en un archivo. La siguiente ilustración muestra el servicio Output creando archivos láser y de etiquetas.

>[!NOTE]
>
>Para obtener información sobre el envío de flujos de impresión a impresoras, consulte [Envío de flujos de impresión a impresoras](creating-document-output-streams.md#sending-print-streams-to-printers).

>[!NOTE]
>
>Para obtener más información sobre el servicio Output, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-5}

Para imprimir en un archivo, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto Output Client.
1. Haga referencia a un origen de datos XML.
1. Configure las opciones de impresión en tiempo de ejecución necesarias para imprimir en un archivo.
1. Imprima el flujo de impresión en un archivo.
1. Recupere los resultados de la operación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no es JBoss, deberá reemplazar los archivos adobe-utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms. (Consulte [Inclusión de archivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)de biblioteca Java de AEM Forms).

**Creación de un objeto Output Client**

Antes de realizar una operación de servicio Output mediante programación, debe crear un objeto cliente de servicio Output. Si utiliza la API de Java, cree un `OutputClient` objeto. Si está utilizando la API de servicio Web Output, cree un `OutputServiceService` objeto.

**Referencia a un origen de datos XML**

Para imprimir un documento que contenga datos, debe hacer referencia a un origen de datos XML que contenga elementos XML para cada campo de formulario que desee rellenar con datos. El nombre del elemento XML debe coincidir con el nombre del campo. Un elemento XML se omite si no se corresponde con un campo de formulario o si el nombre del elemento XML no coincide con el nombre del campo. No es necesario coincidir con el orden en que se muestran los elementos XML si se especifican todos los elementos XML.

**Definición de las opciones de tiempo de ejecución de impresión necesarias para imprimir en un archivo**

Para imprimir en un archivo, debe definir la opción de tiempo de ejecución de URI de archivo especificando la ubicación y el nombre del archivo en el que se imprime el servicio Output. Por ejemplo, para indicar al servicio Output que imprima un archivo PostScript denominado *MortgageForm.ps* en C:\Adobe, especifique C:\Adobe\MortgageForm.ps.

>[!NOTE]
>
>Existen opciones opcionales de tiempo de ejecución que puede definir. Para obtener información sobre todas las opciones que puede definir, consulte la referencia de la `PrintedOutputOptionsSpec` clase en Referencia [de API de formularios](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM.

**Impresión del flujo de impresión en un archivo**

Después de hacer referencia a un origen de datos XML válido que contiene datos de formulario y definir las opciones de impresión en tiempo de ejecución, puede invocar el servicio Output, que hace que imprima un archivo.

**Recuperar los resultados de la operación**

Una vez que el servicio Output realiza una operación, devuelve varios elementos de datos, como datos XML, que especifican si la operación se realizó correctamente.

**Consulte también**

[Imprimir en archivos con la API de Java](creating-document-output-streams.md#print-to-files-using-the-java-api)

[Imprimir en archivos mediante la API de servicio Web](creating-document-output-streams.md#print-to-files-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de API de servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Imprimir en archivos con la API de Java {#print-to-files-using-the-java-api}

Imprimir en un archivo con la API de salida (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-output-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto Output Client.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `OutputClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un origen de datos XML.

   * Cree un `java.io.FileInputStream` objeto que represente el origen de datos XML que se utiliza para rellenar el documento utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo XML.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Configure las opciones de impresión en tiempo de ejecución necesarias para imprimir en un archivo.

   * Cree un `PrintedOutputOptionsSpec` objeto con su constructor.
   * Especifique el archivo invocando el `setFileURI` método del objeto PrintedOutputOptionsSpec y pasando un valor de cadena que represente el nombre y la ubicación del archivo. Por ejemplo, si desea que el servicio Output imprima en un archivo PostScript denominado MortgageForm.ps ubicado en C:\Adobe, especifique C:\\Adobe\MortgageForm.ps.
   * Especifique el número de copias que se van a imprimir invocando el `PrintedOutputOptionsSpec` método `setCopies` del objeto y pasando un valor entero que represente el número de copias.

1. Imprima el flujo de impresión en un archivo.

   Imprimir en un archivo invocando el `OutputClient` método del `generatePrintedOutput` objeto y pasando los siguientes valores:

   * Un valor de `PrintFormat` enumeración que especifica el formato de flujo de impresión que se va a crear. Por ejemplo, para crear un flujo de impresión PostScript, pase `PrintFormat.PostScript`.
   * Un valor de cadena que especifica el nombre del diseño de formulario.
   * Un valor de cadena que especifica la ubicación de los archivos colaterales relacionados, como los archivos de imagen.
   * Un valor de cadena que especifica la ubicación del archivo XDC que se va a utilizar (puede pasar `null` si ha especificado el archivo XDC que se va a utilizar con el `PrintedOutputOptionsSpec` objeto).
   * El `PrintedOutputOptionsSpec` objeto que contiene las opciones de tiempo de ejecución necesarias para imprimir en un archivo.
   * El `com.adobe.idp.Document` objeto que contiene el origen de datos XML que contiene datos de formulario.
   El `generatePrintedOutput` método devuelve un `OutputResult` objeto que contiene los resultados de la operación.

   >[!NOTE]
   >
   >El `OutputResult` método `getRecordLevelMetaDataList` del objeto devuelve `null`.

1. Recupere los resultados de la operación.

   * Cree un `com.adobe.idp.Document` objeto que represente el estado del `generatePrintedOutput` método invocando el `OutputResult` método `getStatusDoc` del objeto (el `OutputResult` objeto fue devuelto por el `generatePrintedOutput` método).
   * Cree un `java.io.File` objeto que contenga los resultados de la operación. Asegúrese de que la extensión de archivo es XML.
   * Invoque el `com.adobe.idp.Document` método del `copyToFile` objeto para copiar el contenido del `com.adobe.idp.Document` objeto en el archivo (asegúrese de utilizar el `com.adobe.idp.Document` objeto devuelto por el `getStatusDoc` método).

**Consulte también**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Inicio rápido (modo SOAP): Impresión en un archivo mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexión.

### Imprimir en archivos mediante la API de servicio Web {#print-to-files-using-the-web-service-api}

Imprimir en un archivo con la API de salida (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto Output Client.

   * Cree un `OutputServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `OutputServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para usar MTOM.
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `OutputServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un origen de datos XML.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar datos de formulario.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que especifica la ubicación del archivo XML que contiene datos de formulario.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `binaryData` propiedad con el contenido de la matriz de bytes.

1. Configure las opciones de impresión en tiempo de ejecución necesarias para imprimir en un archivo.

   * Cree un `PrintedOutputOptionsSpec` objeto con su constructor.
   * Especifique el archivo asignando un valor de cadena que represente la ubicación y el nombre del archivo al miembro de datos del `PrintedOutputOptionsSpec` objeto `fileURI` . Por ejemplo, si desea que el servicio Output imprima en un archivo PostScript denominado *MortgageForm.ps* ubicado en C:\Adobe, especifique C:\\Adobe\MortgageForm.ps.
   * Especifique el número de copias que se van a imprimir asignando un valor entero que represente el número de copias a los miembros de datos del `PrintedOutputOptionsSpec` objeto `copies` .

1. Imprima el flujo de impresión en un archivo.

   Imprimir en un archivo invocando el `OutputServiceService` método del `generatePrintedOutput` objeto y pasando los siguientes valores:

   * Un valor de `PrintFormat` enumeración que especifica el formato de flujo de impresión que se va a crear. Por ejemplo, para crear un flujo de impresión PostScript, pase `PrintFormat.PostScript`.
   * Un valor de cadena que especifica el nombre del diseño de formulario.
   * Un valor de cadena que especifica la ubicación de los archivos colaterales relacionados, como los archivos de imagen.
   * Un valor de cadena que especifica la ubicación del archivo XDC que se va a utilizar (puede pasar `null` si ha especificado el archivo XDC que se va a utilizar con el `PrintedOutputOptionsSpec` objeto).
   * El `PrintedOutputOptionsSpec` objeto que contiene las opciones de tiempo de ejecución de impresión necesarias para imprimir en un archivo.
   * El `BLOB` objeto que contiene el origen de datos XML que contiene datos de formulario.
   * Un `BLOB` objeto que se rellena con el `generatePDFOutput` método . El `generatePDFOutput` método rellena este objeto con metadatos generados que describen el documento. (Este valor de parámetro solo es necesario para la invocación de servicio Web).
   * Un `BLOB` objeto que se rellena con el `generatePDFOutput` método . El `generatePDFOutput` método rellena este objeto con datos de resultados. (Este valor de parámetro solo es necesario para la invocación de servicio Web).
   * Un `OutputResult` objeto que contiene los resultados de la operación. (Este valor de parámetro solo es necesario para la invocación de servicio Web).

1. Recupere los resultados de la operación.

   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa una ubicación de archivo XML que contiene datos de resultados. Asegúrese de que la extensión de archivo es XML.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto que se rellenó con los datos de resultado mediante el `OutputServiceService` método `generatePDFOutput` del objeto (el octavo parámetro). Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en el archivo XML invocando el `System.IO.BinaryWriter` método del `Write` objeto y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Envío de flujos de impresión a impresoras {#sending-print-streams-to-printers}

Puede utilizar el servicio Output para enviar flujos de impresión como PostScript, Printer Control Language (PCL) o los siguientes formatos de etiqueta a impresoras en red:

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Con el servicio Output, puede combinar datos XML con un diseño de formulario y obtener el formulario como una secuencia de impresión. Por ejemplo, puede crear un flujo de impresión PostScript y enviarlo a una impresora de red. La siguiente ilustración muestra el servicio Output que envía flujos de impresión a impresoras de red.

>[!NOTE]
>
>Para mostrar cómo enviar un flujo de impresión a una impresora de red, esta sección envía un flujo de impresión PostScript a una impresora de red mediante el protocolo de impresora SharedPrinter.

>[!NOTE]
>
>Para obtener más información sobre el servicio Output, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-6}

Para enviar un flujo de impresión a una impresora de red, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto Output Client.
1. Haga referencia a un origen de datos XML.
1. Definición de opciones de tiempo de ejecución de impresión
1. Recupere un documento para imprimir.
1. Envíe el documento a una impresora de red.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no es JBoss, deberá reemplazar los archivos adobe-utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms.

**Creación de un objeto Output Client**

Antes de realizar una operación de servicio Output mediante programación, cree un objeto de cliente de servicio Output. Si utiliza la API de Java, cree un `OutputClient` objeto. Si está utilizando la API de servicio Web Output, cree un `OutputServiceClient` objeto.

**Referencia a un origen de datos XML**

Para imprimir un documento que contenga datos, debe hacer referencia a un origen de datos XML que contenga elementos XML para cada campo de formulario que desee rellenar con datos. El nombre del elemento XML debe coincidir con el nombre del campo. Un elemento XML se omite si no se corresponde con un campo de formulario o si el nombre del elemento XML no coincide con el nombre del campo. No es necesario coincidir con el orden en que se muestran los elementos XML si se especifican todos los elementos XML.

**Definición de opciones de tiempo de ejecución de impresión**

Puede definir las opciones de tiempo de ejecución al enviar un flujo de impresión a una impresora, incluidas las siguientes opciones:

* **Copias**: Especifica el número de copias que se van a enviar a la impresora. El valor predeterminado es 1.
* **Grapa**: Se establece una opción XCI cuando se utiliza una grapadora. Esta opción se puede especificar en el modelo de configuración mediante el elemento básico y se utiliza únicamente para impresoras PS y PCL.
* **OutputJog**: Se establece una opción XCI cuando las páginas de salida se deben bloquear (desplazar físicamente en la bandeja de salida). Esta opción es solo para impresoras PS y PCL.
* **OutputBin**: Valor XCI que se utiliza para permitir que el controlador de impresión seleccione la bandeja de salida adecuada.

>[!NOTE]
>
>Para obtener información sobre todas las opciones de tiempo de ejecución que puede establecer, consulte la referencia de la `PrintedOutputOptionsSpec` clase.

**Recuperar un documento para imprimir**

Recupere un flujo de impresión para enviarlo a una impresora. Por ejemplo, puede recuperar un archivo PostScript y enviarlo a una impresora.

Puede elegir enviar un archivo PDF si la impresora admite PDF. Sin embargo, un problema con el envío de un documento PDF a una impresora es que cada fabricante de la impresora tiene una implementación diferente del intérprete de PDF. Es decir, algunos fabricantes de impresión utilizan la interpretación de Adobe PDF, pero depende de la impresora. Otras impresoras tienen su propio intérprete de PDF. Como resultado, los resultados de impresión pueden variar.

Otra limitación del envío de un documento PDF a una impresora es que solo imprime; no puede acceder a la impresión a doble cara, a la selección de bandeja de papel ni al grapado, excepto a través de los ajustes de la impresora.

Para recuperar un documento para imprimir, utilice el `generatePrintedOutput` método . La siguiente tabla especifica los tipos de contenido que se establecen para un flujo de impresión determinado al utilizar el `generatePrintedOutput` método .

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
   <td><p>Crea un archivo dpl203.xdc de forma predeterminada o flujo de salida xdc personalizado.</p></td>
  </tr>
  <tr>
   <td><p>DPL300DPI </p></td>
   <td><p>Crea un flujo de salida DPL 300 PPP.</p></td>
  </tr>
  <tr>
   <td><p>DPL406DPI </p></td>
   <td><p>Crea un flujo de salida DPL 400 PPP.</p></td>
  </tr>
  <tr>
   <td><p>DPL600DPI </p></td>
   <td><p>Crea un flujo de salida DPL 600 PPP.</p></td>
  </tr>
  <tr>
   <td><p>GenericColorPCL </p></td>
   <td><p>Crea un flujo de salida PCL de color genérico (5c).</p></td>
  </tr>
  <tr>
   <td><p>GenericPSLevel3 </p></td>
   <td><p>Crea un flujo de salida PostScript Level 3 genérico.</p></td>
  </tr>
  <tr>
   <td><p>IPL </p></td>
   <td><p>Crea un flujo de salida IPL personalizado.</p></td>
  </tr>
  <tr>
   <td><p>IPL300DPI </p></td>
   <td><p>Crea un flujo de salida IPL 300 PPP.</p></td>
  </tr>
  <tr>
   <td><p>IPL400DPI </p></td>
   <td><p>Crea un flujo de salida IPL de 400 PPP.</p></td>
  </tr>
  <tr>
   <td><p>PCL </p></td>
   <td><p>Crea un flujo de salida monocromo PCL (5e) genérico.</p></td>
  </tr>
  <tr>
   <td><p>PostScript </p></td>
   <td><p>Crea un flujo de salida PostScript Level 2 genérico.</p></td>
  </tr>
  <tr>
   <td><p>TPCL </p></td>
   <td><p>Crea un flujo de salida TPCL personalizado.</p></td>
  </tr>
  <tr>
   <td><p>TPCL305DPI </p></td>
   <td><p>Crea un flujo de salida TPCL 305 PPP.</p></td>
  </tr>
  <tr>
   <td><p>TPCL600DPI </p></td>
   <td><p>Crea un flujo de salida TPCL 600 PPP.</p></td>
  </tr>
  <tr>
   <td><p>ZPL </p></td>
   <td><p>Crea un flujo de salida ZPL 203 PPP.</p></td>
  </tr>
  <tr>
   <td><p>ZPL300DPI </p></td>
   <td><p>Crea un flujo de salida ZPL 300 PPP.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>También puede enviar un flujo de impresión a una impresora mediante el `generatePrintedOutput2` método . Sin embargo, los inicios rápidos asociados con la sección Envío de flujos de impresión a impresoras utilizan el `generatePrintedOutput` método .

**Envío del flujo de impresión a una impresora de red**

Después de recuperar un documento para imprimir, puede invocar el servicio Output, que hace que envíe un flujo de impresión a una impresora de red. Para que el servicio Output pueda localizar correctamente la impresora, debe especificar tanto el servidor de impresión como el nombre de la impresora. Además, también debe especificar el protocolo de impresión.

>[!NOTE]
>
>Si PDFG está instalado en el servidor de formularios y el servidor se ejecuta en Windows Server 2008, no puede utilizar la propiedad SharedPrinter. En este caso, utilice un protocolo de impresora diferente.

>[!NOTE]
>
>Si está utilizando una impresora de red y el mecanismo de acceso es SharedPrinter, debe especificar la ruta de red completa de la impresora.Envíe un flujo de impresión a una impresora de red mediante la API de Java

Envíe un flujo de impresión a una impresora de red mediante la API de salida (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-output-client.jar, en la ruta de clases del proyecto Java.

1. Creación de un objeto Output Client

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `OutputClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Referencia a un origen de datos XML

   * Cree un `java.io.FileInputStream` objeto que represente el origen de datos XML que se utiliza para rellenar el documento utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo XML.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Definición de opciones de tiempo de ejecución de impresión

   Cree un `PrintedOutputOptionsSpec` objeto que represente las opciones de impresión en tiempo de ejecución. Por ejemplo, puede especificar el número de copias que se van a imprimir invocando el `PrintedOutputOptionsSpec` método `setCopies` del objeto.

   >[!NOTE]
   >
   >No se puede establecer el valor de paginación utilizando el `PrintedOutputOptionsSpec` método del `setPagination` objeto si se está generando un flujo de impresión ZPL. Del mismo modo, no puede establecer las siguientes opciones para un flujo de impresión ZPL: OutputJog, PageOffset y Staple. El `setPagination` método no es válido para la generación de PostScript. Sólo es válido para la generación de PCL.

1. Recuperar un documento para imprimir

   * Recupere un documento para imprimir invocando el `OutputClient` método `generatePrintedOutput` del objeto y pasando los valores siguientes:

      * Un valor de `PrintFormat` enumeración que especifica el flujo de impresión. Por ejemplo, para crear un flujo de impresión PostScript, pase `PrintFormat.PostScript`.
      * Un valor de cadena que especifica el nombre del diseño de formulario.
      * Un valor de cadena que especifica la ubicación de los archivos colaterales relacionados, como los archivos de imagen.
      * Un valor de cadena que especifica la ubicación del archivo XDC que se va a utilizar.
      * El `PrintedOutputOptionsSpec` objeto que contiene las opciones de tiempo de ejecución necesarias para imprimir en un archivo.
      * El `com.adobe.idp.Document` objeto que representa el origen de datos XML que contiene los datos de formulario que se van a combinar con el diseño de formulario.
      Este método devuelve un `OutputResult` objeto que contiene los resultados de la operación.

   * Cree un `com.adobe.idp.Document` objeto para enviarlo a la impresora invocando el `OutputResult` método ‘s `getGeneratedDoc` . Este método devuelve un `com.adobe.idp.Document` objeto.


1. Envío del flujo de impresión a una impresora de red

   Envíe el flujo de impresión a una impresora de red invocando el `OutputClient` método `sendToPrinter` del objeto y pasando los valores siguientes:

   * Un `com.adobe.idp.Document` objeto que representa el flujo de impresión que se va a enviar a la impresora.
   * Un valor `PrinterProtocol` de enumeración que especifica el protocolo de impresora que se va a utilizar. Por ejemplo, para especificar el protocolo SharedPrinter, pase `PrinterProtocol.SharedPrinter`.
   * Un valor de cadena que especifica el nombre del servidor de impresión. Por ejemplo, suponiendo que el nombre del servidor de impresión sea PrintServer1, pase `\\\PrintSever1`.
   * Un valor de cadena que especifica el nombre de la impresora. Por ejemplo, suponiendo que el nombre de la impresora es Impresora1, pase `\\\PrintSever1\Printer1`.
   >[!NOTE]
   >
   >El `sendToPrinter` método se agregó a la API de AEM Forms en la versión 8.2.1.

### Envío de un flujo de impresión a una impresora mediante la API de servicio Web {#send-a-print-stream-to-a-printer-using-the-web-service-api}

Envíe un flujo de impresión a una impresora de red mediante la API de salida (servicio Web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto Output Client.

   * Cree un `OutputServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `OutputServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para usar MTOM.
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `OutputServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un origen de datos XML.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar datos de formulario.
   * Cree un `System.IO.FileStream` objeto invocando su constructor. Pase un valor de cadena que especifique la ubicación del archivo XML que contiene los datos del formulario.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Determinar la longitud de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.

1. Configure las opciones de impresión en tiempo de ejecución.

   Cree un `PrintedOutputOptionsSpec` objeto con su constructor. Por ejemplo, puede especificar el número de copias que se van a imprimir asignando un valor entero que represente el número de copias al miembro de `PrintedOutputOptionsSpec` datos del `copies` objeto.

   >[!NOTE]
   >
   >No se puede establecer el valor de paginación utilizando el miembro de datos del `PrintedOutputOptionsSpec` `pagination` objeto si se está generando un flujo de impresión ZPL. Del mismo modo, no puede establecer las siguientes opciones para un flujo de impresión ZPL: OutputJog, PageOffset y Staple. El miembro de datos `pagination` no es válido para la generación de PostScript. Sólo es válido para la generación de PCL.

1. Recupere un documento para imprimir.

   * Recupere un documento para imprimir invocando el `OutputServiceService` método `generatePrintedOutput` del objeto y pasando los valores siguientes:

      * Un valor de `PrintFormat` enumeración que especifica el flujo de impresión. Por ejemplo, para crear un flujo de impresión PostScript, pase `PrintFormat.PostScript`.
      * Un valor de cadena que especifica el nombre del diseño de formulario.
      * Un valor de cadena que especifica la ubicación de los archivos colaterales relacionados, como los archivos de imagen.
      * Un valor de cadena que especifica la ubicación del archivo XDC que se va a utilizar.
      * El `PrintedOutputOptionsSpec` objeto que contiene opciones de tiempo de ejecución de impresión que se utilizan al enviar un flujo de impresión a una impresora de red.
      * El `BLOB` objeto que contiene el origen de datos XML que contiene datos de formulario.
      * Un `BLOB` objeto que se rellena con el `generatePrintedOutput` método . El `generatePrintedOutput` método rellena este objeto con metadatos generados que describen el documento. (Este valor de parámetro solo es necesario para la invocación de servicio Web).
      * Un `BLOB` objeto que se rellena con el `generatePrintedOutput` método . El `generatePrintedOutput` método rellena este objeto con datos de resultados. (Este valor de parámetro solo es necesario para la invocación de servicio Web).
      * Un `OutputResult` objeto que contiene los resultados de la operación. (Este valor de parámetro solo es necesario para la invocación de servicio Web).
   * Cree un `BLOB` objeto para enviarlo a la impresora obteniendo el valor del `OutputResult` método ‘s `generatedDoc` . Este método devuelve un `BLOB` objeto que contiene datos PostScript devueltos por el `generatePrintedOutput` método .


1. Envíe el flujo de impresión a una impresora de red.

   Envíe el flujo de impresión a una impresora de red invocando el `OutputClient` método `sendToPrinter` del objeto y pasando los valores siguientes:

   * Un `BLOB` objeto que representa el flujo de impresión que se va a enviar a la impresora.
   * Un valor `PrinterProtocol` de enumeración que especifica el protocolo de impresora que se va a utilizar. Por ejemplo, para especificar el protocolo SharedPrinter, pase `PrinterProtocol.SharedPrinter`.
   * Un `bool` valor que especifica si se va a usar el valor del parámetro anterior. Pase el valor `true`. (Este valor de parámetro solo es necesario para la invocación de servicio Web).
   * Un valor de cadena que especifica el nombre del servidor de impresión. Por ejemplo, suponiendo que el nombre del servidor de impresión sea PrintServer1, pase `\\\PrintSever1`.
   * Un valor de cadena que especifica el nombre de la impresora. Por ejemplo, suponiendo que el nombre de la impresora sea Impresora1, pase `\\\PrintSever1\Printer1`.
   >[!NOTE]
   >
   >El `sendToPrinter` método se agregó a la API de AEM Forms en la versión 8.2.1.

## Creación de varios archivos de salida {#creating-multiple-output-files}

El servicio Output puede crear documentos independientes para cada registro dentro de un origen de datos XML o un solo archivo que contenga todos los registros (esta funcionalidad es la predeterminada). Por ejemplo, supongamos que diez registros se encuentran en un origen de datos XML y que se indica al servicio Output que cree documentos PDF independientes (u otros tipos de salida) para cada registro mediante la API de servicio de salida. Como resultado, el servicio Output genera diez documentos PDF. (En lugar de crear documentos, puede enviar varios flujos de impresión a una impresora).

La siguiente ilustración también muestra el servicio Output procesando un archivo de datos XML que contiene varios registros. Sin embargo, supongamos que se indica al servicio Output que cree un único documento PDF que contenga todos los registros de datos. En este caso, el servicio Output genera un documento que contiene todos los registros.

La siguiente ilustración muestra el servicio Output procesando un archivo de datos XML que contiene varios registros. Supongamos que se indica al servicio Output que debe crear un documento PDF independiente para cada registro de datos. En este caso, el servicio Output genera un documento PDF independiente para cada registro de datos.

![cm_outputbatchmany](assets/cm_outputbatchmany.png)

Los siguientes datos XML muestran un ejemplo de un archivo de datos que contiene tres registros de datos.

```as3
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

Observe que el elemento XML que inicia y finaliza cada registro de datos es `LoanRecord`. La lógica de la aplicación que genera varios archivos hace referencia a este elemento XML.

>[!NOTE]
>
>Para obtener más información sobre el servicio Output, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-7}

Para crear varios archivos PDF basados en un origen de datos XML, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto Output Client.
1. Haga referencia a un origen de datos XML.
1. Configure las opciones de tiempo de ejecución de PDF.
1. Configure las opciones de procesamiento en tiempo de ejecución.
1. Genere varios archivos PDF.
1. Recupere los resultados de la operación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no es JBoss, deberá reemplazar los archivos adobe-utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms.

**Creación de un objeto Output Client**

Antes de realizar una operación de servicio Output mediante programación, debe crear un objeto cliente de servicio Output. Si utiliza la API de Java, cree un `OutputClient` objeto. Si está utilizando la API de servicio Web Output, cree un `OutputServiceService` objeto.

**Referencia a un origen de datos XML**

Haga referencia a un origen de datos XML que contiene varios registros. Se debe utilizar un elemento XML para separar los registros de datos. Por ejemplo, en el ejemplo del origen de datos XML que se muestra anteriormente en esta sección, se asigna un nombre al elemento XML que separa los registros de datos `LoanRecord`.

Debe existir un elemento XML para cada campo de formulario que desee rellenar con datos. El nombre del elemento XML debe coincidir con el nombre del campo. Un elemento XML se omite si no se corresponde con un campo de formulario o si el nombre del elemento XML no coincide con el nombre del campo. No es necesario coincidir con el orden en que se muestran los elementos XML si se especifican todos los elementos XML.

**Definir opciones de tiempo de ejecución de PDF**

Debe establecer las siguientes opciones de tiempo de ejecución para que el servicio Output cree correctamente varios archivos basados en un origen de datos XML:

* **Muchos archivos**: Especifica si el servicio Output crea un solo documento o varios documentos. Puede especificar true o false. Para crear un documento independiente para cada registro de datos en el origen de datos XML, especifique true.
* **URI** de archivo: Especifica la ubicación de los archivos que genera el servicio Output. Por ejemplo, supongamos que especifica C:\\Adobe\forms\Loan.pdf. En este caso, el servicio Output crea un archivo denominado Loan.pdf y lo coloca en el directorio C:\\Adobe\forms folder. Cuando hay varios archivos, los nombres son Loan0001.pdf, Loan0002.pdf, Loan0003.pdf y así sucesivamente. Si especifica una ubicación de archivo, los archivos se colocan en el servidor, no en el equipo cliente.
* **Nombre** del registro: Especifica el nombre del elemento XML en el origen de datos que separa los registros de datos. Por ejemplo, en el ejemplo del origen de datos XML que se muestra anteriormente en esta sección, se llama al elemento XML que separa los registros de datos `LoanRecord`. (En lugar de establecer la opción de tiempo de ejecución Nombre de registro, puede establecer el nivel de registro asignándole un valor numérico que indique el nivel de elemento que contiene registros de datos. Sin embargo, solo puede establecer el nombre del registro o el nivel de registro. No se pueden establecer ambos valores).

**Definición de opciones de tiempo de ejecución de procesamiento**

Puede definir las opciones de procesamiento en tiempo de ejecución al crear varios archivos. Aunque estas opciones no son necesarias (a diferencia de las opciones de tiempo de ejecución de salida, que son necesarias), puede realizar tareas como mejorar el rendimiento del servicio Output. Por ejemplo, puede almacenar en caché el diseño de formulario que utiliza el servicio Output para mejorar el rendimiento.

Cuando el servicio Output procesa los registros por lotes, lee los datos que contienen varios registros de forma incremental. Es decir, el servicio Output lee los datos en la memoria y los libera a medida que se procesa el lote de registros. El servicio Output carga los datos de forma incremental cuando se establece una de las dos opciones de tiempo de ejecución. Si establece la opción de tiempo de ejecución Nombre de registro, el servicio Output lee los datos de forma incremental. Del mismo modo, si establece la opción de tiempo de ejecución Nivel de registro en 2 o superior, el servicio Output lee los datos de forma incremental.

Puede controlar si el servicio Output realiza una carga incremental mediante el método `PDFOutputOptionsSpec` o el método del `PrintedOutputOptionSpec` objeto `setLazyLoading` . Puede pasar el valor `false` a este método, que desactiva la carga incremental.

**Generar varios archivos PDF**

Después de hacer referencia a un origen de datos XML válido que contiene varios registros de datos y definir las opciones en tiempo de ejecución, puede invocar el servicio Output, que hace que genere varios archivos. Al generar varios registros, el `OutputResult` método `getGeneratedDoc` del objeto devuelve `null`.

**Recuperar los resultados de la operación**

Una vez que el servicio Output realiza una operación, devuelve datos XML que especifican si la operación se realizó correctamente. El servicio Output devuelve el siguiente XML. En este caso, el servicio Output generó 42 documentos.

```as3
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

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de API de servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Creación de varios archivos PDF mediante la API de Java {#create-multiple-pdf-files-using-the-java-api}

Cree varios archivos PDF mediante la API de salida (Java):

1. Incluir archivos de proyecto&quot;

   Incluya archivos JAR de cliente, como adobe-output-client.jar, en la ruta de clases del proyecto Java. .

1. Creación de un objeto Output Client

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `OutputClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Referencia a un origen de datos XML

   * Cree un `java.io.FileInputStream` objeto que represente el origen de datos XML que contiene varios registros utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo XML.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Definir opciones de tiempo de ejecución de PDF

   * Cree un `PDFOutputOptionsSpec` objeto con su constructor.
   * Establezca la opción Muchos archivos invocando el `PDFOutputOptionsSpec` método `setGenerateManyFiles` del objeto. Por ejemplo, pase el valor `true` para indicar al servicio Output que cree un archivo PDF independiente para cada registro en el origen de datos XML. (Si pasa `false`, el servicio Output genera un único documento PDF que contiene todos los registros).
   * Establezca la opción URI de archivo invocando el `PDFOutputOptionsSpec` método `setFileUri` del objeto y pasando un valor de cadena que especifica la ubicación de los archivos que genera el servicio Output. La opción URI de archivo es relativa al servidor de aplicaciones J2EE que aloja AEM Forms, no al equipo cliente.
   * Defina la opción Nombre del registro invocando el `OutputOptionsSpec` método `setRecordName` del objeto y pasando un valor de cadena que especifica el nombre del elemento XML en el origen de datos que separa los registros de datos. (Por ejemplo, considere el origen de datos XML que se muestra anteriormente en esta sección. El nombre del elemento XML que separa los registros de datos es LoanRecord).

1. Definición de opciones de tiempo de ejecución de procesamiento

   * Cree un `RenderOptionsSpec` objeto con su constructor.
   * Almacene en caché el diseño de formulario para mejorar el rendimiento del servicio Output invocando el `RenderOptionsSpec` objeto `setCacheEnabled` y pasando un `Boolean` valor de `true`.

1. Generar varios archivos PDF

   Genere varios archivos PDF invocando el `OutputClient` método `generatePDFOutput` del objeto y pasando los siguientes valores:

   * Un valor `TransformationFormat` enum. Para generar un documento PDF, especifique `TransformationFormat.PDF`.
   * Un valor de cadena que especifica el nombre del diseño de formulario.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentra el diseño de formulario.
   * Un `PDFOutputOptionsSpec` objeto que contiene opciones de tiempo de ejecución de PDF.
   * Un `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * El `com.adobe.idp.Document` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario.
   El `generatePDFOutput` método devuelve un `OutputResult` objeto que contiene los resultados de la operación.

1. Recuperar los resultados de la operación

   * Cree un `java.io.File` objeto que represente un archivo XML que contendrá los resultados del `generatePDFOutput` método. Asegúrese de que la extensión del nombre de archivo sea .xml.
   * Invoque el `com.adobe.idp.Document` método del `copyToFile` objeto para copiar el contenido del `com.adobe.idp.Document` objeto en el archivo (asegúrese de utilizar el `com.adobe.idp.Document` objeto devuelto por el `applyUsageRights` método).

**Consulte también**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Inicio rápido (modo EJB): Creación de varios archivos PDF mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creación de varios archivos PDF mediante la API de servicio web {#create-multiple-pdf-files-using-the-web-service-api}

Cree varios archivos PDF mediante la API de salida (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto Output Client.

   * Cree un `OutputServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `OutputServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para usar MTOM.
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `OutputServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un origen de datos XML.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar datos de formulario que contienen varios registros.
   * Cree un `System.IO.FileStream` objeto invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo XML que contiene varios registros.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.

1. Configure las opciones de tiempo de ejecución de PDF.

   * Cree un `PDFOutputOptionsSpec` objeto con su constructor.
   * Defina la opción Muchos archivos asignando un valor booleano al miembro de datos del `OutputOptionsSpec` objeto `generateManyFiles` . Por ejemplo, asigne el valor `true` a este miembro de datos para indicar al servicio Output que cree un archivo PDF independiente para cada registro del origen de datos XML. (Si se asigna `false` a este miembro de datos, el servicio Output genera un único PDF que contiene todos los registros).
   * Defina la opción de URI de archivo asignando un valor de cadena que especifique la ubicación de los archivos que el servicio Output genera en el miembro de datos del `OutputOptionsSpec` objeto `fileURI` . La opción URI de archivo es relativa al servidor de aplicaciones J2EE que aloja AEM Forms, no al equipo cliente.
   * Defina la opción de nombre de registro asignando un valor de cadena que especifique el nombre del elemento XML en el origen de datos que separa los registros de datos del miembro de `OutputOptionsSpec` datos del `recordName` objeto.
   * Defina la opción de copias asignando un valor entero que especifique el número de copias que el servicio Output genera en el miembro de datos del `OutputOptionsSpec` objeto `copies` .

1. Configure las opciones de procesamiento en tiempo de ejecución.

   * Cree un `RenderOptionsSpec` objeto con su constructor.
   * Almacene en caché el diseño de formulario para mejorar el rendimiento del servicio Output asignando el valor `true` al miembro de datos del `RenderOptionsSpec` objeto `cacheEnabled` .

1. Genere varios archivos PDF.

   Cree varios archivos PDF invocando el `OutputServiceService` método del `generatePDFOutput`objeto y pasando los siguientes valores:

   * Un valor de enumeración TransformationFormat. Para generar un documento PDF, especifique `TransformationFormat.PDF`.
   * Un valor de cadena que especifica el nombre del diseño de formulario.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentra el diseño de formulario.
   * Un `PDFOutputOptionsSpec` objeto que contiene opciones de tiempo de ejecución de PDF.
   * Un `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * El `BLOB` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario.
   * Un `BLOB` objeto que se rellena con el `generatePDFOutput` método . El `generatePDFOutput` método rellena este objeto con metadatos generados que describen el documento.
   * Un `BLOB` objeto que se rellena con el `generatePDFOutput` método . El `generatePDFOutput` método rellena este objeto con datos de resultados.
   * Un `OutputResult` objeto que contiene los resultados de la operación.

1. Recuperar los resultados de la operación

   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa una ubicación de archivo XML que contiene datos de resultados. Asegúrese de que la extensión del nombre de archivo sea .xml.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto que se rellenó con los datos de resultado mediante el `OutputServiceService` método `generatePDFOutput` del objeto (el octavo parámetro). Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `binaryData` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en el archivo XML invocando el `System.IO.BinaryWriter` método del `Write` objeto y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Creación de reglas de búsqueda {#creating-search-rules}

Puede crear reglas de búsqueda que resulten en que el servicio Output examine los datos de entrada y utilice diferentes diseños de formulario basados en el contenido de datos para generar resultados. Por ejemplo, si la *hipoteca* de texto se encuentra dentro de los datos de entrada, el servicio Output puede utilizar un diseño de formulario denominado Mortgage.xdp. Del mismo modo, si el *automóvil* de texto se encuentra en los datos de entrada, el servicio Output puede utilizar un diseño de formulario guardado como AutomobileLoan.xdp. Aunque el servicio Output puede generar diferentes tipos de salida, en esta sección se asume que el servicio Output genera un archivo PDF. En el diagrama siguiente se muestra el servicio Output que genera un archivo PDF procesando un archivo de datos XML y utilizando uno de los muchos diseños de formulario.

Además, el servicio Output puede generar paquetes de documentos, en los que se proporcionan varios registros en el conjunto de datos y cada registro coincide con un diseño de formulario y un solo documento se genera con varios diseños de formulario.

![cs_outputbatchmanyformdesigns2](assets/cs_outputbatchmanyformdesigns2.png)

>[!NOTE]
>
>Para obtener más información sobre el servicio Output, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-8}

Para indicar al servicio Output que utilice reglas de búsqueda al generar un documento, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto Output Client.
1. Haga referencia a un origen de datos XML.
1. Defina las reglas de búsqueda.
1. Configure las opciones de tiempo de ejecución de PDF.
1. Configure las opciones de procesamiento en tiempo de ejecución.
1. Genere un documento PDF.
1. Recupere los resultados de la operación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no es JBoss, deberá reemplazar adobe-utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms.

**Creación de un objeto Output Client**

Antes de realizar una operación de servicio Output mediante programación, debe crear un objeto cliente de servicio Output.

**Referencia a un origen de datos XML**

Debe existir un elemento XML para cada campo de formulario que desee rellenar con datos. El nombre del elemento XML debe coincidir con el nombre del campo. Un elemento XML se omite si no se corresponde con un campo de formulario o si el nombre del elemento XML no coincide con el nombre del campo. No es necesario coincidir con el orden en que se muestran los elementos XML, siempre que se especifiquen todos los elementos XML.

**Definir reglas de búsqueda**

Para definir las reglas de búsqueda, debe definir uno o varios patrones de texto que los servicios Output buscan en los datos de entrada. Para cada patrón de texto que defina, debe especificar un diseño de formulario correspondiente que se utilizará si se encuentra el patrón de texto. Si se encuentra un patrón de texto, el servicio Output utiliza el diseño de formulario correspondiente para generar el resultado. Un ejemplo de un patrón de texto es la *hipoteca*.

>[!NOTE]
>
>Si no se encuentran patrones de texto, se utiliza el formulario predeterminado. Asegúrese de que todos los diseños de formulario que utiliza se encuentran en la raíz del contenido.

**Definir opciones de tiempo de ejecución de PDF**

Configure las siguientes opciones de tiempo de ejecución de PDF para que el servicio Output cree correctamente un documento PDF basado en varios diseños de formulario:

* **URI** de archivo: Especifica el nombre y la ubicación del archivo PDF que genera el servicio Output.
* **Reglas**: Especifica las reglas que ha definido.
* **LookAHead**: Especifica el número de bytes que se utilizarán desde el principio del archivo de datos de entrada para analizar los patrones de texto definidos. El valor predeterminado es 500 bytes.

**Definición de opciones de tiempo de ejecución de procesamiento**

Puede definir opciones de procesamiento en tiempo de ejecución al crear archivos PDF. Aunque estas opciones no son necesarias (a diferencia de las opciones de tiempo de ejecución de PDF), puede realizar tareas como mejorar el rendimiento del servicio Output. Por ejemplo, puede almacenar en caché el diseño de formulario que utiliza el servicio Output para mejorar el rendimiento.

**Generar un documento PDF**

Después de hacer referencia a un origen de datos XML válido y definir las opciones de tiempo de ejecución, puede invocar el servicio Output, lo que le permite generar un documento PDF. Si el servicio Output encuentra un patrón de texto especificado en los datos de entrada, utiliza el diseño de formulario correspondiente. Si no se utiliza un patrón de texto, el servicio Output utiliza el diseño de formulario predeterminado.

**Recuperar los resultados de la operación**

Una vez que el servicio Output realiza una operación, devuelve datos XML que especifican si la operación se realizó correctamente.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de API de servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Creación de reglas de búsqueda mediante la API de Java {#create-search-rules-using-the-java-api}

Cree reglas de búsqueda mediante la API de salida (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-output-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto Output Client.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `OutputClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un origen de datos XML.

   * Cree un `java.io.FileInputStream` objeto que represente el origen de datos XML que se utiliza para rellenar el documento PDF utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo XML.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Defina las reglas de búsqueda.

   * Cree un `Rule` objeto con su constructor.
   * Defina un patrón de texto invocando el `Rule` método `setPattern` del objeto y pasando un valor de cadena que especifica un patrón de texto.
   * Defina el diseño de formulario correspondiente invocando el `Rule` método del `setForm` objeto. Pase un valor de cadena que especifique el nombre del diseño de formulario.
   >[!NOTE]
   >
   >Para cada patrón de texto que desee definir, repita los tres subpasos anteriores.

   * Cree un `java.util.List` objeto mediante un `java.util.ArrayList` constructor.
   * Para cada `Rule` objeto que cree, invoque el `java.util.List` método del `add` objeto y pase el `Rule` objeto.


1. Configure las opciones de tiempo de ejecución de PDF.

   * Cree un `PDFOutputOptionsSpec` objeto con su constructor.
   * Especifique el nombre y la ubicación del archivo PDF que genera el servicio Output invocando el `PDFOutputOptionsSpec` método del `setFileURI` objeto. Pase un valor de cadena que especifique la ubicación del archivo PDF. La opción URI de archivo es relativa al servidor de aplicaciones J2EE que aloja AEM Forms, no al equipo cliente.
   * Defina las reglas definidas invocando el `PDFOutputOptionsSpec` método del `setRules` objeto. Pase el `java.util.List` objeto que contiene los `Rule` objetos.
   * Configure el número de bytes que se analizarán para los patrones de texto definidos mediante la invocación del `PDFOutputOptionsSpec` método `setLookAhead` del objeto. Pase un valor entero que represente los números de bytes.

1. Configure las opciones de procesamiento en tiempo de ejecución.

   * Cree un `RenderOptionsSpec` objeto con su constructor.
   * Almacene en caché el diseño de formulario para mejorar el rendimiento del servicio Output invocando el objeto `RenderOptionsSpec` y `setCacheEnabled` pasando `true`.

1. Genere un documento PDF.

   Genere un documento PDF basado en varios diseños de formulario invocando el `OutputClient` método `generatePDFOutput` del objeto y pasando los valores siguientes:

   * Un valor `TransformationFormat` de enumeración. Para generar un documento PDF, especifique `TransformationFormat.PDF`.
   * Un valor de cadena que especifica el nombre del diseño de formulario predeterminado. Es decir, el diseño de formulario que se utiliza si no se encuentra un patrón de texto.
   * Un valor de cadena que especifica la raíz del contenido en la que se ubican los diseños de formulario.
   * Un `PDFOutputOptionsSpec` objeto que contiene opciones de tiempo de ejecución de PDF.
   * Un `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * El `com.adobe.idp.Document` objeto que contiene los datos de formulario que el servicio Output busca para los patrones de texto definidos.
   El `generatePDFOutput` método devuelve un `OutputResult` objeto que contiene los resultados de la operación.

1. Recupere los resultados de la operación.

   * Cree un `com.adobe.idp.Document` objeto que represente el estado del `generatePDFOutput` método invocando el `OutputResult` método `getStatusDoc` del objeto.
   * Cree un `java.io.File` objeto que contenga los resultados de la operación. Asegúrese de que la extensión de archivo es .xml.
   * Invoque el `com.adobe.idp.Document` método del `copyToFile` objeto para copiar el contenido del `com.adobe.idp.Document` objeto en el archivo (asegúrese de utilizar el `com.adobe.idp.Document` objeto devuelto por el `getStatusDoc` método).

**Consulte también**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Inicio rápido (modo EJB): Creación de reglas de búsqueda mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[Inicio rápido (modo SOAP): Creación de reglas de búsqueda mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creación de reglas de búsqueda mediante la API de servicio Web {#create-search-rules-using-the-web-service-api}

Cree reglas de búsqueda mediante la API de salida (servicio Web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto Output Client.

   * Cree un `OutputServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `OutputServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para usar MTOM.
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `OutputServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un origen de datos XML.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar datos que se combinarán con el documento PDF.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF que desea codificar y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.

1. Defina las reglas de búsqueda.

   * Cree un `Rule` objeto con su constructor.
   * Defina un patrón de texto asignando un valor de cadena que especifique un patrón de texto al miembro de `Rule` datos del `pattern` objeto.
   * Defina el diseño de formulario correspondiente asignando un valor de cadena que especifique el diseño de formulario al miembro de `Rule` datos del `form` objeto.
   >[!NOTE]
   >
   >Para cada patrón de texto que desee definir, repita los tres subpasos anteriores.

   * Cree un `MyArrayOf_xsd_anyType` objeto que almacene las reglas.
   * Asigne cada `Rule` objeto a un elemento de la `MyArrayOf_xsd_anyType` matriz. Invocar el `MyArrayOf_xsd_anyType` método del `Add` objeto para cada `Rule` objeto.


1. Definir opciones de tiempo de ejecución de PDF

   * Cree un `PDFOutputOptionsSpec` objeto con su constructor.
   * Defina la opción de URI de archivo asignando un valor de cadena que especifique la ubicación del archivo PDF que el servicio Output genera para el miembro de `PDFOutputOptionsSpec` datos del `fileURI` objeto. La opción URI de archivo es relativa al servidor de aplicaciones J2EE que aloja AEM Forms, no al equipo cliente.
   * Defina la opción de copias asignando un valor entero que especifique el número de copias que el servicio Output genera en el miembro de datos del `PDFOutputOptionsSpec` objeto `copies` .
   * Defina las reglas que definió asignando el `MyArrayOf_xsd_anyType` objeto que almacena las reglas al miembro de `PDFOutputOptionsSpec` datos del `rules` objeto.
   * Configure el número de bytes que se analizarán para los patrones de texto definidos asignando un valor entero que represente los números de bytes que se analizarán en el método de datos del `PDFOutputOptionsSpec` objeto `lookAhead` .

1. Definición de opciones de tiempo de ejecución de procesamiento

   * Cree un `RenderOptionsSpec` objeto con su constructor.
   * Almacene en caché el diseño de formulario para mejorar el rendimiento del servicio Output asignando el valor `true` al miembro de datos del `RenderOptionsSpec` objeto `cacheEnabled` .
   >[!NOTE]
   >
   >Si el documento de entrada es un formulario de Acrobat, no se puede establecer la versión del documento PDF mediante el `RenderOptionsSpec` miembro del `pdfVersion` objeto. El documento PDF de salida conserva la versión PDF del formulario de Acrobat. Del mismo modo, no se puede establecer la opción PDF con etiquetas utilizando el `RenderOptionsSpec` método del `taggedPDF` objeto si el documento de entrada es un formulario de Acrobat.

   >[!NOTE]
   >
   >No se puede establecer la opción de PDF linealizado mediante el uso del `RenderOptionsSpec` miembro del `linearizedPDF` objeto si el documento PDF de entrada está certificado o firmado digitalmente. Para obtener más información, consulte Firma [digital de documentos](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)PDF.

1. Generar un documento PDF

   Cree un documento PDF invocando el `OutputServiceService` método del `generatePDFOutput`objeto y pasando los siguientes valores:

   * Un valor `TransformationFormat` de enumeración. Para generar un documento PDF, especifique `TransformationFormat.PDF`.
   * Un valor de cadena que especifica el nombre del diseño de formulario.
   * Un valor de cadena que especifica la raíz del contenido donde se encuentra el diseño de formulario.
   * Un `PDFOutputOptionsSpec` objeto que contiene opciones de tiempo de ejecución de PDF.
   * Un `RenderOptionsSpec` objeto que contiene opciones de procesamiento en tiempo de ejecución.
   * El `BLOB` objeto que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario.
   * Un `BLOB` objeto que se rellena con el `generatePDFOutput` método . El `generatePDFOutput` método rellena este objeto con metadatos generados que describen el documento. (Este valor de parámetro solo es necesario para la invocación de servicio Web).
   * Un `BLOB` objeto que se rellena con el `generatePDFOutput` método . El `generatePDFOutput` método rellena este objeto con datos de resultados. (Este valor de parámetro solo es necesario para la invocación de servicio Web).
   * Un `OutputResult` objeto que contiene los resultados de la operación. (Este valor de parámetro solo es necesario para la invocación de servicio Web).
   >[!NOTE]
   >
   >Al generar un documento PDF invocando el `generatePDFOutput` método, tenga en cuenta que no puede combinar datos con un formulario PDF XFA firmado, certificado o que contiene derechos de uso. Para obtener información sobre los derechos de uso, consulte [Aplicación de derechos de uso a documentos](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)PDF.

1. Recuperar los resultados de la operación

   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa una ubicación de archivo XML que contiene datos de resultados. Asegúrese de que la extensión de archivo es XML.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto que se rellenó con los datos de resultado mediante el `OutputServiceService` método `generatePDFOutput` del objeto (el octavo parámetro). Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en el archivo XML invocando el `System.IO.BinaryWriter` método del `Write` objeto y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Acoplamiento de documentos PDF {#flattening-pdf-documents}

Puede utilizar el servicio Output para transformar un documento PDF interactivo en un PDF no interactivo. Un documento PDF interactivo permite a los usuarios introducir o modificar datos que se encuentran en los campos del documento PDF. El proceso de transformar un documento PDF interactivo en un documento PDF no interactivo se denomina *acoplamiento*. Cuando se acopla un documento PDF, un usuario no puede modificar los datos de los campos del documento. Una razón para acoplar un documento PDF es asegurarse de que no se puedan modificar los datos.

Puede acoplar los siguientes tipos de documentos PDF:

* Documentos PDF XFA interactivos
* Acrobat Forms

El intento de acoplar un PDF que es un documento PDF no interactivo provoca una excepción.

>[!NOTE]
>
>Para obtener más información sobre el servicio Output, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-9}

Para acoplar un documento PDF interactivo a un documento PDF no interactivo, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto Output Client.
1. Recupere un documento PDF interactivo.
1. Transforme el documento PDF.
1. Guarde el documento PDF no interactivo como archivo PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no es JBoss, deberá reemplazar los archivos adobe-utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms. Para obtener información sobre la ubicación de todos los archivos JAR de AEM Forms, consulte [Inclusión de archivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)de biblioteca Java de AEM Forms.

**Creación de un objeto Output Client**

Antes de realizar una operación de servicio Output mediante programación, debe crear un objeto cliente de servicio Output. Si utiliza la API de Java, cree un `OutputClient` objeto. Si está utilizando la API de servicio Web Output, cree un `OutputServiceService` objeto.

**Recuperar un documento PDF interactivo**

Recupere un documento PDF interactivo que desee transformar en un documento PDF no interactivo. Intentar transformar un documento PDF no interactivo provoca una excepción.

**Transformar el documento PDF**

Después de recuperar un documento PDF interactivo, puede transformarlo en un documento PDF no interactivo. El servicio Output devuelve un documento PDF no interactivo.

**Guardar el documento PDF no interactivo como archivo PDF**

Puede guardar el documento PDF no interactivo como archivo PDF.

**Consulte también**

[Acoplar un documento PDF con la API de Java](creating-document-output-streams.md#flatten-a-pdf-document-using-the-java-api)

[Acoplar un documento PDF con la API de servicio Web](creating-document-output-streams.md#flatten-a-pdf-document-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de API de servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Acoplar un documento PDF con la API de Java {#flatten-a-pdf-document-using-the-java-api}

Acoplar un documento PDF interactivo a un documento PDF no interactivo mediante la API de salida (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-output-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto Output Client.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `OutputClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recupere un documento PDF interactivo.

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF interactivo que se va a transformar mediante su constructor y pasando un valor de cadena que especifique la ubicación del archivo PDF interactivo.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Transforme el documento PDF.

   Transforme el documento PDF interactivo a un documento PDF no interactivo invocando el `OutputServiceService` método del `transformPDF` objeto y pasando los valores siguientes:

   * El `com.adobe.idp.Document` objeto que contiene el documento PDF interactivo.
   * Un valor `TransformationFormat` enum. Para generar un documento PDF no interactivo, especifique `TransformationFormat.PDF`.
   * Un valor `PDFARevisionNumber` enum que especifica el número de revisión. Dado que este parámetro está diseñado para un documento PDF/A, puede especificar `null`.
   * Un valor de cadena que representa el número y el año de la enmienda, separados por dos puntos. Dado que este parámetro está diseñado para un documento PDF/A, puede especificar `null`.
   * Un valor `PDFAConformance` enum que representa el nivel de conformidad con PDF/A. Dado que este parámetro está diseñado para un documento PDF/A, puede especificar `null`.
   El `transformPDF` método devuelve un `com.adobe.idp.Document` objeto que contiene un documento PDF no interactivo.

1. Guarde el documento PDF no interactivo como archivo PDF.

   * Cree un `java.io.File` objeto y asegúrese de que la extensión del nombre de archivo sea .pdf.
   * Invoque el `Document` método del `copyToFile` objeto para copiar el contenido del `Document` objeto en el archivo (asegúrese de utilizar el `Document` objeto devuelto por el `transformPDF` método).

**Consulte también**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Inicio rápido (modo EJB): Transformación de un documento PDF mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[Inicio rápido (modo SOAP): Transformación de un documento PDF mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Acoplar un documento PDF con la API de servicio Web {#flatten-a-pdf-document-using-the-web-service-api}

Acoplar un documento PDF interactivo a un documento PDF no interactivo mediante la API de salida (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto Output Client.

   * Cree un `OutputServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `OutputServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para usar MTOM.
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `OutputServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere un documento PDF interactivo.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar el documento PDF interactivo.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF interactivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` propiedad con el contenido de la matriz de bytes.

1. Transforme el documento PDF.

   Transforme el documento PDF interactivo a un documento PDF no interactivo invocando el `OutputClient` método del `transformPDF` objeto y pasando los valores siguientes:

   * Un `BLOB` objeto que contiene el documento PDF interactivo.
   * Un valor `TransformationFormat` de enumeración. Para generar un documento PDF no interactivo, especifique `TransformationFormat.PDF`.
   * Un valor `PDFARevisionNumber` enum que especifica el número de revisión.
   * Un valor booleano que especifica si se utiliza el valor `PDFARevisionNumber` enum. Dado que este parámetro está diseñado para un documento PDF/A, puede especificar `false`.
   * Un valor de cadena que representa el número y el año de la enmienda, separados por dos puntos. Dado que este parámetro está diseñado para un documento PDF/A, puede especificar `null`.
   * Un valor `PDFAConformance` enum que representa el nivel de conformidad con PDF/A.
   * Valor booleano que especifica si se utiliza el valor `PDFAConformance` enum. Dado que este parámetro está diseñado para un documento PDF/A, puede especificar `false`.
   El `transformPDF` método devuelve un `BLOB` objeto que contiene un documento PDF no interactivo.

1. Guarde el documento PDF no interactivo como archivo PDF.

   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF no interactivo.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto devuelto por el `transformPDF` método. Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el `System.IO.BinaryWriter` método `Write` del objeto y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](creating-document-output-streams.md#summary-of-steps)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
