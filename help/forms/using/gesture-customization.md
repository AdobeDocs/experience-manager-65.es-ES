---
title: Personalización de gestos
seo-title: Personalización de gestos
description: Personalización de los gestos en la aplicación de AEM Forms
seo-description: Personalización de los gestos en la aplicación de AEM Forms
uuid: 117e0e21-66bd-42f1-879c-6c1443991974
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 747d13d3-e7cc-4aa1-bcc8-4b57157e71ed
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# Personalización de gestos {#gesture-customization}

Puede personalizar los gestos de la aplicación de AEM Forms para proporcionar un método distinto de interacción con la aplicación. Por ejemplo, puede agregar nuevos gestos para abrir o cerrar una tarea o un punto de inicio.

## Para personalizar gestos en la aplicación de AEM Forms {#to-customize-gestures-in-aem-forms-app}

En la aplicación de AEM Forms, el barrido izquierdo abre una nueva tarea o punto de inicio, mientras que el barrido derecho no hace nada. En el siguiente ejemplo se proporcionan pasos para abrir una nueva tarea o un punto de inicio al realizar los gestos de barrido derecho en la aplicación de AEM Forms.

1. Abra el proyecto.

   * Para iOS, abra `Capture.xcodeproj` en Xcode
   * Para Android, abra el proyecto de Android en Eclipse.
   * Para Windows, abra `MWSWindows.sln` en Visual Studio.

1. Vaya a la carpeta vistas y abra el archivo `task.js` para editarlo.

   * En Xcode, vaya a la carpeta **Capture > www > wsmobile > js > tiempo de ejecución > vistas**.
   * En Eclipse, vaya a la carpeta **assets > www > wsmobile > js > Runtime > vistas**.
   * En Visual Studio, vaya a la carpeta **MWSWinwindows > www > wsmobile > js > tiempo de ejecución > vistas**.

   >[!NOTE]
   >
   >El archivo tarea.js contiene la vista de red troncal asociada a cada tarea o punto de inicio que se enumera en las listas de tarea o punto de inicio.

1. En el archivo `task.js`, busque la propiedad eventos de la vista.

   La propiedad eventos es un mapa con cada entrada en el formato:

   `"EventName Selector": "Function"`

   Cuando se déclencheur un evento de JavaScript denominado `EventName`en un elemento HTML especificado por `Selector`, se llama a `Function`.

1. Buscar

   * &quot;toque .taskContentArea&quot; : &quot;onTaskClick&quot;,

      &quot;toque .taskOpenArea&quot; : &quot;onTaskClick&quot;,

      &quot;toque .tarea-contenido&quot; : &quot;onTaskClick&quot;,

      &quot;toque .last_empty_div&quot; : &quot;onTaskClick&quot;,
   y reemplazar por

   * &quot;swipe.taskContentArea&quot; : &quot;onTaskClick&quot;,

      &quot;swipe.taskOpenArea&quot; : &quot;onTaskClick&quot;,

      &quot;barrido .tarea-contenido&quot;: &quot;onTaskClick&quot;,

      &quot;swipe.last_empty_div&quot; : &quot;onTaskClick&quot;,


1. Guarde y cierre el archivo `task.js`.
1. Cree y ejecute la aplicación de AEM Forms. Ahora puede abrir una ventana con barrido izquierdo y barrido derecho.

Del mismo modo, puede realizar cambios en otras vistas para diversas combinaciones de gestos, elementos HTML y funciones.
