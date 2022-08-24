---
title: AEM con MongoDB
seo-title: AEM with MongoDB
description: Obtenga información sobre las tareas y consideraciones necesarias para una AEM correcta con la implementación de MongoDB.
seo-description: Learn about the tasks and considerations needed for a successful AEM with MongoDB deployment.
uuid: 8028832d-10de-4811-a769-fab699c162ec
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cd3b979f-53d4-4274-b4eb-a9533329192a
docset: aem65
exl-id: 70a39462-8584-4c76-a097-05ee436247b7
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '6496'
ht-degree: 0%

---

# AEM con MongoDB{#aem-with-mongodb}

Este artículo pretende mejorar los conocimientos sobre las tareas y consideraciones necesarias para implementar correctamente Adobe Experience Manager con MongoDB.

Para obtener más información relacionada con la implementación, consulte la [Implementación y mantenimiento](/help/sites-deploying/deploy.md) de la documentación.

## Cuándo usar MongoDB con AEM {#when-to-use-mongodb-with-aem}

MongoDB se utilizará normalmente para admitir implementaciones de AEM autor cuando se cumpla uno de los siguientes criterios:

* Más de 1000 usuarios únicos al día;
* Más de 100 usuarios simultáneos;
* Grandes volúmenes de ediciones de páginas;
* Grandes lanzamientos o activaciones.

Los criterios anteriores son solo para las instancias de autor y no para ninguna instancia de publicación que debería estar basada en TarMK. El número de usuarios hace referencia a usuarios autenticados, ya que las instancias de autor no permiten el acceso no autenticado.

Si no se cumplen los criterios, se recomienda una implementación TarMK activa/en espera para abordar la disponibilidad. Por lo general, MongoDB debe considerarse en situaciones en las que los requisitos de escalado sean más de lo que se puede lograr con un solo elemento de hardware.

>[!NOTE]
>
>Puede encontrar información adicional sobre el tamaño de las instancias de autor y la definición de usuarios simultáneos en la [Pautas para el tamaño del hardware](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel).

### Implementación mínima de MongoDB para AEM {#minimal-mongodb-deployment-for-aem}

A continuación se muestra una implementación mínima para AEM en MongoDB. Para simplificar, se han generalizado los componentes de terminación SSL y proxy HTTP. Consiste en un único conjunto de réplicas MongoDB, con uno primario y dos secundarios.

![Chlimage_1-4](assets/chlimage_1-4.png)

Una implementación mínima requiere 3 `mongod` instancias configuradas como un conjunto de réplicas. Una instancia se elegirá principal y las otras instancias serán secundarias, y la elección será administrada por `mongod`. Adjunto a cada instancia hay un disco local. Para que el clúster admita la carga, se recomienda una ganancia mínima de 12 MB/s con más de 3000 operaciones de E/S por segundo (IOPS).

Los AEM autores están conectados al `mongod` instancias, con cada autor AEM conectándose a las tres `mongod` instancias. Las escrituras se envían a la primaria y las lecturas se pueden leer desde cualquiera de las instancias. El tráfico se distribuye en función de la carga de Dispatcher en cualquiera de las instancias de autor de AEM activas. El almacén de datos de OAK es un `FileDataStore`, y MongoDB es proporcionado por MMS o MongoDB Ops Manager según la ubicación de la implementación. Las soluciones de terceros, como Splunk o Ganglia, proporcionan la monitorización del registro y el nivel del sistema operativo.

En esta implementación, todos los componentes son necesarios para una implementación correcta. Cualquier componente que falte dejará la implementación sin funcionar.

### Sistemas operativos {#operating-systems}

Para obtener una lista de los sistemas operativos compatibles con AEM 6, consulte la [Página Requisitos técnicos](/help/sites-deploying/technical-requirements.md).

### Entornos {#environments}

Los entornos virtualizados son compatibles siempre que exista una buena comunicación entre los diferentes equipos técnicos que ejecutan el proyecto. Esto incluye el equipo que está ejecutando AEM, el equipo propietario del sistema operativo y el equipo que administra la infraestructura virtualizada.

Existen requisitos específicos que cubren la capacidad de E/S de las instancias de MongoDB que deben ser administradas por el equipo que administra el entorno virtualizado. Si el proyecto utiliza una implementación en la nube, como Amazon Web Service, las instancias deberán estar aprovisionadas con suficiente capacidad de E/S y coherencia para admitir las instancias de MongoDB. De lo contrario, los procesos MongoDB y el repositorio Oak se ejecutarán de forma infiable y errática.

En los entornos virtualizados, MongoDB requerirá configuraciones específicas de E/S y VM para garantizar que el motor de almacenamiento de MongoDB no se vea paralizado por las políticas de asignación de recursos de VMWare. Una implementación exitosa garantizará que no haya barreras entre los distintos equipos y que todos estén registrados para ofrecer el rendimiento requerido.

## Consideraciones sobre hardware {#hardware-considerations}

### Almacenamiento {#storage}

Para lograr el rendimiento de lectura y escritura para un mejor rendimiento sin necesidad de escalado horizontal prematuro, MongoDB generalmente requiere almacenamiento SSD o almacenamiento con un rendimiento equivalente a SSD.

### RAM {#ram}

Las versiones 2.6 y 3.0 de MongoDB que utilizan el motor de almacenamiento MAP requieren que el conjunto de trabajo de la base de datos y sus índices encaje en RAM.

La insuficiencia de RAM dará lugar a una reducción significativa del rendimiento. El tamaño del conjunto de trabajo y de la base de datos depende en gran medida de la aplicación. Si bien se pueden hacer algunas estimaciones, la manera más fiable de determinar la cantidad de RAM necesaria es crear la aplicación AEM y probarla de carga.

Para ayudar con el proceso de prueba de carga, se puede asumir la siguiente relación entre el conjunto de trabajo y el tamaño total de la base de datos:

* 1:10 para almacenamiento SSD
* 1:3 para almacenamiento en disco duro

Esto significa que en el caso de implementaciones de SSD, se necesitarán 200 GB de RAM para una base de datos de 2 TB.

Aunque las mismas limitaciones se aplican al motor de almacenamiento WiredTiger en MongoDB 3.0, la correlación entre el conjunto de trabajo, la RAM y los errores de página no es tan fuerte como WiredTiger no utiliza la asignación de memoria de la misma manera que lo hace el motor de almacenamiento MAP.

