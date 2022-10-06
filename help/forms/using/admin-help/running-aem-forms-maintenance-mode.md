---
title: Ejecución de AEM formularios en modo de mantenimiento
seo-title: Running AEM forms in maintenance mode
description: El modo de mantenimiento es útil cuando se realizan tareas como parchear un DSC, actualizar AEM formularios o aplicar un Service Pack. Obtenga más información sobre la ejecución de AEM formularios en el modo de mantenimiento.
seo-description: Maintenance mode is useful when performing tasks such as patching a DSC, upgrading AEM forms, or applying a service pack. Learn more about running AEM forms in maintenance mode.
uuid: 9aa3be20-f17e-4384-b4ce-daaee2898c96
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 94047c12-ba3d-457a-954f-e035c7cc3ecd
exl-id: 6f5ce18b-26b4-4c31-b48a-43ccbb3912f6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# Ejecución de AEM formularios en modo de mantenimiento {#running-aem-forms-in-maintenance-mode}

El modo de mantenimiento es útil cuando se realizan tareas como parchear un DSC, actualizar AEM formularios o aplicar un Service Pack.

Evite invocar procesos mientras el servidor está en modo de mantenimiento. Esto es lo que sucede si se invoca un proceso mientras el servidor está en modo de mantenimiento:

* Si el proceso dura mucho tiempo, se agrega a la base de datos de trabajos, pero no se inicia. Al salir del modo de mantenimiento, AEM forms procesa los trabajos de larga duración en su cola, incluso si el servidor se reinició en el modo de mantenimiento.
* Si el proceso es de corta duración, se procesa de inmediato.

**Poner AEM formularios en modo de mantenimiento**

1. En un explorador web, introduzca:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   Se muestra un mensaje &quot;ahora en pausa&quot; en la ventana del explorador.

   >[!NOTE]
   >
   >Si apaga el servidor mientras está en modo de mantenimiento, seguirá en modo de mantenimiento cuando se reinicie. Debe desactivar el modo de mantenimiento cuando haya terminado sus tareas de mantenimiento.

**Comprobar si AEM formularios se están ejecutando en el modo de mantenimiento**

1. En un explorador web, introduzca:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   El estado se muestra en la ventana del explorador. El estado &quot;true&quot; indica que el servidor se está ejecutando en modo de mantenimiento y &quot;false&quot; indica que el servidor no está en modo de mantenimiento.

**Desactivar modo de mantenimiento**

1. En un explorador web, introduzca:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   Se muestra un mensaje &quot;ahora en ejecución&quot; en la ventana del explorador.
