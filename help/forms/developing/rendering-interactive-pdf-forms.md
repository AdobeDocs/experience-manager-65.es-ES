---
title: Renderización de PDF forms interactivos
seo-title: Rendering Interactive PDF Forms
description: Utilice el servicio Forms para procesar PDF forms interactivos en dispositivos cliente, normalmente exploradores web, para recopilar información de los usuarios. Puede utilizar el servicio Forms para procesar formularios interactivos mediante la API de Java y la API del servicio web.
seo-description: Use the Forms service to render interactive PDF forms to client devices, typically web browsers, to collect information from users. You can use Forms service to render interactive forms using the Java API and Web Service API.
uuid: df2a4dc8-f19e-49de-850f-85a204102631
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3cb307ec-9b7b-4f03-b860-48553ccee746
role: Developer
exl-id: d9f32939-c2c0-4531-b15e-f63941c289e3
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2487'
ht-degree: 0%

---

# Renderización de PDF forms interactivos {#rendering-interactive-pdf-forms}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

El servicio Forms procesa PDF forms interactivos en dispositivos cliente, normalmente exploradores web, para recopilar información de los usuarios. Una vez procesado un formulario interactivo, el usuario puede introducir datos en los campos del formulario y hacer clic en un botón de envío ubicado en el formulario para enviar información al servicio de Forms. Adobe Reader o Acrobat deben estar instalados en el equipo que aloje el explorador web del cliente para que pueda verse un formulario de PDF interactivo.

>[!NOTE]
>
>Para poder procesar un formulario con el servicio Forms, debe crear un diseño de formulario. Normalmente, un diseño de formulario se crea en Designer y se guarda como archivo XDP. Para obtener información sobre cómo crear un diseño de formulario, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

**Solicitud de préstamo de muestra**

Se ha introducido una aplicación de préstamo de ejemplo para demostrar cómo el servicio Forms utiliza formularios interactivos para recopilar información de los usuarios. Esta aplicación permite a un usuario rellenar un formulario con los datos necesarios para obtener un préstamo y, a continuación, enviar datos al servicio de Forms. En el diagrama siguiente se muestra el flujo lógico de la aplicación del préstamo.

![ri_ri_finsrv_loanapp_v1](assets/ri_ri_finsrv_loanapp_v1.png)

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
   <td><p>La variable <code>GetLoanForm</code> El servlet Java se invoca desde una página de HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>La variable <code>GetLoanForm</code> Java Servlet utiliza la API de cliente de servicio de Forms para procesar el formulario de préstamo en el explorador web del cliente. (Consulte <a href="#render-an-interactive-pdf-form-using-the-java-api">Representar un formulario de PDF interactivo mediante la API de Java</a>.)</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Una vez que el usuario rellena el formulario de préstamo y hace clic en el botón de envío, los datos se envían al <code>HandleData</code> Servlet Java. (Consulte <i>"Forma de préstamo"</i>.)</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>La variable <code>HandleData</code> Java Servlet utiliza la API de cliente del servicio Forms para procesar el envío del formulario y recuperar los datos del formulario. A continuación, los datos se almacenan en una base de datos empresarial. (Consulte <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">Gestión de Forms enviado</a>.)</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Se devuelve un formulario de confirmación al explorador web. Los datos, como el nombre y los apellidos del usuario, se combinan con el formulario antes de procesarse. (Consulte <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">Rellenado previo de Forms con diseños flexibles</a>.)</p></td>
  </tr>
 </tbody>
</table>

**Formulario de préstamo**

Este formulario de préstamo interactivo se procesa mediante la solicitud de préstamo de ejemplo `GetLoanForm` Servlet Java.

![ri_ri_loanform](assets/ri_ri_loanform.png)

**Formulario de confirmación**

Este formulario se procesa mediante el ejemplo de aplicación de préstamos `HandleData` Servlet Java.

![ri_ri_confirm](assets/ri_ri_confirm.png)

La variable `HandleData` El Servlet Java rellena previamente este formulario con el nombre y los apellidos del usuario, así como la cantidad. Una vez que el formulario se rellena previamente, se envía al explorador web del cliente. (Consulte [Rellenado previo de Forms con diseños flexibles](/help/forms/developing/prepopulating-forms-flowable-layouts.md))

