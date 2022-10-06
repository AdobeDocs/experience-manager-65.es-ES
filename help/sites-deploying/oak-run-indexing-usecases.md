---
title: Casos de uso de indexación de Oak-run.jar
seo-title: Oak-run.jar Indexing Use Cases
description: Obtenga información sobre los distintos casos de usuario para realizar la indexación con la herramienta Oak-run.
seo-description: Learn about the various user cases for performing indexing with the Oak-run tool.
uuid: 3c50080d-1e0d-4886-8d37-269f06881eb4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 084075b8-826d-4f27-9342-35f33368f24f
noindex: true
exl-id: d25e3070-080a-4594-8fdb-9f09164135fc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 0%

---

# Casos de uso de indexación de Oak-run.jar{#oak-run-jar-indexing-use-cases}

Oak-run admite la indexación de casos de uso en la línea de comandos sin tener que orquestar la ejecución de estos casos de uso a través de AEM consola JMX.

Los beneficios generales de utilizar el método de comando de índice oak-run.jar para administrar índices Oak son:

1. El comando de índice Oak-run proporciona un nuevo conjunto de herramientas de indexación para AEM 6.4.
1. Oak-run disminuye el tiempo de reindexación, lo que reduce los tiempos de reindexación en repositorios más grandes.
1. Oak-run reduce el consumo de recursos durante la reindexación en AEM, lo que resulta en un mejor rendimiento general del sistema.
1. Oak-run proporciona reindexación fuera de banda, soporta situaciones en las que la producción debe estar disponible y no puede tolerar el mantenimiento o el downtime que de otra manera se requiere para reindexar.

Las secciones siguientes proporcionarían comandos de ejemplo. el comando oak-run index es compatible con todas las configuraciones de NodeStore y BlobStore. Los ejemplos que se proporcionan a continuación se refieren a configuraciones que tienen FileDataStore y SegmentNodeStore.

## Caso de uso 1 - Comprobación de coherencia del índice {#usercase1indexconsistencycheck}

Este es un caso de uso relacionado con la corrupción de índices. En algunos casos no era posible determinar cuál de los índices está corrupto. Por lo tanto, el Adobe ha proporcionado herramientas que:

1. Realiza comprobaciones de coherencia de índices en todos los índices y proporciona un informe en el que los índices son válidos y no son válidos;
1. La herramienta se puede utilizar aunque no AEM accesible;
1. Es fácil de usar.

La comprobación de índices dañados se puede realizar mediante `--index-consistency-check` operación:

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

Esto generará un informe en `indexing-result/index-consistency-check-report.txt`. Consulte a continuación un informe de muestra:

```
Valid indexes :
        - /content/oak:index/enablementResourceName
        - /oak:index/cqProjectLucene
        - /oak:index/cqTagLucene
        - /oak:index/lucene
        - /oak:index/ntBaseLucene
        - /oak:index/socialLucene
    Invalid indexes :
        - /oak:index/atDamIndex
        - /oak:index/atIndex
        - /oak:index/cqPageLucene
        - /oak:index/damAssetLucene
        - /oak:index/groups
        - /oak:index/slingeventJob
        - /oak:index/users
        - /oak:index/workflowDataLucene
    Ignored indexes as these are not of type lucene:
        - /oak:index/acPrincipalName
        - /oak:index/active
```

### Ventajas {#uc1benefits}

La asistencia técnica y el administrador del sistema ahora pueden usar esta herramienta para determinar rápidamente qué índices están dañados y luego reindexarlos.

## Caso de uso 2: Estadísticas de índice {#usecase2indexstatistics}

Para diagnosticar algunos de los casos relacionados con el Adobe de rendimiento de consultas a menudo requerían una definición de índice existente, las estadísticas relacionadas con el índice de la configuración del cliente. Hasta ahora, esta información se ha distribuido entre varios recursos. Para facilitar la resolución de problemas, Adobe ha creado herramientas que:

1. Volcar toda la definición de índice presente en el sistema en un solo archivo JSON;

1. Volcar estadísticas importantes de índices existentes;

1. Volcar el contenido del índice para el análisis sin conexión;

1. Se puede utilizar incluso si no se puede acceder a AEM

