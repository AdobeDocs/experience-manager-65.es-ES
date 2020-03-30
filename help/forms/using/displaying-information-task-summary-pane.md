---
title: Visualización de información en el panel Resumen de Tarea
seo-title: Visualización de información en el panel Resumen de Tarea
description: En el espacio de trabajo de AEM Forms, se puede configurar un panel Resumen de Tarea para resumir la tarea o mostrar cualquier otra página web.
seo-description: En el espacio de trabajo de AEM Forms, se puede configurar un panel Resumen de Tarea para resumir la tarea o mostrar cualquier otra página web.
uuid: 2fcc3d9f-0ec2-4250-8dc1-9746fd72ea60
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 90d0f584-b598-4b21-85d7-31da5f13d404
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Visualización de información en el panel Resumen de Tarea {#displaying-information-in-the-task-summary-pane}

Al abrir una tarea en el espacio de trabajo de AEM Forms, un panel Resumen de Tarea puede mostrar un resumen de la tarea. Esta información adicional y relevante para una tarea añade más valor al usuario final del espacio de trabajo de AEM Forms.

El espacio de trabajo de AEM Forms permite mostrar una página web de su elección en el panel Resumen de Tarea. Se puede crear un proceso para mostrar un panel Resumen de Tarea mediante Workbench.

1. Cree un proceso de asignación de Tareas en Workbench. Para obtener más información sobre la operación Asignar Tarea, consulte el tema Referencia de servicio en la Ayuda [de](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/)Workbench.

   >[!NOTE]
   >
   >Si existe una dirección URL de TaskSummary, la vista Resumen de Tarea se abre de forma predeterminada en lugar de la vista Formulario. En este caso, incluso cuando un usuario activa la opción &quot;Abrir el formulario en modo maximizado&quot; en Asignar Tarea, el formulario no se abre en modo maximizado.

1. Configure el campo URL de resumen de Tarea. Puede especificar un valor literal, una plantilla, una variable o una expresión XPath.
1. A continuación se muestra un ejemplo de visualización de la información en la página Resumen de Tarea.

   * Inicie sesión en el entorno CRXDE Lite en `https://'[server]:[port]'/lc/crx/de`.
   * `Create a node`**SampleSummary **` under `/` with type `content:`. In the properties of this node, add `unstructuredsling:` of type String and value ``. In the Access Control List of this node, add an entry for `resourceTypeSampleSummaryPERM_WORKSPACE_` allowing `USERjcr:read` privileges.`
   * `Create a folder`**SampleSummary **en`/apps`. En la Lista de Control de acceso de`/apps/SampleSummary`, agregue una entrada para`PERM_WORKSPACE_USER`permitir`jcr:readprivileges`.
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

   * Defina el valor de la URL de resumen de tarea como `/lc/content/SampleSummary.html` en el paso Asignar Tarea.
   * Cuando la tarea asociada con este paso Asignar Tarea se abre en el espacio de trabajo de AEM Forms, el `html.esp` at `/apps/SampleSummary` se procesa en el panel de resumen de tarea.


[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
