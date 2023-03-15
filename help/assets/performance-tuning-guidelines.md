---
title: Ajuste del rendimiento [!DNL Assets].
description: Sugerencias y sugerencias acerca de [!DNL Experience Manager] configuración, cambios en el hardware, el software y los componentes de red para eliminar cuellos de botella y optimizar el rendimiento de [!DNL Experience Manager Assets].
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

# [!DNL Adobe Experience Manager Assets] guía de optimización de rendimiento {#assets-performance-tuning-guide}

Un [!DNL Experience Manager Assets] la instalación contiene una serie de componentes de hardware, software y red. Según el escenario de implementación, es posible que necesite realizar cambios de configuración específicos en los componentes de hardware, software y red para eliminar los cuellos de botella de rendimiento.

Además, la identificación y el cumplimiento de determinadas directrices de optimización de hardware y software ayudan a crear una base sólida que permite [!DNL Experience Manager Assets] implementación para cumplir con las expectativas de rendimiento, escalabilidad y fiabilidad.

Rendimiento deficiente en [!DNL Experience Manager Assets] puede afectar a la experiencia del usuario en cuanto a rendimiento interactivo, procesamiento de recursos, velocidad de descarga y otras áreas.

De hecho, la optimización del rendimiento es una tarea fundamental que se realiza antes de establecer métricas de destino para cualquier proyecto.

Estas son algunas áreas de enfoque clave en torno a las cuales se descubren y corrigen problemas de rendimiento antes de que afecten a los usuarios.

## Plataforma {#platform}

Aunque Experience Manager es compatible con una serie de plataformas, Adobe ha encontrado la buena compatibilidad con las herramientas nativas en Linux y Windows, lo que contribuye a un rendimiento óptimo y a una implementación sencilla. Lo ideal es implementar un sistema operativo de 64 bits para satisfacer los altos requisitos de memoria de un [!DNL Experience Manager Assets] implementación. Como con cualquier implementación de Experience Manager, debe implementar TarMK siempre que sea posible. Aunque TarMK no puede escalar más allá de una sola instancia de autor, se encuentra que tiene un mejor rendimiento que MongoMK. Puede añadir instancias de descarga de TarMK para aumentar la potencia de procesamiento del flujo de trabajo de su [!DNL Experience Manager Assets] implementación.

### Carpeta temporal {#temp-folder}

Para mejorar los tiempos de carga de los recursos, utilice un almacenamiento de alto rendimiento para el directorio temporal de Java. En Linux y Windows, se podría utilizar una unidad RAM o SSD. En entornos basados en la nube, se podría utilizar un tipo de almacenamiento de alta velocidad equivalente. Por ejemplo, en Amazon EC2, una [impulso efímero](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) se puede utilizar para la carpeta temporal.

Si el servidor tiene suficiente memoria, configure una unidad de RAM. En Linux, ejecute estos comandos para crear una unidad de 8 GB de RAM:

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

En el sistema operativo Windows, utilice un controlador de terceros para crear una unidad RAM o simplemente utilice un almacenamiento de alto rendimiento como SSD.

Una vez que el volumen temporal de alto rendimiento esté listo, establezca el parámetro JVM `-Djava.io.tmpdir`. Por ejemplo, puede añadir el parámetro JVM siguiente al `CQ_JVM_OPTS` en la variable `bin/start` script de [!DNL Experience Manager]:

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
* `-Doak.fastQuerySize`=true

## Configuración del almacén de datos y la memoria {#data-store-and-memory-configuration}

### Configuración del almacén de datos de archivos {#file-data-store-configuration}

Se recomienda separar el almacén de datos del almacén de segmentos para todos [!DNL Experience Manager Assets] usuarios. Además, la configuración de `maxCachedBinarySize` y `cacheSizeInMB` Los parámetros de pueden ayudar a maximizar el rendimiento. Establecer `maxCachedBinarySize` hasta el tamaño de archivo más pequeño que se pueda guardar en la caché. Especifique el tamaño de la caché en memoria que se utilizará para el almacén de datos en `cacheSizeInMB`. El Adobe recomienda establecer este valor entre el 2 y el 10 por ciento del tamaño total de la pila. Sin embargo, las pruebas de carga y rendimiento pueden ayudar a determinar la configuración ideal.

