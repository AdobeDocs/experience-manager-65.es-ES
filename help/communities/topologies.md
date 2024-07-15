---
title: Topologías recomendadas para comunidades
description: Cómo abordar la administración del contenido generado por el usuario (UGC)
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
exl-id: b6658330-d862-44e3-aac0-824fb91cd087
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 1%

---

# Topologías recomendadas para comunidades {#recommended-topologies-for-communities}

A partir de AEM Communities 6.1, se ha adoptado un enfoque único para la gestión del contenido generado por el usuario (UGC) enviado por los visitantes del sitio (miembros) desde el entorno de publicación.

AEM Este enfoque es fundamentalmente diferente de la forma en que la plataforma de la gestiona el contenido del sitio que, por lo general, se administra desde el entorno de creación.

AEM La plataforma de utiliza un almacén de nodos que replica el contenido del sitio desde el autor hasta la publicación, mientras que AEM Communities utiliza un único almacén común para UGC que nunca se replica.

Para el almacén UGC común, es necesario elegir un [proveedor de recursos de almacenamiento (SRP)](working-with-srp.md). Las opciones recomendadas son:

* [DSRP: proveedor de recursos de almacenamiento de base de datos relacional](dsrp.md)
* [MSRP: proveedor de recursos de almacenamiento de MongoDB](msrp.md)
* [ASRP: proveedor de recursos de almacenamiento de Adobe](asrp.md)

Otra opción de SRP, [JSRP - Proveedor de recursos de almacenamiento JCR](jsrp.md), no admite un almacén UGC común para los entornos de creación y publicación para el acceso a ambos.

Si se requiere un almacén común, se recomiendan las siguientes topologías.

>[!NOTE]
>
>Para AEM Communities, [UGC nunca se replicará](working-with-srp.md#ugc-never-replicated).
>
>AEM Cuando la implementación no incluye un [almacén común](working-with-srp.md), UGC solo será visible en la instancia de publicación o autor en la que se ingresó en la publicación o en la instancia de autor en la que se haya ingresado.
>

>[!NOTE]
>
>AEM AEM Para obtener más información acerca de la plataforma de, consulte [Implementaciones recomendadas](../../help/sites-deploying/recommended-deploys.md) e [Introducción a la plataforma de la](../../help/sites-deploying/data-store-config.md).

## Para producción {#for-production}

Es esencial establecer un almacén común para UGC y, por lo tanto, el despliegue subyacente depende de su capacidad para admitir un almacén común.

Dos ejemplos:

1. Si el volumen esperado de UGC es alto y es posible una instancia local de MongoDB, la opción sería [MSRP](msrp.md).

1. Para obtener un rendimiento óptimo del contenido de la página, la elección de [conjunto de servidores de publicación](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) y [ASRP](asrp.md) proporcionaría un escalado óptimo de UGC con operaciones relativamente sencillas.

Para ambos, la implementación puede basarse en cualquier microkernel de OAK.

Para elegir el almacén común apropiado, tenga en cuenta las [características](working-with-srp.md#characteristics-of-srp-options) únicas de cada uno.

Para obtener más información sobre los microkernals de Oak, visite [Implementaciones recomendadas](../../help/sites-deploying/recommended-deploys.md).

### TarMK Publish Farm {#tarmk-publish-farm}

Cuando la topología es un conjunto de servidores de publicación, los temas importantes relevantes son:

* [Sincronización de usuarios](sync.md)
* [Administración de usuarios y grupos de usuarios](users.md)

### Recomendado: DSRP, MSRP o ASRP {#recommended-dsrp-msrp-or-asrp}

| MicroKernel | REPOSITORIO DE CONTENIDO DEL SITIO | REPOSITORIO DE CONTENIDO GENERADO POR EL USUARIO | PROVEEDOR DE RECURSOS DE ALMACENAMIENTO | ALMACÉN COMÚN |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| cualquiera | JCR | MySQL | DSRP | Sí |
| cualquiera | JCR | MongoDB | MSRP | Sí |
| cualquiera | JCR | Adobe de almacenamiento bajo demanda | ASRP | Sí |

### JSRP {#jsrp}


| Implementación | REPOSITORIO DE CONTENIDO DEL SITIO | REPOSITORIO DE CONTENIDO GENERADO POR EL USUARIO | PROVEEDOR DE RECURSOS DE ALMACENAMIENTO | ALMACÉN COMÚN |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| Granja TarMK (predeterminada) | JCR | JCR | JSRP | No |
| Clúster Oak | JCR | JCR | JSRP | Sí solo para el entorno de publicación |

## Para desarrollo {#for-development}

En los entornos que no son de producción, [JSRP](jsrp.md) proporciona una configuración sencilla de un entorno de desarrollo con una instancia de autor y una instancia de publicación.

Si elige [ASRP](asrp.md), [DSRP](dsrp.md) o [MSRP](msrp.md) para producción, también es posible configurar un entorno de desarrollo similar usando almacenamiento bajo demanda de Adobe o MongoDB. Para ver un ejemplo, vea [Cómo configurar MongoDB para la demostración](demo-mongo.md).

## Referencias {#references}

* [Sincronización de usuarios](sync.md)

  Analiza la sincronización de datos de usuario entre instancias de conjuntos de servidores de publicación.

* [Administración de usuarios y grupos de usuarios](users.md)

  Describe las funciones de los usuarios y grupos de usuarios en los entornos de creación y publicación.

* UGC [almacén común](working-with-srp.md)

  Describe el almacenamiento del contenido de la comunidad aparte del contenido del sitio.

* [Almacenes de nodos y almacenes de datos](../../help/sites-deploying/data-store-config.md)

  Básicamente, el contenido del sitio se almacena en un almacén de nodos. Para Assets, se puede configurar un almacén de datos para almacenar datos binarios. Para las comunidades, se debe configurar un almacén común para seleccionar el SRP.

* [Elementos de almacenamiento](../../help/sites-deploying/storage-elements-in-aem-6.md)

  Describe las implementaciones de almacenamiento de dos nodos: Tar y MongoDB.
