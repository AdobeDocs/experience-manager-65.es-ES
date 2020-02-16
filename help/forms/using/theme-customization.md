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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Personalización de temas {#theme-customization}

Puede personalizar el código HTML y el archivo CSS para proporcionar a la aplicación AEM Forms un aspecto y una presentación distintos específicos de la organización. Por ejemplo, puede cambiar el color y la altura de fondo de las tareas o los puntos de inicio. El siguiente ejemplo proporciona instrucciones para cambiar:

* mostrar instrucciones en lugar de la descripción
* número de rutas de visualización
* color de degradado de fondo

## Etapas {#steps}

1. Abra el proyecto.

   * Para iOS, abra `Capture.xcodeproj` en Xcode
   * Para Android, abra el proyecto de Android en Eclipse.
   * Para Windows, abra `MWSWindows.sln` en Visual Studio.

1. Vaya a la carpeta de plantillas.

   * En Xcode, vaya a la carpeta **Captura > www > wsmobile > js > tiempo de ejecución > plantillas** .
   * En Eclipse, vaya a la carpeta **assets > www > wsmobile > js > tiempo de ejecución > plantillas** .
   * En Visual Studio, vaya a la carpeta **MWSWinwindows > www > wsmobile > js > tiempo de ejecución > plantillas** .

1. Open the `template.html` file for editing.
1. Busque la siguiente cadena:

   ```
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else
   ```

   Sustitúyalo por `<%`.

1. Busque el código siguiente en el `template.html` archivo:

   ```
   <ul id="task_menu_list">
                                   <li class="approve" title="<%= task.availableCommands.directCommands[0]%>" data-routename="<%= task.availableCommands.directCommands[0]%>">
                                       <%= task.availableCommands.directCommands[0]%>
                                   </li>
                                   <li class="reject last" title="<%= task.availableCommands.directCommands[1]%>" data-routename="<%= task.availableCommands.directCommands[1]%>">
                                       <%= task.availableCommands.directCommands[1]%>
                                   </li>
   ```

1. Comente la siguiente línea y guarde el archivo.

   ```
   task.availableCommands.directCommands[1]%>">
   <%= task.availableCommands.directCommands[1]%>
   </li>
   ```

1. Vaya a la carpeta css.

   * En Xcode, vaya a **Capturar > www > wsmobile > css**.
   * En Eclipse, vaya a **assets > www > wsmobile > css**.
   * En Visual Studio, vaya a **MWSWinwindows > www > wsmobile > css**.

1. Open the `_style.css` file for editing.
1. Para la imagen Fondo, cambie `#323232` a `#fff`.
1. Guarde los cambios y cierre `_style.css` el archivo.
1. Abra la aplicación de AEM Forms.

   La aplicación AEM Forms ahora muestra instrucciones en lugar de descripciones.

[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
