---
title: Ajuste del rendimiento del servidor de AEM Forms
seo-title: Ajuste del rendimiento del servidor de AEM Forms
description: Para que AEM Forms funcione de forma óptima, puede ajustar la configuración de caché y los parámetros JVM. Además, el uso de un servidor web puede mejorar el rendimiento de la implementación de AEM Forms.
seo-description: Para que AEM Forms funcione de forma óptima, puede ajustar la configuración de caché y los parámetros JVM. Además, el uso de un servidor web puede mejorar el rendimiento de la implementación de AEM Forms.
uuid: bf23b62c-7559-4726-8f4e-cc8b1457e501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 38c0ec46-5686-4656-bfb4-7125ec194673
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Ajuste del rendimiento del servidor de AEM Forms{#performance-tuning-of-aem-forms-server}

En este artículo se analizan las estrategias y prácticas recomendadas que puede implementar para reducir los cuellos de botella y optimizar el rendimiento de la implementación de AEM Forms.

## Ajustes de caché {#cache-settings}

Puede configurar y controlar la estrategia de almacenamiento en caché para AEM Forms mediante el componente Configuración **de formularios** móviles en la consola de configuración web de AEM en:

* (AEM Forms en OSGi) `https://'[server]:[port]'/system/console/configMgr`
* (AEM Forms on JEE) `https://'[server]:[port]'/lc/system/console/configMgr`

Las opciones disponibles para el almacenamiento en caché son las siguientes:

* **Ninguno**: Fuerza que no almacene en caché ningún artefacto. En la práctica, esto ralentiza el rendimiento y requiere una alta disponibilidad de memoria debido a la ausencia de memoria caché.
* **Conservador**: Dicta para almacenar en caché solo los artefactos intermedios que se generan antes de procesar el formulario, como una plantilla que contiene fragmentos en línea e imágenes.
* **Agresivo**: Refuerza la caché de casi todo lo que se puede almacenar en caché, incluido el contenido HTML procesado, además de todos los artefactos del nivel de almacenamiento en caché conservador. Da como resultado el mejor rendimiento, pero también consume más memoria para almacenar artefactos en caché. Una estrategia de almacenamiento en caché agresiva significa que obtendrá un rendimiento de tiempo constante al procesar un formulario a medida que el contenido procesado se almacena en caché.

Es posible que la configuración de caché predeterminada para AEM Forms no sea lo suficientemente buena como para lograr un rendimiento óptimo. Por lo tanto, se recomienda utilizar la siguiente configuración:

* **Estrategia** de caché: Agresivo
* **Tamaño** de caché (en términos de número de formularios): Como requerido
* **Tamaño** máximo del objeto: Como requerido

![Configuraciones de formularios móviles](assets/snap.png)

>[!NOTE]
>
>Si utiliza AEM Dispatcher para almacenar en caché formularios adaptables, también almacena en caché formularios adaptables que contienen formularios con datos precargados. Si estos formularios se proporcionan desde la caché de AEM Dispatcher, es posible que sirvan datos precargados o antiguos para los usuarios. Por lo tanto, utilice AEM Dispatcher para almacenar en caché formularios adaptables que no utilicen datos precargados. Además, una caché de despachantes no invalida automáticamente los fragmentos en caché. Por lo tanto, no lo utilice para almacenar en caché fragmentos de formulario. Para estos formularios y fragmentos, utilice la caché [de formularios](../../forms/using/configure-adaptive-forms-cache.md)adaptables.

## Parámetros de JVM {#jvm-parameters}

Para obtener un rendimiento óptimo, se recomienda utilizar los siguientes argumentos JVM `init` para configurar el `Java heap` y `PermGen`.

```java
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xms8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xmx8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:PermSize=256m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:MaxPermSize=1024m
```

**Nota**: Los ajustes recomendados son para Windows 2008 R2 8 Core y JDK de Oracle HotSpot 1.7 (64 bits) y deben ampliarse o reducirse según la configuración del sistema.

## Uso de un servidor web {#using-a-web-server}

Los formularios adaptables y HTML5 se representan en formato HTML5. El resultado podría ser grande según factores como el tamaño del formulario y las imágenes del formulario. Para optimizar la transferencia de datos, el método recomendado es comprimir la respuesta HTML utilizando el servidor web desde el que se está enviando la solicitud. Este método reduce el tamaño de respuesta, el tráfico de red y el tiempo necesario para transmitir datos entre servidores y equipos cliente.

Por ejemplo, realice los siguientes pasos para habilitar la compresión en Apache Web Server 2.0 de 32 bits con JBoss:

***Nota **: Las siguientes instrucciones no se aplican a ningún servidor que no sea Apache Web Server 2.0 de 32 bits. Para ver los pasos específicos de cualquier otro servidor, consulte la documentación del producto correspondiente.*

Los siguientes pasos muestran los cambios necesarios para habilitar la compresión con Apache Web Server

**Obtenga el software de servidor web Apache aplicable a su sistema operativo**

* Windows: descargue el servidor web Apache del sitio del proyecto Apache HTTP Server.
* Solaris de 64 bits: descargue el servidor web Apache del sitio web de Sunfreeware para Solaris.
* Linux: el servidor web Apache está preinstalado en un sistema Linux.

Apache puede comunicarse con CRX mediante el protocolo HTTP. Las configuraciones son para optimización mediante HTTP.

1. Quite los comentarios de las siguientes configuraciones de módulo en el `APACHE_HOME/conf/httpd.conf` archivo.

   ```java
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >Para Linux, el valor predeterminado `APACHE_HOME` es `/etc/httpd/`.

1. Configure el proxy en el puerto 4502 de crx.
Añada la siguiente configuración en el archivo `APACHE_HOME/conf/httpd.conf` de configuración.

   ```java
   ProxyPass / https://<server>:4502/
   ProxyPassReverse / https://<server>:4502/
   ```

1. Habilite Compresión. Añada la siguiente configuración en el archivo `APACHE_HOME/conf/httpd.conf` de configuración.

   **Para formularios HTML5**

   ```java
   <Location /content/xfaforms>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Don’t compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   **Para formularios adaptables**

   ```java
   <Location /content/forms/af>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Don’t compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   Para acceder al servidor crx, utilice `https://'server':80`, donde `server` es el nombre del servidor en el que se ejecuta el servidor Apache.

## Uso de un antivirus en un servidor que ejecuta AEM Forms {#using-an-antivirus-on-server-running-aem-forms}

Puede experimentar un rendimiento lento en los servidores que ejecutan un software antivirus. Un software antivirus (análisis en tiempo real) siempre analiza todos los archivos de un sistema. Puede ralentizar el servidor y afectar al rendimiento de AEM Forms.

Para mejorar el rendimiento, puede ordenar al software antivirus que excluya los siguientes archivos y carpetas de AEM Forms del análisis siempre activo (en tiempo real):

* Directorio de instalación de AEM. Si no es posible excluir el directorio completo, excluya lo siguiente:

   * [Directorio]de instalación de AEM \crx-repository\temp
   * [Directorio]de instalación de AEM \crx-repository\repository
   * [Directorio]de instalación de AEM \crx-repository\launchpad

* Directorio temporal del servidor de aplicaciones. La ubicación predeterminada es:

   * (Jleader) Directorio de instalación de [AEM]\jboss\standalone\tmp
   * (Weblogic) \Oracle\Middleware\user_projects\domains\LCDomain\servers\LCServer1\tmp
   * (Websphere) \Programa Files\IBM\WebSphere\AppServer\profiles\AppSrv01\temp

* **(Solo AEM Forms en JEE)** Directorio de Almacenamiento de Documento global (GDS). La ubicación predeterminada es:

   * (JBoss) [appserver raíz]/server/&#39;server&#39;/svcnative/DocumentStorage
   * (WebLogic) [appserverdomain]/&#39;server&#39;/adobe/LiveCycleServer/DocumentStorage
   * (WebSphere) [appserver raíz]/installApps/adobe/&#39;server&#39;/DocumentStorage

* **(Solo AEM Forms en JEE)** Registros de servidor y directorio temporal de AEM Forms. La ubicación predeterminada es:

   * Registros de servidor: directorio [de instalación de AEM Forms]\Adobe\AEM forms\[app-server]\server\all\logs
   * Directorio temporal - Directorio [de instalación de]AEM Forms\temp

>[!NOTE]
>
>* Si está utilizando una ubicación diferente para GDS y un directorio temporal, abra AdminUI en `https://'[server]:[port]'/adminui`, vaya a **Inicio > Configuración > Configuración del sistema principal > Configuraciones** principales para confirmar la ubicación en uso.

* Si el servidor de AEM Forms funciona lentamente incluso después de excluir los directorios sugeridos, excluya también el archivo ejecutable Java (java.exe).