### Configurar el tamaño máximo de la caché de imágenes almacenadas en búfer {#configure-the-maximum-size-of-the-buffered-image-cache}

Al cargar grandes cantidades de recursos en [!DNL Adobe Experience Manager], para permitir picos inesperados en el consumo de memoria y evitar que JVM falle con OutOfMemoryErrors, reduzca el tamaño máximo configurado de la caché de imágenes almacenadas en búfer. Pongamos un ejemplo de que tiene un sistema con una pila máxima (-) `Xmx`param) de 5 GB, un Oak BlobCache establecido en 1 GB y un cache de documentos establecido en 2 GB. En este caso, la caché almacenada en búfer tardaría un máximo de 1,25 GB y memoria, lo que dejaría solo 0,75 GB de memoria para picos inesperados.

Configure el tamaño de la caché almacenada en búfer en la consola web de OSGi. En `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`, establezca la propiedad `cq.dam.image.cache.max.memory` en bytes. Por ejemplo, 1073741824 es 1 GB (1024 x 1024 x 1024 = 1 GB).

Desde el Experience Manager 6.1 SP1, si utiliza un `sling:osgiConfig` para configurar esta propiedad, asegúrese de establecer el tipo de datos en Long. Para obtener más información, consulte [CQBufferedImageCache consume montón durante las cargas de recursos](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html).

### Almacenes de datos compartidos {#shared-data-stores}

La implementación de un almacén de datos de archivos compartidos o S3 puede ayudar a ahorrar espacio en disco y aumentar el rendimiento de la red en implementaciones a gran escala. Para obtener más información sobre las ventajas y desventajas de utilizar un almacén de datos compartido, consulte [Guía de tamaño de Assets](/help/assets/assets-sizing-guide.md).

### Almacén de datos de S3 {#s-data-store}

La siguiente configuración del almacén de datos de S3 ( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`) ayudó al Adobe a extraer 12,8 TB de objetos binarios grandes (BLOB) de un almacén de datos de archivo existente en un almacén de datos S3 en un sitio de cliente:

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

## Optimización de red {#network-optimization}

Adobe recomienda habilitar HTTPS porque muchas empresas tienen servidores de seguridad que detectan el tráfico HTTP, lo que afecta negativamente a las cargas y corrompe los archivos. Para cargas de archivos grandes, asegúrese de que los usuarios tengan conexiones cableadas a la red, ya que la red WiFi se satura rápidamente. Para obtener instrucciones sobre cómo identificar cuellos de botella de red, consulte [Guía de tamaño de Assets](/help/assets/assets-sizing-guide.md). Para evaluar el rendimiento de la red mediante el análisis de la topología de red, consulte [Consideraciones de red de Assets](/help/assets/assets-network-considerations.md).

Principalmente, la estrategia de optimización de la red depende de la cantidad de ancho de banda disponible y de la carga de su [!DNL Experience Manager] ejemplo. Las opciones de configuración comunes, incluidos los servidores de seguridad o los servidores proxy, pueden ayudar a mejorar el rendimiento de la red. A continuación se indican algunos puntos clave que se deben tener en cuenta:

* Según el tipo de instancia (pequeña, moderada, grande), asegúrese de que dispone de suficiente ancho de banda de red para la instancia de Experience Manager. La asignación adecuada del ancho de banda es especialmente importante si [!DNL Experience Manager] está alojado en AWS.
* Si su [!DNL Experience Manager] está alojada en AWS, puede beneficiarse de tener una política de escalado versátil. Actualice la instancia si los usuarios esperan una carga alta. Reduzca el tamaño para una carga moderada/baja.
* HTTPS: la mayoría de los usuarios tienen servidores de seguridad que detectan el tráfico HTTP, lo que puede afectar negativamente a la carga de archivos o incluso dañar los archivos durante la operación de carga.
* Cargas de archivos grandes: Asegúrese de que los usuarios tengan conexiones cableadas a la red (las conexiones WiFi se saturan rápidamente).

## Flujos de trabajo {#workflows}

### Flujos de trabajo transitorios {#transient-workflows}

Siempre que sea posible, configure el [!UICONTROL Recurso de actualización DAM] flujo de trabajo a Transitorio. La configuración reduce significativamente los costes generales necesarios para procesar flujos de trabajo porque, en este caso, los flujos de trabajo no tienen que pasar por los procesos normales de seguimiento y archivo.

1. Vaya a `/miscadmin` en el [!DNL Experience Manager] implementación en `https://[aem_server]:[port]/miscadmin`.

1. Expandir **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]** > **[!UICONTROL presa]**.

