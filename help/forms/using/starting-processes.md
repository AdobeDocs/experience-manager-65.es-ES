---
title: Inicio de procesos
seo-title: Starting processes
description: 'Cómo utilizar el espacio de trabajo de AEM Forms de LiveCycle: seleccione procesos, añada notas y archivos adjuntos, guarde borradores de copias y agréguelas a favoritos.'
seo-description: How to use LiveCycle AEM Forms workspace--select processes, add notes and attachments, save draft copies, and add to favorites.
uuid: a61da785-25b4-4482-bd72-02e250d35dc7
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c9d3f369-3744-41d5-b340-390ab7e03f36
exl-id: b2a6ba3a-0f4c-44b1-8f9a-c15c6fb8c305
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 0%

---

# Inicio de procesos {#starting-processes}

El espacio de trabajo de AEM Forms organiza los procesos según las categorías que el administrador o el diseñador de procesos configuran. También puede colocar en la categoría Favoritos procesos que utilice con frecuencia para poder encontrarlos rápidamente.

Al iniciar un proceso, es posible que deba rellenar un formulario para iniciar un proceso empresarial que controla el flujo de trabajo de AEM Forms. Si un formulario utiliza el proceso de preparación de datos, parte de la información se puede rellenar previamente en un formulario en blanco cuando se inicia un nuevo proceso.

Por ejemplo, desea adquirir un monitor de equipo nuevo y, por lo tanto, iniciar un proceso llamado *Orden de compra*. Cuando se inicia el proceso, se abre un formulario y se solicita información detallada sobre el elemento que se va a solicitar. Es posible que el nombre, el número de empleado y el nombre del administrador ya se hayan rellenado previamente en el formulario. Al enviar la solicitud, se inicia un proceso empresarial. En función de la definición del proceso, el servidor enruta automáticamente la solicitud a su administrador. La tarea empieza a aparecer en la lista de tareas pendientes del administrador. Cuando el administrador aprueba la solicitud, el flujo de trabajo de formularios envía la solicitud al departamento de compras y le envía una notificación por correo electrónico.

## Selección de procesos para el inicio {#selecting-processes-to-start}

Puede seleccionar un proceso para iniciarlo o para ver más información al respecto.

Al seleccionar un proceso para iniciarlo, es posible que deba rellenar un formulario asociado a dicho proceso. Al enviar el formulario, se inicia el proceso.

Se admite Forms en varios tipos de formatos de archivo, incluidos Adobe PDF, HTML y archivo SWF. Un formulario puede parecer un formulario tradicional imprimible o basado en la Web o puede guiarle a través de una serie de paneles de estilo asistente para recopilar información.

Si el formulario y el proceso lo permiten, también se puede guardar el formulario sin conexión, rellenarlo y enviarlo para completar la tarea. Cuando se envía el formulario, el cliente de correo electrónico se inicia con la dirección de correo electrónico del servidor correspondiente, si se ha configurado el punto final del correo electrónico. A continuación, puede enviar el formulario completado al servidor por correo electrónico.

Al seleccionar un proceso, aparecen la ficha Formulario y la ficha Detalles. Si el proceso permite añadir notas o archivos adjuntos, también aparecen la pestaña Attachments y la pestaña Notes . Si también ha configurado la dirección URL de resumen con el proceso, también aparecerá la pestaña Resumen. La ficha Forms muestra el formulario asociado y la ficha Detalles muestra información sobre la tarea actual y el proceso del que forma parte.

### Iniciar un proceso empresarial {#start-a-business-process}

1. En la página Proceso de Inicio , en la lista de la izquierda, seleccione una categoría. Todos los procesos a los que tiene acceso en la categoría aparecen a la derecha.

   >[!NOTE]
   >
   >Si el panel Categorías está contraído, haga clic en &quot;Abrir categorías&quot;, en el área superior izquierda del espacio de trabajo de AEM Forms, para abrir el panel.

1. Seleccione un proceso haciendo clic en una tarea. El formulario asociado al proceso se abre en la ficha Formulario.

   Cada formulario de un proceso tiene una dirección URL única. Puede utilizar la dirección URL única para iniciar directamente el espacio de trabajo del HTML con el proceso y el formulario específicos. El formato de la dirección URL es https://&lt;server>:&lt;port>/lc/libs/ws/index.html#/startprocess/&lt;applicationname>%2F&lt;processname>. La variable &lt;applicationname>%2F&lt;processname> siempre tiene codificación de dirección URL. Una URL de ejemplo es http://localhost:8080/lc/libs/ws/index.html#/startprocess/MyApplication%2FNewProcess. La cadena ApplicationName%2FProcessName del ejemplo tiene codificación de dirección URL.

