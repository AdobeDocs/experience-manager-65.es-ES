---
title: Perspectiva de contenido
seo-title: Content Insight
description: La perspectiva de contenido proporciona información sobre el rendimiento de la página mediante análisis web y recomendaciones de SEO
seo-description: Content Insight provides information about page performance using web analytics and SEO recommendation
uuid: 32f5b37c-2a82-462a-9f0a-c19bed46e198
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 60f980fd-049e-43c1-8b5d-60a8279b357a
exl-id: 187f3cde-a0db-4c02-9e8b-08272987a67d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Perspectiva de contenido{#content-insight}

La perspectiva de contenido proporciona información sobre el rendimiento de la página mediante análisis web y recomendaciones de SEO. Utilice Perspectiva de contenido para tomar decisiones sobre cómo modificar páginas o conocer cómo los cambios anteriores han cambiado el rendimiento. Para cada página que cree, puede abrir Perspectiva de contenido para analizar la página.

![chlimage_1-311](assets/chlimage_1-311.png)

El diseño de la página Perspectiva de contenido cambia para adaptarse a las dimensiones de pantalla y a la orientación del dispositivo que está utilizando.

## Datos del informe

La página Perspectiva de contenido incluye informes que utilizan datos de Adobe SiteCatalyst, Adobe Target, Adobe Social y BrightEdge:

* SiteCatalyst: Hay disponibles informes para las siguientes métricas:

   * Page views
   * Tiempo promedio empleado en la página
   * Orígenes

* Target: informa sobre la actividad de campaña para la que la página incluye ofertas.
* BrightEdge: informa sobre las funciones de la página que mejoran la visibilidad de la página para los motores de búsqueda y recomienda las funciones que deben implementarse.

Consulte [Abrir Analytics y Recommendations para una página](/help/sites-authoring/ci-analyze.md#opening-analytics-and-recommendations-for-a-page).

## Período de informe

Los informes muestran datos correspondientes a un período de tiempo que usted controla. Al ajustar el período de informe, los informes se actualizan automáticamente con los datos de ese período. Las indicaciones visuales indican el momento en el que cambiaron las versiones de la página, de modo que puede comparar el rendimiento de cada versión.

También puede especificar la granularidad de los datos del informe; por ejemplo, puede ver datos diarios, semanales, mensuales o anuales.

Consulte [Modificación del período de informe](/help/sites-authoring/ci-analyze.md#changing-the-reporting-period).

>[!NOTE]
>
>AEM Los informes de Perspectivas de contenido requieren que el administrador de haya integrado la aplicación con SiteCatalyst, Target y BrightEdge. Consulte [Integración con SightCatalyst](/help/sites-administering/adobeanalytics.md), [Integración con Adobe Target](/help/sites-administering/target.md), y [Integración con BrightEdge](/help/sites-administering/brightedge.md).

## El informe Vistas {#the-views-report}

El informe Vistas incluye las siguientes funciones para evaluar el tráfico de la página:

* Número total de vistas de una página durante el período de informe.
* Gráfico del número de vistas en el período de informe:

   * Vistas totales.
   * Visitantes únicos.

![chlimage_1-312](assets/chlimage_1-312.png)

## El informe Promedio de páginas comprometidas {#the-page-average-engaged-report}

El informe Participación media de la página incluye las siguientes funciones para evaluar la eficacia de la página:

* Promedio de tiempo que la página permanece abierta durante todo el período de informe.
* Gráfico de la longitud promedio de una vista de página durante el período de informe.

![chlimage_1-313](assets/chlimage_1-313.png)

## El informe de fuentes {#the-sources-report}

El informe Fuentes indica cómo navegaron los usuarios hasta la página, por ejemplo, desde los resultados de los motores de búsqueda o utilizando la URL conocida.

![chlimage_1-314](assets/chlimage_1-314.png)

## El informe de devoluciones {#the-bounces-report}

El informe Devoluciones incluye un gráfico que muestra el número de devoluciones que se han producido para una página durante el periodo de informe seleccionado.

![chlimage_1-315](assets/chlimage_1-315.png)

## El informe Actividad de la campaña {#the-campaign-activity-report}

Aparece un informe con el nombre de todas las campañas para las que está activa la página *Nombre de campaña* Actividad. El informe muestra las impresiones y conversiones de página de cada segmento para el que se proporciona una oferta.

![chlimage_1-316](assets/chlimage_1-316.png)

## El informe Recommendations de SEO {#the-seo-recommendations-report}

El informe SEO Recommendations contiene los resultados del análisis de BrightEdge para la página. El informe es una lista de comprobación de las funciones de la página que indica qué funciones incluye y no incluye la página para maximizar la capacidad de búsqueda mediante motores de búsqueda.

El informe permite crear tareas para mejorar la búsqueda de páginas. Recommendations indica que se han creado tareas para implementar la recomendación. Consulte [Asignación de tareas para SEO Recommendations](/help/sites-authoring/ci-analyze.md#assigning-tasks-for-seo-recommendations).

![chlimage_1-317](assets/chlimage_1-317.png)
