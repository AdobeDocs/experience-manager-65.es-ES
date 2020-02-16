---
title: Integración del espacio de trabajo de formularios AEM con Microsoft Office SharePoint Server
seo-title: Integración del espacio de trabajo de formularios AEM con Microsoft Office SharePoint Server
description: 'Puede integrar el espacio de trabajo de formularios AEM con Microsoft Office SharePoint Server. '
seo-description: 'Puede integrar el espacio de trabajo de formularios AEM con Microsoft Office SharePoint Server. '
uuid: 69d51bdf-729f-4eea-8fae-1e2b8aacaae6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 8990b422-f4f6-4080-871a-33cdf7ca6455
docset: aem65
translation-type: tm+mt
source-git-commit: 21623c615ebe69226cfaf84baf4cfb1717b449f4

---


# Integración del espacio de trabajo de formularios AEM con Microsoft Office SharePoint Server{#integrating-aem-forms-workspace-with-microsoft-office-sharepoint-server}

**- Requisitos**

**Conocimientos** previos Para poder agregar AEM Forms Workspace a SharePoint Server, debe tener acceso a SharePoint Server con los privilegios correspondientes y conocer la dirección URL para acceder a Workspace. Los pasos a continuación suponen que usted conoce bien SharePoint Server. Para obtener más información sobre los elementos Web en SharePoint Server, consulte Elementos Web en Windows SharePoint Services.

**Nivel** de usuario Comienzo

Puede utilizar AEM Forms Workspace como elemento Web en Microsoft Office SharePoint Server (por ejemplo, Microsoft Office SharePoint Server 2007). Los usuarios pueden acceder a AEM Forms Workspace conectándose a su servidor de SharePoint mediante un navegador web para proporcionar una experiencia unificada. En este artículo, aprenderá los pasos básicos para mostrar AEM Forms Workspace como elemento web en Microsoft Office SharePoint Server. Puede realizar los pasos descritos en este artículo para proporcionar una experiencia unificada de modo que los usuarios que se conecten a su servidor de SharePoint puedan acceder a AEM Forms Workspace desde el mismo puerto.

>[!NOTE]
>
>Los pasos enumerados en este artículo son específicos de Microsoft SharePoint Server 2007. También puede configurar HTML Workspace con otras versiones compatibles de Microsoft SharePoint.

## Integración de AEM Forms Workspace con Microsoft Office SharePoint Server 2007 {#integrate-aem-forms-workspace-with-microsoft-office-sharepoint-server}

Siga estos pasos para integrar AEM Forms Workspace en un elemento web:

1. En un explorador Web, navegue al sitio de SharePoint como, por ejemplo, `https://[myMOSSserver]:44299/default.aspx` donde `[myMOSSserver]` es el nombre o la dirección IP del servidor de Sharepoint.

   >[!NOTE]
   >
   >44299 es el número de puerto predeterminado para el servidor de SharePoint. El número de puerto depende de la instalación de SharePoint Server.

1. En la parte superior derecha de la página web, haga clic en Acciones **** del sitio y seleccione **Editar página**.
1. Haga clic en el botón **Agregar un elemento** Web.
1. En el cuadro de diálogo Agregar elementos Web - página Web, en Miscelánea, seleccione Elemento **Web Visor de** páginas y, a continuación, haga clic en **Agregar**.
1. En el cuadro Elemento Web del visor de páginas, haga clic en **editar** y seleccione **Modificar elemento** Web compartido.

   >[!NOTE]
   >
   >El cuadro Elemento Web Visor de páginas aparece debajo del botón **Agregar un elemento** Web en el que hizo clic en el paso 3, como se muestra en la siguiente ilustración (Figura 1):

   ![Cuadro de elemento Web del visor de páginas en el servidor de Microsoft Office SharePoint.](assets/page-viewer-web-part-box-in-microsoft-office-sharepoint-server.png)

   Figura 1. - Cuadro Elemento Web del visor de páginas en el servidor de Microsoft Office SharePoint.

1. En la página Visor de páginas, realice las siguientes tareas:

   1. En el cuadro Vínculo, escriba la dirección URL de AEM Forms Workspace, como `https://[AEM_forms_Server]:8080/lc/ws` donde `[AEM_forms_Server]` representa la dirección IP o el nombre del servidor de formularios AEM.
   1. Haga clic en **Aspecto** y modifique la altura, la anchura y el título para que pueda ver toda la interfaz de usuario de Workspace. Por ejemplo, puede establecer la altura y la anchura en 6 pulgadas y 11 pulgadas, respectivamente.
   1. Haga clic en **Test Link**. Aparece una nueva ventana del navegador web con Workspace.
   1. (Opcional) Haga clic en **Diseño** y modifique el diseño de Espacio de trabajo en el elemento Web.
   1. (Opcional) Haga clic en **Avanzadas** y modifique otros ajustes, como la descripción y si Workspace puede minimizarse o cerrarse en el elemento Web.

      Haga clic en **Aplicar**.

1. Haga clic en **Salir del modo** de edición y compruebe que puede acceder a Workspace.

Después de completar los pasos anteriores, el sitio de SharePoint tiene un aspecto similar al de la siguiente ilustración (Figura 2):

![AEM Forms Workspace integrado con Microsoft Office SharePoint Server](assets/aem-forms-workspace.jpg)

Figura 2: Espacio de trabajo de AEM Forms integrado con Microsoft Office SharePoint Server

