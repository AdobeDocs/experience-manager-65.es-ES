---
title: Sistema de informes de Consultas ad hoc en proceso
seo-title: Sistema de informes de Consultas ad hoc en proceso
description: Crear consultas personalizadas para buscar AEM Forms en los detalles de proceso y tarea JEE en Sistema de informes de procesos
seo-description: Crear consultas personalizadas para buscar AEM Forms en los detalles de proceso y tarea JEE en Sistema de informes de procesos
uuid: db0c5c28-b213-4582-a6ed-df127e570a4e
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b0a544e2-2ce4-48e2-a721-82f481d36004
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '1695'
ht-degree: 0%

---


# Consultas ad-hoc en Sistema de informes de proceso{#ad-hoc-queries-in-process-reporting}

## Consultas ad hoc en el Sistema de informes de procesos {#ad-hoc-queries-in-process-reporting-1}

Las consultas ad-hoc en el Sistema de informes de procesos le permiten crear consultas personalizadas que puede utilizar para buscar detalles de proceso y tarea de las instancias de procesos de AEM Forms definidas en su entorno AEM Forms.

Además, se pueden definir consultas ad hoc mediante filtros de propiedades de proceso y tarea. Estos filtros se pueden guardar y utilizar para ejecutar los informes más adelante.

[**Búsqueda**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-search-p) de procesos: Busque instancias de proceso con un filtro de búsqueda definido por el usuario basado en atributos de proceso.

[**Detalles**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-details-p) del proceso: Detalles de vista de una instancia de proceso especificando el ID de proceso.

**Búsqueda** de tarea: Busque instancias de tarea con un filtro de búsqueda definido por el usuario basado en atributos de tarea.

**Detalles** de tarea: Detalles de vista de una instancia de tarea especificando el ID de tarea.

### Procesos y Tareas {#processes-and-tasks}

Los pasos que sigue para crear filtros y ejecutar consultas para los detalles del proceso son los mismos que para las tareas.

Esto significa que las interfaces de usuario para la búsqueda de procesos y la búsqueda de Tareas difieren solamente en los campos por los que puede buscar y los campos devueltos en los resultados de búsqueda. Esto se debe simplemente a que, aunque muchos de los campos son idénticos, ciertos campos son específicos de los procesos y ciertos campos son específicos de las tareas.

Este artículo detalla las descripciones de las secciones Proceso/Búsqueda de Tareas y Detalles de proceso/Tarea. En los lugares apropiados, se señalarán específicamente las diferencias específicas.

## Búsqueda de procesos/Tareas {#process-task-search}

La búsqueda de procesos/Tareas se utiliza para definir filtros para consultar instancias de proceso/tarea.

### Para crear una consulta de búsqueda de proceso/Tarea {#to-create-a-process-task-search-query}

1. Para crear una vista de las consultas de búsqueda de proceso/Tarea guardadas o para crear una consulta, haga clic en **Consultas ad hoc** y, a continuación, haga clic en **Búsqueda de proceso/Tarea**.

   ![search_nodes](assets/search_nodes.png)

   El panel **Mis Filtros** se muestra a la derecha de la vista de árbol.

   En el panel **Mis Filtros**, puede crear nuevas consultas ad-hoc y hacer clic para ejecutar consultas guardadas anteriormente.

   ![my_filtros_panel](assets/my_filters_panel.png)

1. Para ejecutar una consulta existente, simplemente haga clic en la consulta en el panel **Mis Filtros**.
1. Para crear una consulta, haga clic en **Añadir** (+).

   Aparece el panel **Crear filtro**.

   ![create_filter_panel](assets/create_filter_panel.png)

   Una consulta consiste en uno o más filtros de consulta. Para crear un filtro, agregue una fila de filtro a la consulta. De forma predeterminada, se agrega una fila de filtro a la consulta.

   **Definición de un filtro**

   1. Seleccione un campo.

      ![filter_field](assets/filter_field.png)

      >[!NOTE]
      >
      >La lista de campo contiene los campos específicos del proceso/tarea de AEM Forms.

   1. Seleccione una condición.

      ![filter_condition](assets/filter_condition.png)

      >[!NOTE]
      >
      >Las condiciones enumeradas dependen del atributo seleccionado para el filtrado.

   1. Introduzca un valor.

      ![filter_value](assets/filter_value.png)

   1. Para agregar otro filtro a la consulta, haga clic en **Añadir (+)** a la derecha de la fila de filtro.

      Para eliminar un filtro de la consulta, haga clic en **Eliminar (-)** a la derecha de la fila de filtro.

      ![filter_add_del](assets/filter_add_del.png)

Después de crear una consulta, utilice las opciones de la esquina superior derecha del panel **Crear filtro** para:

