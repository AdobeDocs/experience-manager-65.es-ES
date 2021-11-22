---
title: 'Desarrollo sin objetivos para sitios AEM 6.5 '
description: Descubra cómo las potentes capacidades sin objetivos de AEM 6.5, como los modelos de contenido, los fragmentos de contenido y la API de GraphQL, funcionan juntos para permitirle administrar sus experiencias de forma centralizada y servirlas en todos los canales.
source-git-commit: 8c7acd06f3909897e5756170c606e00aead098b8
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 2%

---


# Desarrollo sin objetivos para sitios AEM 6.5 {#headless-development}

Descubra cómo las potentes capacidades sin objetivos de AEM 6.5, como los modelos de contenido, los fragmentos de contenido y la API de GraphQL, funcionan juntos para permitirle administrar sus experiencias de forma centralizada y servirlas en todos los canales.

## Información general {#overview}

La implementación sin objetivos es cada vez más importante para ofrecer experiencias a su audiencia, independientemente del canal y dónde se encuentren.

La implementación sin encabezado renuncia a la administración de páginas y componentes, ya que es tradicional en soluciones híbridas y de pila completas y se centra en la creación de fragmentos de contenido neutros para el canal y reutilizables y su envío por canales cruzados. Es un patrón de desarrollo moderno y dinámico para implementar experiencias web.

![Modelos de implementación de AEM](assets/aem-implementation-models.png)

## Comparación de encabezados y sin encabezado {#headful-headless}

Este documento se centra en el modelo completo de implementación sin objetivos de AEM. Sin embargo, la cabeza contra la cabeza no tiene por qué ser una elección binaria en AEM. Las funciones sin encabezado se pueden usar para administrar y entregar el contenido a una variedad de puntos finales, a la vez que permiten a los autores de contenido editar aplicaciones de una sola página. Todo en AEM.

<!--
>[!TIP]
>
>See the document [Headful and Headless in AEM](/help/implementing/developing/headful-headless.md) for more information.
-->

## AEM 6.5 y sin encabezado {#aem-headless}

AEM 6.5 es una herramienta flexible para el modelo de implementación sin objetivos que ofrece tres servicios potentes:

1. Modelos de contenido
   * Los modelos de contenido son una representación estructurada del contenido.
   * Se definen mediante arquitectos de información en el editor del Modelo de fragmento de contenido de AEM.
   * Los modelos de contenido sirven de base para los fragmentos de contenido.
1. Fragmentos de contenido
   * Los fragmentos de contenido son instancias de modelos de contenido.
   * Los crean los autores de contenido mediante el editor de fragmentos de contenido de AEM.
   * Se almacenan en AEM Assets y se administran en la interfaz de usuario del administrador de recursos.
1. API de contenido para envío
   * La API de AEM GraphQL es compatible con la entrega de fragmentos de contenido.
   * La API de REST de AEM Assets es compatible con las operaciones de CRUD de fragmento de contenido.
   * La entrega de contenido directo también es posible con el [Exportación JSON del componente principal del fragmento de contenido.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)

## Sus primeros pasos con AEM sin encabezado {#first-steps}

Hay varios recursos disponibles para que su usuario comience con AEM funciones sin encabezado. Están pensados para diferentes casos de uso, pero todos ofrecen una visión general sólida de AEM funciones sin encabezado.

| Medio | Descripción | Tipo | Audience | Este. Hora |
|---|---|---|---|---|
| [Tutorial práctico Introducción a AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | **Si prefiere un enfoque práctico y está familiarizado con AEM**, este tutorial se sumerge directamente en la creación de un proyecto sencillo sin encabezado. | Tutorial | Desarrolladores | 2 horas |

<!--
|Resource|Description|Type|Audience|Est. Time|
|---|---|---|---|---|
|[Headless Developer Journey](/help/journey-headless/developer/overview.md)|**For users new to AEM and headless** technologies, start here for a comprehensive introduction to AEM and its headless features from the theory of headless through going live with your first headless project.|Guide|Developers **new to AEM and headless**|1 hour|
|[Headless Getting Started Guide](/help/implementing/developing/headless/getting-started/introduction.md)|**For experienced AEM users** who need a short summary of the key AEM headless features, check out this quick start overview.|Quick Start|Developers, Administrators **with AEM experience**|20 minutes|
|[Getting Started with AEM Headless hands-on tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html)|**If you prefer a hands-on approach and are familiar with AEM**, this tutorial dives directly into creating a simple headless project.|Tutorial|Developers|2 hours|
-->
