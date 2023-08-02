---
title: 'DSRP: proveedor de recursos de almacenamiento de base de datos relacional'
description: Configure AEM Communities para que utilice una base de datos relacional como almacén común
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 15b3a594-efde-4702-9233-232ba1c7e5b0
source-git-commit: f0dd1ac3ab9c17a8b331f5048d84ec97dd23924f
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 3%

---

# DSRP: proveedor de recursos de almacenamiento de base de datos relacional {#dsrp-relational-database-storage-resource-provider}

## Acerca de DSRP {#about-dsrp}

Cuando AEM Communities está configurado para utilizar una base de datos relacional como almacén común, el contenido generado por el usuario (UGC) es accesible desde todas las instancias de autor y publicación sin necesidad de sincronización ni replicación.

Consulte también [Características de las opciones de SRP](working-with-srp.md#characteristics-of-srp-options) y [Topologías recomendadas](topologies.md).

## Requisitos  {#requirements}

* [MySQL](#mysql-configuration), una base de datos relacional.
* [Apache Solr](#solr-configuration), una plataforma de búsqueda.

>[!NOTE]
>
>La configuración de almacenamiento predeterminada ahora se almacena en conf path(`/conf/global/settings/community/srpc/defaultconfiguration`) en lugar de `etc` ruta (`/etc/socialconfig/srpc/defaultconfiguration`). Se le aconseja que siga las [pasos de migración](#zerodt-migration-steps) para que defaultsrp funcione según lo esperado.

## Configuración de base de datos relacional {#relational-database-configuration}

### Configuración de MySQL {#mysql-configuration}

Una instalación de MySQL puede compartirse entre características de habilitación y almacén común (DSRP) dentro del mismo grupo de conexiones utilizando nombres de base de datos (esquema) diferentes y también diferentes conexiones (servidor:puerto).

Para obtener detalles de instalación y configuración, consulte [Configuración de MySQL para DSRP](dsrp-mysql.md).

### Configuración de Solr {#solr-configuration}

Una instalación de Solr puede compartirse entre el almacén de nodos (Oak) y el almacén común (SRP) utilizando diferentes colecciones.

Si las colecciones Oak y SRP se utilizan intensivamente, se puede instalar un segundo Solr por motivos de rendimiento.

Para entornos de producción, el modo SolrCloud proporciona un rendimiento mejorado con respecto al modo independiente (una única configuración de Solr local).

Para obtener detalles de instalación y configuración, consulte [Configuración de Solr para SRP](solr.md).

### Seleccionar DSRP {#select-dsrp}

El [Consola de configuración de almacenamiento](srp-config.md) permite seleccionar la configuración de almacenamiento predeterminada, que identifica qué implementación de SRP utilizar.

En autor, para acceder a la consola Configuración de almacenamiento

* Iniciar sesión con privilegios de administrador
* Desde el **menú principal**

   * Seleccionar **[!UICONTROL Herramientas]** (del panel izquierdo)
   * Seleccionar **[!UICONTROL Communities]**
   * Seleccionar **[!UICONTROL Configuración de almacenamiento]**

      * Por ejemplo, la ubicación resultante es: [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)

     >[!NOTE]
     >
     >La configuración de almacenamiento predeterminada ahora se almacena en conf path(`/conf/global/settings/community/srpc/defaultconfiguration`) en lugar de `etc` ruta (`/etc/socialconfig/srpc/defaultconfiguration`). Se le aconseja que siga las [pasos de migración](#zerodt-migration-steps) para que defaultsrp funcione según lo esperado.

  ![dsrp-config](assets/dsrp-config.png)

* Seleccionar **[!UICONTROL Proveedor de recursos de almacenamiento de bases de datos (DSRP)]**
* **Configuración de la base de datos**

   * **[!UICONTROL Nombre de la fuente de datos JDBC]**

     El nombre dado a la conexión MySQL debe ser el mismo que se introdujo en [Configuración OSGi de JDBC](dsrp-mysql.md#configurejdbcconnections)

     *predeterminado*: comunidades

   * **[!UICONTROL Nombre de la base de datos]**

     Nombre dado al esquema en [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script) script

     *predeterminado*: comunidades

* **SolrConfiguration**

   * **[](https://solr.apache.org/guide/6_6/using-zookeeper-to-manage-configuration-files.html)Host de Zookeeper**

     Deje este valor en blanco si ejecuta Solr con el ZooKeeper interno. De lo contrario, al correr [Modo SolrCloud](solr.md#solrcloud-mode) con un ZooKeeper externo, establezca este valor en el URI del ZooKeeper, como *my.server.com:80*

     *predeterminado*: *&lt;blank>*

   * **[!UICONTROL URL de Solr]**

     *predeterminado*: https://127.0.0.1:8983/solr/

   * **[!UICONTROL Colección Solr]**

     *predeterminado*: colección1

* Seleccione **[!UICONTROL Enviar]**.

### Pasos de migración sin tiempo de inactividad para defaultsrp {#zerodt-migration-steps}

Para asegurarse de que la página predeterminada es [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) funciona según lo esperado, siga estos pasos:

1. Cambie el nombre de la ruta en `/etc/socialconfig` hasta `/etc/socialconfig_old`, para que la configuración del sistema vuelva a jsrp (valor predeterminado).
1. Ir a la página defaultsrp [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp), donde jsrp está configurado. Haga clic en **[!UICONTROL enviar]** para que se cree el nuevo nodo de configuración predeterminado en `/conf/global/settings/community/srpc`.
1. Eliminar la configuración predeterminada creada `/conf/global/settings/community/srpc/defaultconfiguration`.
1. Copiar la configuración antigua `/etc/socialconfig_old/srpc/defaultconfiguration` en lugar del nodo eliminado (`/conf/global/settings/community/srpc/defaultconfiguration`) en el paso anterior.
1. Eliminar el antiguo `etc` nodo `/etc/socialconfig_old`.

## Publicación de la configuración {#publishing-the-configuration}

DSRP debe identificarse como el almacén común en todas las instancias de autor y publicación.

Para que la configuración idéntica esté disponible en el entorno de publicación:

* En autor:

   * Vaya del menú principal a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Replicación]**
   * Doble clic **[!UICONTROL Activar árbol]**
   * **Ruta de inicio**:

      * Navegar a `/etc/socialconfig/srpc/`

   * Asegurar `Only Modified` no está seleccionado.
   * Seleccionar **[!UICONTROL Activar]**.

## Administración de datos de usuario {#managing-user-data}

Para obtener información sobre *usuarios*, *perfiles de usuario* y *grupos de usuarios*, introducidas a menudo en el entorno de publicación, visite:

* [Sincronización de usuarios](sync.md)
* [Administración de usuarios y grupos de usuarios](users.md)

## Reindexación de Solr para DSRP {#reindexing-solr-for-dsrp}

Para reindexar DSRP Solr, siga la documentación de [reindexación de MSRP](msrp.md#msrp-reindex-tool)Sin embargo, cuando vuelva a indexar para DSRP, utilice esta URL en su lugar: **/services/social/datastore/rdb/reindex**

Por ejemplo, un comando curl para reindexar DSRP tendría este aspecto:

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```
