---
title: Representación de Forms como HTML
seo-title: Rendering Forms as HTML
description: Utilice el servicio Forms para procesar formularios como HTML en respuesta a una solicitud HTTP de un explorador web. Puede utilizar la API de Java y la API de servicio web para procesar formularios como HTML.
seo-description: Use the Forms service to render forms as HTML in response to an HTTP request from a web browser. You can use the Java API and Web Service API to render forms as HTML.
uuid: bd8edb6f-333b-4ceb-9877-618f5377f56f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 669ede46-ea55-444b-a23f-23a86e5aff8e
role: Developer
exl-id: e6887e45-a472-41d4-9620-c56fd5b72b4c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4150'
ht-degree: 1%

---

# Representación de Forms como HTML {#rendering-forms-as-html}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

El servicio Forms procesa los formularios como HTML en respuesta a una solicitud HTTP de un explorador web. Una ventaja de procesar un formulario como HTML es que el equipo en el que se encuentra el explorador web del cliente no requiere Adobe Reader, Acrobat ni Flash Player (para guías de formulario (obsoleto)).

Para procesar un formulario como HTML, el diseño de formulario debe guardarse como archivo XDP. Un diseño de formulario guardado como archivo PDF no se puede representar como HTML. Cuando desarrolle un diseño de formulario en Designer que se procese como HTML, tenga en cuenta los siguientes criterios:

* No utilice las propiedades de borde de un objeto para dibujar líneas, cuadros o cuadrículas en el formulario. Algunos exploradores no alinean los bordes tal como se muestran en la vista previa de Los objetos pueden aparecer en capas diferentes o desplazar otros objetos de la posición prevista.
* Puede utilizar líneas, rectángulos y círculos para definir el fondo.
* Dibuje texto ligeramente más grande de lo que parece ser necesario para dar cabida al texto. Algunos exploradores web no muestran el texto de forma legible.

>[!NOTE]
>
>Cuando se procesa un formulario que contiene imágenes de TIFF mediante la variable `FormServiceClient` del objeto `(Deprecated) renderHTMLForm` y `renderHTMLForm2` , las imágenes de TIFF no están visibles en el formulario de HTML procesado que se muestra en los navegadores Internet Explorer o Mozilla Firefox. Estos exploradores no proporcionan compatibilidad nativa con imágenes TIFF.

## páginas del HTML {#html-pages}

Cuando se procesa un diseño de formulario como formulario de HTML, cada subformulario de segundo nivel se procesa como una página de HTML (panel). Puede ver la jerarquía de un subformulario en Designer. Los subformularios secundarios que pertenecen al subformulario raíz (el nombre predeterminado de un subformulario raíz es formulario1) son los subformularios del panel. El siguiente ejemplo muestra los subformularios de un diseño de formulario.

```java
     form1
         Master Pages
         PanelSubform1
             NestedDynamicSubform
                 TextEdit1
         PanelSubform2
             TextEdit1
         PanelSubform3
             TextEdit1
         PanelSubform4
             TextEdit1
```

Cuando los diseños de formulario se representan como formularios HTML, los paneles no se limitan a un tamaño de página determinado. Si tiene subformularios dinámicos, deben anidarse en el subformulario del panel. Los subformularios dinámicos pueden expandirse a un número infinito de páginas HTML.

Cuando un formulario se procesa como un formulario HTML, los tamaños de página (necesarios para paginar los formularios representados como PDF) no tienen significado. Dado que un formulario con presentación flexible puede expandirse a un número infinito de páginas HTML, es importante evitar los pies de página en la página de formato. Un pie de página debajo del área de contenido de una página de formato puede sobrescribir el contenido del HTML que sobrepasa los límites de la página.

Debe moverse explícitamente de un panel a otro utilizando la variable `xfa.host.pageUp` y `xfa.host.pageDown` métodos. Para cambiar de página, envíe un formulario al servicio Forms y haga que el servicio Forms vuelva a procesar el formulario en el dispositivo cliente, normalmente un explorador Web.

>[!NOTE]
>
>El proceso de enviar un formulario al servicio Forms y, a continuación, hacer que el servicio Forms vuelva a procesar el formulario en el dispositivo cliente, se denomina datos de recorte redondos al servidor.

