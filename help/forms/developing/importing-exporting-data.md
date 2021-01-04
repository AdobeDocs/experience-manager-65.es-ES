---
title: Importación y exportación de datos
seo-title: Importación y exportación de datos
description: Utilice el servicio de integración de datos de formulario para importar datos en un formulario PDF y exportar datos desde un formulario PDF mediante la API de Java y la API de servicio Web.
seo-description: Utilice el servicio de integración de datos de formulario para importar datos en un formulario PDF y exportar datos desde un formulario PDF mediante la API de Java y la API de servicio Web.
uuid: 94ccb6f2-6e5f-43ea-a954-9a4402871a17
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2e783745-c986-45ba-8e65-7437d114ca38
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '2796'
ht-degree: 0%

---


# Importación y exportación de datos {#importing-and-exporting-data}

## Acerca del servicio de integración de datos de formulario {#about-the-form-data-integration-service}

El servicio de integración de datos de formulario puede importar datos en un formulario PDF y exportar datos desde un formulario PDF. Las operaciones de importación y exportación admiten dos tipos de PDF forms:

* Un formulario Acrobat (creado en Acrobat) es un documento PDF que contiene campos de formulario.
* Un formulario XML de Adobe (creado en Designer) es un documento PDF que se ajusta a la Arquitectura Forms XML de Adobe XML (XFA).

Los datos del formulario pueden existir en uno de los siguientes formatos, según el tipo de formulario PDF:

* Un archivo XFDF, que es una versión XML del formato de datos de formulario de Acrobat.
* Un archivo XDP, que es un archivo XML que contiene definiciones de campo de formulario. También puede contener datos de campo de formulario y un archivo PDF incrustado. Un archivo XDP generado por Designer solo se puede utilizar si lleva un documento PDF incrustado con codificación base 64.

Puede realizar estas tareas mediante el servicio de integración de datos de formulario:

