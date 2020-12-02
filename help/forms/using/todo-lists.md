---
title: Uso de listas pendientes
seo-title: Uso de listas pendientes
description: Cómo abrir, trabajar y completar las tareas según sea necesario, como aprobar o rechazar una solicitud o agregar más información.
seo-description: Cómo abrir, trabajar y completar las tareas según sea necesario, como aprobar o rechazar una solicitud o agregar más información.
uuid: f9cfad8e-5d0c-4a30-8153-2a03bf7dd986
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: d8546227-d78d-4fe2-a092-222482bb69c9
docset: aem65
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '4025'
ht-degree: 0%

---


# Uso de listas pendientes{#working-with-to-do-lists}

Cuando vista sus listas de tareas pendientes, es posible que vea tareas de un proceso empresarial que se le han asignado, o de cualquier grupo al que pertenezca o que sean tareas compartidas de otros usuarios. Puede abrir, trabajar y completar las tareas según sea necesario, como aprobar o rechazar una solicitud o agregar más información. Después de completar una tarea, se envía a la persona siguiente en el proceso comercial,

## Acerca de las listas pendientes {#about-todo-lists}

El espacio de trabajo de AEM Forms tiene los tres tipos siguientes de listas pendientes:

* Listas individuales, que contienen tareas que se le asignan directamente.
* Listas de grupo, que contienen tareas asignadas a un grupo. Cualquier miembro del grupo puede abrir y completar las tareas. Para abrir una tarea, un miembro de un grupo debe reclamar primero la tarea.
* Listas compartidas, que contienen tareas asignadas a un usuario que ha compartido su lista de tareas pendientes con usted y posiblemente con otros usuarios. Cualquiera de los usuarios que comparte una lista puede solicitar, abrir y completar tareas compartidas.

Puede realizar algunas acciones sin abrir la tarea haciendo clic en los iconos que aparecen cuando pasa el puntero sobre una tarea.

>[!NOTE]
>
>Un icono de exclamación indica que la tarea es de alta prioridad.

## Tareas típicas {#typical-tasks}

Al abrir y trabajar en una tarea, las herramientas disponibles dependen de la tarea. Diferentes tareas requieren que realice diferentes acciones y, por este motivo, es posible que algunas herramientas estén o no disponibles para usted. Las tareas típicas que puede recibir se describen a continuación.

**Proporcione información**: Recibirá una tarea que requiere que complete y envíe un formulario.

**Información** de revisión: Recibirá una tarea que requiere revisar la información y cerrar sesión en el contenido.

**Revisión** multiusuario: Recibirá una tarea al mismo tiempo que otros usuarios recibirán la tarea. Usted y los demás usuarios deben proporcionar información o revisar el contenido, o ambos. Con este tipo de tarea pueden estar disponibles las siguientes herramientas:

* Visualización de las instrucciones para la tarea
* Visualización del estado de finalización de todos los usuarios asignados a la tarea
* Visualización de los comentarios de todos los usuarios asignados a la tarea
* Añadiendo comentarios a la tarea usted mismo

Las herramientas adicionales que pueden estar disponibles con cualquiera de las tareas anteriores incluyen:

* Avanzar
* Compartir
* Consultar
* Devolver
* Notas
* Archivos adjuntos

## Abrir tareas {#opening-tasks}

Puede abrir y bloquear tareas desde la lista de tareas pendientes o reclamar y abrir tareas desde un grupo o una lista de tareas pendientes compartida. Al abrir una tarea, ésta se muestra en el panel principal. Las demás tareas se muestran en la lista de tarea junto a la lista Tareas pendientes.

Si existe una URL de resumen de Tarea, la vista de resumen de Tarea se abre de forma predeterminada, en lugar del formulario asociado a una tarea. Incluso cuando un usuario activa la opción &quot;Abrir el formulario en modo maximizado&quot; en Asignar Tarea, el formulario no se abre en modo maximizado.

>[!NOTE]
>
>Cuando se abre una tarea, según los valores predeterminados de tarea, el formulario asociado puede mostrarse en vista completa.

### Abra y bloquee una tarea de su lista {#open-and-lock-a-task-from-your-list}

