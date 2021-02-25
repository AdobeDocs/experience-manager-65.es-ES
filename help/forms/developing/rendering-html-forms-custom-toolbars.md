---
title: Representación de HTML Forms con barras de herramientas personalizadas
seo-title: Representación de HTML Forms con barras de herramientas personalizadas
description: Utilice el servicio Forms para personalizar una barra de herramientas que se procesa con un formulario HTML. Puede procesar un formulario HTML con una barra de herramientas personalizada mediante la API de Java y una API de servicio Web.
seo-description: Utilice el servicio Forms para personalizar una barra de herramientas que se procesa con un formulario HTML. Puede procesar un formulario HTML con una barra de herramientas personalizada mediante la API de Java y una API de servicio Web.
uuid: b9c9464e-ff19-4051-a39b-4ec71c512d10
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 7eb0e8a8-d76a-43f7-a012-c21157b14cd4
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '2384'
ht-degree: 0%

---


# Representación de HTML Forms con barras de herramientas personalizadas {#rendering-html-forms-with-customtoolbars}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en el entorno JEE.**

## Representación de HTML Forms con barras de herramientas personalizadas {#rendering-html-forms-with-custom-toolbars}

El servicio Forms permite personalizar una barra de herramientas que se procesa con un formulario HTML. Se puede personalizar una barra de herramientas para modificar su aspecto anulando los estilos CSS predeterminados y para añadir un comportamiento dinámico anulando las secuencias de comandos de Java. Una barra de herramientas se personaliza mediante un archivo XML llamado fscmenu.xml. De forma predeterminada, el servicio Forms recupera este archivo desde una ubicación URI especificada internamente.

>[!NOTE]
>
>Esta ubicación URI se encuentra en el archivo adobe-forms-core.jar, que se encuentra en el archivo adobe-forms-dsc.jar. El archivo adobe-forms-dsc.jar se encuentra en C:\Adobe\Adobe_Experience_Manager_forms\ folder (C:\ is the installation directory). Puede utilizar una herramienta de extracción de archivos, como Win RAR, para abrir el adobe.

Puede copiar el archivo fscmenu.xml desde esta ubicación, modificarlo para que cumpla sus requisitos y, a continuación, colocarlo en una ubicación URI personalizada. A continuación, mediante la API de servicio de Forms, establezca las opciones de tiempo de ejecución que resulten en que el servicio de Forms utilice el archivo fscmenu.xml desde la ubicación especificada. Estas acciones resultan en que el servicio de Forms procese un formulario HTML que tiene una barra de herramientas personalizada.

Además del archivo fscmenu.xml, también debe obtener los siguientes archivos:

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS es la secuencia de comandos de Java asociada a cada nodo. Es necesario proporcionar uno para el nodo `div#fscmenu` y opcionalmente para los nodos `ul#fscmenuItem`. Los archivos JS implementan la funcionalidad básica de la barra de herramientas y los archivos predeterminados funcionan.

fscCSS es una hoja de estilo asociada a un nodo concreto. Los estilos de los archivos CSS especifican el aspecto de la barra de herramientas. ** fscVCSS es una hoja de estilo para una barra de herramientas vertical que se muestra a la izquierda del formulario HTML procesado. ** fscIECSS es una hoja de estilo que se utiliza para los formularios HTML que se procesan en Internet Explorer.

Asegúrese de que se hace referencia a todos los archivos anteriores en el archivo fscmenu.xml. Es decir, en el archivo fscmenu.xml, especifique las ubicaciones de URI que deben apuntar a estos archivos para que el servicio de Forms pueda localizarlos. De forma predeterminada, estos archivos están disponibles en ubicaciones de URI que comienzan con palabras clave internas `FSWebRoot` o `ApplicationWebRoot`.

Para personalizar la barra de herramientas, reemplace las palabras clave utilizando la palabra clave externa `FSToolBarURI`. Esta palabra clave representa el URI que se pasa al servicio de Forms en tiempo de ejecución (este método se muestra más adelante en esta sección).

