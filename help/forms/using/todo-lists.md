---
title: Uso de listas de tareas pendientes
seo-title: Working with To-do lists
description: Cómo abrir, trabajar y completar las tareas según sea necesario, como aprobar o rechazar una solicitud o agregar más información.
seo-description: How to open, work on, and complete the tasks as required, such as approving or rejecting a request or adding more information.
uuid: f9cfad8e-5d0c-4a30-8153-2a03bf7dd986
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: d8546227-d78d-4fe2-a092-222482bb69c9
docset: aem65
exl-id: c80bf347-d1ed-488f-a41a-ceb05a6df9e4
source-git-commit: e961ce67e5b1a71e3af6dded304d99cd9e6896bc
workflow-type: tm+mt
source-wordcount: '4033'
ht-degree: 1%

---

# Uso de listas de tareas pendientes{#working-with-to-do-lists}

Al ver las listas de tareas pendientes, puede ver las tareas de un proceso empresarial que esté asignado a usted, a cualquier grupo al que pertenezca o que sean las tareas compartidas de otros usuarios. Puede abrir, trabajar y completar las tareas según sea necesario, como aprobar o rechazar una solicitud o agregar más información. Una vez finalizada una tarea, se envía a la persona siguiente en el proceso empresarial,

## Acerca de las listas de tareas pendientes {#about-todo-lists}

El espacio de trabajo de AEM Forms tiene los tres tipos siguientes de listas de tareas pendientes:

* Listas individuales, que contienen tareas que se le asignan directamente.
* Listas de grupos, que contienen tareas asignadas a un grupo. Cualquier miembro del grupo puede abrir y completar las tareas. Para abrir una tarea, un miembro de un grupo debe reclamar primero la tarea.
* Listas compartidas, que contienen tareas asignadas a un usuario que ha compartido su lista de tareas pendientes con usted y posiblemente con otros usuarios. Cualquiera de los usuarios que comparten una lista puede reclamar, abrir y completar tareas compartidas.

Puede realizar algunas acciones sin abrir la tarea haciendo clic en los iconos que aparecen cuando pasa el puntero sobre una tarea.

>[!NOTE]
>
>Un icono de exclamación indica que la tarea tiene una prioridad alta.

## Tareas habituales {#typical-tasks}

Al abrir y trabajar en una tarea, las herramientas disponibles dependen de la tarea. Las diferentes tareas requieren que realice diferentes acciones y, por este motivo, algunas herramientas pueden estar o no disponibles para usted. A continuación se describen las tareas típicas que puede recibir.

* **Proporcionar información**: Recibe una tarea que requiere que complete y envíe un formulario.

* **Información de revisión**: Recibe una tarea que requiere que revise la información y que firme el contenido.

* **Revisión multiusuario**: Recibe una tarea al mismo tiempo que otros usuarios reciben la tarea. Usted y los demás usuarios deben proporcionar información o revisar el contenido, o ambos. Con este tipo de tarea pueden estar disponibles las siguientes herramientas:

   * Visualización de las instrucciones de la tarea
   * Visualización del estado de finalización de todos los usuarios asignados a la tarea
   * Visualización de los comentarios de todos los usuarios asignados a la tarea
   * Añadir comentarios a la tarea

Las herramientas adicionales que pueden estar disponibles con cualquiera de las tareas anteriores incluyen las siguientes:

* Avanzar
* Compartir
* Consultar
* Devuelve
* Notas
* Archivos adjuntos

## Apertura de tareas {#opening-tasks}

Puede abrir y bloquear tareas de la lista de tareas pendientes o reclamar y abrir tareas de un grupo o de una lista de tareas pendientes compartida. Cuando se abre una tarea, esta se muestra en el panel principal. Las demás tareas se muestran en la lista de tareas junto a la lista Tareas pendientes.

Si existe una URL de resumen de tareas, la vista Resumen de tareas se abre de forma predeterminada, en lugar del formulario asociado a una tarea. Incluso cuando un usuario habilita la opción &quot;Abrir el formulario en modo maximizado&quot; en Asignar tarea, el formulario no se abre en modo maximizado.

>[!NOTE]
>
>Al abrir una tarea, según los valores predeterminados de la tarea, el formulario asociado puede mostrarse en la vista completa.

