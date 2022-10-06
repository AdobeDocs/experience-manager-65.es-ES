---
title: Purgar registros de la base de datos de Job Manager
seo-title: Purge records from the Job Manager database
description: Los datos de procesos grandes pueden disminuir el rendimiento de los formularios AEM. Se recomienda depurar los datos del proceso cuando los registros ya no sean necesarios.
seo-description: Large process data can result in lower AEM forms performance. It is good practice to purge process data when records are no longer necessary.
uuid: cf214498-36e9-4dcc-b4d4-e7c46f80dbab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 69a406f2-4fa8-40bb-b671-7b0f5b6a2c4c
exl-id: 5279f6c3-5954-472c-9ea0-18e8a7ec860e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# Purgar registros de la base de datos de Job Manager {#purge-records-from-the-job-manager-database}

Los datos de proceso que se generan cuando se invoca un proceso de larga duración pueden llegar a ser demasiado grandes, lo que reduce el rendimiento de AEM formularios y el uso de espacio en disco innecesario. Se recomienda depurar los datos del proceso cuando los registros ya no sean necesarios.

Puede utilizar la consola de administración para realizar una depuración única de registros obsoletos o programar purgas automáticas regulares. Otros métodos para purgar registros obsoletos se tratan en [Depuración de datos de procesos](/help/forms/using/admin-help/purging-process-data.md#purging-process-data).

**Acceso a la página Programador de Depuración de Trabajos**

1. En la Consola de administración, haga clic en Monitor de estado en la esquina superior derecha de la página.
1. Haga clic en la ficha Programador de purga de trabajos .

La información sobre las purgas programadas actualmente se muestra en el cuadro Información del planificador de purga de trabajos.

>[!NOTE]
>
>Al hacer clic en Detener planificador, se detiene cualquier depuración programada en el futuro, pero no se detiene un trabajo de depuración que ya esté en curso.

**Programar una depuración única**

1. Seleccione Solo una vez.
1. En el área Purgar el filtro de registros completados , especifique el número de días o semanas después de los cuales un registro se considera obsoleto y listo para la depuración.

   >[!NOTE]
   >
   >Los registros relacionados con procesos que no se han completado no se depuran, aunque tengan una antigüedad mayor que la especificada.

1. Especifique cuándo se producirá la depuración. Active la casilla Usar fecha y hora actuales o desactive la casilla de verificación y haga clic en los iconos de calendario y reloj para especificar la fecha y la hora en que se realizará la depuración.

   >[!NOTE]
   >
   >Si especifica una fecha y hora de inicio anteriores, la depuración se producirá inmediatamente al hacer clic en Iniciar planificador.

1. Haga clic en Iniciar planificador. Cualquier configuración del planificador previamente programada se sustituye por la nueva configuración.

**Configurar una programación de depuración automática**

1. Seleccione Volver a cada y especifique el número de días o semanas entre purgas.
1. En el área Purgar el filtro de registros completados , especifique el número de días o semanas después de los cuales un registro se considera obsoleto y listo para la depuración. No se puede establecer el valor en `0`.

   >[!NOTE]
   >
   >Los registros relacionados con procesos que no se han completado no se depuran, aunque tengan una antigüedad mayor que la especificada.

1. Especifique cuándo comenzarán las purgas. Active la casilla Usar fecha y hora actuales o desactive la casilla de verificación y haga clic en los iconos de calendario y reloj para especificar la fecha y la hora en que se realizará la depuración.

   >[!NOTE]
   >
   >Si especifica una fecha y hora de inicio anteriores, AEM formularios calculará la fecha lógica de inicio siguiente en función de la fecha especificada. Por ejemplo, si programa las purgas de trabajos para que se produzcan semanalmente a partir del 7 de abril y ahora es el 9 de abril, la primera purga se producirá el 14 de abril.

1. Haga clic en Iniciar planificador. Cualquier configuración del planificador previamente programada se sustituye por la nueva configuración.
