---
title: Configuración MySQL para características de habilitación
seo-title: MySQL Configuration for Enablement Features
description: Conexión del servidor MySQL
seo-description: Connecting your MySQL server
uuid: e02d9404-de75-4fdb-896c-ea3f64f980a3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 9222bc93-c231-4ac8-aa28-30d784a4ca3b
role: Admin
exl-id: 2d33e6ba-cd32-40d1-8983-58f636b21470
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 4%

---

# Configuración MySQL para características de habilitación {#mysql-configuration-for-enablement-features}

MySQL es una base de datos relacional que se utiliza principalmente para datos de informes y seguimiento de SCORM para recursos de habilitación. Se incluyen tablas para otras funciones, como el seguimiento de la pausa/reanudación de vídeo.

Estas instrucciones describen cómo conectar con el servidor MySQL, establecer la base de datos de habilitación y rellenar la base de datos con datos iniciales.

## Requisitos  {#requirements}

Antes de configurar la función de habilitación de MySQL para Communities, asegúrese de

* Instalar [Servidor MySQL](https://dev.mysql.com/downloads/mysql/) Servidor de comunidad versión 5.6:
   * La versión 5.7 no es compatible con SCORM.
   * Puede ser el mismo servidor que la instancia AEM autor.
* En todas las AEM instancias, instale el [Controlador JDBC para MySQL](deploy-communities.md#jdbc-driver-for-mysql).
* Instalar [Área de trabajo MySQL](https://dev.mysql.com/downloads/tools/workbench/).
* En todas AEM instancias, instale la variable [Paquete SCORM](enablement.md#scorm).

## Instalación de MySQL {#installing-mysql}

MySQL debe descargarse e instalarse siguiendo las instrucciones para el sistema operativo de destino.

### Nombres de tabla en minúsculas {#lower-case-table-names}

Como SQL no distingue entre mayúsculas y minúsculas, en los sistemas operativos que distinguen entre mayúsculas y minúsculas, es necesario incluir una configuración para que todos los nombres de tabla estén en minúsculas.

Por ejemplo, para especificar todos los nombres de tabla en minúsculas en un sistema operativo Linux:

* Editar archivo `/etc/my.cnf`
* En el `[mysqld]` , agregue la línea siguiente: `lower_case_table_names = 1`

### Conjunto de caracteres UTF8 {#utf-character-set}

Para proporcionar una mejor compatibilidad multilingüe, es necesario utilizar el conjunto de caracteres UTF8.

Cambie MySQL para que tenga UTF8 como conjunto de caracteres:
* mysql > ESTABLECER NOMBRES &#39;utf8&#39;;

Cambie la base de datos MySQL a UTF8 de forma predeterminada:
* Editar archivo `/etc/my.cnf`
* En el `[client]` , añada: `default-character-set=utf8`
* En el `[mysqld]` , añada: `character-set-server=utf8`

## Instalación de MySQL Workbench {#installing-mysql-workbench}

MySQL Workbench proporciona una interfaz de usuario para ejecutar secuencias de comandos SQL que instalan el esquema y los datos iniciales.

MySQL Workbench debe descargarse e instalarse siguiendo las instrucciones para el sistema operativo de destino.

## Conexión de habilitación {#enablement-connection}

Cuando MySQL Workbench se inicia por primera vez, a menos que ya se esté utilizando para otros fines, todavía no mostrará ninguna conexión:

![mysqlconnection](assets/mysqlconnection.png)

### Nueva configuración de conexión {#new-connection-settings}

1. Seleccione el icono &quot;+&quot; a la derecha de `MySQL Connections`.
1. En el cuadro de diálogo `Setup New Connection`, introduzca valores apropiados para su plataforma con fines de demostración, con la instancia de autor AEM y MySQL en el mismo servidor:
   * Nombre de la conexión: `Enablement`
   * Método de conexión: `Standard (TCP/IP)`
   * Nombre del host: `127.0.0.1`
   * Nombre de usuario: `root`
   * Contraseña: `no password by default`
   * Esquema predeterminado: `leave blank`
1. Select `Test Connection` para verificar la conexión con el servicio MySQL en ejecución.

**Notas**:
* El puerto predeterminado es `3306`.
* La variable `Connection Name` se introduce como `datasource` name en [Configuración de JDBC OSGi](#configure-jdbc-connections).

#### Conexión correcta {#successful-connection}

![mysqlconnection1](assets/mysqlconnection1.png)

#### Nueva conexión de habilitación {#new-enablement-connection}

![mysqlconnection2](assets/mysqlconnection2.png)

## Configuración de base de datos {#database-setup}

Al abrir la nueva conexión de habilitación, observe que hay un esquema de prueba y cuentas de usuario predeterminadas.

![configuración de base de datos](assets/database-setup.png)

### Obtener scripts SQL {#obtain-sql-scripts}

Las secuencias de comandos SQL se obtienen mediante CRXDE Lite en la instancia de autor. La variable [Paquete SCORM](deploy-communities.md#scorm) debe estar instalado:

1. Vaya al CRXDE Lite:
   * Por ejemplo, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)
1. Expanda el `/libs/social/config/scorm/` carpeta
1. Descargar `database_scormengine.sql`
1. Descargar `database_scorm_integration.sql`

![sqlscripts](assets/sqlscripts.png)

Un método para descargar el esquema es:

* Seleccione el `jcr:content` para el archivo sql.
* Observe el valor de la variable `jcr:data` es un vínculo de vista.
* Seleccione el vínculo de vista para guardar los datos en un archivo local.

### Crear base de datos SCORM {#create-scorm-database}

La base de datos SCORM de habilitación que se creará es:

* name: `ScormEngineDB`
* creada a partir de secuencias de comandos:
   * esquema: `database_scormengine.sql`
   * datos: `database_scorm_integration.sql`
Siga los pasos a continuación (
[open](#step-open-sql-file), [execute](#step-execute-sql-script)) para instalar cada [Script SQL](#obtain-sql-scripts) . [Actualizar](#refresh) cuando sea necesario para ver los resultados de la ejecución de la secuencia de comandos.

Asegúrese de instalar el esquema antes de instalar los datos.

>[!CAUTION]
>
>Si se cambia el nombre de la base de datos, asegúrese de especificarlo correctamente en:
>
>* [Configuración JDBC](#configure-jdbc-connections)
>* [Configuración de SCORM](#configure-scorm)


#### Paso 1: abrir archivo SQL {#step-open-sql-file}

En MySQL Workbench

* Desde el menú desplegable Archivo
* Seleccione `Open SQL Script ...`
* En este orden, seleccione una de las siguientes opciones:
   1. `database_scormengine.sql`
   1. `database_scorm_integration.sql`

![scrom-database](assets/scrom-database.png)

#### Paso 2: ejecutar script SQL {#step-execute-sql-script}

En la ventana Workbench del archivo abierto en el paso 1, seleccione la opción `lightening (flash) icon` para ejecutar la secuencia de comandos.

Tenga en cuenta que la ejecución de la variable `database_scormengine.sql` la secuencia de comandos para crear la base de datos SCORM puede tardar un minuto en completarse.

![scrom-database1](assets/scrom-database1.png)

#### Actualizar {#refresh}

Una vez ejecutadas las secuencias de comandos, es necesario actualizar la variable `SCHEMAS` de la sección `Navigator` para ver la nueva base de datos. Utilice el icono de actualización a la derecha de &quot;SCHEMAS&quot;:

![scrom-database2](assets/scrom-database2.png)

#### Resultado: scormenginedb {#result-scormenginedb}

Después de instalar y actualizar SCHEMAS, la variable `scormenginedb` estarán visibles.

![scrom-database3](assets/scrom-database3.png)

## Configuración de conexiones JDBC {#configure-jdbc-connections}

La configuración OSGi para **Agrupamiento de conexiones JDBC Day Commons** configura el controlador JDBC de MySQL.

Todas las instancias de AEM de publicación y creación deben apuntar al mismo servidor MySQL.

Cuando MySQL se ejecuta en un servidor diferente de AEM, el nombre de host del servidor debe especificarse en lugar de &quot;localhost&quot; en el conector JDBC (que rellena la variable [ScormEngine](#configurescormengineservice) configuración).

* En cada instancia de autor y publicación AEM
* Inicio de sesión con privilegios de administrador
* Acceda a la [consola web](../../help/sites-deploying/configuring-osgi.md)
   * Por ejemplo, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* Busque la variable `Day Commons JDBC Connections Pool`
* Seleccione el `+` para crear una nueva configuración

   ![jdbcconnection1](assets/jdbcconnection1.png)

* Introduzca los siguientes valores:
   * **[!UICONTROL Clase de controlador JDBC]**: `com.mysql.jdbc.Driver`
   * **URIJ de conexión DBC**: `jdbc:mysql://localhost:3306/aem63reporting` especifique server en lugar de localhost si el servidor MySQL no es lo mismo que &#39;this&#39; AEM server.
   * **[!UICONTROL Nombre de usuario]**: Raíz o introduzca el nombre de usuario configurado para el servidor MySQL, si no es &quot;raíz&quot;.
   * **[!UICONTROL Contraseña]**: Borre este campo si no hay ninguna contraseña establecida para MySQL, sino introduzca la contraseña configurada para el nombre de usuario de MySQL.
   * **[!UICONTROL Nombre de la fuente de datos]**: Nombre introducido para la variable [Conexión MySQL](#new-connection-settings), por ejemplo, &quot;habilitación&quot;.
* Seleccione **[!UICONTROL Guardar]**.

## Configurar Puntuación {#configure-scorm}

### Servicio AEM Communities ScormEngine {#aem-communities-scormengine-service}

La configuración OSGi para **Servicio AEM Communities ScormEngine** configura SCORM para el uso del servidor MySQL por parte de una comunidad de habilitación.

Esta configuración está presente cuando la variable [Paquete SCORM](deploy-communities.md#scorm-package) está instalado.

Todas las instancias de publicación y autor apuntan al mismo servidor MySQL.

Cuando MySQL se ejecuta en un servidor diferente de AEM, el nombre de host del servidor debe especificarse en lugar de &quot;localhost&quot; en el servicio ScormEngine, que generalmente se rellena desde la variable [Conexión JDBC](#configure-jdbc-connections) configuración.

* En cada instancia de autor y publicación AEM
* Inicio de sesión con privilegios de administrador
* Acceda a la [consola web](../../help/sites-deploying/configuring-osgi.md)
   * Por ejemplo, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* Busque la variable `AEM Communities ScormEngine Service`
* Seleccione el icono de edición

   ![scrom-engine](assets/scrom-engine.png)

* Compruebe que los siguientes valores de parámetro son coherentes con la variable [Conexión JDBC](#configurejdbcconnectionspool) config:
   * **[!UICONTROL URI de conexión JDBC]**: `jdbc:mysql://localhost:3306/ScormEngineDB` *ScormEngineDB* es el nombre de base de datos predeterminado en las secuencias de comandos SQL
   * **[!UICONTROL Nombre de usuario]**: Raíz o introduzca el nombre de usuario configurado para el servidor MySQL, si no es &quot;raíz&quot;
   * **[!UICONTROL Contraseña]**: Borre este campo si no hay ninguna contraseña establecida para MySQL, sino introduzca la contraseña configurada para el nombre de usuario de MySQL
* Respecto al siguiente parámetro:
   * **[!UICONTROL Contraseña de usuario de Scorm]**: NO EDITAR

      Solo para uso interno: Es para un usuario de servicio especial utilizado por AEM Communities para comunicarse con el motor de escorm.
* Seleccione **[!UICONTROL Guardar]**

### Filtro Adobe Granite CSRF {#adobe-granite-csrf-filter}

Para garantizar que los cursos de habilitación funcionen correctamente en todos los navegadores, es necesario agregar Mozilla como agente de usuario que no esté seleccionado por el filtro CSRF.

* Inicie sesión en la instancia de publicación de AEM con privilegios de administrador.
* Acceda a la [consola web](../../help/sites-deploying/configuring-osgi.md)
   * Por ejemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)
* Localizar `Adobe Granite CSRF Filter`.
* Seleccione el icono de edición.

   ![jdbcconnection2](assets/jdbcconnection2.png)

* Seleccione el `[+]` para agregar un agente de usuario seguro.
* Entrar `Mozilla/*`.
* Seleccione **[!UICONTROL Guardar]**.
