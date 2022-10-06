---
title: Trabajo con tareas
seo-title: Working with tasks
description: Utilice la página Búsqueda de tareas para buscar tareas por nombre de usuario o ID de tarea. Obtenga más información sobre cómo trabajar con tareas.
seo-description: Use the Task Search page to search for tasks by user name or task ID. Learn more about working with tasks.
uuid: 630372d5-255f-4ea8-974d-d4f923108673
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9161c8ca-ef33-4ec9-affc-94b5b3e48a4c
exl-id: 375376d1-60b3-49a4-8893-ba9336e6bf7b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# Trabajo con tareas {#working-with-tasks}

Utilice la página Búsqueda de tareas para buscar tareas por nombre de usuario o ID de tarea. Los resultados de búsqueda se muestran en la página Lista de tareas, donde puede acceder al historial de una tarea. También puede reasignar una tarea si un usuario tiene demasiadas tareas o si un usuario ha recibido una asignación de tareas por error.

>[!NOTE]
>
>Al realizar búsquedas de tareas, no se devuelven resultados para nombres de usuario que empiecen por un signo de número (#). Si es posible, evite crear nombres de usuario que empiecen por un signo de número.

## Buscar tareas asociadas a un usuario {#search-for-tasks-associated-with-a-user}

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Búsqueda de tareas.
1. En Buscar por, seleccione Nombre de usuario. Si conoce parte del nombre de usuario que está buscando, escríbalo en el cuadro . Haga clic en Buscar usuario.
1. Aparecerá la página Buscar usuario. Puede restringir aún más la búsqueda, buscando por nombre de usuario o correo electrónico. Cuando encuentre el usuario que está buscando, seleccione el botón de opción junto al nombre y haga clic en Aceptar.
1. De forma predeterminada, la búsqueda de tareas busca las tareas que están asignadas actualmente al usuario. Para buscar también tareas que anteriormente estaban asignadas al usuario, seleccione Mostrar tarea sin asignar. Para buscar también tareas que el usuario haya completado, seleccione Mostrar tarea completada.
1. Haga clic en Buscar. Aparece la página Lista de tareas , que enumera el resultado de la búsqueda.

## Buscar una tarea al conocer su ID de tarea {#search-for-a-task-when-you-know-its-task-id}

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Búsqueda de tareas.
1. En Buscar por, seleccione ID de tarea y escriba el ID de la tarea en el cuadro.
1. Haga clic en Buscar. Aparece la página Lista de tareas , que enumera el resultado de la búsqueda.

## Trabajo con la lista de tareas {#working-with-the-task-list}

Los resultados de una búsqueda de tareas se muestran en la página Lista de tareas . Puede seleccionar una tarea para abrir la página Historial de tareas . Desde allí, puede asignar la tarea a otro usuario.

Las tareas se muestran con la siguiente información:

**ID de tarea:** El entero positivo que asigna el flujo de trabajo de formularios cuando se crea una instancia de la tarea (iniciada por un usuario). Puede utilizar este identificador para realizar un seguimiento de la tarea a lo largo de su ciclo de vida. Haga clic en un ID de tarea para ver detalles sobre el historial de tareas o para reasignar la tarea a otro usuario.

**Estado:** Asignada significa que la tarea está asignada actualmente al usuario. Sin asignar significa que la tarea se asignó anteriormente al usuario. El estado también se puede completar.

**Actividad:** Muestra el formulario y el nombre de una operación inicial o de la operación de proceso que generó la tarea.

**ID de proceso:** Este entero positivo que se asigna mediante el flujo de trabajo de formularios cuando se crea una instancia del proceso (es decir, cuando un usuario o un paso automatizado inician un proceso). Puede utilizar este identificador para rastrear la instancia de proceso a lo largo de su ciclo de vida.

**Nombre del proceso - Versión:** Nombre del proceso, tal como se define en Workbench.

**Aplicación:** Nombre de la aplicación a la que pertenece el proceso, tal como se define en Workbench.

**Fecha de creación:** Fecha y hora en que se creó la tarea.

## Visualización del historial de tareas y reasignación de tareas {#viewing-task-history-and-reassigning-tasks}

La página Historial de tareas muestra una lista de los usuarios y grupos que se han asignado a una tarea determinada.

Para cada asignación de tareas, la lista muestra la siguiente información:

**Nombre:** Nombre del usuario.

**Estado:** Asignada significa que la tarea está asignada actualmente al usuario. Sin asignar significa que la tarea se asignó anteriormente al usuario.

**ID de lista de trabajo:** Identificador numérico de la cola de usuario a la que pertenece la tarea. Un proceso se puede compartir entre varios usuarios.

**Tipo:** Indica cómo se asignó la tarea:

**Inicial:** Al usuario se le asignó originalmente la tarea.

**Adelante:** El propietario de la tarea original asignó la tarea a otro usuario.

**Rechazar:** Se rechazó una tarea reenviada o se devolvió una tarea a una lista de trabajo sin haber finalizado.

**Reclamación:** El usuario solicitó la tarea en una lista de trabajo compartida.

**Escalación:** Transcurrió un tiempo predeterminado (como se establece en la acción Usuario en Workbench) sin interacción del usuario y se asignó la tarea a otro usuario.

**Consulte:** El propietario de la tarea ha reenviado esta tarea a otro usuario para consulta que puede abrir el formulario, guardar datos, modificar los archivos adjuntos y las notas, pero no puede completar el paso. El usuario debe devolver la tarea al propietario de la tarea que consultó al usuario.

**Reasignación de administrador:** Un administrador reasignó la tarea.

**Fecha de asignación:** Fecha y hora en que se asignó la tarea al usuario.

### Asignación de un nuevo usuario a una tarea {#assigning-a-new-user-to-a-task}

La página Asignar usuario muestra una lista de los usuarios que pueden asignarse a una tarea. Para acceder a la página Asignar usuario, haga clic en Asignar nuevo usuario en la página Historial de tareas .

1. En el cuadro Buscar de la página Asignar usuario, escriba parte o la totalidad del nombre de usuario o la dirección de correo electrónico necesarios.
1. En Usar, seleccione Nombre o Dirección de correo electrónico y, a continuación, haga clic en Buscar. Se muestran los usuarios que coinciden con la búsqueda.
1. Seleccione el usuario de la lista y haga clic en Aceptar. La página Historial de Tareas aparece con la nueva asignación de usuario.