Al abrir una tarea desde la lista Tareas pendientes, si se comparte la lista, puede bloquear la tarea para evitar que otro usuario que tenga acceso a la lista trabaje en la tarea.

1. En la página Tareas pendientes, en el panel izquierdo, seleccione la lista de tareas individuales. Todas las tareas se muestran en el panel central.

   >[!NOTE]
   >
   >Puede filtrar las tareas seleccionando el tipo de proceso en la lista Tareas pendientes. Puede seleccionar la lista Tareas pendientes para volver a realizar la vista de todas las tareas de la lista Tareas pendientes.

1. Si es necesario, bloquee su tarea. Para bloquear una tarea, haga clic en el icono Todas las opciones de la tarea y seleccione Bloquear. Pase el puntero sobre la tarea para que la opción esté disponible.

   >[!NOTE]
   >
   >También puede bloquear o desbloquear una tarea en cualquier ficha cuando la tarea esté abierta.

   ![lock_tarea](assets/lock_task.png)

   Menú Todas las opciones de una tarea

1. Haga clic en la tarea para abrirla.

### Abrir y reclamar una tarea de una lista compartida o de grupo {#open-and-claim-a-task-from-a-shared-or-group-list}

Al abrir y reclamar una tarea de un grupo o una lista compartida, la tarea se mueve del grupo o la lista compartida a la lista de tareas individuales. A otros usuarios con acceso a la lista se les impide trabajar en la tarea.

1. En la página Tareas pendientes, en el panel izquierdo, seleccione un grupo o una lista de tareas compartidas. Todas las tareas se muestran en el panel central.
1. Realice uno de estos pasos:

   * Para reclamar una tarea, sin abrirla, desde una lista de trabajo de grupo o compartida, haga clic en **Reclamar** pasando el puntero sobre la tarea. Como alternativa, cuando la tarea está abierta, el botón Reclamar está disponible en la barra de acciones debajo del panel tarea. Al reclamar, una tarea pasa del grupo o de la lista de tareas pendientes compartida a la lista.
   * Para reclamar y abrir una tarea de un grupo o de una lista de tareas pendientes compartida, haga clic en **Reclamar y abra**.

## Uso de tareas {#working-with-tasks}

Después de abrir una tarea, las fichas que se muestran en el panel principal y las herramientas disponibles dependen de la tarea. Las fichas que puede ver se describen a continuación:

**Resumen** de tarea: Cuando se abre una tarea, el panel Resumen de Tarea permite mostrar información sobre la tarea, si existe, mediante una URL especificada en el proceso en el paso Asignar Tarea. Al utilizar el panel Resumen de Tareas, se puede mostrar información adicional y relevante para una tarea a fin de agregar más valor para el usuario final del espacio de trabajo de AEM Forms. Esta ficha no está disponible si la URL de resumen de Tarea no existe.

**Detalles**: Proporciona información sobre la tarea actual y el proceso al que pertenece.

**Formulario**: Muestra el formulario asociado a la tarea. El formulario puede ser de varios tipos de archivo, incluidos archivos PDF, HTML, Guide y SWF. El formulario puede tener el aspecto de un formulario normal imprimible o basado en Web o guiarlo por una serie de paneles de estilo asistente para recopilar información.

**Historial**: Lista las tareas que forman parte de la instancia de proceso y el formulario asociado, las asignaciones de tarea y los archivos adjuntos para cada tarea.

**Datos adjuntos**: Muestra los datos adjuntos existentes asociados a la tarea y los datos adjuntos, si es necesario.

**Notas**: Muestra las notas existentes asociadas con la tarea y agrega notas, si es necesario.

Al trabajar en una tarea, las herramientas que puede ver y las acciones que puede realizar se describen a continuación.

### Reenviar, compartir o consultar una tarea {#forward-share-or-consult-on-a-task}

Puede reenviar una tarea junto con cualquier nota o archivo adjunto a otro usuario, compartir la tarea o consultar la tarea con otro usuario. Si cambia los datos de formulario asociados a una tarea, guarde el formulario como borrador antes de reenviar, compartir o consultar la tarea. De lo contrario, la tarea se envía sin el formulario actualizado. Después de reenviar y compartir una tarea, el usuario que recibe la tarea puede reclamarla y completarla o devolverla. Si consulta una tarea, el usuario solo puede devolverle la tarea.

