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
source-git-commit: 4090b1641467c6fb02b2fcce4df97b9fd5da4e2f
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 1%

---


# Instalación del servidor de aplicaciones{#application-server-install}

>[!NOTE]
>
>`JAR` y  `WAR` son los tipos de archivo en los que AEM se libera. Estos formatos están sometidos a un control de calidad para adaptarse a los niveles de soporte que el Adobe se ha comprometido a cumplir.


En esta sección se explica cómo instalar Adobe Experience Manager (AEM) con un servidor de aplicaciones. Consulte la sección [Plataformas admitidas](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) para ver los niveles de soporte específicos proporcionados para los servidores de aplicaciones individuales.

Se describen los pasos de instalación de los siguientes servidores de aplicaciones:

* [WebSphere 8.5](#websphere)
* [JBoss EAP 6.3.0/6.4.0](#jboss-eap)
* [Oracle WebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

Consulte la documentación apropiada del servidor de aplicaciones para obtener más información sobre la instalación de aplicaciones web, configuraciones de servidor y cómo iniciar y detener el servidor.

>[!NOTE]
>
>Si utiliza Dynamic Media en una implementación WAR, consulte la [documentación de Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

## Descripción general {#general-description}

### Comportamiento predeterminado al instalar AEM en un servidor de aplicaciones {#default-behaviour-when-installing-aem-in-an-application-server}

AEM se presenta como un único archivo de guerra que se va a desplegar.

Si se implementa, sucederá lo siguiente de forma predeterminada:

* el modo de ejecución es `author`
* la instancia (Repositorio, entorno Felix OSGI, paquetes, etc.) se instala en `${user.dir}/crx-quickstart`donde `${user.dir}` es el directorio de trabajo actual, esta ruta a crx-quickstart se llama `sling.home`

* la raíz del contexto es el nombre del archivo war, por ejemplo: `aem-6`

#### Configuración {#configuration}

Puede cambiar el comportamiento predeterminado de la siguiente manera:

* modo de ejecución : configure el parámetro `sling.run.modes` en el archivo `WEB-INF/web.xml` del archivo war de AEM antes de la implementación

* sling.home: configure el parámetro `sling.home` en el archivo `WEB-INF/web.xml`del archivo war de AEM antes de la implementación

* raíz de contexto: cambiar el nombre del archivo de guerra de AEM

#### Publicar instalación {#publish-installation}

Para implementar una instancia de publicación, debe establecer el modo de ejecución para publicar:

* Desempaquete el WEB-INF/web.xml del archivo de guerra de AEM
* Cambiar el parámetro sling.run.modes a publicar
* Reempaquete el archivo web.xml en AEM archivo war
* Implementar AEM archivo war

#### Comprobación de instalación {#installation-check}

Para comprobar si todo está instalado, puede:

* siga el archivo `error.log`para ver que todo el contenido está instalado
* compruebe en `/system/console` que todos los paquetes están instalados

#### Dos instancias en el mismo servidor de aplicaciones {#two-instances-on-the-same-application-server}

Para fines de demostración, puede ser apropiado instalar la instancia de autor y publicación en un servidor de aplicaciones. Para ello, haga lo siguiente:

1. Cambie las variables sling.home y sling.run.modes de la instancia de publicación.
1. Desempaquete el archivo WEB-INF/web.xml del archivo war AEM.
1. Cambie el parámetro sling.home a una ruta diferente (las rutas absolutas y relativas son posibles).
1. Cambie sling.run.modes para publicar para la instancia de publicación.
1. Vuelva a empaquetar el archivo web.xml.
1. Cambie el nombre de los archivos de guerra, de modo que tengan nombres diferentes: Por ejemplo, un nombre a aemauthor.war y otro a aempublish.war.
1. Utilizar configuraciones de memoria más altas, por ejemplo, para instancias de AEM predeterminadas, usar, por ejemplo: -Xmx3072m
1. Implemente las dos aplicaciones web.
1. Después de la implementación, detenga las dos aplicaciones web.
1. Tanto en la instancia de autor como en la de publicación, se asegura de que en los archivos sling.properties la propiedad felix.service.urlhandlers=false se establezca en false (de forma predeterminada se establece en true).
1. Vuelva a iniciar las dos aplicaciones web.

## Procedimientos de instalación de los servidores de aplicaciones {#application-servers-installation-procedures}

### WebSphere 8.5 {#websphere}

Antes de una implementación, lea la [Descripción general](#general-description) anterior.

**Preparación del servidor**

* Permita que pasen los encabezados de autenticación básicos:

   * Una forma de permitir que AEM autenticar a un usuario es deshabilitar la seguridad administrativa global del servidor WebSphere, para hacerlo: vaya a Seguridad -> Seguridad global y desmarque la casilla Activar seguridad administrativa , guarde y reinicie el servidor.

* set `"JAVA_OPTS= -Xmx2048m"`
* Si desea instalar AEM usando context root = / entonces primero debe cambiar la raíz de contexto de la aplicación web predeterminada existente

**Implementación AEM aplicación web**

* Descargar AEM archivo de guerra
* Realice sus configuraciones en web.xml si es necesario (consulte más arriba en la Descripción general)

   * Desempaquete WEB-INF/web.xml archivo
   * cambiar el parámetro sling.run.modes a publicar
   * quite el comentario del parámetro inicial sling.home y establezca esta ruta como sea necesario
   * Volver a empaquetar el archivo web.xml

* Implementar AEM archivo war

   * Elija una raíz de contexto (si desea establecer los modos de ejecución de Sling, debe seleccionar los pasos detallados del asistente de implementación y, a continuación, especificarlos en el paso 6 del asistente)

* Iniciar AEM aplicación web

#### JBoss EAP 6.3.0/6.4.0 {#jboss-eap}

Antes de una implementación, lea la [Descripción general](#general-description) anterior.

**Preparación del servidor JBoss**

Establezca los argumentos de memoria en el archivo conf (por ejemplo, `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

si utiliza el analizador de implementación para para instalar la aplicación web AEM, puede que sea bueno aumentar el `deployment-timeout,` para ese conjunto en un atributo `deployment-timeout` en el archivo xml de su instancia (por ejemplo, `configuration/standalone.xml)`:

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**Implementación AEM aplicación web**

* Cargue la aplicación web AEM en la consola de administración de JBoss.

* Active la aplicación web AEM.

#### Oracle WebLogic 12.1.3/12.2 {#oracle-weblogic}

Antes de una implementación, lea la [Descripción general](#general-description) anterior.

Utiliza un diseño de servidor simple con solo un servidor de administración.

**Preparación del servidor WebLogic**

* En `${myDomain}/config/config.xml`agregue a la sección de configuración de seguridad:

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` consulte en  [https://xmlns.oracle.com/weblogic/domain/1.0/domain.](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) xsdpara saber cuál es la posición correcta (de forma predeterminada, para colocarla al final de la sección es correcto)

* Aumente la configuración de memoria de VM:

   * abra `${myDomain}/bin/setDomainEnv.cmd` (resp.sh)busque WLS_MEM_ARGS, establezca, por ejemplo, `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * reiniciar servidor WebLogic

* Cree en `${myDomain}` una carpeta de paquetes y dentro de una carpeta cq y en ella una carpeta Plan

**Implementación AEM aplicación web**

* Descargar AEM archivo de guerra
* Coloque el archivo de guerra AEM en la carpeta ${myDomain}/packages/cq
* Realice las configuraciones en `WEB-INF/web.xml` si es necesario (consulte más arriba en la Descripción general)

   * Desempaquete `WEB-INF/web.xml`archivo
   * cambiar el parámetro sling.run.modes a publicar
   * quite el comentario del parámetro inicial sling.home y establezca esta ruta como sea necesario (consulte Descripción general)
   * Volver a empaquetar el archivo web.xml

* Implementar AEM archivo war como una aplicación (para el resto de configuraciones, utilice la configuración predeterminada)
* La instalación puede llevar tiempo...
* Compruebe que la instalación ha finalizado como se mencionó anteriormente en la Descripción general (por ejemplo, al seguir el archivo error.log)
* Puede cambiar la raíz de contexto en la pestaña Configuración de la aplicación web en WebLogic `/console`

#### Tomcat 8/8.5 {#tomcat}

Antes de una implementación, lea la [Descripción general](#general-description) anterior.

* **Preparar el servidor Tomcat**

   * Aumente la configuración de memoria de VM:

      * En `bin/catalina.bat` (resp `catalina.sh` en unix) agregue la siguiente configuración:
      * `set "JAVA_OPTS= -Xmx2048m`
   * Tomcat no permite acceso de administrador ni de administrador en la instalación. Por lo tanto, debe editar manualmente `tomcat-users.xml` para permitir el acceso para estas cuentas:

      * Edite `tomcat-users.xml` para incluir el acceso para el administrador y el administrador. La configuración debe ser similar al siguiente ejemplo:

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

      * Detener y cancelar la implementación de la aplicación web ROOT
      * Cambie el nombre de la carpeta ROOT.war en la carpeta webapps de tomcat.
      * Inicie webapp de nuevo
   * Si instala la aplicación web AEM utilizando el administrador-gui, debe aumentar el tamaño máximo de un archivo cargado, ya que el tamaño predeterminado solo permite un tamaño de carga de 50 MB. Para que se abra el web.xml de la aplicación web del administrador,

      `webapps/manager/WEB-INF/web.xml`

      y aumente el tamaño máximo del archivo y el tamaño máximo de la solicitud a al menos 500 MB, consulte el siguiente `multipart-config` ejemplo de un archivo `web.xml` de este tipo.

      ```xml
      <multipart-config>
      <!-- 500MB max -->
      <max-file-size>524288000</max-file-size>
      <max-request-size>524288000</max-request-size>
      <file-size-threshold>0</file-size-threshold>
      </multipart-config>
      ```




* **Implementación AEM aplicación web**

   * Descargar AEM archivo de guerra
   * Realice sus configuraciones en web.xml si es necesario (consulte más arriba en la Descripción general)

      * Desempaquete WEB-INF/web.xml archivo
      * cambiar el parámetro sling.run.modes a publicar
      * quite el comentario del parámetro inicial sling.home y establezca esta ruta como sea necesario
      * Volver a empaquetar el archivo web.xml
   * Cambie el nombre AEM archivo war a ROOT.war si desea implementarlo como webapp raíz, cámbielo por ejemplo aemauthor.war si desea tener aemauthor como raíz de contexto
   * cópielo en la carpeta webapps de tomcat.
   * espera hasta que AEM esté instalado


## Solución de problemas {#troubleshooting}

Para obtener información sobre cómo tratar los problemas que pueden surgir durante la instalación, consulte:

* [Solución de problemas](/help/sites-deploying/troubleshooting.md)
