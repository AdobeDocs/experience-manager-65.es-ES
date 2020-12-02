---
title: Conexión a bases de datos SQL
seo-title: Conexión a bases de datos SQL
description: Acceda a una base de datos SQL externa para que las aplicaciones AEM puedan interactuar con los datos
seo-description: Acceda a una base de datos SQL externa para que las aplicaciones AEM puedan interactuar con los datos
uuid: 0af0ed08-9487-4c37-87ce-049c9b4c1ea2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 11a11803-bce4-4099-9b50-92327608f37b
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---


# Conexión a bases de datos SQL{#connecting-to-sql-databases}

Acceda a una base de datos SQL externa para que las aplicaciones de CQ puedan interactuar con los datos:

1. [Cree o obtenga un paquete OSGi que exporte el paquete](#bundling-the-jdbc-database-driver) de controladores JDBC.
1. [Configure un proveedor](#configuring-the-jdbc-connection-pool-service) de grupos de fuentes de datos JDBC.
1. [Obtenga un objeto de origen de datos y cree la conexión en el código](#connecting-to-the-database).

## Compilación del controlador de base de datos JDBC {#bundling-the-jdbc-database-driver}

Algunos proveedores de bases de datos proporcionan controladores JDBC en un paquete OSGi, por ejemplo [MySQL](https://www.mysql.com/downloads/connector/j/). Si el controlador JDBC de la base de datos no está disponible como paquete OSGi, obtenga el JAR del controlador y envuélvalo en un paquete OSGi. El paquete debe exportar los paquetes necesarios para interactuar con el servidor de la base de datos. El paquete también debe importar los paquetes a los que hace referencia.

El ejemplo siguiente utiliza el complemento [Bundle para Maven](https://felix.apache.org/site/apache-felix-maven-bundle-plugin-bnd.html) para envolver el controlador HSQLDB en un paquete OSGi. El POM ordena al complemento que incruste el archivo hsqldb.jar que se identifica como una dependencia. Se exportan todos los paquetes org.hsqldb.

El complemento determina automáticamente qué paquetes se importarán y los lista en el archivo MANIFEST.MF del paquete. Si alguno de los paquetes no está disponible en el servidor de CQ, el paquete no se inicio tras la instalación. Dos soluciones posibles son las siguientes:

* Indique en el POM que los paquetes son opcionales. Utilice esta solución cuando la conexión JDBC no requiera realmente los miembros del paquete. Utilice el elemento Import-Package para indicar paquetes opcionales como en el ejemplo siguiente:

   `<Import-Package>org.jboss.*;resolution:=optional,*</Import-Package>`
* Ajuste los archivos JAR que contienen los paquetes en un paquete OSGi que exporta los paquetes e implemente el paquete. Utilice esta solución cuando se requieran los miembros del paquete durante la ejecución del código.

El conocimiento del código fuente le permite decidir qué solución utilizar. También puede probar cualquiera de las soluciones y realizar pruebas para validar la solución.

### POM que agrupa hsqldb.jar {#pom-that-bundles-hsqldb-jar}

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>hsqldb-jdbc-driver-bundle</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  <name>wrapper-bundle-hsqldb-driver</name>
  <url>www.adobe.com</url>
  <description>Exports the HSQL JDBC driver</description>
  <packaging>bundle</packaging>
  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.felix</groupId>
        <artifactId>maven-bundle-plugin</artifactId>
        <version>1.4.3</version>
        <extensions>true</extensions>
        <configuration>
         <instructions>
            <Embed-Dependency>*</Embed-Dependency>
            <_exportcontents>org.hsqldb.*</_exportcontents>
          </instructions>
        </configuration>
      </plugin>
    </plugins>
  </build>
  <dependencies>
    <dependency>
      <groupId>hsqldb</groupId>
      <artifactId>hsqldb</artifactId>
      <version>2.2.9</version>
    </dependency>
  </dependencies>
</project>
```

Los siguientes vínculos abren las páginas de descarga de algunos productos de base de datos populares:

* [Microsoft SQL Server](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&amp;id=11774)
* [Oracle](https://www.oracle.com/technetwork/database/features/jdbc/index-091264.html)
* [IBM DB2](https://www-01.ibm.com/support/docview.wss?uid=swg27007053)

### Configuración del servicio JDBC Connection Pool {#configuring-the-jdbc-connection-pool-service}

Añada una configuración para el servicio Pool de Conexiones JDBC que utilice el controlador JDBC para crear objetos de origen de datos. El código de la aplicación utiliza este servicio para obtener el objeto y conectarse a la base de datos.

El grupo de conexiones JDBC ( `com.day.commons.datasource.jdbcpool.JdbcPoolService`) es un servicio de fábrica. Si necesita conexiones que utilicen propiedades diferentes, por ejemplo, acceso de solo lectura o de lectura y escritura, cree varias configuraciones.

Al trabajar con CQ existen varios métodos para administrar la configuración de dichos servicios; consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información.

Las siguientes propiedades están disponibles para configurar un servicio de conexión agrupada. Los nombres de las propiedades se muestran tal como aparecen en la consola web. El nombre correspondiente para un nodo `sling:OsgiConfig` aparece entre paréntesis. Se muestran valores de ejemplo para un servidor HSQLDB y una base de datos con un alias de `mydb`:

* Clase de controlador JDBC ( `jdbc.driver.class`): La clase Java que se va a utilizar que implementa la interfaz java.sql.Driver, por ejemplo `org.hsqldb.jdbc.JDBCDriver`. El tipo de datos es `String`.

* URI de conexión JDBC ( `jdbc.connection.uri`): Dirección URL de la base de datos que se va a utilizar para crear la conexión, por ejemplo `jdbc:hsqldb:hsql//10.36.79.223:9001/mydb`. El formato de la dirección URL debe ser válido para utilizarse con el método getConnection de la clase java.sql.DriverManager. El tipo de datos es `String`.

* Nombre de usuario ( `jdbc.username`): Nombre de usuario que se va a utilizar para autenticarse con el servidor de la base de datos. El tipo de datos es `String`.

* Contraseña ( `jdbc.password`): La contraseña que se usará para la autenticación del usuario. El tipo de datos es `String`.

* Consulta de validación ( `jdbc.validation.query`): La instrucción SQL que se va a utilizar para comprobar que la conexión se ha realizado correctamente, por ejemplo `select 1 from INFORMATION_SCHEMA.SYSTEM_USERS`. El tipo de datos es `String`.

* Solo lectura de forma predeterminada (default.readonly): Seleccione esta opción cuando desee que la conexión proporcione acceso de solo lectura. El tipo de datos es `Boolean`.
* Autoconfirmar de forma predeterminada ( `default.autocommit`): Seleccione esta opción para crear transacciones independientes para cada comando SQL que se envíe a la base de datos y cada transacción se confirme automáticamente. No seleccione esta opción cuando confirme transacciones explícitamente en el código. El tipo de datos es `Boolean`.

* Tamaño del grupo ( `pool.size`): Número de conexiones simultáneas que se pondrán a disposición de la base de datos. El tipo de datos es `Long`.

* Espera de grupo ( `pool.max.wait.msec`): Cantidad de tiempo antes de que se agote el tiempo de espera de una solicitud de conexión. El tipo de datos es `Long`.

* Nombre del origen de datos ( `datasource.name`): Nombre de esta fuente de datos. El tipo de datos es `String`.

* Propiedades de servicio adicionales ( `datasource.svc.properties`): Conjunto de pares nombre/valor que desea anexar a la dirección URL de conexión. El tipo de datos es `String[]`.

El servicio JDBC Connections Pool es una fábrica. Por lo tanto, si utiliza un nodo `sling:OsgiConfig` para configurar el servicio de conexión, el nombre del nodo debe incluir el PID de servicio de fábrica seguido de *`-alias`*. El alias que utilice debe ser único para todos los nodos de configuración de ese PID. Un nombre de nodo de ejemplo es `com.day.commons.datasource.jdbcpool.JdbcPoolService-myhsqldbpool`.

![climage_1-7](assets/chlimage_1-7a.png)

### Conexión a la base de datos {#connecting-to-the-database}

En el código Java, utilice el servicio DataSourcePool para obtener un objeto `javax.sql.DataSource` para la configuración que ha creado. El servicio DataSourcePool proporciona el método `getDataSource` que devuelve un objeto `DataSource` para un nombre de fuente de datos determinado. Como argumento del método, utilice el valor de la propiedad Nombre del origen de datos (o `datasource.name`) que especificó para la configuración del grupo de conexiones JDBC.

El siguiente ejemplo de código JSP obtiene una instancia del origen de datos hsqldbds, ejecuta una consulta SQL simple y muestra el número de resultados que se devuelven.

#### JSP que realiza una búsqueda de base de datos {#jsp-that-performs-a-database-lookup}

```java
<%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false"%><%
%><%@ page import="com.day.commons.datasource.poolservice.DataSourcePool" %><%
%><%@ page import="javax.sql.DataSource" %><%
%><%@ page import="java.sql.Connection" %><%
%><%@ page import="java.sql.SQLException" %><%
%><%@ page import="java.sql.Statement" %><%
%><%@ page import="java.sql.ResultSet"%><%
%><html>
<cq:include script="head.jsp"/>
<body>
<%DataSourcePool dspService = sling.getService(DataSourcePool.class);
  try {
     DataSource ds = (DataSource) dspService.getDataSource("hsqldbds");
     if(ds != null) {
         %><p>Obtained the datasource!</p><%
         %><%final Connection connection = ds.getConnection();
          final Statement statement = connection.createStatement();
          final ResultSet resultSet = statement.executeQuery("SELECT * from INFORMATION_SCHEMA.SYSTEM_USERS");
          int r=0;
          while(resultSet.next()){
             r=r+1;
          }
          resultSet.close();
          %><p>Number of results: <%=r%></p><%
      }
   }catch (Exception e) {
        %><p>error! <%=e.getMessage()%></p><%
    }
%></body>
</html>
```

>[!NOTE]
>
>Si el método getDataSource emite una excepción porque no se encuentra el origen de datos, asegúrese de que la configuración del servicio Pool de conexiones sea correcta. Compruebe los nombres, valores y tipos de datos de las propiedades.


>[!NOTE]
>
>Para obtener información sobre cómo inyectar un DataSourcePool en un paquete OSGi, consulte [Inyección de un servicio DataSourcePool en un paquete OSGi de Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/datasourcepool.html).

