---
title: Creación de un Cloud Service personalizado
description: El conjunto predeterminado de Cloud Services se puede ampliar con tipos de Cloud Service personalizados
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 9414c77a-b180-4440-8386-e6eb4426e475
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# Creación de un Cloud Service personalizado{#creating-a-custom-cloud-service}

El conjunto predeterminado de Cloud Services se puede ampliar con tipos de Cloud Service personalizados. Esto permite insertar marcado personalizado en la página de forma estructurada. Esto es principalmente útil para proveedores de análisis de terceros, por ejemplo, Google Analytics, Chartbeat, etc. Los Cloud Service se heredan de las páginas principales a las secundarias, con la capacidad de interrumpir la herencia en cualquier nivel.

>[!NOTE]
>
>Esta guía paso a paso para crear un Cloud Service es un ejemplo con Google Analytics. Es posible que no todo se aplique a su caso de uso.

1. En CRXDE Lite, cree un nodo en `/apps`:

   * **Nombre**: `acs`
   * **Tipo**: `nt:folder`

1. Cree un nodo en `/apps/acs`:

   * **Nombre**: `analytics`
   * **Tipo**: `sling:Folder`

1. Cree dos nodos en `/apps/acs/analytics`:

   * **Nombre**: componentes
   * **Tipo**: `sling:Folder`

   y

   * **Nombre**: plantillas
   * **Tipo**: `sling:Folder`

1. Clic con el botón derecho `/apps/acs/analytics/components`. Seleccionar **Crear...** seguido de **Crear componente...** El cuadro de diálogo que se abre permite especificar lo siguiente:

   * **Etiqueta**: `googleanalyticspage`
   * **Título**: `Google Analytics Page`
   * **Super Type**: `cq/cloudserviceconfigs/components/configpage`
   * **Grupo**: `.hidden`

1. Clic **Siguiente** dos veces y especifique:

   * **Principales permitidos:** `acs/analytics/templates/googleanalytics`

   Clic **Siguiente** dos veces y haga clic **OK**.

1. Añadir una propiedad a `googleanalyticspage`:

   * **Nombre:** `cq:defaultView`
   * **Valor:** `html`

1. Cree un archivo llamado `content.jsp` bajo `/apps/acs/analytics/components/googleanalyticspage`, con el siguiente contenido:

   ```xml
   <%@page contentType="text/html"
               pageEncoding="utf-8"%><%
   %><%@include file="/libs/foundation/global.jsp"%><div>
   
   <div>
       <h3>Google Analytics Settings</h3>
       <ul>
           <li><div class="li-bullet"><strong>accountID: </strong><br><%= xssAPI.encodeForHTML(properties.get("accountID", "")) %></div></li>
       </ul>
   </div>
   ```

1. Cree un nodo en `/apps/acs/analytics/components/googleanalyticspage/`:

   * **Nombre**: `dialog`
   * **Tipo**: `cq:Dialog`
   * **Propiedades**:

      * **Nombre**: `title`
      * **Tipo**: `String`
      * **Valor**: `Google Analytics Config`
      * **Nombre**: `xtype`
      * **Tipo**: `String`
      * **Valor**: `dialog`

1. Cree un nodo en `/apps/acs/analytics/components/googleanalyticspage/dialog`:

   * **Nombre**: `items`
   * **Tipo**: `cq:Widget`
   * **Propiedades**:

      * **Nombre**: `xtype`
      * **Tipo**: `String`
      * **Valor**: `tabpanel`

1. Cree un nodo en `/apps/acs/analytics/components/googleanalyticspage/dialog/items`:

   * **Nombre**: `items`
   * **Tipo**: `cq:WidgetCollection`

1. Cree un nodo en `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items`:

   * **Nombre**: pestaña1
   * **Tipo**: `cq:Panel`
   * **Propiedades**:

      * **Nombre**: `title`
      * **Tipo**: `String`
      * **Valor**: `Config`

