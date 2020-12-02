---
title: Creación de extensiones personalizadas
seo-title: Creación de extensiones personalizadas
description: Puede llamar su código personalizado en Adobe Campaign desde AEM o desde AEM a Adobe Campaign
seo-description: Puede llamar su código personalizado en Adobe Campaign desde AEM o desde AEM a Adobe Campaign
uuid: 8392aa0d-06cd-4b37-bb20-f67e6a0550b1
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: f536bcc1-7744-4f05-ac6a-4cec94a1ffb6
translation-type: tm+mt
source-git-commit: 06f1f753b9bb7f7336454f166e03f753e3735a16
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 2%

---


# Creación de extensiones personalizadas{#creating-custom-extensions}

Generalmente, al implementar un proyecto, tiene código personalizado tanto en AEM como en Adobe Campaign. Con el uso de la API existente, puede llamar a su código personalizado en Adobe Campaign desde AEM o desde AEM hasta Adobe Campaign. Este documento describe cómo hacerlo.

## Requisitos previos {#prerequisites}

Debe tener instalado lo siguiente:

* Adobe Experience Manager
* Adobe Campaign 6.1

Consulte [Integración de AEM con Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md) para obtener más información.

## Ejemplo 1: AEM a Adobe Campaign {#example-aem-to-adobe-campaign}

La integración estándar entre AEM y Campaña se basa en JSON y JSSP (JavaScript Server Page). Estos archivos JSSP se pueden encontrar en la consola de Campaña y en todos los inicios con **amc** (Adobe Marketing Cloud).

![chlimage_1-15](assets/chlimage_1-15a.png)

>[!NOTE]
>
>[Para este ejemplo, consulte Geometrixx](/help/sites-developing/we-retail.md), que está disponible en Uso compartido de paquetes.

En este ejemplo, creamos un nuevo archivo JSSP personalizado y lo llamamos desde el lado AEM para recuperar el resultado. Esto se puede utilizar, por ejemplo, para recuperar datos de Adobe Campaign o para guardar datos en Adobe Campaign.

1. En Adobe Campaign, para crear un nuevo archivo JSSP, haga clic en el icono **Nuevo**.

   ![](do-not-localize/chlimage_1-4a.png)

1. Escriba el nombre de este archivo JSSP. En este ejemplo, utilizamos **cus:custom.jssp** (lo que significa que estará en la Área de nombres **cus**).

   ![chlimage_1-16](assets/chlimage_1-16a.png)

1. Coloque el siguiente código dentro del archivo jssp:

   ```
   <%
   var origin = request.getParameter("origin");
   document.write("Hello from Adobe Campaign, origin : " + origin);
   %>
   ```

1. Guarde su trabajo. El trabajo restante está en AEM.
1. Cree un servlet simple en el lado AEM para llamar a este JSSP. En este ejemplo, suponemos lo siguiente:

   * Tiene la conexión funcionando entre AEM y Campaña
   * El servicio de nube de campaña está configurado en **/content/geometrixx-outdoors**

   El objeto más importante de este ejemplo es **GenericCampaignConnector**, que le permite llamar (obtener y publicar) archivos jssp en el lado de Adobe Campaign.

   Este es un pequeño fragmento de código:

   ```
   @Reference
   private GenericCampaignConnector campaignConnector;
   ...
   Map<String, String> params = new HashMap<String, String>();
   params.put("origin", "AEM");
   CallResults results = campaignConnector.callGeneric("/jssp/cus/custom.jssp", params, credentials);
   return results.bodyAsString();
   ```

1. Como puede ver en este ejemplo, debe pasar las credenciales a la llamada. Esto se puede obtener mediante el método getCredentials(), donde se pasa una página que tiene configurado el servicio de nube de Campañas.

   ```xml
   // page containing the cloudservice for Adobe Campaign
   Configuration config = campaignConnector.getWebserviceConfig(page.getContentResource().getParent());
   CampaignCredentials credentials = campaignConnector.retrieveCredentials(config);
   ```

El código completo es el siguiente:

```java
import java.io.IOException;
import java.io.PrintWriter;
import java.util.HashMap;
import java.util.Map;

import javax.servlet.ServletException;

import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.sling.SlingServlet;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.SlingHttpServletResponse;
import org.apache.sling.api.servlets.SlingSafeMethodsServlet;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.mcm.campaign.CallResults;
import com.day.cq.mcm.campaign.CampaignCredentials;
import com.day.cq.mcm.campaign.GenericCampaignConnector;
import com.day.cq.wcm.api.Page;
import com.day.cq.wcm.api.PageManager;
import com.day.cq.wcm.api.PageManagerFactory;
import com.day.cq.wcm.webservicesupport.Configuration;

@SlingServlet(paths="/bin/campaign", methods="GET")
public class CustomServlet extends SlingSafeMethodsServlet {

 private final Logger log = LoggerFactory.getLogger(this.getClass());

 @Reference
 private GenericCampaignConnector campaignConnector;

 @Reference
 private PageManagerFactory pageManagerFactory;

 @Override
 protected void doGet(SlingHttpServletRequest request,
   SlingHttpServletResponse response) throws ServletException,
   IOException {

  PageManager pm = pageManagerFactory.getPageManager(request.getResourceResolver());

  Page page = pm.getPage("/content/geometrixx-outdoors");

  String result = null;
  if ( page != null) {
   result = callCustomFunction(page);
  }
  if ( result != null ) {
   PrintWriter pw = response.getWriter();
   pw.print(result);
  }
 }

 private String callCustomFunction(Page page ) {
  try {
   Configuration config = campaignConnector.getWebserviceConfig(page.getContentResource().getParent());
   CampaignCredentials credentials = campaignConnector.retrieveCredentials(config);

   Map<String, String> params = new HashMap<String, String>();
   params.put("origin", "AEM");
   CallResults results = campaignConnector.callGeneric("/jssp/cus/custom.jssp", params, credentials);
   return results.bodyAsString();
  } catch (Exception e ) {
   log.error("Something went wrong during the connection", e);
  }
  return null;

 }

}
```

## Ejemplo 2: Adobe Campaign para AEM {#example-adobe-campaign-to-aem}

AEM ofertas de las API integradas para recuperar los objetos disponibles en cualquier parte de la vista de SiteAdmin Explorer.

![chlimage_1-17](assets/chlimage_1-17a.png)

>[!NOTE]
>
>[Para este ejemplo, consulte Geometrixx](/help/sites-developing/we-retail.md), que está disponible en Uso compartido de paquetes.

Para cada nodo del explorador hay una API vinculada a él. Por ejemplo, para el nodo:

* [http://localhost:4502/siteadmin#/content/campaigns/geometrixx/scott-recommends](http://localhost:4502/siteadmin#/content/campaigns/geometrixx/scott-recommends)

la API es:

* [http://localhost:4502/content/campaigns/geometrixx/scott-recommends.1.json](http://localhost:4502/content/campaigns/geometrixx/scott-recommends.2.json)

El final de la dirección URL **.1.json** se puede reemplazar por **.2.json**, **.3.json**, según el número de subniveles que le interese obtener Para obtener todos ellos, se puede utilizar la palabra clave **infinito**:

* [http://localhost:4502/content/campaigns/geometrixx/scott-recommends.infinity.json](http://localhost:4502/content/campaigns/geometrixx/scott-recommends.2.json)

Ahora, para consumir la API, debemos saber que AEM, de forma predeterminada, utiliza la autenticación básica.

Una biblioteca JS con el nombre **amcIntegration.js** está disponible en 6.1.1 (compilación 8624 y posterior) que implementa esa lógica entre otras.

### Llamada de API de AEM {#aem-api-call}

```java
loadLibrary("nms:amcIntegration.js");

var cmsAccountId = sqlGetInt("select iExtAccountId from NmsExtAccount where sName=$(sz)","aemInstance")
var cmsAccount = nms.extAccount.load(String(cmsAccountId));
var cmsServer = cmsAccount.server;

var request = new HttpClientRequest(cmsServer+"/content/campaigns/geometrixx.infinity.json")
aemAddBasicAuthentication(cmsAccount, request);
request.method = "GET"
request.header["Content-Type"] = "application/json; charset=UTF-8";
request.execute();
var response = request.response;
```

