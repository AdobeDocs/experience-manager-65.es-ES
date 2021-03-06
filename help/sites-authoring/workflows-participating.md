---
title: Participación en flujos de trabajo
seo-title: Participación en flujos de trabajo
description: Los flujos de trabajo incluyen normalmente los pasos que una persona debe llevar a cabo para realizar una actividad en una página o un recurso.
seo-description: Los flujos de trabajo incluyen normalmente los pasos que una persona debe llevar a cabo para realizar una actividad en una página o un recurso.
uuid: 15d56bcc-1e84-4cc0-8b71-7fb906cd7ff7
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: f170613c-329e-446b-9ac3-350615f1bfb6
docset: aem65
translation-type: tm+mt
source-git-commit: bcb1840d23ae538c183eecb0678b6a75d346aa50
workflow-type: tm+mt
source-wordcount: '1545'
ht-degree: 77%

---


# Participación en flujos de trabajo{#participating-in-workflows}

Los flujos de trabajo incluyen normalmente los pasos que una persona debe llevar a cabo para realizar una actividad en una página o un recurso. El flujo de trabajo selecciona un usuario o grupo para llevar a cabo la actividad y asigna el elemento de trabajo a esa persona o grupo. El usuario recibe la notificación y puede tomar las medidas adecuadas:

