---
title: Elementos esenciales del foro
seo-title: Elementos esenciales del foro
description: Información general del foro
seo-description: Información general del foro
uuid: 68849582-8742-40be-9e7e-0b574ae38815
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 059c5bbe-07eb-4873-8157-2196df887b27
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 2%

---


# Forum Essentials {#forum-essentials}

Esta página proporciona la información esencial para trabajar con la función de foro.

## Esenciales para el cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceTypes</strong></td>
   <td>social/forum/components/hbs/forum<br /> social/forum/components/hbs/topic<br /> social/forum/components/hbs/post</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusible</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.vote<br /> cq.social.hbs.forum</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/forum/components/hbs/forum/forum.hbs<br /> /libs/social/forum/components/hbs/post/post.hbs<br /> /libs/social/forum/components/hbs/topic/topic.hbs<br /> /libs/social/forum/components/hbs/topic/list-item.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/forum/components/hbs/forum/clientlibs/forum.css</td>
  </tr>
  <tr>
   <td><strong> propiedades</strong></td>
   <td>Consulte <a href="forum.md">Función de foro</a></td>
  </tr>
 </tbody>
</table>

* [Personalizaciones del lado del cliente](client-customize.md)

## Esenciales para servidor {#essentials-for-server-side}

* [API de foro](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/forum/client/api/package-summary.html)

* [Extremos de foro](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/forum/client/endpoints/package-summary.html)

* [Personalizaciones del lado del servidor](server-customize.md)

### Función Foro {#forum-function}

Una estructura de sitio de comunidad que incluye la [función de foro](functions.md#forum-function), incluye un componente `forum` configurado, así como configuraciones que afectan a la moderación, el etiquetado y la traducción.

### Acceso a anuncios de foro (UGC) {#accessing-forum-posts-ugc}

La UGC debe moderarse utilizando uno de los métodos estándar de moderación.
Consulte [Moderación del contenido generado por el usuario](moderate-ugc.md).

A partir de AEM comunidades 6.1, el uso de un [almacén común](working-with-srp.md) para UGC incluye acceso programático a UGC independientemente de la opción de almacenamiento elegida (como ASRP, MSRP o JSRP).

**La ubicación y el formato del UGC en el repositorio están sujetos a cambios sin previo aviso**.

Consulte:

* [Almacenamiento Resource Provider Overview](srp.md) : Introducción y uso del repositorio.
* [SRP y UGC Essentials](srp-and-ugc.md)  - Métodos y ejemplos de utilidad SRP.
* [Acceso a UGC con SRP](accessing-ugc-with-srp.md) - Directrices de codificación.
* [Refactorización](socialutils.md)  de SocialUtils: asignación de métodos de utilidad obsoletos a métodos de utilidad SRP actuales.

