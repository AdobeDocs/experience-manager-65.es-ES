---
title: Tareas de mantenimiento previas a la actualización
description: AEM Obtenga información acerca de las tareas previas a la actualización recomendadas para los.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
exl-id: 37d4aee4-15eb-41ab-ad71-dfbd5c7910f8
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '2014'
ht-degree: 0%

---

# Tareas de mantenimiento previas a la actualización{#pre-upgrade-maintenance-tasks}

Antes de comenzar la actualización, es importante realizar estas tareas de mantenimiento para asegurarse de que el sistema está listo y se puede revertir en caso de que se produzcan problemas:

* [Garantizar suficiente espacio en disco](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [AEM Totalmente de nuevo hacia arriba](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [Realizar copia de seguridad de cambios en /etc](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#backup-changes-etc)
* [Generar el archivo quickstart.properties](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [Configurar depuración de flujo de trabajo y registro de auditoría](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [Instalar, configurar y ejecutar las tareas previas a la actualización](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [Deshabilitar módulos de inicio de sesión personalizados](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-login-modules)
* [Quitar Actualizaciones Del Directorio /install](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [Detener Cualquier Instancia De Espera En Frío](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [Deshabilitar trabajos programados personalizados](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [Ejecutar limpieza de revisión sin conexión](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [Ejecutar recolección de basura del almacén de datos](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [Actualizar el esquema de base de datos si es necesario](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [Eliminar usuarios que puedan obstaculizar la actualización](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#delete-users-that-might-hinder-the-upgrade)

* [Rotar archivos de registro](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## Garantizar suficiente espacio en disco {#ensure-sufficient-disk-space}

Al ejecutar la actualización, además de las actividades de actualización de contenido y código, se debe realizar una migración del repositorio. La migración crea una copia del repositorio en el nuevo formato de Segment TAR. Como resultado, necesita suficiente espacio en disco para conservar una segunda versión, potencialmente más grande, del repositorio.

## AEM Totalmente de nuevo hacia arriba {#fully-back-up-aem}

AEM Se debe realizar una copia de seguridad completa de los datos antes de iniciar la actualización. Asegúrese de realizar una copia de seguridad del repositorio, la instalación de la aplicación, el almacén de datos y las instancias de Mongo si corresponde. AEM Para obtener más información acerca de cómo hacer copias de seguridad y restaurar una instancia de, consulte [Copia de seguridad y restauración](/help/sites-administering/backup-and-restore.md).

## Realizar copia de seguridad de cambios en /etc {#backup-changes-etc}

El proceso de actualización hace un buen trabajo al mantener y combinar el contenido y las configuraciones existentes de las rutas de acceso `/apps` y `/libs` en el repositorio. Para los cambios realizados en la ruta de acceso `/etc`, incluidas las configuraciones de Context Hub, a menudo es necesario volver a aplicar estos cambios después de la actualización. Mientras la actualización realiza una copia de seguridad de los cambios que no se pueden combinar en `/var`, Adobe recomienda que realice una copia de seguridad manual de estos cambios antes de comenzar la actualización.

## Generar el archivo quickstart.properties {#generate-quickstart-properties}

AEM Al iniciar el proceso desde el archivo jar, se genera un archivo `quickstart.properties` en `crx-quickstart/conf`. AEM Si solo se ha iniciado con la secuencia de comandos de inicio en el pasado, este archivo no está presente y la actualización falla. AEM Asegúrese de comprobar la existencia de este archivo y reinicie el proceso desde el archivo jar si no está presente.

## Configurar depuración de flujo de trabajo y registro de auditoría {#configure-wf-audit-purging}

Las tareas `WorkflowPurgeTask` y `com.day.cq.audit.impl.AuditLogMaintenanceTask` requieren configuraciones OSGi independientes y no pueden funcionar sin ellas. Si fallan durante la ejecución de la tarea previa a la actualización, la razón más probable es que falten configuraciones. Por lo tanto, asegúrese de agregar configuraciones de OSGi para estas tareas o eliminarlas por completo de la lista de tareas de optimización previas a la actualización si no desea ejecutarlas. AEM Encontrará documentación para configurar las tareas de depuración del flujo de trabajo en [Administración de instancias del flujo de trabajo](/help/sites-administering/workflows-administering.md) y la configuración de tareas de mantenimiento del registro de auditoría en [Mantenimiento del registro de auditoría en el 6](/help/sites-administering/operations-audit-log.md).

AEM Para la depuración de registros de auditoría y flujo de trabajo en CQ 5.6 y depuración de registros de auditoría en 6.0, consulte [Purgar flujo de trabajo y nodos de auditoría](https://helpx.adobe.com/experience-manager/kb/howtopurgewf.html).

## Instalar, configurar y ejecutar las tareas previas a la actualización {#install-configure-run-pre-upgrade-tasks}

AEM Debido al nivel de personalización que permite el uso de los recursos, los entornos no suelen adherirse a una forma uniforme de realizar las actualizaciones. Como tal, hace que la creación de un procedimiento estandarizado para las actualizaciones sea un proceso difícil.

AEM En versiones anteriores, también resultaba difícil para las actualizaciones de la aplicación que se detenían o que no se reanudaban de forma segura. Este problema llevaba a situaciones en las que era necesario reiniciar el procedimiento de actualización completo o en las que se realizaban actualizaciones defectuosas sin activar ninguna advertencia.

Para solucionar estos problemas, Adobe ha añadido varias mejoras al proceso de actualización, lo que lo hace más resistente y fácil de usar. Las tareas de mantenimiento previas a la actualización que antes se tenían que realizar manualmente se están optimizando y automatizando. Además, se han agregado informes posteriores a la actualización para que el proceso pueda analizarse a fondo con la esperanza de que cualquier problema se encuentre con mayor facilidad.

Las tareas de mantenimiento previas a la actualización se distribuyen actualmente entre varias interfaces que se realizan parcial o totalmente de forma manual. AEM La optimización del mantenimiento previo a la actualización incluida en la versión 6.3 de la versión de permite contar con una forma unificada de déclencheur de estas tareas y de poder inspeccionar sus resultados bajo demanda.

AEM Todas las tareas incluidas en el paso de optimización previo a la actualización son compatibles con todas las versiones a partir de la versión 6.0 de la aplicación de forma independiente.

### Cómo configurarlo. {#how-to-set-it-up}

AEM En la versión 6.3 y posteriores, las tareas de optimización de mantenimiento previas a la actualización se incluyen en el JAR de inicio rápido.

<!-- URLs below are all 404s. This content should probably be removed because it is entirely obsolete.

If you are upgrading from an older version of AEM 6, they are made available through separate packages that you can download from the Package Manager.

You can find the packages at these locations:

* [For upgrading from AEM 6.0](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq600/product/pre-upgrade-tasks-content-cq60)

* [For upgrading from AEM 6.1](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq610/product/pre-upgrade-tasks-content-cq61)

* [For upgrading from AEM 6.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/product/pre-upgrade-tasks-content-cq62) -->

### Cómo se usa {#how-to-use-it}

El componente OSGI `PreUpgradeTasksMBean` viene preconfigurado con una lista de tareas de mantenimiento previas a la actualización que se pueden ejecutar todas a la vez. Puede configurar las tareas siguiendo el siguiente procedimiento:

1. Vaya a la consola web explorando *https://serveraddress:serverport/system/console/configMgr*

1. Busque &quot;**preupgradetasks**&quot; y, a continuación, haga clic en el primer componente que coincida. El nombre completo del componente es `com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`

1. Modifique la lista de tareas de mantenimiento que deben ejecutarse como se muestra a continuación:

   ![1487758925984](assets/1487758925984.png)

La lista de tareas difiere según el modo de ejecución que se esté utilizando para iniciar la instancia. A continuación se describe el modo de ejecución para el que está diseñada cada tarea de mantenimiento.

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
   <td>Marca y barre. Para los almacenes de datos compartidos, quite este paso y ejecute <br /> manual o correctamente para preparar las instancias antes de ejecutarlas.</td>
  </tr>
  <tr>
   <td><code>ConsistencyCheckTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>WorkflowPurgeTask</code></td>
   <td>crx2/crx3</td>
   <td>Debe configurar la configuración OSGi de depuración del flujo de trabajo de Granite de Adobe antes de ejecutar.</td>
  </tr>
  <tr>
   <td><code>GenerateBundlesListFileTask</code></td>
   <td>crx2/crx3</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>RevisionCleanupTask</code></td>
   <td>crx3</td>
   <td>AEM Para las instancias de TarMK en la versión 6.0 a 6.2 de, ejecute manualmente la Limpieza de revisión sin conexión en su lugar.</td>
  </tr>
  <tr>
   <td><code>com.day.cq.audit.impl.AuditLogMaintenanceTask</code></td>
   <td>crx3</td>
   <td>Debe configurar el programador de purga de registros de auditoría OSGi antes de ejecutar.</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>El `DataStoreGarbageCollectionTask` llama a una operación de recolección de elementos no utilizados del almacén de datos con la fase de marcado y barrido si se utiliza. Para las implementaciones que utilizan un almacén de datos compartido, asegúrese de volver a configurarlo correctamente o preparar la instancia para evitar la eliminación de los elementos a los que hace referencia otra instancia. Este proceso puede requerir la ejecución manual de la fase de marcado en todas las instancias antes de activar esta tarea previa a la actualización.

### Configuración predeterminada de las comprobaciones de estado previas a la actualización {#default-configuration-of-the-pre-upgrade-health-checks}

El componente OSGI `PreUpgradeTasksMBeanImpl` viene preconfigurado con una lista de etiquetas de comprobación de estado previas a la actualización para ejecutarse cuando se llame al método `runAllPreUpgradeHealthChecks`:

* **system**: la etiqueta utilizada por las comprobaciones de estado de mantenimiento de granite

* **actualización previa**: una etiqueta personalizada que se podría agregar a todas las comprobaciones de estado que se pueden configurar para que se ejecuten antes de una actualización

La lista es editable. Puede usar los botones más **(+)** y menos **(-)** además de las etiquetas para agregar más etiquetas personalizadas o quitar las predeterminadas.

**Métodos MBean**

Se puede acceder a la funcionalidad de bean administrada mediante la [consola JMX](/help/sites-administering/jmx-console.md).

Puede acceder a los MBeans mediante las siguientes opciones:

1. Ir a la consola JMX en *https://serveraddress:serverport/system/console/jmx*
1. Busque **PreUpgradeTasks** y haga clic en el resultado

1. Seleccione cualquier método de la sección **Operations** y seleccione **Invoke** en la siguiente ventana.

A continuación se muestra una lista de todos los métodos disponibles que expone `PreUpgradeTasksMBeanImpl`:

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
   <td>Muestra la lista de nombres de tareas de mantenimiento previas a la actualización disponibles.</td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeHealthChecksTagNames()</code></td>
   <td>INFORMACIÓN</td>
   <td>Muestra la lista de nombres de etiquetas de comprobaciones de estado previas a la actualización.</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeTasks()</code></td>
   <td>ACCIÓN</td>
   <td>Ejecuta todas las tareas de mantenimiento previas a la actualización de la lista.</td>
  </tr>
  <tr>
   <td><code>runPreUpgradeTask(preUpgradeTaskName)</code></td>
   <td>ACCIÓN</td>
   <td>Ejecuta la tarea de mantenimiento previa a la actualización con el nombre dado como parámetro.</td>
  </tr>
  <tr>
   <td><code>isRunAllPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>Comprueba si la tarea <code>runAllPreUpgradeTasksmaintenance</code> se está ejecutando.</td>
  </tr>
  <tr>
   <td><code>getAnyPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>Comprueba si se está ejecutando alguna tarea de mantenimiento anterior a la actualización y <br /> devuelve una matriz que contiene los nombres de las tareas en ejecución.</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunTime(preUpgradeTaskName)</code></td>
   <td>ACCIÓN</td>
   <td>Muestra el tiempo de ejecución exacto de la tarea de mantenimiento anterior a la actualización con el nombre dado como parámetro.</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunState(preUpgradeTaskName)</code></td>
   <td>ACCIÓN</td>
   <td>Muestra el último estado de ejecución de la tarea de mantenimiento previa a la actualización con el nombre dado como parámetro.</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeHealthChecks(shutDownOnSuccess)</code></td>
   <td>ACCIÓN</td>
   <td><p>Ejecuta todas las comprobaciones de estado previas a la actualización y guarda su estado en un archivo denominado <code>preUpgradeHCStatus.properties</code> que se encuentra en la ruta de acceso principal de sling. AEM Si el parámetro <code>shutDownOnSuccess</code> se establece en <code>true</code>, la instancia de la se cerrará, pero solo si todas las comprobaciones de estado anteriores a la actualización tienen un estado correcto.</p> <p>El archivo de propiedades se usa como condición previa para cualquier actualización futura <br /> y el proceso de actualización se detiene si la ejecución de la comprobación de estado previa a la actualización <br /> falla. Si desea omitir el resultado de las comprobaciones de estado de <br /> anteriores a la actualización e iniciar la actualización de todos modos, puede eliminar el archivo.</p> </td>
  </tr>
  <tr>
   <td><code>detectUsageOfUnavailableAPI(aemVersion)</code></td>
   <td>ACCIÓN</td>
   <td>AEM Enumera todos los paquetes importados que ya no se satisfacen cuando se actualiza <br /> a la versión especificada de la versión de la. AEM La versión del destino de la entrega debe ser <br /> dada como parámetro.</td>
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

## Deshabilitar módulos de inicio de sesión personalizados {#disable-custom-login-modules}

>[!NOTE]
>
>AEM Este paso solo es necesario si actualiza desde una versión de 5. AEM Se puede omitir por completo para las actualizaciones de versiones anteriores de la versión.

La forma en que se configuraron los `LoginModules` personalizados para la autenticación en el nivel de repositorio ha cambiado fundamentalmente en Apache Oak.

AEM En versiones de la aplicación que utilizaban la configuración de CRXAEM 2 se colocaba en el archivo `repository.xml`, mientras que a partir del 6 de mayo se realiza en el servicio de fábrica de configuración de Apache Felix JAAS a través de la consola web.

Por lo tanto, cualquier configuración existente tendrá que deshabilitarse y volver a crearse para Apache Oak después de la actualización.

Para deshabilitar los módulos personalizados definidos en la configuración de JAAS de `repository.xml`, debe editar la configuración para utilizar el valor predeterminado `LoginModule`, como en el siguiente ejemplo:

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
>AEM AEM Para ver un ejemplo de la configuración de `LoginModule` en el 6, consulte [Configuración de LDAP con la configuración de 60000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000](/help/sites-administering/ldap-config.md)

## Quitar Actualizaciones Del Directorio /install {#remove-updates-install-directory}

>[!NOTE]
>
>AEM Solo elimine paquetes del directorio crx-quickstart/install DESPUÉS de cerrar la instancia de la. Este paso es uno de los últimos antes de iniciar el procedimiento de actualización in situ.

Quite los Service Packs, paquetes de características o revisiones que se hayan implementado a través del directorio `crx-quickstart/install` en el sistema de archivos local. AEM Al hacerlo, se evita la instalación involuntaria de revisiones antiguas y Service Packs, además de la nueva versión de la aplicación, una vez completada la actualización.

## Detener Cualquier Instancia De Espera En Frío {#stop-tarmk-coldstandby-instance}

Si utiliza TarMK modo de espera en frío, detenga cualquier instancia de espera en frío. Al hacerlo, se garantiza una forma eficaz de volver a estar en línea si hay problemas en la actualización. Una vez que la actualización se haya completado correctamente, las instancias de espera en frío deben volver a crearse a partir de las instancias principales actualizadas.

## Deshabilitar trabajos programados personalizados {#disable-custom-scheduled-jobs}

Deshabilite los trabajos programados de OSGi que se incluyan en el código de la aplicación.

## Ejecutar limpieza de revisión sin conexión {#execute-offline-revision-cleanup}

>[!NOTE]
>
>Este paso solo es necesario para instalaciones de TarMK

Si utiliza TarMK, debe ejecutar Offline Revision Cleanup antes de actualizar. Al hacerlo, el paso de migración del repositorio y las tareas de actualización subsiguientes se ejecutan mucho más rápido y ayuda a garantizar que Limpieza de revisiones en línea se pueda ejecutar correctamente una vez completada la actualización. Para obtener información sobre cómo ejecutar la limpieza de revisión sin conexión, consulte [Realización de la limpieza de revisión sin conexión](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup).

## Ejecutar recolección de basura del almacén de datos {#execute-datastore-garbage-collection}

>[!NOTE]
>
>Este paso solo es necesario para instancias que ejecuten crx3

Después de ejecutar la limpieza de revisión en instancias de CRX3, debe ejecutar la recolección de basura del almacén de datos para eliminar los blobs a los que no se hace referencia en el almacén de datos. Para obtener instrucciones, consulte la documentación de [Recopilación de elementos no utilizados del almacén de datos](/help/sites-administering/data-store-garbage-collection.md).

## Actualizar el esquema de base de datos si es necesario {#upgrade-the-database-schema-if-needed}

Normalmente, la pila subyacente de Apache Oak AEM que utiliza el usuario para la persistencia se encarga de actualizar el esquema de la base de datos, si es necesario.

Sin embargo, pueden surgir casos en los que el esquema no se pueda actualizar automáticamente. Estos casos son principalmente entornos de alta seguridad en los que la base de datos se está ejecutando bajo un usuario con privilegios limitados. AEM Si se produce una situación de este tipo, el usuario continúa utilizando el esquema antiguo

Para evitar que se produzca un escenario de este tipo, actualice el esquema haciendo lo siguiente:

1. AEM Cierre la instancia de la que debe actualizarse.
1. Actualice el esquema de la base de datos. Consulte la documentación del tipo de base de datos para ver qué herramientas son necesarias para lograr el resultado.

   Para obtener más información sobre cómo administra Oak las actualizaciones de esquema, consulte [esta página en el sitio web de Apache](https://jackrabbit.apache.org/oak/docs/nodestore/document/rdb-document-store.html#upgrade).

1. AEM Continúe con la actualización de la versión de.

## Eliminar usuarios que puedan obstaculizar la actualización {#delete-users-that-might-hinder-the-upgrade}

>[!NOTE]
>
>Esta tarea de mantenimiento previa a la actualización solo es necesaria si:
>
>* AEM AEM Está actualizando desde versiones anteriores a la versión 6.3 de
>* Durante la actualización, se produce cualquiera de los errores que se mencionan a continuación.
>

AEM Existen casos excepcionales en los que los usuarios del servicio pueden terminar en una versión anterior del servicio etiquetada incorrectamente como usuarios habituales.

Si se produce una situación de este tipo, la actualización falla con un mensaje como el siguiente:

```
ERROR [Apache Sling Repository Startup Thread] com.adobe.granite.repository.impl.SlingRepositoryManager Exception in a SlingRepositoryInitializer, SlingRepository service registration aborted
java.lang.RuntimeException: Unable to create service user [communities-utility-reader]:java.lang.RuntimeException: Existing user communities-utility-reader is not a service user.
```

Para solucionar este problema, asegúrese de hacer lo siguiente:

1. Desasociar la instancia del tráfico de producción
1. Cree una copia de seguridad de uno o más usuarios que causan el problema. Puede realizar esta tarea mediante el Administrador de paquetes. Para obtener más información, vea [Cómo trabajar con paquetes.](/help/sites-administering/package-manager.md)
1. Elimine uno o varios usuarios que causan el problema. A continuación se muestra una lista de los usuarios que pueden pertenecer a esta categoría:

   1. `dynamic-media-replication`
   1. `communities-ugc-writer`
   1. `communities-utility-reader`
   1. `communities-user-admin`
   1. `oauthservice`
   1. `sling-scripting`

## Rotar archivos de registro {#rotate-log-files}

El Adobe recomienda archivar los archivos de registro actuales antes de comenzar la actualización. Al hacerlo, resulta más fácil supervisar y analizar los archivos de registro durante y después de la actualización para identificar y resolver los problemas que se puedan producir.