Las operaciones anteriores ahora se pueden realizar a través de los siguientes comandos de índice de operación:

* `--index-info` - Recopila y genera varias estadísticas relacionadas con los índices

* `--index-definitions` - Recopila y volca definiciones de índice

* `--index-dump` : descarga el contenido del índice

Vea a continuación un ejemplo de cómo funcionan los comandos en la práctica:

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

Los informes se generarían en `indexing-result/index-info.txt` y `indexing-result/index-definitions.json`

Además, se proporcionan los mismos detalles a través de la consola web y formarían parte del zip de volcado de configuración. Se puede acceder a ellas en la siguiente ubicación:

`https://serverhost:serverport/system/console/status-oak-index-defn`

### Ventajas {#uc2benefits}

Esta herramienta permite reunir rápidamente todos los detalles requeridos relacionados con problemas de indexación o consulta y reducir el tiempo empleado en extraer esta información.

## Caso de uso 3 - Reindexación {#usecase3reindexing}

Según el [escenarios](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing), en algunos casos es necesario realizar la reindexación. Actualmente, la reindexación se realiza configurando la variable `reindex` marcar como `true` en el nodo de definición de índice a través de CRXDE o a través de la interfaz de usuario del Administrador de índices. Una vez establecido el indicador, la reindexación se realiza asincrónicamente.

Algunos puntos a tener en cuenta en torno a la reindexación:

* La reindexación es mucho más lenta en `DocumentNodeStore` configuraciones comparadas con `SegmentNodeStore` configuraciones en las que todo el contenido es local;

* Con el diseño actual, mientras que la reindexación sucede, el indexador asíncrono se bloquea y todos los demás índices asíncronos se quedan antiguos y no se actualizan durante la indexación. Por ello, si el sistema está en uso, es posible que los usuarios no vean resultados actualizados;
* La reindexación implica la inversión de todo el repositorio, lo que puede suponer una carga elevada en la configuración de la AEM y, por tanto, afectar a la experiencia del usuario final;
* Para un `DocumentNodeStore` instalación en la que la reindexación puede tardar un tiempo considerable, si la conexión a la base de datos de Mongo falla en mitad de la operación, la indexación tendría que reiniciarse desde cero;

* En algunos casos, la reindexación puede llevar mucho tiempo debido a la extracción de texto. Esto es principalmente específico para configuraciones que tienen muchos archivos de PDF, donde el tiempo empleado en la extracción de texto puede afectar al tiempo de indexación.

Para alcanzar estos objetivos, la herramienta de indexación oak-run soporta diferentes modos de reindexación que pueden ser utilizados como sea necesario. El comando oak-run index proporciona las siguientes ventajas:

* **reindexación fuera de banda** - la reindexación de oak-run se puede hacer por separado de una configuración de AEM en ejecución y, por lo tanto, minimiza el impacto en la instancia de AEM que está en uso;

* **reindexación fuera de línea** - La reindexación tiene lugar sin afectar a las operaciones de indexación. Esto significa que el indizador asíncrono puede seguir indexando otros índices;

* **Reindexación simplificada para instalaciones de DocumentNodeStore** - Para `DocumentNodeStore` instalaciones, la reindexación puede realizarse con un único comando que garantice que la reindexación se realiza de la manera más óptima;

* **Admite la actualización de definiciones de índice e introduce nuevas definiciones de índice**

### Reindex - DocumentNodeStore {#reindexdocumentnodestore}

Para `DocumentNodeStore` instalaciones la reindexación se puede realizar mediante un único comando oak-run:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

Esto ofrece las siguientes ventajas

* Impacto mínimo en la ejecución de instancias de AEM. La mayoría de las lecturas se pueden realizar desde servidores secundarios y la ejecución de cachés AEM no se ve afectada de forma adversa debido a toda la travesía necesaria para la reindexación;
* Los usuarios también pueden proporcionar un JSON de un índice nuevo o actualizado a través de la variable `--index-definitions-file` .

### Reindex - SegmentNodeStore {#reindexsegmentnodestore}

Para `SegmentNodeStore` las instalaciones de reindexación se pueden realizar de una de las siguientes maneras:

#### Reindex en línea: SegmentNodeStore {#onlinereindexsegmentnodestore}

