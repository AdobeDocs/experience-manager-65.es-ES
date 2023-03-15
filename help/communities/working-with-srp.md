---
title: 'SRP: almacenamiento de contenido de la comunidad'
seo-title: SRP - Community Content Storage
description: A partir de AEM Communities 6.1, el contenido generado por el usuario (UGC) se almacena en un único almacén común proporcionado por un proveedor de recursos de almacenamiento (SRP)
seo-description: As of AEM Communities 6.1, user generated content (UGC) is stored in a single, common store provided by a storage resource provider (SRP)
uuid: d45e03c4-378b-4510-a6a0-d48c8cb879d9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6f13b21a-f4ef-4889-9b8e-4da3f846fa35
docset: aem65
role: Admin
exl-id: e29aae44-67be-43d2-8004-c986412d9e63
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---

# SRP: almacenamiento de contenido de la comunidad {#srp-community-content-storage}

## Introducción {#introduction}

A partir de AEM Communities 6.1, el contenido generado por el usuario (UGC) se almacena en un único almacén común proporcionado por un proveedor de recursos de almacenamiento (SRP). Hay varias opciones de SRP entre las que elegir, como ASRP, MSRP y JSRP.

AEM A diferencia de las versiones anteriores, no hay replicación inversa/hacia delante de UGC en todas las instancias de la. En su lugar, el SRP hace que UGC sea directamente accesible para las operaciones de creación, lectura, actualización y eliminación (CRUD) desde todas las instancias de autor y publicación, con una excepción para JSRP.

