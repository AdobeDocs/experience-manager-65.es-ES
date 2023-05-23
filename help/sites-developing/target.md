---
title: Desarrollo de contenido de destino
seo-title: Developing for Targeted Content
description: Temas sobre el desarrollo de componentes para su uso con la segmentación de contenido
seo-description: Topics about developing components for use with content targeting
uuid: 2449347e-7e1c-427b-a5b0-561055186934
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: bff078cd-c390-4870-ad1d-192807c67ca4
docset: aem65
exl-id: 92b62532-4f79-410d-903e-d2bca6d0fd1c
source-git-commit: fb9363a39ffc9d3929a31a3a19a124b806607ef4
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 3%

---

# Desarrollo de contenido de destino{#developing-for-targeted-content}

En esta sección se describen temas sobre el desarrollo de componentes para utilizarlos en la segmentación de contenido.

* Para obtener información sobre cómo conectar con Adobe Target, consulte [Integración Con Adobe Target](/help/sites-administering/target.md).
* Para obtener información sobre la creación de contenido de destino, consulte [Creación de contenido segmentado mediante el modo de segmentación](/help/sites-authoring/content-targeting-touch.md).

>[!NOTE]
>
>Cuando se marca un componente como objetivo en el autor AEM, este realiza una serie de llamadas del lado del servidor a Adobe Target para registrar la campaña, configurar ofertas y recuperar segmentos de Adobe Target (si están configurados). No se realizan llamadas del lado del servidor desde publicaciones de AEM a Adobe Target.

## Activación de la segmentación con Adobe Target en las páginas {#enabling-targeting-with-adobe-target-on-your-pages}

Para utilizar componentes de destino en las páginas que interactúen con Adobe Target, incluya código específico del lado del cliente en la variable &lt;head> Elemento.

### La sección de cabecera {#the-head-section}

Agregue ambos de los siguientes bloques de código al &lt;head> de la página:

```xml
<!--/* Include Context Hub */-->
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

```xml
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
```

Este código añade los objetos JavaScript de Analytics necesarios y carga las bibliotecas del servicio en la nube asociadas al sitio web. Para el servicio Target, las bibliotecas se cargan mediante `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

El conjunto de bibliotecas cargadas depende del tipo de biblioteca de cliente de Target (mbox.js o at.js) que se use en la configuración de Target:

**Para mbox.js predeterminado**

```
<script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/mbox.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/personalization/integrations/commons.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/util.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/init.js"></script>
```

**Para mbox.js personalizado**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/mbox.js"></script>
        <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/personalization/integrations/commons.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/util.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/init.js"></script>
```

**Para at.js**

```
<script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs.js"></script>
```

>[!NOTE]
>
>Solo la versión de `at.js` enviado con el producto es compatible. La versión de `at.js` enviado con el producto se puede obtener mirando el `at.js` archivo en ubicación:
>
>**/libs/cq/testandtarget/clientlibs/testandtarget/atjs/source/at.js**.

**Para at.js personalizado**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/at.js"></script>
    <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
```

La funcionalidad de Target en el lado del cliente se administra mediante `CQ_Analytics.TestTarget` objeto. Por lo tanto, la página contendrá código de inicialización como en el siguiente ejemplo:

```
<script type="text/javascript">
            if ( !window.CQ_Analytics ) {
                window.CQ_Analytics = {};
            }
            if ( !CQ_Analytics.TestTarget ) {
                CQ_Analytics.TestTarget = {};
            }
            CQ_Analytics.TestTarget.clientCode = 'my_client_code';
        </script>
      ...

    <div class="cloudservice testandtarget">
  <script type="text/javascript">
  CQ_Analytics.TestTarget.maxProfileParams = 11;

  if (CQ_Analytics.CCM) {
   if (CQ_Analytics.CCM.areStoresInitialized) {
    CQ_Analytics.TestTarget.registerMboxUpdateCalls();
   } else {
    CQ_Analytics.CCM.addListener("storesinitialize", function (e) {
     CQ_Analytics.TestTarget.registerMboxUpdateCalls();
    });
   }
  } else {
   // client context not there, still register calls
   CQ_Analytics.TestTarget.registerMboxUpdateCalls();
  }
  </script>
 </div>
```

