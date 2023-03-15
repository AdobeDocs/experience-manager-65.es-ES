---
title: Creación de la configuración de exportación de recursos compartidos
seo-title: Creating Shared Resources Export Configuration
description: Siga esta página para obtener más información sobre la exportación de recursos compartidos desde Adobe Experience Manager AEM () para su carga en AEM Mobile.
seo-description: Follow this page to learn about exporting shared resources from Adobe Experience Manager (AEM) for upload to AEM Mobile.
uuid: 99b8ff94-8135-4643-a15b-aa6fb91f5401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 1edf6c76-ccb1-40b6-bdf6-924f1461cd28
exl-id: 576b4567-c7b6-4196-84e7-47e980637540
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---

# Creación de la configuración de exportación de recursos compartidos{#creating-shared-resources-export-configuration}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran procesamiento del lado del cliente basado en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**Requisitos previos**:
>
>Antes de aprender a crear y modificar recursos compartidos, consulte [Sincronización de contenido](/help/mobile/mobile-ondemand-contentsync.md) para comprender los conceptos básicos.

Los usuarios de AEM Mobile utilizan la sincronización de contenido para exportar contenido en directo a contenido estático para su uso en aplicaciones móviles. Esta exportación se produce cuando el contenido se carga en Mobile On-Demand Services desde AEM Mobile.

La propiedad ***dps-exportTemplate*** mencionado en la tabla anterior, define la ruta a las configuraciones de exportación de la aplicación. Establezca esta propiedad para crear y modificar recursos compartidos.

En los siguientes recursos se describe la exportación de recursos compartidos desde Adobe Experience Manager AEM () para su carga en AEM Mobile.

Recursos de HTML compartidos permite que los artículos compartan recursos de HTML que, de lo contrario, necesitarían duplicarse para todos los artículos y pueden incluir iconos, fuentes, javascript y css.

La configuración de sincronización de contenido se encuentra en **&lt;dps-exporttemplate>/dps-HTMLResources>** debe configurarse para exportar todo el contenido y los artículos necesarios para la propiedad de procesamiento estático en el dispositivo.

>[!CAUTION]
>
>Puede realizar los pasos siguientes para ver recursos compartidos de ejemplo, solo si tiene lo siguiente:
>
>* instaló el contenido de muestra
>* AEM instancia de ejecución
>* no hay contexto personalizado configurado ni puerto diferente
>


Para ver un ejemplo de recurso compartido, consulte los pasos a continuación:

1. Abra el CRXDE Lite AEM en el servidor de la.
1. Examinar esta ruta *[/etc/contentsync/templates/dps-we-ilimitado-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)*, para ver los recursos compartidos de ejemplo.

   Puede ver todas las propiedades necesarias para crear los recursos compartidos, como se muestra en la figura siguiente:

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>Los recursos compartidos deben cargarse o exportarse a AEM Mobile On-demand Services cuando cambie alguno de los recursos compartidos.
