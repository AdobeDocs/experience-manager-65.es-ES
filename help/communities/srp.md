---
title: Resumen del proveedor de recursos de almacenamiento
description: Almacenamiento común para las comunidades
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 5f313274-1a2a-4e83-9289-60a4729b99b4
source-git-commit: e161c37544c3391607cbe495644f3353b9f77fe3
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 0%

---

# Resumen del proveedor de recursos de almacenamiento {#storage-resource-provider-overview}

## Introducción {#introduction}

A partir de Adobe Experience Manager AEM () Communities 6.1, el contenido de la comunidad, comúnmente denominado contenido generado por el usuario (UGC), se almacena en un único almacén común proporcionado por un [proveedor de recursos de almacenamiento](working-with-srp.md) (SRP).

Existen varias opciones de SRP, todas las cuales acceden a UGC a través de una nueva interfaz de AEM Communities, la [API SocialResourceProvider](srp-and-ugc.md) (API de SRP), que incluye todas las operaciones de creación, lectura, actualización y eliminación (CRUD).

Todos los componentes de SCF se implementan mediante la API de SRP, lo que permite desarrollar código sin conocer ninguno de los dos [topología subyacente](topologies.md) o la ubicación de UGC.

***La API de SocialResourceProvider solo está disponible para los clientes con licencia de AEM Communities.***

>[!NOTE]
>
>**Componentes personalizados**: Para los clientes con licencia de AEM Communities, la API de SRP está disponible para los desarrolladores de componentes personalizados para acceder a UGC independientemente de la topología subyacente. Consulte [SRP y UGC Essentials](srp-and-ugc.md).

Consulte también lo siguiente:

* [SRP y UGC Essentials](srp-and-ugc.md) - Métodos y ejemplos de la utilidad SRP.
* [Acceso a UGC con SRP](accessing-ugc-with-srp.md) - Directrices de codificación.
* [Refactorización de SocialUtils](socialutils.md) : Asignación de métodos de utilidad obsoletos a los métodos de utilidad SRP actuales.

## Acerca del repositorio {#about-the-repository}

AEM AEM Para comprender el SRP, es útil comprender el papel del repositorio de la (Oak) en un sitio de comunidad de la.

