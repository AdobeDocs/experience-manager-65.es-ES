---
title: Creación y administración de revisiones para recursos en formularios
seo-title: Creación y administración de revisiones para recursos en formularios
description: 'Una revisión es un mecanismo que permite a uno o más revisores comentar un recurso que está disponible en un formulario. '
seo-description: 'Una revisión es un mecanismo que permite a uno o más revisores comentar un recurso que está disponible en un formulario. '
uuid: 45c7ff56-3fa8-4a0f-8597-05404e547282
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: d8c1c507-a6c4-44f5-be01-ee902bc28410
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Creación y administración de revisiones para recursos en formularios{#creating-and-managing-reviews-for-assets-in-forms}

## Crítica {#review}

Una revisión es un mecanismo que permite a uno o más revisores comentar un recurso que está disponible en un formulario.

## Configuración de una revisión {#setting-up-a-review}

1. Vaya a la ficha Formularios y seleccione un formulario.
1. Si el recurso no tiene una revisión en curso, aparecerá un icono Iniciar revisión ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) en la barra de acciones. Haga clic en el icono Iniciar revisión ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) .
1. Indique la siguiente información:

   * Nombre de revisión: Obligatorio, puede contener caracteres alfanuméricos, guiones o subrayado.
   * Revisar descripción: Opcional, descripción del propósito/contenido que se va a revisar.
   * Plazo de revisión: Opcional: la fecha en la que finaliza la revisión. Cuando se ha superado la fecha límite, la tarea aparece como &#39;Vencido&#39;.
   * Revisores: Un mínimo de uno es obligatorio. Utilice el cuadro combinado para agregar revisores. Al escribir un nombre se muestran todos los nombres coincidentes; seleccione un nombre y haga clic en Agregar.

1. Complete todos los detalles restantes y haga clic en Iniciar.

### Acciones que se producen cuando se configura una revisión {#actions-that-occur-when-a-review-is-set-up}

Esta sección describe lo que sucede cuando se crea o configura una revisión.

1. Se crea una nueva tarea de revisión y se asigna al iniciador de la revisión.
1. A todos los revisores se les asigna una tarea de revisión. La tarea aparece en la sección Notificaciones. Un revisor puede hacer clic en una notificación o ir a la Bandeja de entrada para ver la tarea. Un revisor puede hacer clic para abrir la tarea de revisión, ver el formulario y empezar a agregar comentarios.

   ![Alerta de notificación del revisor](assets/noti.png)

   Alerta de notificación del revisor

1. El cuadro de comentarios está disponible para el iniciador y los revisores del recurso. Otros pueden ver los comentarios, pero no pueden escribirlos.

## Administración de una revisión {#managing-a-review}

>[!NOTE]
>
>Sólo se pueden modificar las revisiones en curso. Las revisiones completadas no se pueden modificar.

1. Vaya a la ficha Formularios y seleccione un formulario.

1. Si un recurso tiene una revisión en curso y usted es el iniciador de la revisión, aparecerá un icono Administrar revisión ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) en la barra de acciones. Solo el iniciador de revisión puede administrar (actualizar/finalizar) la revisión.

   Haga clic en el ![icono Administrar revisión aem6forms_review_chat_](assets/aem6forms_review_chat_comment.png)comment.

   Para usuarios que no sean el iniciador, el icono Administrar revisión está deshabilitado.

1. Se obtiene una pantalla que muestra información:

   * **Nombre** de revisión: No se puede editar.

   * **Revisar descripción**: Disponible para edición.

   * **Plazo** de revisión: Disponible para edición. Se puede modificar la fecha y la hora límite para cualquier fecha y hora posteriores a la fecha y hora actuales.

   * **Revisores**: Disponible para edición. Puede agregar o eliminar revisores. Si una tarea ha vencido, puede agregar revisores sólo después de extender la fecha límite más allá de la fecha actual.

1. Edite los campos necesarios y haga clic en Actualizar.

   ![Revisar estado actualizado en el Administrador de tareas](assets/tskmgr.png)

   Revisar estado actualizado en el Administrador de tareas

1. Para finalizar la revisión, haga clic en Finalizar.

### Acciones que se producen cuando se modifica una revisión {#actions-that-occur-when-a-review-is-modified}

En esta sección se describe lo que sucede con la modificación o finalización de la revisión:

1. Si se modifica la descripción de la revisión, se actualiza la tarea correspondiente de los revisores y del iniciador.
1. Si se modifica la fecha límite de revisión, la tarea correspondiente para los revisores se actualiza con la nueva fecha.

1. Si se elimina un revisor:

   ![Eliminación de un revisor](assets/removeduser.png)

   Eliminación de un revisor

   1. Si está incompleta, la tarea asignada se termina.
   1. El revisor ya no puede realizar comentarios sobre el recurso.

1. Si se agrega un revisor:

   ![Adición de un revisor](assets/addedreviewer.png)

   Adición de un revisor

   1. Se crea una tarea de revisión y se asigna al revisor recién agregado.
   1. El revisor recién agregado puede agregar comentarios para el recurso.

1. Cuando finaliza una revisión:

   1. **Revisores**: Para cada revisor, se termina la tarea incompleta relacionada con la revisión. La tarea ya no aparece como &#39;Pendiente&#39; en la sección Notificaciones del revisor.
   1. **Iniciador**: La tarea asignada al iniciador de la revisión está marcada como completada. La tarea se elimina de la sección Notificación del iniciador de la revisión.
   1. **Todo**: La revisión aparece en la sección Reseñas anteriores. No se pueden añadir más comentarios.

