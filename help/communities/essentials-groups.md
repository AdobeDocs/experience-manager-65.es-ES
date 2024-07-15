---
title: Elementos esenciales del grupo de comunidad
description: Descubra cómo los usuarios autorizados pueden utilizar la función Grupos de la comunidad para crear dinámicamente una subcomunidad dentro de un sitio de la comunidad.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: f45ae7be-a500-463a-ab3e-81f281651a9d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 1%

---

# Elementos esenciales del grupo de comunidad  {#community-group-essentials}

La función de grupos de comunidad es la capacidad de una subcomunidad para que los usuarios autorizados de los entornos de publicación y creación la creen dinámicamente dentro de un sitio de comunidad.

A partir del paquete de funciones 1](deploy-communities.md#latestfeaturepack) de las comunidades [es posible anidar grupos dentro de otros grupos.

## Essentials para el lado del cliente {#essentials-for-client-side}

### Lista de miembros de grupos de comunidad {#community-groups-member-list}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/community/groupmemberlist</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>plantillas</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/communitygroupmemberlist.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/memberList.css</td>
  </tr>
  <tr>
   <td><strong>propiedades</strong></td>
   <td>Ver <a href="creating-groups.md">grupo de la comunidad</a></td>
  </tr>
 </tbody>
</table>

### Grupos de la comunidad {#community-groups}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/community groups</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>plantillas</strong></td>
   <td> /libs/social/group/components/hbs/communitygroups/communitygroups.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/communitygroups.css</td>
  </tr>
 </tbody>
</table>

* [Personalizaciones del lado del cliente](client-customize.md)

## Essentials para servidor {#essentials-for-server-side}

* [API del grupo de la comunidad](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [Puntos finales de grupo de comunidad](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [Personalizaciones del lado del servidor](server-customize.md)

### Función Grupos {#groups-function}

Una estructura de sitio de comunidad que incluye una función [Grupos](functions.md#groups-function) admite la creación de `community groups` nuevos desde los entornos de publicación y creación. El grupo de comunidad creado incluye un componente `community groups member list` que enumera los miembros del grupo.

Se pueden configurar una o más [plantillas de grupo de comunidad](tools-groups.md), que proporcionan el diseño de las páginas de grupo de comunidad, para la función Grupos. Esto ocurre cuando la función se agrega a una [plantilla del sitio de la comunidad](sites.md) o se anida dentro de una plantilla de grupo de la comunidad.

La inclusión de varias plantillas de grupo de comunidad resulta en una opción. Es decir, la opción de diseño que se presenta al usuario autorizado en el momento en que se crea un grupo de comunidad para el sitio de comunidad. Consulte la sección sobre [grupos de la comunidad](creating-groups.md) para autores.

### Grupos anidados {#nested-groups}

A partir de las comunidades [FP1](deploy-communities.md#latestfeaturepack), es posible incluir una función de grupos dentro de una plantilla de grupo, permitiendo así que haya grupos anidados (subcomunidades).

Cuando un sitio de comunidad o una plantilla de grupo incluye la función Grupos, es posible:

* Cree una subcomunidad en el entorno de creación.

* Cree un grupo en el entorno de publicación, cuando esté configurado para permitirlo.

Al crear un grupo en el entorno de creación, es necesario publicar primero el sitio de la comunidad y, a continuación, publicar el grupo. Al publicar el sitio de la comunidad, se publican las páginas del grupo, sin crear los grupos de miembros de la subcomunidad en los que se establecen las ACL. Por lo tanto, un grupo restringido (secreto) puede ser visible hasta que se publique explícitamente el grupo.

## Vínculos e información relacionada {#links-and-related-information}

* [Administración de usuarios y grupos de usuarios](users.md)
* [Consola de grupos de Communities](groups.md)
* [Función Grupos](functions.md#groups-function)
* [Plantillas de grupo](tools-groups.md)
