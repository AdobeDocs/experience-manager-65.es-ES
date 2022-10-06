---
title: Topologías recomendadas para comunidades
seo-title: Recommended Topologies for Communities
description: Cómo abordar la gestión del contenido generado por el usuario (UGC)
seo-description: How to approach the handling of user-generated content (UGC)
uuid: 4bc1c423-0ba9-4f2e-b11c-4d6824f45641
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: 46f135de-a0bf-451d-bdcc-fb29188250aa
exl-id: b6658330-d862-44e3-aac0-824fb91cd087
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# Topologías recomendadas para comunidades {#recommended-topologies-for-communities}

A partir de AEM Communities 6.1, se ha adoptado un enfoque único para gestionar el contenido generado por el usuario (UGC) enviado por los visitantes del sitio (miembros) desde el entorno de publicación.

Este enfoque es fundamentalmente diferente de la forma en que la plataforma AEM gestiona el contenido del sitio que generalmente se administra desde el entorno de creación.

La plataforma AEM utiliza un almacén de nodos que replica el contenido del sitio de autor a publicación, mientras que AEM Communities utiliza un único almacén común para UGC que nunca se replica.

Para la tienda UGC común, es necesario elegir un [proveedor de recursos de almacenamiento (SRP)](working-with-srp.md). Las opciones recomendadas son:

* [DSRP - Proveedor de recursos de almacenamiento de bases de datos relacionales](dsrp.md)
* [MSRP - Proveedor de recursos de almacenamiento MongoDB](msrp.md)
* [ASRP: proveedor de recursos de almacenamiento de Adobe](asrp.md)

Otra opción de SRP, [JSRP: proveedor de recursos de almacenamiento JCR](jsrp.md), no admite un almacén UGC común para los entornos de autor y publicación para acceder a .

Requerir un almacén común resulta en las siguientes topologías recomendadas.

>[!NOTE]
>
>Para AEM Communities, [UGC nunca se replica](working-with-srp.md#ugc-never-replicated).
>
>Cuando la implementación no incluye un [tienda común](working-with-srp.md), UGC solo estará visible en la instancia de publicación o autor de AEM en la que se introdujo.

>[!NOTE]
>
>Para obtener más información sobre la plataforma AEM, consulte [Implementaciones recomendadas](../../help/sites-deploying/recommended-deploys.md) y [Introducción a la plataforma AEM](../../help/sites-deploying/data-store-config.md).

## Para producción {#for-production}

El establecimiento de un almacén común para UGC es esencial y, por lo tanto, el despliegue subyacente depende de su capacidad para prestar apoyo a un almacén común.

Dos ejemplos:

1. Si el volumen esperado de UGC es alto y una instancia local de MongoDB es posible, entonces la elección sería [MSRP](msrp.md).

1. Para un rendimiento óptimo del contenido de la página, la elección de un [publicar granja](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) y [ASRP](asrp.md) proporcionaría una escala óptima de UGC con operaciones relativamente sencillas.

Para ambos, la implementación puede estar basada en cualquier micronúcleo OAK.

Para elegir el almacén común apropiado, tenga en cuenta el [características](working-with-srp.md#characteristics-of-srp-options) de cada uno.

Para obtener más información sobre los microkernals de Oak, visite [Implementaciones recomendadas](../../help/sites-deploying/recommended-deploys.md).

### Granja de publicación TarMK {#tarmk-publish-farm}

Cuando la topología es una granja de servidores de publicación, los temas relevantes son:

* [Sincronización de usuarios](sync.md)
* [Administración de usuarios y grupos de usuarios](users.md)

### Recomendado: DSRP, MSRP o ASRP {#recommended-dsrp-msrp-or-asrp}

| MicroKernel | CONTENIDO DEL SITIO REPOSITORIO | CONTENIDO GENERADO POR EL USUARIO | PROVEEDOR DE RECURSOS DE ALMACENAMIENTO | CONSERVACIÓN COMÚN |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| cualquiera | JCR | MySQL | DSRP | Sí |
| cualquiera | JCR | MongoDB | MSRP | Sí |
| cualquiera | JCR | Adobe de almacenamiento según demanda | ASRP | Sí |

### JSRP {#jsrp}


| Implementación | CONTENIDO DEL SITIO REPOSITORIO | CONTENIDO GENERADO POR EL USUARIO | PROVEEDOR DE RECURSOS DE ALMACENAMIENTO | CONSERVACIÓN COMÚN |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| Granja TarMK (predeterminada) | JCR | JCR | JSRP | No |
| Oak Cluster | JCR | JCR | JSRP | Sí solo para el entorno de publicación |

## Para el desarrollo {#for-development}

Para entornos que no son de producción, [JSRP](jsrp.md) proporciona simplicidad en la configuración de un entorno de desarrollo con una instancia de autor y una instancia de publicación.

Si elige [ASRP](asrp.md), [DSRP](dsrp.md) o [MSRP](msrp.md) para la producción, también es posible configurar un entorno de desarrollo similar utilizando el almacenamiento bajo demanda de Adobe o MongoDB. Para ver un ejemplo, consulte [Configuración de MongoDB para demostración](demo-mongo.md).

## Referencias {#references}

* [Sincronización de usuarios](sync.md)

   Analiza la sincronización de los datos de usuario entre las instancias del conjunto de servidores de publicación.

* [Administración de usuarios y grupos de usuarios](users.md)

   Explica las funciones de los usuarios y grupos de usuarios en los entornos de autor y publicación.

* UGC [tienda común](working-with-srp.md)

   Describe el almacenamiento del contenido de la comunidad independiente del contenido del sitio.

* [Almacenes de nodos y almacenes de datos](../../help/sites-deploying/data-store-config.md)

   Básicamente, el contenido del sitio se almacena en un almacén de nodos. Para Assets, se puede configurar un almacén de datos para almacenar datos binarios. Para Communities, se debe configurar un almacén común para seleccionar el SRP.

* [Elementos de almacenamiento](../../help/sites-deploying/storage-elements-in-aem-6.md)

   Describe las implementaciones de almacenamiento de dos nodos: Tar y MongoDB.
