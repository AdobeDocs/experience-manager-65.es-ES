---
title: Revisiones esenciales
seo-title: Revisiones esenciales
description: Revisiones y revisión de los componentes de resumen
seo-description: Revisiones y revisión de los componentes de resumen
uuid: 540c106e-ee3b-4261-82b2-a909d254dbf7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 62669a9d-2107-4644-a4bf-143d0ac148b3
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Revisiones esenciales {#reviews-essentials}

Esta función consta de dos componentes que funcionan juntos: revisa y revisa el resumen.

Las revisiones son un componente compuesto basado en un sistema [de](essentials-comments.md) comentarios que contiene uno o más componentes de [clasificación](rating-basics.md) (tally).

No se admite la publicación anónima de una revisión. Los visitantes del sitio deben registrarse e iniciar sesión para agregar una revisión. El visitante (miembro) que ha iniciado sesión puede actualizar su revisión en cualquier momento.

## Esenciales para el cliente {#essentials-for-client-side}

### Críticas {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/reseñas/componentes/hbs/reseñas</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusible</strong></a></td>
   <td>Sí: las propiedades se pueden editar en <i>el </i>modo de diseño</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.reseñas</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/reviews.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/review.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/status.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/toolbar.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/clientlibs/review.css</td>
  </tr>
  <tr>
   <td><strong>propiedades</strong></td>
   <td>Consulte <a href="reviews.md">Uso de las revisiones</a></td>
  </tr>
 </tbody>
</table>

### Resumen de críticas {#review-summary}

| **resourceType** | social/revisiones/componentes/hbs/resumen |
|---|---|
| [**inclusible **](scf.md#add-or-include-a-communities-component) | Sí: las propiedades se pueden editar en *design *mode |
| [**clientllibs **](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reseñas |
| **templates** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **propiedades** | Consulte [Uso de las revisiones](reviews.md) |

* [Personalizaciones del lado del cliente](client-customize.md)

## Esenciales para servidor {#essentials-for-server-side}

* [API de revisión](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [Revisar extremos](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [Personalizaciones del lado del servidor](server-customize.md)

### Acceso a las revisiones publicadas (UGC) {#accessing-posted-reviews-ugc}

La UGC debe moderarse utilizando uno de los métodos estándar de moderación.
Consulte [Moderación del contenido](moderate-ugc.md)generado por el usuario.

A partir de AEM 6.1 Communities, el uso de un almacén [](working-with-srp.md) común para UGC incluye acceso mediante programación a UGC independientemente de la opción de almacenamiento elegida (como ASRP, MSRP o JSRP).

**La ubicación y el formato del UGC en el repositorio están sujetos a cambios sin previo aviso**.

Consulte:

* [Información general](srp.md) del proveedor de recursos de almacenamiento de información: introducción y uso del repositorio
* [Elementos esenciales](srp-and-ugc.md) de SRP y UGC: métodos y ejemplos de utilidad SRP
* [Acceso a UGC con SRP](accessing-ugc-with-srp.md) : directrices de codificación
* [Refactorización](socialutils.md) de SocialUtils: asignación de métodos de utilidad obsoletos a métodos de utilidad SRP actuales