### Abra y bloquee una tarea de la lista {#open-and-lock-a-task-from-your-list}

Cuando abra una tarea desde la lista de tareas pendientes, si la lista está compartida, puede bloquear la tarea para evitar que otro usuario que tenga acceso a la lista trabaje en la tarea.

1. En la página Tareas pendientes, en el panel izquierdo, seleccione la lista Tareas pendientes individual. Todas las tareas se muestran en el panel central.

   >[!NOTE]
   >
   >Puede filtrar las tareas seleccionando el tipo de proceso en la lista Tareas pendientes. Puede seleccionar la lista de tareas pendientes para volver a ver todas las tareas de la lista de tareas pendientes.

1. Si es necesario, bloquee la tarea. Para bloquear una tarea, haga clic en el icono All Options de la tarea y seleccione Lock. Pase el puntero sobre la tarea para que la opción esté disponible.

   >[!NOTE]
   >
   >También puede bloquear o desbloquear una tarea en cualquier pestaña cuando la tarea esté abierta.

   ![lock_task](assets/lock_task.png)

   Todas las opciones del menú de una tarea

1. Abra la tarea haciendo clic en ella.

### Abrir y reclamar una tarea de una lista de grupos o compartidos {#open-and-claim-a-task-from-a-shared-or-group-list}

Cuando abre y reclama una tarea de un grupo o lista compartida, la tarea se mueve del grupo o lista compartida a su lista de tareas individuales. A otros usuarios con acceso a la lista se les impide trabajar en la tarea.

1. En la página Tareas pendientes, en el panel izquierdo, seleccione un grupo o una lista de tareas pendientes compartidas. Todas las tareas se muestran en el panel central.
1. Realice uno de estos pasos:

   * Para reclamar una tarea, sin abrirla, desde un grupo o una lista de tareas pendientes compartida, haga clic en  **Reclamación** pasando el puntero sobre la tarea. Alternativamente, cuando la tarea está abierta, el botón Reclamar está disponible en la barra de acciones debajo del panel de tareas. Al solicitar, una tarea pasa del grupo o de la lista de tareas pendientes compartidas a la lista.
   * Para reclamar y abrir una tarea desde un grupo o una lista de tareas pendientes compartida, haga clic en **Reclamar y abrir**.

## Trabajo con tareas {#working-with-tasks}

Después de abrir una tarea, las pestañas que se muestran en el panel principal y las herramientas disponibles dependen de la tarea. Las pestañas que puede ver se describen a continuación:

* **Resumen de tareas**: Cuando se abre una tarea, el panel Resumen de tareas le permite mostrar información sobre la tarea, si existe, utilizando una URL especificada en el proceso del paso Asignar tarea. Si utiliza el Panel de resumen de tareas, se puede mostrar información adicional y relevante para una tarea a fin de agregar más valor para el usuario final del espacio de trabajo de AEM Forms. Esta pestaña no está disponible si la dirección URL del resumen de tareas no existe.

* **Detalles**: Proporciona información sobre la tarea y el proceso actuales a los que pertenece.

* **Formulario**: Muestra el formulario asociado a la tarea. El formulario puede ser de varios tipos de archivo, como PDF, HTML, Guía y archivo SWF. El formulario puede parecer un formulario normal, imprimible o basado en la Web, o puede guiarlo a través de una serie de paneles de estilo asistente para recopilar información.

* **Historial**: Muestra las tareas que forman parte de la instancia de proceso y el formulario asociado, las asignaciones de tareas y los archivos adjuntos de cada tarea.

* **Archivos adjuntos**: Muestra los archivos adjuntos existentes asociados a la tarea y los archivos adjuntos, si es necesario.

* **Notas**: Muestra las notas existentes asociadas con la tarea y agrega notas, si es necesario.

Al trabajar en una tarea, a continuación se describen las herramientas que puede ver y las acciones que puede realizar.

### Reenviar, compartir o consultar una tarea {#forward-share-or-consult-on-a-task}

