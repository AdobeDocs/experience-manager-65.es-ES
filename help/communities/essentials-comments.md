---
title: Comments Essentials
description: Obtenga información acerca de cómo trabajar con el sistema de comentarios (componente Comentarios) y administrar el contenido generado por el usuario (UGC) en las publicaciones de los miembros de la comunidad.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8b4034f7-2f97-45ad-96d4-51cfbeae5991
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
source-wordcount: '373'
ht-degree: 3%
---
# Comments Essentials {#comments-essentials}

Esta página proporciona los aspectos básicos del trabajo con el sistema de comentarios (componente de comentarios) y las opciones para administrar el contenido generado por el usuario (UGC) que se produce cuando los miembros publican comentarios o respuestas.

El componente de comentarios establece un sistema de comentarios tal que cada publicación individual está representada por un componente de comentario (singular). Es el sistema de comentarios el que se incluye en la página. El sistema de comentarios crea los comentarios individuales cuando se invocan.

## Essentials para el lado del cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/commons/components/hbs/comments</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluido</strong></a></td>
   <td>Sí, las propiedades se pueden editar en el modo </i>design<i></td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.comments<br /> cq.social.hbs.vote</td>
  </tr>
  <tr>
   <td> <strong>plantillas</strong></td>
   <td> /libs/social/commons/components/hbs/comments/comments.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>CSS</strong></td>
   <td> /libs/social/commons/components/hbs/comments/clientlibs/commentsystem.css</td>
  </tr>
  <tr>
   <td><strong> propiedades</strong></td>
   <td> Ver <a href="comments.md">Uso de comentarios</a></td>
  </tr>
 </tbody>
</table>

[Personalizaciones del lado del cliente](client-customize.md)

### Una instancia por página {#one-instance-per-page}

La paginación y el uso de direcciones URL para el almacenamiento en caché y la vinculación requieren que la URL sea única para cada sistema de comentarios. Por lo tanto, solo se permite una instancia de un sistema de comentarios por página.

Otras características ya incluyen el sistema de comentarios. Estos son:

* [Blog](blog-developer-basics.md)
* [Calendario](calendar-basics-for-developers.md)
* [Biblioteca de archivos](essentials-file-library.md)
* [Foro](essentials-forum.md)
* [P y R](qna-essentials.md)
* [Repasos](reviews-basics.md)

### Lista de motivos de indicación {#flag-reason-list}

La lista de motivos de indicación se puede personalizar añadiendo flagreasonlist.hbs a la aplicación para sobrescribir lo que hay en

* `/libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs`

Esto se aplica a cualquier componente que amplía un sistema de comentarios.

## Essentials para servidor {#essentials-for-server-side}

* [API de comentarios](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [Extremos de comentarios](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [Personalizaciones del lado del servidor](server-customize.md)

### Acceder a los comentarios publicados (UGC) {#accessing-posted-comments-ugc}

La UGC debe moderarse utilizando uno de los métodos habituales de moderación.
Consulte [Moderar contenido generado por el usuario](moderate-ugc.md).

A partir de las comunidades de AEM 6.1, el uso de un [almacén común](working-with-srp.md) para UGC incluye acceso programático a UGC independientemente de la opción de almacenamiento elegida (como ASRP, MSRP o JSRP).

**La ubicación y el formato del UGC en el repositorio están sujetos a cambios sin previo aviso**.

Consulte:

* [Resumen del proveedor de recursos de almacenamiento](srp.md) - Introducción y descripción general del uso del repositorio.
* [SRP y UGC Essentials](srp-and-ugc.md): métodos y ejemplos de utilidades SRP.
* [Acceder a UGC con SRP](accessing-ugc-with-srp.md): directrices de codificación.
* [Refactorización de SocialUtils](socialutils.md): asignando métodos de utilidad obsoletos a métodos de utilidad SRP actuales.
