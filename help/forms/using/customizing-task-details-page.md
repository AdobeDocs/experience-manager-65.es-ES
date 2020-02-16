---
title: Personalización de la página de detalles de la tarea
seo-title: Personalización de la página de detalles de la tarea
description: Personalización de la página de detalles de tareas en el espacio de trabajo de AEM Forms para modificar la información predeterminada que se muestra sobre una tarea.
seo-description: Personalización de la página de detalles de tareas en el espacio de trabajo de AEM Forms para modificar la información predeterminada que se muestra sobre una tarea.
uuid: d85fae55-8e66-4595-8560-5485622b6841
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 16e57cf6-aaa1-406d-a6ad-71ec60b15386
translation-type: tm+mt
source-git-commit: 21623c615ebe69226cfaf84baf4cfb1717b449f4

---


# Personalización de la página de detalles de la tarea {#customizing-the-task-details-page}

La página de detalles de la tarea contiene información sobre una tarea y sus procesos. Sin embargo, puede personalizar la página de detalles de la tarea para agregar o eliminar información.

Puede agregar la siguiente información a la página de detalles de la tarea:

* Información disponible en el objeto JSON de una tarea (sección Tarea del espacio de trabajo de [AEM Forms Descripción](/help/forms/using/html-workspace-json-object-description.md)del objeto JSON)
* Información disponible en el objeto JSON de una instancia de proceso (sección Instancia de proceso en el espacio de trabajo de [AEM Forms Descripción](/help/forms/using/html-workspace-json-object-description.md)del objeto JSON)

Para personalizar la página de detalles de la tarea:

1. Siga los pasos [genéricos para personalizar el espacio de trabajo de AEM Forms.](/help/forms/using/generic-steps-html-workspace-customization.md)
1. Para mostrar cualquier información adicional, agregue los pares de clave-valor correspondientes al `translation.json` archivo en `todo`block > `details`block > `app`block > [ block `required`].

   El [ bloque `required`] hace referencia a los bloques disponibles, como el bloque de tareas para información de tareas, el bloque de procesos para información de procesos y el bloque de tareas actual para información de tareas pendientes.

   Por ejemplo, para agregar información sobre la selección de ruta requerida en la página de detalles de la tarea, puede agregar el siguiente par clave-valor en el bloque de tareas:

   ```
   "todo" : {
       .
       .
       .
       "details" : {
           .
           .
           "task" : {
               .
               .
               "RouteSelectionRequired" : "Route Selection Required"
           }
       }
   }
   ```

   >[!NOTE]
   >
   >Agregue los pares de clave-valor correspondientes para todos los idiomas admitidos.

1. Copiar `/libs/ws/js/runtime/templates/taskdetails.html` a `/apps/ws/js/runtime/templates/taskdetails.html`.

   Agregue la nueva información a `/apps/ws/js/runtime/templates/taskdetails.html`. Por ejemplo:

   ```css
   <div class="detailsContainer">
       .
       .
       <ul>
           .
           .
           <li>
               <label for="routeSelectionRequired" title="<%= $.t('todo.details.task.RouteSelectionRequired')%>"><%= $.t('todo.details.task.RouteSelectionRequired')%></label>
               <div>
                   <span id="routeSelectionRequired"><%= isRouteSelectionRequired != null ? isRouteSelectionRequired : ''%></span>
               </div>
           </li>
           .
           .
       </ul>
   </div>
   ```

1. Abra /apps/ws/js/registry.js para editar.

   Busque y reemplace `text!/lc/libs/ws/js/runtime/templates/taskdetails.html` por `text!/lc/apps/ws/js/runtime/templates/taskdetails.html`.

>[!NOTE]
>
>Para personalizar la página de detalles de la tarea con tareas creadas en la ficha **Iniciar proceso** del espacio de trabajo de AEM Forms, agregue la nueva información a `/apps/ws/js/runtime/templates/startprocess.html`.
>
>Para agregar nuevos estilos a la información agregada en la página de detalles, modifique el archivo CSS mediante la sección Cambios *en la interfaz de* usuario de Personalización [del espacio de trabajo](/help/forms/using/changing-locale-user-interface.md#main-pars-header-3).

[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
