---
title: AEM con MongoDB
seo-title: AEM con MongoDB
description: Obtenga información sobre las tareas y consideraciones necesarias para una implementación correcta de AEM con MongoDB.
seo-description: Obtenga información sobre las tareas y consideraciones necesarias para una implementación correcta de AEM con MongoDB.
uuid: 8028832d-10de-4811-a769-fab699c162ec
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cd3b979f-53d4-4274-b4eb-a9533329192a
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# AEM con MongoDB{#aem-with-mongodb}

Este artículo tiene como objetivo mejorar los conocimientos sobre las tareas y consideraciones necesarias para implementar correctamente Adobe Experience Manager con MongoDB.

Para obtener más información relacionada con la implementación, consulte la sección [Implementación y mantenimiento](/help/sites-deploying/deploy.md) de la documentación.

## Cuándo utilizar MongoDB con AEM {#when-to-use-mongodb-with-aem}

MongoDB se utilizará normalmente para admitir implementaciones de autor de AEM cuando se cumpla uno de los siguientes criterios:

* Más de 1000 usuarios únicos al día;
* Más de 100 usuarios simultáneos;
* Grandes volúmenes de ediciones de página;
* Implementaciones o activaciones grandes.

Los criterios anteriores son solo para las instancias de autor y no para ninguna instancia de publicación que debería estar basada en TarMK. El número de usuarios hace referencia a usuarios autenticados, ya que las instancias de autor no permiten el acceso no autenticado.

Si no se cumplen los criterios, se recomienda una implementación TarMK activa/en espera para abordar la disponibilidad. Generalmente, MongoDB debe considerarse en situaciones en las que los requisitos de escalado son más que los que se pueden lograr con un solo elemento de hardware.

>[!NOTE]
>
>Encontrará información adicional sobre el tamaño de las instancias de autor y la definición de usuarios simultáneos en las Directrices sobre el tamaño de [hardware](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel).

### Implementación mínima de MongoDB para AEM {#minimal-mongodb-deployment-for-aem}

A continuación se muestra una implementación mínima de AEM en MongoDB. Para simplificar, se han generalizado los componentes SSL y HTTP Proxy. Consiste en un único conjunto de réplicas MongoBD, con un primario y dos secundarios.

![climage_1-4](assets/chlimage_1-4.png)

Una implementación mínima requiere 3 `mongod` instancias configuradas como conjunto de réplicas. Una instancia será elegida principal y las otras instancias serán secundarias, y la elección será administrada por `mongod`. Se adjunta a cada instancia un disco local. Para que el clúster admita la carga, se recomienda una ganancia mínima de 12 MB/s con más de 3000 operaciones de E/S por segundo (IOPS).

Los autores de AEM están conectados a las `mongod` instancias y cada uno de ellos se conecta a las tres `mongod` instancias. Las escrituras se envían al directorio principal y las lecturas se pueden leer en cualquiera de los casos. El tráfico se distribuye en función de la carga de un distribuidor a cualquiera de las instancias activas de creación de AEM. El almacén de datos OAK es un `FileDataStore`y el Administrador de operaciones de MongoDB proporciona supervisión de MongoDB o MMS según la ubicación de la implementación. Las soluciones de terceros como Splunk o Ganglia proporcionan supervisión de registro y nivel del sistema operativo.

En esta implementación, todos los componentes son necesarios para una implementación correcta. Cualquier componente que falte dejará la implementación infuncional.

### Sistemas operativos {#operating-systems}

Para obtener una lista de los sistemas operativos compatibles con AEM 6, consulte la página [Requisitos](/help/sites-deploying/technical-requirements.md)técnicos.

### Entornos {#environments}

Se admiten entornos virtualizados siempre que haya una buena comunicación entre los diferentes equipos técnicos que ejecutan el proyecto. Esto incluye al equipo que ejecuta AEM, el equipo que posee el sistema operativo y el equipo que administra la infraestructura virtualizada.

Existen requisitos específicos que cubren la capacidad de E/S de las instancias de MongoDB que deben ser administradas por el equipo que administra el entorno virtualizado. Si el proyecto utiliza una implementación en la nube, como Amazon Web Services, las instancias deberán aprovisionarse con suficiente capacidad de E/S y coherencia para admitir las instancias de MongoDB. De lo contrario, los procesos de MongoDB y el repositorio de Oak funcionarán de manera insegura y errática.

En los entornos virtualizados, MongoDB requerirá configuraciones específicas de E/S y VM para garantizar que el motor de almacenamiento de MongoDB no se vea paralizado por las políticas de asignación de recursos de VMWare. Una implementación exitosa garantizará que no haya barreras entre los distintos equipos y que todos estén registrados para ofrecer el rendimiento requerido.

## Consideraciones de hardware {#hardware-considerations}

### Almacenamiento {#storage}

Para lograr el rendimiento de lectura y escritura para un mejor rendimiento sin necesidad de escalado horizontal prematuro, MongoDB generalmente requiere almacenamiento SSD o almacenamiento con un rendimiento equivalente a SSD.

### RAM {#ram}

Las versiones 2.6 y 3.0 de MongoDB que utilizan el motor de almacenamiento MAP requieren que el conjunto de trabajo de la base de datos y sus índices encaje en RAM.

La insuficiencia de RAM provocará una reducción significativa del rendimiento. El tamaño del conjunto de trabajo y de la base de datos depende en gran medida de la aplicación. Aunque se pueden hacer algunas estimaciones, la forma más fiable de determinar la cantidad de RAM necesaria es crear la aplicación AEM y probarla de carga.

Para ayudar con el proceso de prueba de carga, se puede asumir la siguiente relación entre el conjunto de trabajo y el tamaño total de la base de datos:

* 1:10 para almacenamiento SSD
* 1:3 para almacenamiento en disco duro

Esto significa que en el caso de implementaciones de SSD, se necesitarán 200 GB de RAM para una base de datos de 2 TB.

Aunque las mismas limitaciones se aplican al motor de almacenamiento WiredTiger en MongoDB 3.0, la correlación entre el conjunto de trabajo, la RAM y los errores de página no es tan fuerte como WiredTiger no utiliza la asignación de memoria de la misma manera que lo hace el motor de almacenamiento MAP.

>[!NOTE]
>
>Adobe recomienda utilizar el motor de almacenamiento WiredTiger para implementaciones de AEM 6.1 que utilizan MongoDB 3.0.

### Data Store {#data-store}

