---
title: Información general del proveedor de recursos de almacenamiento
seo-title: Storage Resource Provider Overview
description: Almacenamiento común para las comunidades
seo-description: Common storage for Communities
uuid: abdf4e5a-767b-428f-9aa4-0dc06819a26e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 63abeda4-6ea1-4b45-b188-f9c6b44ca0cd
exl-id: 5f313274-1a2a-4e83-9289-60a4729b99b4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 0%

---

# Información general del proveedor de recursos de almacenamiento {#storage-resource-provider-overview}

## Introducción {#introduction}

A partir de AEM Communities 6.1, el contenido de la comunidad, denominado comúnmente contenido generado por el usuario (UGC), se almacena en un único almacén común proporcionado por un [proveedor de recursos de almacenamiento](working-with-srp.md) (SRP).

Existen varias opciones de SRP, todas las cuales acceden a UGC a través de una nueva interfaz de AEM Communities, la [API de SocialResourceProvider](srp-and-ugc.md) (API de SRP), que incluye todas las operaciones de creación, lectura, actualización y eliminación (CRUD).

Todos los componentes de SCF se implementan utilizando la API de SRP, lo que permite desarrollar código sin tener conocimiento de las [topología subyacente](topologies.md) o ubicación de UGC.

***La API de SocialResourceProvider solo está disponible para clientes con licencia de AEM Communities.***

>[!NOTE]
>
>**Componentes personalizados**: Para los clientes con licencia de AEM Communities, la API de SRP está disponible para los desarrolladores de componentes personalizados con el fin de acceder a UGC independientemente de la topología subyacente. Consulte [Elementos esenciales de SRP y UGC](srp-and-ugc.md).

Consulte también lo siguiente:

* [Elementos esenciales de SRP y UGC](srp-and-ugc.md) - Métodos y ejemplos de utilidad SRP.
* [Acceso a UGC con SRP](accessing-ugc-with-srp.md) - Directrices de codificación.
* [Refactorización de SocialUtils](socialutils.md) - Asignación de métodos de utilidad obsoletos a los métodos de utilidad SRP actuales.

## Acerca del repositorio {#about-the-repository}

Para comprender el SRP, es útil comprender el papel del repositorio de AEM (OAK) en un sitio de comunidad de AEM.