Siga la manera establecida en la que la reindexación se realiza mediante la configuración `reindex` indicador.

#### Reindex en línea - SegmentNodeStore - La instancia de AEM se está ejecutando {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

Para `SegmentNodeStore` instalaciones solo un proceso puede acceder a los archivos de segmentos en modo de lectura-escritura. Debido a esto, algunas operaciones en la indexación de oak-run requieren pasos manuales adicionales.

Esto implicaría lo siguiente:

1. Texto del paso
1. Conecte el `oak-run` al mismo repositorio utilizado por AEM en modo de solo lectura y realizar la indexación. Un ejemplo de cómo conseguirlo:

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. Finalmente, importe los archivos de índice creados a través de la variable `IndexerMBean#importIndex` operación desde la ruta donde oak-run guardó los archivos de indexación después de ejecutar el comando anterior.

En esta situación no es necesario detener el servidor de AEM ni aprovisionar ninguna instancia nueva. Sin embargo, como la indexación implica la inversión de todo el repositorio, aumentaría la carga de E/S en la instalación, afectando negativamente al rendimiento del tiempo de ejecución.

#### Reindex en línea - SegmentNodeStore - La instancia de AEM está desactivada {#onlinereindexsegmentnodestoreaeminstanceisdown}

Para `SegmentNodeStore` las instalaciones de reindexación se pueden realizar mediante un único comando oak-run. Sin embargo, la instancia de AEM debe cerrarse.

Se puede déclencheur la reindexación con el siguiente comando:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

La diferencia entre este enfoque y el explicado anteriormente es que la creación de puntos de comprobación y la importación de índices se realizan automáticamente. El inconveniente es que AEM debe estar inactivo durante el proceso.

#### Reindex fuera de banda - SegmentNodeStore {#outofbandreindexsegmentnodestore}

En este caso de uso, puede realizar la reindexación en una configuración clonada para minimizar el impacto en la instancia de AEM en ejecución:

1. Cree un punto de comprobación mediante una operación JMX. Para ello, vaya a la [Consola JMX](/help/sites-administering/jmx-console.md) y busque `CheckpointManager`. A continuación, haga clic en el **createCheckpoint(long p1)** operación con un valor alto para la caducidad en segundos (por ejemplo, **2592000**).
1. Copie el `crx-quickstart` carpeta en un equipo nuevo
1. Reindexar mediante el comando de índice oak-run

1. Copiar los archivos de índice generados en AEM servidor

1. Importe los archivos de índice a través de JMX.

En este caso de uso, se da por hecho que el almacén de datos es accesible en otra instancia, lo que puede no ser posible si `FileDataStore` se ubica en una solución de almacenamiento basada en la nube como EBS. Esto excluye el escenario donde `FileDataStore` también está clonado. Si la definición del índice no realiza la indexación de texto completo, acceda a `DataStore` no es obligatorio.

## Caso de uso 4: Actualización de las definiciones de índice {#usecase4updatingindexdefinitions}

Actualmente, puede enviar cambios en la definición del índice mediante [ACS Asegúrese de que el índice](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) paquete. Esto permite enviar las definiciones de índice a través del paquete de contenido que posteriormente requiere que la reindexación se realice configurando la variable `reindex` marcar como `true`.

Esto funciona bien en instalaciones más pequeñas donde la reindexación no lleva mucho tiempo. Sin embargo, para repositorios muy grandes, la reindexación se realizará en una cantidad de tiempo considerablemente mayor. Para estos casos ahora podemos usar las herramientas de índice oak-run.

Oak-run ahora admite proporcionar definiciones de índice en formato JSON y la creación de índice en modo fuera de banda donde no se realizan cambios en una instancia activa.

El proceso que debe tener en cuenta para este caso de uso es:

1. Un desarrollador actualizaría las definiciones de índice en una instancia local y luego generaría un archivo JSON de definición de índice a través del `--index-definitions` option

1. A continuación, el JSON actualizado se proporciona al administrador del sistema
1. El administrador del sistema sigue el enfoque fuera de banda y prepara el índice en una instalación diferente
1. Una vez finalizado, los archivos de índice generados se importarán en una instalación AEM en ejecución.
