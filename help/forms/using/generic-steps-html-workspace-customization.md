---
title: Pasos genéricos para la personalización de AEM Forms Workspace
seo-title: Generic steps for AEM Forms workspace customization
description: Introducción a la personalización de la interfaz de usuario de AEM Forms Workspace.
seo-description: How to get started customizing AEM Forms workspace user interface.
uuid: da6310b4-1c58-468d-85c6-975fd2c141f9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: dd3218c4-2bb2-40fc-9141-5823b0ea4224
docset: aem65
exl-id: 45e50b47-1b36-4937-9e1a-cc7bfb953861
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '300'
ht-degree: 100%

---

# Pasos genéricos para la personalización de AEM Forms Workspace {#generic-steps-for-aem-forms-workspace-customization}

Los pasos genéricos para realizar cualquier personalización son:

1. Inicie sesión en CRXDE Lite accediendo a `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Cree una carpeta `sling:Folder` denominada `ws` en `/apps`, en el caso de que no exista. Para crear una carpeta `sling:Folder`, haga clic con el botón derecho en la carpeta `apps` y seleccione **[!UICONTROL Crear]** > **[!UICONTROL Crear nodo]**. Especifique como nombre `ws`, seleccione el tipo `sling:Folder` y haga clic en **[!UICONTROL Aceptar]**. Haga clic en **[!UICONTROL Guardar todo]**.
1. Vaya a `/apps/ws` y desplácese hasta la pestaña **[!UICONTROL Control de acceso]**.
1. Seleccione la opción **[!UICONTROL Repositorio]**. En la lista **[!UICONTROL Control de acceso]**, haga clic en **[!UICONTROL +]** para agregar una nueva entrada. Vuelva a hacer clic en **[!UICONTROL +]**.
1. Busque y seleccione el principal **PERM_WORKSPACE_USER**.

   ![Seleccione el principal PERM_WORKSPACE_USER como parte de los pasos genéricos para personalizar HTML Workspace](assets/perm_workspace_user.png).

1. Otorgue el privilegio `jcr:read` al principal.
1. Haga clic en **[!UICONTROL Guardar todo]**.
1. Copie los archivos `GET.jsp`, `index` y `html.jsp` de la carpeta `/libs/ws` a la carpeta `/apps/ws`.
1. Copie la carpeta `/libs/ws/locales` en la carpeta `/apps/ws`. Haga clic en **[!UICONTROL Guardar todo]**.
1. Actualice las referencias y las rutas relativas del archivo `GET.jsp`, como se muestra a continuación, y haga clic en **[!UICONTROL Guardar todo]**.

   ```javascript
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. Siga los siguientes pasos para llevar a cabo las personalizaciones de CSS:

   1. Vaya a la carpeta `/apps/ws` y cree una nueva carpeta con el nombre `css`.

   1. En la carpeta `css`, cree un nuevo archivo con el nombre `newStyle.css`.

   1. Abra `/apps/ws/html`.jsp y cambie

   ```javascript
   <link lang="en" rel="stylesheet" type="text/css" href="css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/jquery-ui.css"/>
   ```

   a

   ```javascript
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/newStyle.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/jquery-ui.css"/>
   ```

   >[!NOTE]
   >
   >Coloque la entrada del archivo CSS definido por el usuario después de la entrada de style.css, como se muestra arriba.

1. En el archivo /apps/ws/html.jsp, cambie

   ```jsp
   <script data-main="js/main" src="js/libs/require/require.js"></script>
   ```

   a

   ```jsp
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. Haga lo siguiente:

   1. Cree una carpeta con el nombre `js` en `/apps/ws`. Haga clic en **[!UICONTROL Guardar todo]**.

   1. Cree una carpeta con el nombre `libs` en `/apps/ws/js`. Haga clic en **[!UICONTROL Guardar todo]**.

   1. Copie la carpeta `/libs/ws/js/libs/jqueryui` a `/apps/ws/js/libs`. Haga clic en **[!UICONTROL Guardar todo]**.

1. Siga los siguientes pasos para llevar a cabo las personalizaciones de HTML:

   1. Cree una carpeta con el nombre `runtime` en `/apps/ws/js`. Haga clic en **[!UICONTROL Guardar todo]**.

   1. Cree una carpeta con el nombre `templates` en `/apps/ws/js/runtime`. Haga clic en **[!UICONTROL Guardar todo]**.

   1. Copie `/libs/ws/js/main.js` en `/apps/ws/js/main.js`.

   1. Copie /libs/ws/js/registry.js en `/apps/ws/js/registry.js`.

1. Haga clic en **[!UICONTROL Guardar todo]**, borre la caché y actualice AEM Forms Workspace.

   Acceda a la dirección URL `https://'[server]:[port]'/lc/ws` e inicie sesión con las credenciales de administrador/contraseña. El explorador le redirigirá a `https://'[server]:[port]'/lc/apps/ws/index.html`.
