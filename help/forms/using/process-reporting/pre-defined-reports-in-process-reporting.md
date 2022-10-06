---
title: Informes predefinidos en informes de proceso
seo-title: Pre-defined reports in Process Reporting
description: Consulta de AEM Forms sobre datos de proceso JEE para crear informes sobre procesos de larga duración, duración del proceso y volumen del flujo de trabajo
seo-description: Query for AEM Forms on JEE process data to create reports on long running processes, Process duration, and Workflow volume
uuid: 704a8886-90ea-4793-a3fc-f998f878c928
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d93375e-ec37-4445-96ea-d315676787b4
docset: aem65
exl-id: 34e55676-6332-4616-aecc-bcc8cc1e8a29
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---

# Informes predefinidos en informes de proceso {#pre-defined-reports-in-process-reporting}

## Informes predefinidos en proceso de informes {#pre-defined-reports-in-process-reporting-1}

Los informes de procesos de AEM Forms se envían con lo siguiente *lista para usar* informes:

* **[Procesos de larga duración](#long-running-processes)**: Un informe de todos los procesos de AEM Forms que tardaron más de un tiempo especificado en completarse.
* **[Gráfico de duración del proceso](#process-duration-report)**: Informe de un proceso AEM Forms especificado por duración
* **[Volumen del flujo de trabajo](#workflow-volume-report)**: Un informe de las instancias en ejecución y completadas del proceso especificado por fecha

## Procesos de larga duración {#long-running-processes}

El informe de procesos de larga duración muestra los procesos de AEM Forms que han tardado más de un tiempo en completarse.

### Para ejecutar un informe de proceso de larga duración {#to-execute-a-long-running-process-report}

1. Para ver la lista de informes predefinidos en Informes de procesos, en la **Informes de procesos** vista de árbol, haga clic en la **Informes** nodo .
1. Haga clic en el **Procesos de larga duración** nodo del informe.

   ![long_running_node](assets/long_running_node.png)

   Al seleccionar un informe, la variable **Parámetros de informe** se muestra a la derecha de la vista de árbol.

   ![panel de parámetros del informe de procesos de larga ejecución](assets/report_parameters_panel.png)

   Parámetros:

   * **Duración** (*mandatory*): Especifique una duración y una unidad de tiempo. Muestre todos los procesos de AEM Forms que se hayan ejecutado durante más de la duración especificada.
   * **Comenzar después** (*opcional*): Seleccione una fecha. Filtre el informe para mostrar las instancias de proceso que se iniciaron después de la fecha especificada.
   * **Primeros pasos** (*opcional*): Seleccione una fecha. Filtre el informe para mostrar las instancias de proceso que se iniciaron antes de la fecha especificada.

1. Haga clic en **Ir** para ejecutar el informe.

   El informe se muestra en la sección **Informe** panel de la derecha del **Informes de procesos** ventana.

   ![long_running_processes](assets/long_running_processes.png)

   Utilice las opciones de la esquina superior derecha de la variable **Informe** para realizar las siguientes operaciones en el informe.

   * **Actualizar**: Actualiza el informe con los datos más recientes en el almacenamiento
   * **Cambiar el color de la leyenda**: Seleccionar y cambiar el color del pie de ilustración del informe
   * **Exportar a CSV**: Exportar y descargar los datos del informe en un archivo separado por comas

## Informe de duración del proceso  {#process-duration-report}

El informe Duración del proceso muestra el número de instancias de un proceso de Forms por número de días que cada instancia se ha ejecutado.

### Para ejecutar un informe de duración del proceso {#to-execute-a-process-duration-report}

1. Para ver los informes predefinidos en Informes de procesos, en la **Informes de procesos** vista de árbol, haga clic en la **Informes** nodo .
1. Haga clic en el **Duración de los procesos** nodo del informe.

   ![process_duration_node](assets/process_duration_node.png)

   Al seleccionar un informe, la variable **Parámetros de informe** se muestra a la derecha de la vista de árbol.

   ![panel de parámetros del informe de procesos de larga ejecución](assets/process_duration_params.png)

   Parámetros:

   * **Seleccionar proceso** (*mandatory*): Seleccione un proceso de AEM Forms.

1. Haga clic en **Ir** para ejecutar el informe.

   El informe se muestra en la sección **Informe** a la derecha de la ventana Process Reporting.

   ![process_duration_report](assets/process_duration_report.png)

   Utilice las opciones de la esquina superior derecha de la variable **Informe** para realizar las siguientes operaciones en el informe.

   * **Actualizar**: Actualiza el informe con los datos más recientes en el almacenamiento
   * **Cambiar el color de la leyenda**: Seleccionar y cambiar el color del pie de ilustración del informe
   * **Exportar a CSV**: Exportar y descargar los datos del informe en un archivo separado por comas

## Informe Volumen del flujo de trabajo {#workflow-volume-report}

El informe Volumen del flujo de trabajo muestra el número de instancias ejecutadas y completadas actualmente de un proceso de AEM Forms por día del calendario.

### Para ejecutar un informe de volumen de flujo de trabajo {#to-execute-a-workflow-volume-report}

1. Para ver los informes predefinidos en Informes de procesos, en la **Informes de procesos** vista de árbol, haga clic en la **Informes** nodo .
1. Haga clic en el **Volumen del flujo de trabajo** nodo del informe.

   ![workflow_volume_node](assets/workflow_volume_node.png)

   Al seleccionar un informe, la variable **Parámetros de informe** se muestra a la derecha de la vista de árbol.

   ![panel de parámetros del informe de procesos de larga ejecución](assets/workflow_volume_params.png)

   Parámetros:

   * **Seleccionar proceso** (*mandatory*): Seleccione un proceso de AEM Forms.

   * **Comenzar después** (*opcional*): Seleccione una fecha. Filtra el informe para mostrar las instancias de proceso que se iniciaron después de la fecha especificada.

   * **Primeros pasos** (*opcional*): Seleccione una fecha. Filtra el informe para mostrar las instancias de proceso que se iniciaron antes de la fecha especificada.

1. Haga clic en **Ir** para ejecutar el informe.

   El informe se muestra en la sección **Informe** panel de la derecha del **Informes de procesos** ventana.

   ![workflow_volume_report](assets/workflow_volume_report.png)

   Utilice las opciones de la esquina superior derecha de la variable **Informe** para realizar las siguientes operaciones en el informe.

   * **Actualizar**: Actualiza el informe con los datos más recientes en el almacenamiento
   * **Cambiar el color de la leyenda**: Seleccionar y cambiar el color del pie de ilustración del informe
   * **Exportar a CSV**: Exportar y descargar los datos del informe en un archivo separado por comas
