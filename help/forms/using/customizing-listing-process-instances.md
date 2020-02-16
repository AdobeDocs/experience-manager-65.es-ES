---
title: Personalización de la lista de instancias de proceso
seo-title: Personalización de la lista de instancias de proceso
description: Personalización de las propiedades que se muestran en la instancia de proceso en el espacio de trabajo de AEM Forms.
seo-description: Personalización de las propiedades que se muestran en la instancia de proceso en el espacio de trabajo de AEM Forms.
uuid: 3b55d9b9-7f73-46dd-9eb6-42be218440a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 40d7d43f-ee0a-4e34-ae93-20c9c940f76b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Personalización de la lista de instancias de proceso {#customizing-the-listing-of-process-instances}

La lista de instancias de proceso se muestra en la ficha Seguimiento del espacio de trabajo de AEM Forms.

En la lista de instancias de proceso, en cada instancia de proceso, el espacio de trabajo de AEM Forms muestra algunas propiedades de esa instancia. Las siguientes propiedades están disponibles para cada instancia de proceso. Estas propiedades se almacenan como atributos en el modelo de componentes de instancia de proceso y están disponibles para su uso en la vista y plantilla.

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
   <td>0 = Iniciado<br /> 1 = Ejecución<br /> 2 = Completado<br /> 3 = Finalización<br /> 4 = Terminado<br /> 5 = Terminación<br /> 6 = Suspendido<br /> 7 = Suspendido<br /> 8 = Sin suspensión</td>
  </tr>
  <tr>
   <td>processName</td>
   <td>Nombre del proceso.</td>
  </tr>
  <tr>
   <td>processStartTime</td>
   <td>Marca de hora cuando se inició el proceso.</td>
  </tr>
  <tr>
   <td>processVariables</td>
   <td>Matriz de objetos de variables de proceso. Cada objeto de variable de proceso contiene <strong>nombre</strong> (el nombre de la variable de proceso), <strong>valor</strong> (el valor de la variable de proceso) y tipo<strong></strong> (el tipo de variable de proceso).</td>
  </tr>
 </tbody>
</table>

**Ejemplo:**

Para mostrar la `description` propiedad de la instancia de proceso en la tarjeta de instancia de proceso, lleve a cabo los siguientes pasos.

1. Siga los pasos [genéricos para personalizar](/help/forms/using/generic-steps-html-workspace-customization.md)el espacio de trabajo de AEM Forms.
1. Haga lo siguiente:

   1. Copie /libs/ws/js/runtime/templates/processinstance.html a/apps/ws/js/Runtime/templates/, si no existe. Haga clic en **Guardar todo**.
   1. Agregue div de descripción del proceso con class = &#39;processDescription&#39; inprocessinstance.html.

   ```
   <div class="processDescription" title="<%= description%>"><%= description%></div>
   ```

1. Haga lo siguiente:

   1. Abra /apps/ws/js/registry.js para editar.
   1. Busque y reemplace `text!/lc/libs/ws/js/runtime/templates/processinstance.html`por `text!/lc/`**las aplicaciones **/ws/js/runtime/templates/processinstance.html.

1. Los cambios anteriores pueden requerir una actualización del archivo CSS mediante la adición de una entrada en la hoja de estilo /apps/ws/css/newStyle.css de la siguiente manera:

   ```css
   .processinstance .processDescription {
    <!--Dummy values, need to be configured by user as per requirement as well as user can add or delete any property depending upon requirement-->
       width : 250px;
       font-size : 11pt;
       padding : 2px;
   }
   ```

[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
