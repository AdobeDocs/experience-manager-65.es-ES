---
title: Personalización de fichas para una tarea
seo-title: Personalización de fichas para una tarea
description: Personalización de los nombres de las fichas de las tareas en el espacio de trabajo de LiveCycle AEM Forms.
seo-description: Personalización de los nombres de las fichas de las tareas en el espacio de trabajo de LiveCycle AEM Forms.
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Personalización de fichas para una tarea {#customizing-tabs-for-a-task}

Puede personalizar los nombres de fichas del `Start Process` componente en la vista `Start Process` Uber y del `Task Details` componente en la vista `ToDo` Uber.

1. Siga los pasos [genéricos para personalizar](/help/forms/using/generic-steps-html-workspace-customization.md)el espacio de trabajo de AEM Forms.
1. Cambie el valor de `tabname`en el `translation.json` archivo.

   Por ejemplo, cambie `/apps/ws/locales/en-US/translation.json` para inglés a lo siguiente.

   * Para las tareas iniciadas en el proceso de inicio, utilice el siguiente fragmento del `"startprocess" : {}` bloque.

   ```
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * Para tareas en Tareas pendientes, utilice el siguiente fragmento del `"todo" : {}` bloque.

   ```
   "tabname" : {
               "summary" : "Bird's-eye view",
               "history" : "Past",
               "form" : "Form",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Notes"
   }
   ```

   >[!NOTE]
   >
   >Agregue el par clave-valor correspondiente para todos los idiomas admitidos.

[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
