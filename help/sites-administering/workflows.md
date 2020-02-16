---
title: Administración de flujos de trabajo
seo-title: Administración de flujos de trabajo
description: Obtenga información sobre cómo administrar flujos de trabajo en AEM.
seo-description: Obtenga información sobre cómo administrar flujos de trabajo en AEM.
uuid: d000a13c-97cb-4b1b-809e-6c3eb0d675e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 4b09cd44-434e-4834-bc0d-c9c082a4ba5a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Administración de flujos de trabajo{#administering-workflows}

Los flujos de trabajo le permiten automatizar las actividades de Adobe Experience Manager (AEM). Flujos de trabajo:

* Consiste en una serie de pasos que se ejecutan en un orden específico.

   * Cada paso realiza una actividad distinta; como esperar la entrada del usuario, activar una página o enviar un mensaje de correo electrónico.

* Puede interactuar con recursos del repositorio, las cuentas de usuario y los servicios de AEM.
* Puede coordinar actividades complicadas que involucran cualquier aspecto de AEM.

Los procesos empresariales que ha establecido su organización pueden representarse como flujos de trabajo. Por ejemplo: el proceso de publicación de contenido del sitio Web generalmente incluye pasos como la aprobación y la aprobación por parte de varios interesados. Estos procesos pueden implementarse como flujos de trabajo de AEM y aplicarse a páginas de contenido y recursos.

* [Iniciando flujos de trabajo](/help/sites-administering/workflows-starting.md)
* [Administración de instancias de flujo de trabajo](/help/sites-administering/workflows-administering.md)
* [Administración del acceso a los flujos de trabajo](/help/sites-administering/workflows-managing.md)

>[!NOTE]
>
>Para obtener más información, consulte:
>
>* Aplicación y participación en flujos de trabajo: [Uso de flujos de trabajo](/help/sites-authoring/workflows.md).
>* Creación de modelos de flujo de trabajo y ampliación de la funcionalidad de flujo de trabajo: [Desarrollo y ampliación de flujos de trabajo](/help/sites-developing/workflows.md).
>* Mejora del rendimiento de los flujos de trabajo que utilizan recursos importantes del servidor: Procesamiento [simultáneo de flujo de trabajo](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing).
>



## Modelos e instancias de flujo de trabajo {#workflow-models-and-instances}

[Los modelos](/help/sites-developing/workflows.md#model) de flujo de trabajo de AEM son la representación e implementación de procesos empresariales:

* Generalmente actúan en páginas o recursos para lograr un resultado específico.
* Estas páginas o recursos se denominan carga útil de flujo de trabajo.
* Los modelos de flujo de trabajo constan de una serie de pasos que realizan una tarea específica.
* La carga útil se pasa de un paso a otro a medida que avanza el flujo de trabajo.

Cuando se inicia (ejecuta) un modelo de flujo de trabajo, se crea una instancia de flujo de trabajo. Un modelo de flujo de trabajo se puede iniciar varias veces, cada vez que se genera una instancia de flujo de trabajo distinta. Se ejecutan los pasos que define el modelo de flujo de trabajo para cada instancia.

>[!CAUTION]
>
>Los pasos realizados son los definidos por el modelo de flujo de trabajo *en el momento en que se genera* la instancia. Consulte [Desarrollo de flujos de trabajo](/help/sites-developing/workflows.md#model) para obtener más detalles.

Las instancias de flujo de trabajo progresan a través del siguiente ciclo de vida:

1. Se inicia el modelo de flujo de trabajo y se crea y ejecuta una instancia de flujo de trabajo.

   1. La carga útil de la instancia de flujo de trabajo se identifica cuando se inicia el modelo.
   1. La instancia es efectivamente una copia del modelo (al momento de la creación).
   1. Los autores, administradores o servicios de AEM pueden iniciar modelos de flujo de trabajo.

1. Se ejecuta el primer paso del modelo de flujo de trabajo.
1. El paso se ha completado y el motor de flujo de trabajo utiliza el modelo para determinar el paso siguiente que se va a ejecutar.
1. Los pasos subsiguientes del modelo de flujo de trabajo se ejecutan y completan.
1. Cuando se completa el paso final, la instancia del flujo de trabajo se completa y, por lo tanto, se archiva.

Con AEM se proporcionan muchos modelos de flujo de trabajo útiles. Además, los desarrolladores de su organización pueden crear modelos de flujo de trabajo personalizados, adaptados a las necesidades específicas de sus procesos empresariales.

## Pasos del flujo de trabajo {#workflow-steps}

Cuando se ejecutan los pasos del flujo de trabajo, se asocian con una instancia de flujo de trabajo. El historial de una instancia de flujo de trabajo incluye información sobre cada paso que se ha ejecutado para la instancia. Esta información es útil para investigar los problemas que se producen durante la ejecución.

Un usuario o un servicio realiza pasos de flujo de trabajo, según el tipo de paso:

* Cuando un usuario realiza un paso, se le asigna un elemento de trabajo que se coloca en su Bandeja de entrada. El usuario es responsable de completar manualmente el paso para que la instancia de flujo de trabajo avance.
* Cuando un servicio realiza un paso, una vez finalizada la instancia de flujo de trabajo avanza automáticamente al paso siguiente.

>[!NOTE]
>
>Si se produce un error, la implementación de servicio/paso debe controlar el comportamiento de un escenario de error. El propio motor de flujo de trabajo volverá a intentar el trabajo y, a continuación, registrará un error y detendrá la instancia.

## Estado y acciones del flujo de trabajo {#workflow-status-and-actions}

Un flujo de trabajo puede tener uno de los siguientes estados:

* **EJECUTANDO**: La instancia de flujo de trabajo se está ejecutando.
* **COMPLETADO**: La instancia de flujo de trabajo ha finalizado correctamente.

* **SUSPENDIDO**: Se ha suspendido la instancia de flujo de trabajo.
* **ABORTADO**: La instancia de flujo de trabajo ha finalizado.
* **ESTILO**: La progresión de la instancia de flujo de trabajo requiere que se ejecute un trabajo en segundo plano, pero el trabajo no se puede encontrar en el sistema. Esta situación puede producirse cuando se produce un error al ejecutar el flujo de trabajo.

>[!NOTE]
>
>Cuando la ejecución de un paso de proceso produce errores, el paso aparece en la Bandeja de entrada del administrador y el estado del flujo de trabajo es **EJECUCIÓN**.

Según el estado actual, puede realizar acciones en las instancias de flujo de trabajo en ejecución cuando necesite intervenir en la progresión normal de una instancia de flujo de trabajo:

* **Suspender**: Detiene temporalmente la ejecución del flujo de trabajo. Suspender es útil en casos excepcionales cuando no desea que continúe el flujo de trabajo, por ejemplo para mantenimiento. La suspensión cambia el estado del flujo de trabajo a Suspendido.
* **Reanudar**: Reinicia un flujo de trabajo suspendido en el mismo punto de ejecución en el que se suspendió, utilizando la misma configuración.
* **Finalizar**: Finaliza la ejecución del flujo de trabajo y cambia el estado a **ABORTED**. No se puede reiniciar una instancia de flujo de trabajo anulada.

