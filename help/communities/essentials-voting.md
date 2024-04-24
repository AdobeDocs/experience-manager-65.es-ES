---
title: Voting Essentials
description: Aprenda a utilizar el componente Votación que permite a los miembros clasificar un fragmento de contenido en particular seleccionando flechas arriba o abajo para indicar su opinión.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: e8ff751f-404a-498d-8e90-62a13ab593ff
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 1%

---

# Voting Essentials {#voting-essentials}

El componente de votación, un [corresponder](tally.md) subclase, es una herramienta útil que permite a los miembros calificar un fragmento particular de contenido simplemente seleccionando flechas arriba o abajo para indicar su opinión.

Se permite colocar varias instancias de un componente de votación en la misma página; cada instancia debe configurarse con un único `tally name` propiedad.

No se admite la publicación anónima de un voto. Los visitantes del sitio deben registrarse e iniciar sesión para participar en la votación solo una vez. El visitante (miembro) conectado puede cambiar su voto en cualquier momento.

## Essentials para el lado del cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/tally/componentes/hbs/votación</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluible</strong></a></td>
   <td>Sí, las propiedades se pueden editar en <i>diseño </i>modo</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.voting</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td><p> /libs/social/tally/components/hbs/voting/voting.hbs<br /> /libs/social/tally/components/hbs/voting/activity-title.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/voting/clientlibs/votingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>propiedades</strong></td>
   <td><p>Consulte <a href="voting.md">Uso de la votación</a></p> </td>
  </tr>
 </tbody>
</table>

* [Personalizaciones del lado del cliente](client-customize.md)

## Essentials para servidor {#essentials-for-server-side}

* [API de recuento](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Extremos de recuento](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personalizaciones del lado del servidor](server-customize.md)

### Acceso a la votación publicada (UGC) {#accessing-posted-voting-ugc}

La UGC debe moderarse utilizando uno de los métodos habituales de moderación.
Consulte [Moderación del contenido generado por el usuario](moderate-ugc.md).

AEM A partir de la versión 6.1 de las comunidades de la, se utilizará [almacén común](working-with-srp.md) para UGC incluye acceso programático a UGC independientemente de la opción de almacenamiento elegida (como ASRP, MSRP o JSRP).

**La ubicación y el formato del UGC en el repositorio están sujetos a cambios sin previo aviso**.

Consulte:

* [Resumen del proveedor de recursos de almacenamiento](srp.md) - introducción y descripción general del uso del repositorio.
* [SRP y UGC Essentials](srp-and-ugc.md) - Métodos y ejemplos de la utilidad SRP.
* [Acceso a UGC con SRP](accessing-ugc-with-srp.md) - directrices de codificación.
* [Refactorización de SocialUtils](socialutils.md) : asignación de métodos de utilidad obsoletos a métodos de utilidad SRP actuales.
