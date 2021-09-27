---
title: Desarrollo y ampliación de flujos de trabajo
seo-title: Developing and Extending Workflows
description: AEM proporciona varias herramientas y recursos para crear modelos de flujo de trabajo, desarrollar pasos de flujo de trabajo e interactuar mediante programación con flujos de trabajo
seo-description: AEM provides several tools and resources for creating workflow models, developing workflow steps, and for programmatically interacting with workflows
uuid: 5a857589-3b13-4519-bda2-b1dab6005550
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 8954e3df-3afa-4d53-a7e1-255f3b8f499f
exl-id: 041b1767-8b6c-4887-a70d-abc96a116976
source-git-commit: 82b9b852fa3134f140f8de0bad229282979c8a30
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 3%

---


# Desarrollo y ampliación de flujos de trabajo{#developing-and-extending-workflows}

AEM proporciona varias herramientas y recursos para crear modelos de flujo de trabajo, desarrollar pasos de flujo de trabajo e interactuar mediante programación con flujos de trabajo.

Los flujos de trabajo permiten automatizar procesos para administrar recursos y publicar contenido en el entorno de AEM. Los flujos de trabajo constan de una serie de pasos, y cada paso realiza una tarea discreta. Puede utilizar la lógica y los datos de tiempo de ejecución para tomar decisiones sobre cuándo puede continuar un proceso y seleccionar el siguiente paso de uno de los múltiples pasos posibles.

Por ejemplo, los procesos empresariales para crear y publicar páginas web incluyen las tareas de aprobación y cierre de sesión realizadas por varios participantes. Estos procesos se pueden modelar utilizando flujos de trabajo AEM y aplicar a contenido específico.

A continuación se tratan los aspectos clave, mientras que en las páginas siguientes se incluyen más detalles:

* [Creación de modelos de flujo de trabajo](/help/sites-developing/workflows-models.md)
* [Ampliación de la funcionalidad del flujo de trabajo](/help/sites-developing/workflows-customizing-extending.md)
* [Interactuar con flujos de trabajo mediante programación](/help/sites-developing/workflows-program-interaction.md)
* [Referencia de pasos de flujo de trabajo](/help/sites-developing/workflows-step-ref.md)
* [Referencia del proceso de flujo de trabajo](/help/sites-developing/workflows-process-ref.md)
* [Prácticas recomendadas del flujo de trabajo](/help/sites-developing/workflows-best-practices.md)

