---
title: Implementaciones recomendadas
description: AEM En este artículo se describen las topologías recomendadas para la creación de informes de.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: baec7fc8-d48c-4bc6-b12b-4bf4eff695ea
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1759'
ht-degree: 2%

---

# Implementaciones recomendadas{#recommended-deployments}

>[!NOTE]
>
>AEM Esta página hace referencia a las topologías recomendadas para la creación de informes de. Para obtener más información sobre las capacidades de agrupación en clúster y cómo configurarlas, consulte la [Documentación de la API de Apache Sling Discovery](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html).

AEM Los microKernels actúan como administradores de persistencia a partir de la versión 6.2 de la. La elección de una que se ajuste a sus necesidades depende del propósito de su instancia y del tipo de implementación que esté considerando.

AEM Los siguientes ejemplos están pensados para indicar cuáles son sus usos recomendados en las configuraciones de administración más comunes de los dispositivos de administración de la.

## Escenarios de implementación {#deployment-scenarios}

### Instancia de TarMK única {#single-tarmk-instance}

En esta situación, se ejecuta una sola instancia de TarMK en un solo servidor.

**Esta es la implementación predeterminada para las instancias de autor.**

![chlimage_1-15](assets/chlimage_1-15.png)

Las ventajas:

* Sencillo
* Fácil mantenimiento
* Buen rendimiento

Los inconvenientes:

* No escalable más allá de los límites de la capacidad del servidor
* Sin capacidad de failover

### TarMK en espera fría {#tarmk-cold-standby}

Una instancia de TarMK actúa como instancia principal. El repositorio del principal se replica en un sistema de failover en espera.

El mecanismo de espera en frío también se puede utilizar como copia de seguridad porque el repositorio completo se replica constantemente en el servidor de conmutación por error. El servidor de conmutación por error se está ejecutando en modo de espera en frío, lo que significa que sólo se está ejecutando el HttpReceiver de la instancia.

![chlimage_1-16](assets/chlimage_1-16.png)

Las ventajas:

* Simplicidad
* Mantenimiento
* Rendimiento
* Failover

Los inconvenientes:

* No escalable más allá de los límites de la capacidad del servidor
* Un servidor está inactivo la mayor parte del tiempo
* La conmutación por error no es automática. Debe detectarse externamente antes de que el sistema de conmutación por error pueda iniciar el servicio de solicitudes.

>[!NOTE]
>
>AEM Para obtener más información sobre cómo configurar el con el modo de espera pasiva de TarMK, consulte [esta](/help/sites-deploying/tarmk-cold-standby.md) artículo.

