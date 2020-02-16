---
title: Elementos de almacenamiento en AEM 6.5
seo-title: Elementos de almacenamiento en AEM 6.5
description: Obtenga información sobre las implementaciones de almacenamiento de nodos disponibles en AEM 6.5 y cómo mantener el repositorio.
seo-description: Obtenga información sobre las implementaciones de almacenamiento de nodos disponibles en AEM 6.5 y cómo mantener el repositorio.
uuid: 3b018830-c42e-48e0-9b6f-cd230b02d914
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0aa2c22f-32bb-4e50-8328-63ed73c0f19e
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6

---


# Elementos de almacenamiento en AEM 6.5{#storage-elements-in-aem}

En este artículo trataremos:

* [Información general sobre el almacenamiento en AEM 6](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [Mantenimiento del repositorio](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## Información general sobre el almacenamiento en AEM 6 {#overview-of-storage-in-aem}

Uno de los cambios más importantes en AEM 6 son las innovaciones a nivel de repositorio.

Actualmente, hay dos implementaciones de almacenamiento de nodos disponibles en AEM6: Almacenamiento de etiquetas y almacenamiento MongoDB.

### Almacenamiento de información de etiquetas {#tar-storage}

#### Ejecución de una instancia de AEM recién instalada con Almacenamiento de la barra {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>El PID para el almacén de nodos del segmento ha cambiado de org.apache.jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService en versiones anteriores de AEM 6 a org.apache.jackrabbit.oak.segment.SegmentNodeStoreService en AEM 6.3. Asegúrese de realizar los ajustes de configuración necesarios para reflejar este cambio.

De forma predeterminada, AEM 6 utiliza el almacenamiento de etiquetas para almacenar nodos y binarios, mediante las opciones de configuración predeterminadas. Para configurar manualmente su configuración de almacenamiento, siga el procedimiento siguiente:

1. Descargue el tarro de inicio rápido de AEM 6 y colóquelo en una nueva carpeta.
1. Desempaquetar AEM ejecutando:

   `java -jar cq-quickstart-6.jar -unpack`

1. Cree una carpeta con el nombre `crx-quickstart\install` en el directorio de instalación.

1. Cree un archivo llamado `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg` en la carpeta recién creada.

1. Edite el archivo y defina las opciones de configuración. Las siguientes opciones están disponibles para el almacén de nodos de segmento, que es la base de la implementación de almacenamiento de información de etiquetas de AEM:

   * `repository.home`:: Ruta al directorio raíz del repositorio en el cual se almacenan varios datos relacionados con el repositorio. De forma predeterminada, los archivos de segmentos se almacenarían en el directorio crx-quickstart/segmentstore.
   * `tarmk.size`:: Tamaño máximo de un segmento en MB. El valor predeterminado es 256 MB.

1. Inicie AEM.

### Almacenamiento de Mongo {#mongo-storage}

#### Ejecución de una instancia de AEM recién instalada con Mongo Storage {#running-a-freshly-installed-aem-instance-with-mongo-storage}

AEM 6 se puede configurar para que se ejecute con el almacenamiento MongoDB siguiendo el procedimiento siguiente:

1. Descargue el tarro de inicio rápido de AEM 6 y colóquelo en una nueva carpeta.
1. Desempaquetar AEM ejecutando el siguiente comando:

   `java -jar cq-quickstart-6.jar -unpack`

1. Asegúrese de que MongoDB está instalado y de que `mongod` se está ejecutando una instancia de. Para obtener más información, consulte [Instalación de MongoDB](https://docs.mongodb.org/manual/installation/).
1. Cree una carpeta con el nombre `crx-quickstart\install` en el directorio de instalación.
1. Configure el almacén de nodos creando un archivo de configuración con el nombre de la configuración que desee utilizar en el `crx-quickstart\install` directorio.

   El almacén de nodos de documentos (que es la base de la implementación de almacenamiento MongoDB de AEM) utiliza un archivo denominado `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`

1. Edite el archivo y defina las opciones de configuración. Las opciones disponibles son las siguientes:

   * `mongouri`:: El [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) necesario para conectarse a la base de datos de Mongo. El valor predeterminado es `mongodb://localhost:27017`
   * `db`:: Nombre de la base de datos de Mongo. De forma predeterminada, las nuevas instalaciones de AEM 6 utilizan **aem-author** como nombre de base de datos.
   * `cache`:: El tamaño de caché en MB. Esto se distribuye entre varias cachés utilizadas en DocumentNodeStore. El valor predeterminado es 256.
   * `changesSize`:: Tamaño en MB de colección con límite utilizada en Mongo para almacenar en caché la salida de diferencias. El valor predeterminado es 256.
   * `customBlobStore`:: Valor booleano que indica que se utilizará un almacén de datos personalizado. El valor predeterminado es false.

1. Cree un archivo de configuración con el PID del almacén de datos que desee utilizar y edite el archivo para configurar las opciones de configuración. Para obtener más información, consulte [Configuración de almacenes de nodos y almacenes](/help/sites-deploying/data-store-config.md)de datos.

1. Inicie el archivo AEM 6 con un servidor de almacenamiento MongoDB ejecutando:

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   Dónde **`-r`** está el modo de ejecución back-end. En este ejemplo, comenzará con la compatibilidad con MongoDB.

#### Desactivación de páginas grandes transparentes {#disabling-transparent-huge-pages}

Red Hat Linux utiliza un algoritmo de administración de memoria llamado Transparent Enorme Pages (THP). Mientras AEM realiza lecturas y escrituras específicas, THP está optimizado para operaciones de gran tamaño. Debido a esto, se recomienda desactivar THP tanto en almacenamiento Tar como en almacenamiento Mongo. Para deshabilitar el algoritmo, siga estos pasos:

1. Abra el `/etc/grub.conf` archivo en el editor de texto que desee.
1. Agregue la siguiente línea al archivo **grub.conf** :

   ```
   transparent_hugepage=never
   ```

1. Por último, compruebe si la configuración ha surtido efecto al ejecutar:

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   Si THP está deshabilitado, el resultado del comando anterior debería ser:

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>Además, también puede consultar los siguientes recursos:
>
>* Para obtener más información acerca de las páginas transparentes y grandes en Red Hat Linux, consulte este [artículo](https://access.redhat.com/solutions/46111).
>* Para obtener sugerencias de ajuste para Linux, consulte este [artículo](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).
>



## Mantenimiento del repositorio {#maintaining-the-repository}

Cada actualización al repositorio crea una nueva revisión de contenido. Como resultado, con cada actualización crece el tamaño del repositorio. Para evitar el crecimiento incontrolado del repositorio, es necesario limpiar las antiguas revisiones para liberar recursos de disco. Esta funcionalidad de mantenimiento se denomina Limpieza de revisión. El mecanismo de limpieza de revisión recuperará espacio en disco eliminando datos obsoletos del repositorio. Para obtener más información sobre la limpieza de revisión, lea la página [Limpieza de](/help/sites-deploying/revision-cleanup.md)revisión.
