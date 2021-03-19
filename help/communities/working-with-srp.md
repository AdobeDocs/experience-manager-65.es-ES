---
title: 'SRP: Almacenamiento de contenido de la comunidad'
seo-title: 'SRP: Almacenamiento de contenido de la comunidad'
description: A partir de AEM Communities 6.1, el contenido generado por el usuario (UGC) se almacena en un único almacén común proporcionado por un proveedor de recursos de almacenamiento (SRP)
seo-description: A partir de AEM Communities 6.1, el contenido generado por el usuario (UGC) se almacena en un único almacén común proporcionado por un proveedor de recursos de almacenamiento (SRP)
uuid: d45e03c4-378b-4510-a6a0-d48c8cb879d9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6f13b21a-f4ef-4889-9b8e-4da3f846fa35
docset: aem65
role: Administrador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 0%

---


# SRP: Almacenamiento de contenido de la comunidad {#srp-community-content-storage}

## Introducción {#introduction}

A partir de AEM Communities 6.1, el contenido generado por el usuario (UGC) se almacena en un único almacén común proporcionado por un proveedor de recursos de almacenamiento (SRP). Existen varias opciones de SRP entre las que elegir, como ASRP, MSRP y JSRP.

A diferencia de las versiones anteriores, no hay una replicación inversa/avanzada de UGC en AEM instancias. En su lugar, el SRP hace que UGC sea directamente accesible para crear, leer, actualizar y eliminar operaciones (CRUD) desde todas las instancias de autor y publicación, con una excepción para JSRP.

