---
title: Referencia de pasos de flujo de trabajo
seo-title: Workflow Step Reference
description: Referencia de pasos de flujo de trabajo
seo-description: null
uuid: 88bf6997-73a1-4639-82aa-5dff08d3ef86
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e3afffd0-d90c-4bd0-b814-f7aeac6ceb6d
docset: aem65
exl-id: 8de78bde-2fcb-4221-873e-59e347ff2d74
source-git-commit: 768576e300b655962adc3e1db20fc5ec06a5ba6c
workflow-type: tm+mt
source-wordcount: '3246'
ht-degree: 7%

---

# Referencia de pasos de flujo de trabajo {#workflow-step-reference}

Los modelos de flujo de trabajo constan de una serie de pasos de varios tipos. Según el tipo, estos pasos se pueden configurar y ampliar con parámetros y secuencias de comandos para proporcionar la funcionalidad y el control que necesite.

>[!NOTE]
>
>Esta sección cubre los pasos estándar del flujo de trabajo.
>
>Para ver los pasos específicos del módulo, consulte lo siguiente:
>
>* [Referencia de pasos del flujo de trabajo de AEM Forms](/help/forms/using/aem-forms-workflow-step-reference.md)
>* [Processing Assets Using Media Handlers and Workflows](/help/assets/media-handlers.md)
>


## Propiedades de la etapa {#step-properties}

Cada componente de paso tiene un **Propiedades de los pasos** que permite definir y editar las propiedades requeridas.

### Propiedades de los pasos: ficha Común {#step-properties-common-tab}

Hay disponible una combinación de las siguientes propiedades para la mayoría de los componentes de paso del flujo de trabajo, en la variable **Frecuentes** del cuadro de diálogo de propiedades:

* **Título**
Título del paso.

* **Descripción**
Descripción del paso.

