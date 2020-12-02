---
title: DSRP - Proveedor de recursos de Almacenamiento de base de datos relacional
seo-title: DSRP - Proveedor de recursos de Almacenamiento de base de datos relacional
description: Configure AEM Communities para utilizar una base de datos relacional como su almacén común
seo-description: Configure AEM Communities para utilizar una base de datos relacional como su almacén común
uuid: f364e7da-ee54-4ab2-a630-7ec9239005ac
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d23acb18-6761-4290-9e7a-a434582791bd
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 3%

---


# DSRP - Proveedor de recursos de Almacenamiento de base de datos relacional {#dsrp-relational-database-storage-resource-provider}

## Acerca de DSRP {#about-dsrp}

Cuando AEM Communities está configurado para utilizar una base de datos relacional como su almacén común, el contenido generado por el usuario (UGC) es accesible desde todas las instancias de creación y publicación sin necesidad de sincronización ni replicación.

Consulte también [Características de las opciones de SRP](working-with-srp.md#characteristics-of-srp-options) y [Topologías recomendadas](topologies.md).

## Requisitos {#requirements}

* [MySQL](#mysql-configuration), una base de datos relacional.
* [Apache Solr](#solr-configuration), una plataforma de búsqueda.

>[!NOTE]
>
>La configuración de almacenamiento predeterminada ahora se almacena en ruta conf(`/conf/global/settings/community/srpc/defaultconfiguration`) en lugar de ruta etc (`/etc/socialconfig/srpc/defaultconfiguration`). Se le aconseja que siga los [pasos de migración](#zerodt-migration-steps) para hacer que defaultsrp funcione según lo esperado.

## Configuración de base de datos relacional {#relational-database-configuration}

### Configuración de MySQL {#mysql-configuration}

Una instalación de MySQL puede compartirse entre las características de habilitación y el almacén común (DSRP) dentro del mismo grupo de conexiones utilizando diferentes nombres de base de datos (esquema) y también diferentes conexiones (server:port).

Para obtener más información sobre la instalación y configuración, consulte [Configuración de MySQL para DSRP](dsrp-mysql.md).

### Configuración de Solr {#solr-configuration}

Una instalación de Solr puede compartirse entre el almacén de nodos (Oak) y el almacén común (SRP) mediante diferentes colecciones.

Si las colecciones Oak y SRP se utilizan intensamente, se puede instalar un segundo Solr por motivos de rendimiento.

En el caso de los entornos de producción, el modo SolrCloud ofrece un rendimiento mejorado con respecto al modo independiente (una única configuración local de Solr).

Para obtener más información sobre la instalación y configuración, consulte [Configuración de Solr para SRP](solr.md).

### Seleccionar DSRP {#select-dsrp}

La [consola de configuración de Almacenamiento](srp-config.md) permite seleccionar la configuración de almacenamiento predeterminada, que identifica la implementación de SRP que se va a utilizar.

Al crear, para acceder a la consola de configuración de Almacenamiento

* Iniciar sesión con privilegios de administrador
* Desde el **menú principal**

   * Seleccione **[!UICONTROL Herramientas]** (del panel izquierdo)
   * Seleccionar **[!UICONTROL Comunidades]**
   * Seleccione **[!UICONTROL Configuración de Almacenamiento]**

      * Por ejemplo, la ubicación resultante es: [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >La configuración de almacenamiento predeterminada ahora se almacena en ruta de acceso conf(`/conf/global/settings/community/srpc/defaultconfiguration`)      en lugar de etc path (`/etc/socialconfig/srpc/defaultconfiguration`). Se le aconseja que siga los [pasos de migración](#zerodt-migration-steps) para hacer que defaultsrp funcione según lo esperado.
   ![dsrp-config](assets/dsrp-config.png)

* Seleccione **[!UICONTROL Proveedor de recursos de Almacenamiento de base de datos (DSRP)]**
* **Configuración de la base de datos**

   * **[!UICONTROL Nombre de la fuente de datos JDBC]**

      El nombre asignado a la conexión MySQL debe ser el mismo que se introdujo en la configuración OSGi de [JDBC](dsrp-mysql.md#configurejdbcconnections)

      *predeterminado*: comunidades

   * **[!UICONTROL Nombre de la base de datos]**

      Nombre dado al esquema en la secuencia de comandos [init_esquema.sql](dsrp-mysql.md#obtain-the-sql-script)

      *predeterminado*: comunidades

* **SolrConfiguration**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Host de Zookeeper**

      Deje este valor en blanco si ejecuta Solr utilizando el ZooKeeper interno. De lo contrario, cuando se ejecuta en [modo de SolrCloud](solr.md#solrcloud-mode) con un ZooKeeper externo, establezca este valor en el URI del ZooKeeper, como *my.server.com:80*

      *predeterminado*:  *&lt;blank>*

   * **[!UICONTROL URL de Solr]**

      *predeterminado*: https://127.0.0.1:8983/solr/

   * **[!UICONTROL Colección Solr]**

      *predeterminado*: collection1

* Seleccione **[!UICONTROL Enviar]**.

### Pasos de migración de tiempo de inactividad cero para defaultsrp {#zerodt-migration-steps}

Siga estos pasos para asegurarse de que la página predeterminada [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) funciona según lo esperado:

1. Cambie el nombre de la ruta de `/etc/socialconfig` a `/etc/socialconfig_old`, de modo que la configuración del sistema vuelva a jsrp(predeterminado).
1. Vaya a la página predeterminada [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp), donde jsrp está configurado. Haga clic en el botón **[!UICONTROL enviar]** para que se cree el nuevo nodo de configuración predeterminado en `/conf/global/settings/community/srpc`.
1. Elimine la configuración predeterminada `/conf/global/settings/community/srpc/defaultconfiguration` creada.
1. Copie la configuración anterior `/etc/socialconfig_old/srpc/defaultconfiguration` en lugar del nodo eliminado (`/conf/global/settings/community/srpc/defaultconfiguration`) en el paso anterior.
1. Elimine el nodo etc antiguo `/etc/socialconfig_old`.

## Publicación de la configuración {#publishing-the-configuration}

DSRP debe identificarse como el almacén común en todas las instancias de creación y publicación.

Para que la configuración idéntica esté disponible en el entorno de publicación:

* Sobre el autor:

   * Vaya del menú principal a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Replicación]**
   * Haga doble clic en **[!UICONTROL Activar árbol]**
   * **Ruta de inicio**:

      * Vaya a `/etc/socialconfig/srpc/`
   * Asegúrese de que `Only Modified` no está seleccionado.
   * Seleccione **[!UICONTROL Activar]**.


## Administración de datos de usuario {#managing-user-data}

Para obtener información acerca de *usuarios*, *perfiles de usuario* y *grupos de usuarios*, que a menudo se introducen en el entorno de publicación, visite:

* [Sincronización de usuarios](sync.md)
* [Administración de usuarios y grupos de usuarios](users.md)

## Reindexación de sol para DSRP {#reindexing-solr-for-dsrp}

Para volver a indexar DSRP Solr, siga la documentación de [reindexación de MSRP](msrp.md#msrp-reindex-tool); sin embargo, al volver a indexar para DSRP, utilice esta dirección URL en su lugar: **/services/social/datastore/rdb/reindex**

Por ejemplo, un comando curl para volver a indexar DSRP tendría este aspecto:

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```