1. Abrir **[!UICONTROL Recurso de actualización DAM]**. En el panel de herramientas flotante, cambie a **[!UICONTROL Página]** y haga clic en **[!UICONTROL Propiedades de página]**.

1. Seleccionar **[!UICONTROL Flujo de trabajo transitorio]** y haga clic en **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Algunas funciones no admiten flujos de trabajo transitorios. Si su [!DNL Assets] la implementación requiere estas funciones, no configure flujos de trabajo transitorios.

En los casos en que no se puedan utilizar flujos de trabajo transitorios, ejecute la depuración de flujos de trabajo regularmente para eliminar los flujos de trabajo archivados [!UICONTROL Recurso de actualización DAM] flujos de trabajo para garantizar que el rendimiento del sistema no se degrada.

Normalmente, ejecuta los flujos de trabajo de depuración de forma semanal. Sin embargo, en situaciones que requieren muchos recursos, como durante la ingesta de recursos a gran escala, puede ejecutarla con mayor frecuencia.

Para configurar la depuración del flujo de trabajo, añada una nueva configuración de depuración del flujo de trabajo de Granite de Adobe a través de la consola OSGi. A continuación, configure y programe el flujo de trabajo como parte de la ventana de mantenimiento semanal.

Si la depuración se ejecuta durante demasiado tiempo, se agota el tiempo de espera. Por lo tanto, debe asegurarse de que los trabajos de depuración se completen para evitar situaciones en las que los flujos de trabajo de depuración no se completen debido al alto número de flujos de trabajo.

Por ejemplo, después de ejecutar numerosos flujos de trabajo no transitorios (lo que crea nodos de instancia de flujo de trabajo), puede ejecutar [AEM Eliminador de flujo de trabajo de ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) de forma ad hoc. Elimina inmediatamente las instancias de flujo de trabajo redundantes y completadas, en lugar de esperar a que se ejecute el programador de depuración del flujo de trabajo de Granite de Adobe.

### Máximo de trabajos paralelos {#maximum-parallel-jobs}

De forma predeterminada, [!DNL Experience Manager] ejecuta un número máximo de trabajos paralelos igual al número de procesadores del servidor. El problema con esta configuración es que durante los períodos de carga pesada, todos los procesadores están ocupados por [!UICONTROL Recurso de actualización DAM] flujos de trabajo, ralentizar la respuesta de la IU y evitar [!DNL Experience Manager] de ejecutar otros procesos que salvaguarden el rendimiento y la estabilidad del servidor. Como práctica recomendada, establezca este valor en la mitad de los procesadores disponibles en el servidor realizando los siguientes pasos:

1. Activado [!DNL Experience Manager] Autor, acceso `https://[aem_server]:[port]/system/console/slingevent`.

1. Clic **[!UICONTROL Editar]** en cada cola de flujo de trabajo relevante para la implementación, por ejemplo **[!UICONTROL Cola de flujo de trabajo transitorio de Granite]**.

1. Actualizar el valor de **[!UICONTROL Máximo de trabajos paralelos]** y haga clic en **[!UICONTROL Guardar]**.

Establecer una cola en la mitad de los procesadores disponibles es una solución viable para empezar. Sin embargo, es posible que tenga que aumentar o disminuir este número para lograr el máximo rendimiento y ajustarlo por entorno. Hay colas independientes para flujos de trabajo transitorios y no transitorios, así como otros procesos, como flujos de trabajo externos. Si varias colas configuradas al 50% de los procesadores están activas simultáneamente, el sistema puede sobrecargarse rápidamente. Las colas muy utilizadas varían en gran medida entre las implementaciones de los usuarios. Por lo tanto, es posible que tenga que configurarlos cuidadosamente para lograr la máxima eficiencia sin sacrificar la estabilidad del servidor.

### Configuración de recursos de actualización DAM {#dam-update-asset-configuration}

