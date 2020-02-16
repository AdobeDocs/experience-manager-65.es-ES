---
title: Realización de una actualización in situ
seo-title: Realización de una actualización in situ
description: Obtenga información sobre cómo realizar una actualización in situ.
seo-description: Obtenga información sobre cómo realizar una actualización in situ.
uuid: 478cb9db-1ea8-4bdb-b333-411dcbf2d927
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: fcb17227-ff1f-4b47-ae94-6b7f60923876
docset: aem65
translation-type: tm+mt
source-git-commit: a8deb66b23e6ddde9c5f6379ef4f766668336369

---


# Realización de una actualización in situ{#performing-an-in-place-upgrade}

>[!NOTE]
>
>Esta página describe el procedimiento de actualización para AEM 6.5. Si tiene una instalación implementada en un servidor de aplicaciones, consulte Pasos [de actualización para instalaciones](/help/sites-deploying/app-server-upgrade.md)de Application Server.

## Pasos previos a la actualización {#pre-upgrade-steps}

Antes de ejecutar la actualización, deben realizarse varios pasos. Consulte [Actualización de código y personalizaciones](/help/sites-deploying/upgrading-code-and-customizations.md) y Tareas [de mantenimiento](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) previas a la actualización para obtener más información. Además, asegúrese de que el sistema cumple los requisitos de la nueva versión de AEM. Vea cómo el Detector de patrones puede ayudarle a estimar la complejidad de la actualización y también consulte la sección Alcance de actualización y requisitos de [Planificación de la actualización](/help/sites-deploying/upgrade-planning.md) para obtener más información.

## Requisitos previos de migración {#migration-prerequisites}

* **** Versión mínima requerida de Java: La herramienta de migración solo funciona con las versiones 7 y posteriores de Java. Tenga en cuenta que para AEM 6.3 y versiones posteriores, JRE 8 de Oracle y JRE 7 y 8 de IBM son las únicas versiones admitidas.

* **** Instancia actualizada: Si va a realizar la actualización desde una versión **anterior a la 5.6**, asegúrese de haber realizado una actualización in-situ a AEM 6.0 siguiendo el procedimiento descrito en la versión 6.0 de la documentación de actualización.

## Preparación del archivo jar de inicio rápido de AEM {#prep-quickstart-file}

1. Detenga la instancia si se está ejecutando.

1. Descargue el nuevo archivo AEM jar y úselo para reemplazar el antiguo que se encuentra fuera de la `crx-quickstart` carpeta.

1. Desempaca el nuevo frasco de arranque rápido ejecutando:

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## Migración del repositorio de contenido {#content-repository-migration}

Esta migración no es necesaria si está actualizando desde AEM 6.3. Para las versiones anteriores a la 6.3, Adobe proporciona una herramienta que se puede utilizar para migrar el repositorio a la nueva versión de la barra de segmentos Oak presente en AEM 6.3. Se proporciona como parte del paquete de inicio rápido y es obligatorio para cualquier actualización que vaya a utilizar TarMK. Las actualizaciones para entornos que utilizan MongoMK no requieren migración de repositorio. For more information on what the benefits of the new Segment Tar format are, see the [Migrating to Oak Segment Tar FAQ](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions).

La migración real se realiza utilizando el archivo jar AEM de inicio rápido estándar, ejecutado con una nueva `-x crx2oak` opción que ejecuta la herramienta crx2oak para simplificar la actualización y hacerla más robusta.

>[!NOTE]
>
>Si está realizando la migración de contenido del repositorio TarMK con la extensión CRX2Oak Quickstart, puede quitar el **modo de ejecución de contenido** de muestra agregando lo siguiente a la línea de comandos de migración:
>
>* `--promote-runmode nosamplecontent`
>



Para determinar el comando que debe ejecutar, utilice el siguiente comando:

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

Donde `<<YOUR_PROFILE>>` y `<<ADDITIONAL_FLAGS>>` se sustituyen por el perfil y los indicadores enumerados en la tabla siguiente:

<table>
 <tbody>
  <tr>
   <td><strong>Repositorio de origen</strong></td>
   <td><strong>Repositorio de objetivos</strong></td>
   <td><strong>Perfil</strong></td>
   <td><strong>Indicadores adicionales</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2 o TarMK con <code>FileDataStore</code></td>
   <td>TarMK</td>
   <td>segment-fds</td>
   <td>Consulte la sección Resolución de problemas más abajo</td>
  </tr>
  <tr>
   <td>crx2</td>
   <td>MongoMK</td>
   <td>mongo-from-crx2 </td>
   <td><code>-T mongo-uri=mongo://mongo-host:mongo-port -T mongo-db=mongo-database-name</code></td>
  </tr>
  <tr>
   <td>TarMK o crx2 con <code>S3DataStore</code></td>
   <td>TarMK</td>
   <td>segment-custom-ds</td>
   <td>Consulte la sección Resolución de problemas más abajo</td>
  </tr>
  <tr>
   <td>TarMK sin almacén de datos</td>
   <td>TarMK</td>
   <td>segment-no-ds</td>
   <td> </td>
  </tr>
  <tr>
   <td>MongoMK</td>
   <td>MongoMK</td>
   <td>No se necesita migración</td>
   <td> </td>
  </tr>
 </tbody>
</table>

**Donde:**

* `mongo-host` es la IP del servidor MongoDB (por ejemplo, 127.0.0.1)

* `mongo-port` es el puerto del servidor MongoDB (por ejemplo: 27 de noviembre de 2017)

* `mongo-database-name` representa el nombre de la base de datos (por ejemplo: aem-author)

**También puede requerir conmutadores adicionales para los siguientes escenarios:**

* Si está realizando la actualización en un sistema Windows en el que la asignación de memoria Java no se gestiona correctamente, agregue el `--disable-mmap` parámetro al comando.

