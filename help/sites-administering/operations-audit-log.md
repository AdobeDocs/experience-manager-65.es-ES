---
title: Mantenimiento del registro de auditoría en AEM 6
seo-title: Audit Log Maintenance in AEM 6
description: Obtenga información sobre el mantenimiento del registro de auditoría en AEM.
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

# Mantenimiento del registro de auditoría en AEM 6{#audit-log-maintenance-in-aem}

AEM eventos que cumplen los requisitos para el registro de auditoría generan muchos datos archivados. Estos datos pueden crecer rápidamente con el tiempo debido a las réplicas, cargas de recursos y otras actividades del sistema.

El mantenimiento del registro de auditoría incluye varias partes de la funcionalidad que permiten automatizar el mantenimiento del registro de auditoría en políticas específicas.

Se implementa como una tarea de mantenimiento semanal configurable y es accesible a través de la consola de supervisión del panel de operaciones.

Para obtener más información, consulte [Documentación del panel de operaciones](/help/sites-administering/operations-dashboard.md).

Existen tres tipos de opciones de Purga de registro de auditoría:

1. [Purga del registro de auditoría de página](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [Depuración de registros de auditoría de DAM](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [Purga del registro de auditoría de replicación](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

Cada uno se puede configurar creando reglas en la consola web AEM. Una vez configuradas, puede realizar el déclencheur en , yendo a **Herramientas - Operaciones - Mantenimiento - Ventana de mantenimiento semanal** y ejecutando **Tarea de mantenimiento de AuditLog**.

## Configurar la depuración del registro de auditoría de páginas {#configure-page-audit-log-purging}

Siga estos pasos para configurar la depuración del registro de auditoría:

1. Vaya al administrador de la consola web señalando el navegador a `http://localhost:4502/system/console/configMgr/`

1. Buscar un elemento llamado **Regla de purga de registro de auditoría de páginas** y haga clic en ella.

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. A continuación, configure el planificador de depuración según sus necesidades. Las opciones disponibles son:

   * **Nombre de la regla:** el nombre de la regla de política de auditoría;
   * **Ruta de contenido:** la ruta del contenido a la que se aplicará la regla;
   * **Edad mínima:** la hora en días en que deben mantenerse los registros de auditoría;
   * **Tipo de registro de auditoría:** el tipo de registro de auditoría que debe depurarse.

   >[!NOTE]
   >
   >La ruta de contenido solo se aplica a los elementos secundarios de la variable `/var/audit/com.day.cq.wcm.core.page` en el repositorio.

1. Guarde la regla.
1. La regla que acaba de crear debe estar expuesta en el panel de operaciones para que se ejecute. Para ello, vaya **Herramientas - Operaciones - Mantenimiento** en la pantalla de bienvenida de AEM.

1. Pulse el botón **Período de mantenimiento semanal** tarjeta.

1. Encontrará la tarea de mantenimiento ya presente en la sección **Tarea de mantenimiento de AuditLog** tarjeta.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. Puede inspeccionar la fecha de la siguiente ejecución, configurarla o ejecutarla manualmente pulsando el botón de reproducción.

En AEM 6.3, si la ventana de mantenimiento programado se cierra antes de que se pueda completar la tarea Purga de registro de auditoría, la tarea se detiene automáticamente. Se reanudará cuando se abra la siguiente ventana de mantenimiento.

**Con AEM 6.5**, puede detener manualmente una tarea de purga de registro de auditoría haciendo clic en el botón **Stop** icono. En la siguiente ejecución, la tarea se reanudará de forma segura.

>[!NOTE]
>
>Detener la tarea de mantenimiento significa suspender su ejecución sin perder el seguimiento del trabajo que ya está en curso.

## Configurar la depuración del registro de auditoría de DAM {#configure-dam-audit-log-purging}

1. Vaya a la consola Sistema en *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Buscar **Purga del registro de auditoría de DAM** y haga clic en el resultado.
1. En la siguiente ventana, configure la regla en consecuencia. Las opciones son:

   * **Nombre de la regla:** el nombre de la regla de política de auditoría;
   * **Ruta de contenido:** la ruta del contenido a la que se aplicará la regla
   * **Edad mínima:** la hora en días en la que se deben mantener los registros de auditoría
   * **Tipos de eventos de DAM de registro de auditoría:** los tipos de eventos de auditoría de DAM que deben depurarse.

1. Haga clic en **Guardar** para guardar la configuración

## Configurar la depuración del registro de auditoría de replicación  {#configure-replication-audit-log-purging}

1. Vaya a la consola Sistema en *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Buscar **Programador de purga de registros de auditoría de replicación** y haga clic en el resultado
1. En la siguiente ventana, configure la regla en consecuencia. Las opciones son:

   * **Nombre de la regla:** nombre de la regla de directiva de auditoría
   * **Ruta de contenido:** la ruta del contenido a la que se aplicará la regla
   * **Edad mínima:** la hora en días en la que se deben mantener los registros de auditoría
   * **Tipos de eventos de replicación del registro de auditoría:** los tipos de eventos de auditoría de replicación que deben purgarse

1. Haga clic en **Guardar** para guardar la configuración.
