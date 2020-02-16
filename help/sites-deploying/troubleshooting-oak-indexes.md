---
title: Resolución de problemas con los índices Oak
seo-title: Resolución de problemas con los índices Oak
description: Cómo detectar y corregir la reindexación lenta.
seo-description: Cómo detectar y corregir la reindexación lenta.
uuid: 6567ddae-128c-4302-b7e8-8befa66b1f43
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: ea70758f-6726-4634-bfb4-a957187baef0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Resolución de problemas con los índices Oak{#troubleshooting-oak-indexes}

## Reindexación lenta {#slow-re-indexing}

El proceso de reindexación interna de AEM recopila datos del repositorio y los almacena en índices Oak para admitir la consulta de contenido por parte del rendimiento. En circunstancias excepcionales, el proceso puede llegar a ser lento o incluso atascado. Esta página sirve como guía de solución de problemas para identificar si la indexación es lenta, encontrar la causa y resolver el problema.

Es importante distinguir entre volver a indexar que lleva una cantidad de tiempo inapropiadamente larga y volver a indexar que lleva mucho tiempo porque está indexando grandes cantidades de contenido. Por ejemplo, el tiempo que lleva indexar el contenido se escala con la cantidad de contenido, por lo que los repositorios de producción grandes tardarán más en volver a indexarse que los repositorios de desarrollo pequeños.

Consulte las [Prácticas recomendadas en consultas e indexación](/help/sites-deploying/best-practices-for-queries-and-indexing.md) para obtener información adicional sobre cuándo y cómo volver a indexar el contenido.

## Detección inicial {#initial-detection}

La detección inicial de la indexación lenta requiere la revisión de los MBeans de `IndexStats` JMX. En la instancia de AEM afectada, haga lo siguiente:

1. Abra la consola web y haga clic en la ficha JMX o vaya a https://&lt;host>:&lt;puerto>/system/console/jmx (por ejemplo, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)).
1. Navegue hasta los `IndexStats` Mbeans.
1. Abra los `IndexStats` MBeans para &quot; `async`&quot; y &quot; `fulltext-async`&quot;.

1. Para ambos MBeans, compruebe si la marca de tiempo **Listo** y la marca de tiempo **LastIndexTime** son inferiores a 45 minutos desde la hora actual.

1. Para MBean, si el valor de tiempo (**Listo** o **ÚltimoTiempoIndexado**) es mayor que 45 minutos a partir del tiempo actual, el trabajo de índice está fallando o tardando demasiado. Esto hace que los índices asincrónicos estén antiguos.

## La indización se pone en pausa después de un cierre forzado {#indexing-is-paused-after-a-forced-shutdown}

Un apagado forzado hace que AEM suspenda la indexación asincrónica hasta 30 minutos después del reinicio y generalmente requiere otros 15 minutos para completar la primera pasada de reindexación, durante un total de aproximadamente 45 minutos (volviendo al intervalo de tiempo de detección [](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection) inicial de 45 minutos). En el caso de que sospeche que la indexación se pone en pausa después de un cierre forzado:

1. En primer lugar, determine si la instancia de AEM se cerró de forma forzada (el proceso de AEM se mató a la fuerza o se produjo una falla eléctrica) y posteriormente se reinició.

   * [El registro](/help/sites-deploying/configure-logging.md) de AEM se puede revisar con este fin.

1. Si se produce el apagado forzoso, al reiniciar, AEM suspende automáticamente la reindexación durante un máximo de 30 minutos.
1. Espere aproximadamente 45 minutos para que AEM reanude las operaciones normales de indexación asincrónica.

## Grupo de subprocesos sobrecargado {#thread-pool-overloaded}

>[!NOTE]
>
>Para AEM 6.1, asegúrese de que está instalado [AEM 6.1 CFP 11](https://helpx.adobe.com/experience-manager/release-notes-aem-6-1-cumulative-fix-pack.html) .

En circunstancias excepcionales, el grupo de subprocesos utilizado para administrar la indexación asincrónica puede sobrecargarse. Para aislar el proceso de indexación, se puede configurar un grupo de subprocesos para evitar que otro trabajo de AEM interfiera con la capacidad de Oak de indexar contenido de manera oportuna. Para ello, debe:

1. Defina un nuevo grupo de subprocesos aislado para Apache Sling Scheduler para utilizarlo en la indexación asincrónica:

   * En la instancia de AEM afectada, vaya a AEM OSGi Web Console>OSGi>Configuration>Apache Sling Scheduler o vaya a https://&lt;host>:&lt;puerto>/system/console/configMgr (por ejemplo, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))
   * Agregue una entrada al campo &quot;Pools de subprocesos permitidos&quot; con el valor &quot;roak&quot;.
   * Haga clic en Guardar en la parte inferior derecha para guardar los cambios.
   ![chlimage_1-119](assets/chlimage_1-119.png)

1. Compruebe que el nuevo grupo de subprocesos de Apache Sling Scheduler esté registrado y se muestre en la consola web Apache Sling Scheduler Status (Estado del programador de Sling de Apache).

   * Vaya a la consola web de AEM OSGi>Estado>Programador de sling o vaya a https://&lt;host>:&lt;puerto>/system/console/status-slingprogramler (por ejemplo, [http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler))
   * Compruebe que existen las siguientes entradas de grupo:

      * ApacheSlingoak
      * ApacheSlingdefault
   ![chlimage_1-120](assets/chlimage_1-120.png)

## La cola de observación está llena {#observation-queue-is-full}

Si se realizan demasiados cambios y confirmaciones en el repositorio en poco tiempo, la indexación puede retrasarse debido a una cola de observación completa. En primer lugar, determine si la cola de observación está llena:

1. Vaya a la consola web y haga clic en la ficha JMX o vaya a https://&lt;host>:&lt;puerto>/system/console/jmx (por ejemplo, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
1. Abra el MBean Estadísticas del repositorio de Oak y determine si algún `ObservationQueueMaxLength` valor es mayor que 10.000.

   * En las operaciones normales, este valor máximo siempre debe reducirse eventualmente a cero (especialmente en la `per second` sección) para verificar que las métricas `ObservationQueueMaxLength`de segundos de Omniture sean 0.
   * Si los valores son 10.000 o más y aumentan de forma constante, esto indica que al menos una (posiblemente más) cola no se puede procesar tan rápido como se produzcan nuevos cambios (confirmaciones).
   * Cada cola de observación tiene un límite (10.000 de forma predeterminada) y si la cola alcanza ese límite, su procesamiento se degrada.
   * Cuando se utiliza MongoMK, a medida que la longitud de la cola crece, el rendimiento interno de la memoria caché Oak se degrada. Esta correlación se puede ver en un aumento `missRate` para la `DocChildren` caché en el MBean de `Consolidated Cache` estadísticas.

1. Para evitar superar los límites aceptables de las colas de observación, se recomienda:

   * Reduzca la velocidad constante de confirmaciones. Los picos cortos en los compromisos son aceptables, pero la tasa constante debe reducirse.
   * Aumente el tamaño del `DiffCache` archivo tal como se describe en Consejos de ajuste de [rendimiento > Ajuste de almacenamiento de mongog > Tamaño](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html#main-pars_text_3)de caché de documento.

## Identificación y corrección de un proceso de re-indexación atascado {#identifying-and-remediating-a-stuck-re-indexing-process}

La reindexación puede considerarse &quot;completamente atascada&quot; bajo dos condiciones:

* La reindexación es muy lenta, hasta el punto de que no se informa de ningún progreso significativo en los archivos de registro con respecto al número de nodos recorridos.

   * Por ejemplo, si no hay mensajes a lo largo de una hora o si el progreso es tan lento que tardará una semana o más en terminar.

* La reindexación está atascada en un bucle infinito si aparecen excepciones repetidas en los archivos de registro (por ejemplo, `OutOfMemoryException`) en el subproceso de indexación. La repetición de las mismas excepciones en el registro indica que Oak intenta indexar la misma cosa repetidamente, pero falla en el mismo problema.

Para identificar y corregir un proceso de reindexación atascado, haga lo siguiente:

1. Para identificar la causa de la indexación atascada, debe recopilarse la siguiente información:

   * Recopile 5 minutos de volcado de subproceso, un volcado de subproceso cada 2 segundos.
   * [Defina el nivel de DEBUG y los registros para los anexadores](/help/sites-deploying/configure-logging.md).

      * *org.apache.jackrabbit.oak.plugins.index.AsyncIndexUpdate*
      * *org.apache.jackrabbit.oak.plugins.index.IndexUpdate*
   * Recopilar datos del `IndexStats` MB asincrónico:

      * Vaya a AEM OSGi Web Console>Main>JMX>IndexStat>async

         o vaya a [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats)
   * Utilice el modo [de consola de](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) oak-run.jar para recopilar los detalles de lo que existe bajo el nodo * `/:async`*.
   * Recopile una lista de puntos de comprobación del repositorio utilizando el `CheckpointManager` MBean:

      * AEM OSGi Web Console>Main>JMX>CheckpointManager>listCheckpoints()

         o vaya a [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager)



1. Después de recopilar toda la información descrita en el paso 1, reinicie AEM.

   * Reiniciar AEM puede resolver el problema en el caso de una carga simultánea alta (desbordamiento de la cola de observación o algo similar).
   * Si un reinicio no resuelve el problema, abra un problema con el Servicio de atención al cliente de [Adobe](https://helpx.adobe.com/marketing-cloud/contact-support.html) y proporcione toda la información recopilada en el paso 1.

## Anulación segura de la reindexación asincrónica {#safely-aborting-asynchronous-re-indexing}

La reindexación puede anularse de forma segura (detenerse antes de completarse) a través de los carriles `async, async-reindex`y f `ulltext-async` de indexación ( `IndexStats` grano). Para obtener más información, consulte también la documentación de Apache Oak sobre [Cómo Abortar el Reindexado](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex). Además, tenga en cuenta que:

* La reindexación de los índices de propiedades Lucene y Lucene puede anularse ya que son naturalmente asíncronos.
* La reindexación de los índices de propiedades Oak solo se puede anular si se ha iniciado la reindexación mediante el `PropertyIndexAsyncReindexMBean`.

Para anular la reindexación de forma segura, siga estos pasos:

1. Identifique el MBean de IndexStats que controla el carril de reindexación que debe detenerse.

   * Vaya al MBean de IndexStats adecuado a través de la consola JMX, ya sea a AEM OSGi Web Console>Main>JMX o https://&lt;host>:&lt;puerto>/system/console/jmx (por ejemplo, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
   * Abra el MBean de IndexStats en función del carril de reindexación que desee detener ( `async`, `async-reindex`o `fulltext-async`)

      * Para identificar la ruta adecuada y, por lo tanto, la instancia MBean de IndexStats, consulte la propiedad &quot;async&quot; de los índices Oak. La propiedad &quot;async&quot; contendrá el nombre del carril: `async`, `async-reindex`o `fulltext-async`.
      * La ruta también está disponible accediendo al Administrador de índices de AEM en la columna &quot;Async&quot;. Para acceder al administrador de índices, vaya a Operaciones>Diagnóstico>Administrador de índices.
   ![chlimage_1-121](assets/chlimage_1-121.png)

1. Invoque el `abortAndPause()` comando en el `IndexStats` MBean correspondiente.
1. Marque la definición del índice Oak correctamente para evitar que se reanude la reindexación cuando se reanude el carril de indexación.

   * Al volver a indexar un índice **existente** , establezca la propiedad reindex en false

      * `/oak:index/someExistingIndex@reindex=false`
   * O bien, para un **nuevo** índice:

      * Definir la propiedad type como disabled

         * `/oak:index/someNewIndex@type=disabled`
      * o eliminar por completo la definición del índice
   Transmita los cambios al repositorio cuando se hayan completado.

1. Finalmente, reanude la indexación asíncrona en el carril de indexación anulado.

   * En el `IndexStats` MBean que emitió el `abortAndPause()` comando en el Paso 2, invoque el `resume()`comando.

## Prevención de la reindexación lenta {#preventing-slow-re-indexing}

Es mejor volver a indexar durante períodos silenciosos (por ejemplo, no durante una ingesta de contenido grande) y, de forma ideal, durante las ventanas de mantenimiento, cuando se conoce y controla la carga de AEM. Además, asegúrese de que la reindexación no se produce durante otras actividades de mantenimiento.
