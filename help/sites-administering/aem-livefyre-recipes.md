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
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 4%

---

# Fórmulas de AEM Livefyre{#aem-livefyre-recipes}

Instrucciones paso a paso sobre casos de uso común de Adobe Experience Manager Livefyre.

## AEM Depure UGC con los componentes listos para usar de Livefyre y la visualización de UGC mediante el Muro de medios de Livefyre. {#curate-ugc-using-the-out-of-the-box-livefyre-aem-components-and-display-using-livefyre-media-wall}

El muro de medios transmite contenido social y nativo de Livefyre a un muro social en tiempo real. AEM Existen varias formas de implementar el muro de medios en los entornos de trabajo en función de su caso de uso y de sus requisitos.

AEM AEM El paquete de Livefyre proporciona una implementación predeterminada, mientras que la integración tradicional ofrece la capacidad de crear componentes personalizados de Livefyre.

### AEM Integración de {#aem-integration}

El paquete de Adobe Experience Manager AEM de Livefyre está disponible para las versiones 6.1, 6.2SP1, 6.3, 6.4 y 6.4 SP1, respectivamente. AEM No se admiten las versiones 5.x y 6.0 de. Para obtener instrucciones detalladas, consulte [Integración con Livefyre](https://helpx.adobe.com/es/experience-manager/6-4/sites/administering/using/livefyre.html).

Para ver qué aplicaciones de Livefyre son compatibles, consulte las [AEM Matriz de soporte para aplicaciones de Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### AEM Implementación tradicional (para componentes personalizados de la) {#traditional-implementation-for-customized-aem-components}

AEM Existen tres maneras de implementar Livefyre en un componente personalizado de la aplicación de la aplicación o en otros CMS como WordPress, Sitecore o DemandWare. Una integración tradicional de Livefyre no depende de CMS.

**Método 1: Implementación de la aplicación de Designer**

* **Qué:** La forma más sencilla y rápida de integrar una aplicación de Livefyre. Puede diseñar, configurar y generar un código incrustado de JavaScript personalizado para integrar una aplicación de muro de medios en una página en minutos.
* **Cómo:**  [Crear, previsualizar, publicar e incrustar una aplicación de muro de medios](https://experienceleague.adobe.com/docs/livefyre/using/apps/c-create-an-app.html)

* **Ejemplo:** [https://codepen.io/dharafyre/pen/bvGrLo](https://codepen.io/dharafyre/pen/bvGrLo)

**Método 2: Implementación del SDK**

* **Qué:** [Livefyre.js](https://experienceleague.adobe.com/docs/livefyre/implementation/c-livefyre_js.html) es la biblioteca principal que alimenta las aplicaciones y la autenticación en un sitio. Define la configuración global *window.Livefyre* y un único método público, *Livefyre.require*, que se puede utilizar para cargar otras bibliotecas de JavaScript de Livefyre que ayudan a incrustar aplicaciones de Livefyre e integrarlas con plataformas de autenticación de usuarios de terceros.

* **Cómo**: [Utilice el paquete streamhub-wallpackage del SDK de JavaScript de Livefyre](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/c-media-wall-integration.html)

* **Ejemplo**: [https://codepen.io/dharafyre/pen/KZKBNv?editors=1010](https://codepen.io/dharafyre/pen/KZKBNv?editors=1010)

Para realizar personalizaciones avanzadas mediante el SDK, consulte [SDK de StreamHub](https://github.com/Livefyre/streamhub-sdk).

**Método 3: Implementación de API**

* Para crear experiencias personalizadas y visualizaciones de datos, las aplicaciones de Livefyre se pueden crear desde cero consumiendo datos sociales y de Livefyre mediante [API de Bootstrap y flujo](https://experienceleague.adobe.com/docs/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

Asegúrese de seguir [Twitter](https://developer.twitter.com/en/developer-terms/display-requirements.html), [Facebook](https://en.facebookbrand.com/guidelines/brand), y [Instagram](https://en.instagram-brand.com/) mostrar directrices al crear la interfaz de usuario para UGC.

### Integración de autenticación de muro de medios {#media-wall-authentication-integration}

Para integraciones de muro de medios que requieran autenticación, consulte:

* [Personalizar integración de inicio de sesión único](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) AEM para Identity Management
* [Integración de identidad](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) para plataformas de autenticación de terceros

### Resumen de casos de uso {#use-case-overview}

AEM AEM Como cliente de Livefyre, quiero depurar UGC utilizando los componentes listos para usar de Livefyre, así como mostrar el muro de medios de Livefyre:

Pasos para implementar:

1. [Introducción](https://helpx.adobe.com/es/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [AEM Configuración del uso de Livefyre por parte de los](https://helpx.adobe.com/es/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [AEM Arrastre y suelte el componente Muro de medios en la página](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMSites)
1. [Configurar flujos y agregar reglas para depurar UGC y mostrarlos en el componente Muro de medios](https://experienceleague.adobe.com/docs/livefyre/using/streams/c-streams.html)

Para ver vídeos de formación sobre el flujo UGC, consulte [Creación de flujos de contenido automáticos y búsqueda de contenido social en Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

### Ejemplos de clientes {#customer-examples}

* [Muro de medios CNN](https://edition.cnn.com/specials/nepal-earthquake-media-wall)
* [Muro de medios de PGA Tour](https://www.pgatour.com/social-hub.html)

Para crear experiencias personalizadas y visualizaciones de datos, las aplicaciones de Livefyre se pueden crear desde cero consumiendo datos sociales y de Livefyre mediante [API de Bootstrap y flujo](https://experienceleague.adobe.com/docs/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

Para las aplicaciones de Livefyre que requieren autenticación, consulte [Integración de identidad](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) para plataformas de autenticación de terceros.

* [Muro de medios de PGA Tour](https://www.pgatour.com/social-hub.html)
* [Tiempo de expiración](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)

## AEM Integración de comentarios de Livefyre mediante componentes de o la integración tradicional de Livefyre {#integrate-livefyre-comments-using-aem-components-or-traditional-livefyre-integration}

### AEM Integración de {#aem-integration-1}

El paquete de Adobe Experience Manager AEM de Livefyre está disponible para las versiones 6.1, 6.2SP1, 6.3, 6.4 y 6.4 SP1, respectivamente. AEM No se admiten las versiones 5.x y 6.0 de. Para obtener instrucciones detalladas, consulte [Integración con Livefyre](https://helpx.adobe.com/es/experience-manager/6-4/sites/administering/using/livefyre.html).

### AEM Implementación tradicional (para componentes personalizados de la) {#traditional-implementation-for-customized-aem-components-1}

AEM Existen tres maneras de implementar la aplicación de comentarios de Livefyre en un componente de personalizado u otros CMS como WordPress, Sitecore o DemandWare. Una integración tradicional de Livefyre no depende de CMS.

**Método 1: Implementación de la aplicación de Designer**

* **Qué:** La forma más sencilla y rápida de integrar una aplicación de Livefyre. Puede diseñar, configurar y generar un código incrustado de JavaScript personalizado para integrar una aplicación de muro de medios en una página en minutos.
* **Cómo:** [Crear, previsualizar, publicar e incrustar una aplicación de comentarios](https://experienceleague.adobe.com/docs/livefyre/using/apps/c-create-an-app.html)

* **Ejemplo:** [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

**Método 2: Implementación del SDK**

* **Qué:** [Livefyre.js](https://experienceleague.adobe.com/docs/livefyre/implementation/c-livefyre_js.html) es la biblioteca principal que alimenta las aplicaciones y la autenticación en un sitio. Define la configuración global *window.Livefyre* y un único método público, *Livefyre.require*, que se puede utilizar para cargar otras bibliotecas de JavaScript de Livefyre que ayudan a incrustar aplicaciones de Livefyre e integrarlas con plataformas de autenticación de usuarios de terceros.

* **Cómo:**

   * Crear una colección/aplicación mediante [Token de CollectionMeta](https://experienceleague.adobe.com/docs/livefyre/implementation/getting-started/implementation-process/c-collectionmeta-tokent.html).
   * Integrar [Aplicación de comentarios](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/comments/c-comments-integration.html) en sitios mediante la estructura de código incrustado de Livefyre.js.

* **Ejemplo:**  [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

Para obtener personalizaciones avanzadas mediante el SDK, consulte [SDK de StreamHub](https://github.com/Livefyre/streamhub-sdk).

**Método 3: Implementación de API**

* Para crear experiencias personalizadas y visualizaciones de datos, las aplicaciones de Livefyre se pueden crear desde cero consumiendo datos sociales y de Livefyre mediante [API de Bootstrap y flujo](https://experienceleague.adobe.com/docs/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

### Integración de autenticación de aplicación de comentarios {#comments-app-authentication-integration}

* [Personalizar integración de inicio de sesión único](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) AEM para Identity Management
* [Integración de identidad](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) para plataformas de autenticación de terceros

### Ejemplos de clientes {#customer-examples-1}

* [Poise (Kimberly Klark)](https://www.poise.com/en-us/advice-and-support/blog-and-podcast/blog/5-holiday-party-tips-for-managing-lbl)

## Uso de la integración de AEM Assets de Livefyre para importar UGC en AEM Assets {#use-livefyre-aem-assets-integration-to-import-ugc-in-aem-assets}

**Configuración de Livefyre (para revisión y Rights Management de UGC):**

1. [Configurar flujos y agregar reglas para depurar UGC en las carpetas de la biblioteca de recursos de Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/streams/c-streams.html).

   1. Para ver vídeos de formación sobre el flujo UGC, consulte [Creación de flujos de contenido automáticos y búsqueda de contenido social en Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Recopile, organice y administre UGC depurados en carpetas de la biblioteca de recursos de Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/library/assets/c-assets.html).

   1. Para ver vídeos de formación sobre la creación y administración de carpetas en la biblioteca de recursos de Livefyre Studio, consulte [Uso de recursos en Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Solicite los derechos de UGC depurado mediante Livefyre Studio](https://experienceleague.adobe.com/docs/livefyre/using/rights-requests/c-how-requesting-rights-works.html).

**AEM Configuración de la (para importar UGC en AEM Assets):**

1. [Introducción](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#GettingStarted)
1. [AEM Configuración del uso de Livefyre por parte de los](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#ConfigureAEMtouseLivefyre)
1. [Importar UGC seleccionados por Livefyre en AEM Assets](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMAssets)

* [Turismo en Australia](https://www.australia.com/en-us)

## AEM Integración de revisiones de Livefyre mediante componentes de o la integración tradicional de Livefyre {#integrate-livefyre-reviews-using-aem-components-or-traditional-livefyre-integration}

### AEM Integración de {#aem-integration-2}

El paquete de Adobe Experience Manager AEM de Livefyre está disponible para las versiones 6.1, 6.2SP1, 6.3, 6.4 y 6.4 SP1, respectivamente. AEM No se admiten las versiones 5.x y 6.0 de. Para obtener instrucciones detalladas, consulte [Integración con Livefyre](https://helpx.adobe.com/es/experience-manager/6-4/sites/administering/using/livefyre.html).

AEM El componente Revisiones no es un componente compatible con la versión 6.1 de la. Compruebe el [AEM Matriz de soporte de la aplicación para todas las aplicaciones de Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### AEM Implementación tradicional (para componentes personalizados de la) {#traditional-implementation-for-customized-aem-components-2}

AEM Existen dos maneras de implementar la aplicación Livefyre Reviews en un componente de la aplicación personalizada de la aplicación o en otros CMS como WordPress, Sitecore o DemandWare. Una integración tradicional de Livefyre no depende de CMS.

**Método 1: Implementación del SDK**

* **Qué:** [Livefyre.js](https://experienceleague.adobe.com/docs/livefyre/implementation/c-livefyre_js.html) es la biblioteca principal que alimenta las aplicaciones y la autenticación en un sitio. Define la configuración global *window.Livefyre* y un único método público, *Livefyre.require*, que se puede utilizar para cargar otras bibliotecas de JavaScript de Livefyre que ayudan a incrustar aplicaciones de Livefyre e integrarlas con plataformas de autenticación de usuarios de terceros.

* **Cómo:**

   * Creación de críticas [Token de CollectionMeta](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/c-reviews-integration.html) para especificar los metadatos que se almacenarán en la colección Reviews.
   * Integrar [Aplicación de críticas](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/c-reviews-integration.html) en Sitios mediante el *Livefyre.js* estructura de código incrustado

* **Ejemplo:**  [https://codepen.io/dharafyre/pen/GXgvvd](https://codepen.io/dharafyre/pen/GXgvvd)

Para obtener personalizaciones avanzadas mediante el SDK, consulte [SDK de StreamHub](https://github.com/Livefyre/streamhub-sdk).

**Método 2: Implementación de API**

* Para crear experiencias personalizadas y visualizaciones de datos, las aplicaciones de Livefyre se pueden crear desde cero consumiendo datos sociales y de Livefyre mediante las API de Bootstrap y Stream.

Se pueden encontrar API de valoraciones y revisiones adicionales [aquí](https://api.livefyre.com/docs/apis/by-category/ratings-and-reviews).

### Integración de autenticación de aplicación de comentarios {#comments-app-authentication-integration-1}

* [Personalizar integración de inicio de sesión único](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) AEM para Identity Management
* [Integración de identidad](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) para plataformas de autenticación de terceros

### Ejemplos de clientes {#customer-examples-2}

* [Tiempo de expiración](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)
* [mirecetas](https://www.myrecipes.com/recipe/shrimp-florentine-pasta)
