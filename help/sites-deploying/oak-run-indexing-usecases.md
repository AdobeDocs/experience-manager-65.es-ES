---
title: Casos de uso de indización de Oak-run.jar
seo-title: Casos de uso de indización de Oak-run.jar
description: Obtenga información sobre los distintos casos de usuarios para realizar indexaciones con la herramienta Oak-run.
seo-description: Obtenga información sobre los distintos casos de usuarios para realizar indexaciones con la herramienta Oak-run.
uuid: 3c50080d-1e0d-4886-8d37-269f06881eb4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 084075b8-826d-4f27-9342-35f33368f24f
noindex: true
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1392'
ht-degree: 0%

---


# Casos de uso de indización de Oak-run.jar{#oak-run-jar-indexing-use-cases}

Oak-run admite la indexación de casos de uso en la línea de comandos sin tener que orquestar la ejecución de estos casos de uso a través de AEM consola JMX.

Los beneficios generales de utilizar el método de comando de índice oak-run.jar para administrar índices Oak son:

1. El comando de índice Oak-run proporciona un nuevo conjunto de herramientas de indexación para AEM 6.4.
1. La ejecución de Oak disminuye el tiempo de reindexación, lo que reduce los tiempos de reindexación en repositorios más grandes.
1. La ejecución de Oak reduce el consumo de recursos durante la reindexación en AEM, lo que resulta en un mejor rendimiento general del sistema.
1. Oak-run proporciona reindexación fuera de banda, soporta situaciones en las que la producción debe estar disponible y no puede tolerar el mantenimiento o el tiempo de inactividad que, de lo contrario, se requiere para volver a indexar.

Las secciones siguientes proporcionan comandos de ejemplo. el comando de índice de ejecución de Oak admite todas las configuraciones de NodeStore y BlobStore. Los ejemplos que se proporcionan a continuación se refieren a las configuraciones que tienen FileDataStore y SegmentNodeStore.

## Caso de uso 1 - Comprobación de coherencia de índice {#usercase1indexconsistencycheck}

Se trata de un caso de uso relacionado con la corrupción de índices. En algunos casos no fue posible determinar cuáles de los índices están corruptos. Por lo tanto, el Adobe ha proporcionado herramientas que:

1. Realiza comprobaciones de coherencia del índice en todos los índices y proporciona un informe en el que los índices son válidos y no son válidos;
1. La herramienta se puede utilizar incluso si no se puede acceder a la AEM;
1. Es fácil de usar.

La comprobación de índices dañados se puede realizar mediante la operación `--index-consistency-check`:

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

### Beneficios {#uc1benefits}

La asistencia técnica y el administrador del sistema pueden utilizar esta herramienta para determinar rápidamente qué índices están dañados y luego volver a indexarlos.

## Caso de uso 2 - Estadísticas de índice {#usecase2indexstatistics}

Para diagnosticar algunos de los casos relacionados con el Adobe de rendimiento de consulta, a menudo se requiere una definición de índice existente, las estadísticas relacionadas con el índice de la configuración del cliente. Hasta ahora, esta información se ha dispersado en varios recursos. Para facilitar la solución de problemas, Adobe ha creado herramientas que:

1. Volcar toda la definición de índice presente en el sistema en un solo archivo JSON;

1. Retirar estadísticas importantes de índices existentes;

1. Volcar el contenido del índice para la análisis sin conexión;

1. Se podrá utilizar incluso si no se puede acceder a AEM

Las operaciones anteriores ahora se pueden realizar mediante los siguientes comandos de índice de operaciones:

* `--index-info` - Recopila y extrae diversas estadísticas relacionadas con los índices

* `--index-definitions` - Recopila y genera definiciones de índice

* `--index-dump` - Voltea el contenido del índice

Vea a continuación un ejemplo de cómo funcionan los comandos en la práctica:

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

Los informes se generarían en `indexing-result/index-info.txt` y `indexing-result/index-definitions.json`

