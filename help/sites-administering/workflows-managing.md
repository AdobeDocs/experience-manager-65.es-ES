---
title: Administración del acceso a los flujos de trabajo
seo-title: Managing Access to Workflows
description: Obtenga información sobre cómo administrar el acceso a los flujos de trabajo.
seo-description: Learn how to manage access to Workflows.
uuid: 58f79b89-fe56-4565-a869-8179c1ac68de
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5150867a-02a9-45c9-b2fd-e536b60ffa8c
exl-id: cc54d637-d66c-49d2-99ee-00d96f1a74e0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 4%

---

# Administración del acceso a los flujos de trabajo{#managing-access-to-workflows}

Configure las ACL según las cuentas de usuario para permitir (o deshabilitar) el inicio y la participación en flujos de trabajo.

## Permisos de usuario necesarios para flujos de trabajo {#required-user-permissions-for-workflows}

Se pueden realizar acciones sobre flujos de trabajo si:

* está trabajando con el `admin` account
* la cuenta se ha asignado al grupo predeterminado `workflow-users`:

   * este grupo tiene todos los privilegios necesarios para que los usuarios realicen acciones de flujo de trabajo.
   * cuando la cuenta está en este grupo, solo tiene acceso a los flujos de trabajo que ha iniciado.

* la cuenta se ha asignado al grupo predeterminado `workflow-administrators`:

   * este grupo tiene todos los privilegios necesarios para que los usuarios con privilegios monitoricen y administren los flujos de trabajo.
   * cuando la cuenta está en este grupo, tiene acceso a todos los flujos de trabajo.

>[!NOTE]
>
>Estos son los requisitos mínimos. Su cuenta también debe ser el participante asignado o un miembro del grupo asignado para realizar pasos específicos.

## Configuración del acceso a los flujos de trabajo {#configuring-access-to-workflows}

Los modelos de flujo de trabajo heredan una lista de control de acceso (ACL) predeterminada para controlar cómo los usuarios pueden interactuar con los flujos de trabajo. Para personalizar el acceso de los usuarios para un flujo de trabajo, modifique la Lista de control de acceso (ACL) en el repositorio para la carpeta que contiene el nodo del modelo de flujo de trabajo:

* [Aplicar una ACL para el modelo de flujo de trabajo específico a /var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)
* [Cree una subcarpeta en /var/workflow/models y aplique la ACL a esa](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that)

>[!NOTE]
>
>Para obtener información sobre el uso de CRXDE Lite para configurar ACL, consulte [Gestión de derechos de acceso](/help/sites-administering/user-group-ac-admin.md#access-right-management).

### Aplicar una ACL para el modelo de flujo de trabajo específico a /var/workflow/models {#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models}

Si el modelo de flujo de trabajo se almacena dentro de `/var/workflow/models` a continuación, puede asignar una ACL específica, relevante solo para ese flujo de trabajo, en la carpeta :

1. Abra el CRXDE Lite en el explorador web (por ejemplo, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. En el árbol de nodos, seleccione el nodo de la carpeta de modelos de flujo de trabajo:

   `/var/workflow/models`

1. Haga clic en el **Control de acceso** pestaña .
1. En el **Políticas de control de acceso local** (**Lista de control de acceso**), haga clic en el icono de signo más para **Agregar entrada**.
1. En el **Agregar nueva entrada** agregue un nuevo ACE con las siguientes propiedades:

   * **Principal**: `content-authors`
   * **Tipo**: `Deny`
   * **Privilegios**: `jcr:read`
   * **rep:glob**: referencia al flujo de trabajo específico

   ![wf-108](assets/wf-108.png)

   La variable **Lista de control de acceso** La tabla ahora incluye la restricción para `content-authors` en el `prototype-wfm-01` modelo de flujo de trabajo.

   ![wf-109](assets/wf-109.png)

1. Haga clic en **Guardar todo**.

   La variable `prototype-wfm-01` el flujo de trabajo ya no está disponible para los miembros del `content-authors` grupo.

### Cree una subcarpeta en /var/workflow/models y aplique la ACL a esa {#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that}

Su [el equipo de desarrollo puede crear los flujos de trabajo en una subcarpeta](/help/sites-developing/workflows-models.md#creating-a-new-workflow) de

`/var/workflow/models`

Comparable a los flujos de trabajo de DAM almacenados en

`/var/workflow/models/dam/`

A continuación, puede agregar una ACL a la propia carpeta.

1. Abra el CRXDE Lite en el explorador web (por ejemplo, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. En el árbol de nodos, seleccione el nodo de la carpeta individual en la carpeta de modelos de flujo de trabajo; por ejemplo:

   `/var/workflow/models/prototypes`

1. Haga clic en el **Control de acceso** pestaña .
1. En el **Política de control de acceso aplicable** , haga clic en el icono de signo más para **Agregar** una entrada.
1. En el **Políticas de control de acceso local** (**Lista de control de acceso**), haga clic en el icono de signo más para **Agregar entrada**.
1. En el **Agregar nueva entrada** agregue un nuevo ACE con las siguientes propiedades:

   * **Principal**: `content-authors`
   * **Tipo**: `Deny`
   * **Privilegios**: `jcr:read`

   >[!NOTE]
   >
   >Como con [Aplicar una ACL para el modelo de flujo de trabajo específico a /var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models) puede incluir un rep:glob para limitar el acceso a un flujo de trabajo específico.

   ![wf-110](assets/wf-110.png)

   La variable **Lista de control de acceso** La tabla ahora incluye la restricción para `content-authors` en el `prototypes` carpeta.

   ![wf-111](assets/wf-111.png)

1. Haga clic en **Guardar todo**.

   Los modelos de `prototypes` ya no están disponibles para los miembros de `content-authors` grupo.
