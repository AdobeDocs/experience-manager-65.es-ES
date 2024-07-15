---
title: AEM Introducción a la extensión de para PWA Studio
description: AEM Obtenga información sobre cómo implementar un proyecto de Commerce y contenido sin encabezado de con PWA Studio.
topics: Commerce
feature: Commerce Integration Framework
exl-id: de7b8f05-b6b7-4105-84a5-940c16ebf2b4
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 0%

---

# AEM Introducción a la extensión de para PWA Studio {#getting-started-pwa}

De forma predeterminada, PWA Studio se integra perfectamente con Adobe Commerce a través de GraphQL, proporcionando opciones ilimitadas para crear tiendas innovadoras y atractivas y otras experiencias digitales.

Los fragmentos de contenido son fragmentos de contenido con una estructura predefinida que les permite consumirse sin encabezado utilizando GraphQL como API en diferentes formatos (por ejemplo, JSON, Markdown) y procesarse de forma independiente. Los fragmentos de contenido incluyen todos los tipos de datos y campos necesarios para que GraphQL garantice que la aplicación solo solicita lo que está disponible y recibe lo que se espera. La flexibilidad que proporcionan en términos de cómo están estructurados los hace perfectos para usarlos en varias ubicaciones y en varios canales.

Diseñar la estructura que necesita es fácil con el Editor del modelo de fragmentos de contenido dentro de Adobe Experience Manager. El principal desafío para la integración de fragmentos de contenido de Adobe Experience Manager (o cualquier otro dato) con la aplicación del PWA Studio es recuperar datos de varios extremos de GraphQL. El motivo es que, de forma predeterminada, PWA Studio funciona con un único punto de conexión de Adobe Commerce GraphQL.

## Arquitectura {#architecture}

![Arquitectura sin encabezado de PWA](/help/commerce/cif/assets/pwa-studio/PWA-Studio_Architecture.png)

## PWA Studio de instalación {#setup-pwa}

Para configurar la aplicación de PWA Studio, siga la [documentación de PWA Studio](https://developer.adobe.com/commerce/pwa-studio/tutorials/) de Adobe Commerce.

Para conectar el PWA Studio con el extremo de GraphQL AEM AEM de la, puede usar la extensión [para el PWA Studio ](https://github.com/adobe/aem-pwa-studio-extensions).

1. Desproteger el repositorio

1. En la aplicación PWA Studio, agregue la extensión como dependencia de desarrollo.

   ```javascript
   yarn add --dev file:{path-to-extension}/extension
   ```

1. Añada el envoltorio Apollo Link a la aplicación de PWA Studio. En pwa-root/src/index.js, realice los siguientes cambios:

   ```javascript
     import { linkWrapper } from '@adobe/pwa-studio-aem-cfm-blog-extension';
   
   // ...
   
   <Adapter apiBase={apiBase} apollo={{ link: linkWrapper(apolloLink) }} store={store}>
   ```

   Puede encontrar más detalles sobre la personalización del cliente Apollo en [linkWrapper.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/linkWrapper.js).

1. Para ampliar el componente de navegación con una entrada de blog, añada las siguientes adaptaciones a pwa-root/local-intercept.js:

   ```javascript
   const addBlogToNavigation = require('@adobe/pwa-studio-aem-cfm-blog-extension/src/addBlogToNavigation');
   
   function localIntercept(targets) {
       addBlogToNavigation(targets);
   }    
   ```

   Puede encontrar más detalles sobre la personalización del componente Navegación en [addBlogToNavigation.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/addBlogToNavigation.js) y en la documentación de [Extensibility Framework](https://developer.adobe.com/commerce/pwa-studio/guides/general-concepts/extensibility/) de PWA Studio.

1. AEM El cliente Apollo espera el extremo de GraphQL en `<https://pwa-studio/endpoint.js>`. Para asignar el extremo a esta ubicación, personalice la configuración UPWARD de la aplicación PWA Studio:
AEM a. Para `pwa-root/.env`, agregue la variable_CFM_GRAPHQL AEM y adáptela para que apunte a su punto de conexión de GraphQL Fragmentos de contenido de.

   AEM Ejemplo:_CFM_GRAPHQL=<http://localhost:4503/content/graphql/global>

   b. Añada una resolución proxy a la configuración UPWARD. Una configuración de muestra ASCENDENTE podría tener este aspecto:

```json
   response:
     resolver: conditional
     when:
       - matches: request.url.pathname
         pattern: ^/endpoint.json(/|$)
         use: aemProxy
     default: veniaResponse

   aemProxy:
     resolver: proxy
     target: env.AEM_CFM_GRAPHQL
     ignoreSSLErrors: true

   status: response.status
   headers: response.headers
   body: response.body
```

## AEM Configuración de {#setup-aem}

AEM Siga la documentación de Fragmentos de contenido de para configurar un punto final de GraphQL AEM para su proyecto de AppMeasurement. AEM Además, en el proyecto de, agregue las siguientes configuraciones para permitir que la aplicación de PWA Studio acceda al extremo de GraphQL:

* Política de uso compartido de recursos de origen cruzado de Adobe Granite (com.adobe.granite.cors.impl.CORSPolicyImpl)

  Establezca la propiedad `allowedorigin` en el nombre de host completo de su aplicación de PWA.

  Ejemplo: `<https://pwa-studio-test-vflyn.local.pwadev:9366>`

* Filtro de referente de Apache Sling (org.apache.sling.security.impl.ReferrerFilter.cfg.json)

  Establezca la propiedad allow.hosts en el nombre de host de la aplicación PWA.

  Ejemplo: pwa-studio-test-vflyn.local.pwadev

Puede encontrar ejemplos completos de ambas configuraciones aquí: <https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension/aem/config/src/main/content/jcr_root/apps/blog-demo/config>.

Para mostrar el punto final de GraphQL, Adobe preparó algunos modelos y datos de fragmentos de contenido de muestra mediante un paquete de contenido. Estas piezas funcionan junto con los componentes React proporcionados con la extensión PWA Studio.

## Usos {#how-to-use}

Esta extensión se considera una implementación de ejemplo de cómo conectar una aplicación PWA Studio AEM con la que se ha creado un vínculo para recuperar y procesar contenido a través de GraphQL.

Según el caso de uso, desea crear sus propios modelos de fragmento de contenido personalizados, que resultan en un esquema de GraphQL personalizado que luego pueden consumir sus propios componentes de React.

Las configuraciones de producción pueden variar en varios aspectos.

* Puede tener un único extremo de GraphQL AEM federado que combine datos de GraphQL de Adobe Commerce y de la aplicación de datos de la aplicación de datos en lugar de personalizar el cliente de Apollo.
* La aplicación de PWA Studio AEM podría utilizar la URL de extremo de GraphQL de la directamente, sin un proxy con UPWARD. El proxy también se puede mover a una capa diferente (por ejemplo, CDN).
* El enfoque que mejor se adapte a sus necesidades también depende en gran medida de cómo entregue la aplicación PWA Studio al usuario final.

Esta extensión incluye dos ejemplos.

### Blog {#blog}

Mostrar publicaciones de blog basadas en algunos modelos de fragmentos de contenido. AEM Además, contiene ejemplos de cómo configurar el cliente Apollo para que funcione con el punto de conexión de GraphQL de y cómo ampliar el componente de navegación en PWA Studio. Consulte [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension) para obtener más información.

### Enriquecimiento de PDP {#pdp-enrichment}

Permite a los especialistas en marketing enriquecer fácilmente los PDP con contenido adicional que se administra como fragmentos de contenido. Consulte [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cif-product-page-extension) para obtener más información.
