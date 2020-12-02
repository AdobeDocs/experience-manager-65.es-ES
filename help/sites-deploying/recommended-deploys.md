---
title: Implementaciones recomendadas
seo-title: Implementaciones recomendadas
description: Este artículo describe las topologías recomendadas para AEM.
seo-description: Este artículo describe las topologías recomendadas para AEM.
uuid: bc638121-c531-43eb-9ec6-3283a33519f8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 66d351e1-87f1-4006-bf8a-3cbbd33db9ed
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '1802'
ht-degree: 0%

---


# Implementaciones recomendadas{#recommended-deployments}

>[!NOTE]
>
>Esta página se refiere a las topologías recomendadas para AEM. Para obtener más información sobre las capacidades de clustering y cómo configurarlas, consulte la [documentación de la API de Apache Sling Discovery](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html).

Los microkernels actúan como gestores de persistencia a partir del AEM 6.2. La elección de una para adaptarse a sus necesidades depende del propósito de su instancia y del tipo de implementación que esté considerando.

Los siguientes ejemplos pretenden indicar cuáles son los usos recomendados en las configuraciones de AEM más comunes.

## Escenarios de implementación {#deployment-scenarios}

### Instancia única de TarMK {#single-tarmk-instance}

En este escenario, una sola instancia de TarMK se ejecuta en un único servidor.

**Ésta es la implementación predeterminada para instancias de autor.**

![chlimage_1-15](assets/chlimage_1-15.png)

Las ventajas:

* Simples
* Fácil mantenimiento
* Buen rendimiento

Los inconvenientes:

* No escalable más allá de los límites de la capacidad del servidor
* Sin capacidad de conmutación por error

### TarMK Cold Standby {#tarmk-cold-standby}

Una instancia de TarMK actúa como instancia principal. El repositorio del primario se replica en un sistema de failover en espera.

El mecanismo de espera en frío también se puede utilizar como una copia de seguridad porque el repositorio completo se replica constantemente en el servidor de conmutación por error. El servidor de conmutación por error se está ejecutando en modo de espera en frío, lo que significa que sólo se está ejecutando HttpReceiver de la instancia.

![chlimage_1-16](assets/chlimage_1-16.png)

Las ventajas:

* Simplicidad
* Mantenimiento
* Actuación
* Conmutación por error

Los inconvenientes:

* No escalable más allá de los límites de la capacidad del servidor
* Un servidor está inactivo la mayor parte del tiempo
* La conmutación por error no es automática. Debe detectarse externamente antes de que el sistema de conmutación por error pueda inicio las solicitudes de servicio.

>[!NOTE]
>
>Para obtener más información sobre cómo configurar AEM con TarMK Cold Standby, consulte [este](/help/sites-deploying/tarmk-cold-standby.md) artículo.

