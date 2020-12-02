---
title: Participación en flujos de trabajo
seo-title: Participación en flujos de trabajo
description: Los flujos de trabajo incluyen normalmente los pasos que una persona debe llevar a cabo para realizar una actividad en una página o un recurso. El flujo de trabajo selecciona un usuario o grupo para llevar a cabo la actividad y asigna el elemento de trabajo a esa persona o grupo.
seo-description: Los flujos de trabajo incluyen normalmente los pasos que una persona debe llevar a cabo para realizar una actividad en una página o un recurso. El flujo de trabajo selecciona un usuario o grupo para llevar a cabo la actividad y asigna el elemento de trabajo a esa persona o grupo.
uuid: 04dcc8f2-dc11-430f-b0ae-47ef2cb069a2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 1d7a4889-82c5-4096-8567-8f66215a8458
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 98%

---


# Participación en flujos de trabajo{#participating-in-workflows}

Los flujos de trabajo incluyen normalmente los pasos que una persona debe llevar a cabo para realizar una actividad en una página o un recurso. El flujo de trabajo selecciona un usuario o grupo para llevar a cabo la actividad y asigna el elemento de trabajo a esa persona o grupo.

## Procesamiento de los elementos de trabajo {#processing-your-work-items}

Puede llevar a cabo las siguientes acciones para procesar un elemento de trabajo:

* **Completar**

   Puede completar un elemento para permitir que el flujo de trabajo vaya al paso siguiente.

* **Delegar**

   Si se le ha asignado un paso, pero por cualquier motivo no puede realizarlo, puede delegar el paso a otro usuario o grupo.

   Los usuarios que están disponibles para la delegación dependen de los usuarios a los que se ha asignado el elemento de trabajo:

   * Si el elemento de trabajo se ha asignado a un grupo, los miembros del grupo estarán disponibles.
   * Si el elemento de trabajo se ha asignado a un grupo y luego se ha delegado a un usuario, los miembros del grupo y el grupo están disponibles.
   * Si el elemento de trabajo se ha asignado a un único usuario, el elemento de trabajo no se puede delegar.

* **Retroceder**

   Si descubre que un paso o una serie de pasos deben repetirse, puede volver atrás. Esto le permite seleccionar un paso que ya se haya visto en el flujo de trabajo, para volver a realizar el procesamiento. El flujo de trabajo vuelve al paso especificado y continúa desde ahí.

## Participar en un flujo de trabajo {#participating-in-a-workflow}

### Notificaciones de las acciones del flujo de trabajo asignado {#notifications-of-assigned-workflow-actions}

Cuando se le asigna un elemento de trabajo (por ejemplo, **Aprobar contenido**), aparecen varias alertas o notificaciones:

* La columna **Estado** de la consola Sitios web indica si una página está en un flujo de trabajo.

   ![workflow-status-1](assets/workflowstatus-1.png)

* Cuando usted o el grupo al que pertenece tengan un elemento de trabajo asignado como parte de un flujo de trabajo, el elemento de trabajo aparecerá en la bandeja de entrada del flujo de trabajo de AEM.

   ![workflowinbox](assets/workflowinbox.png)

### Finalización de una etapa de participante {#completing-a-participant-step}

Una vez haya realizado la acción indicada, puede finalizar el elemento de trabajo; gracias a esto, el flujo de trabajo podrá continuar. Utilice el siguiente procedimiento para finalizar el elemento de trabajo.

1. Seleccione el paso del flujo de trabajo y haga clic en el botón **Completar** en la barra de navegación superior.
1. En el cuadro de diálogo que aparece, seleccione **Paso siguiente**; esto es, el paso que se ejecutará a continuación. Un menú desplegable muestra todos los destinos correctos. También se puede escribir un **comentario**.

   ![flujo de trabajo completado](assets/workflowcomplete.png)

   El número de pasos que se enumera depende del diseño del modelo de flujo de trabajo.

1. Haga clic en **Aceptar** para confirmar la acción.

### Delegación de una etapa de participante  {#delegating-a-participant-step}

Utilice el siguiente procedimiento para delegar el elemento de trabajo.

1. Haga clic en el botón **Delegar** en la barra de navegación superior.
1. En el cuadro de diálogo, utilice la lista desplegable para seleccionar el **Usuario** al que delegará el elemento de trabajo. También puede añadir un **comentario**.

   ![workflowdelegate](assets/workflowdelegate.png)

1. Haga clic en **Aceptar** para confirmar la acción.

### Realización de un paso hacia atrás en un paso de participante  {#performing-step-back-on-a-participant-step}

Utilice el siguiente procedimiento para volver al paso anterior.

1. Haga clic en el botón Atrás en la barra de navegación superior.
1. En el cuadro de diálogo que aparece, seleccione el paso anterior; esto es, el paso que se ejecutará a continuación, aunque sea un paso que ya se realizó con anterioridad en el flujo de trabajo. Un menú desplegable muestra todos los destinos correctos.

   ![screen_shot_2018-08-10at155325](assets/screen_shot_2018-08-10at155325.jpg)

1. Haga clic en Aceptar para confirmar la acción.

