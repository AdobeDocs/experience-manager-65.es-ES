---
title: Límites de contribución de miembros
seo-title: Límites de contribución de miembros
description: La función límites de contribución permite limitar las contribuciones para protegerlas contra el spam
seo-description: La función límites de contribución permite limitar las contribuciones para protegerlas contra el spam
uuid: 99b2a855-3f0d-41a0-9572-517a7f29af9f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d855aac2-f34d-402f-9dc3-c7ad494b45f2
role: Admin
exl-id: d00a8eb2-47ce-425a-a312-f043f82912be
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Límites de contribución de miembros {#member-contribution-limits}

## Información general {#overview}

La función límites de contribución permite limitar las contribuciones de los miembros de la comunidad como medio de protección contra el spam.

Cuando un miembro está limitado, cualquier publicación que supere el número permitido de contribuciones provocará una alerta de que se superó el límite y se rechazó el anuncio. A continuación, el miembro de la comunidad puede ir al centro de mensajes de la comunidad y ponerse en contacto con un administrador de la comunidad que puede eliminar los límites si procede.

Los límites de contribución pueden habilitarse individualmente desde la [consola de miembros](members.md) o configurarse para habilitarse automáticamente cuando los visitantes del sitio se conviertan en nuevos miembros.

Mediante la consola Miembros, un administrador de la comunidad puede eliminar de forma proactiva los límites de contribución de un miembro en cualquier momento, o eliminarlos de forma reactiva cuando un miembro envía un mensaje a un administrador de la comunidad que realiza una solicitud de este tipo.

## Configuración de límites de contribución de contenido generados por el usuario de AEM Communities {#aem-communities-user-generated-content-contribution-limits-configuration}

Esta configuración OSGi:

* Define las características de los límites de contribución (número de puestos dentro de un período de tiempo).
* Identifica a quién puede enviar un mensaje el miembro cuando se alcance el límite.
* Identifica los dominios que nunca deben restringirse.

Para llegar a esta configuración de OSGi:

* En el editor principal:
* Inicie sesión con privilegios de administrador.
* Acceda a la [Consola Web](../../help/sites-deploying/configuring-osgi.md).

   * Por ejemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Busque `AEM Communities User Generated Content Contribution Limits Configuration`.
* Seleccione el icono de edición.

![configure-limits](assets/configure-limits.png)

* **[!UICONTROL Aplicar automáticamente límites de contribución de UGC]**

   Si está marcada esta opción, establezca automáticamente límites de contribución para los usuarios cuando se registren como miembros de la comunidad. Esto se refleja en el perfil del miembro de la comunidad y se puede habilitar/deshabilitar desde la [consola de miembros](members.md). Los nuevos miembros con una dirección de correo electrónico de una lista de permitidos de dominios nunca se ven limitados.

   El valor predeterminado no está seleccionado.

* **[!UICONTROL Límite UGC]**

   Número máximo de contribuciones.

   El valor predeterminado es de 10 anuncios.

* **[!UICONTROL Frecuencia de límite de UGC]**

   Período de tiempo que limita el límite de UGC.

   El valor predeterminado es de 60 minutos.

* **[!UICONTROL Dominios]**

   Una lista de lista de permitidos de uno o varios dominios de correo electrónico. Seleccione el icono + para realizar entradas adicionales.

   Los usuarios con direcciones de correo electrónico en la lista de permitidos de dominios no se ven afectados cuando se aplican automáticamente los límites de contribución de UGC. Por ejemplo, si el dominio `mycompany.com` se agrega a la lista de dominios, un miembro con dirección de correo electrónico `me@mycompany.com` nunca se verá restringido de ser publicado.

   El valor predeterminado es una lista de permitidos vacía.

* **[!UICONTROL Destinatarios de mensajería]**

   Lista de uno o varios ID autorizables de miembros que pueden modificar los límites de contribución de los miembros. Seleccione el icono + para realizar entradas adicionales.

   Los Miembros sólo podrán ponerse en contacto con miembros especificados cuando se haya alcanzado su límite.

   El valor predeterminado no es ningún destinatario de mensajería.

Nota: La configuración predeterminada da como resultado un límite de 10 anuncios en un periodo de una hora.
