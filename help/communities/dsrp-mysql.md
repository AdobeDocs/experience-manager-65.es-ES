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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuración de MySQL para DSRP {#mysql-configuration-for-dsrp}

MySQL es una base de datos relacional que puede utilizarse para almacenar contenido generado por el usuario (UGC).

Estas instrucciones describen cómo conectarse al servidor MySQL y establecer la base de datos UGC.

## Requisitos {#requirements}

* [paquete de funciones de las últimas comunidades](deploy-communities.md#latestfeaturepack)
* [Controlador JDBC para MySQL](deploy-communities.md#jdbc-driver-for-mysql)
* Base de datos relacional:

   * [MySQL Server](https://dev.mysql.com/downloads/mysql/) Community Server versión 5.6 o posterior

      * Puede ejecutarse en el mismo host que AEM o de forma remota
   * [Área de trabajo de MySQL](https://dev.mysql.com/downloads/tools/workbench/)


## Instalación de MySQL {#installing-mysql}

[MySQL](https://dev.mysql.com/downloads/mysql/) debe descargarse e instalarse siguiendo las instrucciones para el sistema operativo de destino.

### Nombres de tablas en minúsculas {#lower-case-table-names}

Como SQL no distingue entre mayúsculas y minúsculas, en los sistemas operativos que distinguen entre mayúsculas y minúsculas, es necesario incluir una configuración para reducir el uso de mayúsculas y minúsculas en todos los nombres de tabla.

Por ejemplo, para especificar todos los nombres de tabla en minúsculas en un sistema operativo Linux:

* Editar archivo `/etc/my.cnf`
* En la `[mysqld]` sección, agregue la línea siguiente:

   `lower_case_table_names = 1`

### Conjunto de caracteres UTF8 {#utf-character-set}

Para ofrecer una mejor compatibilidad multilingüe, es necesario utilizar el conjunto de caracteres UTF8.

Cambie MySQL para que tenga UTF8 como conjunto de caracteres:

* mysql> SET NAMES &#39;utf8&#39;;

Cambie la base de datos MySQL a UTF8 de forma predeterminada:

* Editar archivo `/etc/my.cnf`
* En la `[client]` sección, agregue la línea siguiente:

   `default-character-set=utf8`

* En la `[mysqld]` sección, agregue la línea siguiente:

   `character-set-server=utf8`

## Instalación de MySQL Workbench {#installing-mysql-workbench}

MySQL Workbench proporciona una interfaz de usuario para ejecutar secuencias de comandos SQL que instalan el esquema y los datos iniciales.

MySQL Workbench debe descargarse e instalarse siguiendo las instrucciones del sistema operativo de destino.

## Conexión de comunidades {#communities-connection}

Cuando MySQL Workbench se inicia por primera vez, a menos que ya se esté utilizando para otros fines, aún no mostrará ninguna conexión:

![chlimage_1-104](assets/chlimage_1-104.png)

### Nueva configuración de conexión {#new-connection-settings}

1. Seleccione el `+` icono a la derecha de `MySQL Connections`.
1. En el cuadro de diálogo `Setup New Connection`, introduzca los valores adecuados para la plataforma

   Para fines de demostración, con la instancia de AEM de autor y MySQL en el mismo servidor:

   * Nombre de la conexión: `Communities`
   * Método de conexión: `Standard (TCP/IP)`
   * Hostname: `127.0.0.1`
   * Nombre de usuario: `root`
   * Contraseña: `no password by default`
   * Esquema predeterminado: `leave blank`

1. Seleccione `Test Connection` para verificar la conexión con el servicio MySQL en ejecución

**Notas**:

* El puerto predeterminado es `3306`
* El nombre de conexión elegido se introduce como nombre de origen de datos en la configuración OSGi de [JDBC](#configurejdbcconnections)

#### Nueva conexión de comunidades {#new-communities-connection}

![chlimage_1-105](assets/chlimage_1-105.png)

## Configuración de base de datos {#database-setup}

Abra la conexión Comunidades para instalar la base de datos.

![chlimage_1-106](assets/chlimage_1-106.png)

### Obtención del script SQL {#obtain-the-sql-script}

La secuencia de comandos SQL se obtiene del repositorio de AEM:

1. Navegar a CRXDE Lite

   * Por ejemplo, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. Seleccione la carpeta /libs/social/config/datastore/dsrp/schema
1. Descargar `init-schema.sql`

![chlimage_1-107](assets/chlimage_1-107.png)

Un método para descargar el esquema es

* Seleccione el `jcr:content`nodo para el archivo sql
* Observe que el valor de la `jcr:data`propiedad es un vínculo de vista

* Seleccione el vínculo de vista para guardar los datos en un archivo local

### Crear la base de datos DSRP {#create-the-dsrp-database}

Siga los pasos a continuación para instalar la base de datos. El nombre predeterminado de la base de datos es `communities`.

Si se cambia el nombre de la base de datos en la secuencia de comandos, asegúrese de cambiarlo también en la configuración [de](#configurejdbcconnections)JDBC.

#### Paso 1: abrir archivo SQL {#step-open-sql-file}

En el área de trabajo de MySQL

* Desde el menú desplegable Archivo
* Seleccione el `init_schema.sql`

![chlimage_1-108](assets/chlimage_1-108.png)

#### Paso 2: ejecutar script SQL {#step-execute-sql-script}

En la ventana Workbench del archivo abierto en el paso 1, seleccione el `lightening (flash) icon` para ejecutar la secuencia de comandos.

En la siguiente imagen, el `init_schema.sql` archivo está listo para ejecutarse:

![chlimage_1-109](assets/chlimage_1-109.png)

#### Actualizar {#refresh}

Una vez ejecutada la secuencia de comandos, es necesario actualizar la `SCHEMAS`sección de la `Navigator` para poder ver la nueva base de datos. Utilice el icono de actualización a la derecha de &#39;SCHEMAS&#39;:

![chlimage_1-110](assets/chlimage_1-110.png)

## Configurar conexión JDBC {#configure-jdbc-connection}

La configuración OSGi para el grupo **de conexiones JDBC** Day Commons configura el controlador JDBC MySQL.

Todas las instancias de AEM de publicación y creación deben apuntar al mismo servidor MySQL.

Cuando MySQL se ejecuta en un servidor diferente de AEM, el nombre de host del servidor debe especificarse en lugar de &#39;localhost&#39; en el conector JDBC.

* En cada instancia de AEM de creación y publicación
* Inicio de sesión con privilegios de administrador
* Acceso a la consola [web](../../help/sites-deploying/configuring-osgi.md)

   * Por ejemplo, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)

* Localice la variable `Day Commons JDBC Connections Pool`
* Seleccione el icono `+` para crear una nueva configuración de conexión

![chlimage_1-111](assets/chlimage_1-111.png)

* Introduzca los valores siguientes:

   * **[!UICONTROL Clase]** de controlador JDBC: `com.mysql.jdbc.Driver`
   * **[!UICONTROL URI]** de conexión JDBC: `jdbc:mysql://localhost:3306/communities?characterEncoding=UTF-8`

      Especifique el servidor en lugar de localhost si MySQL Server no es igual que &#39;this&#39; AEM Server

      *comunidades* es el nombre predeterminado de base de datos (esquema)

   * **[!UICONTROL Nombre de usuario]**: `root`

      O escriba el nombre de usuario configurado para el servidor MySQL, si no es &quot;root&quot;

   * **[!UICONTROL Contraseña]**:

      Borre este campo si no hay ninguna contraseña establecida para MySQL,

      especifique la contraseña configurada para el nombre de usuario de MySQL
   * **[!UICONTROL Nombre]** del origen de datos: nombre introducido para la conexión [](#new-connection-settings)MySQL, por ejemplo, &#39;comunidades&#39;

* Seleccione **[!UICONTROL Guardar]**

