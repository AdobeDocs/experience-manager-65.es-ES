---
title: Personalización de las tablas de seguimiento
seo-title: Personalización de las tablas de seguimiento
description: Cómo personalizar la visualización de los detalles de los procesos de usuario en la tabla de tareas que se muestra en la ficha de seguimiento del espacio de trabajo de AEM Forms.
seo-description: Cómo personalizar la visualización de los detalles de los procesos de usuario en la tabla de tareas que se muestra en la ficha de seguimiento del espacio de trabajo de AEM Forms.
uuid: 13d6ebf2-99d5-434f-85f9-b0cba5f5751a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: bb7a6e9f-4f28-4d97-8a0c-949259fd6857
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 3%

---


# Personalizar tablas de seguimiento{#customize-tracking-tables}

La ficha de seguimiento del espacio de trabajo de AEM Forms se utiliza para mostrar los detalles de las instancias de proceso en las que participa el usuario que ha iniciado sesión. Para realizar la vista de las tablas de seguimiento, primero seleccione un nombre de proceso en el panel izquierdo para ver su lista de instancias en el panel medio. Seleccione una instancia de proceso para ver una tabla de tareas generadas por esta instancia en el panel derecho. De forma predeterminada, las columnas de la tabla muestran los atributos de tarea siguientes (el atributo correspondiente del modelo de tarea se indica entre paréntesis):

* ID ( `taskId`)
* Nombre ( `stepName`)
* Instrucciones ( `instructions`)
* Acción seleccionada ( `selectedRoute`)
* Hora de creación ( `createTime`)
* Tiempo de finalización ( `completeTime`)
* Propietario ( `currentAssignment.queueOwner`)

Los atributos restantes del modelo de tarea disponibles para su visualización en la tabla de tareas son:

<table>
 <tbody>
  <tr>
   <td><p>actionInstanceId</p> </td>
   <td><p>isOpenFullScreen</p> </td>
   <td><p>recordatorioCount</p> </td>
  </tr>
  <tr>
   <td><p>classOfTask</p> </td>
   <td><p>isOwner</p> </td>
   <td><p>routeList</p> </td>
  </tr>
  <tr>
   <td><p>queryGroupId</p> </td>
   <td><p>isRouteSelectionRequired</p> </td>
   <td><p>savedFormCount</p> </td>
  </tr>
  <tr>
   <td><p>contentType</p> </td>
   <td><p>isShowAttachments</p> </td>
   <td><p>serializedImageTicket</p> </td>
  </tr>
  <tr>
   <td><p>createTime</p> </td>
   <td><p>isStartTask</p> </td>
   <td><p>serviceName</p> </td>
  </tr>
  <tr>
   <td><p>creatingId</p> </td>
   <td><p>isVisible</p> </td>
   <td><p>serviceTitle</p> </td>
  </tr>
  <tr>
   <td><p>currentAssignment</p> </td>
   <td><p>nextReminder</p> </td>
   <td><p>showACLActions</p> </td>
  </tr>
  <tr>
   <td><p>fecha límite</p> </td>
   <td><p>numForms</p> </td>
   <td><p>showDirectActions</p> </td>
  </tr>
  <tr>
   <td><p>Descripción</p> </td>
   <td><p>numFormsToBeSaved</p> </td>
   <td><p>estado</p> </td>
  </tr>
  <tr>
   <td><p>displayName</p> </td>
   <td><p>outOfOfficeUserId</p> </td>
   <td><p>summaryUrl</p> </td>
  </tr>
  <tr>
   <td><p>forwardGroupId</p> </td>
   <td><p>outOfOfficeUserName</p> </td>
   <td><p>supportSave</p> </td>
  </tr>
  <tr>
   <td><p>isApprovalUI</p> </td>
   <td><p>priority</p> </td>
   <td><p>taskACL</p> </td>
  </tr>
  <tr>
   <td><p>isCustomUI</p> </td>
   <td><p>processInstanceId</p> </td>
   <td><p>taskFormType</p> </td>
  </tr>
  <tr>
   <td><p>isDefaultImage</p> </td>
   <td><p>processInstanceStatus</p> </td>
   <td><p>taskUserInfo</p> </td>
  </tr>
  <tr>
   <td><p>isLocked</p> </td>
   <td><p>processVariables</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p>isMustOpenToComplete</p> </td>
   <td><p>readerSubmitOptions</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

