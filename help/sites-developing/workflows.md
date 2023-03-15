---
title: Desarrollo y ampliación de flujos de trabajo
seo-title: Developing and Extending Workflows
description: AEM proporciona varias herramientas y recursos para crear modelos de flujo de trabajo, desarrollar pasos de flujo de trabajo y para interactuar mediante programación con flujos de trabajo
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

AEM proporciona varias herramientas y recursos para crear modelos de flujo de trabajo, desarrollar pasos de flujo de trabajo y para interactuar mediante programación con flujos de trabajo.

AEM Los flujos de trabajo permiten automatizar los procesos para administrar recursos y publicar contenido en el entorno de la. Los flujos de trabajo se componen de una serie de pasos, en los que cada paso realiza una tarea discreta. Puede utilizar la lógica y los datos de tiempo de ejecución para tomar decisiones sobre cuándo puede continuar un proceso y seleccionar el siguiente paso de uno de los múltiples pasos posibles.

Por ejemplo, los procesos empresariales para crear y publicar páginas web incluyen tareas de aprobación y firma de varios participantes. AEM Estos procesos se pueden modelar mediante flujos de trabajo de la y aplicarse a contenido específico.

Los aspectos clave se tratan a continuación, mientras que las siguientes páginas tratan más detalles:

* [Creación de modelos de flujo de trabajo](/help/sites-developing/workflows-models.md)
* [Ampliación de la funcionalidad del flujo de trabajo](/help/sites-developing/workflows-customizing-extending.md)
* [Interactuar con flujos de trabajo mediante programación](/help/sites-developing/workflows-program-interaction.md)
* [Referencia de pasos de flujo de trabajo](/help/sites-developing/workflows-step-ref.md)
* [Referencia del proceso de flujo de trabajo](/help/sites-developing/workflows-process-ref.md)
* [Prácticas recomendadas de flujo de trabajo](/help/sites-developing/workflows-best-practices.md)

