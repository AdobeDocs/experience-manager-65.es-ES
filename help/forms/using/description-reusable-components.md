---
title: Descripción de los componentes reutilizables
seo-title: Descripción de los componentes reutilizables
description: Una lista completa de componentes reutilizables con nombres de archivo y dependencias para ayudarle a integrar el componente de espacio de trabajo de AEM Forms en sus aplicaciones web.
seo-description: Una lista completa de componentes reutilizables con nombres de archivo y dependencias para ayudarle a integrar el componente de espacio de trabajo de AEM Forms en sus aplicaciones web.
uuid: 8e6accc7-0935-4d7b-b838-d23676df5cda
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: d3facd17-ceb0-4799-8cd9-ff9e81e09793
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 9%

---


# Descripción de los componentes reutilizables {#description-of-reusable-components}

El espacio de trabajo de AEM Forms está compuesto por [componentes reutilizables](/help/forms/using/integrating-html-ws-components-web.md) que están organizados en una [estructura de carpetas](/help/forms/using/folder-structure.md) específica en CRX™. Cada componente tiene un modelo, una vista y un archivo de plantilla en la ubicación especificada en la estructura de carpetas, dependencias de JavaScript™ en otros archivos de componentes, eventos escuchados por el componente y objetos de JavaScript que déclencheur estos eventos en el espacio de trabajo de AEM Forms. Aquí se proporciona la lista completa de los componentes reutilizables con nombres de archivo constituyentes y dependencias.