* **Cancelar**: Cancele los cambios y vuelva al panel  **Mis** filtros.
* **Ejecutar**: Ejecute la consulta actual para ver y/o comprobar los resultados. En este caso, no es necesario guardar la consulta antes de ejecutar la consulta. Puede comprobar los resultados, realizar cambios si es necesario y, a continuación, guardar la consulta cuando esté satisfecho con el resultado.
* **Guardar**: Guarde el filtro. El filtro se puede ver y ejecutar desde el panel **Mis Filtros**.

### Opciones del panel Mis Filtros {#options-in-my-filters-panel}

Utilice las opciones del panel **Mis Filtros** para **Añadir** ![lc_pr_add_filter](assets/lc_pr_add_filter.png), **Editar** ![lc_pr_delete_filter](assets/lc_pr_delete_filter.png) o **Eliminar**> ![lc_pr_edit_filter](assets/lc_pr_edit_filter.png)una consulta ad-hoc.

![my_filtros_options](assets/my_filters_options.png)

### Para ejecutar una consulta de búsqueda {#to-execute-a-search-query}

1. Para ejecutar una consulta, haga clic en el filtro del panel **Mis Filtros** o haga clic en el botón **Ejecutar** si está creando o editando un filtro.
1. Los resultados de la consulta se muestran en el panel **Informe** de la ventana **Sistema de informes de proceso**.

   ![process_search_result](assets/process_search_result.png)

   Puede paginar los resultados de búsqueda con la ayuda del panel de paginación que se muestra en la parte inferior del informe.

   ![process_result_pgn](assets/process_result_pgn.png)

   En la lista desplegable **Mostrar**, elija el número de resultados que se mostrarán por página.

   En el cuadro de texto **Página**, escriba un número de página para ir directamente a esa página.

1. Los siguientes campos se muestran en un resultado de búsqueda de proceso:

   * **ID** de proceso: ID del proceso. El campo está hipervinculado. Si hace clic en un ID de proceso en este campo, se le redirigirá al panel **[!UICONTROL Detalles del proceso]** para el proceso.
   * **Iniciador**: El usuario de AEM Forms que inició la instancia de proceso
   * **Hora** de creación: Fecha y hora en que se inició la instancia de proceso
   * **Hora** de finalización: Fecha y hora en que se completó la instancia del proceso
   * **Duración**: Duración desde el inicio hasta la finalización de la instancia de proceso
   * **Estado**: Estado actual de la instancia de proceso.

   De forma predeterminada, el resultado se ordena por ID de proceso. Sin embargo, para ordenar el resultado por cualquiera de los campos, haga clic en el título del campo.

   Dado que la ordenación es una operación de alternancia, haga clic en un encabezado de columna para ordenar el resultado de forma ascendente y vuelva a hacer clic en él para ordenar de forma descendente.

   Del mismo modo, los campos siguientes se muestran en un resultado de búsqueda de Tarea:

   * **ID** de tarea: ID de la tarea. El campo está hipervinculado. Si hace clic en un ID de tarea en este campo, se le redirigirá al panel **[!UICONTROL Detalles de Tarea]** de la tarea.
   * **Iniciador**: El usuario de AEM Forms que inició la instancia de proceso
   * **Hora** de creación: Fecha y hora en que se inició la instancia de proceso
   * **Hora** de finalización: Fecha y hora en que se completó la instancia del proceso
   * **Duración**: Duración desde el inicio hasta la finalización de la instancia de proceso
   * **Estado**: Estado actual de la instancia de proceso.

   De forma predeterminada, el resultado se ordena por ID de Tarea. Sin embargo, para ordenar el resultado por cualquiera de los campos, haga clic en el título del campo. El resultado se ordena por la columna indicada con una flecha oscura junto al encabezado de la columna.

   Dado que la ordenación es una operación de alternancia, haga clic en un encabezado de campo para ordenar el resultado en orden ascendente y vuelva a hacer clic en él para ordenar en orden descendente. El orden actual (ascendente/descendente) se indica mediante la dirección de la flecha oscurecida situada junto al encabezado de la columna.

   ![tarea_search_result](assets/task_search_result.png)

1. Haga clic en el botón de carril ![lc_pr_rail_button](assets/lc_pr_rail_button.png) en la esquina superior izquierda para contraer el panel **Mis Filtros** y expanda el espacio disponible para el panel **Informe**.
1. Utilice las opciones de la esquina superior derecha del panel **Informe **Para realizar operaciones en el resultado de la consulta.

   * **Actualizar**: Actualiza el informe con los datos más recientes en el almacenamiento

   * **Exportar a CSV**: Exporte los datos del informe a un archivo separado por comas.
   >[!NOTE]
   >
   >Al exportar un informe, todo el resultado de la búsqueda se exporta a un archivo CSV y no sólo a la página actual

## Detalles de proceso/Tarea {#process-task-details}

Utilice el panel **Detalles del proceso** para vista de los detalles de un proceso específico.

Del mismo modo, se utiliza el panel **Detalles de Tarea** para vista de los detalles de una tarea específica.

