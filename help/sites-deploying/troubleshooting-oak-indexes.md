---
title: Resolución de problemas de índices Oak
seo-title: Troubleshooting Oak Indexes
description: Detección y corrección de la reindexación lenta.
uuid: 6567ddae-128c-4302-b7e8-8befa66b1f43
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: ea70758f-6726-4634-bfb4-a957187baef0
exl-id: 85981463-189c-4f50-9d21-1d2f734b960a
source-git-commit: 9defa6d1843007e9375d839f72f6993c691a37c0
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 1%

---

# Resolución de problemas de índices Oak{#troubleshooting-oak-indexes}

## Reindexación lenta  {#slow-re-indexing}

AEM proceso de reindexación interna recopila datos del repositorio y los almacena en los índices Oak para admitir la consulta del contenido de forma más eficaz. En circunstancias excepcionales, el proceso puede llegar a ser lento o incluso atascado. Esta página actúa como guía de solución de problemas para ayudar a identificar si la indexación es lenta, encontrar la causa y resolver el problema.

Es importante distinguir entre la reindexación que lleva una cantidad de tiempo inapropiadamente larga y la reindexación que lleva mucho tiempo porque está indexando grandes cantidades de contenido. Por ejemplo, el tiempo que se tarda en indexar el contenido escala con la cantidad de contenido, por lo que los repositorios de producción grandes tardan más en reindexarse que los repositorios de desarrollo pequeños.

Consulte la [Prácticas recomendadas en consultas e indexación](/help/sites-deploying/best-practices-for-queries-and-indexing.md) para obtener información adicional sobre cuándo y cómo reindexar contenido.

## Detección inicial {#initial-detection}

La detección inicial de la indexación lenta requiere la revisión de la variable `IndexStats` JMX MBeans. En la instancia de AEM afectada, haga lo siguiente:

1. Abra la consola web y haga clic en la pestaña JMX o vaya a https://&lt;host>:&lt;port>/system/console/jmx (por ejemplo, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)).
1. Vaya a la `IndexStats` Mbeans.
1. Abra el `IndexStats` MBeans para &quot; `async`&quot; y &quot; `fulltext-async`&quot;.

1. Para ambos MBeans, compruebe si la variable **Listo** timestamp y **LastIndexTime** la marca de tiempo es inferior a 45 minutos desde la hora actual.

1. Para cualquiera de los MBean, si el valor de tiempo (**Listo** o **LastIndexedTime**) es bueno a 45 minutos desde el momento actual, entonces el trabajo de índice está fallando o tardando demasiado. Este problema hace que los índices asíncronos estén obsoletos.

## La indexación se pone en pausa después de un cierre forzado {#indexing-is-paused-after-a-forced-shutdown}

Un cierre forzado provoca AEM suspensión de la indexación asincrónica durante un máximo de 30 minutos después del reinicio. Y, normalmente se necesitan otros 15 minutos para completar el primer pase de reindexación, durante un total de unos 45 minutos (volviendo al [Detección inicial](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection) periodo de tiempo de 45 minutos). Si la indexación se pone en pausa después de un cierre forzado:

1. En primer lugar, determine si la instancia de AEM se cerró de manera forzada (el proceso de AEM fue violado a la fuerza o si se produjo un fallo de energía) y luego se reinició.

   * [Registro de AEM](/help/sites-deploying/configure-logging.md) puede revisarse con este fin.

1. Si se produjo el cierre forzado, al reiniciar, AEM suspende automáticamente la reindexación durante un máximo de 30 minutos.
1. Espere aproximadamente 45 minutos para que la AEM reanude las operaciones de indexación asíncronas normales.

## Grupo de subprocesos sobrecargado {#thread-pool-overloaded}

>[!NOTE]
>
>Para AEM 6.1, asegúrese de que [AEM 6.1 CFP 11](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=es) está instalado.

En circunstancias excepcionales, el grupo de subprocesos utilizado para administrar la indexación asincrónica puede sobrecargarse. Para aislar el proceso de indexación, se puede configurar un grupo de subprocesos para evitar que otros trabajos de AEM interfieran con la capacidad de Oak de indexar contenido de manera oportuna. En estos casos, haga lo siguiente:

