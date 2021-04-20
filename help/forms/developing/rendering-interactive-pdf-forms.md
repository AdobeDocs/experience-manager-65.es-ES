---
title: Renderización de PDF forms interactivos
seo-title: Renderización de PDF forms interactivos
description: Utilice el servicio Forms para procesar PDF forms interactivos en dispositivos cliente, normalmente exploradores web, para recopilar información de los usuarios. Puede utilizar el servicio Forms para procesar formularios interactivos mediante la API de Java y la API del servicio web.
seo-description: Utilice el servicio Forms para procesar PDF forms interactivos en dispositivos cliente, normalmente exploradores web, para recopilar información de los usuarios. Puede utilizar el servicio Forms para procesar formularios interactivos mediante la API de Java y la API del servicio web.
uuid: df2a4dc8-f19e-49de-850f-85a204102631
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3cb307ec-9b7b-4f03-b860-48553ccee746
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2529'
ht-degree: 0%

---


# Representación de PDF forms interactivos {#rendering-interactive-pdf-forms}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

El servicio Forms procesa PDF forms interactivos en dispositivos cliente, normalmente exploradores web, para recopilar información de los usuarios. Una vez procesado un formulario interactivo, el usuario puede introducir datos en los campos del formulario y hacer clic en un botón de envío ubicado en el formulario para enviar información al servicio de Forms. Adobe Reader o Acrobat deben estar instalados en el equipo que aloje el explorador web del cliente para que pueda verse un formulario PDF interactivo.

>[!NOTE]
>
>Para poder procesar un formulario con el servicio Forms, debe crear un diseño de formulario. Normalmente, un diseño de formulario se crea en Designer y se guarda como archivo XDP. Para obtener información sobre la creación de un diseño de formulario, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

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
   <td><p>El servlet Java <code>GetLoanForm</code> se invoca desde una página HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>El <code>GetLoanForm</code> servlet Java utiliza la API de cliente de servicio de Forms para procesar el formulario de préstamo en el explorador web del cliente. (Consulte <a href="#render-an-interactive-pdf-form-using-the-java-api">Representar un formulario PDF interactivo utilizando la API de Java</a>).</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Una vez que el usuario rellena el formulario de préstamo y hace clic en el botón de envío, los datos se envían al servlet Java <code>HandleData</code>. (Consulte <i>"Loan form"</i>).</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>El <code>HandleData</code> servlet Java utiliza la API de cliente de servicio de Forms para procesar el envío del formulario y recuperar los datos del formulario. A continuación, los datos se almacenan en una base de datos empresarial. (Consulte <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">Gestión de Forms enviado</a>).</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Se devuelve un formulario de confirmación al explorador web. Los datos, como el nombre y los apellidos del usuario, se combinan con el formulario antes de procesarse. (Consulte <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">Rellenado previo de Forms con diseños de posición variable</a>).</p></td>
  </tr>
 </tbody>
</table>

**Formulario de préstamo**

Este formulario de préstamo interactivo lo representa el `GetLoanForm` servlet Java de la aplicación de préstamos de ejemplo.

![ri_ri_loanform](assets/ri_ri_loanform.png)

**Formulario de confirmación**

Este formulario se procesa mediante el servlet Java `HandleData` de la aplicación de préstamos de ejemplo.

![ri_ri_confirm](assets/ri_ri_confirm.png)

El `HandleData` servlet Java rellena previamente este formulario con el nombre y los apellidos del usuario, así como la cantidad. Una vez que el formulario se rellena previamente, se envía al explorador web del cliente. (Consulte [Rellenado previo de Forms con diseños de posición variable](/help/forms/developing/prepopulating-forms-flowable-layouts.md))

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

Normalmente, no colocaría el código de API de cliente de servicio de Forms dentro de los métodos `doGet` o `doPost` de un servlet Java. Es mejor programar el colocar este código dentro de una clase independiente, crear una instancia de la clase desde el método `doPost` (o el método `doGet`) y llamar a los métodos adecuados. Sin embargo, para la brevedad del código, los ejemplos de código de esta sección se reducen al mínimo y los ejemplos de código se colocan en el método `doPost` .

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

**Resumen de los pasos**

Para procesar un formulario PDF interactivo, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Especifique valores de URI.
1. Adjuntar archivos al formulario (opcional).
1. Representar un formulario PDF interactivo.
1. Escriba el flujo de datos del formulario en el explorador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de cliente de Forms**

Para poder realizar una operación de API de cliente de servicio de Forms mediante programación, debe crear un objeto de API de cliente de Forms. Si utiliza la API de Java, cree un objeto `FormsServiceClient`. Si utiliza la API de servicio web de Forms, cree un objeto `FormsService`.

**Especificar valores de URI**

Puede especificar los valores de URI que requiere el servicio Forms para procesar un formulario. Se puede hacer referencia a un diseño de formulario guardado como parte de una aplicación de Forms mediante el valor de URI raíz de contenido `repository:///`. Por ejemplo, considere el siguiente diseño de formulario denominado *Loan.xdp* ubicado dentro de una aplicación de Forms denominada *FormsApplication*:

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

