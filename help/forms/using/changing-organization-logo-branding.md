---
title: Cambio del logotipo de la organización para la marca
seo-title: Cambio del logotipo de la organización para la marca
description: Para personalizar el espacio de trabajo de marca de AEM Forms, proporcione el logotipo de su organización personalizando el logotipo predeterminado.
seo-description: Para personalizar el espacio de trabajo de marca de AEM Forms, proporcione el logotipo de su organización personalizando el logotipo predeterminado.
uuid: f0c340ee-2e54-4bb0-9c30-383cc1bbadb8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2c651302-f4ef-4211-b897-f5942ed0ffb1
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# Cambio del logotipo de organización para la marca {#changing-the-organization-logo-for-branding}

El logotipo de la organización se muestra en la esquina superior izquierda del espacio de trabajo de AEM Forms. Para actualizar el logotipo, siga los [pasos genéricos de personalización del espacio de trabajo de AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization) y, a continuación, siga los pasos siguientes.

1. Cree un logotipo y asigne un nombre al archivo como `NewWorkspace.png`. Coloque el archivo de imagen en la carpeta /apps/ws/images mediante un cliente WebDAV.

   >[!NOTE]
   >
   >El tamaño recomendado para la imagen del logotipo es de 218 px × 20 px.

   >[!NOTE]
   >
   >Para obtener más información sobre el acceso a WebDAV, consulte [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

1. Haga referencia a la nueva imagen del logotipo en la hoja de estilo en /apps/ws/css/newStyle.css añadiendo el siguiente estilo.

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
