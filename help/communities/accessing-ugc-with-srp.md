---
title: Acceso a UGC con SRP
seo-title: Acceso a UGC con SRP
description: Cuando un sitio está configurado para utilizar ASRP o MSRP, el UGC real no se almacena en el almacén de nodos (JCR) de AEM
seo-description: Cuando un sitio está configurado para utilizar ASRP o MSRP, el UGC real no se almacena en el almacén de nodos (JCR) de AEM
uuid: 30549f93-e370-4b8b-a35a-69e05884227e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 72d4022c-43ba-49e0-b94c-f2beabaef64d
docset: aem65
translation-type: tm+mt
source-git-commit: 974d58efa560b90234d5121a11bdb445c7bf94cf

---


# Acceso a UGC con SRP {#accessing-ugc-with-srp}

## Acerca de SRP {#about-srp}

Todos los componentes y funciones de AEM Communities se basan en el marco de componentes [sociales (SCF)](/help/communities/scf.md), que llama a la API de SocialResourceProvider para acceder a todo el contenido generado por el usuario (UGC).

Antes de crear un sitio de comunidad, el proveedor de recursos [de almacenamiento (SRP)](/help/communities/working-with-srp.md) debe configurarse para seleccionar una implementación coherente con la [topología](/help/communities/topologies.md)subyacente. Las implementaciones de SRP se basan en tres opciones de almacenamiento:

1. [ASRP](/help/communities/asrp.md) : almacenamiento a petición de Adobe
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## Acerca del almacenamiento UGC {#about-ugc-storage}

Lo que es importante saber sobre el almacenamiento de UGC es que, cuando un sitio está configurado para utilizar ASRP o MSRP, el UGC real no se almacena en el almacén [de](/help/sites-deploying/data-store-config.md) nodos (JCR) de AEM.

Aunque puede haber nodos en JCR que ocultan el UGC para proporcionar metadatos útiles, estos nodos no deben confundirse con el UGC real.

Consulte Visión General [del Proveedor de Recursos de Almacenamiento de Información.](/help/communities/srp.md)

## Práctica recomendada {#best-practice}

Al desarrollar componentes personalizados, los desarrolladores deben tener cuidado de codificar independientemente de la topología elegida actualmente, conservando así la flexibilidad para pasar a una nueva topología en el futuro.

### Supongamos que JCR no está disponible {#assume-jcr-not-available}

Deben evitarse los métodos específicos de JCR.

Métodos de uso:

* Sling API (recurso de Sling)

   * no asumir que hay nodos JCR

* Eventos OSGi

   * no supongamos que hay eventos JCR

* [SocialResourceUtilities](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtilities](/help/communities/socialutils.md#scfutilities-package)

Métodos para evitar:

* API de nodo
* Eventos de JCR
* lanzadores de flujo de trabajo (que utilizan eventos JCR)

### Usar colecciones de búsqueda {#use-search-collections}

Los distintos SRP pueden tener distintos idiomas de consulta nativos. Se recomienda utilizar métodos del paquete [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) para ejecutar el lenguaje de consulta adecuado.

Para obtener más información, consulte [Search Essentials](/help/communities/search-implementation.md).

## Medios {#resources}

* [Almacenamiento](/help/communities/working-with-srp.md) de contenido de la comunidad: analiza las opciones de SRP disponibles para una tienda común UGC
* [Información general](/help/communities/srp.md) del proveedor de recursos de almacenamiento de información: introducción y uso del repositorio
* [Elementos esenciales](/help/communities/srp-and-ugc.md) de SRP y UGC: métodos y ejemplos de utilidad SRP
* [Esenciales](/help/communities/search-implementation.md) de búsqueda: información esencial para buscar UGC
* [Refactorización](/help/communities/socialutils.md) de SocialUtils: asignación de métodos de utilidad obsoletos a métodos de utilidad SRP actuales

