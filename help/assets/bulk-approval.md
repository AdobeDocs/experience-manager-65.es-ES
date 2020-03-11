---
title: Revisión de los recursos y las colecciones de carpetas
description: Configure flujos de trabajo de revisión para recursos dentro de una carpeta o colección y compártalos con revisores o socios creativos para obtener comentarios.
contentOwner: AG
translation-type: tm+mt
source-git-commit: e71b87b12d45bf12f29af917fddebeddedb18056

---


# Revisión de los recursos y las colecciones de carpetas {#review-folder-assets-and-collections}

Configure flujos de trabajo de revisión para recursos dentro de una carpeta o colección y compártalos con revisores o socios creativos para obtener comentarios.

Recursos Adobe Experience Manager (AEM) le permite configurar un flujo de trabajo de revisión ad-hoc para los recursos de una carpeta o colección y compartirlo con revisores o socios creativos para obtener comentarios.

Puede asociar el flujo de trabajo de revisión con un proyecto o crear una tarea de revisión independiente.

Después de compartir los recursos, los revisores pueden aprobarlos o rechazarlos. Las notificaciones se envían en varias etapas del flujo de trabajo para notificar a los destinatarios previstos la realización de diversas tareas. Por ejemplo, cuando comparte una carpeta o colección, el revisor recibe una notificación de que se ha compartido una carpeta o colección para su revisión.

Una vez que el revisor haya completado la revisión (aprueba o rechaza recursos), recibirá una notificación de finalización de la revisión.

## Crear una tarea de revisión para carpetas {#creating-a-review-task-for-folders}

1. En la interfaz de usuario de Recursos, seleccione la carpeta para la que desea crear una tarea de revisión.
1. From the toolbar, tap **[!UICONTROL Create Review Task]** to open the **[!UICONTROL Review Task]** page. If you cannot see the option in the toolbar, tap/click **[!UICONTROL More]** and then select the option.

   ![chlimage_1-403](assets/chlimage_1-403.png)

1. (Opcional) En la lista **[!UICONTROL Proyecto]** , seleccione el proyecto al que desea asociar la tarea de revisión. De forma predeterminada, está seleccionada la opción **[!UICONTROL Ninguno]** . Si no desea asociar ningún proyecto con la tarea de revisión, mantenga esta selección.

   >[!NOTE]
   >
   >En la lista **[!UICONTROL Proyectos]** solo están visibles los proyectos para los que tiene permisos de nivel Editor (o superior).

1. Escriba un nombre para la tarea de revisión y seleccione un aprobador en la lista **[!UICONTROL Asignar a]** .

   >[!NOTE]
   >
   >Los miembros o grupos del proyecto seleccionado están disponibles como aprobadores en la lista **[!UICONTROL Asignar a]** .

1. Introduzca una descripción, la prioridad de la tarea y la fecha de vencimiento de la tarea de revisión.

   ![task_details](assets/task_details.png)

1. En la ficha Avanzado, escriba una etiqueta para crear el URI.

   ![review_name](assets/review_name.png)

1. Pulse o haga clic en **[!UICONTROL Enviar]** y, a continuación, pulse o haga clic en **[!UICONTROL Listo]** para cerrar el mensaje de confirmación. Se envía una notificación para la nueva tarea al aprobador.
1. Inicie sesión en Recursos AEM como aprobador y vaya a la interfaz de usuario de Recursos. Para aprobar recursos, toque **[!UICONTROL Notificaciones]** y, a continuación, seleccione la tarea de revisión en la lista.

   ![Notificación de activos](assets/aemAssetsNotification.png)

1. En la página **[!UICONTROL Revisar tarea]**, examine los detalles de la tarea de revisión y, a continuación, pulse o haga clic en **[!UICONTROL Revisar]**.
1. In the **[!UICONTROL Review Task]** page, select assets, and tap **[!UICONTROL Approve/Reject]** to approve or reject, as appropriate.

   ![review_task](assets/review_task.png)

1. Tap **[!UICONTROL Complete]** from the toolbar. En el cuadro de diálogo, escriba un comentario y toque o haga clic en **[!UICONTROL Completar]** para confirmar.
1. Vaya a la interfaz de usuario de Recursos y abra la carpeta. Los iconos de estado de aprobación de los recursos aparecen en la vista de tarjeta y en la vista de lista.

   **Vista de tarjeta**

   ![Revisar el estado como se ve en la vista de tarjeta](assets/chlimage_1-404.png)

   **Vista de lista**

   ![Revisar el estado como se ve en la vista de lista](assets/review_status_listview.png)

## Crear una tarea de revisión para colecciones {#creating-a-review-task-for-collections}

1. En la página Colecciones, seleccione la colección para la que desea crear una tarea de revisión.
1. From the toolbar, tap **[!UICONTROL Create Review Task]** to open the **[!UICONTROL Review Task]** page. If you cannot see the option on the toolbar, tap **[!UICONTROL More]** and then select the option.

   ![chlimage_1-405](assets/chlimage_1-405.png)

1. (Opcional) En la lista **[!UICONTROL Proyecto]** , seleccione el proyecto al que desea asociar la tarea de revisión. De forma predeterminada, está seleccionada la opción **[!UICONTROL Ninguno]** . Si no desea asociar ningún proyecto con la tarea de revisión, mantenga esta selección.

   >[!NOTE]
   >
   >En la lista **[!UICONTROL Proyectos]** solo están visibles los proyectos para los que tiene permisos de nivel Editor (o superior).

1. Escriba un nombre para la tarea de revisión y seleccione un aprobador en la lista **[!UICONTROL Asignar a]** .

   >[!NOTE]
   >
   >Los miembros o grupos del proyecto seleccionado están disponibles como aprobadores en la lista **[!UICONTROL Asignar a]** .

1. Introduzca una descripción, la prioridad de la tarea y la fecha de vencimiento de la tarea de revisión.

   ![task_details-collection](assets/task_details-collection.png)

1. Pulse o haga clic en **[!UICONTROL Enviar]** y, a continuación, pulse o haga clic en **[!UICONTROL Listo]** para cerrar el mensaje de confirmación. Se envía una notificación para la nueva tarea al aprobador.
1. Inicie sesión en Recursos AEM como aprobador y vaya a la consola Recursos. Para aprobar recursos, toque **[!UICONTROL Notificaciones]** y, a continuación, seleccione la tarea de revisión en la lista.
1. En la página **[!UICONTROL Revisar tarea]**, examine los detalles de la tarea de revisión y, a continuación, pulse o haga clic en **[!UICONTROL Revisar]**.
1. Todos los recursos de la colección están visibles en la página de revisión. Seleccione los recursos y toque **[!UICONTROL Aprobar/Rechazar]** para aprobarlos o rechazarlos, según corresponda.

   ![review_task_collection](assets/review_task_collection.png)

1. Tap **[!UICONTROL Complete]** from the toolbar. En el cuadro de diálogo, escriba un comentario y toque o haga clic en **[!UICONTROL Completar]** para confirmar.
1. Vaya a la consola Colecciones y abra la colección. Los iconos de estado de aprobación de los recursos aparecen en las vistas Tarjeta y Lista.

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   *Figura: Vista de tarjeta*

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

   *Figura: Vista de lista*
