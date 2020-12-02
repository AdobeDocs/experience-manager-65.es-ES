---
title: Purgar registros de la base de datos de Job Manager
seo-title: Purgar registros de la base de datos de Job Manager
description: Los datos de procesos grandes pueden resultar en un menor rendimiento AEM los formularios. Se recomienda depurar los datos del proceso cuando ya no se necesitan registros.
seo-description: Los datos de procesos grandes pueden resultar en un menor rendimiento AEM los formularios. Se recomienda depurar los datos del proceso cuando ya no se necesitan registros.
uuid: cf214498-36e9-4dcc-b4d4-e7c46f80dbab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 69a406f2-4fa8-40bb-b671-7b0f5b6a2c4c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---


# Purgar registros de la base de datos de Job Manager {#purge-records-from-the-job-manager-database}

Los datos de proceso que se generan cuando se invoca un proceso de larga duración pueden llegar a ser demasiado grandes, lo que reduce el rendimiento de los formularios AEM y reduce el uso de espacio en disco innecesario. Se recomienda depurar los datos del proceso cuando ya no se necesitan registros.

Puede utilizar la consola de administración para realizar una purga única de registros obsoletos o para programar purgas automáticas regulares. Otros métodos para purgar registros obsoletos se analizan en [Depuración de datos de procesos](/help/forms/using/admin-help/purging-process-data.md#purging-process-data).

**Acceso a la página Planificador de Depuración de Trabajos**

1. En la Consola de administración, haga clic en Monitor de estado en la esquina superior derecha de la página.
1. Haga clic en la ficha Planificador Depuración de trabajos.

La información sobre las purgas programadas actualmente se muestra en el cuadro Información del Planificador de depuración de trabajos.

>[!NOTE]
>
>Al hacer clic en Detener Planificador se detienen las purgas programadas en el futuro, pero no se detiene un trabajo de purga que ya está en curso.

**Programar una purga única**

1. Seleccione Solo una vez.
1. En el área Purgar el filtro de registros completados, especifique el número de días o semanas después de los cuales un registro se considera obsoleto y listo para la purga.

   >[!NOTE]
   >
   >Los registros relacionados con los procesos que no se han completado no se purgan, aunque tengan una antigüedad mayor que la especificada.

1. Especifique cuándo se producirá la purga. Seleccione la casilla de verificación Usar fecha y hora actuales o desactive la casilla y haga clic en los iconos de calendario y reloj para especificar la fecha y la hora en que se realizará la purga.

   >[!NOTE]
   >
   >Si especifica una fecha y hora de inicio que ya existían, la purga se produce inmediatamente al hacer clic en Planificador de Inicio.

1. Haga clic en Planificador de Inicio. Cualquier configuración de Planificador previamente programada se sustituye por la nueva configuración.

**Configurar una programación de depuración automática**

1. Seleccione Repetir cada y especifique el número de días o semanas entre las purgas.
1. En el área Purgar el filtro de registros completados, especifique el número de días o semanas después de los cuales un registro se considera obsoleto y listo para la purga. No puede establecer el valor en `0`.

   >[!NOTE]
   >
   >Los registros relacionados con los procesos que no se han completado no se purgan, aunque tengan una antigüedad mayor que la especificada.

1. Especifique cuándo comenzarán las purgas. Seleccione la casilla de verificación Usar fecha y hora actuales o desactive la casilla y haga clic en los iconos de calendario y reloj para especificar la fecha y la hora en que se realizará la purga.

   >[!NOTE]
   >
   >Si especifica una fecha y hora de inicio que ya existían, AEM formularios calculará la fecha lógica siguiente de inicio en función de la fecha especificada. Por ejemplo, si programa que las purgas de trabajos se produzcan semanalmente a partir del 7 de abril y ahora es el 9 de abril, la primera purga tendrá lugar el 14 de abril.

1. Haga clic en Planificador de Inicio. Cualquier configuración de Planificador previamente programada se sustituye por la nueva configuración.

