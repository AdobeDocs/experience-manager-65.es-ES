---
title: Solución de problemas de índices Oak
description: Obtenga información sobre cómo identificar si la indexación es lenta, encontrar la causa y resolver el problema.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 85981463-189c-4f50-9d21-1d2f734b960a
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 1%

---

# Solución de problemas de índices Oak{#troubleshooting-oak-indexes}

## Reindexación lenta  {#slow-re-indexing}

AEM El proceso de reindexación interno de recopila datos del repositorio y los almacena en índices Oak para admitir la consulta de contenido con rendimiento. En circunstancias excepcionales, el proceso puede ralentizarse o incluso atascarse. Esta página actúa como una guía de solución de problemas para identificar si la indexación es lenta, encontrar la causa y resolver el problema.

Es importante distinguir entre una reindexación que lleva una cantidad de tiempo inapropiadamente larga y una reindexación que lleva una cantidad de tiempo larga porque está indexando grandes cantidades de contenido. Por ejemplo, el tiempo que se tarda en indexar el contenido se escala con la cantidad de contenido, por lo que los repositorios de producción grandes tardan más en reindexarse que los pequeños.

Consulte la [Prácticas recomendadas en consultas e indexación](/help/sites-deploying/best-practices-for-queries-and-indexing.md) para obtener información adicional sobre cuándo y cómo reindexar contenido.

## Detección inicial {#initial-detection}

Detección inicial La indexación lenta requiere la revisión de la `IndexStats` MBeans de JMX. AEM En la instancia de afectada, haga lo siguiente:

1. Abra la consola web y haga clic en la pestaña JMX o vaya a https://&lt;host>:&lt;port>/system/console/jmx (por ejemplo, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)).
1. Vaya a `IndexStats` Mbeans.
1. Abra el `IndexStats` MBeans para &quot; `async`&quot; y &quot; `fulltext-async`&quot;.

1. Para ambos MBean, compruebe si la variable **Listo** marca de tiempo y **LastIndexTime** La marca de tiempo es inferior a 45 minutos desde la hora actual.

1. Para MBean, si el valor de tiempo (**Listo** o **LastIndexedTime**) tiene más de 45 minutos desde el momento actual, por lo que el trabajo de indexación está fallando o tardando demasiado. Este problema hace que los índices asíncronos estén obsoletos.

## La indexación se detiene después de un cierre forzado {#indexing-is-paused-after-a-forced-shutdown}

AEM Un apagado forzado resulta en la suspensión de la indexación asíncrona durante un máximo de 30 minutos después del reinicio de la aplicación. Y, por lo general, se requieren otros 15 minutos para completar el primer pase de reindexación, para un total de aproximadamente 45 minutos (vinculando de nuevo con el [Detección inicial](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection) un periodo de tiempo de 45 minutos). Si la indexación está en pausa después de un apagado forzado:

1. AEM AEM En primer lugar, determine si la instancia de la se apagó de forma forzada (el proceso de la se cerró a la fuerza o se produjo un fallo de alimentación) y, a continuación, reinicie.

   * [AEM tala de](/help/sites-deploying/configure-logging.md) puede revisarse para este fin.

1. AEM Si se produce el apagado forzado, al reiniciar, la reindexación se suspende automáticamente durante un máximo de 30 minutos.
1. AEM Espere aproximadamente 45 minutos para que los usuarios reanuden las operaciones normales de indexación asíncrona.

## Grupo de subprocesos sobrecargado {#thread-pool-overloaded}

>[!NOTE]
>
>AEM Para la versión 6.1, asegúrese de que [AEM.1 CFP 11](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=es) está instalado.

En circunstancias excepcionales, el grupo de subprocesos utilizado para administrar la indexación asincrónica puede sobrecargarse. AEM Para aislar el proceso de indexación, se puede configurar un grupo de hilos para evitar que otro trabajo interfiera con la capacidad de Oak de indexar contenido de manera oportuna. En estos casos, haga lo siguiente:

