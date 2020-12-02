---
title: Configuración de la acción Enviar
seo-title: Configuración de la acción Enviar
description: AEM Forms permite configurar una acción de envío para definir cómo se procesa un formulario adaptable después del envío. Puede utilizar acciones de envío integradas o escribir las suyas propias desde cero.
seo-description: AEM Forms permite configurar una acción de envío para definir cómo se procesa un formulario adaptable después del envío. Puede utilizar acciones de envío integradas o escribir las suyas propias desde cero.
uuid: 4368d648-88ea-4f84-a051-46296a1a084e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9d8d7044-ffce-4ab4-9543-a2d2f9da31e3
docset: aem65
translation-type: tm+mt
source-git-commit: c74d9e86727f2deda62b8d1eb105b28ef4b6d184
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 1%

---


# Configuración de la acción Enviar{#configuring-the-submit-action}

## Introducción al envío de acciones {#introduction-to-submit-actions}

Una acción de envío se activa cuando un usuario hace clic en el botón Enviar de un formulario adaptable. Puede configurar la acción de envío en un formulario adaptable. Los formularios adaptables proporcionan algunas acciones de envío predeterminadas. Puede copiar y ampliar las acciones de envío predeterminadas para crear su propia acción de envío. Sin embargo, según sus necesidades, puede escribir y registrar su propia acción de envío para procesar los datos en el formulario enviado. La acción de envío puede utilizar [envío sincrónico o asincrónico](../../forms/using/asynchronous-submissions-adaptive-forms.md).

Puede configurar una acción de envío en la sección **Envío** de las propiedades del Contenedor de formulario adaptable, en la barra lateral.

![Configurar acción de envío](assets/thank-you-setting.png)

Configurar acción de envío

Las acciones de envío predeterminadas disponibles con formularios adaptables son:

* Enviar al extremo REST
* Enviar correo electrónico
* Enviar archivo PDF por correo electrónico
* Invocar un Forms Workflow
* Enviar mediante modelo de datos de formulario
* Acción de envío de Forms Portal
* Invocar un flujo de trabajo AEM

>[!NOTE]
>
>La acción Enviar PDF por correo electrónico solo se aplica a los formularios adaptables que utilizan una plantilla XFA como modelo de formulario.

>[!NOTE]
>
>Asegúrese de que [AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM folder
>existe. El directorio es necesario para almacenar temporalmente archivos adjuntos. Si el directorio no existe, créelo.

>[!CAUTION]
>
>Si [rellena previamente](../../forms/using/prepopulate-adaptive-form-fields.md) una plantilla de formulario, un modelo de datos de formulario o un formulario adaptable basado en esquema con una queja de datos XML o JSON con una esquema (esquema XML, esquema JSON, plantilla de formulario o modelo de datos de formulario) que sea datos no contenga etiquetas &lt;afData>, &lt;afBoundData> y &lt;/afUnboundData>, entonces los datos de los campos no enlazados (datos) Los campos sin límite son campos de formulario adaptables sin [bindref](../../forms/using/prepopulate-adaptive-form-fields.md) propiedad) del formulario adaptable se pierde.

Puede escribir una acción de envío personalizada para los formularios adaptables a fin de que se cumpla el caso de uso. Para obtener más información, consulte [Escritura de una acción Enviar personalizada para formularios adaptables](../../forms/using/custom-submit-action-form.md).

## Enviar al extremo REST {#submit-to-rest-endpoint}

La opción de envío **Enviar a extremo REST** pasa los datos rellenados en el formulario a una página de confirmación configurada como parte de la solicitud de GET HTTP. Puede agregar el nombre de los campos que se van a solicitar. El formato de la solicitud es:

`{fieldName}={request parameter name}`

Como se muestra en la siguiente imagen, los campos `param1` y `param2` se pasan como parámetros con valores copiados de los campos **cuadro de texto** y **cuadro numérico** para la siguiente acción.

También puede **Habilitar solicitud de POST** y proporcionar una dirección URL para publicar la solicitud. Para enviar datos al servidor de AEM que aloja el formulario, utilice una ruta relativa correspondiente a la ruta raíz del servidor de AEM. Por ejemplo, /content/forms/af/SampleForm.html. Para enviar datos a cualquier otro servidor, utilice la ruta absoluta.

