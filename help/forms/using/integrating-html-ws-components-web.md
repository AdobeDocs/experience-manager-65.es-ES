---
title: Integración de componentes de espacio de trabajo de AEM Forms en aplicaciones web
seo-title: Integrating AEM Forms workspace components in web applications
description: Cómo reutilizar los componentes del espacio de trabajo de AEM Forms en sus propias aplicaciones web para aprovechar la funcionalidad y proporcionar una integración más estrecha.
seo-description: How to reuse AEM Forms workspace components in your own webapps to leverage functionality and provide tight integration.
uuid: bb9b8aa0-3f41-4f44-8eb7-944e778ee8a6
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6be87939-007e-42c7-8a41-e34ac2b8bed4
exl-id: bb4a500d-c34f-4586-83f0-ad7ef69b4fb1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# Integración de componentes de espacio de trabajo de AEM Forms en aplicaciones web {#integrating-aem-forms-workspace-components-in-web-applications}

Puede utilizar el espacio de trabajo de AEM Forms [componentes](/help/forms/using/description-reusable-components.md) en su propia aplicación web. La siguiente implementación de ejemplo utiliza componentes de un paquete de desarrollo de espacio de trabajo de AEM Forms instalado en una instancia CRX™ para crear una aplicación web. Personalice la siguiente solución para adaptarla a sus necesidades específicas. La implementación de muestra se reutiliza `UserInfo`, `FilterList`y `TaskList`componentes dentro de un portal web.

1. Inicie sesión en el entorno de CRXDE Lite en `https://'[server]:[port]'/lc/crx/de/`. Asegúrese de tener instalado un paquete de desarrollo del espacio de trabajo de AEM Forms.
1. Crear una ruta `/apps/sampleApplication/wscomponents`.
1. Copie css, imágenes, js/libs, js/runtime y js/registry.js

   * de `/libs/ws`
   * hasta `/apps/sampleApplication/wscomponents`.

1. Cree un archivo admin.js dentro de la carpeta /apps/sampleApplication/wscomponents/js . Copie el código de /libs/ws/js/main.js en demomain.js.
1. En demomain.js, elimine el código para inicializar Router y agregue el siguiente código:

   ```javascript
   require(['initializer','runtime/util/usersession'],
       function(initializer, UserSession) {
           UserSession.initialize(
               function() {
                   // Render all the global components
                   initializer.initGlobal();
               });
       });
   ```

1. Cree un nodo bajo /content por nombre `sampleApplication` y tipo `nt:unstructured`. En las propiedades de este nodo, agregue `sling:resourceType` de tipo String y value `sampleApplication`. En la Lista de control de acceso de este nodo, agregue una entrada para `PERM_WORKSPACE_USER` permitiendo privilegios jcr:read. Además, en la Lista de control de acceso de `/apps/sampleApplication` agregar una entrada para `PERM_WORKSPACE_USER` permitiendo privilegios jcr:read.
1. En `/apps/sampleApplication/wscomponents/js/registry.js` actualizar rutas desde `/lc/libs/ws/` a `/lc/apps/sampleApplication/wscomponents/` para valores de plantilla.
1. En su página de inicio del portal, archivo JSP en `/apps/sampleApplication/GET.jsp`, añada el siguiente código para incluir los componentes necesarios dentro del portal.

   ```jsp
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   Incluya también los archivos CSS necesarios para los componentes del espacio de trabajo de AEM Forms.

   >[!NOTE]
   >
   >Cada componente se añade a la etiqueta del componente (con componente de clase) durante la renderización. Asegúrese de que la página de inicio contenga estas etiquetas. Consulte la `html.jsp` del espacio de trabajo de AEM Forms para obtener más información sobre estas etiquetas de control base.

1. Para personalizar los componentes, puede ampliar las vistas existentes para el componente requerido de la siguiente manera:

   ```javascript
   define([
       ‘jquery’,
       ‘underscore’,
       ‘backbone’,
       ‘runtime/views/userinfo'],
       function($, _, Backbone, UserInfo){
           var demoUserInfo = UserInfo.extend({
               //override the functions to customize the functionality
               render: function() {
                   UserInfo.prototype.render.call(this); // call the render function of the super class
                   …
                   //other tasks
                   …
               }
           });
           return demoUserInfo;
   });
   ```

1. Modifique el portal CSS para configurar el diseño, la posición y el estilo de los componentes necesarios en el portal. Por ejemplo, desea mantener el color de fondo como negro para que este portal vea bien el componente userInfo. Para ello, cambie el color de fondo en `/apps/sampleApplication/wscomponents/css/style.css` de la siguiente manera:

   ```css
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
