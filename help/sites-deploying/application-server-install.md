---
title: Instalación del servidor de aplicaciones
seo-title: Instalación del servidor de aplicaciones
description: Obtenga información sobre cómo instalar AEM con un servidor de aplicaciones.
seo-description: Obtenga información sobre cómo instalar AEM con un servidor de aplicaciones.
uuid: c9571f80-6ed1-46fe-b7c3-946658dfc3f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6fdce35d-2709-41cc-87fb-27a4b867e960
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Instalación del servidor de aplicaciones{#application-server-install}

>[!NOTE]
>
>`JAR` y `WAR` ¿en qué tipos de archivo se libera AEM? Estos formatos están sometidos a un proceso de garantía de calidad para adaptarse a los niveles de asistencia a los que Adobe se ha comprometido.


En esta sección se explica cómo instalar Adobe Experience Manager (AEM) con un servidor de aplicaciones. Consulte la sección Plataformas [](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) admitidas para ver los niveles de soporte específicos proporcionados para los servidores de aplicaciones individuales.

Se describen los pasos de instalación de los siguientes servidores de aplicaciones:

* [WebSphere 8.5](#websphere)
* [EAP de JBoss 6.3.0/6.4.0](#jboss-eap)
* [Oracle WebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

Consulte la documentación del servidor de aplicaciones correspondiente para obtener más información sobre la instalación de aplicaciones Web, configuraciones de servidor y cómo iniciar y detener el servidor.

>[!NOTE]
>
>Si está utilizando Dynamic Media en una implementación de WAR, consulte la documentación [de medios](/help/assets/config-dynamic.md#enabling-dynamic-media)dinámicos.

## Descripción general {#general-description}

### Comportamiento predeterminado al instalar AEM en un servidor de aplicaciones {#default-behaviour-when-installing-aem-in-an-application-server}

AEM se presenta como un solo archivo de guerra para su implementación.

Si se implementa lo siguiente sucederá de forma predeterminada:

* el modo de ejecución es `author`
* la instancia (Repositorio, entorno Felix OSGI, paquetes, etc.) está instalado en `${user.dir}/crx-quickstart`donde `${user.dir}` es el directorio de trabajo actual, se llama esta ruta a crx-quickstart `sling.home`

* la raíz del contexto es el nombre del archivo de guerra, por ejemplo: `aem-6`

#### Configuración {#configuration}

Puede cambiar el comportamiento predeterminado de la siguiente manera:

* modo de ejecución: configure el `sling.run.modes` parámetro en el archivo `WEB-INF/web.xml` del archivo de guerra de AEM antes de la implementación

* sling.home: configurar el `sling.home` parámetro en el `WEB-INF/web.xml`archivo de guerra de AEM antes de la implementación

* raíz de contexto: cambiar el nombre del archivo de guerra de AEM

#### Instalación de publicación {#publish-installation}

Para implementar una instancia de publicación, debe definir el modo de ejecución para la publicación:

* Desempaquetar el WEB-INF/web.xml del archivo de guerra de AEM
* Cambiar el parámetro sling.run.mode para publicar
* Volver a empaquetar el archivo web.xml en el archivo de guerra de AEM
* Implementar archivo de guerra AEM

#### Comprobación de la instalación {#installation-check}

Para comprobar si todo está instalado, puede:

* cola el `error.log`archivo para ver que todo el contenido está instalado
* observe `/system/console` que todos los paquetes están instalados

#### Dos instancias en el mismo servidor de aplicaciones {#two-instances-on-the-same-application-server}

A efectos de demostración, puede ser adecuado instalar la instancia de creación y publicación en un servidor de aplicaciones. Para ello, haga lo siguiente:

1. Cambie las variables sling.home y sling.run.mode de la instancia de publicación.
1. Descomprima el archivo WEB-INF/web.xml del archivo de guerra de AEM.
1. Cambie el parámetro sling.home a una ruta diferente (se pueden usar rutas absolutas y relativas).
1. Cambie sling.run.mode para publicar en la instancia de publicación.
1. Vuelva a empaquetar el archivo web.xml.
1. Cambie el nombre de los archivos de guerra para que tengan nombres diferentes: Por ejemplo, un nombre para aemauthor.war y otro para aempublish.war.
1. Utilice una configuración de memoria superior, por ejemplo, para las instancias predeterminadas de AEM, utilice, por ejemplo: -Xmx3072m
1. Implementar las dos aplicaciones web.
1. Después de la implementación, detenga las dos aplicaciones web.
1. Tanto en el caso de autor como en el de publicación se garantiza que en los archivos sling.properties la propiedad felix.service.urlhandlers=false se establece en false (el valor predeterminado es que se establece en true).
1. Vuelva a iniciar las dos aplicaciones web.

## Procedimientos de instalación de los servidores de aplicaciones {#application-servers-installation-procedures}

### WebSphere 8.5 {#websphere}

Antes de una implementación, lea la Descripción [general](#general-description) anterior.

**Preparación del servidor**

* Permita el paso de los encabezados de autenticación básicos:

   * Una forma de permitir que AEM autentique a un usuario es desactivar la seguridad administrativa global del servidor WebSphere, para ello: vaya a Seguridad -> Seguridad global y desmarque la casilla Activar seguridad administrativa, guarde y reinicie el servidor.

* configurar `"JAVA_OPTS= -Xmx2048m"`
* Si desea instalar AEM mediante context root = /, primero debe cambiar la raíz de contexto de la aplicación web predeterminada existente

**Implementación de la aplicación web AEM**

* Descargar archivo de guerra AEM
* Realice sus configuraciones en web.xml si es necesario (consulte arriba en la Descripción general)

   * Desempaquetar WEB-INF/web.xml archivo
   * cambie el parámetro sling.run.mode para publicar
   * uncomment sling.home, parámetro inicial y establezca esta ruta como lo necesite
   * Volver a empaquetar archivo web.xml

* Implementar archivo de guerra AEM

   * Elija una raíz de contexto (si desea establecer los modos de ejecución de sling, debe seleccionar los pasos detallados del asistente de implementación y luego especificarlos en el paso 6 del asistente)

* Iniciar aplicación web de AEM

#### EAP de JBoss 6.3.0/6.4.0 {#jboss-eap}

Antes de una implementación, lea la Descripción [general](#general-description) anterior.

**Preparar el servidor JBoss**

Configure los argumentos de la memoria en el archivo conf (p. ej. `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

si utiliza el analizador de implementación para instalar la aplicación web de AEM, puede que sea conveniente aumentar el `deployment-timeout,` valor de ese conjunto de `deployment-tiimeout` atributos en el archivo xml de la instancia (por ejemplo, `configuration/standalone.xml)`:

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**Implementación de la aplicación web AEM**

* Cargue la aplicación web de AEM en la consola de administración de JBoss.

* Habilite la aplicación web de AEM.

#### Oracle WebLogic 12.1.3/12.2 {#oracle-weblogic}

Antes de una implementación, lea la Descripción [general](#general-description) anterior.

Utiliza un diseño de servidor sencillo con un servidor de administración único.

**Preparación del servidor WebLogic**

* En `${myDomain}/config/config.xml`Agregar a la sección de configuración de seguridad:

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` consulte en [https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) la posición correcta (la posición predeterminada al final de la sección es correcta)

* Aumentar la configuración de memoria de VM:

   * abrir `${myDomain}/bin/setDomainEnv.cmd` (resp.sh)buscar WLS_MEM_ARGS, establecer, por ejemplo, establecer `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * reiniciar WebLogic Server

* Crear en `${myDomain}` una carpeta de paquetes y dentro de una carpeta cq y en ella una carpeta Plan

**Implementación de la aplicación web AEM**

* Descargar archivo de guerra AEM
* Coloque el archivo de guerra de AEM en la carpeta ${myDomain}/packages/cq
* Realice sus configuraciones en `WEB-INF/web.xml` caso necesario (consulte arriba en la Descripción general)

   * Desempaquetar `WEB-INF/web.xml`archivo
   * cambie el parámetro sling.run.mode para publicar
   * dejar de comentar el parámetro inicial sling.home y establecer esta ruta como sea necesario (consulte Descripción general)
   * Volver a empaquetar archivo web.xml

* Implementar el archivo de guerra de AEM como una aplicación (para los demás ajustes, utilice la configuración predeterminada)
* La instalación puede llevar tiempo...
* Compruebe que la instalación ha finalizado como se mencionó anteriormente en la Descripción general (p. ej., cambiando el error.log)
* Puede cambiar la raíz de contexto en la ficha Configuración de la aplicación Web en WebLogic `/console`

#### Tomcat 8/8.5 {#tomcat}

Antes de una implementación, lea la Descripción [general](#general-description) anterior.

* **Preparar el servidor Tomcat**

   * Aumentar la configuración de memoria de VM:

      * En `bin/catalina.bat` (resp `catalina.sh` en unix) agregue la siguiente configuración:
      * `set "JAVA_OPTS= -Xmx2048m`
   * Tomcat no permite el acceso de administrador ni administrador durante la instalación. Por lo tanto, debe editar manualmente `tomcat-users.xml` para permitir el acceso a estas cuentas:

      * Edite `tomcat-users.xml` para incluir el acceso de administrador y administrador. La configuración debe tener un aspecto similar al siguiente ejemplo:
      * 
         ```
         <?xml version='1.0' encoding='utf-8'?>
          <tomcat-users>
          <role rolename="manager"/>
          <role rolename="tomcat"/>
          <role rolename="admin"/>
          <role rolename="role1"/>
          <role rolename="manager-gui"/>
          <user username="both" password="tomcat" roles="tomcat,role1"/>
          <user username="tomcat" password="tomcat" roles="tomcat"/>
          <user username="admin" password="admin" roles="admin,manager-gui"/>
          <user username="role1" password="tomcat" roles="role1"/>
          </tomcat-users>
         ```
   * Si desea implementar AEM con la raíz de contexto &quot;/&quot;, debe cambiar la raíz de contexto de la aplicación web ROOT existente:

      * Detener y anular la implementación de la aplicación web ROOT
      * Cambiar el nombre de la carpeta ROOT.war en la carpeta webapps de tomcat
      * Iniciar aplicación web de nuevo
   * Si instala la aplicación web de AEM mediante el administrador gui, deberá aumentar el tamaño máximo de un archivo cargado, ya que el valor predeterminado solo permite un tamaño de carga de 50 MB. Para ello, abra el archivo web.xml de la aplicación web del administrador,

      `webapps/manager/WEB-INF/web.xml`

      y aumente el tamaño máximo de archivo y el tamaño máximo de solicitud a al menos 500 MB, consulte el siguiente `multipart-config` ejemplo de un `web.xml` archivo de este tipo:

      ```
        <multipart-config>
         <!-- 500MB max -->
         <max-file-size>524288000</max-file-size>
         <max-request-size>524288000</max-request-size>
         <file-size-threshold>0</file-size-threshold>
         </multipart-config>
      ```




* **Implementación de la aplicación web AEM**

   * Descargar archivo de guerra AEM
   * Realice sus configuraciones en web.xml si es necesario (consulte arriba en la Descripción general)

      * Desempaquetar WEB-INF/web.xml archivo
      * cambie el parámetro sling.run.mode para publicar
      * uncomment sling.home, parámetro inicial y establezca esta ruta como lo necesite
      * Volver a empaquetar archivo web.xml
   * Cambie el nombre del archivo de guerra de AEM a ROOT.war si desea implementarlo como aplicación web raíz, cambie el nombre a aemauthor.war si desea que aemauthor sea raíz de contexto
   * copiarlo en la carpeta de aplicaciones web de tomcat
   * esperar hasta que AEM esté instalado


## Solución de problemas {#troubleshooting}

Para obtener información sobre cómo solucionar los problemas que pueden surgir durante la instalación, consulte:

* [Solución de problemas](/help/sites-deploying/troubleshooting.md)

