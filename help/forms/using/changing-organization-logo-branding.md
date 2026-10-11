---
title: Cambiar el logotipo de la organización para la promoción de la marca
description: Para personalizar la marca de AEM Forms Workspace, proporcione el logotipo de su organización al personalizar el logotipo predeterminado.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 49572f2a-f3ec-4ee6-98b8-2563de1cf96c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
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
source-wordcount: '142'
ht-degree: 78%
---
# Cambiar el logotipo de la organización para la promoción de la marca {#changing-the-organization-logo-for-branding}

El logotipo de la organización se muestra en la esquina superior izquierda de AEM Forms Workspace. Para actualizar el logotipo, siga los [Pasos genéricos de la personalización de AEM Forms Workspace](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization) y luego los siguientes pasos.

1. Cree un logotipo y asigne un nombre al archivo como `NewWorkspace.png`. Coloque el archivo de imagen en la carpeta /apps/ws/images mediante un cliente WebDAV.

   >[!NOTE]
   >
   >El tamaño recomendado para la imagen del logotipo es de 218 px × 20 px.

   >[!NOTE]
   >
   >Para obtener más información, consulte [Acceso a WebDAV](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=es).

   [Acceso de WebDAV](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=es)

1. Haga referencia a la nueva imagen del logotipo en la hoja de estilo en /apps/ws/css/newStyle.css al agregar el siguiente estilo.

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
