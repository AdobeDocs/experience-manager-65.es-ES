---
title: Personalización de imágenes utilizadas en acciones de ruta
seo-title: Personalización de imágenes utilizadas en acciones de ruta
description: Personalización de las imágenes utilizadas en las acciones de ruta en el espacio de trabajo de LiveCycle AEM Forms.
seo-description: Personalización de las imágenes utilizadas en las acciones de ruta en el espacio de trabajo de LiveCycle AEM Forms.
uuid: 42608376-587e-4b57-a9d5-8f9ebd981426
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 10158c13-47b4-43e3-ac47-690f3cbab158
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Personalización de imágenes utilizadas en acciones de ruta {#customize-images-used-in-route-actions}

Para personalizar las imágenes utilizadas en las acciones de ruta, realice los pasos descritos en Pasos [genéricos de personalización](/help/forms/using/generic-steps-html-workspace-customization.md) seguidos de los pasos descritos en este artículo.

## Imágenes para acciones de ruta {#images-for-route-actions}

1. Agregue los estilos que definen imágenes en la CSS en la siguiente ubicación para las nuevas acciones de ruta:

   `/apps/ws/css/newStyle.css`

   Por ejemplo: Agregue un nuevo estilo llamado `myStyle1`como se muestra a continuación y cargue el archivo de imagen `myStyleIcon1.png` en la carpeta `/apps/ws/image`s mediante un cliente WebDAV.

   >[!NOTE]
   >
   >Para obtener más información sobre el acceso a WebDAV, consulte [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

   >[!NOTE]
   >
   >Prefiere que el nombre del estilo sea el mismo que el nombre de la acción de ruta.

   ```css
   .myStyle1{
   
           background-image: url('../images/myStyleIcon1.png');
   
       }
   ```

## Ventana emergente de acción de tarea Lista de tareas {#task-list-task-action-popup}

1. Cree una ventana emergente de acción de lista de tareas, consulte [Creación del código](/help/forms/using/introduction-customizing-html-workspace.md#main-pars-heading-3)del espacio de trabajo de AEM Forms. Requiere usar el paquete dev.

1. Copiar `/libs/ws/js/runtime/templates/task.html` a `/apps/ws/js/runtime/templates/task.html`.

1. Si el nombre del estilo CSS es el mismo que el nombre de la acción de ruta procedente del servidor, modifique el siguiente código en `/apps/ws/js/runtime/templates/task.html`:

   ```
   <%if(routeList == null){%>
               <li>
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li>
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
               </li>
               <%}%>
               <%}%>
   
   To
   
   <%if(routeList == null){%>
               <li class="<%= availableCommands.directCommands[0]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li class="<%= availableCommands.directCommands[i]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
               </li>
               <%}%>
               <%}%>
   ```

1. Si el nombre del estilo CSS es diferente del nombre de la acción de ruta que proviene del servidor, modifique el siguiente código en `/apps/ws/js/runtime/templates/task.html`. Agrega una pila de las condiciones del `if-else` servlet para asignar el estilo con el nombre de la acción de ruta.

```
<%if(routeList == null){%>
            <li>
                <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
            </li>
            <%}else{%>
            <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
            <li>
                <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
            </li>
            <%}%>
            <%}%>

To

<%if(routeList == null){%>
            <li class="<%= availableCommands.directCommands[0]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0]+'.value')%>">
                <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
            </li>
            <%}else{%>
            <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
                <%if(availableCommands.directCommands[i].equals("myAction1")){%>
                     <li class="myStyle1" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                         <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                     </li>
                <%}else if(availableCommands.directCommands[i].equals("myAction2")){%>
                     <li class="myStyle2" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                         <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                     </li>
                <%}%>
            <%}%>
            <%}%>
```

## Ventana emergente de acción de tarea Detalles de tarea {#task-details-task-action-popup}

1. Copiar `/libs/ws/js/runtime/templates/taskdetails.html` a `/apps/ws/js/runtime/templates/taskdetails.html`.

1. Si el nombre del estilo CSS es el mismo que el nombre de la acción de ruta procedente del servidor, modifique el siguiente código en `/apps/ws/js/runtime/templates/taskdetails.html`:

   ```
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                           </li>
                       <%}%>
   
   To
   
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                       <%}%>
   ```

1. Si el nombre del estilo CSS es diferente del nombre de la acción de ruta que proviene del servidor, modifique el siguiente código en `/apps/ws/js/runtime/templates/taskdetails.html`. Agrega una pila de condiciones de `if-else` servlet para asignar el estilo con el nombre de la acción de ruta.

   ```
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                           </li>
                       <%}%>
   
   To
   
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                   <%if(availableCommands.directCommands[i].equals("myAction1")){%>
                       <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="myStyle1" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                   <%}else if(availableCommands.directCommands[i].equals("myAction2")){%>
                       <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="myStyle2" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                   <%}%>
               <%}%>
   ```

1. Abra `/apps/ws/js/registry.js` para editar y busque el siguiente texto:
   `"text!/lc/libs/ws/js/runtime/templates/taskdetails.html"`

1. Sustitúyase el texto por el siguiente:
   `"text!/lc/apps/ws/js/runtime/templates/taskdetails.html"`

**[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)**
