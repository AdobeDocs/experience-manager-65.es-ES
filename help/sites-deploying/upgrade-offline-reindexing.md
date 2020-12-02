---
title: Uso de la reindexación sin conexión para reducir el tiempo de inactividad durante una actualización
description: Aprenda a utilizar la metodología de reindexación sin conexión para reducir el tiempo de inactividad del sistema al realizar una actualización AEM.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
translation-type: tm+mt
source-git-commit: 9a4ae73c08657195da2741cccdb196bd7f7142c9
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 0%

---


# Uso de la reindexación sin conexión para reducir el tiempo de inactividad durante una actualización {#offline-reindexing-to-reduce-downtime-during-upgrades}

## Introducción {#introduction}

Uno de los desafíos clave para la actualización de Adobe Experience Manager es el tiempo de inactividad asociado con el entorno de creación cuando se realiza una actualización in situ. Los autores de contenido no podrán acceder al entorno durante una actualización. Por lo tanto, es deseable minimizar la cantidad de tiempo que se tarda en realizar la actualización. Para repositorios grandes, especialmente proyectos de AEM Assets, que suelen tener grandes almacenes de datos y un alto nivel de cargas de recursos por hora, la reindexación de índices Oak toma un porcentaje significativo del tiempo de actualización.

Esta sección describe cómo utilizar la herramienta Oak-run para reindexar el repositorio **antes de** realizar la actualización, reduciendo así la cantidad de tiempo de inactividad durante la actualización real. Los pasos presentados se pueden aplicar a [índices de Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html) para versiones AEM 6.4 y posteriores.

## Información general {#overview}

Las nuevas versiones de la AEM introducen cambios en las definiciones de índice Oak a medida que se expande el conjunto de funciones. Los cambios en los índices Oak obligan a volver a indexar al actualizar la instancia de AEM. La reindexación resulta costosa para las implementaciones de recursos, ya que el texto de los recursos (por ejemplo, el texto en un archivo pdf) se extrae e e indexa. Con los repositorios de MongoMK, los datos se mantienen en la red, lo que aumenta aún más la cantidad de tiempo que se tarda en volver a indexar.

El problema que la mayoría de los clientes enfrentan durante una actualización es reducir el tiempo de inactividad. La solución es **omitir** la actividad de reindexación durante la actualización. Esto se puede lograr creando los nuevos índices **anterior** para realizar la actualización y luego simplemente importándolos durante la actualización.

## Enfoque {#approach}

![offline-reindexing-upgrade-text-extracción](assets/offline-reindexing-upgrade-process.png)

La idea es crear el índice antes de la actualización, en comparación con las definiciones de índice de la versión de destinatario AEM usando la herramienta [Oak-run](/help/sites-deploying/indexing-via-the-oak-run-jar.md). El diagrama anterior muestra el enfoque de reindexación sin conexión.

Además, este es el orden de los pasos descritos en el enfoque:

1. El texto de los binarios se extrae primero
2. Se crean definiciones de índice de destinatario
3. Se crean índices sin conexión
4. Los índices se importan durante el proceso de actualización

### Extracción de texto {#text-extraction}

Para habilitar la indexación completa en AEM, se extrae el texto de los binarios como PDF y se agrega al índice. Normalmente, este es un paso costoso en el proceso de indexación. La extracción de texto es un paso de optimización que se recomienda especialmente para volver a indexar los repositorios de recursos, ya que almacenan un gran número de binarios.

![offline-reindexing-upgrade-text-extracción](assets/offline-reindexing-upgrade-text-extraction.png)

El texto de los binarios almacenados en el sistema se puede extraer utilizando la herramienta de roble de gran tamaño con la biblioteca tika. Antes de la actualización se puede realizar un clon de los sistemas de producción, que se puede utilizar para este proceso de extracción de texto. A continuación, este proceso crea el almacén de texto siguiendo los pasos siguientes:

**1. Recorra el repositorio y recopila los detalles de los binarios**

Este paso produce un archivo CSV que contiene un tuplo de binarios, con una ruta y un id. de blob.

Ejecute el comando siguiente desde el directorio desde el que desea crear el índice. El ejemplo siguiente supone que el directorio raíz del repositorio.

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

Donde `nodestore path` es `mongo_ur` o `crx-quickstart/repository/segmentstore/`

Utilice el parámetro `--fake-ds-path=temp` en lugar de `–fds-path` para acelerar el proceso.

**2. Reutilice el almacén de texto binario disponible en el índice existente**

Descargue los datos de índice del sistema existente y extraiga el almacén de texto.

Puede volcar los datos de índice existentes mediante el siguiente comando:

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

Donde `nodestore path` es `mongo_ur` o `crx-quickstart/repository/segmentstore/`

A continuación, utilice el volcado de índice anterior para rellenar la tienda:

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

Donde `oak-index-name` es el nombre del índice de texto completo, por ejemplo &quot;lucene&quot;.

**3. Ejecute el proceso de extracción de texto con la biblioteca tika para los binarios omitidos en el paso anterior**

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

Donde `datastore path` es la ruta al almacén de datos binario.

El almacén de texto creado se puede actualizar y reutilizar para volver a indexar escenarios en el futuro.

Para obtener más información sobre el proceso de extracción de texto, consulte la [documentación de ejecución de Oak](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html).

### Reindexación sin conexión {#offline-reindexing}

![offline-reindexing-upgrade-offline-reindexing](assets/offline-reindexing-upgrade-offline-reindexing.png)

