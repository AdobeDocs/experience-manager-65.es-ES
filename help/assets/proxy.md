---
title: '"[!DNL Assets] desarrollo de proxy"'
description: Un proxy es un [!DNL Experience Manager] instancia que utiliza trabajadores proxy para procesar trabajos. Obtenga información sobre cómo configurar un [!DNL Experience Manager] proxy, operaciones compatibles, componentes proxy y cómo desarrollar un trabajador proxy personalizado.
contentOwner: AG
role: Admin, Architect
exl-id: 42fff236-b4e1-4f42-922c-97da32a933cf
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 0%

---

# [!DNL Assets] desarrollo de proxy {#assets-proxy-development}

[!DNL Adobe Experience Manager Assets] utiliza un proxy para distribuir el procesamiento para determinadas tareas.

Un proxy es una instancia de Experience Manager específica (y a veces independiente) que utiliza los trabajadores proxy como procesadores responsables de gestionar un trabajo y crear un resultado. Un trabajador proxy puede utilizarse para una amplia variedad de tareas. En el caso de un [!DNL Assets] proxy esto se puede usar para cargar recursos para procesarlos en Assets. Por ejemplo, la variable [Trabajador de proxy IDS](indesign.md) utiliza un [!DNL Adobe InDesign] Servidor para procesar archivos para utilizarlos en Assets.

Cuando el proxy es un [!DNL Experience Manager] esto ayuda a reducir la carga en la [!DNL Experience Manager] crear instancias. De forma predeterminada, [!DNL Assets] ejecuta las tareas de procesamiento de recursos en la misma JVM (externalizada mediante proxy) para reducir la carga en la variable [!DNL Experience Manager] crear instancia.

## Proxy (acceso HTTP) {#proxy-http-access}

Hay un proxy disponible a través del servlet HTTP cuando está configurado para aceptar trabajos de procesamiento en: `/libs/dam/cloud/proxy`. Este servlet crea un trabajo de sling a partir de los parámetros registrados. A continuación, esto se agrega a la cola de trabajos del proxy y se conecta al trabajador del proxy adecuado.

### Operaciones compatibles {#supported-operations}

* `job`

   **Requisitos**: el parámetro `jobevent` debe establecerse como mapa de valores serializado. Se utiliza para crear un `Event` para un procesador de trabajos.

   **Resultado**: Agrega un nuevo trabajo. Si se realiza correctamente, se devuelve un identificador de trabajo único.

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

   **Requisitos**: el parámetro `jobid` debe estar configurado.

   **Resultado**: Devuelve una representación JSON del nodo de resultado creado por el procesador de trabajos.

```shell
curl -u admin:admin -F":operation=result" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502   /libs/dam/cloud/proxy
```

* `resource`

   **Requisitos**: se debe establecer el parámetro jobid .

   **Resultado**: Devuelve un recurso asociado al trabajo dado.

```shell
curl -u admin:admin -F":operation=resource" -F"jobid=xxxxxxxxxxxx"
    -F"resourcePath=something.pdf" http://localhost:4502/libs/dam/cloud/proxy
```

* `remove`

   **Requisitos**: se debe establecer el parámetro jobid .

   **Resultados**: Elimina un trabajo si se encuentra.

```shell
curl -u admin:admin -F":operation=remove" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502/libs/dam/cloud/proxy
```

### Trabajador de proxy {#proxy-worker}

Un trabajador proxy es un procesador responsable de gestionar un trabajo y crear un resultado. Los trabajadores residen en la instancia de proxy y deben implementar [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) para ser reconocido como trabajador proxy.

>[!NOTE]
>
>El trabajador debe implementar [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) para ser reconocido como trabajador proxy.

### API de cliente {#client-api}

