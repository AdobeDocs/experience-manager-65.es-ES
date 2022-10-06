---
title: Fórmulas de AEM Livefyre
seo-title: AEM Livefyre Recipes
description: Instrucciones paso a paso sobre casos de uso común de Adobe Experience Manager Livefyre.
seo-description: Step-by-step instructions on common use cases for Adobe Experience Manager Livefyre.
uuid: 78695a63-fca6-4990-9755-0aeaae4a7f64
contentOwner: alba
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fdea5ede-d44f-463e-af8a-111ee7469ede
exl-id: 7ccd67a7-9945-48c1-9986-f4eaf0f2b961
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1545'
ht-degree: 4%

---

# Fórmulas de AEM Livefyre{#aem-livefyre-recipes}

Instrucciones paso a paso sobre casos de uso común de Adobe Experience Manager Livefyre.

## Depure UGC con los componentes de AEM de Livefyre listos para usar y muestre con el muro de medios de Livefyre {#curate-ugc-using-the-out-of-the-box-livefyre-aem-components-and-display-using-livefyre-media-wall}

Media Wall transmite contenido social y nativo de Livefyre a un muro social en tiempo real. Existen varias formas de implementar el muro de medios en AEM según el caso de uso y los requisitos.

El paquete AEM Livefyre proporciona una implementación predeterminada, mientras que la integración tradicional permite crear componentes personalizados de AEM de Livefyre.

### Integración AEM {#aem-integration}