>[!NOTE]
>
>La implementación en frío y en espera en este ejemplo de TarMK requiere que las instancias principal y en espera tengan una licencia independiente, ya que existe una replicación constante en el servidor de failover. Para obtener más información acerca de las licencias, consulte los [Términos generales de licencias de Adobe](https://www.adobe.com/legal/terms/enterprise-licensing.html).

### Granja TarMK {#tarmk-farm}

Se ejecutan varias instancias de Oak cada una con una instancia de TarMK. Los repositorios TarMK son independientes y deben mantenerse sincronizados.

Mantener los repositorios sincronizados se proporciona con el hecho de que el servidor de creación está publicando el mismo contenido para cada miembro del conjunto de servidores. Para obtener más información, consulte [Replicación](/help/sites-deploying/replication.md).

Para AEM Communities, el contenido generado por el usuario (UGC) nunca se replica. Para obtener soporte para UGC en una granja TarMK, consulte [consideraciones para AEM Communities](#considerations-for-aem-communities).

**Ésta es la implementación predeterminada para entornos de publicación.**

![chlimage_1-17](assets/chlimage_1-17.png)

Las ventajas:

* Actuación
* Escalabilidad para el acceso de lectura
* Conmutación por error

### Clúster Oak con failover MongoMK para alta disponibilidad en un solo centro de datos {#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter}

Este enfoque implica que varias instancias de Oak tienen acceso a un conjunto de réplicas de MongoDB dentro de un solo centro de datos, lo que en realidad crea un clúster activo-activo para el entorno de creación de AEM. Los conjuntos de réplicas en MongoDB se utilizan para proporcionar alta disponibilidad y redundancia en el evento de un fallo de hardware o de red.

![chlimage_1-18](assets/chlimage_1-18.png)

Las ventajas:

* Capacidad de escalar horizontalmente con nuevas instancias de creación de AEM
* Alta disponibilidad, redundancia y failover automatizado de la capa de datos

Los inconvenientes:

* El rendimiento puede ser menor que con TarMK en algunos casos

### Clúster Oak con failover MongoMK en varios centros de datos {#oak-cluster-with-mongomk-failover-across-multiple-datacenters}

Este enfoque implica que varias instancias de Oak tienen acceso a un conjunto de réplicas de MongoDB en varios centros de datos, lo que en realidad crea un clúster activo-activo para el entorno de creación de AEM. Con múltiples centros de datos, la replicación de MongoDB proporciona la misma alta disponibilidad y redundancia, pero ahora incluye la capacidad de manejar una interrupción en el centro de datos.

![oakclustermongofailover2datacenter](assets/oakclustermongofailover2datacenters.png)

Las ventajas:

* Capacidad de escalar horizontalmente con nuevas instancias de creación de AEM
* Alta disponibilidad, redundancia y failover automatizado de la capa de datos (incluidas las interrupciones del centro de datos)

>[!NOTE]
>
>En el diagrama anterior, AEM Server 3 y AEM Server 4 se presentan con un estado inactivo, suponiendo una latencia de red entre los servidores AEM del Centro de datos 2 y el nodo principal MongoDB del Centro de datos 1 que es superior al requisito documentado [aquí](/help/sites-deploying/aem-with-mongodb.md#checklists). Si la latencia máxima es compatible con los requisitos, por ejemplo mediante el uso de zonas de disponibilidad, los servidores de AEM del Centro de datos 2 también pueden estar activos, lo que crea un clúster de AEM activo-activo en varios centros de datos.

>[!NOTE]
>
>Para obtener información adicional sobre los conceptos arquitectónicos de MongoDB descritos en esta sección, consulte [Replicación de MongoDB](https://docs.mongodb.org/manual/replication/).

## Micronúcleos: cuál utilizar {#microkernels-which-one-to-use}

La regla básica que se debe tener en cuenta al elegir entre los dos microneles disponibles es que TarMK está diseñado para el rendimiento, mientras que MongoMK se utiliza para la escalabilidad.

Puede utilizar estas matrices de decisión para establecer cuál es el mejor tipo de implementación que se adapte a sus necesidades.

Adobe recomienda encarecidamente que TarMK sea la tecnología de persistencia predeterminada utilizada por los clientes en todos los escenarios de implementación, tanto para las instancias de AEM Author como para Publish, excepto en los casos de uso descritos a continuación.

### Excepciones para elegir AEM MongoMK sobre TarMK en instancias de autor {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-author-instances}

La razón principal para elegir el servidor de persistencia MongoMK sobre TarMK es escalar las instancias horizontalmente. Esto significa tener dos o más instancias de autor activas ejecutándose en todo momento y usando MongoDB como sistema de almacenamiento de persistencia. La necesidad de ejecutar más de una instancia de autor se debe en general al hecho de que la CPU y la capacidad de memoria de un único servidor, que admite todas las actividades de creación concurrentes, ya no son sostenibles.

Es casi imposible predecir cuál será el modelo exacto de concurrencia después de que se active un nuevo sitio. Por lo tanto, Adobe recomienda considerar los siguientes criterios al evaluar si se debe utilizar MongoMK y dos o más nodos activos de Author:

1. Número de usuarios con nombre conectados en un día: en miles o más.
1. Número de usuarios simultáneos: en cientos o más.
1. Volumen de ingestas de recursos por día: en cientos de miles o más.
1. Volumen de las ediciones de página por día: en cientos de miles o más (incluyendo actualizaciones automatizadas a través de Multi Site Manager o ingestas de fuentes de noticias, por ejemplo).
1. Volumen de búsquedas por día: en decenas de miles o más.

>[!NOTE]
>
>Se puede utilizar el Día duro para evaluar el rendimiento de la aplicación del cliente en el contexto de la configuración de hardware implementada. Encontrará más información sobre esta herramienta disponible [aquí](/help/sites-developing/tough-day.md).

Una implementación mínima con MongoDB suele incluir la siguiente topología:

* Conjunto de réplicas MongoDB que consta de un nodo primario, dos nodos secundarios con cada una de las instancias de MongoDB que se ejecutan en una zona de disponibilidad con una latencia inferior a 15 milisegundos en cada nodo;
* Un clúster de instancias de autor con un nodo de encabezado, un nodo que no es de encabezado y ambos activos en todo momento, con cada una de las instancias de autor ejecutándose en cada uno de los centros de datos, donde se ejecutan las instancias principal y secundaria de MongoDB.

Además, se recomienda configurar el almacén de datos en un sistema de archivos compartido o Amazon S3, de modo que los recursos o los archivos binarios no se almacenen en MongoDB. Esto garantizará un rendimiento óptimo dentro de la implementación.

Una de las ventajas adicionales de implementar un conjunto de réplicas MongoDB con un clúster de dos o más instancias de autor es tener un escenario de recuperación automatizada con tiempo de inactividad mínimo en caso de que se produzcan instancias de autor, una réplica de MongoDB o una falla completa del centro de datos. Sin embargo, la elección de MongoMK sobre TarMK no debe estar únicamente motivada por el requerimiento de recuperación, ya que TarMK también puede proporcionar una solución de downtime mínima con un mecanismo de failover controlado.

Si no se espera que los criterios anteriores se cumplan durante los primeros dieciocho meses de implementación, se recomienda implementar primero AEM mediante TarMK, luego volver a evaluar la configuración en una fecha posterior cuando se apliquen los criterios anteriores y, finalmente, determinar si desea permanecer en TarMK o migrar a MongoMK.

### Excepciones para elegir AEM MongoMK sobre TarMK en instancias de publicación {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-publish-instances}

No se recomienda implementar MongoMK para instancias de publicación. El nivel de publicación de la implementación casi siempre se implementa como un conjunto de instancias de publicación completamente independientes que ejecutan TarMK, que se mantienen sincronizadas al replicar contenido de las instancias de creación. Esta arquitectura de &quot;nada compartido&quot;, adecuada a las instancias de publicación, permite que la implementación del nivel de publicación se escale horizontalmente de forma lineal. La topología del conjunto de servidores también ofrece la ventaja de aplicar cualquier actualización o actualización para publicar instancias de forma sucesiva, de modo que cualquier cambio en el nivel de publicación no requerirá tiempo de inactividad.

Esto no se aplica a AEM Communities que utiliza clústeres MongoMK en el nivel de publicación siempre que haya más de un editor. Si elige JSRP (consulte [Almacenamiento de contenido de la comunidad](/help/communities/working-with-srp.md)), entonces sería adecuado un clúster MongoMK, como cualquier clúster de publicación independientemente del MK elegido, como MongoDB o RDB.

### Requisitos previos y Recommendations al implementar AEM con MongoMK {#prerequisites-and-recommendations-when-deploying-aem-with-mongomk}

Hay un conjunto de requisitos previos y recomendaciones disponibles si está considerando una implementación MongoMK para AEM:

**Requisitos previos obligatorios para implementaciones de MongoDB:**

1. La arquitectura de implementación y el tamaño de MongoDB deben formar parte de la implementación del proyecto con la ayuda de los arquitectos de Adobe Consulting o MongoDB que estén familiarizados con AEM;
1. La experiencia de MongoDB debe estar presente en el equipo del socio o del cliente para tener confianza en poder mantener y mantener un entorno de MongoDB existente o nuevo;
1. Puede elegir implementar la versión comercial o de código abierto de MongoDB (AEM admite ambos), pero debe adquirir un contrato de mantenimiento y soporte de MongoDB directamente de MongoDB Inc;
1. Las arquitecturas e infraestructuras generales de AEM y MongoDB deben estar bien definidas y validadas por un arquitecto AEM Adobe;
1. Debe revisar el modelo de soporte para AEM implementaciones que incluyen MongoDB.

**Recomendaciones sólidas para implementaciones de MongoDB:**

* Consulte el [artículo](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager) de MongoDB para Adobe Experience Manager;
* Revise la producción de MongoDB [lista de comprobación](https://docs.mongodb.org/manual/administration/production-checklist/);
* Asista a una clase de certificación en MongoDB disponible en línea [aquí](https://university.mongodb.com/).

>[!NOTE]
>
>Para todas las preguntas adicionales sobre estas directrices, requisitos previos y recomendaciones, póngase en contacto con [Adobe Customer Care](https://helpx.adobe.com/es/marketing-cloud/contact-support.html).

### Consideraciones para AEM Communities {#considerations-for-aem-communities}

Para los sitios que planeen implementar [AEM Communities](/help/communities/overview.md), se recomienda [elegir una implementación](/help/communities/working-with-srp.md#characteristicsofstorageoptions) optimizada para administrar UGC anunciados por miembros de la comunidad desde el entorno de publicación.

Al utilizar un [almacén común](/help/communities/working-with-srp.md), no es necesario replicar UGC entre el autor y otras instancias de publicación para obtener una vista coherente del UGC.

A continuación se muestra un conjunto de matrices decisorias que pueden ayudarle a elegir el mejor tipo de persistencia para la implementación:

#### Elección del tipo de implementación para instancias de autor {#choosing-the-deployment-type-for-author-instances}

![chlimage_1-19](assets/chlimage_1-19.png)

#### Elección del tipo de implementación para instancias de publicación {#choosing-the-deployment-type-for-publish-instances}

![chlimage_1-20](assets/chlimage_1-20.png)

>[!NOTE]
>
>MongoDB es un software de terceros y no está incluido en el paquete de licencias de AEM. Para obtener más información, consulte la página [Política de licencias de MongoDB](https://www.mongodb.org/about/licensing/).
>
>Para aprovechar al máximo su implementación de AEM, Adobe recomienda que se le otorgue la licencia de la versión MongoDB Enterprise para beneficiarse de la asistencia profesional.
>
>La licencia incluye un conjunto de réplicas estándar, compuesto por una instancia primaria y dos instancias secundarias que se pueden usar para la implementación de publicación o del autor.
>
>Si desea ejecutar tanto la creación como la publicación en MongoDB, deberá adquirir dos licencias independientes.
>
>Para obtener más información, consulte la página [MongoDB para Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).