>[!NOTE]
>
>Para obtener información acerca de:
>
>* Participación en flujos de trabajo, consulte [Uso de flujos de trabajo](/help/sites-authoring/workflows.md).
>* Administración de flujos de trabajo e instancias de flujo de trabajo, consulte [Administración de flujos de trabajo](/help/sites-administering/workflows.md).
>* Para ver un artículo completo de la comunidad, consulte [Modificación de recursos digitales mediante flujos de trabajo de Adobe Experience Manager.](https://helpx.adobe.com/experience-manager/using/modify_asset_workflow.html)
>* Consulte la [AEM Seminario web para expertos de Adobe sobre flujos de trabajo](https://bit.ly/ATACE218).
>* Para ver un artículo completo de la comunidad, consulte [Creación de un paso de participante dinámico de Adobe Experience Manager 6.3 personalizado](https://helpx.adobe.com/experience-manager/using/dynamic-steps-aem63.html).
>* Cambios en las ubicaciones de la información consulte [AEM Reestructuración de repositorios en 6.5](/help/sites-deploying/repository-restructuring.md) y [Prácticas recomendadas de flujo de trabajo: ubicaciones](/help/sites-developing/workflows-best-practices.md#locations).
>


## Modelo {#model}

A `WorkflowModel` representa una definición (modelo) de un flujo de trabajo. Está hecho de `WorkflowNodes` y `WorkflowTransitions`. Las transiciones conectan los nodos y definen el *fluir*. El modelo siempre tiene un nodo de inicio y un nodo de finalización.

### Modelo Runtime {#runtime-model}

Los modelos de flujo de trabajo tienen versiones. Al ejecutar una instancia de flujo de trabajo, se utiliza (y se mantiene) el modelo de tiempo de ejecución del flujo de trabajo (tal y como estaba disponible en el momento en que se inició el flujo de trabajo).

Un modelo de tiempo de ejecución es [generado al **Sincronización** se activa en el editor del modelo de flujo de trabajo](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model).

Ediciones en el modelo de flujo de trabajo que se producen y/o modelos de tiempo de ejecución que se generan. *después* la instancia específica que se inició no se aplicará a esa instancia.

>[!CAUTION]
>
>Los pasos realizados son los definidos por la variable [modelo de tiempo de ejecución](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model); esto se genera en el momento en que **Sincronización** la acción se activa en el editor del modelo de flujo de trabajo.
>
>Si el modelo de flujo de trabajo se cambia después de este punto temporal (sin **Sincronización** se está activando), la instancia de tiempo de ejecución no reflejará esos cambios. Solo los modelos en tiempo de ejecución generados después de la actualización reflejarán los cambios. Las excepciones son los scripts ECMA subyacentes, que se conservan una sola vez para que se realicen los cambios correspondientes.

### Paso {#step}

Cada paso realiza una tarea discreta. Existen diferentes tipos de pasos del flujo de trabajo:

* Participante (usuario/grupo): estos pasos generan un elemento de trabajo y lo asignan a un usuario o grupo. Un usuario debe completar el elemento de trabajo para avanzar en el flujo de trabajo.
* Process (Script, llamada de método Java): el sistema ejecuta estos pasos automáticamente. Un script ECMA o una clase Java implementan el paso. Los servicios se pueden desarrollar para escuchar eventos de flujo de trabajo especiales y realizar tareas según la lógica empresarial.
* Contenedor (subflujo de trabajo): este tipo de paso inicia otro modelo de flujo de trabajo.
* OR Split/Join: utilice la lógica para decidir qué paso ejecutar en el flujo de trabajo.
* División/unión AND: permite ejecutar varios pasos simultáneamente.

Todos los pasos comparten las siguientes propiedades comunes: `Autoadvance` y `Timeout` alertas (con scripts).

### Transición {#transition}

A `WorkflowTransition` representa una transición entre dos `WorkflowNodes` de a `WorkflowModel`.

* Define el vínculo entre dos pasos consecutivos.
* Es posible aplicar reglas.

### WorkItem {#workitem}

A `WorkItem` es la unidad que pasa a través de un `Workflow` instancia de a `WorkflowModel`. Contiene el `WorkflowData` que la instancia actúa en y una referencia a `WorkflowNode` que describe el paso de flujo de trabajo subyacente.

* Se utiliza para identificar la tarea y se coloca en la bandeja de entrada correspondiente.
* Una instancia de flujo de trabajo puede tener una o varias `WorkItems` al mismo tiempo (según el modelo de flujo de trabajo).
* El `WorkItem` hace referencia a la instancia de flujo de trabajo.
* En el repositorio, la variable `WorkItem` se almacena debajo de la instancia de flujo de trabajo.

### Carga útil {#payload}

Hace referencia al recurso que debe avanzarse a través de un flujo de trabajo.

La implementación de carga útil hace referencia a un recurso del repositorio (por ruta, UUID o URL) o por un objeto java serializado. La referencia a un recurso en el repositorio es muy flexible y, junto con sling, muy productiva; por ejemplo, el nodo al que se hace referencia podría representarse como un formulario.

### Ciclo de vida {#lifecycle}

Se crea al iniciar un nuevo flujo de trabajo (seleccionando el modelo de flujo de trabajo correspondiente y definiendo la carga útil) y finaliza cuando se procesa el nodo final.

Las siguientes acciones son posibles en una instancia de flujo de trabajo:

* Terminar
* Suspender
* Reanudar
* Reiniciar

Se archivan las instancias completadas y terminadas.

### Bandeja de entrada {#inbox}

Cada cuenta de usuario tiene su propia bandeja de entrada de flujo de trabajo en la que se asigna el elemento `WorkItems` son accesibles.

El `WorkItems` se asignan a la cuenta de usuario directamente o al grupo al que pertenecen.

### Tipos de flujo de trabajo {#workflow-types}

Existen varios tipos de flujo de trabajo como se indica en la consola Modelos de flujo de trabajo:

![wf-actualizado-03](assets/wf-upgraded-03.png)

* **Predeterminado**

   AEM Estos son los flujos de trabajo listos para usar incluidos en una instancia de estándar.

* Flujos de trabajo personalizados (sin indicador en la consola)

   Son flujos de trabajo que se han creado como nuevos o a partir de flujos de trabajo predeterminados que se han superpuesto con las personalizaciones.

* **Heredado**

   AEM Flujos de trabajo creados en una versión anterior de. Se pueden retener durante una actualización o exportarse como un paquete de flujo de trabajo de la versión anterior y, a continuación, importarse en la nueva versión.

### Flujos de trabajo transitorios {#transient-workflows}

Los flujos de trabajo estándar guardan la información de tiempo de ejecución (historial) durante su ejecución. También puede definir un modelo de flujo de trabajo como **Transitorio** para evitar que dicho historial se mantenga. Se utiliza para ajustar el rendimiento, ya que ahorra/evita el tiempo/recursos utilizados para mantener la información.

Los flujos de trabajo transitorios se pueden utilizar para cualquier flujo de trabajo que:

* se ejecutan a menudo.
* no necesita el historial del flujo de trabajo.

Se han introducido flujos de trabajo transitorios para cargar un gran número de recursos, donde la información del recurso es importante, pero no el historial de tiempo de ejecución del flujo de trabajo.

>[!NOTE]
>
>Consulte [Creación de un flujo de trabajo transitorio](/help/sites-developing/workflows-models.md#creating-a-transient-workflow) para obtener más información.

>[!CAUTION]
>
>Cuando un modelo de flujo de trabajo se ha marcado como Transitorio, hay algunos escenarios en los que la información de tiempo de ejecución se mantendrá:
>
>* El tipo de carga útil (por ejemplo, vídeo) requiere pasos externos para el procesamiento; en estos casos, el historial de tiempo de ejecución es necesario para la confirmación de estado.
>* El flujo de trabajo introduce un **División Y**; en estos casos, el historial de tiempo de ejecución es necesario para la confirmación de estado.
>* Cuando el flujo de trabajo transitorio introduce un paso de participante, cambia de modo (en tiempo de ejecución) a no transitorio; como la tarea se pasa a una persona, es necesario mantener el historial
>


>[!CAUTION]
>
>Dentro de un flujo de trabajo transitorio, no debe utilizar un **Paso Ir a**.
>
>Esto es como el **Paso Ir a** crea un trabajo de sling para continuar el flujo de trabajo en la `goto` punto. Esto no cumple el propósito de hacer que el flujo de trabajo sea transitorio y genera un error en el archivo de registro.
>
>Para tomar decisiones en un flujo de trabajo transitorio, puede utilizar el **División O**.

>[!NOTE]
>
>Consulte [Prácticas recomendadas para Assets](/help/assets/performance-tuning-guidelines.md#transient-workflows) para obtener más información sobre cómo afectan los flujos de trabajo transitorios al rendimiento de los recursos.

### Compatibilidad con varios recursos {#multi-resource-support}

Activando **Compatibilidad con varios recursos** para el modelo de flujo de trabajo significa que se iniciará una única instancia de flujo de trabajo incluso cuando seleccione varios recursos; estos se adjuntarán como un paquete.

If **Compatibilidad con varios recursos** no está activada para el modelo de flujo de trabajo y se han seleccionado varios recursos, por lo que se iniciará una instancia de flujo de trabajo individual para cada recurso.

>[!NOTE]
>
>Consulte [Configuración de un flujo de trabajo para la compatibilidad con varios recursos](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) para obtener más información.

### Fases del flujo de trabajo {#workflow-stages}

Las fases del flujo de trabajo ayudan a visualizar el progreso de un flujo de trabajo al administrar tareas. Se pueden utilizar para proporcionar una visión general de hasta dónde llega el flujo de trabajo a través del procesamiento, ya que cuando se ejecuta el flujo de trabajo, el usuario puede ver el progreso descrito por **Fase** (a diferencia de los pasos individuales).

Como los nombres de paso individuales pueden ser específicos y técnicos, los nombres de fase se pueden definir para proporcionar una vista conceptual del progreso del flujo de trabajo.

Por ejemplo, para un flujo de trabajo con seis pasos y cuatro fases:

1. Puede [Configure las fases del flujo de trabajo (que muestran el progreso del flujo de trabajo) y luego asigne la fase adecuada a cada paso del flujo de trabajo](/help/sites-developing/workflows-models.md#configuring-workflow-stages-that-show-workflow-progress):

   * Se pueden crear varios nombres de fase.
   * A continuación, se asigna un nombre de etapa individual a cada paso (se puede asignar un nombre de etapa a uno o más pasos).

   | **Nombre del paso** | **Fase (asignada a la etapa)** |
   |---|---|
   | Etapa 1 | Crear |
   | Etapa 2 | Crear |
   | Etapa 3 | Revisión |
   | Etapa 4 | Aprobar |
   | Etapa 5 | Completar |
   | Etapa 6 | Completar |

1. Cuando se ejecuta el flujo de trabajo, el usuario puede ver el progreso según los nombres de las fases (en lugar de los nombres de las fases). El progreso del flujo de trabajo se muestra en la [Pestaña INFORMACIÓN DEL FLUJO DE TRABAJO de la ventana de detalles de tarea del elemento de trabajo](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions) enumerados en la [Bandeja de entrada](/help/sites-authoring/inbox.md).

### Flujos de trabajo y Forms {#workflows-and-forms}

AEM Normalmente, los flujos de trabajo se utilizan para procesar los envíos de formularios en la. Esto puede ser con el [componentes principales de componentes de formulario](https://helpx.adobe.com/experience-manager/core-components/using/form-container.html) AEM disponible en una instancia de estándar o con [solución de AEM Forms](/help/forms/using/aem-forms-workflow.md).

Al crear un nuevo formulario, el envío del formulario se puede asociar fácilmente a un modelo de flujo de trabajo; por ejemplo, para almacenar el contenido en una ubicación concreta del repositorio o para notificar a un usuario el envío del formulario y su contenido.

### Flujos de trabajo y traducción {#workflows-and-translation}

Los flujos de trabajo también forman parte integral de [Traducción](/help/sites-administering/translation.md) proceso.