También puede especificar las ubicaciones absolutas de estos archivos JS y CSS, como https://www.mycompany.com/scripts/misc/fscmenu.js. En este caso, no es necesario utilizar la palabra clave `FSToolBarURI`.

>[!NOTE]
>
>No se recomienda mezclar las formas en que se hace referencia a estos archivos. Es decir, se debe hacer referencia a todos los URI utilizando la palabra clave `FSToolBarURI` o una ubicación absoluta.

Puede obtener los archivos JS y CSS abriendo el archivo adobe-forms-&lt;appserver>.ear. En este archivo, abra adobe-forms-res.war. Todos estos archivos se encuentran en el archivo WAR. El archivo adobe-forms-&lt;appserver>.ear se encuentra en la carpeta de instalación de AEM formularios (C:\ is the installation directory). Puede abrir adobe-forms-&lt;appserver>.ear con una herramienta de extracción de archivos como WinRAR.

La siguiente sintaxis XML muestra un archivo fscmenu.xml de ejemplo.

```html
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

* Cambie los valores de los atributos `fscJS`, `fscCSS`, `fscVCSS`, `fscIECSS` (en el archivo fscmenu.xml) para reflejar las ubicaciones personalizadas de los archivos a los que se hace referencia mediante uno de los métodos descritos en esta sección (por ejemplo, `fscJS="FSToolBarURI/scripts/fscmenu.js"`).
* Se deben especificar todos los archivos CSS y JS. Si no se modifica ninguno de los archivos, especifique el predeterminado en la ubicación personalizada. Puede obtener los archivos predeterminados abriendo varios archivos, como se describe en esta sección.
* Se permite proporcionar una referencia absoluta (por ejemplo, https://www.example.com/scripts/custom-vertical-fscmenu.css) para cualquier archivo.
* Los archivos JS y CSS que requiere el nodo `div#fscmenu` son esenciales para la funcionalidad de la barra de herramientas. Los nodos individuales `ul#fscmenuItem` pueden tener o no admitir archivos JS o CSS.

**Cambio del valor local**

Como parte de la personalización de una barra de herramientas, puede cambiar el valor de configuración regional de la misma. Es decir, se puede mostrar en otro idioma. La siguiente ilustración muestra una barra de herramientas personalizada que se muestra en francés.

>[!NOTE]
>
>No es posible crear una barra de herramientas personalizada en más de un idioma. Las barras de herramientas no pueden utilizar archivos XML diferentes según la configuración regional.

Para cambiar el valor de configuración regional de una barra de herramientas, asegúrese de que el archivo fscmenu.xml contiene el idioma que desea mostrar. La siguiente sintaxis XML muestra el archivo fscmenu.xml que se utiliza para mostrar una barra de herramientas en francés.

