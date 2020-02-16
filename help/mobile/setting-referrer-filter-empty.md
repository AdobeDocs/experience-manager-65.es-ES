---
title: Configuración del filtro de referente para permitir que esté vacío
seo-title: Configuración del filtro de referente para permitir que esté vacío
description: Siga esta página para conocer el filtro de referente. Para permitir que el visor de aplicaciones de AEM Mobile vea las aplicaciones en la instancia de autor, deberá establecer el filtro de referente HTML en 'permitir vacío'.
seo-description: Siga esta página para conocer el filtro de referente. Para permitir que el visor de aplicaciones de AEM Mobile vea las aplicaciones en la instancia de autor, deberá establecer el filtro de referente HTML en 'permitir vacío'.
uuid: 4fb0f95c-ac8f-4a14-8c46-6616d9d4f380
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 8fb7d088-94bf-4799-98b3-8fa58eef83df
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuración del filtro de referente para permitir que esté vacío{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Para permitir que el visor de aplicaciones de AEM Mobile vea las aplicaciones en la instancia de autor, deberá establecer el filtro de referente HTML en &#39;permitir vacío&#39;.

Si no tiene intención de utilizar el visor de aplicaciones para revisar las aplicaciones dentro de los estados de desarrollo y ensayo, no necesita cambiar la configuración predeterminada del filtro de referente.

En la instancia de creación de AEM en ejecución, vaya a: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) y busque &#39;Apache Sling Referrer Filter&#39;. Haga clic para editar el filtro del referente y marque la casilla &#39;Permitir vacío&#39; (ver imagen a continuación). A continuación, pulse el botón save (guardar) y cierre la página del explorador.

![Configuración del filtro de referente](assets/chlimage_1-106.png)
