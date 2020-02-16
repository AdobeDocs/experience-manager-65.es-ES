---
title: Configuración del Conector para IBM Content Manager
seo-title: Configuración del Conector para IBM Content Manager
description: Configure Connector for IBM Content Manager para habilitar la comunicación entre los formularios AEM y IBM Content Manager.
seo-description: Configure Connector for IBM Content Manager para habilitar la comunicación entre los formularios AEM y IBM Content Manager.
uuid: 3d55169d-93e3-4d4e-b18b-2a3394e1de3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3094b178-3b1a-46b3-8fbd-c20388afa3a7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuración del Conector para IBM Content Manager{#configuring-connector-for-ibm-content-manager}

Connector for IBM Content Manager permite la comunicación entre formularios AEM y IBM Content Manager. Para obtener más información, consulte &quot;Conectores para ECM&quot; en [Referencia](https://www.adobe.com/go/learn_aemforms_services_63)de servicios.

## Configurar la conexión de IBM Content Manager {#configure-the-ibm-content-manager-connection}

1. En la consola de administración, haga clic en Servicios > Conector para IBM Content Manager.
1. En el cuadro Nombre del almacén de datos, introduzca el nombre del almacén de datos de IBM Content Manager al que desea conectarse. Si la base de datos es local, introduzca el nombre de la base de datos. Si la base de datos es remota, introduzca su nombre de alias.
1. En el cuadro Nombre de usuario, introduzca el ID de usuario de un usuario que se conectará al almacén de datos de IBM Content Manager.
1. En el cuadro Contraseña, introduzca la contraseña del usuario.
1. (Opcional) En el cuadro Cadena de conexión de alias, introduzca argumentos de conexión adicionales. En la mayoría de los casos, esta casilla debe estar vacía. Para obtener más información, consulte la documentación de IBM.
1. Haga clic en Guardar.

## Validación de la configuración del servicio {#validation-of-service-settings}

Si introduce un alias dataStore, un nombre de usuario o una contraseña incorrectos, obtendrá los siguientes resultados, en función de si el conector del repositorio de contenido para IBM Content Manager se está ejecutando actualmente:

* Si se detiene el servicio, al guardar la información de configuración del servicio no aparece ningún error. Sin embargo, la próxima vez que inicie el servicio, se generará una excepción y el servicio no se iniciará.
* Si se inicia el servicio, al guardar la información de configuración del servicio, el servicio intenta validar la información de las credenciales inmediatamente. En este caso, se produce un error y la información de configuración no se guarda.

