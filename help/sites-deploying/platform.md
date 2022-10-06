---
title: Introducción a la plataforma AEM
seo-title: Introduction to the AEM Platform
description: Este artículo proporciona información general sobre la plataforma AEM y sus componentes más importantes.
seo-description: This article provides a general overview of the AEM platform and its most important components.
uuid: 214d4c49-1f5c-432c-a2c0-c1fbdceee716
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: fccf9a0f-ebab-45ab-8460-84c86b3c4192
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/introduction-to-oak
exl-id: 8ee5f4ff-648d-45ea-a51e-894cd4385e62
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# Introducción a la plataforma AEM{#introduction-to-the-aem-platform}

La plataforma AEM en AEM 6 está basada en Apache Jackrabbit Oak.

Apache Jackrabbit Oak es un esfuerzo para implementar un repositorio de contenido jerárquico escalable y de rendimiento para utilizarlo como la base de los sitios web modernos de nivel mundial y otras aplicaciones de contenido exigentes.

Es el sucesor de Jackrabbit 2 y es utilizado por AEM 6 como el backend predeterminado para su repositorio de contenido, CRX.

## Principios y objetivos del diseño {#design-principles-and-goals}

Oak implementa el [JSR-283](https://www.day.com/day/en/products/jcr/jsr-283.html) (JCR 2.0). Sus principales objetivos de diseño son:

* Mejor soporte para repositorios grandes
* Varios nodos de clúster distribuidos para alta disponibilidad
* Mejor rendimiento
* Compatibilidad con muchos nodos secundarios y niveles de control de acceso

## Concepto de arquitectura {#architecture-concept}

![chlimage_1-84](assets/chlimage_1-84.png)

### Almacenamiento {#storage}

El propósito de la capa de almacenamiento es:

* Implementar un modelo de árbol
* Conversión de almacenamiento en conectable
* Proporcionar un mecanismo de agrupación en clúster

### Oak Core {#oak-core}

El Oak Core agrega varias capas a la capa de almacenamiento:

* Controles de nivel de acceso
* Buscar e indexar
* Observación

### Oak JCR {#oak-jcr}

El objetivo principal del JCR de Oak es transformar la semántica de JCR en operaciones de árbol. También es responsable de:

* Implementación de la API de JCR
* Contiene enlaces de confirmación que implementan restricciones de JCR

Además, las implementaciones que no son de Java ahora son posibles y forman parte del concepto de JCR de Oak.

## Resumen del almacenamiento {#storage-overview}

La capa de almacenamiento Oak proporciona una capa de abstracción para el almacenamiento real del contenido.

Actualmente, hay dos implementaciones de almacenamiento disponibles en AEM6: **Almacenamiento de Tar** y **Almacenamiento MongoDB**.

### Almacenamiento de Tar {#tar-storage}

El almacenamiento Tar utiliza archivos tar. Almacena el contenido como varios tipos de registros dentro de segmentos más grandes. Los diarios se utilizan para realizar el seguimiento del estado más reciente del repositorio.

Existen varios principios clave de diseño en los que se basa:

* **Segmentos inmutables**

El contenido se almacena en segmentos que pueden tener un tamaño máximo de 256 KiB. Son inmutables, lo que facilita la caché de los segmentos a los que se accede con frecuencia y reduce los errores del sistema que pueden dañar el repositorio.

Cada segmento se identifica con un identificador único (UUID) y contiene un subconjunto continuo del árbol de contenido. Además, los segmentos pueden hacer referencia a otro contenido. Cada segmento mantiene una lista de UUID de otros segmentos a los que se hace referencia.

* **Localidad**

Los registros relacionados como un nodo y sus elementos secundarios inmediatos generalmente se almacenan en el mismo segmento. Esto hace que la búsqueda en el repositorio sea muy rápida y evita que la mayoría de los errores de caché de los clientes típicos que acceden a más de un nodo relacionado por sesión.

* **Compactación**

El formato de los registros está optimizado para reducir el tamaño y los costes de E/S y para que quepa el mayor contenido posible en las cachés.

### Almacenamiento de Mongo {#mongo-storage}

El almacenamiento MongoDB aprovecha MongoDB para compartir y agrupar. El árbol de repositorios se mantiene en una base de datos MongoDB donde cada nodo es un documento independiente.

Tiene varias particularidades:

* Revisiones

Para cada actualización (confirmación) del contenido, se crea una nueva revisión. Una revisión es básicamente una cadena que consta de tres elementos:

1. Marca de tiempo derivada de la hora del sistema en la que se generó el equipo
1. Un contador para distinguir revisiones creadas con la misma marca de tiempo
1. ID del nodo de clúster en el que se creó la revisión

* Ramas

Se admiten ramas, lo que permite al cliente realizar varios cambios y hacerlos visibles con una sola llamada de combinación.

* Documentos anteriores

El almacenamiento MongoDB agrega datos a un documento con cada modificación. Sin embargo, solo elimina los datos si se activa explícitamente una limpieza. Los datos antiguos se mueven cuando se alcanza un determinado umbral. Los documentos anteriores solo contienen datos inmutables, lo que significa que solo contienen revisiones comprometidas y fusionadas.

* Metadatos del nodo de clúster

Los datos sobre los nodos de clúster activos e inactivos se mantienen en la base de datos para facilitar las operaciones de clúster.

Una configuración típica de clúster de AEM con almacenamiento MongoDB:

![chlimage_1-85](assets/chlimage_1-85.png)

## ¿En qué se diferencia de Jackrabbit 2? {#what-is-different-from-jackrabbit}

Como Oak está diseñado para ser compatible con versiones anteriores del estándar JCR 1.0, casi no habrá cambios a nivel de usuario. Sin embargo, hay algunas diferencias notables que debe tener en cuenta al configurar una instalación de AEM basada en Oak:

* Oak no crea índices automáticamente. Por este motivo, será necesario crear índices personalizados cuando sea necesario.
* A diferencia de Jackrabbit 2, donde las sesiones siempre reflejan el estado más reciente del repositorio, con Oak una sesión refleja una vista estable del repositorio desde el momento en que se adquirió la sesión. Esto se debe al modelo MVCC en el que se basa Oak.
* Los hermanos del mismo nombre (SNS) no son compatibles con Oak.

## Otra documentación relacionada con la plataforma {#other-platform-related-documentation}

Para obtener más información sobre la plataforma AEM, consulte también los artículos siguientes:

* [Configuración de almacenes de nodos y almacenes de datos en AEM 6](/help/sites-deploying/data-store-config.md)
* [Consultas e indexación de Oak](/help/sites-deploying/queries-and-indexing.md)
* [Elementos de almacenamiento en AEM 6](/help/sites-deploying/storage-elements-in-aem-6.md)
* [AEM con MongoDB](/help/sites-deploying/aem-with-mongodb.md)
