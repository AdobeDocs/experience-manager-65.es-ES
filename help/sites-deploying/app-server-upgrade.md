---
title: Pasos de actualización para instalaciones de Application Server
description: AEM Obtenga información sobre cómo actualizar las instancias de los recursos implementados a través de los servidores de aplicaciones.
feature: Upgrading
exl-id: 86dd10ae-7f16-40c8-84b6-91ff2973a523
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# Pasos de actualización para instalaciones de Application Server{#upgrade-steps-for-application-server-installations}

AEM En esta sección se describe el procedimiento que debe seguirse para actualizar las instalaciones del servidor de aplicaciones en el servidor de aplicaciones de forma que se puedan actualizar los datos de la instalación de un servidor de aplicaciones.

AEM Todos los ejemplos de este procedimiento utilizan Tomcat como servidor de aplicaciones e implican que ya tiene implementada una versión de trabajo de la aplicación de. El procedimiento está diseñado para documentar las actualizaciones realizadas desde **AEM Versión de 6.4 a 6.5**.

1. Primero, inicia TomCat. En la mayoría de los casos, puede hacerlo ejecutando la variable `./catalina.sh` inicie el script de inicio ejecutando este comando desde el terminal:

   ```shell
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. AEM Si ya se ha implementado la versión 6.4 de, compruebe que los paquetes funcionan correctamente accediendo a:

   ```shell
   https://<serveraddress:port>/cq/system/console/bundles
   ```

1. AEM A continuación, anule la implementación de 6.4. Esto se puede hacer desde el Administrador de aplicaciones de TomCat (`http://serveraddress:serverport/manager/html`)

1. Ahora, migre el repositorio con la herramienta de migración crx2oak. Para ello, descargue la versión más reciente de crx2oak desde [esta ubicación](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/).

   ```shell
   SLING_HOME= $AEM-HOME/crx-quickstart java -Xmx4096m -jar crx2oak.jar --load-profile segment-fds
   ```

1. Elimine las propiedades necesarias en el archivo sling.properties haciendo lo siguiente:

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

1. Elimine los archivos y carpetas que ya no sean necesarios. Los elementos que debe eliminar específicamente son los siguientes:

   * El **carpeta launchpad/startup**. Puede eliminarlo ejecutando el siguiente comando en el terminal: `rm -rf crx-quickstart/launchpad/startup`

   * El **archivo base.jar**: `find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * El **Archivo BootstrapCommandFile_timestamp.txt**: `rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

   * Eliminar **sling.options.file** ejecutando: `find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf`

1. AEM Ahora, cree el almacén de nodos y el almacén de datos que se utiliza con la versión 6.5 de. Para ello, cree dos archivos con los siguientes nombres en `crx-quickstart\install`:

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`
   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   AEM Estos dos archivos configurarán el uso de un almacén de nodos TarMK y un almacén de datos de archivos para que los usuarios puedan usar de forma más sencilla.

1. Edite los archivos de configuración para que estén listos para usarlos. Más concretamente:

   * Añada la línea siguiente a `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`:

     `customBlobStore=true`

   * A continuación, añada las siguientes líneas a `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`:

     ```
     path=./crx-quickstart/repository/datastore
     minRecordLength=4096
     ```

1. AEM Ahora necesita cambiar los modos de ejecución en el archivo de guerra de la versión 6.5 de la. AEM Para ello, cree primero una carpeta temporal que aloje la guerra de la versión 6.5 de la. El nombre de la carpeta en este ejemplo es `temp`. Una vez copiado el archivo WAR, extraiga su contenido ejecutando desde la carpeta temporal:

   ```
   jar xvf aem-quickstart-6.5.0.war
   ```

1. Una vez extraído el contenido, vaya a **WEB-INF** y edite el archivo web.xml para cambiar los modos de ejecución. Para encontrar la ubicación donde están configurados en el XML, busque la variable `sling.run.modes` cadena. Una vez encontrado, cambie los modos de ejecución en la siguiente línea de código, que de forma predeterminada está configurada como author:

   ```bash
   <param-value >author</param-value>
   ```

1. Cambie el valor de autor anterior y establezca los modos de ejecución en: `author,crx3,crx3tar`. El bloque final de código debería tener este aspecto:

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. Vuelva a crear el frasco con el contenido modificado:

   ```bash
   jar cvf aem65.war
   ```

1. Finalmente, implemente el nuevo archivo de guerra en TomCat.
