---
title: Descripción del objeto JSON del espacio de trabajo de AEM Forms
seo-title: Descripción del objeto JSON del espacio de trabajo de AEM Forms
description: Información conceptual sobre los objetos JavaScript JSON utilizados en el espacio de trabajo de LiveCycle AEM Forms para la personalización, extensión, modificación y reutilización.
seo-description: Información conceptual sobre los objetos JavaScript JSON utilizados en el espacio de trabajo de LiveCycle AEM Forms para la personalización, extensión, modificación y reutilización.
uuid: 91c923c8-144a-4453-ba91-6a5193f1c4c4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 61b7246d-ed28-4470-a0a2-a4aaf1a061a4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Descripción del objeto JSON del espacio de trabajo de AEM Forms {#aem-forms-workspace-json-object-description}

Los objetos JSON utilizados en el espacio de trabajo de AEM Forms se describen a continuación.

1. Categoría

   Las categorías están presentes en la ficha de inicio del proceso del espacio de trabajo. Estas categorías se utilizan para clasificar los puntos de partida.

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Solo cliente</strong></td>
   <td><strong>Comentarios</strong></td>
  </tr>
  <tr>
   <td>name</td>
   <td>F</td>
   <td>Nombre de la categoría</td>
  </tr>
  <tr>
   <td>id</td>
   <td>F</td>
   <td>Category ID<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>Descripción<br type="_moz" /> </td>
   <td>F</td>
   <td>Descripción de la categoría<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>parentOid<br type="_moz" /> </td>
   <td>F</td>
   <td>Contiene el identificador oid de la categoría principal<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>startPointsList<br type="_moz" /> </td>
   <td>T</td>
   <td>Contiene una lista de todos los puntos de partida presentes en una categoría</td>
  </tr>
  <tr>
   <td>categoryList</td>
   <td>T</td>
   <td>Contiene la lista de categorías secundarias directas de una categoría<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Todos los puntos de inicio y favoritos son categorías definidas en el lado del cliente. La categoría favorita contiene todos los puntos de inicio marcados por el usuario como favoritos. La categoría Todos los puntos de inicio contiene todos los puntos de inicio.

1. Punto de partida

   El punto de inicio se utiliza para iniciar un proceso desde el espacio de trabajo cuando se invoca.

   | **Propiedad** | **Solo cliente** | **Comentarios** |
   |---|---|---|
   | categoryId | F | Contiene la identificación de la categoría a la que pertenece el punto de partida. |
   | Descripción | F | Contiene la descripción de un punto de partida. |
   | name | F | Contiene el nombre del punto de partida. |
   | serializedImageTicket | F | Contiene un ticket de imagen correspondiente al punto de partida. Este ticket de imagen se utiliza en el campo imageUrl del punto de inicio para obtener la imagen del punto de inicio desde el servidor. |
   | serviceName | F | Contiene el nombre del servicio para startpoint. |
   | startpointId | F | Contiene la identificación de startpoint. |
   | isFavorite | T | Indica si el punto de inicio es el favorito o no. True si startpoint es el falso favorito. |
   | isDefaultImage | T | Indica si hay una imagen especificada para el proceso o no. True si no hay ninguna imagen asociada con el proceso else false. |
   | tarea | T | Contiene una tarea creada cuando se invoca startpoint. |
   | imageUrl | T | Contiene la dirección URL de la imagen correspondiente al punto de inicio. |

1. Tarea

   Las tareas se asignan a usuarios o grupos e incluyen una interfaz de usuario (un formulario o una guía (desaprobada)) que se puede rellenar con datos. Cuando a los usuarios se les asigna una tarea, se les proporciona el formulario o la Guía para completar y enviar.

<table>
 <tbody>
  <tr>
   <td>Propiedad<br /> </td>
   <td>Client Only<br /> </td>
   <td>Comentarios<br /> </td>
  </tr>
  <tr>
   <td>classOfTask</td>
   <td>F</td>
   <td>La clase de tarea es 'LC8' cuando la tarea es lc8 tarea else 'Standard'.<br /> </td>
  </tr>
  <tr>
   <td>completeTime<br /> </td>
   <td>F</td>
   <td>Contiene la marca de hora cuando se completa la tarea.<br /> </td>
  </tr>
  <tr>
   <td>queryGroupId<br /> </td>
   <td>F</td>
   <td>Contiene la ID de un grupo al que se puede consultar la tarea. Se configura durante el proceso de diseño.<br /> </td>
  </tr>
  <tr>
   <td>createTime<br /> </td>
   <td>F</td>
   <td>Contiene la marca de hora en la que se crea la tarea.<br /> </td>
  </tr>
  <tr>
   <td>creatingId<br /> </td>
   <td>F</td>
   <td>Contiene la identificación del usuario que creó la tarea.<br /> </td>
  </tr>
  <tr>
   <td>currentAssignment<br /> </td>
   <td>F</td>
   <td>Contiene detalles sobre la asignación actual de la tarea.<br /> </td>
  </tr>
  <tr>
   <td>fecha límite<br /> </td>
   <td>F</td>
   <td>Contiene la marca de hora en la que una tarea alcanzará su fecha límite.<br /> </td>
  </tr>
  <tr>
   <td>Descripción<br /> </td>
   <td>F</td>
   <td>Contiene una descripción de la tarea.<br /> </td>
  </tr>
  <tr>
   <td>displayName<br /> </td>
   <td>F</td>
   <td>Contiene el nombre para mostrar de la tarea.<br /> </td>
  </tr>
  <tr>
   <td>forwardGroupId<br /> </td>
   <td>F</td>
   <td>Contiene la ID de un grupo al que se puede reenviar la tarea. Se configura durante el proceso de diseño.<br /> </td>
  </tr>
  <tr>
   <td>instructions<br /> </td>
   <td>F</td>
   <td>Contiene instrucciones para una tarea.<br /> </td>
  </tr>
  <tr>
   <td>isLocked<br /> </td>
   <td>F</td>
   <td>True si la tarea está bloqueada.<br /> </td>
  </tr>
  <tr>
   <td>isMustOpenToComplete<br /> </td>
   <td>F</td>
   <td>True si se debe abrir el formulario de tareas para completar la tarea.<br /> </td>
  </tr>
  <tr>
   <td>isOpenFullScreen<br /> </td>
   <td>F</td>
   <td>Si el valor es true, al abrir la tarea, el formulario se muestra por primera vez en la pantalla completa.<br /> </td>
  </tr>
  <tr>
   <td>isRouteSelectionRequired<br /> </td>
   <td>F</td>
   <td>Si es true, se debe seleccionar route para completar la tarea.<br /> </td>
  </tr>
  <tr>
   <td>isShowAttachments<br /> </td>
   <td>F</td>
   <td>Los datos adjuntos se muestran si es true.<br /> </td>
  </tr>
  <tr>
   <td>isStartTask<br /> </td>
   <td>F</td>
   <td>Si es true, la tarea se crea desde el punto de inicio.<br /> </td>
  </tr>
  <tr>
   <td>isVisible<br /> </td>
   <td>F</td>
   <td>True si la tarea está visible en el espacio de trabajo.<br /> </td>
  </tr>
  <tr>
   <td>nextReminder<br /> </td>
   <td>F</td>
   <td>Marca de hora para el siguiente recordatorio.<br /> </td>
  </tr>
  <tr>
   <td>priority<br /> </td>
   <td>F</td>
   <td>Contiene la prioridad de la tarea.<br /> 1 = Prioridad<br /> más alta 2 = Prioridad<br /> alta 3 = Prioridad<br /> normal 4 = Prioridad<br /> baja 5 = PrioridadMás baja<br /> </td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>F</td>
   <td>Id. de la instancia de proceso de la que forma parte la tarea.<br /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br /> </td>
   <td>F</td>
   <td>Estado de la instancia de proceso de la tarea.<br /> </td>
  </tr>
  <tr>
   <td>recordatorioCount<br /> </td>
   <td>F</td>
   <td>Contiene un recuento de recordatorios para la tarea.<br /> </td>
  </tr>
  <tr>
   <td>routeList<br /> </td>
   <td>F</td>
   <td>Contiene una lista de rutas asociadas con la tarea. El usuario puede completar la tarea seleccionando cualquiera de las rutas de la lista de rutas.<br /> </td>
  </tr>
  <tr>
   <td>selectedRoute<br /> </td>
   <td>F</td>
   <td>Contiene el nombre de la ruta seleccionada cuando se completó la tarea.<br /> </td>
  </tr>
  <tr>
   <td>serializedImageTicket<br /> </td>
   <td>F</td>
   <td>Contiene un ticket de imagen correspondiente a la tarea. <br /> Este ticket de imagen se utiliza en el campo imageUrl de la tarea para obtener una imagen del servidor para la tarea. <br /> </td>
  </tr>
  <tr>
   <td>serviceName<br /> </td>
   <td>F</td>
   <td>Contiene el nombre del servicio para la tarea.<br /> </td>
  </tr>
  <tr>
   <td>serviceTitle<br /> </td>
   <td>F</td>
   <td>Contiene el título del servicio para la tarea.<br /> </td>
  </tr>
  <tr>
   <td>estado<br /> </td>
   <td>F</td>
   <td>1 = Creada (la tarea se crea desde el punto inicial).<br /> 2 = Creada y guardada (la tarea se crea desde el punto de inicio y se guarda).<br /> 3 = Asignada (la tarea se asigna al usuario una vez iniciado el proceso).<br /> 4 = Asignada y guardada (la tarea se asigna y se guarda).<br /> 100 = Completado (la tarea se ha completado).<br /> 101 = Fecha límite (la tarea ha alcanzado la fecha límite).<br /> 102 = Terminado<br /> </td>
  </tr>
  <tr>
   <td>stepName<br /> </td>
   <td>F</td>
   <td>Contiene el nombre del conjunto de tareas durante el diseño del proceso.<br /> </td>
  </tr>
  <tr>
   <td>summaryUrl<br /> </td>
   <td>F</td>
   <td>Contiene la dirección URL de resumen de la tarea.<br /> </td>
  </tr>
  <tr>
   <td>taskACL<br /> </td>
   <td>F</td>
   <td>Es una lista de control de acceso para una tarea.<br /> </td>
  </tr>
  <tr>
   <td>taskId<br /> </td>
   <td>F</td>
   <td>Id. de una tarea.<br /> </td>
  </tr>
  <tr>
   <td>updateTime<br /> </td>
   <td>F</td>
   <td>Marca de hora en la última actualización de la tarea.<br /> </td>
  </tr>
  <tr>
   <td>formUrl<br /> </td>
   <td>T</td>
   <td>Contiene la dirección URL del formulario para una tarea.<br /> </td>
  </tr>
  <tr>
   <td>taskFormType<br /> </td>
   <td>T</td>
   <td>Contiene el tipo de formulario de tarea. Con este campo, la tarea se procesa en el cliente como pdf para, swf form, etc.<br /> </td>
  </tr>
  <tr>
   <td>showDirectActions<br /> </td>
   <td>T</td>
   <td>Si es true, las acciones de ruta son visibles en el espacio de trabajo.<br /> </td>
  </tr>
  <tr>
   <td>showACLActions<br /> </td>
   <td>T</td>
   <td>Si el valor es true, las acciones como forward, query y share son visibles en el espacio de trabajo.<br /> </td>
  </tr>
  <tr>
   <td>supportOffline<br /> </td>
   <td>T</td>
   <td>Si el valor es true, el formulario se puede desconectar. Esto es solo para formularios PDF.<br /> </td>
  </tr>
  <tr>
   <td>supportSave<br /> </td>
   <td>T</td>
   <td>Si es true, el usuario puede guardar la tarea.<br /> </td>
  </tr>
  <tr>
   <td>readerSubmitOptions<br /> </td>
   <td>T</td>
   <td>Este objeto contiene opciones que se utilizan para enviar formularios PDF mediante un lector en caso de que el formulario PDF no contenga un botón de envío.<br /> </td>
  </tr>
  <tr>
   <td>isDefaultImage<br /> </td>
   <td>T</td>
   <td>Indica si hay una imagen especificada para el proceso o no. True si no hay ninguna imagen asociada con el proceso else false.<br /> </td>
  </tr>
  <tr>
   <td>historyTaskList<br /> </td>
   <td>T</td>
   <td>Contiene una lista de tareas que se utilizan en la ficha de historial de detalles de tareas.<br /> </td>
  </tr>
  <tr>
   <td>isOwner<br /> </td>
   <td>T</td>
   <td>True si el usuario que ha iniciado sesión es el propietario de la tarea.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands<br /> </td>
   <td>T</td>
   <td>Contiene todas las acciones que se pueden realizar en una tarea.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.directCommands<br /> </td>
   <td>T</td>
   <td>Contiene todas las acciones de ruta disponibles para una tarea.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.taskACLCommands<br /> </td>
   <td>T</td>
   <td>Contiene comandos como forward, share y query si están disponibles para una tarea.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.otherCommands<br /> </td>
   <td>T</td>
   <td>Contiene comandos como bloquear, desbloquear, abandonar, devolver, reclamar, etc., según esté disponible.<br /> </td>
  </tr>
  <tr>
   <td>processInstanceInfo<br /> </td>
   <td>T</td>
   <td>Contiene información sobre la instancia de proceso de la tarea.<br /> </td>
  </tr>
  <tr>
   <td>processVariables<br /> </td>
   <td>T<br /> </td>
   <td>Contiene una matriz de objetos de variables de proceso si están presentes.<br /> </td>
  </tr>
  <tr>
   <td>pendingTasks<br /> </td>
   <td>T</td>
   <td>Contiene una lista de tareas pendientes para la instancia de proceso de la tarea.<br /> </td>
  </tr>
  <tr>
   <td>userActions<br /> </td>
   <td>T</td>
   <td>Es una matriz de objetos. Cada objeto contiene detalles sobre la ruta y su correspondiente mensaje de confirmación, si está presente.<br /> </td>
  </tr>
  <tr>
   <td>dataUrl<br /> </td>
   <td>T</td>
   <td>Es la dirección URL para los datos de la forma de una tarea.<br /> </td>
  </tr>
  <tr>
   <td>externalAppConfig<br /> </td>
   <td>T</td>
   <td>Esta es la configuración para formularios de aplicaciones de terceros.<br /> </td>
  </tr>
  <tr>
   <td>submitted<br /> </td>
   <td>T</td>
   <td>True si se envía la tarea.<br /> </td>
  </tr>
  <tr>
   <td>attachments<br /> </td>
   <td>T</td>
   <td>Lista de datos adjuntos de una tarea.<br /> </td>
  </tr>
  <tr>
   <td>asignaciones<br /> </td>
   <td>T</td>
   <td>Lista de asignaciones de una tarea.<br /> </td>
  </tr>
 </tbody>
</table>

1. Filtro

   El filtro es básicamente la cola de usuario o grupo. Cuando se asigna una tarea al usuario o grupo, la tarea se agrega a la cola correspondiente.

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Solo cliente</strong></td>
   <td><strong>Comentarios</strong></td>
  </tr>
  <tr>
   <td>isDefault <br type="_moz" /> </td>
   <td>F</td>
   <td>True si la cola es la cola predeterminada del usuario que ha iniciado sesión, en caso contrario false.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>name<br type="_moz" /> </td>
   <td>F</td>
   <td>Nombre del propietario de la cola.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>qid</td>
   <td>F</td>
   <td>Id de la cola.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>tipo</td>
   <td>F</td>
   <td>Contiene el tipo de la cola.<br /> 0 - Cola de usuarios.<br /> 1. Cola compartida.<br /> 2. Cola de grupo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>query</td>
   <td>T</td>
   <td>Contiene una consulta asociada a un filtro. Esta consulta se utiliza para buscar tareas desde la lista de tareas completa.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>tareas</td>
   <td>T</td>
   <td>Contiene una lista de todas las tareas que pertenecen a un filtro.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Fuera de servicio

   Puede administrar la programación fuera de la oficina y controlar el flujo de tareas asignadas en caso de ausencia.

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong><br type="_moz" /> </td>
   <td><strong>Solo cliente</strong><br type="_moz" /> </td>
   <td><strong>Comentarios</strong><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>dateRanges<br type="_moz" /> </td>
   <td>F</td>
   <td>Contiene objetos de matriz de programaciones fuera de la oficina de un usuario. En cada objeto de programación, el campo startDate contiene la fecha de inicio del programa y el campo endDate contiene la fecha de finalización del programa. Si endDate es nulo en la programación, significa que el usuario no ha programado la fecha de finalización de la programación fuera de la oficina.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isNoPrimaryDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>True si no hay una designación principal en caso de que el usuario no esté en el servicio.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>True si el usuario no está en la oficina.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>Contiene los detalles del usuario asignado como principal designado por usuario.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processSpecificDesignates<br type="_moz" /> </td>
   <td>F</td>
   <td>Contiene una matriz de objetos para la designación fuera de la oficina específica del proceso. En cada objeto designado específico del proceso, processName contiene el nombre del proceso, isNotDesignated es true si no se asigna ningún usuario al proceso correspondiente y userDesignated es null si no se asigna ningún otro usuario a los detalles del usuario asignados al proceso correspondiente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processes<br type="_moz" /> </td>
   <td>T</td>
   <td>Contiene una lista de todos los procesos disponibles para el usuario.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initialOutOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>Contiene la configuración inicial fuera de la oficina del usuario, que se busca inicialmente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>Contiene una configuración fuera de la oficina modificada.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userSearchHistory<br type="_moz" /> </td>
   <td>T</td>
   <td>Contiene una lista de los usuarios que han buscado el usuario que ha iniciado sesión hasta la fecha.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Instancia de proceso

   Se crea una instancia de proceso cuando se invoca un proceso a través del espacio de trabajo o del área de trabajo.

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Solo cliente</strong></td>
   <td><strong>Comentarios</strong></td>
  </tr>
  <tr>
   <td>Descripción<br type="_moz" /> </td>
   <td>F</td>
   <td>Descripción de la instancia de proceso<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>iniciador</td>
   <td>F</td>
   <td>Nombre del iniciador de una instancia de proceso.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>F</td>
   <td>ID del iniciador de la instancia de proceso.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processCompleteTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Marca de hora cuando se complete el proceso.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID de la instancia de proceso.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br type="_moz" /> </td>
   <td>F</td>
   <td>0 = Iniciado<br /> 1 = Ejecución<br /> 2 = Completado<br /> 3 = Finalización<br /> 4 = Terminado<br /> 5 = Terminación<br /> 6 = Suspendido<br /> 7 = Suspendido<br /> 8 = Sin suspensión<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nombre del proceso.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processStartTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Marca de hora cuando se inició el proceso.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processVariables<br type="_moz" /> </td>
   <td>F</td>
   <td>Matriz de objetos de variables de proceso. Cada objeto de variable de proceso contiene el nombre que es el nombre de la variable de proceso, el valor que es el valor de la variable de proceso y el tipo que es el tipo de variable de proceso.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lista de tareas<br type="_moz" /> </td>
   <td>T</td>
   <td>Tareas generadas por esta instancia de proceso.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Nombre del proceso

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Solo cliente</strong></td>
   <td><strong>Comentarios</strong></td>
  </tr>
  <tr>
   <td>processMajorVersion<br type="_moz" /> </td>
   <td>F</td>
   <td>Versión principal de un proceso.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processMinorVersion<br type="_moz" /> </td>
   <td>F</td>
   <td>Versión menor de un proceso.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nombre del proceso.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processTitle<br type="_moz" /> </td>
   <td>F</td>
   <td>Título del proceso.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceList<br type="_moz" /> </td>
   <td>T</td>
   <td>Lista de instancias de proceso para este proceso.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Objeto de asignación de tareas

   El objeto de asignación de tareas contiene información sobre la asignación de la tarea. A continuación se indican las propiedades de la asignación de la tarea.

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Solo cliente</strong></td>
   <td><strong>Comentarios</strong></td>
  </tr>
  <tr>
   <td>AssignmentCreateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Marca de hora cuando se crea esta asignación de una tarea.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>AssignmentType<br type="_moz" /> </td>
   <td>F</td>
   <td>0 = Asignación<br /> inicial 1 = Reenviar (la tarea se ha reenviado al propietario actual de la tarea).<br /> 2 = Devuelta (el propietario anterior de la tarea ha devuelto la tarea al propietario actual de la tarea).<br /> 3 = Reclamado (la tarea ha sido reclamada por el propietario actual de la tarea).<br /> 4 = Escalación (la tarea se ha asignado al propietario actual de la tarea después de la escalación).<br /> 5 = Administrador asignado (el administrador ha asignado la tarea al propietario actual de la tarea).<br /> 6 = Consultado ( Se ha consultado la tarea al propietario actual de la tarea).<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>AssignmentUpdateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Marca de hora cuando se actualiza esta asignación de una tarea.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID de cola del propietario actual de la tarea.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwner<br type="_moz" /> </td>
   <td>F</td>
   <td>Nombre del propietario actual de la tarea.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwnerId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID del propietario actual de la tarea.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Objeto ACL de tarea

   El objeto ACL de tarea contiene información sobre permisos como reenviar, compartir, consultar, etc. de una tarea. A continuación se describen las propiedades de la ACL de la tarea.

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Solo cliente</strong></td>
   <td><strong>Comentarios</strong></td>
  </tr>
  <tr>
   <td>canAddAttachments<br type="_moz" /> </td>
   <td>F</td>
   <td>Si es true, los archivos adjuntos se pueden agregar a la tarea.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canAddNotes<br type="_moz" /> </td>
   <td>F</td>
   <td>Si es true, las notas se pueden agregar a la tarea.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canClaim<br type="_moz" /> </td>
   <td>F</td>
   <td>Si es true, se puede reclamar la tarea.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canConsult<br type="_moz" /> </td>
   <td>F</td>
   <td>Si es true, se puede consultar la tarea.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canForward<br type="_moz" /> </td>
   <td>F</td>
   <td>Si es true, la tarea se puede reenviar.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canShare<br type="_moz" /> </td>
   <td>F</td>
   <td>Si es true, la tarea se puede compartir.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Datos adjuntos de tarea

   Los datos adjuntos se pueden agregar a una tarea. Los datos adjuntos pueden ser del tipo adjunto y nota. A continuación se describen las propiedades del objeto de datos adjuntos.

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Solo cliente</strong></td>
   <td><strong>Comentarios</strong></td>
  </tr>
  <tr>
   <td>creationDate<br type="_moz" /> </td>
   <td>F</td>
   <td>Marca de hora al crear datos adjuntos.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID del usuario que agregó el archivo adjunto.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nombre del usuario que agregó el archivo adjunto.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>Descripción<br type="_moz" /> </td>
   <td>F</td>
   <td>Descripción del adjunto.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>fileName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nombre del archivo adjunto.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>id<br type="_moz" /> </td>
   <td>F</td>
   <td>ID del archivo adjunto.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastModifiedDate<br type="_moz" /> </td>
   <td>F</td>
   <td>Marca de hora cuando se modificó por última vez el archivo adjunto.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>noteExtended<br type="_moz" /> </td>
   <td>F</td>
   <td>Si es true, la nota es una nota extendida (larga).<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>permissions<br type="_moz" /> </td>
   <td>F</td>
   <td>Permisos asociados a un archivo adjunto. allowRead es para permiso de lectura, allowWrite es para permiso de escritura, allowDelete está para permiso de eliminación.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>size<br type="_moz" /> </td>
   <td>F</td>
   <td>Tamaño del archivo adjunto en bytes.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>taskId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID de la tarea a la que se agrega el archivo adjunto.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>tipo<br type="_moz" /> </td>
   <td>F</td>
   <td>El tipo es datos adjuntos para archivos y el tipo es una nota para notas.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedCreationDate<br type="_moz" /> </td>
   <td>T</td>
   <td>Contiene la fecha de creación de datos adjuntos según la configuración de la interfaz de usuario del usuario.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedDescription<br type="_moz" /> </td>
   <td>T</td>
   <td>Descripción de datos adjuntos con formato. Se utiliza para mostrar caracteres especiales presentes en la descripción de datos adjuntos en el espacio de trabajo de AEM Forms.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedFileName<br type="_moz" /> </td>
   <td>T</td>
   <td>Nombre de archivo adjunto con formato. Se utiliza para mostrar caracteres especiales presentes en el nombre del archivo adjunto en el espacio de trabajo de AEM Forms. Esto es solo para notas.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Usuario

   A continuación se describen las propiedades del objeto user.

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Solo cliente</strong></td>
   <td><strong>Comentarios</strong></td>
  </tr>
  <tr>
   <td>address<br type="_moz" /> </td>
   <td>F</td>
   <td>Dirección del usuario.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>commonName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nombre común del usuario.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>Descripción<br type="_moz" /> </td>
   <td>F</td>
   <td>Descripción del usuario.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>directGroupMembership<br type="_moz" /> </td>
   <td>F</td>
   <td>Lista del grupo del usuario.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>displayName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nombre para mostrar del usuario.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>email<br type="_moz" /> </td>
   <td>F</td>
   <td>ID de correo electrónico del usuario.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>True si el usuario no está en la oficina.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastName<br type="_moz" /> </td>
   <td>F</td>
   <td>Apellido del usuario.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>firstName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nombre del usuario.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>oid<br type="_moz" /> </td>
   <td>F</td>
   <td>ID del usuario.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>org<br type="_moz" /> </td>
   <td>F</td>
   <td>Nombre de la organización del usuario.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>postalAddress<br type="_moz" /> </td>
   <td>F</td>
   <td>Dirección postal del usuario.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>telephone<br type="_moz" /> </td>
   <td>F</td>
   <td>Número de contacto del usuario.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>phoneNumber<br type="_moz" /> </td>
   <td>F</td>
   <td>Número de contacto del usuario.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userid<br type="_moz" /> </td>
   <td>F</td>
   <td>Id. de inicio de sesión del usuario.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

**[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)**
