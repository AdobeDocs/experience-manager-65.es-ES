---
title: Añadir el seguimiento de Adobe Analytics a los componentes
seo-title: Añadir el seguimiento de Adobe Analytics a los componentes
description: nulo
seo-description: nulo
uuid: 447b140c-678c-428d-a1c9-ecbdec75cd42
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: a11c39b4-c23b-4207-8898-33aea25f2ad0
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835
workflow-type: tm+mt
source-wordcount: '1263'
ht-degree: 0%

---


# Añadir el seguimiento de Adobe Analytics a componentes{#adding-adobe-analytics-tracking-to-components}

## Inclusión del módulo Adobe Analytics en un componente de página {#including-the-adobe-analytics-module-in-a-page-component}

Componentes de plantilla de página (p. ej. `head.jsp, body.jsp`) necesita incluir JSP para cargar ContextHub y la integración de Adobe Analytics (que forma parte de Cloud Services). Todos incluyen archivos JavaScript de carga.

La entrada de ContextHub debe incluirse inmediatamente debajo de la etiqueta `<head>`, mientras que los Cloud Services deben incluirse en la sección `<head>` y antes de la sección `</body>`; por ejemplo:

```xml
<head>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub" />
...
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
...
</head>
<body>
...
    <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
</body>
```

La secuencia de comandos `contexthub` que se inserta después del elemento `<head>` agrega las funciones de ContextHub a la página.

Las secuencias de comandos `cloudservices` que se agregan en las secciones `<head>` y `<body>` se aplican a las configuraciones de servicios en la nube que se agregan a la página. (Si la página utiliza más de una configuración de Cloud Services, debe incluir el jsp de ContextHub y el jsp de Cloud Services solo una vez).

Cuando se agrega un marco de trabajo de Adobe Analytics a la página, las secuencias de comandos `cloudservices` generan javascript relacionado con Adobe Analytics y referencias a bibliotecas del lado del cliente, similar al siguiente ejemplo:

```xml
<div class="sitecatalyst cloudservice">
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/sitecatalyst.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/util.js"></script>
<script type="text/javascript" src="/content/geometrixx-outdoors/_jcr_content/analytics.sitecatalyst.js"></script>
<script type="text/javascript" src="/etc/clientlibs/mac/mac-sc.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/plugins.js"></script>
<script type="text/javascript">
<!--
CQ_Analytics.Sitecatalyst.frameworkComponents = ['foundation/components/page'];
/**
 * Sets Adobe Analytics variables accordingly to mapped components. If <code>options</code>
 * object is provided only variables matching the options.componentPath are set.
 *
 * @param {Object} options Parameter object from CQ_Analytics.record() call. Optional.
 */
CQ_Analytics.Sitecatalyst.updateEvars = function(options) {
    this.frameworkMappings = [];
 this.frameworkMappings.push({scVar:"pageName",cqVar:"pagedata.title",resourceType:"foundation/components/page"});
    for (var i=0; i<this.frameworkMappings.length; i++){
  var m = this.frameworkMappings[i];
  if (!options || options.compatibility || (options.componentPath == m.resourceType)) {
   CQ_Analytics.Sitecatalyst.setEvar(m);
  }
    }
}

CQ_Analytics.CCM.addListener("storesinitialize", function(e) {
 var collect = true;
    var lte = s.linkTrackEvents;
    s.pageName="content:geometrixx-outdoors:en";
    CQ_Analytics.Sitecatalyst.collect(collect);
    if (collect) {
  CQ_Analytics.Sitecatalyst.updateEvars();
     /************* DO NOT ALTER ANYTHING BELOW THIS LINE ! **************/
     var s_code=s.t();if(s_code)document.write(s_code);
     s.linkTrackEvents = lte;
     if(s.linkTrackVars.indexOf('events')==-1){delete s.events};
     $CQ(document).trigger("sitecatalystAfterCollect");
    }
});
//-->
</script>
<script type="text/javascript">
<!--
if(navigator.appVersion.indexOf('MSIE')>=0)document.write(unescape('%3C')+'\!-'+'-')
//-->
</script>
<noscript><img src="https://daydocumentation.112.2o7.net/b/ss/daydocumentation/1/H.25--NS/1380120772954?cdp=3&gn=content%3Ageometrixx-outdoors%3Aen" height="1" width="1" border="0" alt=""/></noscript>
<span data-tracking="{event:'pageView', values:{}, componentPath:'foundation/components/page'}"></span>
<div id="cq-analytics-texthint" style="background:white; padding:0 10px; display:none;">
 <h3 class="cq-texthint-placeholder">Component clientcontext is missing or misplaced.</h3>
</div>
<script type="text/javascript">
$CQ(function(){
 if( CQ_Analytics &&
  CQ_Analytics.ClientContextMgr &&
  !CQ_Analytics.ClientContextMgr.isConfigLoaded )
  {
   $CQ("#cq-analytics-texthint").show();
  }
});
</script>
</div>
```

