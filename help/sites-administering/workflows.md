---
title: Administración de Flujos de trabajo
seo-title: Administración de Flujos de trabajo
description: Aprenda a administrar flujos de trabajo en AEM.
seo-description: Aprenda a administrar flujos de trabajo en AEM.
uuid: d000a13c-97cb-4b1b-809e-6c3eb0d675e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 4b09cd44-434e-4834-bc0d-c9c082a4ba5a
translation-type: tm+mt
source-git-commit: 5a99daa208d1d109d2736525fdca3accdcfb4dd1
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---


# Administración de Flujos de trabajo{#administering-workflows}

Los flujos de trabajo le permiten automatizar actividades de Adobe Experience Manager (AEM). Flujos de trabajo:

* Consiste en una serie de pasos que se ejecutan en un orden específico.

   * Cada paso realiza una actividad distinta; como esperar la entrada del usuario, activar una página o enviar un mensaje de correo electrónico.

* Puede interactuar con los recursos del repositorio, las cuentas de usuario y los servicios de AEM.
* Puede coordinar actividades complicadas que involucran cualquier aspecto de AEM.

Los procesos comerciales que su organización ha establecido pueden representarse como flujos de trabajo. Por ejemplo: el proceso de publicación de contenido del sitio Web generalmente incluye pasos como la aprobación y la aprobación por parte de varios interesados. Estos procesos se pueden implementar como flujos de trabajo AEM y aplicar a páginas de contenido y recursos.

* [Inicio de Flujos de trabajo](/help/sites-administering/workflows-starting.md)
* [Administración de instancias de flujo de trabajo](/help/sites-administering/workflows-administering.md)
* [Administración del acceso a los Flujos de trabajo](/help/sites-administering/workflows-managing.md)

>[!NOTE]
>
>Para obtener más información, consulte:
>
>* Aplicación y participación en flujos de trabajo: [Trabajar con Flujos de trabajo](/help/sites-authoring/workflows.md).
>* Creación de modelos de flujo de trabajo y ampliación de la funcionalidad de flujo de trabajo: [Desarrollar y ampliar Flujos de trabajo](/help/sites-developing/workflows.md).
>* Mejora del rendimiento de los flujos de trabajo que utilizan recursos importantes del servidor: [Procesamiento simultáneo del flujo de trabajo](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing).

>



## Modelos e instancias de flujo de trabajo {#workflow-models-and-instances}

[Los ](/help/sites-developing/workflows.md#model) modelos de flujo de trabajo de AEM son la representación y la implementación de procesos comerciales:

* Generalmente actúan en páginas o recursos para lograr un resultado específico.
* Estas páginas o recursos se denominan carga útil de flujo de trabajo.
* Los modelos de flujo de trabajo constan de una serie de pasos que realizan una tarea específica.
* La carga útil se pasa de un paso a otro a medida que avanza el flujo de trabajo.

Cuando se inicia (ejecuta) un modelo de flujo de trabajo, se crea una instancia de flujo de trabajo. Un modelo de flujo de trabajo se puede iniciar varias veces, cada vez que se genera una instancia de flujo de trabajo distinta. Se ejecutan los pasos que define el modelo de flujo de trabajo para cada instancia.

>[!CAUTION]
>
>Los pasos realizados son los definidos por el modelo de flujo de trabajo *en el momento en que se genera la instancia*. Consulte [Desarrollo de Flujos de trabajo](/help/sites-developing/workflows.md#model) para obtener más detalles.

Las instancias de flujo de trabajo progresan a través del siguiente ciclo de vida:

1. Se inicia el modelo de flujo de trabajo y se crea y ejecuta una instancia de flujo de trabajo.

   1. La carga útil de la instancia de flujo de trabajo se identifica cuando se inicia el modelo.
   1. La instancia es efectivamente una copia del modelo (al momento de la creación).
   1. Los autores, administradores o servicios de AEM pueden crear modelos de flujo de trabajo de inicio.

1. Se ejecuta el primer paso del modelo de flujo de trabajo.
1. El paso se completa y el motor de flujos de trabajo utiliza el modelo para determinar el siguiente paso que se va a ejecutar.
1. Los pasos subsiguientes del modelo de flujo de trabajo se ejecutan y completan.
1. Cuando se completa el paso final, la instancia del flujo de trabajo se completa y, por lo tanto, se archiva.

Se proporcionan muchos modelos de flujo de trabajo útiles con AEM. Además, los desarrolladores de su organización pueden crear modelos de flujo de trabajo personalizados, adaptados a las necesidades específicas de sus procesos empresariales.

## Pasos del flujo de trabajo {#workflow-steps}

Cuando se ejecutan los pasos del flujo de trabajo, se asocian con una instancia de flujo de trabajo. El historial de una instancia de flujo de trabajo incluye información sobre cada paso que se ha ejecutado para la instancia. Esta información es útil para investigar los problemas que se producen durante la ejecución.

Un usuario o un servicio realiza pasos de flujo de trabajo, según el tipo de paso:

* Cuando un usuario realiza un paso, se le asigna un elemento de trabajo que se coloca en su Bandeja de entrada. El usuario es responsable de completar manualmente el paso para que la instancia de flujo de trabajo avance.
* Cuando un servicio realiza un paso, una vez finalizada la instancia de flujo de trabajo avanza automáticamente al paso siguiente.

>[!NOTE]
>
>Si se produce un error, la implementación de servicio/paso debe controlar el comportamiento de un escenario de error. El propio motor de flujos de trabajo volverá a intentar el trabajo y, a continuación, registrará un error y detendrá la instancia.

## Estado y acciones del flujo de trabajo {#workflow-status-and-actions}

Un flujo de trabajo puede tener uno de los siguientes estados:

* **EJECUTANDO**: La instancia de flujo de trabajo se está ejecutando.
* **COMPLETADO**: La instancia de flujo de trabajo ha finalizado correctamente.

* **SUSPENDIDO**: Marca el flujo de trabajo como suspendido. Sin embargo, consulte la nota de advertencia siguiente sobre un problema conocido con este estado.
* **ABORTADO**: La instancia de flujo de trabajo ha finalizado.
* **ESTILO**: La progresión de la instancia de flujo de trabajo requiere que se ejecute un trabajo en segundo plano, pero el trabajo no se puede encontrar en el sistema. Esta situación puede producirse cuando se produce un error al ejecutar el flujo de trabajo.

>[!NOTE]
>
>Cuando la ejecución de un paso de proceso produce errores, el paso aparece en la Bandeja de entrada del administrador y el estado del flujo de trabajo es **EJECUTANDO**.

Según el estado actual, puede realizar acciones en las instancias de flujo de trabajo en ejecución cuando necesite intervenir en la progresión normal de una instancia de flujo de trabajo:

* **Suspender**: La suspensión cambia el estado del flujo de trabajo a Suspendido. Consulte Precaución a continuación:

>[!CAUTION]
>
>Marcar un estado de flujo de trabajo como &quot;Suspender&quot; tiene un problema conocido. En este estado, es posible realizar acciones en elementos de flujo de trabajo suspendidos en una Bandeja de entrada.

* **Reanudar**: Reinicia un flujo de trabajo suspendido en el mismo punto de ejecución en el que se suspendió, utilizando la misma configuración.
* **Finalizar**: Finaliza la ejecución del flujo de trabajo y cambia el estado a  **ABORTED**. No se puede reiniciar una instancia de flujo de trabajo anulada.

