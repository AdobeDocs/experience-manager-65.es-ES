---
title: Ejecución de AEM con el modo de espera pasiva TarMK
seo-title: How to Run AEM with TarMK Cold Standby
description: Aprenda a crear, configurar y mantener una configuración de modo de espera pasiva de TarMK.
seo-description: Learn how to create, configure and maintain a TarMK Cold Standby setup.
uuid: 004fdf3e-517c-452b-8db1-a47d6b31d8ba
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9559e837-a87e-4ee7-8ca6-13b42c74e6bf
docset: aem65
feature: Configuring
exl-id: dadde3ee-d60c-4b87-9af0-a12697148161
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2730'
ht-degree: 0%

---

# Ejecución de AEM con el modo de espera pasiva TarMK{#how-to-run-aem-with-tarmk-cold-standby}

## Introducción {#introduction}

La capacidad de espera pasiva del micronúcleo Tar permite que una o más instancias de AEM en espera se conecten a una instancia principal. El proceso de sincronización es de una manera, lo que significa que solo se realiza de las instancias principales a las de espera.

El propósito de las instancias en espera es garantizar una copia de datos activa del repositorio principal y garantizar un cambio rápido sin pérdida de datos en caso de que el maestro no esté disponible por ningún motivo.

El contenido se sincroniza linealmente entre la instancia principal y las instancias en espera sin que se verifique la integridad de los archivos o repositorios dañados. Debido a este diseño, las instancias en espera son copias exactas de la instancia principal y no pueden ayudar a mitigar las incoherencias en las instancias principales.

>[!NOTE]
>
>La función Modo de espera en frío está diseñada para asegurar escenarios en los que se requiere alta disponibilidad en **author** instancias. Para situaciones en las que se requiere alta disponibilidad, se requiere **publicar** instancias que utilizan el núcleo Tar Micro, Adobe recomienda utilizar un conjunto de servidores de publicación.
>
>Para obtener información sobre implementaciones más disponibles, consulte la [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md) página.

>[!NOTE]
>
>Cuando se configura la instancia de espera o se deriva del nodo primario, solo permite el acceso a la siguiente consola (para actividades relacionadas con la administración):
>
>* Consola web OSGI
>
>No se puede acceder a otras consolas.

## Funcionamiento {#how-it-works}

En la instancia de AEM principal, se abre un puerto TCP que está escuchando los mensajes entrantes. Actualmente, hay dos tipos de mensajes que los esclavos enviarán al maestro:

* un mensaje que solicita el ID del segmento del encabezado actual
* un mensaje que solicite datos de segmentos con un ID especificado

La espera solicita periódicamente el ID de segmento del encabezado actual del encabezado principal. Si el segmento es localmente desconocido, se recuperará. Si ya está presente, los segmentos se comparan y los segmentos a los que se hace referencia también se solicitarán, si es necesario.

>[!NOTE]
>
>Las instancias en espera no reciben ningún tipo de solicitudes, ya que se ejecutan en modo de solo sincronización. La única sección disponible en una instancia de espera es la Consola Web, para facilitar la configuración de paquetes y servicios.

Una implementación típica de modo en espera pasiva de TarMK:

![imagen_1](assets/chlimage_1.png)

## Otras características {#other-characteristics}

### Solidez {#robustness}

El flujo de datos está diseñado para detectar y gestionar automáticamente los problemas relacionados con la conexión y la red. Todos los paquetes están empaquetados con sumas de comprobación y tan pronto como se activan los problemas con la conexión o los paquetes dañados, se activan mecanismos de reintento.

#### Actuación {#performance}

Habilitar el modo de espera en frío TarMK en la instancia principal casi no tiene ningún impacto medible en el rendimiento. El consumo adicional de CPU es muy bajo y el disco duro adicional y la E/S de red no deben producir problemas de rendimiento.

En el modo de espera, puede esperar un alto consumo de CPU durante el proceso de sincronización. Debido al hecho de que el procedimiento no está multiproceso, no se puede acelerar usando varios núcleos. Si no se cambia ni transfiere ningún dato, no habrá actividad que se pueda medir. La velocidad de conexión variará según el hardware y el entorno de red, pero no depende del tamaño del repositorio o del uso de SSL. Debe tener esto en cuenta cuando estime el tiempo necesario para una sincronización inicial o cuando se hayan cambiado muchos datos mientras tanto en el nodo principal.

