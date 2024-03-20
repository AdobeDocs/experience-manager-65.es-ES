---
title: Implementación de la nomenclatura de páginas del lado del servidor para Analytics
description: Adobe Analytics utiliza la propiedad s.pageName para identificar las páginas de forma exclusiva y asociar los datos recopilados para las páginas
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 17a4e4dc-804e-44a9-9942-c37dbfc8016f
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---

# Implementación de la nomenclatura de páginas del lado del servidor para Analytics{#implementing-server-side-page-naming-for-analytics}

Adobe Analytics utiliza el `s.pageName` para identificar las páginas de forma exclusiva y asociar los datos recopilados para las páginas. AEM AEM Normalmente, se realizan las siguientes tareas en la forma de asignar un valor a esta propiedad que se envía a Analytics de forma:

* Utilice el marco del servicio en la nube de Analytics para asignar una variable CQ a Analytics `s.pageName` propiedad. (Consulte [Asignación de datos de componente con propiedades de Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md).)

* Diseñe el componente de página para que incluya la variable CQ que asigne al `s.pageName` propiedad. (Consulte [Implementación del seguimiento de Adobe Analytics para componentes personalizados](/help/sites-developing/extending-analytics-components.md).)

AEM Para exponer los datos de los informes de Analytics en la consola Sitios y en la Perspectiva de contenido, se requiere el valor de la variable `s.pageName` para cada página. AEM La API de Java de Analytics de define lo siguiente `AnalyticsPageNameProvider` que implementa para proporcionar a la consola Sitios y a las Perspectivas de contenido el valor del `s.pageName` propiedad. Su `AnaltyicsPageNameProvider` resuelve la propiedad pageName en el servidor para la creación de informes, ya que se puede establecer dinámicamente mediante JavaScript en el cliente para la realización de seguimiento.

## El servicio de proveedor de nombres de páginas predeterminado de Analytics {#the-default-analytics-page-name-provider-service}

El `DefaultPageNameProvider` service es el servicio predeterminado que determina el valor de la variable `s.pageName` propiedad que se utilizará para recuperar los datos de Analytics de una página. AEM El servicio funciona junto con el componente de página de base de datos de ( `/libs/foundation/components/page`). Este componente de página define las siguientes variables de CQ que están pensadas para asignarse a `s.pageName` propiedad:

* `pagedata.path`: el valor se establece en la ruta de página.
* `pagedata.title`: el valor se establece en el título de la página.
* `pagedata.navTitle`: el valor se establece en el título de navegación de la página.

El `DefaultPageNameProvider` determina cuál de estas variables de CQ se asigna al `s.pageName` en el marco del servicio en la nube de Analytics. A continuación, el servicio determina la propiedad de página adecuada que se utilizará para recuperar los datos del informe de análisis:

* `pagedata.path`: El servicio utiliza `page.getPath()`

* `pagedata.title`: El servicio utiliza `page.getTitle()`

* `pagedata.navTitle`: El servicio utiliza `page.getNavigationTitle()`

El `page` el objeto es el es el [`com.day.cq.wcm.api.Page`](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) Objeto Java para la página.

Si no asigna una variable CQ al `s.pageName` en el marco de trabajo, el valor para `s.pageName` se genera a partir de la ruta de página. Por ejemplo, la página con la ruta `/content/geometrixx/en` utiliza el valor `content:geometrixx:en` para `s.pageName`.

>[!NOTE]
>
>El servicio DefaultPageNameProvider utiliza una clasificación de servicio de 100.

## Mantenimiento de la continuidad en informes de Analytics {#maintaining-continuity-in-analytics-reporting}

Para mantener un historial completo de los datos de análisis de una página, es necesario que el valor de la propiedad s.pageName que se utiliza para una página no cambie nunca. Sin embargo, las propiedades de análisis que define el componente de página de base se pueden cambiar fácilmente. Por ejemplo, mover una página cambia el valor de `pagedata.path` y rompe la continuidad del historial de informes:

* Los datos recopilados para la ruta anterior ya no están asociados con la página.
* Si una página diferente utiliza la ruta que otra página utilizó una vez, la página diferente hereda los datos de esa ruta.

Para garantizar la continuidad de los informes, el valor de `s.pageName` debe tener las siguientes características:

* Único.
* Estable.
* Legible en lenguaje natural.

Por ejemplo, un componente de página personalizado puede incluir una propiedad de página que los autores utilizan para especificar un ID único para la página que se utiliza como valor para `s.pageProperties` propiedad:

* La página incluye una variable de análisis que se establece en el valor del ID único almacenado en la propiedad de página.
* La variable de análisis está asignada a `s.pageProperties` en el marco de Analytics.
* La implementación de la interfaz AnalyticsPageNameProvider recupera el valor de la propiedad de página que se utilizará para consultar los datos de Analytics de la página.

>[!NOTE]
>
>Solicite ayuda a su consultor de Analytics para desarrollar una estrategia eficaz para su `s.pageName` valor.

### Implementación de un servicio de proveedor de nombres de páginas de Analytics {#implementing-an-analytics-page-name-provider-service}

Implementación de `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider` como un servicio OSGi para personalizar la lógica que recupera el `s.pageName` valor de propiedad. El análisis de página de Sites y la perspectiva de contenido utilizan el servicio para recuperar datos de informes de Analytics.

La interfaz AnalyticsPageNameProvider define dos métodos que debe implementar:

* `getPageName`: Devuelve un `String` valor que representa el valor que se va a utilizar como `s.pageName` propiedad.

* `getResource`: Devuelve un `org.apache.sling.api.resource.Resource` que representa la página asociada con el objeto `s.pageName` propiedad.

Ambos métodos toman una `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext` objeto como parámetro. El `AnalyticsPageNameContext` proporciona información sobre el contexto de las llamadas de analytics:

* Ruta base del recurso de página.
* El `Framework` para la configuración del servicio en la nube de Analytics.
* El `Resource` para la página.
* El `ResourceResolver` para la página.

La clase también proporciona un establecedor para el nombre de página.

### Ejemplo de implementación de AnalyticsPageNameProvider {#example-analyticspagenameprovider-implementation}

El siguiente ejemplo `AnalyticsPageNameProvider` la implementación admite un componente de página personalizado:

* El componente amplía el componente de página de base.
* El cuadro de diálogo incluye un campo que los autores utilizan para especificar el valor del `s.pageName` propiedad.
* El valor de la propiedad se almacena en la propiedad pageName del `jcr:content`nodo de las instancias de página.
* La propiedad de análisis que almacena el `s.pageName` se llama a la propiedad `pagedata.pagename`. Esta propiedad se asigna a la variable `s.pageName` en el marco de Analytics.

La siguiente implementación de la `getPageName` método devuelve el valor de la propiedad del nodo pageName si la asignación de marco de trabajo está configurada correctamente:

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

La implementación siguiente del método getResource devuelve el objeto Resource para la página:

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

El siguiente código representa toda la clase, incluidas las anotaciones SCR que configuran el servicio. La clasificación del servicio es 200, que anula el servicio predeterminado.

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
