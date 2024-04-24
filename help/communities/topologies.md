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

Para la tienda UGC común, es necesario elegir una [proveedor de recursos de almacenamiento (SRP)](working-with-srp.md). Las opciones recomendadas son:

* [DSRP: proveedor de recursos de almacenamiento de base de datos relacional](dsrp.md)
* [MSRP: proveedor de recursos de almacenamiento de MongoDB](msrp.md)
* [ASRP: proveedor de recursos de almacenamiento de Adobe](asrp.md)

Otra opción de SRP, [JSRP: proveedor de recursos de almacenamiento de JCR](jsrp.md), no admite un almacén UGC común para los entornos de creación y publicación tanto para el acceso como para el acceso.

Si se requiere un almacén común, se recomiendan las siguientes topologías.

>[!NOTE]
>
>Para AEM Communities, [UGC nunca se replica](working-with-srp.md#ugc-never-replicated).
>
>Cuando la implementación no incluye un [almacén común](working-with-srp.md)AEM , UGC solo estará visible en la instancia de publicación o autor en la que se haya introducido el código de acceso del usuario (UGC) en la que se haya publicado el código.
>

>[!NOTE]
>
>AEM Para obtener más información sobre la plataforma de la, consulte [Implementaciones recomendadas](../../help/sites-deploying/recommended-deploys.md) y [AEM Introducción a la plataforma de](../../help/sites-deploying/data-store-config.md).

## Para producción {#for-production}

Es esencial establecer un almacén común para UGC y, por lo tanto, el despliegue subyacente depende de su capacidad para admitir un almacén común.

Dos ejemplos:

1. Si el volumen esperado de UGC es alto y es posible una instancia local de MongoDB, la opción sería [MSRP](msrp.md).

1. Para obtener un rendimiento óptimo del contenido de la página, elija una [publicar conjunto de servidores](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) y [ASRP](asrp.md) proporcionaría una escala óptima de UGC con operaciones relativamente sencillas.

Para ambos, la implementación puede basarse en cualquier microkernel de OAK.

Para elegir el almacén común adecuado, tenga en cuenta la variable única [características](working-with-srp.md#characteristics-of-srp-options) de cada uno.

Para obtener más información sobre los microkernals de Oak, visite [Implementaciones recomendadas](../../help/sites-deploying/recommended-deploys.md).

### Granja de publicación TarMK {#tarmk-publish-farm}

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
| Oak Cluster | JCR | JCR | JSRP | Sí solo para el entorno de publicación |

## Para desarrollo {#for-development}

Para entornos que no son de producción, [JSRP](jsrp.md) permite configurar de forma sencilla un entorno de desarrollo con una instancia de autor y una instancia de publicación.

Si elige [ASRP](asrp.md), [DSRP](dsrp.md) o [MSRP](msrp.md) para la producción, también es posible configurar un entorno de desarrollo similar utilizando el almacenamiento bajo demanda de Adobe o MongoDB. Para ver un ejemplo, consulte [Cómo configurar MongoDB para la demostración](demo-mongo.md).

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
