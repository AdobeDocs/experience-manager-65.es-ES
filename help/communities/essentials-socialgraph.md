---
title: Social Graph Essentials
description: Obtenga información acerca del siguiente componente y el componente Seguir.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: c037a788-c943-4f95-a028-1fcb0ef48f86
source-git-commit: f7b24617dec77c6907798b1615debdc2329c9d80
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 3%

---

# Social Graph Essentials  {#social-graph-essentials}

La capacidad de un miembro de la comunidad para seguir [actividades](essentials-activities.md) y a seguir se establece a través de dos componentes:

El `following` el componente debe estar asociado a otro recurso y esta asociación ya está establecida para los miembros y características existentes de Communities en un [sitio comunitario](overview.md#communitiessites).

El `following` El componente enumera los miembros que siguen al miembro actual o que están siendo seguidos por el miembro actual. Este gráfico social de las relaciones entre los miembros se incluye en el perfil de usuario establecido para un sitio de la comunidad.

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
   <td> <strong>templates</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/relationships.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/clientlibs/relationships.css</td>
  </tr>
  <tr>
   <td><strong> propiedades</strong></td>
   <td>Consulte <a href="socialgraph.md">Uso del gráfico social</a></td>
  </tr>
  <tr>
   <td><strong> opcional<br /> propiedad</strong></td>
   <td>
    <ul>
     <li>Nombre: <strong><code>outgoing</code></strong></li>
     <li>Tipo: booleano</li>
     <li>Valor:<br />
      <ul>
       <li><i>Verdadero </i>- El <code>following</code> Este componente enumera los miembros que han iniciado sesión como miembros <code>follows</code></li>
       <li><i>Falso </i>- El <code>following</code> El componente enumera los miembros que <code>follow </code>el miembro conectado</li>
      </ul> </li>
    </ul> <p>El valor predeterminado es <i>true</i> si falta la propiedad. No es posible establecer esta propiedad mediante el cuadro de diálogo de edición en el modo Autor. La propiedad debe añadirse a una instancia de <code>following</code> nodo que utiliza <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Seguir {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**incluible**](scf.md#add-or-include-a-communities-component) | No |
| **templates** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [Personalizaciones del lado del cliente](client-customize.md)

## Essentials para servidor {#essentials-for-server-side}

* [API de gráfico social](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [Extremos de gráfico social](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [Personalizaciones del lado del servidor](server-customize.md)
