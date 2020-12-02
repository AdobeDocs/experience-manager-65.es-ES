---
title: Introducción a la Plataforma AEM
seo-title: Introducción a la Plataforma AEM
description: Este artículo proporciona una visión general de la plataforma de AEM y sus componentes más importantes.
seo-description: Este artículo proporciona una visión general de la plataforma de AEM y sus componentes más importantes.
uuid: 214d4c49-1f5c-432c-a2c0-c1fbdceee716
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: fccf9a0f-ebab-45ab-8460-84c86b3c4192
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/introduction-to-oak
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 0%

---


# Introducción a la Plataforma AEM{#introduction-to-the-aem-platform}

La plataforma AEM en AEM 6 está basada en Apache Jackrabbit Oak.

Apache Jackrabbit Oak es un esfuerzo para implementar un repositorio de contenido jerárquico escalable y de rendimiento para utilizarlo como la base de los sitios Web de clase mundial y otras aplicaciones de contenido exigentes.

Es el sucesor de Jackrabbit 2 y es usado por AEM 6 como el servidor predeterminado para su repositorio de contenido, CRX.

## Principios y objetivos del diseño {#design-principles-and-goals}

Oak implementa la especificación [JSR-283](https://www.day.com/day/en/products/jcr/jsr-283.html) (JCR 2.0). Sus principales objetivos de diseño son:

* Mejor soporte para repositorios grandes
* Varios nodos de clúster distribuidos para alta disponibilidad
* Mejor rendimiento
* Compatibilidad con muchos nodos secundarios y niveles de Control de acceso

## Concepto de arquitectura {#architecture-concept}

![chlimage_1-84](assets/chlimage_1-84.png)

### Almacenamiento {#storage}

El propósito de la capa de Almacenamiento es:

* Implementar un modelo de árbol
* Conversión de almacenamiento en conectable
* Proporcionar un mecanismo de agrupación en clúster

### Oak Core {#oak-core}

El Oak Core agrega varias capas a la capa de almacenamiento:

* Controles de nivel de acceso
* Búsqueda e indexación
* Observación

### Oak JCR {#oak-jcr}

El principal objetivo del JCR Oak es transformar la semántica JCR en operaciones de árbol. También es responsable de:

* Implementación de la API de JCR
* Contener enlaces de confirmación que implementan restricciones de JCR

Además, las implementaciones que no son de Java ahora son posibles y forman parte del concepto de JCR de Oak.

## Información general de almacenamiento {#storage-overview}

La capa de almacenamiento Oak proporciona una capa de abstracción para el almacenamiento real del contenido.

Actualmente, hay dos implementaciones de almacenamiento disponibles en AEM6: **Almacenamiento Tar** y **Almacenamiento MongoDB**.

### Almacenamiento Tar {#tar-storage}

El almacenamiento Tar utiliza archivos tar. Almacena el contenido como varios tipos de registros dentro de segmentos más grandes. Los historiales se utilizan para rastrear el estado más reciente del repositorio.

Existen varios principios de diseño clave sobre los que se construyó:

* **Segmentos inmutables**

El contenido se almacena en segmentos que pueden tener un tamaño de hasta 256 KiB. Son inmutables, lo que facilita la caché de los segmentos a los que se accede con frecuencia y reduce los errores del sistema que pueden dañar el repositorio.

Cada segmento se identifica mediante un identificador único (UUID) y contiene un subconjunto continuo del árbol de contenido. Además, los segmentos pueden hacer referencia a otro contenido. Cada segmento mantiene una lista de UUID de otros segmentos a los que se hace referencia.

* **Localidad**

Los registros relacionados, como un nodo y sus elementos secundarios inmediatos, generalmente se almacenan en el mismo segmento. Esto hace que la búsqueda en el repositorio sea muy rápida y evita la mayoría de errores de caché para clientes típicos que acceden a más de un nodo relacionado por sesión.

* **Compactación**

El formato de los registros está optimizado para reducir los costes de E/S y ajustar el contenido en las cachés lo más posible.

### Almacenamiento Mongo {#mongo-storage}

El almacenamiento MongoDB aprovecha MongoDB para compartir y agrupar. El árbol del repositorio se mantiene en una base de datos MongoDB donde cada nodo es un documento independiente.

Tiene varias particularidades:

* Revisiones

Para cada actualización (confirmación) del contenido, se crea una nueva revisión. Una revisión es básicamente una cadena que consta de tres elementos:

1. Marca de hora derivada de la hora del sistema del equipo en el que se generó
1. Un contador para distinguir las revisiones creadas con la misma marca de tiempo
1. El identificador del nodo de clúster en el que se creó la revisión

* Ramas

Se admiten ramas, lo que permite al cliente realizar varios cambios y hacerlos visibles con una sola llamada de combinación.

* Documentos anteriores

El almacenamiento MongoDB agrega datos a un documento con cada modificación. Sin embargo, solo elimina datos si se activa una limpieza de forma explícita. Los datos antiguos se mueven cuando se alcanza un determinado umbral. Los documentos anteriores solo contienen datos inmutables, lo que significa que solo contienen revisiones confirmadas y combinadas.

* Metadatos del nodo de clúster

Los datos sobre los nodos de clúster activos e inactivos se conservan en la base de datos para facilitar las operaciones de clúster.

Una configuración de clúster AEM típica con almacenamiento MongoDB:

![chlimage_1-85](assets/chlimage_1-85.png)

## ¿Qué es diferente a Jackrabbit 2? {#what-is-different-from-jackrabbit}

Dado que Oak está diseñado para ser compatible con el estándar JCR 1.0, casi no habrá cambios en el nivel de usuario. Sin embargo, hay algunas diferencias notables que debe tener en cuenta al configurar una instalación de AEM basada en Oak:

* Oak no crea índices automáticamente. Debido a esto, los índices personalizados deberán crearse cuando sea necesario.
* A diferencia de Jackrabbit 2, donde las sesiones siempre reflejan el estado más reciente del repositorio, con Oak una sesión refleja una vista estable del repositorio desde el momento en que se adquirió la sesión. Esto se debe al modelo MVCC en el que se basa Oak.
* Los hermanos del mismo nombre (SNS) no son compatibles con Oak.

## Documentación relacionada con otras plataformas {#other-platform-related-documentation}

Para obtener más información sobre la plataforma AEM, consulte también los artículos siguientes:

* [Configuración de almacenes de nodos y almacenes de datos en AEM 6](/help/sites-deploying/data-store-config.md)
* [Consultas de roble e indexación](/help/sites-deploying/queries-and-indexing.md)
* [Elementos de almacenamiento en AEM 6](/help/sites-deploying/storage-elements-in-aem-6.md)
* [AEM con MongoDB](/help/sites-deploying/aem-with-mongodb.md)