```html
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
>Los Inicios rápidos asociados con esta sección utilizan este archivo XML para mostrar una barra de herramientas personalizada en francés, como se muestra en la ilustración anterior.

Además, especifique un valor de configuración regional válido invocando el método `HTMLRenderSpec` del objeto `setLocale` y pasando un valor de cadena que especifica el valor de configuración regional. Por ejemplo, pase `fr_FR` para especificar el francés. El servicio de Forms se incluye con barras de herramientas localizadas.

>[!NOTE]
>
>Antes de procesar un formulario HTML que utiliza una barra de herramientas personalizada, debe saber cómo se procesan los formularios HTML. (Consulte [Representación de Forms como HTML](/help/forms/developing/rendering-forms-html.md)).

Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para procesar un formulario HTML que contenga una barra de herramientas personalizada, lleve a cabo estas tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API Java de Forms.
1. Haga referencia a un archivo XML de fscmenu personalizado.
1. Representar un formulario HTML.
1. Escriba la secuencia de datos del formulario en el navegador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, incluya los archivos proxy.

**Creación de un objeto de API de Forms Java**

Para poder realizar mediante programación una operación que admita el servicio Forms, debe crear un objeto cliente de Forms.

**Hacer referencia a un archivo XML de fscmenu personalizado**

Para procesar un formulario HTML que contenga una barra de herramientas personalizada, haga referencia a un archivo XML fscmenu que describa la barra de herramientas. (Esta sección proporciona dos ejemplos de un archivo XML fscmenu). Además, asegúrese de que el archivo fscmenu.xml especifica correctamente las ubicaciones de todos los archivos a los que se hace referencia. Como se mencionó anteriormente en esta sección, asegúrese de que la palabra clave `FSToolBarURI` o sus ubicaciones absolutas hagan referencia a todos los archivos.

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

[Inicios rápidos de la API de servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Representación de PDF forms interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Representación de Forms como HTML](/help/forms/developing/rendering-forms-html.md)

[Creación de Aplicaciones web que procesan Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Representar un formulario HTML con una barra de herramientas personalizada mediante la API de Java {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

Representar un formulario HTML que contenga una barra de herramientas personalizada mediante la API de servicio de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clases del proyecto Java.

1. Creación de un objeto de API de Forms Java

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `FormsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Hacer referencia a un archivo XML de fscmenu personalizado

   * Cree un objeto `HTMLRenderSpec` utilizando su constructor.
   * Para procesar un formulario HTML con una barra de herramientas, invoque el método `HTMLRenderSpec` del objeto `setHTMLToolbar` y pase un valor de enumeración `HTMLToolbar`. Por ejemplo, para mostrar una barra de herramientas HTML vertical, pase `HTMLToolbar.Vertical`.
   * Especifique la ubicación del archivo XML fscmenu invocando el método `HTMLRenderSpec` del objeto `setToolbarURI` y pasando un valor de cadena que especifica la ubicación URI del archivo XML.
   * Si corresponde, establezca el valor de configuración regional invocando el método `HTMLRenderSpec` del objeto `setLocale` y pasando un valor de cadena que especifique el valor de configuración regional. El valor predeterminado es inglés.

   >[!NOTE]
   >
   >Los Inicios rápidos asociados con esta sección establecen este valor en `fr_FR`*.*

