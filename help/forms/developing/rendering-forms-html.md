---
title: Representación de Forms como HTML
seo-title: Representación de Forms como HTML
description: Utilice el servicio Forms para procesar formularios como HTML en respuesta a una solicitud HTTP procedente de un navegador web. Puede utilizar la API de Java y la API de servicio Web para procesar formularios como HTML.
seo-description: Utilice el servicio Forms para procesar formularios como HTML en respuesta a una solicitud HTTP procedente de un navegador web. Puede utilizar la API de Java y la API de servicio Web para procesar formularios como HTML.
uuid: bd8edb6f-333b-4ceb-9877-618f5377f56f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 669ede46-ea55-444b-a23f-23a86e5aff8e
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '4188'
ht-degree: 1%

---


# Representación de Forms como HTML {#rendering-forms-as-html}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en el entorno JEE.**

El servicio Forms procesa los formularios como HTML en respuesta a una solicitud HTTP procedente de un navegador web. Una ventaja de procesar un formulario como HTML es que el equipo en el que se encuentra el navegador web del cliente no requiere Adobe Reader, Acrobat ni Flash Player (para las guías de formulario (obsoletas)).

Para procesar un formulario como HTML, el diseño de formulario debe guardarse como archivo XDP. Un diseño de formulario guardado como archivo PDF no se puede representar como HTML. Cuando desarrolle un diseño de formulario en Designer que se procesará como HTML, tenga en cuenta los siguientes criterios:

* No utilice las propiedades de borde de un objeto para dibujar líneas, cuadros o cuadrículas en el formulario. Algunos exploradores no alinean los bordes tal como se muestran en la vista previa de Los objetos pueden aparecer en capas diferentes o desplazar otros objetos de la posición prevista.
* Puede utilizar líneas, rectángulos y círculos para definir el fondo.
* Dibuje texto ligeramente más grande de lo que parece necesario para dar cabida al texto. Algunos exploradores web no muestran el texto de forma legible.

>[!NOTE]
>
>Cuando se procesa un formulario que contiene imágenes TIFF con los métodos `FormServiceClient` y `(Deprecated) renderHTMLForm` del objeto `renderHTMLForm2`, las imágenes TIFF no están visibles en el formulario HTML procesado que se muestra en los navegadores Internet Explorer o Mozilla Firefox. Estos exploradores no proporcionan compatibilidad nativa con imágenes TIFF.

## Páginas HTML {#html-pages}

Cuando un diseño de formulario se procesa como un formulario HTML, cada subformulario de segundo nivel se procesa como una página HTML (panel). Puede vista de la jerarquía de un subformulario en Designer. Los subformularios secundarios que pertenecen al subformulario raíz (el nombre predeterminado de un subformulario raíz es formulario1) son los subformularios del panel. El ejemplo siguiente muestra los subformularios de un diseño de formulario.

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

Cuando los diseños de formulario se procesan como formularios HTML, los paneles no se limitan a un tamaño de página determinado. Si tiene subformularios dinámicos, deben anidarse en el subformulario del panel. Los subformularios dinámicos pueden expandirse a un número infinito de páginas HTML.

Cuando un formulario se procesa como un formulario HTML, los tamaños de página (necesarios para paginar formularios procesados como PDF) no tienen significado. Dado que un formulario con presentación flexible puede expandirse a un número infinito de páginas HTML, es importante evitar los pies de página en la página de formato. Un pie de página debajo del área de contenido de una página de formato puede sobrescribir el contenido HTML que pasa por encima del límite de la página.

Debe moverse explícitamente de un panel a otro utilizando los métodos `xfa.host.pageUp` y `xfa.host.pageDown`. Las páginas se cambian enviando un formulario al servicio Forms y haciendo que el servicio Forms vuelva a procesar el formulario en el dispositivo cliente, normalmente un explorador Web.

>[!NOTE]
>
>El proceso de enviar un formulario al servicio de Forms y, a continuación, hacer que el servicio Forms vuelva a procesar el formulario en el dispositivo cliente se denomina datos de transferencia al servidor.

