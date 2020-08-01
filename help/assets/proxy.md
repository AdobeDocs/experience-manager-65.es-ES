---
title: Desarrollo de proxy de [!DNL Assets]
description: Un proxy es [!DNL Experience Manager] instance that uses proxy workers to process jobs. Learn how to configure an [!DNL Experience Manager] un proxy, operaciones admitidas, componentes proxy y cómo desarrollar un trabajador proxy personalizado.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---


# [!DNL Assets] desarrollo de proxy {#assets-proxy-development}

[!DNL Adobe Experience Manager Assets] utiliza un proxy para distribuir el procesamiento para determinadas tareas.

Un proxy es una instancia de Experience Manager específica (y a veces independiente) que utiliza los trabajadores proxy como procesadores responsables de la gestión de un trabajo y la creación de un resultado. Un trabajador proxy puede utilizarse para una amplia variedad de tareas. En el caso de un [!DNL Assets] proxy, se puede utilizar para cargar recursos para procesarlos en Assets. Por ejemplo, el trabajador [proxy](indesign.md) IDS utiliza un [!DNL Adobe InDesign] servidor para procesar los archivos que se utilizan en Assets.

Cuando el proxy es una [!DNL Experience Manager] instancia independiente, esto ayuda a reducir la carga en las instancias de creación del Experience Manager. De forma predeterminada, [!DNL Assets] ejecuta las tareas de procesamiento de recursos en el mismo JVM (externalizado mediante proxy) para reducir la carga en la instancia de creación de Experience Manager.

## Proxy (acceso HTTP) {#proxy-http-access}

Hay un proxy disponible a través del servlet HTTP cuando está configurado para aceptar trabajos de procesamiento en: `/libs/dam/cloud/proxy`. Este servlet crea un trabajo de sling a partir de los parámetros publicados. A continuación, se agrega a la cola de trabajos proxy y se conecta al trabajador proxy correspondiente.

### Operaciones admitidas {#supported-operations}

* `job`

   **Requisitos**: el parámetro `jobevent` debe configurarse como un mapa de valores serializados. Se utiliza para crear un `Event` para un procesador de trabajo.

   **Resultado**: Añade un nuevo trabajo. Si se realiza correctamente, se devuelve una ID de trabajo única.

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

   **Requisitos**: se `jobid` debe establecer el parámetro.

   **Resultado**: Devuelve una representación JSON del nodo resultante tal como la creó el procesador de trabajos.

```shell
curl -u admin:admin -F":operation=result" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502   /libs/dam/cloud/proxy
```

* `resource`

   **Requisitos**: se debe establecer el parámetro jobid.

   **Resultado**: Devuelve un recurso asociado al trabajo dado.

```shell
curl -u admin:admin -F":operation=resource" -F"jobid=xxxxxxxxxxxx"
    -F"resourcePath=something.pdf" http://localhost:4502/libs/dam/cloud/proxy
```

* `remove`

   **Requisitos**: se debe establecer el parámetro jobid.

   **Resultados**: Quita un trabajo si se encuentra.

```shell
curl -u admin:admin -F":operation=remove" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502/libs/dam/cloud/proxy
```

### Proxy Worker {#proxy-worker}

Un trabajador proxy es un procesador responsable de gestionar un trabajo y crear un resultado. Los trabajadores residen en la instancia de proxy y deben implementar [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) para ser reconocidos como un trabajador proxy.

>[!NOTE]
>
>El programa de trabajo debe implementar [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) para ser reconocido como un programa de trabajo proxy.

### API de cliente {#client-api}

