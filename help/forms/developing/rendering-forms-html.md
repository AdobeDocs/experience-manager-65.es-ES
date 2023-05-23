---
title: Procesar formularios como HTML
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

# Procesar formularios como HTML {#rendering-forms-as-html}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

El servicio Forms procesa los formularios como HTML en respuesta a una solicitud HTTP de un explorador web. Una ventaja de procesar un formulario como HTML es que el equipo en el que se encuentra el explorador web del cliente no requiere Adobe Reader, Acrobat ni Flash Player (para las guías del formulario (obsoleto)).

Para procesar un formulario como HTML, el diseño de formulario debe guardarse como archivo XDP. Un diseño de formulario guardado como archivo PDF no se puede procesar como HTML. Al desarrollar un diseño de formulario en Designer que se procesará como HTML, tenga en cuenta los siguientes criterios:

* No utilice las propiedades de borde de un objeto para dibujar líneas, cuadros o cuadrículas en el formulario. Es posible que algunos exploradores no alineen los bordes exactamente como aparecen en una vista previa. Los objetos pueden aparecer en capas o empujar a otros objetos fuera de su posición esperada.
* Puede utilizar líneas, rectángulos y círculos para definir el fondo.
* Dibuje texto ligeramente más grande que lo que parece necesario para acomodar el texto. Algunos exploradores web no muestran el texto de forma legible.

>[!NOTE]
>
>Al procesar un formulario que contiene imágenes de TIFF mediante `FormServiceClient` del objeto `(Deprecated) renderHTMLForm` y `renderHTMLForm2` métodos, las imágenes del TIFF no son visibles en el formulario del HTML procesado que se muestra en los navegadores Internet Explorer o Mozilla Firefox. Estos exploradores no proporcionan compatibilidad nativa con imágenes de TIFF.

## páginas de HTML {#html-pages}

Cuando se representa un diseño de formulario como un formulario de HTML, cada subformulario de segundo nivel se representa como una página de HTML (panel). Puede ver la jerarquía de un subformulario en Designer. Los subformularios secundarios que pertenecen al subformulario raíz (el nombre predeterminado de un subformulario raíz es form1) son los subformularios del panel. El siguiente ejemplo muestra los subformularios de un diseño de formulario.

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

Cuando los diseños de formulario se representan como formularios HTML, los paneles no están restringidos a ningún tamaño de página en particular. Si tiene subformularios dinámicos, deben anidarse dentro del subformulario del panel. Los subformularios dinámicos se pueden expandir a un número infinito de páginas de HTML.

Cuando un formulario se procesa como un formulario de HTML, los tamaños de página (necesarios para paginar formularios procesados como PDF) no tienen significado. Dado que un formulario con un diseño variable puede expandirse a un número infinito de páginas de HTML, es importante evitar los pies de página en la página maestra. Un pie de página debajo del área de contenido de una página maestra puede sobrescribir el contenido del HTML que sobrepasa el límite de una página.

Debe moverse explícitamente de un panel a otro con la variable `xfa.host.pageUp` y `xfa.host.pageDown` métodos. Para cambiar de página, debe enviar un formulario al servicio de Forms y hacer que el servicio de Forms vuelva a representar el formulario en el dispositivo cliente, normalmente un explorador web.

>[!NOTE]
>
>El proceso de enviar un formulario al servicio de Forms y, a continuación, hacer que el servicio de Forms vuelva a procesar el formulario en el dispositivo cliente se denomina envío de datos de ida y vuelta al servidor.

>[!NOTE]
>
>Si desea personalizar el aspecto del botón Firma digital de HTML en un formulario de HTML, debe cambiar las siguientes propiedades en el archivo fscdigsig.css (dentro del archivo adobe-forms-ds.ear > adobe-forms-ds.war ):

**.fsc-ds-ssb**: Esta hoja de estilo es aplicable en el caso de un campo de signo en blanco.

