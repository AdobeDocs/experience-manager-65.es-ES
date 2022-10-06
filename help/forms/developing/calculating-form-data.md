---
title: Cálculo de datos de formulario
seo-title: Calculating Form Data
description: Utilice el servicio Forms para calcular los valores que introduce un usuario en un formulario y mostrar los resultados. El servicio Forms calcula los valores mediante la API de Java y la API de servicio web.
seo-description: Use the Forms service to calculate values that a user enters into a form and display the results. Forms service calculates the values using the Java API and Web Service API.
uuid: ccd85bc7-8ccc-44d9-9424-dfc1f603e688
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: b4f57e42-60a6-407d-9764-15a11615827d
role: Developer
exl-id: 28abf044-6c8e-4578-ae2e-54cdbd694c5f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1882'
ht-degree: 0%

---

# Cálculo de datos de formulario {#calculating-form-data}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

El servicio Forms puede calcular los valores que introduce un usuario en un formulario y mostrar los resultados. Para calcular los datos de formulario, debe realizar dos tareas. En primer lugar, se crea una secuencia de comandos de diseño de formulario que calcula los datos del formulario. Un diseño de formulario admite tres tipos de secuencias de comandos. Se ejecuta un tipo de script en el cliente, otro en el servidor y el tercer tipo se ejecuta tanto en el servidor como en el cliente. El tipo de script analizado en este tema se ejecuta en el servidor. Los cálculos del lado del servidor son compatibles con transformaciones de HTML, PDF y Guía de formulario (obsoletos).

Como parte del proceso de diseño de formularios, puede utilizar cálculos y secuencias de comandos para proporcionar una experiencia de usuario más rica. Los cálculos y las secuencias de comandos se pueden agregar a la mayoría de los objetos y campos de formulario. Debe crear una secuencia de comandos de diseño de formulario para realizar operaciones de cálculo en los datos que introduce un usuario en un formulario interactivo.

El usuario introduce valores en el formulario y hace clic en el botón Calcular para ver los resultados. El siguiente proceso describe una aplicación de ejemplo que permite al usuario calcular datos:

* El usuario accede a una página HTML denominada StartLoan.html que actúa como página de inicio de la aplicación web. Esta página invoca un servlet Java llamado `GetLoanForm`.
* La variable `GetLoanForm` servlet procesa un formulario de préstamo. Este formulario contiene una secuencia de comandos, campos interactivos, un botón de cálculo y un botón de envío.
* El usuario introduce valores en los campos del formulario y hace clic en el botón Calcular . El formulario se envía al `CalculateData` Servlet Java donde se ejecuta la secuencia de comandos. El formulario se devuelve al usuario con los resultados de cálculo mostrados en el formulario.
* El usuario continúa introduciendo y calculando valores hasta que se muestra un resultado satisfactorio. Cuando esté satisfecho, el usuario hace clic en el botón Enviar para procesar el formulario. El formulario se envía a otro servlet Java llamado `ProcessForm` que es responsable de recuperar los datos enviados. (Consulte [Gestión de Forms enviado](/help/forms/developing/rendering-forms.md#handling-submitted-forms).)


El diagrama siguiente muestra el flujo lógico de la aplicación.

![cf_cf_finsrv_loancalcapp_v1](assets/cf_cf_finsrv_loancalcapp_v1.png)

En la tabla siguiente se describen los pasos de este diagrama.

<table>
 <thead>
  <tr>
   <th><p>Etapa</p></th>
   <th><p>Descripción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>La variable <code>GetLoanForm</code> El servlet Java se invoca desde la página de inicio del HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>La variable <code>GetLoanForm</code> Java Servlet utiliza la API de cliente de servicio de Forms para procesar el formulario de préstamo en el explorador web del cliente. La diferencia entre procesar un formulario que contiene una secuencia de comandos configurada para ejecutarse en el servidor y procesar un formulario que no contiene una secuencia de comandos es que debe especificar la ubicación de destino utilizada para ejecutar la secuencia de comandos. Si no se especifica una ubicación de destino, no se ejecuta una secuencia de comandos configurada para ejecutarse en el servidor. Por ejemplo, considere la aplicación introducida en esta sección. La variable <code>CalculateData</code> El Servlet Java es la ubicación de destino en la que se ejecuta el script.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>El usuario introduce datos en campos interactivos y hace clic en el botón Calcular . El formulario se envía al <code>CalculateData</code> Servlet Java, donde se ejecuta la secuencia de comandos. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>El formulario se vuelve a procesar en el explorador web con los resultados de cálculo mostrados en el formulario. </p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>El usuario hace clic en el botón Enviar cuando los valores sean satisfactorios. El formulario se envía a otro servlet Java llamado <code>ProcessForm</code>.</p></td>
  </tr>
 </tbody>
</table>

Normalmente, un formulario enviado como contenido de PDF contiene secuencias de comandos que se ejecutan en el cliente. Sin embargo, también se pueden ejecutar cálculos del lado del servidor. No se puede utilizar un botón Enviar para calcular secuencias de comandos. En este caso, los cálculos no se ejecutan porque el servicio de Forms considera que la interacción ha finalizado.

Para ilustrar el uso de una secuencia de comandos de diseño de formulario, en esta sección se examina un formulario interactivo sencillo que contiene una secuencia de comandos configurada para ejecutarse en el servidor. El diagrama siguiente muestra un diseño de formulario que contiene una secuencia de comandos que agrega valores que el usuario introduce en los dos primeros campos y muestra el resultado en el tercer campo.

![cf_cf_caldata](assets/cf_cf_caldata.png)

**A.** Campo denominado Campo numérico1 **B.** Campo denominado NumericField2 **C.** Campo denominado NumericField3

La sintaxis de la secuencia de comandos ubicada en este diseño de formulario es la siguiente:

```javascript
     NumericField3 = NumericField2 + NumericField1
```

En este diseño de formulario, el botón Calcular es un botón de comando y la secuencia de comandos se encuentra en el `Click` evento. Cuando un usuario introduce valores en los dos primeros campos (NumericField1 y NumericField2) y hace clic en el botón Calcular, el formulario se envía al servicio Forms, donde se ejecuta la secuencia de comandos. El servicio Forms vuelve a procesar el formulario en el dispositivo cliente con los resultados del cálculo mostrados en el campo NumericField3 .

>[!NOTE]
>
>Para obtener información sobre cómo crear una secuencia de comandos de diseño de formulario, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para calcular los datos de formulario, realice las tareas siguientes:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Recupere un formulario que contenga una secuencia de comandos de cálculo.
1. Vuelva a escribir el flujo de datos del formulario en el explorador web del cliente

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de cliente de Forms**

Para poder realizar mediante programación una operación de API de cliente de servicio de Forms, debe crear un cliente de servicio de Forms. Si utiliza la API de Java, cree un `FormsServiceClient` objeto. Si utiliza la API del servicio web de Forms, cree un `FormsServiceService` objeto.

**Recuperar un formulario que contenga una secuencia de comandos de cálculo**

La API de cliente del servicio Forms se utiliza para crear una lógica de aplicación que gestione un formulario que contenga una secuencia de comandos configurada para ejecutarse en el servidor. El proceso es similar a la gestión de un formulario enviado. (Consulte [Gestión de Forms enviado](/help/forms/developing/handling-submitted-forms.md).)

Compruebe que el estado de procesamiento asociado al formulario enviado sea `1` `(Calculate)`, lo que significa que el servicio de Forms está realizando una operación de cálculo en los datos del formulario y que los resultados deben devolverse al usuario. En este caso, se ejecuta automáticamente una secuencia de comandos configurada para ejecutarse en el servidor.

**Vuelva a escribir el flujo de datos del formulario en el explorador web del cliente**

Después de comprobar que el estado de procesamiento asociado a un formulario enviado es `1`, debe volver a escribir los resultados en el explorador web del cliente. Cuando se muestra el formulario, el valor calculado aparece en los campos correspondientes.

**Consulte también lo siguiente**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Calcular los datos de formulario mediante la API de Java](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)
[Calcular los datos de formulario mediante la API de servicio web](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)
[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)
[Renderización de PDF forms interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)
[Creación de aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Calcular los datos de formulario mediante la API de Java {#calculate-form-data-using-the-java-api}

Calcule los datos del formulario utilizando la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-forms-client.jar en la ruta de clase de su proyecto Java.

1. Creación de un objeto de API de cliente de Forms

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `FormsServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recuperar un formulario que contenga una secuencia de comandos de cálculo

   * Para recuperar datos de formulario que contengan una secuencia de comandos de cálculo, cree un `com.adobe.idp.Document` usando su constructor e invocando la variable `javax.servlet.http.HttpServletResponse` del objeto `getInputStream` desde dentro del constructor.
   * Invocar el `FormsServiceClient` del objeto `processFormSubmission` y pase los siguientes valores:

      * La variable `com.adobe.idp.Document` objeto que contiene los datos del formulario.
      * Un valor de cadena que especifica variables de entorno, incluidos todos los encabezados HTTP relevantes. Debe especificar el tipo de contenido que se va a gestionar especificando uno o más valores para la variable `CONTENT_TYPE` variable de entorno. Por ejemplo, para gestionar datos XML y de PDF, especifique el siguiente valor de cadena para este parámetro: `CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`
      * Un valor de cadena que especifica la variable `HTTP_USER_AGENT` valor de encabezado; por ejemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` que almacena opciones en tiempo de ejecución.

      La variable `processFormSubmission` el método devuelve un `FormsResult` que contiene los resultados del envío del formulario.

   * Comprobar que el estado de procesamiento asociado a un formulario enviado es `1` invocando la variable `FormsResult` del objeto `getAction` método. Si este método devuelve el valor `1`, se realizó el cálculo y los datos se pueden escribir de nuevo en el explorador web del cliente.


1. Vuelva a escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un `javax.servlet.ServletOutputStream` objeto utilizado para enviar una secuencia de datos de formulario al explorador web del cliente.
   * Cree un `com.adobe.idp.Document` invocando el objeto `FormsResult` objeto ‘s `getOutputContent` método.
   * Cree un `java.io.InputStream` invocando el objeto `com.adobe.idp.Document` del objeto `getInputStream` método.
   * Cree una matriz de bytes y rellénela con la secuencia de datos del formulario invocando la variable `InputStream` del objeto `read` y pasando la matriz de bytes como argumento.
   * Invocar el `javax.servlet.ServletOutputStream` del objeto `write` método para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes a la `write` método.

**Consulte también lo siguiente**


[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Calcular los datos de formulario mediante la API de servicio web {#calculate-form-data-using-the-web-service-api}

Calcule los datos del formulario utilizando la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases proxy de Java en la ruta de clase.

1. Creación de un objeto de API de cliente de Forms

   Cree un `FormsService` y establezca los valores de autenticación.

1. Recuperar un formulario que contenga una secuencia de comandos de cálculo

   * Para recuperar datos de formulario publicados en un servlet Java, cree un `BLOB` usando su constructor.
   * Cree un `java.io.InputStream` usando la variable `javax.servlet.http.HttpServletResponse` del objeto `getInputStream` método.
   * Cree un `java.io.ByteArrayOutputStream` usando su constructor y pasando la longitud de `java.io.InputStream` objeto.
   * Copie el contenido del `java.io.InputStream` en el `java.io.ByteArrayOutputStream` objeto.
   * Cree una matriz de bytes invocando la variable `java.io.ByteArrayOutputStream` del objeto `toByteArray` método.
   * Rellene el `BLOB` invocando su `setBinaryData` y pasando la matriz de bytes como argumento.
   * Cree un `RenderOptionsSpec` usando su constructor. Establezca el valor de configuración regional invocando la variable `RenderOptionsSpec` del objeto `setLocale` y pasando un valor de cadena que especifica el valor de configuración regional.
   * Invocar el `FormsServiceClient` del objeto `processFormSubmission` y pase los siguientes valores:

      * La variable `BLOB` objeto que contiene los datos del formulario.
      * Un valor de cadena que especifica variables de entorno que incluye todos los encabezados HTTP relevantes. Por ejemplo, puede especificar el siguiente valor de cadena: `HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * Un valor de cadena que especifica la variable `HTTP_USER_AGENT` valor de encabezado; por ejemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` que almacena opciones en tiempo de ejecución. Para obtener más información, .
      * Un vacío `BLOBHolder` objeto que rellena el método .
      * Un vacío `javax.xml.rpc.holders.StringHolder` objeto que rellena el método .
      * Un vacío `BLOBHolder` objeto que rellena el método .
      * Un vacío `BLOBHolder` objeto que rellena el método .
      * Un vacío `javax.xml.rpc.holders.ShortHolder` objeto que rellena el método .
      * Un vacío `MyArrayOf_xsd_anyTypeHolder` objeto que rellena el método . Este parámetro se utiliza para almacenar archivos adjuntos enviados junto con el formulario.
      * Un vacío `FormsResultHolder` objeto que rellena el método con el formulario enviado.

      La variable `processFormSubmission` rellena el `FormsResultHolder` con los resultados del envío del formulario. La variable `processFormSubmission` el método devuelve un `FormsResult` que contiene los resultados del envío del formulario.

   * Comprobar que el estado de procesamiento asociado a un formulario enviado es `1` invocando la variable `FormsResult` del objeto `getAction` método. Si este método devuelve el valor `1`, se realizó el cálculo y los datos se pueden escribir de nuevo en el explorador web del cliente.


1. Vuelva a escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un `javax.servlet.ServletOutputStream` objeto utilizado para enviar una secuencia de datos de formulario al explorador web del cliente.
   * Cree un `BLOB` objeto que contiene datos de formulario invocando la variable `FormsResult` del objeto `getOutputContent` método.
   * Cree una matriz de bytes y rellénela invocando la variable `BLOB` del objeto `getBinaryData` método. Esta tarea asigna el contenido de la variable `FormsResult` a la matriz de bytes.
   * Invocar el `javax.servlet.http.HttpServletResponse` del objeto `write` método para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes a la `write` método.

**Consulte también**
[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
