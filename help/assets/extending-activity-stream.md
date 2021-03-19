---
title: Integrar [!DNL Assets] con el flujo de actividad
description: Describe las capacidades de grabación de [!DNL Experience Manager] y cómo configurarlo para registrar eventos específicos.
contentOwner: AG
role: Desarrollador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 1%

---


# Integrar [!DNL Assets] con el flujo de actividad {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] Los usuarios realizan muchas acciones, como crear, cargar y eliminar recursos. Estas acciones se pueden registrar para que pueda proporcionar un historial de lo que ha hecho un usuario. En esta sección se describen las capacidades de registro de [!DNL Experience Manager] y cómo configurar [!DNL Experience Manager] para registrar eventos específicos.

## Consideraciones de rendimiento y comportamiento predeterminado {#performance-considerations-and-default-behavior}

Esta integración podría requerir CPU y espacio en disco, por ejemplo, al realizar importaciones masivas. Por estos motivos, la integración [!DNL Assets] con el flujo de actividad está deshabilitada de forma predeterminada.

## Eventos de acción admitidos {#supported-action-events}

Se pueden configurar los siguientes eventos para que se registren:

* Licencia aceptada (ACEPTADA)
* Recurso creado (ASSET_CREATED)
* Recurso movido (ASSET_MOVED)
* Recurso quitado (ASSET_REMOVED)
* Licencia rechazada (RECHAZADA)
* Recurso descargado (DESCARGADO)
* Recurso con versión (VERSIONADO)
* Versión del recurso restaurada (RESTAURADA)
* Actualización de metadatos de recursos (METADATA_UPDATED)
* Recurso publicado en un sistema externo (PUBLISHED_EXTERNAL)
* Actualización original del recurso (ORIGINAL_UPDATED)
* Actualización de la representación de recursos (RENDITION_UPDATED)
* Representación de recursos eliminada (RENDITION_REMOVED)
* Subrecurso actualizado (SUBASSET_UPDATED)
* Subrecurso eliminado (SUBASSET_REMOVED)

## Configurar el registro de eventos [!DNL Assets] {#configuring-aem-assets-events-recording}

La [consola web](/help/sites-deploying/configuring-osgi.md) proporciona acceso al ajuste del grabador de eventos de recursos. Para configurar el grabador de eventos de recursos, siga estos pasos:

1. Vaya a la **[!UICONTROL Consola Web]**

1. Haga clic en **[!UICONTROL Configuration]**.

1. Haga doble clic **[!UICONTROL Day CQ DAM Event Recorder]**.

1. Comprobar **[!UICONTROL Habilita este servicio]**.

1. Compruebe qué **[!UICONTROL Tipos de eventos]** desea registrar en el flujo de actividad del usuario.

1. Haga clic en **[!UICONTROL Guardar]**.

## Leer eventos registrados {#reading-recorded-events}

Los eventos registrados se almacenan como actividades. Puede leerlos mediante programación mediante la [API de Activity Manager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
