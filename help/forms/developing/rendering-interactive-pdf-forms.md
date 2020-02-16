---
title: Representación de formularios PDF interactivos
seo-title: Representación de formularios PDF interactivos
description: nulo
seo-description: nulo
uuid: df2a4dc8-f19e-49de-850f-85a204102631
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3cb307ec-9b7b-4f03-b860-48553ccee746
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Representación de formularios PDF interactivos {#rendering-interactive-pdf-forms}

El servicio Forms procesa formularios PDF interactivos en dispositivos cliente, normalmente exploradores Web, para recopilar información de los usuarios. Una vez procesado un formulario interactivo, un usuario puede introducir datos en los campos del formulario y hacer clic en un botón de envío ubicado en el formulario para enviar información al servicio Forms. Adobe Reader o Acrobat deben estar instalados en el equipo que aloja el navegador web del cliente para que un formulario PDF interactivo esté visible.

>[!NOTE]
>
>Para poder procesar un formulario mediante el servicio Forms, cree un diseño de formulario. Normalmente, un diseño de formulario se crea en Designer y se guarda como archivo XDP. Para obtener información sobre la creación de un diseño de formulario, consulte [Diseñador](https://www.adobe.com/go/learn_aemforms_designer_63)de formularios.

**Solicitud de préstamo de muestra**

Se ha introducido una aplicación de préstamo de ejemplo para mostrar cómo el servicio Forms utiliza formularios interactivos para recopilar información de los usuarios. Esta aplicación permite al usuario rellenar un formulario con los datos necesarios para garantizar un préstamo y, a continuación, enviar los datos al servicio Forms. El siguiente diagrama muestra el flujo lógico de la aplicación de préstamo.

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
   <td><p>El servlet <code>GetLoanForm</code> Java se invoca desde una página HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>El servlet <code>GetLoanForm</code> Java utiliza la API del cliente de servicios de Forms para procesar el formulario de préstamo en el navegador web del cliente. (Consulte <a href="#render-an-interactive-pdf-form-using-the-java-api">Representación de un formulario PDF interactivo mediante la API</a>de Java).</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Una vez que el usuario completa el formulario de préstamo y hace clic en el botón de envío, los datos se envían al servlet de <code>HandleData</code> Java. (Consulte <i>"Formulario de préstamo"</i>.)</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>El servlet <code>HandleData</code> Java utiliza la API del cliente de servicios de Forms para procesar el envío del formulario y recuperar los datos del formulario. A continuación, los datos se almacenan en una base de datos empresarial. (Consulte <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">Gestión de formularios</a>enviados).</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Se devuelve un formulario de confirmación al explorador Web. Los datos como el nombre y los apellidos del usuario se combinan con el formulario antes de procesarlo. (Consulte <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">Rellenado previo de formularios con diseños</a>de posición variable).</p></td>
  </tr>
 </tbody>
</table>

**Formulario de préstamo**

Este formulario de préstamo interactivo se procesa mediante el servlet Java de la aplicación de préstamo de muestra `GetLoanForm` .

![ri_ri_loanform](assets/ri_ri_loanform.png)

**Formulario de confirmación**

Este formulario se procesa con el servlet Java de la aplicación de préstamo de ejemplo `HandleData` .

![ri_ri_confirm](assets/ri_ri_confirm.png)

El `HandleData` servlet Java rellena previamente este formulario con el nombre y los apellidos del usuario, así como la cantidad. Una vez que el formulario se rellena previamente, se envía al explorador web del cliente. (Consulte [Rellenado previo de formularios con diseños](/help/forms/developing/prepopulating-forms-flowable-layouts.md)de posición variable)

**Servlets de Java**

La aplicación de préstamo de ejemplo es un ejemplo de una aplicación de servicio Forms que existe como servlet Java. Un servlet Java es un programa Java que se ejecuta en un servidor de aplicaciones J2EE, como WebSphere, y contiene código de API del cliente de servicios de Forms.

El siguiente código muestra la sintaxis de un Servlet Java llamado GetLoanForm:

```as3
     public class GetLoanForm extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

             }
```

Normalmente, no se coloca el código de API de cliente de servicios de Forms dentro de un `doGet` `doPost` método o servlet de Java. Es mejor programar para colocar este código en una clase independiente, crear instancias de la clase desde el `doPost` método (o `doGet` método) y llamar a los métodos adecuados. Sin embargo, para la brevedad del código, los ejemplos de código de esta sección se mantienen al mínimo y los ejemplos de código se colocan en el `doPost` método.

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

**Resumen de los pasos**

Para procesar un formulario PDF interactivo, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de Forms Client.
1. Especifique los valores de URI.
1. Adjuntar archivos al formulario (opcional).
1. Representar un formulario PDF interactivo.
1. Escriba la secuencia de datos del formulario en el navegador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Forms Client**

Para poder realizar mediante programación una operación de API de cliente de servicios de Forms, debe crear un objeto de API de cliente de Forms. Si utiliza la API de Java, cree un `FormsServiceClient` objeto. Si utiliza la API de servicio web de Forms, cree un `FormsService` objeto.

**Especificar valores de URI**

Puede especificar los valores de URI que necesita el servicio Forms para procesar un formulario. Se puede hacer referencia a un diseño de formulario guardado como parte de una aplicación Forms mediante el valor URI raíz de contenido `repository:///`. Por ejemplo, piense en el siguiente diseño de formulario llamado *Loan.xdp* ubicado en una aplicación de formularios denominada *FormsApplication*:

![ri_ri_formRepository](assets/ri_ri_formrepository.png)

Para acceder a este diseño de formulario, especifique `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` como nombre del formulario (el primer parámetro que se pasa al `renderPDFForm` método) y `repository:///` como valor de URI raíz del contenido.

>[!NOTE]
>
>Para obtener información sobre la creación de una aplicación de Forms mediante Workbench, consulte la Ayuda [de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

La ruta a un recurso ubicado en una aplicación Forms es:

`Applications/Application-name/Application-version/Folder.../Filename`

Los siguientes valores muestran algunos ejemplos de valores URI:

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

Cuando se procesa un formulario interactivo, se pueden definir valores de URI como, por ejemplo, la dirección URL de destino en la que se publican los datos del formulario. La dirección URL de destino se puede definir de una de las siguientes formas:

* En el botón Enviar mientras se diseña el diseño de formulario en Designer
* Mediante la API de cliente de servicios de Forms

Si la dirección URL de destino está definida en el diseño de formulario, no la sobrescriba con la API del cliente del servicio Forms. Es decir, si se establece la dirección URL de destino mediante la API de Forms, la dirección URL especificada en el diseño de formulario se restablece en la especificada mediante la API. Si desea enviar el formulario PDF a la dirección URL de destino especificada en el diseño de formulario, defina mediante programación la dirección URL de destino en una cadena vacía.

Si tiene un formulario que contiene un botón de envío y un botón de cálculo (con una secuencia de comandos correspondiente que se ejecuta en el servidor), puede definir mediante programación la dirección URL a la que se envía el formulario para ejecutar la secuencia de comandos. Utilice el botón de envío del diseño de formulario para especificar la dirección URL en la que se registran los datos del formulario. (Consulte [Cálculo de datos](/help/forms/developing/calculating-form-data.md)de formulario.)

>[!NOTE]
>
>En lugar de especificar un valor de URL para hacer referencia a un archivo XDP, también puede pasar una `com.adobe.idp.Document` instancia al servicio Forms. La `com.adobe.idp.Document` instancia contiene un diseño de formulario. (Consulte [Pasar documentos al servicio](/help/forms/developing/passing-documents-forms-service.md)Forms).

**Adjuntar archivos al formulario**

Puede adjuntar archivos a un formulario. Cuando se procesa un formulario PDF con archivos adjuntos, los usuarios pueden recuperar los archivos adjuntos en Acrobat mediante el panel de archivos adjuntos. Puede adjuntar diferentes tipos de archivo a un formulario, como un archivo de texto, o a un archivo binario, como un archivo JPG.

>[!NOTE]
>
>Adjuntar archivos adjuntos a un formulario es opcional.

**Representar un formulario PDF interactivo**

Para procesar un formulario, utilice un diseño de formulario creado en Designer y guardado como archivo XDP o PDF. Asimismo, puede procesar un formulario creado con Acrobat y guardado como archivo PDF. Para procesar un formulario PDF interactivo, invoque el `FormsServiceClient` método o `renderPDFForm` método del `renderPDFForm2` objeto.

El `renderPDFForm` utiliza un `URLSpec` objeto. La raíz de contenido al archivo XDP se pasa al servicio Forms mediante el `URLSpec` método `setContentRootURI` del objeto. El nombre del diseño de formulario ( `formQuery`) se pasa como un valor de parámetro independiente. Los dos valores se concatenan para obtener la referencia absoluta al diseño de formulario.

El `renderPDFForm2` método acepta una `com.adobe.idp.Document` instancia que contiene el documento XDP o PDF que se va a procesar.

>[!NOTE]
>
>La opción de tiempo de ejecución de PDF con etiquetas no se puede establecer si el documento de entrada es un documento PDF. Si el archivo de entrada es un archivo XDP, se puede establecer la opción PDF con etiquetas.

## Representar un formulario PDF interactivo mediante la API de Java {#render-an-interactive-pdf-form-using-the-java-api}

Representar un formulario PDF interactivo mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clases del proyecto Java.

1. Creación de un objeto de API de Forms Client

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `FormsServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Especificar valores de URI

   * Cree un `URLSpec` objeto que almacene valores URI mediante su constructor.
   * Invoque el `URLSpec` método del `setApplicationWebRoot` objeto y pase un valor de cadena que represente la raíz web de la aplicación.
   * Invoque el `URLSpec` método del `setContentRootURI` objeto y pase un valor de cadena que especifique el valor de URI raíz del contenido. Asegúrese de que el diseño de formulario se encuentra en el URI raíz de contenido. De lo contrario, el servicio Forms genera una excepción. Para hacer referencia al repositorio, especifique `repository:///`.
   * Invoque el `URLSpec` método del `setTargetURL` objeto y pase un valor de cadena que especifique el valor de la dirección URL de destino al que se registran los datos del formulario. Si define la dirección URL de destino en el diseño de formulario, puede pasar una cadena vacía. También puede especificar la dirección URL a la que se envía un formulario para realizar cálculos.

1. Adjuntar archivos al formulario

   * Cree un `java.util.HashMap` objeto para almacenar archivos adjuntos mediante su constructor.
   * Invocar el `java.util.HashMap` método del `put` objeto para que cada archivo se adjunte al formulario procesado. Transfiera los siguientes valores a este método:

      * Un valor de cadena que especifica el nombre del archivo adjunto, incluida la extensión del nombre de archivo.
   * Un `com.adobe.idp.Document` objeto que contiene el archivo adjunto.
   >[!NOTE]
   >
   >Repita este paso para cada archivo que desee adjuntar al formulario. Este paso es opcional y puede pasar `null` si no desea enviar archivos adjuntos.

1. Representar un formulario PDF interactivo

   Invoque el `FormsServiceClient` método del `renderPDFForm` objeto y pase los valores siguientes:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un `com.adobe.idp.Document` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un `com.adobe.idp.Document` objeto vacío.
   * Un `PDFFormRenderSpec` objeto que almacena opciones de tiempo de ejecución. Se trata de un parámetro opcional que puede especificar `null` si no desea especificar opciones de tiempo de ejecución.
   * Un `URLSpec` objeto que contiene valores de URI necesarios para el servicio Forms.
   * Un `java.util.HashMap` objeto que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   El `renderPDFForm` método devuelve un `FormsResult` objeto que contiene una secuencia de datos de formulario que se debe escribir en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un `com.adobe.idp.Document` objeto invocando el `FormsResult` método ‘s `getOutputContent` .
   * Obtenga el tipo de contenido del `com.adobe.idp.Document` objeto invocando su `getContentType` método.
   * Defina el tipo de contenido del `javax.servlet.http.HttpServletResponse` objeto invocando su `setContentType` método y pasando el tipo de contenido del `com.adobe.idp.Document` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el `javax.servlet.http.HttpServletResponse` método `getOutputStream` del objeto.
   * Cree un `java.io.InputStream` objeto invocando el `com.adobe.idp.Document` método `getInputStream` del objeto.
   * Cree una matriz de bytes y rellénela con la secuencia de datos del formulario invocando el `InputStream` método del `read` objeto y pasando la matriz de bytes como argumento.
   * Invoque el `javax.servlet.ServletOutputStream` método del `write` objeto para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al `write` método .

## Representar un formulario PDF interactivo mediante la API de servicio web {#render-an-interactive-pdf-form-using-the-web-service-api}

Representar un formulario PDF interactivo mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases proxy de Java que consuman el WSDL del servicio Forms.
   * Incluya las clases proxy de Java en la ruta de clases.

1. Creación de un objeto de API de Forms Client

   Cree un `FormsService` objeto y defina los valores de autenticación.

1. Especificar valores de URI

   * Cree un `URLSpec` objeto que almacene valores URI mediante su constructor.
   * Invoque el `URLSpec` método del `setApplicationWebRoot` objeto y pase un valor de cadena que represente la raíz web de la aplicación.
   * Invoque el `URLSpec` método del `setContentRootURI` objeto y pase un valor de cadena que especifique el valor de URI raíz del contenido. Asegúrese de que el diseño de formulario se encuentra en el URI raíz de contenido. De lo contrario, el servicio Forms genera una excepción. Para hacer referencia al repositorio, especifique `repository:///`.
   * Invoque el `URLSpec` método del `setTargetURL` objeto y pase un valor de cadena que especifique el valor de la dirección URL de destino al que se registran los datos del formulario. Si define la dirección URL de destino en el diseño de formulario, puede pasar una cadena vacía. También puede especificar la dirección URL a la que se envía un formulario para realizar cálculos.

1. Adjuntar archivos al formulario

   * Cree un `java.util.HashMap` objeto para almacenar archivos adjuntos mediante su constructor.
   * Invocar el `java.util.HashMap` método del `put` objeto para que cada archivo se adjunte al formulario procesado. Transfiera los siguientes valores a este método:

      * Un valor de cadena que especifica el nombre del archivo adjunto, incluida la extensión del nombre de archivo
   * Un `BLOB` objeto que contiene el archivo adjunto
   >[!NOTE]
   >
   >Repita este paso para cada archivo que desee adjuntar al formulario.

1. Representar un formulario PDF interactivo

   Invoque el `FormsService` método del `renderPDFForm` objeto y pase los valores siguientes:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un `BLOB` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`.
   * Un `PDFFormRenderSpec` objeto que almacena opciones de tiempo de ejecución. Se trata de un parámetro opcional que puede especificar `null` si no desea especificar opciones de tiempo de ejecución.
   * Un `URLSpec` objeto que contiene valores de URI necesarios para el servicio Forms.
   * Un `java.util.HashMap` objeto que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Objeto vacío `com.adobe.idp.services.holders.BLOBHolder` que se rellena con el método . Se utiliza para almacenar el formulario PDF procesado.
   * Objeto vacío `javax.xml.rpc.holders.LongHolder` que se rellena con el método . (Este argumento almacenará el número de páginas del formulario).
   * Objeto vacío `javax.xml.rpc.holders.StringHolder` que se rellena con el método . (Este argumento almacenará el valor de configuración regional).
   * Un `com.adobe.idp.services.holders.FormsResultHolder` objeto vacío que contendrá los resultados de esta operación.
   El `renderPDFForm` método rellena el `com.adobe.idp.services.holders.FormsResultHolder` objeto que se pasa como el último valor de argumento con una secuencia de datos de formulario que se debe escribir en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un `FormResult` objeto obteniendo el valor del `com.adobe.idp.services.holders.FormsResultHolder` miembro de `value` datos del objeto.
   * Cree un `BLOB` objeto que contenga datos de formulario invocando el `FormsResult` método `getOutputContent` del objeto.
   * Obtenga el tipo de contenido del `BLOB` objeto invocando su `getContentType` método.
   * Defina el tipo de contenido del `javax.servlet.http.HttpServletResponse` objeto invocando su `setContentType` método y pasando el tipo de contenido del `BLOB` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el `javax.servlet.http.HttpServletResponse` método `getOutputStream` del objeto.
   * Cree una matriz de bytes y rellénela invocando el `BLOB` método `getBinaryData` del objeto. Esta tarea asigna el contenido del `FormsResult` objeto a la matriz de bytes.
   * Invoque el `javax.servlet.http.HttpServletResponse` método del `write` objeto para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al `write` método .

**Escribir el flujo de datos del formulario en el navegador web del cliente**

Cuando el servicio Forms procesa un formulario, devuelve una secuencia de datos de formulario que debe escribir en el explorador web del cliente. Cuando se escribe en el navegador web del cliente, el formulario es visible para el usuario.