**.fsc-ds-ssv**: Esta hoja de estilo es aplicable en el caso de un campo de signo válido.

**.fsc-ds-ssc**: esta hoja de estilo es aplicable en el caso de un campo de signo válido pero los datos han cambiado.

**.fsc-ds-ssi**: esta hoja de estilo es aplicable en caso de un campo de signo no válido.

**.fsc-ds-popup-bg**: esta propiedad de hoja de estilos no se está utilizando.

**.fsc-ds-popup-btn**: esta propiedad de hoja de estilos no se está utilizando.

## Ejecución de scripts {#running-scripts}

Un autor de formularios especifica si una secuencia de comandos se ejecuta en el servidor o en el cliente. El servicio Forms crea un entorno de procesamiento de eventos distribuido para la ejecución de inteligencia de formularios que se puede distribuir entre el cliente y el servidor mediante `runAt` atributo. Para obtener información sobre este atributo o la creación de scripts en diseños de formulario, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

El servicio Forms puede ejecutar scripts mientras se procesa el formulario. Como resultado, puede rellenar previamente un formulario con datos conectándose a una base de datos o a servicios web que pueden no estar disponibles en el cliente. También puede establecer el de un botón `Click` evento que se ejecutará en el servidor para que el cliente pueda enviar datos de ida y vuelta al servidor. Esto permite al cliente ejecutar scripts que pueden requerir recursos del servidor, como una base de datos empresarial, mientras un usuario interactúa con un formulario. Para los formularios de HTML, los scripts formcalc solo se pueden ejecutar en el servidor. Como resultado, debe marcar estos scripts para que se ejecuten a las `server` o `both`.

Puede diseñar formularios que se muevan entre páginas (paneles) llamando a `xfa.host.pageUp` y `xfa.host.pageDown` métodos. Esta secuencia de comandos se coloca en la etiqueta de un botón `Click` y el `runAt` el atributo se establece en `Both`. La razón por la que elige `Both` es para que Adobe Reader o Acrobat (para formularios que se representan como PDF) puedan cambiar de página sin ir al servidor y los formularios de HTML pueden cambiar de página recorriendo datos al servidor. Es decir, se envía un formulario al servicio de Forms y se vuelve a procesar como HTML con la nueva página mostrada.

Se recomienda no asignar a las variables de script y a los campos de formulario los mismos nombres, como por ejemplo, elemento. Es posible que algunos exploradores web, como Internet Explorer, no inicialicen una variable con el mismo nombre que un campo de formulario, lo que provoca un error de secuencia de comandos. Se recomienda asignar nombres diferentes a los campos de formulario y a las variables de script.

Al procesar formularios de HTML que contienen funcionalidad de navegación de páginas y scripts de formulario (por ejemplo, supongamos que un script recupera datos de campo de una base de datos cada vez que se procesa el formulario), asegúrese de que el script de formulario se encuentra en el evento form:calculate en lugar de form:readyevent.

Los scripts de formulario ubicados en el evento form:ready se ejecutan solo una vez durante la representación inicial del formulario y no se ejecutan para las recuperaciones de páginas posteriores. Por el contrario, el evento form: calculate se ejecuta para cada navegación de página en la que se procesa el formulario.

>[!NOTE]
En un formulario de varias páginas, los cambios realizados por JavaScript en una página no se conservan si se mueve a una página diferente.

Puede invocar scripts personalizados antes de enviar un formulario. Esta función funciona en todos los navegadores disponibles. Sin embargo, solo se puede utilizar cuando los usuarios procesan el formulario de HTML que tiene su `Output Type` propiedad establecida en `Form Body`. No funcionará cuando la variable `Output Type` es `Full HTML`. Consulte Configuración de formularios en la ayuda de administración para ver los pasos necesarios para configurar esta función.

