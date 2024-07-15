---
title: Rating Essentials
description: Descubra cómo el componente Clasificación, una subclase de recuento, permite que los miembros de la comunidad que iniciaron sesión clasifiquen una función del sitio web.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 49456944-ff0d-4507-b3b8-143c90067573
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---

# Rating Essentials {#rating-essentials}

El componente de clasificación, una subclase [tally](tally.md), permite que los miembros de la comunidad que iniciaron sesión clasifiquen una característica del sitio web.

Se permite colocar varias instancias de un componente de votación en la misma página; cada instancia debe configurarse con una propiedad `tally name` única.

No se admite la publicación anónima de una clasificación. Los visitantes del sitio deben registrarse e iniciar sesión para participar en una valoración solo una vez. El visitante (miembro) que ha iniciado sesión puede cambiar su clasificación en cualquier momento.

## Essentials para el lado del cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/tally/componentes/hbs/rating</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluible</strong></a></td>
   <td>Sí, las propiedades se pueden editar en el modo </i>design<i></td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.rating</td>
  </tr>
  <tr>
   <td> <strong>plantillas</strong></td>
   <td><p> /libs/social/tally/components/hbs/rating/rating.hbs<br /> /libs/social/tally/components/hbs/rating/display.hbs<br /> /libs/social/tally/components/hbs/rating/histogram.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/rating/clientlibs/ratingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>propiedades</strong></td>
   <td><p>Ver <a href="rating.md">Usando clasificación</a></p> </td>
  </tr>
 </tbody>
</table>

* [Personalizaciones del lado del cliente](client-customize.md)

## Essentials para servidor {#essentials-for-server-side}

* [API de recuento](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Puntos finales de recuento](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personalizaciones del lado del servidor](server-customize.md)

### Acceso a valoraciones publicadas (UGC) {#accessing-posted-ratings-ugc}

La UGC debe moderarse utilizando uno de los métodos habituales de moderación.
Consulte [Moderación del contenido generado por el usuario](moderate-ugc.md).

AEM A partir de las comunidades de la versión 6.1 de, el uso de un [almacén común](working-with-srp.md) para UGC incluye el acceso programático a UGC independientemente de la opción de almacenamiento elegida (como ASRP, MSRP o JSRP).

**La ubicación y el formato del UGC en el repositorio están sujetos a cambios sin previo aviso**.

Consulte:

* [Resumen del proveedor de recursos de almacenamiento](srp.md) - introducción y descripción general del uso del repositorio.
* [SRP y UGC Essentials](srp-and-ugc.md): métodos y ejemplos de utilidades SRP.
* [Acceder a UGC con SRP](accessing-ugc-with-srp.md): directrices de codificación.
* [Refactorización de SocialUtils](socialutils.md): asignación de métodos de utilidad obsoletos a métodos de utilidad SRP actuales.
