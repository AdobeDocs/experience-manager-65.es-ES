---
title: Instalación del servidor de aplicaciones
description: Obtenga información sobre cómo instalar Adobe Experience Manager con un servidor de aplicaciones.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 3a90f1d2-e53f-4cc4-8122-024ad6500de0
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 0%

---

# Instalación del servidor de aplicaciones{#application-server-install}

>[!NOTE]
>
>`JAR` y `WAR` son los tipos de archivo en los que se lanza Adobe Experience Manager AEM (). Se está garantizando la calidad de estos formatos para ajustarse a los niveles de soporte que el Adobe se ha comprometido a alcanzar.
>

Esta sección le explica cómo instalar Adobe Experience Manager AEM () con un servidor de aplicaciones. Consulte la [Plataformas compatibles](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) para obtener información sobre los niveles de soporte específicos proporcionados para los servidores de aplicaciones individuales.

Se describen los pasos de instalación de los siguientes servidores de aplicaciones:

* [WebSphere](#websphere)
* [JBoss](#jboss-eap)
* [Oracle WebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

Consulte la documentación adecuada del servidor de aplicaciones para obtener más información sobre la instalación de aplicaciones web, las configuraciones de servidor y cómo iniciar y detener el servidor.

>[!NOTE]
>
>Si utiliza Dynamic Media en una implementación WAR, consulte [Documentación de Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

## Descripción general {#general-description}

### AEM Comportamiento predeterminado al instalar el servidor de aplicaciones en un servidor de aplicaciones {#default-behaviour-when-installing-aem-in-an-application-server}

AEM Se trata de un único archivo de guerra que se va a implementar.

Si se implementa, lo siguiente ocurre de forma predeterminada:

* el modo de ejecución es `author`
* la instancia (Repositorio, entorno Felix OSGI, paquetes, etc.) está instalada en `${user.dir}/crx-quickstart`donde `${user.dir}` es el directorio de trabajo actual, se llama a esta ruta de acceso a crx-quickstart `sling.home`

* la raíz de contexto es el nombre del archivo war, por ejemplo,  `aem-6`

#### Configuración {#configuration}

Puede cambiar el comportamiento predeterminado de la siguiente manera:

* modo de ejecución : configure el `sling.run.modes` en el campo `WEB-INF/web.xml` AEM archivo del archivo de guerra de la antes de la implementación

* sling.home: configure el `sling.home` en el campo `WEB-INF/web.xml`AEM archivo del archivo de guerra de la antes de la implementación

* AEM raíz de contexto: cambie el nombre del archivo de guerra de la

#### Instalación de publicación {#publish-installation}

Para implementar una instancia de publicación, debe establecer el modo de ejecución en Publish:

* AEM Desempaquetar WEB-INF/web.xml del archivo de guerra de la
* Cambie el parámetro sling.run.modes a publish
* AEM Vuelva a empaquetar el archivo web.xml en el archivo WAR de la
* AEM Implementar archivo de guerra de

#### Comprobación de instalación {#installation-check}

Para comprobar si todo está instalado, puede:

* siga el `error.log`para ver que todo el contenido está instalado
* buscar en `/system/console` que todos los paquetes están instalados

#### Dos instancias en el mismo servidor de aplicaciones {#two-instances-on-the-same-application-server}

Para fines de demostración, puede ser adecuado instalar la instancia de autor y publicación en un servidor de aplicaciones. Para ello, haga lo siguiente:

1. Cambie las variables sling.home y sling.run.modes de la instancia de publicación.
1. AEM Desempaquete el archivo WEB-INF/web.xml del archivo de guerra de la.
1. Cambie el parámetro sling.home a una ruta diferente (es posible usar rutas absolutas y relativas).
1. Cambie sling.run.modes a publish para la instancia de publicación.
1. Vuelva a empaquetar el archivo web.xml.
1. Cambie el nombre de los archivos WAR para que tengan nombres diferentes. Por ejemplo, un nombre para aemauthor.war y el otro para aempublish.war.
1. Utilice una configuración de memoria más alta. AEM Por ejemplo, las instancias de predeterminadas utilizan `-Xmx3072m`
1. Implemente las dos aplicaciones web.
1. Después de la implementación, detenga las dos aplicaciones web.
1. Tanto en las instancias de autor como en las de publicación, asegúrese de que la propiedad felix.service.urlhandlers=false de los archivos sling.properties esté establecida en false (el valor predeterminado es que esté establecida en true).
1. Vuelva a iniciar las dos aplicaciones web.

## Procedimientos de instalación de Application Servers {#application-servers-installation-procedures}

### WebSphere® 8.5 {#websphere}

Antes de una implementación, lea la [Descripción general](#general-description) arriba.

**Preparación del servidor**

* Permita que los encabezados de autenticación básicos pasen:

   * AEM Una forma de permitir que los usuarios se autentiquen es desactivar la seguridad administrativa global del servidor WebSphere®, para ello: vaya a Seguridad > Seguridad global y desmarque la casilla de verificación Habilitar seguridad administrativa, guarde y reinicie el servidor.

* set `"JAVA_OPTS= -Xmx2048m"`
* AEM Si desea realizar la instalación utilizando la raíz de contexto = /, cambie la raíz de contexto de la aplicación web predeterminada existente.

**AEM Implementación de aplicación web**

* AEM Descarga de archivo de guerra de
* Realice las configuraciones en web.xml si es necesario (consulte la descripción general anterior)

   * Desempaquetar archivo WEB-INF/web.xml
   * cambie el parámetro sling.run.modes a publish
   * elimine los comentarios del parámetro inicial sling.home y establezca esta ruta como necesite
   * Reempaquetar archivo web.xml

* AEM Implementar archivo de guerra de

   * Elija una raíz de contexto (si desea definir los modos de ejecución de sling, debe seleccionar los pasos detallados del asistente de implementación y, a continuación, especificarlo en el paso 6 del asistente)

* AEM Iniciar aplicación web

#### JBoss® EAP 6.3.0/6.4.0 {#jboss-eap}

Antes de una implementación, lea la [Descripción general](#general-description) arriba.

**Preparar el servidor JBoss®**

Establezca los argumentos de memoria en su archivo conf (por ejemplo, `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

AEM Si utiliza el analizador de implementación para instalar la aplicación web de la aplicación web de la aplicación, puede que sea recomendable aumentar el valor de `deployment-timeout,` para ese conjunto a `deployment-timeout` en el archivo xml de su instancia (por ejemplo, `configuration/standalone.xml)`:

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**AEM Implementación de aplicación web**

* AEM Cargue la aplicación web de en la consola de administración ® JBoss.

* AEM Habilite la aplicación web de.

#### Oracle WebLogic 12.1.3/12.2 {#oracle-weblogic}

Antes de una implementación, lea la [Descripción general](#general-description) arriba.

Utiliza un diseño de servidor simple con solo un servidor de administración.

**Preparación de WebLogic Server**

* Entrada `${myDomain}/config/config.xml`agregue a la sección de configuración de seguridad:

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` ver en [https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) para la posición correcta (de forma predeterminada, colocarlo al final de la sección es correcto)

* Aumentar configuración de memoria de VM:

   * open `${myDomain}/bin/setDomainEnv.cmd` (resp .sh) busque WLS_MEM_ARGS, por ejemplo, set `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * reiniciar WebLogic Server

* Crear en `${myDomain}` una carpeta de paquetes y dentro de una carpeta cq y en ella una carpeta de plan

**AEM Implementación de aplicación web**

* AEM Descarga de archivo de guerra de
* AEM Poner el archivo de guerra de la en ${myDomain}carpeta /packages/cq
* Realice las configuraciones en `WEB-INF/web.xml` si es necesario (consulte más arriba en la Descripción general)

   * Desempaquetar `WEB-INF/web.xml`archivo
   * cambie el parámetro sling.run.modes a publish
   * Elimine los comentarios del parámetro inicial sling.home y establezca esta ruta según sea necesario (consulte la Descripción general).
   * Reempaquetar archivo web.xml

* AEM Implementar archivo de guerra de la aplicación (para el resto de configuraciones, utilice la configuración predeterminada)
* La instalación puede tardar un poco...
* Compruebe que la instalación ha finalizado como se menciona arriba en la Descripción general (por ejemplo, siguiendo el error.log)
* Puede cambiar la raíz de contexto en la pestaña Configuration de la aplicación web en WebLogic `/console`

#### Tomcat 8/8.5 {#tomcat}

Antes de una implementación, lea la [Descripción general](#general-description) arriba.

* **Preparar el servidor Tomcat**

   * Aumente la configuración de memoria de VM:

      * Entrada `bin/catalina.bat` (resp `catalina.sh` en UNIX®) agregue la siguiente configuración:
      * `set "JAVA_OPTS= -Xmx2048m`

   * Tomcat no permite el acceso de administrador o responsable durante la instalación. Por lo tanto, debe editarlo manualmente `tomcat-users.xml` para permitir el acceso a estas cuentas:

      * Editar `tomcat-users.xml` para incluir el acceso de administrador y responsable. La configuración debería ser similar al siguiente ejemplo:

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

   * AEM Si desea implementar la raíz de contexto con la raíz de contexto &quot;/&quot;, debe cambiar la raíz de contexto de la aplicación web ROOT existente:

      * Detener y anular la implementación de la aplicación web ROOT
      * Cambie el nombre de la carpeta ROOT.war en la carpeta webapps de tomcat
      * Iniciar aplicación web de nuevo

   * AEM Si instala la aplicación web de mediante la interfaz de usuario del administrador, deberá aumentar el tamaño máximo de un archivo cargado, ya que el tamaño predeterminado solo permite una carga de 50 MB. Para que abra el archivo web.xml de la aplicación web del administrador,

     `webapps/manager/WEB-INF/web.xml`

     y aumente el tamaño máximo de archivo y el tamaño máximo de solicitud a al menos 500 MB, consulte lo siguiente `multipart-config` ejemplo de un `web.xml` archivo.

     ```xml
     <multipart-config>
     <!-- 500MB max -->
     <max-file-size>524288000</max-file-size>
     <max-request-size>524288000</max-request-size>
     <file-size-threshold>0</file-size-threshold>
     </multipart-config>
     ```

* **AEM Implementación de aplicación web**

   * AEM Descarga de archivo de guerra de
   * Realice las configuraciones en web.xml si es necesario (consulte la descripción general anterior)

      * Desempaquetar archivo WEB-INF/web.xml
      * cambie el parámetro sling.run.modes a publish
      * elimine los comentarios del parámetro inicial sling.home y establezca esta ruta como necesite
      * Reempaquetar archivo web.xml

   * AEM Cambie el nombre del archivo de guerra a RAÍZ.war si desea implementarlo como aplicación web raíz, cambie el nombre a por ejemplo, aemauthor.war si desea tener aemauthor como raíz de contexto
   * cópielo en la carpeta de aplicaciones web de tomcat
   * AEM esperar hasta que se instale el

## Solución de problemas {#troubleshooting}

Para obtener información acerca de cómo solucionar los problemas que pueden producirse durante la instalación, consulte:

* [Solución de problemas](/help/sites-deploying/troubleshooting.md)
