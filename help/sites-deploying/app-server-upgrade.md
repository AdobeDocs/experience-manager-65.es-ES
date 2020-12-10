---
title: Pasos de actualización para las instalaciones de Application Server
seo-title: Pasos de actualización para las instalaciones de Application Server
description: Obtenga información sobre cómo actualizar las instancias de AEM implementadas a través de los servidores de aplicaciones.
seo-description: Obtenga información sobre cómo actualizar las instancias de AEM implementadas a través de los servidores de aplicaciones.
uuid: e4020966-737c-40ea-bfaa-c63ab9a29cee
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 1876d8d6-bffa-4a1c-99c0-f6001acea825
docset: aem65
translation-type: tm+mt
source-git-commit: f696b1081f14ba379cde51a3542a5b1b5f9668e2
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---


# Pasos de actualización para las instalaciones del servidor de aplicaciones{#upgrade-steps-for-application-server-installations}

En esta sección se describe el procedimiento que debe seguirse para actualizar la AEM de las instalaciones de Application Server.

Todos los ejemplos de este procedimiento utilizan Tomcat como servidor de aplicaciones e implican que ya tiene implementada una versión de trabajo de AEM. El procedimiento tiene por objeto el documento de las actualizaciones realizadas desde **AEM versión 6.4 a 6.5**.

1. Primero, inicio TomCat. En la mayoría de los casos, puede hacerlo ejecutando la secuencia de comandos de inicio de inicio `./catalina.sh`, ejecutando este comando desde el terminal:

   ```shell
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. Si AEM 6.4 ya está implementado, compruebe que los paquetes funcionan correctamente accediendo a:

   ```shell
   https://<serveraddress:port>/cq/system/console/bundles
   ```

1. A continuación, anule la implementación de AEM 6.4. Esto se puede hacer desde el Administrador de aplicaciones de TomCat (`http://serveraddress:serverport/manager/html`)

1. Ahora, migre el repositorio utilizando la herramienta de migración crx2oak. Para ello, descargue la última versión de crx2oak de [esta ubicación](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak).

   ```shell
   SLING_HOME= $AEM-HOME/crx-quickstart java -Xmx4096m -XX:MaxPermSize=2048M -jar crx2oak.jar --load-profile segment-fds
   ```

1. Elimine las propiedades necesarias del archivo sling.properties haciendo lo siguiente:

   1. Abra el archivo ubicado en `crx-quickstart/launchpad/sling.properties`
   1. Texto del paso Elimine las siguientes propiedades y guarde el archivo:

      1. `sling.installer.dir`

      1. `felix.cm.dir`

      1. `granite.product.version`

      1. `org.osgi.framework.system.packages`

      1. `osgi-core-packages`

      1. `osgi-compendium-services`

      1. `jre-*`

      1. `sling.run.mode.install.options`

1. Quite los archivos y las carpetas que ya no sean necesarios. Los elementos que debe eliminar específicamente son:

   * La **carpeta launchpad/startup**. Puede eliminarlo ejecutando el siguiente comando en el terminal: `rm -rf crx-quickstart/launchpad/startup`

   * El **archivo base.jar**: `find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * El archivo **BootstrapCommandFile_timestamp.txt**: `rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

   * Elimine **sling.options.file** ejecutando: `find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf`

1. Ahora, cree el almacén de nodos y el almacén de datos que se utilizarán con AEM 6.5. Para ello, cree dos archivos con los nombres siguientes en `crx-quickstart\install`:

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`
   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   Estos dos archivos configurarán AEM para utilizar un almacén de nodos TarMK y un almacén de datos File.

1. Edite los archivos de configuración para que estén listos para su uso. Más específicamente:

   * Añada la siguiente línea a `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`:

      ```customBlobStore=true```

   * A continuación, agregue las siguientes líneas a `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`:

      ```
      path=./crx-quickstart/repository/datastore
      minRecordLength=4096
      ```

1. Ahora debe cambiar los modos de ejecución en el archivo de guerra AEM 6.5. Para hacerlo, primero cree una carpeta temporal que albergue la guerra de AEM 6.5. El nombre de la carpeta en este ejemplo será `temp`. Una vez copiado el archivo de guerra, extraiga su contenido ejecutándose desde la carpeta temp:

   ```
   jar xvf aem-quickstart-6.5.0.war
   ```

1. Una vez extraído el contenido, vaya a la carpeta **WEB-INF** y edite el archivo web.xml para cambiar los modos de ejecución. Para encontrar la ubicación donde se han establecido en XML, busque la cadena `sling.run.modes`. Una vez que lo encuentre, cambie los modos de ejecución en la siguiente línea de código, que de forma predeterminada se establece en author:

   ```bash
   <param-value >author</param-value>
   ```

1. Cambie el valor de autor anterior y defina los modos de ejecución en: `author,crx3,crx3tar`. El bloque final de código debería tener este aspecto:

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. Volver a crear el frasco con el contenido modificado:

   ```bash
   jar cvf aem65.war
   ```

1. Finalmente, despliegue el nuevo archivo de guerra en TomCat.
