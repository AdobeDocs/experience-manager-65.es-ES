---
title: Configuración de MySQL para DSRP
seo-title: Configuración de MySQL para DSRP
description: Cómo conectarse al servidor MySQL y establecer la base de datos UGC
seo-description: Cómo conectarse al servidor MySQL y establecer la base de datos UGC
uuid: c058cc88-7ca2-4aed-9a36-b080e603f886
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: edc3043c-7ec4-4e4a-b008-95f1784f012e
translation-type: tm+mt
source-git-commit: 6693baecb1345c30385eb04caeb03960925f46c3
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 1%

---


# Configuración de MySQL para DSRP {#mysql-configuration-for-dsrp}

MySQL es una base de datos relacional que puede utilizarse para almacenar contenido generado por el usuario (UGC).

Estas instrucciones describen cómo conectarse al servidor MySQL y establecer la base de datos UGC.

## Requisitos {#requirements}

* [Paquete de funciones de las últimas comunidades](deploy-communities.md#latestfeaturepack)
* [Controlador JDBC para MySQL](deploy-communities.md#jdbc-driver-for-mysql)
* Base de datos relacional:

   * [MySQL ](https://dev.mysql.com/downloads/mysql/) serverCommunity Server versión 5.6 o posterior

      * Puede ejecutarse en el mismo host que AEM o de forma remota
   * [Área de trabajo de MySQL](https://dev.mysql.com/downloads/tools/workbench/)


## Instalación de MySQL {#installing-mysql}

[](https://dev.mysql.com/downloads/mysql/) MySQL debe descargarse e instalarse siguiendo las instrucciones para el sistema operativo destinatario.

### Nombres de tablas en minúscula {#lower-case-table-names}

Como SQL no distingue entre mayúsculas y minúsculas, en los sistemas operativos que distinguen entre mayúsculas y minúsculas, es necesario incluir una configuración para reducir el uso de mayúsculas y minúsculas en todos los nombres de tabla.

Por ejemplo, para especificar todos los nombres de tabla en minúsculas en un sistema operativo Linux:

* Editar archivo `/etc/my.cnf`
* En la sección `[mysqld]`, agregue la línea siguiente:

   `lower_case_table_names = 1`

### Conjunto de caracteres UTF8 {#utf-character-set}

Para ofrecer una mejor compatibilidad multilingüe, es necesario utilizar el conjunto de caracteres UTF8.

Cambie MySQL para que tenga UTF8 como conjunto de caracteres:

* mysql > NOMBRES SET &#39;utf8&#39;;

Cambie la base de datos MySQL a UTF8 de forma predeterminada:

* Editar archivo `/etc/my.cnf`
* En la sección `[client]`, agregue la línea siguiente:

   `default-character-set=utf8`

* En la sección `[mysqld]`, agregue la línea siguiente:

   `character-set-server=utf8`

## Instalación de MySQL Workbench {#installing-mysql-workbench}

MySQL Workbench proporciona una interfaz de usuario para ejecutar scripts SQL que instalan el esquema y los datos iniciales.

MySQL Workbench debe descargarse e instalarse siguiendo las instrucciones del sistema operativo destinatario.

## Conexión de comunidades {#communities-connection}

Cuando MySQL Workbench se inicia por primera vez, a menos que ya se esté utilizando para otros fines, aún no mostrará ninguna conexión:

![mysqlconnection](assets/mysqlconnection.png)

### Nueva configuración de conexión {#new-connection-settings}

1. Seleccione el icono `+` a la derecha de `MySQL Connections`.
1. En el cuadro de diálogo `Setup New Connection`, introduzca los valores adecuados para la plataforma

   Para fines de demostración, con el autor AEM instancia y MySQL en el mismo servidor:

   * Nombre de la conexión: `Communities`
   * Método de conexión: `Standard (TCP/IP)`
   * Nombre de host: `127.0.0.1`
   * Nombre de usuario: `root`
   * Contraseña: `no password by default`
   * Esquema predeterminado: `leave blank`

1. Seleccione `Test Connection` para verificar la conexión con el servicio MySQL en ejecución

**Notas**:

* El puerto predeterminado es `3306`
* El nombre de conexión elegido se introduce como nombre del origen de datos en la configuración [OSGi de JDBC](#configurejdbcconnections)

#### Nueva conexión de comunidades {#new-communities-connection}

![community-connection](assets/community-connection.png)

## Configuración de base de datos {#database-setup}

Abra la conexión Comunidades para instalar la base de datos.

![install-database](assets/install-database.png)

### Obtener el script SQL {#obtain-the-sql-script}

La secuencia de comandos SQL se obtiene del repositorio de AEM:

1. Ir al CRXDE Lite

   * Por ejemplo: [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. Seleccione la carpeta /libs/social/config/datastore/dsrp/esquema
1. Descargar `init-schema.sql`

   ![database-esquema-crxde](assets/database-schema-crxde.png)

Un método para descargar el esquema es:

* Seleccione el nodo `jcr:content` para el archivo sql
* Observe que el valor de la propiedad `jcr:data` es un vínculo de vista

* Seleccione el vínculo de vista para guardar los datos en un archivo local

### Crear la base de datos DSRP {#create-the-dsrp-database}

Siga los pasos a continuación para instalar la base de datos. El nombre predeterminado de la base de datos es `communities`.

Si se cambia el nombre de la base de datos en la secuencia de comandos, asegúrese de cambiarlo también en la [configuración JDBC](#configurejdbcconnections).

#### Paso 1: abrir archivo SQL {#step-open-sql-file}

En el área de trabajo de MySQL

* En el menú desplegable Archivo, seleccione la opción **[!UICONTROL Abrir script SQL]**
* Seleccione la secuencia de comandos `init_schema.sql` descargada

![select-sql-script](assets/select-sql-script.png)

#### Paso 2: ejecutar SQL Script {#step-execute-sql-script}

En la ventana Workbench del archivo abierto en el paso 1, seleccione `lightening (flash) icon` para ejecutar la secuencia de comandos.

En la siguiente imagen, el archivo `init_schema.sql` está listo para ejecutarse:

![execute-sql-script](assets/execute-sql-script.png)

#### Actualizar {#refresh}

Una vez ejecutada la secuencia de comandos, es necesario actualizar la sección `SCHEMAS` de `Navigator` para poder ver la nueva base de datos. Utilice el icono de actualización a la derecha de &#39;ESQUEMAS:

![refresh-esquema](assets/refresh-schema.png)

## Configurar la conexión JDBC {#configure-jdbc-connection}

La configuración OSGi para **Day Commons JDBC Connections Pool** configura el controlador JDBC de MySQL.

Todas las instancias de publicación y creación AEM deben apuntar al mismo servidor MySQL.

Cuando MySQL se ejecuta en un servidor diferente de AEM, el nombre de host del servidor debe especificarse en lugar de &#39;localhost&#39; en el conector JDBC.

* En cada instancia de creación y publicación AEM.
* Se ha iniciado sesión con privilegios de administrador.
* Acceda a la [consola web](../../help/sites-deploying/configuring-osgi.md).

   * Por ejemplo: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)

* Busque el `Day Commons JDBC Connections Pool`
* Seleccione el icono `+` para crear una nueva configuración de conexión.

   ![configure-jdbc-connection](assets/configure-jdbc-connection.png)

* Introduzca los valores siguientes:

   * **[!UICONTROL Clase]** de controlador JDBC:  `com.mysql.jdbc.Driver`
   * **[!UICONTROL URI]** de conexión JDBC:  `jdbc:mysql://localhost:3306/communities?characterEncoding=UTF-8`

      Especifique el servidor en lugar de localhost si el servidor MySQL no es el mismo que &#39;this&#39; AEM servidor *comunidades* es el nombre predeterminado de la base de datos (esquema).

   * **[!UICONTROL Nombre de usuario]**:  `root`

      O bien, introduzca el nombre de usuario configurado para el servidor MySQL, si no es &quot;root&quot;.

   * **[!UICONTROL Contraseña]**:

      Borre este campo si no hay ninguna contraseña establecida para MySQL,

      especifique la contraseña configurada para el nombre de usuario de MySQL.

   * **[!UICONTROL Nombre]** del origen de datos: nombre introducido para la conexión [ ](#new-connection-settings)MySQL, por ejemplo, &#39;comunidades&#39;.

* Seleccione **[!UICONTROL Guardar]**

