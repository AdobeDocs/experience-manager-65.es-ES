---
title: Uso de tareas
seo-title: Uso de tareas
description: Utilice la página Búsqueda de Tarea para buscar tareas por nombre de usuario o ID de tarea. Obtenga más información sobre cómo trabajar con tareas.
seo-description: Utilice la página Búsqueda de Tarea para buscar tareas por nombre de usuario o ID de tarea. Obtenga más información sobre cómo trabajar con tareas.
uuid: 630372d5-255f-4ea8-974d-d4f923108673
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9161c8ca-ef33-4ec9-affc-94b5b3e48a4c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---


# Uso de tareas {#working-with-tasks}

Utilice la página Búsqueda de Tarea para buscar tareas por nombre de usuario o ID de tarea. Los resultados de la búsqueda se muestran en la página de Lista de Tarea, donde puede acceder al historial de una tarea. También puede reasignar una tarea si un usuario tiene demasiadas tareas o si un usuario ha recibido una asignación de tarea por error.

>[!NOTE]
>
>Al realizar búsquedas de tarea no se obtienen resultados para los nombres de usuario que comienzan con un signo de número (#). Si es posible, evite crear nombres de usuario que comiencen con un signo de número.

## Buscar tareas asociadas con un usuario {#search-for-tasks-associated-with-a-user}

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Búsqueda de Tareas.
1. En Buscar por, seleccione Nombre de usuario. Si conoce parte del nombre de usuario que está buscando, escríbalo en el cuadro. Haga clic en Buscar usuario.
1. Aparece la página Buscar usuario. Puede restringir aún más la búsqueda, buscando por nombre de usuario o correo electrónico. Cuando encuentre el usuario que busca, seleccione el botón de radio junto al nombre y haga clic en Aceptar.
1. De forma predeterminada, la búsqueda de tareas busca tareas que están asignadas al usuario. Para buscar también tareas asignadas anteriormente al usuario, seleccione Mostrar Tarea sin asignar. Para buscar también tareas que el usuario ha completado, seleccione Mostrar Tarea completada.
1. Haga clic en Buscar. Aparece la página de Lista de Tarea, que enumera los resultados de la búsqueda.

## Buscar una tarea cuando conozca su ID de tarea {#search-for-a-task-when-you-know-its-task-id}

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Búsqueda de Tareas.
1. En Buscar por, seleccione ID de Tarea y escriba el ID de tarea en el cuadro.
1. Haga clic en Buscar. Aparece la página de Lista de Tarea, que enumera los resultados de la búsqueda.

## Uso de la lista de tarea {#working-with-the-task-list}

Los resultados de una búsqueda de tarea se muestran en la página de Lista de Tarea. Puede seleccionar una tarea para abrir la página Historial de Tareas. Desde allí, puede asignar la tarea a otro usuario.

Las tareas se muestran con la siguiente información:

**ID de tarea:** el entero positivo que asigna el flujo de trabajo de formularios cuando se crea una instancia de la tarea (iniciada por un usuario). Puede utilizar este identificador para rastrear la tarea a lo largo de su ciclo de vida. Haga clic en un ID de Tarea para obtener detalles de vista sobre el historial de tareas o para reasignar la tarea a otro usuario.

**Estado:** Asignado significa que la tarea está asignada al usuario. Sin asignar significa que la tarea se asignó previamente al usuario. También se puede completar el estado.

**Actividad:** muestra el formulario y el nombre de una operación inicial o de la operación de proceso que generó la tarea.

**Id. de proceso:** este entero positivo que se asigna por el flujo de trabajo de formularios cuando se crea una instancia del proceso (es decir, cuando un usuario o un paso automatizado inician un proceso). Puede utilizar este identificador para rastrear la instancia de proceso a lo largo de su ciclo de vida.

**Nombre del proceso: Versión:** el nombre del proceso, tal como se define en Workbench.

**Aplicación:** el nombre de la aplicación a la que pertenece el proceso, tal como se define en Workbench.

**Fecha de creación:** la fecha y hora en que se creó la tarea.

## Visualización del historial de tareas y reasignación de tareas {#viewing-task-history-and-reassigning-tasks}

La página Historial de Tareas muestra una lista de los usuarios y grupos asignados a una tarea en particular.

Para cada asignación de tarea, la lista muestra la siguiente información:

**Nombre:** El nombre del usuario.

**Estado:** Asignado significa que la tarea está asignada al usuario. Sin asignar significa que la tarea se asignó previamente al usuario.

**ID de lista de trabajo:** el identificador numérico de la cola de usuario a la que pertenece la tarea. Un proceso se puede compartir entre varios usuarios.

**Tipo:** indica cómo se asignó la tarea:

**Inicial:** Al usuario se le asignó originalmente la tarea.

**Reenvío:** El propietario de la tarea original asignó la tarea a otro usuario.

**Rechazar:** se rechazó una tarea reenviada o se devolvió una tarea a una lista de trabajo sin haber finalizado.

**Reclamación:** El usuario reclamó la tarea en una lista de trabajo compartida.

**Escalación:** tiempo transcurrido predeterminado (como se establece en la acción Usuario en Workbench) sin interacción del usuario y se asignó la tarea a otro usuario.

**Consultar:** El propietario de la tarea ha reenviado esta tarea a otro usuario para consulta, que puede abrir el formulario, guardar datos, modificar los anexos y las notas, pero no puede completar el paso. El usuario debe devolver la tarea al propietario de la tarea que haya consultado con el usuario.

**Reasignación de administración:** un administrador reasignó la tarea.

**Fecha de asignación:** la fecha y hora en que se asignó la tarea al usuario.

### Asignación de un nuevo usuario a una tarea {#assigning-a-new-user-to-a-task}

La página Asignar usuario lista a los usuarios que se pueden asignar a una tarea. Para acceder a la página Asignar usuario, haga clic en Asignar nuevo usuario en la página Historial de Tareas.

1. En el cuadro Buscar de la página Asignar usuario, escriba parte o la totalidad del nombre de usuario o la dirección de correo electrónico necesarios.
1. En Uso, seleccione Nombre o Dirección de correo electrónico y, a continuación, haga clic en Buscar. Se muestran los usuarios que coinciden con la búsqueda.
1. Seleccione el usuario en la lista y haga clic en Aceptar. La página Historial de Tareas aparece con la nueva asignación de usuario.

