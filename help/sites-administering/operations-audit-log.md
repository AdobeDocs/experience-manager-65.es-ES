---
title: AEM Mantenimiento del registro de auditoría en el 6
seo-title: Audit Log Maintenance in AEM 6
description: AEM Obtenga información sobre el mantenimiento del registro de auditoría en la.
seo-description: Lear about Audit Log Maintenance in AEM.
uuid: 212de4df-6bf4-434c-94e1-74186d21945a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 565d89de-b3ca-41a5-8e1c-d10905c25fb5
exl-id: 1e05faf5-619a-4ea3-acbf-2fd37c71e6d2
feature: Operations
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# AEM Mantenimiento del registro de auditoría en el 6{#audit-log-maintenance-in-aem}

AEM Los eventos de que cumplen los requisitos para el registro de auditoría generan muchos datos archivados. Estos datos pueden crecer rápidamente con el tiempo debido a las replicaciones, las cargas de recursos y otras actividades del sistema.

El mantenimiento del registro de auditoría incluye varias partes de funcionalidad que permiten automatizar el mantenimiento del registro de auditoría en directivas específicas.

Se implementa como una tarea de mantenimiento semanal configurable y se puede acceder a ella a través de la consola de monitorización del tablero de operaciones.

Para obtener más información, consulte la [Documentación del Operations Dashboard](/help/sites-administering/operations-dashboard.md).

Existen tres tipos de opciones de depuración de registros de auditoría:

1. [Purga del registro de auditoría de página](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [Depuración del registro de auditoría DAM](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [Purga del registro de auditoría de replicación](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

AEM Cada una de ellas se puede configurar creando reglas en la consola web de. Una vez configuradas, puede almacenarlas en déclencheur en el menú **Herramientas - Operaciones - Mantenimiento - Ventana de mantenimiento semanal** y ejecutar el **Tarea de mantenimiento de AuditLog**.

## Configurar depuración del registro de auditoría de página {#configure-page-audit-log-purging}

Siga estos pasos para configurar la depuración del registro de auditoría:

1. Vaya al administrador de la consola web seleccionando el explorador `http://localhost:4502/system/console/configMgr/`

1. Busque un elemento llamado **Regla de purga de registros de auditoría de páginas** y haga clic en él.

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. A continuación, configure el planificador de depuración según sus necesidades. Las opciones disponibles son:

   * **Nombre de la regla:** el nombre de la regla de política de auditoría;
   * **Ruta de contenido:** la ruta del contenido al que se aplicará la regla;
   * **Edad mínima:** el tiempo en días que deben conservarse los registros de auditoría;
   * **Tipo de registro de auditoría:** el tipo de registro de auditoría que se debe purgar.

   >[!NOTE]
   >
   >La ruta de contenido solo se aplica a los elementos secundarios del `/var/audit/com.day.cq.wcm.core.page` en el repositorio.

1. Guarde la regla.
1. La regla que acaba de crear debe exponerse en el tablero de operaciones para que se ejecute. Para hacer esto, vaya a **Herramientas - Operaciones - Mantenimiento** AEM en la pantalla de bienvenida de la.

1. Pulse el botón **Ventana de mantenimiento semanal** Tarjeta de.

1. La tarea de mantenimiento ya está presente en la **Tarea de mantenimiento de AuditLog** Tarjeta de.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. Puede inspeccionar la fecha de la siguiente ejecución, configurarla o ejecutarla manualmente pulsando el botón de reproducción.

AEM En la versión 6.3, si la ventana de mantenimiento programado se cierra antes de que se complete la tarea Purga del registro de auditoría, la tarea se detendrá automáticamente. Se reanudará cuando se abra la siguiente ventana de mantenimiento.

**AEM Con 6,5**, puede detener manualmente una tarea de purga de registros de auditoría en ejecución haciendo clic en **Detener** icono. En la siguiente ejecución, la tarea se reanudará de forma segura.

>[!NOTE]
>
>Detener la tarea de mantenimiento significa suspender su ejecución sin perder el seguimiento del trabajo ya en curso.

## Configurar depuración del registro de auditoría DAM {#configure-dam-audit-log-purging}

1. Vaya a la consola del sistema en *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Buscar por **Purga del registro de auditoría DAM** y haga clic en el resultado.
1. En la siguiente ventana, configure la regla en consecuencia. Las opciones son:

   * **Nombre de la regla:** el nombre de la regla de política de auditoría;
   * **Ruta de contenido:** la ruta del contenido al que se aplicará la regla
   * **Edad mínima:** el tiempo en días que deben conservarse los registros de auditoría
   * **Tipos de eventos Dam de registro de auditoría:** los tipos de eventos de auditoría DAM que deben purgarse.

1. Clic **Guardar** para guardar la configuración

## Configurar depuración del registro de auditoría de replicación  {#configure-replication-audit-log-purging}

1. Vaya a la consola del sistema en *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Buscar por **Programador de purga del registro de auditoría de replicación** y haga clic en el resultado
1. En la siguiente ventana, configure la regla en consecuencia. Las opciones son:

   * **Nombre de la regla:** nombre de la regla de directiva de auditoría
   * **Ruta de contenido:** la ruta del contenido al que se aplicará la regla
   * **Edad mínima:** el tiempo en días que deben conservarse los registros de auditoría
   * **Tipos de eventos de replicación de registros de auditoría:** los tipos de eventos de auditoría de replicación que deben purgarse

1. Clic **Guardar** para guardar la configuración.
