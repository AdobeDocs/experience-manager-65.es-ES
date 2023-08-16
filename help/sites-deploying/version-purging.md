---
title: Depuración de versiones
seo-title: Version Purging
description: Este artículo describe las opciones disponibles para la depuración de versiones.
seo-description: This article describes the available options for version purging.
uuid: a9fa25c7-e60e-4665-a726-99af9aac8f70
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: fb4d7337-7b94-430b-80d2-f1754f823c2b
docset: aem65
feature: Configuring
exl-id: 6f0b1951-bdda-475f-b6c0-bc18de082b7c
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 1%

---

# Depuración de versiones{#version-purging}

AEM En una instalación estándar, crea una nueva versión de una página o nodo cuando activa una página después de actualizar el contenido.

>[!NOTE]
>
>Si no se realizan cambios en el contenido, verá el mensaje que indica que la página se ha activado, pero no se creará ninguna nueva versión

Puede crear versiones adicionales si lo desea utilizando **Versiones** pestaña de la barra de tareas. Estas versiones se almacenan en el repositorio y se pueden restaurar si es necesario.

Estas versiones nunca se depuran, por lo que el tamaño del repositorio aumentará con el tiempo y, por lo tanto, debe administrarse.

AEM Se envía con varios mecanismos para ayudarle a administrar el repositorio:

* el [Administrador de versiones](#version-manager)
Esto se puede configurar para purgar versiones antiguas cuando se crean nuevas versiones.

* el [Purgar versiones](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) herramienta Se utiliza como parte de la supervisión y el mantenimiento del repositorio.
Permite intervenir para eliminar versiones antiguas de un nodo o una jerarquía de nodos, según estos parámetros:

   * Número máximo de versiones que se guardarán en el repositorio.
Cuando se supera este número, se elimina la versión más antigua.

   * La antigüedad máxima de cualquier versión guardada en el repositorio.
Cuando la antigüedad de una versión supera este valor, se depura del repositorio.

* el [Tarea de mantenimiento de depuración de versiones](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks). Puede planificar la tarea de mantenimiento Depuración de versiones para que se eliminen automáticamente las versiones antiguas. Como resultado, esto minimiza la necesidad de utilizar manualmente las herramientas de depuración de versiones.

>[!CAUTION]
>
>Para optimizar el tamaño del repositorio, debe ejecutar la tarea de depuración de versiones con frecuencia. La tarea debe programarse fuera del horario laboral cuando haya una cantidad limitada de tráfico.

## Administrador de versiones {#version-manager}

Además de la depuración explícita mediante la herramienta de depuración, se puede configurar el Administrador de versiones para que depure las versiones antiguas cuando se crean nuevas.

Para configurar el Administrador de versiones, [crear una configuración](/help/sites-deploying/configuring-osgi.md) para:

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

Las opciones disponibles son las siguientes:

* `versionmanager.createVersionOnActivation` (Booleano, predeterminado: true) Especifica si se crea una versión cuando se activan las páginas.
Se crea una versión a menos que el agente de replicación esté configurado para suprimir la creación de versiones, algo que respeta el Administrador de versiones.
Se crea una versión solo si la activación se produce en una ruta contenida en `versionmanager.ivPaths` (ver más abajo).

* `versionmanager.ivPaths`(Cadena)[], predeterminado: `{"/"}`) Especifica las rutas en las que se crean versiones implícitamente al activarlas `versionmanager.createVersionOnActivation` se establece en true.

* `versionmanager.purgingEnabled` (Booleano, predeterminado: false) Define si se habilita o no la depuración cuando se crean nuevas versiones.

* `versionmanager.purgePaths` (Cadena)[], predeterminado: {&quot;/content&quot;}) Especifica en qué rutas se depuran las versiones cuando se crean nuevas versiones.

* `versionmanager.maxAgeDays` (int, predeterminado: 30) Al purgar la versión, se eliminará cualquier versión anterior al valor configurado. Si el valor es menor que 1, la depuración no se realizará según la antigüedad de la versión.

* `versionmanager.maxNumberVersions` (int, predeterminado 5) Al purgar la versión, se eliminará cualquier versión anterior a la n-ésima más reciente. Si el valor es menor que 1, la depuración no se realiza en función del número de versiones.

* `versionmanager.minNumberVersions` (int, predeterminado 0) El número mínimo de versiones que se conservarán independientemente de la edad. Si el valor se establece en un valor menor que 1, no se conserva un número mínimo de versiones.

>[!NOTE]
>
>No se recomienda mantener un gran número de versiones en el repositorio. Por lo tanto, al configurar la operación de depuración de versiones, tenga en cuenta no excluir demasiadas versiones de la depuración; de lo contrario, el tamaño del repositorio no se optimizará correctamente. Si mantiene un gran número de versiones debido a requisitos comerciales, póngase en contacto con el servicio de asistencia de Adobe para buscar formas alternativas de optimizar el tamaño del repositorio.

### Combinar opciones de retención {#combining-retention-options}

Las opciones que definen cómo se deben conservar las versiones ( `maxAgeDays`, `maxNumberVersions`, `minNumberVersions`), se puede combinar según sus necesidades.

Por ejemplo, al definir el número máximo de versiones que se van a conservar Y la versión más antigua que se va a conservar:

* Configuración:

   * `maxNumberVersions` = 7

   * `maxAgeDays` = 30

* Con:

   * 10 versiones realizadas en los últimos 60 días
   * 3 de esas versiones creadas en los últimos 30 días

* Significará lo siguiente:

   * Se conservarán las últimas 3 versiones

Por ejemplo, al definir el número máximo Y mínimo de versiones que se van a conservar Y la versión más antigua que se va a conservar:

* Configuración:

   * `maxNumberVersions` = 3
   * `maxAgeDays` = 30
   * `minNumberVersions` = 3

* Con:

   * 5 versiones realizadas hace 60 días

* Significará lo siguiente:

   * Se conservarán 3 versiones

## Herramienta Purgar versiones {#purge-versions-tool}

El [Purgar versiones](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) está diseñada para depurar las versiones de un nodo o una jerarquía de nodos en el repositorio. Su propósito principal es ayudarle a reducir el tamaño del repositorio eliminando las versiones antiguas de los nodos.