Para acceder a este diseño de formulario, especifique `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` como nombre del formulario (el primer parámetro pasado al método `renderPDFForm`) y `repository:///` como valor de URI raíz del contenido.

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

Si la dirección URL de destino está definida en el diseño de formulario, no la anule con la API de cliente del servicio de Forms. Es decir, si se define la dirección URL de destino mediante la API de Forms, se restablece la dirección URL especificada en el diseño de formulario en la especificada mediante la API. Si desea enviar el formulario PDF a la dirección URL de destino especificada en el diseño de formulario, defina programáticamente la dirección URL de destino como una cadena vacía.

Si tiene un formulario que contiene un botón de envío y un botón de cálculo (con una secuencia de comandos correspondiente que se ejecuta en el servidor), puede definir mediante programación la dirección URL a la que se envía el formulario para ejecutar la secuencia de comandos. Utilice el botón de envío del diseño de formulario para especificar la dirección URL donde se publican los datos del formulario. (Consulte [Cálculo de datos del formulario](/help/forms/developing/calculating-form-data.md)).

>[!NOTE]
>
>En lugar de especificar un valor de URL para hacer referencia a un archivo XDP, también puede pasar una instancia `com.adobe.idp.Document` al servicio Forms. La instancia `com.adobe.idp.Document` contiene un diseño de formulario. (Consulte [Pasar documentos al servicio de Forms](/help/forms/developing/passing-documents-forms-service.md)).

**Adjuntar archivos al formulario**

Puede adjuntar archivos a un formulario. Cuando se procesa un formulario PDF con archivos adjuntos, los usuarios pueden recuperar los archivos adjuntos en Acrobat mediante el panel de archivos adjuntos. Puede adjuntar distintos tipos de archivo a un formulario, como un archivo de texto, o a un archivo binario, como un archivo JPG.

>[!NOTE]
>
>Adjuntar archivos adjuntos a un formulario es opcional.

**Representar un formulario PDF interactivo**

Para procesar un formulario, utilice un diseño de formulario creado en Designer y guardado como archivo XDP o PDF. Asimismo, puede procesar un formulario creado con Acrobat y guardado como archivo PDF. Para procesar un formulario PDF interactivo, invoque el método `FormsServiceClient` o `renderPDFForm2` del objeto `renderPDFForm`.

El `renderPDFForm` utiliza un objeto `URLSpec`. La raíz de contenido al archivo XDP se pasa al servicio Forms mediante el método `URLSpec` del objeto `setContentRootURI`. El nombre del diseño de formulario ( `formQuery`) se pasa como un valor de parámetro independiente. Los dos valores se concatenan para obtener la referencia absoluta al diseño de formulario.

El método `renderPDFForm2` acepta una instancia `com.adobe.idp.Document` que contiene el documento XDP o PDF que se va a procesar.

>[!NOTE]
>
>La opción etiquetada en tiempo de ejecución de PDF no se puede establecer si el documento de entrada es un documento PDF. Si el archivo de entrada es un archivo XDP, se puede configurar la opción PDF con etiquetas.

## Representar un formulario PDF interactivo mediante la API de Java {#render-an-interactive-pdf-form-using-the-java-api}

Representar un formulario PDF interactivo utilizando la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-forms-client.jar, en la ruta de clase de su proyecto Java.

1. Creación de un objeto de API de cliente de Forms

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `FormsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Especificar valores de URI

   * Cree un objeto `URLSpec` que almacene valores de URI usando su constructor.
   * Invoque el método `URLSpec` del objeto `setApplicationWebRoot` y pase un valor de cadena que represente la raíz web de la aplicación.
   * Invoque el método `URLSpec` del objeto `setContentRootURI` y pase un valor de cadena que especifique el valor de URI raíz del contenido. Asegúrese de que el diseño de formulario se encuentra en el URI raíz del contenido. Si no es así, el servicio de Forms genera una excepción. Para hacer referencia al repositorio, especifique `repository:///`.
   * Invoque el método `URLSpec` del objeto `setTargetURL` y pase un valor de cadena que especifique el valor de la dirección URL de destino donde se registran los datos del formulario. Si define la dirección URL de destino en el diseño de formulario, puede pasar una cadena vacía. También puede especificar la dirección URL a la que se envía un formulario para realizar cálculos.

1. Adjuntar archivos al formulario

   * Cree un objeto `java.util.HashMap` para almacenar archivos adjuntos usando su constructor.
   * Invoque el método `java.util.HashMap` del objeto `put` para cada archivo que se adjuntará al formulario procesado. Pase los siguientes valores a este método:

      * Un valor de cadena que especifica el nombre del archivo adjunto, incluida la extensión de nombre de archivo.
   * Un objeto `com.adobe.idp.Document` que contiene el archivo adjunto.

   >[!NOTE]
   >
   >Repita este paso para cada archivo que desee adjuntar al formulario. Este paso es opcional y puede pasar `null` si no desea enviar archivos adjuntos.

