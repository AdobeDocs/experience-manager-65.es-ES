---
title: Flujos de trabajo de Forms JEE | Gestión de datos de usuario
seo-title: Forms JEE workflows | Handling user data
description: Flujos de trabajo de Forms JEE | Gestión de datos de usuario
uuid: 3b06ef19-d3c4-411e-9530-2c5d2159b559
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5632a8df-a827-4e38-beaa-18b61c2208a3
role: Admin
exl-id: 847fa303-8d1e-4a17-b90d-5f9da5ca2d77
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 3%

---

# Flujos de trabajo de Forms JEE | Gestión de datos de usuario {#forms-jee-workflows-handling-user-data}

Los flujos de trabajo JEE de AEM Forms proporcionan herramientas para diseñar, crear y administrar procesos empresariales. Un proceso de flujo de trabajo consiste en una serie de pasos que se ejecutan en un orden especificado. Cada paso realiza una acción específica, como asignar una tarea a un usuario o enviar un mensaje de correo electrónico. Un proceso puede interactuar con recursos, cuentas de usuario y servicios, y se puede activar mediante cualquiera de los métodos siguientes:

* Inicio de un proceso desde AEM Forms Workspace
* Uso del servicio SOAP o RESTful
* Envío de un formulario adaptable
* El uso de la carpeta vigilada
* Uso del correo electrónico

Para obtener más información sobre la creación del proceso de flujo de trabajo JEE de AEM Forms, consulte [Ayuda de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_65).

## Almacenamiento de datos y datos de usuarios {#user-data-and-data-stores}

Cuando se activa un proceso y a medida que avanza, captura datos sobre los participantes en el proceso, datos introducidos por los participantes en el formulario asociado al proceso y datos adjuntos agregados al formulario. Los datos se almacenan en la base de datos del servidor JEE de AEM Forms y, si se configuran, algunos datos, como los archivos adjuntos, se almacenan en el directorio Global Document Storage (GDS). El directorio GDS se puede configurar en un sistema de archivos compartido o en una base de datos.

## Acceso y eliminación de datos de usuario {#access-and-delete-user-data}

Cuando se activa un proceso, se genera un ID de instancia de proceso único y un ID de invocación de larga duración que se asocian a la instancia de proceso. Puede acceder a los datos y eliminarlos para una instancia de proceso en función del ID de invocación de larga duración. Puede deducir el ID de invocación de larga duración de una instancia de proceso con el nombre de usuario del iniciador del proceso o los participantes en el proceso que han enviado sus tareas.

Sin embargo, no se puede identificar el ID de instancia de proceso para un iniciador en los siguientes casos:

* **Proceso activado a través de una carpeta vigilada**: Una instancia de proceso no se puede identificar con su iniciador si el proceso se activa mediante una carpeta vigilada. En este caso, la información del usuario se codifica en los datos almacenados.
* **Proceso iniciado desde la instancia de AEM de publicación**: Todas las instancias de proceso activadas desde AEM instancia de publicación no capturan información sobre el iniciador. Sin embargo, los datos de usuario se pueden capturar en el formulario asociado al proceso, que se almacena en variables de flujo de trabajo.
* **Proceso iniciado mediante correo electrónico**: El ID de correo electrónico del remitente se captura como una propiedad en una columna de blob opaco del `tb_job_instance` base de datos, que no se pueden consultar directamente.

### Identifique los ID de instancia de proceso cuando se conozca el iniciador o participante del flujo de trabajo {#initiator-participant}

Realice los siguientes pasos para identificar los ID de instancia de proceso para un iniciador de flujo de trabajo o un participante:

1. Ejecute el siguiente comando en la base de datos del servidor de AEM Forms para recuperar el ID principal del iniciador o participante del flujo de trabajo desde el `edcprincipalentity` tabla de base de datos.

   ```sql
   select id from edcprincipalentity where canonicalname='user_ID'
   ```

   La consulta devuelve el ID principal del `user_ID`.

