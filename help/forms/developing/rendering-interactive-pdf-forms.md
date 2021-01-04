---
title: Representación de PDF forms interactivos
seo-title: Representación de PDF forms interactivos
description: Utilice el servicio de Forms para procesar PDF forms interactivos en dispositivos cliente, normalmente exploradores Web, para recopilar información de los usuarios. Puede utilizar el servicio Forms para procesar formularios interactivos mediante la API de Java y la API de servicio Web.
seo-description: Utilice el servicio de Forms para procesar PDF forms interactivos en dispositivos cliente, normalmente exploradores Web, para recopilar información de los usuarios. Puede utilizar el servicio Forms para procesar formularios interactivos mediante la API de Java y la API de servicio Web.
uuid: df2a4dc8-f19e-49de-850f-85a204102631
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3cb307ec-9b7b-4f03-b860-48553ccee746
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '2514'
ht-degree: 0%

---


# Representación de PDF forms interactivos {#rendering-interactive-pdf-forms}

El servicio Forms procesa PDF forms interactivos en los dispositivos cliente, generalmente en los exploradores Web, para recopilar información de los usuarios. Una vez procesado un formulario interactivo, el usuario puede introducir datos en los campos del formulario y hacer clic en un botón de envío ubicado en el formulario para enviar la información al servicio Forms. Adobe Reader o Acrobat deben estar instalados en el equipo que aloja el navegador web del cliente para que un formulario PDF interactivo esté visible.

>[!NOTE]
>
>Antes de procesar un formulario con el servicio Forms, cree un diseño de formulario. Normalmente, un diseño de formulario se crea en Designer y se guarda como archivo XDP. Para obtener información sobre la creación de un diseño de formulario, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

**Solicitud de préstamo de muestra**

Se ha introducido una aplicación de préstamo de muestra para demostrar cómo el servicio de Forms utiliza formularios interactivos para recopilar información de los usuarios. Esta aplicación permite al usuario rellenar un formulario con los datos necesarios para garantizar un préstamo y, a continuación, enviar los datos al servicio de Forms. El siguiente diagrama muestra el flujo lógico de la aplicación de préstamo.

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
   <td><p>El servlet <code>GetLoanForm</code> de Java utiliza la API de cliente de servicio de Forms para procesar el formulario de préstamo en el navegador web del cliente. (Consulte <a href="#render-an-interactive-pdf-form-using-the-java-api">Representar un formulario PDF interactivo utilizando la API de Java</a>).</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Una vez que el usuario completa el formulario de préstamo y hace clic en el botón de envío, los datos se envían al servlet <code>HandleData</code> Java. (Consulte <i>"Formulario de préstamo"</i>.)</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>El servlet <code>HandleData</code> Java utiliza la API de cliente de servicio de Forms para procesar el envío del formulario y recuperar los datos del formulario. A continuación, los datos se almacenan en una base de datos empresarial. (Consulte <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">Administración de Forms</a> enviado).</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Se devuelve un formulario de confirmación al explorador Web. Los datos como el nombre y los apellidos del usuario se combinan con el formulario antes de procesarlo. (Consulte <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">Rellenado previo de Forms con diseños de posición variable</a>).</p></td>
  </tr>
 </tbody>
</table>

**Formulario de préstamo**

Este formulario de préstamo interactivo se procesa mediante el servlet Java `GetLoanForm` de la aplicación de préstamo de muestra.

![ri_ri_loanform](assets/ri_ri_loanform.png)

**Formulario de confirmación**

Este formulario se procesa mediante el servlet Java `HandleData` de la aplicación de préstamo de ejemplo.

![ri_ri_confirm](assets/ri_ri_confirm.png)

El servlet `HandleData` Java rellena previamente este formulario con el nombre y los apellidos del usuario, así como la cantidad. Una vez que el formulario se rellena previamente, se envía al explorador web del cliente. (Consulte [Rellenado previo de Forms con diseños de posición variable](/help/forms/developing/prepopulating-forms-flowable-layouts.md))

**Servlets de Java**

La aplicación de préstamo de muestra es un ejemplo de una aplicación de servicio de Forms que existe como servlet de Java. Un servlet de Java es un programa de Java que se ejecuta en un servidor de aplicaciones J2EE, como WebSphere, y contiene código de API de cliente de servicio de Forms.