1. Cree un nodo en `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items/tab1`:

   * **Nombre**: elementos
   * **Tipo**: `nt:unstructured`
   * **Propiedades**:

      * **Nombre**: `fieldLabel`
      * **Tipo**: cadena
      * **Valor**: ID de cuenta

      * **Nombre**: `fieldDescription`
      * **Tipo**: `String`
      * **Valor**: `The account ID assigned by Google. Usually in the form UA-NNNNNN-N`

      * **Nombre**: `name`
      * **Tipo**: `String`
      * **Valor**: `./accountID`
      * **Nombre**: `validateOnBlur`
      * **Tipo**: `String`
      * **Valor**: `true`
      * **Nombre**: `xtype`
      * **Tipo**: `String`
      * **Valor**: `textfield`

1. Copiar `/libs/cq/cloudserviceconfigs/components/configpage/body.jsp` hasta `/apps/acs/analytics/components/googleanalyticspage/body.jsp` y cambiar `libs` hasta `apps` en la línea 34 y haga de la referencia de la secuencia de comandos en la línea 79 una ruta totalmente cualificada.
1. Cree una plantilla en `/apps/acs/analytics/templates/`:

   * con **Tipo de medio** = `acs/analytics/components/googleanalyticspage`
   * con **Etiqueta** = `googleanalytics`
   * con **Título**= `Google Analytics Configuration`
   * con **allowedPath** = `/etc/cloudservices/googleanalytics(/.*)?`
   * con **allowedChildren** = `/apps/acs/analytics/templates/googleanalytics`
   * con **sling:resourceSuperType** = `cq/cloudserviceconfigs/templates/configpage` (en el nodo de plantilla, no en el nodo jcr:content)
   * con **cq:designPath** = `/etc/designs/cloudservices/googleanalytics` (en jcr:content)

1. Crear un componente: `/apps/acs/analytics/components/googleanalytics`.

   Añada el siguiente contenido a `googleanalytics.jsp`:

   ```xml
   <%@page import="org.apache.sling.api.resource.Resource,
                   org.apache.sling.api.resource.ValueMap,
                   org.apache.sling.api.resource.ResourceUtil,
                   com.day.cq.wcm.webservicesupport.Configuration,
                   com.day.cq.wcm.webservicesupport.ConfigurationManager" %>
   <%@include file="/libs/foundation/global.jsp" %><%
   
   String[] services = pageProperties.getInherited("cq:cloudserviceconfigs", new String[]{});
   ConfigurationManager cfgMgr = resource.getResourceResolver().adaptTo(ConfigurationManager.class);
   if(cfgMgr != null) {
       String accountID = null;
       Configuration cfg = cfgMgr.getConfiguration("googleanalytics", services);
       if(cfg != null) {
           accountID = cfg.get("accountID", null);
       }
   
       if(accountID != null) {
       %>
   <script type="text/javascript">
   
     var _gaq = _gaq || [];
     _gaq.push(['_setAccount', '<%= accountID %>']);
     _gaq.push(['_trackPageview']);
   
     (function() {
       var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
       ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'https://www') + '.google-analytics.com/ga.js';
       var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
     })();
   
   </script><%
       }
   }
   %>
   ```

   Esto debería generar el marcado personalizado en función de las propiedades de configuración.

1. Vaya a `http://localhost:4502/miscadmin#/etc/cloudservices` y cree una página:

   * **Título**: `Google Analytics`
   * **Nombre**: `googleanalytics`

   Vuelve en CRXDE Lite, y debajo de `/etc/cloudservices/googleanalytics`, agregue la siguiente propiedad a `jcr:content`:

   * **Nombre**: `componentReference`
   * **Tipo**: `String`
   * **Valor**: `acs/analytics/components/googleanalytics`

1. Vaya a la página de servicio recién creada ( `http://localhost:4502/etc/cloudservices/googleanalytics.html`) y haga clic en **+** para crear una configuración:

   * **Configuración principal**: `/etc/cloudservices/googleanalytics`
   * **Título:**  `My First GA Config`

   Elegir **Configuración de Google Analytics** y haga clic en **Crear**.

1. Introduzca una **ID de cuenta**, por ejemplo, `AA-11111111-1`. Haga clic en **Aceptar**.
1. Vaya a una página y añada la configuración recién creada en las propiedades de página, en la **Cloud Service** pestaña.
1. Se agregará a la página el marcado personalizado.
