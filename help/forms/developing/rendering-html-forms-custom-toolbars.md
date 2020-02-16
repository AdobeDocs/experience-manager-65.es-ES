---
title: Representación de formularios HTML con barras de herramientas personalizadas
seo-title: Representación de formularios HTML con barras de herramientas personalizadas
description: nulo
seo-description: nulo
uuid: b9c9464e-ff19-4051-a39b-4ec71c512d10
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 7eb0e8a8-d76a-43f7-a012-c21157b14cd4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Representación de formularios HTML con barras de herramientas personalizadas {#rendering-html-forms-with-customtoolbars}

## Representación de formularios HTML con barras de herramientas personalizadas {#rendering-html-forms-with-custom-toolbars}

El servicio Forms permite personalizar una barra de herramientas que se procesa con un formulario HTML. Se puede personalizar una barra de herramientas para modificar su aspecto anulando los estilos CSS predeterminados y para añadir un comportamiento dinámico anulando las secuencias de comandos de Java. Una barra de herramientas se personaliza mediante un archivo XML llamado fscmenu.xml. De forma predeterminada, el servicio Forms recupera este archivo desde una ubicación URI especificada internamente.

>[!NOTE]
>
>Esta ubicación URI se encuentra en el archivo adobe-forms-core.jar, que se encuentra en el archivo adobe-forms-dsc.jar. El archivo adobe-forms-dsc.jar se encuentra en C:\Adobe\Adobe_Experience_Manager_forms\ folder (C:\ is the installation directory). Puede utilizar una herramienta de extracción de archivos, como Win RAR, para abrir el adobe.

Puede copiar el archivo fscmenu.xml desde esta ubicación, modificarlo para que cumpla sus requisitos y, a continuación, colocarlo en una ubicación URI personalizada. A continuación, mediante la API de Forms Service, defina las opciones de tiempo de ejecución que resulten en el servicio Forms mediante el archivo fscmenu.xml desde la ubicación especificada. Estas acciones resultan en que el servicio Forms procese un formulario HTML que tiene una barra de herramientas personalizada.

Además del archivo fscmenu.xml, también debe obtener los siguientes archivos:

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS es la secuencia de comandos de Java asociada a cada nodo. Es necesario proporcionar uno para el `div#fscmenu` nodo y opcionalmente para `ul#fscmenuItem` los nodos. Los archivos JS implementan la funcionalidad básica de la barra de herramientas y los archivos predeterminados funcionan.

fscCSS es una hoja de estilo asociada a un nodo concreto. Los estilos de los archivos CSS especifican el aspecto de la barra de herramientas. *fscVCSS* es una hoja de estilo para una barra de herramientas vertical que se muestra a la izquierda del formulario HTML procesado. *fscIECSS* es una hoja de estilo que se utiliza para los formularios HTML que se procesan en Internet Explorer.

Asegúrese de que se hace referencia a todos los archivos anteriores en el archivo fscmenu.xml. Es decir, en el archivo fscmenu.xml, especifique ubicaciones de URI para que apunten a estos archivos de modo que el servicio Forms pueda localizarlos. De forma predeterminada, estos archivos están disponibles en ubicaciones de URI que comienzan por palabras clave internas `FSWebRoot` o `ApplicationWebRoot`.

Para personalizar la barra de herramientas, reemplace las palabras clave utilizando la palabra clave externa `FSToolBarURI`. Esta palabra clave representa el URI que se pasa al servicio Forms en tiempo de ejecución (este método se muestra más adelante en esta sección).

También puede especificar las ubicaciones absolutas de estos archivos JS y CSS, como https://www.mycompany.com/scripts/misc/fscmenu.js. En este caso, no es necesario utilizar la `FSToolBarURI` palabra clave.

>[!NOTE]
>
>No se recomienda mezclar las formas en que se hace referencia a estos archivos. Es decir, se debe hacer referencia a todos los URI utilizando la `FSToolBarURI` palabra clave o una ubicación absoluta.

Puede obtener los archivos JS y CSS abriendo el archivo adobe-forms-&lt;appserver>.ear. En este archivo, abra adobe-forms-res.war. Todos estos archivos se encuentran en el archivo WAR. El archivo adobe-forms-&lt;appserver>.ear se encuentra en la carpeta de instalación de formularios AEM (C:\ is the installation directory). Puede abrir adobe-forms-&lt;appserver>.ear con una herramienta de extracción de archivos como WinRAR.

La siguiente sintaxis XML muestra un archivo fscmenu.xml de ejemplo.

```as3
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css">
         <ul class="fscmenuItem" id="Home">
             <li>
                 <a href="#" fscTarget="_top" tabindex="1">Home</a>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css">
             <li>
                 <a tabindex="2">Upload Attachments</a>
                 <ul class="fscmenuPopup" id="fscUploadAttachments">
                     <li>
                         <a href="javascript:doUploadDialog();" tabindex="3">Add ...</a>
                     </li>
                     <li>
                         <a href="javascript:doDeleteDialog();" tabindex="4">Delete ...</a>
                     </li>
                 </ul>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Download">
             <li>
                 <a tabindex="100">Download Attachments</a>
                 <ul class="fscmenuPopup">
                     <li>
                         <a tabindex="101">None available</a>
                     </li>
                 </ul>
             </li>
         </ul>
     </div>
```

>[!NOTE]
>
>El texto en negrita representa los URI de los archivos CSS y JS a los que se debe hacer referencia.

Los siguientes elementos describen cómo se puede personalizar una barra de herramientas:

* Cambie los valores de `fscJS`, `fscCSS`, `fscVCSS`, `fscIECSS` atributos (en el archivo fscmenu.xml) para reflejar las ubicaciones personalizadas de los archivos a los que se hace referencia mediante uno de los métodos descritos en esta sección (por ejemplo, `fscJS="FSToolBarURI/scripts/fscmenu.js"`).
* Se deben especificar todos los archivos CSS y JS. Si no se modifica ninguno de los archivos, especifique el predeterminado en la ubicación personalizada. Puede obtener los archivos predeterminados abriendo varios archivos, como se describe en esta sección.
* Se permite proporcionar una referencia absoluta (por ejemplo, https://www.example.com/scripts/custom-vertical-fscmenu.css) para cualquier archivo.
* Los archivos JS y CSS que requiere el `div#fscmenu` nodo son esenciales para la funcionalidad de la barra de herramientas. Los `ul#fscmenuItem` nodos individuales pueden o no tener archivos JS o CSS compatibles.

**Cambio del valor local**

Como parte de la personalización de una barra de herramientas, puede cambiar el valor de configuración regional de la misma. Es decir, se puede mostrar en otro idioma. La siguiente ilustración muestra una barra de herramientas personalizada que se muestra en francés.

>[!NOTE]
>
>No es posible crear una barra de herramientas personalizada en más de un idioma. Las barras de herramientas no pueden utilizar archivos XML diferentes según la configuración regional.

Para cambiar el valor de configuración regional de una barra de herramientas, asegúrese de que el archivo fscmenu.xml contiene el idioma que desea mostrar. La siguiente sintaxis XML muestra el archivo fscmenu.xml que se utiliza para mostrar una barra de herramientas en francés.

```as3
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css">
         <ul class="fscmenuItem" id="Home">
             <li>
                 <a href="#" fscTarget="_top" tabindex="1">Accueil</a>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css">
             <li>
                 <a tabindex="2">Télécharger les pièces jointes</a>
                 <ul class="fscmenuPopup" id="fscUploadAttachments">
                     <li>
                         <a href="javascript:doUploadDialog();" tabindex="3">Ajouter...</a>
                     </li>
                     <li>
                         <a href="javascript:doDeleteDialog();" tabindex="4">Supprimer...</a>
                     </li>
                 </ul>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Download">
             <li>
                 <a tabindex="100">Télécharger les pièces jointes</a>
                 <ul class="fscmenuPopup">
                     <li>
                         <a tabindex="101">Aucune disponible</a>
                     </li>
                 </ul>
             </li>
         </ul>
     </div>
```

>[!NOTE]
>
>Los inicios rápidos asociados a esta sección utilizan este archivo XML para mostrar una barra de herramientas personalizada en francés, como se muestra en la ilustración anterior.

Además, especifique un valor de configuración regional válido invocando el `HTMLRenderSpec` método `setLocale` del objeto y pasando un valor de cadena que especifica el valor de configuración regional. Por ejemplo, pase `fr_FR` para especificar el francés. El servicio Forms se incluye con barras de herramientas localizadas.

>[!NOTE]
>
>Antes de procesar un formulario HTML que utiliza una barra de herramientas personalizada, debe saber cómo se procesan los formularios HTML. (Consulte [Representación de formularios como HTML](/help/forms/developing/rendering-forms-html.md)).

Para obtener más información sobre el servicio Forms, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para procesar un formulario HTML que contenga una barra de herramientas personalizada, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de Java de Forms.
1. Haga referencia a un archivo XML de fscmenu personalizado.
1. Representar un formulario HTML.
1. Escriba la secuencia de datos del formulario en el navegador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, incluya los archivos proxy.

**Creación de un objeto de API de Java de Forms**

Para poder realizar mediante programación una operación que admita el servicio Forms, debe crear un objeto de cliente Forms.

**Hacer referencia a un archivo XML de fscmenu personalizado**

Para procesar un formulario HTML que contenga una barra de herramientas personalizada, haga referencia a un archivo XML fscmenu que describa la barra de herramientas. (Esta sección proporciona dos ejemplos de un archivo XML fscmenu). Además, asegúrese de que el archivo fscmenu.xml especifica correctamente las ubicaciones de todos los archivos a los que se hace referencia. Como se mencionó anteriormente en esta sección, asegúrese de que la palabra clave o sus ubicaciones absolutas hagan referencia a todos los archivos. `FSToolBarURI`

**Representar un formulario HTML**

Para procesar un formulario HTML, especifique un diseño de formulario que se haya creado en Designer y guardado como archivo XDP. Seleccione también un tipo de transformación HTML. Por ejemplo, puede especificar el tipo de transformación HTML que procesa un HTML dinámico para Internet Explorer 5.0 o posterior.

El procesamiento de un formulario HTML también requiere valores, como valores URI para procesar otros tipos de formulario.

**Escribir el flujo de datos del formulario en el navegador web del cliente**

Cuando el servicio Forms procesa un formulario HTML, devuelve una secuencia de datos de formulario que debe escribir en el navegador web del cliente para que el formulario HTML sea visible para los usuarios.

**Consulte también**

[Representar un formulario HTML con una barra de herramientas personalizada mediante la API de Java](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Representación de un formulario HTML con una barra de herramientas personalizada mediante la API de servicio Web](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de formularios](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Representación de formularios PDF interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Representación de formularios como HTML](/help/forms/developing/rendering-forms-html.md)

[Creación de aplicaciones Web que procesan formularios](/help/forms/developing/creating-web-applications-renders-forms.md)

### Representar un formulario HTML con una barra de herramientas personalizada mediante la API de Java {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

Representar un formulario HTML que contenga una barra de herramientas personalizada mediante la API de Forms Service (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clases del proyecto Java.

1. Creación de un objeto de API de Java de Forms

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `FormsServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Hacer referencia a un archivo XML de fscmenu personalizado

   * Cree un `HTMLRenderSpec` objeto con su constructor.
   * Para procesar un formulario HTML con una barra de herramientas, invoque el `HTMLRenderSpec` método del `setHTMLToolbar` objeto y pase un valor `HTMLToolbar` enum. Por ejemplo, para mostrar una barra de herramientas HTML vertical, pase `HTMLToolbar.Vertical`.
   * Especifique la ubicación del archivo XML fscmenu invocando el `HTMLRenderSpec` método `setToolbarURI` del objeto y pasando un valor de cadena que especifica la ubicación URI del archivo XML.
   * Si corresponde, establezca el valor de configuración regional invocando el `HTMLRenderSpec` método del `setLocale` objeto y pasando un valor de cadena que especifique el valor de configuración regional. El valor predeterminado es inglés.
   >[!NOTE]
   >
   >Los inicios rápidos asociados con esta sección establecen este valor en `fr_FR`*.*

1. Representar un formulario HTML

   Invoque el `FormsServiceClient` método del `renderHTMLForm` objeto y pase los valores siguientes:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un valor `TransformTo` enum que especifica el tipo de preferencia HTML. Por ejemplo, para procesar un formulario HTML compatible con HTML dinámico para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * Un `com.adobe.idp.Document` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un `com.adobe.idp.Document` objeto vacío.
   * El `HTMLRenderSpec` objeto que almacena las opciones de tiempo de ejecución HTML.
   * Un valor de cadena que especifica el valor del `HTTP_USER_AGENT` encabezado, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Un `URLSpec` objeto que almacena valores URI necesarios para procesar un formulario HTML.
   * Un `java.util.HashMap` objeto que almacena archivos adjuntos. Se trata de un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   El `renderHTMLForm` método devuelve un `FormsResult` objeto que contiene una secuencia de datos de formulario que se debe escribir en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un `com.adobe.idp.Document` objeto invocando el `FormsResult` método ‘s `getOutputContent` .
   * Obtenga el tipo de contenido del `com.adobe.idp.Document` objeto invocando su `getContentType` método.
   * Defina el tipo de contenido del `javax.servlet.http.HttpServletResponse` objeto invocando su `setContentType` método y pasando el tipo de contenido del `com.adobe.idp.Document` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el `javax.servlet.http.HttpServletResponse` método del `getOutputStream` objeto.
   * Cree un `java.io.InputStream` objeto invocando el `com.adobe.idp.Document` método `getInputStream` del objeto.
   * Cree una matriz de bytes y rellénela con la secuencia de datos del formulario invocando el `InputStream` método del `read` objeto y pasando la matriz de bytes como argumento.
   * Invoque el `javax.servlet.ServletOutputStream` método del `write` objeto para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al `write` método .

**Consulte también**

[Inicio rápido (modo SOAP): Representación de un formulario HTML con una barra de herramientas personalizada mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Representación de un formulario HTML con una barra de herramientas personalizada mediante la API de servicio Web {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

Representar un formulario HTML que contenga una barra de herramientas personalizada mediante la API de Forms Service (servicio Web):

1. Incluir archivos de proyecto

   * Cree clases proxy de Java que consuman el WSDL del servicio Forms.
   * Incluya las clases proxy de Java en la ruta de clases.

1. Creación de un objeto de API de Java de Forms

   Cree un `FormsService` objeto y defina los valores de autenticación.

1. Hacer referencia a un archivo XML de fscmenu personalizado

   * Cree un `HTMLRenderSpec` objeto con su constructor.
   * Para procesar un formulario HTML con una barra de herramientas, invoque el `HTMLRenderSpec` método del `setHTMLToolbar` objeto y pase un valor `HTMLToolbar` enum. Por ejemplo, para mostrar una barra de herramientas HTML vertical, pase `HTMLToolbar.Vertical`.
   * Especifique la ubicación del archivo XML fscmenu invocando el `HTMLRenderSpec` método `setToolbarURI` del objeto y pasando un valor de cadena que especifica la ubicación URI del archivo XML.
   * Si corresponde, establezca el valor de configuración regional invocando el `HTMLRenderSpec` método del `setLocale` objeto y pasando un valor de cadena que especifique el valor de configuración regional. El valor predeterminado es inglés.
   >[!NOTE]
   >
   >Los inicios rápidos asociados con esta sección establecen este valor en `fr_FR`*.*

1. Representar un formulario HTML

   Invoque el `FormsService` método del `renderHTMLForm` objeto y pase los valores siguientes:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un valor `TransformTo` enum que especifica el tipo de preferencia HTML. Por ejemplo, para procesar un formulario HTML compatible con HTML dinámico para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * Un `BLOB` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`.
   * El `HTMLRenderSpec` objeto que almacena las opciones de tiempo de ejecución HTML.
   * Un valor de cadena que especifica el valor del `HTTP_USER_AGENT` encabezado, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`). Puede pasar una cadena vacía si no desea establecer este valor.
   * Un `URLSpec` objeto que almacena valores URI necesarios para procesar un formulario HTML.
   * Un `java.util.HashMap` objeto que almacena archivos adjuntos. Este parámetro es opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Objeto vacío `com.adobe.idp.services.holders.BLOBHolder` que se rellena con el `renderHTMLForm` método . Este valor de parámetro almacena el formulario procesado.
   * Objeto vacío `com.adobe.idp.services.holders.BLOBHolder` que se rellena con el `renderHTMLForm` método . Este parámetro almacena los datos XML de salida.
   * Objeto vacío `javax.xml.rpc.holders.LongHolder` que se rellena con el `renderHTMLForm` método . Este argumento almacena el número de páginas del formulario.
   * Objeto vacío `javax.xml.rpc.holders.StringHolder` que se rellena con el `renderHTMLForm` método . Este argumento almacena el valor de configuración regional.
   * Objeto vacío `javax.xml.rpc.holders.StringHolder` que se rellena con el `renderHTMLForm` método . Este argumento almacena el valor de representación HTML que se utiliza.
   * Un `com.adobe.idp.services.holders.FormsResultHolder` objeto vacío que contendrá los resultados de esta operación.
   El `renderHTMLForm` método rellena el `com.adobe.idp.services.holders.FormsResultHolder` objeto que se pasa como el último valor de argumento con una secuencia de datos de formulario que se debe escribir en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un `FormResult` objeto obteniendo el valor del `com.adobe.idp.services.holders.FormsResultHolder` miembro de `value` datos del objeto.
   * Cree un `BLOB` objeto que contenga datos de formulario invocando el `FormsResult` método `getOutputContent` del objeto.
   * Obtenga el tipo de contenido del `BLOB` objeto invocando su `getContentType` método.
   * Defina el tipo de contenido del `javax.servlet.http.HttpServletResponse` objeto invocando su `setContentType` método y pasando el tipo de contenido del `BLOB` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el `javax.servlet.http.HttpServletResponse` método del `getOutputStream` objeto.
   * Cree una matriz de bytes y rellénela invocando el `BLOB` método `getBinaryData` del objeto. Esta tarea asigna el contenido del `FormsResult` objeto a la matriz de bytes.
   * Invoque el `javax.servlet.http.HttpServletResponse` método del `write` objeto para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al `write` método .

**Consulte también**

[Invocación de formularios AEM con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
