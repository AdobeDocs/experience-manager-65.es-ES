---
title: Ampliación de la funcionalidad del flujo de trabajo
seo-title: Ampliación de la funcionalidad del flujo de trabajo
description: Ampliación de la funcionalidad del flujo de trabajo
seo-description: nulo
uuid: 9f4ea2a8-8b21-4e7c-ac73-dd37d9ada111
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: f23408c3-6b37-4047-9cce-0cab97bb6c5c
translation-type: tm+mt
source-git-commit: 7035c19a109ff67655ee0419aa37d1723e2189cc
workflow-type: tm+mt
source-wordcount: '3587'
ht-degree: 1%

---


# Ampliación de la funcionalidad del flujo de trabajo{#extending-workflow-functionality}

En este tema se describe cómo desarrollar componentes de paso personalizados para los flujos de trabajo y cómo interactuar mediante programación con los flujos de trabajo.

La creación de un paso de flujo de trabajo personalizado implica las siguientes actividades:

* Desarrolle el componente de paso del flujo de trabajo.
* Implemente la funcionalidad de los pasos como un servicio OSGi o un script ECMA.

También puede [interactuar con sus flujos de trabajo desde sus programas y secuencias de comandos](/help/sites-developing/workflows-program-interaction.md).

## Componentes de los pasos del flujo de trabajo: conceptos básicos {#workflow-step-components-the-basics}

Un componente de paso de flujo de trabajo define el aspecto y el comportamiento del paso al crear modelos de flujo de trabajo:

* La categoría y el nombre del paso en la barra de tareas del flujo de trabajo.
* El aspecto del paso en los modelos de flujo de trabajo.
* El cuadro de diálogo de edición para configurar las propiedades de los componentes.
* El servicio o la secuencia de comandos que se ejecutan durante la ejecución.

Al igual que con [todos los componentes](/help/sites-developing/components.md), los componentes de paso del flujo de trabajo heredan del componente especificado para la propiedad `sling:resourceSuperType` . El diagrama siguiente muestra la jerarquía de nodos `cq:component` que forman la base de todos los componentes del paso del flujo de trabajo. El diagrama también incluye los componentes **Paso de proceso**, **Paso de participante** y **Paso de participante dinámico**, ya que estos son los puntos de partida más comunes (y básicos) para desarrollar componentes de paso personalizados.

![aem_wf_components_herit](assets/aem_wf_componentinherit.png)

