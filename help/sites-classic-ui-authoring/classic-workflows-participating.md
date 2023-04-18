---
title: Participación en flujos de trabajo
description: Los flujos de trabajo suelen incluir pasos que requieren que una persona realice una actividad en una página o un recurso. El flujo de trabajo selecciona un usuario o grupo para realizar la actividad y asigna un elemento de trabajo a esa persona o grupo.
uuid: 04dcc8f2-dc11-430f-b0ae-47ef2cb069a2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 1d7a4889-82c5-4096-8567-8f66215a8458
exl-id: 2f1a3a73-7a20-48c7-8f3e-54252f5fb71c
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 9%

---

# Participación en flujos de trabajo{#participating-in-workflows}

Los flujos de trabajo suelen incluir pasos que requieren que una persona realice una actividad en una página o un recurso. El flujo de trabajo selecciona un usuario o grupo para realizar la actividad y asigna un elemento de trabajo a esa persona o grupo.

## Procesamiento de los elementos de trabajo {#processing-your-work-items}

Puede realizar las siguientes acciones para procesar un elemento de trabajo:

* **Completar**

   Puede completar un elemento para permitir que el flujo de trabajo avance hasta el paso siguiente.

* **Delegar**

   Si se le ha asignado un paso, pero por cualquier razón no puede realizar ninguna acción, puede delegar el paso a otro usuario o grupo.

   Los usuarios que están disponibles para la delegación dependen de quién haya asignado el elemento de trabajo:

   * Si el elemento de trabajo se asignó a un grupo, los miembros del grupo estarán disponibles.
   * Si el elemento de trabajo se ha asignado a un grupo y luego se ha delegado a un usuario, los miembros del grupo y el grupo están disponibles.
   * Si el elemento de trabajo se asignó a un solo usuario, no se puede delegar el elemento de trabajo.

* **Retroceder**

   Si descubre que es necesario repetir un paso o una serie de pasos, puede retroceder. Esto le permite seleccionar un paso, que se produjo anteriormente en el flujo de trabajo, para volver a procesarlo. El flujo de trabajo vuelve al paso especificado y continúa desde allí.

## Participación en un flujo de trabajo {#participating-in-a-workflow}

### Notificaciones de acciones de flujo de trabajo asignadas {#notifications-of-assigned-workflow-actions}

Cuando se le asigna un elemento de trabajo (por ejemplo, **Aprobar contenido**), aparecen varias alertas o notificaciones:

* La variable **Estado** La columna de la consola Sitios web indica si una página está en un flujo de trabajo:

   ![workflow-status-1](assets/workflowstatus-1.png)

* Cuando se le asigna un elemento de trabajo como parte de un flujo de trabajo a usted o a un grupo al que pertenece, el elemento de trabajo aparece en la bandeja de entrada del flujo de trabajo AEM.

   ![workflowinbox](assets/workflowinbox.png)

### Finalización de una etapa de participante {#completing-a-participant-step}

Una vez realizada la acción indicada, puede completar el elemento de trabajo, lo que permite que el flujo de trabajo continúe. Utilice el siguiente procedimiento para completar el elemento de trabajo.

1. Seleccione el paso del flujo de trabajo y haga clic en el botón **Completar** en la barra de navegación superior.
1. En el cuadro de diálogo resultante, seleccione la opción **Paso siguiente**; es decir, el paso que se ejecutará a continuación. Una lista desplegable muestra todos los destinos adecuados. A **Comentario** también se puede introducir.

   ![flujo de trabajo completado](assets/workflowcomplete.png)

   El número de pasos que se muestran depende del diseño del modelo de flujo de trabajo.

1. Haga clic en **OK** para confirmar la acción.

### Delegación de una etapa de participante {#delegating-a-participant-step}

Utilice el siguiente procedimiento para delegar un elemento de trabajo.

1. Haga clic en el **Delegar** en la barra de navegación superior.
1. En el cuadro de diálogo, utilice la lista desplegable para seleccionar la **Usuario** para delegar el elemento de trabajo en. También puede agregar un **Comentario**.

   ![workflowdelegate](assets/workflowdelegate.png)

1. Haga clic en **OK** para confirmar la acción.

### Realización de una etapa hacia atrás en una etapa de participante {#performing-step-back-on-a-participant-step}

Utilice el siguiente procedimiento para volver al paso anterior.

1. Haga clic en el botón Retroceder en la barra de navegación superior.
1. En el cuadro de diálogo resultante, seleccione el paso anterior; es decir, el paso que se ejecutará a continuación, aunque sea un paso que se produzca anteriormente en el flujo de trabajo. Una lista desplegable muestra todos los destinos adecuados.

   ![screen_shot_2018-08-10at155325](assets/screen_shot_2018-08-10at155325.jpg)

1. Haga clic en OK para confirmar la acción.
