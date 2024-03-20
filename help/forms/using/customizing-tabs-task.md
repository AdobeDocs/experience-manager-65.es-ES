---
title: Personalizar pestañas para una tarea
description: Personalizar los nombres de las pestañas de las tareas, en AEM Forms Workspace de LiveCycle.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 8412cfec-bcab-40b7-9e5b-fcc211d43c0b
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 100%

---

# Personalizar pestañas para una tarea {#customizing-tabs-for-a-task}

Puede personalizar los nombres de las pestañas para el componente `Start Process` en la `Start Process` vista Uber y el componente `Task Details` en la `ToDo` vista Uber.

1. Siga los [Pasos genéricos para personalizar AEM Forms Workspace](/help/forms/using/generic-steps-html-workspace-customization.md).
1. Cambiar el valor de `tabname` en el archivo `translation.json`.

   Por ejemplo, cambie `/apps/ws/locales/en-US/translation.json` al inglés para lo siguiente.

   * Para las tareas iniciadas en el proceso de inicio, utilice el siguiente fragmento del bloque `"startprocess" : {}`.

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * Para las tareas en Tareas pendientes, use el siguiente fragmento del bloque `"todo" : {}`.

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
