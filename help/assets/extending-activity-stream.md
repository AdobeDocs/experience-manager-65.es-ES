---
title: Integrar recursos con flujo de actividades
description: Describe las funciones de grabación de AEM y cómo configurar AEM para que registre eventos específicos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Integrar recursos con flujo de actividades {#integrating-assets-with-activity-stream}

Los usuarios de Recursos Adobe Experience Manager (AEM) realizan muchas acciones como crear, cargar y eliminar recursos. Estas acciones se pueden registrar para que pueda proporcionar un historial de lo que ha hecho un usuario. En esta sección se describen las funciones de grabación de AEM y cómo configurar AEM para grabar eventos específicos.

## Consideraciones de rendimiento y comportamiento predeterminado {#performance-considerations-and-default-behavior}

Esta integración podría requerir CPU y espacio en disco, por ejemplo, al realizar una importación masiva. Por estos motivos, la integración de Recursos AEM con el flujo de actividades está deshabilitada de forma predeterminada.

## Eventos de acción admitidos {#supported-action-events}

Se pueden configurar los siguientes eventos para que se registren:

* Licencia aceptada (ACEPTADA)
* Recurso creado (ASSET_CREATED)
* Recurso movido (ASSET_MOVED)
* Recurso quitado (ASSET_REMOVED)
* Licencia rechazada (RECHAZADA)
* Recurso descargado (DESCARGADO)
* Recurso con versión (VERSIONADO)
* Versión de recurso restaurada (RESTAURADA)
* Metadatos de recurso actualizados (METADATA_UPDATED)
* Recurso publicado en un sistema externo (PUBLISHED_EXTERNAL)
* Actualización original del recurso (ORIGINAL_UPDATED)
* Se ha actualizado la representación de recursos (RENDITION_UPDATED)
* Representación de recursos eliminada (RENDITION_REMOVED)
* Subrecurso actualizado (SUBASSET_UPDATED)
* Subrecurso eliminado (SUBASSET_REMOVED)

## Configuración del registro de eventos de AEM Assets {#configuring-aem-assets-events-recording}

La consola [](/help/sites-deploying/configuring-osgi.md) web permite acceder al ajuste del grabador de eventos de AEM Assets. Para configurar el grabador de eventos de AEM Assets, realice las acciones siguientes:

1. Navegar a la consola **[!UICONTROL web]**

1. Haga clic en **[!UICONTROL Configuración]**.

1. Haga doble clic en Grabador **[!UICONTROL de eventos de CQ DAM]** de día.

1. Marque **[!UICONTROL Habilita este servicio]**.

1. Compruebe qué tipos **[!UICONTROL de]** eventos desea registrar en el flujo de actividad del usuario.

1. Haga clic en **[!UICONTROL Guardar]**.

## Leer eventos grabados {#reading-recorded-events}

Los eventos registrados se almacenan como actividades. Puede leerlos mediante programación mediante la API [de](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html)Activity Manager.
