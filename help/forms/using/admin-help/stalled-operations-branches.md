---
title: Trabajo con operaciones y ramas estancadas
seo-title: Working with stalled operations and branches
description: La página Operaciones interrumpidas y la página Ramas interrumpidas muestran los procesos que se han estancado.
seo-description: The Stalled Operations page and the Stalled Branches page show the processes that have stalled.
uuid: 5f6202b0-79c2-4c3c-847a-236c0366e60b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8c2567f3-7220-436a-b9f2-2824a98c1ccc
exl-id: c96faae0-2b0f-4334-b61c-f13b2d1ec179
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# Trabajo con operaciones y ramas estancadas {#working-with-stalled-operations-and-branches}

La página Operaciones interrumpidas y la página Ramas interrumpidas muestran los procesos que se han estancado. Un proceso puede paralizarse cuando se produce un error durante o después de la ejecución de una operación o debido a una operación de paralización deliberada en el proceso:

* Las operaciones se pueden detener debido a un error imprevisto. Sin embargo, una operación de bifurcación en un proceso impide deliberadamente que un proceso siga ejecutándose y requiere la intervención del administrador.
* Las ramas se pueden paralizar entre operaciones durante una evaluación de regla.

Cuando un proceso se detiene, no se ejecutan más operaciones hasta que se soluciona el problema y se reinicia la operación o rama.

La lista muestra la siguiente información para cada elemento bloqueado:

**Nombre de operación o nombre de rama:** Nombre de la operación o rama.

**Estado:** Siempre está paralizado para los elementos paralizados.

**Error:** Una breve descripción del problema.

**ID de proceso:** El entero positivo que asigna el flujo de trabajo de formularios cuando se crea una instancia del proceso (es decir, cuando un usuario o un paso automatizado inician un proceso). Puede utilizar este identificador para rastrear la instancia de proceso a lo largo de su ciclo de vida.

**Nombre del proceso - Versión:** Nombre del proceso asignado en Workbench.

**Fecha de interrupción:** La fecha y hora en que la operación o rama se ha estancado.

Puede realizar las siguientes tareas en la página Operaciones paralizadas o Ramas paralizadas :

* Seleccione un error para ver los detalles sobre él. Cuando selecciona un error, aparece la página Detalles del error.
* Finalice o vuelva a intentar las operaciones interrumpidas o vuelva a intentar las ramas interrumpidas.

## Finalización o reintento de operaciones o sucursales interrumpidas {#terminating-or-retrying-stalled-operations-or-branches}

En la página Operaciones paralizadas , puede finalizar las instancias de proceso mostradas.

Cuando finaliza una instancia de proceso, esta deja de ejecutarse y no se realizan más operaciones. Normalmente, un proceso finaliza solo si queda bloqueado o inutilizable debido a un error y no se puede corregir ni reiniciar.

En la página Operaciones paralizadas o en la página Ramas paralizadas , puede reintentar la operación o rama.

Cuando vuelve a intentar una operación, se envía una solicitud al flujo de trabajo de Forms para reiniciar la operación. Si el error que provocó que el proceso se paralizara se ha corregido y la solicitud de reintento se ha realizado correctamente, el proceso comienza a ejecutarse de nuevo desde el punto en que se había estancado y su estado cambia a EJECUTANDO. Si la operación no se puede reiniciar, permanece STALLED y es posible que tenga que terminarla.

### Finalización de una operación interrumpida {#terminate-a-stalled-operation}

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Errores de operaciones interrumpidas.
1. En la página Operaciones interrumpidas , seleccione el artículo que desee finalizar y haga clic en Finalizar.

### Reintentar una operación o rama interrumpida {#retry-a-stalled-operation-or-branch}

1. En la consola de administración, haga clic en Servicios > flujo de trabajo de formularios y, a continuación, haga clic en Errores de operaciones interrumpidas o Errores de ramas interrumpidas.
1. En la página Operaciones interrumpidas o Ramas interrumpidas , seleccione el elemento que desee reintentar y haga clic en Reintentar.

## Visualización de detalles de error sobre operaciones o ramas interrumpidas {#viewing-error-details-about-stalled-operations-or-branches}

Si selecciona un error en la lista de elementos detenidos de la página Operaciones interrumpidas o Ramas interrumpidas, aparecerá la página Detalles del error, que muestra detalles sobre el error que pueden ayudarle a solucionar el problema.

El cuadro de la parte inferior de la página contiene la información de error.

También puede finalizar o reintentar operaciones interrumpidas y reintentar ramas interrumpidas desde la página Detalles del error .

## El proceso no se detiene cuando el usuario de escalación no existe {#process-does-not-stall-when-escalation-user-does-not-exist}

Los errores se producen cuando la operación Asignar tarea del servicio Usuario de formularios AEM está configurada para escalar la tarea a otro usuario después de un período de tiempo específico y el usuario de escalación se elimina después de que se ejecute la operación Asignar tarea pero antes de que se produzca la escalación.

Cuando se produce esta situación, el estado del proceso y la tarea no cambia en el momento de escalación configurado y la escalación no se produce pero el proceso no se detiene. El siguiente mensaje aparece en el registro del servidor:

&quot;La entidad de seguridad especificada para la escalación no es válida para taskID: *number*, cola especificada: *number*.&quot;

Si el usuario de escalación se elimina antes de que se genere la tarea (antes de que se ejecute la operación Asignar tarea), se detendrá el proceso o se generará el evento de excepción InvalidPrincipal.

Para evitar este problema, al eliminar un usuario, busque tareas que pertenezcan a ese usuario y tratarlas según corresponda. (Consulte [Trabajo con tareas](/help/forms/using/admin-help/tasks.md#working-with-tasks).)
