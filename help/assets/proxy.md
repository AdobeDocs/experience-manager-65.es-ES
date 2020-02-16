---
title: Desarrollo de proxy de recursos
description: Un proxy es una instancia de AEM que utiliza trabajadores proxy para procesar trabajos. Obtenga información sobre cómo configurar un proxy AEM, las operaciones admitidas, los componentes proxy y cómo desarrollar un trabajador proxy personalizado.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Desarrollo de proxy de recursos {#assets-proxy-development}

Recursos Adobe Experience Manager (AEM) utiliza un proxy para distribuir el procesamiento para determinadas tareas.

Un proxy es una instancia específica (y a veces independiente) de AEM que utiliza los trabajadores proxy como procesadores responsables de gestionar un trabajo y crear un resultado. Un trabajador proxy puede utilizarse para una amplia variedad de tareas. En el caso de un proxy de Recursos AEM, esto se puede utilizar para cargar recursos para procesarlos en Recursos AEM. Por ejemplo, el trabajador [proxy](indesign.md) IDS utiliza un servidor de InDesign para procesar archivos que se utilizarán en Recursos AEM.

Cuando el proxy es una instancia de AEM independiente, esto ayuda a reducir la carga en las instancias de creación de AEM. De forma predeterminada, AEM Assets ejecuta las tareas de procesamiento de recursos en el mismo JVM (externalizado mediante proxy) para reducir la carga en la instancia de creación de AEM.

## Proxy (acceso HTTP) {#proxy-http-access}

Hay un proxy disponible a través del servlet HTTP cuando está configurado para aceptar trabajos de procesamiento en: `/libs/dam/cloud/proxy`. Este servlet crea un trabajo de sling a partir de los parámetros publicados. A continuación, se agrega a la cola de trabajos proxy y se conecta al trabajador proxy correspondiente.

### Operaciones admitidas {#supported-operations}

* `job`

   **Requisitos**: el parámetro `jobevent` debe configurarse como un mapa de valores serializados. Se utiliza para crear un `Event` para un procesador de trabajo.

   **Resultado**: Agrega un nuevo trabajo. Si se realiza correctamente, se devuelve una ID de trabajo única.

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

   **Requisitos**: se `jobid` debe establecer el parámetro.

   **Resultado**: Devuelve una representación JSON del nodo de resultado tal como la creó el procesador de trabajos.

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

```xml
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

Tanto las configuraciones de trabajo proxy como las de proxy están disponibles mediante configuraciones de servicios en la nube, ya que se puede acceder a ellas desde la consola de **herramientas** de AEM Assets o desde `/etc/cloudservices/proxy`. Se espera que cada trabajador proxy agregue un nodo debajo `/etc/cloudservices/proxy` para los detalles de configuración específicos del trabajador (por ejemplo, `/etc/cloudservices/proxy/workername`).

>[!NOTE]
>
>Consulte Configuración [del trabajo proxy de](indesign.md#configuring-the-proxy-worker-for-indesign-server) Indesign Server y configuración [de](../sites-developing/extending-cloud-config.md) Cloud Services para obtener más información.

A continuación se muestra un ejemplo del uso de API:

```xml
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

El trabajador [proxy](indesign.md) IDS es un ejemplo de un trabajador proxy de Recursos AEM que ya se ha incorporado para externalizar el procesamiento de recursos de Indesign.

También puede desarrollar y configurar su propio trabajador proxy de Recursos AEM para crear un trabajador especializado que distribuya y externalice sus tareas de procesamiento de Recursos AEM.

La configuración de su propio trabajador proxy personalizado requiere que:

* Configure e implemente (mediante eventos Sling):

   * un tema de trabajo personalizado
   * un controlador de eventos de trabajo personalizado

* A continuación, utilice la API de JobService para:

   * enviar el trabajo personalizado al proxy
   * administrar su trabajo

* Si desea utilizar el proxy desde un flujo de trabajo, debe implementar un paso externo personalizado mediante la API WorkflowExternalProcess y la API JobService.

El diagrama y los pasos siguientes detallan cómo proceder:

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>En los pasos siguientes, los equivalentes de Indesign se indican como ejemplos de referencia.

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
>Lo que el marco proxy de Recursos AEM no proporciona de forma predeterminada es el mecanismo de agrupación.
>
>La integración de InDesign permite el acceso a un grupo de servidores de indesign (IDSPool). Este agrupamiento es específico de la integración de Indesign y no forma parte del marco proxy de AEM Assets.

>[!NOTE]
>
>Sincronización de resultados:
>
>Con n instancias que utilizan el mismo proxy, el resultado de procesamiento permanece con el proxy. Es tarea del cliente (AEM Author) solicitar el resultado utilizando la misma ID de trabajo única que se ha dado al cliente en la creación de un trabajo. El proxy simplemente realiza el trabajo y mantiene el resultado listo para ser solicitado.
