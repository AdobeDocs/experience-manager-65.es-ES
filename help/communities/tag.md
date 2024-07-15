---
title: Tag Essentials
description: Obtenga información sobre cuándo se configuran los componentes de las comunidades con el etiquetado habilitado, los miembros de la comunidad pueden etiquetar el contenido que publican en el entorno de publicación.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 6e8af8cf-1239-46f9-b2fe-4aa80abc86ea
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 3%

---

# Tag Essentials {#tag-essentials}

Cuando los componentes de AEM Communities están configurados con el etiquetado habilitado, los miembros de la comunidad pueden etiquetar el contenido que publican en el entorno de publicación.

La infraestructura subyacente para las etiquetas aplicadas en el entorno de publicación es la misma que para las etiquetas aplicadas al contenido en el entorno de creación, como páginas y recursos:

* Consulte [Administración de etiquetas](../../help/sites-administering/tags.md) y [Etiquetado del contenido generado por el usuario](tag-ugc.md) (UGC) para obtener información sobre cómo crear y administrar etiquetas.

* Consulte [Etiquetado para desarrolladores](../../help/sites-developing/tags.md) para obtener información sobre el [marco de etiquetado](../../help/sites-developing/framework.md) y cómo incluir y ampliar etiquetas en [aplicaciones personalizadas](../../help/sites-developing/building.md).

* Consulte [Uso de la nube de etiquetas social](tagcloud.md) para obtener información para autores sobre cómo agregar un componente `social tag cloud` a una página para resaltar las etiquetas aplicadas a UGC en el entorno de publicación.

El etiquetado de UGC puede habilitarse al configurar un [sitio de la comunidad](sites-console.md#tagging) o una de las siguientes características:

* [Blog](blog-feature.md)
* [Calendario](calendar.md)
* [Biblioteca de archivos](file-library.md)
* [Foro](forum.md)
* [P y R](working-with-qna.md)

## Essentials para el lado del cliente {#essentials-for-client-side}

### Nube de etiquetas social {#social-tag-cloud}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/commons/components/hbs/tagcloud</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluible</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.tagcloud</td>
  </tr>
  <tr>
   <td> <strong>plantillas</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/tagcloud.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/clientlibs/tagcloud.css</td>
  </tr>
  <tr>
   <td><strong>propiedades</strong></td>
   <td>Ver <a href="tagcloud.md">Uso de la nube de etiquetas sociales</a></td>
  </tr>
 </tbody>
</table>

* [Personalizaciones del lado del cliente](client-customize.md)

## Essentials para servidor {#essentials-for-server-side}

* [API de nube de etiquetas social](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [Administrador de etiquetas sociales](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [Personalizaciones del lado del servidor](server-customize.md)

## Búsqueda de etiquetas {#tag-searching}

A partir del [paquete de funciones 1](deploy-communities.md#latestfeaturepack) (FP1), la búsqueda de etiquetas se realizará usando [títulos de etiquetas](../../help/sites-developing/framework.md#tag-characteristics).

Antes de FP1, la búsqueda se realizaba con [id. de etiqueta](../../help/sites-developing/framework.md#tagid).