1. Defina un nuevo grupo de subprocesos aislado para el programador de Sling de Apache que se utilizará para la indexación asíncrona:

   * En la instancia de AEM afectada, vaya a AEM OSGi Web Console>OSGi>Configuration>Apache Sling Scheduler o vaya a https://&lt;host>:&lt;port>/system/console/configMgr (por ejemplo, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))
   * Agregue una entrada al campo &quot;Grupos de subprocesos permitidos&quot; con el valor &quot;roak&quot;.
   * Para guardar los cambios, haga clic en **Guardar** en la parte inferior derecha.

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. Compruebe que el nuevo grupo de subprocesos del programador de Sling de Apache esté registrado y se muestre en la consola web del estado del programador de Sling de Apache.

   * Vaya a la consola web OSGi de AEM > Estado > Programador de Sling o vaya a https://&lt;host>:&lt;port>/system/console/status-slingscheduler (por ejemplo, [http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler))
   * Compruebe que existen las siguientes entradas de grupo:

      * ApacheSlingoak
      * ApacheSlingdefault

   ![chlimage_1-120](assets/chlimage_1-120.png)

## La cola de observación está llena {#observation-queue-is-full}

Si se realizan demasiados cambios y confirmaciones en el repositorio en un corto periodo de tiempo, la indexación se puede retrasar debido a una cola de observación completa. En primer lugar, determine si la cola de observación está llena:

