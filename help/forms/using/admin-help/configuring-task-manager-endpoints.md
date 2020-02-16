---
title: Configuración de los extremos del Administrador de tareas
seo-title: Configuración de los extremos del Administrador de tareas
description: Obtenga información sobre cómo configurar los extremos del Administrador de tareas.
seo-description: Obtenga información sobre cómo configurar los extremos del Administrador de tareas.
uuid: 07604b10-0bd7-4bce-9624-7ebac4754f56
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9c55feb9-23d8-4798-a3c5-70ec736df3ad
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuración de los extremos del Administrador de tareas {#configuring-task-manager-endpoints}

Los extremos del Administrador de tareas permiten a los usuarios de Workspace invocar el servicio.

**Configuración del extremo del Administrador de tareas**

Utilice la siguiente configuración para configurar un extremo del Administrador de tareas.

**** Nombre: (Obligatorio) Identifica el extremo. El nombre se muestra en la vista de tarjeta en Workspace. No incluya un carácter &lt; porque truncará el nombre mostrado en Workspace. Si está introduciendo una dirección URL como nombre del extremo, asegúrese de que cumple las reglas de sintaxis especificadas en RFC1738.

**** Descripción: Descripción del extremo. No incluya un carácter &lt; porque truncará la descripción que se muestra en Workspace.

**** Instrucciones de tareas: Instrucciones para el usuario que inicia este flujo de trabajo.

**** Propietario del proceso: Nombre de la persona responsable del proceso.

**** El Usuario Puede Reenviar Tarea: Permite al usuario reenviar la tarea inicial.

**** Mostrar ventana de datos adjuntos: Permite al usuario ver la ventana de datos adjuntos.

**** Permitir adición de datos adjuntos: Permite al usuario agregar archivos adjuntos y notas.

**** Tarea bloqueada inicialmente: Bloquea la tarea inicial.

**** Agregar ACL para colas compartidas: La tarea inicial se crea con ACL para usuarios de cola compartida.

**** Categorización: (Obligatorio) Categoría en la que el usuario verá el formulario en Workspace. Seleccione una categoría de la lista o seleccione Nueva categoría para agregar una categoría.

**** Nombre de la operación: (Obligatorio) Una lista de operaciones que se pueden asignar al extremo.