>[!NOTE]
>
>Para obtener información acerca de:
>
>* Para participar en flujos de trabajo, consulte [Uso de flujos de trabajo](/help/sites-authoring/workflows.md).
>* Administración de flujos de trabajo e instancias de flujo de trabajo, consulte [Administración de flujos de trabajo](/help/sites-administering/workflows.md).
>* Para ver un artículo completo de la comunidad, consulte [Modificación de recursos digitales mediante flujos de trabajo de Adobe Experience Manager.](https://helpx.adobe.com/experience-manager/using/modify_asset_workflow.html)
>* Consulte el [Seminario web de preguntas a los expertos de AEM sobre flujos de trabajo](https://bit.ly/ATACE218).
>* Para ver un artículo completo de la comunidad, consulte [Creación de un participante dinámico personalizado de Adobe Experience Manager 6.3, paso](https://helpx.adobe.com/experience-manager/using/dynamic-steps-aem63.html).
>* Cambios en las ubicaciones de la información consulte [Reestructuración del repositorio en AEM 6.5](/help/sites-deploying/repository-restructuring.md) y [Prácticas recomendadas del flujo de trabajo - Ubicaciones](/help/sites-developing/workflows-best-practices.md#locations).

>


## Modelo {#model}

Un `WorkflowModel` representa una definición (modelo) de un flujo de trabajo. Está hecha de `WorkflowNodes` y `WorkflowTransitions`. Las transiciones conectan los nodos y definen el *flujo*. El modelo siempre tiene un nodo de inicio y un nodo final.

### Modelo de tiempo de ejecución {#runtime-model}

Los modelos de flujo de trabajo tienen versiones. Cuando ejecute una instancia de flujo de trabajo, utilizará (y mantendrá) el modelo de tiempo de ejecución del flujo de trabajo (como disponible en el momento en que se inició el flujo de trabajo).

Se genera un modelo de tiempo de ejecución [cuando **Sync** se activa en el editor de modelos de flujo de trabajo](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model).

Las ediciones al modelo de flujo de trabajo que se producen y/o los modelos de tiempo de ejecución que se generan, *después* de que se haya iniciado la instancia específica no se aplicarán a esa instancia.

>[!CAUTION]
>
>Los pasos realizados son los definidos por el [modelo de tiempo de ejecución](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model); esto se genera cuando se activa la acción **Sync** en el editor del modelo de flujo de trabajo.
>
>Si el modelo de flujo de trabajo se cambia después de este punto en el tiempo (sin activar **Sync**), la instancia de tiempo de ejecución no reflejará esos cambios. Solo los modelos de tiempo de ejecución generados después de la actualización reflejarán los cambios. Las excepciones son los scripts ECMA subyacentes, que se mantienen solo una vez que se realizan cambios en ellos.

### Etapa {#step}

Cada paso realiza una tarea discreta. Existen diferentes tipos de pasos de flujo de trabajo:

* Participante (usuario/grupo): Estos pasos generan un elemento de trabajo y lo asignan a un usuario o grupo. Un usuario debe completar el elemento de trabajo para avanzar en el flujo de trabajo.
* Proceso (Script, llamada de método Java): El sistema ejecuta automáticamente estos pasos. Una secuencia de comandos ECMA o una clase Java implementan el paso . Los servicios se pueden desarrollar para escuchar eventos de flujo de trabajo especiales y realizar tareas según la lógica empresarial.
* Contenedor (Subflujo de trabajo): Este tipo de paso inicia otro modelo de flujo de trabajo.
* O Dividir/Unir: Utilice la lógica para decidir qué paso ejecutar a continuación en el flujo de trabajo.
* Y Dividir/Unir: Permite ejecutar varios pasos simultáneamente.

Todos los pasos comparten las siguientes propiedades comunes: Alertas `Autoadvance` y `Timeout` (lista de comandos).

### Transición {#transition}

Un `WorkflowTransition` representa una transición entre dos `WorkflowNodes` de un `WorkflowModel`.

* Define el vínculo entre dos pasos consecutivos.
* Es posible aplicar reglas.

### WorkItem {#workitem}

Un `WorkItem` es la unidad que pasa a través de una instancia `Workflow` de un `WorkflowModel`. Contiene el `WorkflowData` en el que la instancia actúa y una referencia al `WorkflowNode` que describe el paso subyacente del flujo de trabajo.

* Se utiliza para identificar la tarea y se coloca en la bandeja de entrada correspondiente.
* Una instancia de flujo de trabajo puede tener una o varias `WorkItems` al mismo tiempo (según el modelo de flujo de trabajo).
* El `WorkItem` hace referencia a la instancia de flujo de trabajo.
* En el repositorio, el `WorkItem` se almacena debajo de la instancia de flujo de trabajo.

### Carga útil {#payload}

Hace referencia al recurso que debe avanzarse a través de un flujo de trabajo.

La implementación de carga útil hace referencia a un recurso en el repositorio (por ruta, UUID o URL) o por un objeto java serializado. Hacer referencia a un recurso en el repositorio es muy flexible y junto con sling es muy productivo; por ejemplo, el nodo al que se hace referencia se puede representar como un formulario.

### Ciclo de vida {#lifecycle}

Se crea al iniciar un nuevo flujo de trabajo (eligiendo el modelo de flujo de trabajo correspondiente y definiendo la carga útil) y finaliza cuando se procesa el nodo final.

Las siguientes acciones son posibles en una instancia de flujo de trabajo:

* Terminar
* Suspender
* Reanudar
* Reiniciar

Las instancias completadas y terminadas se archivan.

### Bandeja de entrada {#inbox}

Cada cuenta de usuario tiene su propia bandeja de entrada de flujo de trabajo en la que se puede acceder a la `WorkItems` asignada.

Los `WorkItems` se asignan a la cuenta de usuario directamente o al grupo al que pertenecen.

### Tipos de flujo de trabajo {#workflow-types}

Existen varios tipos de flujo de trabajo, como se indica en la consola Modelos de flujo de trabajo :

![wf-upgrade-03](assets/wf-upgraded-03.png)

* **Predeterminado**

   Estos son los flujos de trabajo listos para usar incluidos en una instancia de AEM estándar.

* Flujos de trabajo personalizados (sin indicador en la consola)

   Son flujos de trabajo que se han creado como nuevos o a partir de flujos de trabajo listos para usar que se han superpuesto con personalizaciones.

* **Heredado**

   Flujos de trabajo creados en una versión anterior de AEM. Se pueden conservar durante una actualización o exportar como paquete de flujo de trabajo desde la versión anterior y luego importarlos a la nueva versión.

### Flujos de trabajo transitorios {#transient-workflows}

Los flujos de trabajo estándar guardan información de tiempo de ejecución (historial) durante su ejecución. También puede definir un modelo de flujo de trabajo como **Transient** para evitar que dicho historial se mantenga. Se utiliza para ajustar el rendimiento, ya que ahorra o evita el tiempo o los recursos utilizados para mantener la información.

Los flujos de trabajo transitorios se pueden utilizar para cualquier flujo de trabajo que:

* se ejecutan a menudo.
* no necesitan el historial del flujo de trabajo.

Se introdujeron flujos de trabajo transitorios para cargar un gran número de recursos, donde la información de los recursos es importante, pero no el historial de tiempo de ejecución del flujo de trabajo.

>[!NOTE]
>
>Consulte [Creación de un flujo de trabajo transitorio](/help/sites-developing/workflows-models.md#creating-a-transient-workflow) para obtener más información.

>[!CAUTION]
>
>Cuando un modelo de flujo de trabajo se ha marcado como transitorio, existen algunos escenarios en los que la información de tiempo de ejecución se mantendrá:
>
>* El tipo de carga útil (por ejemplo, vídeo) requiere pasos externos para el procesamiento; en estos casos, el historial de tiempo de ejecución es necesario para la confirmación del estado.
>* El flujo de trabajo introduce una **AND Split**; en estos casos, el historial de tiempo de ejecución es necesario para la confirmación del estado.
>* Cuando el flujo de trabajo transitorio entra en un paso del participante, cambia de modo (durante la ejecución) a no transitorio; como la tarea se pasa a una persona, el historial debe conservarse

>


>[!CAUTION]
>
>Dentro de un flujo de trabajo transitorio no debe utilizar un **Goto Step**.
>
>Esto sucede cuando el **Goto Step** crea un trabajo de sling para continuar con el flujo de trabajo en el punto `goto`. Esto impide que el flujo de trabajo sea transitorio y genera un error en el archivo de registro.
>
>Para tomar decisiones en un flujo de trabajo transitorio, puede utilizar **OR Split**.

>[!NOTE]
>
>Consulte [Prácticas recomendadas para recursos](/help/assets/performance-tuning-guidelines.md#transient-workflows) para obtener más información sobre cómo afectan los flujos de trabajo transitorios al rendimiento de los recursos.

### Compatibilidad con varios recursos {#multi-resource-support}

Activar **Compatibilidad con varios recursos** para el modelo de flujo de trabajo significa que se iniciará una sola instancia de flujo de trabajo incluso cuando seleccione varios recursos; se adjuntarán como paquete.

Si **Compatibilidad con varios recursos** no está activada para el modelo de flujo de trabajo y se seleccionan varios recursos, se iniciará una instancia de flujo de trabajo individual para cada recurso.

>[!NOTE]
>
>Consulte [Configuración de un flujo de trabajo para compatibilidad con varios recursos](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) para obtener más información.

### Etapas del flujo de trabajo {#workflow-stages}

Las etapas del flujo de trabajo ayudan a visualizar el progreso de un flujo de trabajo al administrar tareas. Se pueden utilizar para proporcionar una descripción general de hasta dónde llega el flujo de trabajo a través del procesamiento, ya que cuando se ejecuta el flujo de trabajo, el usuario puede ver el progreso descrito por **Stage** (en lugar de los pasos individuales).

Como los nombres de paso individuales pueden ser específicos y técnicos, los nombres de escenario se pueden definir para proporcionar una vista conceptual del progreso del flujo de trabajo.

Por ejemplo, para un flujo de trabajo con seis pasos y cuatro etapas:

1. Puede [configurar las etapas del flujo de trabajo (que muestran el progreso del flujo de trabajo) y luego asignar la etapa adecuada a cada paso del flujo de trabajo](/help/sites-developing/workflows-models.md#configuring-workflow-stages-that-show-workflow-progress):

   * Se pueden crear varios nombres de escenario.
   * A continuación, se asigna un nombre de escenario individual a cada paso (se puede asignar un nombre de escenario a uno o varios pasos).

   | **Nombre del paso** | **Etapa (asignada al paso)** |
   |---|---|
   | Etapa 1 | Crear |
   | Etapa 2 | Crear |
   | Etapa 3 | Crítica |
   | Etapa 4 | Aprobar |
   | Etapa 5 | Completar |
   | Etapa 6 | Completar |

1. Cuando se ejecuta el flujo de trabajo, el usuario puede ver el progreso según los nombres de las fases (en lugar de los nombres de las etapas). El progreso del flujo de trabajo se muestra en la pestaña [WORKFLOW INFO de la ventana de detalles de la tarea del elemento de trabajo](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions) que aparece en la [Inbox](/help/sites-authoring/inbox.md).

### Flujos de trabajo y Forms {#workflows-and-forms}

Normalmente, los flujos de trabajo se utilizan para procesar los envíos de formularios en AEM. Esto puede suceder con los [componentes principales de los componentes de formulario](https://helpx.adobe.com/experience-manager/core-components/using/form-container.html) disponibles en una instancia de AEM estándar o con la [solución de AEM Forms](/help/forms/using/aem-forms-workflow.md).

Al crear un nuevo formulario, el envío del formulario puede asociarse fácilmente con un modelo de flujo de trabajo; por ejemplo, para almacenar el contenido en una ubicación concreta del repositorio o para notificar al usuario sobre el envío del formulario y su contenido.

### Flujos de trabajo y traducción {#workflows-and-translation}

Los flujos de trabajo también forman parte integral del proceso [Translation](/help/sites-administering/translation.md).
