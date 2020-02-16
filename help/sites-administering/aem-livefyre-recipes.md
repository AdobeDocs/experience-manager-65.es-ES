---
title: Fórmulas de Livefyre de AEM
seo-title: Fórmulas de Livefyre de AEM
description: Instrucciones paso a paso sobre casos de uso comunes para Adobe Experience Manager Livefyre.
seo-description: Instrucciones paso a paso sobre casos de uso comunes para Adobe Experience Manager Livefyre.
uuid: 78695a63-fca6-4990-9755-0aeaae4a7f64
contentOwner: alba
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fdea5ede-d44f-463e-af8a-111ee7469ede
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Fórmulas de Livefyre de AEM{#aem-livefyre-recipes}

Instrucciones paso a paso sobre casos de uso comunes para Adobe Experience Manager Livefyre.

## Depure UGC con los componentes integrados de Livefyre AEM y visualícelos con Livefyre Media Wall {#curate-ugc-using-the-out-of-the-box-livefyre-aem-components-and-display-using-livefyre-media-wall}

Media Wall transmite contenido social y nativo de Livefyre a un muro social en tiempo real. Existen varias formas de implementar Media Wall en AEM según el caso de uso y los requisitos.

El paquete de Livefyre de AEM proporciona una implementación lista para usar, mientras que la integración tradicional permite crear componentes personalizados de Livefyre AEM.

### Integración de AEM {#aem-integration}

El paquete Livefyre de Adobe Experience Manager está disponible para AEM 6.1, 6.2SP1, 6.3, ,6.4 y 6.4 SP1. AEM 5.x y 6.0 no son compatibles. Para obtener instrucciones detalladas, consulte [Integración con Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

Para ver qué aplicaciones de Livefyre son compatibles, consulte la matriz de compatibilidad de [AEM para aplicaciones](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps)de Livefyre.

### Implementación tradicional (para componentes personalizados de AEM) {#traditional-implementation-for-customized-aem-components}

Existen tres formas de implementar Livefyre en un componente AEM personalizado u otros CMS como WordPress, SiteServer o DemandWare. Una integración tradicional de Livefyre es agnóstica con CMS.

**Método 1: Implementación de la aplicación de Designer**

* **** Qué: La forma más sencilla y rápida de integrar una aplicación de Livefyre. Puede diseñar, configurar y generar un código incrustado de JavaScript personalizado para integrar una aplicación de Media Wall en una página en cuestión de minutos.
* **** Cómo:  [Crear, previsualizar, publicar e incrustar una aplicación de Media Wall](https://marketing.adobe.com/resources/help/en_US/livefyre/c_create_an_app.html)

* **** Ejemplo: [https://codepen.io/dharafyre/pen/bvGrLo](https://codepen.io/dharafyre/pen/bvGrLo)

**Método 2: Implementación de SDK**

* **** Qué: [Livefyre.js](https://marketing.adobe.com/resources/help/en_US/livefyre/c_livefyre.js.html) es la biblioteca principal que activa las aplicaciones y la autenticación en un sitio. Define el objeto *window.Livefyre* global y un único método público, *Livefyre.require*, que se puede utilizar para cargar otras bibliotecas JavaScript de Livefyre que ayudan a incrustar aplicaciones de Livefyre e integrarse con plataformas de autenticación de usuarios de terceros.

* **Cómo**: [Utilice el paquete de optimizaciones del SDK de JavaScript de Livefyre](https://marketing.adobe.com/resources/help/en_US/livefyre/?f=c_media_wall_app&s=c_media_wall_integration)

* **Ejemplo**: [https://codepen.io/dharafyre/pen/KZKBNv?editors=1010](https://codepen.io/dharafyre/pen/KZKBNv?editors=1010)

Para personalizaciones avanzadas con el SDK, consulte los SDK [de StreamHub](https://github.com/Livefyre/streamhub-sdk).

**Método 3: Implementación de API**

* Para crear experiencias y visualizaciones de datos personalizadas, las aplicaciones de Livefyre se pueden crear desde cero consumiendo datos sociales y de Livefyre mediante la API [de](https://marketing.adobe.com/resources/help/en_US/livefyre/bootstrap-stream-api.html)Bootstrap y Stream.

Asegúrese de seguir las directrices de visualización de [Twitter](https://developer.twitter.com/en/developer-terms/display-requirements.html), [Facebook](https://en.facebookbrand.com/guidelines/brand)e [Instagram](https://en.instagram-brand.com/) al crear la IU para UGC.

### Integración de autenticación de Media Wall {#media-wall-authentication-integration}

Para integraciones de Media Wall que requieren autenticación, consulte:

* [Personalización de la integración](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) de inicio de sesión único para AEM Identity Management
* [Integración](https://marketing.adobe.com/resources/help/en_US/livefyre/t_about_identity_integration.html) de identidad para plataformas de autenticación de terceros

### Información general de caso de uso {#use-case-overview}

Como cliente de AEM, deseo depurar UGC mediante los componentes integrados de Livefyre AEM y mostrarlos mediante Livefyre Media Wall:

Pasos para implementar:

1. [Introducción](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Configuración de AEM para utilizar Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Arrastre y suelte el componente AEM Media Wall en la página](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMSites)
1. [Configurar flujos y agregar reglas para conservar UGC y mostrarlas en el componente Media Wall](https://marketing.adobe.com/resources/help/en_US/livefyre/c_streams.html)

Para ver vídeos de formación sobre la transmisión por secuencias UGC, consulte [Creación de flujos de contenido automáticos y Búsqueda de contenido social en Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

### Ejemplos de clientes {#customer-examples}

* [Muro de los medios CNN](https://edition.cnn.com/specials/nepal-earthquake-media-wall)
* [PGA Tour Media Wall](https://www.pgatour.com/social-hub.html)

Para crear experiencias y visualizaciones de datos personalizadas, las aplicaciones de Livefyre se pueden crear desde cero consumiendo datos sociales y de Livefyre mediante la API [de](https://marketing.adobe.com/resources/help/en_US/livefyre/bootstrap-stream-api.html)Bootstrap y Stream.

Para las aplicaciones de Livefyre que requieren autenticación, consulte Integración [de identidad](https://marketing.adobe.com/resources/help/en_US/livefyre/t_about_identity_integration.html) para plataformas de autenticación de terceros.

* [PGA Tour Media Wall](https://www.pgatour.com/social-hub.html)
* [Tiempo de expiración](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)

## Integración de comentarios de Livefyre con componentes de AEM o integración tradicional de Livefyre {#integrate-livefyre-comments-using-aem-components-or-traditional-livefyre-integration}

### Integración de AEM {#aem-integration-1}

El paquete Livefyre de Adobe Experience Manager está disponible para AEM 6.1, 6.2SP1, 6.3, ,6.4 y 6.4 SP1. AEM 5.x y 6.0 no son compatibles. Para obtener instrucciones detalladas, consulte [Integración con Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

### Implementación tradicional (para componentes personalizados de AEM) {#traditional-implementation-for-customized-aem-components-1}

Existen tres formas de implementar la aplicación de comentarios de Livefyre en un componente personalizado de AEM u otros CMS como WordPress, SiteServer o DemandWare. Una integración tradicional de Livefyre es agnóstica con CMS.

**Método 1: Implementación de la aplicación de Designer**

* **** Qué: La forma más sencilla y rápida de integrar una aplicación de Livefyre. Puede diseñar, configurar y generar un código incrustado de JavaScript personalizado para integrar una aplicación de Media Wall en una página en cuestión de minutos.
* **** Cómo: [Crear, previsualizar, publicar e incrustar una aplicación de comentarios](https://marketing.adobe.com/resources/help/en_US/livefyre/c_create_an_app.html)

* **** Ejemplo:  [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

**Método 2: Implementación de SDK**

* **** Qué: [Livefyre.js](https://marketing.adobe.com/resources/help/en_US/livefyre/c_livefyre.js.html) es la biblioteca principal que activa las aplicaciones y la autenticación en un sitio. Define el objeto *window.Livefyre* global y un único método público, *Livefyre.require*, que se puede utilizar para cargar otras bibliotecas JavaScript de Livefyre que ayudan a incrustar aplicaciones de Livefyre e integrarse con plataformas de autenticación de usuarios de terceros.

* **Cómo:**

   * Cree una colección o aplicación mediante [CollectionMeta token](https://marketing.adobe.com/resources/help/en_US/livefyre/t_create_a_collectionmeta_token.html).
   * Integre la aplicación [](https://marketing.adobe.com/resources/help/en_US/livefyre/c_comments_integration.html) Comentarios en sitios mediante la estructura de código incrustado de Livefyre.js.

* **** Ejemplo:  [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

Para obtener personalizaciones avanzadas con el SDK, consulte SDK [de StreamHub](https://github.com/Livefyre/streamhub-sdk).

**Método 3: Implementación de API**

* Para crear experiencias y visualizaciones de datos personalizadas, las aplicaciones de Livefyre se pueden crear desde cero consumiendo datos sociales y de Livefyre mediante la API [de](https://marketing.adobe.com/resources/help/en_US/livefyre/bootstrap-stream-api.html)Bootstrap y Stream.

### Integración de autenticación de aplicación de comentarios {#comments-app-authentication-integration}

* [Personalización de la integración](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) de inicio de sesión único para AEM Identity Management
* [Integración](https://marketing.adobe.com/resources/help/en_US/livefyre/t_about_identity_integration.html) de identidad para plataformas de autenticación de terceros

### Ejemplos de clientes {#customer-examples-1}

* [Poise (Kimberly Klark)](https://www.poise.com/en-us/advice-and-support/blog-and-podcast/blog/5-holiday-party-tips-for-managing-lbl)

## Uso de la integración de Livefyre AEM Assets para importar UGC en AEM Assets {#use-livefyre-aem-assets-integration-to-import-ugc-in-aem-assets}

**Configuración de Livefyre (para Conservación de UGC y Administración de derechos):**

1. [Configure flujos y agregue reglas para conservar UGC en las carpetas](https://marketing.adobe.com/resources/help/en_US/livefyre/c_streams.html)de la biblioteca de recursos de Livefyre.

   1. Para ver vídeos de formación sobre la transmisión por secuencias UGC, consulte [Creación de flujos de contenido automáticos y Búsqueda de contenido social en Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Recopile, organice y administre UGC depurado en carpetas](https://marketing.adobe.com/resources/help/en_US/livefyre/c_assets.html)de la biblioteca de recursos de Livefyre.

   1. Para ver vídeos de formación sobre la creación y administración de carpetas en la biblioteca de recursos de Livefyre Studio, consulte [Trabajo con recursos en Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Solicitar derechos para UGC depurado mediante Livefyre Studio](https://marketing.adobe.com/resources/help/en_US/livefyre/c_how_requesting_rights_works.html).

**Configuración de AEM (para importar UGC a AEM Assets):**

1. [Introducción](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#GettingStarted)
1. [Configuración de AEM para utilizar Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#ConfigureAEMtouseLivefyre)
1. [Importar UGC depurado por Livefyre en AEM Assets](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMAssets)

* [Turismo Australia](https://www.australia.com/en-us)

## Integración de Livefyre Reviews con componentes de AEM o integración tradicional de Livefyre {#integrate-livefyre-reviews-using-aem-components-or-traditional-livefyre-integration}

### Integración de AEM {#aem-integration-2}

El paquete Livefyre de Adobe Experience Manager está disponible para AEM 6.1, 6.2SP1, 6.3, ,6.4 y 6.4 SP1. AEM 5.x y 6.0 no son compatibles. Para obtener instrucciones detalladas, consulte [Integración con Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

El componente Reseñas no es un componente compatible con AEM 6.1. Compruebe la matriz de asistencia de [AEM para todas las aplicaciones](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps)de Livefyre.

### Implementación tradicional (para componentes personalizados de AEM) {#traditional-implementation-for-customized-aem-components-2}

Existen dos formas de implementar la aplicación Livefyre Reviews en un componente personalizado de AEM u otros CMS como WordPress, Sitecore o DemandWare. Una integración tradicional de Livefyre es agnóstica con CMS.

**Método 1: Implementación de SDK**

* **** Qué: [Livefyre.js](https://marketing.adobe.com/resources/help/en_US/livefyre/c_livefyre.js.html) es la biblioteca principal que activa las aplicaciones y la autenticación en un sitio. Define el objeto *window.Livefyre* global y un único método público, *Livefyre.require*, que se puede utilizar para cargar otras bibliotecas JavaScript de Livefyre que ayudan a incrustar aplicaciones de Livefyre e integrarse con plataformas de autenticación de usuarios de terceros.

* **Cómo:**

   * Cree el [tokenMeta de la colección Reviews para especificar los metadatos que se almacenarán en la colección Reviews](https://marketing.adobe.com/resources/help/en_US/livefyre/c_reviews_integration.html) .
   * Integrar la aplicación [de](https://marketing.adobe.com/resources/help/en_US/livefyre/c_reviews_integration.html) revisiones en sitios mediante la estructura de código incrustado de *Livefyre.js*

* **** Ejemplo:  [https://codepen.io/dharafyre/pen/GXgvvd](https://codepen.io/dharafyre/pen/GXgvvd)

Para obtener personalizaciones avanzadas con el SDK, consulte SDK [de StreamHub](https://github.com/Livefyre/streamhub-sdk).

**Método 2: Implementación de API**

* Para crear experiencias y visualizaciones de datos personalizadas, las aplicaciones de Livefyre se pueden crear desde cero consumiendo datos sociales y de Livefyre mediante la API de Bootstrap y Stream.

Las API de Clasificaciones y críticas adicionales se pueden encontrar [aquí](https://api.livefyre.com/docs/apis/by-category/ratings-and-reviews).

### Integración de autenticación de aplicación de comentarios {#comments-app-authentication-integration-1}

* [Personalización de la integración](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) de inicio de sesión único para AEM Identity Management
* [Integración](https://marketing.adobe.com/resources/help/en_US/livefyre/t_about_identity_integration.html) de identidad para plataformas de autenticación de terceros

### Ejemplos de clientes {#customer-examples-2}

* [Tiempo de expiración](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)
* [micras](https://www.myrecipes.com/recipe/shrimp-florentine-pasta)