>[!NOTE]
>
>Si desea personalizar el aspecto del botón Firma digital del HTML en un formulario de HTML, debe cambiar las siguientes propiedades en el archivo fscdigsig.css (en el archivo adobe-forms-ds.ear > adobe-forms-ds.war):

**.fsc-ds-ssb**: Esta hoja de estilo es aplicable en el caso de un campo de signo en blanco.

**.fsc-ds-ssv**: Esta hoja de estilo es aplicable en el caso de un campo de signo válido .

**.fsc-ds-ssc**: Esta hoja de estilo es aplicable en el caso de un campo de signo válido pero los datos han cambiado.

**.fsc-ds-ssi**: Esta hoja de estilo es aplicable en el caso de un campo de signo no válido.

**.fsc-ds-popup-bg**: No se está utilizando esta propiedad de hoja de estilo.

**.fsc-ds-popup-btn**: No se está utilizando esta propiedad de hoja de estilo.

## Ejecución de secuencias de comandos {#running-scripts}

Un autor de formularios especifica si se ejecuta una secuencia de comandos en el servidor o en el cliente. El servicio Forms crea un entorno de procesamiento de eventos distribuido para la ejecución de la inteligencia de formularios que se puede distribuir entre el cliente y el servidor mediante el uso de `runAt` atributo. Para obtener información sobre este atributo o la creación de secuencias de comandos dentro de los diseños de formulario, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

El servicio Forms puede ejecutar secuencias de comandos mientras se procesa el formulario. Como resultado, puede rellenar previamente un formulario con datos conectándose a una base de datos o a servicios Web que pueden no estar disponibles en el cliente. También puede establecer un botón `Click` para que se ejecute en el servidor de modo que el cliente redondee los datos de viaje al servidor. Esto permite al cliente ejecutar secuencias de comandos que pueden requerir recursos del servidor, como una base de datos empresarial, mientras un usuario interactúa con un formulario. Para los formularios HTML, las secuencias de comandos de formcalc se pueden ejecutar solo en el servidor. Como resultado, debe marcar estos scripts para que se ejecuten en `server` o `both`.

Puede diseñar formularios que se desplacen entre páginas (paneles) llamando a `xfa.host.pageUp` y `xfa.host.pageDown` métodos. Esta secuencia de comandos se coloca en el nodo `Click` y `runAt` se configura como `Both`. El motivo que elija `Both` es para que Adobe Reader o Acrobat (en el caso de formularios procesados como PDF) puedan cambiar de página sin ir al servidor, y los formularios de HTML pueden cambiar de página recortando datos al servidor. Es decir, se envía un formulario al servicio Forms y se vuelve a procesar un formulario como HTML con la nueva página mostrada.

Se recomienda no asignar a las variables de secuencia de comandos y a los campos de formulario los mismos nombres, como el elemento. Es posible que algunos exploradores web, como Internet Explorer, no inicialicen una variable con el mismo nombre que un campo de formulario que genere un error de secuencia de comandos. Se recomienda dar nombres diferentes a los campos de formulario y a las variables de secuencia de comandos.

Cuando se procesen formularios HTML que contengan tanto la funcionalidad de navegación de página como las secuencias de comandos de formulario (por ejemplo, supongamos que una secuencia de comandos recupera los datos de campo de una base de datos cada vez que se procesa el formulario), asegúrese de que la secuencia de comandos del formulario se encuentra en el suceso form:calculate en lugar del suceso form:ready .

Las secuencias de comandos de formulario que se encuentran en el suceso form:ready se ejecutan solo una vez durante la renderización inicial del formulario y no se ejecutan para recuperaciones de página posteriores. Por el contrario, el suceso form:calculate se ejecuta para cada navegación de página en la que se procese el formulario.

>[!NOTE]
En un formulario de varias páginas, los cambios realizados por JavaScript en una página no se conservan si se mueve a otra página.

