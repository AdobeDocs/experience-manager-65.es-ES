---
title: 'Desarrollo sin objetivos para sitios AEM 6.5 '
description: Descubra cómo las potentes capacidades sin objetivos de AEM 6.5, como los modelos de contenido, los fragmentos de contenido y la API de GraphQL, funcionan juntos para permitirle administrar sus experiencias de forma centralizada y servirlas en todos los canales.
source-git-commit: 2f400d209148278f0695f7b9523b58bba6845cfb
workflow-type: tm+mt
source-wordcount: '493'
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

>[!TIP]
>
>Consulte el documento [Encabezado y sin cabeza en AEM](/help/sites-developing/headful-headless.md) para obtener más información.

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
| [Recorrido para desarrolladores sin objetivos](/help/journey-headless/developer/overview.md) | **Para usuarios nuevos a AEM y sin periféricos** tecnologías, empiecen aquí por una introducción completa a la AEM y sus características sin cabeza de la teoría de no tener cabeza a través de vivir con su primer proyecto sin cabeza. | Guía | Desarrolladores **nuevo en AEM y sin cabeza** | 1 hora |
| [Guía de introducción sin encabezado](/help/sites-developing/headless/getting-started/introduction.md) | **Para usuarios AEM con experiencia** para obtener un breve resumen de las funciones principales AEM sin encabezado, consulte esta descripción general de inicio rápido. | Inicio rápido | Desarrolladores, administradores **con AEM experiencia** | 20 minutos |
| [Tutorial práctico Introducción a AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | **Si prefiere un enfoque práctico y está familiarizado con AEM**, este tutorial se sumerge directamente en la creación de un proyecto sencillo sin encabezado. | Tutorial | Desarrolladores | 2 horas |
