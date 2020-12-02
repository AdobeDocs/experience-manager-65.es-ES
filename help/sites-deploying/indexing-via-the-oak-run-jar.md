---
title: Indexación a través del Jar de Oak-run
seo-title: Indexación a través del Jar de Oak-run
description: Aprenda a realizar la indexación a través del Jar de Oak-run.
seo-description: Aprenda a realizar la indexación a través del Jar de Oak-run.
uuid: 09a83ab9-92ec-4b55-8d24-2302f28fc2e4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: c8a505ab-a075-47da-8007-43645a8c3ce5
translation-type: tm+mt
source-git-commit: 3f53945579eaf5de1ed0b071aa9cce30dded89f1
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 0%

---


# Indexación mediante el Jar de ejecución de Oak {#indexing-via-the-oak-run-jar}

Oak-run admite todos los casos de uso de indexación en la línea de comandos sin tener que operar desde el nivel JMX. Las ventajas del método de roble son las siguientes:

1. Es un nuevo conjunto de herramientas de indexación para AEM 6.4
1. Disminuye el tiempo de reindexación, lo que beneficia los tiempos de reindexación en repositorios más grandes
1. Está reduciendo el consumo de recursos durante la reindexación en AEM, lo que mejora el rendimiento del sistema en otras actividades AEM
1. Oak-run ofrece compatibilidad fuera de banda: Si las condiciones de producción no permiten ejecutar el reíndice en instancias de producción, se puede usar un entorno clonado para volver a indexar a fin de evitar un impacto crítico en el rendimiento.

A continuación encontrará una lista de casos de uso que se pueden aprovechar al realizar operaciones de indexación mediante la herramienta `oak-run`.

## Comprobaciones de coherencia de índice {#indexconsistencychecks}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Caso de uso 1 - Comprobación de coherencia del índice](/help/sites-deploying/oak-run-indexing-usecases.md#usercase1indexconsistencycheck).

* `oak-run.jar`determina rápidamente si los índices de roble de lucene están dañados.
* Es seguro ejecutar en una instancia de AEM en uso para comprobar la coherencia de los niveles 1 y 2.

![screen_shot_2017-12-14at135758](assets/screen_shot_2017-12-14at135758.png)

## Estadísticas de índice {#indexstatistics}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Caso de uso 2 - Estadísticas de índice](/help/sites-deploying/oak-run-indexing-usecases.md#usecase2indexstatistics)

* `oak-run.jar` muestra todas las definiciones de índice, las estadísticas de índice importantes y el contenido de índice para la análisis sin conexión.
* Segura para ejecutarse en una instancia de AEM en uso.

![image2017-12-19_9-47-40](assets/image2017-12-19_9-47-40.png)

## Volver a indexar el árbol de decisiones del enfoque {#reindexingapproachdecisiontree}

Este diagrama es un árbol de decisiones para determinar cuándo utilizar los distintos enfoques de reindexación.

![oak_-_reindexingwithoak run](assets/oak_-_reindexingwithoak-run.png)

## Volver a indexar MongoMK / RDMBMK {#reindexingmongomk}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Caso de uso 3 - Reindexación](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing).

### Extracción previa de texto para SegmentNodeStore y DocumentNodeStore {#textpre-extraction}

[La extracción](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-perform-text-pre-extraction)  previa de texto (una función que existe con AEM 6.3) se puede utilizar para reducir el tiempo de reindexación. La extracción previa del texto se puede utilizar junto con todos los enfoques de reindexación.

Según el método de indexación `oak-run.jar`, habrá varios pasos a ambos lados del paso Realizar reindexación en el diagrama siguiente.

![4](assets/4.png)

>[!NOTE]
>
>Naranja indica actividades en las que AEM debe estar en una ventana de mantenimiento.

### Reindexación en línea para MongoMK o RDBMK usando oak-run.jar {#onlinere-indexingformongomk}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Reindex - DocumentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexdocumentnodestore).

Este es el método recomendado para el reindexado de las instalaciones AEM MongoMK (y RDBMK). No debe utilizarse ningún otro método.

Este proceso sólo debe ejecutarse con una sola instancia de AEM en el clúster.

![5](assets/5.png)

## Volver a indexar TarMK {#re-indexingtarmk}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Reindex - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexsegmentnodestore).

* **Consideraciones sobre el modo de espera en frío (TarMK)**

   * No hay ninguna consideración especial para el &quot;Cold Standby&quot;; las instancias de Cold Standby sincronizarán los cambios como de costumbre.