1. Si cambia un formulario asociado a una tarea que desea conservar, haga clic en **Guardar**. La opción Guardar está disponible en la barra de acciones de la parte inferior de cada ficha. De lo contrario, la tarea se envía sin el formulario actualizado.

   >[!NOTE]
   >
   >El botón Guardar no está disponible para algunos formularios, según la tarea en la que esté trabajando.

1. En cualquier ficha, haga clic en uno de estos botones:

   * **Avanzar**
   * **Compartir**
   * **Consultar**

   >[!NOTE]
   >
   >Según la tarea, también puede realizar estas acciones desde la lista Tareas pendientes sin abrir la tarea.

1. En la ventana del cuadro de diálogo emergente, busque y seleccione el nombre del usuario con el que desea reenviar, compartir o consultar la tarea.

### Devolver una tarea {#return-a-task}

1. En cualquier ficha, haga clic en **Retorno**. La tarea se devuelve a la lista de tareas pendientes del usuario que le ha enviado previamente la tarea o que ha compartido o consultado la tarea con usted.

### Desconectar una tarea {#take-a-task-offline}

Es posible que pueda trabajar en una tarea sin conexión y enviar su formulario desde Adobe® Reader® o Adobe® Acrobat® Professional o Adobe® Acrobat® Standard. Cuando se envía el formulario, el cliente de correo electrónico se inicia con la dirección de correo electrónico del servidor correspondiente. A continuación, puede enviar el formulario completado al servidor por correo electrónico.

1. En cualquier ficha, haga clic en **Sin conexión**.
1. Especifique un nombre de archivo para guardar el formulario y haga clic en **Guardar**. El formulario asociado a la tarea se guarda localmente y la tarea permanece en la lista Tareas pendientes hasta que se envía el formulario.

### Trabajar con archivos adjuntos {#work-with-attachments}

Es posible que pueda agregar, actualizar, eliminar o guardar archivos adjuntos localmente.

**Añadir un archivo adjunto**

1. En la ficha **Archivos adjuntos**, haga clic en **Examinar** para seleccionar el archivo que desea adjuntar.
1. Seleccione el nivel **Permisos** para los datos adjuntos de otros usuarios que participen en el proceso. Si selecciona **Leer**, otros usuarios pueden guardar el archivo localmente. Si selecciona uno de los permisos de edición, otros usuarios también pueden cargar un nuevo archivo para reemplazar los datos adjuntos.

   >[!NOTE]
   >
   >También puede agregar comentarios junto con los datos adjuntos.

1. Haga clic en **Cargar**. El archivo se adjunta al formulario.

**Vista de datos adjuntos**

1. En la ficha **Archivos adjuntos**, haga clic en el nombre del archivo adjunto de la vista.

**Guardar un archivo adjunto localmente**

1. Haga clic en un archivo adjunto para abrirlo. Guarde el archivo adjunto abierto localmente.

**Actualizar un archivo adjunto**

1. Haga clic en **Editar** para el archivo adjunto. Seleccione el archivo con el que desea reemplazar el archivo adjunto existente haciendo clic en **Examinar**.

**Eliminar un archivo adjunto**

1. Haga clic en **Eliminar** para un archivo adjunto.

### Guarde su trabajo sin completar la tarea {#save-your-work-without-completing-the-task}

1. En cualquier ficha, toque **Guardar**.

   Aparecerá el cuadro de diálogo Guardar como borrador. El nombre predeterminado del borrador es el nombre de la tarea de la plantilla de tarea.

   ![saveasreclutdialog](assets/saveasdraftdialog.png)

   >[!NOTE]
   >
   >Puede configurar el espacio de trabajo para que automáticamente guarde la información introducida por un usuario como borrador. Si el guardado automático está activado y un usuario está trabajando en un borrador, el borrador se guarda periódicamente. En caso de guardar automáticamente, se toma automáticamente el nombre predeterminado de la tarea.
   >
   >
   >Para obtener más información, consulte Guardar borrador periódicamente en [Administración de preferencias](/help/forms/using/getting-started-livecycle-html-workspace.md).

