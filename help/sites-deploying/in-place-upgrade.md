---
title: Realización de una actualización in situ
description: Obtenga información sobre cómo realizar una actualización in situ.
topic-tags: upgrading
feature: Upgrading
exl-id: aef6ef00-993c-4252-b0ad-ddc4917beaf7
source-git-commit: 64c9296554c55b539145dd59a14b2255b1750e47
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 0%

---

# Realización de una actualización in situ{#performing-an-in-place-upgrade}

>[!NOTE]
>
>Esta página describe el procedimiento de actualización para AEM 6.5. Si tiene una instalación implementada en un servidor de aplicaciones, consulte [Pasos de actualización para las instalaciones del servidor de aplicaciones](/help/sites-deploying/app-server-upgrade.md).

## Pasos previos a la actualización {#pre-upgrade-steps}

Antes de ejecutar la actualización, hay que completar varios pasos. Consulte [Actualización de código y personalizaciones](/help/sites-deploying/upgrading-code-and-customizations.md) y [Tareas de mantenimiento previas a la actualización](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) para obtener más información. Además, asegúrese de que su sistema cumpla los requisitos de la nueva versión de AEM. Consulte cómo Pattern Detector puede ayudarle a calcular la complejidad de la actualización y también consulte la sección Alcance de la actualización y Requisitos de [Planificación de la actualización](/help/sites-deploying/upgrade-planning.md) para obtener más información.

<!--Finally, note that the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## Requisitos previos de migración {#migration-prerequisites}

* **Versión mínima requerida de Java:** La herramienta de migración solo funciona con las versiones 7 y posteriores de Java. Tenga en cuenta que para AEM 6.3 y posteriores, JRE 8 de Oracle y JRE 7 y 8 de IBM son las únicas versiones compatibles.

* **Instancia actualizada:** Si está actualizando desde una versión **mayores de 5,6**, asegúrese de haber realizado una actualización in situ a AEM 6.0 siguiendo el procedimiento descrito en la versión 6.0 de la documentación de actualización.

## Preparación del archivo jar de inicio rápido AEM {#prep-quickstart-file}

1. Detenga la instancia si se está ejecutando.

1. Descargue el nuevo archivo jar de AEM y utilícelo para reemplazar el antiguo fuera del `crx-quickstart` carpeta.

1. Desempaquete el nuevo jar de inicio rápido ejecutando:

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## Migración del repositorio de contenido {#content-repository-migration}

Esta migración no es necesaria si actualiza desde AEM 6.3. Para versiones anteriores a la 6.3, Adobe proporciona una herramienta que se puede utilizar para migrar el repositorio a la nueva versión de Oak Segment Tar presente en la AEM 6.3. Se proporciona como parte del paquete de inicio rápido y es obligatoria para cualquier actualización que vaya a utilizar TarMK. Las actualizaciones para entornos que utilizan MongoMK no requieren la migración del repositorio. Para obtener más información sobre las ventajas del nuevo formato Tar de segmento, consulte la [Preguntas frecuentes sobre la migración a Oak Segment Tar](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions).

La migración real se realiza mediante el archivo jar AEM inicio rápido estándar, ejecutado con un nuevo `-x crx2oak` que ejecuta la herramienta crx2oak para simplificar la actualización y hacerla más robusta.

>[!NOTE]
>
>Si está realizando la migración de contenido del repositorio TarMK mediante la extensión CRX2Oak Quickstart, puede quitar la variable **samplecontent** runmode añadiendo lo siguiente a la línea de comandos de migración:
>
>* `--promote-runmode nosamplecontent`
>


Para determinar el comando que debe ejecutar, utilice el siguiente comando:

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

Donde `<<YOUR_PROFILE>>` y `<<ADDITIONAL_FLAGS>>` se sustituyen por el perfil y los indicadores enumerados en la siguiente tabla:

<table>
 <tbody>
  <tr>
   <td><strong>Repositorio de origen</strong></td>
   <td><strong>Repositorio de Target</strong></td>
   <td><strong>Perfil</strong></td>
   <td><strong>Indicadores adicionales</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2 o TarMK con <code>FileDataStore</code></td>
   <td>TarMK</td>
   <td>segment-fds</td>
   <td>Consulte la sección Resolución de problemas a continuación</td>
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
   <td>Consulte la sección Resolución de problemas a continuación</td>
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
   <td>No es necesario realizar ninguna migración</td>
   <td> </td>
  </tr>
 </tbody>
</table>

**Donde:**

* `mongo-host` es la IP del servidor MongoDB (por ejemplo, 127.0.0.1)

* `mongo-port` es el puerto del servidor MongoDB (por ejemplo: 27017)

* `mongo-database-name` representa el nombre de la base de datos (por ejemplo: aem-author)

**También puede requerir conmutadores adicionales para los siguientes escenarios:**

* Si está realizando la actualización en un sistema Windows en el que la asignación de memoria Java no se administra correctamente, agregue la variable `--disable-mmap` al comando.

* Si utiliza Java 7, agregue la variable `-XX:MaxPermSize=2048m` justo después de `-Xmx` parámetro.

