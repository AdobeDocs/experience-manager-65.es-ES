---
title: Uso de la reindexación sin conexión para reducir el tiempo de inactividad durante una actualización
description: AEM Aprenda a utilizar la metodología de reindexación sin conexión para reducir el tiempo de inactividad del sistema al realizar una actualización de la.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: 85bc041e-0ab1-42de-8bcc-c98a175d7494
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 0%

---

# Uso de la reindexación sin conexión para reducir el tiempo de inactividad durante una actualización {#offline-reindexing-to-reduce-downtime-during-upgrades}

## Introducción {#introduction}

Uno de los desafíos clave para actualizar Adobe Experience Manager es el tiempo de inactividad asociado con el entorno de creación cuando se realiza una actualización in situ. Los autores de contenido no podrán acceder al entorno durante una actualización. Por lo tanto, es deseable minimizar la cantidad de tiempo que se tarda en realizar la actualización. Para repositorios grandes, especialmente proyectos de AEM Assets, que normalmente tienen grandes almacenes de datos y un alto nivel de cargas de recursos por hora, la reindexación de índices Oak toma un porcentaje significativo del tiempo de actualización.

Esta sección describe cómo utilizar la herramienta Oak-run para reindexar el repositorio **antes** realizar la actualización, reduciendo así la cantidad de tiempo de inactividad durante la actualización real. Los pasos presentados se pueden aplicar a [Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html) AEM índices para las versiones 6.4 y posteriores de la aplicación.

## Información general {#overview}

AEM Las nuevas versiones de la introducen cambios en las definiciones de índices de Oak a medida que se expande el conjunto de funciones. AEM Los cambios en los índices de Oak obligan a la reindexación al actualizar la instancia de. La reindexación es costosa para las implementaciones de recursos, ya que el texto de los recursos (por ejemplo, el texto del archivo pdf) se extrae y se indexa. Con los repositorios MongoMK, los datos se mantienen en la red, lo que aumenta aún más la cantidad de tiempo que tarda la reindexación.

El problema al que se enfrentan la mayoría de los clientes durante una actualización es la reducción del tiempo de inactividad. La solución es **omitir** la actividad de reindexación durante la actualización. Esto se puede lograr creando nuevos índices **previo** para realizar la actualización y, a continuación, impórtelos durante la actualización.

## Aproximación {#approach}

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-process.png)

AEM La idea es crear el índice antes de la actualización, comparándolo con las definiciones de índice de la versión de la aplicación de destino de la versión de la aplicación de la versión de la aplicación de la versión de la aplicación de índice. [Oak-run](/help/sites-deploying/indexing-via-the-oak-run-jar.md) herramienta. El diagrama anterior muestra el método de reindexación sin conexión.

Además, este es el orden de los pasos que se describen en el enfoque:

1. El texto de los binarios se extrae primero
2. Se crean las definiciones de índice de destino
3. Se crean índices sin conexión
4. Los índices se importan durante el proceso de actualización

### Extracción de texto {#text-extraction}

AEM Para habilitar la indexación completa en los, el texto de los binarios, como el PDF, se extrae y se añade al índice. Esto suele ser un paso costoso en el proceso de indexación. La extracción de texto es un paso de optimización recomendado especialmente para reindexar repositorios de recursos, ya que almacenan un gran número de binarios.

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-text-extraction.png)

El texto de los binarios almacenados en el sistema se puede extraer utilizando la herramienta oak-run con la biblioteca tika. Se puede tomar un clon de los sistemas de producción antes de la actualización y se puede utilizar para este proceso de extracción de texto. A continuación, este proceso crea el almacén de texto siguiendo los pasos siguientes:

**1. Recorra el repositorio y recopile los detalles de los binarios**

Este paso genera un archivo CSV que contiene una tupla de binarios, una ruta y un ID de blob.

Ejecute el siguiente comando desde el directorio desde el que desea crear el índice. El ejemplo siguiente supone el directorio principal del repositorio.

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

Donde `nodestore path` es el `mongo_ur` o `crx-quickstart/repository/segmentstore/`

Utilice el `--fake-ds-path=temp` en lugar de `–fds-path` para acelerar el proceso.

**2. Reutilizar el almacén de texto binario disponible en el índice existente**

Volcar los datos de índice del sistema existente y extraer el almacén de texto.

Puede volcar los datos de índice existentes mediante el siguiente comando:

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

Donde `nodestore path` es el `mongo_ur` o `crx-quickstart/repository/segmentstore/`

A continuación, utilice el volcado de índice anterior para rellenar el almacén:

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

Donde `oak-index-name` es el nombre del índice de texto completo; por ejemplo, &quot;lucene&quot;.

**3. Ejecute el proceso de extracción de texto utilizando la biblioteca tika para los binarios que se han perdido en el paso anterior**

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

Donde `datastore path` es la ruta al almacén de datos binarios.

El almacén de texto creado se puede actualizar y reutilizar para escenarios de reindexación en el futuro.

Para obtener más información sobre el proceso de extracción de texto, consulte la [Documentación de Oak-run](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html).

### Reindexación sin conexión {#offline-reindexing}

![offline-reindexación-actualización-offline-reindexación](assets/offline-reindexing-upgrade-offline-reindexing.png)

Cree el índice Lucene sin conexión antes de la actualización. Si utiliza MongoMK, se recomienda ejecutarlo directamente en uno de los nodos de MongoMk, ya que esto evita la sobrecarga de red.