El JSP añade los objetos de JavaScript de análisis necesarios y las referencias a las bibliotecas de JavaScript del lado del cliente. El archivo testandtarget.js contiene las funciones mbox.js. El HTML que genera el script es similar al siguiente ejemplo:

```xml
<script type="text/javascript">
        if ( !window.CQ_Analytics ) {
            window.CQ_Analytics = {};
        }
        if ( !CQ_Analytics.TestTarget ) {
            CQ_Analytics.TestTarget = {};
        }
        CQ_Analytics.TestTarget.clientCode = 'MyClientCode';
</script>
<link rel="stylesheet" href="/etc/clientlibs/foundation/testandtarget/testandtarget.css" type="text/css">
<script type="text/javascript" src="/etc/clientlibs/foundation/testandtarget/testandtarget.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/testandtarget/init.js"></script>
```

#### El cuerpo Sección (inicio) {#the-body-section-start}

Agregue el siguiente código inmediatamente después de &lt;body> para añadir las funciones de Client Context a la página:

```xml
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

#### Sección del cuerpo (final) {#the-body-section-end}

Agregue el siguiente código inmediatamente antes de la variable &lt;/body> etiqueta final:

```xml
<cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
```

El script JSP de este componente genera llamadas a la API de JavaScript de Target e implementa otras configuraciones necesarias. El HTML que genera el script es similar al siguiente ejemplo:

```xml
<div class="servicecomponents cloudservices">
  <div class="cloudservice testandtarget">
    <script type="text/javascript">
      CQ_Analytics.TestTarget.maxProfileParams = 11;
      CQ_Analytics.CCM.addListener("storesinitialize", function(e) {
        CQ_Analytics.TestTarget.registerMboxUpdateCalls();
      });
    </script>
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
</div>
```

### Uso de un archivo de biblioteca de Target personalizado {#using-a-custom-target-library-file}

>[!NOTE]
>
>Si no utiliza DTM u otro sistema de marketing de destino, puede utilizar archivos de biblioteca de destino personalizados.

>[!NOTE]
>
>De forma predeterminada, los mboxes están ocultos: la clase mboxDefault determina este comportamiento. Al ocultar los mboxes, se asegura de que los visitantes no vean el contenido predeterminado antes de cambiarlo; sin embargo, ocultar los mboxes afecta al rendimiento percibido.

El archivo mbox.js predeterminado que se usa para crear mboxes se encuentra en /etc/clientlibs/foundation/testandtarget/mbox/source/mbox.js. Para utilizar un archivo mbox.js de cliente, agregue el archivo a la configuración de la nube de Target. Para agregar el archivo, el archivo mbox.js debe estar disponible en el sistema de archivos.

Por ejemplo, si desea utilizar la variable [Servicio de ID de Marketing Cloud](https://experienceleague.adobe.com/docs/id-service/using/home.html) debe descargar mbox.js para que contenga el valor correcto para `imsOrgID` , que se basa en su inquilino. Esta variable es necesaria para integrar con el servicio de ID de Marketing Cloud. Para obtener más información, consulte [Adobe Analytics como fuente de informes para Adobe Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) y [Antes de la implementación](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html).

>[!NOTE]
>
>Si se define un mbox personalizado en una configuración de Target, todos deben tener acceso de lectura a **/etc/cloudservices** en servidores de publicación. Sin este acceso, la carga de archivos mbox.js en el sitio web de publicación provoca un error 404.

1. Vaya al CQ **Herramientas** página y seleccione **Cloud Services**. ([https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html))
1. En el árbol, seleccione Adobe Target y, en la lista de configuraciones, haga doble clic en la configuración de Target.
1. En la página de configuración, haga clic en Editar.
1. Para la propiedad mbox.js personalizada, haga clic en Examinar y seleccione el archivo.
1. Para aplicar los cambios, introduzca la contraseña de su cuenta de Adobe Target, haga clic en Volver a conectar con Target y en Aceptar cuando la conexión se haya realizado correctamente. A continuación, haga clic en Aceptar en el cuadro de diálogo Editar componente.

La configuración de Target incluye un archivo mbox.js personalizado, [el código requerido en la sección head](/help/sites-developing/target.md#p-the-head-section-p) de la página agrega el archivo al marco de trabajo de la biblioteca de cliente en lugar de una referencia a la biblioteca testandtarget.js.

## Desactivación del comando de Target para componentes {#disabling-the-target-command-for-components}

La mayoría de los componentes se pueden convertir en componentes de destino mediante el comando Objetivo del menú contextual.

![chlimage_1-21](assets/chlimage_1-21.png)

Para quitar el comando Target del menú contextual, agregue la siguiente propiedad al nodo cq:editConfig del componente:

* Nombre: cq:disableTargeting
* Tipo: booleano
* Valor: True

Por ejemplo, para deshabilitar el direccionamiento para los componentes de título de las páginas del sitio de demostración de Geometrixx, agregue la propiedad al nodo /apps/geometrixx/components/title/cq:editConfig.

![chlimage_1-22](assets/chlimage_1-22.png)

## Envío de información de confirmación de pedido a Adobe Target {#sending-order-confirmation-information-to-adobe-target}

>[!NOTE]
>
>Si no utiliza la DTM, envía una confirmación de pedido a Adobe Target.

Para realizar un seguimiento del rendimiento del sitio web, envíe información de compra desde la página de confirmación de pedido a Adobe Target. (Consulte [Crear un mbox orderConfirmPage](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager/?lang=en) y [Mbox de confirmación de pedido: añada parámetros personalizados.](https://experienceleaguecommunities.adobe.com/t5/adobe-target-questions/order-confirmation-mbox-add-custom-parameters/m-p/275779)) Adobe Target reconoce los datos de mbox como datos de confirmación de pedido cuando su nombre de mbox es `orderConfirmPage` y utiliza los siguientes nombres de parámetro específicos:

* productPurchasedId: Una lista de ID que identifican los productos comprados.
* orderId: ID del pedido.
* orderTotal: El importe total de la compra.

El código de la página del HTML procesado que crea el mbox es similar al siguiente ejemplo:

```xml
<script type="text/javascript">
     mboxCreate('orderConfirmPage',
     'productPurchasedId=product1 product2 product3',
     'orderId=order1234',
     'orderTotal=24.54');