Para obtener instrucciones adicionales sobre el uso de la herramienta crx2oak, consulte Uso de la variable [Herramienta de migración CRX2Oak](/help/sites-deploying/using-crx2oak.md). El JAR de ayuda de crx2oak se puede actualizar manualmente si es necesario, reemplazándolo manualmente con versiones más recientes después de desempaquetar el inicio rápido. Su ubicación en la carpeta de instalación de AEM es: `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`. La versión más reciente de la herramienta de migración CRX2Oak está disponible para su descarga desde el Repositorio de Adobes en: [https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

Si la migración se ha completado correctamente, la herramienta se cerrará con un código de salida de cero. Además, compruebe los mensajes WARN y ERROR en la `upgrade.log` archivo, ubicado en `crx-quickstart/logs` en el directorio de instalación de AEM, ya que podrían indicar errores no fatales que se produjeron durante la migración.

Compruebe los archivos de configuración que hay debajo `crx-quickstart/install` carpeta. Si era necesaria una migración, se actualizarán para reflejar el repositorio de destino.

**Una nota sobre los almacenes de datos:**

While `FileDataStore` es el nuevo valor predeterminado para las instalaciones de AEM 6.3, ya que no se requiere el uso de un almacén de datos externo. Aunque se recomienda utilizar un almacén de datos externo como práctica recomendada para implementaciones de producción, no es un requisito previo para la actualización. Debido a la complejidad ya presente en la actualización de AEM, recomendamos realizar la actualización sin realizar una migración del almacén de datos. Si lo desea, se puede ejecutar posteriormente una migración del almacén de datos como un esfuerzo independiente.

## Solución de problemas de migración {#troubleshooting-migration-issues}

Por favor, omita esta sección si está actualizando desde la versión 6.3. Aunque los perfiles crx2oak proporcionados deben satisfacer las necesidades de la mayoría de los clientes, en ocasiones será necesario usar parámetros adicionales. Si se produce un error durante la migración, es posible que haya aspectos del entorno que requieran opciones de configuración adicionales. Si es así, es probable que encuentre el siguiente error:

**Los puntos de comprobación no se copiarán, ya que no se ha especificado ningún almacén de datos externo. Esto resultará en la reindexación completa del repositorio en el primer inicio. Utilice —skip-checkpoints para forzar la migración o consulte https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration para obtener más información.**

Por alguna razón, el proceso de migración necesita acceder a los binarios en el almacén de datos y no puede encontrarlo. Para especificar la configuración del almacén de datos, incluya los siguientes indicadores en la variable `<<ADDITIONAL_FLAGS>>` del comando de migración:

**Para los almacenes de datos S3:**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

Donde `/path/to/SharedS3DataStore.config` representa la ruta al archivo de configuración del almacén de datos S3 y `/path/to/datastore` representa la ruta al almacén de datos S3.

**Para los almacenes de datos de archivos:**

```shell
--src-datastore=/path/to/datastore
```

Donde `/path/to/datastore` representa la ruta de acceso al almacén de datos del archivo.

## Realización De La Actualización {#performing-the-upgrade}

**Si utiliza S3:**

1. Elimine cualquier frasco debajo `crx-quickstart/install` asociado a una versión anterior del conector S3.

1. Descargue la última versión del conector S3 1.10.x desde [https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/)

1. Extraiga el paquete en una carpeta temporal y copie el contenido de `jcr_root/libs/system/install` a `crx-quickstart/install` carpeta.

### Determinación del comando correcto de inicio de la actualización {#determining-the-correct-upgrade-start-command}

Para ejecutar la actualización, es importante comenzar AEM utilizar el archivo jar para que aparezca la instancia. Para actualizar a la versión 6.5, consulte también otras opciones de migración y reestructuración de contenido en [Migración de contenido diferido](/help/sites-deploying/lazy-content-migration.md) que puede elegir con el comando upgrade.

>[!IMPORTANT]
>
>Si ejecuta Oracle Java 11 (o versiones generales de Java más recientes que 8), será necesario agregar modificadores adicionales a la línea de comandos al iniciar AEM. Para obtener más información, consulte [Consideraciones sobre Java 11](/help/sites-deploying/custom-standalone-install.md#java-considerations).

Tenga en cuenta que iniciar AEM desde el script de inicio no iniciará la actualización. La mayoría de los clientes empiezan AEM usando el script de inicio y han personalizado este script de inicio para incluir conmutadores para configuraciones de entorno como configuración de memoria, certificados de seguridad, etc. Por este motivo, recomendamos seguir este procedimiento para determinar el comando de actualización adecuado:

1. En una instancia de AEM en ejecución, ejecute lo siguiente desde la línea de comandos:

   ```shell
   ps -ef | grep java
   ```

1. Busque el proceso de AEM. Se parecerá a:

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.2.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. Modifique el comando reemplazando la ruta al jar existente ( `crx-quickstart/app/aem-quickstart*.jar` en este caso) con el nuevo jar que es un hermano del `crx-quickstart` carpeta. Con nuestro comando anterior como ejemplo, nuestro comando sería:

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   Esto asegurará que se apliquen todos los parámetros de memoria adecuados, modos de ejecución personalizados y otros parámetros ambientales para la actualización. Una vez finalizada la actualización, la instancia puede iniciarse desde el script de inicio en futuras iniciaciones.

## Implementar base de código actualizada {#deploy-upgraded-codebase}

Una vez completado el proceso de actualización in situ, se debe implementar la base de código actualizada. Los pasos para actualizar el código base para que funcione en la versión de destino de AEM se encuentran en [Página Actualizar código y personalizaciones](/help/sites-deploying/upgrading-code-and-customizations.md).

## Realizar comprobaciones y resolución de problemas posteriores a la actualización {#perform-post-upgrade-check-troubleshooting}

Consulte [Comprobación y solución de problemas posteriores a la actualización](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).
