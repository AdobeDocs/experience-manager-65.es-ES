---
title: Introducción a AEM Extension for PWA Studio
description: Obtenga información sobre cómo implementar un proyecto de Contenido y comercio AEM sin encabezado con PWA Studio.
topics: Commerce
feature: Marco de integración de Commerce
thumbnail: 37843.jpg
source-git-commit: 247c521e93990df2c8026da5edd84d163d5d424b
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 1%

---


# Introducción a AEM Extension for PWA Studio {#getting-started-pwa}

De serie, el PWA Studio se integra perfectamente con el Adobe Commerce a través de GraphQL, proporcionando opciones ilimitadas para crear tiendas innovadoras y atractivas y otras experiencias digitales.

Los fragmentos de contenido son fragmentos de contenido con una estructura predefinida que les permite consumirlos de forma independiente mediante GraphQL como API en diferentes formatos (por ejemplo, JSON, Markdown) y procesarlos de forma independiente. Los fragmentos de contenido incluyen todos los tipos de datos y campos requeridos para GraphQL para garantizar que la aplicación solo solicite lo que está disponible y reciba lo que se espera. La flexibilidad que proporcionan en términos de su estructura los hace perfectos para su uso en varias ubicaciones y en varios canales.

El diseño de la estructura que necesita es sencillo con el Editor del modelo de fragmento de contenido en Adobe Experience Manager. El desafío principal para integrar fragmentos de contenido de Adobe Experience Manager (o cualquier otro dato) con la aplicación de PWA Studio es recuperar datos de varios extremos de GraphQL. Esto se debe a que de forma predeterminada, el PWA Studio funciona con un único extremo de Adobe Commerce GraphQL.

## Arquitectura {#architecture}

![Arquitectura sin encabezado de PWA](/help/commerce/cif/assets/pwa-studio/PWA-Studio_Architecture.png)

## PWA Studio de configuración {#setup-pwa}

Siga la [documentación del PWA Studio](https://magento.github.io/pwa-studio/tutorials/) de Adobe Commerce para configurar la aplicación de PWA Studio.

Para conectar el PWA Studio con el extremo de GraphQL de AEM, puede utilizar la [Extensión de AEM para el PWA Studio](https://github.com/adobe/aem-pwa-studio-extensions).

1. Consulte el repositorio

1. En la aplicación de PWA Studio, añada la extensión como dependencia de desarrollo.

   ```javascript
   yarn add --dev file:{path-to-extension}/extension
   ```

1. Agregue el envoltorio Apollo Link a la aplicación PWA Studio. En pwa-root/src/index.js, realice los cambios siguientes:

   ```javascript
     import { linkWrapper } from '@adobe/pwa-studio-aem-cfm-blog-extension';
   
   // ...
   
   <Adapter apiBase={apiBase} apollo={{ link: linkWrapper(apolloLink) }} store={store}>
   ```

   Puede encontrar más detalles sobre la personalización del cliente Apollo en [linkWrapper.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/linkWrapper.js).

1. Para ampliar el componente de navegación con una entrada Blog , agregue las siguientes adaptaciones a pwa-root/local-intercept.js:

   ```javascript
   const addBlogToNavigation = require('@adobe/pwa-studio-aem-cfm-blog-extension/src/addBlogToNavigation');
   
   function localIntercept(targets) {
       addBlogToNavigation(targets);
   }    
   ```

   Puede encontrar más información sobre la personalización del componente Navegación en [addBlogToNavigation.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/addBlogToNavigation.js) y en la documentación de [Extensibility Framework](https://magento.github.io/pwa-studio/pwa-buildpack/extensibility-framework/) del PWA Studio.

1. El cliente Apollo espera el extremo de AEM GraphQL en <https://pwa-studio/endpoint.js>. Para asignar el punto final a esta ubicación, deberá personalizar la configuración de UPWARD de la aplicación PWA Studio:
a. Agregue la variable AEM_CFM_GRAPHQL a pwa-root/.env y ábrala para que apunte al extremo GraphQL de los fragmentos de contenido de AEM.

   Ejemplo: AEM_CFM_GRAPHQL=<http://localhost:4503/content/graphql/global>

   b. Agregue una resolución de proxy a la configuración de UPWARD. Una configuración de UPWARD de muestra podría tener este aspecto:

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

## Configuración AEM {#setup-aem}

Siga la documentación de los fragmentos de contenido de AEM para configurar un extremo de GraphQL para el proyecto de AEM. Además, en el proyecto de AEM, agregue las siguientes configuraciones para permitir que la aplicación PWA Studio acceda al extremo de GraphQL:

* Política de uso compartido de recursos de origen cruzado de Adobe Granite (com.adobe.granite.cors.impl.CORSPolicyImpl)

   Establezca la propiedad allowedorigin en el nombre de host completo de la aplicación PWA.

   Ejemplo:  <https://pwa-studio-test-vflyn.local.pwadev:9366>

* Filtro de referente de Apache Sling (org.apache.sling.security.impl.ReferrerFilter.cfg.json)

   Establezca la propiedad allow.hosts en el nombre de host de la aplicación PWA.

   Ejemplo: pwa-studio-test-vflyn.local.pwadev

Puede encontrar ejemplos completos de ambas configuraciones aquí: <https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension/aem/config/src/main/content/jcr_root/apps/blog-demo/config>.

Para mostrar el extremo de GraphQL, preparamos algunos modelos de fragmento de contenido de muestra y datos a través de un paquete de contenido. Funcionan bien junto con los componentes React proporcionados con la extensión de PWA Studio.

## Usos {#how-to-use}

Esta extensión se considera una implementación de ejemplo de cómo conectar una aplicación PWA Studio con AEM para recuperar y procesar contenido mediante GraphQL.

Según el caso de uso, desea crear sus propios modelos de fragmento de contenido personalizados que resulten en un esquema de GraphQL personalizado que luego puedan consumir sus propios componentes de React.

Las configuraciones de producción pueden variar en varios aspectos.

* Puede tener un único extremo federado de GraphQL que combine datos de AEM y Magento GraphQL en lugar de personalizar el cliente de Apollo.
* La aplicación PWA Studio podría usar la URL de extremo de AEM GraphQL directamente, sin un proxy con UPWARD. El proxy también se puede mover a una capa diferente (por ejemplo, CDN).
* El enfoque que mejor se adapte a sus necesidades también depende en gran medida de cómo envíe la aplicación PWA Studio al usuario final.

Esta extensión incluye dos ejemplos.

### Blog {#blog}

Mostrar anuncios de blog basados en algunos modelos de fragmento de contenido. Además, contiene ejemplos de cómo configurar el cliente Apollo para que funcione con el extremo AEM GraphQL y cómo ampliar el componente de navegación en PWA Studio. Consulte [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension) para obtener más información.

### Enriquecimiento de PDP {#pdp-enrichment}

Permite a los especialistas en marketing enriquecer fácilmente los PDP con contenido adicional que se administra como fragmentos de contenido.  Consulte [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cif-product-page-extension) para obtener más información.