* **Granjas de AEM Publish (las granjas de AEM Publish siempre deben ser TarMK)**

   * Para el conjunto de servidores de publicación, es necesario hacerlo para todos O ejecutar los pasos en una sola publicación y, a continuación, clonar la configuración para otros (teniendo en cuenta todas las precauciones habituales al clonar instancias de AEM; sling.id - debería vincularse a algo aquí)

### Reindexación en línea para TarMK {#onlinere-indexingfortarmk}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Reíndice en línea - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestore).

Este es el método utilizado antes de la introducción de las nuevas capacidades de indexación de oak-run.jar. Puede hacerlo estableciendo la propiedad `reindex=true` en el índice Oak.

Este método se puede utilizar si el cliente acepta los efectos de rendimiento y tiempo que se van a indexar. Esto suele ocurrir en el caso de las instalaciones de AEM pequeñas y medianas.

![6](assets/6.png)

### TarMK de re-indexación en línea usando oak-run.jar {#onlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Reíndice en línea - SegmentNodeStore - La instancia de AEM se está ejecutando](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoretheaeminstanceisrunning).

El reindexado en línea de TarMK es más rápido que el reindexado en línea de TarkMK descrito arriba. Sin embargo, también requiere la ejecución durante una ventana de mantenimiento, con el método de que la ventana será más corta, y se necesitan más pasos para realizar la reindexación.

>[!NOTE]
>
>Naranja indica las operaciones en las que se deben realizar AEM en un período de mantenimiento.

![7](assets/7.png)

### TarMK de re-indexación sin conexión usando oak-run.jar {#offlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Reíndice en línea - SegmentNodeStore - La instancia de AEM está desactivada](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoreaeminstanceisdown).

La re-indexación sin conexión de TarMK es el método de re-indexación basado en `oak-run.jar` más sencillo para TarMK, ya que requiere un solo comentario `oak-run.jar`. Sin embargo, requiere que se cierre la instancia de AEM.

>[!NOTE]
>
>El rojo indica las operaciones en las que se debe cerrar AEM.

![8](assets/8.png)

### Reindexación fuera de banda TarMK usando oak-run.jar {#out-of-bandre-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Reíndice de fuera de banda - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#outofbandreindexsegmentnodestore).

La reindexación fuera de banda minimiza el impacto de la reindexación en las instancias de AEM en uso.

>[!NOTE]
>
>El rojo indica las operaciones en las que se pueden cerrar AEM.

![9](assets/9.png)

## Actualización de definiciones de indexación {#updatingindexingdefinitions}

>[!NOTE]
>
>Para obtener información más detallada sobre este escenario, consulte [Caso de uso 4 - Actualización de definiciones de índice](/help/sites-deploying/oak-run-indexing-usecases.md#usecase4updatingindexdefinitions).

### Creación y actualización de definiciones de índice en TarMK mediante ACS Asegurar índice {#creatingandupdatingindexdefinitionsontarmkusingacsensureindex}

>[!NOTE]
>
>ACS Asegúrese de que el índice sea un proyecto admitido por la comunidad y no sea compatible con la asistencia de Adobe.

Esto permite enviar la definición del índice mediante el paquete de contenido, lo que posteriormente resulta en una reindexación mediante la configuración del indicador de reindexación en `true`. Esto funciona para configuraciones más pequeñas donde el reindexado no lleva mucho tiempo.

Para obtener más información, consulte la [documentación del índice de seguridad de ACS](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) para obtener más información.

### Creación y actualización de definiciones de índice en TarMK mediante oak-run.jar {#creatingandupdatingindexdefinitionsontarmkusingoak-run-jar}

Si el impacto en el tiempo o el performance del re-indexado mediante métodos que no sean `oak-run.jar` es demasiado alto, se puede utilizar el siguiente enfoque basado en `oak-run.jar` para importar y volver a indexar las definiciones del Índice Lucene en una instalación AEM basada en TarMK.

![10](assets/10.png)

### Creación y actualización de definiciones de índice en MonogMK usando oak-run.jar {#creatingandupdatingindexdefinitionsonmonogmkusingoak-run-jar}

Si el impacto en el tiempo o el performance del re-indexado mediante métodos que no sean `oak-run.jar` es demasiado alto, se puede utilizar el siguiente enfoque basado en `oak-run.jar` para importar y volver a indexar las definiciones del Índice Lucene en instalaciones de AEM basadas en MongoMK.

![11](assets/11.png)

