---
title: Variables en flujos de trabajo de AEM
seo-title: Variables en flujos de trabajo de AEM
description: Cree una variable, establezca un valor para la variable y utilícelo en los pasos de flujo de trabajo de O Split y Goto AEM.
seo-description: Cree una variable, establezca un valor para la variable y utilícelo en los pasos de flujo de trabajo de O Split y Goto AEM.
uuid: cc62ff11-51d4-4db4-9c6d-5dc2caa1da52
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: bbb9936e-ecd2-44b3-b4ae-dd62a3160641
docset: aem65
translation-type: tm+mt
source-git-commit: bc042696506bf1691c2eeffc6ab941be85fa274c

---


# Variables en flujos de trabajo de AEM{#variables-in-aem-workflows}

Una variable en un modelo de flujo de trabajo es una forma de almacenar un valor en función de su tipo de datos. A continuación, puede utilizar el nombre de la variable en cualquier paso del flujo de trabajo para recuperar el valor almacenado en la variable. También puede utilizar nombres de variables para definir expresiones para tomar decisiones de enrutamiento.

En los modelos de flujo de trabajo de AEM, puede:

* [Cree una variable](/help/sites-developing/using-variables-in-aem-workflows.md#create-a-variable) de un tipo de datos según el tipo de información que desee almacenar en él.
* [Establezca un valor para la variable](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable) mediante el paso de flujo de trabajo Establecer variable.
* [Utilice la variable](/help/sites-developing/using-variables-in-aem-workflows.md#use-a-variable) en los pasos de flujo de trabajo de O Split y Goto AEM para definir una expresión para tomar decisiones de enrutamiento. También puede utilizar variables en todos los pasos del flujo de trabajo de AEM Forms.

En el siguiente vídeo se muestra cómo crear, establecer y utilizar variables en modelos de flujo de trabajo de AEM:

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/usevariables_example.mp4)

Las variables son una extensión de la interfaz [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) . Puede utilizar [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) en ECMAScript para acceder a los metadatos guardados mediante variables.

## Crear una variable {#create-a-variable}

Las variables se crean mediante la sección Variables disponible en la barra de tareas del modelo de flujo de trabajo. Las variables de flujo de trabajo de AEM admiten los siguientes tipos de datos:

* **Tipos** de datos primitivos: Long, Double, Boolean, Date y String
* **Tipos** de datos complejos: [XML](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/Document.html) y [JSON](https://static.javadoc.io/com.google.code.gson/gson/2.3/com/google/gson/JsonObject.html)

>[!NOTE]
>
>Los flujos de trabajo solo admiten el formato ISO8601 para variables de tipo Date.

Para obtener más tipos de datos complejos disponibles en flujos de trabajo de AEM Forms, consulte [Variables en flujos de trabajo](/help/forms/using/variable-in-aem-workflows.md)de AEM Forms.  Utilice el tipo de datos ArrayList para crear colecciones de variables. Puede crear una variable ArrayList para todos los tipos de datos primitivos y complejos. Por ejemplo, cree una variable ArrayList y seleccione String como subtipo para almacenar varios valores de cadena mediante la variable.

Ejecute los siguientes pasos para crear una variable:

1. En una instancia de AEM, vaya a Herramientas > Flujo de trabajo > Modelos.
1. Toque **[!UICONTROL Crear]** y especifique el título y un nombre opcional para el modelo de flujo de trabajo. Seleccione el modelo y toque **[!UICONTROL Editar]**.
1. Toque el icono de variables disponible en la barra de tareas del modelo de flujo de trabajo y **[!UICONTROL Agregar variable]**.

   ![Añadir variable](assets/variables_add_variable_new.png)

1. En el cuadro de diálogo Agregar variable, especifique el nombre y seleccione el tipo de la variable.
1. Seleccione el tipo de datos en la lista desplegable **[!UICONTROL Tipo]** y especifique los siguientes valores:

   * Tipo de datos primitivo: especifique un valor predeterminado opcional para la variable.
   * JSON o XML: especifique una ruta de esquema JSON o XML opcional. El sistema valida la ruta de esquema mientras asigna y almacena las propiedades disponibles en este esquema a otra variable.
   * Modelo de datos de formulario: especifique una ruta del modelo de datos de formulario.
   * ArrayList: especifique un subtipo para la colección.

1. Especifique una descripción opcional para la variable y toque ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) para guardar los cambios. La variable se muestra en la lista disponible en el panel izquierdo.

Cuando cree variables, tenga en cuenta las siguientes prácticas:

* Cree tantas variables como necesite un flujo de trabajo. Sin embargo, para conservar los recursos de la base de datos, utilice el número mínimo de variables requeridas y reutilice las variables cuando sea posible.
* Las variables distinguen entre mayúsculas y minúsculas. Asegúrese de hacer referencia a variables usando el mismo caso en el flujo de trabajo.
* Evite utilizar caracteres especiales en el nombre de la variable

## Establecer una variable {#set-a-variable}

Puede utilizar el paso Establecer variable para establecer el valor de una variable y definir el orden en que se configuran los valores. La variable se establece en el orden en que las asignaciones de variables se enumeran en el paso de la variable establecida.

Los cambios en los valores de las variables afectan únicamente a la instancia del proceso en el que se produce el cambio. Por ejemplo, cuando se inicia un flujo de trabajo y cambian los datos variables, los cambios solo afectan a esa instancia del flujo de trabajo. Los cambios no afectan a otras instancias del flujo de trabajo que se iniciaron anteriormente o que se iniciaron posteriormente.

Según el tipo de datos de la variable, puede utilizar las siguientes opciones para establecer el valor de una variable:

* **** Literal: Utilice la opción cuando sepa el valor exacto que desea especificar.
* **** Expresión: Utilice la opción cuando el valor que se va a utilizar se calcule en función de una expresión. La expresión se crea en el editor de expresiones proporcionado.
* **** Notación de punto JSON: Utilice la opción para recuperar un valor de una variable de tipo JSON o FDM.
* **** XPATH: Utilice la opción para recuperar un valor de una variable de tipo XML.
* **** Relativo a la carga útil: Utilice la opción cuando el valor que se va a guardar en la variable esté disponible en una ruta relativa a la carga útil.
* **** Ruta absoluta: Utilice la opción cuando el valor que se va a guardar en la variable esté disponible en una ruta absoluta.

También puede actualizar elementos específicos de una variable de tipo JSON o XML mediante notación DOT JSON o notación XPATH.

### Agregar asignación entre variables {#add-mapping-between-variables}

Ejecute los siguientes pasos para agregar la asignación entre variables:

1. En la página de edición del flujo de trabajo, toque el icono Pasos disponible en la barra de tareas del modelo de flujo de trabajo.
1. Arrastre y suelte el paso **Establecer variable** en el editor de flujo de trabajo, toque el paso y seleccione ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/configure_icon.png) (Configurar).
1. En el cuadro de diálogo Establecer variable, seleccione **[!UICONTROL Asignación]** > **[!UICONTROL Agregar asignación]**.
1. En la sección Variable **de** mapa, seleccione la variable para almacenar datos, seleccione el modo de asignación y especifique un valor para almacenarlo en la variable. Los modos de asignación varían según el tipo de variable.
1. Asigne más variables para crear una expresión significativa. Toque ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) para guardar los cambios.