* Si utiliza Java 7, agregue el `-XX:MaxPermSize=2048m` parámetro justo después del `-Xmx` parámetro.

Para obtener instrucciones adicionales sobre el uso de la herramienta crx2oak, consulte Uso de la herramienta [de migración](/help/sites-deploying/using-crx2oak.md)CRX2Oak. El JAR de ayuda crx2oak se puede actualizar manualmente si es necesario, reemplazándolo manualmente por versiones más nuevas después de desempaquetar el inicio rápido. Su ubicación en la carpeta de instalación de AEM es: `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`. La versión más reciente de la herramienta de migración CRX2Oak se puede descargar del repositorio de Adobe en:
 [https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/)

Si la migración se ha completado correctamente, la herramienta se cerrará con un código de salida de cero. Además, compruebe si hay mensajes WARN y ERROR en el `upgrade.log` archivo, ubicado `crx-quickstart/logs` en el directorio de instalación de AEM, ya que podrían indicar errores no fatales que se produjeron durante la migración.

Compruebe los archivos de configuración debajo de la `crx-quickstart/install` carpeta. Si fuera necesaria una migración, se actualizarán para reflejar el repositorio de destino.

**Una nota sobre los almacenes de datos:**

Aunque `FileDataStore` es el nuevo valor predeterminado para las instalaciones de AEM 6.3, no es necesario utilizar un almacén de datos externo. Aunque se recomienda utilizar un almacén de datos externo como práctica recomendada para implementaciones de producción, no es un requisito previo para la actualización. Debido a la complejidad que ya existe en la actualización de AEM, recomendamos realizar la actualización sin realizar una migración al almacén de datos. Si lo desea, la migración del almacén de datos se puede ejecutar posteriormente como un esfuerzo independiente.

## Solución de problemas de migración {#troubleshooting-migration-issues}

Si está actualizando desde la versión 6.3, omita esta sección. Aunque los perfiles crx2oak proporcionados deben satisfacer las necesidades de la mayoría de los clientes, en ocasiones se necesitarán parámetros adicionales. Si se produce un error durante la migración, es posible que haya aspectos de su entorno que requieran opciones de configuración adicionales. Si es así, probablemente se producirá el siguiente error:

**No se copiarán los puntos de comprobación porque no se especificó ningún almacén de datos externo. Esto resultará en la reindexación completa del repositorio en el primer inicio. Use —Skicheckpoints para forzar la migración o consulte https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration para obtener más información.**

Por alguna razón, el proceso de migración necesita acceder a los binarios en el almacén de datos y no puede encontrarlos. Para especificar la configuración del almacén de datos, incluya los siguientes indicadores en la `<<ADDITIONAL_FLAGS>>` parte del comando de migración:

**Para almacenes de datos S3:**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

Donde `/path/to/SharedS3DataStore.config` representa la ruta de acceso al archivo de configuración del almacén de datos S3 y `/path/to/datastore` representa la ruta de acceso al almacén de datos S3.

**Para almacenes de datos de archivos:**

```shell
--src-datastore=/path/to/datastore
```

Donde `/path/to/datastore` representa la ruta de acceso al almacén de datos de archivos.

## Realización De La Actualización {#performing-the-upgrade}

**Si utiliza S3:**

1. Retire los vástagos que haya debajo `crx-quickstart/install` de una versión anterior del conector S3.

1. Descargue la última versión del conector S3 1.8.x de [https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/)

1. Extraiga el paquete en una carpeta temporal y copie el contenido de `jcr_root/libs/system/install` en la `crx-quickstart/install` carpeta.

### Determinación del comando de inicio de actualización correcto {#determining-the-correct-upgrade-start-command}

Para ejecutar la actualización, es importante iniciar AEM utilizando el archivo jar para que se muestre la instancia. Para actualizar a 6.5, también puede ver otras opciones de migración y reestructuración de contenido en Migración [de contenido](/help/sites-deploying/lazy-content-migration.md) diferida que puede elegir con el comando upgrade.

Tenga en cuenta que iniciar AEM desde el script de inicio no iniciará la actualización. La mayoría de los clientes inician AEM utilizando el script de inicio y han personalizado este script de inicio para incluir conmutadores para configuraciones de entorno como configuración de memoria, certificados de seguridad, etc. Por este motivo, recomendamos seguir este procedimiento para determinar el comando de actualización correcto:

1. En una instancia de AEM en ejecución, ejecute lo siguiente desde la línea de comandos:

   ```shell
   ps -ef | grep java
   ```

1. Busque el proceso de AEM. Se verá como:

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.2.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. Modifique el comando reemplazando la ruta de acceso al tarro existente ( `crx-quickstart/app/aem-quickstart*.jar` en este caso) por el nuevo tarro que es un elemento secundario de la `crx-quickstart` carpeta. Usando nuestro comando anterior como ejemplo, nuestro comando sería:

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   Esto garantizará que se apliquen todos los parámetros de memoria adecuados, los modos de ejecución personalizados y otros parámetros ambientales para la actualización. Una vez completada la actualización, la instancia puede iniciarse desde la secuencia de comandos de inicio en futuras inicios.

## Implementar base de código actualizada {#deploy-upgraded-codebase}

Una vez que se haya completado el proceso de actualización in situ, se debe implementar la base de código actualizada. Los pasos para actualizar la base de código para que funcione en la versión de destino de AEM se encuentran en la página [Código de](/help/sites-deploying/upgrading-code-and-customizations.md)actualización y personalizaciones.

## Realizar comprobaciones posteriores a la actualización y solucionar problemas {#perform-post-upgrade-check-troubleshooting}

Consulte Comprobaciones [posteriores a la actualización y resolución de problemas](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).