>[!NOTE]
>
>Si desea personalizar el aspecto del botón de firma digital HTML en un formulario HTML, debe cambiar las siguientes propiedades en el archivo fscdigsig.css (en el archivo adobe-forms-ds.ear > adobe-forms-ds.war):

**.fsc-ds-ssb**: Esta hoja de estilo es aplicable en el caso de un campo de signo en blanco.

**.fsc-ds-ssv**: Esta hoja de estilo es aplicable en el caso de un campo de signo Válido.

**.fsc-ds-ssc**: Esta hoja de estilo es aplicable en el caso de un campo de signo Válido pero los datos han cambiado.

**.fsc-ds-ssi**: Esta hoja de estilo es aplicable en caso de que el campo de signo no sea válido.

**.fsc-ds-popup-bg**: No se está utilizando esta propiedad de hoja de estilo.

**.fsc-ds-popup-btn**: No se está utilizando esta propiedad de hoja de estilo.

## Ejecución de secuencias de comandos {#running-scripts}

Un autor de formulario especifica si una secuencia de comandos se ejecuta en el servidor o en el cliente. El servicio Forms crea un entorno de procesamiento de evento distribuido para la ejecución de la inteligencia de formularios que se puede distribuir entre el cliente y el servidor mediante el atributo `runAt`. Para obtener información sobre este atributo o la creación de secuencias de comandos en diseños de formulario, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

El servicio Forms puede ejecutar secuencias de comandos mientras se procesa el formulario. Como resultado, puede rellenar previamente un formulario con datos conectándose a una base de datos o a servicios Web que pueden no estar disponibles en el cliente. También puede configurar el evento `Click` de un botón para que se ejecute en el servidor de modo que el cliente redondee los datos al servidor. Esto permite al cliente ejecutar secuencias de comandos que pueden requerir recursos del servidor, como una base de datos empresarial, mientras el usuario interactúa con un formulario. Para los formularios HTML, las secuencias de comandos de formato solo se pueden ejecutar en el servidor. Como resultado, debe marcar estas secuencias de comandos para que se ejecuten en `server` o `both`.

Puede diseñar formularios que se desplacen entre páginas (paneles) llamando a los métodos `xfa.host.pageUp` y `xfa.host.pageDown`. Esta secuencia de comandos se coloca en el evento `Click` de un botón y el atributo `runAt` se establece en `Both`. La razón por la que elige `Both` es que Adobe Reader o Acrobat (para formularios procesados como PDF) pueden cambiar las páginas sin ir al servidor y los formularios HTML pueden cambiar las páginas al enviar datos de ida y vuelta al servidor. Es decir, se envía un formulario al servicio Forms y se procesa un formulario como HTML con la nueva página mostrada.

Se recomienda no asignar a las variables de secuencia de comandos y a los campos de formulario los mismos nombres, como item. Es posible que algunos exploradores Web, como Internet Explorer, no inicialicen una variable con el mismo nombre que un campo de formulario que produzca un error de secuencia de comandos. Se recomienda asignar nombres diferentes a los campos de formulario y a las variables de secuencia de comandos.

Al procesar formularios HTML que contengan tanto la funcionalidad de navegación de página como secuencias de comandos de formulario (por ejemplo, supongamos que una secuencia de comandos recupera datos de campo de una base de datos cada vez que se procesa el formulario), asegúrese de que la secuencia de comandos de formulario se encuentra en el evento form:calculate en lugar en el suceso form:readyevent.

Las secuencias de comandos de formulario que se encuentran en el evento form:ready se ejecutan una sola vez durante la representación inicial del formulario y no se ejecutan para posteriores recuperaciones de página. Por el contrario, el evento form:calculate se ejecuta para cada navegación de página en la que se procesa el formulario.

>[!NOTE]
En un formulario de varias páginas, los cambios realizados por JavaScript en una página no se conservan si se mueve a otra página.

