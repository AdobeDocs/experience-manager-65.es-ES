---
title: Integrar [!DNL Assets] con flujo de actividad
description: Describe las capacidades de grabación de [!DNL Experience Manager] y cómo configurarlo para registrar eventos específicos.
contentOwner: AG
role: Developer
feature: Asset Management
exl-id: 2a08a7c1-8be9-42d1-9983-f9c8b12ea4e8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# Integrar [!DNL Assets] con flujo de actividad {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] Los usuarios de realizan muchas acciones, como crear, cargar y eliminar recursos. Estas acciones se pueden registrar para que pueda proporcionar un historial de lo que ha hecho un usuario. En esta sección se describen las capacidades de grabación de [!DNL Experience Manager] y cómo configurar [!DNL Experience Manager] para registrar eventos específicos.

## Consideraciones de rendimiento y comportamiento predeterminado {#performance-considerations-and-default-behavior}

Esta integración podría consumir CPU y espacio en disco, por ejemplo, al realizar una importación masiva. Por estas razones, la variable [!DNL Assets] La integración con el flujo de actividad está desactivada de forma predeterminada.

## Eventos de acción admitidos {#supported-action-events}

Se pueden configurar los siguientes eventos para registrarlos:

* Licencia aceptada (ACEPTADA)
* Recurso creado (ASSET_CREATED)
* Recurso movido (ASSET_MOVED)
* Recurso eliminado (ASSET_REMOVED)
* Licencia rechazada (RECHAZADA)
* Recurso descargado (DESCARGADO)
* Recurso con versión (VERSIONED)
* Versión del recurso restaurada (RESTAURADA)
* Metadatos de los recursos actualizados (METADATA_UPDATED)
* Recurso publicado en un sistema externo (PUBLISHED_EXTERNAL)
* Actualización del original del recurso (ORIGINAL_UPDATED)
* Representación de recursos actualizada (RENDITION_UPDATED)
* Representación de recursos eliminada (RENDITION_REMOVED)
* Subrecurso actualizado (SUBASSET_UPDATED)
* Subrecurso eliminado (SUBASSET_REMOVED)

## Configurar [!DNL Assets] grabación de eventos {#configuring-aem-assets-events-recording}

El [consola web](/help/sites-deploying/configuring-osgi.md) proporciona acceso al ajuste del grabador de eventos de Assets. Para configurar el registrador de eventos de Assets, siga estos pasos:

1. Vaya a **[!UICONTROL Consola web]**

1. Clic **[!UICONTROL Configuración]**.

1. Doble clic **[!UICONTROL Grabador de eventos de CQ DAM de día]**.

1. Marque **[!UICONTROL Habilita este servicio]**.

1. Compruebe qué **[!UICONTROL Tipos de eventos]** desea que se registre en el flujo de actividad del usuario.

1. Haga clic en **[!UICONTROL Guardar]**.

## Leer eventos grabados {#reading-recorded-events}

Los eventos registrados se almacenan como actividades. Puede leerlas mediante programación utilizando el [API de Activity Manager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