**Repositorio de contenido Java™ (JCR)**
Este estándar define un modelo de datos y una interfaz de programación de aplicaciones ([API JCR](https://jackrabbit.apache.org/jcr/jcr-api.html)) para repositorios de contenido. Combina las características de los sistemas de archivos convencionales con las de las bases de datos relacionales y agrega varias características adicionales que las aplicaciones de contenido suelen necesitar.

AEM Una implementación de JCR es el repositorio de, Oak.

**Apache Jackrabbit Oak**
[Oak](../../help/sites-deploying/platform.md) es una implementación de JCR 2.0 que es un sistema de almacenamiento de datos diseñado para aplicaciones centradas en el contenido. Es un tipo de base de datos jerárquica diseñada para datos no estructurados y semiestructurados. El repositorio almacena no solo el contenido orientado al usuario, sino también todo el código, las plantillas y los datos internos utilizados por la aplicación. La interfaz de usuario para acceder al contenido es [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md).

AEM Tanto JCR como Oak se utilizan generalmente para hacer referencia al repositorio de.

Después de desarrollar el contenido del sitio en el entorno de creación privado, debe copiarse en el entorno de publicación público. A menudo, esto se lleva a cabo mediante una operación llamada *[réplica](deploy-communities.md#replication-agents-on-author)*. Esto sucede bajo el control del autor, desarrollador o administrador.

Para UGC, el contenido lo introducen visitantes registrados del sitio (miembros de la comunidad) en el entorno de publicación público. Esto sucede al azar.

Para fines de administración y creación de informes, es útil tener acceso a UGC desde el entorno de creación privado. Con SRP, el acceso a UGC desde el autor es más coherente y eficaz, ya que la replicación inversa de la publicación al autor no es necesaria.

## Acerca de SRP {#about-srp}

Cuando UGC se guarda en un almacenamiento compartido, hay una sola instancia de contenido miembro a la que, en la mayoría de las implementaciones, se puede acceder desde los entornos de creación y publicación. Independientemente de la opción de SRP (MSRP, ASRP, JSRP), se debe acceder a todos mediante programación con la API de SRP.

>[!NOTE]
>
>Consulte [SRP y UGC Essentials](srp-and-ugc.md) para obtener código de ejemplo y detalles adicionales.
>
>Consulte [Acceso a UGC con SRP](accessing-ugc-with-srp.md) para conocer las prácticas recomendadas al codificar.

### ASRP {#asrp}

Si hay ASRP, UGC no se almacena en JCR, sino que se almacena en un servicio en la nube alojado y administrado por el Adobe. No se puede ver con CRXDE Lite ni acceder a los UGC almacenados en ASRP mediante la API de JCR.

Consulte [ASRP: proveedor de recursos de almacenamiento de Adobe](asrp.md).

Los desarrolladores no pueden acceder directamente al UGC.

ASRP utiliza la nube de Adobe para las consultas.

### MSRP {#msrp}

Si existe, MSRP, UGC no se almacena en JCR, sino en MongoDB. No se puede ver con CRXDE Lite ni acceder a los UGC almacenados en MSRP mediante la API JCR.

Consulte [MSRP: proveedor de recursos de almacenamiento de MongoDB](msrp.md).

AEM Aunque el MSRP es comparable al ASRP, ya que todas las instancias de servidor de acceden al mismo UGC, es posible utilizar herramientas comunes para acceder directamente al UGC almacenado en MongoDB.

MSRP utiliza Solr para las consultas.

### JSRP {#jsrp}

AEM JSRP es el proveedor predeterminado para acceder a todos los UGC en una sola instancia de. Permite experimentar rápidamente AEM Communities 6.1 sin necesidad de configurar MSRP o ASRP.

Consulte [JSRP: proveedor de recursos de almacenamiento de JCR](jsrp.md).

Si hay JSRP, mientras que UGC está almacenado en JCR, y accesible a través de CRXDE Lite y de la API JCR, se recomienda no utilizar nunca la API JCR para hacerlo, de lo contrario los cambios futuros pueden afectar al código personalizado.

Además, el repositorio de los entornos de creación y publicación no se comparte. Mientras que un clúster de instancias de publicación genera un repositorio de publicación compartido, el UGC introducido en la publicación no será visible en el autor, por lo que no es posible administrar el UGC desde el autor. AEM UGC solo persiste en el repositorio de la instancia en la que se ingresó, es decir, en el repositorio de la instancia en la que se ingresó.

JSRP utiliza los índices de Oak para las consultas.

## Acerca de los nodos de sombra en JCR {#about-shadow-nodes-in-jcr}

Los nodos sombreados, que imitan la ruta a UGC, existen en el repositorio local para servir dos propósitos:

1. [Control de acceso (ACL)](#for-access-control-acls)
1. [Recursos no existentes (NER)](#for-non-existing-resources-ners)

Independientemente de la implementación de SRP, el UGC real *no *será visible en la misma ubicación que el nodo en la sombra.

### Para el control de acceso (ACL) {#for-access-control-acls}

Algunas implementaciones de SRP, como ASRP y MSRP, almacenan contenido de la comunidad en bases de datos que no proporcionan verificación de ACL. Los nodos sombreados proporcionan una ubicación en el repositorio local a la que se pueden aplicar las ACL.

Con la API de SRP, todas las opciones de SRP realizan la misma comprobación de la ubicación en la sombra antes de todas las operaciones de CRUD.

La comprobación ACL utiliza un método de utilidad que devuelve una ruta adecuada para comprobar los permisos aplicados al UGC del recurso.

Consulte [SRP y UGC Essentials](srp-and-ugc.md) para el código de ejemplo.

### Para recursos no existentes (NER) {#for-non-existing-resources-ners}

Algunos componentes de Communities se pueden incluir dentro de un script y, por lo tanto, requieren un nodo direccionable de Sling para admitir las funciones de Communities. [Componentes incluidos](scf.md#add-or-include-a-communities-component) se denominan recursos no existentes (NER).

Los nodos sombreados proporcionan una ubicación direccionable de Sling en el repositorio.

>[!CAUTION]
>
>Como el nodo en la sombra tiene varios usos, la presencia de un nodo en la sombra sí lo hace *no* implicar que el componente es un NER.

### Ubicación de almacenamiento {#storage-location}

A continuación se muestra un ejemplo de un nodo en la sombra, con el [Componente Comentarios](http://localhost:4502/content/community-components/en/comments.html) en el [Guía de componentes de la comunidad](components-guide.md):

* El componente existe en el repositorio local en:

  `/content/community-components/en/comments/jcr:content/content/includable/comments`

* El nodo central correspondiente existe en el repositorio local en:

  `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

No se ha encontrado ningún UGC en el nodo de la sombra.

El comportamiento predeterminado es configurar nodos en la sombra en una instancia de publicación siempre que se haga referencia al subárbol relevante para una lectura o escritura.

Por ejemplo, supongamos que la implementación es [MSRP](msrp.md) con una granja de servidores de publicación TarMK.

Cuando un [miembro](users.md) publica UGC en pub1 (almacenado en MongoDB), los nodos sombreados se crean en JCR en pub1.

La primera vez que se lee el UGC en pub2, si no hay nada configurado, el comportamiento predeterminado es crear los nodos en la sombra.

Si se desea un comportamiento distinto del predeterminado, debe configurarse en la instancia de autor y revertirse a todas las instancias de publicación, lo que suele ser un proceso manual.
