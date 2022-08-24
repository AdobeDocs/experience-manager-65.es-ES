---
title: Importación y exportación de datos
seo-title: Importing and Exporting Data
description: Utilice el servicio de integración de datos de formulario para importar datos en un formulario de PDF y exportar datos desde un formulario de PDF mediante la API de Java y la API del servicio web.
seo-description: Use the Form Data Integration service to import data into a PDF form and export data from a PDF form using the Java API and Web Service API.
uuid: 94ccb6f2-6e5f-43ea-a954-9a4402871a17
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2e783745-c986-45ba-8e65-7437d114ca38
role: Developer
exl-id: 96310e0a-8e95-4a55-9508-5298b8d67f83
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2778'
ht-degree: 0%

---

# Importación y exportación de datos {#importing-and-exporting-data}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

## Acerca del servicio de integración de datos de formulario {#about-the-form-data-integration-service}

El servicio de integración de datos de formulario puede importar datos en un formulario de PDF y exportar datos desde un formulario de PDF. Las operaciones de importación y exportación admiten dos tipos de PDF forms:

* Un formulario de Acrobat (creado en Acrobat) es un documento de PDF que contiene campos de formulario.
* Un formulario XML de Adobe (creado en Designer) es un documento de PDF que se ajusta a la arquitectura XML de Forms de Adobe XML (XFA).

Los datos del formulario pueden existir en uno de los siguientes formatos, según el tipo de formulario del PDF:

* Un archivo XFDF, que es una versión XML del formato de datos del formulario Acrobat.
* Un archivo XDP, que es un archivo XML que contiene definiciones de campos de formulario. También puede contener datos de campo de formulario y un archivo PDF incrustado. Un archivo XDP generado por Designer solo se puede utilizar si contiene un documento PDF incrustado codificado en base-64.

Puede realizar estas tareas mediante el servicio de integración de datos de formulario:

* Importar datos en PDF forms. Para obtener más información, consulte [Importación de datos de formulario](importing-exporting-data.md#importing-form-data).
* Exportar datos de PDF forms. Para obtener más información, consulte [Exportación de datos de formulario](importing-exporting-data.md#exporting-form-data).

>[!NOTE]
>
>Para obtener más información sobre el servicio de integración de datos de formulario, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importación de datos de formulario {#importing-form-data}

Puede importar datos de formulario en PDF forms interactivos mediante el servicio de integración de datos de formulario. Un formulario de PDF interactivo es un documento de PDF que contiene uno o más campos para recopilar información de un usuario o para mostrar información personalizada. El servicio de integración de datos de formulario no admite cálculos de formularios, validación ni secuencias de comandos.

Para importar datos en un formulario creado en Designer, debe hacer referencia a un origen de datos XML XDP válido. Consideremos el siguiente ejemplo de formulario de solicitud hipotecaria.

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

Para importar valores de datos en este formulario, debe tener un origen de datos XML XDP válido que corresponda al formulario. No se puede utilizar un origen de datos XML arbitrario para importar datos en un formulario mediante el servicio de integración de datos de formulario. La diferencia entre un origen de datos XML arbitrario y un origen de datos XML XDP es que un origen de datos XDP se ajusta a la Arquitectura Forms XML (XFA). El siguiente XML representa un origen de datos XML XDP que corresponde al formulario de aplicación hipotecaria de ejemplo.

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

Para importar datos de formulario en un formulario de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de integración de datos de formulario.
1. Haga referencia a un formulario de PDF.
1. Haga referencia a un origen de datos XML.
1. Importe datos en el formulario de PDF.
1. Guarde el formulario de PDF como archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creación de un cliente de servicio de integración de datos de formulario**

Para poder importar datos mediante programación a una API de cliente de formulario de PDF, debe crear un cliente de servicio de integración de datos. Al crear un cliente de servicio, define la configuración de conexión necesaria para invocar un servicio. Para obtener más información, consulte [Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Referencia a un formulario de PDF**

Para importar datos en un formulario de PDF, debe hacer referencia a un formulario XML creado en Designer o a un formulario de Acrobat creado en Acrobat.

**Referencia a un origen de datos XML**

Para importar datos de formulario, debe hacer referencia a un origen de datos válido. Para importar datos en un formulario XML XFA creado en Designer, debe utilizar un origen de datos XML XDP. Si hace referencia a un formulario de Acrobat, debe utilizar un origen de datos XFDF. Para cada campo en el que desee importar datos, se debe especificar un valor. Si un elemento ubicado en el origen de datos XML no se corresponde con un campo del formulario, se ignora el elemento.

**Importar datos en el formulario de PDF**

Después de hacer referencia a un formulario de PDF y a un origen de datos XML válido, puede importar los datos en el formulario de PDF.

**Guarde el formulario de PDF como archivo de PDF**

Después de importar los datos en un formulario, puede guardarlo como archivo PDF. Una vez guardado como archivo PDF, un usuario puede abrir el formulario en Adobe Reader o Acrobat y ver el formulario con los datos importados.

**Consulte también lo siguiente**

[Importar datos de formulario mediante la API de Java](importing-exporting-data.md#import-form-data-using-the-java-api)

[Importación de datos de formulario mediante la API de servicio web](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de integración de datos de formulario](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Exportación de datos de formulario](importing-exporting-data.md#exporting-form-data)

### Importar datos de formulario mediante la API de Java {#import-form-data-using-the-java-api}

Importe datos de formulario mediante la API de integración de datos de formulario (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-formdataintegration-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente de servicio de integración de datos de formulario.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `FormDataIntegrationClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un formulario de PDF.

   * Cree un `java.io.FileInputStream` usando su constructor. Pase un valor de cadena que especifique la ubicación del formulario de PDF.
   * Cree un `com.adobe.idp.Document` objeto que almacena el formulario de PDF utilizando la variable `com.adobe.idp.Document` constructor. Pase el `java.io.FileInputStream` objeto que contiene el formulario de PDF al constructor.

1. Haga referencia a un origen de datos XML.

   * Cree un `java.io.FileInputStream` mediante su constructor y pase un valor de cadena que especifique la ubicación del archivo XML que contiene los datos que se van a importar al formulario.
   * Cree un `com.adobe.idp.Document` objeto que almacena datos de formulario mediante la variable `com.adobe.idp.Document` constructor. Pase el `java.io.FileInputStream` objeto que contiene datos de formulario al constructor.

1. Importe datos en el formulario de PDF.

   Importe datos en el formulario del PDF invocando la variable `FormDataIntegrationClient` del objeto `importData` y pasando los siguientes valores:

   * La variable `com.adobe.idp.Document` objeto que almacena el formulario de PDF.
   * La variable `com.adobe.idp.Document` objeto que almacena datos de formulario.

   La variable `importData` el método devuelve un `com.adobe.idp.Document` objeto que almacena un formulario de PDF que contiene los datos ubicados en el origen de datos XML.

1. Guarde el formulario de PDF como archivo de PDF.

   * Cree un `java.io.File` y asegúrese de que la extensión de archivo es &quot;.PDF&quot;.
   * Invocar el `Document` del objeto `copyToFile` para copiar el contenido del `Document` al archivo (asegúrese de usar la variable `Document` objeto devuelto por el `importData` método).

**Consulte también lo siguiente**

[Resumen de los pasos](importing-exporting-data.md#summary-of-steps)

[Inicio rápido (modo SOAP): Importación de datos de formulario mediante la API de Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importación de datos de formulario mediante la API de servicio web {#import-form-data-using-the-web-service-api}

Importe datos de formulario mediante la API de integración de datos de formulario (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de servicio de integración de datos de formulario.

   * Cree un `FormDataIntegrationClient` usando su constructor predeterminado.
   * Cree un `FormDataIntegrationClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`.) No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para usar MTOM.
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `FormDataIntegrationClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un formulario de PDF.

   * Cree un `BLOB` usando su constructor. Esta `BLOB` se utiliza para almacenar el formulario de PDF.
   * Cree un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que especifique la ubicación del formulario del PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` método. Pase la matriz de bytes, la posición de inicio y la longitud del flujo para leerlos.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Haga referencia a un origen de datos XML.

   * Cree un `BLOB` usando su constructor. Esta `BLOB` se utiliza para almacenar los datos importados en el formulario.
   * Cree un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que especifique la ubicación del archivo XML que contiene los datos que se van a importar y el modo en que se va a abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` método. Pase la matriz de bytes, la posición de inicio y la longitud del flujo para leerlos.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Importe datos en el formulario de PDF.

   Importe datos en el formulario del PDF invocando la variable `FormDataIntegrationClient` del objeto `importData` y pasando los siguientes valores:

   * La variable `BLOB` objeto que almacena el formulario de PDF.
   * La variable `BLOB` objeto que almacena datos de formulario.

   La variable `importData` el método devuelve un `BLOB` objeto que almacena un formulario de PDF que contiene los datos ubicados en el origen de datos XML.

1. Guarde el formulario de PDF como archivo de PDF.

   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo PDF.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto devuelto por el `importData` método. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` campo .
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Resumen de los pasos](importing-exporting-data.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Exportación de datos de formulario {#exporting-form-data}

Puede exportar datos de formulario desde un formulario de PDF interactivo utilizando el servicio de integración de datos de formulario. El formato de los datos exportados depende del tipo de formulario. Si el tipo de formulario es un formulario de Acrobat creado en Acrobat, los datos exportados son XFDF. Si el tipo de formulario es un formulario XML creado en Designer, los datos exportados son XDP.

>[!NOTE]
>
>Para obtener más información sobre el servicio de integración de datos de formulario, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para exportar datos de formulario desde un formulario de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto
1. Cree un cliente de servicio de integración de datos de formulario.
1. Haga referencia a un formulario de PDF.
1. Exporte datos desde el formulario de PDF.
1. Guarde los datos exportados como un archivo XML.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

**Creación de un cliente de servicio de integración de datos de formulario**

Antes de poder importar datos mediante programación a una API formClient de PDF, debe crear un cliente de servicio de integración de datos. Al crear un cliente de servicio, define la configuración de conexión necesaria para invocar un servicio. Para obtener información, [Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Referencia a un formulario de PDF**

Para exportar datos desde un formulario de PDF, debe hacer referencia al formulario de PDF creado en Designer o Acrobat y que contiene datos de formulario. Si intenta exportar datos desde un formulario de PDF vacío, obtendrá un esquema XML vacío.

**Exportación de datos desde el formulario de PDF**

Después de hacer referencia a un formulario de PDF que contiene datos de formulario, puede exportar los datos desde el formulario. Los datos se exportan dentro de un esquema XML basado en el formulario.

**Guardar los datos del formulario como un archivo XML**

Después de exportar los datos del formulario, puede guardarlos como un archivo XML. Una vez guardado como archivo XML, puede abrir el archivo XML en un visor XML para ver los datos del formulario.

**Consulte también lo siguiente**

[Exportación de datos de formulario mediante la API de Java](importing-exporting-data.md#export-form-data-using-the-java-api)

[Exportar datos de formulario mediante la API de servicio web](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de integración de datos de formulario](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Importación de datos de formulario](importing-exporting-data.md#importing-form-data)

### Exportación de datos de formulario mediante la API de Java {#export-form-data-using-the-java-api}

Exporte datos de formulario mediante la API de integración de datos de formulario (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-formdataintegration-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente de servicio de integración de datos de formulario.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `FormDataIntegrationClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un formulario de PDF.

   * Cree un `java.io.FileInputStream` mediante su constructor y pase un valor de cadena que especifique la ubicación del formulario de PDF que contiene los datos que se van a exportar.
   * Cree un `com.adobe.idp.Document` objeto que almacena el formulario de PDF utilizando la variable `com.adobe.idp.Document` constructor. Pase el `java.io.FileInputStream` objeto que contiene el formulario de PDF al constructor.

1. Exporte datos desde el formulario de PDF.

   Exportar datos de formulario invocando la variable `FormDataIntegrationClient` del objeto `exportData` y pase el `com.adobe.idp.Document` objeto que almacena el formulario de PDF. Este método devuelve un `com.adobe.idp.Document` objeto que almacena datos de formulario como esquema XML.

1. Guarde el formulario de PDF como archivo de PDF.

   * Cree un `java.io.File` y asegúrese de que la extensión de archivo es XML.
   * Invocar el `Document` del objeto `copyToFile` para copiar el contenido del `Document` al archivo (asegúrese de usar la variable `Document` objeto devuelto por el `exportData` método).

**Consulte también lo siguiente**

[Resumen de los pasos](importing-exporting-data.md#summary-of-steps)

[Inicio rápido (modo SOAP): Exportación de datos de formulario mediante la API de Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exportar datos de formulario mediante la API de servicio web {#export-form-data-using-the-web-service-api}

Exporte datos de formulario mediante la API de integración de datos de formulario (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   * Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de servicio de integración de datos de formulario.

   * Cree un `FormDataIntegrationClient` usando su constructor predeterminado.
   * Cree un `FormDataIntegrationClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`.) No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para usar MTOM.
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `FormDataIntegrationClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un formulario de PDF.

   * Cree un `BLOB` usando su constructor. Esta `BLOB` se utiliza para almacenar el formulario de PDF desde el que se exportan los datos.
   * Cree un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que especifique la ubicación del formulario del PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Exporte datos desde el formulario de PDF.

   Importe datos en el formulario del PDF invocando la variable `FormDataIntegrationClient` del objeto `exportData` y pase el `BLOB` objeto que almacena el formulario de PDF. Este método devuelve un `BLOB` objeto que almacena datos de formulario como esquema XML.

1. Guarde el formulario de PDF como archivo de PDF.

   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo XML.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto devuelto por el `exportData` método. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` campo .
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo XML invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también lo siguiente**

[Resumen de los pasos](importing-exporting-data.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
