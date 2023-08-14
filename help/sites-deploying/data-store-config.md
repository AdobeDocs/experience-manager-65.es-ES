---
title: AEM Configuración de almacenes de nodos y almacenes de datos en el 6
description: Obtenga información sobre cómo configurar almacenes de nodos y almacenes de datos, y cómo realizar la recopilación de elementos no utilizados del almacén de datos.
content-type: reference
topic-tags: deploying
docset: aem65
feature: Configuring
exl-id: c1c90d6a-ee5a-487d-9a8a-741b407c8c06
source-git-commit: 2ed19ac8c60dbf49422b8f1f665be4004689e00e
workflow-type: tm+mt
source-wordcount: '3550'
ht-degree: 2%

---

# AEM Configuración de almacenes de nodos y almacenes de datos en el 6{#configuring-node-stores-and-data-stores-in-aem}

## Introducción {#introduction}

En Adobe Experience Manager AEM (), los datos binarios se pueden almacenar de forma independiente de los nodos de contenido. Los datos binarios se almacenan en un almacén de datos, mientras que los nodos de contenido se almacenan en un almacén de nodos.

Tanto los almacenes de datos como los almacenes de nodos se pueden configurar mediante la configuración OSGi. Se hace referencia a cada configuración de OSGi mediante un identificador persistente (PID).

## Pasos de configuración {#configuration-steps}

Para configurar el almacén de nodos y el almacén de datos, realice estos pasos:

1. AEM Copie el archivo JAR de inicio rápido de la en su directorio de instalación.
1. Crear una carpeta `crx-quickstart/install` en el directorio de instalación.
1. Primero, configure el almacén de nodos creando un archivo de configuración con el nombre de la opción de almacén de nodos que desee utilizar en `crx-quickstart/install` directorio.

   AEM Por ejemplo, el almacén de nodos de documentos (que es la base de la implementación de MongoMK de la) utiliza el archivo `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`.

