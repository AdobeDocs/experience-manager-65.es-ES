---
title: Cálculo de datos de formulario
seo-title: Cálculo de datos de formulario
description: nulo
seo-description: nulo
uuid: ccd85bc7-8ccc-44d9-9424-dfc1f603e688
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: b4f57e42-60a6-407d-9764-15a11615827d
translation-type: tm+mt
source-git-commit: 4b9e2ceafc301db9337868b78bcae87c0f07e14b

---


# Cálculo de datos de formulario {#calculating-form-data}

El servicio Forms puede calcular los valores que un usuario introduce en un formulario y mostrar los resultados. Para calcular los datos del formulario, debe realizar dos tareas. En primer lugar, se crea una secuencia de comandos de diseño de formulario que calcula los datos del formulario. Un diseño de formulario admite tres tipos de secuencias de comandos. Un tipo de secuencia de comandos se ejecuta en el cliente, otro se ejecuta en el servidor y el tercer tipo se ejecuta tanto en el servidor como en el cliente. El tipo de secuencia de comandos analizado en este tema se ejecuta en el servidor. Los cálculos del lado del servidor son compatibles con las transformaciones de HTML, PDF y de la guía de formularios (obsoleto).

Como parte del proceso de diseño de formularios, puede utilizar cálculos y secuencias de comandos para proporcionar una experiencia de usuario más rica. Los cálculos y las secuencias de comandos se pueden agregar a la mayoría de los objetos y campos de formulario. Debe crear una secuencia de comandos de diseño de formulario para realizar operaciones de cálculo en los datos que un usuario introduce en un formulario interactivo.

El usuario introduce valores en el formulario y hace clic en el botón Calcular para ver los resultados. El siguiente proceso describe una aplicación de ejemplo que permite al usuario calcular datos:

* El usuario accede a una página HTML denominada StartLoan.html que actúa como página de inicio de la aplicación web. Esta página invoca un servlet Java llamado `GetLoanForm`.
* El `GetLoanForm` servlet procesa un formulario de préstamo. Este formulario contiene una secuencia de comandos, campos interactivos, un botón de cálculo y un botón de envío.
* El usuario introduce valores en los campos del formulario y hace clic en el botón Calcular. El formulario se envía al servlet de Java `CalculateData` donde se ejecuta la secuencia de comandos. El formulario se devuelve al usuario con los resultados de cálculo mostrados en el formulario.
* El usuario continúa introduciendo y calculando valores hasta que se muestra un resultado satisfactorio. Cuando esté satisfecho, el usuario hace clic en el botón Enviar para procesar el formulario. El formulario se envía a otro servlet Java denominado `ProcessForm` que es responsable de recuperar los datos enviados. (Consulte [Gestión de formularios](/help/forms/developing/rendering-forms.md#handling-submitted-forms)enviados).


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
   <td><p>El servlet <code>GetLoanForm</code> Java se invoca desde la página de inicio de HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>El servlet <code>GetLoanForm</code> Java utiliza la API del cliente de servicios de Forms para procesar el formulario de préstamo en el navegador web del cliente. La diferencia entre procesar un formulario que contiene una secuencia de comandos configurada para ejecutarse en el servidor y procesar un formulario que no contiene una secuencia de comandos es que debe especificar la ubicación de destino utilizada para ejecutar la secuencia de comandos. Si no se especifica una ubicación de destino, no se ejecuta una secuencia de comandos configurada para ejecutarse en el servidor. Por ejemplo, considere la aplicación introducida en esta sección. El servlet <code>CalculateData</code> Java es la ubicación de destino donde se ejecuta la secuencia de comandos.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>El usuario introduce datos en campos interactivos y hace clic en el botón Calcular. El formulario se envía al servlet de <code>CalculateData</code> Java, donde se ejecuta la secuencia de comandos. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>El formulario se vuelve a procesar en el explorador Web con los resultados de cálculo mostrados en el formulario. </p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>El usuario hace clic en el botón Enviar cuando los valores sean satisfactorios. El formulario se envía a otro servlet Java denominado <code>ProcessForm</code>.</p></td>
  </tr>
 </tbody>
</table>

Normalmente, un formulario que se envía como contenido PDF contiene secuencias de comandos que se ejecutan en el cliente. Sin embargo, también se pueden ejecutar cálculos del lado del servidor. No se puede utilizar un botón Enviar para calcular secuencias de comandos. En este caso, los cálculos no se ejecutan porque el servicio Forms considera que la interacción está completa.

Para ilustrar el uso de una secuencia de comandos de diseño de formulario, en esta sección se examina un formulario interactivo sencillo que contiene una secuencia de comandos configurada para ejecutarse en el servidor. El diagrama siguiente muestra un diseño de formulario que contiene una secuencia de comandos que agrega valores que un usuario introduce en los dos primeros campos y muestra el resultado en el tercer campo.

![cf_cf_caldata](assets/cf_cf_caldata.png)

******A. Campo denominado NumericField1** B. Campo denominado NumericField2 **C.** Campo denominado NumericField3

La sintaxis de la secuencia de comandos ubicada en este diseño de formulario es la siguiente:

```as3
     NumericField3 = NumericField2 + NumericField1
```

En este diseño de formulario, el botón Calcular es un botón de comando y la secuencia de comandos se encuentra en el `Click` suceso de este botón. Cuando un usuario introduce valores en los dos primeros campos (NumericField1 y NumericField2) y hace clic en el botón Calcular, el formulario se envía al servicio Forms, donde se ejecuta la secuencia de comandos. El servicio Forms devuelve el formulario al dispositivo cliente con los resultados del cálculo que se muestran en el campo NumericField3.

>[!NOTE]
>
>Para obtener información sobre la creación de una secuencia de comandos de diseño de formulario, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para calcular los datos del formulario, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de Forms Client.
1. Recupere un formulario que contenga una secuencia de comandos de cálculo.
1. Volver a escribir el flujo de datos del formulario en el navegador web del cliente

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Forms Client**

Para poder realizar mediante programación una operación de API de cliente de servicio de Forms, debe crear un cliente de servicio de Forms. Si utiliza la API de Java, cree un `FormsServiceClient` objeto. Si utiliza la API de servicio web de Forms, cree un `FormsServiceService` objeto.

**Recuperar un formulario que contenga una secuencia de comandos de cálculo**

La API de cliente de servicios de Forms se utiliza para crear una lógica de aplicación que gestiona un formulario que contiene una secuencia de comandos configurada para ejecutarse en el servidor. El proceso es similar al de administrar un formulario enviado. (Consulte [Gestión de formularios]enviados (/help/forms/develop/procesing-forms-procesing-forms-handling-submit-forms-handling-submit.md#handling-submit-forms).)

Compruebe que el estado de procesamiento asociado con el formulario enviado es `1``(Calculate)`, lo que significa que el servicio Forms está realizando una operación de cálculo en los datos del formulario y que los resultados se deben devolver al usuario. En este caso, se ejecuta automáticamente una secuencia de comandos configurada para ejecutarse en el servidor.

**Volver a escribir el flujo de datos del formulario en el navegador web del cliente**

Después de comprobar que el estado de procesamiento asociado a un formulario enviado es `1`, debe volver a escribir los resultados en el navegador web del cliente. Cuando se muestra el formulario, el valor calculado aparecerá en los campos correspondientes.

**Consulte también**

[Inclusión de archivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)de biblioteca Java de AEM Forms[Calcular datos de formulario mediante la API](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)[de JavaCalcular datos de formulario mediante la API](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)[Configuración de propiedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexión API de servicio de[Forms Inicio](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)[](/help/forms/developing/rendering-interactive-pdf-forms.md)[rápido de formularios PDF interactivos Procesamiento de formularios PDF Creación de aplicaciones Web](/help/forms/developing/creating-web-applications-renders-forms.md)

## Calcular datos de formulario mediante la API de Java {#calculate-form-data-using-the-java-api}

Calcular los datos del formulario mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clases del proyecto Java.

1. Creación de un objeto de API de Forms Client

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `FormsServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recuperar un formulario que contenga una secuencia de comandos de cálculo

   * Para recuperar datos de formulario que contengan una secuencia de comandos de cálculo, cree un `com.adobe.idp.Document` objeto utilizando su constructor e invocando el `javax.servlet.http.HttpServletResponse` método del `getInputStream` objeto desde el constructor.
   * Invoque el `FormsServiceClient` método del `processFormSubmission` objeto y pase los valores siguientes:

      * El `com.adobe.idp.Document` objeto que contiene los datos del formulario.
      * Un valor de cadena que especifica variables de entorno, incluyendo todos los encabezados HTTP relevantes. Debe especificar el tipo de contenido que se va a gestionar especificando uno o varios valores para la variable de `CONTENT_TYPE` entorno. Por ejemplo, para gestionar datos XML y PDF, especifique el siguiente valor de cadena para este parámetro: `CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`
      * Un valor de cadena que especifica el valor del `HTTP_USER_AGENT` encabezado; por ejemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Un `RenderOptionsSpec` objeto que almacena opciones de tiempo de ejecución.
      El `processFormSubmission` método devuelve un `FormsResult` objeto que contiene los resultados del envío del formulario.

   * Compruebe que el estado de procesamiento asociado a un formulario enviado `1` invoca el `FormsResult` método `getAction` del objeto. Si este método devuelve el valor `1`, se realizó el cálculo y los datos se pueden volver a escribir en el explorador web del cliente.


1. Volver a escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un `javax.servlet.ServletOutputStream` objeto que se utilice para enviar una secuencia de datos de formulario al navegador web del cliente.
   * Cree un `com.adobe.idp.Document` objeto invocando el `FormsResult` método ‘s `getOutputContent` .
   * Cree un `java.io.InputStream` objeto invocando el `com.adobe.idp.Document` método `getInputStream` del objeto.
   * Cree una matriz de bytes y rellénela con la secuencia de datos del formulario invocando el `InputStream` método del `read` objeto y pasando la matriz de bytes como argumento.
   * Invoque el `javax.servlet.ServletOutputStream` método del `write` objeto para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al `write` método .

**Consulte también**


[Inclusión de archivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)de biblioteca Java de AEM Forms[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Calcular datos de formulario mediante la API de servicio Web {#calculate-form-data-using-the-web-service-api}

Calcular los datos del formulario mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases proxy de Java que consuman el WSDL del servicio Forms.
   * Incluya las clases proxy de Java en la ruta de clases.

1. Creación de un objeto de API de Forms Client

   Cree un `FormsService` objeto y defina los valores de autenticación.

1. Recuperar un formulario que contenga una secuencia de comandos de cálculo

   * Para recuperar datos de formulario publicados en un servlet Java, cree un `BLOB` objeto con su constructor.
   * Cree un `java.io.InputStream` objeto mediante el `javax.servlet.http.HttpServletResponse` método `getInputStream` del objeto.
   * Cree un `java.io.ByteArrayOutputStream` objeto utilizando su constructor y pasando la longitud del `java.io.InputStream` objeto.
   * Copie el contenido del `java.io.InputStream` objeto en el `java.io.ByteArrayOutputStream` objeto.
   * Cree una matriz de bytes invocando el `java.io.ByteArrayOutputStream` método `toByteArray` del objeto.
   * Rellene el `BLOB` objeto invocando su `setBinaryData` método y pasando la matriz de bytes como argumento.
   * Cree un `RenderOptionsSpec` objeto con su constructor. Establezca el valor de configuración regional invocando el `RenderOptionsSpec` método `setLocale` del objeto y pasando un valor de cadena que especifica el valor de configuración regional.
   * Invoque el `FormsServiceClient` método del `processFormSubmission` objeto y pase los valores siguientes:

      * El `BLOB` objeto que contiene los datos del formulario.
      * Un valor de cadena que especifica variables de entorno incluye todos los encabezados HTTP relevantes. Por ejemplo, puede especificar el siguiente valor de cadena: `HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * Un valor de cadena que especifica el valor del `HTTP_USER_AGENT` encabezado; por ejemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Un `RenderOptionsSpec` objeto que almacena opciones de tiempo de ejecución. Para obtener más información, .
      * Objeto vacío `BLOBHolder` que se rellena con el método .
      * Objeto vacío `javax.xml.rpc.holders.StringHolder` que se rellena con el método .
      * Objeto vacío `BLOBHolder` que se rellena con el método .
      * Objeto vacío `BLOBHolder` que se rellena con el método .
      * Objeto vacío `javax.xml.rpc.holders.ShortHolder` que se rellena con el método .
      * Objeto vacío `MyArrayOf_xsd_anyTypeHolder` que se rellena con el método . Este parámetro se utiliza para almacenar archivos adjuntos enviados junto con el formulario.
      * Objeto vacío `FormsResultHolder` que se rellena con el método con el formulario que se envía.
      El `processFormSubmission` método rellena el `FormsResultHolder` parámetro con los resultados del envío del formulario. El `processFormSubmission` método devuelve un `FormsResult` objeto que contiene los resultados del envío del formulario.

   * Compruebe que el estado de procesamiento asociado a un formulario enviado `1` invoca el `FormsResult` método `getAction` del objeto. Si este método devuelve el valor `1`, se realizó el cálculo y los datos se pueden volver a escribir en el explorador web del cliente.


1. Volver a escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un `javax.servlet.ServletOutputStream` objeto que se utilice para enviar una secuencia de datos de formulario al navegador web del cliente.
   * Cree un `BLOB` objeto que contenga datos de formulario invocando el `FormsResult` método `getOutputContent` del objeto.
   * Cree una matriz de bytes y rellénela invocando el `BLOB` método `getBinaryData` del objeto. Esta tarea asigna el contenido del `FormsResult` objeto a la matriz de bytes.
   * Invoque el `javax.servlet.http.HttpServletResponse` método del `write` objeto para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al `write` método .

**Consulte también** Invocación[de formularios AEM con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
