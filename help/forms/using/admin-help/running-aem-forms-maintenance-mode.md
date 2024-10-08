---
title: Ejecutar AEM Forms en modo de mantenimiento
description: AEM El modo de mantenimiento es útil cuando se realizan tareas como aplicar parches a un DSC, actualizar formularios de la aplicación o aplicar un Service Pack. AEM Obtenga más información acerca de la ejecución de formularios en modo de mantenimiento.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6f5ce18b-26b4-4c31-b48a-43ccbb3912f6
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 4%

---

# Ejecutar AEM Forms en modo de mantenimiento {#running-aem-forms-in-maintenance-mode}

AEM El modo de mantenimiento es útil cuando se realizan tareas como aplicar parches a un DSC, actualizar formularios de la aplicación o aplicar un Service Pack.

Evite invocar procesos mientras el servidor se encuentra en modo de mantenimiento. Esto es lo que sucede si se invoca un proceso mientras el servidor está en modo de mantenimiento:

* Si el proceso es de larga duración, se añade a la base de datos de trabajos, pero no se inicia. AEM Al salir del modo de mantenimiento, los formularios de la procesan los trabajos de larga duración en su cola, incluso si el servidor se reinició mientras estaba en modo de mantenimiento.
* Si el proceso es de corta duración, se procesa de inmediato.

AEM **Poner formularios en modo de mantenimiento**

1. En un explorador web, introduzca:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   Se muestra el mensaje &quot;ahora en pausa&quot; en la ventana del explorador.

   >[!NOTE]
   >
   >Si apaga el servidor mientras está en modo de mantenimiento, cuando se reinicia aún estará en modo de mantenimiento. Desactive el modo de mantenimiento cuando haya terminado sus tareas de mantenimiento.

AEM **Compruebe si formularios en la que se está ejecutando el servicio de mantenimiento**

1. En un explorador web, introduzca:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   El estado se muestra en la ventana del explorador. El estado &quot;true&quot; indica que el servidor se está ejecutando en modo de mantenimiento y &quot;false&quot; indica que el servidor no está en modo de mantenimiento.

**Desactivar el modo de mantenimiento**

1. En un explorador web, introduzca:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   Se muestra el mensaje &quot;now running&quot; en la ventana del explorador.
