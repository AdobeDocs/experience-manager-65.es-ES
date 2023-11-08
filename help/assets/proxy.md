---
title: "[!DNL Assets] desarrollo de proxy"
description: Un proxy es un [!DNL Experience Manager] instancia que utiliza trabajadores proxy para procesar trabajos. Obtenga información sobre cómo configurar un [!DNL Experience Manager] proxy, operaciones admitidas, componentes proxy y cómo desarrollar un trabajador proxy personalizado.
contentOwner: AG
role: Admin, Architect
exl-id: 42fff236-b4e1-4f42-922c-97da32a933cf
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 0%

---

# [!DNL Assets] desarrollo de proxy {#assets-proxy-development}

[!DNL Adobe Experience Manager Assets] utiliza un proxy para distribuir el procesamiento de determinadas tareas.

Un proxy es una instancia de Experience Manager específica (y a veces independiente) que utiliza los proxies como procesadores responsables de gestionar un trabajo y crear un resultado. Un trabajador proxy puede utilizarse para una amplia variedad de tareas. Si hay un [!DNL Assets] proxy: esto se puede utilizar para cargar recursos para procesarlos en Assets. Por ejemplo, la variable [Trabajador proxy IDS](indesign.md) utiliza un [!DNL Adobe InDesign] Servidor para procesar archivos para usarlos en Assets.

Cuando el proxy es un servidor independiente [!DNL Experience Manager] Esto ayuda a reducir la carga de la [!DNL Experience Manager] instancia(s) de creación. De forma predeterminada, [!DNL Assets] ejecuta las tareas de procesamiento de recursos en la misma JVM (externalizadas mediante proxy) para reducir la carga en la [!DNL Experience Manager] instancia de creación.

## Proxy (acceso HTTP) {#proxy-http-access}

Un proxy está disponible a través del servlet HTTP cuando está configurado para aceptar trabajos de procesamiento en: `/libs/dam/cloud/proxy`. Este servlet crea un trabajo de sling a partir de los parámetros registrados. A continuación, se agrega a la cola de trabajos del proxy y se conecta al trabajador del proxy correspondiente.

### Operaciones admitidas {#supported-operations}

* `job`

  **Requisitos**: el parámetro `jobevent` debe establecerse como un mapa de valores serializados. Se utiliza para crear un `Event` para un procesador de trabajos.

  **Resultado**: Añade un nuevo trabajo. Si se realiza correctamente, se devuelve un ID de trabajo único.

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

  **Requisitos**: el parámetro `jobid` debe estar configurado.

  **Resultado**: Devuelve una representación JSON del nodo resultante creado por el procesador de trabajos.

```shell
curl -u admin:admin -F":operation=result" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502   /libs/dam/cloud/proxy
```

* `resource`

  **Requisitos**: se debe establecer el parámetro jobid.

  **Resultado**: Devuelve un recurso asociado al trabajo determinado.

```shell
curl -u admin:admin -F":operation=resource" -F"jobid=xxxxxxxxxxxx"
    -F"resourcePath=something.pdf" http://localhost:4502/libs/dam/cloud/proxy
```

* `remove`

  **Requisitos**: se debe establecer el parámetro jobid.

  **Resultados**: elimina un trabajo si se encuentra.

```shell
curl -u admin:admin -F":operation=remove" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502/libs/dam/cloud/proxy
```

### Trabajador Proxy {#proxy-worker}

Un trabajador proxy es un procesador responsable de gestionar un trabajo y crear un resultado. Los trabajadores residen en la instancia de proxy y deben implementar [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) para que se reconozca como trabajador proxy.

>[!NOTE]
>
>El trabajador debe implementar [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) para que se reconozca como trabajador proxy.

### API de cliente {#client-api}

