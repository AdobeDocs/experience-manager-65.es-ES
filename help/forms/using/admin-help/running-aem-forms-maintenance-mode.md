---
title: Ejecutar AEM Forms en modo de mantenimiento
seo-title: Running AEM forms in maintenance mode
description: AEM El modo de mantenimiento es útil cuando se realizan tareas como aplicar parches a un DSC, actualizar formularios de la aplicación o aplicar un Service Pack. AEM Obtenga más información acerca de la ejecución de formularios en modo de mantenimiento.
seo-description: Maintenance mode is useful when performing tasks such as patching a DSC, upgrading AEM forms, or applying a service pack. Learn more about running AEM forms in maintenance mode.
uuid: 9aa3be20-f17e-4384-b4ce-daaee2898c96
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 94047c12-ba3d-457a-954f-e035c7cc3ecd
exl-id: 6f5ce18b-26b4-4c31-b48a-43ccbb3912f6
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 4%

---

# Ejecutar AEM Forms en modo de mantenimiento {#running-aem-forms-in-maintenance-mode}

AEM El modo de mantenimiento es útil cuando se realizan tareas como aplicar parches a un DSC, actualizar formularios de la aplicación o aplicar un Service Pack.

Evite invocar procesos mientras el servidor se encuentra en modo de mantenimiento. Esto es lo que sucede si se invoca un proceso mientras el servidor está en modo de mantenimiento:

* Si el proceso es de larga duración, se añade a la base de datos de trabajos, pero no se inicia. AEM Al salir del modo de mantenimiento, los formularios de la procesan los trabajos de larga duración en su cola, incluso si el servidor se reinició mientras estaba en modo de mantenimiento.
* Si el proceso es de corta duración, se procesa de inmediato.

**AEM Poner formularios en modo de mantenimiento**

1. En un explorador web, introduzca:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   Se muestra el mensaje &quot;ahora en pausa&quot; en la ventana del explorador.

   >[!NOTE]
   >
   >Si apaga el servidor mientras está en modo de mantenimiento, cuando se reinicia aún estará en modo de mantenimiento. Desactive el modo de mantenimiento cuando haya terminado sus tareas de mantenimiento.

**AEM Comprobar si el formulario de la se está ejecutando en modo de mantenimiento**

1. En un explorador web, introduzca:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   El estado se muestra en la ventana del explorador. El estado &quot;true&quot; indica que el servidor se está ejecutando en modo de mantenimiento y &quot;false&quot; indica que el servidor no está en modo de mantenimiento.

**Desactivar el modo de mantenimiento**

1. En un explorador web, introduzca:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   Se muestra el mensaje &quot;now running&quot; en la ventana del explorador.