Para crear el índice sin conexión, siga los siguientes pasos:

**1. AEM Genere definiciones de índice de Oak Lucene para la versión de destino de la**

Volcar las definiciones de índice existentes. Las definiciones de índice que sufrieron cambios se generaron utilizando el paquete de repositorio de Adobe AEM Granite de la versión de destino y la versión de Oak-run.

Para volcar la definición de índice desde el **origen** AEM Por ejemplo, ejecute este comando:

>[!NOTE]
>
>Para obtener más información sobre las definiciones de índices de dumping, consulte la [Documentación de Oak](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data).

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

Donde `datastore path` y `nodestore path` son de la **origen** AEM instancia de.

A continuación, genere las definiciones de índice a partir de **destino** AEM versión de que utiliza el paquete de repositorio Granite de la versión de destino.

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
>El proceso de creación de la definición de índice anterior solo es compatible con el `oak-run-1.12.0` versión en adelante. El direccionamiento se realiza mediante el paquete del repositorio Granite `com.adobe.granite.repository-x.x.xx.jar`.

Los pasos anteriores crean un archivo JSON llamado `merge-index-definitions_target.json` que es la definición del índice.

**2. Creación de un punto de comprobación en el repositorio**

Creación de un punto de comprobación en la producción **origen** AEM Ejemplo de la larga duración de la vida. Esto debe hacerse antes de clonar el repositorio.

A través de la consola JMX ubicada en `http://serveraddress:serverport/system/console/jmx`, vaya a `CheckpointMBean` y cree un punto de comprobación con una duración suficiente (por ejemplo, 200 días). Para ello, invoque `CheckpointMBean#createCheckpoint` con `17280000000` como argumento para la duración en milisegundos.

Una vez hecho esto, copie el ID del punto de comprobación recién creado y valide la duración mediante JMX `CheckpointMBean#listCheckpoints`.

>[!NOTE]
>
>Este punto de comprobación se eliminará cuando el índice se importe posteriormente.

Para obtener más información, consulte [creación de puntos de comprobación](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint) en la documentación de Oak.

**Realizar indexación sin conexión para las definiciones de índice generadas**

La reindexación de Lucene se puede realizar sin conexión mediante oak-run. Este proceso crea datos de índice en el disco en `indexing-result/indexes`. Sí lo tiene **no** AEM escribir en el repositorio y, por lo tanto, no requiere detener la instancia de la instancia de la ejecución de la. El almacén de texto creado se inserta en este proceso:

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

Uso del `--doc-traversal-mode` Este parámetro es útil con las instalaciones de MongoMK, ya que mejora significativamente el tiempo de reindexación al poner en cola el contenido del repositorio en un archivo plano local. Sin embargo, requiere un espacio en disco adicional del doble del tamaño del repositorio.

Si hay MongoMK, este proceso se puede acelerar si este paso se ejecuta en una instancia más cercana a la instancia de MongoDB. Si se ejecuta en el mismo equipo, se puede evitar la sobrecarga de red.

Puede encontrar más información técnica en la [documentación de oak-run para la indexación](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html).

### Importación de índices {#importing-indexes}

AEM AEM Con la versión 6.4 y versiones más recientes, el usuario tiene la capacidad integrada para importar índices desde el disco en la secuencia de inicio de la aplicación. La carpeta `<repository>/indexing-result/indexes` se observa la presencia de datos de índice durante el inicio. Puede copiar el índice creado previamente en la ubicación anterior durante la [proceso actualización](in-place-upgrade.md#performing-the-upgrade) antes de comenzar con la nueva versión de **destino** AEM ¡Jarra! AEM lo importa al repositorio y elimina el punto de comprobación correspondiente del sistema. Por lo tanto, se evita completamente un reíndice.

## Sugerencias y solución de problemas adicionales {#troubleshooting}

A continuación encontrará algunas sugerencias útiles e instrucciones para la resolución de problemas.

### Reduzca el impacto en el sistema de producción en directo {#reduce-the-impact-on-the-live-production-system}

Se recomienda clonar el sistema de producción y crear el índice sin conexión utilizando el clon. Esto elimina cualquier posible impacto en el sistema de producción. Sin embargo, el punto de comprobación necesario para importar el índice debe estar presente en el sistema de producción. Por lo tanto, es fundamental crear un punto de comprobación antes de tomar el clon.

### Preparar un Runbook y una ejecución de prueba {#prepare-a-runbook-and-trial-run}

Se recomienda preparar una [runbook](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/upgrade-planning.html#building-the-upgrade-and-rollback-runbook) y realice algunas pruebas antes de ejecutar la actualización en producción.

### Modo de recorrido de documentos con indexación sin conexión {#doc-traversal-mode-with-offline-indexing}

La indexación sin conexión requiere varias travesías de todo el repositorio. Con las instalaciones de MongoMK, se accede al repositorio a través de la red, lo que afecta al rendimiento del proceso de indexación. Una opción es ejecutar el proceso de indexación sin conexión en la propia réplica de MongoDB, lo que eliminará la sobrecarga de red. Otra opción es el uso del modo de recorrido doc.

El modo de recorrido de documentos se puede aplicar añadiendo el parámetro de línea de comandos `—doc-traversal` al comando oak-run para la indexación sin conexión. Este modo pone en cola una copia de todo el repositorio en el disco local como archivo plano y la utiliza para ejecutar la indexación.