**Servlets Java**

La aplicación de préstamo de ejemplo es un ejemplo de una aplicación de servicio de Forms que existe como servlet Java. Un servlet Java es un programa Java que se ejecuta en un servidor de aplicaciones J2EE, como WebSphere, y contiene código de API de cliente del servicio Forms.

El siguiente código muestra la sintaxis de un servlet Java llamado GetLoanForm:

```java
     public class GetLoanForm extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

             }
```

Normalmente, no colocaría el código de API de cliente de servicio de Forms dentro de un servlet Java `doGet` o `doPost` método. Es una mejor práctica de programación colocar este código dentro de una clase separada, crear una instancia de la clase desde el `doPost` método (o `doGet` ) y llame a los métodos adecuados. Sin embargo, para la brevedad del código, los ejemplos de código de esta sección se reducen al mínimo y los ejemplos de código se colocan en la variable `doPost` método.

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

**Resumen de los pasos**

Para procesar un formulario de PDF interactivo, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Especifique valores de URI.
1. Adjuntar archivos al formulario (opcional).
1. Representar un formulario de PDF interactivo.
1. Escriba el flujo de datos del formulario en el explorador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de cliente de Forms**

Para poder realizar una operación de API de cliente de servicio de Forms mediante programación, debe crear un objeto de API de cliente de Forms. Si utiliza la API de Java, cree un `FormsServiceClient` objeto. Si utiliza la API del servicio web de Forms, cree un `FormsService` objeto.

**Especificar valores de URI**

Puede especificar los valores de URI que requiere el servicio Forms para procesar un formulario. Se puede hacer referencia a un diseño de formulario guardado como parte de una aplicación de Forms mediante el valor de URI raíz de contenido `repository:///`. Por ejemplo, considere el siguiente diseño de formulario denominado *Loan.xdp* ubicada dentro de una aplicación de Forms llamada *FormsApplication*:

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

Para acceder a este diseño de formulario, especifique `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` como nombre del formulario (el primer parámetro pasado al `renderPDFForm` método) y `repository:///` como valor de URI raíz de contenido.

