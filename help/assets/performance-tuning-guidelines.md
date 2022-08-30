---
title: Ajuste del rendimiento [!DNL Assets].
description: Sugerencias y sugerencias sobre [!DNL Experience Manager] configuración, cambios en hardware, software y componentes de red para eliminar cuellos de botella y optimizar el rendimiento de [!DNL Experience Manager Assets].
contentOwner: AG
mini-toc-levels: 1
role: Architect, Admin
feature: Asset Management
exl-id: 1d9388de-f601-42bf-885b-6a7c3236b97e
source-git-commit: e3caa3e3067cf5e29cfcdf4286047eb346aefa23
workflow-type: tm+mt
source-wordcount: '2753'
ht-degree: 0%

---

<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] guía de ajuste del rendimiento {#assets-performance-tuning-guide}

Un [!DNL Experience Manager Assets] configuración contiene varios componentes de hardware, software y red. Según el escenario de implementación, es posible que necesite cambios específicos en la configuración del hardware, software y componentes de red para eliminar los cuellos de botella en el rendimiento.

Además, identificar y cumplir ciertas directrices de optimización de hardware y software le ayuda a crear una base sólida que le permita [!DNL Experience Manager Assets] implementación para satisfacer las expectativas de rendimiento, escalabilidad y fiabilidad.

Rendimiento deficiente en [!DNL Experience Manager Assets] puede afectar a la experiencia del usuario en el rendimiento interactivo, el procesamiento de recursos, la velocidad de descarga y otras áreas.

De hecho, la optimización del rendimiento es una tarea fundamental que se realiza antes de establecer métricas de objetivo para cualquier proyecto.

Estas son algunas áreas clave en las que puede descubrir y solucionar problemas de rendimiento antes de que afecten a los usuarios.

## Plataforma {#platform}

Aunque Experience Manager es compatible con varias plataformas, Adobe ha encontrado el soporte bueno para herramientas nativas en Linux y Windows, lo que contribuye a un rendimiento óptimo y a una implementación más sencilla. Lo ideal es implementar un sistema operativo de 64 bits para satisfacer los altos requerimientos de memoria de un [!DNL Experience Manager Assets] implementación. Al igual que con cualquier implementación de Experience Manager, debe implementar TarMK siempre que sea posible. Aunque TarMK no puede escalar más allá de una única instancia de autor, se ha descubierto que funciona mejor que MongoMK. Puede añadir instancias de descarga de TarMK para aumentar el poder de procesamiento del flujo de trabajo de su [!DNL Experience Manager Assets] implementación.

### Carpeta temporal {#temp-folder}

Para mejorar los tiempos de carga de los recursos, utilice almacenamiento de alto rendimiento para el directorio temporal de Java. En Linux y Windows, se puede utilizar una unidad RAM o SSD. En entornos basados en la nube, se podría utilizar un tipo de almacenamiento de alta velocidad equivalente. Por ejemplo, en Amazon EC2, una [unidad efímera](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) para la carpeta temporal.

Si el servidor tiene suficiente memoria, configure una unidad RAM. En Linux, ejecute estos comandos para crear una unidad RAM de 8 GB:

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

En el sistema operativo Windows, utilice un controlador de terceros para crear una unidad RAM o utilice almacenamiento de alto rendimiento como SSD.

Una vez que el volumen temporal de alto rendimiento esté listo, establezca el parámetro JVM `-Djava.io.tmpdir`. Por ejemplo, puede agregar el parámetro JVM siguiente al `CQ_JVM_OPTS` en la variable `bin/start` secuencia de comandos de [!DNL Experience Manager]:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Configuración de Java {#java-configuration}

### Versión de Java {#java-version}

Adobe recomienda implementar [!DNL Experience Manager Assets] en Java 8 para un rendimiento óptimo.

<!-- TBD: Link to the latest official word around Java.
-->

### Parámetros de JVM {#jvm-parameters}

Establezca los siguientes parámetros de JVM:

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=verdadero

## Configuración del almacén de datos y la memoria {#data-store-and-memory-configuration}

### Configuración del almacén de datos de archivo {#file-data-store-configuration}

Se recomienda separar el almacén de datos del almacén de segmentos para todos [!DNL Experience Manager Assets] usuarios. Además, la configuración de la variable `maxCachedBinarySize` y `cacheSizeInMB` los parámetros pueden ayudar a maximizar el rendimiento. Establezca `maxCachedBinarySize` al tamaño de archivo más pequeño que se puede guardar en la caché. Especifique el tamaño de la caché en memoria que se utilizará para el almacén de datos en `cacheSizeInMB`. Adobe recomienda establecer este valor entre el 2 % y el 10 % del tamaño total de pila. Sin embargo, las pruebas de carga/rendimiento pueden ayudar a determinar la configuración ideal.

### Configurar el tamaño máximo de la caché de imágenes almacenada en búfer {#configure-the-maximum-size-of-the-buffered-image-cache}

Al cargar grandes cantidades de recursos en [!DNL Adobe Experience Manager], para permitir picos inesperados en el consumo de memoria y para evitar que JVM falle con OutOfMemoryErrors, reduzca el tamaño máximo configurado de la caché de imágenes almacenada en búfer. Tomemos un ejemplo de que tiene un sistema con una pila máxima (- `Xmx`param) de 5 GB, un Oak BlobCache establecido en 1 GB y una caché de documentos configurada en 2 GB. En este caso, la caché almacenada en búfer tomaría un máximo de 1,25 GB y memoria, lo que dejaría solo 0,75 GB de memoria para picos inesperados.

Configure el tamaño de caché en búfer en la consola web OSGi. At `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`, establezca la propiedad `cq.dam.image.cache.max.memory` en bytes. Por ejemplo, 1073741824 es 1 GB (1024 x 1024 x 1024 = 1 GB).

Desde Experience Manager 6.1 SP1, si utiliza un `sling:osgiConfig` para configurar esta propiedad, asegúrese de establecer el tipo de datos en Long. Para obtener más información, consulte [CQBufferedImageCache consume mucho durante las cargas de recursos](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html).

### Almacenes de datos compartidos {#shared-data-stores}

La implementación de un almacén de datos de archivos compartidos o S3 puede ayudar a ahorrar espacio en disco y aumentar el rendimiento de la red en implementaciones a gran escala. Para obtener más información sobre las ventajas y desventajas de utilizar un almacén de datos compartido, consulte [Guía de tamaño de recursos](/help/assets/assets-sizing-guide.md).

### Almacén de datos S3 {#s-data-store}

La siguiente configuración del almacén de datos S3 ( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`) ayudó a extraer 12,8 TB de objetos grandes binarios (BLOB) de un almacén de datos de archivos existente en un almacén de datos S3 en un sitio del cliente:

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

Adobe recomienda habilitar HTTPS porque muchas empresas tienen cortafuegos que olfatean el tráfico HTTP, lo que afecta negativamente a las cargas y corrompe los archivos. Para cargas de archivos grandes, asegúrese de que los usuarios tengan conexiones cableadas a la red porque una red WiFi se satura rápidamente. Para obtener instrucciones sobre la identificación de cuellos de botella de red, consulte [Guía de tamaño de recursos](/help/assets/assets-sizing-guide.md). Para evaluar el rendimiento de la red analizando la topología de la red, consulte [Consideraciones sobre la red de recursos](/help/assets/assets-network-considerations.md).

Principalmente, su estrategia de optimización de red depende de la cantidad de ancho de banda disponible y de la carga de su [!DNL Experience Manager] instancia. Las opciones de configuración comunes, incluidos los cortafuegos o los proxies, pueden ayudar a mejorar el rendimiento de la red. Estos son algunos puntos clave a tener en cuenta:

* Dependiendo del tipo de instancia (pequeño, moderado, grande), asegúrese de que tiene suficiente ancho de banda de red para la instancia de Experience Manager. La asignación adecuada del ancho de banda es especialmente importante si [!DNL Experience Manager] está alojado en AWS.
* Si su [!DNL Experience Manager] está alojada en AWS, lo que le permite beneficiarse de tener una política de escalado versátil. Actualice la instancia si los usuarios esperan una carga alta. Desactívelo para una carga moderada/baja.
* HTTPS: La mayoría de los usuarios tienen cortafuegos que olfatean el tráfico HTTP, lo que puede afectar negativamente a la carga de archivos o incluso a los archivos dañados durante la operación de carga.
* Cargas de archivos grandes: Asegúrese de que los usuarios tengan conexiones cableadas a la red (las conexiones WiFi se saturan rápidamente).

## Flujos de trabajo {#workflows}

### Flujos de trabajo transitorios {#transient-workflows}

Siempre que sea posible, establezca la variable [!UICONTROL Recurso de actualización DAM] flujo de trabajo a Transient. La configuración reduce significativamente los gastos generales necesarios para procesar flujos de trabajo porque, en este caso, los flujos de trabajo no necesitan pasar por los procesos normales de seguimiento y archivo.

1. Vaya a `/miscadmin` en el [!DNL Experience Manager] implementación en `https://[aem_server]:[port]/miscadmin`.

1. Expandir **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]** > **[!UICONTROL dam]**.

1. Apertura **[!UICONTROL Recurso de actualización DAM]**. Desde el panel de herramientas flotante, cambie a la **[!UICONTROL Página]** y, a continuación, haga clic en **[!UICONTROL Propiedades de página]**.

1. Select **[!UICONTROL Flujo de trabajo transitorio]** y haga clic en **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Algunas funciones no admiten flujos de trabajo transitorios. Si su [!DNL Assets] la implementación requiere estas funciones, no configure flujos de trabajo transitorios.

En los casos en los que no se puedan utilizar flujos de trabajo transitorios, ejecute el flujo de trabajo purgando regularmente para eliminar los archivados [!UICONTROL Recurso de actualización DAM] flujos de trabajo para garantizar que el rendimiento del sistema no se degrada.

Normalmente, ejecute los flujos de trabajo de depuración semanalmente. Sin embargo, en escenarios con gran densidad de recursos, como durante la ingesta de recursos a gran escala, puede ejecutarlo con mayor frecuencia.

Para configurar la depuración del flujo de trabajo, añada una nueva configuración de Adobe Granite Workflow Purge a través de la consola OSGi. A continuación, configure y programe el flujo de trabajo como parte de la ventana de mantenimiento semanal.

Si la depuración se ejecuta durante demasiado tiempo, se agota el tiempo de espera. Por lo tanto, debe asegurarse de que los trabajos de depuración se completen para evitar situaciones en las que los flujos de trabajo de depuración no se completen debido al alto número de flujos de trabajo.

Por ejemplo, después de ejecutar numerosos flujos de trabajo no transitorios (que crean nodos de instancia de flujo de trabajo), puede ejecutar [Flujo de trabajo ACS AEM Commons Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) según sea necesario. Elimina inmediatamente las instancias de flujo de trabajo redundantes y completadas en lugar de esperar a que se ejecute el programador de purga de flujo de trabajo de Granite de Adobe.

### Máximo de trabajos paralelos {#maximum-parallel-jobs}

De forma predeterminada, [!DNL Experience Manager] ejecuta un número máximo de trabajos paralelos igual al número de procesadores en el servidor. El problema con esta configuración es que durante períodos de carga pesada, todos los procesadores están ocupados por [!UICONTROL Recurso de actualización DAM] flujos de trabajo, ralentización de la capacidad de respuesta de la interfaz de usuario y prevención [!DNL Experience Manager] de ejecutar otros procesos que salvaguarden el rendimiento y la estabilidad del servidor. Como práctica recomendada, establezca este valor en la mitad de los procesadores disponibles en el servidor realizando los siguientes pasos:

1. Activado [!DNL Experience Manager] Autor, acceso `https://[aem_server]:[port]/system/console/slingevent`.

1. Haga clic en **[!UICONTROL Editar]** en cada cola de flujo de trabajo relevante para la implementación, por ejemplo **[!UICONTROL Cola de flujo de trabajo transitorio de Granite]**.

1. Actualizar el valor de **[!UICONTROL Trabajos paralelos máximos]** y haga clic en **[!UICONTROL Guardar]**.

Establecer una cola para la mitad de los procesadores disponibles es una solución viable para empezar. Sin embargo, es posible que tenga que aumentar o reducir este número para lograr el máximo rendimiento y ajustarlo por entorno. Existen colas independientes para flujos de trabajo transitorios y no transitorios, así como otros procesos, como flujos de trabajo externos. Si varias colas configuradas en el 50% de los procesadores están activos simultáneamente, el sistema puede sobrecargarse rápidamente. Las colas que se utilizan con frecuencia varían considerablemente entre las implementaciones de los usuarios. Por lo tanto, es posible que tenga que configurarlos cuidadosamente para lograr la máxima eficiencia sin sacrificar la estabilidad del servidor.

### Configuración de recursos de actualización DAM {#dam-update-asset-configuration}

La variable [!UICONTROL Recurso de actualización DAM] flujo de trabajo contiene un conjunto completo de pasos que se configuran para tareas como la generación de Dynamic Media PTIFF y [!DNL Adobe InDesign Server] integración. Sin embargo, es posible que la mayoría de los usuarios no necesiten varios de estos pasos. Adobe recomienda crear una copia personalizada del [!UICONTROL Recurso de actualización DAM] modelo de flujo de trabajo y elimine los pasos innecesarios. En este caso, actualice los lanzadores para [!UICONTROL Recurso de actualización DAM] para apuntar al nuevo modelo.

Ejecución de [!UICONTROL Recurso de actualización DAM] El flujo de trabajo puede aumentar considerablemente el tamaño del almacén de datos del archivo. Los resultados de un experimento realizado por Adobe han demostrado que el tamaño del almacén de datos puede aumentar aproximadamente en 400 GB si se realizan alrededor de 5500 flujos de trabajo en un plazo de 8 horas.

Es un aumento temporal y el almacén de datos se restaura a su tamaño original después de ejecutar la tarea de recolección de residuos del almacén de datos.

Normalmente, la tarea de recolección de basura del almacén de datos se ejecuta semanalmente junto con otras tareas de mantenimiento programadas.

Si tiene un espacio de disco limitado y ejecuta [!UICONTROL Recurso de actualización DAM] flujos de trabajo intensamente, considere la posibilidad de programar la tarea de colección de residuos con más frecuencia.

#### Generación de representaciones en tiempo de ejecución {#runtime-rendition-generation}

Los clientes utilizan imágenes de diversos tamaños y formatos en su sitio web o para su distribución a socios comerciales. Dado que cada representación se añade a la huella del recurso en el repositorio, Adobe recomienda utilizar esta función con cautela. Para reducir la cantidad de recursos necesarios para procesar y almacenar imágenes, puede generar estas imágenes en tiempo de ejecución en lugar de como representaciones durante la ingesta.

Muchos clientes de Sites implementan un servlet de imagen que cambia el tamaño y recorta las imágenes en el momento en que se solicitan, lo que impone una carga adicional en la instancia de publicación. Sin embargo, mientras estas imágenes se puedan almacenar en caché, el desafío se puede mitigar.

Un enfoque alternativo es usar la tecnología de Dynamic Media para evitar por completo la manipulación de imágenes. Además, puede implementar Brand Portal que no solo se haga cargo de las responsabilidades de generación de variantes de representación de [!DNL Experience Manager] infraestructura, pero también todo el nivel de publicación.

#### ImageMagick {#imagemagick}

Si personaliza la variable [!UICONTROL Recurso de actualización DAM] para generar representaciones con ImageMagick, Adobe recomienda modificar el `policy.xml` file at `/etc/ImageMagick/`. De forma predeterminada, ImageMagick utiliza todo el espacio de disco disponible en el volumen del sistema operativo y la memoria disponible. Realice los siguientes cambios de configuración dentro del `policymap` sección de `policy.xml` para limitar estos recursos.

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

Además, establezca la ruta de la carpeta temporal de ImageMagick en la variable `configure.xml` (o configurando la variable de entorno `MAGICK_TEMPORARY_PATH`) a una partición de disco que tenga suficiente espacio y IOPS.

>[!CAUTION]
>
>Una mala configuración puede hacer que su servidor sea inestable si ImageMagick utiliza todo el espacio disponible en disco. Los cambios de política necesarios para procesar archivos de gran tamaño con ImageMagick pueden afectar a la [!DNL Experience Manager] rendimiento. Para obtener más información, consulte [instalar y configurar ImageMagick](/help/assets/best-practices-for-imagemagick.md).

>[!NOTE]
>
>ImageMagick `policy.xml` y `configure.xml` los archivos están disponibles en `/usr/lib64/ImageMagick-&#42;/config/` en lugar de `/etc/ImageMagick/`.Consulte [Documentación de ImageMagick](https://www.imagemagick.org/script/resources.php) para la ubicación de los archivos de configuración.

Si está utilizando [!DNL Experience Manager] en Adobe Managed Services (AMS), póngase en contacto con el servicio de asistencia al cliente de Adobe si tiene pensado procesar muchos archivos de PSD o PSB de gran tamaño. Trabaje con el representante de asistencia al cliente de Adobe para implementar estas prácticas recomendadas para su implementación de AMS y elegir las mejores herramientas y modelos posibles para los formatos propietarios de Adobe. [!DNL Experience Manager] es posible que no procese archivos PSB de alta resolución que superen los 30000 x 23000 píxeles.

### XMP reescritura {#xmp-writeback}

XMP reescritura actualiza el recurso original cada vez que se modifican los metadatos en [!DNL Experience Manager], lo que resulta en lo siguiente:

* El recurso en sí se modifica
* Se crea una versión del recurso
* [!UICONTROL Recurso de actualización DAM] se ejecuta con el recurso

Los resultados enumerados consumen recursos considerables. Por lo tanto, Adobe recomienda desactivar XMP reescritura si no es necesaria. Para obtener más información, consulte [XMP reescritura](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/xmp-writeback.html).

La importación de una gran cantidad de metadatos puede resultar en una actividad de escritura de XMP intensiva en recursos si se marca el indicador de flujos de trabajo de ejecución. Planifique una importación de este tipo durante el uso del servidor liviano para que el rendimiento de otros usuarios no se vea afectado.

## Replicación {#replication}

Al replicar recursos en un gran número de instancias de publicación, por ejemplo en una implementación de Sites, Adobe recomienda utilizar la replicación en cadena. En este caso, la instancia de autor se duplica en una sola instancia de publicación que, a su vez, se duplica en las otras instancias de publicación, lo que libera la instancia de autor.

### Configurar la replicación en cadena {#configure-chain-replication}

1. Elija la instancia de publicación que desea utilizar para encadenar las réplicas a
1. En esa instancia de publicación agregue agentes de replicación que apunten a las otras instancias de publicación
1. En cada uno de esos agentes de replicación, habilite &quot;On Receive&quot; en la pestaña &quot;Déclencheur&quot;

>[!NOTE]
>
>Adobe no recomienda la activación automática de recursos. Sin embargo, si es necesario, Adobe recomienda hacer esto como el último paso de un flujo de trabajo, normalmente Recurso de actualización DAM.

## Índices de búsqueda {#search-indexes}

Instalar [los Service Packs más recientes](/help/release-notes/release-notes.md) y revisiones relacionadas con el rendimiento, ya que a menudo incluyen actualizaciones en los índices del sistema. Consulte [consejos de ajuste del rendimiento](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/performance-tuning-guidelines.html?lang=en) para algunas optimizaciones de índice.

Cree índices personalizados para consultas que ejecuta a menudo. Para obtener más información, consulte [metodología para analizar consultas lentas](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) y [creación de índices personalizados](/help/sites-deploying/queries-and-indexing.md). Para obtener más información sobre las prácticas recomendadas de consulta e índice, consulte [Prácticas recomendadas para consultas e indexación](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Configuraciones de índice de Lucene {#lucene-index-configurations}

Se pueden realizar algunas optimizaciones en las configuraciones de índice Oak que pueden ayudar a mejorar [!DNL Experience Manager Assets] rendimiento. Actualice las configuraciones de índice para mejorar el tiempo de reindexación:

1. Abrir CRXDe `/crx/de/index.jsp` e inicie sesión como usuario administrativo.
1. Vaya a `/oak:index/lucene`.
1. Agregue un `String[]` property `excludedPaths` con valores `/var`, `/etc/workflow/instances`y `/etc/replication`.
1. Vaya a `/oak:index/damAssetLucene`. Agregue un `String[]` property `includedPaths` con valor `/content/dam`. Guarde los cambios.

Si los usuarios no necesitan realizar búsquedas de texto completo de recursos, por ejemplo, buscando texto en documentos del PDF, desactívelo. Se mejora el rendimiento del índice al deshabilitar la indexación de texto completo. Para desactivar [!DNL Apache Lucene] extracción de texto, siga estos pasos:

1. En [!DNL Experience Manager] interfaz, acceso [!UICONTROL Administrador de paquetes].
1. Cargue e instale el paquete disponible en [disable_indexingbinarytextextraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip).

### Total de la oferta {#guess-total}

Al crear consultas que generen grandes conjuntos de resultados, utilice el `guessTotal` para evitar una gran utilización de la memoria cuando se ejecutan.

## Problemas conocidos {#known-issues}

### Archivos grandes {#large-files}

Existen dos problemas conocidos principales relacionados con archivos grandes en [!DNL Experience Manager]. Cuando los archivos alcanzan tamaños buenos de más de 2 GB, la sincronización en espera en frío puede encontrarse con una situación de falta de memoria. En algunos casos, evita que se ejecute la sincronización en espera. En otros casos, provoca que la instancia principal se bloquee. Este escenario se aplica a cualquier archivo de [!DNL Experience Manager] que supera los 2 GB, incluidos los paquetes de contenido.

Del mismo modo, cuando los archivos alcanzan el tamaño de 2 GB mientras se utiliza un almacén de datos S3 compartido, puede tardar algún tiempo en que el archivo se mantenga completamente desde la caché al sistema de archivos. Como resultado, cuando se utiliza la replicación sin binarios, es posible que los datos binarios no se hayan mantenido antes de que se complete la replicación. Esta situación puede dar lugar a problemas, especialmente si la disponibilidad de los datos es importante.

## Pruebas de rendimiento {#performance-testing}

Para cada [!DNL Experience Manager] implementación, establezca un régimen de pruebas de rendimiento que pueda identificar y resolver cuellos de botella rápidamente. Aquí hay algunas áreas clave en las que centrarse.

### Pruebas de red {#network-testing}

Para todos los problemas de rendimiento de la red del cliente, realice las siguientes tareas:

* Probar el rendimiento de la red desde la red del cliente
* Pruebe el rendimiento de la red desde la red de Adobe. Para los clientes de AMS, trabaje con su CSE para realizar pruebas desde la red de Adobe.
* Probar el rendimiento de la red desde otro punto de acceso
* Utilizando una herramienta de referencia de red
* Realización de pruebas con Dispatcher

### [!DNL Experience Manager] prueba de implementación {#aem-deployment-testing}

Para minimizar la latencia y lograr un alto rendimiento mediante la utilización eficiente de la CPU y el uso compartido de la carga, supervise el rendimiento de su [!DNL Experience Manager] implementación regularmente. En particular:

* Ejecute pruebas de carga con el [!DNL Experience Manager] implementación.
* Monitorice el rendimiento de carga y la capacidad de respuesta de la interfaz de usuario.

## [!DNL Experience Manager Assets] lista de comprobación de rendimiento e impacto de las tareas de administración de recursos {#checklist}

* Habilite HTTPS para evitar cualquier husmeador de tráfico HTTP corporativo.
* Utilice una conexión por cable para la carga pesada de recursos.
* Implementar en Java 8.
* Establezca parámetros óptimos de JVM.
* Configure un almacén de datos de sistema de archivos o un almacén de datos S3.
* Deshabilite la generación de subrecursos. Si está activado, AEM flujo de trabajo crea un recurso independiente para cada página en un recurso de varias páginas. Cada una de estas páginas es un recurso individual que consume espacio en disco adicional, requiere control de versiones y procesamiento adicional del flujo de trabajo. Si no necesita páginas independientes, deshabilite la generación de subrecursos y las actividades de extracción de páginas.
* Habilitar flujos de trabajo transitorios.
* Ajuste las colas del flujo de trabajo de Granite para limitar los trabajos simultáneos.
* Configurar [!DNL ImageMagick] para limitar el consumo de recursos.
* Elimine los pasos innecesarios del [!UICONTROL Recurso de actualización DAM] flujo de trabajo.
* Configure el flujo de trabajo y la depuración de versiones.
* Optimice los índices con los Service Packs y las revisiones más recientes. Consulte con el Servicio de atención al cliente de Adobe si hay optimizaciones de índice adicionales que puedan estar disponibles.
* Utilice adivinenTotal para optimizar el rendimiento de la consulta.
* Si configura [!DNL Experience Manager] detectar tipos de archivo a partir del contenido de los archivos (habilitando **[!UICONTROL Servicio Day CQ DAM Mime Type]** en el **[!UICONTROL Consola web AEM]**), cargue muchos archivos de forma masiva durante las horas de menor afluencia, ya que consume muchos recursos.
