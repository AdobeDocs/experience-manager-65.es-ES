---
title: Optimización de formularios HTML5
seo-title: Optimización de formularios HTML5
description: Puede optimizar el tamaño de salida de los formularios HTML5.
seo-description: Puede optimizar el tamaño de salida de los formularios HTML5.
uuid: 959f0b6a-9e4d-478a-afa8-4c39011fdf7a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdb9edc2-6a37-4d3f-97d5-0fc5664316be
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Optimización de formularios HTML5 {#optimizing-html-forms}

Los formularios HTML5 se procesan en formato HTML5. El resultado podría ser grande según factores como el tamaño del formulario y las imágenes del formulario. Para optimizar la transferencia de datos, el método recomendado es comprimir la respuesta HTML mediante el servidor web desde el que se está enviando la solicitud. Este método reduce el tamaño de respuesta, el tráfico de red y el tiempo necesario para transmitir datos entre el servidor y los equipos cliente.

Este artículo describe los pasos necesarios para habilitar la compresión para Apache Web Server 2.0 de 32 bits, con JBoss.

*Nota: Las siguientes instrucciones no se aplican a servidores que no sean Apache Web Server 2.0 de 32 bits.*

Obtenga el software de servidor web Apache aplicable a su sistema operativo:

* Para Windows, descargue el servidor web Apache del sitio del proyecto Apache HTTP Server.
* Para Solaris de 64 bits, descargue el servidor web Apache del sitio web de Sunfreeware para Solaris.
* Para Linux, el servidor web Apache está preinstalado en un sistema Linux.

Apache puede comunicarse con JBoss mediante HTTP o el protocolo AJP.

1. Quite los comentarios de las siguientes configuraciones de módulo en el archivo *APACHE_HOME/conf/httpd.conf* .

   ```java
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >Para Linux, el directorio APACHE_HOME predeterminado es /etc/httpd/.

1. Configure el proxy en el puerto 8080 de JBoss.

   Agregue la siguiente configuración al archivo de configuración *APACHE_HOME/conf/httpd.conf* .

   ```java
   ProxyPass / https://<server_Name>:8080/
   ProxyPassReverse / https://<server_Name>:8080/
   ```

   >[!NOTE]
   >
   >Cuando se utiliza un proxy, se requieren los siguientes cambios de configuración:
   >
   >* Acceso: *https://&lt;servidor>:&lt;puerto>/system/console/configMgr*
   * Editar la configuración del filtro de referente de Sling de Apache
   * En Permitir hosts, agregue la entrada para el servidor proxy


1. Habilite Compresión.

   Agregue la siguiente configuración al archivo de configuración *APACHE_HOME/conf/httpd.conf* .

   ```java
   <Location /content/xfaforms>
     <IfModule mod_deflate.c>
        SetOutputFilter DEFLATE
        # Don’t compress
        SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
        SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
       #Dealing with proxy servers
   
        <IfModule mod_headers.c>
           Header append Vary User-Agent
        </IfModule>
     </IfModule>
   </Location>
   ```

1. Para acceder al servidor AEM, utilice https://[Apache_server]:80.

**[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)**
