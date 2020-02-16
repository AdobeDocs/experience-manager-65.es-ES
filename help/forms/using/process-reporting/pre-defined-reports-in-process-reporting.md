---
title: Informes predefinidos en informes de proceso
seo-title: Informes predefinidos en informes de proceso
description: Consulte los datos de proceso de AEM Forms en JEE para crear informes sobre procesos de larga ejecución, duración del proceso y volumen del flujo de trabajo
seo-description: Consulte los datos de proceso de AEM Forms en JEE para crear informes sobre procesos de larga ejecución, duración del proceso y volumen del flujo de trabajo
uuid: 704a8886-90ea-4793-a3fc-f998f878c928
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d93375e-ec37-4445-96ea-d315676787b4
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Informes predefinidos en informes de proceso {#pre-defined-reports-in-process-reporting}

## Informes predefinidos en los informes en curso {#pre-defined-reports-in-process-reporting-1}

Los informes de procesos de AEM Forms se envían con los siguientes informes *listos para usar* :

* **[Procesos](#long-running-processes)**de larga duración: Un informe de todos los procesos de AEM Forms que tardaron más de un tiempo en completarse
* **[Gráfico](#process-duration-report)**de duración del proceso: Informe de un proceso de AEM Forms especificado por duración
* **[Volumen](#workflow-volume-report)**de flujo de trabajo: Un informe de las instancias en ejecución y completadas del proceso especificado por fecha

## Procesos de larga duración {#long-running-processes}

El informe Procesos de larga ejecución muestra los procesos de AEM Forms que han tardado más de un tiempo en completarse.

### Para ejecutar un informe de proceso de larga ejecución {#to-execute-a-long-running-process-report}

1. Para ver la lista de informes predefinidos en Informes de procesos, en la vista de árbol de informes **de** procesos, haga clic en el nodo **Informes **.
1. Haga clic en el nodo del informe Procesos **de ejecución** prolongada.

   ![long_running_node](assets/long_running_node.png)

   Al seleccionar un informe, se muestra el panel Parámetros **del** informe a la derecha de la vista de árbol.

   ![panel Parámetros del informe de procesos en ejecución prolongada](assets/report_parameters_panel.png)

   Parámetros:

   * **Duración**(*obligatoria*): Especifique una duración y una unidad de tiempo. Muestre todos los procesos de AEM Forms que se hayan ejecutado durante más tiempo del especificado.
   * **Iniciado después** (*opcional*): Seleccione una fecha. Filtre el informe para mostrar las instancias de proceso que comenzaron después de la fecha especificada.
   * **Iniciado antes** (*opcional*): Seleccione una fecha. Filtre el informe para mostrar las instancias de proceso que comenzaron antes de la fecha especificada.

1. Haga clic en **Ir** para ejecutar el informe.

   El informe se muestra en el panel **Informe **A a la derecha de la ventana Informes **de** procesos.

   ![long_running_process](assets/long_running_processes.png)

   Utilice las opciones de la esquina superior derecha del panel **Informe **Para realizar las siguientes operaciones en el informe.

   * **Actualizar**: Actualiza el informe con los datos más recientes que se encuentran en el almacenamiento
   * **Cambiar el color** de la leyenda: Seleccionar y cambiar el color de la leyenda del informe
   * **Exportar a CSV**: Exportar y descargar los datos del informe en un archivo separado por comas

## Informe de duración del proceso {#process-duration-report}

El informe Duración del proceso muestra el número de instancias de un proceso de Forms según el número de días que se ha ejecutado cada instancia.

### Para ejecutar un informe de duración del proceso {#to-execute-a-process-duration-report}

1. Para ver los informes predefinidos en Informes de procesos, en la vista de árbol de Informes **de** procesos, haga clic en el nodo **Informes **Nodo.
1. Haga clic en el nodo del informe **Duración** de los procesos.

   ![process_duration_node](assets/process_duration_node.png)

   Al seleccionar un informe, se muestra el panel Parámetros **del** informe a la derecha de la vista de árbol.

   ![panel Parámetros del informe de procesos en ejecución prolongada](assets/process_duration_params.png)

   Parámetros:

   * **Seleccionar proceso **(*obligatorio*): Seleccione un proceso de AEM Forms.

1. Haga clic en **Ir **para ejecutar el informe.

   El informe se muestra en el panel **Informe **A a la derecha de la ventana Informes de procesos.

   ![process_duration_report](assets/process_duration_report.png)

   Utilice las opciones de la esquina superior derecha del panel **Informe **Para realizar las siguientes operaciones en el informe.

   * **Actualizar**: Actualiza el informe con los datos más recientes que se encuentran en el almacenamiento
   * **Cambiar el color** de la leyenda: Seleccionar y cambiar el color de la leyenda del informe
   * **Exportar a CSV**: Exportar y descargar los datos del informe en un archivo separado por comas

## Informe de volumen de flujo de trabajo {#workflow-volume-report}

El informe Volumen del flujo de trabajo muestra el número de instancias que se están ejecutando y completadas de un proceso de AEM Forms por día calendario.

### Para ejecutar un informe de volumen de flujo de trabajo {#to-execute-a-workflow-volume-report}

1. Para ver los informes predefinidos en Informes de procesos, en la vista de árbol **Informes de procesos **haga clic en el nodo **Informes **1.
1. Haga clic en el nodo del informe Volumen **de** flujo de trabajo.

   ![workflow_volume_node](assets/workflow_volume_node.png)

   Al seleccionar un informe, se muestra el panel Parámetros **del** informe a la derecha de la vista de árbol.

   ![panel Parámetros del informe de procesos en ejecución prolongada](assets/workflow_volume_params.png)

   Parámetros:

   * **Seleccionar proceso **(*obligatorio*): Seleccione un proceso de AEM Forms.

   * **Iniciado después** (*opcional*): Seleccione una fecha. Filtra el informe para mostrar las instancias de proceso que comenzaron después de la fecha especificada.

   * **Iniciado antes** (*opcional*): Seleccione una fecha. Filtra el informe para mostrar las instancias de proceso que comenzaron antes de la fecha especificada.

1. Haga clic en **Ir **para ejecutar el informe.

   El informe se muestra en el panel **Informe **A a la derecha de la ventana Informes **de** procesos.

   ![workflow_volume_report](assets/workflow_volume_report.png)

   Utilice las opciones de la esquina superior derecha del panel **Informe **Para realizar las siguientes operaciones en el informe.

   * **Actualizar**: Actualiza el informe con los datos más recientes que se encuentran en el almacenamiento
   * **Cambiar el color** de la leyenda: Seleccionar y cambiar el color de la leyenda del informe
   * **Exportar a CSV**: Exportar y descargar los datos del informe en un archivo separado por comas

[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
