---
title: Asignación dinámica de modelo a componente para SPA
seo-title: Asignación dinámica de modelo a componente para SPA
description: En este artículo se describe cómo se produce la asignación de modelos dinámicos a componentes en el SDK de SPA de JavaScript para AEM.
seo-description: En este artículo se describe cómo se produce la asignación de modelos dinámicos a componentes en el SDK de SPA de JavaScript para AEM.
uuid: 337b8d90-efd7-442e-9fac-66c33cc26212
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 8b4b0afc-8534-4010-8f34-cb10475a8e79
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# Asignación dinámica de modelo a componente para SPA{#dynamic-model-to-component-mapping-for-spas}

En este documento se describe cómo se produce la asignación de modelos dinámicos a componentes en el SDK de SPA de Javascript para AEM.

>[!NOTE]
>
>El Editor de SPA es la solución recomendada para proyectos que requieren SPA procesamiento del lado del cliente basado en el marco de trabajo (por ejemplo, React o Angular).

## Módulo ComponentMapping {#componentmapping-module}

El módulo `ComponentMapping` se proporciona como paquete NPM al proyecto front-end. Almacena componentes front-end y proporciona una forma para que la aplicación de una sola página asigne componentes front-end a AEM tipos de recursos. Esto permite una resolución dinámica de los componentes al analizar el modelo JSON de la aplicación.

Cada elemento presente en el modelo contiene un campo `:type` que expone un tipo de recurso AEM. Cuando se monta, el componente front-end puede procesarse utilizando el fragmento de modelo que ha recibido de las bibliotecas subyacentes.

Consulte el documento [SPA modelo](/help/sites-developing/spa-blueprint.md) para obtener más información sobre el análisis de modelos y el acceso de componentes front-end al modelo.

Consulte también el paquete npm: [https://www.npmjs.com/package/@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## Aplicación de página única basada en modelo {#model-driven-single-page-application}

Las aplicaciones de una sola página que utilizan el SDK de SPA de Javascript para AEM están basadas en modelos:

1. Los componentes front-end se registran en el [Almacenamiento de asignación de componentes](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module).
1. A continuación, el [Contenedor](/help/sites-developing/spa-blueprint.md#container), una vez proporcionado con un modelo por el [Proveedor del modelo](/help/sites-developing/spa-blueprint.md#the-model-provider), se repite sobre su contenido del modelo ( `:items`).

1. En el caso de una página, sus elementos secundarios ( `:children`) primero obtienen una clase de componente de la [Asignación de componentes](/help/sites-developing/spa-blueprint.md#componentmapping) y luego la instancian.

## Inicialización de la aplicación {#app-initialization}

Cada componente se amplía con las capacidades de [ `ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider). Por consiguiente, la inicialización tiene la siguiente forma general:

1. Cada proveedor de modelos se inicializa y escucha los cambios realizados en la pieza del modelo que corresponde a su componente interior.
1. El [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) debe inicializarse como representado por el [flujo de inicialización](/help/sites-developing/spa-blueprint.md).

1. Una vez almacenado, el administrador de modelos de página devuelve el modelo completo de la aplicación.
1. A continuación, este modelo se pasa al componente raíz [Contenedor](/help/sites-developing/spa-blueprint.md#container) del front-end de la aplicación.
1. Las partes del modelo se propagan finalmente a cada componente secundario individual.

![app_model_initialize](assets/app_model_initialization.png)

