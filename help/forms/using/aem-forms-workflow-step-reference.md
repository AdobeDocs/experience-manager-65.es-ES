---
title: 'Flujo de trabajo centrado en Forms en OSGi: referencia de los pasos'
seo-title: 'Flujo de trabajo centrado en Forms en OSGi: referencia de los pasos'
description: El flujo de trabajo centrado en Forms en los pasos de OSGi le permite crear rápidamente flujos de trabajo basados en formularios adaptables.
seo-description: El flujo de trabajo centrado en Forms en los pasos de OSGi le permite crear rápidamente flujos de trabajo basados en formularios adaptables.
uuid: 6f791c45-0e35-4c55-9106-5340caab94b7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: f0a5588d-f210-4f04-bc35-b62834f90ab1
docset: aem65
exl-id: 470fcfda-dfde-437c-b539-d5af1e13a7d6
source-git-commit: aaafda59c63ea47c67ec974263013ead468df9cc
workflow-type: tm+mt
source-wordcount: '7268'
ht-degree: 0%

---

# Flujo de trabajo centrado en Forms en OSGi: referencia de los pasos{#forms-centric-workflow-on-osgi-step-reference}

## Pasos del Forms Workflow {#forms-workflow-steps}

Los pasos del flujo de trabajo de Forms realizan operaciones específicas de AEM Forms en un flujo de trabajo AEM. Estos pasos le permiten crear rápidamente formularios adaptables basados en un flujo de trabajo centrado en Forms en OSGi. Estos flujos de trabajo se pueden utilizar para desarrollar flujos de trabajo básicos de revisión y aprobación, procesos empresariales internos y entre cortafuegos. También puede utilizar los pasos del Forms Workflow para iniciar document services, integrar con el flujo de trabajo de firma de Adobe Sign y realizar otras operaciones de AEM Forms. Debe [AEM Forms add-on](https://www.adobe.com/go/learn_aemforms_documentation_63) para utilizar estos pasos en un flujo de trabajo.

## Asignar paso de tarea {#assign-task-step}

El paso asignar tarea crea una tarea y la asigna a un usuario o grupo. Junto con asignar la tarea, el componente también especifica el formulario adaptable o el PDF no interactivo para la tarea. El formulario adaptable es necesario para aceptar datos introducidos por los usuarios, y el PDF no interactivo o un formulario adaptable de solo lectura se utiliza para revisar solo flujos de trabajo.

También puede utilizar el componente para controlar el comportamiento de la tarea. Por ejemplo, crear un documento de registro automático, asignar la tarea a un usuario o grupo específico, especificar la ruta de los datos enviados, especificar la ruta de los datos que se van a rellenar previamente y especificar las acciones predeterminadas. El paso Asignar tarea tiene las siguientes propiedades:

* **Título:** Título de la tarea. El título se muestra en AEM Bandeja de entrada.
* **Descripción:** Explicación de las operaciones que se realizan en la tarea. Esta información resulta útil para otros desarrolladores de procesos cuando trabaja en un entorno de desarrollo compartido.

* **Ruta de vista en miniatura:** Ruta de la miniatura de la tarea. Si no se especifica ninguna ruta, se muestra la miniatura predeterminada de un formulario adaptable y, para el Documento de registro, se muestra un icono predeterminado.
* **Etapa de flujo de trabajo:** un flujo de trabajo puede tener varias etapas. Estas etapas se muestran en la Bandeja de entrada AEM. Puede definir estas etapas en las propiedades del modelo (Barra de tareas > Página > Propiedades de la página > Etapas).
* **Prioridad:** la prioridad seleccionada se muestra en la Bandeja de entrada de AEM. Las opciones disponibles son Alto, Medio y Bajo. El valor predeterminado es Medio.
* **Fecha de vencimiento:** especifique el número de días u horas después de los cuales se marca la tarea con retraso. Si selecciona **Off**, la tarea nunca se marca como pendiente. También puede especificar un controlador de tiempo de espera para realizar tareas específicas después de que la tarea haya caducado.

* **Días:** el número de días antes de que se complete la tarea. El número de días se cuenta después de que la tarea se asigne a un usuario. Si una tarea no está completa y sobrepasa el número de días especificado en el campo Días, si se selecciona, se activa un controlador de tiempo de espera después de la fecha de vencimiento.
* **Horas:** el número de horas antes de las cuales se completará la tarea. El número de horas se cuenta después de que la tarea se asigne a un usuario. Si una tarea no está completa y sobrepasa el número de horas especificado en el campo Horas , si se selecciona, se activa un controlador de tiempo de espera después de las horas de vencimiento.
* **Tiempo de espera después de la fecha de vencimiento:** seleccione esta opción para habilitar el campo de selección Controlador de tiempo de espera.
* **Controlador de tiempo de espera:** seleccione la secuencia de comandos que se ejecutará cuando el paso asignar tarea supere la fecha de vencimiento. Los scripts colocados en el repositorio CRX en [apps]/fd/dashboard/scripts/timeoutHandler están disponibles para su selección. La ruta especificada no existe en el repositorio crx. Un administrador crea la ruta antes de utilizarla.
* **Resalte la acción y el comentario de la última tarea en Detalles de la tarea:** seleccione esta opción para mostrar la última acción realizada y el comentario recibido en la sección de detalles de la tarea de una tarea.
* **Tipo:** elija el tipo de documento que se rellenará al iniciar el flujo de trabajo. Puede elegir un formulario adaptable, un formulario adaptable de solo lectura, un documento PDF no interactivo, una interfaz de usuario del Agente de comunicación interactiva o un documento del canal web de comunicación interactiva.
* **Utilizar formulario adaptable:** especifique el método para localizar el formulario adaptable de entrada. Esta opción está disponible si selecciona Formulario adaptable o Formulario adaptable de solo lectura en la lista desplegable Tipo . Puede utilizar el formulario adaptable enviado al flujo de trabajo, disponible en una ruta absoluta o disponible en una ruta en una variable. Puede utilizar una variable de tipo String para especificar la ruta.\
   Puede asociar varios formularios adaptables a un flujo de trabajo. Como resultado, se puede especificar un formulario adaptable en tiempo de ejecución mediante los métodos de entrada disponibles.

* **Utilizar comunicación interactiva:** especifique el método para localizar la comunicación interactiva de entrada. Puede utilizar la comunicación interactiva enviada al flujo de trabajo, disponible en una ruta absoluta o disponible en una ruta en una variable. Puede utilizar una variable de tipo String para especificar la ruta. Esta opción está disponible si selecciona la interfaz de usuario del Agente de comunicación interactiva o el documento del canal web de comunicación interactiva en la lista desplegable Tipo .

>[!NOTE]
>
>Debe tener asignaciones de cm-agent-users y de grupo de flujo de trabajo-usuarios para acceder a la interfaz de usuario de Interactive Communications Agent en AEM bandeja de entrada.

* **Formulario adaptable o ruta de comunicación interactiva**: Especifique la ruta del formulario adaptable o la comunicación interactiva. Puede utilizar el formulario adaptable o la comunicación interactiva que se envía al flujo de trabajo, que está disponible en una ruta absoluta, o recuperar el formulario adaptable de una ruta almacenada en una variable de tipo de datos de cadena.
* **Seleccionar PDF de entrada mediante:** especifique la ruta de un documento PDF no interactivo. El campo está disponible cuando se elige un documento PDF no interactivo en el campo Tipo. Puede seleccionar el PDF de entrada utilizando la ruta relativa a la carga útil, guardada en una ruta absoluta o utilizando una variable del tipo de datos Document . Por ejemplo, [Payload_Directory]/Workflow/PDF/credit-card.pdf. La ruta no existe en el repositorio crx. Un administrador crea la ruta antes de utilizarla. Se necesita una opción Documento de registro activada o formularios adaptables basados en plantillas de formulario para utilizar la opción Ruta de PDF.
* **Para las tareas completadas, renderice el formulario adaptable como**: Cuando se marca una tarea como completada, puede procesar el formulario adaptable como un formulario adaptable de solo lectura o como un documento PDF. Se necesita una opción Documento de registro activada o formularios adaptables basados en plantillas de formulario para procesar el formulario adaptable como Documento de registro.
* **Rellenado previamente:**  Los campos siguientes enumerados a continuación sirven como entradas para la tarea:

   * **Seleccione el archivo de datos de entrada mediante:** Ruta del archivo de datos de entrada (.json,). xml, .doc o modelo de datos de formulario). Puede recuperar el archivo de datos de entrada mediante una ruta relativa a la carga útil o recuperar el archivo almacenado en una variable de tipo de datos Document, XML o JSON. Por ejemplo, el archivo contiene los datos enviados para el formulario a través de una aplicación Bandeja de entrada AEM. Una ruta de ejemplo es [Payload_Directory]/workflow/data.
   * **Seleccione los archivos adjuntos de entrada mediante:**  Los archivos adjuntos disponibles en la ubicación se adjuntan al formulario asociado a la tarea. La ruta siempre es relativa a la carga útil. Una ruta de ejemplo es [Payload_Directory]/attachment/
   * **Elegir JSON de entrada:** seleccione un archivo JSON de entrada utilizando una ruta relativa a la carga útil o almacenada en una variable del tipo de datos Document, JSON o Form Data Model. Esta opción está disponible si selecciona la interfaz de usuario del Agente de comunicación interactiva o el documento del canal web de comunicación interactiva en la lista desplegable Tipo .
   * **Elija un servicio de relleno previo personalizado:** seleccione el servicio de rellenado previo para recuperar los datos y cumplimente previamente el documento del canal web de comunicación interactiva o la interfaz del agente.

   * **Utilice el servicio de rellenado previo de la comunicación interactiva seleccionada arriba:** Utilice esta opción para utilizar el servicio de rellenado previo de la comunicación interactiva definida en la lista desplegable Usar comunicación interactiva.
   * **Asignación de atributos de solicitud:** utilice la sección Asignación de atributos de solicitud para definir el  [nombre y el valor del atributo de solicitud](../../forms/using/work-with-form-data-model.md#bindargument). Recupere los detalles de la fuente de datos en función del nombre del atributo y el valor especificados en la solicitud. Puede definir un valor de atributo de solicitud utilizando un valor literal o una variable del tipo de datos String .\
      Las opciones de asignación de atributos de solicitud y servicio de prellenado solo están disponibles si selecciona la interfaz de usuario del Agente de comunicación interactiva o el documento de canal web de comunicación interactiva en la lista desplegable Tipo .

* **Información enviada:**  Los campos siguientes enumerados a continuación sirven como ubicaciones de salida para la tarea:

   * **Guarde el archivo de datos de salida usando:** Guarde el archivo de datos (.json,). xml, .doc o modelo de datos de formulario). El archivo de datos contiene información enviada a través del formulario asociado. Puede guardar el archivo de datos de salida utilizando una ruta relativa a la carga útil o almacenarla en una variable de tipo de datos Document, XML o JSON. Por ejemplo, [Payload_Directory]/Workflow/data, donde los datos son un archivo.
   * **Guardar archivos adjuntos mediante:** guarde los datos adjuntos del formulario que se proporcionan en una tarea. Puede guardar los archivos adjuntos utilizando una ruta relativa a la carga útil o almacenarla en una variable de matriz del tipo Document data .
   * **Guardar documento de registro mediante:** ruta para guardar un archivo de documento de registro. Por ejemplo, [Payload_Directory]/DocumentofRecord/credit-card.pdf. Puede guardar el documento de registro mediante una ruta relativa a la carga útil o almacenarlo en una variable del tipo de datos Document . Si selecciona la opción **Relative to Payload**, el documento de registro no se genera si el campo de ruta se deja vacío. Esta opción solo está disponible si selecciona Formulario adaptable en la lista desplegable Tipo .

   * **Guarde los datos del canal web mediante:** guarde el archivo de datos del canal web con una ruta relativa a la carga útil o almacénelo en una variable del tipo de datos Documento, JSON o Modelo de datos de formulario. Esta opción solo está disponible si selecciona la IU de Interactive Communication Agent en la lista desplegable Tipo .
   * **Guardar documento PDF con:** Guarde el documento PDF con una ruta relativa a la carga útil o guárdelo en una variable del tipo de datos Document. Esta opción solo está disponible si selecciona la IU de Interactive Communication Agent en la lista desplegable Tipo .
   * **Guarde la plantilla de diseño utilizando:** Guarde la plantilla de diseño utilizando una ruta relativa a la carga útil o guárdela en una variable del tipo de datos Document. La [plantilla de diseño](../../forms/using/layout-design-details.md) hace referencia a un archivo XDP que se crea con Forms Designer. Esta opción solo está disponible si selecciona la IU de Interactive Communication Agent en la lista desplegable Tipo .

