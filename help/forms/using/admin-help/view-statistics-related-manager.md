---
title: Ver estadísticas relacionadas con Work Manager
seo-title: View statistics related to Work Manager
description: La ficha Administrador de trabajo muestra las estadísticas relacionadas con los elementos del Administrador de trabajo. Aprenda a ver y filtrar los elementos de trabajo.
seo-description: The Work Manager tab displays statistics that relate to Work Manager items. Learn how you can view and filter the work items.
uuid: c3a575c7-773d-477a-bc75-6cbcf8b836b8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8e1b2f7c-2609-474b-a1b2-fa820df74ae3
exl-id: ce8f7257-bb9a-428d-b816-27b1d1632ee1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 0%

---

# Ver estadísticas relacionadas con Work Manager {#view-statistics-related-to-work-manager}

La ficha Administrador de trabajo muestra las estadísticas relacionadas con los elementos del Administrador de trabajo. Estos elementos de trabajo se encuentran en distintos estados según su ubicación en el proceso. (Consulte [Estado (solo para las categorías Predeterminado, Flujo de trabajo o Eventos)](view-statistics-related-manager.md#status-for-default-workflow-or-events-categories-only).) Puede filtrar la información para ver solo un subconjunto de los elementos utilizando las distintas opciones disponibles (por ejemplo, Estado o Categoría). Puede ordenar los elementos de trabajo o trabajo resultantes (en orden ascendente o descendente) haciendo clic en uno de los encabezados de columna. Además, puede administrar los elementos de trabajo utilizando las herramientas de operación que se muestran encima de la lista de elementos de trabajo.

## Filtrado de elementos de trabajo {#filter-the-work-items}

1. Haga clic en la ficha Administrador de trabajo .
1. Seleccione los criterios de uno o varios de los filtros descritos a continuación y haga clic en Ir.

### Categoría {#category}

**Predeterminado:** Todos los elementos de trabajo a los que el cliente no asignó una categoría cuando se enviaron. El administrador de trabajo administra estos elementos, por lo que los estados pertenecen al administrador de trabajo.

**Administrador de trabajos:** Todos los trabajos que pertenecen a Job Manager. El administrador de trabajos administra sus propios trabajos y tiene sus propios estados. Consulte los estados de trabajos específicos que se describen a continuación.

**Flujo de trabajo:** Todos los elementos de trabajo que pertenecen a la ejecución del flujo de trabajo. El flujo de trabajo no administra sus propios elementos de trabajo, sino que depende del administrador de trabajo; por lo tanto, los estados pertenecen a Work Manager.

**Eventos:** Todos los elementos de trabajo que pertenecen a Gestión de eventos. La gestión de eventos no gestiona sus propios elementos de trabajo, sino que depende de Work Manager; por lo tanto, los estados pertenecen a Work Manager.

### Estado (solo para las categorías Predeterminado, Flujo de trabajo o Eventos) {#status-for-default-workflow-or-events-categories-only}

**Mostrar todo:** Muestra todos los elementos de trabajo actuales.

**Programado:** Muestra todos los elementos de trabajo listos para ser ejecutados por el servidor de aplicaciones pero aún no iniciados.

**En pausa:** Muestra todos los elementos de trabajo programados que la aplicación cliente ha pausado. Estos elementos se pueden ejecutar o eliminar. (Consulte Administración de los elementos de trabajo o trabajos).

**En curso:** Muestra todos los elementos de trabajo que el Work Manager del servidor de aplicaciones recogió y que se completarán o no. No puede utilizar operaciones en estos elementos de trabajo.

**Completar:** Muestra todos los elementos de trabajo que se ejecutaron correctamente. Los elementos de trabajo persistentes permanecen en este estado y los elementos no persistentes se eliminan al completar las rellamadas a los controladores de rellamadas. Puede eliminar estos elementos utilizando la operación Eliminar elementos. (Consulte Administración de los elementos de trabajo o trabajos).

**Error:** Muestra todos los elementos de trabajo que no se completaron correctamente debido a una condición de error. Estos elementos de trabajo se pueden volver a intentar varias veces mediante la operación Reintentar elementos. (Consulte Administración de los elementos de trabajo o trabajos). El vínculo Error de la columna Estado le permite acceder a los detalles sobre el error.

**Desconocido:** Muestra todos los elementos de trabajo cuyo estado es desconocido.

### Estado (solo para la categoría Administrador de trabajos) {#status-for-job-manager-category-only}

**Finalizado:** Muestra todos los trabajos que se han ejecutado correctamente. Los elementos de trabajo persistentes permanecen en este estado y los elementos no persistentes se eliminan al completar las rellamadas a los controladores de rellamadas.

**Completar solicitud:** Muestra los trabajos para los que se realizó una solicitud completa.

**Error solicitado:** Muestra los trabajos para los que se realizó una solicitud de error.

**Error:** Muestra los trabajos que no se completaron correctamente debido a una condición de error. El vínculo Error de la columna Estado le permite acceder a los detalles sobre el error.

**Finalización solicitada:** Muestra los trabajos para los que se realizó una solicitud de finalización.

**Finalizado:** Muestra los trabajos que finalizaron sin completarse.

**Suspender solicitud:** Muestra los trabajos para los que se realizó una solicitud de suspensión.

**Suspendido:** Muestra los trabajos que están suspendidos.

**Reanudar solicitado:** Muestra los trabajos para los que se realizó una solicitud de reanudación.

**En cola:** Muestra los trabajos que están en cola.

**En ejecución:** Muestra los trabajos que se están ejecutando.

### Nombre del servidor {#server-name}

Solo para servidores agrupados, seleccione el nombre del nodo para mostrar los elementos de trabajo o los elementos de trabajo creados solo en ese servidor. Si se selecciona Mostrar todo , se muestran todos los elementos de trabajo de todos los nodos de un clúster.

### Hora de la creación {#create-time}

Seleccione una opción de este filtro para mostrar solo los elementos de trabajo creados dentro del lapso de tiempo seleccionado. Por ejemplo, si selecciona 1 día, se mostrarán todos los elementos de trabajo creados en un plazo de 24 horas antes de la hora establecida en el filtro Antes de .

### Antes de {#prior-to}

Establece la fecha y la hora que utiliza el filtro Crear hora como fecha de finalización. Mantenga la opción Usar fecha y hora actuales seleccionada para volver a filtrar desde la fecha y la hora actuales, o anule la selección de la opción e introduzca los valores adecuados. Haga clic en los iconos del calendario o en los iconos del reloj para seleccionar valores utilizando esas herramientas.

Por ejemplo, si selecciona Crear hora = 1 día y Antes de = Usar fecha y hora actuales , se devuelven todos los elementos de trabajo creados en las últimas 24 horas.

>[!NOTE]
>
>En implementaciones de bases de datos de Oracle, los filtros de intervalo de fechas (es decir, Crear tiempo y Antes de la configuración) no funcionan con precisión. Utilice otro filtro para recuperar elementos de trabajo.

## Acerca de la interfaz de la ficha Administrador de trabajo {#about-the-work-manager-tab-interface}

Cuando se ejecuta una consulta de Work Manager o se realiza una operación en un trabajo o trabajo, aparece un mensaje encima de la lista. Este mensaje proporciona comentarios sobre la acción que ha iniciado y, en algunos casos, un vínculo de Más información para proporcionar detalles. Por ejemplo, si la operación que inició falla, el mensaje lo indica y proporciona un vínculo para obtener detalles sobre el error.

Al hacer clic en Más información, el cuadro de diálogo Detalles de la operación muestra una lista de los elementos de trabajo o trabajos seleccionados durante la operación. Puede hacer clic en cada elemento de la lista para ver los detalles del error en la parte inferior del cuadro de diálogo.

### Administrar los elementos de trabajo o trabajos {#manage-the-work-items-or-jobs}

1. Utilice las herramientas de operación descritas a continuación para administrar los elementos de trabajo o trabajos de la lista.

   >[!NOTE]
   >
   >Las operaciones están disponibles en función del estado del elemento.

   **Eliminar elementos:** Elimina el trabajo o elemento de trabajo seleccionado.

   **Pausar elementos:** Pone en pausa el trabajo o elemento de trabajo seleccionado.

   **Reanudar elementos:** Reanuda el trabajo o elemento de trabajo seleccionado desde su estado en pausa.

   **Reintentar elementos:** Intenta volver a ejecutar el trabajo o elemento de trabajo seleccionado desde su estado actual.

   Para comprobar si una operación se ha realizado correctamente, haga clic en Más información encima de la lista. Se muestra un cuadro de diálogo que contiene los elementos de trabajo o trabajos seleccionados y sus estados.

## Información adicional sobre los estados de elementos de trabajo {#additional-information-about-work-item-statuses}

Una transición de estado típica para un elemento de trabajo es Nuevo > Programado > En curso > Completado o Fallo.

El estado En pausa interrumpe este flujo normal. Tanto la aplicación cliente como el administrador del sistema pueden iniciar esta interrupción (por ejemplo, para mantenimiento o actualización). Puede invertir esta acción utilizando la operación Reanudar para mover el elemento de trabajo de nuevo al estado Programado.

Un elemento de trabajo en estado Programado está en cola para su ejecución que aún no ha comenzado. Estos elementos se pueden pausar o eliminar, o se moverán al estado En curso cuando el Administrador de trabajo los saque de la cola. Los elementos de trabajo en curso no se pueden modificar. Se completarán o fallarán.

El estado Failed se produce como resultado de una condición de error que se produce durante la ejecución del elemento de trabajo. Si cree que los errores son circunstanciales (debido al contexto en el momento de la ejecución), puede reintentar la ejecución y volver a poner el elemento de trabajo en cola. Solo se permite un número limitado de reintentos.