Además, los mismos detalles se proporcionan a través de la consola web y formarían parte del zip de volcado de configuración. Se puede acceder a ellos en la siguiente ubicación:

`https://serverhost:serverport/system/console/status-oak-index-defn`

### Beneficios {#uc2benefits}

Esta herramienta permite recopilar rápidamente todos los detalles necesarios relacionados con problemas de indexación o consulta y reducir el tiempo empleado en extraer esta información.

## Caso de uso 3 - Reindexación {#usecase3reindexing}

Según los [escenarios](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing), en algunos casos es necesario volver a indexar. Actualmente, el reindexado se realiza estableciendo el indicador `reindex` en `true` en el nodo de definición de índice mediante CRXDE o mediante la interfaz de usuario del Administrador de índices. Una vez configurado el indicador, el reindexado se realiza de forma asíncrona.

Algunos puntos a destacar en torno al reindexado:

* La reindexación es mucho más lenta en las configuraciones `DocumentNodeStore` que en las configuraciones `SegmentNodeStore` donde todo el contenido es local;

* Con el diseño actual, mientras se produce el reindexado asíncrono, el indizador se bloquea y todos los demás índices asíncronos se quedan antiguos y no se actualizan mientras dure la indexación. Debido a esto, si el sistema está en uso, es posible que los usuarios no vean los resultados actualizados;
* La reindexación implica la inversión de todo el repositorio, lo que puede poner una carga elevada en la configuración de la AEM y, por tanto, afectar a la experiencia del usuario final;
* Para una instalación `DocumentNodeStore` en la que el reindexado puede tardar bastante tiempo, si la conexión a la base de datos de Mongo falla en medio de la operación, la indexación tendría que reiniciarse desde cero;

* En algunos casos, el reindexado puede llevar mucho tiempo debido a la extracción del texto. Esto es especialmente específico para configuraciones que tienen muchos archivos PDF, donde el tiempo empleado en la extracción de texto puede afectar al tiempo de indexación.

Para alcanzar estos objetivos, la herramienta de indexación de roble admite diferentes modos de reindexación que pueden utilizarse según sea necesario. El comando oak-run index proporciona las siguientes ventajas:

* **el reindexado fuera de banda**  puede realizarse por separado de una configuración de AEM en marcha y, por tanto, minimiza el impacto en la instancia de AEM que se está utilizando;

* **reindexación**  fuera de carril: el reindexado se lleva a cabo sin afectar a las operaciones de indexación. Esto significa que el indizador asincrónico puede seguir indexando otros índices;

* **Reindexación simplificada de las instalaciones**  de DocumentNodeStore: en el caso de  `DocumentNodeStore` las instalaciones, el reindexado se puede realizar con un único comando que garantice que el reindexado se realiza de la manera más óptima posible;

* **Es compatible con la actualización de definiciones de índice y la introducción de nuevas definiciones de índice**

### Reindex - DocumentNodeStore {#reindexdocumentnodestore}

Para las instalaciones `DocumentNodeStore` la reindexación se puede realizar mediante un único comando de ejecución de roble:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

Esto proporciona los siguientes beneficios

* Impacto mínimo en la ejecución de instancias de AEM. La mayoría de las lecturas se pueden realizar desde servidores secundarios y la ejecución de memorias caché AEM no se ve afectada de forma adversa debido a todo el recorrido necesario para el reindexado;
* Los usuarios también pueden proporcionar un JSON de un índice nuevo o actualizado mediante la opción `--index-definitions-file`.

### Reindex - SegmentNodeStore {#reindexsegmentnodestore}

Para las instalaciones `SegmentNodeStore` el reindexado se puede realizar de una de las siguientes maneras:

#### Reíndice en línea - SegmentNodeStore {#onlinereindexsegmentnodestore}

Siga la manera establecida en la que el reindexado se realiza mediante el indicador `reindex`.

#### Reíndice en línea - SegmentNodeStore - La instancia de AEM se está ejecutando {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