* Importar datos a PDF forms. Para obtener más información, consulte [Importación de datos de formulario](importing-exporting-data.md#importing-form-data).
* Exportar datos de PDF forms. Para obtener más información, consulte [Exportación de datos de formulario](importing-exporting-data.md#exporting-form-data).

>[!NOTE]
>
>Para obtener más información sobre el servicio de integración de datos de formulario, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importación de datos de formulario {#importing-form-data}

Puede importar datos de formulario en PDF forms interactivos mediante el servicio de integración de datos de formulario. Un formulario PDF interactivo es un documento PDF que contiene uno o varios campos para recopilar información de un usuario o para mostrar información personalizada. El servicio de integración de datos de formulario no admite cálculos, validación ni secuencias de comandos de formularios.

Para importar datos en un formulario creado en Designer, debe hacer referencia a un origen de datos XDP XML válido. Considere el siguiente ejemplo de formulario de solicitud de hipoteca.

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

Para importar valores de datos en este formulario, debe tener un origen de datos XDP XML válido que corresponda al formulario. No se puede utilizar un origen de datos XML arbitrario para importar datos en un formulario mediante el servicio de integración de datos de formulario. La diferencia entre un origen de datos XML arbitrario y un origen de datos XML XDP es que un origen de datos XDP se ajusta a la Arquitectura de Forms XML (XFA). El siguiente XML representa un origen de datos XML XDP que corresponde al formulario de solicitud de hipoteca de ejemplo.

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

>[!NOTE]
>
>Para obtener más información sobre el servicio de integración de datos de formulario, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente del servicio de integración de datos de formulario**

Para poder importar datos mediante programación en una API de cliente de formulario PDF, debe crear un cliente de servicio de integración de datos. Al crear un cliente de servicio, se define la configuración de conexión necesaria para invocar un servicio. Para obtener más información, consulte [Configuración de propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Hacer referencia a un formulario PDF**

Para importar datos a un formulario PDF, debe hacer referencia a un formulario XML creado en Designer o a un formulario Acrobat creado en Acrobat.

**Referencia a un origen de datos XML**

Para importar datos de formulario, debe hacer referencia a un origen de datos válido. Para importar datos en un formulario XML XFA creado en Designer, debe utilizar un origen de datos XML XDP. Si hace referencia a un formulario Acrobat, debe utilizar un origen de datos XFDF. Para cada campo en el que desee importar datos, debe especificarse un valor. Si un elemento ubicado en el origen de datos XML no se corresponde con un campo del formulario, se ignora el elemento.

**Importar datos en el formulario PDF**

Después de hacer referencia a un formulario PDF y a un origen de datos XML válido, puede importar los datos en el formulario PDF.

**Guardar el formulario PDF como archivo PDF**

Después de importar datos en un formulario, puede guardarlo como archivo PDF. Una vez guardado como archivo PDF, un usuario puede abrir el formulario en Adobe Reader o Acrobat y ver el formulario con los datos importados.

**Consulte también**

[Importación de datos de formulario mediante la API de Java](importing-exporting-data.md#import-form-data-using-the-java-api)

[Importación de datos de formulario mediante la API de servicio Web](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API del servicio de integración de datos de formulario](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Exportación de datos de formulario](importing-exporting-data.md#exporting-form-data)

### Importar datos de formulario mediante la API de Java {#import-form-data-using-the-java-api}

Importar datos de formulario mediante la API de integración de datos de formulario (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-formdataintegration-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente del servicio de integración de datos de formulario.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `FormDataIntegrationClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Haga referencia a un formulario PDF.

   * Cree un objeto `java.io.FileInputStream` utilizando su constructor. Pase un valor de cadena que especifique la ubicación del formulario PDF.
   * Cree un objeto `com.adobe.idp.Document` que almacene el formulario PDF mediante el constructor `com.adobe.idp.Document`. Pase el objeto `java.io.FileInputStream` que contiene el formulario PDF al constructor.

1. Haga referencia a un origen de datos XML.

   * Cree un objeto `java.io.FileInputStream` utilizando su constructor y pase un valor de cadena que especifique la ubicación del archivo XML que contiene los datos que se van a importar al formulario.
   * Cree un objeto `com.adobe.idp.Document` que almacene datos de formulario mediante el constructor `com.adobe.idp.Document`. Pase el objeto `java.io.FileInputStream` que contiene datos de formulario al constructor.

1. Importe datos en el formulario PDF.

   Importe datos en un formulario PDF invocando el método `FormDataIntegrationClient` del objeto `importData` y pasando los valores siguientes:

   * El objeto `com.adobe.idp.Document` que almacena el formulario PDF.
   * El objeto `com.adobe.idp.Document` que almacena datos de formulario.

   El método `importData` devuelve un objeto `com.adobe.idp.Document` que almacena un formulario PDF que contiene los datos ubicados en el origen de datos XML.

1. Guarde el formulario PDF como archivo PDF.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea &quot;.PDF&quot;.
   * Invoque el método `Document` del objeto `copyToFile` para copiar el contenido del objeto `Document` en el archivo (asegúrese de utilizar el objeto `Document` devuelto por el método `importData`).

**Consulte también**

[Resumen de los pasos](importing-exporting-data.md#summary-of-steps)

[Inicio rápido (modo SOAP): Importación de datos de formulario mediante la API de Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importar datos de formulario mediante la API de servicio Web {#import-form-data-using-the-web-service-api}

Importar datos de formulario mediante la API de integración de datos de formulario (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente del servicio de integración de datos de formulario.

   * Cree un objeto `FormDataIntegrationClient` utilizando su constructor predeterminado.
   * Cree un objeto `FormDataIntegrationClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`). No es necesario usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para utilizar MTOM.
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `FormDataIntegrationClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un formulario PDF.

   * Cree un objeto `BLOB` utilizando su constructor. Este objeto `BLOB` se utiliza para almacenar el formulario PDF.
   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que especifique la ubicación del formulario PDF y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read`. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Haga referencia a un origen de datos XML.

   * Cree un objeto `BLOB` utilizando su constructor. Este objeto `BLOB` se utiliza para almacenar los datos importados en el formulario.
   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que especifique la ubicación del archivo XML que contiene los datos que se van a importar y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read`. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Importe datos en el formulario PDF.

   Importe datos en el formulario PDF invocando el método `FormDataIntegrationClient` del objeto `importData` y pasando los valores siguientes:

   * El objeto `BLOB` que almacena el formulario PDF.
   * El objeto `BLOB` que almacena datos de formulario.

   El método `importData` devuelve un objeto `BLOB` que almacena un formulario PDF que contiene los datos ubicados en el origen de datos XML.

1. Guarde el formulario PDF como archivo PDF.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo PDF.
   * Cree una matriz de bytes que almacene el contenido de datos del objeto `BLOB` devuelto por el método `importData`. Rellene la matriz de bytes obteniendo el valor del campo `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](importing-exporting-data.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Exportación de datos de formulario {#exporting-form-data}

Puede exportar datos de formulario desde un formulario PDF interactivo mediante el servicio de integración de datos de formulario. El formato de los datos exportados depende del tipo de formulario. Si el tipo de formulario es un formulario Acrobat creado en Acrobat, los datos exportados son XFDF. Si el tipo de formulario es un formulario XML creado en Designer, los datos exportados son XDP.

>[!NOTE]
>
>Para obtener más información sobre el servicio de integración de datos de formulario, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Antes de poder importar datos mediante programación a una API formClient de PDF, debe crear un cliente de servicio de integración de datos. Al crear un cliente de servicio, se define la configuración de conexión necesaria para invocar un servicio. Para obtener más información, [Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Hacer referencia a un formulario PDF**

Para exportar datos desde un formulario PDF, debe hacer referencia a un formulario PDF creado en Designer o Acrobat y que contiene datos de formulario. Si intenta exportar datos desde un formulario PDF vacío, obtendrá un esquema XML vacío.

**Exportar datos desde el formulario PDF**

Después de hacer referencia a un formulario PDF que contiene datos de formulario, puede exportar los datos desde el formulario. Los datos se exportan dentro de un esquema XML basado en el formulario.

**Guardar los datos del formulario como un archivo XML**

Después de exportar los datos del formulario, puede guardarlos como un archivo XML. Una vez guardado como archivo XML, puede abrir el archivo XML en un visor XML para realizar una vista de los datos del formulario.

**Consulte también**

[Exportación de datos de formulario mediante la API de Java](importing-exporting-data.md#export-form-data-using-the-java-api)

[Exportación de datos de formulario mediante la API de servicio Web](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API del servicio de integración de datos de formulario](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Importación de datos de formulario](importing-exporting-data.md#importing-form-data)

### Exportar datos de formulario mediante la API de Java {#export-form-data-using-the-java-api}

Exportar datos de formulario mediante la API de integración de datos de formulario (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-formdataintegration-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente del servicio de integración de datos de formulario.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `FormDataIntegrationClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Haga referencia a un formulario PDF.

   * Cree un objeto `java.io.FileInputStream` utilizando su constructor y pase un valor de cadena que especifique la ubicación del formulario PDF que contiene datos para exportar.
   * Cree un objeto `com.adobe.idp.Document` que almacene el formulario PDF mediante el constructor `com.adobe.idp.Document`. Pase el objeto `java.io.FileInputStream` que contiene el formulario PDF al constructor.

1. Exporte datos desde el formulario PDF.

   Exporte datos de formulario invocando el método `FormDataIntegrationClient` del objeto `exportData` y pase el objeto `com.adobe.idp.Document` que almacena el formulario PDF. Este método devuelve un objeto `com.adobe.idp.Document` que almacena datos de formulario como un esquema XML.

1. Guarde el formulario PDF como archivo PDF.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo es XML.
   * Invoque el método `Document` del objeto `copyToFile` para copiar el contenido del objeto `Document` en el archivo (asegúrese de utilizar el objeto `Document` devuelto por el método `exportData`).

**Consulte también**

[Resumen de los pasos](importing-exporting-data.md#summary-of-steps)

[Inicio rápido (modo SOAP): Exportación de datos de formulario mediante la API de Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exportar datos de formulario mediante la API de servicio Web {#export-form-data-using-the-web-service-api}

Exportar datos de formulario mediante la API de integración de datos de formulario (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   * Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente del servicio de integración de datos de formulario.

   * Cree un objeto `FormDataIntegrationClient` utilizando su constructor predeterminado.
   * Cree un objeto `FormDataIntegrationClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`). No es necesario usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para utilizar MTOM.
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `FormDataIntegrationClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un formulario PDF.

   * Cree un objeto `BLOB` utilizando su constructor. Este objeto `BLOB` se utiliza para almacenar el formulario PDF desde el que se exportan los datos.
   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que especifique la ubicación del formulario PDF y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Exporte datos desde el formulario PDF.

   Importe datos en un formulario PDF invocando el método `FormDataIntegrationClient` del objeto `exportData` y pasando el objeto `BLOB` que almacena el formulario PDF. Este método devuelve un objeto `BLOB` que almacena datos de formulario como un esquema XML.

1. Guarde el formulario PDF como archivo PDF.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo XML.
   * Cree una matriz de bytes que almacene el contenido de datos del objeto `BLOB` devuelto por el método `exportData`. Rellene la matriz de bytes obteniendo el valor del campo `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo XML invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](importing-exporting-data.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
