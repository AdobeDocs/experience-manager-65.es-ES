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
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 1%

---


# Elementos de almacenamiento en AEM 6.5{#storage-elements-in-aem}

En este artículo trataremos:

* [Visión general del Almacenamiento en el AEM 6](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [Mantenimiento del repositorio](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## Visión general del Almacenamiento en el AEM 6 {#overview-of-storage-in-aem}

Uno de los cambios más importantes del AEM 6 son las innovaciones a nivel de repositorio.

Actualmente, hay dos implementaciones de almacenamiento de nodos disponibles en AEM6: Almacenamiento Tar y almacenamiento MongoDB.

### Almacenamiento Tar {#tar-storage}

#### Ejecución de una instancia de AEM recién instalada con el Almacenamiento Tar {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>El PID para el almacén de nodos del segmento ha cambiado de org.apache.jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService en versiones anteriores de AEM 6 a org.apache.jackrabbit.oak.segment.SegmentNodeStoreService en AEM 6.3. Asegúrese de realizar los ajustes de configuración necesarios para reflejar este cambio.

De forma predeterminada, AEM 6 utiliza el almacenamiento Tar para almacenar nodos y binarios, utilizando las opciones de configuración predeterminadas. Para configurar manualmente su configuración de almacenamiento, siga el procedimiento siguiente:

1. Descargue el tarro de inicio rápido AEM 6 y colóquelo en una nueva carpeta.
1. Desempaquetar AEM ejecutando:

   `java -jar cq-quickstart-6.jar -unpack`

1. Cree una carpeta con el nombre `crx-quickstart\install` en el directorio de instalación.

1. Cree un archivo denominado `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg` en la carpeta recién creada.

1. Edite el archivo y defina las opciones de configuración. Las siguientes opciones están disponibles para el almacén de nodos de segmento, que es la base de AEM implementación de almacenamiento de etiquetas:

   * `repository.home`:: Ruta al directorio raíz del repositorio en el cual se almacenan varios datos relacionados con el repositorio. De forma predeterminada, los archivos de segmentos se almacenarían en el directorio crx-quickstart/segmentstore.
   * `tarmk.size`:: Tamaño máximo de un segmento en MB. El valor predeterminado es 256 MB.

1. Inicio AEM.

### Almacenamiento Mongo {#mongo-storage}

#### Ejecución de una instancia de AEM recién instalada con el Almacenamiento Mongo {#running-a-freshly-installed-aem-instance-with-mongo-storage}

AEM 6 puede configurarse para ejecutarse con el almacenamiento MongoDB siguiendo el procedimiento siguiente:

1. Descargue el tarro de inicio rápido AEM 6 y colóquelo en una nueva carpeta.
1. Desempaquetar AEM ejecutando el siguiente comando:

   `java -jar cq-quickstart-6.jar -unpack`

1. Asegúrese de que MongoDB está instalado y de que se está ejecutando una instancia de `mongod`. Para obtener más información, consulte [Instalación de MongoDB](https://docs.mongodb.org/manual/installation/).
1. Cree una carpeta con el nombre `crx-quickstart\install` en el directorio de instalación.
1. Configure el almacén de nodos creando un archivo de configuración con el nombre de la configuración que desee utilizar en el directorio `crx-quickstart\install`.

   El almacén de nodos de Documento (que es la base para AEM implementación de almacenamiento de MongoDB) utiliza un archivo llamado `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`

1. Edite el archivo y defina las opciones de configuración. Las opciones disponibles son las siguientes:

   * `mongouri`:: El  [](https://docs.mongodb.org/manual/reference/connection-string/) MongoURIrequired para conectarse a la base de datos Mongo. El valor predeterminado es `mongodb://localhost:27017`
   * `db`:: Nombre de la base de datos de Mongo. De forma predeterminada, las nuevas instalaciones de AEM 6 utilizan **aem-author** como nombre de la base de datos.
   * `cache`:: El tamaño de caché en MB. Esto se distribuye entre varias cachés utilizadas en DocumentNodeStore. El valor predeterminado es 256.
   * `changesSize`:: Tamaño en MB de colección con límite utilizada en Mongo para almacenar en caché la salida de diferencias. El valor predeterminado es 256.
   * `customBlobStore`:: Valor booleano que indica que se utilizará un almacén de datos personalizado. El valor predeterminado es false.

1. Cree un archivo de configuración con el PID del almacén de datos que desee utilizar y edite el archivo para configurar las opciones de configuración. Para obtener más información, consulte [Configuración de almacenes de nodos y almacenes de datos](/help/sites-deploying/data-store-config.md).

1. Inicio el tarro de AEM 6 con un fondo de almacenamiento MongoDB ejecutando:

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   Donde **`-r`** es el modo de ejecución back-end. En este ejemplo, inicio con la compatibilidad con MongoDB.

#### Desactivación de páginas grandes transparentes {#disabling-transparent-huge-pages}

Red Hat Linux utiliza un algoritmo de administración de memoria llamado Transparent Enorme Pages (THP). Mientras AEM realiza lecturas y escrituras específicas, THP está optimizado para operaciones de gran tamaño. Debido a esto, se recomienda desactivar THP tanto en Tar como en el almacenamiento Mongo. Para deshabilitar el algoritmo, siga estos pasos:

1. Abra el archivo `/etc/grub.conf` en el editor de texto que desee.
1. Añada la línea siguiente en el archivo **grub.conf**:

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

Cada actualización al repositorio crea una nueva revisión de contenido. Como resultado, con cada actualización crece el tamaño del repositorio. Para evitar el crecimiento incontrolado del repositorio, es necesario limpiar las antiguas revisiones para liberar recursos de disco. Esta funcionalidad de mantenimiento se denomina Limpieza de revisión. El mecanismo de limpieza de revisión recuperará espacio en disco eliminando datos obsoletos del repositorio. Para obtener más información sobre la limpieza de revisión, lea la [página de limpieza de revisión](/help/sites-deploying/revision-cleanup.md).
