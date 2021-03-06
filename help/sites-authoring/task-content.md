---
title: Uso de tareas
seo-title: Working with Tasks
description: Las tareas representan elementos de trabajo que tienen que implementarse en el contenido y se utilizan en los proyectos para determinar el nivel de conclusión de las tareas actuales
seo-description: Tasks represent items of work to be done on content and are used in projects to determine the level of completeness of current tasks
uuid: df4efb3f-8298-4159-acfe-305ba6b46791
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: 1b79d373-73f4-4228-b309-79e74d191f3e
exl-id: a0719745-8d67-44bc-92ba-9ab07f31f8d2
source-git-commit: 200b47070b7ead54ee54eea504bd960d4e0731d9
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 41%

---


# Uso de tareas {#working-with-tasks}

Las tareas representan elementos de trabajo que se deben realizar con respecto al contenido. Cuando se le asigna una tarea, aparece en su Bandeja de entrada de Workflow. Los elementos de tarea se pueden distinguir de los elementos de flujo de trabajo según el valor de **Tipo** para abrir el Navegador.

Las tareas también se utilizan en los proyectos para determinar el nivel de integridad del proyecto.

## Seguimiento del progreso del proyecto {#tracking-project-progress}

Para realizar un seguimiento del progreso del proyecto, fíjese en las tareas activas/terminadas en un proyecto representadas en el mosaico **Tareas**. Los elementos siguientes sirven para determinar el progreso del proyecto:

* **Mosaico de tareas:** En el mosaico de tareas, disponible en la página de detalles del proyecto, se muestra un progreso general del proyecto.

* **Lista de tareas:** Al hacer clic en el mosaico de tareas, se muestra una lista de tareas. Esta lista contiene información detallada sobre todas las tareas relacionadas con el proyecto.

Ambas opciones enumeran las tareas de flujo de trabajo, así como las tareas que crea directamente en el mosaico tareas .

### Mosaico Tareas {#task-tile}

Si un proyecto tiene tareas relacionadas, se muestra un mosaico de tareas dentro del proyecto. El mosaico de tareas muestra el estado actual del proyecto. Esto se basa en tareas existentes en el flujo de trabajo y no incluye ninguna tarea que se genere en el futuro al ritmo del progreso del flujo de trabajo. La información siguiente está visible en el mosaico Tareas:

* Porcentaje de tareas completadas
* Porcentaje de tareas activas
* Porcentaje de tareas caducadas

![mosaico Tareas](assets/project-tile-tasks.png)

### Ver o modificar las tareas en un proyecto {#viewing-or-modifying-the-tasks-in-a-project}

Además de realizar un seguimiento del progreso, puede que también desee ver más información sobre el proyecto o modificarlo.

#### Lista de tareas {#task-list}

Haga clic en el botón de puntos suspensivos en la parte inferior derecha del mosaico de tareas para mostrar la bandeja de entrada filtrada en las tareas relacionadas con el proyecto. Los detalles de la tarea se muestran junto con metadatos como la fecha de caducidad, el usuario asignado, la prioridad y el estado.

![Bandeja de entrada de tareas del proyecto](assets/project-tasks.png)

#### Detalles de la tarea {#task-details}

Para obtener más información sobre una tarea en particular, en la bandeja de entrada, toque o haga clic en la tarea para seleccionarla y, a continuación, toque o haga clic en **Apertura** en la barra de herramientas.

![Detalles de la tarea](assets/project-task-detail.png)

Puede ver, editar o agregar detalles a la tarea a través de diferentes pestañas.

* **Tarea** - Información general de tareas
* **Información del proyecto** - Resumen del proyecto al que está asociada la tarea
* **Ino de flujo de trabajo** : Resumen del flujo de trabajo con el que está asociada la tarea (si corresponde)
* **Comentarios** - Observaciones generales sobre la propia tarea

### Adición de tareas {#adding-tasks}

Puede añadir tareas nuevas a los proyectos. A continuación, estas tareas aparecen en el mosaico tareas y están disponibles en la bandeja de entrada de notificaciones para que sepa cuáles son sus tareas pendientes.

Para añadir una tarea:

1. En el proyecto, localice la variable **Tareas** tile
1. Toque o haga clic en el elemento adicional inferior situado en la parte superior derecha del mosaico y seleccione **Crear tarea**.
1. En el **Agregar tarea** , proporcione detalles de tareas como prioridad, usuario asignado y fecha de vencimiento.

   ![Adición de una tarea](assets/project-add-task.png)

1. Toque o haga clic **Submit**.

## Trabajo con tareas en la bandeja de entrada {#working-with-tasks-in-the-inbox}

En lugar de acceder a las tareas del proyecto desde el propio proyecto, puede acceder a ellas directamente desde la bandeja de entrada. La bandeja de entrada le ofrece una descripción general de las tareas de los distintos proyectos para que pueda comprender todo el flujo de trabajo.

Desde la bandeja de entrada, puede abrir las tareas y establecer el estado de la tarea. Las tareas también aparecen en la bandeja de entrada cuando se asignen a un grupo de usuarios al que pertenece. En ese caso, cualquier miembro del grupo puede realizar el trabajo y completar la tarea.

![Bandeja de entrada](assets/project-inbox.png)

Para completar una tarea, seleccione la tarea y haga clic en **Completar** en la barra de herramientas. Añada información a la tarea y, a continuación, haga clic en **Hecho**. Consulte la [bandeja de entrada](/help/sites-authoring/inbox.md) para obtener más información.
