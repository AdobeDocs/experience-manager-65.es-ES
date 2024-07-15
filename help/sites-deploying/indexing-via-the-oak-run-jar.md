---
title: Indexación mediante el Jar ejecutado por Oak
description: Aprenda a realizar la indexación mediante el Jar ejecutado en Oak.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: dcec8c1b-13cc-486c-b1a4-62e6eb3184ad
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# Indexación mediante el Jar ejecutado por Oak {#indexing-via-the-oak-run-jar}

Oak-run admite todos los casos de uso de indexación en la línea de comandos sin tener que operar desde el nivel JMX. Las ventajas del enfoque oak-run son:

1. AEM Es un nuevo conjunto de herramientas de indexación para la versión 6.4 de
1. Reduce el tiempo de reindexación, lo que afecta positivamente a los tiempos de reindexación en repositorios más grandes
1. AEM AEM Está reduciendo el consumo de recursos durante la reindexación en la, lo que mejora el rendimiento del sistema para otras actividades de la
1. La ejecución de Oak proporciona compatibilidad fuera de banda: Si las condiciones de producción no permiten ejecutar reindexaciones en instancias de producción, se puede utilizar un entorno clonado para la reindexación a fin de evitar un impacto crítico en el rendimiento.

A continuación se muestra una lista de casos de uso que se pueden utilizar al realizar operaciones de indexación mediante la herramienta `oak-run`.

## Comprobaciones de coherencia de índice {#indexconsistencychecks}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Caso de uso 1 - Comprobación de coherencia del índice](/help/sites-deploying/oak-run-indexing-usecases.md#usercase1indexconsistencycheck).

* `oak-run.jar` determina rápidamente si los índices de Lucene Oak están dañados.
* AEM Es seguro ejecutarse en una instancia de prueba en uso para los niveles de comprobación de coherencia 1 y 201000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000

![Comprobaciones de coherencia del índice](assets/screen_shot_2017-12-14at135758.png)

## Estadísticas de índice {#indexstatistics}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Caso de uso 2 - Estadísticas de índice](/help/sites-deploying/oak-run-indexing-usecases.md#usecase2indexstatistics)

* `oak-run.jar` elimina todas las definiciones de índice, las estadísticas de índice importantes y el contenido de índice para el análisis sin conexión.
* AEM Es seguro ejecutarlo en una instancia en uso de la aplicación de seguridad de la aplicación de seguridad de la aplicación de seguridad

![image2017-12-19_9-47-40](assets/image2017-12-19_9-47-40.png)

## Árbol de decisión de método de reindexación {#reindexingapproachdecisiontree}

Este diagrama es un árbol de decisión para saber cuándo utilizar los distintos métodos de reindexación.

![oak_-_reindexingwithoak-run](assets/oak_-_reindexingwithoak-run.png)

## Reindexación de MongoMK/RDMBMK {#reindexingmongomk}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Caso de uso 3 - Reindexación](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing).

### Extracción previa de texto para SegmentNodeStore y DocumentNodeStore {#textpre-extraction}

AEM [La extracción previa de texto](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-perform-text-pre-extraction) (una característica que ya existe con la versión 6.3) se puede usar para reducir el tiempo de reindexación. La preextracción de texto se puede utilizar con todos los enfoques de reindexación.

Dependiendo del método de indexación `oak-run.jar`, hay varios pasos a cada lado del paso Realizar reindexación en el diagrama siguiente.

![Extracción previa de texto para SegmentNodeStore y DocumentNodeStore](assets/4.png)

>[!NOTE]
>
>AEM Naranja indica las actividades en las que debe estar en una ventana de mantenimiento.

### Reindexación en línea para MongoMK o RDBMK con oak-run.jar {#onlinere-indexingformongomk}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, vea [Reindex: DocumentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexdocumentnodestore).

AEM Este es el método recomendado para reindexar instalaciones de MongoMK (y RDBMK) en el mercado de la distribución de datos (RDBMK). No se debe utilizar ningún otro método.

AEM Ejecute este proceso sólo con una instancia de la instancia de la instancia de la instancia de la base de datos del clúster.

![Reindexación en línea para MongoMK o RDBMK mediante oak-run.jar](assets/5.png)

## Reindexación de TarMK {#re-indexingtarmk}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Reindexar: SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexsegmentnodestore).

* **Consideraciones de espera en frío (TarMK)**

   * No hay consideraciones especiales para el modo de espera en frío; las instancias de espera en frío se sincronizan como de costumbre.

* AEM **granjas de Publish (las granjas de Publish de AEM siempre deben ser TarMK)**

   * Para la granja de servidores de publicación, debe realizarse para todos los pasos O ejecutar en una sola publicación. AEM A continuación, clone la configuración para otros (tomando todas las precauciones habituales al clonar instancias de; sling.id: debe vincularse a algo aquí).

