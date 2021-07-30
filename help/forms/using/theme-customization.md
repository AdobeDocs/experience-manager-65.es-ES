---
title: Personalización de temas
seo-title: Personalización de temas
description: Cómo personalizar el tema de la aplicación de AEM Forms.
seo-description: Cómo personalizar el tema de la aplicación de AEM Forms.
uuid: 36632e67-1cc6-416d-ae80-d84bbabab4bd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: c72f608e-052a-4bf9-b7bc-ddf57483af35
exl-id: 9b8c5933-b783-48f9-b463-15a01e06ee98
source-git-commit: 6bc228866aca785ec768daefb73970fc24568ef0
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Personalización de temas {#theme-customization}

Puede personalizar el código HTML y el archivo CSS para proporcionar a la aplicación AEM Forms un aspecto y una presentación distintos específicos de la organización. Por ejemplo, puede cambiar el color de fondo y la altura de las tareas o puntos de inicio. El ejemplo siguiente proporciona instrucciones para cambiar:

* instrucciones de visualización en lugar de la descripción
* número de rutas de visualización
* color de degradado de fondo

## Etapas {#steps}

1. Abra el proyecto.

   * Para iOS, abra `Capture.xcodeproj` en Xcode
   * Para Android, abra el proyecto de Android en Eclipse.
   * Para Windows, abra `MWSWindows.sln` en Visual Studio.

1. Vaya a la carpeta de plantillas.

   * En Xcode, vaya a la carpeta **Capture > www > wsmobile > js > runtime > templates** .
   * En Eclipse, vaya a la carpeta **assets > www > wsmobile > js > runtime > templates** .
   * En Visual Studio, vaya a la carpeta **MWSWinwindows > www > wsmobile > js > runtime > templates**.

1. Abra el archivo `template.html` para editarlo.
1. Busque la siguiente cadena:

   ```jsp
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else
   ```

   Sustitúyalo por `<%`.

1. Busque el siguiente código en el archivo `template.html`:

   ```jsp
   <ul id="task_menu_list">
                                   <li class="approve" title="<%= task.availableCommands.directCommands[0]%>" data-routename="<%= task.availableCommands.directCommands[0]%>">
                                       <%= task.availableCommands.directCommands[0]%>
                                   </li>
                                   <li class="reject last" title="<%= task.availableCommands.directCommands[1]%>" data-routename="<%= task.availableCommands.directCommands[1]%>">
                                       <%= task.availableCommands.directCommands[1]%>
                                   </li>
   ```

1. Comente la siguiente línea y guarde el archivo.

   ```jsp
   task.availableCommands.directCommands[1]%>">
   <%= task.availableCommands.directCommands[1]%>
   </li>
   ```

1. Vaya a la carpeta css.

   * En Xcode, vaya a **Capture > www > wsmobile > css**.
   * En Eclipse, vaya a **assets > www > wsmobile > css**.
   * En Visual Studio, vaya a **MWSWinwindows > www > wsmobile > css**.

1. Abra el archivo `_style.css` para editarlo.
1. Para la imagen de fondo, cambie `#323232` a `#fff`.
1. Guarde los cambios y cierre el archivo `_style.css`.
1. Abra la aplicación de AEM Forms.

   La aplicación AEM Forms ahora muestra instrucciones en lugar de descripción.
