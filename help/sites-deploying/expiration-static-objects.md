---
title: Caducidad de objetos estáticos
seo-title: Caducidad de objetos estáticos
description: Aprenda a configurar AEM para que los objetos estáticos no caduquen (durante un período de tiempo razonable).
seo-description: Aprenda a configurar AEM para que los objetos estáticos no caduquen (durante un período de tiempo razonable).
uuid: ee019a3d-4133-4d40-98ec-e0914b751fb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 73f37b3c-5dbe-4132-bb60-daa8de871884
feature: Configuring
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---


# Caducidad de objetos estáticos{#expiration-of-static-objects}

Los objetos estáticos (por ejemplo, los iconos) no cambian. Por lo tanto, el sistema debe configurarse para que no caduque (durante un período de tiempo razonable) y reduzca así el tráfico innecesario.

Esto tiene el siguiente impacto:

* Descarga las solicitudes de la infraestructura del servidor.
* Aumenta el rendimiento de la carga de páginas, ya que el explorador almacena en caché los objetos en la caché del explorador.

El estándar HTTP especifica las caducidades con respecto a la &quot;caducidad&quot; de los archivos (consulte, por ejemplo, el capítulo 14.21 de [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) &quot; Protocolo de transferencia de hipertexto — HTTP 1.1&quot;). Este estándar utiliza el encabezado para permitir que los clientes almacenen en caché los objetos hasta que se consideren obsoletos; estos objetos se almacenan en caché durante el tiempo especificado sin que se realice ninguna comprobación de estado en el servidor de origen.

>[!NOTE]
>
>Esta configuración es completamente independiente (y no funcionará para) Dispatcher.
>
>El propósito de Dispatcher es almacenar en caché los datos delante de AEM.

Todos los archivos, que no son dinámicos y que no cambian con el tiempo, pueden y deben almacenarse en caché. La configuración del servidor HTTP de Apache podría parecerse a una de las siguientes: depende del entorno:

>[!CAUTION]
>
>Debe tener cuidado al definir el periodo de tiempo durante el cual un objeto se considera actualizado. Como no hay *comprobación hasta que el período de tiempo especificado ha caducado*, el cliente puede terminar presentando contenido antiguo desde la caché.

1. **Para una instancia de Autor:**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /libs>
     ExpiresByType text/css "access plus 1 month"
     ExpiresByType text/javascript "access plus 1 month"
     ExpiresByType image/png "access plus 1 month"
     ExpiresByType image/gif "access plus 1 month"
   </Location>
   ```

   Esto permite que la caché intermedia (por ejemplo, la caché del navegador) almacene archivos CSS, Javascript, PNG y GIF durante un mes hasta que caduquen. Esto significa que no es necesario solicitarlas a AEM o al servidor web, pero puede permanecer en la caché del explorador.

   Otras secciones del sitio no deben almacenarse en caché en una instancia de autor, ya que están sujetas a cambios en cualquier momento.

1. **Para una instancia de publicación:**

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

   Esto permite que la caché intermedia (por ejemplo, la caché del navegador) almacene archivos CSS, Javascript, PNG y GIF durante un día como máximo en las cachés del cliente. Aunque este ejemplo ilustra la configuración global de todo lo que está debajo de `/content` y `/etc/designs`, debe hacerlo más granular.

   Según la frecuencia con la que se actualice el sitio, también puede considerar la posibilidad de almacenar en caché las páginas HTML. Un período de tiempo razonable sería de 1 hora:

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

Después de configurar los objetos estáticos, analice `request.log`, mientras selecciona páginas que contienen dichos objetos, para confirmar que no se realizan solicitudes (innecesarias) para objetos estáticos.