### Ejemplo 1: Consultar una variable XML para establecer el valor de una variable de cadena {#example-query-an-xml-variable-to-set-value-for-a-string-variable}

Seleccione una variable de tipo XML para almacenar un archivo XML. Consulte la variable XML para establecer el valor de una variable de cadena para la propiedad disponible en el archivo XML. Utilice **Especificar XPATH para el campo de variable** XML para definir la propiedad que se almacenará en la variable de cadena.

En este ejemplo, seleccione una variable **de datos** de formulario para almacenar el archivo **cc-app.xml** . Consulte la variable **formdata** para establecer el valor de la variable de cadena **email** a fin de almacenar el valor de la propiedad **emailAddress** disponible en el archivo **cc-app.xml** .

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/set_variable_example1.mp4 "Definir el valor de una variable")

### Ejemplo 2: Usar una expresión para almacenar valores basados en otras variables {#example2}

Utilice una expresión para calcular la suma de las variables y almacenar el resultado en una variable.

En este ejemplo, utilice el editor de expresiones para definir una expresión que calcule la suma de **las variables** value **y** balanceamount **y almacene el resultado en una variable** totalvalue.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_expression.mp4)

## Usar editor de expresiones {#use-expression-editor}

También se utilizan expresiones para calcular el valor de una variable en tiempo de ejecución. Las variables proporcionan un editor de expresiones para definir expresiones.

