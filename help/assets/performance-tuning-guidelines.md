---
title: Ajuste de rendimiento para [!DNL Adobe Experience Manager Assets].
description: Sugerencias y directrices [!DNL Experience Manager] sobre configuración, cambios en hardware, software y componentes de red para eliminar cuellos de botella y optimizar el rendimiento del [!DNL Experience Manager Assets]producto.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: b59f7471ab9f3c5e6eb3365122262b592c8e6244
workflow-type: tm+mt
source-wordcount: '2767'
ht-degree: 0%

---


<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] guía de optimización del rendimiento {#assets-performance-tuning-guide}

Una [!DNL Experience Manager Assets] configuración contiene varios componentes de hardware, software y red. Según el escenario de implementación, es posible que necesite cambios específicos en la configuración de hardware, software y componentes de red para eliminar los cuellos de botella de rendimiento.

Además, la identificación y el cumplimiento de ciertas directrices de optimización de hardware y software ayuda a crear una base sólida que permite que su [!DNL Experience Manager Assets] implementación cumpla con las expectativas de rendimiento, escalabilidad y confiabilidad.

El rendimiento deficiente en [!DNL Experience Manager Assets] puede afectar a la experiencia del usuario en cuanto al rendimiento interactivo, el procesamiento de recursos, la velocidad de descarga y otras áreas.

De hecho, la optimización del rendimiento es una tarea fundamental que se realiza antes de establecer métricas de destinatario para cualquier proyecto.

A continuación se indican algunas áreas de enfoque clave en las que se detectan y corrigen los problemas de rendimiento antes de que afecten a los usuarios.

## Plataforma {#platform}

Aunque Experience Manager es compatible con varias plataformas, Adobe ha encontrado la buena compatibilidad con herramientas nativas en Linux y Windows, lo que contribuye a un rendimiento óptimo y a una implementación más sencilla. Lo ideal es implementar un sistema operativo de 64 bits para cumplir los requisitos de memoria alta de una [!DNL Experience Manager Assets] implementación. Al igual que con cualquier implementación de Experience Manager, debe implementar TarMK siempre que sea posible. Aunque TarMK no puede escalar más allá de una sola instancia de autor, se ha descubierto que funciona mejor que MongoMK. Puede agregar instancias de descarga de TarMK para aumentar la potencia de procesamiento del flujo de trabajo de su [!DNL Experience Manager Assets] implementación.

### Carpeta temporal {#temp-folder}

Para mejorar los tiempos de carga de recursos, utilice almacenamientos de alto rendimiento para el directorio temporal de Java. En Linux y Windows, se puede utilizar una unidad RAM o SSD. En los entornos basados en la nube, se puede utilizar un tipo de almacenamiento de alta velocidad equivalente. Por ejemplo, en Amazon EC2, se puede utilizar una unidad de [disco](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) efímero para la carpeta temporal.

Si el servidor tiene una memoria amplia, configure una unidad de RAM. En Linux, ejecute estos comandos para crear una unidad de 8 GB de RAM:

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

En el sistema operativo Windows, utilice un controlador de terceros para crear una unidad de RAM o simplemente utilice almacenamientos de alto rendimiento como SSD.

Una vez que el volumen temporal de alto rendimiento esté listo, establezca el parámetro JVM `-Djava.io.tmpdir`. Por ejemplo, puede agregar el parámetro JVM siguiente a la `CQ_JVM_OPTS` variable en la `bin/start` secuencia de comandos de [!DNLEExperience Manager]:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Configuración de Java {#java-configuration}

### Versión de Java {#java-version}

Adobe recomienda la implementación [!DNL Experience Manager Assets] en Java 8 para un rendimiento óptimo.

<!-- TBD: Link to the latest official word around Java.
-->

### Parámetros de JVM {#jvm-parameters}

Defina los siguientes parámetros de JVM:

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=verdadero

## Almacenamiento de datos y configuración de memoria {#data-store-and-memory-configuration}

### Configuración del almacén de datos de archivos {#file-data-store-configuration}

Se recomienda separar el almacén de datos del almacén de segmentos para todos [!DNL Experience Manager Assets] los usuarios. Además, la configuración de los parámetros `maxCachedBinarySize` y `cacheSizeInMB` puede ayudar a maximizar el rendimiento. Establezca `maxCachedBinarySize` el tamaño de archivo más pequeño que se puede guardar en la caché. Especifique el tamaño de la caché en memoria que se va a usar para el almacén de datos dentro de `cacheSizeInMB`. Adobe recomienda configurar este valor entre el 2 y el 10 por ciento del tamaño total del montón. Sin embargo, las pruebas de carga y rendimiento pueden ayudar a determinar la configuración ideal.

### Configurar el tamaño máximo de la caché de imágenes en búfer {#configure-the-maximum-size-of-the-buffered-image-cache}

Al cargar grandes cantidades de recursos en [!DNLAAdobe Experience Manager], para permitir picos inesperados en el consumo de memoria y evitar que JVM falle con OutOfMemoryErrors, reduzca el tamaño máximo configurado de la caché de imágenes en memoria intermedia. Considere un ejemplo en el que tiene un sistema con una pila máxima (- `Xmx`param) de 5 GB, un Oak BlobCache establecido en 1 GB y una caché de documento establecida en 2 GB. En este caso, la memoria caché almacenada en el búfer requeriría un máximo de 1,25 GB y memoria, lo que dejaría sólo 0,75 GB de memoria para picos inesperados.

Configure el tamaño de caché en búfer en la consola web OSGi. En `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`, establezca la propiedad `cq.dam.image.cache.max.memory` en bytes. Por ejemplo, 1073741824 es 1 GB (1024 x 1024 x 1024 = 1 GB).

Desde Experience Manager 6.1 SP1, si está utilizando un `sling:osgiConfig` nodo para configurar esta propiedad, asegúrese de establecer el tipo de datos en Long. Para obtener más información, consulte [CQBufferedImageCache consume mucha información durante las cargas](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html)de recursos.

### Almacenes de datos compartidos {#shared-data-stores}

La implementación de un almacén de datos de archivos compartidos o S3 puede ayudar a ahorrar espacio en disco y aumentar el rendimiento de la red en implementaciones a gran escala. Para obtener más información sobre los pros y los contras del uso de un almacén de datos compartido, consulte Guía [de tamaño de](/help/assets/assets-sizing-guide.md)recursos.

### S3 data store {#s-data-store}

La siguiente configuración del almacén de datos S3 ( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`) ayudó a Adobe a extraer 12,8 TB de objetos binarios grandes (BLOB) de un almacén de datos de archivos existente en un almacén de datos S3 en un sitio del cliente:

```conf
accessKey=<snip>
 secretKey=<snip>
 s3Bucket=<snip>
 s3Region=us-standard
 s3EndPoint=<a href="https://s3.amazonaws.com/">s3.amazonaws.com</a>
 connectionTimeout=120000
 socketTimeout=120000
 maxConnections=80
 writeThreads=60
 concurrentUploadsThreads=30
 asyncUploadLimit=30
 maxErrorRetry=1000
 path=/opt/author/crx-quickstart/repository/datastore
 s3RenameKeys=false
 s3Encryption=SSE_S3
 proactiveCaching=true
 uploadRetries=1000
 migrateFailuresCount=400
```

## Optimización de la red {#network-optimization}

Adobe recomienda habilitar HTTPS porque muchas compañías tienen cortafuegos que detectan el tráfico HTTP, lo que afecta negativamente a las cargas y corrompe los archivos. Para cargas de archivos de gran tamaño, asegúrese de que los usuarios tienen conexiones cableadas a la red porque una red WiFi se satura rápidamente. Para obtener instrucciones sobre cómo identificar cuellos de botella de red, consulte Guía [de tamaño de](/help/assets/assets-sizing-guide.md)recursos. Para evaluar el rendimiento de la red mediante el análisis de la topología de la red, consulte Consideraciones [de la red de](/help/assets/assets-network-considerations.md)Assets.

Principalmente, su estrategia de optimización de red depende de la cantidad de ancho de banda disponible y de la carga de la instancia de [!DNLEExperience Manager] . Las opciones de configuración comunes, incluyendo servidores de seguridad o proxies, pueden ayudar a mejorar el rendimiento de la red. Estos son algunos de los puntos clave a tener en cuenta:

* En función del tipo de instancia (pequeña, moderada y grande), asegúrese de que dispone de ancho de banda de red suficiente para la instancia de Experience Manager. La asignación adecuada del ancho de banda es especialmente importante si [!DNLEExperience Manager] está alojado en AWS.
* Si la instancia de [!DNLEExperience Manager] está alojada en AWS, puede beneficiarse de una política de escala versátil. Actualice la instancia si los usuarios esperan una carga alta. Disminuya el tamaño para una carga moderada o baja.
* HTTPS: La mayoría de los usuarios tiene servidores de seguridad que detectan el tráfico HTTP, lo que puede afectar negativamente a la carga de archivos o incluso dañar archivos durante la operación de carga.
* Cargas de archivos grandes: Asegúrese de que los usuarios tienen conexiones cableadas a la red (las conexiones Wi-Fi se saturan rápidamente).

## Flujos de trabajo {#workflows}

### flujos de trabajo transitorios {#transient-workflows}

Siempre que sea posible, establezca el flujo de trabajo de recursos [!UICONTROL de actualización de] DAM en Temporal. La configuración reduce considerablemente los gastos generales necesarios para procesar flujos de trabajo porque, en este caso, los flujos de trabajo no necesitan pasar por los procesos normales de seguimiento y archivo.

1. Vaya a `/miscadmin` la instancia de [!DNLEExperience Manager] en `https://[aem_server]:[port]/miscadmin`.

1. Expanda **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]** > **[!UICONTROL presa]**.

1. Abra **[!UICONTROL DAM Update Asset]**. En el panel de herramientas flotante, cambie a la ficha **[!UICONTROL Página]** y, a continuación, haga clic en Propiedades **[!UICONTROL de página]**.

1. Select **[!UICONTROL Transient Workflow]** and click **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Algunas funciones no admiten flujos de trabajo transitorios. Si la implementación [!DNL Assets] requiere estas funciones, no configure flujos de trabajo transitorios.

En los casos en los que no se pueden usar flujos de trabajo transitorios, ejecute la depuración regular del flujo de trabajo para eliminar flujos de trabajo de recursos [!UICONTROL de actualización de] DAM archivados para garantizar que el rendimiento del sistema no se deteriore.

Generalmente, ejecute los flujos de trabajo de depuración semanalmente. Sin embargo, en situaciones de uso intensivo de recursos, como durante la ingestión de recursos a gran escala, puede ejecutarlo con más frecuencia.

Para configurar la depuración del flujo de trabajo, agregue una nueva configuración de depuración del flujo de trabajo de Adobe Granite a través de la consola OSGi. A continuación, configure y programe el flujo de trabajo como parte de la ventana de mantenimiento semanal.

Si la purga dura demasiado tiempo, se agota el tiempo de espera. Por lo tanto, debe asegurarse de que los trabajos de depuración se completen para evitar situaciones en las que los flujos de trabajo de purga no se completen debido al elevado número de flujos de trabajo.

Por ejemplo, después de ejecutar numerosos flujos de trabajo no transitorios (que crean nodos de instancia de flujo de trabajo), puede ejecutar [ACS AEM Commons Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) de forma ad-hoc. Elimina inmediatamente las instancias de flujo de trabajo redundantes y completadas en lugar de esperar a que se ejecute el Planificador de purga de flujo de trabajo de Adobe Granite.

### Número máximo de trabajos en paralelo {#maximum-parallel-jobs}

De forma predeterminada, [!DNLEExperience Manager] ejecuta un número máximo de trabajos paralelos igual al número de procesadores del servidor. El problema con esta configuración es que durante períodos de carga pesada, todos los procesadores están ocupados por flujos de trabajo de recursos [!UICONTROL de actualización de] DAM, lo que ralentiza la capacidad de respuesta de la interfaz de usuario e impide que [!DNLEExperience Manager] ejecute otros procesos que salvaguardan el rendimiento y la estabilidad del servidor. Como práctica recomendada, ajuste este valor a la mitad de los procesadores disponibles en el servidor realizando los siguientes pasos:

1. En [!DNLEExperience Manager] Author, acceda a `https://[aem_server]:[port]/system/console/slingevent`.

1. Haga clic en **[!UICONTROL Editar]** en cada cola de flujo de trabajo que sea relevante para la implementación, por ejemplo, **[!UICONTROL Granite Transient Workflow Queue]**.

1. Actualice el valor de **[!UICONTROL Número máximo de trabajos]** paralelos y haga clic en **[!UICONTROL Guardar]**.

Establecer una cola en la mitad de los procesadores disponibles es una solución viable para el inicio. Sin embargo, es posible que tenga que aumentar o disminuir este número para lograr el máximo rendimiento y ajustarlo por entorno. Hay colas independientes para flujos de trabajo transitorios y no transitorios, así como para otros procesos, como flujos de trabajo externos. Si varias colas configuradas en el 50% de los procesadores están activas simultáneamente, el sistema puede sobrecargarse rápidamente. Las colas que se utilizan con frecuencia varían considerablemente según las implementaciones de los usuarios. Por lo tanto, es posible que tenga que configurarlas cuidadosamente para lograr la máxima eficacia sin sacrificar la estabilidad del servidor.

### Configuración del recurso de actualización DAM {#dam-update-asset-configuration}

El flujo de trabajo de recursos [!UICONTROL de actualización de] DAM contiene un conjunto completo de pasos configurados para tareas, como la generación y la integración de Scene7 PTIFF [!DNL Adobe InDesign Server] . Sin embargo, es posible que la mayoría de los usuarios no requieran varios de estos pasos. Adobe recomienda crear una copia personalizada del modelo de flujo de trabajo de recursos [!UICONTROL de actualización de] DAM y eliminar los pasos innecesarios. En este caso, actualice los lanzadores de [!UICONTROL DAM Update Asset] para que apunten al nuevo modelo.

La ejecución intensiva del flujo de trabajo de recursos [!UICONTROL de actualización de] DAM puede aumentar considerablemente el tamaño del almacén de datos de archivos. Los resultados de un experimento realizado por Adobe han demostrado que el tamaño del almacén de datos puede aumentar en aproximadamente 400 GB si se realizan alrededor de 5500 flujos de trabajo en un plazo de 8 horas.

Se trata de un aumento temporal y el almacén de datos se restaura a su tamaño original después de ejecutar la tarea de recolección de elementos no utilizados del almacén de datos.

Normalmente, la tarea de recolección de elementos no utilizados del almacén de datos se ejecuta semanalmente junto con otras tareas de mantenimiento programadas.

Si tiene un espacio limitado en disco y ejecuta los flujos de trabajo de recursos [!UICONTROL de actualización de] DAM intensamente, considere programar la tarea de recolección de elementos no utilizados con más frecuencia.

#### Generación de representaciones en tiempo de ejecución {#runtime-rendition-generation}

Los clientes utilizan imágenes de diversos tamaños y formatos en su sitio web o para su distribución a socios comerciales. Dado que cada representación se añade a la huella del recurso en el repositorio, Adobe recomienda utilizar esta función con prudencia. Para reducir la cantidad de recursos necesarios para procesar y almacenar imágenes, puede generar estas imágenes en tiempo de ejecución en lugar de como representaciones durante la ingestión.

Muchos clientes de Sitios implementan un servlet de imagen que cambia el tamaño y recorta las imágenes en el momento en que se solicitan, lo que impone una carga adicional en la instancia de publicación. Sin embargo, mientras estas imágenes se puedan almacenar en caché, el desafío se puede mitigar.

Un método alternativo es utilizar la tecnología de Scene7 para eliminar por completo la manipulación de imágenes. Además, puede implementar Brand Portal que no solo se haga cargo de las responsabilidades de generación de representaciones de la infraestructura del Administrador de [!DNLEexperiencias] , sino también de todo el nivel de publicación.

#### ImageMagick {#imagemagick}

Si personaliza el flujo de trabajo de recursos [!UICONTROL de actualización de] DAM para generar representaciones mediante ImageMagick, Adobe recomienda modificar el `policy.xml` archivo en `/etc/ImageMagick/`. De forma predeterminada, ImageMagick utiliza todo el espacio de disco disponible en el volumen del sistema operativo y la memoria disponible. Realice los siguientes cambios en la configuración dentro de la `policymap` sección de `policy.xml` para limitar estos recursos.

```xml
<policymap>
  <!-- <policy domain="system" name="precision" value="6"/> -->
  <policy domain="resource" name="temporary-path" value="/ephemeral0/imagemagick_tmp"/>
  <policy domain="resource" name="memory" value="1000MiB"/>
  <policy domain="resource" name="map" value="1000MiB"/>
  <!-- <policy domain="resource" name="area" value="1gb"/> -->
  <policy domain="resource" name="disk" value="10000MiB"/>
  <!-- <policy domain="resource" name="file" value="768"/> -->
  <policy domain="resource" name="thread" value="1"/>
  <policy domain="resource" name="throttle" value="50"/>
  <!-- <policy domain="resource" name="time" value="3600"/> -->
</policymap>
```

Además, establezca la ruta de la carpeta temporal de ImageMagick en el `configure.xml` archivo (o estableciendo la variable de entorno `MAGIC_TEMPORARY_PATH`) en una partición de disco que tenga suficiente espacio y IOPS.

>[!CAUTION]
>
>Una configuración incorrecta puede hacer que el servidor sea inestable si ImageMagick utiliza todo el espacio disponible en el disco. Los cambios de política necesarios para procesar archivos de gran tamaño con ImageMagick pueden afectar al rendimiento del Administrador de [!DNLEexperiencias] . Para obtener más información, consulte [Instalación y configuración de ImageMagick](/help/assets/best-practices-for-imagemagick.md).

>[!NOTE]
>
>ImageMagick `policy.xml` y `configure.xml` los archivos están disponibles en `/usr/lib64/ImageMagick-&#42;/config/` lugar de `/etc/ImageMagick/`.Consulte la documentación [de](https://www.imagemagick.org/script/resources.php) ImageMagick para la ubicación de los archivos de configuración.

Si utiliza [!DNL Experience Manager] Adobes Managed Services (AMS), póngase en contacto con el Servicio de atención al cliente de Adobe si tiene previsto procesar muchos archivos PSD o PSB de gran tamaño. Póngase en contacto con el representante del Servicio de atención al cliente de Adobe para implementar estas optimizaciones para la implementación de AMS y para elegir las mejores herramientas y modelos posibles para los formatos propietarios de Adobe. [!DNL Experience Manager] es posible que no procese archivos PSB de alta resolución que superen los 30000 x 23000 píxeles.

### XMP writeback {#xmp-writeback}

La reescritura XMP actualiza el recurso original cada vez que se modifican los metadatos en [!DNL Experience Manager], lo que resulta en lo siguiente:

* Se modifica el recurso mismo
* Se crea una versión del recurso
* [!UICONTROL El recurso] de actualización DAM se ejecuta con el recurso

Los resultados de la lista consumen recursos considerables. Por lo tanto, Adobe recomienda [desactivar la reescritura](https://helpx.adobe.com/experience-manager/kb/disable-xmp-writeback.html)XMP si no es necesaria.

La importación de una gran cantidad de metadatos puede dar como resultado una actividad de reescritura XMP intensiva en recursos si se marca el indicador de flujos de trabajo de ejecución. Planifique una importación de este tipo durante el uso del servidor liso para que el rendimiento de otros usuarios no se vea afectado.

## Replicación {#replication}

Al replicar recursos en un gran número de instancias de publicación, por ejemplo en una implementación de sitios, Adobe recomienda utilizar la replicación en cadena. En este caso, la instancia de autor se replica en una única instancia de publicación que, a su vez, se replica en las otras instancias de publicación, lo que libera la instancia de autor.

### Configurar replicación de cadenas {#configure-chain-replication}

1. Elija la instancia de publicación que desea utilizar para encadenar las replicaciones a
1. En esa instancia de publicación, agregue agentes de replicación que apunten a otras instancias de publicación
1. En cada uno de esos agentes de replicación, habilite &quot;Al recibir&quot; en la ficha &quot;Desencadenadores&quot;

>[!NOTE]
>
>Adobe no recomienda la activación automática de recursos. Sin embargo, si es necesario, Adobe recomienda que esto sea el último paso de un flujo de trabajo, normalmente DAM Update Asset.

## Índices de búsqueda {#search-indexes}

Asegúrese de implementar los Service Packs más recientes y las revisiones relacionadas con el rendimiento, ya que suelen incluir actualizaciones en los índices del sistema. Consulte Sugerencias [de ajuste de](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) rendimiento para obtener optimizaciones de índice.

Cree índices personalizados para consultas que se ejecutan con frecuencia. Para obtener más información, consulte [metodología para analizar consultas](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) lentas y [diseñar índices](/help/sites-deploying/queries-and-indexing.md)personalizados. Para obtener más información sobre las optimizaciones de consulta e índice, consulte [Prácticas recomendadas para Consultas e indexación](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Configuraciones de índice de Lucene {#lucene-index-configurations}

Se pueden realizar algunas optimizaciones en las configuraciones de índice Oak que pueden ayudar a mejorar [!DNL Experience Manager Assets] el rendimiento. Actualice las configuraciones de índice para mejorar el tiempo de reindexación:

1. Abra CRXDe `/crx/de/index.jsp` e inicie sesión como usuario administrativo.
1. Vaya a `/oak:index/lucene`.
1. Añada una `String[]` propiedad `excludedPaths` con valores `/var`, `/etc/workflow/instances`y `/etc/replication`.
1. Vaya a `/oak:index/damAssetLucene`. Añada una `String[]` propiedad `includedPaths` con valor `/content/dam`. Guarde los cambios.

Si los usuarios no necesitan realizar una búsqueda de texto completo de recursos, por ejemplo, buscando texto en documentos PDF, desactívelo. Para mejorar el rendimiento del índice, deshabilite la indexación de texto completo. Para desactivar la extracción [!DNL Apache Lucene] de texto, siga estos pasos:

1. En [!DNL Experience Manager] la interfaz, acceda al Administrador [!UICONTROL de paquetes].
1. Cargue e instale el paquete disponible en [disable_indexingbinarytextextract-10.zip](assets/disable_indexingbinarytextextraction-10.zip).

### Total de asistentes {#guess-total}

Cuando cree consultas que generen grandes conjuntos de resultados, utilice el `guessTotal` parámetro para evitar una utilización excesiva de la memoria al ejecutarlos.

## Problemas conocidos {#known-issues}

### Archivos grandes {#large-files}

Existen dos problemas conocidos principales relacionados con archivos de gran tamaño en [!DNL Experience Manager]. Cuando los archivos alcanzan tamaños buenos de 2 GB, la sincronización en espera en frío puede encontrarse en una situación de memoria insuficiente. En algunos casos, evita que se ejecute la sincronización en espera. En otros casos, provoca el bloqueo de la instancia principal. Este escenario se aplica a cualquier archivo de [!DNL Experience Manager] más de 2 GB, incluidos los paquetes de contenido.

Del mismo modo, cuando los archivos alcanzan los 2 GB de tamaño mientras se utiliza un almacén de datos S3 compartido, puede que tarde algún tiempo en que el archivo permanezca completamente desde la caché hasta el sistema de archivos. Como resultado, al utilizar la replicación sin binarios, es posible que los datos binarios no se hayan mantenido antes de que se complete la replicación. Esta situación puede dar lugar a problemas, especialmente si la disponibilidad de datos es importante.

## Pruebas de rendimiento {#performance-testing}

Para cada [!DNL Experience Manager] implementación, establezca un régimen de pruebas de rendimiento que pueda identificar y resolver rápidamente los cuellos de botella. A continuación se indican algunas áreas clave en las que centrar la atención.

### Pruebas de red {#network-testing}

Para todos los problemas de rendimiento de la red del cliente, realice las siguientes tareas:

* Probar el rendimiento de la red desde la red del cliente
* Compruebe el rendimiento de la red desde la red de Adobe. Para los clientes de AMS, trabaje con su CSE para realizar pruebas desde la red de Adobe.
* Probar el rendimiento de la red desde otro punto de acceso
* Mediante el uso de una herramienta de referencia de red
* Prueba con el despachante

### [!DNL Experience Manager] prueba de instancia {#aem-instance-testing}

Para minimizar la latencia y lograr un alto rendimiento mediante la utilización eficiente de la CPU y el uso compartido de la carga, supervise el rendimiento de su [!DNL Experience Manager] instancia de forma regular. En particular:

* Ejecute pruebas de carga con la [!DNL Experience Manager] instancia.
* Monitoree el rendimiento de carga y la capacidad de respuesta de la interfaz de usuario.

## [!DNL Experience Manager Assets] lista de comprobación de rendimiento e impacto de las tareas de administración de activos {#checklist}

* Active HTTPS para evitar cualquier husmeador de tráfico HTTP corporativo.
* Utilice una conexión por cable para cargar recursos en exceso.
* Implementar en Java 8.
* Configure parámetros JVM óptimos.
* Configure un almacén de datos del sistema de archivos o un almacén de datos S3.
* Deshabilitar la generación de subrecursos. Si está activado, el flujo de trabajo de AEM crea un recurso independiente para cada página en un recurso de varias páginas. Cada una de estas páginas es un recurso individual que consume espacio en disco adicional, requiere control de versiones y procesamiento adicional del flujo de trabajo. Si no necesita páginas independientes, deshabilite la generación de subrecursos y las actividades de extracción de página.
* Habilitar flujos de trabajo transitorios.
* Ajuste las colas de flujo de trabajo de Granite para limitar los trabajos simultáneos.
* Configure [!DNL ImageMagick] para limitar el consumo de recursos.
* Elimine los pasos innecesarios del flujo de trabajo de recursos [!UICONTROL de actualización de] DAM.
* Configure el flujo de trabajo y la depuración de versiones.
* Optimice los índices con los paquetes de servicios y revisiones más recientes. Consulte con el Servicio de atención al cliente de Adobe si hay optimizaciones de índice adicionales disponibles.
* Use adivinen el total para optimizar el rendimiento de la consulta.
* If you configure [!DNL Experience Manager] to detect file types from the content of the files (by enabling **[!UICONTROL Day CQ DAM Mime Type Service]** in the **[!UICONTROL AEM Web Console]**), upload many files in bulk during non-peak hours as it is resource-intensive.
