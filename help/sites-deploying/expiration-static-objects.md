---
title: Caducidad de objetos estáticos
description: Aprenda a configurar Adobe Experience Manager para que los objetos estáticos no caduquen (durante un período de tiempo razonable).
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: bfd5441c-19cc-4fa8-b597-b1221465f75d
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# Caducidad de objetos estáticos{#expiration-of-static-objects}

Los objetos estáticos (por ejemplo, los iconos) no cambian. Por lo tanto, el sistema debe configurarse para que no caduque (durante un periodo de tiempo razonable) y, por lo tanto, reducir el tráfico innecesario.

Esto tiene el siguiente impacto:

* Descarga solicitudes desde la infraestructura del servidor.
* Aumenta el rendimiento de la carga de páginas, ya que el explorador almacena en caché los objetos de la caché del explorador.

El estándar HTTP especifica las caducidades en relación con la &quot;caducidad&quot; de los archivos (por ejemplo, consulte el capítulo 14.21 de [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) &quot; Protocolo de transferencia de hipertexto — HTTP 1.1&quot;). Este estándar utiliza el encabezado para permitir a los clientes almacenar en caché los objetos hasta que se consideren obsoletos; dichos objetos se almacenan en caché durante el tiempo especificado sin que se realice ninguna comprobación de estado en el servidor de origen.

>[!NOTE]
>
>Esta configuración es independiente de Dispatcher (y no funcionará para).
>
>El propósito de Dispatcher es almacenar en caché los datos delante de Adobe Experience Manager AEM ().

Todos los archivos, que no son dinámicos y que no cambian con el tiempo, se pueden y deben almacenar en caché. La configuración del servidor HTTPD de Apache podría parecerse a una de las siguientes opciones, según el entorno:

>[!CAUTION]
>
>Tenga cuidado al definir el período de tiempo durante el cual se considera que un objeto está actualizado. Como hay *no se realizará ninguna comprobación hasta que haya transcurrido el período de tiempo especificado*, el cliente puede terminar presentando contenido antiguo desde la caché.

1. **Para una instancia de autor:**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /libs>
     ExpiresByType text/css "access plus 1 month"
     ExpiresByType text/javascript "access plus 1 month"
     ExpiresByType image/png "access plus 1 month"
     ExpiresByType image/gif "access plus 1 month"
   </Location>
   ```

   Esto permite que la caché intermedia (por ejemplo, la del explorador) almacene archivos CSS, JavaScript, PNG y GIF durante un máximo de un mes, hasta que caduquen. AEM Esto significa que no es necesario solicitarlas desde o desde el servidor web, pero pueden permanecer en la caché del explorador.

   Otras secciones del sitio no deben almacenarse en caché en una instancia de autor, ya que están sujetas a cambios en cualquier momento.

1. **Para una instancia de Publish:**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /content>
     ExpiresByType text/css "access plus 1 day"
     ExpiresByType text/javascript "access plus 1 day"
     ExpiresByType image/png "access plus 1 day"
     ExpiresByType image/gif "access plus 1 day"
   </Location>
   <Location /etc/designs>
     ExpiresByType text/css "access plus 1 day"
     ExpiresByType text/javascript "access plus 1 day"
     ExpiresByType image/png "access plus 1 day"
     ExpiresByType image/gif "access plus 1 day"
   </Location>
   ```

   Esto permite que la caché intermedia (por ejemplo, la caché del explorador) almacene archivos CSS, JavaScript, PNG y GIF durante un máximo de un día en las cachés de cliente. Aunque este ejemplo ilustra la configuración global de todo lo siguiente `/content` y `/etc/designs`, debe hacerlo más granular.

   Dependiendo de la frecuencia con la que se actualice el sitio, también puede considerar el almacenamiento en caché de las páginas del HTML. Un período de tiempo razonable sería de una hora:

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

Una vez configurados los objetos estáticos, realice el análisis `request.log`, al seleccionar páginas que contienen estos objetos, para confirmar que no se realizan solicitudes (innecesarias) para objetos estáticos.
