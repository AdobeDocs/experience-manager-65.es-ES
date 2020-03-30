---
title: Alojamiento de dos instancias de espacio de trabajo de AEM Forms en un servidor
seo-title: Alojamiento de dos instancias de espacio de trabajo de AEM Forms en un servidor
description: Cómo los administradores de LC pueden personalizar HTML WS para alojar dos instancias en un único servidor accesible a través de distintas direcciones URL.
seo-description: Cómo los administradores de LC pueden personalizar HTML WS para alojar dos instancias en un único servidor accesible a través de distintas direcciones URL.
uuid: 0584f512-6b92-4418-b71c-93605cfa1927
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 1254a7c2-2c67-4661-803e-afd53e817916
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Alojamiento de dos instancias de espacio de trabajo de AEM Forms en un servidor {#hosting-two-aem-forms-workspace-instances-on-one-server}

La instalación y configuración predeterminadas de AEM Forms permiten que solo haya un espacio de trabajo de AEM Forms disponible en el servidor. Sin embargo, es posible que tenga que alojar dos instancias diferentes del espacio de trabajo de AEM Forms en un único servidor de AEM Forms. Las dos instancias son accesibles mediante distintas direcciones URL.

Los administradores de AEM Forms personalizan el espacio de trabajo para crear dos direcciones URL diferentes y hacer que dos espacios de trabajo estén disponibles en el mismo servidor. En este artículo de personalización, suponemos que los dos espacios de trabajo son accesibles en `https://'[server]:[port]'/lc/ws` y `https://'[server]:[port]':/lc/ws2`.

Siga estos pasos para configurar el espacio de trabajo de AEM Forms.

1. Instale el paquete dev del espacio de trabajo de AEM Forms en su servidor. Consulte [dev package](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)para obtener instrucciones para crearlo.
1. Inicie sesión en CRXDE Lite como administrador, accediendo a `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Copie el nodo ws en /content y péguelo en /content. Cambie el nombre del nodo a ws2. Haga clic en **[!UICONTROL Guardar todo]**. En las propiedades de este nodo, cambie el valor de `sling:resourceType` a ws2. Haga clic en **[!UICONTROL Guardar todo]**.

1. Copie las carpetas de /libs y péguelas en /apps. Cambie el nombre de la carpeta a ws2. Haga clic en **[!UICONTROL Guardar todo]**.
1. En `GET.jsp` at `/apps/ws2`, realice los siguientes cambios en el código. Reemplace lo siguiente

   ```
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/libs/ws/index.html'" /><html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/libs/ws/index.html'" />
   ```

   con el siguiente código

   ```
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. En `registry.js` at `/apps/ws2/js`, cambie la ruta de las plantillas para hacer referencia a las plantillas en `/apps/ws2/js/runtime/templates`. Reemplazar el siguiente código

   ```css
   "tasklist" : {
   "name": "tasklist",
   "path": "tasklistview",
   "model": "tasklist",
   "template": "text!/lc/libs/ws/js/runtime/templates/tasklist.html",
   "utility": "utility",
   "view": "taskview",
   "errorModel": null
   }
   ```

   con el siguiente código

   ```css
   "tasklist" : {
   "name": "tasklist",
   "path": "tasklistview",
   "model": "tasklist",
   "template": "text!/lc/apps/ws2/js/runtime/templates/tasklist.html",
   "utility": "utility",
   "view": "taskview",
   "errorModel": null
   }
   ```

1. En `userinfo.js` at `/apps/ws2/js/runtime/models` y `/apps/ws2/js/runtime/views`, cambie la cadena `/lc/content/ws` a `lc/content/ws2`.

1. En `/apps/ws2/js/runtime/services/service.js`, cambie la ruta de la `getLocalizationData` función para que señale a `/lc/apps/ws2/Locale.html`.

1. Para hacer referencia a `pdf.html` del nuevo espacio de trabajo, cambie la ruta de `pdf.html` entrada `/apps/ws2/js/runtime/views/forms/pdftaskform.js`.

1. Para hacer referencia a `pdf.html` del nuevo espacio de trabajo, cambie las rutas de acceso de `pdf.html` y `WsNextAdapter.swf` en `startprocess.html`, `taskdetails.html`y `processinstancehistory.html` en `/apps/ws2/js/runtime/templates`.

1. Copiar `/etc/map/ws` carpeta y pegar en `/etc/map`. Cambie el nombre de la nueva carpeta a ws2. Haga clic en Guardar todo.

1. En las propiedades de `ws2`, cambie el valor de `sling:redirect` a `content/ws2`.

1. Cambiar el valor de `sling:match` a `^[^/\||]/[^/\||]/ws2$`.

[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
