---
title: Funciones de configuración de MySQL para habilitación
seo-title: Funciones de configuración de MySQL para habilitación
description: Conexión del servidor MySQL
seo-description: Conexión del servidor MySQL
uuid: e02d9404-de75-4fdb-896c-ea3f64f980a3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 9222bc93-c231-4ac8-aa28-30d784a4ca3b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Funciones de configuración de MySQL para habilitación {#mysql-configuration-for-enablement-features}

MySQL es una base de datos relacional que se utiliza principalmente para el seguimiento SCORM y los datos de informes para los recursos de habilitación. Se incluyen tablas para otras funciones, como el seguimiento de pausa/reanudación de vídeo.

Estas instrucciones describen cómo conectarse al servidor MySQL, establecer la base de datos de habilitación y rellenar la base de datos con datos iniciales.

## Requisitos {#requirements}

Antes de configurar la función de habilitación de MySQL para Comunidades, asegúrese de

* Instalación de [MySQL Server](https://dev.mysql.com/downloads/mysql/) Community Server versión 5.6
   * La versión 5.7 no es compatible con SCORM
   * Puede ser el mismo servidor que la instancia de AEM de creación
* En todas las instancias de AEM, instale el controlador [JDBC oficial para MySQL](deploy-communities.md#jdbc-driver-for-mysql)
* Instalación de [MySQL Workbench](https://dev.mysql.com/downloads/tools/workbench/)
* En todas las instancias de AEM, instale el paquete [SCORM](enablement.md#scorm)

## Instalación de MySQL {#installing-mysql}

MySQL debe descargarse e instalarse siguiendo las instrucciones del sistema operativo de destino.

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

## Habilitación de la conexión {#enablement-connection}

Cuando MySQL Workbench se inicia por primera vez, a menos que ya se esté utilizando para otros fines, aún no mostrará ninguna conexión:

![chlimage_1-327](assets/chlimage_1-327.png)

### Nueva configuración de conexión {#new-connection-settings}

1. Seleccione el icono &#39;+&#39; a la derecha de `MySQL Connections`.
1. En el cuadro de diálogo `Setup New Connection`, introduzca los valores adecuados para su plataforma con fines de demostración, con la instancia de AEM de autor y MySQL en el mismo servidor:
   * Nombre de la conexión: `Enablement`
   * Método de conexión: `Standard (TCP/IP)`
   * Hostname: `127.0.0.1`
   * Nombre de usuario: `root`
   * Contraseña: `no password by default`
   * Esquema predeterminado: `leave blank`
1. Seleccione `Test Connection` para verificar la conexión con el servicio MySQL en ejecución

**Notas**:

* El puerto predeterminado es `3306`
* El `Connection Name` nombre elegido se introduce como `datasource` nombre en la configuración OSGi de [JDBC](#configure-jdbc-connections)

#### Conexión correcta {#successful-connection}

![chlimage_1-328](assets/chlimage_1-328.png)

#### Nueva conexión de habilitación {#new-enablement-connection}

![chlimage_1-329](assets/chlimage_1-329.png)

## Configuración de base de datos {#database-setup}

Al abrir la nueva conexión de habilitación, observe que hay un esquema de prueba y cuentas de usuario predeterminadas.

![chlimage_1-330](assets/chlimage_1-330.png)

### Obtención de secuencias de comandos SQL {#obtain-sql-scripts}

Las secuencias de comandos SQL se obtienen utilizando CRXDE Lite en la instancia de creación. El paquete [](deploy-communities.md#scorm) SCORM debe estar instalado:

1. Navegar a CRXDE Lite
   * Por ejemplo, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)
1. Expandir la `/libs/social/config/scorm/` carpeta
1. Descargar `database_scormengine.sql`
1. Descargar `database_scorm_integration.sql`

![chlimage_1-331](assets/chlimage_1-331.png)

Un método para descargar el esquema es

* Seleccione el `jcr:content`nodo para el archivo sql
* Observe que el valor de la `jcr:data`propiedad es un vínculo de vista
* Seleccione el vínculo de vista para guardar los datos en un archivo local

### Crear base de datos SCORM {#create-scorm-database}

La base de datos SCORM de habilitación que se va a crear es:

* name: `ScormEngineDB`
* creados a partir de secuencias de comandos:
   * esquema: `database_scormengine.sql`
   * data: `database_scorm_integration.sql`Siga los pasos a continuación ([abra](#step-open-sql-file), [ejecute](#step-execute-sql-script)) para instalar cada secuencia de comandos [SQL](#obtain-sql-scripts) . [Actualice](#refresh) cuando sea necesario para ver los resultados de la ejecución de la secuencia de comandos.

Asegúrese de instalar el esquema antes de instalar los datos.

>[!CAUTION]
>
>Si se cambia el nombre de la base de datos, asegúrese de especificarlo correctamente en
>
>* [Configuración JDBC](#configure-jdbc-connections)
>* [Configuración de SCORM](#configure-scorm)
>



#### Paso 1: abrir archivo SQL {#step-open-sql-file}

En el área de trabajo de MySQL

* Desde el menú desplegable Archivo
* Seleccione `Open SQL Script ...`
* En este orden, seleccione una de las siguientes opciones:
   1. `database_scormengine.sql`
   1. `database_scorm_integration.sql`

![chlimage_1-332](assets/chlimage_1-332.png)

#### Paso 2: ejecutar script SQL {#step-execute-sql-script}

En la ventana Workbench del archivo abierto en el paso 1, seleccione el `lightening (flash) icon` para ejecutar la secuencia de comandos.

Tenga en cuenta que la ejecución de la `database_scormengine.sql` secuencia de comandos para crear la base de datos SCORM puede tardar un minuto en completarse.

![chlimage_1-333](assets/chlimage_1-333.png)

#### Actualizar {#refresh}

Una vez ejecutadas las secuencias de comandos, es necesario actualizar la `SCHEMAS`sección de la `Navigator` para ver la nueva base de datos. Utilice el icono de actualización a la derecha de &#39;SCHEMAS&#39;:

![chlimage_1-334](assets/chlimage_1-334.png)

#### Resultado: scormenginedb {#result-scormenginedb}

Después de instalar y actualizar SCHEMAS, el **`scormenginedb`*** estará visible.

![chlimage_1-335](assets/chlimage_1-335.png)

## Configurar conexiones JDBC {#configure-jdbc-connections}

La configuración OSGi para el grupo **de conexiones JDBC** Day Commons configura el controlador JDBC MySQL.

Todas las instancias de AEM de publicación y creación deben apuntar al mismo servidor MySQL.

Cuando MySQL se ejecuta en un servidor diferente de AEM, el nombre de host del servidor debe especificarse en lugar de &#39;localhost&#39; en el conector JDBC (que rellena la configuración de [ScormEngine](#configurescormengineservice) ).

* En cada instancia de AEM de creación y publicación
* Inicio de sesión con privilegios de administrador
* Acceso a la consola [web](../../help/sites-deploying/configuring-osgi.md)
   * Por ejemplo, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* Localice la variable `Day Commons JDBC Connections Pool`
* Seleccione el icono `+` para crear una nueva configuración

![chlimage_1-336](assets/chlimage_1-336.png)

* Introduzca los valores siguientes:
   * **[!UICONTROL Clase]** de controlador JDBC: `com.mysql.jdbc.Driver`
   * **URL **de conexión DBC:`jdbc:mysql://localhost:3306/aem63reporting`especifique el servidor en lugar de localhost si MySQL Server no es igual que &#39;this&#39; AEM Server
   * **[!UICONTROL Nombre de usuario]**: Raíz o escriba el nombre de usuario configurado para el servidor MySQL, si no &#39;raíz&#39;
   * **[!UICONTROL Contraseña]**: Borre este campo si no hay ninguna contraseña establecida para MySQL, de lo contrario introduzca la contraseña configurada para el nombre de usuario de MySQL
   * **[!UICONTROL Nombre]** del origen de datos: Nombre introducido para la conexión [](#new-connection-settings)MySQL, por ejemplo, &#39;habilitación&#39;
* Seleccione **[!UICONTROL Guardar]**

## Configurar Scorm {#configure-scorm}

### Servicio ScormEngine de comunidades AEM {#aem-communities-scormengine-service}

La configuración OSGi para el servicio **ScormEngine de comunidades de** AEM configura SCORM para el uso del servidor MySQL por parte de una comunidad de habilitación.

Esta configuración está presente cuando se instala el paquete [](deploy-communities.md#scorm-package) SCORM.

Todas las instancias de publicación y creación apuntan al mismo servidor MySQL.

Cuando MySQL se ejecuta en un servidor diferente de AEM, el nombre de host del servidor debe especificarse en lugar de &#39;localhost&#39; en el servicio ScormEngine, que generalmente se rellena desde la configuración de la conexión [](#configure-jdbc-connections) JDBC.

* En cada instancia de AEM de creación y publicación
* Inicio de sesión con privilegios de administrador
* Acceso a la consola [web](../../help/sites-deploying/configuring-osgi.md)
   * Por ejemplo, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* Localice la variable `AEM Communities ScormEngine Service`
* Seleccione el icono de edición
   ![chlimage_1-337](assets/chlimage_1-337.png)
* Compruebe que los siguientes valores de parámetro son coherentes con la configuración de la conexión [](#configurejdbcconnectionspool) JDBC:
   * **[!UICONTROL URI]** de conexión JDBC: `jdbc:mysql://localhost:3306/ScormEngineDB` ScormEngineDB ** es el nombre de base de datos predeterminado en las secuencias de comandos de SQL
   * **[!UICONTROL Nombre de usuario]**: Raíz o escriba el nombre de usuario configurado para el servidor MySQL, si no &#39;raíz&#39;
   * **[!UICONTROL Contraseña]**: Borre este campo si no hay ninguna contraseña establecida para MySQL, de lo contrario introduzca la contraseña configurada para el nombre de usuario de MySQL
* Respecto al parámetro siguiente:
   * **[!UICONTROL Contraseña]** de usuario de Scorm: NO EDITAR

      Solo para uso interno. Es para un usuario de servicios especiales que AEM Communities comunicarse con el motor de escorm.
* Seleccione **[!UICONTROL Guardar]**

### Filtro CSRF de Adobe Granite {#adobe-granite-csrf-filter}

Para garantizar que los cursos de habilitación funcionen correctamente en todos los exploradores, es necesario agregar Mozilla como agente de usuario que no esté marcado por el filtro CSRF.

* En cada instancia de AEM de publicación
* Inicio de sesión con privilegios de administrador
* Acceso a la consola [web](../../help/sites-deploying/configuring-osgi.md)
   * Por ejemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)
* Localizar `Adobe Granite CSRF Filter`
* Seleccione el icono de edición
   ![chlimage_1-337](assets/chlimage_1-338.png)
* Seleccione el `[+]` icono para agregar un agente de usuario seguro
* Enter `Mozilla/*`
* Seleccione **[!UICONTROL Guardar]**

