---
title: Administración de flujos de trabajo
seo-title: Administering Workflows
description: Obtenga información sobre cómo administrar flujos de trabajo en AEM.
seo-description: Learn how to administer workflows in AEM.
uuid: d000a13c-97cb-4b1b-809e-6c3eb0d675e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 4b09cd44-434e-4834-bc0d-c9c082a4ba5a
exl-id: 10eecfb8-d43d-4f01-9778-87c752dee64c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 2%

---

# Administración de flujos de trabajo{#administering-workflows}

Los flujos de trabajo permiten automatizar las actividades de Adobe Experience Manager (AEM). Flujos de trabajo:

* Consiste en una serie de pasos que se ejecutan en un orden específico.

   * Cada paso realiza una actividad distinta; como esperar la entrada del usuario, activar una página o enviar un mensaje de correo electrónico.

* Puede interactuar con recursos en el repositorio, las cuentas de usuario y los servicios de AEM.
* Puede coordinar actividades complicadas que involucran cualquier aspecto de AEM.

Los procesos empresariales que ha establecido su organización pueden representarse como flujos de trabajo. Por ejemplo, el proceso de publicación del contenido de un sitio web suele incluir pasos como la aprobación y la desactivación por parte de varias partes interesadas. Estos procesos se pueden implementar como flujos de trabajo AEM y aplicar a páginas de contenido y recursos.

* [Inicio de flujos de trabajo](/help/sites-administering/workflows-starting.md)
* [Administración de instancias de flujo de trabajo](/help/sites-administering/workflows-administering.md)
* [Administración del acceso a los flujos de trabajo](/help/sites-administering/workflows-managing.md)

>[!NOTE]
>
>Para obtener más información, consulte lo siguiente:
>
>* Aplicación y participación en flujos de trabajo: [Uso de flujos de trabajo](/help/sites-authoring/workflows.md).
>* Creación de modelos de flujo de trabajo y ampliación de la funcionalidad del flujo de trabajo: [Desarrollo y ampliación de flujos de trabajo](/help/sites-developing/workflows.md).
>* Mejora del rendimiento de los flujos de trabajo que utilizan recursos de servidor significativos: [Procesamiento De Flujo De Trabajo Simultáneo](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing).
>


## Modelos e instancias de flujo de trabajo {#workflow-models-and-instances}

[Modelos de flujo de trabajo](/help/sites-developing/workflows.md#model) en AEM están la representación y la implementación de procesos empresariales:

* Normalmente actúan en páginas o recursos para obtener un resultado específico.
* Estas páginas o recursos se denominan carga útil de flujo de trabajo.
* Los modelos de flujo de trabajo constan de una serie de pasos que realizan una tarea específica.
* La carga útil se pasa de un paso a otro a medida que progresa el flujo de trabajo.

Cuando se inicia (se ejecuta) un modelo de flujo de trabajo, se crea una instancia de flujo de trabajo. Un modelo de flujo de trabajo se puede iniciar varias veces, cada vez que se genera una instancia de flujo de trabajo distinta. Para cada instancia, se ejecutan los pasos que define el modelo de flujo de trabajo.

>[!CAUTION]
>
>Los pasos realizados son los definidos por el modelo de flujo de trabajo *en el momento en que se genera la instancia*. Consulte [Desarrollo de flujos de trabajo](/help/sites-developing/workflows.md#model) para obtener más información.

Las instancias de flujo de trabajo progresan durante el siguiente ciclo vital:

1. Se inicia el modelo de flujo de trabajo y se crea y se ejecuta una instancia de flujo de trabajo.

   1. La carga útil de la instancia de flujo de trabajo se identifica cuando se inicia el modelo.
   1. La instancia es en realidad una copia del modelo (al momento de la creación).
   1. AEM autores, administradores o servicios pueden iniciar modelos de flujo de trabajo.

1. Se ejecuta el primer paso del modelo de flujo de trabajo.
1. El paso se completa y el motor de flujo de trabajo utiliza el modelo para determinar el paso siguiente que se va a ejecutar.
1. Los pasos siguientes del modelo de flujo de trabajo se ejecutan y completan.
1. Cuando se completa el paso final, la instancia del flujo de trabajo se completa y, por lo tanto, se archiva.

Se proporcionan muchos modelos de flujo de trabajo útiles con AEM. Además, los desarrolladores de su organización pueden crear modelos de flujo de trabajo personalizados, adaptados a las necesidades específicas de sus procesos empresariales.

## Pasos del flujo de trabajo {#workflow-steps}

Cuando se ejecutan los pasos del flujo de trabajo, se asocian a una instancia de flujo de trabajo. El historial de una instancia de flujo de trabajo incluye información sobre cada paso que se ha ejecutado para la instancia. Esta información es útil para investigar los problemas que se producen durante la ejecución.

Un usuario o un servicio realizan pasos de flujo de trabajo según el tipo de paso:

* Cuando un usuario realiza un paso, se le asigna un elemento de trabajo que se coloca en su Bandeja de entrada. El usuario es responsable de completar manualmente el paso para que la instancia de flujo de trabajo progrese.
* Cuando un servicio realiza un paso, una vez finalizada, la instancia del flujo de trabajo progresa automáticamente al siguiente paso.

>[!NOTE]
>
>Si se produce un error, la implementación de servicio/paso debe controlar el comportamiento de un escenario de error. El propio motor de flujo de trabajo reintentará el trabajo, luego registrará un error y detendrá la instancia.

## Estado y acciones del flujo de trabajo {#workflow-status-and-actions}

Un flujo de trabajo puede tener uno de los siguientes estados:

* **EJECUCIÓN**: La instancia de flujo de trabajo se está ejecutando.
* **FINALIZADO**: La instancia de flujo de trabajo se ha finalizado correctamente.

* **SUSPENDIDO**: Marca el flujo de trabajo como suspendido. Sin embargo, consulte la nota de precaución a continuación sobre un problema conocido con este estado.
* **ABORTED**: La instancia de flujo de trabajo se ha finalizado.
* **STALE**: La progresión de la instancia de flujo de trabajo requiere que se ejecute un trabajo en segundo plano, pero el trabajo no se puede encontrar en el sistema. Esta situación puede producirse cuando se produce un error al ejecutar el flujo de trabajo.

>[!NOTE]
>
>Cuando la ejecución de un paso de proceso resulta en errores, el paso aparece en la bandeja de entrada del administrador y el estado del flujo de trabajo es **EJECUCIÓN**.

Según el estado actual, puede realizar acciones en la ejecución de instancias de flujo de trabajo cuando necesite intervenir en la progresión normal de una instancia de flujo de trabajo:

* **Suspender**: Suspender cambia el estado del flujo de trabajo a Suspendido. Consulte Precaución a continuación:

>[!CAUTION]
>
>Marcar un estado de flujo de trabajo como &quot;Suspender&quot; tiene un problema conocido. En este estado es posible realizar acciones en elementos de flujo de trabajo suspendidos en una bandeja de entrada.

* **Reanudar**: Reinicia un flujo de trabajo suspendido en el mismo punto de ejecución en el que se suspendió, utilizando la misma configuración.
* **Finalizar**: Finaliza la ejecución del flujo de trabajo y cambia el estado a **ABORTED**. No se puede reiniciar una instancia de flujo de trabajo anulada.
