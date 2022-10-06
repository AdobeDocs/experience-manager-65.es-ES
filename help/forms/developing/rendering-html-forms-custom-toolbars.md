---
title: Representación de Forms HTML con barras de herramientas personalizadas
seo-title: Rendering HTML Forms with CustomToolbars
description: Utilice el servicio Forms para personalizar una barra de herramientas que se procese con un formulario de HTML. Puede procesar un formulario de HTML con una barra de herramientas personalizada mediante la API de Java y una API de servicio web.
seo-description: Use the Forms service to customize a toolbar that is rendered with an HTML form. You can render an HTML Form with a custom toolbar using the Java API and a Web Service API.
uuid: b9c9464e-ff19-4051-a39b-4ec71c512d10
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 7eb0e8a8-d76a-43f7-a012-c21157b14cd4
role: Developer
exl-id: 0b992b1c-3878-447a-bccc-7034aa3e98bc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2345'
ht-degree: 0%

---

# Representación de Forms HTML con barras de herramientas personalizadas {#rendering-html-forms-with-customtoolbars}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

## Representación de Forms HTML con barras de herramientas personalizadas {#rendering-html-forms-with-custom-toolbars}

El servicio Forms permite personalizar una barra de herramientas que se procesa con un formulario de HTML. Se puede personalizar una barra de herramientas para modificar su aspecto anulando los estilos CSS predeterminados y para añadir un comportamiento dinámico anulando los scripts Java. Una barra de herramientas se personaliza utilizando un archivo XML llamado fscmenu.xml. De forma predeterminada, el servicio Forms recupera este archivo desde una ubicación URI especificada internamente.

>[!NOTE]
>
>Esta ubicación URI se encuentra en el archivo adobe-forms-core.jar , que se encuentra en el archivo adobe-forms-dsc.jar . El archivo adobe-forms-dsc.jar se encuentra en C:\Adobe\Adobe_Experience_Manager_forms\ folder (C:\ is the installation directory). Puede utilizar una herramienta de extracción de archivos, como Win RAR, para abrir el adobe.

Puede copiar el archivo fscmenu.xml desde esta ubicación, modificarlo para satisfacer sus necesidades y, a continuación, colocarlo en una ubicación URI personalizada. A continuación, con la API de servicio de Forms, establezca las opciones en tiempo de ejecución que resulten en que el servicio de Forms use su archivo fscmenu.xml desde la ubicación especificada. Estas acciones resultan en que el servicio de Forms procese un formulario de HTML que tiene una barra de herramientas personalizada.

Además del archivo fscmenu.xml, también debe obtener los siguientes archivos:

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS es la secuencia de comandos Java asociada a cada nodo. Es necesario suministrar uno para el `div#fscmenu` nodo y, opcionalmente, para `ul#fscmenuItem` nodos. Los archivos JS implementan la funcionalidad principal de la barra de herramientas y los archivos predeterminados funcionan.

fscCSS es una hoja de estilos asociada a un nodo en particular. Los estilos de los archivos CSS especifican el aspecto de la barra de herramientas. *fscVCSS* es una hoja de estilo para una barra de herramientas vertical que se muestra a la izquierda del formulario HTML procesado. *fscIECSS* es una hoja de estilo que se utiliza para formularios HTML que se procesan en Internet Explorer.

Asegúrese de que todos los archivos anteriores están referenciados en el archivo fscmenu.xml. Es decir, en el archivo fscmenu.xml, especifique las ubicaciones de URI que apunten a estos archivos para que el servicio de Forms pueda localizarlos. De forma predeterminada, estos archivos están disponibles en ubicaciones de URI que empiezan por palabras clave internas `FSWebRoot` o `ApplicationWebRoot`.

Para personalizar la barra de herramientas, reemplace las palabras clave utilizando la palabra clave externa `FSToolBarURI`. Esta palabra clave representa el URI que se pasa al servicio de Forms en tiempo de ejecución (este método se muestra más adelante en esta sección).

También puede especificar las ubicaciones absolutas de estos archivos JS y CSS, como https://www.mycompany.com/scripts/misc/fscmenu.js. En este caso, no es necesario usar la variable `FSToolBarURI` palabra clave.

