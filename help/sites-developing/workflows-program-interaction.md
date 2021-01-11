---
title: Interactuar con Flujos de trabajo mediante programación
seo-title: Interactuar con Flujos de trabajo mediante programación
description: nulo
seo-description: nulo
uuid: a0f19fc6-b9bd-4b98-9c0e-fbf4f7383026
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: cb621332-a149-4f8d-9425-fd815b033c38
translation-type: tm+mt
source-git-commit: edf7ef93372e44cb71d8eac8712db53f4e45b6cf
workflow-type: tm+mt
source-wordcount: '2006'
ht-degree: 0%

---


# Interactuar con Flujos de trabajo mediante programación{#interacting-with-workflows-programmatically}

Al [personalizar y ampliar sus flujos de trabajo](/help/sites-developing/workflows-customizing-extending.md) puede acceder a los objetos del flujo de trabajo:

* [Uso de la API de Java de workflow](#using-the-workflow-java-api)
* [Obtención de objetos de flujo de trabajo en secuencias de comandos de ECMA](#obtaining-workflow-objects-in-ecma-scripts)
* [Uso de la API de flujo de trabajo REST](#using-the-workflow-rest-api)

## Uso de la API de Java de flujo de trabajo {#using-the-workflow-java-api}

La API de Java de flujo de trabajo consiste en el paquete [`com.adobe.granite.workflow`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/package-summary.html) y varios subpaquetes. El miembro más significativo de la API es la clase `com.adobe.granite.workflow.WorkflowSession`. La clase `WorkflowSession` proporciona acceso a objetos de flujo de trabajo de tiempo de diseño y tiempo de ejecución:

* modelos de flujo de trabajo
* elementos de trabajo
* instancias de flujo de trabajo
* datos de flujo de trabajo
* elementos de bandeja de entrada

La clase también proporciona varios métodos para intervenir en los ciclos de vida del flujo de trabajo.

La siguiente tabla proporciona vínculos a la documentación de referencia de varios objetos Java clave que se utilizarán al interactuar programáticamente con flujos de trabajo. Los siguientes ejemplos muestran cómo obtener y utilizar los objetos de clase en el código.

| Características | Objetos |
|---|---|
| Acceso a un flujo de trabajo | [`WorkflowSession`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html) |
| Ejecución y consulta de una instancia de flujo de trabajo | [`Workflow`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html)</br>[`WorkItem`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkItem.html)</br>[`WorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html) |
| Administración de un modelo de flujo de trabajo | [`WorkflowModel`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowModel.html)</br>[`WorkflowNode`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowNode.html)</br>[`WorkflowTransition`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowTransition.html) |
| Información de un nodo que está en el flujo de trabajo (o no) | [`WorkflowStatus`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html) |

## Obtención de objetos de flujo de trabajo en secuencias de comandos de ECMA {#obtaining-workflow-objects-in-ecma-scripts}

Como se describe en [Localización de la secuencia de comandos](/help/sites-developing/the-basics.md#locating-the-script), AEM (a través de Apache Sling) proporciona un motor de secuencias de comandos ECMA que ejecuta secuencias de comandos ECMA del lado del servidor. La clase [`org.apache.sling.scripting.core.ScriptHelper`](https://sling.apache.org/apidocs/sling5/org/apache/sling/scripting/core/ScriptHelper.html) está inmediatamente disponible para sus secuencias de comandos como la variable `sling`.

La clase `ScriptHelper` proporciona acceso a `SlingHttpServletRequest` que puede utilizar para obtener finalmente el objeto `WorkflowSession`; por ejemplo:

```
var wfsession = sling.getRequest().getResource().getResourceResolver().adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
```

## Uso de la API de flujo de trabajo REST {#using-the-workflow-rest-api}

La consola Flujo de trabajo utiliza en gran medida la API de REST; esta página describe la API de REST para flujos de trabajo.

>[!NOTE]
>
>La herramienta de línea de comandos curl le permite utilizar la API de flujo de trabajo REST para acceder a los objetos de flujo de trabajo y administrar los ciclos de vida de las instancias. Los ejemplos de esta página muestran el uso de la API de REST a través de la herramienta de línea de comandos curl.

Las siguientes acciones son compatibles con la API de REST:

* inicio o parada de un servicio de flujo de trabajo
* crear, actualizar o eliminar modelos de flujo de trabajo
* [inicio, suspensión, reanudación o finalización de instancias de flujo de trabajo](/help/sites-administering/workflows.md#workflow-status-and-actions)
* completar o delegar elementos de trabajo

>[!NOTE]
>
>Al utilizar Firebug, una extensión de Firefox para el desarrollo web, es posible seguir el tráfico HTTP cuando la consola está en funcionamiento. Por ejemplo, puede comprobar los parámetros y los valores enviados al servidor de AEM con una solicitud `POST`.

En esta página se supone que AEM se ejecuta en localhost en el puerto `4502` y que el contexto de instalación es &quot; `/`&quot; (raíz). Si no es el caso de su instalación, los URI, a los que se aplican las solicitudes HTTP, deben adaptarse en consecuencia.

El procesamiento admitido para solicitudes `GET` es el procesamiento JSON. Las direcciones URL para `GET` deben tener la extensión `.json`, por ejemplo:

`http://localhost:4502/etc/workflow.json`

### Administración de instancias de flujo de trabajo {#managing-workflow-instances}

Los siguientes métodos de solicitud HTTP se aplican a:

`http://localhost:4502/etc/workflow/instances`

<table>
 <tbody>
  <tr>
   <td>Método de solicitud HTTP</td>
   <td>Acciones</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>Lista las instancias de flujo de trabajo disponibles.</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td><p>Crea una nueva instancia de flujo de trabajo. Los parámetros son:<br /> - <code>model</code>: el ID (URI) del modelo de flujo de trabajo correspondiente<br /> - <code>payloadType</code>: que contiene el tipo de carga útil (por ejemplo, <code>JCR_PATH</code> o URL).<br /> La carga útil se envía como parámetro  <code>payload</code>. Se devuelve una respuesta <code>201</code> (<code>CREATED</code>) con un encabezado de ubicación que contiene la dirección URL del nuevo recurso de instancia de flujo de trabajo.</p> </td>
  </tr>
 </tbody>
</table>

#### Administración de una instancia de flujo de trabajo por su estado {#managing-a-workflow-instance-by-its-state}

Los siguientes métodos de solicitud HTTP se aplican a:

`http://localhost:4502/etc/workflow/instances.{state}`

| Método de solicitud HTTP | Acciones |
|---|---|
| `GET` | Lista las instancias de flujo de trabajo disponibles y sus estados ( `RUNNING`, `SUSPENDED`, `ABORTED` o `COMPLETED`) |

#### Administración de una instancia de flujo de trabajo por su ID {#managing-a-workflow-instance-by-its-id}

Los siguientes métodos de solicitud HTTP se aplican a:

`http://localhost:4502/etc/workflow/instances/{id}`

<table>
 <tbody>
  <tr>
   <td>Método de solicitud HTTP</td>
   <td>Acciones</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>Obtiene los datos de instancias (definición y metadatos), incluido el vínculo al modelo de flujo de trabajo correspondiente.</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>Cambia el estado de la instancia. El nuevo estado se envía como parámetro <code>state</code> y debe tener uno de los siguientes valores: <code>RUNNING</code>, <code>SUSPENDED</code> o <code>ABORTED</code>.<br /> Si el nuevo estado no está disponible (por ejemplo, al suspender una instancia terminada), se devuelve una respuesta  <code>409</code> (<code>CONFLICT</code>) al cliente.</td>
  </tr>
 </tbody>
</table>

### Administración de modelos de flujo de trabajo {#managing-workflow-models}

Los siguientes métodos de solicitud HTTP se aplican a:

`http://localhost:4502/etc/workflow/models`

<table>
 <tbody>
  <tr>
   <td>Método de solicitud HTTP</td>
   <td>Acciones</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>Lista los modelos de flujo de trabajo disponibles.</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>Crea un nuevo modelo de flujo de trabajo. Si se envía el parámetro <code>title</code>, se crea un nuevo modelo con el título especificado. Al adjuntar una definición de modelo JSON como parámetro <code>model</code>, se crea un nuevo modelo de flujo de trabajo según la definición proporcionada.<br /> Se devuelve una  <code>201</code> respuesta (<code>CREATED</code>) con un encabezado de ubicación que contiene la dirección URL del nuevo recurso del modelo de flujo de trabajo.<br /> Lo mismo ocurre cuando se adjunta una definición de modelo como un parámetro de archivo denominado  <code>modelfile</code>.<br /> Tanto en el caso de los  <code>model</code> parámetros  <code>modelfile</code> como en el de los parámetros,  <code>type</code> se requiere un parámetro adicional denominado para definir el formato de serialización. Los nuevos formatos de serialización se pueden integrar mediante la API OSGI. Se entrega un serializador JSON estándar con el motor de flujos de trabajo. Su tipo es JSON. Consulte a continuación un ejemplo del formato.</td>
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

Donde `*{uri}*` es la ruta al nodo de modelo en el repositorio.

<table>
 <tbody>
  <tr>
   <td>Método de solicitud HTTP</td>
   <td>Acciones</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>Obtiene la versión <code>HEAD</code> del modelo (definición y metadatos).</td>
  </tr>
  <tr>
   <td><code>PUT</code></td>
   <td>Actualiza la versión <code>HEAD</code> del modelo (crea una nueva versión).<br /> La definición completa del modelo para la nueva versión del modelo debe agregarse como un parámetro llamado  <code>model</code>. Además, se necesita un parámetro <code>type</code> como al crear nuevos modelos y debe tener el valor <code>JSON</code>.<br /> </td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>El mismo comportamiento que con el PUT. Necesario porque AEM utilidades no admiten operaciones <code>PUT</code>.</td>
  </tr>
  <tr>
   <td><code>DELETE</code></td>
   <td>Elimina el modelo. Para resolver los problemas de firewall/proxy, también se aceptará como solicitud <code>DELETE</code> una <code>POST</code> que contenga una entrada de encabezado <code>X-HTTP-Method-Override</code> con el valor <code>DELETE</code>.</td>
  </tr>
 </tbody>
</table>

Ejemplo: en el explorador, una solicitud para `http://localhost:4502/var/workflow/models/publish_example.json` devuelve una respuesta `json` similar al siguiente código:

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

#### Administración de un modelo de flujo de trabajo por su versión {#managing-a-workflow-model-by-its-version}

Los siguientes métodos de solicitud HTTP se aplican a:

`http://localhost:4502/etc/workflow/models/{id}.{version}`

| Método de solicitud HTTP | Acciones |
|---|---|
| `GET` | Obtiene los datos del modelo en la versión dada (si existe). |

### Administración de bandejas de entrada (de usuario) {#managing-user-inboxes}

Los siguientes métodos de solicitud HTTP se aplican a:

`http://localhost:4502/bin/workflow/inbox`

<table>
 <tbody>
  <tr>
   <td>Método de solicitud HTTP</td>
   <td>Acciones</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>Lista los elementos de trabajo que se encuentran en la bandeja de entrada del usuario, que se identifica mediante los encabezados de autenticación HTTP.</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>Completa el elemento de trabajo cuyo URI se envía como parámetro <code>item</code> y avanza la instancia de flujo de trabajo de acuerdo a los nodos siguientes, que se define mediante el parámetro <code>route</code> o <code>backroute</code> en caso de retroceder un paso.<br /> Si  <code>delegatee</code> se envía el parámetro, el elemento de trabajo identificado por el parámetro  <code>item</code> se delega al participante especificado.</td>
  </tr>
 </tbody>
</table>

#### Administración de una bandeja de entrada (de usuario) mediante el ID de elemento de trabajo {#managing-a-user-inbox-by-the-workitem-id}

Los siguientes métodos de solicitud HTTP se aplican a:

`http://localhost:4502/bin/workflow/inbox/{id}`

| Método de solicitud HTTP | Acciones |
|---|---|
| `GET` | Obtiene los datos (definición y metadatos) de la bandeja de entrada `WorkItem` identificada por su ID. |

## Ejemplos {#examples}

### Cómo obtener una Lista de todos los Flujos de trabajo en ejecución con sus ID {#how-to-get-a-list-of-all-running-workflows-with-their-ids}

Para obtener una lista de todos los flujos de trabajo en ejecución, haga una GET para:

`http://localhost:4502/etc/workflow/instances.RUNNING.json`

#### Cómo obtener una Lista de todos los Flujos de trabajo en ejecución con sus ID: REST mediante curl {#how-to-get-a-list-of-all-running-workflows-with-their-ids-rest-using-curl}

Ejemplo con curl:

```shell
curl -u admin:admin http://localhost:4502/etc/workflow/instances.RUNNING.json
```

El `uri` mostrado en los resultados puede utilizarse como instancia `id` en otros comandos; por ejemplo:

```shell
[
    {"uri":"/etc/workflow/instances/server0/2017-03-08/request_for_activation_1"}
]
```

>[!NOTE]
>
>Este comando `curl` puede utilizarse con cualquier estado de [flujo de trabajo](/help/sites-administering/workflows.md#workflow-status-and-actions) en lugar de `RUNNING`.

### Cómo cambiar el título del flujo de trabajo {#how-to-change-the-workflow-title}

Para cambiar el **Título del flujo de trabajo** que se muestra en la ficha **Instancias** de la consola del flujo de trabajo, envíe un comando `POST`:

* hasta: `http://localhost:4502/etc/workflow/instances/{id}`

* con los parámetros siguientes:

   * `action`:: su valor debe ser:  `UPDATE`
   * `workflowTitle`:: el título del flujo de trabajo

#### Cómo cambiar el título del flujo de trabajo - REST usando curl {#how-to-change-the-workflow-title-rest-using-curl}

Ejemplo con curl:

```shell
curl -u admin:admin -d "action=UPDATE&workflowTitle=myWorkflowTitle" http://localhost:4502/etc/workflow/instances/{id}

# for example
curl -u admin:admin -d "action=UPDATE&workflowTitle=myWorkflowTitle" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
```

### Cómo realizar la Lista de todos los modelos de flujo de trabajo {#how-to-list-all-workflow-models}

Para obtener una lista de todos los modelos de flujo de trabajo disponibles, realice un GET para:

`http://localhost:4502/etc/workflow/models.json`

#### Lista de todos los modelos de flujo de trabajo: REST mediante curl {#how-to-list-all-workflow-models-rest-using-curl}

Ejemplo con curl:

```shell
curl -u admin:admin http://localhost:4502/etc/workflow/models.json
```

>[!NOTE]
>
>Consulte también [Administración de modelos de flujo de trabajo](#managing-workflow-models).

### Obtención de un objeto WorkflowSession {#obtaining-a-workflowsession-object}

La clase `com.adobe.granite.workflow.WorkflowSession` se puede adaptar desde un objeto `javax.jcr.Session` o un objeto `org.apache.sling.api.resource.ResourceResolver`.

#### Obtención de un objeto WorkflowSession: Java {#obtaining-a-workflowsession-object-java}

En una secuencia de comandos JSP (o código Java para una clase servlet), utilice el objeto de solicitud HTTP para obtener un objeto `SlingHttpServletRequest`, que proporciona acceso a un objeto `ResourceResolver`. Adapte el objeto `ResourceResolver` a `WorkflowSession`.

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

#### Obtención de un objeto WorkflowSession: secuencia de comandos de ECMA {#obtaining-a-workflowsession-object-ecma-script}

Utilice la variable `sling` para obtener el objeto `SlingHttpServletRequest` que utiliza para obtener un objeto `ResourceResolver`. Adapte el objeto `ResourceResolver` al objeto `WorkflowSession`.

```
var wfsession = sling.getRequest().getResource().getResourceResolver().adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
```

### Creación, lectura o eliminación de modelos de flujo de trabajo {#creating-reading-or-deleting-workflow-models}

Los siguientes ejemplos muestran cómo acceder a los modelos de flujo de trabajo:

* El código para Java y la secuencia de comandos ECMA utiliza el método `WorkflowSession.createNewModel`.
* El comando curl accede al modelo directamente mediante su URL.

Los ejemplos utilizados:

1. Cree un modelo (con la ID `/var/workflow/models/mymodel/jcr:content/model`).
1. Elimine el modelo.

>[!NOTE]
>
>Al eliminar el modelo, se establece la propiedad `deleted` del nodo secundario `metaData` del modelo en `true`.
>
>La eliminación no elimina el nodo de modelo.

Al crear un modelo nuevo:

* El editor de modelos de flujo de trabajo requiere que los modelos utilicen una estructura de nodos específica por debajo de `/var/workflow/models`. El nodo principal del modelo debe ser del tipo `cq:Page` que tenga un nodo `jcr:content` con los siguientes valores de propiedad:

   * `sling:resourceType`: `cq/workflow/components/pages/model`
   * `cq:template`::  `/libs/cq/workflow/templates/model`

   Al crear un modelo, primero debe crear este nodo `cq:Page` y utilizar su nodo `jcr:content` como principal del nodo del modelo.

* El argumento `id` que algunos métodos requieren para identificar el modelo es la ruta absoluta del nodo de modelo en el repositorio:

   `/var/workflow/models/<*model_name>*/jcr:content/model`

   >[!NOTE]
   >
   >Consulte [Lista de todos los modelos de flujo de trabajo](#how-to-list-all-workflow-models).

#### Creación, lectura o eliminación de modelos de flujo de trabajo - Java {#creating-reading-or-deleting-workflow-models-java}

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

#### Creación, lectura o eliminación de modelos de flujo de trabajo: secuencia de comandos de ECMA {#creating-reading-or-deleting-workflow-models-ecma-script}

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

#### Eliminación de un modelo de flujo de trabajo: REST con curl {#deleting-a-workflow-model-rest-using-curl}

```shell
# deleting the model by its id
curl -u admin:admin -X DELETE http://localhost:4502/etc/workflow/models/{id}
```

>[!NOTE]
>
>Debido al nivel de detalle requerido, el curl no se considera práctico para crear y/o leer un modelo.

### Filtrar Flujos de trabajo del sistema al comprobar el estado del flujo de trabajo {#filtering-out-system-workflows-when-checking-workflow-status}

Puede utilizar la [API WorkflowStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html) para recuperar información sobre el estado del flujo de trabajo de un nodo.

Varios métodos tienen el parámetro:

`excludeSystemWorkflows`

Este parámetro se puede establecer en `true` para indicar que los flujos de trabajo del sistema deben excluirse de los resultados relevantes.

[puede actualizar la configuración de OSGi](/help/sites-deploying/configuring-osgi.md) **Adobe Granite Workflow PayloadMapCache** que especifica el flujo de trabajo `Models` que debe considerarse como flujos de trabajo del sistema. Los modelos de flujo de trabajo predeterminados (tiempo de ejecución) son:

* `/var/workflow/models/scheduled_activation/jcr:content/model`
* `/var/workflow/models/scheduled_deactivation/jcr:content/model`

### Avance automático del participante Paso después de un tiempo de espera {#auto-advance-participant-step-after-a-timeout}

Si necesita avanzar automáticamente un paso **Participante** que no se haya completado dentro de un tiempo predefinido, puede:

1. Implemente un detector de eventos OSGI para escuchar la creación y modificación de tareas.
1. Especifique un tiempo de espera (fecha límite) y, a continuación, cree un trabajo de sling programado para que se active en ese momento.
1. Escriba un controlador de trabajo que reciba una notificación cuando caduque el tiempo de espera y active el trabajo.

   Este controlador realizará la acción necesaria en la tarea si la tarea aún no se ha completado

>[!NOTE]
>
>Las medidas que deben adoptarse deben definirse claramente para poder utilizar este enfoque.

### Interactuar con instancias de flujo de trabajo {#interacting-with-workflow-instances}

A continuación se proporcionan ejemplos básicos de cómo interactuar (de forma programada) con instancias de flujo de trabajo.

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

#### Interactuar con instancias de flujo de trabajo: secuencia de comandos de ECMA {#interacting-with-workflow-instances-ecma-script}

```
// starting a workflow
var model = wfSession.getModel(workflowId);
var wfData = wfSession.newWorkflowData("JCR_PATH", repoPath);
wfSession.startWorkflow(model, wfData);

// querying and managing a workflow
var workflows = wfSession.getWorkflows(“RUNNING“);
var workflow= wfSession.getWorkflow(id);
wfSession.suspendWorkflow(workflow);
wfSession.resumeWorkflow(workflow);
wfSession.terminateWorkflow(workflow);
```

#### Interactuar con instancias de flujo de trabajo: REST mediante curl {#interacting-with-workflow-instances-rest-using-curl}

* **Inicio de un flujo de trabajo**

   ```shell
   # starting a workflow
   curl -d "model={id}&payloadType={type}&payload={payload}" http://localhost:4502/etc/workflow/instances
   
   # for example:
   curl -u admin:admin -d "model=/var/workflow/models/request_for_activation&payloadType=JCR_PATH&payload=/content/we-retail/us/en/products" http://localhost:4502/etc/workflow/instances
   ```

* **Lista de instancias**

   ```shell
   # listing the instances
   curl -u admin:admin http://localhost:4502/etc/workflow/instances.json
   ```

   Esto lista todas las instancias; por ejemplo:

   ```shell
   [
       {"uri":"/var/workflow/instances/server0/2018-02-26/prototype-01_1"}
       ,{"uri":"/var/workflow/instances/server0/2018-02-26/prototype-01_2"}
   ]
   ```

   >[!NOTE]
   >
   >Consulte [Cómo obtener una Lista de todos los Flujos de trabajo en ejecución](#how-to-get-a-list-of-all-running-workflows-with-their-ids) con sus ID para enumerar las instancias con un estado específico.

* **Suspensión de un flujo de trabajo**

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

A continuación se proporcionan ejemplos básicos de cómo interactuar (de forma programada) con elementos de trabajo.

#### Interactuar con elementos de trabajo - Java {#interacting-with-work-items-java}

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

#### Interactuar con elementos de trabajo - Secuencia de comandos ECMA {#interacting-with-work-items-ecma-script}

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

#### Interactuar con elementos de trabajo: REST con curl {#interacting-with-work-items-rest-using-curl}

* **Lista de elementos de trabajo de la bandeja de entrada**

   ```shell
   # listing the work items
   curl -u admin:admin http://localhost:4502/bin/workflow/inbox
   ```

   Se enumerarán los detalles de los elementos de trabajo que se encuentran actualmente en la Bandeja de entrada; por ejemplo:

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

* **Cómo completar o avanzar elementos de trabajo al paso siguiente**

   ```xml
   # retrieve the list of routes; the results will be similar to {"results":1,"routes":[{"rid":"233123169","label":"End","label_xss":"End"}]}
   http://localhost:4502/etc/workflow/instances/<path-to-the-workitem>.routes.json
   
   # completing or advancing to the next step; use the appropriate route ID (rid value) from the above list
   curl -d "item={item}&route={route}" http://localhost:4502/bin/workflow/inbox
   
   # for example:
   curl -u admin:admin -d "item=/etc/workflow/instances/server0/2017-03-08/request_for_activation_1/workItems/node1_etc_workflow_instances_server0_2017-03-08_request_for_activation_1&route=233123169" http://localhost:4502/bin/workflow/inbox
   ```

### Escuchar Eventos de flujo de trabajo {#listening-for-workflow-events}

Utilice la estructura de evento OSGi para detectar eventos que define la clase [ `com.adobe.granite.workflow.event.WorkflowEvent`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/event/WorkflowEvent.html). Esta clase también proporciona varios métodos útiles para obtener información sobre el tema del evento. Por ejemplo, el método `getWorkItem` devuelve el objeto `WorkItem` del elemento de trabajo que está involucrado en el evento.

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

