---
title: Integración de componentes del espacio de trabajo de AEM Forms en aplicaciones web
seo-title: Integración de componentes del espacio de trabajo de AEM Forms en aplicaciones web
description: Cómo reutilizar los componentes del espacio de trabajo de AEM Forms en sus propias aplicaciones web para aprovechar la funcionalidad y proporcionar una estrecha integración.
seo-description: Cómo reutilizar los componentes del espacio de trabajo de AEM Forms en sus propias aplicaciones web para aprovechar la funcionalidad y proporcionar una estrecha integración.
uuid: bb9b8aa0-3f41-4f44-8eb7-944e778ee8a6
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6be87939-007e-42c7-8a41-e34ac2b8bed4
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# Integración de componentes del espacio de trabajo de AEM Forms en aplicaciones Web {#integrating-aem-forms-workspace-components-in-web-applications}

Puede utilizar el espacio de trabajo [componentes](/help/forms/using/description-reusable-components.md) de AEM Forms en su propia aplicación Web. La siguiente implementación de ejemplo utiliza componentes de un paquete de desarrollo de espacio de trabajo de AEM Forms instalado en una instancia de CRX™ para crear una aplicación web. Personalice la siguiente solución para adaptarla a sus necesidades específicas. La implementación de muestra reutiliza `UserInfo`, `FilterList` y `TaskList`componentes dentro de un portal Web.

1. Inicie sesión en el entorno del CRXDE Lite en `https://'[server]:[port]'/lc/crx/de/`. Asegúrese de tener instalado un paquete de desarrollo de espacio de trabajo de AEM Forms.
1. Cree una ruta `/apps/sampleApplication/wscomponents`.
1. Copiar css, imágenes, js/libs, js/Runtime y js/registry.js

   * de `/libs/ws`
   * hasta `/apps/sampleApplication/wscomponents`.

1. Cree un archivo demoain.js en la carpeta /apps/sampleApplication/wscomponents/js. Copie el código de /libs/ws/js/main.js en demomain.js.
1. En demomain.js, elimine el código para inicializar el router y agregue el siguiente código:

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

1. Cree un nodo bajo /content por nombre `sampleApplication` y escriba `nt:unstructured`. En las propiedades de este nodo, agregue `sling:resourceType` de tipo String y valor `sampleApplication`. En la Lista de Control de acceso de este nodo, agregue una entrada para `PERM_WORKSPACE_USER` que permita privilegios jcr:read. Además, en la Lista de Control de acceso de `/apps/sampleApplication` agregue una entrada para `PERM_WORKSPACE_USER` que permita privilegios jcr:read.
1. En `/apps/sampleApplication/wscomponents/js/registry.js`, actualice las rutas de `/lc/libs/ws/` a `/lc/apps/sampleApplication/wscomponents/` para los valores de plantilla.
1. En el archivo JSP de la página de inicio del portal, en `/apps/sampleApplication/GET.jsp`, agregue el siguiente código para incluir los componentes necesarios dentro del portal.

   ```jsp
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   También incluya los archivos CSS necesarios para los componentes del espacio de trabajo de AEM Forms.

   >[!NOTE]
   >
   >Cada componente se agrega a la etiqueta de componente (con componente de clase) durante el procesamiento. Asegúrese de que la página de inicio contenga estas etiquetas. Consulte el archivo `html.jsp` del espacio de trabajo de AEM Forms para obtener más información sobre estas etiquetas de control base.

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

1. Modifique la CSS del portal para configurar el diseño, la posición y el estilo de los componentes necesarios en el portal. Por ejemplo, desea mantener el color de fondo como negro para que este portal pueda realizar una vista correcta del componente userInfo. Puede hacerlo cambiando el color de fondo en `/apps/sampleApplication/wscomponents/css/style.css` de la siguiente manera:

   ```css
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
