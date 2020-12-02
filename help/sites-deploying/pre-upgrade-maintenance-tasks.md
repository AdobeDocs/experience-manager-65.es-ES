---
title: Tareas de mantenimiento previas a la actualización
seo-title: Tareas de mantenimiento previas a la actualización
description: Obtenga información sobre las tareas previas a la actualización en AEM.
seo-description: Obtenga información sobre las tareas previas a la actualización en AEM.
uuid: 5da1cfc7-8a10-47b1-aafb-2cd112e3f818
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 291c91e5-65ff-473d-ac11-3da480239e76
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '2158'
ht-degree: 0%

---


# Tareas de mantenimiento previas a la actualización{#pre-upgrade-maintenance-tasks}

Antes de comenzar la actualización, es importante que siga estas tareas de mantenimiento para asegurarse de que el sistema está listo y puede revertirse en caso de que se produzcan problemas:

* [Asegurar suficiente espacio en disco](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [AEM de copia de seguridad completa](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [Realizar copia de seguridad de cambios en /etc](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#backup-changes-etc)
* [Generar el archivo quickstart.properties](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [Configurar la depuración del flujo de trabajo y del registro de auditoría](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [Instalar, configurar y ejecutar las Tareas previas a la actualización](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [Deshabilitar los módulos de inicio de sesión personalizados](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-login-modules)
* [Quitar Actualizaciones Del Directorio /install](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [Detener Cualquier Instancia En Espera En Frío](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [Deshabilitar trabajos programados personalizados](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [Ejecutar limpieza de revisión sin conexión](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [Ejecutar recopilación de elementos no utilizados del almacén de datos](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [Actualizar el Esquema de la base de datos si es necesario](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [Eliminar usuarios que podrían obstaculizar la actualización](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#delete-users-that-might-hinder-the-upgrade)

* [Rotar archivos de registro](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## Asegurar suficiente espacio en disco {#ensure-sufficient-disk-space}

Al ejecutar la actualización, además de las actividades de actualización de contenido y código, será necesario realizar una migración de repositorio. La migración creará una copia del repositorio en el nuevo formato de la barra de segmentos. Como resultado, necesitará suficiente espacio en disco para conservar una segunda versión, potencialmente más grande, del repositorio.

## Backup completo de AEM {#fully-back-up-aem}

AEM debe realizarse una copia de seguridad completa antes de comenzar la actualización. Asegúrese de realizar una copia de seguridad del repositorio, la instalación de la aplicación, el almacén de datos y las instancias de Mongo, si corresponde. Para obtener más información sobre cómo realizar copias de seguridad y restaurar una instancia de AEM, consulte [Backup y restauración](/help/sites-administering/backup-and-restore.md).

## Realizar copia de seguridad de cambios en /etc {#backup-changes-etc}

El proceso de actualización permite mantener y combinar el contenido y las configuraciones existentes desde las `/apps` y `/libs` rutas del repositorio. Para los cambios realizados en la ruta `/etc`, incluidas las configuraciones de Context Hub, a menudo es necesario volver a aplicar estos cambios después de la actualización. Aunque la actualización hará una copia de seguridad de los cambios que no pueda combinar en `/var`, recomendamos realizar una copia de seguridad de estos cambios manualmente antes de comenzar la actualización.

## Generar el archivo quickstart.properties {#generate-quickstart-properties}

Al iniciar AEM desde el archivo jar, se generará un archivo `quickstart.properties` en `crx-quickstart/conf`. Si AEM se ha iniciado con la secuencia de comandos de inicio anteriormente, este archivo no estará presente y la actualización fallará. Asegúrese de comprobar la existencia de este archivo y reiniciar AEM desde el archivo jar si no está presente.

## Configurar la depuración del registro de auditoría y del flujo de trabajo {#configure-wf-audit-purging}

Las tareas `WorkflowPurgeTask` y `com.day.cq.audit.impl.AuditLogMaintenanceTask` requieren configuraciones OSGi independientes y no funcionarán sin ellas. Si se producen errores durante la ejecución de la tarea previa a la actualización, la razón más probable es que falten configuraciones. Por lo tanto, asegúrese de agregar configuraciones OSGi para estas tareas o de eliminarlas por completo de la lista de tareas de optimización previa a la actualización si no desea ejecutarlas. La documentación para configurar tareas de depuración de flujo de trabajo se encuentra en [Administración de instancias de flujo de trabajo](/help/sites-administering/workflows-administering.md) y la configuración de tarea de mantenimiento de registro de auditoría se encuentra en [Mantenimiento del registro de auditoría en AEM 6](/help/sites-administering/operations-audit-log.md).

Para depurar el flujo de trabajo y el registro de auditoría en CQ 5.6, así como el registro de auditoría que se depura en AEM 6.0, consulte [Depurar los nodos de auditoría y del flujo de trabajo](https://helpx.adobe.com/experience-manager/kb/howtopurgewf.html).

## Instalar, configurar y ejecutar las Tareas previas a la actualización {#install-configure-run-pre-upgrade-tasks}

Debido al nivel de personalización que AEM permite, los entornos no suelen seguir una forma uniforme de realizar actualizaciones. Esto dificulta la creación de un procedimiento estandarizado para las actualizaciones.

En versiones anteriores, también resultaba difícil AEM actualizaciones que se detenían o que no se habían reanudado de forma segura. Esto daba lugar a situaciones en las que era necesario reiniciar el procedimiento completo de actualización o en las que se realizaban actualizaciones defectuosas sin activar ninguna advertencia.

Para solucionar estos problemas, Adobe ha añadido varias mejoras al proceso de actualización, lo que lo hace más flexible y fácil de usar. Las tareas de mantenimiento previas a la actualización que antes debían realizarse manualmente se están optimizando y automatizando. Además, se han agregado informes posteriores a la actualización para que el proceso pueda analizarse a fondo con la esperanza de encontrar cualquier problema más fácilmente.

Las tareas de mantenimiento previas a la actualización se distribuyen actualmente en varias interfaces que se realizan de forma manual o parcial. La optimización de mantenimiento previa a la actualización introducida en la AEM 6.3 permite activar estas tareas de forma unificada y poder inspeccionar sus resultados según la demanda.

Todas las tareas incluidas en el paso de optimización previo a la actualización son compatibles con todas las versiones a partir de AEM 6.0.

### Cómo configurarlo {#how-to-set-it-up}

En AEM 6.3 y posteriores, las tareas de optimización de mantenimiento previas a la actualización se incluyen en el tarro de inicio rápido. Si está actualizando desde una versión anterior de AEM 6, estarán disponibles a través de paquetes separados que puede descargar desde el Administrador de paquetes.

Puede encontrar los paquetes en estas ubicaciones:

* [Para actualizar desde AEM 6.0](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq600/product/pre-upgrade-tasks-content-cq60)

* [Para actualizar desde AEM 6.1](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq610/product/pre-upgrade-tasks-content-cq61)

* [Para actualizar desde AEM 6.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/product/pre-upgrade-tasks-content-cq62)

### Cómo usarla {#how-to-use-it}

El componente OSGI `PreUpgradeTasksMBean` viene preconfigurado con una lista de tareas de mantenimiento previas a la actualización que se pueden ejecutar de una vez. Puede configurar las tareas siguiendo el procedimiento siguiente:

1. Vaya a la consola web navegando a *https://serveraddress:serverport/system/console/configMgr*

1. Busque &quot;**preupgradeTasks**&quot; y, a continuación, haga clic en el primer componente coincidente. El nombre completo del componente es `com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`

1. Modifique la lista de tareas de mantenimiento que deben ejecutarse como se muestra a continuación:

   ![1487758925984](assets/1487758925984.png)

La lista de tarea varía según el modo de ejecución que se esté utilizando para inicio de la instancia. A continuación se muestra una descripción del modo de ejecución para el que está diseñada cada tarea de mantenimiento.

<table>
 <tbody>
  <tr>
   <td><strong>Tarea</strong></td>
   <td><strong>Modo de ejecución</strong></td>
   <td><strong>Notas</strong></td>
  </tr>
  <tr>
   <td><code>TarIndexMergeTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>DataStoreGarbageCollectionTask</code></td>
   <td>crx2</td>
   <td>Se ejecutará mark y sweep. Para los almacenes de datos compartidos, elimine este paso y ejecute<br /> de forma manual o adecuada para preparar las instancias antes de la ejecución.</td>
  </tr>
  <tr>
   <td><code>ConsistencyCheckTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>WorkflowPurgeTask</code></td>
   <td>crx2/crx3</td>
   <td>Debe configurar el OSGi de configuración de depuración de flujo de trabajo de granito de Adobe antes de ejecutar.</td>
  </tr>
  <tr>
   <td><code>GenerateBundlesListFileTask</code></td>
   <td>crx2/crx3</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>RevisionCleanupTask</code></td>
   <td>crx3</td>
   <td>Para las instancias de TarMK en AEM 6.0 a 6.2, ejecute manualmente la limpieza de revisión sin conexión en su lugar.</td>
  </tr>
  <tr>
   <td><code>com.day.cq.audit.impl.AuditLogMaintenanceTask</code></td>
   <td>crx3</td>
   <td>Debe configurar OSGi Planificador de depuración de registros de auditoría antes de ejecutar.</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>`DataStoreGarbageCollectionTask` llama a una operación de recolección de elementos no utilizados del almacén de datos con la fase de marca y barrido si se utiliza. Para implementaciones que utilizan un almacén de datos compartido, asegúrese de volver a configurarlo o bien de preparar la instancia para evitar la eliminación de elementos a los que hace referencia otra instancia. Esto puede requerir ejecutar la fase de marca manualmente en todas las instancias antes de activar esta tarea previa a la actualización.

### Configuración predeterminada de las comprobaciones de estado previas a la actualización {#default-configuration-of-the-pre-upgrade-health-checks}

El componente OSGI `PreUpgradeTasksMBeanImpl` viene preconfigurado con una lista de etiquetas de comprobación de estado previas a la actualización para ejecutarse cuando se llama al método `runAllPreUpgradeHealthChecks`:

* **sistema** : la etiqueta utilizada por las comprobaciones de mantenimiento de granito

* **preactualización** : es una etiqueta personalizada que se puede agregar a todas las comprobaciones de estado que se pueden configurar para que se ejecuten antes de una actualización

La lista es editable. Puede utilizar los botones más **(+)** y menos **(-)** además de las etiquetas para agregar más etiquetas personalizadas o quitar las predeterminadas.

**Métodos MBean**

Se puede acceder a la funcionalidad de granos administrados mediante la [Consola JMX](/help/sites-administering/jmx-console.md).

Puede acceder a los MBeans mediante:

1. Ir a la consola de JMX en *https://serveraddress:serverport/system/console/jmx*
1. Busque **PreUpgradeTasks** y haga clic en el resultado

1. Seleccione cualquier método en la sección **Operaciones** y seleccione **Invocar** en la siguiente ventana.

A continuación se muestra una lista de todos los métodos disponibles que `PreUpgradeTasksMBeanImpl` expone:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre del método</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeTasksNames()</code></td>
   <td>INFORMACIÓN</td>
   <td>Muestra la lista de los nombres de tareas de mantenimiento previas a la actualización disponibles.</td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeHealthChecksTagNames()</code></td>
   <td>INFORMACIÓN</td>
   <td>Muestra la lista de los nombres de las etiquetas de comprobación de estado previas a la actualización.</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeTasks()</code></td>
   <td>ACCIÓN</td>
   <td>Ejecuta todas las tareas de mantenimiento previas a la actualización en la lista.</td>
  </tr>
  <tr>
   <td><code>runPreUpgradeTask(preUpgradeTaskName)</code></td>
   <td>ACCIÓN</td>
   <td>Ejecuta la tarea de mantenimiento previa a la actualización con el nombre proporcionado como parámetro.</td>
  </tr>
  <tr>
   <td><code>isRunAllPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>Comprueba si la tarea <code>runAllPreUpgradeTasksmaintenance</code> se está ejecutando actualmente.</td>
  </tr>
  <tr>
   <td><code>getAnyPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>Comprueba si hay alguna tarea de mantenimiento previa a la actualización en ejecución y<br /> devuelve una matriz que contiene los nombres de tareas en ejecución.</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunTime(preUpgradeTaskName)</code></td>
   <td>ACCIÓN</td>
   <td>Muestra el tiempo de ejecución exacto de la tarea de mantenimiento previa a la actualización con el nombre dado como parámetro.</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunState(preUpgradeTaskName)</code></td>
   <td>ACCIÓN</td>
   <td>Muestra el último estado de ejecución de la tarea de mantenimiento previa a la actualización con el nombre dado como parámetro.</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeHealthChecks(shutDownOnSuccess)</code></td>
   <td>ACCIÓN</td>
   <td><p>Ejecuta todas las comprobaciones de estado previas a la actualización y guarda su estado en un archivo denominado <code>preUpgradeHCStatus.properties</code> que se encuentra en la ruta de inicio de sling. Si el parámetro <code>shutDownOnSuccess</code> está establecido en <code>true</code>, la instancia de AEM se cerrará, pero sólo si todas las comprobaciones de estado previas a la actualización tienen un estado correcto.</p> <p>El archivo de propiedades se utilizará como condición previa para cualquier actualización futura<br /> y el proceso de actualización se detendrá si falla la ejecución de la comprobación de estado previa a la actualización<br />. Si desea ignorar el resultado de las comprobaciones de estado previas a la actualización<br /> e iniciar la actualización de todos modos, puede eliminar el archivo.</p> </td>
  </tr>
  <tr>
   <td><code>detectUsageOfUnavailableAPI(aemVersion)</code></td>
   <td>ACCIÓN</td>
   <td>Lista todos los paquetes importados que ya no se satisfarán cuando<br /> se actualice a la versión de AEM especificada. La versión AEM destinatario debe estar<br /> dada como parámetro.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Los métodos MBean se pueden invocar mediante:
>
>* La consola JMX
>* Cualquier aplicación externa que se conecte a JMX
>* cURL

>



## Deshabilitar los módulos de inicio de sesión personalizados {#disable-custom-login-modules}

>[!NOTE]
>
>Este paso solo es necesario si está actualizando desde una versión AEM 5. Se puede omitir por completo para actualizaciones de versiones anteriores de AEM 6.

El modo en que se configuran los `LoginModules` personalizados para la autenticación a nivel de repositorio ha cambiado fundamentalmente en Apache Oak.

En AEM versiones que usaban la configuración CRX2 se ubicaban en el archivo `repository.xml`, mientras que a partir de AEM 6 se realizaba en el servicio de fábrica de configuración Apache Felix JAAS a través de la consola web.

Por lo tanto, cualquier configuración existente tendrá que deshabilitarse y volverse a crear para Apache Oak después de la actualización.

Para deshabilitar los módulos personalizados definidos en la configuración JAAS de `repository.xml`, debe modificar la configuración para utilizar el `LoginModule` predeterminado, como en este ejemplo:

```xml
<Security >
             ....
          <!--
                 Use LoginModule authenticating against repository itself
                 -->
                 <LoginModule class = "com.day.crx.core.CRXLoginModule" >
                     <param name = "anonymousId" value = "anonymous" />
                     <param name = "adminId" value ="admin" />
                     <param name = "disableNTLMAuth" value = "true" />
                     <param name = "tokenExpiration" value = "43200000" />
                     <!-- param name="trust_credentials_attribute" value="d5b9167e95dad6e7d3b5d6fa8df48af8"/
                -->
                 </LoginModule >
         </ Security>
```

>[!NOTE]
>
>Para obtener más información, consulte [Autenticación con el módulo de inicio de sesión externo](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html).
>
>Para ver un ejemplo de la configuración `LoginModule` en AEM 6, consulte [Configuración de LDAP con AEM 6](/help/sites-administering/ldap-config.md).

## Quitar Actualizaciones Del Directorio /install {#remove-updates-install-directory}

>[!NOTE]
>
>Sólo elimine paquetes del directorio crx-quickstart/install DESPUÉS de apagar la instancia de AEM. Este será uno de los últimos pasos antes de iniciar el procedimiento de actualización in situ.

Elimine todos los paquetes de servicios, paquetes de funciones o revisiones que se hayan implementado a través del directorio `crx-quickstart/install` en el sistema de archivos local. Esto evitará la instalación involuntaria de revisiones y Service Packs antiguos sobre la nueva versión de AEM una vez finalizada la actualización.

## Detener cualquier instancia en espera en frío {#stop-tarmk-coldstandby-instance}

Si utiliza TarMK en espera fría, detenga las instancias en espera en frío. Esto garantizará una manera eficiente de volver a conectarse en caso de problemas en la actualización. Una vez que la actualización se haya completado correctamente, las instancias en espera en frío deberán reconstruirse a partir de las instancias primarias actualizadas.

## Deshabilitar trabajos programados personalizados {#disable-custom-scheduled-jobs}

Deshabilite los trabajos programados de OSGi que estén incluidos en el código de la aplicación.

## Ejecutar limpieza de revisión sin conexión {#execute-offline-revision-cleanup}

>[!NOTE]
>
>Este paso solo es necesario para las instalaciones TarMK

Si utiliza TarMK, debe ejecutar la limpieza de revisión sin conexión antes de la actualización. Esto hará que el paso de migración del repositorio y las tareas de actualización posteriores se ejecuten mucho más rápido y ayudará a garantizar que la limpieza de revisión en línea se pueda ejecutar correctamente una vez completada la actualización. Para obtener información sobre cómo ejecutar la limpieza de revisión sin conexión, consulte [Realización de la limpieza de revisión sin conexión](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup).

## Ejecutar recolección de elementos no utilizados del almacén de datos {#execute-datastore-garbage-collection}

>[!NOTE]
>
>Este paso solo es necesario para instancias que ejecutan crx3

Después de ejecutar la limpieza de revisión en instancias de CRX3, debe ejecutar la recopilación de elementos no utilizados del almacén de datos para eliminar los blobs no referenciados del almacén de datos. Para obtener instrucciones, consulte la documentación sobre [Recopilación de elementos no utilizados del almacén de datos](/help/sites-administering/data-store-garbage-collection.md).

## Actualizar el Esquema de base de datos si es necesario {#upgrade-the-database-schema-if-needed}

Normalmente, la pila de Apache Oak subyacente que utiliza AEM persistencia se encargará de actualizar el esquema de la base de datos si es necesario.

Sin embargo, pueden surgir casos cuando el esquema no se puede actualizar automáticamente. Estos son entornos de alta seguridad donde la base de datos se ejecuta bajo un usuario con privilegios muy limitados. Si esto sucede, AEM seguirá usando el esquema antiguo.

Para evitar que esto ocurra, debe actualizar el esquema siguiendo el procedimiento siguiente:

1. Cierre la instancia de AEM que debe actualizarse.
1. Actualice el esquema de la base de datos. Consulte la documentación de su tipo de base de datos para ver cuál es la herramienta que necesita utilizar para conseguirlo.

   Para obtener más información sobre cómo Oak gestiona las actualizaciones de esquema, consulte [esta página en el sitio Web de Apache](https://jackrabbit.apache.org/oak/docs/nodestore/document/rdb-document-store.html#upgrade).

1. Continúe con la actualización de AEM.

## Eliminar usuarios que podrían obstaculizar la actualización {#delete-users-that-might-hinder-the-upgrade}

>[!NOTE]
>
>Esta tarea de mantenimiento previa a la actualización solo es necesaria si:
>
>* Está actualizando desde AEM versiones anteriores a AEM 6.3
>* Durante la actualización se produce cualquiera de los errores mencionados a continuación.

>



Hay casos excepcionales en los que los usuarios de servicios pueden terminar en versiones AEM anteriores etiquetadas incorrectamente como usuarios normales.

Si esto sucede, la actualización fallará con un mensaje como este:

```
ERROR [Apache Sling Repository Startup Thread] com.adobe.granite.repository.impl.SlingRepositoryManager Exception in a SlingRepositoryInitializer, SlingRepository service registration aborted
java.lang.RuntimeException: Unable to create service user [communities-utility-reader]:java.lang.RuntimeException: Existing user communities-utility-reader is not a service user.
```

Para solucionar este problema, asegúrese de hacer lo siguiente:

1. Desasociar la instancia del tráfico de producción
1. Cree una copia de seguridad de los usuarios que ocasionan el problema. Puede hacerlo a través del Administrador de paquetes. Para obtener más información, consulte [Cómo trabajar con paquetes.](/help/sites-administering/package-manager.md)
1. Elimine los usuarios que ocasionan el problema. A continuación se muestra una lista de los usuarios que podrían incluirse en esta categoría:

   1. `dynamic-media-replication`
   1. `communities-ugc-writer`
   1. `communities-utility-reader`
   1. `communities-user-admin`
   1. `oauthservice`
   1. `sling-scripting`

## Rotar archivos de registro {#rotate-log-files}

Se recomienda archivar los archivos de registro actuales antes de comenzar la actualización. Esto facilitará la supervisión y exploración de los archivos de registro durante y después de la actualización para identificar y resolver cualquier problema que pueda producirse.
