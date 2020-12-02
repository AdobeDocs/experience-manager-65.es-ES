---
title: 'Flujo de trabajo centrado en Forms en OSGi: referencia de pasos'
seo-title: 'Flujo de trabajo centrado en Forms en OSGi: referencia de pasos'
description: El flujo de trabajo centrado en Forms en los pasos de OSGi le permite crear rápidamente flujos de trabajo basados en formularios adaptables.
seo-description: El flujo de trabajo centrado en Forms en los pasos de OSGi le permite crear rápidamente flujos de trabajo basados en formularios adaptables.
uuid: 6f791c45-0e35-4c55-9106-5340caab94b7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: f0a5588d-f210-4f04-bc35-b62834f90ab1
docset: aem65
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '7109'
ht-degree: 0%

---


# Flujo de trabajo centrado en Forms en OSGi: referencia de pasos{#forms-centric-workflow-on-osgi-step-reference}

## Pasos del Forms Workflow {#forms-workflow-steps}

Los pasos del flujo de trabajo de Forms realizan operaciones específicas de AEM Forms en un flujo de trabajo AEM. Estos pasos le permiten crear rápidamente formularios adaptables basados en un flujo de trabajo centrado en Forms en OSGi. Estos flujos de trabajo se pueden utilizar para desarrollar flujos de trabajo básicos de revisión y aprobación, procesos comerciales internos y entre servidores de seguridad. También puede utilizar los pasos de Forms Workflow para inicio de servicios de documento, integrarlos con el flujo de trabajo de firma de Adobe Sign y realizar otras operaciones de AEM Forms. Debe [AEM Forms Add-on](https://www.adobe.com/go/learn_aemforms_documentation_63) utilizar estos pasos en un flujo de trabajo.

## Asignar paso de tarea {#assign-task-step}

El paso de asignación de tarea crea una tarea y la asigna a un usuario o grupo. Junto con la asignación de la tarea, el componente también especifica el formulario adaptable o PDF no interactivo para la tarea. El formulario adaptable es necesario para aceptar datos introducidos por los usuarios y se utiliza un PDF no interactivo o un formulario adaptable de sólo lectura para flujos de trabajo solo de revisión.

También puede utilizar el componente para controlar el comportamiento de la tarea. Por ejemplo, crear un documento de registro automático, asignar la tarea a un usuario o grupo específico, especificar la ruta de los datos enviados, especificar la ruta de los datos que se van a rellenar previamente y especificar las acciones predeterminadas. El paso Asignar Tarea tiene las siguientes propiedades:

* **Título:** Título de la tarea. El título se muestra en AEM Bandeja de entrada.
* **Descripción:** Explicación de las operaciones que se realizan en la tarea. Esta información resulta útil para otros desarrolladores de procesos cuando trabaja en un entorno de desarrollo compartido.

* **Ruta de miniatura:** Ruta de la miniatura de la tarea. Si no se especifica ninguna ruta, se muestra una miniatura predeterminada de formulario adaptable y, en Documento de Grabar, se muestra un icono predeterminado.
* **Etapa de flujo de trabajo:** un flujo de trabajo puede tener varias etapas. Estas etapas se muestran en la Bandeja de entrada AEM. Puede definir estas etapas en las propiedades del modelo (barra de tareas > Página > Propiedades de la página > Fases).
* **Prioridad:la prioridad** seleccionada se muestra en la Bandeja de entrada de AEM. Las opciones disponibles son Alta, Media y Baja. El valor predeterminado es Medio.
* **Fecha de vencimiento:** especifique el número de días u horas después de los cuales la tarea se marca como vencida. Si selecciona **Desactivado**, la tarea nunca se marca con retraso. También puede especificar un controlador de tiempo de espera para realizar tareas específicas después de que la tarea haya vencido.

* **Días:** el número de días antes de los cuales se completará la tarea. El número de días se contabiliza después de que la tarea se asigne a un usuario. Si una tarea no está completa y sobrepasa el número de días especificado en el campo Días, se activa un controlador de tiempo de espera después de la fecha de vencimiento.
* **Horas:** el número de horas antes de las cuales se completará la tarea. El número de horas se contabiliza después de que la tarea se asigne a un usuario. Si una tarea no está completa y sobrepasa el número de horas especificado en el campo Horas, si se selecciona, se activa un controlador de tiempo de espera después de las horas de vencimiento.
* **Tiempo de espera después de la fecha de vencimiento:** seleccione esta opción para activar el campo de selección del controlador de tiempo de espera.
* **Controlador de tiempo de espera:** seleccione la secuencia de comandos que se ejecutará cuando el paso de asignación de tarea sobrepase la fecha de vencimiento. Los scripts colocados en el repositorio de CRX en [aplicaciones]/fd/panel/scripts/timeoutHandler están disponibles para su selección. La ruta especificada no existe en crx-repository. Un administrador crea la ruta antes de usarla.
* **Resalte la acción y el comentario de la última tarea en Detalles de Tarea:** seleccione esta opción para mostrar la última acción realizada y los comentarios recibidos en la sección de detalles de tarea de una tarea.
* **Tipo:** elija el tipo de documento que se va a rellenar al iniciar el flujo de trabajo. Puede elegir un formulario adaptable, un formulario adaptable de solo lectura, un documento PDF no interactivo, una interfaz de usuario del agente de comunicación interactiva o un Documento de Canal web de comunicación interactiva.
* **Utilizar formulario adaptable:** especifique el método para localizar el formulario adaptable de entrada. Esta opción está disponible si selecciona Formulario adaptable o Formulario adaptable de sólo lectura en la lista desplegable Tipo. Puede utilizar el formulario adaptable enviado al flujo de trabajo, disponible en una ruta absoluta o disponible en una ruta de acceso en una variable. Puede utilizar una variable de tipo String para especificar la ruta.\
   Puede asociar varios formularios adaptables con un flujo de trabajo. Como resultado, puede especificar un formulario adaptable en tiempo de ejecución mediante los métodos de entrada disponibles.

* **Utilizar comunicación interactiva:** especifique el método para localizar la comunicación interactiva de entrada. Puede utilizar la comunicación interactiva enviada al flujo de trabajo, disponible en una ruta absoluta o disponible en una ruta en una variable. Puede utilizar una variable de tipo String para especificar la ruta. Esta opción está disponible si selecciona la interfaz de usuario del agente de comunicación interactiva o el Documento del Canal web de comunicación interactiva en la lista desplegable Tipo.

>[!NOTE]
>
>Debe tener asignaciones de cm-agent-users y grupos de usuarios de flujo de trabajo para acceder a la interfaz de usuario de Interactive Communications Agent en AEM bandeja de entrada.

* **Formulario adaptable o Ruta** de comunicación interactiva: Especifique la ruta del formulario adaptable o la comunicación interactiva. Puede utilizar el formulario adaptable o la comunicación interactiva que se envía al flujo de trabajo, disponible en una ruta absoluta, o recuperar el formulario adaptable de una ruta almacenada en una variable de tipo de datos de cadena.
* **Seleccione el PDF de entrada mediante:** especifique la ruta de un documento PDF no interactivo. El campo está disponible cuando se selecciona un documento PDF no interactivo en el campo Tipo. Puede seleccionar el PDF de entrada utilizando la ruta relativa a la carga útil, guardada en una ruta absoluta o utilizando una variable de tipo de datos de Documento. Por ejemplo, [Directorio_de_carga]/Workflow/PDF/credit-card.pdf. La ruta no existe en crx-repository. Un administrador crea la ruta antes de usarla. Se requiere una opción Documento de registro activada o formularios adaptables basados en plantillas de formulario para utilizar la opción Ruta de PDF.
* **Para la tarea completada, procese el formulario adaptable como**: Cuando se marca una tarea como completa, el formulario adaptable se puede representar como un formulario adaptable de sólo lectura o como un documento PDF. Se requiere un Documento de la opción Registro activado o formularios adaptables basados en plantilla para procesar el formulario adaptable como Documento de registro.
* **Prerellenado:** Los siguientes campos sirven como entradas para la tarea:

   * **Seleccione el archivo de datos de entrada mediante:** Ruta del archivo de datos de entrada (.json,). xml, .doc o modelo de datos de formulario). Puede recuperar el archivo de datos de entrada mediante una ruta relativa a la carga útil o recuperar el archivo almacenado en una variable de tipo de datos Documento, XML o JSON. Por ejemplo, el archivo contiene los datos enviados para el formulario a través de una aplicación Bandeja de entrada AEM. Una ruta de ejemplo es [Payload_Directory]/workflow/data.
   * **Seleccione los datos adjuntos de entrada mediante:** Los datos adjuntos disponibles en la ubicación se adjuntan al formulario asociado a la tarea. La ruta siempre es relativa a la carga útil. Una ruta de ejemplo es [Payload_Directory]/attachments/
   * **Elija JSON de entrada:** seleccione un archivo JSON de entrada mediante una ruta relativa a la carga útil o almacenada en una variable de tipo de datos de Documento, JSON o Modelo de datos de formulario. Esta opción está disponible si selecciona la interfaz de usuario del agente de comunicación interactiva o el Documento del Canal web de comunicación interactiva en la lista desplegable Tipo.
   * **Elija un servicio de relleno previo personalizado:** seleccione el servicio de rellenado previo para recuperar los datos y cumplimente previamente el documento de canal web de comunicación interactiva o la interfaz de usuario del agente.

   * **Utilice el servicio de cumplimentación previa de la comunicación interactiva seleccionada arriba:** utilice esta opción para utilizar el servicio de cumplimentación previa de la comunicación interactiva definida en la lista desplegable Utilizar comunicación interactiva.
   * **Asignación de atributos de solicitud:** utilice la sección Asignación de atributos de solicitud para definir el  [nombre y el valor del atributo](../../forms/using/work-with-form-data-model.md#bindargument) de solicitud. Recupere los detalles del origen de datos en función del nombre y el valor del atributo especificados en la solicitud. Puede definir un valor de atributo de solicitud utilizando un valor literal o una variable de tipo de datos String.\
      Las opciones de asignación de atributos de solicitud y servicio de cumplimentación previa solo están disponibles si selecciona la IU de Agente de comunicación interactiva o el Documento de Canal Web de comunicación interactiva en la lista desplegable Tipo.

* **Información enviada:** Los siguientes campos sirven como ubicaciones de salida para la tarea:

   * **Guarde el archivo de datos de salida con:** Guarde el archivo de datos (.json,). xml, .doc o modelo de datos de formulario). El archivo de datos contiene información enviada a través del formulario asociado. Puede guardar el archivo de datos de salida con una ruta relativa a la carga útil o almacenarlo en una variable de tipo de datos Documento, XML o JSON. Por ejemplo, [Payload_Directory]/Workflow/data, donde los datos son un archivo.
   * **Guardar datos adjuntos mediante:** Guarde los datos adjuntos del formulario proporcionados en una tarea. Puede guardar los datos adjuntos mediante una ruta relativa a la carga útil o almacenarlos en una variable de matriz de tipo de datos de Documento.
   * **Guardar Documento de registro mediante:** Ruta para guardar un Documento del archivo de registro. Por ejemplo, [Directorio_de_carga]/DocumentofRecord/credit-card.pdf. Puede guardar el Documento de registro utilizando una ruta relativa a la carga útil o almacenarla en una variable de tipo de datos de Documento. Si selecciona la opción **Relativo a carga útil**, el Documento de registro no se genera si el campo de ruta se deja vacío. Esta opción solo está disponible si selecciona Formulario adaptable en la lista desplegable Tipo.

   * **Guarde los datos de Canal web con:** Guarde el archivo de datos de Canal web con una ruta relativa a la carga útil o almacene los datos en una variable de tipo de datos de Documento, JSON o Modelo de datos de formulario. Esta opción solo está disponible si selecciona la IU de Agente de comunicación interactiva en la lista desplegable Tipo.
   * **Guarde el documento PDF mediante:** Guarde el documento PDF utilizando una ruta relativa a la carga útil o bien almacene el archivo en una variable de tipo de datos de Documento. Esta opción solo está disponible si selecciona la IU de Agente de comunicación interactiva en la lista desplegable Tipo.
   * **Guarde la plantilla de diseño con:** Guarde la plantilla de diseño con una ruta relativa a la carga útil o almacenarla en una variable de tipo de datos de Documento. La [plantilla de diseño](../../forms/using/layout-design-details.md) hace referencia a un archivo XDP que se crea con Forms Designer. Esta opción solo está disponible si selecciona la IU de Agente de comunicación interactiva en la lista desplegable Tipo.