</script>
```

Los valores de cada parámetro son diferentes para cada orden. Por lo tanto, necesita un componente que genere el código en función de las propiedades de la compra. El CQ [eCommerce Integration Framework](/help/commerce/cif-classic/administering/ecommerce.md) le permite integrar con su catálogo de productos e implementar un carro de compras y una página de cierre de compra.

El ejemplo de Geometrixx Outdoors muestra la siguiente página de confirmación cuando un visitante compra productos:

![chlimage_1-23](assets/chlimage_1-23.png)

El siguiente código para el script JSP de un componente accede a las propiedades del carro de compras y, a continuación, imprime el código para crear el mbox.

```java
<%--

  confirmationmbox component.

--%><%
%><%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false"
          import="com.adobe.cq.commerce.api.CommerceService,
                  com.adobe.cq.commerce.api.CommerceSession,
                  com.adobe.cq.commerce.common.PriceFilter,
                  com.adobe.cq.commerce.api.Product,
                  java.util.List, java.util.Iterator"%><%

/* obtain the CommerceSession object */
CommerceService commerceservice = resource.adaptTo(CommerceService.class);
CommerceSession session = commerceservice.login(slingRequest, slingResponse);

/* obtain the cart items */
List<CommerceSession.CartEntry> entries = session.getCartEntries();
Iterator<CommerceSession.CartEntry> cartiterator = entries.iterator();