Puede invocar secuencias de comandos personalizadas antes de enviar un formulario. Esta función funciona en todos los navegadores disponibles. Sin embargo, solo se puede utilizar cuando los usuarios procesen el formulario de HTML que tenga su `Output Type` propiedad establecida en `Form Body`. No funcionará cuando la variable `Output Type` es `Full HTML`. Consulte Configuración de formularios en la ayuda de administración para ver los pasos necesarios para configurar esta función.

Primero debe definir una función de llamada de retorno a la que se llame antes de enviar el formulario, donde el nombre de la función es `_user_onsubmit`. Se da por hecho que la función no emitirá ninguna excepción o, si lo hace, se ignorará la excepción. Se recomienda colocar la función JavaScript en la sección head del html; sin embargo, puede declararlo en cualquier lugar antes del final de las etiquetas de script que incluyen `xfasubset.js`.

Cuando formserver procesa un XDP que contiene una lista desplegable, además de crear la lista desplegable, también crea dos campos de texto ocultos. Estos campos de texto almacenan los datos de la lista desplegable (uno almacena el nombre para mostrar de las opciones y otro almacena el valor de las opciones). Por lo tanto, cada vez que un usuario envía el formulario, se envían todos los datos de la lista desplegable. Suponiendo que no desee enviar tantos datos cada vez, puede escribir una secuencia de comandos personalizada para deshabilitarla. Por ejemplo: El nombre de la lista desplegable es `drpOrderedByStateProv` y se ajusta en el encabezado del subformulario. El nombre del elemento de entrada del HTML será `header[0].drpOrderedByStateProv[0]`. El nombre de los campos ocultos que almacenan y envían los datos de la lista desplegable tiene los siguientes nombres: `header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

Puede deshabilitar estos elementos de entrada de la siguiente manera si no desea publicar los datos. `var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature function _user_onsubmit() { var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); elems[0].disabled = true; elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); elems[0].disabled = true; }`

```java
header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]
```

```java
var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature
    function _user_onsubmit() {
    var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]");
    elems[0].disabled = true;
    elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]");
    elems[0].disabled = true;
    }
