---
title: Configuración del conector para Microsoft SharePoint
seo-title: Configuración del conector para Microsoft SharePoint
description: Configure Connector para Microsoft SharePoint para habilitar la comunicación entre formularios AEM y Microsoft SharePoint.
seo-description: Configure Connector para Microsoft SharePoint para habilitar la comunicación entre formularios AEM y Microsoft SharePoint.
uuid: f1561b41-da20-4220-b13a-e78472a9449f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0ec881c9-8dcc-4847-9edf-24d9e6c4a7ea
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Configuración del conector para Microsoft SharePoint {#configuring-connector-for-microsoft-sharepoint}

Connector for Microsoft SharePoint permite la comunicación entre formularios AEM y Microsoft SharePoint. Para obtener más información, consulte &quot;Conectores para ECM&quot; en [Referencia](https://www.adobe.com/go/learn_aemforms_services_63)de servicios.

1. En la consola de administración, haga clic en Servicios > Conector para Microsoft SharePoint.
1. Especifique la siguiente configuración para el servidor de SharePoint:

   **Nombre de host de SharePoint Server:** El número de puerto del nombre de host de la aplicación web en el servidor de SharePoint, en formato `[hostname]:'port'`.

   **Nombre de usuario:** Cuenta de usuario utilizada para conectarse al servidor de SharePoint.

   **Contraseña:** Contraseña de la cuenta de usuario utilizada para conectarse al servidor de SharePoint

   **Nombre de dominio:** Dominio donde se encuentra el servidor de SharePoint.

1. Haga clic en Guardar.

## Servicio de configuración de Microsoft SharePoint {#microsoft-sharepoint-configuration-service}

El servicio de configuración de Microsoft SharePoint `(MSSharePointConfigService)` permite especificar las credenciales del usuario de formularios AEM que tiene permisos de suplantación. Para obtener más información sobre los permisos de suplantación, consulte [Configuración del conector para Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html). Siga estos pasos para especificar la configuración de `MSSharePointConfigService`:

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de servicios.
1. Navegue por la lista de servicios y haga clic en `MSSharePointConfigService`.
1. Especifique la siguiente configuración en la página Configuración:

   * Nombre De Usuario Para Un Usuario Con Permisos De Suplantación
   * Contraseña Del Usuario Anterior

1. Haga clic en Guardar.