Para las instalaciones `SegmentNodeStore` sólo un proceso puede acceder a los archivos de segmentos en modo de lectura y escritura. Debido a esto, algunas operaciones de indexación en roble requieren pasos manuales adicionales.

Esto implicaría lo siguiente:

1. Texto del paso
1. Conecte el `oak-run` al mismo repositorio utilizado por AEM en modo de solo lectura y realice la indexación. Un ejemplo de cómo lograr esto:

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. Por último, importe los archivos de índice creados mediante la operación `IndexerMBean#importIndex` desde la ruta de acceso donde oak-run guardó los archivos de indexación después de ejecutar el comando anterior.

En este escenario no es necesario detener el servidor de AEM ni aprovisionar ninguna instancia nueva. Sin embargo, dado que la indexación implica la inversión de todo el repositorio, aumentaría la carga de E/S en la instalación, afectando negativamente el rendimiento del tiempo de ejecución.

#### Reindexación en línea - SegmentNodeStore - La instancia de AEM se cierra {#onlinereindexsegmentnodestoreaeminstanceisdown}

Para las instalaciones `SegmentNodeStore` el reindexado se puede realizar mediante un único comando de ejecución de roble. Sin embargo, la instancia de AEM debe cerrarse.

Puede activar la reindexación con el siguiente comando:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

La diferencia entre este enfoque y el explicado anteriormente es que la creación de puntos de comprobación y la importación de índices se realizan automáticamente. La desventaja es que AEM debe estar inoperativo durante el proceso.

#### Reíndice de fuera de banda - SegmentNodeStore {#outofbandreindexsegmentnodestore}

En este caso de uso, puede realizar reindexación en una configuración clonada para minimizar el impacto en la instancia de AEM en ejecución:

1. Cree un punto de comprobación mediante una operación JMX. Para ello, vaya a la [Consola JMX](/help/sites-administering/jmx-console.md) y busque `CheckpointManager`. A continuación, haga clic en la operación **createCheckpoint(long p1)** utilizando un valor alto para la caducidad en segundos (por ejemplo, **2592000**).
1. Copiar la carpeta `crx-quickstart` en un equipo nuevo
1. Realizar reindexación mediante el comando de índice oak-run

1. Copiar los archivos de índice generados en AEM servidor

1. Importe los archivos de índice mediante JMX.

En este caso de uso, se da por hecho que el Almacén de datos es accesible en otra instancia, lo cual puede no ser posible si `FileDataStore` se coloca en una solución de almacenamiento basada en la nube como EBS. Esto excluye el escenario en el que `FileDataStore` también está clonado. Si la definición de índice no realiza la indexación de texto completo, no se requiere el acceso a `DataStore`.

## Caso de uso 4 - Actualización de definiciones de índice {#usecase4updatingindexdefinitions}

Actualmente, puede enviar cambios en la definición del índice mediante el paquete [ACS Asegúrese de que el índice](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html). Esto permite el envío de las definiciones de índice a través de un paquete de contenido que posteriormente requiere que el reindexado se realice estableciendo el indicador `reindex` en `true`.

Esto funciona bien en instalaciones más pequeñas donde el reindexado no lleva mucho tiempo. Sin embargo, para repositorios muy grandes, el reindexado se realizará en una cantidad de tiempo considerablemente mayor. En estos casos, ahora podemos utilizar la herramienta de indexación de roble.

Oak-run ahora admite la provisión de definiciones de índice en formato JSON y la creación de índice en modo fuera de banda donde no se realizan cambios en una instancia activa.

El proceso que debe tener en cuenta para este caso de uso es:

1. Un desarrollador actualizaría las definiciones de índice en una instancia local y luego generaría un archivo JSON de definición de índice mediante la opción `--index-definitions`

1. El JSON actualizado se proporciona al administrador del sistema
1. System Administrator sigue el enfoque fuera de banda y prepara el índice en una instalación diferente
1. Una vez finalizado, los archivos de índice generados se importarán en una instalación AEM en ejecución.

