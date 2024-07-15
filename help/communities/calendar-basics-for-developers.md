---
title: Calendar Essentials
description: Aprenda a trabajar con la función Calendario en las comunidades de Experience Manager. El calendario admite la identificación de grupos de usuarios miembros privilegiados.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 069e379d-c6fd-49ca-b337-df6fd466e023
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 2%

---

# Calendar Essentials {#calendar-essentials}

Esta página proporciona información esencial sobre cómo trabajar con la función de calendario.

## Essentials para el lado del cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/calendar/components/hbs/calendar</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluible</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.calendar</td>
  </tr>
  <tr>
   <td> <strong>plantillas</strong></td>
   <td>/libs/social/calendar/components/hbs/calendar/calendar.hbs</td>
   <td> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td>/libs/social/calendar/components/hbs/calendar/clientlibs/css/calendar.css<br /> /libs/social/calendar/components/hbs/calendar/clientlibs/css/jqueryui.css</td>
  </tr>
  <tr>
   <td><strong> propiedades</strong></td>
   <td>vea <a href="calendar.md">Usar calendarios</a></td>
  </tr>
 </tbody>
</table>

* [Personalizaciones del lado del cliente](client-customize.md)

## Essentials para servidor {#essentials-for-server-side}

* [API de calendario](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/calendar/client/api/package-summary.html)

* [Extremos de calendario](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/calendar/client/endpoints/package-summary.html)

* [Personalizaciones del lado del servidor](server-customize.md)

### Función Calendario {#calendar-function}

Una estructura de sitio de comunidad que incluye la [función Calendario](functions.md#calendar-function) tiene configurado un componente `calendar`. La función Calendario admite la identificación de un [grupo de usuarios miembros privilegiados](users.md#privileged-members-group).

### Acceso a las publicaciones del calendario (UGC) {#accessing-calendar-posts-ugc}

AEM A partir de las comunidades de la versión 6.1 de, el uso de un [almacén común](working-with-srp.md) para UGC incluye el acceso programático a UGC independientemente de la opción de almacenamiento elegida (como ASRP, MSRP o JSRP).

**La ubicación y el formato del UGC en el repositorio están sujetos a cambios sin previo aviso**.

Consulte:

* [Resumen del proveedor de recursos de almacenamiento](srp.md) - introducción y descripción general del uso del repositorio
* [SRP y UGC Essentials](srp-and-ugc.md): métodos y ejemplos de utilidades SRP
* [Acceder a UGC con SRP](accessing-ugc-with-srp.md): directrices de codificación
* [Refactorización de SocialUtils](socialutils.md): asignación de métodos de utilidad obsoletos a métodos de utilidad SRP actuales
