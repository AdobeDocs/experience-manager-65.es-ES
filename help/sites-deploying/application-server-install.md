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
source-git-commit: 0a082d3cff66b82ef6de551a735a16a001446a1e
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 1%

---


# Instalación del servidor de aplicaciones{#application-server-install}

>[!NOTE]
>
>`JAR` y  `WAR` son los tipos de archivo en los que se AEM. Estos formatos están siendo sometidos a un control de calidad para adaptarse a los niveles de soporte a los que se ha comprometido el Adobe.


En esta sección se explica cómo instalar Adobe Experience Manager (AEM) con un servidor de aplicaciones. Consulte la sección [Plataformas admitidas](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) para ver los niveles de soporte específicos proporcionados para los servidores de aplicaciones individuales.

Se describen los pasos de instalación de los siguientes servidores de aplicaciones:

* [WebSphere 8.5](#websphere)
* [EAP de JBoss 6.3.0/6.4.0](#jboss-eap)
* [Oracle WebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

Consulte la documentación del servidor de aplicaciones correspondiente para obtener más información sobre la instalación de aplicaciones Web, configuraciones de servidor y cómo realizar el inicio y detener el servidor.

>[!NOTE]
>
>Si está utilizando Dynamic Media en una implementación de WAR, consulte la [documentación de Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

## Descripción general {#general-description}

### Comportamiento predeterminado al instalar AEM en un servidor de aplicaciones {#default-behaviour-when-installing-aem-in-an-application-server}

AEM viene como un único archivo de guerra para desplegar.

Si se implementa lo siguiente sucederá de forma predeterminada:

* el modo de ejecución es `author`
* la instancia (Repositorio, entorno Felix OSGI, paquetes, etc.) se instala en `${user.dir}/crx-quickstart`donde `${user.dir}` es el directorio de trabajo actual, esta ruta a crx-quickstart se denomina `sling.home`

* la raíz del contexto es el nombre del archivo de guerra, por ejemplo: `aem-6`

#### Configuración {#configuration}

Puede cambiar el comportamiento predeterminado de la siguiente manera:

* modo de ejecución: configure el parámetro `sling.run.modes` en el archivo `WEB-INF/web.xml` del archivo de guerra de AEM antes de la implementación

* sling.home: configure el parámetro `sling.home` en el archivo `WEB-INF/web.xml`del archivo de guerra de AEM antes de la implementación

* raíz de contexto: cambiar el nombre del archivo de guerra AEM

#### Instalación de publicación {#publish-installation}

Para implementar una instancia de publicación, debe definir el modo de ejecución para la publicación:

* Desempaquetar el WEB-INF/web.xml del archivo de guerra de AEM
* Cambiar el parámetro sling.run.mode para publicar
* Volver a empaquetar el archivo web.xml en AEM archivo de guerra
* Implementar AEM archivo de guerra

#### Comprobación de la instalación {#installation-check}

Para comprobar si todo está instalado, puede:

* etiquete el archivo `error.log`para ver que todo el contenido está instalado
* observe en `/system/console` que todos los paquetes están instalados

#### Dos instancias en el mismo servidor de aplicaciones {#two-instances-on-the-same-application-server}

A efectos de demostración, puede ser adecuado instalar la instancia de creación y publicación en un servidor de aplicaciones. Para ello, haga lo siguiente:

1. Cambie las variables sling.home y sling.run.mode de la instancia de publicación.
1. Descomprima el archivo WEB-INF/web.xml del archivo de guerra de AEM.
1. Cambie el parámetro sling.home a una ruta diferente (se pueden usar rutas absolutas y relativas).
1. Cambie sling.run.mode para publicar en la instancia de publicación.
1. Vuelva a empaquetar el archivo web.xml.
1. Cambie el nombre de los archivos de guerra para que tengan nombres diferentes: Por ejemplo, un nombre para aemauthor.war y otro para aempublish.war.
1. Utilice una configuración de memoria más alta, por ejemplo para las instancias de AEM predeterminadas, utilice, por ejemplo: -Xmx3072m
1. Implementar las dos aplicaciones web.
1. Después de la implementación, detenga las dos aplicaciones web.
1. Tanto en el caso de autor como en el de publicación se garantiza que en los archivos sling.properties la propiedad felix.service.urlhandlers=false se establece en false (el valor predeterminado es que se establece en true).
1. Vuelva a poner en inicio las dos aplicaciones web.

## Procedimientos de instalación de los servidores de aplicaciones {#application-servers-installation-procedures}

### WebSphere 8.5 {#websphere}

Antes de una implementación, lea la [Descripción general](#general-description) anterior.

**Preparación del servidor**

* Permita el paso de los encabezados de autenticación básicos:

   * Una manera de permitir que AEM autentique a un usuario es deshabilitar la seguridad administrativa global del servidor WebSphere, para ello: vaya a Seguridad -> Seguridad global y desmarque la casilla Activar seguridad administrativa, guarde y reinicie el servidor.

* configurar `"JAVA_OPTS= -Xmx2048m"`
* Si desea instalar AEM usando context root = /, primero debe cambiar la raíz de contexto de la aplicación web predeterminada existente

**Implementar AEM aplicación web**

* Descargar AEM archivo de guerra
* Realice sus configuraciones en web.xml si es necesario (consulte arriba en la Descripción general)

   * Desempaquetar WEB-INF/web.xml archivo
   * cambie el parámetro sling.run.mode para publicar
   * uncomment sling.home, parámetro inicial y establezca esta ruta como lo necesite
   * Volver a empaquetar archivo web.xml

* Implementar AEM archivo de guerra

   * Elija una raíz de contexto (si desea establecer los modos de ejecución de sling, debe seleccionar los pasos detallados del asistente de implementación y luego especificarlos en el paso 6 del asistente)

* Inicio AEM aplicación Web

#### EAP de JBoss 6.3.0/6.4.0 {#jboss-eap}

Antes de una implementación, lea la [Descripción general](#general-description) anterior.

**Preparar el servidor JBoss**

Configure los argumentos de la memoria en el archivo conf (p. ej. `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

si utiliza el analizador de implementación para instalar la aplicación Web AEM, puede que sea conveniente aumentar el atributo `deployment-timeout,` para ese conjunto de atributos `deployment-timeout` en el archivo xml de la instancia (por ejemplo, `configuration/standalone.xml)`:

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**Implementar AEM aplicación web**

* Cargue la aplicación Web AEM en la Consola de administración de JBoss.

* Habilite la aplicación Web AEM.

#### Oracle WebLogic 12.1.3/12.2 {#oracle-weblogic}

Antes de una implementación, lea la [Descripción general](#general-description) anterior.

Utiliza un diseño de servidor sencillo con un servidor de administración único.

**Preparación del servidor WebLogic**

* En `${myDomain}/config/config.xml`agregue a la sección de configuración de seguridad:

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` consulte en  [https://xmlns.oracle.com/weblogic/domain/1.0/domain.](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) xsdpara ver la posición correcta (de forma predeterminada, la posición al final de la sección es correcta)

* Aumentar la configuración de memoria de VM:

   * abrir `${myDomain}/bin/setDomainEnv.cmd` (resp.sh)buscar WLS_MEM_ARGS, establecer por ejemplo `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * reiniciar WebLogic Server

* Cree en `${myDomain}` una carpeta de paquetes y dentro de una carpeta cq y en ella una carpeta Plan

**Implementar AEM aplicación web**

* Descargar AEM archivo de guerra
* Coloque el archivo de guerra AEM en la carpeta ${myDomain}/packages/cq
* Realice sus configuraciones en `WEB-INF/web.xml` si es necesario (consulte arriba en la Descripción general)

   * Desempaquetar `WEB-INF/web.xml`archivo
   * cambie el parámetro sling.run.mode para publicar
   * dejar de comentar el parámetro inicial sling.home y establecer esta ruta como sea necesario (consulte Descripción general)
   * Volver a empaquetar archivo web.xml

* Implementar AEM archivo de guerra como una aplicación (para el resto de configuraciones, use la configuración predeterminada)
* La instalación puede llevar tiempo...
* Compruebe que la instalación ha finalizado como se mencionó anteriormente en la Descripción general (p. ej., cambiando el error.log)
* Puede cambiar la raíz de contexto en la ficha Configuración de la aplicación Web en WebLogic `/console`

#### Tomcat 8/8.5 {#tomcat}

Antes de una implementación, lea la [Descripción general](#general-description) anterior.

* **Preparar el servidor Tomcat**

   * Aumentar la configuración de memoria de VM:

      * En `bin/catalina.bat` (resp `catalina.sh` en unix) agregue la siguiente configuración:
      * `set "JAVA_OPTS= -Xmx2048m`
   * Tomcat no permite el acceso de administrador ni administrador durante la instalación. Por lo tanto, debe editar `tomcat-users.xml` manualmente para permitir el acceso a estas cuentas:

      * Edite `tomcat-users.xml` para incluir el acceso de administrador y administrador. La configuración debe tener un aspecto similar al siguiente ejemplo:

         ```xml
         <?xml version='1.0' encoding='utf-8'?>
         <tomcat-users>
         role rolename="manager"/>
         role rolename="tomcat"/>
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
      * aplicación web de inicio de nuevo
   * Si instala la aplicación web AEM con el manager-gui, deberá aumentar el tamaño máximo de un archivo cargado, ya que el valor predeterminado solo permite un tamaño de carga de 50 MB. Para ello, abra el archivo web.xml de la aplicación web del administrador,

      `webapps/manager/WEB-INF/web.xml`

      y aumente el tamaño máximo de archivo y el tamaño máximo de solicitud a al menos 500 MB, consulte el siguiente ejemplo `multipart-config` de un archivo `web.xml` de este tipo.

      ```xml
      <multipart-config>
      <!-- 500MB max -->
      <max-file-size>524288000</max-file-size>
      <max-request-size>524288000</max-request-size>
      <file-size-threshold>0</file-size-threshold>
      </multipart-config>
      ```




* **Implementar AEM aplicación web**

   * Descargar AEM archivo de guerra
   * Realice sus configuraciones en web.xml si es necesario (consulte arriba en la Descripción general)

      * Desempaquetar WEB-INF/web.xml archivo
      * cambie el parámetro sling.run.mode para publicar
      * uncomment sling.home, parámetro inicial y establezca esta ruta como lo necesite
      * Volver a empaquetar archivo web.xml
   * Cambie AEM archivo de guerra a ROOT.war si desea implementarlo como aplicación web raíz, cambie el nombre a aemauthor.war si desea que aemauthor sea context root
   * copiarlo en la carpeta de aplicaciones web de tomcat
   * esperar hasta que AEM instalado


## Solución de problemas {#troubleshooting}

Para obtener información sobre cómo solucionar los problemas que pueden surgir durante la instalación, consulte:

* [Solución de problemas](/help/sites-deploying/troubleshooting.md)
