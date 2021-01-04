---
title: Topologías recomendadas para las comunidades
seo-title: Topologías recomendadas para las comunidades
description: Cómo abordar la administración de contenido generado por el usuario (UGC)
seo-description: Cómo abordar la administración de contenido generado por el usuario (UGC)
uuid: 4bc1c423-0ba9-4f2e-b11c-4d6824f45641
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: 46f135de-a0bf-451d-bdcc-fb29188250aa
translation-type: tm+mt
source-git-commit: 612d102b5925704ce459ad818554e487ec0d5355
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---


# Topologías recomendadas para las comunidades {#recommended-topologies-for-communities}

A partir de AEM Communities 6.1, se ha adoptado un enfoque único para gestionar el contenido generado por el usuario (UGC) enviado por los visitantes del sitio (miembros) desde el entorno de publicación.

Este enfoque difiere fundamentalmente de la forma en que la plataforma AEM gestiona el contenido del sitio que generalmente se administra desde el entorno de creación.

La plataforma AEM utiliza un almacén de nodos que replica el contenido del sitio del autor para publicarlo, mientras que AEM Communities utiliza un único almacén común para UGC que nunca se replica.

Para el almacén UGC común, es necesario elegir un [proveedor de recursos de almacenamiento (SRP)](working-with-srp.md). Las opciones recomendadas son:

* [DSRP - Proveedor de recursos de Almacenamiento de base de datos relacional](dsrp.md)
* [MSRP - Proveedor de recursos de Almacenamiento MongoDB](msrp.md)
* [ASRP - Proveedor de recursos de Almacenamiento de Adobe](asrp.md)

Otra opción de SRP, [JSRP - Proveedor de recursos de Almacenamiento JCR](jsrp.md), no admite un almacén UGC común para el autor y entornos de publicación para ambos accesos.

Requerir un almacén común resulta en las siguientes topologías recomendadas.

>[!NOTE]
>
>Para AEM Communities, [UGC nunca se replica](working-with-srp.md#ugc-never-replicated).
>
>Cuando la implementación no incluye un [almacén común](working-with-srp.md), UGC solo estará visible en la instancia de publicación o autor AEM en la que se introdujo.


>[!NOTE]
>
>Para obtener más información sobre la plataforma de AEM, consulte [Implementaciones recomendadas](../../help/sites-deploying/recommended-deploys.md) y [Introducción a la plataforma de AEM](../../help/sites-deploying/data-store-config.md).

## Para producción {#for-production}

El establecimiento de un almacén común para UGC es esencial y, por lo tanto, el despliegue subyacente depende de su capacidad de apoyar un almacén común.

Dos ejemplos:

1. Si el volumen previsto de UGC es alto y es posible una instancia local de MongoDB, la opción sería [MSRP](msrp.md).

1. Para un rendimiento óptimo del contenido de la página, la elección de [conjunto de servidores de publicación](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) y [ASRP](asrp.md) proporcionaría una escala óptima de UGC con operaciones relativamente simples.

Para ambos, la implementación puede estar basada en cualquier micronúcleo OAK.

Para elegir el almacén común apropiado, considere cuidadosamente las [características](working-with-srp.md#characteristics-of-srp-options) únicas de cada uno.

Para obtener más información sobre los microkernals de Oak, visite [Implementaciones recomendadas](../../help/sites-deploying/recommended-deploys.md).

### Granja de publicación TarMK {#tarmk-publish-farm}

Cuando la topología es un conjunto de servidores de publicación, los temas relevantes son:

* [Sincronización de usuarios](sync.md)
* [Administración de usuarios y grupos de usuarios](users.md)

### Recomendado: DSRP, MSRP o ASRP {#recommended-dsrp-msrp-or-asrp}

| MicroKernel | CONTENIDO DEL SITIO REPOSITORIO | CONTENTREPOSITORIO GENERADO POR EL USUARIO | PROVEEDOR DE RECURSOS DE almacenamiento | CONSERVACIÓN COMÚN |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| cualquiera | JCR | MySQL | DSRP | Sí |
| cualquiera | JCR | MongoDB | MSRP | Sí |
| cualquiera | JCR | Adobe de almacenamiento a pedido | ASRP | Sí |

### JSRP {#jsrp}


| Implementación | CONTENIDO DEL SITIO REPOSITORIO | CONTENTREPOSITORIO GENERADO POR EL USUARIO | PROVEEDOR DE RECURSOS DE almacenamiento | CONSERVACIÓN COMÚN |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| Granja TarMK (predeterminada) | JCR | JCR | JSRP | No |
| Oak Cluster | JCR | JCR | JSRP | Solo para entorno de publicación |

## Para desarrollo {#for-development}

Para entornos que no son de producción, [JSRP](jsrp.md) proporciona simplicidad en la configuración de un entorno de desarrollo con una instancia de autor y una instancia de publicación.

Si elige [ASRP](asrp.md), [DSRP](dsrp.md) o [MSRP](msrp.md) para producción, también es posible configurar un entorno de desarrollo similar utilizando almacenamiento a petición de Adobe o MongoDB. Para ver un ejemplo, consulte [HowTo Setup MongoDB for Demo](demo-mongo.md).

## Referencias {#references}

* [Sincronización de usuarios](sync.md)

   Analiza la sincronización de los datos de usuario entre las instancias del conjunto de publicaciones.

* [Administración de usuarios y grupos de usuarios](users.md)

   Explica las funciones de los usuarios y los grupos de usuarios en los entornos de creación y publicación.

* UGC [almacén común](working-with-srp.md)

   Describe el almacenamiento de contenido de comunidad independiente del contenido del sitio.

* [Almacenes de nodos y almacenes de datos](../../help/sites-deploying/data-store-config.md)

   Básicamente, el contenido del sitio se almacena en un almacén de nodos. Para Assets, se puede configurar un almacén de datos para almacenar datos binarios. Para Comunidades, se debe configurar un almacén común para seleccionar el SRP.

* [Elementos de almacenamiento](../../help/sites-deploying/storage-elements-in-aem-6.md)

   Describe las implementaciones de almacenamiento de dos nodos: Tar y MongoDB.
