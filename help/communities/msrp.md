---
title: MSRP - Proveedor de recursos de almacenamiento MongoDB
seo-title: MSRP - Proveedor de recursos de almacenamiento MongoDB
description: Configurar las comunidades AEM para que utilicen una base de datos relacional como su almacén común
seo-description: Configurar las comunidades AEM para que utilicen una base de datos relacional como su almacén común
uuid: 9fc06d4f-a60f-4ce3-8586-bcc836aa7de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 048f7b30-20c3-4567-bd32-38cf2643cf39
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# MSRP - Proveedor de recursos de almacenamiento MongoDB {#msrp-mongodb-storage-resource-provider}

## Acerca de MSRP {#about-msrp}

Cuando AEM Communities está configurada para utilizar MSRP como su almacén común, el contenido generado por el usuario (UGC) es accesible desde todas las instancias de creación y publicación sin necesidad de sincronización ni replicación.

Consulte también [Características de las Opciones](working-with-srp.md#characteristics-of-srp-options) de SRP y Topologías [](topologies.md)recomendadas.

## Requisitos {#requirements}

* [MongoDB](https://www.mongodb.org/):

   * Versión 2.6 o posterior
   * No es necesario configurar los mongos ni el uso compartido
   * Recomendar enérgicamente el uso de un conjunto de [réplicas](#mongoreplicaset)
   * Puede ejecutarse en el mismo host que AEM o de forma remota

* [Apache Solr](https://lucene.apache.org/solr/):

   * Versión 4.10 o 5
   * Solr requiere Java 1.7 o superior
   * No se necesita ningún servicio
   * Opción de modos de ejecución:
      * Modo independiente
      * [Modo](solr.md#solrcloud-mode) SolrCloud (recomendado para entornos de producción)
   * Opción de búsqueda multilingüe (MLS)
      * [Instalación de MLS estándar](solr.md#installing-standard-mls)
      * [Instalación de MLS avanzados](solr.md#installing-advanced-mls)

## MongoDB Configuration {#mongodb-configuration}

### Seleccionar MSRP {#select-msrp}

La consola [Configuración](srp-config.md) de almacenamiento permite seleccionar la configuración de almacenamiento predeterminada, que identifica la implementación de SRP que se va a utilizar.

Al crear, para acceder a la consola de configuración de almacenamiento:

* Desde la navegación global: **[!UICONTROL Herramientas > Comunidades > Configuración de almacenamiento]**

![chlimage_1-28](assets/chlimage_1-28.png)

* Select **[!UICONTROL MongoDB Storage Resource Provider (MSRP)]**
* **[!UICONTROL Configuración de mongoDB]**

   * **[!UICONTROL URI de mongoDB]**

      *predeterminado*: mongodb://localhost/?maxPoolSize=10&amp;waitQueueMultiple=5&amp;readPreference=secondaryPreferred

   * **[!UICONTROL Base de datos mongoDB]**

      *predeterminado*: comunidades

   * **[!UICONTROL Colección de UGC mongoDB]**

      *predeterminado*:content

   * **[!UICONTROL Colección de datos adjuntos mongoDB]**

      *predeterminado*:adjuntos

* **[!UICONTROL SolrConfiguration]**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Host de Zookeeper **

      Cuando se ejecuta en el modo [](solr.md#solrcloud-mode) SolrCloud con un zooKeeper externo, establezca este valor en el `HOST:PORT` para ZooKeeper, como *my.server.com:2181* Para un ensamblado ZooKeeper, introduzca `HOST:PORT` valores separados por comas, como *host1:2181,host2:2181*Deje en blanco si ejecuta Solr en modo independiente mediante el zooKeeper interno.
      *Predeterminado*: *&lt;blank>*
   * **[!UICONTROL Solr URL]**La URL que se utiliza para comunicarse con Solr en modo independiente.
Deje en blanco si se ejecuta en el modo de SolrCloud.
      *Predeterminado*: https://127.0.0.1:8983/solr/
   * **[!UICONTROL Colección]**Solr El nombre de la colección Solr.
      *Predeterminado*: collection1
* Seleccione **[!UICONTROL Enviar]**

>[!NOTE]
>
>La base de datos mongoDB, que se establece de forma predeterminada en el nombre `communities`, no debe establecerse en el nombre de una base de datos que se esté utilizando para almacenes de [nodos o almacenes](../../help/sites-deploying/data-store-config.md)de datos (binarios). Consulte también Elementos [de almacenamiento en AEM 6](../../help/sites-deploying/storage-elements-in-aem-6.md).

### Conjunto de réplicas MongoDB {#mongodb-replica-set}

Para el entorno de producción, se recomienda enfáticamente configurar un conjunto de réplicas, un clúster de servidores MongoDB que implemente la replicación esclava maestra y el failover automatizado.

Para obtener más información sobre los conjuntos de réplicas, visite la documentación de [replicación](https://docs.mongodb.org/manual/replication/) de MongoDB.

Para trabajar con conjuntos de réplicas y aprender a definir conexiones entre las aplicaciones y las instancias de MongoDB, visite la documentación de Formato [URI de cadena de](https://docs.mongodb.org/manual/reference/connection-string/) conexión de MongoDB.

#### Url de ejemplo para la conexión a un conjunto de réplicas {#example-url-for-connecting-to-a-replica-set}

```shell
# Example url for:
#     servers "mongoserver1", "mongoserver2", "mongoserver3"
#     replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Configuración de Solr {#solr-configuration}

Una instalación de Solr puede compartirse entre el almacén de nodos (Oak) y el almacén común (MSRP) mediante diferentes colecciones.

Si se utilizan intensamente las colecciones Oak y MSRP, se puede instalar un segundo Solr por motivos de rendimiento.

Para los entornos de producción, el modo [](solr.md#solrcloud-mode) SolrCloud ofrece un rendimiento mejorado respecto al modo independiente (una única configuración local de Solr).

Para obtener más información sobre la configuración, consulte Configuración [solar para SRP](solr.md).

### Actualización {#upgrading}

Si se actualiza desde una versión anterior configurada con MSRP, será necesario

1. Realizar la [actualización a AEM Communities](upgrade.md)
1. Instalar nuevos archivos de configuración de Solr
   * Para MLS [estándar](solr.md#installing-standard-mls)
   * Para MLS [avanzados](solr.md#installing-advanced-mls)
1. Reindexar MSRPSee sección Herramienta de reindexación [MSRP](#msrp-reindex-tool)

## Publicación de la configuración {#publishing-the-configuration}

El MSRP debe identificarse como el almacén común en todas las instancias de creación y publicación.

Para que la configuración idéntica esté disponible en el entorno de publicación:

* Sobre el autor:
   * Vaya del menú principal a **[!UICONTROL Herramientas > Operaciones > Replicación]**
   * Seleccione **[!UICONTROL Activar árbol]**
   * **[!UICONTROL Ruta de inicio]**:
      * Vaya a `/etc/socialconfig/srpc/`
   * Seleccionar **[!UICONTROL activar]**

## Administración de datos de usuario {#managing-user-data}

Para obtener información sobre *usuarios*, perfiles *de* usuario y grupos *de* usuarios, que a menudo se introducen en el entorno de publicación, visite

* [Sincronización de usuarios](sync.md)
* [Administración de usuarios y grupos de usuarios](users.md)

## Herramienta de reindexación MSRP {#msrp-reindex-tool}

Hay un extremo HTTP para volver a indexar Solr para MSRP al instalar nuevos archivos de configuración o reparar un índice Solr dañado.

Con esta herramienta, MongoDB es la fuente de la *verdad* para el MSRP; las copias de seguridad sólo se deben realizar de MongoDB.

El árbol UGC completo se puede volver a indexar, o solo un subárbol específico, tal como se especifica en el parámetro *path *data.

Esta herramienta se puede ejecutar desde la línea de comandos mediante cURL o cualquier otra herramienta HTTP.

Al reindexar, hay un equilibrio entre la memoria y el rendimiento controlado por el parámetro *batchSize *data, que especifica cuántos registros UGC se reindexan por lote.

Un valor predeterminado razonable es 5000:

* Si la memoria es un problema, especifique un número menor
* Si la velocidad es un problema, especifique un número mayor para aumentar la velocidad

### Ejecución de la herramienta de reindexación MSRP mediante el comando cURL {#running-msrp-reindex-tool-using-curl-command}

El siguiente comando cURL muestra lo que es necesario para que una solicitud HTTP vuelva a indexar UGC almacenado en MSRP.

El formato básico es:

cURL -u *inicio de sesión* -d *datos* *reindex-url*

*inicio de sesión* = id-administrador:contraseñaPor ejemplo: admin:admin

*data* = &quot;batchSize=*size*&amp;path=*path&quot;*

*size* = cuántas entradas de UGC se reindexarán por operación`/content/usergenerated/asi/mongo/`

*path* = la ubicación raíz del árbol de UGC para volver a indexar

* Para volver a indexar todo el UGC, especifique el valor de la `asipath`propiedad de
   `/etc/socialconfig/srpc/defaultconfiguration`
* Para limitar el índice a algún UGC, especifique un subárbol de `asipath`

*reindex-url* = el punto final para volver a indexar el SRP`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>Si está [reindexando DSRP Solr](dsrp.md), la dirección URL es **/services/social/datastore/rdb/reindex**

### Ejemplo de reindexación MSRP {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## Cómo Demostrar el MSRP {#how-to-demo-msrp}

Para configurar el MSRP para un entorno de demostración o desarrollo, consulte [HowTo Setup MongoDB for Demo](demo-mongo.md).

## Solución de problemas {#troubleshooting}

### UGC no visible en MongoDB {#ugc-not-visible-in-mongodb}

Compruebe la configuración de la opción de almacenamiento para asegurarse de que MSRP se ha configurado como el proveedor predeterminado. De forma predeterminada, el proveedor de recursos de almacenamiento es JSRP.

En todas las instancias de AEM de creación y publicación, vuelva a la consola [Configuración](srp-config.md) de almacenamiento o compruebe el repositorio de AEM:

* En JCR, if [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * No contiene un nodo [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) , significa que el proveedor de almacenamiento es JSRP
   * Si el nodo srpc existe y contiene la configuración [predeterminada](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)del nodo, las propiedades de configuración predeterminada deben definir MSRP para que sea el proveedor predeterminado

### UGC desaparece tras la actualización {#ugc-disappears-after-upgrade}

Si realiza la actualización desde un sitio existente de AEM Communities 6.0, cualquier UGC preexistente debe convertirse para ajustarse a la estructura necesaria para la API de [SRP](srp.md) después de actualizar a AEM Communities 6.3.

Hay una herramienta de código abierto disponible en GitHub para este propósito:

* [Herramienta de migración UGC de AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

La herramienta de migración se puede personalizar para exportar UGC de versiones anteriores de comunidades sociales de AEM para importarlos a AEM Communities 6.1 o posterior.

### Error: proveedor de campos no definido {#error-undefined-field-provider-id}

Si se muestra el siguiente error en los registros, indica que el archivo de esquema Solr no está configurado correctamente.

#### JsonMappingException: field provider_id no definido {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

Para resolver el error, cuando siga las instrucciones para [instalar MLS](solr.md#installing-standard-mls)estándar, asegúrese de

* Los archivos de configuración XML se copiaron en la ubicación de Solr correcta
* Solr se reinició después de que los nuevos archivos de configuración reemplazaran a los existentes

### Falla la conexión segura con MongoDB {#secure-connection-to-mongodb-fails}

Si un intento de establecer una conexión segura con el servidor MongoDB falla debido a la falta de una definición de clase, es necesario actualizar el paquete de controladores MongoDB, `mongo-java-driver`, disponible en el repositorio público.

1. Descargue el controlador de [https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar) (versión 2.13.2 o posterior)
1. Copie el paquete en la carpeta &quot;crx-quickstart/install&quot; para una instancia de AEM
1. Reinicie la instancia de AEM

## Medios {#resources}

* [AEM con MongoDB](../../help/sites-deploying/aem-with-mongodb.md)
* [Documentación de MongoDB](https://docs.mongodb.org/)

