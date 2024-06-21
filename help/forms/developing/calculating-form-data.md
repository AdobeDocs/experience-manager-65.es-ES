---
title: Calcular datos de formulario
description: Utilice el servicio Forms para calcular los valores que un usuario introduce en un formulario y mostrar los resultados. El servicio Forms calcula los valores mediante la API de Java y la API de servicio web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
role: Developer
exl-id: 28abf044-6c8e-4578-ae2e-54cdbd694c5f
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '1858'
ht-degree: 0%

---

# Calcular datos de formulario {#calculating-form-data}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

El servicio Forms puede calcular los valores que un usuario introduce en un formulario y mostrar los resultados. Para calcular los datos del formulario, debe realizar dos tareas. En primer lugar, se crea un script de diseño de formulario que calcula los datos del formulario. Un diseño de formulario admite tres tipos de scripts. Un tipo de script se ejecuta en el cliente, otro se ejecuta en el servidor y el tercer tipo se ejecuta tanto en el servidor como en el cliente. El tipo de script que se describe en este tema se ejecuta en el servidor. Los cálculos del lado del servidor son compatibles con las transformaciones de HTML, PDF y Guía de formularios (obsoletas).

Como parte del proceso de diseño del formulario, puede utilizar cálculos y scripts para proporcionar una experiencia de usuario más rica. Los cálculos y las secuencias de comandos se pueden agregar a la mayoría de los campos y objetos de formulario. Cree una secuencia de comandos de diseño de formulario para realizar operaciones de cálculo con los datos que un usuario introduce en un formulario interactivo.

El usuario introduce valores en el formulario y hace clic en el botón Calcular para ver los resultados. El siguiente proceso describe una aplicación de ejemplo que permite a un usuario calcular datos:

* El usuario tiene acceso a una página de HTML denominada StartLoan.html que actúa como página de inicio de la aplicación web. Esta página invoca un servlet Java denominado `GetLoanForm`.
* El `GetLoanForm` servlet procesa un formulario de préstamo. Este formulario contiene un script, campos interactivos, un botón de cálculo y un botón de envío.
* El usuario introduce valores en los campos del formulario y hace clic en el botón Calcular. El formulario se envía a `CalculateData` Servlet Java donde se ejecuta el script. El formulario se devuelve al usuario con los resultados del cálculo mostrados en el formulario.
* El usuario continúa introduciendo y calculando valores hasta que se muestra un resultado satisfactorio. Cuando esté satisfecho, el usuario hace clic en el botón Enviar para procesar el formulario. El formulario se enviará a otro servlet Java denominado `ProcessForm` que es responsable de recuperar los datos enviados. (Consulte [Gestión de Forms enviados](/help/forms/developing/rendering-forms.md#handling-submitted-forms).)


El diagrama siguiente muestra el flujo lógico de la aplicación.

![cf_cf_finsrv_loancalcapp_v1](assets/cf_cf_finsrv_loancalcapp_v1.png)

En la tabla siguiente se describen los pasos de este diagrama.

<table>
 <thead>
  <tr>
   <th><p>Paso</p></th>
   <th><p>Descripción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>El <code>GetLoanForm</code> El servlet Java se invoca desde la página de inicio del HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>El <code>GetLoanForm</code> Java Servlet utiliza la API del cliente del servicio de Forms para procesar el formulario de préstamo en el explorador web del cliente. La diferencia entre procesar un formulario que contiene una secuencia de comandos configurada para ejecutarse en el servidor y procesar un formulario que no contiene una secuencia de comandos es que debe especificar la ubicación de destino utilizada para ejecutar la secuencia de comandos. Si no se especifica una ubicación de destino, no se ejecuta ninguna secuencia de comandos configurada para ejecutarse en el servidor. Por ejemplo, considere la aplicación introducida en esta sección. El <code>CalculateData</code> Servlet Java es la ubicación de destino en la que se ejecuta el script.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>El usuario introduce datos en campos interactivos y hace clic en el botón Calcular. El formulario se envía a <code>CalculateData</code> Servlet Java, donde se ejecuta el script. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>El formulario se vuelve a procesar en el explorador web con los resultados del cálculo mostrados en el formulario. </p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>El usuario hace clic en el botón Enviar cuando los valores son satisfactorios. El formulario se enviará a otro servlet Java denominado <code>ProcessForm</code>.</p></td>
  </tr>
 </tbody>
</table>

Normalmente, un formulario enviado como contenido de PDF contiene scripts que se ejecutan en el cliente. Sin embargo, también se pueden ejecutar cálculos del lado del servidor. No se puede utilizar un botón Enviar para calcular scripts. En este caso, los cálculos no se ejecutan porque el servicio Forms considera que la interacción ha finalizado.

Para ilustrar el uso de una secuencia de comandos de diseño de formulario, esta sección examina un formulario interactivo simple que contiene una secuencia de comandos configurada para ejecutarse en el servidor. El diagrama siguiente muestra un diseño de formulario que contiene una secuencia de comandos que agrega valores que un usuario introduce en los dos primeros campos y muestra el resultado en el tercer campo.

![cf_cf_caldata](assets/cf_cf_caldata.png)

**A.** Campo denominado NumericField1 **B.** Campo denominado NumericField2 **C.** Campo denominado NumericField3

La sintaxis de la secuencia de comandos en este diseño de formulario es la siguiente:

```javascript
     NumericField3 = NumericField2 + NumericField1
```

En este diseño de formulario, el botón Calcular es un botón de comando y la secuencia de comandos se encuentra en el `Click` evento. Cuando un usuario introduce valores en los dos primeros campos (NumericField1 y NumericField2) y hace clic en el botón Calcular, el formulario se envía al servicio de Forms, donde se ejecuta la secuencia de comandos. El servicio Forms vuelve a procesar el formulario en el dispositivo cliente con los resultados del cálculo mostrados en el campo NumericField3.

>[!NOTE]
>
>Para obtener información sobre la creación de scripts de diseño de formulario, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para calcular los datos del formulario, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Recupere un formulario que contenga un script de cálculo.
1. Escribir el flujo de datos de formulario en el explorador web del cliente

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API de cliente de Forms**

Para poder realizar mediante programación una operación de API de cliente de servicio de Forms, debe crear un cliente de servicio de Forms. Si utiliza la API de Java, cree un `FormsServiceClient` objeto. Si utiliza la API del servicio web de Forms, cree un `FormsServiceService` objeto.

**Recuperar un formulario que contiene un script de cálculo**

La API de cliente del servicio de Forms se utiliza para crear una lógica de aplicación que administra un formulario que contiene una secuencia de comandos configurada para ejecutarse en el servidor. El proceso es similar a la gestión de un formulario enviado. (Consulte [Gestión de Forms enviados](/help/forms/developing/handling-submitted-forms.md).)

Compruebe que el estado de procesamiento asociado al formulario enviado es `1` `(Calculate)`, lo que significa que el servicio Forms está realizando una operación de cálculo en los datos del formulario y los resultados deben escribirse en el usuario. En este caso, se ejecuta automáticamente un script configurado para ejecutarse en el servidor.

**Escribir el flujo de datos de formulario en el explorador web del cliente**

Después de comprobar que el estado de procesamiento asociado a un formulario enviado es `1`, debe escribir los resultados de nuevo en el explorador web del cliente. Cuando se muestra el formulario, el valor calculado aparece en los campos correspondientes.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Calcular datos de formulario mediante la API de Java](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)
[Calcular datos de formulario mediante la API de servicio web](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)
[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
[Inicios rápidos de la API del servicio Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)
[Procesamiento de PDF forms interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)
[Crear aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Calcular datos de formulario mediante la API de Java {#calculate-form-data-using-the-java-api}

Calcular datos de formulario mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar en la ruta de clase del proyecto Java.

1. Crear un objeto de API de cliente de Forms

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `FormsServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Recuperar un formulario que contiene un script de cálculo

   * Para recuperar datos de formulario que contengan un script de cálculo, cree un `com.adobe.idp.Document` mediante su constructor e invocando al objeto `javax.servlet.http.HttpServletResponse` del objeto `getInputStream` dentro del constructor.
   * Invoque el `FormsServiceClient` del objeto `processFormSubmission` y pasar los siguientes valores:

      * El `com.adobe.idp.Document` que contiene los datos del formulario.
      * Un valor de cadena que especifica variables de entorno, incluidos todos los encabezados HTTP relevantes. Especifique el tipo de contenido que se va a gestionar especificando uno o más valores para `CONTENT_TYPE` variable de entorno. Por ejemplo, para gestionar datos XML y de PDF, especifique el siguiente valor de cadena para este parámetro: `CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`
      * Un valor de cadena que especifica la variable `HTTP_USER_AGENT` valor del encabezado; por ejemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` que almacena opciones en tiempo de ejecución.

     El `processFormSubmission` El método devuelve un valor `FormsResult` que contiene los resultados del envío del formulario.

   * Compruebe que el estado de procesamiento asociado a un formulario enviado es `1` invocando el método `FormsResult` del objeto `getAction` método. Si este método devuelve el valor `1`, se realizó el cálculo y los datos se pueden escribir de nuevo en el explorador web del cliente.

1. Escribir el flujo de datos de formulario en el explorador web del cliente

   * Crear un `javax.servlet.ServletOutputStream` objeto utilizado para enviar un flujo de datos de formulario al explorador web del cliente.
   * Crear un `com.adobe.idp.Document` invocando el objeto de `FormsResult` del objeto `getOutputContent` método.
   * Crear un `java.io.InputStream` invocando el objeto de `com.adobe.idp.Document` del objeto `getInputStream` método.
   * Cree una matriz de bytes y rellénela con el flujo de datos de formulario invocando el método `InputStream` del objeto `read` y pasando la matriz de bytes como argumento.
   * Invoque el `javax.servlet.ServletOutputStream` del objeto `write` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes a `write` método.

**Consulte también**


[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Calcular datos de formulario mediante la API de servicio web {#calculate-form-data-using-the-web-service-api}

Calcular datos de formulario mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases de proxy Java en la ruta de clase.

1. Crear un objeto de API de cliente de Forms

   Crear un `FormsService` y establezca los valores de autenticación.

1. Recuperar un formulario que contiene un script de cálculo

   * Para recuperar datos de formulario publicados en un servlet Java, cree un `BLOB` mediante su constructor.
   * Crear un `java.io.InputStream` mediante el uso del objeto `javax.servlet.http.HttpServletResponse` del objeto `getInputStream` método.
   * Crear un `java.io.ByteArrayOutputStream` utilizando su constructor y pasando la longitud del objeto `java.io.InputStream` objeto.
   * Copie el contenido del `java.io.InputStream` en el `java.io.ByteArrayOutputStream` objeto.
   * Cree una matriz de bytes invocando el método `java.io.ByteArrayOutputStream` del objeto `toByteArray` método.
   * Rellene el `BLOB` invocando su objeto `setBinaryData` y pasando la matriz de bytes como argumento.
   * Crear un `RenderOptionsSpec` mediante su constructor. Establezca el valor locale invocando el `RenderOptionsSpec` del objeto `setLocale` y pasando un valor de cadena que especifica el valor de configuración regional.
   * Invoque el `FormsServiceClient` del objeto `processFormSubmission` y pasar los siguientes valores:

      * El `BLOB` que contiene los datos del formulario.
      * Un valor de cadena que especifica variables de entorno que incluyen todos los encabezados HTTP relevantes. Por ejemplo, puede especificar el siguiente valor de cadena: `HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * Un valor de cadena que especifica la variable `HTTP_USER_AGENT` valor del encabezado; por ejemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` que almacena opciones en tiempo de ejecución. Para obtener más información, consulte .
      * Un vacío `BLOBHolder` objeto que rellena el método.
      * Un vacío `javax.xml.rpc.holders.StringHolder` objeto que rellena el método.
      * Un vacío `BLOBHolder` objeto que rellena el método.
      * Un vacío `BLOBHolder` objeto que rellena el método.
      * Un vacío `javax.xml.rpc.holders.ShortHolder` objeto que rellena el método.
      * Un vacío `MyArrayOf_xsd_anyTypeHolder` objeto que rellena el método. Este parámetro se utiliza para almacenar los archivos adjuntos enviados junto con el formulario.
      * Un vacío `FormsResultHolder` que rellena el método con el formulario que se envía.

     El `processFormSubmission` rellena el método `FormsResultHolder` con los resultados del envío del formulario. El `processFormSubmission` El método devuelve un valor `FormsResult` que contiene los resultados del envío del formulario.

   * Compruebe que el estado de procesamiento asociado a un formulario enviado es `1` invocando el método `FormsResult` del objeto `getAction` método. Si este método devuelve el valor `1`, se realizó el cálculo y los datos se pueden escribir de nuevo en el explorador web del cliente.

1. Escribir el flujo de datos de formulario en el explorador web del cliente

   * Crear un `javax.servlet.ServletOutputStream` objeto utilizado para enviar un flujo de datos de formulario al explorador web del cliente.
   * Crear un `BLOB` que contiene datos de formulario invocando el `FormsResult` del objeto `getOutputContent` método.
   * Cree una matriz de bytes y rellénela invocando el método `BLOB` del objeto `getBinaryData` método. Esta tarea asigna el contenido del `FormsResult` a la matriz de bytes.
   * Invoque el `javax.servlet.http.HttpServletResponse` del objeto `write` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes a `write` método.

**Consulte también**
[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
