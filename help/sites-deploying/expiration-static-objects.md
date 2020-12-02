---
title: Caducidad de objetos estáticos
seo-title: Caducidad de objetos estáticos
description: Obtenga información sobre cómo configurar AEM para que los objetos estáticos no caduquen (durante un período de tiempo razonable).
seo-description: Obtenga información sobre cómo configurar AEM para que los objetos estáticos no caduquen (durante un período de tiempo razonable).
uuid: ee019a3d-4133-4d40-98ec-e0914b751fb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 73f37b3c-5dbe-4132-bb60-daa8de871884
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---


# Caducidad de objetos estáticos{#expiration-of-static-objects}

Los objetos estáticos (por ejemplo, iconos) no cambian. Por lo tanto, el sistema debe configurarse de modo que no caduque (durante un período de tiempo razonable) y se reduzca así el tráfico innecesario.

Esto tiene el siguiente impacto:

* Descarga las solicitudes de la infraestructura del servidor.
* Aumenta el rendimiento de la carga de páginas, a medida que el explorador almacena en caché los objetos en la caché del explorador.

El estándar HTTP especifica las caducidad de los archivos (consulte, por ejemplo, el capítulo 14.21 de [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) &quot; Protocolo de transferencia de hipertexto — HTTP 1.1&quot;). Este estándar utiliza el encabezado para permitir que los clientes almacenen en caché los objetos hasta que se consideren antiguos; estos objetos se almacenan en caché durante el tiempo especificado sin que se realice ninguna comprobación de estado en el servidor de origen.

>[!NOTE]
>
>Esta configuración está completamente separada (y no funcionará para) el despachante.
>
>El propósito del despachante es almacenar en caché los datos delante de AEM.

Todos los archivos, que no son dinámicos y que no cambian con el tiempo, pueden y deben almacenarse en caché. La configuración del servidor Apache HTTPD podría tener el aspecto siguiente: según el entorno:

>[!CAUTION]
>
>Debe tener cuidado al definir el período de tiempo durante el cual un objeto se considera actualizado. Dado que *no hay comprobación hasta que el período de tiempo especificado haya caducado*, el cliente puede terminar presentando contenido antiguo de la caché.

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

   Esto permite que la caché intermedia (por ejemplo, la caché del navegador) almacene archivos CSS, Javascript, PNG y GIF durante un mes, hasta que caduquen. Esto significa que no es necesario solicitarlas a AEM o al servidor web, pero sí pueden permanecer en la caché del explorador.

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

   Esto permite que la caché intermedia (por ejemplo, la caché del navegador) almacene archivos CSS, Javascript, PNG y GIF durante un día como máximo en las memorias caché del cliente. Aunque este ejemplo ilustra la configuración global de todo lo que está por debajo de `/content` y `/etc/designs`, debe hacerlo más granular.

   Según la frecuencia con la que se actualice el sitio, también puede considerar la posibilidad de almacenar en caché páginas HTML. Un período de tiempo razonable sería de 1 hora:

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

Después de configurar los objetos estáticos, analice `request.log`, mientras selecciona las páginas que contienen dichos objetos, para confirmar que no se están realizando solicitudes (innecesarias) para los objetos estáticos.