>[!NOTE]
>
>Para obtener información sobre la creación de una aplicación de Forms mediante Workbench, consulte [Ayuda de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

La ruta a un recurso ubicado en una aplicación de Forms es:

`Applications/Application-name/Application-version/Folder.../Filename`

Los siguientes valores muestran algunos ejemplos de valores de URI:

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

Cuando procesa un formulario interactivo, puede definir valores de URI como la dirección URL de destino donde se publican los datos del formulario. La dirección URL de destino se puede definir de una de las siguientes maneras:

* En el botón Enviar mientras se diseña el diseño de formulario en Designer
* Mediante la API de cliente del servicio Forms

Si la dirección URL de destino está definida en el diseño de formulario, no la anule con la API de cliente del servicio de Forms. Es decir, si se define la dirección URL de destino mediante la API de Forms, se restablece la dirección URL especificada en el diseño de formulario en la especificada mediante la API. Si desea enviar el formulario de PDF a la dirección URL de destino especificada en el diseño de formulario, establezca programáticamente la dirección URL de destino en una cadena vacía.

Si tiene un formulario que contiene un botón de envío y un botón de cálculo (con una secuencia de comandos correspondiente que se ejecuta en el servidor), puede definir mediante programación la dirección URL a la que se envía el formulario para ejecutar la secuencia de comandos. Utilice el botón de envío del diseño de formulario para especificar la dirección URL donde se publican los datos del formulario. (Consulte [Cálculo de datos de formulario](/help/forms/developing/calculating-form-data.md).)

>[!NOTE]
>
>En lugar de especificar un valor de URL para hacer referencia a un archivo XDP, también puede pasar un `com.adobe.idp.Document` al servicio de Forms. La variable `com.adobe.idp.Document` contiene un diseño de formulario. (Consulte [Pasar documentos al servicio de Forms](/help/forms/developing/passing-documents-forms-service.md).)

**Adjuntar archivos al formulario**

Puede adjuntar archivos a un formulario. Cuando se procesa un formulario de PDF con archivos adjuntos, los usuarios pueden recuperar los archivos adjuntos en Acrobat mediante el panel de archivos adjuntos. Puede adjuntar distintos tipos de archivo a un formulario, como un archivo de texto, o a un archivo binario, como un archivo JPG.

>[!NOTE]
>
>Adjuntar archivos adjuntos a un formulario es opcional.

**Representar un formulario PDF interactivo**

Para procesar un formulario, utilice un diseño de formulario creado en Designer y guardado como archivo XDP o PDF. Además, puede procesar un formulario creado con Acrobat y guardado como archivo de PDF. Para procesar un formulario de PDF interactivo, invoque la variable `FormsServiceClient` del objeto `renderPDFForm` método o `renderPDFForm2` método.

La variable `renderPDFForm` utiliza un `URLSpec` objeto. La raíz de contenido al archivo XDP se pasa al servicio de Forms mediante la variable `URLSpec` del objeto `setContentRootURI` método. El nombre del diseño de formulario ( `formQuery`) se pasa como un valor de parámetro independiente. Los dos valores se concatenan para obtener la referencia absoluta al diseño de formulario.

La variable `renderPDFForm2` acepta un `com.adobe.idp.Document` instancia que contiene el documento XDP o PDF que se va a procesar.

>[!NOTE]
>
>La opción de tiempo de ejecución del PDF etiquetado no se puede establecer si el documento de entrada es un documento del PDF. Si el archivo de entrada es un archivo XDP, se puede configurar la opción de PDF etiquetado.

## Representar un formulario de PDF interactivo mediante la API de Java {#render-an-interactive-pdf-form-using-the-java-api}

Representar un formulario de PDF interactivo mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-forms-client.jar, en la ruta de clase de su proyecto Java.

1. Creación de un objeto de API de cliente de Forms

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `FormsServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Especificar valores de URI

   * Cree un `URLSpec` objeto que almacena valores de URI utilizando su constructor.
   * Invocar el `URLSpec` del objeto `setApplicationWebRoot` y pase un valor de cadena que represente la raíz web de la aplicación.
   * Invocar el `URLSpec` del objeto `setContentRootURI` y pase un valor de cadena que especifique el valor de URI raíz del contenido. Asegúrese de que el diseño de formulario se encuentra en el URI raíz del contenido. Si no es así, el servicio de Forms genera una excepción. Para hacer referencia al repositorio, especifique `repository:///`.
   * Invocar el `URLSpec` del objeto `setTargetURL` y pase un valor de cadena que especifique el valor de la dirección URL de destino donde se publican los datos del formulario. Si define la dirección URL de destino en el diseño de formulario, puede pasar una cadena vacía. También puede especificar la dirección URL a la que se envía un formulario para realizar cálculos.

1. Adjuntar archivos al formulario

   * Cree un `java.util.HashMap` para almacenar archivos adjuntos usando su constructor.
   * Invocar el `java.util.HashMap` del objeto `put` para cada archivo que se adjuntará al formulario procesado. Pase los siguientes valores a este método:

      * Un valor de cadena que especifica el nombre del archivo adjunto, incluida la extensión de nombre de archivo.
   * A `com.adobe.idp.Document` objeto que contiene el archivo adjunto.

   >[!NOTE]
   >
   >Repita este paso para cada archivo que desee adjuntar al formulario. Este paso es opcional y puede pasar `null` si no desea enviar archivos adjuntos.

1. Representar un formulario PDF interactivo

   Invocar el `FormsServiceClient` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un vacío `com.adobe.idp.Document` objeto.
   * A `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución. Este es un parámetro opcional y puede especificar `null` si no desea especificar opciones de tiempo de ejecución.
   * A `URLSpec` que contiene valores de URI necesarios para el servicio Forms.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   La variable `renderPDFForm` el método devuelve un `FormsResult` objeto que contiene un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un `com.adobe.idp.Document` invocando el objeto `FormsResult` objeto ‘s `getOutputContent` método.
   * Obtenga el tipo de contenido de la variable `com.adobe.idp.Document` invocando su `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasar el tipo de contenido de la variable `com.adobe.idp.Document` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos del formulario en el explorador web del cliente invocando la variable `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Cree un `java.io.InputStream` invocando el objeto `com.adobe.idp.Document` del objeto `getInputStream` método.
   * Cree una matriz de bytes y rellénela con la secuencia de datos del formulario invocando la variable `InputStream` del objeto `read` y pasando la matriz de bytes como argumento.
   * Invocar el `javax.servlet.ServletOutputStream` del objeto `write` método para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes a la `write` método.

## Representar un formulario de PDF interactivo mediante la API de servicio web {#render-an-interactive-pdf-form-using-the-web-service-api}

Representar un formulario de PDF interactivo mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases proxy de Java en la ruta de clase.

1. Creación de un objeto de API de cliente de Forms

   Cree un `FormsService` y establezca los valores de autenticación.

1. Especificar valores de URI

   * Cree un `URLSpec` objeto que almacena valores de URI utilizando su constructor.
   * Invocar el `URLSpec` del objeto `setApplicationWebRoot` y pase un valor de cadena que represente la raíz web de la aplicación.
   * Invocar el `URLSpec` del objeto `setContentRootURI` y pase un valor de cadena que especifique el valor de URI raíz del contenido. Asegúrese de que el diseño de formulario se encuentra en el URI raíz del contenido. Si no es así, el servicio de Forms genera una excepción. Para hacer referencia al repositorio, especifique `repository:///`.
   * Invocar el `URLSpec` del objeto `setTargetURL` y pase un valor de cadena que especifique el valor de la dirección URL de destino donde se publican los datos del formulario. Si define la dirección URL de destino en el diseño de formulario, puede pasar una cadena vacía. También puede especificar la dirección URL a la que se envía un formulario para realizar cálculos.

1. Adjuntar archivos al formulario

   * Cree un `java.util.HashMap` para almacenar archivos adjuntos usando su constructor.
   * Invocar el `java.util.HashMap` del objeto `put` para cada archivo que se adjuntará al formulario procesado. Pase los siguientes valores a este método:

      * Un valor de cadena que especifica el nombre del archivo adjunto, incluida la extensión del nombre de archivo
   * A `BLOB` objeto que contiene el archivo adjunto

   >[!NOTE]
   >
   >Repita este paso para cada archivo que desee adjuntar al formulario.

1. Representar un formulario PDF interactivo

   Invocar el `FormsService` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`.
   * A `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución. Este es un parámetro opcional y puede especificar `null` si no desea especificar opciones de tiempo de ejecución.
   * A `URLSpec` que contiene valores de URI necesarios para el servicio Forms.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un vacío `com.adobe.idp.services.holders.BLOBHolder` objeto que rellena el método . Se utiliza para almacenar el formulario de PDF procesado.
   * Un vacío `javax.xml.rpc.holders.LongHolder` objeto que rellena el método . (Este argumento almacenará el número de páginas del formulario).
   * Un vacío `javax.xml.rpc.holders.StringHolder` objeto que rellena el método . (Este argumento almacenará el valor de configuración regional).
   * Un vacío `com.adobe.idp.services.holders.FormsResultHolder` que contendrá los resultados de esta operación.

   La variable `renderPDFForm` rellena el `com.adobe.idp.services.holders.FormsResultHolder` objeto que se pasa como el último valor de argumento con un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un `FormResult` obteniendo el valor de `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value` miembro de datos.
   * Cree un `BLOB` objeto que contiene datos de formulario invocando la variable `FormsResult` del objeto `getOutputContent` método.
   * Obtenga el tipo de contenido de la variable `BLOB` invocando su `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasar el tipo de contenido de la variable `BLOB` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos del formulario en el explorador web del cliente invocando la variable `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Cree una matriz de bytes y rellénela invocando la variable `BLOB` del objeto `getBinaryData` método. Esta tarea asigna el contenido de la variable `FormsResult` a la matriz de bytes.
   * Invocar el `javax.servlet.http.HttpServletResponse` del objeto `write` método para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes a la `write` método.

**Escribir el flujo de datos del formulario en el explorador web del cliente**

Cuando el servicio Forms procesa un formulario, devuelve un flujo de datos de formulario que debe escribir en el explorador web del cliente. Cuando se escribe en el explorador web del cliente, el formulario es visible para el usuario.