#### Seguridad {#security}

Suponiendo que todas las instancias se ejecuten en la misma zona de seguridad de intranet, el riesgo de una infracción de seguridad se reduce considerablemente. Sin embargo, puede agregar una capa de seguridad adicional habilitando conexiones SSL entre los esclavos y el maestro. Al hacerlo, se reduce la posibilidad de que los datos se vean comprometidos por un intermediario.

Además, puede especificar las instancias en espera que pueden conectarse restringiendo la dirección IP de las solicitudes entrantes. Esto debería ayudar a garantizar que nadie en la intranet pueda copiar el repositorio.

>[!NOTE]
>
>Se recomienda agregar un equilibrador de carga entre Dispatcher y los servidores que forman parte de la configuración del modo de espera pasiva. El equilibrador de carga debe configurarse para dirigir el tráfico del usuario solo a la variable **principal** para garantizar la coherencia y evitar que el contenido se copie en la instancia de espera por otros medios que no sean el mecanismo de espera pasiva.

## Creación de una configuración de espera pasiva AEM TarMK {#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>El PID para el almacén de nodos del segmento y el servicio de almacenamiento en espera ha cambiado en AEM 6.3 en comparación con las versiones anteriores de la siguiente manera:
>
>* de org.apache.jackrabbit.oak.**plugins**.segment.standby.store.StandbyStoreService a org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService
>* de org.apache.jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService para org.apache.jackrabbit.oak.segment.SegmentNodeStoreService
>
>Asegúrese de realizar los ajustes de configuración necesarios para reflejar este cambio.

Para crear una configuración de espera en frío de TarMK, primero debe crear las instancias en espera realizando una copia del sistema de archivos de toda la carpeta de instalación del primario a una nueva ubicación. A continuación, puede iniciar cada instancia con un modo de ejecución que especifique su función ( `primary` o `standby`).

A continuación se muestra el procedimiento que debe seguirse para crear una configuración con una instancia maestra y una instancia de espera:

1. Instalar AEM.

