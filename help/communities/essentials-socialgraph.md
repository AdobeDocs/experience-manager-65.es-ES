---
title: Elementos básicos de gráficos sociales
seo-title: Elementos básicos de gráficos sociales
description: información general sobre el componente y los componentes siguientes
seo-description: información general sobre el componente y los componentes siguientes
uuid: 8ea33760-62b1-4de2-b07f-bc2417ade156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f8d85d72-0215-4680-a334-e37a530fba58
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 4%

---


# Social Graph Essentials {#social-graph-essentials}

La capacidad de un miembro de la comunidad para seguir [actividades](essentials-activities.md) y seguir se establece mediante dos componentes:

El componente `following` debe asociarse con otro recurso y esta asociación ya está establecida para los miembros y funciones existentes de Communities en un [sitio de comunidad](overview.md#communitiessites).

El componente `following` lista los miembros que siguen al miembro actual o que siguen el miembro actual. Este gráfico social de las relaciones entre los miembros se incluye en el perfil de usuario creado para un sitio de comunidad.

## Esenciales para el cliente {#essentials-for-client-side}

### Siguiente {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/social/componentes/hbs/relaciones</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusible</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.socialgraph</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/relationships.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/clientlibs/relationships.css</td>
  </tr>
  <tr>
   <td><strong> propiedades</strong></td>
   <td>Consulte <a href="socialgraph.md">Uso de Social Graph</a></td>
  </tr>
  <tr>
   <td><strong> opcional<br />, propiedad</strong></td>
   <td>
    <ul>
     <li>Nombre: <strong><code>outgoing</code></strong></li>
     <li>Tipo: Boolean (booleano)</li>
     <li>Value:<br />
      <ul>
       <li><i>Verdadero  </i>- El  <code>following</code> componente lista a los miembros que son el miembro que ha iniciado sesión en ese momento <code>follows</code></li>
       <li><i>Falso  </i>- El  <code>following</code> componente lista a los miembros que  <code>follow </code>el miembro que ha iniciado sesión en ese momento</li>
      </ul> </li>
    </ul> <p>El valor predeterminado es <i>true</i> si falta la propiedad. Actualmente, no es posible establecer esta propiedad mediante el cuadro de diálogo de edición en modo de autor. La propiedad debe agregarse a una instancia del nodo <code>following </code>mediante <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Seguir {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**inclusible**](scf.md#add-or-include-a-communities-component) | No |
| **plantillas** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [Personalizaciones del lado del cliente](client-customize.md)

## Esenciales para servidor {#essentials-for-server-side}

* [API de gráfico social](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [Extremos de gráficos sociales](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [Personalizaciones del lado del servidor](server-customize.md)