Todos los sitios de muestra AEM como Geometrixx Outdoors tienen este código incluido.

### El Evento sitecatalystAfterCollect {#the-sitecatalystaftercollect-event}

La secuencia de comandos `cloudservices` déclencheur el evento `sitecatalystAfterCollect`:

```
$CQ(document).trigger("sitecatalystAfterCollect");
```

Este evento se activa para indicar que se ha completado el seguimiento de páginas. Si está realizando operaciones de seguimiento adicionales en esta página, debe escuchar este evento en lugar de la carga del documento o el evento listo para documento. El uso del evento `sitecatalystAfterCollect` evita conflictos u otro comportamiento impredecible.

>[!NOTE]
>
>La biblioteca `/libs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst.js` incluye el código del archivo Adobe Analytics `s_code.js`.

## Implementación del seguimiento de Adobe Analytics para componentes personalizados {#implementing-adobe-analytics-tracking-for-custom-components}

Habilite los componentes de AEM para que interactúen con el marco de trabajo de Adobe Analytics. A continuación, configure el marco para que Adobe Analytics rastree los datos del componente.

Los componentes que interactúan con el marco de trabajo de Adobe Analytics aparecen en SideKick al editar un marco. Después de arrastrar el componente al marco, aparecen las propiedades del componente y, a continuación, puede asignarlas con propiedades de Adobe Analytics. (Consulte [Configuración de un marco para el seguimiento básico](/help/sites-administering/adobeanalytics-connect.md#creating-a-adobe-analytics-framework)).

Los componentes pueden interactuar con la estructura de Adobe Analytics cuando el componente tiene un nodo secundario denominado `analytics`. El nodo `analytics` tiene las siguientes propiedades:

* `cq:trackevents`:: Identifica los eventos de CQ que expone el componente. (Consulte Eventos personalizados).
* `cq:trackvars`:: Asigna un nombre a las variables de CQ asignadas a propiedades de Adobe Analytics.
* `cq:componentName`:: Nombre del componente que aparece en la barra de tareas.
* `cq:componentGroup`:: Grupo en la barra de tareas que incluye el componente.

El código en el JSP del componente agrega javascript a la página que déclencheur el seguimiento y define los datos que se rastrean. El nombre del evento y los nombres de datos utilizados en javascript deben coincidir con los valores correspondientes de las propiedades del nodo `analytics`.

* Utilice el atributo de seguimiento de datos para rastrear los datos de evento cuando se cargue una página. (Consulte [Seguimiento de Eventos personalizados en la carga de página](/help/sites-developing/extending-analytics.md#tracking-custom-events-on-page-load)).
* Utilice la función CQ_Analytics.record para realizar un seguimiento de los datos de evento cuando los usuarios interactúan con las funciones de la página. (Consulte [Seguimiento de Eventos personalizados tras carga de página](/help/sites-developing/extending-analytics.md#tracking-custom-events-after-page-load)).

Cuando se utilizan estos métodos de seguimiento de datos, el módulo de integración de Adobe Analytics realiza automáticamente las llamadas a Adobe Analytics para registrar los eventos y los datos.

### Ejemplo: Rastreo de clics de topnav {#example-tracking-topnav-clicks}

Amplíe el componente de navegación de base para que Adobe Analytics rastree los clics en los vínculos de navegación en la parte superior de la página. Cuando se hace clic en un vínculo de navegación, Adobe Analytics registra el vínculo en el que se hizo clic y la página en la que se hizo clic.

Los siguientes procedimientos requieren que ya haya realizado las siguientes tareas:

* Se ha creado una aplicación de CQ.
* Se ha creado una configuración de Adobe Analytics y un Adobe Analytics Framework.

#### Copiar el componente topnav {#copy-the-topnav-component}

Copie el componente topnav en la aplicación CQ. El procedimiento requiere que la aplicación esté configurada en CRXDE Lite.

1. Haga clic con el botón derecho en el nodo `/libs/foundation/components/topnav` y haga clic en Copiar.
1. Haga clic con el botón secundario en la carpeta Componentes debajo de la carpeta de la aplicación y haga clic en Pegar.
1. Haga clic en Guardar todo.

#### Integración de topnav con Adobe Analytics Framework {#integrating-topnav-with-the-adobe-analytics-framework}

Configure el componente topnav y edite el archivo JSP para definir los eventos y datos de seguimiento.

1. Haga clic con el botón derecho en el nodo de navegación superior y haga clic en Crear > Crear nodo. Especifique los siguientes valores de propiedad y haga clic en Aceptar:

   * Nombre: `analytics`
   * Tipo: `nt:unstructured`

1. Añada la siguiente propiedad en el nodo analytics para asignar un nombre al evento de seguimiento:

   * Nombre: cq:trackevents
   * Tipo: Cadena
   * Valor: topnavClick

1. Añada la siguiente propiedad en el nodo analytics para asignar un nombre a las variables de datos:

   * Nombre: cq:trackvars
   * Tipo: Cadena
   * Valor: topnavTarget,topnavLocation

1. Añada la siguiente propiedad en el nodo analytics para asignar un nombre al componente de la barra de tareas:

   * Nombre: cq:componentName
   * Tipo: Cadena
   * Valor: topnav (seguimiento)

1. Añada la siguiente propiedad en el nodo analytics para asignar un nombre al grupo de componentes de la barra de tareas:

   * Nombre: cq:componentGroup
   * Tipo: Cadena
   * Valor: General

1. Haga clic en Guardar todo.
1. Abra el archivo `topnav.jsp`.
1. En el elemento a, agregue el atributo siguiente:

   ```xml
   onclick = "tracknav('<%= child.getPath() %>.html')"
   ```

1. En la parte inferior de la página, agregue el siguiente código de javascript:

   ```xml
   <script type="text/javascript">
       function tracknav(target) {
               if (CQ_Analytics.Sitecatalyst) {
                   CQ_Analytics.record({
                       event: 'topnavClick',
                       values: {
                           topnavTarget: target,
                           topnavLocation:'<%=currentPage.getPath() %>.html'
                       },
                       componentPath: '<%=resource.getResourceType()%>'
                   });
               }
       }
   </script>
   ```

1. Haga clic en Guardar todo.

El contenido del archivo `topnav.jsp` debe aparecer de la siguiente manera:

```xml
<%@page session="false"%><%--
  Copyright 1997-2008 Day Management AG
  Barfuesserplatz 6, 4001 Basel, Switzerland
  All Rights Reserved.

  This software is the confidential and proprietary information of
  Day Management AG, ("Confidential Information"). You shall not
  disclose such Confidential Information and shall use it only in
  accordance with the terms of the license agreement you entered into
  with Day.

  ==============================================================================

  Top Navigation component

  Draws the top navigation

--%><%@include file="/libs/foundation/global.jsp"%><%
%><%@ page import="java.util.Iterator,
        com.day.text.Text,
        com.day.cq.wcm.api.PageFilter,
        com.day.cq.wcm.api.Page,
        com.day.cq.commons.Doctype,
        org.apache.commons.lang3.StringEscapeUtils" %><%

    // get starting point of navigation
    long absParent = currentStyle.get("absParent", 2L);
    String navstart = Text.getAbsoluteParent(currentPage.getPath(), (int) absParent);

    //if not deep enough take current node
    if (navstart.equals("")) navstart=currentPage.getPath();

    Resource rootRes = slingRequest.getResourceResolver().getResource(navstart);
    Page rootPage = rootRes == null ? null : rootRes.adaptTo(Page.class);
    String xs = Doctype.isXHTML(request) ? "/" : "";
    if (rootPage != null) {
        Iterator<Page> children = rootPage.listChildren(new PageFilter(request));
        while (children.hasNext()) {
            Page child = children.next();
            %><a onclick = "tracknav('<%= child.getPath() %>.html')"  href="<%= child.getPath() %>.html"><%
            %><img alt="<%= StringEscapeUtils.escapeXml(child.getTitle()) %>" src="<%= child.getPath() %>.navimage.png"<%= xs %>></a><%
        }
    }
%><script type="text/javascript">
    function tracknav(target) {
            if (CQ_Analytics.Sitecatalyst) {
                CQ_Analytics.record({
                    event: 'topnavClick',
                    values: {
                        topnavTarget:target,
                        topnavLocation:'<%=currentPage.getPath() %>.html'
                    },
                    componentPath: '<%=resource.getResourceType()%>'
                });
            }
    }
</script>
```

>[!NOTE]
>
>A menudo es deseable rastrear datos desde ContextHub. Para obtener más información sobre el uso de javascript para obtener esta información, consulte [Acceso a valores en ContextHub](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub).

#### Añadir el componente de seguimiento en la barra de tareas {#adding-the-tracking-component-to-sidekick}

Añada los componentes habilitados para el seguimiento con Adobe Analytics en la barra de tareas para poder agregarlos a la estructura.

1. Abra el marco de Adobe Analytics desde la configuración de Adobe Analytics. ([http://localhost:4502/etc/cloudservices/sitecatalyst.html](http://localhost:4502/etc/cloudservices/sitecatalyst.html))
1. En la barra de tareas, haga clic en el botón Diseño.

   ![](assets/chlimage_1a.png)

1. En el área Configuración del seguimiento de vínculos, haga clic en Configurar herencia.

   ![chlimage_1](assets/chlimage_1aa.png)

1. En la lista Componentes permitidos, seleccione topnav (seguimiento) en la sección General y, a continuación, haga clic en OK.
1. Expanda la barra de tareas para entrar en el modo de edición. El componente ya está disponible en el grupo General.

#### Añadir el componente topnav a su entorno {#adding-the-topnav-component-to-your-framework}

Arrastre el componente topnav al marco de Adobe Analytics y asigne las variables y eventos del componente a las variables y eventos de Adobe Analytics. (Consulte [Configuración de un marco para el seguimiento básico](/help/sites-administering/adobeanalytics-connect.md)).

![chlimage_1-1](assets/chlimage_1-1a.png)

El componente topnav ahora está integrado en el marco de Adobe Analytics. Al agregar el componente a una página, al hacer clic en los elementos de la barra de navegación superior, los datos de seguimiento se envían a Adobe Analytics.

### Envío de datos de s.products a Adobe Analytics {#sending-s-products-data-to-adobe-analytics}

Los componentes pueden generar datos para la variable s.products que se envía a Adobe Analytics. Diseñe los componentes para que contribuyan a la variable s.products:

* Registre un valor denominado `product` de una estructura específica.
* Exponga los miembros de datos del valor `product` para que se puedan asignar con variables de Adobe Analytics en el marco de trabajo de Adobe Analytics.

La variable s.products de Adobe Analytics utiliza la siguiente sintaxis:

```
s.products="category;product;quantity;price;eventY={value}|eventZ={value};evarA={value}|evarB={value}"
```

El módulo de integración de Adobe Analytics construye la variable `s.products` utilizando los valores `product` que generan AEM componentes. El valor `product` de javascript que generan AEM componentes es una matriz de valores que tienen la siguiente estructura:

```
"product": [{
    "category": "",
    "sku"     : "path to product node",
    "quantity": quantity,
    "price"   : price,
    "events   : {
      "eventName1": "eventValue1",
      "eventName_n": "eventValue_n"
    }
    "evars"   : {
      "eVarName1": "eVarValue1",
      "eVarName_n": "eVarValue_n"
    }
}]
```

Cuando se omite un elemento de datos del valor `product`, se envía como una cadena vacía en s.products.

>[!NOTE]
>
>Cuando no hay ningún evento asociado con un valor de producto, Adobe Analytics utiliza el evento `prodView` de forma predeterminada.

El nodo `analytics` del componente debe exponer los nombres de las variables mediante la propiedad `cq:trackvars`:

* product.category
* product.sku
* product.quantity
* product.price
* product.events.eventName1
* product.events.eventName_n
* product.evars.eVarName1
* product.evars.eVarName_n

El módulo eCommerce proporciona varios componentes que generan datos de variables s.products. Por ejemplo, el componente de submitorder ([http://localhost:4502/crx/de/index.jsp#/libs/commerce/components/submitorder/submitorder.jsp](http://localhost:4502/crx/de/index.jsp#/libs/commerce/components/submitorder/submitorder.jsp)) genera javascript similar al siguiente ejemplo:

```
<script type="text/javascript">
    function trackCartPurchase() {
        if (CQ_Analytics.Sitecatalyst) {
            CQ_Analytics.record({
                "event": ["productsCartPurchase"],
                "values": {
                    "product": [
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/1",
                            "quantity": 3,
                            "price"   : 179.7,
                            "evars"   : {
                                "childSku": "/path/to/prod/1/green/xs",
                                "size"    : "XS"
                            }
                        },
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/2",
                            "quantity": 10,
                            "price"   : 150,
                            "evars"   : {
                                "childSku": "/path/to/prod/2",
                                "size"    : ""
                            }
                        },
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/3",
                            "quantity": 2,
                            "price"   : 102,
                            "evars"   : {
                                "childSku": "/path/to/prod/3/m",
                                "size"    : "M"
                            }
                        }
                    ]
                },
                "componentPath": "commerce/components/submitorder"
            });
            CQ_Analytics.record({
                "event": ["discountRedemption"],
                "values": {
                    "discount": "/path/to/discount/1 - /path/to/discount/2",
                    "product" : [{
                        "category": "",
                        "sku"     : "Promotional Discount",
                        "events"  : {"discountRedemption": 20.00}
                    }]
                },
                "componentPath": "commerce/components/submitorder"
            });
            CQ_Analytics.record({
                "event": ["cartPurchase"],
                "values": {
                    "orderId"       : "00e40e2d-13a2-4a00-a8ee-01a9ebb0bf68",
                    "shippingMethod": "overnight",
                    "paymentMethod" : "Amex",
                    "billingState"  : "NY",
                    "billingZip"    : "10458",
                    "product"       : [{"category": "", "sku": "", "quantity": "", "price": ""}]
                },
                "componentPath": "commerce/components/submitorder"
            });
        }
        return true;
    }
</script>
```

#### Limitación del tamaño de las llamadas de seguimiento {#limiting-the-size-of-tracking-calls}

Generalmente, los exploradores Web limitan el tamaño de las solicitudes de GET. Debido a que los valores de SKU y producto de CQ son rutas de repositorio, las matrices de productos que incluyen varios valores pueden superar el límite de tamaño de la solicitud. Por lo tanto, los componentes deben limitar el número de elementos en la matriz `product` de cada `CQ_Analytics.record function`. Cree varias funciones si el número de elementos que necesita rastrear puede superar el límite.

Por ejemplo, el componente del subadministrador de comercio electrónico limita el número de `product` elementos de una llamada a cuatro. Cuando el carro de compras contiene más de cuatro productos, genera múltiples `CQ_Analytics.record` funciones.
