---
title: Configuración de almacenes de nodos y almacenes de datos en AEM 6
description: Obtenga información sobre cómo configurar almacenes de nodos y almacenes de datos y cómo realizar la colección de residuos del almacén de datos.
content-type: reference
topic-tags: deploying
docset: aem65
feature: Configuring
exl-id: c1c90d6a-ee5a-487d-9a8a-741b407c8c06
source-git-commit: bb8dbb9069c4575af62a4d0b21195cee75944fea
workflow-type: tm+mt
source-wordcount: '3583'
ht-degree: 2%

---

# Configuración de almacenes de nodos y almacenes de datos en AEM 6{#configuring-node-stores-and-data-stores-in-aem}

## Introducción {#introduction}

En Adobe Experience Manager (AEM), los datos binarios se pueden almacenar de forma independiente de los nodos de contenido. Los datos binarios se almacenan en un almacén de datos, mientras que los nodos de contenido se almacenan en un almacén de nodos.

Tanto los almacenes de datos como los almacenes de nodos se pueden configurar mediante la configuración OSGi. Se hace referencia a cada configuración de OSGi mediante un identificador persistente (PID).

## Pasos de configuración {#configuration-steps}

Para configurar el almacén de nodos y el almacén de datos, siga estos pasos:

1. Copie el archivo JAR de inicio rápido AEM en su directorio de instalación.
1. Crear una carpeta `crx-quickstart/install` en el directorio de instalación.
1. En primer lugar, configure el almacén de nodos creando un archivo de configuración con el nombre de la opción de almacén de nodos que desea utilizar en la variable `crx-quickstart/install` directorio.

   Por ejemplo, el almacén de nodos Document (que es la base de AEM implementación MongoMK) utiliza el archivo `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`.