Debido a las limitaciones del conjunto de trabajo de MongoDB, se recomienda encarecidamente que el almacén de datos se mantenga independiente del MongoDB. En la mayoría de los entornos, se debe utilizar un NAS `FileDataStore` disponible para todas las instancias de AEM. Para situaciones en las que se utilizan los servicios web de Amazon, también hay un `S3 DataStore`. Si por algún motivo el almacén de datos se mantiene dentro de MongoDB, el tamaño del almacén de datos debe agregarse al tamaño total de la base de datos y los cálculos del conjunto de trabajo deben ajustarse adecuadamente. Esto puede significar aprovisionar una cantidad significativamente mayor de RAM para mantener el rendimiento sin errores de página.

## Monitoreo {#monitoring}

La supervisión es fundamental para que el proyecto se ejecute con éxito. Aunque con suficiente conocimiento es posible ejecutar AEM en MongoDB sin supervisión, ese conocimiento se encuentra normalmente en ingenieros especializados para cada sección de la implementación.

Esto suele implicar a un ingeniero de I+D que trabaja en el Apache Oak Core y a un especialista en MongoDB.

Sin supervisión a todos los niveles, se requerirá un conocimiento detallado de la base de códigos para diagnosticar problemas. Con la supervisión y la orientación adecuada sobre las principales estadísticas, los equipos de ejecución podrán reaccionar adecuadamente ante las anomalías.

Aunque es posible utilizar herramientas de línea de comandos para obtener una instantánea rápida del funcionamiento de un clúster, hacerlo en tiempo real sobre muchos hosts es casi imposible. Las herramientas de la línea de comandos rara vez proporcionan información histórica más allá de unos minutos y nunca permiten la correlación cruzada entre diferentes tipos de métricas. Un breve período de `mongod` sincronización en segundo plano lenta requiere un esfuerzo manual considerable para correlacionarse con un tiempo de espera de E/S o con niveles de escritura excesivos con un recurso de almacenamiento compartido desde una máquina virtual aparentemente desconectada.

### MongoDB Cloud Manager {#mongodb-cloud-manager}

MongoDB Cloud Manager es un servicio gratuito ofrecido por MongoDB que permite el control y la gestión de las instancias de MongoDB. Proporciona una visión del rendimiento y el estado del clúster de MongoDB en tiempo real. Gestiona las instancias alojadas en la nube y en privado, siempre que la instancia pueda llegar al servidor de supervisión del Administrador de nube.

Requiere un agente instalado en la instancia de MongoDB que se conecte al servidor de supervisión. Hay 3 niveles del agente:

* Un agente de automatización que puede automatizar completamente todo lo que se encuentra en el servidor MongoDB,
* Un agente de supervisión que puede supervisar la `mongod` instancia,
* Agente de copia de seguridad que puede realizar copias de seguridad programadas de los datos.

Aunque el uso del Administrador de nube para la automatización de mantenimiento de un clúster de MongoDB facilita muchas de las tareas rutinarias, no es necesario y tampoco lo está usando para la copia de seguridad. Sin embargo, al elegir Cloud Manager para supervisar, es necesario realizar un seguimiento.

