---
title: Activity Stream Essentials
description: Lista de actividades recientes realizadas por un miembro o una lista de actividades recientes en un solo hilo de contenido
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: d98bcbe4-3f80-49ec-b40c-417be0d97350
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 1%
---
# Activity Stream Essentials {#activity-stream-essentials}

Las actividades de un miembro de la comunidad que ha iniciado sesión, como publicar en un foro o blog, se recopilan en un flujo que se puede filtrar y mostrar de varias formas mediante la configuración del componente flujos de actividad.

La capacidad de seguir agrega otro conjunto de actividades cuando los miembros de la comunidad siguen publicaciones de interés u otros miembros de la comunidad.

Todos los [sitios de la comunidad](/help/communities/overview.md#communitiessites) incluyen una página de perfil de usuario para el miembro que ha iniciado sesión que mostrará las actividades de los miembros de la misma manera.

## Conceptos {#concepts}

Un *flujo de actividad* es la lista de actividades recientes realizadas por un miembro o una lista de actividades recientes en un solo hilo de contenido, como un tema de foro o un blog.

Un miembro puede seguir un flujo de actividad, ya sea siguiendo a otro individuo o contenido.

Una fuente de noticias *news feed* es una combinación de los flujos de actividad seguidos por un miembro en un solo flujo.

Un *[gráfico social](/help/communities/essentials-socialgraph.md)* captura las siguientes relaciones de un miembro a otro.

## Essentials para el lado del cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/activity/streams/components/hbs/activity streams</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>incluible</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.activitystreams</td>
  </tr>
  <tr>
   <td> <strong>plantillas</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/activitystreams.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity-title.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/clientlibs/activitystreams.css</td>
  </tr>
  <tr>
   <td><strong> propiedades</strong></td>
   <td>Ver <a href="/help/communities/activities.md">Función de flujos de actividad</a></td>
  </tr>
 </tbody>
</table>

* [Personalizaciones del lado del cliente](/help/communities/client-customize.md)

## Essentials para servidor {#essentials-for-server-side}

* [API de flujos de actividad](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [API de escucha de flujos de actividad](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [Personalizaciones del lado del servidor](/help/communities/server-customize.md)

### Función Secuencia de actividades {#activity-stream-function}

Una estructura de sitio de comunidad que incluye la [función de flujo de actividad](/help/communities/functions.md#activity-stream-function), incluye un componente `activity streams` configurado.
