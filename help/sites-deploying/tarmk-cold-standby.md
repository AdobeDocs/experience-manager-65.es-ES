---
title: Cómo ejecutar AEM con TarMK Cold Standby
seo-title: Cómo ejecutar AEM con TarMK Cold Standby
description: Aprenda a crear, configurar y mantener una configuración de TarMK Cold Standby.
seo-description: Aprenda a crear, configurar y mantener una configuración de TarMK Cold Standby.
uuid: 004fdf3e-517c-452b-8db1-a47d6b31d8ba
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9559e837-a87e-4ee7-8ca6-13b42c74e6bf
docset: aem65
translation-type: tm+mt
source-git-commit: a99c5794cee88d11ca3fb9eeed443c4d0178c7b3
workflow-type: tm+mt
source-wordcount: '2731'
ht-degree: 0%

---


# Cómo ejecutar AEM con TarMK Cold Standby{#how-to-run-aem-with-tarmk-cold-standby}

## Introducción {#introduction}

La capacidad de espera en frío del núcleo Tar Micro permite que una o más instancias de AEM en espera se conecten a una instancia primaria. El proceso de sincronización es de una sola forma, lo que significa que solo se realiza desde las instancias principales a las de espera.

El propósito de las instancias en espera es garantizar una copia de datos activa del repositorio principal y garantizar un cambio rápido sin pérdida de datos en caso de que el maestro no esté disponible por ningún motivo.

El contenido se sincroniza linealmente entre la instancia principal y las instancias en espera sin comprobar la integridad del archivo o repositorio dañado. Debido a este diseño, las instancias en espera son copias exactas de la instancia principal y no pueden ayudar a mitigar las incoherencias en las instancias principales.

>[!NOTE]
>
>La función de espera en frío está pensada para asegurar situaciones en las que se requiere alta disponibilidad en instancias de **autor**. En situaciones en las que se requiere alta disponibilidad en instancias de **publicación** que utilizan el núcleo Tar Micro, Adobe recomienda utilizar un conjunto de servidores de publicación.
>
>Para obtener información sobre más implementaciones disponibles, consulte la página [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md).

## Cómo funciona {#how-it-works}

En la instancia de AEM principal, se abre un puerto TCP que escucha los mensajes entrantes. Actualmente, hay dos tipos de mensajes que los esclavos enviarán al maestro:

* un mensaje que solicita el ID de segmento del encabezado actual
* un mensaje que solicita datos de segmento con un ID especificado

El modo de espera solicita periódicamente la ID del segmento del encabezado actual del elemento principal. Si el segmento es desconocido localmente, se recuperará. Si ya está presente, los segmentos se comparan y los segmentos a los que se hace referencia también se solicitarán, si es necesario.

>[!NOTE]
>
>Las instancias en espera no reciben ningún tipo de solicitudes, ya que se ejecutan en modo de solo sincronización. La única sección disponible en una instancia de espera es la consola web, para facilitar la configuración del paquete y los servicios.

Una implementación típica de TarMK Cold Standby:

![chlimage_1](assets/chlimage_1.png)

## Otras características {#other-characteristics}

### Solidez {#robustness}

El flujo de datos está diseñado para detectar y gestionar automáticamente los problemas relacionados con la conexión y la red. Todos los paquetes están empaquetados con sumas de comprobación y tan pronto como se producen problemas con la conexión o los paquetes dañados se activan mecanismos de reintento.

#### Actuación {#performance}

La activación de TarMK Cold Standby en la instancia principal casi no tiene un impacto medible en el rendimiento. El consumo adicional de CPU es muy bajo y el E/S de red y el disco duro extra no deben producir problemas de rendimiento.

En espera, puede esperar un alto consumo de CPU durante el proceso de sincronización. Debido a que el procedimiento no se multiproceso, no se puede acelerar utilizando varios núcleos. Si no se cambia o transfiere ningún dato, no habrá actividad mensurable. La velocidad de conexión variará según el hardware y el entorno de red, pero no depende del tamaño del repositorio o del uso de SSL. Debe tener esto en cuenta al calcular el tiempo necesario para una sincronización inicial o cuando se cambiaron muchos datos mientras tanto en el nodo principal.

#### Seguridad {#security}

Suponiendo que todas las instancias se ejecutan en la misma zona de seguridad de intranet, el riesgo de una infracción de seguridad se reduce considerablemente. Sin embargo, puede agregar una capa de seguridad adicional habilitando las conexiones SSL entre los esclavos y el maestro. Al hacerlo, se reduce la posibilidad de que los datos se vean comprometidos por un intermediario.

