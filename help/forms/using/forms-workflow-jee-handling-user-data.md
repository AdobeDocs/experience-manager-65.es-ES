---
title: Flujos de trabajo de Forms JEE| Gestión de datos de usuario
seo-title: Flujos de trabajo de Forms JEE| Gestión de datos de usuario
description: nulo
seo-description: nulo
uuid: 3b06ef19-d3c4-411e-9530-2c5d2159b559
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5632a8df-a827-4e38-beaa-18b61c2208a3
translation-type: tm+mt
source-git-commit: 5831c173114a5a6f741e0721b55d85a583e52f78

---


# Flujos de trabajo de Forms JEE| Gestión de datos de usuario {#forms-jee-workflows-handling-user-data}

Los flujos de trabajo JEE de AEM Forms proporcionan herramientas para diseñar, crear y administrar procesos empresariales. Un proceso de flujo de trabajo consiste en una serie de pasos que se ejecutan en un orden especificado. Cada paso realiza una acción específica, como asignar una tarea a un usuario o enviar un mensaje de correo electrónico. Un proceso puede interactuar con recursos, cuentas de usuario y servicios, y se puede activar mediante cualquiera de los siguientes métodos:

* Inicio de un proceso desde AEM Forms Workspace
* Uso del servicio SOAP o RESTful
* Envío de un formulario adaptable
* Uso de la carpeta vigilada
* Uso del correo electrónico

