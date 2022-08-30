---
title: Limpieza de revisión
seo-title: Revision Cleanup
description: Aprenda a utilizar la funcionalidad Limpieza de revisión de AEM 6.3.
seo-description: Learn how to use the Revision Cleanup functionality in AEM 6.3.
uuid: 321f5038-44b0-4f1e-a1aa-2d29074eed70
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: f03ebe60-88c0-4fc0-969f-949490a8e768
feature: Configuring
exl-id: e53c4c81-f62e-4b6d-929a-6649c8ced23c
source-git-commit: 550e7993f88367ec4b5c1d024dc742c087c1a9eb
workflow-type: tm+mt
source-wordcount: '5912'
ht-degree: 0%

---

# Limpieza de revisión{#revision-cleanup}

## Introducción {#introduction}

Cada actualización del repositorio crea una nueva revisión de contenido. Como resultado, con cada actualización, el tamaño del repositorio crece. Para evitar el crecimiento incontrolado del repositorio, es necesario limpiar las viejas revisiones para liberar recursos de disco. Esta funcionalidad de mantenimiento se denomina Limpieza de revisión. Ha estado disponible como rutina sin conexión desde AEM 6.0.

Con AEM 6.3 se ha introducido una versión en línea de esta funcionalidad denominada Limpieza de revisión en línea. En comparación con la Limpieza de revisión sin conexión, donde la instancia de AEM debe cerrarse, la Limpieza de revisión en línea se puede ejecutar mientras la instancia de AEM está en línea. La limpieza de revisión en línea está activada de forma predeterminada y es la forma recomendada de realizar una limpieza de revisión.

**Nota**: [Consulte el vídeo](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/revision-cleanup-technical-video-use.html) para obtener una introducción y cómo utilizar la limpieza de revisión en línea.

El proceso de limpieza de revisión consta de tres fases: **estimación**, **compactación** y **limpiar**. La estimación determina si se ejecutará la siguiente fase (compactación) o no en función de la cantidad de basura que se recopilará. Durante la fase de compactación, los segmentos y los archivos tar se reescriben dejando fuera el contenido no utilizado. La fase de limpieza elimina posteriormente los segmentos antiguos, incluida la basura que puedan contener. El modo sin conexión generalmente puede recuperar más espacio porque el modo en línea necesita tener en cuenta AEM conjunto de trabajo que evita que se recopilen segmentos adicionales.

Para obtener más información sobre la limpieza de revisión, consulte los siguientes vínculos:

* [Cómo ejecutar la limpieza de revisión en línea](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup)
* [Preguntas más frecuentes sobre la limpieza de revisiones en línea](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions)
* [Cómo ejecutar la limpieza de revisión sin conexión](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup)

Además, también puede leer el [documentación oficial de Oak.](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html)

### ¿Cuándo se utiliza la limpieza de revisión en línea en lugar de la limpieza de revisión sin conexión? {#when-to-use-online-revision-cleanup-as-opposed-to-offline-revision-cleanup}

**Limpieza de revisión en línea es la forma recomendada de realizar la limpieza de revisión.** La limpieza de revisiones sin conexión solo debe utilizarse de forma excepcional, por ejemplo, antes de migrar al nuevo formato de almacenamiento o si el Servicio de atención al cliente de Adobe le solicita que lo haga.

## Cómo ejecutar la limpieza de revisión en línea {#how-to-run-online-revision-cleanup}

La limpieza de revisión en línea está configurada de forma predeterminada para ejecutarse automáticamente una vez al día en las instancias de AEM Author y Publish. Todo lo que debe hacer es definir la ventana de mantenimiento durante un periodo con la menor actividad del usuario. Puede configurar la tarea Limpieza de revisión en línea de la siguiente manera:

