---
title: Social Graph Essentials
description: Obtenga información acerca de los aspectos básicos del gráfico social mediante los componentes Siguiendo y Seguir en un sitio de la comunidad.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: c037a788-c943-4f95-a028-1fcb0ef48f86
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 9f5812d7b252bcf39896b4fbf2e3ac5c24bdb808
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 2%
---
# Social Graph Essentials  {#social-graph-essentials}

La capacidad de un miembro de la comunidad para seguir [actividades](essentials-activities.md) y ser seguido se establece mediante dos componentes:

El componente `following` debe estar asociado con otro recurso y esta asociación ya está establecida para los miembros y características de las comunidades existentes en un [sitio de la comunidad](overview.md#communitiessites).

El componente `following` enumera los miembros que están siguiendo al miembro actual o que están siendo seguidos por el miembro actual. Este gráfico social de las relaciones entre los miembros se incluye en el perfil de usuario establecido para un sitio de la comunidad.

## Essentials para el lado del cliente {#essentials-for-client-side}

### Siguiente {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/socialgraph/components/hbs/related</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluible</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.socialgraph</td>
  </tr>
  <tr>
   <td> <strong>plantillas</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/relationships.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/clientlibs/relationships.css</td>
  </tr>
  <tr>
   <td><strong> propiedades</strong></td>
   <td>Ver <a href="socialgraph.md">Uso del gráfico social</a></td>
  </tr>
  <tr>
   <td><strong> propiedad <br /> opcional</strong></td>
   <td>
    <ul>
     <li>Nombre: <strong><code>outgoing</code></strong></li>
     <li>Tipo: booleano</li>
     <li>Valor:<br />
      <ul>
       <li><i>True </i>- El componente <code>following</code> enumera los miembros que han iniciado sesión como miembros <code>follows</code></li>
       <li><i>False </i>- El componente <code>following</code> enumera los miembros que <code>follow </code>el miembro que inició sesión</li>
      </ul> </li>
    </ul> <p>El valor predeterminado es <i>true</i> si falta la propiedad. No es posible establecer esta propiedad mediante el cuadro de diálogo de edición en el modo Autor. La propiedad debe agregarse a una instancia del nodo <code>following</code> mediante <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Seguir {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**incluible**](scf.md#add-or-include-a-communities-component) | No |
| **plantillas** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [Personalizaciones del lado del cliente](client-customize.md)

## Essentials para servidor {#essentials-for-server-side}

* [API de gráfico social](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [Extremos de gráfico social](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [Personalizaciones del lado del servidor](server-customize.md)
