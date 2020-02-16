---
title: Límites de contribución de miembros
seo-title: Límites de contribución de miembros
description: La función de límites de contribución permite limitar las contribuciones para protegerlas contra el spam
seo-description: La función de límites de contribución permite limitar las contribuciones para protegerlas contra el spam
uuid: 99b2a855-3f0d-41a0-9572-517a7f29af9f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d855aac2-f34d-402f-9dc3-c7ad494b45f2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Límites de contribución de miembros {#member-contribution-limits}

## Información general {#overview}

La función de límites de contribución permite limitar las contribuciones de los miembros de la comunidad como medio de protección contra el spam.

Cuando un miembro está limitado, cualquier anuncio que supere el número permitido de contribuciones generará una alerta de que se excedió el límite y se rechazó el anuncio. A continuación, el miembro de la comunidad puede dirigirse al centro de mensajes de la comunidad y ponerse en contacto con un administrador de la comunidad que puede eliminar los límites si es necesario.

Los límites de contribución pueden habilitarse individualmente desde la consola [](members.md) Miembros y/o configurarse para habilitarse automáticamente cuando los visitantes del sitio se conviertan en nuevos miembros.

Con la consola Miembros, un administrador de comunidad puede eliminar de forma proactiva los límites de contribución para un miembro en cualquier momento, o eliminarlos de forma reactiva cuando un miembro envía un mensaje a un administrador de comunidad que realiza una solicitud de este tipo.

## Configuración de límites de contribución de contenido generado por usuarios de AEM Communities {#aem-communities-user-generated-content-contribution-limits-configuration}

Esta configuración OSGi

* Define las características de los límites de contribución (número de puestos dentro de un período de tiempo)
* Identifica a quién puede enviar un mensaje el miembro cuando se alcance el límite
* Identifica los dominios que nunca deben restringirse

Para alcanzar esta configuración OSGi:

* En el editor principal
* Iniciar sesión con privilegios de administrador
* Acceso a la consola [web](../../help/sites-deploying/configuring-osgi.md)

   * Por ejemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Localizar `AEM Communities User Generated Content Contribution Limits Configuration`
* Seleccione el icono de edición

![chlimage_1-127](assets/chlimage_1-127.png)

* **[!UICONTROL Aplicar automáticamente límites de contribución UGC]**

   Si se selecciona, establezca automáticamente límites de contribución para los usuarios cuando se registren como miembros de la comunidad. Esto se refleja en el perfil del miembro de la comunidad y puede habilitarse o deshabilitarse desde la consola [de](members.md)miembros. Los nuevos miembros con una dirección de correo electrónico de un dominio de la lista blanca nunca se restringen.

   El valor predeterminado no está marcado.

* **[!UICONTROL Límite UGC]**

   Número máximo de contribuciones.

   El valor predeterminado es 10 publicaciones.

* **[!UICONTROL Frecuencia límite de UGC]**

   Período de tiempo que restringe el límite UGC.

   El valor predeterminado es de 60 minutos.

* **[!UICONTROL Dominios]**

   Lista blanca de uno o varios dominios de correo electrónico. Seleccione el icono + para realizar entradas adicionales.

   Los usuarios con direcciones de correo electrónico en los dominios de la lista blanca no se ven afectados cuando se aplican automáticamente los límites de contribución UGC. Por ejemplo, si `mycompany.com` se agrega un dominio a la lista de dominios, nunca se restringirá la publicación de un miembro con dirección de correo electrónico `me@mycompany.com` .

   El valor predeterminado es una lista blanca vacía.

* **[!UICONTROL Destinatarios de mensajería]**

   Lista de uno o varios ID autorizados de miembros que pueden modificar los límites de contribución de los miembros. Seleccione el icono + para realizar entradas adicionales.

   Los Miembros sólo podrán ponerse en contacto con miembros especificados cuando se haya alcanzado su límite.

   El valor predeterminado no es ningún destinatario de mensajería.

Nota: La configuración predeterminada da como resultado un límite de 10 publicaciones en un período de una hora.