Además, puede especificar las instancias en espera que pueden conectarse restringiendo la dirección IP de las solicitudes entrantes. Esto debería ayudar a garantizar que nadie en la intranet pueda copiar el repositorio.

>[!NOTE]
>
>Se recomienda añadir un equilibrador de carga entre el despachante y los servidores que forman parte de la configuración de Coldy Standby. El equilibrador de carga debe configurarse para dirigir el tráfico del usuario únicamente a la instancia **primaria** a fin de garantizar la coherencia y evitar que el contenido se copie en la instancia de espera por otros medios que no sean el mecanismo de espera en frío.

## Creación de una configuración AEM TarMK Cold Standby {#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>El PID para el almacén de nodos Segment y el servicio de almacenamiento en espera han cambiado en AEM 6.3 en comparación con las versiones anteriores de la siguiente manera:
>
>* de org.apache.jackrabbit.oak.**plugins**.segment.standby.store.StandbyStoreService a org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService
>* de org.apache.jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService a org.apache.jackrabbit.oak.segment.SegmentNodeStoreService

>
>
Asegúrese de realizar los ajustes de configuración necesarios para reflejar este cambio.

Para crear una configuración de TarMK en espera en frío, primero debe crear las instancias en espera realizando una copia del sistema de archivos de toda la carpeta de instalación del primario a una nueva ubicación. A continuación, puede inicio cada instancia con un modo de ejecución que especifique su función ( `primary` o `standby`).

A continuación se muestra el procedimiento que debe seguirse para crear una configuración con una instancia maestra y una de espera:

1. Instale AEM.

