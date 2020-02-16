---
title: Integración de componentes del espacio de trabajo de AEM Forms en aplicaciones web
seo-title: Integración de componentes del espacio de trabajo de AEM Forms en aplicaciones web
description: Cómo reutilizar los componentes del espacio de trabajo de AEM Forms en sus propias aplicaciones web para aprovechar la funcionalidad y proporcionar una integración estrecha.
seo-description: Cómo reutilizar los componentes del espacio de trabajo de AEM Forms en sus propias aplicaciones web para aprovechar la funcionalidad y proporcionar una integración estrecha.
uuid: bb9b8aa0-3f41-4f44-8eb7-944e778ee8a6
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6be87939-007e-42c7-8a41-e34ac2b8bed4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Integración de componentes del espacio de trabajo de AEM Forms en aplicaciones web {#integrating-aem-forms-workspace-components-in-web-applications}

Puede utilizar [componentes](/help/forms/using/description-reusable-components.md) del espacio de trabajo de AEM Forms en su propia aplicación web. La siguiente implementación de ejemplo utiliza componentes de un paquete de desarrollo de espacio de trabajo de AEM Forms instalado en una instancia de CRX™ para crear una aplicación web. Personalice la siguiente solución para adaptarla a sus necesidades específicas. La implementación de muestra reutiliza `UserInfo``FilterList`y `TaskList`componentes dentro de un portal web.

1. Inicie sesión en el entorno CRXDE Lite en `https://[server]:[port]/lc/crx/de/`. Asegúrese de tener instalado un paquete de desarrollo de espacio de trabajo de AEM Forms.
1. Cree una ruta `/apps/sampleApplication/wscomponents`.
1. Copiar css, imágenes, js/libs, js/Runtime y js/registry.js

   * from `/libs/ws`
   * hasta `/apps/sampleApplication/wscomponents`.

1. Cree un archivo demoain.js en la carpeta /apps/sampleApplication/wscomponents/js. Copie el código de /libs/ws/js/main.js en demomain.js.
1. En demomain.js, elimine el código para inicializar el router y agregue el siguiente código:

   ```
   require(['initializer','runtime/util/usersession'],
       function(initializer, UserSession) {
           UserSession.initialize(
               function() {
                   // Render all the global components
                   initializer.initGlobal();
               });
       });
   ```

1. Cree un nodo en /content por nombre `sampleApplication` y escriba `nt:unstructured`. En las propiedades de este nodo, agregue `sling:resourceType` el tipo String y value `sampleApplication`. En la lista de control de acceso de este nodo, agregue una entrada para `PERM_WORKSPACE_USER` permitir privilegios jcr:read. Además, en la Lista de control de acceso de `/apps/sampleApplication` agregue una entrada para `PERM_WORKSPACE_USER` permitir privilegios jcr:read.
1. En `/apps/sampleApplication/wscomponents/js/registry.js` las rutas de actualización de `/lc/libs/ws/` a `/lc/apps/sampleApplication/wscomponents/` para los valores de plantilla.
1. En el archivo JSP de la página principal del portal en `/apps/sampleApplication/GET.jsp`, agregue el siguiente código para incluir los componentes necesarios dentro del portal.

   ```as3
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   Incluya también los archivos CSS necesarios para los componentes del espacio de trabajo de AEM Forms.

   >[!NOTE]
   >
   >Cada componente se agrega a la etiqueta de componente (con componente de clase) durante el procesamiento. Asegúrese de que la página principal contenga estas etiquetas. Consulte el archivo `html.jsp` del espacio de trabajo de AEM Forms para obtener más información sobre estas etiquetas de control base.

1. Para personalizar los componentes, puede ampliar las vistas existentes para el componente requerido de la siguiente manera:

   ```as3
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

1. Modifique la CSS del portal para configurar el diseño, la posición y el estilo de los componentes necesarios en el portal. Por ejemplo, desea mantener el color de fondo como negro para que este portal pueda ver bien el componente userInfo. Para ello, cambie el color de fondo de la `/apps/sampleApplication/wscomponents/css/style.css` siguiente manera:

   ```as3
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```

**[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)**
