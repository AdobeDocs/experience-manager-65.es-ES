---
title: Indexación mediante el Jar de Oak-run
seo-title: Indexing via the Oak-run Jar
description: Aprenda a realizar la indexación mediante el Jar de Oak-run.
seo-description: Learn how to perform indexing via the Oak-run Jar.
uuid: 09a83ab9-92ec-4b55-8d24-2302f28fc2e4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: c8a505ab-a075-47da-8007-43645a8c3ce5
exl-id: dcec8c1b-13cc-486c-b1a4-62e6eb3184ad
source-git-commit: c61bf629e35db848c3f2f88c6c7e1dd3b7074b1c
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%

---

# Indexación mediante el Jar de Oak-run {#indexing-via-the-oak-run-jar}

Oak-run admite todos los casos de uso de indexación en la línea de comandos sin tener que operar desde el nivel JMX. Las ventajas del enfoque oak-run son:

1. AEM Es un nuevo conjunto de herramientas de indexación para la versión 6.4 de
1. Reduce el tiempo de reindexación, lo que afecta negativamente a los tiempos de reindexación en repositorios más grandes
1. AEM AEM Está reduciendo el consumo de recursos durante la reindexación, lo que da como resultado un mejor rendimiento del sistema para otras actividades de la
1. Oak-run proporciona compatibilidad fuera de banda: Si las condiciones de producción no permiten ejecutar un reíndice en instancias de producción, se puede utilizar un entorno clonado para la reindexación a fin de evitar un impacto crítico en el rendimiento.

A continuación, encontrará una lista de casos de uso que se pueden aprovechar al realizar operaciones de indexación a través de la `oak-run` herramienta.

## Comprobaciones de coherencia de índice {#indexconsistencychecks}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Caso de uso 1: Comprobación de la coherencia del índice](/help/sites-deploying/oak-run-indexing-usecases.md#usercase1indexconsistencycheck).

* `oak-run.jar`determina rápidamente si los índices de Lucene oak están dañados.
* AEM Es seguro ejecutarse en una instancia de prueba en uso para los niveles de comprobación de coherencia 1 y 2.

![Comprobaciones de coherencia de índice](assets/screen_shot_2017-12-14at135758.png)

## Estadísticas de índice {#indexstatistics}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Caso de uso 2: Estadísticas de índice](/help/sites-deploying/oak-run-indexing-usecases.md#usecase2indexstatistics)

* `oak-run.jar` elimina todas las definiciones de índice, las estadísticas de índice importantes y el contenido de índice para el análisis sin conexión.
* AEM Es seguro ejecutarlo en una instancia en uso de la aplicación de seguridad de la aplicación de seguridad de la aplicación de seguridad

![image2017-12-19_9-47-40](assets/image2017-12-19_9-47-40.png)

## Árbol de decisión de método de reindexación {#reindexingapproachdecisiontree}

Este diagrama es un árbol de decisión para saber cuándo utilizar los distintos métodos de reindexación.

![oak_-_reindexingwithoak-run](assets/oak_-_reindexingwithoak-run.png)

## Reindexación de MongoMK/RDMBMK {#reindexingmongomk}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Caso de uso 3: Reindexación](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing).

### Extracción previa de texto para SegmentNodeStore y DocumentNodeStore {#textpre-extraction}

[Preextracción de texto](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-perform-text-pre-extraction) AEM (una función que ha existido con la versión 6.3 de) se puede utilizar para reducir el tiempo de reindexación. La preextracción de texto se puede utilizar junto con todos los enfoques de reindexación.

Según la variable `oak-run.jar` enfoque de indexación habrá varios pasos a cada lado del paso Realizar reindexación en el diagrama siguiente.

![Extracción previa de texto para SegmentNodeStore y DocumentNodeStore](assets/4.png)

>[!NOTE]
>
>AEM Naranja indica las actividades en las que debe estar en una ventana de mantenimiento.

### Reindexación en línea para MongoMK o RDBMK con oak-run.jar {#onlinere-indexingformongomk}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Reindexar: DocumentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexdocumentnodestore).

AEM Este es el método recomendado para volver a indexar instalaciones de MongoMK (y RDBMK) en el mercado de la distribución de datos (RDBMK). No se debe utilizar ningún otro método.

AEM Este proceso sólo debe ejecutarse con una única instancia de en el clúster.

![Reindexación en línea para MongoMK o RDBMK con oak-run.jar](assets/5.png)

## Reindexación de TarMK {#re-indexingtarmk}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Reindexar: SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexsegmentnodestore).

* **Consideraciones sobre el modo de espera en frío (TarMK)**

   * No hay ninguna consideración especial para el modo de espera en frío; las instancias de modo de espera en frío sincronizarán los cambios de la forma habitual.