Para las siguientes personalizaciones en la tabla de tarea, debe realizar cambios semánticos en el código fuente. Consulte [Introducción a la personalización del espacio de trabajo de AEM Forms](/help/forms/using/introduction-customizing-html-workspace.md) para obtener información sobre cómo puede realizar cambios semánticos mediante el SDK de espacio de trabajo y crear un paquete reducido a partir del origen modificado.

## Cambio de las columnas de la tabla y su orden {#changing-table-columns-and-their-order}

1. Para modificar los atributos de tarea mostrados en la tabla y su orden, configure el archivo /ws/js/runtime/templates/processinstancehistory.html :

   ```html
   <table>
       <thead>
           <tr>
               <!-- put the column headings in order here, for example-->
               <th><%= $.t('history.fixedTaskTableHeader.taskName')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskInstructions')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskRoute')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskCreateTime')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskCompleteTime')%></th>
           </tr>
       </thead>
   </table>
   ```

   ```html
   <table>
       <tbody>
           <%_.each(obj, function(task){%>
           <tr>
               <!-- Put the task attributes in the order of headings, for example -->
               <td><%= task.stepName %></td>
               <td><%= task.instructions %></td>
               <td><%= !task.selectedRoute?'':(task.selectedRoute=='null'?'Default':task.selectedRoute) %></td>
               <td><%= task.createTime?task.formattedCreateTime:'' %></td>
               <td><%= task.completeTime? task.formattedCompleteTime:'' %></td>
           </tr>
           <%});%>
       </tbody>
   </table>
   ```

## Ordenar una tabla de seguimiento {#sorting-a-tracking-table}

Para ordenar la tabla de lista de tareas al hacer clic en el encabezado de columna:

1. Registre un controlador de clics para `.fixedTaskTableHeader th` en el archivo `js/runtime/views/processinstancehistory.js`.

   ```javascript
   events: {
       //other handlers
       "click .fixedTaskTableHeader th": "onTaskTableHeaderClick",
       //other handlers
   }
   ```

   En el controlador, invoque la función `onTaskTableHeaderClick` de `js/runtime/util/history.js`.

   ```javascript
   onTaskTableHeaderClick: function (event) {
           history.onTaskTableHeaderClick(event);
   }
   ```

1. Exponga el método `TaskTableHeaderClick` en `js/runtime/util/history.js`.

   El método busca el atributo de tarea desde el evento de clic, ordena la lista de tareas de ese atributo y procesa la tabla de tareas con la lista de tareas ordenada.

   La ordenación se realiza mediante la función de ordenación de la red troncal de la colección de listas de tareas, proporcionando una función de comparación.

   ```javascript
       return {
           //other methods
           onTaskTableHeaderClick  : onTaskTableHeaderClick,
           //other methods
       };
   ```

   ```javascript
   onTaskTableHeaderClick = function (event) {
           var target = $(event.target),
            comparator,
               attribute;
           if(target.hasClass('taskName')){
            attribute = 'stepName';
           } else if(target.hasClass('taskInstructions')){
               attribute = 'instructions';
           } else if(target.hasClass('taskRoute')){
               attribute = 'selectedRoute';
           } else if(target.hasClass('taskCreateTime')){
               attribute = 'createTime';
           } else if(target.hasClass('taskCompleteTime')){
               attribute = 'completeTime';
           }
           taskList.comparator = function (task) {
            return task.get(attribute);
           };
           taskList.sort();
           render();
       };
   ```