/* iterate the items and get the product IDs */
String productIDs = new String();
while(cartiterator.hasNext()){
 CommerceSession.CartEntry entry = cartiterator.next();
 productIDs = productIDs + entry.getProduct().getSKU();
    if (cartiterator.hasNext()) productIDs = productIDs + ", ";
}

/* get the cart price and orderID */
String total = session.getCartPrice(new PriceFilter("CART", "PRE_TAX"));
String orderID = session.getOrderId();

%><div class="mboxDefault"></div>
<script type="text/javascript">
     mboxCreate('orderConfirmPage',
     'productPurchasedId=<%= productIDs %>',
     'orderId=<%= orderID %>',
     'orderTotal=<%= total %>');
</script>
```

Cuando el componente se incluye en la página de cierre de compra del ejemplo anterior, el origen de página incluye la siguiente secuencia de comandos que crea el mbox:

```
<div class="mboxDefault"></div>
<script type="text/javascript">

     mboxCreate('orderConfirmPage',
     'productPurchasedId=47638-S, 46587',
     'orderId=d03cb015-c30f-4bae-ab12-1d62b4d105ca',
     'orderTotal=US$677.00');

</script>
```

## Explicación del componente Target {#understanding-the-target-component}

El componente Target permite a los autores crear mboxes dinámicos a partir de componentes de contenido de CQ. (Consulte [Segmentación de contenido](/help/sites-authoring/content-targeting-touch.md).) El componente Target se encuentra en /libs/cq/personalization/components/target.

El script target.jsp accede a las propiedades de página para determinar el motor de segmentación que se utilizará para el componente y, a continuación, ejecuta el script adecuado:

* Adobe Target: /libs/cq/personalization/components/target/engine_tnt.jsp
* [Adobe Target con AT.JS](/help/sites-administering/target.md): /libs/cq/personalization/components/target/engine_atjs.jsp
* [Adobe Campaign](/help/sites-authoring/target-adobe-campaign.md): /libs/cq/personalization/components/target/engine_cq_campaign.jsp
* Reglas de cliente/ContextHub: /libs/cq/personalization/components/target/engine_cq.jsp

### La creación de mboxes {#the-creation-of-mboxes}

>[!NOTE]
>
>De forma predeterminada, los mboxes están ocultos: la clase mboxDefault determina este comportamiento. Al ocultar los mboxes, se asegura de que los visitantes no vean el contenido predeterminado antes de cambiarlo; sin embargo, ocultar los mboxes afecta al rendimiento percibido.

Cuando Adobe Target administra la segmentación de contenido, el script engine_tnt.jsp crea mboxes que contienen el contenido de la experiencia de destino:

* Agrega un `div` con la clase de `mboxDefault`, según lo requerido por la API de Adobe Target.

* Añade el contenido de mbox (el contenido de la experiencia segmentada) dentro de la variable `div` Elemento.

Siguiendo las `mboxDefault` div, se inserta el javascript que crea el mbox:

* El nombre, el ID y la ubicación del mbox se basan en la ruta del repositorio del componente.
* La secuencia de comandos obtiene los nombres y valores de los parámetros de Client Context.
* Se realizan llamadas a las funciones que mbox.js y otras bibliotecas de cliente definen para crear mboxes.

#### Bibliotecas de cliente para la segmentación de contenido {#client-libraries-for-content-targeting}

Las siguientes son las categorías clientlib disponibles:

* testandtarget.mbox
* testandtarget.init
* testandtarget.util
* testandtarget.atjs
* testandtarget.atjs-integration
