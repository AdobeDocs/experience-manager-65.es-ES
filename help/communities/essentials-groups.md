---
title: Community Group Essentials
seo-title: Community Group Essentials
description: Creación dinámica de sitios de comunidad
seo-description: Creating community sites dynamically
uuid: 168e7aeb-6e9a-468d-8ac4-274007cea252
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4f85cd3c-5158-4f23-abe2-7e375fd0c8d4
exl-id: f45ae7be-a500-463a-ab3e-81f281651a9d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 1%

---

# Community Group Essentials  {#community-group-essentials}

La función de grupos de comunidades es la capacidad de los usuarios autorizados de los entornos de publicación y creación de crear dinámicamente una subcomunidad dentro de un sitio de comunidad.

Como comunidades [paquete de características 1](deploy-communities.md#latestfeaturepack), es posible anidar grupos dentro de otros grupos

## Elementos esenciales para el cliente {#essentials-for-client-side}

### Lista de miembros de grupos de la comunidad {#community-groups-member-list}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/community groupmemberlist</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/communitygroupmemberlist.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/memberList.css</td>
  </tr>
  <tr>
   <td><strong>propiedades</strong></td>
   <td>Consulte <a href="creating-groups.md">Grupo de la comunidad</a></td>
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
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
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

## Elementos esenciales para el servidor {#essentials-for-server-side}

* [API de grupo de comunidad](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [Puntos finales de grupo de la comunidad](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [Personalizaciones del lado del servidor](server-customize.md)

### Función Grupos {#groups-function}

Una estructura de sitio de la comunidad que incluye un [Función de grupos](functions.md#groups-function) admitirá la creación de `community groups` desde los entornos de publicación y autor. El grupo de comunidad creado incluirá un `community groups member list` componente que enumera los miembros del grupo.

Uno o más [plantillas de grupo de la comunidad](tools-groups.md), que proporcionan el diseño de las páginas del grupo de la comunidad, pueden configurarse para la función Grupos cuando la función se agrega a un [plantilla del sitio de la comunidad](sites.md) o anidada en una plantilla de grupo de la comunidad.

La inclusión de varias plantillas de grupo de comunidad hace que se presente al usuario autorizado una selección de diseño en el momento en que se crea un nuevo grupo de comunidad para el sitio de la comunidad, como se muestra en la sección de [grupos de la comunidad](creating-groups.md) para autores.

### Grupos anidados {#nested-groups}

Como comunidades [FP1](deploy-communities.md#latestfeaturepack), es posible incluir una función Grupos dentro de una plantilla de grupo, lo que permite grupos anidados (subcomunidades).

Cuando una plantilla de grupo o sitio de comunidad incluye la función Grupos , es posible:

* Cree una subcomunidad en el entorno de creación.

* Cree un grupo en el entorno de publicación, cuando esté configurado para permitirlo.

Al crear un grupo en el entorno de creación, primero es necesario publicar el sitio de comunidad y después publicar el grupo. La publicación del sitio de la comunidad publicará las páginas del grupo, sin crear los grupos de miembros de la subcomunidad en los que se establecen las ACL. Por lo tanto, un grupo restringido (secreto) puede ser visible hasta que el grupo se publique explícitamente.

## Vínculos e información relacionada {#links-and-related-information}

* [Administración de usuarios y grupos de usuarios](users.md)
* [Consola Grupos de comunidades](groups.md)
* [Función Grupos](functions.md#groups-function)
* [Plantillas de grupos](tools-groups.md)
