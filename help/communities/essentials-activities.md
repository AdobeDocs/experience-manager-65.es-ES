---
title: Elementos esenciales del flujo de actividad
seo-title: Elementos esenciales del flujo de actividad
description: Lista de las actividades recientes realizadas por un miembro o una lista de actividades recientes en un solo subproceso de contenido
seo-description: Lista de las actividades recientes realizadas por un miembro o una lista de actividades recientes en un solo subproceso de contenido
uuid: 30c5ac08-0af0-4670-9d81-0beb5c93e00a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8714b456-527a-457b-82c4-21bd445dfd9c
docset: aem65
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 2%

---


# Actividad Stream Essentials {#activity-stream-essentials}

Las actividades de un miembro de la comunidad firmado, como publicar en un foro o blog, se recopilan en un flujo que puede filtrarse y mostrarse de diversas maneras a través de la configuración del componente de flujos de actividad.

La capacidad de seguir agrega otro conjunto de actividades cuando los miembros de la comunidad siguen publicaciones de interés u otros miembros de la comunidad.

Todos los [sitios de comunidad](/help/communities/overview.md#communitiessites) incluyen una página de perfil de usuario para el miembro que ha iniciado sesión que mostrará las actividades de miembros de la misma manera.

## Conceptos {#concepts}

Un *flujo de actividad* es la lista de actividades recientes realizadas por un miembro o una lista de actividades recientes en un único subproceso de contenido, como un tema de foro o un blog.

Un miembro puede seguir un flujo de actividad, ya sea siguiendo a otro individuo o contenido.

Una *fuente de noticias* es una combinación de los flujos de actividad seguidos por un miembro en un único flujo.

Un *[gráfico social](/help/communities/essentials-socialgraph.md)* captura las siguientes relaciones de un miembro a otro.

## Esenciales para el cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>flujos sociales/de actividad/componentes/hbs/flujos de actividad</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>inclusible</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
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
   <td>Consulte <a href="/help/communities/activities.md">Función de flujos de Actividad</a></td>
  </tr>
 </tbody>
</table>

* [Personalizaciones del lado del cliente](/help/communities/client-customize.md)

## Esenciales para servidor {#essentials-for-server-side}

* [API de flujos de actividad](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [API de escucha de flujos de actividad](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [Personalizaciones del lado del servidor](/help/communities/server-customize.md)

### Función Secuencia de actividades {#activity-stream-function}

Una estructura de sitio de comunidad que incluye la función [Flujo de Actividad](/help/communities/functions.md#activity-stream-function), incluye un componente `activity streams` configurado.
