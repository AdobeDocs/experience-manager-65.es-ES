---
title: Interactuar con flujos de trabajo mediante programación
seo-title: Interacting with Workflows Programmatically
description: Aprenda a interactuar con flujos de trabajo mediante programación en Adobe Experience Manager.
seo-description: null
uuid: a0f19fc6-b9bd-4b98-9c0e-fbf4f7383026
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: cb621332-a149-4f8d-9425-fd815b033c38
exl-id: 2b396850-e9fb-46d9-9daa-ebd410a9e1a5
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '2011'
ht-degree: 1%

---

# Interactuar con flujos de trabajo mediante programación{#interacting-with-workflows-programmatically}

Cuándo [personalización y ampliación de flujos de trabajo](/help/sites-developing/workflows-customizing-extending.md) puede acceder a los objetos de flujo de trabajo:

* [Uso de la API de Java de flujo de trabajo](#using-the-workflow-java-api)
* [Obtención de objetos de flujo de trabajo en scripts ECMA](#obtaining-workflow-objects-in-ecma-scripts)
* [Uso de la API de REST de flujo de trabajo](#using-the-workflow-rest-api)

## Uso de la API de Java de flujo de trabajo {#using-the-workflow-java-api}

La API de Java del flujo de trabajo consiste en [`com.adobe.granite.workflow`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/package-summary.html) y varios subpaquetes. El miembro más significativo de la API es el `com.adobe.granite.workflow.WorkflowSession` clase. El `WorkflowSession` proporciona acceso a los objetos de flujo de trabajo en tiempo de diseño y en tiempo de ejecución:

* modelos de flujo de trabajo
* elementos de trabajo
* instancias de flujo de trabajo
* datos de flujo de trabajo
* elementos de bandeja de entrada

La clase también proporciona varios métodos para intervenir en los ciclos de vida del flujo de trabajo.

En la tabla siguiente se proporcionan vínculos a la documentación de referencia de varios objetos Java clave que se pueden utilizar al interactuar mediante programación con flujos de trabajo. En los ejemplos siguientes se muestra cómo obtener y utilizar los objetos de clase en el código.

| Características | Objetos |
|---|---|
| Acceso a un flujo de trabajo | [`WorkflowSession`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html) |
| Ejecución y consulta de una instancia de flujo de trabajo | [`Workflow`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html)</br>[`WorkItem`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkItem.html)</br>[`WorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html) |
| Administración de un modelo de flujo de trabajo | [`WorkflowModel`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowModel.html)</br>[`WorkflowNode`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowNode.html)</br>[`WorkflowTransition`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowTransition.html) |
| Información para un nodo que está en el flujo de trabajo (o no) | [`WorkflowStatus`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html) |

## Obtención de objetos de flujo de trabajo en scripts ECMA {#obtaining-workflow-objects-in-ecma-scripts}

Como se describe en [Localización del script](/help/sites-developing/the-basics.md#locating-the-script)AEM , (a través de Apache Sling) proporciona un motor de scripts ECMA que ejecuta scripts ECMA del lado del servidor. El [`org.apache.sling.scripting.core.ScriptHelper`](https://sling.apache.org/apidocs/sling5/org/apache/sling/scripting/core/ScriptHelper.html) está disponible inmediatamente para los scripts como la clase `sling` variable.

El `ScriptHelper` proporciona acceso a la clase `SlingHttpServletRequest` que puede utilizar para obtener finalmente el `WorkflowSession` objeto; por ejemplo:

```
var wfsession = sling.getRequest().getResource().getResourceResolver().adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
```

## Uso de la API de REST de flujo de trabajo {#using-the-workflow-rest-api}

La consola de flujo de trabajo utiliza en gran medida la API de REST, por lo que esta página describe la API de REST para los flujos de trabajo.

>[!NOTE]
>
>La herramienta de línea de comandos curl permite utilizar la API de REST de flujo de trabajo para acceder a los objetos de flujo de trabajo y administrar los ciclos de vida de las instancias. Los ejemplos de esta página muestran el uso de la API de REST a través de la herramienta de línea de comandos curl.

La API de REST admite las siguientes acciones:

* inicio o detención de un servicio de flujo de trabajo
* crear, actualizar o eliminar modelos de flujo de trabajo
* [iniciar, suspender, reanudar o finalizar instancias de flujo de trabajo](/help/sites-administering/workflows.md#workflow-status-and-actions)
* completar o delegar elementos de trabajo

>[!NOTE]
>
>Al utilizar Firebug, una extensión de Firefox para el desarrollo web, es posible seguir el tráfico HTTP cuando se opera la consola. AEM Por ejemplo, puede comprobar los parámetros y los valores enviados al servidor de la con un `POST` solicitud.

AEM En esta página se da por hecho que se ejecuta en el host local en el puerto de `4502` y que el contexto de instalación es &quot; `/`&quot; (raíz). Si no es el caso de su instalación, los URI, a los que se aplican las solicitudes HTTP, deben adaptarse en consecuencia.

El procesamiento admitido para `GET` Solicitudes de es el procesamiento de JSON. Las direcciones URL de `GET` debería tener el `.json` extensión, por ejemplo:

`http://localhost:4502/etc/workflow.json`

### Administración de instancias de flujo de trabajo {#managing-workflow-instances}

Los siguientes métodos de solicitud HTTP se aplican a:

`http://localhost:4502/etc/workflow/instances`

<table>
 <tbody>
  <tr>
   <td>método de petición HTTP</td>
   <td>Acciones</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>Muestra las instancias de flujo de trabajo disponibles.</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td><p>Crea una nueva instancia de flujo de trabajo. Los parámetros son:<br /> - <code>model</code>: el ID (URI) del modelo de flujo de trabajo correspondiente<br /> - <code>payloadType</code>: que contiene el tipo de carga útil (por ejemplo, <code>JCR_PATH</code> o URL).<br /> La carga útil se envía como parámetro <code>payload</code>. A <code>201</code> (<code>CREATED</code>) se devuelve la respuesta con un encabezado de ubicación que contiene la dirección URL del nuevo recurso de instancia de flujo de trabajo.</p> </td>
  </tr>
 </tbody>
</table>

#### Administración de una instancia de flujo de trabajo por su estado {#managing-a-workflow-instance-by-its-state}

Los siguientes métodos de solicitud HTTP se aplican a:

`http://localhost:4502/etc/workflow/instances.{state}`

| método de petición HTTP | Acciones |
|---|---|
| `GET` | Muestra las instancias de flujo de trabajo disponibles y sus estados ( `RUNNING`, `SUSPENDED`, `ABORTED` o `COMPLETED`) |

#### Administración de una instancia de flujo de trabajo por su ID {#managing-a-workflow-instance-by-its-id}

Los siguientes métodos de solicitud HTTP se aplican a:

`http://localhost:4502/etc/workflow/instances/{id}`

<table>
 <tbody>
  <tr>
   <td>método de petición HTTP</td>
   <td>Acciones</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>Obtiene los datos de instancias (definición y metadatos), incluido el vínculo al modelo de flujo de trabajo correspondiente.</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>Cambia el estado de la instancia. El nuevo estado se envía como parámetro <code>state</code> y debe tener uno de los siguientes valores: <code>RUNNING</code>, <code>SUSPENDED</code>, o <code>ABORTED</code>.<br /> Si no se puede acceder al nuevo estado (por ejemplo, al suspender una instancia finalizada), <code>409</code> (<code>CONFLICT</code>) la respuesta se devuelve al cliente.</td>
  </tr>
 </tbody>
</table>

### Administrar modelos de flujo de trabajo {#managing-workflow-models}

Los siguientes métodos de solicitud HTTP se aplican a:

`http://localhost:4502/etc/workflow/models`

<table>
 <tbody>
  <tr>
   <td>método de petición HTTP</td>
   <td>Acciones</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>Muestra los modelos de flujo de trabajo disponibles.</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>Crea un nuevo modelo de flujo de trabajo. Si el parámetro <code>title</code> se envía, se crea un nuevo modelo con el título especificado. Adjuntar una definición de modelo JSON como parámetro <code>model</code> crea un nuevo modelo de flujo de trabajo según la definición proporcionada.<br /> A <code>201</code> Respuesta (<code>CREATED</code>) se devuelve con un encabezado de ubicación que contiene la dirección URL del nuevo recurso de modelo de flujo de trabajo.<br /> Lo mismo ocurre cuando se adjunta una definición de modelo como parámetro de fichero denominado <code>modelfile</code>.<br /> En ambos casos, la variable <code>model</code> y <code>modelfile</code> parámetros, un parámetro adicional llamado <code>type</code> es necesario para definir el formato de serialización. Se pueden integrar nuevos formatos de serialización mediante la API OSGI. Se entrega un serializador JSON estándar con el motor de flujo de trabajo. Su tipo es JSON. Consulte a continuación un ejemplo del formato.</td>
  </tr>
 </tbody>
</table>

Ejemplo: en el explorador, una solicitud a `http://localhost:4502/etc/workflow/models.json` genera una respuesta json similar a la siguiente:

```
[
    {"uri":"/var/workflow/models/activationmodel"}
    ,{"uri":"/var/workflow/models/dam/adddamsize"}
    ,{"uri":"/var/workflow/models/cloudconfigs/dtm-reactor/library-download"}
    ,{"uri":"/var/workflow/models/ac-newsletter-workflow-simple"}
    ,{"uri":"/var/workflow/models/dam/dam-create-language-copy"}
    ,{"uri":"/var/workflow/models/dam/dam-create-and-translate-language-copy"}
    ,{"uri":"/var/workflow/models/dam-indesign-proxy"}
    ,{"uri":"/var/workflow/models/dam-xmp-writeback"}
    ,{"uri":"/var/workflow/models/dam-parse-word-documents"}
    ,{"uri":"/var/workflow/models/dam/process_subasset"}
    ,{"uri":"/var/workflow/models/dam/dam_set_last_modified"}
    ,{"uri":"/var/workflow/models/dam/dam-autotag-assets"}
    ,{"uri":"/var/workflow/models/dam/update_asset"}
    ,{"uri":"/var/workflow/models/dam/update_asset_offloading"}
    ,{"uri":"/var/workflow/models/dam/dam-update-language-copy"}
    ,{"uri":"/var/workflow/models/dam/update_from_lightbox"}
    ,{"uri":"/var/workflow/models/cloudservices/DTM_bundle_download"}
    ,{"uri":"/var/workflow/models/dam/dam_download_asset"}
    ,{"uri":"/var/workflow/models/dam/dynamic-media-encode-video"}
    ,{"uri":"/var/workflow/models/dam/dynamic-media-video-thumbnail-replacement"}
    ,{"uri":"/var/workflow/models/dam/dynamic-media-video-user-uploaded-thumbnail"}
    ,{"uri":"/var/workflow/models/newsletter_bounce_check"}
    ,{"uri":"/var/workflow/models/projects/photo_shoot_submission"}
    ,{"uri":"/var/workflow/models/projects/product_photo_shoot"}
    ,{"uri":"/var/workflow/models/projects/approval_workflow"}
    ,{"uri":"/var/workflow/models/prototype-01"}
    ,{"uri":"/var/workflow/models/publish_example"}
    ,{"uri":"/var/workflow/models/publish_to_campaign"}
    ,{"uri":"/var/workflow/models/screens/publish_to_author_bin"}
    ,{"uri":"/var/workflow/models/s7dam/request_to_publish_to_youtube"}
    ,{"uri":"/var/workflow/models/projects/request_copy"}
    ,{"uri":"/var/workflow/models/projects/request_email"}
    ,{"uri":"/var/workflow/models/projects/request_landing_page"}
    ,{"uri":"/var/workflow/models/projects/request_launch"}
    ,{"uri":"/var/workflow/models/request_for_activation"}
    ,{"uri":"/var/workflow/models/request_for_deactivation"}
    ,{"uri":"/var/workflow/models/request_for_deletion"}
    ,{"uri":"/var/workflow/models/request_for_deletion_without_deactivation"}
    ,{"uri":"/var/workflow/models/request_to_complete_move_operation"}
    ,{"uri":"/var/workflow/models/reverse_replication"}
    ,{"uri":"/var/workflow/models/salesforce-com-export"}
    ,{"uri":"/var/workflow/models/scene7"}
    ,{"uri":"/var/workflow/models/scheduled_activation"}
    ,{"uri":"/var/workflow/models/scheduled_deactivation"}
    ,{"uri":"/var/workflow/models/screens/screens-update-asset"}
    ,{"uri":"/var/workflow/models/translation"}
    ,{"uri":"/var/workflow/models/s7dam/request_to_remove_from_youtube"}
    ,{"uri":"/var/workflow/models/wcm-translation/create_language_copy"}
    ,{"uri":"/var/workflow/models/wcm-translation/prepare_translation_project"}
    ,{"uri":"/var/workflow/models/wcm-translation/translate-i18n-dictionary"}
    ,{"uri":"/var/workflow/models/wcm-translation/sync_translation_job"}
    ,{"uri":"/var/workflow/models/wcm-translation/translate-language-copy"}
    ,{"uri":"/var/workflow/models/wcm-translation/update_language_copy"}
]
```

#### Administración de un modelo de flujo de trabajo específico {#managing-a-specific-workflow-model}

Los siguientes métodos de solicitud HTTP se aplican a:

`http://localhost:4502*{uri}*`

Donde `*{uri}*` es la ruta al nodo del modelo en el repositorio.

<table>
 <tbody>
  <tr>
   <td>método de petición HTTP</td>
   <td>Acciones</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>Obtiene el <code>HEAD</code> versión del modelo (definición y metadatos).</td>
  </tr>
  <tr>
   <td><code>PUT</code></td>
   <td>Actualiza el <code>HEAD</code> versión del modelo (crea una nueva versión).<br /> La definición completa del modelo para la nueva versión del modelo debe añadirse como parámetro denominado <code>model</code>. Además, un <code>type</code> Este parámetro es necesario ya que al crear nuevos modelos y necesita tener el valor <code>JSON</code>.<br /> </td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>Igual que con el PUT. AEM Necesario porque los widgets de no admiten <code>PUT</code> operaciones.</td>
  </tr>
  <tr>
   <td><code>DELETE</code></td>
   <td>Elimina el modelo. Para resolver los problemas de servidor de seguridad/proxy, <code>POST</code> que contiene un <code>X-HTTP-Method-Override</code> entrada de encabezado con valor <code>DELETE</code> también se aceptarán como <code>DELETE</code> solicitud.</td>
  </tr>
 </tbody>
</table>

Ejemplo: en el explorador, una solicitud a `http://localhost:4502/var/workflow/models/publish_example.json` devuelve un valor `json` Una respuesta de similar al siguiente código:

```shell
{
  "id":"/var/workflow/models/publish_example",
  "title":"Publish Example",
  "version":"1.0",
  "description":"This example shows a simple review and publish process.",
  "metaData":
  {
    "multiResourceSupport":"true",
    "tags":"wcm,publish"
  },
  "nodes":
  [{
    "id":"node0",
    "type":"START",
    "title":"Start",
    "description":"The start node of the workflow.",
    "metaData":
    {
    }
  },
  {
    "id":"node1",
    "type":"PARTICIPANT",
    "title":"Validate Content",
    "description":"Validate the modified content.",
    "metaData":
    {
      "PARTICIPANT":"admin"
    }
  },
  {
    "id":"node2",
    "type":"PROCESS",
    "title":"Publish Content",
    "description":"Publish the modified content.",
    "metaData":
    {
      "PROCESS_AUTO_ADVANCE":"true",
      "PROCESS":"com.day.cq.wcm.workflow.process.ActivatePageProcess"
    }
  },
  {
    "id":"node3",
    "type":"END",
    "title":"End",
    "description":"The end node of the workflow.",
    "metaData":
    {
    }
  }],
  "transitions":
  [{
    "from":"node0",
    "to":"node1",
    "metaData":
    {
    }
  },
  {
    "from":"node1",
    "to":"node2",
    "metaData":
    {
    }
  },
  {
    "from":"node2",
    "to":"node3",
    "metaData":
    {
    }
  }
]}
```

#### Administrar un modelo de flujo de trabajo por su versión {#managing-a-workflow-model-by-its-version}

Los siguientes métodos de solicitud HTTP se aplican a:

`http://localhost:4502/etc/workflow/models/{id}.{version}`

| método de petición HTTP | Acciones |
|---|---|
| `GET` | Obtiene los datos del modelo en la versión dada (si existe). |

### Administración de bandejas de entrada (de usuario) {#managing-user-inboxes}

Los siguientes métodos de solicitud HTTP se aplican a:

`http://localhost:4502/bin/workflow/inbox`

<table>
 <tbody>
  <tr>
   <td>método de petición HTTP</td>
   <td>Acciones</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>Enumera los elementos de trabajo que se encuentran en la bandeja de entrada del usuario, que se identifica mediante los encabezados de autenticación HTTP.</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>Completa el elemento de trabajo cuyo URI se envía como parámetro <code>item</code> y avanza la instancia de flujo de trabajo correspondiente a los nodos siguientes, definidos por el parámetro <code>route</code> o <code>backroute</code> en caso de retroceder un paso.<br /> Si el parámetro <code>delegatee</code> , el elemento de trabajo identificado por el parámetro <code>item</code> se delega al participante especificado.</td>
  </tr>
 </tbody>
</table>

#### Administración de una bandeja de entrada (de usuario) mediante el ID de elemento de trabajo {#managing-a-user-inbox-by-the-workitem-id}

Los siguientes métodos de solicitud HTTP se aplican a:

`http://localhost:4502/bin/workflow/inbox/{id}`

| método de petición HTTP | Acciones |
|---|---|
| `GET` | Obtiene los datos (definición y metadatos) de la bandeja de entrada `WorkItem` identificado por su ID. |

## Ejemplos {#examples}

### Obtención de una lista de todos los flujos de trabajo en ejecución con sus ID {#how-to-get-a-list-of-all-running-workflows-with-their-ids}

Para obtener una lista de todos los flujos de trabajo en ejecución, haga una GET a:

`http://localhost:4502/etc/workflow/instances.RUNNING.json`

#### Cómo obtener una lista de todos los flujos de trabajo en ejecución con sus ID: REST mediante curl {#how-to-get-a-list-of-all-running-workflows-with-their-ids-rest-using-curl}

Ejemplo con curl:

```shell
curl -u admin:admin http://localhost:4502/etc/workflow/instances.RUNNING.json
```

El `uri` mostrado en los resultados puede utilizarse como instancia de `id` en otros comandos; por ejemplo:

```shell
[
    {"uri":"/etc/workflow/instances/server0/2017-03-08/request_for_activation_1"}
]
```

>[!NOTE]
>
>Esta `curl` El comando se puede utilizar con cualquier [estado del flujo de trabajo](/help/sites-administering/workflows.md#workflow-status-and-actions) en lugar de `RUNNING`.

### Cómo cambiar el título del flujo de trabajo {#how-to-change-the-workflow-title}

Para cambiar el **Título de flujo de trabajo** mostrado en la **Instancias** de la consola de flujo de trabajo, envíe un `POST` comando:

* hasta: `http://localhost:4502/etc/workflow/instances/{id}`

* con los siguientes parámetros:

   * `action`: su valor debe ser: `UPDATE`
   * `workflowTitle`: el título del flujo de trabajo

#### Cómo cambiar el Título del flujo de trabajo - REST mediante curl {#how-to-change-the-workflow-title-rest-using-curl}

Ejemplo con curl:

```shell
curl -u admin:admin -d "action=UPDATE&workflowTitle=myWorkflowTitle" http://localhost:4502/etc/workflow/instances/{id}

# for example
curl -u admin:admin -d "action=UPDATE&workflowTitle=myWorkflowTitle" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
```

### Cómo enumerar todos los modelos de flujo de trabajo {#how-to-list-all-workflow-models}

Para obtener una lista de todos los modelos de flujo de trabajo disponibles, haga una GET a:

`http://localhost:4502/etc/workflow/models.json`

#### Cómo enumerar todos los modelos de flujo de trabajo: REST mediante curl {#how-to-list-all-workflow-models-rest-using-curl}

Ejemplo con curl:

```shell
curl -u admin:admin http://localhost:4502/etc/workflow/models.json
```

>[!NOTE]
>
>Consulte también [Administrar modelos de flujo de trabajo](#managing-workflow-models).

### Obtención de un objeto WorkflowSession {#obtaining-a-workflowsession-object}

El `com.adobe.granite.workflow.WorkflowSession` La clase es adaptable desde `javax.jcr.Session` objeto o un `org.apache.sling.api.resource.ResourceResolver` objeto.

#### Obtención de un objeto WorkflowSession - Java {#obtaining-a-workflowsession-object-java}

En una secuencia de comandos JSP (o código Java para una clase de servlet), utilice el objeto de solicitud HTTP para obtener una `SlingHttpServletRequest` , que proporciona acceso a un objeto `ResourceResolver` objeto. Adaptar el `ResourceResolver` objeto a `WorkflowSession`.

```java
<%
%><%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false"
    import="com.adobe.granite.workflow.WorkflowSession,
  org.apache.sling.api.SlingHttpServletRequest"%><%

SlingHttpServletRequest slingReq = (SlingHttpServletRequest)request;
WorkflowSession wfSession = slingReq.getResourceResolver().adaptTo(WorkflowSession.class);
%>
```

#### Obtención de un objeto WorkflowSession: script ECMA {#obtaining-a-workflowsession-object-ecma-script}

Utilice el `sling` para obtener la variable `SlingHttpServletRequest` objeto que se utiliza para obtener un `ResourceResolver` objeto. Adaptar el `ResourceResolver` objeto a `WorkflowSession` objeto.

```
var wfsession = sling.getRequest().getResource().getResourceResolver().adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
```

### Creación, lectura o eliminación de modelos de flujo de trabajo {#creating-reading-or-deleting-workflow-models}

Los siguientes ejemplos muestran cómo acceder a los modelos de flujo de trabajo:

* El código para Java y el script ECMA utiliza el `WorkflowSession.createNewModel` método.
* El comando curl accede al modelo directamente mediante su dirección URL.

Los ejemplos utilizados son:

1. Creación de un modelo (con el ID `/var/workflow/models/mymodel/jcr:content/model`).
1. Elimine el modelo.

>[!NOTE]
>
>Al eliminar el modelo, se establece el `deleted` propiedad del modelo de `metaData` nodo secundario a `true`.
>
>La eliminación no elimina el nodo del modelo.

Al crear un nuevo modelo:

* El editor del modelo de flujo de trabajo requiere que los modelos utilicen una estructura de nodos específica debajo de `/var/workflow/models`. El nodo principal del modelo debe ser del tipo `cq:Page` teniendo un `jcr:content` con los siguientes valores de propiedad:

   * `sling:resourceType`: `cq/workflow/components/pages/model`
   * `cq:template`: `/libs/cq/workflow/templates/model`

  Al crear un modelo, primero debe crearlo `cq:Page` y utilice su `jcr:content` nodo como nodo principal del nodo de modelo.

* El `id` El argumento que algunos métodos requieren para identificar el modelo es la ruta absoluta del nodo del modelo en el repositorio:

  `/var/workflow/models/<*model_name>*/jcr:content/model`

  >[!NOTE]
  >
  >Consulte [Cómo enumerar todos los modelos de flujo de trabajo](#how-to-list-all-workflow-models).

#### Creación, lectura o eliminación de modelos de flujo de trabajo: Java {#creating-reading-or-deleting-workflow-models-java}

```java
<%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false" import="com.adobe.granite.workflow.WorkflowSession,
                 com.adobe.granite.workflow.model.WorkflowModel,
             org.apache.sling.api.SlingHttpServletRequest"%><%

SlingHttpServletRequest slingReq = (SlingHttpServletRequest)request;
WorkflowSession wfSession = slingReq.getResourceResolver().adaptTo(WorkflowSession.class);
/* Create the parent page */
String modelRepo = new String("/var/workflow/models");
String modelTemplate = new String ("/libs/cq/workflow/templates/model");
String modelName = new String("mymodel");
Page modelParent = pageManager.create(modelRepo, modelName, modelTemplate, "My workflow model");

/* create the model */
String modelId = new String(modelParent.getPath()+"/jcr:content/model")
WorkflowModel model = wfSession.createNewModel("Made using Java",modelId);

/* delete the model */
wfSession.deleteModel(modelId);
%>
```

#### Creación, lectura o eliminación de modelos de flujo de trabajo: script ECMA {#creating-reading-or-deleting-workflow-models-ecma-script}

```
var resolver = sling.getRequest().getResource().getResourceResolver();
var wfSession = resolver.adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
var pageManager = resolver.adaptTo(Packages.com.day.cq.wcm.api.PageManager);

//create the parent page node
var workflowPage = pageManager.create("/var/workflow/models", "mymodel", "/libs/cq/workflow/templates/model", "Created via ECMA Script");
var modelId = workflowPage.getPath()+ "/jcr:content/model";
//create the model
var model = wfSession.createNewModel("My Model", modelId);
//delete the model
var model = wfSession.deleteModel(modelId);
```

#### Eliminación de un modelo de flujo de trabajo: REST mediante curl {#deleting-a-workflow-model-rest-using-curl}

```shell
# deleting the model by its id
curl -u admin:admin -X DELETE http://localhost:4502/etc/workflow/models/{id}
```

>[!NOTE]
>
>Debido al nivel de detalle requerido, el curl no se considera práctico para crear y/o leer un modelo.

### Filtrado de flujos de trabajo del sistema al comprobar el estado del flujo de trabajo {#filtering-out-system-workflows-when-checking-workflow-status}

Puede usar el complemento [API WorkflowStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html) para recuperar información sobre el estado del flujo de trabajo de un nodo.

Varios métodos tienen el parámetro:

`excludeSystemWorkflows`

Este parámetro se puede establecer en `true` para indicar que los flujos de trabajo del sistema deben excluirse de los resultados relevantes.

Usted [Puede actualizar la configuración de OSGi](/help/sites-deploying/configuring-osgi.md) **Adobe Granite Workflow PayloadMapCache** que especifica el flujo de trabajo `Models` para que se consideren como flujos de trabajo del sistema. Los modelos predeterminados (de tiempo de ejecución) del flujo de trabajo son:

* `/var/workflow/models/scheduled_activation/jcr:content/model`
* `/var/workflow/models/scheduled_deactivation/jcr:content/model`

### Paso de participante de avance automático después de un tiempo de espera {#auto-advance-participant-step-after-a-timeout}

Si necesita avanzar automáticamente un **Participante** paso que no se ha completado en un tiempo predefinido puede:

1. Implemente un detector de eventos OSGI para escuchar la creación y modificación de tareas.
1. Especifique un tiempo de espera (fecha límite) y, a continuación, cree un trabajo de sling programado para activarse en ese momento.
1. Escriba un controlador de trabajo al que se notifique cuando caduque el tiempo de espera y déclencheur el trabajo.

   Este controlador realizará la acción necesaria en la tarea si esta aún no se ha completado

>[!NOTE]
>
>Las medidas que se adopten deben estar claramente definidas para poder utilizar este enfoque.

### Interactuar con instancias de flujo de trabajo {#interacting-with-workflow-instances}

A continuación se proporcionan ejemplos básicos de cómo interactuar (mediante programación) con instancias de flujo de trabajo.

#### Interactuar con instancias de flujo de trabajo: Java {#interacting-with-workflow-instances-java}

```java
// starting a workflow
WorkflowModel model = wfSession.getModel(workflowId);
WorkflowData wfData = wfSession.newWorkflowData("JCR_PATH", repoPath);
wfSession.startWorkflow(model, wfData);

// querying and managing a workflow
Workflow[] workflows workflows = wfSession.getAllWorkflows();
Workflow workflow= wfSession.getWorkflow(id);
wfSession.suspendWorkflow(workflow);
wfSession.resumeWorkflow(workflow);
wfSession.terminateWorkflow(workflow);
```

#### Interactuar con instancias de flujo de trabajo: script ECMA {#interacting-with-workflow-instances-ecma-script}

```
// starting a workflow
var model = wfSession.getModel(workflowId);
var wfData = wfSession.newWorkflowData("JCR_PATH", repoPath);
wfSession.startWorkflow(model, wfData);

// querying and managing a workflow
var workflows = wfSession.getWorkflows("RUNNING");
var workflow= wfSession.getWorkflow(id);
wfSession.suspendWorkflow(workflow);
wfSession.resumeWorkflow(workflow);
wfSession.terminateWorkflow(workflow);
```

#### Interactuar con instancias de flujo de trabajo: REST mediante curl {#interacting-with-workflow-instances-rest-using-curl}

* **Inicio de flujos de trabajo**

  ```shell
  # starting a workflow
  curl -d "model={id}&payloadType={type}&payload={payload}" http://localhost:4502/etc/workflow/instances
  
  # for example:
  curl -u admin:admin -d "model=/var/workflow/models/request_for_activation&payloadType=JCR_PATH&payload=/content/we-retail/us/en/products" http://localhost:4502/etc/workflow/instances
  ```

* **Listado de instancias**

  ```shell
  # listing the instances
  curl -u admin:admin http://localhost:4502/etc/workflow/instances.json
  ```

  Esto enumerará todas las instancias; por ejemplo:

  ```shell
  [
      {"uri":"/var/workflow/instances/server0/2018-02-26/prototype-01_1"}
      ,{"uri":"/var/workflow/instances/server0/2018-02-26/prototype-01_2"}
  ]
  ```

  >[!NOTE]
  >
  >Consulte [Cómo obtener una lista de todos los flujos de trabajo en ejecución](#how-to-get-a-list-of-all-running-workflows-with-their-ids) con sus ID para enumerar instancias con un estado específico.

* **Suspender un flujo de trabajo**

  ```shell
  # suspending a workflow
  curl -d "state=SUSPENDED" http://localhost:4502/etc/workflow/instances/{id}
  
  # for example:
  curl -u admin:admin -d "state=SUSPENDED" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
  ```

* **Reanudación de un flujo de trabajo**

  ```shell
  # resuming a workflow
  curl -d "state=RUNNING" http://localhost:4502/etc/workflow/instances/{id}
  
  # for example:
  curl -u admin:admin -d "state=RUNNING" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
  ```

* **Finalización de una instancia de flujo de trabajo**

  ```shell
  # terminating a workflow
  curl -d "state=ABORTED" http://localhost:4502/etc/workflow/instances/{id}
  
  # for example:
  curl -u admin:admin -d "state=ABORTED" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
  ```

### Interactuar con elementos de trabajo {#interacting-with-work-items}

A continuación se proporcionan ejemplos básicos de cómo interactuar (mediante programación) con elementos de trabajo.

#### Interactuar con elementos de trabajo: Java {#interacting-with-work-items-java}

```java
// querying work items
WorkItem[] workItems = wfSession.getActiveWorkItems();
WorkItem workItem = wfSession.getWorkItem(id);

// getting routes
List<Route> routes = wfSession.getRoutes(workItem);

// delegating
Iterator<Participant> delegatees = wfSession.getDelegatees(workItem);
wfSession.delegateWorkItem(workItem, delegatees.get(0));

// completing or advancing to the next step
wfSession.complete(workItem, routes.get(0));
```

#### Interactuar con elementos de trabajo: script ECMA {#interacting-with-work-items-ecma-script}

```
// querying work items
var workItems = wfSession.getActiveWorkItems();
var workItem = wfSession.getWorkItem(id);

// getting routes
var routes = wfSession.getRoutes(workItem);

// delegating
var delegatees = wfSession.getDelegatees(workItem);
wfSession.delegateWorkItem(workItem, delegatees.get(0));

// completing or advancing to the next step
wfSession.complete(workItem, routes.get(0));
```

#### Interactuar con elementos de trabajo: REST mediante curl {#interacting-with-work-items-rest-using-curl}

* **Lista de elementos de trabajo de la bandeja de entrada**

  ```shell
  # listing the work items
  curl -u admin:admin http://localhost:4502/bin/workflow/inbox
  ```

  Se enumerarán los detalles de los elementos de trabajo que se encuentran actualmente en la bandeja de entrada; por ejemplo:

  ```shell
  [{
      "uri_xss": "/var/workflow/instances/server0/2018-02-26/prototype-01_2/workItems/node2_var_workflow_instances_server0_2018-02-26_prototype-01_2",
      "uri": "/var/workflow/instances/server0/2018-02-26/prototype-01_2/workItems/node2_var_workflow_instances_server0_2018-02-26_prototype-01_2",
      "currentAssignee_xss": "workflow-administrators",
      "currentAssignee": "workflow-administrators",
      "startTime": 1519656289274,
      "payloadType_xss": "JCR_PATH",
      "payloadType": "JCR_PATH",
      "payload_xss": "/content/we-retail/es/es",
      "payload": "/content/we-retail/es/es",
      "comment_xss": "Process resource is null",
      "comment": "Process resource is null",
      "type_xss": "WorkItem",
      "type": "WorkItem"
    },{
      "uri_xss": "configuration/configure_analyticstargeting",
      "uri": "configuration/configure_analyticstargeting",
      "currentAssignee_xss": "administrators",
      "currentAssignee": "administrators",
      "type_xss": "Task",
      "type": "Task"
    },{
      "uri_xss": "configuration/securitychecklist",
      "uri": "configuration/securitychecklist",
      "currentAssignee_xss": "administrators",
      "currentAssignee": "administrators",
      "type_xss": "Task",
      "type": "Task"
    },{
      "uri_xss": "configuration/enable_collectionofanonymoususagedata",
      "uri": "configuration/enable_collectionofanonymoususagedata",
      "currentAssignee_xss": "administrators",
      "currentAssignee": "administrators",
      "type_xss": "Task",
      "type": "Task"
    },{
      "uri_xss": "configuration/configuressl",
      "uri": "configuration/configuressl",
      "currentAssignee_xss": "administrators",
      "currentAssignee": "administrators",
      "type_xss": "Task",
      "type": "Task"
    }
  ```

* **Delegación de elementos de trabajo**

  ```xml
  # delegating
  curl -d "item={item}&delegatee={delegatee}" http://localhost:4502/bin/workflow/inbox
  
  # for example:
  curl -u admin:admin -d "item=/etc/workflow/instances/server0/2017-03-08/request_for_activation_1/workItems/node1_etc_workflow_instances_server0_2017-03-08_request_for_act_1&delegatee=administrators" http://localhost:4502/bin/workflow/inbox
  ```

  >[!NOTE]
  >
  >El `delegatee` debe ser una opción válida para el paso del flujo de trabajo.

* **Completar o avanzar elementos de trabajo al paso siguiente**

  ```xml
  # retrieve the list of routes; the results will be similar to {"results":1,"routes":[{"rid":"233123169","label":"End","label_xss":"End"}]}
  http://localhost:4502/etc/workflow/instances/<path-to-the-workitem>.routes.json
  
  # completing or advancing to the next step; use the appropriate route ID (rid value) from the above list
  curl -d "item={item}&route={route}" http://localhost:4502/bin/workflow/inbox
  
  # for example:
  curl -u admin:admin -d "item=/etc/workflow/instances/server0/2017-03-08/request_for_activation_1/workItems/node1_etc_workflow_instances_server0_2017-03-08_request_for_activation_1&route=233123169" http://localhost:4502/bin/workflow/inbox
  ```

### Escucha de eventos de flujo de trabajo {#listening-for-workflow-events}

Utilice el marco de eventos OSGi para detectar eventos que [`com.adobe.granite.workflow.event.WorkflowEvent`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/event/WorkflowEvent.html) define la clase. Esta clase también proporciona varios métodos útiles para obtener información sobre el asunto del evento. Por ejemplo, la variable `getWorkItem` El método devuelve el `WorkItem` objeto para el elemento de trabajo implicado en el evento.

El siguiente código de ejemplo define un servicio que escucha eventos de flujo de trabajo y realiza tareas según el tipo de evento.

```java
package com.adobe.example.workflow.listeners;

import org.apache.sling.event.jobs.JobProcessor;
import org.apache.sling.event.jobs.JobUtil;

import org.osgi.service.event.Event;
import org.osgi.service.event.EventHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;

import com.adobe.granite.workflow.event.WorkflowEvent;
import com.adobe.granite.workflow.exec.WorkItem;

/**
 * The <code>WorkflowEventCatcher</code> class listens to workflow events.
 */
@Component(metatype=false, immediate=true)
@Service(value=org.osgi.service.event.EventHandler.class)
public class WorkflowEventCatcher implements EventHandler, JobProcessor {

 @Property(value=com.adobe.granite.workflow.event.WorkflowEvent.EVENT_TOPIC)
 static final String EVENT_TOPICS = "event.topics";

 private static final Logger logger = LoggerFactory.getLogger(WorkflowEventCatcher.class);

 public void handleEvent(Event event) {
  JobUtil.processJob(event, this);
 }

 public boolean process(Event event) {
  logger.info("Received event of topic: " + event.getTopic());
  String topic = event.getTopic();

  try {
   if (topic.equals(WorkflowEvent.EVENT_TOPIC)) {
    WorkflowEvent wfevent = (WorkflowEvent)event;
    String eventType = wfevent.getEventType();
    String instanceId = wfevent.getWorkflowInstanceId();

    if (instanceId != null) {
     //workflow instance events
     if (eventType.equals(WorkflowEvent.WORKFLOW_STARTED_EVENT) ||
       eventType.equals(WorkflowEvent.WORKFLOW_RESUMED_EVENT) ||
       eventType.equals(WorkflowEvent.WORKFLOW_SUSPENDED_EVENT)) {
      // your code comes here...
     } else if (
       eventType.equals(WorkflowEvent.WORKFLOW_ABORTED_EVENT) ||
       eventType.equals(WorkflowEvent.WORKFLOW_COMPLETED_EVENT)) {
      // your code comes here...
     }
     // workflow node event
     if (eventType.equals(WorkflowEvent.NODE_TRANSITION_EVENT)) {
      WorkItem currentItem = (WorkItem) event.getProperty(WorkflowEvent.WORK_ITEM);
      // your code comes here...
     }
    }
   }
  } catch(Exception e){
   logger.debug(e.getMessage());
   e.printStackTrace();
  }
  return true;
 }
}
```
