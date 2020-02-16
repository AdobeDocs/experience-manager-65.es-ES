---
title: Configuración de la configuración del servidor
seo-title: Configuración de la configuración del servidor
description: La página Ajustes del servidor proporciona acceso al correo electrónico, la notificación de tareas y la configuración de la notificación del administrador.
seo-description: La página Ajustes del servidor proporciona acceso al correo electrónico, la notificación de tareas y la configuración de la notificación del administrador.
uuid: 73b51ac0-56e5-4748-bb33-e3986c69eb2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e047a95e-0acb-438a-8d27-f005c0adc508
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuración de la configuración del servidor {#configuring-server-settings}

La página Ajustes del servidor proporciona acceso a varias opciones de configuración para el flujo de trabajo de formularios:

* **Configuración** de correo electrónico que habilita los mensajes de correo electrónico salientes, junto con la configuración del servidor de correo electrónico utilizada para dichos mensajes. (See [Configuring email settings](configuring-server-settings.md#configuring-email-settings).)
* **Configuración** de notificación de tareas que habilita, deshabilita o modifica los mensajes enviados en notificaciones por correo electrónico a usuarios finales y grupos con respecto a sus tareas. (Consulte [Configuración de notificaciones para usuarios y grupos](configuring-server-settings.md#configuring-notifications-for-users-and-groups)).
* **Configuración** de notificación del administrador que habilita, deshabilita o modifica los mensajes enviados en las notificaciones por correo electrónico para tareas administrativas. (Consulte [Configuración de notificaciones para administradores](configuring-server-settings.md#configuring-notifications-for-administrators)).

## Configuración de la configuración de correo electrónico {#configuring-email-settings}

Puede especificar una cuenta de correo electrónico para el servidor de formularios, a través del cual se envían mensajes de correo electrónico a los usuarios y administradores de formularios AEM. Estos mensajes de correo electrónico se utilizan para notificar y recordar a los usuarios las tareas que deben completar, notificar al usuario las tareas que han alcanzado un plazo y notificar al administrador los errores de proceso que se produzcan.

Para habilitar el envío de mensajes de correo electrónico entre los formularios AEM y los usuarios, configure la configuración de correo electrónico saliente en la página Configuración de correo electrónico. El correo electrónico saliente debe utilizar un servidor SMTP.

Para permitir que los formularios AEM reciban y gestionen mensajes de correo electrónico entrantes de los usuarios, cree un extremo de correo electrónico para el servicio de tareas completas. (Consulte [Creación de un extremo de correo electrónico para el servicio](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service)de tareas completas).

Si los procesos están diseñados e implementados sin necesidad de enviar un correo electrónico, no es necesario configurar ninguna de las opciones de la página Configuración de correo electrónico.

### Configurar opciones de correo electrónico saliente {#configure-outgoing-email-settings}

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Configuración del servidor > Configuración de correo electrónico.
1. Seleccione Habilitar mensajes salientes.
1. En el cuadro Servidor SMTP, escriba el nombre del servidor de correo electrónico o la dirección IP. Todos los mensajes de correo electrónico de notificación del flujo de trabajo de formularios se envían desde este servidor de correo electrónico.
1. En los cuadros Nombre de usuario y Contraseña, escriba el nombre de inicio de sesión y la contraseña que se utilizarán cuando el servidor SMTP requiera autenticación. Déjelas en blanco si se permite el inicio de sesión anónimo.
1. En el cuadro Dirección de correo electrónico, escriba la dirección de correo electrónico que desea utilizar como dirección de retorno para los mensajes de correo electrónico que envía el flujo de trabajo de formularios.

   >[!NOTE]
   >
   >Si utiliza Microsoft Exchange Server y la dirección de correo electrónico no es válida, el servidor de Microsoft Exchange no puede enviar un correo electrónico a las listas de distribución. Para resolver el problema, seleccione la opción **Activar comunicación** externa por separado para cada lista de distribución en el servidor de Microsoft Exchange.

1. Haga clic en Guardar.

>[!NOTE]
>
>Si introduce información incorrecta, puede hacer clic en Cancelar para volver a la página mostrada anteriormente.

### Configuración de plantillas de correo electrónico para utilizar AEM Forms Workspace {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>Flex Workspace está en desuso para la versión de formularios AEM.

De forma predeterminada, los correos electrónicos enviados por formularios AEM contienen vínculos a Flex Workspace (obsoleto para formularios AEM en JEE). Puede configurar formularios AEM para enviar correos electrónicos con vínculos a AEM Forms Workspace. Para obtener más información sobre las ventajas de AEM Forms Workspace sobre Flex Workspace (obsoleto para formularios AEM en JEE), consulte [este](/help/forms/using/features-html-workspace-available-flex.md) artículo.

1. En la consola de administración, haga clic en Inicio > Servicios > Flujo de trabajo de formularios > Configuración del servidor > Notificaciones de tareas.
1. Abra la plantilla de asignación de tareas.
1. Defina la plantilla en las notificaciones de tareas de la siguiente manera: `https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```as3
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## Configuración de notificaciones para usuarios y grupos {#configuring-notifications-for-users-and-groups}

En la página Notificación de tareas, puede configurar plantillas que el flujo de trabajo de formularios utilizará para generar las notificaciones por correo electrónico que se envían a usuarios y grupos. Puede personalizar y dar formato a las notificaciones mediante variables de flujo de trabajo de formularios.

Puede configurar los siguientes tipos de notificaciones para usuarios y grupos:

* recordatorios
* asignaciones de tareas
* plazos

Para generar notificaciones por correo electrónico para un grupo, especifique una dirección de correo electrónico para el grupo en Administración de usuarios. <!--Fix broken link See Setting up and organizing users -->Cuando el flujo de trabajo de formularios envía una notificación por correo electrónico a un grupo, cada miembro del grupo que tenga una dirección de correo electrónico especificada recibe la notificación por correo electrónico. Cuando un miembro del grupo recibe una notificación por correo electrónico y desea reclamar la tarea, debe hacer clic en el vínculo de la notificación por correo electrónico, que abre la página de detalles de la tarea en Workspace. Desde allí, el miembro puede reclamar o reclamar y abrir el elemento de trabajo.

>[!NOTE]
>
>Flex Workspace está en desuso para la versión de formularios AEM.

### Configurar recordatorios para usuarios o grupos {#configure-reminders-for-users-or-groups}

Puede enviar notificaciones de recordatorio al usuario o grupo asignado cuando se aproxime una fecha límite para completar una tarea. El desarrollador del proceso determina las reglas para determinar exactamente cuándo se envía una notificación de recordatorio.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Configuración del servidor > Notificaciones de tareas.
1. En Tipo de notificación, haga clic en Recordatorio (para usuarios) o Grupo - Recordatorio (para grupos).
1. Seleccione Habilitar recordatorio o Habilitar grupo: recordatorio.
1. (Solo notificaciones del usuario) Para incluir un archivo adjunto del formulario y sus datos con el mensaje de correo electrónico del recordatorio, seleccione Incluir datos del formulario.
1. En el cuadro Asunto, escriba el texto de la línea de asunto del mensaje de correo electrónico. Este campo se rellena previamente con texto predeterminado. Para obtener más información sobre la personalización de este campo, consulte [Personalización del contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. En el cuadro Plantilla de notificación, escriba el texto del cuerpo del mensaje de correo electrónico. Este campo se rellena previamente con texto predeterminado. Para obtener más información sobre la personalización de este campo, consulte [Personalización del contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. En la lista Formato del mensaje, seleccione el formato en el que se envía el mensaje de correo electrónico, ya sea HTML o Texto. El formato predeterminado es HTML.
1. En la lista Codificación de correo electrónico, seleccione el formato de codificación que se utilizará para el mensaje de correo electrónico. El valor predeterminado es UTF-8, que usará la mayoría de los usuarios fuera de Japón. Los usuarios de Japón pueden seleccionar ISO2022-JP.
1. Haga clic en Guardar.

### Configurar las notificaciones de asignación de tareas para usuarios o grupos {#configure-task-assignment-notifications-for-users-or-groups}

Puede enviar notificaciones de asignación de tareas a un usuario o grupo cuando se les asigne una tarea.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Configuración del servidor > Notificaciones de tareas.
1. En Tipo de notificación, haga clic en Asignación de tareas para usuarios o Grupo - Asignación de tareas para grupos.
1. Seleccione Habilitar la asignación de tareas para usuarios o Habilitar la asignación de grupo - tarea para grupos.
1. (Solo notificaciones del usuario) Para incluir un archivo adjunto del formulario y sus datos con el mensaje de correo electrónico de asignación de tareas, seleccione Incluir datos del formulario.
1. En el cuadro Asunto, escriba el texto de la línea de asunto del mensaje de correo electrónico. Este campo se rellena previamente con texto predeterminado. Para obtener más información sobre la personalización de este campo, consulte [Personalización del contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. En el cuadro Plantilla de notificación, escriba el texto del cuerpo del mensaje de correo electrónico. Este campo se rellena previamente con texto predeterminado. Para obtener más información sobre la personalización de este campo, consulte [Personalización del contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. En la lista Formato del mensaje, seleccione el formato en el que se envía el mensaje de correo electrónico, ya sea HTML o Texto. El formato predeterminado es HTML.
1. En la lista Codificación de correo electrónico, seleccione el formato de codificación que se utilizará para el mensaje de correo electrónico. El valor predeterminado es UTF-8, que usará la mayoría de los usuarios fuera de Japón. Los usuarios de Japón pueden seleccionar ISO2022-JP.
1. Haga clic en Guardar.

### Configuración de las notificaciones de fecha límite para usuarios o grupos {#configure-deadline-notifications-for-users-or-groups}

Puede enviar notificaciones de fecha límite a usuarios y grupos cuando haya transcurrido el plazo para actuar en función de una tarea asignada. Una notificación de fecha límite suele ser informativa porque el usuario ya no puede actuar en la tarea asignada.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Configuración del servidor > Notificaciones de tareas.
1. En Tipo de notificación, haga clic en Fecha límite (para usuarios) o Grupo - Fecha límite (para grupos).
1. Seleccione Activar fecha límite o Habilitar grupo: fecha límite.
1. En el cuadro Asunto, escriba el texto de la línea de asunto del mensaje de correo electrónico. Este campo se rellena previamente con texto predeterminado. Para obtener más información sobre la personalización de este campo, consulte [Personalización del contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. En el cuadro Plantilla de notificación, escriba el texto del cuerpo del mensaje de correo electrónico. Este campo se rellena previamente con texto predeterminado. Para obtener más información sobre la personalización de este campo, consulte [Personalización del contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. En la lista Formato del mensaje, seleccione el formato en el que se envía el mensaje de correo electrónico, ya sea HTML o Texto. El formato predeterminado es HTML.
1. En la lista Codificación de correo electrónico, seleccione el formato de codificación que se utilizará para el mensaje de correo electrónico. El valor predeterminado es UTF-8, que usará la mayoría de los usuarios fuera de Japón. Los usuarios de Japón pueden seleccionar ISO2022-JP.
1. Haga clic en Guardar.

### Ocultar la etiqueta NO ELIMINAR para todos los correos electrónicos {#hide-the-do-not-delete-tag-for-all-emails}

Puede configurar el correo electrónico para que se oculte en la etiqueta de seguimiento DO NOT DELETE en todos los correos electrónicos enviados en un proceso centrado en el ser humano. Para obtener más información, consulte [Cómo ocultar la etiqueta &#39;NO-ELIMINAR&#39; con CSS](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html)

## Configuración de notificaciones para administradores {#configuring-notifications-for-administrators}

Puede configurar plantillas que el flujo de trabajo de formularios utilizará para generar las notificaciones por correo electrónico que se envían a los administradores.

Los administradores pueden configurar los siguientes tipos de notificaciones:

* rama detenida
* operación detenida

### Configuración de notificaciones de ramas estancadas {#configure-stalled-branch-notifications}

Si una rama se detiene (deja de continuar deliberadamente o debido a un error), puede enviar una notificación por correo electrónico a un administrador u otro usuario, que luego puede investigar el problema.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Configuración del servidor > Notificaciones de administrador.
1. En Tipo de notificación, haga clic en Rama detenida.
1. Seleccione Activar rama paralizada.
1. En el cuadro Dirección de correo electrónico, escriba las direcciones de los usuarios a los que se debe notificar cuando se estanca una rama. Utilice el formato user@domain.com y separe cada dirección con una coma. Normalmente, esta dirección de correo electrónico es para un administrador.
1. En el cuadro Asunto, escriba el texto de la línea de asunto del mensaje de correo electrónico. Este campo se rellena previamente con texto predeterminado. Para obtener más información sobre la personalización de este campo, consulte [Personalización del contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. En el cuadro Plantilla de notificación, escriba el texto del cuerpo del mensaje de correo electrónico. Este campo se rellena previamente con texto predeterminado. Para obtener más información sobre la personalización de este campo, consulte [Personalización del contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. En la lista Formato del mensaje, seleccione el formato en el que se envía el mensaje de correo electrónico, ya sea HTML o Texto. El formato predeterminado es HTML.
1. En la lista Codificación de correo electrónico, seleccione el formato de codificación que se utilizará para el mensaje de correo electrónico. El valor predeterminado es UTF-8, que utiliza la mayoría de los usuarios fuera de Japón. Los usuarios de Japón pueden seleccionar ISO2022-JP.
1. Haga clic en Guardar.

### Configuración de notificaciones de operaciones inmovilizadas {#configure-stalled-operation-notifications}

Si una operación se detiene (deja de continuar deliberadamente o debido a un error), puede enviar una notificación por correo electrónico a un administrador u otro usuario, que puede investigar el problema.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Configuración del servidor > Notificaciones de administrador.
1. En Tipo de notificación, haga clic en Operación detenida.
1. Seleccione Activar operación paralizada.
1. En el cuadro Direcciones de correo electrónico, escriba las direcciones de los usuarios a los que se notificará cuando se detenga una operación. Utilice el formato user@domain.com y separe cada dirección con una coma. Normalmente, esta dirección de correo electrónico es para un administrador.
1. En el cuadro Asunto, escriba el texto de la línea de asunto del mensaje de correo electrónico. Este campo se rellena previamente con texto predeterminado. Para obtener más información sobre la personalización de este campo, consulte [Personalización del contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications)
1. En el cuadro Plantilla de notificación, escriba el texto del cuerpo del mensaje de correo electrónico. Este campo se rellena previamente con texto predeterminado. Para obtener más información sobre la personalización de este campo, consulte [Personalización del contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Haga clic en Guardar.

## Personalización del contenido de las notificaciones {#customizing-the-content-of-notifications}

Las páginas Notificaciones de tareas y Notificaciones de administrador proporcionan varias funciones que le permiten personalizar los mensajes de notificación:

* editor de texto enriquecido
* selector de variable
* Generación de direcciones URL

### Rich text editor {#rich-text-editor}

El área Plantilla de notificación es un editor de texto enriquecido que permite generar HTML para los mensajes de notificación por correo electrónico. Proporciona opciones de formato de fuente y párrafo, que se encuentran debajo del cuadro Plantilla de notificación. Las opciones incluyen tipo de fuente, tamaño, estilo y color, así como alineación de párrafo y viñetas.

### Generación de direcciones URL {#url-generation}

Solo para Notificaciones de tareas, el flujo de trabajo de Forms incluye dos configuraciones de URL predefinidas que puede arrastrar desde la lista Generación de direcciones URL al cuadro Plantilla de notificación y, a continuación, personalizar:

* OpenTask está disponible para los tipos de notificación Reminder y Asignación de tareas. Esta URL proporciona un vínculo a la tarea en Workspace, lo que permite al usuario acceder rápidamente a la tarea desde la notificación por correo electrónico. Cuando arrastra la dirección URL OpenTask al cuadro Plantilla de notificación, la dirección URL tiene el siguiente formato:

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* ClaimTask está disponible para los tipos de notificación Grupo - Recordatorio y Grupo - Asignación de tareas. Esta URL proporciona un vínculo a la página de detalles de la tarea en Workspace, donde el usuario puede reclamar o reclamar y abrir el elemento de trabajo. Cuando arrastra la URL de ClaimTask al cuadro Plantilla de notificación, la URL tiene el siguiente formato:

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>Flex Workspace está en desuso para la versión de formularios AEM.

Si la solución está implementada en un entorno agrupado, reemplace `@@notification-host@@` por la dirección del clúster.

`<`*PORT *`>`es el número de puerto del listener HTTP para el servidor de aplicaciones. El puerto de escucha HTTP predeterminado para los servidores de aplicaciones admitidos es el siguiente:

**** JBoss: 8080

**** Oracle WebLogic Server: 7001

**** IBM WebSphere: 9080

Para que estas direcciones URL funcionen correctamente, reemplace `<`*PORT *`>`por el número de puerto adecuado para su entorno.

***Nota **: Si utiliza una aplicación web personalizada que no sea Forms para proporcionar a los usuarios acceso a las tareas, debe utilizar un formato de URL adecuado para la aplicación personalizada.*

### Selector de variable {#variable-picker}

La lista Selector de variables proporciona variables útiles que puede arrastrar y soltar en los cuadros Asunto o Plantilla de notificación. Cuando se coloca una variable en los cuadros Asunto o Plantilla de notificación, cambia al nombre real de la variable de flujo de trabajo de formularios con dos símbolos @ a ambos lados, por ejemplo `@@taskid@@`.

Para recordatorios, asignaciones de tareas y fechas límite para usuarios y grupos, puede utilizar las siguientes variables en los cuadros Asunto y Plantilla de notificación:

**description** El contenido de la propiedad Description, tal como se define en el paso del usuario (punto de inicio, operación Asignar tarea o operación Asignar varias tareas) del proceso en Workbench.

**instrucciones** El contenido de la propiedad Instrucciones de tarea, tal como se define en el paso del usuario del proceso en Workbench.

**notification-host** El nombre de host del servidor de aplicaciones de formularios AEM.

**process-name** El nombre del proceso.

**operation-name** El nombre del paso.

**taskid** El identificador único de la tarea actual.

**acciones** Produce una lista numerada de rutas válidas (por ejemplo, Aprobar, Rechazar) en la que el destinatario puede hacer clic.

Además, para los recordatorios de grupo, las asignaciones de tareas de grupo y las fechas límite de grupo, también puede utilizar:

**group-name** El nombre del grupo al que se asigna el elemento de trabajo.

**Nota**: *Si una variable no tiene ningún valor, no se devuelve nada.*

En el caso de las ramas paralizadas, puede utilizar las siguientes variables en los cuadros Asunto y Plantilla de notificación:

**branch-id** El identificador de rama.

**process-id** El identificador de instancia de proceso.

**notification-host** El nombre de host del servidor de aplicaciones de formularios AEM.

Para las operaciones paralizadas, puede utilizar las siguientes variables en los cuadros Asunto y Plantilla de notificación:

**action-id** El identificador de la operación.

**branch-id** El identificador de rama.

**process-id** El identificador de instancia de proceso.

**notification-host** El nombre de host del servidor de aplicaciones de formularios AEM.

### Uso de una variable en el cuadro Asunto {#using-a-variable-in-the-subject-box}

Si escribe el siguiente texto en el cuadro Asunto para las notificaciones de asignación de tareas:

`Please complete task @@taskid@@`

El usuario recibe un mensaje de correo electrónico con el siguiente asunto si tiene asignada la tarea 376:

`Please complete task 376`

### Uso de variables en el cuadro Plantilla de notificación {#using-variables-in-the-notification-template-box}

Si escribe el siguiente texto en el cuadro Plantilla de notificación para las notificaciones de ramificación paralizada:

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

El administrador recibe un mensaje de correo electrónico con el siguiente contenido si el número de ramificación es 4868 y el nombre del servidor es `ServerXYZ`:

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## Configuración de las conexiones de supervisión de la actividad comercial {#configuring-business-activity-monitoring-connections}

Business Activity Monitoring, un módulo opcional, proporciona un conjunto de tableros operativos que proporcionan visibilidad en tiempo real de sus operaciones e indicadores de rendimiento clave.

En la página Configuración de BAM, configure las conexiones al servidor que ejecuta BAM para que los eventos relacionados con el proceso se puedan rastrear y transmitir a ese servidor.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Configuración del servidor > Configuración de BAM.
1. En el cuadro Host de BAM, escriba el nombre del servidor que ejecuta BAM. El valor predeterminado es localhost.
1. En el cuadro Puerto de BAM, escriba el puerto que se va a utilizar para conectarse al servidor que ejecuta BAM. El puerto predeterminado de BAM para JBoss es 8080, WebLogic es 7001 y WebSphere es 9080.
1. En el cuadro Host del servidor, escriba el nombre o la dirección IP del servidor de formularios de host. El valor predeterminado es localhost.
1. En el cuadro Puerto del servidor, escriba el número de puerto utilizado por el servidor de formularios.
1. En los cuadros Nombre de usuario y Contraseña, escriba el ID de usuario y la contraseña correspondientes para acceder al servidor de BAM. El nombre de usuario predeterminado es CognosNowAdmin y la contraseña predeterminada es manager.
1. Haga clic en Guardar.