**Repositorio de contenido Java (JCR)**
Este estándar define un modelo de datos y una interfaz de programación de aplicaciones ([API de JCR](https://jackrabbit.apache.org/jcr/jcr-api.html)) para repositorios de contenido. Combina características de file systems convencionales con las de bases de datos relacionales y agrega una serie de características adicionales que las aplicaciones de contenido a menudo necesitan.

Una implementación de JCR es el repositorio AEM, OAK.

**Apache Jackrabbit Oak (OAK)**
[OAK](../../help/sites-deploying/platform.md) es una implementación de JCR 2.0 que es un sistema de almacenamiento de datos diseñado específicamente para aplicaciones centradas en el contenido. Es un tipo de base de datos jerárquica diseñada para datos no estructurados y semiestructurados. El repositorio almacena no solo el contenido orientado al usuario, sino también todo el código, las plantillas y los datos internos utilizados por la aplicación. La IU para acceder al contenido es [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md).

Tanto JCR como OAK suelen utilizarse para hacer referencia al repositorio de AEM.

Después de desarrollar el contenido del sitio en el entorno de creación privado, debe copiarse en el entorno de publicación público. Esto a menudo se realiza mediante una operación denominada *[replicación](deploy-communities.md#replication-agents-on-author)*. Esto sucede bajo el control del autor/desarrollador/administrador.

Para UGC, el contenido lo introducen los visitantes del sitio registrados (miembros de la comunidad) en el entorno de publicación pública. Esto sucede aleatoriamente.

A los efectos de la gestión y la presentación de informes, es útil tener acceso a UGC desde el entorno de creación privado. Con SRP, el acceso a UGC desde el autor es más coherente y eficaz, ya que no es necesario realizar la replicación inversa de la publicación al autor.

## Acerca de SRP {#about-srp}

Cuando UGC se guarda en almacenamiento compartido, existe una única instancia de contenido miembro a la que se puede acceder, en la mayoría de las implementaciones, desde los entornos de autor y publicación. Independientemente de la elección de SRP (MSRP, ASRP, JSRP), se debe acceder a todos mediante programación con la API de SRP.

>[!NOTE]
>
>Consulte [Elementos esenciales de SRP y UGC](srp-and-ugc.md) para obtener un código de muestra y detalles adicionales.
>
>Consulte [Acceso a UGC con SRP](accessing-ugc-with-srp.md) para conocer las prácticas recomendadas al codificar.

### ASRP {#asrp}

En el caso de ASRP, UGC no se almacena en JCR, sino en un servicio en la nube alojado y administrado por Adobe. El UGC almacenado en ASRP no se puede ver con el CRXDE Lite ni se puede acceder a él mediante la API de JCR.

Consulte [ASRP: proveedor de recursos de almacenamiento de Adobe](asrp.md).

Los desarrolladores no pueden acceder directamente a UGC.

ASRP utiliza la nube de Adobe para las consultas.

### MSRP {#msrp}

En el caso del MSRP, UGC no se almacena en JCR, sino en MongoDB. El UGC almacenado en MSRP no se puede ver con el CRXDE Lite ni se puede acceder a él mediante la API de JCR.

Consulte [MSRP - Proveedor de recursos de almacenamiento MongoDB](msrp.md).

Aunque el MSRP es comparable al ASRP, como todas las instancias de servidor AEM acceden al mismo UGC, es posible utilizar herramientas comunes para acceder directamente al UGC almacenado en MongoDB.

MSRP utiliza Solr para las consultas.

### JSRP {#jsrp}

JSRP es el proveedor predeterminado para acceder a todo UGC en una única instancia de AEM. Proporciona la capacidad de experimentar rápidamente AEM Communities 6.1 sin necesidad de configurar MSRP o ASRP.

Consulte [JSRP: proveedor de recursos de almacenamiento JCR](jsrp.md).

En el caso de JSRP, mientras que UGC se almacena en JCR y se puede acceder a él a través de la API de CRXDE Lite y JCR, se recomienda encarecidamente que la API de JCR no se utilice nunca para hacerlo, de lo contrario, los cambios futuros podrían afectar al código personalizado.

Además, el repositorio para los entornos de autor y publicación no se comparte. Aunque un clúster de instancias de publicación resulta en un repositorio de publicación compartido, el UGC introducido en la publicación no será visible para el autor, por lo que no se puede administrar el UGC desde el autor. UGC solo se mantiene en el repositorio AEM (JCR) de la instancia en la que se introdujo.

JSRP utiliza los índices Oak para las consultas.

## Acerca de los nodos de sombra en JCR {#about-shadow-nodes-in-jcr}

Los nodos de sombra, que imitan la ruta a UGC, existen en el repositorio local para cumplir dos propósitos:

1. [Control de acceso (ACL)](#for-access-control-acls)
1. [Recursos no existentes (NER)](#for-non-existing-resources-ners)

Independientemente de la implementación de SRP, el UGC real *no será visible en la misma ubicación que el nodo de sombra.

### Para control de acceso (ACL) {#for-access-control-acls}

Algunas implementaciones de SRP, como ASRP y MSRP, almacenan contenido de la comunidad en bases de datos que no proporcionan verificación de ACL. Los nodos de sombra proporcionan una ubicación en el repositorio local al que se pueden aplicar las ACL.

Con la API de SRP, todas las opciones de SRP realizan la misma comprobación de la ubicación de sombra antes de todas las operaciones de CRUD.

La comprobación ACL utiliza un método de utilidad que devuelve una ruta adecuada para comprobar los permisos aplicados al UGC del recurso.

Consulte [Elementos esenciales de SRP y UGC](srp-and-ugc.md) para código de muestra.

### Para recursos no existentes (NER) {#for-non-existing-resources-ners}

Algunos componentes de Communities pueden incluirse en un script y, por lo tanto, es necesario un nodo direccionable de Sling para admitir funciones de Communities. [Componentes incluidos](scf.md#add-or-include-a-communities-component) se denominan recursos no existentes.

Los nodos de sombra proporcionan una ubicación direccionable de Sling en el repositorio.

>[!CAUTION]
>
>Como el nodo de sombra tiene varios usos, la presencia de un nodo de sombra sí *not* implican que el componente es un NER.

### Ubicación de almacenamiento {#storage-location}

A continuación, se muestra un ejemplo de un nodo de sombra que utiliza la variable [Componente Comentarios](http://localhost:4502/content/community-components/en/comments.html) en el [Guía de componentes de comunidad](components-guide.md):

* El componente existe en el repositorio local en:

   `/content/community-components/en/comments/jcr:content/content/includable/comments`

* El nodo de sombra correspondiente existe en el repositorio local en:

   `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

No se encontrará ningún UGC en el nodo de sombra.

El comportamiento predeterminado es configurar nodos de sombra en una instancia de publicación siempre que se haga referencia al subárbol correspondiente para una lectura o escritura.

A modo de ejemplo, supongamos que la implementación es [MSRP](msrp.md) con una granja de publicación TarMK.

Cuando [miembro](users.md) publica UGC en pub1 (almacenado en MongoDB), los nodos sombra se crean en JCR en pub1.

La primera vez que se lee el UGC en pub2, si no hay nada configurado, el comportamiento predeterminado es crear los nodos de sombra.

Si no se desea el comportamiento predeterminado, debe configurarse en la instancia de autor y redirigirse a todas las instancias de publicación, que suele ser un proceso manual.
