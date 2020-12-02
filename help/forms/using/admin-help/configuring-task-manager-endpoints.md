---
title: Configuración de los extremos del Administrador de Tareas
seo-title: Configuración de los extremos del Administrador de Tareas
description: Obtenga información sobre cómo configurar los extremos del Administrador de Tareas.
seo-description: Obtenga información sobre cómo configurar los extremos del Administrador de Tareas.
uuid: 07604b10-0bd7-4bce-9624-7ebac4754f56
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9c55feb9-23d8-4798-a3c5-70ec736df3ad
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Configuración de los extremos del Administrador de Tareas {#configuring-task-manager-endpoints}

Los extremos del Administrador de tareas permiten a los usuarios de Workspace invocar el servicio.

**Configuración del extremo del Administrador de tareas**

Utilice los siguientes ajustes para configurar un extremo del Administrador de Tareas.

**Nombre:**  (obligatorio) Identifica el extremo. El nombre se muestra en la vista de la tarjeta en Workspace. No incluya un carácter &lt; porque truncará el nombre mostrado en Workspace. Si está introduciendo una dirección URL como nombre del extremo, asegúrese de que cumple las reglas de sintaxis especificadas en RFC1738.

**Descripción:** Descripción del extremo. No incluya un carácter &lt; porque truncará la descripción que se muestra en Workspace.

**Instrucciones de tarea:** Instrucciones para el usuario que inicio este flujo de trabajo.

**Propietario del proceso:** el nombre de la persona responsable del proceso.

**Tarea Puede reenviar:** permite al usuario reenviar la tarea inicial.

**Mostrar ventana de datos adjuntos:** permite al usuario ver la ventana de datos adjuntos.

**Permitir Añadir datos adjuntos:** permite al usuario agregar datos adjuntos y notas.

**Tarea bloqueada inicialmente:** bloquea la tarea inicial.

**Añadir ACL para colas compartidas:** la tarea inicial se crea con ACL para usuarios de colas compartidas.

**Categorización:**  (obligatoria) la categoría en la que el usuario verá el formulario en Workspace. Seleccione una categoría de la lista o seleccione Nueva Categoría para agregar una categoría.

**Nombre de la Operación:**  (obligatorio) lista de operaciones que se pueden asignar al extremo.
