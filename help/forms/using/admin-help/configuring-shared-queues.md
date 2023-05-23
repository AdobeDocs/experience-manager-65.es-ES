---
title: Configurar colas compartidas
seo-title: Configuring Shared Queues
description: Las colas compartidas le permiten configurar y administrar las colas de usuario de forma eficaz. Obtenga información sobre cómo configurar colas compartidas.
seo-description: Shared Queues allow you to configure and manage user queues effectively. Learn how to configure shared queues.
uuid: 69ab611d-334b-40a5-bd2d-533d4cb25eda
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc403a60-b635-4334-9bf8-2f3d2036b2f3
exl-id: 5f4467c1-0f3f-4dc6-9bd5-98259f327295
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---

# Configurar colas compartidas{#configuring-shared-queues}

Las colas compartidas le permiten configurar y administrar las colas de usuario de forma eficaz. Una cola de usuario es simplemente todas las tareas asignadas a un usuario. Consulte [Listas de tareas pendientes](https://help.adobe.com/en_US/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html) para obtener más información. Puede asignar, anular la asignación y reasignar colas de usuario según sus necesidades organizativas. Puede administrar colas compartidas de dos formas:

**Administrar El Acceso A Un Usuario**

Puede administrar el acceso a una cola de usuario seleccionada mediante esta opción.

**Administrar El Acceso De Un Usuario**

Puede administrar las colas compartidas asignadas a un usuario seleccionado mediante esta opción.

## Administrar el acceso a una cola de usuarios seleccionada {#managing-access-to-a-selected-user-queue}

La funcionalidad Administrar el acceso a un usuario permite administrar el acceso a una cola de usuarios seleccionada. Puede conceder o revocar el acceso a una cola de usuario seleccionada a otros usuarios de su organización. Por ejemplo, Kara Bowman está fuera de la oficina. Con la funcionalidad Administrar el acceso a un usuario, su cola se puede compartir con Akira Tanaka y John Jacobs para su finalización. En un momento posterior, cuando Kara Bowman regrese a la oficina, puede revocar el acceso a su cola a Akira Tanaka y John Jacobs.

Una vez compartidas, el usuario puede completar estas tareas, con acceso a la cola, mediante Workspace.

>[!NOTE]
>
>Flex AEM Workspace está en desuso para la versión de formularios en la que se ha realizado un.

### Configurar el acceso a una cola de usuarios seleccionada {#configuring-access-to-a-selected-user-queue}

1. Inicie sesión en la consola de administración con una cuenta de administrador.
1. Seleccionar **Servicios** > **flujo de trabajo de formularios** > **Cola compartida**.

1. En la pestaña Administrar el acceso a un usuario, busque y seleccione el usuario cuya cola desee compartir. En cualquier momento, el panel inferior derecho muestra la lista de usuarios con acceso a la cola de usuarios seleccionada.
1. En el panel inferior izquierdo, busque y seleccione el usuario. Haga clic en Compartir.
1. Haga clic en Guardar para completar el proceso.

### Revocar acceso a una cola de usuario seleccionada {#revoking-access-to-a-selected-user-queue}

1. Inicie sesión en la consola de administración con una cuenta de administrador.
1. Seleccionar **Servicios** > **flujo de trabajo de formularios** > **Cola compartida**.

1. En la pestaña Administrar el acceso a un usuario, busque y seleccione el usuario cuya cola desea administrar.
1. El panel inferior derecho muestra la lista de usuarios con acceso a la cola de usuarios seleccionada. Seleccione el usuario y haga clic en Revocar.
1. Haga clic en Guardar para completar el proceso.

## Administrar colas asignadas a un usuario {#managing-queues-assigned-to-a-user}

La funcionalidad Administrar el acceso de un usuario permite administrar las colas asignadas a un usuario seleccionado. Puede conceder o revocar el acceso a las colas de usuario a un usuario seleccionado de forma individual. Por ejemplo, desea asignar las colas de usuario de Akira Tanaka y John Jacobs a Kara Bowman. Con la funcionalidad Administrar el acceso de un usuario, puede buscar Kara Bowman y conceder acceso a las tareas asignadas a Akira Tanaka y John Jacobs. En un momento posterior, puede revocar el acceso de Kara Bowman a estas colas de usuarios.

Una vez asignadas, el usuario puede completar estas tareas mediante Workspace.

>[!NOTE]
>
>Flex AEM Workspace está en desuso para la versión de formularios en la que se ha realizado un.

### Conceder acceso a una cola de usuario seleccionada {#granting-access-to-a-selected-user-queue}

1. Inicie sesión en la consola de administración con una cuenta de administrador.
1. Seleccionar **Servicios** > **flujo de trabajo de formularios** > **Cola compartida**.

1. En la pestaña Administrar el acceso a un usuario, busque y seleccione el usuario cuya cola desee compartir. En cualquier momento, el panel inferior derecho muestra la lista de usuarios con acceso a la cola de usuarios seleccionada.
1. En el panel inferior izquierdo, busque y seleccione las colas de usuario que desea compartir con el usuario seleccionado. Haga clic en Compartir.
1. Haga clic en Guardar para completar el proceso.

### Revocar acceso a una cola de usuario seleccionada {#revoking_access_to_a_selected_user_queue-1}

1. Inicie sesión en la consola de administración con una cuenta de administrador.
1. Seleccionar **Servicios** > **flujo de trabajo de formularios** > **Cola compartida**.

1. En la pestaña Administrar el acceso de un usuario, busque y seleccione el usuario cuya cola desea administrar.
1. El panel inferior derecho muestra la lista de colas de usuario asignadas al usuario seleccionado. Seleccione la cola del usuario y haga clic en Revocar.
1. Haga clic en Guardar para completar el proceso.
