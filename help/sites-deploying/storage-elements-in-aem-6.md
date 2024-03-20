---
title: AEM Elementos de almacenamiento en 6.5
description: AEM Obtenga información acerca de las implementaciones de almacenamiento de nodos disponibles en la versión 6.5 de y cómo mantener el repositorio.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
exl-id: 52437eb5-f9fb-4945-9950-5a1562fe878d
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---

# AEM Elementos de almacenamiento en 6.5{#storage-elements-in-aem}

Este artículo trata sobre lo siguiente:

* [AEM Información general sobre el almacenamiento en el 6](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [Mantenimiento del repositorio](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## AEM Información general sobre el almacenamiento en el 6 {#overview-of-storage-in-aem}

AEM Uno de los cambios más importantes en la 6 son las innovaciones a nivel de repositorio.

AEM Actualmente, hay dos implementaciones de almacenamiento de nodos disponibles en la versión 6 de la versión: Almacenamiento de tar y Almacenamiento de MongoDB.

### Almacenamiento de tar {#tar-storage}

#### AEM Ejecución de una instancia de recién instalada con el almacenamiento Tar {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>El PID del almacén de nodos de segmentos ha cambiado de org.apache.jackrabbit.oak.**complementos** AEM AEM .segment.SegmentNodeStoreService en versiones anteriores de la versión 6 a la versión 8 de la aplicación, en lugar de la versión 6.3 de la aplicación, de la versión 6 de la aplicación, a la versión 6.3 de la aplicación. Asegúrese de que se realizan los ajustes de configuración necesarios para que se reflejen los cambios.

AEM De forma predeterminada, el 6 utiliza el almacenamiento Tar para almacenar nodos y binarios, utilizando las opciones de configuración predeterminadas. Puede configurar manualmente su configuración de almacenamiento haciendo lo siguiente:

1. AEM Descargue el JAR de inicio rápido de la 6 y colóquelo en una nueva carpeta.
1. AEM Desempaquetar el paquete ejecutando:

   `java -jar cq-quickstart-6.jar -unpack`

1. Cree una carpeta llamada `crx-quickstart\install` en el directorio de instalación.

1. Cree un archivo llamado `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg` en la carpeta recién creada.

1. Edite el archivo y defina las opciones de configuración. AEM Las siguientes opciones están disponibles para el almacén de nodos de segmentos, que es la base de la implementación del almacenamiento de Tar de la:

   * `repository.home`: ruta al inicio del repositorio en el que se almacenan varios datos relacionados con el repositorio. De forma predeterminada, los archivos de segmento se almacenarían en el directorio crx-quickstart/segmentstore.
   * `tarmk.size`: Tamaño máximo de un segmento en MB. El valor predeterminado es 256 MB.

1. AEM Inicio de.

### Almacenamiento de Mongo {#mongo-storage}

#### AEM Ejecución de una instancia de recién instalada con Mongo Storage {#running-a-freshly-installed-aem-instance-with-mongo-storage}

AEM Se puede configurar 6 para que se ejecute con el almacenamiento MongoDB siguiendo el siguiente procedimiento:

1. AEM Descargue el JAR de inicio rápido de la 6 y colóquelo en una nueva carpeta.
1. AEM Desempaquete el paquete ejecutando el siguiente comando:

   `java -jar cq-quickstart-6.jar -unpack`

1. Asegúrese de que MongoDB está instalado y es una instancia de `mongod` se está ejecutando. Para obtener más información, consulte [Instalación de MongoDB](https://docs.mongodb.org/manual/installation/).
1. Cree una carpeta llamada `crx-quickstart\install` en el directorio de instalación.
1. Configure el almacén de nodos creando un archivo de configuración con el nombre de la configuración que desea utilizar en `crx-quickstart\install` directorio.

   AEM El almacén de nodos de documentos (que es la base de la implementación de almacenamiento de MongoDB en la que se basa) utiliza un archivo denominado `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`

1. Edite el archivo y defina las opciones de configuración. Las opciones disponibles son las siguientes:

   * `mongouri`: La [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) necesario para conectarse a la base de datos de Mongo. El valor predeterminado es `mongodb://localhost:27017`
   * `db`: Nombre de la base de datos Mongo. AEM De forma predeterminada, las nuevas instalaciones de utilizan **aem-author** como nombre de la base de datos.
   * `cache`: tamaño de la caché en megabytes. Este tamaño de caché se distribuye entre varias cachés utilizadas en DocumentNodeStore. El valor predeterminado es 256.
   * `changesSize`: Tamaño en MB de la colección limitada utilizada en Mongo para almacenar en caché la salida de diferencia. El valor predeterminado es 256.
   * `customBlobStore`: Valor booleano que indica que se utiliza un almacén de datos personalizado. El valor predeterminado es false.

1. Cree un archivo de configuración con el PID del almacén de datos que desea utilizar y edite el archivo para establecer las opciones de configuración. Para obtener más información, consulte [Configuración de almacenes de nodos y almacenes de datos](/help/sites-deploying/data-store-config.md).

1. AEM Inicie el JAR de 6 con un back-end de almacenamiento MongoDB ejecutando:

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   Donde está el modo de ejecución back-end **`-r`** A continuación, el ejemplo comienza con la compatibilidad con MongoDB.

#### Desactivación de páginas enormes transparentes {#disabling-transparent-huge-pages}

Red Hat® Linux® utiliza un algoritmo de administración de memoria denominado Transparent Huge Pages (THP). AEM Mientras realiza lecturas y escrituras específicas, el lenguaje HTTP está optimizado para operaciones grandes. Por lo tanto, se recomienda deshabilitar THP en el almacenamiento Tar y Mongo. Para desactivar el algoritmo, siga estos pasos:

1. Abra el `/etc/grub.conf` en el editor de texto que elija.
1. Añada la línea siguiente a **grub.conf** archivo:

   ```
   transparent_hugepage=never
   ```

1. Finalmente, compruebe si la configuración ha surtido efecto ejecutando:

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   Si THP está deshabilitado, el resultado del comando anterior debería ser:

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>Consulte los siguientes recursos:
>
>* Para obtener más información sobre Transparent Huge Pages en Red Hat® Linux®, consulte esto [artículo](https://access.redhat.com/solutions/46111).
>* Para obtener sugerencias de optimización de Linux®, consulte esto [artículo](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=es).
>

## Mantenimiento del repositorio {#maintaining-the-repository}

Cada actualización del repositorio crea una revisión de contenido. Como resultado, con cada actualización el tamaño del repositorio aumenta. Para evitar el crecimiento incontrolado del repositorio, las revisiones antiguas deben limpiarse para liberar recursos de disco. Esta funcionalidad de mantenimiento se denomina Limpieza de revisión. El mecanismo Revision Cleanup recupera el espacio en disco eliminando los datos obsoletos del repositorio. Para obtener más información acerca de Revision Cleanup, lea la [Página Limpieza de revisión](/help/sites-deploying/revision-cleanup.md).
