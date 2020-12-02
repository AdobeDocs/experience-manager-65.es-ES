---
title: Fórmulas AEM Livefyre
seo-title: Fórmulas AEM Livefyre
description: Instrucciones paso a paso sobre casos de uso común de Adobe Experience Manager Livefyre.
seo-description: Instrucciones paso a paso sobre casos de uso común de Adobe Experience Manager Livefyre.
uuid: 78695a63-fca6-4990-9755-0aeaae4a7f64
contentOwner: alba
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fdea5ede-d44f-463e-af8a-111ee7469ede
translation-type: tm+mt
source-git-commit: 072898f18d418eac8e9d9e94453db34d62dd3ed9
workflow-type: tm+mt
source-wordcount: '1559'
ht-degree: 0%

---


# Fórmulas de Livefyre de AEM{#aem-livefyre-recipes}

Instrucciones paso a paso sobre casos de uso común de Adobe Experience Manager Livefyre.

## Depure UGC con los componentes de AEM de Livefyre integrados y visualícelos con Livefyre Media Wall {#curate-ugc-using-the-out-of-the-box-livefyre-aem-components-and-display-using-livefyre-media-wall}

Media Wall transmite contenido social y nativo de Livefyre a un muro social en tiempo real. Existen varias formas de implementar Media Wall en AEM según el caso de uso y los requisitos.

El paquete de Livefyre de AEM proporciona una implementación lista para usar, mientras que la integración tradicional ofrece la capacidad de crear componentes AEM Livefyre personalizados.

### Integración de AEM {#aem-integration}