A continuación se muestran las [características de cada opción de SRP](#characteristics-of-srp-options), que es información crucial para el proceso de decisión al elegir el SRP apropiado y la [implementación subyacente](/help/communities/topologies.md).

Para obtener más información sobre el uso de SRP para UGC, consulte [Información general del proveedor de recursos de almacenamiento](/help/communities/srp.md).

>[!NOTE]
>
>La SRP se aplica solo al contenido de la comunidad. No afecta al lugar en el que se almacena el contenido del sitio ([almacén de nodos](/help/sites-deploying/data-store-config.md)) y no afecta a la gestión segura del registro de usuarios, los perfiles de usuario y los grupos de usuarios entre AEM instancias (consulte también [Administración de datos de usuario](#managing-user-data)).

>[!CAUTION]
>
>A partir de AEM 6.1, [UGC nunca se replica](#ugc-never-replicated).
>
>Cuando la implementación no incluye un almacén común, como la topología predeterminada [JSRP](/help/communities/topologies.md#jsrp), UGC solo será visible en la instancia de autor o publicación de AEM en la que se introdujo. Solo si la topología incluye un clúster de publicación, el UGC estará visible en cualquier instancia de publicación.

## Características de las opciones de SRP {#characteristics-of-srp-options}

[ASRP: proveedor de recursos de almacenamiento de Adobe](/help/communities/asrp.md)

Con esta opción, el UGC se mantiene de forma remota en un servicio en la nube alojado y administrado por Adobe. Se requiere una licencia adicional y trabajar con un representante de cuentas para suministrar la cuenta para esa licencia específica. ASRP requiere:

* Un servicio de nube asociado que proporciona y admite Adobe para almacenar contenido de la comunidad.
* Elección de un centro de datos en una geografía específica (EE.UU., EMEA, APAC).

* Todo el acceso programático a UGC se realiza a través de la API de SRP.

ASRP es adecuado:

* Para la granja de publicación TarMK.
* Cuando no hay intención de invertir en almacenamiento local.

>[!NOTE]
>
>La carga de archivos adjuntos a anuncios (o comentarios) en ASRP tiene un límite de 50 MB.

[MSRP - Proveedor de recursos de almacenamiento MongoDB](/help/communities/msrp.md)

Con esta opción, el UGC se mantiene directamente en una instancia local de MongoDB.

El MSRP requiere:

* Instalación local con licencia de MongoDB para almacenar contenido de la comunidad.
* Instalación local de Apache Solr.
* Todo el acceso programático a UGC se realiza a través de la API de SRP.

ASRP es adecuado:

* Para una granja de publicación TarMK existente.
* Para un clúster MongoMK o RdbMK.
* Cuando se esperan grandes volúmenes de contenido de la comunidad.

[DSRP - Proveedor de recursos de almacenamiento de bases de datos relacionales](/help/communities/dsrp.md)

Con esta opción, el UGC se mantiene directamente en una instancia local de base de datos MySQL.

DSRP requiere:

* Instalación local de MySQL para almacenar contenido comunitario.
* Instalación local de Apache Solr.
* Todo el acceso programático a UGC se realiza a través de la API de SRP.

DSRP es adecuado:

* Para una granja de publicación TarMK existente.
* Para un clúster MongoMK o RdbMK.
* Cuando se esperan grandes volúmenes de contenido de la comunidad.

[JSRP: proveedor de recursos de almacenamiento JCR](/help/communities/jsrp.md)

Con la opción predeterminada, no hay ningún almacén común. El UGC solo se mantiene en el mismo repositorio JCR que la instancia de AEM en la que se introdujo.

JSRP:

* Almacena contenido de la comunidad en el repositorio JCR de la instancia de autor o publicación AEM en la que se publicó.
* Requiere que todo acceso programático a UGC se realice a través de la API de SRP.
* Requiere un clúster de publicación si se implementa más de una instancia de publicación (no hay ningún mecanismo de replicación entre instancias de publicación en una granja TarMK).
* la moderación solo se realiza en el entorno de publicación (no hay ningún mecanismo de replicación inversa/reenvío entre el autor y la publicación).
* Es mejor para desarrollo, demostraciones y capacitación.

## Configuración de SRP {#configuring-srp}

La especificación de la opción de almacenamiento predeterminada, basada en la implementación subyacente, se realiza a través de la [Consola de configuración de almacenamiento](/help/communities/srp-config.md).

Para obtener detalles de configuración de cada opción, consulte:

* [ASRP: proveedor de recursos de almacenamiento de Adobe](/help/communities/asrp.md)
* [MSRP - Proveedor de recursos de almacenamiento MongoDB](/help/communities/msrp.md)
* [DSRP - Proveedor de recursos de almacenamiento de bases de datos relacionales](/help/communities/dsrp.md)
* [JSRP: proveedor de recursos de almacenamiento JCR](/help/communities/jsrp.md)

Si no hay ninguna opción de almacenamiento seleccionada activamente, JSRP está habilitado de forma predeterminada.

## Información adicional {#additional-information}

### UGC nunca se replicó {#ugc-never-replicated}

En el entorno de creación, un autor crea contenido de página y lo replica en el entorno de publicación. Cuando una página incluye una función interactiva de AEM Communities, como comentarios, revisiones, foros, blogs o control de calidad, la interacción de los miembros (visitantes registrados en el sitio) en una instancia de publicación provoca que el contenido generado por el usuario (UGC) se introduzca en el entorno de publicación.

Anteriormente, el contenido de esta comunidad se replicaba de forma inversa en instancias de autor y de autor replicado en instancias de publicación. Era problemático mantener la coherencia entre AEM instancias con replicación inversa y avanzada.

A partir de AEM Communities 6.1, la necesidad de replicación de UGC se ha eliminado mediante el uso del almacenamiento compartido para UGC, como se describe anteriormente.

Mientras el contenido del sitio se replica, UGC nunca se replica.

### Administración de datos de usuario {#managing-user-data}

También son de interés para CommunitiesIes [*usuarios*, *grupos de usuarios* y *perfiles de usuario*](/help/communities/users.md). Estos datos relacionados con el usuario, cuando se crean y actualizan en el entorno de publicación, deben estar disponibles para otras instancias de publicación cuando la topología es un [conjunto de servidores de publicación](/help/sites-deploying/recommended-deploys.md#tarmk-farm).

A partir de AEM Communities 6.1, los datos relacionados con el usuario se sincronizan mediante la distribución Sling en lugar de la replicación. Para obtener más información, visite [Sincronización de usuarios](/help/communities/sync.md).

### Actualización a AEM Communities 6.5 {#upgrading-to-aem-communities}

Al actualizar a AEM 6.5 Communities, si es necesario conservar UGC preexistente, se deben tomar medidas en función de si la comunidad AEM 5.6.1 o AEM 6.0 utilizaba almacenamiento de Adobe bajo demanda o almacenamiento local de UGC.

Para obtener más información, visite [Actualización a AEM Communities 6.5](/help/communities/upgrade.md).