Para obtener más información sobre la creación del proceso de flujo de trabajo JEE de AEM Forms, consulte la Ayuda [de Workbench](http://www.adobe.com/go/learn_aemforms_workbench_65).

## Almacenes de datos y datos de usuarios {#user-data-and-data-stores}

Cuando se activa un proceso y avanza, captura datos sobre los participantes en el proceso, datos introducidos por los participantes en el formulario asociado al proceso y datos adjuntos agregados al formulario. Los datos se almacenan en la base de datos del servidor JEE de AEM Forms y, si se configuran, algunos datos como los adjuntos se almacenan en el directorio Global Document Storage (GDS). El directorio GDS se puede configurar en un sistema de archivos compartido o en una base de datos.

## Acceso y eliminación de datos de usuario {#access-and-delete-user-data}

Cuando se activa un proceso, se genera un ID de instancia de proceso único y un ID de invocación de larga duración que se asocian a la instancia de proceso. Puede acceder y eliminar datos de una instancia de proceso en función del ID de invocación de larga duración. Puede deducir el ID de invocación de larga duración de una instancia de proceso con el nombre de usuario del iniciador del proceso o los participantes del proceso que han enviado sus tareas.

Sin embargo, no se puede identificar la ID de instancia de proceso para un iniciador en los siguientes casos:

* **Proceso activado mediante una carpeta** vigilada: No se puede identificar una instancia de proceso con su iniciador si el proceso se activa con una carpeta vigilada. En este caso, la información del usuario se codifica en los datos almacenados.
* **Proceso iniciado desde la instancia** de AEM de publicación: Todas las instancias de proceso activadas desde la instancia de publicación de AEM no capturan información sobre el iniciador. Sin embargo, los datos de usuario se pueden capturar en el formulario asociado al proceso, que se almacena en variables de flujo de trabajo.
* **Proceso iniciado por correo electrónico**: El ID de correo electrónico del remitente se captura como una propiedad en una columna de blob opaca de la tabla de la `tb_job_instance` base de datos, que no se puede consultar directamente.

### Identifique las ID de instancia de proceso cuando se conozca el iniciador o participante del flujo de trabajo {#initiator-participant}

Siga estos pasos para identificar los ID de instancia de proceso para un iniciador de flujo de trabajo o un participante:

1. Ejecute el siguiente comando en la base de datos del servidor de AEM Forms para recuperar el ID principal del iniciador o participante del flujo de trabajo de la tabla de la `edcprincipalentity` base de datos.

   ```sql
   select id from edcprincipalentity where canonicalname='user_ID'
   ```

   La consulta devuelve el identificador principal del `user_ID`objeto especificado.

1. (**Para el iniciador** del flujo de trabajo) Ejecute el siguiente comando para recuperar todas las tareas asociadas con el identificador principal del iniciador desde la tabla de la `tb_task` base de datos.

   ```sql
   select * from tb_task where start_task = 1 and create_user_id= 'initiator_principal_id'
   ```

   La consulta devuelve tareas iniciadas por el `initiator`_ `principal_id`especificado. Las tareas son de dos tipos:

   * **Tareas** completadas: Estas tareas se han enviado y muestran un valor alfanumérico en el `process_instance_id` campo. Tome nota de todos los ID de instancia de proceso para las tareas enviadas y continúe con los pasos.
   * **Tareas iniciadas pero no finalizadas**: Estas tareas se han iniciado pero aún no se han enviado. El valor en el `process_instance_id` campo para estas tareas es **0** (cero). En este caso, tome nota de los ID de tareas correspondientes y consulte [Trabajo con tareas](#orphan)huérfanas.

1. (**Para los participantes** del flujo de trabajo) Ejecute el siguiente comando para recuperar los ID de instancia de proceso asociados al ID principal del participante del proceso para el iniciador desde la tabla de la `tb_assignment` base de datos.

   ```sql
   select distinct a.process_instance_id from tb_assignment a join tb_queue q on a.queue_id = q.id where q.workflow_user_id='participant_principal_id'
   ```

   La consulta devuelve ID de instancia para todos los procesos asociados con el participante, incluidos aquellos en los que el participante no ha enviado ninguna tarea.

   Tome nota de todos los ID de instancia de proceso para las tareas enviadas y continúe con los pasos.

   Para las tareas huérfanas o las tareas en las que `process_instance_id` es 0 (cero), tome nota de los ID de tareas correspondientes y consulte [Trabajo con tareas](#orphan)huérfanas.

1. Siga las instrucciones de la sección [Depurar datos de usuario de instancias de flujo de trabajo en función de IDs](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) de instancias de proceso para eliminar datos de usuario de ID de instancias de proceso identificadas.

### Identifique las ID de instancia de proceso cuando los datos de usuario se almacenan en variables primitivas {#primitive}

Se puede diseñar un flujo de trabajo de modo que los datos del usuario se capturen en una variable que se almacene como blob en la base de datos. En estos casos, solo puede consultar los datos de usuario si están almacenados en una de las siguientes variables de tipo primitivo:

* **Cadena**: Contiene el ID de usuario directamente o como subcadena y se puede consultar mediante SQL.
* **Numérico**: Contiene el ID de usuario directamente.
* **XML**: Contiene el ID de usuario como una subcadena dentro del texto almacenado como columnas de texto en la base de datos y se puede consultar como cadenas.

Siga los pasos siguientes para determinar si un flujo de trabajo que almacena datos en variables de tipo primitivo contiene datos para el usuario:

1. Ejecute el siguiente comando de base de datos:

   ```sql
   select database_table from omd_object_type where name='pt_<app_name>/<workflow_name>'
   ```

   La consulta devuelve un nombre de tabla en `tb_<number>` formato para la aplicación ( `app_name`) y el flujo de trabajo ( `workflow_name`) especificados.

   >[!NOTE]
   >
   >El valor de la propiedad `name` puede ser complejo si el flujo de trabajo está anidado en subcarpetas dentro de la aplicación. Asegúrese de especificar la ruta completa exacta del flujo de trabajo, que puede obtener de la tabla de la `omd_object_type` base de datos.

1. Revise el esquema de la `tb_<number>` tabla. La tabla contiene variables que almacenan datos de usuario para el flujo de trabajo especificado. Las variables de la tabla corresponden a las variables del flujo de trabajo.

   Identifique y tome nota de la variable que corresponde a la variable de flujo de trabajo que contiene la ID de usuario. Si la variable identificada es de tipo primitivo, puede ejecutar una consulta para determinar las instancias de flujo de trabajo asociadas con un ID de usuario.

1. Ejecute el siguiente comando de base de datos. En este comando, `user_var` es la variable de tipo primitivo que contiene el ID de usuario.

   ```sql
   select process_instance_id from <tb_name> where <user_var>=<user_ID>
   ```

   La consulta devuelve todos los ID de instancia de proceso asociados con el `user_ID`.

1. Siga las instrucciones de la sección [Depurar datos de usuario de instancias de flujo de trabajo en función de IDs](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) de instancias de proceso para eliminar datos de usuario de ID de instancias de proceso identificadas.

### Purgar datos de usuario de instancias de flujo de trabajo en función de ID de instancias de proceso {#purge}

Ahora que ha identificado los ID de instancia de proceso asociados a un usuario, haga lo siguiente para eliminar los datos de usuario de las instancias de proceso correspondientes.

1. Ejecute el siguiente comando para recuperar el ID de invocación y el estado de larga duración de una instancia de proceso desde la `tb_process_instance` tabla.

   ```sql
   select long_lived_invocation_id, status from tb_process_instance where id='process_instance_id'
   ```

   La consulta devuelve el ID y el estado de invocación de larga duración para el `process_instance_id`.

1. Cree una instancia del cliente público `ProcessManager` ( `com.adobe.idp.workflow.client.ProcessManager`) utilizando una `ServiceClientFactory` instancia con la configuración de conexión correcta.

   Para obtener más información, consulte Referencia de API de Java para [Class ProcessManager](https://helpx.adobe.com/experience-manager/6-3/forms/ProgramLC/javadoc/com/adobe/idp/workflow/client/ProcessManager.html).

1. Compruebe el estado de la instancia de flujo de trabajo. Si el estado es distinto de 2 (COMPLETE) o 4 (TERMINADO), finalice la instancia primero llamando al siguiente método:

   `ProcessManager.terminateProcess(<long_lived_invocation_id>)`.

1. Purgue la instancia de workflow llamando al siguiente método:

   `ProcessManager.purgeProcessInstance(<long_lived_invocation_id>)`

   El `purgeProcessInstance` método elimina por completo todos los datos del ID de invocación especificado de la base de datos del servidor de AEM Forms y de GDS, si están configurados.

### Trabajar con tareas huérfanas {#orphan}

Las tareas huérfanas son las tareas cuyo proceso de contención se ha iniciado pero aún no se ha enviado. en este caso, el valor `process_instance_id` es **0** (cero). Por lo tanto, no se pueden rastrear los datos de usuario almacenados para tareas huérfanas mediante ID de instancia de proceso. Sin embargo, puede rastrearlo con el ID de tarea de una tarea huérfana. Puede identificar las ID de tareas de la `tb_task` tabla para un usuario, tal como se describe en [Identificar las ID de instancias de procesos cuando se conoce](/help/forms/using/forms-workflow-jee-handling-user-data.md#initiator-participant)al iniciador o participante del flujo de trabajo.

Una vez que tenga los ID de tarea, haga lo siguiente para depurar los archivos y datos asociados con una tarea huérfana de GDS y base de datos.

1. Ejecute el siguiente comando en la base de datos del servidor de AEM Forms para recuperar los ID de las tareas identificadas.

   ```sql
   select id from tb_form_data where task_id=<task_id>
   ```

   La consulta devuelve una lista de ID. Para cada ID ( `fd_id`) devuelto en los resultados, cree una lista de cadenas de ID de sesión de la siguiente manera:

   * _ `wfattach<task_id>`
   * `_wftask<fd_id>`
   * `_wftaskformid<fd_id>`

1. Según si el GDS apunta a un sistema de archivos o a una base de datos, realice uno de los siguientes pasos:

   1. **GDS en el sistema de archivos**

      En el sistema de archivos GDS:

      1. Busque archivos con las siguientes cadenas de ID de sesión como extensiones:
      * `_wfattach<task_id>`
      * `_wftask<fd_id>`
      * `_wftaskformid<fd_id>`
      Los archivos con estas extensiones son los archivos de marcador. Se almacenan con nombres de archivo en el siguiente formato:

      `<file_name_guid>.session<session_id_string>`

      1. Elimine todos los archivos de marcador y otros archivos con el nombre exacto `<file_name_guid>` del archivo del sistema de archivos.
   1. **GDS en la base de datos**

      Ejecute los siguientes comandos para cada ID de sesión:

      ```sql
      delete from tb_dm_chunk where documentid in (select documentid from tb_dm_session_reference where sessionid=<session_id>)
      delete from tb_dm_session_reference where sessionid=<session_id>
      delete from tb_dm_deletion where sessionid=<session_id>
      ```




1. Ejecute los siguientes comandos para eliminar datos de ID de tareas de la base de datos del servidor de AEM Forms:

   ```sql
   delete from tb_task_acl where task_id=<task_id>
   delete from tb_task_attachment where task_id=<task_id>
   delete from tb_form_data where task_id=<task_id>
   delete from tb_assignment where task_id=<task_id>
   delete from tb_task where id=<task_id>
   ```

