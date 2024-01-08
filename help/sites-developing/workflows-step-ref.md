---
title: Referencia de pasos de flujo de trabajo
description: Consulte esta referencia de paso para flujos de trabajo en Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 8de78bde-2fcb-4221-873e-59e347ff2d74
source-git-commit: 3bcdbfc17efe1f4c6069fd97fd6a16ec41d0579e
workflow-type: tm+mt
source-wordcount: '3229'
ht-degree: 6%

---

# Referencia de pasos de flujo de trabajo {#workflow-step-reference}

Los modelos de flujo de trabajo constan de una serie de pasos de varios tipos. Según el tipo, estos pasos se pueden configurar y ampliar con parámetros y secuencias de comandos para proporcionar la funcionalidad y el control necesarios.

>[!NOTE]
>
>Esta sección describe los pasos estándar del flujo de trabajo.
>
>Para ver los pasos específicos del módulo, consulte lo siguiente:
>
>* [Referencia de pasos de flujo de trabajo AEM Forms](/help/forms/using/aem-forms-workflow-step-reference.md)
>* [Procesamiento de recursos mediante controladores de medios y flujos de trabajo](/help/assets/media-handlers.md)
>

## Propiedades de la etapa {#step-properties}

Cada componente de paso tiene un **Propiedades del paso** que permite definir y editar las propiedades necesarias.

### Propiedades del paso: pestaña Común {#step-properties-common-tab}

Una combinación de las siguientes propiedades están disponibles para la mayoría de los componentes de paso de flujo de trabajo, en la **Común** pestaña del cuadro de diálogo propiedades:

* **Título**
El título del paso.

* **Descripción**
Una descripción de la etapa.