Puede invocar secuencias de comandos personalizadas antes de enviar un formulario. Esta función funciona en todos los exploradores disponibles. Sin embargo, solo se puede utilizar cuando los usuarios procesan el formulario HTML que tiene su propiedad `Output Type` establecida en `Form Body`. No funcionará cuando `Output Type` sea `Full HTML`. Consulte Configuración de formularios en la ayuda de administración para ver los pasos para configurar esta función.

Primero debe definir una función de llamada de retorno que se llame antes de enviar el formulario, donde el nombre de la función es `_user_onsubmit`. Se da por hecho que la función no emitirá ninguna excepción o, si lo hace, se omitirá la excepción. Se recomienda colocar la función JavaScript en la sección head del html; sin embargo, puede declararlo en cualquier lugar antes del final de las etiquetas de script que incluyen `xfasubset.js`.

Cuando formserver procesa un XDP que contiene una lista desplegable, además de crear la lista desplegable, también crea dos campos de texto ocultos. Estos campos de texto almacenan los datos de la lista desplegable (uno almacena el nombre para mostrar de las opciones y otro almacena el valor de las opciones). Por lo tanto, cada vez que un usuario envía el formulario, se envían todos los datos de la lista desplegable. Si no desea enviar tantos datos cada vez, puede escribir una secuencia de comandos personalizada para deshabilitarla. Por ejemplo: El nombre de la lista desplegable es `drpOrderedByStateProv` y se ajusta en el encabezado del subformulario. El nombre del elemento de entrada HTML será `header[0].drpOrderedByStateProv[0]`. El nombre de los campos ocultos que almacenan y envían los datos de la lista desplegable tiene los siguientes nombres: `header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

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

Al crear diseños de formulario para procesarlos como HTML, debe restringir la secuencia de comandos al subconjunto XFA para las secuencias de comandos en lenguaje JavaScript.

Las secuencias de comandos que se ejecutan en el cliente o en el cliente y en el servidor deben escribirse en el subconjunto XFA. Las secuencias de comandos que se ejecutan en el servidor pueden utilizar el modelo completo de secuencias de comandos XFA y también FormCalc. Para obtener información sobre el uso de JavaScript, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

Cuando se ejecutan secuencias de comandos en el cliente, sólo el panel actual que se está mostrando puede utilizar secuencias de comandos; por ejemplo, cuando se muestra el panel B, no se puede crear una secuencia de comandos para los campos ubicados en el panel A. Al ejecutar secuencias de comandos en el servidor, se puede acceder a todos los paneles.

También debe tener cuidado al utilizar expresiones del Modelo de objetos de secuencias de comandos (SOM) en secuencias de comandos que se ejecutan en el cliente. Solo un subconjunto simplificado de expresiones SOM se admite en las secuencias de comandos que se ejecutan en el cliente.

## Temporización de evento {#event-timing}

El subconjunto XFA define los eventos XFA asignados a eventos HTML. Hay una ligera diferencia de comportamiento en el tiempo de cálculo y validación de eventos. En un navegador web, se ejecuta un evento de cálculo completo al salir de un campo. Los eventos de cálculo no se ejecutan automáticamente cuando se realiza un cambio en un valor de campo. Puede forzar un evento de cálculo llamando al método `xfa.form.execCalculate`.

En un navegador web, las eventos de validación solo se ejecutan al salir de un campo o al enviar un formulario. Puede forzar un evento de validación mediante el método `xfa.form.execValidate`.

Forms que se muestra en un navegador web (a diferencia de Adobe Reader o Acrobat) cumple con la prueba XFA null (errores o advertencias) para los campos obligatorios.

* Si la prueba nula produce un error y sale de un campo sin especificar un valor, se muestra un cuadro de mensaje y se le reasigna el campo después de hacer clic en Aceptar.
* Si una prueba nula genera una advertencia y sale de un campo sin especificar un valor, se le pedirá que haga clic en Aceptar o en Cancelar, lo que le dará la opción de continuar sin especificar un valor o volver al campo para introducir un valor.

Para obtener más información sobre una prueba nula, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Botones de formulario {#form-buttons}

Al hacer clic en un botón de envío, se envían datos de formulario al servicio Forms y se representa el final del procesamiento del formulario. El evento `preSubmit` puede configurarse para ejecutarse en el cliente o servidor. El evento `preSubmit` se ejecuta antes del envío del formulario si está configurado para ejecutarse en el cliente. De lo contrario, el evento `preSubmit` se ejecuta en el servidor durante el envío del formulario. Para obtener más información sobre el evento `preSubmit`, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

Si un botón no tiene ninguna secuencia de comandos del lado del cliente asociada, los datos se envían al servidor, los cálculos se realizan en el servidor y se regenera el formulario HTML. Si un botón contiene una secuencia de comandos del lado del cliente, los datos no se envían al servidor y la secuencia de comandos del lado del cliente se ejecuta en el explorador Web.

## Navegador web HTML 4.0 {#html-4-0-web-browser}

Un navegador web que solo admite HTML 4.0 no puede admitir el modelo de secuencias de comandos de cliente de subconjunto XFA. Cuando se crea un diseño de formulario para que funcione tanto en HTML 4.0 como en MSDHTML o CSS2HTML, una secuencia de comandos marcada para ejecutarse en el cliente se ejecutará realmente en el servidor. Por ejemplo, supongamos que un usuario hace clic en un botón que se encuentra en un formulario mostrado en un explorador Web HTML 4.0. En este caso, los datos del formulario se envían al servidor en el que se ejecuta la secuencia de comandos del lado del cliente.

Se recomienda colocar la lógica del formulario en eventos de cálculo, que se ejecutan en el servidor en HTML 4.0 y en el cliente para MSDHTML o CSS2HTML.

## Mantenimiento de los cambios de presentación {#maintaining-presentation-changes}

A medida que se desplaza entre páginas HTML (paneles), solo se mantiene el estado de los datos. La configuración, como el color de fondo o la configuración de campo obligatoria, no se mantiene (si es diferente a la configuración inicial). Para mantener el estado de presentación, debe crear campos (normalmente ocultos) que representen el estado de presentación de los campos. Si agrega una secuencia de comandos al evento `Calculate` de un campo que cambia la presentación en función de los valores de campo ocultos, podrá conservar el estado de la presentación a medida que avanza y avanza entre páginas HTML (paneles).

La siguiente secuencia de comandos mantiene el `fillColor` de un campo en función del valor de `hiddenField`. Supongamos que esta secuencia de comandos se encuentra en el evento `Calculate` de un campo.

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
Los objetos estáticos no se muestran en un formulario HTML procesado cuando se anidan dentro de una celda de tabla. Por ejemplo, un círculo y un rectángulo anidados dentro de una celda de tabla no se muestran en un formulario HTML de procesamiento. Sin embargo, estos mismos objetos estáticos se muestran correctamente cuando se encuentran fuera de la tabla.

## Firma digital de formularios HTML {#digitally-signing-html-forms}

No se puede firmar un formulario HTML que contenga un campo de firma digital si el formulario se procesa como una de las siguientes transformaciones HTML:

* AHTML
* HTML4
* StaticHTML
* NoScriptXHTML

Para obtener información sobre la firma digital de un documento, consulte [Firma y certificación digitales de Documentos](/help/forms/developing/digitally-signing-certifying-documents.md)

## Representación de un formulario XHTML compatible con las directrices de accesibilidad {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

Puede procesar un formulario HTML completo que cumpla las directrices de accesibilidad. Es decir, el formulario se procesa con etiquetas HTML completas, a diferencia del formulario HTML que se procesa con etiquetas body (no una página HTML completa).

## Validación de datos de formulario {#validating-form-data}

Se recomienda limitar el uso de reglas de validación para los campos de formulario al procesar el formulario como un formulario HTML. Es posible que algunos formularios HTML no admitan algunas reglas de validación. Por ejemplo, cuando se aplica un patrón de validación de MM-DD-AAAA a un campo `Date/Time` ubicado en un diseño de formulario que se procesa como formulario HTML, no funciona correctamente, incluso si la fecha se escribe correctamente. Sin embargo, este patrón de validación funciona correctamente para los formularios procesados como PDF.

>[!NOTE]
Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para procesar un formulario HTML, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Configure las opciones de tiempo de ejecución de HTML.
1. Representar un formulario HTML.
1. Escriba la secuencia de datos del formulario en el navegador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Forms Client**

Antes de poder importar datos mediante programación a una API de FormClient de PDF, debe crear un cliente del servicio de integración de datos de formulario. Al crear un cliente de servicio, se define la configuración de conexión necesaria para invocar un servicio.

**Definición de opciones de tiempo de ejecución de HTML**

Las opciones de tiempo de ejecución HTML se definen al procesar un formulario HTML. Por ejemplo, puede agregar una barra de herramientas a un formulario HTML para permitir a los usuarios seleccionar archivos adjuntos ubicados en el equipo cliente o recuperar archivos adjuntos procesados con el formulario HTML. De forma predeterminada, una barra de herramientas HTML está deshabilitada. Para agregar una barra de herramientas a un formulario HTML, debe definir mediante programación las opciones en tiempo de ejecución. De forma predeterminada, una barra de herramientas HTML consta de los siguientes botones:

* `Home`:: Proporciona un vínculo a la raíz web de la aplicación.
* `Upload`:: Proporciona una interfaz de usuario para seleccionar los archivos que se adjuntarán al formulario actual.
* `Download`:: Proporciona una interfaz de usuario para mostrar los archivos adjuntos.

Cuando aparece una barra de herramientas HTML en un formulario HTML, el usuario puede seleccionar un máximo de diez archivos para enviarlos junto con los datos del formulario. Una vez enviados los archivos, el servicio de Forms puede recuperarlos.

Al procesar un formulario como HTML, puede especificar un valor de usuario-agente. Un valor user-agent proporciona información del explorador y del sistema. Es un valor opcional y puede pasar un valor de cadena vacío. El inicio rápido Representar un formulario HTML mediante la API de Java muestra cómo obtener un valor de agente de usuario y utilizarlo para procesar un formulario como HTML.

Las direcciones URL HTTP en las que se publican los datos del formulario se pueden especificar estableciendo la dirección URL del destinatario mediante la API del cliente de servicios de Forms o se pueden especificar en el botón Enviar contenido en el diseño de formulario XDP. Si la URL de destinatario se especifica en el diseño de formulario, no defina un valor mediante la API de Forms Service Client.

>[!NOTE]
Representar un formulario HTML con una barra de herramientas es opcional.

>[!NOTE]
Si procesa un formulario AHTML, se recomienda no agregar una barra de herramientas al formulario.

**Representar un formulario HTML**

Para procesar un formulario HTML, debe especificar un diseño de formulario creado en Designer y guardado como archivo XDP. También debe seleccionar un tipo de transformación HTML. Por ejemplo, puede especificar el tipo de transformación HTML que procesa un HTML dinámico para Internet Explorer 5.0 o posterior.

La representación de un formulario HTML también requiere valores, como valores URI, que son necesarios para representar otros tipos de formulario.

**Escribir el flujo de datos del formulario en el navegador web del cliente**

Cuando el servicio Forms procesa un formulario HTML, devuelve una secuencia de datos de formulario que debe escribir en el navegador web del cliente. Cuando se escribe en el navegador web del cliente, el formulario HTML es visible para el usuario.

**Consulte también**

[Representar un formulario como HTML mediante la API de Java](#render-a-form-as-html-using-the-java-api)

[Representar un formulario como HTML mediante la API de servicio web](#render-a-form-as-html-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API de servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Representación de PDF forms interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Representación de HTML Forms con barras de herramientas personalizadas](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[Creación de Aplicaciones web que procesan Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Representar un formulario como HTML mediante la API de Java {#render-a-form-as-html-using-the-java-api}

Representar un formulario HTML mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clases del proyecto Java.

1. Creación de un objeto de API de Forms Client

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `FormsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Definición de opciones de tiempo de ejecución de HTML

   * Cree un objeto `HTMLRenderSpec` utilizando su constructor.
   * Para procesar un formulario HTML con una barra de herramientas, invoque el método `HTMLRenderSpec` del objeto `setHTMLToolbar` y pase un valor de enumeración `HTMLToolbar`. Por ejemplo, para mostrar una barra de herramientas HTML vertical, pase `HTMLToolbar.Vertical`.
   * Para establecer el valor de configuración regional para el formulario HTML, invoque el método `HTMLRenderSpec` del objeto `setLocale` y pase un valor de cadena que especifique el valor de configuración regional. (Esta es una configuración opcional).
   * Para procesar el formulario HTML con etiquetas HTML completas, invoque el método `HTMLRenderSpec` del objeto `setOutputType` y pase `OutputType.FullHTMLTags`. (Esta es una configuración opcional).

   >[!NOTE]
   Forms no se procesa correctamente en HTML cuando la opción `StandAlone` es `true` y `ApplicationWebRoot` hace referencia a un servidor que no es el servidor de aplicaciones J2EE que aloja AEM Forms (el valor `ApplicationWebRoot` se especifica utilizando el objeto `URLSpec` que se pasa al método `FormsServiceClient` del objeto). `(Deprecated) renderHTMLForm` Cuando `ApplicationWebRoot` es otro servidor del que aloja AEM Forms, el valor del URI de raíz web en la consola de administración debe configurarse como el valor URI de la aplicación web del formulario. Para ello, inicie sesión en la consola de administración, haga clic en Servicios > Forms y defina el URI de raíz web como https://server-name:port/FormServer. A continuación, guarde la configuración.

