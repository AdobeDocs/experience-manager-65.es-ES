---
title: Purgar registros de la base de datos de Job Manager
description: AEM Los datos de proceso grandes pueden reducir el rendimiento de los formularios en la. Se recomienda depurar los datos de proceso cuando ya no son necesarios los registros.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 5279f6c3-5954-472c-9ea0-18e8a7ec860e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 2%

---

# Purgar registros de la base de datos de Job Manager {#purge-records-from-the-job-manager-database}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

AEM Los datos de proceso que se generan cuando se invoca un proceso de larga duración pueden llegar a ser demasiado grandes, lo que da como resultado un rendimiento de formularios más bajo y el uso de espacio en disco innecesario. Se recomienda depurar los datos de proceso cuando ya no son necesarios los registros.

Puede utilizar la consola de administración para realizar una depuración única de registros obsoletos o para programar depuraciones automáticas regulares. En [Depuración de datos de proceso](/help/forms/using/admin-help/purging-process-data.md#purging-process-data) se describen otros métodos para purgar registros obsoletos.

**Acceder a la página Planificador de purga de trabajos**

1. En la consola de administración, haga clic en Monitor de estado en la esquina superior derecha de la página.
1. Haga clic en la pestaña Programador de Depuración de Trabajos.

La información sobre cualquier depuración programada actualmente se muestra en la casilla Información del Planificador de Depuración de Tareas.

>[!NOTE]
>
>Al hacer clic en Detener planificador, se detienen las depuraciones programadas en el futuro, pero no se detiene un trabajo de depuración que ya está en curso.

**Programar una depuración única**

1. Seleccione Solo Una Vez.
1. En el área Filtro Purgar registros completados, especifique el número de días o semanas después de los cuales un registro se considera obsoleto y está listo para la depuración.

   >[!NOTE]
   >
   >Los registros relacionados con los procesos que no se han completado no se depuran, aunque sean anteriores a la edad especificada.

1. Especifique cuándo se producirá la depuración. Seleccione la casilla de verificación Usar fecha y hora actuales o desmarque la casilla de verificación y haga clic en los iconos de calendario y reloj para especificar la fecha y la hora en que se realizará la depuración.

   >[!NOTE]
   >
   >Si especifica una fecha y una hora de inicio anteriores, la depuración se producirá inmediatamente al hacer clic en Iniciar programador.

1. Haga clic en Iniciar planificador. Cualquier configuración del programador programada anteriormente se reemplaza por la nueva configuración.

**Configurar una programación de depuración automática**

1. Seleccione Recurrir cada y especifique el número de días o semanas entre depuraciones.
1. En el área Filtro Purgar registros completados, especifique el número de días o semanas después de los cuales un registro se considera obsoleto y está listo para la depuración. No puede establecer el valor en `0`.

   >[!NOTE]
   >
   >Los registros relacionados con los procesos que no se han completado no se depuran, aunque sean anteriores a la edad especificada.

1. Especifique cuándo comenzarán las depuraciones. Seleccione la casilla de verificación Usar fecha y hora actuales o desmarque la casilla de verificación y haga clic en los iconos de calendario y reloj para especificar la fecha y la hora en que se realizará la depuración.

   >[!NOTE]
   >
   >AEM Si especifica una fecha y una hora de inicio que sean anteriores, los formularios de datos de la aplicación calcularán la fecha de inicio siguiente lógica en función de la fecha especificada. Por ejemplo, si programa las depuraciones del trabajo para que se produzcan semanalmente a partir del 7 de abril y ahora es el 9 de abril, la primera depuración se producirá el 14 de abril.

1. Haga clic en Iniciar planificador. Cualquier configuración del programador programada anteriormente se reemplaza por la nueva configuración.
