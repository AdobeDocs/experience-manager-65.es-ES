---
title: Creación de un Cloud Service personalizado
seo-title: Creación de un Cloud Service personalizado
description: El conjunto predeterminado de Cloud Services se puede ampliar con tipos de Cloud Service personalizados
seo-description: El conjunto predeterminado de Cloud Services se puede ampliar con tipos de Cloud Service personalizados
uuid: b105a0c1-b68c-4f57-8e3b-561c8051a08e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e48e87c6-43ca-45ba-bd6b-d74c969757cd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 12%

---


# Creación de un Cloud Service personalizado{#creating-a-custom-cloud-service}

El conjunto predeterminado de Cloud Services se puede ampliar con tipos de Cloud Service personalizados. Esto le permite insertar marcas personalizadas en la página de forma estructurada. Esto será útil principalmente para proveedores de análisis de terceros, como Google Analytics, Chartbeat, etc. Los Cloud Services se heredan de las páginas principales a las páginas secundarias con la capacidad de romper la herencia en cualquier nivel.

>[!NOTE]
>
>Esta guía paso a paso para crear un nuevo Cloud Service es un ejemplo de uso de Google Analytics. Todo podría no aplicarse a su caso de uso.

1. En CRXDE Lite, cree un nuevo nodo en `/apps`:

   * **Nombre**: `acs`
   * **Tipo**: `nt:folder`

1. Cree un nuevo nodo en `/apps/acs`:

   * **Nombre**: `analytics`
   * **Tipo**: `sling:Folder`

1. Cree 2 nuevos nodos en `/apps/acs/analytics`:

   * **Nombre**: componentes
   * **Tipo**: `sling:Folder`

   y

   * **Nombre**: plantillas
   * **Tipo**: `sling:Folder`


1. Haga clic con el botón derecho en `/apps/acs/analytics/components`. Seleccione **Crear...** seguido de **Crear componente...** El cuadro de diálogo que se abre le permite especificar:

   * **Etiqueta**: `googleanalyticspage`
   * **Título**: `Google Analytics Page`
   * **Super Type**: `cq/cloudserviceconfigs/components/configpage`
   * **Agrupar**: `.hidden`

1. Haga clic **Siguiente** dos veces y especifique:

   * **Principales permitidos:** `acs/analytics/templates/googleanalytics`

   Haga clic en **Siguiente** dos veces y haga clic en **Aceptar**.

1. Añada una propiedad a `googleanalyticspage`:

   * **Nombre:** `cq:defaultView`
   * **Valor:** `html`

1. Cree un nuevo archivo denominado `content.jsp` en `/apps/acs/analytics/components/googleanalyticspage`, con el siguiente contenido:

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

1. Cree un nuevo nodo en `/apps/acs/analytics/components/googleanalyticspage/`:

   * **Nombre**: `dialog`
   * **Tipo**: `cq:Dialog`
   * **Propiedades**:

      * **Nombre**: `title`
      * **Tipo**: `String`
      * **Valor**:  `Google Analytics Config`
      * **Nombre**: `xtype`
      * **Tipo**: `String`
      * **Valor**:  `dialog`

1. Cree un nuevo nodo en `/apps/acs/analytics/components/googleanalyticspage/dialog`:

   * **Nombre**: `items`
   * **Tipo**: `cq:Widget`
   * **Propiedades**:

      * **Nombre**: `xtype`
      * **Tipo**: `String`
      * **Valor**:  `tabpanel`

1. Cree un nuevo nodo en `/apps/acs/analytics/components/googleanalyticspage/dialog/items`:

   * **Nombre**: `items`
   * **Tipo**: `cq:WidgetCollection`

1. Cree un nuevo nodo en `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items`:

   * **Nombre**: tab1
   * **Tipo**: `cq:Panel`
   * **Propiedades**:

      * **Nombre**: `title`
      * **Tipo**: `String`
      * **Valor**:  `Config`

1. Cree un nuevo nodo en `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items/tab1`:

   * **Nombre**: elementos
   * **Tipo**: `nt:unstructured`
   * **Propiedades**:

      * **Nombre**: `fieldLabel`
      * **Tipo**: Cadena
      * **Valor**: ID de cuenta

      * **Nombre**: `fieldDescription`
      * **Tipo**: `String`
      * **Valor**:  `The account ID assigned by Google. Usually in the form UA-NNNNNN-N`

      * **Nombre**: `name`
      * **Tipo**: `String`
      * **Valor**:  `./accountID`
      * **Nombre**: `validateOnBlur`
      * **Tipo**: `String`
      * **Valor**:  `true`
      * **Nombre**: `xtype`
      * **Tipo**: `String`
      * **Valor**:  `textfield`

1. Copie `/libs/cq/cloudserviceconfigs/components/configpage/body.jsp` en `/apps/acs/analytics/components/googleanalyticspage/body.jsp` y cambie `libs` a `apps` en la línea 34 y convierta la referencia de secuencia de comandos en la línea 79 en una ruta completa.
1. Cree una nueva plantilla en `/apps/acs/analytics/templates/`:

   * con **Tipo de recurso** = `acs/analytics/components/googleanalyticspage`
   * con **Etiqueta** = `googleanalytics`
   * con **Título**= `Google Analytics Configuration`
   * with **allowPath** = `/etc/cloudservices/googleanalytics(/.*)?`
   * con **allowChildren** = `/apps/acs/analytics/templates/googleanalytics`
   * con **sling:resourceSuperType** = `cq/cloudserviceconfigs/templates/configpage` (en el nodo de plantilla, no en el nodo jcr:content)
   * con **cq:designPath** = `/etc/designs/cloudservices/googleanalytics` (en jcr:content)

1. Crear nuevo componente: `/apps/acs/analytics/components/googleanalytics`.

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

   Esto debería generar el marcado personalizado basado en las propiedades de configuración.

1. Vaya a `http://localhost:4502/miscadmin#/etc/cloudservices` y cree una nueva página:

   * **Título**: `Google Analytics`
   * **Nombre**: `googleanalytics`

   Vuelva al CRXDE Lite y, en `/etc/cloudservices/googleanalytics`, agregue la siguiente propiedad a `jcr:content`:

   * **Nombre**: `componentReference`
   * **Tipo**: `String`
   * **Valor**:  `acs/analytics/components/googleanalytics`


1. Vaya a la página Servicio recientemente creada ( `http://localhost:4502/etc/cloudservices/googleanalytics.html`) y haga clic en **+** para crear una nueva configuración:

   * **Configuración principal**: `/etc/cloudservices/googleanalytics`
   * **Título:**  `My First GA Config`

   Elija **Configuración de Google Analytics** y haga clic en **Crear**.

1. Escriba un **ID de cuenta**, por ejemplo `AA-11111111-1`. Haga clic en **Aceptar**.
1. Vaya a una página y agregue la configuración recién creada en las propiedades de la página, en la ficha **Cloud Services**.
1. Se agregará el marcado personalizado a la página.

