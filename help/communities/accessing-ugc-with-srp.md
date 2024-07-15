---
title: Acceso a UGC con SRP
description: AEM Cuando un sitio está configurado para utilizar ASRP o MSRP, el UGC real no se almacena en el almacén de nodos (JCR) de la base de datos de administración de nodos (CGU) de la red de distribución de datos (CGU) de la base de datos de usuario (CGU) de la base de datos de usuario (CGU) de la base de datos de datos de usuario (CGU) de la base de datos de usuario (CGU) de la base de datos de usuario (JCR) de la base de datos
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 1157366f-2cc5-46e4-8ec6-e66fe5d0a0f6
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Acceso a UGC con SRP {#accessing-ugc-with-srp}

## Acerca de SRP {#about-srp}

Todos los componentes y características de AEM Communities se basan en la [estructura de componentes sociales (SCF)](/help/communities/scf.md), que llama a la API de SocialResourceProvider para tener acceso al contenido generado por el usuario (UGC).

Antes de crear un sitio de la comunidad, el [proveedor de recursos de almacenamiento (SRP)](/help/communities/working-with-srp.md) debe estar configurado para seleccionar una implementación compatible con la [topología](/help/communities/topologies.md) subyacente. Las implementaciones de SRP se basan en tres opciones de almacenamiento:

1. [ASRP](/help/communities/asrp.md): almacenamiento de Adobe bajo demanda
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## Acerca del almacenamiento UGC {#about-ugc-storage}

AEM Lo que es importante saber acerca del almacenamiento de UGC es que, cuando un sitio está configurado para usar ASRP o MSRP, el UGC real no se almacena en el almacén de nodos [(JCR).](/help/sites-deploying/data-store-config.md)

Aunque puede haber nodos en JCR que sombrean el UGC para proporcionar metadatos útiles, estos nodos no se deben confundir con el UGC real.

Consulte [Información general sobre el proveedor de recursos de almacenamiento.](/help/communities/srp.md)

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

Los distintos SRP pueden tener diferentes idiomas de consulta nativos. Use los métodos del paquete [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) para ejecutar el idioma de consulta adecuado.

Para obtener más información, consulte [Search Essentials](/help/communities/search-implementation.md).

## Recursos {#resources}

* [Almacenamiento de contenido de la comunidad](/help/communities/working-with-srp.md): analiza las opciones de SRP disponibles para un almacén común de UGC
* [Resumen del proveedor de recursos de almacenamiento](/help/communities/srp.md) - introducción y descripción general del uso del repositorio
* [SRP y UGC Essentials](/help/communities/srp-and-ugc.md): métodos y ejemplos de utilidades SRP
* [Search Essentials](/help/communities/search-implementation.md): información esencial para buscar UGC
* [Refactorización de SocialUtils](/help/communities/socialutils.md): asignación de métodos de utilidad obsoletos a métodos de utilidad SRP actuales
