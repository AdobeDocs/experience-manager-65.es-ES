---
title: Cambiar el logotipo de la organización para la promoción de la marca
description: Para personalizar la marca de AEM Forms Workspace, proporcione el logotipo de su organización al personalizar el logotipo predeterminado.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 49572f2a-f3ec-4ee6-98b8-2563de1cf96c
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 100%

---

# Cambiar el logotipo de la organización para la promoción de la marca {#changing-the-organization-logo-for-branding}

El logotipo de la organización se muestra en la esquina superior izquierda de AEM Forms Workspace. Para actualizar el logotipo, siga los [Pasos genéricos de la personalización de AEM Forms Workspace](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization) y luego los siguientes pasos.

1. Cree un logotipo y asigne un nombre al archivo como `NewWorkspace.png`. Coloque el archivo de imagen en la carpeta /apps/ws/images mediante un cliente WebDAV.

   >[!NOTE]
   >
   >El tamaño recomendado para la imagen del logotipo es de 218 px × 20 px.

   >[!NOTE]
   >
   >Para obtener más información sobre el acceso a WebDAV, consulte [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=es).

1. Haga referencia a la nueva imagen del logotipo en la hoja de estilo en /apps/ws/css/newStyle.css al agregar el siguiente estilo.

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