El [!UICONTROL Recurso de actualización DAM] El flujo de trabajo de contiene un conjunto completo de pasos configurados para tareas como, por ejemplo, la generación de PTIFF de Dynamic Media y [!DNL Adobe InDesign Server] integración. Sin embargo, es posible que la mayoría de los usuarios no requieran varios de estos pasos. El Adobe recomienda crear una copia personalizada del [!UICONTROL Recurso de actualización DAM] modelo de flujo de trabajo y elimine los pasos innecesarios. En este caso, actualice los iniciadores para [!UICONTROL Recurso de actualización DAM] para apuntar al nuevo modelo.

Ejecución de la [!UICONTROL Recurso de actualización DAM] Un flujo de trabajo intensivo puede aumentar considerablemente el tamaño del almacén de datos de archivos. Los resultados de un experimento realizado por Adobe han mostrado que el tamaño del almacén de datos puede aumentar en aproximadamente 400 GB si se realizan alrededor de 5500 flujos de trabajo en un plazo de 8 horas.

Se trata de un aumento temporal y el almacén de datos vuelve a su tamaño original después de ejecutar la tarea de recolección de elementos no utilizados del almacén de datos.

Normalmente, la tarea de recolección de elementos no utilizados del almacén de datos se ejecuta semanalmente junto con otras tareas de mantenimiento programadas.

Si tiene un espacio en disco limitado y ejecuta [!UICONTROL Recurso de actualización DAM] flujos de trabajo de forma intensiva, considere la posibilidad de programar la tarea de recolección de elementos no utilizados con mayor frecuencia.

#### Generación de representación en tiempo de ejecución {#runtime-rendition-generation}

Los clientes utilizan imágenes de diversos tamaños y formatos en su sitio web o para su distribución a socios comerciales. Dado que cada representación aumenta el espacio del recurso en el repositorio, Adobe recomienda utilizar esta función con prudencia. Para reducir la cantidad de recursos necesarios para procesar y almacenar imágenes, puede generar estas imágenes en tiempo de ejecución en lugar de como representaciones durante la ingesta.

Muchos clientes de Sites implementan un servlet de imagen que cambia de tamaño y recorta las imágenes en el momento en que se solicitan, lo que impone una carga adicional a la instancia de publicación. Sin embargo, mientras estas imágenes se puedan almacenar en caché, el desafío se puede mitigar.

Un enfoque alternativo es utilizar la tecnología de Dynamic Media para manipular las imágenes por completo. Además, puede implementar Brand Portal que no solo se haga cargo de las responsabilidades de generación de representaciones desde [!DNL Experience Manager] , pero también todo el nivel de publicación.

#### ImageMagick {#imagemagick}

Si personaliza la variable [!UICONTROL Recurso de actualización DAM] flujo de trabajo para generar representaciones mediante ImageMagick, Adobe recomienda modificar `policy.xml` archivo en `/etc/ImageMagick/`. De forma predeterminada, ImageMagick utiliza todo el espacio disponible en disco en el volumen del sistema operativo y la memoria disponible. Realice los siguientes cambios de configuración en la `policymap` sección de `policy.xml` para limitar estos recursos.

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

Además, establezca la ruta de la carpeta temporal de ImageMagick en `configure.xml` (o configurando la variable de entorno) `MAGICK_TEMPORARY_PATH`) a una partición de disco que tenga suficiente espacio e IOPS.

>[!CAUTION]
>
>Una configuración incorrecta puede hacer que el servidor sea inestable si ImageMagick utiliza todo el espacio en disco disponible. Los cambios de directiva necesarios para procesar archivos grandes mediante ImageMagick pueden afectar al [!DNL Experience Manager] rendimiento. Para obtener más información, consulte [instalar y configurar ImageMagick](/help/assets/best-practices-for-imagemagick.md).

