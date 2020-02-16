---
title: Importación y exportación de datos
seo-title: Importación y exportación de datos
description: nulo
seo-description: nulo
uuid: 94ccb6f2-6e5f-43ea-a954-9a4402871a17
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2e783745-c986-45ba-8e65-7437d114ca38
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Importación y exportación de datos {#importing-and-exporting-data}

## Acerca del servicio de integración de datos de formulario {#about-the-form-data-integration-service}

El servicio de integración de datos de formulario puede importar datos en un formulario PDF y exportar datos desde un formulario PDF. Las operaciones de importación y exportación admiten dos tipos de formularios PDF:

* Un formulario de Acrobat (creado en Acrobat) es un documento PDF que contiene campos de formulario.
* Un formulario XML de Adobe (creado en Designer) es un documento PDF que se ajusta a la Arquitectura de formularios XML de Adobe XML (XFA).

Los datos del formulario pueden existir en uno de los siguientes formatos, según el tipo de formulario PDF:

* Un archivo XFDF, que es una versión XML del formato de datos de formulario de Acrobat.
* Un archivo XDP, que es un archivo XML que contiene definiciones de campo de formulario. También puede contener datos de campo de formulario y un archivo PDF incrustado. Un archivo XDP generado por Designer solo se puede utilizar si lleva un documento PDF incrustado con codificación base 64.

Puede realizar estas tareas mediante el servicio de integración de datos de formulario:

* Importar datos en formularios PDF. Para obtener más información, consulte [Importación de datos](importing-exporting-data.md#importing-form-data)de formulario.
* Exporte datos desde formularios PDF. Para obtener más información, consulte [Exportación de datos](importing-exporting-data.md#exporting-form-data)de formulario.

>[!NOTE]
>
>Para obtener más información sobre el servicio de integración de datos de formulario, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importación de datos de formulario {#importing-form-data}

Puede importar datos de formulario en formularios PDF interactivos mediante el servicio de integración de datos de formulario. Un formulario PDF interactivo es un documento PDF que contiene uno o varios campos para recopilar información de un usuario o para mostrar información personalizada. El servicio de integración de datos de formulario no admite cálculos, validación ni secuencias de comandos de formularios.

Para importar datos en un formulario creado en Designer, debe hacer referencia a un origen de datos XDP XML válido. Considere el siguiente ejemplo de formulario de solicitud de hipoteca.

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

Para importar valores de datos en este formulario, debe tener un origen de datos XDP XML válido que corresponda al formulario. No se puede utilizar un origen de datos XML arbitrario para importar datos en un formulario mediante el servicio de integración de datos de formulario. La diferencia entre un origen de datos XML arbitrario y un origen de datos XML XDP es que un origen de datos XDP se ajusta a la Arquitectura de formularios XML (XFA). El siguiente XML representa un origen de datos XML XDP que corresponde al formulario de solicitud de hipoteca de ejemplo.

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

>[!NOTE]
>
>Para obtener más información sobre el servicio de integración de datos de formulario, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para importar datos de formulario en un formulario PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente del servicio de integración de datos de formulario.
1. Haga referencia a un formulario PDF.
1. Haga referencia a un origen de datos XML.
1. Importe datos en el formulario PDF.
1. Guarde el formulario PDF como archivo PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)de biblioteca Java de AEM Forms.

**Crear un cliente del servicio de integración de datos de formulario**

Para poder importar datos mediante programación en una API de cliente de formulario PDF, debe crear un cliente de servicio de integración de datos. Al crear un cliente de servicio, se define la configuración de conexión necesaria para invocar un servicio. Para obtener más información, consulte [Configuración de propiedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexión.

**Hacer referencia a un formulario PDF**

Para importar datos a un formulario PDF, debe hacer referencia a un formulario XML creado en Designer o a un formulario de Acrobat creado en Acrobat.

**Referencia a un origen de datos XML**

Para importar datos de formulario, debe hacer referencia a un origen de datos válido. Para importar datos en un formulario XML XFA creado en Designer, debe utilizar un origen de datos XML XDP. Si hace referencia a un formulario de Acrobat, debe utilizar un origen de datos XFDF. Para cada campo en el que desee importar datos, debe especificarse un valor. Si un elemento ubicado en el origen de datos XML no se corresponde con un campo del formulario, se ignora el elemento.

**Importar datos en el formulario PDF**

Después de hacer referencia a un formulario PDF y a un origen de datos XML válido, puede importar los datos en el formulario PDF.

**Guardar el formulario PDF como archivo PDF**

Después de importar datos en un formulario, puede guardarlo como archivo PDF. Una vez guardado como archivo PDF, un usuario puede abrir el formulario en Adobe Reader o Acrobat y ver el formulario con los datos importados.

**Consulte también**

[Importación de datos de formulario mediante la API de Java](importing-exporting-data.md#import-form-data-using-the-java-api)

[Importación de datos de formulario mediante la API de servicio Web](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de integración de datos de formulario](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Exportación de datos de formulario](importing-exporting-data.md#exporting-form-data)

### Importación de datos de formulario mediante la API de Java {#import-form-data-using-the-java-api}

Importar datos de formulario mediante la API de integración de datos de formulario (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-formdataintegration-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente del servicio de integración de datos de formulario.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `FormDataIntegrationClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un formulario PDF.

   * Cree un `java.io.FileInputStream` objeto con su constructor. Pase un valor de cadena que especifique la ubicación del formulario PDF.
   * Cree un `com.adobe.idp.Document` objeto que almacene el formulario PDF mediante el `com.adobe.idp.Document` constructor. Pase el `java.io.FileInputStream` objeto que contiene el formulario PDF al constructor.

1. Haga referencia a un origen de datos XML.

   * Cree un `java.io.FileInputStream` objeto con su constructor y pase un valor de cadena que especifique la ubicación del archivo XML que contiene los datos que se van a importar al formulario.
   * Cree un `com.adobe.idp.Document` objeto que almacene datos de formulario mediante el `com.adobe.idp.Document` constructor. Pase el `java.io.FileInputStream` objeto que contiene datos de formulario al constructor.

1. Importe datos en el formulario PDF.

   Importe datos en un formulario PDF invocando el `FormDataIntegrationClient` método `importData` del objeto y pasando los valores siguientes:

   * El `com.adobe.idp.Document` objeto que almacena el formulario PDF.
   * El `com.adobe.idp.Document` objeto que almacena datos de formulario.
   El `importData` método devuelve un `com.adobe.idp.Document` objeto que almacena un formulario PDF que contiene los datos ubicados en el origen de datos XML.

1. Guarde el formulario PDF como archivo PDF.

   * Cree un `java.io.File` objeto y asegúrese de que la extensión del archivo sea &quot;.PDF&quot;.
   * Invoque el `Document` método del `copyToFile` objeto para copiar el contenido del `Document` objeto en el archivo (asegúrese de utilizar el `Document` objeto devuelto por el `importData` método).

**Consulte también**

[Resumen de los pasos](importing-exporting-data.md#summary-of-steps)

[Inicio rápido (modo SOAP): Importación de datos de formulario mediante la API de Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importación de datos de formulario mediante la API de servicio Web {#import-form-data-using-the-web-service-api}

Importar datos de formulario mediante la API de integración de datos de formulario (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente del servicio de integración de datos de formulario.

   * Cree un `FormDataIntegrationClient` objeto utilizando su constructor predeterminado.
   * Cree un `FormDataIntegrationClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para usar MTOM.
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `FormDataIntegrationClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un formulario PDF.

   * Cree un `BLOB` objeto con su constructor. Este `BLOB` objeto se utiliza para almacenar el formulario PDF.
   * Cree un `System.IO.FileStream` objeto invocando su constructor. Pase un valor de cadena que especifique la ubicación del formulario PDF y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.

1. Haga referencia a un origen de datos XML.

   * Cree un `BLOB` objeto con su constructor. Este `BLOB` objeto se utiliza para almacenar los datos importados en el formulario.
   * Cree un `System.IO.FileStream` objeto invocando su constructor. Pase un valor de cadena que especifique la ubicación del archivo XML que contiene los datos que se van a importar y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.

1. Importe datos en el formulario PDF.

   Importe datos en el formulario PDF invocando el `FormDataIntegrationClient` método del `importData` objeto y pasando los valores siguientes:

   * El `BLOB` objeto que almacena el formulario PDF.
   * El `BLOB` objeto que almacena datos de formulario.
   El `importData` método devuelve un `BLOB` objeto que almacena un formulario PDF que contiene los datos ubicados en el origen de datos XML.

1. Guarde el formulario PDF como archivo PDF.

   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo PDF.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto devuelto por el `importData` método. Rellene la matriz de bytes obteniendo el valor del `BLOB` campo del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el `System.IO.BinaryWriter` método `Write` del objeto y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](importing-exporting-data.md#summary-of-steps)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Exportación de datos de formulario {#exporting-form-data}

Puede exportar datos de formulario desde un formulario PDF interactivo mediante el servicio de integración de datos de formulario. El formato de los datos exportados depende del tipo de formulario. Si el tipo de formulario es un formulario de Acrobat creado en Acrobat, los datos exportados son XFDF. Si el tipo de formulario es un formulario XML creado en Designer, los datos exportados son XDP.

>[!NOTE]
>
>Para obtener más información sobre el servicio de integración de datos de formulario, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para exportar datos de formulario desde un formulario PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto
1. Cree un cliente del servicio de integración de datos de formulario.
1. Haga referencia a un formulario PDF.
1. Exporte datos desde el formulario PDF.
1. Guarde los datos exportados como un archivo XML.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

**Crear un cliente del servicio de integración de datos de formulario**

Antes de poder importar datos mediante programación a una API formClient de PDF, debe crear un cliente de servicio de integración de datos. Al crear un cliente de servicio, se define la configuración de conexión necesaria para invocar un servicio. Para obtener más información, [Configuración de las propiedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexión.

**Hacer referencia a un formulario PDF**

Para exportar datos desde un formulario PDF, debe hacer referencia a un formulario PDF creado en Designer o Acrobat y que contiene datos de formulario. Si intenta exportar datos desde un formulario PDF vacío, obtendrá un esquema XML vacío.

**Exportar datos desde el formulario PDF**

Después de hacer referencia a un formulario PDF que contiene datos de formulario, puede exportar los datos desde el formulario. Los datos se exportan dentro de un esquema XML basado en el formulario.

**Guardar los datos del formulario como un archivo XML**

Después de exportar los datos del formulario, puede guardarlos como un archivo XML. Una vez guardado como archivo XML, puede abrir el archivo XML en un visor XML para ver los datos del formulario.

**Consulte también**

[Exportación de datos de formulario mediante la API de Java](importing-exporting-data.md#export-form-data-using-the-java-api)

[Exportación de datos de formulario mediante la API de servicio Web](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de integración de datos de formulario](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Importación de datos de formulario](importing-exporting-data.md#importing-form-data)

### Exportación de datos de formulario mediante la API de Java {#export-form-data-using-the-java-api}

Exportar datos de formulario mediante la API de integración de datos de formulario (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-formdataintegration-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente del servicio de integración de datos de formulario.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `FormDataIntegrationClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un formulario PDF.

   * Cree un `java.io.FileInputStream` objeto con su constructor y pase un valor de cadena que especifique la ubicación del formulario PDF que contiene los datos que se van a exportar.
   * Cree un `com.adobe.idp.Document` objeto que almacene el formulario PDF mediante el `com.adobe.idp.Document` constructor. Pase el `java.io.FileInputStream` objeto que contiene el formulario PDF al constructor.

1. Exporte datos desde el formulario PDF.

   Exporte datos de formulario invocando el `FormDataIntegrationClient` método `exportData` del objeto y pasando el `com.adobe.idp.Document` objeto que almacena el formulario PDF. Este método devuelve un `com.adobe.idp.Document` objeto que almacena datos de formulario como un esquema XML.

1. Guarde el formulario PDF como archivo PDF.

   * Cree un `java.io.File` objeto y asegúrese de que la extensión del archivo es XML.
   * Invoque el `Document` método del `copyToFile` objeto para copiar el contenido del `Document` objeto en el archivo (asegúrese de utilizar el `Document` objeto devuelto por el `exportData` método).

**Consulte también**

[Resumen de los pasos](importing-exporting-data.md#summary-of-steps)

[Inicio rápido (modo SOAP): Exportación de datos de formulario mediante la API de Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exportación de datos de formulario mediante la API de servicio Web {#export-form-data-using-the-web-service-api}

Exportar datos de formulario mediante la API de integración de datos de formulario (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   * Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente del servicio de integración de datos de formulario.

   * Cree un `FormDataIntegrationClient` objeto utilizando su constructor predeterminado.
   * Cree un `FormDataIntegrationClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para usar MTOM.
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `FormDataIntegrationClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un formulario PDF.

   * Cree un `BLOB` objeto con su constructor. Este `BLOB` objeto se utiliza para almacenar el formulario PDF desde el que se exportan los datos.
   * Cree un `System.IO.FileStream` objeto invocando su constructor. Pase un valor de cadena que especifique la ubicación del formulario PDF y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.

1. Exporte datos desde el formulario PDF.

   Importe datos en un formulario PDF invocando el `FormDataIntegrationClient` método del `exportData` objeto y pasando el `BLOB` objeto que almacena el formulario PDF. Este método devuelve un `BLOB` objeto que almacena datos de formulario como un esquema XML.

1. Guarde el formulario PDF como archivo PDF.

   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo XML.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto devuelto por el `exportData` método. Rellene la matriz de bytes obteniendo el valor del `BLOB` campo del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo XML invocando el `System.IO.BinaryWriter` método del `Write` objeto y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](importing-exporting-data.md#summary-of-steps)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
