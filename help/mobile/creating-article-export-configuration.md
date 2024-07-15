---
title: Creando configuración de exportación del artículo
description: Siga esta página para obtener más información sobre la exportación de contenido desde Adobe Experience Manager AEM () para su carga en AEM Mobile.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 5295f383-3b46-4456-9177-65de68e39a85
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Creando configuración de exportación del artículo{#creating-article-export-configuration}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran una representación del lado del cliente basada en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**Requisito previo**:
>
>Antes de aprender a crear y modificar recursos compartidos, consulta [Sincronización de contenido](/help/mobile/mobile-ondemand-contentsync.md) para comprender los conceptos básicos.

Los usuarios de AEM Mobile utilizan la sincronización de contenido para exportar contenido en directo a contenido estático para su uso en aplicaciones móviles. Esta exportación se produce cuando el contenido se carga en Mobile On-Demand Services desde AEM Mobile.

La propiedad ***dps-exportTemplate*** mencionada en la tabla anterior define la ruta a las configuraciones de exportación de la aplicación. Establezca esta propiedad para crear y modificar recursos compartidos.

En los siguientes recursos se describe la exportación de contenido desde Adobe Experience Manager AEM () para su carga en AEM Mobile.

Los artículos tienen contenido que debe exportarse y cargarse. Parte de este contenido se puede compartir entre artículos.

Use [ContentSync](/help/mobile/mobile-ondemand-contentsync.md) para reunir el contenido y crear un paquete de ***Recursos compartidos***.

La configuración de ContentSync encontrada en **&lt;dps-exportTemplate>/dps-article>** debe configurarse para exportar todo el contenido y el artículo necesarios para la representación estática de la propiedad en el dispositivo.

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
1. Vaya a esta ruta [/etc/contentsync/templates/dps-we-ilimitado-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article) para ver los recursos compartidos de ejemplo.

   Puede ver todas las propiedades necesarias para crear los recursos compartidos, como se muestra en la figura siguiente:

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>Los artículos deben cargarse o exportarse a AEM Mobile On-demand Services cuando cambie el contenido de uno de ellos.
