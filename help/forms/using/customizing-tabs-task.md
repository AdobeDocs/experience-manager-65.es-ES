---
title: Personalización de pestañas para una tarea
seo-title: Customizing tabs for a task
description: Personalización de los nombres de las pestañas de las tareas, en el espacio de trabajo de AEM Forms de LiveCycle.
seo-description: How-to customize the names of the tabs for your tasks, in LiveCycle AEM Forms workspace.
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
exl-id: 8412cfec-bcab-40b7-9e5b-fcc211d43c0b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# Personalización de pestañas para una tarea {#customizing-tabs-for-a-task}

Puede personalizar los nombres de las fichas para el `Start Process` en el `Start Process` La vista Uber y la `Task Details` en el `ToDo` Vista Uber.

1. Siga las [Pasos genéricos para la personalización del espacio de trabajo de AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md).
1. Cambiar el valor de `tabname`en el `translation.json` archivo.

   Por ejemplo, cambie `/apps/ws/locales/en-US/translation.json` para inglés a lo siguiente.

   * Para las tareas iniciadas en el proceso de inicio, utilice el siguiente fragmento de la sección `"startprocess" : {}` bloque.

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * Para tareas en Tareas pendientes, use el siguiente fragmento de código de `"todo" : {}` bloque.

   ```json
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
   >Agregue el par clave-valor correspondiente a todos los idiomas compatibles.
