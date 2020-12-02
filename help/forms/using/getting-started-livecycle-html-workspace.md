---
title: Introducción al espacio de trabajo de AEM Forms
seo-title: Introducción al espacio de trabajo de AEM Forms
description: Cómo empezar a utilizar el espacio de trabajo de LiveCycle AEM Forms para administrar los procesos de automatización empresarial.
seo-description: Cómo empezar a utilizar el espacio de trabajo de LiveCycle AEM Forms para administrar los procesos de automatización empresarial.
uuid: 35ca1a51-92c3-40d8-8de3-604be8704752
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: fa6e0246-6bd2-4ffb-b54c-15eda605f213
translation-type: tm+mt
source-git-commit: 49da3dbe590f70b98185a6bc330db6077dc864c0
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 0%

---


# Introducción al área de trabajo de AEM Forms {#getting-started-with-aem-forms-workspace}

Puede utilizar el espacio de trabajo de AEM Forms para realizar las siguientes tareas:

* Inicio de un proceso comercial
* Vista y actuar en función de tareas que estén asignadas a usted o a otras listas de tareas pendientes a las que tenga acceso
* Rastree tareas que formen parte de los procesos en los que ha iniciado o en los que ha participado

## Navegación por el espacio de trabajo de AEM Forms {#navigating-html-workspace}

Se muestran diferentes elementos en la interfaz de usuario del espacio de trabajo de AEM Forms según el proceso y la tarea en que esté trabajando. Puede ver o no las fichas Resumen, Forms, Detalles, Historial, Anexos o Notas, o todos los botones que se describen en esta Ayuda en todo momento.

Puede desplazarse por la interfaz de usuario principal del espacio de trabajo de AEM Forms mediante cualquiera de los siguientes métodos:

* Haga clic en los elementos de la barra de navegación superior para acceder a la opción Proceso de Inicio, lista de tareas pendientes, Preferencias, Seguimiento, Ayuda y Cerrar sesión.
* Haga clic en la ficha Proceso de Inicio, Tareas pendientes o Seguimiento para acceder a las tres áreas de trabajo principales.
* En las fichas Proceso de Inicio, Tareas pendientes y Seguimiento, haga clic en los elementos de la lista del panel izquierdo para acceder a favoritos, categorías de proceso, plantillas de búsqueda, borradores o tareas asignadas. Utilice la barra de desplazamiento para ver elementos adicionales en la lista.
* Todos los botones de acción (Aprobar, Rechazar, Avanzar, Consultar, Bloquear y Compartir) muestran tanto el documento como la propiedad.
* Haga clic en el icono Todas las opciones de la barra de navegación, en la parte inferior de la página, para reenviar la tarea a otro usuario, compartir la tarea con otro usuario, consultar la tarea con otro usuario o bloquear la tarea.
* En la ficha Historial, seleccione una tarea para mostrar las fichas Datos adjuntos y Asignaciones de esa tarea.
* Utilice la tecla de tabulación, las teclas de flecha y la barra espaciadora para navegar por el espacio de trabajo de AEM Forms sin utilizar el ratón.

## Uso del espacio de trabajo de AEM Forms con lectores de pantalla {#using-html-workspace-with-screen-readers}

El espacio de trabajo de AEM Forms es una aplicación HTML basada en web y es compatible con los lectores de pantalla. Puede navegar por la interfaz del espacio de trabajo de AEM Forms mediante el teclado.

Para utilizar el espacio de trabajo de AEM Forms con un lector de pantalla, tenga en cuenta estos puntos:

* El espacio de trabajo de AEM Forms es una aplicación HTML estándar que cumple con cualquier herramienta de lectura de pantalla estándar. No necesita ningún script específico para ejecutar una herramienta de lectura de pantalla.
* Toda la navegación en el espacio de trabajo de AEM Forms se realiza mediante etiquetas de anclaje, a las que se puede acceder fácilmente a través de fichas.
* Forms puede tardar unos segundos en cargarse. El lector de pantalla no le informa de forma auditiva de que el formulario se está cargando y de que debe esperar.

## Desplazamiento por el espacio de trabajo de AEM Forms mediante un teclado {#navigating-html-workspace-using-a-keyboard}

