---
title: SPA Asignación de modelos dinámicos a componentes para la creación de
seo-title: Dynamic Model to Component Mapping for SPAs
description: SPA AEM En este artículo se describe cómo se produce la asignación de modelos dinámicos a componentes en el SDK de Javascript para la de la aplicación.
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

# SPA Asignación de modelos dinámicos a componentes para la creación de{#dynamic-model-to-component-mapping-for-spas}

SPA AEM En este documento se describe cómo se produce la asignación de modelos dinámicos a componentes en el SDK de Javascript para la creación de.

>[!NOTE]
>
>SPA SPA El editor de segmentos es la solución recomendada para los proyectos que requieren un procesamiento basado en el marco de trabajo del cliente basado en el marco de trabajo de la aplicación (por ejemplo, React o Angular).

## Módulo de asignación de componentes {#componentmapping-module}

El `ComponentMapping` El módulo se proporciona como paquete NPM al proyecto front-end. AEM Almacena componentes front-end y proporciona una forma para que la aplicación de una sola página asigne componentes front-end a tipos de recursos de. Esto permite una resolución dinámica de componentes al analizar el modelo JSON de la aplicación.

Cada elemento presente en el modelo contiene un `:type` AEM campo que expone un tipo de recurso de. Cuando se monta, el componente front-end puede representarse a sí mismo utilizando el fragmento de modelo que ha recibido de las bibliotecas subyacentes.

Consulte la [SPA Modelo de](/help/sites-developing/spa-blueprint.md) para obtener más información sobre el análisis del modelo y el acceso del componente front-end al modelo.

Consulte también el paquete npm: [https://www.npmjs.com/package/@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## Aplicación de una sola página impulsada por modelo {#model-driven-single-page-application}

SPA AEM Las aplicaciones de una sola página que aprovechan el SDK de Javascript para la creación de informes de usuarios para la creación de informes están basadas en modelos:

1. Los componentes front-end se registran en el [Almacén de asignación de componentes](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module).
1. A continuación, el [Contenedor](/help/sites-developing/spa-blueprint.md#container), una vez proporcionada con un modelo por el [Proveedor de modelo](/help/sites-developing/spa-blueprint.md#the-model-provider), se repite sobre el contenido de su modelo ( `:items`).

1. En el caso de una página, sus elementos secundarios ( `:children`) obtenga primero una clase de componente del [Asignación de componentes](/help/sites-developing/spa-blueprint.md#componentmapping) y luego instanciarlo.

## Inicialización de aplicaciones {#app-initialization}

Cada componente se amplía con las capacidades del [ `ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider). Por lo tanto, la inicialización adopta la siguiente forma general:

1. Cada proveedor de modelos se inicializa a sí mismo y escucha los cambios realizados en el fragmento de modelo que corresponde a su componente interno.
1. El [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) se debe inicializar tal como lo representa el [flujo de inicialización](/help/sites-developing/spa-blueprint.md).

1. Una vez almacenado, el administrador de modelos de página devuelve el modelo completo de la aplicación.
1. Este modelo se pasa a la raíz del front-end [Contenedor](/help/sites-developing/spa-blueprint.md#container) componente de la aplicación.
1. Las partes del modelo finalmente se propagan a cada componente secundario individual.

![app_model_initialization](assets/app_model_initialization.png)
