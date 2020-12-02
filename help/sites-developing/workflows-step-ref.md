---
title: Referencia de pasos de flujo de trabajo
seo-title: Referencia de pasos de flujo de trabajo
description: nulo
seo-description: nulo
uuid: 88bf6997-73a1-4639-82aa-5dff08d3ef86
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e3afffd0-d90c-4bd0-b814-f7aeac6ceb6d
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '3286'
ht-degree: 2%

---


# Referencia de pasos del flujo de trabajo {#workflow-step-reference}

Los modelos de flujo de trabajo constan de una serie de pasos de varios tipos. Según el tipo, estos pasos pueden configurarse y ampliarse con parámetros y secuencias de comandos para proporcionar la funcionalidad y el control que necesite.

>[!NOTE]
>
>Esta sección trata los pasos estándar del flujo de trabajo.
>
>Para ver los pasos específicos del módulo, consulte también:
>
>* [Referencia de pasos de flujo de trabajo de AEM Forms](/help/forms/using/aem-forms-workflow-step-reference.md)
>* [Processing Assets Using Media Handlers and Workflows](/help/assets/media-handlers.md)

>



## Propiedades de la etapa {#step-properties}

Cada componente de paso tiene un cuadro de diálogo **Propiedades del paso** que le permite definir y editar las propiedades requeridas.

### Propiedades del paso: ficha común {#step-properties-common-tab}

Hay una combinación de las siguientes propiedades disponibles para la mayoría de los componentes de paso del flujo de trabajo, en la ficha **Common** del cuadro de diálogo de propiedades:

* ****
TítuloTítulo del paso.

* ****
DescripciónDescripción del paso.

