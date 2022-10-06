---
title: Visualización de información en el panel Resumen de tareas
seo-title: Displaying information in the Task Summary pane
description: En el espacio de trabajo de AEM Forms, se puede configurar un panel Resumen de tareas para resumir la tarea o mostrar cualquier otra página web.
seo-description: In AEM Forms workspace, a Task Summary pane can be configured to summarize the task or display any other web page.
uuid: 2fcc3d9f-0ec2-4250-8dc1-9746fd72ea60
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 90d0f584-b598-4b21-85d7-31da5f13d404
exl-id: 0b3087fe-a3fb-4eac-ad4b-c123526e8195
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Visualización de información en el panel Resumen de tareas {#displaying-information-in-the-task-summary-pane}

Cuando se abre una tarea en el espacio de trabajo de AEM Forms, un panel Resumen de tareas puede mostrar un resumen de la tarea. Esta información adicional y relevante para una tarea añade más valor para el usuario final del espacio de trabajo de AEM Forms.

El espacio de trabajo de AEM Forms le permite mostrar una página web de su elección en el panel Resumen de tareas. Se puede crear un proceso para mostrar un panel Resumen de tareas utilizando Workbench.

1. Cree un proceso Asignar tarea en Workbench. Para obtener más información sobre la operación Asignar tarea, consulte el tema Referencia de servicio en [Ayuda de Workbench](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/).

   >[!NOTE]
   >
   >Si existe una URL de resumen de tareas, la vista Resumen de tareas se abre de forma predeterminada en lugar de la vista Formulario. En este caso, incluso cuando un usuario habilita la opción &quot;Abrir el formulario en modo maximizado&quot; en Asignar tarea, el formulario no se abre en modo maximizado.

1. Configure el campo URL de resumen de tareas . Puede especificar un valor literal, una plantilla, una variable o una expresión XPath.
1. A continuación se muestra un ejemplo de visualización de la información en la página Resumen de tareas.

   * Inicie sesión en el entorno de CRXDE Lite en `https://'[server]:[port]'/lc/crx/de`.
   * `Create a node`**SampleSummary** ` under `/content` with type `nt:unstructured`. In the properties of this node, add `sling:resourceType` of type String and value `SampleSummary`. In the Access Control List of this node, add an entry for `PERM_WORKSPACE_USER` allowing `jcr:read` privileges.`
   * `Create a folder`**SampleSummary** under `/apps`. En la Lista de control de acceso de `/apps/SampleSummary`, agregue una entrada para `PERM_WORKSPACE_USER` allow `jcr:readprivileges`.
   * `Create a file `html.esp` at `/apps/SampleSummary`. For example, add the following lines in `html.esp`.`

   ```html
   <html>
       <body>
           <h1>Sample Summary</h1>
           <br/>
           <p>Hello Sir!
               <br/>
               This is sample summary page for this task.
           </p>
       </body>
   </html>
   ```

   * Establezca el valor de la url del resumen de la tarea como `/lc/content/SampleSummary.html` en el paso Asignar tarea .
   * Cuando la tarea asociada con este paso Asignar tarea se abre en el espacio de trabajo de AEM Forms, la variable `html.esp` at `/apps/SampleSummary` se representa en el panel de resumen de tareas.