![Configuración de la acción de envío de extremo restante](assets/action-config.png)

Configuración de la acción de envío de extremo restante

>[!NOTE]
Para pasar los campos como parámetros en una URL REST, todos los campos deben tener nombres de elementos diferentes, incluso si los campos se colocan en paneles diferentes.

### Publicar datos enviados a un recurso o punto final de reposo externo  {#post-submitted-data-to-a-resource-or-external-rest-end-point-nbsp}

Utilice la acción **Enviar al extremo REST** para publicar los datos enviados en una URL de reposo. La dirección URL puede ser de un servidor interno (el servidor en el que se procesa el formulario) o de un servidor externo.

Para enviar datos a un servidor interno, proporcione la ruta del recurso. Los datos se publican en la ruta del recurso. Por ejemplo, /content/restEndPoint. Para esas solicitudes de publicación se utiliza la información de autenticación de la solicitud de envío.

Para enviar datos a un servidor externo, proporcione una URL. El formato de la dirección URL es https://host:port/path_to_rest_end_point. Asegúrese de configurar la ruta de acceso para gestionar la solicitud de POST de forma anónima.

![Asignación de valores de campo pasados como parámetros de página de agradecimiento](assets/post-enabled-actionconfig.png)

En el ejemplo anterior, la información introducida por el usuario en `textbox` se captura usando el parámetro `param1`. La sintaxis para publicar datos capturados con `param1` es:

`String data=request.getParameter("param1");`

Del mismo modo, los parámetros que se utilizan para publicar datos XML y archivos adjuntos son `dataXml` y `attachments`.

Por ejemplo, estos dos parámetros se utilizan en la secuencia de comandos para analizar los datos en un punto final de descanso. Se utiliza la siguiente sintaxis para almacenar y analizar los datos:

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

En este ejemplo, `data` almacena los datos XML y `att` almacena los datos adjuntos.

## Enviar correo electrónico {#send-email}

La acción de envío **Enviar correo electrónico** envía un mensaje de correo electrónico a uno o varios destinatarios cuando el formulario se envía correctamente. El correo electrónico generado puede contener datos de formulario en un formato predefinido.

>[!NOTE]
Todos los campos de formulario deben tener nombres de elementos diferentes, incluso si se colocan en paneles diferentes), para incluir datos de formulario en un mensaje de correo electrónico.

## Enviar archivo PDF por correo electrónico {#send-pdf-via-email}

La acción de envío **Enviar PDF por correo electrónico** envía un mensaje de correo electrónico con un PDF que contiene datos del formulario a uno o más destinatarios cuando el formulario se envía correctamente.

>[!NOTE]
Esta acción de envío está disponible para formularios adaptables basados en XFA y formularios de adaptación basados en XSD que tienen el Documento de plantilla de registro.

## Invocar un flujo de trabajo de formularios {#invoke-a-forms-workflow}

La opción de envío **Enviar a Forms workflow** envía un xml de datos y archivos adjuntos (si los hay) a un LiveCycle de Adobe existente o a AEM Forms en el proceso JEE.

Para obtener información sobre cómo configurar la acción de envío del flujo de trabajo Enviar a formularios, consulte [Envío y procesamiento de los datos del formulario mediante flujos de trabajo de formulario](../../forms/using/submit-form-data-livecycle-process.md).

## Enviar mediante modelo de datos de formulario {#submit-using-form-data-model}

La acción de envío **Enviar mediante el modelo de datos de formulario** escribe los datos del formulario adaptable enviados para el objeto del modelo de datos especificado en un modelo de datos de formulario a su origen de datos. Al configurar la acción de envío, puede elegir un objeto de modelo de datos cuyos datos enviados desee volver a escribir en su origen de datos.

Además, puede enviar un archivo adjunto de formulario mediante un modelo de datos de formulario y un Documento de registro (DoR) al origen de datos.

Para obtener información sobre el modelo de datos de formulario, consulte [Integración de datos de AEM Forms](../../forms/using/data-integration.md).

## Acción de envío de Forms Portal {#forms-portal-submit-action}

La opción **Acción de envío de Forms Portal** hace que los datos del formulario estén disponibles a través de un portal de AEM Forms.

Para obtener más información sobre el portal de Forms y la acción de envío, consulte [Componente Borradores y envíos](../../forms/using/draft-submission-component.md).