```

## Subconjuntos XFA {#xfa-subsets}

Al crear diseños de formulario para procesarlos como HTML, debe restringir las secuencias de comandos al subconjunto XFA para secuencias de comandos en lenguaje JavaScript.

Las secuencias de comandos que se ejecutan en el cliente o en el servidor deben escribirse en el subconjunto XFA. Las secuencias de comandos que se ejecutan en el servidor pueden utilizar el modelo completo de secuencias de comandos XFA y también usar FormCalc. Para obtener información sobre el uso de JavaScript, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

Cuando se ejecutan secuencias de comandos en el cliente, solo el panel actual que se muestra puede utilizar la secuencia de comandos; por ejemplo, no se puede crear una secuencia de comandos para los campos ubicados en el panel A cuando se muestra el panel B. Al ejecutar secuencias de comandos en el servidor, se puede acceder a todos los paneles.

También debe tener cuidado al utilizar expresiones del Modelo de objetos de secuencias de comandos (SOM) dentro de secuencias de comandos que se ejecutan en el cliente. Solo se admite un subconjunto simplificado de expresiones SOM con secuencias de comandos que se ejecutan en el cliente.

## Temporización del evento {#event-timing}

El subconjunto XFA define los eventos XFA que se asignan a eventos de HTML. Hay una ligera diferencia de comportamiento en el tiempo de los sucesos calculate y validate . En un explorador web, se ejecuta un suceso full calculate al salir de un campo. Los eventos de cálculo no se ejecutan automáticamente cuando se realiza un cambio en un valor de campo. Puede forzar un suceso calculate llamando a la función `xfa.form.execCalculate` método.

En un explorador web, los sucesos validate solo se ejecutan al salir de un campo o al enviar un formulario. Puede forzar un evento de validación utilizando la variable `xfa.form.execValidate` método.

Forms mostrado en un explorador web (a diferencia de Adobe Reader o Acrobat) se ajusta a la prueba XFA null (errores o advertencias) para los campos obligatorios.

* Si la prueba nula produce un error y sale de un campo sin especificar ningún valor, se muestra un cuadro de mensaje y se le reasigna al campo después de hacer clic en Aceptar.
* Si una prueba nula genera una advertencia y sale de un campo sin especificar ningún valor, se le pedirá que haga clic en Aceptar o en Cancelar, lo que le dará la opción de continuar sin especificar ningún valor o volver al campo para introducir un valor.

Para obtener más información sobre una prueba nula, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Botones de formulario {#form-buttons}

Al hacer clic en un botón de envío, los datos del formulario se envían al servicio Forms y representan el final del procesamiento del formulario. La variable `preSubmit` se puede configurar para que se ejecute en el cliente o servidor. La variable `preSubmit` se ejecuta antes del envío del formulario si está configurado para ejecutarse en el cliente. De lo contrario, la función `preSubmit` se ejecuta en el servidor durante el envío del formulario. Para obtener más información sobre la variable `preSubmit` evento, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

Si un botón no tiene ninguna secuencia de comandos del lado del cliente asociada, los datos se envían al servidor, los cálculos se realizan en el servidor y se regenera el formulario del HTML. Si un botón contiene una secuencia de comandos del lado del cliente, los datos no se envían al servidor y la secuencia de comandos del lado del cliente se ejecuta en el explorador web.

## Navegador web HTML 4.0 {#html-4-0-web-browser}

Un explorador web que solo admita HTML 4.0 no puede admitir el modelo de secuencias de comandos del lado del cliente de subconjuntos XFA. Al crear un diseño de formulario para que funcione tanto en HTML 4.0 como en HTML MSDHTML o CSS2, una secuencia de comandos que esté marcada para ejecutarse en el cliente se ejecutará en el servidor. Por ejemplo, supongamos que un usuario hace clic en un botón ubicado en un formulario mostrado en un explorador web HTML 4.0. En este caso, los datos del formulario se envían al servidor en el que se ejecuta la secuencia de comandos del lado del cliente.

Se recomienda colocar la lógica del formulario en sucesos calculate , que se ejecutan en el servidor del HTML 4.0 y en el cliente del HTML MSDHTML o CSS2.

## Mantenimiento de los cambios de presentación {#maintaining-presentation-changes}

A medida que se desplaza entre páginas del HTML (paneles), solo se mantiene el estado de los datos. La configuración, como el color de fondo o la configuración de campo obligatoria, no se mantiene (si no es la configuración inicial). Para mantener el estado de presentación, debe crear campos (normalmente ocultos) que representen el estado de presentación de los campos. Si agrega una secuencia de comandos a la sección `Calculate` que cambia la presentación en función de los valores de campo ocultos, puede conservar el estado de presentación al moverse de una página a otra (paneles) del HTML.

La siguiente secuencia de comandos mantiene la variable `fillColor` de un campo basado en el valor de `hiddenField`. Supongamos que esta secuencia de comandos se encuentra en la sección `Calculate` evento.

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
Los objetos estáticos no se muestran en un formulario HTML representado cuando se anidan dentro de una celda de tabla. Por ejemplo, un círculo y un rectángulo anidados dentro de una celda de tabla no se muestran dentro de un formulario de HTML de renderización. Sin embargo, estos mismos objetos estáticos se muestran correctamente cuando se encuentran fuera de la tabla.

## Firma digital de formularios HTML {#digitally-signing-html-forms}

No se puede firmar un formulario de HTML que contenga un campo de firma digital si el formulario se procesa como una de las siguientes transformaciones de HTML:

* AHTML
* HTML4
* StaticHTML
* NoScriptXHTML

Para obtener información acerca de la firma digital de un documento, consulte [Firma y certificación digitales de documentos](/help/forms/developing/digitally-signing-certifying-documents.md)

## Representación de un formulario XHTML compatible con las directrices de accesibilidad {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

Puede procesar un formulario de HTML completo que cumpla las directrices de accesibilidad. Es decir, el formulario se procesa con etiquetas de HTML completas, a diferencia del formulario de HTML que se procesa con etiquetas de cuerpo (no con una página de HTML completa).

## Validación de datos de formulario {#validating-form-data}

Se recomienda limitar el uso de las reglas de validación para los campos de formulario al procesar el formulario como un formulario de HTML. Es posible que algunas reglas de validación no sean compatibles con los formularios de HTML. Por ejemplo, cuando se aplica un patrón de validación de MM-DD-AAAA a una `Date/Time` campo ubicado en un diseño de formulario procesado como formulario HTML, no funciona correctamente, aunque la fecha esté escrita correctamente. Sin embargo, este patrón de validación funciona correctamente para los formularios procesados como PDF.

>[!NOTE]
Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para procesar un formulario de HTML, realice los pasos siguientes:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Establezca las opciones de tiempo de ejecución del HTML.
1. Representar un formulario de HTML.
1. Escriba el flujo de datos del formulario en el explorador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de cliente de Forms**

Para poder importar datos mediante programación a una API de PDF formClient, debe crear un cliente de servicio de integración de datos de formulario. Al crear un cliente de servicio, define la configuración de conexión necesaria para invocar un servicio.

**Establecer opciones de tiempo de ejecución del HTML**

Las opciones de tiempo de ejecución del HTML se definen al procesar un formulario de HTML. Por ejemplo, se puede agregar una barra de herramientas a un formulario de HTML para que los usuarios puedan seleccionar archivos adjuntos ubicados en el equipo cliente o recuperar archivos adjuntos procesados con el formulario de HTML. De forma predeterminada, una barra de herramientas del HTML está deshabilitada. Para agregar una barra de herramientas a un formulario de HTML, debe definir mediante programación las opciones en tiempo de ejecución. De forma predeterminada, una barra de herramientas de HTML consta de los siguientes botones:

* `Home`: Proporciona un vínculo a la raíz web de la aplicación.
* `Upload`: Proporciona una interfaz de usuario para seleccionar archivos que se adjuntarán al formulario actual.
* `Download`: Proporciona una interfaz de usuario para mostrar los archivos adjuntos.

Cuando aparece una barra de herramientas de HTML en un formulario de HTML, un usuario puede seleccionar un máximo de diez archivos para enviar junto con los datos del formulario. Una vez enviados los archivos, el servicio de Forms puede recuperarlos.

Al procesar un formulario como HTML, puede especificar un valor de usuario-agente. Un valor de usuario-agente proporciona información del sistema y del explorador. Se trata de un valor opcional y puede pasar un valor de cadena vacío. El formulario Rendering an HTML using the Java API quick start muestra cómo obtener un valor de agente de usuario y utilizarlo para procesar un formulario como HTML.

Las direcciones URL HTTP en las que se publican los datos del formulario se pueden especificar estableciendo la dirección URL de destino mediante la API de cliente de servicio de Forms o en el botón Enviar incluido en el diseño de formulario XDP. Si la dirección URL de destino se especifica en el diseño de formulario, no configure ningún valor con la API de cliente del servicio de Forms.

>[!NOTE]
Representar un formulario de HTML con una barra de herramientas es opcional.

>[!NOTE]
Si procesa un formulario AHTML, se recomienda no agregar ninguna barra de herramientas al formulario.

**Representar un formulario de HTML**

Para procesar un formulario de HTML, debe especificar un diseño de formulario creado en Designer y guardado como archivo XDP. También debe seleccionar un tipo de transformación de HTML. Por ejemplo, puede especificar el tipo de transformación del HTML que representa un HTML dinámico para Internet Explorer 5.0 o posterior.

La renderización de un formulario de HTML también requiere valores, como valores de URI necesarios para procesar otros tipos de formulario.

**Escribir el flujo de datos del formulario en el explorador web del cliente**

Cuando el servicio Forms procesa un formulario de HTML, devuelve un flujo de datos de formulario que debe escribir en el explorador web del cliente. Cuando se escribe en el explorador web del cliente, el formulario de HTML es visible para el usuario.

**Consulte también lo siguiente**

[Representar un formulario como HTML mediante la API de Java](#render-a-form-as-html-using-the-java-api)

[Representar un formulario como HTML mediante la API de servicio web](#render-a-form-as-html-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderización de PDF forms interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Representación de Forms HTML con barras de herramientas personalizadas](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[Creación de aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Representar un formulario como HTML mediante la API de Java {#render-a-form-as-html-using-the-java-api}

Representar un formulario de HTML mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-forms-client.jar, en la ruta de clase de su proyecto Java.

1. Creación de un objeto de API de cliente de Forms

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `FormsServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Establecer opciones de tiempo de ejecución del HTML

   * Cree un `HTMLRenderSpec` usando su constructor.
   * Para procesar un formulario de HTML con una barra de herramientas, invoque la función `HTMLRenderSpec` del objeto `setHTMLToolbar` método y pasar un `HTMLToolbar` valor de enumeración. Por ejemplo, para mostrar una barra de herramientas vertical del HTML, pase `HTMLToolbar.Vertical`.
   * Para definir el valor de configuración regional para el formulario de HTML, invoque la variable `HTMLRenderSpec` del objeto `setLocale` y pase un valor de cadena que especifique el valor de configuración regional. (Se trata de una configuración opcional).
   * Para procesar el formulario del HTML con etiquetas de HTML completas, invoque la variable `HTMLRenderSpec` del objeto `setOutputType` método y pase `OutputType.FullHTMLTags`. (Se trata de una configuración opcional).

   >[!NOTE]
   Forms no se procesa correctamente en el HTML cuando la variable `StandAlone` la opción es `true` y `ApplicationWebRoot` hace referencia a un servidor que no es el servidor de aplicaciones J2EE que hospeda AEM Forms (la variable `ApplicationWebRoot` se especifica utilizando la variable `URLSpec` objeto que se pasa al `FormsServiceClient` del objeto `(Deprecated) renderHTMLForm` método). Cuando la variable `ApplicationWebRoot` es otro servidor del que aloja AEM Forms, el valor del URI raíz web en la consola de administración debe establecerse como el valor URI de la aplicación web del formulario. Para ello, inicie sesión en la consola de administración, haga clic en Servicios > Forms y establezca el URI de la raíz web como https://server-name:port/FormServer. A continuación, guarde la configuración.

