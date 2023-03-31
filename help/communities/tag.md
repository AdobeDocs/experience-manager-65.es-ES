---
title: Aspectos básicos de las etiquetas
seo-title: Tag Essentials
description: Información general de etiquetas
seo-description: Tag overview
uuid: a5d52319-f821-4608-b0ab-abc8a1374343
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d355a3ee-c8a8-4a07-8d28-d1a99bda315c
exl-id: 6e8af8cf-1239-46f9-b2fe-4aa80abc86ea
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 3%

---

# Aspectos básicos de las etiquetas {#tag-essentials}

Cuando los componentes de AEM Communities se configuran con el etiquetado habilitado, los miembros de la comunidad pueden etiquetar el contenido que publican en el entorno de publicación.

La infraestructura subyacente para las etiquetas aplicadas en el entorno de publicación es la misma que para las etiquetas aplicadas al contenido en el entorno de creación, como páginas y recursos:

* Consulte [Administración de etiquetas](../../help/sites-administering/tags.md) y [Etiquetado del contenido generado por el usuario](tag-ugc.md) (UGC) para obtener información sobre la creación y administración de etiquetas.

* Consulte [Etiquetado para desarrolladores](../../help/sites-developing/tags.md) para obtener información sobre la variable [marco de etiquetado](../../help/sites-developing/framework.md) , así como la inclusión y ampliación de etiquetas en [aplicaciones personalizadas](../../help/sites-developing/building.md).

* Consulte [Uso de la nube de etiquetas social](tagcloud.md) para obtener información para los autores sobre cómo añadir un `social tag cloud` a una página para resaltar las etiquetas aplicadas a UGC en el entorno de publicación.

El etiquetado de UGC puede estar habilitado al configurar un [sitio de la comunidad](sites-console.md#tagging) o una de las siguientes características:

* [Blog](blog-feature.md)
* [Calendario](calendar.md)
* [Biblioteca de archivos](file-library.md)
* [Foro](forum.md)
* [P y R](working-with-qna.md)

## Elementos esenciales para el cliente {#essentials-for-client-side}

### Nube de etiquetas social {#social-tag-cloud}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/commons/components/hbs/tagcloud</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusible</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.tagcloud</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/tagcloud.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/clientlibs/tagcloud.css</td>
  </tr>
  <tr>
   <td><strong>propiedades</strong></td>
   <td>Consulte <a href="tagcloud.md">Uso de la nube de etiquetas social</a></td>
  </tr>
 </tbody>
</table>

* [Personalizaciones del lado del cliente](client-customize.md)

## Elementos esenciales para el servidor {#essentials-for-server-side}

* [API de Social Tag Cloud](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [Administrador de etiquetas de Social](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [Personalizaciones del lado del servidor](server-customize.md)

## Búsqueda de etiquetas {#tag-searching}

A partir de [paquete de características 1](deploy-communities.md#latestfeaturepack) (FP1), la búsqueda de etiquetas se realiza utilizando [títulos de etiquetas](../../help/sites-developing/framework.md#tag-characteristics).

Antes de FP1, la búsqueda se realizaba mediante [id de etiqueta](../../help/sites-developing/framework.md#tagid).
