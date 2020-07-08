---
title: Operaciones asincrónicas
description: Adobe Experience Manager optimiza el rendimiento completando de forma asíncrona algunas tareas que requieren muchos recursos.
translation-type: tm+mt
source-git-commit: 69b90432ac6028a64f36300819e1bead1ae8d671
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 2%

---


# Operaciones asincrónicas {#asynchronous-operations}

Para reducir el impacto negativo en el rendimiento, Adobe Experience Manager procesa de forma asíncrona determinadas operaciones de larga duración y con gran cantidad de recursos.

Estas operaciones incluyen:

* Eliminación de muchos recursos
* Desplazamiento de muchos recursos o recursos con muchas referencias
* Exportación e importación masiva de metadatos de recursos
* Recuperación de recursos, que están por encima del límite establecido, desde una implementación de Experience Manager remoto
* Desplazamiento de páginas
* Despliegue de Live Copies

El procesamiento asincrónico implica poner en cola varios trabajos y ejecutarlos en serie, según la disponibilidad de los recursos del sistema.

Puede vista del estado de los trabajos asincrónicos desde el panel Estado **[!UICONTROL de trabajo]** asincrónico en Navegación **** global -> **Herramientas** -> **Operaciones** -> **Trabajos**.

>[!NOTE]
>
>De forma predeterminada, los trabajos asincrónicos se ejecutan en paralelo. Si *`n`* *`n/2`* es el número de núcleos de CPU, los trabajos se pueden ejecutar en paralelo, de forma predeterminada. Para utilizar la configuración personalizada para la cola de trabajos, modifique la configuración **[!UICONTROL predeterminada de cola de operaciones]** asincrónicas y la configuración **de movimiento y despliegue de página de operaciones** asincrónicas desde la consola web.
>
>Para obtener más información, consulte Configuraciones [de cola](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations).

## Monitorear el estado de las operaciones asincrónicas {#monitor-the-status-of-asynchronous-operations}

Siempre que AEM procese una operación de forma asíncrona, recibirá una notificación en la bandeja de entrada y por correo electrónico (si está activada).

Para realizar una vista detallada del estado de las operaciones asincrónicas, vaya a la página Estado **[!UICONTROL del trabajo]** asincrónico.

1. En la interfaz de Experience Manager, haga clic en **[!UICONTROL Operaciones]** > **[!UICONTROL Trabajos]**.

1. En la página Estado **[!UICONTROL del trabajo]** asincrónico, revise los detalles de las operaciones.

   ![Estado y detalles de las operaciones asincrónicas](assets/async-operation-status.png)

   Para determinar el progreso de una operación en particular, consulte el valor en la columna **[!UICONTROL Estado]** . Según el progreso, se muestra uno de los siguientes estados:

   * **[!UICONTROL Activo]**: Se está procesando la operación

   * **[!UICONTROL Correcto]**: Se completó la operación

   * **[!UICONTROL Fallo]** o **[!UICONTROL Error]**: No se pudo procesar la operación

   * **[!UICONTROL Programado]**: La operación está programada para procesarse más tarde

1. Para detener una operación activa, selecciónela en la lista y haga clic en **[!UICONTROL Detener]** en la barra de herramientas.

   ![stop_icon](assets/async-stop-icon.png)

1. Para vista de detalles adicionales, como descripción y registros, seleccione la operación y haga clic en **[!UICONTROL Abrir]** en la barra de herramientas.

   ![open_icon](assets/async-open-icon.png)

   Se muestra la página de detalles del trabajo.

   ![job_details](assets/async-job-details.png)

1. Para eliminar la operación de la lista, seleccione **[!UICONTROL Eliminar]** en la barra de herramientas. Para descargar los detalles en un archivo CSV, haga clic en **[!UICONTROL Descargar]**.

   >[!NOTE]
   >
   >No puede eliminar un trabajo si su estado es **Activo** o **En cola**.

## Purgar trabajos completados {#purging-completed-jobs}

AEM ejecuta un trabajo de depuración todos los días a las 01:00 para eliminar los trabajos asincrónicos completados que tengan más de un día de antigüedad.

