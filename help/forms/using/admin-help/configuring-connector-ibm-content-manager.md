---
title: Configuración del conector para IBM Content Manager
seo-title: Configuring Connector for IBM Content Manager
description: Configure el conector para IBM Content Manager para permitir la comunicación entre AEM formularios y IBM Content Manager.
seo-description: Configure the Connector for IBM Content Manager to enable communication between AEM forms and IBM Content Manager.
uuid: 3d55169d-93e3-4d4e-b18b-2a3394e1de3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3094b178-3b1a-46b3-8fbd-c20388afa3a7
exl-id: 50f0c963-8007-4e2a-aa73-d99b97d9a1aa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Configuración del conector para IBM Content Manager{#configuring-connector-for-ibm-content-manager}

El conector para IBM Content Manager permite la comunicación entre AEM formularios y IBM Content Manager. Para obtener más información, consulte &quot;Conectores para ECM&quot; en [Referencia de servicios](https://www.adobe.com/go/learn_aemforms_services_63).

## Configuración de la conexión de IBM Content Manager {#configure-the-ibm-content-manager-connection}

1. En la consola de administración, haga clic en Servicios > Conector para IBM Content Manager.
1. En el cuadro Nombre del almacén de datos, introduzca el nombre del almacén de datos de IBM Content Manager al que desea conectarse. Si la base de datos es local, introduzca el nombre de la base de datos. Si la base de datos es remota, introduzca su nombre de alias.
1. En el cuadro Nombre de usuario, introduzca el ID de usuario de un usuario que se conectará al almacén de datos del Administrador de contenido de IBM.
1. En el cuadro Contraseña, introduzca la contraseña del usuario.
1. (Opcional) En el cuadro Cadena de conexión de alias, introduzca argumentos de conexión adicionales. En la mayoría de los casos, esta casilla debe estar vacía. Para obtener más información, consulte la documentación de IBM .
1. Haga clic en Guardar.

## Validación de la configuración del servicio {#validation-of-service-settings}

Si introduce un alias dataStore, un nombre de usuario o una contraseña incorrectos, obtendrá los siguientes resultados, en función de si el conector del repositorio de contenido para el servicio Administrador de contenido de IBM se está ejecutando actualmente:

* Si se detiene el servicio, al guardar la información de configuración del servicio no aparece ningún error. Sin embargo, la próxima vez que inicie el servicio, se generará una excepción y el servicio no se iniciará.
* Si se inicia el servicio, al guardar la información de configuración del servicio, el servicio intenta validar la información de las credenciales inmediatamente. En este caso, se produce un error y la información de configuración no se guarda.