[`JobService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html) está disponible como servicio de OSGi que proporciona métodos para crear trabajos, eliminarlos y obtener resultados de esos trabajos. La implementación predeterminada de este servicio (`JobServiceImpl`) utiliza el cliente HTTP para comunicarse con el servlet proxy remoto.

El siguiente es un ejemplo de uso de API:

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

### configuraciones del Cloud Service {#cloud-service-configurations}

<!-- TBD: Cannot find com.day.cq.dam.api.proxy at https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html which were generated in May 2020. Hiding this broken link for now.
>[!NOTE]
>
>Reference documentation for the proxy API is available under [`com.day.cq.dam.api.proxy`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/proxy/package-summary.html).
-->

Las configuraciones de trabajo proxy y proxy están disponibles a través de configuraciones de servicios en la nube, a las que se puede acceder desde [!DNL Assets] **Herramientas** consola o en `/etc/cloudservices/proxy`. Se espera que cada trabajador proxy agregue un nodo en `/etc/cloudservices/proxy` para detalles de configuración específicos del trabajador (por ejemplo, `/etc/cloudservices/proxy/workername`).

>[!NOTE]
>
>Consulte [Configuración de InDesign Server Proxy Worker](indesign.md#configuring-the-proxy-worker-for-indesign-server) y [Configuración de Cloud Services](../sites-developing/extending-cloud-config.md) para obtener más información.

El siguiente es un ejemplo de uso de API:

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

### Desarrollo de un Trabajador de Proxy Personalizado {#developing-a-customized-proxy-worker}

La variable [Trabajador de proxy IDS](indesign.md) es un ejemplo de [!DNL Assets] trabajador proxy que ya se ha proporcionado de forma predeterminada para externalizar el procesamiento de recursos de InDesign.

También puede desarrollar y configurar sus propios [!DNL Assets] trabajador proxy para crear un trabajador especializado para distribuir y subcontratar su [!DNL Assets] tareas de procesamiento.

La configuración de su propio trabajador proxy personalizado requiere que:

* Configure e implemente (mediante eventos de Sling):

   * un tema de trabajo personalizado
   * un controlador de eventos de trabajo personalizado

* A continuación, utilice la API de JobService para:

   * envíe su trabajo personalizado al proxy
   * administrar su trabajo

* Si desea utilizar el proxy desde un flujo de trabajo, debe implementar un paso externo personalizado mediante la API WorkflowExternalProcess y la API JobService.

El diagrama y los pasos siguientes detallan cómo continuar:

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>En los pasos siguientes, los equivalentes de InDesign se indican como ejemplos de referencia.

1. A [Trabajo de Sling](https://sling.apache.org/site/eventing-and-jobs.html) por lo que debe definir un tema de trabajo para su caso de uso.

   Como ejemplo, consulte `IDSJob.IDS_EXTENDSCRIPT_JOB` para el programa de trabajo del proxy IDS.

1. El paso externo se utiliza para almacenar en déclencheur el evento y luego esperar hasta que finalice; esto se hace sondeando en el id. Debe desarrollar su propio paso para implementar la nueva funcionalidad.

   Implemente un `WorkflowExternalProcess`, utilice la API de JobService y el tema de su trabajo para preparar un evento de trabajo y enviarlo al JobService (un servicio de OSGi).

   Como ejemplo, consulte `INDDMediaExtractProcess`.java para el programa de trabajo del proxy IDS.

1. Implemente un controlador de trabajo para su tema. Este controlador requiere desarrollo para que realice su acción específica y se considere la implementación del trabajador.

   Como ejemplo, consulte `IDSJobProcessor.java` para el programa de trabajo del proxy IDS.

1. Utilizar `ProxyUtil.java` en dam-commons. Esto le permite enviar trabajos a los trabajadores usando el proxy de la represa.

>[!NOTE]
>
>Qué es [!DNL Assets] el marco de proxy no proporciona el mecanismo de agrupación predeterminado.
>
>La variable [!DNL InDesign] la integración permite el acceso de un grupo de [!DNL InDesign] servidores (IDSPool). Este agrupamiento es específico de [!DNL InDesign] integración y no parte de [!DNL Assets] estructura de proxy.

>[!NOTE]
>
>Sincronización de resultados:
>
>Con n instancias que utilizan el mismo proxy, el resultado de procesamiento permanece con el proxy. Es tarea del cliente (Autor Experience Manager) solicitar el resultado utilizando el mismo id de trabajo único que se dio al cliente en la creación de trabajos. El proxy simplemente realiza el trabajo y mantiene el resultado listo para ser solicitado.
