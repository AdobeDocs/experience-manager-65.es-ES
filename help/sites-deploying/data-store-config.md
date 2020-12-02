---
title: Configuración de almacenes de nodos y almacenes de datos en AEM 6
seo-title: Configuración de almacenes de nodos y almacenes de datos en AEM 6
description: Obtenga información sobre cómo configurar almacenes de nodos y almacenes de datos y cómo realizar la recopilación de elementos no utilizados del almacén de datos.
seo-description: Obtenga información sobre cómo configurar almacenes de nodos y almacenes de datos y cómo realizar la recopilación de elementos no utilizados del almacén de datos.
uuid: 1a58c0ba-1c32-4539-ad0d-0a27c8c4ff5e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: b97482f2-2791-4d14-ae82-388302d9eab3
docset: aem65
legacypath: /deploy/platform/data-store-config
translation-type: tm+mt
source-git-commit: 93cb84763cfd77b67a5dd1481caab79337f6e7c4
workflow-type: tm+mt
source-wordcount: '3423'
ht-degree: 1%

---


# Configuración de almacenes de nodos y almacenes de datos en AEM 6{#configuring-node-stores-and-data-stores-in-aem}

## Introducción {#introduction}

En Adobe Experience Manager (AEM), los datos binarios se pueden almacenar independientemente de los nodos de contenido. Los datos binarios se almacenan en un almacén de datos, mientras que los nodos de contenido se almacenan en un almacén de nodos.

Tanto los almacenes de datos como los almacenes de nodos se pueden configurar mediante la configuración OSGi. Se hace referencia a cada configuración OSGi mediante un identificador persistente (PID).

## Pasos de configuración {#configuration-steps}

Para configurar el almacén de nodos y el almacén de datos, lleve a cabo los siguientes pasos:

1. Copie el archivo JAR de inicio rápido AEM en su directorio de instalación.
1. Cree una carpeta `crx-quickstart/install` en el directorio de instalación.
1. Primero, configure el almacén de nodos creando un archivo de configuración con el nombre de la opción de almacén de nodos que desee utilizar en el directorio `crx-quickstart/install`.

   Por ejemplo, el almacén de nodos de Documento (que es la base para AEM implementación de MongoMK) utiliza el archivo `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`.