Puede reenviar una tarea junto con las notas o archivos adjuntos a otro usuario, compartir la tarea o consultar la tarea con otro usuario. Si cambia los datos del formulario asociados a una tarea, guarde el formulario como borrador antes de reenviar, compartir o consultar la tarea. De lo contrario, la tarea se envía sin el formulario actualizado. Después de reenviar y compartir una tarea, el usuario que la recibe puede reclamarla y completarla o devolverla a usted. Si consulta una tarea, el usuario solo puede devolverle la tarea.

1. Si cambia un formulario asociado a una tarea que desea conservar, haga clic en **Guardar**. La opción Guardar está disponible en la barra de acciones de la parte inferior de cada pestaña. De lo contrario, la tarea se envía sin el formulario actualizado.

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

1. En la ventana del cuadro de diálogo emergente, busque y seleccione el nombre del usuario con el que reenviar, compartir o consultar la tarea.

### Devolver una tarea {#return-a-task}

1. En cualquier pestaña, haga clic en **Devuelve**. La tarea se devuelve a la lista de tareas pendientes del usuario que anteriormente le había reenviado la tarea, o ha compartido o consultado la tarea con usted.

### Desconectar una tarea {#take-a-task-offline}

Es posible que se le permita trabajar en una tarea sin conexión y enviar posteriormente su formulario desde Adobe® Reader® o Adobe® Acrobat® Professional o Adobe® Acrobat® Standard. Cuando se envía el formulario, el cliente de correo electrónico se inicia con la dirección de correo electrónico del servidor correspondiente. A continuación, puede enviar por correo electrónico el formulario completado al servidor.

1. En cualquier pestaña, haga clic en **Sin conexión**.
1. Especifique un nombre de archivo en el que guardar el formulario y haga clic en **Guardar**. El formulario asociado a la tarea se guarda localmente y la tarea permanece en la lista de tareas pendientes hasta que se envíe el formulario.

### Trabajo con archivos adjuntos {#work-with-attachments}

Se le puede permitir añadir, actualizar, eliminar o guardar archivos adjuntos localmente.

**Añadir un archivo adjunto**

1. En el **Archivos adjuntos** , haga clic en **Examinar** para seleccionar el archivo que desea adjuntar.
1. Seleccione el **Permisos** para el archivo adjunto para otros usuarios que participan en el proceso. Si selecciona **Lectura**, otros usuarios pueden guardar el archivo localmente. Si selecciona uno de los permisos de edición, otros usuarios también pueden cargar un nuevo archivo para reemplazar el archivo adjunto.

   >[!NOTE]
   >
   >También puede agregar comentarios junto con los archivos adjuntos.

1. Haga clic en **Cargar**. El archivo se adjunta al formulario.

**Ver un archivo adjunto**

1. En el **Archivos adjuntos** , haga clic en el nombre del archivo adjunto que desea ver.

**Guardar un archivo adjunto localmente**

1. Haga clic en un archivo adjunto para abrirlo. Guarde el archivo adjunto abierto localmente.

**Actualizar un archivo adjunto**

1. Haga clic en **Editar** para el archivo adjunto. Seleccione el archivo con el que desea reemplazar el archivo adjunto existente haciendo clic en **Examinar**.

**Eliminar un archivo adjunto**

1. Haga clic en **Eliminar** para un archivo adjunto.

### Guarde el trabajo sin completar la tarea {#save-your-work-without-completing-the-task}

1. En cualquier pestaña, pulse **Guardar**.

   Aparecerá el cuadro de diálogo Guardar como borrador. El nombre predeterminado del borrador es el nombre de la tarea de la plantilla de tarea.

   ![saveasreclutdialog](assets/saveasdraftdialog.png)

   >[!NOTE]
   >
   >Puede configurar Workspace para que, periódicamente, guarde automáticamente la información introducida por un usuario como borrador. Si el guardado automático está habilitado y un usuario está trabajando en un borrador, el borrador se guarda periódicamente. En caso de guardado automático, se toma automáticamente el nombre predeterminado de la tarea.
   >
   >
   >Para obtener más información, consulte Guardar borrador periódicamente en [Preferencias de administración](/help/forms/using/getting-started-livecycle-html-workspace.md).