1. Representar un formulario de HTML

   Invocar el `FormsServiceClient` del objeto `(Deprecated) renderHTMLForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valor enum que especifica el tipo de preferencia de HTML. Por ejemplo, para procesar un formulario de HTML compatible con dynamic HTML para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un vacío `com.adobe.idp.Document` objeto.
   * La variable `HTMLRenderSpec` que almacena las opciones de tiempo de ejecución del HTML.
   * Un valor de cadena que especifica la variable `HTTP_USER_AGENT` valor de encabezado; por ejemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` objeto que almacena valores de URI necesarios para procesar un formulario de HTML.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   La variable `(Deprecated) renderHTMLForm` el método devuelve un `FormsResult` objeto que contiene una secuencia de datos de formulario que se puede escribir en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un `com.adobe.idp.Document` invocando el objeto `FormsResult` objeto ‘s `getOutputContent` método.
   * Obtenga el tipo de contenido de la variable `com.adobe.idp.Document` invocando su `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasar el tipo de contenido de la variable `com.adobe.idp.Document` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos del formulario en el explorador web del cliente invocando la variable `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Cree un `java.io.InputStream` invocando el objeto `com.adobe.idp.Document` del objeto `getInputStream` método.
   * Cree una matriz de bytes y rellénela con la secuencia de datos del formulario invocando la variable `InputStream` del objeto `read` y pasando la matriz de bytes como argumento.
   * Invocar el `javax.servlet.ServletOutputStream` del objeto `write` método para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes a la `write` método.

