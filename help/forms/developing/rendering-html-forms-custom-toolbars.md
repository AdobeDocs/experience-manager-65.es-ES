---
title: Procesar formularios HTML con barras de herramientas personalizadas
seo-title: Rendering HTML Forms with CustomToolbars
description: Utilice el servicio Forms para personalizar una barra de herramientas que se procesa con un formulario de HTML. Puede procesar un formulario de HTML con una barra de herramientas personalizada mediante la API de Java y una API de servicio web.
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
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2340'
ht-degree: 1%

---

# Procesar formularios HTML con barras de herramientas personalizadas {#rendering-html-forms-with-customtoolbars}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

## Representar Forms de HTML con barras de herramientas personalizadas {#rendering-html-forms-with-custom-toolbars}

El servicio Forms permite personalizar una barra de herramientas que se procesa con un formulario de HTML. Se puede personalizar una barra de herramientas para modificar su aspecto al anular los estilos CSS predeterminados y agregar un comportamiento dinámico al anular los scripts de Java. Una barra de herramientas se personaliza mediante un archivo XML denominado fscmenu.xml. De forma predeterminada, el servicio Forms recupera este archivo desde una ubicación URI especificada internamente.

>[!NOTE]
>
>Esta ubicación de URI se encuentra en el archivo adobe-forms-core.jar, que se encuentra en el archivo adobe-forms-dsc.jar. El archivo adobe-forms-dsc.jar se encuentra en la carpeta C:\Adobe\Adobe_Experience_Manager_forms\ (C:\ es el directorio de instalación). Puede utilizar una herramienta de extracción de archivos, como Win RAR, para abrir Adobe.

Puede copiar el archivo fscmenu.xml desde esta ubicación, modificarlo para que se ajuste a sus necesidades y, a continuación, colocarlo en una ubicación URI personalizada. A continuación, mediante la API del servicio de Forms, establezca las opciones en tiempo de ejecución que resultan en el servicio de Forms mediante el archivo fscmenu.xml desde la ubicación especificada. Estas acciones hacen que el servicio Forms procese un formulario de HTML que tiene una barra de herramientas personalizada.

Además del archivo fscmenu.xml, también necesita obtener los siguientes archivos:

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS es la secuencia de comandos Java asociada a cada nodo. Es necesario suministrar uno para el `div#fscmenu` nodo y, opcionalmente, para `ul#fscmenuItem` nodos. Los archivos JS implementan la funcionalidad principal de la barra de herramientas y funcionan los archivos predeterminados.

fscCSS es una hoja de estilos asociada a un nodo concreto. Los estilos de los archivos CSS especifican el aspecto de la barra de herramientas. *fscVCSS* es una hoja de estilos para una barra de herramientas vertical que se muestra a la izquierda del formulario de HTML procesado. *fscIECSS* es una hoja de estilos que se utiliza para los formularios de HTML que se representan en Internet Explorer.

Asegúrese de que se hace referencia a todos los archivos anteriores en el archivo fscmenu.xml. Es decir, en el archivo fscmenu.xml, especifique las ubicaciones de los URI que apuntarán a estos archivos para que el servicio de Forms pueda localizarlos. De forma predeterminada, estos archivos están disponibles en ubicaciones de URI que comienzan con palabras clave internas `FSWebRoot` o `ApplicationWebRoot`.

Para personalizar la barra de herramientas, reemplace las palabras clave por la palabra clave externa `FSToolBarURI`. Esta palabra clave representa el URI que se pasa al servicio Forms en tiempo de ejecución (este método se muestra más adelante en esta sección).

También puede especificar las ubicaciones absolutas de estos archivos JS y CSS, como https://www.mycompany.com/scripts/misc/fscmenu.js. En este caso, no es necesario utilizar el `FSToolBarURI` palabra clave.

>[!NOTE]
>
>No se recomienda mezclar las formas en que se hace referencia a estos archivos. Es decir, se debe hacer referencia a todos los URI utilizando el método `FSToolBarURI` palabra clave o una ubicación absoluta.

