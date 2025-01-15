---
title: Creación de la configuración de exportación de recursos compartidos
description: Siga esta página para obtener más información sobre la exportación de recursos compartidos desde Adobe Experience Manager AEM () para su carga en AEM Mobile.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 576b4567-c7b6-4196-84e7-47e980637540
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# Creación de la configuración de exportación de recursos compartidos{#creating-shared-resources-export-configuration}

{{ue-over-mobile}}

>[!CAUTION]
>
>**Requisito previo**:
>
>Antes de aprender a crear y modificar recursos compartidos, consulte [Sincronización de contenido](/help/mobile/mobile-ondemand-contentsync.md) para comprender los conceptos básicos.

Los usuarios de Adobe Experience Manager AEM () Mobile utilizan la sincronización de contenido para exportar contenido en directo a contenido estático para su uso en aplicaciones móviles y esta exportación se produce cuando el contenido se carga en Mobile On-Demand Services desde AEM Mobile.

La propiedad ***dps-exportTemplate*** mencionada en la tabla anterior define la ruta a las configuraciones de exportación de la aplicación. Establezca esta propiedad para crear y modificar recursos compartidos.

AEM Los siguientes recursos describen la exportación de recursos compartidos desde la interfaz de usuario de para su carga en AEM Mobile.

Los recursos de HTML compartidos permiten que los artículos compartan recursos de HTML que, de lo contrario, se duplicarían para todos los artículos, y pueden incluir iconos, fuentes, JavaScript y css.

La configuración de sincronización de contenido que se encuentra en **&lt;dps-exportTemplate>/dps-HTMLResources>** debe configurarse para exportar todo el contenido y los artículos necesarios para la representación estática de la propiedad en el dispositivo.

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
1. Examine esta ruta *[/etc/contentsync/templates/dps-we-ilimitado-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)* para ver los recursos compartidos de ejemplo.

   Puede ver todas las propiedades necesarias para crear los recursos compartidos, como se muestra en la figura siguiente:

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>Los recursos compartidos deben cargarse o exportarse a AEM Mobile On-demand Services cuando cambie alguno de los recursos compartidos.
