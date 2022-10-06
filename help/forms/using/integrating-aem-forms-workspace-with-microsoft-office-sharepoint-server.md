---
title: Integración de AEM espacio de trabajo de formularios con Microsoft Office SharePoint Server
seo-title: Integrating AEM forms workspace with Microsoft Office SharePoint Server
description: Puede integrar AEM espacio de trabajo de formularios con Microsoft Office SharePoint Server.
seo-description: You can integrate AEM forms workspace with Microsoft Office SharePoint Server.
uuid: 69d51bdf-729f-4eea-8fae-1e2b8aacaae6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 8990b422-f4f6-4080-871a-33cdf7ca6455
docset: aem65
exl-id: d080932f-d5fb-482d-9329-62da5df10362
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# Integración de AEM espacio de trabajo de formularios con Microsoft Office SharePoint Server{#integrating-aem-forms-workspace-with-microsoft-office-sharepoint-server}

**- Requisitos**

**Conocimientos previos**
Para poder agregar AEM Forms Workspace al servidor de SharePoint, debe tener acceso al servidor de SharePoint con los privilegios correspondientes y conocer la URL para acceder a Workspace. Los pasos siguientes suponen que está familiarizado con SharePoint Server. Para obtener más información acerca de los elementos Web en el servidor de SharePoint, vea Elementos Web en los servicios de Windows SharePoint.

**Nivel de usuario**
Inicio

Puede utilizar AEM Forms Workspace como elemento Web en Microsoft Office SharePoint Server( Por ejemplo, Microsoft Office SharePoint Server 2007). Los usuarios pueden acceder a AEM Forms Workspace conectándose al servidor de SharePoint mediante un navegador web para proporcionar una experiencia unificada. En este artículo, aprenderá los pasos básicos para mostrar AEM Forms Workspace como elemento web en Microsoft Office SharePoint Server. Puede realizar los pasos descritos en este artículo para proporcionar una experiencia unificada de modo que los usuarios que se conecten al servidor de SharePoint puedan acceder a AEM Forms Workspace desde el mismo puerto.

>[!NOTE]
>
>Los pasos que se enumeran en este artículo son específicos de Microsoft SharePoint Server 2007. También puede configurar HTML Workspace con otras versiones compatibles de Microsoft SharePoint.

## Integración de AEM Forms Workspace con Microsoft Office SharePoint Server 2007 {#integrate-aem-forms-workspace-with-microsoft-office-sharepoint-server}

Siga los siguientes pasos para integrar AEM Forms Workspace en un elemento web:

1. En un explorador web, vaya al sitio de SharePoint como, por ejemplo, `https://[myMOSSserver]:44299/default.aspx` donde `[myMOSSserver]` es el nombre o la dirección IP del servidor de Sharepoint.

   >[!NOTE]
   >
   >44299 es el número de puerto predeterminado para el servidor SharePoint. El número de puerto depende de la instalación de SharePoint Server.

1. En la parte superior derecha de la página web, haga clic en **Acciones del sitio** y seleccione **Editar página**.
1. Haga clic en el **Agregar un elemento Web** botón.
1. En el cuadro de diálogo Agregar elementos Web - página Web, en Miscelánea, seleccione **Elemento web del visualizador de páginas** y haga clic en **Agregar**.
1. En el cuadro Elemento web del visualizador de páginas, haga clic en **editar** y seleccione **Modificar elemento web compartido**.

   >[!NOTE]
   >
   >El cuadro Elemento Web Visor de páginas aparece en la sección **Agregar un elemento Web** botón en el que ha hecho clic en el paso 3 como se muestra en la siguiente ilustración (Figura 1):

   ![Cuadro Elemento Web Visor de páginas en el servidor SharePoint de Microsoft Office.](assets/page-viewer-web-part-box-in-microsoft-office-sharepoint-server.png)

   Figura 1. - El cuadro Elemento Web Visor de páginas del servidor SharePoint de Microsoft Office.

1. En la página Visualizador de páginas, realice las siguientes tareas:

   1. En el cuadro Vínculo, escriba la dirección URL de AEM Forms Workspace, como `https://[AEM_forms_Server]:8080/lc/ws` donde `[AEM_forms_Server]` representa la IP o el nombre de AEM servidor de formularios.
   1. Haga clic en **Aspecto** y modifique la altura, la anchura y el título para que pueda ver la interfaz de usuario de Workspace completa. Por ejemplo, puede establecer la altura y la anchura en 6 pulgadas y 11 pulgadas, respectivamente.
   1. Haga clic en **Vínculo de prueba**. Aparece una nueva ventana del explorador web con Workspace.
   1. (Opcional) Haga clic en **Diseño** y modificar el diseño de Workspace en el elemento web.
   1. (Opcional) Haga clic en **Avanzadas** y modificar otras opciones de configuración, como la descripción y si Workspace se puede minimizar o cerrar en el elemento web.

      Haga clic en **Aplicar**.

1. Haga clic en **Salir del modo de edición** y compruebe que puede acceder a Workspace.

Después de completar los pasos anteriores, el sitio de SharePoint tiene un aspecto similar al de la siguiente ilustración (Figura 2):

![AEM Forms Workspace integrado con Microsoft Office SharePoint Server](assets/aem-forms-workspace.jpg)

Figura 2: AEM Forms Workspace integrado con Microsoft Office SharePoint Server
