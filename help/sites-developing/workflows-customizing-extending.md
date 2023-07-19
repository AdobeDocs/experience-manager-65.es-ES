---
title: Ampliación de la funcionalidad del flujo de trabajo
seo-title: Extending Workflow Functionality
description: Ampliación de la funcionalidad del flujo de trabajo
seo-description: null
uuid: 9f4ea2a8-8b21-4e7c-ac73-dd37d9ada111
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: f23408c3-6b37-4047-9cce-0cab97bb6c5c
exl-id: 9e205912-50a6-414a-b8d4-a0865269d0e0
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '3584'
ht-degree: 2%

---

# Ampliación de la funcionalidad del flujo de trabajo{#extending-workflow-functionality}

En este tema se describe cómo desarrollar componentes de paso personalizados para los flujos de trabajo y, a continuación, cómo interactuar mediante programación con los flujos de trabajo.

La creación de un paso de flujo de trabajo personalizado implica las siguientes actividades:

* Desarrollar el componente de paso de flujo de trabajo.
* Implemente la funcionalidad de paso como servicio OSGi o script ECMA.

También puede [interactuar con los flujos de trabajo desde los programas y scripts](/help/sites-developing/workflows-program-interaction.md).

## Componentes de pasos del flujo de trabajo: conceptos básicos {#workflow-step-components-the-basics}

Un componente de paso de flujo de trabajo define el aspecto y el comportamiento del paso al crear modelos de flujo de trabajo:

* La categoría y el nombre del paso en la barra de tareas del flujo de trabajo.
* El aspecto del paso en los modelos de flujo de trabajo.
* Cuadro de diálogo de edición para configurar las propiedades del componente.
* El servicio o script que se ejecuta durante la ejecución.

Al igual que con [todos los componentes](/help/sites-developing/components.md), los componentes de paso del flujo de trabajo heredan del componente especificado para `sling:resourceSuperType` propiedad. El diagrama siguiente muestra la jerarquía de `cq:component` nodos que forman la base de todos los componentes de paso del flujo de trabajo. El diagrama también incluye el **Etapa del proceso**, **Etapa de participante**, y **Etapa de participante dinámica** componentes, ya que estos son los puntos de partida más comunes (y básicos) para desarrollar componentes de paso personalizados.

![aem_wf_componentinherit](assets/aem_wf_componentinherit.png)