1. Representar un formulario HTML

   Invoque el método `FormsServiceClient` del objeto `(Deprecated) renderHTMLForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un valor de enumeración `TransformTo` que especifica el tipo de preferencia HTML. Por ejemplo, para procesar un formulario HTML compatible con HTML dinámico para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * Un objeto `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un objeto vacío `com.adobe.idp.Document`.
   * El objeto `HTMLRenderSpec` que almacena las opciones de tiempo de ejecución HTML.
   * Un valor de cadena que especifica el valor de encabezado `HTTP_USER_AGENT`; por ejemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Un objeto `URLSpec` que almacena valores URI necesarios para procesar un formulario HTML.
   * Objeto `java.util.HashMap` que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El método `(Deprecated) renderHTMLForm` devuelve un objeto `FormsResult` que contiene una secuencia de datos de formulario que se puede escribir en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un objeto `com.adobe.idp.Document` invocando el método `FormsResult` del objeto ‘s `getOutputContent`.
   * Obtenga el tipo de contenido del objeto `com.adobe.idp.Document` invocando su método `getContentType`.
   * Configure el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `com.adobe.idp.Document`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el método `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream`.
   * Cree un objeto `java.io.InputStream` invocando el método `com.adobe.idp.Document` del objeto `getInputStream`.
   * Cree una matriz de bytes y rellénela con la secuencia de datos del formulario invocando el método `InputStream` del objeto `read` y pasando la matriz de bytes como argumento.
   * Invoque el método `javax.servlet.ServletOutputStream` del objeto `write` para enviar la secuencia de datos del formulario al explorador Web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Representación de Forms como HTML](#rendering-forms-as-html)

[Inicio rápido (modo SOAP): Representación de un formulario HTML mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Representar un formulario como HTML mediante la API de servicio Web {#render-a-form-as-html-using-the-web-service-api}

Representar un formulario HTML mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases proxy de Java que consuman el WSDL del servicio de Forms.
   * Incluya las clases proxy de Java en la ruta de clases.

1. Creación de un objeto de API de Forms Client

   Cree un objeto `FormsService` y defina los valores de autenticación.

1. Definición de opciones de tiempo de ejecución de HTML

   * Cree un objeto `HTMLRenderSpec` utilizando su constructor.
   * Para procesar un formulario HTML con una barra de herramientas, invoque el método `HTMLRenderSpec` del objeto `setHTMLToolbar` y pase un valor de enumeración `HTMLToolbar`. Por ejemplo, para mostrar una barra de herramientas HTML vertical, pase `HTMLToolbar.Vertical`.
   * Para establecer el valor de configuración regional para el formulario HTML, invoque el método `HTMLRenderSpec` del objeto `setLocale` y pase un valor de cadena que especifique el valor de configuración regional. Para obtener más información, consulte [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Para procesar el formulario HTML con etiquetas HTML completas, invoque el método `HTMLRenderSpec` del objeto `setOutputType` y pase `OutputType.FullHTMLTags`.

   >[!NOTE]
   Forms no se procesa correctamente en HTML cuando la opción `StandAlone` es `true` y `ApplicationWebRoot` hace referencia a un servidor que no es el servidor de aplicaciones J2EE que aloja AEM Forms (el valor `ApplicationWebRoot` se especifica utilizando el objeto `URLSpec` que se pasa al método `FormsServiceClient` del objeto). `(Deprecated) renderHTMLForm` Cuando `ApplicationWebRoot` es otro servidor del que aloja AEM Forms, el valor del URI de raíz web en la consola de administración debe configurarse como el valor URI de la aplicación web del formulario. Para ello, inicie sesión en la consola de administración, haga clic en Servicios > Forms y defina el URI de raíz web como https://server-name:port/FormServer. A continuación, guarde la configuración.

1. Representar un formulario HTML

   Invoque el método `FormsService` del objeto `(Deprecated) renderHTMLForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un valor de enumeración `TransformTo` que especifica el tipo de preferencia HTML. Por ejemplo, para procesar un formulario HTML compatible con HTML dinámico para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * Un objeto `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`. (Consulte [Rellenado previo de Forms con diseños de posición variable](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts)).
   * El objeto `HTMLRenderSpec` que almacena las opciones de tiempo de ejecución HTML.
   * Un valor de cadena que especifica el valor de encabezado `HTTP_USER_AGENT`; por ejemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Puede pasar una cadena vacía si no desea establecer este valor.
   * Un objeto `URLSpec` que almacena valores URI necesarios para procesar un formulario HTML. (Consulte [Especificar valores de URI](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * Objeto `java.util.HashMap` que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario. (Consulte [Adjuntar archivos al formulario](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * Un objeto vacío `com.adobe.idp.services.holders.BLOBHolder` que se rellena con el método. Este valor de parámetro almacena el formulario procesado.
   * Un objeto vacío `com.adobe.idp.services.holders.BLOBHolder` que se rellena con el método. Este parámetro almacenará los datos XML de salida.
   * Un objeto vacío `javax.xml.rpc.holders.LongHolder` que se rellena con el método. Este argumento almacenará el número de páginas del formulario.
   * Un objeto vacío `javax.xml.rpc.holders.StringHolder` que se rellena con el método. Este argumento almacenará el valor de configuración regional.
   * Un objeto vacío `javax.xml.rpc.holders.StringHolder` que se rellena con el método. Este argumento almacenará el valor de representación HTML que se utiliza.
   * Un objeto vacío `com.adobe.idp.services.holders.FormsResultHolder` que contendrá los resultados de esta operación.

   El método `(Deprecated) renderHTMLForm` rellena el objeto `com.adobe.idp.services.holders.FormsResultHolder` que se pasa como el último valor de argumento con una secuencia de datos de formulario que debe escribirse en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un objeto `FormResult` obteniendo el valor del miembro de datos `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value`.
   * Cree un objeto `BLOB` que contenga datos de formulario invocando el método `FormsResult` del objeto `getOutputContent`.
   * Obtenga el tipo de contenido del objeto `BLOB` invocando su método `getContentType`.
   * Configure el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `BLOB`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el método `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream`.
   * Cree una matriz de bytes y rellénela invocando el método `BLOB` del objeto `getBinaryData`. Esta tarea asigna el contenido del objeto `FormsResult` a la matriz de bytes.
   * Invoque el método `javax.servlet.http.HttpServletResponse` del objeto `write` para enviar la secuencia de datos del formulario al explorador Web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Representación de Forms como HTML](#rendering-forms-as-html)

[Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

