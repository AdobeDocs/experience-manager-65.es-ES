---
title: DSRP - Proveedor de recursos de almacenamiento de bases de datos relacionales
seo-title: DSRP - Proveedor de recursos de almacenamiento de bases de datos relacionales
description: Configuración de AEM Communities para utilizar una base de datos relacional como su tienda común
seo-description: Configuración de AEM Communities para utilizar una base de datos relacional como su tienda común
uuid: f364e7da-ee54-4ab2-a630-7ec9239005ac
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d23acb18-6761-4290-9e7a-a434582791bd
role: Admin
exl-id: 15b3a594-efde-4702-9233-232ba1c7e5b0
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 3%

---

# DSRP - Proveedor de recursos de almacenamiento de bases de datos relacionales {#dsrp-relational-database-storage-resource-provider}

## Acerca de DSRP {#about-dsrp}

Cuando AEM Communities está configurado para utilizar una base de datos relacional como su almacén común, el contenido generado por el usuario (UGC) es accesible desde todas las instancias de autor y publicación sin necesidad de sincronización ni replicación.

Consulte también [Características de las opciones de SRP](working-with-srp.md#characteristics-of-srp-options) y [Topologías recomendadas](topologies.md).

## Requisitos {#requirements}

* [MySQL](#mysql-configuration), una base de datos relacional.
* [Apache Solr](#solr-configuration), una plataforma de búsqueda.

>[!NOTE]
>
>La configuración de almacenamiento predeterminada ahora se almacena en ruta conf(`/conf/global/settings/community/srpc/defaultconfiguration`) en lugar de en ruta de acceso etc (`/etc/socialconfig/srpc/defaultconfiguration`). Se recomienda seguir los [pasos de migración](#zerodt-migration-steps) para que defaultsrp funcione según lo esperado.

## Configuración de base de datos relacional {#relational-database-configuration}

### Configuración de MySQL {#mysql-configuration}

Una instalación de MySQL puede compartirse entre las características de habilitación y el almacén común (DSRP) dentro del mismo grupo de conexiones utilizando diferentes nombres de base de datos (esquema) y también diferentes conexiones (servidor:puerto).

Para obtener más información sobre la instalación y configuración, consulte [Configuración MySQL para DSRP](dsrp-mysql.md).

### Configuración de Solr {#solr-configuration}

Una instalación de Solr se puede compartir entre el almacén de nodos (Oak) y el almacén común (SRP) utilizando diferentes colecciones.

Si las colecciones Oak y SRP se utilizan intensamente, puede instalarse un segundo Solr por motivos de rendimiento.

Para los entornos de producción, el modo SolrCloud proporciona un rendimiento mejorado con respecto al modo independiente (una única configuración local de Solr).

Para obtener más información sobre la instalación y configuración, consulte [Configuración de Solr para SRP](solr.md).

### Seleccionar DSRP {#select-dsrp}

La [consola de configuración de almacenamiento](srp-config.md) permite seleccionar la configuración de almacenamiento predeterminada, que identifica qué implementación de SRP utilizar.

Al autor, para acceder a la consola de configuración de almacenamiento

* Iniciar sesión con privilegios de administrador
* Desde el **menú principal**

   * Seleccionar **[!UICONTROL Herramientas]** (en el panel izquierdo)
   * Seleccione **[!UICONTROL Communities]**
   * Seleccione **[!UICONTROL Configuración de almacenamiento]**

      * Por ejemplo, la ubicación resultante es: [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >La configuración de almacenamiento predeterminada ahora se almacena en la ruta conf(`/conf/global/settings/community/srpc/defaultconfiguration`)      en lugar de etc ruta (`/etc/socialconfig/srpc/defaultconfiguration`). Se recomienda seguir los [pasos de migración](#zerodt-migration-steps) para que defaultsrp funcione según lo esperado.
   ![dsrp-config](assets/dsrp-config.png)

* Seleccione **[!UICONTROL Proveedor de recursos de almacenamiento de bases de datos (DSRP)]**
* **Configuración de la base de datos**

   * **[!UICONTROL Nombre de la fuente de datos JDBC]**

      El nombre proporcionado a la conexión MySQL debe ser el mismo que se introdujo en la configuración [JDBC OSGi](dsrp-mysql.md#configurejdbcconnections)

      *predeterminado*: comunidades

   * **[!UICONTROL Nombre de la base de datos]**

      Nombre dado al esquema en la secuencia de comandos [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script)

      *predeterminado*: comunidades

* **SolrConfiguration**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Host de Zookeeper**

      Deje este valor en blanco si ejecuta Solr utilizando el ZooKeeper interno. Si no, cuando se ejecuta en [modo SolrCloud](solr.md#solrcloud-mode) con un ZooKeeper externo, establezca este valor en el URI del ZooKeeper, como *my.server.com:80*

      *predeterminado*:  *&lt;blank>*

   * **[!UICONTROL URL de Solr]**

      *predeterminado*: https://127.0.0.1:8983/solr/

   * **[!UICONTROL Colección Solr]**

      *predeterminado*: colección1

* Seleccione **[!UICONTROL Enviar]**.

### Pasos de migración de tiempo de inactividad cero para defaultsrp {#zerodt-migration-steps}

Siga estos pasos para asegurarse de que la página predeterminada [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) funciona según lo esperado:

1. Cambie el nombre de la ruta de `/etc/socialconfig` a `/etc/socialconfig_old`, de modo que la configuración del sistema vuelva a jsrp(predeterminado).
1. Vaya a la página predeterminada [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp), donde jsrp está configurado. Haga clic en el botón **[!UICONTROL submit]** para crear el nuevo nodo de configuración predeterminado en `/conf/global/settings/community/srpc`.
1. Elimine la configuración predeterminada creada `/conf/global/settings/community/srpc/defaultconfiguration`.
1. Copie la configuración antigua `/etc/socialconfig_old/srpc/defaultconfiguration` en lugar del nodo eliminado (`/conf/global/settings/community/srpc/defaultconfiguration`) en el paso anterior.
1. Elimine el nodo antiguo de etc `/etc/socialconfig_old`.

## Publicación de la configuración {#publishing-the-configuration}

El DSRP debe identificarse como el almacén común en todas las instancias de autor y publicación.

Para que la configuración idéntica esté disponible en el entorno de publicación:

* Sobre el autor:

   * Vaya del menú principal a **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Replication]**
   * Haga doble clic en **[!UICONTROL Activar árbol]**
   * **Ruta de inicio**:

      * Vaya a `/etc/socialconfig/srpc/`
   * Asegúrese de que `Only Modified` no esté seleccionado.
   * Seleccione **[!UICONTROL Activate]**.


## Administración de datos de usuario {#managing-user-data}

Para obtener información sobre *usuarios*, *perfiles de usuario* y *grupos de usuarios*, que a menudo se introducen en el entorno de publicación, visite:

* [Sincronización de usuarios](sync.md)
* [Administración de usuarios y grupos de usuarios](users.md)

## Reindexación de Solr para DSRP {#reindexing-solr-for-dsrp}

Para reindexar DSRP Solr, siga la documentación de [reindexación de MSRP](msrp.md#msrp-reindex-tool), sin embargo, al reindexar para DSRP, utilice esta URL en su lugar: **/services/social/datastore/rdb/reindex**

Por ejemplo, un comando curl para reindexar DSRP tendría este aspecto:

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```