1. Vaya a la consola web y haga clic en la pestaña JMX o vaya a https://&lt;host>:&lt;port>/system/console/jmx (por ejemplo, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
1. Abra Oak Repository Statistics MBean y determine si existe `ObservationQueueMaxLength` es bueno que 10 000.

   * En las operaciones normales, este valor máximo siempre debe reducirse eventualmente a cero (especialmente en la variable `per second` (sección) para verificar que la variable `ObservationQueueMaxLength`Las métricas de segundos de son 0.
   * Si los valores son 10 000 o más y aumentan de forma constante, indica que al menos una cola (posiblemente más) no se puede procesar tan rápido como se produzcan nuevos cambios (confirmaciones).
   * Cada cola de observación tiene un límite (10 000 por defecto) y si la cola alcanza ese límite, su procesamiento se degrada.
   * Cuando se utiliza MongoMK, a medida que aumentan las longitudes de cola, se degrada el rendimiento interno de la caché de Oak. Esta correlación se puede ver en un aumento `missRate` para el `DocChildren` en el `Consolidated Cache` statistics MBean.

1. Para evitar superar los límites aceptables de las colas de observación, se recomienda:

   * Reduzca la velocidad constante de confirmaciones. Los picos cortos en confirmaciones son aceptables, pero la tasa constante debería reducirse.
   * Aumente el tamaño de la variable `DiffCache` tal como se describe en [Consejos de ajuste de rendimiento > Ajuste de almacenamiento Mongo > Tamaño de la caché del documento](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/configuring/configuring-performance.html?lang=en).

## Identificación y corrección de un proceso de reindexación atascado {#identifying-and-remediating-a-stuck-re-indexing-process}

La reindexación puede considerarse &quot;completamente atascada&quot; bajo dos condiciones:

* La reindexación es lenta, hasta el punto en que no se notifica ningún progreso significativo en los archivos de registro con respecto al número de nodos atravesados.

   * Por ejemplo, si no hay mensajes en el curso de una hora o si el progreso es tan lento que se tarda una semana o más en terminar.

* La reindexación está atascada en un bucle sin fin si aparecen excepciones repetidas en los archivos de registro (por ejemplo, `OutOfMemoryException`) en el subproceso de indexación. La repetición de una o más de las mismas excepciones en el registro, indica que Oak intenta indexar lo mismo repetidamente, pero falla en el mismo tema.

Para identificar y corregir un proceso de reindexación atascado, haga lo siguiente:

1. Para identificar la causa de la indexación atascada, se debe recopilar la siguiente información:

   * Recopile 5 minutos de volcado de subprocesos, un volcado de subprocesos cada 2 segundos.
   * [Establezca el nivel de depuración y los registros para los anexadores](/help/sites-deploying/configure-logging.md).

      * *org.apache.jackrabbit.oak.plugins.index.AsyncIndexUpdate*
      * *org.apache.jackrabbit.oak.plugins.index.IndexUpdate*
   * Recopilación de datos de async `IndexStats` MBean:

      * Vaya a AEM OSGi Web Console>Main>JMX>IndexStat>async

         o vaya a [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats)
   * Uso [modo de consola de oak-run.jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) para recopilar los detalles de lo que existe en el * `/:async`* nodo.
   * Recopile una lista de puntos de comprobación del repositorio utilizando el `CheckpointManager` MBean:

      * AEM OSGi Web Console>Principal>JMX>CheckpointManager>listCheckpoints()

         o vaya a [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager)



1. Después de recopilar toda la información descrita en el paso 1, reinicie AEM.

   * Reiniciar AEM puede resolver el problema si hay una carga simultánea alta (desbordamiento de la cola de observación o algo similar).
   * Si un reinicio no resuelve el problema, abra un problema con [Servicio de atención al cliente de Adobe](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home&amp;lang=es#support) y proporcionar toda la información recopilada en el paso 1.

## Anulación segura de la reindexación asíncrona {#safely-aborting-asynchronous-re-indexing}

La reindexación se puede abortar de forma segura (se detiene antes de completarse) mediante el método `async, async-reindex`y f `ulltext-async` rutas de indexación ( `IndexStats` Mbean). Para obtener más información, consulte también la documentación de Apache Oak sobre [Cómo evitar la reindexación](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex). Además, tenga en cuenta lo siguiente:

* La reindexación de los índices de propiedades de Lucene y Lucene se puede anular porque son asíncronos de forma natural.
* La reindexación de los índices de propiedades de Oak solo se puede anular si la reindexación se inició mediante la variable `PropertyIndexAsyncReindexMBean`.

Para anular la reindexación de forma segura, siga estos pasos:

1. Identifique el IndexStats MBean que controla el carril de reindexación que debe detenerse.

   * Vaya a la consola JMX de IndexStats MBean adecuada en AEM OSGi Web Console>Main>JMX o https://&lt;host>:&lt;port>/system/console/jmx (por ejemplo, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
   * Abra IndexStats MBean en función del carril de reindexación que desee detener ( `async`, `async-reindex`o `fulltext-async`)

      * Para identificar el carril apropiado y, por lo tanto, la instancia de IndexStats MBean, consulte la propiedad &quot;async&quot; de los índices Oak. La propiedad &quot;async&quot; contiene el nombre del carril: `async`, `async-reindex`o `fulltext-async`.
      * El carril también está disponible accediendo AEM Administrador de índices en la columna &quot;Sincronización&quot;. Para acceder al Administrador de índices, vaya a Operaciones > Diagnóstico > Administrador de índices.

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. Invocar el `abortAndPause()` en el `IndexStats` MBean.
1. Marque la definición del índice Oak adecuadamente para evitar reanudar la reindexación cuando se reanude el carril de indexación.

   * Al reindexar un **existente** index, establezca la propiedad reindex en false

      * `/oak:index/someExistingIndex@reindex=false`
   * O bien, para un **new** índice, ya sea:

      * Establezca la propiedad de tipo como deshabilitada

         * `/oak:index/someNewIndex@type=disabled`
      * o eliminar por completo la definición del índice

   Confirme los cambios en el repositorio cuando se completen.

1. Finalmente, reanude la indexación asíncrona en el carril de indexación anulado.

   * En el `IndexStats` MBean que emitió el `abortAndPause()` en el paso 2, invoque la función `resume()`comando.

## Prevención de la reindexación lenta {#preventing-slow-re-indexing}

Es mejor reindexar durante periodos silenciosos (por ejemplo, no durante una ingesta de contenido grande) e idealmente durante las ventanas de mantenimiento cuando AEM carga se conoce y controla. Además, asegúrese de que la reindexación no se lleve a cabo durante otras actividades de mantenimiento.
