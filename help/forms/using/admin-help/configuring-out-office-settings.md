---
title: Configuración de fuera de la oficina
seo-title: Configuración de fuera de la oficina
description: La función Fuera de la oficina permite especificar cuándo un usuario dejará de trabajar y no podrá completar las tareas asignadas por los formularios AEM.
seo-description: La función Fuera de la oficina permite especificar cuándo un usuario dejará de trabajar y no podrá completar las tareas asignadas por los formularios AEM.
uuid: 0d01df0a-aa6a-40e5-bf24-423ed1c932cc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 30312159-58a5-4781-b554-29dcbce696cb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuración de fuera de la oficina {#configuring-out-of-office-settings}

La función Fuera de la oficina permite a los usuarios o administradores especificar cuándo un usuario estará fuera de la oficina y no podrá completar las tareas asignadas por los formularios AEM. Mientras un usuario está establecido en Fuera de la oficina, sus tareas se asignan a uno o más usuarios designados. Los usuarios pueden cambiar la configuración fuera de la oficina en Workspace o los administradores pueden cambiar la configuración en nombre de un usuario en el flujo de trabajo de formularios.

Al crear un proceso, el usuario de Workbench puede especificar si una tarea puede redirigirse debido a la configuración de fuera de Office.

## Visualización de la información fuera de la oficina de un usuario {#view-a-user-s-out-of-office-information}

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Fuera de Office.
1. En el cuadro situado cerca de la parte superior de la página Fuera de la oficina, puede realizar una de las siguientes acciones:

   **Buscar por nombre**

   Seleccione la opción Buscar por nombre. Escriba todo o parte del nombre de usuario y haga clic en Buscar. Si deja el campo en blanco, el flujo de trabajo de Forms devuelve una lista de todos los usuarios

   **Buscar por intervalo de fechas**

   Seleccione la opción Buscar por intervalo de fechas. Especifique las fechas de origen y de destino junto con las marcas de hora deseadas para reducir el resultado de la búsqueda. Haga clic en Buscar.

1. Haga clic en un nombre de usuario para mostrar la información fuera de la oficina del usuario debajo de la lista de usuarios.

## Cambiar el estado de un usuario fuera de la oficina {#change-a-user-s-out-of-office-status}

1. Busque al usuario, tal como se describe en [Ver la información](configuring-out-office-settings.md#view-a-user-s-out-of-office-information)de un usuario fuera de la oficina.
1. Haga clic en el nombre del usuario que desee cambiar.
1. En la lista *Nombre* de usuario que hay actualmente, seleccione En la oficina o Fuera de la oficina.
1. Haga clic en Guardar.

## Agregar un intervalo de fechas fuera de la oficina para un usuario {#add-an-out-of-office-date-range-for-a-user}

1. Busque al usuario, tal como se describe en [Ver la información](configuring-out-office-settings.md#view-a-user-s-out-of-office-information)de un usuario fuera de la oficina.
1. Haga clic en el nombre del usuario que desee cambiar.
1. Haga clic en Agregar intervalo de fechas.
1. Introduzca una hora de inicio y una hora de finalización. Puede hacer clic en el icono Calendario para seleccionar una fecha. Si no especifica una hora de finalización, el usuario se configurará como fuera de la oficina indefinidamente.
1. Haga clic en Guardar.

## Asignar un usuario para tareas fuera de la oficina {#assign-a-user-for-out-of-office-tasks}

Mientras un usuario no está en la oficina, puede asignar uno o más usuarios para realizar cualquier tarea nueva para el usuario. Puede configurar las siguientes configuraciones:

* Asigne todas las tareas nuevas a un usuario predeterminado designado.
* No reasigne ninguna tarea. Las nuevas tareas permanecen asignadas al usuario que no está en la oficina.
* Asigne un usuario predeterminado que recibirá la mayoría de las tareas del usuario, pero especifique que las tareas de determinados procesos se reasignarán a otros usuarios o se seguirán asignando al usuario que no esté en la oficina.
* No asigne un usuario predeterminado, sino que asigne determinadas tareas de determinados procesos a usuarios específicos.

   1. Busque al usuario, tal como se describe en [Ver la información](configuring-out-office-settings.md#view-a-user-s-out-of-office-information)de un usuario fuera de la oficina.
   1. Haga clic en el nombre del usuario que desee cambiar.
   1. En la lista Usuario predeterminado para tareas fuera de la oficina, seleccione un usuario de la lista. Si no desea designar un usuario predeterminado para que reciba los elementos reasignados, seleccione No asignar.

      Si el nombre de usuario adecuado no aparece en la lista, haga clic en Buscar usuario y utilice el cuadro de diálogo Buscar usuario para buscar al usuario. Seleccione el usuario apropiado en la lista y haga clic en Seleccionar usuario. También puede hacer clic en Ver programación del usuario en el cuadro de diálogo Buscar usuario para ver la programación de usuarios seleccionados que no están en la oficina.

   1. Si hay procesos que no deben enviarse al usuario predeterminado, haga clic en Agregar una excepción y seleccione el proceso y otro usuario de la lista. También puede seleccionar No asignar para que la tarea permanezca asignada al usuario que no está en la oficina.
   1. Haga clic en Guardar.

