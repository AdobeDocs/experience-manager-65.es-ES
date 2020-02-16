---
title: Integración con Adobe Marketing Cloud
seo-title: Integración con Adobe Marketing Cloud
description: Obtenga información sobre cómo integrar AEM con Adobe Marketing Cloud.
seo-description: Obtenga información sobre cómo integrar AEM con Adobe Marketing Cloud.
uuid: 36d71dd3-7fb0-4237-99d3-4fbb2e162e7b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: ba496f6a-c9aa-49b5-8207-8633748d2c17
translation-type: tm+mt
source-git-commit: 471b57a52efc849eb57201e6397221fa4f88c746

---


# Integración con Adobe Marketing Cloud{#integrating-with-the-adobe-marketing-cloud}

Adobe [Marketing Cloud](https://www.adobe.com/solutions/digital-marketing.html)incluye potentes productos de optimización de sitios web y análisis web que ofrecen datos y perspectivas procesables en tiempo real para impulsar iniciativas en línea exitosas. Ofrece una plataforma integrada y abierta para la optimización comercial en línea. La nube consiste en aplicaciones integradas para recopilar y liberar el poder de la perspectiva del cliente para optimizar los esfuerzos de adquisición, conversión y retención del cliente, así como la creación y distribución de contenido.

Con Adobe Experience Manager (AEM), puede integrarse sin problemas con los siguientes productos de Adobe Marketing Cloud:

* Adobe Analytics proporciona a los especialistas en marketing inteligencia procesable en tiempo real sobre estrategias en línea e iniciativas de marketing.
* Adobe Target ofrece a los especialistas en marketing la posibilidad de hacer que su contenido en línea sea más relevante para sus clientes: lo que genera una mayor conversión.
* Adobe Scene7 automatiza la administración de medios, optimiza la publicación web y mejora las experiencias web, todo ello en un entorno alojado.
* La administración dinámica de etiquetas de Adobe proporciona a los especialistas en marketing herramientas intuitivas para administrar rápida y fácilmente un número ilimitado de etiquetas de Adobe y de terceros.
* Adobe Search&amp;Promote ofrece a los especialistas en mercadotecnia la capacidad de controlar y optimizar los resultados de búsqueda en sus sitios.
* Adobe Campaign permite administrar el contenido de la entrega por correo electrónico directamente en Adobe Experience Manager.

Además, puede [integrar AEM con Creative Cloud](/help/assets/aem-cc-folder-sharing-best-practices.md) y con servicios [de](/help/sites-administering/third-party-services.md)terceros.

## Integración con Adobe Analytics {#integrating-with-adobe-analytics}

[Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst) es la solución líder del sector que proporciona a los especialistas en marketing digital un lugar para medir, analizar y optimizar los datos integrados de todas las iniciativas en línea en varios canales de marketing. Proporciona a los especialistas en marketing inteligencia de análisis web procesable y en tiempo real sobre estrategias digitales e iniciativas de marketing. Adobe Analytics ayuda a los especialistas en mercadotecnia a identificar rápidamente las rutas más rentables a través de un sitio web, segmentar el tráfico para identificar a los visitantes web de alto valor, determinar dónde se desplazan los visitantes fuera del sitio e identificar las métricas de éxito críticas para las campañas de mercadotecnia en línea.

Puede utilizar Adobe Analytics para analizar los datos de sus sitios.

La integración con Adobe Analytics le permite hacer lo siguiente:

* Habilite el seguimiento de usuarios de Analytics.
* Asigne los modos de ejecución (por ejemplo, autor, publicación) a diferentes grupos de informes.
* Envíe variables de ClientContext como variables de conversión o propiedades de tráfico.
* Utilice asignaciones de variables predefinidas.
* Configure las secciones completas del sitio a la vez.
* Rastree eventos personalizados.

Para obtener información sobre la integración de AEM con Analytics, consulte [Integración con Adobe Analytics](/help/sites-administering/adobeanalytics.md).

También puede utilizar el asistente para la [inclusión](/help/sites-administering/opt-in.md) para realizar fácilmente la integración.

## Integración con Adobe Target {#integrating-with-adobe-target}

[Los especialistas en marketing utilizan Adobe Target](https://www.omniture.com/en/products/conversion/test-and-target) para diseñar y ejecutar pruebas en línea, crear segmentos de audiencia sobre la marcha (según el comportamiento) y automatizar la segmentación del contenido y las experiencias en línea.

Los consumidores en línea hoy en día tienen necesidades en constante evolución y esperan contenido relevante, incluso personalizado, de la amplia variedad de sitios y fuentes de contenido que pueden elegir. Para atraer a una audiencia en línea, es fundamental que los especialistas en mercadotecnia en línea identifiquen rápidamente qué ofertas y contenido son relevantes y convincentes para sus audiencias. Con este conocimiento, los especialistas en mercadotecnia necesitan la capacidad de evolucionar continuamente sus sitios y dirigir el contenido apropiado a diferentes audiencias.

[La integración con Adobe Target](/help/sites-administering/target.md) explica cómo integrar el sitio con Target.

También puede utilizar el asistente para la [inclusión](/help/sites-administering/opt-in.md) para realizar fácilmente la integración.

## Opción de inclusión en Analytics y Target {#opting-in-to-analytics-and-target}

AEM ofrece un procedimiento de selección sencillo para integrarlo con Adobe Analytics y Adobe Target. Al iniciar sesión como administrador y visitar la consola Proyectos, se le mostrará un asistente para la selección.

![chlimage_1-107](assets/chlimage_1-107a.png)

Seleccione la integración con Analytics y/o Target para habilitar el uso de sus capacidades de seguimiento y análisis de páginas y de personalización. Al optar por la opción, debe proporcionar la información de su cuenta de usuario y especificar las páginas que se rastrean.

Para obtener más información, consulte [Opción en Adobe Analytics y Adobe Target.](/help/sites-administering/opt-in.md)

## Integración con Scene7 {#integrating-with-scene}

[Adobe Scene7](https://www.adobe.com/products/scene7.html) es una solución alojada para publicar, gestionar, mejorar y distribuir recursos de marketing dinámicos y una amplia comercialización visual en la Web, dispositivos móviles, correo electrónico, medios sociales, pantallas conectadas a Internet e impresión.

En AEM, puede publicar recursos digitales directamente desde AEM a Scene7 y puede publicarlos en AEM.

Además, puede ver los recursos de AEM publicados en Scene7 en varios visores:

* Zoom básico
* Zoom flotante DHTML
* Zoom flotante de Flash
* Vídeo
* Flash Plantilla
* Plantilla de imagen

Para obtener más información sobre cómo se integra AEM con Scene7, consulte la documentación [de](/help/sites-administering/scene7.md)Integración con Scene7.

## Integración con la administración dinámica de etiquetas de Adobe {#integrating-with-adobe-dynamic-tag-management}

[La administración](https://www.adobe.com/solutions/digital-marketing/dynamic-tag-management.html) dinámica de etiquetas de Adobe proporciona a los especialistas en marketing herramientas intuitivas para administrar rápida y fácilmente un número ilimitado de etiquetas de Adobe y de terceros. Tendrá más control y flexibilidad para optimizar prácticamente cualquier cosa en línea, todo mientras reduce la dependencia de los recursos de TI.

[Integre la administración](/help/sites-administering/dtm.md) dinámica de etiquetas de Adobe con AEM para que pueda utilizar las propiedades web de la administración dinámica de etiquetas con el fin de realizar un seguimiento de los sitios de AEM.

## Integración con Adobe Audience Manager {#integrating-with-adobe-audience-manager}

La integración de Audience Manager se ha eliminado en AEM 6.3.

## Integración con Search&amp;Promote {#integrating-with-search-promote}

[Adobe Search&amp;Promote](https://www.omniture.com/en/products/conversion/search-and-promote) permite a los especialistas en mercadotecnia optimizar la forma en que los visitantes exploran, buscan, comparan y seleccionan los productos y el contenido relevantes en los sitios web y móviles. Las empresas pueden promocionar fácilmente elementos prioritarios en función de los objetivos comerciales y la intención del visitante, así como automatizar la actividad de comercialización y promociones a través de activadores o métricas basados en KPI.

Adobe Search&amp;Promote es una aplicación de búsqueda alojada fiable y escalable, capaz de escalar a millones de páginas o productos, para negocios en línea muy visitados, desde sitios minoristas hasta sitios de noticias. Ofrece niveles sin precedentes de control de los especialistas en mercadotecnia y relevancia basada en métricas.

Para obtener información sobre la integración de AEM y Search&amp;Promote, consulte [Integración con Adobe Search&amp;Promote](/help/sites-administering/search-and-promote.md).

## Integración con Adobe Campaign {#integrating-with-adobe-campaign}

[Adobe Campaign](https://www.adobe.com/solutions/campaign-management.html) permite administrar el contenido de la entrega por correo electrónico directamente en Adobe Experience Manager.

Para obtener información sobre cómo AEM se integra con Adobe Campaign, consulte [Integración con Adobe Campaign](/help/sites-administering/campaignstandard.md).

## Integración con Livefyre {#integrating-with-livefyre}

Obtenga información sobre AEM y Livefyre:

* [Introducción a Livefyre](https://answers.livefyre.com/developers/getting-started)

* [Livefyre y AEM](https://answers.livefyre.com/product/livefyre-for-adobe-experience-manager-aem/livefyre-for-adobe-experience-manager/) 