A continuación se muestran los [características de cada opción de SRP](#characteristics-of-srp-options), que es información crucial para el proceso de decisión al elegir el SRP adecuado y [implementación subyacente](/help/communities/topologies.md).

Para obtener más información sobre el uso de SRP para UGC, consulte [Resumen del proveedor de recursos de almacenamiento](/help/communities/srp.md).

>[!NOTE]
>
>SRP solo se aplica al contenido de la comunidad. No afecta a dónde se almacena el contenido del sitio ([almacén de nodos](/help/sites-deploying/data-store-config.md)AEM ), y no afecta a la gestión segura del registro de usuarios, perfiles de usuarios y grupos de usuarios entre instancias de (consulte también [Administración de datos de usuario](#managing-user-data)).

>[!CAUTION]
>
>AEM A partir de la versión 6.1, [UGC nunca se replica](#ugc-never-replicated).
>
>Cuando la implementación no incluye un almacén común, como el predeterminado [JSRP](/help/communities/topologies.md#jsrp) AEM , UGC solo será visible en la instancia de publicación o autor en la que se haya ingresado el código de acceso de la publicación o el autor de la. Solo si la topología incluye un clúster de publicación, el UGC será visible en cualquier instancia de publicación.

## Características de las opciones de SRP {#characteristics-of-srp-options}

[ASRP: proveedor de recursos de almacenamiento de Adobe](/help/communities/asrp.md)

Con esta opción, el UGC se mantiene de forma remota en un servicio en la nube alojado y administrado por el Adobe. Requiere una licencia adicional y trabajar con un representante de cuentas para aprovisionar la cuenta de esa licencia específica. ASRP requiere:

* Un servicio en la nube asociado proporcionado y admitido por el Adobe para almacenar contenido de la comunidad.
* Elección de un centro de datos en una ubicación geográfica específica (EE. UU., EMEA, APAC).

* Todo el acceso programático a UGC se puede realizar a través de la API de SRP.

ASRP es adecuado:

* Para el conjunto de servidores de publicación TarMK.
* Cuando no hay intención de invertir en almacenamiento local.

>[!NOTE]
>
>La carga de archivos adjuntos a publicaciones (o comentarios) en ASRP tiene un límite de 50 MB.

[MSRP: proveedor de recursos de almacenamiento de MongoDB](/help/communities/msrp.md)

Con esta opción, el UGC se mantiene directamente en una instancia local de MongoDB.

El MSRP requiere:

* Una instalación local con licencia de MongoDB para almacenar contenido de la comunidad.
* Una instalación local de Apache Solr.
* Todo el acceso programático a UGC se puede realizar a través de la API de SRP.

ASRP es adecuado:

* Para una granja de servidores de publicación TarMK existente.
* Para un clúster de MongoMK o RdbMK.
* Cuando se esperan grandes volúmenes de contenido de la comunidad.

[DSRP: proveedor de recursos de almacenamiento de base de datos relacional](/help/communities/dsrp.md)

Con esta opción, el UGC se mantiene directamente en una instancia de base de datos MySQL local.

DSRP requiere:

* Una instalación local de MySQL para almacenar contenido de la comunidad.
* Una instalación local de Apache Solr.
* Todo el acceso programático a UGC se puede realizar a través de la API de SRP.

DSRP es adecuado:

* Para una granja de servidores de publicación TarMK existente.
* Para un clúster de MongoMK o RdbMK.
* Cuando se esperan grandes volúmenes de contenido de la comunidad.

[JSRP: proveedor de recursos de almacenamiento de JCR](/help/communities/jsrp.md)

Con la opción predeterminada, no hay ningún almacén común. AEM El UGC solo se mantiene en el mismo repositorio JCR que la instancia de en la que se introdujo.

JSRP:

* AEM Almacena el contenido de la comunidad en el repositorio JCR de la instancia de autor o publicación de la en la que se publicó.
* Requiere que todo acceso programático a UGC se realice a través de la API de SRP.
* Requiere un clúster de publicación si se implementa más de una instancia de publicación (no hay ningún mecanismo de replicación entre las instancias de publicación de una granja de TarMK).
* la moderación solo se realiza en el entorno de publicación (no hay mecanismo de replicación inversa/hacia delante entre autor y publicación).
* Es mejor para el desarrollo, las demostraciones y la formación.

## Configuración de SRP {#configuring-srp}

La especificación de la opción de almacenamiento predeterminado, basada en la implementación subyacente, se realiza mediante la variable [Consola de configuración de almacenamiento](/help/communities/srp-config.md).

Para obtener detalles de configuración de cada opción, consulte:

* [ASRP: proveedor de recursos de almacenamiento de Adobe](/help/communities/asrp.md)
* [MSRP: proveedor de recursos de almacenamiento de MongoDB](/help/communities/msrp.md)
* [DSRP: proveedor de recursos de almacenamiento de base de datos relacional](/help/communities/dsrp.md)
* [JSRP: proveedor de recursos de almacenamiento de JCR](/help/communities/jsrp.md)

Si no se selecciona ninguna opción de almacenamiento de forma activa, JSRP está habilitado de forma predeterminada.

## Información adicional {#additional-information}

### UGC nunca replicado {#ugc-never-replicated}

En el entorno de creación, un autor crea contenido de página y lo replica en el entorno de publicación. Cuando una página incluye una función interactiva de AEM Communities, como comentarios, revisiones, foros, blogs o controles de calidad, la interacción por parte de los miembros (visitantes del sitio conectados) en una instancia de publicación resulta en contenido generado por el usuario (UGC) introducido en el entorno de publicación.

Anteriormente, este contenido de la comunidad se replicaba de forma inversa en instancias de autor y de autor replicado en instancias de publicación. AEM Resultaba problemático mantener la coherencia entre las instancias de con la replicación inversa y hacia delante.

A partir de AEM Communities 6.1, la necesidad de replicación de UGC se ha eliminado utilizando el almacenamiento compartido para UGC, como se ha descrito anteriormente.

Mientras el contenido del sitio se duplique, UGC nunca se duplicará.

### Administración de datos de usuario {#managing-user-data}

También son de interés para CommunitiesIes [*usuarios*, *grupos de usuarios*, y *perfiles de usuario*](/help/communities/users.md). Estos datos relacionados con el usuario, cuando se crean y actualizan en el entorno de publicación, deben estar disponibles para otras instancias de publicación cuando la topología es una variable [publicar conjunto de servidores](/help/sites-deploying/recommended-deploys.md#tarmk-farm).

A partir de AEM Communities 6.1, los datos relacionados con el usuario se sincronizan mediante la distribución de Sling en lugar de la replicación. Para obtener más información, visite [Sincronización de usuarios](/help/communities/sync.md).

### Actualización a AEM Communities 6.5 {#upgrading-to-aem-communities}

AEM AEM AEM Al actualizar a comunidades de la versión 6.5 de la comunidad de, si es necesario conservar el UGC preexistente, se deben tomar medidas en función de si el UGC de la comunidad de la versión 5.6.1 o la versión 6.0 de la comunidad de la versión se utiliza para almacenar el Adobe bajo demanda o el UGC de la versión local.

Para obtener más información, visite [Actualización a AEM Communities 6.5](/help/communities/upgrade.md).