Cuando navega por el espacio de trabajo de AEM Forms mediante un teclado, la navegación se ajusta a las convenciones de accesibilidad HTML. En determinadas situaciones, el orden de tabulación no sigue el orden convencional habitual. Las siguientes sugerencias le ayudan a navegar por la interfaz:

* Si tiene problemas al desplazarse por las barras de herramientas de la parte superior del explorador, pulse Ctrl+Tab para desplazarse por el contenido de la ventana del explorador.
* La Ayuda del espacio de trabajo de AEM Forms se abre en una ventana separada del explorador. Tras la vista de la Ayuda, el enfoque vuelve a la ventana del explorador que contiene el espacio de trabajo de AEM Forms. El menú Ayuda permanece enfocado cuando vuelve el enfoque.
* Al abrir un formulario para inicio de un proceso o completar una tarea, el enfoque permanece en el elemento existente y no cambia al formulario. Utilice la ficha para mover el enfoque al formulario y navegar por él. El orden de tabulación a través del formulario depende del tipo y el diseño del formulario.

   Para los PDF forms, cuando se desplaza el cursor hasta el final del formulario o se envía el formulario, el cursor se desplaza a la barra de direcciones del explorador. Para ir a los botones de acción del formulario, como Guardar como borrador y Completar, debe volver a desplazarse por los menús mediante el tabulador (pero no por todo el formulario). Si el formulario sigue abierto, también puede tabular más allá de los botones y volver al formulario.

## Administración de preferencias {#managing-preferences}

Puede definir las distintas preferencias del espacio de trabajo de AEM Forms en las siguientes categorías:

**Fuera de la oficina:** defina las preferencias para controlar cómo se asignan las tareas a otras personas mientras se encuentra fuera de la oficina. Consulte [Configuración de preferencias fuera de la oficina](todo-lists.md#setting-out-of-office-preferences).

**Colas:** defina las preferencias para compartir la lista de tareas pendientes con otros usuarios o para solicitar acceso a la lista de otro usuario. Consulte [Trabajo con tareas de grupos y colas compartidas](todo-lists.md#working-with-tasks-from-group-and-shared-queues).

**Configuración de interfaz de usuario:** defina las preferencias para la forma en que interactúa con el espacio de trabajo de AEM Forms. Consulte [Configuración de las preferencias de la interfaz de usuario](#set-user-interface-preferences).

### Establecer las preferencias de la interfaz de usuario {#set-user-interface-preferences}

Defina las preferencias de la interfaz de usuario en la ficha Preferencias > Configuración de la interfaz de usuario. Están disponibles las siguientes preferencias.

* **Ubicación de inicio:** especifica la página que aparece al iniciar sesión en el espacio de trabajo de AEM Forms. Las cuatro opciones disponibles son Proceso de Inicio, Tareas pendientes, Seguimiento y Favoritos.
* **Mensaje de cierre de sesión:** especifica si se le solicita que confirme que desea cerrar la sesión después de hacer clic en Cerrar sesión.
* **Formato de fecha:** especifica el formato de visualización de fecha utilizado en el espacio de trabajo de AEM Forms.
* **Formato** de hora: Especifica el formato de visualización de tiempo utilizado en el espacio de trabajo de AEM Forms.
* **Notificar Eventos de Tarea por correo electrónico:** especifica si recibe notificaciones por correo electrónico de eventos de tarea, incluidas asignaciones de tarea, recordatorios y plazos para tareas en la lista de tareas pendientes y en listas de tareas pendientes de grupo a las que pertenece.
* **Adjuntar Forms en correo electrónico:** especifica si una copia del formulario está adjunta a los mensajes de notificación por correo electrónico. Los archivos adjuntos solo se admiten para formularios PDF y XDP.
* **Guardar borrador periódicamente:** especifica si los borradores de formulario se guardan automáticamente de forma periódica o no. Para guardar los borradores periódicamente, habilite esta opción y defina la duración del guardado automático de 1 a 30 minutos. Cuando el guardado automático está activado y un usuario está trabajando en un borrador, el borrador se guarda periódicamente después del número especificado de minutos. El borrador se guarda automáticamente solo cuando se produce un cambio en el borrador desde la última vez que se guarda o se guarda automáticamente. Cuando se guarda el borrador, aparece un mensaje de alerta en la pantalla.
