---
title: Configuración del filtro de referente para permitir que esté vacío
seo-title: Setting Your Referrer Filter to Allow Empty
description: Siga esta página para obtener más información sobre el filtro de referente. Para permitir que el visualizador de aplicaciones de AEM Mobile vea aplicaciones en la instancia de autor, deberá establecer el filtro de referente de HTML en "permitir vacío".
seo-description: Follow this page to learn about Referrer Filter. In order to allow the AEM Mobile Application Viewer to view apps on your Author instance, you'll need to set your HTML referrer filter to 'allow empty'.
uuid: 4fb0f95c-ac8f-4a14-8c46-6616d9d4f380
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 8fb7d088-94bf-4799-98b3-8fa58eef83df
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 3%

---

# Configuración del filtro de referente para permitir que esté vacío{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Para permitir que el visualizador de aplicaciones de AEM Mobile vea aplicaciones en la instancia de autor, deberá establecer el filtro de referente de HTML en &quot;permitir vacío&quot;.

Si no tiene intención de usar el Visor de aplicaciones para revisar aplicaciones dentro de los estados de desarrollo y ensayo, no necesita cambiar la configuración predeterminada del filtro de remitente del reenvío.

Dentro de la instancia de autor de AEM en ejecución, vaya a: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) y busque &quot;Filtro de referente de Apache Sling&quot;. Haga clic en para editar el filtro del referente y marque la casilla &quot;Permitir vacío&quot; (consulte la imagen siguiente). A continuación, pulse el botón Guardar y cierre la página del explorador.

![Configuración del filtro de referente](assets/chlimage_1-106.png)
