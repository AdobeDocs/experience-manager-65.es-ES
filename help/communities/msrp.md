---
title: 'MSRP: proveedor de recursos de almacenamiento de MongoDB'
description: Configure AEM Communities para que utilice una base de datos relacional como almacén común
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 799d5ae1-caac-4c92-8835-696ad25de553
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 0%

---

# MSRP: proveedor de recursos de almacenamiento de MongoDB {#msrp-mongodb-storage-resource-provider}

## Acerca de MSRP {#about-msrp}

Cuando AEM Communities está configurado para utilizar MSRP como almacén común, el contenido generado por el usuario (UGC) es accesible desde todas las instancias de autor y publicación sin necesidad de sincronización ni replicación.

Consulte también [Características de las opciones de SRP](working-with-srp.md#characteristics-of-srp-options) y [Topologías recomendadas](topologies.md).

## Requisitos  {#requirements}

* [MongoDB](https://www.mongodb.org/):

   * Versión 2.6 o superior
   * No es necesario configurar mongos ni el uso compartido
   * Recomendamos encarecidamente el uso de un [conjunto de réplicas](#mongoreplicaset)
   * AEM Puede ejecutarse en el mismo host que el servidor de correo o puede ejecutarse de forma remota.

* [Apache Solr](https://lucene.apache.org/solr/):

   * Solr versión 7.0
   * Solr requiere Java 1.7 o superior
   * No se necesita ningún servicio
   * Elección de los modos de ejecución:
      * Modo independiente
      * [Modo SolrCloud](solr.md#solrcloud-mode) (recomendado para entornos de producción)
   * Opción de búsqueda multilingüe (MLS):
      * [Instalación de MLS estándar](solr.md#installing-standard-mls)
      * [Instalación de MLS avanzado](solr.md#installing-advanced-mls)

## Configuración de MongoDB {#mongodb-configuration}

### Seleccionar MSRP {#select-msrp}

El [Consola de configuración de almacenamiento](srp-config.md) permite seleccionar la configuración de almacenamiento predeterminada, que identifica qué implementación de SRP utilizar.

En autor, para acceder a la consola Configuración de almacenamiento:

* En la navegación global, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Communities]** > **[!UICONTROL Configuración de almacenamiento]**.

![msrp](assets/msrp.png)

* Seleccionar **[!UICONTROL Proveedor de recursos de almacenamiento de MongoDB (MSRP)]**
* **[!UICONTROL Configuración de mongoDB]**

   * **[!UICONTROL URI de mongoDB]**

     *predeterminado*: mongodb://localhost/?maxPoolSize=10&amp;waitQueueMultiple=5&amp;readPreference=secondaryPreferred

   * **[!UICONTROL Base de datos mongoDB]**

     *predeterminado*: comunidades

   * **[!UICONTROL Colección de UGC mongoDB]**

     *predeterminado*: contenido

   * **[!UICONTROL Colección de datos adjuntos mongoDB]**

     *predeterminado*: archivos adjuntos

* **[!UICONTROL SolrConfiguration]**

   * **[Zookeeper](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files) Host**

     Cuando se ejecuta en [Modo SolrCloud](solr.md#solrcloud-mode) con un ZooKeeper externo, establezca este valor en el `HOST:PORT` para el ZooKeeper, como *my.server.com:2181*

     Para un conjunto ZooKeeper, introduzca separados por comas `HOST:PORT` valores, como *host1:2181,host2:2181*

     Déjelo en blanco si ejecuta Solr en modo independiente utilizando el ZooKeeper interno.
     *Predeterminado*: *&lt;blank>*

      * **[!UICONTROL URL de Solr]**
Dirección URL utilizada para comunicarse con Solr en modo independiente.
Déjelo en blanco si se ejecuta en el modo SolrCloud.
        *Predeterminado*: https://127.0.0.1:8983/solr/

      * **[!UICONTROL Colección Solr]**
Nombre de la colección Solr.
        *Predeterminado*: colección1

* Seleccionar **[!UICONTROL Enviar]**

>[!NOTE]
>
>La base de datos mongoDB, que toma el nombre predeterminado `communities`, no debe configurarse con el nombre de la base de datos utilizada para [almacenes de nodos o almacenes de datos (binarios)](../../help/sites-deploying/data-store-config.md). Consulte también [AEM Elementos de almacenamiento en 6.5](../../help/sites-deploying/storage-elements-in-aem-6.md).

### Conjunto de réplicas de MongoDB {#mongodb-replica-set}

Para el entorno de producción, se recomienda encarecidamente configurar un conjunto de réplicas, un clúster de servidores MongoDB que implementa replicación primaria-secundaria y conmutación por error automatizada.

Para obtener más información acerca de los conjuntos de réplicas, visite MongoDB&#39;s [Replicación](https://docs.mongodb.org/manual/replication/) documentación.

Para trabajar con conjuntos de réplicas y aprender a definir conexiones entre aplicaciones e instancias de MongoDB, visite la página de MongoDB [Formato URI de cadena de conexión](https://docs.mongodb.org/manual/reference/connection-string/) documentación.

#### URL de ejemplo para conectarse a un conjunto de réplicas  {#example-url-for-connecting-to-a-replica-set}

```shell
# Example url for:
# servers "mongoserver1", "mongoserver2", "mongoserver3"
# replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Configuración de Solr {#solr-configuration}

Una instalación de Solr puede compartirse entre el almacén de nodos (Oak) y el almacén común (MSRP) utilizando diferentes colecciones.

Si las colecciones Oak y MSRP se utilizan intensivamente, se puede instalar un segundo Solr por motivos de rendimiento.

Para entornos de producción, [Modo SolrCloud](solr.md#solrcloud-mode) proporciona un rendimiento mejorado con respecto al modo independiente (una única configuración local de Solr).

Para obtener más información, consulte [Configuración de Solr para SRP](solr.md).

### Actualización {#upgrading}

Si se actualiza desde una versión anterior configurada con MSRP, será necesario:

1. Realice la [actualización a AEM Communities](upgrade.md)
1. Instalar nuevos archivos de configuración de Solr
   * Para [MLS estándar](solr.md#installing-standard-mls)
   * Para [MLS avanzado](solr.md#installing-advanced-mls)
1. Reindexar MSRP Consulte la sección [Herramienta de reindexación MSRP](#msrp-reindex-tool)

## Publicación de la configuración {#publishing-the-configuration}

El MSRP debe identificarse como el almacén común en todas las instancias de autor y publicación.

Para que la configuración idéntica esté disponible en el entorno de publicación, inicie sesión en la instancia de autor y siga los pasos:

* Vaya del menú principal a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Replicación]**.
* Seleccionar **[!UICONTROL Activar árbol]**
* **[!UICONTROL Ruta de inicio]**:
   * Navegar a `/etc/socialconfig/srpc/`
* Seleccionar **[!UICONTROL Activar]**

## Administración de datos de usuario {#managing-user-data}

Para obtener información sobre *usuarios*, *perfiles de usuario* y *grupos de usuarios*, introducidas a menudo en el entorno de publicación, visite

* [Sincronización de usuarios](sync.md)
* [Administración de usuarios y grupos de usuarios](users.md)

## Herramienta de reindexación MSRP {#msrp-reindex-tool}

Existe un extremo HTTP para reindexar Solr para MSRP al instalar nuevos archivos de configuración o reparar un índice de Solr dañado.

Con esta herramienta, MongoDB es la fuente de *verdad* para MSRP; las copias de seguridad solo deben realizarse en MongoDB.

Se puede reindexar todo el árbol UGC o solo un subárbol específico, tal como se especifica en el parámetro de datos *path *data.

Esta herramienta se puede ejecutar desde la línea de comandos utilizando cURL o cualquier otra herramienta HTTP.

Al reindexar, existe un equilibrio entre la memoria y el rendimiento controlado por el parámetro de datos *batchSize *, que especifica cuántos registros UGC se reindexan por lote.

Un valor predeterminado razonable es 5000:

* Si la memoria es un problema, especifique un número menor
* Si la velocidad es un problema, especifique un número mayor para aumentar la velocidad

### Ejecución de la herramienta de reindexación MSRP mediante el comando cURL {#running-msrp-reindex-tool-using-curl-command}

El siguiente comando cURL muestra lo necesario para que una solicitud HTTP reindexe UGC almacenados en MSRP.

El formato básico es:

cURL -u *firma* -d *datos* *reindex-url*

*firma* = administrator-id:contraseña Por ejemplo: admin:admin

*datos* = &quot;batchSize=*talla*&amp;path=*path&quot;*

*talla* = cuántas entradas UGC reindexar por operación
`/content/usergenerated/asi/mongo/`

*ruta* = la ubicación raíz del árbol de UGC para reindexar

* Para reindexar todos los UGC, especifique el valor de `asipath`propiedad de
  `/etc/socialconfig/srpc/defaultconfiguration`
* Para limitar el índice a algunos UGC, especifique un subárbol de `asipath`

*reindex-url* = el punto final para la reindexación de SRP
`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>Si es usted [reindexación de DSRP Solr](dsrp.md), la dirección URL es **/services/social/datastore/rdb/reindex**

### Ejemplo de reindexación de MSRP {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## Cómo hacer una demostración de MSRP {#how-to-demo-msrp}

Para configurar el MSRP para un entorno de demostración o desarrollo, consulte [Cómo configurar MongoDB para la demostración](demo-mongo.md).

## Solución de problemas {#troubleshooting}

### UGC no visible en MongoDB {#ugc-not-visible-in-mongodb}

Asegúrese de que MSRP se ha configurado para ser el proveedor predeterminado comprobando la configuración de la opción de almacenamiento. De forma predeterminada, el proveedor de recursos de almacenamiento es JSRP.

AEM En todas las instancias de creación y publicación de la aplicación, vuelva a visitar la página de inicio de sesión [Consola de configuración de almacenamiento](srp-config.md) AEM o compruebe el repositorio de la:

* En JCR, si [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * No contiene un [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) , significa que el proveedor de almacenamiento es JSRP.
   * Si el nodo srpc existe y contiene un nodo [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration), las propiedades de la configuración predeterminada deben definir MSRP para que sea el proveedor predeterminado.

### UGC desaparece tras la actualización {#ugc-disappears-after-upgrade}

Si se actualiza desde un sitio de AEM Communities 6.0 existente, cualquier UGC preexistente debe convertirse para ajustarse a la estructura requerida para el [SRP](srp.md) API después de actualizar a AEM Communities 6.3.

Hay una herramienta de código abierto disponible en GitHub para este fin:

* [Herramienta de migración de UGC para AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

AEM La herramienta de migración se puede personalizar para exportar UGC desde versiones anteriores de comunidades sociales de la comunidad de la comunidad de la comunidad de la comunidad de la comunidad de la comunidad de la comunidad de la comunidad para importarlo en AEM Communities 6.1 o posterior.

### Error - campo indefinido provider_id {#error-undefined-field-provider-id}

Si se ve el siguiente error en los registros, indica que el archivo de esquema de Solr no está configurado correctamente.

#### JsonMappingException: campo indefinido provider_id {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

Para resolver el error, siga las instrucciones de [Instalación de MLS estándar](solr.md#installing-standard-mls), asegúrese de que:

* Los archivos de configuración XML se copiaron en la ubicación Solr correcta.
* Solr se reinició después de que los nuevos archivos de configuración reemplazaran a los existentes.

### Error en la conexión segura con MongoDB {#secure-connection-to-mongodb-fails}

Si un intento de realizar una conexión segura al servidor MongoDB falla debido a la falta de una definición de clase, es necesario actualizar el paquete de controladores MongoDB, `mongo-java-driver`, disponible en el repositorio público de maven.

1. Descargue el controlador desde [https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar) (versión 2.13.2 o posterior).
1. AEM Copie el paquete en la carpeta &quot;crx-quickstart/install&quot; para una instancia de.
1. Reinicie la instancia de AEM.

## Recursos {#resources}

* [AEM con MongoDB](../../help/sites-deploying/aem-with-mongodb.md)
* [Documentación de MongoDB](https://docs.mongodb.org/)
