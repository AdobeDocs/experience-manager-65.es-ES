---
title: Desarrollo sin objetivos para sitios AEM 6.5
description: Descubra cómo las potentes capacidades sin objetivos de AEM 6.5, como los modelos de contenido, los fragmentos de contenido y la API de GraphQL, colaboran para permitirle administrar sus experiencias de forma centralizada y servirlas en todos los canales.
exl-id: b6598bcf-b2ce-403a-87cf-6895fec8a91b
source-git-commit: ac70fb534a95c9eee6f8340d9b8720a607b9f79f
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 38%

---

# Desarrollo sin objetivos para sitios AEM 6.5 {#headless-development}

Descubra cómo las potentes capacidades sin objetivos de AEM 6.5, como los modelos de contenido, los fragmentos de contenido y la API de GraphQL, colaboran para permitirle administrar sus experiencias de forma centralizada y servirlas en todos los canales.

## Información general {#overview}

La implementación sin objetivos es cada vez más importante para ofrecer experiencias a su audiencia, independientemente del canal y dónde se encuentren.

La implementación sin encabezado renuncia a la administración de páginas y componentes, ya que es tradicional en soluciones híbridas y full-stack y se centra en la creación de fragmentos de contenido neutros para el canal y reutilizables y en su entrega multicanal. Es un patrón de desarrollo moderno y dinámico para implementar experiencias web.

![Modelos de implementación de AEM](/help/sites-developing/headless/getting-started/assets/aem-implementation-models.png)

## Comparación entre con encabezado y sin encabezado {#headful-headless}

Este documento se centra en el modelo completo de implementación sin objetivos de AEM. Sin embargo, con encabezado o sin encabezado no tiene por qué ser una elección binaria en AEM. Las funciones sin encabezado se pueden usar para administrar y entregar el contenido a una variedad de puntos finales, a la vez que permiten a los autores de contenido editar aplicaciones de una sola página. Todo en AEM.

>[!TIP]
>
>Consulte el documento [Con encabezado y sin encabezado en AEM](/help/sites-developing/headful-headless.md) para obtener más información.

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
1. API de contenido para entrega
   * La API de GraphQL de AEM es compatible con la entrega de fragmentos de contenido.
   * La API de REST de AEM Assets es compatible con las operaciones de CRUD de fragmento de contenido.
   * La entrega de contenido directo también es posible con el [Exportación JSON del componente principal del fragmento de contenido.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=es)

## Primeros pasos con AEM Headless {#first-steps}

Hay varios recursos disponibles para que su usuario comience con AEM funciones sin encabezado. Están pensados para diferentes casos de uso, pero todos ofrecen una visión general sólida de AEM funciones sin encabezado.

| Recurso | Descripción | Tipo | Audiencia | EST Hora |
|---|---|---|---|---|
| [Recorrido para desarrolladores de Headless](/help/journey-headless/developer/overview.md) | **Para usuarios nuevos a AEM y sin periféricos** tecnologías, empiecen aquí por una introducción completa a la AEM y sus características sin cabeza de la teoría de no tener cabeza a través de vivir con su primer proyecto sin cabeza. | Guía  | Desarrolladores **nuevos en las tecnologías de AEM y sin encabezado** | 1 hora |
| [Guía de introducción de Headless](/help/sites-developing/headless/getting-started/introduction.md) | **Para usuarios de AEM con experiencia** que necesiten un breve resumen de las funciones principales de AEM sin encabezado, se recomienda consultar esta descripción general de inicio rápido. | Inicio rápido | Desarrolladores, administradores **con experiencia en AEM** | 20 minutos |
| [Tutorial práctico Introducción a AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=es) | **Si prefiere un enfoque práctico y está familiarizado con AEM**, este tutorial se sumerge directamente en la creación de un proyecto sencillo sin encabezado. | Tutorial | Desarrolladores | 2 horas |
