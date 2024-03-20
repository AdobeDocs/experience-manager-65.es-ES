---
title: Migración de contenido diferido
description: Obtenga información acerca de la migración de contenido diferido en Adobe Experience Manager 6.4.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
exl-id: 946c7c2a-806b-4461-a38b-9c2e5ef1e958
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 2%

---

# Migración de contenido diferido {#lazy-content-migration}

En aras de la compatibilidad con versiones anteriores, el contenido y la configuración en **/etc** y **/content** a partir de Adobe Experience Manager AEM () 6.3, no se tocará ni transformará inmediatamente con la actualización. Esto se hace para garantizar que las dependencias de las aplicaciones de los clientes en esas estructuras permanezcan intactas. AEM La funcionalidad relacionada con estas estructuras de contenido sigue siendo la misma aunque el contenido de una versión predeterminada de 6.5 se alojaría en otro lugar.

Aunque no todas esas ubicaciones pueden transformarse automáticamente, hay algunas que se retrasan `CodeUpgradeTasks` también se denomina Migración de contenido diferida. Esto permite a los clientes almacenar en déclencheur esas transformaciones automáticas reiniciando la instancia con esta propiedad del sistema:

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

Esto provoca que `CodeUpgradeTasks` para que se ejecute durante la migración.

Aunque el objetivo es una ejecución eficaz, este proceso de actualización es sincrónico y, por lo tanto, conlleva un tiempo de inactividad en función de la cantidad de contenido que se debe procesar. Adobe recomienda evaluar los tiempos de ejecución en un entorno de ensayo antes de un sistema de producción para planificar una ventana de mantenimiento adecuada.

Dado que esto suele requerir el ajuste de la aplicación, esta actividad debe realizarse junto con la implementación de la aplicación correspondiente.

A continuación se muestra la lista completa de `CodeUpgradeTasks` introducido en 6.5:

| **Nombre** | **Relevante** **AEM para las versiones de anteriores** | **Migración** **Tipo** | **Detalles** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | Inmediato |  |
| `Cq60MSMContentUpgrade` | &lt; 6,0 | Inmediato | Detecta todos los `LiveRelationShips` de `VersionStorage` que se han eliminado y agregar la propiedad de exclusión al elemento principal |
| `Cq61CloudServicesContentUpgrade` | &lt; 6,1 | Inmediato | Reestructura Cloud Services para una configuración segura de forma predeterminada |
| `Cq62ConfContentUpgrade` | &lt; 6,2 | Inmediato | Quita la vinculación basada en propiedades de **/content** hasta **/conf** (reemplazado por el mecanismo OSGi), genera la configuración OSGi correspondiente |
| `Cq62FormsContentUpgrade` | &lt; 6,2 | Inmediato | Debido a la gestión merge_preserve, la regla de denegación segura de forma predeterminada anula los permisos dados, lo que provoca la necesidad de reordenar en la actualización |
| `CQ62Html5SmartFileUpgrade` | &lt; 6,2 | Inmediato | Detecta componentes mediante el widget Html5SmartFile, busca usos del componente en el contenido y reestructura la persistencia, moviendo efectivamente el binario un nivel hacia abajo y no lo almacena en el nivel de componente. |
| `Cq62ProjectsCodeUpgrade` | &lt; 6,2 | Inmediato | Mueve proyectos de estilo antiguos de **/etc/projects** hasta **/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6,2 | Inmediato | Introduce una capa contenedora en la jerarquía (Areas) y ajusta las referencias. |
| `Cq62TargetContentUpgrade` | &lt; 6,2 | Inmediato | Establece nombres de ubicación fijos para los componentes de destino. |
| `Cq62WorkflowContentUpgrade` | &lt; 6,2 | Inmediato | Transformación compleja de modelos de flujo de trabajo anteriores a las estructuras, instancias y notificaciones de la versión 6.2 y que vuelven a combinarse desde la ubicación de copia de seguridad de **/var/backup** |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6,3 | Inmediato | Mueve recursos, esquemas de metadatos personalizados y perfiles de procesamiento de **/apps** hasta **/conf** y traduce los formularios esquema de metadatos y perfiles de metadatos de coral2 a coral3. |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6,3 | Inmediato | Mueve recursos y facetas de búsqueda personalizadas de **/apps** hasta **/conf** y traduce los formularios esquema de metadatos y perfiles de metadatos de coral2 a coral3. |
| `CQ63InboxItemsUpgrade` | &lt; 6,3 | Inmediato | Actualiza la Bandeja de entradaElementos para ordenar los elementos de la Bandeja de entrada (ajustar los metadatos para una ordenación eficaz) |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6,3 | Inmediato | Ajusta la propiedad metadataSchema de la carpeta al reemplazar las rutas relativas a **/conf** en lugar de **/apps** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6,3 | Inmediato | Ajuste de la estructura de navegación |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6,3 | Inmediato | Mueve las configuraciones personalizadas para los paneles de monitorización de **/libs** y **/apps** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6,3 | Inmediato | Traduce la propiedad processingProfile (utilizada hasta 6.1) en Assets para que coincida con la estructura de 6.3 y versiones posteriores. También ajusta las rutas relativas del perfil a **/conf** en lugar de **/apps**. |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6,3 | Inmediato | Tarea de actualización que elimina las entradas de menú del CRXDE Lite y la consola web obsoletas en caso de que se produzca una actualización. |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6,3 | Retrasado | Al mover las configuraciones de nube de SRP, las configuraciones de palabras observadas de la comunidad, se limpia **/etc/social** y **/etc/enablement** (todas las referencias y datos deben ajustarse cuando se ejecute la migración diferida; ya no debe haber ninguna parte de la aplicación que dependa de esta estructura). |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6,4 | Retrasado | Limpia **/etc/cloudsettings** (que contiene Configuración de ContextHub). La configuración se migra automáticamente en el primer acceso. En caso de que la migración de contenido diferido se inicie junto con la actualización de este contenido en, **/etc/cloudsettings** debe preservarse mediante el paquete antes de la actualización y reinstalarse para que se inicie la transformación implícita, junto con una desinstalación posterior del paquete una vez finalizado. |
| `CQ64UsersTitleFixTask` | &lt; 6,4 | Retrasado | Ajusta la estructura de título heredada al título en el nodo de perfil del usuario. |
| `CQ64CommerceMigrationTask` | &lt; 6,4 | Retrasado | Migración del contenido comercial desde **/etc/commerce** hasta **/var/commerce**. Durante la migración, el contenido se mueve y las referencias al contenido movido se actualizan para reflejar la nueva ubicación. |
| `CQ65DMMigrationTask` | &lt; 6,5 | Retrasado | Migración de la configuración del catálogo heredado y la configuración de los Cloud Service de Dynamic Media desde **/etc** hasta **/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6,5 | Retrasado | Limpie los clientlibs heredados existentes en **/etc/clientlibs** |
