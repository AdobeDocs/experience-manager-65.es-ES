---
title: Configuración del conector para Microsoft SharePoint
seo-title: Configuring Connector for Microsoft SharePoint
description: Configure Connector para Microsoft SharePoint para habilitar la comunicación entre AEM formularios y Microsoft SharePoint.
seo-description: Configure Connector for Microsoft SharePoint to enable communication between AEM forms and Microsoft SharePoint.
uuid: f1561b41-da20-4220-b13a-e78472a9449f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0ec881c9-8dcc-4847-9edf-24d9e6c4a7ea
exl-id: a8be58f1-1961-4bf5-aaad-feb4489fb389
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 1%

---

# Configuración del conector para Microsoft SharePoint {#configuring-connector-for-microsoft-sharepoint}

Connector for Microsoft SharePoint permite la comunicación entre AEM formularios y Microsoft SharePoint. Para obtener más información, consulte &quot;Conectores para ECM&quot; en [Referencia de servicios](https://www.adobe.com/go/learn_aemforms_services_63).

1. En la consola de administración, haga clic en Servicios > Conector para Microsoft SharePoint.
1. Especifique la siguiente configuración para el servidor de SharePoint:

   **Nombre de host del servidor de SharePoint:** El número de puerto del nombre de host de la aplicación web en el servidor SharePoint, con el formato `[hostname]:'port'`.

   **Nombre de usuario:** Cuenta de usuario utilizada para conectarse al servidor de SharePoint.

   **Contraseña:** Contraseña de la cuenta de usuario utilizada para conectarse al servidor de SharePoint

   **Nombre de dominio:** Dominio donde se encuentra el servidor de SharePoint.

1. Haga clic en Guardar.

## Servicio de configuración de Microsoft SharePoint {#microsoft-sharepoint-configuration-service}

El servicio de configuración de Microsoft SharePoint `(MSSharePointConfigService)` permite especificar credenciales para el usuario de formularios AEM que tiene permisos de suplantación. Para obtener información sobre los permisos de suplantación, consulte [Configuración del conector para Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html). Siga estos pasos para especificar la configuración de `MSSharePointConfigService`:

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de servicios.
1. Navegue por la lista de servicios y haga clic en `MSSharePointConfigService`.
1. Especifique la siguiente configuración en la página Configuración :

   * Nombre De Usuario De Un Usuario Con Permisos De Suplantación
   * Contraseña Del Usuario Anterior

1. Haga clic en Guardar.
