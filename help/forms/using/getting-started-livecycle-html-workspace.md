---
title: Introducción al espacio de trabajo de AEM Forms
seo-title: Getting started with AEM Forms workspace
description: Introducción al uso del espacio de trabajo de AEM Forms de LiveCycle para administrar los procesos de automatización empresarial.
seo-description: How to get started with using the LiveCycle AEM Forms workspace to manage your business automation processes.
uuid: 35ca1a51-92c3-40d8-8de3-604be8704752
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: fa6e0246-6bd2-4ffb-b54c-15eda605f213
exl-id: d2a962b6-16be-4866-a856-5064f81c9610
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 0%

---

# Introducción al espacio de trabajo de AEM Forms {#getting-started-with-aem-forms-workspace}

Puede utilizar el espacio de trabajo de AEM Forms para realizar las siguientes tareas:

* Iniciar un proceso empresarial
* Ver y actuar sobre las tareas asignadas a usted o a otras listas de tareas pendientes a las que tiene acceso
* Rastree las tareas que forman parte de los procesos en los que ha iniciado o en los que ha participado

## Navegación por el espacio de trabajo de AEM Forms {#navigating-html-workspace}

Se muestran distintos elementos en la interfaz de usuario del espacio de trabajo de AEM Forms según el proceso y la tarea en los que esté trabajando. Puede que vea o no las fichas Resumen, Forms, Detalles, Historial, Archivos adjuntos o Notas, o todos los botones que se describen en esta Ayuda en todo momento.

Puede navegar por la interfaz de usuario principal del espacio de trabajo de AEM Forms mediante cualquiera de los métodos siguientes:

* Haga clic en los elementos de la barra de navegación superior para acceder a la opción Iniciar proceso, Lista de tareas pendientes, Preferencias, Seguimiento, Ayuda y cierre de sesión.
* Haga clic en la pestaña Iniciar proceso, Tareas pendientes o Seguimiento para acceder a las tres áreas de trabajo principales.
* En las pestañas Iniciar proceso, Tareas pendientes y Seguimiento, haga clic en los elementos de la lista del panel izquierdo para acceder a favoritos, categorías de proceso, plantillas de búsqueda, borradores o tareas asignadas. Utilice la barra de desplazamiento para ver elementos adicionales en la lista.
* Todos los botones de acción (Aprobar, Rechazar, Reenviar, Consultar, Bloquear y Compartir) muestran tanto el documento como la propiedad.
* Haga clic en el icono Todas las opciones de la barra de navegación, en la parte inferior de la página, para reenviar la tarea a otro usuario, para compartir la tarea con otro usuario, para consultar la tarea con otro usuario o para bloquear la tarea.
* En la pestaña History , seleccione una tarea para mostrar las pestañas Attachments y Assigned de esa tarea.
* Utilice la tecla de tabulación, las teclas de flecha y la barra espaciadora para navegar por el espacio de trabajo de AEM Forms sin utilizar el ratón.

## Uso del espacio de trabajo de AEM Forms con lectores de pantalla {#using-html-workspace-with-screen-readers}

El espacio de trabajo de AEM Forms es una aplicación de HTML basada en web y es compatible con los lectores de pantalla. Puede navegar por la interfaz del espacio de trabajo de AEM Forms mediante el teclado.

Para utilizar el espacio de trabajo de AEM Forms con un lector de pantalla, tenga en cuenta estos puntos:

* AEM Forms workspace es una aplicación de HTML estándar que cumple con cualquier herramienta de lector de pantalla estándar. No necesita ningún script específico para ejecutar una herramienta de lector de pantalla.
* Toda la navegación en el espacio de trabajo de AEM Forms se realiza mediante etiquetas de anclaje, a las que se puede acceder fácilmente mediante pestañas.
* Forms puede tardar unos segundos en cargarse. El lector de pantalla no le informa de forma auditiva de que el formulario se está cargando y que debe esperar.

## Navegación por el espacio de trabajo de AEM Forms mediante un teclado {#navigating-html-workspace-using-a-keyboard}

