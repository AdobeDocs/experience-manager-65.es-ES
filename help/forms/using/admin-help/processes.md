---
title: Administración de procesos
seo-title: Administración de procesos
description: La página Lista de procesos muestra los procesos que un usuario ha iniciado o que se iniciaron automáticamente. Obtenga más información sobre la administración de los procesos.
seo-description: La página Lista de procesos muestra los procesos que un usuario ha iniciado o que se iniciaron automáticamente. Obtenga más información sobre la administración de los procesos.
uuid: 4cd17400-681a-4e40-996c-7dda57ce449a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 37e702c2-8716-4360-a3eb-d9877b28cc86
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Administración de procesos {#managing-processes}

La página Lista de procesos muestra los procesos que un usuario ha iniciado o que se iniciaron automáticamente.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Flujo de trabajo de formularios. La lista de procesos muestra la siguiente información:

   **** Nombre del proceso - Versión: Nombre del proceso, tal como se define en Workbench.

   **** Aplicación: Aplicación a la que pertenece el proceso, tal como se define en Workbench.

   **** Estado: Activo significa que el proceso es el que se activa para la versión del proceso. Inactivo significa que el proceso es una versión antigua que aún tiene instancias de proceso.

   **** Fecha de creación: Fecha y hora en que se implementó el proceso.

1. Haga clic en un nombre de proceso para ver sus instancias de proceso en la página Instancia de proceso.

## Uso de instancias de proceso {#working-with-process-instances}

Si accede a la página Instancia de proceso desde la página Lista de procesos, se enumerarán todas las instancias de proceso del proceso seleccionado. Si accede a la página Instancia de proceso después de realizar una búsqueda, solo se enumerarán las instancias de proceso encontradas.

Para cada instancia de proceso, la lista muestra la siguiente información:

**** ID del proceso: El identificador que asigna el flujo de trabajo de formularios cuando se crea una instancia del proceso (es decir, cuando un usuario o un paso automatizado inicia un proceso). Puede utilizar este identificador para rastrear la instancia de proceso a lo largo de su ciclo de vida.

**** Nombre del proceso - Versión: Nombre del proceso, tal como se define en Workbench.

**** Estado: Indica si la instancia de proceso se está ejecutando con normalidad, cambia de estado o se ha detenido. (Consulte Acerca de los estados de instancias de proceso).

**** Fecha de creación: Fecha y hora en que se creó la instancia de proceso.

**** Fecha de actualización: Fecha y hora en que se cambió por última vez el estado de la instancia de proceso.

Puede realizar las siguientes tareas en la página Instancia de proceso:

* Seleccione una instancia de proceso para ver los detalles del mismo, como sus operaciones y subprocesos. Cuando se selecciona una instancia de proceso, aparece la página Detalles de instancia de proceso.
* Suspender, aprobar o finalizar instancias de proceso.
* Busque una instancia de proceso. Para comenzar una búsqueda, haga clic en Buscar.

### Acerca de los estados de instancias de proceso {#about-process-instance-statuses}

Una instancia de proceso, incluidos los subprocesos, puede tener los siguientes estados:

**** COMPLETAR: Se han completado todas las ramas y operaciones de la instancia de proceso. COMPLETE es el estado final de una instancia de proceso.

**** COMPLETANDO: El estado de la instancia de proceso está a punto de cambiar a COMPLETE.

**** INICIADO: La instancia de proceso se ha creado pero aún no se está ejecutando. INICIADO es el primer estado de una instancia de proceso.

**** EJECUTANDO: La instancia de proceso se está ejecutando normalmente. Es posible que se esté llevando a cabo un paso automatizado o que la instancia de proceso esté recibiendo la entrada del usuario o esperando la interacción del usuario.

**** SUSPENDIDO: La instancia de proceso ha sido suspendida por un administrador o por un paso en el proceso. No se realizarán más operaciones hasta que se cambie el estado.

**** SUSPENDIENTE: El estado está a punto de cambiar a SUSPENDIDO. Si una operación se ha diseñado para ignorar las solicitudes de suspensión y aún no se ha completado, dicha operación debe completarse antes de que se suspenda la instancia de proceso.

**** TERMINADO: Un administrador ha terminado la instancia de proceso.

**** FINALIZACIÓN: El estado está a punto de cambiar a TERMINADO. Si una operación se ha diseñado para ignorar las solicitudes de finalización y aún no se ha completado, dicha operación debe completarse antes de que finalice la instancia de proceso.

**** DESSUSPENDIENTE: El estado está a punto de cambiar a EJECUCIÓN después de SUSPENDER.

**Nota**: *Cuando se realiza una solicitud para cambiar el estado de una instancia de proceso (por ejemplo, suspender o finalizar), la solicitud entra en la cola de comandos para el flujo de trabajo de formularios. Según el tamaño de la cola y la velocidad de procesamiento general, es posible que el estado mostrado no cambie hasta que la página se vuelva a cargar una o más veces.*

### Suspender o anular la suspensión de instancias de proceso {#suspend-or-unsuspend-process-instances}

Si necesita solucionar un problema o si sabe que una instancia de proceso encontrará un problema en un paso posterior debido a alguna condición externa, puede suspender la instancia de proceso temporalmente.

Puede suspender las instancias de proceso que tengan un estado de EJECUCIÓN.

Después de suspender una instancia de proceso, su estado cambia a SUSPENDENTE, SUSPENDIDO y el proceso se pausa en la operación actual. La instancia de proceso permanece en este estado hasta que se cambia el estado a SUSPENDIDO.

Sólo las instancias de proceso que tengan el estado SUSPENDIDO pueden cambiarse a SUSPENDIDO.

Cuando se deja de suspender una instancia de proceso, su estado cambia a EJECUCIÓN y continúa con la operación donde se había suspendido.

Cuando se suspende una instancia de proceso que ha invocado otros procesos (procesos secundarios) mediante la operación de invocación, los procesos secundarios también se suspenden.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Flujo de trabajo de formularios.
1. En la página Instancia de proceso, seleccione el proceso y haga clic en Suspender o en Aprobar.

### Finalización de instancias de proceso {#terminate-a-process-instances}

Si una operación de una instancia de proceso se ha detenido o ha encontrado alguna otra condición de error, o si necesita forzar una instancia de proceso para que deje de ejecutarse, puede finalizar la instancia de proceso.

Puede finalizar instancias de proceso que tengan cualquier estado.

Al finalizar una instancia de proceso, su estado cambia a TERMINATING, luego TERMINATED y el proceso se detiene en su operación actual. No se ejecutan más operaciones y se finalizan todas las operaciones y tareas asociadas.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Flujo de trabajo de formularios.
1. En la página Instancia de proceso, seleccione el proceso y haga clic en Finalizar.

## Trabajo con detalles de instancias de proceso {#working-with-process-instance-details}

La página Detalle de Instancia de Proceso muestra el historial de una instancia de proceso.

El área Resumen muestra información básica sobre la instancia de proceso.

En la ficha Operaciones, cada operación de la instancia de proceso se muestra en orden de finalización del primero al último con la siguiente información:

**** Nombre de la operación: Nombre de la operación, tal como se define en Workbench.

**** Estado: Indica si la operación se está ejecutando normalmente o se ha detenido. (Consulte Acerca de los estados de instancias de proceso).

**** Nombre de rama: Nombre de la rama, tal como se define en Workbench.

**** Fecha inicial: Fecha y hora en que se inició la operación.

**** Fecha de finalización: Fecha y hora en que se completó la operación.

Un subproceso es una instancia de proceso que se inicia con otro proceso y se ejecuta independientemente del otro. Los subprocesos solo se muestran si se diseñaron como parte del proceso en Workbench. En la ficha Subprocesos, se muestra cada subproceso con la siguiente información:

**** ID del proceso: Este entero positivo que asigna el flujo de trabajo de formularios cuando se crea una instancia del proceso (es decir, cuando un usuario o un paso automatizado inicia el proceso). Puede utilizar este identificador para rastrear la instancia de proceso a través de su ciclo vital.

**** Nombre del proceso - Versión: Nombre del proceso, tal como se define en Designer.

**** Estado: Indica si la instancia de proceso se está ejecutando con normalidad, cambia de estado o se ha detenido. (Consulte Acerca de los estados de instancias de proceso).

**** Fecha de creación: Fecha y hora en que se creó el subproceso.

**** Fecha de actualización: Fecha y hora en que se cambió por última vez el estado del subproceso.

Puede realizar las siguientes tareas en la página Detalle de Instancia de Proceso:

* Seleccione una operación para ver los detalles sobre ella. Cuando selecciona una operación, aparece la página Detalle de la operación.
* Seleccione un subproceso para ver los detalles del mismo. Cuando se selecciona un subproceso, aparece la página Detalle de instancia de proceso.
* Terminar o reintentar operaciones o subprocesos, según su estado.

### Acerca de los estados de las operaciones {#about-operation-statuses}

Una operación (un paso en un proceso) puede tener los siguientes estados:

**** COMPLETAR: Operación completada.

**** EJECUTANDO: La operación se está ejecutando normalmente. Es posible que reciba la entrada del usuario o esté esperando la interacción del usuario, o que se esté llevando a cabo un paso automatizado.

**** INSTALADO: Se produjo un problema mientras se procesaba la operación. Compruebe el error o la excepción en la página Operaciones en espera.

**** TERMINADO: Un administrador terminó la operación.

### Finalización de operaciones o subprocesos {#terminate-operations-or-subprocesses}

Si una operación o un subproceso se ha detenido o ha encontrado alguna otra condición de error, o si necesita forzar una operación o un subproceso para que deje de ejecutarse, puede finalizarlo.

Puede finalizar una operación que se esté EJECUTANDO.

Al finalizar una operación, su estado cambia a TERMINADO. La operación no se completa y la instancia de proceso deja de ejecutarse.

Puede finalizar un subproceso que tenga cualquier estado.

Al finalizar un subproceso, su estado cambia a TERMINATING, TERMINATED y la instancia de proceso se detiene en sus operaciones actuales. No se ejecutan más operaciones en el subproceso, aunque la instancia de proceso principal sigue ejecutándose.

No puede finalizar procesos que tengan elementos de puerta de enlace en el diagrama de proceso. Si intenta finalizar estos tipos de procesos, las operaciones dentro de los elementos de la puerta de enlace no se verán afectadas. Para finalizar operaciones que se encuentran dentro de un elemento de puerta de enlace, debe finalizar las operaciones directamente.

1. En la página Detalles de instancia de proceso, haga clic en la ficha Operaciones o Subprocesos.
1. Seleccione la operación o el subproceso y haga clic en Terminar.

### Reintentar una operación {#retry-an-operation}

Puede reintentar la operación que tenga el estado STALLED.

Cuando se reintenta una operación, se envía una solicitud al flujo de trabajo de Forms para reiniciar la operación. Si la solicitud se realiza correctamente, el estado cambia a EJECUCIÓN. Si la operación no se puede reiniciar, permanece INSTALADA y es posible que tenga que finalizarla.

1. En la página Detalles de instancia de proceso, haga clic en la ficha Operaciones.
1. Seleccione la operación y haga clic en Reintentar.

## Trabajo con operaciones {#working-with-operations}

La página Detalles de la Operación muestra un resumen de una operación en un proceso y sus asignaciones de usuario actuales.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Flujo de trabajo de formularios.
1. Haga clic en un nombre de proceso para mostrar sus instancias de proceso. Haga clic en una instancia de proceso para mostrar la página Detalles de instancia de proceso y, a continuación, seleccione una operación para mostrar la página Detalle de la operación.

   Para cada tarea, la lista muestra la siguiente información:

   **** Nombre del proceso - Versión: Nombre del proceso, tal como se define en Workbench.

   **** Aplicación: Aplicación a la que pertenece el proceso, tal como se define en Workbench.

   **** Estado: Activo significa que el proceso es el que se activa para la versión del proceso. Inactivo significa que el proceso es una versión antigua que aún tiene instancias de proceso.

   **** Fecha de creación: Fecha y hora en que se implementó el proceso.