* [Visualización de notificaciones](#notifications-of-available-workflow-actions) 
* [Finalización de una etapa de participante](#completing-a-participant-step) 
* [Delegación de una etapa de participante](#delegating-a-participant-step) 
* [Realización de una etapa hacia atrás en una etapa de participante](#performing-step-back-on-a-participant-step) 
* [Apertura de un elemento de flujo de trabajo para ver los detalles (y tomar medidas)](#opening-a-workflow-item-to-view-details-and-take-actions) 
* [Visualización de la carga útil del flujo de trabajo (varios recursos)](#viewing-the-workflow-payload-multiple-resources) 

## Notificaciones de las acciones de flujo de trabajo disponibles {#notifications-of-available-workflow-actions}

Cuando se le asigna un elemento de trabajo (por ejemplo, **Aprobar contenido**), aparecen varias alertas o notificaciones:

* El indicador de [notificaciones](/help/sites-authoring/inbox.md) (barra de herramientas) se incrementará:

   ![](do-not-localize/wf-57.png)

* El elemento figurará en la [Bandeja de entrada](/help/sites-authoring/inbox.md) de notificaciones:

   ![wf-58](assets/wf-58.png)

* Cuando utilice el editor de página, la barra de estado mostrará lo siguiente:

   * El nombre de los flujos de trabajo que se aplican a la página; por ejemplo, solicitud de activación.
   * Las acciones disponibles para el usuario actual para la etapa actual del flujo de trabajo; por ejemplo, Completar, Delegar, Ver detalles.
   * El número de flujos de trabajo en los que se encuentra la página. Puede hacer lo siguiente:

      * Usar las flechas izquierda/derecha para navegar por la información de estado de los distintos flujos de trabajo.
      * Hacer clic o pulsar en el número real para abrir una lista desplegable de todos los flujos de trabajo aplicables y, a continuación, seleccionar el flujo de trabajo que desee visualizar en la barra de estado.

   ![wf-59](assets/wf-59.png)

   >[!NOTE]
   >
   >La barra de estado solo está visible para los usuarios con privilegios de flujo de trabajo; por ejemplo, miembros del grupo `workflow-users`.
   >
   >
   >Las acciones se muestran cuando el usuario actual participa directamente en el paso actual del flujo de trabajo.

* Cuando la opción **Escala de tiempo** está abierta para el recurso, se mostrará la etapa del flujo de trabajo. Al hacer clic o pulsar en el titular de alerta, se mostrarán las acciones disponibles:

   ![screen-shot_2019-03-05at120453](assets/screen-shot_2019-03-05at120453.png)

### Finalización de una etapa de participante {#completing-a-participant-step}

Puede completar un elemento para permitir que el flujo de trabajo vaya al paso siguiente.

En esta acción, puede indicar lo siguiente:

* **Etapa siguiente**: la etapa siguiente que se debe llevar a cabo. Se puede seleccionar una de la lista que se proporciona.
* **Comentario**: si fuera necesario

Puede completar una etapa de participante desde las ubicaciones siguientes:

* [la Bandeja de entrada](#completing-a-participant-step-inbox)
* [el Editor de página](#completing-a-participant-step-page-editor)
* [Escala de tiempo](#completing-a-participant-step-timeline)
* al [abrir un elemento de flujo de trabajo para ver los detalles](#opening-a-workflow-item-to-view-details-and-take-actions).

#### Finalización de una etapa de participante: bandeja de entrada  {#completing-a-participant-step-inbox}

Utilice el siguiente procedimiento para completar el elemento de trabajo:

1. Abra la **[Bandeja de entrada AEM](/help/sites-authoring/inbox.md)**.
1. Seleccione el elemento de flujo de trabajo en el que desee realizar la acción (pulsar o hacer clic en la miniatura).
1. Seleccione **Completar** en la barra de herramientas.
1. Se abre el cuadro de diálogo **Completar elemento de trabajo**. Seleccione el **Paso siguiente** en el selector desplegable y agregue un **Comentario** si es necesario.
1. Utilice **Aceptar** para completar el paso (o **Cancelar** para cancelar la acción).

#### Finalización de una etapa de participante: editor de la página {#completing-a-participant-step-page-editor}

Utilice el siguiente procedimiento para completar el elemento de trabajo:

1. Abra la [página para editarla](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing).
1. Seleccione **Completar** en la barra de estado de la parte superior.
1. Se abre el cuadro de diálogo **Completar elemento de trabajo**. Seleccione el **Paso siguiente** en el selector desplegable y agregue un **Comentario** si es necesario.
1. Utilice **Aceptar** para completar el paso (o **Cancelar** para cancelar la acción).

#### Finalización de una etapa de participante: escala de tiempo {#completing-a-participant-step-timeline}

También puede utilizar la escala de tiempo para completar y hacer avanzar una etapa:

1. Seleccione la página requerida y abra **Línea de tiempo** (o abra **Línea de tiempo** y seleccione la página):

   ![screen-shot_2019-03-05at120744](assets/screen-shot_2019-03-05at120744.png)

1. Haga clic o pulse en el titular de alerta para mostrar las acciones disponibles. Seleccione **Avanzar**:

   ![screen-shot_2019-03-05at120453-1](assets/screen-shot_2019-03-05at120453-1.png)

1. Según el flujo de trabajo, puede seleccionar la siguiente etapa:

   ![screen-shot_2019-03-05at120905](assets/screen-shot_2019-03-05at120905.png)

1. Seleccione **Avanzar** para confirmar la acción.

### Delegación de una etapa de participante  {#delegating-a-participant-step}

Si se le ha asignado un paso, pero por cualquier motivo no puede realizarlo, puede delegar el paso a otro usuario o grupo.

Los usuarios que están disponibles para la delegación dependen de los usuarios a los que se ha asignado el elemento de trabajo:

* Si el elemento de trabajo se ha asignado a un grupo, los miembros del grupo estarán disponibles.
* Si el elemento de trabajo se ha asignado a un grupo y luego se ha delegado a un usuario, los miembros del grupo y el grupo están disponibles.
* Si el elemento de trabajo se ha asignado a un único usuario, el elemento de trabajo no se puede delegar.

En esta acción, puede indicar lo siguiente:

* **Usuario**: el usuario al que desea delegar el elemento de trabajo. Puede seleccionarlo de una lista proporcionada
* **Comentario**: si fuera necesario

Puede delegar una etapa de participante desde las ubicaciones siguientes:

* [la Bandeja de entrada](#delegating-a-participant-step-inbox)
* [el Editor de página](#delegating-a-participant-step-page-editor)
* [Escala de tiempo](#delegating-a-participant-step-timeline)
* al [abrir un elemento de flujo de trabajo para ver los detalles](#opening-a-workflow-item-to-view-details-and-take-actions).

#### Delegación de una etapa de participante: bandeja de entrada  {#delegating-a-participant-step-inbox}

Utilice el siguiente procedimiento para delegar un elemento de trabajo:

1. Abra la **[Bandeja de entrada AEM](/help/sites-authoring/inbox.md)**.
1. Seleccione el elemento de flujo de trabajo en el que desee realizar la acción (pulsar o hacer clic en la miniatura).
1. Seleccione **Delegar** en la barra de herramientas.
1. Se abrirá el cuadro de diálogo. Especifique el **usuario** en el selector desplegable (también puede ser un grupo) y agregue un **comentario** si es necesario.
1. Utilice **Aceptar** para completar el paso (o **Cancelar** para cancelar la acción).

#### Delegación de una etapa de participante: editor de la página {#delegating-a-participant-step-page-editor}

Utilice el siguiente procedimiento para delegar un elemento de trabajo:

1. Abra la [página para editarla](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing).
1. Seleccione **Delegar** en la barra de estado de la parte superior.
1. Se abrirá el cuadro de diálogo. Especifique el **usuario** en el selector desplegable (también puede ser un grupo) y agregue un **comentario** si es necesario.
1. Utilice **Aceptar** para completar el paso (o **Cancelar** para cancelar la acción).

#### Delegación de una etapa de participante: escala de tiempo {#delegating-a-participant-step-timeline}

También puede utilizar la escala de tiempo para delegar o asignar una etapa:

1. Seleccione la página requerida y abra **Línea de tiempo** (o abra **Línea de tiempo** y seleccione la página).
1. Haga clic o pulse en el titular de alerta para mostrar las acciones disponibles. Seleccione **Cambiar asignación**:

   ![screen-shot_2019-03-05at120453-2](assets/screen-shot_2019-03-05at120453-2.png)

1. Especifique un nuevo usuario para la asignación:

   ![screen-shot_2019-03-05at121025](assets/screen-shot_2019-03-05at121025.png)

1. Seleccione **Asignar** para confirmar la acción.

### Realización de un paso hacia atrás en un paso de participante {#performing-step-back-on-a-participant-step}

Si descubre que un paso o una serie de pasos deben repetirse, puede volver atrás. Esto le permite seleccionar un paso que ya se haya visto en el flujo de trabajo, para volver a realizar el procesamiento. El flujo de trabajo vuelve al paso especificado y continúa desde ahí.

En esta acción, puede indicar lo siguiente:

* **Etapa anterior:** la etapa a la que se va a regresar. Se puede seleccionar una de la lista que se proporciona
* **Comentario**: si fuera necesario

Puede volver a una etapa anterior durante cualquier etapa de participante desde las ubicaciones siguientes:

* [la Bandeja de entrada](#performing-step-back-on-a-participant-step-inbox)
* [el Editor de página](#performing-step-back-on-a-participant-step-page-editor)
* [Escala de tiempo](#performing-step-back-on-a-participant-step-timeline)
* al [abrir un elemento de flujo de trabajo para ver los detalles](#opening-a-workflow-item-to-view-details-and-take-actions).

#### Realización de una etapa hacia atrás en una etapa de participante: bandeja de entrada  {#performing-step-back-on-a-participant-step-inbox}

Utilice el siguiente procedimiento para volver a la etapa anterior:

1. Abra la **[Bandeja de entrada AEM](/help/sites-authoring/inbox.md)**.
1. Seleccione el elemento de flujo de trabajo en el que desee realizar la acción (pulsar o hacer clic en la miniatura).
1. Seleccione **Retroceder** para abrir el cuadro de diálogo.

1. Especifique un valor en **Etapa anterior** y añada un comentario en el campo **Comentario**, si fuera necesario.
1. Utilice **Aceptar** para completar el paso (o **Cancelar** para cancelar la acción).

#### Realización de una etapa hacia atrás en una etapa de participante: editor de página {#performing-step-back-on-a-participant-step-page-editor}

Utilice el siguiente procedimiento para volver a la etapa anterior:

1. Abra la [página para editarla](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing).
1. Seleccione **Retroceder** en la barra de estado de la parte superior.
1. Especifique un valor en **Etapa anterior** y añada un comentario en el campo **Comentario**, si fuera necesario.
1. Utilice **Aceptar** para completar el paso (o **Cancelar** para cancelar la acción).

#### Realización de una etapa hacia atrás en una etapa de participante: escala de tiempo {#performing-step-back-on-a-participant-step-timeline}

También puede utilizar la escala de tiempo para restablecer hasta una etapa anterior:

1. Seleccione la página requerida y abra **Línea de tiempo** (o abra **Línea de tiempo** y seleccione la página).
1. Haga clic o pulse en el titular de alerta para mostrar las acciones disponibles. Seleccione **Restablecer**:

   ![screen-shot_2019-03-05at121131](assets/screen-shot_2019-03-05at121131.png)

1. Especifique la etapa a la que debe restablecerse el flujo de trabajo:

   ![screen-shot_2019-03-05at121158](assets/screen-shot_2019-03-05at121158.png)

1. Seleccione **Revertir** para confirmar la acción.

### Apertura de un elemento de flujo de trabajo a los detalles de Vista (y acciones) {#opening-a-workflow-item-to-view-details-and-take-actions}

Visualice los detalles del elemento de trabajo del flujo de trabajo y tome las medidas adecuadas.

Los detalles del flujo de trabajo se muestran en fichas y las acciones adecuadas están disponibles en la barra de herramientas:

* Ficha **ELEMENTO DE TRABAJO:**

   ![wf-72](assets/wf-72.png)

* **INFORMACIÓN DEL** FLUJO DE TRABAJOficha:

   ![wf-73](assets/wf-73.png)

   Si se han configurado [etapas de flujo de trabajo](/help/sites-developing/workflows.md#workflow-stages) para el modelo, puede ver el progreso según los siguientes elementos:

   ![wf-107](assets/wf-107.png)

* **** COMENTARIOSficha:

   ![wf-75](assets/wf-75.png)

Puede abrir los detalles del elemento de trabajo desde las ubicaciones siguientes:

* [la Bandeja de entrada](#performing-step-back-on-a-participant-step-inbox)
* [el Editor de página](#performing-step-back-on-a-participant-step-page-editor)

#### Apertura de los detalles del flujo de trabajo: bandeja de entrada  {#opening-workflow-details-inbox}

Para abrir un elemento de flujo de trabajo y ver los detalles:

1. Abra la **[Bandeja de entrada AEM](/help/sites-authoring/inbox.md)**.
1. Seleccione el elemento de flujo de trabajo en el que desee realizar la acción (pulsar o hacer clic en la miniatura).
1. Seleccione **Abrir** para abrir las fichas de información.

1. Si fuera necesario, seleccione la acción adecuada, proporcione los detalles necesarios y confirme con **Aceptar** (o **Cancelar**).
1. Utilice **Guardar** o **Cancelar** para salir.

#### Apertura de los detalles del flujo de trabajo: editor de página {#opening-workflow-details-page-editor}

Para abrir un elemento de flujo de trabajo y ver los detalles:

1. Abra la [página para editarla](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing).
1. Seleccione **Detalles de Vista** en la barra de estado para abrir las fichas de información.

1. Si fuera necesario, seleccione la acción adecuada, proporcione los detalles necesarios y confirme con **Aceptar** (o **Cancelar**).
1. Utilice **Guardar** o **Cancelar** para salir.

### Visualización de la carga útil del flujo de trabajo (varios recursos) {#viewing-the-workflow-payload-multiple-resources}

Puede ver los detalles de la carga útil asociada con la instancia de flujo de trabajo. Inicialmente, se muestran los recursos del paquete y luego puede explorar en profundidad para mostrar las páginas individuales.

Para ver la carga útil y los recursos de la instancia de flujo de trabajo:

1. Abra la **[Bandeja de entrada AEM](/help/sites-authoring/inbox.md)**.
1. Seleccione el elemento de flujo de trabajo en el que desee realizar la acción (pulsar o hacer clic en la miniatura).
1. Seleccione **Carga útil de Vista** en la barra de herramientas para abrir el cuadro de diálogo.

   Dado que un paquete de flujo de trabajo es simplemente una colección de punteros a rutas dentro del repositorio, puede añadir, quitar o modificar las entradas aquí para ajustar los elementos a los que el paquete de flujo de trabajo hace referencia. Utilice el componente **Definición de medios** para añadir nuevas entradas.

   ![wf-78](assets/wf-78.png)

1. Los vínculos se pueden utilizar para abrir las páginas individuales.