1. En el cuadro de diálogo Guardar como borrador, especifique un nombre único para la tarea y toque **Aceptar**.

   ![saveasreclutdialog_name](assets/saveasdraftdialog_name.png)

   El borrador se guarda con el nombre especificado. La tarea permanece en la lista Tareas pendientes y los cambios realizados en el formulario se guardan en la carpeta Borradores. Además, en la lista Tareas pendientes, puede buscar el borrador con el nombre del borrador para reanudar el trabajo en él.

   ![searchfortarea](assets/searchfortask.png)

## Finalización de tareas {#completing-tasks}

El modo de completar una tarea depende de la propia tarea y de su papel en el proceso. Se le puede pedir que apruebe o rechace una solicitud, proporcione contenido, revise y verifique la información o indique que ha actuado.

Puede completar una tarea de varias formas:

* Uso de las acciones disponibles en cualquiera de las fichas
* Uso de las acciones generadas en el propio formulario
* Desde la lista de tareas pendientes, sin abrir la tarea

>[!NOTE]
>
>Esta opción está disponible si el campo `isMustOpenToComplete` no está seleccionado en el paso `Assign Task` de Workbench mientras se diseña un proceso.

* Por correo electrónico, si recibe notificaciones por correo electrónico

Al completar una tarea, según la tarea, puede aparecer un cuadro de diálogo de confirmación que reafirme la acción. Por ejemplo, puede ver un cuadro de diálogo que le solicita que confirme la validez de la información proporcionada.

>[!NOTE]
>
>Si ha cambiado una tarea pero no está listo para finalizarla, puede guardar el trabajo como borrador haciendo clic en Guardar y volver a ella más tarde.

### Completar una tarea {#complete-a-task}

1. Realice uno de los siguientes pasos:

   * Seleccione la tarea y haga clic en el botón correspondiente para el siguiente paso requerido en el proceso en la parte inferior de la lista.
   * Si el formulario no tiene botones y el botón de completado del espacio de trabajo de AEM Forms está disponible, haga clic en **Completar**.
   * Si el formulario tiene botones y el botón de completado del espacio de trabajo de AEM Forms no está disponible, haga clic en el botón correspondiente del formulario para el siguiente paso requerido en el proceso.

   Si el formulario no tiene botones y el botón de completado del espacio de trabajo de AEM Forms no está disponible, aparece un mensaje que indica que no se puede enviar el formulario.

1. Si aparece un cuadro de diálogo de confirmación, realice una de estas acciones:

   * Haga clic en **Aceptar** si ha completado la tarea y está listo para cerrar sesión en ella.
   * Haga clic en **Cancelar** si desea volver a la tarea y no está listo para cerrar sesión en ella.

>[!NOTE]
>
>Puede ver un botón Enviar dentro de los formularios HTML cuando se utilizan propiedades de proceso en un formulario. Este botón no está visible cuando el mismo formulario se procesa como PDF. Para completar una tarea, haga clic en el botón Enviar disponible en la parte inferior del espacio de trabajo de AEM Forms, fuera del formulario y no en el botón Enviar dentro del formulario.

### Tareas de aprobación masiva {#bulk-approve-tasks}

Puede enviar varias tareas desde la lista Tareas pendientes. Sólo se pueden enviar juntos tareas del mismo proceso, con los mismos nombres de tarea, y las mismas opciones de ruta.

>[!NOTE]
>
>Esta opción está disponible si el campo isMustOpenToComplete no está seleccionado en el paso Asignar Tarea en Workbench mientras se diseña un proceso.

1. En la página Tareas pendientes, en el panel izquierdo, seleccione la lista de tareas individuales. Todas las tareas se muestran en el panel central.
1. Seleccione **Activar modo masivo**. Las casillas de verificación aparecen delante de las tareas de la lista.

   >[!NOTE]
   >
   >Esta opción no está disponible para tareas para las que el campo isMustOpenToComplete está seleccionado en el paso Asignar Tarea en Workbench, mientras se diseña un proceso. Las casillas de verificación de dichas tareas en la lista TO-DO permanecen siempre desactivadas.

1. Seleccione tareas para la aprobación masiva. Se pueden seleccionar varias tareas del mismo proceso, con los mismos nombres de tarea, y las mismas opciones de ruta. Una vez seleccionada una tarea para aprobación, solo permanecerán habilitadas las tareas con el mismo proceso, con los mismos nombres de tarea y las mismas opciones de ruta. El resto están desactivados.

   ![1_bulkapproved](assets/1_bulkapproval.png)