Cree el índice de Lucene sin conexión antes de la actualización. Si utiliza MongoMK, se recomienda ejecutarlo directamente en uno de los nodos MongoMk, ya que esto evita la sobrecarga de red.

Para crear el índice sin conexión, siga los siguientes pasos:

**1. Generar definiciones de índice Oak Lucene para la versión de AEM de destinatario**

Volcar las definiciones de índice existentes. Las definiciones de índice que fueron objeto de cambios se generaron utilizando el paquete de repositorio de Adobe Granite de la versión de destinatario AEM y de oak-run.

Para volcar la definición de índice de la instancia de AEM **source**, ejecute este comando:

>[!NOTE]
>
>Para obtener más información sobre las definiciones de los índices de dumping, consulte la [documentación de Oak](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data).

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

Donde `datastore path` y `nodestore path` son de la instancia de AEM **source**.

A continuación, genere definiciones de índice a partir de la versión de AEM **destinatario** utilizando el paquete de repositorios Granite de la versión de destinatario.

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
> El proceso de creación de definiciones de índice anterior solo se admite a partir de la versión `oak-run-1.12.0`. La segmentación se realiza mediante el paquete de repositorios Granite `com.adobe.granite.repository-x.x.xx.jar`.

Los pasos anteriores crean un archivo JSON llamado `merge-index-definitions_target.json` que es la definición de índice.

**2. Cree un punto de comprobación en el repositorio**

Cree un punto de comprobación en la instancia de producción **origen** AEM con una duración prolongada. Esto debe hacerse antes de clonar el repositorio.

A través de la consola JMX ubicada en `http://serveraddress:serverport/system/console/jmx`, vaya a `CheckpointMBean` y cree un punto de comprobación con una duración suficiente (por ejemplo, 200 días). Para ello, invoque `CheckpointMBean#createCheckpoint` con `17280000000` como el argumento de la duración de duración en milisegundos.

Una vez finalizado, copie la identificación del punto de comprobación recién creada y valide la duración utilizando JMX `CheckpointMBean#listCheckpoints`.

>[!NOTE]
>
> Este punto de comprobación se eliminará cuando el índice se importe más tarde.

Para obtener más información, consulte [creación de puntos de comprobación](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint) en la documentación de Oak.

**Realizar indexación sin conexión para las definiciones de índice generadas**

El reindexado de Lucene se puede realizar sin conexión mediante roble. Este proceso crea datos de índice en el disco en `indexing-result/indexes`. **no** escribe en el repositorio y, por lo tanto, no requiere detener la ejecución de la instancia de AEM. El almacén de texto creado se incluye en este proceso:

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

El uso del parámetro `--doc-traversal-mode` resulta práctico con las instalaciones de MongoMK, ya que mejora considerablemente el tiempo de reindexación al colocar el contenido del repositorio en un archivo plano local. Sin embargo, requiere espacio adicional en disco de doble del tamaño del repositorio.

En el caso de MongoMK, este proceso puede acelerarse si este paso se ejecuta en una instancia más cercana a la instancia de MongoDB. Si se ejecuta en el mismo equipo, se puede evitar la sobrecarga de red.

Encontrará más detalles técnicos en la [documentación de ejecución de roble para indexar](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html).

### Importación de índices {#importing-indexes}

Con AEM versión 6.4 y versiones posteriores, AEM tiene la capacidad integrada de importar índices desde el disco en la secuencia de inicio. La carpeta `<repository>/indexing-result/indexes` está vigilada por la presencia de datos de índice durante el inicio. Puede copiar el índice precreado en la ubicación anterior durante el [proceso de actualización](in-place-upgrade.md#performing-the-upgrade) antes de comenzar con la nueva versión de la carpeta **destinatario** AEM. AEM lo importa en el repositorio y quita el punto de control correspondiente del sistema. Por lo tanto, se evita completamente un reíndice.

## Sugerencias adicionales y resolución de problemas {#troubleshooting}

A continuación encontrará algunos consejos útiles e instrucciones para la resolución de problemas.

### Reducir el impacto en el sistema de producción en directo {#reduce-the-impact-on-the-live-production-system}

Se recomienda clonar el sistema de producción y crear el índice sin conexión mediante el clon. Esto elimina cualquier impacto potencial en el sistema de producción. Sin embargo, el punto de comprobación necesario para importar el índice debe estar presente en el sistema de producción. Por lo tanto, es fundamental crear un punto de comprobación antes de tomar el clon.

### Preparar un Runbook y una ejecución de prueba {#prepare-a-runbook-and-trial-run}

Se recomienda preparar un runbook [](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/upgrade-planning.html#building-the-upgrade-and-rollback-runbook) y realizar algunas pruebas antes de ejecutar la actualización en producción.

### Modo de recorrido de documento con indización sin conexión {#doc-traversal-mode-with-offline-indexing}

La indexación sin conexión requiere múltiples transmisiones de todo el repositorio. Con las instalaciones de MongoMK, se accede al repositorio a través de la red que afecta al rendimiento del proceso de indexación. Una opción es ejecutar el proceso de indexación sin conexión en la réplica MongoDB misma, lo que eliminará la sobrecarga de red. Otra opción es el uso del modo doc-versal.

El modo de recorrido Doc se puede aplicar agregando el parámetro de línea de comandos `—doc-traversal` al comando oak-run para la indexación sin conexión. Este modo convierte una copia de todo el repositorio del disco local en un archivo plano y lo utiliza para ejecutar la indexación.
