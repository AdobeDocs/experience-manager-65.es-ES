---
cloud: Experience Cloud
product: adobe experience manager
solution: Experience Manager, Experience Manager Sites
audience: end-user
user-guide-title: Guía de implementación de AEM 6.5
breadcrumb-title: Guía de implementación
user-guide-description: Obtenga más información sobre la instalación, la implementación y la arquitectura de Adobe Experience Manager 6.5, incluida nuestra implementación en la nube de Adobe Managed Services.
feature: Deploying
role: Architect
source-git-commit: f29612ee633d2a62144b770f3c225fc82b9174f8
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 19%

---


# AEM Guía del usuario de implementación de.5 {#deploying}

+ [Guía del usuario de implementación](home.md)
+ AEM Introducción a la plataforma de {#introduction}
   + [AEM Introducción a la plataforma de](platform.md)
   + [Requisitos técnicos](technical-requirements.md)
   + [AEM Elementos de almacenamiento en 6.5](storage-elements-in-aem-6.md)
   + [AEM con MongoDB](aem-with-mongodb.md)
+ Implementación de AEM {#deploying}
   + [Implementación y mantenimiento](deploy.md)
   + [Implementaciones recomendadas](recommended-deploys.md)
   + [Instalación del servidor de aplicaciones](application-server-install.md)
   + [Instalación independiente personalizada](custom-standalone-install.md)
   + [Línea de comandos: start y stop](command-line-start-and-stop.md)
   + [AEM Configuración de almacenes de nodos y almacenes de datos en el 6](data-store-config.md)
   + [Limpieza de revisión](revision-cleanup.md)
   + [Consultas e indexación de Oak](queries-and-indexing.md)
   + [AEM Cómo ejecutar el con TarMK Cold Standby](tarmk-cold-standby.md)
   + [AEM Compatibilidad con RDBMS en 6.5](rdbms-support-in-aem.md)
   + [Indexación mediante el Jar de Oak-run](indexing-via-the-oak-run-jar.md)
   + [Casos de uso de indexación Oak-run.jar](oak-run-indexing-usecases.md)
   + [Solución de problemas de índices Oak](troubleshooting-oak-indexes.md)
   + [Inclusión En La Recopilación De Estadísticas De Uso Agregadas](opt-in-aggregated-usage-statistics.md)
   + [Solución de problemas](troubleshooting.md)
+ Configurar AEM {#configuring}
   + [Conceptos básicos de configuración](configuring.md)
   + [Registro](configure-logging.md)
   + [Configurar OSGi](configuring-osgi.md)
   + [Ajustes de configuración de OSGi](osgi-configuration-settings.md)
   + [Ejecutar modos](configure-runmodes.md)
   + [Consola web](web-console.md)
   + [Replicación](replication.md)
   + [Duplicación mediante SSL mutuo](mssl-replication.md)
   + [Solución de problemas de replicación](troubleshoot-rep.md)
   + [Caducidad de objetos estáticos](expiration-static-objects.md)
   + [Depuración de versiones](version-purging.md)
   + [AEM Monitorización y mantenimiento de la instancia de](monitoring-and-maintaining.md)
   + [Descargando trabajos](offloading.md)
   + [Inicio de sesión único](single-sign-on.md)
   + [Asignación de recursos](resource-mapping.md)
   + [Habilitar HTTP sobre SSL](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/ssl-by-default.html)
   + [Comprobaciones de coherencia y recorrido](consistency-check.md)
   + [Directrices de rendimiento](performance-guidelines.md)
   + [Optimización del rendimiento](configuring-performance.md)
   + [Guía de rendimiento de Assets](assets-performance-sizing.md)
   + [Artículos sobre procedimientos de configuración](ht-deploy.md)
   + [Configuración de la consola web](configuring-web-console.md)
+ AEM Actualización a 6.5 {#upgrading}
   + [AEM Actualización a 6.5](upgrade.md)
   + [Planificación de la actualización](upgrade-planning.md)
   + [Evaluación de la complejidad de la actualización con Pattern Detector](pattern-detector.md)
   + [AEM Compatibilidad con versiones anteriores en 6.5](backward-compatibility.md)
   + [Procedimiento de actualización](upgrade-procedure.md)
   + [Realización de una actualización in situ](in-place-upgrade.md)
   + [Uso de la reindexación sin conexión para reducir el tiempo de inactividad durante una actualización](upgrade-offline-reindexing.md)
   + [Migración de contenido diferido](lazy-content-migration.md)
   + [Uso de la herramienta de migración CRX2Oak](using-crx2oak.md)
   + [Tareas de mantenimiento previas a la actualización](pre-upgrade-maintenance-tasks.md)
   + [Comprobaciones posteriores a la actualización y solución de problemas](post-upgrade-checks-and-troubleshooting.md)
   + [Actualización de Forms de búsqueda personalizada](upgrading-custom-search-forms.md)
   + [Actualizaciones sostenibles](sustainable-upgrades.md)
   + [Actualizar código y personalizaciones](upgrading-code-and-customizations.md)
   + [Pasos de actualización para instalaciones de Application Server](app-server-upgrade.md)
   + [Lista de paquetes obsoletos desinstalados después de la actualización](obsolete-bundles.md)
+ Reestructuración de repositorios {#restructuring}
   + [AEM Reestructuración de repositorios en 6.5](repository-restructuring.md)
   + [AEM Reestructuración común de repositorios en 6.5](all-repository-restructuring-in-aem-6-5.md)
   + [AEM Reestructuración de repositorios de Sites en 6.5](sites-repository-restructuring-in-aem-6-5.md)
   + [AEM Reestructuración del repositorio de activos en la versión 6.5 de](assets-repository-restructuring-in-aem-6-5.md)
   + [Reestructuración de repositorios de Dynamic Media AEM en 6.5](dynamicmedia-repository-restructuring-in-aem-6-5.md)
   + [Reestructuración de repositorios de Forms AEM en 6.5](forms-repository-restructuring-in-aem-6-5.md)
   + [AEM Reestructuración del repositorio de comercio electrónico en la versión 6.5 de](ecommerce-repository-restructuring-in-aem-6-5.md)
   + [Reestructuración de repositorios para AEM Communities en 6.5](communities-repository-restructuring-in-aem-6-5.md)
+ Prácticas recomendadas   {#practices}
   + [Implementación de prácticas recomendadas](best-practices.md)
   + [Árbol de rendimiento](performance-tree.md)
   + [Prácticas recomendadas para las pruebas de rendimiento](best-practices-for-performance-testing.md)
   + [Prácticas recomendadas para consultas e indexación](best-practices-for-queries-and-indexing.md)
   + [Interfaz de usuario de Recommendations para clientes](ui-recommendations.md)
   + [Rendimiento y escalabilidad](performance.md)