1. En la ventana de AEM principal, vaya a **Herramientas - Operaciones - Tablero - Mantenimiento** o dirija el navegador a: `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. Pase el ratón **Ventana de mantenimiento diario** y haga clic en el botón **Configuración** icono.

   ![imagen_1-91](assets/chlimage_1-91.png)

1. Introduzca los valores deseados (periodicidad, hora de inicio y hora de finalización) y haga clic en **Guardar**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

Alternativamente, si desea ejecutar la tarea de limpieza de revisión manualmente, puede:

1. Vaya a **Herramientas - Operaciones - Tablero - Mantenimiento** o navegue directamente a `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`
1. Haga clic en el **Ventana de mantenimiento diario**.
1. Pase el ratón sobre la **Limpieza de revisión** icono.
1. Haga clic en **Ejecutar**.

   ![imagen_1-93](assets/chlimage_1-93.png)

### Ejecución De La Limpieza De Revisión En Línea Después De La Limpieza De Revisión Sin Conexión {#running-online-revision-cleanup-after-offline-revision-cleanup}

El proceso de limpieza de revisiones reclama viejas revisiones por generaciones. Esto significa que cada vez que ejecuta la limpieza de revisión, se crea una nueva generación y se mantiene en el disco. Sin embargo, hay una diferencia entre los dos tipos de limpieza de revisión: la limpieza de revisiones sin conexión mantiene una generación mientras que la limpieza de revisiones en línea mantiene dos generaciones. Por lo tanto, cuando ejecute la limpieza de revisión en línea **after** la revisión sin conexión limpia lo siguiente sucede:

1. Después de ejecutar la primera limpieza de revisión en línea, el repositorio tendrá un tamaño doble. Esto sucede porque ahora hay dos generaciones que se mantienen en disco.
1. Durante las ejecuciones posteriores, el repositorio crecerá temporalmente mientras se crea la nueva generación y, a continuación, se estabilizará de nuevo con el tamaño que tenía después de la primera ejecución, ya que el proceso de limpieza de revisiones en línea reclama la generación anterior.

Además, tenga en cuenta que, según el tipo y el número de confirmaciones, cada generación puede variar en tamaño en comparación con la anterior, por lo que el tamaño final puede variar de una ejecución a otra.

Debido a este hecho, se recomienda dimensionar el disco al menos dos o tres veces más grande que el tamaño del repositorio estimado inicialmente.

## Modos De Compactación Completos Y Seguros  {#full-and-tail-compaction-modes}

**AEM 6.5** introduce **dos modos nuevos** para el **compactación** fase del proceso de limpieza de revisión en línea:

* La variable **compactación completa** reescribe todos los segmentos y archivos tar en todo el repositorio. La siguiente fase de limpieza puede eliminar la cantidad máxima de basura en el repositorio. Dado que la compactación completa afecta a todo el repositorio, requiere una cantidad considerable de recursos del sistema y tiempo para completarse. La compactación completa corresponde a la fase de compactación de la AEM 6.3.
* La variable **compactación de cola** reescribe solo los segmentos y archivos tar más recientes del repositorio. Los segmentos y archivos tar más recientes son los que se han añadido desde la última vez que se ejecutó la compactación completa o de cola. La siguiente fase de limpieza solo puede eliminar la basura contenida en la parte reciente del repositorio. Dado que la compactación de cola solo afecta a una parte del repositorio, requiere considerablemente menos recursos y tiempo para completar que la compactación completa.

Estos modos de compactación constituyen un equilibrio entre la eficiencia y el consumo de recursos: aunque la compactación de cola es menos eficaz, también tiene menos impacto en el funcionamiento normal del sistema. Por el contrario, la compactación completa es más eficaz, pero tiene un mayor impacto en el funcionamiento normal del sistema.

AEM 6.5 también introduce un mecanismo de deduplicación de contenido más eficiente durante la compactación, lo que reduce aún más la huella en disco del repositorio.

Los dos gráficos siguientes presentan resultados de pruebas internas de laboratorio que ilustran la reducción de los tiempos de ejecución promedio y de la huella media en disco en el AEM 6,5 en comparación con el AEM 6,3:

![onrc-duration-6_4vs63](assets/onrc-duration-6_4vs63.png) ![segmentstore-6_4vs63](assets/segmentstore-6_4vs63.png)

### Configuración de la compactación completa y de cola {#how-to-configure-full-and-tail-compaction}

La configuración predeterminada ejecuta una compactación de cola en días de semana y una compactación completa los domingos. La configuración predeterminada se puede cambiar utilizando el nuevo valor de configuración `full.gc.days` del `RevisionCleanupTask` [tarea de mantenimiento](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup).

Al configurar la variable `full.gc.days` tenga en cuenta que la compactación completa se ejecutará durante los días definidos en el valor y la compactación de cola se ejecutará durante los días no definidos en el valor. Por ejemplo, si configura la compactación completa para que se ejecute el domingo, la compactación de cola se ejecutará de lunes a sábado. Si, por ejemplo, configura la compactación completa para que se ejecute todos los días de la semana, la compactación de cola no se ejecutará en absoluto.

Además, tenga en cuenta que:

* **Compactación de cola** es menos eficaz y tiene menos impacto en las operaciones normales del sistema. Por lo tanto, está previsto que se ejecute durante los días hábiles.
* **Compactación completa** es más eficaz, pero también tiene un mayor impacto en las operaciones normales del sistema. Por lo tanto, está previsto que se utilice fuera de los días hábiles.
* La compactación de cola y la compactación completa deben programarse para que se ejecuten durante las horas de menor actividad.

### Solución de problemas {#troubleshooting}

Cuando utilice los nuevos modos de compactación, tenga en cuenta lo siguiente:

* Puede monitorizar la actividad de entrada/salida (E/S), por ejemplo: Operaciones de E/S, CPU esperando IO, confirmar tamaño de cola. Esto ayuda a determinar si el sistema se está convirtiendo en un dispositivo de E/S y requiere un cambio de tamaño.
* La variable `RevisionCleanupTaskHealthCheck` indica el estado de salud general de la limpieza de revisión en línea. Funciona del mismo modo que en el AEM 6.3 y no distingue entre compactación completa y de cola.
* Los mensajes de registro contienen información relevante sobre los modos de compactación. Por ejemplo, cuando se inicia la limpieza de revisión en línea, los mensajes de registro correspondientes indicarán el modo de compactación. Además, en algunos casos de esquina, el sistema volverá a la compactación completa cuando se programó para ejecutar una compactación de cola y los mensajes de registro indicarán este cambio. Las muestras de registro siguientes indican el modo de compactación y el cambio de cola a compactación completa:

```
TarMK GC: running tail compaction
TarMK GC: no base state available, running full compaction instead
```

### Limitaciones conocidas {#known-limitations}

En algunos casos, la alternancia entre los modos de cola y compactación completa retrasa el proceso de limpieza. Más precisamente, el repositorio crecerá después de una compactación completa (su tamaño se duplicará). El espacio adicional se regenerará en la siguiente compactación de cola, cuando el repositorio caerá por debajo del tamaño de compactación pre-completo. También deben evitarse las ejecuciones de tareas de mantenimiento paralelas.

**Se recomienda dimensionar el disco al menos dos o tres veces más grande que el tamaño del repositorio estimado inicialmente.**

## Preguntas más frecuentes sobre la limpieza de revisiones en línea {#online-revision-cleanup-frequently-asked-questions}

### Consideraciones sobre la actualización a AEM 6.5 {#aem-upgrade-considerations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td>Preguntas </td>
   <td>Respuestas</td>
  </tr>
  <tr>
   <td>¿Qué debo tener en cuenta al actualizar a AEM 6.5?</td>
   <td><p>El formato de persistencia de TarMK cambiará con AEM 6.5. Estos cambios no requieren un paso de migración proactiva. Los repositorios existentes se migrarán progresivamente, lo que es transparente para el usuario. El proceso de migración se inicia la primera vez AEM 6.5 (o herramientas relacionadas) acceder al repositorio.</p> <p><strong>Una vez iniciada la migración al formato de persistencia AEM 6.5, el repositorio no se puede volver al formato de persistencia AEM 6.3 anterior.</strong></p> </td>
  </tr>
 </tbody>
</table>

### Migración a Oak Segment Tar {#migrating-to-oak-segment-tar}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Preguntas</strong></td>
   <td><strong>Respuestas</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Por qué necesito migrar el repositorio?</strong></td>
   <td><p>En AEM 6.3 se necesitaron cambios en el formato de almacenamiento, especialmente para mejorar el rendimiento y la eficacia de la limpieza de revisión en línea. Estos cambios no son compatibles con versiones anteriores, y los repositorios creados con el segmento Oak antiguo (AEM 6.2 y anteriores) deben migrarse.</p> <p>Ventajas adicionales de cambiar el formato de almacenamiento:</p>
    <ul>
     <li>Mejor escalabilidad (tamaño de segmento optimizado).</li>
     <li>Más rápido <a href="/help/sites-administering/data-store-garbage-collection.md" target="_blank">Colección de residuos del almacén de datos</a>.<br /> </li>
     <li>Masa de trabajo para futuras mejoras.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Sigue siendo compatible el formato Tar anterior?</strong></td>
   <td>Solo se admite el nuevo Oak Segment Tar con AEM 6.3.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿La migración de contenido siempre es obligatoria?</strong></td>
   <td>Sí. A menos que comience con una instancia nueva, siempre tendrá que migrar el contenido.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Puedo actualizar a la versión 6.3 y realizar la migración más tarde (por ejemplo, utilizando otra ventana de mantenimiento)?</strong></td>
   <td>No, como se ha explicado anteriormente, la migración de contenido es obligatoria.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Se puede evitar el tiempo de inactividad al migrar?</strong></td>
   <td>No. Este es un esfuerzo único que no se puede realizar en una instancia en ejecución.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Qué sucede si se ejecuta accidentalmente con el formato de repositorio incorrecto?</strong></td>
   <td>Si intenta ejecutar el módulo oak-segment en un repositorio oak-segment-tar (o viceversa), el inicio fallará con un <em>IllegalStateException</em> con el mensaje "Formato de segmento no válido". No se dañará ningún dato.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Será necesario un reíndice de los índices de búsqueda?</strong></td>
   <td>No. La migración de oak-segment a oak-segment-tar introduce cambios en el formato del contenedor. Los datos contenidos no se ven afectados y no se modificarán.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Cómo calcular mejor el espacio en disco esperado durante y después de la migración?</strong></td>
   <td>La migración equivale a recrear el almacén de segmentos en el nuevo formato. Se puede usar para calcular el espacio de disco adicional necesario durante la migración. Después de la migración, se puede eliminar el antiguo almacén de segmentos para recuperar espacio.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Cómo se puede estimar mejor la duración de la migración?</strong></td>
   <td>El rendimiento de la migración puede mejorarse considerablemente si <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup">limpieza de revisión sin conexión</a> se ejecuta antes de la migración. Se recomienda a todos los clientes que lo ejecuten como requisito previo del proceso de actualización. En general, la duración de la migración debe ser similar a la duración de la tarea de limpieza de revisión sin conexión, suponiendo que la tarea de limpieza de revisión sin conexión se haya ejecutado antes de la migración.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Ejecución de la limpieza de revisión en línea {#running-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Preguntas</strong></td>
   <td><strong>Respuestas</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Con qué frecuencia se debe ejecutar la limpieza de revisión en línea?</strong></td>
   <td>Una vez al día. Esta es la configuración predeterminada en el Tablero de operaciones.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Cómo puedo configurar la hora de inicio de la tarea de mantenimiento Limpieza de revisión en línea ?</strong></td>
   <td>Consulte la <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">Cómo ejecutar la limpieza de revisión en línea</a> para obtener más información. </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Existe una frecuencia máxima que no debe superarse para la limpieza de revisión en línea?</strong></td>
   <td>Se recomienda ejecutar la limpieza de revisión en línea una vez al día, según lo configurado de forma predeterminada.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Cuáles son los indicadores clave que determinan la frecuencia con la que se debe ejecutar la limpieza de revisión en línea?</strong></td>
   <td>No es necesario determinar la frecuencia, ya que la limpieza de revisión en línea está configurada como tarea de mantenimiento y se ejecuta automáticamente cada día.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Por qué la limpieza de revisión en línea no recupera ningún espacio cuando se ejecuta por primera vez?</strong></td>
   <td>Limpieza de revisión en línea reclama viejas revisiones por generaciones. Se genera una nueva generación cada vez que se ejecuta la limpieza de revisión. Solo se recuperará el contenido que tenga al menos dos generaciones, lo que significa que en una primera ejecución no hay nada que reclamar.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Por qué la primera limpieza de revisión en línea no recupera ningún espacio cuando se ejecuta después de la limpieza de revisión sin conexión?</strong></td>
   <td><p>La limpieza de revisión sin conexión está reclamando todo menos la última generación comparada con las últimas dos generaciones para limpieza de revisión en línea. En el caso de un repositorio nuevo, la limpieza de revisión en línea no recuperará ningún espacio cuando se ejecute por primera vez después de la limpieza de revisión sin conexión porque no hay una generación lo suficientemente antigua como para ser reclamada.</p> <p>Además, lea la sección "Ejecución de la limpieza de revisión en línea después de la limpieza de revisión sin conexión" de <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">este capítulo</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Generalmente Autor y Publicación tendrían diferentes ventanas de Limpieza de revisión en línea?</strong></td>
   <td>Esto depende del horario de oficina y de los patrones de tráfico de la presencia en línea del cliente. Las ventanas de mantenimiento deben configurarse fuera de los principales tiempos de producción para permitir la mejor eficacia de limpieza. Para varias instancias de AEM Publish (granja TarMK), las ventanas de mantenimiento para la limpieza de revisión en línea deben escalonar.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Existen requisitos previos para ejecutar la limpieza de revisión en línea?</strong></td>
   <td><p>Limpieza de revisión en línea solo está disponible con AEM versión 6.3 y posteriores. Además, si utiliza una versión anterior de AEM, debe migrar al nuevo <a href="/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar">Tar de segmentos de Oak</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Cuáles son los factores que determinan la duración de la limpieza de revisión en línea?</strong></td>
   <td>Los factores son:<br />
    <ul>
     <li>Tamaño del repositorio</li>
     <li>Carga en el sistema (solicitudes por minuto, específicamente operaciones de escritura)</li>
     <li>Patrón de actividad (lecturas frente a escrituras)</li>
     <li>Especificaciones de hardware (rendimiento de CPU, memoria, IOPS)</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Pueden los autores seguir trabajando mientras se ejecuta la limpieza de revisión en línea?</strong></td>
   <td>Sí, la Limpieza de revisiones en línea puede lidiar con escrituras simultáneas. Sin embargo, la limpieza de revisiones en línea funciona de forma más rápida y eficaz sin transacciones de escritura concurrentes. Se recomienda programar la tarea de mantenimiento Limpieza de revisión en línea para un tiempo relativamente tranquilo sin mucho tráfico.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Cuáles son los requisitos mínimos de espacio en disco y memoria acumulada al ejecutar la limpieza de revisión en línea?</strong></td>
   <td><p>El espacio en disco se monitorea continuamente durante la limpieza de revisión en línea. Si el espacio en disco disponible cae por debajo de un valor crítico, el proceso se cancelará. El valor crítico es el 25% de la huella de disco actual del repositorio y no es configurable.</p> <p><strong>Se recomienda dimensionar el disco al menos dos o tres veces más grande que el tamaño del repositorio estimado inicialmente.</strong></p> <p>Durante el proceso de limpieza, se monitoriza continuamente el espacio libre en pilas. Si el espacio libre en montículos cae por debajo de un valor crítico, el proceso se cancela. El valor crítico se configura mediante org.apache.jackrabbit.oak.segment.SegmentNodeStoreService#MEMORY_THRESHOLD. El valor predeterminado es 15%.</p> <p>Recommendations para el tamaño mínimo de la pila de compactación no está separado de las recomendaciones de tamaño de la memoria AEM. Como regla general: <strong>Si una instancia de AEM tiene el tamaño suficiente para hacer frente a los casos de uso y a la carga útil esperada en ellos, el proceso de limpieza obtendrá suficiente memoria.</strong></p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Cuál es el impacto esperado en el rendimiento al ejecutar la limpieza de revisión en línea?</strong></td>
   <td>La limpieza de revisión en línea es un proceso en segundo plano que lee desde el repositorio y escribe en él simultáneamente a las operaciones normales del sistema. En particular, es posible que necesite adquirir acceso exclusivo al repositorio durante un corto periodo de tiempo, evitando que otros subprocesos escriban en el repositorio.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Durante cuánto tiempo se espera que se ejecute la limpieza de revisión en línea?</strong></td>
   <td>No debería tardar más de 2 horas en ejecutarse de acuerdo con las últimas pruebas de rendimiento que realizamos internamente.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Qué debe hacerse si la limpieza de revisión en línea tarda más?</strong></td>
   <td>
    <ul>
     <li>Asegúrese de que se ejecuta a diario.<br /> </li>
     <li>Asegúrese de que se ejecute durante las actividades mínimas del repositorio configurando las ventanas de mantenimiento en el panel de operaciones en consecuencia.</li>
     <li>Aumente los recursos del sistema (CPU, memoria, E/S).</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Qué sucede si la limpieza de revisión en línea supera las ventanas de mantenimiento configuradas?</strong></td>
   <td>Asegúrese de que otras tareas de mantenimiento no retrasen su ejecución. Este podría ser el caso si se ejecutan más tareas de mantenimiento que Limpieza de revisión en línea dentro de la misma ventana de mantenimiento. Tenga en cuenta que las tareas de mantenimiento se ejecutan secuencialmente sin un orden configurable.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Por qué se omite la colección de residuos de revisión?</strong></td>
   <td><p>Limpieza de revisión se basa en una fase de estimación para decidir si hay suficiente basura para limpiar. El estimador compara el tamaño actual con el tamaño del repositorio después de la última compactación. Si el tamaño supera el delta configurado, se ejecutará la limpieza. El tamaño delta se establece en 1 GB. Esto significa que si el tamaño del repositorio no aumentó en 1 GB desde la última ejecución de limpieza, se omitirá la nueva iteración de limpieza de revisión. </p> <p>A continuación se muestran las entradas de registro relevantes para la fase de estimación:</p>
    <ul>
     <li>Revision GC se ejecutará: <em>El delta de tamaño es N% o N/N (N/N bytes), por lo que se ejecuta la compactación</em></li>
     <li>Revisión GC <strong>not</strong> ejecutar: <em>El delta de tamaño es N% o N/N (N/N bytes), por lo que omitirá la compactación por ahora</em></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Es posible anular de forma segura la compactación automática si el impacto en el rendimiento es demasiado alto?</strong></td>
   <td>Sí. Desde AEM 6.3 se puede detener de forma segura a través de la ventana de tareas de mantenimiento dentro del panel de operaciones o a través de JMX.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Si la instancia de AEM se apaga durante una tarea de limpieza programada, ¿el proceso se interrumpe de forma segura o el apagado se bloquea hasta que la compactación haya finalizado?</strong></td>
   <td>La limpieza de revisión se interrumpirá y el repositorio se cerrará de forma segura.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Qué sucede cuando el sistema se bloquea durante la limpieza de revisión en línea?</strong></td>
   <td>No existe riesgo de corrupción de datos en estos casos. Las sobras de basura se limpiarán con una ejecución posterior.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Cuál es el impacto de no ejecutar la limpieza de revisión en línea?</strong></td>
   <td>Degradación del rendimiento a lo largo del tiempo.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Qué revisiones se están recopilando?</strong></td>
   <td>De forma predeterminada, la limpieza de revisión en línea solo recopila revisiones que tengan al menos 24 horas de antigüedad.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Qué sucede en caso de demasiada interferencia de escrituras simultáneas en el repositorio?</strong></td>
   <td><p>Si hay concurrencia de escritura en el sistema, la limpieza de revisión en línea puede requerir acceso de escritura exclusivo para poder confirmar los cambios al final de un ciclo de compactación. El sistema entrará en <strong>forceCompact mode</strong>, tal y como se explica más detalladamente en la sección <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html" target="_blank">documentación de oak</a>. Durante la fuerza compacta, se adquiere un bloqueo de escritura exclusivo para confirmar finalmente los cambios sin que interfiera ninguna escritura concurrente. Para limitar el impacto en los tiempos de respuesta, se puede definir un valor de tiempo de espera. Este valor se establece en 1 minuto de forma predeterminada, lo que significa que si force Compact no se completa en 1 minuto, el proceso de compactación se anulará en favor de confirmaciones simultáneas.</p> <p>La duración del pacto de fuerza depende de los siguientes factores:</p>
    <ul>
     <li>hardware: específicamente IOPS. La duración disminuye con más IOPS.</li>
     <li>tamaño del almacén de segmentos: la duración aumenta con el tamaño del almacén de segmentos.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>¿Cómo se ejecuta la limpieza de revisión en línea en una instancia de espera?</strong></p> </td>
   <td><p>En una configuración de espera en frío, solo la instancia principal debe configurarse para ejecutar la limpieza de revisión en línea. En la instancia de espera, la limpieza de revisión en línea no necesita programarse específicamente.</p> <p>La operación correspondiente en una instancia de espera es la limpieza automática, que corresponde a la fase de limpieza de la limpieza de revisión en línea. La limpieza automática se ejecuta en la instancia de espera después de la ejecución de la limpieza de revisión en línea en la instancia principal.</p> <p>Las fases de estimación y compactación no se ejecutarán en una instancia de espera.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿La limpieza de revisión sin conexión es capaz de liberar más espacio en disco que la limpieza de revisión en línea?</strong></td>
   <td><p>La limpieza de revisión sin conexión puede eliminar inmediatamente las revisiones antiguas, mientras que la limpieza de revisión en línea debe tener en cuenta las revisiones antiguas a las que sigue haciendo referencia la pila de aplicaciones. Por lo tanto, el primero puede eliminar la basura de manera más agresiva que el segundo, donde el efecto se amortiza durante algunos ciclos de recolección de basura.</p> <p>Además, lea la sección "Ejecución de la limpieza de revisión en línea después de la limpieza de revisión sin conexión" de <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">este capítulo</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>¿Alguna consideración sobre las operaciones de archivos asignados a memoria?</td>
   <td>
    <ul>
     <li><strong>En entornos Windows</strong>, el acceso regular a archivos siempre se aplica, por lo que no se utiliza el acceso asignado a memoria. Como consejo general, toda la RAM disponible debe asignarse a la pila y el tamaño de segmentCache debe aumentarse. Aumente segmentCache agregando la opción segmentCache.size a org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config (por ejemplo, segmentCache.size=20480). Recuerde dejar fuera parte de la RAM para el sistema operativo y otros procesos.</li>
     <li><strong>En entornos que no son de Windows</strong>, aumente el tamaño de la memoria física para mejorar la asignación de memoria del repositorio.</li>
    </ul> </td>
   <td>
    <ul>
     <li> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Supervisión de la limpieza de revisión en línea {#monitoring-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>¿Qué debe monitorizarse durante la limpieza de revisión en línea?</strong></td>
   <td>
    <ul>
     <li>El espacio en disco debe monitorizarse cuando la limpieza de revisión en línea está habilitada. La limpieza no se ejecutará o terminará de forma preventiva cuando no haya suficiente espacio en disco.</li>
     <li>Compruebe los registros para la hora de finalización de la limpieza de revisión en línea. No debe tardar más de 2 horas.</li>
     <li>Número de puntos de comprobación. Si hay más de 3 puntos de comprobación cuando se ejecuta la compactación, se recomienda limpiar los puntos de comprobación.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Cómo comprobar si la limpieza de revisión en línea se ha completado correctamente?</strong></td>
   <td><p>Puede comprobar si la limpieza de revisión en línea se ha completado correctamente comprobando los registros.</p> <p>Por ejemplo, "<code>TarMK GC #{}: compaction completed in {} ({} ms), after {} cycles</code>" significa que el paso de compactación se completó correctamente a menos que esté precedido por el mensaje "<code>TarMK GC #{}: compaction gave up compacting concurrent commits after {} cycles</code>", lo que significa que había demasiada carga simultánea.</p> <p>Por lo tanto, hay un mensaje "<code>TarMK GC #{}: cleanup completed in {} ({} ms</code>" para completar correctamente el paso de limpieza.</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><strong>¿Dónde podemos encontrar las estadísticas de las últimas ejecuciones de limpieza de revisión en línea ?</strong></td>
   <td><p>El estado, el progreso y las estadísticas se exponen a través de JMX (<code>SegmentRevisionGarbageCollection</code> MBean). Para obtener más información sobre la variable <code>SegmentRevisionGarbageCollection</code> MBean, lea el <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">párrafo siguiente</a>.</p> <p>Se puede realizar un seguimiento del progreso mediante la variable <code>EstimatedRevisionGCCompletion</code> del <code>SegmentRevisionGarbageCollection MBean.</code></p> <p>Puede obtener una referencia de MBean mediante la variable <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection"</code>.</p> <p>Tenga en cuenta que las estadísticas solo están disponibles desde el último inicio del sistema. Se podrían aprovechar las herramientas de monitorización externa para mantener los datos más allá AEM tiempo de actividad. Consulte <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">la documentación AEM para adjuntar los controles sanitarios a Nagios como ejemplo de herramienta de monitorización externa</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Qué son las entradas de registro relevantes?</strong></td>
   <td>
    <ul>
     <li>Se ha iniciado o detenido la limpieza de revisión en línea
      <ul>
       <li>La limpieza de revisión en línea consta de tres fases: estimación, compactación y limpieza. La estimación puede obligar a que se omita la compactación y la limpieza si el repositorio no contiene suficiente basura. En la última versión de AEM, el mensaje "<code>TarMK GC #{}: estimation started</code>" marca el inicio de la estimación, "<code>TarMK GC #{}: compaction started, strategy={}</code>" marca el inicio de la compactación y "T<code>arMK GC #{}: cleanup started. Current repository size is {} ({} bytes</code>" marca el inicio de la limpieza.</li>
      </ul> </li>
     <li>Espacio en disco obtenido por la limpieza de revisión
      <ul>
       <li>El espacio solo se recupera cuando termina la fase de limpieza. La finalización de la fase de limpieza se marca con el mensaje de registro "T<code>arMK GC #{}: cleanup completed in {} ({} ms</code>". El tamaño de la limpieza posterior es de {} ({} bytes) y el espacio recuperado es de {} ({} bytes). El peso/profundidad del mapa de compactación es {}/{} ({} bytes/{})."</li>
      </ul> </li>
     <li>Se ha producido un problema durante la limpieza de revisión
      <ul>
       <li>Existen muchas condiciones de error, todas ellas están marcadas por los mensajes de registro WARN o ERROR que empiezan con "TarMK GC".</li>
      </ul> </li>
    </ul> <p>Consulte también la <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">Resolución de problemas basados en mensajes de error</a> a continuación.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Cómo comprobar cuánto espacio se ha reclamado después de que se haya completado la limpieza de revisión en línea?</strong></td>
   <td>Hay un mensaje en el registro al final del ciclo de limpieza: "<code>TarMK GC #3: cleanup completed</code>" que incluye el tamaño del repositorio y la cantidad de basura reclamada.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Cómo comprobar la integridad del repositorio después de que se haya completado la limpieza de revisión en línea?</strong></td>
   <td><p>No se necesita una comprobación de integridad del repositorio después de la limpieza de revisión en línea. </p> <p>Sin embargo, puede realizar las siguientes acciones para comprobar el estado del repositorio después de la limpieza:</p>
    <ul>
     <li>Un repositorio <a href="/help/sites-deploying/consistency-check.md" target="_blank">comprobación transversal</a></li>
     <li>Utilice la herramienta Oak-run después de completar el proceso de limpieza para comprobar si hay incoherencias. Para obtener más información sobre cómo hacerlo, consulte la <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Documentación de Apache.</a> No es necesario apagar AEM para ejecutar la herramienta.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Cómo se detecta si la limpieza de revisión en línea ha fallado y cuáles son los pasos a seguir para recuperarse?</strong></td>
   <td>Las condiciones de error se marcan con los mensajes WARN o ERROR log que comienzan con "TarMK GC". Consulte también la <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">Resolución de problemas basados en mensajes de error</a> a continuación.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Qué información se expone en la Revisión del estado de limpieza de revisión? ¿Cómo y cuándo contribuyen a los niveles de estado codificados por color? </strong></td>
   <td><p>La comprobación de estado de limpieza de revisión forma parte del <a href="/help/sites-administering/operations-dashboard.md#health-reports" target="_blank">Tablero de operaciones</a>.<br /> </p> <p>El estado será <strong>VERDE</strong> si la última ejecución de la tarea de mantenimiento Limpieza de revisión en línea se ha completado correctamente.</p> <p>Será <strong>AMARILLO</strong> si la tarea de mantenimiento Limpieza de revisión en línea se canceló una vez.<br /> </p> <p>Será <strong>RED</strong> si la tarea de mantenimiento Limpieza de revisión en línea se canceló tres veces seguidas. <strong>En este caso se requiere interacción manual</strong> o es probable que la limpieza de revisión en línea vuelva a fallar. Para obtener más información, lea la <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-online-revision-cleanup">Resolución de problemas</a> a continuación.<br /> </p> <p>Tenga en cuenta también que el estado de la comprobación de estado se restablecerá después de reiniciar el sistema. Por lo tanto, una instancia que se haya reiniciado recientemente mostrará un estado verde en la Revisión de estado de limpieza de revisión. Se podrían aprovechar las herramientas de monitorización externa para mantener los datos más allá AEM tiempo de actividad. Consulte <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios">la documentación AEM para adjuntar los controles sanitarios a Nagios como ejemplo de herramienta de monitorización externa</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>¿Cómo monitorizar la limpieza automática en una instancia de espera?</strong></p> </td>
   <td><p>El estado, el progreso y las estadísticas se exponen a través de JMX usando la variable <code>SegmentRevisionGarbageCollection</code> MBean. Consulte también lo siguiente <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">Documentación de Oak</a>. </p> <p>Puede obtener una referencia de MBean utilizando la variable <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection"</code>.</p> <p>Tenga en cuenta que las estadísticas solo están disponibles desde el último inicio del sistema. Se podrían aprovechar las herramientas de monitorización externa para mantener los datos más allá del tiempo AEM activo. Consulte también <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">la documentación AEM para adjuntar los controles sanitarios a Nagios como ejemplo de herramienta de monitorización externa</a>.</p> <p>Los archivos de registro también pueden utilizarse para comprobar el estado, el progreso y las estadísticas de la limpieza automática.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>¿Qué debe monitorizarse durante la limpieza automática en una instancia de espera?</strong></p> </td>
   <td>
    <ul>
     <li>El espacio en disco debe monitorizarse cuando se ejecuta la limpieza automática.</li>
     <li>Tiempo de finalización (mediante los registros) para garantizar que no se superen las 2 horas.</li>
     <li>Tamaño del almacén de segmentos después de ejecutar la limpieza automática. El tamaño del almacén de segmentos en la instancia de espera debe ser aproximadamente el mismo que el de la instancia principal.</li>
    </ul> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Solución de problemas de limpieza de revisión en línea {#troubleshooting-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>¿Qué es lo peor que puede suceder si no ejecuta la limpieza de revisión en línea?</strong></td>
   <td>La instancia de AEM se quedará sin espacio en disco, lo que provocará interrupciones en la producción.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Es problemático el alto tráfico de usuarios para ejecutar la limpieza de revisión en línea en una instancia de publicación?</strong></td>
   <td>El alto tráfico del usuario afecta si la fase de compactación puede finalizar o no correctamente.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Según la Comprobación de estado y las entradas de registro, la Limpieza de revisión en línea no se ha completado correctamente tres veces seguidas. ¿Qué se necesita para que la limpieza de revisión en línea se complete correctamente?</strong></td>
   <td>Puede realizar varios pasos para encontrar y solucionar el problema:<br />
    <ul>
     <li>Primero, compruebe las entradas de registro<br /> </li>
     <li>Según la información de los registros, tome las medidas adecuadas:
      <ul>
       <li>Si los registros muestran cinco ciclos compactos faltantes y un tiempo de espera en la variable <code>forceCompact</code> , programe la ventana de mantenimiento en un momento silencioso cuando la cantidad de escrituras del repositorio sea baja. Puede comprobar las escrituras del repositorio en la herramienta de monitorización de métricas del repositorio ubicada en <em>https://serveraddress:serverport/libs/granite/operations/content/monitoring/page.html</em></li>
       <li>Si la limpieza se detuvo al final de la ventana de mantenimiento, asegúrese de que la configuración de la ventana de mantenimiento en la interfaz de usuario Tareas de mantenimiento sea lo suficientemente grande</li>
       <li>Si la memoria de pila disponible no es suficiente, asegúrese de que la instancia tiene suficiente memoria.</li>
       <li>En caso de una reacción tardía, el almacén de segmentos podría crecer demasiado para que la Limpieza de revisiones en línea se complete incluso dentro de un período de mantenimiento más largo. Por ejemplo, si no se completó correctamente la limpieza de revisión en línea en la última semana, se recomienda planificar un mantenimiento sin conexión y ejecutar la limpieza de revisión sin conexión para que el almacén de segmentos vuelva a tener un tamaño manejable.</li>
      </ul> </li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Qué se debe hacer una vez que la alerta de control de salud esté activada?</strong></td>
   <td>Véase el punto anterior.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Qué sucede si la limpieza de revisión en línea se queda sin tiempo durante el período de mantenimiento programado?</strong></td>
   <td>La limpieza de revisión en línea se cancelará y se eliminarán los restos. Se iniciará de nuevo la próxima vez que se programe la ventana de mantenimiento.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Qué está causando <code>SegmentNotFoundException</code> instancias que se van a registrar en el <code>error.log</code> ¿y cómo puedo recuperarme?</strong></td>
   <td><p>A <code>SegmentNotFoundException</code> es registrado por TarMK cuando intenta acceder a una unidad de almacenamiento (un segmento) que no puede encontrar. Hay tres escenarios que podrían causar este problema:</p>
    <ol>
     <li>Una aplicación que elude los mecanismos de acceso recomendados (como Sling y la API de JCR) y utiliza una API/SPI de nivel inferior para acceder al repositorio y luego supera el tiempo de retención de un segmento. Es decir, mantiene una referencia a una entidad más allá del tiempo de retención permitido por la limpieza de revisión en línea (de forma predeterminada, 24 horas). Este caso es transitorio y no provoca daños en los datos. Para recuperarse, la herramienta oak-run debe utilizarse para confirmar la naturaleza transitoria de la excepción (la comprobación oak-run no debe notificar ningún error). Para ello, la instancia debe desconectarse y reiniciarse posteriormente.</li>
     <li>Un evento externo provocó la corrupción de los datos en el disco. Esto puede ser una falla en el disco, una falta de espacio en disco o una modificación accidental de los archivos de datos necesarios. En este caso, la instancia debe desconectarse y repararse con la comprobación oak-run. Para obtener más información sobre cómo realizar la comprobación Oak-run, lea lo siguiente <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Documentación de Apache</a>.</li>
     <li>Todas las demás ocurrencias deben solucionarse a través del <a href="https://helpx.adobe.com/es/marketing-cloud/contact-support.html" target="_blank">Servicio de atención al cliente de Adobe</a>.</li>
    </ol> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Resolución de problemas basados en mensajes de error {#troubleshooting-based-on-error-messages}

El archivo error.log será detallado si hay incidentes durante el proceso de limpieza de revisión en línea. La siguiente matriz pretende explicar los mensajes más comunes y proporcionar posibles soluciones:

<!---| **Phase** |**Log Messages** |**Explanation** |**Next Steps** |
|---|---|---|---|
|   |  |  |  |
| Estimation |TarMK GC #2: estimation skipped because compaction is paused |The estimation phase is skipped when compaction is disabled on the system by configuration. |Enable Online Revision Cleanup. |
|   |TarMK GC #2: estimation interrupted: ${REASON}. Skipping compaction. |The estimation phase terminated prematurely. Some examples of events that could interrupt the estimation phase: not enough memory or disk space on the host system. |Depends on the given reason. |
| Compaction |TarMK GC #2: compaction paused |As long as the compaction phase is paused by configuration, neither the estimation phase nor the compaction phase will be executed. |Enable online revision cleanup. |
|   |TarMK GC #2: compaction cancelled: ${REASON}. |The compaction phase terminated prematurely. Some examples of events that could interrupt the compaction phase: not enough memory or disk space on the host system. Moreover, compaction can also be cancelled by shutting down the system or by explicitly cancelling it via administrative interfaces such as the Maintenance Window within the Operations Dashobard. |Depends on the given reason. |
|   |TarMK GC #2: compaction failed in 32.902 min (1974140 ms), after 5 cycles |This message doesn’t mean that there was an unrecoverable error, but only that compaction was terminated after a certain amount of attempts. Also, read the [following paragraph](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes). |Read the following [Oak documentation](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes), and the last question of the [Running Online Revision Cleanup](/help/sites-deploying/revision-cleanup.md#running-online-revision-cleanup) section. |
| Cleanup |TarMK GC #2: cleanup interrupted |Cleanup has been cancelled by shutting down the repository. No impact on consistency is expected. Also, disk space is most likely not reclaimed to full extent. It will be reclaimed during next revision cleanup cycle. |Investigate why repository has been shut down and going forward try to avoid shutting down the repository during maintenance windows. |-->

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>Fase</th>
    <th>Mensajes de registro</th>
    <th>Explicación</th>
    <th>Siguientes pasos</th>
  </tr>  
  <tr>
    <td>Estimación</td>
    <td>TarMK GC #2: estimación omitida porque la compactación está en pausa.</td>
    <td>La fase de estimación se omite cuando la compactación está deshabilitada en el sistema por configuración.</td>
    <td>Habilite la limpieza de revisión en línea.</td>
  </td>
  </tr>
  <tr>
    <td>N/D</td>
    <td>TarMK GC #2: estimación interrumpida: ${REASON}. Omitiendo la compactación.</td>
    <td>La fase de estimación finalizó prematuramente. Algunos ejemplos de eventos que podrían interrumpir la fase de estimación: no hay suficiente memoria o espacio en disco en el sistema host.</td>
    <td>Depende del motivo dado.</td>
  </td>
  </tr>
  <tr>
    <td>Compactación</td>
    <td>TarMK GC #2: compactación pausada.</td>
    <td>Mientras la fase de compactación esté pausada por la configuración, no se ejecutará ni la fase de estimación ni la fase de compactación.</td>
    <td>Habilite la limpieza de revisiones en línea.</td>
  </td>
  </tr>
   <tr>
    <td>N/D</td>
    <td>TarMK GC #2: compactación cancelada: ${REASON}.</td>
    <td>La fase de compactación finalizó prematuramente. Algunos ejemplos de eventos que podrían interrumpir la fase de compactación: no hay suficiente memoria o espacio en disco en el sistema host. Además, la compactación también puede cancelarse apagando el sistema o cancelándolo explícitamente a través de interfaces administrativas como la Ventana de Mantenimiento dentro del Tablero de Operaciones.</td>
    <td>Depende del motivo dado.</td>
  </td>
  </tr>
  <tr>
    <td>N/D</td>
    <td>TarMK GC #2: la compactación falló en 32,902 min (1974140 ms), después de 5 ciclos.</td>
    <td>Este mensaje no significa que haya un error irrecuperable, pero solo que esa compactación se terminó después de una cierta cantidad de intentos. Lea también el <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes">párrafo siguiente.</a></td>
    <td>Lea lo siguiente <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes">Documentación de Oak</a>y la última pregunta de la sección Ejecución de Limpieza de Revisión en línea .</a></td>
  </td>
  </tr>
  <tr>
    <td>Limpiar</td>
    <td>TarMK GC #2: limpieza interrumpida.</td>
    <td>La limpieza se ha cancelado cerrando el repositorio. No se espera ningún impacto en la coherencia. Además, es muy probable que el espacio en disco no se vuelva a reclamar en su totalidad. Se recuperará durante el próximo ciclo de limpieza de revisión.</td>
    <td>Investigue por qué el repositorio se ha cerrado y en adelante intente evitar apagar el repositorio durante las ventanas de mantenimiento.</td>
  </td>
  </tr>
  </tbody>
</table>

## Cómo ejecutar la limpieza de revisión sin conexión {#how-to-run-offline-revision-cleanup}

>[!CAUTION]
>
>Es necesario utilizar diferentes versiones de la herramienta Oak-run dependiendo de la versión Oak que utilice con la instalación de AEM. Compruebe la lista de requisitos de la versión que aparece a continuación antes de utilizar la herramienta:
>
>* Para versiones de Oak **De 1.0.0 a 1.0.11** o **1.1.0 a 1.1.6**, utilice la versión Oak-run** 1.0.11**
>
>* Para versiones de Oak **más reciente que el anterior**, utilice la versión de Oak-run que coincida con el núcleo Oak de su instalación de AEM.
>


El Adobe proporciona una herramienta llamada **Oak-run** para realizar la limpieza de revisión. Se puede descargar desde la siguiente ubicación:

[https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/)

La herramienta es un jar ejecutable que se puede ejecutar manualmente para compactar el repositorio. El proceso se denomina limpieza de revisión sin conexión porque el repositorio debe cerrarse para ejecutar correctamente la herramienta. Asegúrese de planificar la limpieza de acuerdo con su ventana de mantenimiento.

Para obtener sugerencias sobre cómo aumentar el rendimiento del proceso de limpieza, consulte [Aumento del rendimiento de la limpieza de revisión sin conexión](/help/sites-deploying/revision-cleanup.md#increasing-the-performance-of-offline-revision-cleanup).

>[!NOTE]
>
>También puede borrar los puntos de comprobación antiguos antes de que tenga lugar el mantenimiento (pasos 2 y 3 del procedimiento siguiente). Esto solo se recomienda para las instancias que tienen más de 100 puntos de comprobación.

1. Asegúrese siempre de tener una copia de seguridad reciente de la instancia de AEM.

   Apague AEM.

1. (Opcional) Utilice la herramienta para encontrar puntos de comprobación antiguos:

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore
   ```