1. Representar un formulario HTML

   Invoque el método `FormsServiceClient` del objeto `renderHTMLForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un valor de enumeración `TransformTo` que especifica el tipo de preferencia HTML. Por ejemplo, para procesar un formulario HTML compatible con HTML dinámico para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * Un objeto `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un objeto vacío `com.adobe.idp.Document`.
   * El objeto `HTMLRenderSpec` que almacena las opciones de tiempo de ejecución HTML.
   * Un valor de cadena que especifica el valor del encabezado `HTTP_USER_AGENT`, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Un objeto `URLSpec` que almacena valores URI necesarios para procesar un formulario HTML.
   * Objeto `java.util.HashMap` que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El método `renderHTMLForm` devuelve un objeto `FormsResult` que contiene una secuencia de datos de formulario que debe escribirse en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un objeto `com.adobe.idp.Document` invocando el método `FormsResult` del objeto ‘s `getOutputContent`.
   * Obtenga el tipo de contenido del objeto `com.adobe.idp.Document` invocando su método `getContentType`.
   * Configure el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `com.adobe.idp.Document`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el método `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream`.
   * Cree un objeto `java.io.InputStream` invocando el método `com.adobe.idp.Document` del objeto `getInputStream`.
   * Cree una matriz de bytes y rellénela con la secuencia de datos del formulario invocando el método `InputStream` del objeto `read` y pasando la matriz de bytes como argumento.
   * Invoque el método `javax.servlet.ServletOutputStream` del objeto `write` para enviar la secuencia de datos del formulario al explorador Web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Inicio rápido (modo SOAP): Representación de un formulario HTML con una barra de herramientas personalizada mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Representación de un formulario HTML con una barra de herramientas personalizada mediante la API de servicio Web {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

Representar un formulario HTML que contenga una barra de herramientas personalizada mediante la API de servicio de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases proxy de Java que consuman el WSDL del servicio de Forms.
   * Incluya las clases proxy de Java en la ruta de clases.

1. Creación de un objeto de API de Forms Java

   Cree un objeto `FormsService` y defina los valores de autenticación.

1. Hacer referencia a un archivo XML de fscmenu personalizado

   * Cree un objeto `HTMLRenderSpec` utilizando su constructor.
   * Para procesar un formulario HTML con una barra de herramientas, invoque el método `HTMLRenderSpec` del objeto `setHTMLToolbar` y pase un valor de enumeración `HTMLToolbar`. Por ejemplo, para mostrar una barra de herramientas HTML vertical, pase `HTMLToolbar.Vertical`.
   * Especifique la ubicación del archivo XML fscmenu invocando el método `HTMLRenderSpec` del objeto `setToolbarURI` y pasando un valor de cadena que especifica la ubicación URI del archivo XML.
   * Si corresponde, establezca el valor de configuración regional invocando el método `HTMLRenderSpec` del objeto `setLocale` y pasando un valor de cadena que especifique el valor de configuración regional. El valor predeterminado es inglés.

   >[!NOTE]
   >
   >Los Inicios rápidos asociados con esta sección establecen este valor en `fr_FR`*.*

1. Representar un formulario HTML

   Invoque el método `FormsService` del objeto `renderHTMLForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un valor de enumeración `TransformTo` que especifica el tipo de preferencia HTML. Por ejemplo, para procesar un formulario HTML compatible con HTML dinámico para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * Un objeto `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`.
   * El objeto `HTMLRenderSpec` que almacena las opciones de tiempo de ejecución HTML.
   * Un valor de cadena que especifica el valor del encabezado `HTTP_USER_AGENT`, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`). Puede pasar una cadena vacía si no desea establecer este valor.
   * Un objeto `URLSpec` que almacena valores URI necesarios para procesar un formulario HTML.
   * Objeto `java.util.HashMap` que almacena archivos adjuntos. Este parámetro es opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un objeto vacío `com.adobe.idp.services.holders.BLOBHolder` que se rellena con el método `renderHTMLForm`. Este valor de parámetro almacena el formulario procesado.
   * Un objeto vacío `com.adobe.idp.services.holders.BLOBHolder` que se rellena con el método `renderHTMLForm`. Este parámetro almacena los datos XML de salida.
   * Un objeto vacío `javax.xml.rpc.holders.LongHolder` que se rellena con el método `renderHTMLForm`. Este argumento almacena el número de páginas del formulario.
   * Un objeto vacío `javax.xml.rpc.holders.StringHolder` que se rellena con el método `renderHTMLForm`. Este argumento almacena el valor de configuración regional.
   * Un objeto vacío `javax.xml.rpc.holders.StringHolder` que se rellena con el método `renderHTMLForm`. Este argumento almacena el valor de representación HTML que se utiliza.
   * Un objeto vacío `com.adobe.idp.services.holders.FormsResultHolder` que contendrá los resultados de esta operación.

   El método `renderHTMLForm` rellena el objeto `com.adobe.idp.services.holders.FormsResultHolder` que se pasa como el último valor de argumento con una secuencia de datos de formulario que debe escribirse en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un objeto `FormResult` obteniendo el valor del miembro de datos `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value`.
   * Cree un objeto `BLOB` que contenga datos de formulario invocando el método `FormsResult` del objeto `getOutputContent`.
   * Obtenga el tipo de contenido del objeto `BLOB` invocando su método `getContentType`.
   * Configure el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `BLOB`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el método `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream`.
   * Cree una matriz de bytes y rellénela invocando el método `BLOB` del objeto `getBinaryData`. Esta tarea asigna el contenido del objeto `FormsResult` a la matriz de bytes.
   * Invoque el método `javax.servlet.http.HttpServletResponse` del objeto `write` para enviar la secuencia de datos del formulario al explorador Web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
