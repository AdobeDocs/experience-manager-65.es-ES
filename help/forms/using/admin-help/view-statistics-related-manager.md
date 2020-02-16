---
title: Ver estadísticas relacionadas con el Administrador de trabajo
seo-title: Ver estadísticas relacionadas con el Administrador de trabajo
description: La ficha Administrador de trabajo muestra las estadísticas relacionadas con los elementos del Administrador de trabajo. Descubra cómo puede ver y filtrar los elementos de trabajo.
seo-description: La ficha Administrador de trabajo muestra las estadísticas relacionadas con los elementos del Administrador de trabajo. Descubra cómo puede ver y filtrar los elementos de trabajo.
uuid: c3a575c7-773d-477a-bc75-6cbcf8b836b8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8e1b2f7c-2609-474b-a1b2-fa820df74ae3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Ver estadísticas relacionadas con el Administrador de trabajo {#view-statistics-related-to-work-manager}

La ficha Administrador de trabajo muestra las estadísticas relacionadas con los elementos del Administrador de trabajo. Estos elementos de trabajo se encuentran en diferentes estados según el lugar en el que se encuentren en el proceso. (Consulte [Estado (solo para las categorías Predeterminado, Flujo de trabajo o Eventos)](view-statistics-related-manager.md#status-for-default-workflow-or-events-categories-only).) Puede filtrar la información para ver solo un subconjunto de los elementos mediante las distintas opciones disponibles (por ejemplo, Estado o Categoría). Puede ordenar los elementos de trabajo o trabajo resultantes (en orden ascendente o descendente) haciendo clic en uno de los encabezados de columna. Además, puede administrar los elementos de trabajo mediante las herramientas de operación que se muestran encima de la lista de elementos de trabajo.

## Filtrar los elementos de trabajo {#filter-the-work-items}

1. Haga clic en la ficha Administrador de trabajo.
1. Seleccione los criterios para uno o varios de los filtros descritos a continuación y haga clic en Ir.

### Categoría {#category}

**** Predeterminado: Todos los elementos de trabajo a los que el cliente no asignó una categoría cuando se enviaron. El Administrador de trabajo administra estos elementos, por lo que los estados pertenecen al Administrador de trabajo.

**** Administrador de trabajos: Todos los trabajos que pertenecen al Administrador de trabajos. Job Manager administra sus propios trabajos y tiene sus propios estados. Consulte los estados de trabajos específicos que se describen a continuación.

**** Flujo de trabajo: Todos los elementos de trabajo que pertenecen a la ejecución del flujo de trabajo. Workflow no administra sus propios elementos de trabajo, sino que depende del Administrador de trabajo; por lo tanto, los estados pertenecen al Administrador de trabajos.

**** Eventos: Todos los elementos de trabajo que pertenecen a Gestión de eventos. La Administración de eventos no administra sus propios elementos de trabajo, sino que depende del Administrador de trabajo; por lo tanto, los estados pertenecen al Administrador de trabajos.

### Estado (solo para las categorías Predeterminado, Flujo de trabajo o Eventos) {#status-for-default-workflow-or-events-categories-only}

**** Mostrar todo: Muestra todos los elementos de trabajo actuales.

**** Programado: Muestra todos los elementos de trabajo listos para ser ejecutados por el servidor de aplicaciones pero aún no iniciados.

**** En pausa: Muestra todos los elementos de trabajo programados que la aplicación cliente ha pausado. Estos elementos se pueden ejecutar o eliminar. (Consulte Gestión de los elementos de trabajo o los trabajos).

**** En curso: Muestra todos los elementos de trabajo que el Administrador de trabajo del servidor de aplicaciones seleccionó y que se completarán o no. No se pueden usar operaciones en estos elementos de trabajo.

**** Completado: Muestra todos los elementos de trabajo que se ejecutaron correctamente. Los elementos de trabajo persistentes permanecen en este estado y los elementos no persistentes se eliminan al completar las rellamadas a los controladores de rellamada. Puede eliminar estos elementos mediante la operación Eliminar elementos. (Consulte Gestión de los elementos de trabajo o los trabajos).

**** Error: Muestra todos los elementos de trabajo que no se completaron correctamente debido a una condición de error. Estos elementos de trabajo se pueden volver a intentar varias veces mediante la operación Reintentar elementos. (Consulte Gestión de los elementos de trabajo o los trabajos). Un vínculo Error en la columna Estado permite acceder a los detalles del error.

**** Desconocido: Muestra todos los elementos de trabajo cuyo estado es desconocido.

### Estado (solo para la categoría Administrador de trabajos) {#status-for-job-manager-category-only}

**** Finalizado: Muestra todos los trabajos que se han ejecutado correctamente. Los elementos de trabajo persistentes permanecen en este estado y los elementos no persistentes se eliminan al completar las rellamadas a los controladores de rellamada.

**** Completar solicitado: Muestra los trabajos para los que se realizó una solicitud completa.

**** Error solicitado: Muestra los trabajos para los que se realizó una solicitud de error.

**** Error: Muestra los trabajos que no se completaron correctamente debido a una condición de error. Un vínculo Error en la columna Estado permite acceder a los detalles del error.

**** Finalización solicitada: Muestra los trabajos para los que se realizó una solicitud de finalización.

**** Finalizado: Muestra los trabajos que finalizaron sin completarse.

**** Suspender solicitado: Muestra los trabajos para los que se realizó una solicitud de suspensión.

**** Suspendido: Muestra los trabajos que están suspendidos.

**** Reanudación solicitada: Muestra los trabajos para los que se realizó una solicitud de reanudación.

**** En cola: Muestra los trabajos que están en la cola.

**** Ejecutando: Muestra los trabajos que se están ejecutando.

### Nombre del servidor {#server-name}

Solo para servidores agrupados, seleccione el nombre del nodo para mostrar los elementos de trabajo o los elementos de trabajo creados solo en ese servidor. Si Mostrar todo está seleccionado, se muestran todos los elementos de trabajo de todos los nodos de un clúster.

### Crear hora {#create-time}

Seleccione una opción en este filtro para mostrar solo los elementos de trabajo que se crearon dentro del intervalo de tiempo seleccionado. Por ejemplo, si selecciona 1 día, se muestran todos los elementos de trabajo que se crearon dentro de las 24 horas anteriores al tiempo establecido en el filtro Antes de.

### Antes de {#prior-to}

Establece la fecha y la hora que utiliza el filtro Crear hora como fecha de finalización. Mantenga seleccionada la opción Usar fecha y hora actuales para filtrar desde la fecha y hora actuales, o anule la selección de la opción e introduzca los valores correspondientes. Haga clic en los iconos del calendario o en los iconos del reloj para seleccionar los valores mediante esas herramientas.

Por ejemplo, si selecciona Crear hora = 1 día y Antes de = Usar fecha y hora actuales, se devuelven todos los elementos de trabajo que se crearon en las últimas 24 horas.

>[!NOTE]
>
>En implementaciones de bases de datos Oracle, los filtros de intervalo de fechas (es decir, Crear tiempo y Antes de los ajustes) no funcionan correctamente. Utilice otro filtro para recuperar elementos de trabajo.

## Acerca de la interfaz de la ficha Administrador de trabajo {#about-the-work-manager-tab-interface}

Cuando se ejecuta una consulta de Administrador de trabajo o se realiza una operación en un trabajo o trabajo, aparece un mensaje encima de la lista. Este mensaje proporciona comentarios sobre la acción que ha iniciado y, en algunos casos, un vínculo Más información para proporcionar detalles. Por ejemplo, si falla la operación iniciada, el mensaje indica tanto y proporciona un vínculo para obtener detalles sobre el error.

Al hacer clic en Más información, el cuadro de diálogo Detalles de la operación muestra una lista de los elementos de trabajo o trabajos seleccionados durante la operación. Puede hacer clic en cada elemento de la lista para ver los detalles del error en la parte inferior del cuadro de diálogo.

### Administrar los elementos de trabajo o los trabajos {#manage-the-work-items-or-jobs}

1. Utilice las herramientas de operación que se describen a continuación para administrar los elementos de trabajo o los trabajos de la lista.

   >[!NOTE]
   >
   >Las operaciones están disponibles en función del estado del elemento.

   **** Eliminar elementos: Elimina el elemento de trabajo o trabajo seleccionado.

   **** Pausar elementos: Pausa el elemento de trabajo o trabajo seleccionado.

   **** Reanudar elementos: Reanuda el elemento de trabajo o trabajo seleccionado desde su estado en pausa.

   **** Elementos de reintento: Intenta volver a ejecutar el trabajo o elemento de trabajo seleccionado desde su estado actual.

   Puede comprobar si una operación se ha realizado correctamente haciendo clic en Más información sobre la lista. Se muestra un cuadro de diálogo que contiene los elementos de trabajo o trabajos seleccionados y sus estados.

## Información adicional sobre los estados de elementos de trabajo {#additional-information-about-work-item-statuses}

Una transición de estado típica para un elemento de trabajo es Nuevo > Programado > En curso > Completado o Error.

El estado Pausado interrumpe este flujo normal. La aplicación cliente o el administrador del sistema pueden iniciar esta interrupción (por ejemplo, para mantenimiento o actualización). Puede revertir esta acción utilizando la operación Reanudar para volver a mover el elemento de trabajo a un estado Programado.

Un elemento de trabajo en estado Programado está en cola para la ejecución que aún no ha comenzado. Estos elementos se pueden pausar o eliminar, o se moverán al estado En curso cuando el Administrador de trabajo los saque de la cola. Los elementos de trabajo en curso no se pueden modificar. Se completarán o fracasarán.

El estado Fallido se produce como resultado de una condición de error que se produce durante la ejecución del elemento de trabajo. Si sospecha que los errores son circunstanciales (debido al contexto en el momento de la ejecución), puede volver a intentar la ejecución y colocar el elemento de trabajo en la cola. Sólo se permite un número limitado de reintentos.
