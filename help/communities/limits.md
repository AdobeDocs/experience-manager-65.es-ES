---
title: Límites de contribución de miembros
description: La función de límites de contribución permite limitar las contribuciones para protegerlas contra el correo no deseado
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: d00a8eb2-47ce-425a-a312-f043f82912be
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# Límites de contribución de miembros {#member-contribution-limits}

## Información general {#overview}

La función de límites de contribución permite limitar las contribuciones de los miembros de la comunidad como medio de protección contra el correo no deseado.

Cuando un usuario es limitado, cualquier publicación que exceda el número permitido de contribuciones genera una alerta que indica que se ha superado el límite y que la publicación se rechaza. El miembro de la comunidad puede ir al centro de mensajes de la comunidad y ponerse en contacto con un administrador de la comunidad que pueda eliminar los límites si procede.

Los límites de contribución se pueden habilitar individualmente desde el [Consola Miembros](members.md) y/o configurarse para que se habilite automáticamente cuando los visitantes del sitio se conviertan en nuevos miembros.

Mediante la consola Miembros, un administrador de la comunidad puede quitar de forma proactiva los límites de contribución de un miembro en cualquier momento, o bien eliminarlos de forma reactiva cuando un miembro envía un mensaje a un administrador de la comunidad que realiza dicha solicitud.

## Configuración de límites de contribución de contenido generado por el usuario de AEM Communities {#aem-communities-user-generated-content-contribution-limits-configuration}

Esta configuración de OSGi:

* Define las características de los límites de contribución (número de entradas dentro de un periodo de tiempo).
* Identifica a quién puede enviar un mensaje el miembro cuando se alcanza el límite.
* Identifica los dominios que nunca deben restringirse.

Para llegar a esta configuración de OSGi:

* En el editor principal:
* Iniciar sesión con privilegios de administrador.
* Acceda a la [Consola web](../../help/sites-deploying/configuring-osgi.md).

   * Por ejemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Localizar `AEM Communities User Generated Content Contribution Limits Configuration`.
* Seleccione el icono de edición.

![configure-limits](assets/configure-limits.png)

* **[!UICONTROL Aplicar automáticamente límites de contribución UGC]**

  Si se selecciona, se establecen automáticamente límites de contribución para los usuarios cuando se registren como miembros de la comunidad. Esto se refleja en el perfil del miembro de la comunidad y se puede habilitar/deshabilitar en [consola de miembros](members.md). Los nuevos miembros con una dirección de correo electrónico de una lista de permitidos de dominios nunca están restringidos.

  El valor predeterminado está desmarcado.

* **[!UICONTROL Límite de UGC]**

  Número máximo de contribuciones.

  El valor predeterminado es diez entradas.

* **[!UICONTROL Frecuencia de límite UGC]**

  Período de tiempo que restringe el límite de UGC.

  El valor predeterminado es de 60 minutos.

* **[!UICONTROL Domains]**

  Una lista de lista de permitidos de uno o más dominios de correo electrónico. Seleccione el icono + para realizar entradas adicionales.

  Los usuarios con direcciones de correo electrónico en la lista de permitidos de dominios no se ven afectados cuando los límites de contribución UGC se aplican automáticamente. Por ejemplo, si el dominio `mycompany.com` se agrega a la lista de dominios y, a continuación, un miembro con dirección de correo electrónico `me@mycompany.com` nunca tiene restricciones para publicar.

  El valor predeterminado es una lista de permitidos vacía.

* **[!UICONTROL Destinatarios de mensajería]**

  Lista de uno o más ID autorizados de miembros que pueden modificar los límites de contribución de los miembros. Seleccione el icono + para realizar entradas adicionales.

  Los miembros sólo podrán ponerse en contacto con miembros especificados cuando se haya alcanzado su límite.

  El valor predeterminado es sin destinatarios de mensajería.

Nota: La configuración predeterminada da como resultado un límite de diez entradas en un periodo de una hora.