>[!NOTE]
>
>ImageMagick `policy.xml` y `configure.xml` Los archivos de están disponibles en `/usr/lib64/ImageMagick-&#42;/config/` en lugar de `/etc/ImageMagick/`.Consulte [Documentación de ImageMagick](https://www.imagemagick.org/script/resources.php) para la ubicación de los archivos de configuración.

Si está utilizando [!DNL Experience Manager] en Adobe Managed Services (AMS), póngase en contacto con Asistencia al cliente de Adobe si tiene pensado procesar muchos archivos PSD o PSB de gran tamaño. Póngase en contacto con el departamento de Asistencia al cliente de Adobe para implementar estas prácticas recomendadas en su implementación de AMS y para elegir las mejores herramientas y modelos posibles para los formatos propietarios de Adobe. [!DNL Experience Manager] puede que no procese archivos PSB de muy alta resolución que tengan más de 30000 x 23000 píxeles.

### XMP respuesta de escritura de la {#xmp-writeback}

XMP La reescritura de datos actualiza el recurso original cada vez que se modifican los metadatos en [!DNL Experience Manager], lo que da como resultado lo siguiente:

* Se modifica el recurso en sí
* Se crea una versión del recurso
* [!UICONTROL Recurso de actualización DAM] se ejecuta con el recurso

Los resultados enumerados consumen recursos considerables. Por lo tanto, el Adobe XMP recomienda desactivar la reescritura de la escritura de la si no es necesaria. Para obtener más información, consulte [XMP respuesta de escritura de la](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/xmp-writeback.html).

XMP La importación de una gran cantidad de metadatos puede dar como resultado una actividad de reescritura de recursos intensivos en recursos si se marca el indicador de ejecución de flujos de trabajo. Planifique una importación de este tipo durante el uso del servidor lean para que el rendimiento de otros usuarios no se vea afectado.

## Replicación {#replication}

Al replicar recursos en un gran número de instancias de publicación, por ejemplo en una implementación de Sites, Adobe recomienda utilizar la replicación en cadena. En este caso, la instancia de autor se replica en una sola instancia de publicación, que a su vez se replica en las demás instancias de publicación, liberando la instancia de autor.

### Configurar replicación de cadena {#configure-chain-replication}

1. Elija la instancia de publicación que desea utilizar para encadenar las replicaciones
1. En esa instancia de publicación, agregue agentes de replicación que apunten a las demás instancias de publicación
1. En cada uno de estos agentes de replicación, habilite &quot;Recepción&quot; en la pestaña &quot;Déclencheur&quot;

>[!NOTE]
>
>El Adobe no recomienda la activación automática de recursos. Sin embargo, si es necesario, Adobe recomienda hacerlo como el paso final de un flujo de trabajo, normalmente Recurso de actualización DAM.

## Buscar índices {#search-indexes}

Instalar [los paquetes de servicio más recientes](/help/release-notes/release-notes.md) y revisiones relacionadas con el rendimiento, ya que suelen incluir actualizaciones de los índices del sistema. Consulte [consejos para optimizar el rendimiento](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/performance-tuning-guidelines.html?lang=en) para algunas optimizaciones de índice.

Cree índices personalizados para consultas que ejecute con frecuencia. Para obtener más información, consulte [metodología para analizar consultas lentas](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) y [crear índices personalizados](/help/sites-deploying/queries-and-indexing.md). Para obtener información adicional sobre las prácticas recomendadas de consultas e índices, consulte [Prácticas recomendadas para consultas e indexación](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Configuraciones de índice de Lucene {#lucene-index-configurations}

Se pueden realizar algunas optimizaciones en las configuraciones del índice de Oak que pueden ayudar a mejorar [!DNL Experience Manager Assets] rendimiento. Actualice las configuraciones de índice para mejorar el tiempo de reindexación:

1. Abrir CRXDe `/crx/de/index.jsp` e inicie sesión como usuario administrativo.
1. Navegar a `/oak:index/lucene`.
1. Añadir un `String[]` propiedad `excludedPaths` con valores `/var`, `/etc/workflow/instances`, y `/etc/replication`.
1. Navegar a `/oak:index/damAssetLucene`. Añadir un `String[]` propiedad `includedPaths` con valor `/content/dam`. Guardar cambios.

Si los usuarios no necesitan realizar búsquedas de texto completo de recursos, por ejemplo, buscando texto en documentos del PDF, deshabilite la búsqueda. Se mejora el rendimiento del índice al deshabilitar la indexación de texto completo. Para deshabilitar [!DNL Apache Lucene] extracción de texto, siga estos pasos:

1. Entrada [!DNL Experience Manager] interfaz, acceso [!UICONTROL Administrador de paquetes].
1. Cargue e instale el paquete disponible en [disable_indexingbinarytextextraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip).

### Total de estimación {#guess-total}

Cuando cree consultas que generen grandes conjuntos de resultados, utilice el `guessTotal` para evitar un uso intensivo de la memoria al ejecutarlos.

## Problemas conocidos {#known-issues}

### Archivos grandes {#large-files}

Hay dos problemas conocidos importantes relacionados con los archivos grandes en [!DNL Experience Manager]. Cuando los archivos alcanzan tamaños de bueno de 2 GB, la sincronización en espera en frío puede quedarse sin memoria. En algunos casos, evita que se ejecute la sincronización en espera. En otros casos, hace que la instancia principal se bloquee. Este escenario se aplica a cualquier archivo de [!DNL Experience Manager] superior a 2 GB, incluidos los paquetes de contenido.

Del mismo modo, cuando los archivos alcanzan los 2 GB de tamaño mientras se utiliza un almacén de datos S3 compartido, puede tardar algún tiempo en persistir completamente desde la caché al sistema de archivos. Como resultado, cuando se utiliza la replicación sin binarios, es posible que los datos binarios no se hayan mantenido antes de que finalice la replicación. Esta situación puede dar lugar a problemas, especialmente si la disponibilidad de datos es importante.

## Pruebas de rendimiento {#performance-testing}

Para cada [!DNL Experience Manager] , establezca un régimen de pruebas de rendimiento que pueda identificar y resolver los cuellos de botella rápidamente. Estas son algunas áreas clave en las que centrarse.

### Pruebas de red {#network-testing}

Para todos los problemas de rendimiento de red del cliente, realice las siguientes tareas:

* Pruebe el rendimiento de la red desde la red del cliente
* Pruebe el rendimiento de la red desde la red de Adobe. Para los clientes de AMS, trabaje con su CSE para realizar pruebas desde la red de Adobe.
* Prueba del rendimiento de la red desde otro punto de acceso
* Mediante el uso de una herramienta de referencia de red
* Comprobación con el despachante

### [!DNL Experience Manager] pruebas de implementación {#aem-deployment-testing}

Para minimizar la latencia y lograr un alto rendimiento a través de un uso eficiente de la CPU y el uso compartido de la carga, monitorice el rendimiento de su [!DNL Experience Manager] implementación con regularidad. En particular:

* Ejecute pruebas de carga con el [!DNL Experience Manager] implementación.
* Monitorice el rendimiento de carga y la capacidad de respuesta de IU.

## [!DNL Experience Manager Assets] lista de comprobación de rendimiento e impacto de las tareas de administración de recursos {#checklist}

* Habilite HTTPS para evitar cualquier detector de tráfico HTTP corporativo.
* Utilice una conexión con cable para cargar recursos pesados.
* Implementación en Java 8.
* Establezca los parámetros óptimos de JVM.
* Configurar un almacén de datos del sistema de archivos o un almacén de datos de S3.
* Deshabilite la generación de subrecursos. AEM Si está activada, el flujo de trabajo de la crea un recurso independiente para cada página en un recurso de varias páginas. Cada una de estas páginas es un recurso individual que consume espacio en disco adicional, requiere versiones y un procesamiento de flujo de trabajo adicional. Si no necesita páginas separadas, deshabilite la generación de subrecursos y las actividades de extracción de páginas.
* Habilitar flujos de trabajo transitorios.
* Ajuste las colas del flujo de trabajo de Granite para limitar los trabajos simultáneos.
* Configurar [!DNL ImageMagick] para limitar el consumo de recursos.
* Elimine los pasos innecesarios del [!UICONTROL Recurso de actualización DAM] flujo de trabajo.
* Configure el flujo de trabajo y la depuración de versiones.
* Optimice los índices con los últimos Service Packs y revisiones. Consulte con Asistencia al cliente de Adobe las optimizaciones de índice adicionales que puedan estar disponibles.
* Utilice guessTotal para optimizar el rendimiento de la consulta.
* Si configura [!DNL Experience Manager] para detectar tipos de archivo a partir del contenido de los archivos (habilitando **[!UICONTROL Servicio Day CQ DAM Mime Type]** en el **[!UICONTROL AEM Consola web de]**), cargue muchos archivos de forma masiva durante las horas de menor afluencia, ya que consume muchos recursos.
