---
title: AEM Compatibilidad con RDBMS en 6.4
description: AEM Obtenga información acerca de la compatibilidad con la persistencia de bases de datos relacionales en la versión 6.4 de y las opciones de configuración disponibles.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
feature: Administering
exl-id: 1e34c5ca-9e08-4b2a-901c-ab28aeb4a807
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---

# AEM Compatibilidad con RDBMS en 6.4{#rdbms-support-in-aem}

## Información general {#overview}

AEM La compatibilidad con la persistencia de bases de datos relacionales en la base de datos se implementa mediante el Microkernel de documentos. El Microkernel del documento es la base que también se utiliza para implementar la persistencia de MongoDB.

Consiste en una API de Java basada en la API de Java de Mongo. También se proporciona una implementación de una API de BlobStore. De forma predeterminada, los blobs se almacenan en la base de datos.

Para obtener más información sobre los detalles de la implementación, consulte la [RDBDocumentStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBDocumentStore.html) y la [documentación de RDBBlobStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBBlobStore.html).

>[!NOTE]
>
>También se proporciona compatibilidad con **PostgreSQL 9.4**, pero solo con fines de demostración. No estará disponible para entornos de producción.

## Bases de datos compatibles {#supported-databases}

AEM Para obtener más información sobre el nivel de compatibilidad con bases de datos relacionales en la base de datos de la base de datos de la base de datos, vea la [página de requisitos técnicos](/help/sites-deploying/technical-requirements.md).

## Pasos de configuración {#configuration-steps}

El repositorio se crea configurando el servicio OSGi `DocumentNodeStoreService`. Se ha ampliado para admitir la persistencia de bases de datos relacionales, además de MongoDB.

AEM Para que funcione, es necesario configurar una fuente de datos con la opción de configuración de la fuente de datos de la aplicación de forma. Esto se realiza a través del archivo `org.apache.sling.datasource.DataSourceFactory.config`. Los controladores JDBC para la base de datos correspondiente deben proporcionarse por separado como paquetes OSGi dentro de la configuración local.

Para ver los pasos de creación de paquetes OSGi para controladores JDBC, consulte esta [documentación](https://sling.apache.org/documentation/bundles/datasource-providers.html#convert-driver-jars-to-bundle) en el sitio web de Apache Sling.

AEM Una vez que los paquetes estén en su lugar, siga los siguientes pasos para configurar la con persistencia de RDB:

1. AEM Asegúrese de que se ha iniciado el daemon de base de datos y de que dispone de una base de datos activa para su uso con el servicio de base de datos de.
1. AEM Copie el JAR de la versión 6.3 de la en el directorio de instalación.
1. Cree una carpeta llamada `crx-quickstart\install` en el directorio de instalación.
1. Configure el almacén de nodos del documento creando un archivo de configuración con el siguiente nombre en el directorio `crx-quickstart\install`:

   * `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

1. Configure la fuente de datos y los parámetros JDBC creando otro archivo de configuración con el siguiente nombre en la carpeta `crx-quickstart\install`:

   * `org.apache.sling.datasource.DataSourceFactory-oak.config`

   >[!NOTE]
   >
   >Para obtener información detallada sobre la configuración del origen de datos para cada base de datos compatible, consulte [Opciones de configuración de Data Source](/help/sites-deploying/rdbms-support-in-aem.md#data-source-configuration-options).

1. AEM A continuación, prepare los paquetes OSGi de JDBC que se van a utilizar con la:

   1. En la carpeta `crx-quickstart/install`, cree una carpeta denominada `9`.

   1. Coloque el JDBC jar en la nueva carpeta.

1. AEM Finalmente, comience a con los modos de ejecución `crx3` y `crx3rdb`:

   ```java
   java -jar quickstart.jar -r crx3,crx3rdb
   ```

## Opciones de configuración de Data Source {#data-source-configuration-options}

AEM La configuración de OSGi `org.apache.sling.datasource.DataSourceFactory-oak.config` se usa para configurar los parámetros necesarios para la comunicación entre las capas de persistencia de la base de datos y la capa de comunicación entre las bases de datos y la base de datos.

Estas son las opciones de configuración disponibles:

* `datasource.name:` El nombre del origen de datos. El valor predeterminado es `oak`.

* `url:` La cadena URL de la base de datos que debe usarse con JDBC. Cada tipo de base de datos tiene su propio formato de cadena de URL. Para obtener más información, consulte [Formatos de cadena de URL](/help/sites-deploying/rdbms-support-in-aem.md#url-string-formats) a continuación.

* `driverClassName:` nombre de clase del controlador JDBC. Esto variará según la base de datos que desee utilizar y, posteriormente, el controlador necesario para conectarse a ella. AEM A continuación, se muestran los nombres de clase de todas las bases de datos compatibles con el servicio de bases de datos de:

   * `org.postgresql.Driver` para PostgreSQL;
   * `com.ibm.db2.jcc.DB2Driver` para DB2;
   * `oracle.jdbc.OracleDriver` para Oracle;
   * `com.mysql.jdbc.Driver` para MySQL y MariaDB (experimental);
   * c `om.microsoft.sqlserver.jdbc.SQLServerDriver` para Microsoft SQL Server (experimental).

* `username:` El nombre de usuario con el que se ejecuta la base de datos.

* `password:` Contraseña de la base de datos.

### Formatos de cadena de URL {#url-string-formats}

En la configuración de la fuente de datos se utiliza un formato de cadena de URL diferente en función del tipo de base de datos que se deba utilizar. AEM A continuación se muestra una lista de formatos para las bases de datos que admite actualmente el sistema de bases de datos de que se dispone en la actualidad:

* `jdbc:postgresql:databasename` para PostgreSQL;
* `jdbc:db2://localhost:port/databasename` para DB2;
* `jdbc:oracle:thin:localhost:port:SID` para Oracle;
* `jdbc:mysql://localhost:3306/databasename` para MySQL y MariaDB (experimental);
* `jdbc:sqlserver://localhost:1453;databaseName=name` para Microsoft SQL Server (experimental).

## Limitaciones conocidas {#known-limitations}

AEM Aunque la persistencia de RDBMS admite el uso simultáneo de varias instancias de con una sola base de datos, las instalaciones simultáneas no lo son.

Para solucionar esto, asegúrese de ejecutar primero la instalación con un solo miembro y agregue los demás después de que el primero haya finalizado la instalación.
