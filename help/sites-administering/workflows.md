---
title: Administración de flujos de trabajo
seo-title: Administering Workflows
description: AEM Obtenga información sobre cómo administrar flujos de trabajo de en la.
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

Los flujos de trabajo permiten automatizar las actividades de Adobe Experience Manager AEM (). Flujos de trabajo:

* Consiste en una serie de pasos que se ejecutan en un orden específico.

   * Cada paso realiza una actividad distinta, como esperar los datos introducidos por el usuario, activar una página o enviar un mensaje de correo electrónico.

* AEM Puede interactuar con recursos del repositorio, cuentas de usuario y servicios de.
* AEM Puede coordinar actividades complicadas que implican cualquier aspecto de la.

Los procesos empresariales que ha establecido su organización se pueden representar como flujos de trabajo. Por ejemplo, el proceso de publicación de contenido del sitio web suele incluir pasos como la aprobación y la aprobación por parte de varias partes interesadas. AEM Estos procesos se pueden implementar como flujos de trabajo de y aplicarse a páginas de contenido y recursos.

* [Inicio de flujos de trabajo](/help/sites-administering/workflows-starting.md)
* [Administración de instancias de flujo de trabajo](/help/sites-administering/workflows-administering.md)
* [Administración del acceso a los flujos de trabajo](/help/sites-administering/workflows-managing.md)

>[!NOTE]
>
>Para obtener más información, consulte lo siguiente:
>
>* Aplicación y participación en flujos de trabajo: [Uso de flujos de trabajo](/help/sites-authoring/workflows.md).
>* Creación de modelos de flujo de trabajo y ampliación de funciones de flujo de trabajo: [Desarrollo y ampliación de flujos de trabajo](/help/sites-developing/workflows.md).
>* Mejora del rendimiento de los flujos de trabajo que utilizan recursos de servidor significativos: [Procesamiento de flujo de trabajo simultáneo](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing).
>


## Modelos de flujo de trabajo e instancias {#workflow-models-and-instances}

[Modelos de flujo de trabajo](/help/sites-developing/workflows.md#model) AEM en los que se encuentran los procesos de representación e implementación de los negocios:

* Normalmente, actúan en páginas o recursos para lograr un resultado específico.
* Estas páginas o activos se denominan carga útil de flujo de trabajo.
* Los modelos de flujo de trabajo constan de una serie de pasos que realizan una tarea específica.
* La carga útil se pasa de paso en paso a medida que progresa el flujo de trabajo.

Cuando se inicia (ejecuta) un modelo del flujo de trabajo, se crea una instancia de flujo de trabajo. Un modelo de flujo de trabajo se puede iniciar varias veces, cada una de las cuales genera una instancia de flujo de trabajo distinta. Para cada instancia, se ejecutan los pasos que define el modelo de flujo de trabajo.

>[!CAUTION]
>
>Los pasos realizados son los definidos por el modelo de flujo de trabajo *en el momento de generar la instancia*. Consulte [Desarrollo de flujos de trabajo](/help/sites-developing/workflows.md#model) para obtener más información.

Las instancias de flujo de trabajo progresan a través del siguiente ciclo vital:

1. El modelo de flujo de trabajo se inicia, y se crea y ejecuta una instancia de flujo de trabajo.

   1. La carga útil de la instancia de flujo de trabajo se identifica cuando se inicia el modelo.
   1. La instancia es en realidad una copia del modelo (en el momento de su creación).
   1. AEM Los autores, administradores o servicios de pueden iniciar modelos de flujo de trabajo.

1. Se ejecuta el primer paso del modelo del flujo de trabajo.
1. El paso se completa y el motor de flujo de trabajo utiliza el modelo para determinar el siguiente paso que se va a ejecutar.
1. Los pasos siguientes del modelo de flujo de trabajo se ejecutan y finalizan.
1. Cuando se completa el paso final, la instancia de flujo de trabajo se completa y, por lo tanto, se archiva.

AEM Muchos modelos de flujo de trabajo útiles se proporcionan con la opción de trabajo Además, los desarrolladores de su organización pueden crear modelos de flujo de trabajo personalizados, adaptados a las necesidades específicas de los procesos empresariales.

## Pasos del flujo de trabajo {#workflow-steps}

Cuando se ejecutan pasos del flujo de trabajo, se asocian a una instancia de flujo de trabajo. El historial de una instancia de flujo de trabajo incluye información sobre cada paso que se ha ejecutado para la instancia. Esta información resulta útil para investigar los problemas que se producen durante la ejecución.

Un usuario o un servicio realizan pasos del flujo de trabajo según el tipo de paso:

* Cuando un usuario realiza un paso, se le asigna un elemento de trabajo que se coloca en su bandeja de entrada. El usuario es responsable de completar manualmente el paso para que la instancia del flujo de trabajo progrese.
* Cuando un servicio realiza una etapa, al completarse, la instancia de flujo de trabajo progresa automáticamente a la etapa siguiente.

>[!NOTE]
>
>Si se produce un error, la implementación del servicio/paso debe gestionar el comportamiento para un escenario de error. El motor de flujo de trabajo en sí reintentará el trabajo, registrará un error y detendrá la instancia.

## Estado y acciones del flujo de trabajo {#workflow-status-and-actions}

Un flujo de trabajo puede tener uno de los siguientes estados:

* **EN EJECUCIÓN**: la instancia del flujo de trabajo se está ejecutando.
* **COMPLETADO**: la instancia del flujo de trabajo se ha finalizado correctamente.

* **SUSPENDIDO**: marca el flujo de trabajo como suspendido. Sin embargo, consulte la nota de precaución siguiente sobre un problema conocido con este estado.
* **ANULADO**: se ha finalizado la instancia del flujo de trabajo.
* **ANTICUADO**: el progreso de la instancia de flujo de trabajo requiere que se ejecute un trabajo en segundo plano, pero el trabajo no se puede encontrar en el sistema. Esta situación se puede producir cuando se produce un error al ejecutar el flujo de trabajo.

>[!NOTE]
>
>Cuando la ejecución de un paso de proceso genera errores, el paso aparece en la bandeja de entrada del administrador y el estado del flujo de trabajo es **EN EJECUCIÓN**.

Según el estado actual, puede realizar acciones en instancias de flujo de trabajo en ejecución cuando necesite intervenir en la progresión normal de una instancia de flujo de trabajo:

* **Suspender**: Suspender cambia el estado del flujo de trabajo a Suspendido. Consulte Precaución a continuación:

>[!CAUTION]
>
>Marcar el estado de un flujo de trabajo como &quot;Suspender&quot; tiene un problema conocido. En este estado es posible realizar acciones en elementos de flujo de trabajo suspendidos en una bandeja de entrada.

* **Reanudar**: reinicia un flujo de trabajo suspendido en el mismo punto de ejecución en el que se suspendió, utilizando la misma configuración.
* **Finalizar**: finaliza la ejecución del flujo de trabajo y cambia el estado a **ANULADO**. No se puede reiniciar una instancia de flujo de trabajo anulada.