1. Edite el archivo y establezca las opciones de configuración.
1. Cree un archivo de configuración con el PID del almacén de datos que desea utilizar. Edite el archivo para establecer las opciones de configuración.

   >[!NOTE]
   >
   >Consulte [Configuraciones del almacén de nodos](#node-store-configurations) y [Configuraciones del almacén de datos](#data-store-configurations) para las opciones de configuración.

1. Inicie AEM.

## Configuraciones del almacén de nodos {#node-store-configurations}

>[!CAUTION]
>
>Las versiones más recientes de Oak emplean un nuevo esquema de nombres y formato para los archivos de configuración OSGi. El nuevo esquema de nombres requiere que se nombre el archivo de configuración **.config** y el nuevo formato requiere que se escriban valores y [documentado aquí](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format).
>
>Si actualiza desde una versión anterior de Oak, asegúrese de realizar una copia de seguridad de la variable `crx-quickstart/install`en primer lugar. Después de la actualización, restaure el contenido de la carpeta en la instalación actualizada y modifique la extensión de los archivos de configuración desde **.cfg** a **.config**.
>
>En caso de que esté leyendo este artículo como preparación para una actualización de un **AEM 5.x** instalación, asegúrese de consultar la [actualización](https://docs.adobe.com/content/docs/en/aem/6-0/deploy/upgrade.html) en primer lugar.

### Almacén de nodos de segmento {#segment-node-store}

El almacén de nodos del segmento es la base de la implementación de TarMK de Adobe en AEM6. Utiliza el `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` PID para configuración.

>[!CAUTION]
>
>El PID del almacén de nodos del segmento ha cambiado de `org.apache.jackrabbit.oak.plugins.segment.SegmentNodeStoreService in previous versions` del AEM 6 al `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` en AEM 6.3. Asegúrese de realizar los ajustes de configuración necesarios para reflejar este cambio.

Puede configurar las siguientes opciones:

* `repository.home`: Ruta al inicio del repositorio en el cual se almacenan los datos relacionados con el repositorio. De forma predeterminada, los archivos de segmentos se almacenan en la sección `crx-quickstart/segmentstore` directorio.

* `tarmk.size`: Tamaño máximo de un segmento en MB. El máximo predeterminado es 256 MB.
* `customBlobStore`: Valor booleano que indica que se utiliza un almacén de datos personalizado. El valor predeterminado es true para AEM versión 6.3 y posteriores. Antes de AEM 6.3, el valor predeterminado era false.

El siguiente es un ejemplo `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` archivo:

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### Almacén de nodos de documento {#document-node-store}

El almacén de nodos del documento es la base de AEM implementación de MongoMK. Utiliza el `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService`* *PID. Estas son las opciones de configuración disponibles:

* `mongouri`: La variable [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) necesario para conectarse a la base de datos Mongo. El valor predeterminado es `mongodb://localhost:27017`

* `db`: Nombre de la base de datos de Mongo. El valor predeterminado es **Oak** ``. However, new AEM 6 installations use **aem-author** ``como nombre predeterminado de la base de datos.

* `cache`: El tamaño de caché en MB. Esto se distribuye entre varias cachés utilizadas en DocumentNodeStore. El valor predeterminado es `256`

* `changesSize`: Tamaño en MB de colección restringida utilizada en Mongo para almacenar en caché la salida diff. El valor predeterminado es `256`

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

Por ejemplo, si el proyecto requiere un gran número de recursos multimedia, almacenarlos en el File o S3 Data Store hará que el acceso a ellos sea más rápido que almacenarlo directamente en un MongoDB.

El almacén de datos de archivos proporciona un mejor rendimiento que MongoDB, y las operaciones de copia de seguridad y restauración de Mongo también son más lentas con un gran número de activos.

A continuación se describen los detalles de los diferentes almacenes de datos y configuraciones.

>[!NOTE]
>
>Para habilitar los almacenes de datos personalizados, debe asegurarse de que `customBlobStore` está configurado como `true` en el archivo de configuración del almacén de nodos correspondiente ([almacén de nodos de segmento](/help/sites-deploying/data-store-config.md#segment-node-store) o [almacén de nodos del documento](/help/sites-deploying/data-store-config.md#document-node-store)).

### Almacén de datos de archivo {#file-data-store}

Esta es la implementación de [FileDataStore](https://jackrabbit.apache.org/api/2.8/org/apache/jackrabbit/core/data/FileDataStore.html) presente en Jackrabbit 2. Proporciona una forma de almacenar los datos binarios como archivos normales en el sistema de archivos. Utiliza el `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore` PID.

Estas opciones de configuración están disponibles:

* `repository.home`: Ruta al inicio del repositorio donde se almacenan varios datos relacionados con el repositorio. De forma predeterminada, los archivos binarios se almacenan en `crx-quickstart/repository/datastore` directory

* `path`: Ruta al directorio bajo el cual se almacenarán los archivos. Si se especifica, tiene prioridad sobre `repository.home` value

* `minRecordLength`: El tamaño mínimo en bytes de un archivo almacenado en el almacén de datos. El contenido binario menor que este valor se insertaría.

>[!NOTE]
>
>Cuando utilice un NAS para almacenar almacenes de datos de archivos compartidos, asegúrese de usar solamente dispositivos de alto rendimiento para evitar problemas de performance.

## Almacenamiento de datos de Amazon S3 {#amazon-s-data-store}

AEM puede configurarse para almacenar datos en el servicio de almacenamiento simple (S3) de Amazon. Utiliza el `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` PID para configuración.

Para habilitar la funcionalidad del almacén de datos S3, es necesario descargar e instalar un paquete de funciones que contenga el conector S3 Datastore. Vaya a la [Repositorio de Adobes](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/) y descargue la versión más reciente de las versiones 1.10.x del feature pack (por ejemplo, com.adobe.granite.oak.s3connector-1.10.0.zip). Además, también debe descargar e instalar el Service Pack de AEM más reciente, tal y como se indica en la [Notas de la versión de AEM 6.5](/help/release-notes/release-notes.md) página.

>[!NOTE]
>
>Al utilizar AEM con TarMK, los binarios se almacenan de forma predeterminada en la variable `FileDataStore`. Para usar TarMK con el almacén de datos S3, debe empezar a AEM usando la variable `crx3tar-nofds` runmode, por ejemplo:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

Una vez descargado, puede instalar y configurar el S3 Connector de la siguiente manera:

1. Extraiga el contenido del archivo zip del paquete de características a una carpeta temporal.

1. Vaya a la carpeta temporal y vaya a la siguiente ubicación:

   ```xml
   jcr_root/libs/system/install
   ```

   Copie todo el contenido de la ubicación anterior a `<aem-install>/crx-quickstart/install.`

1. Si ya AEM está configurado para trabajar con el almacenamiento Tar o MongoDB, elimine los archivos de configuración existentes del ***&lt;aem-install>***/*crx-quickstart*/*instalar* antes de continuar. Los archivos que deben eliminarse son:

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Vuelva a la ubicación temporal en la que se ha extraído el paquete de funciones y copie el contenido de la siguiente carpeta:

   * `jcr_root/libs/system/config`

   hasta

   * `<aem-install>/crx-quickstart/install`

   Asegúrese de copiar únicamente los archivos de configuración necesarios para la configuración actual. Para un almacén de datos dedicado y una configuración de almacén de datos compartidos, copie la variable `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` archivo.

   >[!NOTE]
   >
   >En una configuración de clúster, realice los pasos anteriores en todos los nodos del clúster uno por uno. Además, asegúrese de utilizar la misma configuración de S3 para todos los nodos.

1. Edite el archivo y añada las opciones de configuración requeridas por su configuración.
1. Inicie AEM.

## Actualización a una nueva versión del conector S3 1.10.x {#upgrading-to-a-new-version-of-the-s-connector}

Si necesita actualizar el conector 1.10.x S3 a una nueva versión (por ejemplo, de 1.10.0 a 1.10.4), siga estos pasos:

1. Detenga la instancia de AEM.

1. Vaya a `<aem-install>/crx-quickstart/install/15` en la carpeta de instalación de AEM y haga una copia de seguridad de su contenido.
1. Después de la copia de seguridad, elimine la versión antigua del S3 Connector y sus dependencias eliminando todos los archivos jar en la `<aem-install>/crx-quickstart/install/15` carpeta, por ejemplo:

   * **oak-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**

   >[!NOTE]
   >
   >Los nombres de archivo presentados anteriormente se utilizan únicamente con fines ilustrativos.

1. Descargue la versión más reciente del paquete de funciones 1.10.x del [Repositorio de Adobes](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/).
1. Descomprima el contenido en una carpeta independiente y, a continuación, vaya a `jcr_root/libs/system/install/15`.
1. Copiar los archivos jar en **&lt;aem-install>**/crx-quickstart/install/15 en la carpeta de instalación de AEM.
1. Inicie AEM y compruebe la funcionalidad del conector.

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
>El conector S3 admite la autenticación de usuarios de IAM y la autenticación de funciones de IAM. Para utilizar la autenticación de funciones de IAM, omita el `accessKey` y `secretKey` del archivo de configuración. El conector S3 pasará de forma predeterminada a la variable [Función IAM](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) asignado a la instancia.

| Clave | Descripción | Predeterminado | Requerido |
| --- | --- | --- | --- |
| accessKey | Acceso al ID de clave para el usuario de IAM con acceso al bucket. |  | Sí, cuando no se utilizan funciones de IAM. |
| secretKey | Clave de acceso secreta para el usuario de IAM con acceso al bucket. |  | Sí, cuando no se utilizan funciones de IAM. |
| cacheSize | El tamaño (en bytes) de la caché local. | 64 GB | No. |
| connectionTimeout | Establezca la cantidad de tiempo de espera (en milisegundos) antes de que se agote el tiempo de espera al establecer inicialmente una conexión. | 10 000 | No. |
| maxCachedBinarySize | Los binarios con un tamaño menor o igual que este valor (en bytes) se almacenarán en la caché de memoria. | 17408 (17 KB) | No. |
| maxConnections | Establezca el número máximo de conexiones HTTP abiertas permitidas. | 50 | No. |
| maxErrorRetry | Establezca el número máximo de intentos de reintento para solicitudes fallidas (recuperables). | 3 | No. |
| minRecordLength | El tamaño mínimo de un objeto (en bytes) que debe almacenarse en el almacén de datos. | 16384 | No. |
| path | Ruta local del almacén de datos de AEM. | `crx-quickstart/repository/datastore` | No. |
| proxyHost | Establezca el host proxy opcional a través del que se conectará el cliente. |  | No. |
| proxyPort | Establezca el puerto proxy opcional por el que se conectará el cliente. |  | No. |
| s3Bucket | Nombre del depósito S3. |  | Sí |
| s3EndPoint | Punto final de la API de REST S3. |  | No. |
| s3Region | Región donde reside el bloque. Consulte esta [página](https://docs.aws.amazon.com/general/latest/gr/s3.html) para obtener más información. | Región en la que se está ejecutando la instancia de AWS. | No. |
| socketTimeout | Establezca el tiempo de espera (en milisegundos) para que los datos se transfieran a través de una conexión abierta establecida antes de que se agote el tiempo de espera de la conexión y se cierre. | 50000 | No. |
| stagingPurgeInterval | El intervalo (en segundos) para la depuración finalizó las cargas desde la caché de ensayo. | 300 | No. |
| stagingRetryInterval | El intervalo (en segundos) para reintentar cargas fallidas. | 600 | No. |
| stagingSplitPercentage | El porcentaje de `cacheSize` para su uso en el ensayo de cargas asíncronas. | 10 | No. |
| uploadThreads | Número de subprocesos de carga utilizados para cargas asincrónicas. | 10 | No. |
| writeThreads | Número de subprocesos simultáneos utilizados para escribir mediante S3 Transfer Manager. | 10 | No. |

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

### Almacenamiento en caché del almacén de datos {#data-store-caching}

>[!NOTE]
>
>Las implementaciones de DataStore de `S3DataStore`, `CachingFileDataStore` y `AzureDataStore` admiten el almacenamiento en caché del sistema de archivos local. La variable `CachingFileDataStore` La implementación es útil cuando DataStore está en NFS (Network File System).

Al actualizar desde una implementación de caché anterior (anterior a Oak 1.6), existe una diferencia en la estructura del directorio de caché del sistema de archivos local. En la estructura de caché antigua, tanto los archivos descargados como los cargados se colocaron directamente en la ruta de caché. La nueva estructura separa las descargas y cargas y las almacena en dos directorios llamados `upload` y `download` en ruta de caché. El proceso de actualización debe ser fluido y cualquier carga pendiente debe programarse para su carga, y cualquier archivo descargado previamente en la caché se colocará en la caché en la inicialización.

También puede actualizar la caché sin conexión utilizando el `datastorecacheupgrade` comando de oak-run. Para obtener más información sobre cómo ejecutar el comando, consulte la [readme](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md) para el módulo oak-run.

La caché tiene un límite de tamaño y se puede configurar utilizando el parámetro cacheSize .

#### Descargas {#downloads}

Se comprobará la caché local para el registro del archivo o blob solicitado antes de acceder a él desde el DataStore. Cuando la caché exceda el límite configurado (consulte la `cacheSize` ) al agregar un archivo a la caché, algunos de los archivos se desalojarán para recuperar espacio.

#### Carga asíncrona {#async-upload}

La caché admite cargas asíncronas a DataStore. Los archivos se montan localmente, en la caché (en el sistema de archivos), y un trabajo asincrónico comienza a cargar el archivo. El número de cargas asincrónicas está limitado por el tamaño de la caché de ensayo. El tamaño de la caché de ensayo se configura usando la variable `stagingSplitPercentage` parámetro. Este parámetro define el porcentaje de tamaño de caché que se utilizará para la caché de ensayo. Además, el porcentaje de caché disponible para las descargas se calcula como **(100 - `stagingSplitPercentage`) &#42;`cacheSize`**.

Las cargas asincrónicas son multiproceso y el número de subprocesos se configura usando la variable `uploadThreads` parámetro.

Los archivos se mueven a la caché de descarga principal una vez completadas las cargas. Cuando el tamaño de la caché de ensayo supera su límite, los archivos se cargan sincrónicamente en DataStore hasta que las cargas asincrónicas anteriores se completen y vuelva a haber espacio disponible en la caché de ensayo. Los archivos cargados se eliminan del área de ensayo mediante un trabajo periódico cuyo intervalo está configurado por el `stagingPurgeInterval` parámetro.

Las cargas fallidas (por ejemplo, debido a una interrupción de la red) se colocan en una cola de reintentos y se vuelven a intentar periódicamente. El intervalo de reintento se configura usando la variable `stagingRetryInterval parameter`.

#### Configuración de la replicación sin binarios con Amazon S3 {#configuring-binaryless-replication-with-amazon-s}

Para configurar la replicación binaria con S3, se requieren los siguientes pasos:

1. Instale las instancias de autor y publicación y asegúrese de que se inicien correctamente.
1. Vaya a la configuración del agente de replicación, abriendo una página en *https://localhost:4502/etc/replication/agents.author/publish.html*.
1. Pulse el botón **Editar** en el **Configuración** para obtener más información.
1. Cambie el **Serialización** opción de tipo **Menor binario**.

1. Añada el parámetro &quot; `binaryless`= `true`&quot; en el uri de transporte. Después del cambio, el uri debe tener un aspecto similar al siguiente:

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. Reinicie todas las instancias de autor y publicación para que los cambios surtan efecto.

#### Creación de un clúster mediante S3 y MongoDB {#creating-a-cluster-using-s-and-mongodb}

1. Desempaquete el inicio rápido de CQ usando el siguiente comando:

   `java -jar cq-quickstart.jar -unpack`

1. Una vez desempaquetado AEM, cree una carpeta dentro del directorio de instalación *crx-quickstart*/*instalar*.

1. Cree estos dos archivos dentro del `crx-quickstart` carpeta:

   * *org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService*.*Configuración*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*.*Configuración*

   Una vez creados los archivos, añada las opciones de configuración según sea necesario.

1. Instale los dos paquetes necesarios para el almacén de datos S3 como se explica más arriba.
1. Asegúrese de que MongoDB esté instalado y que haya una instancia de `mongod` se está ejecutando.
1. Inicie AEM con el siguiente comando:

   `java -Xmx1024m -jar cq-quickstart.jar -r crx3,crx3mongo`

1. Repita los pasos del 1 al 4 para la segunda instancia de AEM.
1. Inicie la segunda instancia de AEM.

#### Configuración de un almacén de datos compartido {#configuring-a-shared-data-store}

1. En primer lugar, cree el archivo de configuración del almacén de datos en cada instancia necesaria para compartir el almacén de datos:

   * Si está utilizando un `FileDataStore`, cree un archivo con el nombre `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` y colóquelo en el `<aem-install>/crx-quickstart/install` carpeta.

   * Si utiliza S3 como almacén de datos, cree un archivo denominado o `rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` en el `<aem-install>/crx-quickstart/install` como se muestra arriba.

1. Modifique los archivos de configuración del almacén de datos en cada instancia para que apunten al mismo almacén de datos. Para obtener más información, consulte [este artículo](/help/sites-deploying/data-store-config.md#data-store-configurations).
1. Si la instancia se ha clonado desde un servidor existente, debe quitar la variable `clusterId` de la nueva instancia utilizando la última herramienta oak-run mientras el repositorio está sin conexión. El comando que debe ejecutar es:

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >Si se configura un almacén de nodos de segmento, se debe especificar la ruta del repositorio. De forma predeterminada, la ruta es `<aem-install-folder>/crx-quickstart/repository/segmentstore.` Si está configurado un almacén de nodos de documento, puede utilizar un [URI de cadena de conexión Mongo](https://docs.mongodb.org/manual/reference/connection-string/).

   >[!NOTE]
   >
   >La herramienta Oak-run se puede descargar desde esta ubicación:
   >
   >
   >[https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)
   >
   >
   >Tenga en cuenta que es necesario utilizar distintas versiones de la herramienta en función de la versión de Oak que utilice con la instalación de AEM. Compruebe la lista de requisitos de la versión que aparece a continuación antes de utilizar la herramienta:
   >
   >
   >
   >    * Para versiones de Oak **1.2.x** usar Oak-run **1.2.12 o posterior**
   >    * Para versiones de Oak **más reciente que el anterior**, utilice la versión de Oak-run que coincida con el núcleo Oak de su instalación de AEM.


1. Finalmente, valide la configuración. Para ello, debe buscar un archivo único agregado al almacén de datos por cada repositorio que lo esté compartiendo. El formato de los archivos es `repository-[UUID]`, donde el UUID es un identificador único de cada repositorio individual.

   Por lo tanto, una configuración adecuada debe tener tantos archivos únicos como repositorios que compartan el almacén de datos.

   Los archivos se almacenan de forma diferente, según el almacén de datos:

   * Para la variable `FileDataStore` los archivos se crean en la ruta raíz de la carpeta del almacén de datos.
   * Para la variable `S3DataStore` los archivos se crean en el compartimento configurado S3 en el `META` carpeta.

## Almacén de datos de Azure {#azure-data-store}

AEM puede configurarse para almacenar datos en el servicio de almacenamiento de Azure de Microsoft. Utiliza el `org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` PID para configuración.

Para habilitar la funcionalidad del almacén de datos de Azure, es necesario descargar e instalar un paquete de funciones que contenga el conector de Azure. Vaya a la [Repositorio de Adobes](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.azureblobconnector/) y descargue la versión más reciente de las versiones 1.6.x del feature pack (por ejemplo, com.adobe.granite.oak.azureblobconnector-1.6.3.zip).

>[!NOTE]
>
>Al utilizar AEM con TarMK, los binarios se almacenan de forma predeterminada en FileDataStore. Para usar TarMK con el DataStore de Azure, debe empezar a AEM usando la variable `crx3tar-nofds` runmode, por ejemplo:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

Una vez descargado, puede instalar y configurar el conector de Azure de la siguiente manera:

1. Extraiga el contenido del archivo zip del paquete de características a una carpeta temporal.

1. Vaya a la carpeta temporal y copie el contenido de `jcr_root/libs/system/install` a `<aem-install>crx-quickstart/install` carpeta.
1. Si ya AEM está configurado para trabajar con el almacenamiento Tar o MongoDB, elimine los archivos de configuración existentes del `/crx-quickstart/install` antes de continuar. Los archivos que deben eliminarse son:

   Para MongoMK:

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   Para TarMK:

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Vuelva a la ubicación temporal en la que se ha extraído el paquete de funciones y copie el contenido de `jcr_root/libs/system/config` a `<aem-install>/crx-quickstart/install` carpeta.
1. Edite el archivo de configuración y añada las opciones de configuración requeridas por la configuración.
1. Inicie AEM.

Puede utilizar el archivo de configuración con las siguientes opciones:

* azureSas=&quot;&quot;: En la versión 1.6.3 del conector, se agregó compatibilidad con Azure Shared Access Signature (SAS). **Si tanto SAS como credenciales de almacenamiento existen en el archivo de configuración, SAS tiene prioridad.** Para obtener más información sobre SAS, consulte [documentación oficial](https://docs.microsoft.com/en-us/azure/storage/common/storage-dotnet-shared-access-signature-part-1). Asegúrese de que el carácter &#39;=&#39; se escapa como &#39;\=&#39;.

* azureBlobEndpoint=&quot;&quot;: Punto final de Azure Blob. Por ejemplo, https://&lt;storage-account>.blob.core.windows.net.
* accessKey=&quot;&quot;: El nombre de la cuenta de almacenamiento. Para obtener más información sobre las credenciales de autenticación de Microsoft Azure, consulte la [documentación oficial](https://azure.microsoft.com/en-us/documentation/articles/storage-create-storage-account).

* secretKey=&quot;&quot;: La clave de acceso al almacenamiento. Asegúrese de que el carácter &#39;=&#39; se escapa como &#39;\=&#39;.
* container=&quot;&quot;: El nombre del contenedor de almacenamiento del blob de Microsoft Azure. El contenedor es una agrupación de un conjunto de blobs. Para obtener más información, lea la [documentación oficial](https://msdn.microsoft.com/en-us/library/dd135715.aspx).
* maxConnections=&quot;&quot;: Número simultáneo de solicitudes simultáneas por operación. El valor predeterminado es 1.
* maxErrorRetry=&quot;&quot;: Número de reintentos por solicitud. El valor predeterminado es 3.
* socketTimeout=&quot;&quot;: El intervalo de tiempo de espera, en milisegundos, utilizado para la solicitud. El valor predeterminado es de 5 minutos.

Además de los ajustes anteriores, también se pueden configurar los siguientes ajustes:

* ruta: Ruta del almacén de datos. El valor predeterminado es `<aem-install>/repository/datastore.`
* RecordLength: El tamaño mínimo de un objeto que debe almacenarse en el almacén de datos. El valor predeterminado es 16 KB.
* maxCachedBinarySize: Los binarios con un tamaño menor o igual que este tamaño se almacenarán en la caché de memoria. El tamaño se expresa en bytes. El valor predeterminado es 17408 (17 KB).
* cacheSize: El tamaño de la caché. El valor se especifica en bytes. El valor predeterminado es de 64 GB.
* secreto: Solo para su uso si utiliza replicación sin binarios para la configuración del almacén de datos compartido.
* stagingSplitPercentage: El porcentaje de tamaño de caché configurado para utilizarse en el ensayo de cargas asincrónicas. El valor predeterminado es 10.
* uploadThreads: Número de subprocesos de carga que se utilizan para cargas asincrónicas. El valor predeterminado es 10.
* stagingPurgeInterval: El intervalo en segundos para la depuración finalizó las cargas desde la caché de ensayo. El valor predeterminado es de 300 segundos (5 minutos).
* stagingRetryInterval: Intervalo de reintentos en segundos para cargas fallidas. El valor predeterminado es 600 segundos (10 minutos).

>[!NOTE]
>
>Todos los ajustes deben introducirse entre comillas, por ejemplo:

```shell
accessKey="ASDASDERFAERAER"
secretKey="28932hfjlkwdo8fufsdfas\=\="
```

## Colección de residuos del almacén de datos {#data-store-garbage-collection}

El proceso de colección de residuos del almacén de datos se utiliza para eliminar cualquier archivo no utilizado en el almacén de datos, lo que libera espacio en disco valioso durante el proceso.

Para ejecutar la colección de residuos del almacén de datos, haga lo siguiente:

1. Accediendo a la consola JMX ubicada en *https://&lt;serveraddress:port>/system/console/jmx*
1. Buscando **RepositoryManagement.** Una vez que encuentre el Repository Manager MBean, haga clic en él para que aparezcan las opciones disponibles.
1. Desplácese hasta el final de la página y haga clic en el botón **startDataStoreGC(boolean markOnly)** vínculo.
1. En el cuadro de diálogo siguiente, introduzca `false` para el `markOnly` y, a continuación, haga clic en **Invocar**:

   ![Chlimage_1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >La variable `markOnly` paramater significa si la fase de barrido de la colección de basura se ejecutará o no.

## Colección de residuos del almacén de datos para un almacén de datos compartido {#data-store-garbage-collection-for-a-shared-data-store}

>[!NOTE]
>
>Al realizar la colección de residuos en una configuración de almacén de datos agrupada o compartida (con Mongo o Segment Tar), el registro puede mostrar advertencias sobre la incapacidad de eliminar ciertos ID de blob. Esto sucede porque otros clústeres o nodos compartidos a los que no hay información sobre las eliminaciones de ID hacen referencia incorrectamente a los ID de blob eliminados en una colección de residuos anterior. Como resultado, cuando se realiza la colección de residuos, registra una advertencia cuando intenta eliminar un ID que ya se ha eliminado en la última ejecución. Este comportamiento no afecta al rendimiento ni a la funcionalidad.

>[!NOTE]
> Si está utilizando una configuración compartida del almacén de datos y la colección de residuos del almacén de datos está deshabilitada, la ejecución de la tarea de limpieza binaria de Lucene puede aumentar repentinamente el espacio en disco utilizado. Para evitarlo, debe deshabilitar BlobTracker en todas las instancias de autor y publicación de la siguiente manera:
>
> 1. Detenga la instancia de AEM.
> 2. Agregue la variable `blobTrackSnapshotIntervalInSecs=L"0"` en el `crx-quickstart/install/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` archivo. Este parámetro requiere Oak 1.12.0, 1.10.2 o posterior.
> 3. Vuelva a iniciar la instancia de AEM.


Con versiones más recientes de AEM, la colección de residuos del almacén de datos también se puede ejecutar en almacenes de datos compartidos por más de un repositorio. Para poder ejecutar la colección de residuos del almacén de datos en un almacén de datos compartido, siga los siguientes pasos:

1. Asegúrese de que todas las tareas de mantenimiento configuradas para la colección de residuos del almacén de datos estén deshabilitadas en todas las instancias del repositorio que compartan el almacén de datos.
1. Ejecute los pasos mencionados en [Colección de residuos binarios](/help/sites-deploying/data-store-config.md#data-store-garbage-collection) individualmente en **all** instancias del repositorio que comparten el almacén de datos. Sin embargo, asegúrese de introducir `true` para el `markOnly` antes de hacer clic en el botón Invocar:

   ![imagen_1-10](assets/chlimage_1-10.png)

1. Después de completar el procedimiento anterior en todas las instancias, ejecute de nuevo la colección de residuos del almacén de datos desde **any** de las instancias:

   1. Vaya a la consola JMX y seleccione el Mbean de Repository Manager.
   1. Haga clic en el **Haga clic en startDataStoreGC(boolean markOnly)** vínculo.
   1. En el cuadro de diálogo siguiente, introduzca `false` para el `markOnly` de nuevo.
   Esto recopilará todos los archivos encontrados utilizando la fase de marca utilizada anteriormente y eliminará el resto que no se utilice del almacén de datos.