1. Edite el archivo y defina las opciones de configuración.
1. Cree un archivo de configuración con el PID del almacén de datos que desee utilizar. Edite el archivo para establecer las opciones de configuración.

   >[!NOTE]
   >
   >Consulte [Configuraciones del almacén de nodos](#node-store-configurations) y [Configuraciones del almacén de datos](#data-store-configurations) para ver las opciones de configuración.

1. AEM Inicio de.

## Configuraciones del almacén de nodos {#node-store-configurations}

>[!CAUTION]
>
>Las versiones más recientes de Oak emplean un nuevo esquema de nomenclatura y formato para los archivos de configuración OSGi. El nuevo esquema de nombres requiere que se asigne un nombre al archivo de configuración **.config** y el nuevo formato requiere que se escriban valores y es [documentado aquí](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format).
>
>Si actualiza desde una versión anterior de Oak, asegúrese de realizar una copia de seguridad del `crx-quickstart/install`carpeta primero. Después de la actualización, restaure el contenido de la carpeta a la instalación actualizada y modifique la extensión de los archivos de configuración desde **.cfg** hasta **.config**.
>
>Si está leyendo este artículo como preparación para una actualización de un **AEM.x** instalación, asegúrese de consultar la [actualización](https://experienceleague.adobe.com/docs/) primero, la documentación.

### Almacén de nodos de segmentos {#segment-node-store}

El almacén de nodos de segmentos es la base de la implementación de TarMK de Adobe AEM en la versión 6 de. Utiliza el `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` PID para la configuración.

>[!CAUTION]
>
>El PID del almacén de nodos de segmentos ha cambiado de `org.apache.jackrabbit.oak.plugins.segment.SegmentNodeStoreService in previous versions` AEM de a `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` AEM en el punto 6.3. Asegúrese de realizar los ajustes de configuración necesarios para reflejar este cambio.

Puede configurar las siguientes opciones:

* `repository.home`: ruta al inicio del repositorio en el que se almacenan los datos relacionados con el repositorio. De forma predeterminada, los archivos de segmentos de se almacenan en `crx-quickstart/segmentstore` directorio.

* `tarmk.size`: Tamaño máximo de un segmento en MB. El máximo predeterminado es 256 MB.
* `customBlobStore`: Valor booleano que indica que se utiliza un almacén de datos personalizado. AEM El valor predeterminado es True para la versión 6.3 y versiones posteriores de la versión de. AEM Antes de la versión 6.3, el valor predeterminado era false.

El siguiente es un ejemplo `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` archivo:

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### Almacén de nodos de documentos {#document-node-store}

AEM El almacén de nodos de documentos es la base de la implementación de MongoMK de la aplicación de la. Utiliza el `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService`* *PID. Estas son las opciones de configuración disponibles:

* `mongouri`: La [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) necesario para conectarse a la base de datos de Mongo. El valor predeterminado es `mongodb://localhost:27017`

* `db`: Nombre de la base de datos Mongo. El valor predeterminado es **Oak** ``. However, new AEM 6 installations use **aem-author** ``como nombre predeterminado de la base de datos.

* `cache`: el tamaño de la caché en MB. Se distribuye entre varias memorias caché utilizadas en DocumentNodeStore. El valor predeterminado es `256`

* `changesSize`: Tamaño en MB de la colección limitada utilizada en Mongo para almacenar en caché la salida de diferencia. El valor predeterminado es `256`

* `customBlobStore`: Valor booleano que indica que se utilizará un almacén de datos personalizado. El valor predeterminado es `false`.

El siguiente es un ejemplo `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config` archivo:

```shell
#Mongo server details
mongouri="mongodb://localhost:27017"

#Name of Mongo database to use
db="aem-author"

#Store binaries in custom BlobStore
customBlobStore=B"false"
```

## Configuraciones del almacén de datos {#data-store-configurations}

Cuando se trata de un gran número de binarios, se recomienda utilizar un almacén de datos externo en lugar de los almacenes de nodos predeterminados para maximizar el rendimiento.

Por ejemplo, si el proyecto requiere muchos recursos multimedia, almacenarlos en el almacén de datos de archivos o S3 hace que el acceso a ellos sea más rápido que almacenarlos directamente en un MongoDB.

El almacén de datos de archivos proporciona un mejor rendimiento que MongoDB, y las operaciones de copia de seguridad y restauración de Mongo también son más lentas con un gran número de recursos.

A continuación se describen los detalles de los diferentes almacenes de datos y configuraciones.

>[!NOTE]
>
>Para habilitar los almacenes de datos personalizados, debe asegurarse de que `customBlobStore` se establece en `true` en el archivo de configuración del almacén de nodos correspondiente ([almacén de nodos de segmentos](/help/sites-deploying/data-store-config.md#segment-node-store) o [almacén de nodos de documentos](/help/sites-deploying/data-store-config.md#document-node-store)).

### Almacén de datos de archivo {#file-data-store}

Esta es la implementación de [FileDataStore](https://jackrabbit.apache.org/api/trunk/org/apache/jackrabbit/core/data/FileDataStore.html) presente en Jackrabbit 2. Proporciona una forma de almacenar los datos binarios como archivos normales en el sistema de archivos. Utiliza el `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore` PID.

Estas opciones de configuración están disponibles:

* `repository.home`: ruta al inicio del repositorio en el que se almacenan varios datos relacionados con el repositorio. De forma predeterminada, los archivos binarios se almacenarían en `crx-quickstart/repository/datastore` directorio

* `path`: Ruta al directorio en el que se almacenarán los archivos. Si se especifica, tiene prioridad sobre `repository.home` valor

* `minRecordLength`: El tamaño mínimo en bytes de un archivo almacenado en el almacén de datos. El contenido binario inferior a este valor estaría en la línea.

>[!NOTE]
>
>Cuando utilice un NAS para almacenar almacenes de datos de archivos compartidos, asegúrese de utilizar solo dispositivos de alto rendimiento para evitar problemas de rendimiento.

## Almacén de datos de Amazon S3 {#amazon-s-data-store}

AEM Se puede configurar el almacenamiento de datos en el servicio de almacenamiento simple (S3) de Amazon. Utiliza el `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` PID para la configuración.

>[!NOTE]
>
>AEM 6.5 admite el almacenamiento de datos en la versión S3 de Amazon; sin embargo, la compatibilidad no se amplía al almacenamiento de datos en otras plataformas, cuyos proveedores pueden tener sus propias implementaciones de las API S3 de Amazon.

Para habilitar la funcionalidad del almacén de datos S3, se debe descargar e instalar un paquete de funciones que contenga el conector del almacén de datos S3. Vaya a la [Repositorio de Adobe](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/) y descargue la versión más reciente de las versiones 1.10.x del paquete de funciones (por ejemplo, com.adobe.granite.oak.s3connector-1.10.0.zip). AEM Además, debe descargar e instalar el paquete de servicio más reciente, tal y como se indica en la lista de [AEM Notas de la versión de 6.5](/help/release-notes/release-notes.md) página.

>[!NOTE]
>
>AEM Al utilizar la con TarMK, los binarios se almacenan de forma predeterminada en `FileDataStore`. AEM Para usar TarMK con el almacén de datos S3, debe empezar a usar el almacén de datos de la versión de la aplicación de la versión de la aplicación de datos de `crx3tar-nofds` modo de ejecución, por ejemplo:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

Una vez descargado, puede instalar y configurar el conector S3 de la siguiente manera:

1. Extraiga el contenido del archivo zip del paquete de funciones en una carpeta temporal.

1. Vaya a la carpeta temporal y navegue hasta la siguiente ubicación:

   ```xml
   jcr_root/libs/system/install
   ```

   Copie todo el contenido de la ubicación anterior en `<aem-install>/crx-quickstart/install.`

1. AEM Si ya está configurado para trabajar con el almacenamiento Tar o MongoDB, elimine los archivos de configuración existentes del ***&lt;aem-install>***/*crx-quickstart*/*instalar* antes de continuar. Los archivos que deben eliminarse son los siguientes:

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Vuelva a la ubicación temporal en la que se ha extraído el paquete de funciones y copie el contenido de la siguiente carpeta:

   * `jcr_root/libs/system/config`

   hasta

   * `<aem-install>/crx-quickstart/install`

   Asegúrese de copiar únicamente los archivos de configuración necesarios para la configuración actual. Tanto para un almacén de datos dedicado como para una configuración de almacén de datos compartido, copie el `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` archivo.

   >[!NOTE]
   >
   >En una configuración de clúster, realice los pasos anteriores en todos los nodos del clúster uno a uno. Además, asegúrese de utilizar la misma configuración de S3 para todos los nodos.

1. Edite el archivo y añada las opciones de configuración que requiera el programa de instalación.
1. AEM Inicio de.

## Actualización a una nueva versión del conector S3 1.10.x {#upgrading-to-a-new-version-of-the-s-connector}

Para actualizar a una nueva versión del conector 1.10.x S3 (por ejemplo, de 1.10.0 a 1.10.4), siga estos pasos:

1. Detenga la instancia de AEM.

1. Vaya a `<aem-install>/crx-quickstart/install/15` AEM en la carpeta de instalación de la y realice una copia de seguridad de su contenido.
1. Después de la copia de seguridad, elimine la versión antigua del conector S3 y sus dependencias eliminando todos los archivos jar de la `<aem-install>/crx-quickstart/install/15` carpeta, por ejemplo:

   * **oak-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**

   >[!NOTE]
   >
   >Los nombres de archivo presentados anteriormente se utilizan únicamente con fines ilustrativos.

1. Descargue la última versión del paquete de funciones 1.10.x desde el [Repositorio de Adobe](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/).
1. Descomprima el contenido en una carpeta independiente y, a continuación, vaya a `jcr_root/libs/system/install/15`.
1. Copie los archivos jar en **&lt;aem-install>** AEM /crx-quickstart/install/15 en la carpeta de instalación de la.
1. AEM Inicie y compruebe la funcionalidad del conector.

Puede utilizar el archivo de configuración con las opciones detalladas a continuación.

<!--
* accessKey: The AWS access key.
* secretKey: The AWS secret access key. **Note:** When the `accessKey` or `secretKey` is not specified then the [IAM role](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) is used for authentication.
* s3Bucket: The bucket name.
* s3Region: The bucket region.
* path: The path of the data store. The default is **&lt;AEM install folder&gt;/repository/datastore**
* minRecordLength: The minimum size of an object that should be stored in the data store. The minimum/default is **16KB.**
* maxCachedBinarySize: Binaries with size less than or equal to this size will be stored in memory cache. The size is in bytes. The default is **17408 **(17 KB).
* cacheSize: The size of the cache. The value is specified in bytes. The default is **64GB**.
* secret: Only to be used if using binaryless replication for shared datastore setup.
* stagingSplitPercentage: The percentage of cache size configured to be used for staging asynchronous uploads. The default value is **10**.
* uploadThreads: The number of uploads threads that are used for asynchronous uploads. The default value is **10**.
* stagingPurgeInterval: The interval in seconds for purging finished uploads from the staging cache. The default value is **300** seconds (5 minutes).
* stagingRetryInterval: The retry interval in seconds for failed uploads. The default value is **600** seconds (10 minutes).
-->

### Opciones del archivo de configuración del conector S3 {#s3-connector-configuration-file-options}

>[!NOTE]
>
>El conector S3 admite la autenticación de usuario IAM y la autenticación de función IAM. Para utilizar la autenticación de función IAM, omita la `accessKey` y `secretKey` valores del archivo de configuración. El conector S3 toma como valor predeterminado la variable [Función IAM](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) asignado a la instancia de.

| Clave | Descripción | Predeterminado | Requerido |
| --- | --- | --- | --- |
| accessKey | ID de clave de acceso para el usuario de IAM con acceso al bloque. | | Sí, cuando no se usan los roles de IAM. |
| secretKey | Clave de acceso secreta del usuario de IAM con acceso al bloque. | | Sí, cuando no se usan los roles de IAM. |
| cacheSize | El tamaño (en bytes) de la caché local. | 64GB | No. |
| connectionTimeout | Establezca la cantidad de tiempo de espera (en milisegundos) antes de que se agote el tiempo de espera al establecer inicialmente una conexión. | 10 000 | No. |
| maxCachedBinarySize | Los binarios con un tamaño inferior o igual a este valor (en bytes) se almacenan en la memoria caché. | 17408 (17 KB) | No. |
| maxConnections | Establezca el número máximo de conexiones HTTP abiertas permitidas. | 50 | No. |
| maxErrorRetry | Establezca el número máximo de intentos de reintento para solicitudes fallidas (recuperables). | 3 | No. |
| minRecordLength | El tamaño mínimo de un objeto (en bytes) que debe almacenarse en el almacén de datos. | 16384 | No. |
| path | AEM Ruta de acceso local del almacén de datos de. | `crx-quickstart/repository/datastore` | No. |
| proxyHost | Establezca el host proxy opcional mediante el que se conecta el cliente. | | No. |
| proxyPort | Configure el puerto proxy opcional mediante el que se conecta el cliente. | | No. |
| s3Bucket | Nombre del contenedor de S3. | | Sí |
| s3EndPoint | Extremo de API de REST S3. | | No. |
| s3Region | Región donde reside el bloque. Ver esto [página](https://docs.aws.amazon.com/general/latest/gr/s3.html) para obtener más información. | Región donde se está ejecutando la instancia de AWS. | No. |
| socketTimeout | Establezca la cantidad de tiempo de espera (en milisegundos) para que los datos se transfieran a través de una conexión abierta establecida antes de que se agote el tiempo de espera de la conexión y se cierre. | 50000 | No. |
| stagingPurgeInterval | El intervalo (en segundos) para purgar las cargas finalizadas de la caché de ensayo. | 300 | No. |
| stagingRetryInterval | Intervalo (en segundos) para reintentar cargas fallidas. | 600 | No. |
| stagingSplitPercentage | El porcentaje de `cacheSize` para su uso para el ensayo de cargas asíncronas. | 10 | No. |
| uploadThreads | El número de subprocesos de carga utilizados para las cargas asincrónicas. | 10 | No. |
| writeThreads | El número de subprocesos simultáneos utilizados para escribir a través de S3 Transfer Manager. | 10 | No. |

<!---
### Bucket region options {#bucket-region-options}

<table>
 <tbody>
  <tr>
   <td>US Standard</td>
   <td><code>us-standard</code></td>
  </tr>
  <tr>
   <td>US West</td>
   <td><code>us-west-2</code></td>
  </tr>
  <tr>
   <td>US West (Northern California)</td>
   <td><code>us-west-1</code></td>
  </tr>
  <tr>
   <td>EU (Ireland)<br /> </td>
   <td><code>EU</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Singapore)<br /> </td>
   <td><code>ap-southeast-1</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Sydney)<br /> </td>
   <td><code>ap-southeast-2</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Tokyo)</td>
   <td><code>ap-northeast-1</code></td>
  </tr>
  <tr>
   <td>South America (Sao Paolo)<br /> </td>
   <td><code>sa-east-1</code></td>
  </tr>
 </tbody>
</table>
-->

### Almacenamiento en caché de DataStore {#data-store-caching}

>[!NOTE]
>
>Implementaciones de DataStore de `S3DataStore`, `CachingFileDataStore` y `AzureDataStore` admite el almacenamiento en caché del sistema de archivos local. El `CachingFileDataStore` La implementación es útil cuando DataStore está en NFS (Network File System).

Al actualizar desde una implementación de caché anterior (anterior a Oak 1.6) hay una diferencia en la estructura del directorio de caché del sistema de archivos local. En la estructura de caché antigua, tanto los archivos descargados como los cargados se colocaban directamente debajo de la ruta de caché. La nueva estructura separa las descargas y cargas y las almacena en dos directorios llamados `upload` y `download` en ruta de caché. El proceso de actualización debe ser fluido, y cualquier carga pendiente debe programarse para su carga, y cualquier archivo descargado anteriormente en la caché se coloca en la caché en la inicialización.

También puede actualizar la caché sin conexión utilizando la variable `datastorecacheupgrade` comando de oak-run. Para obtener más información sobre cómo ejecutar el comando, consulte la [readme](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md) para el módulo oak-run.

La caché tiene un límite de tamaño y se puede configurar utilizando el parámetro cacheSize.

#### Descargas {#downloads}

Se comprueba el registro del archivo/blob solicitado en la caché local antes de acceder a él desde el almacén de datos. Cuando la caché supera el límite configurado (consulte la `cacheSize` ) al agregar un archivo a la caché, algunos de los archivos se desalojan para reclamar espacio.

#### Carga asincrónica {#async-upload}

La caché admite cargas asincrónicas al DataStore. Los archivos se almacenan localmente en la caché (en el sistema de archivos) y se inicia un trabajo asincrónico para cargar el archivo. El número de cargas asincrónicas está limitado por el tamaño de la caché de ensayo. El tamaño de la caché de ensayo se configura utilizando la variable `stagingSplitPercentage` parámetro. Este parámetro define el porcentaje del tamaño de la caché que se utilizará para la caché de ensayo. Además, el porcentaje de caché disponible para descargas se calcula como **(100 - `stagingSplitPercentage`) &#42;`cacheSize`**.

Las cargas asíncronas son de varios procesos y el número de subprocesos se configura mediante la variable `uploadThreads` parámetro.

Los archivos se mueven a la caché de descarga principal una vez completadas las cargas. Cuando el tamaño de la caché de ensayo supera su límite, los archivos se cargan sincrónicamente en el almacén de datos hasta que se completan las cargas asincrónicas anteriores y vuelve a haber espacio disponible en la caché de ensayo. Los archivos cargados se eliminan del área de ensayo mediante un trabajo periódico cuyo intervalo se configura mediante `stagingPurgeInterval` parámetro.

Las cargas que generan errores (por ejemplo, debido a una interrupción de la red) se colocan en una cola de reintentos y se vuelven a intentar periódicamente. El intervalo de reintento se configura mediante el `stagingRetryInterval parameter`.

#### Configuración de la replicación binaria con Amazon S3 {#configuring-binaryless-replication-with-amazon-s}

Para configurar la replicación binaria con S3, se requieren los siguientes pasos:

1. Instale las instancias de autor y publicación y asegúrese de que se inician correctamente.
1. Vaya a la configuración del agente de replicación abriendo una página en *https://localhost:4502/etc/replication/agents.author/publish.html*.
1. Pulse el botón **Editar** botón en el **Configuración** sección.
1. Cambie el **Serialización** escriba la opción en **Binario menos**.

1. Añada el parámetro &quot; `binaryless`= `true`&quot; en el uri de transporte. Después del cambio, el URI debe ser similar al siguiente:

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. Reinicie todas las instancias de autor y publicación para que los cambios surtan efecto.

#### Creación de un clúster con S3 y MongoDB {#creating-a-cluster-using-s-and-mongodb}

1. Desempaquete el inicio rápido de CQ con el siguiente comando:

   `java -jar cq-quickstart.jar -unpack`

1. AEM Una vez desempaquetado el paquete, cree una carpeta dentro del directorio de instalación de *crx-quickstart*/*instalar*.

1. Cree estos dos archivos dentro de la `crx-quickstart` carpeta:

   * *org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService*.*Configuración*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*.*Configuración*

   Una vez creados los archivos, agregue las opciones de configuración según sea necesario.

1. Instale los dos paquetes necesarios para el almacén de datos S3 tal como se explica más arriba.
1. Asegúrese de que MongoDB está instalado y es una instancia de `mongod` se está ejecutando.
1. AEM Comience con el siguiente comando:

   `java -Xmx1024m -jar cq-quickstart.jar -r crx3,crx3mongo`

1. AEM Repita los pasos del 1 al 4 para la segunda instancia de.
1. AEM Inicie la segunda instancia de.

#### Configuración de un almacén de datos compartido {#configuring-a-shared-data-store}

1. En primer lugar, cree el archivo de configuración del almacén de datos en cada instancia necesaria para compartir el almacén de datos:

   * Si utiliza un `FileDataStore`, cree un archivo llamado `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` y colóquelo en el `<aem-install>/crx-quickstart/install` carpeta.

   * Si utiliza S3 como almacén de datos, cree un archivo denominado o `rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` en el `<aem-install>/crx-quickstart/install` como se ha indicado anteriormente.

1. Modifique los archivos de configuración del almacén de datos en cada instancia para que apunten al mismo almacén de datos. Para obtener más información, consulte [este artículo](/help/sites-deploying/data-store-config.md#data-store-configurations).
1. Si la instancia se ha clonado desde un servidor existente, debe quitar la variable `clusterId` de la nueva instancia mediante la última herramienta oak-run mientras el repositorio está sin conexión. El comando que debe ejecutar es:

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >Si se configura un almacén de nodos de segmentos, se debe especificar la ruta del repositorio. La ruta predeterminada es `<aem-install-folder>/crx-quickstart/repository/segmentstore.` Si se ha configurado un almacén de nodos de documento, puede utilizar un [URI de cadena de conexión Mongo](https://docs.mongodb.org/manual/reference/connection-string/).

   >[!NOTE]
   >
   >La herramienta Oak-run se puede descargar desde esta ubicación:
   >
   >
   >[https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)
   >
   >
   >AEM Se deben utilizar distintas versiones de la herramienta en función de la versión de Oak que utilice con la instalación de la. Compruebe la lista de requisitos de versión que aparece a continuación antes de utilizar la herramienta:
   >
   >
   >
   >    * Para versiones de Oak **1.2.x** use el Oak-run **1.2.12 o posterior**
   >    * Para versiones de Oak **más reciente que el anterior** AEM , use la versión de Oak-run que coincida con el núcleo de Oak de su instalación de la.
   >
   >

1. Por último, valide la configuración. Para validarlo, busque un archivo único agregado al almacén de datos por cada repositorio que lo comparta. El formato de los archivos es el siguiente `repository-[UUID]`, donde UUID es un identificador único de cada repositorio individual.

   Por lo tanto, una configuración adecuada debe tener tantos archivos únicos como repositorios que compartan el almacén de datos.

   Los archivos se almacenan de forma diferente, según el almacén de datos:

   * Para el `FileDataStore` los archivos se crean en la ruta raíz de la carpeta del almacén de datos.
   * Para el `S3DataStore` los archivos se crean en el contenedor S3 configurado en la variable `META` carpeta.

## Almacén de datos de Azure {#azure-data-store}

AEM Se puede configurar el almacenamiento de datos en el servicio de almacenamiento de Azure de Microsoft®. Utiliza el `org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` PID para la configuración.

Para habilitar la funcionalidad del almacén de datos de Azure, se debe descargar e instalar un paquete de funciones que contenga el conector de Azure. Vaya a la [Repositorio de Adobe](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.azureblobconnector/) y descargue la versión más reciente de las versiones 1.6.x del paquete de funciones (por ejemplo, com.adobe.granite.oak.azureblobconnector-1.6.3.zip).

>[!NOTE]
>
>AEM Cuando se utiliza el archivo con TarMK, los binarios se almacenan de forma predeterminada en el almacén de datos de archivo. AEM Para usar TarMK con el almacén de datos de Azure, debe empezar a usar la interfaz de usuario de TarMK en el almacén de datos de `crx3tar-nofds` modo de ejecución, por ejemplo:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

Una vez descargado, puede instalar y configurar el conector de Azure de la siguiente manera:

1. Extraiga el contenido del archivo zip del paquete de funciones en una carpeta temporal.

1. Vaya a la carpeta temporal y copie el contenido de `jcr_root/libs/system/install` a la `<aem-install>crx-quickstart/install` carpeta.
1. AEM Si ya está configurado para trabajar con el almacenamiento Tar o MongoDB, elimine los archivos de configuración existentes del `/crx-quickstart/install` antes de continuar. Los archivos que deben eliminarse son los siguientes:

   Para MongoMK:

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   Para TarMK:

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Vuelva a la ubicación temporal en la que se ha extraído el paquete de funciones y copie el contenido de `jcr_root/libs/system/config` a la `<aem-install>/crx-quickstart/install` carpeta.
1. Edite el archivo de configuración y añada las opciones de configuración que requiera el programa de instalación.
1. AEM Inicio de.

Puede utilizar el archivo de configuración con las siguientes opciones:

* azureSas=&quot;&quot;: en la versión 1.6.3 del conector, se agregó compatibilidad con la firma de acceso compartido (SAS) de Azure. **Si existen credenciales de SAS y de almacenamiento en el archivo de configuración, SAS tiene prioridad.** Para obtener más información acerca de SAS, consulte [documentación oficial](https://learn.microsoft.com/en-us/azure/storage/common/storage-sas-overview). Asegúrese de que el carácter &quot;=&quot; tiene un carácter de escape similar a &quot;\=&quot;.

* azureBlobEndpoint=&quot;&quot;: El extremo del blob de Azure. Por ejemplo, https://&lt;storage-account>.blob.core.windows.net.
* accessKey=&quot;&quot;: nombre de la cuenta de almacenamiento. Para obtener más información sobre las credenciales de autenticación de Microsoft® Azure, consulte la [documentación oficial](https://azure.microsoft.com/en-us/documentation/articles/storage-create-storage-account).

* secretKey=&quot;&quot;: La clave de acceso de almacenamiento. Asegúrese de que el carácter &quot;=&quot; tiene un carácter de escape similar a &quot;\=&quot;.
* container=&quot;&quot;: el nombre del contenedor de almacenamiento del blob de Microsoft® Azure. El contenedor es una agrupación de un conjunto de blobs. Para obtener más información, lea la [documentación oficial](https://learn.microsoft.com/en-us/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata?redirectedfrom=MSDN).
* maxConnections=&quot;&quot;: el número simultáneo de solicitudes simultáneas por operación. El valor predeterminado es 1.
* maxErrorRetry=&quot;&quot;: número de reintentos por solicitud. El valor predeterminado es 3.
* socketTimeout=&quot;&quot;: intervalo de tiempo de espera, en milisegundos, utilizado para la solicitud. El valor predeterminado es 5 minutos.

Además de los ajustes anteriores, también se pueden configurar los siguientes ajustes:

* ruta: la ruta del almacén de datos. El valor predeterminado es `<aem-install>/repository/datastore.`
* RecordLength: tamaño mínimo de un objeto que debe almacenarse en el almacén de datos. El valor predeterminado es 16 KB.
* maxCachedBinarySize: Los binarios con un tamaño menor o igual a este tamaño se almacenan en la memoria caché. El tamaño es en bytes. El valor predeterminado es 17408 (17 KB).
* cacheSize: Tamaño de la caché. El valor se especifica en bytes. El valor predeterminado es 64 GB.
* secret: solo se debe utilizar si se utiliza la replicación binaria para la configuración del almacén de datos compartido.
* stagingSplitPercentage: porcentaje del tamaño de caché configurado para utilizarse en las cargas asincrónicas de ensayo. El valor predeterminado es 10.
* uploadThreads: número de subprocesos de carga que se utilizan para cargas asincrónicas. El valor predeterminado es 10.
* stagingPurgeInterval: intervalo en segundos para purgar cargas finalizadas de la caché de ensayo. El valor predeterminado es 300 segundos (5 minutos).
* stagingRetryInterval: intervalo de reintento en segundos para cargas fallidas. El valor predeterminado es 600 segundos (10 minutos).

>[!NOTE]
>
>Todos los ajustes deben colocarse entre comillas, por ejemplo:

```shell
accessKey="ASDASDERFAERAER"
secretKey="28932hfjlkwdo8fufsdfas\=\="
```

## Recopilación de residuos del almacén de datos {#data-store-garbage-collection}

El proceso de recolección de elementos no utilizados del almacén de datos se utiliza para quitar los archivos no utilizados del almacén de datos, lo que libera espacio en disco valioso en el proceso.

Para ejecutar la recolección de elementos no utilizados del almacén de datos:

1. Vaya a la consola JMX en *https://&lt;serveraddress:port>/system/console/jmx*
1. Buscando por **RepositoryManagement.** Cuando encuentre el MBean del Administrador de repositorios, haga clic en él para que aparezcan las opciones disponibles.
1. Desplácese hasta el final de la página y haga clic en **startDataStoreGC(boolean markOnly)** vínculo.
1. En el siguiente cuadro de diálogo, escriba `false` para el `markOnly` y haga clic en **Invocar**:

   ![chlimage_1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >El `markOnly` indica si se ejecuta o no la fase de barrido de la recolección de elementos no utilizados.

## Recolección de elementos no utilizados del almacén de datos para un almacén de datos compartido {#data-store-garbage-collection-for-a-shared-data-store}

>[!NOTE]
>
>Al realizar la recolección de elementos no utilizados en un almacén de datos agrupado o compartido, la configuración (con Mongo o Segment TAR) del registro puede mostrar advertencias sobre la incapacidad para eliminar ciertos ID de blob. Los identificadores de blob eliminados en una recolección de elementos no utilizados anterior vuelven a ser referenciados incorrectamente por otros clústeres o nodos compartidos que no tienen información sobre las eliminaciones de identificadores. Como resultado, cuando se realiza la recolección de elementos no utilizados, se registra una advertencia cuando se intenta eliminar un ID que ya se ha eliminado en la última ejecución. Este comportamiento no afecta al rendimiento ni a la funcionalidad.

>[!NOTE]
>
>Si utiliza una configuración de almacén de datos compartida y la recopilación de elementos no utilizados del almacén de datos está deshabilitada, la ejecución de la tarea de limpieza binaria de Lucene puede aumentar repentinamente el espacio en disco utilizado. Considere la posibilidad de deshabilitar BlobTracker en todas las instancias de autor y publicación haciendo lo siguiente:
>
>1. AEM Detenga la instancia de.
>2. Añada el `blobTrackSnapshotIntervalInSecs=L"0"` en el campo `crx-quickstart/install/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` archivo. Este parámetro requiere Oak 1.12.0, 1.10.2 o posterior.
>3. AEM Vuelva a iniciar la instancia de.

AEM Con las versiones más recientes de la aplicación, la recolección de elementos no utilizados del almacén de datos también se puede ejecutar en almacenes de datos compartidos por más de un repositorio. Para poder ejecutar la recolección de elementos no utilizados del almacén de datos en un almacén de datos compartido, siga estos pasos:

1. Asegúrese de que todas las tareas de mantenimiento configuradas para la recopilación de residuos del almacén de datos estén desactivadas en todas las instancias del repositorio que compartan el almacén de datos.
1. Ejecute los pasos mencionados en [Recolección binaria de elementos no utilizados](/help/sites-deploying/data-store-config.md#data-store-garbage-collection) individualmente el **todo** instancias del repositorio que comparten el almacén de datos. Sin embargo, asegúrese de introducir lo siguiente `true` para el `markOnly` antes de hacer clic en el botón Invocar:

   ![chlimage_1-10](assets/chlimage_1-10.png)

1. Después de completar el procedimiento anterior en todas las instancias, ejecute de nuevo el recolector de elementos no utilizados del almacén de datos desde **cualquiera** de las instancias:

   1. Vaya a la consola JMX y seleccione el MBean Repository Manager.
   1. Haga clic en **Haga clic en startDataStoreGC(boolean markOnly)** vínculo.
   1. En el siguiente cuadro de diálogo, escriba `false` para el `markOnly` parámetro de nuevo.

   Todos los archivos encontrados se recopilan utilizando la fase de marcado utilizada anteriormente y eliminando el resto que no se utilicen del almacén de datos.
