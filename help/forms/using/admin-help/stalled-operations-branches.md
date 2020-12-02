---
title: Trabajar con operaciones y ramas paralizadas
seo-title: Trabajar con operaciones y ramas paralizadas
description: La página Operaciones fijas y la página Ramas fijas muestran los procesos que se han detenido.
seo-description: La página Operaciones fijas y la página Ramas fijas muestran los procesos que se han detenido.
uuid: 5f6202b0-79c2-4c3c-847a-236c0366e60b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8c2567f3-7220-436a-b9f2-2824a98c1ccc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 0%

---


# Trabajar con operaciones y ramas paralizadas {#working-with-stalled-operations-and-branches}

La página Operaciones fijas y la página Ramas fijas muestran los procesos que se han detenido. Un proceso puede paralizarse cuando se produce un error durante o después de la ejecución de una operación o debido a una operación deliberada de paralización en el proceso:

* Las operaciones se pueden detener debido a un error imprevisto. Sin embargo, una operación de bifurcación de stall en un proceso impide deliberadamente que un proceso continúe y requiere la intervención del administrador.
* Las ramas pueden estancarse entre operaciones durante una evaluación de regla.

Cuando un proceso se detiene, no se ejecutan más operaciones hasta que se soluciona el problema y se reinicia la operación o ramificación.

Para cada elemento detenido, la lista muestra la siguiente información:

**Nombre de Operación o Nombre de Rama:** El nombre de la operación o ramificación.

**Estado:** Siempre se INSTALA para los elementos que están inmovilizados.

**Error:** una breve descripción del problema.

**ID de proceso:** el entero positivo que asigna el flujo de trabajo de formularios cuando se crea una instancia del proceso (es decir, cuando un usuario o un paso automatizado inician un proceso). Puede utilizar este identificador para rastrear la instancia de proceso a lo largo de su ciclo de vida.

**Nombre del proceso: Versión:** el nombre del proceso asignado en Workbench.

**Fecha de Parada:** La fecha y la hora en que la operación o rama se ha detenido.

Puede realizar las siguientes tareas en la página Operaciones paralizadas o Ramas paralizadas:

* Seleccione un error para vista de detalles sobre él. Cuando selecciona un error, aparece la página Detalles del error.
* Finalice o vuelva a intentar las operaciones que se han detenido o reintente las ramas que se han detenido.

## Finalización o reintento de operaciones o ramas paralizadas {#terminating-or-retrying-stalled-operations-or-branches}

En la página Operaciones fijas, puede finalizar las instancias de proceso mostradas.

Al finalizar una instancia de proceso, esta se detiene y no se realizan más operaciones. Normalmente, un proceso se cierra solo si queda bloqueado o inutilizable debido a un error y no puede repararse ni reiniciarse.

En la página Operaciones fijas o en la página Ramas fijas, puede reintentar la operación o rama.

Cuando reintenta una operación, se envía una solicitud al flujo de trabajo de Forms para reiniciar la operación. Si el error que provocó que el proceso se paralizara se ha corregido y la solicitud de reintento se realiza correctamente, el proceso comienza a ejecutarse de nuevo desde el punto en que se detuvo y su estado cambia a EJECUCIÓN. Si la operación no se puede reiniciar, permanece INSTALADA y es posible que tenga que finalizarla.

### Finalización de una operación detenida {#terminate-a-stalled-operation}

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Errores de operaciones fijas.
1. En la página Operaciones fijas, seleccione el elemento que desee finalizar y haga clic en Finalizar.

### Reintentar una operación o rama inmovilizada {#retry-a-stalled-operation-or-branch}

1. En la consola de administración, haga clic en Servicios > flujo de trabajo de formularios y, a continuación, haga clic en Errores de operaciones paralizadas o Errores de ramificación paralizados.
1. En la página Operaciones fijas o Ramas fijas, seleccione el elemento que desee reintentar y haga clic en Reintentar.

## Visualización de detalles de error sobre operaciones o ramas paralizadas {#viewing-error-details-about-stalled-operations-or-branches}

Si selecciona un error en la lista de los elementos que se han detenido en la página Operaciones paralizadas o Ramas paralizadas, aparecerá la página Detalles del error, que muestra detalles sobre el error que pueden ayudarle a solucionar el problema.

El cuadro en la parte inferior de la página contiene la información de error.

También puede finalizar o reintentar las operaciones en espera y reintentar las ramas en espera desde la página Detalles del error.

## El proceso no se detiene cuando el usuario de escalación no existe {#process-does-not-stall-when-escalation-user-does-not-exist}

Los errores se producen cuando la operación Asignar Tarea del servicio Usuario de formularios AEM está configurada para escalar la tarea a otro usuario después de un período de tiempo específico y el usuario de escalación se elimina después de que se ejecute la operación Asignar Tarea pero antes de que se produzca la escalación.

Cuando se produce esta situación, el estado del proceso y la tarea no cambia en el tiempo de escalación configurado y la escalación no se produce pero el proceso no se detiene. Aparece el siguiente mensaje en el registro del servidor:

&quot;La entidad de seguridad especificada para la escalación no es válida para taskID: *número*, cola especificada: *número*.&quot;

Si se elimina el usuario de escalación antes de que se genere la tarea (antes de que se ejecute la operación Asignar Tarea), se detendrá el proceso o se emitirá el evento de excepción InvalidPrincipal.

Para evitar este problema, al eliminar un usuario, busque tareas que pertenezcan a ese usuario y tratarlas como corresponde. (Consulte [Uso de tareas](/help/forms/using/admin-help/tasks.md#working-with-tasks).)