>[!NOTE]
>
>No se recomienda mezclar las formas en que se hace referencia a estos archivos. Es decir, se debe hacer referencia a todos los URI utilizando la variable `FSToolBarURI` o una ubicación absoluta.

Puede obtener los archivos JS y CSS abriendo adobe-forms-&lt;appserver>archivo .ear. En este archivo, abra adobe-forms-res.war. Todos estos archivos se encuentran en el archivo WAR. Los adobe-forms-&lt;appserver>El archivo .ear se encuentra en la carpeta de instalación de AEM forms (C:\ is the installation directory). Puede abrir adobe-forms-&lt;appserver>.ear con una herramienta de extracción de archivos como WinRAR.

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

* Cambiar los valores de `fscJS`, `fscCSS`, `fscVCSS`, `fscIECSS` (en el archivo fscmenu.xml ) para reflejar las ubicaciones personalizadas de los archivos a los que se hace referencia utilizando uno de los métodos que se describen en esta sección (por ejemplo, `fscJS="FSToolBarURI/scripts/fscmenu.js"`).
* Se deben especificar todos los archivos CSS y JS. Si no se modifica ninguno de los archivos, proporcione el predeterminado en la ubicación personalizada. Puede obtener los archivos predeterminados abriendo varios archivos como se describe en esta sección.
* Se permite proporcionar una referencia absoluta (por ejemplo, https://www.example.com/scripts/custom-vertical-fscmenu.css) para cualquier archivo.
* Los archivos JS y CSS que la variable `div#fscmenu` Los requisitos del nodo son esenciales para la funcionalidad de la barra de herramientas. Individual `ul#fscmenuItem` los nodos pueden tener o no admitir archivos JS o CSS.

**Modificación del valor local**

Como parte de la personalización de una barra de herramientas, puede cambiar el valor de configuración regional de la barra de herramientas. Es decir, puede mostrarlo en otro idioma. La siguiente ilustración muestra una barra de herramientas personalizada que se muestra en francés.

>[!NOTE]
>
>No es posible crear una barra de herramientas personalizada en más de un idioma. Las barras de herramientas no pueden utilizar diferentes archivos XML basados en la configuración regional.

Para cambiar el valor de configuración regional de una barra de herramientas, asegúrese de que el archivo fscmenu.xml contenga el idioma que desea mostrar. La siguiente sintaxis XML muestra el archivo fscmenu.xml que se utiliza para mostrar una barra de herramientas en francés.

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
>Los Quick Starts asociados a esta sección utilizan este archivo XML para mostrar una barra de herramientas personalizada en francés, como se muestra en la ilustración anterior.

Además, especifique un valor de configuración regional válido invocando la variable `HTMLRenderSpec` del objeto `setLocale` y pasando un valor de cadena que especifica el valor de configuración regional. Por ejemplo, pase `fr_FR` para especificar el francés. El servicio Forms está empaquetado con barras de herramientas localizadas.

>[!NOTE]
>
>Antes de procesar un formulario de HTML que utilice una barra de herramientas personalizada, debe saber cómo se procesan los formularios de HTML. (Consulte [Representación de Forms como HTML](/help/forms/developing/rendering-forms-html.md).)

Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para procesar un formulario de HTML que contenga una barra de herramientas personalizada, realice estas tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API Java de Forms.
1. Haga referencia a un archivo XML de fscmenu personalizado.
1. Representar un formulario de HTML.
1. Escriba el flujo de datos del formulario en el explorador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

**Creación de un objeto de API Java de Forms**

Para poder realizar mediante programación una operación que admita el servicio Forms, debe crear un objeto cliente Forms.

**Hacer referencia a un archivo XML de fscmenu personalizado**

Para procesar un formulario de HTML que contenga una barra de herramientas personalizada, haga referencia a un archivo XML fscmenu que describe la barra de herramientas. (Esta sección proporciona dos ejemplos de archivo XML fscmenu). Además, asegúrese de que el archivo fscmenu.xml especifica las ubicaciones de todos los archivos a los que se hace referencia correctamente. Como se mencionó anteriormente en esta sección, asegúrese de que todos los archivos estén referenciados por `FSToolBarURI` o sus ubicaciones absolutas.

**Representar un formulario de HTML**

Para procesar un formulario de HTML, especifique un diseño de formulario creado en Designer y guardado como archivo XDP. Seleccione también un tipo de transformación de HTML. Por ejemplo, puede especificar el tipo de transformación del HTML que representa un HTML dinámico para Internet Explorer 5.0 o posterior.

La renderización de un formulario de HTML también requiere valores, como valores de URI, para procesar otros tipos de formulario.

**Escribir el flujo de datos del formulario en el explorador web del cliente**

Cuando el servicio Forms procesa un formulario de HTML, devuelve un flujo de datos de formulario que debe escribir en el explorador web del cliente para que el formulario de HTML sea visible para los usuarios.

**Consulte también lo siguiente**

[Representar un formulario de HTML con una barra de herramientas personalizada mediante la API de Java](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Representación de un formulario de HTML con una barra de herramientas personalizada mediante la API de servicio web](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderización de PDF forms interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Representación de Forms como HTML](/help/forms/developing/rendering-forms-html.md)

[Creación de aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Representar un formulario de HTML con una barra de herramientas personalizada mediante la API de Java {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

Representar un formulario de HTML que contenga una barra de herramientas personalizada mediante la API de servicio de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-forms-client.jar, en la ruta de clase de su proyecto Java.

1. Creación de un objeto de API Java de Forms

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `FormsServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Hacer referencia a un archivo XML de fscmenu personalizado

   * Cree un `HTMLRenderSpec` usando su constructor.
   * Para procesar un formulario de HTML con una barra de herramientas, invoque la función `HTMLRenderSpec` del objeto `setHTMLToolbar` método y pasar un `HTMLToolbar` valor de enumeración. Por ejemplo, para mostrar una barra de herramientas vertical del HTML, pase `HTMLToolbar.Vertical`.
   * Especifique la ubicación del archivo XML fscmenu invocando la variable `HTMLRenderSpec` del objeto `setToolbarURI` y pasando un valor de cadena que especifica la ubicación URI del archivo XML.
   * Si corresponde, establezca el valor de configuración regional invocando la variable `HTMLRenderSpec` del objeto `setLocale` y pasando un valor de cadena que especifica el valor de configuración regional. El valor predeterminado es inglés.

   >[!NOTE]
   >
   >El valor Inicio rápido asociado a esta sección se establece en `fr_FR`*.*

1. Representar un formulario de HTML

   Invocar el `FormsServiceClient` del objeto `renderHTMLForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valor enum que especifica el tipo de preferencia de HTML. Por ejemplo, para procesar un formulario de HTML compatible con dynamic HTML para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un vacío `com.adobe.idp.Document` objeto.
   * La variable `HTMLRenderSpec` que almacena las opciones de tiempo de ejecución del HTML.
   * Un valor de cadena que especifica la variable `HTTP_USER_AGENT` valor de encabezado, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` objeto que almacena valores de URI necesarios para procesar un formulario de HTML.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   La variable `renderHTMLForm` el método devuelve un `FormsResult` objeto que contiene un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un `com.adobe.idp.Document` invocando el objeto `FormsResult` objeto ‘s `getOutputContent` método.
   * Obtenga el tipo de contenido de la variable `com.adobe.idp.Document` invocando su `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasar el tipo de contenido de la variable `com.adobe.idp.Document` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto que se utiliza para escribir el flujo de datos del formulario en el explorador web del cliente invocando la variable `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Cree un `java.io.InputStream` invocando el objeto `com.adobe.idp.Document` del objeto `getInputStream` método.
   * Cree una matriz de bytes y rellénela con la secuencia de datos del formulario invocando la variable `InputStream` del objeto `read` y pasando la matriz de bytes como argumento.
   * Invocar el `javax.servlet.ServletOutputStream` del objeto `write` método para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes a la `write` método.

**Consulte también lo siguiente**

[Inicio rápido (modo SOAP): Representación de un formulario de HTML con una barra de herramientas personalizada mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Representación de un formulario de HTML con una barra de herramientas personalizada mediante la API de servicio web {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

Representar un formulario de HTML que contenga una barra de herramientas personalizada mediante la API de servicio de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases proxy de Java en la ruta de clase.

1. Creación de un objeto de API Java de Forms

   Cree un `FormsService` y establezca los valores de autenticación.

1. Hacer referencia a un archivo XML de fscmenu personalizado

   * Cree un `HTMLRenderSpec` usando su constructor.
   * Para procesar un formulario de HTML con una barra de herramientas, invoque la función `HTMLRenderSpec` del objeto `setHTMLToolbar` método y pasar un `HTMLToolbar` valor de enumeración. Por ejemplo, para mostrar una barra de herramientas vertical del HTML, pase `HTMLToolbar.Vertical`.
   * Especifique la ubicación del archivo XML fscmenu invocando la variable `HTMLRenderSpec` del objeto `setToolbarURI` y pasando un valor de cadena que especifica la ubicación URI del archivo XML.
   * Si corresponde, establezca el valor de configuración regional invocando la variable `HTMLRenderSpec` del objeto `setLocale` y pasando un valor de cadena que especifica el valor de configuración regional. El valor predeterminado es inglés.

   >[!NOTE]
   >
   >El valor Inicio rápido asociado a esta sección se establece en `fr_FR`*.*

1. Representar un formulario de HTML

   Invocar el `FormsService` del objeto `renderHTMLForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valor enum que especifica el tipo de preferencia de HTML. Por ejemplo, para procesar un formulario de HTML compatible con dynamic HTML para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * A `BLOB` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`.
   * La variable `HTMLRenderSpec` que almacena las opciones de tiempo de ejecución del HTML.
   * Un valor de cadena que especifica la variable `HTTP_USER_AGENT` valor de encabezado, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`). Puede pasar una cadena vacía si no desea establecer este valor.
   * A `URLSpec` objeto que almacena valores de URI necesarios para procesar un formulario de HTML.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este parámetro es opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un vacío `com.adobe.idp.services.holders.BLOBHolder` objeto que rellena el `renderHTMLForm` método. Este valor de parámetro almacena el formulario procesado.
   * Un vacío `com.adobe.idp.services.holders.BLOBHolder` objeto que rellena el `renderHTMLForm` método. Este parámetro almacena los datos XML de salida.
   * Un vacío `javax.xml.rpc.holders.LongHolder` objeto que rellena el `renderHTMLForm` método. Este argumento almacena el número de páginas del formulario.
   * Un vacío `javax.xml.rpc.holders.StringHolder` objeto que rellena el `renderHTMLForm` método. Este argumento almacena el valor de configuración regional.
   * Un vacío `javax.xml.rpc.holders.StringHolder` objeto que rellena el `renderHTMLForm` método. Este argumento almacena el valor de renderización del HTML que se utiliza.
   * Un vacío `com.adobe.idp.services.holders.FormsResultHolder` que contendrá los resultados de esta operación.

   La variable `renderHTMLForm` rellena el `com.adobe.idp.services.holders.FormsResultHolder` objeto que se pasa como el último valor de argumento con un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un `FormResult` obteniendo el valor de `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value` miembro de datos.
   * Cree un `BLOB` objeto que contiene datos de formulario invocando la variable `FormsResult` del objeto `getOutputContent` método.
   * Obtenga el tipo de contenido de la variable `BLOB` invocando su `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasar el tipo de contenido de la variable `BLOB` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto que se utiliza para escribir el flujo de datos del formulario en el explorador web del cliente invocando la variable `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Cree una matriz de bytes y rellénela invocando la variable `BLOB` del objeto `getBinaryData` método. Esta tarea asigna el contenido de la variable `FormsResult` a la matriz de bytes.
   * Invocar el `javax.servlet.http.HttpServletResponse` del objeto `write` método para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes a la `write` método.

**Consulte también lo siguiente**

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