>[!CAUTION]
>
>Usted ***debe*** no cambie nada en el `/libs` ruta.
>
>Esto se debe al contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y es posible que se sobrescriba al aplicar una revisión o un paquete de funciones).
>
>El método recomendado para la configuración y otros cambios es:
>
>1. Vuelva a crear el elemento necesario (es decir, tal como existe en `/libs` bajo `/apps`
>2. Realice cualquier cambio en `/apps`

El `/libs/cq/workflow/components/model/step` El componente es el antecesor común más cercano del **Etapa del proceso**, **Etapa de participante**, y **Etapa de participante dinámica**, que heredan los siguientes elementos:

* `step.jsp`

  El `step.jsp` La secuencia de comandos procesa el título del componente de paso cuando se añade a un modelo.

  ![wf-22-1](assets/wf-22-1.png)

* [cq:dialog](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog)

  Un cuadro de diálogo con las siguientes pestañas:

   * **Común**: para editar el título y la descripción.
   * **Avanzadas**: para editar propiedades de notificación por correo electrónico.

  ![wf-44](assets/wf-44.png) ![wf-45](assets/wf-45.png)

  >[!NOTE]
  >
  >Cuando las pestañas del cuadro de diálogo de edición de un componente de paso no coinciden con esta apariencia predeterminada, el componente de paso tiene scripts definidos, propiedades de nodo o pestañas de diálogo que anulan estas pestañas heredadas.

### Scripts ECMA {#ecma-scripts}

Los siguientes objetos están disponibles (según el tipo de paso) en los scripts ECMA:

* [WorkItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkItem.html) workItem
* [WorkflowSession](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/WorkflowSession.html) workflowSession
* [WorkflowData](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkflowData.html) workflowData
* `args`: matriz con los argumentos de proceso.

* `sling`: para acceder a otros servicios de osgi.
* `jcrSession`

### MetaDataMaps {#metadatamaps}

Puede utilizar los metadatos del flujo de trabajo para conservar la información necesaria durante la duración del flujo de trabajo. Un requisito común de los pasos del flujo de trabajo es conservar los datos para su uso futuro en el flujo de trabajo o recuperar los datos persistentes.

Existen tres tipos de objetos MetaDataMap: para `Workflow`, `WorkflowData` y `WorkItem` objetos. Todas tienen el mismo propósito: almacenar metadatos.

Un elemento de trabajo tiene su propio MetaDataMap que sólo se puede utilizar mientras se está ejecutando ese elemento de trabajo (por ejemplo, step).

Ambos `Workflow` y `WorkflowData` los mapas de metadatos se comparten en todo el flujo de trabajo. Para estos casos, se recomienda utilizar únicamente la variable `WorkflowData` asignación de metadatos.

## Creación de componentes de paso de flujo de trabajo personalizados {#creating-custom-workflow-step-components}

Los componentes de paso de flujo de trabajo pueden ser [creado de la misma manera que cualquier otro componente](/help/sites-developing/components.md).

Para heredar de uno de los componentes de paso base (existentes), agregue la siguiente propiedad al `cq:Component` nodo:

* Nombre: `sling:resourceSuperType`
* Tipo: `String`
* Valor: una de las siguientes rutas que se resuelve en un componente base:

   * `cq/workflow/components/model/process`
   * `cq/workflow/components/model/participant`
   * `cq/workflow/components/model/dynamic_participant`

### Especificación del título y la descripción predeterminados para las instancias de paso {#specifying-the-default-title-and-description-for-step-instances}

Utilice el siguiente procedimiento para especificar los valores predeterminados de **Título** y **Descripción** campos en la **Común** pestaña.

>[!NOTE]
>
>Los valores de campo aparecen en la instancia de paso cuando se cumplen los dos requisitos siguientes:
>
>* El cuadro de diálogo de edición del paso almacena el título y la descripción en las siguientes ubicaciones: >
>* `./jcr:title`
>* `./jcr:description` ubicaciones
>
>  Este requisito se cumple cuando el cuadro de diálogo de edición utiliza la pestaña Común que muestra el `/libs/cq/flow/components/step/step` el componente implementa.
>
>* El componente de paso o un antecesor del componente no anula la variable `step.jsp` script que la variable `/libs/cq/flow/components/step/step` el componente implementa.

1. Debajo de `cq:Component` , agregue el siguiente nodo:

   * Nombre: `cq:editConfig`
   * Tipo: `cq:EditConfig`

   >[!NOTE]
   >
   >Para obtener más información sobre el nodo cq:editConfig, consulte [Configuración del comportamiento de edición de un componente](/help/sites-developing/developing-components.md#configuring-the-edit-behavior).

1. Debajo de `cq:EditConfig` , agregue el siguiente nodo:

   * Nombre: `cq:formParameters`
   * Tipo: `nt:unstructured`

1. Añadir `String` propiedades de los siguientes nombres para la variable `cq:formParameters` nodo:

   * `jcr:title`: El valor rellena el **Título** del campo **Común** pestaña.
   * `jcr:description`: El valor rellena el **Descripción** del campo **Común** pestaña.

### Guardar valores de propiedad en metadatos de flujo de trabajo {#saving-property-values-in-workflow-metadata}

>[!NOTE]
>
>Consulte [Conservación y acceso a datos](#persisting-and-accessing-data). En particular, para obtener información sobre el acceso al valor de la propiedad durante la ejecución, consulte [Acceder a valores de propiedad de diálogo en tiempo de ejecución](#accessing-dialog-property-values-at-runtime).

La propiedad name de `cq:Widget` items especifica el nodo JCR que almacena el valor del widget. Cuando los widgets del cuadro de diálogo de los componentes del paso del flujo de trabajo almacenan valores debajo de `./metaData` , el valor se añade al flujo de trabajo `MetaDataMap`.

Por ejemplo, un campo de texto en un cuadro de diálogo es un `cq:Widget` nodo que tiene las siguientes propiedades:

| Nombre | Tipo | Valor  |
|---|---|---|
| `xtype` | `String` | `textarea` |
| `name` | `String` | `./metaData/subject` |
| `fieldLabel` | `String` | `Email Subject` |

El valor especificado en este campo de texto se agrega al de la instancia de flujo de trabajo ` [MetaDataMap](#metadatamaps)` y está asociado con el objeto `subject` clave.

>[!NOTE]
>
>Cuando la clave es `PROCESS_ARGS`, el valor está fácilmente disponible en implementaciones de scripts ECMA a través de la variable `args` variable. En este caso, el valor de la propiedad name es `./metaData/PROCESS_ARGS.`

### Anulación de la implementación por pasos {#overriding-the-step-implementation}

Cada componente de paso base permite a los desarrolladores de modelos de flujo de trabajo configurar las siguientes funciones clave en tiempo de diseño:

* Paso del proceso: El servicio o el script ECMA que se ejecutará durante la ejecución.
* Etapa de participante: la ID del usuario al que se asigna el elemento de trabajo generado.
* Paso de participante dinámico: servicio o script ECMA que selecciona el ID del usuario al que se asigna el elemento de trabajo.

Para enfocar el componente para utilizarlo en un escenario de flujo de trabajo específico, configure la función clave en el diseño y elimine la capacidad para que los desarrolladores de modelos lo cambien.

1. Bajo el nodo cq:component, agregue el siguiente nodo:

   * Nombre: `cq:editConfig`
   * Tipo: `cq:EditConfig`

   Para obtener más información sobre el nodo cq:editConfig, consulte [Configuración del comportamiento de edición de un componente](/help/sites-developing/developing-components.md#configuring-the-edit-behavior).

1. Bajo el nodo cq:EditConfig, agregue el siguiente nodo:

   * Nombre: `cq:formParameters`
   * Tipo: `nt:unstructured`

1. Añadir un `String` a la propiedad `cq:formParameters` nodo. El supertipo de componente determina el nombre de la propiedad:

   * Etapa del proceso: `PROCESS`
   * Etapa de participante: `PARTICIPANT`
   * Etapa de participante dinámica: `DYNAMIC_PARTICIPANT`

1. Especifique el valor de la propiedad:

   * `PROCESS`: Ruta al script ECMA o al PID del servicio que implementa el comportamiento del paso.
   * `PARTICIPANT`: ID del usuario al que se ha asignado el elemento de trabajo.
   * `DYNAMIC_PARTICIPANT`: Ruta al script ECMA o al PID del servicio que selecciona el usuario para asignar el elemento de trabajo.

1. Para eliminar la capacidad de los desarrolladores de modelos de cambiar los valores de las propiedades, anule el cuadro de diálogo del supertipo de componente.

### Adición de Forms y cuadros de diálogo a los pasos del participante {#adding-forms-and-dialogs-to-participant-steps}

Personalice el componente de paso de participante para proporcionar las funciones que se encuentran en [Etapa de participante de formulario](/help/sites-developing/workflows-step-ref.md#form-participant-step) y [Etapa de participante de diálogo](/help/sites-developing/workflows-step-ref.md#dialog-participant-step) componentes:

* Presentar un formulario al usuario cuando abra el elemento de trabajo generado.
* Presentar un cuadro de diálogo personalizado al usuario cuando complete el elemento de trabajo generado.

Realice el siguiente procedimiento en el nuevo componente (consulte [Creación de componentes de paso de flujo de trabajo personalizados](#creating-custom-workflow-step-components)):

1. Debajo de `cq:Component` , agregue el siguiente nodo:

   * Nombre: `cq:editConfig`
   * Tipo: `cq:EditConfig`

   Para obtener más información sobre el nodo cq:editConfig, consulte [Configuración del comportamiento de edición de un componente](/help/sites-developing/components-basics.md#edit-behavior).

1. Bajo el nodo cq:EditConfig, agregue el siguiente nodo:

   * Nombre: `cq:formParameters`
   * Tipo: `nt:unstructured`

1. Para presentar un formulario cuando el usuario abra el elemento de trabajo, agregue la siguiente propiedad al `cq:formParameters` nodo:

   * Nombre: `FORM_PATH`
   * Tipo: `String`
   * Valor: La ruta que se resuelve en el formulario

1. Para presentar un cuadro de diálogo personalizado cuando el usuario complete el elemento de trabajo, agregue la siguiente propiedad al `cq:formParameters` nodo

   * Nombre: `DIALOG_PATH`
   * Tipo: `String`
   * Valor: la ruta que se resuelve en el cuadro de diálogo

### Configuración del comportamiento del tiempo de ejecución de pasos de flujo de trabajo {#configuring-the-workflow-step-runtime-behavior}

Debajo de `cq:Component` nodo, añadir un `cq:EditConfig` nodo. Debajo de esto, añada un `nt:unstructured` node (debe tener nombre `cq:formParameters`) y a ese nodo agregue las siguientes propiedades:

* Nombre: `PROCESS_AUTO_ADVANCE`

   * Tipo: `Boolean`
   * Valor:

      * cuando se establece en `true` el flujo de trabajo ejecutará ese paso y continuará: esto es predeterminado y también recomendado
      * cuando `false`, el flujo de trabajo se ejecutará y se detendrá; esto requiere una administración adicional, por lo que `true` se recomienda

* Nombre: `DO_NOTIFY`

   * Tipo: `Boolean`
   * Value: indica si se deben enviar notificaciones por correo electrónico para los pasos de participación del usuario (y supone que el servidor de correo está configurado correctamente)

## Conservación y acceso a datos {#persisting-and-accessing-data}

### Conservación de datos para pasos de flujo de trabajo posteriores {#persisting-data-for-subsequent-workflow-steps}

Puede utilizar los metadatos del flujo de trabajo para conservar la información necesaria durante la duración del flujo de trabajo y entre pasos. Un requisito común de los pasos del flujo de trabajo es mantener los datos para un uso futuro o recuperar los datos persistentes de pasos anteriores.

Los metadatos de flujo de trabajo se almacenan en una [`MetaDataMap`](#metadatamaps) objeto. La API de Java proporciona el [`Workflow.getWorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html) método para devolver un [`WorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html) que proporciona el objeto adecuado `MetaDataMap` objeto. Esta `WorkflowData` `MetaDataMap` está disponible para el servicio OSGi o el script ECMA de un componente de paso.

#### Java {#java}

El método execute del `WorkflowProcess` La implementación se pasa el `WorkItem` objeto. Utilice este objeto para obtener el `WorkflowData` para la instancia de flujo de trabajo actual. El siguiente ejemplo agrega un elemento al flujo de trabajo `MetaDataMap` y, a continuación, registra cada elemento. El elemento (&quot;mykey&quot;, &quot;Mi valor de paso&quot;) está disponible para los pasos siguientes en el flujo de trabajo.

```java
public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {

    MetaDataMap wfd = item.getWorkflow().getWorkflowData().getMetaDataMap();

    wfd.put("mykey", "My Step Value");

    Set<String> keyset = wfd.keySet();
    Iterator<String> i = keyset.iterator();
    while (i.hasNext()){
     Object key = i.next();
     log.info("The workflow medata includes key {} and value {}",key.toString(),wfd.get(key).toString());
    }
}
```

#### Script de ECMA {#ecma-script}

El `graniteWorkItem` es la representación de secuencia de comandos ECMA del `WorkItem` Objeto Java. Por lo tanto, puede utilizar la variable `graniteWorkItem` para obtener los metadatos del flujo de trabajo. El siguiente script ECMA se puede utilizar para implementar un **Etapa del proceso** para agregar un elemento al flujo de trabajo `MetaDataMap` y, a continuación, registrar cada elemento. Estos elementos están disponibles para pasos posteriores en el flujo de trabajo.

>[!NOTE]
>
>El `metaData` que está disponible inmediatamente para el script de paso son los metadatos del paso. Los metadatos de la etapa son diferentes de los metadatos del flujo de trabajo.

```
var currentDateInMillis = new Date().getTime();

graniteWorkItem.getWorkflowData().getMetaDataMap().put("hardcodedKey","theKey");

graniteWorkItem.getWorkflowData().getMetaDataMap().put("currentDateInMillisKey",currentDateInMillis);

var iterator = graniteWorkItem.getWorkflowData().getMetaDataMap().keySet().iterator();
while (iterator.hasNext()){
    var key = iterator.next();
    log.info("Workflow metadata key, value = " + key.toString() + ", " + graniteWorkItem.getWorkflowData().getMetaDataMap().get(key));
}
```

### Acceder a valores de propiedad de diálogo en tiempo de ejecución {#accessing-dialog-property-values-at-runtime}

El `MetaDataMap` El objeto de las instancias de flujo de trabajo es útil para almacenar y recuperar datos a lo largo de la duración del flujo de trabajo. Para implementaciones de componentes de paso de flujo de trabajo, la variable `MetaDataMap` es especialmente útil para recuperar valores de propiedad de componentes en tiempo de ejecución.

>[!NOTE]
>
>Para obtener información sobre la configuración del cuadro de diálogo de componentes para almacenar propiedades como metadatos de flujo de trabajo, consulte [Guardar valores de propiedad en metadatos de flujo de trabajo](#saving-property-values-in-workflow-metadata).

El flujo de trabajo `MetaDataMap` está disponible para implementaciones de procesos de scripts Java y ECMA:

* En implementaciones Java de la interfaz WorkflowProcess, la variable `args` El parámetro es el `MetaDataMap` para el flujo de trabajo.

* En implementaciones de scripts ECMA, el valor está disponible mediante la variable `args` y `metadata` variables.

### Ejemplo: Recuperación de los argumentos del componente Paso de proceso {#example-retrieving-the-arguments-of-the-process-step-component}

El cuadro de diálogo de edición de **Etapa del proceso** El componente incluye el **Argumentos** propiedad. El valor del **Argumentos** se almacena en los metadatos del flujo de trabajo y se asocia a la propiedad `PROCESS_ARGS` clave.

En el diagrama siguiente, el valor de **Argumentos** la propiedad es `argument1, argument2`:

![wf-24](assets/wf-24.png)

#### Java {#java-1}

El siguiente código Java es el `execute` método para un `WorkflowProcess` implementación. El método registra el valor en `args` `MetaDataMap` que está asociado con el `PROCESS_ARGS` clave.

```java
public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {
     if (args.containsKey("PROCESS_ARGS")){
      log.info("workflow metadata for key PROCESS_ARGS and value {}",args.get("PROCESS_ARGS","string").toString());
     }
    }
```

Cuando se ejecuta un paso del proceso que utiliza esta implementación de Java, el registro contiene la siguiente entrada:

```xml
16.02.2018 12:07:39.566 *INFO* [JobHandler: /var/workflow/instances/server0/2018-02-16/model_855140139900189:/content/we-retail/de] com.adobe.example.workflow.impl.process.LogArguments workflow metadata for key PROCESS_ARGS and value argument1, argument2
```

#### Script de ECMA {#ecma-script-1}

El siguiente script ECMA se utiliza como proceso para la variable **Etapa del proceso**. Registra el número de argumentos y los valores de los argumentos:

```
var iterator = graniteWorkItem.getWorkflowData().getMetaDataMap().keySet().iterator();
while (iterator.hasNext()){
    var key = iterator.next();
    log.info("Workflow metadata key, value = " + key.toString() + ", " + graniteWorkItem.getWorkflowData().getMetaDataMap().get(key));
}
log.info("hardcodedKey "+ graniteWorkItem.getWorkflowData().getMetaDataMap().get("hardcodedKey"));
log.info("currentDateInMillisKey "+ graniteWorkItem.getWorkflowData().getMetaDataMap().get("currentDateInMillisKey"));
```

>[!NOTE]
>
>En esta sección se describe cómo trabajar con argumentos para pasos de proceso. La información también se aplica a los selectores dinámicos de participantes.

>[!NOTE]
>Para ver otro ejemplo de almacenamiento de propiedades de componentes en metadatos de flujo de trabajo, consulte Ejemplo: Creación de un paso de flujo de trabajo de registrador. Este ejemplo incluye un cuadro de diálogo que asocia el valor de los metadatos con una clave distinta de PROCESS_ARGS.

### Scripts y argumentos de proceso {#scripts-and-process-arguments}

Dentro de un script para una **Etapa del proceso** , los argumentos están disponibles a través del `args` objeto.

Al crear un componente de paso personalizado, el objeto `metaData` está disponible en una secuencia de comandos. Este objeto está limitado a un solo argumento de cadena.

## Desarrollo de implementaciones de pasos de proceso {#developing-process-step-implementations}

Cuando los pasos del proceso se inician durante el proceso de un flujo de trabajo, los pasos envían una solicitud a un servicio OSGi o ejecutan un script ECMA. Desarrolle el servicio o el script ECMA que realice las acciones que requiera el flujo de trabajo.

>[!NOTE]
>
>Para obtener información sobre cómo asociar el componente Paso de proceso con el servicio o script, consulte [Etapa del proceso](/help/sites-developing/workflows-step-ref.md#process-step) o [Anulación de la implementación por pasos](#overriding-the-step-implementation).

### Implementar un paso del proceso con una clase Java {#implementing-a-process-step-with-a-java-class}

Para definir un paso de proceso como un componente de servicio OSGI (paquete Java):

1. Cree el paquete e impleméntelo en el contenedor OSGI. Consulte la documentación sobre la creación de un paquete con [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) o [Eclipse](/help/sites-developing/howto-projects-eclipse.md).

   >[!NOTE]
   >
   >El componente OSGI necesita implementar el `WorkflowProcess` interfaz con su `execute()` método. Consulte el código de ejemplo siguiente.

   >[!NOTE]
   >
   >El nombre del paquete debe añadirse a `<*Private-Package*>` de la sección `maven-bundle-plugin` configuración.

1. Añadir la propiedad SCR `process.label`  y establezca el valor que desee. Este será el nombre con el que se enumera el paso de proceso al utilizar el genérico **Etapa del proceso** componente. Consulte el ejemplo siguiente.
1. En el **Modelos** editor, agregue el paso del proceso al flujo de trabajo utilizando el genérico **Etapa del proceso** componente.
1. En el cuadro de diálogo de edición (de la **Etapa del proceso**), vaya a la **Proceso** y seleccione su implementación de proceso.
1. Si utiliza argumentos en el código, establezca el **Argumentos del proceso**. Por ejemplo: false.
1. Guarde los cambios, tanto para el paso como para el modelo de flujo de trabajo (esquina superior izquierda del editor de modelos).

Los métodos java, respectivamente las clases que implementan el método Java ejecutable, se registran como servicios OSGI, lo que permite agregar métodos en cualquier momento durante el tiempo de ejecución.

El siguiente componente OSGI agrega la propiedad `approved` al nodo de contenido de página cuando la carga útil es una página:

```java
package com.adobe.example.workflow.impl.process;

import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.exec.WorkflowData;
import com.adobe.granite.workflow.exec.WorkflowProcess;
import com.adobe.granite.workflow.metadata.MetaDataMap;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;

import org.osgi.framework.Constants;

import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

/**
 * Sample workflow process that sets an <code>approve</code> property to the payload based on the process argument value.
 */
@Component
@Service
public class MyProcess implements WorkflowProcess {

 @Property(value = "An example workflow process implementation.")
 static final String DESCRIPTION = Constants.SERVICE_DESCRIPTION;
 @Property(value = "Adobe")
 static final String VENDOR = Constants.SERVICE_VENDOR;
 @Property(value = "My Sample Workflow Process")
 static final String LABEL="process.label";

 private static final String TYPE_JCR_PATH = "JCR_PATH";

 public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {
  WorkflowData workflowData = item.getWorkflowData();
  if (workflowData.getPayloadType().equals(TYPE_JCR_PATH)) {
   String path = workflowData.getPayload().toString() + "/jcr:content";
   try {
    Session jcrSession = session.adaptTo(Session.class);
    Node node = (Node) jcrSession.getItem(path);
    if (node != null) {
     node.setProperty("approved", readArgument(args));
     jcrSession.save();
    }
   } catch (RepositoryException e) {
    throw new WorkflowException(e.getMessage(), e);
   }
  }
 }

 private boolean readArgument(MetaDataMap args) {
  String argument = args.get("PROCESS_ARGS", "false");
  return argument.equalsIgnoreCase("true");
 }
}
```

>[!NOTE]
>
>Si el proceso falla tres veces seguidas, se coloca un elemento en la bandeja de entrada del administrador del flujo de trabajo.

### Uso de ECMAScript {#using-ecmascript}

Los scripts ECMA permiten a los desarrolladores de scripts implementar pasos de proceso. Los scripts se encuentran en el repositorio JCR y se ejecutan desde allí.

En la tabla siguiente se enumeran las variables disponibles inmediatamente para procesar scripts, lo que proporciona acceso a los objetos de la API de Java del flujo de trabajo.

| Clase Java | Nombre de variable de script | Descripción |
|---|---|---|
| `com.adobe.granite.workflow.exec.WorkItem` | `graniteWorkItem` | La instancia del paso actual. |
| `com.adobe.granite.workflow.WorkflowSession` | `graniteWorkflowSession` | La sesión de flujo de trabajo de la instancia de paso actual. |
| `String[]` (contiene argumentos de proceso) | `args` | Los argumentos de la etapa. |
| `com.adobe.granite.workflow.metadata.MetaDataMap` | `metaData` | Los metadatos de la instancia de paso actual. |
| `org.apache.sling.scripting.core.impl.InternalScriptHelper` | `sling` | Proporciona acceso al entorno de ejecución de Sling. |

El siguiente script de ejemplo muestra cómo acceder al nodo JCR que representa la carga útil del flujo de trabajo. El `graniteWorkflowSession` se adapta a una variable de sesión JCR, que se utiliza para obtener el nodo de la ruta de carga útil.

```
var workflowData = graniteWorkItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH") {
    var path = workflowData.getPayload().toString();
    var jcrsession = graniteWorkflowSession.adaptTo(Packages.javax.jcr.Session);
    var node = jcrsession.getNode(path);
    if (node.hasProperty("approved")){
     node.setProperty("approved", args[0] == "true" ? true : false);
     node.save();
 }
}
```

El siguiente script comprueba si la carga útil es una imagen ( `.png` ), crea una imagen en blanco y negro a partir de ella y la guarda como nodo secundario.

```
var workflowData = graniteWorkItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH") {
    var path = workflowData.getPayload().toString();
    var jcrsession = graniteWorkflowSession.adaptTo(Packages.javax.jcr.Session);
    var node = jcrsession.getRootNode().getNode(path.substring(1));
     if (node.isNodeType("nt:file") && node.getProperty("jcr:content/jcr:mimeType").getString().indexOf("image/") == 0) {
        var is = node.getProperty("jcr:content/jcr:data").getStream();
        var layer = new Packages.com.day.image.Layer(is);
        layer.grayscale();
                var parent = node.getParent();
                var gn = parent.addNode("grey" + node.getName(), "nt:file");
        var content = gn.addNode("jcr:content", "nt:resource");
                content.setProperty("jcr:mimeType","image/png");
                var cal = Packages.java.util.Calendar.getInstance();
                content.setProperty("jcr:lastModified",cal);
                var f = Packages.java.io.File.createTempFile("test",".png");
        var tout = new Packages.java.io.FileOutputStream(f);
        layer.write("image/png", 1.0, tout);
        var fis = new Packages.java.io.FileInputStream(f);
                content.setProperty("jcr:data", fis);
                parent.save();
        tout.close();
        fis.close();
        is.close();
        f.deleteOnExit();
    }
}
```

Para utilizar la secuencia de comandos:

1. Cree la secuencia de comandos (por ejemplo, con el CRXDE Lite ) y guárdela en el repositorio siguiente `//apps/workflow/scripts/`
1. Para especificar un título que identifique el script en la variable **Etapa del proceso** cuadro de diálogo de edición, agregue las siguientes propiedades al `jcr:content` nodo del script:

   | Nombre | Tipo | Valor  |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | Nombre que aparecerá en el cuadro de diálogo de edición. |

1. Edite el **Etapa del proceso** y especifique la secuencia de comandos que se va a utilizar.

## Desarrollo de selectores de participantes {#developing-participant-choosers}

Puede desarrollar selectores de participantes para **Etapa de participante dinámica** componentes.

Cuando un **Etapa de participante dinámica** El componente se inicia durante un flujo de trabajo y el paso debe determinar el participante al que se puede asignar el elemento de trabajo generado. Para ello, realice el siguiente paso:

* envía una solicitud a un servicio OSGi
* ejecuta un script ECMA para seleccionar el participante

Puede desarrollar un servicio o un script ECMA que seleccione al participante según los requisitos del flujo de trabajo.

>[!NOTE]
>
>Para obtener información sobre cómo asociar su **Etapa de participante dinámica** con el servicio o script, consulte [Etapa de participante dinámica](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step) o [Anulación de la implementación por pasos](#persisting-and-accessing-data).

### Desarrollo de un selector de participantes mediante una clase Java {#developing-a-participant-chooser-using-a-java-class}

Para definir una etapa de participante como un componente de servicio OSGI (clase Java):

1. El componente OSGI necesita implementar el `ParticipantStepChooser` interfaz con su `getParticipant()` método. Consulte el código de ejemplo siguiente.

   Cree el paquete e impleméntelo en el contenedor OSGI.

1. Añadir la propiedad SCR `chooser.label` y establezca el valor según sea necesario. Este será el nombre con el que se enumera el selector de participantes, usando el **Etapa de participante dinámica** componente. Consulte el ejemplo:

   ```java
   package com.adobe.example.workflow.impl.process;
   
   import com.adobe.granite.workflow.WorkflowException;
   import com.adobe.granite.workflow.WorkflowSession;
   import com.adobe.granite.workflow.exec.ParticipantStepChooser;
   import com.adobe.granite.workflow.exec.WorkItem;
   import com.adobe.granite.workflow.exec.WorkflowData;
   import com.adobe.granite.workflow.metadata.MetaDataMap;
   
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   
   import org.osgi.framework.Constants;
   
   /**
    * Sample dynamic participant step that determines the participant based on a path given as argument.
    */
   @Component
   @Service
   
   public class MyDynamicParticipant implements ParticipantStepChooser {
   
    @Property(value = "An example implementation of a dynamic participant chooser.")
    static final String DESCRIPTION = Constants.SERVICE_DESCRIPTION;
       @Property(value = "Adobe")
       static final String VENDOR = Constants.SERVICE_VENDOR;
       @Property(value = "Dynamic Participant Chooser Process")
       static final String LABEL=ParticipantStepChooser.SERVICE_PROPERTY_LABEL;
   
       private static final String TYPE_JCR_PATH = "JCR_PATH";
   
       public String getParticipant(WorkItem workItem, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
           WorkflowData workflowData = workItem.getWorkflowData();
           if (workflowData.getPayloadType().equals(TYPE_JCR_PATH)) {
               String path = workflowData.getPayload().toString();
               String pathFromArgument = args.get("PROCESS_ARGS", String.class);
               if (pathFromArgument != null && path.startsWith(pathFromArgument)) {
                   return "admin";
               }
           }
           return "administrators";
       }
   }
   ```

1. En el **Modelos** editor, agregue el paso participante dinámico al flujo de trabajo utilizando el genérico **Etapa de participante dinámica** componente.
1. En el cuadro de diálogo de edición, seleccione **Selector de participantes** y seleccione la implementación del selector.
1. Si utiliza argumentos en el código, establezca el **Argumentos del proceso**. Para este ejemplo: `/content/we-retail/de`.
1. Guarde los cambios, tanto para el paso como para el modelo del flujo de trabajo.

### Desarrollo de un selector de participantes mediante un script ECMA {#developing-a-participant-chooser-using-an-ecma-script}

Puede crear un script ECMA que seleccione el usuario al que se asigna el elemento de trabajo que el **Etapa de participante** genera. La secuencia de comandos debe incluir una función denominada `getParticipant` que no requiere argumentos y devuelve un valor `String` que contiene el ID de un usuario o grupo.

Los scripts se encuentran en el repositorio JCR y se ejecutan desde allí.

En la tabla siguiente se enumeran las variables que proporcionan acceso inmediato a los objetos Java de flujo de trabajo en los scripts.

| Clase Java | Nombre de variable de script |
|---|---|
| `com.adobe.granite.workflow.exec.WorkItem` | `graniteWorkItem` |
| `com.adobe.granite.workflow.WorkflowSession` | `graniteWorkflowSession` |
| `String[]` (contiene argumentos de proceso) | `args` |
| `com.adobe.granite.workflow.metadata.MetaDataMap` | `metaData` |
| `org.apache.sling.scripting.core.impl.InternalScriptHelper` | `sling` |

```
function getParticipant() {
    var workflowData = graniteWorkItem.getWorkflowData();
    if (workflowData.getPayloadType() == "JCR_PATH") {
        var path = workflowData.getPayload().toString();
        if (path.indexOf("/content/we-retail/de") == 0) {
            return "admin";
        } else {
            return "administrators";
        }
    }
}
```

1. Cree la secuencia de comandos (por ejemplo, con el CRXDE Lite ) y guárdela en el repositorio siguiente `//apps/workflow/scripts`
1. Para especificar un título que identifique el script en la variable **Etapa del proceso** cuadro de diálogo de edición, agregue las siguientes propiedades al `jcr:content` nodo del script:

   | Nombre | Tipo | Valor  |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | Nombre que aparecerá en el cuadro de diálogo de edición. |

1. Edite el [Etapa de participante dinámica](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step) y especifique la secuencia de comandos que se va a utilizar.

## Administrar paquetes de flujo de trabajo {#handling-workflow-packages}

[Paquetes de flujo de trabajo](/help/sites-authoring/workflows-applying.md#specifying-workflow-details-in-the-create-workflow-wizard) se puede pasar a un flujo de trabajo para su procesamiento. Los paquetes de flujo de trabajo contienen referencias a recursos como páginas y recursos.

>[!NOTE]
>
>Los siguientes pasos del proceso de flujo de trabajo aceptan paquetes de flujo de trabajo para la activación masiva de páginas:
>
>* [`com.day.cq.wcm.workflow.process.ActivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/ActivatePageProcess.html)
>* [`com.day.cq.wcm.workflow.process.DeactivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/DeactivatePageProcess.html)
>

Puede desarrollar pasos del flujo de trabajo que obtengan los recursos del paquete y los procesen. Los siguientes miembros del `com.day.cq.workflow.collection` proporcionan acceso a los paquetes de flujo de trabajo:

* `ResourceCollection`: clase de paquete de flujo de trabajo.
* `ResourceCollectionUtil`: se utiliza para recuperar objetos ResourceCollection.
* `ResourceCollectionManager`: crea y recupera colecciones. Una implementación se implementa como un servicio OSGi.

En el siguiente ejemplo, la clase Java muestra cómo obtener recursos de paquetes:

```java
package com.adobe.example;

import java.util.ArrayList;
import java.util.List;

import com.day.cq.workflow.WorkflowException;
import com.day.cq.workflow.WorkflowSession;
import com.day.cq.workflow.collection.ResourceCollection;
import com.day.cq.workflow.collection.ResourceCollectionManager;
import com.day.cq.workflow.collection.ResourceCollectionUtil;
import com.day.cq.workflow.exec.WorkItem;
import com.day.cq.workflow.exec.WorkflowData;
import com.day.cq.workflow.exec.WorkflowProcess;
import com.day.cq.workflow.metadata.MetaDataMap;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Reference;
import org.osgi.framework.Constants;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import javax.jcr.Node;
import javax.jcr.PathNotFoundException;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

@Component
@Service
public class LaunchBulkActivate implements WorkflowProcess {

 private static final Logger log = LoggerFactory.getLogger(LaunchBulkActivate.class);

 @Property(value="Bulk Activate for Launches")
  static final String PROCESS_NAME ="process.label";
 @Property(value="A sample workflow process step to support Launches bulk activation of pages")
 static final String SERVICE_DESCRIPTION = Constants.SERVICE_DESCRIPTION;

 @Reference
 private ResourceCollectionManager rcManager;
public void execute(WorkItem workItem, WorkflowSession workflowSession) throws Exception {
    Session session = workflowSession.getSession();
    WorkflowData data = workItem.getWorkflowData();
    String path = null;
    String type = data.getPayloadType();
    if (type.equals(TYPE_JCR_PATH) && data.getPayload() != null) {
        String payloadData = (String) data.getPayload();
        if (session.itemExists(payloadData)) {
            path = payloadData;
        }
    } else if (data.getPayload() != null && type.equals(TYPE_JCR_UUID)) {
        Node node = session.getNodeByUUID((String) data.getPayload());
        path = node.getPath();
    }

    // CUSTOMIZED CODE IF REQUIRED....

    if (path != null) {
        // check for resource collection
        ResourceCollection rcCollection = ResourceCollectionUtil.getResourceCollection((Node)session.getItem(path), rcManager);
        // get list of paths to replicate (no resource collection: size == 1
        // otherwise size >= 1
        List<String> paths = getPaths(path, rcCollection);
        for (String aPath: paths) {

            // CUSTOMIZED CODE....

        }
    } else {
        log.warn("Cannot process because path is null for this " + "workitem: " + workItem.toString());
    }
}

/**
 * helper
 */
private List<String> getPaths(String path, ResourceCollection rcCollection) {
    List<String> paths = new ArrayList<String>();
    if (rcCollection == null) {
        paths.add(path);
    } else {
        log.debug("ResourceCollection detected " + rcCollection.getPath());
        // this is a resource collection. the collection itself is not
        // replicated. only its members
        try {
            List<Node> members = rcCollection.list(new String[]{"cq:Page", "dam:Asset"});
            for (Node member: members) {
                String mPath = member.getPath();
                paths.add(mPath);
            }
        } catch(RepositoryException re) {
            log.error("Cannot build path list out of the resource collection " + rcCollection.getPath());
        }
    }
    return paths;
}
}
```

## Ejemplo: Creación de un paso personalizado {#example-creating-a-custom-step}

Una manera sencilla de empezar a crear su propio paso personalizado es copiar un paso existente de:

`/libs/cq/workflow/components/model`

### Creación del paso básico {#creating-the-basic-step}

1. Vuelva a crear la ruta en /apps; por ejemplo:

   `/apps/cq/workflow/components/model`

   Las carpetas nuevas son del tipo `nt:folder`:

   ```xml
   - apps
     - cq
       - workflow (nt:folder)
         - components (nt:folder)
           - model (nt:folder)
   ```

   >[!NOTE]
   >
   >Este paso no se aplica al editor del modelo de interfaz de usuario clásico.

1. A continuación, coloque el paso copiado en la carpeta /apps; por ejemplo:

   `/apps/cq/workflow/components/model/myCustomStep`

   Este es el resultado de nuestro ejemplo de paso personalizado:

   ![wf-34](assets/wf-34.png)

   >[!CAUTION]
   >
   >Porque en la IU estándar, solo el título y no los detalles no se muestran en la tarjeta, `details.jsp` no es necesario, ya que era para el editor de IU clásico.

1. Aplique las siguientes propiedades al nodo:

   `/apps/cq/workflow/components/model/myCustomStep`

   **Propiedades de interés:**

   * `sling:resourceSuperType`

     Debe heredar de un paso existente.

     En este ejemplo, heredamos del paso base en `cq/workflow/components/model/step`, pero puede utilizar otros supertipos como `participant`, `process`, etc.

   * `jcr:title`

     Es el título que se muestra cuando el componente aparece en la lista en el explorador de pasos (panel izquierdo del editor de modelos de flujo de trabajo).

   * `cq:icon`

     Se utiliza para especificar un [Icono de Coral](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) para el paso.

   * `componentGroup`

     Debe ser uno de los siguientes:

      * Flujo de trabajo de colaboración
      * Flujo de trabajo DAM
      * Flujo de trabajo de formularios
      * Proyectos
      * Flujo de trabajo WCM
      * Flujo de trabajo

   ![wf-35](assets/wf-35.png)

1. Ahora puede abrir un modelo de flujo de trabajo para editarlo. En el explorador de pasos puede filtrar para ver **Mi paso personalizado**:

   ![wf-36](assets/wf-36.png)

   Arrastrando **Mi paso personalizado** en el modelo se muestra la tarjeta:

   ![wf-37](assets/wf-37.png)

   Si no `cq:icon` se ha definido para el paso y, a continuación, se representa un icono predeterminado con las dos primeras letras del título. Por ejemplo:

   ![wf-38](assets/wf-38.png)

#### Definición del cuadro de diálogo Configurar paso {#defining-the-step-configure-dialog}

Después [Creación del paso básico](#creating-the-basic-step), defina la etapa **Configurar** como se indica a continuación:

1. Configure las propiedades en el nodo `cq:editConfig` como sigue:

   **Propiedades de interés:**

   * `cq:inherit`

     Cuando se establece en `true`, el componente paso heredará las propiedades del paso especificado en `sling:resourceSuperType`.

   * `cq:disableTargeting`

     Configúrelo como sea necesario.

   ![wf-39](assets/wf-39.png)

1. Configure las propiedades en el nodo `cq:formsParameter` como sigue:

   **Propiedades de interés:**

   * `jcr:title`

     Establece el título predeterminado en la tarjeta de paso del mapa del modelo y en la variable **Título** del campo **Mi personalizado: propiedades de la etapa** diálogo de configuración.

   * También puede definir sus propias propiedades personalizadas.

   ![wf-40](assets/wf-40.png)

1. Configure las propiedades en el nodo `cq:listeners`.

   El `cq:listener` El nodo y sus propiedades permiten establecer controladores de eventos que reaccionan a los eventos en el editor de modelos de interfaz de usuario táctil; como arrastrar un paso a una página de modelo o editar propiedades de un paso.

   **Propiedades de interés:**

   * `afterMove: REFRESH_PAGE`
   * `afterdelete: CQ.workflow.flow.Step.afterDelete`
   * `afteredit: CQ.workflow.flow.Step.afterEdit`
   * `afterinsert: CQ.workflow.flow.Step.afterInsert`

   Esta configuración es esencial para el correcto funcionamiento del editor. En la mayoría de los casos, esta configuración no debe cambiarse.

   Sin embargo, configurar `cq:inherit` a true (en el `cq:editConfig` , consulte más arriba) le permite heredar esta configuración, sin necesidad de incluirla explícitamente en su definición de paso. Si no hay herencia, debe agregar este nodo con las siguientes propiedades y valores.

   En este ejemplo, la herencia se ha activado para que se pueda eliminar el `cq:listeners` y el paso seguirá funcionando correctamente.

   ![wf-41](assets/wf-41.png)

1. Ahora puede agregar una instancia del paso a un modelo de flujo de trabajo. Cuando usted **Configurar** En el paso verá el cuadro de diálogo:

   ![wf-42](assets/wf-42.png) ![wf-43](assets/wf-43.png)

#### Marcado de muestra utilizado en este ejemplo {#sample-markup-used-in-this-example}

El marcado de un paso personalizado se debe representar en la variable `.content.xml` del nodo raíz del componente. La muestra `.content.xml` se utiliza para este ejemplo:

`/apps/cq/workflow/components/model/myCustomStep/.content.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:icon="bell"
    jcr:primaryType="cq:Component"
    jcr:title="My Custom Step"
    sling:resourceSuperType="cq/workflow/components/model/process"
    allowedParents="[*/parsys]"
    componentGroup="Workflow"/>
```

El `_cq_editConfig.xml` ejemplo utilizado en este ejemplo:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    cq:disableTargeting="{Boolean}true"
    cq:inherit="{Boolean}true"
    jcr:primaryType="cq:EditConfig">
    <cq:formParameters
        jcr:primaryType="nt:unstructured"
        jcr:title="My Custom Step Card"
        SAMPLE_PROPERY="sample value"/>
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="CQ.workflow.flow.Step.afterDelete"
        afteredit="CQ.workflow.flow.Step.afterEdit"
        afterinsert="CQ.workflow.flow.Step.afterInsert"
        afterMove="REFRESH_PAGE"/>
</jcr:root>
```

El `_cq_dialog/.content.xml` ejemplo utilizado en este ejemplo:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    jcr:title="My Custom - Step Properties"
    sling:resourceType="cq/gui/components/authoring/dialog">
    <content
        jcr:primaryType="nt:unstructured"
        sling:resourceType="granite/ui/components/coral/foundation/tabs">
        <items jcr:primaryType="nt:unstructured">
            <common
                cq:hideOnEdit="true"
                jcr:primaryType="nt:unstructured"
                jcr:title="Common"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns"/>
            <process
                cq:hideOnEdit="true"
                jcr:primaryType="nt:unstructured"
                jcr:title="Process"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns"/>
            <mycommon
                jcr:primaryType="nt:unstructured"
                jcr:title="Common"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                <items jcr:primaryType="nt:unstructured">
                    <columns
                        jcr:primaryType="nt:unstructured"
                        sling:resourceType="granite/ui/components/coral/foundation/container">
                        <items jcr:primaryType="nt:unstructured">
                            <title
                                jcr:primaryType="nt:unstructured"
                                sling:resourceType="granite/ui/components/coral/foundation/form/textfield"
                                fieldLabel="Title"
                                name="./jcr:title"/>
                            <description
                                jcr:primaryType="nt:unstructured"
                                sling:resourceType="granite/ui/components/coral/foundation/form/textarea"
                                fieldLabel="Description"
                                name="./jcr:description"/>
                        </items>
                    </columns>
                </items>
            </mycommon>
            <advanced
                jcr:primaryType="nt:unstructured"
                jcr:title="Advanced"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                <items jcr:primaryType="nt:unstructured">
                    <columns
                        jcr:primaryType="nt:unstructured"
                        sling:resourceType="granite/ui/components/coral/foundation/container">
                        <items jcr:primaryType="nt:unstructured">
                            <email
                                jcr:primaryType="nt:unstructured"
                                sling:resourceType="granite/ui/components/coral/foundation/form/checkbox"
                                fieldDescription="Notify user via email."
                                fieldLabel="Email"
                                name="./metaData/PROCESS_AUTO_ADVANCE"
                                text="Notify user via email."
                                value="true"/>
                        </items>
                    </columns>
                </items>
            </advanced>
        </items>
    </content>
</jcr:root>
```

>[!NOTE]
>
>Observe los nodos comunes y de proceso en la definición del cuadro de diálogo. Se heredan del paso de proceso que utilizamos como supertipo para nuestro paso personalizado:
>
>`sling:resourceSuperType : cq/workflow/components/model/process`

>[!NOTE]
>
>Los cuadros de diálogo del editor del modelo de interfaz de usuario clásica seguirán funcionando con el editor de interfaz de usuario táctil estándar.
>
>AEM Aunque tiene un [herramientas de modernización](/help/sites-developing/modernization-tools.md) si desea actualizar los cuadros de diálogo de los pasos de la IU clásica a los cuadros de diálogo de la IU estándar. Después de la conversión, aún hay algunas mejoras manuales que se pueden realizar en el cuadro de diálogo para determinados casos.
>
>* En los casos en los que un cuadro de diálogo actualizado esté vacío, puede consultar los cuadros de diálogo en `/libs` que tienen una funcionalidad similar a la de los ejemplos de cómo proporcionar una solución. Por ejemplo:
>
>* `/libs/cq/workflow/components/model`
>* `/libs/cq/workflow/components/workflow`
>* `/libs/dam/components`
>* `/libs/wcm/workflow/components/autoassign`
>* `/libs/cq/projects`
>
>  No debe modificar nada en `/libs`, utilícelos simplemente como ejemplos. Si desea aprovechar cualquiera de los pasos existentes, cópielos en `/apps` y modifíquelas allí.
