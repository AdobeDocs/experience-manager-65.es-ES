---
title: Comentarios esenciales
seo-title: Comentarios esenciales
description: Descripción general del componente Comentarios
seo-description: Descripción general del componente Comentarios
uuid: 58b7bb58-f598-4bcb-93ae-b7795cab51cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 18f54a1c-52aa-414d-b494-1f19b5c10345
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Comentarios esenciales {#comments-essentials}

Esta página proporciona lo esencial de trabajar con el sistema de comentarios (componente de comentarios) y opciones para administrar el contenido generado por el usuario (UGC) que se genera cuando los miembros publican comentarios o respuestas.

El componente de comentarios establece un sistema de comentarios de modo que cada publicación individual está representada por un componente de comentarios (singular). Es el sistema de comentarios que se incluye en la página. El sistema de comentarios creará los comentarios individuales cuando se invoquen.

## Esenciales para el cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/commons/components/hbs/comments</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusible</strong></a></td>
   <td>Sí: las propiedades se pueden editar en <i>el </i>modo de diseño</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>Clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.comments<br /> cq.social.hbs.vote</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/commons/components/hbs/comments/comments.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>CSS</strong></td>
   <td> /libs/social/commons/components/hbs/comments/clientlibs/commentsystem.css</td>
  </tr>
  <tr>
   <td><strong> propiedades</strong></td>
   <td> Consulte <a href="comments.md">Uso de comentarios</a></td>
  </tr>
 </tbody>
</table>

[Personalizaciones del lado del cliente](client-customize.md)

### Una instancia por página {#one-instance-per-page}

La paginación y el uso de direcciones URL para almacenar en caché y vincular requieren que la dirección URL sea única por sistema de comentarios. Por lo tanto, solo se permite una instancia de un sistema de comentarios por página.

Otras funciones ya incluyen el sistema de comentarios. Estos son:

* [Blog](blog-developer-basics.md)
* [Calendario](calendar-basics-for-developers.md)
* [Biblioteca de archivos](essentials-file-library.md)
* [Foro](essentials-forum.md)
* [P y R](qna-essentials.md)
* [Críticas](reviews-basics.md)

### Lista de motivos de indicación {#flag-reason-list}

La lista de motivos de marcado se puede personalizar agregando flagreasonlist.hbs a la aplicación para sobrescribir lo que se encuentra en

* /libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs

Esto se aplica a cualquier componente que extienda un sistema de comentarios.

## Esenciales para servidor {#essentials-for-server-side}

* [API de comentarios](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [Extremos de comentarios](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [Personalizaciones del lado del servidor](server-customize.md)

### Acceso a los comentarios enviados (UGC) {#accessing-posted-comments-ugc}

La UGC debe moderarse utilizando uno de los métodos estándar de moderación.
Consulte [Moderación del contenido](moderate-ugc.md)generado por el usuario.

A partir de AEM 6.1 Communities, el uso de un almacén [](working-with-srp.md) común para UGC incluye acceso mediante programación a UGC independientemente de la opción de almacenamiento elegida (como ASRP, MSRP o JSRP).

**La ubicación y el formato del UGC en el repositorio están sujetos a cambios sin previo aviso**.

Consulte:

* [Información general](srp.md) del proveedor de recursos de almacenamiento de información: Introducción y uso del repositorio
* [Elementos esenciales](srp-and-ugc.md) de SRP y UGC: métodos y ejemplos de utilidad SRP
* [Acceso a UGC con SRP](accessing-ugc-with-srp.md) - Directrices de codificación
* [Refactorización](socialutils.md) de SocialUtils: asignación de métodos de utilidad obsoletos a métodos de utilidad SRP actuales

