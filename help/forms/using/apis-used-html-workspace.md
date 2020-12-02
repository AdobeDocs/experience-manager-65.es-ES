---
title: API utilizadas en el espacio de trabajo de AEM Forms
seo-title: API utilizadas en el espacio de trabajo de AEM Forms
description: API públicas de Java y JavaScript y métodos del espacio de trabajo de LiveCycle AEM Forms, expuestos para personalización y automatización.
seo-description: API públicas de Java y JavaScript y métodos del espacio de trabajo de LiveCycle AEM Forms, expuestos para personalización y automatización.
uuid: 9602990e-8ac7-42eb-b507-50b3594055ba
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 4a73a973-fccf-466b-b4a0-47652a14a080
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 1%

---


# API utilizadas en el espacio de trabajo de AEM Forms {#apis-used-in-aem-forms-workspace}

Las siguientes API se utilizan en el espacio de trabajo de AEM Forms.

<table>
 <tbody>
  <tr>
   <td><strong>Método Javascript</strong></td>
   <td><strong>Nombre de servicio</strong></td>
   <td><strong>Nombre de API</strong></td>
   <td><strong>Comentarios</strong></td>
  </tr>
  <tr>
   <td>getGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getGroups</td>
   <td>Busca grupos. devuelve una lista de todos los grupos si no se ha especificado nada; de lo contrario, devuelve grupos con el nombre especificado.</td>
  </tr>
  <tr>
   <td>getUsersAndGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersAndGroups</td>
   <td>Busca usuarios y grupos. Devuelve una lista de todos los usuarios y grupos, si no se especifica nada, devuelve usuarios y grupos con el nombre especificado.</td>
  </tr>
  <tr>
   <td>prepareForSubmit</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>prepareForSubmit</td>
   <td>Se llama antes de enviar el formulario mediante DocumentSubmitServlet. Establece la ID de tarea en una variable de sesión (junto con la hora de caducidad) que se recupera durante el envío real.</td>
  </tr>
  <tr>
   <td>submitTask</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>submit</td>
   <td>Envía el objeto de documento asociado a una tarea (y a su vez envía el proceso).</td>
  </tr>
  <tr>
   <td>getRootEndpointCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getRootEndpointCategories</td>
   <td>Recupera todas las categorías raíz presentes en el servidor.</td>
  </tr>
  <tr>
   <td>getDirectChildCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getDirectChildCategories2</td>
   <td>Busca todos los niños directos para una categoría.</td>
  </tr>
  <tr>
   <td>getAllStartpoints</td>
   <td>ProcessManagementStartpointService</td>
   <td>getAllStartpoints</td>
   <td>Recupera todos los puntos de partida presentes en el servidor bajo todas las categorías.</td>
  </tr>
  <tr>
   <td>invokeStartpoint</td>
   <td>ProcessManagementStartpointService</td>
   <td>invokeStartpoint</td>
   <td>Esto invoca un punto de inicio y crea una nueva tarea correspondiente a un punto de inicio</td>
  </tr>
  <tr>
   <td>getAllTasks</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllActionableTasks</td>
   <td>Recupera todas las tareas que se crean y reenvían o consultan, guardan, asignan, asignan y guardan para el usuario que ha iniciado sesión.</td>
  </tr>
  <tr>
   <td>getTask</td>
   <td>ProcessManagementTaskService</td>
   <td>getTask</td>
   <td>Busca una tarea específica.</td>
  </tr>
  <tr>
   <td>outputTask</td>
   <td>ProcessManagementTaskService</td>
   <td>procesar</td>
   <td>Procesa una tarea y devuelve la información necesaria para procesar el formulario, como la dirección URL del formulario, el tipo de formulario, la dirección URL de los datos, si es necesario, etc.</td>
  </tr>
  <tr>
   <td>submitWithPreviousData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithPreviousData</td>
   <td>Devuelve el resultado de la API de envío de TaskManager mediante la clave de resultado.</td>
  </tr>
  <tr>
   <td>submitWithData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithData</td>
   <td>Envía los datos del formulario (pasados como cadena) asociados con la tarea mediante la API de envío de TaskManager. Se utiliza para formularios flexibles que no llaman a la API de envío de TaskManager.</td>
  </tr>
  <tr>
   <td>save</td>
   <td>ProcessManagementTaskService</td>
   <td>guardar</td>
   <td>Guarda una tarea en el servidor.</td>
  </tr>
  <tr>
   <td>complete</td>
   <td>ProcessManagementTaskService</td>
   <td>complete</td>
   <td>Finaliza una tarea y la tarea se pasa al siguiente paso según el diseño del proceso.</td>
  </tr>
  <tr>
   <td>getAttachment</td>
   <td>ProcessManagementTaskService</td>
   <td>getAttachment</td>
   <td>Devuelve la dirección URL de un archivo adjunto en el que está disponible.</td>
  </tr>
  <tr>
   <td>getAllAttachments</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllActionableAttachments</td>
   <td>Recupera todos los archivos adjuntos y notas de una tarea.</td>
  </tr>
  <tr>
   <td>compartir</td>
   <td>ProcessManagementTaskService</td>
   <td>compartir</td>
   <td>Comparte una tarea con otro usuario. Otro usuario puede reclamar la tarea y convertirse en propietario de la tarea.</td>
  </tr>
  <tr>
   <td>adelante</td>
   <td>ProcessManagementTaskService</td>
   <td>adelante</td>
   <td>Reenvía una tarea a otro usuario.</td>
  </tr>
  <tr>
   <td>consulta</td>
   <td>ProcessManagementTaskService</td>
   <td>consulta</td>
   <td>Consulta una tarea con otro usuario.</td>
  </tr>
  <tr>
   <td>reclamar</td>
   <td>ProcessManagementTaskService</td>
   <td>reclamar</td>
   <td>Afirma que hay una tarea disponible en la cola compartida.</td>
  </tr>
  <tr>
   <td>desbloquear</td>
   <td>ProcessManagementTaskService</td>
   <td>desbloquear</td>
   <td>Desbloquea una tarea.</td>
  </tr>
  <tr>
   <td>bloquear</td>
   <td>ProcessManagementTaskService</td>
   <td>bloquear</td>
   <td>Bloquea una tarea y otro usuario no puede reclamar la tarea si se comparte.</td>
  </tr>
  <tr>
   <td>rechazar</td>
   <td>ProcessManagementTaskService</td>
   <td>rechazar</td>
   <td>Devuelve la tarea al propietario anterior de la tarea.</td>
  </tr>
  <tr>
   <td>abandono</td>
   <td>ProcessManagementTaskService</td>
   <td>abandono</td>
   <td>Elimina una tarea.</td>
  </tr>
  <tr>
   <td>setVisibility</td>
   <td>ProcessManagementTaskService</td>
   <td>setVisibility</td>
   <td>Establece la visibilidad de una tarea. Si la visibilidad se establece en false, la tarea no será visible para el usuario posteriormente.</td>
  </tr>
  <tr>
   <td>getUsers</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsers</td>
   <td>Se utiliza para buscar usuarios. Devuelve todos los usuarios si no se especifica ningún nombre, de lo contrario, devuelve los usuarios con un nombre especificado.</td>
  </tr>
  <tr>
   <td>getUsersInGroup</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersInGroupByName</td>
   <td>Devuelve todos los usuarios de un grupo.</td>
  </tr>
  <tr>
   <td>GrantQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>GrantQueueAccess</td>
   <td>Otorga al usuario especificado acceso a la cola del usuario que ha iniciado sesión. Básicamente está compartiendo su propia cola con otro usuario.</td>
  </tr>
  <tr>
   <td>requestQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>requestQueueAccess</td>
   <td>Realiza una solicitud de acceso de la cola del usuario especificado para el usuario que ha iniciado sesión. Si el usuario aprueba la solicitud, la cola del usuario se comparte con el usuario que ha iniciado sesión.</td>
  </tr>
  <tr>
   <td>getGrantedUsers</td>
   <td>ProcessManagementQueueService</td>
   <td>getGrantedUsers</td>
   <td>Devuelve todos los usuarios que tienen acceso a la cola del usuario que ha iniciado sesión.</td>
  </tr>
  <tr>
   <td>getUsersForAccessibleQueues</td>
   <td>ProcessManagementQueueService</td>
   <td>getUsersForAccessibleQueues</td>
   <td>Devuelve todos los usuarios a los que un usuario tiene acceso a la cola.</td>
  </tr>
  <tr>
   <td>revokeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>revokeQueueAccess</td>
   <td>Elimina a un usuario de la lista de usuarios que tienen acceso a la cola del usuario que ha iniciado sesión.</td>
  </tr>
  <tr>
   <td>removeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>removeQueueAccess</td>
   <td>Elimina un usuario de la lista de usuarios a los que el usuario que ha iniciado sesión puede acceder a la cola.</td>
  </tr>
  <tr>
   <td>getAllQueues<br /> </td>
   <td>ProcessManagementQueueService<br /> </td>
   <td>getAllQueues<br /> </td>
   <td>Obtiene todas las colas (propias, compartidas y de grupo) accesibles para el usuario que ha iniciado sesión.<br /> </td>
  </tr>
  <tr>
   <td>getOutOfOfficeSettings</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>getOutOfOfficeSettings</td>
   <td>Se sale de la configuración de oficina de un usuario.</td>
  </tr>
  <tr>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>Guarda la configuración de un usuario fuera de la oficina.</td>
  </tr>
  <tr>
   <td>getAllProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getAllProcesses</td>
   <td>Devuelve la lista de todos los procesos.</td>
  </tr>
  <tr>
   <td>getParticipatedProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getParticipatedProcesses</td>
   <td>Devuelve la lista de todos los nombres de proceso que participaron los usuarios que iniciaron sesión.</td>
  </tr>
  <tr>
   <td>getProcessInstance<br /> </td>
   <td>ProcessManagementProcessService<br /> </td>
   <td>getProcessInstance<br /> </td>
   <td>Obtiene detalles de una instancia de proceso.<br /> </td>
  </tr>
  <tr>
   <td>getProcessInstances</td>
   <td>ProcessManagementQueryService</td>
   <td>getProcessInstances</td>
   <td>Recupera todas las instancias de proceso de un proceso.</td>
  </tr>
  <tr>
   <td>getpendingTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getpendingTasksForProcessInstance</td>
   <td>Obtiene tareas pendientes para una instancia de proceso.</td>
  </tr>
  <tr>
   <td>getTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getTasksForProcessInstance</td>
   <td>Obtiene todas las tareas de una instancia de proceso.</td>
  </tr>
  <tr>
   <td>getAllSearchTemplates</td>
   <td>ProcessManagementQueryService</td>
   <td>getAllSearchTemplates</td>
   <td>Devuelve la lista de todas las plantillas de búsqueda.</td>
  </tr>
  <tr>
   <td>getTemplate</td>
   <td>ProcessManagementQueryService</td>
   <td>getTemplate</td>
   <td>Devuelve el contenido de una plantilla de búsqueda.</td>
  </tr>
  <tr>
   <td>findTasksJson<br /> </td>
   <td>ProcessManagementQueryService</td>
   <td>findTasksJson</td>
   <td>Busca y devuelve todas las tareas que cumplen todas las condiciones de una plantilla de búsqueda.</td>
  </tr>
  <tr>
   <td>getAssignmentsForTask</td>
   <td>ProcessManagementTaskService</td>
   <td>getAssignmentsForTask</td>
   <td>Obtiene todas las asignaciones para una tarea. Por ejemplo:- Si el usuario reenvía o consulta una tarea con otro usuario, entonces es una asignación para una tarea.</td>
  </tr>
  <tr>
   <td>deleteAttachment </td>
   <td>TaskManagerService</td>
   <td>deleteAttachment</td>
   <td>Elimina un archivo adjunto.</td>
  </tr>
  <tr>
   <td>initialize</td>
   <td>ProcessManagementClientSessionService</td>
   <td>initialize</td>
   <td>De ser necesario, renueva la afirmación. Autentica al usuario. Establece los parámetros de sesión para la información de servidor y cliente. Devuelve la información del usuario y el intervalo de sondeo.</td>
  </tr>
  <tr>
   <td>getTasksForDirectReports</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getTasksForDirectReports</td>
   <td>Devuelve todas las tareas de los informes directos del administrador de inicio de sesión.</td>
  </tr>
  <tr>
   <td>getTaskOfDirectReport<br /> </td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getDirectReportTask</td>
   <td>Devuelve la tarea del informe directo especificado del administrador de inicio de sesión.</td>
  </tr>
  <tr>
   <td>forwardTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>forwardTaskOfDirectReport</td>
   <td>Reenvía una tarea de un informe directo a otro usuario.</td>
  </tr>
  <tr>
   <td>rechacarTareaDeDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>rechacarTareaDeDirectReport</td>
   <td>Devuelve una tarea de un informe directo al usuario anterior.</td>
  </tr>
  <tr>
   <td>getProperty</td>
   <td>WorkspacePropertyService</td>
   <td>getProperty</td>
   <td>Obtiene una propiedad Workspace para un usuario.</td>
  </tr>
  <tr>
   <td>removeProperty</td>
   <td>WorkspacePropertyService</td>
   <td>delete</td>
   <td>Elimina una propiedad Workspace para un usuario.</td>
  </tr>
  <tr>
   <td>getProperties</td>
   <td>WorkspacePropertyService</td>
   <td>getPropertiesAsMap</td>
   <td>Devuelve todas las propiedades de Workspace de un usuario.</td>
  </tr>
  <tr>
   <td>setProperty</td>
   <td>WorkspacePropertyService</td>
   <td>setProperty</td>
   <td>Establece una propiedad Workspace para un usuario.</td>
  </tr>
  <tr>
   <td>getCurrentUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getCurrentUserImageUrl</td>
   <td>Obtiene la dirección URL de imagen del usuario para el usuario que ha iniciado sesión.</td>
  </tr>
  <tr>
   <td>getUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getUserImageUrl</td>
   <td>Obtiene la dirección URL de imagen del usuario para un usuario especificado.</td>
  </tr>
  <tr>
   <td>uploadNote</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadNote</td>
   <td>Carga una nota en el servidor para una tarea.</td>
  </tr>
  <tr>
   <td>uploadRMAToServer (también se llama directamente desde la plantilla html)<br /> </td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadAttachment</td>
   <td>Carga un archivo adjunto en el servidor para una tarea.</td>
  </tr>
  <tr>
   <td>getImageURL (también se llama directamente desde una plantilla html)</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>getImage</td>
   <td>Obtiene la imagen para un proceso.</td>
  </tr>
 </tbody>
</table>