>[!NOTE]
>
>La implementación en modo de espera en frío en este ejemplo de TarMK requiere que las instancias primaria y en espera tengan licencia por separado, ya que hay una replicación constante en el servidor de conmutación por error. Para obtener más información sobre las licencias, consulte la [Adobe Términos generales de licencia](https://www.adobe.com/legal/terms/enterprise-licensing.html).

### Granja TarMK {#tarmk-farm}

Varias instancias de Oak se ejecutan cada una con una instancia de TarMK. Los repositorios TarMK son independientes y deben estar sincronizados.

Mantener los repositorios sincronizados se proporciona con el hecho de que el servidor de creación publica el mismo contenido en cada miembro de la granja. Para obtener más información, consulte [Replicación](/help/sites-deploying/replication.md).

Para AEM Communities, el contenido generado por el usuario (UGC) nunca se duplica. Para admitir UGC en una granja TarMK, consulte [consideraciones para AEM Communities](#considerations-for-aem-communities).

**Esta es la implementación predeterminada para los entornos de publicación.**

![chlimage_1-17](assets/chlimage_1-17.png)

Las ventajas:

* Rendimiento
* Escalabilidad para acceso de lectura
* Failover

### Clúster Oak con failover MongoMK para alta disponibilidad en un solo centro de datos {#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter}

AEM Este enfoque implica varias instancias de Oak que acceden a un conjunto de réplicas de MongoDB dentro de un solo centro de datos, lo que de hecho crea un clúster activo-activo para el entorno de creación de la. Los conjuntos de réplicas de MongoDB se utilizan para proporcionar alta disponibilidad y redundancia en caso de un error de hardware o de red.

![chlimage_1-18](assets/chlimage_1-18.png)

Las ventajas:

* AEM Capacidad de escalar horizontalmente con nuevas instancias de autor de
* Alta disponibilidad, redundancia y failover automatizado de la capa de datos

Los inconvenientes:

* El rendimiento puede ser menor que con TarMK en algunos casos

### Clúster Oak con failover MongoMK en varios centros de datos {#oak-cluster-with-mongomk-failover-across-multiple-datacenters}

AEM Este enfoque implica varias instancias de Oak que acceden a un conjunto de réplicas de MongoDB en varios centros de datos, lo que de hecho crea un clúster activo-activo para el entorno de creación de la. Con varios centros de datos, la replicación MongoDB proporciona la misma alta disponibilidad y redundancia, pero ahora incluye la capacidad de gestionar una interrupción del centro de datos.

![oakclustermongofailover2datacenters](assets/oakclustermongofailover2datacenters.png)

Las ventajas:

* AEM Capacidad de escalar horizontalmente con nuevas instancias de autor de
* Alta disponibilidad, redundancia y failover automatizado de la capa de datos (incluidas las interrupciones del centro de datos)

>[!NOTE]
>
>AEM AEM AEM En el diagrama anterior, el servidor de 3 y el servidor de 4 se presentan con un estado inactivo suponiendo una latencia de red entre los servidores de la red del centro de datos 2 y el nodo principal de MongoDB del centro de datos 1 que es superior al requisito documentado [aquí](/help/sites-deploying/aem-with-mongodb.md#checklists). AEM AEM Si la latencia máxima es compatible con los requisitos, por ejemplo, mediante el uso de zonas de disponibilidad, los servidores de datos del centro de datos 2 también pueden estar activos, lo que crea un clúster de datos activo-activo en varios centros de datos.

>[!NOTE]
>
>Para obtener información adicional sobre los conceptos arquitectónicos de MongoDB descritos en esta sección, consulte [Replicación de MongoDB](https://docs.mongodb.org/manual/replication/).

## Microkernels: cuál utilizar {#microkernels-which-one-to-use}

La regla básica que debe tenerse en cuenta al elegir entre los dos micro núcleos disponibles es que TarMK está diseñado para el rendimiento, mientras que MongoMK se utiliza para la escalabilidad.

Puede utilizar estas matrices de decisión para establecer cuál es el mejor tipo de implementación que se adapta a sus necesidades.

Adobe AEM recomienda encarecidamente que TarMK sea la tecnología de persistencia predeterminada utilizada por los clientes en todos los escenarios de implementación, tanto para las instancias de autor de como de publicación, excepto en los casos de uso descritos a continuación.

### AEM Excepciones para elegir MongoMK en lugar de TarMK en instancias de autor {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-author-instances}

La razón principal para elegir el backend de persistencia MongoMK sobre TarMK es escalar las instancias horizontalmente. Esto significa tener dos o más instancias de autor activas ejecutándose en todo momento y usar MongoDB como sistema de almacenamiento de persistencia. La necesidad de ejecutar más de una instancia de autor se debe generalmente al hecho de que la capacidad de CPU y memoria de un solo servidor, que admite todas las actividades de creación simultáneas, ya no es sostenible.

Es casi imposible predecir cuál será el modelo de concurrencia exacto después de que se publique un nuevo sitio. Por lo tanto, Adobe recomienda tener en cuenta los siguientes criterios al evaluar si se debe utilizar MongoMK y dos o más nodos activos de Author:

1. Número de usuarios con nombre conectados en un día: en miles o más.
1. Número de usuarios simultáneos: en cientos o más.
1. Volumen de ingestas de recursos por día: en cientos de miles o más.
1. Volumen de ediciones de página al día: en cientos de miles o más (incluidas actualizaciones automatizadas a través del Administrador de varios sitios o ingestas de fuentes de noticias, por ejemplo).
1. Volumen de búsquedas por día: en decenas de miles o más.

>[!NOTE]
>
>Tough Day se puede utilizar para evaluar el rendimiento de la aplicación del cliente en el contexto de la configuración de hardware implementada. Encontrará más información sobre esta herramienta [aquí](/help/sites-developing/tough-day.md).

Una implementación mínima con MongoDB suele incluir la siguiente topología:

* Un conjunto de réplicas de MongoDB que consta de un nodo principal, dos nodos secundarios con cada una de las instancias de MongoDB que se ejecutan en una zona de disponibilidad con una latencia inferior a 15 milisegundos en cada nodo;
* Clúster de instancias de autor con un nodo maestro, un nodo no maestro y ambos activos en todo momento, con cada una de las instancias de autor en ejecución en cada uno de los centros de datos, donde se ejecutan las instancias principales y secundarias de MongoDB.

Además, es muy recomendable configurar el almacén de datos en un sistema de archivos compartido o Amazon S3, de modo que los recursos o binarios no se almacenen en MongoDB. Esto garantizará un rendimiento óptimo dentro de la implementación.

Una de las ventajas adicionales de implementar un conjunto de réplicas MongoDB con un clúster de dos o más instancias de autor es tener un escenario de recuperación automatizada con un tiempo de inactividad mínimo si hay instancias de autor, una réplica MongoDB o un error completo del centro de datos. Sin embargo, la elección de MongoMK sobre TarMK no debe ser impulsada únicamente por el requisito de recuperación, ya que TarMK también puede proporcionar una solución de tiempo de inactividad mínima con un mecanismo de failover controlado.

AEM Si no se espera que los criterios anteriores se cumplan durante los primeros 18 meses de implementación, se recomienda primero implementar mediante TarMK, luego volver a evaluar la configuración en una fecha posterior cuando se apliquen los criterios anteriores y, finalmente, determinar si debe permanecer en TarMK o migrar a MongoMK.

### AEM Excepciones para elegir MongoMK en lugar de TarMK en las instancias de publicación de los datos {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-publish-instances}

No se recomienda implementar MongoMK para instancias de publicación. El nivel de publicación de la implementación casi siempre se implementa como una granja de instancias de publicación completamente independientes que ejecutan TarMK, que se mantienen sincronizadas replicando contenido de las instancias de autor. Esta arquitectura de &quot;no se ha compartido nada&quot;, propia de las instancias de publicación, permite la implementación del nivel de publicación para escalar horizontalmente de forma lineal. La topología de conjunto de servidores también ofrece la ventaja de aplicar cualquier actualización o actualización a las instancias de publicación de forma gradual, de modo que cualquier cambio en el nivel de publicación no requerirá ningún tiempo de inactividad.

Esto no se aplica a AEM Communities que utiliza clústeres MongoMK en el nivel de publicación siempre que haya más de un editor. Si elige JSRP (consulte [Almacenamiento de contenido de comunidad](/help/communities/working-with-srp.md)), sería adecuado un clúster de MongoMK, como cualquier clúster de lado de publicación independientemente del MK elegido, como MongoDB o RDB.

### Requisitos previos y Recommendations AEM al implementar la implementación de la aplicación con MK {#prerequisites-and-recommendations-when-deploying-aem-with-mongomk}

AEM Hay disponible un conjunto de requisitos previos y recomendaciones si está considerando una implementación de MongoMK para lo siguiente:

**Requisitos previos obligatorios para implementaciones de MongoDB:**

1. La arquitectura y el tamaño de la implementación de MongoDB deben formar parte de la implementación del proyecto con la ayuda de la asesoría de Adobe AEM o de arquitectos de MongoDB familiarizados con el uso de la tecnología de la base de datos de la plataforma de datos de la plataforma de datos de;
1. La experiencia de MongoDB debe estar presente dentro del equipo del socio o cliente para tener confianza en poder mantener y mantener un entorno de MongoDB existente o nuevo;
1. AEM Puede elegir implementar la versión comercial o de código abierto de MongoDB (admite ambas), pero debe adquirir un contrato de mantenimiento y soporte de MongoDB directamente de MongoDB Inc;
1. AEM Las arquitecturas e infraestructuras generales y de MongoDB deben ser bien definidas y validadas por un arquitecto de Adobe AEM
1. AEM Revise el modelo de soporte para implementaciones de que incluyan MongoDB.

**Recomendaciones sólidas para implementaciones de MongoDB:**

* Consulte MongoDB para Adobe Experience Manager [artículo](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager);
* Revise la producción de MongoDB [lista de comprobación](https://docs.mongodb.org/manual/administration/production-checklist/);
* Asista a una clase de certificación en MongoDB disponible en línea [aquí](https://university.mongodb.com/).

>[!NOTE]
>
>Si tiene más preguntas sobre estas directrices, requisitos previos y recomendaciones, póngase en contacto con [Adobe del Servicio de atención al cliente](https://helpx.adobe.com/es/marketing-cloud/contact-support.html).

### Consideraciones para AEM Communities {#considerations-for-aem-communities}

Para sitios que planean implementar [AEM Communities](/help/communities/overview.md), se recomienda [elija una implementación](/help/communities/working-with-srp.md#characteristicsofstorageoptions) optimizado para administrar UGC publicados por miembros de la comunidad desde el entorno de publicación.

Mediante un [almacén común](/help/communities/working-with-srp.md)Sin embargo, no es necesario replicar el UGC entre las instancias de autor y otras instancias de publicación para obtener una vista coherente del UGC.

A continuación se muestra un conjunto de matrices de decisiones que pueden ayudarle a elegir el mejor tipo de persistencia para su implementación:

#### Elección del tipo de implementación para instancias de autor {#choosing-the-deployment-type-for-author-instances}

![chlimage_1-19](assets/chlimage_1-19.png)

#### Elección del tipo de implementación para instancias de publicación {#choosing-the-deployment-type-for-publish-instances}

![chlimage_1-20](assets/chlimage_1-20.png)

>[!NOTE]
>
>MongoDB es software de terceros y no está incluido en el paquete de licencias de AEM. Para obtener más información, consulte la página [Directiva de licencias de MongoDB](https://www.mongodb.org/about/licensing/).
>
>AEM Para aprovechar al máximo su implementación, Adobe recomienda licenciar la versión de MongoDB Enterprise para beneficiarse del soporte profesional.
>
>La licencia incluye un conjunto de réplicas estándar, que está compuesto por una instancia principal y dos secundarias que se pueden utilizar para las implementaciones de autor o publicación.
>
>Si desea ejecutar tanto la creación como la publicación en MongoDB, se deben adquirir dos licencias independientes.
>
>Para obtener más información, consulte la [Página MongoDB para Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).
