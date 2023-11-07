---
title: Procesar formularios PDF interactivos
description: Utilice el servicio Forms para representar PDF forms interactivos en dispositivos cliente, normalmente exploradores web, para recopilar información de los usuarios. Puede utilizar el servicio Forms para procesar formularios interactivos mediante la API de Java y la API de servicio web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: d9f32939-c2c0-4531-b15e-f63941c289e3
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2478'
ht-degree: 1%

---

# Procesar formularios PDF interactivos {#rendering-interactive-pdf-forms}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

El servicio Forms procesa PDF forms interactivos en dispositivos cliente, normalmente exploradores web, para recopilar información de los usuarios. Una vez procesado un formulario interactivo, un usuario puede introducir datos en los campos de formulario y hacer clic en un botón de envío ubicado en el formulario para enviar información de vuelta al servicio de Forms. Adobe Reader o Acrobat deben estar instalados en el equipo que aloja el explorador web del cliente para que un formulario de PDF interactivo sea visible.

>[!NOTE]
>
>Para poder procesar un formulario mediante el servicio Forms, cree un diseño de formulario. Normalmente, se crea un diseño de formulario en Designer y se guarda como archivo XDP. Para obtener información sobre la creación de un diseño de formulario, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

**Ejemplo de solicitud de préstamo**

Se presenta una aplicación de préstamo de ejemplo para demostrar cómo el servicio Forms utiliza formularios interactivos para recopilar información de los usuarios. Esta aplicación permite al usuario rellenar un formulario con los datos necesarios para obtener un préstamo y, a continuación, enviar datos al servicio de Forms. El diagrama siguiente muestra el flujo lógico de la aplicación del préstamo.

![ri_ri_finsrv_loanapp_v1](assets/ri_ri_finsrv_loanapp_v1.png)

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
   <td><p>El <code>GetLoanForm</code> El servlet Java se invoca desde una página de HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>El <code>GetLoanForm</code> Java Servlet utiliza la API del cliente del servicio de Forms para procesar el formulario de préstamo en el explorador web del cliente. (Consulte <a href="#render-an-interactive-pdf-form-using-the-java-api">Procesar un formulario interactivo de PDF mediante la API de Java</a>.)</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Una vez que el usuario rellena el formulario de préstamo y hace clic en el botón Enviar, los datos se envían al <code>HandleData</code> Servlet Java. (Consulte <i>"Formulario de préstamo"</i>.)</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>El <code>HandleData</code> Java Servlet utiliza la API de cliente del servicio Forms para procesar el envío del formulario y recuperar los datos del formulario. A continuación, los datos se almacenan en una base de datos empresarial. (Consulte <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">Gestión de Forms enviados</a>.)</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Se devuelve un formulario de confirmación al explorador web. Los datos como el nombre y los apellidos del usuario se combinan con el formulario antes de procesarse. (Consulte <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">Rellenado previo de Forms con diseños flexibles</a>.)</p></td>
  </tr>
 </tbody>
</table>

**Formulario de préstamo**

Este formulario de préstamo interactivo lo procesa el administrador de la solicitud de préstamo de ejemplo `GetLoanForm` Servlet Java.

![ri_ri_loanform](assets/ri_ri_loanform.png)

**Formulario de confirmación**

Este formulario lo procesa el administrador de la solicitud de préstamo de ejemplo `HandleData` Servlet Java.

![ri_ri_confirm](assets/ri_ri_confirm.png)

El `HandleData` Java Servlet rellena previamente este formulario con el nombre y los apellidos del usuario y la cantidad. Una vez rellenado previamente el formulario, se envía al explorador web del cliente. (Consulte [Rellenado previo de Forms con diseños flexibles](/help/forms/developing/prepopulating-forms-flowable-layouts.md))

**Servlets Java**

La aplicación de préstamo de ejemplo es un ejemplo de una aplicación de servicio de Forms que existe como servlet Java. Un servlet Java es un programa Java que se ejecuta en un servidor de aplicaciones J2EE, como WebSphere, y contiene el código de API del cliente del servicio Forms.

El siguiente código muestra la sintaxis de un servlet Java denominado GetLoanForm:

```java
     public class GetLoanForm extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

             }
```

Normalmente, no colocaría el código de la API del cliente del servicio de Forms dentro de un servidor Java `doGet` o `doPost` método. Se recomienda colocar este código en una clase independiente, crear instancias de la clase desde dentro de `doPost` método (o `doGet` método) y llame a los métodos adecuados. Sin embargo, para que el código sea más breve, los ejemplos de código de esta sección se mantienen al mínimo y los ejemplos de código se colocan en el `doPost` método.

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

**Resumen de los pasos**

Para procesar un formulario de PDF interactivo, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Especifique los valores de URI.
1. Adjuntar archivos al formulario (opcional).
1. Procesar un formulario interactivo de PDF.
1. Escriba el flujo de datos del formulario en el explorador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API de cliente de Forms**

Para poder realizar mediante programación una operación de la API de cliente del servicio de Forms, debe crear un objeto de la API de cliente de Forms. Si utiliza la API de Java, cree un `FormsServiceClient` objeto. Si utiliza la API del servicio web de Forms, cree un `FormsService` objeto.

**Especificar valores de URI**

Puede especificar los valores de URI que requiere el servicio Forms para procesar un formulario. Se puede hacer referencia a un diseño de formulario que se guarda como parte de una aplicación de Forms mediante el valor URI de raíz de contenido `repository:///`. Por ejemplo, considere el siguiente diseño de formulario denominado *Loan.xdp* ubicado en una aplicación de Forms denominada *FormsApplication*:

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

Para acceder a este diseño de formulario, especifique `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` como nombre del formulario (el primer parámetro que se pasa a la variable `renderPDFForm` método) y `repository:///` como el valor URI de la raíz de contenido.

