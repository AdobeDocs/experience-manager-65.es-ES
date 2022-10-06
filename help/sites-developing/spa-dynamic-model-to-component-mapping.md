---
title: Asignación de modelos dinámicos a componentes para SPA
seo-title: Dynamic Model to Component Mapping for SPAs
description: En este artículo se describe cómo se produce la asignación del modelo dinámico a los componentes en el SDK de SPA de JavaScript para AEM.
seo-description: This article describes how the dynamic model to component mapping occurs in the Javascript SPA SDK for AEM.
uuid: 337b8d90-efd7-442e-9fac-66c33cc26212
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 8b4b0afc-8534-4010-8f34-cb10475a8e79
exl-id: 5b2ccac0-bf1d-4f06-8743-7fce6fb68378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# Asignación de modelos dinámicos a componentes para SPA{#dynamic-model-to-component-mapping-for-spas}

En este documento se describe cómo se produce la asignación de modelos dinámicos a componentes en el SDK de SPA de JavaScript para AEM.

>[!NOTE]
>
>El Editor de SPA es la solución recomendada para proyectos que requieren SPA procesamiento del lado del cliente basado en el marco de trabajo (por ejemplo, React o Angular).

## Módulo ComponentMapping {#componentmapping-module}

La variable `ComponentMapping` se proporciona como paquete NPM al proyecto front-end. Almacena componentes front-end y proporciona una forma para que la aplicación de una sola página asigne componentes front-end a AEM tipos de recursos. Esto permite una resolución dinámica de los componentes al analizar el modelo JSON de la aplicación.

Cada elemento presente en el modelo contiene un `:type` campo que muestra un tipo de recurso AEM. Cuando se monta, el componente frontal puede procesarse utilizando el fragmento de modelo que ha recibido de las bibliotecas subyacentes.

Consulte la [Modelo SPA](/help/sites-developing/spa-blueprint.md) documento para obtener más información sobre el análisis de modelos y el acceso de componentes front-end al modelo.

Consulte también el paquete npm: [https://www.npmjs.com/package/@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## Aplicación de página única impulsada por modelo {#model-driven-single-page-application}

Las aplicaciones de una sola página que aprovechan el SDK de SPA de Javascript para AEM están basadas en modelos:

1. Los componentes del front-end se registran a sí mismos en el [Almacén de asignación de componentes](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module).
1. A continuación, el [Contenedor](/help/sites-developing/spa-blueprint.md#container), una vez que el [Proveedor de modelo](/help/sites-developing/spa-blueprint.md#the-model-provider), se repite sobre el contenido del modelo ( `:items`).

1. En el caso de una página, sus elementos secundarios ( `:children`) obtenga primero una clase de componente de la [Asignación de componentes](/help/sites-developing/spa-blueprint.md#componentmapping) y luego instancie.

## Inicialización de la aplicación {#app-initialization}

Cada componente se amplía con las capacidades del [ `ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider). Por lo tanto, la inicialización adopta la siguiente forma general:

1. Cada proveedor de modelos se inicializa y escucha los cambios realizados en la pieza del modelo que corresponde a su componente interno.
1. La variable [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) debe inicializarse tal y como lo representa el [flujo de inicialización](/help/sites-developing/spa-blueprint.md).

1. Una vez almacenado, el administrador del modelo de página devuelve el modelo completo de la aplicación.
1. Este modelo se pasa entonces a la raíz del front-end [Contenedor](/help/sites-developing/spa-blueprint.md#container) de la aplicación.
1. Los fragmentos del modelo se propagan finalmente a cada componente secundario individual.

![app_model_initialize](assets/app_model_initialization.png)