Para obtener más información acerca de MongoDB Cloud Manager, consulte la documentación [de](https://docs.cloud.mongodb.com/)MongoDB.

### Administrador de operaciones de MongoDB {#mongodb-ops-manager}

MongoDB Ops Manager es el mismo software que MongoDB Cloud Manager. Una vez registrado, Ops Manager puede descargarse e instalarse localmente en un centro de datos privado o en cualquier otro equipo portátil o de escritorio. Utiliza una base de datos local de MongoDB para almacenar datos y comunicarse exactamente del mismo modo que Cloud Manager con los servidores gestionados. Si tiene directivas de seguridad que prohíben un agente de supervisión, debe utilizar el Administrador de operaciones de MongoDB.

### Supervisión del sistema operativo {#operating-system-monitoring}

Se requiere supervisión a nivel del sistema operativo para ejecutar un clúster MongoDB de AEM.

Ganglia es un buen ejemplo de un sistema de este tipo y ofrece una imagen del rango y detalle de la información requerida que va más allá de las métricas básicas de salud como CPU, promedio de carga y espacio libre en disco. Para diagnosticar problemas, se requiere información de nivel inferior, como niveles de agrupación de entropía, espera de E/S de CPU, sockets en estado FIN_WAIT2.

### Agregación de registros {#log-aggregation}

Con un clúster de varios servidores, la agregación de registros centrales es un requisito para un sistema de producción. Software como Splunk soporta la agregación de registros y permite a los equipos analizar los patrones de comportamiento de la aplicación sin tener que recopilar manualmente los registros.

## Listas de comprobación {#checklists}

Esta sección trata de los distintos pasos que debe seguir para asegurarse de que las implementaciones de AEM y MongoDB están correctamente configuradas antes de implementar el proyecto.

### Red {#network}

1. Primero, asegúrese de que todos los hosts tengan una entrada DNS
1. Todos los hosts deben resolverse mediante su entrada DNS de todos los demás hosts enrutables
1. Todos los hosts MongoDB se pueden enrutar desde todos los demás hosts MongoDB del mismo clúster
1. Los hosts MongoDB pueden enrutar paquetes al Administrador de nube MongoDB y a los demás servidores de supervisión
1. Los servidores AEM pueden enrutar paquetes a todos los servidores MongoDB
1. La latencia de paquetes entre cualquier servidor AEM y cualquier servidor MongoDB es inferior a dos milisegundos, sin pérdida de paquetes y con una distribución estándar de un milisegundo o menos.
1. Asegúrese de que no haya más de dos saltos entre un servidor AEM y un servidor MongoDB
1. No hay más de dos saltos entre dos servidores MongoDB
1. No hay enrutadores superiores a OSI Nivel 3 entre servidores principales (MongoDB, AEM o cualquier combinación).
1. Si se utiliza el trunking VLAN o cualquier forma de tunelización de red, debe cumplir con las comprobaciones de latencia de paquetes.

### Configuración de AEM {#aem-configuration}

#### Configuración del almacén de nodos {#node-store-configuration}

Las instancias de AEM deben configurarse para utilizar AEM con MongoMK. La base de la implementación de MongoMK en AEM es Document Node Store.

Para obtener más información sobre cómo configurar los almacenes de nodos, consulte [Configuración de los almacenes de nodos y los almacenes de datos en AEM](/help/sites-deploying/data-store-config.md).

A continuación se muestra un ejemplo de la configuración de Document Node Store para una implementación mínima de MongoDB:

```xml
# org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config
#MongoDB server details
mongodburi=mongodb://aem:aempassword@mongodbserver1.customer.com:27000,mongodbserver2.customer.com:27000

#Name of MongoDB database to use
db=aem

#Store binaries in custom BlobStore e.g. FileDataStore
customBlobStore=true

cache=2048
blobCacheSize=1024
```

Donde:

* `mongodburi`
Este es el servidor MongoDB al que AEM debe conectarse. Las conexiones se realizan a todos los miembros conocidos del conjunto de réplicas predeterminado. Si se utiliza MongoDB Cloud Manager, se habilita la seguridad del servidor. En consecuencia, la cadena de conexión debe contener un nombre de usuario y una contraseña adecuados. Las versiones no empresariales de MongoDB solo admiten autenticación de nombre de usuario y contraseña. Para obtener más información sobre la sintaxis de la cadena de conexión, consulte la [documentación](https://docs.mongodb.org/manual/reference/connection-string/).

* `db`
Nombre de la base de datos. El valor predeterminado para AEM es `aem-author`.

* `customBlobStore`
Si la implementación almacena binarios en la base de datos, formarán parte del conjunto de trabajo. Por esta razón, se recomienda no almacenar binarios dentro de MongoDB, prefiriendo un almacén de datos alternativo como un almacén de datos `FileSystem` en un NAS.

* `cache`
Tamaño de caché en megabytes. Esto se distribuye entre varios cachés utilizados en la `DocumentNodeStore`. El valor predeterminado es 256 MB. Sin embargo, el rendimiento de lectura de Oak se beneficiará de una caché más grande.

* `blobCacheSize`
AEM puede almacenar en caché los blobs utilizados con frecuencia para evitar que se vuelvan a extraer del almacén de datos. Esto tendrá un mayor impacto en el rendimiento, especialmente al almacenar blobs en la base de datos de MongoDB. Todos los Almacenes de datos basados en el sistema de archivos se beneficiarán de la caché de disco a nivel del sistema operativo.

#### Configuración del almacén de datos {#data-store-configuration}

El almacén de datos se utiliza para almacenar archivos de un tamaño mayor que un umbral. Por debajo de ese umbral, los archivos se almacenan como propiedades en el almacén de nodos de documentos. Si `MongoBlobStore` se utiliza, se crea una colección dedicada en MongoDB para almacenar los blobs. Esta colección contribuye al conjunto de trabajo de la `mongod` instancia y requiere que `mongod` tenga más RAM para evitar problemas de rendimiento. Por este motivo, la configuración recomendada es evitar el uso `MongoBlobStore` de implementaciones de producción y el `FileDataStore` respaldo de un NAS compartido entre todas las instancias de AEM. Dado que la caché de nivel del sistema operativo es eficiente en la administración de archivos, el tamaño mínimo de un archivo en disco debe establecerse cerca del tamaño de bloque del disco para que el sistema de archivos se utilice de manera eficiente y muchos documentos pequeños no contribuyan excesivamente al conjunto de trabajo de la `mongod` instancia.

Esta es una configuración típica del almacén de datos para una implementación mínima de AEM con MongoDB:

```xml
# org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config
# The minimum size of an object that should be stored in this data store.
minRecordLength=4096
path=/datastore
maxCachedBinarySize=4096
cacheSizeInMB=128
```

Donde:

* `minRecordLength`
Tamaño en bytes. Los binarios de menos o igual a este tamaño se almacenan con el almacén de nodos de documentos. En lugar de almacenar el ID del blob, se almacena el contenido del binario. Para binarios mayores que este tamaño, el ID del binario se almacena como propiedad del documento en la colección de nodos y el cuerpo del binario se almacena en el `FileDataStore` disco. 4096 bytes es un tamaño de bloque típico del sistema de archivos.

* `path`
Ruta a la raíz del almacén de datos. Para una implementación de MongoMK, debe ser un sistema de archivos compartido disponible para todas las instancias de AEM. Generalmente se utiliza un servidor NAS (Network Attached Storage). Para implementaciones en la nube como Amazon Web Services, también `S3DataFileStore` está disponible.

* `cacheSizeInMB`
El tamaño total de la memoria caché binaria en megabytes. Se utiliza para almacenar en caché los binarios menos que la `maxCacheBinarySize` configuración.

* `maxCachedBinarySize`
Tamaño máximo en bytes de un binario almacenado en caché en la memoria caché binaria. Si se utiliza un almacén de datos basado en el sistema de archivos, no se recomienda utilizar valores altos para la caché del almacén de datos, ya que el sistema operativo ya almacena en caché los binarios.

#### Desactivación de la sugerencia de consulta {#disabling-the-query-hint}

Se recomienda desactivar la sugerencia de consulta enviada con todas las consultas agregando la propiedad

`-Doak.mongo.disableIndexHint=true`

al iniciar AEM. De esta manera, MongoDB calculará en el índice más apropiado para usar en base a las estadísticas internas.

Si la sugerencia de consulta no está deshabilitada, cualquier ajuste del rendimiento de los índices no afectará al rendimiento de AEM.

#### Habilitar caché persistente para MongoMK {#enable-persistent-cache-for-mongomk}

Se recomienda habilitar una configuración de caché persistente para implementaciones de MongoDB, a fin de maximizar la velocidad para entornos con alto rendimiento de lectura de E/S. Para obtener más información, consulte la documentación [de](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html)Jackrabbit Oak.

## Optimizaciones del sistema operativo MongoDB {#mongodb-operating-system-optimizations}

### Compatibilidad con sistemas operativos {#operating-system-support}

MongoDB 2.6 utiliza un motor de almacenamiento de memoria asignada que es sensible a algunos aspectos de la administración de nivel del sistema operativo entre RAM y disco. El rendimiento de consulta y lectura de la instancia de MongoDB depende de evitar o eliminar las operaciones de E/S lentas a menudo denominadas errores de página. Son errores de página que se aplican al `mongod` proceso en particular. No deben confundirse con los errores de página a nivel del sistema operativo.

Para un funcionamiento rápido, la base de datos MongoDB sólo debe acceder a los datos que ya están en RAM. Los datos a los que necesita acceder están formados por índices y datos. Esta colección de índices y datos se denomina conjunto de trabajo. Cuando el conjunto de trabajo es mayor que la RAM disponible, MongoDB tiene que introducir esos datos desde el disco con un costo de E/S, desalojando otros datos que ya están en la memoria. Si el desalojo hace que los datos se vuelvan a cargar desde los errores de la página del disco, predominará y el rendimiento se degradará. Cuando el conjunto de trabajo es dinámico y variable, se producirán más errores de página para admitir operaciones.

MongoDB se ejecuta en una serie de sistemas operativos que incluyen una amplia variedad de sabores Linux, Windows y Mac OS. Consulte [https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms) para obtener más información. Según la elección del sistema operativo, MongoDB tiene diferentes recomendaciones de nivel de sistema operativo. Hay documentos en [https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration) y resumidos aquí para mayor comodidad.

#### Linux {#linux}

* Desactive las páginas de desplazamiento transparentes y desactívelo. Consulte Configuración [de páginas grandes](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/) transparentes para obtener más información.
* [Ajuste la configuración](https://docs.mongodb.com/manual/administration/production-notes/#readahead) de lectura anticipada en los dispositivos que almacenan los archivos de base de datos para adaptarlos a su caso de uso.

   * Para el motor de almacenamiento MAPv1, si el conjunto de trabajo es más grande que la RAM disponible y el patrón de acceso al documento es aleatorio, considere reducir el avance a 32 o 16. Evalúe diferentes configuraciones para encontrar un valor óptimo que maximice la memoria residente y reduzca el número de errores de página.
   * Para el motor de almacenamiento WiredTiger, establezca readforward en 0 independientemente del tipo de medio de almacenamiento (giro, SSD, etc.). En general, utilice la configuración de lectura anticipada recomendada a menos que la prueba muestre un beneficio medible, repetible y confiable en un valor de lectura anticipada más alto. [La asistencia](https://docs.mongodb.com/manual/administration/production-notes/#readahead) profesional de MongoDB puede proporcionar asesoramiento y orientación sobre configuraciones de lectura anticipadas distintas de cero.

* Desactive la herramienta sintonizada si está ejecutando RHEL 7 / CentOS 7 en un entorno virtual.
* Cuando RHEL 7 / CentOS 7 se ejecutan en un entorno virtual, la herramienta sintonizada invoca automáticamente un perfil de rendimiento derivado del rendimiento, que establece automáticamente la configuración de readforward en 4 MB. Esto puede afectar negativamente al rendimiento.
* Utilice los programadores de discos noop o de fecha límite para las unidades SSD.
* Utilice el programador de discos noop para unidades virtualizadas en VM invitadas.
* Deshabilite NUMA o establezca vm.zone_reclaim_mode en 0 y ejecute instancias [mongood](https://docs.mongodb.com/manual/administration/production-notes/#readahead) con entrelazado de nodos. Consulte: Hardware [MongoDB y NUMA](https://docs.mongodb.com/manual/administration/production-notes/#readahead) para obtener más información.

* Ajuste los valores límite del hardware para adaptarlos a su caso de uso. Si se ejecutan varias instancias de [mondios](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) o [mongos](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) bajo el mismo usuario, escale los valores de ulimit en consecuencia. Consulte: Configuración de límite [UNIX para obtener más información](https://docs.mongodb.com/manual/reference/ulimit/) .

* Utilice noatime para el punto de montaje de [dbPath](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath) .
* Configure suficientes controladores de archivo (fs.file-max), límite de pid del núcleo (kernel.pid_max) y máximo de subprocesos por proceso (kernel.thread-max) para su implementación. Para sistemas grandes, los valores siguientes proporcionan un buen punto de partida:

   * fs.file-max valor de 98000,
   * valor kernel.pid_max de 64000,
   * valor andkernel.thread-max de 64000

* Asegúrese de que el sistema tenga configurado el espacio de intercambio. Consulte la documentación del sistema operativo para obtener detalles sobre el tamaño adecuado.
* Asegúrese de que el mantenimiento TCP predeterminado del sistema está configurado correctamente. Un valor de 300 suele proporcionar un mejor rendimiento para conjuntos de réplicas y clústeres compartidos. Consulte: ¿ [Afecta el tiempo de mantenimiento de TCP a las implementaciones de MongoDB?](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) en las Preguntas más frecuentes para obtener más información.

#### Windows {#windows}

* Considere desactivar las actualizaciones de &quot;hora de último acceso&quot; NTFS. Esto es análogo a desactivar el tiempo en sistemas similares a Unix.

### WiredTiger {#wiredtiger}

A partir de MongoDB 3.2 el motor de almacenamiento predeterminado para MongoDB es el motor de almacenamiento WiredTiger. Este motor proporciona una serie de funciones robustas y escalables que lo hacen mucho mejor para cargas de trabajo generales de bases de datos. Las siguientes secciones describen estas funciones.

#### Conversión de nivel de documento {#document-level-concurrency}

WiredTiger utiliza el control de concurrencia a nivel de documento para operaciones de escritura. Como resultado, varios clientes pueden modificar diferentes documentos de una colección al mismo tiempo.

Para la mayoría de las operaciones de lectura y escritura, WiredTiger utiliza un control de concurrencia optimista. WiredTiger utiliza únicamente bloqueos por intención en los niveles global, de base de datos y de recopilación. Cuando el motor de almacenamiento detecta conflictos entre dos operaciones, se produce un conflicto de escritura que hace que MongoDB vuelva a intentar esa operación de forma transparente.Algunas operaciones globales, generalmente operaciones de corta duración que involucran múltiples bases de datos, aún requieren un bloqueo global &quot;de toda la instancia&quot;.

Algunas otras operaciones, como soltar una colección, aún requieren un bloqueo exclusivo de la base de datos.

#### Instantáneas y puntos de comprobación {#snapshots-and-checkpoints}

WiredTiger utiliza el control de simultaneidad de múltiples versiones (MVCC). Al inicio de una operación, WiredTiger proporciona una instantánea puntual de los datos de la transacción. Una instantánea presenta una vista coherente de los datos en memoria.

Al escribir en el disco, WiredTiger escribe todos los datos en una instantánea en el disco de forma coherente en todos los archivos de datos. Los datos ahora [duraderos](https://docs.mongodb.com/manual/reference/glossary/#term-durable) actúan como un punto de comprobación en los archivos de datos. El punto de comprobación garantiza que los archivos de datos sean coherentes hasta el último punto de comprobación, incluido el último; es decir, los puntos de comprobación pueden actuar como puntos de recuperación.

MongoDB configura WiredTiger para crear puntos de comprobación (es decir, escribir los datos de la instantánea en el disco) a intervalos de 60 segundos o 2 gigabytes de datos del diario.

Durante la escritura de un nuevo punto de control, el anterior sigue siendo válido. Como tal, incluso si MongoDB termina o encuentra un error al escribir un nuevo punto de control, al reiniciar, MongoDB puede recuperarse del último punto de control válido.

El nuevo punto de comprobación se vuelve accesible y permanente cuando la tabla de metadatos de WiredTiger se actualiza automáticamente para hacer referencia al nuevo punto de comprobación. Una vez que el nuevo punto de control es accesible, WiredTiger libera las páginas de los puntos de comprobación antiguos.

Usando WiredTiger, incluso sin [transacciones](https://docs.mongodb.com/manual/reference/glossary/#term-durable), MongoDB puede recuperarse del último punto de control; sin embargo, para recuperar los cambios realizados después del último punto de comprobación, ejecute con [diario](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### Diario {#journal}

WiredTiger utiliza un registro de transacciones por adelantado en combinación con [puntos](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints) de comprobación para garantizar la durabilidad de los datos.

El diario WiredTiger mantiene todas las modificaciones de datos entre puntos de comprobación. Si MongoDB sale entre puntos de comprobación, utiliza el diario para reproducir todos los datos modificados desde el último punto de comprobación. Para obtener información sobre la frecuencia con la que MongoDB escribe los datos del diario en el disco, consulte Proceso [de diario](https://docs.mongodb.com/manual/core/journaling/#journal-process).

El diario WiredTiger se comprime con la biblioteca de compresión [inteligente](https://docs.mongodb.com/manual/core/journaling/#journal-process) . Para especificar un algoritmo de compresión alternativo o sin compresión, utilice la configuración [storage.wiredTiger.engineConfig.journalCompressor](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor) .

Para obtener más información, consulte: [Viendo con WiredTiger](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger).

>[!NOTE]
>
>El tamaño mínimo del registro para WiredTiger es de 128 bytes. Si un registro de registro es de 128 bytes o menor, WiredTiger no comprime ese registro.
>
>Puede deshabilitar el diario estableciendo [storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled) en false, lo que puede reducir la sobrecarga del mantenimiento del diario.
>
>Para las instancias [independientes](https://docs.mongodb.com/manual/reference/glossary/#term-standalone) , no utilizar el diario significa que se perderán algunas modificaciones de datos cuando MongoDB se cierre inesperadamente entre puntos de comprobación. Para los miembros de conjuntos [de](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set)réplicas, el proceso de replicación puede proporcionar suficientes garantías de durabilidad.

#### Compresión {#compression}

Con WiredTiger, MongoDB admite compresión para todas las colecciones e índices. La compresión minimiza el uso del almacenamiento a expensas de la CPU adicional.

De forma predeterminada, WiredTiger utiliza la compresión de bloques con la biblioteca de compresión [inteligente](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) para todas las colecciones y la compresión [de](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression) prefijos para todos los índices.

Para las colecciones, también está disponible la compresión de bloques con [zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) . Para especificar un algoritmo de compresión alternativo o sin compresión, utilice la configuración [storage.wiredTiger.collectionConfig.blockCompressor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) .

Para los índices, para deshabilitar la compresión [de](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)prefijos, utilice la configuración [storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression) .

La configuración de la compresión también se puede configurar por colección y por índice durante la creación de la colección y del índice. Consulte [Especificar las opciones](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options) del motor de almacenamiento y la opción [db.collection.createIndex() storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options) .

Para la mayoría de las cargas de trabajo, la configuración de compresión predeterminada equilibra la eficiencia del almacenamiento y los requisitos de procesamiento.

El diario WiredTiger también está comprimido de forma predeterminada. Para obtener información sobre la compresión de asientos, consulte [Diario](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### Uso de memoria {#memory-use}

Con WiredTiger, MongoDB utiliza tanto la caché interna de WiredTiger como la caché del sistema de archivos.

A partir de la versión 3.4, la caché interna de WiredTiger utilizará, de forma predeterminada, la mayor de las siguientes opciones:

* 50% de RAM menos 1 GB, o
* 256 MB

De forma predeterminada, WiredTiger utiliza la compresión de bloques de aplicación para todas las colecciones y la compresión de prefijos para todos los índices. Los valores predeterminados de compresión se pueden configurar a nivel global y también se pueden establecer por colección y por índice durante la creación de la colección y del índice.

Se utilizan diferentes representaciones para los datos en la caché interna de WiredTiger en comparación con el formato en disco:

* Los datos de la memoria caché del sistema de archivos son los mismos que el formato en disco, incluyendo los beneficios de cualquier compresión de archivos de datos. El sistema operativo utiliza la memoria caché del sistema de archivos para reducir la E/S del disco.

Los índices cargados en la memoria caché interna de WiredTiger tienen una representación de datos diferente al formato en disco, pero pueden aprovechar la compresión de prefijos de índice para reducir el uso de RAM.

La compresión de prefijos de índice anula la duplicación de prefijos comunes de campos indexados.

Los datos de recopilación en la caché interna de WiredTiger no están comprimidos y utilizan una representación diferente del formato en disco. La compresión de bloques puede proporcionar ahorros significativos en el almacenamiento de información en disco, pero los datos deben descomprimirse para que los manipule el servidor.

A través de la memoria caché del sistema de archivos, MongoDB utiliza automáticamente toda la memoria libre que no sea utilizada por la memoria caché de WiredTiger o por otros procesos.

Para ajustar el tamaño de la caché interna de WiredTiger, consulte [storage.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) y [—wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb). Evite aumentar el tamaño de caché interna de WiredTiger por encima de su valor predeterminado.

### NUMA {#numa}

El acceso a memoria no uniforme (NUMA) permite al núcleo administrar cómo se asigna la memoria a los núcleos del procesador. Aunque esto intenta acelerar el acceso a la memoria para que los núcleos garanticen que pueden acceder a los datos requeridos, NUMA interfiere con el MMAP que introduce latencia adicional ya que no se puede predecir la lectura. Debido a esto, es necesario deshabilitar NUMA para el `mongod` proceso en todos los sistemas operativos que tengan la capacidad.

En esencia, en una arquitectura NUMA la memoria está conectada a CPUs y las CPUs están conectadas a un bus. En una arquitectura SMP o UMA, la memoria está conectada al bus y compartida por CPU. Cuando un subproceso asigna memoria en una CPU NUMA, la asigna según una política. El valor predeterminado es asignar la memoria conectada a la CPU local del subproceso a menos que no haya espacio libre, en cuyo momento utiliza la memoria de una CPU gratuita a un costo mayor. Una vez asignada, la memoria no se mueve entre las CPU. La asignación se realiza mediante una directiva heredada del subproceso principal, que en última instancia es el subproceso que inició el proceso.

En muchas bases de datos que ven a la máquina como una arquitectura de memoria uniforme de varios núcleos, esto lleva a que la CPU inicial se llene primero y la CPU secundaria se llene más tarde, especialmente si un subproceso central es responsable de asignar búferes de memoria. La solución es cambiar la política de NUMA del subproceso principal utilizado para iniciar el `mongod` proceso.

Esto se puede hacer ejecutando el siguiente comando:

```shell
numactl --interleaved=all <mongod> -f config
```

Esta directiva asigna la memoria de forma rodada en todos los nodos de CPU, lo que garantiza una distribución uniforme en todos los nodos. No genera el acceso de mayor rendimiento a la memoria, como en sistemas con múltiples hardware de CPU. Cerca de la mitad de las operaciones de memoria serán más lentas y estarán sobre el bus, pero no `mongod` se ha escrito para dirigirse a NUMA de una manera óptima, por lo que es un compromiso razonable.

### Problemas de NUMA {#numa-issues}

Si el `mongod` proceso se inicia desde una ubicación distinta a la `/etc/init.d` carpeta, es probable que no se inicie con la directiva NUMA correcta. Dependiendo de la política predeterminada, pueden surgir problemas. Esto se debe a que los diversos instaladores del administrador de paquetes Linux para MongoDB también instalan un servicio con archivos de configuración ubicados en los `/etc/init.d` que realizan el paso descrito anteriormente. Si instala y ejecuta MongoDB directamente desde un archivo ( `.tar.gz`), deberá ejecutar manualmente mongood bajo el `numactl` proceso.

>[!NOTE]
>
>Para obtener más información sobre las políticas de NUMA disponibles, consulte la documentación [numactl](https://linux.die.net/man/8/numactl).

El proceso de MongoDB se comportará de manera diferente bajo diferentes políticas de asignación:

```

```

* `-membind=<nodes>`
Asignar solo en los nodos enumerados. El mongol no asignará memoria en los nodos enumerados y puede que no utilice toda la memoria disponible.

* `-cpunodebind=<nodes>`
Sólo se ejecutan en los nodos. El mongol solo se ejecutará en los nodos especificados y solo usará la memoria disponible en esos nodos.

* `-physcpubind=<nodes>`
Solo se ejecutan en CPU (núcleos) enumeradas. El mongol solo se ejecutará en las CPU enumeradas y solo usará la memoria disponible en esas CPU.

* `--localalloc`
Asigne siempre memoria en el nodo actual, pero utilice todos los nodos en los que se ejecuta el subproceso. Si un subproceso realiza la asignación, sólo se utilizará la memoria disponible para esa CPU.

* `--preferred=<node>`
Prefiere la asignación a un nodo, pero se devuelve a otros si el nodo preferido está lleno. Se puede utilizar notación relativa para definir un nodo. Además, los subprocesos se ejecutan en todos los nodos.

Algunas de las políticas pueden dar como resultado que el `mongod` proceso reciba menos RAM de la que dispone. A diferencia de MySQL, MongoDB evita activamente la paginación a nivel del sistema operativo, y consecuentemente el `mongod` proceso puede obtener menos memoria que parece disponible.

#### Intercambiar {#swapping}

Debido a la gran cantidad de memoria de las bases de datos, el intercambio a nivel de sistema operativo debe deshabilitarse. El proceso MongoDB evitará el intercambio por diseño.

#### Sistemas de archivos remotos {#remote-filesystems}

No se recomiendan los sistemas de archivos remotos como NFS para los archivos de datos internos de MongoDB (los archivos de base de datos de proceso mondial), ya que introducen demasiada latencia. Esto no debe confundirse con el sistema de archivos compartido requerido para el almacenamiento de Oak Blob (FileDataStore), donde se recomienda NFS.

#### Leer adelante {#read-ahead}

Leer hacia delante debe ajustarse para que cuando una página se pagina con una lectura aleatoria, los bloques innecesarios no se leen desde el disco, lo que resulta en un consumo innecesario de ancho de banda de E/S.

### Requisitos de Linux {#linux-requirements}

#### Versiones mínimas del núcleo {#minimum-kernel-versions}

* **2.6.23** para `ext4` filesystems

* **2.6.25** para `xfs` filesystems

#### Configuración recomendada para discos de base de datos {#recommended-settings-for-database-disks}

**Desactivar hora**

Se recomienda desactivar `atime` los discos que contengan las bases de datos.

**Configurar el programador de discos NOOP**

Puede hacerlo mediante:

En primer lugar, compruebe el programador de E/S que está establecido actualmente. Esto se puede hacer ejecutando el siguiente comando:

```shell
cat /sys/block/sdg/queue/scheduler
```

Si la respuesta es `noop` que no hay nada que hacer más.

Si NOOP no es el programador de E/S que está configurado, puede cambiarlo ejecutando:

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**Ajustar el valor de lectura anticipada**

Se recomienda utilizar un valor de 32 para los discos desde los que se ejecutan las bases de datos MongoDB. Esto equivale a 16 kilobytes. Puede configurarlo ejecutando:

```shell
sudo blockdev --setra <value> <device>
```

#### Habilitar NTP {#enable-ntp}

Asegúrese de tener NTP instalado y en ejecución en el equipo que aloja las bases de datos de MongoDB. Por ejemplo, puede instalarlo con el administrador de paquetes yum en un equipo CentOS:

```shell
sudo yum install ntp
```

Una vez que el daemon NTP se haya instalado y se haya iniciado correctamente, puede comprobar el desplazamiento del servidor en el archivo de deriva.

#### Deshabilitar páginas grandes transparentes {#disable-transparent-huge-pages}

Red Hat Linux utiliza un algoritmo de administración de memoria llamado Transparent Enorme Pages (THP). Se recomienda deshabilitarlo si utiliza el sistema operativo para cargas de trabajo de base de datos.

Puede deshabilitarlo siguiendo el procedimiento siguiente:

1. Abra el `/etc/grub.conf` archivo en el editor de texto que desee.
1. Agregue la siguiente línea al archivo grub.conf:

   ```xml
   transparent_hugepage=never
   ```

1. Por último, compruebe si la configuración ha surtido efecto al ejecutar:

   ```shell
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   Si THP está deshabilitado, el resultado del comando anterior debería ser:

   ```xml
   always madvise [never]
   ```

>[!NOTE]
>
>Para obtener más información acerca de las páginas transparentes de gran tamaño, consulte este [artículo](https://access.redhat.com/solutions/46111).

#### Deshabilitar NUMA {#disable-numa}

En la mayoría de las instalaciones en las que NUMA está habilitado, el demonio MongoDB lo desactivará automáticamente si se ejecuta como un servicio desde la `/etc/init.d` carpeta.

Si no es así, puede desactivar NUMA a nivel de proceso. Para desactivarlo, ejecute estos comandos:

```shell
numactl --interleave=all <path_to_process>
```

¿Dónde `<path_to_process>` está el camino hacia el proceso mongoso?

A continuación, deshabilite la recuperación de zona ejecutando:

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### Ajuste la configuración de ulimit para el proceso mondios {#tweak-the-ulimit-settings-for-the-mongod-process}

Linux permite un control configurable sobre la asignación de recursos a través del `ulimit` comando. Esto se puede hacer por usuario o por proceso.

Se recomienda configurar ulimit para el proceso mondios de acuerdo con la Configuración de límite recomendada de [MongoDB](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings).

#### Probar el rendimiento de E/S de MongoDB {#test-mongodb-i-o-performance}

MongoDB proporciona una herramienta llamada `mongoperf` que está diseñada para probar el rendimiento de E/S. Se recomienda que lo utilice para probar el rendimiento de todas las instancias de MongoDB que conforman su infraestructura.

Para obtener información sobre cómo usar `mongoperf`, consulte la documentación [de](https://docs.mongodb.org/manual/reference/program/mongoperf/)MongoDB.

>[!NOTE]
>
>Tenga en cuenta que `mongoperf` está diseñado para ser un indicador del rendimiento de MongoDB en la plataforma en la que se ejecuta. Por ello, los resultados no deben considerarse definitivos para el funcionamiento de un sistema de producción.
>
>Para obtener resultados de rendimiento más precisos, puede ejecutar pruebas complementarias con la herramienta `fio` Linux.

**Probar el rendimiento de lectura en las máquinas virtuales que conforman la implementación**

Después de instalar la herramienta, cambie al directorio de la base de datos MongoDB para ejecutar las pruebas. A continuación, inicie la primera prueba `mongoperf`con esta configuración:

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

La salida deseada debe alcanzar hasta dos gigabytes por segundo (2 GB/s) y 500.000 IOPS que se ejecutan en 32 subprocesos para todas las instancias de MongoDB.

Ejecute una segunda prueba, esta vez con archivos asignados a memoria, estableciendo el `mmf:true` parámetro:

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

La salida de la segunda prueba debe ser considerablemente mayor que la primera, lo que indica el rendimiento de la transferencia de memoria.

>[!NOTE]
>
>Al realizar las pruebas, compruebe las estadísticas de uso de E/S de las máquinas virtuales en cuestión en el sistema de supervisión del sistema operativo. Si indican valores inferiores al 100 por ciento para lecturas de E/S, puede que haya algún problema con la máquina virtual.

**Probar el rendimiento de escritura de la instancia principal de MongoDB**

A continuación, compruebe el rendimiento de escritura de E/S de la instancia principal de MongoDB ejecutándose `mongoperf` desde el directorio de base de datos MongoDB con la misma configuración:

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

La salida deseada debería ser de 12 megabytes por segundo y alcanzar alrededor de 3000 IOPS, con poca variación entre el número de subprocesos.

## Pasos para entornos virtualizados {#steps-for-virtualised-environments}

### VMWare {#vmware}

Si está utilizando WMWare ESX para administrar e implementar sus entornos virtualizados, asegúrese de realizar las siguientes configuraciones desde la consola ESX a fin de acomodar la operación MongoDB:

1. Desactivación de la ampliación de memoria
1. Asignar previamente y reservar memoria para las máquinas virtuales que alojarán las bases de datos MongoDB
1. Utilice el Control de E/S de almacenamiento para asignar suficiente E/S al `mongod` proceso.
1. Garantizar los recursos de CPU de los equipos que alojan MongoDB configurando Reserva [de CPU](https://pubs.vmware.com/vsphere-4-esx-vcenter/index.jsp?topic=/com.vmware.vsphere.vmadmin.doc_41/vsp_vm_guide/configuring_virtual_machines/t_allocate_cpu_resources.html)

1. Considere el uso de controladores de E/S ParaVirtual. Para obtener más información sobre cómo hacerlo, consulte este artículo [de la base de](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1010398)conocimiento.

### Amazon Web Services {#amazon-web-services}

Para obtener documentación sobre cómo configurar MongoDB con Amazon Web Services, consulte el artículo [Configurar la integración](https://docs.cloud.mongodb.com/tutorial/configure-aws-settings/) de AWS en el sitio Web de MongoDB.

## Seguridad de MongoDB antes de la implementación {#securing-mongodb-before-deployment}

Consulte esta publicación sobre la implementación [segura de MongoDB](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html) para obtener consejos sobre cómo asegurar la configuración de las bases de datos antes de la implementación.

## Dispatcher {#dispatcher}

### Elección del sistema operativo del despachante {#choosing-the-operating-system-for-the-dispatcher}

Para poder servir correctamente la implementación de MongoDB, el sistema operativo que alojará al despachante debe estar ejecutando **Apache httpd** **versión 2.4 o superior.**

Además, asegúrese de que todas las bibliotecas utilizadas en la compilación están actualizadas para minimizar las implicaciones de seguridad.

### Dispatcher Configuration {#dispatcher-configuration}

Una configuración de despachante típica servirá entre diez y veinte veces más el rendimiento de la solicitud de una única instancia de AEM.

Dado que el despachante es principalmente apátrida, puede escalarse horizontalmente con facilidad. En algunas implementaciones, es necesario restringir el acceso de los autores a determinados recursos. Debido a esto, se recomienda utilizar un despachante con las instancias de autor.

La ejecución de AEM sin despachante requerirá que otra aplicación realice la terminación de SSL y el equilibrio de carga. Esto es necesario porque las sesiones deben tener afinidad con la instancia de AEM en la que han creado, concepto conocido como conexiones adhesivas. El propósito de esto es garantizar que las actualizaciones del contenido muestren una latencia mínima.

Consulte la documentación [de](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) Dispatcher para obtener más información sobre cómo configurarla.

### Configuración adicional {#additional-configuration}

#### Conexiones adhesivas {#sticky-connections}

Las conexiones estrictas garantizan que las páginas personalizadas y los datos de sesión de un usuario se componen en la misma instancia de AEM. Estos datos se almacenan en la instancia, por lo que las solicitudes posteriores del mismo usuario volverán a la misma instancia.

Se recomienda habilitar las conexiones adhesivas para todas las solicitudes de enrutamiento de capas internas a las instancias de AEM, lo que anima a las solicitudes posteriores a llegar a la misma instancia de AEM. Esto ayudará a minimizar la latencia que, de lo contrario, se notará cuando el contenido se actualice entre instancias.

#### Caduca larga {#long-expires}

De forma predeterminada, el contenido enviado desde un despachante de AEM tiene encabezados Última modificación y Etag, sin indicar la caducidad del contenido. Aunque esto garantiza que la interfaz de usuario siempre obtenga la versión más reciente del recurso, también significa que el explorador realizará una operación GET para comprobar si el recurso ha cambiado. Esto puede resultar en varias solicitudes a las que la respuesta HTTP es 304 (sin modificar), según la carga de la página. Para los recursos que se sabe que no caducan, si se configura un encabezado Expires y se eliminan los encabezados Last-Modified y ETag, el contenido se almacenará en caché y no se realizarán más solicitudes de actualización hasta que se cumpla la fecha en el encabezado Expires.

Sin embargo, el uso de este método significa que no hay una manera razonable de hacer que el recurso caduque en el explorador antes de que caduque el encabezado Caduca. Para mitigar esto, se puede configurar HtmlClientLibraryManager para que utilice direcciones URL inmutables para las bibliotecas de cliente.

Se garantiza que estas direcciones URL no cambien. Cuando cambie el cuerpo del recurso contenido en la dirección URL, los cambios se reflejarán automáticamente en la dirección URL, lo que garantiza que el explorador solicitará la versión correcta del recurso.

La configuración predeterminada agrega un selector a HtmlClientLibraryManager. Al ser un selector, el recurso se almacena en caché en el despachante con el selector intacto. Este selector también se puede utilizar para garantizar el comportamiento de caducidad correcto. El selector predeterminado sigue el `lc-.*?-lc` patrón. Las siguientes directivas de configuración httpd de Apache asegurarán que todas las solicitudes que coincidan con ese patrón se proporcionen con una hora de caducidad adecuada.

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### Sin recorte {#no-sniff}

Cuando el contenido se envía sin tipo de contenido, muchos exploradores intentarán adivinar el tipo de contenido leyendo los primeros bytes del contenido. Esto se llama &quot;husmear&quot;. El borrado abre una vulnerabilidad de seguridad, ya que los usuarios que pueden escribir en el repositorio pueden cargar contenido malintencionado sin tipo de contenido.

Por este motivo, es aconsejable agregar un `no-sniff` encabezado a los recursos proporcionados por el distribuidor. Sin embargo, el despachante no almacena en caché los encabezados. Esto significa que cualquier contenido servido desde el sistema de archivos local tendrá su tipo de contenido determinado por su extensión, en lugar de utilizar el encabezado de tipo de contenido original de su servidor de origen AEM.

No se puede habilitar ningún sniff de forma segura si se sabe que la aplicación web nunca proporciona recursos en caché sin un tipo de archivo.

Puede activar Sin recorte de forma inclusiva:

```xml
Header set X-Content-Type-Options "nosniff"
```

También se puede habilitar de forma selectiva:

```xml
RewriteCond %{REQUEST_URI} \.(?:js|jsonp)$ [OR]
RewriteCond %{QUERY_STRING} (callback|jsonp|cb)=\w+
RewriteRule .* - [E=jsonp_request:1]
Header set X-Content-Type-Options "nosniff"  env=jsonp_request
Header setifempty Content-Type application/javascript env=jsonp_request
```

#### Directiva de seguridad del contenido {#content-security-policy}

La configuración predeterminada del distribuidor permite abrir una directiva de seguridad de contenido, también conocida como CSP. Esto permite que una página cargue recursos de todos los dominios sujetos a las directivas predeterminadas del entorno limitado del explorador.

Es recomendable restringir el lugar desde el que se pueden cargar los recursos para evitar cargar código en el motor de javascript desde servidores extranjeros no confiables o no verificados.

El CSP permite perfeccionar las políticas. Sin embargo, en una aplicación compleja, los encabezados CSP deben desarrollarse con cuidado, ya que las políticas demasiado restrictivas pueden dañar partes de la interfaz de usuario.

>[!NOTE]
>
>Para obtener más información sobre cómo funciona, consulte la página [OWASP sobre la directiva](https://www.owasp.org/index.php/Content_Security_Policy)de seguridad de contenido.

### Tamaño {#sizing}

Para obtener más información sobre el tamaño, consulte las Directrices [de cambio de tamaño de hardware](/help/managing/hardware-sizing-guidelines.md).

### Optimización del rendimiento de MongoDB {#mongodb-performance-optimization}

Para obtener información genérica sobre el rendimiento de MongoDB, consulte [Análisis del rendimiento](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/)de MongoDB.

## Limitaciones conocidas {#known-limitations}

### Instalaciones simultáneas {#concurrent-installations}

Aunque MongoMK admite el uso simultáneo de varias instancias de AEM con una sola base de datos, las instalaciones simultáneas no.

Para solucionar esto, asegúrese de ejecutar primero la instalación con un solo miembro y agregar los demás después de que el primero haya terminado de realizar la instalación.

### Longitud del nombre de la página {#page-name-length}

If AEM is running on a MongoMK persistence manager deployment, [page names are limited to 150 characters.](/help/sites-authoring/managing-pages.md)

>[!NOTE]
>
>[Consulte la documentación](https://docs.mongodb.com/manual/reference/limits/) de MongoDB para familiarizarse con las limitaciones y umbrales conocidos de MongoDB.

