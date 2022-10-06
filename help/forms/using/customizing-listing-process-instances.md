---
title: Personalización de la lista de instancias de proceso
seo-title: Customizing the listing of process instances
description: Personalización de las propiedades mostradas en la instancia de proceso en el espacio de trabajo de AEM Forms.
seo-description: How-to customize the properties displayed in process instance in AEM Forms workspace.
uuid: 3b55d9b9-7f73-46dd-9eb6-42be218440a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 40d7d43f-ee0a-4e34-ae93-20c9c940f76b
exl-id: b27ffe92-8491-43a0-bf42-613eb39a606e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 4%

---

# Personalización de la lista de instancias de proceso {#customizing-the-listing-of-process-instances}

La lista de instancias de proceso se muestra en la pestaña Tracking del espacio de trabajo de AEM Forms.

En la lista de instancias de proceso, para cada instancia de proceso, el espacio de trabajo de AEM Forms muestra algunas propiedades de esa instancia. Las siguientes propiedades están disponibles para cada instancia de proceso. Estas propiedades se almacenan como atributos en el modelo de componentes de instancias de proceso y están disponibles para su uso en su vista y plantilla.

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Comentarios</strong></td>
  </tr>
  <tr>
   <td>Descripción</td>
   <td>Descripción de la instancia de proceso.</td>
  </tr>
  <tr>
   <td>iniciador</td>
   <td>Nombre del iniciador de la instancia de proceso.</td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>ID del iniciador de la instancia de proceso.</td>
  </tr>
  <tr>
   <td>processCompleteTime</td>
   <td>Marca de hora cuando se completó el proceso.</td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>ID de la instancia de proceso.</td>
  </tr>
  <tr>
   <td>processInstanceStatus</td>
   <td>0 = Iniciado<br /> 1 = En ejecución<br /> 2 = Completo<br /> 3 = Finalización<br /> 4 = Terminado<br /> 5 = Finalización<br /> 6 = Suspendido<br /> 7 = Suspender<br /> 8 = Sin suspensión</td>
  </tr>
  <tr>
   <td>processName</td>
   <td>Nombre del proceso.</td>
  </tr>
  <tr>
   <td>processStartTime</td>
   <td>Marca de tiempo cuando se inició el proceso.</td>
  </tr>
  <tr>
   <td>processVariables</td>
   <td>Matriz de objetos de variables de proceso. Cada objeto de variable de proceso contiene <strong>name</strong> (el nombre de la variable de proceso), <strong>value</strong> (valor de la variable de proceso), y<strong> type</strong> (el tipo de variable de proceso).</td>
  </tr>
 </tbody>
</table>

**Ejemplo:**

Para mostrar el `description` de la instancia de proceso en la tarjeta de instancia de proceso, realice los siguientes pasos.

1. Siga las [Pasos genéricos para la personalización del espacio de trabajo de AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md).
1. Haga lo siguiente:

   1. Copie /libs/ws/js/runtime/templates/processinstance.html a/apps/ws/js/runtime/templates/, si no existe. Haga clic en **Guardar todo**.
   1. Añada div de descripción del proceso con class = &#39;processDescription&#39; inprocessinstance.html.

   ```jsp
   <div class="processDescription" title="<%= description%>"><%= description%></div>
   ```

1. Haga lo siguiente:

   1. Abra /apps/ws/js/registry.js para editarlo.
   1. Buscar y reemplazar `text!/lc/libs/ws/js/runtime/templates/processinstance.html`con `text!/lc/`**apps**/ws/js/runtime/templates/processinstance.html.

1. Los cambios anteriores pueden requerir una actualización del archivo CSS añadiendo una entrada en la hoja de estilo /apps/ws/css/newStyle.css de la siguiente manera:

   ```css
   .processinstance .processDescription {
    <!--Dummy values, need to be configured by user as per requirement as well as user can add or delete any property depending upon requirement-->
       width : 250px;
       font-size : 11pt;
       padding : 2px;
   }
   ```