1. Haga clic en la opción Enviar disponible. Se envían las tareas seleccionadas.

   ![aprobación masiva](assets/bulkapproval.png)

## Participación en tareas a través del correo electrónico {#participating-in-tasks-through-email}

Puede recibir y completar tareas por correo electrónico. La participación en tareas mediante correos electrónicos elimina la necesidad de comprobar rutinariamente la lista de tareas pendientes en busca de nuevas tareas o comprobar el estado de una tarea en la página de seguimiento.

En primer lugar, defina las preferencias del espacio de trabajo de AEM Forms para recibir notificaciones por correo electrónico. El espacio de trabajo de AEM Forms puede enviar notificaciones por correo electrónico para tareas en la lista de tareas pendientes o en cualquier lista de trabajo de grupo a la que pertenezca. El administrador determina cuándo se envían los mensajes de notificación por correo electrónico y quién los recibe.

Los mensajes de correo electrónico pueden contener un vínculo que abre la tarea en el espacio de trabajo de AEM Forms, un archivo adjunto del formulario que se utiliza para la tarea o acciones para completar la tarea por correo electrónico. Si se incluye un formulario en el mensaje de correo electrónico, puede abrirlo y completar la tarea si los botones para completar la tarea están creados en el formulario. Si las acciones para completar la tarea se incluyen en el mensaje de correo electrónico, puede completar la tarea haciendo clic en las acciones del correo electrónico o respondiendo al correo electrónico con la acción escrita como primera línea en el cuerpo del correo electrónico.

>[!NOTE]
>
>Para configurar el espacio de trabajo para que utilice las plantillas de correo electrónico adecuadas, consulte la [Guía del administrador de AEM Forms JEE](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/).

Cuando completa una tarea por correo electrónico, la tarea se elimina de la lista de tareas pendientes en el espacio de trabajo de AEM Forms.

>[!NOTE]
>
>Si el usuario no ha iniciado sesión en el espacio de trabajo de AEM Forms en el navegador y abre un vínculo a una tarea de tareas pendientes, el vínculo de tareas pendientes directo no se abre y muestra una excepción. Inicie sesión en el espacio de trabajo de AEM Forms antes de hacer clic en los vínculos de los correos electrónicos.

>[!NOTE]
>
>No puede reenviar una notificación por correo electrónico para asignar una tarea a otra persona. Solo puede reenviar tareas a otros usuarios desde el espacio de trabajo de AEM Forms.

### Recibir mensajes de notificación por correo electrónico {#receive-email-notification-messages}

1. Haga clic en **Preferencias**.
1. En la lista **Notificar Eventos de Tarea por correo electrónico**, seleccione **Sí**.
1. Para incluir el formulario y los datos con el mensaje de correo electrónico, en la lista **Adjuntar Forms en correo electrónico**, seleccione **Sí**.

## Participación en tareas a través de dispositivos móviles {#participating-in-tasks-through-mobile-devices}

Puede utilizar la aplicación de espacio de trabajo de AEM Forms para participar en tareas desde su dispositivo móvil. Antes de instalar la aplicación, póngase en contacto con el administrador del sistema para asegurarse de que su organización admite el uso de la aplicación de espacio de trabajo de AEM Forms.

## Acerca de los plazos y los recordatorios {#about-deadlines-and-reminders}

Una *fecha límite* determina la fecha y la hora en que debe completar una tarea. Cuando se supera una fecha límite, el servidor enruta la tarea al siguiente paso del proceso (que puede ser la lista de otro usuario) y, a continuación, aparece el icono de fecha límite en la tarea. El icono de fecha límite aparece independientemente de las reglas asociadas al proceso.

Un *recordatorio* le notifica de una tarea que requiere su atención. Los recordatorios se producen en un momento predeterminado y, a continuación, a intervalos regulares hasta que se completa la tarea asociada. Cuando recibe un recordatorio, aparece el icono de recordatorio en la tarea.

