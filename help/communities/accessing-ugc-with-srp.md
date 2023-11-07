---
title: Acceso a UGC con SRP
description: AEM Cuando un sitio está configurado para utilizar ASRP o MSRP, el UGC real no se almacena en el almacén de nodos de la (JCR)
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 1157366f-2cc5-46e4-8ec6-e66fe5d0a0f6
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# Acceso a UGC con SRP {#accessing-ugc-with-srp}

## Acerca de SRP {#about-srp}

Todos los componentes y funciones de AEM Communities se basan en la variable [marco de componentes sociales (SCF)](/help/communities/scf.md), que llama a la API de SocialResourceProvider para acceder a todo el contenido generado por el usuario (UGC).

Antes de crear un sitio de la comunidad, la variable [proveedor de recursos de almacenamiento (SRP)](/help/communities/working-with-srp.md) debe configurarse para seleccionar una implementación coherente con el subyacente [topología](/help/communities/topologies.md). Las implementaciones de SRP se basan en tres opciones de almacenamiento:

1. [ASRP](/help/communities/asrp.md) - Adobe de almacenamiento bajo demanda
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## Acerca del almacenamiento UGC {#about-ugc-storage}

AEM Lo que es importante saber sobre el almacenamiento de UGC es que, cuando un sitio está configurado para utilizar ASRP o MSRP, el UGC real no se almacena en la base de datos de usuario de la red de almacenamiento de UGC (por sus siglas en inglés) de la red (por sus siglas en inglés), el UGC no se almacena en la base de datos de la red de almacenamiento de UGCs (por sus siglas en inglés) de la red de almacenamiento de UGCs [almacén de nodos](/help/sites-deploying/data-store-config.md) (JCR).

Aunque puede haber nodos en JCR que sombrean el UGC para proporcionar metadatos útiles, estos nodos no se deben confundir con el UGC real.

Consulte [Resumen del proveedor de recursos de almacenamiento.](/help/communities/srp.md)

## Práctica recomendada {#best-practice}

Al desarrollar componentes personalizados, los desarrolladores deben tener cuidado de codificar independientemente de la topología elegida actualmente, conservando así la flexibilidad para pasar a una nueva topología en el futuro.

### Suponer que JCR no está disponible {#assume-jcr-not-available}

Se deben evitar los métodos específicos para JCR.

Métodos que se deben utilizar:

* API de Sling (recurso de Sling)

   * no asuma que hay nodos JCR

* Eventos OSGi

   * no asuma que hay eventos JCR

* [SocialResourceUtilities](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtilities](/help/communities/socialutils.md#scfutilities-package)

Métodos para evitar :

* API del nodo
* Eventos JCR
* iniciadores de flujo de trabajo (que utilizan eventos JCR)

### Usar colecciones de búsqueda {#use-search-collections}

Los distintos SRP pueden tener diferentes idiomas de consulta nativos. Utilice los métodos de [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) para ejecutar el idioma de consulta adecuado.

Para obtener más información, consulte [Search Essentials](/help/communities/search-implementation.md).

## Recursos {#resources}

* [Almacenamiento de contenido de comunidad](/help/communities/working-with-srp.md) - analiza las opciones de SRP disponibles para un almacén común de UGC
* [Resumen del proveedor de recursos de almacenamiento](/help/communities/srp.md) - introducción y descripción general del uso del repositorio
* [SRP y UGC Essentials](/help/communities/srp-and-ugc.md) - Métodos y ejemplos de la utilidad SRP
* [Search Essentials](/help/communities/search-implementation.md) - información esencial para la búsqueda UGC
* [Refactorización de SocialUtils](/help/communities/socialutils.md) - Asignación de métodos de utilidad obsoletos a los métodos de utilidad SRP actuales