1. Rellene el formulario según las instrucciones proporcionadas. Si es necesario, haga clic en **Maximizar** para aumentar el área visible del formulario.
1. Si la pestaña Attachments está disponible, añada los archivos adjuntos según sea necesario.
1. Si la ficha Notas está disponible, proporcione las notas que sean necesarias.
1. Realice uno de estos pasos:

   * Haga clic en el botón Enviar del formulario si este tiene un botón Enviar.
   * Haga clic en Completar debajo del formulario si este no tiene un botón Enviar.

   Process Management inicia el proceso y enruta el formulario a las listas de tareas pendientes de las personas adecuadas que necesiten completar la siguiente tarea del proceso.

   Si debe cerrar un formulario antes de enviarlo y sin perder los datos introducidos, guarde un borrador y complételo más tarde si el proceso lo permite. Si el formulario y el proceso lo permiten, también puede hacer clic en **Sin conexión** y luego envíelo desde Adobe® Reader® o Adobe® Acrobat® Professional o Acrobat Standard.

   >[!NOTE]
   >
   >La opción sin conexión solo está disponible para PDF forms.

## Adición de notas y archivos adjuntos {#adding-notes-and-attachments}

Puede agregar notas y archivos adjuntos a un proceso si el proceso lo permite. Puede proporcionar permisos para otros usuarios que participen en el proceso para ver, actualizar y eliminar las notas o archivos adjuntos.

### Agregar una nota {#add-a-note}

Puede agregar varias notas, editarlas y eliminarlas. Cada nota tiene un título, una descripción y un permiso de acceso asociado. Puede establecer uno de los siguientes permisos de acceso en una nota:

* Solo lectura (el permiso predeterminado)
* Leer/Editar/Eliminar
* Lectura/Edición
* Lectura/Eliminación
* Sin acceso

1. Abra una tarea y haga clic en el botón **Notas** , si el proceso lo permite.
1. Escriba un título para la nota en la **Título** y escriba el texto de la nota en el **Nota** en la ventana
1. Seleccione el **Permisos** para la nota para otros usuarios que participan en el proceso.
1. Haga clic en **Aceptar**. Se adjunta al formulario un archivo de texto que contiene la nota. Para actualizar una nota, haga clic en ella y modifique directamente el texto. Para eliminar una nota, haga clic en el botón **Eliminar** botón ![Imagen de una papelera](assets/icondelete.png) junto a la nota.

### Añadir un archivo adjunto {#add-an-attachment}

También puede añadir sus comentarios sobre el archivo adjunto. Puede establecer uno de los siguientes permisos de acceso en un archivo adjunto:

* Solo lectura (el permiso predeterminado)
* Leer/Editar/Eliminar
* Lectura/Edición
* Lectura/Eliminación
* Sin acceso

1. Haga clic en el **Archivos adjuntos** y seleccione **Archivo adjunto**.
1. Haga clic en **Examinar** para seleccionar el archivo que desea adjuntar.
1. Seleccione el **Permisos** para el archivo adjunto para otros usuarios que participan en el proceso. Si selecciona **Lectura**, otros usuarios pueden guardar el archivo localmente. Si selecciona uno de los permisos de edición, otros usuarios también pueden cargar un nuevo archivo para reemplazar el archivo adjunto.
1. Haga clic en **Aceptar**. El archivo se adjunta al formulario. Para eliminar un archivo, haga clic en el botón **Eliminar** botón ![Imagen de una papelera](assets/icondelete.png) junto al archivo adjunto.

## Guardado de copias de borrador de formularios {#saving-draft-copies-of-forms}

Si debe completar y enviar un formulario más adelante, puede guardar una copia borrador de un formulario para que no pierda el trabajo existente. Los borradores de copias se añaden a la categoría Borradores de la página Tareas pendientes .

Después de volver a abrir y enviar un formulario borrador, el borrador se elimina de la categoría Borradores .

Además, puede configurar Workspace para que guarde automáticamente la información introducida por un usuario como borrador. Para obtener más información, consulte [Preferencias de administración](/help/forms/using/getting-started-livecycle-html-workspace.md).

>[!NOTE]
>
>El botón Guardar no está disponible para algunos formularios, según el proceso con el que esté asociado.

### Guardar una copia de borrador {#save-a-draft-copy}

1. Haga clic en **Guardar** en la esquina inferior izquierda de cualquier pestaña. El formulario se agrega a la categoría Borradores de la página Tareas pendientes. Se guardarán todos los cambios realizados en el formulario.

### Volver a abrir un borrador {#reopen-a-draft-copy}

1. En la página Tareas pendientes, seleccione la opción **Borradores** y haga clic en el borrador de la copia del formulario.

   Si el formulario contiene una serie de paneles, es posible que tenga que ir al panel donde finalizó la última sesión.

## Adición de procesos a la categoría Favoritos {#adding-processes-to-the-favorites-category}

Puede agregar cualquier proceso a la categoría Favoritos . Al establecer favoritos, puede agrupar todos los procesos que inicia con frecuencia en una sola categoría para que pueda encontrarlos rápidamente.

>[!NOTE]
>
>Si normalmente inicia procesos al utilizar el espacio de trabajo de AEM Forms, puede establecer la preferencia Iniciar ubicación para que muestre automáticamente la categoría Favoritos al iniciar el espacio de trabajo de AEM Forms. Para obtener más información, consulte Administración de preferencias en [Introducción al espacio de trabajo de AEM Forms](/help/forms/using/getting-started-livecycle-html-workspace.md).

Para marcar un proceso como favorito, seleccione la tarea en su categoría y haga clic en la estrella hueca. La estrella se vuelve dorada. Para desmarcar un proceso como favorito, haga clic de nuevo en la estrella dorada.
