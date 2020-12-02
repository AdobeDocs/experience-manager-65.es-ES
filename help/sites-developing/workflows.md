---
title: Desarrollo y ampliación de Flujos de trabajo
seo-title: Desarrollo y ampliación de Flujos de trabajo
description: AEM proporciona varias herramientas y recursos para crear modelos de flujo de trabajo, desarrollar pasos de flujo de trabajo e interactuar mediante programación con flujos de trabajo
seo-description: AEM proporciona varias herramientas y recursos para crear modelos de flujo de trabajo, desarrollar pasos de flujo de trabajo e interactuar mediante programación con flujos de trabajo
uuid: 5a857589-3b13-4519-bda2-b1dab6005550
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 8954e3df-3afa-4d53-a7e1-255f3b8f499f
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6
workflow-type: tm+mt
source-wordcount: '1535'
ht-degree: 1%

---


# Desarrollo y ampliación de Flujos de trabajo{#developing-and-extending-workflows}

AEM proporciona varias herramientas y recursos para crear modelos de flujo de trabajo, desarrollar pasos de flujo de trabajo e interactuar mediante programación con flujos de trabajo.

Los flujos de trabajo le permiten automatizar procesos para administrar recursos y publicar contenido en su entorno de AEM. Los flujos de trabajo constan de una serie de pasos, cada uno de los cuales realiza una tarea discreta. Puede utilizar datos lógicos y de tiempo de ejecución para tomar decisiones sobre cuándo puede continuar un proceso y seleccionar el siguiente paso de uno de los varios pasos posibles.

Por ejemplo, los procesos empresariales para crear y publicar páginas web incluyen tareas de aprobación y de cierre de sesión de varios participantes. Estos procesos se pueden modelar con flujos de trabajo de AEM y aplicar a contenido específico.

A continuación se explican los aspectos clave, mientras que en las páginas siguientes se explican más detalles:

* [Creación de modelos de flujo de trabajo](/help/sites-developing/workflows-models.md)
* [Ampliación de la funcionalidad del flujo de trabajo](/help/sites-developing/workflows-customizing-extending.md)
* [Interactuar con Flujos de trabajo mediante programación](/help/sites-developing/workflows-program-interaction.md)
* [Referencia de pasos de flujo de trabajo](/help/sites-developing/workflows-step-ref.md)
* [Referencia del proceso de flujo de trabajo](/help/sites-developing/workflows-process-ref.md)
* [Prácticas recomendadas del flujo de trabajo](/help/sites-developing/workflows-best-practices.md)

