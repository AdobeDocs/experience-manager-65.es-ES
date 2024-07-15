---
title: Reviews Essentials
description: Obtenga información sobre cómo las revisiones en AEM Communities son un componente compuesto basado en un sistema de comentarios que contiene uno o más componentes de clasificación (recuento).
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 91e0e245-a2f1-4bd7-b38f-7641fd94a547
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 1%

---

# Reviews Essentials {#reviews-essentials}

Esta función consta de dos componentes que funcionan juntos: revisiones y resúmenes de revisiones.

Las revisiones son un componente compuesto basado en un [sistema de comentarios](essentials-comments.md) que contiene uno o más [componentes de clasificación](rating-basics.md) (recuento).

No se admite la publicación anónima de una revisión. Los visitantes del sitio deben registrarse e iniciar sesión para agregar una revisión. El visitante (miembro) que inició sesión puede actualizar su revisión en cualquier momento.

## Essentials para el lado del cliente {#essentials-for-client-side}

### Repasos {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/evaluaciones/componentes/hbs/evaluaciones</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluible</strong></a></td>
   <td>Sí, las propiedades se pueden editar en el modo </i>design<i></td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.reviews</td>
  </tr>
  <tr>
   <td> <strong>plantillas</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/reviews.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/review.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/status.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/toolbar.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/clientlibs/review.css</td>
  </tr>
  <tr>
   <td><strong>propiedades</strong></td>
   <td>Ver <a href="reviews.md">Usando críticas</a></td>
  </tr>
 </tbody>
</table>

### Resumen de críticas {#review-summary}

| **resourceType** | social/evaluaciones/componentes/hbs/summary |
|---|---|
| [**incluible**](scf.md#add-or-include-a-communities-component) | Sí, las propiedades se pueden editar en el modo *design *mode |
| [**clientlibs**](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **plantillas** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **propiedades** | Ver [Usando críticas](reviews.md) |

* [Personalizaciones del lado del cliente](client-customize.md)

## Essentials para servidor {#essentials-for-server-side}

* [Revisar API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [Revisar extremos](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [Personalizaciones del lado del servidor](server-customize.md)

### Acceder a las críticas publicadas (UGC) {#accessing-posted-reviews-ugc}

La UGC debe moderarse utilizando uno de los métodos habituales de moderación.
Consulte [Moderación del contenido generado por el usuario](moderate-ugc.md).

AEM A partir de las comunidades de la versión 6.1 de, el uso de un [almacén común](working-with-srp.md) para UGC incluye el acceso programático a UGC independientemente de la opción de almacenamiento elegida (como ASRP, MSRP o JSRP).

**La ubicación y el formato del UGC en el repositorio están sujetos a cambios sin previo aviso**.

Consulte:

* [Resumen del proveedor de recursos de almacenamiento](srp.md) - Introducción y descripción general del uso del repositorio.
* [SRP y UGC Essentials](srp-and-ugc.md): métodos y ejemplos de utilidades SRP.
* [Acceder a UGC con SRP](accessing-ugc-with-srp.md): directrices de codificación.
* [Refactorización de SocialUtils](socialutils.md): asignando métodos de utilidad obsoletos a métodos de utilidad SRP actuales.