>[!NOTE]
>
>Para obtener información sobre la creación de una aplicación de Forms mediante Workbench, consulte [Ayuda de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

La ruta a un recurso en una aplicación de Forms es:

`Applications/Application-name/Application-version/Folder.../Filename`

Los siguientes valores muestran algunos ejemplos de valores de URI:

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

Cuando procesa un formulario interactivo, puede definir valores de URI como la dirección URL de destino donde se publican los datos del formulario. La dirección URL de destino se puede definir de una de las siguientes maneras:

* Haga clic en el botón Enviar mientras diseña el diseño de formulario en Designer
* Mediante la API de cliente del servicio de Forms

Si la dirección URL de destino se define dentro del diseño de formulario, no la anule con la API de cliente del servicio de Forms. Es decir, al establecer la dirección URL de destino mediante la API de Forms, se restablece la dirección URL especificada en el diseño de formulario a la especificada mediante la API. Si desea enviar el formulario de PDF a la URL de destino especificada en el diseño de formulario, establezca mediante programación la URL de destino en una cadena vacía.

Si tiene un formulario que contiene un botón de envío y un botón de cálculo (con una secuencia de comandos correspondiente que se ejecuta en el servidor), puede definir mediante programación la dirección URL a la que se envía el formulario para ejecutar la secuencia de comandos. Utilice el botón de envío del diseño de formulario para especificar la dirección URL a la que se publican los datos del formulario. (Consulte [Calcular datos de formulario](/help/forms/developing/calculating-form-data.md).)

>[!NOTE]
>
>En lugar de especificar un valor de URL para hacer referencia a un archivo XDP, también puede pasar un `com.adobe.idp.Document` al servicio Forms. El `com.adobe.idp.Document` La instancia de contiene un diseño de formulario. (Consulte [Pasar documentos al servicio de Forms](/help/forms/developing/passing-documents-forms-service.md).)

**Adjuntar archivos al formulario**

Puede adjuntar archivos a un formulario. Cuando procesa un formulario de PDF con archivos adjuntos, los usuarios pueden recuperar los archivos adjuntos en Acrobat mediante el panel de archivos adjuntos. Puede adjuntar distintos tipos de archivo a un formulario, como un archivo de texto, o a un archivo binario, como un archivo JPG.

>[!NOTE]
>
>Adjuntar archivos adjuntos a un formulario es opcional.

**Procesar un formulario interactivo de PDF**

Para procesar un formulario, utilice un diseño de formulario creado en Designer y guardado como archivo XDP o de PDF. Además, puede procesar un formulario creado con Acrobat y guardado como archivo de PDF. Para procesar un formulario de PDF interactivo, invoque el `FormsServiceClient` del objeto `renderPDFForm` método o `renderPDFForm2` método.

El `renderPDFForm` utiliza un `URLSpec` objeto. La raíz de contenido del archivo XDP se pasa al servicio de Forms mediante el `URLSpec` del objeto `setContentRootURI` método. El nombre del diseño del formulario ( `formQuery`) se pasa como un valor de parámetro independiente. Los dos valores se concatenan para obtener la referencia absoluta al diseño de formulario.

El `renderPDFForm2` El método acepta un `com.adobe.idp.Document` que contiene el documento XDP o de PDF que se va a procesar.

>[!NOTE]
>
>La opción de tiempo de ejecución del PDF etiquetado no se puede establecer si el documento de entrada es un documento del PDF. Si el archivo de entrada es un archivo XDP, se puede establecer la opción de PDF etiquetado.

## Procesar un formulario interactivo de PDF mediante la API de Java {#render-an-interactive-pdf-form-using-the-java-api}

Procesar un formulario interactivo de PDF mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clase del proyecto Java.

1. Crear un objeto de API de cliente de Forms

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `FormsServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Especificar valores de URI

   * Crear un `URLSpec` que almacena los valores de URI mediante su constructor.
   * Invoque el `URLSpec` del objeto `setApplicationWebRoot` y pasar un valor de cadena que represente la raíz web de la aplicación.
   * Invoque el `URLSpec` del objeto `setContentRootURI` y pasan un valor de cadena que especifica el valor de URI de la raíz de contenido. Asegúrese de que el diseño del formulario esté en el URI raíz del contenido. Si no es así, el servicio Forms genera una excepción. Para hacer referencia al repositorio, especifique `repository:///`.
   * Invoque el `URLSpec` del objeto `setTargetURL` y pasan un valor de cadena que especifica el valor de la dirección URL de destino donde se publican los datos del formulario. Si define la dirección URL de destino en el diseño de formulario, puede pasar una cadena vacía. También puede especificar la dirección URL a la que se envía un formulario para realizar cálculos.

1. Adjuntar archivos al formulario

   * Crear un `java.util.HashMap` para almacenar los archivos adjuntos mediante su constructor.
   * Invoque el `java.util.HashMap` del objeto `put` para que cada archivo se adjunte al formulario procesado. Pase los siguientes valores a este método:

      * Valor de cadena que especifica el nombre del archivo adjunto, incluida la extensión del nombre de archivo.

   * A `com.adobe.idp.Document` que contiene el archivo adjunto.

   >[!NOTE]
   >
   >Repita este paso para cada archivo que desee adjuntar al formulario. Este paso es opcional y puede pasar `null` si no desea enviar archivos adjuntos.

1. Procesar un formulario interactivo de PDF

   Invoque el `FormsServiceClient` del objeto `renderPDFForm` y pasar los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta de acceso completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un vacío `com.adobe.idp.Document` objeto.
   * A `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución. Este es un parámetro opcional y puede especificar `null` si no desea especificar opciones en tiempo de ejecución.
   * A `URLSpec` que contiene valores de URI requeridos por el servicio de Forms.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El `renderPDFForm` El método devuelve un valor `FormsResult` que contiene un flujo de datos de formulario que debe escribirse en el explorador web cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Crear un `com.adobe.idp.Document` invocando el objeto de `FormsResult` del objeto `getOutputContent` método.
   * Obtenga el tipo de contenido del `com.adobe.idp.Document` invocando su objeto `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasando el tipo de contenido del `com.adobe.idp.Document` objeto.
   * Crear un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos de formulario en el explorador web del cliente invocando el `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Crear un `java.io.InputStream` invocando el objeto de `com.adobe.idp.Document` del objeto `getInputStream` método.
   * Cree una matriz de bytes y rellénela con el flujo de datos de formulario invocando el método `InputStream` del objeto `read` y pasando la matriz de bytes como argumento.
   * Invoque el `javax.servlet.ServletOutputStream` del objeto `write` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes a `write` método.

## Procesar un formulario interactivo de PDF mediante la API de servicio web {#render-an-interactive-pdf-form-using-the-web-service-api}

Procesar un formulario interactivo de PDF mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases de proxy Java en la ruta de clase.

1. Crear un objeto de API de cliente de Forms

   Crear un `FormsService` y establezca los valores de autenticación.

1. Especificar valores de URI

   * Crear un `URLSpec` que almacena los valores de URI mediante su constructor.
   * Invoque el `URLSpec` del objeto `setApplicationWebRoot` y pasar un valor de cadena que represente la raíz web de la aplicación.
   * Invoque el `URLSpec` del objeto `setContentRootURI` y pasan un valor de cadena que especifica el valor de URI de la raíz de contenido. Asegúrese de que el diseño del formulario esté en el URI raíz del contenido. Si no es así, el servicio Forms genera una excepción. Para hacer referencia al repositorio, especifique `repository:///`.
   * Invoque el `URLSpec` del objeto `setTargetURL` y pasan un valor de cadena que especifica el valor de la dirección URL de destino donde se publican los datos del formulario. Si define la dirección URL de destino en el diseño de formulario, puede pasar una cadena vacía. También puede especificar la dirección URL a la que se envía un formulario para realizar cálculos.

1. Adjuntar archivos al formulario

   * Crear un `java.util.HashMap` para almacenar los archivos adjuntos mediante su constructor.
   * Invoque el `java.util.HashMap` del objeto `put` para que cada archivo se adjunte al formulario procesado. Pase los siguientes valores a este método:

      * Valor de cadena que especifica el nombre del archivo adjunto, incluida la extensión del nombre de archivo

   * A `BLOB` objeto que contiene el archivo adjunto

   >[!NOTE]
   >
   >Repita este paso para cada archivo que desee adjuntar al formulario.

1. Procesar un formulario interactivo de PDF

   Invoque el `FormsService` del objeto `renderPDFForm` y pasar los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta de acceso completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar los datos, apruebe `null`.
   * A `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución. Este es un parámetro opcional y puede especificar `null` si no desea especificar opciones en tiempo de ejecución.
   * A `URLSpec` que contiene valores de URI requeridos por el servicio de Forms.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un vacío `com.adobe.idp.services.holders.BLOBHolder` objeto que rellena el método. Se utiliza para almacenar el formulario de PDF procesado.
   * Un vacío `javax.xml.rpc.holders.LongHolder` objeto que rellena el método. (Este argumento almacenará el número de páginas del formulario).
   * Un vacío `javax.xml.rpc.holders.StringHolder` objeto que rellena el método. (Este argumento almacenará el valor de configuración regional.)
   * Un vacío `com.adobe.idp.services.holders.FormsResultHolder` que contendrá los resultados de esta operación.

   El `renderPDFForm` rellena el método `com.adobe.idp.services.holders.FormsResultHolder` que se pasa como el último valor de argumento con un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Crear un `FormResult` al obtener el valor de la variable `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value` miembro de datos.
   * Crear un `BLOB` que contiene datos de formulario invocando el `FormsResult` del objeto `getOutputContent` método.
   * Obtenga el tipo de contenido del `BLOB` invocando su objeto `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasando el tipo de contenido del `BLOB` objeto.
   * Crear un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos de formulario en el explorador web del cliente invocando el `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Cree una matriz de bytes y rellénela invocando el método `BLOB` del objeto `getBinaryData` método. Esta tarea asigna el contenido del `FormsResult` a la matriz de bytes.
   * Invoque el `javax.servlet.http.HttpServletResponse` del objeto `write` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes a `write` método.

**Escribir el flujo de datos del formulario en el explorador web del cliente**

Cuando el servicio Forms procesa un formulario, devuelve un flujo de datos de formulario que debe escribir en el explorador web del cliente. Cuando se escribe en el explorador web del cliente, el formulario es visible para el usuario.
