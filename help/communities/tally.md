---
title: Tally Essentials
seo-title: Tally Essentials
description: Información general de la clase tally
seo-description: Tally class overview
uuid: c369c6a1-9ced-4b5c-af43-8c03236eaa52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 9941ba90-3d40-4c90-bca8-5db49603cbfa
exl-id: 0b508df9-1a24-4728-a254-f913eeb9b391
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# Tally Essentials {#tally-essentials}

Tally es una clase abstracta que proporciona un método estándar para recopilar comentarios de los miembros sobre cómo valoran productos y servicios específicos. No se admiten comentarios anónimos. El visitante del sitio debe registrarse e iniciar sesión para participar e iniciar sesión para cambiar sus comentarios. El requisito de iniciar sesión facilita la moderación y mejora el valor de los comentarios al evitar que se publiquen varias publicaciones.

Se puede crear un componente de recuento personalizado ampliando la clase de recuento abstracto.

[&quot;Me gusta&quot;](essentials-liking.md) es una implementación de la cuenta que es una forma simple de expresar una opinión positiva.

[Votación](essentials-voting.md) es una implementación de la cuenta que es una forma simple de expresar una opinión positiva o negativa.

[Clasificación](rating-basics.md) es una implementación de la cuenta que utiliza un sistema de estrellas para expresar una gama de opiniones desde positivas a negativas.

A partir de AEM 6.1, el componente de encuesta ya no está disponible.

[Reseñas](reviews-basics.md) es un componente SCF que es híbrido de [comentarios](essentials-comments.md) y [clasificación](rating-basics.md).

## Elementos esenciales para el cliente {#essentials-for-client-side}

* [Personalizaciones del lado del cliente](client-customize.md)

## Elementos esenciales para el servidor {#essentials-for-server-side}

* [API de Tally](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Puntos finales totales](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personalizaciones del lado del servidor](server-customize.md)

### Acceso a listas de correos (UGC) {#accessing-posted-tallies-ugc}

UGC debe moderarse utilizando uno de los métodos estándar de moderación.
Consulte [Moderación del contenido generado por el usuario](moderate-ugc.md).

A partir del AEM 6.1 Comunidades, se utilizará un [tienda común](working-with-srp.md) para UGC incluye acceso programático a UGC independientemente de la opción de almacenamiento elegida (como ASRP, MSRP o JSRP).

**La ubicación y el formato del UGC en el repositorio están sujetos a cambios sin previo aviso**.

Consulte:

* [Información general del proveedor de recursos de almacenamiento](srp.md) - Introducción y descripción general del uso del repositorio.
* [Elementos esenciales de SRP y UGC](srp-and-ugc.md) - Métodos y ejemplos de utilidad SRP.
* [Acceso a UGC con SRP](accessing-ugc-with-srp.md) - Directrices de codificación.
* [Refactorización de SocialUtils](socialutils.md) - Asignación de métodos de utilidad obsoletos a los métodos de utilidad SRP actuales.
