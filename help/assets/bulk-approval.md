---
title: Revisar recursos y colecciones de carpetas
description: Configure flujos de trabajo de revisión para los recursos de una carpeta o colección y compártalos con revisores o socios creativos para obtener comentarios.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 4%

---


# Revisar recursos y colecciones de carpetas {#review-folder-assets-and-collections}

Configure flujos de trabajo de revisión para los recursos de una carpeta o colección y compártalos con revisores o socios creativos para obtener comentarios.

Recursos Adobe Experience Manager le permite configurar un flujo de trabajo de revisión ad-hoc para los recursos de una carpeta o colección, y compartirlo con revisores o socios creativos para obtener comentarios.

Puede asociar el flujo de trabajo de revisión con un proyecto o crear una tarea de revisión independiente.

Después de compartir los recursos, los revisores pueden aprobarlos o rechazarlos. Las notificaciones se envían en varias etapas del flujo de trabajo para notificar a los destinatarios previstos la finalización de diversas tareas. Por ejemplo, cuando comparte una carpeta o colección, el revisor recibe una notificación de que se ha compartido una carpeta o colección para su revisión.

Una vez que el revisor haya completado la revisión (aprueba o rechaza recursos), recibirá una notificación de finalización de la revisión.

## Crear una tarea de revisión para carpetas {#creating-a-review-task-for-folders}

1. En la interfaz de usuario de Recursos, seleccione la carpeta para la que desea crear una tarea de revisión.
1. From the toolbar, click **[!UICONTROL Create Review Task]** to open the **[!UICONTROL Review Task]** page. If you cannot see the option in the toolbar, click **[!UICONTROL More]** and then select the option.

   ![chlimage_1-403](assets/chlimage_1-403.png)

1. (Opcional) En la lista **[!UICONTROL Proyecto]** , seleccione el proyecto al que desea asociar la tarea de revisión. De forma predeterminada, está seleccionada la opción **[!UICONTROL Ninguno]** . Si no desea asociar ningún proyecto con la tarea de revisión, mantenga esta selección.

   >[!NOTE]
   >
   >En la lista **[!UICONTROL Proyectos]** solo están visibles los proyectos para los que tiene permisos de nivel Editor (o superior).

1. Introduzca un nombre para la tarea de revisión y seleccione un aprobador en la lista **[!UICONTROL Asignar a]** .

   >[!NOTE]
   >
   >Los miembros o grupos del proyecto seleccionado están disponibles como aprobadores en la lista **[!UICONTROL Asignar a]** .

1. Introduzca una descripción, la prioridad de tarea y la fecha de vencimiento de la tarea de revisión.

   ![tarea_details](assets/task_details.png)

1. En la ficha Avanzado, escriba una etiqueta para crear el URI.

   ![review_name](assets/review_name.png)

1. Click **[!UICONTROL Submit]**, and then click **[!UICONTROL Done]** to close the confirmation message. Se envía una notificación para la nueva tarea al aprobador.
1. Inicie sesión en Recursos como aprobador y vaya a la interfaz de usuario de Recursos. Para aprobar recursos, haga clic en **[!UICONTROL Notificaciones]** y, a continuación, seleccione la tarea de revisión en la lista.

   ![Notificación de activos](assets/aemAssetsNotification.png)

1. In the **[!UICONTROL Review Task]** page, examine the details of the review task, and then click **[!UICONTROL Review]**.
1. In the **[!UICONTROL Review Task]** page, select assets, and click **[!UICONTROL Approve/Reject]** to approve or reject, as appropriate.

   ![review_tarea](assets/review_task.png)

1. Click **[!UICONTROL Complete]** from the toolbar. En el cuadro de diálogo, introduzca un comentario y haga clic en **[!UICONTROL Completar]** para confirmar.
1. Vaya a la interfaz de usuario de Recursos y abra la carpeta. Los iconos de estado de aprobación de los recursos aparecen en la vista de lista y vista de tarjetas.

   **Vista de tarjeta**

   ![Revisar el estado como se ve en la vista de la tarjeta](assets/chlimage_1-404.png)

   **Vista de lista**

   ![Revisar el estado como se ve en la vista de lista](assets/review_status_listview.png)

## Crear una tarea de revisión para las colecciones {#creating-a-review-task-for-collections}

1. En la página Colecciones, seleccione la colección para la que desea crear una tarea de revisión.
1. From the toolbar, click **[!UICONTROL Create Review Task]** to open the **[!UICONTROL Review Task]** page. If you cannot see the option on the toolbar, click **[!UICONTROL More]** and then select the option.

   ![chlimage_1-405](assets/chlimage_1-405.png)

1. (Opcional) En la lista **[!UICONTROL Proyecto]** , seleccione el proyecto al que desea asociar la tarea de revisión. De forma predeterminada, está seleccionada la opción **[!UICONTROL Ninguno]** . Si no desea asociar ningún proyecto con la tarea de revisión, mantenga esta selección.

   >[!NOTE]
   >
   >En la lista **[!UICONTROL Proyectos]** solo están visibles los proyectos para los que tiene permisos de nivel Editor (o superior).

1. Introduzca un nombre para la tarea de revisión y seleccione un aprobador en la lista **[!UICONTROL Asignar a]** .

   >[!NOTE]
   >
   >Los miembros o grupos del proyecto seleccionado están disponibles como aprobadores en la lista **[!UICONTROL Asignar a]** .

1. Introduzca una descripción, la prioridad de tarea y la fecha de vencimiento de la tarea de revisión.

   ![tarea_details-collection](assets/task_details-collection.png)

1. Click **[!UICONTROL Submit]**, and then click **[!UICONTROL Done]** to close the confirmation message. Se envía una notificación para la nueva tarea al aprobador.
1. Inicie sesión en Recursos como aprobador y vaya a la consola Recursos. Para aprobar recursos, haga clic en **[!UICONTROL Notificaciones]** y, a continuación, seleccione la tarea de revisión en la lista.
1. In the **[!UICONTROL Review Task]** page, examine the details of the review task, and then click **[!UICONTROL Review]**.
1. Todos los recursos de la colección están visibles en la página de revisión. Seleccione los recursos y haga clic en **[!UICONTROL Aprobar/Rechazar]** para aprobarlos o rechazarlos, según corresponda.

   ![review_tarea_collection](assets/review_task_collection.png)

1. Click **[!UICONTROL Complete]** from the toolbar. En el cuadro de diálogo, introduzca un comentario y haga clic en **[!UICONTROL Completar]** para confirmar.
1. Vaya a la consola Colecciones y abra la colección. Los iconos de estado de aprobación de los recursos aparecen en las vistas Tarjeta y Lista.

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   *Figura: vista de tarjetas.*

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

   *Figura: vista de Lista.*
