---
title: Acceso a UGC con SRP
seo-title: Accessing UGC with SRP
description: Cuando un sitio está configurado para utilizar ASRP o MSRP, el UGC real no se almacena en AEM almacén de nodos (JCR)
seo-description: When a site is configured to use ASRP or MSRP, the actual UGC is not be stored in AEM's node store (JCR)
uuid: 30549f93-e370-4b8b-a35a-69e05884227e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 72d4022c-43ba-49e0-b94c-f2beabaef64d
docset: aem65
exl-id: 1157366f-2cc5-46e4-8ec6-e66fe5d0a0f6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Acceso a UGC con SRP {#accessing-ugc-with-srp}

## Acerca de SRP {#about-srp}

Todos los componentes y funciones de AEM Communities se basan en la variable [marco de componentes sociales (SCF)](/help/communities/scf.md), que llama a la API de SocialResourceProvider para acceder a todo el contenido generado por el usuario (UGC).

Antes de crear un sitio de comunidad, la variable [proveedor de recursos de almacenamiento (SRP)](/help/communities/working-with-srp.md) debe configurarse para seleccionar una implementación coherente con el subyacente [topología](/help/communities/topologies.md). Las implementaciones de SRP se basan en tres opciones de almacenamiento:

1. [ASRP](/help/communities/asrp.md) - Adobe de almacenamiento bajo demanda
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## Acerca del almacenamiento UGC {#about-ugc-storage}

Lo que es importante saber sobre el almacenamiento de UGC es que, cuando un sitio está configurado para utilizar ASRP o MSRP, el UGC real no se almacena en AEM [almacén de nodos](/help/sites-deploying/data-store-config.md) (JCR).

Aunque puede haber nodos en JCR que ensombrecen el UGC para proporcionar metadatos útiles, estos nodos no deben confundirse con el UGC real.

Consulte [Información general del proveedor de recursos de almacenamiento.](/help/communities/srp.md)

## Práctica recomendada {#best-practice}

Al desarrollar componentes personalizados, los desarrolladores deben tener cuidado de codificar independientemente de la topología elegida actualmente, conservando así la flexibilidad para pasar a una nueva topología en el futuro.

### Supongamos que JCR no está disponible {#assume-jcr-not-available}

Se deben evitar los métodos específicos de JCR.

Métodos para utilizar :

* API de Sling (recurso de Sling)

   * no asumir que hay nodos JCR

* Eventos de OSGi

   * no asumir que hay eventos JCR

* [SocialResourceUtilities](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtilities](/help/communities/socialutils.md#scfutilities-package)

Métodos para evitar :

* API de nodo
* Eventos de JCR
* iniciadores de flujo de trabajo (que utilizan eventos JCR)

### Usar colecciones de búsqueda {#use-search-collections}

Los diferentes SRP pueden tener diferentes idiomas de consulta nativos. Se recomienda utilizar métodos del [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) para ejecutar el idioma de consulta adecuado.

Para obtener más información, consulte [Elementos básicos de búsqueda](/help/communities/search-implementation.md).

## Medios {#resources}

* [Almacenamiento de contenido de la comunidad](/help/communities/working-with-srp.md) - analiza las opciones de SRP disponibles para una tienda común UGC
* [Información general del proveedor de recursos de almacenamiento](/help/communities/srp.md) : introducción y descripción general del uso del repositorio
* [Elementos esenciales de SRP y UGC](/help/communities/srp-and-ugc.md) - Métodos y ejemplos de utilidad SRP
* [Elementos básicos de búsqueda](/help/communities/search-implementation.md) - información esencial para la búsqueda de UGC
* [Refactorización de SocialUtils](/help/communities/socialutils.md) : asignación de métodos de utilidad obsoletos a métodos de utilidad SRP actuales