Utilice el editor de expresiones para:

* Establezca el valor de las variables mediante otras variables de flujo de trabajo, números o expresiones matemáticas.
* Utilizar variables de flujo de trabajo, cadena, número o expresión dentro de una expresión matemática
* Agregue condiciones para establecer los valores de las variables.
* Agregue operadores entre condiciones.

![Editor de expresiones](assets/variables_expression_editor_new.png)

Se basa en el editor de reglas de formularios adaptables con los siguientes cambios. Editor de reglas en variables:

* No admite funciones.
* No proporciona una interfaz de usuario para ver el resumen de reglas
* No tiene editor de código.
* No admite la activación y desactivación del valor de un objeto.
* No admite la propiedad de configuración de un objeto.
* No admite llamar a un servicio Web.

Para obtener más información, consulte Editor [de reglas de formularios](/help/forms/using/rule-editor.md)adaptables.

## Usar una variable {#use-a-variable}

Puede utilizar variables para recuperar entradas y salidas o guardar el resultado de un paso. El editor de flujo de trabajo proporciona dos tipos de pasos de flujo de trabajo:

* Pasos de flujo de trabajo compatibles con variables
* Pasos del flujo de trabajo sin compatibilidad con variables

### Pasos de flujo de trabajo compatibles con variables {#workflow-steps-with-support-for-variables}

El paso Ir a, O Dividir y todos los pasos del flujo de trabajo de AEM Forms admiten variables.

#### Paso dividido OR {#or-split-step}

La división O crea una división en el flujo de trabajo, tras la cual solo una rama está activa. Este paso le permite introducir rutas de procesamiento condicionales en el flujo de trabajo. Puede agregar pasos de flujo de trabajo a cada rama según sea necesario.

Puede definir la expresión de enrutamiento para una rama mediante una definición de regla, una secuencia de comandos ECMA o una secuencia de comandos externa.