El proceso comercial determina el comportamiento y el momento de los plazos y los recordatorios. No todos los procesos tienen plazos y recordatorios. El administrador especifica si se envían notificaciones por correo electrónico para los plazos y recordatorios. Puede establecer sus preferencias para recibir notificaciones por correo electrónico.

## Trabajar con tareas de colas compartidas y de grupo {#working-with-tasks-from-group-and-shared-queues}

Todas las tareas asignadas aparecerán en la lista Tareas pendientes (cola).

Cualquier grupo y listas de tareas pendientes compartidas a las que tenga acceso también aparecerán en el panel izquierdo de la página Tareas pendientes. Puede completar tareas desde cualquier lista de tareas pendientes a la que tenga acceso.

Una lista de grupo de tareas pendientes puede tener más de un miembro. Un administrador configura listas de tareas pendientes de grupo en función de los requisitos específicos de su organización. Las listas de trabajo grupal proporcionan una manera de distribuir el trabajo entre varias personas que comparten responsabilidades similares.

Por ejemplo, cada miembro del equipo procesa los formularios de solicitud de préstamo. Todas estas tareas se envían a una lista de grupo de tareas a las que todos los miembros del grupo tienen acceso. Cada miembro del grupo puede acceder a las tareas desde esa lista de tareas pendientes.

Aparece una lista de tareas pendientes compartida cuando otro usuario comparte su lista de tareas pendientes con usted o comparte explícitamente una tarea con usted. A continuación, puede realizar la vista de las tareas en la lista de tareas de ese usuario y completarlas en su nombre. Por ejemplo: si está tomando unas vacaciones, puede elegir compartir su lista de tareas pendientes con un colega que complete sus tareas mientras está fuera.

>[!NOTE]
>
>También puede especificar opciones de configuración fuera de la oficina para reenviar tareas a otros usuarios mientras no esté en la oficina.

Para trabajar en una tarea de un grupo o en una lista de tareas pendientes compartida, primero debe reclamar la tarea. A continuación, se convertirá en el propietario de la tarea hasta que la complete o la envíe a otro usuario.

### Colocación de colas {#sharing-queues}

Puede compartir su lista de tareas pendientes con otro usuario, que podrá realizar la vista de las nuevas tareas en su lista de tareas pendientes y actuar en consecuencia por usted. Si existe alguna tarea en la lista de tareas pendientes antes de compartir la lista de tareas pendientes, el otro usuario no puede realizar la vista. El usuario puede vista y reclamar únicamente las tareas que llegan a su lista de tareas pendientes después de conceder acceso a su lista de tareas pendientes.

Tenga en cuenta que para que un usuario pueda ver una tarea en una cola compartida, el diseñador del proceso debe habilitar la opción Añadir ACL para cola compartida en la ficha Lista de Control de acceso de Tarea (ACL) del Servicio de usuario.

>[!NOTE]
>
>Si planea estar fuera de la oficina, también puede especificar la configuración externa para reenviar tareas a otros usuarios mientras se encuentra fuera en lugar de compartir toda la lista de tareas pendientes.

**Compartir la cola**

1. En la ficha **Colas** de la ficha **Preferencias**, haga clic en el icono &#39;+&#39; para &#39;Usuarios que comparten mi cola actualmente&#39;.
1. Busque y seleccione el nombre del usuario.
1. Haga clic en el botón **Compartir** para compartir la cola con el usuario seleccionado.
1. Seleccione el nombre del usuario y haga clic en **Compartir**.

   >[!NOTE]
   >
   >Puede eliminar un usuario para que no comparta su lista de tareas pendientes haciendo clic en el icono **X** al final de la fila en la que aparece el usuario.

### Acceso a otras colas {#accessing-other-queues}

Puede solicitar acceso a la lista de tareas pendientes de otro usuario para la vista y solicitar cualquier tarea nueva en la lista de tareas pendientes del usuario.

Cuando se solicita el acceso a la lista de tareas pendientes de otro usuario, el usuario recibe una tarea en su lista de tareas pendientes para aprobar o rechazar la solicitud. Una vez que el usuario complete la tarea, recibirá una notificación en la lista de tareas pendientes.

