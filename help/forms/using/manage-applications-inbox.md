---
title: Administrar aplicaciones y tareas de formularios en la bandeja de entrada de AEM
seo-title: Administrar aplicaciones y tareas de formularios en la bandeja de entrada de AEM
description: La bandeja de entrada de AEM le permite iniciar flujos de trabajo centrados en Forms mediante el envío de aplicaciones y la administración de tareas.
seo-description: La bandeja de entrada de AEM le permite iniciar flujos de trabajo centrados en Forms mediante el envío de aplicaciones y la administración de tareas.
uuid: c6c0d8ea-743f-4852-99d1-69fd50a0994e
contentOwner: vishgupt
topic-tags: publish
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dd11fd83-3df1-4727-8340-8c5426812823
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Administrar aplicaciones y tareas de formularios en la bandeja de entrada de AEM{#manage-forms-applications-and-tasks-in-aem-inbox}

Una de las muchas formas de iniciar o activar un flujo de trabajo centrado en formularios es a través de las aplicaciones de la Bandeja de entrada de AEM. Debe crear una aplicación de flujo de trabajo para que un flujo de trabajo de formularios esté disponible como aplicación en la Bandeja de entrada. Para obtener más información sobre la aplicación de flujo de trabajo y otras formas de iniciar flujos de trabajo de formularios, consulte [Iniciar un flujo de trabajo centrado en formularios en OSGi](../../forms/using/aem-forms-workflow.md#launch).

Además, AEM Inbox consolida las notificaciones y tareas de varios componentes de AEM, incluidos los flujos de trabajo de formularios. Cuando se activa un flujo de trabajo de formularios que contiene un paso Asignar tarea, la aplicación asociada aparece como una tarea en la Bandeja de entrada del usuario asignado. Si el usuario asignado es un grupo, la tarea aparece en la Bandeja de entrada de todos los miembros del grupo hasta que un individuo reclame o delega la tarea.

La interfaz de usuario de la Bandeja de entrada proporciona vistas de lista y calendario a tareas de vista. También puede configurar la vista. Puede filtrar tareas en función de varios parámetros. Para obtener más información sobre la vista y los filtros, consulte [Su bandeja de entrada](/help/sites-authoring/inbox.md).

En resumen, la Bandeja de entrada permite crear una nueva aplicación y administrar las tareas asignadas.

>[!NOTE] {graybox=&quot;true&quot;}
>
>Debe ser miembro del grupo de usuarios del flujo de trabajo para poder utilizar la Bandeja de entrada de AEM.

## Crear aplicación {#create-application}

1. Vaya a la bandeja de entrada de AEM en https://&#39;[server]:[port]&#39;/aem/inbox.
1. En la interfaz de usuario de la bandeja de entrada, toque **[!UICONTROL Crear > Aplicación]**. Aparece la página Seleccionar aplicación.
1. Seleccione una aplicación y haga clic en **[!UICONTROL Crear]**. Se abre el formulario adaptable asociado a la aplicación. Rellene la información del formulario adaptable y toque **[!UICONTROL Enviar]**. Inicia el flujo de trabajo asociado y crea una tarea en la Bandeja de entrada del usuario asignado.

## Administrar tareas {#manage-tasks}

Cuando se activa un flujo de trabajo de Forms y usted es un usuario asignado o parte del grupo asignado, aparece una tarea en la Bandeja de entrada. Puede vista de los detalles de la tarea y realizar las acciones disponibles en la tarea desde la Bandeja de entrada.

### Reclamar o delegar tareas {#claim-or-delegate-tasks}

Las Tareas asignadas a un grupo aparecen en la Bandeja de entrada de todos los miembros del grupo. Cualquier miembro del grupo puede reclamar esa tarea o delegarla en otro miembro del grupo. Para ello:

1. Toque para seleccionar la miniatura de la tarea. Las opciones para abrir o delegar la tarea aparecen en la parte superior.

   ![select-tarea](assets/select-task.png)

1. Realice una de las acciones siguientes:

   * Para delegar la tarea, toque **[!UICONTROL Delegar]**. Se Abre El Cuadro De Diálogo Delegar Elemento. Seleccione un usuario, agregue un comentario de forma opcional y toque **[!UICONTROL Aceptar]**.
   ![delegate](assets/delegate.png)

   * Para solicitar la tarea, toque **[!UICONTROL Abrir]**. Se abre el cuadro de diálogo Asignar a sí mismo. Toque **[!UICONTROL Continuar]** para reclamar la tarea. La tarea reclamada aparece con usted como el usuario asignado en la Bandeja de entrada.
   ![reclamar](assets/claim.png)

### Detalles de Vista y realización de acciones en tareas {#view-details-and-perform-actions-on-tasks}

Al abrir una tarea, puede realizar vistas de los detalles de la tarea y realizar las acciones disponibles. Las acciones disponibles para una tarea se definen en el paso Asignar tarea del flujo de trabajo de formularios asociado.

1. Toque para seleccionar la miniatura de la tarea. Las opciones para abrir o delegar la tarea seleccionada aparecen en la parte superior.
1. Toque **Abrir** en detalles de tarea de vista y realice acciones. Se abre la vista de tarea detallada. En esta vista, puede realizar vistas en los detalles de tarea y realizar acciones en la tarea.

   >[!NOTE]
   >
   >Si se asigna una tarea a un grupo, debe reclamarla para que pueda abrirla en una vista detallada.

![tarea-detalles](assets/task-details.png)

La vista detallada de la tarea comprende las siguientes secciones:

* Detalles de Tarea
* Formulario 
* Detalles del flujo de trabajo
* Barra de herramientas Acciones

#### Task details {#task-details}

La sección Detalles de Tarea muestra información sobre la tarea. La información mostrada depende de la configuración del paso [](/help/sites-developing/workflows-step-ref.md) Asignar tarea en el flujo de trabajo. En el ejemplo anterior se muestra la descripción, el estado, la fecha de inicio y el flujo de trabajo utilizados para la tarea. También permite adjuntar un archivo a la tarea.

#### Formulario {#form}

La ficha Formulario del área de contenido principal muestra los datos adjuntos del formulario y del campo enviados, si los hay.

#### Workflow details {#workflow-details}

La ficha Detalles del flujo de trabajo de la parte superior muestra el progreso de la tarea en varias etapas del flujo de trabajo. Muestra las etapas completadas, actuales y pendientes de la tarea. Las etapas de un flujo de trabajo se definen en el paso [](/help/sites-developing/workflows-step-ref.md) Asignar tarea del flujo de trabajo asociado.

Además, la ficha muestra el historial de tareas de cada etapa completada en el flujo de trabajo. Puede tocar Detalles **[!UICONTROL de]** Vista en una etapa completa para conocer los detalles de esa etapa. Muestra comentarios, datos adjuntos de formulario y tarea, estado, fechas de inicio y finalización, etc., sobre la tarea.

![workflow-details](assets/workflow-details.png)

#### Actions toolbar {#actions-toolbar}

La barra de herramientas Acciones muestra todas las opciones disponibles para la tarea. Mientras Guardar, Restablecer y Delegar son acciones predeterminadas, otras acciones disponibles se configuran en el paso [](/help/sites-developing/workflows-step-ref.md)Asignar tarea. En el ejemplo anterior, Aprobar y Rechazar están configurados en el flujo de trabajo.

A medida que realiza una acción en la tarea, esta continúa en el flujo de trabajo.

### tareas completadas de Vista {#view-completed-tasks}

La Bandeja de entrada de AEM solo muestra tareas activas. Las tareas completadas no aparecen en la lista. Sin embargo, puede utilizar filtros de la Bandeja de entrada para filtrar tareas en función de varios parámetros, como el tipo de tarea, el estado, las fechas de inicio y finalización, etc. Para vista tareas completadas:

1. En la Bandeja de entrada de AEM, toque ![alternar panel1](assets/toggle-side-panel1.png) para abrir el selector de filtros.
1. Toque el acordeón Estado **[!UICONTROL de]** Tarea y seleccione **[!UICONTROL Completar]**. Aparecerán todas las tareas completadas.

   ![filter](assets/filter.png)

1. Toque para seleccionar una tarea y haga clic en **[!UICONTROL Abrir]**.

La tarea se abre para mostrar el documento o el formulario adaptable asociado con la tarea. En el caso de los formularios adaptables, la tarea muestra el formulario adaptable de sólo lectura o su documento de registro en PDF, tal como se ha configurado en la ficha Formulario/Documento del paso [del flujo de trabajo](/help/sites-developing/workflows-step-ref.md)Asignar Tarea.

La sección Detalles de la tarea muestra información como la acción realizada, el estado de la tarea, la fecha de inicio y la fecha de finalización.

![tarea completada](assets/completed-task.png)

La ficha Detalles **[!UICONTROL del]** flujo de trabajo muestra cada paso del flujo de trabajo. Toque los detalles **[!UICONTROL de la]** Vista para obtener información detallada.

![complete-tarea-workflow](assets/completed-task-workflow.png)

