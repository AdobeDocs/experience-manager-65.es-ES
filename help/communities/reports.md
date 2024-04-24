---
title: Consola Informes
description: Aprenda a utilizar varios informes a los que puede acceder de varias formas desde el entorno de Adobe Experience Manager Author.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 2aff2ffe-ba6f-4cc9-a126-40fc2a1161e2
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 6%

---

# Consola Informes {#reports-console}

## Información general {#overview}

Para AEM Communities, hay varios informes a los que se puede acceder de varias formas desde el entorno de creación.

En general, los distintos informes son:

* [Informe de vistas](#views-report)

  Proporciona un gráfico de vistas del contenido realizadas por los miembros de la comunidad y los visitantes del sitio para cualquier sitio de la comunidad.

* [Informe de anuncios](#posts-report)

  Proporciona un gráfico de varios tipos de publicaciones realizadas por los miembros de la comunidad en cualquier sitio de la comunidad.

Los informes tabulares se pueden exportar en formato .csv para su posterior procesamiento.

## Consolas de informes {#reporting-consoles}

### Informes de sitios de la comunidad {#reports-for-community-sites}

* Desde la navegación global: **[!UICONTROL Navegación]** > **[!UICONTROL Communities]** >  **[!UICONTROL Informes]**

* Elija entre:

   * **[!UICONTROL Informe de asignaciones]**

      * Genere un informe para el sitio, el usuario o el grupo y la asignación de la comunidad seleccionados.

   * **[!UICONTROL Informe de anuncios]**

      * Genere un informe para el sitio de la comunidad, el tipo de contenido y el período de tiempo seleccionados.

   * **[!UICONTROL Informe de vistas]**

      * genere un informe para el sitio de la comunidad, el tipo de contenido y el período de tiempo seleccionados.

![informes](assets/reports1.png)

## Informe de vistas {#views-report}

La consola Vistas permite que las funciones de la comunidad generen informes en las vistas de página durante un período de tiempo determinado.

![view-report](assets/view-report.png)

Seleccione los criterios del informe:

* **[!UICONTROL Sitio]**

  Seleccione un sitio de la comunidad.

* **[!UICONTROL Tipo de contenido]**

  Puede elegir Todo el contenido o seleccionar una de las funciones que están presentes en el sitio.

* **[!UICONTROL Lapso de tiempo]**

  Seleccione una de las siguientes opciones:

   * Últimos 7 días
   * Últimos 30 días
   * Últimos 90 días
   * Año pasado

Seleccionar **[!UICONTROL Generar]** para crear el informe.

![generate-views](assets/generate-views.png)

## Informe de anuncios {#posts-report}

La consola Publicaciones permite generar informes sobre el número de publicaciones en las funciones de la comunidad durante un período de tiempo determinado.

![post-report](assets/posts-report.png)

Seleccione los criterios del informe:

* **[!UICONTROL Sitio]**

  Seleccione un sitio de la comunidad.

* **[!UICONTROL Tipo de contenido]**

  Puede elegir Todo el contenido o seleccionar una de las funciones que están presentes en el sitio.

* **[!UICONTROL Lapso de tiempo]**

  Seleccione una de las siguientes opciones:

   * Últimos 7 días
   * Últimos 30 días
   * Últimos 90 días
   * Año pasado

Seleccionar **[!UICONTROL Generar]** para crear el informe.

![generate-report](assets/generate-posts-report.png)

## Resolución de problemas {#troubleshooting}

### No hay sitios de la comunidad enumerados {#no-community-sites-listed}

Si no aparece ningún sitio de la comunidad, asegúrese de que Adobe Analytics se haya habilitado para un sitio. Si elige informes sobre las asignaciones, asegúrese de que la función de asignaciones se encuentra en la estructura del sitio de la comunidad.

### AEM Los informes no se muestran en instancia de autor {#reports-do-not-show-in-aem-author-instance}

AEM Si los informes no se muestran en la instancia de autor de la, compruebe las personalizaciones, como la asignación de URL en la instancia de publicación. AEM AEM Si la asignación de URL solo se realiza en la instancia de publicación de la comunidad del sitio de comunidades, asegúrese de que se haya configurado la misma en la instancia de autor de la en **Fábrica de componentes sociales de informe de tendencias del sitio** configuración.

![AEM Asignación de URL en el autor del](assets/sitetrend.png)
