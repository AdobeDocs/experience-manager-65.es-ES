---
title: Guardar una tarea o un formulario como borrador
seo-title: Guardar una tarea o un formulario como borrador
description: Pasos para guardar una copia borrador de una tarea o un formulario en la aplicación de AEM Forms
seo-description: Pasos para guardar una copia borrador de una tarea o un formulario en la aplicación de AEM Forms
uuid: 1192d2c2-05a4-4a96-9015-e56111aa2646
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 9950288c-b5a2-4945-afad-be9ce2abc8e9
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---


# Guardar una tarea o un formulario como borrador {#saving-a-task-or-form-as-a-draft}

La opción Guardar como borrador guarda una instantánea de una tarea o formulario junto con los datos rellenados en el formulario asociado. También puede crear un borrador a partir de una plantilla. Los borradores se guardan en el dispositivo móvil y se sincronizan con el servidor de Adobe Experience Manager Forms para una recuperación posterior.

Puede [actualizar el formulario](/help/forms/using/working-with-form.md), [anotarlo](/help/forms/using/add-attachments.md) con fotografías y garabatos. A medida que continúa actualizando un formulario, se recomienda guardarlo como borrador. En el caso de situaciones en las que decida enviar un formulario rellenado más adelante, es útil guardarlo como borrador.

Para habilitar la función Guardar como borrador para formularios guardados en el portal de formularios, consulte [Guardado de un formulario HTML5 como borrador](/help/forms/using/saving-html5-form-draft.md).
Para configurar el envío de formularios adaptables, consulte [Componente Borradores y envíos](/help/forms/using/draft-submission-component.md). (No válido para formularios sincronizados con el servidor JEE de AEM Forms).

Para crear un borrador, abra el formulario y toque **Guardar como borrador** ![guardar como borrador](assets/save-as-draft.png). Proporcione el nombre del borrador y toque **Guardar**. El borrador se guarda en la carpeta Borradores y se sincroniza con el servidor. Se guarda en la carpeta Bandeja de salida si la aplicación está sin conexión.

Si actualiza el formulario correspondiente posteriormente, los cambios se reflejan inmediatamente. Al sincronizar la aplicación de AEM Forms con el servidor de AEM Forms, el borrador se carga en el servidor de AEM Forms. Además, el borrador se mueve de la Bandeja de salida a la carpeta Tareas o Borradores. Aparece un icono de edición junto a él.

Mientras continúa trabajando en varias tareas y puntos de inicio y los guarda, los borradores se guardan. Cada vez que la aplicación se sincroniza con el servidor de AEM Forms, el borrador se guarda en el servidor. Garantiza que en cualquier momento pueda recuperar los borradores en función de la última fecha y hora guardadas. Por ejemplo, si vuelve a instalar la aplicación o cambia el dispositivo móvil, puede descargar el borrador del servidor.

## Eliminar un borrador {#delete-a-draft}

La carpeta Borradores lista todos los borradores. Puede utilizar la opción Eliminar borrador para eliminar permanentemente los borradores del dispositivo móvil y del servidor.

La opción para eliminar borradores creados a partir de una tarea no está disponible. Al eliminar un borrador creado a partir de una tarea, se abandona la tarea.

Puede descartar los borradores tanto en modo sin conexión como en modo en línea. Al descartar los borradores en modo sin conexión, los borradores se eliminan del servidor únicamente cuando se restaura la conexión con el servidor.

Siga los pasos siguientes para eliminar un borrador:

1. En la aplicación de AEM Forms, vaya a **Forms.**
1. Seleccione **Borradores** en la lista desplegable situada junto a Buscar.
1. Un formulario con el icono de edición ![edit-draft-app](assets/edit-draft-app.png) indica un borrador. Puntee en las elipsis horizontales junto al borrador.
1. En las opciones que aparecen al tocar los puntos suspensivos horizontales, toque **Eliminar borrador**.
