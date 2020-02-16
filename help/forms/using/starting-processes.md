---
title: Iniciando procesos
seo-title: Iniciando procesos
description: 'Cómo utilizar el espacio de trabajo de LiveCycle AEM Forms: seleccione procesos, agregue notas y archivos adjuntos, guarde copias de borrador y agréguelas a favoritos.'
seo-description: 'Cómo utilizar el espacio de trabajo de LiveCycle AEM Forms: seleccione procesos, agregue notas y archivos adjuntos, guarde copias de borrador y agréguelas a favoritos.'
uuid: a61da785-25b4-4482-bd72-02e250d35dc7
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c9d3f369-3744-41d5-b340-390ab7e03f36
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Iniciando procesos {#starting-processes}

El espacio de trabajo de AEM Forms organiza los procesos según las categorías configuradas por el administrador o el diseñador de procesos. También puede colocar procesos que utilice con frecuencia en la categoría Favoritos para que pueda encontrarlos rápidamente.

Al iniciar un proceso, es posible que deba rellenar un formulario para iniciar un proceso empresarial que controla el flujo de trabajo de AEM Forms. Si un formulario utiliza Preparar proceso de datos, parte de la información se puede rellenar previamente en un formulario en blanco cuando se inicia un nuevo proceso.

Por ejemplo, desea comprar un nuevo monitor de equipo y, por lo tanto, iniciar un proceso denominado Orden *de compra*. Cuando se inicia el proceso, se abre un formulario y se le solicita información detallada sobre el elemento que se va a ordenar. Es posible que el nombre, el número de empleado y el nombre del administrador ya estén rellenados previamente en el formulario. Al enviar la solicitud, se inicia un proceso comercial. En función de la definición del proceso, el servidor redirecciona automáticamente la solicitud a su administrador. La tarea empieza a aparecer en la lista de tareas pendientes del administrador. Cuando el administrador aprueba la solicitud, el flujo de trabajo de formularios envía la solicitud al departamento de compras y le envía una notificación por correo electrónico.

## Selección de procesos para iniciar {#selecting-processes-to-start}

Puede seleccionar un proceso para iniciarlo o para ver más información al respecto.

Al seleccionar un proceso para iniciar, es posible que deba rellenar un formulario asociado a dicho proceso. Al enviar el formulario, se inicia el proceso.

Se admiten formularios en varios tipos de formatos de archivo, incluidos archivos PDF, HTML y SWF de Adobe. Un formulario puede parecer un formulario tradicional imprimible o basado en Web o puede guiarlo a través de una serie de paneles de estilo asistente para recopilar información.

Si el formulario y el proceso lo permiten, también puede guardarlo sin conexión, rellenarlo y enviarlo para completar la tarea. Cuando se envía el formulario, el cliente de correo electrónico se inicia con la dirección de correo electrónico del servidor correspondiente, si se ha configurado el punto final del correo electrónico. A continuación, puede enviar el formulario completado al servidor por correo electrónico.

Al seleccionar un proceso, aparecen la ficha Formulario y la ficha Detalles. Si el proceso le permite agregar notas o archivos adjuntos, también aparecen la ficha Archivos adjuntos y la ficha Notas. Si también ha configurado la URL de resumen con el proceso, también aparecerá la ficha Resumen. La ficha Formularios muestra el formulario asociado y la ficha Detalles muestra información sobre la tarea actual y el proceso del que forma parte.

### Iniciar un proceso comercial {#start-a-business-process}

1. En la lista de la izquierda de la página Iniciar proceso, seleccione una categoría. Todos los procesos a los que tiene acceso en la categoría aparecen a la derecha.

   >[!NOTE]
   >
   >Si el panel Categorías está contraído, haga clic en &#39;Abrir categorías&#39;, en el área superior izquierda del espacio de trabajo de AEM Forms, para abrir el panel.

1. Seleccione un proceso haciendo clic en una tarea. El formulario asociado al proceso se abre en la ficha Formulario.

   Cada formulario de un proceso tiene una dirección URL única. Puede utilizar la dirección URL única para iniciar directamente el espacio de trabajo HTML con el proceso y el formulario específicos. El formato de la dirección URL es https://&lt;server>:&lt;port>/lc/libs/ws/index.html#/startprocess/&lt;ApplicationName>%2F&lt;ProcessName>. La cadena &lt;ApplicationName>%2F&lt;ProcessName> siempre está codificada en la dirección URL. Una URL de ejemplo es http://localhost:8080/lc/libs/ws/index.html#/startprocess/MyApplication%2FNewProcess. La cadena ApplicationName%2FProcessName del ejemplo está codificada con dirección URL.

1. Rellene el formulario según las instrucciones proporcionadas. Si es necesario, haga clic en **Maximizar** para aumentar el área visible del formulario.
1. Si la ficha Archivos adjuntos está disponible, agregue los archivos adjuntos según sea necesario.
1. Si la ficha Notas está disponible, proporcione las notas necesarias.
1. Realice uno de estos pasos:

   * Haga clic en el botón Enviar del formulario, si el formulario tiene un botón Enviar.
   * Haga clic en Completar debajo del formulario, si éste no tiene un botón Enviar.
   Process Management inicia el proceso y enruta el formulario a las listas de tareas pendientes de las personas adecuadas que necesiten completar la siguiente tarea del proceso.

   Si debe cerrar un formulario antes de enviarlo y sin perder los datos introducidos, guarde un borrador y rellénelo más tarde si el proceso lo permite. Si el formulario y el proceso lo permiten, también puede hacer clic en **Sin conexión** y enviarlo posteriormente desde Adobe® Reader® o Adobe® Acrobat® Professional o Acrobat Standard.

   >[!NOTE]
   >
   >La opción sin conexión solo está disponible para formularios PDF.

## Adición de notas y archivos adjuntos {#adding-notes-and-attachments}

Puede agregar notas y archivos adjuntos a un proceso si el proceso lo permite. Puede proporcionar permisos a otros usuarios que participen en el proceso para ver, actualizar y eliminar las notas o los archivos adjuntos.

### Agregar una nota {#add-a-note}

Puede agregar varias notas, editarlas y eliminarlas. Cada nota tiene un título, una descripción y un permiso de acceso asociado. Puede definir uno de los siguientes permisos de acceso en una nota:

* Solo lectura (el permiso predeterminado)
* Leer/Editar/Eliminar
* Leer/Editar
* Leer/Eliminar
* Sin acceso

1. Abra una tarea y haga clic en la ficha **Notas** , si el proceso lo permite.
1. Escriba un título para la nota en el cuadro **Título** y escriba el texto de la nota en el cuadro **Nota** .
1. Seleccione el nivel de **permisos** de la nota para otros usuarios que participen en el proceso.
1. Haga clic en **Aceptar**. Se adjunta al formulario un archivo de texto que contiene la nota. Puede actualizar una nota haciendo clic en ella y modificando directamente el texto. Puede eliminar una nota haciendo clic en el botón **Eliminar** ![Imagen de una papelera](assets/icondelete.png) al lado de la nota.

### Agregar un archivo adjunto {#add-an-attachment}

También puede agregar sus comentarios sobre el archivo adjunto. Puede definir uno de los siguientes permisos de acceso en un archivo adjunto:

* Solo lectura (el permiso predeterminado)
* Leer/Editar/Eliminar
* Leer/Editar
* Leer/Eliminar
* Sin acceso

1. Haga clic en la ficha **Archivos adjuntos** y seleccione **Datos adjuntos**.
1. Haga clic en **Examinar** para seleccionar el archivo que desea adjuntar.
1. Seleccione el nivel de **permisos** para los datos adjuntos de otros usuarios que participen en el proceso. Si selecciona **Leer**, otros usuarios pueden guardar el archivo localmente. Si selecciona uno de los permisos de edición, otros usuarios también pueden cargar un nuevo archivo para reemplazar los datos adjuntos.
1. Haga clic en **Aceptar**. El archivo se adjunta al formulario. Puede eliminar un archivo haciendo clic en el botón **Eliminar** ![Imagen de una papelera](assets/icondelete.png) al lado del archivo adjunto.

## Guardar copias de borrador de formularios {#saving-draft-copies-of-forms}

Si debe completar y enviar un formulario más adelante, puede guardar una copia borrador de un formulario para que no pierda el trabajo existente. Los borradores se agregan a la categoría Borradores de la página Tareas pendientes.

Después de volver a abrir y enviar un formulario de borrador, el borrador se elimina de la categoría Borradores.

Además, puede configurar el espacio de trabajo para guardar automáticamente la información introducida por un usuario como borrador. Para obtener más información, consulte [Administración de preferencias](/help/forms/using/getting-started-livecycle-html-workspace.md).

>[!NOTE]
>
>El botón Guardar no está disponible para algunos formularios, según el proceso con el que esté asociado.

### Guardar una copia de borrador {#save-a-draft-copy}

1. Haga clic en **Guardar** en la esquina inferior izquierda de cualquier ficha. El formulario se agrega a la categoría Borradores de la página Tareas pendientes. Se guardarán todos los cambios realizados en el formulario.

### Volver a abrir una copia de borrador {#reopen-a-draft-copy}

1. En la página Tareas pendientes, seleccione la cola **Borradores** y haga clic en la copia de borrador del formulario.

   Si el formulario contiene una serie de paneles, es posible que tenga que ir al panel donde finalizó la última sesión.

## Adición de procesos a la categoría Favoritos {#adding-processes-to-the-favorites-category}

Puede agregar cualquier proceso a la categoría Favoritos. Al establecer favoritos, puede agrupar todos los procesos que inicia con frecuencia en una sola categoría para que pueda encontrarlos rápidamente.

>[!NOTE]
>
>Si normalmente inicia procesos al utilizar el espacio de trabajo de AEM Forms, puede definir la preferencia de Ubicación de inicio para que se muestre automáticamente la categoría Favoritos al iniciar el espacio de trabajo de AEM Forms. Para obtener más información, consulte Administración de preferencias en [Introducción al espacio de trabajo](/help/forms/using/getting-started-livecycle-html-workspace.md)de AEM Forms.

Para marcar un proceso como favorito, seleccione la tarea en su categoría y haga clic en la estrella vacía. La estrella se vuelve dorada. Para desmarcar un proceso como favorito, vuelva a hacer clic en la estrella dorada.

[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