1. (**Para el iniciador del flujo de trabajo**) Ejecute el siguiente comando para recuperar todas las tareas asociadas con el ID principal para el iniciador desde el `tb_task` tabla de base de datos.

   ```sql
   select * from tb_task where start_task = 1 and create_user_id= 'initiator_principal_id'
   ```

   La consulta devuelve tareas iniciadas por el `initiator`_ `principal_id`. Las tareas son de dos tipos:

   * **Tareas completadas**: Estas tareas se han enviado y muestran un valor alfanumérico en la variable `process_instance_id` campo . Tome nota de todos los ID de instancia de proceso para las tareas enviadas y continúe con los pasos.
   * **Tareas iniciadas pero no finalizadas**: Estas tareas se han iniciado pero aún no se han enviado. El valor de la variable `process_instance_id` el campo para estas tareas es **0** (cero). En este caso, tome nota de los ID de tarea correspondientes y consulte [Trabajo con tareas huérfanas](#orphan).

1. (**Para participantes de flujo de trabajo**) Ejecute el siguiente comando para recuperar los ID de instancia de proceso asociados al ID principal del participante del proceso para el iniciador desde el `tb_assignment` tabla de base de datos.

   ```sql
   select distinct a.process_instance_id from tb_assignment a join tb_queue q on a.queue_id = q.id where q.workflow_user_id='participant_principal_id'
   ```

   La consulta devuelve ID de instancia para todos los procesos asociados con el participante, incluidos aquellos en los que el participante no ha enviado ninguna tarea.

   Tome nota de todos los ID de instancia de proceso para las tareas enviadas y continúe con los pasos.

   Para tareas huérfanas o tareas en las que `process_instance_id` es 0 (cero), tome nota de los ID de tarea correspondientes y consulte [Trabajo con tareas huérfanas](#orphan).

1. Siga las instrucciones indicadas en [Purgar los datos de usuario de las instancias de flujo de trabajo en función de los ID de instancia de proceso](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) para eliminar los datos de usuario de los ID de instancia de proceso identificados.

### Identificar los ID de instancia de proceso cuando los datos de usuario se almacenan en variables primitivas {#primitive}

Se puede diseñar un flujo de trabajo de modo que los datos del usuario se capturen en una variable que se almacene como un blob en la base de datos. En estos casos, los datos de usuario solo se pueden consultar si están almacenados en una de las siguientes variables de tipo primitivo:

* **Cadena**: Contiene el ID de usuario directamente o como subcadena y se puede consultar mediante SQL.
* **Numérico**: Contiene el ID de usuario directamente.
* **XML**: Contiene el ID de usuario como una subcadena dentro del texto almacenado como columnas de texto en la base de datos y se puede consultar como cadenas.

Realice los siguientes pasos para determinar si un flujo de trabajo que almacena datos en variables de tipo primitivo contiene datos para el usuario:

1. Ejecute el siguiente comando de base de datos:

   ```sql
   select database_table from omd_object_type where name='pt_<app_name>/<workflow_name>'
   ```

   La consulta devuelve un nombre de tabla en `tb_<number>` para la aplicación especificada ( `app_name`) y flujo de trabajo ( `workflow_name`).

   >[!NOTE]
   >
   >El valor de la variable `name` puede ser compleja si el flujo de trabajo está anidado en subcarpetas dentro de la aplicación. Asegúrese de especificar la ruta completa exacta al flujo de trabajo, que puede obtener de la variable `omd_object_type` tabla de base de datos.

1. Consulte la `tb_<number>` esquema de tabla. La tabla contiene variables que almacenan datos de usuario para el flujo de trabajo especificado. Las variables de la tabla corresponden a las variables del flujo de trabajo.

   Identifique y tome nota de la variable que corresponde a la variable de flujo de trabajo que contiene el ID de usuario. Si la variable identificada es de tipo primitivo, puede ejecutar una consulta para determinar las instancias de flujo de trabajo asociadas a un ID de usuario.

1. Ejecute el siguiente comando de base de datos. En este comando, la variable `user_var` es la variable de tipo primitivo que contiene el ID de usuario.

   ```sql
   select process_instance_id from <tb_name> where <user_var>=<user_ID>
   ```

   La consulta devuelve todos los ID de instancia de proceso asociados con el `user_ID`.

1. Siga las instrucciones indicadas en [Purgar los datos de usuario de las instancias de flujo de trabajo en función de los ID de instancia de proceso](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) para eliminar los datos de usuario de los ID de instancia de proceso identificados.

### Purgar los datos de usuario de las instancias de flujo de trabajo en función de los ID de instancia de proceso {#purge}

Ahora que ha identificado los ID de instancia de proceso asociados a un usuario, haga lo siguiente para eliminar los datos de usuario de las instancias de proceso correspondientes.

1. Ejecute el siguiente comando para recuperar el ID de invocación de larga duración y el estado de una instancia de proceso desde el `tb_process_instance` tabla.

   ```sql
   select long_lived_invocation_id, status from tb_process_instance where id='process_instance_id'
   ```

   La consulta devuelve el ID de invocación de larga duración y el estado del `process_instance_id`.

1. Crear una instancia del público `ProcessManager` cliente ( `com.adobe.idp.workflow.client.ProcessManager`) usando un `ServiceClientFactory` con la configuración de conexión correcta.

   Para obtener más información, consulte Referencia de API de Java para [Class ProcessManager](https://helpx.adobe.com/experience-manager/6-3/forms/ProgramLC/javadoc/com/adobe/idp/workflow/client/ProcessManager.html).

1. Compruebe el estado de la instancia de flujo de trabajo. Si el estado es distinto de 2 (COMPLETE) o 4 (TERMINATED), termine la instancia primero llamando al siguiente método:

   `ProcessManager.terminateProcess(<long_lived_invocation_id>)`.

1. Purgue la instancia del flujo de trabajo llamando al siguiente método:

   `ProcessManager.purgeProcessInstance(<long_lived_invocation_id>)`

   La variable `purgeProcessInstance` elimina completamente todos los datos del ID de invocación especificado de la base de datos del servidor de AEM Forms y GDS, si están configurados.

### Trabajo con tareas huérfanas {#orphan}

Las tareas huérfanas son las tareas cuyo proceso contiene se ha iniciado pero aún no se ha enviado. en este caso, la variable `process_instance_id` es **0** (cero). Por lo tanto, no se pueden rastrear los datos de usuario almacenados para tareas huérfanas mediante ID de instancias de proceso. Sin embargo, puede rastrearlo con el ID de la tarea para una tarea huérfana. Puede identificar los ID de tareas desde la variable `tb_task` para un usuario como se describe en [Identifique los ID de instancia de proceso cuando se conozca el iniciador o participante del flujo de trabajo](/help/forms/using/forms-workflow-jee-handling-user-data.md#initiator-participant).

Una vez que tenga los ID de la tarea, haga lo siguiente para depurar los archivos y datos asociados con una tarea huérfana de GDS y de la base de datos.

1. Ejecute el siguiente comando en la base de datos del servidor de AEM Forms para recuperar los ID de las tareas identificadas.

   ```sql
   select id from tb_form_data where task_id=<task_id>
   ```

   La consulta devuelve una lista de ID. Para cada ID ( `fd_id`) que se devuelve en los resultados, cree una lista de cadenas de ID de sesión de la siguiente manera:

   * _ `wfattach<task_id>`
   * `_wftask<fd_id>`
   * `_wftaskformid<fd_id>`

1. Dependiendo de si el GDS apunta a un sistema de archivos o a una base de datos, realice uno de los siguientes pasos:

   1. **GDS en el sistema de archivos**

      En el sistema de archivos GDS:

      1. Busque archivos con las siguientes cadenas de ID de sesión como extensiones:
      * `_wfattach<task_id>`
      * `_wftask<fd_id>`
      * `_wftaskformid<fd_id>`

      Los archivos con estas extensiones son los archivos de marcador. Se almacenan con nombres de archivo en el siguiente formato:

      `<file_name_guid>.session<session_id_string>`

      1. Elimine todos los archivos de marcador y otros archivos con el nombre de archivo exacto como `<file_name_guid>` del sistema de archivos.
   1. **GDS en la base de datos**

      Ejecute los siguientes comandos para cada ID de sesión:

      ```sql
      delete from tb_dm_chunk where documentid in (select documentid from tb_dm_session_reference where sessionid=<session_id>)
      delete from tb_dm_session_reference where sessionid=<session_id>
      delete from tb_dm_deletion where sessionid=<session_id>
      ```




1. Ejecute los siguientes comandos para eliminar los datos de los ID de tareas de la base de datos del servidor de AEM Forms:

   ```sql
   delete from tb_task_acl where task_id=<task_id>
   delete from tb_task_attachment where task_id=<task_id>
   delete from tb_form_data where task_id=<task_id>
   delete from tb_assignment where task_id=<task_id>
   delete from tb_task where id=<task_id>
   ```