Primero debe definir una función de llamada de retorno que se llame antes de enviar el formulario, donde el nombre de la función es `_user_onsubmit`. Se supone que la función no producirá ninguna excepción o, si lo hace, se ignorará la excepción. Se recomienda colocar la función de JavaScript en la sección head del HTML; sin embargo, puede declararla en cualquier lugar antes del final de las etiquetas de script que incluyen `xfasubset.js`.

Cuando el servidor de formularios procesa un XDP que contiene una lista desplegable, además de crear la lista desplegable, también crea dos campos de texto ocultos. Estos campos de texto almacenan los datos de la lista desplegable (uno almacena el nombre para mostrar de las opciones y otro almacena el valor de las opciones). Por lo tanto, cada vez que un usuario envía el formulario, se envían todos los datos de la lista desplegable. Suponiendo que no desee enviar tantos datos cada vez, puede escribir un script personalizado para deshabilitarlo. Por ejemplo: el nombre de la lista desplegable es `drpOrderedByStateProv` y se coloca debajo del encabezado del subformulario. El nombre del elemento de entrada del HTML es `header[0].drpOrderedByStateProv[0]`. El nombre de los campos ocultos que almacenan y envían los datos de la lista desplegable tiene los siguientes nombres: `header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

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

Al crear diseños de formulario para procesarlos como HTML, debe restringir los scripts al subconjunto XFA para scripts en lenguaje JavaScript.

Los scripts que se ejecutan en el cliente o en el cliente y en el servidor deben escribirse dentro del subconjunto XFA. Los scripts que se ejecutan en el servidor pueden utilizar el modelo de scripts XFA completo y también utilizar FormCalc. Para obtener información sobre el uso de JavaScript, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

Al ejecutar secuencias de comandos en el cliente, solo el panel que se está mostrando puede utilizar secuencias de comandos; por ejemplo, no puede crear secuencias de comandos con campos ubicados en el panel A cuando se muestra el panel B. Al ejecutar scripts en el servidor, se puede acceder a todos los paneles.

También debe tener cuidado al utilizar expresiones del Modelo de objetos de script (SOM) en scripts que se ejecutan en el cliente. Los scripts que se ejecutan en el cliente solo admiten un subconjunto simplificado de expresiones SOM.

## Programación de eventos {#event-timing}

El subconjunto XFA define los eventos XFA asignados a eventos de HTML. Hay una ligera diferencia en el comportamiento en el tiempo de los eventos de cálculo y validación. En un explorador web, se ejecuta un evento de cálculo completo al salir de un campo. Los eventos de cálculo no se ejecutan automáticamente cuando se realiza un cambio en un valor de campo. Puede forzar un evento de cálculo llamando a la función `xfa.form.execCalculate` método.

En un explorador web, los eventos de validación solo se ejecutan al salir de un campo o al enviar un formulario. Puede forzar un evento de validación utilizando el `xfa.form.execValidate` método.

Forms mostrado en un explorador web (a diferencia de Adobe Reader o Acrobat) se ajusta a la prueba nula de XFA (errores o advertencias) para campos obligatorios.

* Si la prueba nula produce un error y sale de un campo sin especificar un valor, se muestra un cuadro de mensaje y se cambia la posición al campo después de hacer clic en Aceptar.
* Si una prueba nula produce una advertencia y sale de un campo sin especificar un valor, se le pedirá que haga clic en Aceptar o en Cancelar, lo que le dará la opción de continuar sin especificar un valor o volver al campo para escribir un valor.

Para obtener más información sobre una prueba nula, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Botones de formulario {#form-buttons}

Al hacer clic en un botón de envío, se envían datos de formulario al servicio Forms y se representa el final del procesamiento del formulario. El `preSubmit` El evento se puede configurar para que se ejecute en el cliente o en el servidor. El `preSubmit` se ejecuta antes del envío del formulario si está configurado para ejecutarse en el cliente. De lo contrario, la variable `preSubmit` se ejecuta en el servidor durante el envío del formulario. Para obtener más información sobre `preSubmit` evento, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

Si un botón no tiene ningún script de cliente asociado, los datos se envían al servidor, los cálculos se realizan en el servidor y se regenera el formulario del HTML. Si un botón contiene una secuencia de comandos del lado del cliente, los datos no se envían al servidor y la secuencia de comandos del lado del cliente se ejecuta en el explorador web.

## explorador web de HTML 4.0 {#html-4-0-web-browser}

Un explorador web que solo admite HTML 4.0 no puede admitir el modelo de scripts del lado del cliente del subconjunto XFA. Al crear un diseño de formulario para que funcione tanto en el HTML 4.0 como en el HTML MSDHTML o CSS2, un script marcado para ejecutarse en el cliente se ejecutará en el servidor. Por ejemplo, supongamos que un usuario hace clic en un botón ubicado en un formulario mostrado en un explorador web de HTML 4.0. En este caso, los datos del formulario se envían al servidor donde se ejecuta el script del lado del cliente.

Se recomienda colocar la lógica de formulario en los eventos calculate, que se ejecutan en el servidor en el HTML 4.0 y en el cliente para el HTML MSDHTML o CSS2.

## Mantener cambios de presentación {#maintaining-presentation-changes}

A medida que se desplaza entre páginas de HTML (paneles), solo se mantiene el estado de los datos. La configuración, como el color de fondo o la configuración de campo obligatoria, no se mantiene (si es diferente a la configuración inicial). Para mantener el estado de la presentación, debe crear campos (normalmente ocultos) que representen el estado de presentación de los campos. Si añade una secuencia de comandos al `Calculate` Si cambia la presentación en función de valores de campos ocultos, puede conservar el estado de la presentación al moverse de un lado a otro entre las páginas del HTML (paneles).

La siguiente secuencia de comandos mantiene el `fillColor` de un campo basado en el valor de `hiddenField`. Supongamos que esta secuencia de comandos se encuentra en el campo `Calculate` evento.

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
Los objetos estáticos no se muestran en un formulario de HTML procesado cuando están anidados dentro de una celda de tabla. Por ejemplo, un círculo y un rectángulo anidados dentro de una celda de tabla no se muestran dentro de un formulario de HTML de procesamiento. Sin embargo, estos mismos objetos estáticos se muestran correctamente cuando se encuentran fuera de la tabla.

## Firma digital de formularios de HTML {#digitally-signing-html-forms}

No se puede firmar un formulario de HTML que contenga un campo de firma digital si el formulario se representa como una de las siguientes transformaciones de HTML:

* AHTML
* HTML4
* StaticHTML
* NoScriptXHTML

Para obtener información sobre cómo firmar digitalmente un documento, consulte [Firmar y certificar documentos digitalmente](/help/forms/developing/digitally-signing-certifying-documents.md)

## Procesar un formulario XHTML compatible con las directrices de accesibilidad {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

Puede procesar un formulario de HTML completo que cumpla con las directrices de accesibilidad. Es decir, el formulario se procesa con etiquetas de HTML HTML completas, en lugar de procesarse en las etiquetas de cuerpo (no en una página de HTML completa).

## Validación de datos de formulario {#validating-form-data}

Se recomienda limitar el uso de reglas de validación para los campos de formulario al procesar el formulario como un formulario de HTML. Es posible que algunas reglas de validación no sean compatibles con los formularios de HTML. Por ejemplo, cuando se aplica un patrón de validación de DD-MM-AAAA a una `Date/Time` que se encuentra en un diseño de formulario que se representa como un formulario de HTML, no funciona correctamente, aunque la fecha se escriba correctamente. Sin embargo, este patrón de validación funciona correctamente para formularios procesados como PDF.

>[!NOTE]
Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para procesar un formulario de HTML, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Establecer las opciones de tiempo de ejecución del HTML.
1. Procesar un formulario de HTML.
1. Escriba el flujo de datos del formulario en el explorador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API de cliente de Forms**

Para poder importar datos mediante programación en una API de cliente de formulario de PDF, debe crear un cliente del servicio de integración de datos de formulario. Al crear un cliente de servicios, define la configuración de conexión necesaria para invocar un servicio.

**Establecer las opciones de tiempo de ejecución del HTML**

Las opciones en tiempo de ejecución de HTML se establecen al procesar un formulario de HTML. Por ejemplo, puede agregar una barra de herramientas a un formulario de HTML para permitir a los usuarios seleccionar archivos adjuntos ubicados en el equipo cliente o recuperar archivos adjuntos que se representan con el formulario de HTML. De forma predeterminada, una barra de herramientas del HTML está desactivada. Para agregar una barra de herramientas a un formulario de HTML, debe establecer las opciones en tiempo de ejecución mediante programación. De forma predeterminada, una barra de herramientas del HTML consta de los siguientes botones:

* `Home`: Proporciona un vínculo a la raíz web de la aplicación.
* `Upload`: proporciona una interfaz de usuario para seleccionar archivos que se adjuntarán al formulario actual.
* `Download`: Proporciona una interfaz de usuario para mostrar los archivos adjuntos.

Cuando aparece una barra de herramientas de HTML en un formulario de HTML, un usuario puede seleccionar un máximo de diez archivos para enviarlos junto con los datos del formulario. Una vez enviados los archivos, el servicio Forms puede recuperarlos.

Al procesar un formulario como HTML, puede especificar un valor de usuario-agente. Un valor user-agent proporciona información sobre el explorador y el sistema. Este es un valor opcional y puede pasar un valor de cadena vacío. El inicio rápido Representar un formulario de HTML mediante la API de Java muestra cómo obtener un valor de agente de usuario y utilizarlo para procesar un formulario como HTML.

Las direcciones URL HTTP donde se publican los datos del formulario se pueden especificar estableciendo la dirección URL de destino mediante la API del cliente de servicio de Forms o en el botón Enviar incluido en el diseño de formulario XDP. Si la dirección URL de destino se especifica en el diseño de formulario, no establezca ningún valor mediante la API de cliente de servicio de Forms.

>[!NOTE]
La representación de un formulario de HTML con una barra de herramientas es opcional.

>[!NOTE]
Si procesa un formulario AHTML, se recomienda no agregar una barra de herramientas al formulario.

**Procesar un formulario de HTML**

Para procesar un formulario de HTML, debe especificar un diseño de formulario creado en Designer y guardado como archivo XDP. También debe seleccionar un tipo de transformación de HTML. Por ejemplo, puede especificar el tipo de transformación de HTML que procesa un HTML dinámico para Internet Explorer 5.0 o posterior.

El procesamiento de un formulario de HTML también requiere valores, como valores de URI, necesarios para procesar otros tipos de formulario.

**Escribir el flujo de datos del formulario en el explorador web del cliente**

Cuando el servicio Forms procesa un formulario de HTML, devuelve un flujo de datos de formulario que debe escribir en el explorador web del cliente. Cuando se escribe en el explorador web del cliente, el formulario del HTML es visible para el usuario.

**Consulte también**

[Procesar un formulario como HTML mediante la API de Java](#render-a-form-as-html-using-the-java-api)

[Procesar un formulario como HTML mediante la API de servicio web](#render-a-form-as-html-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Procesar formularios PDF interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Representar Forms de HTML con barras de herramientas personalizadas](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[Crear aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Procesar un formulario como HTML mediante la API de Java {#render-a-form-as-html-using-the-java-api}

Procesar un formulario de HTML mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clase del proyecto Java.

1. Crear un objeto de API de cliente de Forms

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `FormsServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Establecer las opciones de tiempo de ejecución del HTML

   * Crear un `HTMLRenderSpec` mediante su constructor.
   * Para procesar un formulario de HTML con una barra de herramientas, invoque la variable `HTMLRenderSpec` del objeto `setHTMLToolbar` método y pase un `HTMLToolbar` valor de enumeración. Por ejemplo, para mostrar una barra de herramientas de HTML vertical, pase `HTMLToolbar.Vertical`.
   * Para establecer el valor de configuración regional del formulario de HTML, invoque el `HTMLRenderSpec` del objeto `setLocale` y pasan un valor de cadena que especifica el valor de configuración regional. (Es una configuración opcional).
   * Para procesar el formulario de HTML con las etiquetas de HTML completas, invoque el `HTMLRenderSpec` del objeto `setOutputType` método y pase `OutputType.FullHTMLTags`. (Es una configuración opcional).

   >[!NOTE]
   Forms no se representan correctamente en HTML cuando el `StandAlone` La opción es `true` y el `ApplicationWebRoot` hace referencia a un servidor que no es el servidor de aplicaciones J2EE que aloja AEM Forms (el `ApplicationWebRoot` El valor se especifica utilizando `URLSpec` objeto que se pasa al `FormsServiceClient` del objeto `(Deprecated) renderHTMLForm` método). Si la variable `ApplicationWebRoot` es otro servidor del que aloja AEM Forms, el valor del URI raíz de la web en la consola de administración debe establecerse como el valor del URI de la aplicación web del formulario. Esto se puede hacer iniciando sesión en la consola de administración, haciendo clic en Servicios > Forms y estableciendo el URI de la raíz web como https://server-name:port/FormServer. A continuación, guarde la configuración.

