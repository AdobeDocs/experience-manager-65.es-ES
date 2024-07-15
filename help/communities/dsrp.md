---
title: 'DSRP: proveedor de recursos de almacenamiento de base de datos relacional'
description: Configure AEM Communities para que utilice una base de datos relacional como almacén común
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 15b3a594-efde-4702-9233-232ba1c7e5b0
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# DSRP: proveedor de recursos de almacenamiento de base de datos relacional {#dsrp-relational-database-storage-resource-provider}

## Acerca de DSRP {#about-dsrp}

Cuando AEM Communities está configurado para utilizar una base de datos relacional como almacén común, el contenido generado por el usuario (UGC) es accesible desde todas las instancias de autor y publicación sin necesidad de sincronización ni replicación.

Vea también [Características de las opciones de SRP](working-with-srp.md#characteristics-of-srp-options) y [Topologías recomendadas](topologies.md).

## Requisitos  {#requirements}

* [MySQL](#mysql-configuration), una base de datos relacional.
* [Apache Solr](#solr-configuration), una plataforma de búsqueda.

>[!NOTE]
>
>La configuración de almacenamiento predeterminada ahora se almacena en la ruta de acceso conf (`/conf/global/settings/community/srpc/defaultconfiguration`) en lugar de en la ruta de acceso `etc` (`/etc/socialconfig/srpc/defaultconfiguration`). Se le aconseja que siga los [pasos de migración](#zerodt-migration-steps) para que defaultsrp funcione según lo esperado.

## Configuración de base de datos relacional {#relational-database-configuration}

### Configuración de MySQL {#mysql-configuration}

Una instalación de MySQL puede compartirse entre características de habilitación y almacén común (DSRP) dentro del mismo grupo de conexiones utilizando nombres de base de datos (esquema) diferentes y también diferentes conexiones (servidor:puerto).

Para obtener detalles de instalación y configuración, consulte [Configuración de MySQL para DSRP](dsrp-mysql.md).

### Configuración de Solr {#solr-configuration}

Una instalación de Solr se puede compartir entre el almacén de nodos (Oak) y el almacén común (SRP) utilizando diferentes colecciones.

Si las colecciones Oak y SRP se utilizan de forma intensiva, se puede instalar un segundo Solr por motivos de rendimiento.

Para entornos de producción, el modo SolrCloud proporciona un rendimiento mejorado con respecto al modo independiente (una única configuración de Solr local).

Para obtener detalles de instalación y configuración, consulte [Configuración de Solr para SRP](solr.md).

### Seleccionar DSRP {#select-dsrp}

La [consola de configuración de almacenamiento](srp-config.md) permite seleccionar la configuración de almacenamiento predeterminada, que identifica qué implementación de SRP utilizar.

En autor, para acceder a la consola Configuración de almacenamiento

* Iniciar sesión con privilegios de administrador
* Desde el **menú principal**

   * Seleccione **[!UICONTROL Herramientas]** (en el panel izquierdo)
   * Seleccionar **[!UICONTROL comunidades]**
   * Seleccionar **[!UICONTROL configuración de almacenamiento]**

      * Por ejemplo, la ubicación resultante es: [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)

     >[!NOTE]
     >
     >La configuración de almacenamiento predeterminada ahora se almacena en la ruta de acceso conf(`/conf/global/settings/community/srpc/defaultconfiguration`)      en lugar de la ruta de acceso `etc` (`/etc/socialconfig/srpc/defaultconfiguration`). Se le aconseja que siga los [pasos de migración](#zerodt-migration-steps) para que defaultsrp funcione según lo esperado.

  ![dsrp-config](assets/dsrp-config.png)

* Seleccione **[!UICONTROL Proveedor de recursos de almacenamiento de la base de datos (DSRP)]**
* **Configuración de base de datos**

   * **[!UICONTROL Nombre de origen de datos JDBC]**

     El nombre dado a la conexión MySQL debe ser el mismo que se introdujo en [Configuración OSGi de JDBC](dsrp-mysql.md#configurejdbcconnections)

     *predeterminado*: comunidades

   * **[!UICONTROL Nombre de base de datos]**

     Nombre dado al esquema en el script [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script)

     *predeterminado*: comunidades

* **ConfiguraciónSolr**

   * **[Zookeeper](https://solr.apache.org/guide/6_6/using-zookeeper-to-manage-configuration-files.html) Host**

     Deje este valor en blanco si ejecuta Solr con el ZooKeeper interno. De lo contrario, cuando se ejecuta en [modo SolrCloud](solr.md#solrcloud-mode) con un ZooKeeper externo, establezca este valor en el URI del ZooKeeper, como *my.server.com:80*

     *predeterminado*: *&lt;en blanco>*

   * **[!UICONTROL URL de Solr]**

     *valor predeterminado*: https://127.0.0.1:8983/solr/

   * **[!UICONTROL Colección Solr]**

     *predeterminado*: colección1

* Seleccione **[!UICONTROL Enviar]**.

### Pasos de migración sin tiempo de inactividad para defaultsrp {#zerodt-migration-steps}

Para asegurarse de que la página defaultsrp [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) funciona según lo esperado, siga estos pasos:

1. Cambie el nombre de la ruta de acceso en `/etc/socialconfig` a `/etc/socialconfig_old`, de modo que la configuración del sistema vuelva a jsrp (valor predeterminado).
1. Vaya a la página defaultsrp [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp), donde está configurado jsrp. Haga clic en el botón **[!UICONTROL submit]** para que se cree un nuevo nodo de configuración predeterminado en `/conf/global/settings/community/srpc`.
1. Elimine la configuración predeterminada creada `/conf/global/settings/community/srpc/defaultconfiguration`.
1. Copie la configuración antigua `/etc/socialconfig_old/srpc/defaultconfiguration` en lugar del nodo eliminado (`/conf/global/settings/community/srpc/defaultconfiguration`) en el paso anterior.
1. Elimine el nodo `etc` anterior `/etc/socialconfig_old`.

## Publicación de la configuración {#publishing-the-configuration}

DSRP debe identificarse como el almacén común en todas las instancias de autor y publicación.

Para que la configuración idéntica esté disponible en el entorno de publicación:

* En autor:

   * Vaya del menú principal a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Replicación]**
   * Haga doble clic en **[!UICONTROL Activar árbol]**
   * **Ruta de inicio**:

      * Examinar `/etc/socialconfig/srpc/`

   * Asegúrese de que `Only Modified` no esté seleccionado.
   * Seleccione **[!UICONTROL Activar]**.

## Administración de datos de usuario {#managing-user-data}

Para obtener información sobre *usuarios*, *perfiles de usuario* y *grupos de usuarios* que se especifican con frecuencia en el entorno de publicación, visite:

* [Sincronización de usuarios](sync.md)
* [Administración de usuarios y grupos de usuarios](users.md)

## Reindexación de Solr para DSRP {#reindexing-solr-for-dsrp}

Para reindexar DSRP Solr, siga la documentación de [reindexación de MSRP](msrp.md#msrp-reindex-tool), sin embargo, cuando vuelva a indexar para DSRP, utilice esta URL en su lugar: **/services/social/datastore/rdb/reindex**

Por ejemplo, un comando curl para reindexar DSRP tendría este aspecto:

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```