Puede modificar la programación del trabajo de depuración y la duración durante la cual se conservan los detalles de los trabajos completados antes de que se eliminen. También puede configurar el número máximo de trabajos completados para los que se conservan los detalles en cualquier momento.

1. En Navegación global, haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > Consola **** web.
1. Abra el trabajo Trabajo **[!UICONTROL programado de depuración de trabajos asincrónicos de]** Adobe Granite.
1. Especifique:
   * El número de umbral de días después de los cuales se eliminan los trabajos completados.
   * Número máximo de trabajos para los que se conservan detalles en el historial.
   * La expresión de cron para cuándo debe ejecutarse la purga.
   ![Configuración para programar la depuración de trabajos asincrónicos](assets/async-purge-job.png)

1. Guarde los cambios.

## Configurar procesamiento asincrónico {#configuring-asynchronous-processing}

Puede configurar el número de umbral de recursos, páginas o referencias para que AEM procese una operación concreta de forma asincrónica, así como alternar las notificaciones por correo electrónico cuando se procesen los trabajos.

### Configurar operaciones de eliminación de recursos asincrónicos {#configuring-synchronous-delete-operations}

Si el número de recursos o carpetas que se van a eliminar supera el número de umbral, la operación de eliminación se realiza de forma asíncrona.

1. En Navegación global, haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > Consola **** web.
1. Desde la consola web, abra la configuración de cola predeterminada del proceso **[!UICONTROL asincrónico.]**
1. En el cuadro **[!UICONTROL Umbral de número de recursos]** , especifique el número de umbral de recursos/carpetas para el procesamiento asincrónico de las operaciones de eliminación.

   ![Umbral de eliminación de recursos](assets/async-delete-threshold.png)

1. Marque la opción **Habilitar notificación** por correo electrónico para recibir notificaciones por correo electrónico para este estado del trabajo. Por ejemplo: éxito, error.
1. Guarde los cambios.

### Configurar operaciones de movimiento de recursos asincrónicos {#configuring-asynchronous-move-operations}

Si el número de recursos/carpetas o referencias que se van a mover supera el número de umbral, la operación de movimiento se realiza de forma asíncrona.

1. En Navegación global, haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > Consola **** web.
1. Desde la consola web, abra la Configuración de procesamiento de trabajos de operación de movimiento **[!UICONTROL asincrónico.]**
1. En el cuadro **[!UICONTROL Umbral número de recursos/referencias]** , especifique el número de umbral de recursos/carpetas o referencias para el procesamiento asincrónico de operaciones de movimiento.

   ![Umbral de movimiento de recursos](assets/async-move-threshold.png)

1. Marque la opción **Habilitar notificación** por correo electrónico para recibir notificaciones por correo electrónico para este estado del trabajo. Por ejemplo: éxito, error.
1. Guarde los cambios.

### Configurar operaciones de movimiento de página asincrónicas {#configuring-asynchronous-page-move-operations}

Si el número de referencias a las páginas que se van a mover supera el número de umbral, la operación de movimiento se realiza de forma asíncrona.

1. En Navegación global, haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > Consola **** web.
1. Desde la consola web, abra la Configuración de procesamiento de trabajo de operación de movimiento de página **[!UICONTROL asincrónica.]**
1. En el campo **[!UICONTROL Umbral de número de referencias]** , especifique el número de umbral de referencias para el procesamiento asincrónico de las operaciones de movimiento de página.

   ![Umbral de movimiento de página](assets/async-page-move.png)

1. Marque la opción **Habilitar notificación** por correo electrónico para recibir notificaciones por correo electrónico para este estado del trabajo. Por ejemplo: éxito, error.
1. Guarde los cambios.

### Configurar operaciones de MSM asincrónicas {#configuring-asynchronous-msm-operations}

1. En Navegación global, haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > Consola **** web.
1. Desde la consola web, abra la Configuración de procesamiento de trabajo de operación de movimiento de página **[!UICONTROL asincrónica.]**
1. Marque la opción **Habilitar notificación** por correo electrónico para recibir notificaciones por correo electrónico para este estado del trabajo. Por ejemplo: éxito, error.

   ![Configuración de MSM](assets/async-msm.png)

1. Guarde los cambios.
