---
title: Visualización de datos adicionales en la lista de tareas pendientes
seo-title: Displaying additional data in ToDo list
description: Personalización de la visualización de la lista de tareas pendientes del espacio de trabajo de AEM Forms de LiveCycle para mostrar más información además del predeterminado.
seo-description: How-to customize the display of the To-do list of LiveCycle AEM Forms workspace to show more information besides the default.
uuid: 9467c655-dce2-43ce-8e8f-54542fe81279
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: fed3b562-bcc2-4fb7-8fd2-35b1ac621e16
docset: aem65
exl-id: f8b84f13-02d3-4787-95e1-25fd684e6d3b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 1%

---

# Visualización de datos adicionales en la lista de tareas pendientes{#displaying-additional-data-in-todo-list}

De forma predeterminada, la lista Tareas pendientes de AEM Forms workspace muestra el nombre y la descripción de la tarea. Sin embargo, puede agregar otra información, como fecha de creación o fecha límite. También puede añadir iconos y cambiar el estilo de la pantalla.

![Una mirada a la pestaña HTML Workspace To-do que muestra la configuración predeterminada](assets/html-todo-list.png)

Este artículo detalla los pasos para agregar información para mostrar para cada tarea en la lista Tareas pendientes.

## Qué se puede añadir {#what-can-be-added}

Puede añadir la información disponible en `task.json` enviado por el servidor. La información se puede añadir como texto sin formato o puede utilizar estilos para dar formato a la información.

Para obtener más información sobre la descripción del objeto JSON, consulte [this](/help/forms/using/html-workspace-json-object-description.md) artículo.

## Visualización de información sobre una tarea {#displaying-information-on-a-task}

1. Siga las [Pasos genéricos para la personalización del espacio de trabajo de AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md).
1. Para mostrar información adicional para una tarea, se deben agregar los pares de clave-valor correspondientes dentro del bloque de tareas de `translation.json`.

   Por ejemplo, cambiar `/apps/ws/locales/en-US/translation.json` para inglés:

   ```json
   "task" : {
           "reminder" : {
               "value" : "Reminder",
               "tooltip" : "This is reminder __reminderCount__, for this task."
           },
           "deadlined" : {
               "value" : "Deadlined",
               "tooltip" : "This task has deadlined"
           },
           "save" : {
               "message" : "Task has been saved successfully"
           },
           "status" : {
               "deadlined" : "Deadlined",
               "created" : "Created",
               "assignedsaved" : "Draft from assigned task",
               "terminated" : "Terminated",
               "assigned" : "Assigned",
               "unknown" : "Unknown",
               "createdsaved" : "Draft from created task",
               "completed" : "Completed"
           },
           "draft" : {
               "value" : "Saved",
               "tooltip" : "This task is marked as a draft"
           },
           "escalated" : {
               "value" : "Escalated",
               "tooltip" : "This task has been escalated"
           },
           "forward" : {
               "value" : "Forwarded",
               "tooltip" : "This task was forwarded"
           },
           "priority" : {
               "highest" : "Highest priority",
               "normal" : "Normal priority",
               "high" : "High priority",
               "low" : "Low priority",
               "lowest" : "Lowest priority"
           },
           "claimed" : {
               "value" : "Claimed",
               "tooltip" : "This task has been claimed"
           },
           "locked" : {
               "value" : "Locked",
               "tooltip" : "This task is locked"
           },
           "consulted" : {
               "value" : "Consulted",
               "tooltip" : "This task has been consulted"
           },
           "returned" : {
               "value" : "Returned",
               "tooltip" : "This task was returned back"
           },
           "multiplesubmitbuttons" : {
               "message" : "The form associated with this task has multiple submit buttons so the Workspace Complete button will be disabled. Click the appropriate button on the form to submit it."
           },
           "nosubmitbutton" : {
               "message" : "The form associated with this task does not appear to have submit buttons. You may need to upgrade your Adobe Reader version to 9.1 or greater and enable the Reader Submit option in your process."
           },
           "icon" : {
               "tooltip" : "open the task __taskName__"
           }
       }
   ```

   >[!NOTE]
   >
   >Agregue los pares de clave-valor correspondientes para todos los idiomas compatibles.

1. Por ejemplo, agregue información dentro del bloque de tareas:

   ```json
   "stepname" : {
               "value" : "Step Name",
               "tooltip" : "This task belongs to __stepName__ step"
   }
   ```

## Definición de CSS para la nueva propiedad {#defining-css-for-the-new-property}

1. Puede aplicar estilo a la información (propiedad) añadida a una tarea. Para ello, debe agregar información de estilo para la nueva propiedad agregada a `/apps/ws/css/newStyle.css`.

   Por ejemplo, agregue:

   ```css
   .task .taskProperties .stepname{
       width: 25px;
       background: url(../images/stepname.png) no-repeat; /*-------- Or just reuse background image / image-sprite defined .task .taskProperties span of style.css---------------------*/
       background-position: 0px 0px; /*-------- Dummy values, need to be configured as per user background image / image-sprite ---------------------*/
   }
   ```

## Adición de una entrada en la plantilla de HTML {#adding-entry-in-the-html-template}

Finalmente, debe incluir una entrada en el paquete dev para cada propiedad que desee agregar a la tarea. Para crear una, consulte Creación del código de espacio de trabajo de AEM Forms .

1. Copiar `task.html`:

   * de: `/libs/ws/js/runtime/templates/`
   * hasta: `/apps/ws/js/runtime/templates/`

1. Agregue la nueva información a `/apps/ws/js/runtime/templates/task.html`.

   Por ejemplo, agregue debajo de `div class="taskProperties"`:

   ```jsp
   <span class="stepname" alt="<%= $.t('task.stepname.value')%>" title = '<%= $.t("task.stepname.tooltip",{stepName:stepName})%>'/>
   ```
