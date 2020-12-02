---
title: Migración de contenido diferido
seo-title: Migración de contenido diferido
description: Obtenga información sobre la migración de contenido flotante en AEM 6.4.
seo-description: Obtenga información sobre la migración de contenido flotante en AEM 6.4.
uuid: f5b0aa84-5638-4708-9da2-89964d394632
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: d72b8844-d782-4b5b-8999-338217dbefb9
docset: aem65
translation-type: tm+mt
source-git-commit: 7d93df515bf98f0a947428b8093e059d63b21a34
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 6%

---


# Migración de contenido diferido {#lazy-content-migration}

En aras de la compatibilidad con versiones anteriores, el contenido y la configuración de **/etc** y **/content** a partir de AEM 6.3 no se tocarán ni transformarán inmediatamente con la actualización. Esto se hace para garantizar que la dependencia de las aplicaciones de los clientes en esas estructuras permanezca intacta. La funcionalidad relacionada con estas estructuras de contenido sigue siendo la misma, aunque el contenido dentro y fuera de la caja AEM 6.5 se alojaría en otro lugar.

Aunque no todas esas ubicaciones se pueden transformar automáticamente, hay algunas `CodeUpgradeTasks` retrasadas también denominadas Migración de contenido flotante. Esto permite a los clientes activar estas transformaciones automáticas reiniciando la instancia con esta propiedad del sistema:

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

Esto hará que `CodeUpgradeTasks` se ejecute durante la migración.

Aunque el objetivo es una ejecución eficiente, este proceso de actualización es sincrónico y, por lo tanto, incluye un tiempo de inactividad en función de la cantidad de contenido que debe procesarse. Se recomienda evaluar los tiempos de ejecución en un entorno de fase antes de un sistema de producción para planificar una ventana de mantenimiento según el valor.

Como esto generalmente también requiere ajustar la aplicación, esta actividad debe realizarse junto con la implementación de la aplicación correspondiente.

A continuación se presenta la lista completa de `CodeUpgradeTasks` introducida en la versión 6.5:

| **Nombre** | **** **Relevante para versiones AEM anteriores a** | **** **MigrationType** | **Detalles** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5=&quot;&quot;> | Inmediato |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | Inmediato | Detecta todos los `LiveRelationShips` de `VersionStorage` que se han eliminado y agrega la propiedad de exclusión a parent |
| `Cq61CloudServicesContentUpgrade` | &lt; 6=&quot;&quot;> | Inmediato | Reestructura cloudservices para una configuración segura de forma predeterminada |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | Inmediato | Quita la vinculación basada en propiedades de **/content** a **/conf** (reemplazada por el mecanismo OSGi), genera la configuración OSGi correspondiente |
| `Cq62FormsContentUpgrade` | &lt; 6=&quot;&quot;> | Inmediato | Debido a que merge_preserve maneja la regla de denegación segura de forma predeterminada, invalida los permisos dados, lo que provoca la necesidad de reordenar al actualizar |
| `CQ62Html5SmartFileUpgrade` | &lt; 6=&quot;&quot;> | Inmediato | Detecta los componentes que utilizan el widget Html5SmartFile, busca los usos del componente en el contenido y reestructura la persistencia, moviendo el binario un nivel hacia abajo y no almacenándolo en el nivel del componente. |
| `Cq62ProjectsCodeUpgrade` | &lt; 6=&quot;&quot;> | Inmediato | Mueve proyectos de estilo antiguo de **/etc/projects** a **/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6=&quot;&quot;> | Inmediato | Introduce una capa de contenedor en la jerarquía (Áreas) y ajusta las referencias. |
| `Cq62TargetContentUpgrade` | &lt; 6=&quot;&quot;> | Inmediato | Establece los nombres de ubicación fijos en los componentes de destinatario. |
| `Cq62WorkflowContentUpgrade` | &lt; 6=&quot;&quot;> | Inmediato | Transformación compleja de modelos de flujo de trabajo que preceden a estructuras, instancias y notificaciones de 6.2 y que luego se combinan desde la ubicación de backup desde **/var/backup** |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | Inmediato | Mueve recursos, esquemas de metadatos personalizados y perfiles de procesamiento de **/apps** a **/conf** y traduce los formularios de perfiles de metadatos y esquemas de metadatos de coral2 a coral3. |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6=&quot;&quot;> | Inmediato | Mueve los recursos y las facetas de búsqueda personalizadas de **/apps** a **/conf** y traduce los formularios de perfiles de metadatos y esquemas de metadatos de coral2 a coral3. |
| `CQ63InboxItemsUpgrade` | &lt; 6=&quot;&quot;> | Inmediato | Actualiza la bandeja de entradaElementos para ordenar los elementos de la bandeja de entrada (ajuste de metadatos para una ordenación eficaz) |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6=&quot;&quot;> | Inmediato | Ajusta la propiedad metadataSchema de la carpeta reemplazando las rutas relativas a **/conf** en lugar de **/apps** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6=&quot;&quot;> | Inmediato | Ajuste de la estructura de navegación |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6=&quot;&quot;> | Inmediato | Mueve las configuraciones personalizadas para los paneles de supervisión de **/libs** y **/apps** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6=&quot;&quot;> | Inmediato | Traduce la propiedad processingProfile (utilizada hasta 6.1) en Assets para que coincida con la estructura 6.3 y posterior. También ajusta las rutas relativas del perfil a **/conf** en lugar de **/apps**. |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6=&quot;&quot;> | Inmediato | Tarea de actualización que elimina las entradas del menú CRXDE Lite y consola web obsoletas en caso de una actualización. |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6=&quot;&quot;> | Retrasado | Moviendo configuraciones de nube SRP, configuraciones de palabras de observación de la comunidad, limpia **/etc/social** y **/etc/enablement** (cualquier referencia y datos debe ajustarse cuando se ejecute la migración floja; ninguna parte de la aplicación debe depender de esta estructura). |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | Retrasado | Limpia **/etc/cloudsettings** (que contiene la configuración de ContextHub). La configuración se migra automáticamente en el primer acceso. En caso de que la migración de contenido diferido se inicie junto con la actualización de este contenido en **/etc/cloudsettings** debe conservarse mediante paquete antes de la actualización y reinstalarse para que se inicie la transformación implícita, junto con la posterior desinstalación del paquete después de la finalización. |
| `CQ64UsersTitleFixTask` | &lt; 6=&quot;&quot;> | Retrasado | Ajusta la estructura de título heredado al título en el nodo de perfil de usuario. |
| `CQ64CommerceMigrationTask` | &lt; 6=&quot;&quot;> | Retrasado | Migrar contenido comercial de **/etc/commerce** a **/var/commerce**. Durante la migración, el contenido se mueve y las referencias al contenido movido se actualizan para reflejar la nueva ubicación. |
| `CQ65DMMigrationTask` | &lt; 6.5 | Retrasado | Migrar la configuración del catálogo heredado y la configuración de los servicios de nube de medios dinámicos de **/etc** a **/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6=&quot;&quot;> | Retrasado | Limpiar clientes heredados existentes en **/etc/clientlibs** |