El siguiente código muestra la sintaxis de un Servlet Java llamado GetLoanForm:

```java
     public class GetLoanForm extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

             }
```

Normalmente, no colocaría el código de API de cliente de servicio de Forms dentro de un método `doGet` o `doPost` de servlet de Java. Es mejor programar para colocar este código en una clase independiente, crear instancias de la clase desde el método `doPost` (o método `doGet`) y llamar a los métodos apropiados. Sin embargo, para la brevedad del código, los ejemplos de código de esta sección se mantienen al mínimo y los ejemplos de código se colocan en el método `doPost`.

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

**Resumen de los pasos**

Para procesar un formulario PDF interactivo, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Especifique los valores de URI.
1. Adjuntar archivos al formulario (opcional).
1. Representar un formulario PDF interactivo.
1. Escriba la secuencia de datos del formulario en el navegador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Forms Client**

Para poder realizar mediante programación una operación de API de cliente de servicio de Forms, debe crear un objeto de API de cliente de Forms. Si utiliza la API de Java, cree un objeto `FormsServiceClient`. Si utiliza la API de servicio Web de Forms, cree un objeto `FormsService`.

**Especificar valores de URI**

Puede especificar los valores de URI necesarios para que el servicio Forms procese un formulario. Se puede hacer referencia a un diseño de formulario guardado como parte de una aplicación de Forms mediante el valor URI raíz de contenido `repository:///`. Por ejemplo, piense en el siguiente diseño de formulario denominado *Loan.xdp* ubicado en una aplicación de Forms denominada *FormsApplication*:

![ri_ri_formRepository](assets/ri_ri_formrepository.png)

Para acceder a este diseño de formulario, especifique `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` como nombre del formulario (el primer parámetro pasado al método `renderPDFForm`) y `repository:///` como valor URI raíz del contenido.

