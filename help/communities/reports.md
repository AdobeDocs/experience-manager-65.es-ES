---
title: Consola Informes
seo-title: Reports Console
description: Obtenga información sobre cómo acceder a los informes
seo-description: Learn how to access reports
uuid: 7bb15a15-077b-4bfb-aaf4-50fddc67f237
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: fde053ff-b671-456b-869c-81f16ea1f1be
docset: aem65
role: Admin
exl-id: 2aff2ffe-ba6f-4cc9-a126-40fc2a1161e2
source-git-commit: 942db8fe3dad16be53dc6abe0e519d97a659e480
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 9%

---

# Consola Informes {#reports-console}

## Información general {#overview}

Para AEM Communities, existen varios informes a los que se puede acceder de varias formas desde el entorno de creación.

En general, los diversos informes son:

* [Informe de vistas](#views-report)

   Proporciona un gráfico de vistas de contenido por miembros de la comunidad y visitantes del sitio para cualquier sitio de la comunidad.

* [Informe de anuncios](#posts-report)

   Proporciona un gráfico de varios tipos de anuncios de los miembros de la comunidad en cualquier sitio de la comunidad.

Los informes tabulares se pueden exportar en formato .csv para su procesamiento posterior.

## Consolas de informes {#reporting-consoles}

### Informes para sitios de la comunidad {#reports-for-community-sites}

* Desde la navegación global: **[!UICONTROL Navegación]** > **[!UICONTROL Comunidades]** >  **[!UICONTROL Informes]**

* Elija entre:

   * **[!UICONTROL Informe de asignaciones]**

      * Genere un informe para el sitio, el usuario o el grupo de la comunidad y la asignación seleccionados.
   * **[!UICONTROL Informe de anuncios]**

      * Genere un informe para el sitio de la comunidad, el tipo de contenido y el período de tiempo seleccionados.
   * **[!UICONTROL Informe de vistas]**

      * genere un informe para el sitio de la comunidad, el tipo de contenido y el período de tiempo seleccionados.



![informes](assets/reports1.png)

## Informe de vistas {#views-report}

La consola Vistas permite que las funciones de la comunidad generen informes sobre las vistas de página durante un período de tiempo determinado.

![view-report](assets/view-report.png)

Seleccione los criterios del informe:

* **[!UICONTROL Sitio]**

   Seleccione un sitio de comunidad.

* **[!UICONTROL Tipo de contenido]**

   Puede elegir Todo el contenido o seleccionar una de las funciones presentes en el sitio.

* **[!UICONTROL Lapso de tiempo]**

   Seleccione una de las siguientes opciones:

   * Últimos 7 días
   * Últimos 30 días
   * Últimos 90 días
   * Año pasado

Select **[!UICONTROL Generar]** para crear el informe.

![generate-views](assets/generate-views.png)

## Informe de anuncios {#posts-report}

La consola Anuncios permite generar informes sobre el número de anuncios a las funciones de la comunidad durante un período de tiempo determinado.

![post-report](assets/posts-report.png)

Seleccione los criterios del informe:

* **[!UICONTROL Sitio]**

   Seleccione un sitio de comunidad.

* **[!UICONTROL Tipo de contenido]**

   Puede elegir Todo el contenido o seleccionar una de las funciones presentes en el sitio.

* **[!UICONTROL Lapso de tiempo]**

   Seleccione una de las siguientes opciones:

   * Últimos 7 días
   * Últimos 30 días
   * Últimos 90 días
   * Año pasado

Select **[!UICONTROL Generar]** para crear el informe.

![generate-report](assets/generate-posts-report.png)

## Solución de problemas {#troubleshooting}

### No hay sitios de la comunidad enumerados {#no-community-sites-listed}

Si no aparece ningún sitio de la comunidad, asegúrese de que Adobe Analytics esté habilitado para un sitio. Si elige informes sobre asignaciones, asegúrese de que la función de asignaciones esté en la estructura del sitio de la comunidad.

### Los informes no se muestran en la instancia de autor de AEM {#reports-do-not-show-in-aem-author-instance}

Si los informes no aparecen en la instancia de AEM Author, compruebe las personalizaciones, como la asignación de URL en la instancia de publicación. Si la asignación de URL solo se realiza en la instancia de publicación de AEM del sitio de comunidades, asegúrese de que lo mismo se haya configurado en la instancia de autor de AEM en **Informe de tendencias del sitio Factoría de componentes sociales** configuración.

![Asignación de URL en AEM Author](assets/sitetrend.png)
