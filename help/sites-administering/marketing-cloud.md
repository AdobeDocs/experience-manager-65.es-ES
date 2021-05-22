---
title: Integración con Adobe Marketing Cloud
description: Aprenda a integrar Adobe Experience Manager con Adobe Marketing Cloud.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: ba518290-dd82-44dc-ae7c-c8152df89179
source-git-commit: d19b203ffe75a5628f350113d4d74a2916beffc8
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 1%

---

# Integración con Adobe Marketing Cloud{#integrating-with-the-adobe-marketing-cloud}

El [Adobe Marketing Cloud](https://www.adobe.com/solutions/digital-marketing.html) incluye potentes productos de optimización de análisis web y sitios web que ofrecen datos y perspectivas procesables en tiempo real para impulsar iniciativas en línea exitosas. Ofrece una plataforma integrada y abierta para la optimización empresarial en línea. La nube consiste en aplicaciones integradas para recopilar y liberar el poder de la perspectiva del cliente para optimizar los esfuerzos de adquisición, conversión y retención del cliente, así como la creación y distribución del contenido.

Con Adobe Experience Manager (AEM), puede integrarse perfectamente con los siguientes productos de Adobe Marketing Cloud:

* Adobe Analytics proporciona a los especialistas en marketing inteligencia de acción en tiempo real sobre estrategias en línea e iniciativas de marketing.
* Adobe Target ofrece a los especialistas en marketing la capacidad de hacer que el contenido en línea sea más relevante para sus clientes, lo que resulta en buenas conversiones.
* Adobe Dynamic Media Classic automatiza la administración de medios, optimiza la publicación web y mejora las experiencias web, todo en un entorno alojado.
* Adobe Dynamic Tag Management proporciona a los especialistas en marketing herramientas intuitivas para administrar rápida y fácilmente un número ilimitado de Adobes y etiquetas de terceros.
* El Search&amp;Promote de Adobe permite a los especialistas en marketing controlar y optimizar los resultados de búsqueda en sus sitios.
* Adobe Campaign permite administrar el contenido de la entrega por correo electrónico directamente en Adobe Experience Manager.

Además, puede [integrar AEM con el Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) y con [servicios de terceros](/help/sites-administering/third-party-services.md).

## Integración con Adobe Analytics {#integrating-with-adobe-analytics}

[Adobe ](https://www.omniture.com/en/products/analytics/sitecatalyst) Analytics es la solución líder del sector que proporciona a los especialistas en marketing digital un lugar para medir, analizar y optimizar los datos integrados de todas las iniciativas en línea en varios canales de marketing. Proporciona a los especialistas en marketing inteligencia de análisis web en tiempo real y procesable sobre estrategias digitales e iniciativas de marketing. Adobe Analytics ayuda a los especialistas en marketing a identificar rápidamente las rutas más rentables a través de un sitio web, segmentar el tráfico para detectar visitantes web de alto valor, determinar dónde los visitantes se desplazan fuera del sitio e identificar métricas de éxito críticas para las campañas de marketing en línea.

Puede utilizar Adobe Analytics para analizar los datos de sus sitios.

La integración con Adobe Analytics le permite hacer lo siguiente:

* Habilite el seguimiento de usuarios de Analytics.
* Asigne los modos de ejecución (por ejemplo, autor o publicación) a diferentes grupos de informes.
* Envíe variables de Client Context como variables de conversión o propiedades de tráfico.
* Utilice asignaciones de variables predefinidas.
* Configure secciones completas del sitio a la vez.
* Rastree eventos definidos personalizados.

Para obtener información sobre la integración de AEM con Analytics, consulte [Integración con Adobe Analytics](/help/sites-administering/adobeanalytics.md).

También puede utilizar el [Asistente para la inclusión](/help/sites-administering/opt-in.md) para realizar fácilmente la integración.

## Integración con Adobe Target {#integrating-with-adobe-target}

[Los especialistas en marketing utilizan la ](https://www.omniture.com/en/products/conversion/test-and-target) segmentación de Adobe para diseñar y ejecutar pruebas en línea, crear segmentos de audiencia sobre la marcha (basados en el comportamiento) y automatizar la segmentación del contenido y las experiencias en línea.

Los consumidores en línea de hoy en día tienen necesidades en constante evolución y esperan contenido relevante, incluso personalizado, de la amplia variedad de sitios y fuentes de contenido entre las que pueden elegir. Para atraer a una audiencia en línea, es fundamental que los especialistas en marketing en línea identifiquen rápidamente qué ofertas y contenido son relevantes y convincentes para sus audiencias. Con este conocimiento, los especialistas en marketing necesitan la capacidad de evolucionar continuamente sus sitios y dirigir el contenido adecuado a diferentes audiencias.

[Integración con Adobe ](/help/sites-administering/target.md) Target explica cómo integrar su sitio con Target.

También puede utilizar el [Asistente para la inclusión](/help/sites-administering/opt-in.md) para realizar fácilmente la integración.

## Inclusión en Analytics y Target {#opting-in-to-analytics-and-target}

AEM proporciona un procedimiento de inclusión simple para integrarlo con Adobe Analytics y Adobe Target. Cuando inicia sesión como administrador y visita la consola Proyectos , aparece un asistente de inclusión.

![chlimage_1-107](assets/chlimage_1-107a.png)

Participe en la integración con Analytics y/o Target para permitir el uso de sus capacidades de seguimiento y análisis de página, así como de las capacidades de personalización. Cuando decida unirse, debe proporcionar la información de su cuenta de usuario y especificar las páginas de las que se realiza un seguimiento.

Para obtener más información, consulte [Inclusión en Adobe Analytics y Adobe Target.](/help/sites-administering/opt-in.md)

## Integración con Adobe Dynamic Media Classic {#integrating-with-scene}

Adobe Dynamic Media Classic es una solución alojada para la publicación, administración, mejora y entrega de recursos de marketing dinámico y de comercialización visual enriquecida en la web, dispositivos móviles, correo electrónico, medios sociales, pantallas e impresiones conectadas a Internet.

En Adobe Experience Manager, puede publicar recursos digitales directamente de Adobe Experience Manager a Dynamic Media Classic y recursos digitales de Dynamic Media Classic a Adobe Experience Manager.

Además, puede ver los recursos de Adobe Experience Manager publicados en Dynamic Media Classic en varios visores, como Zoom básico y Vídeo.

Para obtener más información sobre cómo se integra Adobe Experience Manager con Dynamic Media Classic, consulte la documentación [Integración con Dynamic Media Classic](/help/sites-administering/scene7.md) .

## Integración con Adobe Dynamic Tag Management {#integrating-with-adobe-dynamic-tag-management}

[Adobe Dynamic Tag ](https://www.adobe.com/solutions/digital-marketing/dynamic-tag-management.html) Management proporciona a los especialistas en marketing herramientas intuitivas para administrar rápida y fácilmente un número ilimitado de Adobes y etiquetas de terceros. Tendrá más control y flexibilidad para optimizar prácticamente cualquier cosa en línea, al tiempo que reducirá la dependencia de los recursos de TI.

[Integre Adobe Dynamic Tag ](/help/sites-administering/dtm.md) Management con AEM para que pueda usar las propiedades web de Dynamic Tag Management para rastrear sitios AEM.

## Integración con Adobe Audience Manager {#integrating-with-adobe-audience-manager}

La integración del Audience Manager se ha eliminado en la AEM 6.3.

## Integración con Search&amp;Promote {#integrating-with-search-promote}

El Search&amp;Promote de Adobe permite a los especialistas en marketing optimizar la forma en que los visitantes examinan, buscan, comparan y seleccionan los productos y el contenido relevantes en sitios web y móviles. Las empresas pueden promocionar fácilmente elementos prioritarios según los objetivos empresariales y la intención del visitante, así como automatizar la actividad de comercialización y promociones mediante déclencheur o métricas basados en KPI.

El Search&amp;Promote de Adobe es una aplicación alojada de búsqueda fiable y escalable, capaz de escalar a millones de páginas o productos, para negocios en línea muy visitados que van desde minoristas hasta sitios de noticias. Ofrece niveles sin precedentes de control de especialistas en marketing y relevancia basada en métricas.

Para obtener información sobre la integración de AEM y Search&amp;Promote, consulte [Integración con el Search&amp;Promote de Adobe](/help/sites-administering/search-and-promote.md).

## Integración con Adobe Campaign {#integrating-with-adobe-campaign}

[Adobe ](https://www.adobe.com/solutions/campaign-management.html) Campaign permite administrar el contenido de la entrega por correo electrónico directamente en Adobe Experience Manager.

Para obtener información sobre cómo AEM se integra con Adobe Campaign, consulte [Integración con Adobe Campaign](/help/sites-administering/campaignstandard.md).

## Integración con Livefyre {#integrating-with-livefyre}

Obtenga información sobre AEM y Livefyre:

* [Introducción a Livefyre](https://answers.livefyre.com/developers/getting-started)

* [Livefyre y AEM](https://answers.livefyre.com/product/livefyre-for-adobe-experience-manager-aem/livefyre-for-adobe-experience-manager/) 
