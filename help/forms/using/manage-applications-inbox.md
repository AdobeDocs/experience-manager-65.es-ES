---
title: Administrar aplicaciones y tareas de Forms en AEM Bandeja de entrada
seo-title: Administrar aplicaciones y tareas de Forms en AEM Bandeja de entrada
description: AEM bandeja de entrada le permite iniciar flujos de trabajo centrados en Forms mediante el envío de aplicaciones y la administración de tareas.
seo-description: AEM bandeja de entrada le permite iniciar flujos de trabajo centrados en Forms mediante el envío de aplicaciones y la administración de tareas.
uuid: c6c0d8ea-743f-4852-99d1-69fd50a0994e
contentOwner: vishgupt
topic-tags: document_services, publish
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dd11fd83-3df1-4727-8340-8c5426812823
docset: aem65
translation-type: tm+mt
source-git-commit: d324586eb1d4fb809bf87641001b92a1941e6548
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 2%

---


# Administrar aplicaciones y tareas de Forms en AEM Bandeja de entrada{#manage-forms-applications-and-tasks-in-aem-inbox}

Una de las muchas maneras de iniciar o déclencheur un flujo de trabajo centrado en Forms es a través de las aplicaciones de AEM Bandeja de entrada. Debe crear una aplicación de flujo de trabajo para que un flujo de trabajo de Forms esté disponible como aplicación en la Bandeja de entrada. Para obtener más información sobre la aplicación de flujo de trabajo y otras formas de iniciar flujos de trabajo de Forms, consulte [Iniciar un flujo de trabajo centrado en Forms en OSGi](../../forms/using/aem-forms-workflow.md#launch).

Además, AEM Bandeja de entrada consolida las notificaciones y tareas de diversos componentes de AEM, incluidos los flujos de trabajo de Forms. Cuando se activa un flujo de trabajo de formularios que contiene un paso Asignar tarea, la aplicación asociada aparece como una tarea en la Bandeja de entrada del usuario asignado. Si el usuario asignado es un grupo, la tarea aparece en la Bandeja de entrada de todos los miembros del grupo hasta que un individuo reclame o delega la tarea.

La interfaz de usuario de la Bandeja de entrada proporciona vistas de lista y calendario a tareas de vista. También puede configurar la vista. Puede filtrar tareas en función de varios parámetros. Para obtener más información sobre la vista y los filtros, consulte [Su bandeja de entrada](/help/sites-authoring/inbox.md).

En resumen, la Bandeja de entrada permite crear una nueva aplicación y administrar las tareas asignadas.

>[!NOTE]
>
>Debe ser miembro del grupo de usuarios del flujo de trabajo para poder utilizar AEM Bandeja de entrada.

## Crear aplicación {#create-application}

1. Vaya a AEM Bandeja de entrada en https://&#39;[server]:[port]&#39;/aem/inbox.
1. En la interfaz de usuario de la bandeja de entrada, toque **[!UICONTROL Crear > Aplicación]**. Aparece la página Seleccionar aplicación.
1. Seleccione una aplicación y haga clic en **[!UICONTROL Crear]**. Se abre el formulario adaptable asociado a la aplicación. Rellene la información del formulario adaptable y toque **[!UICONTROL Enviar]**. Inicia el flujo de trabajo asociado y crea una tarea en la Bandeja de entrada del usuario asignado.

## Administrar tareas {#manage-tasks}

Cuando un flujo de trabajo de Forms déclencheur y usted es un usuario asignado o parte del grupo de usuarios asignados, aparecerá una tarea en la Bandeja de entrada. Puede vista de los detalles de la tarea y realizar las acciones disponibles en la tarea desde la Bandeja de entrada.

### Reclamar o delegar tareas {#claim-or-delegate-tasks}

Las tareas asignadas a un grupo aparecen en la Bandeja de entrada de todos los miembros del grupo. Cualquier miembro del grupo puede reclamar esa tarea o delegarla en otro miembro del grupo. Para ello:

1. Toque para seleccionar la miniatura de la tarea. Las opciones para abrir o delegar la tarea aparecen en la parte superior.

   ![select-tarea](assets/select-task.png)

1. Realice una de las acciones siguientes:

   * Para delegar la tarea, toque **[!UICONTROL Delegar]**. Se Abre El Cuadro De Diálogo Delegar Elemento. Seleccione un usuario, opcionalmente agregue un comentario y toque **[!UICONTROL Aceptar]**.

   ![delegate](assets/delegate.png)

   * Para reclamar la tarea, toque **[!UICONTROL Abrir]**. Se abre el cuadro de diálogo Asignar a sí mismo. Toque **[!UICONTROL Continuar]** para reclamar la tarea. La tarea reclamada aparece con usted como el usuario asignado en la Bandeja de entrada.

   ![reclamar](assets/claim.png)

### Detalles de vista y realizar acciones en tareas {#view-details-and-perform-actions-on-tasks}

Al abrir una tarea, puede realizar vistas de los detalles de la tarea y realizar las acciones disponibles. Las acciones disponibles para una tarea se definen en el paso Asignar tarea del flujo de trabajo de Forms asociado.

1. Toque para seleccionar la miniatura de la tarea. Las opciones para abrir o delegar la tarea seleccionada aparecen en la parte superior.
1. Toque **Abrir** para obtener detalles de la tarea de vista y realizar acciones. Se abre la vista de tarea detallada. En esta vista, puede realizar vistas en los detalles de tarea y realizar acciones en la tarea.

   >[!NOTE]
   >
   >Si se asigna una tarea a un grupo, debe reclamarla para que pueda abrirla en una vista detallada.

![tarea-detalles](assets/task-details.png)

La vista detallada de la tarea comprende las siguientes secciones:

* Detalles de tarea
* Formulario 
* Detalles de flujo de trabajo
* Barra de herramientas Acciones

#### Detalles de tarea {#task-details}

La sección Detalles de Tarea muestra información sobre la tarea. La información mostrada depende de la configuración del [paso Asignar tarea](/help/sites-developing/workflows-step-ref.md) del flujo de trabajo. En el ejemplo anterior se muestra la descripción, el estado, la fecha de inicio y el flujo de trabajo utilizados para la tarea. También permite adjuntar un archivo a la tarea.

#### Formulario {#form}

La ficha Formulario del área de contenido principal muestra los datos adjuntos del formulario y del campo enviados, si los hay.

#### Detalles de flujo de trabajo {#workflow-details}

La ficha Detalles del flujo de trabajo de la parte superior muestra el progreso de la tarea en varias etapas del flujo de trabajo. Muestra las etapas completadas, actuales y pendientes de la tarea. Las etapas de un flujo de trabajo se definen en el [paso Asignar tarea](/help/sites-developing/workflows-step-ref.md) del flujo de trabajo asociado.

Además, la ficha muestra el historial de tareas de cada etapa completada en el flujo de trabajo. Puede tocar **[!UICONTROL Detalles de Vista]** para una etapa completa para conocer los detalles de esa etapa. Muestra comentarios, datos adjuntos de formulario y tarea, estado, fechas de inicio y finalización, etc., sobre la tarea.

![workflow-details](assets/workflow-details.png)

#### Barra de herramientas Acciones {#actions-toolbar}

La barra de herramientas Acciones muestra todas las opciones disponibles para la tarea. Mientras Guardar, Restablecer y Delegar son acciones predeterminadas, otras acciones disponibles se configuran en [Asignar paso de tarea](/help/sites-developing/workflows-step-ref.md). En el ejemplo anterior, Aprobar y Rechazar están configurados en el flujo de trabajo.

A medida que realiza una acción en la tarea, esta continúa en el flujo de trabajo.

### Tareas completadas de vista {#view-completed-tasks}

AEM bandeja de entrada solo muestra tareas activas. Las tareas completadas no aparecen en la lista. Sin embargo, puede utilizar filtros de la Bandeja de entrada para filtrar tareas en función de varios parámetros, como el tipo de tarea, el estado, las fechas de inicio y finalización, etc. Para vista tareas completadas:

1. En AEM Bandeja de entrada, toque ![toggle-side-panel1](assets/toggle-side-panel1.png) para abrir el selector de filtros.
1. Toque **[!UICONTROL Estado de Tarea]** acordeón y seleccione **[!UICONTROL Completar]**. Aparecerán todas las tareas completadas.

   ![filter](assets/filter.png)

1. Toque para seleccionar una tarea y haga clic en **[!UICONTROL Abrir]**.

La tarea se abre para mostrar el documento o el formulario adaptable asociado con la tarea. En el caso de los formularios adaptables, la tarea muestra el formulario adaptable de sólo lectura o su documento de registro en PDF, tal como se ha configurado en la ficha Formulario/Documento del [paso del flujo de trabajo Asignar Tarea](/help/sites-developing/workflows-step-ref.md).

La sección Detalles de la tarea muestra información como la acción realizada, el estado de la tarea, la fecha de inicio y la fecha de finalización.

![tarea completada](assets/completed-task.png)

La ficha **[!UICONTROL Detalles del flujo de trabajo]** muestra cada paso del flujo de trabajo. Toque **[!UICONTROL Detalles de la Vista]** para obtener información detallada.

![complete-tarea-workflow](assets/completed-task-workflow.png)

## Solución de problemas {#troubleshooting-workflows}

### No se pueden vista los elementos relacionados con AEM flujo de trabajo en AEM bandeja de entrada {#unable-to-see-aem-worklow-items}

El propietario de un modelo de flujo de trabajo no puede vista elementos relacionados con AEM flujo de trabajo en AEM bandeja de entrada. Para resolver el problema, agregue los siguientes índices al repositorio de AEM y vuelva a compilar el índice.

1. Utilice uno de los siguientes métodos para agregar índices:

   * Cree los siguientes nodos en CRX DE en `/oak:index/workflowDataLucene/indexRules/granite:InboxItem/properties` con las propiedades correspondientes, como se especifica en la tabla siguiente:

      | Nodo | Propiedad | Tipo |
      |---|---|---|
      | sharedWith | sharedWith | CADENA |
      | bloqueado | bloqueado | BOOLEANO |
      | devuelto | devuelto | BOOLEANO |
      | allowInboxSharing | allowInboxSharing | BOOLEANO |
      | allowExpliedSharing | allowExpliedSharing | BOOLEANO |


   * Implemente los índices mediante un paquete AEM. Puede utilizar un proyecto [AEM Archetype](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/developing/archetype) para crear un paquete de AEM implementable. Utilice el siguiente código de muestra para agregar índices a un proyecto de Arquetipo AEM:

   ```Java
      .property("sharedWith", "sharedWith").type(TYPENAME_STRING).propertyIndex()
      .property("locked", "locked").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("returned", "returned").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("allowInboxSharing", "allowInboxSharing").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("allowExplicitSharing", "allowExplicitSharing").type(TYPENAME_BOOLEAN).propertyIndex()
   ```

1. [Cree un índice de propiedades y configúrelo en true](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/queries-and-indexing.html#the-property-index).

1. Después de configurar los índices en CRX DE o de implementar mediante un paquete, [vuelva a indexar el repositorio](https://helpx.adobe.com/in/experience-manager/kb/HowToCheckLuceneIndex.html#Completelyrebuildtheindex).

https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/queries-and-indexing.html