[`JobService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html) está disponible como un servicio OSGi que proporciona métodos para crear trabajos, eliminar trabajos y obtener resultados de dichos trabajos. La implementación predeterminada de este servicio (`JobServiceImpl`) utiliza el cliente HTTP para comunicarse con el servlet proxy remoto.

A continuación se muestra un ejemplo del uso de API:

```java
@Reference
 JobService proxyJobService;

 // to create a new job
 final Hashtable props = new Hashtable();
 props.put("someproperty", "some value");
 props.put(JobUtil.PROPERTY_JOB_TOPIC, "myworker/job"); // this is an identifier of the worker
 final String jobId = proxyJobService.addJob(props, new Asset[]{asset});

 // to check status (returns JobService.STATUS_FINISHED or JobService.STATUS_INPROGRESS)
 int status = proxyJobService.getStatus(jobId)

 // to get the result
 final String jsonString = proxyJobService.getResult(jobId);

 // to remove job and cleanup
 proxyJobService.removeJob(jobId);
```

### Configuraciones de Cloud Service {#cloud-service-configurations}

>[!NOTE]
>
>La documentación de referencia para la API de proxy está disponible en [`com.day.cq.dam.api.proxy`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/proxy/package-summary.html).

Tanto las configuraciones de trabajo proxy como las de proxy están disponibles mediante configuraciones de servicios en la nube, ya que se puede acceder a ellas desde la consola [!DNL Assets] Herramientas **o desde** `/etc/cloudservices/proxy`. Se espera que cada trabajador proxy agregue un nodo debajo `/etc/cloudservices/proxy` para los detalles de configuración específicos del trabajador (por ejemplo, `/etc/cloudservices/proxy/workername`).

>[!NOTE]
>
>Consulte Configuración [y configuración](indesign.md#configuring-the-proxy-worker-for-indesign-server) de [InDesign Server Proxy Worker y](../sites-developing/extending-cloud-config.md) Cloud Service para obtener más información.

A continuación se muestra un ejemplo del uso de API:

```java
@Reference(policy = ReferencePolicy.STATIC)
 ProxyConfig proxyConfig;

 // to get proxy config
 Configuration cloudConfig = proxyConfig.getConfiguration();
 final String value = cloudConfig.get("someProperty", "defaultValue");

 // to get worker config
 Configuration cloudConfig = proxyConfig.getConfiguration("workername");
 final String value = cloudConfig.get("someProperty", "defaultValue");
```

### Desarrollo de un trabajador proxy personalizado {#developing-a-customized-proxy-worker}

El trabajador [proxy de](indesign.md) IDS es un ejemplo de un trabajador [!DNL Assets] proxy que ya se ha proporcionado de forma predeterminada para externalizar el procesamiento de recursos de InDesign.

También puede desarrollar y configurar su propio [!DNL Assets] proxy para crear un trabajador especializado que distribuya y externalice sus tareas [!DNL Assets] de procesamiento.

La configuración de su propio trabajador proxy personalizado requiere que:

* Configure e implemente (mediante eventos Sling):

   * un tema de trabajo personalizado
   * un controlador de evento de trabajo personalizado

* A continuación, utilice la API de JobService para:

   * enviar el trabajo personalizado al proxy
   * administrar su trabajo

* Si desea utilizar el proxy desde un flujo de trabajo, debe implementar un paso externo personalizado mediante la API WorkflowExternalProcess y la API JobService.

El diagrama y los pasos siguientes detallan cómo proceder:

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>En los pasos siguientes, los equivalentes de InDesign se indican como ejemplos de referencia.

1. Se utiliza un trabajo [de](https://sling.apache.org/site/eventing-and-jobs.html) Sling, por lo que debe definir un tema de trabajo para el caso de uso.

   Como ejemplo, consulte `IDSJob.IDS_EXTENDSCRIPT_JOB` para el programa de trabajo proxy IDS.

1. El paso externo se utiliza para desencadenar el evento y luego esperar hasta que finalice; esto se realiza sondeando en el identificador. Debe desarrollar su propio paso para implementar la nueva funcionalidad.

   Implemente un `WorkflowExternalProcess`, luego utilice la API de JobService y el tema de su trabajo para preparar un evento de trabajo y enviarlo al JobService (un servicio OSGi).

   Por ejemplo, consulte `INDDMediaExtractProcess`.java para el programa de trabajo proxy IDS.

1. Implemente un controlador de trabajo para el tema. Este controlador requiere desarrollo para que realice la acción específica y se considere la implementación de trabajador.

   Como ejemplo, consulte `IDSJobProcessor.java` para el programa de trabajo proxy IDS.

1. Hacer uso de `ProxyUtil.java` en dam-commons. Esto le permite enviar trabajos a los trabajadores mediante el proxy de la presa.

>[!NOTE]
>
>Lo que el marco de trabajo del [!DNL Assets] proxy no proporciona de forma predeterminada es el mecanismo de agrupación.
>
>La [!DNL InDesign] integración permite el acceso de un grupo de [!DNL InDesign] servidores (IDSPool). Este agrupamiento es específico para [!DNL InDesign] la integración y no para el marco [!DNL Assets] proxy.

>[!NOTE]
>
>Sincronización de resultados:
>
>Con n instancias que utilizan el mismo proxy, el resultado de procesamiento permanece con el proxy. Es tarea del cliente (autor Experience Manager) solicitar el resultado utilizando la misma identificación de trabajo única que se le ha dado al cliente al crear un trabajo. El proxy simplemente realiza el trabajo y mantiene el resultado listo para ser solicitado.