Cuando navega por el espacio de trabajo de AEM Forms mediante un teclado, la navegación se ajusta a las convenciones de accesibilidad del HTML. En determinadas situaciones, el orden de tabulación no sigue el orden convencional típico. Las siguientes sugerencias le ayudan a navegar por la interfaz:

* Si tiene problemas para desplazarse por las barras de herramientas en la parte superior del explorador, pulse Ctrl+Tab para acceder a la pestaña del contenido de la ventana del explorador.
* La Ayuda del espacio de trabajo de AEM Forms se abre en una ventana independiente del explorador. Después de ver la Ayuda, el foco vuelve a la ventana del explorador que contiene el espacio de trabajo de AEM Forms. El menú Ayuda permanece centrado cuando vuelve el foco.
* Cuando se abre un formulario para iniciar un proceso o completar una tarea, el foco permanece en el elemento existente y no cambia en el formulario. Utilice la pestaña para mover el enfoque al formulario y navegar por él. El orden de tabulación a través del formulario depende del tipo y el diseño del formulario.

   Para los PDF forms, cuando se desplaza hasta el final del formulario o se envía el formulario, el cursor salta a la barra de direcciones del explorador. Debe volver a desplazarse por los menús (pero no por todo el formulario) para ir a los botones de acción del formulario, como Guardar como borrador y completado. Si el formulario sigue abierto, también puede tabular más allá de los botones y volver al formulario.

## Administración de preferencias {#managing-preferences}

Puede definir las distintas preferencias de espacio de trabajo de AEM Forms en las siguientes categorías:

**Fuera de la oficina:** Establezca preferencias para controlar cómo se asignan las tareas a otras personas mientras esté fuera de la oficina. Consulte [Configuración de las preferencias fuera de la oficina](todo-lists.md#setting-out-of-office-preferences).

**Colas:** Establezca preferencias para compartir la lista de tareas pendientes con otros usuarios o para solicitar acceso a la lista de otros usuarios. Consulte [Trabajo con tareas de grupos y colas compartidas](todo-lists.md#working-with-tasks-from-group-and-shared-queues).

**Configuración de la interfaz de usuario:** Defina las preferencias de cómo interactúa con el espacio de trabajo de AEM Forms. Consulte [Definir las preferencias de la interfaz de usuario](#set-user-interface-preferences).

### Definir las preferencias de la interfaz de usuario {#set-user-interface-preferences}

Establezca las preferencias de la interfaz de usuario en la pestaña Preferencias > Configuración de la interfaz de usuario . Estas son las preferencias disponibles.

* **Ubicación inicial:** Especifica la página que aparece al iniciar sesión en el espacio de trabajo de AEM Forms. Las cuatro opciones disponibles son Iniciar proceso, Tareas pendientes, Seguimiento y Favoritos.
* **Mensaje de cierre de sesión:** Especifica si se le pedirá que confirme que desea cerrar la sesión después de hacer clic en Cerrar sesión.
* **Formato de fecha:** Especifica el formato de visualización de fecha que se utiliza en todo el espacio de trabajo de AEM Forms.
* **Formato de hora**: Especifica el formato de visualización de tiempo utilizado en todo el espacio de trabajo de AEM Forms.
* **Notificar eventos de tarea por correo electrónico:** Especifica si recibe notificaciones por correo electrónico para eventos de tareas, incluidas asignaciones de tareas, recordatorios y fechas límite para tareas de la lista de tareas pendientes y de las listas de tareas pendientes de grupo a las que pertenece.
* **Adjuntar Forms en correo electrónico:** Especifica si una copia del formulario se adjunta a los mensajes de notificación por correo electrónico. Los archivos adjuntos solo son compatibles con los formularios PDF y XDP.
* **Guarde el borrador periódicamente:** Especifica si los borradores de formulario se guardan automáticamente de forma periódica o no. Para guardar los borradores periódicamente, habilite esta opción y establezca la duración del guardado automático de 1 a 30 minutos. Cuando el guardado automático está habilitado y un usuario está trabajando en un borrador, el borrador se guarda periódicamente después del número especificado de minutos. El borrador se guarda automáticamente únicamente cuando hay un cambio en el borrador desde la última vez que se guarda o se guarda automáticamente. Cuando se guarda el borrador, aparece un mensaje de alerta en la pantalla.