El paquete Adobe Experience Manager de Livefyre está disponible para AEM 6.1, 6.2SP1, 6.3, ,6.4 y 6.4 SP1. AEM 5.x y 6.0 no son compatibles. Para obtener instrucciones detalladas, consulte [Integración con Livefyre](https://helpx.adobe.com/es/experience-manager/6-4/sites/administering/using/livefyre.html).

Para ver qué aplicaciones de Livefyre son compatibles, consulte la [Matriz de soporte AEM para aplicaciones de Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### Implementación tradicional (para componentes de AEM personalizados) {#traditional-implementation-for-customized-aem-components}

Existen tres maneras de implementar Livefyre en un componente de AEM personalizado u otros CMS como WordPress, SiteServer o DemandWare. Una integración tradicional de Livefyre es independiente de CMS.

**Método 1: Implementación de aplicación de Designer**

* **Qué:** La forma más sencilla y rápida de integrar una aplicación Livefyre. Puede diseñar, configurar y generar un código incrustado de JavaScript personalizado para integrar una aplicación de muro de medios en una página en cuestión de minutos.
* **Cómo:**  [Crear, previsualizar, publicar e incrustar una aplicación de muro de medios](https://docs.adobe.com/content/help/en/livefyre/using/apps/c-create-an-app.html)

* **Ejemplo:** [https://codepen.io/dharafyre/pen/bvGrLo](https://codepen.io/dharafyre/pen/bvGrLo)

**Método 2: Implementación del SDK**

* **Qué:** [Livefyre.js](https://docs.adobe.com/content/help/en/livefyre/implementation/c-livefyre_js.html) es la biblioteca principal que alimenta las aplicaciones y la autenticación en un sitio. Define el *window.Livefyre* y un único método público, *Livefyre.required*, que se puede utilizar para cargar otras bibliotecas JavaScript de Livefyre que ayuden a incrustar aplicaciones de Livefyre e integrarse con plataformas de autenticación de usuarios de terceros.

* **Cómo**: [Utilice el paquete streamhub-wallpackage del SDK de JavaScript de Livefyre](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/c-media-wall-integration.html)

* **Ejemplo**: [https://codepen.io/dharafyre/pen/KZKBNv?editors=1010](https://codepen.io/dharafyre/pen/KZKBNv?editors=1010)

Para personalizaciones avanzadas con el SDK, consulte [SDK de StreamHub](https://github.com/Livefyre/streamhub-sdk).

**Método 3: Implementación de API**

* Para crear experiencias personalizadas y visualizaciones de datos, las aplicaciones de Livefyre se pueden crear desde cero consumiendo datos sociales y de Livefyre utilizando la variable [API de Bootstrap y flujo](https://docs.adobe.com/content/help/en/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

Asegúrese de seguir [Twitter](https://developer.twitter.com/en/developer-terms/display-requirements.html), [Facebook](https://en.facebookbrand.com/guidelines/brand)y [Instagram](https://en.instagram-brand.com/) mostrar directrices al crear la interfaz de usuario para UGC.

### Integración de autenticación de Media Wall {#media-wall-authentication-integration}

Para integraciones de muro de medios que requieran autenticación, consulte:

* [Personalizar la integración del inicio de sesión único](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) para AEM Identity Management
* [Integración de identidad](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html) para plataformas de autenticación de terceros

### Información general de caso de uso {#use-case-overview}

Como cliente AEM, quiero depurar UGC usando los componentes de AEM de Livefyre listos para usar y mostrarlos usando el muro de medios de Livefyre:

Pasos para implementar:

1. [Introducción](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Configuración de AEM para utilizar Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Arrastre y suelte AEM componente Muro de medios en su página](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMSites)
1. [Configurar flujos y agregar reglas para depurar UGC y mostrar en el componente de muro de medios](https://docs.adobe.com/content/help/en/livefyre/using/streams/c-streams.html)

Para ver vídeos de formación sobre la transmisión de UGC, consulte [Crear flujos de contenido automáticos y buscar contenido social en Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

### Ejemplos de clientes {#customer-examples}

* [Muro de medios CNN](https://edition.cnn.com/specials/nepal-earthquake-media-wall)
* [Pared de medios Tour PGA](https://www.pgatour.com/social-hub.html)

Para crear experiencias personalizadas y visualizaciones de datos, las aplicaciones de Livefyre se pueden crear desde cero consumiendo datos sociales y de Livefyre utilizando la variable [API de Bootstrap y flujo](https://docs.adobe.com/content/help/en/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

Para las aplicaciones de Livefyre que requieren autenticación, consulte [Integración de identidad](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html) para plataformas de autenticación de terceros.

* [Pared de medios Tour PGA](https://www.pgatour.com/social-hub.html)
* [Tiempo de expiración](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)

## Integración de comentarios de Livefyre mediante componentes AEM o integración tradicional de Livefyre {#integrate-livefyre-comments-using-aem-components-or-traditional-livefyre-integration}

### Integración AEM {#aem-integration-1}

El paquete Adobe Experience Manager de Livefyre está disponible para AEM 6.1, 6.2SP1, 6.3, ,6.4 y 6.4 SP1. AEM 5.x y 6.0 no son compatibles. Para obtener instrucciones detalladas, consulte [Integración con Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

### Implementación tradicional (para componentes de AEM personalizados) {#traditional-implementation-for-customized-aem-components-1}

Existen tres maneras de implementar la aplicación de comentarios de Livefyre en un componente de AEM personalizado u otros CMS como WordPress, SiteServer o DemandWare. Una integración tradicional de Livefyre es independiente de CMS.

**Método 1: Implementación de aplicación de Designer**

* **Qué:** La forma más sencilla y rápida de integrar una aplicación Livefyre. Puede diseñar, configurar y generar un código incrustado de JavaScript personalizado para integrar una aplicación de muro de medios en una página en cuestión de minutos.
* **Cómo:** [Crear, previsualizar, publicar e incrustar una aplicación de comentarios](https://docs.adobe.com/content/help/en/livefyre/using/apps/c-create-an-app.html)

* **Ejemplo:** [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

**Método 2: Implementación del SDK**

* **Qué:** [Livefyre.js](https://docs.adobe.com/content/help/en/livefyre/implementation/c-livefyre_js.html) es la biblioteca principal que alimenta las aplicaciones y la autenticación en un sitio. Define el *window.Livefyre* y un único método público, *Livefyre.required*, que se puede utilizar para cargar otras bibliotecas JavaScript de Livefyre que ayuden a incrustar aplicaciones de Livefyre e integrarse con plataformas de autenticación de usuarios de terceros.

* **Cómo:**

   * Creación de una colección o aplicación mediante [CollectionMeta token](https://docs.adobe.com/content/help/en/livefyre/implementation/getting-started/implementation-process/c-collectionmeta-tokent.html).
   * Integrar [Aplicación de comentarios](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/comments/c-comments-integration.html) en sitios mediante la estructura de código incrustado de Livefyre.js.

* **Ejemplo:**  [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

Para personalizaciones avanzadas con el SDK, consulte [SDK de StreamHub](https://github.com/Livefyre/streamhub-sdk).

**Método 3: Implementación de API**

* Para crear experiencias personalizadas y visualizaciones de datos, las aplicaciones de Livefyre se pueden crear desde cero consumiendo datos sociales y de Livefyre utilizando la variable [API de Bootstrap y flujo](https://docs.adobe.com/content/help/en/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

### Integración de la autenticación de la aplicación de comentarios {#comments-app-authentication-integration}

* [Personalizar la integración del inicio de sesión único](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) para AEM Identity Management
* [Integración de identidad](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html) para plataformas de autenticación de terceros

### Ejemplos de clientes {#customer-examples-1}

* [Poise (Kimberly Klark)](https://www.poise.com/en-us/advice-and-support/blog-and-podcast/blog/5-holiday-party-tips-for-managing-lbl)

## Utilice la integración de Livefyre AEM Assets para importar UGC en AEM Assets {#use-livefyre-aem-assets-integration-to-import-ugc-in-aem-assets}

**Configuración de Livefyre (para Rights Management y depuración de UGC):**

1. [Configurar flujos y agregar reglas para depurar UGC en carpetas de la biblioteca de activos de Livefyre](https://docs.adobe.com/content/help/en/livefyre/using/streams/c-streams.html).

   1. Para ver vídeos de formación sobre la transmisión de UGC, consulte [Crear flujos de contenido automáticos y buscar contenido social en Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Recopile, organice y administre UGC depurado en carpetas de la biblioteca de activos de Livefyre](https://docs.adobe.com/content/help/en/livefyre/using/library/assets/c-assets.html).

   1. Para ver vídeos de formación sobre la creación y administración de carpetas en la biblioteca de activos de Livefyre Studio, consulte [Trabajar con Assets en Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Solicitar derechos para UGC depurado usando Livefyre Studio](https://docs.adobe.com/content/help/en/livefyre/using/rights-requests/c-how-requesting-rights-works.html).

**Configuración de AEM (para importar UGC a AEM Assets):**

1. [Introducción](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#GettingStarted)
1. [Configuración de AEM para utilizar Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#ConfigureAEMtouseLivefyre)
1. [Importar UGC depurado por Livefyre en AEM Assets](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMAssets)

* [Turismo Australia](https://www.australia.com/en-us)

## Integración de revisiones de Livefyre mediante componentes AEM o integración tradicional de Livefyre {#integrate-livefyre-reviews-using-aem-components-or-traditional-livefyre-integration}

### Integración AEM {#aem-integration-2}

El paquete Adobe Experience Manager de Livefyre está disponible para AEM 6.1, 6.2SP1, 6.3, ,6.4 y 6.4 SP1. AEM 5.x y 6.0 no son compatibles. Para obtener instrucciones detalladas, consulte [Integración con Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

El componente de revisiones no es un componente compatible para AEM 6.1. Compruebe la [Matriz de soporte de AEM para todas las aplicaciones de Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### Implementación tradicional (para componentes de AEM personalizados) {#traditional-implementation-for-customized-aem-components-2}

Existen dos maneras de implementar la aplicación de reseñas de Livefyre en un componente de AEM personalizado u otros CMS como WordPress, SiteServer o DemandWare. Una integración tradicional de Livefyre es independiente de CMS.

**Método 1: Implementación del SDK**

* **Qué:** [Livefyre.js](https://docs.adobe.com/content/help/en/livefyre/implementation/c-livefyre_js.html) es la biblioteca principal que alimenta las aplicaciones y la autenticación en un sitio. Define el *window.Livefyre* y un único método público, *Livefyre.required*, que se puede utilizar para cargar otras bibliotecas JavaScript de Livefyre que ayuden a incrustar aplicaciones de Livefyre e integrarse con plataformas de autenticación de usuarios de terceros.

* **Cómo:**

   * Crear las revisiones [CollectionMeta token](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/c-reviews-integration.html) para especificar los metadatos que se guardarán en la colección de revisiones.
   * Integrar [Aplicación de revisiones](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/c-reviews-integration.html) en Sitios que usan la variable *Livefyre.js* estructura de código incrustado

* **Ejemplo:**  [https://codepen.io/dharafyre/pen/GXgvvd](https://codepen.io/dharafyre/pen/GXgvvd)

Para personalizaciones avanzadas con el SDK, consulte [SDK de StreamHub](https://github.com/Livefyre/streamhub-sdk).

**Método 2: Implementación de API**

* Para crear experiencias personalizadas y visualizaciones de datos, las aplicaciones de Livefyre se pueden crear desde cero consumiendo datos sociales y de Livefyre mediante el Bootstrap y la API de Stream.

Encontrará API de valoraciones y revisiones adicionales [here](https://api.livefyre.com/docs/apis/by-category/ratings-and-reviews).

### Integración de la autenticación de la aplicación de comentarios {#comments-app-authentication-integration-1}

* [Personalizar la integración del inicio de sesión único](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) para AEM Identity Management
* [Integración de identidad](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html) para plataformas de autenticación de terceros

### Ejemplos de clientes {#customer-examples-2}

* [Tiempo de expiración](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)
* [fórmulas](https://www.myrecipes.com/recipe/shrimp-florentine-pasta)
