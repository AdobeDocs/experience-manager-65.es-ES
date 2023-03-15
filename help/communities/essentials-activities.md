---
title: Activity Stream Essentials
seo-title: Activity Stream Essentials
description: Lista de actividades recientes realizadas por un miembro o una lista de actividades recientes en un solo hilo de contenido
seo-description: List of recent activites performed by a member or a list of recent activities on a single thread of content
uuid: 30c5ac08-0af0-4670-9d81-0beb5c93e00a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8714b456-527a-457b-82c4-21bd445dfd9c
docset: aem65
exl-id: d98bcbe4-3f80-49ec-b40c-417be0d97350
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 2%

---

# Activity Stream Essentials {#activity-stream-essentials}

Las actividades de un miembro de la comunidad que ha iniciado sesión, como publicar en un foro o blog, se recopilan en un flujo que se puede filtrar y mostrar de varias formas mediante la configuración del componente flujos de actividad.

La capacidad de seguir agrega otro conjunto de actividades cuando los miembros de la comunidad siguen publicaciones de interés u otros miembros de la comunidad.

Todo [sitios de la comunidad](/help/communities/overview.md#communitiessites) incluya una página de perfil de usuario para el miembro conectado que mostrará las actividades de los miembros de la misma manera.

## Conceptos  {#concepts}

Un *flujo de actividad* es la lista de actividades recientes realizadas por un miembro o una lista de actividades recientes en un solo hilo de contenido, como un tema de foro o un blog.

Un miembro puede seguir un flujo de actividad, ya sea siguiendo a otro individuo o contenido.

A *suministro de noticias* es una combinación de los flujos de actividad que sigue un miembro en un solo flujo.

A *[gráfico social](/help/communities/essentials-socialgraph.md)* registra las siguientes relaciones de un miembro a otro.

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
   <td> <strong>templates</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/activitystreams.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity-title.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/clientlibs/activitystreams.css</td>
  </tr>
  <tr>
   <td><strong> propiedades</strong></td>
   <td>Consulte <a href="/help/communities/activities.md">Función Flujos de actividad</a></td>
  </tr>
 </tbody>
</table>

* [Personalizaciones del lado del cliente](/help/communities/client-customize.md)

## Essentials para servidor {#essentials-for-server-side}

* [API de flujos de actividad](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [API de escucha de flujos de actividad](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [Personalizaciones del lado del servidor](/help/communities/server-customize.md)

### Función Secuencia de actividades {#activity-stream-function}

Una estructura de sitio de la comunidad que incluye [Función Secuencia de actividades](/help/communities/functions.md#activity-stream-function), incluye un configurado `activity streams` componente.
