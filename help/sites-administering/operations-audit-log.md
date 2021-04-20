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
exl-id: 1e05faf5-619a-4ea3-acbf-2fd37c71e6d2
feature: Operations
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---

# Mantenimiento del registro de auditoría en AEM 6{#audit-log-maintenance-in-aem}

AEM eventos que cumplen los requisitos para el registro de auditoría generan muchos datos archivados. Estos datos pueden crecer rápidamente con el tiempo debido a las réplicas, cargas de recursos y otras actividades del sistema.

El mantenimiento del registro de auditoría incluye varias partes de la funcionalidad que permiten automatizar el mantenimiento del registro de auditoría en políticas específicas.

Se implementa como una tarea de mantenimiento semanal configurable y es accesible a través de la consola de supervisión del panel de operaciones.

Para obtener más información, consulte [Operations Dashboard Documentation](/help/sites-administering/operations-dashboard.md).

Existen tres tipos de opciones de Purga de registro de auditoría:

1. [Purga del registro de auditoría de página](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [Depuración de registros de auditoría de DAM](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [Purga del registro de auditoría de replicación](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

Cada uno se puede configurar creando reglas en la consola web AEM. Una vez configuradas, puede realizar el déclencheur en ellas yendo a **Tools - Operations - Maintenance - Weekly Maintenance Window** y ejecutando la **AuditLog Maintenance Task**.

## Configurar la depuración del registro de auditoría de página {#configure-page-audit-log-purging}

Siga estos pasos para configurar la depuración del registro de auditoría:

1. Vaya al administrador de la consola web señalando el navegador a `http://localhost:4502/system/console/configMgr/`

1. Busque un elemento llamado **Pages audit Log Purge rule** y haga clic en él.

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. A continuación, configure el planificador de depuración según sus necesidades. Las opciones disponibles son:

   * **Nombre de la regla:** el nombre de la regla de directiva de auditoría;
   * **Ruta de contenido:** la ruta de contenido a la que se aplicará la regla;
   * **Edad mínima:** tiempo en días que deben mantenerse los registros de auditoría;
   * **Tipo de registro de auditoría:** el tipo de registro de auditoría que debe depurarse.

   >[!NOTE]
   >
   >La ruta de contenido solo se aplica a los elementos secundarios del nodo `/var/audit/com.day.cq.wcm.core.page` en el repositorio.

1. Guarde la regla.
1. La regla que acaba de crear debe estar expuesta en el panel de operaciones para que se ejecute. Para ello, vaya a **Tools - Operations - Maintenance** desde la pantalla de bienvenida de AEM.

1. Presione la tarjeta **Weekly Maintenance Window**.

1. Encontrará la tarea de mantenimiento ya presente en la tarjeta **AuditLog Maintenance Task**.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. Puede inspeccionar la fecha de la siguiente ejecución, configurarla o ejecutarla manualmente pulsando el botón de reproducción.

En AEM 6.3, si la ventana de mantenimiento programado se cierra antes de que se pueda completar la tarea Purga de registro de auditoría, la tarea se detiene automáticamente. Se reanudará cuando se abra la siguiente ventana de mantenimiento.

**Con AEM 6.5**, puede detener manualmente una tarea de purga de registro de auditoría haciendo clic en el  **** icono Detener. En la siguiente ejecución, la tarea se reanudará de forma segura.

>[!NOTE]
>
>Detener la tarea de mantenimiento significa suspender su ejecución sin perder el seguimiento del trabajo que ya está en curso.

## Configurar la depuración del registro de auditoría de DAM {#configure-dam-audit-log-purging}

1. Vaya a la consola del sistema en *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Busque la regla **DAM audit Log Purge** y haga clic en el resultado.
1. En la siguiente ventana, configure la regla en consecuencia. Las opciones son:

   * **Nombre de la regla:** el nombre de la regla de directiva de auditoría;
   * **Ruta de contenido:** la ruta del contenido al que se aplicará la regla
   * **Edad mínima:** tiempo en días que se deben conservar los registros de auditoría
   * **Tipos de eventos de DAM de registro de auditoría:** los tipos de eventos de auditoría de DAM que deben purgarse.

1. Haga clic en **Guardar** para guardar la configuración

## Configurar la depuración del registro de auditoría de replicación {#configure-replication-audit-log-purging}

1. Vaya a la consola del sistema en *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Busque **Replication audit Log Purge Scheduler** y haga clic en el resultado
1. En la siguiente ventana, configure la regla en consecuencia. Las opciones son:

   * **Nombre de regla:** el nombre de la regla de directiva de auditoría
   * **Ruta de contenido:** la ruta del contenido al que se aplicará la regla
   * **Edad mínima:** tiempo en días que se deben conservar los registros de auditoría
   * **Tipos de eventos de replicación del registro de auditoría:** los tipos de eventos de auditoría de replicación que deben purgarse.

1. Haga clic en **Guardar** para guardar la configuración.
