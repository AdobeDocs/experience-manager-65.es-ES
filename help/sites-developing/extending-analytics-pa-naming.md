---
title: Implementación de la nominación de páginas del lado del servidor para Analytics
seo-title: Implementación de la nominación de páginas del lado del servidor para Analytics
description: Adobe Analytics utiliza la propiedad s.pageName para identificar de forma exclusiva las páginas y asociar los datos recopilados para las páginas
seo-description: Adobe Analytics utiliza la propiedad s.pageName para identificar de forma exclusiva las páginas y asociar los datos recopilados para las páginas
uuid: 37b92099-0cce-4b2d-b55c-928f636dbd7e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: be2aa297-5b78-4b1d-8ff1-e6a585a177dd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Implementación de la nominación de páginas del lado del servidor para Analytics{#implementing-server-side-page-naming-for-analytics}

Adobe Analytics utiliza la `s.pageName` propiedad para identificar de forma exclusiva las páginas y asociar los datos recopilados para las páginas. Normalmente, se realizan las siguientes tareas en AEM para asignar un valor a esta propiedad que AEM envía a Analytics:

* Utilice el marco de servicios en la nube de Analytics para asignar una variable de CQ a la `s.pageName` propiedad de Analytics. (Consulte [Asignación de datos de componentes con propiedades](/help/sites-administering/adobeanalytics-mapping.md)de Adobe Analytics).

* Diseñe el componente de página para que incluya la variable de CQ que asigne a la `s.pageName` propiedad. (Consulte [Implementación del seguimiento de Adobe Analytics para componentes](/help/sites-developing/extending-analytics-components.md)personalizados).

Para exponer datos de informes de Analytics en la consola Sitios y en Content Insight, AEM requiere el valor de la propiedad de cada página `s.pageName` . La API de Java de AEM Analytics define la `AnalyticsPageNameProvider` interfaz que implementa para proporcionar a la consola Sitios y a Content Insights el valor de la `s.pageName` propiedad. El `AnaltyicsPageNameProvider` servicio resuelve la propiedad pageName en el servidor para la generación de informes, ya que se puede establecer dinámicamente mediante JavaScript en el cliente para fines de seguimiento.

## El servicio de proveedor de nombres de página de Analytics predeterminado {#the-default-analytics-page-name-provider-service}

El `DefaultPageNameProvider` servicio es el servicio predeterminado que determina el valor de la `s.pageName` propiedad que se utilizará para recuperar datos de Analytics para una página. El servicio funciona junto con el componente de página de base de AEM ( `/libs/foundation/components/page`). Este componente de página define las siguientes variables de CQ que se pretenden asignar a la `s.pageName` propiedad:

* `pagedata.path`:: El valor se establece en la ruta de la página.
* `pagedata.title`:: El valor se establece en el título de la página.
* `pagedata.navTitle`:: El valor se establece en el título de navegación de la página.

El `DefaultPageNameProvider` servicio determina qué variables de CQ se asignan a la `s.pageName` propiedad en el marco del servicio en la nube de Analytics. A continuación, el servicio determina la propiedad de página adecuada que se utilizará para recuperar datos de informes de análisis:

* `pagedata.path`:: El servicio utiliza `page.getPath()`

* `pagedata.title`:: El servicio utiliza `page.getTitle()`

* `pagedata.navTitle`:: El servicio utiliza `page.getNavigationTitle()`

El `page` objeto es el objeto es el [ objeto Java `com.day.cq.wcm.api.Page`](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) de la página.

Si no asigna una variable de CQ a la `s.pageName` propiedad en el marco, el valor de `s.pageName` se genera a partir de la ruta de la página. Por ejemplo, la página con la ruta `/content/geometrixx/en` utiliza el valor `content:geometrixx:en` para `s.pageName`.

>[!NOTE]
>
>El servicio DefaultPageNameProvider utiliza una clasificación de servicio de 100.

## Mantenimiento de la continuidad en los informes de Analytics {#maintaining-continuity-in-analytics-reporting}

El mantenimiento de un historial completo de datos de análisis para una página requiere que el valor de la propiedad s.pageName que se utiliza para una página nunca cambie. Sin embargo, las propiedades de análisis que define el componente de página de base se pueden cambiar fácilmente. Por ejemplo, al mover una página se cambia el valor de `pagedata.path` y se rompe la continuidad del historial de informes:

* Los datos recopilados para la ruta anterior ya no se asocian a la página.
* Si una página diferente utiliza la ruta que otra vez utilizó, la página diferente hereda los datos de esa ruta.

Para garantizar la continuidad de los informes, el valor de `s.pageName` debe tener las características siguientes:

* Única.
* Estable.
* legible para el ser humano.

Por ejemplo, un componente de página personalizado puede incluir una propiedad de página que los autores utilizan para especificar un ID único para la página que se utiliza como valor para la `s.pageProperties` propiedad:

* La página incluye una variable de análisis que se establece en el valor del ID único que se almacena en la propiedad page.
* La variable analytics se asigna a la `s.pageProperties` propiedad en el marco de Analytics.
* La implementación de la interfaz AnalyticsPageNameProvider recupera el valor de la propiedad page que se va a utilizar para consultar los datos de Analytics de la página.

>[!NOTE]
>
>Pida ayuda a su consultor de Analytics para desarrollar una estrategia eficaz para su `s.pageName` valor.

### Implementación de un servicio de proveedor de nombres de página de Analytics {#implementing-an-analytics-page-name-provider-service}

Implemente la `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider` interfaz como un servicio OSGi para personalizar la lógica que recupera el valor de la `s.pageName` propiedad. Los análisis de página Sitios y Content Insight utilizan el servicio para recuperar datos de informes de Analytics.

La interfaz AnalyticsPageNameProvider define dos métodos que debe implementar:

* `getPageName`:: Devuelve un `String` valor que representa el valor que se va a utilizar como `s.pageName` propiedad.

* `getResource`:: Devuelve un `org.apache.sling.api.resource.Resource` objeto que representa la página asociada a la `s.pageName` propiedad.

Ambos métodos toman un `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext` objeto como parámetro. La `AnalyticsPageNameContext` clase proporciona información sobre el contexto de las llamadas de análisis:

* Ruta base del recurso de página.
* El `Framework` objeto para la configuración del servicio en la nube de Analytics.
* El `Resource` objeto de la página.
* El `ResourceResolver` objeto de la página.

La clase también proporciona un establecedor para el nombre de la página.

### Ejemplo de implementación de AnalyticsPageNameProvider {#example-analyticspagenameprovider-implementation}

El siguiente ejemplo `AnalyticsPageNameProvider` de implementación admite un componente de página personalizado:

* El componente extiende el componente de página de base.
* El cuadro de diálogo incluye un campo que los autores utilizan para especificar el valor de la `s.pageName` propiedad.
* El valor de propiedad se almacena en la propiedad pageName del `jcr:content`nodo de las instancias de página.
* Se llama a la propiedad analytics que almacena la `s.pageName` propiedad `pagedata.pagename`. Esta propiedad está asignada a la `s.pageName` propiedad en el marco de Analytics.

La siguiente implementación del `getPageName` método devuelve el valor de la propiedad del nodo pageName si la asignación del marco está configurada correctamente:

```java
public String getPageName(AnalyticsPageNameContext context) {
        String pageName = null;

        Framework framework = context.getFramework();
        Resource resource = context.getResource();

        if (resource != null && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            Page page = resource.adaptTo(Page.class);
            if (cqVar.equals("pagedata.pagename")) {
                pageName = page.getProperties().get("pageName",null);
            }
        }
        return pageName;
    }
```

La siguiente implementación del método getResource devuelve el objeto Resource de la página:

```java
     public Resource getResource(AnalyticsPageNameContext context) {
        Resource res = null;

        Framework framework = context.getFramework();
        ResourceResolver resolver = context.getResourceResolver();
        String pageName = context.getPageName();
        String basePath = context.getBasePath();

        if (pageName != null && basePath != null && resolver != null
                && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            if (cqVar.equals("pagedata.pagename")) {
             Iterator<Resource>
             hits = resolver.findResources(createQuery(pageName, basePath, "pagename"), Query.JCR_SQL2);
             if (hits.hasNext()) {
              res = hits.next();
              res = res.getParent();
             }
            }
        }
        return res;
    }

    private String createQuery(String pageName, String basePath, String propName) {
        return "SELECT * FROM [cq:PageContent] WHERE ISDESCENDANTNODE(["
                + basePath + "]) and [" + propName + "] = \"" + pageName + "\"";
    }
```

El siguiente código representa toda la clase, incluidas las anotaciones de SCR que configuran el servicio. Tenga en cuenta que la clasificación de servicio es 200, lo que anula el servicio predeterminado.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2019 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.day.cq.analytics.sitecatalyst;

import java.util.Iterator;

import javax.jcr.query.Query;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;
import org.osgi.framework.Constants;
import org.osgi.service.component.annotations.Component;

import com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext;
import com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider;
import com.day.cq.analytics.sitecatalyst.Framework;
import com.day.cq.wcm.api.Page;

import static com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext.S_PAGE_NAME;

/**
 * Default implementation of {@link AnalyticsPageNameProvider} that resolves
 * page title, path or navTitle if mapped in {@link Framework}.
 */
@Component(
    service = { AnalyticsPageNameProvider.class },
    property = {
        Constants.SERVICE_DESCRIPTION + "=Example Page Name Resolver implementation",
        Constants.SERVICE_RANKING + ":Integer=200"
    }
)
public class ExamplePageNameProvider implements AnalyticsPageNameProvider {
    public String getPageName(AnalyticsPageNameContext context) {
        String pageName = null;

        Framework framework = context.getFramework();
        Resource resource = context.getResource();

        if (resource != null && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            Page page = resource.adaptTo(Page.class);
            if (cqVar.equals("pagedata.path")) {
                pageName = page.getProperties().get("pageName",null);
            }
        }
        return pageName;
    }

    public Resource getResource(AnalyticsPageNameContext context) {
        Resource res = null;

        Framework framework = context.getFramework();
        ResourceResolver resolver = context.getResourceResolver();
        String pageName = context.getPageName();
        String basePath = context.getBasePath();

        if (pageName != null && basePath != null && resolver != null
                && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            if (cqVar.equals("pagedata.pagename")) {
                Iterator<Resource>
                hits = resolver.findResources(createQuery(pageName, basePath, "pagename"), Query.JCR_SQL2);
                if (hits.hasNext()) {
                    res = hits.next();
                    res = res.getParent();
                }
            }
        }
        return res;
    }

    private String createQuery(String pageName, String basePath, String propName) {
        return "SELECT * FROM [cq:PageContent] WHERE ISDESCENDANTNODE(["
                + basePath + "]) and [" + propName + "] = \"" + pageName + "\"";
    }
}
```

