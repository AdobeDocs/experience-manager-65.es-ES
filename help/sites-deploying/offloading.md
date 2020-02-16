---
title: Descarga de trabajos
seo-title: Descarga de trabajos
description: Obtenga información sobre cómo configurar y utilizar instancias de AEM en una topología para realizar tipos específicos de procesamiento.
seo-description: Obtenga información sobre cómo configurar y utilizar instancias de AEM en una topología para realizar tipos específicos de procesamiento.
uuid: e971d403-dfd2-471f-b23d-a67e35f1ed88
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 370151df-3b8e-41aa-b586-5c21ecb55ffe
translation-type: tm+mt
source-git-commit: 4ccaf401d561087f864c95e2be4c594cf34a7cb7

---


# Descarga de trabajos{#offloading-jobs}

## Introducción {#introduction}

La descarga distribuye tareas de procesamiento entre instancias de Experience Manager en una topología. Con la descarga, puede utilizar instancias específicas de Experience Manager para realizar tipos de procesamiento específicos. El procesamiento especializado le permite maximizar el uso de los recursos de servidor disponibles.

La descarga se basa en las funciones [Apache Sling Discovery](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html) y Sling JobManager. Para utilizar la descarga, agregue clústeres de Experience Manager a una topología e identifique los temas de trabajo que procesa el clúster. Los clústeres están compuestos de una o varias instancias de Experience Manager, de modo que una sola instancia se considera un clúster.