* **Fase del flujo de trabajo**

   Un selector desplegable para aplicar un [escenario](/help/sites-developing/workflows.md#workflow-stages) al paso.

* **Tiempo de espera**

   Período después del cual se &quot;agotó el tiempo de espera&quot; del paso.
Puede seleccionar entre: **Desactivado**, **Inmediato**, **1h**, **6h**, **12h**, **24h**.

* **Controlador de tiempo de espera**

   El controlador que controlará el flujo de trabajo cuando se agote el tiempo de espera; por ejemplo:
   `Auto Advancer`

* **Avance de controlador**

   Seleccione esta opción para avanzar automáticamente el flujo de trabajo al paso siguiente después de la ejecución. Si no se selecciona, la secuencia de comandos de implementación debe gestionar el avance del flujo de trabajo.

### Propiedades del paso - ficha Usuario/Grupo {#step-properties-user-group-tab}

Las siguientes propiedades están disponibles para muchos componentes de paso de flujo de trabajo, en la ficha **Usuario/Grupo** del cuadro de diálogo de propiedades:

* **Notificar al usuario a través del correo electrónico**

   * Puede notificar a los participantes enviándoles un correo electrónico cuando el flujo de trabajo llegue al paso.
   * Si está habilitada, se enviará un correo electrónico al usuario definido por la propiedad **User/Group** o a cada miembro del grupo si se define un grupo.

* **Usuario/grupo**

   * Un cuadro de selección desplegable le permitirá desplazarse y seleccionar un usuario o grupo.
   * Si asigna el paso a un usuario específico, sólo este usuario puede realizar una acción en el paso.
   * Si asigna el paso a un grupo completo, cuando el flujo de trabajo alcance este paso, todos los usuarios de este grupo tendrán la acción en su **Bandeja de entrada de workflow**.
   * Consulte [Participación en Flujos de trabajo](/help/sites-authoring/workflows-participating.md) para obtener más información.

## División AND {#and-split}

La división **AND** crea una división en el flujo de trabajo, tras la cual ambas ramas estarán activas. Puede agregar pasos de flujo de trabajo a cada rama según sea necesario. Este paso le permite introducir varias rutas de procesamiento en el flujo de trabajo. Por ejemplo, puede permitir que ciertos pasos de revisión se produzcan en paralelo, lo que ahorra tiempo.

![wf-26](assets/wf-26.png)

### División AND - Configuración {#and-split-configuration}

Para configurar la división:

* Edite las **Propiedades de división AND**:

   * **Nombre** dividido: asignar un nombre para fines explicativos
   * Seleccione el número de ramas necesarias; 2, 3, 4 o 5.

* Añada los pasos del flujo de trabajo a las ramas según sea necesario.

   ![wf-27](assets/wf-27.png)

## Paso de contenedor {#container-step}

Un paso de contenedor inicio otro modelo de flujo de trabajo que se ejecuta como flujo de trabajo secundario.

Este contenedor le permite reutilizar modelos de flujo de trabajo para implementar secuencias comunes de pasos. Por ejemplo, un modelo de flujo de trabajo de traducción podría utilizarse en varios flujos de trabajo de edición.

![wf-28](assets/wf-28.png)

### Paso de contenedor: Configuración {#container-step-configuration}

Para configurar el paso, edite y utilice las fichas siguientes:

* [Común](#step-properties-common-tab)
* **Contenedor**

   * **Subflujo de trabajo**: Seleccione el flujo de trabajo para el inicio.

## Ir a la etapa {#goto-step}

El **Paso Goto** le permite especificar el siguiente paso que se ejecutará en el modelo de flujo de trabajo. Puede especificar una definición de regla, una secuencia de comandos externa o una secuencia de comandos ECMA como expresión de enrutamiento para evaluar el paso siguiente del modelo de flujo de trabajo.

* Si la condición especificada tiene el valor true, se completa el **Paso Goto** y el motor de flujos de trabajo ejecuta el paso especificado.
* Si la condición especificada no tiene el valor true, el **Paso de goto** se completa y la lógica de enrutamiento normal determina el siguiente paso que se va a ejecutar.

El **Paso Goto** le permite implementar estructuras de enrutamiento avanzadas en los modelos de flujo de trabajo. Por ejemplo, para implementar un bucle, se puede definir el **paso Goto** para ejecutar un paso anterior en el flujo de trabajo, con la expresión enrutamiento evaluando una condición de bucle.

### Ir al paso - Configuración {#goto-step-configuration}

Para configurar el paso, edite y utilice las fichas siguientes:

* [Común](#step-properties-common-tab)
* **Proceso**

   * **Paso** de destinatario: Seleccione el paso que se va a ejecutar después de evaluar la condición de la expresión de enrutamiento.
   * **Expresión** de enrutamiento: Seleccione Definición de regla, Secuencia de comandos externa o una secuencia de comandos ECMA que determine si se va a ejecutar el paso **de** Destinatario.

      * **Definición de regla:** utilice el  [editor de ](/help/forms/using/variable-in-aem-workflows.md#use-expression-editor) expresiones para definir la regla.
      * **Secuencia de comandos externa:** la ruta de la secuencia de comandos externa.
      * **Secuencia de comandos** de ECMA: La secuencia de comandos que determina si se va a ejecutar el paso  **Goto**.

#### Simulación de un bucle para {#simulating-a-for-loop}

Para simular un bucle for es necesario mantener un recuento del número de iteraciones de bucle que se han producido:

* El recuento representa normalmente un índice de elementos en los que se actúa en el flujo de trabajo.
* El recuento se evalúa como el criterio de salida del bucle.

Por ejemplo, para implementar un flujo de trabajo que realiza una acción en varios nodos JCR, puede utilizar un contador de bucle como índice para los nodos. Para mantener el recuento, almacene un valor `integer` en el mapa de datos de la instancia de flujo de trabajo. Utilice la secuencia de comandos de **Goto Step** para incrementar el recuento y comparar el recuento con los criterios de salida.

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

También puede simular un bucle for utilizando Definición de regla como expresión de enrutamiento. [Cree una  **** ](/help/forms/using/variable-in-aem-workflows.md#create-a-variable) variable contable de tipo de datos Long. Utilice **Expresión** como modo de asignación en el paso **[Establecer variable](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable)** para establecer el valor de la variable **count** en **count + 1** en cada ejecución del paso **Establecer variable**.

![Simulación de un bucle for](assets/variable_use_case_count_new.png)

En el **Paso Goto**, utilice **Variable de conjunto** como el **Paso de Destinatario** y **cuente &lt; 5** como expresión de enrutamiento.

![Condición para simular un bucle for](assets/variable_use_case_count1_new.png)

El paso **Establecer variable** se ejecuta incrementando repetidamente el valor de la variable **count** en 1 en cada ejecución hasta que el valor alcance 5.

## División OR {#or-split}

La división **O** crea una división en el flujo de trabajo, tras la cual sólo una rama estará activa. Este paso le permite introducir rutas de procesamiento condicionales en el flujo de trabajo. Puede agregar pasos de flujo de trabajo a cada rama según sea necesario.

>[!NOTE]
>
>Para obtener información adicional sobre la creación de una división O, consulte: [https://helpx.adobe.com/experience-manager/using/aem64_workflow_servlet.html](https://helpx.adobe.com/experience-manager/using/aem64_workflow_servlet.html)

![Ramificación mediante O división](assets/variables_orsplit_new.png)

### División OR - Configuración {#or-split-configuration}

Para configurar la división:

* Edite las **Propiedades divididas OR**:

   * **Común**

      * Especifique el nombre dividido.
   * **Ramas (*x)***

      * **Añadir rama:** Añada más ramas al paso.
      * **Seleccionar Expresión** de Enrutamiento: Seleccione la expresión de enrutamiento para evaluar la rama activa. Los valores posibles incluyen: Definición de regla, script externo y secuencia de comandos ECMA.
      * **Haga clic para Añadir la Expresión**: Añada la expresión para evaluar la rama activa si selecciona  **Definición de** regla como expresión de enrutamiento.
      * **Ruta** de script: Ruta de acceso a un archivo que contiene la secuencia de comandos para evaluar la rama activa si selecciona  **Secuencias de** comandos externas en la expresión enrutamiento.
      * **Secuencia de comandos**: Añada la secuencia de comandos en el cuadro para evaluar la rama activa si selecciona  **Secuencias de** comandos de ECMA en la expresión de enrutamiento.
      * **Ruta** predeterminada: La rama predeterminada se sigue en el caso de varias ramas. Sólo puede especificar una rama como predeterminada.

   >[!NOTE]
   >
   >    * Una rama se evalúa a la vez según la expresión de enrutamiento.
   >    * Las ramas se evalúan de arriba abajo.
   >    * Se ejecuta la primera secuencia de comandos que se evalúa como true.
   >    * Si ninguna rama se evalúa como verdadera, el flujo de trabajo no avanza.


   >[!NOTE]
   >
   >Consulte [Definición de una regla para una división OR](/help/sites-developing/workflows-models.md#defineruleecmascript).

* Añada los pasos del flujo de trabajo a las ramas según sea necesario.

## Pasos y opciones del participante {#participant-steps-and-choosers}

### Etapa de participante {#participant-step}

Un **paso de participante** le permite asignar la propiedad para una acción en particular. El flujo de trabajo sólo se realizará cuando el usuario haya reconocido manualmente el paso. Se utiliza cuando se desea que alguien realice una acción en el flujo de trabajo; por ejemplo, un paso de revisión.

Aunque no está directamente relacionada, la autorización del usuario debe tenerse en cuenta al asignar una acción; el usuario debe tener acceso a la página que es la carga útil del flujo de trabajo.

#### Paso del participante: configuración {#participant-step-configuration}

Para configurar el paso, edite y utilice las fichas siguientes:

* [Común](#step-properties-common-tab)
* [Usuario/grupo](#step-properties-user-group-tab)

>[!NOTE]
>
>El iniciador del flujo de trabajo siempre recibe una notificación cuando:
>
>* El flujo de trabajo se ha completado (terminado).
>* El flujo de trabajo se anula (termina).

>



>[!NOTE]
>
>Es necesario configurar algunas propiedades para habilitar las notificaciones por correo electrónico. También puede personalizar la plantilla de correo electrónico o agregar una plantilla de correo electrónico para un nuevo idioma. Consulte [Configuración de la notificación por correo electrónico](/help/sites-administering/notification.md#configuringemailnotification) para configurar las notificaciones por correo electrónico en AEM.

### Etapa de participante de cuadro de diálogo {#dialog-participant-step}

Utilice un **paso del participante en el cuadro de diálogo** para recopilar información del usuario al que se asignó el elemento de trabajo. Este paso resulta útil para recopilar pequeñas cantidades de datos que se utilizan más adelante en el flujo de trabajo.

Al completar el paso, el cuadro de diálogo **Completar elemento de trabajo** contiene los campos que se definen en el cuadro de diálogo. Los datos recopilados en los campos se almacenan en nodos de la carga útil del flujo de trabajo. Los siguientes pasos del flujo de trabajo pueden leer el valor del repositorio.

Para configurar el paso, especifique el grupo o usuario al que desea asignar el elemento de trabajo y la ruta al cuadro de diálogo.

#### Paso de participante en el cuadro de diálogo: configuración {#dialog-participant-step-configuration}

Para configurar el paso, edite y utilice las fichas siguientes:

* [Común](#step-properties-common-tab)
* [Usuario/grupo](#step-properties-user-group-tab)
* **Cuadro de diálogo**

   * **Ruta** del cuadro de diálogo: Ruta al nodo de cuadro de diálogo del  [cuadro de diálogo que cree](#dialog-participant-step-creating-a-dialog).

#### Paso del participante en el cuadro de diálogo - Creación de un cuadro de diálogo {#dialog-participant-step-creating-a-dialog}

Para crear un cuadro de diálogo debe crear el cuadro de diálogo:

* Decida dónde se almacenarán los datos resultantes [en la carga útil](#dialog-participant-step-storing-data-in-the-payload).
* [Definir el cuadro de diálogo; esto incluye definir los campos utilizados para recopilar (y guardar) los datos](#dialog-participant-step-dialog-definition).

#### Paso del participante en el cuadro de diálogo: Almacenamiento de datos en la carga útil {#dialog-participant-step-storing-data-in-the-payload}

Puede almacenar datos de utilidades en la carga útil del flujo de trabajo o en los metadatos del elemento de trabajo. El formato de la propiedad `name` del nodo del widget determina dónde se almacenan los datos.

* **Almacenar datos con la carga útil**

   * Para almacenar datos de utilidades como propiedad de la carga útil del flujo de trabajo, utilice el siguiente formato para el valor de la propiedad name del nodo de la utilidad:
      `./jcr:content/nodename`

   * Los datos se almacenan en la propiedad `nodename` del nodo de carga útil. Si el nodo no contiene esa propiedad, se crea la propiedad.
   * Cuando se almacena con la carga útil, los usos posteriores del cuadro de diálogo con la misma carga útil sobrescriben el valor de la propiedad.

* **Almacenar datos con el elemento de trabajo**

   * Para almacenar datos de utilidades como propiedad de los metadatos del elemento de trabajo, utilice el siguiente formato para el valor de la propiedad name:
      `nodename`

   * Los datos se almacenan en la propiedad `nodename` del elemento de trabajo `metadata`. Los datos se conservan si el cuadro de diálogo se utiliza posteriormente con la misma carga útil.

#### Paso del participante en el cuadro de diálogo: definición del cuadro de diálogo {#dialog-participant-step-dialog-definition}

1. **Estructura de cuadro de diálogo**

   Los cuadros de diálogo Pasos de los participantes son similares a los cuadros de diálogo que se crean para la creación de componentes. Se almacenan en:

   `/apps/myapp/workflow/dialogs`

   Los cuadros de diálogo para la IU estándar con capacidad táctil tienen la siguiente estructura de nodos:

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
   >Para obtener más información, consulte [Creación y configuración de un cuadro de diálogo](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog).

1. **Propiedad de ruta de cuadro de diálogo**

   El **paso del participante en el cuadro de diálogo** tiene la propiedad **Ruta de diálogo** (junto con las propiedades de un [paso del participante](#participant-step)). El valor de la propiedad **Dialog Path** es la ruta al nodo `dialog` del cuadro de diálogo.

   Por ejemplo, el cuadro de diálogo está contenido en un componente denominado `EmailWatch` que se almacena en el nodo:

   `/apps/myapp/workflows/dialogs`

   Para la IU táctil, se utiliza el siguiente valor para la propiedad **Ruta de diálogo**:

   `/apps/myapp/workflow/dialogs/EmailWatch/cq:dialog`

   ![wf-30](assets/wf-30.png)

1. **Ejemplo de definición de cuadro de diálogo**

   El siguiente fragmento de código XML representa un cuadro de diálogo que almacena un valor `String` en el nodo `watchEmail` del contenido de la carga útil. El nodo title representa el componente [TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/textfield/index.html):

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

   En este ejemplo, en el caso de la IU táctil, se mostrará un cuadro de diálogo como:

   ![chlimage_1-70](assets/chlimage_1-70.png)

### Etapa de participante dinámica {#dynamic-participant-step}

El componente **Paso de participante dinámico** es similar a **[Paso de participante](#participant-step)** con la diferencia de que el participante se selecciona automáticamente en tiempo de ejecución.

Para configurar el paso, seleccione un **Selector de participantes** que identifique al participante al que asignar el elemento de trabajo, junto con un cuadro de diálogo.

#### Paso de participante dinámico: configuración {#dynamic-participant-step-configuration}

Para configurar el paso, edite y utilice las fichas siguientes:

* [Común](#step-properties-common-tab)
* **Selector de participantes**

   * **Selector** de participantes: Nombre del selector de  [participantes que cree](#developingtheparticipantchooser).
   * **Argumentos**: Cualquier argumento necesario.
   * **Correo electrónico**: Si se debe enviar una notificación por correo electrónico al usuario.

* **Cuadro de diálogo**

   * **Ruta** del cuadro de diálogo: Ruta al nodo de cuadro de diálogo del  [cuadro de diálogo que cree (como con el paso **del participante del** cuadro de diálogo)](#dialog-participant-step-creating-a-dialog).

#### Etapa de participante dinámico: desarrollo del selector de participantes {#dynamic-participant-step-developing-the-participant-chooser}

Puede crear el selector de participantes. Por lo tanto, puede utilizar cualquier lógica o criterio de selección. Por ejemplo, el selector de participantes puede seleccionar el usuario (dentro de un grupo) que tenga la menor cantidad de elementos de trabajo. Puede crear cualquier número de usuarios que desee utilizar con distintas instancias del componente **Paso de participante dinámico** en los modelos de flujo de trabajo.

Cree un servicio OSGi o un ECMAScript que seleccione un usuario al que asignar el elemento de trabajo.

* **ECMAscript**

   Las secuencias de comandos deben incluir una función denominada getParticipant que devuelve un ID de usuario como un valor `String`. Almacene las secuencias de comandos personalizadas en, por ejemplo, la carpeta `/apps/myapp/workflow/scripts` o una subcarpeta.

   Se incluye una secuencia de comandos de ejemplo en una instancia de AEM estándar:

   `/libs/workflow/scripts/initiator-participant-chooser.ecma`

   >[!CAUTION]
   >
   >Usted ***no debe*** cambiar nada en la ruta `/libs`.
   >
   >
   >Esto se debe a que el contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y puede sobrescribirse al aplicar una revisión o un paquete de funciones).

   Esta secuencia de comandos selecciona el iniciador del flujo de trabajo como participante:

   ```
   function getParticipant() {
       return workItem.getWorkflow().getInitiator();
   }
   ```

   >[!NOTE]
   >
   >El componente **Selector de participantes del iniciador de flujo de trabajo** amplía el **paso de participante dinámico** y utiliza esta secuencia de comandos como implementación de paso.

* **Servicio OSGi**

   Los servicios deben implementar la interfaz [com.day.cq.workflow.exec.ParticipantStepChooser](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/ParticipantStepChooser.html). La interfaz define los siguientes miembros:

   * `SERVICE_PROPERTY_LABEL` field: Utilice este campo para especificar el nombre del selector de participantes. El nombre aparece en una lista de los usuarios participantes disponibles en las propiedades **Paso de participante dinámico**.

   * `getParticipant` método: Devuelve la identificación principal resuelta dinámicamente como un  `String` valor.
   >[!CAUTION]
   >
   >El método `getParticipant` devuelve la identificación principal resuelta dinámicamente. Puede ser una identificación de grupo o de usuario.
   >
   >
   >Sin embargo, una identificación de grupo solo se puede utilizar para un **paso del participante**, cuando se devuelve una lista de participantes. Para un **paso de participante dinámico** se devuelve una lista vacía y no se puede usar para delegación.

   Para que la implementación esté disponible para los componentes **Paso de participante dinámico**, agregue la clase Java a un paquete OSGi que exporte el servicio e implemente el paquete en el servidor de AEM.

   >[!NOTE]
   >
   >**Las** opciones de participante aleatorio son un servicio de muestra que selecciona un usuario aleatorio (  `com.day.cq.workflow.impl.process.RandomParticipantChooser`). El ejemplo de componente **Elegir participante aleatorio** r extiende el **paso de participante dinámico** y utiliza este servicio como implementación de paso.

#### Etapa de participante dinámico: Ejemplo de servicio de selector de participantes {#dynamic-participant-step-example-participant-chooser-service}

La siguiente clase Java implementa la interfaz `ParticipantStepChooser`. La clase devuelve el nombre del participante que inició el flujo de trabajo. El código utiliza la misma lógica que la secuencia de comandos de ejemplo (`initiator-participant-chooser.ecma`).

La anotación `@Property` establece el valor del campo `SERVICE_PROPERTY_LABEL` en `Workflow Initiator Participant Chooser`.

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

En el cuadro de diálogo de propiedades **Paso de participante dinámico**, la lista **Selector de participante** incluye el elemento `Workflow Initiator Participant Chooser (script)`, que representa este servicio.

Cuando se inicia el modelo de flujo de trabajo, el registro indica el ID del usuario que inició el flujo de trabajo y a quién se le asigna el elemento de trabajo. En este ejemplo, el usuario `admin` inició el flujo de trabajo.

`13.09.2015 15:48:53.037 *INFO* [10.176.129.223 [1347565733037] POST /etc/workflow/instances HTTP/1.1] com.adobe.example.InitiatorParticipantChooser Assigning Dynamic Participant Step work item to admin`

### Etapa de participante de formulario {#form-participant-step}

El **paso del participante en el formulario** presenta un formulario cuando se abre el elemento de trabajo. Cuando el usuario rellena y envía el formulario, los datos del campo se almacenan en los nodos de la carga útil del flujo de trabajo.

Para configurar el paso, debe especificar el grupo o usuario al que asignar el elemento de trabajo y la ruta al formulario.

>[!CAUTION]
>
>Esta sección trata la sección [Forms de Componentes básicos para la creación de páginas](/help/sites-authoring/default-components-foundation.md#form).

#### Paso del participante en el formulario - Configuración {#form-participant-step-configuration}

Para configurar el paso, edite y utilice las fichas siguientes:

* [Común](#step-properties-common-tab)
* [Usuario/grupo](#step-properties-user-group-tab)
* **Formulario**

   * **Ruta** del formulario: Ruta al  [formulario que se crea](#form-participant-step-creating-the-form).

#### Paso del participante en el formulario - Creación del formulario {#form-participant-step-creating-the-form}

Cree un formulario para utilizarlo con un **paso del participante en el formulario** como de costumbre. Sin embargo, los formularios para un paso de participante en el formulario deben tener las siguientes configuraciones:

* El Inicio **del componente Formulario** debe tener la propiedad **Tipo de acción** establecida en `Edit Workflow Controlled Resource(s)`.
* El Inicio **del componente Formulario** debe tener un valor para la propiedad `Form Identifier`.
* Los componentes del formulario deben tener la propiedad **Nombre del elemento** establecida en la ruta del nodo donde se almacenan los datos del campo. La ruta debe ubicar un nodo en el contenido de la carga útil del flujo de trabajo. El valor utiliza el siguiente formato:

   `./jcr:content/path_to_node`

* El formulario debe incluir un componente **Botón(s) de envío de flujo de trabajo**. No se configura ninguna propiedad del componente.

Los requisitos del flujo de trabajo determinan dónde debe almacenar los datos de campo. Por ejemplo, los datos de campo pueden utilizarse para configurar las propiedades del contenido de la página. El siguiente valor de una propiedad **Nombre del elemento** almacena los datos de campo como el valor de la propiedad `redirectTarget` del nodo `jcr:content`:

`./jcr:content/redirectTarget`

En el ejemplo siguiente, los datos de campo se utilizan como contenido de un componente **Text** en la página de carga útil:

`./jcr:content/par/text_3/text`

El primer ejemplo se puede utilizar para cualquier página que el componente `cq:Page` procese. El segundo ejemplo solo se puede usar cuando la página de carga útil incluye un componente **Texto** con un ID de `text_3`.

El formulario puede ubicarse en cualquier lugar del repositorio, pero los usuarios del flujo de trabajo deben estar autorizados para leerlo.

### Selector de participante aleatorio {#random-participant-chooser}

El paso **Selector de participantes aleatorio** es un selector de participantes que asigna el elemento de trabajo generado a un usuario seleccionado aleatoriamente desde una lista.

![wf-31](assets/wf-31.png)

#### Selector de participante aleatorio: configuración {#random-participant-chooser-configuration}

Para configurar el paso, edite y utilice las fichas siguientes:

* [Común](#step-properties-common-tab)
* **Argumentos**

   * **Participantes**: Especifica la lista de usuarios disponibles para la selección. Para agregar un usuario a la lista, haga clic en **Añadir elemento** y escriba la ruta de inicio del nodo de usuario o del ID de usuario. El orden de los usuarios no afecta a la probabilidad de que se les asigne un elemento de trabajo.

### Selector de participante de iniciador de flujo de trabajo {#workflow-initiator-participant-chooser}

El paso **Selector de participantes del iniciador de flujo de trabajo** es un selector de participantes que asigna el elemento de trabajo generado al usuario que inició el flujo de trabajo. No hay propiedades que configurar que no sean las propiedades **Common**.

#### Selector de participante del iniciador de flujo de trabajo: configuración {#workflow-initiator-participant-chooser-configuration}

Para configurar el paso, edite con las fichas siguientes:

* [Común](#step-properties-common-tab)

## Etapa del proceso {#process-step}

Un **paso de proceso** ejecuta un ECMAScript o llama a un servicio OSGi para realizar el procesamiento automático.

![wf-32](assets/wf-32.png)

### Paso de proceso: Configuración {#process-step-configuration}

Para configurar el paso, edite y utilice las fichas siguientes:

* [Común](#step-properties-common-tab)
* **Proceso**

   * **Proceso**: Implementación del proceso que se va a ejecutar. Utilice el menú desplegable para seleccionar el servicio ECMAScript o OSGi. Para obtener información sobre:

      * Los servicios estándar de ECMAScripts y OSGi, consulte [Procesos integrados para los pasos del proceso](/help/sites-developing/workflows-process-ref.md).
      * Creación de ECMAScripts para un paso de proceso, consulte [Implementación de un paso de proceso con un ECMAScript](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript).
      * Creación de servicios OSGi para un paso de proceso, consulte [Implementación de un paso de proceso con una clase de Java](/help/sites-developing/workflows-customizing-extending.md#implementing-a-process-step-with-a-java-class).
   * **Avance** del controlador: Seleccione esta opción para avanzar automáticamente el flujo de trabajo al paso siguiente después de la ejecución. Si no se selecciona, la secuencia de comandos de implementación debe gestionar el avance del flujo de trabajo.
   * **Argumentos**: Argumentos que se van a pasar al proceso.


## Establecer variable {#set-variable}

El paso Establecer variable permite establecer el valor de una variable y definir el orden en que se configuran los valores. La variable se establece en el orden en que las asignaciones de variables se enumeran en el paso Establecer variable.

![Añadir asignación para configurar una variable](assets/set_variable_addmappingnew.png)

### Establecer variable - Configuración {#setvariable}

Para configurar el paso, edite y utilice las fichas siguientes:

* [Común](/help/sites-developing/workflows-step-ref.md#step-properties-common-tab)
* **Asignación**

   * **Seleccionar variable:** utilice esta opción para seleccionar una variable para establecer su valor.
   * **Seleccionar modo de asignación:** seleccione un modo de asignación para definir el valor de la variable. Según el tipo de datos de la variable, puede utilizar las siguientes opciones para establecer el valor de una variable:

      * **Literal:** utilice la opción cuando sepa el valor exacto que desea especificar.
      * **Expresión:** utilice la opción cuando el valor que se va a utilizar se calcule en función de una expresión. La expresión se crea en el editor de expresiones proporcionado.
      * **Notación de punto JSON:** utilice la opción para recuperar un valor de una variable de tipo JSON o FDM.
      * **XPATH:** utilice la opción para recuperar un valor de una variable de tipo XML.
      * **Relativo a la carga útil:** utilice la opción cuando el valor que se va a guardar en la variable esté disponible en una ruta relativa a la carga útil.
      * **Ruta absoluta:** utilice la opción cuando el valor que se va a guardar en la variable esté disponible en una ruta absoluta.
   * **Especificar valor:** especifique un valor para asignarlo a la variable. El valor que especifique en este campo depende del modo de asignación.
   * **Añadir asignación:** utilice esta opción para agregar más asignaciones para establecer un valor para la variable.
