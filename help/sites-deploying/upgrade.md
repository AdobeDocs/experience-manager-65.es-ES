---
title: Actualización a AEM 6.5
seo-title: Actualización a AEM 6.5
description: Obtenga información sobre los conceptos básicos para actualizar una instalación AEM anterior a AEM 6.5.
seo-description: Obtenga información sobre los conceptos básicos para actualizar una instalación AEM anterior a AEM 6.5.
uuid: 45368056-273c-4f1a-9da6-e7ba5c2bbc0d
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: ebd99cc4-8762-4c28-a177-d62dac276afe
docset: aem65
targetaudience: target-audience upgrader
translation-type: tm+mt
source-git-commit: cbd48b28798c1bb7c00175fc1faecfea5484b07b
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 4%

---


# Actualización a AEM 6.5 {#upgrading-to-aem}

En esta sección tratamos la actualización de una instalación de AEM a AEM 6.5:

* [Planificación de la actualización](/help/sites-deploying/upgrade-planning.md)
* [Evaluación de la complejidad de la actualización con el detector de patrones](/help/sites-deploying/pattern-detector.md)
* [Compatibilidad con versiones anteriores en AEM 6.5](/help/sites-deploying/backward-compatibility.md)

<!--* [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->
* [Procedimiento de actualización](/help/sites-deploying/upgrade-procedure.md)
* [Actualización del código y las personalizaciones](/help/sites-deploying/upgrading-code-and-customizations.md)
* [Tareas de mantenimiento previas a la actualización](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [Realización de una actualización in situ](/help/sites-deploying/in-place-upgrade.md)
* [Comprobaciones posteriores a la actualización y resolución de problemas](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [Upgrades sostenibles](/help/sites-deploying/sustainable-upgrades.md)
* [Migración de contenido diferido](/help/sites-deploying/lazy-content-migration.md)
* [Reestructuración del repositorio en AEM 6.5](/help/sites-deploying/repository-restructuring.md)

Para facilitar la referencia a los casos AEM implicados en estos procedimientos, se utilizan los términos siguientes en todos estos artículos:

* La instancia *source* es la instancia de AEM desde la que está realizando la actualización.
* La instancia de *destinatario* es la que se está actualizando.

>[!NOTE]
>
>Como parte de los esfuerzos por mejorar la fiabilidad de las actualizaciones, AEM ha sido objeto de una reestructuración general de los repositorios. Para obtener más información sobre cómo alinearse con la nueva estructura, consulte [Reestructuración del repositorio en AEM.](/help/sites-deploying/repository-restructuring.md)

## ¿Qué Ha Cambiado? {#what-has-changed}

A continuación se indican los principales cambios de nota en las últimas versiones de AEM:

AEM 6.0 presentó el nuevo repositorio Jackrabbit Oak. Los administradores de persistencia se reemplazaron por [microneles](/help/sites-deploying/platform.md#contentbody_title_4). A partir de la versión 6.1, CRX2 ya no es compatible. Es necesario ejecutar una herramienta de migración llamada crx2oak para migrar repositorios CRX2 de instancias 5.6.1. Para obtener más información, consulte [Uso de la herramienta de migración CRX2OAK](/help/sites-deploying/using-crx2oak.md).

Si se va a utilizar Asset Insights y se está actualizando desde una versión anterior a AEM 6.2, los recursos deben migrarse y deben generarse ID mediante un archivo .porter JMX. En nuestras pruebas internas, se migraron 125.000 recursos en un entorno TarMK en una hora, pero los resultados pueden variar.

6.3 introdujo un nuevo formato para la `SegmentNodeStore`, que es la base de la implementación de TarMK. Si está actualizando desde una versión anterior a AEM 6.3, esto requerirá una migración del repositorio como parte de la actualización, lo que implica downtime del sistema.

Adobe Engineering calcula que esto es de unos 20 minutos. Tenga en cuenta que no será necesario volver a indexar. Además, se ha lanzado una nueva versión de la herramienta crx2oak para trabajar con el nuevo formato de repositorio.

**Esta migración no es necesaria si se actualiza de AEM 6.3 a AEM 6.5.**

Las tareas de mantenimiento previas a la actualización se han optimizado para admitir la automatización.

Las opciones de uso de la línea de comandos de la herramienta crx2oak han sido cambiadas para facilitar la automatización y admitir más rutas de actualización.

Las comprobaciones posteriores a la actualización también han permitido la automatización.

La recolección periódica de elementos no utilizados de las revisiones y la recolección de elementos no utilizados del almacén de datos son ahora tareas de mantenimiento rutinarias que deben realizarse periódicamente. Con la introducción de AEM 6.3, Adobe apoya y recomienda la limpieza de revisiones en línea. Consulte [Limpieza de revisión](/help/sites-deploying/revision-cleanup.md) para obtener información sobre cómo configurar estas tareas.

AEM presenta recientemente el [detector de patrones](/help/sites-deploying/pattern-detector.md) para evaluar la complejidad de la actualización a medida que planifica el inicio para la actualización. 6.5 también se centra en [compatibilidad con versiones anteriores](/help/sites-deploying/backward-compatibility.md) de las funciones. Finalmente, también se agregan las optimizaciones para [upgrades sostenibles](/help/sites-deploying/sustainable-upgrades.md).

Para obtener más información sobre los cambios que se han producido en las versiones AEM recientes, consulte las notas de la versión completas:

* [https://helpx.adobe.com/es/experience-manager/6-2/release-notes.html](https://helpx.adobe.com/es/experience-manager/6-2/release-notes.html)
* [https://helpx.adobe.com/es/experience-manager/6-3/release-notes.html](https://helpx.adobe.com/es/experience-manager/6-3/release-notes.html)
* [https://helpx.adobe.com/es/experience-manager/6-4/release-notes.html](https://helpx.adobe.com/es/experience-manager/6-4/release-notes.html)
* [https://helpx.adobe.com/es/experience-manager/6-5/release-notes.html](https://helpx.adobe.com/es/experience-manager/6-5/release-notes.html)

## Información general de actualización {#upgrade-overview}

La actualización de AEM es un proceso de varios pasos, a veces de varios meses. Se ha proporcionado el siguiente esquema como resumen de lo que se incluye en un proyecto de actualización y del contenido que se ha incluido en esta documentación:

![screen_shot_2018-03-30at80708am](assets/screen_shot_2018-03-30at80708am.png)

## Flujo de actualización {#upgrade-overview-1}

El diagrama siguiente captura el flujo general recomendado que resalta el método de actualización. Tenga en cuenta la referencia a las nuevas funciones que hemos introducido. La actualización debe estar en inicio con el detector de patrones (consulte [Evaluación de la complejidad de la actualización con el detector de patrones](/help/sites-deploying/pattern-detector.md)), que debería permitirle decidir la ruta que desee tomar para la compatibilidad con AEM 6.4 según los patrones en el informe generado.

En 6.5 se ha centrado la atención en mantener todas las nuevas funciones compatibles con versiones anteriores, pero en los casos en que aún se observan algunos problemas de compatibilidad con versiones anteriores, el modo de compatibilidad permite aplazar temporalmente el desarrollo para mantener el código personalizado conforme con 6.5. Este método le ayuda a evitar el esfuerzo de desarrollo inmediatamente después de la actualización (consulte [Compatibilidad con versiones anteriores en AEM 6.5](/help/sites-deploying/backward-compatibility.md)).

Por último, en su ciclo de desarrollo 6.5, las funciones introducidas en Actualizaciones sostenibles (consulte [Actualizaciones sostenibles](/help/sites-deploying/sustainable-upgrades.md)) le ayudan a seguir las mejores prácticas para que las futuras actualizaciones sean aún más eficientes y sin problemas.

![6_4_upgrade_overviewflowchart-newpage3](assets/6_4_upgrade_overviewflowchart-newpage3.png)

