---
title: Creación de la configuración de exportación de artículos
seo-title: Creación de la configuración de exportación de artículos
description: Siga esta página para obtener información sobre la exportación de contenido desde Adobe Experience Manager (AEM) para cargarlo en AEM Mobile.
seo-description: Siga esta página para obtener información sobre la exportación de contenido desde Adobe Experience Manager (AEM) para cargarlo en AEM Mobile.
uuid: 089bc15b-669e-4623-bdbb-fd9abf46e098
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: bc681589-5d46-44cd-888d-b0722a2fd006
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Creación de la configuración de exportación de artículos{#creating-article-export-configuration}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**Requisitos previos**:
>
>Antes de aprender a crear y modificar recursos compartidos, consulte Sincronización [de contenido](/help/mobile/mobile-ondemand-contentsync.md) para comprender los conceptos básicos.

Los usuarios de AEM Mobile utilizan la sincronización de contenido para exportar contenido en directo a contenido estático y utilizarlo en aplicaciones móviles. Esta exportación se produce cuando el contenido se carga en Mobile On-Demand Services desde AEM Mobile.

La propiedad ***dps-exportTemplate*** mencionada en la tabla anterior define la ruta a las configuraciones de exportación de la aplicación. Establezca esta propiedad para crear y modificar recursos compartidos.

Los siguientes recursos describen la exportación de contenido desde Adobe Experience Manager (AEM) para cargarlo en AEM Mobile.

Los artículos tienen contenido que se debe exportar y cargar. Parte de este contenido se puede compartir entre artículos.

Utilice [ContentSync](/help/mobile/mobile-ondemand-contentsync.md) para reunir el contenido y crear un paquete de recursos ****** compartidos.

La configuración de ContentSync que se encuentra en **&lt;dps-exportTemplate>/dps-article>** debe configurarse para exportar todo el contenido que un artículo requiere para la representación estática de propiedades en el dispositivo.

>[!CAUTION]
>
>Puede realizar los pasos siguientes para ver los recursos compartidos de muestra, solo si tiene:
>
>* se instaló el contenido de muestra
>* ejecución de una instancia de AEM
>* no hay contexto personalizado configurado o un puerto diferente
>



Para ver un recurso compartido de muestra, consulte los pasos siguientes:

1. Abra CRXDE Lite en su servidor AEM.
1. Vaya a esta ruta [/etc/contentsync/templates/dps-we-less-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article)para ver los recursos compartidos de muestra.

   Puede ver todas las propiedades necesarias para crear los recursos compartidos, como se muestra en la figura siguiente:

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>Los artículos deben cargarse o exportarse a On-Demand Services de AEM Mobile cuando cambie el contenido de los artículos.

