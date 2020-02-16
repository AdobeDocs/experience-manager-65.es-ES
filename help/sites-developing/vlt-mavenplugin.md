---
title: Administración de paquetes con Maven
seo-title: Administración de paquetes con Maven
description: Utilice el complemento Content Package Maven para integrar las tareas de administración de paquetes en sus proyectos de Maven
seo-description: Utilice el complemento Content Package Maven para integrar las tareas de administración de paquetes en sus proyectos de Maven
uuid: fa73f0d6-8848-4911-9b96-311c875b45be
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 943de371-0149-4307-be3a-b11c590b3451
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# Administración de paquetes con Maven{#managing-packages-using-maven}

Utilice el complemento Content Package Maven para integrar las tareas de administración de paquetes en sus proyectos de Maven. Los objetivos y parámetros del complemento le permiten automatizar muchas de las tareas que normalmente realizaría mediante la página Administrador de paquetes o la línea de comandos de FileVault:

* Cree nuevos paquetes a partir de archivos del sistema de archivos.
* Instale y desinstale paquetes en el servidor CRX o CQ.
* Genere paquetes que ya estén definidos en el servidor.
* Obtenga una lista de los paquetes instalados en el servidor.
* Elimine un paquete del servidor.

## Adición del complemento Maven del paquete de contenido al archivo POM {#adding-the-content-package-maven-plugin-to-the-pom-file}

Para utilizar el complemento Maven del paquete de contenido, agregue el siguiente elemento de complemento dentro del elemento build del archivo POM:

```xml
<plugin>
 <groupId>com.day.jcr.vault</groupId>
 <artifactId>content-package-maven-plugin</artifactId>
 <version>0.0.24</version>
 <configuration>
       <!-- parameters and values common to all goals, as required -->
 </configuration>
</plugin>
```

