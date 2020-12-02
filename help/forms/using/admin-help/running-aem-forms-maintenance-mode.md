---
title: Ejecución de AEM formularios en modo de mantenimiento
seo-title: Ejecución de AEM formularios en modo de mantenimiento
description: El modo de mantenimiento resulta útil cuando se realizan tareas como la aplicación de parches en DSC, la actualización de formularios AEM o la aplicación de un Service Pack. Obtenga más información sobre la ejecución de AEM formularios en modo de mantenimiento.
seo-description: El modo de mantenimiento resulta útil cuando se realizan tareas como la aplicación de parches en DSC, la actualización de formularios AEM o la aplicación de un Service Pack. Obtenga más información sobre la ejecución de AEM formularios en modo de mantenimiento.
uuid: 9aa3be20-f17e-4384-b4ce-daaee2898c96
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 94047c12-ba3d-457a-954f-e035c7cc3ecd
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# Ejecución de AEM formularios en modo de mantenimiento {#running-aem-forms-in-maintenance-mode}

El modo de mantenimiento resulta útil cuando se realizan tareas como la aplicación de parches en DSC, la actualización de formularios AEM o la aplicación de un Service Pack.

Evite invocar procesos mientras el servidor está en modo de mantenimiento. Esto es lo que sucede si se invoca un proceso mientras el servidor está en modo de mantenimiento:

* Si el proceso es de larga duración, se agrega a la base de datos de trabajos, pero no se inicia. Al salir del modo de mantenimiento, AEM formularios procesa los trabajos de larga duración en su cola, incluso si el servidor se reinició en el modo de mantenimiento.
* Si el proceso es de corta duración, se procesa de inmediato.

**Poner AEM formularios en modo de mantenimiento**

1. En un navegador web, introduzca:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   En la ventana del explorador se muestra un mensaje &quot;ahora en pausa&quot;.

   >[!NOTE]
   >
   >Si apaga el servidor mientras está en modo de mantenimiento, seguirá en modo de mantenimiento cuando se reinicie. Debe desactivar el modo de mantenimiento cuando haya finalizado sus tareas de mantenimiento.

**Comprobar si AEM formularios se están ejecutando en modo de mantenimiento**

1. En un navegador web, introduzca:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   El estado se muestra en la ventana del explorador. El estado &quot;true&quot; indica que el servidor se está ejecutando en modo de mantenimiento y &quot;false&quot; indica que el servidor no está en modo de mantenimiento.

**Desactivar modo de mantenimiento**

1. En un navegador web, introduzca:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   Se muestra un mensaje &quot;ahora en ejecución&quot; en la ventana del explorador.

