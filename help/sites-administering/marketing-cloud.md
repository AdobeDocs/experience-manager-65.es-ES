---
title: Integración con el Adobe Marketing Cloud
description: Aprenda a integrar Adobe Experience Manager con Adobe Marketing Cloud.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
translation-type: tm+mt
source-git-commit: 4333cfde433d00ddc4cb013b31fe52956791da46
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 1%

---


# Integración con Adobe Marketing Cloud{#integrating-with-the-adobe-marketing-cloud}

El [Adobe Marketing Cloud](https://www.adobe.com/solutions/digital-marketing.html) incluye potentes productos de optimización de sitios web y análisis de Web que proporcionan datos y perspectivas procesables en tiempo real para impulsar iniciativas en línea exitosas. Oferta una plataforma integrada y abierta para la optimización comercial en línea. La nube consiste en aplicaciones integradas para recopilar y liberar el poder de la perspectiva del cliente para optimizar los esfuerzos de adquisición, conversión y retención del cliente, así como la creación y distribución de contenido.

Con Adobe Experience Manager (AEM), puede integrarse sin problemas con los siguientes productos de Adobe Marketing Cloud:

* Adobe Analytics proporciona a los especialistas en marketing inteligencia procesable y en tiempo real sobre estrategias en línea e iniciativas de marketing.
* Adobe Target ofrece a los especialistas en marketing la posibilidad de hacer que su contenido en línea sea más relevante para sus clientes: generando buena conversión.
* Adobe Dynamic Media Classic automatiza la administración de medios, optimiza la publicación web y mejora las experiencias web, todo ello en un entorno alojado.
* La administración dinámica de etiquetas de Adobe proporciona a los especialistas en marketing herramientas intuitivas para administrar rápida y fácilmente un número ilimitado de etiquetas de Adobe y de terceros.
* El Search&amp;Promote de Adobe permite a los especialistas en mercadotecnia controlar y optimizar los resultados de búsqueda en sus sitios.
* Adobe Campaign le permite administrar el contenido del envío de correo electrónico directamente en Adobe Experience Manager.

Además, puede [integrar AEM con Creative Cloud](/help/assets/aem-cc-folder-sharing-best-practices.md) y con [servicios de terceros](/help/sites-administering/third-party-services.md).

## Integración con Adobe Analytics {#integrating-with-adobe-analytics}

[Adobe ](https://www.omniture.com/en/products/analytics/sitecatalyst) Analytics es la solución líder del sector que proporciona a los especialistas en mercadotecnia digital un lugar para medir, analizar y optimizar los datos integrados de todas las iniciativas en línea en varios canales de mercadotecnia. Proporciona a los especialistas en marketing inteligencia de análisis web procesable y en tiempo real sobre estrategias digitales e iniciativas de marketing. Adobe Analytics ayuda a los especialistas en mercadotecnia a identificar rápidamente las rutas más rentables a través de un sitio web, segmentar el tráfico para detectar visitantes Web de alto valor, determinar dónde los visitantes se desplazan fuera del sitio e identificar las métricas de éxito críticas para las campañas de mercadotecnia en línea.

Puede utilizar Adobe Analytics para analizar los datos de sus sitios.

La integración con Adobe Analytics le permite hacer lo siguiente:

* Habilite el seguimiento de usuarios de Analytics.
* Asigne los modos de ejecución (por ejemplo, autor, publicación) a diferentes grupos de informes.
* Envíe variables de ClientContext como variables de conversión o propiedades de tráfico.
* Utilice asignaciones de variables predefinidas.
* Configure las secciones completas del sitio a la vez.
* Rastree eventos personalizados.

Para obtener información sobre la integración de AEM con Analytics, consulte [Integración con Adobe Analytics](/help/sites-administering/adobeanalytics.md).

También puede utilizar el [Asistente para la selección](/help/sites-administering/opt-in.md) para realizar fácilmente la integración.

## Integración con Adobe Target {#integrating-with-adobe-target}

[Los especialistas en marketing utilizan ](https://www.omniture.com/en/products/conversion/test-and-target) objetivos de Adobe para diseñar y ejecutar pruebas en línea, crear segmentos de audiencia sobre la marcha (basados en el comportamiento) y automatizar la segmentación del contenido y las experiencias en línea.

Los consumidores en línea hoy en día tienen necesidades en constante evolución y esperan contenido relevante, incluso personalizado, de la amplia variedad de sitios y fuentes de contenido que pueden elegir. Para participar en una audiencia en línea, es fundamental que los especialistas en mercadotecnia en línea identifiquen rápidamente qué ofertas y contenido son relevantes y convincentes para sus audiencias. Con este conocimiento, los especialistas en mercadotecnia necesitan la capacidad de evolucionar continuamente sus sitios y de destinatario del contenido apropiado a diferentes audiencias.

[La integración con Adobe ](/help/sites-administering/target.md) Target explica cómo integrar el sitio con Destinatario.

También puede utilizar el [Asistente para la selección](/help/sites-administering/opt-in.md) para realizar fácilmente la integración.

## adhesión a Analytics y Destinatario {#opting-in-to-analytics-and-target}

AEM ofrece un procedimiento de inclusión simple para integrarlo con Adobe Analytics y Adobe Target. Al iniciar sesión como administrador y visitar la consola Proyectos, se le mostrará un asistente para la selección.

![chlimage_1-107](assets/chlimage_1-107a.png)

Opte por la integración con Analytics y/o Destinatario para habilitar el uso de sus funciones de seguimiento de páginas y análisis, así como las funciones de personalización. Cuando adhesión, debe proporcionar la información de su cuenta de usuario y especificar las páginas que se rastrean.

Para obtener más información, consulte [Opción en Adobe Analytics y Adobe Target.](/help/sites-administering/opt-in.md)

## Integración con Adobe Dynamic Media Classic {#integrating-with-scene}

Adobe Dynamic Media Classic es una solución alojada para publicar, administrar, mejorar y distribuir recursos de marketing dinámicos y una amplia comercialización visual en la Web, dispositivos móviles, correo electrónico, medios sociales, pantallas conectadas a Internet e impresión.

En Adobe Experience Manager, puede publicar recursos digitales directamente desde Adobe Experience Manager a Dynamic Media Classic y puede publicarlos desde Dynamic Media Classic a Adobe Experience Manager.

Además, puede realizar la vista de recursos de Adobe Experience Manager publicados en Dynamic Media Classic en varios visores, como Zoom básico y Vídeo.

Para obtener más información sobre cómo se integra Adobe Experience Manager con Dynamic Media Classic, consulte la documentación de [Integración con Dynamic Media Classic](/help/sites-administering/scene7.md).

## Integración con la administración dinámica de etiquetas de Adobe {#integrating-with-adobe-dynamic-tag-management}

[La ](https://www.adobe.com/solutions/digital-marketing/dynamic-tag-management.html) administración dinámica de etiquetas de Adobe proporciona a los especialistas en marketing herramientas intuitivas para administrar rápida y fácilmente un número ilimitado de etiquetas de Adobe y de terceros. Tendrá más control y flexibilidad para optimizar prácticamente cualquier cosa en línea, todo mientras reduce la dependencia de los recursos de TI.

[Integre la ](/help/sites-administering/dtm.md) administración dinámica de etiquetas de Adobe con AEM para que pueda utilizar las propiedades web de la administración dinámica de etiquetas para rastrear AEM sitios.

## Integración con Adobe Audience Manager {#integrating-with-adobe-audience-manager}

La integración de Audience Manager se ha eliminado en la AEM 6.3.

## Integración con Search&amp;Promote {#integrating-with-search-promote}

El Search&amp;Promote de Adobe permite a los especialistas en marketing optimizar la forma en que los visitantes exploran, buscan, comparan y seleccionan los productos y el contenido relevantes en los sitios web y móviles. Las empresas pueden promocionar fácilmente los elementos prioritarios en función de los objetivos empresariales y la intención de visitante, así como automatizar la actividad de promociones y mercadotecnia mediante déclencheur o métricas basados en KPI.

Adobe Search&amp;Promote es una aplicación de búsqueda alojada confiable y escalable, capaz de escalar a millones de páginas o productos, para negocios en línea muy visitados que van desde sitios minoristas hasta sitios de noticias. Oferta niveles sin precedentes de control de los especialistas en mercadotecnia y relevancia basada en métricas.

Para obtener información sobre la integración de AEM y Search&amp;Promote, consulte [Integración con Adobe Search&amp;Promote](/help/sites-administering/search-and-promote.md).

## Integración con Adobe Campaign {#integrating-with-adobe-campaign}

[Adobe ](https://www.adobe.com/solutions/campaign-management.html) Campaign permite administrar el contenido del envío de correo electrónico directamente en Adobe Experience Manager.

Para obtener información sobre cómo se integra AEM con Adobe Campaign, consulte [Integración con Adobe Campaign](/help/sites-administering/campaignstandard.md).

## Integración con Livefyre {#integrating-with-livefyre}

Obtenga información sobre AEM y Livefyre:

* [Introducción a Livefyre](https://answers.livefyre.com/developers/getting-started)

* [Livefyre y AEM](https://answers.livefyre.com/product/livefyre-for-adobe-experience-manager-aem/livefyre-for-adobe-experience-manager/) 