1. En el cuadro de diálogo Guardar como borrador , especifique un nombre único para la tarea y pulse **OK**.

   ![saveasreclutdialog_name](assets/saveasdraftdialog_name.png)

   El borrador se guarda con el nombre especificado. La tarea permanece en la lista de tareas pendientes y los cambios realizados en el formulario se guardan en la carpeta Borradores . Además, en la lista de tareas pendientes, puede buscar el borrador con el nombre del borrador para reanudar el trabajo en él.

   ![searchfortask](assets/searchfortask.png)

## Finalización de tareas {#completing-tasks}

La forma de completar una tarea depende de la propia tarea y de su función en el proceso. Se le puede pedir que apruebe o rechace una solicitud, proporcione contenido, revise y verifique la información, o que indique que ha actuado.

Puede completar una tarea de varias maneras:

* Uso de las acciones disponibles en cualquiera de las pestañas
* Uso de las acciones creadas en el propio formulario
* Desde la lista de tareas pendientes, sin abrir la tarea

>[!NOTE]
>
>Esta opción está disponible si `isMustOpenToComplete` no está seleccionado en la variable `Assign Task` en Workbench, mientras diseña un proceso.

* Por correo electrónico, si recibe notificaciones por correo electrónico

Cuando complete una tarea, según la tarea, puede aparecer un cuadro de diálogo de confirmación que reafirme la acción. Por ejemplo, puede que aparezca un cuadro de diálogo que le pedirá que confirme la validez de la información proporcionada.

>[!NOTE]
>
>Si ha cambiado una tarea pero no está lista para completarla, puede guardar el trabajo como borrador haciendo clic en Guardar y volver a ella más tarde.

### Completar una tarea {#complete-a-task}

1. Realice uno de los siguientes pasos:

   * Seleccione la tarea y haga clic en el botón correspondiente para el paso siguiente requerido en el proceso en la parte inferior de la lista.
   * Si el formulario no tiene botones y el botón Completar del espacio de trabajo de AEM Forms está disponible, haga clic en **Completar**.
   * Si el formulario tiene botones y el botón de completado del espacio de trabajo de AEM Forms no está disponible, haga clic en el botón correspondiente del formulario para el siguiente paso requerido en el proceso.

   Si el formulario no tiene botones y el botón de completado del espacio de trabajo de AEM Forms no está disponible, aparece un mensaje que indica que el formulario no se puede enviar.

1. Si aparece un cuadro de diálogo de confirmación, realice una de estas acciones:

   * Haga clic en **OK** si ha completado la tarea y está lista para desconectarla.
   * Haga clic en **Cancelar** si desea volver a la tarea y no está listo para desconectarla.

>[!NOTE]
>
>Puede ver un botón Enviar dentro de los formularios de HTML cuando se utilizan Propiedades de proceso en un formulario. Este botón no está visible cuando el mismo formulario se procesa como PDF. Para completar una tarea, haga clic en el botón Enviar disponible en la parte inferior del espacio de trabajo de AEM Forms, fuera del formulario y no en el botón Enviar dentro del formulario.

### Tareas de aprobación masiva {#bulk-approve-tasks}

Puede enviar varias tareas desde la lista Tareas pendientes. Solo se pueden enviar juntas las tareas del mismo proceso, con los mismos nombres de tarea y las mismas opciones de ruta.

>[!NOTE]
>
>Esta opción está disponible si el campo isMustOpenToComplete no está seleccionado en el paso Asignar tarea de Workbench mientras se diseña un proceso.

1. En la página Tareas pendientes, en el panel izquierdo, seleccione la lista Tareas pendientes individual. Todas las tareas se muestran en el panel central.
1. Select **Habilitar modo masivo**. Las casillas de verificación aparecen delante de las tareas de la lista.

   >[!NOTE]
   >
   >Esta opción no está disponible para tareas para las que el campo isMustOpenToComplete está seleccionado en el paso Asignar tarea del área de trabajo, mientras se diseña un proceso. Las casillas de verificación de dichas tareas en la lista de tareas pendientes de ejecución permanecen deshabilitadas siempre.

1. Seleccione tareas para la aprobación masiva. Se pueden seleccionar varias tareas del mismo proceso, con los mismos nombres de tareas y las mismas opciones de ruta. Una vez que seleccione una tarea para su aprobación, solo permanecerán habilitadas las tareas con el mismo proceso, con los mismos nombres de tareas y las mismas opciones de ruta. El resto están incapacitados.

   ![1_bulkapproval](assets/1_bulkapproval.png)