## TaskList {#tasklist}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>tasklist.html</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td>
    <ul>
     <li><p>UserSearch</p></li>
     <li><p>Tarea</p></li>
     <li><p>Tarea en equipo</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td>
    <ul>
     <li><p>modelo de tarea</p></li>
     <li><p>modelo de tarea de equipo</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (nombre del Evento - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>filterSelected - modelo de lista de tareas</p></li>
     <li><p>quitar - modelo de lista de tareas</p></li>
     <li><p>updateQueue - modelo de lista de tareas</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Este componente se puede utilizar independientemente del espacio de trabajo de AEM Forms, siempre que se utilice el déclencheur filterevento seleccionado para este componente desde la aplicación personalizada.

## Tarea {#task}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>task.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>task.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>task.html</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td>
    <ul>
     <li><p>modelo de lista de tareas</p></li>
     <li><p>utilidad taskactions</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (nombre del Evento - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>submitComplete: modelo de tarea</p></li>
     <li><p>Rechazar - modelo de tarea</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Workspace llama a la función fetchTasks del modelo TaskList para crear modelos de Tarea para este componente.

## FilterList {#filterlist}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>filterlist.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>filterlist.html</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (nombre del Evento - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>buscado - modelo de lista de tareas </p></li>
     <li><p>quitar - modelo de lista de tareas </p></li>
     <li><p>updateQueue - modelo de lista de tareas </p></li>
     <li><p>refreshQueue: modelo de lista de tareas </p></li>
     <li><p>filterSelected - modelo de lista de tareas</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## Filtro {#filter}

<table>
 <tbody>
  <tr>
   <td><p>Ver</p> </td>
   <td><p>filter.js</p> </td>
  </tr>
  <tr>
   <td><p>Plantilla</p> </td>
   <td><p>filter.html</p> </td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td>
    <ul>
     <li><p>Campo: cola: { name, qid, isDefault, type}</p> </li>
     <li><p>Campo: consulta: string</p> </li>
     <li><p>Campo: parentView: vista de lista de filtros</p> </li>
     <li><p>Campo: parentModel: modelo de lista de tareas</p> </li>
     <li><p>Campo: utilidad</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados</p> </td>
   <td><p>ND</p> </td>
  </tr>
 </tbody>
</table>

## TeamQueues {#teamqueues}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>teamqueues.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>teamqueues.html</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (nombre del Evento - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>buscado - modelo de lista de tareas </p></li>
     <li><p>quitar - modelo de lista de tareas </p></li>
     <li><p>updateQueue - modelo de lista de tareas </p></li>
     <li><p>teamQueuesFetched - modelo de lista de tareas </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## TeamFilter {#teamfilter}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Ver</p> </td>
   <td><p>teamfilter.js</p> </td>
  </tr>
  <tr>
   <td><p>Plantilla</p> </td>
   <td><p>teamfilter.html</p> </td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td>
    <ul>
     <li><p>Extiende : vista de filtro</p> </li>
     <li><p>Campo: queue :{ name, qid, isDefault, type }</p> </li>
     <li><p>Campo: consulta: string</p> </li>
     <li><p>Campo: parentView: vista de lista de filtros</p> </li>
     <li><p>Campo: parentModel : modelo de lista de tareas</p> </li>
     <li><p>Campo: utilidad</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados</p> </td>
   <td><p>ND</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>TeamFilter obtiene el evento que indica qué tarea se ha seleccionado del componente TaskList. Aunque estos componentes comparten la clase de modelo, no hay otra dependencia.

## Detalles de tarea {#taskdetails}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>tasklist.js</p> </td>
  </tr>
  <tr>
   <td><p>Ver</p> </td>
   <td><p>taskdetails.js</p> </td>
  </tr>
  <tr>
   <td><p>Plantilla</p> </td>
   <td><p>taskdetails.html</p> </td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p> </td>
   <td><p>La mayoría de las clases de Utilidad</p> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td>
    <ul>
     <li><p>processinstancehistory.html</p> </li>
     <li><p>utilidad de procesamiento de formularios</p> </li>
     <li><p>utilidad de notas</p> </li>
     <li><p>utilidad de archivos adjuntos</p> </li>
     <li><p>utilidad taskactions</p> </li>
     <li><p>utilidad de historial</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (nombre del Evento - Déclencheur)</p> </td>
   <td>
    <ul>
     <li><p>reenviado - modelo de tarea</p> </li>
     <li><p>compartido: modelo de tarea</p> </li>
     <li><p>consultado - modelo de tarea</p> </li>
     <li><p>rechazado - modelo de tarea</p> </li>
     <li><p>abandonado - modelo de tarea</p> </li>
     <li><p>desbloqueado - modelo de tarea</p> </li>
     <li><p>bloqueado - modelo de tarea</p> </li>
     <li><p>reclamado - modelo de tarea</p> </li>
     <li><p>cambio:selección de tareas - modelo de lista de tareas</p> </li>
     <li><p>change:formUrl - modelo de tarea</p> </li>
     <li>attachmentURLFetched - modelo de tarea</li>
    </ul>
    <ul>
     <li>newAttachment - modelo de tarea</li>
     <li><p>taskHistoryFetched - modelo de tarea</p> </li>
     <li>prepareForSubmitComplete: modelo de tarea</li>
     <li><p>submitComplete: modelo de tarea</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## CategoryList {#categorylist}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>startprocess.html (en la carpeta route)</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>Categoría</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td>
    <ul>
     <li><p>modelo favoritecategoryFactory</p></li>
     <li><p>modelo allcategoryFactory</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (nombre del Evento - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>allStartpointsFetched - modelo de lista de categorías </p></li>
     <li><p>agregar - modelo de lista de categorías </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Este componente utiliza clases de modelo de otros componentes como StartPointList, StartPoint y Tarea. Además de esta dependencia, CategoryList puede utilizarse de forma independiente.

## Categoría {#category}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>category.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>category.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>category.html</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td>
    <ul>
     <li><p>modelo de lista de categorías</p></li>
     <li><p>modelo startpointlist</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (nombre del Evento - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>cambiado - modelo de categoría </p></li>
     <li><p>childrenFetched - modelo de categoría </p></li>
     <li><p>categoría:seleccionada - modelo de lista de categorías </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## StartPointList {#startpointlist}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>startpointlist.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>startprocess.html (en la carpeta route)</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td>
    <ul>
     <li><p>modelo de categoría</p></li>
     <li><p>modelo favoritecategoryFactory</p></li>
     <li><p>modelo allcategoryFactory</p></li>
     <li><p>vista de startpoint</p></li>
     <li><p>modelo startpointlist</p></li>
     <li><p>modelo startpoint</p></li>
     <li><p>modelo de tarea</p></li>
     <li><p>modelo de tarea</p></li>
     <li><p>modelo de lista de tareas</p></li>
     <li><p>modelo de tarea de equipo</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (nombre del Evento - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>categoría:seleccionada - modelo de lista de categorías </p></li>
     <li><p>allStartpointsFetched - modelo de lista de categorías </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Los componentes StartPointList y CategoryList comparten la clase de modelo, por lo que la primera depende de la segunda. CategoryList accede a la información sobre los puntos de inicio de la categoría que se muestran. Para utilizar StartPointList de forma independiente, simule el déclencheur de evento de CategoryList.

## StartPoint {#startpoint}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>startpoint.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>startpoint.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>startpoint.html</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td><p>modelo de tarea</p></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (nombre del Evento - Déclencheur)</p></td>
   <td><p>change - modelo de punto de partida </p></td>
  </tr>
 </tbody>
</table>

## StartProcess {#startprocess}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>categorylist.js</p> </td>
  </tr>
  <tr>
   <td><p>Ver</p> </td>
   <td><p>startprocess.js</p> </td>
  </tr>
  <tr>
   <td><p>Plantilla</p> </td>
   <td><p>startprocess.html</p> </td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p> </td>
   <td>
    <ul>
     <li><p>La mayoría de las clases de Utilidad</p> </li>
     <li><p>UserSearch</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td>
    <ul>
     <li><p>modelo de categoría</p> </li>
     <li><p>modelo favoritecategoryFactory</p> </li>
     <li><p>modelo allcategoryFactory</p> </li>
     <li><p>utilidad de procesamiento de formularios</p> </li>
     <li><p>utilidad de notas</p> </li>
     <li><p>utilidad de archivos adjuntos</p> </li>
     <li><p>utilidad taskactions</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (nombre del Evento - Déclencheur)</p> </td>
   <td>
    <ul>
     <li><p>categoría:seleccionada - modelo de lista de categorías</p> </li>
     <li><p>change:alledTask - modelo startpointlist</p> </li>
     <li><p>change:formUrl - modelo de tarea</p> </li>
     <li><p>punto de inicio:seleccionado - modelo de lista de puntos de inicio</p> </li>
     <li><p>reenviado - modelo de tarea</p> </li>
     <li><p>abandonado - modelo de tarea</p> </li>
     <li><p>desbloqueado - modelo de tarea</p> </li>
     <li><p>bloqueado - modelo de tarea</p> </li>
     <li>attachmentURLFetched - modelo de tarea</li>
     <li>newAttachment - modelo de tarea</li>
     <li>prepareForSubmitComplete: modelo de tarea </li>
     <li><p>submitComplete: modelo de tarea</p> </li>
     <li><p>allStartpointsFetched - modelo de lista de categorías</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Los componentes StartProcess y StartPointList comparten la clase de modelo. Este componente resulta relevante cuando selecciona un punto de partida en StartPointList.

## ProcessNameList {#processnamelist}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>tracking.html (en la carpeta route)</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td><p>modelo processname</p></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (nombre del Evento - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>add - modelo processnamelist </p></li>
     <li><p>buscado:nombreproceso - modelo nombredeproceso </p></li>
     <li><p>change - modelo de lista de nombres de procesos </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessNameList no depende de otros componentes. Sin embargo, de forma interna depende de la clase de modelo ProcessInstanceList que, a su vez, depende de otros componentes. Por lo tanto, ProcessNameList utiliza muchas clases de modelo como ProcessInstanceList, ProcessInstance, TaskList, Teamtask y Tarea. Además de estas dependencias, ProcessNameList puede utilizarse de forma independiente.

## ProcessName {#processname}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>processname.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>nombreproceso (en nombredeproceso.js)</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>processname.html</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td><p>modelo processinstancelist</p></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (nombre del Evento - Déclencheur)</p></td>
   <td><p>change - modelo processname </p></td>
  </tr>
 </tbody>
</table>

## ProcessInstanceList {#processinstancelist}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>processinstancelist.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>tracking.html (en la carpeta route)</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td><p>modelo processname</p></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (nombre del Evento - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>nombreproceso:seleccionado - modelo de lista de nombres de procesos </p></li>
     <li><p>nombreproceso:instancesfetched - modelo processnamelist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceList espera un evento de ProcessNameList que indica el nombre del proceso para recuperar y mostrar instancias. Para utilizar ProcessInstanceList de forma independiente, simule el déclencheur de evento por separado.

## ProcessInstance {#processinstance}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>processinstance.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>nombreproceso dentro de processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>processinstance.html</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td><p>modelo de lista de tareas</p></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (nombre del Evento - Déclencheur)</p></td>
   <td><p>change - modelo de instancia de proceso </p></td>
  </tr>
 </tbody>
</table>

## ProcessInstanceHistory {#processinstancehistory}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>processinstancehistory.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>processinstancehistory.html</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td>
    <ul>
     <li><p>modelo processname</p></li>
     <li><p>utilidad de historial</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (nombre del Evento - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>nombreproceso:seleccionado - modelo de lista de nombres de procesos </p></li>
     <li><p>processinstance:selected - modelo processinstancelist </p></li>
     <li><p>TasksFetched - modelo de instancia de proceso </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceHistory espera un evento de ProcessInstanceList que indica qué historial de instancias de proceso se va a mostrar. Además de esta dependencia, el componente se puede utilizar de forma independiente.

## OutofOffice {#outofoffice}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>outofoffice.js</p> </td>
  </tr>
  <tr>
   <td><p>Ver</p> </td>
   <td><p>outofoffice.js</p> </td>
  </tr>
  <tr>
   <td><p>Plantilla</p> </td>
   <td><p>outofoffice.html</p> </td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p> </td>
   <td><p>UserSearch</p> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td><p>vista usersearch</p> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (nombre del Evento - Déclencheur)</p> </td>
   <td>
    <ul>
     <li><p>outOfOfficeSettingsFetched - modelo de outtofoffice</p> </li>
     <li><p>outOfOfficeSettingsSaved - modelo de outtofoffice</p> </li>
     <li><p>processFetched - modelo de OUTOFoffice</p> </li>
     <li><p>principalSelected - vista de búsqueda principal</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>OutofOffice puede utilizarse de forma independiente.

## ShareQueue {#sharequeue}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>sharequeue.js</p> </td>
  </tr>
  <tr>
   <td><p>Ver</p> </td>
   <td><p>sharequeue.js</p> </td>
  </tr>
  <tr>
   <td><p>Plantilla</p> </td>
   <td><p>sharequeue.html</p> </td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p> </td>
   <td><p>UserSearch</p> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td><p>vista usersearch</p> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (nombre del Evento - Déclencheur)</p> </td>
   <td>
    <ul>
     <li><p>queueAccessGranted - modelo sharequeue</p> </li>
     <li><p>queueAccessRequested - modelo sharequeue</p> </li>
     <li><p>approvedUsersFetched - modelo sharequeue</p> </li>
     <li>accessibleUsersFetched - modelo sharequeue</li>
     <li><p>queueAccessRevected - modelo sharequeue</p> </li>
     <li><p>queueAccessRemoved - modelo sharequeue</p> </li>
     <li><p>principalSelected - vista de búsqueda principal</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ShareQueue se puede usar de forma independiente.

## UISettings {#uisettings}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>uisettings.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>uisettings.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>uisettings.html</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (nombre del Evento - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>PreferencesFetched - modelo de configuración </p></li>
     <li><p>SettingUpdated: modelo uisettings </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UISettings se puede utilizar de forma independiente.

## AppNavigation {#appnavigation}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>appnavigation.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>appnavigation.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>appnavigation.html</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados</p></td>
   <td><p>ND</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AppNavigation puede utilizarse de forma independiente.

## UserInfo {#userinfo}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>userinfo.js</p> </td>
  </tr>
  <tr>
   <td><p>Ver</p> </td>
   <td><p>userinfo.js</p> </td>
  </tr>
  <tr>
   <td><p>Plantilla</p> </td>
   <td><p>userinfo.html</p> </td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (nombre del Evento - Déclencheur)</p> </td>
   <td>
    <ul>
     <li>userImageUrlFetched - modelo userinfo</li>
     <li>sessionRenewed - modelo userinfo <br /> </li>
     <li>sessionExpired - modelo userinfo </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UserInfo se puede utilizar de forma independiente.

## WSError {#wserror}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>wserror.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>wserror.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>wserror.html</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (nombre del Evento - Déclencheur)</p></td>
   <td><p>newWsError - modelo de wserror </p></td>
  </tr>
 </tbody>
</table>

## UserSearch {#usersearch}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>usersearch.js</p> </td>
  </tr>
  <tr>
   <td><p>Ver</p> </td>
   <td><p>usersearch.js</p> </td>
  </tr>
  <tr>
   <td><p>Plantilla</p> </td>
   <td><p>usersearch.html</p> </td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (nombre del Evento - Déclencheur)</p> </td>
   <td>
    <ul>
     <li>principalSearched - modelo de búsqueda principal</li>
     <li>outOfOfficeInfoFetched - modelo de búsqueda de usuarios</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## SearchTemplate {#searchtemplate}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>searchtemplate.js</p> </td>
  </tr>
  <tr>
   <td><p>Ver</p> </td>
   <td><p>searchtemplate (en searchtemplatelist.js) </p> </td>
  </tr>
  <tr>
   <td><p>Plantilla</p> </td>
   <td><p>searchtemplate.html</p> </td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (nombre del Evento - Déclencheur)</p> </td>
   <td><p>templateFetched - modelo de plantilla de búsqueda</p> </td>
  </tr>
 </tbody>
</table>

## SearchTemplateList {#searchtemplatelist}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>Ver</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>Plantilla</p> </td>
   <td><p>tracking.html (en la carpeta route)</p> </td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td><p>modelo de plantilla de búsqueda</p> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (nombre del Evento - Déclencheur)</p> </td>
   <td><p>change - searchtemplatelist modelo</p> </td>
  </tr>
 </tbody>
</table>

## SearchTemplateDetails {#searchtemplatedetails}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>Ver</p> </td>
   <td><p>searchtemplatedetails.js</p> </td>
  </tr>
  <tr>
   <td><p>Plantilla</p> </td>
   <td><p>searchtemplatedetails.html</p> </td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td>ND<br /> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (nombre del Evento - Déclencheur)</p> </td>
   <td><p>searchTemplate:selected - modelo de plantilla de búsqueda</p> </td>
  </tr>
 </tbody>
</table>