* **Asignación > Opciones de asignación:** especifique el método para asignar la tarea a un usuario. Puede asignar dinámicamente la tarea a un usuario o grupo mediante la secuencia de comandos Selector de participantes o asignar la tarea a un usuario o grupo de AEM específico.
* **Selector de participantes:** la opción está disponible cuando se selecciona la opción  **Dinámicamente para un usuario o** grupo en el campo Opciones de asignación. Puede utilizar un ECMAScript o un servicio para seleccionar dinámicamente un usuario o un grupo. Para obtener más información, consulte [Asignación dinámica de un flujo de trabajo a los usuarios](https://helpx.adobe.com/experience-manager/kb/HowToAssignAWorkflowDynamicallyToParticipants.html) y [Creación de un paso de participante dinámico de Adobe Experience Manager personalizado.](https://helpx.adobe.com/experience-manager/using/dynamic-steps.html)

* **Participantes:** el campo está disponible cuando se selecciona la opción  **[!UICONTROL com.adobe.granite.workflow.core.process.]** RandomParticipantChooseren en el campo  **Participante** Chooserfield. El campo permite seleccionar usuarios o grupos para la opción SelectorParticipanteAleatorio.

* **Usuario asignado:** El campo está disponible cuando se selecciona  **[!UICONTROL com.adobe.fd.workspace.step.service.]** VariableParticipantChooseris en el campo  **Selector de** participantes. El campo permite seleccionar una variable de tipo de datos String para definir al usuario asignado.

* **Argumentos:** El campo está disponible cuando se selecciona una secuencia de comandos distinta de la secuencia de comandos RandomParticipantChoose en el campo Selector de participantes. El campo permite proporcionar una lista de argumentos separados por coma para la secuencia de comandos seleccionada en el campo Selector de participantes.

* **Usuario o Grupo:** La tarea se asigna al usuario o grupo seleccionado. La opción está disponible cuando se selecciona la **opción para un usuario o grupo específico** en el campo **Asignar opciones**. El campo lista a todos los usuarios y grupos del grupo de usuarios del flujo de trabajo.\
   El menú desplegable **Usuario o Grupo** lista a los usuarios y grupos a los que tiene acceso el usuario que ha iniciado sesión. La visualización del nombre de usuario depende de si tiene permisos de acceso en el nodo **users** en crx-repository para ese usuario en particular.

* **Notificar al usuario asignado por correo electrónico:** seleccione esta opción para enviar notificaciones por correo electrónico al usuario asignado. Estas notificaciones se envían cuando se asigna una tarea a un usuario. Antes de utilizar la opción, habilite las notificaciones desde AEM consola web. Para obtener instrucciones paso a paso, consulte [configuración de las notificaciones por correo electrónico para el paso de asignación de tarea](../../forms/using/aem-forms-workflow.md)

* **Plantilla** de correo electrónico HTML: Seleccione la plantilla de correo electrónico para el correo electrónico de notificación. Para editar una plantilla, modifique el archivo ubicado en /libs/fd/dashboard/templates/email/htmlEmailTemplate.txt en crx-repository.
* **Permitir delegación a:** AEM la bandeja de entrada ofrece una opción al usuario que ha iniciado sesión para delegar el flujo de trabajo asignado a otro usuario. Puede delegar en el mismo grupo o en el usuario del flujo de trabajo de otro grupo. Si la tarea está asignada a un solo usuario y la opción **permitir delegación a miembros del grupo asignado** está seleccionada, no es posible delegar la tarea a otro usuario o grupo.
* **Compartir configuración:** AEM bandeja de entrada ofrece opciones para compartir una o todas las tareas de la bandeja de entrada con otros usuarios:
   * Cuando se selecciona la opción **Permitir que el usuario asignado comparta explícitamente en la bandeja de entrada**, el usuario puede hacer clic en la tarea y compartirla con otro usuario AEM.
   * Cuando se selecciona la opción **Permitir que el usuario asignado comparta mediante el uso compartido de la bandeja de entrada** y un usuario comparte los elementos de la Bandeja de entrada o permite que otros usuarios accedan a los elementos de la Bandeja de entrada, solo se comparten con otros usuarios las tareas con la opción antes mencionada.

* **Acciones > Acciones predeterminadas:están disponibles** las acciones Enviar, Guardar y Restablecer. De forma predeterminada, todas las acciones predeterminadas están activadas.
* **Variable de ruta:** Nombre de la variable de ruta. La variable route captura las acciones personalizadas que un usuario selecciona en AEM Bandeja de entrada.
* **Rutas:** una tarea puede ramificarse a diferentes rutas. Cuando se selecciona en AEM Bandeja de entrada, la ruta devuelve un valor y las ramas del flujo de trabajo se basan en la ruta seleccionada. Puede almacenar rutas en una variable de matriz de tipo de datos String o seleccionar **Literal** para agregar rutas manualmente.

* **Título**: Especifique el título de la ruta. Se muestra en AEM Bandeja de entrada.
* **Icono** de coral: Especifique el atributo HTML de un icono de coral. La biblioteca CorelUI de Adobe proporciona un amplio conjunto de iconos que se utilizan para el primer toque. Puede elegir y utilizar un icono para la ruta. Se muestra junto con el título en AEM Bandeja de entrada. Si almacena las rutas en una variable, las rutas utilizan un icono de coral &#39;Etiquetas&#39; predeterminado.
* **Permitir que el usuario asignado agregue un comentario**: Seleccione esta opción para activar los comentarios de la tarea. Un usuario asignado puede agregar los comentarios desde AEM Bandeja de entrada en el momento del envío de la tarea.
* **Guardar comentario en variable:** Guarde el comentario en una variable de tipo de datos String. Esta opción solo se muestra si selecciona la casilla **Permitir que el usuario asignado agregue un comentario**.

* **Permitir que el usuario asignado agregue datos adjuntos a la tarea**: Seleccione esta opción para activar los datos adjuntos para la tarea. Un usuario asignado puede agregar los datos adjuntos desde AEM Bandeja de entrada en el momento del envío de la tarea.
* **Guarde los datos adjuntos de tarea de salida mediante**: Especifique la ubicación de la carpeta de datos adjuntos. Puede guardar los datos adjuntos de tarea de salida utilizando una ruta relativa a la carga útil o en una variable de matriz de tipo de datos de documento. Esta opción solo se muestra si selecciona la casilla **Permitir que el usuario asignado agregue datos adjuntos a la casilla de verificación tarea** y selecciona **Formulario adaptable**, **Formulario adaptable de sólo lectura** o **documento PDF no interactivo** en la lista desplegable **Tipo**  en la ficha **Formulario/Documento**.

>[!NOTE]
>
>Utilice la ficha Datos adjuntos de la interfaz de usuario del agente durante el tiempo de ejecución para asociar los datos adjuntos a una comunicación interactiva. Los datos adjuntos asociados se muestran como datos adjuntos de tarea en la barra de tareas después de abrir el elemento de trabajo en estado Completo.

* **Usar metadatos personalizados:** seleccione esta opción para habilitar el campo de metadatos personalizado. Los metadatos personalizados se utilizan en plantillas de correo electrónico.
* **Metadatos personalizados:** seleccione metadatos personalizados para las plantillas de correo electrónico. Los metadatos personalizados están disponibles en el repositorio crx en apps/fd/panel/scripts/metadataScripts. La ruta especificada no existe en crx-repository. Un administrador crea la ruta antes de usarla. También puede utilizar un servicio para los metadatos personalizados. También puede ampliar la interfaz WorkitemUserMetadataService para proporcionar metadatos personalizados.
* **Mostrar datos de pasos** anteriores: Seleccione esta opción para habilitar a los cesionarios para la vista de los anteriores cesionarios, las medidas ya adoptadas en la tarea, los comentarios agregados a la tarea y el documento del registro de la tarea completada, si está disponible.
* **Mostrar datos de pasos subsiguientes:** seleccione esta opción para permitir que el usuario asignado actual vista la acción realizada y los comentarios agregados a la tarea por los usuarios asignados subsiguientes. También permite que el cesionario actual vista un documento del registro de la tarea finalizada, si está disponible.
* **Visibilidad del tipo de datos:** de forma predeterminada, un usuario asignado puede realizar una vista de un Documento de registro, de los usuarios asignados, de la acción realizada y de los comentarios que hayan agregado los usuarios asignados anteriores y posteriores. Utilice la opción de visibilidad de tipo de datos para limitar el tipo de datos visibles para los usuarios asignados.

## Enviar paso de correo electrónico {#send-email-step}

Utilice el paso de correo electrónico para enviar un correo electrónico, por ejemplo, un correo electrónico con un documento de registro, un vínculo de un formulario adaptable, un vínculo de una comunicación interactiva o un documento PDF adjunto. El paso Enviar correo electrónico admite [correo electrónico HTML](https://en.wikipedia.org/wiki/HTML_email). Los correos electrónicos HTML responden y se adaptan al cliente de correo electrónico y al tamaño de pantalla de los destinatarios. Puede utilizar una plantilla de correo electrónico HTML para definir el aspecto, el esquema de colores y el comportamiento del contenido del correo electrónico.

El paso de correo electrónico utiliza Day CQ Mail Service para enviar correos electrónicos. Antes de usar el paso de correo electrónico, asegúrese de que el [servicio de correo electrónico](../../forms/using/aem-forms-workflow.md) está configurado. El paso de correo electrónico tiene las siguientes propiedades:

**Título:** El título del paso ayuda a identificar el paso en el editor de flujo de trabajo.

**Descripción:** La explicación es útil para otros desarrolladores de procesos cuando trabaja en un entorno de desarrollo compartido.

**Asunto del correo electrónico:** Asunto se puede recuperar de los metadatos de un flujo de trabajo, especificarlos manualmente o recuperarlos del valor almacenado en una variable. Seleccione una de las siguientes opciones:

* **Literal: especifique** manualmente un asunto.
* **Recuperar de metadatos**  de flujo de trabajo: recupere el asunto de una propiedad de metadatos.
* **Variable** : recupere el asunto del valor almacenado en una variable de tipo de datos de cadena.

**Plantilla** de correo electrónico HTML: Plantilla HTML para el correo electrónico. Puede especificar variables en una plantilla de correo electrónico. El paso Correo electrónico extrae y muestra todas las variables incluidas en una plantilla para entradas.

**Metadatos de plantilla de correo electrónico: el** valor de las variables de plantilla de correo electrónico puede ser un valor especificado por el usuario, la ruta de un recurso en el autor o en el servidor de publicación, la imagen o una propiedad de metadatos del flujo de trabajo.

* **Literal:** utilice la opción cuando sepa el valor exacto que desea especificar. Por ejemplo, [example@example.com](mailto:example@example.com).

* **Metadatos de flujo de trabajo:** utilice la opción cuando el valor que se va a utilizar se guarde en una propiedad de metadatos de flujo de trabajo. Después de seleccionar la opción, introduzca el nombre de la propiedad de metadatos en el cuadro de texto vacío debajo de la opción Metadatos del flujo de trabajo. Por ejemplo, emailAddress.
* **URL del recurso:** utilice la opción para incrustar un vínculo web de una comunicación interactiva en el correo electrónico. Después de seleccionar la opción, busque y elija la comunicación interactiva que desea incrustar. El recurso puede residir en el autor o en el servidor de publicación.
* **Imagen:** utilice la opción para incrustar una imagen en el correo electrónico. Después de seleccionar la opción, busque y elija la imagen. La opción de imagen solo está disponible para las etiquetas de imagen (&lt;img src=&quot;*&quot;/>) disponibles en la plantilla de correo electrónico.

**Dirección de correo electrónico del remitente/Destinatario:** seleccione la opción  **** Literalpara especificar manualmente una dirección de correo electrónico o seleccione la opción  **Recuperar** metadatos del flujo de trabajo para recuperar la dirección de correo electrónico de una propiedad de metadatos. También puede especificar una lista de matrices de propiedades de metadatos para la opción **Recuperar de metadatos del flujo de trabajo**. Seleccione la opción **Variable** para recuperar la dirección de correo electrónico del valor almacenado en una variable de tipo de datos de cadena.

**Archivo adjunto:** el recurso disponible en la ubicación especificada se adjunta al correo electrónico. La ruta del recurso puede ser relativa a la carga útil o a la ruta absoluta. Una ruta de ejemplo es [Payload_Directory]/attachments/.

Seleccione la opción **Variable** para recuperar el archivo adjunto almacenado en una variable de tipo de datos Documento, XML o JSON.

**Nombre de archivo:** Nombre del archivo adjunto de correo electrónico. El paso de correo electrónico cambia el nombre de archivo original del archivo adjunto al nombre de archivo especificado. El nombre puede especificarse manualmente o recuperarse de una propiedad de metadatos de flujo de trabajo o de una variable. Utilice la opción **Literal** cuando sepa el valor exacto que desea especificar. Utilice la opción **Variable** para recuperar el nombre de archivo del valor almacenado en una variable de tipo de datos de cadena. Utilice la opción **Recuperar de un flujo de trabajo de metadatos** cuando el valor que se va a utilizar se guarde en una propiedad de metadatos de flujo de trabajo.

## Generar Documento del paso de registro {#generate-document-of-record-step}

Cuando se rellena o envía un formulario, puede guardarlo, en formato impreso o en documento. Esto se denomina Documento de registro (DoR). Puede utilizar el paso Generar Documento de registro para crear una versión PDF interactiva o de solo lectura de un formulario adaptable. La versión PDF contiene información rellenada en el formulario junto con la presentación del formulario adaptable.

El paso Documento de registro tiene las siguientes propiedades:

**Utilizar formulario** adaptable: Especifique el método para localizar el formulario adaptable de entrada. Puede utilizar el formulario adaptable enviado al flujo de trabajo, disponible en una ruta absoluta o disponible en una ruta de acceso en una variable. Puede utilizar una variable de tipo de datos String para especificar la ruta en el campo **Seleccionar variable para resolver**.\
Puede asociar varios formularios adaptables con un flujo de trabajo. Como resultado, puede especificar un formulario adaptable en tiempo de ejecución mediante los métodos de entrada disponibles.

**Ruta** de formulario adaptable: Especifique la ruta del formulario adaptable. El campo está disponible cuando selecciona la opción **Disponible en una ruta absoluta** en el campo **Usar formulario adaptable**.

**Seleccione Datos de entrada mediante:** Ruta de los datos de entrada para el formulario adaptable. Puede mantener los datos en una ubicación relativa a la carga útil, especificar una ruta absoluta de los datos o recuperar los datos almacenados en una variable de tipo de datos Documento, JSON o XML. Los datos de entrada se combinan con el formulario adaptable para crear un documento de registro.

**Seleccione Ruta de datos adjuntos de entrada mediante:** Ruta de los datos adjuntos. Estos anexos se incluyen en el Documento de registro. Puede mantener los datos adjuntos en una ubicación relativa a la carga útil, especificar una ruta absoluta de los datos adjuntos o recuperar los datos adjuntos almacenados en una variable de matriz de tipo de datos de Documento.

Si especifica la ruta de una carpeta, por ejemplo, los archivos adjuntos, todos los archivos disponibles directamente en la carpeta se adjuntan al Documento de registro. Si hay algún archivo disponible en las carpetas directamente disponibles en la ruta de datos adjuntos especificada, los archivos se incluyen en el Documento de Grabar como archivos adjuntos. Si hay carpetas en carpetas disponibles directamente, se omitirán.

**Guardar Documento generado de registro con las siguientes opciones:** especifique la ubicación para guardar un documento del archivo de registro. Puede sobrescribir la carpeta de carga útil, colocar el documento del registro en una ubicación dentro del directorio de carga útil o almacenar el documento del registro en una variable de tipo de datos de Documento.

**Configuración regional**: Especifique el idioma del documento del registro. Seleccione **Literal** para seleccionar la configuración regional en una lista desplegable o seleccione **Variable** para recuperar la configuración regional del valor almacenado en una variable de tipo de datos de cadena. Debe definir el código de configuración regional mientras almacena el valor de la configuración regional en una variable. Por ejemplo, especifique **es_ES** para inglés y **fr_FR** para francés.

## Invocar el paso del servicio del modelo de datos de formulario {#invoke-form-data-model-service-step}

Puede utilizar [Integración de datos de AEM Forms](../../forms/using/data-integration.md) para configurar y conectarse a orígenes de datos dispares. Estas fuentes de datos pueden ser una base de datos, servicio Web, servicio REST, servicio OData y solución CRM. La integración de datos de AEM Forms le permite crear un modelo de datos de formulario que incluye varios servicios para realizar operaciones de recuperación de datos, además de actualizar en la base de datos configurada. Puede utilizar el paso **Invocar el servicio del modelo de datos** para seleccionar un modelo de datos de formulario (FDM) y utilizar los servicios de FDM para recuperar, actualizar o agregar datos a orígenes de datos dispares.

Para explicar las entradas de los campos del paso, se utiliza como ejemplo la siguiente tabla de base de datos y el archivo JSON:

**Tabla CustomerDetails de muestra**

<table>
 <tbody> 
  <tr> 
   <td>Propiedad</td> 
   <td>Value<br /> </td> 
  </tr> 
  <tr> 
   <td>Nombre<br /> </td> 
   <td>Sarah<br /> </td> 
  </tr> 
  <tr> 
   <td>Apellidos</td> 
   <td>Rosa</td> 
  </tr> 
  <tr> 
   <td>ID de cliente</td> 
   <td>1</td> 
  </tr> 
  <tr> 
   <td>Dirección de correo electrónico<br /> </td> 
   <td>srose@we.info</td> 
  </tr> 
 </tbody> 
</table>

**Archivo JSON de muestra**

```json
  { 
    customer: { 
     firstName: "Sarah", 
     lastName:"Rose", 
     customerId: "1", 
     emailAddress:"srose@we.info" 
   }, 
    insurance: {
     customerId: "1", 
    policyType: "Premium,
    policyNumber: "Premium-521499",
    customerDetails: { 
     firstName: "Sarah",
     lastName: "Rose",
     customerId: "1",
     emailAddress: "srose@we.info" 
    }
   }
  }
```

El paso Invocar el servicio del modelo de datos de formulario tiene los campos siguientes para facilitar las operaciones del modelo de datos de formulario:

* **Título:** Título del paso. Ayuda a identificar el paso en el editor de flujo de trabajo.
* **Descripción:** Explicación útil para otros desarrolladores de procesos cuando trabaja en un entorno de desarrollo compartido.

* **Ruta** del modelo de datos de formulario: Busque y seleccione un modelo de datos de formulario presente en el servidor.

* **Servicio**: Lista de los servicios que proporciona el modelo de datos de formulario seleccionado.
* **Entrada para servicios > Proporcionar datos de entrada mediante metadatos literales, variables o de flujo de trabajo, y un archivo** JSON: Un servicio puede tener varios argumentos. Seleccione la opción para obtener el valor de los argumentos de servicio de una propiedad de metadatos de flujo de trabajo, un objeto JSON o una variable, o bien, introduzca directamente el valor en el cuadro de texto proporcionado:

   * **Literal:** utilice la opción cuando sepa el valor exacto que desea especificar. Por ejemplo, srose@we.info.
   * **Variable:** utilice la opción para recuperar el valor almacenado en una variable.
   * **Recuperar de metadatos de flujo de trabajo:** utilice la opción cuando el valor que se va a utilizar se guarde en una propiedad de metadatos de flujo de trabajo. Por ejemplo, emailAddress.
   * **Notación de punto JSON:** utilice la opción cuando el valor que se va a utilizar esté en un archivo JSON. Por ejemplo, seguro.customerDetails.emailAddress. La opción Anotación de punto JSON solo está disponible si está seleccionada la opción Asignar campos de entrada de la opción JSON de entrada.
   * **Asignar campos de entrada desde JSON de entrada:** especifique la ruta de un archivo JSON para obtener el valor de entrada de algunos argumentos de servicio del archivo JSON. La ruta del archivo JSON puede ser relativa a la carga útil, una ruta absoluta o puede seleccionar un documento JSON de entrada mediante una variable de tipo JSON o Modelo de datos de formulario.

* **Entrada para servicios > Proporcionar datos de entrada mediante una variable o un archivo JSON:** seleccione la opción para obtener valores para todos los argumentos de un archivo JSON guardado en una ruta absoluta, en una ruta relativa a la carga útil o en una variable.
* **Seleccione el documento de entrada JSON mediante**: El archivo JSON que contiene valores para todos los argumentos de servicio. La ruta del archivo JSON puede ser **relativa a la carga útil** o una **ruta absoluta.** También puede recuperar el documento JSON de entrada mediante una variable de tipo de datos JSON o del Modelo de datos de formulario.

* **Notación de punto JSON:** deje el campo en blanco para utilizar todos los objetos del archivo JSON especificado como entrada para argumentos de servicio. Para leer un objeto JSON específico del archivo JSON especificado como entrada para argumentos de servicio, especifique la notación de puntos para el objeto JSON; por ejemplo, si tiene un JSON similar al que aparece en el inicio de la sección, especifique seguro.customerDetails para proporcionar todos los detalles de un cliente como entrada al servicio.
* **Salida de servicio > Asignar y escribir valores de salida en variables o metadatos:** seleccione la opción para guardar los valores de salida como propiedades del nodo de metadatos de instancia de flujo de trabajo en crx-repository. Especifique el nombre de la propiedad metadata y seleccione el atributo de salida de servicio correspondiente que se va a asignar con la propiedad metadata; por ejemplo, asigne el número_teléfono devuelto por el servicio de salida con la propiedad phone_number de los metadatos del flujo de trabajo. Del mismo modo, puede almacenar el resultado en una variable de tipo de datos Long.Cuando selecciona una propiedad para la opción **[!UICONTROL Service output attribute que se va a asignar]**, solo se rellenan las variables capaces de almacenar datos de la propiedad seleccionada para la opción **[!UICONTROL Guardar el resultado en]**.

* **Salida de servicio > Guardar salida en variable o un archivo JSON:** seleccione la opción para guardar los valores de salida en un archivo JSON en una ruta absoluta, en una ruta relativa a la carga útil o en una variable.
* **Guarde el documento JSON de salida con las siguientes opciones:** Guarde el archivo JSON de salida. La ruta del archivo JSON de salida puede ser relativa a la carga útil o a una ruta absoluta. También puede guardar el archivo JSON de salida con una variable de tipo de datos JSON o del Modelo de datos de formulario.

## Firmar paso de Documento {#sign-document-step}

El paso Firmar Documento le permite utilizar Adobe Sign para firmar documentos. El paso Firmar Documento tiene las siguientes propiedades:

* **Nombre del acuerdo:** especifique el título del acuerdo. El nombre del acuerdo pasa a formar parte del asunto y del texto principal del correo electrónico enviado a los firmantes. Puede almacenar el nombre en una variable de tipo de datos String o seleccionar **Literal** para agregar el nombre manualmente.

* **Configuración regional:** especifique el idioma para las opciones de correo electrónico y verificación. Puede almacenar la configuración regional en una variable de tipo de datos String o seleccionar **Literal** para elegir la configuración regional de la lista de opciones disponibles. Debe definir el código de configuración regional mientras almacena el valor de la configuración regional en una variable. Por ejemplo, especifique **es_ES** para inglés y **fr_FR** para francés.

* **Configuración** de Adobe Sign Cloud: Elija una configuración de Adobe Sign Cloud. Si no ha configurado Adobe Sign para AEM Forms, consulte [Integración de Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

* **Seleccionar Documento para firmar:** Puede elegir un documento de una ubicación relativa a la carga útil, utilizar la carga útil como documento, especificar una ruta absoluta del documento o recuperar el documento almacenado en una variable de tipo de datos de Documento.
* **Días hasta la fecha límite:** un documento se marca con vencimiento (fecha límite superada) después de que no haya actividad en la tarea del número de días especificado en el campo  **Días hasta la** fecha límite. El número de días se contabiliza después de que el documento se asigne a un usuario para firmar.
* **Frecuencia de correo electrónico del recordatorio:** puede enviar un mensaje de correo electrónico de recordatorio a intervalos diarios o semanales. La semana se cuenta a partir del día en que se asigna el documento a un usuario para firmar.
* **Proceso de firma:** puede firmar un documento en un orden secuencial o paralelo. En orden secuencial, un firmante recibe el documento por vez para firmar. Una vez que el primer firmante haya terminado de firmar el documento, el documento se enviará al segundo firmante, etc. En orden paralelo, varios firmantes pueden firmar un documento a la vez.
* **URL de redirección:** especifique una URL de redirección. Una vez firmado el documento, puede redirigir al usuario asignado a una dirección URL. Normalmente, esta dirección URL contiene un mensaje de agradecimiento o instrucciones adicionales.
* **Etapa de flujo de trabajo:** un flujo de trabajo puede tener varias etapas. Estas etapas se muestran en la Bandeja de entrada AEM. Puede definir estas etapas en las propiedades del modelo (barra de tareas > Página > Propiedades de la página > Fases).
* **Seleccionar firmantes:** especifique el método para elegir firmantes para el documento. Puede asignar dinámicamente el flujo de trabajo a un usuario o grupo, o bien agregar manualmente los detalles de un firmante.
* **Secuencia de comandos o servicio para seleccionar firmantes:** la opción solo está disponible si la opción Dinámicamente está seleccionada en el campo Seleccionar firmantes. Puede especificar un ECMAScript o un servicio para elegir los firmantes y las opciones de verificación de un documento.
* **Detalles del firmante:** la opción solo está disponible si se ha seleccionado la opción Manualmente en el campo Seleccionar firmantes. Especifique la dirección de correo electrónico y elija un mecanismo de verificación opcional. Antes de seleccionar un mecanismo de verificación de 2 pasos, asegúrese de que la opción de verificación correspondiente está activada para la cuenta de Adobe Sign configurada. Puede utilizar una variable de tipo de datos String para definir los valores de los campos **[!UICONTROL Correo electrónico]**, **[!UICONTROL Código de país]** y **[!UICONTROL Número de teléfono]**. Los campos **[!UICONTROL Código de país]** y **[!UICONTROL Número de teléfono]** sólo se muestran si selecciona **[!UICONTROL Verificación por teléfono]** en la lista desplegable **[!UICONTROL Verificación de 2 pasos]**.
* **Variable de estado:** Un documento habilitado para Adobe Sign almacena el estado de firma del documento en una variable de tipo de datos String. Especifique el nombre de la variable de estado (adobeSignStatus). Hay una variable de estado de una instancia disponible en CRXDE en /etc/workflow/instance/&lt;server>/&lt;date-time>/&lt;instance of workflow model>/workItems/&lt;node>/metaData que contiene el estado de una variable.
* **Guardar documento firmado con las siguientes opciones:** especifique la ubicación en la que desea mantener los documentos firmados. Puede sobrescribir el archivo de carga útil, colocar el documento firmado en una ubicación dentro del directorio de carga útil o almacenar el documento firmado en una variable de tipo Documento.

## Pasos de documento Services {#document-services-steps}

AEM servicios de Documento son un conjunto de servicios para crear, montar y asegurar Documentos PDF. AEM Forms proporciona un paso AEM Flujo de trabajo independiente para cada servicio de documento.

De forma similar a otros pasos del flujo de trabajo de AEM Forms, como Asignar Tarea, Enviar correo electrónico y Documento de firma, puede utilizar variables en todos los pasos de los servicios de Documento AEM. Para obtener más información sobre cómo crear y administrar variables, consulte [Variables en flujos de trabajo de AEM](../../forms/using/variable-in-aem-workflows.md).

### Aplicar marca de hora de Documento paso {#apply-document-time-stamp-step}

Añada la marca de hora en un documento. Puede proporcionar detalles de documento, como ruta de documento de entrada, nombre del documento de entrada y ubicación para almacenar los datos exportados. Puede elegir sobrescribir el archivo de carga útil existente, elegir un nombre de archivo diferente para almacenar datos en un archivo diferente en la carpeta de carga útil, proporcionar una ruta absoluta a los datos o almacenar datos en una variable de tipo de datos de Documento.

### Convertir en paso de imagen {#convert-to-image-step}

Convierte un documento PDF en lista de imágenes. Los formatos de imagen admitidos son JPEG, JPEG2000, PNG y TIFF. La siguiente información se aplica a las conversiones a imágenes TIFF:

* Se genera un archivo TIFF de varias páginas.
* Algunas anotaciones no se incluyen en las imágenes TIFF. No se incluyen las anotaciones que requieren Acrobat para generar su apariencia.

### Convertir a PDF/A paso {#convert-to-pdf-a-step}

Convierte un documento PDF a formato PDF/A con las opciones proporcionadas. La versión PDF/A de Formato de Documento portátil (PDF) está especializada en archivar y preservar documentos a largo plazo.

### Convertir en paso de PS {#convert-to-ps-step}

Convertir documentos PDF a PostScript. Al convertir a PostScript, puede utilizar la operación de conversión para especificar el documento de origen y si desea convertir a PostScript nivel 2 o 3. El documento PDF que se convierte en un archivo PostScript debe ser no interactivo.

### Crear PDF a partir del paso de tipo especificado {#create-pdf-from-specified-type-step}

Genere un documento PDF a partir de un archivo de entrada. El documento de entrada puede ser relativo a la carga útil, tener una ruta absoluta, puede ser carga útil en sí mismo o almacenarse en una variable de tipo de datos de Documento.

### Crear archivos PDF desde URL/HTML/ZIP paso {#create-pdf-from-url-html-zip-step}

Genera un documento PDF a partir de la dirección URL, el HTML y el archivo ZIP proporcionados.

### Paso Exportar datos {#export-data-step}

Exporta datos de un archivo PDF forms o XDP. Requiere que introduzca la ruta de acceso de archivo del Documento de entrada y del formato de datos de exportación. Las opciones para Exportar formato de datos son Automático, XDP y XmlData.

### Export PDF al paso de tipo especificado {#export-pdf-to-specified-type-step}

Convierte un documento PDF a un formato seleccionado.

### Generar paso de PDF no interactivo {#generatenoninteractive}

Generar un PDF no interactivo. Proporciona varias opciones de personalización.

>[!NOTE]
>
>Puede utilizar variables para especificar el archivo de plantilla para los documentos de entrada. Almacene la ruta del archivo de plantilla en una variable del tipo de datos String.

### Paso Importar datos {#import-data-step}

Combina datos de formulario en un formulario PDF. Puede importar datos de formulario en un formulario PDF.

### Invocar paso DDX {#invokeddx}

Ejecuta el archivo DDX en el mapa especificado de documentos de entrada y devuelve los documentos PDF manipulados.

>[!NOTE]
>
>Puede utilizar variables para especificar el archivo DDX para documentos de entrada. Almacene el archivo DDX en una variable de tipo de datos Documento o XML.

### Paso del Optimize PDF {#optimize-pdf-step}

Optimiza los archivos PDF reduciendo su tamaño. El resultado de esta conversión son archivos PDF que pueden ser menores que sus versiones originales. Esta operación también convierte documentos PDF a la versión PDF especificada en los parámetros de optimización.

La configuración de optimización especifica cómo se optimizan los archivos. A continuación se muestran los ajustes de ejemplo:

* Versión de destinatario PDF
* Descartar objetos como acciones de JavaScript y miniaturas de página incrustadas
* Descartar datos de usuario, como comentarios y archivos adjuntos
* Descartar configuración no válida o no utilizada
* Compresión de datos sin comprimir o uso de algoritmos de compresión más eficientes
* Eliminación de fuentes incrustadas
* Configuración de los valores de transparencia

### Paso de formulario PDF de procesamiento {#renderpdf}

Procesa un formulario creado en el Diseñador de formularios (XDP) en un formulario PDF.

>[!NOTE]
>
>Puede utilizar variables para especificar el archivo de plantilla para los documentos de entrada. Almacene la ruta del archivo de plantilla en una variable del tipo de datos String.

### Paso de Documento seguro {#secure-document-step}

Codificar, firmar y certificar un documento. AEM Forms admite el cifrado basado en contraseña y en certificado. También puede elegir entre varios algoritmos para firmar documentos. Por ejemplo, SHA-256 y SH-512. También puede utilizar el paso del flujo de trabajo para que el lector pueda ampliar los documentos PDF. El paso del flujo de trabajo proporciona una opción para habilitar la descodificación de códigos de barras, las firmas digitales, la importación y exportación de datos PDF y otras opciones.

### Enviar a la impresora paso {#send-to-printer-step}

Enviar un documento directamente a una impresora. Admite los siguientes mecanismos de acceso a la impresión:

* **Impresora** accesible directa: Una impresora instalada en el mismo equipo se denomina impresora directa accesible y el equipo se denomina host de impresora. Este tipo de impresora puede ser una impresora local que esté conectada directamente al equipo.
* **Impresora** accesible indirecta: A la impresora instalada en un servidor de impresión se accede desde otros equipos. Tecnologías como el sistema de impresión UNIX® (CUPS) común y el protocolo Line Printer Daemon (LPD) están disponibles para conectarse a una impresora en red. Para obtener acceso a una impresora accesible indirecta, especifique la dirección IP o el nombre de host del servidor de impresión. Con este mecanismo, puede enviar un documento a un URI LPD cuando la red tenga un LPD en ejecución. Este mecanismo le permite enrutar el documento a cualquier impresora conectada a la red que tenga un LPD en ejecución.

### Generar paso de salida impresa {#generatePrintedOutput}

El paso genera una salida PCL, PostScript, ZPL, IPL, TPCL o DPL con un diseño de formulario y un archivo de datos. El archivo de datos se combina con el diseño de formulario y se le da formato para imprimirlo. La salida generada por este paso se puede enviar directamente a una impresora o guardar como archivo. Se recomienda que utilice este paso cuando desee utilizar diseños de formulario o datos de una aplicación. Si los diseños de formulario o los diseños de formulario se encuentran en la red, el sistema de archivos local o la ubicación HTTP, utilice la operación generatePrintedOutput.

Por ejemplo, la aplicación requiere que combine un diseño de formulario con un archivo de datos. Los datos contienen cientos de registros. Además, requiere que la salida se envíe a una impresora compatible con ZPL. El diseño de formulario y los datos de entrada se encuentran en una aplicación. Utilice la operación generatePrintedOutput para combinar cada registro con un diseño de formulario y enviar el resultado a una impresora compatible con ZPL.

El paso Generar salida impresa tiene las siguientes propiedades:

**Propiedades de entrada**

* **[!UICONTROL Seleccione el archivo de plantilla mediante]**: Especifique la ruta del archivo de plantilla. Puede seleccionar el archivo de plantilla utilizando la ruta relativa a la carga útil, guardada en una ruta absoluta o utilizando una variable de tipo de datos de Documento. Por ejemplo, [Directorio_de_carga]/Workflow/data.xml. Si la ruta no existe en crx-repository, un administrador puede crear la ruta antes de utilizarla. Además, también puede aceptar la carga útil como archivo de datos de entrada.

* **[!UICONTROL Seleccione el documento de datos mediante]**: Especifique la ruta de un archivo de datos de entrada. Puede seleccionar el archivo de datos de entrada utilizando la ruta relativa a la carga útil, guardada en una ruta absoluta o utilizando una variable de tipo de datos de Documento. Por ejemplo, [Directorio_de_carga]/Workflow/data.xml. Si la ruta no existe en crx-repository, un administrador puede crear la ruta antes de utilizarla.

* **[!UICONTROL Formato]** de impresora: Un valor de Formato de impresión que especifica el lenguaje de descripción de página que se utilizará, cuando no se proporcione un archivo XDC, para generar el flujo de salida. Si proporciona un valor literal, seleccione uno de estos valores:

   * **[!UICONTROL PCL]** personalizado: Utilice la opción para especificar un archivo XDC personalizado para PCL.
   * **[!UICONTROL PostScript]** personalizado: Utilice la opción para especificar un archivo XDC personalizado para PostScript.
   * **[!UICONTROL ZPL]** personalizado: Utilice la opción para especificar un archivo XDC personalizado para ZPL.
   * **[!UICONTROL Generic Color PCL (5c)]**: Utilice un PCL de color genérico (5c).
   * **[!UICONTROL PostScript genérico Level3]**: Utilice PostScript Level 3 genérico.
   * **[!UICONTROL ZPL 300 PPP]**: Utilice ZPL 300 PPP. Se utiliza zpl300.xdc.
   * **[!UICONTROL ZPL 600 PPP]**: Utilice ZPL 600 PPP. Se utiliza el archivo zpl600.xdc.
   * **[!UICONTROL IPL]** personalizado: Utilice la opción para especificar un archivo XDC personalizado para IPL.
   * **[!UICONTROL IPL 300 PPP]**: Utilice IPL 300 PPP. Se utiliza ipl300.xdc.
   * **[!UICONTROL IPL 400 PPP]**: Utilice IPL 400 PPP. Se utiliza el archivo ipl400.xdc.
   * **[!UICONTROL TPCL]** personalizado: Utilice la opción para especificar un archivo XDC personalizado para TPCL.
   * **[!UICONTROL TPCL 305 PPP]**: Utilice TPCL 300 PPP. Se utiliza el archivo tpcl305.xdc.
   * **[!UICONTROL PCL 600 PPP]**: Utilice TPCL 600 PPP. Se utiliza el archivo tpcl600.xdc.
   * **[!UICONTROL DPL]** personalizado: Utilice la opción para especificar un archivo XDC DPL personalizado.
   * **[!UICONTROL DPL300DPI]**: Utilice DPL 300 PPP. Se utiliza el archivo dpl300.xdc.
   * **[!UICONTROL DPL406PPP]**: Utilice DPL 400 PPP. Se utiliza dpl406.xdc.
   * **[!UICONTROL DPL600PPP]**: Utilice DPL 600 PPP. Se utiliza dpl600.xdc.

**Propiedades de salida**

* **[!UICONTROL Guardar documento de salida mediante]**: Especifique la ubicación en la que desea guardar el archivo de salida. Puede guardar el archivo de salida en una ubicación relativa a la carga útil, en una variable, o especificar una ubicación absoluta para guardar el archivo de salida. Si la ruta no existe en crx-repository, un administrador puede crear la ruta antes de utilizarla.

**Propiedades avanzadas**

* **[!UICONTROL Seleccione la ubicación de la raíz del contenido mediante]**: La raíz del contenido es un valor de cadena que especifica el URI, la referencia absoluta o la ubicación en el repositorio para recuperar los recursos relativos utilizados por el diseño de formulario. Por ejemplo, si el diseño de formulario hace referencia a una imagen de forma relativa, como ../myImage.gif, myImage.gif debe encontrarse en repository://. El valor predeterminado es repository://, que apunta al nivel raíz del repositorio.

   Al elegir un recurso de la aplicación, la ruta URI de raíz del contenido debe tener la estructura correcta. Por ejemplo, si se selecciona un formulario de una aplicación denominada SampleApp y se coloca en SampleApp/1.0/forms/Test.xdp, el URI de raíz del contenido debe especificarse como repository://administrator@password/Applications/SampleApp/1.0/forms/ o repositorio:/Applications/SampleApp/1.0/forms/ (cuando la autoridad es nula). Cuando se especifica el URI de raíz de contenido de esta manera, las rutas de todos los recursos a los que se hace referencia en el formulario se resuelven con este URI.

* **[!UICONTROL Seleccione el archivo XCI mediante]**: Los archivos XCI se utilizan para describir fuentes y otras propiedades que se utilizan para los elementos de diseño de formulario. Puede mantener un archivo XCI relativo a la carga útil, en una ruta absoluta o utilizando una variable de tipo de datos de Documento.

* **[!UICONTROL Configuración regional]**: Especifica el idioma utilizado para generar el documento PDF. Si proporciona un valor literal, seleccione un idioma en la lista o seleccione uno de estos valores:
   * **Para utilizar el servidor predeterminado**: (Predeterminado) Utilice la configuración regional configurada en el servidor de AEM Forms. La configuración regional se configura con la Consola de administración. (Consulte [Ayuda de Designer](http://www.adobe.com/go/learn_aemforms_designer_65).)

   * **Para utilizar un valor** personalizado: Escriba el código de configuración regional en el cuadro literal o seleccione una variable de cadena que contenga el código de configuración regional. Para obtener una lista completa de los códigos de configuración regional admitidos, consulte http://java.sun.com/j2se/1.5.0/docs/guide/intl/locale.doc.html.

* **[!UICONTROL Copias]**: Un valor entero que especifica el número de copias que se van a generar para la salida. El valor predeterminado es 1.

* **[!UICONTROL Impresión]** a doble cara: Un valor de Paginación que especifica si se utiliza la impresión a doble cara o a una sola cara. Las impresoras que admiten PostScript y PCL utilizan este valor.Si proporciona un valor literal, seleccione uno de estos valores:
   * **[!UICONTROL Borde]** largo dúplex: Utilice la impresión a doble cara y la impresión mediante paginación de borde largo.
   * **[!UICONTROL Borde]** corto dúplex: Utilice la impresión a doble cara y la impresión mediante paginación de borde corto.
   * **[!UICONTROL Simple]**: Utilice la impresión a una sola cara.