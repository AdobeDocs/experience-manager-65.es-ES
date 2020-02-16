---
title: Pasos genéricos para la personalización del espacio de trabajo de AEM Forms
seo-title: Pasos genéricos para la personalización del espacio de trabajo de AEM Forms
description: Cómo empezar a personalizar la interfaz de usuario del espacio de trabajo de AEM Forms.
seo-description: Cómo empezar a personalizar la interfaz de usuario del espacio de trabajo de AEM Forms.
uuid: da6310b4-1c58-468d-85c6-975fd2c141f9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: dd3218c4-2bb2-40fc-9141-5823b0ea4224
docset: aem65
translation-type: tm+mt
source-git-commit: 21623c615ebe69226cfaf84baf4cfb1717b449f4

---


# Pasos genéricos para la personalización del espacio de trabajo de AEM Forms{#generic-steps-for-aem-forms-workspace-customization}

Los pasos genéricos para realizar cualquier personalización son:

1. Inicie sesión en CRXDE Lite accediendo `https://[server]:[port]/lc/crx/de/index.jsp`.
1. Cree una carpeta denominada `ws`at `/apps`, si no existe. Haga clic en **[!UICONTROL Guardar todo]**.
1. Vaya a `/apps/ws`la ficha Control **[!UICONTROL de]** acceso y desplácese hasta ella.
1. En la lista Control **[!UICONTROL de]** acceso, haga clic en **[!UICONTROL +]** para agregar una nueva entrada. Haga clic **[!UICONTROL +]** nuevamente.
1. Busque y seleccione la entidad **PERM_WORKSPACE_USER** Principal.

   ![Seleccione el principal PERM_WORKSPACE_USER como parte de los pasos genéricos para personalizar HTML Workspace](assets/perm_workspace_user.png)

1. Dar `jcr:read` privilegio al director.
1. Haga clic en **[!UICONTROL Guardar todo]**.
1. Copie los `GET.jsp` archivos `html.jsp`y de la `/libs/ws`carpeta en la `/apps/ws` carpeta.
1. Copie la `/libs/ws/locales` carpeta en la `/apps/ws` carpeta. Haga clic en **[!UICONTROL Guardar todo]**.
1. Actualice las referencias y las rutas relativas en el `GET.jsp` archivo, como se muestra a continuación, y haga clic en **[!UICONTROL Guardar todo]**.

   ```
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. Para las personalizaciones de CSS, haga lo siguiente:

   1. Vaya a la `/apps/ws` carpeta y cree una nueva carpeta con el nombre `css`.

   1. En la carpeta de `css`carpetas, cree un nuevo archivo denominado `newStyle.css`.

   1. Abrir `/apps/ws/html`.jsp y cambiar de

   ```css
   <link lang="en" rel="stylesheet" type="text/css" href="css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/jquery-ui.css"/>
   ```

   hasta

   ```css
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/newStyle.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/jquery-ui.css"/>
   ```

   >[!NOTE]
   >
   >Coloque la entrada del archivo CSS definido por el usuario después de la entrada de newStyle.css, como se muestra arriba.

1. En el archivo /apps/ws/html.jsp, cambie de

   ```css
   <script data-main="js/main" src="js/libs/require/require.js"></script>
   ```

   hasta

   ```css
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. Haga lo siguiente:

   1. Cree una carpeta con el nombre `js`en `/apps/ws`. Haga clic en **[!UICONTROL Guardar todo]**.

   1. Cree una carpeta con el nombre `libs`en `/apps/ws/js`. Haga clic en **[!UICONTROL Guardar todo]**.

   1. Cree una carpeta con el nombre `jqueryui`en `/apps/ws/js/libs`. Haga clic en **[!UICONTROL Guardar todo]**.

   1. Copiar `/libs/ws/js/libs/jqueryui/jquery.ui.datepicker-ja.js` a `/apps/ws/js/libs/jqueryui`. Haga clic en **[!UICONTROL Guardar todo]**.

1. Para las personalizaciones de HTML, haga lo siguiente:

   1. En `/apps/ws/js`, cree una carpeta con el nombre `runtime`. Haga clic en **[!UICONTROL Guardar todo]**.

   1. En `/apps/ws/js/runtime`, cree una carpeta con el nombre `templates`. Haga clic en **[!UICONTROL Guardar todo]**.

   1. Copiar `/libs/ws/js/main.js` a `/apps/ws/js/main.js`.

   1. Copie /libs/ws/js/registry.js en `/apps/ws/js/registry.js`.

1. Haga clic en **[!UICONTROL Guardar todo]**, borre la caché y actualice el espacio de trabajo de AEM Forms.

   Acceda a la URL `https://[server]:[port]/lc/ws` e inicie sesión con credenciales de administrador/contraseña. El explorador redirige a `https://[server]:[port]/lc/apps/ws/index.html`.

[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
