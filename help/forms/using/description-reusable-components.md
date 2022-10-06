---
title: Descripción de los componentes reutilizables
seo-title: Description of reusable components
description: Una lista completa de componentes reutilizables con nombres de archivo y dependencias para ayudarle a integrar el componente de espacio de trabajo de AEM Forms en sus aplicaciones web.
seo-description: A complete list of reusable components with filenames and dependencies, to help you integrate AEM Forms workspace component in your web applications.
uuid: 8e6accc7-0935-4d7b-b838-d23676df5cda
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: d3facd17-ceb0-4799-8cd9-ff9e81e09793
exl-id: b8cb7233-3d9e-41d4-85c5-8e8c2481f89c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 9%

---

# Descripción de los componentes reutilizables {#description-of-reusable-components}

El espacio de trabajo de AEM Forms está compuesto por [reutilizable](/help/forms/using/integrating-html-ws-components-web.md) componentes organizados en una [estructura de carpetas](/help/forms/using/folder-structure.md) en CRX™. Cada componente tiene un modelo, una vista y un archivo de plantilla en la ubicación especificada en la estructura de carpetas, dependencias JavaScript™ de otros archivos de componentes, eventos escuchados por el componente y objetos JavaScript que déclencheur estos eventos en el espacio de trabajo de AEM Forms. La lista completa de componentes reutilizables con nombres de archivo y dependencias constituyentes se proporciona aquí.