1. Edite el archivo y defina las opciones de configuración.
1. Cree un archivo de configuración con el PID del almacén de datos que desee utilizar. Edite el archivo para establecer las opciones de configuración.

   >[!NOTE]
   >
   >Consulte [Configuraciones del almacén de nodos](#node-store-configurations) y [Configuraciones del almacén de datos](#data-store-configurations) para ver las opciones de configuración.

1. Inicio AEM.

## Configuraciones del almacén de nodos {#node-store-configurations}

>[!CAUTION]
>
>Las versiones más recientes de Oak emplean un nuevo esquema y formato de nombres para los archivos de configuración OSGi. El nuevo esquema de nombres requiere que el archivo de configuración se llame **.config** y que el nuevo formato requiera que se escriban valores y esté [documentado aquí](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format).
>
>Si actualiza desde una versión anterior de Oak, asegúrese de realizar una copia de seguridad de la carpeta `crx-quickstart/install`primero. Después de la actualización, restaure el contenido de la carpeta en la instalación actualizada y modifique la extensión de los archivos de configuración de **.cfg** a **.config**.
>
>Si está leyendo este artículo como preparación para una actualización desde una instalación **AEM 5.x**, asegúrese de consultar primero la documentación de [actualización](https://docs.adobe.com/content/docs/en/aem/6-0/deploy/upgrade.html).

### Almacén de nodos de segmento {#segment-node-store}

El almacén de nodos de segmentos es la base de la implementación TarMK del Adobe en AEM6. Utiliza el PID `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` para la configuración.

>[!CAUTION]
>
>El PID para el almacén de nodos del segmento ha cambiado de `org.apache.jackrabbit.oak.plugins.segment.SegmentNodeStoreService in previous versions` de AEM 6 a `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` en AEM 6.3. Asegúrese de realizar los ajustes de configuración necesarios para reflejar este cambio.

Puede configurar las siguientes opciones:

* `repository.home`:: Ruta al directorio raíz del repositorio en el cual se almacenan los datos relacionados con el repositorio. De forma predeterminada, los archivos de segmentos se almacenan en el directorio `crx-quickstart/segmentstore`.

* `tarmk.size`:: Tamaño máximo de un segmento en MB. El máximo predeterminado es 256 MB.
* `customBlobStore`:: Valor booleano que indica que se utiliza un almacén de datos personalizado. El valor predeterminado es true para AEM versiones 6.3 y posteriores. Antes de AEM 6.3, el valor predeterminado era false.

A continuación se muestra un archivo `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` de muestra:

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### Almacén de nodos de documento {#document-node-store}

El almacén de nodos de documento es la base de AEM implementación de MongoMK. Utiliza el `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService`* *PID. Están disponibles las siguientes opciones de configuración:

* `mongouri`:: El  [](https://docs.mongodb.org/manual/reference/connection-string/) MongoURIrequired para conectarse a la base de datos Mongo. El valor predeterminado es `mongodb://localhost:27017`

* `db`:: Nombre de la base de datos de Mongo. El valor predeterminado es **Oak** ``. However, new AEM 6 installations use **aem-author** ``como nombre de base de datos predeterminado.

* `cache`:: El tamaño de caché en MB. Esto se distribuye entre varias cachés utilizadas en DocumentNodeStore. El valor predeterminado es `256`

* `changesSize`:: Tamaño en MB de colección con límite utilizada en Mongo para almacenar en caché la salida de diferencias. El valor predeterminado es `256`

* `customBlobStore`:: Valor booleano que indica que se utilizará un almacén de datos personalizado. El valor predeterminado es `false`.

A continuación se muestra un archivo `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config` de muestra:

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

Por ejemplo, si el proyecto requiere un gran número de recursos multimedia, almacenarlos en el almacén de datos S3 o File hará que el acceso a ellos sea más rápido que almacenarlos directamente en una base de datos Mongo.

El almacén de datos de archivos ofrece un mejor rendimiento que MongoDB, y las operaciones de backup y restore de Mongo también son más lentas con un gran número de activos.

A continuación se describen los detalles de las diferentes configuraciones y almacenes de datos.

>[!NOTE]
>
>Para habilitar los Almacenes de datos personalizados, debe asegurarse de que `customBlobStore` se establezca en `true` en el archivo de configuración correspondiente del Almacén de nodos ([almacén de nodos de segmentos](/help/sites-deploying/data-store-config.md#segment-node-store) o [almacén de nodos de documento](/help/sites-deploying/data-store-config.md#document-node-store)).

### Almacén de datos de archivo {#file-data-store}

Esta es la implementación de [FileDataStore](https://jackrabbit.apache.org/api/2.8/org/apache/jackrabbit/core/data/FileDataStore.html) presente en Jackrabbit 2. Proporciona una manera de almacenar los datos binarios como archivos normales en el sistema de archivos. Utiliza el PID `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore`.

Estas opciones de configuración están disponibles:

* `repository.home`:: Ruta al directorio raíz del repositorio en el cual se almacenan varios datos relacionados con el repositorio. De forma predeterminada, los archivos binarios se almacenan en el directorio `crx-quickstart/repository/datastore`

* `path`:: Ruta al directorio en el cual se almacenarán los archivos. Si se especifica, tiene prioridad sobre el valor `repository.home`

* `minRecordLength`:: Tamaño mínimo en bytes de un archivo almacenado en el almacén de datos. El contenido binario menor que este valor se colocaría en la línea.

>[!NOTE]
>
>Al utilizar un NAS para almacenar almacenes de datos de archivos compartidos, asegúrese de utilizar solo dispositivos de alto rendimiento para evitar problemas de performance.

## Almacén de datos Amazon S3 {#amazon-s-data-store}

AEM se puede configurar para almacenar datos en Amazon Simple Almacenamiento Service (S3). Utiliza el PID `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` para la configuración.

Para habilitar la funcionalidad del almacén de datos S3, es necesario descargar e instalar un paquete de funciones que contenga el conector del almacén de datos S3. Vaya al [Repositorio de Adobe](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/) y descargue la versión más reciente de las versiones 1.10.x del paquete de funciones (por ejemplo, com.adobe.granite.oak.s3Connector-1.10.0.zip). Además, también debe descargar e instalar el Service Pack de AEM más reciente, tal como se indica en la página [Notas de la versión de AEM 6.5](/help/release-notes/sp-release-notes.md).

>[!NOTE]
>
>Al utilizar AEM con TarMK, los binarios se almacenarán de forma predeterminada en `FileDataStore`. Para utilizar TarMK con el almacén de datos S3, debe realizar un inicio AEM usando el modo de ejecución `crx3tar-nofds`, por ejemplo:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

Una vez descargado, puede instalar y configurar el S3 Connector de la siguiente manera:

1. Extraiga el contenido del archivo zip del paquete de funciones en una carpeta temporal.

1. Vaya a la carpeta temporal y vaya a la siguiente ubicación:

   ```xml
   jcr_root/libs/system/install
   ```

   Copie todo el contenido de la ubicación anterior en `<aem-install>/crx-quickstart/install.`

1. Si AEM ya está configurado para trabajar con el almacenamiento Tar o MongoDB, elimine los archivos de configuración existentes de la carpeta ***&lt;aem-install>**/*crx-quickstart*/*install* antes de continuar. Los archivos que deben eliminarse son:

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Vuelva a la ubicación temporal en la que se ha extraído el paquete de funciones y copie el contenido de la siguiente carpeta:

   * `jcr_root/libs/system/config`

   hasta

   * `<aem-install>/crx-quickstart/install`

   Asegúrese de que sólo copia los archivos de configuración necesarios para la configuración actual. Tanto para un almacén de datos dedicado como para una configuración de almacén de datos compartidos, copie el archivo `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config`.

   >[!NOTE]
   >
   >En una configuración de clúster, realice los pasos anteriores en todos los nodos del clúster uno por uno. Además, asegúrese de utilizar la misma configuración de S3 para todos los nodos.

1. Edite el archivo y agregue las opciones de configuración requeridas por la configuración.
1. Inicio AEM.

### Actualización a una nueva versión del conector 1.10.x S3 {#upgrading-to-a-new-version-of-the-s-connector}

Si necesita actualizar a una nueva versión del conector 1.10.x S3 (por ejemplo, de 1.10.0 a 1.10.4), siga estos pasos:

1. Detenga la instancia de AEM.

1. Vaya a `<aem-install>/crx-quickstart/install/15` en la carpeta de instalación de AEM y realice una copia de seguridad de su contenido.
1. Después de la copia de seguridad, elimine la versión antigua del S3 Connector y sus dependencias eliminando todos los archivos jar de la carpeta `<aem-install>/crx-quickstart/install/15`, por ejemplo:

   * **oak-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**

   >[!NOTE]
   >
   >Los nombres de archivo presentados anteriormente se utilizan únicamente con fines ilustrativos.

1. Descargue la versión más reciente del paquete de funciones 1.8.x del [Repositorio de Adobe](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/).
1. Descomprima el contenido en una carpeta independiente y luego navegue a `jcr_root/libs/system/install/15`.
1. Copie los archivos jar a **&lt;aem-install>**/crx-quickstart/install/15 en la carpeta de instalación de AEM.
1. Inicio AEM y compruebe la funcionalidad del conector.

Puede utilizar el archivo de configuración con las siguientes opciones:

* accessKey: Clave de acceso de AWS.
* secretKey: La clave de acceso secreto de AWS. **Nota:** Alternativamente, se pueden utilizar las funciones  [de ](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) IAM para la autenticación. Si está utilizando funciones de IAM, ya no necesita especificar `accessKey` y `secretKey`.

* s3Bucket: El nombre del bloque.
* s3Region: La región del cubo.
* path: Ruta del almacén de datos. El valor predeterminado es **&lt;carpeta de instalación de AEM>/repositorio/almacén de datos**
* minRecordLength: El tamaño mínimo de un objeto que debe almacenarse en el almacén de datos. El valor mínimo/predeterminado es **16 KB.**
* maxCachedBinarySize: Los binarios con un tamaño menor o igual que este tamaño se almacenarán en la memoria caché. El tamaño está en bytes. El valor predeterminado es **17408 **(17 KB).

* cacheSize: El tamaño de la caché. El valor se especifica en bytes. El valor predeterminado es **64 GB**.
* secret: Solo se debe utilizar si se utiliza replicación sin binarios para la configuración del almacén de datos compartido.
* stagingSplitPerpercentage: El porcentaje de tamaño de caché configurado para utilizarse en cargas asincrónicas de ensayo. El valor predeterminado es **10**.
* uploadThwords: Número de subprocesos de carga que se utilizan para cargas asincrónicas. El valor predeterminado es **10**.
* stagingPurgeInterval: El intervalo en segundos para la depuración de cargas terminadas desde la caché de ensayo. El valor predeterminado es **300** segundos (5 minutos).
* stagingRetryInterval: Intervalo de reintentos en segundos para cargas fallidas. El valor predeterminado es **600** segundos (10 minutos).

### Opciones de región de bucket {#bucket-region-options}

<table>
 <tbody>
  <tr>
   <td>US Standard</td>
   <td><code>us-standard</code></td>
  </tr>
  <tr>
   <td>Estados Unidos Occidental</td>
   <td><code>us-west-2</code></td>
  </tr>
  <tr>
   <td>Estados Unidos Occidental (California del Norte)</td>
   <td><code>us-west-1</code></td>
  </tr>
  <tr>
   <td>UE (Irlanda)<br /> </td>
   <td><code>EU</code></td>
  </tr>
  <tr>
   <td>Asia-Pacífico (Singapur)<br /> </td>
   <td><code>ap-southeast-1</code></td>
  </tr>
  <tr>
   <td>Asia-Pacífico (Sídney)<br /> </td>
   <td><code>ap-southeast-2</code></td>
  </tr>
  <tr>
   <td>Asia-Pacífico (Tokio)</td>
   <td><code>ap-northeast-1</code></td>
  </tr>
  <tr>
   <td>Sudamérica (São Paulo)<br /> </td>
   <td><code>sa-east-1</code></td>
  </tr>
 </tbody>
</table>

**Almacenamiento en caché de DataStore**

>[!NOTE]
>
>Las implementaciones de DataStore de `S3DataStore`, `CachingFileDataStore` y `AzureDataStore` admiten el almacenamiento en caché del sistema de archivos local. La implementación `CachingFileDataStore` resulta útil cuando DataStore está en NFS (Network File System).


Al realizar la actualización desde una implementación de caché anterior (anterior a Oak 1.6), existe una diferencia en la estructura del directorio de caché del sistema de archivos local. En la antigua estructura de caché, tanto los archivos descargados como los cargados se colocaron directamente debajo de la ruta de la caché. La nueva estructura divide las descargas y las carga y las almacena en dos directorios denominados `upload` y `download` en la ruta de la memoria caché. El proceso de actualización debe ser fluido y cualquier carga pendiente debe programarse para cargarse y cualquier archivo descargado anteriormente en la caché se colocará en la caché al inicializarse.

También puede actualizar la caché sin conexión mediante el comando `datastorecacheupgrade` de oak-run. Para obtener más información sobre cómo ejecutar el comando, consulte el [readme](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md) para obtener información sobre el módulo de ejecución de roble.

La caché tiene un límite de tamaño y se puede configurar usando el parámetro cacheSize.

**Descargas**

Se buscará en la caché local el registro del archivo o blob solicitado antes de acceder a él desde DataStore. Cuando la caché excede el límite configurado (consulte el parámetro `cacheSize`) al agregar un archivo a la caché, algunos de los archivos se desalojarán para recuperar espacio.

**Carga asincrónica**

La caché admite cargas asincrónicas en DataStore. Los archivos se escalonan localmente, en la caché (en el sistema de archivos) y en un inicio de trabajo asincrónico para cargar el archivo. El número de cargas asincrónicas está limitado por el tamaño de la caché de ensayo. El tamaño de la caché de ensayo se configura mediante el parámetro `stagingSplitPercentage`. Este parámetro define el porcentaje de tamaño de caché que se utilizará para la caché de ensayo. Además, el porcentaje de caché disponible para descargas se calcula como **(100 - `stagingSplitPercentage`) *`cacheSize`**.

Las cargas asincrónicas son de varios subprocesos y el número de subprocesos se configura mediante el parámetro `uploadThreads`.

Los archivos se mueven a la caché de descarga principal una vez finalizadas las cargas. Cuando el tamaño de caché de ensayo supera su límite, los archivos se cargan sincrónicamente en DataStore hasta que se completen las cargas asincrónicas anteriores y vuelva a haber espacio disponible en la caché de ensayo. Los archivos cargados se eliminan del área de ensayo mediante un trabajo periódico cuyo intervalo está configurado por el parámetro `stagingPurgeInterval`.

Las cargas fallidas (por ejemplo, debido a una interrupción de la red) se colocan en una cola de reintentos y se vuelven a intentar periódicamente. El intervalo de reintentos se configura mediante `stagingRetryInterval parameter`.

#### Configuración de la replicación sin binarios con Amazon S3 {#configuring-binaryless-replication-with-amazon-s}

Para configurar la replicación sin binarios con S3, se requieren los siguientes pasos:

1. Instale las instancias de creación y publicación y asegúrese de que se inician correctamente.
1. Vaya a la configuración del agente de replicación, abriendo una página en *https://localhost:4502/etc/replication/agents.author/publish.html*.
1. Pulse el botón **Editar** en la sección **Configuración**.
1. Cambie la opción de tipo **Serialización** a **Binary less**.

1. Añada el parámetro &quot; `binaryless`= `true`&quot; en el URI de transporte. Después del cambio, el URI debería tener un aspecto similar al siguiente:

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. Reinicie todas las instancias de creación y publicación para que los cambios surtan efecto.

#### Creación de un clúster con S3 y MongoDB {#creating-a-cluster-using-s-and-mongodb}

1. Descomprima el inicio rápido de CQ con el siguiente comando:

   `java -jar cq-quickstart.jar -unpack`

1. Después de desempaquetar AEM, cree una carpeta dentro del directorio de instalación *crx-quickstart*/*install*.

1. Cree estos dos archivos dentro de la carpeta `crx-quickstart`:

   * *org.apache.jackrabbit.oak.plugins.documento.DocumentNodeStoreService*.*config*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*.*config*

   Después de crear los archivos, agregue las opciones de configuración según sea necesario.

1. Instale los dos paquetes necesarios para el almacén de datos S3 como se explica anteriormente.
1. Asegúrese de que MongoDB esté instalado y de que se esté ejecutando una instancia de `mongod`.
1. Inicio AEM con el siguiente comando:

   `java -Xmx1024m -XX:MaxPermSize=256M -jar cq-quickstart.jar -r crx3,crx3mongo`

1. Repita los pasos del 1 al 4 para la segunda instancia de AEM.
1. Inicio de la segunda instancia de AEM.

#### Configuración de un almacén de datos compartido {#configuring-a-shared-data-store}

1. En primer lugar, cree el archivo de configuración del almacén de datos en cada instancia necesaria para compartir el almacén de datos:

   * Si utiliza un `FileDataStore`, cree un archivo denominado `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` y colóquelo en la carpeta `<aem-install>/crx-quickstart/install`.

   * Si utiliza S3 como almacén de datos, cree un archivo denominado o `rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` en la carpeta `<aem-install>/crx-quickstart/install` como se indica más arriba.

1. Modifique los archivos de configuración del almacén de datos en cada instancia para que apunten al mismo almacén de datos. Para obtener más información, consulte [este artículo](/help/sites-deploying/data-store-config.md#data-store-configurations).
1. Si la instancia se ha clonado desde un servidor existente, debe eliminar la `clusterId` de la nueva instancia utilizando la herramienta de ejecución de roble más reciente mientras el repositorio está sin conexión. El comando que necesita ejecutar es:

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >Si se configura un almacén de nodos de segmento, se debe especificar la ruta del repositorio. De forma predeterminada, la ruta es `<aem-install-folder>/crx-quickstart/repository/segmentstore.` Si se configura un almacén de nodos de Documento, puede utilizar un URI de cadena de conexión [Mongo](https://docs.mongodb.org/manual/reference/connection-string/).

   >[!NOTE]
   >
   >La herramienta Oak-run se puede descargar desde esta ubicación:
   >
   >
   >[https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)
   >
   >
   >Tenga en cuenta que es necesario utilizar diferentes versiones de la herramienta en función de la versión de Oak que utilice con la instalación de AEM. Compruebe la lista de requisitos de versión que aparece a continuación antes de utilizar la herramienta:
   >
   >
   >
   >    * Para las versiones Oak **1.2.x** utilice Oak-run **1.2.12 o posterior**
   >    * Para las versiones Oak **más recientes que las anteriores**, utilice la versión de Oak-run que coincida con el núcleo Oak de su instalación AEM.


1. Por último, valide la configuración. Para ello, debe buscar un archivo único agregado al almacén de datos por cada repositorio que lo comparte. El formato de los archivos es `repository-[UUID]`, donde el UUID es un identificador único de cada repositorio individual.

   Por lo tanto, una configuración adecuada debe tener tantos archivos únicos como repositorios que compartan el almacén de datos.

   Los archivos se almacenan de forma diferente, según el almacén de datos:

   * Para `FileDataStore` los archivos se crean en la ruta raíz de la carpeta del almacén de datos.
   * Para `S3DataStore` los archivos se crean en el bucket S3 configurado en la carpeta `META`.

## Almacén de datos de Azure {#azure-data-store}

AEM se puede configurar para almacenar datos en el servicio de almacenamiento de Microsoft Azure. Utiliza el PID `org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` para la configuración.

Para habilitar la funcionalidad del almacén de datos de Azure, es necesario descargar e instalar un paquete de funciones que contenga el conector de Azure. Vaya al [Repositorio de Adobe](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.azureblobconnector/) y descargue la versión más reciente de las versiones 1.6.x del paquete de funciones (por ejemplo, com.adobe.granite.oak.azureblobConnector-1.6.3.zip).

>[!NOTE]
>
>Al utilizar AEM con TarMK, los binarios se almacenarán de forma predeterminada en FileDataStore. Para utilizar TarMK con el Almacén de datos de Azure, debe realizar un inicio AEM usando el modo de ejecución `crx3tar-nofds`, por ejemplo:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

Una vez descargado, puede instalar y configurar el conector de Azure de la siguiente manera:

1. Extraiga el contenido del archivo zip del paquete de funciones en una carpeta temporal.

1. Vaya a la carpeta temporal y copie el contenido de `jcr_root/libs/system/install` en la carpeta `<aem-install>crx-quickstart/install`.
1. Si AEM ya está configurado para trabajar con el almacenamiento Tar o MongoDB, elimine los archivos de configuración existentes de la carpeta `/crx-quickstart/install` antes de continuar. Los archivos que deben eliminarse son:

   Para MongoMK:

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   Para TarMK:

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Vuelva a la ubicación temporal en la que se ha extraído el paquete de funciones y copie el contenido de `jcr_root/libs/system/config` en la carpeta `<aem-install>/crx-quickstart/install`.
1. Edite el archivo de configuración y agregue las opciones de configuración requeridas por la configuración.
1. Inicio AEM.

Puede utilizar el archivo de configuración con las siguientes opciones:

* azureSas=&quot;&quot;: En la versión 1.6.3 del conector, se agregó compatibilidad con la firma Azure Shared Access (SAS). **Si las credenciales SAS y almacenamiento existen en el archivo de configuración, SAS tiene prioridad.** Para obtener más información sobre SAS, consulte la documentación  [oficial](https://docs.microsoft.com/en-us/azure/storage/common/storage-dotnet-shared-access-signature-part-1). Asegúrese de que el carácter &#39;=&#39; tiene un carácter de escape como &#39;\=&#39;.

* azureBlobEndpoint=&quot;&quot;: Extremo de blob de Azure. Por ejemplo, https://&lt;cuenta-almacenamiento>.blob.core.windows.net.
* accessKey=&quot;&quot;: El nombre de la cuenta de almacenamiento. Para obtener más información sobre las credenciales de autenticación de Microsoft Azure, consulte la [documentación oficial](https://azure.microsoft.com/en-us/documentation/articles/storage-create-storage-account).

* secretKey=&quot;&quot;: La clave de acceso de almacenamiento. Asegúrese de que el carácter &#39;=&#39; tiene un carácter de escape como &#39;\=&#39;.
* contenedor=&quot;&quot;: El nombre del contenedor de almacenamiento blob de Microsoft Azure. El contenedor es una agrupación de un conjunto de blobs. Para obtener más información, lea la [documentación oficial](https://msdn.microsoft.com/en-us/library/dd135715.aspx).
* maxConnections=&quot;&quot;: Número simultáneo de solicitudes simultáneas por operación. El valor predeterminado es 1.
* maxErrorRetry=&quot;&quot;: Número de reintentos por solicitud. El valor predeterminado es 3.
* socketTimeout=&quot;&quot;: Intervalo de tiempo de espera, en milisegundos, utilizado para la solicitud. El valor predeterminado es 5 minutos.

Además de la configuración anterior, también se pueden configurar las siguientes opciones:

* path: Ruta del almacén de datos. El valor predeterminado es `<aem-install>/repository/datastore.`
* RecordLength: El tamaño mínimo de un objeto que debe almacenarse en el almacén de datos. El valor predeterminado es 16 KB.
* maxCachedBinarySize: Los binarios con un tamaño menor o igual que este tamaño se almacenarán en la memoria caché. El tamaño está en bytes. El valor predeterminado es 17408 (17 KB).
* cacheSize: El tamaño de la caché. El valor se especifica en bytes. El valor predeterminado es 64 GB.
* secret: Solo se debe utilizar si se utiliza replicación sin binarios para la configuración del almacén de datos compartido.
* stagingSplitPerpercentage: El porcentaje de tamaño de caché configurado para utilizarse en cargas asincrónicas de ensayo. El valor predeterminado es 10.
* uploadThwords: Número de subprocesos de carga que se utilizan para cargas asincrónicas. El valor predeterminado es 10.
* stagingPurgeInterval: El intervalo en segundos para la depuración de cargas terminadas desde la caché de ensayo. El valor predeterminado es 300 segundos (5 minutos).
* stagingRetryInterval: Intervalo de reintentos en segundos para cargas fallidas. El valor predeterminado es 600 segundos (10 minutos).

>[!NOTE]
>
>Todas las opciones de configuración deben estar entre comillas, por ejemplo:

```shell
accessKey="ASDASDERFAERAER"
secretKey="28932hfjlkwdo8fufsdfas\=\="
```

## Recopilación de elementos no utilizados del almacén de datos {#data-store-garbage-collection}

El proceso de recolección de elementos no utilizados del almacén de datos se utiliza para eliminar los archivos no utilizados del almacén de datos, lo que libera espacio valioso en el disco durante el proceso.

Puede ejecutar la recopilación de elementos no utilizados del almacén de datos mediante:

1. Ir a la consola JMX ubicada en *https://&lt;serveraddress:port>/system/console/jmx*
1. Buscando **RepositoryManagement.** Una vez que encuentre el MBean del Administrador de repositorios, haga clic en él para ver las opciones disponibles.
1. Desplácese hasta el final de la página y haga clic en el vínculo **startDataStoreGC(boolean markOnly)**.
1. En el siguiente cuadro de diálogo, escriba `false` para el parámetro `markOnly` y haga clic en **Invocar**:

   ![chlimage_1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >El parámetro `markOnly` significa si la fase de barrido de la recolección de elementos no utilizados se ejecutará o no.

## Recopilación de elementos no utilizados del almacén de datos para un almacén de datos compartido {#data-store-garbage-collection-for-a-shared-data-store}

>[!NOTE]
>
>Al realizar la recopilación de elementos no utilizados en una configuración de almacén de datos agrupados o compartidos (con Mongo o Segment Tar), el registro puede mostrar advertencias sobre la imposibilidad de eliminar determinados identificadores de blob. Esto sucede porque otros clústeres o nodos compartidos que no tienen información sobre las eliminaciones de ID vuelven a hacer referencia a los ID de blob eliminados en una colección de elementos no utilizados anterior. Como resultado, cuando se realiza la recolección de elementos no utilizados, registra una advertencia cuando intenta eliminar un ID que ya se eliminó en la última ejecución. Este comportamiento no afecta al rendimiento ni a la funcionalidad.

Con versiones más recientes de AEM, la recopilación de elementos no utilizados del almacén de datos también se puede ejecutar en almacenes de datos compartidos por más de un repositorio. Para poder ejecutar la recopilación de elementos no utilizados del almacén de datos en un almacén de datos compartido, lleve a cabo los siguientes pasos:

1. Asegúrese de que todas las tareas de mantenimiento configuradas para la recopilación de elementos no utilizados del almacén de datos estén desactivadas en todas las instancias del repositorio que compartan el almacén de datos.
1. Ejecute los pasos mencionados en [Recopilación de datos binarios](/help/sites-deploying/data-store-config.md#data-store-garbage-collection) individualmente en **todas las instancias del repositorio** que compartan el almacén de datos. Sin embargo, asegúrese de introducir `true` para el parámetro `markOnly` antes de hacer clic en el botón Invocar:

   ![chlimage_1-10](assets/chlimage_1-10.png)

1. Después de completar el procedimiento anterior en todas las instancias, vuelva a ejecutar la recopilación de elementos no utilizados del almacén de datos de **cualquiera** de las instancias:

   1. Vaya a la consola JMX y seleccione el grano del administrador de repositorios.
   1. Haga clic en el vínculo **Haga clic en startDataStoreGC(boolean markOnly)**.
   1. En el siguiente cuadro de diálogo, vuelva a introducir `false` para el parámetro `markOnly`.

   De este modo, se recopilarán todos los archivos encontrados con la fase de marca utilizada anteriormente y se eliminarán los demás que no se utilicen del almacén de datos.

