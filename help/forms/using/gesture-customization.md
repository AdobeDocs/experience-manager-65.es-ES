---
title: Personalizar gestos
description: Aprenda a personalizar los gestos en la aplicación AEM Forms. Puede personalizar los gestos para proporcionar un método distinto de interactuar con la aplicación.
uuid: 117e0e21-66bd-42f1-879c-6c1443991974
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 747d13d3-e7cc-4aa1-bcc8-4b57157e71ed
exl-id: 6debb1a7-7889-4fdd-87c7-ecb87cc0b1f5
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 82%

---

# Personalizar gestos {#gesture-customization}

Puede personalizar los gestos de la aplicación AEM Forms para proporcionar un método distinto de interactuar con la aplicación. Por ejemplo, puede añadir nuevos gestos para abrir o cerrar una tarea o un punto de inicio.

## Personalizar los gestos en la aplicación AEM Forms {#to-customize-gestures-in-aem-forms-app}

En la aplicación AEM Forms, el gesto de deslizar el dedo hacia la izquierda abre una nueva tarea o un punto de inicio, mientras que el gesto de deslizar el dado hacia la derecha no realiza ninguna acción. En el siguiente ejemplo se proporcionan los pasos para abrir una nueva tarea o un punto de inicio deslizando el dedo hacia la derecha en la aplicación AEM Forms.

1. Abra su proyecto.

   * Si utiliza un dispositivo iOS, abra `Capture.xcodeproj` en Xcode.
   * Si utiliza un dispositivo Android, abra el proyecto de Android en Eclipse.
   * Si utiliza un dispositivo Windows, abra `MWSWindows.sln` en Visual Studio.

1. Vaya a la carpeta views y abra el archivo `task.js` para editarlo.

   * En Xcode, vaya a la carpeta **Capture > www > wsmobile > js > runtime > views**.
   * En Eclipse, vaya a la carpeta **assets > www > wsmobile > js > runtime > views**.
   * En Visual Studio, vaya a la carpeta **MWSWindows > www > wsmobile > js > runtime > views**.

   >[!NOTE]
   >
   >El archivo task.js contiene la vista de Backbone asociada a todas las tareas o puntos de inicio que aparecen en las listas de tareas o puntos de inicio.

1. Busque la propiedad events de la vista en el archivo `task.js`.

   La propiedad events es un mapa que contiene todas las entradas con el formato:

   `"EventName Selector": "Function"`

   Al almacenar en déclencheur un evento de JavaScript denominado `EventName`en un elemento de HTML especificado por `Selector`, el `Function`se llama.

1. Busque

   * &quot;select .taskContentArea&quot; : &quot;onTaskClick&quot;,

     &quot;select .taskOpenArea&quot; : &quot;onTaskClick&quot;,

     &quot;select .task-content&quot; : &quot;onTaskClick&quot;,

     &quot;select .last_empty_div&quot; : &quot;onTaskClick&quot;,

   y reemplácelo por

   * &quot;swipe .taskContentArea&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .taskOpenArea&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .task-content&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .last_empty_div&quot; : &quot;onTaskClick&quot;,

1. Guarde y cierre el archivo `task.js`.
1. Genere y ejecute la aplicación AEM Forms. Ahora puede realizar la acción Abrir deslizando el dedo a la izquierda y a la derecha.

Del mismo modo, puede realizar cambios en otras vistas para utilizar diversas combinaciones de gestos, elementos HTML y funciones.