## Lista de tareas {#tasklist}

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
     <li><p>Teamtask</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td>
    <ul>
     <li><p>modelo de tareas</p></li>
     <li><p>modelo teamtask</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento - Déclencheur)</p></td>
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
>Este componente se puede utilizar de forma independiente del espacio de trabajo de AEM Forms, siempre que filtre el déclencheurEvento seleccionado para este componente desde la aplicación personalizada.

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
   <td><p>Eventos escuchados (Nombre del evento - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>submitComplete - modelo de tareas</p></li>
     <li><p>Rechazar - modelo de tareas</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Workspace llama a la función fetchTasks del modelo TaskList para crear modelos de Task para este componente.

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
   <td><p>Eventos escuchados (Nombre del evento - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>fetch - modelo de lista de tareas </p></li>
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

## Colas de equipo {#teamqueues}

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
   <td><p>Eventos escuchados (Nombre del evento - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>fetch - modelo de lista de tareas </p></li>
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
     <li><p>Amplía : vista de filtro</p> </li>
     <li><p>Campo : queue :{ name, qid, isDefault, type }</p> </li>
     <li><p>Campo : consulta : string</p> </li>
     <li><p>Campo : parentView : vista de lista de filtros</p> </li>
     <li><p>Campo : parentModel : modelo de lista de tareas</p> </li>
     <li><p>Campo : utilidad</p> </li>
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

## Detalles de la tarea {#taskdetails}

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
   <td><p>La mayoría de las clases de utilidades</p> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td>
    <ul>
     <li><p>processinstancehistory.html</p> </li>
     <li><p>utilidad de renderización</p> </li>
     <li><p>utilidad notas</p> </li>
     <li><p>utilidad de archivos adjuntos</p> </li>
     <li><p>utilidad taskactions</p> </li>
     <li><p>utilidad de historial</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento - Déclencheur)</p> </td>
   <td>
    <ul>
     <li><p>reenviado: modelo de tareas</p> </li>
     <li><p>shared - task model</p> </li>
     <li><p>consultado - modelo de tareas</p> </li>
     <li><p>rechazado - modelo de tareas</p> </li>
     <li><p>abandonado - modelo de tarea</p> </li>
     <li><p>desbloqueado - modelo de tareas</p> </li>
     <li><p>bloqueado - modelo de tareas</p> </li>
     <li><p>clamado - modelo de tarea</p> </li>
     <li><p>cambio:selección de tareas - modelo de lista de tareas</p> </li>
     <li><p>change:formUrl - modelo de tareas</p> </li>
     <li>attachmentURLFetched - modelo de tareas</li>
    </ul>
    <ul>
     <li>newAttachment - modelo de tareas</li>
     <li><p>taskHistoryFetched - modelo de tareas</p> </li>
     <li>prepareForSubmitComplete - modelo de tareas</li>
     <li><p>submitComplete - modelo de tareas</p> </li>
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
   <td><p>startProcess.html (en la carpeta de ruta)</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>Categoría</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td>
    <ul>
     <li><p>modelo favoritecategoryfactory</p></li>
     <li><p>modelo allcategoryfactory</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>allStartpointsFetched - modelo de lista de categorías </p></li>
     <li><p>add - categorylist model </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Este componente utiliza clases de modelo de otros componentes, como StartPointList, StartPoint y Task. Además de esta dependencia, CategoryList puede utilizarse de forma independiente.

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
   <td><p>Eventos escuchados (Nombre del evento - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>modificado: modelo de categoría </p></li>
     <li><p>childrenFetched - modelo de categoría </p></li>
     <li><p>categoría:seleccionado - modelo de lista de categorías </p></li>
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
   <td><p>startProcess.html (en la carpeta de ruta)</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td>
    <ul>
     <li><p>modelo category</p></li>
     <li><p>modelo favoritecategoryfactory</p></li>
     <li><p>modelo allcategoryfactory</p></li>
     <li><p>vista de punto de inicio</p></li>
     <li><p>modelo startpointlist</p></li>
     <li><p>modelo startpoint</p></li>
     <li><p>modelo de tareas</p></li>
     <li><p>modelo de tareas</p></li>
     <li><p>modelo de lista de tareas</p></li>
     <li><p>modelo teamtask</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>categoría:seleccionado - modelo de lista de categorías </p></li>
     <li><p>allStartpointsFetched - modelo de lista de categorías </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Los componentes StartPointList y CategoryList comparten la clase modelo, por lo que la primera depende de la segunda. CategoryList accede a la información sobre los puntos de inicio de la categoría que se muestran. Para utilizar StartPointList de forma independiente, simule el déclencheur de evento de CategoryList.

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
   <td><p>modelo de tareas</p></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento - Déclencheur)</p></td>
   <td><p>change - modelo de punto de inicio </p></td>
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
     <li><p>La mayoría de las clases de utilidades</p> </li>
     <li><p>UserSearch</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td>
    <ul>
     <li><p>modelo category</p> </li>
     <li><p>modelo favoritecategoryfactory</p> </li>
     <li><p>modelo allcategoryfactory</p> </li>
     <li><p>utilidad de renderización</p> </li>
     <li><p>utilidad notas</p> </li>
     <li><p>utilidad de archivos adjuntos</p> </li>
     <li><p>utilidad taskactions</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento - Déclencheur)</p> </td>
   <td>
    <ul>
     <li><p>categoría:seleccionado - modelo de lista de categorías</p> </li>
     <li><p>change:invocaTask - modelo startpointlist</p> </li>
     <li><p>change:formUrl - modelo de tareas</p> </li>
     <li><p>punto de inicio:seleccionado: modelo de lista de inicio</p> </li>
     <li><p>reenviado: modelo de tareas</p> </li>
     <li><p>abandonado - modelo de tarea</p> </li>
     <li><p>desbloqueado - modelo de tareas</p> </li>
     <li><p>bloqueado - modelo de tareas</p> </li>
     <li>attachmentURLFetched - modelo de tareas</li>
     <li>newAttachment - modelo de tareas</li>
     <li>prepareForSubmitComplete - modelo de tareas </li>
     <li><p>submitComplete - modelo de tareas</p> </li>
     <li><p>allStartpointsFetched - modelo de lista de categorías</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Los componentes StartProcess y StartPointList comparten la clase de modelo. Este componente se vuelve relevante si selecciona un punto de inicio de StartPointList.

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
   <td><p>tracking.html (en la carpeta de ruta)</p></td>
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
   <td><p>Eventos escuchados (Nombre del evento - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>add - processnamelist modelo </p></li>
     <li><p>fetched:nombreproceso - modelo nombreproceso </p></li>
     <li><p>change - modelo processnamelist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessNameList no depende de otros componentes. Sin embargo, depende internamente de la clase del modelo ProcessInstanceList que a su vez depende de otros componentes. Por lo tanto, ProcessNameList utiliza muchas clases de modelo como ProcessInstanceList, ProcessInstance, TaskList, Teamtask y Task. Además de estas dependencias, ProcessNameList puede utilizarse de forma independiente.

## ProcessName {#processname}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>processname.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>nombreproceso (en processnamelist.js)</p></td>
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
   <td><p>Eventos escuchados (Nombre del evento - Déclencheur)</p></td>
   <td><p>change - modelo de nombre de proceso </p></td>
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
   <td><p>tracking.html (en la carpeta de ruta)</p></td>
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
   <td><p>Eventos escuchados (Nombre del evento - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>nombreproceso:seleccionado - modelo de lista de nombres de procesos </p></li>
     <li><p>nombreproceso:instancesfetched - modelo de lista de nombres de procesos </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceList espera un evento de ProcessNameList que indica el nombre del proceso para recuperar y mostrar instancias. Para utilizar ProcessInstanceList de forma independiente, simule el déclencheur de eventos por separado.

## ProcessInstance {#processinstance}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>processinstance.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>nombre de proceso dentro de nombelist.js</p></td>
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
   <td><p>Eventos escuchados (Nombre del evento - Déclencheur)</p></td>
   <td><p>change - process, modelo de instancia </p></td>
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
   <td><p>Eventos escuchados (Nombre del evento - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>nombreproceso:seleccionado - modelo de lista de nombres de procesos </p></li>
     <li><p>processinstance:selected - processinstancelist modelo </p></li>
     <li><p>tasksFetched - modelo de instancia de proceso </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceHistory espera un evento de ProcessInstanceList que indique qué historial de instancias de proceso se va a mostrar. Además de esta dependencia, el componente se puede utilizar de forma independiente.

## Fuera de oficina {#outofoffice}

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
   <td><p>vista de búsqueda de usuarios</p> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento - Déclencheur)</p> </td>
   <td>
    <ul>
     <li><p>outOfOfficeSettingsFetched - modelo de fuera de la oficina</p> </li>
     <li><p>outOfOfficeSettingsSaved - modelo de oficina externa</p> </li>
     <li><p>processesFetched - modelo de outfoffice</p> </li>
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
   <td><p>vista de búsqueda de usuarios</p> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento - Déclencheur)</p> </td>
   <td>
    <ul>
     <li><p>queueAccessGranted - modelo sharequeue</p> </li>
     <li><p>queueAccessRequested - modelo sharequeue</p> </li>
     <li><p>allowedUsersFetched - modelo sharequeue</p> </li>
     <li>accessibleUsersFetched - modelo sharequeue</li>
     <li><p>queueAccessRevewed - modelo sharequeue</p> </li>
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
   <td><p>Eventos escuchados (Nombre del evento - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>preferencias recuperadas: modelo de configuración de usuario </p></li>
     <li><p>settingUpdated: modelo de configuración de usuario </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UISettings se puede usar de forma independiente.

## Navegación de aplicaciones {#appnavigation}

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
   <td><p>Eventos escuchados (Nombre del evento - Déclencheur)</p> </td>
   <td>
    <ul>
     <li>userImageUrlFetched - modelo userinfo</li>
     <li>sessionRenewed: modelo userinfo <br /> </li>
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
   <td><p>Eventos escuchados (Nombre del evento - Déclencheur)</p></td>
   <td><p>newWsError - modelo wserror </p></td>
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
   <td><p>Eventos escuchados (Nombre del evento - Déclencheur)</p> </td>
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
   <td><p>Eventos escuchados (Nombre del evento - Déclencheur)</p> </td>
   <td><p>templateFetched- searchtemplate modelo</p> </td>
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
   <td><p>tracking.html (en la carpeta de ruta)</p> </td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td><p>modelo searchtemplate</p> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento - Déclencheur)</p> </td>
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
   <td><p>Eventos escuchados (Nombre del evento - Déclencheur)</p> </td>
   <td><p>searchTemplate:selected - modelo de plantilla de búsqueda</p> </td>
  </tr>
 </tbody>
</table>
