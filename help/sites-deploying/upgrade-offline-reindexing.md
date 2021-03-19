---
title: Uso de la reindexación sin conexión para reducir el tiempo de inactividad durante una actualización
description: Aprenda a utilizar la metodología de reindexación sin conexión para reducir el tiempo de inactividad del sistema al realizar una actualización AEM.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Actualización
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1344'
ht-degree: 0%

---


# Uso de la reindexación sin conexión para reducir el tiempo de inactividad durante una actualización {#offline-reindexing-to-reduce-downtime-during-upgrades}

## Introducción {#introduction}

Uno de los desafíos clave para actualizar Adobe Experience Manager es el tiempo de inactividad asociado con el entorno de creación cuando se realiza una actualización in situ. Los autores de contenido no podrán acceder al entorno durante una actualización. Por lo tanto, es deseable minimizar la cantidad de tiempo que se tarda en realizar la actualización. Para repositorios grandes, especialmente proyectos de AEM Assets, que generalmente tienen grandes almacenes de datos y un alto nivel de cargas de recursos por hora, la reindexación de los índices de Oak toma un porcentaje significativo del tiempo de actualización.

En esta sección se describe cómo utilizar la herramienta Oak-run para reindexar el repositorio **antes** de realizar la actualización, reduciendo así la cantidad de downtime durante la actualización real. Los pasos presentados se pueden aplicar a los índices de [Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html) para las versiones AEM 6.4 y posteriores.

## Información general {#overview}

Las nuevas versiones de la AEM introducen cambios en las definiciones de índices de Oak a medida que se expande el conjunto de funciones. Los cambios en los índices de Oak obligan a la reindexación al actualizar la instancia de AEM. La reindexación es costosa para las implementaciones de recursos, ya que el texto de los recursos (por ejemplo, texto en un archivo pdf) se extrae e e indexa. Con los repositorios MongoMK, los datos se mantienen en la red, lo que aumenta aún más la cantidad de tiempo que se tarda en reindexar.

El problema que la mayoría de los clientes enfrentan durante una actualización es reducir el tiempo de inactividad. La solución es **omitir** la actividad de reindexación durante la actualización. Esto se puede lograr creando los nuevos índices **previous** para realizar la actualización y luego simplemente importándolos durante la actualización.

## Enfoque {#approach}

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-process.png)

La idea es crear el índice antes de la actualización, frente a las definiciones de índice de la versión de AEM de destino usando la herramienta [Oak-run](/help/sites-deploying/indexing-via-the-oak-run-jar.md). El diagrama anterior muestra el método de reindexación sin conexión.

Además, este es el orden de los pasos descritos en el enfoque:

1. El texto de los binarios se extrae primero
2. Se crean definiciones de índice de Target
3. Se crean índices sin conexión
4. Los índices se importan durante el proceso de actualización

### Extracción de texto {#text-extraction}

Para habilitar la indexación completa en AEM, el texto de binarios como PDF se extrae y se agrega al índice. Normalmente, este es un paso costoso en el proceso de indexación. La extracción de texto es un paso de optimización que se recomienda especialmente para reindexar repositorios de recursos, ya que almacenan un gran número de binarios.

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-text-extraction.png)

El texto de los binarios almacenados en el sistema se puede extraer utilizando la herramienta oak-run con la biblioteca tika. Un clon de los sistemas de producción se puede tomar antes de la actualización y se puede utilizar para este proceso de extracción de texto. A continuación, este proceso crea el almacén de texto siguiendo estos pasos:

**1. Recorra el repositorio y recopila los detalles de los binarios**

Este paso genera un archivo CSV que contiene un tuplo de binarios, con una ruta y un id. de blob.

Ejecute el siguiente comando desde el directorio desde el que desea crear el índice. El ejemplo siguiente asume el directorio raíz del repositorio.

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

Donde `nodestore path` es `mongo_ur` o `crx-quickstart/repository/segmentstore/`

Utilice el parámetro `--fake-ds-path=temp` en lugar de `–fds-path` para acelerar el proceso.

**2. Vuelva a utilizar el almacén de texto binario disponible en el índice existente**

Descargue los datos de índice del sistema existente y extraiga el almacén de texto.

Puede volcar los datos de índice existentes mediante el siguiente comando:

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

Donde `nodestore path` es `mongo_ur` o `crx-quickstart/repository/segmentstore/`

A continuación, utilice el volcado de índice anterior para rellenar el almacén:

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

Donde `oak-index-name` es el nombre del índice de texto completo, por ejemplo &quot;lucene&quot;.

**3. Ejecute el proceso de extracción de texto utilizando la biblioteca tika para los binarios omitidos en el paso anterior**

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

Donde `datastore path` es la ruta al almacén de datos binario.

El almacén de texto creado se puede actualizar y reutilizar para reindexar escenarios en el futuro.

Para obtener más información sobre el proceso de extracción de texto, consulte la [documentación de Oak-run](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html).

### Reindexación sin conexión {#offline-reindexing}

![offline-reindexing-upgrade-offline-reindexxing](assets/offline-reindexing-upgrade-offline-reindexing.png)

Cree el índice de Lucene sin conexión antes de la actualización. Si utiliza MongoMK, se recomienda ejecutarlo directamente en uno de los nodos MongoMk, ya que esto evita sobrecargas de red.

