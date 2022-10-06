---
title: Pasos genéricos para la personalización del espacio de trabajo de AEM Forms
seo-title: Generic steps for AEM Forms workspace customization
description: Introducción a la personalización de la interfaz de usuario del espacio de trabajo de AEM Forms.
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
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 9%

---

# Pasos genéricos para la personalización del espacio de trabajo de AEM Forms {#generic-steps-for-aem-forms-workspace-customization}

Los pasos genéricos para realizar cualquier personalización son:

1. Inicie sesión en el CRXDE Lite accediendo a `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Cree un `sling:Folder` carpeta denominada `ws` at `/apps`, si no existe. Para crear un `sling:Folder` carpeta, haga clic con el botón derecho en la `apps` carpeta y seleccione **[!UICONTROL Crear]** > **[!UICONTROL Crear nodo]**. Especifique el nombre como `ws`, seleccione tipo `sling:Folder` y haga clic en **[!UICONTROL OK]**. Haga clic en **[!UICONTROL Guardar todo]**.
1. Vaya a `/apps/ws`y vaya a la **[!UICONTROL Control de acceso]** pestaña .
1. Seleccione el **[!UICONTROL Repositorio]** . En el **[!UICONTROL Control de acceso]** lista, haga clic en **[!UICONTROL +]** para agregar una nueva entrada. Haga clic en **[!UICONTROL +]** de nuevo.
1. Busque y seleccione el **PERM_WORKSPACE_USER** Principal.

   ![Seleccione la entidad de seguridad PERM_WORKSPACE_USER como parte de los pasos genéricos para personalizar HTML Workspace](assets/perm_workspace_user.png)

1. Dar `jcr:read` a Principal.
1. Haga clic en **[!UICONTROL Guardar todo]**.
1. Copie el `GET.jsp`, `index`y `html.jsp` los archivos de `/libs/ws` a la `/apps/ws` carpeta.
1. Copie el `/libs/ws/locales` en la carpeta `/apps/ws` carpeta. Haga clic en **[!UICONTROL Guardar todo]**.
1. Actualice las referencias y las rutas relativas en el `GET.jsp` , como se muestra a continuación, y haga clic en **[!UICONTROL Guardar todo]**.

   ```javascript
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. Haga lo siguiente para las personalizaciones de CSS:

   1. Vaya a la `/apps/ws` carpeta y cree una nueva carpeta con el nombre `css`.

   1. En el `css` carpeta, cree un nuevo archivo con el nombre `newStyle.css`.

   1. Apertura `/apps/ws/html`.jsp y cambiar de

   ```javascript
   <link lang="en" rel="stylesheet" type="text/css" href="css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/jquery-ui.css"/>
   ```

   hasta

   ```javascript
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/newStyle.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/jquery-ui.css"/>
   ```

   >[!NOTE]
   >
   >Coloque la entrada del archivo CSS definido por el usuario después de la entrada de style.css, como se muestra arriba.

1. En el archivo /apps/ws/html.jsp, cambie de

   ```jsp
   <script data-main="js/main" src="js/libs/require/require.js"></script>
   ```

   hasta

   ```jsp
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. Haga lo siguiente:

   1. Crear una carpeta con el nombre `js` at `/apps/ws`. Haga clic en **[!UICONTROL Guardar todo]**.

   1. Crear una carpeta con el nombre `libs` at `/apps/ws/js`. Haga clic en **[!UICONTROL Guardar todo]**.

   1. Copiar `/libs/ws/js/libs/jqueryui` carpeta a `/apps/ws/js/libs`. Haga clic en **[!UICONTROL Guardar todo]**.

1. Haga lo siguiente para las personalizaciones de HTML:

   1. En `/apps/ws/js`, cree una carpeta con el nombre `runtime`. Haga clic en **[!UICONTROL Guardar todo]**.

   1. En `/apps/ws/js/runtime`, cree una carpeta con el nombre `templates`. Haga clic en **[!UICONTROL Guardar todo]**.

   1. Copiar `/libs/ws/js/main.js` a `/apps/ws/js/main.js`.

   1. Copiar /libs/ws/js/registry.js en `/apps/ws/js/registry.js`.

1. Haga clic en **[!UICONTROL Guardar todo]**, borre la caché y actualice el espacio de trabajo de AEM Forms.

   Acceso a la dirección URL `https://'[server]:[port]'/lc/ws` e inicie sesión con credenciales de administrador/contraseña. El explorador redirige a `https://'[server]:[port]'/lc/apps/ws/index.html`.