1. Haga clic en la opción Submit disponible. Se envían las tareas seleccionadas.

   ![aprobación masiva](assets/bulkapproval.png)

## Participación en tareas a través del correo electrónico {#participating-in-tasks-through-email}

Puede recibir y completar tareas por correo electrónico. Al participar en tareas a través de correos electrónicos, no es necesario comprobar rutinariamente la lista de tareas pendientes para ver si hay nuevas tareas o consultar la página Seguimiento para ver el estado de una tarea.

En primer lugar, configure las preferencias de su espacio de trabajo de AEM Forms para recibir notificaciones por correo electrónico. El espacio de trabajo de AEM Forms puede enviar notificaciones por correo electrónico para tareas de la lista de tareas pendientes o de cualquier grupo al que pertenezca. El administrador determina cuándo se envían los mensajes de notificación por correo electrónico y quién los recibe.

Los mensajes de correo electrónico pueden contener un vínculo que abra la tarea en el espacio de trabajo de AEM Forms, un archivo adjunto del formulario que se utiliza para la tarea o acciones para completar la tarea por correo electrónico. Si se incluye un formulario en el mensaje de correo electrónico, se puede abrir el formulario y completar la tarea si los botones para completar la tarea están creados en el formulario. Si las acciones para completar la tarea se incluyen en el mensaje de correo electrónico, puede completar la tarea haciendo clic en las acciones del correo electrónico o respondiendo al correo electrónico con la acción escrita como primera línea en el cuerpo del correo electrónico.

>[!NOTE]
>
>* Para configurar el espacio de trabajo para que utilice las plantillas de correo electrónico adecuadas, consulte la [Guía del administrador de AEM Forms JEE](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/).
>
>* Si los borradores se reenvían después de enviar la tarea en el espacio de trabajo de AEM Forms, se envían notificaciones por correo electrónico. Si los borradores se reenvían desde el punto de partida del espacio de trabajo de AEM Forms, no se envían notificaciones por correo electrónico.


Cuando completa una tarea por correo electrónico, la tarea se elimina de la lista de tareas pendientes en el espacio de trabajo de AEM Forms.

>[!NOTE]
>
>Si el usuario no ha iniciado sesión en el espacio de trabajo de AEM Forms en el explorador y abre un vínculo a una tarea pendiente, el vínculo directo Tareas pendientes no se abre y muestra una excepción. Inicie sesión en el espacio de trabajo de AEM Forms antes de hacer clic en los vínculos de los correos electrónicos.

>[!NOTE]
>
>No se puede reenviar una notificación por correo electrónico para asignar una tarea a otra persona. Solo puede reenviar tareas a otros usuarios desde el espacio de trabajo de AEM Forms.

### Recibir mensajes de notificación por correo electrónico {#receive-email-notification-messages}

1. Haga clic en **Preferencias**.
1. En el **Notificar eventos de tarea por correo electrónico** lista, seleccionar **Sí**.
1. Para incluir el formulario y los datos con el mensaje de correo electrónico, en la variable **Adjuntar Forms en correo electrónico** lista, seleccionar **Sí**.

## Participación en tareas a través de dispositivos móviles {#participating-in-tasks-through-mobile-devices}

Puede utilizar la aplicación de espacio de trabajo de AEM Forms para participar en tareas desde su dispositivo móvil. Antes de instalar la aplicación, póngase en contacto con el administrador de sistemas para asegurarse de que su organización admite el uso de la aplicación de espacio de trabajo de AEM Forms.

## Acerca de los plazos y recordatorios {#about-deadlines-and-reminders}

A *límite* determina la fecha y la hora en la que debe completar una tarea. Cuando pasa una fecha límite, el servidor enruta la tarea al siguiente paso del proceso (que puede ser la lista de tareas pendientes de otro usuario) y, a continuación, aparece el icono de fecha límite en la tarea. El icono de fecha límite aparece independientemente de las reglas asociadas al proceso.

A *recordatorio* le notifica de una tarea que requiere su atención. Los recordatorios se producen en un momento predeterminado y luego a intervalos regulares hasta que se completa la tarea asociada. Cuando recibe un recordatorio, el icono del recordatorio aparece en la tarea.

