---
title: Ejecución de formularios AEM en modo de mantenimiento
seo-title: Ejecución de formularios AEM en modo de mantenimiento
description: El modo de mantenimiento resulta útil cuando se realizan tareas como parches en DSC, actualización de formularios AEM o aplicación de un Service Pack. Obtenga más información sobre la ejecución de formularios AEM en modo de mantenimiento.
seo-description: El modo de mantenimiento resulta útil cuando se realizan tareas como parches en DSC, actualización de formularios AEM o aplicación de un Service Pack. Obtenga más información sobre la ejecución de formularios AEM en modo de mantenimiento.
uuid: 9aa3be20-f17e-4384-b4ce-daaee2898c96
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 94047c12-ba3d-457a-954f-e035c7cc3ecd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Ejecución de formularios AEM en modo de mantenimiento {#running-aem-forms-in-maintenance-mode}

El modo de mantenimiento resulta útil cuando se realizan tareas como parches en DSC, actualización de formularios AEM o aplicación de un Service Pack.

Evite invocar procesos mientras el servidor está en modo de mantenimiento. Esto es lo que sucede si se invoca un proceso mientras el servidor está en modo de mantenimiento:

* Si el proceso es de larga duración, se agrega a la base de datos de trabajos, pero no se inicia. Al salir del modo de mantenimiento, los formularios AEM procesan los trabajos de larga duración en su cola, incluso si el servidor se reinició en el modo de mantenimiento.
* Si el proceso es de corta duración, se procesa de inmediato.

**Poner los formularios AEM en modo de mantenimiento**

1. En un navegador web, introduzca:

   `https://`*[nombre ]*de host`:`*[puerto]* `/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=`*[administrador nombre de usuario ]*`&password=`*[contraseña]*

   En la ventana del explorador se muestra un mensaje &quot;ahora en pausa&quot;.

   >[!NOTE]
   >
   >Si apaga el servidor mientras está en modo de mantenimiento, seguirá en modo de mantenimiento cuando se reinicie. Debe desactivar el modo de mantenimiento cuando haya finalizado las tareas de mantenimiento.

**Compruebe si los formularios AEM se están ejecutando en modo de mantenimiento**

1. En un navegador web, introduzca:

   `https://`*[hostname]:[port ]*`/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=`*[admin nombre de usuario]* `&password=`*[contraseña ]*

   El estado se muestra en la ventana del explorador. El estado &quot;true&quot; indica que el servidor se está ejecutando en modo de mantenimiento y &quot;false&quot; indica que el servidor no está en modo de mantenimiento.

**Desactivar modo de mantenimiento**

1. En un navegador web, introduzca:

   `https://`*[hostname]:[port ]*`/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=`*[admin nombre de usuario]* `&password=`*[contraseña ]*

   Se muestra un mensaje &quot;ahora en ejecución&quot; en la ventana del explorador.