>[!NOTE]
>
>Adobe recomienda utilizar el motor de almacenamiento WiredTiger para implementaciones AEM 6.1 que utilicen MongoDB 3.0.

### Almacén de datos {#data-store}

Debido a las limitaciones del conjunto de trabajo de MongoDB, se recomienda mantener el almacén de datos independiente del MongoDB. En la mayoría de los entornos a `FileDataStore` debe usarse el uso de un NAS disponible para todas AEM instancias. Para situaciones en las que se utiliza Amazon Web Service, también existe un `S3 DataStore`. Si, por cualquier motivo, el almacén de datos se mantiene dentro de MongoDB, el tamaño del almacén de datos debe agregarse al tamaño total de la base de datos y los cálculos del conjunto de trabajo deben ajustarse adecuadamente. Esto puede significar un aprovisionamiento significativamente mayor de RAM para mantener el rendimiento sin errores de página.

## Monitoreo {#monitoring}

La supervisión es fundamental para que el proyecto se ejecute con éxito. Aunque con suficiente conocimiento es posible ejecutar AEM en MongoDB sin supervisión, ese conocimiento normalmente se encuentra en ingenieros especializados para cada sección del despliegue.

Normalmente, esto implica que un ingeniero de I+D trabaja en el Apache Oak Core y un especialista de MongoDB.

Sin supervisión a todos los niveles, se necesitará un conocimiento detallado de la base de código para diagnosticar los problemas. Con la supervisión y la orientación adecuada sobre las principales estadísticas, los equipos de implementación podrán reaccionar adecuadamente ante las anomalías.

Aunque es posible utilizar herramientas de línea de comandos para obtener una instantánea rápida de la operación de un clúster, hacerlo en tiempo real en muchos hosts es casi imposible. Las herramientas de línea de comandos rara vez proporcionan información histórica después de unos minutos y nunca permiten la correlación cruzada entre distintos tipos de métricas. Un breve periodo de fondo lento `mongod` la sincronización requiere un esfuerzo manual significativo para correlacionarse con los niveles de espera de E/S o de escritura excesivos con un recurso de almacenamiento compartido desde una máquina virtual aparentemente desconectada.

### MongoDB Cloud Manager {#mongodb-cloud-manager}

MongoDB Cloud Manager es un servicio gratuito ofrecido por MongoDB que permite la supervisión y administración de instancias de MongoDB. Proporciona una visión del rendimiento y el estado del clúster MongoDB en tiempo real. Administra instancias tanto en la nube como alojadas de forma privada, siempre que la instancia pueda acceder al servidor de supervisión de Cloud Manager.

Requiere un agente instalado en la instancia MongoDB que se conecte al servidor de monitorización. Hay 3 niveles del agente:

* Un agente de automatización que puede automatizar completamente todo en el servidor MongoDB,
* Un agente de monitorización que puede monitorizar la variable `mongod` instancia,
* Agente de copia de seguridad que puede realizar copias de seguridad programadas de los datos.

Aunque el uso de Cloud Manager para la automatización de mantenimiento de un clúster MongoDB facilita muchas de las tareas rutinarias, no es obligatorio y tampoco lo es para la copia de seguridad. Sin embargo, al elegir Cloud Manager para monitorizar, es necesario monitorizar.

