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
source-git-commit: 01f14c203e45b85c9d7733d88437bd56e3c27c8e

---


# Tally Essentials {#tally-essentials}

Tally es una clase abstracta que proporciona un método estándar para recopilar comentarios de los miembros sobre cómo valoran productos y servicios específicos. No se admiten comentarios anónimos. El visitante del sitio debe registrarse e iniciar sesión para participar e iniciar sesión para cambiar sus comentarios. El requisito de iniciar sesión facilita la moderación y mejora el valor de los comentarios al evitar múltiples publicaciones.

Se puede crear un componente de recuento personalizado ampliando la clase de recuento abstracto.

[&quot;Me gusta](essentials-liking.md) &quot; es una implementación de la cuenta que es una forma simple de expresar una opinión positiva.

[Votar](essentials-voting.md) es una implementación de la cuenta que es una simple forma de expresar una opinión positiva o negativa.

[La clasificación](rating-basics.md) es una implementación del recuento que utiliza un sistema de estrellas para expresar una gama de opiniones desde positivas a negativas.

A partir de AEM 6.1, el componente de encuesta ya no está disponible.

[Revistas](reviews-basics.md) es un componente SCF que es un híbrido de [comentarios](essentials-comments.md) y [clasificación](rating-basics.md).

## Esenciales para el cliente {#essentials-for-client-side}

* [Personalizaciones del lado del cliente](client-customize.md)

## Esenciales para servidor {#essentials-for-server-side}

* [API de Tally](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Extremos de recuento](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personalizaciones del lado del servidor](server-customize.md)

### Acceso a las tablas publicadas (UGC) {#accessing-posted-tallies-ugc}

La UGC debe moderarse utilizando uno de los métodos estándar de moderación.
Consulte [Moderación del contenido](moderate-ugc.md)generado por el usuario.

A partir de AEM 6.1 Communities, el uso de un almacén [](working-with-srp.md) común para UGC incluye acceso mediante programación a UGC independientemente de la opción de almacenamiento elegida (como ASRP, MSRP o JSRP).

**La ubicación y el formato del UGC en el repositorio están sujetos a cambios sin previo aviso**.

Consulte:

* [Información general](srp.md) del proveedor de recursos de almacenamiento de información: introducción y uso del repositorio
* [Elementos esenciales](srp-and-ugc.md) de SRP y UGC: métodos y ejemplos de utilidad SRP
* [Acceso a UGC con SRP](accessing-ugc-with-srp.md) : directrices de codificación
* [Refactorización](socialutils.md) de SocialUtils: asignación de métodos de utilidad obsoletos a métodos de utilidad SRP actuales

