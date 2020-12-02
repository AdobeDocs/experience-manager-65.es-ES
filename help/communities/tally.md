---
title: Tally Essentials
seo-title: Tally Essentials
description: Descripción general de la clase Tally
seo-description: Descripción general de la clase Tally
uuid: c369c6a1-9ced-4b5c-af43-8c03236eaa52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 9941ba90-3d40-4c90-bca8-5db49603cbfa
translation-type: tm+mt
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---


# Tally Essentials {#tally-essentials}

Tally es una clase abstracta que proporciona un método estándar para recopilar comentarios de los miembros sobre cómo valoran productos y servicios específicos. No se admiten comentarios anónimos. El visitante del sitio debe registrarse e iniciar sesión para participar e iniciar sesión para cambiar sus comentarios. El requisito de iniciar sesión facilita la moderación y mejora el valor de los comentarios al evitar múltiples publicaciones.

Se puede crear un componente de recuento personalizado ampliando la clase de recuento abstracto.

[&quot;](essentials-liking.md) Me gusta&quot; es una implementación de la cuenta que es una simple forma de expresar una opinión positiva.

[](essentials-voting.md) Votinges es una implementación de la cuenta que es una simple forma de expresar una opinión positiva o negativa.

[](rating-basics.md) Ratinges es una implementación del recuento que utiliza un sistema de estrellas para expresar una gama de opiniones desde positivas a negativas.

A partir de AEM 6.1, el componente de encuesta ya no está disponible.

[](reviews-basics.md) Revisa un componente SCF que es un híbrido de  [](essentials-comments.md) comentarios y  [calificaciones](rating-basics.md).

## Esenciales para el cliente {#essentials-for-client-side}

* [Personalizaciones del lado del cliente](client-customize.md)

## Esenciales para servidor {#essentials-for-server-side}

* [API de Tally](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Extremos de recuento](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personalizaciones del lado del servidor](server-customize.md)

### Acceso a listas de contenido (UGC) {#accessing-posted-tallies-ugc}

La UGC debe moderarse utilizando uno de los métodos estándar de moderación.
Consulte [Moderación del contenido generado por el usuario](moderate-ugc.md).

A partir de AEM comunidades 6.1, el uso de un [almacén común](working-with-srp.md) para UGC incluye acceso programático a UGC independientemente de la opción de almacenamiento elegida (como ASRP, MSRP o JSRP).

**La ubicación y el formato del UGC en el repositorio están sujetos a cambios sin previo aviso**.

Consulte:

* [Almacenamiento Resource Provider Overview](srp.md) : Introducción y uso del repositorio.
* [SRP y UGC Essentials](srp-and-ugc.md)  - Métodos y ejemplos de utilidad SRP.
* [Acceso a UGC con SRP](accessing-ugc-with-srp.md) - Directrices de codificación.
* [Refactorización](socialutils.md)  de SocialUtils: asignación de métodos de utilidad obsoletos a métodos de utilidad SRP actuales.

