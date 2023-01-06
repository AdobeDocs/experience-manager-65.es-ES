---
title: Guardar una tarea o formulario como borrador
seo-title: Saving a task or form as a draft
description: Pasos para guardar una copia del borrador de una tarea o un formulario en la aplicación de AEM Forms
seo-description: Steps to save a draft copy of a task or a form in the AEM Forms app
uuid: 1192d2c2-05a4-4a96-9015-e56111aa2646
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 9950288c-b5a2-4945-afad-be9ce2abc8e9
exl-id: b4a23b2e-ab18-402c-8dfa-2533ee692912
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '492'
ht-degree: 100%

---

# Guardar una tarea o formulario como borrador {#saving-a-task-or-form-as-a-draft}

La opción Guardar como borrador guarda una instantánea de una tarea o formulario junto con los datos rellenados en el formulario asociado. También puede crear un borrador a partir de una plantilla. Los borradores se guardan en el dispositivo móvil y se sincronizan con el servidor de Adobe Experience Manager Forms para una recuperación posterior.

Puede [actualizar el formulario](/help/forms/using/working-with-form.md), [anotarlo](/help/forms/using/add-attachments.md) con fotografías y hacer garabatos. A medida que actualice un formulario, se recomienda guardarlo como borrador. En el caso de situaciones en las que decida enviar un formulario rellenado en un momento posterior, guardarlo como borrador resulta útil.

Para habilitar la función Guardar como borrador para formularios guardados en el portal de formularios, consulte [Guardar un formulario HTML5 como borrador](/help/forms/using/saving-html5-form-draft.md).
Para configurar el envío de formularios adaptables, consulte [Componente Borradores y envíos](/help/forms/using/draft-submission-component.md). (No válido para formularios sincronizados con el servidor JEE de AEM Forms).

Para crear un borrador, abra el formulario y pulse el botón **Guardar como borrador** ![save-as-draft](assets/save-as-draft.png). Proporcione el nombre del borrador y pulse **Guardar**. El borrador se guardará en la carpeta Borradores y se sincronizará con el servidor. Se guardará en la carpeta Bandeja de salida si la aplicación está sin conexión.

Si actualiza el formulario correspondiente posteriormente, los cambios se reflejarán inmediatamente. Al sincronizar la aplicación de AEM Forms con el servidor de AEM Forms, el borrador se cargará en el servidor de AEM Forms. Además, el borrador se moverá de la Bandeja de salida a la carpeta Tareas o Borradores. Aparece un icono de edición junto a él.

A medida que trabaje en varias tareas y puntos de inicio y los guarde, los borradores se guardarán. Cada vez que la aplicación se sincronice con el servidor de AEM Forms, el borrador se guardará en el servidor. Garantiza que en cualquier momento pueda recuperar los borradores en función de la última fecha y hora guardadas. Por ejemplo, si vuelve a instalar la aplicación o cambia el dispositivo móvil, puede descargar el borrador desde el servidor.

## Eliminar un borrador {#delete-a-draft}

La carpeta de borradores enumera todos los borradores. Puede utilizar la opción Eliminar borrador para eliminar de manera permanente los borradores del dispositivo móvil y del servidor.

La opción para eliminar borradores creados a partir de una tarea no está disponible. Al eliminar un borrador creado a partir de una tarea, la tarea se abandona.

Puede descartar los borradores tanto en modo sin conexión como en modo en línea. Al descartar los borradores en modo sin conexión, se eliminarán del servidor solo cuando se restaure la conexión con el servidor.

Realice los siguientes pasos para eliminar un borrador:

1. En la aplicación de AEM Forms, navegue hasta **Formularios.**
1. Seleccione **Borradores** de la lista desplegable situada junto a Buscar.
1. Un formulario con el icono de edición ![edit-draft-app](assets/edit-draft-app.png) denota un borrador. Pulse los puntos suspensivos horizontales junto al borrador.
1. En las opciones que aparecen al pulsar los puntos suspensivos horizontales, pulse **Eliminar borrador**.
