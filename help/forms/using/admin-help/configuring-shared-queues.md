---
title: Configuración de colas compartidas
seo-title: Configuración de colas compartidas
description: Las colas compartidas le permiten configurar y administrar las colas de usuarios de forma eficaz. Obtenga información sobre cómo configurar las colas compartidas.
seo-description: Las colas compartidas le permiten configurar y administrar las colas de usuarios de forma eficaz. Obtenga información sobre cómo configurar las colas compartidas.
uuid: 69ab611d-334b-40a5-bd2d-533d4cb25eda
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc403a60-b635-4334-9bf8-2f3d2036b2f3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuración de colas compartidas{#configuring-shared-queues}

Las colas compartidas le permiten configurar y administrar las colas de usuarios de forma eficaz. Una cola de usuario es simplemente todas las tareas asignadas a un usuario. Para obtener más información, consulte Listas [de tareas](https://help.adobe.com/en_US/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html) pendientes. Puede asignar, anular la asignación y reasignar colas de usuarios según sus necesidades organizativas. Puede administrar las colas compartidas de dos formas:

**Administrar El Acceso A Un Usuario**

Puede administrar el acceso a una cola de usuarios seleccionada mediante esta opción.

**Administrar El Acceso De Un Usuario**

Puede administrar las colas compartidas asignadas a un usuario seleccionado mediante esta opción.

## Administración del acceso a una cola de usuarios seleccionada {#managing-access-to-a-selected-user-queue}

La funcionalidad Administrar acceso a un usuario le permite administrar el acceso a una cola de usuarios seleccionada. Puede otorgar o revocar el acceso a una cola de usuarios seleccionada a otros usuarios de la organización. Por ejemplo, Kara Bowman está fuera del cargo. Con la funcionalidad Administrar acceso a un usuario, su cola se puede compartir con Akira Tanaka y John Jacobs para finalizarla. Más tarde, cuando Kara Bowman regresa a la oficina, puedes revocar el acceso a su fila de Akira Tanaka y John Jacobs.

Una vez compartidas, estas tareas las puede completar el usuario, con acceso a la cola, mediante Workspace.

>[!NOTE]
>
>Flex Workspace está en desuso para la versión de formularios AEM.

### Configuración del acceso a una cola de usuarios seleccionada {#configuring-access-to-a-selected-user-queue}

1. Inicie sesión en la consola de administración con una cuenta de administrador.
1. Seleccione **Servicios** > Flujo de **trabajo** de formularios > Cola **** compartida.

1. En la ficha Administrar acceso a un usuario, busque y seleccione el usuario cuya cola desee compartir. En cualquier momento, el panel inferior derecho muestra la lista de usuarios con acceso a la cola de usuarios seleccionada.
1. En el panel inferior izquierdo, busque y seleccione el usuario. Haga clic en Compartir.
1. Haga clic en Guardar para finalizar.

### Revocación del acceso a una cola de usuarios seleccionada {#revoking-access-to-a-selected-user-queue}

1. Inicie sesión en la consola de administración con una cuenta de administrador.
1. Seleccione **Servicios** > Flujo de **trabajo** de formularios > Cola **** compartida.

1. En la ficha Administrar acceso a un usuario, busque y seleccione el usuario cuya cola desee administrar.
1. El panel inferior derecho muestra la lista de usuarios con acceso a la cola de usuarios seleccionada. Seleccione el usuario y haga clic en Revocar.
1. Haga clic en Guardar para finalizar.

## Administración de colas asignadas a un usuario {#managing-queues-assigned-to-a-user}

La funcionalidad Administrar el acceso por un usuario le permite administrar las colas asignadas a un usuario seleccionado. Puede conceder o revocar el acceso a las colas de usuario a un usuario seleccionado individualmente. Por ejemplo, desea asignar colas de usuarios de Akira Tanaka y John Jacobs a Kara Bowman. Con la funcionalidad Administrar acceso por un usuario, puede buscar Kara Bowman y otorgar acceso a las tareas asignadas a Akira Tanaka y John Jacobs. Más adelante, puede revocar el acceso de Kara Bowman a estas colas de usuarios.

Una vez asignadas, el usuario puede completar estas tareas mediante Workspace.

>[!NOTE]
>
>Flex Workspace está en desuso para la versión de formularios AEM.

### Concesión de acceso a una cola de usuarios seleccionada {#granting-access-to-a-selected-user-queue}

1. Inicie sesión en la consola de administración con una cuenta de administrador.
1. Seleccione **Servicios** > Flujo de **trabajo** de formularios > Cola **** compartida.

1. En la ficha Administrar acceso a un usuario, busque y seleccione el usuario cuya cola desee compartir. En cualquier momento, el panel inferior derecho muestra la lista de usuarios con acceso a la cola de usuarios seleccionada.
1. En el panel inferior izquierdo, busque y seleccione las colas de usuario que desee compartir con el usuario seleccionado. Haga clic en Compartir.
1. Haga clic en Guardar para finalizar.

### Revocación del acceso a una cola de usuarios seleccionada {#revoking_access_to_a_selected_user_queue-1}

1. Inicie sesión en la consola de administración con una cuenta de administrador.
1. Seleccione **Servicios** > Flujo de **trabajo** de formularios > Cola **** compartida.

1. En la ficha Administrar acceso por un usuario, busque y seleccione el usuario cuya cola desee administrar.
1. El panel inferior derecho muestra la lista de colas de usuario asignadas al usuario seleccionado. Seleccione la cola de usuario y haga clic en Revocar.
1. Haga clic en Guardar para finalizar.

