---
title: Administración de sitios web
seo-title: Website Administration
description: AEM Obtenga información sobre cómo administrar sitios web multilingües en el sitio web de.
seo-description: Learn how to manage multilingual websites in AEM.
uuid: a32d458b-a5ad-46ef-a68c-4717c63b4bdd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: fabaa3e8-1657-4ed4-abb2-990117bec39c
exl-id: 8f11f5de-f5af-4ce7-a448-2b4299de2930
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 41%

---

# Administración de sitios web{#website-administration}

Las siguientes herramientas de administración están disponibles para administrar sitios web y páginas:

* El Administrador de varios sitios (MSM) le permite usar el mismo contenido del sitio en varias ubicaciones, a la vez que permite variaciones:

   * [Reutilización del contenido: administrador de varios sitios y Live Copy](/help/sites-administering/msm.md)

* La traducción le permite automatizar la traducción del contenido de la página, los activos y el contenido generado por el usuario para crear y mantener sitios web multilingües:

   * [Traducción de contenido para sitios multilingües](/help/sites-administering/translation.md)

* Estas dos funciones se pueden combinar para adaptarse a los sitios web que son [Multinacional y multilingüe](#multinational-and-multilingual-sites).

## Sitios multinacionales y multilingües {#multinational-and-multilingual-sites}

Puede crear contenido de forma eficaz para sitios multinacionales y multilingües mediante el uso combinado de Administrador de varios sitios y el flujo de trabajo de traducción. Cree un sitio principal en un idioma para un país específico y luego utilice ese contenido como base para los demás sitios, traduciendo lo que sea necesario:

* [Traducir](/help/sites-administering/translation.md) el sitio principal a diferentes idiomas.

* Use [Administrador de varios sitios](/help/sites-administering/msm.md) para lo siguiente:

   * Reutilice el contenido del sitio principal y las traducciones para crear sitios destinados a otros países y culturas.
   * Asegúrese de limitar el uso del Administrador de varios sitios al contenido en un idioma, por ejemplo, inglés principal -> ramas en inglés en sitios de países, francés principal -> ramas en francés en sitios de países.
   * Cuando sea necesario, desasocie elementos de las Live Copies para añadir detalles de localización.

El diagrama siguiente ilustra cómo se cruzan los conceptos principales (pero no muestra todos los niveles/elementos implicados):

![Diagrama que muestra los conceptos principales de MSM y traducción](assets/chlimage_1-71a.png)

>[!NOTE]
>
>En este escenario, y en otros comparables, MSM no gestiona las diferentes versiones lingüísticas como tal.
>
>* [MSM](/help/sites-administering/msm.md) administra la implementación del contenido traducido de un modelo (por ejemplo, un maestro global) a live copies (por ejemplo, los sitios locales), dentro de los límites de un idioma.
>* Las funciones de integración de [traducciones](/help/sites-administering/translation.md) de AEM, junto con los servicios de administración de traducciones de terceros, gestionan los diferentes idiomas y traducen el contenido a estos.
>
>Para casos de uso más avanzados, también se pueden usar MSM entre idiomas principales.

>[!NOTE]
>
>Para todos los casos de uso, se recomienda leer las siguientes prácticas recomendadas:
>
>* [Prácticas recomendadas para MSM](/help/sites-administering/msm-best-practices.md); especialmente:
>
>   * [Crear sitio](/help/sites-administering/msm-best-practices.md#create-site)
>   * [MSM y sitios web multilingües](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites)
>
>* [Prácticas recomendadas para la traducción](/help/sites-administering/tc-bp.md)
