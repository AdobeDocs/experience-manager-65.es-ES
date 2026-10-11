---
title: Configuración del filtro de referente para permitir vacío
description: Más información sobre el Filtro de referente. Para permitir que el visualizador de aplicaciones móviles de Adobe Experience Manager (AEM) vea aplicaciones en su instancia de autor, debe establecer el filtro de referente de HTML en "permitir vacío".
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
solution: Experience Manager
feature: Mobile
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 3%
---
# Configuración del filtro de referente para permitir vacío{#setting-your-referrer-filter-to-allow-empty}

{{ue-over-mobile}}

Para permitir que el visualizador de aplicaciones móviles de Adobe Experience Manager (AEM) vea aplicaciones en su instancia de autor, debe establecer el filtro de referente de HTML en &quot;permitir vacío&quot;.

Si no tiene intención de utilizar el Visor de aplicaciones para revisar las aplicaciones en los estados de desarrollo y ensayo, no es necesario cambiar la configuración predeterminada del filtro de referente.

En la instancia de autor de AEM que está ejecutando, vaya a: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) y busque &quot;Filtro de referente de Apache Sling&quot;. Haga clic para editar el filtro de remitente del reenvío y marque la casilla de verificación &quot;permitir vacío&quot; (ver la siguiente imagen). A continuación, pulse el botón Guardar y cierre la página del explorador.

![Configuración del filtro de referente](assets/chlimage_1-106.png)