>[!NOTE]
>
>Para obtener información sobre:
>
>* Participar en flujos de trabajo, consulte [Uso de Flujos de trabajo](/help/sites-authoring/workflows.md).
>* Administrar flujos de trabajo e instancias de flujo de trabajo, consulte [Administración de Flujos de trabajo](/help/sites-administering/workflows.md).
>* Para consultar un artículo completo de la comunidad, consulte [Modificación de recursos digitales mediante Flujos de trabajo de Adobe Experience Manager.](https://helpx.adobe.com/experience-manager/using/modify_asset_workflow.html)
>* Consulte el [Seminario web de preguntas a los AEM expertos sobre Flujos de trabajo](https://bit.ly/ATACE218).
>* Para consultar un artículo completo de la comunidad, consulte [Creación de un paso personalizado de participante dinámico de Adobe Experience Manager 6.3](https://helpx.adobe.com/experience-manager/using/dynamic-steps-aem63.html).
>* Los cambios en las ubicaciones de la información se pueden consultar en [Reestructuración del repositorio en AEM 6.5](/help/sites-deploying/repository-restructuring.md) y [Prácticas recomendadas del flujo de trabajo - Ubicaciones](/help/sites-developing/workflows-best-practices.md#locations).

>



## Modelo {#model}

Un `WorkflowModel` representa una definición (modelo) de un flujo de trabajo. Está compuesto por `WorkflowNodes` y `WorkflowTransitions`. Las transiciones conectan los nodos y definen el *flujo*. El modelo siempre tiene un nodo de inicio y un nodo final.

### Modelo de tiempo de ejecución {#runtime-model}

Los modelos de flujo de trabajo tienen versiones. Cuando ejecute una instancia de flujo de trabajo, utilizará (y mantendrá) el modelo de tiempo de ejecución del flujo de trabajo (tal como está disponible en el momento en que se inició el flujo de trabajo).

Un modelo de tiempo de ejecución se [genera cuando **Sync** se activa en el editor de modelos de flujo de trabajo](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model).

Las ediciones al modelo de flujo de trabajo que se producen y/o a los modelos de tiempo de ejecución que se generan, *después de* que se inició la instancia específica no se aplicarán a esa instancia.

>[!CAUTION]
>
>Los pasos realizados son los definidos por el [modelo de tiempo de ejecución](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model); esto se genera cuando se activa la acción **Sync** en el editor de modelos de flujo de trabajo.
>
>Si el modelo de flujo de trabajo se cambia después de este momento (sin **sincronizar** activarse), la instancia de tiempo de ejecución no reflejará esos cambios. Solo los modelos de tiempo de ejecución generados después de la actualización reflejarán los cambios. Las excepciones son las secuencias de comandos de ECMA subyacentes, que sólo se conservan una vez que se realizan los cambios.

### Paso {#step}

Cada paso logra una tarea discreta. Existen diferentes tipos de pasos de flujo de trabajo:

* Participante (usuario/grupo): Estos pasos generan un elemento de trabajo y lo asignan a un usuario o grupo. Un usuario debe completar el elemento de trabajo para avanzar en el flujo de trabajo.
* Proceso (secuencia de comandos, llamada al método Java): El sistema ejecuta automáticamente estos pasos. Una secuencia de comandos ECMA o una clase Java implementa el paso. Los servicios se pueden desarrollar para escuchar eventos especiales de flujo de trabajo y realizar tareas según la lógica empresarial.
* Contenedor (Subflujo de trabajo): Este tipo de paso inicio otro modelo de flujo de trabajo.
* O Dividir/Unir: Utilice la lógica para decidir qué paso ejecutar después en el flujo de trabajo.
* Y dividir/unir: Permite ejecutar varios pasos simultáneamente.

Todos los pasos comparten las siguientes propiedades comunes: `Autoadvance` y `Timeout` alertas (script).

### Transición {#transition}

Un `WorkflowTransition` representa una transición entre dos `WorkflowNodes` de un `WorkflowModel`.

* Define el vínculo entre dos pasos consecutivos.
* Es posible aplicar reglas.

### WorkItem {#workitem}

Una `WorkItem` es la unidad que se pasa a través de una instancia `Workflow` de un `WorkflowModel`. Contiene el `WorkflowData` en el que la instancia actúa y una referencia al `WorkflowNode` que describe el paso subyacente del flujo de trabajo.

* Se utiliza para identificar la tarea y se coloca en la bandeja de entrada correspondiente.
* Una instancia de flujo de trabajo puede tener uno o varios `WorkItems` al mismo tiempo (según el modelo de flujo de trabajo).
* El `WorkItem` hace referencia a la instancia de workflow.
* En el repositorio, `WorkItem` se almacena debajo de la instancia de flujo de trabajo.

### Carga útil {#payload}

Hace referencia al recurso que se debe avanzar a través de un flujo de trabajo.

La implementación de carga útil hace referencia a un recurso del repositorio (por ruta, UUID o URL) o por un objeto Java serializado. Hacer referencia a un recurso en el repositorio es muy flexible y en conjunto con sling muy productivo; por ejemplo, el nodo al que se hace referencia se puede representar como un formulario.

### Ciclo de vida {#lifecycle}

Se crea al iniciar un nuevo flujo de trabajo (eligiendo el modelo de flujo de trabajo correspondiente y definiendo la carga útil) y finaliza cuando se procesa el nodo final.

Las siguientes acciones son posibles en una instancia de flujo de trabajo:

* Terminar
* Suspender
* Reanudar
* Reiniciar

Las instancias completadas y terminadas se archivan.

### Bandeja de entrada {#inbox}

Cada cuenta de usuario tiene su propia bandeja de entrada de flujo de trabajo en la que se puede acceder a los `WorkItems` asignados.

Los `WorkItems` se asignan directamente a la cuenta de usuario o al grupo al que pertenecen.

### Tipos de flujo de trabajo {#workflow-types}

Existen varios tipos de flujo de trabajo, como se indica en la consola Modelos de flujo de trabajo:

![wf-upgrade-03](assets/wf-upgraded-03.png)

* **Valor predeterminado**

   Estos son los flujos de trabajo predeterminados incluidos en una instancia de AEM estándar.

* Flujos de trabajo personalizados (sin indicador en la consola)

   Son flujos de trabajo que se han creado como nuevos o a partir de flujos de trabajo listos para usar que se han superpuesto con personalizaciones.

* **Heredado**

   Flujos de trabajo creados en una versión anterior de AEM. Estos se pueden conservar durante una actualización o exportar como paquete de workflow desde la versión anterior y luego importar a la nueva versión.

### Flujos de trabajo transitorios {#transient-workflows}

Los flujos de trabajo estándar guardan información de tiempo de ejecución (historial) durante la ejecución. También puede definir un modelo de flujo de trabajo como **Temporal** para evitar que este historial se mantenga. Se utiliza para ajustar el rendimiento, ya que ahorra/evita el tiempo/recursos utilizados para mantener la información.

Pueden utilizarse flujos de trabajo transitorios para cualquier flujos de trabajo que:

* se ejecutan con frecuencia.
* no necesita el historial de flujo de trabajo.

Se introdujeron flujos de trabajo transitorios para cargar un gran número de recursos, donde la información de los recursos es importante, pero no el historial de tiempo de ejecución del flujo de trabajo.

>[!NOTE]
>
>Consulte [Creación de un flujo de trabajo transitorio](/help/sites-developing/workflows-models.md#creating-a-transient-workflow) para obtener más detalles.

>[!CAUTION]
>
>Cuando un modelo de flujo de trabajo se marca como transitorio, hay algunos escenarios en los que la información del tiempo de ejecución se mantendrá:
>
>* El tipo de carga útil (por ejemplo, vídeo) requiere pasos externos para el procesamiento; en estos casos, el historial de tiempo de ejecución es necesario para la confirmación del estado.
>* El flujo de trabajo introduce un **Y dividido**; en estos casos, el historial de tiempo de ejecución es necesario para la confirmación del estado.
>* Cuando el flujo de trabajo transitorio entra en el paso de un participante, cambia el modo (en tiempo de ejecución) a no transitorio; a medida que la tarea se pasa a una persona, el historial debe persistir

>



>[!CAUTION]
>
>Dentro de un flujo de trabajo transitorio no debe utilizar un **paso Goto**.
>
>Esto sucede cuando el **Paso de goto** crea un trabajo de sling para continuar el flujo de trabajo en el punto `goto`. Esto frustra el propósito de hacer que el flujo de trabajo sea transitorio y genera un error en el archivo de registro.
>
>Para tomar decisiones en un flujo de trabajo transitorio, puede utilizar el **OR Split**.

>[!NOTE]
>
>Consulte [Prácticas recomendadas para los recursos](/help/assets/performance-tuning-guidelines.md#transient-workflows) para obtener más información sobre el impacto de los Flujos de trabajo transitorios en el rendimiento de los recursos.

### Compatibilidad con varios recursos {#multi-resource-support}

La activación de **Compatibilidad con varios recursos** para el modelo de flujo de trabajo significa que se iniciará una sola instancia de flujo de trabajo incluso cuando se seleccionen varios recursos; se adjuntarán como paquete.

Si **Compatibilidad con varios recursos** no está activada para el modelo de flujo de trabajo y se seleccionan varios recursos, se iniciará una instancia de flujo de trabajo individual para cada recurso.

>[!NOTE]
>
>Consulte [Configuración de un flujo de trabajo para compatibilidad con varios recursos](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) para obtener más detalles.

### Etapas de flujo de trabajo {#workflow-stages}

Las etapas del flujo de trabajo ayudan a visualizar el progreso de un flujo de trabajo al administrar tareas. Se pueden utilizar para proporcionar una visión general de hasta dónde se encuentra el flujo de trabajo a través del procesamiento, ya que cuando se ejecuta el flujo de trabajo, el usuario puede realizar una vista del progreso descrito en **Stage** (a diferencia de un paso individual).

Como los nombres de los pasos individuales pueden ser específicos y técnicos, los nombres de las etapas se pueden definir para proporcionar una vista conceptual del progreso del flujo de trabajo.

Por ejemplo, para un flujo de trabajo con seis pasos y cuatro etapas:

1. Puede [configurar las fases del flujo de trabajo (que muestran el progreso del flujo de trabajo) y luego asignar la etapa adecuada a cada paso del flujo de trabajo](/help/sites-developing/workflows-models.md#configuring-workflow-stages-that-show-workflow-progress):

   * Se pueden crear varios nombres de etapa.
   * A continuación, se asigna un nombre de escenario individual a cada paso (se puede asignar un nombre de escenario a uno o varios pasos).

   | **Nombre del paso** | **Etapa (asignada al paso)** |
   |---|---|
   | Etapa 1 | Crear |
   | Etapa 2 | Crear |
   | Etapa 3 | Crítica |
   | Etapa 4 | Aprobar |
   | Etapa 5 | Completar |
   | Etapa 6 | Completar |

1. Cuando se ejecuta el flujo de trabajo, el usuario puede realizar la vista del progreso según los nombres de las fases (en lugar de los nombres de los pasos). El progreso del flujo de trabajo se mostrará en la ficha [INFORMACIÓN DEL FLUJO DE TRABAJO de la ventana de detalles de tarea del elemento de trabajo](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions) que se encuentra en la [Bandeja de entrada](/help/sites-authoring/inbox.md).

### Flujos de trabajo y Forms {#workflows-and-forms}

Normalmente, los flujos de trabajo se utilizan para procesar los envíos de formularios en AEM. Esto puede suceder con los [componentes principales de los componentes de formulario](https://helpx.adobe.com/experience-manager/core-components/using/form-container.html) disponibles en una instancia de AEM estándar o con la [solución de AEM Forms](/help/forms/using/aem-forms-workflow.md).

Al crear un nuevo formulario, el envío del formulario se puede asociar fácilmente con un modelo de flujo de trabajo; por ejemplo, almacenar el contenido en una ubicación concreta del repositorio o notificar al usuario el envío del formulario y su contenido.

### Flujos de trabajo y traducción {#workflows-and-translation}

Los flujos de trabajo también forman parte integrante del proceso de [traducción](/help/sites-administering/translation.md).