### Reindexación en línea para TarMK {#onlinere-indexingfortarmk}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Reindexación en línea: SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestore).

Este es el método utilizado antes de la introducción de las nuevas capacidades de indexación de oak-run.jar. Se realiza estableciendo la propiedad `reindex=true` en el índice Oak.

Este método se puede utilizar si el cliente acepta los efectos de tiempo y rendimiento que se van a indexar. AEM Este suele ser el caso de las instalaciones de pequeñas y medianas dimensiones en el sector de la.

![Reindexación en línea para TarMK](assets/6.png)

### Reindexación en línea de TarMK con oak-run.jar {#onlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>AEM Para obtener información más detallada sobre este escenario, consulte [Reindexación en línea - SegmentNodeStore - La instancia de la se está ejecutando](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoretheaeminstanceisrunning).

La reindexación en línea de TarMK usando oak-run.jar es más rápida que la [reindexación en línea para TarMK](#onlinere-indexingfortarmk) descrita anteriormente. Sin embargo, también requiere ejecución durante una ventana de mantenimiento; con la mención de que la ventana es más corta y se requieren más pasos para realizar la reindexación.

>[!NOTE]
>
>AEM Naranja indica las operaciones en las que se debe realizar la operación en un período de mantenimiento.

![Reindexación en línea de TarMK con oak-run.jar](assets/7.png)

### Volver a indexar TarMK sin conexión mediante oak-run.jar {#offlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>AEM Para obtener información más detallada sobre este escenario, consulte [Reindexación en línea - SegmentNodeStore - La instancia de la se ha cerrado](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoreaeminstanceisdown).

La reindexación sin conexión de TarMK es el método de reindexación basado en `oak-run.jar` más sencillo para TarMK, ya que requiere un solo comentario `oak-run.jar`. AEM Sin embargo, requiere que se cierre la instancia de.

>[!NOTE]
>
>AEM Rojo indica las operaciones en las que debe cerrarse el servicio de la.

![Volver a indexar TarMK sin conexión usando oak-run.jar](assets/8.png)

### TarMK de reindexación fuera de banda con oak-run.jar  {#out-of-bandre-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Reindexación fuera de banda - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#outofbandreindexsegmentnodestore).

AEM La reindexación fuera de banda minimiza el impacto de la reindexación en las instancias de en uso.

>[!NOTE]
>
>AEM Rojo indica las operaciones en las que se pueden cerrar los puntos de conexión de los.

![Reindexación fuera de banda de TarMK usando oak-run.jar](assets/9.png)

## Actualización de definiciones de indexación {#updatingindexingdefinitions}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Caso de uso 4 - Actualización de definiciones de índice](/help/sites-deploying/oak-run-indexing-usecases.md#usecase4updatingindexdefinitions).

### Crear y actualizar definiciones de índice en TarMK usando ACS {#creatingandupdatingindexdefinitionsontarmkusingacsensureindex}

>[!NOTE]
>
>ACS Asegúrese de que el índice sea un proyecto compatible con la comunidad y no con la asistencia del Adobe.

Esto permite la definición del índice de envío a través del paquete de contenido, lo que posteriormente resulta en una reindexación a través de la configuración del indicador de reindexación en `true`. Esto funciona en configuraciones más pequeñas en las que la reindexación no tarda mucho tiempo.

Para obtener más información, consulte la [Documentación sobre el índice seguro de ACS](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) para obtener más detalles.

### Creación y actualización de definiciones de índice en TarMK mediante oak-run.jar {#creatingandupdatingindexdefinitionsontarmkusingoak-run-jar}

AEM Si el tiempo o el impacto en el rendimiento de la reindexación mediante métodos que no son `oak-run.jar` es demasiado elevado, se puede utilizar el siguiente enfoque basado en `oak-run.jar` para importar y reindexar definiciones de índice de Lucene en una instalación basada en TarMK, que se basa en el código de tiempo de la instalación de la base de datos de la base de datos de la base de.

![Creación y actualización de definiciones de índice en TarMK mediante oak-run.jar](assets/10.png)

### Creación y actualización de definiciones de índice en MonogMK con oak-run.jar {#creatingandupdatingindexdefinitionsonmonogmkusingoak-run-jar}

AEM Si el tiempo o el impacto en el rendimiento de la reindexación mediante métodos que no son `oak-run.jar` es demasiado alto, se puede utilizar el siguiente enfoque basado en `oak-run.jar` para importar y reindexar definiciones de índice Lucene en instalaciones basadas en MongoMK, según el índice de Lucene.

![Creación y actualización de definiciones de índice en MonogMK mediante oak-run.jar](assets/11.png)