### Para obtener detalles del proceso de vista/Tarea {#to-view-process-task-details}

Puede vista de los detalles de un proceso/tarea de AEM Forms específico:

* **A partir de un resultado de búsqueda de proceso/Tarea**
* **Al introducir el ID de proceso/Tarea en el panel Detalles de proceso/Tarea**

#### A partir de un resultado de búsqueda de proceso/Tarea {#from-a-process-task-search-result}

1. Ejecutar una búsqueda de proceso/tarea. Para obtener más información, consulte [Ejecución de una consulta de búsqueda de procesos](#to-execute-a-search-query).

   Observe que los ID de proceso mostrados en el resultado están hipervinculados.

   ![process_id_lista](assets/process_id_list.png)

1. Haga clic en un ID de proceso en la lista para vista de los detalles de este proceso en el panel **Detalles del proceso**.

   El resultado de la consulta **Detalles de proceso/Tarea** muestra detalles de las tareas/formularios contenidos en el proceso/tarea.

   De forma predeterminada, el resultado se ordena por Tarea o ID de formulario. Sin embargo, para ordenar el resultado por cualquiera de los campos, haga clic en el título del campo. La columna por la que se ordena el resultado se indica con una flecha oscura junto al encabezado de la columna.

   Dado que la ordenación es una operación de alternancia, haga clic en un encabezado de campo para ordenar el resultado en orden ascendente y vuelva a hacer clic en él para ordenar en orden descendente. El orden actual (ascendente/descendente) se indica mediante la dirección de la flecha oscurecida situada junto al encabezado de la columna.

   **Resultado de los detalles del proceso**

   ![process_details](assets/process_details.png)

   **Panel izquierdo:** muestra los siguientes detalles del proceso seleccionado:

   * Nombre del proceso
   * Hora de la fecha de creación del proceso
   * Hora de finalización del proceso
   * Duración del proceso
   * Estado del proceso
   * Iniciador de proceso

   **Panel superior derecho:** muestra los siguientes detalles de las tareas que conforman el proceso seleccionado:

   * ID de tarea
   * Nombre de tarea
   * Propietario de la tarea
   * Hora de la fecha de creación de la tarea
   * Hora de la fecha de actualización de la tarea
   * Hora de la fecha de finalización de la tarea
   * Duración de la tarea
   * Estado de tarea

   **Panel inferior derecho:** muestra los siguientes detalles del historial de procesos del proceso seleccionado:

   * Nombre del proceso
   * Iniciador de proceso
   * Hora de la fecha de actualización del proceso
   * Hora de finalización del proceso
   * Estado del proceso

   **Resultado de Detalles de tarea**

   ![tarea_details](assets/task_details.png)

   **Panel izquierdo:** muestra los siguientes detalles de la tarea seleccionada:

   * Nombre de tarea
   * ID del proceso al que pertenece esta tarea
   * Descripción de la tarea
   * Hora de la fecha de creación de la tarea
   * Hora de la fecha de finalización de la tarea
   * Duración de la tarea
   * Estado de tarea
   * Ruta de tarea seleccionada

   **Panel superior derecho:** muestra los siguientes detalles de los formularios que conforman la tarea seleccionada:

   * ID de Foprm
   * Hora de creación del formulario
   * Hora de la actualización del formulario
   * Url de plantilla de formulario

   **Panel inferior derecho:** muestra los siguientes detalles del historial de procesos de la tarea seleccionada:

   * Tipo de asignación de tarea
   * Propietario de la tarea
   * Fecha y hora de creación de la asignación de tareas
   * Hora de la fecha de actualización de la tarea






1. Haga clic en **Volver a la búsqueda de proceso/Tarea** para volver al resultado de búsqueda desde el cual se analizaron los detalles del proceso/tarea.

   ![back_to_search](assets/back_to_search.png)

   Sin embargo, si los detalles del proceso/tarea se encontraron ingresando un ID de proceso/tarea específico, al hacer clic en Volver al proceso/Búsqueda de Tarea regresa a **Búsqueda de proceso/Tarea**, sin mostrar ningún resultado de búsqueda.

#### Al introducir el ID de proceso/Tarea en el panel Detalles de proceso/Tarea {#by-entering-the-process-task-id-in-the-process-task-details-panel-br}

1. Vaya al panel **Detalles de proceso/Tarea**.

   ![details_nodes](assets/details_nodes.png)

1. En el cuadro de texto Id. de proceso/Tarea, introduzca el Id. de proceso/tarea.

   ![process_details-1](assets/process_details-1.png)

   Los campos del resultado de la consulta **Detalles de proceso/Tarea** son campos específicos de un proceso/tarea de AEM Forms.

   Para un proceso, el resultado de la consulta muestra los detalles de las tareas contenidas en el proceso.

   Para una tarea, el resultado de la consulta muestra los detalles de los formularios contenidos en la tarea.
