---
title: Elementos de almacenamiento en AEM 6.5
seo-title: Storage Elements in AEM 6.5
description: Obtenga información sobre las implementaciones de almacenamiento de nodos disponibles en AEM 6.5 y cómo mantener el repositorio.
seo-description: Learn about the node storage implementations available in AEM 6.5 and how to maintain the repository.
uuid: 3b018830-c42e-48e0-9b6f-cd230b02d914
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0aa2c22f-32bb-4e50-8328-63ed73c0f19e
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
exl-id: 52437eb5-f9fb-4945-9950-5a1562fe878d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 1%

---

# Elementos de almacenamiento en AEM 6.5{#storage-elements-in-aem}

En este artículo trataremos:

* [Descripción general del almacenamiento en AEM 6](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [Mantenimiento del repositorio](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## Descripción general del almacenamiento en AEM 6 {#overview-of-storage-in-aem}

Uno de los cambios más importantes en el AEM 6 son las innovaciones a nivel de repositorio.

Actualmente, hay dos implementaciones de almacenamiento de nodos disponibles en AEM6: Almacenamiento Tar y almacenamiento MongoDB.

### Almacenamiento de Tar {#tar-storage}

#### Ejecución de una instancia de AEM recién instalada con Almacenamiento de Tar {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>El PID para el almacén de nodos del segmento ha cambiado de org.apache.jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService en versiones anteriores de AEM 6 a org.apache.jackrabbit.oak.segment.SegmentNodeStoreService en AEM 6.3. Asegúrese de realizar los ajustes de configuración necesarios para reflejar este cambio.

De forma predeterminada, AEM 6 utiliza el almacenamiento Tar para almacenar nodos y binarios, utilizando las opciones de configuración predeterminadas. Para configurar manualmente su configuración de almacenamiento, siga el siguiente procedimiento:

1. Descargue el tarro de inicio rápido AEM 6 y colóquelo en una carpeta nueva.
1. Desempaquete AEM ejecutando:

   `java -jar cq-quickstart-6.jar -unpack`

1. Crear una carpeta con el nombre `crx-quickstart\install` en el directorio de instalación.

1. Cree un archivo llamado `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg` en la carpeta recién creada.

1. Edite el archivo y establezca las opciones de configuración. Las siguientes opciones están disponibles para el almacén de nodos de segmento, que es la base de AEM implementación de almacenamiento de Tar:

   * `repository.home`: Ruta al inicio del repositorio donde se almacenan varios datos relacionados con el repositorio. De forma predeterminada, los archivos de segmento se almacenarían en el directorio crx-quickstart/segmentstore.
   * `tarmk.size`: Tamaño máximo de un segmento en MB. El valor predeterminado es 256 MB.

1. Inicie AEM.

### Almacenamiento de Mongo {#mongo-storage}

#### Ejecución de una instancia de AEM recién instalada con Mongo Storage {#running-a-freshly-installed-aem-instance-with-mongo-storage}

AEM 6 se puede configurar para que se ejecute con el almacenamiento MongoDB siguiendo el siguiente procedimiento:

1. Descargue el tarro de inicio rápido AEM 6 y colóquelo en una carpeta nueva.
1. Desempaquete AEM ejecutando el siguiente comando:

   `java -jar cq-quickstart-6.jar -unpack`

1. Asegúrese de que MongoDB esté instalado y que haya una instancia de `mongod` se está ejecutando. Para obtener más información, consulte [Instalación de MongoDB](https://docs.mongodb.org/manual/installation/).
1. Crear una carpeta con el nombre `crx-quickstart\install` en el directorio de instalación.
1. Configure el almacén de nodos creando un archivo de configuración con el nombre de la configuración que desea utilizar en el `crx-quickstart\install` directorio.

   El almacén de nodos de documentos (que es la base de AEM implementación de almacenamiento MongoDB) utiliza un archivo denominado `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`

1. Edite el archivo y configure las opciones de configuración. Las opciones disponibles son las siguientes:

   * `mongouri`: La variable [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) necesario para conectarse a la base de datos Mongo. El valor predeterminado es `mongodb://localhost:27017`
   * `db`: Nombre de la base de datos de Mongo. De forma predeterminada, las nuevas instalaciones AEM 6 utilizan **aem-author** como nombre de la base de datos.
   * `cache`: El tamaño de caché en MB. Esto se distribuye entre varias cachés utilizadas en DocumentNodeStore. El valor predeterminado es 256.
   * `changesSize`: Tamaño en MB de colección restringida utilizada en Mongo para almacenar en caché la salida diff. El valor predeterminado es 256.
   * `customBlobStore`: Valor booleano que indica que se utilizará un almacén de datos personalizado. El valor predeterminado es false.

1. Cree un archivo de configuración con el PID del almacén de datos que desea usar y edite el archivo para establecer las opciones de configuración. Para obtener más información, consulte [Configuración de almacenes de nodos y almacenes de datos](/help/sites-deploying/data-store-config.md).

1. Inicie el AEM 6 jar con un back-end de almacenamiento MongoDB ejecutando:

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   Donde **`-r`** es el modo de ejecución back-end. En este ejemplo, comenzará con la compatibilidad con MongoDB.

#### Desactivación de páginas grandes transparentes {#disabling-transparent-huge-pages}

Red Hat Linux utiliza un algoritmo de administración de memoria llamado Transparent Huge Pages (THP). Mientras AEM realiza lecturas y escrituras específicas, THP está optimizado para operaciones grandes. Debido a esto, se recomienda deshabilitar THP tanto en el almacenamiento Tar como en el de Mongo. Para deshabilitar el algoritmo, siga estos pasos:

1. Abra el `/etc/grub.conf` en el editor de texto de su elección.
1. Añada la línea siguiente al **grub.conf** archivo:

   ```
   transparent_hugepage=never
   ```

1. Finalmente, compruebe si la configuración se ha aplicado ejecutando:

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
>* Para obtener más información acerca de Transparent Huge Pages en Red Hat Linux, vea esto [article](https://access.redhat.com/solutions/46111).
>* Para obtener sugerencias de ajuste de Linux, consulte esta [article](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).
>


## Mantenimiento del repositorio {#maintaining-the-repository}

Cada actualización del repositorio crea una nueva revisión de contenido. Como resultado, con cada actualización, el tamaño del repositorio crece. Para evitar el crecimiento incontrolado del repositorio, es necesario limpiar las viejas revisiones para liberar recursos de disco. Esta funcionalidad de mantenimiento se denomina Limpieza de revisión. El mecanismo de limpieza de revisión recuperará espacio en disco eliminando datos obsoletos del repositorio. Para obtener más información sobre la limpieza de revisión, lea la [Página de limpieza de revisión](/help/sites-deploying/revision-cleanup.md).