1. Cierre la instancia y copie su carpeta de instalación en la ubicación desde la que se ejecutará la instancia de espera en frío. Incluso si se ejecuta desde diferentes equipos, asegúrese de dar a cada carpeta un nombre descriptivo (como *aem-primary* o *aem-standby*) para diferenciar entre las instancias.
1. Vaya a la carpeta de instalación de la instancia principal y:

   1. Compruebe y elimine cualquier configuración OSGi anterior que pueda tener en `aem-primary/crx-quickstart/install`

   1. Cree una carpeta llamada `install.primary` under `aem-primary/crx-quickstart/install`

   1. Cree las configuraciones necesarias para el almacén de nodos y el almacén de datos preferidos en `aem-primary/crx-quickstart/install/install.primary`
   1. Cree un archivo llamado `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config` en la misma ubicación y configúrela según corresponda. Para obtener más información sobre las opciones de configuración, consulte [Configuración](/help/sites-deploying/tarmk-cold-standby.md#configuration).

   1. Si utiliza una instancia AEM TarMK con un almacén de datos externo, cree una carpeta denominada `crx3` under `aem-primary/crx-quickstart/install` named `crx3`

   1. Coloque el archivo de configuración del almacén de datos en la variable `crx3` carpeta.

   Si, por ejemplo, está ejecutando una instancia AEM TarMK con un almacén de datos de archivos externo, necesita estos archivos de configuración:

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`

   A continuación, encontrará configuraciones de muestra para la instancia principal:

   **Ejemplo de** **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

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

1. Inicie el principal asegurándose de especificar el modo de ejecución principal:

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. Cree un nuevo registrador de registros de Apache Sling para la **org.apache.jackrabbit.oak.segment** paquete. Establezca el nivel de registro en &quot;Depurar&quot; y dirija su salida de registro a un archivo de registro independiente, como */logs/tarmk-coldstandby.log*. Para obtener más información, consulte [Registro](/help/sites-deploying/configure-logging.md).
1. Vaya a la ubicación del **secundario** e iníciela ejecutando el jar.
1. Cree la misma configuración de registro que para el primario. A continuación, detenga la instancia.
1. A continuación, prepare la instancia de espera. Para ello, realice los mismos pasos que para la instancia principal:

   1. Elimine los archivos que pueda tener en `aem-standby/crx-quickstart/install`.
   1. Cree una nueva carpeta llamada `install.standby` under `aem-standby/crx-quickstart/install`

   1. Cree dos archivos de configuración llamados:

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   1. Cree una nueva carpeta llamada `crx3` under `aem-standby/crx-quickstart/install`

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

1. Inicie el **secundario** mediante el modo de ejecución en espera:

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

El servicio también se puede configurar mediante la consola web mediante:

1. Accediendo a la consola web en: *https://serveraddress:serverport/system/console/configMgr*
1. Buscando un servicio llamado **Servicio de espera pasiva de Apache Jackrabbit Oak Segment Tar** y haga doble clic en ella para editar la configuración.
1. Guarde la configuración y reinicie las instancias para que la nueva configuración pueda tener efecto.

>[!NOTE]
>
>Puede comprobar la función de una instancia en cualquier momento comprobando la presencia de la variable **principal** o **secundario** modos de ejecución en la consola web de configuración de Sling.
>
>Para ello, vaya a *https://localhost:4502/system/console/status-slingsettings* y comprobando **&quot;Modos de ejecución&quot;** línea.

## Primera sincronización {#first-time-synchronization}

Una vez finalizada la preparación y iniciada la espera por primera vez, habrá mucho tráfico de red entre las instancias a medida que la espera alcance el principal. Puede consultar los registros para observar el estado de la sincronización.

En espera *tarmk-coldstandby.log*, verá entradas como las siguientes:

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

En el informe *error.log*, debería ver una entrada como esta:

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

En el fragmento de registro anterior, *10.20.30.40* es la dirección IP del principal.

En el **principal** *tarmk-coldstandby.log*, verá entradas como las siguientes:

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message ‘s.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd’ from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

En este caso, el &quot;cliente&quot; mencionado en el registro es el **secundario** instancia.

Una vez que estas entradas dejen de aparecer en el registro, puede suponer con seguridad que el proceso de sincronización ha finalizado.

Aunque las entradas anteriores muestran que el mecanismo de sondeo está funcionando correctamente, a menudo resulta útil saber si hay datos que se estén sincronizando mientras se realiza la encuesta. Para ello, busque entradas como las siguientes:

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

Además, cuando se ejecuta con un `FileDataStore`, mensajes como los siguientes confirmarán que los archivos binarios se están transmitiendo correctamente:

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### Configuración {#configuration}

La siguiente configuración OSGi está disponible para el servicio de espera pasiva:

* **Configuración de persistencia:** si está habilitado, se almacenará la configuración en el repositorio en lugar de los archivos de configuración OSGi tradicionales. Se recomienda mantener esta configuración deshabilitada en los sistemas de producción para que la configuración principal no se recupere mediante el modo de espera.

* **Modo (`mode`):** esto elegirá el modo de ejecución de la instancia.

* **Puerto (puerto):** el puerto que se utilizará para la comunicación. El valor predeterminado es `8023`.

* **Host principal (`primary.host`):** : el host de la instancia principal. Esta configuración solo es aplicable para la espera.
* **Intervalo de sincronización (`interval`):** : este ajuste determina el intervalo entre la solicitud de sincronización y solo es aplicable a la instancia de espera.

* **Intervalos IP permitidos (`primary.allowed-client-ip-ranges`):** - los rangos de IP desde los que el principal permitirá conexiones.
* **Seguro (`secure`):** Habilite el cifrado SSL. Para utilizar esta configuración, debe habilitarse en todas las instancias.
* **Tiempo de espera de lectura en espera (`standby.readtimeout`):** Tiempo de espera para solicitudes emitidas desde la instancia de espera en milisegundos. El valor predeterminado utilizado es 60000 (un minuto).

* **Limpieza automática en espera (`standby.autoclean`):** Llame al método de limpieza si el tamaño del almacén aumenta en un ciclo de sincronización.

>[!NOTE]
>
>Se recomienda que el principal y el en espera tengan ID de repositorio diferentes para que se puedan indexar separadamente para servicios como Descarga.
>
>La mejor manera de asegurarse de que esto se cubre es eliminando la variable *sling.id* en espera y reiniciando la instancia.

## Procedimientos de conmutación por error {#failover-procedures}

En caso de que la instancia principal falle por cualquier motivo, puede configurar una de las instancias en espera para que asuma la función de la instancia principal cambiando el modo de ejecución inicial como se detalla a continuación:

>[!NOTE]
>
>Los archivos de configuración también deben modificarse para que coincidan con los ajustes utilizados para la instancia principal.

1. Vaya a la ubicación en la que está instalada la instancia de espera y deténgalo.

1. En caso de que tenga un equilibrador de carga configurado con la configuración, puede quitar el principal de la configuración del equilibrador de carga en este momento.
1. Haga una copia de seguridad de `crx-quickstart` de la carpeta de instalación en espera. Se puede utilizar como punto de partida al configurar una nueva espera.

1. Reinicie la instancia utilizando el `primary` runmode:

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. Agregue el nuevo principal al equilibrador de carga.
1. Cree e inicie una nueva instancia de espera. Para obtener más información, consulte el procedimiento anterior en [Creación de una configuración de espera pasiva AEM TarMK](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup).

## Aplicación de revisiones a una configuración en espera pasiva {#applying-hotfixes-to-a-cold-standby-setup}

La forma recomendada de aplicar revisiones a una configuración de espera en frío es instalarlas en la instancia principal y luego clonarlas en una nueva instancia de espera en frío con las revisiones instaladas.

Para ello, siga los pasos descritos a continuación:

1. Para detener el proceso de sincronización en la instancia de espera en frío, vaya a la consola JMX y utilice el archivo **org.apache.jackrabbit.oak: Estado (&quot;En espera&quot;)**media. Para obtener más información sobre cómo hacerlo, consulte la sección sobre [Monitorización](#monitoring).
1. Detenga la instancia de espera en frío.
1. Instale la corrección en la instancia principal. Para obtener más información sobre cómo instalar una corrección, consulte [Cómo trabajar con paquetes](/help/sites-administering/package-manager.md).
1. Pruebe la instancia para ver si hay problemas después de la instalación.
1. Elimine la instancia de espera en frío eliminando su carpeta de instalación.
1. Detenga la instancia principal y clóquela realizando una copia del sistema de archivos de toda la carpeta de instalación en la ubicación de la espera en frío.
1. Vuelva a configurar el clon recién creado para que actúe como una instancia de espera en frío. Para obtener más información, consulte [Creación de una configuración de espera pasiva AEM TarMK.](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)
1. Inicie las instancias principal y de espera en frío.

## Monitoreo {#monitoring}

La función expone información usando JMX o MBeans. De este modo, puede inspeccionar el estado actual del modo de espera y del maestro mediante la función [Consola JMX](/help/sites-administering/jmx-console.md). La información se puede encontrar en un MBean de `type org.apache.jackrabbit.oak:type="Standby"`named `Status`.

**En espera**

Al observar una instancia de espera, se mostrará un nodo. El ID suele ser un UUID genérico.

Este nodo tiene cinco atributos de solo lectura:

* `Running:` valor booleano que indica si el proceso de sincronización se está ejecutando o no.

* `Mode:` Cliente: seguido del UUID utilizado para identificar la instancia. Tenga en cuenta que este UUID cambiará cada vez que se actualice la configuración.

* `Status:` una representación textual del estado actual (como `running` o `stopped`).

* `FailedRequests:`el número de errores consecutivos.
* `SecondsSinceLastSuccess:` número de segundos transcurridos desde la última comunicación correcta con el servidor. Se mostrará `-1` si no se ha realizado una comunicación con éxito.

También hay tres métodos invocables:

* `start():` inicia el proceso de sincronización.
* `stop():` detiene el proceso de sincronización.
* `cleanup():` ejecuta la operación de limpieza en espera.

**Principal**

Al observar el objeto principal se muestra cierta información general a través de un MBean cuyo valor de ID es el número de puerto que utiliza el servicio en espera TarMK (8023 de forma predeterminada). La mayoría de los métodos y atributos son los mismos que para la espera, pero algunos son diferentes:

* `Mode:` siempre mostrará el valor `primary`.

Además, se puede recuperar información para hasta 10 clientes (instancias en espera) conectados al maestro. El ID de MBean es el UUID de la instancia. No existen métodos invocables para estos MBeans, pero algunos atributos de solo lectura muy útiles:

* `Name:` el ID del cliente.
* `LastSeenTimestamp:` la marca de tiempo de la última solicitud en una representación textual.
* `LastRequest:` la última solicitud del cliente.
* `RemoteAddress:` la dirección IP del cliente.
* `RemotePort:` el puerto que el cliente utilizó para la última solicitud.
* `TransferredSegments:` el número total de segmentos transferidos a este cliente.
* `TransferredSegmentBytes:`el número total de bytes transferidos a este cliente.

## Mantenimiento del repositorio en espera pasiva {#cold-standby-repository-maintenance}

### Limpieza de revisión {#revision-clean}

>[!NOTE]
>
>Si se ejecuta [Limpieza de revisión en línea](/help/sites-deploying/revision-cleanup.md) en la instancia principal, no es necesario el procedimiento manual presentado a continuación. Además, si utiliza la limpieza de revisión en línea, la variable `cleanup ()` la operación en la instancia de espera se realizará automáticamente.

>[!NOTE]
>
>No ejecute la limpieza de revisiones sin conexión en espera. No es necesario y no reducirá el tamaño del almacén de segmentos.

Adobe recomienda ejecutar el mantenimiento de forma regular para evitar el crecimiento excesivo del repositorio a lo largo del tiempo. Para realizar manualmente el mantenimiento del repositorio en espera fría, siga los pasos a continuación:

1. Para detener el proceso de espera en la instancia de espera, vaya a la consola JMX y utilice el **org.apache.jackrabbit.oak: Estado (&quot;En espera&quot;)** grano. Para obtener más información sobre cómo hacerlo, consulte la sección anterior sobre [Monitorización](/help/sites-deploying/tarmk-cold-standby.md#monitoring).

1. Detenga la instancia de AEM principal.
1. Ejecute la herramienta de compactación de oak en la instancia principal. Para obtener más información, consulte [Mantenimiento del repositorio](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
1. Inicie la instancia principal.
1. Inicie el proceso de espera en la instancia de espera utilizando el mismo conjunto de datos JMX descrito en el primer paso.
1. Observe los registros y espere a que se complete la sincronización. Es posible que en este momento se observe un crecimiento sustancial en el repositorio de reserva.
1. Ejecute el `cleanup()` operación en la instancia de espera, utilizando el mismo archivo JMX descrito en el primer paso.

Puede tardar más de lo normal que la instancia de espera complete la sincronización con el principal, ya que la compactación sin conexión reescribe efectivamente el historial del repositorio, haciendo que el cálculo de los cambios en los repositorios tome más tiempo. También debe tenerse en cuenta que una vez que este proceso se complete, el tamaño del repositorio en espera será aproximadamente el mismo que el repositorio en el primario.

Como alternativa, el repositorio principal se puede copiar en el modo de espera manualmente después de ejecutar la compactación en el repositorio principal, reconstruyendo esencialmente el modo de espera cada vez que se ejecute la compactación.

### Recolección de papelera del almacén de datos {#data-store-garbage-collection}

Es importante ejecutar la recolección de basura en instancias del almacén de datos de archivos de vez en cuando, de lo contrario, los binarios borrados permanecerán en el sistema de archivos, y eventualmente llenarán la unidad. Para ejecutar la colección de residuos, siga el siguiente procedimiento:

1. Ejecute el mantenimiento del repositorio de espera en frío como se describe en la sección [above](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance).
1. Una vez completado el proceso de mantenimiento y reiniciadas las instancias:

   * En el almacén de datos principal, ejecute la colección de residuos del almacén de datos a través del bean JMX correspondiente, tal como se describe en [este artículo](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console).
   * En espera, la colección de residuos del almacén de datos solo está disponible a través de la variable **BlobGarbageCollection** MBean - `startBlobGC()`. El **RepositoryManagement **MBean no está disponible en espera.

   >[!NOTE]
   >
   >En caso de que no utilice un almacén de datos compartido, la colección de residuos primero tendrá que ejecutarse en el almacén principal y, a continuación, en el modo de espera.
