---
title: Configuración del filtro de referente para permitir vacío
description: Más información sobre el Filtro de referente. Para permitir que el Visor de aplicaciones móviles de Adobe Experience Manager AEM () vea aplicaciones en la instancia de autor, debe establecer el filtro de referente de HTML en Permitir vacío.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
source-git-commit: 6799f1d371734b69c547f3c0c68e1e633aa63229
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 3%

---

# Configuración del filtro de referente para permitir vacío{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran una representación del lado del cliente basada en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Para permitir que el Visor de aplicaciones móviles de Adobe Experience Manager AEM () vea aplicaciones en la instancia de autor, debe establecer el filtro de referente de HTML en Permitir vacío.

Si no tiene intención de utilizar el Visor de aplicaciones para revisar las aplicaciones en los estados de desarrollo y ensayo, no es necesario cambiar la configuración predeterminada del filtro de referente.

AEM En la instancia de autor de la ejecución de, vaya a: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) y busque &quot;Filtro de referente de Apache Sling&quot;. Haga clic para editar el filtro de remitente del reenvío y marque la casilla de verificación &quot;permitir vacío&quot; (ver la siguiente imagen). A continuación, pulse el botón Guardar y cierre la página del explorador.

![Configuración del filtro de referente](assets/chlimage_1-106.png)
