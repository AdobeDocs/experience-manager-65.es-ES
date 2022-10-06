---
title: Configuración del servidor
seo-title: Configuring Server Settings
description: La página Configuración del servidor proporciona acceso al correo electrónico, la notificación de tareas y la configuración de notificación del administrador.
seo-description: The Server Settings page provides access to email, task notification and administrator notification settings.
uuid: 73b51ac0-56e5-4748-bb33-e3986c69eb2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e047a95e-0acb-438a-8d27-f005c0adc508
exl-id: 362b7b91-c58b-4e47-a6ef-56a4b54a100c
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '2625'
ht-degree: 0%

---

# Configuración del servidor {#configuring-server-settings}

La página Configuración del servidor proporciona acceso a varias configuraciones para el flujo de trabajo de formularios:

* **Configuración de correo electrónico** que habilitan los mensajes de correo electrónico salientes, junto con la configuración del servidor de correo electrónico que se utiliza para dichos mensajes. (Consulte [Configuración de correo electrónico](configuring-server-settings.md#configuring-email-settings).)
* **Configuración de notificaciones de tareas** que habiliten, deshabiliten o modifiquen los mensajes enviados en notificaciones por correo electrónico a usuarios y grupos finales con respecto a sus tareas. (Consulte [Configuración de notificaciones para usuarios y grupos](configuring-server-settings.md#configuring-notifications-for-users-and-groups).)
* **Configuración de notificaciones del administrador** que habiliten, deshabiliten o modifiquen los mensajes enviados en notificaciones por correo electrónico para tareas administrativas. (Consulte [Configuración de notificaciones para administradores](configuring-server-settings.md#configuring-notifications-for-administrators).)

## Configuración de correo electrónico {#configuring-email-settings}

Puede especificar una cuenta de correo electrónico para el servidor de formularios, a través de la cual envía mensajes de correo electrónico a los usuarios y administradores de formularios AEM. Estos mensajes de correo electrónico se utilizan para notificar y recordar a los usuarios las tareas que deben completar, notificar al usuario las tareas que han alcanzado una fecha límite y notificar al administrador de cualquier error de proceso que se produzca.

Para permitir el envío de mensajes de correo electrónico entre AEM formularios y los usuarios, configure la configuración de correo electrónico saliente en la página Configuración de correo electrónico . El correo electrónico saliente debe utilizar un servidor SMTP.

Para permitir que AEM formularios reciban y gestionen mensajes de correo electrónico entrantes de los usuarios, cree un extremo de correo electrónico para el servicio Tarea completa. (Consulte [Creación de un extremo de correo electrónico para el servicio Tarea completa](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service)).

Si los procesos están diseñados e implementados sin requerir correo electrónico, no es necesario configurar ninguna de las opciones de la página Configuración de correo electrónico .

### Configurar las opciones de correo electrónico salientes {#configure-outgoing-email-settings}

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Configuración del servidor > Configuración del correo electrónico.
1. Seleccione Habilitar mensajes salientes.
1. En el cuadro Servidor SMTP, escriba el nombre del servidor de correo electrónico o la dirección IP. Todos los mensajes de correo electrónico de notificación del flujo de trabajo de formularios se envían desde este servidor de correo electrónico.
1. En los cuadros Nombre de usuario y Contraseña, escriba el nombre de inicio de sesión y la contraseña que se utilizarán cuando el servidor SMTP requiera autenticación. Déjelos en blanco si se permite el inicio de sesión anónimo.
1. En el cuadro Dirección de correo electrónico, escriba la dirección de correo electrónico que se utilizará como dirección de retorno para los mensajes de correo electrónico que envía el flujo de trabajo de formularios.

   >[!NOTE]
   >
   >Si utiliza Microsoft Exchange Server y la dirección de correo electrónico es una dirección de correo electrónico no válida, el servidor de Microsoft Exchange no puede enviar un correo electrónico a las listas de distribución. Para resolver el problema, seleccione la opción **Habilitar la comunicación externa** por separado para cada Lista de distribución en el servidor de Microsoft Exchange.

1. Haga clic en Guardar.

>[!NOTE]
>
>Si introduce información incorrecta, puede hacer clic en Cancelar para volver a la página mostrada anteriormente.

### Configuración de plantillas de correo electrónico para utilizar AEM Forms Workspace {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>Flex Workspace está obsoleto para AEM versión de formularios.

De forma predeterminada, los correos electrónicos enviados por AEM formularios contienen vínculos a Flex Workspace (obsoleto para AEM formularios en JEE). Puede configurar AEM formularios para enviar correos electrónicos con vínculos a AEM Forms Workspace. Para obtener más información sobre las ventajas de AEM Forms Workspace sobre Flex Workspace (obsoleto para AEM formularios en JEE), consulte [this](/help/forms/using/features-html-workspace-available-flex.md) artículo.

1. En la consola de administración, haga clic en Inicio > Servicios > Flujo de trabajo de formularios > Configuración del servidor > Notificaciones de tareas.
1. Abra la plantilla de asignación de tareas.
1. Establezca la plantilla en las notificaciones de tareas de la siguiente manera: `https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```java
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## Configuración de notificaciones para usuarios y grupos {#configuring-notifications-for-users-and-groups}

En la página Notificación de tareas , puede configurar las plantillas que utilizará el flujo de trabajo de formularios para generar las notificaciones por correo electrónico que se envían a los usuarios y grupos. Puede personalizar y dar formato a las notificaciones mediante variables de flujo de trabajo de formularios.

Los siguientes tipos de notificaciones se configuran para usuarios y grupos:

* recordatorios
* asignaciones de tareas
* plazos

Para generar notificaciones por correo electrónico para un grupo, especifique una dirección de correo electrónico para el grupo en Administración de usuarios. <!--Fix broken link See Setting up and organizing users -->Cuando el flujo de trabajo de formularios envía una notificación por correo electrónico a un grupo, cada miembro del grupo que tenga una dirección de correo electrónico especificada recibe la notificación por correo electrónico. Cuando un miembro del grupo recibe una notificación por correo electrónico y desea reclamar la tarea, el miembro debe hacer clic en el vínculo de la solicitud en la notificación por correo electrónico, que abre la página de detalles de la tarea en Workspace. Desde allí, el miembro puede reclamar o reclamar y abrir el elemento de trabajo.

>[!NOTE]
>
>Flex Workspace está en desuso para AEM versión de formularios.

### Configurar recordatorios para usuarios o grupos {#configure-reminders-for-users-or-groups}

Puede enviar notificaciones de recordatorio al usuario o grupo asignado cuando se acerca una fecha límite para completar una tarea. El desarrollador del proceso determina las reglas para determinar exactamente cuándo se envía una notificación de recordatorio.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de Forms > Configuración del servidor > Notificaciones de tareas.
1. En Tipo de notificación, haga clic en Recordatorio (para usuarios) o Grupo - Recordatorio (para grupos).
1. Seleccione Activar recordatorio o Activar grupo - Recordatorio.
1. (Solo notificaciones del usuario) Para incluir un archivo adjunto del formulario y sus datos con el mensaje de correo electrónico recordatorio, seleccione Incluir datos del formulario.
1. En el cuadro Asunto, escriba el texto de la línea de asunto del mensaje de correo electrónico. Este campo se rellena previamente con texto predeterminado. Para obtener más información sobre la personalización de este campo, consulte [Personalización del contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. En el cuadro Plantilla de notificación, escriba el texto para el cuerpo del mensaje de correo electrónico. Este campo se rellena previamente con texto predeterminado. Para obtener más información sobre la personalización de este campo, consulte [Personalización del contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. En la lista Formato del mensaje, seleccione el formato en el que se envía el mensaje de correo electrónico, HTML o Texto. El formato predeterminado es HTML.
1. En la lista Codificación de correo electrónico, seleccione el formato de codificación que se utilizará para el mensaje de correo electrónico. El valor predeterminado es UTF-8, que la mayoría de los usuarios fuera de Japón utilizarán. Los usuarios de Japón pueden seleccionar ISO2022-JP.
1. Haga clic en Guardar.

### Configuración de notificaciones de asignación de tareas para usuarios o grupos {#configure-task-assignment-notifications-for-users-or-groups}

Puede enviar notificaciones de asignación de tareas a un usuario o grupo cuando se les asigne una tarea.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de Forms > Configuración del servidor > Notificaciones de tareas.
1. En Tipo de notificación, haga clic en Asignación de tareas para usuarios o Asignación de grupo - tarea para grupos.
1. Seleccione Habilitar asignación de tareas para usuarios o Habilitar asignación de grupo - tarea para grupos.
1. (Solo notificaciones del usuario) Para incluir un archivo adjunto del formulario y sus datos con el mensaje de correo electrónico de asignación de tareas, seleccione Incluir datos del formulario.
1. En el cuadro Asunto, escriba el texto de la línea de asunto del mensaje de correo electrónico. Este campo se rellena previamente con texto predeterminado. Para obtener más información sobre la personalización de este campo, consulte [Personalización del contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. En el cuadro Plantilla de notificación, escriba el texto para el cuerpo del mensaje de correo electrónico. Este campo se rellena previamente con texto predeterminado. Para obtener más información sobre la personalización de este campo, consulte [Personalización del contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. En la lista Formato del mensaje, seleccione el formato en el que se envía el mensaje de correo electrónico, HTML o Texto. El formato predeterminado es HTML.
1. En la lista Codificación de correo electrónico, seleccione el formato de codificación que se utilizará para el mensaje de correo electrónico. El valor predeterminado es UTF-8, que la mayoría de los usuarios fuera de Japón utilizarán. Los usuarios de Japón pueden seleccionar ISO2022-JP.
1. Haga clic en Guardar.

### Configuración de notificaciones de fechas límite para usuarios o grupos {#configure-deadline-notifications-for-users-or-groups}

Puede enviar notificaciones de fecha límite a usuarios y grupos cuando haya pasado la fecha límite para actuar sobre una tarea asignada. Una notificación de fecha límite suele ser informativa porque el usuario ya no puede actuar en la tarea asignada.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de Forms > Configuración del servidor > Notificaciones de tareas.
1. En Tipo de notificación, haga clic en Plazo (para usuarios) o Grupo - Plazo (para grupos).
1. Seleccione Activar fecha límite o Activar grupo - Fecha límite.
1. En el cuadro Asunto, escriba el texto de la línea de asunto del mensaje de correo electrónico. Este campo se rellena previamente con texto predeterminado. Para obtener más información sobre la personalización de este campo, consulte [Personalización del contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. En el cuadro Plantilla de notificación, escriba el texto para el cuerpo del mensaje de correo electrónico. Este campo se rellena previamente con texto predeterminado. Para obtener más información sobre la personalización de este campo, consulte [Personalización del contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. En la lista Formato del mensaje, seleccione el formato en el que se envía el mensaje de correo electrónico, HTML o Texto. El formato predeterminado es HTML.
1. En la lista Codificación de correo electrónico, seleccione el formato de codificación que se utilizará para el mensaje de correo electrónico. El valor predeterminado es UTF-8, que la mayoría de los usuarios fuera de Japón utilizarán. Los usuarios de Japón pueden seleccionar ISO2022-JP.
1. Haga clic en Guardar.

### Ocultar la etiqueta del DELETE DO NOT para todos los correos electrónicos {#hide-the-do-not-delete-tag-for-all-emails}

Puede configurar el correo electrónico para que se oculte a la etiqueta de seguimiento DO NOT DELETE en todos los correos electrónicos enviados en un proceso centrado en el ser humano.

<!-- 
For details, see [How to hide the 'DO-NOT-DELETE' tag with CSS](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html) 
-->

## Configuración de notificaciones para administradores {#configuring-notifications-for-administrators}

Puede configurar plantillas que el flujo de trabajo de formularios utilizará para generar las notificaciones de correo electrónico que se envían a los administradores.

Los siguientes tipos de notificaciones se configuran para los administradores:

* sucursal paralizada
* operación interrumpida

### Configurar notificaciones de ramas interrumpidas {#configure-stalled-branch-notifications}

Si una rama se detiene (deja de continuar deliberadamente o debido a un error), puede enviar una notificación por correo electrónico a un administrador u otro usuario, que puede investigar el problema.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de Forms > Configuración del servidor > Notificaciones de administrador.
1. En Tipo de notificación, haga clic en Rama de interrupción.
1. Seleccione Habilitar rama paralizada.
1. En el cuadro Dirección de correo electrónico, escriba las direcciones de los usuarios a los que se notificará cuando una rama se detenga. Utilice el formato user@domain.com y separe cada dirección con una coma. Normalmente, esta dirección de correo electrónico es para un administrador.
1. En el cuadro Asunto, escriba el texto de la línea de asunto del mensaje de correo electrónico. Este campo se rellena previamente con texto predeterminado. Para obtener más información sobre la personalización de este campo, consulte [Personalización del contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. En el cuadro Plantilla de notificación, escriba el texto para el cuerpo del mensaje de correo electrónico. Este campo se rellena previamente con texto predeterminado. Para obtener más información sobre la personalización de este campo, consulte [Personalización del contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. En la lista Formato del mensaje, seleccione el formato en el que se envía el mensaje de correo electrónico, HTML o Texto. El formato predeterminado es HTML.
1. En la lista Codificación de correo electrónico, seleccione el formato de codificación que se utilizará para el mensaje de correo electrónico. El valor predeterminado es UTF-8, que la mayoría de los usuarios fuera de Japón utilizan. Los usuarios de Japón pueden seleccionar ISO2022-JP.
1. Haga clic en Guardar.

### Configuración de notificaciones de operaciones interrumpidas {#configure-stalled-operation-notifications}

Si una operación se detiene (deja de continuar deliberadamente o debido a un error), puede enviar una notificación por correo electrónico a un administrador u otro usuario, que puede investigar el problema.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de Forms > Configuración del servidor > Notificaciones de administrador.
1. En Tipo de notificación, haga clic en Operación paralizada.
1. Seleccione Habilitar operación interrumpida.
1. En el cuadro Direcciones de correo electrónico, escriba las direcciones de los usuarios a los que se notificará cuando se detenga una operación. Utilice el formato user@domain.com y separe cada dirección con una coma. Normalmente, esta dirección de correo electrónico es para un administrador.
1. En el cuadro Asunto, escriba el texto de la línea de asunto del mensaje de correo electrónico. Este campo se rellena previamente con texto predeterminado. Para obtener más información sobre la personalización de este campo, consulte [Personalización del contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications)
1. En el cuadro Plantilla de notificación, escriba el texto para el cuerpo del mensaje de correo electrónico. Este campo se rellena previamente con texto predeterminado. Para obtener más información sobre la personalización de este campo, consulte [Personalización del contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Haga clic en Guardar.

## Personalización del contenido de las notificaciones {#customizing-the-content-of-notifications}

Las páginas Notificaciones de tareas y Notificaciones de administrador proporcionan varias funciones que le permiten personalizar los mensajes de notificación:

* editor de texto enriquecido
* selector de variables
* Generación de URL

### Editor de texto enriquecido {#rich-text-editor}

El área Plantilla de notificación es un editor de texto enriquecido que le permite generar un HTML para los mensajes de notificación de correo electrónico. Proporciona opciones de formato de fuente y párrafo, que se encuentran debajo del cuadro Plantilla de notificación. Las opciones incluyen tipo de fuente, tamaño, estilo y color, así como alineación de párrafos y viñetas.

### Generación de URL {#url-generation}

Solo para las notificaciones de tareas, el flujo de trabajo de Forms incluye dos configuraciones de URL predefinidas que puede arrastrar desde la lista Generación de direcciones URL al cuadro Plantilla de notificación y, a continuación, personalizar:

* OpenTask está disponible para los tipos de notificación Reminder y Task Assignment. Esta URL proporciona un vínculo a la tarea en Workspace, lo que permite al usuario acceder rápidamente a la tarea desde la notificación por correo electrónico. Cuando arrastra la dirección URL de OpenTask al cuadro Plantilla de notificación, la dirección URL tiene el siguiente formato:

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* ClaimTask está disponible para los tipos de notificación Group - Reminder y Group - Task Assignment. Esta URL proporciona un vínculo a la página de detalles de la tarea en Workspace, donde el usuario puede reclamar o reclamar y abrir el elemento de trabajo. Cuando arrastra la URL de ClaimTask al cuadro Plantilla de notificación, la URL tiene el siguiente formato:

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>Flex Workspace está en desuso para AEM versión de formularios.

Si su solución está implementada en un entorno agrupado, sustituya `@@notification-host@@` con la dirección del clúster.

`<`*PUERTO* `>` es el número de puerto del listener HTTP del servidor de aplicaciones. El puerto de escucha HTTP predeterminado para los servidores de aplicaciones compatibles es el siguiente:

**JBoss:** 8080

**Oracle WebLogic Server:** 7001

**IBM WebSphere:** 9080

Para que estas URL funcionen correctamente, reemplace `<`*PUERTO* `>` con el número de puerto adecuado para su entorno.

>[!NOTE]
>
>Si utiliza una aplicación web personalizada que no sea Forms para proporcionar a los usuarios acceso a las tareas, en su lugar debe utilizar un formato de URL apropiado para su aplicación personalizada.

### Selector de variables {#variable-picker}

La lista Selector de variables proporciona variables útiles que puede arrastrar y soltar en los cuadros Asunto o Plantilla de notificación. Cuando se coloca una variable en los cuadros Asunto o Plantilla de notificación, esta cambia al nombre de la variable de flujo de trabajo de los formularios reales con dos símbolos @ a ambos lados, por ejemplo, `@@taskid@@`.

Para recordatorios, asignaciones de tareas y fechas límite para usuarios y grupos, puede utilizar las siguientes variables en los cuadros Asunto y Plantilla de notificación:

**descripción** El contenido de la propiedad Description, tal como se define en el paso del usuario (punto de inicio, operación Assign Task o operación Assign Multiple Tasks) del proceso en Workbench.

**instrucciones** El contenido de la propiedad Instrucciones de tarea, tal como se define en el paso de usuario del proceso en Workbench.

**notification-host** El nombre de host del servidor de aplicaciones de AEM forms .

**process-name** Nombre del proceso.

**operation-name** Nombre del paso.

**taskid** Identificador único de la tarea actual.

**acciones** Genera una lista numerada de rutas válidas (por ejemplo, Aprobar, Rechazar) en las que el destinatario puede hacer clic.

Además, para recordatorios de grupo, asignaciones de tareas de grupo y fechas límite de grupo, también puede utilizar:

**group-name** Nombre del grupo al que se asigna el elemento de trabajo.

>[!NOTE]
>
>Si una variable no tiene valor, no se devuelve nada.

Para ramas interrumpidas, puede utilizar las siguientes variables en los cuadros Asunto y Plantilla de notificación:

**branch-id** Identificador de rama.

**process-id** Identificador de instancia de proceso.

**notification-host** El nombre de host del servidor de aplicaciones de AEM forms .

Para las operaciones interrumpidas, puede utilizar las siguientes variables en los cuadros Asunto y Plantilla de notificación:

**action-id** Identificador de la operación.

**branch-id** Identificador de rama.

**process-id** Identificador de instancia de proceso.

**notification-host** El nombre de host del servidor de aplicaciones de AEM forms .

### Uso de una variable en el cuadro Asunto {#using-a-variable-in-the-subject-box}

Si escribe el siguiente texto en el cuadro Asunto para las notificaciones de asignación de tareas:

`Please complete task @@taskid@@`

El usuario recibe un mensaje de correo electrónico con el siguiente asunto si se le asigna la tarea 376:

`Please complete task 376`

### Uso de variables en el cuadro Plantilla de notificación {#using-variables-in-the-notification-template-box}

Si escribe el siguiente texto en el cuadro Plantilla de notificación para notificaciones de bifurcación paralizada:

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

El administrador recibe un mensaje de correo electrónico que contiene el siguiente contenido si el número de rama es 4868 y el nombre del servidor es `ServerXYZ`:

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## Configuración de las conexiones de supervisión de actividades comerciales {#configuring-business-activity-monitoring-connections}

La supervisión de la actividad empresarial, módulo opcional, proporciona un conjunto de paneles operativos que proporcionan visibilidad en tiempo real de sus operaciones y de los indicadores clave de rendimiento.

En la página Configuración de BAM , configure las conexiones al servidor que ejecuta BAM para que se puedan rastrear y transmitir a ese servidor los eventos relacionados con el proceso.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de Forms > Configuración del servidor > Configuración de BAM.
1. En el cuadro Host de BAM, escriba el nombre del servidor que ejecuta BAM. El valor predeterminado es localhost.
1. En el cuadro Puerto de BAM, escriba el puerto que se utilizará para conectar con el servidor que ejecuta BAM. El puerto predeterminado de BAM para JBoss es 8080, WebLogic es 7001 y WebSphere es 9080.
1. En el cuadro Host de servidor, escriba el nombre o la dirección IP del servidor de formularios de host. El valor predeterminado es localhost.
1. En el cuadro Puerto del servidor, escriba el número de puerto utilizado por el servidor de formularios.
1. En los cuadros Nombre de usuario y Contraseña, escriba el ID de usuario y la contraseña correspondientes para acceder al servidor de BAM. El nombre de usuario predeterminado es CognosNowAdmin y la contraseña predeterminada es manager.
1. Haga clic en Guardar.