1. (Opcional) A continuación, elimine los puntos de comprobación no referenciados:

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore rm-unreferenced
   ```

1. Ejecute la compactación y espere a que se complete:

   ```xml
   java -jar -Dsun.arch.data.model=32 oak-run.jar compact install-folder/crx-quickstart/repository/segmentstore
   ```

### Aumento del rendimiento de la limpieza de revisión sin conexión {#increasing-the-performance-of-offline-revision-cleanup}

La herramienta Oak-run introduce varias funciones que pretenden aumentar el rendimiento del proceso de limpieza de revisiones y minimizar la ventana de mantenimiento en la medida de lo posible.

La lista incluye varios parámetros de línea de comandos, como se describe a continuación:

* **-mmap.** Puede establecerlo como verdadero o falso. Si se establece en true, se utiliza el acceso asignado a memoria. Si se establece en false, se utiliza el acceso a los archivos. Si no se especifica, el acceso asignado a memoria se utiliza en sistemas de 64 bits y el acceso a archivos se utiliza en sistemas de 32 bits. En Windows, el acceso a archivos regular siempre se aplica y esta opción se ignora. **Este parámetro ha reemplazado el parámetro -Dtar.memoryMapped.**

* **-Dupdate.limit**. Define el umbral para el vaciado de una transacción temporal en disco. El valor predeterminado es 10000.

* **-Descomprimir-intervalo**. Número de entradas del mapa de compactación que se van a mantener hasta que se comprime el mapa actual. El valor predeterminado es 1000000. Debería aumentar este valor a un número aún mayor para un rendimiento más rápido, si hay suficiente memoria acumulada disponible. **Este parámetro se ha eliminado en la versión 1.6 de Oak y no tiene ningún efecto.**

* **-Dcompaction-progress-log**. Número de nodos compuestos que se registrarán. El valor predeterminado es 150000, lo que significa que los primeros 150000 nodos compactados se registrarán durante la operación. Utilícelo junto con el siguiente parámetro documentado a continuación.

* **-Dtar.PersistCompactionMap.** Establezca este parámetro en true para usar espacio en disco en lugar de memoria en pilas para la persistencia del mapa de compactación. Requiere la herramienta Oak-run **versiones 1.4** y superior. Para más detalles, véase la pregunta 3 de la sección [Preguntas más frecuentes sobre la limpieza de revisiones sin conexión](/help/sites-deploying/revision-cleanup.md#offline-revision-cleanup-frequently-asked-questions) para obtener más información. **Este parámetro se ha eliminado en la versión 1.6 de Oak y no tiene ningún efecto.**

* **—force.** Forzar la compactación e ignorar una versión del almacén de segmentos que no coincida.

>[!CAUTION]
>
>Al usar la variable `--force` actualizará el almacén de segmentos a la última versión, lo que no es compatible con versiones anteriores de Oak. Además, tenga en cuenta que no es posible reducir la categoría. Como regla general, debe usar estos parámetros con precaución y solo si conoce cómo utilizarlos.

Ejemplo de los parámetros en uso:

```xml
java -Dupdate.limit=10000 -Dcompaction-progress-log=150000 -Dlogback.configurationFile=logback.xml -Xmx8g -jar oak-run-*.jar checkpoints <repository>
```

### Métodos adicionales para activar la limpieza de revisión {#additional-methods-of-triggering-revision-cleanup}

Además de los métodos presentados anteriormente, también puede almacenar en déclencheur el mecanismo de limpieza de revisiones utilizando la consola JMX de la siguiente manera:

1. Abra la consola JMX en [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)
1. Haga clic en el **RevisionGarbageCollection** MBean.
1. En la siguiente ventana, haga clic en **startRevisionGC()** y luego **Invocar** para iniciar el trabajo de colección de residuos de revisión.

### Preguntas más frecuentes sobre la limpieza de revisiones sin conexión {#offline-revision-cleanup-frequently-asked-questions}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>¿Cuáles son los factores que determinan la duración de la limpieza de revisión sin conexión?</strong></td>
   <td><p>El tamaño del repositorio y la cantidad de revisiones que deben limpiarse determinan la duración de la limpieza.</p> </td>
  </tr>
  <tr>
   <td><strong>¿Cuál es la diferencia entre una revisión y una versión de página?</strong></td>
   <td>
    <ul>
     <li><strong>Revisión de Oak:</strong> Oak organiza todo el contenido en una jerarquía de árbol grande que consta de nodos y propiedades. Cada instantánea o revisión de este árbol de contenido es inmutable, y los cambios en el árbol se expresan como una secuencia de nuevas revisiones. Normalmente, cada modificación de contenido déclencheur una nueva revisión. Consulte también <a href="https://jackrabbit.apache.org/dev/ngp.html" target="_blank"> Seguir vínculo</a>.</li>
     <li><strong>Versión de la página:</strong> Al generar una versión se crea una "instantánea" de una página en un punto específico en el tiempo. Normalmente, se crea una nueva versión cuando se activa una página. Para obtener más información, consulte <a href="/help/sites-authoring/working-with-page-versions.md" target="_blank">Uso de versiones de página</a>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>¿Cómo acelerar la tarea de limpieza de revisión sin conexión si no se completa en un plazo de 8 horas?</strong></td>
   <td>Si la tarea de revisión no se completa en un plazo de 8 horas y <a href="/help/sites-administering/operations-dashboard.md#diagnosis-tools" target="_blank">volcados de subprocesos</a> revelar que el punto interactivo principal es <code>InMemoryCompactionMap.findEntry</code>, utilice el siguiente parámetro con la herramienta oak-run <strong>versiones 1.4 </strong>o superior: <code>-Dtar.PersistCompactionMap=true</code>. Tenga en cuenta que <code>-Dtar.PersistCompactionMap</code> se ha eliminado en la versión 1.6 de Oak.</td>
  </tr>
 </tbody>
</table>