* **Fase del flujo de trabajo**

   Un selector desplegable para aplicar un [Prueba](/help/sites-developing/workflows.md#workflow-stages) al paso.

* **Tiempo de espera**

   El periodo después del cual se agota el tiempo de espera del paso.
Puede seleccionar entre: **Off**, **Inmediato**, **1h**, **6h**, **12h**, **24 h**.

* **Controlador de tiempo de espera**

   El controlador que controla el flujo de trabajo cuando se agota el tiempo de espera del paso. Por ejemplo, `Auto Advancer`. 

* **Avance de controlador**

   Seleccione esta opción para avanzar automáticamente el flujo de trabajo al paso siguiente después de la ejecución. Si no se selecciona, la secuencia de comandos de implementación debe gestionar el progreso del flujo de trabajo.

### Propiedades de los pasos: ficha Usuario/Grupo {#step-properties-user-group-tab}

Las siguientes propiedades están disponibles para muchos componentes de paso del flujo de trabajo, en la variable **Usuario/Grupo** del cuadro de diálogo de propiedades:

* **Notificar al usuario a través del correo electrónico**

   * Puede notificar a los participantes enviándoles un correo electrónico cuando el flujo de trabajo llega al paso .
   * Si está habilitado, se envía un correo electrónico al usuario definido por la propiedad **Usuario/Grupo**, o a cada miembro del grupo si se define un grupo.

* **Usuario/grupo**

   * Un cuadro de selección desplegable le permite desplazarse a un usuario o grupo y seleccionarlo.
   * Si asigna el paso a un usuario específico, solo este usuario puede actuar en el paso.
   * Si asigna el paso a un grupo completo, cuando el flujo de trabajo llegue a este paso, todos los usuarios de este grupo tendrán la acción en su **Bandeja de entrada del flujo de trabajo**.
   * Consulte [Participación en flujos de trabajo](/help/sites-authoring/workflows-participating.md) para obtener más información.

## División Y {#and-split}

La variable **División AND** crea una división en el flujo de trabajo, tras la cual ambas ramas están activas. Los pasos del flujo de trabajo se agregan a cada rama según sea necesario. Este paso permite introducir varias rutas de procesamiento en el flujo de trabajo. Por ejemplo, puede permitir que ciertos pasos de revisión se produzcan en paralelo, lo que ahorra tiempo.

![wf-26](assets/wf-26.png)

### División AND: Configuración {#and-split-configuration}

Para configurar la división:

* Edite el **Propiedades de división AND**:

   * **Nombre de división**: asignar un nombre con fines explicativos
   * Seleccione el número de ramas necesarias; 2, 3, 4 o 5.

* Añada los pasos del flujo de trabajo a las ramas según sea necesario.

   ![wf-27](assets/wf-27.png)

## Etapa del contenedor {#container-step}

Un paso de contenedor inicia otro modelo de flujo de trabajo que se ejecuta como flujo de trabajo secundario.

Este contenedor puede permitirle reutilizar modelos de flujo de trabajo para implementar secuencias comunes de pasos. Por ejemplo, un modelo de flujo de trabajo de traducción se puede utilizar en varios flujos de trabajo de edición.

![wf-28](assets/wf-28.png)

### Paso de contenedor: configuración {#container-step-configuration}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](#step-properties-common-tab)
* **Contenedor**

   * **Subflujo de trabajo**: Seleccione el flujo de trabajo que desea iniciar.

## Ir a la etapa {#goto-step}

La variable **Ir al paso** permite especificar el paso siguiente que se ejecutará en el modelo de flujo de trabajo. Puede especificar una definición de regla, un script externo o un script ECMA como expresión de enrutamiento para evaluar el siguiente paso del modelo de flujo de trabajo.

* Si la condición especificada tiene el valor &quot;True&quot;, la variable **Ir al paso** finaliza y el motor de flujo de trabajo ejecuta el paso especificado.
* Si la condición especificada no tiene el valor &quot;True&quot;, la variable **Ir al paso** completa y la lógica de enrutamiento normal determina el siguiente paso que se va a ejecutar.

La variable **Ir al paso** permite implementar estructuras de enrutamiento avanzadas en los modelos de flujo de trabajo. Por ejemplo, para implementar un bucle, la variable **Ir al paso** se puede definir para ejecutar un paso anterior en el flujo de trabajo, con la expresión de enrutamiento evaluando una condición de bucle.

### Ir al paso: configuración {#goto-step-configuration}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](#step-properties-common-tab)
* **Proceso**

   * **Paso de Target**: Seleccione el paso que se ejecutará después de evaluar la condición para la expresión de enrutamiento.
   * **Expresión de enrutamiento**: Seleccione Definición de regla, Script externo o una secuencia de comandos ECMA que determine si se ejecutará la variable **Paso de Target**.

      * **Definición de regla:** Utilice la variable [editor de expresiones](/help/forms/using/variable-in-aem-workflows.md#use-expression-editor) para definir la regla.
      * **Script externo:** Ruta de acceso de la secuencia de comandos externa.
      * **Script ECMA**: La secuencia de comandos que determina si se ejecutará la variable **Ir al paso**.

#### Simulación de un bucle for {#simulating-a-for-loop}

Para simular un bucle for es necesario mantener un recuento del número de iteraciones de bucle que se han producido:

* El recuento representa normalmente un índice de elementos en los que se actúa en el flujo de trabajo.
* El recuento se evalúa como criterios de salida del bucle.

Por ejemplo, para implementar un flujo de trabajo que realice una acción en varios nodos JCR, puede utilizar un contador de bucle como índice para los nodos. Para mantener el recuento, almacene un `integer` en el mapa de datos de la instancia de flujo de trabajo. Para incrementar el recuento y comparar el recuento con los criterios de salida, utilice la secuencia de comandos del **Ir al paso**.

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

También puede simular un bucle for utilizando la Definición de regla como expresión de enrutamiento. [Cree un **count** variable](/help/forms/using/variable-in-aem-workflows.md#create-a-variable) del tipo de datos Long. Uso **Expresión** como el modo de asignación en la variable **[Establecer variable](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable)** para definir el valor de la variable **count** a **count + 1** en cada ejecución del **Establecer variable** paso a paso.

![Simulación de un bucle for](assets/variable_use_case_count_new.png)

En el **Ir al paso**, use **Establecer variable** como el **Paso de Target** y **recuento &lt; 5** como la expresión de enrutamiento.

![Condición para simular un bucle for](assets/variable_use_case_count1_new.png)

La variable **Establecer variable** step se ejecuta repetidamente, incrementando el valor de **count** por 1 en cada ejecución hasta que el valor alcance 5.

## División O {#or-split}

La variable **División OR** crea una división en el flujo de trabajo, tras la cual solo una rama está activa. Este paso le permite introducir rutas de procesamiento condicionales en su flujo de trabajo. Los pasos del flujo de trabajo se agregan a cada rama según sea necesario.

>[!NOTE]
>
>Consulte [Paso dividido OR](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/using-variables-in-aem-workflows.html?lang=en#use-a-variable)

![Ramificación mediante OR Split](assets/variables_orsplit_new.png)

### División OR: configuración {#or-split-configuration}

Para configurar la división:

* Edite el **Propiedades divididas OR**:

   * **Común**

      * Especifique el nombre dividido.
   * **Ramas (*x)***

      * **Agregar rama:** Agregue más ramas al paso.
      * **Seleccionar expresión de enrutamiento**: Para evaluar la rama activa, seleccione la expresión de enrutamiento. Los valores posibles incluyen: Definición de regla, Script externo y secuencia de comandos ECMA.
      * **Haga clic para agregar expresión**: Agregue expresión para evaluar la rama activa si selecciona **Definición de regla** como la expresión de enrutamiento.
      * **Ruta de acceso del script**: Ruta a un archivo que contiene la secuencia de comandos para evaluar la rama activa si selecciona **Secuencia de comandos externa** como la expresión de enrutamiento.
      * **Secuencia de comandos**: Agregue la secuencia de comandos en el cuadro para evaluar la rama activa si selecciona **Script ECMA** como la expresión de enrutamiento.
      * **Ruta predeterminada**: La rama predeterminada se sigue si hay varias ramas. Solo se puede especificar una rama como la predeterminada.

   >[!NOTE]
   >
   >    * Una rama se evalúa a la vez según la expresión de enrutamiento.
   >    * Las ramas se evalúan de arriba a abajo.
   >    * Se ejecuta la primera secuencia de comandos que evalúa como verdadera.
   >    * Si ninguna rama se evalúa como verdadera, el flujo de trabajo no avanza.


   >[!NOTE]
   >
   >Consulte [Definición de una regla para una división OR](/help/sites-developing/workflows-models.md#defineruleecmascript).

* Añada los pasos del flujo de trabajo a las ramas según sea necesario.

## Pasos y opciones del participante {#participant-steps-and-choosers}

### Etapa de participante {#participant-step}

A **Etapa de participante** permite asignar la propiedad a una acción determinada. El flujo de trabajo solo se ejecuta cuando el usuario ha reconocido manualmente el paso. Este flujo de trabajo se utiliza cuando desea que alguien actúe en el flujo de trabajo. Por ejemplo, un paso de revisión.

Aunque no está directamente relacionada, se debe tener en cuenta la autorización del usuario al asignar una acción; el usuario debe tener acceso a la página que es la carga útil del flujo de trabajo.

#### Etapa de participante: configuración {#participant-step-configuration}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](#step-properties-common-tab)
* [Usuario/grupo](#step-properties-user-group-tab)

>[!NOTE]
>
>El iniciador del flujo de trabajo siempre recibe una notificación cuando:
>
>* El flujo de trabajo se ha completado (finalizado).
>* El flujo de trabajo se interrumpe (termina).
>


>[!NOTE]
>
>Algunas propiedades deben configurarse para habilitar las notificaciones por correo electrónico. También puede personalizar la plantilla de correo electrónico o añadir una plantilla de correo electrónico para un nuevo idioma. Para configurar las notificaciones de correo electrónico en AEM, consulte [Configuración de notificaciones por correo electrónico](/help/sites-administering/notification.md#configuringemailnotification).

### Etapa de participante de cuadro de diálogo {#dialog-participant-step}

Utilice un **Etapa de participante del cuadro de diálogo** para recopilar información del usuario al que se asigna el elemento de trabajo. Este paso es útil para recopilar pequeñas cantidades de datos que se utilizan más adelante en el flujo de trabajo.

Al completar el paso, la variable **Completar elemento de trabajo** contiene los campos definidos en el cuadro de diálogo. Los datos recopilados en los campos se almacenan en los nodos de la carga útil del flujo de trabajo. Los pasos subsiguientes del flujo de trabajo pueden leer el valor del repositorio.

Para configurar el paso, especifique el grupo o usuario al que desea asignar el elemento de trabajo y la ruta al cuadro de diálogo.

#### Etapa de participante del cuadro de diálogo: configuración {#dialog-participant-step-configuration}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](#step-properties-common-tab)
* [Usuario/grupo](#step-properties-user-group-tab)
* **Cuadro de diálogo**

   * **Ruta de diálogo**: La ruta al nodo de diálogo del [cuadro de diálogo que cree](#dialog-participant-step-creating-a-dialog).

#### Etapa de participante del cuadro de diálogo: creación de un cuadro de diálogo {#dialog-participant-step-creating-a-dialog}

Para crear un cuadro de diálogo, debe crear el cuadro de diálogo:

* Decida dónde están los datos resultantes [almacenado en la carga útil](#dialog-participant-step-storing-data-in-the-payload).
* [Definir el cuadro de diálogo; incluye la definición de los campos que se utilizan para recopilar y guardar los datos](#dialog-participant-step-dialog-definition).

#### Paso de participante del cuadro de diálogo: almacenamiento de datos en la carga útil {#dialog-participant-step-storing-data-in-the-payload}

Puede almacenar datos de widget en la carga útil del flujo de trabajo o en los metadatos del elemento de trabajo. El formato de la variable `name` propiedad del nodo widget determina dónde se almacenan los datos.

* **Almacenar datos con la carga útil**

   * Para almacenar datos de widget como propiedad de la carga útil del flujo de trabajo, utilice el siguiente formato para el valor de la propiedad name del nodo de widget:
      `./jcr:content/nodename`

   * Los datos se almacenan en la variable `nodename` propiedad del nodo de carga útil. Si el nodo no contiene esa propiedad, se crea la propiedad .
   * Cuando se almacena con la carga útil, los usos subsiguientes del cuadro de diálogo con la misma carga útil sobrescriben el valor de la propiedad.

* **Almacenar datos con el elemento de trabajo**

   * Para almacenar datos de widget como propiedad de los metadatos del elemento de trabajo, utilice el siguiente formato para el valor de la propiedad name :
      `nodename`

   * Los datos se almacenan en la variable `nodename` propiedad del elemento de trabajo `metadata`. Los datos se conservan si el cuadro de diálogo se utiliza posteriormente con la misma carga útil.

#### Etapa del participante del cuadro de diálogo: definición del cuadro de diálogo {#dialog-participant-step-dialog-definition}

1. **Estructura del cuadro de diálogo**

   Los cuadros de diálogo Pasos de los participantes son similares a los cuadros de diálogo que crea para crear componentes. Se almacenan en:

   `/apps/myapp/workflow/dialogs`

   Los cuadros de diálogo para la IU táctil estándar tienen la siguiente estructura de nodos:

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

1. **Propiedad Dialog Path**

   La variable **Etapa de participante del cuadro de diálogo** tiene la variable **Ruta de diálogo** (junto con las propiedades de un [Etapa de participante](#participant-step)). El valor de la variable **Ruta de diálogo** es la ruta a la `dialog` del cuadro de diálogo.

   Por ejemplo, el cuadro de diálogo está contenido en un componente denominado `EmailWatch` que se almacena en el nodo :

   `/apps/myapp/workflows/dialogs`

   Para la IU táctil, se utiliza el siguiente valor para la variable **Ruta de diálogo** propiedad:

   `/apps/myapp/workflow/dialogs/EmailWatch/cq:dialog`

   ![wf-30](assets/wf-30.png)

1. **Ejemplo de definición de cuadro de diálogo**

   El siguiente fragmento de código XML representa un cuadro de diálogo que almacena un `String` en la variable `watchEmail` del contenido de carga útil. El nodo de título representa la variable [CampoTexto](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/textfield/index.html) componente:

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

La variable **Etapa de participante dinámica** es similar a **[Etapa de participante](#participant-step)** con la diferencia de que el participante se selecciona automáticamente en tiempo de ejecución.

Para configurar el paso, seleccione una **Selector de participante** que identifica al participante al que asignar el elemento de trabajo, junto con un cuadro de diálogo.

#### Etapa de participante dinámica: configuración {#dynamic-participant-step-configuration}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](#step-properties-common-tab)
* **Selector de participantes**

   * **Selector de participante**: El nombre del [selector de participantes que cree](#developingtheparticipantchooser).
   * **Argumentos**: Cualquier argumento necesario.
   * **Correo electrónico**: Si se debe enviar una notificación por correo electrónico al usuario.

* **Cuadro de diálogo**

   * **Ruta de diálogo**: La ruta al nodo de diálogo del [diálogo que cree (como con el **Etapa de participante del cuadro de diálogo**)](#dialog-participant-step-creating-a-dialog).

#### Etapa de participante dinámica: desarrollo del selector de participantes {#dynamic-participant-step-developing-the-participant-chooser}

Usted crea el selector de participantes. Por lo tanto, puede utilizar cualquier lógica o criterio de selección. Por ejemplo, el selector de participantes puede seleccionar el usuario (dentro de un grupo) que tenga la menor cantidad de elementos de trabajo. Puede crear cualquier número de usuarios que desee utilizar con diferentes instancias de la variable **Etapa de participante dinámica** en los modelos de flujo de trabajo.

Cree un servicio OSGi o un ECMAScript que seleccione un usuario al que asignar el elemento de trabajo.

* **ECMAscript**

   Las secuencias de comandos deben incluir una función denominada getParticipant que devuelva un ID de usuario como `String` valor. Almacene los scripts personalizados en, por ejemplo, la variable `/apps/myapp/workflow/scripts` o una subcarpeta.

   Se incluye un script de ejemplo en una instancia de AEM estándar:

   `/libs/workflow/scripts/initiator-participant-chooser.ecma`

   >[!CAUTION]
   >
   >No cambie nada en la variable `/libs` ruta.
   >
   >
   >El motivo es que el contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y se puede sobrescribir al aplicar una corrección o un paquete de funciones).

   Esta secuencia de comandos selecciona el iniciador del flujo de trabajo como participante:

   ```
   function getParticipant() {
       return workItem.getWorkflow().getInitiator();
   }
   ```

   >[!NOTE]
   >
   >La variable **Selector de participante del iniciador de flujo de trabajo** amplía el **Etapa de participante dinámica** y utiliza esta secuencia de comandos como implementación de paso.

* **Servicio OSGi**

   Los servicios deben implementar la variable [com.day.cq.workflow.exec.ParticipantStepChooser](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/workflow/exec/ParticipantStepChooser.html) interfaz. La interfaz define los siguientes miembros:

   * `SERVICE_PROPERTY_LABEL` campo: Utilice este campo para especificar el nombre del selector de participantes. El nombre aparece en una lista de los usuarios participantes disponibles en la **Etapa de participante dinámica** propiedades.

   * `getParticipant` método: Devuelve el identificador principal resuelto dinámicamente como un `String` valor.
   >[!CAUTION]
   >
   >La variable `getParticipant` devuelve el identificador principal resuelto dinámicamente. Este id puede ser un id de grupo o un id de usuario.
   >
   >
   >Sin embargo, un id de grupo solo se puede usar para un **Etapa de participante**, cuando se devuelve una lista de participantes. Para un **Etapa de participante dinámica**, se devuelve una lista vacía que no se puede usar para la delegación.

   Para que la implementación esté disponible para **Etapa de participante dinámica** , añada su clase Java™ a un paquete OSGi que exporte el servicio e implemente el paquete en el servidor AEM.

   >[!NOTE]
   >
   >**Selector de participante aleatorio** es un servicio de ejemplo que selecciona un usuario aleatorio ( `com.day.cq.workflow.impl.process.RandomParticipantChooser`). La variable **Elección de participante aleatoria** o muestra de componente de paso amplía el **Etapa de participante dinámica** y utiliza este servicio como implementación de paso.

#### Etapa de participante dinámica: servicio de selección de participantes de ejemplo {#dynamic-participant-step-example-participant-chooser-service}

La siguiente clase Java™ implementa el `ParticipantStepChooser` interfaz. La clase devuelve el nombre del participante que inició el flujo de trabajo. El código utiliza la misma lógica que la secuencia de comandos de ejemplo (`initiator-participant-chooser.ecma`).

La variable `@Property` la anotación define el valor de la variable `SERVICE_PROPERTY_LABEL` campo a `Workflow Initiator Participant Chooser`.

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

En el **Etapa de participante dinámica** cuadro de diálogo de propiedades, **Selector de participante** La lista incluye el elemento `Workflow Initiator Participant Chooser (script)`, que representa este servicio.

Cuando se inicia el modelo de flujo de trabajo, el registro indica el ID del usuario que inició el flujo de trabajo y al que se asigna el elemento de trabajo. En este ejemplo, la variable `admin` el usuario inició el flujo de trabajo.

`13.09.2015 15:48:53.037 *INFO* [10.176.129.223 [1347565733037] POST /etc/workflow/instances HTTP/1.1] com.adobe.example.InitiatorParticipantChooser Assigning Dynamic Participant Step work item to admin`

### Etapa de participante de formulario {#form-participant-step}

La variable **Etapa de participante del formulario** presenta un formulario cuando se abre el elemento de trabajo. Cuando el usuario rellena y envía el formulario, los datos del campo se almacenan en los nodos de la carga útil del flujo de trabajo.

Para configurar el paso, debe especificar el grupo o usuario al que asignar el elemento de trabajo y la ruta al formulario.

>[!CAUTION]
>
>Esta sección trata la [Sección Forms de componentes base para la creación de páginas](/help/sites-authoring/default-components-foundation.md#form).

#### Etapa del participante del formulario: configuración {#form-participant-step-configuration}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](#step-properties-common-tab)
* [Usuario/grupo](#step-properties-user-group-tab)
* **Formulario**

   * **Ruta del formulario**: La ruta al [formulario creado](#form-participant-step-creating-the-form).

#### Paso del participante en el formulario: Creación del formulario {#form-participant-step-creating-the-form}

Cree un formulario para utilizarlo con un **Etapa de participante del formulario** como normal. Sin embargo, los formularios para una etapa de participante en el formulario deben tener las siguientes configuraciones:

* La variable **Inicio de formulario** debe tener el **Tipo de acción** propiedad establecida en `Edit Workflow Controlled Resource(s)`.
* La variable **Inicio de formulario** debe tener un valor para la variable `Form Identifier` propiedad.
* Los componentes de formulario deben tener la variable **Nombre del elemento** propiedad establecida en la ruta del nodo en el que se almacenan los datos del campo. La ruta debe localizar un nodo en el contenido de carga útil del flujo de trabajo. El valor utiliza el siguiente formato:

   `./jcr:content/path_to_node`

* El formulario debe incluir un **Botón de envío del flujo de trabajo** componente. No se configura ninguna propiedad del componente.

Los requisitos del flujo de trabajo determinan dónde se deben almacenar los datos de campo. Por ejemplo, los datos de campo se pueden utilizar para configurar las propiedades del contenido de la página. El siguiente valor de un **Nombre del elemento** la propiedad almacena datos de campo como el valor del `redirectTarget` propiedad de la variable `jcr:content` nodo:

`./jcr:content/redirectTarget`

En el ejemplo siguiente, los datos de campo se utilizan como contenido de un **Texto** en la página de carga útil:

`./jcr:content/par/text_3/text`

El primer ejemplo se puede utilizar para cualquier página en la que `cq:Page` se procesa el componente. El segundo ejemplo solo se puede usar cuando la página de carga útil incluye un **Texto** componente que tiene un ID de `text_3`.

El formulario puede encontrarse en cualquier lugar del repositorio, pero los usuarios del flujo de trabajo deben estar autorizados para leer el formulario.

### Selector aleatorio de participantes {#random-participant-chooser}

La variable **Selector de participante aleatorio** es un selector de participantes que asigna el elemento de trabajo generado a un usuario que se selecciona aleatoriamente en una lista.

![wf-31](assets/wf-31.png)

#### Selector de participante aleatorio: configuración {#random-participant-chooser-configuration}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](#step-properties-common-tab)
* **Argumentos**

   * **Participantes**: Especifica la lista de usuarios disponibles para la selección. Para agregar un usuario a la lista, haga clic en **Agregar elemento** y escriba la ruta principal del nodo de usuario o del ID de usuario. El orden de los usuarios no afecta a la probabilidad de que se les asigne un elemento de trabajo.

### Selector de participantes del lanzador de flujo de trabajo {#workflow-initiator-participant-chooser}

La variable **Selector de participante del iniciador de flujo de trabajo** es un selector de participantes que asigna el elemento de trabajo generado al usuario que inició el flujo de trabajo. No hay propiedades para configurar que no sean la **Frecuentes** propiedades.

#### Selector de participante del iniciador de flujo de trabajo: configuración {#workflow-initiator-participant-chooser-configuration}

Para configurar el paso, edite mediante las siguientes pestañas:

* [Común](#step-properties-common-tab)

## Etapa del proceso {#process-step}

A **Paso de proceso** ejecuta un ECMAScript o llama a un servicio OSGi para realizar el procesamiento automático.

![wf-32](assets/wf-32.png)

### Paso de proceso: Configuración {#process-step-configuration}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](#step-properties-common-tab)
* **Proceso**

   * **Proceso**: Implementación del proceso que se va a ejecutar. Utilice el menú desplegable para seleccionar el servicio ECMAScript o OSGi. Para obtener información acerca de:

      * Los servicios estándar ECMAScripts y OSGi, consulte [Procesos integrados para pasos de proceso](/help/sites-developing/workflows-process-ref.md).
      * Creación de ECMAScripts para un paso de proceso, consulte [Implementación de un paso de proceso con un ECMAScript](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript).
      * Creación de servicios OSGi para un paso de proceso, consulte [Implementación de un paso de proceso con una clase Java™](/help/sites-developing/workflows-customizing-extending.md#implementing-a-process-step-with-a-java-class).
   * **Avance del controlador**: Seleccione esta opción para avanzar automáticamente el flujo de trabajo al paso siguiente después de la ejecución. Si no se selecciona, la secuencia de comandos de implementación debe gestionar el progreso del flujo de trabajo.
   * **Argumentos**: Argumentos que se van a pasar al proceso.


## Establecer variable {#set-variable}

El paso Establecer variable permite establecer el valor de una variable y definir el orden en que se configuran los valores. La variable se configura en el orden en que las asignaciones de variables se enumeran en el paso Establecer variable .

![Añadir asignación para configurar una variable](assets/set_variable_addmappingnew.png)

### Establecer variable: configuración {#setvariable}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](/help/sites-developing/workflows-step-ref.md#step-properties-common-tab)
* **Asignación**

   * **Seleccionar variable:** Utilice esta opción para seleccionar una variable y establecer su valor.
   * **Seleccione Modo de asignación:**  Para configurar el valor de la variable , seleccione un modo de asignación. Según el tipo de datos de la variable, puede utilizar las siguientes opciones para establecer su valor:

      * **Literal:** utilice la opción cuando conozca el valor exacto que desea especificar.
      * **Expresión:** utilice la opción cuando el valor que se va a utilizar se calcule en función de una expresión. La expresión se crea en el editor de expresiones proporcionado.
      * **Notación de puntos JSON:** Utilice la opción para recuperar un valor de una variable de tipo JSON o FDM.
      * **XPATH:** Utilice la opción para recuperar un valor de una variable de tipo XML.
      * **En relación con la carga útil:** Utilice la opción cuando el valor que se va a guardar en la variable esté disponible en una ruta relativa a la carga útil.
      * **Ruta absoluta:** Utilice la opción cuando el valor que se va a guardar en la variable esté disponible en una ruta absoluta.
   * **Especificar valor:** Para asignar a la variable , especifique un valor. El valor que especifique en este campo depende del modo de asignación.
   * **Agregar asignación:** Utilice esta opción para agregar más asignaciones y establecer un valor para la variable .
