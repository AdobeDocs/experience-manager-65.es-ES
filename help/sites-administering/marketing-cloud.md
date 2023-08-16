---
title: Integración con Adobe Experience Cloud
description: Obtenga información sobre cómo integrar Adobe Experience Manager con Adobe Experience Cloud.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: ba518290-dd82-44dc-ae7c-c8152df89179
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 4%

---

# Integración con Adobe Experience Cloud{#integrating-with-the-adobe-marketing-cloud}

El [Adobe Experience Cloud](https://business.adobe.com/products/marketing-cloud/main.html), incluye potentes análisis web y productos de optimización de sitios web que ofrecen datos y perspectivas procesables en tiempo real para impulsar iniciativas en línea exitosas. Ofrece una plataforma integrada y abierta para la optimización comercial en línea. La nube consiste en aplicaciones integradas para recopilar y liberar el poder de la perspectiva del cliente para optimizar los esfuerzos de adquisición, conversión y retención del cliente, así como la creación y distribución de contenido.

Con Adobe Experience Manager AEM (), puede integrarse fácilmente con los siguientes productos de Adobe Experience Cloud:

* Adobe Analytics proporciona a los especialistas en marketing información práctica en tiempo real sobre las estrategias en línea y las iniciativas de marketing.
* Adobe Target ofrece a los especialistas en marketing la capacidad de mejorar continuamente la relevancia de su contenido en línea para sus clientes, lo que resulta en una mayor conversión.
* Adobe Dynamic Media Classic automatiza la administración de medios, optimiza la publicación web y mejora las experiencias web, todo en un entorno alojado.
* Adobe Dynamic Tag Management ofrece a los especialistas en marketing herramientas intuitivas para administrar de forma rápida y sencilla un número ilimitado de etiquetas de Adobe y de terceros.
<!-- Search&Promote is end of life as of September 1, 2022 * Adobe Search&Promote gives marketers the ability to control and optimize the search results on their sites. -->
* Adobe Campaign permite administrar el contenido de las entregas por correo electrónico directamente en Adobe Experience Manager.

Además, puede [AEM integrar con Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) y con [servicios de terceros](/help/sites-administering/third-party-services.md).

## Integración con Adobe Analytics {#integrating-with-adobe-analytics}

[Adobe Analytics](https://business.adobe.com/products/analytics/adobe-analytics.html) es la solución líder del sector que proporciona a los especialistas en marketing digital un lugar para medir, analizar y optimizar los datos integrados de todas las iniciativas en línea en varios canales de marketing. Proporciona a los especialistas en marketing inteligencia de análisis web en tiempo real y procesable acerca de las estrategias digitales y las iniciativas de marketing. Adobe Analytics ayuda a los expertos en marketing a identificar rápidamente las rutas más rentables de un sitio web, dividir el tráfico en segmentos para detectar los visitantes web de mayor valor, determinar dónde abandonan el sitio los visitantes e identificar las métricas de éxito esenciales para las campañas de marketing en línea.

Puede utilizar Adobe Analytics para analizar los datos de sus sitios.

Al integrar con Adobe Analytics, puede hacer lo siguiente:

* Habilite el seguimiento de usuarios de Analytics.
* Asigne los modos de ejecución (por ejemplo, creación y publicación) a diferentes grupos de informes.
* Envíe variables de Client Context como variables de conversión o propiedades de tráfico.
* Utilice asignaciones de variables predefinidas.
* Configure secciones completas del sitio a la vez.
* Rastrear eventos definidos a medida.

AEM Para obtener información sobre la integración de los con Analytics, consulte [Integración con Adobe Analytics](/help/sites-administering/adobeanalytics.md).

También puede utilizar la variable [Asistente de inclusión](/help/sites-administering/opt-in.md) para realizar fácilmente la integración.

## Integración con Adobe Target {#integrating-with-adobe-target}

[Los especialistas en marketing utilizan Adobe Target para diseñar y ejecutar pruebas en línea, crear segmentos de audiencia sobre la marcha (basados en el comportamiento) y automatizar el direccionamiento del contenido y las experiencias en línea.](https://business.adobe.com/products/target/adobe-target.html)

Los consumidores en línea de hoy en día tienen necesidades en constante evolución y esperan contenido relevante, incluso personalizado, de la amplia variedad de sitios y fuentes de contenido que pueden elegir. Para atraer a una audiencia en línea, es fundamental que los especialistas en marketing en línea identifiquen rápidamente qué ofertas y contenido son relevantes y atractivos para sus audiencias. Armados con este conocimiento, los especialistas en marketing necesitan la capacidad de evolucionar continuamente sus sitios y dirigir el contenido adecuado a diferentes audiencias.

[Integración con Adobe Target](/help/sites-administering/target.md) explica cómo integrar su sitio con Target.

También puede utilizar la variable [Asistente de inclusión](/help/sites-administering/opt-in.md) para realizar fácilmente la integración.

## Inclusión en Analytics y Target {#opting-in-to-analytics-and-target}

AEM proporciona un procedimiento de inclusión sencillo para integrar con Adobe Analytics y Adobe Target. Cuando inicia sesión como administrador y visita la consola Proyectos, aparece un asistente de inclusión.

![chlimage_1-107](assets/chlimage_1-107a.png)

Opte por la integración con Analytics o Target para permitir el uso de las funcionalidades de seguimiento y análisis de páginas y de personalización. Cuando decida adherirse, proporcione la información de su cuenta de usuario y especifique las páginas de las que se realiza un seguimiento.

Para obtener más información, consulte [Inclusión en Adobe Analytics y Adobe Target.](/help/sites-administering/opt-in.md)

## Integración con Adobe Dynamic Media Classic {#integrating-with-scene}

Adobe Dynamic Media Classic es una solución alojada para publicar, administrar, mejorar y ofrecer recursos de marketing dinámico y comercialización visual enriquecida en web, móvil, correo electrónico, medios sociales, pantallas conectadas a Internet e impresión.

En Adobe Experience Manager, puede publicar recursos digitales directamente desde Adobe Experience Manager a Dynamic Media Classic y recursos digitales desde Dynamic Media Classic a Adobe Experience Manager.

Además, puede ver los recursos de Adobe Experience Manager publicados en Dynamic Media Classic en varios visores, como Zoom básico y Vídeo.

Para obtener más información sobre cómo Adobe Experience Manager se integra con Dynamic Media Classic, consulte la [Integración con Dynamic Media Classic](/help/sites-administering/scene7.md) documentación.

## Integración con Adobe Dynamic Tag Management {#integrating-with-adobe-dynamic-tag-management}

[Adobe Dynamic Tag Management](https://business.adobe.com/products/experience-platform/adobe-experience-platform.html) proporciona a los especialistas en marketing herramientas intuitivas para administrar rápida y fácilmente un número ilimitado de Adobes de y de terceros. Dispone de más control y flexibilidad para optimizar prácticamente cualquier elemento en línea, al tiempo que reduce la dependencia de los recursos de TI.

[Integración de Adobe con Dynamic Tag Management](/help/sites-administering/dtm.md) AEM con para que pueda utilizar sus propiedades web de Dynamic Tag Management AEM para realizar un seguimiento de los sitios de la.

## Integración con Adobe Audience Manager {#integrating-with-adobe-audience-manager}

La integración de Audience Manager AEM se ha eliminado en la versión 6.3 de la.

<!-- Search&Promote is end of life as of September 1, 2022 ## Integrating with Search&Promote {#integrating-with-search-promote} -->

<!-- Search&Promote is end of life as of September 1, 2022 Adobe Search&Promote enables marketers to optimizehow visitors browse, find, compare, and select relevant products and content on web and mobile sites. Businesses can easily promote priority items based on business objectives and visitor intent, as well as automate merchandising and promotions activity via KPI-based triggers or metrics. -->

<!-- Search&Promote is end of life as of September 1, 2022 Adobe Search&Promote is a reliable and scalable hosted site search application, capable of scaling to millions of pages or products, for heavily visited online businesses ranging from retail to news sites. It offers unprecedented levels of marketer control and metrics-based relevance. -->

<!-- Search&Promote is end of life as of September 1, 2022 For information about integrating AEM and Search&Promote, see [Integrating with Adobe Search&Promote](/help/sites-administering/search-and-promote.md). -->

## Integración con Adobe Campaign {#integrating-with-adobe-campaign}

[Adobe Campaign](https://business.adobe.com/products/campaign/adobe-campaign.html) permite administrar el contenido de las entregas de los correos electrónicos directamente en Adobe Experience Manager.

AEM Para obtener información sobre cómo se integra la con Adobe Campaign, consulte [Integración con Adobe Campaign](/help/sites-administering/campaignstandard.md).