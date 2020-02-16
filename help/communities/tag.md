---
title: Aspectos básicos de etiquetas
seo-title: Aspectos básicos de etiquetas
description: Descripción general de la etiqueta
seo-description: Descripción general de la etiqueta
uuid: a5d52319-f821-4608-b0ab-abc8a1374343
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d355a3ee-c8a8-4a07-8d28-d1a99bda315c
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Aspectos básicos de etiquetas {#tag-essentials}

Cuando los componentes de Comunidades AEM están configurados con etiquetado habilitado, los miembros de la comunidad pueden etiquetar el contenido que publican en el entorno de publicación.

La infraestructura subyacente para las etiquetas aplicadas en el entorno de publicación es la misma que para las etiquetas aplicadas al contenido en el entorno de creación, como páginas y recursos:

* Consulte [Administración de etiquetas](../../help/sites-administering/tags.md) y [Etiquetado de contenido](tag-ugc.md) generado por el usuario (UGC) para obtener información sobre cómo crear y administrar etiquetas.

* See [Tagging for Developers](../../help/sites-developing/tags.md) for information about the [tagging framework](../../help/sites-developing/framework.md) as well as including and extending tags in [custom applications](../../help/sites-developing/building.md).

* Consulte [Uso de Social Tag Cloud](tagcloud.md) para obtener información sobre cómo agregar un `social tag cloud` componente a una página para resaltar las etiquetas aplicadas a UGC en el entorno de publicación.

* Consulte [Etiquetado de recursos](tag-resources.md) de habilitación para obtener información sobre cómo etiquetar recursos para catálogos.

El etiquetado de UGC puede habilitarse al configurar un sitio [de](sites-console.md#tagging) comunidad o una de las siguientes funciones:

* [Blog](blog-feature.md)
* [Calendario](calendar.md)
* [Biblioteca de archivos](file-library.md)
* [Foro](forum.md)
* [P y R](working-with-qna.md)

## Esenciales para el cliente {#essentials-for-client-side}

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
   <td>Consulte <a href="tagcloud.md">Uso de Social Tag Cloud</a></td>
  </tr>
 </tbody>
</table>

* [Personalizaciones del lado del cliente](client-customize.md)

## Esenciales para servidor {#essentials-for-server-side}

* [API de nube de etiquetas de Social](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [Administrador de etiquetas de Social](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [Personalizaciones del lado del servidor](server-customize.md)

## Búsqueda de etiquetas {#tag-searching}

A partir del paquete de [funciones 1](deploy-communities.md#latestfeaturepack) (FP1), la búsqueda de etiquetas se realiza mediante títulos [de](../../help/sites-developing/framework.md#tag-characteristics)etiquetas.

Antes de FP1, la búsqueda se realizaba mediante identificadores [de etiqueta](../../help/sites-developing/framework.md#tagid).
