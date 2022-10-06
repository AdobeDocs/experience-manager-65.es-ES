---
title: Social Graph Essentials
seo-title: Social Graph Essentials
description: información general sobre el componente siguiente
seo-description: follow component and following component overview
uuid: 8ea33760-62b1-4de2-b07f-bc2417ade156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f8d85d72-0215-4680-a334-e37a530fba58
exl-id: c037a788-c943-4f95-a028-1fcb0ef48f86
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 4%

---

# Social Graph Essentials  {#social-graph-essentials}

La capacidad de un miembro de la Comunidad de seguir [actividades](essentials-activities.md) además de ser seguido, se establece mediante dos componentes:

La variable `following` debe asociarse con otro recurso y esta asociación ya está establecida para los miembros de Communities y las funciones de una [sitio de la comunidad](overview.md#communitiessites).

La variable `following` en el componente se enumeran los miembros que siguen al miembro actual o al miembro actual. Este gráfico social de las relaciones entre los miembros se incluye en el perfil de usuario establecido para un sitio de comunidad.

## Elementos esenciales para el cliente {#essentials-for-client-side}

### Siguiente {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>gráfico social/social/componentes/hbs/relaciones</td>
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
   <td>Consulte <a href="socialgraph.md">Uso del gráfico social</a></td>
  </tr>
  <tr>
   <td><strong> opcional<br /> property</strong></td>
   <td>
    <ul>
     <li>Nombre: <strong><code>outgoing</code></strong></li>
     <li>Tipo: Boolean (booleano)</li>
     <li>Valor:<br />
      <ul>
       <li><i>True </i>- El <code>following</code> presentará una lista de los miembros que son el miembro que ha iniciado sesión en ese momento <code>follows</code></li>
       <li><i>False </i>- El <code>following</code> enumerará los miembros que <code>follow </code>el miembro con sesión iniciada actualmente</li>
      </ul> </li>
    </ul> <p>El valor predeterminado es <i>true</i> si falta la propiedad. Actualmente, no es posible establecer esta propiedad mediante el cuadro de diálogo de edición en modo de autor. La propiedad debe agregarse a una instancia de la variable <code>following </code>nodo que utiliza <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td>
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

## Elementos esenciales para el servidor {#essentials-for-server-side}

* [API de gráfico social](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [Puntos finales de gráfico social](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [Personalizaciones del lado del servidor](server-customize.md)