1. Representar un formulario PDF interactivo

   Invoque el método `FormsServiceClient` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un objeto `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un objeto `com.adobe.idp.Document` vacío.
   * Un objeto `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución. Se trata de un parámetro opcional y puede especificar `null` si no desea especificar opciones en tiempo de ejecución.
   * Un objeto `URLSpec` que contiene valores de URI necesarios para el servicio Forms.
   * Un objeto `java.util.HashMap` que almacena archivos adjuntos. Se trata de un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El método `renderPDFForm` devuelve un objeto `FormsResult` que contiene un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un objeto `com.adobe.idp.Document` invocando el método `FormsResult` del objeto ‘s `getOutputContent`.
   * Obtenga el tipo de contenido del objeto `com.adobe.idp.Document` invocando su método `getContentType`.
   * Establezca el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `com.adobe.idp.Document`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se utilice para escribir el flujo de datos del formulario en el explorador web del cliente invocando el método `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream`.
   * Cree un objeto `java.io.InputStream` invocando el método `com.adobe.idp.Document` del objeto `getInputStream`.
   * Cree una matriz de bytes y rellénela con la secuencia de datos del formulario invocando el método `InputStream` del objeto `read` y pasando la matriz de bytes como argumento.
   * Invoque el método `javax.servlet.ServletOutputStream` del objeto `write` para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

## Representar un formulario PDF interactivo mediante la API de servicio web {#render-an-interactive-pdf-form-using-the-web-service-api}

Representar un formulario PDF interactivo mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases proxy de Java en la ruta de clase.

1. Creación de un objeto de API de cliente de Forms

   Cree un objeto `FormsService` y establezca valores de autenticación.

1. Especificar valores de URI

   * Cree un objeto `URLSpec` que almacene valores de URI usando su constructor.
   * Invoque el método `URLSpec` del objeto `setApplicationWebRoot` y pase un valor de cadena que represente la raíz web de la aplicación.
   * Invoque el método `URLSpec` del objeto `setContentRootURI` y pase un valor de cadena que especifique el valor de URI raíz del contenido. Asegúrese de que el diseño de formulario se encuentra en el URI raíz del contenido. Si no es así, el servicio de Forms genera una excepción. Para hacer referencia al repositorio, especifique `repository:///`.
   * Invoque el método `URLSpec` del objeto `setTargetURL` y pase un valor de cadena que especifique el valor de la dirección URL de destino donde se registran los datos del formulario. Si define la dirección URL de destino en el diseño de formulario, puede pasar una cadena vacía. También puede especificar la dirección URL a la que se envía un formulario para realizar cálculos.

1. Adjuntar archivos al formulario

   * Cree un objeto `java.util.HashMap` para almacenar archivos adjuntos usando su constructor.
   * Invoque el método `java.util.HashMap` del objeto `put` para cada archivo que se adjuntará al formulario procesado. Pase los siguientes valores a este método:

      * Un valor de cadena que especifica el nombre del archivo adjunto, incluida la extensión del nombre de archivo
   * Un objeto `BLOB` que contiene el archivo adjunto

   >[!NOTE]
   >
   >Repita este paso para cada archivo que desee adjuntar al formulario.

1. Representar un formulario PDF interactivo

   Invoque el método `FormsService` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un objeto `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`.
   * Un objeto `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución. Se trata de un parámetro opcional y puede especificar `null` si no desea especificar opciones en tiempo de ejecución.
   * Un objeto `URLSpec` que contiene valores de URI necesarios para el servicio Forms.
   * Un objeto `java.util.HashMap` que almacena archivos adjuntos. Se trata de un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un objeto `com.adobe.idp.services.holders.BLOBHolder` vacío que se rellena con el método . Se utiliza para almacenar el formulario PDF procesado.
   * Un objeto `javax.xml.rpc.holders.LongHolder` vacío que se rellena con el método . (Este argumento almacenará el número de páginas del formulario).
   * Un objeto `javax.xml.rpc.holders.StringHolder` vacío que se rellena con el método . (Este argumento almacenará el valor de configuración regional).
   * Un objeto `com.adobe.idp.services.holders.FormsResultHolder` vacío que contendrá los resultados de esta operación.

   El método `renderPDFForm` rellena el objeto `com.adobe.idp.services.holders.FormsResultHolder` que se pasa como el último valor de argumento con un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un objeto `FormResult` obteniendo el valor del miembro de datos `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value`.
   * Cree un objeto `BLOB` que contenga datos de formulario invocando el método `FormsResult` del objeto `getOutputContent`.
   * Obtenga el tipo de contenido del objeto `BLOB` invocando su método `getContentType`.
   * Establezca el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `BLOB`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se utilice para escribir el flujo de datos del formulario en el explorador web del cliente invocando el método `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream`.
   * Cree una matriz de bytes y rellénela invocando el método `BLOB` del objeto `getBinaryData`. Esta tarea asigna el contenido del objeto `FormsResult` a la matriz de bytes.
   * Invoque el método `javax.servlet.http.HttpServletResponse` del objeto `write` para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

**Escribir el flujo de datos del formulario en el explorador web del cliente**

Cuando el servicio Forms procesa un formulario, devuelve un flujo de datos de formulario que debe escribir en el explorador web del cliente. Cuando se escribe en el explorador web del cliente, el formulario es visible para el usuario.