* **Fase del flujo de trabajo**

  Un selector desplegable para aplicar una variable [Fase](/help/sites-developing/workflows.md#workflow-stages) al paso.

* **Tiempo de espera**

  Período después del cual se agota el tiempo de espera del paso.
Puede seleccionar entre: **Desactivado**, **Inmediato**, **1 h**, **6 h**, **12 h**, **24 h**.

* **Controlador de tiempo de espera**

  Controlador que controla el flujo de trabajo cuando se agota el tiempo de espera del paso. Por ejemplo, `Auto Advancer`

* **Avance del controlador**

  Seleccione esta opción para avanzar automáticamente el flujo de trabajo al siguiente paso después de la ejecución. Si no se selecciona, el script de implementación debe gestionar el avance del flujo de trabajo.

### Propiedades del paso: pestaña Usuario/grupo {#step-properties-user-group-tab}

Las siguientes propiedades están disponibles para muchos componentes de paso de flujo de trabajo, en la **Usuario/grupo** pestaña del cuadro de diálogo propiedades:

* **Notificar al usuario por correo electrónico**

   * Puede notificar a los participantes enviándoles un correo electrónico cuando el flujo de trabajo alcance el paso.
   * Si está habilitado, se envía un correo electrónico al usuario definido por la propiedad **Usuario/grupo** o a cada miembro del grupo si se ha definido uno.

* **Usuario/grupo**

   * Un cuadro de selección desplegable le permite desplazarse hasta un usuario o grupo y seleccionarlos.
   * Si asigna el paso a un usuario específico, solo este puede actuar en el paso.
   * Si asigna el paso a un grupo completo, cuando el flujo de trabajo alcance este paso, todos los usuarios de este grupo tendrán la acción en su **Bandeja de entrada de flujo**.
   * Consulte [Participación en flujos de trabajo](/help/sites-authoring/workflows-participating.md) para obtener más información.

## División Y {#and-split}

El **División Y** crea una división en el flujo de trabajo, tras la cual ambas ramas están activas. Los pasos del flujo de trabajo se agregan a cada rama según sea necesario. Este paso permite introducir varias rutas de procesamiento en el flujo de trabajo. Por ejemplo, puede permitir que ciertos pasos de revisión se produzcan en paralelo, lo que ahorra tiempo.

![wf-26](assets/wf-26.png)

### División AND: configuración {#and-split-configuration}

Para configurar la división:

* Edite el **Propiedades de la división Y**:

   * **Dividir nombre**: asigne un nombre con fines explicativos
   * Seleccione el número de ramas necesarias; 2, 3, 4 o 5.

* Añada los pasos del flujo de trabajo a las ramas según sea necesario.

  ![wf-27](assets/wf-27.png)

## Etapa del contenedor {#container-step}

Un paso de contenedor inicia otro modelo de flujo de trabajo que se ejecuta como flujo de trabajo secundario.

Este contenedor puede permitirle reutilizar los modelos de flujo de trabajo para implementar secuencias comunes de pasos. Por ejemplo, un modelo del flujo de trabajo de traducción se puede utilizar en varios flujos de trabajo de edición.

![wf-28](assets/wf-28.png)

### Paso del contenedor: configuración {#container-step-configuration}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](#step-properties-common-tab)
* **Contenedor**

   * **Flujo de trabajo secundario**: seleccione el flujo de trabajo que desea iniciar.

## Ir a la etapa {#goto-step}

El **Paso Ir a** permite especificar el siguiente paso que se ejecutará en el modelo de flujo de trabajo. Puede especificar una definición de regla, un script externo o un script ECMA como expresión de enrutamiento para evaluar el siguiente paso del modelo de flujo de trabajo.

* Si la condición especificada es verdadera, la variable **Paso Ir a** finaliza y el motor de flujo de trabajo ejecuta el paso especificado.
* Si la condición especificada no es verdadera, la variable **Paso Ir a** finaliza y la lógica de enrutamiento normal determina el siguiente paso que se va a ejecutar.

El **Paso Ir a** permite implementar estructuras de enrutamiento avanzadas en los modelos de flujo de trabajo. Por ejemplo, para implementar un bucle, la variable **Paso Ir a** se puede definir para ejecutar un paso anterior en el flujo de trabajo, con la expresión de enrutamiento evaluando una condición de bucle.

### Paso Ir a: Configuración {#goto-step-configuration}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](#step-properties-common-tab)
* **Proceso**

   * **Paso de destino**: Seleccione el paso que se ejecutará después de evaluar la condición para la expresión de enrutamiento.
   * **Expresión de enrutamiento**: seleccione la definición de regla, el script externo o un script ECMA que determine si se ejecutará el **Paso de destino**.

      * **Definición de regla:** Utilice el [editor de expresiones](/help/forms/using/variable-in-aem-workflows.md#use-expression-editor) para definir la regla.
      * **Script externo:** La ruta del script externo.
      * **Script ECMA**: Script que determina si se ejecuta el **Paso Ir a**.

#### Simulación de un bucle for {#simulating-a-for-loop}

La simulación de un &quot;bucle for&quot; requiere que mantenga un recuento del número de iteraciones de bucle que se han producido:

* El recuento suele representar un índice de elementos en los que se actúa en el flujo de trabajo.
* El recuento se evalúa como criterio de salida del bucle.

Por ejemplo, para implementar un flujo de trabajo que realice una acción en varios nodos JCR, puede utilizar un contador de bucle como índice para los nodos. Para mantener el recuento, almacene un `integer` en la asignación de datos de la instancia de flujo de trabajo. Para incrementar el recuento y comparar el recuento con los criterios de salida, utilice la secuencia de comandos del **Paso Ir a**.

```
function check(){
   var count=0;
   var keyname="loopcount"
   try{
      if (workflowData.getMetaDataMap().containsKey(keyname)){
        log.info("goto script: found loopcount key");
        count= parseInt(workflowData.getMetaDataMap().get(keyname))+1;
      }

     workflowData.getMetaDataMap().put(keyname,count);

     }catch(err) {
         log.info(err.message);
         return false;
    }
   if (parseInt(count) <7){
       return true;
   } else {
      return false;
   }
}
```

### Simulación de un bucle for mediante la definición de regla {#simulateforloop}

También puede simular un bucle for utilizando la definición de regla como expresión de enrutamiento. [Crear un **count** variable](/help/forms/using/variable-in-aem-workflows.md#create-a-variable) del tipo de datos Long. Uso **Expresión** como modo de asignación en la **[Establecer variable](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable)** paso para establecer el valor de **count** variable a **count + 1** en cada ejecución de **Establecer variable** paso.

![Simulación de un bucle for](assets/variable_use_case_count_new.png)

En el **Paso Ir a**, use **Establecer variable** como el **Paso de destino** y **recuento &lt; 5** como la expresión de enrutamiento.

![Condición para simular un bucle for](assets/variable_use_case_count1_new.png)

El **Establecer variable** Este paso se ejecuta repetidamente, incrementando el valor de **count** por 1 en cada ejecución hasta que el valor alcance 5.

## División O {#or-split}

El **División O** crea una división en el flujo de trabajo, tras la cual solo una rama está activa. Este paso le permite introducir rutas de procesamiento condicionales en su flujo de trabajo. Los pasos del flujo de trabajo se agregan a cada rama según sea necesario.

>[!NOTE]
>
>Consulte [Paso OR Split](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/using-variables-in-aem-workflows.html#use-a-variable)

![Bifurcación mediante OR Split](assets/variables_orsplit_new.png)

### OR Split - Configuración {#or-split-configuration}

Para configurar la división:

* Edite el **Propiedades de división O**:

   * **Común**

      * Especifique el nombre de la división.

   * **Ramas (*x)***

      * **Agregar rama:** Añada más ramas al paso.
      * **Seleccionar expresión de enrutamiento**: para evaluar la rama activa, seleccione la expresión de enrutamiento. Los valores posibles incluyen: Definición de regla, Script externo y script ECMA.
      * **Haga clic para agregar una expresión**: Añada una expresión para evaluar la rama activa si selecciona **Definición de regla** como la expresión de enrutamiento.
      * **Ruta de script**: Ruta a un archivo que contiene el script para evaluar la rama activa si selecciona **Script externo** como la expresión de enrutamiento.
      * **Script**: Añada el script en el cuadro para evaluar la rama activa si selecciona **Script ECMA** como la expresión de enrutamiento.
      * **Ruta predeterminada**: Se sigue la rama predeterminada si hay varias ramas. Solo se puede especificar una rama como predeterminada.

  >[!NOTE]
  >
  >    * Se evalúa una rama a la vez en función de la expresión de enrutamiento.
  >    * Las ramas se evalúan de arriba a abajo.
  >    * Se ejecuta el primer script que se evalúa como true.
  >    * Si ninguna rama se evalúa como verdadera, el flujo de trabajo no avanza.
  >
  >

  >[!NOTE]
  >
  >Consulte [Definición de una regla para una división O](/help/sites-developing/workflows-models.md#defineruleecmascript).

* Añada los pasos del flujo de trabajo a las ramas según sea necesario.

## Pasos y selectores de participantes {#participant-steps-and-choosers}

### Etapa de participante {#participant-step}

A **Etapa de participante** permite asignar la propiedad de una acción concreta. El flujo de trabajo se ejecuta únicamente cuando el usuario ha reconocido manualmente el paso. Este flujo de trabajo se utiliza cuando desea que alguien actúe en él. Por ejemplo, un paso de revisión.

Aunque no está directamente relacionado, la autorización de usuario debe tenerse en cuenta al asignar una acción; el usuario debe tener acceso a la página que es la carga útil del flujo de trabajo.

#### Etapa de participante: configuración {#participant-step-configuration}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](#step-properties-common-tab)
* [Usuario/grupo](#step-properties-user-group-tab)

>[!NOTE]
>
>El iniciador del flujo de trabajo siempre recibe una notificación cuando:
>
>* El flujo de trabajo se ha completado (finalizado).
>* El flujo de trabajo se interrumpe (finaliza).
>

>[!NOTE]
>
>Algunas propiedades deben configurarse para habilitar las notificaciones por correo electrónico. También puede personalizar la plantilla de correo electrónico o agregar una plantilla de correo electrónico para un nuevo idioma. AEM Para configurar las notificaciones por correo electrónico en la, consulte [Configuración de notificaciones por correo electrónico](/help/sites-administering/notification.md#configuringemailnotification).

### Etapa de participante de cuadro de diálogo {#dialog-participant-step}

Utilice un **Etapa de participante de diálogo** para recopilar información del usuario que tiene asignado el elemento de trabajo. Este paso es útil para recopilar pequeñas cantidades de datos que se utilizan más adelante en el flujo de trabajo.

Al completar el paso, la variable **Completar elemento de trabajo** El cuadro de diálogo contiene los campos que define en el cuadro de diálogo. Los datos recopilados en los campos se almacenan en los nodos de la carga útil del flujo de trabajo. Los pasos posteriores del flujo de trabajo pueden leer el valor desde el repositorio.

Para configurar el paso, especifique el grupo o usuario al que asignar el elemento de trabajo y la ruta al cuadro de diálogo.

#### Paso de participante del diálogo: configuración {#dialog-participant-step-configuration}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](#step-properties-common-tab)
* [Usuario/grupo](#step-properties-user-group-tab)
* **Diálogo**

   * **Ruta de diálogo**: La ruta al nodo de diálogo del [diálogo que cree](#dialog-participant-step-creating-a-dialog).

#### Paso de participante del diálogo: Creación de un cuadro de diálogo {#dialog-participant-step-creating-a-dialog}

Para crear un cuadro de diálogo, debe crearlo:

* Decida dónde están los datos resultantes [almacenado en la carga útil](#dialog-participant-step-storing-data-in-the-payload).
* [Definir el cuadro de diálogo; incluye la definición de los campos utilizados para recopilar y guardar los datos](#dialog-participant-step-dialog-definition).

#### Paso de participante del cuadro de diálogo: Almacenamiento de datos en la carga útil {#dialog-participant-step-storing-data-in-the-payload}

Puede almacenar datos de widget en la carga útil de flujo de trabajo o en los metadatos del elemento de trabajo. El formato del `name` La propiedad del nodo del widget determina dónde se almacenan los datos.

* **Almacenar datos con la carga útil**

   * Para almacenar datos de widget como una propiedad de la carga útil del flujo de trabajo, utilice el siguiente formato para el valor de la propiedad name del nodo de widget:
     `./jcr:content/nodename`

   * Los datos se almacenan en `nodename` del nodo de carga útil. Si el nodo no contiene esa propiedad, se crea la propiedad.
   * Cuando se almacena con la carga útil, los usos posteriores del cuadro de diálogo con la misma carga útil sobrescriben el valor de la propiedad.

* **Almacenar datos con el elemento de trabajo**

   * Para almacenar los datos del widget como una propiedad de los metadatos del elemento de trabajo, utilice el siguiente formato para el valor de la propiedad name:
     `nodename`

   * Los datos se almacenan en `nodename` propiedad del elemento de trabajo `metadata`. Los datos se conservan si el cuadro de diálogo se utiliza posteriormente con la misma carga útil.

#### Paso de participante del cuadro de diálogo: definición del cuadro de diálogo {#dialog-participant-step-dialog-definition}

1. **Estructura de diálogo**

   Los cuadros de diálogo de los pasos de los participantes del cuadro de diálogo son similares a los cuadros de diálogo que crea para los componentes de creación. Se almacenan en:

   `/apps/myapp/workflow/dialogs`

   Los cuadros de diálogo de la IU táctil estándar tienen la siguiente estructura de nodos:

   ```xml
   newComponent (cq:Component)
     |- cq:dialog (nt:unstructured)
       |- content
         |- layout
           |- items
             |- column
               |- items
                 |- component0
                 |- component1
                 |- ...
   ```

   >[!NOTE]
   >
   >Consulte [Creación y configuración de un cuadro de diálogo](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog).

1. **Propiedad de ruta de diálogo**

   El **Etapa de participante de diálogo** tiene el **Ruta de diálogo** propiedad (junto con las propiedades de una propiedad ) [Etapa de participante](#participant-step)). El valor del **Ruta de diálogo** es la ruta a la propiedad `dialog` del cuadro de diálogo.

   Por ejemplo, el cuadro de diálogo está contenido en un componente llamado `EmailWatch` que se almacena en el nodo:

   `/apps/myapp/workflows/dialogs`

   Para la IU táctil, se utiliza el siguiente valor para **Ruta de diálogo** propiedad:

   `/apps/myapp/workflow/dialogs/EmailWatch/cq:dialog`

   ![wf-30](assets/wf-30.png)

1. **Ejemplo de definición de diálogo**

   El siguiente fragmento de código XML representa un cuadro de diálogo que almacena un `String` valor en `watchEmail` del contenido de carga útil. El nodo de título representa el [TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/textfield/index.html) componente:

   ```xml
   jcr:primaryType="nt:unstructured"
       jcr:title="Watcher Email Address Dialog"
       sling:resourceType="cq/gui/components/authoring/dialog">
       <content jcr:primaryType="nt:unstructured"
           sling:resourceType="granite/ui/components/foundation/container">
           <layout jcr:primaryType="nt:unstructured"
               margin="false"
               sling:resourceType="granite/ui/components/foundation/layouts/fixedcolumns"
           />
           <items jcr:primaryType="nt:unstructured">
               <column jcr:primaryType="nt:unstructured"
                   sling:resourceType="granite/ui/components/foundation/container">
                   <items jcr:primaryType="nt:unstructured">
                       <title jcr:primaryType="nt:unstructured"
                           fieldLabel="Notification Email Address"
                           name="./jcr:content/watchEmails"
                           sling:resourceType="granite/ui/components/foundation/form/textfield"
                       />
                   </items>
               </column>
           </items>
       </content>
   </cq:dialog>
   ```

   En la IU táctil, este ejemplo genera un cuadro de diálogo como el siguiente:

   ![chlimage_1-70](assets/chlimage_1-70.png)

### Etapa de participante dinámica {#dynamic-participant-step}

El **Etapa de participante dinámica** el componente es similar a **[Etapa de participante](#participant-step)** con la diferencia de que el participante se selecciona automáticamente en tiempo de ejecución.

Para configurar el paso, seleccione un **Selector de participantes** que identifica al participante al que asignar el elemento de trabajo, junto con un cuadro de diálogo.

#### Etapa de participante dinámica: configuración {#dynamic-participant-step-configuration}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](#step-properties-common-tab)
* **Selector de participantes**

   * **Selector de participantes**: el nombre del [selector de participantes que ha creado](#developingtheparticipantchooser).
   * **Argumentos**: cualquier argumento requerido.
   * **Correo electrónico**: Si se debe enviar una notificación por correo electrónico al usuario.

* **Diálogo**

   * **Ruta de diálogo**: La ruta al nodo de diálogo del [diálogo que cree (como con el **Etapa de participante de diálogo**)](#dialog-participant-step-creating-a-dialog).

#### Etapa de participante dinámica: desarrollo del selector de participantes {#dynamic-participant-step-developing-the-participant-chooser}

Puede crear el selector de participantes. Por lo tanto, puede utilizar cualquier lógica o criterio de selección. Por ejemplo, el selector de participantes puede seleccionar el usuario (dentro de un grupo) que tenga menos elementos de trabajo. Puede crear cualquier número de selectores de participantes para utilizarlos con diferentes instancias del **Etapa de participante dinámica** en los modelos de flujo de trabajo.

Cree un servicio OSGi o un ECMAScript que seleccione un usuario al que asignar el elemento de trabajo.

* **ECMAscript**

  Los scripts deben incluir una función denominada getParticipant que devuelva un ID de usuario como `String` valor. Almacene sus scripts personalizados en, por ejemplo, la `/apps/myapp/workflow/scripts` o una subcarpeta.

  AEM Se incluye un script de ejemplo en una instancia de estándar:

  `/libs/workflow/scripts/initiator-participant-chooser.ecma`

  >[!CAUTION]
  >
  >No cambie nada en el `/libs` ruta.
  >
  >
  >El motivo es que el contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y puede sobrescribirse al aplicar una revisión o un paquete de funciones).

  Esta secuencia de comandos selecciona el iniciador del flujo de trabajo como participante:

  ```
  function getParticipant() {
      return workItem.getWorkflow().getInitiator();
  }
  ```

  >[!NOTE]
  >
  >El **Selector de participantes del iniciador de flujo de trabajo** El componente amplía el **Etapa de participante dinámica** y utiliza este script como implementación de la etapa.

* **Servicio OSGi**

  Los servicios deben implementar el [com.day.cq.workflow.exec.ParticipantStepChooser](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/workflow/exec/ParticipantStepChooser.html) interfaz. La interfaz define los siguientes miembros:

   * `SERVICE_PROPERTY_LABEL` field: utilice este campo para especificar el nombre del selector de participantes. El nombre aparece en una lista de selectores de participantes disponibles en la **Etapa de participante dinámica** propiedades.

   * `getParticipant` método: devuelve el ID principal resuelto dinámicamente como un `String` valor.

  >[!CAUTION]
  >
  >El `getParticipant` devuelve el ID principal resuelto dinámicamente. Este ID puede ser un ID de grupo o un ID de usuario.
  >
  >
  >Sin embargo, un ID de grupo solo se puede utilizar para una **Etapa de participante**, cuando se devuelve una lista de participantes. Para un **Etapa de participante dinámica**, se devuelve una lista vacía y no se puede utilizar para la delegación.

  Para que la implementación esté disponible para **Etapa de participante dinámica** AEM componentes, agregue la clase Java™ a un paquete OSGi que exporte el servicio e implemente el paquete en el servidor de.

  >[!NOTE]
  >
  >**Selector aleatorio de participantes** es un servicio de ejemplo que selecciona un usuario aleatorio ( `com.day.cq.workflow.impl.process.RandomParticipantChooser`). El **Selección aleatoria de participantes** La muestra de componente de paso r amplía la **Etapa de participante dinámica** y utiliza este servicio como implementación de la etapa.

#### Etapa de participante dinámica: ejemplo de servicio de selector de participantes {#dynamic-participant-step-example-participant-chooser-service}

La siguiente clase Java™ implementa el `ParticipantStepChooser` interfaz. La clase devuelve el nombre del participante que inició el flujo de trabajo. El código utiliza la misma lógica que el script de ejemplo (`initiator-participant-chooser.ecma`) utiliza.

El `@Property` La anotación define el valor de `SERVICE_PROPERTY_LABEL` field a `Workflow Initiator Participant Chooser`.

```java
package com.adobe.example;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.osgi.framework.Constants;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.ParticipantStepChooser;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.metadata.MetaDataMap;

@Component
@Service
@Properties({
        @Property(name = Constants.SERVICE_DESCRIPTION, value = "An example implementation of a dynamic participant chooser."),
        @Property(name = ParticipantStepChooser.SERVICE_PROPERTY_LABEL, value = "Workflow Initiator Participant Chooser (service)") })
public class InitiatorParticipantChooser implements ParticipantStepChooser {

 private Logger logger = LoggerFactory.getLogger(this.getClass());

 public String getParticipant(WorkItem arg0, WorkflowSession arg1,
   MetaDataMap arg2) throws WorkflowException {

  String initiator = arg0.getWorkflow().getInitiator();
  logger.info("Assigning Dynamic Participant Step work item to {}",initiator);

  return initiator;
 }
}
```

En el **Etapa de participante dinámica** diálogo de propiedades, el **Selector de participantes** La lista incluye el elemento `Workflow Initiator Participant Chooser (script)`, que representa este servicio.

Cuando se inicia el modelo de flujo de trabajo, el registro indica el ID del usuario que inició el flujo de trabajo y a quién se asigna el elemento de trabajo. En este ejemplo, la variable `admin` El usuario inició el flujo de trabajo.

`13.09.2015 15:48:53.037 *INFO* [10.176.129.223 [1347565733037] POST /etc/workflow/instances HTTP/1.1] com.adobe.example.InitiatorParticipantChooser Assigning Dynamic Participant Step work item to admin`

### Etapa de participante de formulario {#form-participant-step}

El **Etapa de participante de formulario** presenta un formulario cuando se abre el elemento de trabajo. Cuando el usuario rellena y envía el formulario, los datos de campo se almacenan en los nodos de la carga útil del flujo de trabajo.

Para configurar el paso, especifique el grupo o usuario al que asignar el elemento de trabajo y la ruta al formulario.

>[!CAUTION]
>
>Esta sección trata sobre [Sección Forms de componentes de base para la creación de páginas](/help/sites-authoring/default-components-foundation.md#form).

#### Paso de participante de formulario: configuración {#form-participant-step-configuration}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](#step-properties-common-tab)
* [Usuario/grupo](#step-properties-user-group-tab)
* **Form**

   * **Ruta de formulario**: La ruta al [formulario que cree](#form-participant-step-creating-the-form).

#### Paso de participante del formulario: creación del formulario {#form-participant-step-creating-the-form}

Crear un formulario para utilizarlo con una **Etapa de participante de formulario** como de costumbre. Sin embargo, los formularios de un paso de participante de formulario deben tener las siguientes configuraciones:

* El **Inicio de formulario** el componente debe tener el **Tipo de acción** propiedad establecida en `Edit Workflow Controlled Resource(s)`.
* El **Inicio de formulario** el componente debe tener un valor para `Form Identifier` propiedad.
* Los componentes del formulario deben tener el **Nombre de elemento** propiedad se establece en la ruta del nodo donde se almacenan los datos del campo. La ruta debe localizar un nodo en el contenido de carga útil del flujo de trabajo. El valor utiliza el siguiente formato:

  `./jcr:content/path_to_node`

* El formulario debe incluir un **Botón Enviar de flujo de trabajo** componente. No se configura ninguna propiedad del componente.

Los requisitos del flujo de trabajo determinan dónde se deben almacenar los datos de campo. Por ejemplo, los datos de campo se pueden utilizar para configurar las propiedades del contenido de la página. El siguiente valor de un **Nombre de elemento** La propiedad almacena datos de campo como el valor de `redirectTarget` propiedad del `jcr:content` nodo:

`./jcr:content/redirectTarget`

En el ejemplo siguiente, los datos de campo se utilizan como contenido de un **Texto** en la página de carga útil:

`./jcr:content/par/text_3/text`

El primer ejemplo se puede utilizar para cualquier página que tenga el valor `cq:Page` procesamientos de componentes. El segundo ejemplo solo se puede utilizar cuando la página de carga útil incluye un **Texto** componente que tiene un ID de `text_3`.

El formulario se puede encontrar en cualquier lugar del repositorio, pero los usuarios del flujo de trabajo deben tener autorización para leer el formulario.

### Selector aleatorio de participantes {#random-participant-chooser}

El **Selector aleatorio de participantes** Este paso es un selector participante que asigna el elemento de trabajo generado a un usuario que se selecciona aleatoriamente de una lista.

![wf-31](assets/wf-31.png)

#### Selector aleatorio de participantes - Configuración {#random-participant-chooser-configuration}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](#step-properties-common-tab)
* **Argumentos**

   * **Participantes**: especifica la lista de usuarios disponibles para la selección. Para añadir un usuario a la lista, haga clic en **Agregar elemento** y escriba la ruta de acceso principal del nodo de usuario o el ID de usuario. El orden de los usuarios no afecta a la probabilidad de que se les asigne un elemento de trabajo.

### Selector de participantes del lanzador de flujo de trabajo {#workflow-initiator-participant-chooser}

El **Selector de participantes del iniciador de flujo de trabajo** step es un selector de participantes que asigna el elemento de trabajo generado al usuario que inició el flujo de trabajo. No hay propiedades que configurar que no sean **Común** propiedades.

#### Selector de participantes del iniciador de flujo de trabajo - Configuración {#workflow-initiator-participant-chooser-configuration}

Para configurar el paso, edite utilizando las siguientes pestañas:

* [Común](#step-properties-common-tab)

## Etapa del proceso {#process-step}

A **Etapa del proceso** ejecuta un ECMAScript o llama a un servicio OSGi para realizar un procesamiento automático.

![wf-32](assets/wf-32.png)

### Etapa del proceso: configuración {#process-step-configuration}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](#step-properties-common-tab)
* **Proceso**

   * **Proceso**: Implementación del proceso que se va a ejecutar. Utilice el menú desplegable para seleccionar el servicio ECMAScript o OSGi. Para obtener información acerca de:

      * Los servicios estándar ECMAScripts y OSGi, consulte [Procesos integrados para pasos del proceso](/help/sites-developing/workflows-process-ref.md).
      * Creación de ECMAScripts para un paso de proceso, consulte [Implementación de un paso del proceso con un ECMAScript](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript).
      * Creación de servicios OSGi para un paso Proceso, consulte [Implementar un paso del proceso con una clase Java™](/help/sites-developing/workflows-customizing-extending.md#implementing-a-process-step-with-a-java-class).

   * **Avance del controlador**: seleccione esta opción para avanzar automáticamente el flujo de trabajo al siguiente paso después de la ejecución. Si no se selecciona, el script de implementación debe gestionar el avance del flujo de trabajo.
   * **Argumentos**: argumentos que se van a pasar al proceso.

## Establecer variable {#set-variable}

El paso Establecer variable permite establecer el valor de una variable y definir el orden en que se configuran los valores. La variable se configura en el orden en que se enumeran las asignaciones de variables en el paso Establecer variable.

![Agregar asignación para establecer una variable](assets/set_variable_addmappingnew.png)

### Establecer variable - Configuración {#setvariable}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](/help/sites-developing/workflows-step-ref.md#step-properties-common-tab)
* **Asignación**

   * **Seleccionar variable:** Utilice esta opción para seleccionar una variable y establecer su valor.
   * **Seleccione el modo de asignación:**  Para establecer el valor de la variable, seleccione un modo de asignación. Según el tipo de datos de la variable, puede utilizar las siguientes opciones para establecer su valor:

      * **Literal:** utilice la opción cuando conozca el valor exacto que desea especificar.
      * **Expresión:** utilice la opción cuando el valor que se va a utilizar se calcule en función de una expresión. La expresión se crea en el editor de expresiones proporcionado.
      * **Notación de puntos JSON:** Utilice la opción para recuperar un valor de una variable de tipo JSON o FDM.
      * **XPATH:** Utilice la opción para recuperar un valor de una variable de tipo XML.
      * **En relación con la carga útil:** Utilice la opción cuando el valor que se va a guardar en la variable esté disponible en una ruta relativa a la carga útil.
      * **Ruta absoluta:** Utilice la opción cuando el valor que se va a guardar en la variable esté disponible en una ruta absoluta.

   * **Especifique el valor:** Para asignar a la variable, especifique un valor. El valor que especifique en este campo depende del modo de asignación.
   * **Agregar asignación:** Utilice esta opción para agregar más asignaciones y establecer un valor para la variable.
