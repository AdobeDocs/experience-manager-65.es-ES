---
title: Mantenimiento del registro de auditoría en AEM 6
seo-title: Mantenimiento del registro de auditoría en AEM 6
description: Obtenga información sobre el mantenimiento del registro de auditoría en AEM.
seo-description: Obtenga información sobre el mantenimiento del registro de auditoría en AEM.
uuid: 212de4df-6bf4-434c-94e1-74186d21945a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 565d89de-b3ca-41a5-8e1c-d10905c25fb5
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---


# Mantenimiento del registro de auditoría en AEM 6{#audit-log-maintenance-in-aem}

Los eventos de AEM que cumplen los requisitos para el registro de auditoría generan muchos datos archivados. Estos datos pueden crecer rápidamente con el tiempo debido a las replicaciones, cargas de recursos y otras actividades del sistema.

El mantenimiento del registro de auditoría incluye varias partes de la funcionalidad que permiten automatizar el mantenimiento del registro de auditoría según políticas específicas.

Se implementa como una tarea de mantenimiento semanal configurable y se puede acceder a ella a través de la consola de supervisión de Operations Panel.

Para obtener más información, consulte [Operations Panel Documentation](/help/sites-administering/operations-dashboard.md).

Existen tres tipos de opciones de Depuración del registro de auditoría:

1. [Depuración del registro de auditoría de página](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [Depuración del registro de auditoría DAM](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [Depuración del registro de auditoría de replicación](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

Cada una de ellas se puede configurar creando reglas en la consola web de AEM. Después de configurarlas, puede realizar el déclencheur de las mismas si ingresa a **Herramientas - Operaciones - Mantenimiento - Ventana de mantenimiento semanal** y ejecuta la Tarea de mantenimiento **AuditLog**.

## Configurar la depuración del registro de auditoría de página {#configure-page-audit-log-purging}

Siga estos pasos para configurar la depuración del registro de auditoría:

1. Vaya al Administrador de la consola web señalando su explorador a `http://localhost:4502/system/console/configMgr/`

1. Busque un elemento llamado **Reglas de depuración de registro de auditoría de páginas** y haga clic en él.

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. A continuación, configure el Planificador de purga según sus necesidades. Las opciones disponibles son:

   * **Nombre de regla:** el nombre de la regla de directiva de auditoría;
   * **Ruta de contenido:** la ruta del contenido a la que se aplicará la regla;
   * **Edad mínima:** el tiempo en días que deben mantenerse los registros de auditoría;
   * **Tipo de registro de auditoría:** el tipo de registro de auditoría que se debe purgar.

   >[!NOTE]
   >
   >La ruta de contenido solo se aplica a los elementos secundarios del nodo `/var/audit/com.day.cq.wcm.core.page` del repositorio.

1. Guarde la regla.
1. La regla que acaba de crear debe estar expuesta en el Panel de operaciones para que se pueda ejecutar. Para ello, vaya a **Herramientas - Operaciones - Mantenimiento** desde la pantalla de bienvenida de AEM.

1. Presione la tarjeta **Ventana de mantenimiento semanal**.

1. Encontrará la tarea de mantenimiento ya presente en la tarjeta **Tarea de mantenimiento de AuditLog**.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. Puede inspeccionar la fecha de la siguiente ejecución, configurarla o ejecutarla manualmente pulsando el botón de reproducción.

En AEM 6.3, si la ventana de mantenimiento programado se cierra antes de que se pueda completar la tarea de Depuración del registro de auditoría, la tarea se detiene automáticamente. Se reanudará cuando se abra la siguiente ventana de mantenimiento.

**Con AEM 6.5**, puede detener manualmente una Tarea de Depuración del registro de auditoría haciendo clic en el  **** icono Detener. En la próxima ejecución, la tarea se reanudará de forma segura.

>[!NOTE]
>
>Detener la tarea de mantenimiento significa suspender su ejecución sin perder la pista del trabajo que ya está en curso.

## Configurar la depuración del registro de auditoría DAM {#configure-dam-audit-log-purging}

1. Vaya a la Consola de sistema en *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Busque la regla **Depuración del registro de auditoría de DAM** y haga clic en el resultado.
1. En la siguiente ventana, configure la regla según corresponda. Las opciones son:

   * **Nombre de regla:** el nombre de la regla de directiva de auditoría;
   * **Ruta de contenido:** la ruta del contenido a la que se aplicará la regla
   * **Edad mínima:** el tiempo en días que deben mantenerse los registros de auditoría
   * **Tipos de evento de DAM de registro de auditoría:** los tipos de eventos de auditoría DAM que deben eliminarse.

1. Haga clic en **Guardar** para guardar la configuración

## Configurar la depuración del registro de auditoría de replicación {#configure-replication-audit-log-purging}

1. Vaya a la Consola de sistema en *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Busque **Planificador de depuración de registro de auditoría de replicación** y haga clic en el resultado
1. En la siguiente ventana, configure la regla según corresponda. Las opciones son:

   * **Nombre de regla:** el nombre de la regla de directiva de auditoría
   * **Ruta de contenido:** la ruta del contenido a la que se aplicará la regla
   * **Edad mínima:** el tiempo en días que deben mantenerse los registros de auditoría
   * **Tipos de evento de replicación del registro de auditoría:** los tipos de eventos de auditoría de replicación que deben eliminarse

1. Haga clic en **Guardar** para guardar la configuración.