1. Cierre la instancia y copie la carpeta de instalación en la ubicación desde la que se ejecutará la instancia de espera en frío. Incluso si se ejecuta desde diferentes equipos, asegúrese de asignar a cada carpeta un nombre descriptivo (como *aem-parent* o *aem-standby*) para diferenciar entre las instancias.
1. Vaya a la carpeta de instalación de la instancia principal y:

   1. Compruebe y elimine cualquier configuración OSGi anterior que pueda tener en `aem-primary/crx-quickstart/install`

   1. Cree una carpeta llamada `install.primary` en `aem-primary/crx-quickstart/install`

   1. Cree las configuraciones necesarias para el almacén de nodos y el almacén de datos preferidos en `aem-primary/crx-quickstart/install/install.primary`
   1. Cree un archivo llamado `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config` en la misma ubicación y configúrelo según corresponda. Para obtener más información sobre las opciones de configuración, consulte [Configuration](/help/sites-deploying/tarmk-cold-standby.md#configuration).

   1. Si está utilizando una instancia AEM TarMK con un almacén de datos externo, cree una carpeta con el nombre `crx3` en `aem-primary/crx-quickstart/install` con el nombre `crx3`

   1. Coloque el archivo de configuración del almacén de datos en la carpeta `crx3`.

   Si, por ejemplo, está ejecutando una instancia AEM TarMK con un almacén de datos de archivos externo, necesita estos archivos de configuración:

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`

   A continuación encontrará configuraciones de muestra para la instancia principal:

   **Ejemplo de** **oforg.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   customBlobStore=B"true"
   standby=B"false"
   ```

   **Ejemplo de org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="primary"
   port=I"8023"
   ```

   **Ejemplo de org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. Inicio el principal asegurándose de especificar el modo de ejecución principal:

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. Cree un nuevo registrador de registros de Apache Sling para el paquete **org.apache.jackrabbit.oak.segment**. Establezca el nivel de registro en &quot;Debug&quot; y dirija su salida de registro a un archivo de registro independiente, como */logs/tarmk-coldstandby.log*. Para obtener más información, consulte [Registro](/help/sites-deploying/configure-logging.md).
1. Vaya a la ubicación de la instancia **standby** y inicio mediante la ejecución del tarro.
1. Cree la misma configuración de registro que para el principal. A continuación, detenga la instancia.
1. A continuación, prepare la instancia de espera. Para ello, siga los mismos pasos que para la instancia principal:

   1. Elimine los archivos que pueda tener en `aem-standby/crx-quickstart/install`.
   1. Cree una nueva carpeta llamada `install.standby` en `aem-standby/crx-quickstart/install`

   1. Cree dos archivos de configuración llamados:

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   1. Cree una nueva carpeta llamada `crx3` en `aem-standby/crx-quickstart/install`

   1. Cree la configuración del almacén de datos y colóquela en `aem-standby/crx-quickstart/install/crx3`. Para este ejemplo, el archivo que debe crear es:

      * org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config
   1. Edite los archivos y cree las configuraciones necesarias.

   A continuación se muestran archivos de configuración de ejemplo para una instancia de espera típica:

   **Ejemplo de org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   name="Oak-Tar"
   service.ranking=I"100"
   standby=B"true"
   customBlobStore=B"true"
   ```

   **Ejemplo de org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="standby"
   primary.host="127.0.0.1"
   port=I"8023"
   secure=B"false"
   interval=I"5"
   standby.autoclean=B"true"
   ```

   **Ejemplo de org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. Inicio de la instancia **standby** mediante el modo de ejecución en espera:

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

El servicio también se puede configurar mediante la consola web, mediante:

1. Ir a la consola web en: *https://serveraddress:serverport/system/console/configMgr*
1. Buscando un servicio llamado **Apache Jackrabbit Oak Segment Tar Cold Standby Service** y doble haga clic en él para editar la configuración.
1. Guarde la configuración y reinicie las instancias para que la nueva configuración surta efecto.

>[!NOTE]
>
>Puede comprobar la función de una instancia en cualquier momento comprobando la presencia de los modos de ejecución **primario** o **en espera** en la consola web de configuración de Sling.
>
>Esto se puede hacer yendo a *https://localhost:4502/system/console/status-slingsettings* y marcando la línea **&quot;Run Modes&quot;**.

## Primera sincronización {#first-time-synchronization}

Una vez finalizada la preparación y iniciada la espera por primera vez, habrá mucho tráfico de red entre las instancias a medida que la capacidad de espera alcance el nivel primario. Puede consultar los registros para observar el estado de la sincronización.

En el archivo de espera *tarmk-coldstandby.log*, verá entradas como estas:

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

En el archivo *error.log* de espera, debería ver una entrada como esta:

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

En el fragmento de registro anterior, *10.20.30.40* es la dirección IP del elemento principal.

En **primario** *tarmk-coldstandby.log*, verá entradas como estas:

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message ‘s.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd’ from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

En este caso, el &quot;cliente&quot; mencionado en el registro es la instancia **standby**.

Una vez que estas entradas dejen de aparecer en el registro, puede suponer con seguridad que el proceso de sincronización ha finalizado.

Aunque las entradas anteriores muestran que el mecanismo de sondeo funciona correctamente, a menudo resulta útil saber si hay datos sincronizados mientras se realiza una encuesta. Para ello, busque entradas como las siguientes:

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

Además, cuando se ejecuta con un `FileDataStore` no compartido, mensajes como el siguiente confirman que los archivos binarios se transmiten correctamente:

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### Configuración {#configuration}

Los siguientes ajustes de OSGi están disponibles para el servicio de espera en frío:

* **Configuración persistente:** si está habilitada, almacenará la configuración en el repositorio en lugar de en los archivos de configuración OSGi tradicionales. Se recomienda mantener esta configuración deshabilitada en los sistemas de producción para que la configuración principal no se recupere con la configuración en espera.

* **Modo (`mode`):** se seleccionará el modo de ejecución de la instancia.

* **Puerto (puerto):** el puerto que se va a utilizar para la comunicación. El valor predeterminado es `8023`.

* **Host principal (`primary.host`):**  el host de la instancia principal. Esta configuración solo se aplica a la espera.
* **Intervalo de sincronización (`interval`):** - este ajuste determina el intervalo entre la solicitud de sincronización y solo se aplica a la instancia de espera.

* **Intervalos IP permitidos (`primary.allowed-client-ip-ranges`):** - los intervalos IP desde los que el principal permitirá las conexiones.
* **Seguro (`secure`):** activar codificación SSL. Para utilizar esta configuración, debe habilitarse en todas las instancias.
* **Tiempo de espera de lectura en espera (`standby.readtimeout`):** tiempo de espera para solicitudes emitidas desde la instancia en espera en milisegundos. El valor de tiempo de espera recomendado es 43200000. Generalmente se recomienda que establezca el tiempo de espera en un valor de al menos 12 horas.

* **Limpieza automática en espera (`standby.autoclean`):** llame al método de limpieza si el tamaño del almacén aumenta en un ciclo de sincronización.

>[!NOTE]
>
>Se recomienda que el principal y el en espera tengan ID de repositorio diferentes para que sean independientes para servicios como Descarga.
>
>La mejor manera de asegurarse de que esto se cubre es eliminando el archivo *sling.id* en espera y reiniciando la instancia.

## Procedimientos de conmutación por error {#failover-procedures}

En caso de que la instancia principal falle por cualquier motivo, puede configurar una de las instancias en espera para que asuma la función de principal cambiando el modo de ejecución de inicio como se detalla a continuación:

>[!NOTE]
>
>Los archivos de configuración también deben modificarse para que coincidan con la configuración utilizada para la instancia principal.

1. Vaya a la ubicación donde está instalada la instancia de espera y deténgalo.

1. Si tiene un equilibrador de carga configurado con la configuración, puede quitar el principal de la configuración del equilibrador de carga en este punto.
1. Haga una copia de seguridad de la carpeta `crx-quickstart` desde la carpeta de instalación en espera. Se puede utilizar como punto de partida al configurar una nueva suspensión.

1. Reinicie la instancia con el modo de ejecución `primary`:

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. Añada el nuevo principal al equilibrador de carga.
1. Cree y inicio una nueva instancia de espera. Para obtener más información, consulte el procedimiento anterior sobre [Creación de una configuración de AEM TarMK Cold Standby](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup).

## Aplicación de revisiones a una instalación en espera fría {#applying-hotfixes-to-a-cold-standby-setup}

La manera recomendada de aplicar revisiones a una configuración de un punto muerto en frío es instalarlas en la instancia primaria y luego clonar en una nueva instancia de espera en frío con las revisiones instaladas.

Para ello, siga los pasos que se describen a continuación:

1. Detenga el proceso de sincronización en la instancia de espera en frío yendo a la consola JMX y utilizando el archivo **org.apache.jackrabbit.oak: Estado (&quot;En espera&quot;)**. Para obtener más información sobre cómo hacerlo, consulte la sección sobre [Monitoreo](#monitoring).
1. Detenga la instancia de espera en frío.
1. Instale la revisión en la instancia principal. Para obtener más información sobre cómo instalar una revisión, consulte [Cómo trabajar con paquetes](/help/sites-administering/package-manager.md).
1. Pruebe la instancia en busca de problemas después de la instalación.
1. Elimine la instancia de espera en frío eliminando su carpeta de instalación.
1. Detenga la instancia principal y clóquela realizando una copia del sistema de archivos de toda la carpeta de instalación en la ubicación del modo de espera en frío.
1. Vuelva a configurar el clon recién creado para que actúe como una instancia de espera en frío. Para obtener más información, consulte [Creación de una configuración AEM TarMK Cold Standby.](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)
1. Inicio las instancias principal y en frío.

## Monitoreo {#monitoring}

La función expone información mediante JMX o MBeans. De este modo, puede inspeccionar el estado actual del modo de espera y del patrón mediante la [consola JMX](/help/sites-administering/jmx-console.md). La información se encuentra en un MBean de `type org.apache.jackrabbit.oak:type="Standby"`denominado `Status`.

**En espera**

Al observar una instancia de espera, se mostrará un nodo. El ID suele ser un UUID genérico.

Este nodo tiene cinco atributos de solo lectura:

* `Running:` valor booleano que indica si el proceso de sincronización se está ejecutando o no.

* `Mode:` Cliente: seguido del UUID utilizado para identificar la instancia. Tenga en cuenta que este UUID cambiará cada vez que se actualice la configuración.

* `Status:` una representación textual del estado actual (como  `running` o  `stopped`).

* `FailedRequests:`el número de errores consecutivos.
* `SecondsSinceLastSuccess:` el número de segundos transcurridos desde la última comunicación correcta con el servidor. Se mostrará `-1` si no se ha realizado una comunicación exitosa.

También hay tres métodos invocables:

* `start():` inicio el proceso de sincronización.
* `stop():` detiene el proceso de sincronización.
* `cleanup():` ejecuta la operación de limpieza en espera.

**Principal**

Al observar el principal se expone cierta información general mediante un MBean cuyo valor de ID es el número de puerto que utiliza el servicio TarMK en espera (8023 de forma predeterminada). La mayoría de los métodos y atributos son los mismos que para el modo de espera, pero algunos difieren:

* `Mode:` siempre mostrará el valor  `primary`.

Además, se puede recuperar la información de hasta 10 clientes (instancias en espera) conectados al maestro. El ID de MBean es el UUID de la instancia. No existen métodos invocables para estos MBeans, pero sí algunos atributos de solo lectura muy útiles:

* `Name:` ID del cliente.
* `LastSeenTimestamp:` la marca de tiempo de la última solicitud en una representación textual.
* `LastRequest:` la última solicitud del cliente.
* `RemoteAddress:` la dirección IP del cliente.
* `RemotePort:` el puerto que el cliente utilizó para la última solicitud.
* `TransferredSegments:` el número total de segmentos transferidos a este cliente.
* `TransferredSegmentBytes:`el número total de bytes transferidos a este cliente.

## Mantenimiento del repositorio en espera en frío {#cold-standby-repository-maintenance}

### Limpieza de revisión {#revision-clean}

>[!NOTE]
>
>Si ejecuta [Limpieza de revisión en línea](/help/sites-deploying/revision-cleanup.md) en la instancia principal, no es necesario el procedimiento manual que se presenta a continuación. Además, si utiliza la limpieza de revisión en línea, la operación `cleanup ()` en la instancia de espera se realizará automáticamente.

>[!NOTE]
>
>No ejecute la limpieza de revisión sin conexión en espera. No es necesario y no reducirá el tamaño del almacén de segmentos.

Adobe recomienda ejecutar el mantenimiento de forma regular para evitar un crecimiento excesivo del repositorio con el paso del tiempo. Para realizar manualmente el mantenimiento del repositorio en espera en frío, siga los pasos a continuación:

1. Detenga el proceso de espera en la instancia de espera yendo a la consola JMX y utilizando el archivo **org.apache.jackrabbit.oak: Estado (&quot;En espera&quot;)** grano. Para obtener más información sobre cómo hacerlo, consulte la sección anterior sobre [Monitoreo](/help/sites-deploying/tarmk-cold-standby.md#monitoring).

1. Detenga la instancia de AEM principal.
1. Ejecute la herramienta de compactación de roble en la instancia principal. Para obtener más información, consulte [Mantenimiento del repositorio](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
1. Inicio de la instancia principal.
1. Inicio el proceso de espera en la instancia de espera utilizando el mismo grano JMX como se describe en el primer paso.
1. Observe los registros y espere a que se complete la sincronización. Es posible que en este momento se observe un crecimiento sustancial en el repositorio de reserva.
1. Ejecute la operación `cleanup()` en la instancia de espera, utilizando el mismo grano JMX como se describe en el primer paso.

Puede que la instancia de espera tarde más de lo habitual en completar la sincronización con la compactación sin conexión principal, ya que la compactación sin conexión reescribe efectivamente el historial del repositorio, haciendo que el cálculo de los cambios en los repositorios tome más tiempo. También debe tenerse en cuenta que una vez que se complete este proceso, el tamaño del repositorio en espera será aproximadamente del mismo tamaño que el repositorio principal.

Como alternativa, el repositorio principal se puede copiar en modo manual al modo de espera después de ejecutar la compactación en el repositorio principal, lo que básicamente consiste en volver a generar el modo de espera cada vez que se ejecuta la compactación.

### Recolección de papelera del almacén de datos {#data-store-garbage-collection}

Es importante ejecutar la recolección de elementos no utilizados en instancias del almacén de datos de archivos de vez en cuando, ya que de lo contrario, los binarios eliminados permanecerán en el sistema de archivos, llenando finalmente la unidad. Para ejecutar la recolección de elementos no utilizados, siga el procedimiento siguiente:

1. Ejecute el mantenimiento del repositorio en espera en frío como se describe en la sección [anterior](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance).
1. Una vez finalizado el proceso de mantenimiento y reiniciadas las instancias:

   * En el almacén de datos principal, ejecute la recopilación de elementos no utilizados del almacén de datos a través del elemento de base JMX correspondiente, tal como se describe en [este artículo](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console).
   * En espera, la recopilación de elementos no utilizados del almacén de datos solo está disponible mediante **BlobGarbageCollection** MBean - `startBlobGC()`. El **RepositoryManagement **MBean no está disponible en espera.

   >[!NOTE]
   >
   >En caso de que no utilice un almacén de datos compartido, la recolección de elementos no utilizados deberá ejecutarse primero en el almacén primario y, a continuación, en el modo de espera.