* **Publicar granjas AEM (las granjas de publicación AEM siempre deben ser TarMK)**

   * AEM Para la granja de servidores de publicación, debe hacerse para todos los pasos de O ejecutar en una sola publicación y luego clonar la configuración para otros (tomando todas las precauciones habituales al clonar instancias de; sling.id - debe vincularse a algo aquí)

### Reindexación en línea para TarMK {#onlinere-indexingfortarmk}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Reindexación en línea - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestore).

Este es el método utilizado antes de la introducción de las nuevas capacidades de indexación de oak-run.jar. Se puede hacer configurando la variable `reindex=true` en el índice Oak.

Este método se puede utilizar si el cliente acepta los efectos de tiempo y rendimiento que se van a indexar. AEM Este suele ser el caso de las instalaciones de pequeñas y medianas dimensiones en el sector de la.

![Reindexación en línea para TarMK](assets/6.png)

### Reindexación en línea de TarMK con oak-run.jar {#onlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [AEM Reindexación en línea - SegmentNodeStore - Se está ejecutando la instancia de la](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoretheaeminstanceisrunning).

La reindexación en línea de TarMK con oak-run.jar es más rápida que la [Reindexación en línea para TarMK](#onlinere-indexingfortarmk) descrito anteriormente. Sin embargo, también requiere ejecución durante una ventana de mantenimiento; con la mención de que la ventana será más corta y se requieren más pasos para realizar la reindexación.

>[!NOTE]
>
>AEM Naranja indica las operaciones en las que se debe realizar la operación en un período de mantenimiento.

![Reindexación en línea de TarMK con oak-run.jar](assets/7.png)

### Volver a indexar TarMK sin conexión mediante oak-run.jar {#offlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [AEM Reindexación en línea - SegmentNodeStore - Se cierra la instancia de la](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoreaeminstanceisdown).

La reindexación sin conexión de TarMK es la más sencilla `oak-run.jar` basado en un enfoque de reindexación para TarMK, ya que requiere un único `oak-run.jar` comentario. AEM Sin embargo, requiere que se cierre la instancia de.

>[!NOTE]
>
>AEM Rojo indica las operaciones en las que debe cerrarse el servicio de la.

![Volver a indexar TarMK sin conexión mediante oak-run.jar](assets/8.png)

### TarMK de reindexación fuera de banda con oak-run.jar  {#out-of-bandre-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Reindexación fuera de banda: SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#outofbandreindexsegmentnodestore).

AEM La reindexación fuera de banda minimiza el impacto de la reindexación en las instancias de en uso.

>[!NOTE]
>
>AEM Rojo indica las operaciones en las que se pueden cerrar los puntos de conexión de los.

![TarMK de reindexación fuera de banda con oak-run.jar](assets/9.png)

## Actualización de definiciones de indexación {#updatingindexingdefinitions}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Caso de uso 4: Actualización de definiciones de índice](/help/sites-deploying/oak-run-indexing-usecases.md#usecase4updatingindexdefinitions).

### Crear y actualizar definiciones de índice en TarMK usando ACS {#creatingandupdatingindexdefinitionsontarmkusingacsensureindex}

>[!NOTE]
>
>ACS Asegúrese de que el índice sea un proyecto compatible con la comunidad y no con el soporte de Adobe.

Esto permite la definición del índice de envío mediante el paquete de contenido, lo que posteriormente resulta en una reindexación mediante la configuración del indicador de reindexación en `true`. Esto funciona para configuraciones más pequeñas en las que la reindexación no tarda mucho tiempo.

Para obtener más información, consulte la [Documentación de índice seguro de ACS](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) para obtener más información.

### Creación y actualización de definiciones de índice en TarMK mediante oak-run.jar {#creatingandupdatingindexdefinitionsontarmkusingoak-run-jar}

Si el tiempo o el impacto en el rendimiento de la reindexación mediante no `oak-run.jar` métodos es demasiado alto, los siguientes `oak-run.jar` AEM Este método basado en puede utilizarse para importar y reindexar definiciones de índice de Lucene en una instalación basada en TarMK de la base de la base de datos de la base de datos de la base de datos de.

![Creación y actualización de definiciones de índice en TarMK mediante oak-run.jar](assets/10.png)

### Creación y actualización de definiciones de índice en MonogMK con oak-run.jar {#creatingandupdatingindexdefinitionsonmonogmkusingoak-run-jar}

Si el tiempo o el impacto en el rendimiento de la reindexación mediante no `oak-run.jar` métodos es demasiado alto, los siguientes `oak-run.jar` AEM Este método basado en puede utilizarse para importar y reindexar definiciones de índice de Lucene en instalaciones basadas en MongoMK, en el que se utilizan diferentes tipos de instalaciones basadas en el índice de Lucene.

![Creación y actualización de definiciones de índice en MonogMK con oak-run.jar](assets/11.png)
