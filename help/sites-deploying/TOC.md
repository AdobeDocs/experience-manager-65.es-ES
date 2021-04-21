---
cloud: Experience Cloud
product: adobe experience manager
solution: Experience Manager, Experience Manager Sites
audience: end-user
user-guide-title: Guía de implementación de AEM 6.5
breadcrumb-title: Guía de implementación
user-guide-description: Obtenga más información sobre la instalación, la implementación y la arquitectura de Adobe Experience Manager 6.5, incluida nuestra implementación en la nube de Adobe Managed Services.
feature: Implementación
role: Architect
translation-type: tm+mt
source-git-commit: ad67634278088f8f953fde61a3543acdd70537dd
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 18%

---


# Guía del usuario de implementación de AEM 6.5 {#deploying}

+ [Guía del usuario sobre implementación](home.md)
+ Introducción a la plataforma de AEM {#introduction}
   + [Introducción a la plataforma AEM](platform.md)
   + [Requisitos técnicos](technical-requirements.md)
   + [Elementos de almacenamiento en AEM 6.5](storage-elements-in-aem-6.md)
   + [AEM con MongoDB](aem-with-mongodb.md)
+ Implementación de AEM {#deploying}
   + [Implementación y mantenimiento](deploy.md)
   + [Implementaciones recomendadas](recommended-deploys.md)
   + [Instalación del servidor de aplicaciones](application-server-install.md)
   + [Instalación independiente personalizada](custom-standalone-install.md)
   + [Línea de comandos: start y stop](command-line-start-and-stop.md)
   + [Configuración de almacenes de nodos y almacenes de datos en AEM 6](data-store-config.md)
   + [Limpieza de revisión](revision-cleanup.md)
   + [Consultas e indexación de Oak](queries-and-indexing.md)
   + [Ejecución de AEM con el modo de espera pasiva TarMK](tarmk-cold-standby.md)
   + [Compatibilidad con RDBMS en AEM 6.5](rdbms-support-in-aem.md)
   + [Indexación a través de Oak-run Jar](indexing-via-the-oak-run-jar.md)
   + [Casos de uso de indexación de Oak-run.jar](oak-run-indexing-usecases.md)
   + [Resolución de problemas de índices Oak](troubleshooting-oak-indexes.md)
   + [Inclusión En La Recopilación De Estadísticas De Uso Agregado](opt-in-aggregated-usage-statistics.md)
   + [Solución de problemas](troubleshooting.md)
+ Configuración de AEM {#configuring}
   + [Conceptos básicos de configuración](configuring.md)
   + [Registro](configure-logging.md)
   + [Configuración de OSGi](configuring-osgi.md)
   + [Ajustes de configuración de OSGi](osgi-configuration-settings.md)
   + [Ejecutar modos](configure-runmodes.md)
   + [Consola web](web-console.md)
   + [Replicación](replication.md)
   + [Replicar usando SSL mutuo](mssl-replication.md)
   + [Solución de problemas de replicación](troubleshoot-rep.md)
   + [Caducidad de objetos estáticos](expiration-static-objects.md)
   + [Depuración de versiones](version-purging.md)
   + [Supervisión y mantenimiento de la instancia de AEM](monitoring-and-maintaining.md)
   + [Descarga de trabajos](offloading.md)
   + [Inicio de sesión único](single-sign-on.md)
   + [Asignación de recursos](resource-mapping.md)
   + [Habilitación de HTTP en SSL](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/ssl-by-default.html)
   + [Comprobaciones de coherencia y travesía](consistency-check.md)
   + [Directrices de rendimiento](performance-guidelines.md)
   + [Optimización del rendimiento](configuring-performance.md)
   + [Guía de rendimiento de recursos](assets-performance-sizing.md)
   + [Artículos de procedimientos de configuración](ht-deploy.md)
   + [Configuración de la consola web](configuring-web-console.md)
+ Actualización a AEM 6.5 {#upgrading}
   + [Actualización a AEM 6.5](upgrade.md)
   + [Planificación de la actualización](upgrade-planning.md)
   + [Evaluación de la complejidad de la actualización con Pattern Detector](pattern-detector.md)
   + [Compatibilidad con versiones anteriores en AEM 6.5](backward-compatibility.md)
   + [Procedimiento de actualización](upgrade-procedure.md)
   + [Realización de una actualización in situ](in-place-upgrade.md)
   + [Uso de la reindexación sin conexión para reducir el tiempo de inactividad durante una actualización](upgrade-offline-reindexing.md)
   + [Migración de contenido diferido](lazy-content-migration.md)
   + [Uso de la herramienta de migración CRX2Oak](using-crx2oak.md)
   + [Tareas de mantenimiento previas a la actualización](pre-upgrade-maintenance-tasks.md)
   + [Comprobación y solución de problemas posteriores a la actualización](post-upgrade-checks-and-troubleshooting.md)
   + [Actualización de Forms de búsqueda personalizada](upgrading-custom-search-forms.md)
   + [Actualizaciones sostenibles](sustainable-upgrades.md)
   + [Actualización de código y personalizaciones](upgrading-code-and-customizations.md)
   + [Pasos de actualización para las instalaciones del servidor de aplicaciones](app-server-upgrade.md)
   + [Lista de paquetes obsoletos desinstalados después de la actualización](obsolete-bundles.md)
+ Reestructuración del repositorio {#restructuring}
   + [Reestructuración de repositorios en AEM 6.5](repository-restructuring.md)
   + [Reestructuración común de repositorios en AEM 6.5](all-repository-restructuring-in-aem-6-5.md)
   + [Reestructuración del repositorio de sitios en AEM 6.5](sites-repository-restructuring-in-aem-6-5.md)
   + [Reestructuración del repositorio de activos en AEM 6.5](assets-repository-restructuring-in-aem-6-5.md)
   + [Reestructuración del repositorio de Dynamic Media en AEM 6.5](dynamicmedia-repository-restructuring-in-aem-6-5.md)
   + [Reestructuración del repositorio de Forms en AEM 6.5](forms-repository-restructuring-in-aem-6-5.md)
   + [Reestructuración de repositorios de comercio electrónico en AEM 6.5](ecommerce-repository-restructuring-in-aem-6-5.md)
   + [Reestructuración de repositorios para AEM Communities en la versión 6.5](communities-repository-restructuring-in-aem-6-5.md)
+ eCommerce {#ecommerce}
   + [Información general sobre comercio electrónico](ecommerce.md)
   + [Commerce Cloud SAP](sap-commerce-cloud.md)
   + [Commerce Cloud de Salesforce](https://github.com/adobe/commerce-salesforce)
   + [Magento](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)
+ Prácticas recomendadas   {#practices}
   + [Prácticas Recomendadas De Implementación](best-practices.md)
   + [Árbol de rendimiento](performance-tree.md)
   + [Prácticas recomendadas para pruebas de rendimiento](best-practices-for-performance-testing.md)
   + [Prácticas recomendadas para consultas e indexación](best-practices-for-queries-and-indexing.md)
   + [Interfaz de usuario de Recommendations para clientes](ui-recommendations.md)
   + [Rendimiento y escalabilidad](performance.md)
