---
title: Creación de la configuración de exportación de artículos
seo-title: Creating Article Export Configuration
description: Siga esta página para obtener más información sobre la exportación de contenido desde Adobe Experience Manager (AEM) para cargarlo en AEM Mobile.
seo-description: Follow this page to learn about exporting content from Adobe Experience Manager (AEM) for upload to AEM Mobile.
uuid: 089bc15b-669e-4623-bdbb-fd9abf46e098
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: bc681589-5d46-44cd-888d-b0722a2fd006
exl-id: 5295f383-3b46-4456-9177-65de68e39a85
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 1%

---

# Creación de la configuración de exportación de artículos{#creating-article-export-configuration}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**Requisitos previos**:
>
>Antes de obtener información sobre la creación y modificación de recursos compartidos, consulte [Sincronización de contenido](/help/mobile/mobile-ondemand-contentsync.md) para comprender los conceptos básicos.

Los usuarios de AEM Mobile utilizan la sincronización de contenido para exportar contenido en directo a contenido estático para utilizarlo en aplicaciones móviles. Esta exportación se produce cuando el contenido se carga en Mobile On-Demand Services desde AEM Mobile.

La propiedad ***dps-exportTemplate*** mencionado en la tabla anterior, define la ruta a las configuraciones de exportación de la aplicación. Establezca esta propiedad para crear y modificar recursos compartidos.

En los siguientes recursos se describe la exportación de contenido desde Adobe Experience Manager (AEM) para cargarlo en AEM Mobile.

Los artículos tienen contenido que debe exportarse y cargarse. Parte de este contenido se puede compartir entre Artículos.

Uso [ContentSync](/help/mobile/mobile-ondemand-contentsync.md) para recopilar el contenido y crear un ***Recursos compartidos*** paquete.

La configuración de ContentSync que se encuentra en **&lt;dps-exporttemplate>/dps-article>** debe configurarse para exportar todo el contenido que se necesita en un artículo para la representación estática de la propiedad en el dispositivo.

>[!CAUTION]
>
>Puede realizar los pasos siguientes para ver recursos compartidos de ejemplo, solo si tiene:
>
>* se ha instalado el contenido de ejemplo
>* ejecución de AEM instancia
>* no hay contexto personalizado configurado o un puerto diferente
>


Para ver un recurso compartido de ejemplo, consulte los pasos a continuación:

1. Abra el CRXDE Lite en el servidor AEM.
1. Vaya a esta ruta [/etc/contentsync/templates/dps-we-limited-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article), para ver los recursos compartidos de ejemplo.

   Puede ver todas las propiedades necesarias para crear los recursos compartidos, como se muestra en la figura siguiente:

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>Los artículos deben cargarse o exportarse a AEM Mobile On-demand Services cuando cambia el contenido de un artículo.