Para obtener información sobre cómo agregar instancias a una topología, consulte [Administración de topologías](/help/sites-deploying/offloading.md#administering-topologies).

### Distribución de trabajos {#job-distribution}

Sling JobManager y JobConsumer permiten la creación de trabajos procesados en una topología:

* JobManager: Un servicio que crea trabajos para temas específicos.
* JobConsumer: Un servicio que ejecuta trabajos de uno o más temas. Se pueden registrar varios servicios de JobConsumer para el mismo tema.

Cuando JobManager crea un trabajo, el marco de descarga selecciona un clúster de Experience Manager en la topología para ejecutar el trabajo:

* El clúster debe incluir una o varias instancias que ejecuten un JobConsumer registrado para el tema del trabajo.
* El tema debe estar habilitado para al menos una instancia del clúster.

Consulte [Configuración del consumo](/help/sites-deploying/offloading.md#configuring-topic-consumption) de temas para obtener información sobre cómo refinar la distribución de trabajos.

![chlimage_1-109](assets/chlimage_1-109.png)

Cuando el marco de descarga selecciona un clúster para ejecutar un trabajo y el clúster está compuesto de varias instancias, Sling Distribution determina qué instancia del clúster ejecuta el trabajo.

### Cargas de trabajo {#job-payloads}

El marco de descarga admite cargas de trabajo que asocian trabajos con recursos del repositorio. Las cargas de trabajo son útiles cuando se crean trabajos para procesar recursos y el trabajo se descarga a otro equipo.

Al crear un trabajo, la carga útil sólo se encuentra en la instancia que lo crea. Al descargar el trabajo, los agentes de replicación se aseguran de que la carga útil se crea en la instancia que finalmente consume el trabajo. Una vez finalizada la ejecución del trabajo, la replicación inversa hace que la carga útil se copie de nuevo en la instancia que creó el trabajo.

## Administración de topologías {#administering-topologies}

Las topologías son clústeres de Experience Manager con poco acoplamiento que participan en la descarga. Un clúster consta de una o varias instancias de servidor de Experience Manager (una sola instancia se considera un clúster).

Cada instancia de Experience Manager ejecuta los siguientes servicios relacionados con la descarga:

* Servicio de detección: Envía solicitudes a un conector de topología para unirse a la topología.
* Conector de topología: Recibe las solicitudes de combinación y acepta o rechaza cada solicitud.

El servicio de detección de todos los miembros de la topología apunta al conector de topología de uno de los miembros. En las secciones siguientes, este miembro se denomina miembro raíz.

![chlimage_1-110](assets/chlimage_1-110.png)

Cada clúster de la topología contiene una instancia que se reconoce como el encabezado. El líder del clúster interactúa con la topología en nombre de los demás miembros del clúster. Cuando el encabezado abandona el clúster, se elige automáticamente un nuevo encabezado para el clúster.

### Visualización de la topología {#viewing-the-topology}

Utilice el Explorador de topología para explorar el estado de la topología en la que participa la instancia de Experience Manager. Topology Browser muestra los clústeres y las instancias de la topología.

Para cada clúster, verá una lista de miembros del clúster que indica el orden en que cada miembro se unió al clúster y qué miembro es el encabezado. La propiedad Current indica la instancia que está administrando.

Para cada instancia del clúster, puede ver varias propiedades relacionadas con la topología:

* Lista blanca de temas para el consumidor de trabajos de la instancia.
* Los extremos expuestos para la conexión con la topología.
* Temas de trabajo para los que se ha registrado la instancia para la descarga.
* Temas de trabajo que procesa la instancia.

1. Con la IU táctil, haga clic en la ficha Herramientas. ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. En el área Operaciones de granito, haga clic en Navegador de descarga.
1. En el panel de navegación, haga clic en Explorador de topología.

   Aparecerán los clústeres que participan en la topología.

   ![chlimage_1-111](assets/chlimage_1-111.png)

1. Haga clic en un clúster para ver una lista de las instancias del clúster y su ID, estado actual y estado de encabezado.
1. Haga clic en un ID de instancia para ver propiedades más detalladas.

También puede utilizar la consola web para ver la información de topología. La consola proporciona más información sobre los clústeres de topología:

* Qué instancia es la instancia local.
* Los servicios del conector de topología que utiliza esta instancia para conectarse a la topología (saliente) y los servicios que se conectan a esta instancia (entrante).
* Cambiar el historial de las propiedades de topología e instancia.

Utilice el procedimiento siguiente para abrir la página Administración de topología de la consola web:

1. Abra la consola web en el explorador. ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. Haga clic en Principal > Administración de topología.

   ![chlimage_1-112](assets/chlimage_1-112.png)

### Configuración de la pertenencia a la topología {#configuring-topology-membership}

El servicio de detección basado en recursos de Apache Sling se ejecuta en cada instancia para controlar cómo interactúan las instancias de Experience Manager con una topología.

El servicio de detección envía solicitudes POST periódicas (latidos) a los servicios de Topology Connector para establecer y mantener conexiones con la topología. El servicio Conector de topología mantiene una lista blanca de direcciones IP o nombres de host que pueden unirse a la topología:

* Para unir una instancia a una topología, especifique la dirección URL del servicio Conector de topología del miembro raíz.
* Para habilitar una instancia para que se una a una topología, agregue la instancia a la lista blanca del servicio Topology Connector del miembro raíz.

Utilice la consola web o un nodo sling:OsgiConfig para configurar las siguientes propiedades del servicio org.apache.sling.discover.impt.Config:

<table>
 <tbody>
  <tr>
   <th>Nombre de propiedad</th>
   <th>Nombre OSGi</th>
   <th>Descripción</th>
   <th>Valor predeterminado</th>
  </tr>
  <tr>
   <td>Tiempo de espera de Heartbeat (segundos)</td>
   <td>heartbeatTimeout</td>
   <td>Cantidad de tiempo en segundos que se espera una respuesta de latidos antes de que la instancia de destino se considere no disponible. </td>
   <td>20</td>
  </tr>
  <tr>
   <td>Intervalo de monitoreo del funcionamiento (segundos)</td>
   <td>heartbeatInterval</td>
   <td>Cantidad de tiempo en segundos entre latidos.</td>
   <td>15</td>
  </tr>
  <tr>
   <td>Retraso mínimo del evento (segundos)</td>
   <td>minEventDelay</td>
   <td><p>Cuando se produce un cambio en la topología, la cantidad de tiempo que se tarda en retrasar el cambio de estado de TOPOLOGY_CHANGING a TOPOLOGY_CHANGED. Cada cambio que se produce cuando el estado es TOPOLOGY_CHANGING aumenta el retraso en esta cantidad de tiempo.</p> <p>Este retraso evita que los oyentes se vean inundados de eventos. </p> <p>Para no utilizar ningún retraso, especifique 0 o un número negativo.</p> </td>
   <td>3</td>
  </tr>
  <tr>
   <td>Direcciones URL del conector de topología</td>
   <td>topologíaConnectorUrls</td>
   <td>Las direcciones URL de los servicios de Topology Connector para enviar mensajes de Heartbeat.</td>
   <td>http://localhost:4502/libs/sling/topology/connector</td>
  </tr>
  <tr>
   <td>Lista blanca del conector de topología</td>
   <td>topologíaConnectorWhitelist</td>
   <td>Lista de direcciones IP o nombres de host que permite el servicio Conector de topología local en la topología. </td>
   <td><p>localhost</p> <p>127.0.0.1</p> </td>
  </tr>
  <tr>
   <td>Nombre del descriptor del repositorio</td>
   <td>leaderElectionRepositoryDescriptor</td>
   <td> </td>
   <td>&lt;ningún valor&gt;</td>
  </tr>
 </tbody>
</table>

Utilice el siguiente procedimiento para conectar una instancia de CQ al miembro raíz de una topología. El procedimiento señala la instancia a la URL del conector de topología del miembro de topología raíz. Realice este procedimiento en todos los miembros de la topología.

1. Abra la consola web en el explorador. ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. Haga clic en Principal > Administración de topología.
1. Haga clic en Configurar servicio de detección.
1. Agregue un elemento a la propiedad URL del conector de topología y especifique la dirección URL del servicio Conector de topología del miembro de la topología raíz. La dirección URL tiene el formato https://rootservername:4502/libs/sling/topology/connector.

Realice el siguiente procedimiento en el miembro raíz de la topología. El procedimiento agrega los nombres de los demás miembros de la topología a su lista blanca de Discovery Service.

1. Abra la consola web en el explorador. ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. Haga clic en Principal > Administración de topología.
1. Haga clic en Configurar servicio de detección.
1. Para cada miembro de la topología, agregue un elemento a la propiedad Lista blanca del conector de topología y especifique el nombre de host o la dirección IP del miembro de la topología.

## Configuración del consumo de temas {#configuring-topic-consumption}

Utilice el navegador de descarga para configurar el consumo de temas para las instancias de Experience Manager en la topología. Para cada instancia, puede especificar los temas que consume. Por ejemplo, para configurar la topología de modo que solo una instancia consuma temas de un tipo específico, deshabilite el tema en todas las instancias excepto en una.

Los trabajos se distribuyen entre instancias que tienen activado el tema asociado mediante la lógica de rotación.

1. Con la IU táctil, haga clic en la ficha Herramientas. ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. En el área Operaciones de granito, haga clic en Navegador de descarga.
1. En el panel de navegación, haga clic en Descarga del navegador.

   Aparecerán los temas de descarga y las instancias del servidor que pueden consumir los temas.

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. Para desactivar el consumo de un tema para una instancia, haga clic en Deshabilitar, junto a la instancia, debajo del nombre del tema.
1. Para configurar todo el consumo de temas de una instancia, haga clic en el identificador de instancia debajo de cualquier tema.

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. Haga clic en uno de los siguientes botones junto a un tema para configurar el comportamiento de consumo de la instancia y, a continuación, haga clic en Guardar:

   * Habilitado: Esta instancia consume trabajos de este tema.
   * Deshabilitado: Esta instancia no consume trabajos de este tema.
   * Exclusivo: Esta instancia solo consume trabajos de este tema.
   **** Nota: Al seleccionar Exclusivo para un tema, todos los demás temas se establecen automáticamente como Deshabilitado.

### Consumidores de trabajos instalados {#installed-job-consumers}

Con Experience Manager se instalan varias implementaciones de JobConsumer. Los temas para los que están registrados estos JobConsumers aparecen en el Explorador de descargas. Los temas adicionales que aparecen son los que se han registrado en JobConsumers personalizados. En la tabla siguiente se describe el valor predeterminado de JobConsumers.

| Tema del trabajo | PID de servicio | Descripción |
|---|---|---|
| / | org.apache.sling.event.impl.Jobs.deprecated.EventAdminBridge | Instalado con Apache Sling. Procesa los trabajos que genera el administrador de eventos OSGi para lograr compatibilidad con versiones anteriores. |
| com/day/cq/Replication/job/&amp;ast; | com.day.cq.replication.impl.AgentManagerImpl | Agente de replicación que replica cargas de trabajo. |
| com/adobe/granite/workflow/offloading | com.adobe.granite.workflow.core.offloading.WorkflowOffloadingJobConsumer | Procesa los trabajos que genera el flujo de trabajo de descarga de recursos de actualización de DAM. |

### Desactivación y activación de temas para una instancia {#disabling-and-enabling-topics-for-an-instance}

El servicio Apache Sling Job Consumer Manager proporciona propiedades de lista blanca y lista negra de temas. Configure estas propiedades para habilitar o deshabilitar el procesamiento de temas específicos en una instancia de Experience Manager.

**** Nota: Si la instancia pertenece a una topología, también puede utilizar el Explorador de descargas en cualquier equipo de la topología para habilitar o deshabilitar temas.

La lógica que crea la lista de temas habilitados primero permite todos los temas que están en la lista blanca y, a continuación, elimina los temas que están en la lista negra. De forma predeterminada, todos los temas están habilitados (el valor de la lista blanca es `*`) y no hay temas deshabilitados (la lista negra no tiene valor).

Utilice la consola web o un `sling:OsgiConfig` nodo para configurar las siguientes propiedades. Para `sling:OsgiConfig` los nodos, el PID del servicio Job Consumer Manager es org.apache.sling.event.impl.job.JobConsumerManager.

| Nombre de propiedad en la consola web | ID de OSGi | Descripción |
|---|---|---|
| Lista blanca del tema | job.consumermanager.whitelist | Una lista de temas que procesa el servicio local de JobManager. El valor predeterminado de &amp;ast; hace que todos los temas se envíen al servicio TopicConsumer registrado. |
| Lista negra de temas | job.consumermanager.blacklist | Una lista de temas que el servicio local de JobManager no procesa. |

## Creación De Agentes De Replicación Para Descarga {#creating-replication-agents-for-offloading}

El marco de descarga utiliza la replicación para transportar recursos entre el autor y el trabajador. El marco de descarga crea automáticamente agentes de replicación cuando las instancias se unen a la topología. Los agentes se crean con valores predeterminados. Debe cambiar manualmente la contraseña que utilizan los agentes para la autenticación.

>[!CAUTION]
>
>Un problema conocido con los agentes de replicación generados automáticamente requiere que cree manualmente nuevos agentes de replicación. Siga el procedimiento que se describe en [Problemas al utilizar los agentes](/help/sites-deploying/offloading.md#problems-using-the-automatically-generated-replication-agents) de replicación generados automáticamente antes de crear los agentes para la descarga.

Cree los agentes de replicación que transportan cargas de trabajo entre instancias para la descarga. La siguiente ilustración muestra los agentes que se deben descargar del autor a una instancia de trabajo. El autor tiene un Sling ID de 1 y la instancia de trabajo tiene un Sling ID de 2:

![chlimage_1-115](assets/chlimage_1-115.png)

Esta configuración requiere los tres agentes siguientes:

1. Agente saliente en la instancia de autor que se replica en la instancia de trabajador.
1. Agente inverso en la instancia de autor que extrae de la bandeja de salida de la instancia de trabajo.
1. Agente de salida en la instancia de trabajo.

Este esquema de replicación es similar al utilizado entre instancias de autor y publicación. Sin embargo, para la situación de descarga, todas las instancias implicadas son instancias de creación.

>[!NOTE]
>
>El marco de descarga utiliza la topología para obtener las direcciones IP de las instancias de descarga. A continuación, el marco crea automáticamente los agentes de replicación basados en estas direcciones IP. Si las direcciones IP de las instancias de descarga cambian más adelante, el cambio se propaga automáticamente en la topología después de que se reinicia la instancia. Sin embargo, el marco de descargas no actualiza automáticamente los agentes de replicación para reflejar las nuevas direcciones IP. Para evitar esta situación, utilice direcciones IP fijas para todas las instancias de la topología.

### Asignación de nombres a los agentes de replicación para la descarga {#naming-the-replication-agents-for-offloading}

Utilice un formato específico para la propiedad ***Name*** de los agentes de replicación de modo que el marco de descarga utilice automáticamente el agente correcto para instancias de trabajo específicas.

**Asignación de nombres al agente saliente en la instancia de creación:**

`offloading_<slingid>`, donde `<slingid>` es el ID de Sling de la instancia de trabajo.

Ejemplo: `offloading_f5c8494a-4220-49b8-b079-360a72f71559`

**Asignación de un nombre al agente inverso en la instancia de creación:**

`offloading_reverse_<slingid>`, donde `<slingid>` es el ID de Sling de la instancia de trabajo.

Ejemplo: `offloading_reverse_f5c8494a-4220-49b8-b079-360a72f71559`

**Asignación de un nombre a la bandeja de salida en la instancia de trabajo:**

`offloading_outbox`

### Creación del agente saliente {#creating-the-outgoing-agent}

1. Cree un agente **de replicación** en el autor. (Consulte la [documentación de los agentes](/help/sites-deploying/replication.md)de replicación). Especifique cualquier **título**. El **nombre** debe seguir la convención de nombre.
1. Cree el agente con las siguientes propiedades:

   | Propiedad | Value |
   |---|---|
   | Configuración > Tipo de serialización | Predeterminado |
   | Transporte > URI de transporte | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | Transporte > Usuario de transporte | Usuario de replicación en instancia de destino |
   | Transporte > Pasaporte de transporte | Contraseña de usuario de replicación en la instancia de destino |
   | Extended > Método HTTP | POST |
   | Activadores > Ignorar predeterminado | Verdadero |

### Creación del agente inverso {#creating-the-reverse-agent}

1. Cree un agente **de replicación** inversa en el autor. (Consulte la [documentación de los agentes](/help/sites-deploying/replication.md)de replicación). Especifique cualquier **título**. El **nombre** debe seguir la convención de nombre.
1. Cree el agente con las siguientes propiedades:

   | Propiedad | Value |
   |---|---|
   | Configuración > Tipo de serialización | Predeterminado |
   | Transporte > URI de transporte | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | Transporte > Usuario de transporte | Usuario de replicación en instancia de destino |
   | Transporte > Pasaporte de transporte | Contraseña de usuario de replicación en la instancia de destino |
   | Extended > Método HTTP | OBTENER |

### Creación del agente de salida {#creating-the-outbox-agent}

1. Cree un agente **de** replicación en la instancia de trabajo. (Consulte la [documentación de los agentes](/help/sites-deploying/replication.md)de replicación). Especifique cualquier **título**. El **nombre** debe ser `offloading_outbox`.
1. Cree el agente con las siguientes propiedades.

   | Propiedad | Value |
   |---|---|
   | Configuración > Tipo de serialización | Predeterminado |
   | Transporte > URI de transporte | repo://var/replication/outbox |
   | Activador > Ignorar predeterminado | Verdadero |

### Búsqueda del ID de Sling {#finding-the-sling-id}

Obtenga el Sling ID de una instancia de Experience Manager mediante cualquiera de los siguientes métodos:

* Abra la consola web y, en Configuración de Sling, busque el valor de la propiedad ID de Sling ([http://localhost:4502/system/console/status-slingsettings](http://localhost:4502/system/console/status-slingsettings)). Este método es útil si la instancia todavía no forma parte de la topología.
* Utilice el navegador de topología si la instancia ya forma parte de la topología.

## Descarga del procesamiento de recursos DAM {#offloading-the-processing-of-dam-assets}

Configure las instancias de una topología para que instancias específicas realicen el procesamiento en segundo plano de los recursos que se agregan o actualizan en DAM.

De forma predeterminada, Experience Manager ejecuta el flujo de trabajo de recursos de actualización de DAM cuando cambia un recurso DAM o cuando se agrega uno a DAM. Cambie el comportamiento predeterminado para que, en su lugar, Experience Manager ejecute el flujo de trabajo de descarga de recursos de actualización de DAM. Este flujo de trabajo genera un trabajo de JobManager que tiene un tema de `com/adobe/granite/workflow/offloading`. A continuación, configure la topología para que el trabajo se descargue a un trabajador dedicado.

>[!CAUTION]
>
>Ningún flujo de trabajo debe ser transitorio cuando se utiliza con la descarga del flujo de trabajo. Por ejemplo, el flujo de trabajo de recursos de actualización de DAM no debe ser transitorio cuando se utiliza para la descarga de recursos. Para establecer o anular el indicador transitorio de un flujo de trabajo, consulte Flujos de trabajo [transitorios](/help/assets/performance-tuning-guidelines.md#workflows).

El siguiente procedimiento asume las siguientes características para la topología de descarga:

* Una o varias instancias de Experience Manager son instancias de creación con las que los usuarios interactúan para agregar o actualizar recursos DAM.
* Los usuarios no interactúan directamente con una o varias instancias de Experience Manager que procesan los recursos de DAM. Estas instancias están dedicadas al procesamiento en segundo plano de los recursos DAM.

1. En cada instancia de Experience Manager, configure el servicio de detección para que apunte al conector de topografía raíz. (Consulte [Configuración de la pertenencia](#title4)a la topología).
1. Configure el Conector de topografía raíz para que las instancias de conexión estén en la lista de direcciones permitidas.
1. Abra el navegador de descargas y deshabilite el `com/adobe/granite/workflow/offloading` tema en las instancias con las que los usuarios interactúan para cargar o cambiar recursos DAM.

   ![chlimage_1-116](assets/chlimage_1-116.png)

1. En cada instancia con la que los usuarios interactúan para cargar o cambiar recursos DAM, configure los iniciadores de flujo de trabajo para utilizar el flujo de trabajo de descarga de recursos de actualización de DAM:

   1. Abra la consola Flujo de trabajo.
   1. Haga clic en la ficha Iniciador.
   1. Busque las dos configuraciones del iniciador que ejecutan el flujo de trabajo de recursos de actualización de DAM. Un tipo de evento de configuración del iniciador es Nodo creado y el otro tipo es Nodo modificado.
   1. Cambie ambos tipos de eventos para que ejecuten el flujo de trabajo de descarga de recursos de actualización de DAM. (Para obtener información sobre las configuraciones del iniciador, consulte [Inicio de flujos de trabajo cuando cambian](/help/sites-administering/workflows-starting.md)los nodos).

1. En las instancias que realizan el procesamiento en segundo plano de recursos DAM, deshabilite los iniciadores de flujo de trabajo que ejecutan el flujo de trabajo de recursos de actualización de DAM.

## Lectura adicional {#further-reading}

Además de los detalles presentados en esta página, también puede leer lo siguiente:

* Para obtener información sobre el uso de las API de Java para crear trabajos y para los consumidores de trabajos, consulte [Creación y consumo de trabajos para la descarga](/help/sites-developing/dev-offloading.md).