Para habilitar Maven para descargar el complemento, utilice el perfil proporcionado en la sección [Obtención del complemento](#obtaining-the-content-package-maven-plugin) Content Package Maven de esta página.

## Objetivos del complemento Maven del paquete de contenido {#goals-of-the-content-package-maven-plugin}

Los objetivos y parámetros de objetivo que proporciona el complemento Paquete de contenido se describen en las secciones siguientes. Los parámetros que se describen en la sección Parámetros comunes pueden utilizarse para la mayoría de los objetivos. Los parámetros que se aplican a un objetivo se describen en la sección correspondiente.

**Prefijo de complemento**

El prefijo del complemento es content-package. Utilice este prefijo para ejecutar un objetivo desde la línea de comandos, como en el ejemplo siguiente:

```shell
mvn content-package:build
```

**Prefijo de parámetro**

A menos que se indique lo contrario, los objetivos y parámetros del complemento utilizan el prefijo vault, como en el siguiente ejemplo:

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

**Sustitutos**

Los objetivos que utilizan proxies para el servidor CRX o CQ utilizan la primera configuración de proxy válida que se encuentra en la configuración de Maven. Si no se encuentra ninguna configuración proxy, no se utiliza ningún proxy. Consulte el parámetro useProxy en la sección Configuración común.

### Parámetros comunes {#common-parameters}

Los parámetros de la siguiente tabla son comunes a todos los objetivos excepto cuando se los indica en la columna Objetivos.

<table>
 <tbody>
  <tr>
   <th>Nombre</th>
   <th>Tipo</th>
   <th>Requerido</th>
   <th>Valor predeterminado</th>
   <th>Descripción</th>
   <th>Objetivos</th>
  </tr>
  <tr>
   <td>failOnError</td>
   <td>boolean</td>
   <td>No</td>
   <td>false</td>
   <td>Un valor de <code>true</code> hace que la compilación falle cuando se produce un error. Un valor de hace que <code>false</code> la compilación ignore el error.</td>
   <td>Todos los objetivos excepto el paquete.</td>
  </tr>
  <tr>
   <td>name</td>
   <td>Cadena</td>
   <td>build: Sí<br /> instalación: No<br /> rm:Sí</td>
   <td>Generar: No hay valores predeterminados.<br /> install: Valor de la propiedad artifactsId del proyecto Maven.</td>
   <td>Nombre del paquete en el que se va a actuar.</td>
   <td>Todos los objetivos excepto ls.</td>
  </tr>
  <tr>
   <td>password</td>
   <td>Cadena</td>
   <td>Sí</td>
   <td>administrador</td>
   <td>La contraseña utilizada para la autenticación con el servidor CRX.</td>
   <td>Todos los objetivos excepto el paquete.</td>
  </tr>
  <tr>
   <td>serverId</td>
   <td>Cadena</td>
   <td>No</td>
   <td></td>
   <td>ID del servidor desde el que se recuperarán el nombre de usuario y la contraseña para la autenticación.</td>
   <td>Todos los objetivos excepto el paquete.</td>
  </tr>
  <tr>
   <td>targetURL</td>
   <td>Cadena</td>
   <td>Sí</td>
   <td>http://localhost:4502/<br /> crx/packmgr/<br /> service.jsp</td>
   <td>Dirección URL de la API de servicio HTTP del administrador de paquetes CRX.</td>
   <td>Todos los objetivos excepto el paquete.</td>
  </tr>
  <tr>
   <td>timeout</td>
   <td>int</td>
   <td>No</td>
   <td>5</td>
   <td>Tiempo de espera de conexión para comunicarse con el servicio del administrador de paquetes, en segundos.</td>
   <td>Todos los objetivos excepto el paquete.</td>
  </tr>
  <tr>
   <td>useProxy</td>
   <td>boolean</td>
   <td>No</td>
   <td>verdadero</td>
   <td>Determina si se usarán configuraciones proxy desde el archivo de configuración Maven. Un valor de <code>true</code> provoca el uso de la primera configuración proxy activa que se encuentra en las solicitudes de proxy al administrador de paquetes. Un valor false hace que no se utilice ningún proxy.</td>
   <td>Todos los objetivos excepto el paquete.</td>
  </tr>
  <tr>
   <td>userId</td>
   <td>Cadena</td>
   <td>Sí</td>
   <td>administrador</td>
   <td>El nombre de usuario que se va a autenticar con el servidor CRX.</td>
   <td>Todos los objetivos excepto el paquete.</td>
  </tr>
  <tr>
   <td>verbose</td>
   <td>boolean</td>
   <td>No</td>
   <td>false</td>
   <td>Activa o desactiva el registro detallado. Un valor de <code>true</code> habilita el registro detallado.</td>
   <td>Todos los objetivos excepto el paquete.</td>
  </tr>
 </tbody>
</table>

### build {#build}

Crea un paquete de contenido que ya está definido en una instancia de AEM.

>[!NOTE]
>
>Este objetivo no necesita ser ejecutado dentro de un proyecto Maven.

#### Parámetros {#parameters}

Todos los parámetros del objetivo de compilación se describen en la sección Parámetros [](#common-parameters) comunes.

#### Ejemplo {#example}

El ejemplo siguiente crea el paquete workflow-mbean que se instala en la instancia de AEM con la dirección IP 10.36.79.223. El objetivo se ejecuta con el siguiente comando:

```shell
mvn content-package:build
```

El siguiente archivo POM se encuentra en el directorio actual de la herramienta de línea de comandos. El POM especifica el nombre del paquete y la dirección URL del servicio de paquetes.

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>example-package</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
   <name>workflow-mbean</name>
   <failOnError>true</failOnError>
   <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
     </plugin>
 </plugins>
    </build>
</project>
```

### install {#install}

Instala un paquete en el repositorio. La ejecución de este objetivo no requiere un proyecto Maven. El objetivo está enlazado a la fase de instalación del ciclo vital de la compilación de Maven.

#### Parámetros {#parameters-1}

Además de los parámetros siguientes, consulte las descripciones de la sección Parámetros [](#common-parameters) comunes.

<table>
 <tbody>
  <tr>
   <th>Nombre</th>
   <th>Tipo</th>
   <th>Requerido</th>
   <th>Valor predeterminado</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>artefacto</td>
   <td>Cadena</td>
   <td>No</td>
   <td> Valor de la propiedad artifactsId del proyecto Maven.</td>
   <td>Una cadena del formulario groupId:artiactId:version[:packing].</td>
  </tr>
  <tr>
   <td>artiactId</td>
   <td>Cadena</td>
   <td>No</td>
   <td></td>
   <td>ID del artefacto que se va a instalar</td>
  </tr>
  <tr>
   <td>groupId</td>
   <td>Cadena</td>
   <td>No</td>
   <td></td>
   <td>GroupId del artefacto que se va a instalar</td>
  </tr>
  <tr>
   <td>instalar</td>
   <td>boolean</td>
   <td>No</td>
   <td>verdadero</td>
   <td>Determina si se desempaqueta el paquete automáticamente al cargarse. Un valor de true descomprime el paquete y false no lo descomprime.</td>
  </tr>
  <tr>
   <td>localRepository</td>
   <td>org.apache.maven.<br /> artefacto. repositorio.<br /> ArtiactRepository</td>
   <td>No</td>
   <td>Valor de la variable de sistema localRepository.</td>
   <td>Repositorio local de Maven. No puede configurar este parámetro con la configuración del complemento. La propiedad system siempre se utiliza.</td>
  </tr>
  <tr>
   <td>packageFile</td>
   <td>java.io.File</td>
   <td>No</td>
   <td>El artefacto principal definido para el proyecto Maven.</td>
   <td>Nombre del archivo de paquete que se va a instalar.</td>
  </tr>
  <tr>
   <td>empaquetado</td>
   <td>Cadena</td>
   <td>No</td>
   <td>zip</td>
   <td>Tipo de embalaje del artefacto que se va a instalar</td>
  </tr>
  <tr>
   <td>pomRemoteRepositories</td>
   <td>java.util.List</td>
   <td>Sí</td>
   <td>Valor de la propiedad remoteActRepositories definida para el proyecto Maven.</td>
   <td>Este valor no se puede configurar con la configuración del complemento. El valor debe especificarse en el proyecto. </td>
  </tr>
  <tr>
   <td>proyecto</td>
   <td>org.apache.maven.<br /> project.MavenProject</td>
   <td>Sí</td>
   <td>Proyecto para el cual se configura el complemento.</td>
   <td>El proyecto Maven. El proyecto está implícito porque contiene la configuración del complemento.</td>
  </tr>
  <tr>
   <td>repositoryId <i>(POM)</i><br /> repoID <i>(línea de comandos)</i></td>
   <td>Cadena</td>
   <td>No</td>
   <td>temp</td>
   <td>ID del repositorio desde el que se recupera el artefacto. En un POM, utilice repositoryID. En una línea de comandos, utilice repoID.</td>
  </tr>
  <tr>
   <td>repositorioUrl <i>(POM)</i><br /> repoURL <i>(línea de comandos)</i></td>
   <td>Cadena</td>
   <td>No</td>
   <td></td>
   <td>Dirección URL del repositorio desde el que se recupera el artefacto. En un POM, utilice repositoryURL. En una línea de comandos, utilice repoURL.</td>
  </tr>
  <tr>
   <td>version</td>
   <td>Cadena</td>
   <td>No</td>
   <td></td>
   <td>Versión del artefacto que se va a instalar.</td>
  </tr>
 </tbody>
</table>

#### Ejemplo {#example-1}

En el siguiente ejemplo se crea un paquete que contiene el paquete OSGi de flujo de trabajo (consulte el ejemplo del objetivo de [compilación](#build) ) y luego se instala el paquete. Dado que el objetivo de instalación está enlazado a la fase de instalación del paquete, el siguiente comando ejecuta el objetivo de instalación:

```shell
mvn install
```

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
    https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>

  <build>
    <plugins>
      <plugin>
        <groupId>com.day.jcr.vault</groupId>
        <artifactId>content-package-maven-plugin</artifactId>
        <version>0.0.24</version>
        <configuration>
          <builtContentDirectory>jcr_root</builtContentDirectory>
          <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
        </configuration>
        <executions>
          <execution>
            <goals>
              <goal>package</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
</project>
```

### ls {#ls}

Enumera los paquetes implementados en el Administrador de paquetes.

#### Parámetros {#parameters-2}

Todos los parámetros del objetivo ls se describen en la sección Parámetros [](#common-parameters) comunes.

#### Ejemplo {#example-2}

En el siguiente ejemplo se muestran los paquetes instalados en la instancia de AEM con la dirección IP 10.36.79.223. El objetivo se ejecuta con el siguiente comando:

```shell
mvn content-package:ls
```

El siguiente archivo POM se encuentra en el directorio actual de la herramienta de línea de comandos. El POM especifica la dirección URL del servicio de paquetes.

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>example-package</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
      <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
      </plugin>
   </plugins>
     </build>
</project>
```

### rm {#rm}

Quita un paquete del Administrador de paquetes.

#### Parámetros {#parameters-3}

Todos los parámetros del objetivo rm se describen en la sección Parámetros [](#common-parameters) comunes.

#### Ejemplo {#example-3}

En el ejemplo siguiente se elimina el paquete workflow-mbean que está instalado en la instancia de AEM con la dirección IP 10.36.79.223. El objetivo se ejecuta con el siguiente comando:

```shell
mvn content-package:rm
```

El siguiente archivo POM se encuentra en el directorio actual de la herramienta de línea de comandos. El POM especifica la dirección URL del servicio de paquetes y el nombre del paquete.

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>example-package</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
                    <name>workflow-mbean</name>
      <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
      </plugin>
   </plugins>
     </build>
</project>
```

### uninstall {#uninstall}

Desinstala un paquete. El paquete permanece en el servidor en estado desinstalado.

#### Parámetros {#parameters-4}

Todos los parámetros del objetivo de desinstalación se describen en la sección Parámetros [](#common-parameters) comunes.

#### Ejemplo {#example-4}

En el siguiente ejemplo se desinstala el paquete workflow-mbean que está instalado en la instancia de AEM con la dirección IP 10.36.79.223. El objetivo se ejecuta con el siguiente comando:

```shell
mvn content-package:uninstall
```

El siguiente archivo POM se encuentra en el directorio actual de la herramienta de línea de comandos. El POM especifica el nombre del paquete y la dirección URL del servicio de paquetes.

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
   <name>workflow-mbean</name>
   <failOnError>true</failOnError>
   <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
     </plugin>
 </plugins>
    </build>
</project>
```

### package {#package}

Crea un paquete de contenido. La configuración predeterminada del objetivo del paquete incluye el contenido del directorio donde se guardan los archivos compilados. La ejecución del objetivo del paquete requiere que la fase de compilación se haya completado. El objetivo del paquete está enlazado a la fase del paquete del ciclo vital de la compilación de Maven.

#### Parámetros {#parameters-5}

Además de los parámetros siguientes, consulte la descripción del `name` parámetro en la sección Parámetros [](#common-parameters) comunes.

<table>
 <tbody>
  <tr>
   <th>Nombre</th>
   <th>Tipo</th>
   <th>Requerido</th>
   <th>Valor predeterminado</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>archive</td>
   <td>org.apache.maven.<br /> archiver.<br /> MavenArchiveConfiguration</td>
   <td>No</td>
   <td></td>
   <td>La configuración del archivo que se va a utilizar. Consulte <a href="https://maven.apache.org/shared/maven-archiver/index.html">la documentación de Maven Archiver</a>.</td>
  </tr>
  <tr>
   <td>buildContentDirectory</td>
   <td>java.io.File</td>
   <td>Sí</td>
   <td>Valor del directorio de salida de la compilación de Maven.</td>
   <td>El directorio que contiene el contenido que se va a incluir en el paquete.</td>
  </tr>
  <tr>
   <td>dependencias</td>
   <td>java.util.List</td>
   <td>No</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>EmbeddedTarget</td>
   <td>java.lang.String</td>
   <td>No</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>incrustado</td>
   <td>java.util.List</td>
   <td>No</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>failOnMissingEmbed</td>
   <td>boolean</td>
   <td>Sí</td>
   <td>false</td>
   <td>Un valor true hace que la compilación falle cuando no se encuentra un artefacto incrustado en las dependencias del proyecto. Un valor false hace que la compilación ignore el error.</td>
  </tr>
  <tr>
   <td>filterSource</td>
   <td>java.io.File</td>
   <td>No</td>
   <td></td>
   <td>Archivo que especifica el origen del filtro de área de trabajo. Los filtros especificados en la configuración e insertados mediante emebed o subpackages se combinan con el contenido del archivo.</td>
  </tr>
  <tr>
   <td>filtros</td>
   <td>com.day.jcr.<br /> vault.maven.pack.impl.<br /> DefaultWorkspaceFilter</td>
   <td>No</td>
   <td></td>
   <td>Contiene elementos de filtro que definen el contenido del paquete. Cuando se ejecutan, los filtros se incluyen en el archivo filter.xml. Consulte la sección Uso de filtros a continuación.</td>
  </tr>
  <tr>
   <td>finalName</td>
   <td>java.lang.String</td>
   <td>Sí</td>
   <td>El valor finalName definido en el proyecto Maven (fase de compilación).</td>
   <td>Nombre del archivo ZIP del paquete generado, sin la extensión de archivo .zip.</td>
  </tr>
  <tr>
   <td>grupo</td>
   <td>java.lang.String</td>
   <td>Sí</td>
   <td>El groupID definido en el proyecto Maven.</td>
   <td>El groupId del paquete de contenido generado. Este valor forma parte de la ruta de instalación de destino para el paquete de contenido.</td>
  </tr>
  <tr>
   <td>outputDirectory</td>
   <td>java.io.File</td>
   <td>Sí</td>
   <td>Directorio de compilación definido en el proyecto Maven.</td>
   <td>El directorio local donde se guarda el paquete de contenido.</td>
  </tr>
  <tr>
   <td>prefix</td>
   <td>java.lang.String</td>
   <td>No</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>proyecto</td>
   <td>org.apache.maven.<br /> project.MavenProject</td>
   <td>Sí</td>
   <td></td>
   <td>El proyecto Maven.</td>
  </tr>
  <tr>
   <td>propiedades</td>
   <td>java.util.Map</td>
   <td>No</td>
   <td></td>
   <td>Propiedades adicionales que puede establecer en el archivo properties.xml. Estas propiedades no pueden sobrescribir las siguientes propiedades predefinidas:
    <ul>
     <li>grupo: Use el parámetro de grupo para establecer</li>
     <li>name: Utilice el parámetro name para establecer</li>
     <li>version: Utilice el parámetro version para establecer</li>
     <li>description: Se configura a partir de la descripción del proyecto</li>
     <li>groupId: groupId del descriptor de proyecto de Maven</li>
     <li>artiactId: artiactId del descriptor de proyecto de Maven</li>
     <li>dependencias: Usar parámetro de dependencias para establecer</li>
     <li>createdBy: El valor de la propiedad del sistema user.name</li>
     <li>creado: Hora del sistema actual</li>
     <li>requireRoot: Use el parámetro requirementsRoot para establecer</li>
     <li>packagePath: Generado automáticamente a partir del nombre del grupo y del paquete</li>
    </ul> </td>
  </tr>
  <tr>
   <td>requirementsRoot</td>
   <td>boolean</td>
   <td>Sí</td>
   <td>false</td>
   <td>Define si el paquete requiere root. Se convertirá en la propiedad &lt;code&gt;requirementsRoot&lt;/code&gt; del archivo properties.xml.</td>
  </tr>
  <tr>
   <td>subPackages</td>
   <td>java.util.List</td>
   <td>No</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>version</td>
   <td>java.lang.String</td>
   <td>Sí</td>
   <td>Versión definida en el proyecto Maven</td>
   <td>Versión del paquete de contenido.</td>
  </tr>
  <tr>
   <td>workDirectory</td>
   <td>java.io.File</td>
   <td>Sí</td>
   <td>Directorio definido en el proyecto Maven (fase de compilación).</td>
   <td>El directorio que contiene el contenido que se incluirá en el paquete.</td>
  </tr>
 </tbody>
</table>

#### Uso de filtros {#using-filters}

Utilice el elemento filters para definir el contenido del paquete. Los filtros se agregan al elemento spaceFilter del `META-INF/vault/filter.xml` archivo del paquete.

El siguiente ejemplo de filtro muestra la estructura XML que se va a utilizar:

```xml
<filter>
   <root>/apps/myapp</root>
   <mode>merge</mode>
       <includes>
              <include>/apps/myapp/install/</include>
              <include>/apps/myapp/components</include>
       </includes>
       <excludes>
              <exclude>/apps/myapp/config/*</exclude>
       </excludes>
</filter>
```

**Modo de importación**

El `mode` elemento define cómo se ve afectado el contenido del repositorio cuando se importa el paquete. Se pueden utilizar los siguientes valores:

* **** Combinar: Se agrega el contenido del paquete que no se encuentra en el repositorio. El contenido que se encuentra tanto en el paquete como en el repositorio no cambia. No se elimina contenido del repositorio.
* **** Reemplazar: El contenido del paquete que no está en el repositorio se agrega al repositorio. El contenido del repositorio se sustituye por el contenido coincidente del paquete. El contenido se elimina del repositorio cuando no existe en el paquete.
* **** Actualización: El contenido del paquete que no está en el repositorio se agrega al repositorio. El contenido del repositorio se sustituye por el contenido coincidente del paquete. El contenido existente se elimina del repositorio.

Cuando el filtro no contiene ningún `mode` elemento, se utiliza el valor predeterminado de `replace` .

#### Ejemplo {#example-5}

En el ejemplo siguiente se crea un paquete que contiene el paquete OSGi de flujo de trabajo. El archivo POM identifica el directorio jcr_root como el valor de la propiedad buildContentDirectory. El directorio jcr_root contiene el archivo JAR del paquete en la estructura de directorio que refleja el repositorio:

`jcr_root/apps/myapp/install/workflow-mbean-0.03-SNAPSHOT.jar`

Dado que el objetivo está enlazado a la fase de compilación del paquete, el siguiente comando ejecuta el objetivo del paquete:

`mvn package`

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
    https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>

  <build>
    <plugins>
      <plugin>
        <groupId>com.day.jcr.vault</groupId>
        <artifactId>content-package-maven-plugin</artifactId>
        <version>0.0.24</version>
        <configuration>
          <builtContentDirectory>jcr_root</builtContentDirectory>
          <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
        </configuration>
        <executions>
          <execution>
            <goals>
              <goal>package</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
</project>
```

En lugar de expresar el `package` objetivo en la sección del complemento `executions` , puede usar `content-package` como valor del `packaging` elemento del proyecto:

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
    https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>
  <packaging>content-package</packaging>
  <build>
    <plugins>
      <plugin>
        <groupId>com.day.jcr.vault</groupId>
        <artifactId>content-package-maven-plugin</artifactId>
        <version>0.0.24</version>
        <configuration>
          <builtContentDirectory>jcr_root</builtContentDirectory>
          <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

### ayuda {#help}

#### Parámetros {#parameters-6}

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción |
|---|---|---|---|---|
| detalle | boolean | No | false | Determina si se mostrarán todas las propiedades configurables para cada objetivo. El valor true muestra todas las propiedades configurables. |
| objetivo | Cadena | No |  | Nombre del objetivo para el cual mostrar la ayuda. Si no se especifica ningún valor, se muestra la ayuda para todos los objetivos. |
| indentSize | int | No | 2 | Número de espacios que se utilizarán para la sangría de cada nivel. Si especifica un valor, el valor debe ser positivo. |
| lineLength | int | No | 80 | Longitud máxima de una línea de visualización. Si especifica un valor, el valor debe ser positivo. |

## Obtención del complemento Content Package Maven {#obtaining-the-content-package-maven-plugin}

El complemento está disponible en el repositorio público de Adobe. Para descargar el complemento, agregue el siguiente perfil de Maven al archivo de configuración de Maven y actívelo. Cuando se utiliza un comando Maven, el complemento se descarga en el repositorio local si es necesario.

>[!NOTE]
>
>El repositorio de versiones públicas de Adobe no se puede explorar, por lo que la navegación a la dirección URL del repositorio mediante el navegador web produce un error No encontrado. Sin embargo, Maven puede acceder a los directorios del repositorio.

```xml
<profile>
    <id>adobe-public</id>
    <activation>
         <activeByDefault>false</activeByDefault>
    </activation>
    <properties>
         <releaseRepository-Id>adobe-public-releases</releaseRepository-Id>
         <releaseRepository-Name>Adobe Public Releases</releaseRepository-Name>
         <releaseRepository-URL>https://repo.adobe.com/nexus/content/groups/public</releaseRepository-URL>
    </properties>
    <repositories>
         <repository>
             <id>adobe-public-releases</id>
             <name>Adobe Basel Public Repository</name>
             <url>https://repo.adobe.com/nexus/content/groups/public</url>
             <releases>
                 <enabled>true</enabled>
                 <updatePolicy>never</updatePolicy>
             </releases>
             <snapshots>
                 <enabled>false</enabled>
             </snapshots>
         </repository>
     </repositories>
     <pluginRepositories>
         <pluginRepository>
             <id>adobe-public-releases</id>
             <name>Adobe Basel Public Repository</name>
             <url>https://repo.adobe.com/nexus/content/groups/public</url>
             <releases>
                 <enabled>true</enabled>
                 <updatePolicy>never</updatePolicy>
             </releases>
             <snapshots>
                 <enabled>false</enabled>
             </snapshots>
         </pluginRepository>
     </pluginRepositories>
</profile>
```

## Incrustación de paquetes OSGi en un paquete de contenido {#embedding-osgi-bundles-in-a-content-package}

Utilice el complemento Maven del paquete de contenido para incrustar paquetes OSGi en el paquete de contenido. Para incrustar el paquete, implemente las siguientes configuraciones:

* El paquete debe declararse como una dependencia del proyecto Maven.
* La configuración del complemento hace referencia al paquete usando la ruta deseada del paquete en el paquete.

El siguiente ejemplo de POM crea un paquete que contiene el paquete UserManager de Apache Sling JCR. En el paquete, el JAR del paquete se encuentra en la `jcr_root/apps/myapp/install` carpeta:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0"
             xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
             https://maven.apache.org/maven-v4_0_0.xsd">
 <modelVersion>4.0.0</modelVersion>
   <groupId>com.adobe.example.myapp</groupId>
 <artifactId>embedded-example</artifactId>
 <packaging>content-package</packaging>
 <version>1.0.0-SNAPSHOT</version>

   <build>
 <plugins>
     <plugin>
        <groupId>com.day.jcr.vault</groupId>
      <artifactId>content-package-maven-plugin</artifactId>
      <version>0.0.24</version>
      <extensions>true</extensions>
      <configuration>
   <filters>
       <filter>
    <root>/apps/myapp</root>
       </filter>
    </filters>
    <embeddeds>
       <embedded>
    <groupId>org.apache.sling</groupId>
    <artifactId>org.apache.sling.jcr.jackrabbit.usermanager</artifactId>
    <target>/apps/myproject/install</target>
        </embedded>
    </embeddeds>
       </configuration>
  </plugin>
    </plugins>
    </build>
    <dependencies>
 <dependency>
      <groupId>org.apache.sling</groupId>
      <artifactId>org.apache.sling.jcr.jackrabbit.usermanager</artifactId>
      <version>2.2.0</version>
 </dependency>
    </dependencies>
</project>
```

## Inclusión de una imagen en miniatura o un archivo de propiedades en el paquete {#including-a-thumbnail-image-or-properties-file-in-the-package}

Reemplace los archivos de configuración de paquete predeterminados para personalizar las propiedades del paquete. Por ejemplo, incluya una imagen en miniatura para distinguir el paquete en el Administrador de paquetes y Uso compartido de paquetes.

En el paquete, los archivos específicos de FileVault se encuentran en la carpeta /META-INF/vault. Los archivos de origen pueden ubicarse en cualquier lugar del sistema de archivos. En el archivo POM, defina los recursos de compilación para copiar los archivos de origen en target/vault-work/META-INF para incluirlos en el paquete.

El siguiente código POM agrega los archivos de la carpeta META-INF del origen del proyecto al paquete:

```xml
<build>
    <resources>
        <!-- vault META-INF resources (thumbnail etc.) -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF</directory>
            <targetPath>../vault-work/META-INF</targetPath>
        </resource>
    </resources>
</build>
```

El siguiente código POM sólo agrega una imagen en miniatura al paquete. La imagen en miniatura debe tener el nombre thumbnail.png y estar ubicada en la carpeta META-INF/vault/definition del paquete. En este ejemplo, el archivo de origen se encuentra en la carpeta /src/main/content/META-INF/vault/definition del proyecto:

```xml
<build>
    <resources>
        <!-- thumbnail only -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF/vault/definition</directory>
            <targetPath>../vault-work/META-INF/vault/definition</targetPath>
        </resource>
    </resources>
</build>
```

## Uso De Tipos De Archivo Para Generar Proyectos De AEM {#using-archetypes-to-generate-aem-projects}

Hay varios tipos de arquetes Maven disponibles para generar proyectos de AEM. Utilice el arquetipo que se corresponda con sus objetivos de desarrollo:

* Paquete de contenido que instala recursos para una aplicación AEM: [simple-content-package-archetype](#simple-content-package-archetype)
* Paquete de contenido que incluye artefactos de terceros: [simple-content-package-with-Embedded-archetype](#simple-content-package-with-embedded-archetype).
* Aplicación multimódulo que acompaña el desarrollo de clases y pruebas unitarias de Java: [multimodule-content-package-archetype](#multimodule-content-package-archetype).

>[!NOTE]
>
>El proyecto Apache Sling también ofrece arquetipos útiles para el desarrollo de AEM. Estos documentos están documentados en [https://sling.apache.org/site/maven-archetypes.html](https://sling.apache.org/documentation/development/maven-archetypes.html).

Cada arquetipo genera los siguientes elementos:

* Estructura de carpetas del proyecto.
* Archivos POM.
* Archivos de configuración de FileVault.

Los artefactos de arquetipo están disponibles en el repositorio público de Adobe Maven. Para descargar y ejecutar un arquetipo, identifique el arquetipo y el repositorio de Adobe utilizando los parámetros del comando Maven archetype:generate:

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId={id_of_archetype} -DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

El complemento arquetipo Maven utiliza el modo interactivo en el shell o en el símbolo del sistema para recopilar información sobre su proyecto. La información proporcionada se utiliza para configurar diversas propiedades del proyecto, como nombres de carpetas e ID de artefactos.

**Archivos POM**

Los archivos POM generados incluyen comandos para compilar código, crear paquetes e implementarlos en AEM en paquetes. Las propiedades `groupID`, `artifactId`, `version`y `name` del proyecto Maven se rellenan automáticamente con los valores que proporcione al mensaje interactivo de Maven `archetype:generate` .

Puede que desee cambiar los siguientes valores predeterminados en el archivo pom.xml generado:

* El nombre del servidor de CQ o la dirección IP: El valor predeterminado es `localhost`. El `crx.host` elemento siguiente `project/properties` contiene este valor.

* El número de puerto del servidor CQ: El valor predeterminado es `4502`. El `crx.port` elemento siguiente `project/properties` contiene este valor.

* Versión del complemento Content Package Maven: Utilice la versión más reciente como contenido del `version` elemento para el complemento con `artifactId` de `content-package-maven-plugin`. El valor predeterminado es `0.0.24`.

**Uso de los arquetipos**

1. En una ventana shell o símbolo del sistema, introduzca el comando Maven `archetype:generate` . Cuando se le pida, proporcione valores para los parámetros restantes.

   Para obtener información sobre cada parámetro, consulte la sección correspondiente al arquetipo que está utilizando.

1. Utilice un editor de texto para abrir el archivo pom.xml y editar los valores predeterminados según sus requisitos.
1. Rellene las carpetas generadas con recursos.
1. Introduzca el `mvn clean install` comando.

### simple-content-package-archetype {#simple-content-package-archetype}

Crea un proyecto concreto adecuado para instalar recursos para una aplicación sencilla de AEM. La estructura de carpetas es la que se utiliza debajo de la `/apps` carpeta del repositorio de AEM. El POM define comandos para empaquetar los recursos que se colocan en las carpetas e instalar los paquetes en la instancia de AEM.

**Propiedades del artefacto de arquetipo:**

* ID del grupo: `com.day.jcr.vault`
* ID del artefacto: `simple-content-package-archetype`
* Versión: `1.0.2`
* Repositorio: `adobe-public-releases`

**Maven, comando:**

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId=simple-content-package-archetype \
-DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

**Parámetros de arquetipo:**

* groupId: GroupId del paquete de contenido que genera Maven. El valor se utiliza automáticamente en el archivo POM.
* artiactId: Nombre del paquete de contenido. El valor también se utiliza como nombre de la carpeta del proyecto.
* version:Versión del paquete de contenido.
* paquete: Este valor no se utiliza para simple-content-package-archetype.
* appsFolderName: El nombre de la carpeta debajo de /apps.
* artiactName: Descripción del paquete de contenido.
* packageGroup: Nombre del grupo de paquetes de contenido. Este valor configura el parámetro group para el objetivo Package del complemento Content Package Maven.

**Estructura de carpetas:**

```xml
${artifactId}
   |- pom.xml
   |- README.txt
   |- src
      |- main
         |- content
             |- jcr_root
                 |- apps
                     |- ${appsFolderName}
                            |- components
                               |- .content.xml
                            |- config
                            |- install
             |- META-INF
                 |- vault
                     |- config.xml
                     |- filter.xml
                     |- nodetypes.cnd
                     |- properties.xml
                     |- definition
                        |- .content.xml
```

### simple-content-package-with-Embedded-archetype {#simple-content-package-with-embedded-archetype}

Realiza las mismas tareas que el simple-content-package-archetype, y también descarga e incluye un artefacto de un repositorio público de Maven.

**Propiedades del paquete de arquetipos:**

* ID del grupo: `com.day.jcr.vault`
* ID del artefacto: `simple-content-package-with-embedded-archetype`
* Versión: `1.0.2`
* Repositorio: `adobe-public-releases`

**Maven, comando:**

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId=simple-content-package-with-embedded-archetype \
-DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

**Parámetros de arquetipo:**

* groupId: GroupId del paquete de contenido que genera Maven. El valor se utiliza automáticamente en el archivo POM.
* artiactId: Nombre del paquete de contenido. El valor también se utiliza como nombre de la carpeta del proyecto.
* version:Versión del paquete de contenido.
* paquete: Este parámetro no se utiliza.
* appsFolderName: El nombre de la carpeta debajo de /apps.
* artiactName: Descripción del paquete de contenido.
* EmbeddedArtiactId: ID del artefacto que se va a incrustar en el paquete de contenido.
* EmbeddedGroupId: ID de grupo del artefacto que se va a incrustar.
* EmbeddedVersion: Versión del artefacto que se va a incrustar.
* packageGroup: Nombre del grupo de paquetes de contenido. Este valor configura el parámetro group para el objetivo Package del complemento Content Package Maven.

**Estructura de carpetas:**

```xml
${artifactId}
   |- pom.xml
   |- README.txt
   |- src
      |- main
         |- content
             |- jcr_root
                 |- apps
                     |- ${appsFolderName}
                            |- components
                            |- config
                            |- install
             |- META-INF
                 |- vault
                     |- config.xml
                     |- filter.xml
                     |- nodetypes.cnd
                     |- properties.xml
                     |- definition
```

### multimodule-content-package-archetype {#multimodule-content-package-archetype}

Crea un proyecto dinámico que incluye la estructura de carpetas para desarrollar una aplicación de AEM e instalar recursos en el servidor.

La `bundle` carpeta contiene la estructura de carpetas que almacena los archivos de origen Java y JUnit que desarrolla. El archivo pom.xml de esta carpeta crea el paquete OSGi. Los siguientes valores del POM identifican el artefacto y el paquete:

* artiactID: `${artifactID}-bundle`.
* Nombre simbólico del paquete: `${groupId}.${artifactId}-bundle`.

`${artifactID}` y `${groupId}` son los valores que se proporcionan para estos parámetros al ejecutar los arquetipos.

La `content` carpeta contiene los recursos instalados en la instancia de AEM. El valor de artifactsID es `${artifactID}multimodule-bundle`.

La carpeta principal contiene el POM principal que administra los complementos y las dependencias de Maven.

**Propiedades del paquete de arquetipos:**

* ID del grupo: `com.day.jcr.vault`
* ID del artefacto: `multimodule-content-package-archetype`
* Versión: `1.0.2`
* Repositorio: `adobe-public-releases`

**Maven, comando:**

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId=multimodule-content-package-archetype \
-DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

**Parámetros de arquetipo:**

* groupId: GroupId del paquete de contenido que genera Maven. El valor se utiliza automáticamente en el archivo POM.
* artiactId: Nombre del paquete de contenido. El valor también se utiliza como nombre de la carpeta del proyecto.
* version:Versión del paquete de contenido.
* paquete: Este valor no se utiliza para multimodule-content-package-archetype.
* appsFolderName: El nombre de la carpeta debajo de /apps.
* artiactName: Descripción del paquete de contenido.
* packageGroup: Nombre del grupo de paquetes de contenido. Este valor configura el parámetro group para el objetivo Package del complemento Content Package Maven.

**Estructura de carpetas:**

```xml
${artifactId}
   |- pom.xml
   |- bundle
      |- pom.xml
      |- src
         |- main
            |- java
               |- ${groupId}
                  |- SimpleDSComponent.java
         |- test
            |- java
               |- ${groupId}
                  |- SimpleUnitTest.java
   |- content
      |- pom.xml
      |- src
         |- main
            |- content
               |- jcr_root
                  |- apps
                     |- ${appsFolderName}
                            |- config
                            |- install
                  |- META-INF
                      |- vault
                         |- config.xml
                         |- filter.xml
                         |- nodetypes.cnd
                         |- properties.xml
                         |- definition
                            |- .content.xml
```

