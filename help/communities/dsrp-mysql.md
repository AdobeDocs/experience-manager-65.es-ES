---
title: Configuración de MySQL para DSRP
seo-title: MySQL Configuration for DSRP
description: Cómo conectarse al servidor MySQL y establecer la base de datos UGC
seo-description: How to connect to the MySQL server and establish the UGC database
uuid: c058cc88-7ca2-4aed-9a36-b080e603f886
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: edc3043c-7ec4-4e4a-b008-95f1784f012e
role: Admin
exl-id: eafb60be-2963-4ac9-8618-50fd9bc6fe6c
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 3%

---

# Configuración de MySQL para DSRP {#mysql-configuration-for-dsrp}

MySQL es una base de datos relacional que se puede utilizar para almacenar contenido generado por el usuario (UGC).

Estas instrucciones describen cómo conectarse al servidor MySQL y establecer la base de datos UGC.

## Requisitos  {#requirements}

* [Último paquete de funciones de Communities](deploy-communities.md#latestfeaturepack)
* [Controlador JDBC para MySQL](deploy-communities.md#jdbc-driver-for-mysql)
* Una base de datos relacional:

   * [servidor MySQL](https://dev.mysql.com/downloads/mysql/) Community Server versión 5.6 o posterior

      * AEM Puede ejecutarse en el mismo host que el servidor de correo o puede ejecutarse de forma remota.

   * [MySQL Workbench](https://dev.mysql.com/downloads/tools/workbench/)

## Instalación de MySQL {#installing-mysql}

[MySQL](https://dev.mysql.com/downloads/mysql/) debe descargarse e instalarse siguiendo las instrucciones para el sistema operativo de destino.

### Nombres de tabla en minúsculas {#lower-case-table-names}

Como SQL no distingue entre mayúsculas y minúsculas, en los sistemas operativos que distinguen entre mayúsculas y minúsculas es necesario incluir una configuración para que todos los nombres de tabla estén en minúsculas.

Por ejemplo, para especificar todos los nombres de tablas en minúsculas en un sistema operativo Linux:

* Editar archivo `/etc/my.cnf`
* En el `[mysqld]` , añada la línea siguiente:

  `lower_case_table_names = 1`

### Conjunto de caracteres UTF8 {#utf-character-set}

Para proporcionar una mejor compatibilidad multilingüe, es necesario utilizar el conjunto de caracteres UTF8.

Cambie MySQL para que tenga UTF8 como conjunto de caracteres:

* mysql > SET NAMES &#39;utf8&#39;;

Cambie la base de datos MySQL a UTF8 de forma predeterminada:

* Editar archivo `/etc/my.cnf`
* En el `[client]` , añada la línea siguiente:

  `default-character-set=utf8`

* En el `[mysqld]` , añada la línea siguiente:

  `character-set-server=utf8`

## Instalación de MySQL Workbench {#installing-mysql-workbench}

MySQL Workbench proporciona una interfaz de usuario para ejecutar scripts SQL que instalan el esquema y los datos iniciales.

MySQL Workbench debe descargarse e instalarse siguiendo las instrucciones para el sistema operativo de destino.

## Conexión de Communities {#communities-connection}

Cuando se inicia por primera vez MySQL Workbench, a menos que ya se esté utilizando para otros fines, aún no se mostrará ninguna conexión:

![mysqlconnection](assets/mysqlconnection.png)

### Nueva configuración de conexión {#new-connection-settings}

1. Seleccione el `+` a la derecha de `MySQL Connections`.
1. En el diálogo `Setup New Connection`, introduzca los valores adecuados para su plataforma

   AEM Para fines de demostración, con la instancia de creación de la aplicación y con MySQL en el mismo servidor:

   * Nombre de la conexión: `Communities`
   * Método de conexión: `Standard (TCP/IP)`
   * Nombre de host: `127.0.0.1`
   * Nombre de usuario: `root`
   * Una contraseña: `no password by default`
   * Esquema predeterminado: `leave blank`

1. Seleccionar `Test Connection` para comprobar la conexión con el servicio MySQL en ejecución

**Notas**:

* El puerto predeterminado es `3306`
* El nombre de conexión seleccionado se introduce como nombre de la fuente de datos en [Configuración OSGi de JDBC](#configurejdbcconnections)

#### Nueva conexión de Communities {#new-communities-connection}

![community-connection](assets/community-connection.png)

## Configuración de base de datos {#database-setup}

Abra la conexión Communities para instalar la base de datos.

![install-database](assets/install-database.png)

### Obtener el script SQL {#obtain-the-sql-script}

AEM La secuencia de comandos SQL se obtiene del repositorio de:

1. Navegar al CRXDE Lite

   * Por ejemplo, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. Seleccione la carpeta /libs/social/config/datastore/dsrp/schema
1. Descargar `init-schema.sql`

   ![database-schema-crxde](assets/database-schema-crxde.png)

Un método para descargar el esquema es el siguiente:

* Seleccione el `jcr:content` nodo para el archivo sql
* Observe el valor de `jcr:data` La propiedad es un vínculo de vista

* Seleccione el vínculo de vista para guardar los datos en un archivo local

### Creación de la base de datos DSRP {#create-the-dsrp-database}

Siga los pasos a continuación para instalar la base de datos. El nombre predeterminado de la base de datos es `communities`.

Si el nombre de la base de datos se cambia en la secuencia de comandos, asegúrese de cambiarlo también en la [Configuración de JDBC](#configurejdbcconnections).

#### Paso 1: abrir el archivo SQL {#step-open-sql-file}

En MySQL Workbench

* En el menú desplegable Archivo, seleccione **[!UICONTROL Abrir script SQL]** opción
* Seleccione el descargado `init_schema.sql` script

![select-sql-script](assets/select-sql-script.png)

#### Paso 2: Ejecutar Script SQL {#step-execute-sql-script}

En la ventana de Workbench para el archivo abierto en el paso 1, seleccione `lightening (flash) icon` para ejecutar la secuencia de comandos.

En la siguiente imagen, la variable `init_schema.sql` el archivo está listo para ejecutarse:

![execute-sql-script](assets/execute-sql-script.png)

#### Actualizar {#refresh}

Una vez ejecutado el script, es necesario actualizar el `SCHEMAS` de la sección `Navigator` para ver la nueva base de datos. Utilice el icono de actualización a la derecha de &quot;ESQUEMAS&quot;:

![refresh-schema](assets/refresh-schema.png)

## Configurar conexión JDBC {#configure-jdbc-connection}

La configuración OSGi para **Grupo de conexiones JDBC de Day Commons** configura el Controlador JDBC de MySQL.

AEM Todas las instancias de publicación y de creación de la instancia de deben apuntar al mismo servidor MySQL.

AEM Cuando MySQL se ejecuta en un servidor diferente de, se debe especificar el nombre de host del servidor en lugar de &quot;localhost&quot; en el conector JDBC.

* AEM En cada instancia de autor y publicación de la.
* Ha iniciado sesión con privilegios de administrador.
* Acceda a la [consola web](../../help/sites-deploying/configuring-osgi.md).

   * Por ejemplo, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)

* Busque el `Day Commons JDBC Connections Pool`
* Seleccione el `+` para crear una nueva configuración de conexión.

  ![configure-jdbc-connection](assets/configure-jdbc-connection.png)

* Introduzca los siguientes valores:

   * **[!UICONTROL Clase de controlador JDBC]**: `com.mysql.jdbc.Driver`
   * **[!UICONTROL URI de conexión JDBC]**: `jdbc:mysql://localhost:3306/communities?characterEncoding=UTF-8`

     AEM Especifique el servidor en lugar del host local si el servidor MySQL no es el mismo que el servidor de &quot;este&quot; servidor de *comunidades* es el nombre predeterminado de la base de datos (esquema).

   * **[!UICONTROL Nombre de usuario]**: `root`

     O introduzca el nombre de usuario configurado para el servidor MySQL, si no es &quot;root&quot;.

   * **[!UICONTROL Contraseña]**:

     Borrar este campo si no se ha definido ninguna contraseña para MySQL,

     de lo contrario, introduzca la contraseña configurada para el nombre de usuario de MySQL.

   * **[!UICONTROL Nombre de Datasource]**: nombre introducido para el [Conexión MySQL](#new-connection-settings), por ejemplo, &quot;comunidades&quot;.

* Seleccione **[!UICONTROL Guardar]**