El proceso empresarial determina el comportamiento y el tiempo de los plazos y recordatorios. No todos los procesos tienen plazos y recordatorios. El administrador especifica si las notificaciones por correo electrónico se envían para los plazos y recordatorios. Puede establecer sus preferencias sobre si desea recibir notificaciones por correo electrónico.

## Trabajo con tareas de grupos y colas compartidas {#working-with-tasks-from-group-and-shared-queues}

Todas las tareas asignadas aparecerán en la lista de tareas pendientes (cola).

Cualquier grupo y lista de tareas pendientes compartidas a las que tenga acceso también aparecerán en el panel izquierdo de la página de tareas pendientes. Puede completar tareas desde cualquier lista de tareas pendientes a la que tenga acceso.

Una lista de tareas pendientes de grupo puede tener más de un miembro. Un administrador configura listas de tareas pendientes de grupo en función de los requisitos específicos de su organización. Las listas de tareas pendientes de grupo ofrecen una forma de distribuir el trabajo entre varias personas que comparten responsabilidades similares.

Por ejemplo, cada miembro del equipo procesa los formularios de solicitud de préstamos. Todas estas tareas se envían a una lista de tareas pendientes de grupo a la que todos los miembros de su grupo tienen acceso. Cada miembro del grupo puede acceder a las tareas desde esa lista de tareas pendientes.

Se muestra una lista de tareas pendientes compartidas cuando otro usuario comparte con usted su lista de tareas pendientes o comparte explícitamente una tarea con usted. A continuación, puede ver las tareas de la lista de tareas pendientes de ese usuario y completarlas en su nombre. Por ejemplo, si está tomando unas vacaciones, puede optar por compartir la lista de tareas pendientes con un compañero que complete sus tareas mientras está fuera.

>[!NOTE]
>
>También puede especificar la configuración fuera de la oficina para reenviar tareas a otros usuarios mientras esté fuera.

Para trabajar en una tarea desde un grupo o una lista de tareas pendientes compartida, primero debe reclamar la tarea. A continuación, pase a ser el propietario de la tarea hasta que la complete o la reenvíe a otro usuario.

### Uso compartido de colas {#sharing-queues}

Puede compartir la lista de tareas pendientes con otro usuario, que puede ver las nuevas tareas en la lista de tareas pendientes y actuar en consecuencia por usted. Si existen tareas en la lista de tareas pendientes antes de compartir la lista de tareas pendientes, el otro usuario no puede verlas. El usuario puede ver y reclamar solamente las tareas que llegan a su lista de tareas pendientes después de conceder acceso a su lista de tareas pendientes.

Tenga en cuenta que para que un usuario vea una tarea en una cola compartida, el diseñador de procesos debe habilitar la opción Add ACL for Shared Queue en la pestaña Task Access Control List (ACL) del Servicio de usuario.

>[!NOTE]
>
>Si planea estar fuera de la oficina, también puede especificar la configuración fuera de la oficina para reenviar tareas a otros usuarios mientras esté fuera, en lugar de compartir toda la lista de tareas pendientes.

**Compartir la cola**

1. En el **Colas** en la ficha **Preferencias** , haga clic en el icono &quot;+&quot; para &quot;Usuarios que están compartiendo mi cola&quot;.
1. Busque y seleccione el nombre del usuario.
1. Haga clic en **Compartir** para compartir la cola con el usuario seleccionado.
1. Seleccione el nombre del usuario y haga clic en **Compartir**.

   >[!NOTE]
   >
   >Puede quitar un usuario para que no comparta su lista de tareas pendientes haciendo clic en **X** al final de la fila en la que aparece el usuario.

### Acceso a otras colas {#accessing-other-queues}

Puede solicitar acceso a la lista de tareas pendientes de otro usuario para ver y reclamar cualquier tarea nueva en la lista de tareas pendientes del usuario.

Cuando solicita acceso a la lista de tareas pendientes de otro usuario, el usuario recibe una tarea en la lista de tareas pendientes para aprobar o denegar la solicitud. Una vez que el usuario haya completado la tarea, recibirá una notificación en la lista de tareas pendientes.