1. Defina un nuevo grupo de hilos aislado para el planificador de Apache Sling que se utilizará para la indexación asíncrona:

   * AEM AEM En la instancia de afectada, vaya a Consola web OSGi de OSGi>Configuración>Planificador de Apache Sling o vaya a https://&lt;host>:&lt;port>/system/console/configMgr (por ejemplo, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))
   * Agregue una entrada al campo &quot;Grupos de hilos permitidos&quot; con el valor &quot;oak&quot;.
   * Para guardar los cambios, haga clic en **Guardar** en la parte inferior derecha.

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. Compruebe que el nuevo grupo de hilos del Planificador de Apache Sling esté registrado y se muestre en la consola web Estado del planificador de Apache Sling.

   * AEM Vaya a la consola web de OSGi de la interfaz de usuario de la barra de herramientas de la interfaz de usuario de OSGi>Status>Sling Scheduler o a https://&lt;host>:&lt;port>/system/console/status-slingscheduler (por ejemplo, [http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler))
   * Compruebe que existen las siguientes entradas de grupo:

      * ApacheSlingoak
      * ApacheSlingdefault

   ![chlimage_1-120](assets/chlimage_1-120.png)

## La cola de observación está llena {#observation-queue-is-full}

Si se realizan demasiados cambios y confirmaciones en el repositorio en un corto período de tiempo, la indexación se puede retrasar debido a una cola de observación completa. En primer lugar, determine si la cola de observación está llena:

1. Vaya a la consola web y haga clic en la pestaña JMX o vaya a https://&lt;host>:&lt;port>/system/console/jmx (por ejemplo, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
1. Abra el MBean Estadísticas del repositorio de Oak y determine si hay alguna `ObservationQueueMaxLength` el valor es mayor que 10 000.

   * En operaciones normales, este valor máximo siempre debe reducirse finalmente a cero (especialmente en el `per second` ), de modo que compruebe que las `ObservationQueueMaxLength`Las métricas de segundos de son 0.
   * Si los valores son 10 000 o más y aumentan de forma constante, indica que al menos una cola (posiblemente más) no se puede procesar tan rápido como se producen nuevos cambios (confirmaciones).
   * Cada cola de observación tiene un límite (10 000 de forma predeterminada) y, si la cola alcanza ese límite, se degrada su procesamiento.
   * Al utilizar MongoMK, a medida que la longitud de la cola crece, el rendimiento interno de la caché de Oak se degrada. Esta correlación se puede ver en un aumento de `missRate` para el `DocChildren` caché en `Consolidated Cache` MBean de estadísticas.

1. Para evitar superar los límites aceptables de la cola de observación, se recomienda:

   * Reduzca la tasa constante de confirmaciones. Los picos cortos en las confirmaciones son aceptables, pero la tasa constante debe reducirse.
   * Aumentar el tamaño del `DiffCache` como se describe en [Consejos de rendimiento > Ajuste del almacenamiento Mongo > Tamaño de la caché del documento](/help/sites-deploying/configuring-performance.md).

## Identificación y corrección de un proceso de reindexación bloqueado {#identifying-and-remediating-a-stuck-re-indexing-process}

La reindexación se puede considerar &quot;completamente atascada&quot; bajo dos condiciones:

* La reindexación es lenta, hasta el punto de que no se informa de ningún progreso significativo en los archivos de registro con respecto al número de nodos atravesados.

   * Por ejemplo, si no hay mensajes en el transcurso de una hora o si el progreso es tan lento que tarda una semana o más en finalizar.

* La reindexación se queda atascada en un bucle interminable si aparecen excepciones repetidas en los archivos de registro (por ejemplo, `OutOfMemoryException`) en el hilo de indexación. La repetición de una o más excepciones iguales en el registro indica que Oak intenta indexar lo mismo repetidamente, pero falla en el mismo problema.

Para identificar y corregir un proceso de reindexación atascado, haga lo siguiente:

1. Para identificar la causa de la indexación atascada, se debe recopilar la siguiente información:

   * Recopile 5 minutos del volcado de hilos, un volcado de hilos cada 2 segundos.
   * [Establecer el nivel de depuración y los registros para los anexadores](/help/sites-deploying/configure-logging.md).

      * *org.apache.jackrabbit.oak.plugins.index.AsyncIndexUpdate*
      * *org.apache.jackrabbit.oak.plugins.index.IndexUpdate*

   * Recopilación de datos de la lista asíncrona `IndexStats` MBean:

      * AEM Vaya a Consola web de OSGi>Principal>JMX>IndexStat>asíncrona.

        o vaya a [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats)

   * Uso [modo de consola de oak-run.jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) para recopilar los detalles de lo que existe en * `/:async`* nodo.
   * Recopile una lista de puntos de comprobación del repositorio mediante el `CheckpointManager` MBean:

      * AEM OSGi Web Console>Main>JMX>CheckpointManager>listCheckpoints()

        o vaya a [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager)

1. AEM Después de recopilar toda la información descrita en el paso 1, reinicie el proceso de.

   * AEM El reinicio de la puede resolver el problema si hay una carga simultánea alta (desbordamiento de la cola de observación o algo similar).
   * Si un reinicio no resuelve el problema, abra un problema con [Adobe del Servicio de atención al cliente](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home&amp;lang=es#support) y proporcionar toda la información recopilada en el paso 1.

## Anulación segura de la reindexación asíncrona {#safely-aborting-asynchronous-re-indexing}

La reindexación se puede cancelar de forma segura (se detiene antes de que se complete) mediante el `async, async-reindex`y f `ulltext-async` rutas de indexación ( `IndexStats` Mbean). Para obtener más información, consulte también la documentación de Apache Oak sobre [Cómo abortar la reindexación](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex). Además, tenga en cuenta lo siguiente:

* La reindexación de los índices de propiedades Lucene y Lucene se puede cancelar porque son asíncronos por naturaleza.
* La reindexación de los índices de propiedades de Oak solo se puede cancelar si la reindexación se ha iniciado a través de `PropertyIndexAsyncReindexMBean`.

Para anular la reindexación de forma segura, siga estos pasos:

1. Identifique el MBean IndexStats que controla el carril de reindexación que debe detenerse.

   * AEM Vaya al MBean de IndexStats adecuado a través de la consola JMX en OSGi Web Console>Main>JMX o https://.&lt;host>:&lt;port>/system/console/jmx (por ejemplo, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
   * Abra el MBean IndexStats en función de la ruta de reindexación que desee detener ( `async`, `async-reindex`, o `fulltext-async`)

      * Para identificar el carril adecuado y, por lo tanto, la instancia de MBean IndexStats, observe la propiedad &quot;async&quot; de Oak Indexes. La propiedad &quot;async&quot; contiene el nombre de la ruta: `async`, `async-reindex`, o `fulltext-async`.
      * AEM El carril también está disponible accediendo al Administrador de índices de la sección &quot;Asíncrona&quot; de la barra de herramientas del Administrador de índices de la barra de herramientas. Para acceder al Administrador de índices, vaya a Operaciones>Diagnóstico>Administrador de índices.

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. Invoque el `abortAndPause()` en el adecuado `IndexStats` MBean.
1. Marque la definición de índice de Oak correctamente para evitar que se reanude la reindexación cuando se reanude la ruta de indexación.

   * Al reindexar un **existente** índice, establezca la propiedad reindex en false

      * `/oak:index/someExistingIndex@reindex=false`

   * O si no, por un **nuevo** index, ya sea:

      * Establezca la propiedad type como disabled

         * `/oak:index/someNewIndex@type=disabled`

      * o elimine la definición del índice por completo

   Confirme los cambios en el repositorio cuando se hayan completado.

1. Finalmente, reanude la indexación asíncrona en la ruta de indexación anulada.

   * En el `IndexStats` MBean que emitió el `abortAndPause()` en el paso 2, invoque el comando `resume()`comando.

## Prevención de la reindexación lenta {#preventing-slow-re-indexing}

AEM Es mejor reindexar durante periodos de silencio (por ejemplo, no durante una ingesta de contenido grande), e idealmente durante periodos de mantenimiento en los que se conoce y controla la carga de la. Además, asegúrese de que la reindexación no se produzca durante otras actividades de mantenimiento.
