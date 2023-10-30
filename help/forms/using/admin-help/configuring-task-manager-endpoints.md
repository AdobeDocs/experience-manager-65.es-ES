---
title: Configurar los extremos del Administrador de tareas
description: Obtenga información sobre cómo configurar los extremos del Administrador de tareas para invocar el servicio. Se requieren diferentes configuraciones para configurar los extremos del Administrador de tareas.
uuid: 07604b10-0bd7-4bce-9624-7ebac4754f56
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9c55feb9-23d8-4798-a3c5-70ec736df3ad
exl-id: 8495a3d7-6ac9-41f5-b1f9-31decaba118a
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 3%

---

# Configurar los extremos del Administrador de tareas {#configuring-task-manager-endpoints}

Los extremos del Administrador de tareas permiten a los usuarios de Workspace invocar el servicio.

**Configuración de extremo del Administrador de tareas**

Use la siguiente configuración para configurar un extremo del Administrador de tareas.

**Nombre:** (Obligatorio) Identifica el punto final. El nombre se muestra en la vista de tarjeta del Espacio de trabajo. No incluya un carácter &lt; porque truncará el nombre mostrado en Workspace. Si introduce una dirección URL como nombre del extremo, asegúrese de que se ajuste a las reglas de sintaxis especificadas en RFC1738.

**Descripción:** Una descripción del extremo. No incluya un carácter &lt; porque truncará la descripción mostrada en Workspace.

**Instrucciones de tarea:** Instrucciones para el usuario que inicia este flujo de trabajo.

**Propietario del proceso:** El nombre de la persona responsable del proceso.

**El usuario puede reenviar la tarea:** Permite al usuario reenviar la tarea inicial.

**Mostrar ventana de datos adjuntos:** Permite al usuario ver la ventana de datos adjuntos.

**Permitir adición de datos adjuntos:** Permite al usuario agregar archivos adjuntos y notas.

**Tarea Bloqueada Inicialmente:** Bloquea la tarea inicial.

**Agregar ACL para colas compartidas:** La tarea inicial se crea con ACL para los usuarios de la cola compartida.

**Categorización:** (Obligatorio) Categoría en la que el usuario verá el formulario en Workspace. Seleccione una categoría de la lista o seleccione Nueva categoría para añadir una categoría.

**Nombre de operación:** (Obligatorio) Una lista de operaciones que se pueden asignar al extremo.
