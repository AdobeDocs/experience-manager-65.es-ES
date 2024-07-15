---
title: Tally Essentials
description: Descubra cómo Tally es una clase abstracta que proporciona un método estándar para recopilar comentarios de los miembros sobre cómo valoran productos y servicios específicos.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0b508df9-1a24-4728-a254-f913eeb9b391
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# Tally Essentials {#tally-essentials}

Tally es una clase abstracta que proporciona un método estándar de recopilar comentarios de los miembros sobre cómo valoran productos y servicios específicos. No se admiten comentarios anónimos. Los visitantes del sitio deben registrarse e iniciar sesión para participar e iniciar sesión para cambiar sus comentarios. El requisito de iniciar sesión facilita la moderación y aumenta el valor de los comentarios al evitar varias publicaciones.

Se puede crear un componente de recuento personalizado ampliando la clase de recuento abstracto.

[Me gusta](essentials-liking.md) es una implementación de recuento que es una forma sencilla de expresar una opinión positiva.

[Votar](essentials-voting.md) es una implementación de recuento que es una forma simple de expresar una opinión positiva o negativa.

[Clasificación](rating-basics.md) es una implementación de recuento que usa un sistema de estrella para expresar una amplia gama de opiniones, desde positivas a negativas.

AEM A partir de la versión 6.1, el componente de encuesta ya no está disponible.

[Críticas](reviews-basics.md) es un componente SCF que es un híbrido de [comentarios](essentials-comments.md) y [clasificación](rating-basics.md).

## Essentials para el lado del cliente {#essentials-for-client-side}

* [Personalizaciones del lado del cliente](client-customize.md)

## Essentials para servidor {#essentials-for-server-side}

* [API de recuento](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Puntos finales de recuento](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personalizaciones del lado del servidor](server-customize.md)

### Acceso a los recuentos publicados (UGC) {#accessing-posted-tallies-ugc}

La UGC debe moderarse utilizando uno de los métodos habituales de moderación.
Consulte [Moderación del contenido generado por el usuario](moderate-ugc.md).

AEM A partir de las comunidades de la versión 6.1 de, el uso de un [almacén común](working-with-srp.md) para UGC incluye el acceso programático a UGC independientemente de la opción de almacenamiento elegida (como ASRP, MSRP o JSRP).

**La ubicación y el formato del UGC en el repositorio están sujetos a cambios sin previo aviso**.

Consulte:

* [Resumen del proveedor de recursos de almacenamiento](srp.md) - Introducción y descripción general del uso del repositorio.
* [SRP y UGC Essentials](srp-and-ugc.md): métodos y ejemplos de utilidades SRP.
* [Acceder a UGC con SRP](accessing-ugc-with-srp.md): directrices de codificación.
* [Refactorización de SocialUtils](socialutils.md): asignando métodos de utilidad obsoletos a métodos de utilidad SRP actuales.
