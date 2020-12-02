---
cloud: experience-cloud
product: adobe experience manager
solution: Experience Manager, Experience Manager Sites
audience: end-user
user-guide-title: Guía de implementación de AEM 6.5
breadcrumb-title: Guía de implementación
user-guide-description: Obtenga más información sobre la instalación, la implementación y la arquitectura de Adobe Experience Manager 6.5, incluida nuestra implementación en la nube de Adobe Managed Services.
translation-type: tm+mt
source-git-commit: 984e50ec1a523ff8a4f618016797c326fd679511
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 18%

---


# Guía del usuario de implementación de AEM 6.5 {#deploying}

+ [Guía del usuario de implementación](home.md)
+ Introducción a la Plataforma AEM {#introduction}
   + [Introducción a la Plataforma AEM](platform.md)
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
   + [Consultas de roble e indexación](queries-and-indexing.md)
   + [Cómo ejecutar AEM con TarMK Cold Standby](tarmk-cold-standby.md)
   + [Compatibilidad con RDBMS en AEM 6.5](rdbms-support-in-aem.md)
   + [Indexación a través del Jar de Oak-run](indexing-via-the-oak-run-jar.md)
   + [Casos de uso de indización de Oak-run.jar](oak-run-indexing-usecases.md)
   + [Resolución de problemas con los índices Oak](troubleshooting-oak-indexes.md)
   + [Opción En La Recopilación De Estadísticas De Uso Agregado](opt-in-aggregated-usage-statistics.md)
   + [Solución de problemas](troubleshooting.md)
+ Configuración de AEM {#configuring}
   + [Conceptos básicos de configuración](configuring.md)
   + [Registro](configure-logging.md)
   + [Configuración de OSGi](configuring-osgi.md)
   + [Configuración de OSGi](osgi-configuration-settings.md)
   + [Ejecutar modos](configure-runmodes.md)
   + [Consola web](web-console.md)
   + [Replicación](replication.md)
   + [Replicar usando SSL mutuo](mssl-replication.md)
   + [Resolución de problemas de replicación](troubleshoot-rep.md)
   + [Caducidad de objetos estáticos](expiration-static-objects.md)
   + [Depuración de versiones](version-purging.md)
   + [Monitoreo y mantenimiento de la instancia de AEM](monitoring-and-maintaining.md)
   + [Descarga de trabajos](offloading.md)
   + [Inicio de sesión único](single-sign-on.md)
   + [Asignación de recursos](resource-mapping.md)
   + [Habilitación de HTTP sobre SSL](/help/sites-administering/ssl-by-default.md)
   + [Comprobaciones de coherencia y de recorrido](consistency-check.md)
   + [Directrices de rendimiento](performance-guidelines.md)
   + [Optimización del rendimiento](configuring-performance.md)
   + [Guía de rendimiento de recursos](assets-performance-sizing.md)
   + [Artículos de procedimientos de configuración](ht-deploy.md)
   + [Configuración de la consola web](configuring-web-console.md)
+ Actualización a AEM 6.5 {#upgrading}
   + [Actualización a AEM 6.5](upgrade.md)
   + [Planificación de la actualización](upgrade-planning.md)
   + [Evaluación de la complejidad de la actualización con el detector de patrones](pattern-detector.md)
   + [Compatibilidad con versiones anteriores en AEM 6.5](backward-compatibility.md)
   + [Procedimiento de actualización](upgrade-procedure.md)
   + [Realización de una actualización in situ](in-place-upgrade.md)
   + [Uso de la reindexación sin conexión para reducir el tiempo de inactividad durante una actualización](upgrade-offline-reindexing.md)
   + [Migración de contenido diferido](lazy-content-migration.md)
   + [Uso de la herramienta de migración CRX2Oak](using-crx2oak.md)
   + [Tareas de mantenimiento previas a la actualización](pre-upgrade-maintenance-tasks.md)
   + [Comprobaciones posteriores a la actualización y resolución de problemas](post-upgrade-checks-and-troubleshooting.md)
   + [Actualización de Forms de búsqueda personalizada](upgrading-custom-search-forms.md)
   + [Upgrades sostenibles](sustainable-upgrades.md)
   + [Actualización del código y las personalizaciones](upgrading-code-and-customizations.md)
   + [Pasos de actualización para las instalaciones de Application Server](app-server-upgrade.md)
   + [Lista de paquetes obsoletos desinstalados tras la actualización](obsolete-bundles.md)
+ Reestructuración del repositorio {#restructuring}
   + [Reestructuración del repositorio en AEM 6.5](repository-restructuring.md)
   + [Reestructuración común de repositorios en AEM 6.5](all-repository-restructuring-in-aem-6-5.md)
   + [Reestructuración del repositorio de sitios en AEM 6.5](sites-repository-restructuring-in-aem-6-5.md)
   + [Reestructuración del repositorio de activos en AEM 6.5](assets-repository-restructuring-in-aem-6-5.md)
   + [Reestructuración del repositorio de Dynamic Media en AEM 6.5](dynamicmedia-repository-restructuring-in-aem-6-5.md)
   + [Reestructuración del repositorio de Forms en AEM 6.5](forms-repository-restructuring-in-aem-6-5.md)
   + [Reestructuración del repositorio de comercio electrónico en AEM 6.5](ecommerce-repository-restructuring-in-aem-6-5.md)
   + [Reestructuración del repositorio para AEM Communities en 6.5](communities-repository-restructuring-in-aem-6-5.md)
+ eCommerce {#ecommerce}
   + [Información general sobre comercio electrónico](ecommerce.md)
   + [COMMERCE CLOUD SAP](sap-commerce-cloud.md)
   + [Commerce Cloud de Salesforce](https://github.com/adobe/commerce-salesforce)
   + [Magento](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)
+ Prácticas recomendadas   {#practices}
   + [Implementación de optimizaciones](best-practices.md)
   + [Árbol de rendimiento](performance-tree.md)
   + [Prácticas recomendadas para pruebas de rendimiento](best-practices-for-performance-testing.md)
   + [Prácticas recomendadas para Consultas e indexación](best-practices-for-queries-and-indexing.md)
   + [Interfaz de usuario de Recommendations para clientes](ui-recommendations.md)
   + [Rendimiento y escalabilidad](performance.md)
