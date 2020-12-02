---
title: Visión general del monitor de estado
seo-title: Visión general del monitor de estado
description: Este documento proporciona información general sobre el monitor de mantenimiento y detalles sobre cómo puede acceder a él.
seo-description: Este documento proporciona información general sobre el monitor de mantenimiento y detalles sobre cómo puede acceder a él.
uuid: 5934fd2d-80a5-4c6d-b3ee-882c2865705b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c303e967-944d-40b0-96ca-f91e2f42a0d0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---


# Visión general del monitor de estado {#overview-of-health-monitor}

El monitor de estado proporciona información crítica sobre el sistema de formularios AEM, como información del servidor, uso de memoria y uso del procesador. También están disponibles las estadísticas del Administrador de trabajo, como el número de elementos de trabajo o trabajos en la cola y sus estados. Puede realizar las siguientes tareas mediante el Monitor de estado:

* Verifique que el sistema se esté ejecutando correctamente
* Información de vista para ayudar a diagnosticar problemas del sistema a medida que se producen
* Realizar operaciones en elementos de trabajo o trabajos que muestren problemas
* Purgar registros obsoletos de la base de datos de Job Manager

La página Monitor de estado de la consola de administración tiene tres fichas:

* La ficha Sistema muestra gráficos de supervisión de recursos e información sobre el servidor de formularios (o nodo en un entorno agrupado). (Consulte [información del sistema de Vista](/help/forms/using/admin-help/view-system-information.md#view-system-information).)
* La ficha Administrador de trabajo muestra los datos relacionados con el Administrador de trabajo, como el número de elementos de trabajo en la cola del Administrador de trabajo. Puede filtrar la información mediante varios criterios o administrar elementos de trabajo individuales mediante las herramientas de operación. (Consulte [Estadísticas de Vista relacionadas con el Administrador de trabajo](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)
* La ficha Planificador Depuración de Trabajos permite purgar registros obsoletos de la base de datos de Job Manager. (Consulte [Purgar registros de la base de datos de Job Manager](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)

La página web del Monitor de estado se llena con estadísticas recopiladas a través de la API de Gemfire. Esta API detecta automáticamente todos los nodos de un clúster. También resuelve los problemas de seguridad que se producen al recopilar estadísticas desde servidores proxy o equilibradores de carga. Las opciones de Java están disponibles para ajustar el monitor de estado, lo que reduce el impacto en el rendimiento del entorno de formularios AEM. (Consulte [Ajuste del rendimiento del monitor de estado](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance)).

**Control de estado de acceso**

1. En la consola de administración, haga clic en Monitor de estado en la esquina superior derecha de la página.