Puede obtener los archivos JS y CSS abriendo adobe-forms-&lt;appserver>archivo .ear. Dentro de este archivo, abra adobe-forms-res.war. Todos estos archivos se encuentran en el archivo WAR. El adobe-forms-&lt;appserver>AEM El archivo .ear se encuentra en la carpeta de instalación de formularios de la aplicación (C:\ es el directorio de instalación). Puede abrir adobe-forms-&lt;appserver>.ear utilizando una herramienta de extracción de archivos como WinRAR.

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

* Cambiar los valores de `fscJS`, `fscCSS`, `fscVCSS`, `fscIECSS` atributos (en el archivo fscmenu.xml) para reflejar las ubicaciones personalizadas de los archivos a los que se hace referencia mediante uno de los métodos que se describen en esta sección (por ejemplo, `fscJS="FSToolBarURI/scripts/fscmenu.js"`).
* Se deben especificar todos los archivos CSS y JS. Si no se modifica ninguno de los archivos, proporcione el predeterminado en la ubicación personalizada. Puede obtener los archivos predeterminados abriendo varios archivos como se describe en esta sección.
* Se permite proporcionar una referencia absoluta (por ejemplo, https://www.example.com/scripts/custom-vertical-fscmenu.css) para cualquier archivo.
* Los archivos JS y CSS que `div#fscmenu` Los requisitos de nodo son esenciales para la funcionalidad de la barra de herramientas. Individual `ul#fscmenuItem` Los nodos de pueden tener o no archivos JS o CSS compatibles.

**Cambio del valor local**

Al personalizar una barra de herramientas, puede cambiar su valor de configuración regional. Es decir, puede mostrarlo en otro idioma. La siguiente ilustración muestra una barra de herramientas personalizada que se muestra en francés.

>[!NOTE]
>
>No es posible crear una barra de herramientas personalizada en más de un idioma. Las barras de herramientas no pueden utilizar archivos XML diferentes basados en la configuración regional.

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
>Los tutoriales rápidos asociados a esta sección utilizan este archivo XML para mostrar una barra de herramientas personalizada en francés, como se muestra en la ilustración anterior.

Especifique también un valor de configuración regional válido invocando el `HTMLRenderSpec` del objeto `setLocale` y pasando un valor de cadena que especifica el valor de configuración regional. Por ejemplo, pase `fr_FR` para especificar francés. El servicio Forms está empaquetado con barras de herramientas localizadas.

>[!NOTE]
>
>Antes de procesar un formulario de HTML que utilice una barra de herramientas personalizada, debe saber cómo se procesan los formularios de HTML. (Consulte [Representar Forms como HTML](/help/forms/developing/rendering-forms-html.md).)

Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para procesar un formulario de HTML que contenga una barra de herramientas personalizada, realice estas tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de Java de Forms.
1. Hacer referencia a un archivo XML fscmenu personalizado.
1. Procesar un formulario de HTML.
1. Escriba el flujo de datos del formulario en el explorador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

**Creación de un objeto de API de Java de Forms**

Para poder realizar mediante programación una operación compatible con el servicio Forms, debe crear un objeto de cliente de Forms.

**Hacer referencia a un archivo XML fscmenu personalizado**

Para procesar un formulario de HTML que contenga una barra de herramientas personalizada, haga referencia a un archivo XML fscmenu que describa la barra de herramientas. (Esta sección proporciona dos ejemplos de un archivo XML fscmenu.) Asegúrese también de que el archivo fscmenu.xml especifica correctamente las ubicaciones de todos los archivos a los que se hace referencia. Como se mencionó anteriormente en esta sección, asegúrese de que todas las referencias de los archivos sean `FSToolBarURI` o sus ubicaciones absolutas.

**Procesar un formulario de HTML**

Para procesar un formulario de HTML, especifique un diseño de formulario creado en Designer y guardado como archivo XDP. Seleccione también un tipo de transformación de HTML. Por ejemplo, puede especificar el tipo de transformación de HTML que procesa un HTML dinámico para Internet Explorer 5.0 o posterior.

El procesamiento de un formulario HTML también requiere valores, como valores URI para el procesamiento de otros tipos de formulario.

**Escribir el flujo de datos del formulario en el explorador web del cliente**

Cuando el servicio Forms procesa un formulario de HTML, devuelve un flujo de datos de formulario que debe escribir en el explorador web del cliente para que el formulario de HTML sea visible para los usuarios.

**Consulte también**

[Procesar un formulario de HTML con una barra de herramientas personalizada mediante la API de Java](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Representar un formulario de HTML con una barra de herramientas personalizada mediante la API de servicio web](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Procesar formularios PDF interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Procesar formularios como HTML](/help/forms/developing/rendering-forms-html.md)

[Crear aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Procesar un formulario de HTML con una barra de herramientas personalizada mediante la API de Java {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

Procese un formulario de HTML que contenga una barra de herramientas personalizada mediante la API del servicio de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clase del proyecto Java.

1. Creación de un objeto de API de Java de Forms

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `FormsServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Hacer referencia a un archivo XML fscmenu personalizado

   * Crear un `HTMLRenderSpec` mediante su constructor.
   * Para procesar un formulario de HTML con una barra de herramientas, invoque la variable `HTMLRenderSpec` del objeto `setHTMLToolbar` método y pase un `HTMLToolbar` valor de enumeración. Por ejemplo, para mostrar una barra de herramientas de HTML vertical, pase `HTMLToolbar.Vertical`.
   * Especifique la ubicación del archivo XML fscmenu invocando la variable `HTMLRenderSpec` del objeto `setToolbarURI` y pasando un valor de cadena que especifica la ubicación URI del archivo XML.
   * Si procede, establezca el valor de configuración regional invocando la variable `HTMLRenderSpec` del objeto `setLocale` y pasando un valor de cadena que especifica el valor de configuración regional. El valor predeterminado es inglés.

   >[!NOTE]
   >
   >Los inicios rápidos asociados con esta sección establecen este valor como `fr_FR`*.*

1. Procesar un formulario de HTML

   Invoque el `FormsServiceClient` del objeto `renderHTMLForm` y pasar los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta de acceso completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valor de enumeración que especifica el tipo de preferencia del HTML. Por ejemplo, para procesar un formulario de HTML compatible con dynamic HTML para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un vacío `com.adobe.idp.Document` objeto.
   * El `HTMLRenderSpec` que almacena las opciones de tiempo de ejecución de HTML.
   * Un valor de cadena que especifica la variable `HTTP_USER_AGENT` valor de encabezado, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` que almacena valores de URI necesarios para procesar un formulario de HTML.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El `renderHTMLForm` El método devuelve un valor `FormsResult` que contiene un flujo de datos de formulario que debe escribirse en el explorador web cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Crear un `com.adobe.idp.Document` invocando el objeto de `FormsResult` objeto ‘s `getOutputContent` método.
   * Obtenga el tipo de contenido del `com.adobe.idp.Document` invocando su objeto `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasando el tipo de contenido del `com.adobe.idp.Document` objeto.
   * Crear un `javax.servlet.ServletOutputStream` objeto que se utiliza para escribir el flujo de datos de formulario en el explorador web del cliente invocando el `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Crear un `java.io.InputStream` invocando el objeto de `com.adobe.idp.Document` del objeto `getInputStream` método.
   * Cree una matriz de bytes y rellénela con el flujo de datos de formulario invocando el método `InputStream` del objeto `read` y pasando la matriz de bytes como argumento.
   * Invoque el `javax.servlet.ServletOutputStream` del objeto `write` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes a `write` método.

**Consulte también**

[Inicio rápido (modo SOAP): Procesamiento de un formulario de HTML con una barra de herramientas personalizada mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Representar un formulario de HTML con una barra de herramientas personalizada mediante la API de servicio web {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

Procese un formulario de HTML que contenga una barra de herramientas personalizada mediante la API del servicio Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases de proxy Java en la ruta de clase.

1. Creación de un objeto de API de Java de Forms

   Crear un `FormsService` y establezca los valores de autenticación.

1. Hacer referencia a un archivo XML fscmenu personalizado

   * Crear un `HTMLRenderSpec` mediante su constructor.
   * Para procesar un formulario de HTML con una barra de herramientas, invoque la variable `HTMLRenderSpec` del objeto `setHTMLToolbar` método y pase un `HTMLToolbar` valor de enumeración. Por ejemplo, para mostrar una barra de herramientas de HTML vertical, pase `HTMLToolbar.Vertical`.
   * Especifique la ubicación del archivo XML fscmenu invocando la variable `HTMLRenderSpec` del objeto `setToolbarURI` y pasando un valor de cadena que especifica la ubicación URI del archivo XML.
   * Si procede, establezca el valor de configuración regional invocando la variable `HTMLRenderSpec` del objeto `setLocale` y pasando un valor de cadena que especifica el valor de configuración regional. El valor predeterminado es inglés.

   >[!NOTE]
   >
   >Los inicios rápidos asociados con esta sección establecen este valor como `fr_FR`*.*

1. Procesar un formulario de HTML

   Invoque el `FormsService` del objeto `renderHTMLForm` y pasar los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta de acceso completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valor de enumeración que especifica el tipo de preferencia del HTML. Por ejemplo, para procesar un formulario de HTML compatible con dynamic HTML para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * A `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar los datos, apruebe `null`.
   * El `HTMLRenderSpec` que almacena las opciones de tiempo de ejecución de HTML.
   * Un valor de cadena que especifica la variable `HTTP_USER_AGENT` valor de encabezado, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`). Puede pasar una cadena vacía si no desea establecer este valor.
   * A `URLSpec` que almacena valores de URI necesarios para procesar un formulario de HTML.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este parámetro es opcional y puede especificar `null` si no tiene intención de adjuntar archivos al formulario.
   * Un vacío `com.adobe.idp.services.holders.BLOBHolder` objeto que se rellena con la variable `renderHTMLForm` método. Este valor de parámetro almacena el formulario procesado.
   * Un vacío `com.adobe.idp.services.holders.BLOBHolder` objeto que se rellena con la variable `renderHTMLForm` método. Este parámetro almacena los datos XML de salida.
   * Un vacío `javax.xml.rpc.holders.LongHolder` objeto que se rellena con la variable `renderHTMLForm` método. Este argumento almacena el número de páginas del formulario.
   * Un vacío `javax.xml.rpc.holders.StringHolder` objeto que se rellena con la variable `renderHTMLForm` método. Este argumento almacena el valor de configuración regional.
   * Un vacío `javax.xml.rpc.holders.StringHolder` objeto que se rellena con la variable `renderHTMLForm` método. Este argumento almacena el valor de procesamiento del HTML que se utiliza.
   * Un vacío `com.adobe.idp.services.holders.FormsResultHolder` que contendrá los resultados de esta operación.

   El `renderHTMLForm` rellena el método `com.adobe.idp.services.holders.FormsResultHolder` que se pasa como el último valor de argumento con un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Crear un `FormResult` al obtener el valor de la variable `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value` miembro de datos.
   * Crear un `BLOB` que contiene datos de formulario invocando el `FormsResult` del objeto `getOutputContent` método.
   * Obtenga el tipo de contenido del `BLOB` invocando su objeto `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasando el tipo de contenido del `BLOB` objeto.
   * Crear un `javax.servlet.ServletOutputStream` objeto que se utiliza para escribir el flujo de datos de formulario en el explorador web del cliente invocando el `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Cree una matriz de bytes y rellénela invocando el método `BLOB` del objeto `getBinaryData` método. Esta tarea asigna el contenido del `FormsResult` a la matriz de bytes.
   * Invoque el `javax.servlet.http.HttpServletResponse` del objeto `write` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes a `write` método.

**Consulte también**

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
