---
title: Depuración de versiones
seo-title: Depuración de versiones
description: Este artículo describe las opciones disponibles para la depuración de versiones.
seo-description: Este artículo describe las opciones disponibles para la depuración de versiones.
uuid: a9fa25c7-e60e-4665-a726-99af9aac8f70
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: fb4d7337-7b94-430b-80d2-f1754f823c2b
docset: aem65
feature: Configuración
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 2%

---


# Depuración de versiones{#version-purging}

En una instalación estándar, AEM crea una nueva versión de una página o nodo cuando activa una página después de actualizar el contenido.

>[!NOTE]
>
>Si no se realizan cambios en el contenido, verá el mensaje que indica que la página se ha activado, pero no se creará ninguna versión nueva

Puede crear versiones adicionales si lo solicita utilizando la pestaña **Versioning** de la barra de tareas. Estas versiones se almacenan en el repositorio y se pueden restaurar si es necesario.

Estas versiones nunca se depuran, por lo que el tamaño del repositorio crecerá con el tiempo y, por lo tanto, debe administrarse.

AEM incluye varios mecanismos para ayudarle a administrar su repositorio:

* el [Administrador de versiones](#version-manager)
Esto se puede configurar para depurar versiones antiguas cuando se crean versiones nuevas.

* la herramienta [Purge Versions](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool)
Se utiliza como parte de la supervisión y el mantenimiento del repositorio.
Le permite intervenir para eliminar versiones antiguas de un nodo o una jerarquía de nodos, según estos parámetros:

   * Número máximo de versiones que se guardarán en el repositorio.
Cuando se supera este número, se elimina la versión más antigua.

   * La edad máxima de cualquier versión guardada en el repositorio.
Cuando la antigüedad de una versión supera este valor, se depura del repositorio.

* la [tarea de mantenimiento de purga de versión](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks). Puede programar la tarea de mantenimiento Purga de versión para eliminar automáticamente las versiones antiguas. Como resultado, esto minimiza la necesidad de utilizar manualmente las herramientas de purga de versión.

>[!CAUTION]
>
>Para optimizar el tamaño del repositorio, debe ejecutar la tarea de depuración de versiones con frecuencia. La tarea debe programarse fuera del horario laboral cuando haya una cantidad limitada de tráfico.

## Administrador de versiones {#version-manager}

Además de la depuración explícita mediante la herramienta de depuración, el Administrador de versiones se puede configurar para depurar versiones antiguas cuando se crean versiones nuevas.

Para configurar el Administrador de versiones, [cree una configuración](/help/sites-deploying/configuring-osgi.md) para:

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

Las opciones disponibles son las siguientes:

* `versionmanager.createVersionOnActivation` (Booleano, predeterminado: true) Especifica si se creará una versión cuando se activen las páginas.
Se crea una versión a menos que el agente de replicación esté configurado para suprimir la creación de versiones, que es respetado por el Administrador de versiones.
Una versión solo se crea si la activación se produce en una ruta contenida en `versionmanager.ivPaths` (consulte a continuación).

* `versionmanager.ivPaths`(Cadena[], predeterminada:  `{"/"}`) Especifica las rutas en las que se crean las versiones implícitamente al activarlas si  `versionmanager.createVersionOnActivation` se establece en true.

* `versionmanager.purgingEnabled` (Booleano, predeterminado: false) Define si se habilita o no la depuración cuando se crean nuevas versiones.

* `versionmanager.purgePaths` (Cadena[], predeterminada: {&quot;/content&quot;}) Especifica en qué rutas se purgan las versiones cuando se crean nuevas versiones.

* `versionmanager.maxAgeDays` (int, predeterminado: 30) Al purgar la versión, se eliminará cualquier versión anterior al valor configurado. Si el valor es menor que 1, la depuración no se realizará en función de la edad de la versión.

* `versionmanager.maxNumberVersions` (int, predeterminado 5) En la depuración de la versión, se eliminará cualquier versión anterior a la n-ª versión más reciente. Si el valor es menor que 1, la depuración no se realiza en función del número de versiones.

* `versionmanager.minNumberVersions` (int, predeterminado 0) El número mínimo de versiones que se conservarán independientemente de la edad. Si el valor se establece en un valor menor que 1, no se conserva ningún número mínimo de versiones.

>[!NOTE]
>
>No se recomienda mantener un gran número de versiones en el repositorio. Por lo tanto, al configurar la operación de depuración de versiones tenga en cuenta que no excluya demasiadas versiones de la depuración de otra manera, el tamaño del repositorio no se optimizará correctamente. Si mantiene un gran número de versiones debido a los requisitos del negocio, póngase en contacto con el servicio de asistencia al Adobe para encontrar formas alternativas de optimizar el tamaño del repositorio.

### Combinación de opciones de retención {#combining-retention-options}

Las opciones que definen cómo se deben conservar las versiones ( `maxAgeDays`, `maxNumberVersions`, `minNumberVersions`) se pueden combinar según sus necesidades.

Por ejemplo, al definir el número máximo de versiones que desea conservar Y la versión más antigua que desea conservar:

* Configuración:

   * `maxNumberVersions` = 7

   * `maxAgeDays` = 30

* Mediante una de las opciones siguientes:

   * 10 versiones realizadas en los últimos 60 días
   * 3 de esas versiones creadas en los últimos 30 días

* Significará que:

   * Se mantendrán las últimas 3 versiones

Por ejemplo, al definir el número máximo Y mínimo de versiones que se deben conservar Y la versión más antigua que se deben conservar:

* Configuración:

   * `maxNumberVersions` = 3
   * `maxAgeDays` = 30
   * `minNumberVersions` = 3

* Mediante una de las opciones siguientes:

   * 5 versiones realizadas hace 60 días

* Significará que:

   * Se conservarán 3 versiones

## Herramienta Purgar versiones {#purge-versions-tool}

La herramienta [Purge Versions](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) está diseñada para depurar las versiones de un nodo o una jerarquía de nodos en el repositorio. Su principal propósito es ayudarle a reducir el tamaño de su repositorio eliminando versiones antiguas de sus nodos.