Para obtener más información sobre MongoDB Cloud Manager, consulte la [Documentación de MongoDB](https://docs.cloud.mongodb.com/).

### Administrador de operaciones de MongoDB {#mongodb-ops-manager}

MongoDB Ops Manager es el mismo software que MongoDB Cloud Manager. Una vez registrado, Ops Manager puede descargarse e instalarse localmente en un centro de datos privado o en cualquier otro equipo portátil o de escritorio. Utiliza una base de datos local de MongoDB para almacenar datos y comunicarse de la misma manera que Cloud Manager con los servidores administrados. Si tiene directivas de seguridad que prohíben un agente de supervisión, debe utilizar el Administrador de operaciones de MongoDB.

### Supervisión del sistema operativo {#operating-system-monitoring}

Para ejecutar un clúster AEM MongoDB es necesario supervisar el nivel del sistema operativo.

Ganglia es un buen ejemplo de este sistema y proporciona una imagen sobre el rango y detalle de la información requerida que va más allá de las métricas básicas de salud como CPU, promedio de carga y espacio libre en disco. Para diagnosticar problemas, se requiere información de nivel inferior como niveles de pool de entropía, espera de E/S de CPU, sockets en estado FIN_WAIT2.

### Agregación de registros {#log-aggregation}

Con un clúster de varios servidores, la agregación de registros centrales es un requisito para un sistema de producción. Software como Splunk admite la agregación de registros y permite a los equipos analizar los patrones de comportamiento de la aplicación sin tener que recopilar manualmente los registros.

## Listas de comprobación {#checklists}

Esta sección trata de los pasos que debe seguir para asegurarse de que las implementaciones de AEM y MongoDB estén configuradas correctamente antes de implementar el proyecto.

### Red {#network}

1. En primer lugar, asegúrese de que todos los hosts tengan una entrada DNS
1. Todos los hosts deben ser resueltos por su entrada DNS de todos los demás hosts enrutables
1. Todos los hosts de MongoDB son enrutables de todos los demás hosts de MongoDB del mismo clúster
1. Los hosts MongoDB pueden enrutar paquetes a MongoDB Cloud Manager y a los demás servidores de monitorización
1. Los servidores AEM pueden enrutar paquetes a todos los servidores MongoDB
1. La latencia de paquetes entre cualquier servidor AEM y cualquier servidor MongoDB es menor a dos milisegundos, sin pérdida de paquetes y una distribución estándar de un milisegundo o menos.
1. Asegúrese de que no haya más de dos saltos entre un AEM y un servidor MongoDB
1. No hay más de dos saltos entre dos servidores MongoDB
1. No hay enrutadores superiores a OSI Level 3 entre cualquier servidor principal (MongoDB o AEM o cualquier combinación).
1. Si se utiliza el trunking VLAN o cualquier forma de tunelización de red, debe cumplir con las comprobaciones de latencia del paquete.

### Configuración AEM {#aem-configuration}

#### Configuración del almacén de nodos {#node-store-configuration}

Las instancias AEM deben configurarse para utilizar AEM con MongoMK. La base de la implementación de MongoMK en AEM es Document Node Store.

Para obtener más información sobre cómo configurar los almacenes de nodos, consulte [Configuración de almacenes de nodos y almacenes de datos en AEM](/help/sites-deploying/data-store-config.md).

A continuación se muestra un ejemplo de la configuración del almacén de nodos de documentos para una implementación mínima de MongoDB:

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
Este es el servidor MongoDB al que AEM conectar. Las conexiones se realizan a todos los miembros conocidos del conjunto de réplicas predeterminado. Si se utiliza MongoDB Cloud Manager, la seguridad del servidor está habilitada. Por lo tanto, la cadena de conexión debe contener un nombre de usuario y una contraseña adecuados. Las versiones no empresariales de MongoDB solo admiten autenticación de nombre de usuario y contraseña. Para obtener más información sobre la sintaxis de la cadena de conexión, consulte la [documentación](https://docs.mongodb.org/manual/reference/connection-string/).

* `db`
Nombre de la base de datos. El valor predeterminado de AEM es 
`aem-author`.

* `customBlobStore`
Si la implementación almacena binarios en la base de datos, formarán parte del conjunto de trabajo. Por esta razón, se recomienda no almacenar binarios dentro de MongoDB, prefiriendo un almacén de datos alternativo como un 
`FileSystem` almacén de datos en un NAS.

* `cache`
El tamaño de la caché en megabytes. Esto se distribuye entre las distintas cachés utilizadas en la variable 
`DocumentNodeStore`. El valor predeterminado es 256 MB. Sin embargo, el rendimiento de lectura de Oak se beneficiará de una caché más grande.

* `blobCacheSize`
Los blobs utilizados con frecuencia pueden almacenarse en la caché de AEM para evitar que se recuperen del almacén de datos. Esto tendrá un mayor impacto en el rendimiento, especialmente cuando se almacenan blobs en la base de datos MongoDB. Todos los Almacenes de datos basados en el sistema de archivos se beneficiarán de la caché de disco a nivel del sistema operativo.

#### Configuración del almacén de datos {#data-store-configuration}

El almacén de datos se utiliza para almacenar archivos de un tamaño mayor que un umbral. Por debajo de ese umbral, los archivos se almacenan como propiedades dentro del almacén de nodos de documentos. Si la variable `MongoBlobStore` se utiliza, se crea una colección dedicada en MongoDB para almacenar los blobs. Esta colección contribuye al conjunto de trabajo del `mongod` y requerirán que `mongod` tiene más RAM para evitar problemas de rendimiento. Por este motivo, la configuración recomendada es evitar el `MongoBlobStore` para implementaciones de producción y uso `FileDataStore` respaldado por un NAS compartido entre todas las instancias AEM. Dado que la caché a nivel del sistema operativo es eficiente en la administración de archivos, el tamaño mínimo de un archivo en disco debe establecerse cerca del tamaño de bloque del disco, de modo que el sistema de archivos se utilice de manera eficiente y muchos documentos pequeños no contribuyan excesivamente al conjunto de trabajo del `mongod` instancia.

Esta es una configuración típica del almacén de datos para una implementación de AEM mínima con MongoDB:

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
Tamaño en bytes. Los binarios cuyo tamaño sea menor o igual que este tamaño se almacenan con el almacén de nodos de documentos. En lugar de almacenar el ID del blob, se almacena el contenido del binario. Para binarios buenos de este tamaño, el ID del binario se almacena como una propiedad del Document en la colección de nodos y el cuerpo del binario se almacena en la variable 
`FileDataStore` en disco. 4096 bytes es un tamaño típico de bloque del sistema de archivos.

* `path`
Ruta a la raíz del almacén de datos. Para una implementación MongoMK, debe ser un sistema de archivos compartido disponible para todas las instancias AEM. Normalmente se utiliza un servidor de Almacenamiento conectado en red (NAS). Para implementaciones en la nube como Amazon Web Service, la variable 
`S3DataFileStore` también está disponible.

* `cacheSizeInMB`
El tamaño total de la caché binaria en megabytes. Se utiliza para almacenar en caché los binarios inferiores a la variable 
`maxCacheBinarySize` configuración.

* `maxCachedBinarySize`
El tamaño máximo en bytes de un binario almacenado en caché en la caché binaria. Si se utiliza un almacén de datos basado en el sistema de archivos, no se recomienda utilizar valores altos para la caché del almacén de datos, ya que el sistema operativo ya almacena en caché los binarios.

#### Desactivación de la sugerencia de consulta {#disabling-the-query-hint}

Se recomienda deshabilitar la sugerencia de consulta enviada con todas las consultas agregando la propiedad

`-Doak.mongo.disableIndexHint=true`

al iniciar AEM. De esta manera, MongoDB calculará en el índice más apropiado para usar basado en estadísticas internas.

Si la sugerencia de consulta no está deshabilitada, cualquier ajuste de rendimiento de los índices no tendrá ningún impacto en el rendimiento de AEM.

#### Habilitar caché persistente para MongoMK {#enable-persistent-cache-for-mongomk}

Se recomienda habilitar una configuración de caché persistente para implementaciones MongoDB, con el fin de maximizar la velocidad para entornos con alto rendimiento de lectura de E/S. Para obtener más información, consulte la [Documentación de Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html).

## Optimizaciones del sistema operativo MongoDB {#mongodb-operating-system-optimizations}

### Compatibilidad con sistemas operativos {#operating-system-support}

MongoDB 2.6 utiliza un motor de almacenamiento asignado a memoria que es sensible a algunos aspectos de la administración a nivel de sistema operativo entre RAM y disco. El rendimiento de consulta y lectura de la instancia de MongoDB se basa en evitar o eliminar las operaciones de E/S lentas a menudo denominadas errores de página. Estos son errores de página que se aplican al `mongod` en particular. No deben confundirse con los errores de página a nivel de sistema operativo.

Para un funcionamiento rápido, la base de datos MongoDB solo debe acceder a los datos que ya están en RAM. Los datos a los que debe acceder están formados por índices y datos. Esta colección de índices y datos se denomina conjunto de trabajo. Cuando el conjunto de trabajo es más grande que la RAM disponible, MongoDB debe paginar esos datos desde el disco incurriendo en un coste de E/S, desalojando otros datos que ya están en memoria. Si el desalojo hace que los datos se vuelvan a cargar desde los errores de la página del disco, el rendimiento se verá afectado. Cuando el conjunto de trabajo es dinámico y variable, se incurrirán más errores de página para admitir operaciones.

MongoDB se ejecuta en una serie de sistemas operativos que incluyen una amplia variedad de sabores Linux, Windows y el sistema operativo Mac. Consulte [https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms) para obtener más información. Según la elección del sistema operativo, MongoDB tiene diferentes recomendaciones a nivel de sistema operativo. Hay documentos en [https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration) y resumido aquí para mayor comodidad.

#### Linux {#linux}

* Desactive las páginas de abrazos transparentes y desactívelo. Consulte [Configuración transparente de páginas grandes](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/) para obtener más información.
* [Ajuste de la configuración de lectura por adelantado](https://docs.mongodb.com/manual/administration/production-notes/#readahead) en los dispositivos que almacenan los archivos de base de datos para adaptarlos a su caso de uso.

   * Para el motor de almacenamiento MAPv1, si el conjunto de trabajo es más grande que la RAM disponible y el patrón de acceso al documento es aleatorio, considere la posibilidad de reducir el avance a 32 o 16. Evalúe diferentes configuraciones para encontrar un valor óptimo que maximice la memoria residente y reduzca el número de errores de página.
   * Para el motor de almacenamiento WiredTiger, establezca readadvance en 0 independientemente del tipo de medio de almacenamiento (giro, SSD, etc.). En general, utilice la configuración de lectura por adelantado recomendada a menos que las pruebas muestren un beneficio medible, repetible y fiable en un valor de lectura por adelantado más alto. [Soporte profesional de MongoDB](https://docs.mongodb.com/manual/administration/production-notes/#readahead) puede proporcionar consejos y directrices sobre configuraciones de readforward distintas de cero.

* Deshabilite la herramienta sintonizada si está ejecutando RHEL 7/CentOS 7 en un entorno virtual.
* Cuando RHEL 7 / CentOS 7 se ejecuta en un entorno virtual, la herramienta sintonizada invoca automáticamente un perfil de rendimiento derivado del rendimiento, que establece automáticamente la configuración de readforward en 4 MB. Esto puede afectar negativamente al rendimiento.
* Utilice los programadores de discos noop o deadline para las unidades SSD.
* Utilice el programador de discos noop para unidades virtualizadas en VM invitadas.
* Desactive NUMA o establezca vm.zone_reclaim_mode en 0 y ejecute [mondios](https://docs.mongodb.com/manual/administration/production-notes/#readahead) instancias con entrelazado de nodos. Consulte: [Hardware MongoDB y NUMA](https://docs.mongodb.com/manual/administration/production-notes/#readahead) para obtener más información.

* Ajuste los valores límite del hardware para adaptarlos a su caso de uso. Si es múltiple [mondios](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) o [mongo](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) se ejecutan bajo el mismo usuario, escale los valores límite en consecuencia. Consulte: [Configuración de límite de UNIX](https://docs.mongodb.com/manual/reference/ulimit/) para obtener más información.

* Use la nota para el [dbPath](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath) punto de montaje.
* Configure suficientes controladores de archivos (fs.file-max), límite de pid del núcleo (kernel.pid_max) y máximo de subprocesos por proceso (kernel.threads-max) para su implementación. Para los sistemas grandes, los siguientes valores proporcionan un buen punto de partida:

   * fs.file-max valor de 98000,
   * valor kernel.pid_max de 64000,
   * andkernel.threads-max valor de 64000

* Asegúrese de que el sistema tenga configurado el espacio de intercambio. Consulte la documentación del sistema operativo para obtener más información sobre el tamaño adecuado.
* Asegúrese de que el sistema de mantenimiento TCP predeterminado está configurado correctamente. Un valor de 300 a menudo proporciona un mejor rendimiento para conjuntos de réplicas y clústeres compartidos. Consulte: [¿El tiempo de mantenimiento de TCP afecta a las implementaciones de MongoDB?](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) en las Preguntas más frecuentes para obtener más información.

#### Windows {#windows}

* Considere desactivar las actualizaciones de &quot;hora de último acceso&quot; de NTFS. Esto es similar a deshabilitar la hora en sistemas similares a Unix.

### WiredTiger {#wiredtiger}

A partir de MongoDB 3.2 el motor de almacenamiento predeterminado para MongoDB es el motor de almacenamiento WiredTiger. Este motor proporciona una serie de funciones sólidas y escalables, lo que lo hace mucho mejor para cargas de trabajo generales de bases de datos. Las secciones siguientes describen estas funciones.

#### Conversión de nivel de documento {#document-level-concurrency}

WiredTiger utiliza el control de concurrencia a nivel de documento para operaciones de escritura. Como resultado, varios clientes pueden modificar diferentes documentos de una colección al mismo tiempo.

Para la mayoría de las operaciones de lectura y escritura, WiredTiger utiliza un control de concurrencia optimista. WiredTiger solo utiliza bloqueos de intención en los niveles global, de base de datos y de recopilación. Cuando el motor de almacenamiento detecta conflictos entre dos operaciones, se producirá un conflicto de escritura que hará que MongoDB vuelva a intentar esa operación de forma transparente. Algunas operaciones globales, generalmente operaciones de corta duración que involucran múltiples bases de datos, aún requieren un bloqueo global &quot;en toda la instancia&quot;.

Algunas otras operaciones, como soltar una colección, aún requieren un bloqueo exclusivo de la base de datos.

#### Instantáneas y puntos de comprobación {#snapshots-and-checkpoints}

WiredTiger utiliza MultiVersion Concurrency Control (MVCC). Al inicio de una operación, WiredTiger proporciona una instantánea puntual de los datos de la transacción. Una instantánea presenta una vista coherente de los datos en memoria.

Al escribir en disco, WiredTiger escribe todos los datos en una instantánea en disco de forma consistente en todos los archivos de datos. El ahora- [durable](https://docs.mongodb.com/manual/reference/glossary/#term-durable) Los datos actúan como un punto de comprobación en los archivos de datos. El punto de comprobación garantiza que los archivos de datos sean coherentes hasta el último punto de comprobación, incluido el que lo incluya; es decir, los puntos de comprobación pueden actuar como puntos de recuperación.

MongoDB configura WiredTiger para crear puntos de comprobación (es decir, escribir los datos de la instantánea en el disco) a intervalos de 60 segundos o 2 gigabytes de datos del diario.

Durante la escritura de un nuevo punto de comprobación, el punto de comprobación anterior sigue siendo válido. Como tal, incluso si MongoDB termina o encuentra un error mientras escribe un nuevo punto de comprobación, al reiniciar, MongoDB puede recuperarse del último punto de comprobación válido.

El nuevo punto de comprobación se vuelve accesible y permanente cuando la tabla de metadatos de WiredTiger se actualiza automáticamente para hacer referencia al nuevo punto de comprobación. Una vez que se puede acceder al nuevo punto de comprobación, WiredTiger libera las páginas de los puntos de comprobación antiguos.

Uso de WiredTiger, incluso sin [diario](https://docs.mongodb.com/manual/reference/glossary/#term-durable), MongoDB puede recuperarse del último punto de comprobación; sin embargo, para recuperar los cambios realizados después del último punto de comprobación, ejecute con [diario](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### Diario {#journal}

WiredTiger utiliza un registro de transacciones por adelantado en combinación con [puntos de comprobación](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints) para garantizar la durabilidad de los datos.

El diario WiredTiger mantiene todas las modificaciones de datos entre puntos de comprobación. Si MongoDB sale entre puntos de comprobación, utiliza el diario para reproducir todos los datos modificados desde el último punto de comprobación. Para obtener información sobre la frecuencia con la que MongoDB escribe los datos del diario en disco, consulte [Proceso de diario](https://docs.mongodb.com/manual/core/journaling/#journal-process).

El diario WiredTiger se comprime mediante la variable [snply](https://docs.mongodb.com/manual/core/journaling/#journal-process) biblioteca de compresión. Para especificar un algoritmo de compresión alternativo o sin compresión, utilice la variable [storage.wiredTiger.engineConfig.journalCompressor](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor) configuración.

Para obtener más información, consulte: [Recorriendo con WiredTiger](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger).

>[!NOTE]
>
>El tamaño mínimo del registro para WiredTiger es de 128 bytes. Si un registro es de 128 bytes o menor, WiredTiger no comprime ese registro.
>
>Puede deshabilitar el diario estableciendo [storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled) en false, lo que puede reducir la sobrecarga de mantenimiento del historial.
>
>Para [independiente](https://docs.mongodb.com/manual/reference/glossary/#term-standalone) , al no utilizar el historial, se pierden algunas modificaciones de datos cuando MongoDB se cierre inesperadamente entre puntos de comprobación. Para miembros de [conjuntos de réplicas](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set), el proceso de replicación puede proporcionar suficientes garantías de durabilidad.

#### Compresión {#compression}

Con WiredTiger, MongoDB soporta la compresión para todas las colecciones e índices. La compresión minimiza el uso del almacenamiento a expensas de la CPU adicional.

De forma predeterminada, WiredTiger utiliza la compresión de bloques con la variable [snply](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) biblioteca de compresión para todas las colecciones y [compresión de prefijo](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression) para todos los índices.

Para colecciones, compresión de bloques con [zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) también está disponible. Para especificar un algoritmo de compresión alternativo o sin compresión, utilice la variable [storage.wiredTiger.collectionConfig.blockCompressor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) configuración.

Para índices, para desactivar [compresión de prefijo](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression), use el [storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression) configuración.

La configuración de compresión también se puede configurar por colección y por índice durante la recopilación y la creación del índice. Consulte [Especificar las opciones del motor de almacenamiento](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options) y [db.collection.createIndex() storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options) .

Para la mayoría de las cargas de trabajo, la configuración de compresión predeterminada equilibra la eficiencia del almacenamiento y los requisitos de procesamiento.

El diario WiredTiger también está comprimido de forma predeterminada. Para obtener información sobre la compresión de asientos, consulte [Historial](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### Uso de memoria {#memory-use}

Con WiredTiger, MongoDB utiliza tanto la caché interna de WiredTiger como la caché del sistema de archivos.

A partir de la versión 3.4, la caché interna de WiredTiger utilizará, de forma predeterminada, la mayor de las siguientes opciones:

* 50% de RAM menos 1 GB, o
* 256 MB

De forma predeterminada, WiredTiger utiliza la compresión de bloques Snapse para todas las colecciones y la compresión de prefijos para todos los índices. Los valores predeterminados de compresión se pueden configurar a nivel global y también se pueden configurar por colección y por índice durante la recopilación y la creación del índice.

Se utilizan representaciones diferentes para los datos en la caché interna de WiredTiger en comparación con el formato en disco:

* Los datos de la caché del sistema de archivos son los mismos que el formato en disco, incluyendo los beneficios de cualquier compresión para archivos de datos. El sistema operativo utiliza la caché del sistema de archivos para reducir la E/S del disco.

Los índices cargados en la caché interna de WiredTiger tienen una representación de datos diferente al formato en disco, pero aún pueden aprovechar la compresión de prefijos índice para reducir el uso de RAM.

La compresión de prefijos de índice anula la duplicación de prefijos comunes de campos indexados.

Los datos de recopilación en la caché interna de WiredTiger no están comprimidos y utilizan una representación diferente del formato en disco. La compresión de bloques puede proporcionar ahorros significativos en el almacenamiento en disco, pero el servidor debe descomprimir los datos para manipularlos.

A través de la caché del sistema de archivos, MongoDB utiliza automáticamente toda la memoria libre que no sea utilizada por la caché de WiredTiger o por otros procesos.

Para ajustar el tamaño de la caché interna de WiredTiger, consulte [storage.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) y [—wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb). Evite aumentar el tamaño de la caché interna de WiredTiger por encima de su valor predeterminado.

### NUMA {#numa}

El acceso a memoria no uniforme (NUMA) permite que un núcleo gestione cómo se asigna la memoria a los núcleos del procesador. Aunque esto intenta hacer que el acceso a la memoria sea más rápido para los núcleos, lo que garantiza que puedan acceder a los datos necesarios, la NUMA interfiere con el MAP al introducir latencia adicional, ya que no se puede predecir la lectura. Debido a esto, es necesario deshabilitar la NUMA para el `mongod` en todos los sistemas operativos que tengan la capacidad.

En esencia, en una arquitectura NUMA, la memoria está conectada a CPUs y las CPUs están conectadas a un bus. En una arquitectura SMP o UMA, la memoria está conectada al bus y compartida por CPUs. Cuando un subproceso asigna memoria en una CPU NUMA, la asigna según una directiva. El valor predeterminado es asignar la memoria conectada a la CPU local del subproceso a menos que no haya disponible, en cuyo momento utiliza la memoria de una CPU gratuita a un costo mayor. Una vez asignada, la memoria no se mueve entre CPUs. La asignación se realiza mediante una directiva heredada del subproceso principal, que en última instancia es el subproceso que inició el proceso.

En muchas bases de datos que ven la máquina como una arquitectura de memoria uniforme de varios núcleos, esto lleva a que la CPU inicial se llene primero y la CPU secundaria se llene más tarde, especialmente si un subproceso central es responsable de asignar búferes de memoria. La solución es cambiar la política de NUMA del hilo principal utilizado para iniciar el `mongod` proceso.

Esto se puede hacer ejecutando el siguiente comando:

```shell
numactl --interleaved=all <mongod> -f config
```

Esta directiva asigna memoria de forma rotona en todos los nodos de CPU, lo que garantiza una distribución uniforme en todos los nodos. No genera el acceso de mayor rendimiento a la memoria, como en sistemas con múltiples hardware de CPU. Aproximadamente la mitad de las operaciones de memoria serán más lentas y estarán por encima del bus, pero `mongod` no ha sido escrito para dirigirse a la NUMA de una manera óptima, por lo que es un compromiso razonable.

### Problemas de NUMA {#numa-issues}

Si la variable `mongod` el proceso se inicia desde una ubicación distinta a la `/etc/init.d` , es probable que no se inicie con la directiva NUMA correcta. Dependiendo de la directiva predeterminada, pueden surgir problemas. Esto se debe a que los diversos instaladores del gestor de paquetes Linux para MongoDB también instalan un servicio con archivos de configuración ubicados en `/etc/init.d` que realizan el paso descrito anteriormente. Si instala y ejecuta MongoDB directamente desde un archivo ( `.tar.gz`), entonces tendrá que ejecutar manualmente mongod en el `numactl` proceso.

>[!NOTE]
>
>Para obtener más información sobre las políticas NUMA disponibles, consulte la [documentación de numactl](https://linux.die.net/man/8/numactl).

El proceso MongoDB se comportará de forma diferente en diferentes políticas de asignación:

```

```

* `-membind=<nodes>`
Asigne solo en los nodos enumerados. El mongol no asignará memoria en los nodos enumerados y es posible que no utilice toda la memoria disponible.

* `-cpunodebind=<nodes>`
Solo se ejecutan en los nodos. El mongodo solo se ejecutará en los nodos especificados y usará solamente la memoria disponible en esos nodos.

* `-physcpubind=<nodes>`
Solo se ejecutan en las CPU (núcleos) enumeradas. El mongol solo se ejecutará en las CPU enumeradas y usará solamente la memoria disponible en esas CPU.

* `--localalloc`
Asigne siempre memoria en el nodo actual, pero utilice todos los nodos en los que se ejecuta el subproceso. Si un subproceso realiza la asignación, solo se utilizará la memoria disponible para esa CPU.

* `--preferred=<node>`
Prefiere la asignación a un nodo, pero regresa a otros si el nodo preferido está lleno. Se puede utilizar la notación relativa para definir un nodo. Además, los subprocesos se ejecutan en todos los nodos.

Algunas de las políticas pueden dar como resultado que menos de toda la RAM disponible se asigne al `mongod` proceso. A diferencia de MySQL, MongoDB evita activamente la paginación a nivel del sistema operativo y, en consecuencia, el `mongod` puede obtener menos memoria que parece disponible.

#### Intercambio {#swapping}

Debido a la naturaleza intensiva en la memoria de las bases de datos, el intercambio a nivel de sistema operativo debe deshabilitarse. El proceso MongoDB evitará el intercambio por diseño.

#### Sistemas de archivos remotos {#remote-filesystems}

Los sistemas de archivos remotos como NFS no son recomendables para los archivos de datos internos de MongoDB (los archivos de base de datos del proceso mondial) , ya que introducen demasiada latencia. Esto no debe confundirse con el sistema de archivos compartidos necesario para el almacenamiento de Oak Blob (FileDataStore), donde NFS es recomendado.

#### Leer adelante {#read-ahead}

Leer con anticipación debe ser ajustado para que cuando una página se pagine usando una lectura aleatoria, los bloques innecesarios no se lean desde el disco, lo que resulta en un consumo innecesario de ancho de banda de E/S.

### Requisitos de Linux {#linux-requirements}

#### Versiones mínimas del núcleo {#minimum-kernel-versions}

* **2,6,23** para `ext4` filesystems

* **2,6,25** para `xfs` filesystems

#### Configuración recomendada para los discos de base de datos {#recommended-settings-for-database-disks}

**Apagar tiempo**

Se recomienda que `atime` está desactivado para los discos que contendrán las bases de datos.

**Establezca el programador de discos NOOP**

Para ello:

En primer lugar, compruebe el planificador de E/S que está configurado actualmente. Esto se puede hacer ejecutando el siguiente comando:

```shell
cat /sys/block/sdg/queue/scheduler
```

Si la respuesta es `noop` no hay nada que hacer más.

Si NOOP no es el programador de E/S configurado, puede cambiarlo ejecutando:

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**Ajuste el valor de lectura anticipada**

Se recomienda utilizar un valor de 32 para los discos desde los que se ejecutan las bases de datos MongoDB. Esto equivale a 16 kilobytes. Puede configurarlo ejecutando:

```shell
sudo blockdev --setra <value> <device>
```

#### Habilitar NTP {#enable-ntp}

Asegúrese de tener NTP instalado y en ejecución en el equipo que hospeda las bases de datos MongoDB. Por ejemplo, puede instalarlo utilizando el administrador de paquetes yum en un equipo CentOS:

```shell
sudo yum install ntp
```

Una vez que el daemon NTP se haya instalado y se haya iniciado correctamente, puede comprobar el archivo de deriva para ver la compensación horaria de su servidor.

#### Deshabilitar páginas grandes transparentes {#disable-transparent-huge-pages}

Red Hat Linux utiliza un algoritmo de administración de memoria llamado Transparent Huge Pages (THP). Se recomienda deshabilitarlo si utiliza el sistema operativo para cargas de trabajo de base de datos.

Puede desactivarlo siguiendo el procedimiento siguiente:

1. Abra el `/etc/grub.conf` en el editor de texto de su elección.
1. Añada la siguiente línea al archivo grub.conf:

   ```xml
   transparent_hugepage=never
   ```

1. Finalmente, compruebe si la configuración se ha aplicado ejecutando:

   ```shell
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   Si THP está deshabilitado, el resultado del comando anterior debería ser:

   ```xml
   always madvise [never]
   ```

>[!NOTE]
>
>Para obtener más información sobre las páginas grandes transparentes, consulte esta [article](https://access.redhat.com/solutions/46111).

#### Deshabilitar NUMA {#disable-numa}

En la mayoría de las instalaciones en las que NUMA está habilitado, el demonio MongoDB lo desactivará automáticamente si se ejecuta como un servicio desde el `/etc/init.d` carpeta.

En los casos en que no sea así, puede desactivar NUMA por proceso. Para desactivarlo, ejecute estos comandos:

```shell
numactl --interleave=all <path_to_process>
```

Donde `<path_to_process>` es el camino al proceso mondios.

A continuación, desactive la recuperación de zona ejecutando:

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### Ajuste de la configuración de límite para el proceso mondios {#tweak-the-ulimit-settings-for-the-mongod-process}

Linux permite un control configurable sobre la asignación de recursos a través del `ulimit` comando. Esto se puede hacer por usuario o por proceso.

Se recomienda configurar ulimit para el proceso mondios según la variable [Configuración de límites recomendados de MongoDB](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings).

#### Probar el rendimiento de E/S de MongoDB {#test-mongodb-i-o-performance}

MongoDB proporciona una herramienta llamada `mongoperf` que está diseñado para probar el rendimiento de E/S. Se recomienda usarlo para probar el rendimiento de todas las instancias de MongoDB que conforman su infraestructura.

Para obtener información sobre cómo usar `mongoperf`, consulte la [Documentación de MongoDB](https://docs.mongodb.org/manual/reference/program/mongoperf/).

>[!NOTE]
>
>Tenga en cuenta que `mongoperf` está diseñado para ser un indicador del rendimiento de MongoDB en la plataforma en la que se ejecuta. Por ello, los resultados no deben considerarse definitivos para el funcionamiento de un sistema de producción.
>
>Para obtener resultados de rendimiento más precisos, puede ejecutar pruebas complementarias con la variable `fio` Herramienta Linux.

**Probar el rendimiento de lectura en las máquinas virtuales que conforman la implementación**

Después de instalar la herramienta, cambie al directorio de la base de datos MongoDB para ejecutar las pruebas. A continuación, inicie la primera prueba ejecutando `mongoperf`con esta configuración:

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

La salida deseada debe alcanzar hasta dos gigabytes por segundo (2GB/s) y 500.000 IOPS que se ejecutan en 32 subprocesos para todas las instancias de MongoDB.

Ejecute una segunda prueba, esta vez con archivos asignados a memoria, configurando la variable `mmf:true` parámetro:

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

La salida de la segunda prueba debe ser considerablemente mayor que la primera, lo que indica el rendimiento de la transferencia de memoria.

>[!NOTE]
>
>Al realizar las pruebas, compruebe las estadísticas de uso de E/S de las máquinas virtuales en cuestión en su sistema de supervisión del sistema operativo. Si indican valores inferiores al 100 por ciento para lecturas de E/S, puede haber un problema con su máquina virtual.

**Probar el rendimiento de escritura de la instancia principal de MongoDB**

A continuación, compruebe el rendimiento de escritura de E/S de la instancia principal de MongoDB ejecutando `mongoperf` del directorio de la base de datos MongoDB con la misma configuración:

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

El resultado deseado debería ser de 12 megabytes por segundo y alcanzar alrededor de 3000 IOPS, con poca variación entre el número de subprocesos.

## Pasos para entornos virtualizados {#steps-for-virtualised-environments}

### VMWare {#vmware}

Si está utilizando WMWare ESX para administrar e implementar sus entornos virtualizados, asegúrese de realizar las siguientes configuraciones desde la consola ESX para dar cabida a la operación MongoDB:

1. Desactivación de la reproducción de memoria
1. Preasignar y reservar memoria para las máquinas virtuales que alojarán las bases de datos MongoDB
1. Utilice el Control de E/S de almacenamiento para asignar suficientes I/O a la `mongod` proceso.
1. Garantizar recursos de CPU de las máquinas que alojan MongoDB configurando [Reserva de CPU](https://pubs.vmware.com/vsphere-4-esx-vcenter/index.jsp?topic=/com.vmware.vsphere.vmadmin.doc_41/vsp_vm_guide/configuring_virtual_machines/t_allocate_cpu_resources.html)

1. Considere la posibilidad de utilizar controladores de E/S ParaVirtual. Para obtener más información sobre cómo hacerlo, consulte esta [artículo de la base de conocimiento](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1010398).

### Amazon Web Service {#amazon-web-services}

Para obtener documentación sobre cómo configurar MongoDB con Amazon Web Service, consulte la [Configuración de la integración de AWS](https://docs.cloud.mongodb.com/tutorial/configure-aws-settings/) artículo en el sitio web de MongoDB.

## Protección de MongoDB antes de la implementación {#securing-mongodb-before-deployment}

Ver este post en [implementación segura de MongoDB](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html) para obtener consejos sobre cómo proteger la configuración de sus bases de datos antes de la implementación.

## Dispatcher {#dispatcher}

### Elección del sistema operativo para Dispatcher {#choosing-the-operating-system-for-the-dispatcher}

Para poder servir correctamente la implementación de MongoDB, el sistema operativo que alojará a Dispatcher debe estar en ejecución **Apache httpd** **versión 2.4 o superior.**

Además, asegúrese de que todas las bibliotecas utilizadas en la compilación estén actualizadas para minimizar las implicaciones de seguridad.

### Configuración de Dispatcher {#dispatcher-configuration}

Una configuración típica de Dispatcher servirá entre diez y veinte veces más el rendimiento de las solicitudes de una única instancia de AEM.

Dado que Dispatcher es principalmente apátrida, puede escalar horizontalmente con facilidad. En algunas implementaciones, es necesario restringir el acceso de los autores a ciertos recursos. Debido a esto, es muy recomendable que utilice un Dispatcher con las instancias de autor.

La ejecución de AEM sin Dispatcher requerirá que otra aplicación realice la terminación de SSL y el equilibrio de carga. Esto es necesario porque las sesiones deben tener afinidad con la instancia de AEM en la que crearon, un concepto conocido como conexiones duraderas. El propósito de esto es garantizar que las actualizaciones del contenido muestren una latencia mínima.

Marque la [Documentación de Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) para obtener más información sobre cómo configurarlo.

### Configuración adicional {#additional-configuration}

#### Conexiones fijas {#sticky-connections}

Las conexiones duraderas garantizan que las páginas personalizadas y los datos de sesión de un usuario están compuestos en la misma instancia de AEM. Estos datos se almacenan en la instancia, por lo que las solicitudes posteriores del mismo usuario devolverán a la misma instancia.

Se recomienda habilitar las conexiones duraderas para todas las capas internas que dirijan solicitudes a las instancias de AEM, lo que anima a las solicitudes posteriores a llegar a la misma instancia de AEM. Esto ayudará a minimizar la latencia que, de lo contrario, es visible cuando el contenido se actualiza entre instancias.

#### Caduca larga {#long-expires}

De forma predeterminada, el contenido enviado desde un Dispatcher AEM tiene encabezados Last-Modified y Etag , sin indicar la caducidad del contenido. Aunque esto garantiza que la interfaz de usuario siempre obtenga la versión más reciente del recurso, también significa que el explorador realizará una operación de GET para comprobar si el recurso ha cambiado. Esto puede dar como resultado varias solicitudes a las que la respuesta HTTP es 304 (sin modificar), según la carga de la página. Para los recursos que se sabe que no caducan, si se configura un encabezado Expires y se eliminan los encabezados Last-Modified y ETag , el contenido se almacenará en caché y no se realizarán solicitudes de actualización adicionales hasta que se cumpla la fecha en el encabezado Expires .

Sin embargo, el uso de este método significa que no hay una manera razonable de hacer que el recurso caduque en el explorador antes de que caduque el encabezado Caduca. Para mitigar esto, se puede configurar HtmlClientLibraryManager para que utilice direcciones URL inmutables para las bibliotecas de cliente.

Se garantiza que estas direcciones URL no cambien. Cuando cambie el cuerpo del recurso contenido en la dirección URL, los cambios se reflejarán automáticamente en la dirección URL, lo que garantiza que el explorador solicitará la versión correcta del recurso.

La configuración predeterminada agrega un selector a HtmlClientLibraryManager. Al ser un selector, el recurso se almacena en caché en Dispatcher con el selector intacto. Este selector también se puede utilizar para garantizar el comportamiento de caducidad correcto. El selector predeterminado sigue el `lc-.*?-lc` patrón. Las siguientes directivas de configuración httpd de Apache asegurarán que todas las solicitudes que coincidan con ese patrón se proporcionen con una hora de caducidad adecuada.

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### Sin Franqueo {#no-sniff}

Cuando el contenido se envía sin tipo de contenido, muchos navegadores intentarán adivinar el tipo de contenido leyendo los primeros bytes del contenido. Esto se llama &quot;esnifado&quot;. El filtrado abre una vulnerabilidad de seguridad, ya que los usuarios que pueden escribir en el repositorio pueden cargar contenido malicioso sin tipo de contenido.

Por este motivo, es aconsejable agregar un `no-sniff` Encabezado a los recursos servidos por Dispatcher. Sin embargo, Dispatcher no almacena en caché los encabezados. Esto significa que cualquier contenido servido desde el sistema de archivos local tendrá su tipo de contenido determinado por su extensión, en lugar de usar el encabezado de tipo de contenido original desde su servidor de origen AEM.

No se puede habilitar ningún sniff de forma segura si se sabe que la aplicación web nunca proporciona recursos en caché sin un tipo de archivo.

Puede activar Sin recorte de forma inclusiva:

```xml
Header set X-Content-Type-Options "nosniff"
```

También se puede activar de forma selectiva:

```xml
RewriteCond %{REQUEST_URI} \.(?:js|jsonp)$ [OR]
RewriteCond %{QUERY_STRING} (callback|jsonp|cb)=\w+
RewriteRule .* - [E=jsonp_request:1]
Header set X-Content-Type-Options "nosniff"  env=jsonp_request
Header setifempty Content-Type application/javascript env=jsonp_request
```

#### Política de seguridad de contenido {#content-security-policy}

La configuración predeterminada de Dispatcher permite abrir una Política de seguridad de contenido, también conocida como CSP. Esto permite que una página cargue recursos de todos los dominios sujetos a las políticas predeterminadas del entorno limitado del explorador.

Es deseable restringir desde dónde se pueden cargar los recursos para evitar cargar código en el motor de javascript desde servidores externos que no sean de confianza o que no estén verificados.

La CSP permite ajustar las políticas de forma más precisa. Sin embargo, en una aplicación compleja, los encabezados CSP deben desarrollarse con cuidado, ya que las políticas demasiado restrictivas pueden romper partes de la interfaz de usuario.

>[!NOTE]
>
>Para obtener más información sobre cómo funciona esto, consulte la [Página OWASP en la directiva de seguridad de contenido](https://www.owasp.org/index.php/Content_Security_Policy).

### Tamaño {#sizing}

Para obtener más información sobre el tamaño, consulte la [Pautas para el tamaño del hardware](/help/managing/hardware-sizing-guidelines.md).

### Optimización del rendimiento de MongoDB {#mongodb-performance-optimization}

Para obtener información genérica sobre el rendimiento de MongoDB, consulte [Análisis del rendimiento de MongoDB](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/).

## Limitaciones conocidas {#known-limitations}

### Instalaciones concurrentes {#concurrent-installations}

Aunque MongoMK admite el uso simultáneo de varias instancias de AEM con una sola base de datos, no lo son las instalaciones simultáneas.

Para solucionar este problema, asegúrese de ejecutar primero la instalación con un solo miembro y añada los demás después de que el primero haya finalizado la instalación.

### Longitud del nombre de página {#page-name-length}

Si AEM se está ejecutando en una implementación del administrador de persistencia de MongoMK, [los nombres de página están limitados a 150 caracteres.](/help/sites-authoring/managing-pages.md)

>[!NOTE]
>
>[Consulte la documentación de MongoDB](https://docs.mongodb.com/manual/reference/limits/) para familiarizarse con las limitaciones y umbrales conocidos de MongoDB.
