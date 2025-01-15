---
title: Configuración del filtro de referente para permitir vacío
description: Más información sobre el Filtro de referente. Para permitir que el Visor de aplicaciones móviles de Adobe Experience Manager AEM () vea aplicaciones en la instancia de autor, debe establecer el filtro de referente de HTML en Permitir vacío.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# Configuración del filtro de referente para permitir vacío{#setting-your-referrer-filter-to-allow-empty}

{{ue-over-mobile}}

Para permitir que el Visor de aplicaciones móviles de Adobe Experience Manager AEM () vea aplicaciones en la instancia de autor, debe establecer el filtro de referente de HTML en Permitir vacío.

Si no tiene intención de utilizar el Visor de aplicaciones para revisar las aplicaciones en los estados de desarrollo y ensayo, no es necesario cambiar la configuración predeterminada del filtro de referente.

AEM Dentro de la instancia de autor de la ejecución de la aplicación, navegue hasta: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) y busque &quot;Filtro de referente de Apache Sling&quot;. Haga clic para editar el filtro de remitente del reenvío y marque la casilla de verificación &quot;permitir vacío&quot; (ver la siguiente imagen). A continuación, pulse el botón Guardar y cierre la página del explorador.

![Configuración del filtro de referente](assets/chlimage_1-106.png)