[`JobService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html) está disponible como servicio OSGi que proporciona métodos para crear trabajos, eliminar trabajos y obtener resultados de esos trabajos. La implementación predeterminada de este servicio (`JobServiceImpl`) utiliza el cliente HTTP para comunicarse con el servlet proxy remoto.

A continuación se muestra un ejemplo de uso de API:

```java
@Reference
 JobService proxyJobService;

 // to create a job
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

### Configuraciones del Cloud Service {#cloud-service-configurations}

<!-- TBD: Cannot find com.day.cq.dam.api.proxy at https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html which were generated in May 2020. Hiding this broken link for now.
>[!NOTE]
>
>Reference documentation for the proxy API is available under [`com.day.cq.dam.api.proxy`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/proxy/package-summary.html).
-->

Las configuraciones de trabajo de proxy y proxy están disponibles a través de las configuraciones de los servicios en la nube, como accesibles desde el [!DNL Assets] **Herramientas** consola o en `/etc/cloudservices/proxy`. Se espera que cada trabajador proxy agregue un nodo en `/etc/cloudservices/proxy` para detalles de configuración específicos del trabajador (por ejemplo, `/etc/cloudservices/proxy/workername`).

>[!NOTE]
>
>Consulte [Configuración de InDesign Server Proxy Worker](indesign.md#configuring-the-proxy-worker-for-indesign-server) y [Configuración de Cloud Service](../sites-developing/extending-cloud-config.md) para obtener más información.

A continuación se muestra un ejemplo de uso de API:

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

El [Trabajador proxy IDS](indesign.md) es un ejemplo de [!DNL Assets] trabajador proxy que ya se proporciona de forma predeterminada para externalizar el procesamiento de recursos de InDesign.

También puede desarrollar y configurar sus propios [!DNL Assets] trabajador proxy para crear un trabajador especializado para distribuir y externalizar su [!DNL Assets] tareas de procesamiento.

La configuración de su propio trabajador de proxy personalizado requiere lo siguiente:

* Configurar e implementar (con eventos de Sling):

   * un tema de trabajo personalizado
   * un controlador de eventos de trabajo personalizado

* A continuación, utilice la API de JobService para:

   * enviar el trabajo personalizado al proxy
   * administre su trabajo

* Si desea utilizar el proxy de un flujo de trabajo, debe implementar un paso externo personalizado mediante la API WorkflowExternalProcess y la API JobService.

El siguiente diagrama y pasos detallan cómo proceder:

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>En los pasos siguientes, se indican equivalentes de InDesign como ejemplos de referencia.

1. A [Trabajo de Sling](https://sling.apache.org/site/eventing-and-jobs.html) se utiliza, por lo que debe definir un tema de trabajo para el caso de uso.

   Como ejemplo, consulte `IDSJob.IDS_EXTENDSCRIPT_JOB` para el trabajador del proxy IDS.

1. El paso externo se utiliza para almacenar en déclencheur el evento y luego esperar hasta que termine; esto se hace sondeando el ID. Debe desarrollar su propio paso para implementar nuevas funciones.

   Implementación de un `WorkflowExternalProcess`A continuación, utilice la API del servicio de trabajos y el tema del trabajo para preparar un evento de trabajo y enviarlo al servicio de trabajos (un servicio OSGi).

   Como ejemplo, consulte `INDDMediaExtractProcess`.java para el trabajador del proxy IDS.

1. Implemente un controlador de trabajo para el tema. Este controlador requiere desarrollo para que realice la acción específica y se considere la implementación de trabajador.

   Como ejemplo, consulte `IDSJobProcessor.java` para el trabajador del proxy IDS.

1. Utilizar de `ProxyUtil.java` en dam-commons. Esto permite enviar trabajos a los trabajadores mediante el proxy DAM.

>[!NOTE]
>
>¿Qué [!DNL Assets] el marco proxy no proporciona de forma predeterminada el mecanismo de grupo.
>
>El [!DNL InDesign] La integración de permite el acceso de un grupo de [!DNL InDesign] servidores de (IDSPool). Este conjunto es específico de [!DNL InDesign] integración y no forma parte del [!DNL Assets] marco proxy.

>[!NOTE]
>
>Sincronización de resultados:
>
>Con n instancias que utilizan el mismo proxy, el resultado del procesamiento permanece con el proxy. Es tarea del cliente (Autor Experience Manager) solicitar el resultado utilizando el mismo ID de trabajo único que se le proporcionó al cliente al crear el trabajo. El proxy simplemente realiza el trabajo y mantiene el resultado listo para solicitarlo.
