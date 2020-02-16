---
title: Visualización de información en el panel Resumen de tareas
seo-title: Visualización de información en el panel Resumen de tareas
description: En el espacio de trabajo de AEM Forms, se puede configurar un panel de resumen de tareas para resumir la tarea o mostrar cualquier otra página web.
seo-description: En el espacio de trabajo de AEM Forms, se puede configurar un panel de resumen de tareas para resumir la tarea o mostrar cualquier otra página web.
uuid: 2fcc3d9f-0ec2-4250-8dc1-9746fd72ea60
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 90d0f584-b598-4b21-85d7-31da5f13d404
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Visualización de información en el panel Resumen de tareas {#displaying-information-in-the-task-summary-pane}

Al abrir una tarea en el espacio de trabajo de AEM Forms, un panel Resumen de tareas puede mostrar un resumen de la tarea. Esta información adicional y relevante para una tarea añade más valor al usuario final del espacio de trabajo de AEM Forms.

El espacio de trabajo de AEM Forms permite mostrar una página web de su elección en el panel Resumen de tareas. Se puede crear un proceso para mostrar un panel Resumen de tareas mediante Workbench.

1. Crear un proceso de asignación de tareas en Workbench. Para obtener más información sobre la operación Asignar tarea, consulte el tema Referencia de servicio en la Ayuda [de](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/)Workbench.

   >[!NOTE]
   >
   >Si existe una URL de resumen de tareas, la vista Resumen de tareas se abre de forma predeterminada en lugar de la vista Formulario. En este caso, incluso cuando un usuario activa la opción &quot;Abrir el formulario en modo maximizado&quot; en Asignar tarea, el formulario no se abre en modo maximizado.

1. Configure el campo URL de resumen de tareas. Puede especificar un valor literal, una plantilla, una variable o una expresión XPath.
1. A continuación se muestra un ejemplo de visualización de la información en la página Resumen de tareas.

   * Inicie sesión en el entorno CRXDE Lite en `https://[server]:[port]/lc/crx/de`.
   * `Create a node`**SampleSummary **` under `/` with type `content:`. In the properties of this node, add `unstructuredsling:` of type String and value ``. In the Access Control List of this node, add an entry for `resourceTypeSampleSummaryPERM_WORKSPACE_` allowing `USERjcr:read` privileges.`
   * `Create a folder`**SampleSummary **en`/apps`. En la lista de control de acceso de`/apps/SampleSummary`, agregue una entrada para`PERM_WORKSPACE_USER`permitir`jcr:readprivileges`.
   * `Create a file `html.esp` at `/apps/`. For example, add the following lines in `SampleSummaryhtml.esp`.`

   ```
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

   * Defina el valor de la dirección URL del resumen de tareas como `/lc/content/SampleSummary.html` en el paso Asignar tarea.
   * Cuando la tarea asociada con este paso Asignar tarea se abre en el espacio de trabajo de AEM Forms, el `html.esp` at `/apps/SampleSummary` se procesa en el panel de resumen de tareas.


[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
