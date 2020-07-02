---
title: Configurar operaciones asincrónicas en [!DNL Adobe Experience Manager].
description: Efectúe de forma asincrónica algunas tareas con gran cantidad de recursos para optimizar el rendimiento en [!DNL Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 18b81ba3fcf15838ac9bebd451f4ad8b0b6e3bbb
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 2%

---


# Operaciones asincrónicas {#asynchronous-operations}

Para reducir el impacto negativo en el rendimiento, [!DNL Adobe Experience Manger Assets] procesa de forma asíncrona ciertas operaciones de activos de larga duración y con gran densidad de recursos. El procesamiento asincrónico implica poner en cola varias tareas y, finalmente, ejecutarlas en serie, según la disponibilidad de los recursos del sistema. Estas operaciones incluyen:

* Eliminación de muchos recursos.
* Mover muchos recursos o recursos con muchas referencias.
* Exportación e importación masiva de metadatos de recursos.
* Obtención de recursos de una implementación remota [!DNL Experience Manager] , que superan el límite de umbral establecido. El límite es el número de recursos.

Puede vista del estado de las tareas asincrónicas desde la página Estado **[!UICONTROL del trabajo]** asincrónico.

>[!NOTE]
>
>De forma predeterminada, las [!DNL Assets] tareas se ejecutan en paralelo. Si `N` es el número de núcleos de CPU, `N/2` las tareas se pueden ejecutar en paralelo de forma predeterminada. Para utilizar la configuración personalizada de la cola de tareas, modifique la configuración de la cola **[!UICONTROL predeterminada de operaciones]** asincrónicas desde la consola web. Para obtener más información, consulte Configuraciones [de cola](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations).

## Monitorear el estado de las operaciones asincrónicas {#monitoring-the-status-of-asynchronous-operations}

Siempre que [!DNL Assets] procese una operación de forma asíncrona, recibirá una notificación en la [!DNL Experience Manager] Bandeja de entrada [](/help/sites-authoring/inbox.md) y por correo electrónico. Para realizar una vista detallada del estado de las operaciones asincrónicas, vaya a la página Estado **[!UICONTROL del trabajo]** asincrónico.

1. En la [!DNL Experience Manager] interfaz, haga clic en **[!UICONTROL Operaciones]** > **[!UICONTROL Trabajos]**.

1. En la página Estado **[!UICONTROL del trabajo]** asincrónico, revise los detalles de las operaciones.

   ![Estado y detalles de las operaciones asincrónicas](assets/AsyncOperation-status.png)

   Para comprobar el progreso de una operación, consulte la columna **[!UICONTROL Estado]** . Según el progreso, se muestra uno de los siguientes estados:

   * **[!UICONTROL Activo]**: La operación se está procesando.
   * **[!UICONTROL Correcto]**: Se completó la operación.
   * **[!UICONTROL Fallo]** o **[!UICONTROL Error]**: No se pudo procesar la operación.
   * **[!UICONTROL Programado]**: La operación está programada para procesarse más tarde.

1. Para detener una operación activa, selecciónela en la lista y haga clic en **[!UICONTROL Detener]** icono ![de](assets/do-not-localize/stop_icon.svg) detención en la barra de herramientas.

1. Para vista de detalles adicionales, por ejemplo descripción y registros, seleccione la operación y haga clic en **[!UICONTROL Abrir]** ![open_icon](assets/do-not-localize/edit_icon.svg) en la barra de herramientas. Se muestra la página de detalles de la tarea.

   ![Detalles de una tarea de importación de metadatos](assets/job_details.png)

1. Para eliminar la operación de la lista, seleccione **[!UICONTROL Eliminar]** en la barra de herramientas. Para descargar los detalles en un archivo CSV, haga clic en **[!UICONTROL Descargar]**.

   >[!NOTE]
   >
   >No puede eliminar una tarea si su estado está activo o en cola.

## Purgar tareas completadas {#purge-completed-tasks}

[!DNL Experience Manager Assets] ejecuta una tarea de depuración todos los días a las 1.00 horas para eliminar tareas asincrónicas completadas que tienen más de un día de antigüedad.

<!-- TBD: Find out from the engineering team and mention the time zone of this 1:00 am task.
-->

Puede modificar la programación de la tarea de depuración y la duración durante la cual se conservan los detalles de las tareas completadas antes de que se eliminen. También puede configurar el número máximo de tareas completadas para las que se conservan los detalles en cualquier momento.

1. En la [!DNL Experience Manager] interfaz, haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > Consola **** web.
1. Abra la tarea Depuración programada **[!UICONTROL de trabajos asincrónicos de]** Adobe CQ DAM.
1. Especifique el número de umbral de días después de los cuales se eliminan las tareas completadas y el número máximo de tareas para las que se conservan los detalles en el historial. Guarde los cambios.

   ![Configuración para programar la depuración de tareas asincrónicas](assets/configmgr_purge_asyncjobs.png)

## Configurar umbral para operaciones de eliminación asincrónica {#configure-thresholds-for-asynchronous-delete-operations}

Si el número de recursos o carpetas que se van a eliminar supera el número de umbral establecido, la operación de eliminación se realiza de forma asíncrona.

1. En la [!DNL Experience Manager] interfaz, haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > Consola **** web.
1. En la consola web, abra la configuración Procesamiento **[!UICONTROL de trabajos de operación de eliminación]** asincrónica.
1. En el cuadro **[!UICONTROL Umbral de número de recursos]** , especifique los números de umbral para eliminar de forma asíncrona recursos, carpetas o referencias. Guarde los cambios.

   ![Establecer el límite de umbral para la tarea de eliminación de recursos](assets/delete_threshold.png)

## Configurar umbral para operaciones de movimiento asincrónico {#configure-thresholds-for-asynchronous-move-operations}

Si el número de recursos, carpetas o referencias que se van a mover supera el número de umbral establecido, la operación de movimiento se realiza de forma asíncrona.

1. En la [!DNL Experience Manager] interfaz, haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > Consola **** web.
1. En la consola web, abra la configuración Procesamiento **[!UICONTROL de trabajos de operación de movimiento]** asincrónico.
1. En el cuadro **[!UICONTROL Umbral número de recursos/referencias]** , especifique los números de umbral para mover recursos, carpetas o referencias de forma asíncrona. Guarde los cambios.

   ![Establecer el límite de umbral para que la tarea mueva recursos](assets/move_threshold.png)

>[!MORELIKETHIS]
>
>* [Configure el correo electrónico en el Experience Manager](/help/sites-administering/notification.md).
>* [Importe y exporte metadatos de recursos de forma masiva](/help/assets/metadata-import-export.md).
>* [Utilice Recursos conectados para compartir recursos DAM de implementaciones](/help/assets/use-assets-across-connected-assets-instances.md)remotas.

