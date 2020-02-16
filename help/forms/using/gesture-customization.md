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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Personalización de gestos {#gesture-customization}

Puede personalizar los gestos de la aplicación AEM Forms para proporcionar un método distinto de interacción con la aplicación. Por ejemplo, puede agregar nuevos gestos para abrir o cerrar una tarea o un punto de inicio.

## Personalización de gestos en la aplicación de AEM Forms {#to-customize-gestures-in-aem-forms-app}

En la aplicación de AEM Forms, el barrido izquierdo abre una nueva tarea o un punto de inicio, mientras que el barrido derecho no hace nada. En el ejemplo siguiente se proporcionan pasos para abrir una nueva tarea o un punto de inicio al realizar los gestos de barrido derecho en la aplicación de AEM Forms.

1. Abra el proyecto.

   * Para iOS, abra `Capture.xcodeproj` en Xcode
   * Para Android, abra el proyecto de Android en Eclipse.
   * Para Windows, abra `MWSWindows.sln` en Visual Studio.

1. Vaya a la carpeta de vistas y abra el `task.js` archivo para editarlo.

   * En Xcode, vaya a la carpeta **Captura > www > wsmobile > js > tiempo de ejecución > vistas** .
   * En Eclipse, vaya a la carpeta **assets > www > wsmobile > js > tiempo de ejecución > vistas** .
   * En Visual Studio, vaya a la carpeta **MWSWinwindows > www > wsmobile > js > tiempo de ejecución > vistas** .
   >[!NOTE]
   >
   >El archivo task.js contiene la vista de red troncal asociada a cada tarea o punto de inicio enumerada en las listas de tareas o puntos de inicio.

1. En el `task.js` archivo, busque la propiedad events de la vista.

   La propiedad events es un mapa con cada entrada en el formato:

   `"EventName Selector": "Function"`

   Cuando se activa un evento de Javascript denominado `EventName`en un elemento HTML especificado por `Selector`, `Function`se llama a.

1. Buscar

   * &quot;toque .taskContentArea&quot; : &quot;onTaskClick&quot;,

      &quot;toque .taskOpenArea&quot; : &quot;onTaskClick&quot;,

      &quot;toque .task-content&quot; : &quot;onTaskClick&quot;,

      &quot;toque .last_empty_div&quot; : &quot;onTaskClick&quot;,
   y reemplazar por

   * &quot;swipe.taskContentArea&quot; : &quot;onTaskClick&quot;,

      &quot;swipe.taskOpenArea&quot; : &quot;onTaskClick&quot;,

      &quot;barrido.task-content&quot;: &quot;onTaskClick&quot;,

      &quot;swipe.last_empty_div&quot; : &quot;onTaskClick&quot;,


1. Guarde y cierre el `task.js` archivo.
1. Cree y ejecute la aplicación de AEM Forms. Ahora puede abrir una ventana con barrido izquierdo y barrido derecho.

Del mismo modo, puede realizar cambios en otras vistas para diversas combinaciones de gestos, elementos HTML y funciones.

**[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)**