Si se le concede acceso a la lista de tareas pendientes de otro usuario, no podrá realizar vistas de ninguna tarea que existiera en la lista de tareas pendientes del usuario antes de que se le concediera acceso. Solo puede realizar la vista de las tareas que llegan a la lista de tareas pendientes del usuario después de que se le haya concedido acceso a la lista de tareas pendientes.

**Acceso a otra cola**

1. En la ficha **Preferencias**, abra la ficha **Colas**.
1. Haga clic en &#39;+&#39; para las &#39;colas de usuario a las que tengo acceso&#39;. Busque el nombre del usuario en el cuadro de diálogo emergente.
1. Seleccione el nombre del usuario y haga clic en **Solicitud**.

   >[!NOTE]
   >
   >Puede eliminar el acceso a otra lista de tareas pendientes seleccionando el nombre de usuario en las colas de usuarios a las que tengo acceso a la lista y haciendo clic en **X** al final de la fila que menciona el nombre del usuario. No puede quitar el acceso a otra lista de tareas pendientes cuando la solicitud de acceso a la lista de tareas pendientes sigue pendiente.

## Configuración de preferencias fuera de la oficina {#setting-out-of-office-preferences}

Si planea estar fuera de la oficina, puede especificar lo que sucede con las tareas que se le han asignado para ese período.

Tiene la opción de especificar una fecha y hora de inicio y una fecha y hora de finalización para que la configuración fuera de la oficina esté en vigor. Si se encuentra en un huso horario distinto del servidor, el huso horario utilizado es el del servidor.

Puede establecer una persona predeterminada a la que se envíen todas sus tareas. También puede especificar excepciones para tareas de procesos específicos que se enviarán a un usuario diferente o para permanecer en la lista de tareas pendientes hasta que vuelva. Si la persona designada también está fuera de la oficina, la tarea se dirige al usuario que designaron. Si la tarea no se puede asignar a un usuario que no está fuera de la oficina, la tarea permanece en la lista de tareas pendientes.

>[!NOTE]
>
>Cuando se encuentra fuera de la oficina, las tareas que anteriormente estaban en la lista de tareas pendientes permanecen allí y no se reenvían a otros usuarios.

### Configurar las preferencias fuera de la oficina {#set-out-of-office-preferences}

1. Haga clic en **Preferencias** y haga clic en **Fuera de Office**.
1. Para especificar cuándo está fuera de la oficina, realice uno de estos pasos:

   * Para especificar que está fuera de la oficina ahora por un período de tiempo indefinido, en la lista **Actualmente estoy**, seleccione **Fuera de la oficina** pero no agregue un intervalo de fechas.
   * Para especificar una fecha y hora de inicio que está fuera de la oficina y hacer clic en &#39;+&#39; para **Programación fuera de la oficina**. Utilice la lista de calendario y hora para especificar la fecha y hora del inicio. Si no especifica una fecha y hora de finalización, se le considerará fuera de la oficina indefinidamente desde la fecha y hora de inicio hasta que cambie sus preferencias.

1. Para especificar cómo se deben gestionar sus tareas de forma predeterminada, seleccione una de estas opciones en el cuadro de diálogo **Al salir de Office: Lista predeterminada Usuario para tareas fuera de la oficina**:

   * Seleccione **No asignar** para mantener tareas en la lista de tareas pendientes hasta que vuelva.
   * Seleccione **Buscar usuario** para buscar un usuario al que asignar sus tareas. Al seleccionar un usuario, también puede realizar la vista de su programación fuera de la oficina.

1. Para establecer excepciones al valor predeterminado, haga clic en + para **Excepciones de proceso**, seleccione el proceso para el que desea crear una excepción y, a continuación, seleccione otro usuario o seleccione **No asignar** de la lista **asignada a**.

   >[!NOTE]
   >
   >El diseñador de procesos puede especificar que las tareas de algunos procesos siempre se mantengan privadas y no se reenvíen a otros usuarios. Esta configuración anula cualquier configuración que realice.

1. Cuando termine de establecer las preferencias, haga clic en **Guardar**. Si la configuración indica que se encuentra fuera de la oficina, los cambios surtirán efecto inmediatamente. De lo contrario, surtirán efecto en la fecha y hora de inicio especificadas. Si inicia sesión mientras está fuera de la oficina, no se le considerará en la oficina hasta que cambie la configuración.