Si se le concede acceso a la lista de tareas pendientes de otro usuario, no podrá ver ninguna tarea que existiera en la lista de tareas pendientes del usuario antes de que se le concediera acceso. Solo puede ver las tareas que llegan a la lista de tareas pendientes del usuario después de que se le haya concedido acceso a la lista de tareas pendientes.

**Acceso a otra cola**

1. En el **Preferencias** , abra la pestaña **Colas** pestaña .
1. Haga clic en &quot;+&quot; para las &quot;colas de usuario a las que tengo acceso&quot;. Busque el nombre del usuario en el cuadro de diálogo emergente.
1. Seleccione el nombre del usuario y haga clic en **Solicitud**.

   >[!NOTE]
   >
   >Puede quitar el acceso a otra lista de tareas pendientes seleccionando el nombre de usuario en la lista Colas de usuarios a las que tengo acceso y haciendo clic en **X** al final de la fila que menciona el nombre del usuario. No puede quitar el acceso a otra lista de tareas pendientes cuando la solicitud de acceso a la lista de tareas pendientes sigue pendiente.

## Configuración de las preferencias fuera de la oficina {#setting-out-of-office-preferences}

Si planea estar fuera de la oficina, puede especificar lo que sucede con las tareas asignadas a usted durante ese período.

Tiene la opción de especificar una fecha y una hora de inicio y una fecha y una hora de finalización para aplicar la configuración de Fuera de la oficina. Si se encuentra en una zona horaria diferente del servidor, la zona horaria utilizada es la del servidor.

Puede establecer una persona predeterminada a la que se envían todas las tareas. También puede especificar excepciones para que las tareas de procesos específicos se envíen a un usuario diferente o se mantengan en la lista de tareas pendientes hasta que vuelva. Si la persona designada también está fuera de la oficina, la tarea se dirige al usuario que designaron. Si la tarea no se puede asignar a un usuario que no está fuera de la oficina, la tarea permanece en la lista de tareas pendientes.

>[!NOTE]
>
>Cuando esté fuera de la oficina, cualquier tarea que anteriormente estaba en la lista de tareas pendientes permanecerá allí y no se reenviará a otros usuarios.

### Establecer preferencias fuera de la oficina {#set-out-of-office-preferences}

1. Haga clic en **Preferencias** y haga clic en **Fuera de la oficina**.
1. Para especificar cuándo está fuera de la oficina, realice uno de estos pasos:

   * Para especificar que está fuera de la oficina ahora por un período de tiempo indefinido, en la **Actualmente** lista, seleccionar **Fuera de la oficina** pero no agregue un intervalo de fechas.
   * Para especificar la fecha y hora de inicio en las que se encuentra fuera de la oficina, haga clic en &quot;+&quot; para **Programación fuera de la oficina**. Utilice el calendario y la lista de tiempo para especificar la fecha y la hora de inicio. Si no especifica una fecha y hora de finalización, se considerará que está fuera de la oficina indefinidamente desde la fecha y hora de inicio hasta que cambie sus preferencias.

1. Para especificar cómo se van a gestionar las tareas de forma predeterminada, seleccione una de estas opciones en el **Fuera de la oficina: Usuario predeterminado para tareas fuera de la oficina** lista:

   * Select **No asignar** para mantener las tareas en la lista de tareas pendientes hasta que vuelva.
   * Select **Buscar usuario** para buscar un usuario al que asignar sus tareas. Al seleccionar un usuario, también puede ver su programación fuera de la oficina.

1. Para establecer excepciones a la opción predeterminada, haga clic en + para **Excepciones de procesos**, seleccione el proceso para crear una excepción y, a continuación, seleccione un usuario diferente o **No asignar** de la variable **se asigna a** lista.

   >[!NOTE]
   >
   >El diseñador de procesos puede especificar que las tareas de algunos procesos siempre se mantengan privadas y no se reenvíen a otros usuarios. Esta configuración anula cualquier configuración que realice.

1. Cuando termine de configurar las preferencias, haga clic en **Guardar**. Si la configuración indica que actualmente está fuera de la oficina, los cambios entrarán en vigor inmediatamente. De lo contrario, se aplican en la fecha y hora de inicio especificadas. Si inicia sesión mientras está fuera de la oficina, no se considerará que ha vuelto hasta que cambie la configuración.