>[!CAUTION]
>
>***no debe*** cambiar nada en la ruta `/libs`.
>
>Esto se debe a que el contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y puede sobrescribirse al aplicar una corrección o un paquete de funciones).
>
>El método recomendado para la configuración y otros cambios es:
>
>1. Volver a crear el elemento requerido (es decir, tal como existe en `/libs` en `/apps`
>2. Realizar cambios en `/apps`


El componente `/libs/cq/workflow/components/model/step` es el antecesor común más cercano de **Paso de proceso**, **Paso de participante** y **Paso de participante dinámico**, que heredan todos los elementos siguientes:

* `step.jsp`

   La secuencia de comandos `step.jsp` renderiza el título del componente del paso cuando se agrega a un modelo.

   ![wf-22-1](assets/wf-22-1.png)

* [cq:dialog](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog)

   Un cuadro de diálogo con las fichas siguientes:

   * **Frecuentes**: para editar el título y la descripción.
   * **Avanzado**: para editar las propiedades de las notificaciones por correo electrónico.

   ![wf-44](assets/wf-44.png) ![wf-45](assets/wf-45.png)

   >[!NOTE]
   >
   >Cuando las pestañas del cuadro de diálogo de edición de un componente de paso no coinciden con este aspecto predeterminado, el componente de paso tiene secuencias de comandos, propiedades de nodo o pestañas de diálogo definidas que anulan estas pestañas heredadas.

### Scripts ECMA {#ecma-scripts}

Los siguientes objetos están disponibles (según el tipo de paso) en las secuencias de comandos de ECMA:

* [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkItem.html) WorkItemWorkItem
* [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/WorkflowSession.html) WorkflowSessionworkflowSession
* [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkflowData.html) WorkflowDataworkflowData
* `args`: matriz con los argumentos de proceso.

* `sling`: para acceder a otros servicios osgi.
* `jcrSession`

### MetaDataMaps {#metadatamaps}

Puede utilizar metadatos de flujo de trabajo para mantener la información necesaria durante la duración del flujo de trabajo. Un requisito común de los pasos del flujo de trabajo es mantener los datos para su uso futuro en el flujo de trabajo o recuperar los datos persistentes.

Existen tres tipos de objetos MetaDataMap: para objetos `Workflow`, `WorkflowData` y `WorkItem`. Todos tienen el mismo propósito: almacenar metadatos.

Un elemento de trabajo tiene su propio MetaDataMap que solo se puede usar mientras se esté ejecutando ese elemento de trabajo (por ejemplo, el paso ).

Los metadatos `Workflow` y `WorkflowData` se comparten en todo el flujo de trabajo. En estos casos, se recomienda utilizar únicamente el mapa de metadatos `WorkflowData`.

## Creación de componentes de paso de flujo de trabajo personalizados {#creating-custom-workflow-step-components}

Los componentes de paso del flujo de trabajo se pueden [crear de la misma manera que cualquier otro componente](/help/sites-developing/components.md).

Para heredar de uno de los componentes de paso base (existentes), agregue la siguiente propiedad al nodo `cq:Component` :

* Nombre: `sling:resourceSuperType`
* Tipo: `String`
* Valor: Una de las rutas siguientes que se resuelve en un componente base:

   * `cq/workflow/components/model/process`
   * `cq/workflow/components/model/participant`
   * `cq/workflow/components/model/dynamic_participant`

### Especificación del título y la descripción predeterminados para las instancias de paso {#specifying-the-default-title-and-description-for-step-instances}

Utilice el siguiente procedimiento para especificar los valores predeterminados de los campos **Title** y **Description** en la pestaña **Common**.

>[!NOTE]
>
>Los valores de los campos aparecen en la instancia del paso cuando se cumplen los dos requisitos siguientes:
>
>* El cuadro de diálogo de edición del paso almacena el título y la descripción en las siguientes ubicaciones: >
>* `./jcr:title`
>* `./jcr:description` ubicaciones

>
>  
Este requisito se cumple cuando el cuadro de diálogo de edición utiliza la pestaña Común que implementa el componente `/libs/cq/flow/components/step/step` .
>
>* El componente de paso o un antecesor del componente no anula la secuencia de comandos `step.jsp` que implementa el componente `/libs/cq/flow/components/step/step`.


1. Bajo el nodo `cq:Component`, agregue el siguiente nodo:

   * Nombre: `cq:editConfig`
   * Tipo: `cq:EditConfig`

   >[!NOTE]
   >
   >Para obtener más información sobre el nodo cq:editConfig , consulte [Configuración del comportamiento de edición de un componente](/help/sites-developing/developing-components.md#configuring-the-edit-behavior).

1. Bajo el nodo `cq:EditConfig`, agregue el siguiente nodo:

   * Nombre: `cq:formParameters`
   * Tipo: `nt:unstructured`

1. Agregue `String` propiedades de los nombres siguientes al nodo `cq:formParameters`:

   * `jcr:title`: El valor rellena el campo  **** Título de la  **** ficha Común.
   * `jcr:description`: El valor rellena el campo  **** Descripción de la  **** pestaña Comúnmente.

### Guardar valores de propiedades en metadatos de flujo de trabajo {#saving-property-values-in-workflow-metadata}

>[!NOTE]
>
>Consulte [Persistencia y acceso a datos](#persisting-and-accessing-data). En concreto, para obtener información sobre el acceso al valor de propiedad en tiempo de ejecución, consulte [Acceso a los valores de propiedad de cuadro de diálogo en tiempo de ejecución](#accessing-dialog-property-values-at-runtime).

La propiedad name de los elementos `cq:Widget` especifica el nodo JCR que almacena el valor del widget. Cuando los widgets del cuadro de diálogo de los componentes de paso del flujo de trabajo almacenan valores por debajo del nodo `./metaData` , el valor se añade al flujo de trabajo `MetaDataMap`.

Por ejemplo, un campo de texto de un cuadro de diálogo es un nodo `cq:Widget` que tiene las siguientes propiedades:

| Nombre | Tipo | Value |
|---|---|---|
| `xtype` | `String` | `textarea` |
| `name` | `String` | `./metaData/subject` |
| `fieldLabel` | `String` | `Email Subject` |

El valor especificado en este campo de texto se agrega al objeto ` [MetaDataMap](#metadatamaps)` de la instancia de flujo de trabajo y se asocia con la clave `subject`.

>[!NOTE]
>
>Cuando la clave es `PROCESS_ARGS`, el valor está fácilmente disponible en las implementaciones de secuencias de comandos de ECMA a través de la variable `args` . En este caso, el valor de la propiedad name es `./metaData/PROCESS_ARGS.`

### Anulación de la implementación de pasos {#overriding-the-step-implementation}

Cada componente de paso base permite a los desarrolladores de modelos de flujo de trabajo configurar las siguientes funciones clave en el momento del diseño:

* Paso del proceso: El servicio o la secuencia de comandos ECMA que se ejecutará durante la ejecución.
* Etapa del participante: El ID del usuario al que se asigna el elemento de trabajo generado.
* Etapa de participante dinámica: El servicio o la secuencia de comandos ECMA que selecciona el ID del usuario al que se asigna el elemento de trabajo.

Para enfocar el componente para utilizarlo en un escenario de flujo de trabajo específico, configure la función clave en el diseño y elimine la capacidad de los desarrolladores de modelos para cambiarlo.

1. Bajo el nodo cq:component , agregue el siguiente nodo:

   * Nombre: `cq:editConfig`
   * Tipo: `cq:EditConfig`

   Para obtener más información sobre el nodo cq:editConfig , consulte [Configuración del comportamiento de edición de un componente](/help/sites-developing/developing-components.md#configuring-the-edit-behavior).

1. Debajo del nodo cq:EditConfig , agregue el siguiente nodo:

   * Nombre: `cq:formParameters`
   * Tipo: `nt:unstructured`

1. Agregue una propiedad `String` al nodo `cq:formParameters`. El supertipo de componente determina el nombre de la propiedad:

   * Etapa del proceso: `PROCESS`
   * Etapa de participante: `PARTICIPANT`
   * Etapa de participante dinámica: `DYNAMIC_PARTICIPANT`

1. Especifique el valor de la propiedad:

   * `PROCESS`: Ruta al script ECMA o al PID del servicio que implementa el comportamiento del paso.
   * `PARTICIPANT`: ID del usuario al que se asigna el elemento de trabajo.
   * `DYNAMIC_PARTICIPANT`: Ruta de acceso al script ECMA o al PID del servicio que selecciona al usuario para asignar el elemento de trabajo.

1. Para eliminar la capacidad de los desarrolladores de modelos para cambiar los valores de propiedad, anule el cuadro de diálogo del supertipo de componente.

### Añadir Forms y cuadros de diálogo a los pasos de los participantes {#adding-forms-and-dialogs-to-participant-steps}

Personalice el componente de paso del participante para proporcionar las funciones que se encuentran en los componentes [Paso del participante en el formulario](/help/sites-developing/workflows-step-ref.md#form-participant-step) y [Paso del participante en el cuadro de diálogo](/help/sites-developing/workflows-step-ref.md#dialog-participant-step):

* Presente un formulario al usuario cuando abra el elemento de trabajo generado.
* Presente un cuadro de diálogo personalizado al usuario cuando complete el elemento de trabajo generado.

Realice el siguiente procedimiento en el nuevo componente (consulte [Creación de componentes de paso de flujo de trabajo personalizados](#creating-custom-workflow-step-components)):

1. Bajo el nodo `cq:Component`, agregue el siguiente nodo:

   * Nombre: `cq:editConfig`
   * Tipo: `cq:EditConfig`

   Para obtener más información sobre el nodo cq:editConfig , consulte [Configuración del comportamiento de edición de un componente](/help/sites-developing/components-basics.md#edit-behavior).

1. Debajo del nodo cq:EditConfig , agregue el siguiente nodo:

   * Nombre: `cq:formParameters`
   * Tipo: `nt:unstructured`

1. Para presentar un formulario cuando el usuario abra el elemento de trabajo, agregue la siguiente propiedad al nodo `cq:formParameters` :

   * Nombre: `FORM_PATH`
   * Tipo: `String`
   * Valor: Ruta de acceso que se resuelve en el formulario

1. Para presentar un cuadro de diálogo personalizado cuando el usuario complete el elemento de trabajo, agregue la siguiente propiedad al nodo `cq:formParameters`

   * Nombre: `DIALOG_PATH`
   * Tipo: `String`
   * Valor: La ruta que se resuelve en el cuadro de diálogo

### Configuración del comportamiento del tiempo de ejecución de los pasos del flujo de trabajo {#configuring-the-workflow-step-runtime-behavior}

Bajo el nodo `cq:Component`, agregue un nodo `cq:EditConfig`. A continuación, agregue un nodo `nt:unstructured` (debe llamarse `cq:formParameters`) y a ese nodo agregue las siguientes propiedades:

* Nombre: `PROCESS_AUTO_ADVANCE`

   * Tipo: `Boolean`
   * Value:

      * cuando se establece en `true`, el flujo de trabajo ejecutará ese paso y continuará: este es el valor predeterminado y también se recomienda
      * cuando `false`, el flujo de trabajo se ejecutará y se detendrá; esto requiere una administración adicional, por lo que se recomienda `true`

* Nombre: `DO_NOTIFY`

   * Tipo: `Boolean`
   * Valor: indica si se deben enviar notificaciones por correo electrónico para los pasos de participación del usuario (y supone que el servidor de correo está configurado correctamente)

## Persistencia y acceso a datos {#persisting-and-accessing-data}

### Datos persistentes para pasos subsiguientes del flujo de trabajo {#persisting-data-for-subsequent-workflow-steps}

Puede utilizar metadatos de flujo de trabajo para mantener la información necesaria durante la duración del flujo de trabajo y entre pasos. Un requisito común de los pasos del flujo de trabajo es persistir en los datos para su uso futuro o recuperar los datos persistentes de pasos anteriores.

Los metadatos del flujo de trabajo se almacenan en un objeto [`MetaDataMap`](#metadatamaps). La API de Java proporciona el método [`Workflow.getWorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html) para devolver un objeto [`WorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html) que proporciona el objeto `MetaDataMap` apropiado. Este `WorkflowData` `MetaDataMap` objeto está disponible para el servicio OSGi o la secuencia de comandos ECMA de un componente de paso.

#### Java {#java}

El método execute de la implementación `WorkflowProcess` se pasa al objeto `WorkItem`. Utilice este objeto para obtener el objeto `WorkflowData` para la instancia de flujo de trabajo actual. En el siguiente ejemplo se agrega un elemento al objeto `MetaDataMap` del flujo de trabajo y, a continuación, se registra cada elemento. El elemento (&quot;mykey&quot;, &quot;My Step Value&quot;) está disponible para los pasos siguientes del flujo de trabajo.

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

La variable `graniteWorkItem` es la representación de secuencia de comandos ECMA del objeto Java actual `WorkItem`. Por lo tanto, puede utilizar la variable `graniteWorkItem` para obtener los metadatos del flujo de trabajo. La siguiente secuencia de comandos ECMA se puede utilizar para implementar un **paso de proceso** para agregar un elemento al objeto de flujo de trabajo `MetaDataMap` y luego registrar cada elemento. Estos elementos están disponibles para los pasos posteriores del flujo de trabajo.

>[!NOTE]
>
>La variable `metaData` que está disponible inmediatamente para el script de paso son los metadatos del paso. Los metadatos de paso son diferentes de los metadatos del flujo de trabajo.

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

### Acceso a los valores de propiedad de cuadro de diálogo en tiempo de ejecución {#accessing-dialog-property-values-at-runtime}

El objeto `MetaDataMap` de las instancias de flujo de trabajo es útil para almacenar y recuperar datos durante toda la duración del flujo de trabajo. Para implementaciones de componentes de paso de flujo de trabajo, el `MetaDataMap` es especialmente útil para recuperar valores de propiedad de componente durante la ejecución.

>[!NOTE]
>
>Para obtener información sobre la configuración del cuadro de diálogo de componentes para almacenar propiedades como metadatos de flujo de trabajo, consulte [Guardar valores de propiedades en metadatos de flujo de trabajo](#saving-property-values-in-workflow-metadata).

El flujo de trabajo `MetaDataMap` está disponible para las implementaciones de procesos de script Java y ECMA:

* En implementaciones Java de la interfaz WorkflowProcess, el parámetro `args` es el objeto `MetaDataMap` para el flujo de trabajo.

* En implementaciones de secuencias de comandos ECMA, el valor está disponible mediante las variables `args` y `metadata` .

### Ejemplo: Recuperación de los argumentos del componente de paso de proceso {#example-retrieving-the-arguments-of-the-process-step-component}

El cuadro de diálogo de edición del componente **Paso de proceso** incluye la propiedad **Argumentos**. El valor de la propiedad **Arguments** se almacena en los metadatos del flujo de trabajo y se asocia con la clave `PROCESS_ARGS`.

En el diagrama siguiente, el valor de la propiedad **Arguments** es `argument1, argument2`:

![wf-24](assets/wf-24.png)

#### Java {#java-1}

El siguiente código Java es el método `execute` para una implementación `WorkflowProcess`. El método registra el valor en el `args` `MetaDataMap` asociado con la clave `PROCESS_ARGS`.

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

El siguiente script ECMA se utiliza como proceso para el **paso del proceso**. Registra el número de argumentos y los valores de argumento:

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
>En esta sección se describe cómo trabajar con argumentos para pasos de proceso. La información también se aplica a los usuarios que elijan participantes de forma dinámica.

>[!NOTE]
>Para ver otro ejemplo del almacenamiento de propiedades de componentes en metadatos de flujo de trabajo, consulte Ejemplo: Crear un paso de flujo de trabajo de registrador . Este ejemplo incluye un cuadro de diálogo que asocia el valor de los metadatos con una clave distinta de PROCESS_ARGS.

### Secuencias de comandos y argumentos de proceso {#scripts-and-process-arguments}

Dentro de una secuencia de comandos para un componente **Paso de proceso**, los argumentos están disponibles a través del objeto `args`.

Al crear un componente de paso personalizado, el objeto `metaData` está disponible en una secuencia de comandos. Este objeto está limitado a un único argumento de cadena.

## Desarrollo de implementaciones de pasos de proceso {#developing-process-step-implementations}

Cuando se inician los pasos del proceso durante el proceso de un flujo de trabajo, los pasos envían una solicitud a un servicio OSGi o ejecutan una secuencia de comandos ECMA. Desarrolle el servicio o la secuencia de comandos ECMA que realice las acciones que requiera su flujo de trabajo.

>[!NOTE]
>
>Para obtener información sobre la asociación del componente Paso de proceso con el servicio o la secuencia de comandos, consulte [Paso de proceso](/help/sites-developing/workflows-step-ref.md#process-step) o [Anulación de la implementación del paso](#overriding-the-step-implementation).

### Implementación de un paso de proceso con una clase Java {#implementing-a-process-step-with-a-java-class}

Para definir un paso del proceso como un componente de servicio OSGI (paquete Java):

1. Cree el paquete e impleméntelo en el contenedor OSGI. Consulte la documentación sobre la creación de un paquete con [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) o [Eclipse](/help/sites-developing/howto-projects-eclipse.md).

   >[!NOTE]
   >
   >El componente OSGI debe implementar la interfaz `WorkflowProcess` con su método `execute()`. Consulte el código de ejemplo a continuación.

   >[!NOTE]
   >
   >El nombre del paquete debe añadirse a la sección `<*Private-Package*>` de la configuración `maven-bundle-plugin`.

1. Agregue la propiedad SCR `process.label` y establezca el valor como necesite. Este será el nombre como aparece en el paso del proceso al utilizar el componente genérico **Paso del proceso**. Consulte el ejemplo siguiente.
1. En el editor **Models** , agregue el paso de proceso al flujo de trabajo mediante el componente genérico **Process Step**.
1. En el cuadro de diálogo de edición (del **Paso de proceso**), vaya a la pestaña **Process** y seleccione la implementación del proceso.
1. Si utiliza argumentos en el código, establezca los **Argumentos de proceso**. Por ejemplo: false.
1. Guarde los cambios, tanto para el paso como para el modelo de flujo de trabajo (esquina superior izquierda del editor de modelos).

Los métodos java, respectivamente, las clases que implementan el método Java ejecutable están registradas como servicios OSGI, lo que permite agregar métodos en cualquier momento durante el tiempo de ejecución.

El siguiente componente OSGI agrega la propiedad `approved` al nodo de contenido de la página cuando la carga útil es una página:

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
>Si el proceso falla tres veces seguidas, se coloca un elemento en la Bandeja de entrada del administrador del flujo de trabajo.

### Uso de ECMAScript {#using-ecmascript}

Los scripts ECMA permiten a los desarrolladores de scripts implementar pasos de proceso. Los scripts se encuentran en el repositorio JCR y se ejecutan desde allí.

En la tabla siguiente se enumeran las variables que están disponibles inmediatamente para procesar secuencias de comandos, lo que proporciona acceso a los objetos de la API de Java del flujo de trabajo.

| Clase Java | Nombre de variable de secuencia de comandos | Descripción |
|---|---|---|
| `com.adobe.granite.workflow.exec.WorkItem` | `graniteWorkItem` | La instancia del paso actual. |
| `com.adobe.granite.workflow.WorkflowSession` | `graniteWorkflowSession` | Sesión de flujo de trabajo de la instancia del paso actual. |
| `String[]` (contiene argumentos de proceso) | `args` | Los argumentos de paso. |
| `com.adobe.granite.workflow.metadata.MetaDataMap` | `metaData` | Los metadatos de la instancia del paso actual. |
| `org.apache.sling.scripting.core.impl.InternalScriptHelper` | `sling` | Proporciona acceso al entorno de tiempo de ejecución de Sling. |

La siguiente secuencia de comandos de ejemplo muestra cómo acceder al nodo JCR que representa la carga útil del flujo de trabajo. La variable `graniteWorkflowSession` está adaptada a una variable de sesión JCR, que se utiliza para obtener el nodo de la ruta de carga útil.

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

El siguiente script comprueba si la carga útil es una imagen ( `.png` archivo), crea una imagen en blanco y negro a partir de ella y la guarda como un nodo del mismo nivel.

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

Para usar la secuencia de comandos:

1. Cree el script (por ejemplo con CRXDE Lite) y guárdelo en el repositorio debajo de `/apps/myapp/workflow/scripts`
1. Para especificar un título que identifique la secuencia de comandos en el cuadro de diálogo de edición **Paso de proceso**, agregue las siguientes propiedades al nodo `jcr:content` de la secuencia de comandos:

   | Nombre | Tipo | Valor |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | Nombre que aparecerá en el cuadro de diálogo de edición. |

1. Edite la instancia **Process Step** y especifique el script que se utilizará.

## Desarrollar los seleccionadores de participantes {#developing-participant-choosers}

Puede desarrollar usuarios que elijan participantes para los componentes de **Paso de participante dinámico**.

Cuando se inicia un componente **Paso de participante dinámico** durante un flujo de trabajo, es necesario determinar el participante al que se puede asignar el elemento de trabajo generado. Para ello, siga estos pasos:

* envía una solicitud a un servicio OSGi
* ejecuta una secuencia de comandos ECMA para seleccionar al participante

Puede desarrollar un servicio o una secuencia de comandos ECMA que seleccione el participante según los requisitos del flujo de trabajo.

>[!NOTE]
>
>Para obtener información sobre la asociación del componente **Paso de participante dinámico** con el servicio o la secuencia de comandos, consulte [Paso de participante dinámico](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step) o [Anulación de la implementación de paso](#persisting-and-accessing-data).

### Desarrollo de un selector de participantes mediante una clase Java {#developing-a-participant-chooser-using-a-java-class}

Para definir un paso del participante como un componente de servicio OSGI (clase Java):

1. El componente OSGI debe implementar la interfaz `ParticipantStepChooser` con su método `getParticipant()`. Consulte el código de ejemplo a continuación.

   Cree el paquete e impleméntelo en el contenedor OSGI.

1. Agregue la propiedad SCR `chooser.label` y establezca el valor como sea necesario. Este será el nombre como se indica en la lista del selector de participantes, con el componente **Paso de participante dinámico**. Consulte el ejemplo:

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

1. En el editor **Modelos**, añada el paso de participante dinámico al flujo de trabajo mediante el componente genérico **Paso de participante dinámico**.
1. En el cuadro de diálogo de edición, seleccione la pestaña **Selector de participante** y seleccione la implementación del selector.
1. Si utiliza argumentos en el código, establezca los **Argumentos de proceso**. Para este ejemplo: `/content/we-retail/de`.
1. Guarde los cambios, tanto para el paso como para el modelo de flujo de trabajo.

### Desarrollo de un selector de participantes mediante un script ECMA {#developing-a-participant-chooser-using-an-ecma-script}

Puede crear una secuencia de comandos ECMA que seleccione el usuario al que se asigna el elemento de trabajo que genera el **paso del participante**. La secuencia de comandos debe incluir una función denominada `getParticipant` que no requiera argumentos y devuelve un valor `String` que contenga el ID de un usuario o grupo.

Las secuencias de comandos se encuentran en el repositorio JCR y se ejecutan desde allí.

En la tabla siguiente se enumeran las variables que proporcionan acceso inmediato a los objetos Java de flujo de trabajo en las secuencias de comandos.

| Clase Java | Nombre de variable de secuencia de comandos |
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

1. Cree el script (por ejemplo con CRXDE Lite) y guárdelo en el repositorio debajo de `/apps/myapp/workflow/scripts`
1. Para especificar un título que identifique la secuencia de comandos en el cuadro de diálogo de edición **Paso de proceso**, agregue las siguientes propiedades al nodo `jcr:content` de la secuencia de comandos:

   | Nombre | Tipo | Valor |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | Nombre que aparecerá en el cuadro de diálogo de edición. |

1. Edite la instancia [Dynamic Participant Step](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step) y especifique el script que se utilizará.

## Gestión de paquetes de flujo de trabajo {#handling-workflow-packages}

[Los ](/help/sites-authoring/workflows-applying.md#specifying-workflow-details-in-the-create-workflow-wizard) paquetes de flujo de trabajo se pueden pasar a un flujo de trabajo para su procesamiento. Los paquetes de flujo de trabajo contienen referencias a recursos como páginas y recursos.

>[!NOTE]
>
>Los siguientes pasos del proceso del flujo de trabajo aceptan paquetes de flujo de trabajo para la activación de páginas por lotes:
>
>* [`com.day.cq.wcm.workflow.process.ActivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/ActivatePageProcess.html)
>* [`com.day.cq.wcm.workflow.process.DeactivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/DeactivatePageProcess.html)

>



Puede desarrollar pasos de flujo de trabajo para obtener los recursos del paquete y procesarlos. Los siguientes miembros del paquete `com.day.cq.workflow.collection` proporcionan acceso a los paquetes de flujo de trabajo:

* `ResourceCollection`: Clase de paquete de flujo de trabajo.
* `ResourceCollectionUtil`: Se utiliza para recuperar objetos ResourceCollection.
* `ResourceCollectionManager`: Crea y recupera colecciones. Una implementación se implementa como un servicio OSGi.

El siguiente ejemplo de clase Java muestra cómo obtener recursos de paquetes:

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

Una forma sencilla de empezar a crear su propio paso personalizado es copiar un paso existente de:

`/libs/cq/workflow/components/model`

### Creación del paso básico {#creating-the-basic-step}

1. Vuelva a crear la ruta en /apps; por ejemplo:

   `/apps/cq/workflow/components/model`

   Las nuevas carpetas son de tipo `nt:folder`:

   ```xml
   - apps
     - cq
       - workflow (nt:folder)
         - components (nt:folder)
           - model (nt:folder)
   ```

   >[!NOTE]
   >
   >Este paso no se aplica al editor clásico del modelo de IU.

1. A continuación, coloque el paso copiado en la carpeta /apps; por ejemplo:

   `/apps/cq/workflow/components/model/myCustomStep`

   Este es el resultado de nuestro paso personalizado de ejemplo:

   ![wf-36](assets/wf-34.png)

   >[!CAUTION]
   >
   >Debido a que en la interfaz de usuario estándar, solo el título y no los detalles se muestran en la tarjeta, `details.jsp` no es necesario, ya que era para el editor de IU clásico.

1. Aplique las siguientes propiedades al nodo :

   `/apps/cq/workflow/components/model/myCustomStep`

   **Propiedades de interés:**

   * `sling:resourceSuperType`

      Debe heredar de un paso existente.

      En este ejemplo heredamos del paso base en `cq/workflow/components/model/step`, pero puede utilizar otros supertipos como `participant`, `process`, etc.

   * `jcr:title`

      Es el título que se muestra cuando el componente aparece en la lista del navegador de pasos (panel izquierdo del editor de modelos de flujo de trabajo).

   * `cq:icon`

      Se utiliza para especificar un [icono de Coral](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) para el paso.

   * `componentGroup`

      Debe ser uno de los siguientes:

      * Flujo de trabajo de colaboración
      * Flujo de trabajo DAM
      * Flujo de trabajo de formularios
      * Proyectos
      * Flujo de trabajo de WCM
      * Flujo de trabajo

   ![wf-35](assets/wf-35.png)

1. Ahora puede abrir un modelo de flujo de trabajo para editarlo. En el navegador de pasos, puede filtrar para ver **My Custom Step**:

   ![wf-34](assets/wf-36.png)

   Al arrastrar **My Custom Step** al modelo se muestra la tarjeta:

   ![wf-37](assets/wf-37.png)

   Si no se ha definido ningún `cq:icon` para el paso, se representa un icono predeterminado con las dos primeras letras del título. Por ejemplo:

   ![wf-38](assets/wf-38.png)

#### Definición del cuadro de diálogo Configuración de pasos {#defining-the-step-configure-dialog}

Después de [Crear el paso básico](#creating-the-basic-step), defina el cuadro de diálogo del paso **Configurar** como se indica a continuación:

1. Configure las propiedades en el nodo `cq:editConfig` de la siguiente manera:

   **Propiedades de interés:**

   * `cq:inherit`

      Cuando se establece en `true`, el componente de paso heredará propiedades del paso especificado en `sling:resourceSuperType`.

   * `cq:disableTargeting`

      Configúrelo según sea necesario.
   ![wf-39](assets/wf-39.png)

1. Configure las propiedades en el nodo `cq:formsParameter` de la siguiente manera:

   **Propiedades de interés:**

   * `jcr:title`

      Establece el título predeterminado en la tarjeta de paso del mapa del modelo y en el campo **Title** del cuadro de diálogo de configuración **My Custom - Step Properties**.

   * También puede definir sus propias propiedades personalizadas.

   ![wf-40](assets/wf-40.png)

1. Configure las propiedades en el nodo `cq:listeners`.

   El nodo `cq:listener` y sus propiedades le permiten establecer controladores de eventos que reaccionan a eventos en el editor de modelos de la IU táctil; como arrastrar un paso a una página de modelo o editar las propiedades de un paso.

   **Propiedades de interés:**

   * `afterMove: REFRESH_PAGE`
   * `afterdelete: CQ.workflow.flow.Step.afterDelete`
   * `afteredit: CQ.workflow.flow.Step.afterEdit`
   * `afterinsert: CQ.workflow.flow.Step.afterInsert`

   Esta configuración es esencial para el correcto funcionamiento del editor. En la mayoría de los casos, esta configuración no debe cambiarse.

   Sin embargo, si establece `cq:inherit` en true (en el nodo `cq:editConfig`, consulte más arriba), podrá heredar esta configuración, sin necesidad de incluirla explícitamente en la definición del paso. Si no hay herencia, es necesario agregar este nodo con las siguientes propiedades y valores.

   En este ejemplo, se ha activado la herencia para que podamos eliminar el nodo `cq:listeners` y el paso seguirá funcionando correctamente.

   ![wf-41](assets/wf-41.png)

1. Ahora puede añadir una instancia del paso a un modelo de flujo de trabajo. Cuando configure **Configure**, verá el cuadro de diálogo:

   ![wf-42](assets/wf-42.png) ![wf-43](assets/wf-43.png)

#### Ejemplo de marcado utilizado en este ejemplo {#sample-markup-used-in-this-example}

El marcado de un paso personalizado se representa en el `.content.xml` del nodo raíz del componente. El ejemplo `.content.xml` utilizado para este ejemplo:

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

El ejemplo `_cq_editConfig.xml` utilizado en este ejemplo:

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

El ejemplo `_cq_dialog/.content.xml` utilizado en este ejemplo:

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
>Observe los nodos comunes y de proceso en la definición del cuadro de diálogo. Estos se heredan del paso de proceso que utilizamos como supertipo para nuestro paso personalizado:
>
>`sling:resourceSuperType : cq/workflow/components/model/process`

>[!NOTE]
>
>Los cuadros de diálogo del editor de modelos de la IU clásica seguirán funcionando con el editor de IU táctil estándar.
>
>Aunque AEM dispone de [herramientas de modernización](/help/sites-developing/modernization-tools.md) si desea actualizar los cuadros de paso de la IU clásica a los cuadros de diálogo de la IU estándar. Después de la conversión aún hay algunas mejoras manuales que se pueden hacer en el cuadro de diálogo para algunos casos.
>
>* En los casos en los que un cuadro de diálogo actualizado esté vacío, puede ver los cuadros de diálogo de `/libs` que tienen una funcionalidad similar a la de ejemplos de cómo proporcionar una solución. Por ejemplo:
   >
   >
* `/libs/cq/workflow/components/model`
>* `/libs/cq/workflow/components/workflow`
>* `/libs/dam/components`
>* `/libs/wcm/workflow/components/autoassign`
>* `/libs/cq/projects`

>
>  
No debe modificar nada en `/libs`, simplemente utilícelo como ejemplos. Si desea aprovechar cualquiera de los pasos existentes, cópielos en `/apps` y modifíquelos allí.
