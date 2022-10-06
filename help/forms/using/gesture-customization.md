---
title: Personalización de gestos
seo-title: Gesture customization
description: Personalice los gestos en la aplicación de AEM Forms
seo-description: Customize the gestures on your AEM Forms app
uuid: 117e0e21-66bd-42f1-879c-6c1443991974
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 747d13d3-e7cc-4aa1-bcc8-4b57157e71ed
exl-id: 6debb1a7-7889-4fdd-87c7-ecb87cc0b1f5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 2%

---

# Personalización de gestos {#gesture-customization}

Puede personalizar los gestos de la aplicación de AEM Forms para proporcionar un método distinto de interacción con la aplicación. Por ejemplo, puede añadir nuevos gestos para abrir o cerrar una tarea o un punto de inicio.

## Para personalizar gestos en la aplicación de AEM Forms {#to-customize-gestures-in-aem-forms-app}

En la aplicación de AEM Forms, el barrido izquierdo abre una nueva tarea o un punto de inicio, mientras que el barrido derecho no hace nada. En el siguiente ejemplo se proporcionan los pasos para abrir una nueva tarea o un punto de inicio al realizar los gestos de barrido derecho en la aplicación AEM Forms.

1. Abra el proyecto.

   * Para iOS, abra `Capture.xcodeproj` en Xcode
   * Para Android, abra el proyecto de Android en Eclipse.
   * Para Windows, abra `MWSWindows.sln` en Visual Studio.

1. Vaya a la carpeta de vistas y abra la `task.js` para editar.

   * En Xcode, vaya a la **Captura > www > wsmobile > js > tiempo de ejecución > vistas** carpeta.
   * En Eclipse, vaya a la **assets > www > wsmobile > js > tiempo de ejecución > vistas** carpeta.
   * En Visual Studio, vaya a la **Windows MWSW > www > wsmobile > js > tiempo de ejecución > vistas** carpeta.

   >[!NOTE]
   >
   >El archivo task.js contiene la vista de la columna vertebral asociada a cada tarea o punto de inicio enumerada en las listas de tareas o puntos de inicio.

1. En el `task.js` , busque la propiedad events de la vista.

   La propiedad events es un mapa con cada entrada en formato :

   `"EventName Selector": "Function"`

   Cuando se déclencheur un evento de Javascript con el nombre `EventName`en un elemento HTML especificado por `Selector`, el `Function`se llama.

1. Buscar

   * &quot;toque .taskContentArea&quot; : &quot;onTaskClick&quot;,

      &quot;pulse .taskOpenArea&quot; : &quot;onTaskClick&quot;,

      &quot;toque .task-content&quot; : &quot;onTaskClick&quot;,

      &quot;pulse .last_empty_div&quot; : &quot;onTaskClick&quot;,
   y reemplace por

   * &quot;deslizar.taskContentArea&quot; : &quot;onTaskClick&quot;,

      &quot;deslizar.taskOpenArea&quot; : &quot;onTaskClick&quot;,

      &quot;deslizar .task-content&quot; : &quot;onTaskClick&quot;,

      &quot;deslizar .last_empty_div&quot; : &quot;onTaskClick&quot;,


1. Guarde y cierre el archivo `task.js`.
1. Cree y ejecute la aplicación de AEM Forms. Ahora puede abrir un con el desliz izquierdo y el desliz derecho.

Del mismo modo, puede realizar cambios en otras vistas para diversas combinaciones de gestos, elementos HTML y funciones.