El paquete de Adobe Experience Manager Livefyre está disponible para AEM 6.1, 6.2SP1, 6.3, ,6.4 y 6.4 SP1. AEM 5.x y 6.0 no son compatibles. Para obtener instrucciones detalladas, consulte [Integración con Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

Para ver qué aplicaciones de Livefyre son compatibles, consulte la [Matriz de soporte de AEM para aplicaciones de Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### Implementación tradicional (para componentes de AEM personalizados) {#traditional-implementation-for-customized-aem-components}

Existen tres formas de implementar Livefyre en un componente de AEM personalizado u otros CMS como WordPress, SiteServer o DemandWare. Una integración tradicional de Livefyre es agnóstica con CMS.

**Método 1: Implementación de la aplicación de Designer**

* **Qué:** La forma más sencilla y rápida de integrar una aplicación de Livefyre. Puede diseñar, configurar y generar un código incrustado de JavaScript personalizado para integrar una aplicación de Media Wall en una página en cuestión de minutos.
* **Cómo:**  [Crear, Previsualización, publicar e incrustar una aplicación de Media Wall](https://docs.adobe.com/content/help/en/livefyre/using/apps/c-create-an-app.html)

* **Ejemplo:** [https://codepen.io/dharafyre/pen/bvGrLo](https://codepen.io/dharafyre/pen/bvGrLo)

**Método 2: Implementación de SDK**

* **Qué:** [Livefyre.](https://docs.adobe.com/content/help/en/livefyre/implementation/c-livefyre_js.html) jsis es la biblioteca principal que activa las aplicaciones y la autenticación en un sitio. Define el objeto *window.Livefyre* global y un único método público, *Livefyre.requirements*, que se puede utilizar para cargar otras bibliotecas JavaScript de Livefyre que ayudan a incrustar aplicaciones de Livefyre e integrarse con plataformas de autenticación de usuarios de terceros.

* **Cómo**:  [Utilice el paquete de Strehub-wallpackage del SDK de JavaScript de Livefyre](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/c-media-wall-integration.html)

* **Ejemplo**:  [https://codepen.io/dharafyre/pen/KZKBNv?editors=1010](https://codepen.io/dharafyre/pen/KZKBNv?editors=1010)

Para obtener personalizaciones avanzadas con el SDK, consulte [SDK de StreamHub](https://github.com/Livefyre/streamhub-sdk).

**Método 3: Implementación de API**

* Para crear experiencias y visualizaciones de datos personalizadas, las aplicaciones de Livefyre se pueden crear desde cero consumiendo datos sociales y de Livefyre mediante el [Bootstrap y la API de flujo](https://docs.adobe.com/content/help/en/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

Asegúrese de seguir [Twitter](https://developer.twitter.com/en/developer-terms/display-requirements.html), [Facebook](https://en.facebookbrand.com/guidelines/brand) e [Instagram](https://en.instagram-brand.com/) las pautas de visualización al crear la IU para UGC.

### Integración de autenticación de muro de medios {#media-wall-authentication-integration}

Para integraciones de Media Wall que requieren autenticación, consulte:

* [Personalizar la ](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) integración del inicio de sesión único para AEM Identity Management
* [Integración ](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html) de identidades para plataformas de autenticación de terceros

### Información general de caso de uso {#use-case-overview}

Como cliente AEM, quiero depurar UGC usando los componentes de Livefyre integrados AEM y mostrarlos con Livefyre Media Wall:

Pasos para implementar:

1. [Introducción](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Configurar AEM para usar Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Arrastre y suelte AEM componente de Media Wall en la página](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMSites)
1. [Configurar flujos y agregar reglas para conservar UGC y mostrarlas en el componente Media Wall](https://docs.adobe.com/content/help/en/livefyre/using/streams/c-streams.html)

Para ver vídeos de capacitación sobre transmisión por secuencias UGC, consulte [Creación de flujos de contenido automático y Búsqueda de contenido social en Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

### Ejemplos de clientes {#customer-examples}

* [Muro de los medios CNN](https://edition.cnn.com/specials/nepal-earthquake-media-wall)
* [PGA Tour Media Wall](https://www.pgatour.com/social-hub.html)

Para crear experiencias y visualizaciones de datos personalizadas, las aplicaciones de Livefyre se pueden crear desde cero consumiendo datos sociales y de Livefyre mediante el [Bootstrap y la API de flujo](https://docs.adobe.com/content/help/en/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

Para las aplicaciones de Livefyre que requieren autenticación, consulte [Integración de identidad](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html) para plataformas de autenticación de terceros.

* [PGA Tour Media Wall](https://www.pgatour.com/social-hub.html)
* [Tiempo de expiración](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)

## Integrar comentarios de Livefyre mediante componentes AEM o integración tradicional de Livefyre {#integrate-livefyre-comments-using-aem-components-or-traditional-livefyre-integration}

### Integración de AEM {#aem-integration-1}

El paquete de Adobe Experience Manager Livefyre está disponible para AEM 6.1, 6.2SP1, 6.3, ,6.4 y 6.4 SP1. AEM 5.x y 6.0 no son compatibles. Para obtener instrucciones detalladas, consulte [Integración con Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

### Implementación tradicional (para componentes de AEM personalizados) {#traditional-implementation-for-customized-aem-components-1}

Existen tres formas de implementar la aplicación de comentarios de Livefyre en un componente de AEM personalizado u otros CMS como WordPress, SiteServer o DemandWare. Una integración tradicional de Livefyre es agnóstica con CMS.

**Método 1: Implementación de la aplicación de Designer**

* **Qué:** La forma más sencilla y rápida de integrar una aplicación de Livefyre. Puede diseñar, configurar y generar un código incrustado de JavaScript personalizado para integrar una aplicación de Media Wall en una página en cuestión de minutos.
* **Cómo:** [Crear, Previsualización, publicar e incrustar una aplicación de comentarios](https://docs.adobe.com/content/help/en/livefyre/using/apps/c-create-an-app.html)

* **Ejemplo:** [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

**Método 2: Implementación de SDK**

* **Qué:** [Livefyre.](https://docs.adobe.com/content/help/en/livefyre/implementation/c-livefyre_js.html) jsis es la biblioteca principal que activa las aplicaciones y la autenticación en un sitio. Define el objeto *window.Livefyre* global y un único método público, *Livefyre.requirements*, que se puede utilizar para cargar otras bibliotecas JavaScript de Livefyre que ayudan a incrustar aplicaciones de Livefyre e integrarse con plataformas de autenticación de usuarios de terceros.

* **Cómo:**

   * Cree una colección o aplicación con [token de CollectionMeta](https://docs.adobe.com/content/help/en/livefyre/implementation/getting-started/implementation-process/c-collectionmeta-tokent.html).
   * Integre [Aplicación de comentarios](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/comments/c-comments-integration.html) en sitios mediante la estructura de código incrustado de Livefyre.js.

* **Ejemplo:**  [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

Para obtener personalizaciones avanzadas con el SDK, consulte [SDK de StreamHub](https://github.com/Livefyre/streamhub-sdk).

**Método 3: Implementación de API**

* Para crear experiencias y visualizaciones de datos personalizadas, las aplicaciones de Livefyre se pueden crear desde cero consumiendo datos sociales y de Livefyre mediante el [Bootstrap y la API de flujo](https://docs.adobe.com/content/help/en/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

### Integración de autenticación de aplicación de comentarios {#comments-app-authentication-integration}

* [Personalizar la ](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) integración del inicio de sesión único para AEM Identity Management
* [Integración ](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html) de identidades para plataformas de autenticación de terceros

### Ejemplos de clientes {#customer-examples-1}

* [Poise (Kimberly Klark)](https://www.poise.com/en-us/advice-and-support/blog-and-podcast/blog/5-holiday-party-tips-for-managing-lbl)

## Utilice la integración de AEM Assets de Livefyre para importar UGC en AEM Assets {#use-livefyre-aem-assets-integration-to-import-ugc-in-aem-assets}

**Configuración de Livefyre (para Rights Management y depuración UGC):**

1. [Configure flujos y Añada reglas para conservar UGC en carpetas](https://docs.adobe.com/content/help/en/livefyre/using/streams/c-streams.html) de la biblioteca de recursos de Livefyre.

   1. Para ver vídeos de capacitación sobre transmisión por secuencias UGC, consulte [Creación de flujos de contenido automático y Búsqueda de contenido social en Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Recopile, organice y administre UGC depurado en carpetas](https://docs.adobe.com/content/help/en/livefyre/using/library/assets/c-assets.html) de la biblioteca de recursos de Livefyre.

   1. Para ver vídeos de formación sobre la creación y administración de carpetas en la biblioteca de recursos de Livefyre Studio, consulte [Trabajo con recursos en Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Solicitar derechos para UGC depurado mediante Livefyre Studio](https://docs.adobe.com/content/help/en/livefyre/using/rights-requests/c-how-requesting-rights-works.html).

**Configuración de AEM (para importar UGC a AEM Assets):**

1. [Introducción](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#GettingStarted)
1. [Configurar AEM para usar Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#ConfigureAEMtouseLivefyre)
1. [Importar UGC depurado por Livefyre en AEM Assets](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMAssets)

* [Turismo Australia](https://www.australia.com/en-us)

## Integrar las revisiones de Livefyre mediante componentes AEM o integración tradicional de Livefyre {#integrate-livefyre-reviews-using-aem-components-or-traditional-livefyre-integration}

### Integración de AEM {#aem-integration-2}

El paquete de Adobe Experience Manager Livefyre está disponible para AEM 6.1, 6.2SP1, 6.3, ,6.4 y 6.4 SP1. AEM 5.x y 6.0 no son compatibles. Para obtener instrucciones detalladas, consulte [Integración con Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

El componente Reseñas no es un componente admitido para AEM 6.1. Verifique la [matriz de soporte de AEM para todas las aplicaciones de Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### Implementación tradicional (para componentes de AEM personalizados) {#traditional-implementation-for-customized-aem-components-2}

Existen dos maneras de implementar la aplicación de análisis de Livefyre en un componente de AEM personalizado u otros CMS como WordPress, SiteServer o DemandWare. Una integración tradicional de Livefyre es agnóstica con CMS.

**Método 1: Implementación de SDK**

* **Qué:** [Livefyre.](https://docs.adobe.com/content/help/en/livefyre/implementation/c-livefyre_js.html) jsis es la biblioteca principal que activa las aplicaciones y la autenticación en un sitio. Define el objeto *window.Livefyre* global y un único método público, *Livefyre.requirements*, que se puede utilizar para cargar otras bibliotecas JavaScript de Livefyre que ayudan a incrustar aplicaciones de Livefyre e integrarse con plataformas de autenticación de usuarios de terceros.

* **Cómo:**

   * Cree el [token de CollectionMeta](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/c-reviews-integration.html) de críticas para especificar los metadatos que se almacenarán en la colección de revisiones.
   * Integrar [Revisa la aplicación](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/c-reviews-integration.html) en sitios mediante la estructura de código incrustado *Livefyre.js*

* **Ejemplo:**  [https://codepen.io/dharafyre/pen/GXgvvd](https://codepen.io/dharafyre/pen/GXgvvd)

Para obtener personalizaciones avanzadas con el SDK, consulte [SDK de StreamHub](https://github.com/Livefyre/streamhub-sdk).

**Método 2: Implementación de API**

* Para crear experiencias y visualizaciones de datos personalizadas, las aplicaciones de Livefyre se pueden crear desde cero mediante el uso de datos sociales y de Livefyre mediante la API de flujo y Bootstrap.

Encontrará más API de clasificaciones y revisiones [aquí](https://api.livefyre.com/docs/apis/by-category/ratings-and-reviews).

### Integración de autenticación de aplicación de comentarios {#comments-app-authentication-integration-1}

* [Personalizar la ](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) integración del inicio de sesión único para AEM Identity Management
* [Integración ](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html) de identidades para plataformas de autenticación de terceros

### Ejemplos de clientes {#customer-examples-2}

* [Tiempo de expiración](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)
* [micras](https://www.myrecipes.com/recipe/shrimp-florentine-pasta)

