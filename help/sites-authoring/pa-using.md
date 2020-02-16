---
title: Visualización de datos de análisis de la página
seo-title: Visualización de datos de análisis de la página
description: Utilice los datos de análisis de la página para medir la eficacia del contenido de la página.
seo-description: Utilice los datos de análisis de la página para medir la eficacia del contenido de la página.
uuid: 8dda89be-13e3-4a13-9a44-0213ca66ed9c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 42d2195a-1327-45c0-a14c-1cf5ca196cfc
translation-type: tm+mt
source-git-commit: e3683f6254295e606e9d85e88979feaaea76c42e

---


# Visualización de datos de análisis de la página{#seeing-page-analytics-data}

Utilice los datos de análisis de la página para medir la eficacia del contenido de la página.

## Análisis visible desde la consola {#analytics-visible-from-the-console}

![aa-10](assets/aa-10.png)

Los datos de análisis de la página se muestran en [Vista de lista](/help/sites-authoring/basic-handling.md#list-view) de la consola Sitios. Cuando las páginas se muestran en forma de lista, las columnas siguientes están disponibles de forma predeterminada:

* Vistas de la página
* Visitantes únicos
* Tiempo empleado en la página

Cada columna muestra un valor para el período de notificación actual, y también indica si el valor ha aumentado o disminuido desde el período de notificación anterior. Los datos que ve se actualizan cada 12 horas.

>[!NOTE]
>
>Para cambiar el período de actualización, [configure el intervalo de importación](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval).

1. Abra la consola **Sitios**; por ejemplo, [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)
1. En el extremo derecho de la barra de herramientas (esquina superior derecha), pulse o haga clic en el icono para seleccionar **Vista de lista** (el icono mostrado dependerá de la [vista actual](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)). 

1. Una vez más, en el extremo derecho de la barra de herramientas (esquina superior derecha), haga clic o pulse el icono y seleccione **Ver configuración**. Se abrirá el diálogo **Configurar columnas**. Realice los cambios necesarios y confírmelos con **Actualizar**.

   ![aa-04](assets/aa-04.png)

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

   ![aa-15](assets/aa-15.png)

1. Seleccione las métricas que quiera exponer a los autores en la consola de Sitios y haga clic en **Agregar**.

   Las columnas que aparecen se recuperan de Adobe Analytics.

   ![aa-16](assets/aa-16.png)

### Abrir la información del contenido desde Sitios {#opening-content-insights-from-sites}

Open [Content Insight](/help/sites-authoring/content-insights.md) from the Sites console to further investigate page effectiveness.

1. En la consola de Sitios, seleccione la página en la cual quiera ver la información del contenido.
1. En la barra de herramientas, haga clic en el icono de análisis y recomendaciones.

   ![](do-not-localize/chlimage_1-16a.png)

## Análisis visible desde el editor de páginas (mapa de actividad) {#analytics-visible-from-the-page-editor-activity-map}

>[!NOTE]
>
>Se mostrará si el [mapa de actividad se ha configurado](/help/sites-administering/adobeanalytics-connect.md#configuring-for-the-activity-map) para el sitio web.

>[!NOTE]
>
>Los datos del mapa de actividad se toman de Adobe Analytics.

Cuando el sitio web se haya [configurado para Adobe Analytics](/help/sites-administering/adobeanalytics-connect.md), puede utilizar el [modo Mapa de actividad](/help/sites-authoring/author-environment-tools.md#page-modes) para ver los datos relevantes. Por ejemplo:

![aa-07](assets/aa-07.png)

### Acceso al mapa de actividad {#accessing-the-activity-map}

Después de seleccionar el modo [Mapa de actividad](/help/sites-authoring/author-environment-tools.md#page-modes), se le solicitará que introduzca las credenciales de Adobe Analytics.

![aa-03](assets/aa-03.png)

Se muestra la barra de herramientas flotante de **Analytics**; aquí puede:

* cambiar el formato de la barra de herramientas con las dos flechas (**>>**};)
* alternar los detalles la de página (icono con forma de ojo)};
* establecer la configuración del mapa de actividad (icono con forma de engranaje)};
* seleccionar el análisis que quiere mostrar (varios selectores desplegables)};
* salir del mapa de actividad y cerrar la barra de herramientas (x).

![aa-09](assets/aa-09.png)

### Selección del análisis que se va a mostrar {#selecting-the-analytics-to-show}

Puede seleccionar los datos analíticos que se van a mostrar y el modo en que aparecerán mediante diversos criterios:

* **Estándar**/**En directo**

* tipo de evento
* grupo de usuarios
* **Burbujas**/**Degradado**/**Ganadores y perdedores**/**Desactivado**

* período que se va a mostrar

![aa-13](assets/aa-13.png)

### Configuración del mapa de actividad {#configuring-the-activity-map}

Utilice el icono **Mostrar configuración** para abrir el cuadro de diálogo **Configuración del mapa de actividad**.

![aa-04-1](assets/aa-04-1.png)

El cuadro de diálogo **Configuración del mapa de actividad** proporciona una gama de opciones en tres fichas:

![aa-06](assets/aa-06.png)

* General

   * Grupo de informes
   * Nombre de página
   * Idioma
   * Superposiciones de etiquetas con
   * Tamaño del tipo de letra de la etiqueta
   * Color de degradado
   * Color de burbuja
   * Degradación de color según
   * Transparencia de degradación

* Estándar

   * Visualización (tipo y número de vínculos)
   * Oculte las superposiciones de los vínculos que no hayan recibido ninguna visita

* En directo

   * Mostrar principales (ganadores o perdedores
   * Excluir inferior %
   * Actualización automática (datos y punto)