1. Procesar un formulario de HTML

   Invoque el `FormsServiceClient` del objeto `(Deprecated) renderHTMLForm` y pasar los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta de acceso completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valor de enumeración que especifica el tipo de preferencia del HTML. Por ejemplo, para procesar un formulario de HTML compatible con dynamic HTML para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un vacío `com.adobe.idp.Document` objeto.
   * El `HTMLRenderSpec` que almacena las opciones de tiempo de ejecución de HTML.
   * Un valor de cadena que especifica la variable `HTTP_USER_AGENT` valor del encabezado; por ejemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` que almacena los valores de URI necesarios para procesar un formulario de HTML.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El `(Deprecated) renderHTMLForm` El método devuelve un valor `FormsResult` que contiene un flujo de datos de formulario que se puede escribir en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Crear un `com.adobe.idp.Document` invocando el objeto de `FormsResult` objeto ‘s `getOutputContent` método.
   * Obtenga el tipo de contenido del `com.adobe.idp.Document` invocando su objeto `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasando el tipo de contenido del `com.adobe.idp.Document` objeto.
   * Crear un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos de formulario en el explorador web del cliente invocando el `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Crear un `java.io.InputStream` invocando el objeto de `com.adobe.idp.Document` del objeto `getInputStream` método.
   * Cree una matriz de bytes y rellénela con el flujo de datos de formulario invocando el método `InputStream` del objeto `read` y pasando la matriz de bytes como argumento.
   * Invoque el `javax.servlet.ServletOutputStream` del objeto `write` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes a `write` método.

**Consulte también**

[Procesar formularios como HTML](#rendering-forms-as-html)

[Inicio rápido (modo SOAP): Procesamiento de un formulario de HTML mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Procesar un formulario como HTML mediante la API de servicio web {#render-a-form-as-html-using-the-web-service-api}

Procesar un formulario de HTML mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases de proxy Java en la ruta de clase.

1. Crear un objeto de API de cliente de Forms

   Crear un `FormsService` y establezca los valores de autenticación.

1. Establecer las opciones de tiempo de ejecución del HTML

   * Crear un `HTMLRenderSpec` mediante su constructor.
   * Para procesar un formulario de HTML con una barra de herramientas, invoque la variable `HTMLRenderSpec` del objeto `setHTMLToolbar` método y pase un `HTMLToolbar` valor de enumeración. Por ejemplo, para mostrar una barra de herramientas de HTML vertical, pase `HTMLToolbar.Vertical`.
   * Para establecer el valor de configuración regional del formulario de HTML, invoque el `HTMLRenderSpec` del objeto `setLocale` y pasan un valor de cadena que especifica el valor de configuración regional. Para obtener más información, consulte [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Para procesar el formulario de HTML con las etiquetas de HTML completas, invoque el `HTMLRenderSpec` del objeto `setOutputType` método y pase `OutputType.FullHTMLTags`.

   >[!NOTE]
   Forms no se representan correctamente en HTML cuando el `StandAlone` La opción es `true` y el `ApplicationWebRoot` hace referencia a un servidor que no es el servidor de aplicaciones J2EE que aloja AEM Forms (el `ApplicationWebRoot` El valor se especifica utilizando `URLSpec` objeto que se pasa al `FormsServiceClient` del objeto `(Deprecated) renderHTMLForm` método). Si la variable `ApplicationWebRoot` es otro servidor del que aloja AEM Forms, el valor del URI raíz de la web en la consola de administración debe establecerse como el valor del URI de la aplicación web del formulario. Esto se puede hacer iniciando sesión en la consola de administración, haciendo clic en Servicios > Forms y estableciendo el URI de la raíz web como https://server-name:port/FormServer. A continuación, guarde la configuración.

1. Procesar un formulario de HTML

   Invoque el `FormsService` del objeto `(Deprecated) renderHTMLForm` y pasar los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta de acceso completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valor de enumeración que especifica el tipo de preferencia del HTML. Por ejemplo, para procesar un formulario de HTML compatible con dynamic HTML para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * A `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar los datos, apruebe `null`. (Consulte [Rellenado previo de Forms con diseños flexibles](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts).)
   * El `HTMLRenderSpec` que almacena las opciones de tiempo de ejecución de HTML.
   * Un valor de cadena que especifica la variable `HTTP_USER_AGENT` valor del encabezado; por ejemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Puede pasar una cadena vacía si no desea establecer este valor.
   * A `URLSpec` que almacena los valores de URI necesarios para procesar un formulario de HTML. (Consulte [Especificar valores de URI](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario. (Consulte [Adjuntar archivos al formulario](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * Un vacío `com.adobe.idp.services.holders.BLOBHolder` objeto que rellena el método. Este valor de parámetro almacena el formulario procesado.
   * Un vacío `com.adobe.idp.services.holders.BLOBHolder` objeto que rellena el método. Este parámetro almacenará los datos XML de salida.
   * Un vacío `javax.xml.rpc.holders.LongHolder` objeto que rellena el método. Este argumento almacenará el número de páginas en el formulario.
   * Un vacío `javax.xml.rpc.holders.StringHolder` objeto que rellena el método. Este argumento almacenará el valor de configuración regional.
   * Un vacío `javax.xml.rpc.holders.StringHolder` objeto que rellena el método. Este argumento almacenará el valor de procesamiento del HTML que se utiliza.
   * Un vacío `com.adobe.idp.services.holders.FormsResultHolder` que contendrá los resultados de esta operación.

   El `(Deprecated) renderHTMLForm` rellena el método `com.adobe.idp.services.holders.FormsResultHolder` que se pasa como el último valor de argumento con un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Crear un `FormResult` al obtener el valor de la variable `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value` miembro de datos.
   * Crear un `BLOB` que contiene datos de formulario invocando el `FormsResult` del objeto `getOutputContent` método.
   * Obtenga el tipo de contenido del `BLOB` invocando su objeto `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasando el tipo de contenido del `BLOB` objeto.
   * Crear un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos de formulario en el explorador web del cliente invocando el `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Cree una matriz de bytes y rellénela invocando el método `BLOB` del objeto `getBinaryData` método. Esta tarea asigna el contenido del `FormsResult` a la matriz de bytes.
   * Invoque el `javax.servlet.http.HttpServletResponse` del objeto `write` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes a `write` método.

**Consulte también**

[Procesar formularios como HTML](#rendering-forms-as-html)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