* **Opciones de Asignación > Asignar:** especifique el método para asignar la tarea a un usuario. Puede asignar dinámicamente la tarea a un usuario o grupo mediante la secuencia de comandos del selector de participantes o asignar la tarea a un usuario o grupo AEM específico.
* **Selector de participante:** la opción está disponible cuando se selecciona la opción  **Dinámicamente a un usuario o** grupo en el campo Asignar opciones . Puede utilizar un ECMAScript o un servicio para seleccionar dinámicamente un usuario o un grupo. Para obtener más información, consulte [Asignación dinámica de un flujo de trabajo a los usuarios](https://helpx.adobe.com/experience-manager/kb/HowToAssignAWorkflowDynamicallyToParticipants.html) y [Creación de un paso de participante dinámico personalizado de Adobe Experience Manager.](https://helpx.adobe.com/experience-manager/using/dynamic-steps.html)

* **Participantes:** el campo está disponible cuando se selecciona la opción  **[!UICONTROL com.adobe.granite.workflow.core.process.]** RandomParticipantChooseren en el campo  **Selector** de participantes. El campo permite seleccionar usuarios o grupos para la opción RandomParticipantChooser .

* **Usuario asignado:** el campo está disponible cuando se selecciona  **[!UICONTROL com.adobe.fd.workspace.step.service.]** VariableParticipantChoosers en el campo  **Selector** de participante. El campo permite seleccionar una variable de tipo String data para definir el usuario asignado.

* **Argumentos:** El campo está disponible cuando se selecciona una secuencia de comandos distinta de la de RandomParticipantChoose en el campo Selector de participantes. El campo permite proporcionar una lista de argumentos separados por coma para la secuencia de comandos seleccionada en el campo Selector de participantes .

* **Usuario o Grupo:** la tarea se asigna al usuario o grupo seleccionado. La opción está disponible cuando la opción **To a specific user or group option** está seleccionada en el campo **Assign options**. El campo enumera todos los usuarios y grupos del grupo de usuarios del flujo de trabajo.\
   El menú desplegable **Usuario o Grupo** enumera los usuarios y grupos a los que el usuario que ha iniciado sesión tiene acceso. La visualización del nombre de usuario depende de si tiene permisos de acceso en el nodo **users** en el repositorio crx para ese usuario en particular.

* **[!UICONTROL Enviar correo electrónico]** de notificación: Seleccione esta opción para enviar notificaciones por correo electrónico al usuario asignado. Estas notificaciones se envían cuando se asigna una tarea a un usuario o a un grupo. Puede utilizar la opción **[!UICONTROL Recipient Email Address]** para especificar el mecanismo para recuperar la dirección de correo electrónico.

* **[!UICONTROL Dirección]** de correo electrónico del destinatario: Puede almacenar la dirección de correo electrónico en una variable, usar un literal para especificar una dirección de correo electrónico permanente o usar la dirección de correo electrónico predeterminada del usuario asignado especificada en el perfil del usuario asignado. Puede utilizar el literal o una variable para especificar la dirección de correo electrónico de un grupo. La opción de variable es útil para recuperar y utilizar dinámicamente una dirección de correo electrónico. La opción **[!UICONTROL Use default email address of the assignee]** solo es para un único usuario asignado. En este caso, se utiliza la dirección de correo electrónico almacenada en el perfil de usuario asignado.

* **Plantilla** de correo electrónico HTML: Seleccione la plantilla de correo electrónico para el correo electrónico de notificación. Para editar una plantilla, modifique el archivo ubicado en /libs/fd/dashboard/templates/email/htmlEmailTemplate.txt en el repositorio crx.
* **Permitir delegación en:** AEM bandeja de entrada proporciona una opción al usuario que ha iniciado sesión para delegar el flujo de trabajo asignado a otro usuario. Se le permite delegar dentro del mismo grupo o al usuario del flujo de trabajo de otro grupo. Si la tarea se asigna a un solo usuario y la opción **allow delegation to member of the assignee group** está seleccionada, no es posible delegar la tarea a otro usuario o grupo.
* **Compartir configuración:** AEM bandeja de entrada ofrece opciones para compartir una o todas las tareas de la bandeja de entrada con otros usuarios:
   * Cuando se selecciona la opción **Permitir que el usuario asignado comparta explícitamente en la bandeja de entrada**, el usuario puede hacer clic en la tarea y compartirla con otro usuario AEM.
   * Cuando se selecciona la opción **Permitir que el usuario asignado comparta mediante el uso compartido de la bandeja de entrada** y un usuario comparte los elementos de la bandeja de entrada o permite que otros usuarios accedan a los elementos de la bandeja de entrada, solo se comparten las tareas con la opción mencionada habilitada con otros usuarios.

* **Acciones > Acciones predeterminadas:** de forma predeterminada, las acciones Enviar, Guardar y Restablecer están disponibles. De forma predeterminada, todas las acciones predeterminadas están habilitadas.
* **Variable de ruta:** Nombre de la variable de ruta. La variable de ruta captura las acciones personalizadas que selecciona un usuario en AEM Bandeja de entrada.
* **Rutas:** una tarea puede ramificarse a diferentes rutas. Cuando se selecciona en AEM Bandeja de entrada, la ruta devuelve un valor y las ramas del flujo de trabajo se basan en la ruta seleccionada. Puede almacenar rutas en una variable de matriz del tipo de datos String o seleccionar **Literal** para agregar rutas manualmente.

* **Título**: Especifique el título de la ruta. Se muestra en AEM Bandeja de entrada.
* **Icono** de coral: Especifique el atributo HTML de un icono de coral. La biblioteca CorelUI de Adobe proporciona un amplio conjunto de iconos táctiles. Puede elegir y utilizar un icono para la ruta. Se muestra junto con el título en AEM Bandeja de entrada. Si almacena las rutas en una variable, las rutas utilizan un icono de coral predeterminado &quot;Etiquetas&quot;.
* **Permitir que el usuario asignado añada un comentario**: Seleccione esta opción para activar los comentarios en la tarea. Un usuario asignado puede agregar los comentarios desde AEM Bandeja de entrada en el momento del envío de la tarea.
* **Guarde el comentario en la variable:** guarde el comentario en una variable de tipo String data . Esta opción solo se muestra si selecciona la casilla **Permitir que el usuario asignado añada un comentario**.

* **Permitir que el usuario asignado añada archivos adjuntos a la tarea**: Seleccione esta opción para activar los archivos adjuntos en la tarea. Un usuario asignado puede añadir los archivos adjuntos desde AEM Bandeja de entrada en el momento del envío de la tarea.
* **Guardar archivos adjuntos de tareas de salida mediante**: Especifique la ubicación de la carpeta de archivos adjuntos. Puede guardar archivos adjuntos de tareas de salida utilizando una ruta relativa a la carga útil o en una variable de matriz de tipo de datos de documento. Esta opción solo se muestra si selecciona la casilla **Permitir que el usuario asignado añada archivos adjuntos a la tarea** y selecciona **Formulario adaptable**, **Formulario adaptable de solo lectura** o **Documento PDF no interactivo** en la lista desplegable **Tipo** Ficha **Formulario/Documento**.

>[!NOTE]
>
>Utilice la pestaña Attachments en la interfaz de usuario del agente durante el tiempo de ejecución para asociar los archivos adjuntos a una comunicación interactiva. Los archivos adjuntos asociados se muestran como archivos adjuntos de tarea en la barra de tareas después de abrir el elemento de trabajo en estado Complete .

* **Usar metadatos personalizados:** seleccione esta opción para habilitar el campo de metadatos personalizado. Los metadatos personalizados se utilizan en plantillas de correo electrónico.
* **Metadatos personalizados:** seleccione un metadatos personalizado para las plantillas de correo electrónico. Los metadatos personalizados están disponibles en crx-repository en apps/fd/dashboard/scripts/metadataScripts. La ruta especificada no existe en el repositorio crx. Un administrador crea la ruta antes de utilizarla. También puede utilizar un servicio para los metadatos personalizados. También puede ampliar la interfaz WorkitemUserMetadataService para proporcionar metadatos personalizados.
* **Mostrar datos de pasos** anteriores: Seleccione esta opción para permitir que los usuarios asignados vean los destinatarios anteriores, las acciones ya realizadas en la tarea, los comentarios añadidos a la tarea y el documento de registro de la tarea completada, si está disponible.
* **Mostrar datos de pasos subsiguientes:** seleccione esta opción para permitir que el usuario asignado actual vea la acción realizada y los comentarios agregados a la tarea por los usuarios asignados subsiguientes. También permite al usuario asignado actual ver un documento de registro de la tarea completada, si está disponible.
* **Visibilidad del tipo de datos:** de forma predeterminada, un usuario asignado puede ver un documento de registro, los usuarios asignados, las acciones realizadas y los comentarios que hayan añadido los usuarios asignados anteriores y posteriores. Utilice la opción visibility of data type para limitar el tipo de datos visibles para los usuarios asignados.

## Enviar paso de correo electrónico {#send-email-step}

Utilice el paso de correo electrónico para enviar un correo electrónico, por ejemplo un correo electrónico con un documento de registro, un vínculo de un formulario adaptable, un vínculo de una comunicación interactiva o un documento PDF adjunto. El paso Enviar correo electrónico admite [correo electrónico HTML](https://en.wikipedia.org/wiki/HTML_email). Los correos electrónicos HTML responden y se adaptan al cliente de correo electrónico y al tamaño de pantalla de los destinatarios. Puede utilizar una plantilla de correo electrónico HTML para definir el aspecto, el esquema de colores y el comportamiento del correo electrónico.

El paso de correo electrónico utiliza el servicio de correo de Day CQ para enviar correos electrónicos. Antes de utilizar el paso de correo electrónico, asegúrese de que el [servicio de correo electrónico](../../forms/using/aem-forms-workflow.md) está configurado. El paso de correo electrónico tiene las siguientes propiedades:

**Título:** El título del paso ayuda a identificar el paso en el editor de flujo de trabajo.

**Descripción:**  La explicación es útil para otros desarrolladores de procesos que estén trabajando en un entorno de desarrollo compartido.

**Asunto del correo electrónico:** el asunto se puede recuperar de los metadatos de un flujo de trabajo, especificarse manualmente o recuperarse del valor almacenado en una variable. Seleccione entre las siguientes opciones:

* **Literal:** especifique manualmente un asunto.
* **Recuperar de metadatos del flujo de trabajo** : recupere el asunto de una propiedad de metadatos.
* **Variable** : recupere el asunto del valor almacenado en una variable de tipo de datos de cadena.

**Plantilla** de correo electrónico HTML: Plantilla HTML para el correo electrónico. Puede especificar variables en una plantilla de correo electrónico. El paso Correo electrónico extrae y muestra todas las variables incluidas en una plantilla para las entradas.

**Metadatos de plantilla de correo electrónico:** El valor de las variables de plantilla de correo electrónico puede ser un valor especificado por el usuario, la ruta de un recurso en el autor o en el servidor de publicación, la imagen o una propiedad de metadatos de flujo de trabajo.

* **Literal:** utilice la opción cuando sepa el valor exacto que desea especificar. Por ejemplo, [example@example.com](mailto:example@example.com).

* **Metadatos del flujo de trabajo:** utilice la opción cuando el valor que se va a utilizar se guarde en una propiedad de metadatos del flujo de trabajo. Después de seleccionar la opción , introduzca el nombre de la propiedad de metadatos en el cuadro de texto vacío debajo de la opción Metadatos del flujo de trabajo . Por ejemplo, emailAddress.
* **URL del recurso:** utilice la opción para incrustar un vínculo web de una comunicación interactiva al correo electrónico. Después de seleccionar la opción , busque y elija la comunicación interactiva que desea incrustar. El recurso puede residir en el autor o en el servidor de publicación.
* **Imagen:** utilice la opción para incrustar una imagen en el correo electrónico. Después de seleccionar la opción , busque y elija la imagen. La opción de imagen solo está disponible para las etiquetas de imagen (&lt;img src=&quot;*&quot;/>) disponibles en la plantilla de correo electrónico.

**Dirección de correo electrónico del remitente/destinatario:** seleccione la opción  **** Literalpara especificar manualmente una dirección de correo electrónico o seleccione la opción  **Recuperar de** metadatos del flujo de trabajo para recuperar la dirección de correo electrónico de una propiedad de metadatos. También puede especificar una lista de matrices de propiedades de metadatos para la opción **Recuperar de metadatos del flujo de trabajo**. Seleccione la opción **Variable** para recuperar la dirección de correo electrónico del valor almacenado en una variable de tipo de datos de cadena.

**Archivo adjunto:** el recurso disponible en la ubicación especificada se adjunta al correo electrónico. La ruta del recurso puede ser relativa a la carga útil o a la ruta absoluta. Una ruta de ejemplo es [Payload_Directory]/attachment/.

Seleccione la opción **Variable** para recuperar el archivo adjunto almacenado en una variable de tipo de datos Document, XML o JSON.

**Nombre de archivo:** Nombre del archivo adjunto de correo electrónico. El paso Correo electrónico cambia el nombre de archivo original del archivo adjunto al nombre de archivo especificado. El nombre se puede especificar manualmente o recuperar desde una propiedad de metadatos de flujo de trabajo o una variable. Utilice la opción **Literal** cuando sepa el valor exacto que debe especificar. Utilice la opción **Variable** para recuperar el nombre de archivo del valor almacenado en una variable de tipo de datos de cadena. Utilice la opción **Retrieve from a Workflow Metadata** cuando el valor que se va a utilizar se guarde en una propiedad de metadatos del flujo de trabajo.

## Generar paso de documento de registro {#generate-document-of-record-step}

Cuando se rellena o se envía un formulario, se puede guardar un registro del formulario, en formato impreso o en formato de documento. Esto se denomina Documento de registro (DoR). Puede utilizar el paso Generar documento de registro para crear una versión PDF de solo lectura o interactiva de un formulario adaptable. La versión PDF contiene información rellenada en el formulario junto con la presentación del formulario adaptable.

El paso Documento de registro tiene las siguientes propiedades:

**Utilizar formulario** adaptable: Especifique el método para localizar el formulario adaptable de entrada. Puede utilizar el formulario adaptable enviado al flujo de trabajo, disponible en una ruta absoluta o disponible en una ruta en una variable. Puede utilizar una variable de tipo String data para especificar la ruta en el campo **Select variable to resolve**.\
Puede asociar varios formularios adaptables a un flujo de trabajo. Como resultado, se puede especificar un formulario adaptable en tiempo de ejecución mediante los métodos de entrada disponibles.

**Ruta de formulario adaptable**: Especifique la ruta del formulario adaptable. El campo está disponible cuando se selecciona la opción **Available at an Absolutive path** en el campo **Use Adaptive Form**.

**Seleccione Input data using:** Path of the input data for the adaptive form. Puede mantener los datos en una ubicación relativa a la carga útil, especificar una ruta absoluta de los datos o recuperar datos almacenados en una variable de tipo de datos Document, JSON o XML. Los datos de entrada se combinan con el formulario adaptable para crear un documento de registro.

**Seleccione Input attachment path mediante:** Path of the attachment. Estos archivos adjuntos se incluyen en el Documento de registro. Puede mantener los archivos adjuntos en una ubicación relativa a la carga útil, especificar una ruta absoluta de los archivos adjuntos o recuperar los archivos adjuntos almacenados en una variable de matriz del tipo Document data .

Si especifica la ruta de una carpeta, por ejemplo, los archivos adjuntos, todos los archivos disponibles directamente en la carpeta se adjuntan al documento de registro. Si hay archivos disponibles en las carpetas disponibles directamente en la ruta de datos de los archivos adjuntos especificada, los archivos se incluyen en el documento de registro como archivos adjuntos. Si hay carpetas en carpetas disponibles directamente, se omiten.

**Guardar documento de registro generado usando las siguientes opciones:** especifique la ubicación para guardar un archivo de documento de registro. Puede sobrescribir la carpeta de carga útil, colocar el documento de registro en una ubicación del directorio de carga útil o almacenar el documento de registro en una variable del tipo Document data .

**Configuración regional**: Especifique el idioma del documento de registro. Seleccione **Literal** para seleccionar la configuración regional de una lista desplegable o seleccione **Variable** para recuperar la configuración regional del valor almacenado en una variable de tipo de datos de cadena. Debe definir el código de configuración regional mientras almacena el valor de la configuración regional en una variable. Por ejemplo, especifique **en_US** para inglés y **fr_FR** para francés.

## Invocar el paso del servicio del modelo de datos de formulario {#invoke-form-data-model-service-step}

Puede utilizar [AEM Forms Data Integration](../../forms/using/data-integration.md) para configurar y conectar con fuentes de datos diferentes. Estas fuentes de datos pueden ser una base de datos, un servicio web, un servicio REST, un servicio OData y una solución CRM. La integración de datos de AEM Forms le permite crear un modelo de datos de formulario que incluya varios servicios para realizar operaciones de recuperación, adición y actualización de datos en la base de datos configurada. Puede utilizar el paso **Invocar servicio de modelo de datos** para seleccionar un modelo de datos de formulario (FDM) y utilizar los servicios de FDM para recuperar, actualizar o agregar datos a orígenes de datos dispares.

Para explicar las entradas de los campos del paso , se utilizan como ejemplo la siguiente tabla de base de datos y el archivo JSON :

**Tabla de detalles del cliente de muestra**

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
   <td>Rose</td> 
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
* **Descripción:** Explicación útil para otros desarrolladores de procesos que estén trabajando en un entorno de desarrollo compartido.

* **Ruta del modelo de datos del formulario**: Busque y seleccione un modelo de datos de formulario presente en el servidor.

* **Servicio**: Lista de los servicios que proporciona el modelo de datos de formulario seleccionado.
* **Entrada para servicios > Proporcionar datos de entrada utilizando metadatos literales, variables o de flujo de trabajo, y un archivo** JSON: Un servicio puede tener varios argumentos. Seleccione la opción para obtener el valor de los argumentos de servicio de una propiedad de metadatos de flujo de trabajo, un objeto JSON o una variable, o introduzca directamente el valor en el cuadro de texto proporcionado:

   * **Literal:** utilice la opción cuando sepa el valor exacto que desea especificar. Por ejemplo, srose@we.info.
   * **Variable:** utilice la opción para recuperar el valor almacenado en una variable.
   * **Recuperar de metadatos del flujo de trabajo:** utilice la opción cuando el valor que se va a utilizar se guarde en una propiedad de metadatos del flujo de trabajo. Por ejemplo, emailAddress.
   * **[!UICONTROL Relativo a la carga útil]**: Utilice la opción para recuperar el archivo adjunto guardado en una ruta relativa a la carga útil. Seleccione la opción y especifique el nombre de la carpeta que incluye el archivo adjunto o especifique el nombre del archivo adjunto en el cuadro de texto.

      Por ejemplo, si la carpeta Relative to Payload del repositorio CRX incluye un archivo adjunto en la ubicación `attachment\attachment-folder` , especifique `attachment\attachment-folder` en el cuadro de texto después de seleccionar la opción **[!UICONTROL Relative to Payload]** .
   * **Notación de puntos JSON:** utilice la opción cuando el valor que va a utilizar esté en un archivo JSON. Por ejemplo, insurance.customerDetails.emailAddress. La opción Anotación de puntos JSON solo está disponible si está seleccionada la opción Asignar campos de entrada de JSON de entrada .
   * **Asignar campos de entrada del JSON de entrada:** especifique la ruta de un archivo JSON para obtener el valor de entrada de algunos argumentos de servicio del archivo JSON. La ruta del archivo JSON puede ser relativa a la carga útil, una ruta absoluta o puede seleccionar un documento JSON de entrada utilizando una variable de tipo JSON o Modelo de datos de formulario.

* **Entrada para servicios > Proporcionar datos de entrada mediante una variable o un archivo JSON:** seleccione la opción para obtener valores para todos los argumentos de un archivo JSON guardado en una ruta absoluta, en una ruta relativa a la carga útil o en una variable.
* **Seleccione el documento JSON de entrada mediante**: El archivo JSON que contiene valores para todos los argumentos de servicio. La ruta del archivo JSON puede ser **relativa a la carga útil** o una **ruta absoluta.** También puede recuperar el documento JSON de entrada utilizando una variable de tipo de datos JSON o del Modelo de datos de formulario.

* **Notación de puntos JSON:** deje el campo en blanco para utilizar todos los objetos del archivo JSON especificado como entrada para argumentos de servicio. Para leer un objeto JSON específico del archivo JSON especificado como entrada para argumentos de servicio, especifique la notación de puntos para el objeto JSON, por ejemplo, si tiene un JSON similar al que aparece al principio de la sección, especifique insurance.customerDetails para proporcionar todos los detalles de un cliente como entrada al servicio.
* **Salida de servicio > Asignar y escribir valores de salida en variables o metadatos:**  seleccione la opción para guardar los valores de salida como propiedades del nodo de metadatos de instancia de flujo de trabajo en el repositorio crx. Especifique el nombre de la propiedad metadata y seleccione el atributo de salida de servicio correspondiente que se va a asignar con la propiedad metadata, por ejemplo, asigne el phone_number devuelto por el servicio de salida con la propiedad phone_number de los metadatos del flujo de trabajo. Del mismo modo, se puede almacenar el resultado en una variable de tipo Long data. Cuando se selecciona una propiedad para la opción **[!UICONTROL Service output attribute to be mapping]**, solo se rellenan las variables capaces de almacenar datos de la propiedad seleccionada para la opción **[!UICONTROL Save the output to]**.

* **Salida de servicio > Guardar salida en variable o un archivo JSON:** seleccione la opción para guardar los valores de salida en un archivo JSON en una ruta absoluta, en una ruta relativa a la carga útil o en una variable.
* **Guarde el documento JSON de salida con las siguientes opciones:** Guarde el archivo JSON de salida. La ruta del archivo JSON de salida puede ser relativa a la carga útil o a una ruta absoluta. También puede guardar el archivo JSON de salida con una variable de tipo de datos JSON o del Modelo de datos de formulario.

## Paso Firmar documento {#sign-document-step}

El paso Firmar documento le permite utilizar Adobe Sign para firmar documentos. El paso Firmar documento tiene las siguientes propiedades:

* **Nombre del Acuerdo:** especifique el título del acuerdo. El nombre del acuerdo forma parte del asunto y del texto del cuerpo del correo electrónico enviado a los firmantes. Puede almacenar el nombre en una variable del tipo de datos String o seleccionar **Literal** para agregar el nombre manualmente.

* **Configuración regional:** especifique el idioma para las opciones de correo electrónico y verificación. Puede almacenar la configuración regional en una variable del tipo de datos String o seleccionar **Literal** para elegir la configuración regional de la lista de opciones disponibles. Debe definir el código de configuración regional mientras almacena el valor de la configuración regional en una variable. Por ejemplo, especifique **en_US** para inglés y **fr_FR** para francés.

* **Configuración** de Adobe Sign Cloud: Elija una configuración de Adobe Sign Cloud . Si no ha configurado Adobe Sign para AEM Forms, consulte [Integrar Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

* **Seleccionar documento para firmar mediante:** puede elegir un documento de una ubicación relativa a la carga útil, utilizar la carga útil como documento, especificar una ruta absoluta del documento o recuperar el documento almacenado en una variable de tipo Document data.
* **Días hasta la fecha límite:** un documento se marca con retraso (fecha límite superada) después de que no haya actividad en la tarea para el número de días especificado en el campo  **Días hasta la** fecha límite. El número de días se cuenta después de que el documento se asigne a un usuario para su firma.
* **Frecuencia de correo electrónico del recordatorio:** puede enviar un correo electrónico recordatorio a intervalos diarios o semanales. La semana se cuenta desde el día en que se asigna el documento a un usuario para su firma.
* **Proceso de firma:** puede optar por firmar un documento en un orden secuencial o paralelo. En orden secuencial, un firmante recibe el documento a la vez para su firma. Una vez que el primer firmante completa la firma del documento, el documento se envía al segundo firmante, etc. En orden paralelo, varios firmantes pueden firmar un documento a la vez.
* **Dirección URL de redirección:** especifique una dirección URL de redirección. Una vez firmado el documento, puede redirigir al usuario asignado a una dirección URL. Normalmente, esta URL contiene un mensaje de agradecimiento o instrucciones adicionales.
* **Etapa de flujo de trabajo:** un flujo de trabajo puede tener varias etapas. Estas etapas se muestran en la Bandeja de entrada AEM. Puede definir estas etapas en las propiedades del modelo (Barra de tareas > Página > Propiedades de la página > Etapas).
* **Seleccionar firmantes:** especifique el método para elegir firmantes para el documento. Puede asignar dinámicamente el flujo de trabajo a un usuario o grupo, o agregar manualmente los detalles de un firmante.
* **Script o servicio para seleccionar firmantes:**  la opción solo está disponible si la opción Dinámicamente está seleccionada en el campo Seleccionar firmantes . Puede especificar un ECMAScript o un servicio para elegir los firmantes y las opciones de verificación de un documento.
* **Detalles del firmante:** la opción solo está disponible si la opción Manualmente está seleccionada en el campo Seleccionar firmantes . Especifique la dirección de correo electrónico y elija un mecanismo de verificación opcional. Antes de seleccionar un mecanismo de verificación de 2 pasos, asegúrese de que la opción de verificación correspondiente esté habilitada para la cuenta de Adobe Sign configurada. Puede utilizar una variable del tipo de datos String para definir los valores de los campos **[!UICONTROL Email]**, **[!UICONTROL Country Code]** y **[!UICONTROL Phone Number]**. Los campos **[!UICONTROL Country Code]** y **[!UICONTROL Phone Number]** solo se muestran si selecciona **[!UICONTROL Phone Verify]** en la lista desplegable **[!UICONTROL Verificación en 2 pasos]**.
* **Variable de estado:** un documento habilitado para Adobe Sign almacena el estado de firma del documento en una variable de tipo de datos String. Especifique el nombre de la variable de estado (adobeSignStatus). Una variable de estado de una instancia está disponible en CRXDE en /etc/workflow/instances/&lt;server>/&lt;date-time>/&lt;instance of workflow model>/workItems/&lt;node>/metaData contiene el estado de una variable.
* **Guardar documento firmado con las siguientes opciones:** especifique la ubicación para conservar los documentos firmados. Puede sobrescribir el archivo de carga útil, colocar el documento firmado en una ubicación del directorio de carga útil o almacenar el documento firmado en una variable de tipo Document .

## Pasos de Servicios de documentos {#document-services-steps}

AEM Document Services son un conjunto de servicios para crear, ensamblar y proteger documentos PDF. AEM Forms proporciona un paso AEM Workflow independiente para cada servicio de documentos.

Al igual que otros pasos del flujo de trabajo de AEM Forms, como Asignar tarea, Enviar correo electrónico y Firmar documento, puede utilizar variables en todos los pasos de AEM Document Services. Para obtener más información sobre la creación y administración de variables, consulte [Variables en flujos de trabajo de AEM](../../forms/using/variable-in-aem-workflows.md).

### Aplicar marca de hora de documento {#apply-document-time-stamp-step}

Agregue una marca de hora a un documento. Proporcione detalles del documento, como la ruta del documento de entrada, el nombre del documento de entrada y la ubicación para almacenar los datos exportados. Puede optar por sobrescribir el archivo de carga útil existente, elegir un nombre de archivo diferente para almacenar datos en un archivo diferente en la carpeta de carga útil, proporcionar una ruta absoluta a los datos o almacenar datos en una variable de tipo Document data .

### Convertir en paso de imagen {#convert-to-image-step}

Convierte un documento PDF en una lista de imágenes. Los formatos de imagen admitidos son JPEG, JPEG2000, PNG y TIFF. La siguiente información se aplica a las conversiones a imágenes TIFF:

* Se genera un archivo TIFF de varias páginas.
* Algunas anotaciones no se incluyen en imágenes TIFF. No se incluyen las anotaciones que requieren que Acrobat genere su aspecto.

### Convertir en paso PDF/A {#convert-to-pdf-a-step}

Convierte un documento PDF en formato PDF/A utilizando las opciones proporcionadas. La versión PDF/A de Portable Document Format (PDF) está especializada en archivar y conservar documentos a largo plazo.

### Convertir en paso PS {#convert-to-ps-step}

Convertir documentos PDF a PostScript. Al convertir a PostScript, puede utilizar la operación de conversión para especificar el documento de origen y si desea convertir a PostScript de nivel 2 o 3. El documento PDF que convierta a un archivo PostScript debe ser no interactivo.

### Crear PDF desde el paso de tipo especificado {#create-pdf-from-specified-type-step}

Genere un documento PDF a partir de un archivo de entrada. El documento de entrada puede ser relativo a la carga útil, tener una ruta absoluta, puede ser carga útil en sí mismo o almacenarse en una variable del tipo de datos Document .

### Crear PDF a partir del paso URL/HTML/ZIP {#create-pdf-from-url-html-zip-step}

Genera un documento PDF a partir de la dirección URL, HTML y archivo ZIP suministrados.

### Paso Exportar datos {#export-data-step}

Exporta datos de un archivo PDF forms o XDP. Es necesario que introduzca la ruta de archivo del Documento de entrada y el Formato de datos de exportación. Las opciones de Formato de datos de exportación son Auto, XDP y XmlData.

### Export PDF al paso de tipo especificado {#export-pdf-to-specified-type-step}

Convierte un documento PDF en un formato seleccionado.

### Generar paso de PDF no interactivo {#generatenoninteractive}

Generar un PDF no interactivo. Proporciona varias opciones de personalización.

>[!NOTE]
>
>Puede utilizar variables para especificar el archivo de plantilla para los documentos de entrada. Almacene la ruta del archivo de plantilla en una variable del tipo de datos String .

### Paso Importar datos {#import-data-step}

Combina datos de formulario en un formulario PDF. Puede importar datos de formulario en un formulario PDF.

### Invocar paso DDX {#invokeddx}

Ejecuta el archivo DDX en el mapa especificado de documentos de entrada y devuelve los documentos PDF manipulados.

>[!NOTE]
>
>Puede utilizar variables para especificar el archivo DDX para los documentos de entrada. Almacene el archivo DDX en una variable de tipo de datos Document o XML.

### paso del Optimize PDF {#optimize-pdf-step}

Optimiza los archivos PDF reduciendo su tamaño. El resultado de esta conversión son archivos PDF que pueden ser más pequeños que sus versiones originales. Esta operación también convierte los documentos PDF a la versión PDF especificada en los parámetros de optimización.

La configuración de optimización especifica cómo se optimizan los archivos. A continuación se muestra un ejemplo de configuración:

* Versión de PDF de Target
* Descartar objetos, como acciones de JavaScript y miniaturas de páginas incrustadas
* Descartar datos de usuario, como comentarios y archivos adjuntos
* Descartar configuración no válida o no utilizada
* Compresión de datos sin comprimir o uso de algoritmos de compresión más eficientes
* Eliminación de fuentes incrustadas
* Configuración de los valores de transparencia

### paso Procesar formulario PDF {#renderpdf}

Procesa un formulario creado en Form Designer (XDP) en un formulario PDF.

>[!NOTE]
>
>Puede utilizar variables para especificar el archivo de plantilla para los documentos de entrada. Almacene la ruta del archivo de plantilla en una variable del tipo de datos String .

### Paso Secure Document {#secure-document-step}

Codificar, firmar y certificar un documento. AEM Forms admite el cifrado basado en contraseña y en certificado. También puede elegir entre varios algoritmos para firmar documentos. Por ejemplo, SHA-256 y SH-512. También puede utilizar el paso del flujo de trabajo para leer y ampliar documentos PDF. El paso del flujo de trabajo ofrece la opción de habilitar la descodificación de código de barras, las firmas digitales, la importación y exportación de datos PDF, y otras opciones.

### Paso Enviar a impresora {#send-to-printer-step}

Envíe un documento directamente a una impresora. Admite los siguientes mecanismos de acceso de impresión:

* **Impresora** accesible directa: Una impresora instalada en el mismo equipo se denomina impresora de acceso directo y el equipo se denomina host de impresora. Este tipo de impresora puede ser una impresora local que esté conectada al equipo directamente.
* **Impresora** accesible indirecto: Se accede a la impresora instalada en un servidor de impresión desde otros equipos. Tecnologías como el sistema de impresión UNIX® (CUPS) común y el protocolo Line Printer Daemon (LPD) están disponibles para conectarse a una impresora de red. Para acceder a una impresora accesible indirectamente, especifique la IP o el nombre de host del servidor de impresión. Con este mecanismo, puede enviar un documento a un URI LPD cuando la red tenga un LPD en ejecución. El mecanismo permite enrutar el documento a cualquier impresora que esté conectada a la red que tenga una LPD en ejecución.

### Generar paso de salida impreso {#generatePrintedOutput}

El paso genera una salida PCL, PostScript, ZPL, IPL, TPCL o DPL a partir de un diseño de formulario y un archivo de datos. El archivo de datos se combina con el diseño de formulario y se le aplica un formato para imprimirlo. La salida generada por este paso se puede enviar directamente a una impresora o guardarse como archivo. Se recomienda utilizar este paso cuando desee utilizar diseños de formulario o datos de una aplicación. Si los diseños de formulario o los diseños de formulario se encuentran en la red, el sistema de archivos local o la ubicación HTTP, utilice la operación generatePrintedOutput .

Por ejemplo, la aplicación requiere que combine un diseño de formulario con un archivo de datos. Los datos contienen cientos de registros. Además, requiere que la salida se envíe a una impresora compatible con ZPL. El diseño de formulario y los datos de entrada se encuentran en una aplicación. Utilice la operación generatePrintedOutput para combinar cada registro con un diseño de formulario y enviar la salida a una impresora compatible con ZPL.

El paso Generar salida impresa tiene las siguientes propiedades:

**Propiedades de entrada**

* **[!UICONTROL Seleccione el archivo de plantilla mediante]**: Especifique la ruta del archivo de plantilla. Puede seleccionar el archivo de plantilla utilizando la ruta relativa a la carga útil, guardada en una ruta absoluta o utilizando una variable del tipo de datos Document . Por ejemplo, [Payload_Directory]/Workflow/data.xml. Si la ruta no existe en el repositorio crx, un administrador puede crear la ruta antes de utilizarla. Además, también puede aceptar la carga útil como archivo de datos de entrada.

* **[!UICONTROL Seleccionar documento de datos mediante]**: Especifique la ruta de un archivo de datos de entrada. Puede seleccionar el archivo de datos de entrada utilizando la ruta relativa a la carga útil, guardada en una ruta absoluta o utilizando una variable del tipo de datos Document . Por ejemplo, [Payload_Directory]/Workflow/data.xml. Si la ruta no existe en el repositorio crx, un administrador puede crear la ruta antes de utilizarla.

* **[!UICONTROL Formato]** de impresora: Valor de formato de impresión que especifica el idioma de descripción de la página que se utilizará, cuando no se proporcione un archivo XDC, para generar el flujo de salida. Si proporciona un valor literal, seleccione uno de estos valores:

   * **[!UICONTROL PCL]** personalizado: Utilice la opción para especificar un archivo XDC personalizado para PCL.
   * **[!UICONTROL PostScript]** personalizado: Utilice la opción para especificar un archivo XDC personalizado para PostScript.
   * **[!UICONTROL ZPL]** personalizado: Utilice la opción para especificar un archivo XDC personalizado para ZPL.
   * **[!UICONTROL Color genérico PCL (5c)]**: Utilice un PCL de color genérico (5c).
   * **[!UICONTROL PostScript genérico Nivel3]**: Utilice PostScript Level 3 genérico.
   * **[!UICONTROL ZPL 300 DPI]**: Utilice ZPL 300 DPI. Se utiliza zpl300.xdc.
   * **[!UICONTROL ZPL 600 DPI]**: Utilice ZPL 600 DPI. Se utiliza el archivo zpl600.xdc.
   * **[!UICONTROL IPL]** personalizado: Utilice la opción para especificar un archivo XDC personalizado para IPL.
   * **[!UICONTROL IPL 300 DPI]**: Utilice IPL 300 DPI. Se utiliza ipl300.xdc.
   * **[!UICONTROL IPL 400 DPI]**: Utilice IPL 400 DPI. Se utiliza el archivo ipl400.xdc.
   * **[!UICONTROL TPCL]** personalizado: Utilice la opción para especificar un archivo XDC personalizado para TPCL.
   * **[!UICONTROL TPCL 305 DPI]**: Utilice TPCL 300 DPI. Se utiliza el archivo tpcl305.xdc.
   * **[!UICONTROL PCL 600 DPI]**: Utilice TPCL 600 DPI. Se utiliza el archivo tpcl600.xdc.
   * **[!UICONTROL DPL]** personalizado: Utilice la opción para especificar un DPL de archivo XDC personalizado.
   * **[!UICONTROL DPL300DPI]**: Utilice DPL 300 DPI. Se utiliza el archivo dpl300.xdc.
   * **[!UICONTROL DPL406DPI]**: Utilice DPL 400 DPI. Se utiliza el dpl406.xdc.
   * **[!UICONTROL DPL600DPI]**: Utilice DPL 600 DPI. Se utiliza el dpl600.xdc.

**Propiedades de salida**

* **[!UICONTROL Guarde el documento de salida mediante]**: Especifique la ubicación para guardar el archivo de salida. Puede guardar el archivo de salida en una ubicación relativa a la carga útil, en una variable, o especificar una ubicación absoluta para guardar el archivo de salida. Si la ruta no existe en el repositorio crx, un administrador puede crear la ruta antes de utilizarla.

**Propiedades avanzadas**

* **[!UICONTROL Seleccione la ubicación raíz del contenido mediante]**: La raíz del contenido es un valor de cadena que especifica el URI, la referencia absoluta o la ubicación en el repositorio para recuperar los recursos relativos utilizados por el diseño de formulario. Por ejemplo, si el diseño de formulario hace referencia a una imagen de forma relativa, como ../myImage.gif, myImage.gif debe estar ubicado en repository://. El valor predeterminado es repository://, que apunta al nivel raíz del repositorio.

   Cuando elige un recurso de la aplicación, la ruta URI raíz del contenido debe tener la estructura correcta. Por ejemplo, si se selecciona un formulario de una aplicación denominada SampleApp y se coloca en SampleApp/1.0/forms/Test.xdp, el URI de raíz de contenido debe especificarse como repository://administrator@password/Applications/SampleApp/1.0/forms/ o repositorio:/Applications/SampleApp/1.0/forms/ (cuando la autoridad es nula). Cuando se especifica el URI de raíz de contenido de esta forma, las rutas de todos los recursos a los que se hace referencia en el formulario se resuelven en relación con este URI.

* **[!UICONTROL Seleccione el archivo XCI mediante]**: Los archivos XCI se utilizan para describir fuentes y otras propiedades que se utilizan para elementos de diseño de formulario. Puede mantener un archivo XCI relativo a la carga útil, en una ruta absoluta o utilizando una variable del tipo de datos Document .

* **[!UICONTROL Configuración regional]**: Especifica el idioma utilizado para generar el documento PDF. Si proporciona un valor literal, seleccione un idioma de la lista o seleccione uno de estos valores:
   * **Para usar el servidor predeterminado**: (Predeterminado) Use la configuración regional configurada en el servidor de AEM Forms. La configuración regional se configura con la Consola de administración. (Consulte [Ayuda de Designer](http://www.adobe.com/go/learn_aemforms_designer_65)).

   * **Para utilizar un valor** personalizado: Escriba el código de configuración regional en el cuadro literal o seleccione una variable de cadena que contenga el código de configuración regional. Para obtener una lista completa de los códigos de configuración regional admitidos, consulte http://java.sun.com/j2se/1.5.0/docs/guide/intl/locale.doc.html.

* **[!UICONTROL Copias]**: Un valor entero que especifica el número de copias que se generarán para la salida. El valor predeterminado es 1.

* **[!UICONTROL Impresión]** a doble cara: Un valor de Paginación que especifica si se utiliza la impresión a doble cara o a una sola cara. Las impresoras compatibles con PostScript y PCL utilizan este valor. Si proporciona un valor literal, seleccione uno de estos valores:
   * **[!UICONTROL Borde largo dúplex]**: Utilice la impresión a doble cara y la impresión mediante paginación de borde largo.
   * **[!UICONTROL Borde]** corto dúplex: Utilice la impresión a doble cara y la impresión mediante paginación de borde corto.
   * **[!UICONTROL Simple]**: Utilice la impresión a una sola cara.
