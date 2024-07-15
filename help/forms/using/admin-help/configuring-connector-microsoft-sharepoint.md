---
title: Configurar el conector para Microsoft SharePoint
description: Configure el conector para Microsoft SharePoint AEM para habilitar la comunicación entre los formularios de y Microsoft SharePoint.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a8be58f1-1961-4bf5-aaad-feb4489fb389
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 7%

---

# Configurar el conector para Microsoft SharePoint {#configuring-connector-for-microsoft-sharepoint}

El conector para Microsoft SharePoint AEM permite la comunicación entre los formularios de y Microsoft SharePoint. Para obtener información adicional, consulte &quot;Conectores para ECM&quot; en [Referencia de servicios](https://www.adobe.com/go/learn_aemforms_services_63).

1. En la consola de administración, haga clic en Servicios > Conector para Microsoft SharePoint.
1. Especifique la siguiente configuración para el servidor de SharePoint:

   **Nombre de host de SharePoint Server:** El número de puerto del nombre de host de la aplicación web en el servidor de SharePoint, con el formato `[hostname]:'port'`.

   **Nombre de usuario:** Cuenta de usuario utilizada para conectarse al servidor de SharePoint.

   **Contraseña:** Contraseña de la cuenta de usuario utilizada para conectarse al servidor de SharePoint

   **Nombre de dominio:** Dominio donde se encuentra el servidor de SharePoint.

1. Haga clic en Guardar.

## Servicio de configuración de Microsoft SharePoint {#microsoft-sharepoint-configuration-service}

El servicio de configuración de Microsoft SharePoint AEM `(MSSharePointConfigService)` le permite especificar credenciales para el usuario de formularios en forma de que tiene permisos de suplantación. Para obtener información acerca de los permisos de suplantación, consulte [Configuración del conector para Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html). Siga estos pasos para especificar la configuración de `MSSharePointConfigService`:

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de servicios.
1. Navegue por la lista de servicios y haga clic en `MSSharePointConfigService`.
1. Especifique las siguientes opciones en la página Configuración:

   * Nombre De Usuario Para Un Usuario Con Permisos De Suplantación
   * Contraseña Del Usuario Anterior

1. Haga clic en Guardar.
