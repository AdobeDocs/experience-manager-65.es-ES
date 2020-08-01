---
title: ' [!DNL Assets] Integración con flujo de actividad.'
description: Describe las funciones [!DNL Experience Manager] de grabación y cómo configurarlas para grabar eventos específicos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# Integración [!DNL Assets] con flujo de actividad {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] los usuarios realizan muchas acciones como crear, cargar y eliminar recursos. Estas acciones se pueden registrar para que pueda proporcionar un historial de lo que ha hecho un usuario. En esta sección se describen las funciones de grabación [!DNL Experience Manager] y cómo configurarlas [!DNL Experience Manager] para grabar eventos específicos.

## Consideraciones de rendimiento y comportamiento predeterminado {#performance-considerations-and-default-behavior}

Esta integración podría requerir CPU y espacio en disco, por ejemplo, al realizar una importación masiva. Por estos motivos, la [!DNL Assets] integración con el flujo de Actividad está deshabilitada de forma predeterminada.

## eventos de acción admitidos {#supported-action-events}

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

## Configurar la grabación de [!DNL Assets] eventos {#configuring-aem-assets-events-recording}

La consola [](/help/sites-deploying/configuring-osgi.md) web proporciona acceso al ajuste del grabador de Evento de recursos. Para configurar el grabador de Evento de recursos, siga estos pasos:

1. Navegar a la consola **[!UICONTROL web]**

1. Haga clic en **[!UICONTROL Configuración]**.

1. Doble haga clic en **[!UICONTROL Día de CQ DAM Evento Grabador]**.

1. Marque **[!UICONTROL Habilita este servicio]**.

1. Compruebe qué **[!UICONTROL Tipos de evento]** desea que se registren en el flujo de actividad del usuario.

1. Haga clic en **[!UICONTROL Guardar]**.

## Leer eventos grabados {#reading-recorded-events}

Los eventos registrados se almacenan como actividades. Puede leerlos mediante programación mediante la API [de](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html)Activity Manager.
