---
title: Configurar el conector para Microsoft SharePoint
description: Configure el conector para Microsoft SharePoint para habilitar la comunicación entre los formularios de AEM y Microsoft SharePoint.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a8be58f1-1961-4bf5-aaad-feb4489fb389
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 9%
---

# Configurar el conector para Microsoft SharePoint

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

El conector para Microsoft SharePoint permite la comunicación entre los formularios de AEM y Microsoft SharePoint. Para obtener información adicional, consulte &quot;Conectores para ECM&quot; en [Referencia de servicios](https://www.adobe.com/go/learn_aemforms_services_63).

1. En la consola de administración, haga clic en Servicios > Conector para Microsoft SharePoint.
2. Especifique la siguiente configuración para el servidor de SharePoint:

   **Nombre de host de SharePoint Server:** El número de puerto del nombre de host de la aplicación web en el servidor de SharePoint, con el formato `[hostname]:'port'`.

   **Nombre de usuario:** Cuenta de usuario utilizada para conectarse al servidor de SharePoint.

   **Contraseña:** Contraseña de la cuenta de usuario utilizada para conectarse al servidor de SharePoint

   **Nombre de dominio:** Dominio donde se encuentra el servidor de SharePoint.

3. Haga clic en Guardar.

## Servicio de configuración de Microsoft SharePoint {#microsoft-sharepoint-configuration-service}

El servicio de configuración de Microsoft SharePoint `(MSSharePointConfigService)` le permite especificar credenciales para el usuario de formularios AEM que tiene permisos de suplantación. Para obtener información acerca de los permisos de suplantación, consulte [Configuración del conector para Microsoft SharePoint](https://help.adobe.com/es_ES/AEMForms/6.1/SharePointConfig/index.html). Siga estos pasos para especificar la configuración de `MSSharePointConfigService`:

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de servicios.
1. Navegue por la lista de servicios y haga clic en `MSSharePointConfigService`.
1. Especifique las siguientes opciones en la página Configuración:

   * Nombre De Usuario Para Un Usuario Con Permisos De Suplantación
   * Contraseña Del Usuario Anterior

1. Haga clic en Guardar.