Puede utilizar variables para definir la expresión de enrutamiento mediante el editor de expresiones. Para obtener más información sobre el uso de expresiones de enrutamiento para el paso División O, consulte [OR Split step](/help/sites-developing/workflows-step-ref.md#or-split).

En este ejemplo, antes de definir la expresión de enrutamiento, utilice el [ejemplo 2](/help/sites-developing/using-variables-in-aem-workflows.md#example2) para establecer el valor de la variable **totalvalue** . La rama 1 está activa si el valor de la variable **totalvalue** es mayor que 50000. Del mismo modo, puede definir una regla para activar la rama 2 si el valor de la variable **totalvalue** es menor que 50000.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_orsplit_example.mp4)

Del mismo modo, seleccione una ruta de script externa o especifique la secuencia de comandos ECMA para las expresiones de enrutamiento para evaluar la rama activa. Toque **[!UICONTROL Cambiar nombre de rama]** para especificar un nombre alternativo para la rama.

Para obtener más ejemplos, consulte [Creación de un modelo](/help/forms/using/aem-forms-workflow.md#create-a-workflow-model)de flujo de trabajo.

#### Ir al paso {#go-to-step}

El paso **** Goto permite especificar el siguiente paso en el modelo de flujo de trabajo que se va a ejecutar, según el resultado de una expresión de enrutamiento.

De forma similar al paso División OR, puede definir la expresión de enrutamiento para el paso Goto mediante una definición de regla, una secuencia de comandos ECMA o una secuencia de comandos externa.

Puede utilizar variables para definir la expresión de enrutamiento mediante el editor de expresiones. Para obtener más información sobre el uso de expresiones de enrutamiento para el paso Goto, consulte [Ir a paso](/help/sites-developing/workflows-step-ref.md#goto-step).

![Ir a regla](assets/variables_goto_rule1_new.png)

En este ejemplo, el paso Ir especifica la aplicación Revisar tarjeta de crédito como el siguiente paso si el valor de la variable de **acción realizada** es igual a **Necesita más información**.

Para obtener más ejemplos sobre el uso de la definición de regla en el paso Ir, consulte [Simulación de un bucle](/help/sites-developing/workflows-step-ref.md#simulateforloop)For.

#### Pasos del flujo de trabajo centrado en el flujo de trabajo de formularios {#forms-workflow-centric-workflow-steps}

Todos los pasos del flujo de trabajo de AEM Forms admiten variables. Para obtener más información, consulte Flujo de trabajo centrado en [formularios en OSGi](/help/forms/using/aem-forms-workflow-step-reference.md).

### Pasos del flujo de trabajo sin compatibilidad con variables {#workflow-steps-without-support-for-variables}

Puede utilizar la interfaz [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) para acceder a variables en los pasos del flujo de trabajo que no admiten variables.

#### Recuperar el valor de la variable {#retrieve-the-variable-value}

Utilice las siguientes API en el script ECMA para recuperar los valores de las variables existentes según el tipo de datos:

| Tipo de datos variable | API |
|---|---|
| Primitiva (larga, doble, booleana, fecha y cadena) | workItem.getWorkflowData().getMetaDataMap().get(variableName, type) |
| XML | Packages.org.w3c.dom.Document xmlObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.org.w3c.dom.Document.class); |
| JSON | Packages.com.google.gson.JsonObject jsonObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.com.google.gson.JsonObject.class); |

Para obtener información sobre las API para tipos de datos de variables complejas adicionales disponibles en los flujos de trabajo de AEM Forms, consulte [Variables en los flujos de trabajo](/help/forms/using/variable-in-aem-workflows.md)de AEM Forms.

**Ejemplo**

Recupere el valor del tipo de datos de cadena mediante la siguiente API:

```
workItem.getWorkflowData().getMetaDataMap().get(accname, Packages.java.lang.String)
```

#### Actualizar el valor de la variable {#update-the-variable-value}

Utilice la siguiente API en el script ECMA para actualizar el valor de una variable:

```
workItem.getWorkflowData().getMetaDataMap().put(variableName, value)
```

**Ejemplo**

```
workItem.getWorkflowData().getMetaDataMap().put(salary, 50000)
```

actualiza el valor de la variable de **salario** a 50000.

### Establecer variables para invocar flujos de trabajo {#apiinvokeworkflow}

Puede utilizar una API para establecer variables y pasarlas para invocar instancias de flujo de trabajo.

[workflowSession.startWorkflow](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html#startWorkflow-com.adobe.granite.workflow.model.WorkflowModel-com.adobe.granite.workflow.exec.WorkflowData-java.util.Map-) utiliza el modelo, wfData y metaData como argumentos. Utilice MetaDataMap para establecer el valor de la variable.

En esta API, la variable **variableName** se establece en **value **using metaData.put(variableName, valor);

```java
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*Assume that you already have a workflowSession and modelId along with the payloadType and payload*/
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
metaData.put(variableName, value); //Create a variable "variableName" in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

## Editar una variable {#edit-a-variable}

1. En la página de flujo de trabajo de edición, toque el icono Variables disponible en la barra de tareas del modelo de flujo de trabajo. La sección Variables del panel izquierdo muestra todas las variables existentes.
1. Toque el icono ![](https://helpx.adobe.com/content/dam/help/images/en/edit.png) (Editar) junto al nombre de la variable que desee editar.
1. Edite la información de la variable y toque ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) para guardar los cambios. No se pueden editar los campos **[!UICONTROL Nombre]** y **[!UICONTROL Tipo]** de una variable.

## Eliminar una variable {#delete-a-variable}

Antes de eliminar la variable, elimine todas las referencias de la misma del flujo de trabajo. Asegúrese de que la variable no se utilice en el flujo de trabajo.

Ejecute los siguientes pasos para eliminar una variable:

1. En la página de flujo de trabajo de edición, toque el icono Variables disponible en la barra de tareas del modelo de flujo de trabajo. La sección Variables del panel izquierdo muestra todas las variables existentes.
1. Toque el icono Eliminar junto al nombre de la variable que desee eliminar.
1. Toque ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) para confirmar y eliminar la variable.

