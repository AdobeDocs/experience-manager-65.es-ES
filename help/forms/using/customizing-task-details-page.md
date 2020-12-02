---
title: Personalización de la página de detalles de tarea
seo-title: Personalización de la página de detalles de tarea
description: Personalización de la página de detalles de la tarea en el espacio de trabajo de AEM Forms para modificar la información predeterminada que se muestra sobre una tarea.
seo-description: Personalización de la página de detalles de la tarea en el espacio de trabajo de AEM Forms para modificar la información predeterminada que se muestra sobre una tarea.
uuid: d85fae55-8e66-4595-8560-5485622b6841
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 16e57cf6-aaa1-406d-a6ad-71ec60b15386
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Personalización de la página de detalles de tarea {#customizing-the-task-details-page}

La página de detalles de tarea contiene información sobre una tarea y sus procesos. Sin embargo, puede personalizar la página de detalles de la tarea para agregar o eliminar información.

Puede agregar la siguiente información a la página de detalles de la tarea:

* Información disponible en el objeto JSON de una tarea (sección Tarea en [área de trabajo de AEM Forms Descripción del objeto JSON](/help/forms/using/html-workspace-json-object-description.md))
* Información disponible en el objeto JSON de una instancia de proceso (sección Procesar instancia en [Área de trabajo de AEM Forms Descripción del objeto JSON](/help/forms/using/html-workspace-json-object-description.md))

Para personalizar la página de detalles de la tarea:

1. Siga [Pasos genéricos para la personalización del espacio de trabajo de AEM Forms.](/help/forms/using/generic-steps-html-workspace-customization.md)
1. Para mostrar cualquier información adicional, agregue los pares clave-valor correspondientes al archivo `translation.json` en `todo`block > `details`block > `app`block > [ `required`block].

   El [ `required`bloque] hace referencia a los bloques disponibles, como el bloque de tarea para información de tarea, el bloque de proceso para información de proceso y el bloque de tareas actual para información de tareas pendientes.

   Por ejemplo, para agregar información sobre la selección de ruta requerida en la página de detalles de la tarea, puede agregar el siguiente par clave-valor en el bloque de tarea:

   ```json
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
   >Añada los pares de clave-valor correspondientes para todos los idiomas admitidos.

1. Copie `/libs/ws/js/runtime/templates/taskdetails.html` en `/apps/ws/js/runtime/templates/taskdetails.html`.

   Añada la nueva información a `/apps/ws/js/runtime/templates/taskdetails.html`. Por ejemplo:

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
>Para personalizar la página de detalles de la tarea con tareas creadas en la ficha **Proceso de Inicio** del espacio de trabajo de AEM Forms, agregue la nueva información a `/apps/ws/js/runtime/templates/startprocess.html`.
>
>Para agregar nuevos estilos a la información agregada en la página de detalles, modifique el archivo CSS mediante la sección *Cambios en la interfaz de usuario* en [Personalización del espacio de trabajo](changing-locale-user-interface.md).