## Invocar un flujo de trabajo AEM {#invoke-an-aem-workflow}

La acción de envío **Invocar un flujo de trabajo de AEM** asocia un formulario adaptable con un flujo de trabajo de AEM. Cuando se envía un formulario, el flujo de trabajo asociado se inicio automáticamente en el nodo de procesamiento. Además, coloca el archivo de datos, los archivos adjuntos y el documento de registro, si corresponde, en la ubicación de carga útil del flujo de trabajo.

Antes de usar la acción de envío **Invocar un flujo de trabajo AEM**, [configure la configuración de DS AEM](../../forms/using/configuring-the-processing-server-url-.md). Para obtener información sobre la creación de un flujo de trabajo AEM, consulte [flujos de trabajo centrados en el formulario en OSGi](../../forms/using/aem-forms-workflow.md).

## Revalidación del lado del servidor en formulario adaptable {#server-side-revalidation-in-adaptive-form}

Normalmente, en cualquier sistema de captura de datos en línea, los desarrolladores colocan algunas validaciones de JavaScript en el lado del cliente para aplicar algunas reglas comerciales. Pero en los navegadores modernos, los usuarios finales pueden evitar estas validaciones y realizar envíos manualmente utilizando diversas técnicas, como la consola DevTools del explorador Web. Estas técnicas también son válidas para los formularios adaptables. Un desarrollador de formularios puede crear varios objetivos de validación, pero, técnicamente, los usuarios finales pueden omitir dichos objetivos de validación y enviar datos no válidos al servidor. Los datos no válidos rompen las reglas comerciales que ha aplicado un autor de formularios.

La función de revalidación del lado del servidor permite ejecutar también las validaciones proporcionadas por un autor de formularios adaptables al diseñar un formulario adaptable en el servidor. Evita cualquier posible transacción de envíos de datos y violaciones de reglas comerciales representadas en términos de validaciones de formularios.

### ¿Qué validar en el servidor? {#what-to-validate-on-server-br}

Todas las validaciones de campo predefinidas (OOTB) de un formulario adaptable que se vuelven a ejecutar en el servidor son:

* Requerido
* Cláusula de imagen de validación
* Expresión de validación

### Habilitación de la validación del lado del servidor {#enabling-server-side-validation-br}

Use la **Revalidate en server** en Contenedor de formulario adaptable en la barra lateral para habilitar o deshabilitar la validación del lado del servidor para el formulario actual.

![Activación de la validación del lado del servidor](assets/revalidate-on-server.png)

Activación de la validación del lado del servidor

Si el usuario final omite esas validaciones y envía los formularios, el servidor volverá a realizar la validación. Si la validación falla al finalizar el servidor, se detiene la transacción de envío. Al usuario final se le presenta de nuevo el formulario original. Los datos capturados y enviados se presentan al usuario como un error.

### Compatibilidad con funciones personalizadas en Expresiones de validación {#supporting-custom-functions-in-validation-expressions-br}

En ocasiones, en el caso de **reglas de validación complejas**, la secuencia de comandos de validación exacta reside en funciones personalizadas y el autor llama a estas funciones personalizadas desde la expresión de validación de campo. Para que esta biblioteca de funciones personalizada sea conocida y esté disponible mientras realiza validaciones en el servidor, el autor del formulario puede configurar el nombre de AEM biblioteca de cliente en la ficha **Basic** de las propiedades del Contenedor de formulario adaptable, como se muestra a continuación.

![Compatibilidad con funciones personalizadas en Expresiones de validación](assets/clientlib-cat.png)

Compatibilidad con funciones personalizadas en Expresiones de validación

El autor puede configurar la biblioteca customJavaScript por formulario adaptable. En la biblioteca, solo mantenga las funciones reutilizables, que dependen de bibliotecas de terceros jquery y underscore.js.

## Administración de errores en la acción de envío {#error-handling-on-submit-action}

Como parte de AEM directrices de seguridad y endurecimiento, configure páginas de error personalizadas como 404.jsp y 500.jsp. Se llama a estos controladores cuando aparece un error 404 o 500 al enviar un formulario. También se llaman a los controladores cuando estos códigos de error se activan en el nodo Publicar.

Para obtener más información, consulte [Personalización de páginas que muestra el controlador de errores](/help/sites-developing/customizing-errorhandler-pages.md).