Para crear el índice sin conexión, siga los siguientes pasos:

**1. Generar definiciones de índice Oak Lucene para la versión de AEM de destino**

Volcar las definiciones de índice existentes. Las definiciones de índice que sufrieron cambios se generaron usando el paquete de repositorios de Adobe Granite de la versión de AEM de destino y oak-run.

Para volcar la definición de índice de la instancia de AEM **source**, ejecute este comando:

>[!NOTE]
>
>Para obtener más información sobre las definiciones de índice de dumping, consulte la [documentación de Oak](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data).

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

Donde `datastore path` y `nodestore path` son de la instancia de AEM **source**.

A continuación, genere definiciones de índice a partir de la versión de AEM **target** utilizando el paquete de repositorios Granite de la versión de destino.

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
> El proceso de creación de la definición del índice anterior solo es compatible con la versión `oak-run-1.12.0` posterior. La segmentación se realiza utilizando el paquete de repositorios de Granite `com.adobe.granite.repository-x.x.xx.jar`.

Los pasos anteriores crean un archivo JSON llamado `merge-index-definitions_target.json` que es la definición de índice.

**2. Crear un punto de comprobación en el repositorio**

Cree un punto de comprobación en la instancia de AEM **source** de producción con una duración prolongada. Esto debe hacerse antes de clonar el repositorio.

A través de la consola JMX ubicada en `http://serveraddress:serverport/system/console/jmx`, vaya a `CheckpointMBean` y cree un punto de comprobación con una duración suficiente (por ejemplo, 200 días). Para ello, invoque `CheckpointMBean#createCheckpoint` con `17280000000` como argumento para la duración en milisegundos.

Una vez hecho esto, copie el ID del punto de comprobación recién creado y valide la duración utilizando JMX `CheckpointMBean#listCheckpoints`.

>[!NOTE]
>
> Este punto de comprobación se eliminará cuando el índice se importe más adelante.

Para obtener más información, consulte [checkpoint creation](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint) en la documentación de Oak.

**Realizar la indexación sin conexión para las definiciones de índice generadas**

La reindexación de Lucene se puede realizar sin conexión usando oak-run. Este proceso crea datos de índice en el disco en `indexing-result/indexes`. Hace **no** escritura en el repositorio y, por lo tanto, no requiere detener la ejecución de la instancia de AEM. El almacén de texto creado se alimenta de este proceso:

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

El uso del parámetro `--doc-traversal-mode` es útil con las instalaciones MongoMK, ya que mejora significativamente el tiempo de reindexación al colocar en cola el contenido del repositorio en un archivo plano local. Sin embargo, requiere un espacio de disco adicional del doble del tamaño del repositorio.

En el caso de MongoMK, este proceso se puede acelerar si este paso se ejecuta en una instancia más cercana a la instancia de MongoDB. Si se ejecuta en el mismo equipo, se puede evitar la sobrecarga de red.

Encontrará detalles técnicos adicionales en la [documentación de oak-run para la indexación](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html).

### Importación de índices {#importing-indexes}

Con AEM 6.4 y versiones más recientes, AEM tiene la capacidad incorporada para importar índices desde disco en la secuencia de inicio. Se observa la presencia de datos de índice durante el inicio en la carpeta `<repository>/indexing-result/indexes`. Puede copiar el índice precreado en la ubicación anterior durante el [proceso de actualización](in-place-upgrade.md#performing-the-upgrade) antes de comenzar con la nueva versión del **destino** AEM jar. AEM lo importa en el repositorio y elimina el punto de comprobación correspondiente del sistema. Por lo tanto, se evita completamente un reíndice.

## Sugerencias y resolución de problemas adicionales {#troubleshooting}

A continuación encontrará algunas sugerencias útiles e instrucciones para la resolución de problemas.

### Reducir el impacto en el sistema de producción en directo {#reduce-the-impact-on-the-live-production-system}

Se recomienda clonar el sistema de producción y crear el índice sin conexión mediante el clon. Esto elimina cualquier impacto potencial en el sistema de producción. Sin embargo, el punto de comprobación necesario para importar el índice debe estar presente en el sistema de producción. Por lo tanto, es fundamental crear un punto de comprobación antes de tomar el clon.

### Preparación de un Runbook y ejecución de prueba {#prepare-a-runbook-and-trial-run}

Se recomienda preparar un [runbook](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/upgrade-planning.html#building-the-upgrade-and-rollback-runbook) y realizar algunas pruebas antes de ejecutar la actualización en producción.

### Modo de travesía de documento con indexación sin conexión {#doc-traversal-mode-with-offline-indexing}

La indexación sin conexión requiere múltiples transmisiones de todo el repositorio. Con las instalaciones de MongoMK, se accede al repositorio a través de la red que afecta el rendimiento del proceso de indexación. Una opción es ejecutar el proceso de indexación sin conexión en la propia réplica de MongoDB, que eliminará la sobrecarga de red. Otra opción es el uso del modo doc-transversal.

El modo de travesía Doc se puede aplicar añadiendo el parámetro de línea de comandos `—doc-traversal` al comando oak-run para la indexación sin conexión. Este modo estropea una copia de todo el repositorio en el disco local como un archivo plano y lo utiliza para ejecutar la indexación.
