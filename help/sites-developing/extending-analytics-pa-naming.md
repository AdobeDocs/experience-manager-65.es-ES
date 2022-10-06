---
title: Implementación de la nomenclatura de páginas del lado del servidor para Analytics
seo-title: Implementing Server-Side Page Naming for Analytics
description: Adobe Analytics utiliza la propiedad s.pageName para identificar páginas de forma única y asociar los datos recopilados para las páginas
seo-description: Adobe Analytics uses the s.pageName property to uniquely identify pages and to associate the data that is collected for the pages
uuid: 37b92099-0cce-4b2d-b55c-928f636dbd7e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: be2aa297-5b78-4b1d-8ff1-e6a585a177dd
exl-id: 17a4e4dc-804e-44a9-9942-c37dbfc8016f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 0%

---

# Implementación de la nomenclatura de páginas del lado del servidor para Analytics{#implementing-server-side-page-naming-for-analytics}

Adobe Analytics utiliza la variable `s.pageName` para identificar páginas de forma única y asociar los datos recopilados para las páginas. Normalmente, se realizan las siguientes tareas en AEM para asignar un valor a esta propiedad que AEM envía a Analytics:

* Utilice el marco de servicios en la nube de Analytics para asignar una variable de CQ a Analytics `s.pageName` propiedad. (Consulte [Asignación de datos de componente con propiedades de Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md).)

* Diseñe el componente de página de modo que incluya la variable de CQ que asigne al `s.pageName` propiedad. (Consulte [Implementación del seguimiento de Adobe Analytics para componentes personalizados](/help/sites-developing/extending-analytics-components.md).)

Para exponer los datos de informes de Analytics en la consola Sitios y en la perspectiva de contenido, AEM requiere el valor de la variable `s.pageName` para cada página. La API Java de AEM Analytics define la variable `AnalyticsPageNameProvider` interfaz que implementa para proporcionar la consola Sitios y Perspectivas de contenido con el valor de la variable `s.pageName` propiedad. Su `AnaltyicsPageNameProvider` resuelve la propiedad pageName en el servidor con fines de creación de informes, ya que se puede establecer de forma dinámica utilizando JavaScript en el cliente con fines de seguimiento.

## El servicio de proveedor de nombres de página predeterminado de Analytics {#the-default-analytics-page-name-provider-service}

La variable `DefaultPageNameProvider` es el servicio predeterminado que determina el valor de la variable `s.pageName` propiedad que se utilizará para recuperar datos de Analytics para una página. El servicio funciona junto con el componente de la página de base de AEM ( `/libs/foundation/components/page`). Este componente de página define las siguientes variables de CQ que están destinadas a ser asignadas al `s.pageName` propiedad:

* `pagedata.path`: El valor se establece en la ruta de la página.
* `pagedata.title`: El valor se establece en el título de la página.
* `pagedata.navTitle`: El valor se establece en el título de navegación de la página.

La variable `DefaultPageNameProvider` determina cuál de estas variables de CQ está asignada al `s.pageName` en el marco de servicios de nube de Analytics. A continuación, el servicio determina la propiedad de página adecuada que se utilizará para recuperar datos de informes de Analytics:

* `pagedata.path`: El servicio utiliza `page.getPath()`

* `pagedata.title`: El servicio utiliza `page.getTitle()`

* `pagedata.navTitle`: El servicio utiliza `page.getNavigationTitle()`

La variable `page` es que la variable [ `com.day.cq.wcm.api.Page`](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) Objeto Java de la página.

Si no asigna una variable de CQ a la variable `s.pageName` en el marco, el valor de `s.pageName` se genera a partir de la ruta de página. Por ejemplo, la página con la ruta `/content/geometrixx/en` utiliza el valor `content:geometrixx:en` para `s.pageName`.

>[!NOTE]
>
>El servicio DefaultPageNameProvider utiliza una clasificación de servicio de 100.

## Mantenimiento de la continuidad en los informes de Analytics {#maintaining-continuity-in-analytics-reporting}

Para mantener un historial completo de datos de análisis para una página, es necesario que el valor de la propiedad s.pageName que se utiliza para una página nunca cambie. Sin embargo, las propiedades de análisis que define el componente de la página base se pueden cambiar fácilmente. Por ejemplo, al mover una página, se cambia el valor de `pagedata.path` y rompe la continuidad del historial de informes:

* Los datos recopilados para la ruta anterior ya no están asociados a la página.
* Si una página diferente utiliza la ruta que otra página usó una vez, la página diferente hereda los datos de esa ruta.

Para garantizar la continuidad de los informes, el valor de `s.pageName` deben tener las siguientes características:

* Única.
* Estable.
* Legible para el ser humano.

Por ejemplo, un componente de página personalizado puede incluir una propiedad de página que los autores utilizan para especificar un ID único para la página que se utiliza como valor para la variable `s.pageProperties` propiedad:

* La página incluye una variable de análisis que se establece en el valor del ID exclusivo que se almacena en la propiedad de página.
* La variable de análisis está asignada a la variable `s.pageProperties` en el marco de Analytics.
* La implementación de la interfaz AnalyticsPageNameProvider recupera el valor de la propiedad page que se utiliza para consultar los datos de Analytics de la página.

>[!NOTE]
>
>Solicite ayuda a su consultor de Analytics para desarrollar una estrategia eficaz para su `s.pageName` valor.

### Implementación de un servicio de proveedor de nombres de página de Analytics {#implementing-an-analytics-page-name-provider-service}

Implementación de `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider` como servicio OSGi para personalizar la lógica que recupera el `s.pageName` valor de propiedad. El análisis de páginas de Sitios y la perspectiva de contenido utilizan el servicio para recuperar datos de informes de Analytics.

La interfaz AnalyticsPageNameProvider define dos métodos que debe implementar:

* `getPageName`: Devuelve un `String` que representa el valor que se va a usar como el `s.pageName` propiedad.

* `getResource`: Devuelve un `org.apache.sling.api.resource.Resource` objeto que representa la página asociada con la variable `s.pageName` propiedad.

Ambos métodos tienen una `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext` como parámetro. La variable `AnalyticsPageNameContext` proporciona información sobre el contexto de las llamadas de analytics:

* Ruta base del recurso de página.
* La variable `Framework` para la configuración del servicio en la nube de Analytics.
* La variable `Resource` para la página.
* La variable `ResourceResolver` para la página.

La clase también proporciona un separador para el nombre de página.

### Ejemplo de implementación de AnalyticsPageNameProvider {#example-analyticspagenameprovider-implementation}

El siguiente ejemplo `AnalyticsPageNameProvider` la implementación admite un componente de página personalizado:

* El componente amplía el componente de página base.
* El cuadro de diálogo incluye un campo que los autores utilizan para especificar el valor de la variable `s.pageName` propiedad.
* El valor de la propiedad se almacena en la propiedad pageName del `jcr:content`de las instancias de página.
* La propiedad de análisis que almacena el `s.pageName` se llama a la propiedad `pagedata.pagename`. Esta propiedad está asignada al `s.pageName` en el marco de Analytics.

La siguiente implementación de `getPageName` devuelve el valor de la propiedad del nodo pageName si la asignación de marco está configurada correctamente:

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

El siguiente código representa toda la clase, incluidas las anotaciones SCR que configuran el servicio. Tenga en cuenta que la clasificación del servicio es 200, lo que anula el servicio predeterminado.

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
