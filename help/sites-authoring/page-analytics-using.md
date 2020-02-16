---
title: Visualización de datos de análisis de la página
seo-title: Visualización de datos de análisis de la página
description: Utilice los datos de análisis de la página para medir la eficacia del contenido de la página.
seo-description: Utilice los datos de análisis de la página para medir la eficacia del contenido de la página.
uuid: 5398a5d5-0239-4194-a403-77f5e6fcd741
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 5d192a48-c86f-4803-bb0d-0411ac7470f5
docset: aem65
legacypath: /content/help/en/experience-manager/6-4/help/sites-authoring/pa-using.html
translation-type: tm+mt
source-git-commit: e3683f6254295e606e9d85e88979feaaea76c42e

---


# Visualización de datos de análisis de la página{#seeing-page-analytics-data}

Utilice los datos de análisis de la página para medir la eficacia del contenido de la página.

## Análisis visible desde la consola {#analytics-visible-from-the-console}

![spad-01](assets/spad-01.png)

Los datos de análisis de la página se muestran en [Vista de lista](/help/sites-authoring/basic-handling.md#list-view) de la consola Sitios. Cuando las páginas se muestran en forma de lista, las columnas siguientes están disponibles de forma predeterminada:

* Vistas de la página
* Visitantes únicos
* Tiempo empleado en la página

Cada columna muestra un valor para el período de notificación actual, y también indica si el valor ha aumentado o disminuido desde el período de notificación anterior. Los datos que ve se actualizan cada 12 horas.

>[!NOTE]
>
>Para cambiar el período de actualización, [configure el intervalo de importación](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval).

1. Open the **Sites** console; for example [https://localhost:4502/sites.html/content](https://localhost:4502/sites.html/content)
1. En el extremo derecho de la barra de herramientas (esquina superior derecha), pulse o haga clic en el icono para seleccionar **Vista de lista** (el icono mostrado dependerá de la [vista actual](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)). 

1. Una vez más, en el extremo derecho de la barra de herramientas (esquina superior derecha), haga clic o pulse el icono y seleccione **Ver configuración**. Se abrirá el diálogo **Configurar columnas**. Realice los cambios necesarios y confírmelos con **Actualizar**.

   ![spad-02](assets/spad-02.png)

### Seleccionar el período de notificación {#selecting-the-reporting-period}

Seleccione el período de notificación para el cual los datos de análisis aparecen en la consola Sitios:

* Datos de los últimos 30 días
* Datos de los últimos 90 días
* Datos de este año

El período de notificación actual aparece en la barra de herramientas de la consola Sitios (en la parte derecha de la barra de herramientas superior). Utilice el menú desplegable para seleccionar el período de notificación requerido.

![aa-05](assets/aa-05.png)

### Configuración de las columnas de datos disponibles {#configuring-available-data-columns}

Los miembros del grupo de usuarios de administradores analíticos pueden configurar la consola de Sitios para permitir que los autores vean las columnas de Analytics adicionales.

>[!NOTE]
>
>Cuando un árbol de páginas contiene elementos secundarios asociados a distintas configuraciones de la nube de Adobe Analytics, no puede configurar las columnas de datos disponibles para las páginas.

1. In List View, use the view selectors (right of toolbar), select **View Settings** and then **Add Custom Analytics Data**.

   ![spad-03](assets/spad-03.png)

1. Seleccione las métricas que quiera exponer a los autores en la consola de Sitios y haga clic en **Agregar**.

   Las columnas que aparecen se recuperan de Adobe Analytics.

   ![aa-16](assets/aa-16.png)

### Abrir la información del contenido desde Sitios {#opening-content-insights-from-sites}

Open [Content Insight](/help/sites-authoring/content-insights.md) from the Sites console to further investigate page effectiveness.

1. En la consola de Sitios, seleccione la página en la cual quiera ver la información del contenido.
1. En la barra de herramientas, haga clic en el icono de análisis y recomendaciones.

   ![](do-not-localize/chlimage_1-14.png)

## Análisis visible desde el editor de páginas (mapa de actividad) {#analytics-visible-from-the-page-editor-activity-map}

>[!CAUTION]
>
>Debido a los cambios de seguridad de la API de Adobe Analytics, ya no es posible utilizar la versión de Activity Map incluida en AEM.
>
>The [ActivityMap plugin provided by Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) should now be used.