**Consulte también lo siguiente**

[Representación de Forms como HTML](#rendering-forms-as-html)

[Inicio rápido (modo SOAP): Representación de un formulario de HTML mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Representar un formulario como HTML mediante la API de servicio web {#render-a-form-as-html-using-the-web-service-api}

Representar un formulario de HTML mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases proxy de Java en la ruta de clase.

1. Creación de un objeto de API de cliente de Forms

   Cree un `FormsService` y establezca los valores de autenticación.

1. Establecer opciones de tiempo de ejecución del HTML

   * Cree un `HTMLRenderSpec` usando su constructor.
   * Para procesar un formulario de HTML con una barra de herramientas, invoque la función `HTMLRenderSpec` del objeto `setHTMLToolbar` método y pasar un `HTMLToolbar` valor de enumeración. Por ejemplo, para mostrar una barra de herramientas vertical del HTML, pase `HTMLToolbar.Vertical`.
   * Para definir el valor de configuración regional para el formulario de HTML, invoque la variable `HTMLRenderSpec` del objeto `setLocale` y pase un valor de cadena que especifique el valor de configuración regional. Para obtener más información, consulte [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Para procesar el formulario del HTML con etiquetas de HTML completas, invoque la variable `HTMLRenderSpec` del objeto `setOutputType` método y pase `OutputType.FullHTMLTags`.

   >[!NOTE]
   Forms no se procesa correctamente en el HTML cuando la variable `StandAlone` la opción es `true` y `ApplicationWebRoot` hace referencia a un servidor que no es el servidor de aplicaciones J2EE que hospeda AEM Forms (la variable `ApplicationWebRoot` se especifica utilizando la variable `URLSpec` objeto que se pasa al `FormsServiceClient` del objeto `(Deprecated) renderHTMLForm` método). Cuando la variable `ApplicationWebRoot` es otro servidor del que aloja AEM Forms, el valor del URI raíz web en la consola de administración debe establecerse como el valor URI de la aplicación web del formulario. Para ello, inicie sesión en la consola de administración, haga clic en Servicios > Forms y establezca el URI de la raíz web como https://server-name:port/FormServer. A continuación, guarde la configuración.

1. Representar un formulario de HTML

   Invocar el `FormsService` del objeto `(Deprecated) renderHTMLForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valor enum que especifica el tipo de preferencia de HTML. Por ejemplo, para procesar un formulario de HTML compatible con dynamic HTML para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * A `BLOB` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`. (Consulte [Rellenado previo de Forms con diseños flexibles](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts).)
   * La variable `HTMLRenderSpec` que almacena las opciones de tiempo de ejecución del HTML.
   * Un valor de cadena que especifica la variable `HTTP_USER_AGENT` valor de encabezado; por ejemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Puede pasar una cadena vacía si no desea establecer este valor.
   * A `URLSpec` objeto que almacena valores de URI necesarios para procesar un formulario de HTML. (Consulte [Especificar valores de URI](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario. (Consulte [Adjuntar archivos al formulario](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * Un vacío `com.adobe.idp.services.holders.BLOBHolder` objeto que rellena el método . Este valor de parámetro almacena el formulario procesado.
   * Un vacío `com.adobe.idp.services.holders.BLOBHolder` objeto que rellena el método . Este parámetro almacenará los datos XML de salida.
   * Un vacío `javax.xml.rpc.holders.LongHolder` objeto que rellena el método . Este argumento almacenará el número de páginas del formulario.
   * Un vacío `javax.xml.rpc.holders.StringHolder` objeto que rellena el método . Este argumento almacenará el valor de configuración regional.
   * Un vacío `javax.xml.rpc.holders.StringHolder` objeto que rellena el método . Este argumento almacena el valor de procesamiento del HTML que se utiliza.
   * Un vacío `com.adobe.idp.services.holders.FormsResultHolder` que contendrá los resultados de esta operación.

   La variable `(Deprecated) renderHTMLForm` rellena el `com.adobe.idp.services.holders.FormsResultHolder` objeto que se pasa como el último valor de argumento con un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un `FormResult` obteniendo el valor de `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value` miembro de datos.
   * Cree un `BLOB` objeto que contiene datos de formulario invocando la variable `FormsResult` del objeto `getOutputContent` método.
   * Obtenga el tipo de contenido de la variable `BLOB` invocando su `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasar el tipo de contenido de la variable `BLOB` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos del formulario en el explorador web del cliente invocando la variable `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Cree una matriz de bytes y rellénela invocando la variable `BLOB` del objeto `getBinaryData` método. Esta tarea asigna el contenido de la variable `FormsResult` a la matriz de bytes.
   * Invocar el `javax.servlet.http.HttpServletResponse` del objeto `write` método para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes a la `write` método.

**Consulte también lo siguiente**

[Representación de Forms como HTML](#rendering-forms-as-html)

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