>[!NOTE]
>
>Para obtener información sobre la creación de una aplicación de Forms mediante Workbench, consulte la [Ayuda de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

La ruta a un recurso ubicado en una aplicación de Forms es:

`Applications/Application-name/Application-version/Folder.../Filename`

Los siguientes valores muestran algunos ejemplos de valores URI:

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

Cuando se procesa un formulario interactivo, se pueden definir valores de URI como, por ejemplo, la URL de destinatario en la que se publican los datos del formulario. La dirección URL de destinatario se puede definir de una de las siguientes formas:

* En el botón Enviar mientras se diseña el diseño de formulario en Designer
* Mediante la API de cliente de servicio de Forms

Si la URL de destinatario está definida en el diseño de formulario, no la sobrescriba con la API de cliente de servicio de Forms. Es decir, si se establece la URL de destinatario mediante la API de Forms, se restablece la URL especificada en el diseño de formulario con la especificada mediante la API. Si desea enviar el formulario PDF a la dirección URL de destinatario especificada en el diseño de formulario, defina mediante programación la dirección URL de destinatario en una cadena vacía.

Si tiene un formulario que contiene un botón de envío y un botón de cálculo (con una secuencia de comandos correspondiente que se ejecuta en el servidor), puede definir mediante programación la dirección URL a la que se envía el formulario para ejecutar la secuencia de comandos. Utilice el botón de envío del diseño de formulario para especificar la dirección URL en la que se registran los datos del formulario. (Consulte [Cálculo de datos de formulario](/help/forms/developing/calculating-form-data.md).)

>[!NOTE]
>
>En lugar de especificar un valor de URL para hacer referencia a un archivo XDP, también puede pasar una instancia `com.adobe.idp.Document` al servicio de Forms. La instancia `com.adobe.idp.Document` contiene un diseño de formulario. (Consulte [Pasar Documentos al servicio de Forms](/help/forms/developing/passing-documents-forms-service.md)).

**Adjuntar archivos al formulario**

Puede adjuntar archivos a un formulario. Cuando se procesa un formulario PDF con archivos adjuntos, los usuarios pueden recuperar los archivos adjuntos en Acrobat mediante el panel de archivos adjuntos. Puede adjuntar diferentes tipos de archivo a un formulario, como un archivo de texto, o a un archivo binario, como un archivo JPG.

>[!NOTE]
>
>Adjuntar archivos adjuntos a un formulario es opcional.

**Representar un formulario PDF interactivo**

Para procesar un formulario, utilice un diseño de formulario creado en Designer y guardado como archivo XDP o PDF. Asimismo, puede procesar un formulario creado con Acrobat y guardado como archivo PDF. Para procesar un formulario PDF interactivo, invoque el método `FormsServiceClient` o `renderPDFForm2` del objeto `renderPDFForm`.

El `renderPDFForm` utiliza un objeto `URLSpec`. La raíz de contenido al archivo XDP se pasa al servicio de Forms mediante el método `URLSpec` del objeto `setContentRootURI`. El nombre del diseño de formulario ( `formQuery`) se pasa como un valor de parámetro independiente. Los dos valores se concatenan para obtener la referencia absoluta al diseño de formulario.

El método `renderPDFForm2` acepta una instancia `com.adobe.idp.Document` que contiene el documento XDP o PDF que se va a procesar.

>[!NOTE]
>
>La opción de tiempo de ejecución de PDF con etiquetas no se puede establecer si el documento de entrada es un documento PDF. Si el archivo de entrada es un archivo XDP, se puede establecer la opción PDF con etiquetas.

## Representar un formulario PDF interactivo mediante la API de Java {#render-an-interactive-pdf-form-using-the-java-api}

Representar un formulario PDF interactivo mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clases del proyecto Java.

1. Creación de un objeto de API de Forms Client

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `FormsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Especificar valores de URI

   * Cree un objeto `URLSpec` que almacene valores URI mediante su constructor.
   * Invoque el método `URLSpec` del objeto `setApplicationWebRoot` y pase un valor de cadena que represente la raíz web de la aplicación.
   * Invoque el método `URLSpec` del objeto `setContentRootURI` y pase un valor de cadena que especifique el valor de URI raíz del contenido. Asegúrese de que el diseño de formulario se encuentra en el URI raíz de contenido. Si no es así, el servicio Forms emite una excepción. Para hacer referencia al repositorio, especifique `repository:///`.
   * Invoque el método `URLSpec` del objeto `setTargetURL` y pase un valor de cadena que especifique el valor de la URL de destinatario al que se registran los datos del formulario. Si define la URL de destinatario en el diseño de formulario, puede pasar una cadena vacía. También puede especificar la dirección URL a la que se envía un formulario para realizar cálculos.

1. Adjuntar archivos al formulario

   * Cree un objeto `java.util.HashMap` para almacenar archivos adjuntos mediante su constructor.
   * Invoque el método `java.util.HashMap` del objeto `put` para cada archivo que se adjuntará al formulario procesado. Transfiera los siguientes valores a este método:

      * Un valor de cadena que especifica el nombre del archivo adjunto, incluida la extensión del nombre de archivo.
   * Un objeto `com.adobe.idp.Document` que contiene el archivo adjunto.

   >[!NOTE]
   >
   >Repita este paso para cada archivo que desee adjuntar al formulario. Este paso es opcional y puede pasar `null` si no desea enviar archivos adjuntos.

1. Representar un formulario PDF interactivo

   Invoque el método `FormsServiceClient` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un objeto `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un objeto vacío `com.adobe.idp.Document`.
   * Un objeto `PDFFormRenderSpec` que almacena opciones de tiempo de ejecución. Es un parámetro opcional y puede especificar `null` si no desea especificar opciones de tiempo de ejecución.
   * Un objeto `URLSpec` que contiene valores de URI necesarios para el servicio de Forms.
   * Objeto `java.util.HashMap` que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El método `renderPDFForm` devuelve un objeto `FormsResult` que contiene una secuencia de datos de formulario que debe escribirse en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un objeto `com.adobe.idp.Document` invocando el método `FormsResult` del objeto ‘s `getOutputContent`.
   * Obtenga el tipo de contenido del objeto `com.adobe.idp.Document` invocando su método `getContentType`.
   * Configure el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `com.adobe.idp.Document`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el método `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream`.
   * Cree un objeto `java.io.InputStream` invocando el método `com.adobe.idp.Document` del objeto `getInputStream`.
   * Cree una matriz de bytes y rellénela con la secuencia de datos del formulario invocando el método `InputStream` del objeto `read` y pasando la matriz de bytes como argumento.
   * Invoque el método `javax.servlet.ServletOutputStream` del objeto `write` para enviar la secuencia de datos del formulario al explorador Web del cliente. Pase la matriz de bytes al método `write`.

## Representar un formulario PDF interactivo mediante la API de servicio Web {#render-an-interactive-pdf-form-using-the-web-service-api}

Representar un formulario PDF interactivo mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases proxy de Java que consuman el WSDL del servicio de Forms.
   * Incluya las clases proxy de Java en la ruta de clases.

1. Creación de un objeto de API de Forms Client

   Cree un objeto `FormsService` y defina los valores de autenticación.

1. Especificar valores de URI

   * Cree un objeto `URLSpec` que almacene valores URI mediante su constructor.
   * Invoque el método `URLSpec` del objeto `setApplicationWebRoot` y pase un valor de cadena que represente la raíz web de la aplicación.
   * Invoque el método `URLSpec` del objeto `setContentRootURI` y pase un valor de cadena que especifique el valor de URI raíz del contenido. Asegúrese de que el diseño de formulario se encuentra en el URI raíz de contenido. Si no es así, el servicio Forms emite una excepción. Para hacer referencia al repositorio, especifique `repository:///`.
   * Invoque el método `URLSpec` del objeto `setTargetURL` y pase un valor de cadena que especifique el valor de la URL de destinatario al que se registran los datos del formulario. Si define la URL de destinatario en el diseño de formulario, puede pasar una cadena vacía. También puede especificar la dirección URL a la que se envía un formulario para realizar cálculos.

1. Adjuntar archivos al formulario

   * Cree un objeto `java.util.HashMap` para almacenar archivos adjuntos mediante su constructor.
   * Invoque el método `java.util.HashMap` del objeto `put` para cada archivo que se adjuntará al formulario procesado. Transfiera los siguientes valores a este método:

      * Un valor de cadena que especifica el nombre del archivo adjunto, incluida la extensión del nombre de archivo
   * Un objeto `BLOB` que contiene el archivo adjunto

   >[!NOTE]
   >
   >Repita este paso para cada archivo que desee adjuntar al formulario.

1. Representar un formulario PDF interactivo

   Invoque el método `FormsService` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un objeto `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`.
   * Un objeto `PDFFormRenderSpec` que almacena opciones de tiempo de ejecución. Es un parámetro opcional y puede especificar `null` si no desea especificar opciones de tiempo de ejecución.
   * Un objeto `URLSpec` que contiene valores de URI necesarios para el servicio de Forms.
   * Objeto `java.util.HashMap` que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un objeto vacío `com.adobe.idp.services.holders.BLOBHolder` que se rellena con el método. Se utiliza para almacenar el formulario PDF procesado.
   * Un objeto vacío `javax.xml.rpc.holders.LongHolder` que se rellena con el método. (Este argumento almacenará el número de páginas del formulario).
   * Un objeto vacío `javax.xml.rpc.holders.StringHolder` que se rellena con el método. (Este argumento almacenará el valor de configuración regional).
   * Un objeto vacío `com.adobe.idp.services.holders.FormsResultHolder` que contendrá los resultados de esta operación.

   El método `renderPDFForm` rellena el objeto `com.adobe.idp.services.holders.FormsResultHolder` que se pasa como el último valor de argumento con una secuencia de datos de formulario que debe escribirse en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un objeto `FormResult` obteniendo el valor del miembro de datos `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value`.
   * Cree un objeto `BLOB` que contenga datos de formulario invocando el método `FormsResult` del objeto `getOutputContent`.
   * Obtenga el tipo de contenido del objeto `BLOB` invocando su método `getContentType`.
   * Configure el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `BLOB`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el método `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream`.
   * Cree una matriz de bytes y rellénela invocando el método `BLOB` del objeto `getBinaryData`. Esta tarea asigna el contenido del objeto `FormsResult` a la matriz de bytes.
   * Invoque el método `javax.servlet.http.HttpServletResponse` del objeto `write` para enviar la secuencia de datos del formulario al explorador Web del cliente. Pase la matriz de bytes al método `write`.

**Escribir el flujo de datos del formulario en el navegador web del cliente**

Cuando el servicio Forms procesa un formulario, devuelve una secuencia de datos de formulario que debe escribir en el explorador web del cliente. Cuando se escribe en el navegador web del cliente, el formulario es visible para el usuario.
