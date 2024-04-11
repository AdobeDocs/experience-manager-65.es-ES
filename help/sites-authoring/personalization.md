---
title: Personalización y segmentación de contenido
description: Descubra cómo Adobe Experience Manager 6.5 puede crear contenido personalizado.
exl-id: be34760a-875b-419d-9fa4-2359b314a3b7
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 36%

---

# Personalización y targeting de contenido {#personalization}

## Personalización y segmentación de contenido {#personalization-and-content-targeting}

AEM proporciona un marco de herramientas para crear contenido dirigido y presentar experiencias personalizadas.

## Modo Targeting {#targeting-mode}

[Contenido orientado por el autor mediante el modo de Orientación de AEM. ](/help/sites-authoring/content-targeting-touch.md) En el modo segmentación y el componente de Target se proporcionan las herramientas necesarias para crear contenido para las experiencias de las actividades de marketing.

## Actividades {#activities}

Las actividades definen y organizan los esfuerzos de marketing. Las actividades comprenden las audiencias a las que se dirige y el período de tiempo en que se aplica el objetivo.

Por ejemplo, el catálogo de productos We.Retail incluye teasers que destacan los productos de temporada. La actividad Deportes de verano define los segmentos de marketing a los que se dirigen los teasers durante los meses de verano.

Las actividades también identifican el [motor de segmentación](/help/sites-authoring/personalization.md#targeting-engine) que utilizan sus páginas.

Utilice el [Consola Actividades](/help/sites-authoring/activitylib.md) para crear y administrar las actividades de sus marcas. También puede crear actividades a medida que [crea contenido de destino](/help/sites-authoring/content-targeting-touch.md).

## Experiencias {#experiences}

Para cada actividad, se definen una o más experiencias que identifican las audiencias a las que se va a dirigir. AEM permite controlar el contenido de que consta cada experiencia.

AEM Las audiencias se basan en segmentos de marketing creados en o Adobe Target. Cuando un visitante abre una página web, la lógica de la página determina la audiencia a la que pertenece y muestra el contenido que ha creado para esa audiencia.

Por ejemplo, una actividad define las experiencias para dos audiencias independientes: mujeres mayores de 30 años y mujeres menores de 30 años. La página para mujeres del sitio web de We.Retail muestra diferentes productos para cada experiencia.

Las experiencias se definen para una actividad. Puede usar el complemento [Consola Actividades](/help/sites-authoring/activitylib.md#adding-editing-an-activity-using-the-activities-console) o [Modo Targeting](/help/sites-authoring/content-targeting-touch.md#adding-and-removing-experiences-using-targeting-mode) para añadir experiencias a una actividad.

## Ofertas {#offers}

Una oferta es contenido que aparece en una ubicación de una página para una experiencia. Utilice distintas ofertas para diferentes experiencias a fin de maximizar la eficacia del contenido para las audiencias.

Por ejemplo, la página para mujeres del sitio web de muestra de We.Retail puede utilizar ofertas para la imagen de teaser que aparece en la parte superior de la página. Se utiliza una oferta diferente como teaser para la experiencia de mujeres mayores de 30 años y de mujeres menores de 30 años.

Utilice el [Consola Ofertas](/help/sites-authoring/offerlib.md) para crear ofertas que se puedan usar en varias experiencias. Crear ofertas de un solo uso o agregar ofertas desde una biblioteca de ofertas cuando [creación de contenido de destino](/help/sites-authoring/content-targeting-touch.md).

## Motor de segmentación {#targeting-engine}

El motor de segmentación es el mecanismo que determina la lógica para el contenido de destino. Las [actividades](/help/sites-authoring/activitylib.md) se configuran para utilizar uno de estos dos motores de segmentación disponibles: AEM y Adobe Target.

### AEM {#aem}

AEM proporciona un motor de segmentación integrado que procesa las solicitudes de páginas y determina el contenido que se va a mostrar. Al utilizar el motor de segmentación de AEM, el uso se limita a los segmentos que se crean en AEM para definir las audiencias de las experiencias.

### Adobe Target {#adobe-target}

El motor de segmentación de Adobe Target hace que la información recopilada de las visitas a la página sean rastreadas en Adobe Target.

* Al utilizar este motor de segmentación, se usan los segmentos importados de Adobe Target para definir los públicos para las experiencias.
* Las actividades que utilizan el motor de Adobe Target se [sincronizan con Target](/help/sites-authoring/activitylib.md#synchronizing-activities-with-adobe-target).

Puede utilizar este motor cuando se haya [integrado con Adobe Target](/help/sites-administering/opt-in.md).
