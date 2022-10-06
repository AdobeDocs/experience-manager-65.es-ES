---
title: MSRP - Proveedor de recursos de almacenamiento MongoDB
seo-title: MSRP - MongoDB Storage Resource Provider
description: Configuración de AEM Communities para utilizar una base de datos relacional como su tienda común
seo-description: Set up AEM Communities to use a relational database as its common store
uuid: 9fc06d4f-a60f-4ce3-8586-bcc836aa7de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 048f7b30-20c3-4567-bd32-38cf2643cf39
role: Admin
exl-id: 799d5ae1-caac-4c92-8835-696ad25de553
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1191'
ht-degree: 2%

---

# MSRP - Proveedor de recursos de almacenamiento MongoDB {#msrp-mongodb-storage-resource-provider}

## Acerca del MSRP {#about-msrp}

Cuando AEM Communities está configurado para utilizar MSRP como su tienda común, el contenido generado por el usuario (UGC) es accesible desde todas las instancias de autor y publicación sin necesidad de sincronización ni replicación.

Consulte también [Características de las opciones de SRP](working-with-srp.md#characteristics-of-srp-options) y [Topologías recomendadas](topologies.md).

## Requisitos  {#requirements}

* [MongoDB](https://www.mongodb.org/):

   * Versión 2.6 o buena
   * No es necesario configurar los mongos o el uso compartido
   * Recomendar encarecidamente el uso de un [conjunto de réplicas](#mongoreplicaset)
   * Puede ejecutarse en el mismo host que AEM o ejecutar de forma remota

* [Apache Solr](https://lucene.apache.org/solr/):

   * Versión de Solr 7.0
   * Solr requiere Java 1.7 o bueno
   * No se necesita ningún servicio
   * Elección de modos de ejecución:
      * Modo independiente
      * [Modo SolrCloud](solr.md#solrcloud-mode) (recomendado para entornos de producción)
   * Opción de búsqueda multilingüe (MLS):
      * [Instalación de MLS estándar](solr.md#installing-standard-mls)
      * [Instalación de MLS avanzados](solr.md#installing-advanced-mls)

## Configuración de MongoDB {#mongodb-configuration}

### Seleccionar MSRP {#select-msrp}

La variable [Consola de configuración de almacenamiento](srp-config.md) permite seleccionar la configuración de almacenamiento predeterminada, que identifica qué implementación de SRP utilizar.

Al autor, para acceder a la consola de configuración de almacenamiento:

* En la navegación global, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Configuración de almacenamiento]**.

![msrp](assets/msrp.png)

* Select **[!UICONTROL Proveedor de recursos de almacenamiento de MongoDB (MSRP)]**
* **[!UICONTROL Configuración de mongoDB]**

   * **[!UICONTROL URI de mongoDB]**

      *default*: mongodb://localhost/?maxPoolSize=10&amp;waitQueueMultiple=5&amp;readPreference=secondaryPreferred

   * **[!UICONTROL Base de datos mongoDB]**

      *default*: comunidades

   * **[!UICONTROL Colección de UGC mongoDB]**

      *default*: contenido

   * **[!UICONTROL Colección de datos adjuntos mongoDB]**

      *default*: archivos adjuntos

* **[!UICONTROL SolrConfiguration]**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Host de Zookeeper**

      Al ejecutar [Modo SolrCloud](solr.md#solrcloud-mode) con un ZooKeeper externo, establezca este valor en la variable `HOST:PORT` para ZooKeeper, como *my.server.com:2181*

      Para un ensamblado ZooKeeper, introduzca separados por coma `HOST:PORT` valores como *host1:2181,host2:2181*

      Deje en blanco si ejecuta Solr en modo independiente utilizando el ZooKeeper interno.
      *Predeterminado*: *&lt;blank>*

      * **[!UICONTROL URL de Solr]**
La URL utilizada para comunicarse con Solr en modo independiente.
Déjelo en blanco si se ejecuta en el modo SolrCloud.

         *Predeterminado*: https://127.0.0.1:8983/solr/

      * **[!UICONTROL Colección Solr]**
El nombre de la colección Solr.

         *Predeterminado*: colección1

* Seleccione **[!UICONTROL Enviar]**

>[!NOTE]
>
>La base de datos mongoDB, que toma el nombre predeterminado `communities`, no debe establecerse en el nombre de una base de datos para la que se esté utilizando [almacenes de nodos o almacenes de datos (binarios)](../../help/sites-deploying/data-store-config.md). Consulte también [Elementos de almacenamiento en AEM 6.5](../../help/sites-deploying/storage-elements-in-aem-6.md).

### Conjunto de réplicas de MongoDB {#mongodb-replica-set}

Para el entorno de producción, se recomienda configurar un conjunto de réplicas, un clúster de servidores MongoDB que implementa replicación primaria-secundaria y failover automatizado.

Para obtener más información sobre los conjuntos de réplicas, visite MongoDB [Replicación](https://docs.mongodb.org/manual/replication/) documentación.

Para trabajar con conjuntos de réplicas y aprender a definir conexiones entre aplicaciones y instancias de MongoDB, visite el [Formato de URI de cadena de conexión](https://docs.mongodb.org/manual/reference/connection-string/) documentación.

#### Url de ejemplo para conectarse a un conjunto de réplicas  {#example-url-for-connecting-to-a-replica-set}

```shell
# Example url for:
# servers "mongoserver1", "mongoserver2", "mongoserver3"
# replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Configuración de Solr {#solr-configuration}

Una instalación de Solr se puede compartir entre el almacén de nodos (Oak) y el almacén común (MSRP) utilizando diferentes colecciones.

Si se utilizan intensamente las colecciones Oak y MSRP, puede instalarse un segundo Solr por motivos de rendimiento.

Para entornos de producción, [Modo SolrCloud](solr.md#solrcloud-mode) proporciona un rendimiento mejorado con respecto al modo independiente (una única configuración local de Solr).

Para obtener más información sobre la configuración, consulte [Configuración de Solr para SRP](solr.md).

### Actualización {#upgrading}

Si actualiza desde una versión anterior configurada con MSRP, será necesario:

1. Realice la [actualizar a AEM Communities](upgrade.md)
1. Instalar nuevos archivos de configuración de Solr
   * Para [MLS estándar](solr.md#installing-standard-mls)
   * Para [MLS avanzado](solr.md#installing-advanced-mls)
1. Reindexar MSRP Véase sección [Herramienta de reindexación de MSRP](#msrp-reindex-tool)

## Publicación de la configuración {#publishing-the-configuration}

El MSRP debe identificarse como el almacén común en todas las instancias de autor y publicación.

Para que la configuración idéntica esté disponible en el entorno de publicación, inicie sesión en la instancia de autor y siga los pasos:

* Vaya del menú principal a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Replicación]**.
* Select **[!UICONTROL Activar árbol]**
* **[!UICONTROL Ruta de inicio]**:
   * Vaya a `/etc/socialconfig/srpc/`
* Select **[!UICONTROL Activar]**

## Administración de datos de usuario {#managing-user-data}

Para obtener información sobre *usuarios*, *perfiles de usuario* y *grupos de usuarios*, introducidos a menudo en el entorno de publicación, visita

* [Sincronización de usuarios](sync.md)
* [Administración de usuarios y grupos de usuarios](users.md)

## Herramienta de reindexación de MSRP {#msrp-reindex-tool}

Hay un extremo HTTP para reindexar Solr para MSRP cuando se instalan nuevos archivos de configuración o se repare un índice Solr dañado.

Con esta herramienta, MongoDB es la fuente de *verdad* para el MSRP; las copias de seguridad solo deben realizarse con MongoDB.

El árbol UGC completo se puede reindexar, o solo un subárbol específico, como se especifica en el parámetro *path *data .

Esta herramienta se puede ejecutar desde la línea de comandos utilizando cURL o cualquier otra herramienta HTTP.

Al reindexar, existe un equilibrio entre la memoria y el rendimiento controlado por el parámetro *batchSize *data , que especifica cuántos registros UGC se reindexan por lote.

Un valor predeterminado razonable es 5000:

* Si la memoria es un problema, especifique un número menor
* Si la velocidad es un problema, especifique un número mayor para aumentar la velocidad

### Ejecución de la herramienta de reindexación MSRP mediante el comando cURL {#running-msrp-reindex-tool-using-curl-command}

El siguiente comando cURL muestra lo que es necesario para que una solicitud HTTP reindexe el UGC almacenado en MSRP.

El formato básico es:

cURL -u *inicio de sesión* -d *data* *reindex-url*

*inicio de sesión* = id-administrador:contraseña Por ejemplo: admin:admin

*data* = &quot;batchSize=*size*&amp;path=*path&quot;*

*size* = cuántas entradas UGC reindexar por operación
`/content/usergenerated/asi/mongo/`

*ruta* = la ubicación raíz del árbol de UGC para reindexar

* Para reindexar todo UGC, especifique el valor de la variable `asipath`propiedad de
   `/etc/socialconfig/srpc/defaultconfiguration`
* Para limitar el índice a algún UGC, especifique un subárbol de `asipath`

*reindex-url* = el punto final para la reindexación del SRP
`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>Si [reindexación de DSRP Solr](dsrp.md), la dirección URL es **/services/social/datastore/rdb/reindex**

### Ejemplo de reindexación de MSRP {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## Cómo mostrar el MSRP {#how-to-demo-msrp}

Para configurar el MSRP para un entorno de demostración o desarrollo, consulte [Configuración de MongoDB para demostración](demo-mongo.md).

## Solución de problemas {#troubleshooting}

### UGC no visible en MongoDB {#ugc-not-visible-in-mongodb}

Asegúrese de que MSRP se haya configurado para ser el proveedor predeterminado comprobando la configuración de la opción de almacenamiento. De forma predeterminada, el proveedor de recursos de almacenamiento es JSRP.

En todas las instancias de creación y publicación de AEM, vuelva a la sección [Consola de configuración de almacenamiento](srp-config.md) o compruebe el repositorio AEM:

* En JCR, si [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * No contiene un [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) , significa que el proveedor de almacenamiento es JSRP.
   * Si el nodo srpc existe y contiene el nodo [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration), las propiedades de la configuración predeterminada deben definir MSRP para que sea el proveedor predeterminado.

### UGC desaparece después de la actualización {#ugc-disappears-after-upgrade}

Si se actualiza desde un sitio de AEM Communities 6.0 existente, cualquier UGC preexistente debe convertirse para ajustarse a la estructura necesaria para el [SRP](srp.md) API después de actualizar a AEM Communities 6.3.

Hay una herramienta de código abierto disponible en GitHub para este fin:

* [Herramienta de migración UGC de AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

La herramienta de migración se puede personalizar para exportar UGC de versiones anteriores de AEM comunidades sociales para importarlo a AEM Communities 6.1 o posterior.

### Error: identificador_proveedor_campo no definido {#error-undefined-field-provider-id}

Si se ve el siguiente error en los registros, indica que el archivo de esquema Solr no está configurado correctamente.

#### JsonMappingException: field provider_id no definido {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

Para resolver el error, cuando siga las instrucciones para [Instalación de MLS estándar](solr.md#installing-standard-mls), asegúrese de:

* Los archivos de configuración XML se copiaron en la ubicación Solr correcta.
* Solr se reinició después de que los nuevos archivos de configuración reemplazaran a los existentes.

### Falla la conexión segura con MongoDB {#secure-connection-to-mongodb-fails}

Si falla un intento de establecer una conexión segura con el servidor MongoDB debido a la falta de una definición de clase, es necesario actualizar el paquete de controladores MongoDB, `mongo-java-driver`, disponible desde el repositorio público maven.

1. Descargue el controlador de [https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar) (versión 2.13.2 o posterior).
1. Copie el paquete en la carpeta &quot;crx-quickstart/install&quot; para una instancia de AEM.
1. Reinicie la instancia de AEM.

## Medios {#resources}

* [AEM con MongoDB](../../help/sites-deploying/aem-with-mongodb.md)
* [Documentación de MongoDB](https://docs.mongodb.org/)
